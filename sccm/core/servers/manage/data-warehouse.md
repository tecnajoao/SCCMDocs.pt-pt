---
title: "Armazém de dados | Microsoft Docs"
description: "Ponto de serviço do armazém de dados e base de dados para o System Center Configuration Manager"
ms.custom: na
ms.date: 8/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 744614d7e1ec97a4d4b4646c45cb41d734c6be34
ms.sourcegitcommit: 974fbc4408028c8be28911e5cd646efcf47c7f15
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/28/2017
---
#  <a name="the-data-warehouse-service-point-for-system-center-configuration-manager"></a>O ponto de serviço do armazém de dados para o System Center Configuration Manager
*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir da versão 1702 que pode utilizar o ponto de serviço do armazém de dados para armazenar e elaborar relatórios sobre dados históricos de longo prazo para a sua implementação do Configuration Manager.

> [!TIP]
> O ponto de serviço do armazém de dados é uma funcionalidade de pré-lançamento introduzida na versão 1702. Para ativá-la, consulte o artigo [utilizar funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features).

> A partir da versão 1706, esta funcionalidade já não é uma funcionalidade de pré-lançamento.

O armazém de dados suporta até 2 TB de dados, com carimbos de registo de alterações. Armazenamento de dados é conseguido ao sincronizações automáticas da base de dados do site do Configuration Manager para a base de dados do armazém de dados. Esta informação, em seguida, é acessível a partir do seu ponto de Reporting Services. Dados que são sincronizados para a base de dados do armazém de dados são mantidos três anos. Periodicamente, uma tarefa incorporada remove os dados que é mais antigos do que três anos.

Dados que são sincronizados incluem o seguinte dos grupos de dados globais e dados do Site:
- Estado de funcionamento da infraestrutura
- Segurança
- Conformidade
- Software maligno   
- Implementações de software
- Detalhes de inventário (no entanto, o histórico de inventário não está sincronizado)

Quando instala a função de sistema de sites, instala e configura a base de dados do armazém de dados. Instala também vários relatórios para que possam procurar facilmente e relatórios sobre estes dados.



## <a name="prerequisites-for-the-data-warehouse-service-point"></a>Pré-requisitos para o ponto de serviço do armazém de dados
- A função de sistema de sites de armazém de dados é suportada apenas no site de nível superior da hierarquia. (Um site de administração central ou site primário autónomo).
- O computador onde instalou a função de sistema de sites requer o .NET Framework 4.5.2 ou posterior.
- A conta de computador do computador onde instalou a função de sistema de sites é utilizada para sincronizar dados com a base de dados do armazém de dados. Esta conta necessita das seguintes permissões:  
  - **Administrador** no computador que alojará a base de dados do armazém de dados.
  - **DB_Creator** permissão na base de dados de armazém de dados.
  - O **DB_owner** ou **DB_reader** com **executar** permissões para os sites de nível superior da base de dados do site.
- A base de dados do armazém de dados requer a utilização do SQL Server 2012 ou posterior. A edição pode ser Standard, Enterprise ou Datacenter.
- As seguintes configurações do SQL Server são suportadas para alojar a base de dados do armazém:  
  - Uma instância predefinida
  - Instância nomeada
  - SQL Server Always On o grupo de disponibilidade
  - Cluster de ativação pós-falha do SQL Server
-   Quando a base de dados do armazém de dados remota da base de dados de servidor do site, tem de ter uma licença separada para cada SQL Server que aloja a base de dados.
- Se utilizar [vistas distribuídas](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews), função de sistema de sites de ponto de dados do armazém serviço tem de instalar no mesmo servidor que aloja a base de dados de site dos sites de administração central.



> [!IMPORTANT]  
> O armazém de dados não é suportado quando o computador que executa o ponto de serviço do armazém de dados ou que aloja a base de dados do armazém de dados é executada uma das seguintes idiomas:
> - JPN – Japonês
> - KOR – Coreano
> - CHS – Chinês simples
> - CHT – Chinês tradicional, este problema será resolvido numa versão futura.


## <a name="install-the-data-warehouse"></a>Instalar o armazém de dados
Cada hierarquia suporta uma única instância desta função, em qualquer sistema de site do site de nível superior. O SQL Server que aloja a base de dados para o armazém pode ser local para a função de sistema de sites ou remoto. Embora o armazém de dados funciona com o ponto do Reporting Services que está instalado no mesmo site, as funções de sistema de dois sites não tem de ser instalado no mesmo servidor.   

Para instalar a função, utilize o **Adicionar Assistente de funções de sistema de Site** ou **criar Assistente de servidor de sistema de Site**. Consulte [instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles) para obter mais informações.  

Quando instalar a função, o Configuration Manager cria a base de dados do armazém de dados para si na instância do SQL Server que especificou. Se especificar o nome da base de dados existente (como iria fazer se a [mover a base de dados do armazém de dados para um novo SQL Server](#move-the-data-warehouse-database)), do Configuration Manager não criar uma nova base de dados, mas em vez disso, utiliza um que especificar.

### <a name="configurations-used-during-installation"></a>Configurações utilizadas durante a instalação
**Seleção da função do sistema** página:  

**Geral** página:
-   **Definições de ligação de base de dados do armazém de dados do Configuration Manager**:
 - **SQL Server nome de domínio completamente qualificado**:  
 Especifique o nome de domínio totalmente qualificado (FQDN) do servidor que aloja a base de dados do ponto de serviço do armazém de dados.
 - **Nome da instância do SQL Server, se aplicável**:   
 Se utilizar uma instância predefinida do SQL Server, tem de especificar a instância.
 - **Nome da base de dados**:   
 Especifique um nome para a base de dados do armazém de dados. O nome de base de dados não pode exceder 10 carateres. (Será possível aumentar o comprimento do nome suportados numa versão futura).
 O Configuration Manager cria a base de dados do armazém de dados com este nome. Se especificar um nome de base de dados que já existe na instância do SQL server, o Configuration Manager utiliza essa base de dados.
 - **Porta do SQL Server utilizada para ligação**:   
 Especifique o número de porta de TCP/IP que está configurado para o SQL Server que aloja a base de dados do armazém de dados. Esta porta é utilizada pelo serviço de sincronização do armazém de dados para ligar à base de dados do armazém de dados.  

**Agenda de sincronização** página:   
- **Agenda de sincronização**:
 - **Hora de início**:  
 Especifique o tempo que pretende que a sincronização do armazém de dados para iniciar.
 - **Padrão de periodicidade**:
    - **Diária**: Especifique que a sincronização é executada diariamente.
    - **Semanalmente**: Especifique um único dia cada semana e a periodicidade semanal para sincronização.

## <a name="reporting"></a>Relatórios
Depois de instalar um ponto de serviço do armazém de dados, vários relatórios fiquem disponíveis no ponto de Reporting Services está instalado no mesmo site. Se instalar o ponto de serviço do armazém de dados antes de instalar um ponto do Reporting Services, os relatórios serão adicionados automaticamente quando, posteriormente, instalar o ponto do Reporting Services.

A função de sistema de sites do armazém de dados inclui os seguintes relatórios, que tem uma categoria de **do armazém de dados**:
 - **Implementação da aplicação - histórica**:   
 Ver os detalhes para a implementação de aplicação para uma aplicação específica e a máquina.
 - **Proteção de ponto final e atualização de Software conformidade - histórica**: Computadores de vista que estão em falta atualizações de software.  
 - **Inventário de Hardware geral - históricos**:   
 Ver todo o inventário de hardware para um computador específico.
 - **Inventário de Software geral - históricos**:   
 Ver todo o inventário de software para uma máquina específica.
 - **Descrição geral de estado de funcionamento do infraestrutura - histórico**:  
 Apresenta uma descrição geral do Estado de funcionamento da infraestrutura do Configuration Manager
 - **Lista de software maligno detetado - históricos**:    
 Software maligno de vista que foi detetado na organização.
 - **Resumo de distribuição de software - histórico**:   
 Um resumo de distribuição de software para um anúncio específico e a máquina.


## <a name="expand-an-existing-stand-alone-primary-into-a-hierarchy"></a>Expandir um site primário autónomo existente numa hierarquia
Antes de poder instalar um site de administração central para expandir um site primário autónomo existente, tem primeiro de desinstalar a função de ponto de serviço do armazém de dados. Depois de instalar o site de administração central, em seguida, pode instalar a função de sistema de sites no site de administração central.  

Ao contrário de uma mudança da base de dados de armazém de dados, esta alteração resulta em perda de dados históricos que tiver sincronizado anteriormente no site primário. Não é suportada para a base de dados do site primário de cópia de segurança e restaurá-lo no site de administração central.




## <a name="move-the-data-warehouse-database"></a>Mover a base de dados do armazém de dados
Utilize os seguintes passos para mover a base de dados do armazém de dados para um novo SQL Server:

1.  Utilize o SQL Server Management Studio para a base de dados do armazém de dados de cópia de segurança. Em seguida, restaure a base de dados para um SQL Server no novo computador que aloja o armazém de dados.   
> [!NOTE]     
> Depois de restaurar a base de dados para o novo servidor, certifique-se de que as permissões de acesso de base de dados são os mesmos na nova base de dados de armazém de dados idênticos na base de dados de armazém de dados original.  

2.  Utilize a consola do Configuration Manager para remover a função de sistema de sites do ponto de serviço do armazém de dados do servidor atual.
3.  Reinstalar o ponto de serviço do armazém de dados e especifique o nome do novo SQL Server e instância que aloja a base de dados do armazém de dados que é restaurada.
4.  Após a instalação da função de sistema de sites, a mudança está concluída.

## <a name="troubleshooting-data-warehouse-issues"></a>Resolução de problemas do armazém de dados
**Ficheiros de registo**:  
Utilize os seguintes registos para investigar problemas com a instalação do ponto de serviço do armazém de dados, ou uma sincronização de dados:
 - *DWSSMSI.log* e *DWSSSetup.log* -utilizar estes registos para investigar erros ao instalar o ponto de serviço do armazém de dados.
 - *Microsoft.ConfigMgrDataWarehouse.log* – utilizar este registo para investigar a sincronização de dados entre a base de dados do site para a base de dados do armazém de dados.

**Falha de multimédia**  
 A instalação do ponto de serviço do armazém de dados de falha num servidor de sistema de sites remoto quando o armazém de dados é a primeira função do sistema de sites que instala nesse computador.  
  - **Solução**:   
    Certifique-se de que o computador que estiver a instalar o ponto de serviço do armazém de dados num já aloja pelo menos uma outra função do sistema de sites.  


**Problemas de sincronização conhecidos**:   
A sincronização falhar com a seguinte mensagem no *Microsoft.ConfigMgrDataWarehouse.log*: **"Falha ao povoar objetos de esquema"**  
 - **Solução**:  
    Certifique-se de que a conta de computador do computador que aloja a função de sistema de sites é um **db_owner** na base de dados de armazém de dados.

Relatórios de armazém de dados não abrirá quando a base de dados do armazém de dados e o ponto de serviço Reporting Services estão em diferentes sistemas de site.  

 - **Solução**:  
    Conceda o **conta de ponto do Reporting Services** o **db_datareader** permissão na base de dados de armazém de dados.

Quando abre um relatório de armazém de dados, é devolvido o erro seguinte:

*Ocorreu um erro durante o processamento do relatório. (rsProcessingAborted) Não é possível criar uma ligação à origem de dados 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection) Uma ligação foi estabelecida com êxito o servidor, mas, em seguida, Ocorreu um erro durante o handshake de Pré-início de sessão. (fornecedor: Fornecedor de SSL, erro: 0 - a cadeia de certificados foi emitida por uma autoridade de que não é fidedigna.)*

- **Solução**: Utilize os seguintes passos para configurar certificados:

  1. No computador que aloja a base de dados do armazém de dados:

    1. Abra o IIS, clique em **certificados de servidor**, faça duplo clique no **Criar certificado autoassinado**e, em seguida, especifique o "nome amigável" o nome do certificado como **dados do armazém de SQL Server Identification Certificate**. Selecione o arquivo de certificados como **pessoais**.
    2. Abra **Gestor de configuração do SQL Server**, em **configuração de rede do SQL Server**, rato para selecionar **propriedades** em **protocolos para MSSQLSERVER**. Em seguida, no **certificado** separador, selecione **dados do armazém de SQL Server Identification Certificate** como o certificado e, em seguida, guarde as alterações.  
    3. Abra **Gestor de configuração do SQL Server**, em **do SQL Server Services**, reinicie **serviço do SQL Server** e **Reporting Service**.
    4.  Abra a consola de gestão da Microsoft (MMC) e adicione o snap-in **certificados**, selecione para gerir o certificado para **conta de computador** do computador local. Em seguida, na MMC, expanda o **pessoais** pasta > **certificados**e exportar o **dados do armazém de SQL Server Identification Certificate** como um **x. 509 binário codificado de DER (. CER)** ficheiro.    
  2.    No computador que aloja o SQL Server Reporting Services, abra a MMC e adicionar o snap-in para **certificados**. Em seguida, selecione para gerir os certificados **conta de computador**. Sob o **autoridades de certificação de raiz fidedigna** pasta, importar o **dados do armazém de SQL Server Identification Certificate**.


## <a name="data-warehouse-dataflow"></a>Fluxo de dados de armazém de dados   
![Datawarehouse_flow](./media/datawarehouse.png)

**Armazenamento de dados e sincronização**

| Passo   | Detalhes  |
|:------:|-----------|  
| **1**  |  O servidor do site transfere e armazena dados na base de dados do site.  |  
| **2**  |      Com base na respetiva agenda e a configuração, o ponto de serviço do Data Warehouse obtém dados da base de dados do site.  |  
| **3**  |  O ponto de serviço do armazém de dados é transferida e armazena uma cópia dos dados sincronizados na base de dados do armazém de dados. |  
**Relatórios**

| Passo   | Detalhes  |
|:------:|-----------|  
| **A**  |  Utilizar relatórios incorporados, um utilizador solicita dados. Este pedido é passado para o Reporting Services ponto utilizando o SQL Server Reporting Services. |  
| **B**  |      A maioria dos relatórios são para obter informações atuais e estes pedidos são executados na base de dados do site. |  
| **C**  | Quando um relatório solicita dados históricos, utilizando um dos relatórios com um *categoria* de **do armazém de dados**, o pedido é executado na base de dados do armazém de dados.   |  

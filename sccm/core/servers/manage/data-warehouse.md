---
title: "Armazém de dados | Documentos do Microsoft"
description: "Ponto de serviço do armazém de dados e base de dados para o System Center Configuration Manager"
ms.custom: na
ms.date: 3/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 3c2a07f560e0aa3d2beb7cc50e71c98ac45c27e1
ms.openlocfilehash: 9239f6e749c368835e8594ca2d07378d8555b99e
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
#  <a name="the-data-warehouse-service-point-for-system-center-configuration-manager"></a>O ponto de serviço do armazém de dados para o System Center Configuration Manager
*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir da versão 1702 que pode utilizar o ponto de serviço do armazém de dados para armazenar e elaborar relatórios sobre dados históricos de longo prazo para a implementação do Configuration Manager.

> [!TIP]  
> Introduzida com a versão 1702, o ponto de serviço do armazém de dados é uma funcionalidade de versão de pré-lançamento. Para ativá-lo, consulte o artigo [utilizar funcionalidades da versão de pré-lançamento](/sccm/core/servers/manage/pre-release-features).

O armazém de dados suporta até 2 TB de dados, com carimbos de registo de alterações. Armazenamento de dados é realizado por sincronizações automáticas da base de dados do site do Configuration Manager para a base de dados do armazém de dados. Esta informação, em seguida, é acessível a partir do seu ponto de Reporting Services.


Os dados que estão sincronizados incluem o seguinte a partir de grupos de dados globais e os dados do Site:
- Estado de funcionamento da infraestrutura
- Segurança
- Conformidade
- Software maligno   
- Implementações de software
- Detalhes de inventário (no entanto, o histórico de inventário não está sincronizado)

Quando instala a função de sistema de sites, instala e configura a base de dados do armazém de dados. Instala também vários relatórios para que possa procurar facilmente para e relatórios sobre estes dados.



## <a name="prerequisites-for-the-data-warehouse-service-point"></a>Pré-requisitos para o ponto de serviço do armazém de dados
- O computador onde irá instalar a função de sistema de sites requer o .NET Framework 4.5.2 ou posterior.
- A conta de computador do computador onde instalou a função de sistema de sites é utilizada para sincronizar dados com a base de dados do armazém de dados. Esta conta necessita das seguintes permissões:  
  - **Administrador** no computador que alojará a base de dados do armazém de dados.
  - **DB_owner** permissão a base de dados do armazém de dados.
-    A base de dados do armazém de dados é suportada numa predefinição ou instância do SQL Server 2012 ou posterior com o nome. Tem de ser a edição Enterprise ou Datacenter.
  - Grupo de Disponibilidade AlwaysOn do SQL Server: Esta configuração não é suportada.
  - Cluster de servidor do SQL Server: Não são suportados clusters de ativação pós-falha do SQL Server. Isto acontece porque a base de dados do armazém de dados não foi serem testado em clusters de ativação pós-falha do SQL Server.
  - Quando a base de dados do armazém de dados forem remoto a partir da base de dados do servidor do site, tem de ter uma licença separada do SQL Server que aloja a base de dados.

> [!IMPORTANT]  
> O armazém de dados não é suportado quando o computador que executa o ponto de serviço do armazém de dados ou que aloja a base de dados do armazém de dados é executada uma das seguintes idiomas:
> - JPN-Japonês
> - KOR-Coreano
> - CHS – Chinês simples
> - CHT – Chinês tradicional, este problema será resolvido numa versão futura.


## <a name="install-the-data-warehouse"></a>Instalar o armazém de dados
Pode instalar a função de sistema do site do armazém de dados apenas no site de nível superior da hierarquia (um site de administração central ou site primário autónomo).

Cada hierarquia suporta uma única instância desta função, e pode estar localizada em qualquer sistema de site desse site de nível superior. O SQL Server que aloja a base de dados para o armazém de pode ser local à função de sistema de sites, ou remoto. Apesar do armazém de dados é funciona com o ponto do Reporting Services que está instalado no mesmo site, as funções de sistema de dois sites não precisam de ser instalado no mesmo servidor.   

Para instalar a função, utilize o **Adicionar Assistente de funções de sistema de sites** ou **criar Assistente de servidor de sistema de sites**. Consulte o artigo [instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles) para obter mais informações.  

Quando instala a função, o Configuration Manager cria a base de dados do armazém de dados por si na instância do SQL Server que especificou. Se especificar o nome da base de dados existente (como o faria se que [mover a base de dados do armazém de dados para um novo SQL Server](#move-the-data-warehouse-database)), o Configuration Manager não será criada uma nova base de dados, mas em vez disso, utilizará a especificar.

### <a name="configurations-used-during-installation"></a>Configurações utilizadas durante a instalação
**Seleção da função do sistema** página:  

**Geral** página:
-     **As definições de ligação de base de dados do armazém de dados do Configuration Manager**:
 - **SQL Server nome de domínio completamente qualificado**:  
 Especifique o nome completo do domínio qualificado (FQDN) do servidor que aloja a base de dados do ponto de serviço do armazém de dados.
 - **Nome da instância do SQL Server, se aplicável**:   
 Se não utilizar uma instância predefinida do SQL Server, tem de especificar a instância.
 - **Nome da base de dados**:   
 Especifique um nome para a base de dados do armazém de dados.  Configuration Manager irá criar a base de dados do armazém de dados com este nome. Se especificar um nome de base de dados que já existe na instância do SQL server, o Configuration Manager irá utilizar essa base de dados.
 - **Porta do SQL Server utilizada para ligação**:   
 Especifique o número de porta de TCP/IP que esteja configurado para o SQL Server que aloja o datbase de armazém de dados. Esta porta é utilizada pelo serviço de sincronização do armazém de dados para ligar à base de dados do armazém de dados.  

**Agenda de sincronização** página:   
- **Agenda de sincronização**:
 - **Hora de início**:  
 Especifica a hora que pretende que a sincronização do armazém de dados para iniciar.
 - **Padrão de periodicidade**:
    - **Diária**: Especifique a execução de sincronização para todos os dias.
    - **Semanal**: Especifique um único dia de cada semana e periodicidade semanal para sincronização.

## <a name="reporting"></a>Relatórios
Depois de instalar um ponto de serviço do armazém de dados, vários relatórios ficam disponíveis no ponto do Reporting Services que está instalado no mesmo site. Se instalar o ponto de serviço do armazém de dados antes de instalar um ponto do Reporting Services, os relatórios serão adicionados automaticamente quando, posteriormente, instalar o ponto do Reporting Services.

A função de sistema de sites do armazém de dados inclui os seguintes relatórios, uma categoria de **do armazém de dados**:
 - **Implementação da aplicação - histórica**:   
 Veja detalhes de implementação de aplicação para uma aplicação específica e a máquina.
 - **Conformidade - histórico de atualização de Software e do Endpoint Protection**: Computadores de vista que estão em falta as atualizações de software.  
 - **Inventário de Hardware geral – históricos**:      
 Ver todo o inventário de hardware para uma máquina específica.
 - **Inventário de Software geral – históricos**:      
 Ver todo o inventário de software para uma máquina específica.
 - **Descrição geral de estado de funcionamento do infraestrutura - histórico**:     
 Apresenta uma descrição geral do Estado de funcionamento da infraestrutura do Configuration Manager
 - **Lista de software maligno detetado - históricos**:     
 Vista contra software maligno que foi detetado na organização.
 - **Resumo de distribuição de software - histórico**:     
 Um resumo da distribuição de software para um anúncio específico e a máquina.


## <a name="expand-an-existing-stand-alone-primary-into-a-hierarchy"></a>Expandir um primário autónomo existente para uma hierarquia
Antes de poder instalar um site de administração central para expandir um site primário autónomo existente, primeiro deve desinstalar a função de ponto de serviço do armazém de dados. Depois de instalar o site de administração central, em seguida, pode instalar a função de sistema de sites no site de administração central.  

Ao contrário de uma deslocação da base de dados do armazém de dados, esta alteração resulta numa perda de dados históricos que tenha sido anteriormente sincronizado no site primário. Não é suportada para a base de dados do site primário de cópia de segurança e restaurá-lo no site de administração central.




## <a name="move-the-data-warehouse-database"></a>Mover a base de dados do armazém de dados
Utilize os seguintes passos para mover a base de dados do armazém de dados para um novo SQL Server:

1.    Utilize o SQL Server Management Studio para os dados de cópia de segurança do armazém de base de dados e, em seguida, restaure a base de dados para um SQL Server no novo computador que irá alojar o armazém de dados.   
> [!NOTE]     
> Depois de restaurar a base de dados para o novo servidor, certifique-se de que as permissões de acesso à base de dados são os mesmos na nova base de dados de armazém de dados que estavam na base de dados de armazém de dados original.  

2.    Utilize a consola do Configuration Manager para remover a função de sistema de sites do ponto de serviço do armazém de dados do servidor atual.
3.    Reinstale o ponto de serviço do armazém de dados e especifique o nome do novo SQL Server e instância que aloja a base de dados do armazém de dados que é restaurada.
4.    Após instala a função de sistema de sites, a mudança está concluída.

## <a name="troubleshooting-data-warehouse-issues"></a>Resolução de problemas do armazém de dados
**Ficheiros de registo**:  
Utilize os seguintes registos para investigar problemas com a instalação do armazém de dados do ponto de serviço, ou uma sincronização de dados:
 - *DWSSMSI.log* e *DWSSSetup.log* -utilizar estes registos para investigar erros ao instalar o ponto de serviço do armazém de dados.
 - *Microsoft.ConfigMgrDataWarehouse.log* – utilizar este registo para investigar a sincronização de dados entre a base de dados do site para a base de dados do armazém de dados.

**Configurar o falha**  
 A instalação do ponto de serviço do armazém de dados de falha num servidor de sistema de site remoto quando o armazém de dados é a primeira função de sistema de sites instalada nesse computador.  
  - **Solução**:   
    Certifique-se de que o computador que estiver a instalar o ponto de serviço do armazém de dados num já aloja pelo menos uma outra função do sistema de sites.  


**Problemas de sincronização conhecidos**:   
Falha na sincronização com o seguinte no *Microsoft.ConfigMgrDataWarehouse.log*: **"Falha ao povoar objetos de esquema"**  
 - **Solução**:  
    Certifique-se de que a conta de computador do computador que aloja a função de sistema de sites é um **db_owner** na base de dados de armazém de dados.

Relatórios do armazém de dados não abrirá quando a base de dados do armazém de dados e relatórios ponto de serviço estão em sistemas de sites diferentes.  

 - **Solução**:  
    Conceder a **conta ao ponto do Reporting Services** o **db_datareader** permissão a base de dados do armazém de dados.

Quando abre um relatório de armazém de dados, é devolvido o erro seguinte:

*Ocorreu um erro durante o processamento do relatório. (rsProcessingAborted) Não é possível criar uma ligação à origem de dados 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection) Com êxito foi estabelecida uma ligação com o servidor, mas, em seguida, Ocorreu um erro durante o handshake de Pré-início de sessão. (fornecedor: Fornecedor de SSL, erro: 0 - cadeia de certificados foi emitida por uma autoridade de que não seja fidedigna.)*

- **Solução**: Utilize os seguintes passos para configurar os certificados:

  1. No computador que aloja a base de dados do armazém de dados:

    1. Abra o IIS, clique em **certificados de servidor**, com o botão direito no **Criar certificado assinados**e, em seguida, especifique o "nome amigável" o nome do certificado como **certificado de identificação de servidor de SQL Server do armazém de dados**. Selecione o arquivo de certificados como **pessoal**.
    2. Abrir **SQL Server Configuration Manager**, em **configuração de rede do SQL Server**, clique o botão direito para selecionar **propriedades** em **protocolos para MSSQLSERVER**. Em seguida, no **certificado** separador, selecione **certificado de identificação de servidor de SQL Server do armazém de dados** como o certificado e, em seguida, guardar as alterações.  
    3. Abrir **SQL Server Configuration Manager**, em **do SQL Server Services**, reinicie **serviço do SQL Server** e **reporte**.
    4.    Abra a consola de gestão da Microsoft (MMC) e adicionar o snap-in para **certificados**, selecione para gerir o certificado para **conta de computador** da máquina local. Em seguida, na MMC, expanda o **pessoal** pasta > **certificados**e exportar a **certificado de identificação de servidor de SQL Server do armazém de dados** como um **x. 509 binário de codificado DER (. CER)** ficheiro.    
  2.    No computador que aloja o SQL Server Reporting Services, abrir a MMC e adicionar o snap-in para **certificados**e, em seguida, selecione para gerir certificados para **conta de computador**. Sob o **autoridades de certificação de raiz fidedigna** pasta, importar o **certificado de identificação de servidor de SQL Server do armazém de dados**.


## <a name="data-warehouse-dataflow"></a>Fluxo de dados de armazém de dados   
![Datawarehouse_flow](./media/datawarehouse.png)

**Armazenamento de dados e sincronização**

| Passo   | Detalhes  |
|:------:|-----------|  
| **1**  |     O servidor do site é transferida e armazena os dados na base de dados do site.  |  
| **2**  |      Com base na sua agenda e a configuração, o ponto de serviço do armazém de dados obtém dados a partir da base de dados do site.  |  
| **3**  |  O ponto de serviço do armazém de dados é transferida e armazena uma cópia dos dados sincronizados na base de dados do armazém de dados. |  
**Relatórios**

| Passo   | Detalhes  |
|:------:|-----------|  
| **A**  |  Utilizar relatórios incorporados, um utilizador solicita dados. Este pedido é transmitido ao Reporting Services ponto através de SQL Server Reporting Services. |  
| **B**  |      A maioria dos relatórios são para obter informações atuais e estes pedidos são executados na base de dados do site. |  
| **C**  | Quando um relatório de pedidos de dados históricos, utilizando um dos relatórios com uma *categoria* de **do armazém de dados**, o pedido é executado na base de dados do armazém de dados.   |  


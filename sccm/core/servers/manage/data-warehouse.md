---
title: "Depósito de dados | Microsoft Docs"
description: "Ponto de serviço do Data Warehouse e banco de dados para o System Center Configuration Manager"
ms.custom: na
ms.date: 5/31/2017
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
ms.sourcegitcommit: dc221ddf547c43ab1f25ff83c3c9bb603297ece6
ms.openlocfilehash: f11a53bbc85b40077b3909568db5ae5552b0456c
ms.contentlocale: pt-pt
ms.lasthandoff: 06/01/2017


---
#  <a name="the-data-warehouse-service-point-for-system-center-configuration-manager"></a>O ponto de serviço do Data Warehouse do System Center Configuration Manager
*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Começando com a versão 1702, que você pode usar o ponto de serviço do Data Warehouse para armazenar e relatar dados históricos de longo prazo para implantação do Configuration Manager.

> [!TIP]  
> Introduzida com a versão 1702, o ponto de serviço do Data Warehouse é um recurso de pré-lançamento. Para habilitá-lo, consulte [usar recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features).

O data warehouse oferece suporte a até 2 TB de dados, com carimbos de controle de alterações. Armazenamento de dados é feito pela sincronizações automatizadas do banco de dados de site do Configuration Manager para o banco de dados do data warehouse. Essas informações estarão acessíveis a partir do ponto do Reporting Services.


Dados que são sincronizados incluem os seguintes dos grupos de dados globais e dados do Site:
- Integridade da infraestrutura
- Segurança
- Conformidade
- Malware   
- Implementações de software
- Detalhes do inventário (no entanto, o histórico de inventário não está sincronizado)

Quando a função do sistema de site é instalado, ele instala e configura o banco de dados do data warehouse. Ele também instala vários relatórios para que você pode facilmente procurar e relatórios nesses dados.



## <a name="prerequisites-for-the-data-warehouse-service-point"></a>Pré-requisitos para o ponto de serviço do Data Warehouse
- O computador onde você instala a função do sistema de site requer o .NET Framework 4.5.2 ou posterior.
- A conta de computador do computador onde você instala a função do sistema de site é usada para sincronizar dados com o banco de dados do data warehouse. Essa conta requer as seguintes permissões:  
  - **Administrador** no computador que hospedará o banco de dados do data warehouse.
  - **DB_owner** permissão no banco de dados do data warehouse.
  - **Db_reader para** e **executar** permissões para os sites de nível superior do banco de dados do site.
-    O banco de dados do data warehouse é tem suporte em um padrão ou nomeado instância do SQL Server 2012 ou posterior. Deve ser a edição Enterprise ou Datacenter.
  - Grupo de disponibilidade do AlwaysOn do SQL Server: Esta configuração não é suportada.
  - Cluster do SQL Server: Não há suporte para clusters de failover do SQL Server. Isso ocorre porque o banco de dados do data warehouse não foi testado profundamente em clusters de failover do SQL Server.
  - Quando o banco de dados do data warehouse é remoto do servidor do site, você deve ter uma licença separada para o SQL Server que hospeda o banco de dados.

> [!IMPORTANT]  
> Não há suporte para o Data Warehouse quando o computador que executa o ponto de serviço do Data Warehouse ou que hospeda o banco de dados do data warehouse executa um dos seguintes idiomas:
> - JPN-japonês
> - KOR-coreano
> - CHS-chinês simplificado
> - CHT-chinês tradicional, esse problema será resolvido em uma versão futura.


## <a name="install-the-data-warehouse"></a>Instalar o Data Warehouse
Você pode instalar a função do sistema de site do depósito de dados apenas no site de nível superior da hierarquia (um site de administração central ou site primário autônomo).

Cada hierarquia oferece suporte a uma única instância dessa função e pode ser localizado em qualquer sistema de site do site de nível superior. O SQL Server que hospeda o banco de dados para o warehouse pode ser local para a função do sistema de site ou remoto. Embora o data warehouse funciona com o ponto do Reporting Services está instalado no mesmo site, as funções do sistema de dois site não precisa ser instalado no mesmo servidor.   

Para instalar a função, use o **Adicionar Assistente de funções de sistema de Site** ou **criar Assistente de servidor de sistema de Site**. Consulte [instalar funções do sistema de site](/sccm/core/servers/deploy/configure/install-site-system-roles) para obter mais informações.  

Quando você instala a função, o Configuration Manager cria o banco de dados do data warehouse para você na instância do SQL Server que você especificar. Se você especificar o nome do banco de dados existente (como você faria se você [mover o banco de dados do data warehouse para um novo servidor SQL](#move-the-data-warehouse-database)), não cria um novo banco de dados do Configuration Manager, mas utiliza aquele que você especificou.

### <a name="configurations-used-during-installation"></a>Configurações usadas durante a instalação
**Seleção de função do sistema** página:  

**Geral** página:
-     **Configurações de conexão de banco de dados de depósito de dados do Configuration Manager**:
 - **Nome de domínio totalmente qualificado do servidor de SQL**:  
 Especifique o nome de domínio totalmente qualificado (FQDN) do servidor que hospeda o banco de dados do ponto de serviço do Data Warehouse.
 - **Nome da instância do SQL Server, se aplicável**:   
 Se você não usar uma instância padrão do SQL Server, você deve especificar a instância.
 - **Nome do banco de dados**:   
 Especifique um nome para o banco de dados do data warehouse.  Configuration Manager criará o banco de dados do data warehouse com esse nome. Se você especificar um nome de banco de dados que já existe na instância do SQL server, o Configuration Manager usará esse banco de dados.
 - **Porta do SQL Server usada para conexão**:   
 Especifique o número de porta de TCP/IP está configurado para o SQL Server que hospeda o banco de depósito de dados. Esta porta é usada pelo serviço de sincronização de depósito de dados para se conectar ao banco de dados do data warehouse.  

**Agenda de sincronização** página:   
- **Agenda de sincronização**:
 - **Hora de início**:  
 Especifique a hora em que você deseja que a sincronização do data warehouse para iniciar.
 - **Padrão de recorrência**:
    - **Diário**: Especifique que a sincronização é executada diariamente.
    - **Semanal**: Especifique um único dia de cada semana e recorrência semanal para sincronização.

## <a name="reporting"></a>Relatórios
Depois de instalar um ponto de serviço do Data Warehouse, vários relatórios ficam disponíveis no ponto do Reporting Services está instalado no mesmo site. Se você instalar o ponto de serviço do Data Warehouse antes de instalar um ponto do Reporting Services, os relatórios serão adicionados automaticamente quando você instala o ponto do Reporting Services mais tarde.

A função de sistema de site do Data Warehouse inclui os relatórios a seguir, que têm uma categoria de **Data Warehouse**:
 - **Implantação de aplicativo - histórica**:   
 Exibir detalhes de implantação de aplicativo para um aplicativo específico e o computador.
 - **Proteção de ponto de extremidade e atualização de Software conformidade - histórica**: Exibir computadores que estão faltando as atualizações de software.  
 - **Inventário de Hardware geral - históricos**:      
 Exiba todo o inventário de hardware para um computador específico.
 - **Inventário de Software geral - históricos**:      
 Exiba todo o inventário de software para um computador específico.
 - **Integridade visão geral da infraestrutura - histórico**:     
 Exibe uma visão geral da integridade da infra-estrutura do Configuration Manager
 - **Lista de malwares detectados - históricos**:     
 Exibição contra malware foi detectado na organização.
 - **Resumo de distribuição de software - histórico**:     
 Um resumo da distribuição de software para um anúncio específico e o computador.


## <a name="expand-an-existing-stand-alone-primary-into-a-hierarchy"></a>Expandir um primário autônomo existente em uma hierarquia
Antes de instalar um site de administração central para expandir um site primário autônomo existente, você deve primeiro desinstalar a função de ponto de serviço do Data Warehouse. Depois de instalar o site de administração central, em seguida, você pode instalar a função do sistema de site no site de administração central.  

Ao contrário de um movimento de banco de dados do data warehouse, essa alteração resulta em perda de dados históricos sincronizadas anteriormente no site primário. Não há suporte para fazer backup do banco de dados do site primário e restaurá-lo no site de administração central.




## <a name="move-the-data-warehouse-database"></a>Mover o banco de dados do Data Warehouse
Use as etapas a seguir para mover o banco de dados do data warehouse para um novo servidor SQL:

1.    Use o SQL Server Management Studio para fazer backup dos dados do data warehouse banco de dados e, em seguida, restaurar esse banco de dados para um SQL Server no novo computador que hospedará o data warehouse.   
> [!NOTE]     
> Depois de restaurar o banco de dados para o novo servidor, certifique-se de que as permissões de acesso de banco de dados são os mesmos do data warehouse banco de dados, assim como estavam no banco de dados de depósito de dados original.  

2.    Use o console do Configuration Manager para remover a função de sistema de site do ponto de serviço do Data Warehouse do servidor atual.
3.    Reinstale o ponto de serviço do Data Warehouse e especifique o nome do novo servidor SQL e a instância que hospeda o banco de dados do Data Warehouse que é restaurado.
4.    Depois de instala a função do sistema de site, a movimentação é concluída.

## <a name="troubleshooting-data-warehouse-issues"></a>Solucionando problemas do data warehouse
**Arquivos de log**:  
Use os seguintes logs para investigar problemas com a instalação do ponto de serviço do Data Warehouse ou sincronização de dados:
 - *DWSSMSI.log* e *DWSSSetup.log* -usar esses logs para investigar os erros ao instalar o ponto de serviço do Data Warehouse.
 - *Microsoft.ConfigMgrDataWarehouse.log* – usar esse log para investigar a sincronização de dados entre o banco de dados do site para o banco de dados do data warehouse.

**Configurar a falha**  
 Instalação do ponto de serviço do Data Warehouse de falha em um servidor de sistema de site remoto quando o data warehouse é a primeira função de sistema de site instalada nesse computador.  
  - **Solução**:   
    Certifique-se de que o computador que você estiver instalando o ponto de serviço do Data Warehouse em já hospeda pelo menos uma outra função de sistema de site.  


**Problemas de sincronização**:   
A sincronização falha com o seguinte o *Microsoft.ConfigMgrDataWarehouse.log*: **"Falha ao popular objetos de esquema"**  
 - **Solução**:  
    Certifique-se de que a conta de computador do computador que hospeda a função de sistema de site é um **db_owner** no banco de dados do data warehouse.

Relatórios do data warehouse não é aberto quando o banco de dados do data warehouse e o ponto de serviço de relatório estão em sistemas de site diferente.  

 - **Solução**:  
    Conceda o **conta de ponto do Reporting Services** o **db_datareader** permissão no banco de dados do data warehouse.

Quando você abre um relatório do data warehouse, é retornado o seguinte erro:

*Ocorreu um erro durante o processamento de relatório. (rsProcessingAborted) Não é possível criar uma conexão à fonte de dados 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection) Uma conexão foi estabelecida com êxito com o servidor, mas ocorreu um erro durante o handshake de pré-logon. (provedor: Provedor de SSL, erro: 0 - a cadeia de certificado foi emitida por uma autoridade que não é confiável.)*

- **Solução**: Use as etapas a seguir para configurar certificados:

  1. No computador que hospeda o banco de dados de data warehouse:

    1. Abra o IIS, clique em **certificados de servidor**, clique duas vezes em **criar um certificado autoassinado**e, em seguida, especifique o "nome amigável" do nome do certificado como **Data Warehouse SQL Server Identification Certificate**. Selecione o repositório de certificados como **pessoais**.
    2. Abra **SQL Server Configuration Manager**, em **configuração de rede do SQL Server**, com o botão direito para selecionar **propriedades** em **protocolos para MSSQLSERVER**. Em seguida, no **certificado** guia, selecione **Data Warehouse SQL Server Identification Certificate** como o certificado e, em seguida, salve as alterações.  
    3. Abra **SQL Server Configuration Manager**, em **SQL Server Services**, reiniciar **serviço do SQL Server** e **Reporting Service**.
    4.    Abra o Console de gerenciamento Microsoft (MMC) e adicione o snap-in para **certificados**, selecione para gerenciar o certificado para **conta de computador** da máquina local. Em seguida, no MMC, expanda o **pessoal** pasta > **certificados**e exportar o **Data Warehouse SQL Server Identification Certificate** como um **x. 509 binário codificado por DER (. CER)** arquivo.    
  2.    No computador que hospeda o SQL Server Reporting Services, abra o MMC e adicione o snap-in para **certificados**e, em seguida, selecione para gerenciar certificados para **conta de computador**. Sob o **autoridades de certificação raiz confiáveis** pastas, importar o **Data Warehouse SQL Server Identification Certificate**.


## <a name="data-warehouse-dataflow"></a>O fluxo de dados do Data Warehouse   
![Datawarehouse_flow](./media/datawarehouse.png)

**Sincronização e o armazenamento de dados**

| Passo   | Detalhes  |
|:------:|-----------|  
| **1**  |     O servidor do site transfere e armazena dados no banco de dados do site.  |  
| **2**  |      O ponto de serviço do Data Warehouse com base em sua agenda e configuração, obtém dados do banco de dados do site.  |  
| **3**  |  O ponto de serviço do Data Warehouse transfere e armazena uma cópia dos dados sincronizados no banco de dados do Data Warehouse. |  
**Relatórios**

| Passo   | Detalhes  |
|:------:|-----------|  
| **UM**  |  Usando relatórios internos, um usuário solicita dados. Essa solicitação é passada para o Reporting Services ponto usando o SQL Server Reporting Services. |  
| **B**  |      A maioria dos relatórios são para obter informações atuais, e essas solicitações são executadas no banco de dados do site. |  
| **C**  | Quando um relatório solicita dados históricos, usando um dos relatórios com um *categoria* de **Data Warehouse**, a solicitação é executada no banco de dados do Data Warehouse.   |  


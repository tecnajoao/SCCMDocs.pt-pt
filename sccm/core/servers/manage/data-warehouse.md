---
title: Armazém de dados
titleSuffix: Configuration Manager
description: Ponto de serviço do armazém de dados e a base de dados para o Configuration Manager
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a4d95495f2f200eaff39699c65cc391a2a81b009
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897564"
---
#  <a name="the-data-warehouse-service-point-for-configuration-manager"></a>O ponto de serviço de armazém de dados para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1277922--> Utilize o ponto de serviço do armazém de dados para armazenar e gerar relatórios sobre dados históricos de longo prazo para a sua implementação do Configuration Manager.

> [!Note]  
> O Configuration Manager não permite esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


O armazém de dados suporta até 2 TB de dados, carimbos de data de registo de alterações. O armazém de dados armazena os dados ao sincronizar automaticamente os dados da base de dados do site do Configuration Manager para a base de dados do armazém de dados. Esta informação, em seguida, é acessível a partir do seu ponto de serviço de geração de relatórios. Dados sincronizados com a base de dados do armazém de dados são mantidos durante três anos. Periodicamente, uma tarefa incorporada remove os dados que é mais antigos do que três anos.

Dados que são sincronizados incluem o seguinte dos grupos de dados globais e de dados do Site:
- Estado de funcionamento da infraestrutura
- Segurança
- Conformidade
- Malware   
- Implementações de software
- Detalhes de inventário (no entanto, histórico de inventário não está sincronizado)

Quando instala a função de sistema de sites, instala e configura a base de dados do armazém de dados. Ele também instala vários relatórios para que possam procurar facilmente e relatórios sobre estes dados.

A partir da versão 1810, pode sincronizar mais tabelas da base de dados do site para o armazém de dados. Esta alteração permite-lhe criar relatórios mais com base nos seus requisitos empresariais.<!--1358870--> 



## <a name="prerequisites"></a>Pré-requisitos

- A função de sistema de sites de armazém de dados é suportada apenas no site de nível superior da sua hierarquia. Por exemplo, um site de administração central ou site primário autónomo.  

- O computador onde instalou a função de sistema de sites requer o .NET Framework 4.5.2 ou posterior.  

- Conceder a **conta do ponto de Reporting Services** a **db_datareader** permissão na base de dados do armazém de dados.  

- Para sincronizar dados com a base de dados do armazém de dados, o Configuration Manager utiliza a conta de computador da função de sistema de sites. Esta conta necessita das seguintes permissões:  

    - **Administrador** no computador que aloja a base de dados do armazém de dados.  

    - **DB_Creator** permissão na base de dados do armazém de dados.  

    - Qualquer um dos **DB_owner** ou **DB_reader** com **executar** permissões para a base de dados do site de nível superior.  

- A base de dados do armazém de dados requer o uso do SQL Server 2012 ou posterior. A edição pode ser Standard, Enterprise ou Datacenter. A versão do SQL Server para o armazém de dados não precisa de ser o mesmo que o servidor de base de dados do site.<!--SCCMDocs issue 662-->  

- A base de dados do armazém suporta as seguintes configurações do SQL Server:  

    - Uma instância predefinida ou nomeada  

    - Grupo de disponibilidade Always On do SQL Server  

    - Cluster de ativação pós-falha do SQL Server  

- Se usar [vistas distribuídas](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews), tem de instalar o ponto de serviço do armazém de dados no mesmo servidor que aloja a base de dados do site de administração central.  

Para obter mais informações sobre o licenciamento do SQL Server, consulte a [produtos e licenciamento FAQ](/sccm/core/understand/product-and-licensing-faq). <!-- sms500967 -->

Tamanho do armazém de dados do banco de dados igual à sua base de dados do site. Enquanto o armazém de dados for menor em primeiro lugar, ele crescerá ao longo do tempo. <!--SCCMDocs issue 756-->



## <a name="install"></a>Instalar

Cada hierarquia suporta uma única instância desta função, em qualquer sistema de site do site de nível superior. O SQL Server que aloja a base de dados para o armazém pode ser local para a função de sistema de sites ou remoto. O armazém de dados funciona com o ponto do reporting services instalado no mesmo site. Não precisa de instalar as funções de sistema de sites de dois no mesmo servidor.   

Para instalar a função, utilize o **Adicionar Assistente de funções de sistema de sites** ou o **criar Assistente de servidor de sistema de sites**. Para obter mais informações, consulte [instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles). Sobre o **seleção da função do sistema** página do assistente, selecione a **ponto de serviço do armazém de dados** função. 

Quando instalar a função, o Configuration Manager cria a base de dados do armazém de dados para na instância do SQL Server que especificou. Se especificar o nome da base de dados existente, o Configuration Manager não cria uma nova base de dados. Em vez disso, ele usa aquele que especificar. Este processo é o mesmo que quando [mover a base de dados do armazém de dados para um novo servidor SQL](#move-the-data-warehouse-database).


### <a name="configure-properties"></a>Configurar as propriedades

#### <a name="general-page"></a>Página geral

- **SQL Server nome de domínio completamente qualificado**: Especifique o nome de domínio completamente qualificado (FQDN) do servidor que aloja a base de dados de ponto de serviço de armazém do dados.  

- **Nome da instância do SQL Server, se aplicável**: Se não usar uma instância predefinida do SQL Server, especifique a instância nomeada.  

- **Nome da base de dados**: Especifique um nome para a base de dados do armazém de dados. O Configuration Manager cria a base de dados do armazém de dados com este nome. Se especificar um nome de base de dados que já existe na instância do SQL server, o Configuration Manager utiliza essa base de dados.  

- **Porta do SQL Server utilizada para ligação**: Especifique o número de porta de TCP/IP utilizado pelo SQL Server que aloja a base de dados do armazém de dados. O serviço de sincronização do armazém de dados utiliza esta porta para ligar à base de dados do armazém de dados. Por padrão, ele usa a porta do SQL Server **1433** para comunicação.  

- **Conta de ponto de serviço do armazém de dados**: A partir da versão 1802, definir o **nome de utilizador** que utiliza o SQL Server Reporting Services para estabelecer a ligação à base de dados do armazém de dados.  


#### <a name="synchronization-schedule-page"></a>Página de agenda de sincronização
*Aplica-se a versão 1806 e anterior*

- **Hora de início**: Especifique o tempo que pretende que a sincronização do armazém de dados para iniciar.  

- **Padrão de periodicidade**

    - **Diária**: Especifique que a sincronização é executada diariamente.  

    - **Semanal**: Especifique um único dia de cada semana e a periodicidade semanal para sincronização.


#### <a name="synchronization-settings-page"></a>Página de definições de sincronização
*Aplica-se a versão 1810 e posterior*

- **Definição personalizada de sincronização de dados**: Escolha a opção para **selecionar tabelas**. Na janela de tabelas do banco de dados, selecione os nomes de tabela para sincronizar com a base de dados do armazém de dados. Utilize o filtro para procurar por nome ou selecione a lista pendente para escolher a grupos específicos. Selecione **OK** quando terminar para guardar.  

    > [!Note]  
    > Não é possível remover tabelas que a função seleciona por predefinição.  

- **Hora de início**: Especifique o tempo que pretende que a sincronização do armazém de dados para iniciar.  

- **Padrão de periodicidade**

    - **Diária**: Especifique que a sincronização é executada diariamente.  

    - **Semanal**: Especifique um único dia de cada semana e a periodicidade semanal para sincronização.



## <a name="reporting"></a>Relatórios

Depois de instalar um ponto de serviço do armazém de dados, vários relatórios disponibilizados no ponto do reporting services para o site. Se instalar o ponto de serviço do armazém de dados antes de instalar um ponto do reporting services, os relatórios são adicionados automaticamente, quando, posteriormente, instalar o ponto do reporting services.

> [!WARNING]  
> A partir da versão 1802, o ponto de armazém de dados suporta credenciais alternativas.<!--507334--> Se tiver atualizado de uma versão anterior do Configuration Manager, tem de especificar as credenciais que o SQL Server Reporting Services utiliza para ligar à base de dados do armazém de dados. Relatórios do armazém de dados não abrem até adicionar credenciais. 
> 
> Para especificar uma conta, defina o **nome de utilizador** para a conta de ponto de serviço ao armazém de dados nas propriedades de função. Para obter mais informações, consulte [configurar as propriedades](#configure-properties). 

A função de sistema de sites de armazém de dados inclui os seguintes relatórios, menos os **armazém de dados** categoria:  

- **Implementação de aplicações - histórico**: Ver os detalhes para a implementação de aplicação para uma aplicação específica e a máquina.  

- **Conformidade - histórico de atualizações de Software e proteção de ponto final**: Ver os computadores que estão em falta atualizações de software.  

- **Inventário de Hardware geral - histórico**: Ver todo o inventário de hardware de uma máquina específica.  

- **Inventário de Software geral - histórico**: Ver todo o inventário de software para uma máquina específica.  

- **Descrição geral de estado de funcionamento do infraestrutura - histórico**: Apresenta uma visão geral do Estado de funcionamento da sua infraestrutura do Configuration Manager.  

- **Lista de software maligno detetado - histórico**:    Software maligno do modo de exibição que foi detetado na organização.  

- **Resumo de distribuição de software - histórico**: Um resumo da distribuição de software para um anúncio específico e a máquina.  



## <a name="site-expansion"></a>Expansão do site

Antes de instalar um site de administração central para expandir um site de primário autónomo existente, primeiro de desinstalar a função de ponto de serviço de armazém de dados. Depois de instalar o site de administração central, em seguida, pode instalar a função de sistema de sites no site de administração central.  

Ao contrário de uma mudança da base de dados de armazém de dados, esta alteração resulta numa perda de histórico de dados que tiver sincronizado anteriormente no site primário. Não é suportada a cópia de segurança da base de dados do site primário e restaurá-lo no site de administração central.



## <a name="move-the-database"></a>Mover a base de dados

Utilize os seguintes passos para mover a base de dados do armazém de dados para um novo servidor SQL:  

1. Utilize o SQL Server Management Studio para criar cópias de segurança da base de dados do armazém de dados. Em seguida, restaure a base de dados para um SQL Server no novo computador que aloja o armazém de dados.  

    > [!NOTE]  
    > Depois de restaurar a base de dados para o novo servidor, certifique-se de que as permissões de acesso de base de dados são os mesmos na nova base de dados de armazém de dados, tal como estavam na base de dados de armazém de dados original.  

2. Utilize a consola do Configuration Manager para remover a função de ponto de serviço de armazém de dados do servidor atual.  

3. Reinstale o ponto de serviço do armazém de dados. Especifique o nome do novo SQL Server e instância que aloja a base de dados do armazém de dados restaurados.  

4. Depois de instala a função de sistema de sites, a migração está concluída.  



## <a name="troubleshooting"></a>Resolução de Problemas 

### <a name="log-files"></a>Ficheiros de registo 

Utilize os seguintes registos para investigar problemas com a instalação do ponto de serviço do armazém de dados ou sincronização de dados:

- **DWSSMSI.log** e **DWSSSetup.log**: Utilize estes registos para investigar erros ao instalar o ponto de serviço do armazém de dados.  

- **Microsoft.ConfigMgrDataWarehouse.log**: Utilize este registo para investigar a sincronização de dados entre a base de dados na base de dados do armazém de dados.  


### <a name="set-up-failure"></a>Configurar a falha 

Quando a função de ponto de serviço de armazém de dados é o primeiro que instalar num servidor remoto, a instalação falha para o armazém de dados.  

#### <a name="workaround"></a>Solução 
Certifique-se de que o computador no qual instala o serviço de armazém de dados ponto já anfitriões pelo menos uma outra função.  


### <a name="synchronization-failed-to-populate-schema-objects"></a>Falha na sincronização preencher os objetos de esquema 

A sincronização falha com a seguinte mensagem no **Microsoft.ConfigMgrDataWarehouse.log**: `failed to populate schema objects`

#### <a name="workaround"></a>Solução 
Certifique-se de que a conta de computador da função de sistema de sites é um **db_owner** na base de dados de armazém de dados.


### <a name="reports-fail-to-open"></a>Relatórios de não conseguem abrir

Relatórios do armazém de dados não abrirá quando a base de dados do armazém de dados e o ponto de serviço do reporting estiverem em diferentes sistemas de site.  

#### <a name="workaround"></a>Solução
Conceder a **conta do ponto de Reporting Services** a **db_datareader** permissão na base de dados do armazém de dados.


### <a name="error-opening-reports"></a>Erro ao abrir relatórios

Quando abre um relatório de armazém de dados, ele retorna o seguinte erro:

```
An error has occurred during report processing. (rsProcessingAborted)
Cannot create a connection to data source 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection)
A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)
```

#### <a name="workaround"></a>Solução 
Utilize os seguintes passos para configurar certificados:

1. No computador que aloja a base de dados do armazém de dados:  

    1. IIS aberto, selecione **certificados de servidor**e, em seguida, clique em **Criar certificado autoassinado**. Em seguida, especifique o "nome amigável" do nome do certificado como **Data Warehouse SQL Server Identification Certificate**. Selecione o arquivo de certificados como **pessoais**.  

    2. Abra o **Gestor de Configuração do SQL Server**. Sob **configuração de rede do SQL Server**, botão direito do mouse para selecionar **propriedades** sob **protocolos para MSSQLSERVER**. Mude para o **certificado** separador, selecione **Data Warehouse SQL Server Identification Certificate** como o certificado e, em seguida, guarde as alterações.  

    3. Na **Gestor de configuração do SQL Server**, em **dos serviços do SQL Server**, reinicie o **serviço do SQL Server**. Se o SQL Reporting Services também está instalado no servidor que aloja a base de dados do armazém de dados, reinicie **Reporting Service** serviços também.  

    4. Abra a consola de gestão da Microsoft (MMC) e adicione a **certificados** snap-in. Selecione **conta de computador** da máquina local. Expanda a **pessoais** pasta e selecione **certificados**. Exportar os **Data Warehouse SQL Server Identification Certificate** como um **binário codificado DER X.509 (. CER)** ficheiro.  

2. No computador que aloja o SQL Server Reporting Services, abra a MMC e adicione a **certificados** snap-in. Selecione **conta de computador**. Sob o **autoridades de certificação de raiz confiáveis** pasta, importar os **Data Warehouse SQL Server Identification Certificate**.  



## <a name="data-flow"></a>Fluxo de dados   

![Diagrama que mostra o fluxo de dados lógicos entre componentes do site para o armazém de dados](./media/datawarehouse.png)

#### <a name="data-storage-and-synchronization"></a>Armazenamento de dados e sincronização

| Passo   | Detalhes  |
|--------|----------|  
| **1**  | O servidor do site transfere e armazena dados na base de dados do site. |  
| **2**  | Com base na sua agenda e a configuração, o ponto de serviço do armazém de dados obtém os dados da base de dados do site. |  
| **3**  | O ponto de serviço do armazém de dados transferidos e armazena uma cópia dos dados sincronizados na base de dados do armazém de dados. |  


#### <a name="reporting"></a>Relatórios

| Passo   | Detalhes  |
|--------|----------|  
| **A**  | Utilizar relatórios incorporados, um utilizador solicita dados. Este pedido é passado para o ponto do service reporting utilizando o SQL Server Reporting Services. |  
| **B**  | A maioria dos relatórios são para obter informações atuais, e estes pedidos são executados na base de dados do site. |  
| **C**  | Quando um relatório solicita dados históricos utilizando um dos relatórios com uma *categoria* dos **armazém de dados**, o pedido for executado relativamente a base de dados do armazém de dados. |  

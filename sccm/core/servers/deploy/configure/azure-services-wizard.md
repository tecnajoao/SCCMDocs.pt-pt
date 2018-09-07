---
title: Configurar os serviços do Azure
titleSuffix: Configuration Manager
description: Ligar o seu ambiente do Configuration Manager com serviços do Azure para gestão na cloud, preparação de atualizações, Microsoft Store para empresas e o Log Analytics.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ea47941be51d1bf38de53203aad00c02d0a11d3
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893775"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configurar os serviços do Azure para utilização com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilizar o **Assistente de serviços do Azure** para simplificar o processo de configuração de serviços cloud do Azure que utiliza com o Configuration Manager. Este assistente fornece uma experiência de configuração comuns ao utilizar registos de aplicações web do Azure Active Directory (Azure AD). Estas aplicações fornecem detalhes de subscrição e a configuração e autenticar as comunicações com o Azure AD. A aplicação substitui introduzir essas mesmas informações sempre que configurou um novo componente do Configuration Manager ou o serviço com o Azure.



## <a name="available-services"></a>Serviços disponíveis

Configure os seguintes serviços do Azure, utilizar este assistente:  

-   **Gestão da cloud**: Este serviço permite que os clientes autenticar através da utilização do Azure AD e o site. Esta autenticação permite que outros cenários, tais como:  

    - [Instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

    - [Configurar a deteção de utilizador do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - Suporte a determinados [cenários de gateway de gestão na cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#scenarios)  

-   **Conector de análise de registo**: [Ligar ao Azure Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics). Sincronizar dados de coleção para o Log Analytics.  

    > [!Note]  
    > Este artigo refere-se para o *conector do Log Analytics*, que era anteriormente denominado o *conector OMS*. Não existe nenhuma diferença funcional. Para obter mais informações, consulte [gestão do Azure - monitorização](https://docs.microsoft.com/azure/monitoring/#operations-management-suite).  

-   **Conector do Upgrade Readiness**: Ligar ao Windows Analytics [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics). Ver dados de compatibilidade da atualização de cliente.  

-   **Microsoft Store para empresas**: Ligar para o [Microsoft Store para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business). Obter aplicações da loja para a sua organização que pode implementar com o Configuration Manager.  

### <a name="service-details"></a>Detalhes do serviço

A tabela seguinte lista os detalhes sobre cada um dos serviços.  

- **Os inquilinos**: O número de instâncias de serviço, que pode configurar. Cada instância tem de ser um inquilino do Azure distinto.  

- **Nuvens**: Todos os serviços suportam a cloud global do Azure, mas nem todos os serviços suporte nuvens privadas, tais como a cloud do Azure US Government.  

- **Aplicação Web**: Se o serviço utiliza uma aplicação do Azure AD do tipo *aplicação Web / API*, também referido como uma aplicação de servidor no Configuration Manager.  

- **Aplicação nativa**: Se o serviço utiliza uma aplicação do Azure AD do tipo *nativo*, também referido como uma aplicação de cliente no Configuration Manager.  

- **Ações**: Se pode importar ou criar estas aplicações no Assistente de serviços do Configuration Manager do Azure.  


|Serviço  |Inquilinos  |Clouds  |Aplicação Web  |Aplicação nativa  |Ações  |
|---------|---------|---------|---------|---------|---------|
|Gestão da cloud com</br>Deteção de utilizador do Azure AD | Vários | Público | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | Importar, criar |
|Conector do log Analytics | Um | Público, privado | ![Suportado](media/green_check.png) | ![Não suportado](media/Red_X.png) | Importar |
|Preparação para atualização | Um | Público | ![Suportado](media/green_check.png) | ![Não suportado](media/Red_X.png) | Importar |
|Microsoft Store para</br>negócios | Um | Público | ![Suportado](media/green_check.png) | ![Não suportado](media/Red_X.png) | Importar, criar |


### <a name="about-azure-ad-apps"></a>Sobre as aplicações do Azure AD

Diferentes serviços do Azure requerem diferentes configurações, o que fizer no portal do Azure. Além disso, as aplicações para cada serviço podem exigir permissões separadas a recursos do Azure.  

Pode usar um único aplicativo para vários serviços. Existe apenas um objeto para gerir no Configuration Manager e o Azure AD. Quando a chave de segurança na aplicação expira, só tem de atualizar uma chave.

A configuração mais segura está a utilizar aplicações separadas para cada serviço. Uma aplicação para um serviço pode requerer permissões adicionais que não necessita de outro serviço. A utilização de uma aplicação para diferentes serviços pode fornecer a aplicação com mais permissões do que de outra forma requer. 

Ao criar serviços do Azure adicionais no assistente, Configuration Manager foi projetado para reutilizar as informações que são comuns entre serviços. Este comportamento ajuda-a necessidade das mesmas informações de entrada várias vezes. 

Para obter mais informações sobre as permissões de aplicação necessária e configurações para cada serviço, consulte o artigo de Configuration Manager relevantes na [serviços disponíveis](#available-services). 

Para obter mais informações sobre as aplicações do Azure, comece com os seguintes artigos:
- [Autenticação e autorização no serviço de aplicações do Azure](/azure/app-service/app-service-authentication-overview)
- [Descrição geral de aplicações Web](/azure/app-service-web/app-service-web-overview)
- [Noções básicas do registo de aplicações no Azure AD](/azure/active-directory/develop/active-directory-authentication-scenarios#basics-of-registering-an-application-in-azure-ad)  
- [Registar a sua aplicação com o seu inquilino do Azure Active Directory](/azure/active-directory/active-directory-app-registration)



## <a name="before-you-begin"></a>Antes de começar

Depois de decidir o serviço ao qual pretende ligar, consulte a tabela na [detalhes do serviço](#service-details). Esta tabela fornece informações de que precisa para concluir o Assistente de serviço do Azure. Ter uma discussão com antecedência com o administrador do Azure AD. Decida se cria manualmente as aplicações com antecedência no portal do Azure e, em seguida, importar os detalhes da aplicação para o Configuration Manager. Ou utilize o Gestor de configuração para criar diretamente as aplicações no Azure AD. Para recolher os dados necessários do Azure AD, reveja as informações em outras seções deste artigo.

Alguns serviços requerem as aplicações do Azure AD tenham permissões específicas. Reveja as informações para cada serviço determinar todas as permissões necessárias. Por exemplo, antes de pode importar uma aplicação web, um administrador do Azure tem primeiro de criá-lo na [portal do Azure](https://portal.azure.com). Ao configurar a preparação de atualizações ou o conector do Log Analytics, que deve fornecer a sua aplicação web recentemente registada *contribuinte* permissão no grupo de recursos que contém a área de trabalho relevante. Esta permissão permite ao Configuration Manager para aceder a essa área de trabalho. Ao atribuir a permissão, procure o nome do registo de aplicações no **adicionar utilizadores** área do portal do Azure. Este processo é o mesmo que quando [fornecer do Configuration Manager com permissões para o Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics). Um administrador do Azure tem de atribuir estas permissões antes de importar a aplicação para o Configuration Manager.



## <a name="start-the-azure-services-wizard"></a>Iniciar o Assistente de serviços do Azure

1.  Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **serviços Cloud**e selecione o **dos serviços do Azure** nó.  

2.  Sobre o **home page** separador do Friso, na **dos serviços do Azure** , clique em **configurar os serviços do Azure**.  

3.  Sobre o **dos serviços do Azure** página do Assistente de serviços do Azure:  

    1. Especifique um **nome** para o objeto no Configuration Manager.  

    2. Especifique um opcional **Descrição** para ajudar a identificar o serviço.  

    3. Selecione o serviço do Azure que pretende estabelecer ligação com o Configuration Manager.  

4. Clique em **próxima** para continuar para o [as propriedades da aplicação do Azure](#azure-app-properties) página do Assistente de serviços do Azure.  



## <a name="azure-app-properties"></a>Propriedades da aplicação do Azure

Na **App** página do Assistente de serviços do Azure, selecione a **ambiente do Azure** da lista. Consulte a tabela na [detalhes do serviço](#service-details) para que ambiente está atualmente disponível para o serviço.

O restante da página da aplicação varia consoante o serviço específico. Consulte a tabela na [detalhes do serviço](#service-details) para o serviço de que tipo de aplicação utiliza e a ação, pode utilizar. 
- Se a aplicação suporta ambas as importação e cria as ações, clique em **procurar**. Esta ação abre o [caixa de diálogo de aplicativo de servidor](#server-app-dialog) ou o [caixa de diálogo da aplicação de cliente](#client-app-dialog).
- Se a aplicação só suporta a ação de importação, clique em **importar**. Esta ação abre o [caixa de diálogo Importar aplicações (servidor)](#import-apps-dialog-server) ou o [caixa de diálogo Importar aplicações (cliente)](#import-apps-dialog-client).

Depois de especificar as aplicações nesta página, clique em **próxima** para continuar para o [configuração ou a deteção de](#configuration-or-discovery) página do Assistente de serviços do Azure.

### <a name="web-app"></a>Aplicação Web

Esta aplicação é o tipo do Azure AD *aplicação Web / API*, também referido como uma aplicação de servidor no Configuration Manager.

#### <a name="server-app-dialog"></a>Caixa de diálogo de aplicativo de servidor

Quando clica em **navegue** para o **aplicação Web** na página da aplicação do Assistente de serviços do Azure, é aberta a caixa de diálogo de aplicação de servidor. Ele apresenta uma lista que mostra as seguintes propriedades de todas as aplicações web existente:
- Nome amigável de inquilino
- Nome amigável de aplicação
- Tipo de serviço

Existem três ações que pode demorar entre a caixa de diálogo de aplicação de servidor:
- Para reutilizar uma aplicação web existente, selecione-o na lista. 
- Clique em **importação** para abrir o [caixa de diálogo Importar aplicações](#import-apps-dialog-server).
- Clique em **Create** para abrir o [caixa de diálogo Criar aplicação de servidor](#create-server-application-dialog).

Depois de selecionar, importar ou criar uma aplicação web, clique em **OK** para fechar a caixa de diálogo de aplicação de servidor. Esta ação devolve para o [página da aplicação](#azure-app-properties) do Assistente de serviços do Azure.

#### <a name="import-apps-dialog-server"></a>Caixa de diálogo Importar aplicações (servidor)

Quando clica em **importação** a partir da caixa de diálogo do aplicativo de servidor ou a página de aplicações do Assistente de serviços do Azure, é aberta a caixa de diálogo de aplicações de importação. Esta página permite-lhe introduzir informações sobre uma aplicação web do Azure AD que já foi criada no portal do Azure. Importa os metadados sobre essa aplicação web para o Configuration Manager. Especifique as seguintes informações:
- **Nome de inquilino do Azure AD**
- **ID de inquilino do Azure AD**
- **Nome da aplicação**: Um nome amigável para a aplicação.
- **ID de cliente**
- **Chave secreta**
- **Expiração da chave secreta**: Selecione uma data futura do calendário. 
- **URI de ID de aplicação**: Este valor tem de ser exclusivo no seu inquilino do Azure AD. É no token de acesso utilizado pelo cliente do Configuration Manager para pedir acesso ao serviço. Por predefinição, este valor é https://ConfigMgrService.  

Após introduzir as informações, clique em **Verifique se**. Em seguida, clique em **OK** para fechar a caixa de diálogo de aplicações de importação. Esta ação devolve para o a [página da aplicação](#azure-app-properties) do Assistente de serviços do Azure, ou o [caixa de diálogo de aplicativo de servidor](#server-app-dialog).

#### <a name="create-server-application-dialog"></a>Criar aplicação de servidor caixa de diálogo

Quando clica em **criar** caixa de diálogo da aplicação de servidor, é aberta a caixa de diálogo Criar aplicação de servidor. Esta página automatiza a criação de uma aplicação web no Azure AD. Especifique as seguintes informações:
- **Nome da aplicação**: Um nome amigável para a aplicação.
- **URL da home page**: Este valor não é utilizado pelo Configuration Manager, mas necessários pelo Azure AD. Por predefinição, este valor é https://ConfigMgrService.  
- **URI de ID de aplicação**: Este valor tem de ser exclusivo no seu inquilino do Azure AD. É no token de acesso utilizado pelo cliente do Configuration Manager para pedir acesso ao serviço. Por predefinição, este valor é https://ConfigMgrService.  
- **Período de validade de chave secreto**: clique na lista pendente e selecione **1 ano** ou **2 anos**. Um ano é o valor predefinido.

Clique em **iniciar sessão** para autenticar para o Azure como um utilizador administrativo. Estas credenciais não são guardadas pelo Configuration Manager. Essa pessoa não requer permissões no Configuration Manager e não precisa de ser a mesma conta que executa o Assistente de serviços do Azure. Após a autenticação bem-sucedida para o Azure, a página mostra os **nome de inquilino do Azure AD** para referência. 

Clique em **OK** para criar a aplicação web no Azure AD e fechar a caixa de diálogo Criar aplicação de servidor. Esta ação devolve para o [caixa de diálogo de aplicativo de servidor](#server-app-dialog).


### <a name="native-client-app"></a>Aplicação de cliente nativo
    
Esta aplicação é o tipo do Azure AD *nativo*, também referido como uma aplicação de cliente no Configuration Manager.

#### <a name="client-app-dialog"></a>Caixa de diálogo de aplicação de cliente

Quando clica em **navegue** para o **aplicação de cliente nativo** na página da aplicação do Assistente de serviços do Azure, é aberta a caixa de diálogo da aplicação de cliente. Ele apresenta uma lista que mostra as seguintes propriedades de quaisquer aplicações nativas existentes:
- Nome amigável de inquilino
- Nome amigável de aplicação
- Tipo de serviço

Existem três ações que pode demorar entre a caixa de diálogo da aplicação de cliente:
- Para reutilizar uma aplicação nativa existente, selecione-o na lista. 
- Clique em **importação** para abrir o [caixa de diálogo Importar aplicações](#import-apps-dialog-client).
- Clique em **Create** para abrir o [caixa de diálogo Criar aplicação de cliente](#create-client-application-dialog).

Depois de selecionar, importe ou crie uma aplicação nativa, clique em **OK** para fechar a caixa de diálogo da aplicação de cliente. Esta ação devolve para o [página da aplicação](#azure-app-properties) do Assistente de serviços do Azure.

#### <a name="import-apps-dialog-client"></a>Caixa de diálogo Importar aplicações (cliente)

Quando clica em **importação** a caixa de diálogo de aplicação de cliente, ela abre a caixa de diálogo de aplicações de importação. Esta página permite-lhe introduzir informações sobre uma aplicação nativa do Azure AD que já foi criada no portal do Azure. Importa os metadados sobre essa aplicação nativa para o Configuration Manager. Especifique as seguintes informações:
- **Nome da aplicação**: Um nome amigável para a aplicação.
- **ID de cliente** 

Após introduzir as informações, clique em **Verifique se**. Em seguida, clique em **OK** para fechar a caixa de diálogo de aplicações de importação. Esta ação devolve para o [caixa de diálogo da aplicação de cliente](#client-app-dialog).

#### <a name="create-client-application-dialog"></a>Criar caixa de diálogo do aplicativo cliente

Quando clica em **criar** a caixa de diálogo de aplicação de cliente, ela abre a caixa de diálogo Criar aplicação de cliente. Esta página automatiza a criação de uma aplicação nativa no Azure AD. Especifique as seguintes informações:
- **Nome da aplicação**: Um nome amigável para a aplicação.
- **URL de resposta**: Este valor não é utilizado pelo Configuration Manager, mas necessários pelo Azure AD. Por predefinição, este valor é https://ConfigMgrService. 

Clique em **iniciar sessão** para autenticar para o Azure como um utilizador administrativo. Estas credenciais não são guardadas pelo Configuration Manager. Essa pessoa não requer permissões no Configuration Manager e não precisa de ser a mesma conta que executa o Assistente de serviços do Azure. Após a autenticação bem-sucedida para o Azure, a página mostra os **nome de inquilino do Azure AD** para referência. 

Clique em **OK** para criar a aplicação nativa no Azure AD e fechar a caixa de diálogo Criar aplicação de cliente. Esta ação devolve para o [caixa de diálogo da aplicação de cliente](#client-app-dialog).


## <a name="configuration-or-discovery"></a>Configuração ou a deteção

Depois de especificar as aplicações web e nativas na página de aplicações, o Assistente de serviços do Azure continua a qualquer uma um **Configuration** ou **deteção** página, de acordo com o serviço ao qual está a ligar. Os detalhes desta página variam a partir de serviços. Para obter mais informações, consulte um dos seguintes artigos:  

-   **Gestão da cloud** serviço, **deteção** página: [Configurar a deteção de utilizador do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

-   **Conector de análise de registo** serviço, **configuração** página: [Configurar a ligação para o Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics#configure-the-connection-to-log-analytics)  

-   **Conector do Upgrade Readiness** serviço, **configuração** página: [Utilize o Assistente do Azure para criar a ligação](/sccm/core/clients/manage/upgrade/upgrade-analytics#use-the-azure-wizard-to-create-the-connection)  

-   **Microsoft Store para empresas** serviço, **configurações** página: [Configurar o Microsoft Store para a sincronização de negócios](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#bkmk_config)  


Por fim, conclua o Assistente de serviços do Azure através das páginas de resumo, o progresso e conclusão. Concluiu a configuração de um serviço do Azure no Configuration Manager. Repita este processo para configurar outros serviços do Azure.


## <a name="view-the-configuration-of-an-azure-service"></a>Ver a configuração de um serviço do Azure
Ver as propriedades de um serviço do Azure que configurou para utilização. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **serviços Cloud**e selecione **dos serviços do Azure**. Selecione o serviço que pretende ver ou editar e, em seguida, clique em **propriedades**.

Se selecionar um serviço e, em seguida, clique em **eliminar** na faixa de opções, esta ação elimina a ligação no Configuration Manager. Ele não remove a aplicação no Azure AD. Peça ao seu administrador do Azure para eliminar a aplicação quando já não for necessário. Ou execute o Assistente de serviço do Azure para importar a aplicação.<!--483440-->


## <a name="cloud-management-data-flow"></a>Fluxo de dados de gestão na cloud

O diagrama a seguir é um fluxo de dados conceitual para a interação entre o Configuration Manager, do Azure AD e ligados a serviços cloud. Este exemplo específico utiliza a **gestão na Cloud** service, que inclui um cliente do Windows 10 e servidor e aplicações de cliente. Os fluxos de outros serviços são semelhantes.

![Diagrama de fluxo de dados para o Configuration Manager com o Azure AD e gestão da Cloud](media/aad-auth.png)

1.  Administrador do Configuration Manager importa ou cria as aplicações de cliente e servidor no Azure AD.  

2.  Método de deteção de utilizador do Gestor de configuração do Azure AD é executado. O site utiliza o token de aplicação de servidor do Azure AD para consultar o Microsoft Graph para objetos de utilizador.  

3.  O site armazena os dados sobre os objetos de utilizador. Para obter mais informações, consulte [do Azure AD User Discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).  

4.  O cliente do Configuration Manager solicita o token de utilizador do Azure AD. O cliente faz a afirmação com o ID da aplicação de cliente do Azure AD e a aplicação de servidor como o público-alvo. Para obter mais informações, consulte [afirmações nos Tokens de segurança do Azure AD](/azure/active-directory/develop/active-directory-authentication-scenarios#claims-in-azure-ad-security-tokens).  

5.  O cliente é autenticado com o site ao apresentar o token do Azure AD para o gateway de gestão na cloud e/ou no local ponto de gestão ativado para HTTPS.  



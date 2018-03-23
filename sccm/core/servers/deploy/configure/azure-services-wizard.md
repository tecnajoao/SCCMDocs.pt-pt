---
title: Configurar os serviços do Azure
titleSuffix: Configuration Manager
description: Ligar o seu ambiente do Configuration Manager com os serviços do Azure para a gestão de nuvem, preparação da atualização, Microsoft Store para empresas e o Operations Management Suite.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b86c73f3f5662a00ca0b7f80b0c785c37aff0b1a
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configurar os serviços do Azure para utilização com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize o **Assistente de serviços do Azure** para simplificar o processo de configuração de cloud services do Azure utiliza com o Configuration Manager. Este assistente fornece uma experiência de configuração comum com registos de aplicação de web do Azure Active Directory (Azure AD). Estas aplicações fornecem detalhes da subscrição e a configuração e autenticar as comunicações com o Azure AD. A aplicação substitui introduzir esta mesma informação sempre que configurou um novo componente do Configuration Manager ou o serviço com o Azure.



## <a name="available-services"></a>Serviços disponíveis

Configure os seguintes serviços do Azure utilizar este assistente:  

-   **Gestão de nuvem**: Este serviço permite que o site e os clientes para autenticar através da utilização do Azure AD. Esta autenticação permite que outros cenários, tais como:  

    - [Instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

    - [Configurar a deteção de utilizador do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - Suporta determinados [cenários de gestão de gateway de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#scenarios)  

-   **Conector do OMS**: [Ligar ao Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS). Sincronizar os dados, como coleções para análise de registos do OMS.  

-   **Atualizar o conector de preparação**: Ligar à análise do Windows [preparação para a atualização](/sccm/core/clients/manage/upgrade/upgrade-analytics). Ver dados de compatibilidade de atualização de cliente.  

-   **Microsoft loja para empresas**: Ligar para o [Microsoft loja para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business). Obter aplicações da loja para a sua organização que pode implementar com o Configuration Manager.  

### <a name="service-details"></a>Detalhes do serviço

A tabela seguinte lista os detalhes sobre cada um dos serviços.  

- **Os inquilinos**: O número de instâncias de serviço, que pode configurar. Cada instância tem de ser um inquilino do Azure distinto.  

- **Nuvens**: Suportam todos os serviços de nuvem global do Azure, mas nem todos os serviços suporte nuvens privadas, tais como a nuvem do Azure US Government.  

- **Aplicação Web**: Indica se o serviço utiliza uma aplicação do Azure AD do tipo *aplicação Web / API*, também referido como uma aplicação de servidor no Configuration Manager.  

- **Aplicação nativa**: Indica se o serviço utiliza uma aplicação do Azure AD do tipo *nativo*, também referido como uma aplicação de cliente no Configuration Manager.  

- **Ações**: Indica se pode importar ou criar estas aplicações o Assistente de serviços do Configuration Manager do Azure.  


|Serviço  |Inquilinos  |Clouds  |Aplicação Web  |Aplicação nativa  |ações  |
|---------|---------|---------|---------|---------|---------|
|Gestão de nuvem com o</br>Deteção de utilizador do Azure AD | Vários | Público | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | Importar, crie |
|Conector do OMS | um | Público, privado | ![Suportado](media/green_check.png) | ![Não suportado](media/Red_X.png) | Importar |
|Preparação para a atualização | um | Público | ![Suportado](media/green_check.png) | ![Não suportado](media/Red_X.png) | Importar |
|Loja Microsoft para</br>Empresariais e as educação | um | Público | ![Suportado](media/green_check.png) | ![Não suportado](media/Red_X.png) | Importar, crie |


### <a name="about-azure-ad-apps"></a>Sobre as aplicações do Azure AD

Serviços do Azure diferentes requerem configurações diferentes, o que fazer no portal do Azure. Além disso, as aplicações para cada serviço podem requerem permissões separadas para recursos do Azure.  

Pode utilizar uma única aplicação para vários serviços. Não há apenas um objeto para gerir no Configuration Manager e o Azure AD. Quando expira a chave de segurança da aplicação, apenas terá de atualizar uma chave.

A configuração mais segura está a utilizar aplicações separadas para cada serviço. Uma aplicação para um serviço pode requerer permissões adicionais que não necessita de outro serviço. Utilizar uma aplicação para diferentes serviços pode fornecer a aplicação com mais permissões do requer caso contrário. 

Quando criar serviços Azure adicionais no assistente, o Configuration Manager foi concebido para reutilizar as informações que são comuns entre os serviços. Este comportamento ajuda-o a necessidade de introduzir as mesmas informações várias vezes. 

Para obter mais informações sobre as permissões de aplicações necessárias e as configurações para cada serviço, consulte o artigo de Configuration Manager relevantes no [serviços disponíveis](#available-services). 

Para obter mais informações sobre as aplicações do Azure, comece com os seguintes artigos:
- [Autenticação e autorização no serviço de aplicações do Azure](/azure/app-service/app-service-authentication-overview)
- [Descrição geral de aplicações Web](/azure/app-service-web/app-service-web-overview)
- [Noções básicas de registar uma aplicação no Azure AD](/azure/active-directory/develop/active-directory-authentication-scenarios#basics-of-registering-an-application-in-azure-ad)  
- [Registar a aplicação com o seu inquilino do Azure Active Directory](/azure/active-directory/active-directory-app-registration)



## <a name="before-you-begin"></a>Antes de começar

Depois de decidir o serviço ao qual pretende ligar, consulte a tabela [detalhes do serviço](#service-details). Esta tabela fornece informações de que precisa para concluir o Assistente de serviço do Azure. Ter um debate antecipadamente com o seu administrador do Azure AD. Decida se criar manualmente as aplicações antecipadamente no portal do Azure e, em seguida, importar os detalhes da aplicação para o Configuration Manager. Ou utilize o Gestor de configuração para criar diretamente as aplicações no Azure AD. Para recolher os dados necessários do Azure AD, reveja as informações nas secções deste artigo.

Alguns serviços necessitam de aplicações do Azure AD para ter permissões específicas. Reveja as informações para cada serviço determinar as permissões necessárias. Por exemplo, antes de importar uma aplicação web, um administrador do Azure tem primeiro de criar no [portal do Azure](https://portal.azure.com). Quando configurar preparação de atualização ou o conector do OMS, terá de conceder a sua aplicação web recentemente registado *contribuinte* permissão no grupo de recursos que contém a área de trabalho do OMS relevante. Esta permissão permite que o Configuration Manager para aceder à área de trabalho. Procure o nome do registo de aplicação no **adicionar utilizadores** painel ao atribuir a permissão. Este processo é o mesmo quando [fornecer do Configuration Manager permissões ao OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms). Um administrador do Azure tem de atribuir estas permissões antes de importar a aplicação para o Configuration Manager.



## <a name="start-the-azure-services-wizard"></a>Iniciar o Assistente de serviços do Azure

1.  Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **serviços Cloud**e selecione o **serviços do Azure** nós.  

2.  No **home page** separador do Friso, no **serviços do Azure** , clique em **configurar os serviços do Azure**.  

3.  No **serviços do Azure** página do Assistente de serviços do Azure:  

    1. Especifique um **nome** para o objeto no Configuration Manager.  

    2. Especifique um opcional **Descrição** para o ajudar a identificar o serviço.  

    3. Selecione o serviço do Azure que pretende estabelecer ligação com o Configuration Manager.  

4. Clique em **seguinte** para avançar para o [as propriedades da aplicação do Azure](#azure-app-properties) página do Assistente de serviços do Azure.  



## <a name="azure-app-properties"></a>Propriedades da aplicação do Azure

No **aplicação** página do Assistente de serviços do Azure, selecione o **ambiente do Azure** da lista. Consulte a tabela [detalhes do serviço](#service-details) para o ambiente está atualmente disponível para o serviço.

O resto da página da aplicação varia consoante o serviço específico. Consulte a tabela [detalhes do serviço](#service-details) para o tipo de aplicação de serviço utiliza e a ação pode utilizar. 
- Se a aplicação suporta ambos os importar e cria as ações, clique em **procurar**. Esta ação abre o [caixa de diálogo de aplicação de servidor](#server-app-dialog) ou [caixa de diálogo de aplicação de cliente](#client-app-dialog).
- Se a aplicação suporta apenas a ação de importação, clique em **importar**. Esta ação abre o [caixa de diálogo Importar aplicações (servidor)](#import-apps-dialog-server) ou [caixa de diálogo Importar aplicações (cliente)](#import-apps-dialog-client).

Depois de especificar as aplicações nesta página, clique em **seguinte** para avançar para o [configuração ou deteção](#configuration-or-discovery) página do Assistente de serviços do Azure.

### <a name="web-app"></a>Aplicação Web

Esta aplicação é o tipo do Azure AD *aplicação Web / API*, também referido como uma aplicação de servidor no Configuration Manager.

#### <a name="server-app-dialog"></a>Caixa de diálogo de aplicação de servidor

Ao clicar em **procurar** para o **aplicação Web** na página da aplicação do Assistente de serviços do Azure, é aberta a caixa de diálogo de aplicação de servidor. Apresenta uma lista que mostra as seguintes propriedades de quaisquer aplicações web existentes:
- Nome amigável do inquilino
- Nome amigável da aplicação
- Tipo de serviço

Existem três ações que pode tomar a caixa de diálogo de aplicação de servidor:
- Para reutilizar uma aplicação web existente, selecione-o da lista. 
- Clique em **importação** para abrir o [caixa de diálogo de aplicações de importação](#import-apps-dialog-server).
- Clique em **criar** para abrir o [caixa de diálogo Criar aplicação de servidor](#create-server-application-dialog).

Depois de selecionar, importar ou criar uma aplicação web, clique em **OK** para fechar a caixa de diálogo de aplicação de servidor. Esta ação devolve para o [página da aplicação](#azure-app-properties) do Assistente de serviços do Azure.

#### <a name="import-apps-dialog-server"></a>Caixa de diálogo Importar aplicações (servidor)

Ao clicar em **importação** da caixa de diálogo da aplicação de servidor ou na página da aplicação do Assistente de serviços do Azure, é aberta a caixa de diálogo de aplicações de importação. Esta página permite-lhe introduzir informações sobre uma aplicação web do Azure AD que já está a ser criada no portal do Azure. Importa os metadados sobre essa aplicação web para o Configuration Manager. Especifique as seguintes informações:
- **Nome de inquilino do Azure AD**
- **ID de inquilino do Azure AD**
- **Nome da aplicação**: Um nome amigável para a aplicação.
- **ID de cliente**
- **Chave secreta**
- **Expiração de chave secreta**: Selecione uma data futura no calendário. 
- **URI de ID de aplicação**: Este valor tem de ser exclusivo no seu inquilino do Azure AD. É no token de acesso utilizado pelo cliente do Configuration Manager para pedir acesso ao serviço. Por predefinição, este valor é https://ConfigMgrService.  

Depois de introduzir as informações, clique em **verifique**. Em seguida, clique em **OK** para fechar a caixa de diálogo de aplicações de importação. Esta ação devolve para o [página da aplicação](#azure-app-properties) do Assistente de serviços do Azure, ou o [caixa de diálogo de aplicação de servidor](#server-app-dialog).

#### <a name="create-server-application-dialog"></a>Criar caixa de diálogo de aplicação de servidor

Ao clicar em **criar** da caixa de diálogo de aplicação de servidor, é aberta a caixa de diálogo Criar aplicação de servidor. Esta página automatiza a criação de uma aplicação web no Azure AD. Especifique as seguintes informações:
- **Nome da aplicação**: Um nome amigável para a aplicação.
- **URL de home page**: Este valor não é utilizado pelo Configuration Manager, mas necessário pelo Azure AD. Por predefinição, este valor é https://ConfigMgrService.  
- **URI de ID de aplicação**: Este valor tem de ser exclusivo no seu inquilino do Azure AD. É no token de acesso utilizado pelo cliente do Configuration Manager para pedir acesso ao serviço. Por predefinição, este valor é https://ConfigMgrService.  
- **Período de validade de chave secreto**: clique na lista pendente e selecione **1 ano** ou **2 anos**. Um ano é o valor predefinido.

Clique em **sessão** autenticar no Azure como um utilizador administrativo. Estas credenciais não são gravadas pelo Configuration Manager. Esta pessoa não necessita de permissões no Configuration Manager e não tem de ser a mesma conta que executa o Assistente de serviços do Azure. Após a autenticação com êxito no Azure, a página mostra o **nome de inquilino do Azure AD** para referência. 

Clique em **OK** para criar a aplicação web no Azure AD e fechar a caixa de diálogo Criar aplicação de servidor. Esta ação devolve para o [caixa de diálogo de aplicação de servidor](#server-app-dialog).


### <a name="native-client-app"></a>Aplicação cliente nativa
    
Esta aplicação é o tipo do Azure AD *nativo*, também referido como uma aplicação de cliente no Configuration Manager.

#### <a name="client-app-dialog"></a>Caixa de diálogo de aplicação de cliente

Ao clicar em **procurar** para o **aplicação cliente nativa** na página da aplicação do Assistente de serviços do Azure, é aberta a caixa de diálogo de aplicação de cliente. Apresenta uma lista que mostra as seguintes propriedades de quaisquer aplicações nativas existentes:
- Nome amigável do inquilino
- Nome amigável da aplicação
- Tipo de serviço

Existem três ações que pode tomar da caixa de diálogo de aplicação de cliente:
- Para reutilizar uma aplicação nativa existente, selecione-o da lista. 
- Clique em **importação** para abrir o [caixa de diálogo de aplicações de importação](#import-apps-dialog-client).
- Clique em **criar** para abrir o [caixa de diálogo Criar aplicação de cliente](#create-client-application-dialog).

Depois de selecionar, importar ou criar uma aplicação nativa, clique em **OK** para fechar a caixa de diálogo de aplicação de cliente. Esta ação devolve para o [página da aplicação](#azure-app-properties) do Assistente de serviços do Azure.

#### <a name="import-apps-dialog-client"></a>Caixa de diálogo Importar aplicações (cliente)

Ao clicar em **importação** da caixa de diálogo de aplicação de cliente, é aberta a caixa de diálogo de aplicações de importação. Esta página permite-lhe introduzir informações sobre uma aplicação nativa do Azure AD que já está a ser criada no portal do Azure. Importa os metadados sobre essa aplicação nativa para o Configuration Manager. Especifique as seguintes informações:
- **Nome da aplicação**: Um nome amigável para a aplicação.
- **ID de cliente** 

Depois de introduzir as informações, clique em **verifique**. Em seguida, clique em **OK** para fechar a caixa de diálogo de aplicações de importação. Esta ação devolve para o [caixa de diálogo de aplicação de cliente](#client-app-dialog).

#### <a name="create-client-application-dialog"></a>Criar caixa de diálogo de aplicação de cliente

Ao clicar em **criar** da caixa de diálogo de aplicação de cliente, é aberta a caixa de diálogo Criar aplicação de cliente. Esta página automatiza a criação de uma aplicação nativa no Azure AD. Especifique as seguintes informações:
- **Nome da aplicação**: Um nome amigável para a aplicação.
- **URL de resposta**: Este valor não é utilizado pelo Configuration Manager, mas necessário pelo Azure AD. Por predefinição, este valor é https://ConfigMgrService. 

Clique em **sessão** autenticar no Azure como um utilizador administrativo. Estas credenciais não são gravadas pelo Configuration Manager. Esta pessoa não necessita de permissões no Configuration Manager e não tem de ser a mesma conta que executa o Assistente de serviços do Azure. Após a autenticação com êxito no Azure, a página mostra o **nome de inquilino do Azure AD** para referência. 

Clique em **OK** para criar a aplicação nativa no Azure AD e fechar a caixa de diálogo Criar aplicação de cliente. Esta ação devolve para o [caixa de diálogo de aplicação de cliente](#client-app-dialog).


## <a name="configuration-or-discovery"></a>Configuração ou a deteção

Depois de especificar as aplicações nativas e web na página de aplicações, o Assistente de serviços do Azure continua como um **configuração** ou **deteção** página, consoante o serviço ao qual está a ligar. Os detalhes desta página variam para cada serviço. Para obter mais informações, consulte um dos seguintes artigos:  

-   **Gestão de nuvem** serviço, **deteção** página: [Configurar a deteção de utilizador do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

-   **Conector do OMS** serviço, **configuração** página: [Configurar a ligação ao OMS](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#use-the-azure-services-wizard-to-configure-the-connection-to-oms)  

-   **Atualizar o conector de preparação** serviço, **configuração** página: [Utilize o Assistente do Azure para criar a ligação](/sccm/core/clients/manage/upgrade/upgrade-analytics#use-the-azure-wizard-to-create-the-connection)  

-   **Microsoft Store para empresas** serviço, **configurações** página: [Configurar o Microsoft Store para a sincronização de negócio](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#for-configuration-manager-version-1706-and-later)  


Por fim, conclua o Assistente de serviços do Azure através de páginas de resumo, progresso e conclusão. Concluiu a configuração de um serviço do Azure no Configuration Manager. Repita este processo para configurar outros serviços do Azure.


## <a name="view-the-configuration-of-an-azure-service"></a>Ver a configuração de um serviço do Azure
Pode ver as propriedades de um serviço do Azure que configurou para utilização. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **serviços em nuvem**e selecione **serviços do Azure**. Selecione o serviço que pretende ver ou editar e, em seguida, clique em **propriedades**.

Se selecionar um serviço e, em seguida, clique em **eliminar** no Friso, esta ação elimina a ligação no Configuration Manager. Se não remove a aplicação no Azure AD. Peça ao seu administrador do Azure para eliminar a aplicação quando já não é necessário. Ou execute o Assistente de serviço do Azure para importar a aplicação.<!--483440-->


## <a name="cloud-management-data-flow"></a>Fluxo de dados de gestão de nuvem

O diagrama seguinte é um fluxo de dados conceptual para a interação entre o Configuration Manager, do Azure AD e ligada a serviços em nuvem. Este exemplo específico utiliza o **gestão de nuvem** serviço, que inclui um cliente do Windows 10 e servidor e as aplicações cliente. Os fluxos para outros serviços são semelhantes.

![Diagrama de fluxo de dados para o Configuration Manager com o Azure AD e gestão de nuvem](media/aad-auth.png)

1.  O administrador do Configuration Manager importa ou cria as aplicações de cliente e servidor no Azure AD.  

2.  Método de deteção de utilizador do Configuration Manager do Azure AD é executado. O site utiliza o token de aplicação de servidor do Azure AD para consulta Microsoft Graph para objetos de utilizador.  

3.  O site armazena os dados sobre os objetos de utilizador. Para obter mais informações, consulte [do Azure AD User Discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).  

4.  O token de utilizador do Azure AD os pedidos de cliente do Configuration Manager. O cliente efetua a afirmação com o ID da aplicação de cliente do Azure AD e a aplicação de servidor como o público-alvo. Para obter mais informações, consulte [afirmações em Tokens de segurança do Azure AD](/azure/active-directory/develop/active-directory-authentication-scenarios#claims-in-azure-ad-security-tokens).  

5.  O cliente efetua a autenticação com o site através da apresentação de token do Azure AD para o gateway de gestão de nuvem e/ou no local ponto de gestão ativado para HTTPS.  



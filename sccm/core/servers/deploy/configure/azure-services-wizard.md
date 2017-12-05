---
title: "Assistente de serviços do Azure"
titleSuffix: Configuration Manager
description: "Sobre o Assistente de serviços do Azure para o System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 7646e8bc368e5c01ddef41592c513f7bd1643cdb
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configurar os serviços do Azure para utilização com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir da versão do ramo atual 1706, o **Assistente de serviços do Azure** é utilizado para simplificar o processo de configuração dos serviços do Azure que utiliza com o Configuration Manager.

Este assistente fornece uma experiência de configuração comum utilizando um **registo de aplicação de web do Azure AD** para fornecer os detalhes da subscrição e a configuração e autenticar as comunicações com o Azure AD. A aplicação web substitui introduzir esta mesma informação sempre que configurou um novo componente do Configuration Manager ou o serviço com o Azure.

Os seguintes serviços do Azure podem ser configurados utilizando o Assistente de serviços do Azure:
-   **Gestão de nuvem**   
    [Permitir que os clientes autenticar com o Azure Active Directory](/sccm/core/clients/deploy/deploy-clients-cmg-azure) (Azure AD). Também pode [configurar a deteção de utilizador do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).
-   **Conector do OMS**
    [ligar ao Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS) e sincronizar os dados, como coleções para análise de registos do OMS.
-   **Preparação para a atualização**
    [ligar a preparação de atualização](/sccm/core/clients/manage/upgrade/upgrade-analytics) e ver os dados de compatibilidade de atualização de cliente.
-   **Microsoft Store para empresas** estabelecer ligação com o [Microsoft Store para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) e obter aplicações da sua organização que pode implementar com o Configuration Manager.

Ao utilizar o Assistente para configurar um serviço, várias ações comuns estão disponíveis.
Estas atualizações incluem:
-   *Configurar o ambiente do Azure*:  No **aplicação** página do assistente, selecione o **ambiente do Azure** que utilizar. Consulte o conteúdo para cada serviço saber se suporta apenas na nuvem pública do Azure, ou se pode suportar uma nuvem privada.
-   *Criar ou importar uma aplicação de servidor*:   No **aplicação** página do assistente, pode **criar** e **importação** metadados de registo de aplicação web do Azure. As opções disponíveis dependem do serviço que estiver a configurar. Além disso, alguns serviços poderão necessitar de uma aplicação adicional. Por exemplo, o **nuvem gestão** serviço requer um **aplicação cliente nativa** que é utilizado para clientes diretamente autenticar as comunicações com os serviços do Azure.


Para obter informações sobre aplicações web do Azure, consulte [autenticação e autorização no serviço de aplicações do Azure](/azure/app-service/app-service-authentication-overview), e [descrição geral das aplicações Web](/azure/app-service-web/app-service-web-overview).


## <a name="webapp"></a>Criar ou importar um registo de aplicação web do Azure Active Directory para utilização com o Configuration Manager

O registo de aplicação de web de serviços do Azure se liga o site do Configuration Manager para o Azure AD e é um pré-requisito para utilizar os serviços do Azure com a sua infraestrutura. Para efetuar este procedimento:

1.  No **administração** área de trabalho da consola do Configuration Manager, expanda **serviços em nuvem**e, em seguida, clique em **serviços do Azure**.
2.  No **home page** separador o **serviços do Azure** , clique em **configurar os serviços do Azure**.
3.  No **serviços do Azure** página do Assistente de serviços do Azure, selecione o serviço do Azure que pretende estabelecer ligação ao Configuration Manager.
4.  No **geral** página do assistente, especifique um nome e uma descrição para o serviço do Azure.
5.  No **aplicação** página do assistente, selecione o seu ambiente do Azure da lista e clique em **procurar** para selecionar o *aplicação Web* e *Native Client app* (apenas se for necessário) que será utilizado para configurar o serviço do Azure.

    **Aplicação Web:**   Procurar abre a janela de aplicação de servidor.    
      No **aplicação Server** janela, selecione a aplicação de servidor que pretende utilizar e, em seguida, clique em **OK**. Aplicações de servidor são registos de aplicação de web do Azure AD que contêm as configurações para a sua conta do Azure, incluindo o ID de inquilino, ID de cliente e uma chave secreta para clientes.
    Se não tiver uma aplicação disponível, utilize um dos seguintes:

    - **Criar**: Automatizar a criação de um registo de aplicação web do Azure AD com base nas informações de entrada na consola do Configuration Manager. Forneça um nome amigável para a aplicação, o URL de home page, URI de ID de aplicação e o período de validade da chave secreta. Por predefinição, o período de validade da chave secreta é um ano.
        
        Para continuar, alguém tem agora iniciar sessão com as suas credenciais do Azure AD para concluir a criação da aplicação web no Azure. A conta que utiliza para iniciar sessão no Azure não tem de ser a mesma conta que executa o Assistente de serviços do Azure. Depois de iniciarem sessão no Azure, o Configuration Manager cria a aplicação web no Azure para si, incluindo o ID de cliente e a chave secreta para utilização com a aplicação web. Mais tarde, pode ver estes do portal do Azure.

        Quando utiliza *criar* para configurar uma aplicação web, o Configuration Manager pode criar a aplicação web para si no Azure AD.
    
    - **Importar**: Introduza as informações sobre um registo de aplicação de web do Azure AD que já foi criado no **portal do Azure** para importar os metadados sobre esse registo para o Configuration Manager. Forneça um nome amigável para a aplicação e de inquilino e, em seguida, especifique o ID do inquilino, ID de cliente e a chave secreta para a aplicação web do Azure que pretende utilizar o Configuration Manager. Depois de verificar as informações, clique em **OK** para continuar.
        > [!NOTE]
        > Antes de **importação** pode ser utilizado, um registo de aplicações do Azure AD do tipo *aplicação Web / API* tem de ser criada no [portal do Azure](https://portal.azure.com). Para ler mais informações sobre como criar um registo de aplicação, consulte [registar a aplicação com o seu inquilino do Azure Active Directory](/azure/active-directory/active-directory-app-registration). Quando configurar a preparação de atualização ou o Operations Management Suite, também terá de conceder a sua aplicação web recentemente registado *contribuinte* permissões no grupo de recursos que contém a área de trabalho do OMS relevante para que Configuration Manager para conseguir aceder à área de trabalho. Para tal, terá de procurar o nome do registo de aplicação no **adicionar utilizadores** painel ao atribuir a permissão. Este é o mesmo processo que tem de ser seguido quando [fornecer do Configuration Manager permissões ao OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) para ligações ao [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm). Estas permissões devem ser atribuídas antes da aplicação é importada para o Configuration Manager.


    **Aplicação cliente nativa:**  Procurar abre a janela de aplicação de cliente.  
     No **aplicação cliente** janela, selecione a aplicação de cliente que pretende utilizar e, em seguida, clique em **OK**.

     Se não tiver uma aplicação de cliente disponíveis, utilize um dos seguintes:
     - **Criar**: Para criar uma nova aplicação de cliente, clique em **criar**. Em seguida, forneça um nome amigável para a aplicação e o URI de redirecionamento.

         Para continuar, alguém tem agora iniciar sessão com as respetivas credenciais do Azure AD para concluir a criação da aplicação web no Azure. A conta que utiliza para início de sessão para o Azure não precisa de ser a mesma conta que executa o Assistente de serviços do Azure. Após o início de sessão para o Azure, o Configuration Manager cria a aplicação cliente nativa no Azure AD para si, incluindo o ID de cliente e a chave secreta. Mais tarde, pode ver estes do [portal do Azure](https://portal.azure.com). 

     - **Importar**: Utilize uma aplicação de cliente que já exista na sua subscrição do Azure. Forneça um nome amigável para a aplicação e o ID de cliente. Em seguida, clique em **OK** para continuar.

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  (Apenas quando configurar o **nuvem gestão** serviço) no **deteção** página do assistente, clique em **ativar o Azure Active Directory deteção de utilizadores**e, em seguida, clique em  **Definições**.
No **definições de deteção de utilizador do Azure AD** diálogo caixa, configure uma agenda para quando ocorre a deteção. Também pode ativar a deteção de diferenças que verifica a existência de apenas novos ou alterados contas no Azure AD. Saiba mais sobre [do Azure AD User Discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

7.  Conclua o assistente.

Neste momento, concluiu a configuração de um serviço do Azure no Configuration Manager. Pode repetir este processo para configurar outros serviços do Azure.

## <a name="view-the-configuration-of-an-azure-service"></a>Ver a configuração de um serviço do Azure
Pode ver as propriedades de um serviço do Azure que configurou para utilização.

Na consola, aceda a **administração** > **descrição geral** > **serviços em nuvem** > **serviços do Azure**. Em seguida, escolha o serviço que pretende ver ou editar e, em seguida, clique em **propriedades**.

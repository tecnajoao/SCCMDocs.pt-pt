---
title: "Assistente de serviços do Azure | Microsoft Docs"
description: "Sobre o Assistente de serviços do Azure para o System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: MT
ms.sourcegitcommit: 0663ba84762c44a5c303562548499f195bae9e1c
ms.openlocfilehash: 22203b358830903cf2e531c0532ae3111b8265fc
ms.contentlocale: pt-pt
ms.lasthandoff: 08/01/2017

---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configurar os serviços do Azure para utilização com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir da versão do ramo atual 1706, o **Assistente de serviços do Azure** é utilizado para simplificar o processo de configuração de serviços do Azure a utilizar com o Configuration Manager.

Este assistente fornece uma experiência de configuração comum utilizando um **aplicação web do Azure** faculte os detalhes da subscrição e a configuração. A aplicação web substitui introduzir esta mesma informação sempre que configurou um novo componente do Configuration Manager ou o serviço com o Azure.

Os seguintes serviços do Azure são configurados utilizando o Assistente para configurar os serviços do Azure:
-   **Gestão de nuvem**   
    [Permitir que os clientes autenticar com o Azure Active Directory]() (Azure AD). Também pode [configurar a deteção de utilizador do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).
-   **Conector do OMS**
    [ligar ao Operations Manager Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS) e sincronizar os dados, como coleções para análise de registos do OMS.
-   **Preparação para a atualização**
    [ligar a preparação de atualização](/sccm/core/clients/manage/upgrade/upgrade-analytics) e ver os dados de compatibilidade de atualização de cliente.
-   **Loja Windows para empresas** ligar para a loja online para [loja Windows para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) e obter aplicações da sua organização que pode implementar com o Configuration Manager.

Ao utilizar o Assistente para configurar um serviço, várias ações comuns estão disponíveis.
Estas atualizações incluem:
-   Configure o ambiente do Azure:  No **aplicação** página do assistente, selecione o **ambiente do Azure** que utilizar. Consulte o conteúdo para cada serviço saber se suporta apenas na nuvem pública do Azure, ou se pode suportar uma nuvem privada.
-   Criar ou importar uma aplicação de servidor:   No **aplicação** página do assistente, pode **criar** e **importação** aplicações web do Azure. As opções disponíveis dependem do serviço que estiver a configurar.  Além disso, alguns serviços poderão necessitar de uma aplicação adicional. Por exemplo, um serviço pode igualmente necessitar de um **aplicação cliente nativa**.


Para obter informações sobre aplicações web do Azure, consulte [autenticação e autorização no serviço de aplicações do Azure](/azure/app-service/app-service-authentication-overview), e [descrição geral das aplicações Web](/azure/app-service-web/app-service-web-overview)


## <a name="webapp"></a>Criar a aplicação web do Azure para utilização com o Configuration Manager

A aplicação web de serviços do Azure liga o site do Configuration Manager para o Azure AD e é um pré-requisito para utilizar os serviços do Azure com a sua infraestrutura. Para efetuar este procedimento:

1.  No **administração** área de trabalho da consola do Configuration Manager, expanda **serviços em nuvem**e, em seguida, clique em **serviços do Azure**.
2.  No **home page** separador o **serviços do Azure** , clique em **configurar os serviços do Azure**.
3.  No **serviços do Azure** página do Assistente de serviços do Azure, selecione **gestão de nuvem** para permitir que os clientes autenticar com a hierarquia de utilizar o Azure AD.
4.  No **geral** página do assistente, especifique um nome e uma descrição para o serviço do Azure.
5.  No **aplicação** página do assistente, selecione o seu ambiente do Azure da lista e clique em **procurar** para selecionar o *aplicação Web* e *aplicação cliente nativa* que será utilizado para configurar o serviço do Azure.     
    **Aplicação Web:**   Procurar abre a janela de aplicação de servidor.    
      No **aplicação Server** janela, selecione a aplicação de servidor que pretende utilizar e, em seguida, clique em **OK**. Aplicações de servidor são as aplicações web do Azure que contêm as configurações para a sua conta do Azure, incluindo o ID de inquilino, ID de cliente e uma chave secreta para clientes.
    Se não tiver uma aplicação disponível, utilize um dos seguintes:
        - **Criar**: Para criar uma nova aplicação de servidor, clique em **criar**. Em seguida, forneça um nome amigável para a aplicação, o URL de home page, URI de ID de aplicação e o período de validade da chave secreta. Por predefinição, o período de validade da chave secreta é um ano.

         Para continuar, alguém tem agora iniciar sessão no Azure para concluir a criação da aplicação web no Azure. A conta que utiliza para início de sessão para o Azure não precisa de ser a mesma conta que executa o Assistente de serviços do Azure. Após o início de sessão para o Azure, o Configuration Manager cria a aplicação web no Azure para si, incluindo o ID de cliente e a chave secreta para utilização com a aplicação web. Mais tarde, pode ver estes do portal do Azure.

         Quando a utiliza para configurar uma aplicação web, Configuration Manager pode criar a aplicação web para si no Azure AD.
        - **Importar**: Para utilizar uma aplicação web que já existe na sua subscrição do Azure, clique em **importação**. Forneça um nome amigável para a aplicação e de inquilino e, em seguida, especifique o ID do inquilino, ID de cliente e a chave secreta para a aplicação web do Azure que pretende utilizar o Configuration Manager. Depois de verificar as informações, clique em **OK** para continuar.

          Esta opção não está disponível para todos os serviços que poderá configurar.

   **Aplicação cliente nativa:**  Procurar abre a janela de aplicação de cliente.  
     No **aplicação cliente** janela, selecione a aplicação de cliente que pretende utilizar e, em seguida, clique em **OK**.

     Se não tiver uma aplicação de cliente disponíveis, utilize um dos seguintes:
     - **Criar**: Para criar uma nova aplicação de cliente, clique em **criar**. Em seguida, forneça um nome amigável para a aplicação e o URL de resposta.

          Para continuar, alguém tem agora iniciar sessão no Azure para concluir a criação da aplicação cliente no Azure. A conta que utiliza para início de sessão para o Azure não precisa de ser a mesma conta que executa o Assistente de serviços do Azure. Após o início de sessão para o Azure, o Configuration Manager cria a aplicação cliente nativa no Azure para si, incluindo o ID de cliente para utilização com a aplicação web. Mais tarde, pode ver estes do portal do Azure.
          Quando a utiliza para configurar a aplicação, Configuration Manager pode cria a aplicação cliente nativa para si no Azure AD.
     - **Importar**: Para utilizar uma aplicação de cliente que já exista na sua subscrição do Azure, clique em **importação**. Forneça um nome amigável para a aplicação e o ID de cliente. Em seguida, clique em **OK** para continuar.
           Esta opção não está disponível para todos os serviços que poderá configurar.

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  No **deteção** página do assistente, clique em **ativar o Azure Active Directory deteção de utilizadores**e, em seguida, clique em **definições**.
No **definições de deteção de utilizador do Azure AD** diálogo caixa, configure uma agenda para quando ocorre a deteção. Também pode ativar a deteção de diferenças que verifica a existência de apenas novos ou alterados contas no Azure AD. Saiba mais sobre [do Azure AD User Discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).
 
 7. Conclua o assistente.

Neste momento, ligou-se o site do Configuration Manager para o Azure AD.

## <a name="view-the-configuration-of-an-azure-service"></a>Ver a configuração de um serviço do Azure
Pode ver as propriedades de um serviço do Azure que configurou para utilização.

Na consola, aceda a **administração** > **descrição geral** > **serviços em nuvem** > **serviços do Azure**. Em seguida, escolha o serviço que pretende ver ou editar e, em seguida, clique em **propriedades**.


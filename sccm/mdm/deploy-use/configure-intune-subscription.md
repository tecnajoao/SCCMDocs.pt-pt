---
title: Configurar sua assinatura do Intune usando o System Center Configuration Manager | Microsoft Docs
description: Configure sua assinatura do Intune usando o System Center Configuration Manager.
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99de8fe7-560e-401a-8ab2-6d87d091be17
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 662901e850566756759fcfc61c58f3c0e56bc5aa
ms.openlocfilehash: 22d890c972d3166f9c7b583d8d3fa917c1897880
ms.contentlocale: pt-pt
ms.lasthandoff: 06/03/2017

---
# <a name="configure-your-intune-subscription-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar sua assinatura do Intune com System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

A assinatura do Intune permite que você gerencie dispositivos pela internet. Isso inclui especificar qual coleção de usuários pode registrar dispositivos e definir as informações apresentadas aos usuários. Ao criar a assinatura do Intune, você também pode adicionar esquemas de identidade visual ao portal da empresa do Intune com o logotipo da empresa e cores personalizadas.

A subscrição do Intune faz o seguinte:

-   Obtém o certificado de que o ponto de ligação de serviço necessita para efetuar a ligação ao serviço Intune
-   Define a coleção de utilizadores que permite aos utilizadores inscreverem dispositivos móveis
-   Define e configura as plataformas móveis que pretende suportar

> [!IMPORTANT]
>  Criando uma assinatura do Microsoft Intune no Configuration Manager colocará o ponto de conexão de serviço do seu site no "modo online". Veja [Acerca do ponto de ligação de serviço no System Center Configuration Manager](../../core/servers/deploy/configure/about-the-service-connection-point.md).

## <a name="to-create-the-microsoft-intune-subscription"></a>Para criar a subscrição do Microsoft Intune

1.  Se ainda não o fez, inscreva-se numa conta do Microsoft Intune em [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216).  Depois de criar sua conta do Intune, você não precisa adicionar todos os usuários para a conta do Intune ou executar configurações adicionais.

2.  Na consola do Configuration Manager, clique em **Administração**.

3.  Na área de trabalho **Administração**, expanda **Serviços Cloud** e clique em **Subscrições do Microsoft Intune**. No separador **Home Page**, clique em **Adicionar Subscrição do Microsoft Intune**.

![Criar uma assinatura do Intune](../media/mdm-set-intune.png)

4.  Na página **Introdução** do Assistente Criar Subscrição do Microsoft Intune, reveja o texto e clique em **Seguinte**.

5.  Na página **Subscrição**, clique em **Iniciar sessão** e inicie sessão utilizando a sua conta escolar ou profissional. No **definir a autoridade de gerenciamento de dispositivos móveis** caixa de diálogo, selecione a caixa de seleção para somente gerencia dispositivos móveis usando o Configuration Manager por meio do console do Configuration Manager. Para continuar a subscrição, terá de selecionar esta opção.

    > [!IMPORTANT]
    >  Quando você seleciona o Configuration Manager como sua autoridade de gerenciamento, você pode alterar apenas sua autoridade de gerenciamento para Microsoft Intune no Configuration Manager versão 1610 ou posterior e o Microsoft Intune version 1705 sem precisar entrar em contato com o Microsoft Support e sem a necessidade de cancelar o registro e registrar novamente os dispositivos gerenciados existentes. Para obter detalhes, consulte [alterar sua autoridade MDM](/sccm/mdm/deploy-use/change-mdm-authority).

6.  Clique nas hiperligações de privacidade para revê-las e clique em **Seguinte**.

7.  Na página **Geral**, especifique as seguintes opções e clique em **Seguinte**.

  -   **Coleção**: Especifique uma coleção de usuários que contém usuários que registrarão seus dispositivos móveis.

      > [!NOTE]
      >  Se um usuário for removido da coleção, o dispositivo do usuário continuará a ser gerenciado por até 24 horas, quando o registro do usuário é removido do banco de dados do usuário.

  -   **Nome da empresa**: Especifique o nome da sua empresa.

  -   **URL da documentação de privacidade**: Se você publicar suas informações de privacidade da empresa em um link acessível pela Internet, forneça um link que os usuários possam acessar pelo portal da empresa, por exemplo, http://www.contoso.com/CP_privacy.html. As informações de privacidade permitem clarificar as informações que os utilizadores partilham com a empresa.

  -   **Esquema de cores do portal da empresa**: Opcionalmente, altere a cor padrão da azul portais da empresa.

  -   **Código de site do Configuration Manager**: Especifique um código de site para um site primário para gerenciar os dispositivos móveis.

    > [!NOTE]
    >  A alteração do código do site afeta apenas as novas inscrições, não afetando os dispositivos já inscritos.

8.  No **as informações de contato da empresa** página, especifique as informações de contato da empresa são exibidas aos usuários em **contate a TI** no aplicativo do Portal da empresa. Fornecer informações de contato da sua empresa e, em seguida, clique em **próximo**.

9. Sobre o **logotipo da empresa** página, você pode optar por exibir logotipos no portal da empresa e, em seguida, clique em **próximo**.

10. Conclua o assistente.

> [!div class="button"]
[< Anterior etapa](confirm-dns.md)[próxima etapa >  ](terms-and-conditions.md)


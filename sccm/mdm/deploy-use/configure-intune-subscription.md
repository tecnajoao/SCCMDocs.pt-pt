---
title: "Configurar a sua subscrição do Intune com o System Center Configuration Manager | Documentos do Microsoft"
description: "Configure a sua subscrição do Intune com o System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
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
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 10cc64ae7e4d91f53201c2896b359e77ef04d32d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="configure-your-intune-subscription-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a sua subscrição do Intune com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A subscrição do Intune permite-lhe gerir dispositivos através da internet. Isto inclui a especificação que coleção de utilizadores pode inscrever dispositivos e definir as informações apresentadas aos utilizadores. Ao criar a subscrição do Intune, também pode adicionar uma imagem corporativa ao portal da empresa do Intune com o seu logótipo da empresa e cor personalizada esquemas de empresa.

A subscrição do Intune faz o seguinte:

-   Obtém o certificado de que o ponto de ligação de serviço necessita para efetuar a ligação ao serviço Intune
-   Define a coleção de utilizadores que permite aos utilizadores inscreverem dispositivos móveis
-   Define e configura as plataformas móveis que pretende suportar

> [!IMPORTANT]
>  Criar uma subscrição do Microsoft Intune no Configuration Manager irá colocar o ponto de ligação de serviço do seu site no "modo online". Veja [Acerca do ponto de ligação de serviço no System Center Configuration Manager](../../core/servers/deploy/configure/about-the-service-connection-point.md).

## <a name="to-create-the-microsoft-intune-subscription"></a>Para criar a subscrição do Microsoft Intune

1.  Se ainda não o fez, inscreva-se numa conta do Microsoft Intune em [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216).  Depois de criar a sua conta do Intune, não terá de adicionar utilizadores à conta do Intune ou efetuar configurações definições adicionais.

2.  Na consola do Configuration Manager, clique em **Administração**.

3.  Na área de trabalho **Administração**, expanda **Serviços Cloud** e clique em **Subscrições do Microsoft Intune**. No separador **Home Page**, clique em **Adicionar Subscrição do Microsoft Intune**.

![Criar uma subscrição do Intune](../media/mdm-set-intune.png)

4.  Na página **Introdução** do Assistente Criar Subscrição do Microsoft Intune, reveja o texto e clique em **Seguinte**.

5.  Na página **Subscrição**, clique em **Iniciar sessão** e inicie sessão utilizando a sua conta escolar ou profissional. No **definir a autoridade de gestão de dispositivos móveis** caixa de diálogo, selecione a caixa de verificação apenas gere dispositivos móveis utilizando o Configuration Manager através da consola do Configuration Manager. Para continuar a subscrição, terá de selecionar esta opção.

    > [!IMPORTANT]
    >  Depois de selecionar o Configuration Manager como autoridade de gestão, é possível alterar a autoridade de gestão para o Microsoft Intune no futuro.

6.  Clique nas hiperligações de privacidade para revê-las e clique em **Seguinte**.

7.  Na página **Geral**, especifique as seguintes opções e clique em **Seguinte**.

  -   **Recolha**: Especifique uma coleção de utilizadores que contenha os utilizadores que irão inscrever os respetivos dispositivos móveis.

      > [!NOTE]
      >  Se um utilizador for removido da coleção, o dispositivo do utilizador continuará a ser gerido durante até 24 horas, quando o registo de utilizador é removido da base de dados do utilizador.

  -   **Nome da empresa**: Especifique o nome da sua empresa.

  -   **URL para a documentação de privacidade**: Se publicar as informações de privacidade da empresa numa ligação acessível a partir da Internet, forneça uma ligação que os utilizadores podem aceder a partir do portal da empresa, por exemplo http://www.contoso.com/CP_privacy.html. As informações de privacidade permitem clarificar as informações que os utilizadores partilham com a empresa.

  -   **Esquema de cores para o portal da empresa**: Opcionalmente, altere a cor predefinida dos azul portais de empresa.

  -   **Código de site do Configuration Manager**: Especifique um código de site para um site primário gerir os dispositivos móveis.

    > [!NOTE]
    >  A alteração do código do site afeta apenas as novas inscrições, não afetando os dispositivos já inscritos.

8.  No **informações de contacto da empresa** página, especifique as informações de contacto da empresa que são apresentadas aos utilizadores em **contactar TI** na aplicação do Portal da empresa. Fornecer informações de contacto da sua empresa e, em seguida, clique em **seguinte**.

9. No **o logótipo da empresa** página, pode optar por apresentar logótipos no portal da empresa e, em seguida, clique em **seguinte**.

10. Conclua o assistente.

> [!div class="button"]
[< Passo anterior](confirm-dns.md)[junto passo >  ](terms-and-conditions.md)


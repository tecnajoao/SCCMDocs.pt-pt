---
title: "Criar um ponto de ligação de serviço através do Configuration Manager do System Center | Documentos do Microsoft"
description: "Crie um ponto de ligação de serviço com o System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 617abb22-d22f-41fb-a76b-1c4259e419d2
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 9a21d02cb2a50162e5de50481f0f27f2dd7a616c
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="create-a-service-connection-point-with-system-center-configuration-manager-and-microsoft-intune"></a>Criar um ponto de ligação de serviço com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando tiver criado a sua subscrição, poderá instalar a função do sistema de sites do ponto de ligação de serviço que permite estabelecer ligação ao serviço Intune. Esta função do sistema de sites emitirá as definições e aplicações para o serviço Intune.

 O ponto de ligação de serviço envia definições e informações de implementação de software do Configuration Manager e obtém mensagens de estado e de inventário de dispositivos móveis. O serviço do Configuration Manager é funciona como um gateway que comunica com dispositivos móveis e armazena as definições.

> [!NOTE]
>  A função do sistema de sites do ponto de ligação de serviço só pode ser instalada num site de administração central ou num site primário autónomo. O ponto de ligação de serviço deve ter acesso à Internet.


## <a name="configure-the-service-connection-point-role"></a>Configurar a função de ponto de ligação de serviço

1.  Na consola do Configuration Manager, clique em **Administração**.

2.  No **administração** área de trabalho, expanda **Sites**e, em seguida, clique em **servidores e funções de sistema de sites**.

3.  Adicione a função **Ponto de ligação de serviço** a um servidor do sistema de sites novo ou existente através do passo associado:

    -   Novo servidor de sistema de sites: No **base** separador o **criar** grupo, clique em **criar servidor do sistema de sites** para iniciar o assistente servidor criar de sistema de sites.

    -   Servidor de sistema de sites existente: Clique no servidor no qual pretende instalar a função de ponto de ligação de serviço. Em seguida, no separador **Home Page**, no grupo **Servidor**, clique em **Adicionar Funções do Sistema de Sites** para iniciar o Assistente para Adicionar Funções ao Sistema de Sites.

4.  Na página **Seleção da Função do Sistema**, selecione **Ponto de ligação de serviço** e clique em **Seguinte**.
![Criar um ponto de ligação de serviço](../media/mdm-service-connection-point.png)

* Conclua o assistente.

## <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>Como é que o ponto de ligação de serviço é autenticado com o serviço Microsoft Intune?
 O ponto de ligação de serviço expande o Configuration Manager ao estabelecer uma ligação para o serviço Intune baseado na nuvem, que gere dispositivos móveis através da Internet. O ponto de ligação de serviço autentica com o serviço Intune da seguinte forma:

1.  Quando cria uma subscrição do Intune na consola do Configuration Manager, o administrador do Configuration Manager efetuar a autenticação ao estabelecer ligação ao Azure Active Directory, que redireciona para o respetivo servidor do ADFS para lhe pedir para nome de utilizador e palavra-passe. Em seguida, o Intune emite um certificado do inquilino.

2.  O certificado do passo 1 é instalado na função do site do ponto de ligação de serviço e é utilizado para autenticar e autorizar toda a comunicação futura com o serviço Microsoft Intune.

> [!div class="button"]
[< Passo anterior](terms-and-conditions.md)[junto passo >  ](enable-platform-enrollment.md)


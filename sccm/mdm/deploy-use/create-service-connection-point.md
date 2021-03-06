---
title: Criar um ponto de ligação de serviço
titleSuffix: Configuration Manager
description: Crie um ponto de ligação de serviço com o System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 617abb22-d22f-41fb-a76b-1c4259e419d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d0ce47e9ade73d76e99aa5c0d4e5581c713a847a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139032"
---
# <a name="create-a-service-connection-point-with-system-center-configuration-manager-and-microsoft-intune"></a>Criar um ponto de ligação de serviço com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando tiver criado a sua subscrição, poderá instalar a função do sistema de sites do ponto de ligação de serviço que permite estabelecer ligação ao serviço Intune. Esta função do sistema de sites emitirá as definições e aplicações para o serviço Intune.

 O ponto de ligação de serviço envia definições e informações de implementação de software para o Configuration Manager e obtém mensagens de estado e de inventário de dispositivos móveis. O serviço do Configuration Manager age como um gateway que comunica com dispositivos móveis e armazena as definições.

> [!NOTE]
>  A função do sistema de sites do ponto de ligação de serviço só pode ser instalada num site de administração central ou num site primário autónomo. O ponto de ligação de serviço deve ter acesso à Internet.


## <a name="configure-the-service-connection-point-role"></a>Configurar a função de ponto de ligação de serviço

1.  Na consola do Configuration Manager, clique em **Administração**.

2.  Na **administração** área de trabalho, expanda **configuração do Site**, em seguida, clique em **servidores e funções de sistema de sites**.

3.  Adicione a função **Ponto de ligação de serviço** a um servidor do sistema de sites novo ou existente através do passo associado:

    -   Novo servidor do sistema de sites: Sobre o **home page** separador a **criar** , clique em **criar servidor do sistema de sites** para iniciar o assistente servidor criar de sistema de sites.

    -   Servidor de sistema de sites existente: Clique no servidor no qual pretende instalar a função de ponto de ligação de serviço. Em seguida, no separador **Home Page**, no grupo **Servidor**, clique em **Adicionar Funções do Sistema de Sites** para iniciar o Assistente para Adicionar Funções ao Sistema de Sites.

4.  Na página **Seleção da Função do Sistema**, selecione **Ponto de ligação de serviço** e clique em **Seguinte**.
![Criar um ponto de ligação de serviço](../media/mdm-service-connection-point.png)

* Conclua o assistente.

## <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>Como é que o ponto de ligação de serviço é autenticado com o serviço Microsoft Intune?
 O ponto de ligação de serviço expande o Configuration Manager ao estabelecer uma ligação para o serviço do Intune com base na cloud que gere dispositivos móveis através da Internet. O ponto de ligação de serviço é autenticado com o serviço do Intune da seguinte forma:

1.  Quando cria uma subscrição do Intune na consola do Configuration Manager, o administrador do Configuration Manager é autenticado ao ligar ao Azure Active Directory, que redireciona para o respetivo servidor ADFS para pedir o nome de utilizador e palavra-passe. Em seguida, o Intune emite um certificado para o inquilino.

2.  O certificado do passo 1 é instalado na função do site do ponto de ligação de serviço e é utilizado para autenticar e autorizar toda a comunicação futura com o serviço Microsoft Intune.

> [!div class="button"]
> [< Anterior passo](terms-and-conditions.md)[passo seguinte >](enable-platform-enrollment.md)

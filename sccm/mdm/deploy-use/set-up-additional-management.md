---
title: "Configurar a gestão adicional com o System Center Configuration Manager | Documentos do Microsoft"
description: "Configure a gestão adicional com o System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4877d674-6bbc-4e16-810c-daad70c74daa
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 947d2a85f2ac68c7ccaf9a1237fd60e89e7d1d10
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="set-up-additional-management-with-system-center-configuration-manager"></a>Configurar a gestão adicional com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

(Opcional) Pode configurar a gestão adicional antes dos dispositivos são inscritos. Estas soluções de gestão podem ser criadas e implementadas após a inscrição dos dispositivos, apesar de muitas organizações preferem implementá-los como os dispositivos são importados para gestão.

**Itens de configuração** permitem-lhe gerir as definições, tais como a necessidade de um PIN ou exigir encriptação em dispositivos inscritos com base na plataforma de dispositivo:
- [Dispositivos Windows 10 e Windows 8.1](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Dispositivos Windows Phone](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
- [iOS e dispositivos de Mac](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
- [Android e dispositivos Samsung KNOX Standard](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)

**Aplicações** podem ser implementadas nos dispositivos geridos:
- [aplicações iOS](creating-ios-applications.md)
- [Aplicações Mac](../../apps/get-started/creating-mac-computer-applications.md)
- [Aplicações do Windows PC](../../apps/get-started/creating-windows-applications.md)
- [Aplicações do Windows Phone](creating-windows-phone-applications.md)
- [Aplicações Android](creating-android-applications.md)

**Acesso condicional** permite-lhe gerir o acesso aos recursos da empresa, incluindo:  
- [Acesso ao e-mail](manage-email-access.md)
- [Acesso do SharePoint](manage-sharepoint-online-access.md)
- [Skype para acesso de negócio](manage-skype-for-business-online-access.md)
- [Dinâmica CRM Online](manage-dynamics-crm-online-access.md)

**Multi-factor Authentication (MFA)** permite-lhe necessitam de mais do que um método de verificação, que adiciona uma segunda camada crítica de segurança aos inícios de sessão de utilizador e de transações.
Anteriormente, poderá aceder a consola do Intune ou a consola do Configuration Manager para configurar a MFA para inscrições através do Intune. Agora, pode iniciar sessão a [portal do Microsoft Azure](https://manage.windowsazure.com) com as suas credenciais do Intune e configurar definições de MFA através do Azure AD. Para obter mais informações, consulte o artigo [multi-factor authentication do Microsoft Intune](https://aka.ms/mfa_ad).

> [!div class="button"]
[< Passo anterior](enable-platform-enrollment.md)[junto passo >  ](verify-mdm-configuration.md)

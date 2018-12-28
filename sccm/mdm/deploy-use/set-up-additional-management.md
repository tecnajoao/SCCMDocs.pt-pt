---
title: Configurar a gestão adicional
titleSuffix: Configuration Manager
description: Configure gestão adicional através do System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4877d674-6bbc-4e16-810c-daad70c74daa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8c2ded7509c8097ae219aa594e56fda3f0c35ccd
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417154"
---
# <a name="set-up-additional-management-with-system-center-configuration-manager"></a>Configurar a gestão adicional com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

(Opcional) Pode configurar a gestão adicional antes dos dispositivos são inscritos. Estas soluções de gestão podem ser criadas e implementadas depois de a inscrição dos dispositivos, embora muitas organizações preferem para implantá-los como dispositivos são colocados em gestão.

**Itens de configuração** permitem-lhe gerir as definições, como exigir um PIN ou a encriptação em dispositivos inscritos com base na plataforma de dispositivo:
- [Dispositivos Windows 10 e Windows 8.1](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Dispositivos Windows Phone](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
- [dispositivos iOS e Mac](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
- [Android e Samsung KNOX Standard](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)

**Aplicativos** podem ser implementados em dispositivos geridos:
- [aplicações iOS](creating-ios-applications.md)
- [Aplicações Mac](../../apps/get-started/creating-mac-computer-applications.md)
- [Aplicativos de PC do Windows](../../apps/get-started/creating-windows-applications.md)
- [Aplicativos do Windows Phone](creating-windows-phone-applications.md)
- [Aplicações Android](creating-android-applications.md)

**Acesso condicional** permite-lhe gerir o acesso aos recursos da empresa, incluindo:  
- [Acesso ao e-mail](manage-email-access.md)
- [Acesso do SharePoint](manage-sharepoint-online-access.md)
- [Skype para acesso de negócios](manage-skype-for-business-online-access.md)
- [Dynamic CRM Online](manage-dynamics-crm-online-access.md)

**Multi-factor Authentication (MFA)** permite que exija mais do que um método de verificação, que adiciona uma segunda camada crítica de segurança aos inícios de sessão de utilizador e de transações.
Anteriormente, utilizariam a consola do Intune ou a consola do Configuration Manager para configurar a MFA para inscrições no Intune. Agora, faça logon para o [portal do Microsoft Azure](https://manage.windowsazure.com) com as suas credenciais do Intune e configurar as definições da MFA através do Azure AD. Para obter mais informações, consulte [multi-factor authentication do Microsoft Intune](https://aka.ms/mfa_ad).

> [!div class="button"]
> [< Anterior passo](enable-platform-enrollment.md)[passo seguinte >  ](verify-mdm-configuration.md)

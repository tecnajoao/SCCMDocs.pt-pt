---
title: Configurar a gestão adicional
titleSuffix: Configuration Manager
description: Configure a gestão adicional através do System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4877d674-6bbc-4e16-810c-daad70c74daa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58a61dffbdd9b04d3e872e23f88ddc0ac864f99d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346350"
---
# <a name="set-up-additional-management-with-system-center-configuration-manager"></a>Configurar a gestão adicional com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

(Opcional) Pode configurar gestão adicional antes dos dispositivos são inscritos. Estas soluções de gestão podem ser criadas e implementadas depois dos dispositivos são inscritos, apesar de muitas organizações preferem implementá-los como dispositivos são colocados em gestão.

**Itens de configuração** permitem-lhe gerir as definições, tais como exigir um PIN ou exigir encriptação em dispositivos inscritos com base na plataforma de dispositivos:
- [Dispositivos Windows 10 e Windows 8.1](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Dispositivos Windows Phone](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
- [dispositivos iOS e Mac](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
- [Android e dispositivos Samsung KNOX Standard](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)

**Aplicações** podem ser implementadas em dispositivos geridos:
- [aplicações iOS](creating-ios-applications.md)
- [Aplicações Mac](../../apps/get-started/creating-mac-computer-applications.md)
- [Aplicações de Windows PC](../../apps/get-started/creating-windows-applications.md)
- [Aplicações do Windows Phone](creating-windows-phone-applications.md)
- [Aplicações Android](creating-android-applications.md)

**Acesso condicional** permite-lhe gerir o acesso aos recursos da empresa, incluindo:  
- [Acesso ao e-mail](manage-email-access.md)
- [Acesso do SharePoint](manage-sharepoint-online-access.md)
- [Skype para acesso de negócio](manage-skype-for-business-online-access.md)
- [Dinâmica CRM Online](manage-dynamics-crm-online-access.md)

**Autenticação multifator (MFA)** permite-lhe necessitam de mais do que um método de verificação, que adiciona uma segunda camada crítica de segurança aos inícios de sessão de utilizador e de transações.
Anteriormente, passará a consola do Intune ou a consola do Configuration Manager para configurar a MFA para inscrições através do Intune. Agora, pode iniciar sessão a [portal do Microsoft Azure](https://manage.windowsazure.com) com as suas credenciais do Intune e configurar as definições da MFA através do Azure AD. Para obter mais informações, consulte [multi-factor authentication do Microsoft Intune](https://aka.ms/mfa_ad).

> [!div class="button"]
[< Anterior passo](enable-platform-enrollment.md)[passo seguinte >](verify-mdm-configuration.md)

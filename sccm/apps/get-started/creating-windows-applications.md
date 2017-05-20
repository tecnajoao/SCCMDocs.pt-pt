---
title: "Criar aplicações do Windows | Documentos do Microsoft"
description: "Consulte as considerações tem de efetuar para conta quando criar e implementar aplicações para dispositivos Windows."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 557888d1f1f899e3198c430bbe5ccdd44178f824
ms.openlocfilehash: 9c80cc42f9ce6775067a89a9f5a63c1bf4a0c7ca
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="create-windows-applications-with-system-center-configuration-manager"></a>Criar aplicações do Windows com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para além de outros requisitos do System Center Configuration Manager e procedimentos para criar uma aplicação, tem também de efetuar as seguintes considerações de consideração quando criar e implementar aplicações para dispositivos Windows.  

## <a name="general-considerations"></a>Considerações gerais  
 O Configuration Manager suporta os seguintes tipos de ficheiro de aplicação a implementar:  

|Tipo de Dispositivo|Tipos de ficheiro suportados|  
|-----------------|---------------------|  
|Windows RT e Windows RT 8.1|*. AppX, \*. appxbundle|  
|Windows 8.1 e posterior inscrito como um dispositivo móvel|*. AppX, \*. appxbundle|  

 As seguintes ações de implementação são suportadas:  

|Tipo de Dispositivo|Ações suportadas|  
|-----------------|-----------------------|  
|Windows 8.1 e posterior|disponível, necessário, desinstalar|  
|Windows RT|disponível, necessário, desinstalar|  

## <a name="support-for-universal-windows-platform-uwp-apps"></a>Suporte para aplicações da Plataforma Universal do Windows (UWP)  
 Dispositivos Windows 10 não necessitam de uma chave de sideload para instalar aplicações de linha de negócio. Para efetuar sideload de estar ativadas, no entanto, a chave de registo **HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps** tem de ter um valor de 1.  

 Se esta chave de registo não estiver configurada, o Configuration Manager configura automaticamente este valor **1** pela primeira vez implementa uma aplicação para o dispositivo. Se tem de definir este valor como **0**, Configuration Manager não conseguirá alterar automaticamente o valor e a implementação de aplicações de linha de negócio falhar.  

 Aplicações de linha de negócio de plataforma Windows universais têm de ser assinadas com um certificado de assinatura de código é considerada fidedigna em cada dispositivo em que a aplicação é implementada. Pode utilizar certificados a partir de uma infraestrutura PKI interna ou um certificado a partir de um certificado de raiz público de terceiros instalado no dispositivo.  

 Em dispositivos Windows 10 Mobile, pode utilizar um certificado de assinatura de código não Symantec para assinar aplicações **.appx** universais. Para aplicações **.xap** e pacotes **.appx** incorporados para o Windows Phone 8.1 que pretende instalar em dispositivos Windows 10 Mobile, tem de utilizar um certificado de assinatura de código da Symantec.  

## <a name="deploy-windows-installer-apps-to-enrolled-windows-10-pcs"></a>Implementar aplicações do Windows Installer em PCs Windows 10 inscritos  
 O **do Windows Installer através de MDM (\*. msi)** tipo de instalador permite-lhe criar e implementar aplicações baseadas no Windows Installer para PCs inscritos que executam o Windows 10.  

 As considerações seguintes são aplicáveis quando utiliza este tipo de instalador:  

-   Só pode carregar um único ficheiro com a extensão .msi.  

-   O código de produto do ficheiro e a versão do produto são utilizados para deteção da aplicação.  

-   O comportamento de reinício predefinido da aplicação é utilizado. O Configuration Manager não controla esta.  

-   Por utilizador MSI são instalados pacotes para um único utilizador.  

-   Por máquina MSI é instalado para todos os utilizadores no dispositivo.  

-   As atualizações de aplicações são suportadas quando o código de produto MSI de cada versão for igual.  

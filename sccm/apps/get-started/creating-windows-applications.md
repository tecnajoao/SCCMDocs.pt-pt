---
title: Criar aplicações do Windows
titleSuffix: Configuration Manager
description: Consulte as considerações deve ter em conta quando criar e implementar aplicações em dispositivos Windows.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3ac0526d31bb46cce18e096ff1d120eda452c806
ms.sourcegitcommit: 1701943932818e0df1928d9be36ebaf424dd93b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/10/2018
---
# <a name="create-windows-applications-with-system-center-configuration-manager"></a>Criar aplicações do Windows com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para além de outros requisitos do System Center Configuration Manager e procedimentos para criar uma aplicação, terá também de ter em conta as seguintes considerações ao criar e implementar aplicações em dispositivos Windows.  

## <a name="general-considerations"></a>Considerações gerais  
 O Configuration Manager suporta a implementação dos seguintes tipos de ficheiro de aplicação:  

|Tipo de Dispositivo|Tipos de ficheiro suportados|  
|-----------------|---------------------|  
|Windows RT e Windows RT 8.1|\*. AppX, \*. appxbundle|  
|Windows 8.1 e posterior|\*. AppX, \*. appxbundle|  



 As seguintes ações de implementação são suportadas:  

|Tipo de Dispositivo|Ações suportadas|  
|-----------------|-----------------------|  
|Windows 8.1 e posterior|disponível, necessário, desinstalar|  
|Windows RT|disponível, necessário, desinstalar|  

## <a name="support-for-universal-windows-platform-uwp-apps"></a>Suporte para aplicações da Plataforma Universal do Windows (UWP)  
 Dispositivos Windows 10 não requerem uma chave de sideload para instalar aplicações de linha de negócio. Para efetuar sideload ser ativada, no entanto, a chave de registo **HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps** tem de ter um valor de 1.  

 Se esta chave de registo não estiver configurada, o Configuration Manager configura automaticamente este valor **1** pela primeira vez implementa uma aplicação no dispositivo. Se tiver definido este valor como **0**, Configuration Manager não pode alterar automaticamente o valor e a implementação de aplicações de linha de negócio falhará.  

 Aplicações de linha de negócio da plataforma Windows universal tem de ser assinadas com um certificado de assinatura de código considerado fidedigno em cada dispositivo em que a aplicação é implementada. Pode utilizar certificados a partir de uma infraestrutura PKI interna ou um certificado a partir de um certificado de raiz público de terceiros instalado no dispositivo.  

 Em dispositivos Windows 10 Mobile, pode utilizar um certificado de assinatura de código não Symantec para assinar aplicações **.appx** universais. Para aplicações **.xap** e pacotes **.appx** incorporados para o Windows Phone 8.1 que pretende instalar em dispositivos Windows 10 Mobile, tem de utilizar um certificado de assinatura de código da Symantec.  

## <a name="deploy-windows-installer-apps-to-enrolled-windows-10-pcs"></a>Implementar aplicações do Windows Installer em PCs Windows 10 inscritos  
 O **do Windows Installer através de MDM (\*. msi)** tipo de instalador permite-lhe criar e implementar aplicações baseadas no Windows Installer em PCs inscritos que executam o Windows 10.  

 As considerações seguintes são aplicáveis quando utiliza este tipo de instalador:  

-   Só pode carregar um único ficheiro com a extensão .msi.  

-   O código de produto do ficheiro e a versão do produto são utilizados para deteção da aplicação.  

-   É utilizado o comportamento de reinício predefinido da aplicação. O Configuration Manager não controla este procedimento.  

-   Por utilizador MSI são instalados pacotes para um único utilizador.  

-   Por máquina, são instalados pacotes MSI para todos os utilizadores do dispositivo.  

-   As atualizações de aplicações são suportadas quando o código de produto MSI de cada versão for igual.  

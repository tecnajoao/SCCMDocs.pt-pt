---
title: 'Como os utilizadores inscrevem dispositivos com o MDM no local '
titleSuffix: Configuration Manager
description: Compreenda como os utilizadores inscrevem dispositivos com gestão de dispositivos móveis no local no System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: dcf12937009a91bb8cc5a8c1c191861fec06ac13
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137563"
---
# <a name="how-users-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Como os utilizadores inscrevem dispositivos com gestão de dispositivos móveis no local no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Gestão de dispositivos móveis no local do System Center Configuration Manager, os utilizadores podem inscrever dispositivos se eles tem recebidos permissão de inscrição (através de definições de cliente atualizadas) e respetivos dispositivos tiverem o certificado de raiz necessário instalado para ter comunicações fidedignas com os servidores que alojam as funções do sistema de sites necessárias. Para obter mais informações sobre como configurar a inscrição, consulte [Configurar a inscrição de dispositivos para Gestão de Dispositivos Móveis no Local do System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md).  

> [!NOTE]  
>  O current branch do Configuration Manager suporta a inscrição na gestão de dispositivos móveis no local para dispositivos com os seguintes sistemas operativos:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team \(a partir do Configuration Manager versão 1602\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

As tarefas seguintes explicam como inscrever e verificar a inscrição de computadores e dispositivos para no\-no local a gestão de dispositivos móveis:  

-   [Inscrever um computador Windows 10](#bkmk_enrollDesk)  

-   [Inscrever um dispositivo Windows 10 Mobile](#bkmk_enrollMob)  

-   [Verificar inscrição de dispositivos](#bkmk_verify)  

##  <a name="bkmk_enrollDesk"></a> Inscrever um computador Windows 10  

1.  Num computador Windows 10, aceda a **Definições**.  

2.  Clique em **Contas**e, em seguida, clique em **Acesso a trabalho**.  

3.  Em Acesso a trabalho, sob **Ligar ao trabalho ou escola**, clique em **Ligar**, introduza o seu endereço de e-mail de trabalho e clique em **Continuar**.  

4.  Introduza o FQDN do servidor que aloja a função de sistema de sites de ponto de proxy de registo e clique em **continuar**.  

5.  Em A ligar a um serviço, introduza a palavra-passe do seu e-mail de trabalho e clique em **Iniciar sessão**.  

6.  Clique em **Ignorar** para memorizar as informações de início de sessão e, após um curto período de tempo, o dispositivo está ligado.  

##  <a name="bkmk_enrollMob"></a> Inscrever um dispositivo Windows 10 Mobile  

1.  Num dispositivo Windows 10 Mobile, aceda a **Definições**.  

2.  Clique em **Contas**e, em seguida, clique em **Acesso a trabalho**.  

3.  Clique em **Ligar**.  

4.  Introduza o seu endereço de e-mail de trabalho e o FQDN do servidor que aloja a função de sistema de sites de ponto proxy de registo. Clique em **Ligar**.  

5.  No ecrã seguinte, introduza o seu endereço de e-mail de trabalho e a palavra-passe e, em seguida, clique em **Iniciar sessão**. Após um curto período de tempo, o dispositivo é inscrito. Clique em **Concluído**.  

##  <a name="bkmk_verify"></a> Verificar inscrição de dispositivos  
 Pode verificar que dispositivos foram inscritos com êxito na consola do Configuration Manager.  

1.  Inicie a consola do Configuration Manager.  

2.  Clique em **Ativos e Compatibilidade** > **Descrição geral** > **Dispositivos**. O dispositivo inscrito aparece na lista.  

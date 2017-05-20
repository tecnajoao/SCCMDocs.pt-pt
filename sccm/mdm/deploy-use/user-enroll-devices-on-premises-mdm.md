---
title: Como os utilizadores inscrevem os dispositivos com MDM no local - Configuration Manager | Documentos do Microsoft
description: "Compreenda como os utilizadores inscrevem os dispositivos com gestão de dispositivos móveis no local no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
caps.latest.revision: 9
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 507bad02c6e028f09a8b0c8a566ac55f7c3942a5
ms.openlocfilehash: 8c7438c2cc0bc66654eb3e74de10553df53181d9
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-users-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Como os utilizadores inscrevem os dispositivos com gestão de dispositivos móveis no local no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com a gestão de dispositivos móveis do System Center Configuration Manager no local, os utilizadores podem registar dispositivos se estes foram concedidas permissões de inscrição (título de definições de cliente atualizado) e os respetivos dispositivos tenham o certificado de raiz necessário instalado para ter fidedignidade comunicações com os servidores que alojam as funções do sistema de sites necessários. Para obter mais informações sobre como configurar a inscrição, consulte o artigo [configurado a inscrição de dispositivos para gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md).  

> [!NOTE]  
>  O ramo atual do Configuration Manager suporta a inscrição na gestão de dispositivos móveis no local para os dispositivos que executem os seguintes sistemas operativos:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team \(partir 1602 de versão do Configuration Manager\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

As tarefas seguintes explicam como inscrever e verifique se a inscrição de computadores e dispositivos no\-local gestão de dispositivos móveis:  

-   [Inscrever um computador Windows 10](#bkmk_enrollDesk)  

-   [Inscrever um dispositivo Windows 10 Mobile](#bkmk_enrollMob)  

-   [Verificar inscrição de dispositivos](#bkmk_verify)  

##  <a name="bkmk_enrollDesk"></a> Inscrever um computador Windows 10  

1.  Num computador Windows 10, aceda a **Definições**.  

2.  Clique em **Contas**e, em seguida, clique em **Acesso a trabalho**.  

3.  Em Acesso a trabalho, sob **Ligar ao trabalho ou escola**, clique em **Ligar**, introduza o seu endereço de e-mail de trabalho e clique em **Continuar**.  

4.  Introduza o FQDN do servidor que aloja a função de sistema de sites de ponto de proxy de inscrição e, clique em **continuar**.  

5.  Em A ligar a um serviço, introduza a palavra-passe do seu e-mail de trabalho e clique em **Iniciar sessão**.  

6.  Clique em **Ignorar** para memorizar as informações de início de sessão e, após um curto período de tempo, o dispositivo está ligado.  

##  <a name="bkmk_enrollMob"></a> Inscrever um dispositivo Windows 10 Mobile  

1.  Num dispositivo Windows 10 Mobile, aceda a **Definições**.  

2.  Clique em **Contas**e, em seguida, clique em **Acesso a trabalho**.  

3.  Clique em **Ligar**.  

4.  Introduza o seu endereço de e-mail de trabalho e o FQDN do servidor que aloja a função de sistema de sites de ponto proxy de registo. Clique em **Ligar**.  

5.  No ecrã seguinte, introduza o seu endereço de e-mail de trabalho e a palavra-passe e, em seguida, clique em **Iniciar sessão**. Após um curto período de tempo, o dispositivo é inscrito. Clique em **Concluído**.  

##  <a name="bkmk_verify"></a> Verificar inscrição de dispositivos  
 Pode verificar que dispositivos tenham sido inscritos com êxito na consola do Configuration Manager.  

1.  Inicie a consola do Configuration Manager.  

2.  Clique em **Ativos e Compatibilidade** > **Descrição geral** > **Dispositivos**. O dispositivo inscrito aparece na lista.  


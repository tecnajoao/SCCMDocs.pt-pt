---

title: Inscrever dispositivos | Documentos do Microsoft
description: "Saiba mais sobre os métodos de inscrição de dispositivos para gestão de dispositivos móveis no local no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
caps.latest.revision: 6
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 3b1451edaed69a972551bd060293839aa11ec8b2
ms.openlocfilehash: 4abaef35969ef1a5340ae8ca8aa5699cd3942642
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="enroll-devices-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Inscrever dispositivos para Gestão de Dispositivos Móveis no Local do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para gerir computadores e dispositivos com gestão de dispositivos móveis no local do System Center Configuration Manager, os dispositivos tem de estar inscritos para que o Configuration Manager pode comunicar com os dispositivos para tarefas de gestão. O Configuration Manager fornece dois métodos para a inscrição de dispositivos:  

-   **Inscrição de utilizadores** - Neste método, os utilizadores iniciam o processo de inscrição nos respetivos dispositivos. Para inscrição de utilizadores ser concluída com êxito, o dispositivo tem de ter um certificado de raiz fidedigna instalado no mesmo e o utilizador têm de ser aprovisionado para inscrição pelo Configuration Manager.  Para inscrever o dispositivo, o utilizador fornece simplesmente as credenciais de trabalho e o dispositivo é inscrito para ser gerido.  

     Para obter mais informações, consulte o artigo [como os utilizadores inscrevem os dispositivos com gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

-   **Inscrição em massa** - Neste método, o utilizador do dispositivo não tem de iniciar a inscrição. Em vez disso, um pacote de inscrição em massa criado no Configuration Manager e é, em seguida, colocar no dispositivo e aberto. Quando aberto, o pacote fornece as informações necessárias para inscrever o dispositivo.  

     Para obter mais informações, consulte o artigo [como efetuar a inscrição em massa de dispositivos com gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/deploy-use/bulk-enroll-devices-on-premises-mdm.md)  

 > [!NOTE]  
>  O ramo atual do Configuration Manager suporta a inscrição na gestão de dispositivos móveis no local para os dispositivos que executem os seguintes sistemas operativos:  
>   
>  -   Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team 
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise   


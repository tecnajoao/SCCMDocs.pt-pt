---
title: Inscrever dispositivos | Microsoft Docs
description: "Saiba mais sobre métodos para inscrever dispositivos para gestão de dispositivos móveis no local no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
caps.latest.revision: "6"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 4abaef35969ef1a5340ae8ca8aa5699cd3942642
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="enroll-devices-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Inscrever dispositivos para Gestão de Dispositivos Móveis no Local do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para gerir computadores e dispositivos com gestão de dispositivos móveis no local do System Center Configuration Manager, os dispositivos têm de estar inscritos para que o Configuration Manager podem comunicar com os dispositivos para tarefas de gestão. Configuration Manager fornece dois métodos de inscrição de dispositivos:  

-   **Inscrição de utilizadores** - Neste método, os utilizadores iniciam o processo de inscrição nos respetivos dispositivos. Para inscrição do utilizador seja concluída com êxito, o dispositivo tem de ter um certificado de raiz fidedigna instalado e o utilizador tem de ser aprovisionado para inscrição pelo Configuration Manager.  Para inscrever o dispositivo, o utilizador fornece simplesmente as credenciais de trabalho e o dispositivo é inscrito para ser gerido.  

     Para obter mais informações, consulte [como os utilizadores inscrevem dispositivos com gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

-   **Inscrição em massa** - Neste método, o utilizador do dispositivo não tem de iniciar a inscrição. Em vez disso, um pacote de inscrição em volume criados no Configuration Manager e é, em seguida, colocado no dispositivo e aberto. Quando aberto, o pacote fornece as informações necessárias para inscrever o dispositivo.  

     Para obter mais informações, consulte [como a inscrição em massa de dispositivos com gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/deploy-use/bulk-enroll-devices-on-premises-mdm.md)  

 > [!NOTE]  
>  O ramo atual do Configuration Manager suporta a inscrição na gestão de dispositivos móveis no local para dispositivos que executam os sistemas operativos seguintes:  
>   
>  -   Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team 
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise   

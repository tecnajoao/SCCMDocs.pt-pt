---
title: 'Inscrever dispositivos '
titleSuffix: Configuration Manager
description: Saiba mais sobre métodos para inscrever dispositivos para gestão de dispositivos móveis no local no System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d27e81da4da7caa89988d78a705648c5709cc2c3
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130348"
---
# <a name="enroll-devices-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Inscrever dispositivos para Gestão de Dispositivos Móveis no Local do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para gerir computadores e dispositivos com gestão de dispositivos móveis no local do System Center Configuration Manager, os dispositivos têm de ser inscritos para que o Configuration Manager pode comunicar com os dispositivos para tarefas de gestão. O Configuration Manager fornece dois métodos de inscrição de dispositivos:  

- **Inscrição de utilizadores** - Neste método, os utilizadores iniciam o processo de inscrição nos respetivos dispositivos. Para a inscrição de utilizador seja concluída com êxito, o dispositivo tem de ter um certificado de raiz fidedigna instalado no mesmo e o utilizador tem de ser aprovisionado para inscrição pelo Configuration Manager.  Para inscrever o dispositivo, o utilizador fornece simplesmente as credenciais de trabalho e o dispositivo é inscrito para ser gerido.  

   Para obter mais informações, consulte [Como os utilizadores inscrevem dispositivos com gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

- **Inscrição em massa** - Neste método, o utilizador do dispositivo não tem de iniciar a inscrição. Em vez disso, um pacote de inscrição em massa criada no Configuration Manager e é, em seguida, colocado no dispositivo e aberto. Quando aberto, o pacote fornece as informações necessárias para inscrever o dispositivo.  

   Para obter mais informações, consulte [como inscrição em massa de dispositivos com gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/deploy-use/bulk-enroll-devices-on-premises-mdm.md)  

  > [!NOTE]
  >  O current branch do Configuration Manager suporta a inscrição na gestão de dispositivos móveis no local para dispositivos com os seguintes sistemas operativos:  
  > 
  > - Windows 10 Enterprise  
  >   -   Windows 10 Pro  
  >   -   Windows 10 Team 
  >   -   Windows 10 Mobile  
  >   -   Windows 10 Mobile Enterprise   

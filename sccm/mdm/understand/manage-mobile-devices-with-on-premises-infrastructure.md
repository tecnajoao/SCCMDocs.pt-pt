---
title: "No local a gestão de dispositivos móveis (MDM) | Documentos do Microsoft"
description: "Saiba mais sobre gestão de dispositivos móveis no local, uma solução de gestão de dispositivos no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
caps.latest.revision: 8
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: 7b96c4d4d87aa150eacc5d7d20710f5d2199e48a
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="on-premises-mobile-device-management-mdm-in-system-center-configuration-manager"></a>Gestão de dispositivos móveis no local (MDM) no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager no\-local a gestão de dispositivos móveis é uma solução de gestão de dispositivos que se baseie nas capacidades de gestão incorporado dos sistemas operativos de dispositivo (com base num padrão abra Gestão de dispositivos de Alliance móveis ou OMA DM) ao utilizar a infraestrutura do Configuration Manager de um enterprise para gerir e manter os dispositivos. No\-local gestão de dispositivos móveis requer o Microsoft Intune para configurar a capacidade de gestão, mas só é necessária para a subscrição (e a horas para ajudar a notificar dispositivos para procurar alterações na política), mas não é utilizado para gerir dispositivos ou armazenar dados acerca dos mesmos.  

 ![No\-local conceptual](media/On-premises-conceptual.png)  

 No\-local gestão de dispositivos móveis é diferente do Microsoft Intune, que depende também capacidades de OMA DM incorporadas, mas todas as funções de gestão são entregues através dos serviços de nuvem.  No\-local gestão de dispositivos móveis também é diferente da solução de gestão baseados no cliente tradicionalmente oferecida pelo Configuration Manager-depende da infraestrutura de empresa semelhantes mas não utiliza separadamente instalado o software de cliente em computadores e dispositivos que gere.  

 A tabela abaixo lista as vantagens e desvantagens no\-local gestão de dispositivos móveis em comparação com tradicional gestão baseadas no cliente:  

|Vantagens|Desvantagens|  
|----------------|-------------------|  
|**Infraestrutura simplificada** - são necessárias menos funções do sistema de sites.<br /><br /> **Mais fácil manter** -porque a funcionalidade de gestão está incorporada para o sistema operativo do dispositivo, novas versões do software de cliente não são necessárias quando são introduzidas novas funcionalidades de gestão para o sistema do Configuration Manager.<br /><br /> **No local** - todos os dados e gestão são mantidos no local.|**Menos funcionalidades de gestão de clientes** - sem orquestração, medição de software, integração de terceiros, a sequências de tarefas ou centro de suporte de software.<br /><br /> **Dispositivo suporte limitado** - atualmente no\-local gestão de dispositivos móveis apenas suporta dispositivos que executam o Windows 10 e Windows 10 Mobile.|  

 Os tópicos seguintes fornece informações que pode utilizar para planear, preparar e inscrever dispositivos para no\-local gestão de dispositivos móveis:  

-   [Planear a gestão de dispositivos móveis no local no System Center Configuration Manager](../plan-design/plan-on-premises-mdm.md)  

     Saiba mais sobre o que deve ter em conta quando configurar a infraestrutura do Configuration Manager e planeamento de inscrição de dispositivos no\-local gestão de dispositivos móveis.  

-   [Passos de preparação para a gestão de dispositivos móveis no local no System Center Configuration Manager](../get-started/preparation-steps-for-on-premises-mdm.md)  

     Saiba mais sobre como obter o sistema do Configuration Manager está preparado para no\-local gestão de dispositivos móveis ao configurar a subscrição do Microsoft Intune, configurar certificados, instalar funções do sistema de sites e configurar a inscrição de dispositivos.  

-   [Inscrever dispositivos para gestão de dispositivos móveis no local no System Center Configuration Manager](../deploy-use/enroll-devices-on-premises-mdm.md)  

     Saiba como ocorre a inscrição, como os utilizadores podem inscrever os seus dispositivos e como inscrever dispositivos em volume com um pacote de inscrição.  


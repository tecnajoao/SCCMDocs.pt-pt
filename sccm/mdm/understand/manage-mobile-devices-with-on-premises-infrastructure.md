---
title: Gestão de dispositivos móveis no local (MDM)
titleSuffix: Configuration Manager
description: Saiba mais sobre a gestão de dispositivos móveis no local, uma solução de gestão de dispositivos no System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ac0e4426b2025a88f126f9cc0b2e57f5a5313740
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347404"
---
# <a name="on-premises-mobile-device-management-mdm-in-system-center-configuration-manager"></a>Gestão de dispositivos móveis no local (MDM) no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager no\-no local de gestão de dispositivos móveis é uma solução de gestão de dispositivos que se baseia nas capacidades de gestão incorporada dos sistemas operativos de dispositivos (com base num padrão Open Mobile Alliance Device Management ou OMA DM) ao utilizar a infraestrutura do Configuration Manager de uma empresa para gerir e manter os dispositivos. No\-no local a gestão de dispositivos móveis requer o Microsoft Intune para configurar a capacidade de gestão, mas só é necessária para a subscrição (e, em alturas para ajudar a notificar os dispositivos para procurar alterações de política), mas não é utilizado para gerir dispositivos ou armazenar dados sobre os mesmos.  

 ![No\-local conceptual](media/On-premises-conceptual.png)  

 No\-local difere de gestão de dispositivos móveis do Microsoft Intune, que também baseia-se nas capacidades de OMA DM incorporadas, mas todas as funções de gestão são fornecidas através de serviços em nuvem.  No\-local gestão de dispositivos móveis também difere de acordo com a solução de gestão baseada no cliente tradicionalmente pelo Configuration Manager em que se baseia-se na infraestrutura da empresa semelhante, mas não utiliza separadamente o software de cliente instalado nos computadores e dispositivos que gere.  

 A tabela abaixo lista as vantagens e desvantagens de On\-no local a gestão de dispositivos móveis em comparação com a gestão tradicional baseada no cliente:  

|Vantagens|Desvantagens|  
|----------------|-------------------|  
|**Infraestrutura simplificada** - são necessárias menos funções do sistema de sites.<br /><br /> **Mais fácil de manter** -porque a funcionalidade de gestão está incorporada no sistema operativo do dispositivo, novas versões do software de cliente não são necessárias quando são introduzidas novas funcionalidades de gestão para o sistema do Configuration Manager.<br /><br /> **No local** - todos os dados e gestão são mantidos no local.|**Menos funcionalidades de gestão de clientes** - sem orquestração, medição de software, integração de terceiros, a sequências de tarefas ou centro de suporte de software.<br /><br /> **Suporte de dispositivos limitado** - atualmente na\-local gestão de dispositivos móveis apenas suporta dispositivos com Windows 10 e Windows 10 Mobile.|  

 Os tópicos seguintes fornecem informações que pode utilizar para planear, preparar e inscrever dispositivos para no\-no local a gestão de dispositivos móveis:  

-   [Planear a gestão de dispositivos móveis no local no System Center Configuration Manager](../plan-design/plan-on-premises-mdm.md)  

     Saiba mais sobre o que considerar ao configurar a infraestrutura do Configuration Manager e planeamento de inscrição de dispositivos num\-no local a gestão de dispositivos móveis.  

-   [Passos de preparação para gestão de dispositivos móveis no local no System Center Configuration Manager](../get-started/preparation-steps-for-on-premises-mdm.md)  

     Saiba mais sobre como preparar o sistema do Configuration Manager para no\-local gestão de dispositivos móveis ao configurar a subscrição do Microsoft Intune, configurar certificados, instalar funções do sistema de sites e como configurar a inscrição de dispositivos.  

-   [Inscrever dispositivos para gestão de dispositivos móveis no local no System Center Configuration Manager](../deploy-use/enroll-devices-on-premises-mdm.md)  

     Saiba como ocorre a inscrição, como os utilizadores podem inscrever os seus dispositivos e como inscrever dispositivos em volume com um pacote de inscrição.  

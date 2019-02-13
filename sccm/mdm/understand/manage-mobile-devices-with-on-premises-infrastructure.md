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
ms.collection: M365-identity-device-management
ms.openlocfilehash: 63a82c6b81d5a2e09c6f73b79c39372c96ed4e07
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56143661"
---
# <a name="on-premises-mobile-device-management-mdm-in-system-center-configuration-manager"></a>Gestão de dispositivos móveis no local (MDM) no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager no\-no local de gestão de dispositivos móveis é uma solução de gestão de dispositivos que se baseia nos recursos internos de gerenciamento de sistemas operativos de dispositivos (com base no Open Mobile Alliance Device Management ou OMA Padrão de DM) ao utilizar a infraestrutura do Configuration Manager de uma empresa para gerir e manter os dispositivos. No\-no local a gestão de dispositivos móveis requer o Microsoft Intune para configurar a capacidade de gestão, mas só é necessária para a subscrição (e, em momentos para ajudar a notificar os dispositivos para check-in para que as alterações de política), mas não é utilizado para gerir os dispositivos ou armazene dados sobre eles.  

 ![No\-locais conceituais](media/On-premises-conceptual.png)  

 No\-local a gestão de dispositivos móveis é diferente do Microsoft Intune, que também se baseia em capacidades de OMA DM incorporadas, mas todas as funções de gerenciamento são fornecidas por meio de serviços cloud.  No\-locais a gestão de dispositivos móveis também é diferente da solução de gestão baseada no cliente disponibilizada tradicionalmente pelo Configuration Manager em que ele baseia-se na infraestrutura da empresa semelhante, mas não utiliza separadamente instalou o cliente software nos computadores e dispositivos que gere.  

 A tabela abaixo lista as vantagens e desvantagens de On\-no local a gestão de dispositivos móveis em comparação com a gestão tradicional baseada no cliente:  

|Vantagens|Desvantagens|  
|----------------|-------------------|  
|**Infraestrutura simplificada** - são necessárias menos funções do sistema de sites.<br /><br /> **Mais fácil de manter** -porque a funcionalidade de gestão está incorporada no sistema operativo do dispositivo, as novas versões do software de cliente não são necessárias quando são introduzidas novas funcionalidades de gestão do sistema do Configuration Manager.<br /><br /> **No local** - todos os dados e gestão são mantidos no local.|**Menos funcionalidades de gestão de clientes** - sem orquestração, medição de software, integração de terceiros, a sequências de tarefas ou centro de suporte de software.<br /><br /> **Suporte de dispositivos limitado** – no momento\-locais a gestão de dispositivos móveis apenas suporta dispositivos com Windows 10 e Windows 10 Mobile.|  

 Os tópicos seguintes fornecem informações que pode utilizar para planejar, preparar e inscrever dispositivos para no\-no local a gestão de dispositivos móveis:  

-   [Planear a Gestão de Dispositivos Móveis no Local no System Center Configuration Manager](../plan-design/plan-on-premises-mdm.md)  

     Saiba mais sobre o que considerar ao configurar a infraestrutura do Configuration Manager e planejamento de inscrição de dispositivos na\-no local a gestão de dispositivos móveis.  

-   [Passos de preparação para Gestão de Dispositivos Móveis no Local do System Center Configuration Manager](../get-started/preparation-steps-for-on-premises-mdm.md)  

     Saiba mais sobre como preparar o sistema do Configuration Manager para no\-locais gestão de dispositivos móveis ao configurar a subscrição do Microsoft Intune, como configurar certificados, instalar funções do sistema de sites e configurar a inscrição do dispositivo.  

-   [Inscrever dispositivos para Gestão de Dispositivos Móveis no Local do System Center Configuration Manager](../deploy-use/enroll-devices-on-premises-mdm.md)  

     Saiba como ocorre a inscrição, como os utilizadores podem inscrever os seus dispositivos e como inscrever dispositivos em volume com um pacote de inscrição.  

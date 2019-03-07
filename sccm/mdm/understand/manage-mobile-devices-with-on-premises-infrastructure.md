---
title: MDM no local
titleSuffix: Configuration Manager
description: Saiba mais sobre a gestão de dispositivos móveis no local, uma solução de gestão de dispositivos no Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49e07a7ebe6ec53d61ea9e2ee3bc941dd8561094
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558223"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>MDM no local no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager no local a gestão de dispositivos móveis (MDM) é uma solução de gestão de dispositivos que se baseia nos recursos internos de gerenciamento do SO do dispositivo. Esta funcionalidade baseia-se a norma de gestão de dispositivos da Open Mobile Alliance (OMA) (DM). Utiliza a infraestrutura do Configuration Manager da sua organização para gerir e manter os dispositivos. No local requer o Microsoft Intune para configurar a capacidade de gestão MDM, mas só é necessária para a subscrição. Intune é por vezes, utilizado para o ajudar a notificar os dispositivos para check-in para que as alterações de política, mas não é utilizado para gerir dispositivos ou armazenar dados sobre eles.  

![No\-locais conceituais](media/On-premises-conceptual.png)  

MDM no local é diferente do Microsoft Intune, que também conta com capacidades de OMA DM incorporadas. Todas as funções de gestão no Intune são fornecidas por meio de serviços cloud. MDM no local também é diferente da solução de gestão baseada no cliente disponibilizada tradicionalmente pelo Configuration Manager. Ele se baseia numa infraestrutura semelhante, mas não utiliza software de cliente instalado em separado nos dispositivos que gere.  

> [!Note]  
> A partir da versão 1810, uma ligação do Intune já não é necessária para novas implementações de MDM no local.<!--3607730, fka 1359124--> Sua organização ainda requer licenças do Intune para utilizar esta funcionalidade. Atualmente não é possível remover a ligação do Intune a partir de implementações de MDM no local existentes. Para obter mais informações, consulte a [mensagem de blogue de suporte do Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

A tabela seguinte lista as vantagens e desvantagens da MDM no local em comparação com a gestão tradicional baseada no cliente:  

|Vantagens|Desvantagens|  
|----------------|-------------------|  
|**Infraestrutura simplificada** - são necessárias menos funções do sistema de sites.<br /><br /> **Mais fácil de manter** – porque a funcionalidade de gestão incorporada no sistema operativo do dispositivo, as novas versões do software de cliente não são necessários quando são introduzidas novas funcionalidades de gestão do sistema do Configuration Manager.<br /><br /> **No local** - todos os dados e gestão são mantidos no local.|**Menos funcionalidades de gestão de clientes** - sem orquestração, medição de software, integração de terceiros, a sequências de tarefas ou centro de suporte de software.<br /><br /> **Suporte de dispositivos limitado** – atualmente no local MDM apenas suporta dispositivos com o Windows 10 e Windows 10 Mobile.|  

Os seguintes artigos fornecem informações que pode utilizar para planejar, preparar e inscrever dispositivos para MDM no local:  

- [Plano de MDM no local](/sccm/mdm/plan-design/plan-on-premises-mdm)  

    Saiba mais sobre o que considerar quando configurar a infraestrutura do Configuration Manager e o planejamento para inscrição de dispositivos no MDM no local  

- [Passos de preparação para a MDM no local](/sccm/mdm/get-started/preparation-steps-for-on-premises-mdm)  

    Prepare-se do Configuration Manager para MDM no local. Configurar a subscrição do Microsoft Intune, configurar certificados, instalar funções do sistema de sites e configurar a inscrição do dispositivo.  

- [Inscrever dispositivos para MDM no local](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  

    Saiba como ocorre a inscrição, como os utilizadores podem inscrever os seus dispositivos e como inscrever dispositivos em volume com um pacote de inscrição.  


---
title: Preparar para a MDM no local
titleSuffix: Configuration Manager
description: Preparar para gerir dispositivos com gestão de dispositivos móveis no local no Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fad5ce96b84b5a6edfafdead64cff0223009ebf8
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558053"
---
# <a name="preparation-steps-for-on-premises-mdm-in-configuration-manager"></a>Passos de preparação para a MDM no local no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para gerir dispositivos com gestão de dispositivos móveis no local do Configuration Manager (MDM), primeiro configure a infraestrutura necessária. Tem das funções do sistema de sites necessárias comunicar através de um canal fidedigno com os dispositivos móveis. Estas funções incluem o ponto proxy de registo, ponto de registo, ponto de gestão de dispositivos e ponto de distribuição.

As seguintes tarefas de alto nível são necessários para preparar o Configuration Manager para MDM no local:  

- [Configurar uma subscrição do Microsoft Intune para MDM no local](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm)  

    Inscreva-se para o Microsoft Intune e, em seguida, adicione a subscrição para o Configuration Manager através da consola do Configuration Manager. Este passo é necessário apenas para efeitos de licenciamento. O Intune não é utilizado para gerir os dispositivos ou armazenar informações de gestão. Todos os coordenação e gestão de dispositivos é com a sua organização com a infraestrutura do Configuration Manager no local.  

    > [!Note]  
    > A partir da versão 1810, uma ligação do Intune já não é necessária para novas implementações de MDM no local.<!--3607730, fka 1359124--> Sua organização ainda requer licenças do Intune para utilizar esta funcionalidade. Atualmente não é possível remover a ligação do Intune a partir de implementações de MDM no local existentes. Para obter mais informações, consulte a [mensagem de blogue de suporte do Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

- [Instalar funções do sistema de sites para MDM no local](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm)  

    Instalar e configurar os sistemas de sites necessários para gerir dispositivos com a infraestrutura do Configuration Manager no local. No mínimo, esta funcionalidade requer o ponto proxy de registo, ponto de registo, ponto de gestão de dispositivos e as funções de ponto de distribuição.  

- [Configurar certificados para comunicações fidedignas para a MDM no local](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  

    Configure a infraestrutura do Configuration Manager no local para permitir comunicações fidedignas (HTTPS) entre dispositivos geridos e os servidores que alojam as funções do sistema de sites necessárias.  

- [Configurar a inscrição de dispositivos para MDM no local](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

    Conceder permissão aos utilizadores inscrever computadores e dispositivos. Instale o certificado de raiz fidedigna nos dispositivos para permitir ligações HTTPS para os servidores de sistema de sites. Estes dispositivos normalmente não são associados a um domínio.  


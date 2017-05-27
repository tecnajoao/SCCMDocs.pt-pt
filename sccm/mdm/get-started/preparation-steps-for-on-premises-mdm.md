---
title: "Passos de preparação | Documentos do Microsoft"
description: "Prepare para gerir dispositivos com gestão de dispositivos móveis no local no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
caps.latest.revision: 4
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: 85bdadaaaeed9a42cfa5165d2b9f0f3ef434dc03
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="preparation-steps-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Passos de preparação para Gestão de Dispositivos Móveis no Local do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Gestão de dispositivos com o System Center Configuration Manager\-local a gestão de dispositivos móveis requer a infraestrutura do Configuration Manager para configurar o modo a que as funções de sistema de sites necessários (ponto de proxy de inscrição, o ponto de inscrição, o ponto de gestão de dispositivos e ponto de distribuição) podem comunicar através de um canal fidedigno com os dispositivos móveis para serem geridos.  

 As seguintes tarefas de alto nível necessários para preparar o sistema do Configuration Manager no\-local gestão de dispositivos móveis:  

-   [Configurar uma subscrição do Microsoft Intune para gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md)  

     Nesta tarefa, inscreva-se para o Microsoft Intune e, em seguida, adicione a subscrição para o Configuration Manager através da consola do Configuration Manager. Este passo é necessário apenas para efeitos de licenciamento. Intune não é utilizado para gerir os dispositivos ou armazenar informações de gestão. Todos os coordenação de problemas e gestão de dispositivos é com empresarial da sua organização utilizar a infraestrutura do Configuration Manager no local.  

-   [Instalar funções do sistema de sites para gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     Nesta tarefa, instalar e configurar as funções de sistema de sites necessárias para gerir dispositivos com a infraestrutura do Configuration Manager no local. No\-local gestão de dispositivos móveis requer mínimo funções do sistema de site de ponto a ponto proxy de registo, o ponto de inscrição, o ponto de gestão de dispositivos e a distribuição.  

-   [Configurar certificados para comunicações de fidedignas para gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

     Nesta tarefa, configurar a infraestrutura do Configuration Manager no local para permitirem comunicações fidedignas (HTTPS) entre os dispositivos geridos e servidores que alojam as funções do sistema de sites necessários.  

-   [Configurar a inscrição de dispositivos para gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

     Nesta tarefa, vai conceder permissão aos utilizadores para inscrever computadores e dispositivos e vai instalar o certificado de raiz fidedigna nos dispositivos (normalmente, aqueles que não estejam associados ao domínio) para permitir ligações HTTPS aos servidores do sistema de sites.  


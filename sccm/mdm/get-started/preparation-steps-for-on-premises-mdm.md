---
title: 'Passos de preparação '
titleSuffix: Configuration Manager
description: Prepare para gerir dispositivos com gestão de dispositivos móveis no local no System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 711af365353d68020a7bbbef8026f452d4203ce3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346761"
---
# <a name="preparation-steps-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Passos de preparação para Gestão de Dispositivos Móveis no Local do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Gerir dispositivos com o System Center Configuration Manager no\-no local requer a gestão de dispositivos móveis a infraestrutura do Configuration Manager para configurar para que as funções do sistema de sites necessárias (ponto proxy de registo, ponto de registo, ponto de gestão de dispositivos e ponto de distribuição) possam comunicar através de um canal fidedigno com os dispositivos móveis para serem geridos.  

 As seguintes tarefas de alto nível são necessários para preparar o sistema do Configuration Manager no\-no local a gestão de dispositivos móveis:  

-   [Configurar uma subscrição do Microsoft Intune para gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md)  

     Nesta tarefa, inscreva-se para o Microsoft Intune e, em seguida, adicione a subscrição para o Configuration Manager através da consola do Configuration Manager. Este passo é necessário apenas para efeitos de licenciamento. Intune não é utilizado para gerir os dispositivos ou armazenar informações de gestão. Toda a coordenação e gestão de dispositivos é com enterprise da sua organização através da infraestrutura do Configuration Manager no local.  

-   [Instalar funções do sistema de sites para gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     Nesta tarefa, instalar e configurar as funções de sistema de sites necessárias para gerir dispositivos com a infraestrutura do Configuration Manager no local. No\-local minimamente gestão de dispositivos móveis requer o ponto proxy de registo, ponto de registo, ponto de gestão de dispositivos e pontos de distribuição funções do sistema de sites.  

-   [Configurar certificados para comunicações fidedignas para a gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

     Nesta tarefa, configurar a infraestrutura do Configuration Manager no local para permitir comunicações fidedignas (HTTPS) entre os dispositivos geridos e os servidores que alojam as funções do sistema de sites necessárias.  

-   [Configurar a inscrição de dispositivos para gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

     Nesta tarefa, vai conceder permissão aos utilizadores para inscrever computadores e dispositivos e vai instalar o certificado de raiz fidedigna nos dispositivos (normalmente, aqueles que não estejam associados ao domínio) para permitir ligações HTTPS aos servidores do sistema de sites.  

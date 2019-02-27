---
title: Cenários para implementar sistemas operativos empresariais
titleSuffix: Configuration Manager
description: Saiba mais sobre os vários cenários para implementar sistemas operativos empresariais com o Configuration Manager.
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6d34c3d8dfa753934f03337d68e989a8bf8fcd7
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838706"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-configuration-manager"></a>Cenários para implementar sistemas operativos empresariais com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os seguintes cenários de implementação do sistema operacional estão disponíveis no Configuration Manager:  

#### <a name="upgrade-windows-to-the-latest-version"></a>Atualizar o Windows para a versão mais recente
Este cenário atualiza o sistema operacional nos computadores atualmente com o Windows 7, Windows 8.1 ou Windows 10. O processo de atualização mantém as aplicações, definições e dados de utilizador no computador. Não existem sem dependências externas, como o Windows ADK. Este processo pode ser mais rápido e mais resiliente do que as Implantações de SO tradicionais.  

Para obter mais informações, consulte [atualizar o Windows para a versão mais recente](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version).


#### <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot para dispositivos existentes
<!--3607717, fka 1358333--> Windows Autopilot para dispositivos existentes a partir da versão 1810, está disponível com o Windows 10 versão 1809 ou posterior. Esta funcionalidade permite-lhe criar uma nova imagem e aprovisionar um dispositivo Windows 7 para o modo de controlada pelo usuário de Windows Autopilot com uma única sequência de tarefas do Configuration Manager.

Para obter mais informações, consulte [Windows Autopilot para dispositivos existentes](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices).


#### <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Atualizar um computador existente com uma nova versão do Windows
Este cenário particiona e formata (limpa) um computador existente e instala um novo sistema operacional no computador. É possível migrar as definições e dados de utilizador após a instalação do sistema operacional.  

Para obter mais informações, consulte [atualizar um computador existente com uma nova versão do Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows).


#### <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal"></a>Instalar uma nova versão do Windows num novo computador (bare-metal)
Este cenário instala um sistema operacional num novo computador. É uma nova instalação do sistema operacional e não inclui definições ou migração de dados do utilizador.  

Para obter mais informações, consulte [instalar uma nova versão do Windows num novo computador (bare-metal)](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal).


#### <a name="replace-an-existing-computer-and-transfer-settings"></a>Substituir um computador existente e transferir definições
Este cenário instala um sistema operacional num novo computador. Opcionalmente, é possível migrar as definições e dados do utilizador do computador antigo para o novo computador.  

Para obter mais informações, consulte [substituir um computador existente e transferir definições](/sccm/osd/deploy-use/replace-an-existing-computer-and-transfer-settings).



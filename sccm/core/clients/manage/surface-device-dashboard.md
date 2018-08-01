---
title: Dashboard de dispositivos Surface
titleSuffix: Configuraton Manager
description: Rever as informações sobre dispositivos Surface, utilizar o dashboard.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: 96bca886b25cbe5f6ae1c2f06cbc823b4f017075
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383920"
---
# <a name="surface-device-dashboard-in-system-center-configuration-manager"></a>Dashboard de dispositivos Surface no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir na versão 1802, o dashboard de dispositivos Surface fornece informações sobre dispositivos Surface encontrado no seu ambiente único rapidamente. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Abra o dashboard de dispositivos Surface

Para abrir o dashboard de dispositivos Surface, utilize os seguintes passos: 

1. Abra a consola do Configuration Manager. 
2. Clique nas **monitorização** nó. 
3. Para carregar o dashboard, clique em **os dispositivos Surface**.

**Dashboard de dispositivos Surface**
![dashboard de dispositivos Surface](media\Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Rever informações no dashboard do dispositivo Surface

O dashboard de dispositivos Surface apresenta três gráficos para o seu ambiente. 

- **Percentagem de dispositivos Surface** -dá-lhe a percentagem de dispositivos Surface em todo o seu ambiente.

    ![Por cento do gráfico de dispositivos Surface](media\Percent-Surface-Devices.PNG)
- **Modelos de superfície** -mostra o número de dispositivos por modelo de superfície. 
    - Pairar o rato sobre uma seção de gráfico lhe dará a percentagem de dispositivos Surface que são o modelo selecionado. 

         ![Gráfico de modelos de surfaces](media\Surface-Models-Hover.PNG)
    - Clicar numa seção de gráfico leva-o para uma lista de dispositivos para o modelo. 
        ![Lista de dispositivos de superfície do modelo](media\Surface-Model-Device-List.PNG)

- **Principais cinco versões de firmware**-apresenta um gráfico com os modelos de firmware de cinco principais no seu ambiente. 
    - Pairar o rato sobre uma seção de gráfico fornece o número de dispositivos Surface que são a versão de firmware selecionada. A partir do Configuration Manager versão 1806, clicar numa seção de gráfico mostra uma lista de dispositivos relevantes. <!--1358654--> ![Lista de dispositivos de superfície do modelo](media\Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Mais informações

Para obter mais informações sobre dispositivos Surface, consulte:
 - O [superfície]( https://go.microsoft.com/fwlink/?linkid=861998) Web site.
    
Para obter mais informações sobre a implementação de atualizações de firmware superfície no Configuration Manager, consulte:
 - [Como gerir atualizações de controlador do Surface no Configuration Manager]( https://support.microsoft.com/help/4098906).





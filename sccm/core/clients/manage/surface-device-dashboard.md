---
title: Dashboard de dispositivo superfície
titleSuffix: Configuraton Manager
description: Rever as informações sobre dispositivos superfície através do dashboard.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: db5df73db6a973ca689def785ee99a40425303fa
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334560"
---
# <a name="surface-device-dashboard-in-system-center-configuration-manager"></a>Dashboard de dispositivo superfície no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir da versão 1802, o dashboard de dispositivo superfície dá-lhe informações sobre dispositivos superfície encontrado no seu ambiente rapidamente único. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Abra o dashboard de dispositivo superfície

Para abrir o dashboard de superfície do dispositivo, utilize os seguintes passos: 

1. Abra a consola do Configuration Manager. 
2. Clique em de **monitorização** nós. 
3. Para carregar o dashboard, clique em **dispositivos Surface**.

**Dashboard de dispositivo superfície**
![dashboard superfície do dispositivo](media\Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Rever informações no dashboard do dispositivo superfície

O dashboard de dispositivo superfície mostra três gráficos para o seu ambiente. 

- **Percentagem de dispositivos superfície** -dá-lhe a percentagem de dispositivos superfície em todo o seu ambiente.

    ![Percentagem do gráfico de dispositivos superfície](media\Percent-Surface-Devices.PNG)
- **Modelos de superfície** -mostra o número de dispositivos por modelo superfície. 
    - Posicionado sobre uma secção do gráfico irá dar-lhe a percentagem de dispositivos de descobrir que o modelo selecionado. 

         ![Gráfico de modelos superfície](media\Surface-Models-Hover.PNG)
    - Clicar numa secção gráfico leva-o para uma lista de dispositivos para o modelo. 
        ![Lista de dispositivos de modelo superfície](media\Surface-Model-Device-List.PNG)

- **Principais cinco versões de firmware**-apresenta um gráfico com os modelos de firmware primeiras cinco no seu ambiente. 
    - Posicionado sobre uma secção do gráfico irá dar-lhe o número de dispositivos de descobrir que a versão de firmware selecionado. 
       ![Lista de dispositivos de modelo superfície](media\Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Mais informações

Para obter mais informações sobre dispositivos superfície, consulte:
 - O [superfície]( https://go.microsoft.com/fwlink/?linkid=861998) Web site.
    
Para obter mais informações sobre a implementação de atualizações de firmware superfície no Configuration Manager, consulte:
 - [Como gerir atualizações de superfície controladores no Configuration Manager]( https://support.microsoft.com/help/4098906).





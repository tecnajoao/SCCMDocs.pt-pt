---
title: Dashboard de cogestão
titleSuffix: Configuration Manager
description: Rever as informações sobre como utilizar o dashboard de cogestão.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 72b42aec2b50e229b90e9a642343386e8588aab7
ms.sourcegitcommit: 2cc635835709fb8d86cdb63ea34233b36c94d4d8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/20/2018
ms.locfileid: "52259009"
---
# <a name="co-management-dashboard-in-system-center-configuration-manager"></a>Dashboard de cogestão no System Center Configuration Manager
*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir na versão 1802, pode ver um dashboard com informações sobre a cogestão. O dashboard ajuda-o a rever as máquinas que fazem cogeridas no seu ambiente. Os gráficos podem ajudar a identificar os dispositivos que possam necessitar de atenção.<!--1356648-->

## <a name="open-the-co-management-dashboard"></a>Abra o dashboard de cogestão
Para abrir o dashboard de cogestão, utilize os seguintes passos: 

1. Abra a consola do Configuration Manager. 
2. Clique nas **monitorização** nó. 
3. Para carregar o dashboard, clique em **cogestão**.

## <a name="reviewing-information-in-the-co-management-dashboard"></a>Rever informações no dashboard de cogestão

O dashboard de cogestão mostra quatro gráficos para o seu ambiente. 

- **Dispositivos cogeridos** -dá-lhe a percentagem de dispositivos cogeridos em todo o seu ambiente.

    ![Gráfico de dispositivos cogeridos](media\co-management-dashboard\Percent-Co-managed-graph.PNG)

- **Distribuição de SO de cliente** -mostra o número de cliente dispositivos por sistema operacional por versão. Os seguintes agrupamentos são usados: </br>
    - Windows 7 & 8.x
    - Windows 10 inferior a 1709
    - Windows 10 1709 e superior

         > [!NOTE] 
         > Windows 10, versão 1709 ou posterior, é um pré-requisito para a cogestão.

     Pairar o rato sobre uma seção de gráfico lhe dará a percentagem de dispositivos no SO de agrupamento selecionado.

     ![Gráfico de distribuição de SO de cliente](media\co-management-dashboard\Co-management-OS-distribution-graph.PNG)

- **Estado de cogestão**-a divisão de êxito de dispositivo ou a falha nas seguintes categorias:
    - Êxito, Azure AD híbrido associado
    - Êxito, associados ao Azure AD
    - Falha de: Inscrição automática falhou
    
     Pairar o rato sobre uma seção de gráfico dá-lhe a percentagem de dispositivos na categoria. 

     ![Gráfico de estado para a cogestão](media\co-management-dashboard\Co-management-status-graph.PNG)

     Clicar numa seção de gráfico, leva-o para uma lista de dispositivos para a categoria.
 
     ![Lista de dispositivos de falha de inscrição](media\co-management-dashboard\Enrollment-Failure_Device-List.PNG)


- **Transição da carga de trabalho**-apresenta um gráfico de barras com o número de dispositivos que transitado para o Microsoft Intune para as cargas de trabalho disponíveis quatro:
    - Políticas de conformidade
    - Acesso a recursos
    - Windows Update para empresas
    - Endpoint Protection

     Pairar o rato sobre uma seção de gráfico fornece o número de dispositivos a transição para a carga de trabalho. 
     ![Gráfico de barras de transição de carga de trabalho](media\co-management-dashboard\Workload-Transition.PNG)


## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre a cogestão, consulte:
 - [Cogestão para os dispositivos com Windows 10](/sccm/core/clients/manage/co-management-overview)
 - [Preparar os dispositivos com Windows 10 para a cogestão](/sccm/core/clients/manage/co-management-prepare)

    

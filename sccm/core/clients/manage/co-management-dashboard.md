---
title: Dashboard de gestão conjunta
titleSuffix: Configuraton Manager
description: Rever as informações sobre a gestão conjunta através do dashboard.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cdf073aa3e9ca3be6062ea0e5e0528bb97937989
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32333407"
---
# <a name="co-management-dashboard-in-system-center-configuration-manager"></a>Dashboard de gestão conjunta no System Center Configuration Manager
*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir da versão 1802, pode ver um dashboard com informações sobre a gestão conjunta. O dashboard ajuda a rever máquinas que estejam conjuntamente geridas no seu ambiente. Os gráficos podem ajudar a identificar dispositivos que necessitem de atenção.<!--1356648-->

## <a name="open-the-co-management-dashboard"></a>Abra o dashboard de gestão conjunta
Para abrir o dashboard de gestão conjunta, utilize os seguintes passos: 

1. Abra a consola do Configuration Manager. 
2. Clique em de **monitorização** nós. 
3. Para carregar o dashboard, clique em **gestão conjunta**.

## <a name="reviewing-information-in-the-co-management-dashboard"></a>Rever informações no dashboard de gestão conjunta

O dashboard de gestão conjunta mostra quatro gráficos para o seu ambiente. 

- **Dispositivos geridos conjuntamente** -dá-lhe a percentagem de dispositivos geridos conjuntamente em todo o seu ambiente.

    ![Gráfico de dispositivos geridos conjuntamente](media\co-management-dashboard\Percent-Co-managed-graph.PNG)

- **Distribuição de SO de cliente** -mostra o número de cliente dispositivos por SO por versão. São utilizados os agrupamentos seguintes: </br>
    - Windows 7 e 8. x
    - Windows 10 menor 1709
    - Windows 10 1709 e acima

         > [!NOTE] 
         > Windows 10, versão 1709 e posterior, é um pré-requisito para a gestão conjunta.

     Posicionado sobre uma secção do gráfico irá dar-lhe a percentagem de dispositivos no SO agrupamento selecionado.

     ![Gráfico de distribuição de SO de cliente](media\co-management-dashboard\Co-management-OS-distribution-graph.PNG)

- **Estado de gestão conjunta**-a repartição de dispositivo com êxito ou falha nas seguintes categorias:
    - Concluído com sucesso, híbrida do Azure AD associados
    - Concluído com sucesso, do Azure AD associado
    - Falha de: Falhada de inscrição automática
    
     Posicionado sobre uma secção do gráfico dá-lhe a percentagem de dispositivos da categoria. 

     ![Gráfico de estado para a gestão conjunta](media\co-management-dashboard\Co-management-status-graph.PNG)

     Clicar numa secção gráfico leva-o para uma lista de dispositivos para a categoria.
 
     ![Lista de dispositivos de falha de inscrição](media\co-management-dashboard\Enrollment-Failure_Device-List.PNG)


- **Transição de carga de trabalho**-apresenta um gráfico de barras com o número de dispositivos que transitou para o Microsoft Intune para as cargas de trabalho disponíveis quatro:
    - Políticas de conformidade
    - Acesso a recursos
    - Atualização do Windows para empresas
    - Endpoint Protection

     Posicionado sobre uma secção do gráfico irá dar-lhe o número de dispositivos transferidas para a carga de trabalho. 
     ![Gráfico de barras de transição de carga de trabalho](media\co-management-dashboard\Workload-Transition.PNG)


## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre a gestão de conjunta, consulte:
 - [Cogestão para os dispositivos com Windows 10](/sccm/core/clients/manage/co-management-overview.md)
 - [Preparar os dispositivos com Windows 10 para a cogestão](/sccm/core/clients/manage/co-management-prepare.md)

    

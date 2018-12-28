---
title: Dashboard de cogestão
titleSuffix: Configuration Manager
description: Utilize o dashboard de cogestão para rever as informações sobre dispositivos cogeridos.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5e20985ac8fc39f2384cee5d202e19fc69e2b348
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53414689"
---
# <a name="co-management-dashboard-in-configuration-manager"></a>Dashboard de cogestão no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir da versão 1802, ver um dashboard com informações sobre a cogestão. O dashboard ajuda-o a rever as máquinas que fazem cogeridas no seu ambiente. Os gráficos podem ajudar a identificar os dispositivos que possam necessitar de atenção.<!--1356648-->

Na consola do Configuration Manager, vá para o **monitorização** área de trabalho e selecione o **cogestão** nó.

A partir da versão 1810, o dashboard de cogestão é aprimorado com informações mais detalhadas. <!--1358980-->



## <a name="dashboard-tiles"></a>Mosaicos do dashboard 

O dashboard de cogestão apresenta mosaicos diferentes consoante a versão do site. 


### <a name="co-managed-devices"></a>Dispositivos cogeridos

*Aplica-se a versões 1802 e 1806*

Mostra a percentagem de dispositivos cogeridos em todo o seu ambiente.
 ![Mosaico de dispositivos cogeridos](media/co-management-dashboard/Percent-Co-managed-graph.PNG)


### <a name="client-os-distribution"></a>Distribuição de SO de cliente

*Aplica-se a todas as versões* 

Mostra o número de cliente dispositivos por sistema operacional por versão. Ele usa os seguintes agrupamentos:  
- Windows 7 & 8.x  
- Windows 10 inferior a 1709  
- Windows 10 1709 e superior  

    > [!Tip]  
    > Windows 10, versão 1709 ou posterior, é um pré-requisito para a cogestão.  

Coloque o cursor sobre uma seção de gráfico para mostrar a percentagem de dispositivos nesse grupo de sistema operacional.
 ![Mosaico de distribuição de SO de cliente](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)


### <a name="co-management-status-donut"></a>Estado de cogestão (anel)

*Aplica-se a versões 1802 e 1806*

Mostra a divisão de dispositivo êxito ou falha nas seguintes categorias:
- Êxito, Azure AD híbrido associado  
- Êxito, associados ao Azure AD  
- Falha de: Inscrição automática falhou  

Coloque o cursor sobre uma seção de gráfico para mostrar a percentagem de dispositivos dessa categoria. 
 ![Mosaico de estado (anel) de cogestão](media/co-management-dashboard/Co-management-status-graph.PNG)

Selecione uma seção de gráfico para ver a lista de dispositivos dessa categoria.
 ![Lista de dispositivos de falha de inscrição](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)


### <a name="co-management-status-funnel"></a>Estado de cogestão (funil)

*Aplica-se a versão 1810 e posterior*

Um gráfico de funil que mostra o número de dispositivos com os seguintes Estados do processo de inscrição:  
- Dispositivos elegíveis  
- Agendado  
- Inscrição iniciada  
- Inscritos  

![Mosaico de estado (funil) de cogestão](media/co-management-dashboard/1358980-status-funnel.png)


### <a name="co-management-enrollment-status"></a>Estado de inscrição de cogestão

*Aplica-se a versão 1810 e posterior*

Mostra a divisão de estado do dispositivo nas seguintes categorias:
- Êxito, híbrido do Azure AD associado  
- Êxito, Azure AD associado  
- A inscrição, híbrido do Azure AD associado  
- Falha, híbrido do Azure AD associado  
- Falha, o Azure AD associado  
- Início de sessão de utilizadores pendentes  

Selecione um Estado no mosaico para explorar para obter uma lista de dispositivos com esse Estado.  

![Mosaico de estado de inscrição de cogestão](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="enrollment-errors"></a>Erros de inscrição

*Aplica-se a versão 1810 e posterior*

Uma tabela que mostra a contagem de erros de inscrição de dispositivos.  


### <a name="workload-transition"></a>Transição da carga de trabalho

*Aplica-se a todas as versões*

Apresenta um gráfico de barras com o número de dispositivos que tenha transferido para o Microsoft Intune para as cargas de trabalho disponíveis. (A lista de cargas de trabalho varia conforme a versão do Configuration Manager. Para obter mais informações, consulte [cargas de trabalho capazes de ser transferido para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune).)

Coloque o cursor sobre uma seção de gráfico para ver o número de dispositivos a transição para a carga de trabalho. 
 ![Gráfico de barras de transição de carga de trabalho](media/co-management-dashboard/Workload-Transition.PNG)


## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre a cogestão, consulte:
 - [Cogestão para os dispositivos com Windows 10](/sccm/core/clients/manage/co-management-overview)
 - [Preparar os dispositivos com Windows 10 para a cogestão](/sccm/core/clients/manage/co-management-prepare)

    

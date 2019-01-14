---
title: Monitor de cogestão
titleSuffix: Configuration Manager
description: Utilize o dashboard de cogestão para rever as informações sobre dispositivos cogeridos.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79ccb57b49f57f80e0915c8ab037d9f356166474
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54250995"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>Como monitorizar a cogestão no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Depois de ativar a cogestão, monitorize dispositivos de cogestão através dos seguintes métodos:

- [Dashboard de cogestão](#co-management-dashboard)  

- [Políticas de implementação](#deployment-policies)

- [Dados de dispositivo WMI](#wmi-device-data)



## <a name="co-management-dashboard"></a>Dashboard de cogestão

A partir da versão 1802, ver um dashboard com informações sobre a cogestão. O dashboard ajuda-o a rever as máquinas que fazem cogeridas no seu ambiente. Os gráficos podem ajudar a identificar os dispositivos que possam necessitar de atenção.<!--1356648-->

Na consola do Configuration Manager, vá para o **monitorização** área de trabalho e selecione o **cogestão** nó.

A partir da versão 1810, o dashboard de cogestão é aprimorado com informações mais detalhadas. <!--1358980-->

![Captura de ecrã do dashboard de cogestão](media/co-management-dashboard.png)


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

Apresenta um gráfico de barras com o número de dispositivos que tenha transferido para o Microsoft Intune para as cargas de trabalho disponíveis. 

A lista de cargas de trabalho varia consoante a versão do Configuration Manager. Para obter mais informações, consulte [cargas de trabalho capazes de ser transferido para o Intune](/sccm/comanage/workloads).

Coloque o cursor sobre uma seção de gráfico para ver o número de dispositivos a transição para a carga de trabalho. 

![Gráfico de barras de transição de carga de trabalho](media/co-management-dashboard/Workload-Transition.PNG)



## <a name="deployment-policies"></a>Políticas de implementação

Duas políticas são criadas no **implementações** nó da **monitorização** área de trabalho. É uma política para o grupo piloto e outro para produção. Estas políticas apenas o número de dispositivos onde o Configuration Manager tem aplicada a política de relatório. Eles não considerarem quantos dispositivos estão inscritos no Intune, que é um requisito antes dos dispositivos podem ser geridos conjuntamente.  



## <a name="wmi-device-data"></a>Dados de dispositivo WMI

Consulta a **SMS_Client_ComanagementState** classe WMI. Pode criar coleções personalizadas no Configuration Manager, que ajudam a determinar o estado da implementação da cogestão. Para obter mais informações sobre como criar coleções personalizadas, consulte [como criar coleções](/sccm/core/clients/manage/collections/create-collections). 

Os campos seguintes estão disponíveis na classe WMI:  

- **MachineId**: Um ID de dispositivo exclusivo para o cliente do Configuration Manager  

- **MDMEnrolled**: Especifica se o dispositivo é inscrito para MDM  

- **Autoridade**: A autoridade para o qual o dispositivo está inscrito  

- **ComgmtPolicyPresent**: Especifica se a política de cogestão do Configuration Manager existe no cliente. Se o **MDMEnrolled** valor é **0**, o dispositivo não está conjuntamente gerido independentemente disso, se a política de cogestão existe no cliente.  

Um dispositivo é cogeridos quando o **MDMEnrolled** campo e **ComgmtPolicyPresent** ambos os campos têm um valor de **1**.  

---
title: Gateway de gestão de cloud de monitor
titleSuffix: Configuration Manager
description: Monitorize os clientes e tráfego de rede através do gateway de gestão da cloud (CMG).
ms.date: 09/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ef27c67b9b17f41fbe71d57fdea9552b7dff9f7
ms.sourcegitcommit: 2badee2b63ae63687795250e298f463474063100
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/14/2018
ms.locfileid: "45601046"
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Monitorizar gateway de gestão da nuvem no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois do gateway de gestão na cloud (CMG) está em execução e os clientes estão a ligar através do mesmo, pode monitorizar os clientes e tráfego de rede para se certificar de que sabe como o serviço está sendo executada.



## <a name="monitor-clients"></a>Monitorar clientes

Os clientes ligados através do CMG aparecem na consola do Configuration Manager da mesma forma no local os clientes fazem. Para obter mais informações, consulte [como monitorizar clientes](/sccm/core/clients/manage/monitor-clients).



## <a name="monitor-traffic-in-the-console"></a>Tráfego de monitor na consola do

Monitorizar o tráfego na CMG utilizando a consola do Configuration Manager:

1. Vá para o **administração** área de trabalho, expanda **serviços Cloud**e selecione o **Gateway de gestão da nuvem** nó.  

2. Selecione de CMG no painel de lista.  

3. Ver as informações de tráfego no painel de detalhes para o ponto de ligação do CMG e as funções do sistema de sites liga-se ao.  



## <a name="set-up-outbound-traffic-alerts"></a>Configurar alertas de tráfego de saída

Alertas de tráfego de saída ajudá-lo a saber quando o tráfego de rede se aproxima de um nível de limiar de 14 dias. Ao criar CMG, pode configurar alertas de tráfego. Se saltou a essa parte, pode ainda configurar os alertas depois do serviço está em execução. Ajuste as definições de alerta em qualquer altura.

1. Vá para o **administração** área de trabalho, expanda **serviços Cloud**e selecione o **Gateway de gestão da nuvem** nó.  

2. Selecionar de CMG no painel de lista e, em seguida, selecione **propriedades** na faixa de opções.  

3. Vá para o **alertas** separador para permitir que o limiar e alertas. Especifique o limiar de 14 dias de dados em gigabytes (GB). Especifique também a percentagem de limiar para aumentar os diferentes níveis de alerta.  

4. Quando tiver terminado, selecione **OK**.  



## <a name="monitor-logs"></a>Registos de monitor

O CMG gera entradas num número de ficheiros de registo. Para obter mais informações, consulte [registos do Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="cloud-management-dashboard"></a>Dashboard de gestão da cloud
<!--1358461--> O dashboard de gestão da cloud a partir da versão 1806, fornece uma visão centralizada para utilização do CMG. Quando o site está incluído no [serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para gestão na cloud, também apresenta dados sobre os utilizadores da nuvem e dispositivos.  

Captura de ecrã seguinte é uma parte do dashboard de gestão na cloud, que mostra dois dos mosaicos disponíveis:  
![Tráfego de CMG de mosaicos de dashboard de gestão de nuvem e de clientes online atuais](media/1358461-cmg-dashboard.png)

Na consola do Configuration Manager, vá para o **monitorização** área de trabalho. Selecione o **gestão na Cloud** mosaicos do nó e ver o dashboard.  



## <a name="connection-analyzer"></a>Analisador da ligação

A partir da versão 1806, utilize o analisador de ligação CMG para a verificação em tempo real para ajudar a resolução de problemas. O utilitário na consola verifica o estado atual do serviço e o canal de comunicação através da ligação do CMG aponte para pontos de gestão que permitam o tráfego CMG.

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **serviços Cloud** e selecione o **gateway de gestão da nuvem** nó.  

2. Selecione a instância CMG de destino e, em seguida, selecione **analisador da ligação** na faixa de opções.  

3. Na janela de analisador da ligação do CMG, selecione uma das seguintes opções para autenticar com o serviço:  

     1. **Utilizador do Azure AD**: Utilize esta opção para simular communication o mesmo que uma identidade de utilizador baseadas na cloud entrar para um dispositivo do Azure Windows 10 associados ao AD. Clique em **sessão** em segurança, introduza as credenciais para esta conta de utilizador do Azure AD.  

     2. **Certificado de cliente**: Utilize esta opção para simular communication o mesmo que um cliente do Configuration Manager com um [certificado de autenticação de cliente](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate).  

4. Selecione **iniciar** para iniciar a análise. A janela de analisador apresenta os resultados. Selecione uma entrada para ver mais detalhes no campo Descrição.  


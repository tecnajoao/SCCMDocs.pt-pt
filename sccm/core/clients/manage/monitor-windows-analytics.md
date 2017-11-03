---
title: Monitor de clientes com Windows Analytics
titleSuffix: Configuration Manager
description: "A análise do Windows é um conjunto de soluções que são executados no Operations Management Suite que lhe permitem que desenhar informações valiosas para o estado atual do seu ambiente, tirando partido os dados de telemetria do Windows são reportados pelos dispositivos no seu ambiente."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
caps.latest.revision: "23"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 4d8c0eef8c85645ceb6f12aaf776ce1b1f82cbdd
ms.sourcegitcommit: d025a2cbd1ed82f42f67255c97b913f2163b3baf
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/02/2017
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Utilize a análise do Windows com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

[Análise de Windows](https://www.microsoft.com/WindowsForBusiness/windows-analytics) é um conjunto de soluções que são executados no [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview). Estas soluções permitem-lhe obter conhecimentos aprofundados sobre o estado atual do seu ambiente. Dispositivos no seu ambiente reportam dados de telemetria do Windows e estes dados podem ser acedidos e analisados através de soluções no [portal web do Operations Management Suite](https://mms.microsoft.com). Em case de [atualizar preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics) os dados podem também ser efetuados diretamente acionáveis no nó de monitorização da consola do Configuration Manager através da ligação de preparação de atualização para o Configuration Manager.

Os dados de telemetria do Windows utilizados pelo Windows Analytics não são transferidos diretamente para o servidor de site do Configuration Manager. Os computadores cliente enviam dados de telemetria do Windows para o serviço de telemetria e os dados relevantes, em seguida, são transferidos para soluções de análise do Windows alojadas de uma das áreas de trabalho OMS da sua organização. O Configuration Manager pode, em seguida, direcioná-lo para dados relevantes no portal web com ligações no contexto ou diretamente apresentar dados que façam parte das soluções que ligou ao Configuration Manager. Também diretamente pode consultar os dados a partir do portal web operação Management Suite.

>[!Important]
>[Dados de diagnóstico e utilização do Configuration Manager](../../plan-design/diagnostics/diagnostics-and-usage-data.md), que é comunicada para a Microsoft do servidor do site do Configuration Manager, é completamente independente da análise do Windows e a telemetria do Windows.

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Configurar clientes para dados de relatório para análise do Windows

Para dispositivos de cliente para o relatório de dados para análise do Windows, dispositivos tem de ser configurados com um ID de comerciais chave associado a área de trabalho do Operations Management Suite que aloja os dados de análise do Windows para a sua organização. Os dispositivos também tem de ser configurados para telemetria de relatório, um nível de telemetria adequado para a solução específica ou soluções que pretende utilizar. 

### <a name="configure-windows-analytics-client-settings"></a>Configurar definições de cliente Windows Analytics
Para configurar a análise do Windows, na consola do Configuration Manager escolha **administração** > **as definições de cliente**, faça duplo clique em **criar definições personalizadas do dispositivo cliente**e, em seguida, verifique **Windows Analytics**.  

Depois de navegar para o **Windows Analytics** separador Definições, configure o seguinte:
  -  **Chave de ID comercial**  
A chave de ID comercial mapeia informações dos dispositivos que gere para a área de trabalho do OMS que aloja os dados de análise do Windows da sua organização. Se já tiver configurado uma chave de ID comercial para utilização com a preparação de atualização, utilize esse ID. Se ainda não tiver uma chave de ID comercial, consulte [gerar a chave de ID comercial]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

  -  **Nível de telemetria para dispositivos Windows 10**   
Para obter informações sobre o que é recolhido por cada nível de telemetria do Windows 10, consulte [telemetria de configurar o Windows na sua organização](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

  -  **Escolher coleção de dados comerciais em dispositivos Windows 7, 8 e 8.1**   
Para informações sobre os dados recolhidos a partir destes sistemas operativos quando que optar ativamente por participar sessão, consulte Transferir o [eventos de telemetria appraiser Windows 7, Windows 8 e Windows 8.1 e campos](https://go.microsoft.com/fwlink/?LinkID=822965) ficheiro pdf da Microsoft.

  -  **Configurar o Internet explorar a recolha de dados**  
Em dispositivos com Windows 8.1 ou anteriores, Internet Explorer dados coleção pode permitir que a preparação de atualização detetar incompatibilidades de aplicação web que podem impedir uma atualização sem problemas para o Windows 10. Recolha de dados do Internet Explorer, pode ser ativada num por base de zona de internet. Para obter mais informações sobre as zonas de internet, consulte [sobre zonas de segurança do URL](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx).

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Utilize atualizar preparação para identificar problemas de compatibilidade do Windows 10

Preparação de atualização (anteriormente, análise de atualização) permite-lhe analisar a preparação do dispositivo e a compatibilidade com o Windows 10. Esta avaliação permite smoother atualizações. Depois de ligar o Configuration Manager a preparação de atualização, pode aceder a estes dados de compatibilidade da atualização do cliente diretamente na consola do Configuration Manager. Em seguida, poderá nos dispositivos de destino para a atualização ou correção da lista de dispositivos.

Para obter mais detalhes e informações sobre como configurar e ligar a preparação de atualização, consulte [atualizar preparação](../../clients/manage/upgrade/upgrade-analytics.md).

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Utilize a análise do Windows para identificar lacunas nas políticas de proteção de informações do Windows

Dispositivos do Windows 10 versão 1703 e posterior que estão configurados com um [Windows Information Protection](https://docs.microsoft.com/en-us/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) telemetria de relatório de política (WIP) em aplicações que aceder a dados empresariais no seu ambiente, mas que não são contabilizados nas regras de aplicação de política WIP. Estes são potencialmente aplicações que os utilizadores no seu ambiente tem de permanecer produtivo, mas que estão a ser bloqueou o acesso, para que os dados de conhecimento que estão a aceder a dados empresariais podem ser úteis para a manutenção das políticas de proteção de informações do Windows no Configuration Manager. 

Estes dados de proteção de informações do Windows podem ser acedidos utilizando este [consulta Operations Management Suite](https://go.microsoft.com/fwlink/?linkid=849952).
---
title: Monitorar clientes com o Windows Analytics
titleSuffix: Configuration Manager
description: Análise do Windows é um conjunto de soluções que permite a desenhar informações valiosas para o estado atual do seu ambiente.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8405a212f9e4cd845ac7591767eb27e5425f404e
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893656"
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Utilize o Windows Analytics com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

[Windows Analytics](https://docs.microsoft.com/windows/deployment/update/windows-analytics-overview) é um conjunto de soluções que permitem que pode obter informações sobre o estado atual do seu ambiente. Dispositivos do Windows nos seus dados de relatório de ambiente para a Microsoft, que pode aceder e analisar através destas soluções. Por exemplo, ligar [preparação de atualizações](/sccm/core/clients/manage/upgrade-readiness) para o Configuration Manager para acessar diretamente os dados no **monitorização** área de trabalho da consola do Configuration Manager.

Os dados usados pelo Windows Analytics não são disponibilizados diretamente para o servidor de site do Configuration Manager. Computadores cliente enviarem dados para o serviço em nuvem do Windows. Este serviço, então, transfere os dados relevantes para as soluções de análise de Windows hospedadas em uma das áreas de trabalho da sua organização. O Configuration Manager, em seguida, direciona-o para dados relevantes no portal web com links de contextual. Ele também diretamente pode exibir dados que fazem parte das soluções que se liga ao Configuration Manager.

> [!Important]  
> Relatórios do Configuration Manager diagnósticos e dados de utilização à Microsoft. Estes dados são separados dos dados de análise do Windows. Para obter mais informações, consulte [diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  



## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Configurar clientes para dados de relatório para o Windows Analytics

Para dispositivos de cliente para dados de relatório para o Windows Analytics, configurá-las com um *chave de ID comercial*. Esta chave é a área de trabalho do Log Analytics do Azure que aloja os seus dados de análise do Windows. Também configure dispositivos para os dados de relatório num nível adequado para as soluções específicas que pretende utilizar. 

### <a name="configure-windows-analytics-client-settings"></a>Configurar definições de cliente do Windows Analytics
Para configurar o Windows Analytics: 
1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho e selecione o **definições de cliente** nó.  
2. No Friso, selecione **criar definições personalizadas do dispositivo cliente**.  
3. Adicionar a **Windows Analytics** grupo para esta política de definições de cliente personalizadas do dispositivo.  

Para obter mais informações sobre como criar definições de cliente personalizada do dispositivo, consulte [como configurar as definições de cliente](/sccm/core/clients/deploy/configure-client-settings).

Selecione o **Windows Analytics** separador Definições e configure as seguintes definições:  

#### <a name="manage-windows-telemetry-settings-with-configuration-manager"></a>Gerir definições de telemetria do Windows com o Configuration Manager
Configure esta definição para **Sim** para configurar definições de dados de diagnóstico do Windows nos clientes do Windows.   

#### <a name="commercial-id-key"></a>Chave do ID comercial
A chave ID comercial mapeia informações dos dispositivos que gere para a área de trabalho do Log Analytics que aloja os dados de análise do Windows da sua organização. Se já tiver configurado uma chave de ID comercial para utilização com a preparação, use esse ID. Se ainda não tiver uma chave de ID comercial, veja [copiar a chave de ID comercial](https://docs.microsoft.com/windows/deployment/update/windows-analytics-get-started#copy-your-commercial-id-key).

#### <a name="windows-10-telemetry"></a>Telemetria do Windows 10
Para obter mais informações, consulte [dados de diagnóstico de configurar o Windows na sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization##diagnostic-data-level).

> [!Note]  
> Também pode definir a recolha de dados do Windows 10 para **avançado (limitado)**. Esta definição permite-lhe obter informações acionáveis sobre dispositivos no seu ambiente sem dispositivos que reportem todos os dados no **avançado** nível com o Windows 10 versão 1709 ou posterior. O nível avançado (limitado) inclui métricas a partir do nível básico, bem como um subconjunto dos dados recolhidos do nível avançado relevante para o Windows Analytics.

#### <a name="windows-81-and-earlier-telemetry"></a>Windows 8.1 e telemetria anterior   
Para obter mais informações, consulte [eventos de telemetria de appraiser do Windows 7, Windows 8 e Windows 8.1 e campos](https://go.microsoft.com/fwlink/?LinkID=822965).

#### <a name="enable-windows-81-and-earlier-internet-explorer-data-collection"></a>Ativar o Windows 8.1 e recolha de dados anterior do Internet Explorer
Em dispositivos com o Windows 8.1 ou anterior, o Internet Explorer pode recolher dados sobre as aplicações web. Estes dados podem permitir que a preparação de atualizações detetar incompatibilidades de aplicativos web que poderiam impedir uma atualização suave para o Windows 10. Ative a recolha de dados do Internet Explorer com base na zona da internet. Para obter mais informações sobre as zonas de internet, consulte [sobre zonas de segurança do URL](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537183\(v=vs.85\)).



## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Utilize a preparação de atualizações para identificar problemas de compatibilidade do Windows 10

Preparação de atualizações permite-lhe analisar a prontidão do dispositivo e a compatibilidade com Windows 10. Essa avaliação permite que as atualizações mais suaves. Depois de ligar o Configuration Manager para o Upgrade Readiness, acessar esses dados de compatibilidade da atualização de cliente diretamente na consola do Configuration Manager. Em seguida, dispositivos de destino para a atualização ou correção a partir da lista de dispositivos.

Para obter mais informações e detalhes sobre como configurar e ligar à preparação, consulte [preparação](/sccm/core/clients/manage/upgrade-readiness).



## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Utilizar a análise do Windows para identificar lacunas nas políticas de proteção de informações do Windows

Pode configurar a versão 1703 do Windows 10 e dispositivos posteriores com um [Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) política (WIP). Dados de diagnóstico que reportam em aplicativos que acederem a dados empresariais no seu ambiente, mas não estão incluídos nas regras de aplicação de política. Os usuários podem precisar desses aplicativos para se manterem produtivos, mas WIP bloqueia o acesso dos utilizadores. Estas informações são úteis para manter as políticas de proteção de informações do Windows no Configuration Manager. 


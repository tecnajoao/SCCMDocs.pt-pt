---
title: Atualizações no ambiente de trabalho Analytics
titleSuffix: Configuration Manager
description: Saiba mais sobre as atualizações de segurança e funcionalidade na análise de ambiente de trabalho.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 1b0ad377b260f106aa859ed9b25ff1ac3e32f49b
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55073376"
---
# <a name="updates-in-desktop-analytics"></a>Atualizações no ambiente de trabalho Analytics 

> [!Note]  
> Estas informações se relaciona com o serviço de pré-visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft faz não oferece quaisquer garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

No portal do Analytics de ambiente de trabalho, ver o estado das atualizações de segurança e funcionalidade. Selecione estes nós no grupo de Monitor do menu principal do ambiente de trabalho de análise. Estes nós dão-lhe informações sobre o estado destas atualizações no seu ambiente. 



## <a name="security-updates"></a>Atualizações de segurança

Para rever o estado atual das atualizações de segurança, selecione **atualizações de segurança** no **Monitor** secção da área de trabalho de análise:

![Nó de atualizações de segurança da área de trabalho de análise](media/security-updates.png)

Esta vista resume *segurança* atualizações para dispositivos que estejam a executar o Windows 10 ou o Office 365 ProPlus. Dispositivos no gráfico de barras são categorizados pelos seguintes etiquetas:

#### <a name="latest"></a>mais recente
Dispositivos estão a executar a atualização de segurança mais recente para essa versão e o canal.

#### <a name="latest-1"></a>Versão mais recente-1
Dispositivos com uma atualização de segurança com uma versão de mais antiga do que a atualização mais recente disponível nesse canal.

#### <a name="older"></a>Mais antiga
Dispositivos estão a executar uma atualização de segurança mais antiga do que 1 da versão mais recente.

#### <a name="not-measured"></a>Não monitorizado
Análise de área de trabalho não tiver avaliado o dispositivo. 

- Para Windows, isso inclui dispositivos que executam o Windows 7 ou Windows 8.1  

- Para o Office, isto inclui dispositivos com uma das seguintes versões:  

    - Canal de Insider ProPlus, do Office 365  

    - Uma versão perpétua do Office que utilizam o Windows installer. Por exemplo, Office 2016, Office 2013 ou Office 2010.  

    - O Office 365 ProPlus num dispositivo que ainda não devolveu dados suficientes para avaliar o estado de segurança  



## <a name="feature-updates"></a>Atualizações de funcionalidade

Para rever o estado atual das atualizações de funcionalidade, selecione **atualizações de funcionalidades** no **Monitor** secção da área de trabalho de análise:

![Nó de atualizações de funcionalidade de análise de ambiente de trabalho](media/feature-updates.png)

Esta vista resume *funcionalidade* atualizações para dispositivos que estejam a executar o Windows 10 ou o Office 365 ProPlus. 

Para obter mais informações sobre pontos finais de serviço, consulte os artigos seguintes: 
- [Folha de fatos de ciclo de vida do Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)  
- [Histórico de atualizações do Office 365 ProPlus](https://docs.microsoft.com/officeupdates/update-history-office365-proplus-by-date)  

Dispositivos no gráfico de barras são categorizados pelos seguintes etiquetas:

#### <a name="in-service"></a>No serviço
Dispositivos estão a executar a atualização mais recente do recurso para essa versão e o canal.  

#### <a name="near-end-of-service"></a>Próximo do final de serviço
Dispositivos estão a executar uma atualização de funcionalidade que está dentro de 90 dias após atingir o final do serviço.

#### <a name="end-of-service"></a>Fim do serviço
Dispositivos estão a executar uma atualização de funcionalidades que passou a data de fim de serviço. Para obter detalhes sobre a fim de datas do serviço, consulte {xlink na seção relevante de UDR_monitoring} |

#### <a name="not-measured"></a>Não monitorizado
Análise de área de trabalho não tiver avaliado o dispositivo. 

- Para Windows, isso inclui dispositivos que executam o Windows 7 ou Windows 8.1  

- Para o Office, isto inclui dispositivos com uma das seguintes versões:  

    - Canal de Insider ProPlus, do Office 365  

    - Uma versão perpétua do Office que utilizam o Windows installer. Por exemplo, Office 2016, Office 2013 ou Office 2010.  

    - O Office 365 ProPlus num dispositivo que ainda não devolveu dados suficientes para avaliar o estado de segurança  



## <a name="next-steps"></a>Passos seguintes

- [Saiba mais sobre os recursos de análise de ambiente de trabalho](/sccm/desktop-analytics/about-assets): dispositivos, aplicações, aplicações do Office, os suplementos do Office e macros do Office  

- [Saiba mais sobre os planos de implantação](/sccm/desktop-analytics/about-deployment-plans)  


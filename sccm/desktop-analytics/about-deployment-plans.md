---
title: Planos de implantação no ambiente de trabalho de análise
titleSuffix: Configuration Manager
description: Saiba mais sobre os planos de implantação no ambiente de trabalho de análise.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce726ffa0dfc8a46bd0891e50ff087ad4931d901
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140344"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Sobre os planos de implantação no ambiente de trabalho de análise 

> [!Note]  
> Estas informações se relaciona com o serviço de pré-visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft faz não oferece quaisquer garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Ambiente de trabalho Analytics recolhe e analisa dados de controladores, aplicações e dispositivos na sua organização. Com base na sua entrada e essa análise, pode utilizar o serviço para criar planos de implantação do Windows 10 e Office 365 ProPlus. Planos de implantação têm as seguintes funcionalidades:  

- Recomende automaticamente os dispositivos a incluir na pilotos  

- Identificar problemas de compatibilidade e atenuações de Sugerir  

- Avaliar o estado de funcionamento da implementação antes, durante e após as atualizações  

- Acompanhar o progresso da implementação  


Como parte do seu plano de implementação, efetue as seguintes ações:  

 - Defina que produtos e versões que pretende implementar: Windows 10, o Office 365 ProPlus, ou ambos  

 - Escolha os grupos de dispositivos aos quais pretende implementar  

 - Criar regras de preparação para a implementação  

 - Definir a importância das suas aplicações e suplementos do Office  

 - Selecione dispositivos pilotos com base nas recomendações automática  

 - Decidir como corrigir problemas com aplicações e suplementos Office com base nas recomendações da análise de ambiente de trabalho  


Análise de área de trabalho atualiza os dados de plano de implementação diariamente. As alterações que fizer podem não aparecer durante 24 horas. Essas alterações incluem a atribuição de importância a uma aplicação, ou ao escolher um dispositivo para incluir um piloto.  

Se ligar a análise de ambiente de trabalho para o Configuration Manager, selecione as coleções nos planos de implementação. Em seguida, esta integração permite-lhe implementar o Windows ou do Office para uma coleção com base nos dados de análise de ambiente de trabalho. 

Se não utilizar o Configuration Manager, pode criar grupos no Log Analytics. Para obter mais informações, consulte [pesquisas de registos de grupos de computadores no Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-computer-groups). 



## <a name="readiness-rules"></a>Regras de preparação

As seguintes regras de preparação estão disponíveis nos planos de implantação:

- Se os dispositivos recebem automaticamente drivers do Windows Update. Se os dispositivos recebem as atualizações de driver do Windows Update, em seguida, quaisquer problemas de driver identificados como parte da avaliação de preparação são marcados automaticamente como **pronto**.  

- Baixa instalar o limiar de contagem para as suas aplicações do Windows. Se uma aplicação é instalada numa porcentagem maior de computadores a este limiar, o plano de implantação marca a aplicação como **Noteworthy**. Esta etiqueta significa que pode decidir como é importante testar durante a fase piloto.  

- Atualização do Office 365 ProPlus de 32 bits para 64 bits em dispositivos que tenham uma versão de 64 bits do Windows. Este comportamento é a predefinição.  

- Ao atualizar a partir de uma versão mais antiga do Office, deixe as aplicações do Office mais antigas, mesmo que essas aplicações não existem na versão mais recente do Office. Este comportamento não está por predefinição.  

- Baixa instalar o limiar de contagem de seus suplementos Office. O limiar predefinido é `2%`. Suplementos abaixo deste limiar são definidos automaticamente como *baixa instalar contagem*. Análise de área de trabalho não será validado esses suplementos durante o piloto. 

    Se estiver instalado um suplemento numa porcentagem maior de computadores a este limiar, o plano de implantação marca o suplemento como *Noteworthy*. Em seguida, pode decidir sua importância para testar durante a fase piloto.   



## <a name="importance"></a>Importância

Como parte do plano de implantação, defina o *importância* das aplicações e suplementos do Office. Análise de área de trabalho Deteta estas aplicações como instalado nos dispositivos de destino. Esta definição ajuda a determinar quais os dispositivos que inclui na fase piloto da implantação de análise de ambiente de trabalho. 

Se uma aplicação ou um suplemento estiver instalado em menos de 2% dos dispositivos visados, ele é marcado **baixa instalar contagem**. Dois por cento é o valor predefinido. Pode ajustar o limiar em que as definições de preparação de 0% a 10%. Análise de área de trabalho marca automaticamente estas aplicações e suplementos como **pronto para atualizar**.  

Para aplicações e suplementos, escolha uma importância de **crítico**, **importante**, ou **não importante**. Se marcar um como críticos ou importantes, análise de ambiente de trabalho inclui na implantação piloto alguns dispositivos com esse suplemento ou aplicação. O serviço inclui, no projeto piloto, mais instâncias de um suplemento ou aplicações críticas. Se marca uma aplicação ou suplemento como não importante, análise de ambiente de trabalho define automaticamente-lo **pronto para atualizar**.



## <a name="pilot-devices"></a>Dispositivos pilotos

Análise de área de trabalho combina as informações de importância com as definições globais do pilotos. Em seguida, cria uma recomendação para o qual os dispositivos devem ser parte da implementação do piloto. A implementação piloto recomendada inclui dispositivos com diferentes configurações de hardware e uma ou mais instâncias de todas as aplicações críticas e importantes. Se uma aplicação está marcada como crítica, o serviço recomenda mais dispositivos com essa aplicação no projeto piloto.



## <a name="deployment-plans-in-configuration-manager"></a>Planos de implementação no Configuration Manager

Depois de criar um plano de implantação, utilize o Configuration Manager para implementar os produtos. Uma vez iniciada a implementação, análise de área de trabalho monitoriza a implementação com base nas definições no plano.

<!--more on deployment plans in SCCM-->

<!-- test comment-->

## <a name="next-steps"></a>Passos seguintes

- [Saiba mais sobre os recursos de análise de ambiente de trabalho](/sccm/desktop-analytics/about-assets): dispositivos, aplicações, aplicações do Office, os suplementos do Office e macros do Office  

- [Saiba mais sobre as atualizações de segurança e funcionalidade](/sccm/desktop-analytics/about-updates)  

- [Criar um plano de implantação](/sccm/desktop-analytics/create-deployment-plans)  


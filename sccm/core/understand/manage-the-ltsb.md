---
title: Gerir o LTSB | Microsoft Docs
description: "Diferenças de gestão para o LTSB do System Center Configuration Manager."
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9c6f349ead906532a7a58df74609de976769e251
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>Gerir o Long Term Servicing Branch do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo de manutenção longo prazo)*

Quando utiliza a longo prazo Servicing Branch (LTSB) do System Center Configuration Manager, o seguinte pode ajudar a compreender as alterações importantes que afetam a forma como gerir a sua infraestrutura.

Porque o LTSB é equivalente ao ramo atual versão 1606 (com algumas exceções, como a integração do Intune e as funcionalidades relacionadas com a nuvem), a maioria das tarefas que utiliza para o planeamento, implementação, configuração e gestão diária são os mesmos.

Por exemplo, o LTSB suporta o mesmo número de sites, tipos de site, os clientes e infraestrutura geral como ramo atual. Por conseguinte, utilize a documentação de orientação encontrada no site e da hierarquia tópicos de planeamento e design para o ramo atual. Da mesma forma, para funcionalidades com o LTSB que são suportadas por ambos os ramos, como atualizações de Software ou a implementação do sistema operativo, utilize as orientações encontrada dessas secções da documentação Current Branch com os avisos de não ter acesso a alterações da funcionalidade introduzida após a versão 1606 da filial atual.

As secções seguintes fornecem informações sobre gerir as tarefas que não são semelhantes.

## <a name="updates-and-servicing"></a>Atualizações e manutenção
Apenas as atualizações de segurança críticas são disponibilizadas como atualizações na consola no LTSB.  

Informações sobre atualizações regulares para as versões subsequentes do Current Branch são visíveis na consola, mas não são disponibilizados para o LTSB. Estes não são transferidas e não podem ser instalados.

Para suportar atualizações na consola para correções de segurança críticas, um site LTSB requer a utilização de [o ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point). Pode configurar esta função de sistema de sites no modo offline ou online, como é feito para o ramo atual. O LTSB recolhe e envia os mesmos dados de telemetria e de utilização que o ramo atual.

O LTSB suporta a utilização de instalador de correções e a ferramenta de registo de atualização, conforme documentado para o ramo atual.

Para obter informações gerais sobre as atualizações e manutenção, consulte [atualizações do Configuration Manager](/sccm/core/servers/manage/updates).


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Alterações de expansão do site e CD. Pasta mais recente
Quando executar o LTSB e está a expandir um site primário autónomo, instalando um novo site de administração central, tem de utilizar o programa de configuração e os ficheiros de origem do suporte de dados de linha de base do versão 1606. Para o ramo atual, executar a configuração e utilizar ficheiros de origem a partir do CD. Pasta mais recente.

Embora não executar a configuração de expansão do site a partir do CD. Pasta mais recente, continua a utilizar o CD. Pasta mais recente para a recuperação de site e para instalar um novo site primário subordinado quando o primeiro site LTSB era um site de administração central.

Para obter mais informações sobre a expansão do site, consulte [expandir um site primário autónomo](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site). Para obter mais informações sobre o CD. Pasta mais recente, consulte [o CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder).


## <a name="recovery"></a>Recuperação
Quando recupera um site, tem de restaurar o site ou a base de dados do site para o ramo original. Não é possível recuperar uma base de dados do site do ramo atual para uma instalação de LTSB, ou vice versa.

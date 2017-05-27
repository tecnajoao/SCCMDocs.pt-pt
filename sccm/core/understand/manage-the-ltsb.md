---
title: Gerir o LTSB | Documentos do Microsoft
description: "Diferenças de gestão para o LTSB do System Center Configuration Manager."
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 31819a1df4e63e1114682490a9b3c3b4e5c99cfa
ms.openlocfilehash: 9c6f349ead906532a7a58df74609de976769e251
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>Gerir a longo prazo manutenção secundário do Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramo longa duração de manutenção)*

Quando utiliza a longo prazo manutenção ramo (LTSB) do System Center Configuration Manager, o seguinte pode ajudar a compreender alterações importantes que afetam a forma como gerir a sua infraestrutura.

Uma vez que o LTSB é equivalente à versão do ramo atual 1606 (com algumas exceções como integração do Intune e funcionalidades relacionadas com a nuvem), a maioria das tarefas a que utilizar para o planeamento, implementação, configuração e na gestão diária são os mesmos.

Por exemplo, o LTSB suporta o mesmo número de sites, tipos de site, os clientes e infraestrutura geral como o ramo atual. Por conseguinte, utilize as orientações encontradas no site e da hierarquia tópicos de planeamento e design para o ramo atual. Do mesmo modo, para funcionalidades com o LTSB que são suportadas por ambos os ramos, como atualizações de Software ou a implementação do sistema operativo, utilize as orientações encontrada dessas secções da documentação ramo atual com as advertências de não ter acesso à funcionalidade alterações introduzidas após versão 1606 do mesmo atual.

As secções seguintes fornecem informações sobre gerir as tarefas que não são semelhantes.

## <a name="updates-and-servicing"></a>As atualizações e manutenção
Apenas as atualizações de segurança importantes são disponibilizadas como na consola atualizações no LTSB.  

Informações sobre atualizações regulares do versões de ramo atual subsequentes são visíveis na consola, mas não ficam disponíveis para o LTSB. Estes não são transferidas e não podem ser instalados.

Para suportar as atualizações na consola de correções de segurança importantes, um site LTSB requer a utilização de [o ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point). Pode configurar esta função do sistema de sites no modo offline ou online, como é feito para o ramo atual. O LTSB recolhe e envia os mesmos dados de telemetria e a utilização, como o ramo atual.

O LTSB suporta a utilização do instalador de correção e a ferramenta de registo de atualização, conforme documentado para o ramo atual.

Para obter informações gerais sobre as atualizações e manutenção, consulte o artigo [atualizações para o Configuration Manager](/sccm/core/servers/manage/updates).


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Alterações para a expansão do site e o CD. Pasta mais recente
Quando executar o LTSB e está a expandir um site primário autónomo ao instalar um novo site de administração central, tem de utilizar o programa de configuração e os ficheiros de origem a partir do suporte de dados de linha de base de 1606 de versão. Para o ramo atual, execute a configuração e utilizar ficheiros de origem a partir do CD. Pasta mais recente.

Apesar de não executar a configuração de expansão do site a partir do CD. Pasta mais recente, continuar a utilizar o CD. Pasta mais recente para a recuperação de site e para instalar um novo site primário subordinado quando o primeiro site LTSB foi um site de administração central.

Para obter mais informações sobre a expansão do site, consulte o artigo [expandir um site primário autónomo](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site). Para mais informações sobre o CD. Pasta mais recente, consulte o artigo [o CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder).


## <a name="recovery"></a>Recuperação
Quando recupera um site, tem de restaurar o site ou a base de dados do site para o ramo original. Não é possível recuperar uma base de dados do site secundário atual para uma instalação LTSB ou vice versa.


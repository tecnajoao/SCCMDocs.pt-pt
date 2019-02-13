---
title: Gerir o LTSB
titleSuffix: Configuration Manager
description: Diferenças de gestão para o LTSB do System Center Configuration Manager.
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 34e0ae19fc7bb3680a148fd5e4ac52feb294963f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121316"
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>Gerir a longo prazo Servicing Branch do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Long term Servicing Branch)*

Quando utiliza o term Servicing Branch (LTSB) do System Center Configuration Manager, o seguinte pode ajudar a compreender as alterações importantes que afetam a forma como gerir a sua infraestrutura.

Como o LTSB é equivalente à versão 1606 do ramo atual (com algumas exceções, como a integração do Intune e as funcionalidades relacionadas com a cloud), a maioria das tarefas que utiliza para planejamento, implantação, configuração e gerenciamento diário são os mesmos.

Por exemplo, o LTSB suporta o mesmo número de sites, tipos de site, os clientes e a infraestrutura geral de como o ramo atual. Por conseguinte, utilizar a documentação de orientação encontrada no site e da hierarquia, tópicos de planeamento e conceção para o ramo atual. Da mesma forma, para as funcionalidades com o LTSB que são suportadas pelas duas ramificações, como atualizações de Software ou a implementação do sistema operativo, utilize as orientações encontrada dessas secções da documentação do ramo atual com os avisos de não ter acesso às alterações de funcionalidade introduziu depois da versão 1606 do ramo atual.

As secções seguintes fornecem informações sobre gerir as tarefas que não são semelhantes.

## <a name="updates-and-servicing"></a>As atualizações e manutenção
Apenas as atualizações críticas de segurança estão disponíveis como atualizações na consola no LTSB.  

Informações sobre atualizações regulares para as versões subsequentes do ramo atual são visíveis na consola, mas não são disponibilizados para o LTSB. Eles não são transferidos e não podem ser instalados.

Para suportar atualizações na consola para correções de segurança críticas, um site LTSB requer a utilização de [o ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point). Pode configurar esta função de sistema de sites no modo offline ou online, como é feito para o ramo atual. O LTSB recolhe e envia os mesmos dados de telemetria e de utilização, como o ramo atual.

O LTSB suporta a utilização de instalador de correções e a ferramenta de registo de atualização, conforme documentado para o ramo atual.

Para obter informações gerais sobre as atualizações e manutenção, consulte [atualizações do Configuration Manager](/sccm/core/servers/manage/updates).


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Alterações à expansão do site e do CD. Pasta mais recente
Quando executa o LTSB e expande um site primário autónomo, instalando um novo site de administração central, tem de utilizar o programa de configuração e os ficheiros de origem do suporte de dados de linha de base do versão 1606. Para o ramo atual, execute a configuração e utilizar ficheiros de origem a partir do CD. Pasta mais recente.

Embora não executar a configuração para expansão do site a partir do CD. Pasta mais recente, continua a utilizar o CD. Pasta mais recente para o site recovery e para instalar um novo site primário subordinado quando o primeiro site LTSB era um site de administração central.

Para obter mais informações sobre a expansão do site, consulte [expandir um site primário autónomo](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site). Para obter mais informações sobre o CD. Pasta mais recente, consulte [The CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder).


## <a name="recovery"></a>Recuperação
Quando recupera um site, tem de restaurar o site ou a base de dados do site para o seu ramo original. Não é possível recuperar uma base de dados do site do ramo atual para uma instalação de LTSB, ou vice versa.

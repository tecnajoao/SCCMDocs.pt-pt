---
title: Anexar na cloud com a cogestão
titleSuffix: Configuration Manager
description: Cogestão oferece valor imediato se a ativar.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d878443-90e7-46e4-9cd3-99e2a19b2ad0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b6e58db8e593278258c8583c2de7d4edecec7e08
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54251177"
---
# <a name="cloud-attach-with-co-management"></a>Anexar na cloud com a cogestão

![Faixa da série blastoff](media/blastoff-banner.png)

Cogestão adiciona novas funcionalidades à sua implementação do Configuration Manager existente, sem alterar a forma como já trabalha. Quando ativar a cogestão, começa imediatamente beneficie da cloud. Pode aplicar esse valor à sua infraestrutura de gestão existente e processos.

Nesta série de início rápido de cogestão, veja como pode promover rapidamente novo valor de gestão. Cogestão baseia-se para criar recursos e ferramentas que pode utilizar neste momento.


No vídeo seguinte, a Microsoft vice-presidente Brad Anderson apresenta esta série de cogestão:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Cloud-Connecting-with-Co-Management/player]


| Valor imediato | Introdução |
|-----------------|-----------------|
| - [Acesso condicional](#bkmk_ca)<br> - [Ações remotas do Intune](#bkmk_remote)<br> - [Estado de funcionamento do cliente](#bkmk_client-health)<br> - [Azure AD híbrido](#bkmk_hybrid-aad)<br> - [Windows Autopilot](#bkmk_autopilot) | - [Caminhos de cogestão](#bkmk_paths)<br> - [Configurar o Azure AD híbrido](#bkmk_setup-hybrid-aad)<br> - [Atualizar para o Windows 10](#bkmk_upgrade-win10)<br> - [Migrar da MDM híbrida](#bkmk_migrate-hybrid-mdm)<br> - [Obtenha ajuda de FastTrack](#bkmk_fasttrack) | 



## <a name="immediate-value"></a>Valor imediato

| | | |
|-|-|-|
| <a name="bkmk_ca"></a>**Acesso condicional com a conformidade do dispositivo** | Controlar o acesso de utilizador aos recursos empresariais com base nas regras de conformidade do Intune | [![Miniatura de vídeo de acesso condicional](media/thumbnail-conditional-access.png)](/sccm/comanage/quickstart-conditional-access) |
| <a name="bkmk_remote"></a>**Ações remotas do Intune** | Execute ações remotas do Intune para dispositivos cogeridos. Por exemplo, apagar e repor um dispositivo e a manter a inscrição e conta | [![Miniatura de vídeo de ações remota](media/thumbnail-remote-action.png)](/sccm/comanage/quickstart-remote-actions) |
| <a name="bkmk_client-health"></a>**Estado de funcionamento do cliente do Configuration Manager** | Manter a visibilidade do Estado de funcionamento de cliente do Configuration Manager do Intune no portal do Azure | [![Miniatura de vídeo da estado de funcionamento do cliente](media/thumbnail-client-health.png)](/sccm/comanage/quickstart-client-health) |
| <a name="bkmk_hybrid-aad"></a>**Azure Active Directory (Azure AD)** | Com o Azure AD pode tirar partido do maior produtividade para os utilizadores e a segurança para os seus recursos em ambientes de cloud e no local | [![Miniatura de vídeo do Azure AD híbrido](media/thumbnail-azure-ad.png)](/sccm/comanage/quickstart-hybrid-aad) |
| <a name="bkmk_autopilot"></a>**Windows Autopilot** | Reduza o tempo, recursos e complexidade associada à implementação, a gerir e a extinguir ou a Reciclagem de dispositivos. Autopilot também cria uma melhor experiência para os utilizadores finais. | [![Miniatura de vídeo do Windows Autopilot](media/thumbnail-autopilot.png)](/sccm/comanage/quickstart-autopilot) |



## <a name="getting-started"></a>Introdução

Se pretender ativar a cogestão, comece por aqui para desbloquear as preocupações técnicas, que pode ter.

| | | |
|-|-|-|
| <a name="bkmk_paths"></a>**Caminhos de cogestão** | Existem duas formas principais para configurar cogestão e é importante compreender os pré-requisitos para cada caminho.  Cada caminho requer alguma combinação do Azure AD, cliente do ConfigMgr, o Intune e o Windows. | [![Miniatura de slide de caminhos de cogestão](media/thumbnail-paths.png)](/sccm/comanage/quickstart-paths) |
| <a name="bkmk_setup-hybrid-aad"></a>**Configurar o Azure AD híbrido** | Se o seu ambiente tem atualmente a dispositivos associados a domínios do Windows 10, configurar híbrida do Azure AD antes de poder ativar a cogestão | [![Miniatura do Azure AD híbrido configurar vídeo](media/thumbnail-setup-azure-ad.png)](/sccm/comanage/quickstart-setup-hybrid-aad) |
| <a name="bkmk_upgrade-win10"></a>**Atualizar para o Windows 10** | Windows 10 versão 1709 ou posterior é necessária para a cogestão | [![Miniatura de vídeo atualização do Windows 10](media/thumbnail-upgrade-win10.png)](/sccm/comanage/quickstart-upgrade-win10) |
| <a name="bkmk_migrate-hybrid-mdm"></a>**Migrar da MDM híbrida** | Hybrid MDM (Intune integrado com o Configuration Manager) foi preterido. É necessário para a cogestão o Intune autónomo. | [![Migrar de miniatura de vídeo MDM híbrida](media/thumbnail-migrate-hybrid-mdm.png)](/sccm/comanage/quickstart-migrate-hybrid-mdm) |
| <a name="bkmk_fasttrack"></a>**Obtenha ajuda de FastTrack** | A organização de FastTrack é um grupo grande de engenheiros da Microsoft que se especializam nos ajudar a todos os tipos de organizações implementar aplicações do Microsoft 365, incluindo a configuração de cogestão. | [![Miniatura de vídeo do FastTrack](media/thumbnail-fasttrack.png)](/sccm/comanage/quickstart-fasttrack) |


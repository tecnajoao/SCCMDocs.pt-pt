---
title: Atualizar o Windows 10
titleSuffix: Configuration Manager
description: Atualizar dispositivos para Windows 10 versão 1709 ou posterior, que é necessário para a cogestão
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ca0e395c3f85dc7cff0be36b234a978b34206df0
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54250983"
---
# <a name="upgrade-windows-10-for-co-management"></a>Atualizar o Windows 10 para a cogestão

À medida que trabalha em direção à integração de sua organização para a cogestão, obter atual é uma barreira significativa para alguns clientes. Necessita de cogestão [Windows 10 versão 1709](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709) ou posterior. Depois de atualizar o Windows e configurar a inscrição automática, os clientes são automaticamente inscritos para cogestão.

No vídeo seguinte, o gerente de programas sênior Rob Iorque e marketing Ainley Locky do Gestor de produtos, discutem e atualizar para o Windows 10 para a cogestão de demonstração:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>Por que atualizar?

Entre outros aprimoramentos de plataforma, o Windows 10 versão 1709 ou posterior suporta a inscrição automática. Esse comportamento faz com que um dispositivo automaticamente se inscreverem no Intune quando associado a um Azure Active Directory (Azure AD). 

Para obter mais informações, consulte [inscrição automática de ativar o Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment).


## <a name="how-to-do-it"></a>Como fazê-lo

Aqui estão algumas dicas que aprendemos de ajudar milhares de clientes Obtenha rapidamente atual:

- Utilize as implementações faseadas para implementar esta atualização para as pessoas certas na direita vezes. Para obter mais informações, consulte [criar implementações faseadas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).  

- Utilize a colocação em pré-cache para reduzir os tempos de espera de utilizador. Para obter mais informações, consulte [configurar pré-armazenar conteúdo em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

- Utilize o modelo de sequência de tarefas de atualização no local padrão. Em seguida, configure os passos para pré e pós-atualização e quaisquer ações de falha. Para obter mais informações, consulte [recomendado passos de sequência de tarefas de pós-processamento](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-for-post-processing).  

- Se o ambiente tiver uma força de trabalho altamente móvel, o Configuration Manager suporta atualização no local através do gateway de gestão da cloud (CMG). Esta funcionalidade permite-lhe atualizar os clientes do Windows 10, quando eles são baseados na internet. Para obter mais informações sobre o CMG, consulte [ ](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

- Oferecem uma participação ativa na cogestão para os usuários que desejam ser pioneiros. Essa abordagem acelera a adoção inicial. Ao identificar essas pessoas com antecedência, pode tornar-se de que boa cobertura no início de uma implementação. Também receberá validação e comentários dos utilizadores que são Feliz de alteração e interessados em versões mais freqüentes. Programas de pioneiro na adoção antecipada geram interesse em novas tecnologias e crescem em tamanho ao longo do tempo.  


## <a name="case-studies"></a>Estudos de caso

Microsoft IT implementar o Windows 10 aos utilizadores distribuídos 96,000 na Microsoft. A implementação incluído usuários remotos e utilizadores na rede empresarial. A implementação foi concluída em nove semanas. Para obter mais informações sobre a experiência deles, consulte [Implantando o Windows 10 na Microsoft, como uma atualização in-loco](https://www.microsoft.com/download/details.aspx?id=50377).  

Um fabricante de software Européia grandes com êxito utiliza um grupo de pioneiro na adoção antecipada. Depois de testes iniciais e os grupos de testes de, aproximadamente 2000 empregados recebem a primeira atualização, atualizações e software. Esse grupo inclui a equipe de TI e optar por voluntários. Este nível de interação com os seus utilizadores dá a eles um maior nível de confiança ao testar e mais credibilidade quando começam a distribuições em massa.



## <a name="contact-fasttrack"></a>Entre em contato com FastTrack

Se precisar de assistência com a atualização do Windows 10 em qualquer ponto do processo, aceda a [Microsoft FastTrack](https://Microsoft.com/FastTrack/), inicie sessão e pedir assistência. 

Para obter mais informações, consulte [Obtenha ajuda de FastTrack](/sccm/comanage/quickstart-fasttrack). 


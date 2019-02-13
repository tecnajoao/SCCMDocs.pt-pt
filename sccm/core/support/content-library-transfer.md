---
title: Ferramenta de transferência da biblioteca de conteúdos
titleSuffix: Configuration Manager
description: Utilize a ferramenta de transferência da biblioteca de conteúdos para a transferência de conteúdo de uma unidade de disco para outro num ponto de distribuição do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f7375a62349aba30ee239aa34fa594650f5a844
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121986"
---
# <a name="content-library-transfer-tool"></a>Ferramenta de transferência da biblioteca de conteúdos

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A ferramenta de transferência da biblioteca de conteúdos é um da [ferramentas do Configuration Manager](/sccm/core/support/tools). Transferir conteúdo de uma unidade de disco para outro. A ferramenta foi criada para ser executado em sistemas de sites do ponto de distribuição. Ele oferece suporte a pontos de distribuição colocalizados com um site ou sistemas de sites remotos.  

A ferramenta é útil para o cenário quando a unidade de disco que aloja a biblioteca de conteúdos ficar cheio. Primeiro, adicione ou identificar outro disco rígido com espaço suficiente para alojar a biblioteca de conteúdos. Em seguida, utilize **ContentLibraryTransfer.exe** para transferir conteúdo a partir do disco rígido de manchas antigo para o novo, vazio unidade.
 
Quando a transferência estiver concluída, o conteúdo está acessível para computadores cliente a partir da nova localização.



## <a name="usage"></a>Utilização 

Execute **ContentLibraryTransfer.exe** como um utilizador com permissões administrativas no ponto de distribuição. 

#### <a name="syntax"></a>Sintaxe 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>Exemplo
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>Limitações

- Execute a ferramenta localmente no ponto de distribuição. Não é possível executá-lo a partir de um computador remoto.  

- Utilize apenas quando os clientes não são aceder ativamente ao ponto de distribuição. Se executar a ferramenta, embora os clientes estão a aceder ao conteúdo, a biblioteca de conteúdos na unidade de destino pode ter dados incompletos. A transferência de dados poderá falhar totalmente que leva a uma biblioteca de conteúdos não utilizável.  

- Não distribua o conteúdo para o ponto de distribuição quando executar a ferramenta. Se executar a ferramenta, enquanto o conteúdo está a ser escrito para o ponto de distribuição, a biblioteca de conteúdos na unidade de destino pode ter dados incompletos. A transferência de dados poderá falhar totalmente que leva a uma biblioteca de conteúdos não utilizável.



## <a name="see-also"></a>Consulte também

- [Conceitos fundamentais da gestão de conteúdos](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [A biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/the-content-library)

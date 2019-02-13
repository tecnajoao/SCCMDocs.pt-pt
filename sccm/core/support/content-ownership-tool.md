---
title: Ferramenta de Propriedade do Conteúdo
titleSuffix: Configuration Manager
description: Utilize a ferramenta de propriedade de conteúdo para alterar a propriedade de órfãos pacotes no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 753d2681-ea72-4f47-94d1-ac10188d9d5b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3ba864914afb6794d460b81f5df346902b8ab0ce
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121888"
---
# <a name="content-ownership-tool"></a>Ferramenta de Propriedade do Conteúdo

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Ferramenta de propriedade do conteúdo é um da [ferramentas do Configuration Manager](/sccm/core/support/tools). Ele altera a propriedade de órfãos pacotes no Configuration Manager. Pacotes órfãos não tem um servidor de site proprietário. Pacotes podem tornar-se órfã ao remover o servidor do site, enquanto ainda estiver detinham por este servidor de site.

Execute a ferramenta de propriedade do conteúdo em qualquer servidor de site na hierarquia do Configuration Manager. Inicie sessão como um utilizador administrativo com permissões suficientes do pacote.  

> [!Tip]  
> Uso **ContentLibraryCleanup.exe** na `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` para *remover* órfãos conteúdo a partir de um ponto de distribuição. Para obter mais informações, consulte [ferramenta de limpeza da biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool).  



## <a name="features"></a>Funcionalidades

- Exibir todos os pacotes órfãos  

- Exibir todos os pacotes, mesmo que eles não estiverem órfãos  

- Ver o estado da ligação a um site  

- Filtro de pacotes por nome, o código do site ou o tipo de pacote  

- Ordenar por qualquer coluna exibida  

- Alterar a atribuição de um ou mais pacotes com uma única ação  

- Ver progresso da atividade de transferência de propriedade  



## <a name="usage"></a>Utilização

Execute **ContentOwnershipTool.exe** para iniciar a ferramenta. Não são necessárias permissões de administrador local no computador para executar a ferramenta.

Não há nenhum parâmetro da linha de comandos.

> [!Important]   
> Essa ferramenta altera a propriedade de um pacote de órfão. O pacote propriamente dito não move-se de que ele é armazenado no ponto de distribuição. Esta alteração de propriedade não fazer com que o pacote de atualização em pontos de distribuição. Também não causa clientes reavaliar a política para implementação do pacote. Depois da propriedade for alterada, certifique-se de que o novo servidor de site pode acessar os arquivos de origem. Deve ter pelo menos **leitura** permissões para os ficheiros de origem de cada pacote. 



## <a name="see-also"></a>Consulte também

- [Conceitos fundamentais da gestão de conteúdos](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [A biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/the-content-library)

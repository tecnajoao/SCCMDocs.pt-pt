---
title: Preparar a implementação do SO
titleSuffix: Configuration Manager
description: Saiba mais sobre como preparar implementações de sistemas operativos no Configuration Manager
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8d27e5ac-4f19-4b3d-85c7-fa34eb5d5e7e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e303a7363e0641210cc7c6e436546d864fe0571
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838723"
---
# <a name="prepare-for-os-deployment-in-configuration-manager"></a>Preparar para a implementação do sistema operacional no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Há várias coisas que deve fazer no Configuration Manager antes de poder implementar sistemas operativos. Utilize os artigos seguintes para preparar a implementação do sistema operacional:  

-   [Gerir imagens de arranque](manage-boot-images.md)  

-   [Gerir imagens do SO](manage-operating-system-images.md)  

-   [Gerir pacotes de atualização do SO](manage-operating-system-upgrade-packages.md)  

-   [Gerir controladores](manage-drivers.md)  

-   [Gerir o estado do utilizador](manage-user-state.md)  

-   [Preparar implementações de computadores desconhecidos](prepare-for-unknown-computer-deployments.md)  

-   [Associar utilizadores a um computador de destino](associate-users-with-a-destination-computer.md)  



### <a name="os-image-size"></a>Tamanho da imagem de SO  

Imagens do sistema operacional são grandes de tamanho. Por exemplo, o tamanho da imagem do Windows 7 é 3 GB ou mais. O tamanho da imagem e o número de computadores nos quais implementou simultaneamente o sistema operacional afeta o desempenho de rede e a largura de banda disponível. Certifique-se testar o desempenho de rede. Teste o impacto melhor mede o efeito que a implementação de imagem poderá ter e o tempo necessário para concluir a implementação. Atividades do Configuration Manager que afetam o desempenho de rede incluem a distribuição da imagem para um ponto de distribuição, a distribuição da imagem de um site para outro e a transferência da imagem para o cliente.  

Além disso, certifique-se de que planeia para o espaço de armazenamento em disco suficiente nos pontos de distribuição que alojam as imagens de sistema operacional.  

Para obter mais informações, consulte [adicionais de considerações sobre planeamento para pontos de distribuição](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_AdditionalPlanning).


### <a name="client-cache-size"></a>Tamanho da cache do cliente  

Quando os clientes do Configuration Manager transferirem conteúdo, eles automaticamente usar Background Intelligent Transfer Service (BITS), se estiver disponível. Quando implementa uma sequência de tarefas que instala um sistema operacional, pode definir uma opção na implementação, de modo a que os clientes do Configuration Manager transferem a imagem completa para uma cache local antes da sequência de tarefas é executado.  

Quando um cliente do Configuration Manager tem de transferir uma imagem de SO, mas não existir espaço suficiente na cache, o cliente pode limpar o espaço na respetiva cache. Ele verifica os outros pacotes na cache para determinar se a eliminação de alguns os pacotes antigos permitiria libertar espaço em disco suficiente para acomodar a imagem. Se a eliminação de pacotes não libertar espaço suficiente, o cliente não transferirá a imagem e a implementação falhará. Esse comportamento pode ocorrer se a cache tiver um pacote de grandes dimensões que configurar para se manter na cache. Se a eliminação de pacotes antigos libertar espaço suficiente de disco na cache, o cliente eliminá-los-á e transferirá em seguida a imagem para a cache.  

O tamanho da cache padrão em clientes do Configuration Manager pode não ser suficientemente grande para a maioria das implementações de imagem do sistema operacional. Se quiser transferir a imagem completa para a cache do cliente, ajuste o tamanho de cache do cliente nos computadores de destino para acomodar o tamanho da imagem que estiver a implementar.  

Para obter mais informações, consulte [configurar a cache do cliente](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache).  



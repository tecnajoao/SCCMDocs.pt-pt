---
title: Cenários para implementar sistemas operativos empresariais
titleSuffix: Configuration Manager
description: Saiba mais sobre os vários cenários para implementar sistemas de operativos empresariais com o System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92b968a8dae63d15e087e098452b56b0397c7b78
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137580"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-system-center-configuration-manager"></a>Cenários para implementar sistemas operativos empresariais com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Após o sistema operativo cenários de implementação estão disponíveis no System Center Configuration Manager:  

-   [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md): Este cenário atualiza o sistema operativo nos computadores que executam o Windows 7, Windows 8, Windows 8.1 ou Windows 10. O processo de atualização mantém as aplicações, definições e dados do utilizador no computador. Não existem dependências externas, como o Windows ADK, e este processo é mais rápido e mais resiliente do que as implementações tradicionais do sistema operativo.  

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md): Este cenário particiona e formata (limpa) um computador existente e instala um novo sistema operativo no computador. É possível migrar as definições e dados do utilizador após a instalação do sistema operativo.  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md): Este cenário instala um sistema operativo num novo computador. Esta é uma instalação de raiz do sistema operativo e não inclui definições ou migração de dados do utilizador.  

-   [Substituir um computador existente e transferir definições](replace-an-existing-computer-and-transfer-settings.md): Este cenário instala um sistema operativo num novo computador. Opcionalmente, é possível migrar as definições e dados do utilizador do computador antigo para o novo computador.  

## <a name="things-to-consider-before-you-deploy-operating-system-images"></a>Aspetos a considerar antes de implementar imagens do sistema operativo  
 Existem alguns aspetos a considerar antes de implementar um sistema operativo.  

### <a name="operating-system-image-size"></a>Tamanho da imagem do sistema operativo  
 O tamanho de uma imagem do sistema operativo pode ser bastante grande. Por exemplo, o tamanho da imagem do Windows 7 é igual ou superior a 3 gigabytes (GB). O tamanho da imagem e o número de computadores em que implementa simultaneamente o sistema operativo afeta o desempenho da rede e a largura de banda disponível. Certifique-se de que testa o desempenho da rede para avaliar melhor o efeito que a implementação da imagem poderá ter, e o tempo que demora a concluir a implementação. Atividades do Configuration Manager que afetam o desempenho de rede incluem a distribuição da imagem para um ponto de distribuição, a distribuição da imagem de um site para outro e a transferência da imagem para o cliente do Configuration Manager.  

 Certifique-se também de que planeia espaço de armazenamento em disco suficiente nos pontos de distribuição que alojam as imagens do sistema operativo.  

### <a name="client-cache-size"></a>Tamanho da cache do cliente  
 Quando os clientes do Configuration Manager transferirem conteúdo, eles automaticamente utilizarem o serviço de transferência inteligente em segundo plano (BITS) se estiver disponível. Quando implementa uma sequência de tarefas que instala um sistema operativo, pode definir uma opção na implementação, de modo a que os clientes do Configuration Manager transferem a imagem completa para uma cache local antes da sequência de tarefas é executado.  

 Em geral, quando um cliente do Configuration Manager tem de transferir uma imagem do sistema operativo (ou qualquer outro pacote), mas não existe espaço suficiente na cache, o cliente verifica os outros pacotes na cache para determinar se a eliminação de alguns ou de todos, dos mais antigos pacotes de libertar espaço em disco suficiente para acomodar a imagem. Se a eliminação de pacotes não libertar espaço suficiente no disco, o cliente não transferirá a imagem e a implementação falhará. Isto poderá ocorrer se a cache tiver um pacote de grandes dimensões que tenha sido configurado para se manter na cache. Se a eliminação de pacotes antigos libertar espaço suficiente de disco na cache, o cliente eliminá-los-á e transferirá em seguida a imagem para a cache.  

 O tamanho da cache padrão em clientes do Configuration Manager pode não ser suficientemente grande para a maioria das implementações de imagem do sistema operativo. Se quiser transferir a imagem completa para a cache do cliente, terá de ajustar o tamanho de cache do cliente de Configuration Manager nos computadores de destino para acomodar o tamanho da imagem que está a implementar.  

 Para obter mais informações, veja [Configurar a Cache do Cliente para Clientes do Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

## <a name="task-sequence-deployments"></a>Implementações da sequência de tarefas  
 A sequência de tarefas que criar pode implementar a imagem do sistema operativo num computador cliente do Configuration Manager em uma das seguintes formas:  

- Baixe a imagem e o respetivo conteúdo pela primeira vez para a cache do cliente do Configuration Manager de um ponto de distribuição e, em seguida, instalá-lo.  

- Instalar imediatamente a imagem e o respetivo conteúdo a partir do ponto de distribuição.  

- Instalar a imagem e o respetivo conteúdo, conforme necessário, a partir do ponto de distribuição  

  Por predefinição, quando criar a implementação da sequência de tarefas, a imagem é primeiro transferida para a cache do cliente do Configuration Manager e, em seguida, instalada. Se optar por transferir a imagem para a cache do cliente do Configuration Manager antes de executar a imagem e a sequência de tarefas contiver um passo para reparticionar a unidade de disco rígida, o passo de repartição falhará porque a criação de partições de disco rígido elimina os conteúdos das Cache do cliente do Configuration Manager. Se a sequência de tarefas tiver de reparticionar a unidade de disco rígido, terá de executar a instalação da imagem a partir do ponto de distribuição com a opção **Executar programa a partir do ponto de distribuição**  ao implementar a sequência de tarefas.  

  Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

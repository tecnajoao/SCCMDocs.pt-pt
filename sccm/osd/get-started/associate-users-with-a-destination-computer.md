---
title: Associar utilizadores a um computador
titleSuffix: Configuration Manager
description: Configure o Configuration Manager para associar utilizadores a computadores de destino ao implementar sistemas operativos.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 325b571adbcb2750eaa0b3a856dda753c43634f0
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/23/2018
ms.locfileid: "42755905"
---
# <a name="associate-users-with-a-destination-computer-in-configuration-manager"></a>Associar utilizadores a um computador de destino no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Quando utilizar o Configuration Manager para implementar sistemas operativos, pode associar utilizadores ao computador de destino. Esta opção funciona se um utilizador único ou vários utilizadores são os utilizadores primários do computador de destino.  

 A afinidade dispositivo/utilizador suporta a gestão centrada no utilizador para a implementação de aplicações. Quando associa um utilizador ao computador de destino em que pretende instalar um sistema operacional, pode, posteriormente, implementar aplicações para esse utilizador e as mesmas serão instaladas automaticamente no computador de destino. Embora possa configurar suporte para a afinidade dispositivo / utilizador durante a implementação do sistema operacional, não é possível utilizar a afinidade dispositivo / utilizador para implantar o sistema operacional.  

 Para obter mais informações sobre a afinidade de dispositivo do utilizador, consulte [associar utilizadores e dispositivos à afinidade dispositivo / utilizador](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  

 Existem vários métodos que pode integrar a afinidade dispositivo / utilizador as suas implementações do sistema operacional. É possível integrar a afinidade dispositivo/utilizador em implementações de PXE, implementações de suportes de dados de arranque e implementações de suportes de dados pré-configurados.  


### <a name="create-a-task-sequence-that-includes-the-smstsassignusersmode-variable"></a>Criar uma sequência de tarefas que inclui a variável **SMSTSAssignUsersMode**

 Adicionar a **SMSTSAssignUsersMode** variável para o início da sequência de tarefas utilizando o [definir variável da sequência de tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) passo. Esta variável especifica o modo como a sequência de tarefas processa as informações do utilizador.

 Para obter mais informações, consulte [variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSAssignUsersMode).


### <a name="create-a-prestart-command-that-gathers-the-user-information"></a>Criar um comando de pré-início que reúne as informações do utilizador

 O comando de Pré-início pode ser um VBScript com uma caixa de entrada. Também pode ser um aplicativo HTML (HTA) que valida os dados de utilizador que introduza. 

 Este comando de Pré-início deve definir os **SMSTSUDAUsers** variável que será utilizada quando executa a sequência de tarefas. Esta variável pode ser definida num computador, numa coleção ou numa variável de sequência de tarefas.

 Para obter mais informações, consulte [variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSUDAUsers).


### <a name="configure-how-distribution-points-and-media-associate-the-user-with-the-destination-computer"></a>Configurar o modo como os pontos de distribuição e os suportes de dados associam o utilizador ao computador de destino

 O ponto de distribuição ou o suporte de dados suporta a associação de utilizadores ao computador de destino em que o sistema operativo é implementado. Utilize um dos seguintes métodos: 

 - [Configurar um ponto de distribuição para aceitar pedidos de arranque PXE](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_PXEDistributionPoint)  
 - [Criar suportes de dados de arranque](/sccm/osd/deploy-use/create-bootable-media)  
 - [Criar suportes de dados pré-configurados](/sccm/osd/deploy-use/create-prestaged-media)  


 Configurar o suporte de afinidade de dispositivo de utilizador não tem um método incorporado para validar a identidade do utilizador. Este comportamento é importante quando um técnico de aprovisionamento do computador e introduz as informações em nome do utilizador. Além de definir como a sequência de tarefas processa as informações de utilizador, a configuração destas opções no ponto de distribuição e suporte de dados permite restringir as implementações iniciadas a partir de um arranque PXE ou de um tipo específico de suporte de dados.

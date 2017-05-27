---
title: Associar utilizadores um computador de destino | Documentos do Microsoft
description: Configure o System Center Configuration Manager para associar os utilizadores com computadores de destino ao implementar sistemas operativos.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
caps.latest.revision: 9
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: c0331567b94a99b29cc73c16de17a9f3bc6b9e43
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="associate-users-with-a-destination-computer-in-system-center-configuration-manager"></a>Associar utilizadores a um computador de destino no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando utiliza o System Center Configuration Manager para implementar o sistema operativo, pode associar utilizadores ao computador de destino em que o sistema operativo é implementado. Esta configuração inclui o seguinte:  

-   Se o principal utilizador do computador de destino é um único utilizador.  

-   Se os principais utilizadores do computador de destino são vários utilizadores.  

 A afinidade dispositivo/utilizador suporta a gestão centrada no utilizador para a implementação de aplicações. Ao associar um utilizador ao computador de destino em que pretende instalar um sistema operativo, poderá, posteriormente, implementar aplicações para esse utilizador e as mesmas serão instaladas automaticamente no computador de destino. No entanto, embora seja possível configurar o suporte para a afinidade dispositivo/utilizador ao implementar sistemas operativos, não é possível utilizar a afinidade dispositivo/utilizador para implementar sistemas operativos.  

 Para obter mais informações sobre a afinidade dispositivo / utilizador, consulte o artigo [associar utilizadores e dispositivos com a afinidade dispositivo / utilizador](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

## <a name="how-to-specify-a-user-when-you-deploy-operating-systems"></a>Como especificar um utilizador ao implementar sistemas operativos  
 A tabela seguinte lista as ações que pode efetuar para integrar a afinidade dispositivo/utilizador nas implementações de sistemas operativos. É possível integrar a afinidade dispositivo/utilizador em implementações de PXE, implementações de suportes de dados de arranque e implementações de suportes de dados pré-configurados.  

|Ação|Mais informações|  
|------------|----------------------|  
|Criar uma sequência de tarefas que inclui a variável **SMSTSAssignUsersMode**|Adicione a variável **SMSTSAssignUsersMode** ao início da sequência de tarefas utilizando o passo da sequência de tarefas [Definir Variável da Sequência de Tarefas](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable). Esta variável especifica o modo como a sequência de tarefas processa as informações do utilizador.<br /><br /> Defina a variável num dos seguintes valores:<br /><br /> <br /><br /> **Automática**: A sequência de tarefas cria automaticamente uma relação entre o utilizador e de destino computador e implementa o sistema operativo.<br /><br /> **Pendente**: A sequência de tarefas cria uma relação entre o utilizador e o computador de destino, mas aguarda a aprovação do utilizador administrativo antes do sistema operativo é implementado.<br /><br /> **Desativado**: A sequência de tarefas não associa um utilizador ao computador de destino e continua a implementar o sistema operativo.<br /><br /> <br /><br /> Esta variável também pode ser definida num computador ou numa coleção. Para mais informações sobre as variáveis incorporadas, consulte o artigo [variáveis incorporadas de sequência de tarefas](../../osd/understand/task-sequence-built-in-variables.md).|  
|Criar um comando de pré-início que reúne as informações do utilizador|O comando de pré-início pode ser um script do Visual Basic (VB) com uma caixa de entrada ou uma aplicação de HTML (HTA) que valide os dados do utilizador introduzidos.<br /><br /> O comando de pré-início deve definir a variável **SMSTSUdaUsers** que é utilizada quando a sequência de tarefas é executada. Esta variável pode ser definida num computador, numa coleção ou numa variável de sequência de tarefas. Utilize o seguinte formato para adicionar múltiplos utilizadores: *domínio\utilizador1, domínio\utilizador2, domínio\utilizador3*.|  
|Configurar o modo como os pontos de distribuição e os suportes de dados associam o utilizador ao computador de destino|Ao [configurar um ponto de distribuição para aceitar pedidos de arranque PXE](https://technet.microsoft.com/library/mt627944\(TechNet.10\).aspx#BKMK_PXEDistributionPoint) e ao criar [suportes de dados de arranque](http://technet.microsoft.com/library/mt627921\(TechNet.10\).aspx) ou [suportes de dados pré-configurados](https://technet.microsoft.com/library/mt627922\(TechNet.10\).aspx) através do Assistente de Criação de Suporte de Dados da Sequência de Tarefas, é possível especificar o modo como o ponto de distribuição ou o suporte de dados suporta a associação de utilizadores ao computador de destino em que o sistema operativo é implementado.<br /><br /> A configuração do suporte da afinidade dispositivo/utilizador não possui um método incorporado para validar a identidade do utilizador. Este aspeto pode ser importante quando um técnico, durante o aprovisionamento do computador, introduz as informações em nome do utilizador. Além de definir o modo como as informações do utilizador serão processadas pela sequência de tarefas, a configuração destas opções no ponto de distribuição e no suporte de dados permite restringir as implementações iniciadas a partir de um arranque PXE ou de um tipo de suporte de dados específico.|  


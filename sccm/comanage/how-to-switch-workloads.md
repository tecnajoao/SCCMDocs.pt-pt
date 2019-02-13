---
title: Mudar cargas de trabalho de cogestão
titleSuffix: Configuration Manager
description: Saiba como mudar cargas de trabalho atualmente gerenciadas pelo Configuration Manager para o Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.collection: M365-identity-device-management
ms.openlocfilehash: a4b50d0491644e6be0967c1adcf2db641c1bb1cd
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137997"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Como mudar cargas de trabalho do Configuration Manager para o Intune

Um dos benefícios de cogestão oscila cargas de trabalho do Configuration Manager para o Microsoft Intune. Quando um dispositivo Windows 10 tem o cliente do Configuration Manager e é inscrito no Intune, obtém os benefícios de ambos os serviços. Pode controlar quais cargas de trabalho, se houver, que mudar a autoridade do Configuration Manager para o Intune. O Configuration Manager continua a gerir todas as outras cargas de trabalho, incluindo essas cargas de trabalho que não mude para o Intune e não oferece suporte a todos os outros recursos do Configuration Manager que cogestão.

Para obter mais informações sobre as cargas de trabalho suportadas, consulte [cargas de trabalho](/sccm/comanage/workloads).

Pode mudar as cargas de trabalho ao ativar a cogestão ou posteriormente, quando estiver pronto. Se ainda não ativou a cogestão, faça-o primeiro. Para obter mais informações, consulte [como ativar a cogestão](/sccm/comanage/how-to-enable).


Depois de ativar a cogestão, modifique as definições nas propriedades de cogestão. 

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **serviços Cloud**e selecione o **cogestão** nó.  

2. Selecione o objeto de cogestão e, em seguida, escolha **propriedades** na faixa de opções.  

3. Mude para o **cargas de trabalho** separador. Por predefinição, todas as cargas de trabalho são configuradas para o **Configuration Manager** definição. Para mudar uma carga de trabalho, mova o controlo de deslize para essa carga de trabalho para a definição pretendida.  

    ![Separador de captura de ecrã de cargas de trabalho na página de propriedades de cogestão](media/properties-workloads.png)

    - **O Configuration Manager**: O Configuration Manager continua a gerir esta carga de trabalho.  

    - **Criar um piloto do Intune**: Alterne esta carga de trabalho apenas para os dispositivos na coleção piloto. Pode alterar o **coleção de projetos-piloto** sobre o **teste** separador da página de propriedades de cogestão.  

    - **Intune**: Comutador esta carga de trabalho para todos os dispositivos Windows 10 inscritos na cogestão.  


> [!Important]  
> Antes de alternar quaisquer cargas de trabalho, certifique-se de que configure corretamente e implementar a carga de trabalho correspondente no Intune. Certifique-se de que as cargas de trabalho são sempre gerenciadas por uma das ferramentas de gerenciamento para os seus dispositivos.  

<!--1357377--> Os dispositivos cogeridos automaticamente a partir do Configuration Manager versão 1806, quando alterna uma carga de trabalho de cogestão, sincronizar política MDM do Microsoft Intune. Esta sincronização ocorre também quando inicia o **transferir política do computador** ação a partir de notificações do cliente na consola do Configuration Manager. Para obter mais informações, consulte [iniciar a obtenção de política de cliente com a notificação do cliente](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).



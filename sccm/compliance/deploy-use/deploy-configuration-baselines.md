---
title: "Implemente linhas de base de configuração | Documentos do Microsoft"
description: "Implemente linhas de base de configuração para definir as implementações de linha de base de configuração e para adicionar ou remover linhas de base de configuração de implementações."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9be8aaf3-075e-4acd-abd2-7459254e16e2
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f9e939d871e95a3248d8e5d96cb73063a81fd5cf
ms.openlocfilehash: 9c9e6b7780c7c10c20a60dbbbf506e916031eb88
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-deploy-configuration-baselines-in-system-center-configuration-manager"></a>Como implementar linhas de base de configuração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Linhas de base de configuração no System Center Configuration Manager devem ser implementadas numa ou mais coleções de utilizadores ou dispositivos antes de dispositivos cliente dessas coleções podem avaliar a respetiva conformidade com a linha de base de configuração.  

Utilize a caixa de diálogo **Implementar Linhas de Base de Configuração** para definir implementações da linha de base de configuração, que inclui adicionar ou remover linhas de base de configuração de implementações, além de especificar o agendamento de avaliação.  

## <a name="deploy-a-configuration-baseline"></a>Implementar uma linha de base de configuração  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **linhas de base de configuração**.  

3.  Na lista **Perfis de E-mail** , selecione o perfil de e-mail que pretende implementar e, em seguida, no separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.  

4.  Na caixa de diálogo **Implementar Linhas de Base de Configuração** , selecione as linhas de base de configuração que pretende implementar na lista **Linhas de base de configuração disponíveis** . Clique em **Adicionar** para adicioná-las à lista **Linhas de base de configuração selecionadas** .  

    > [!IMPORTANT]  
    >  Se alterar um item de configuração adicionado a uma linha de base de configuração implementada, o item de configuração revisto só é avaliado em termos de conformidade depois da próxima hora de avaliação agendada.  

5.  Especifique as seguintes informações adicionais:  

    -   **Remediar regras incompatíveis quando suportado** – automaticamente retifica quaisquer regras não compatíveis para o Windows Management Instrumentation (WMI), o registo, scripts e todas as definições para dispositivos móveis inscritos pelo Configuration Manager.  

    -   **Permitir remediação fora da janela de manutenção** – Se uma janela de manutenção tiver sido configurada para a coleção onde pretende implementar a linha de base de configuração, ative esta opção para que as definições de conformidade retifiquem o valor fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte o artigo [como utilizar as janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).  

6.  **Gerar um alerta** – configura um alerta que é gerado se a compatibilidade da linha de base de configuração for inferior a uma percentagem especificada até uma data e hora especificadas. Também pode especificar se pretende que seja enviado um alerta para o System Center Operations Manager.  

7.  **Coleção** - Clique em **Procurar** para selecionar a coleção na qual pretende implementar a linha de base de configuração.  

8.  **Especifique o agendamento de avaliação de compatibilidade para esta linha de base de configuração** Especifica o agendamento através do qual a linha de base de configuração implementado é avaliada nos computadores cliente. Pode ser um agendamento simples ou personalizado.  

    > [!NOTE]  
    >  Se a linha de base de configuração for implementada num computador, esta é avaliada em termos de conformidade duas horas após a hora de início agendada. Se for implementado num utilizador, é avaliada em termos de compatibilidade quando o utilizador inicia sessão.  

9. Clique em **OK** para fechar a caixa de diálogo **Implementar Linhas de Base de Configuração** e criar a implementação. Para obter mais informações sobre como monitorizar a implementação, consulte o artigo [monitorizar as definições de compatibilidade](/sccm/compliance/deploy-use/monitor-compliance-settings).  


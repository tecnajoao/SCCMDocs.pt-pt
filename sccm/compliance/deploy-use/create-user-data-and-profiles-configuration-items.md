---
title: "Criar perfis e dados de utilizador de itens de configuração | Documentos do Microsoft"
description: "Utilize dados e perfis de itens de configuração no System Center Configuration Manager para gerir o redirecionamento de pastas, ficheiros offline e perfis itinerantes."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9fcbcc81-cd6f-496e-b075-ef1afa2b8ccc
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f9e939d871e95a3248d8e5d96cb73063a81fd5cf
ms.openlocfilehash: 85b984d739dc9f9d2046186b381eff54ba687c66
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---

# <a name="create-user-data-and-profiles-configuration-items-in-system-center-configuration-manager"></a>Criar perfis e dados de utilizador itens de configuração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilizador dados e perfis de itens de configuração no System Center Configuration Manager contêm definições que podem gerir o redirecionamento de pastas, ficheiros offline e perfis itinerantes em computadores que executam o Windows 8 e posterior para utilizadores na hierarquia. Por exemplo, pode:  

-   Redirecionar a pasta de documentos de um utilizador para uma partilha de rede.  

-   Garantir que os ficheiros especificados armazenados na rede estão disponíveis no computador do utilizador quando a ligação de rede está indisponível.  

-   Configurar os ficheiros no perfil itinerante do utilizador, que são sincronizados com uma partilha de rede quando o utilizador iniciar e fechar sessão.  

 Ao contrário de outros itens de configuração no Configuration Manager, não adicionar dados de utilizador e itens de configuração para uma linha de base de configuração que irá depois implementar de perfil. Em vez disso, implementa o item de configuração diretamente através da caixa de diálogo **Implementar Item de Configuração de Perfis e Dados do Utilizador** .  

> [!IMPORTANT]  
>  Só pode implementar itens de configuração de dados e perfis de utilizador em coleções de utilizadores.  

## <a name="enable-user-data-and-profiles-for-compliance-settings"></a>Ativar dados e perfis de utilizador para definições de compatibilidade  
 Utilize o procedimento seguinte para configurar a predefinição do cliente para definições de compatibilidade de dados e perfis de utilizador, que serão aplicadas a todos os computadores na sua hierarquia. Se pretender que estas definições se apliquem apenas a alguns computadores, crie uma definição personalizada do cliente do dispositivo e atribua-a a uma coleção que contenha os computadores para os quais pretende utilizar as definições de compatibilidade de dados e perfis de utilizador. Para obter mais informações sobre como criar definições personalizadas do dispositivo, consulte o artigo [como configurar as definições de cliente](../../core/clients/deploy/configure-client-settings.md).  

1.  Na consola do Configuration Manager, clique em **administração** > **definições de cliente** > **predefinições**.  

4.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Na caixa de diálogo **Predefinições** , clique em **Definições de Compatibilidade**.  

6.  Na lista pendente **Ativar Dados e Perfis de Utilizador** , selecione **Sim**.  

7.  Clique em **OK** para fechar a caixa de diálogo **Predefinições** .  

## <a name="create-a-user-data-and-profiles-configuration-item"></a>Criar um item de configuração de dados e perfis de utilizador  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **perfis e dados de utilizador**.  

3.  No separador **Início** , no grupo **Criar** , clique em **Criar Item de Configuração de Dados e Perfis de Utilizador**.  

4.  Na página **Geral** do **Assistente para Criar Itens de Configuração de Perfis e Dados do Utilizador**, especifique as seguintes informações:  

    -   **Nome:** Introduza um nome exclusivo para o item de configuração. Pode utilizar até 256 carateres.  

    -   **Descrição:** Forneça uma descrição que proporcione uma descrição geral sobre o item de configuração e outras informações relevantes que ajudem a identificá-la na consola do Configuration Manager. Pode utilizar até 256 carateres.  

    -   **Redirecionamento de pastas:** Selecione esta caixa se pretender configurar as definições de redirecionamento de pastas para este item de configuração.  

    -   **Ficheiros offline:** Selecione esta caixa se pretender configurar definições para os ficheiros offline para este item de configuração.  

    -   **Perfis de utilizador itinerantes:** Selecione esta caixa se pretender configurar as definições de perfis de utilizador itinerantes para este item de configuração.  

5.  Na página **Redirecionamento de Pastas** do **Assistente para Criar Itens de Configuração de Perfis e Dados do Utilizador**, especifique como pretende que os computadores cliente dos utilizadores que recebam este item de configuração façam a gestão do redirecionamento de pastas. Pode configurar as definições de qualquer dispositivo a que o utilizador inicie sessão ou apenas para os dispositivos primários do utilizador. Para mais informações sobre redirecionamento de pastas, consulte a documentação do Windows Server.  

    > [!NOTE]  
    >  Nesta página só aparece se assinalado **redirecionamento de pastas** no **geral** página do assistente.  

6.  Na página **Ficheiros Offline** do **Assistente para Criar Itens de Configuração de Perfis e Dados do Utilizador**, pode ativar ou desativar a utilização de ficheiros offline para os utilizadores que recebem este item de configuração e configuram definições para o comportamento dos ficheiros offline. Também pode especificar os ficheiros offline que estarão sempre disponíveis em qualquer computador em que o utilizador inicie sessão. Para mais informações sobre ficheiros offline, consulte a documentação do Windows Server.  

    > [!NOTE]  
    >  Nesta página só aparece se tiver dado que a caixa **ficheiros Offline** no **geral** página do assistente.  

7.  Na página **Perfis Itinerantes** do **Assistente para Criar Itens de Configuração de Perfis e Dados do Utilizador**, pode configurar se os perfis itinerantes estão disponíveis nos computadores onde o utilizador iniciar sessão e também configurar outras informações sobre como se comportam estes perfis. Para mais informações sobre perfis itinerantes, consulte a documentação do Windows Server.  

    > [!NOTE]  
    >  Nesta página só aparece se tiver dado que a caixa **perfis de utilizador itinerantes** no **geral** página do assistente.  

8.  Conclua o assistente.  

 Os novos itens de configuração de perfis e dados do utilizador são mostrados no nó **Perfis e Dados do Utilizador** da área de trabalho **Ativos e Compatibilidade** .  

## <a name="deploy-a-user-data-and-profiles-configuration-item"></a>Implementar um item de configuração de dados e perfis de utilizador  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **perfis e dados de utilizador**.  

3.  Selecione o item de configuração de perfis e dados do utilizador que pretende implementar e, em seguida, no separador **Início** , no grupo **Implementação** , clique em **Implementar**.  

4.  Na caixa de diálogo **Implementar Item de Configuração de Perfis e Dados do Utilizador** , especifique as seguintes informações.  

    -   **Coleção** - Clique em **Procurar** para selecionar a coleção do utilizador na qual pretende implementar o item de configuração.  

        > [!IMPORTANT]  
        >  Só pode implementar itens de configuração de dados e perfis de utilizador em coleções de utilizadores.  

    -   **Remediar regras incompatíveis quando suportado** – Ative esta opção para retificar automaticamente quaisquer regras que sejam consideradas não compatíveis em computadores cliente.  

    -   **Permitir remediação fora da janela de manutenção** – Se uma janela de manutenção tiver sido configurada para a coleção onde pretende implementar o item de configuração, ative esta opção para que as definições de conformidade retifiquem o valor fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte o artigo [como utilizar as janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Gerar um alerta** - Ative esta opção para configurar um alerta que é gerado se a compatibilidade do item de configuração for inferior a uma percentagem especificada por data e hora específicas. Também pode especificar se pretende que seja enviado um alerta para o System Center Operations Manager.  

    -   **Especificar a agenda de avaliação de conformidade deste item de configuração** - Especifica o agendamento através do qual o item de configuração implementado é avaliado nos computadores cliente. Pode ser um agendamento simples ou personalizado.  

5.  Clique em **OK** para fechar a caixa de diálogo **Implementar Item de Configuração de Perfis e Dados do Utilizador** e criar a implementação.  

## <a name="monitor-a-user-data-and-profiles-configuration-item"></a>Monitorizar um item de configuração de perfis e dados do utilizador  
 Monitorizar este tipo de item de configuração da mesma forma que monitorizar outras definições de compatibilidade.  

 Para obter mais informações, consulte o artigo [como monitorizar as definições de compatibilidade](../../compliance/deploy-use/monitor-compliance-settings.md).  

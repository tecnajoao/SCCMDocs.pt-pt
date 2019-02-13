---
title: Criar itens de configuração de dados e perfis de utilizador
titleSuffix: Configuration Manager
description: Use itens de configuração de perfis e dados no System Center Configuration Manager para gerir o redirecionamento de pastas, ficheiros offline e perfis itinerantes.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9fcbcc81-cd6f-496e-b075-ef1afa2b8ccc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: e6ae7f6b14da4f5959e336e08bec0e71896425ff
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129923"
---
# <a name="create-user-data-and-profiles-configuration-items-in-system-center-configuration-manager"></a>Criar perfis e dados de utilizador itens de configuração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilizador de perfis e dados de itens de configuração no System Center Configuration Manager contêm definições que gerem o redirecionamento de pastas, ficheiros offline e perfis itinerantes em computadores que executam o Windows 8 e posterior para utilizadores na sua hierarquia. Por exemplo, pode:  

- Redirecionar a pasta de documentos de um utilizador para uma partilha de rede.  

- Garantir que os ficheiros especificados armazenados na rede estão disponíveis no computador do utilizador quando a ligação de rede está indisponível.  

- Configurar os ficheiros no perfil itinerante do utilizador, que são sincronizados com uma partilha de rede quando o utilizador iniciar e fechar sessão.  

  Ao contrário de outros itens de configuração no Configuration Manager, não adicionar dados de utilizador e itens de configuração para uma linha de base de configuração que, em seguida, implementar o perfil. Em vez disso, implementa o item de configuração diretamente através da caixa de diálogo **Implementar Item de Configuração de Perfis e Dados do Utilizador** .  

> [!IMPORTANT]  
>  Só pode implementar itens de configuração de dados e perfis de utilizador em coleções de utilizadores.  

## <a name="enable-user-data-and-profiles-for-compliance-settings"></a>Ativar dados e perfis de utilizador para definições de compatibilidade  
 Utilize o procedimento seguinte para configurar a predefinição do cliente para definições de compatibilidade de dados e perfis de utilizador, que serão aplicadas a todos os computadores na sua hierarquia. Se pretender que estas definições se apliquem apenas a alguns computadores, crie uma definição personalizada do cliente do dispositivo e atribua-a a uma coleção que contenha os computadores para os quais pretende utilizar as definições de compatibilidade de dados e perfis de utilizador. Para obter mais informações sobre como criar definições personalizadas do dispositivo, consulte [como configurar as definições de cliente](../../core/clients/deploy/configure-client-settings.md).  

1.  Na consola do Configuration Manager, clique em **Administration** > **definições de cliente** > **predefinições**.  

4.  No separador **Home page** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Na caixa de diálogo **Predefinições** , clique em **Definições de Compatibilidade**.  

6.  Na lista pendente **Ativar Dados e Perfis de Utilizador** , selecione **Sim**.  

7.  Clique em **OK** para fechar a caixa de diálogo **Predefinições** .  

## <a name="create-a-user-data-and-profiles-configuration-item"></a>Criar um item de configuração de perfis e dados do utilizador  

1. Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **perfis e dados de utilizador**.  

2. No separador **Início** , no grupo **Criar** , clique em **Criar Item de Configuração de Dados e Perfis de Utilizador**.  

3. Na página **Geral** do **Assistente para Criar Itens de Configuração de Perfis e Dados do Utilizador**, especifique as seguintes informações:  

   -   **Nome:** Introduza um nome exclusivo para o item de configuração. Pode utilizar até 256 carateres.  

   -   **Descrição:** Forneça uma descrição que proporcione uma descrição geral do item de configuração e outras informações relevantes que ajudem a identificá-la na consola do Configuration Manager. Pode utilizar até 256 carateres.  

   -   **Redirecionamento de pastas:** Marque esta caixa se quiser configurar as definições de redirecionamento de pasta para este item de configuração.  

   -   **Ficheiros offline:** Marque esta caixa se quiser configurar as definições de ficheiros offline deste item de configuração.  

   -   **Perfis de utilizador itinerantes:** Marque esta caixa se quiser configurar as definições para perfis de utilizador itinerantes para este item de configuração.  

4. Na página **Redirecionamento de Pastas** do **Assistente para Criar Itens de Configuração de Perfis e Dados do Utilizador**, especifique como pretende que os computadores cliente dos utilizadores que recebam este item de configuração façam a gestão do redirecionamento de pastas. Pode configurar as definições de qualquer dispositivo a que o utilizador inicie sessão ou apenas para os dispositivos primários do utilizador. Para mais informações sobre redirecionamento de pastas, consulte a documentação do Windows Server.  

   > [!NOTE]  
   >  Esta página só é apresentada se tiver selecionado **redirecionamento de pastas** sobre o **geral** página do assistente.  

5. Na página **Ficheiros Offline** do **Assistente para Criar Itens de Configuração de Perfis e Dados do Utilizador**, pode ativar ou desativar a utilização de ficheiros offline para os utilizadores que recebem este item de configuração e configuram definições para o comportamento dos ficheiros offline. Também pode especificar os ficheiros offline que estarão sempre disponíveis em qualquer computador em que o utilizador inicie sessão. Para mais informações sobre ficheiros offline, consulte a documentação do Windows Server.  

   > [!NOTE]  
   >  Esta página é apresentada apenas se tiver selecionado a caixa **arquivos Offline** sobre o **geral** página do assistente.  

6. Na página **Perfis Itinerantes** do **Assistente para Criar Itens de Configuração de Perfis e Dados do Utilizador**, pode configurar se os perfis itinerantes estão disponíveis nos computadores onde o utilizador iniciar sessão e também configurar outras informações sobre como se comportam estes perfis. Para mais informações sobre perfis itinerantes, consulte a documentação do Windows Server.  

   > [!NOTE]  
   >  Esta página é apresentada apenas se tiver selecionado a caixa **perfis de utilizador itinerantes** sobre o **geral** página do assistente.  

7. Conclua o assistente.  

   Os novos itens de configuração de perfis e dados do utilizador são mostrados no nó **Perfis e Dados do Utilizador** da área de trabalho **Ativos e Compatibilidade** .  

## <a name="deploy-a-user-data-and-profiles-configuration-item"></a>Implementar um item de configuração de perfis e dados do utilizador  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **perfis e dados de utilizador**.  

3.  Selecione o item de configuração de perfis e dados do utilizador que pretende implementar e, em seguida, no separador **Início** , no grupo **Implementação** , clique em **Implementar**.  

4.  Na caixa de diálogo **Implementar Item de Configuração de Perfis e Dados do Utilizador** , especifique as seguintes informações.  

    -   **Coleção** - Clique em **Procurar** para selecionar a coleção do utilizador na qual pretende implementar o item de configuração.  

        > [!IMPORTANT]  
        >  Só pode implementar itens de configuração de dados e perfis de utilizador em coleções de utilizadores.  

    -   **Remediar regras incompatíveis quando suportado** – Ative esta opção para retificar automaticamente quaisquer regras que sejam consideradas não compatíveis em computadores cliente.  

    -   **Permitir remediação fora da janela de manutenção** – Se uma janela de manutenção tiver sido configurada para a coleção onde pretende implementar o item de configuração, ative esta opção para que as definições de conformidade retifiquem o valor fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [como utilizar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Gerar um alerta** - Ative esta opção para configurar um alerta que é gerado se a compatibilidade do item de configuração for inferior a uma percentagem especificada por data e hora específicas. Também pode especificar se pretende que seja enviado um alerta para o System Center Operations Manager.  

    -   **Especificar a agenda de avaliação de conformidade deste item de configuração** - Especifica o agendamento através do qual o item de configuração implementado é avaliado nos computadores cliente. Pode ser um agendamento simples ou personalizado.  

5.  Clique em **OK** para fechar a caixa de diálogo **Implementar Item de Configuração de Perfis e Dados do Utilizador** e criar a implementação.  

## <a name="monitor-a-user-data-and-profiles-configuration-item"></a>Monitorizar um item de configuração de perfis e dados do utilizador  
 Monitorizar este tipo de item de configuração da mesma forma que monitoriza outras definições de compatibilidade.  

 Para obter mais informações, consulte [como monitorizar as definições de conformidade](../../compliance/deploy-use/monitor-compliance-settings.md).  

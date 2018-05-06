---
title: Planear e configurar as definições de compatibilidade
titleSuffix: Configuration Manager
description: Saiba mais sobre os pré-requisitos e as tarefas de configuração para trabalhar com as definições de compatibilidade no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 84643f38b5dd0c42a611ca50aaae6ab6d9f52405
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="plan-for-and-configure-compliance-settings-in-system-center-configuration-manager"></a>Planear e configurar as definições de compatibilidade no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de começar a trabalhar com as definições de compatibilidade do System Center Configuration Manager, existem alguns pré-requisitos que deve conhecer e algumas tarefas de configuração, terá de efetuar.  

## <a name="prerequisites-for-compliance-settings"></a>Pré-requisitos para definições de compatibilidade  

|Pré-requisito|Mais informações|  
|------------------|----------------------|  
|Os clientes do Gestor de configuração do Windows tem de estar ativados e configurados para a avaliação de compatibilidade.|Consulte abaixo|  
|Se pretender executar relatórios, tem de configurar relatórios para o seu site.|[Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md)|  
|Permissões de segurança necessário.|O **Gestor de definições de compatibilidade** função de segurança inclui as permissões necessárias para gerir as definições de compatibilidade, itens de configuração de perfis e dados de utilizador e perfis de ligação remota.<br /><br /> [Configurar a administração baseada em funções](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>Ativar e configurar as definições de compatibilidade (para apenas PCs Windows)  

Este procedimento configura as predefinições de cliente para definições de compatibilidade e aplica-se a todos os computadores na sua hierarquia. Se pretender que estas definições se apliquem apenas a alguns computadores, crie uma definição personalizada do cliente do dispositivo e atribua-a a uma coleção que contenha os computadores para os quais pretende utilizar definições de compatibilidade. Para obter mais informações sobre como criar definições personalizadas de dispositivos, consulte [como configurar as definições de cliente](../../core/clients/deploy/configure-client-settings.md).  

> [!TIP]  
>  Outros tipos de dispositivo não requerem nenhuma configuração específica para avaliar definições de compatibilidade.  

1.  Na consola do Configuration Manager, clique em **administração** > **as definições de cliente** > **predefinições**.  
2.  No separador **Home page** , no grupo **Propriedades** , clique em **Propriedades**.  
3.  Na caixa de diálogo **Predefinições** , clique em **Definições de Compatibilidade**.  
4.  Configure as seguintes definições do cliente para as definições de compatibilidade:
    - **Ativar avaliação de compatibilidade nos clientes** -definido como **verdadeiro** se pretender avaliar a compatibilidade nos dispositivos cliente.
    - **Agendar avaliação de compatibilidade** -clique em **agenda** se pretender modificar a agenda de avaliação de compatibilidade predefinido nos dispositivos cliente.
    - **Ativar perfis e dados de utilizador** -ative esta opção se pretende criar e implementar itens de configuração de perfis e dados do utilizador em computadores Windows. Para obter mais informações, consulte [criar itens de configuração de perfis e dados de utilizador](/sccm/compliance/deploy-use/create-remote-connection-profiles).
5. Clique em **OK** para fechar a caixa de diálogo **Predefinições** .  

Os computadores cliente são configurados com estas definições da próxima vez que transferirem a política de cliente.  

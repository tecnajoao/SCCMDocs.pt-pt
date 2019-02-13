---
title: Planear e configurar as definições de compatibilidade
titleSuffix: Configuration Manager
description: Saiba mais sobre os pré-requisitos e as tarefas de configuração para trabalhar com definições de compatibilidade no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49f7d898e5cb744771694ce49adb52457fb25e01
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156428"
---
# <a name="plan-for-and-configure-compliance-settings-in-system-center-configuration-manager"></a>Planear e configurar as definições de compatibilidade no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de começar a trabalhar com as definições de compatibilidade do System Center Configuration Manager, existem alguns pré-requisitos, que precisa saber sobre e precisará executar algumas tarefas de configuração.  

## <a name="prerequisites-for-compliance-settings"></a>Pré-requisitos para definições de compatibilidade  

|Pré-requisito|Mais informações|  
|------------------|----------------------|  
|Os clientes do Configuration Manager do Windows tem de ser ativados e configurados para a avaliação de conformidade.|Veja a seguir|  
|Se pretender executar relatórios, tem de configurar relatórios para o seu site.|[Os relatórios do System Center Configuration Manager.](../../core/servers/manage/reporting.md)|  
|Permissões de segurança necessárias.|O **Gestor de definições de conformidade** função de segurança inclui as permissões necessárias para gerir as definições de compatibilidade, itens de configuração de perfis e dados de utilizador e perfis de ligação remota.<br /><br /> [Configurar a administração baseada em funções](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>Ativar e configurar definições de conformidade (para apenas para PCs Windows)  

Este procedimento configura as predefinições de cliente para definições de compatibilidade e aplica-se a todos os computadores na sua hierarquia. Se pretender que estas definições se apliquem apenas a alguns computadores, crie uma definição personalizada do cliente do dispositivo e atribua-a a uma coleção que contenha os computadores para os quais pretende utilizar definições de compatibilidade. Para obter mais informações sobre como criar definições personalizadas do dispositivo, consulte [como configurar as definições de cliente](../../core/clients/deploy/configure-client-settings.md).  

> [!TIP]  
>  Outros tipos de dispositivo não requerem nenhuma configuração específica para avaliar definições de compatibilidade.  

1.  Na consola do Configuration Manager, clique em **Administration** > **definições de cliente** > **predefinições**.  
2.  No separador **Home page** , no grupo **Propriedades** , clique em **Propriedades**.  
3.  Na caixa de diálogo **Predefinições** , clique em **Definições de Compatibilidade**.  
4.  Configure as seguintes definições do cliente para as definições de compatibilidade:
    - **Ativar avaliação de compatibilidade nos clientes** -definido como **True** se pretender avaliar a compatibilidade nos dispositivos cliente.
    - **Agendar avaliação de conformidade** -clique em **agenda** se pretender modificar o agendamento de avaliação de compatibilidade predefinido nos dispositivos cliente.
    - **Ativar perfis e dados de utilizador** -ative esta opção se pretender criar e implementar itens de configuração de perfis e dados de utilizador para computadores Windows. Para obter detalhes, consulte [criar perfis e dados de utilizador de itens de configuração](/sccm/compliance/deploy-use/create-remote-connection-profiles).
5. Clique em **OK** para fechar a caixa de diálogo **Predefinições** .  

Os computadores cliente são configurados com estas definições da próxima vez que transferirem a política de cliente.  

---
title: "Planear e configurar as definições de compatibilidade | Documentos do Microsoft"
description: "Saiba mais sobre os pré-requisitos e as tarefas de configuração para trabalhar com as definições de compatibilidade no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f9e939d871e95a3248d8e5d96cb73063a81fd5cf
ms.openlocfilehash: d26ac3de58d2f0ef447725e63fc2d8adda6ea06c
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="plan-for-and-configure-compliance-settings-in-system-center-configuration-manager"></a>Planear e configurar as definições de compatibilidade no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de começar a trabalhar com definições de compatibilidade do System Center Configuration Manager, existem alguns pré-requisitos, que é necessário saber sobre e terá de realizar algumas tarefas de configuração.  

## <a name="prerequisites-for-compliance-settings"></a>Pré-requisitos para definições de compatibilidade  

|Pré-requisito|Mais informações|  
|------------------|----------------------|  
|Os clientes do Gestor de configuração do Windows tem de ser ativados e configurados para avaliação de compatibilidade.|Consulte abaixo|  
|Se pretender executar relatórios, tem de configurar relatórios para o seu site.|[Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md)|  
|Permissões de segurança necessárias.|O **Gestor de definições de compatibilidade** função de segurança inclui as permissões necessárias para gerir as definições de compatibilidade, itens de configuração de dados e perfis de utilizador e perfis de ligação remota.<br /><br /> [Configurar a administração baseada em funções](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>Ativar e configurar as definições de compatibilidade (para Windows PCs)  

Este procedimento configura as predefinições de cliente para definições de compatibilidade e aplica-se a todos os computadores na sua hierarquia. Se pretender que estas definições se apliquem apenas a alguns computadores, crie uma definição personalizada do cliente do dispositivo e atribua-a a uma coleção que contenha os computadores para os quais pretende utilizar definições de compatibilidade. Para obter mais informações sobre como criar definições personalizadas do dispositivo, consulte o artigo [como configurar as definições de cliente](../../core/clients/deploy/configure-client-settings.md).  

> [!TIP]  
>  Outros tipos de dispositivo não requerem nenhuma configuração específica para avaliar definições de compatibilidade.  

1.  Na consola do Configuration Manager, clique em **administração** > **definições de cliente** > **predefinições**.  
2.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  
3.  Na caixa de diálogo **Predefinições** , clique em **Definições de Compatibilidade**.  
4.  Configure as seguintes definições do cliente para as definições de compatibilidade:
    - **Ativar avaliação de compatibilidade nos clientes** -definido como **verdadeiro** se pretender avaliar a compatibilidade em dispositivos cliente.
    - **Agendar avaliação de compatibilidade** -clique em **agenda** se pretender modificar a agenda de avaliação de compatibilidade predefinido nos dispositivos cliente.
    - **Ativar dados e utilizador perfis** -ative esta opção se pretende criar e implementar itens de configuração de dados e perfis de utilizador para computadores com o Windows. Para obter mais detalhes, consulte o artigo [criar perfis e dados de utilizador de itens de configuração](/sccm/compliance/deploy-use/create-remote-connection-profiles).
5. Clique em **OK** para fechar a caixa de diálogo **Predefinições** .  

Os computadores cliente são configurados com estas definições da próxima vez que transferirem a política de cliente.  


---
title: Políticas de Firewall do Windows para o Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como criar e implementar políticas de firewall para o Endpoint Protection no System Center 2012 Configuration Manager.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6ecdfad1-6305-45a8-ae75-3f33b967cb8f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3217fe8f6d9ee541105abdecf9963898af38b907
ms.sourcegitcommit: 316899b08f2ef372993909e08e069f7edfed1d33
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/07/2018
ms.locfileid: "44111030"
---
# <a name="create-and-deploy-windows-firewall-policies-for-endpoint-protection-in-system-center-configuration-manager"></a>Criar e implementar políticas de Firewall do Windows para o Endpoint Protection no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Políticas de firewall para o Endpoint Protection no System Center Configuration Manager permitem-lhe efetuar tarefas de manutenção e de configuração básica do Firewall do Windows em computadores cliente na sua hierarquia. Pode utilizar as políticas de Firewall do Windows para efetuar as seguintes tarefas:  

-   Controlar se a Firewall do Windows está ativada ou desativada.  

-   Controlar se as ligações recebidas têm permissões para computadores cliente.  

-   Controlar se os utilizadores são avisados quando a Firewall do Windows bloqueia um programa novo.  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na **ativos e compatibilidade** área de trabalho, expanda **Endpoint Protection**e, em seguida, clique em **políticas de Firewall do Windows**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Política de Firewall do Windows**.  

4.  Na página **Geral** do **Assistente da Criação da Política de Firewall do Windows**, especifique um nome e uma descrição opcional para esta política de firewall e, em seguida, clique **Seguinte**.  

5.  Na página **Definições de Perfil** do assistente, configure as seguintes definições para cada perfil de rede:  

    > [!IMPORTANT]  
    >  Se pretender implementar as políticas da Firewall do Windows em computadores com o Windows Server 2008 e o Windows Vista Service Pack 1, primeiro tem de instalar a [Correção KB971800](http://go.microsoft.com/fwlink/p/?LinkId=231239) nesses computadores.  

    > [!NOTE]  
    >  Para mais informações sobre perfis de rede, consulte a documentação do Windows.  

    -   **Ativar a Firewall do Windows**  

        > [!NOTE]  
        >  Se **Ativar a Firewall do Windows** não estiver ativado, as outras definições nesta página do assistente ficam indisponíveis.  

    -   **Bloquear todas as ligações recebidas, incluindo as que se encontram na lista de programas permitidos**  

    -   **Notificar o utilizador quando a Firewall do Windows bloquear um programa novo**  

6.  Na página **Resumo** do assistente, reveja as ações a executar e conclua o assistente.  

7.  Certifique-se de que a nova política de Firewall do Windows é apresentada na lista **Políticas de Firewall do Windows** .  

##  <a name="BKMK_Assign"></a> Para implementar uma política de Firewall do Windows  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na **ativos e compatibilidade** área de trabalho, expanda **Endpoint Protection**e, em seguida, clique em **políticas de Firewall do Windows**.  

3.  Na lista **Políticas de Firewall do Windows** , selecione a política de Firewall do Windows que pretende implementar.  

4.  No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.  

5.  Na caixa de diálogo **Implementar Política de Firewall do Windows** , especifique a coleção à qual pretende atribuir esta política de Firewall do Windows e especifique um agendamento de atribuição. A política de Firewall do Windows avalia a compatibilidade, utilizando este agendamento e as definições de Firewall do Windows nos clientes para reconfigurar, de modo a corresponder à política de Firewall do Windows.  

6.  Clique em **OK** para fechar a caixa de diálogo **Implementar Política de Firewall do Windows** e para implementar a política de Firewall do Windows.  

    > [!IMPORTANT]  
    >  Ao implementar uma política de Firewall do Windows numa coleção, esta política é aplicada a computadores numa ordem aleatória durante um período de 2 horas, para evitar sobrecarregar a rede.

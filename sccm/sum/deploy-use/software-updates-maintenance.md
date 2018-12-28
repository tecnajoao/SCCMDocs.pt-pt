---
title: Manutenção das atualizações de software
titleSuffix: Configuration Manager
description: Para a manutenção de atualizações no Configuration Manager, pode agendar a tarefa de limpeza do WSUS ou pode executá-lo manualmente.
author: aczechowski
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: d2196890070aa842ac58bc127af8aaa876640ec4
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417035"
---
# <a name="software-updates-maintenance"></a>Manutenção das atualizações de software

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode agendar e executar as tarefas de limpeza do WSUS a partir da consola do Configuration Manager a partir das propriedades do componente de ponto de atualização de Software. Quando seleciona para executar a tarefa de limpeza do WSUS, ele será executado após a próxima sincronização de atualizações de software.  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>Para agendar e executar a tarefa de limpeza do WSUS 
Agende a tarefa de limpeza do WSUS ao executar os seguintes passos:   

1.  Na consola do Configuration Manager, navegue até **Administration** > **descrição geral** > **configuração do Site**  >   **Sites**. 
2. Selecione o site no topo da hierarquia do Configuration Manager. 

3.  Clique em **Configurar Componentes do Site** no grupo **Definições** e, em seguida, clique em **Ponto de Atualização de Software** para abrir as Propriedades do Componente do Ponto de Atualização de Software.  

4. Reveja os **comportamento de substituição**. Modificar o comportamento se for necessário. 
![captura de ecrã de comportamento de substituição](media/sccm-supersedence-behavior.PNG)

5.  Clique nas **regras de substituição** separador, selecione **Assistente de limpeza do WSUS executar**. Na versão 1806, a opção foi mudada para **limpeza de WSUS executar após a sincronização**. 
 
6. Clique em **OK** (clique em **fechar** se estiver a executar a versão 1806).

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>Comportamento de limpeza do WSUS na versão 1802 e anterior
Antes de 1806 de versão do Configuration Manager, a opção de limpeza do WSUS é executado o item seguinte: 
- O **expirado atualizações** opção a partir do Assistente de limpeza do WSUS no servidor dos WSUS do site de nível superior apenas. 
![WSUS expirou a captura de ecrã de limpeza de atualização](media/wsus-cleanup-expired.PNG)

-  Uma limpeza para itens de configuração de atualização de software na base de dados do Configuration Manager ocorre a cada sete dias e remove desnecessárias atualizações a partir da consola. 
   - Este limpeza não remover atualizações expiradas da consola do Configuration Manager se serem atualmente implementadas. 

Manutenção adicional ainda é necessária na base de dados do WSUS nível superior e todas as outras WSUS bases de dados no ambiente. Para obter mais informações e instruções, consulte [o guia completo para manutenção Microsoft WSUS e do Configuration Manager SUP](https://blogs.technet.microsoft.com/configurationmgr/2016/01/26/the-complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maintenance/) postagem de blog. 


## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>Comportamento de limpeza WSUS a partir da versão 1806
A opção de limpeza WSUS a partir da versão 1806, ocorre após cada sincronização e faz os seguintes itens de limpeza: <!--1357898 -->
- O **expirado atualizações** opção para servidores WSUS nas ACs e sites primários.
    - Servidores do WSUS para sites secundários, não executar a limpeza do WSUS para atualizações expiradas. 
- O Configuration Manager cria uma lista de atualizações substituídas da sua base de dados. A lista baseia-se do comportamento de substituição nas propriedades do componente de ponto de atualização de Software. 
    - Os itens de configuração de atualização satisfaçam os critérios de comportamento de substituição são expirou na consola do Configuration Manager.
    - As atualizações serão recusadas no WSUS para ACs e sites primários, mas não para os sites secundários.
- Uma limpeza para itens de configuração de atualização de software na base de dados do Configuration Manager ocorre a cada sete dias e remove desnecessárias atualizações a partir da consola. 
    - Este limpeza não remover atualizações expiradas da consola do Configuration Manager se serem atualmente implementadas. 

> [!NOTE]
> Os "meses a aguardar antes de uma atualização substituída expirar" baseia-se a data de criação da atualização substituta. Por exemplo, se usar 2 meses para esta definição, em seguida, as atualizações que tem sido substituídas serão recusou-se no WSUS e expirou no Configuration Manager, quando a atualização superceding é 2 meses antigos. 

Toda a manutenção de WSUS tem de ser executada manualmente nas bases de dados do site secundário WSUS. O seguinte procedimento **Assistente de limpeza do WSUS Server** opções não são executadas no ACs e sites primários:

- Não utilizadas atualizações e revisões de atualização
- Computadores não entrar em contato com o servidor
- Ficheiros de atualização desnecessários

  Para obter mais informações e instruções, consulte [o guia completo para manutenção Microsoft WSUS e do Configuration Manager SUP](https://blogs.technet.microsoft.com/configurationmgr/2016/01/26/the-complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maintenance/) postagem de blog. 

## <a name="updates-cleanup-log-entries"></a>Entradas de registo de limpeza de atualizações
 
Pode verificar esta limpeza ao rever o Wsyncmgr para as seguintes entradas: 
  - O declínio de atualizações substituídas no WSUS está concluído quando vir esta entrada de registo: `Cleanup processed <number> total updates and declined <number>`
  - A limpeza do WSUS está a ser iniciado quando vir esta entrada: `Calling WSUS Cleanup.`
  - A limpeza do WSUS para atualizações expiradas estiver concluída, quando vir esta entrada: `Successfully completed WSUS Cleanup.`
  - O Gestor de configuração expirou atualizações de limpeza de itens de configuração está a ser iniciado quando vir esta entrada: `Deleting old expired updates...`
  - A limpeza de itens de configuração de atualizações expiradas do Configuration Manager estiver concluída, quando vir esta entrada: `Deleted <number> expired updates total`

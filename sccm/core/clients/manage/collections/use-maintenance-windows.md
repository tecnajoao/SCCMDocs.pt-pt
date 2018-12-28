---
title: Utilizar janelas de manutenção
titleSuffix: Configuration Manager
description: Utilize coleções e janelas de manutenção para gerir clientes no System Center Configuration Manager de forma eficaz.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8e81c1b5f5898c00d004cbf903bee2eff41fdd4e
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421115"
---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>Como utilizar janelas de manutenção no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Janelas de manutenção permitem-lhe definir um período de tempo quando podem ser executadas operações do Configuration Manager numa coleção de dispositivos. Utilizar janelas de manutenção para ajudar a garantir que as alterações ocorrem durante períodos que não afetam a produtividade de configuração do cliente. A partir do Configuration Manager versão 1806, os utilizadores podem ver quando a sua próxima janela de manutenção é do **estado de instalação** separador a **Centro de Software**. <!--1358131-->

 As seguintes operações suportam janelas de manutenção:  

- Implementações de software  

- Implementações de atualizações de software  

- Avaliação e implementação das definições de compatibilidade  

- Implementações do sistema operativo  

- Implementações da sequência de tarefas  

  Configurar janelas de manutenção com uma data de início, uma para o início e de fim tempo e um padrão de periodicidade. A duração máxima de uma janela tem de ser inferior a 24 horas. Por predefinição, os reinícios do computador causados por uma implementação não são permitidos fora da janela de manutenção, mas pode substituir a predefinição. Janelas de manutenção determinam apenas o tempo quando executa o programa de implementação; aplicações configuradas para transferir e executar localmente podem transferir conteúdo fora da janela.  

  Quando um computador cliente for membro de uma coleção de dispositivos que tenha uma janela de manutenção, um programa de implementação é executado apenas se o máximo permitido de tempo de execução não ultrapassar a duração configurada para a janela. Se o programa falhar a execução, é gerado um alerta e a implementação é executada novamente durante a próxima janela de manutenção agendada com tempo disponível.  

## <a name="using-multiple-maintenance-windows"></a>Utilizar várias janelas de manutenção  
 Quando um computador cliente for membro de várias coleções de dispositivos com janelas de manutenção, estas regras aplicam-se:  

- Se as janelas de manutenção não se sobreponham, eles são tratados como duas janelas de manutenção independentes.  

- Se as janelas de manutenção se sobrepuserem, eles são tratados como uma janela de manutenção única que abrange o período de tempo coberto por ambas as janelas de manutenção. Por exemplo, se duas janelas, cada uma hora de duração, se sobrepusessem por 30 minutos, a duração efetiva da janela de manutenção seria de 90 minutos.  

  Quando um utilizador inicia a instalação de uma aplicação do Centro de Software, a aplicação é instalada imediatamente, independentemente das janelas de manutenção.  

  Se uma implementação de aplicação **Necessária** atingir o prazo de instalação durante as horas fora de expediente configuradas pelo utilizador no Centro de Software, a aplicação será instalada. 

### <a name="how-to-configure-maintenance-windows"></a>Como configurar janelas de manutenção  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade**>  **coleções de dispositivos**.  

3.  Na **coleções de dispositivos** , selecione uma coleção. Não é possível criar janelas de manutenção para o **todos os sistemas** coleção.  

4.  Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

5.  Na **Windows de manutenção** separador da  **&lt;nome da coleção\> propriedades** caixa de diálogo caixa, escolha o **New** ícone.  

6.  Concluir o  **&lt;novos\> agenda** caixa de diálogo.  

7.  Fazer uma seleção a partir da **aplicar esta agenda a** na lista pendente.  

8.  Escolher **OK** e, em seguida, feche a  **&lt;nome da coleção\> propriedades** caixa de diálogo.  

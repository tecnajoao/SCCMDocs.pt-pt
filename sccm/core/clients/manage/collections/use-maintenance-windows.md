---
title: Utilizar janelas de manutenção
titleSuffix: Configuration Manager
description: Utilize as coleções e janelas de manutenção para gerir clientes no System Center Configuration Manager de forma eficaz.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18a870b111b141cb9b95664a2f66403ea37cb99e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332530"
---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>Como utilizar janelas de manutenção no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Janelas de manutenção permitem-lhe definir um período de tempo quando podem ser realizadas operações do Configuration Manager numa coleção de dispositivos. Pode utilizar janelas de manutenção para ajudar a garantir que as alterações ocorrem durante períodos que não afetam a produtividade de configuração do cliente.  

 As seguintes operações suportam janelas de manutenção:  

-   Implementações de software  

-   Implementações de atualizações de software  

-   Avaliação e implementação das definições de compatibilidade  

-   Implementações do sistema operativo  

-   Implementações da sequência de tarefas  

 Configurar janelas de manutenção com uma data de início, um início e fim tempo e um padrão de periodicidade. A duração máxima de uma janela tem de ser inferior a 24 horas. Por predefinição, os reinícios do computador causados por uma implementação não são permitidos fora da janela de manutenção, mas pode substituir a predefinição. Janelas de manutenção determinam apenas o tempo quando executa o programa de implementação; as aplicações configuradas para transferir e executar localmente podem transferir conteúdo fora da janela.  

 Quando um computador cliente é um membro de uma coleção de dispositivos que tenha uma janela de manutenção, um programa de implementação é executado apenas se o número máximo permitido de tempo de execução não ultrapassar a duração configurada para a janela. Se o programa falhar a execução, é gerado um alerta e a implementação é executada novamente durante a próxima janela de manutenção agendada com tempo disponível.  

## <a name="using-multiple-maintenance-windows"></a>Utilizar várias janelas de manutenção  
 Quando um computador cliente é um membro de várias coleções de dispositivos com janelas de manutenção, estas regras aplicam-se:  

-   Se as janelas de manutenção não se sobrepuserem, são tratadas como duas janelas de manutenção independentes.  

-   Se as janelas de manutenção se sobrepuserem, são tratadas como uma janela de manutenção única que abrange o período de tempo coberto por ambas as janelas de manutenção. Por exemplo, se duas janelas, cada uma hora na duração, se sobrepusessem por 30 minutos, a duração efetiva da janela de manutenção seria de 90 minutos.  

 Quando um utilizador inicia a instalação de uma aplicação do Centro de Software, a aplicação é instalada imediatamente, independentemente de quaisquer janelas de manutenção.  

 Se uma implementação de aplicação **Necessária** atingir o prazo de instalação durante as horas fora de expediente configuradas pelo utilizador no Centro de Software, a aplicação será instalada.  

### <a name="how-to-configure-maintenance-windows"></a>Como configurar janelas de manutenção  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade**>  **coleções de dispositivos**.  

3.  No **coleções de dispositivos** lista, selecione uma coleção. Não é possível criar janelas de manutenção para a coleção **Todos os Sistemas** .  

4.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

5.  No **janelas de manutenção** separador do  **&lt;nome da coleção\> propriedades** diálogo caixa, escolha o **novo** ícone.  

6.  Concluir o  **&lt;novo\> agenda** caixa de diálogo.  

7.  Fazer uma seleção do **aplicar esta agenda a** na lista pendente.  

8.  Escolha **OK** e, em seguida, feche o  **&lt;nome da coleção\> propriedades** caixa de diálogo.  

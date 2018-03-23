---
title: Criar uma implementação faseada para uma sequência de tarefas
titleSuffix: System Center Configuration Manager
description: Criar faseadas implementações de sequências de tarefas
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
caps.latest.revision: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 130d1f68638427e6ee71c5c8c9686e9050bff401
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="create-phased-deployments-for-a-task-sequence-with-system-center-configuration-manager"></a>Criar implementações faseadas de uma sequência de tarefas com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Implementações faseadas automatizam uma coordenada, sequenciada implementação da sequência de tarefas em várias coleções. Pode criar implementações faseadas com a predefinição de duas fases ou configurar manualmente a várias fases. Implementação faseada de sequências de tarefas não suporta a instalação de PXE ou suportes de dados. 

>[!NOTE]
> Implementações faseadas é uma funcionalidade de pré-lançamento introduzida no Configuration Manager 1802. <!--1356837-->

## <a name="security-scope-and-log-file-information"></a>Informações de ficheiro de registo e o âmbito de segurança

**Âmbito de segurança**:</br>
Às implementações criadas por fases implementações não são visíveis para qualquer pessoa que não tenha o **todos os** âmbito de segurança.

**Ficheiros de registo**: </br>
SMS_PhasedDeployment.log

## <a name="create-a-default-two-phased-deployment-for-a-task-sequence"></a>Criar uma implementação de duas fases para predefinido para uma sequência de tarefas

Utilize as seguintes instruções para criar uma implementação faseada. 

1. No **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.

2. Faça duplo clique na sequência de tarefas existente e selecione **criar implementação fases**. 

3. No **geral** separador, atribua a implementação faseada um nome, descrição (opcional) e selecione **criar automaticamente uma implementação de fase dois predefinido**. 

4. Preencher o **primeira coleção** e **segunda coleção** campos. Selecione **seguinte**.

5. No **definições** separador, escolha uma opção para cada uma das definições de agendamento e selecione **seguinte** quando concluir. 
    - **Critérios de êxito da primeira fase.** 
        - **Percentagem de êxito da implementação** -especifique a percentagem de dispositivos que concluem com êxito a implementação para os critérios de sucesso de fase. 
    - **As condições para a partir da segunda fase da implementação depois de concluída a primeira fase** (escolher um):
        - **Iniciar automaticamente nesta fase após um período de diferimento por (em dias)** -escolher o número de dias a aguardar antes de iniciar a segunda fase após o êxito do primeiro. 
        - **Iniciar manualmente a segunda fase da implementação** -não começar a segunda fase automaticamente após foi efetuada com êxito o primeiro. Requerer ser iniciadas manualmente. 
    - **Depois de um dispositivo é direcionado, instalar o software** (escolher um):
        - **Logo que possível** -define o prazo de instalação no dispositivo, assim que o dispositivo é visado.
        - **Prazo de tempo (em relação à hora de dispositivo é direcionado)** -conjuntos do prazo de instalação de um determinado número de dias após o dispositivo é direcionado. 

6. No **fases** separador, clique no primeiro a primeira fase, em seguida, **editar**.  Especifique **experiência de utilizador** como **notificações do utilizador** e **filtro de escrita de processamento para dispositivos Windows Embedded**. Clique em **Aplicar**.

7. Especifique **pontos de distribuição** definições para a fase no **pontos de distribuição** separador. Clique em **aplicar** e **OK**.        

8. No **fases** separador, edite a segunda fase para **experiência de utilizador** e **pontos de distribuição**. Clique em **aplicar** e **OK**.

9. Confirme as suas seleções no **resumo** separador e, em seguida, clique em **seguinte** e continuar apesar do assistente.

>[!WARNING]
>Implementações faseadas não notificá-lo se for uma implementação de sequência de tarefas [alto risco](/sccm/protect/understand/settings-to-manage-high-risk-deployments.md). 


## <a name="suspend-and-resume-phases-or-move-to-the-next-phase"></a>Suspender e retomar fases ou mova para a fase seguinte
No occasion, poderá ter de suspender uma implementação faseada manualmente, retomar uma implementação faseada suspensa ou mover para a fase seguinte. 

### <a name="move-to-the-next-phase"></a>Mover para a fase seguinte
Quando seleciona a definição **iniciar manualmente a segunda fase da implementação**, terá de iniciar a segunda fase. Utilize as seguintes instruções para mover para a segunda fase: 

1. Na consola do Configuration Manager, selecione **biblioteca de Software**, expanda **sistemas operativos**e clique em **sequências de tarefas**.
2. Realce a sequência de tarefas.
3. Clique em de **fases de implementação** separador perto da parte inferior da consola. 
4. A implementação faseada com o botão direito e selecione **mover para a fase seguinte**.
![Suspender, retomar ou mover para a fase seguinte](media/Suspend-phased-deployment.PNG)

### <a name="suspend-or-resume-a-phased-deployment"></a>Suspender ou retomar uma implementação faseada
1. Na consola do Configuration Manager, selecione **biblioteca de Software**, expanda **sistemas operativos**e clique em **sequências de tarefas**.
2. Realce a sequência de tarefas e clique em de **fases de implementação** separador perto da parte inferior da consola. 
3. Selecione a implementação faseada e clique em **suspender** ou **retomar** no Friso.

## <a name="next-steps"></a>Passos seguintes
[Criar uma sequência de tarefas personalizada](create-a-custom-task-sequence.md) </br>
[Criar uma sequência de tarefas para implementações do sistema de operativo](create-a-task-sequence-for-non-operating-system-deployments.md). 









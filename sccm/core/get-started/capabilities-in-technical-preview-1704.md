---
title: "Capacidades na pré-visualização técnica 1704 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1704."
ms.custom: na
ms.date: 4/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d7caee47ca74064630e09c1bdb94187af256d4b4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1704-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1704 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1704. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja o tópico introdutórias, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>Configurar as aplicações Android com políticas de configuração de aplicação
Pode utilizar políticas de configuração de aplicações no System Center Configuration Manager (Configuration Manager) para distribuir as definições que poderão ser necessárias quando um utilizador executa uma aplicação no Android para dispositivos de trabalho. Políticas de configuração de aplicação Android estão disponíveis apenas em dispositivos com Android para o trabalho e aplicam a aplicações aprovadas da Play para o arquivo de trabalho.

### <a name="try-it-out"></a>Experimente                 

Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **políticas de configuração de aplicação** e escolha **criar política de configuração de aplicação**. No **geral** página do assistente, pode agora **selecione um tipo de política de configuração**. Especifique a plataforma visada pela política de configuração de aplicação: **Política de configuração para Android para aplicações de trabalho**. Pode, em seguida, **Especifique pares nome / valor** ou **procure um ficheiro JSON de lista de propriedade**. A nova política de configuração de aplicação é apresentada no **biblioteca de Software** área de trabalho, no **políticas de configuração de aplicação** nós. Para associar uma política de configuração de aplicação com a implementação de um Android para a aplicação de trabalho, implementar a aplicação como faria normalmente, utilizando o procedimento a [implementar aplicações](/sccm/apps/deploy-use/deploy-applications) tópico.

## <a name="hardware-inventory-collects-secure-boot-information"></a>Inventário de hardware recolhe informações de arranque seguro
Inventário de hardware agora recolhe informações sobre se o arranque seguro está ativado nos clientes. Esta informação é armazenada no **SMS_Firmware** classe (introduzida na versão 1702) e de hardware ativado no inventário por predefinição. Para obter mais informações sobre o inventário de hardware, consulte [como configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Adicionar sequências de tarefas de subordinados a uma sequência de tarefas
Nesta versão, pode adicionar um novo passo de sequência de tarefas é executada outra sequência de tarefas, que cria uma relação principal/subordinado entre as sequências de tarefas. Isto permite-lhe criar mais sequências de tarefas modulares que pode utilizar novamente.  

Quando adicionar uma sequência de tarefas subordinados a uma sequência de tarefas, considere o seguinte:

- As sequências de tarefas principais e subordinados eficazmente são combinadas uma única política que executa o cliente.
- Não é suportada para adicionar uma sequência de tarefas de subordinados que é um elemento principal de outra sequência de tarefas.
- O ambiente é global. Por exemplo, se uma variável é definida pela sequência de tarefas principal e, em seguida, alterada pela sequência de tarefas subordinado, a variável permanece alterado mover reencaminhar. Da mesma forma, se a sequência de tarefas subordinado cria uma nova variável, a variável está disponível para os passos restantes da sequência de tarefas principal.
- Mensagens de estado são enviadas por normal para uma operação de sequência de tarefas único.
- As sequências de tarefas escreverem entradas no ficheiro smsts.log, com o novo registo de entradas que desmarque quando uma sequência de tarefas subordinado é iniciado.
- No Technical Preview para o Configuration Manager, versão 1704, se as sequências de tarefas subordinado referencia qualquer pacote e o utilizador executar principal sequência de tarefas do Centro de Software, o cliente será não encontrar o conteúdo do pacote quando a sequência de tarefas subordinado é executada. Neste cenário, tem de executar a sequência de tarefas do suporte de dados (arranque suportes de dados, PXE, etc.).  

    Se a sequência de tarefas subordinado utiliza passos como **executar linha de comandos** (sem qualquer referência de pacote), **formato**, **BitLocker**, etc., em seguida, a sequência de tarefas será executado com êxito a partir do Centro de Software.

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>Para adicionar uma sequência de tarefas subordinados a uma sequência de tarefas
1. No editor de sequência de tarefas, clique em **adicionar**, selecione **geral**e clique em **executar a sequência de tarefas**.
2. Clique em **procurar** para selecionar a sequência de tarefas subordinado.  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>Volte a carregar as imagens de arranque com a versão atual do Windows PE
Quando executa **atualizar pontos de distribuição** numa imagem de arranque selecionada, agora, pode escolher recarregar a versão mais recente do Windows PE (a partir do diretório de instalação do Windows ADK) na imagem de arranque. O **geral** página do assistente fornece informações sobre a versão do Windows ADK instalada no servidor do site, a versão do Windows ADK partir do qual o Windows PE foi utilizado na imagem de arranque e a versão do cliente do Configuration Manager. Pode utilizar estas informações para ajudar a decidir se pretende recarregar a imagem de arranque. Além disso, uma nova coluna (**versão de cliente**) foi adicionado ao ver as imagens de arranque no **imagens de arranque** nó para saber qual a versão do cliente do Configuration Manager utiliza de cada imagem de arranque.

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>Recarregar uma imagem de arranque com a versão atual do Windows PE

1. Na consola do Configuration Manager, vá para **biblioteca de Software** > **sistemas operativos** > **imagens de arranque**.
2. Selecione uma imagem de arranque e clique em **atualizar pontos de distribuição**.
3. No **geral** página do assistente, selecione **imagem de arranque de recarregar a utilizar a versão atual do Windows PE do Windows ADK instalado**.

## <a name="improvements-to-operating-system-deployment"></a>Melhorias para implementação do sistema operativo
Efetuamos as seguintes melhorias para implementação do sistema operativo, que eram o resultado dos seus comentários de voz do utilizador.

- [Novo **versão do SO** coluna para imagens de sistema operativo](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f): Iremos adicionou uma nova coluna com o nome **versão do SO** para apresentar a versão do sistema operativo da imagem quando visualiza informações no **imagens do sistema operativo** e **pacotes de atualização do sistema operativo** nós. Apenas a versão do índice do primeiro o. WIM é apresentado. Vá para o **detalhes** separador para a imagem rever as versões do sistema operativo para outros índices.

- [Início de sessão mais eficiente em Smsts.log](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless): A partir desta versão, iremos deixam de entradas de escrita para o ficheiro smsts.log para CCM_CIVersionInfo.PolicyID informações. Antes desta versão, pode haver um grande número de entradas com estas informações, que efetuadas difíceis de encontrar informações mais relevantes no ficheiro de registo.

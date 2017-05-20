---
title: "Capacidades na pré-visualização técnica 1704 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1704."
ms.custom: na
ms.date: 4/21/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: ae008c91a7387ba76f2bfac13f8feb489a0cc558
ms.openlocfilehash: d7caee47ca74064630e09c1bdb94187af256d4b4
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1704-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1704 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1704. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>Configurar as aplicações Android com as políticas de configuração de aplicação
Pode utilizar as políticas de configuração da aplicação no System Center Configuration Manager (Configuration Manager) para distribuir as definições que poderão ser necessárias quando um utilizador executa uma aplicação no Android para dispositivos de trabalho. Políticas de configuração de aplicação Android estão disponíveis apenas em dispositivos que executam o Android para trabalhar e aplicam a aplicações aprovadas da Play para o arquivo de trabalho.

### <a name="try-it-out"></a>Experimente                 

Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **políticas de configuração de aplicação** e escolha **criar política de configuração de aplicação**. No **geral** página do assistente, pode agora **selecionar um tipo de política de configuração**. Especifique a plataforma direcionada pela política de configuração de aplicação: **Política de configuração para Android para aplicações de trabalho**. Pode, em seguida, **especificar pares valor / nome** ou **procure um ficheiro JSON da lista de propriedade**. A nova política de configuração de aplicação é apresentada no **biblioteca de Software** área de trabalho, no **políticas de configuração de aplicação** nó. Para associar uma política de configuração de aplicação com a implementação do Android para a aplicação de trabalho, a implementar a aplicação, como faria normalmente, utilizando o procedimento apresentado a [implementar aplicações](/sccm/apps/deploy-use/deploy-applications) tópico.

## <a name="hardware-inventory-collects-secure-boot-information"></a>Inventário de hardware recolhe informações de arranque seguro
Inventário de hardware agora recolhe informações sobre se o arranque seguro está ativado nos clientes. Estas informações são armazenadas no **SMS_Firmware** classe (introduzido na versão 1702) e de hardware ativada no inventário por predefinição. Para obter mais informações sobre o inventário de hardware, consulte o artigo [como configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Adicionar sequências de tarefas do subordinado a uma sequência de tarefas
Nesta versão, pode adicionar um novo passo de sequência de tarefas que é executado outro sequência de tarefas, que cria uma relação principal/subordinado entre as sequências de tarefas. Isto permite-lhe criar mais sequências de tarefas modular que pode utilizar novamente.  

Quando adiciona uma sequência de tarefas subordinado a uma sequência de tarefas, considere o seguinte:

- As sequências de tarefas principais e subordinados eficazmente são combinadas uma única política que executa o cliente.
- Não é suportada para adicionar uma sequência de tarefas de subordinados que é um elemento principal de outro sequência de tarefas.
- É global para o ambiente. Por exemplo, se uma variável é definida pela sequência de tarefas principal e, em seguida, alterada pela sequência de tarefas subordinados, a variável permanece alteradas mover reencaminhar. Do mesmo modo, se a sequência de tarefas de subordinados cria uma nova variável, a variável está disponível para os passos restantes na sequência de tarefas principal.
- Mensagens de estado são enviadas por normal para uma operação de sequência de tarefas único.
- As sequências de tarefas escreverem entradas para o ficheiro smsts log, com o novo registo de entradas que a tornam limpar quando uma sequência de tarefas subordinado é iniciado.
- A pré-visualização técnica para o Configuration Manager, versão 1704, se as sequências de tarefas de subordinados referencia qualquer pacote e executar o elemento principal de sequência de tarefas a partir do Centro de Software, o cliente não encontrará o conteúdo do pacote quando a sequência de tarefas subordinado é executada. Neste cenário, tem de executar a sequência de tarefas a partir do suporte de dados (arranque suportes de dados, PXE, etc.).  

    Se a sequência de tarefas de subordinados utiliza passos como **executar linha de comandos** (sem qualquer referência de pacote), **formato**, **BitLocker**, etc., em seguida, a sequência de tarefas será executado com êxito a partir do Centro de Software.

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>Para adicionar uma sequência de tarefas subordinado a uma sequência de tarefas
1. No editor de sequência de tarefas, clique em **adicionar**, selecione **geral**e clique em **sequência de tarefas executar**.
2. Clique em **procurar** para selecionar a sequência de tarefas de subordinados.  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>Recarregar imagens de arranque com a versão atual do Windows PE
Quando executa **atualizar pontos de distribuição** na imagem de arranque selecionada, agora, pode escolher recarregar a versão mais recente do Windows PE (a partir do diretório de instalação Windows ADK) na imagem de arranque. O **geral** página do assistente fornece informações sobre a versão do Windows ADK instalada no servidor do site, a versão do Windows ADK a partir do qual o Windows PE foi utilizado na imagem de arranque e a versão do cliente do Configuration Manager. Pode utilizar estas informações para ajudar a decidir se pretende recarregar a imagem de arranque. Além disso, uma nova coluna (**versão do cliente**) foi adicionado ao ver imagens de arranque no **imagens de arranque** nó para saber qual a versão do cliente do Configuration Manager utiliza de cada imagem de arranque.

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>Carregue uma imagem de arranque com a versão atual do Windows PE

1. Na consola do Configuration Manager, aceda a **biblioteca de Software** > **sistemas operativos** > **imagens de arranque**.
2. Selecione uma imagem de arranque e clique em **atualizar pontos de distribuição**.
3. No **geral** página do assistente, selecione **imagem de arranque de recarregar a utilizar a versão atual do Windows PE a partir do Windows ADK instalado**.

## <a name="improvements-to-operating-system-deployment"></a>Melhorias na implementação do sistema operativo
Vamos efetuar os seguintes melhoramentos à implementação de sistema operativo, que eram o resultado dos seus comentários de voz do utilizador.

- [Novo **versão do SO** coluna para imagens do sistema operativo](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f): Adicionámos uma nova coluna com o nome **versão do SO** para apresentar a versão do sistema operativo da imagem quando visualiza informações no **imagens do sistema operativo** e **pacotes de atualização do sistema operativo** nós. Apenas a versão do índice primeiro na. WIM é apresentado. Aceda ao **detalhes** separador para a imagem rever as versões do sistema operativo para outros índices.

- [Registo mais eficiente no smsts](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless): A partir nesta versão, iremos já não são entradas de escrita para o ficheiro smsts log para obter informações de CCM_CIVersionInfo.PolicyID. Antes desta versão, podem existir muitas entradas com estas informações, que efetuadas difíceis de encontrar informações mais relevantes no ficheiro de registo.


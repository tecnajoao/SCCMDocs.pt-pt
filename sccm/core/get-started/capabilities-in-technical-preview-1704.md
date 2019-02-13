---
title: Funcionalidades no Technical Preview 1704
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1704.
ms.date: 4/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: e01270a5666e06f7072c4680398f5c5b590208b3
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135141"
---
# <a name="capabilities-in-technical-preview-1704-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1704 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1704. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.    


**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>Configurar aplicações Android com políticas de configuração de aplicação
Pode utilizar políticas de configuração de aplicações no System Center Configuration Manager (Gestor de configuração) para distribuir as definições que poderão ser necessárias quando um utilizador executa uma aplicação no Android para dispositivos de trabalho. Políticas de configuração de aplicação Android estão disponíveis apenas em dispositivos Android for Work e aplicam-se para aplicações aprovadas a partir da Play for Work store.

### <a name="try-it-out"></a>Experimentar                 

Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **políticas de configuração de aplicação** e escolher **criar política de configuração de aplicação**. Sobre o **gerais** página do assistente, pode agora **selecione um tipo de política de configuração**. Especifique a plataforma visada pela política de configuração de aplicação: **Política de configuração para Android para aplicações de trabalho**. Pode, em seguida, **Especifique pares nome / valor** ou **procure um ficheiro JSON de lista de propriedade**. A nova política de configuração de aplicações é mostrada na **biblioteca de Software** área de trabalho, na **políticas de configuração de aplicação** nó. Para associar uma política de configuração de aplicação com a implementação de uma aplicação Android for Work, a implementar a aplicação, tal como faria normalmente utilizando o procedimento a [implementar aplicações](/sccm/apps/deploy-use/deploy-applications) tópico.

## <a name="hardware-inventory-collects-secure-boot-information"></a>Inventário de hardware recolhe informações de arranque seguro
Agora o inventário de hardware recolhe informações sobre se o arranque seguro está ativado nos clientes. Essas informações são armazenadas no **SMS_Firmware** classe (introduzida na versão 1702) e ativado no hardware de inventário por predefinição. Para obter mais informações sobre o inventário de hardware, consulte [como configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Adicionar sequências de tarefas filho a uma sequência de tarefas
Nesta versão, pode adicionar um novo passo de sequência de tarefas que executa outra sequência de tarefas, que cria uma relação de pai/filho entre as sequências de tarefas. Isto permite-lhe criar mais sequências de tarefas modulares que pode utilizar novamente.  

Quando adicionar uma sequência de tarefas filho a uma sequência de tarefas, considere o seguinte:

- As sequências de tarefas principais e subordinados com eficiência são combinadas numa única política que executa o cliente.
- Não é suportada para adicionar uma sequência de tarefas de subordinado é um elemento principal de outra sequência de tarefas.
- O ambiente é global. Por exemplo, se uma variável é definida pela sequência de tarefas principal e, em seguida, foi alterada pela sequência de tarefas filho, o variável permanece alterado mover para a frente. Da mesma forma, se a sequência de tarefas filho cria uma nova variável, a variável está disponível para os restantes passos da sequência de tarefa principal.
- Mensagens de estado são enviadas por normal para uma operação de sequência de tarefa única.
- As sequências de tarefas gravar entradas para o ficheiro smsts log, com o novo log entradas que ficar claro quando uma sequência de tarefas de subordinado é iniciado.
- No Technical Preview no Configuration Manager, versão 1704, se as sequências de tarefas filho faz referência a qualquer pacote e executar o elemento principal de sequência de tarefas do Centro de Software, o cliente será não encontrar o conteúdo do pacote ao executar a sequência de tarefas filho. Neste cenário, tem de executar a sequência de tarefas do suporte de dados (inicializar dados de arranque PXE, etc.).  

    Se a sequência de tarefas filho utiliza passos, como **executar linha de comandos** (sem qualquer referência de pacote), **formato**, **BitLocker**, etc., em seguida, a sequência de tarefas será executado com êxito no Centro de Software.

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>Para adicionar uma sequência de tarefas filho a uma sequência de tarefas
1. No editor de sequência de tarefas, clique em **Add**, selecione **gerais**e clique em **executar a sequência de tarefas**.
2. Clique em **procurar** para selecionar a sequência de tarefas filho.  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>Volte a carregar imagens de arranque com a versão atual do Windows PE
Quando executa **atualizar pontos de distribuição** numa imagem de arranque selecionada, pode agora escolher recarregar a versão mais recente do Windows PE (a partir do diretório de instalação do Windows ADK) na imagem de arranque. O **gerais** página do assistente fornece informações sobre a versão do Windows ADK instalada no servidor do site, a versão do Windows ADK partir do qual o Windows PE foi utilizada na imagem de arranque e a versão do Configuration Manager cliente. Pode usar essas informações para ajudar a decidir se pretende recarregar a imagem de arranque. Além disso, uma nova coluna (**versão de cliente**) foi adicionado quando visualizar imagens de arranque no **imagens de arranque** nó para saber qual versão do cliente do Configuration Manager utiliza de cada imagem de arranque.

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>Recarregar uma imagem de arranque com a versão atual do Windows PE

1. Na consola do Configuration Manager, aceda a **biblioteca de Software** > **sistemas operativos** > **imagens de arranque**.
2. Selecione uma imagem de arranque e clique em **atualizar pontos de distribuição**.
3. Sobre o **gerais** página do assistente, selecione **imagem de arranque de recarregar a utilizar a versão atual do Windows PE do Windows ADK instalado**.

## <a name="improvements-to-operating-system-deployment"></a>Melhorias para implementação do sistema operativo
Que fizemos as seguintes melhorias para implementação do sistema operativo, que foram o resultado dos seus comentários de voz do utilizador.

- [Novos **versão do SO** coluna para imagens do sistema operativo](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f): Adicionámos uma nova coluna chamada **versão do SO** para apresentar a versão do sistema operativo para a imagem quando ver as informações a **imagens do sistema operativo** e **sistema operativo Pacotes de atualização** nós. Apenas a versão do primeiro índice no. WIM é apresentado. Vá para o **detalhes** separador para a imagem rever as versões do sistema operativo para outros índices.

- [O registo mais eficiente no smsts](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless): A partir desta versão, não estão mais entradas de escrita para o ficheiro smsts log para obter informações de CCM_CIVersionInfo.PolicyID. Antes desta versão, pode haver muitas entradas com essas informações, o que o tornou difícil encontrar informações mais relevantes no ficheiro de registo.

---
title: Pré-visualização técnica 1711 | Documentos da Microsoft
titleSuffix: Configuration Manager
description: Saiba mais sobre funcionalidades disponíveis na versão 1711 pré-visualização técnica do System Center Configuration Manager.
ms.date: 11/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 645f41a7bad4bd9365c9ec9d51e2567ae270385a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123302"
---
# <a name="capabilities-in-technical-preview-1711-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1711 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1711. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para a utilização de um técnico de pré-visualização, como atualizar entre as versões e como fornecer comentários sobre os recursos de uma technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos neste Technical Preview:**
- **Suporte para Windows 10, versão 1709 (também conhecido como o Fall Creators Update)**.  Começando com esta versão do Windows, o suporte de dados do Windows inclui várias edições. Ao configurar uma sequência de tarefas para utilizar um pacote de atualização do sistema operativo ou a imagem do sistema operativo, certifique-se de que selecione um [edition que é suportada para utilização pelo Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).
- **Atualização para uma nova versão de pré-visualização falha quando tem um servidor de site em modo passivo**. Quando executa uma versão de pré-visualização que tem um [servidor do site primário em modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), tem de desinstalar o servidor do site de modo passivo antes de poder atualizar com êxito o site de pré-visualização para esta nova versão de pré-visualização. Pode reinstalar o servidor do site de modo passivo após a atualização do seu site estiver concluída.

  Para desinstalar o servidor do site de modo passivo:
  1. Na consola, aceda a **Administration** > **descrição geral** > **configuração do Site** > **servidores e sites Funções do sistema**e, em seguida, selecione o servidor de site de modo passivo.
  2. Na **funções do sistema de sites** painel, clique direito na **servidor do Site** função e, em seguida, escolha **remover função**.
  3. Faça duplo clique no servidor do site de modo passivo e, em seguida, escolha **eliminar**.
  4. Depois de desinstala o servidor do site, no servidor do site primário active reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.

**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-to-run-task-sequence"></a>Melhorias para executar a sequência de tarefas
<!-- 1261338 -->

Este technical preview irá melhorar o passo de sequência de tarefas executar. Melhoramentos incluem os seguintes itens:

 - Suporte para todos os cenários de implementação do sistema operativo do Centro de Software, PXE e suporte de dados.
 - Melhorias para ações como copiar, importar, exportar e aviso durante a eliminação de objetos da consola.
 - Suporte para o **criar conteúdo pré-configurado** assistente.
 - Integração com verificação de implementação.
 - O passo de sequência de tarefas executar agora pode ser utilizado em vários níveis de sequências de tarefas, não apenas uma relação de único principal-subordinado. Relações de múltiplos níveis aumentar a complexidade, use com cautela. Esses relacionamentos ainda estão marcados para referências circulares.

### <a name="try-it-out"></a>Experimente!  

Experimente concluir as seguintes tarefas e, em seguida, envie-nos **comentários** partir do **home page** separador do friso para nos informar como correu:

1. No editor de sequência de tarefas, clique em **Add**, selecione **gerais**e clique em **executar a sequência de tarefas**.
2. Clique em **procurar** para selecionar a sequência de tarefas filho.

## <a name="allow-user-interaction-when-installing-an-application----1356976---"></a>Permitir a interação do usuário ao instalar um aplicativo <!-- 1356976 -->

Com esta pré-visualização, pode permitir que um utilizador final interagir com uma instalação da aplicação durante a execução da sequência de tarefas. Por exemplo, execute um processo de configuração que solicita ao usuário final para várias opções. Alguns instaladores de aplicativo não podem ter silenced avisos do utilizador ou o processo de instalação pode exigir valores de configuração específicas apenas conhecidas do usuário. Esta funcionalidade permite-lhe lidar com esses cenários de instalação.

### <a name="try-it-out"></a>Experimente!

Experimente concluir as seguintes tarefas e, em seguida, envie **comentários** partir a **home page** separador do friso para nos informar como correu:

1.  Criar ou editar uma aplicação. Para obter mais informações, consulte [criar aplicações com o System Center Configuration Manager](/sccm/apps/deploy-use/create-applications).

    a. Escolha o **experiência de utilizador** separador a **Windows Installer (\*arquivo msi) propriedades**.

    b. Selecione **instalar para o sistema** para **comportamento de instalação**.

    c. Selecione **se deve ou não um usuário é conectado** para **logon requisito**.

    d. Selecione **Normal** para **visibilidade do programa de instalação**. Pode selecionar entre três opções: **Minimizado**, **Normal**, ou **maximizada**.

    e. Selecione o **permitir que os utilizadores interajam com a instalação do programa** caixa.

2.  Criar ou editar uma sequência de tarefas para instalar a aplicação através da **instalar aplicação** passo. Para obter mais informações, consulte [instalar aplicação](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication) no [passos de sequência de tarefas no System Center Configuration Manager](/sccm/osd/understand/task-sequence-steps).

    a. Geração de imagens sequência de tarefas após o passo de configuração do Windows e o Configuration Manager.

    b. No local a sequência de tarefas de atualização no grupo de pós-processamento.

3.  Implemente a sequência de tarefas para um cliente.
4.  Instale a sequência de tarefas a partir do Centro de Software.

Durante o progresso da sequência de tarefas, é apresentada a interface de instalação de aplicações no dispositivo do utilizador final de destino. O progresso da sequência de tarefas coloca em pausa até que o utilizador final conclua o fluxo de trabalho de instalação do aplicativo.

### <a name="install-using-the-wizard"></a>Instalar utilizando o Assistente

Também pode utilizar esta funcionalidade quando implementar uma aplicação utilizando o assistente.

1. Criar ou editar uma aplicação.
2. Implemente a aplicação a um cliente.
3. Instale a aplicação a partir do Centro de Software. A interface de instalação do aplicativo deve aparecer. O utilizador final deve seguir o Assistente de instalação do aplicativo e a aplicação será instalada com êxito.




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Passos Seguintes
Para obter informações sobre a instalação ou a atualizar o ramo de pré-visualização técnica, veja [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    

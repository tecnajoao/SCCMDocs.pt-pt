---
title: "Pré-visualização técnica 1711 | Microsoft Docs"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades disponíveis na versão de pré-visualização técnica 1711 para o System Center Configuration Manager."
ms.custom: na
ms.date: 11/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: erikje
ms.author: erikje
manager: angrobe
ms.openlocfilehash: e970dff4ea295694fcc5cf80e238baf2c9d081b5
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="capabilities-in-technical-preview-1711-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1711 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1711. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos neste Technical Preview:**
-   **Suporte para Windows 10, versão 1709 (também conhecido como a atualização de criadores de reversão)**.  A partir desta versão do Windows, o suporte de dados do Windows inclui várias edições. Quando configurar uma sequência de tarefas para utilizar um pacote de atualização do sistema operativo ou a imagem do sistema operativo, é necessário selecionar um [edição que é suportada para utilização pelo Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).
-   **Falha de atualização para uma nova versão de pré-visualização quando tiver um servidor de site no modo passivo**. Quando executa uma versão de pré-visualização que tem um [servidor do site primário em modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), tem de desinstalar o servidor do site de modo passivo antes de poder atualizar com êxito o site de pré-visualização para esta nova versão de pré-visualização. Pode reinstalar o servidor do site de modo passivo depois do seu site é concluída a atualização.

  Para desinstalar o servidor do site de modo passivo:
  1. Na consola, aceda a **administração** > **descrição geral** > **configuração do Site** > **servidores e funções de sistema de sites**e, em seguida, selecione o servidor de site de modo passivo.
  2. No **funções do sistema de sites** painel, clique direito no **servidor do Site** função e, em seguida, escolha **remover função**.
  3. Faça duplo clique no servidor do site de modo passivo e, em seguida, escolha **eliminar**.
  4. Depois de desinstala o servidor do site, no servidor do site primário Active Directory reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-to-run-task-sequence"></a>Melhoramentos para executar a sequência de tarefas
<!-- 1261338 -->

Este technical preview irá melhorar o passo de sequência de tarefas executar. Melhoramentos incluem os seguintes itens:

 - Suporte para todos os cenários de implementação de sistema operativo no Centro de Software, PXE e suporte de dados.
 - Melhorias na consola ações como copiar, importar, exportar e aviso durante a eliminação de objetos.
 - Suporte para o **criar conteúdo pré-configurado** assistente.
 - Integração com verificação de implementação.
 - O passo de sequência de tarefas executar pode agora ser utilizado em vários níveis de sequências de tarefas, não apenas uma relação de único principal-subordinado. Relações de múltiplos níveis aumente a complexidade, por isso, utilize com cuidado. Estas relações ainda são verificados relativamente à referências circulares.

### <a name="try-it-out"></a>Experimente!  

Experimente concluir as seguintes tarefas e, em seguida, envie-nos **comentários** do **home page** separador do friso para nos informar como correu:

1. No editor de sequência de tarefas, clique em **adicionar**, selecione **geral**e clique em **executar a sequência de tarefas**.
2. Clique em **procurar** para selecionar a sequência de tarefas subordinado.

## <a name="allow-user-interaction-when-installing-an-application----1356976---"></a>Permitir interação do utilizador quando instalar uma aplicação<!-- 1356976 -->

Com esta pré-visualização, pode permitir que um utilizador final interagir com a instalação de uma aplicação durante a execução da sequência de tarefas. Por exemplo, execute um processo de configuração que pede ao utilizador final para várias opções. Alguns programas de instalação da aplicação não podem ter silenciados avisos do utilizador ou o processo de instalação pode necessitar de valores de configuração específicas conhecidos apenas ao utilizador. Esta funcionalidade permite-lhe lidar com estes cenários de instalação.

### <a name="try-it-out"></a>Experimente!

Experimente concluir as seguintes tarefas e, em seguida, enviar **comentários** do **home page** separador do friso para nos informar como correu:

1.  Criar ou editar uma aplicação. Para obter mais informações, consulte [criar aplicações com o System Center Configuration Manager](/sccm/apps/deploy-use/create-applications).

    a. Escolha o **experiência de utilizador** separador o **do Windows Installer (\*ficheiro msi) propriedades**.

    b. Selecione **instalar para o sistema** para **comportamento de instalação**.

    c. Selecione **se deve ou não um utilizador iniciado** para **iniciar sessão requisito**.

    d. Selecione **Normal** para **visibilidade do programa de instalação**. Pode selecionar um dos três opções: **Minimizado**, **Normal**, ou **maximizado**.

    e. Selecione o **permitir que os utilizadores interajam com a instalação do programa** caixa.

2.  Criar ou editar uma sequência de tarefas para instalar a aplicação a utilizar o **instalar aplicação** passo. Para obter mais informações, consulte [instalar aplicação](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication) no [passos de sequência de tarefas no System Center Configuration Manager](/sccm/osd/understand/task-sequence-steps).

    a. Processamento de imagens sequência de tarefas após o passo configurar Windows e Configuration Manager.

    b. No local a sequência de tarefas de atualização no grupo de pós-processamento.

3.  Implemente a sequência de tarefas para um cliente.
4.  Instale a sequência de tarefas a partir do Centro de Software.

Durante o progresso da sequência de tarefas, a interface de instalação da aplicação é apresentado no dispositivo do utilizador final de destino. O progresso da sequência de tarefas interrompe até que o utilizador final conclui o fluxo de trabalho de instalação de aplicações.

### <a name="install-using-the-wizard"></a>Instalar utilizando o Assistente

Também pode utilizar esta funcionalidade quando implementar uma aplicação utilizando o assistente.

1. Criar ou editar uma aplicação.
2. Implemente a aplicação para um cliente.
3. Instale a aplicação a partir do Centro de Software. A interface de instalação da aplicação deve aparecer. O utilizador final deve seguir o Assistente de instalação da aplicação e a aplicação será instalada com êxito.

## <a name="new-compliance-policy-options-for-windows-10"></a>Novas opções de política de conformidade para o Windows 10
Seguem-se novas políticas de conformidade pode configurar em dispositivos Windows 10.
- **Requerer Firewall**.  Especifique se um dispositivo tem de ter uma firewall ativada e monitorização de todas as redes.
- **Requerem controlo de conta de utilizador**. Especifique a que um dispositivo tem de ter controlo de conta de utilizador ativado.
- **Defender**:
  - **Requer o Windows Defender antivírus**.  Requer um dispositivo com o Windows Defender antivírus ativada.
  - **Versão do Windows Defender antivírus**.  Especifique a versão mínima do spyware atualizadas que um dispositivo tem de ter instalado.
  - **Exigir assinatura atual do Windows Defender antivírus**. Certifique-se de que uma assinatura de janela Defender antivírus de dispositivos está atualizada.
  - **Exigir proteção em tempo real**.  Especifique se um dispositivo tem de ter o Windows Defender antivírus em tempo real Protection ativado.
- **Sistema operativo válido compilações**.  Especifique os requisitos de compilação do sistema operativo mínimo e máximo.  

Utilize o Assistente para criar políticas de conformidade para configurar estas políticas e selecione estas novas opções quando adicionar uma regra para a política que está a configurar.  
Saiba como [criar](/sccm/mdm/deploy-use/create-compliance-policy#create-a-compliance-policy) e [implementar](/sccm/mdm/deploy-use/create-compliance-policy#deploy-a-compliance-policy) políticas de conformidade.




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Passos Seguintes
Para obter informações sobre instalar ou atualizar o ramo de pré-visualização técnica, consulte [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    

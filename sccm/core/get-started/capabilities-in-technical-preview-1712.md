---
title: "Pré-visualização técnica 1712 | Microsoft Docs"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades disponíveis na versão de pré-visualização técnica 1712 para o System Center Configuration Manager."
ms.custom: na
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 85f0b22b3dc067f6f07816ad36d23a090885f355
ms.sourcegitcommit: ed8b2438ef85c9160741ef61f9171be41dd1ae0a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/17/2017
---
# <a name="capabilities-in-technical-preview-1712-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1712 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1712. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. 

Reveja [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview) antes de instalar esta versão do technical preview. Esse artigo familiarizes, com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Problemas conhecidos neste Technical Preview:**
-   **Falha de atualização para uma nova versão de pré-visualização quando tiver um servidor de site no modo passivo**. Se tiver um [servidor do site primário em modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), em seguida, tem de desinstalar o servidor do site de modo passivo antes de atualizar para esta nova versão de pré-visualização. Pode reinstalar o servidor do site de modo passivo depois do seu site é concluída a atualização.

  Para desinstalar o servidor do site de modo passivo:
  1. Na consola do Configuration Manager, vá para **administração** > **descrição geral** > **configuração do Site**  >  **Servidores e funções de sistema de sites**e, em seguida, selecione o servidor de site de modo passivo.
  2. No **funções do sistema de sites** painel, o botão direito no **servidor do Site** função e, em seguida, escolha **remover função**.
  3. Faça duplo clique no servidor do site de modo passivo e, em seguida, escolha **eliminar**.
  4. Depois de desinstala o servidor do site, no servidor do site primário Active Directory reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.
<!--sms489412-->


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="do-not-automatically-upgrade-superseded-applications"></a>Não atualizar automaticamente as aplicações substituídas
<!-- 1351266 -->
Com base no seu [comentários de voz do utilizador](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior), nesta versão tem a opção para configurar uma implementação de aplicações para atualizar automaticamente qualquer versão de substituição. Agora ao criar a implementação no **definições de implementação** página do **Assistente de implementação de Software**, para um **disponível** ou **necessário**instalar fim, pode ativar ou desativar a opção para **atualizar automaticamente qualquer substituídas versões desta aplicação**.


## <a name="install-multiple-applications-in-software-center"></a>Instalar várias aplicações no Centro de Software
<!-- 1357126 -->
Se um utilizador final ou o técnico de ambiente de trabalho tem de instalar várias aplicações num dispositivo, o Centro de Software suporta agora a instalar várias aplicações selecionadas. Isto permite ao utilizador ser mais eficiente ao não espera uma instalação concluir antes de iniciar a próxima.

Quando utilizar o modo selecionar vários no **aplicações** separador, os seguintes critérios determinam que aplicações de centro de Software permite que selecione multi:
 - A aplicação está visível ao utilizador
 - A aplicação já não está instalada
 - Aprovação do administrador não é necessária ou já é concedida
 - O estado da aplicação está disponível (por exemplo, já não transferir conteúdo)

### <a name="try-it-out"></a>Experimente!
**Na consola do Configuration Manager:** Implemente um utilizador ou dispositivo várias aplicações para a instalação, como disponível ou necessário (com o prazo no futuro). Não necessitam de aprovação do administrador. Para obter mais informações, consulte [implementar aplicações](/sccm/apps/deploy-use/deploy-applications).

**No Centro de Software:**
 1. O **aplicações** separador deve abrir por predefinição. 
 2. Para introduzir o modo selecionar vários na vista de lista, clique no ícone novo ![Ícone de seleção múltipla do Centro de software](media/software-center-multi-select-apps.png) no canto superior direito.
 3. Selecione a instalação clicando na caixa de verificação à esquerda das aplicações na lista de dois ou mais aplicações.
 4. Clique em de **instalar selecionado** botão.

As aplicações instalar como normal, apenas agora sucessivamente.


## <a name="client-based-pxe-responder-service"></a>Serviço baseado em clientes de dispositivo de resposta PXE
<!-- 1357148 -->
Um desafio comum para clientes que está a fornecer serviços PXE filiais remoto/com pouca ou nenhuma infraestrutura de servidor. A distribuição do ponto de função suporta sistemas de operativos cliente, mas não pode ser ativado por PXE devido uma dependência nos serviços de implementação do Windows.

Novas definições de cliente estão agora disponíveis para permitir que um serviço de dispositivo de resposta PXE nos clientes do Configuration Manager. Uma imagem de arranque preparada para PXE têm de residir na cache do cliente do dispositivo de resposta PXE.

### <a name="try-it-out"></a>Experimente!
Certifique-se de que existem pontos de distribuição com PXE ativado não existente ou outros servidores PXE no ambiente de teste que poderá entrar em conflito com este dispositivo de resposta do cliente PXE.

Na consola do Configuration Manager:
 1. No **biblioteca de Software** área de trabalho na **sistemas operativos**, **sequências de tarefas**: criar uma sequência de tarefas utilizando o modelo personalizado.
    1. Clique em **adicionar**, selecione **geral**e, em seguida, o **Set Task Sequence Variable** passo. Introduza **SMSTSPersistContent** como a variável de sequência de tarefas e introduza o valor **verdadeiro**.
    1. Clique em **adicionar**, selecione **Software**e, em seguida, o **transferir conteúdo do pacote** passo. Clique o asterisco gold e, em seguida, selecione uma imagem de arranque preparada para PXE. Incluem imagens de arranque x86 e x64. Configurar o passo para colocá-lo para o **cache do cliente do Configuration Manager**.
    1. Clique em **adicionar**, selecione **geral**e, em seguida, o **Set Task Sequence Variable** passo. Introduza **SMSTSPreserveContent** como a variável de sequência de tarefas e introduza o valor **verdadeiro**.
 2. No **administração** área de trabalho na **as definições de cliente**: criar uma política de definições de dispositivos de cliente personalizadas.
    1. Selecione o **as definições de Cache do cliente** grupo.
  1. Definir o **cliente de ativar o Configuration Manager no SO completo para partilhar conteúdo** definição **Sim**.
    1. Definir o **serviço dispositivo de resposta de ativar PXE** definição **Sim**.
  1. Para o **criar um certificado autoassinado ou importar um certificado de cliente PKI** definição, clique em **forneça um certificado**. Selecione **importar certificado** se o ambiente de teste tiver PKI, caso contrário clique em **OK** para criar um certificado autoassinado. 
    1. Configure as restantes definições conforme necessário para o seu ambiente de teste. (As predefinições deverão funcionar, a menos que existem requisitos de segurança ou de rede específicas.)
 3. Implemente a sequência de tarefas e definições personalizadas de cliente numa coleção de clientes de destino ser dispositivos de resposta de PXE. Aguarde que as políticas a aplicar e a sequência de tarefas a executar.
 4. Inicie outro cliente na mesma sub-rede PXE/arranque de rede como habitualmente.

### <a name="known-issues"></a>Problemas conhecidos
 - O editor de sequência de tarefas apresenta um ícone de erro vermelho para o **transferir conteúdo do pacote** passo quando adicionar uma imagem de arranque, mas a sequência de tarefas guarda com êxito. Abrir esta sequência de tarefas novamente no editor também mostra um aviso de inofensivos referenciado objetos não é possível encontrar. <!-- sms427542 -->
 - A imagem de arranque a partir do passo transferir conteúdo do pacote não for apresentada na lista de sequência de tarefas personalizada de referências. Também o **distribuir conteúdo** ação não está disponível. <!-- sms504017 -->


## <a name="change-in-the-configuration-manager-client-install"></a>Instalar a alteração no cliente do Configuration Manager  
Como resultado o comentários de voz do utilizador, [Silverlight já não está instalado nos clientes automaticamente.](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v) <!--1356195-->
  

## <a name="change-to-the-surface-device-dashboard"></a>Mude para o dashboard de dispositivo superfície
O dashboard superfície apresenta agora versões de firmware para descobrir dispositivos, em vez de versão do sistema operativo. Na consola, aceda a **monitorização** > **dispositivos Surface**. Pode ver os seguintes itens:
- percentagem de analisa
- percentagem dos modelos superfície
- Principais cinco versões de firmware
 <!--1355788-->


## <a name="improvements-to-office-365-client-management-dashboard"></a>Melhoramentos ao dashboard de gestão de clientes do Office 365 
O dashboard de gestão de clientes do Office 365 agora apresenta uma lista de dispositivos relevantes quando estão selecionadas secções de gráfico. Na consola, aceda a **biblioteca de Software** >**descrição geral** >**gestão de clientes do Office 365**. O dashboard é apresentado no lado direito. Selecionar critérios do gráfico de mostra uma lista de dispositivos.  
<!--1357281-->


## <a name="improvements-to-the-configuration-manager-console"></a>Melhorias à consola do Configuration Manager 
Efetuamos as seguintes melhorias à consola do Configuration Manager, que foram um resultado dos seus comentários de voz do utilizador.

- [Lista de dispositivos mostra utilizador primário](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user): Apresenta uma lista de dispositivos em ativos e compatibilidade, dispositivos, agora apresenta o utilizador primário por predefinição. Também pode ser adicionado o último utilizador com sessão iniciado como uma coluna opcional. <!-- 1357280 -->
- [Coleções cujo nome foi alteradas apresentam nas regras de associação de coleção existente](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections): Se uma coleção é um membro de outra coleção e nome é alterado, o novo nome é atualizado nas regras de associação.<!--1357282--> 


## <a name="improvements-to-operating-system-deployment"></a>Melhorias para implementação do sistema operativo
Iremos efetuadas as seguintes melhorias para implementação do sistema operativo, alguns dos quais foram o resultado dos seus comentários de voz do utilizador.
 - [Visualizador de registo de predefinição na imagem de arranque](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a): No Windows PE, quando iniciar cmtrace.exe, já não for pedido para escolher se pretende que este programa o Visualizador de predefinidos para ficheiros de registo. <!-- SMS 500897 -->
 - Transferir conteúdo do pacote passo: Agora pode adicionar imagens de arranque para este passo de sequência de tarefas.


## <a name="windows-10-feedback-hub-app-integration"></a>Integração de aplicações do Hub de comentários do Windows 10

Iremos adoram, tanto que iremos agora está a ativar comentários através de comentários o [comentários Hub aplicação](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) incorporada para o Windows 10. Quando a **adicionar comentários novo**, certifique-se de selecionar o **gestão empresarial** categoria e, em seguida, escolha uma das seguintes subcategorias:
 - Cliente do Configuration Manager
 - Consola do Configuration Manager
 - Implementação do SO do Configuration Manager
 - Servidor do Configuration Manager

Continuar a utilizar o nosso [página do uservoice](http://configurationmanager.uservoice.com/) votar em ideias de funcionalidade nova no Configuration Manager.


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre instalar ou atualizar o ramo de pré-visualização técnica, consulte [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    

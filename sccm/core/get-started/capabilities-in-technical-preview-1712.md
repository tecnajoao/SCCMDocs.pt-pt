---
title: Technical Preview 1712 | Microsoft Docs
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis na versão Technical Preview versão 1712 para o System Center Configuration Manager.
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: c3154f705afc48cebe075083666e7a5d2b7f726b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130280"
---
# <a name="capabilities-in-technical-preview-1712-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview versão 1712 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão versão 1712. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. 

Revisão [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview) antes de instalar esta versão do technical preview. Nesse artigo familiariza com os requisitos gerais e limitações para a utilização de uma technical preview, como ao atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Problemas conhecidos neste Technical Preview:**
- **Atualização para uma nova versão de pré-visualização falha quando tem um servidor de site em modo passivo**. Se tiver um [servidor do site primário em modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), em seguida, tem de desinstalar o servidor do site de modo passivo antes de atualizar para esta nova versão de pré-visualização. Pode reinstalar o servidor do site de modo passivo após a atualização do seu site estiver concluída.

  Para desinstalar o servidor do site de modo passivo:
  1. Na consola do Configuration Manager, aceda a **Administration** > **descrição geral** > **configuração do Site**  >  **Servidores e funções de sistema de sites**e, em seguida, selecione o servidor de site de modo passivo.
  2. Na **funções do sistema de sites** painel, o botão direito do mouse no **servidor do Site** função e, em seguida, escolha **remover função**.
  3. Faça duplo clique no servidor do site de modo passivo e, em seguida, escolha **eliminar**.
  4. Depois de desinstala o servidor do site, no servidor do site primário active reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.
  <!--sms489412-->


**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="do-not-automatically-upgrade-superseded-applications"></a>Não atualizar automaticamente aplicações substituídas
<!-- 1351266 --> Com base no seu [comentários da voz do utilizador](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior), nesta versão, tem a opção de configurar uma implementação de aplicações para atualizar automaticamente todas as versões substituídas. Agora quando criar a implementação, na **definições de implementação** página do **Assistente de implementação de Software**, por qualquer **disponível** ou **necessário**instalar o fim, pode ativar ou desativar a opção para **atualizar automaticamente qualquer substituídas versões desta aplicação**.


## <a name="install-multiple-applications-in-software-center"></a>Instalar várias aplicações no Centro de Software
<!-- 1357126 --> Se um usuário final ou técnico de área de trabalho tem de instalar várias aplicações num dispositivo, o Centro de Software suporta agora a instalar diversas aplicações selecionadas. Isso permite que o usuário a ser mais eficiente enquanto não aguarda uma instalação seja concluída antes de iniciar a próxima.

Ao utilizar o modo de seleção múltipla na **aplicativos** guia, os seguintes critérios determinam que permite que o Centro de Software para a seleção múltipla de aplicações:
 - A aplicação é visível ao utilizador
 - A aplicação já não está instalada
 - Aprovação do administrador não é necessária ou já é concedida
 - O estado da aplicação está disponível (por exemplo, ainda não estiver a transferir conteúdo)

### <a name="try-it-out"></a>Experimente!
**Na consola do Configuration Manager:** Implemente para um utilizador ou dispositivo em várias aplicações para a instalação, como disponível ou necessário (com o prazo no futuro). Não exigem a aprovação de administrador. Para obter mais informações, consulte [implementar aplicações](/sccm/apps/deploy-use/deploy-applications).

**No Centro de Software:**
 1. O **aplicativos** separador deve abrir por predefinição. 
 2. Para introduzir o modo de seleção múltipla na vista de lista, clique no ícone novo ![Ícone de seleção múltipla de centro de software](media/software-center-multi-select-apps.png) no canto superior direito.
 3. Selecione duas ou mais aplicações para instalar clicando na caixa de verificação à esquerda das aplicações na lista.
 4. Clique nas **instalar selecionadas** botão.

As aplicações instalam normalmente, apenas agora consecutivas.


## <a name="client-based-pxe-responder-service"></a>Serviço de resposta PXE baseada no cliente
<!-- 1357148 --> Um desafio comum para clientes está fornecendo serviços PXE remoto/das filiais com pouca ou nenhuma infra-estrutura de servidor. A distribuição do ponto de função suporta sistemas operacionais, mas não pode ser ativado por PXE devido à dependência de serviços de implantação do Windows.

Novas definições de cliente estão agora disponíveis para permitir que um serviço de resposta PXE nos clientes do Configuration Manager. Uma imagem de arranque com PXE ativado deve residir na cache do cliente do dispositivo de resposta PXE.

### <a name="try-it-out"></a>Experimente!
Certifique-se de que existem não existem pontos de distribuição com PXE ativado existentes ou outros servidores PXE no ambiente de teste que podem entrar em conflito com este dispositivo de resposta do cliente PXE.

Na consola do Configuration Manager:
1. Na **biblioteca de Software** área de trabalho sob **sistemas operativos**, **sequências de tarefas**: criar uma sequência de tarefas utilizando o modelo personalizado.
   1. Clique em **Add**, selecione **gerais**e, em seguida, o **Set Task Sequence Variable** passo. Introduza **SMSTSPersistContent** como a variável de sequência de tarefas e introduza o valor **verdadeiro**.
   1. Clique em **Add**, selecione **Software**e, em seguida, o **transferir conteúdo do pacote** passo. Clique com o asterisco gold e, em seguida, selecione uma imagem de arranque preparada para PXE. Inclua imagens de arranque x86 e x64. Configurar o passo para colocá-lo para o **cache do cliente do Configuration Manager**.
   1. Clique em **Add**, selecione **gerais**e, em seguida, o **Set Task Sequence Variable** passo. Introduza **SMSTSPreserveContent** como a variável de sequência de tarefas e introduza o valor **verdadeiro**.
2. Na **administração** área de trabalho sob **definições de cliente**: criar uma política de definições personalizadas de cliente.
   1. Selecione o **definições de Cache do cliente** grupo.
   1. Definir o **ativar o Configuration Manager cliente em OS completo partilhem conteúdo** na definição **Sim**.
   1. Definir o **serviço de resposta PXE ativar** definição **Sim**.
   1. Para o **criar um certificado autoassinado ou importar um certificado de cliente PKI** definir, clique em **fornecer um certificado**. Selecione **importar certificado** se o ambiente de teste tiver PKI, caso contrário clique em **OK** para criar um certificado autoassinado. 
   1. Configure as restantes definições conforme necessário para o seu ambiente de teste. (As predefinições deverão funcionar a menos que haja requisitos de segurança de rede ou.)
3. Implemente a sequência de tarefas e definições personalizadas de cliente numa coleção de clientes de destino para ser respondentes PXE. Aguarde que as políticas a aplicar e a sequência de tarefas para executar.
4. Inicie outro cliente na mesma sub-rede para o arranque de PXE/rede como habitualmente.

### <a name="known-issues"></a>Problemas conhecidos
 - O editor de sequência de tarefas exibe um ícone vermelho de erro para o **transferir conteúdo do pacote** passo quando adiciona uma imagem de arranque, mas a sequência de tarefas salva com êxito. Abrir esta sequência de tarefas novamente no editor também mostra um aviso de inofensivo referenciado objetos não é possível encontrar. <!-- sms427542 -->
 - A imagem de arranque do passo transferir conteúdo do pacote não mostra na lista da sequência de tarefas personalizada de referências. Também o **distribuir conteúdo** ação não está disponível. <!-- sms504017 -->


## <a name="change-in-the-configuration-manager-client-install"></a>Instalar a alteração no cliente do Configuration Manager  
Como resultado de seus comentários de voz do utilizador, [Silverlight já não está instalado nos clientes automaticamente.](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v) <!--1356195-->
  

## <a name="change-to-the-surface-device-dashboard"></a>Alterar para o dashboard de dispositivos Surface
O painel do Surface apresenta agora versões de firmware para dispositivos Surface, em vez de versão do sistema operativo. Na consola, aceda a **monitorização** > **dispositivos Surface**. Pode ver os seguintes itens:
- Número de Surfaces
- Percentagem de modelos de surfaces
- Principais cinco versões de firmware <!--1355788-->


## <a name="improvements-to-office-365-client-management-dashboard"></a>Melhorias ao dashboard de gestão de clientes do Office 365 
O dashboard de gestão de clientes do Office 365 agora exibe uma lista de dispositivos relevantes quando as secções do gráfico estão selecionadas. Na consola, aceda a **biblioteca de Software** >**descrição geral** >**gestão de clientes do Office 365**. O dashboard é apresentado no lado direito. Selecionar critérios do gráfico mostra uma lista de dispositivos.  
<!--1357281-->


## <a name="improvements-to-the-configuration-manager-console"></a>Melhorias à consola do Configuration Manager 
Que fizemos as seguintes melhorias à consola do Configuration Manager, que era um resultado dos seus comentários de voz do utilizador.

- [Lista de dispositivos mostra o utilizador primário](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user): Listas de dispositivos em ativos e compatibilidade, dispositivos, agora apresentam o utilizador primário por predefinição. O último utilizador com sessão iniciado também pode ser adicionado como uma coluna opcional. <!-- 1357280 -->
- [Coleções de nome mudadas apresentam nas regras de associação de coleção existente](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections): Se uma coleção é um membro de outra coleção e o nome é mudado, em seguida, o novo nome é atualizado nas regras de associação.<!--1357282--> 


## <a name="improvements-to-operating-system-deployment"></a>Melhorias para implementação do sistema operativo
Fizemos as seguintes melhorias para implementação do sistema operativo, alguns dos quais foram o resultado dos seus comentários de voz do utilizador.
 - [Visualizador de log padrão numa imagem de arranque](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a): No Windows PE, ao iniciar cmtrace.exe, já não for pedido para escolher se pretende tornar este Visualizador padrão para ficheiros de registo do programa. <!-- SMS 500897 -->
 - Transferir o conteúdo do pacote passo: Agora pode adicionar imagens de arranque para este passo de sequência de tarefas.


## <a name="windows-10-feedback-hub-app-integration"></a>Integração de aplicações do Hub de comentários do Windows 10

Adoramos comentários tanto que vamos agora ativar comentários através do [aplicação do Hub de comentários](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) incorporada para o Windows 10. Quando **adicionar novo comentário**, certifique-se de que selecionar o **Enterprise Management** categoria e, em seguida, escolha uma das seguintes subcategorias:
 - Cliente do Configuration Manager
 - Consola do Configuration Manager
 - Implementação do SO do Configuration Manager
 - Servidor do Configuration Manager

Continuar a utilizar o nosso [página do uservoice](http://configurationmanager.uservoice.com/) votar em ideias para novas funcionalidades no Configuration Manager.


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre a instalação ou a atualizar o ramo de pré-visualização técnica, veja [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    

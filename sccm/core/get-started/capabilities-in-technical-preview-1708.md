---
title: "Pré-visualização técnica 1708 | Microsoft Docs"
description: "Saiba mais sobre as funcionalidades disponíveis na versão de pré-visualização técnica 1708 para o System Center Configuration Manager."
ms.custom: na
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 022c9b2540f7ed403c38521c8e68f6c416c15c7c
ms.sourcegitcommit: 974fbc4408028c8be28911e5cd646efcf47c7f15
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/26/2017
---
# <a name="capabilities-in-technical-preview-1708-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1708 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1708. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos neste Technical Preview:**
-   **Falha de atualização para pré-visualizar versão 1708 quando tiver um servidor de site no modo passivo**. Quando executar a versão de pré-visualização 1706 ou 1707 e ter um [servidor do site primário em modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), tem de desinstalar o servidor do site de modo passivo antes de poder atualizar o site de pré-visualização com êxito para a versão 1708. Pode reinstalar o servidor do site de modo passivo depois do site executa a versão 1708.

  Para desinstalar o servidor do site de modo passivo:
  1. Na consola, aceda a **administração** > **descrição geral** > **configuração do Site** > **servidores e funções de sistema de sites**e, em seguida, selecione o servidor de site de modo passivo.
  2. No **funções do sistema de sites** painel, clique direito no **servidor do Site** função e, em seguida, escolha **remover função**.
  3. Faça duplo clique no servidor do site de modo passivo e, em seguida, escolha **eliminar**.
  4. Depois de desinstala o servidor do site, no servidor do site primário Active Directory reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.




**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Melhoramentos para especificar os parâmetros do script ao implementar scripts do PowerShell do Configuration Manager
<!-- 1236459 -->

Partir do Configuration Manager 1706, pode [criar e executadas scripts do PowerShell da consola do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).

No [1707 de pré-visualização técnica](/sccm/core/get-started/capabilities-in-technical-preview-1707#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager), iremos expandido sobre esta capacidade de permitir que o Configuration Manager a ler parâmetros do script.

Esta pré-visualização técnica, iremos tiver expandir a capacidade de parâmetros do script para detetar os parâmetros são obrigatórios e que são opcionais e pedido que introduza estes.

### <a name="try-it-out"></a>Experimente!

1. Siga as instruções para [criar e executadas scripts do PowerShell da consola do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).
2. No novo **parâmetros do Script** página do **Assistente de criação de scripts**, escolha um parâmetro e, em seguida, edite os respetivos valores.
O assistente apresenta os parâmetros são obrigatórios e que são opcionais.
4. Quando tiver concluído a edição de parâmetros, conclua o assistente.

Quando o script é executado, irá utilizar os valores de parâmetros que configurou. Se não tiver configurado um parâmetro obrigatório, o utilizador final será ser-lhe pedido para fornecer o parâmetro quando o script é executado.

## <a name="management-insights"></a>Informações de gestão
<!-- 1353967 -->
Agora pode obter informações sobre o estado atual do seu ambiente com base na análise de dados na base de dados do site. Insights ajudam-para melhor compreender o seu ambiente e atue com base nas informações. Reveja as informações de gestão na consola do Configuration Manager em **administração** > **gestão Insights** > **Insights todos os**. Nesta versão, as informações seguintes estão agora disponíveis:

- **Aplicações sem implementações**: Lista as aplicações no seu ambiente que não tem implementações ativas. Isto ajuda a localizar e eliminar as aplicações não utilizadas para simplificar a lista de aplicações apresentada na consola do.
- **Vazio coleções**: Lista as coleções no seu ambiente sem membros. Pode eliminar estas coleções para simplificar a lista de coleções apresentado quando a implementação de objetos, por exemplo.


## <a name="restart-computers-from-the-configuration-manager-console"></a>Reinicie os computadores a partir da consola do Configuration Manager   
<!-- 1356283 -->
A partir desta versão, pode utilizar a consola do Configuration Manager para identificar dispositivos cliente que requerem o reinício e, em seguida, utilizar uma ação de notificação de cliente reiniciá-las.

Para identificar dispositivos que tenham um reinício pendente, aceda a **ativos e compatibilidade** > **dispositivos** e selecione uma coleção com dispositivos que possam necessitar de um reinício. Depois de selecionar uma coleção pode ver o estado de cada dispositivo no painel de detalhes de uma nova coluna com o nome **pendente de reinício**. Cada dispositivo tem um valor de **Sim**, ou **não**.

Para criar a notificação de cliente para reiniciar um dispositivo:
1.  Localize o dispositivo que pretende reiniciar o nó de dispositivos da consola.
2.  Faça duplo clique no dispositivo, selecione **notificação do cliente**e, em seguida, selecione **reiniciar**. Esta ação abre uma janela de informações sobre o reinício. Clique em **OK** para confirmar o pedido de reinício.

Quando a notificação é recebida por um cliente, um **Centro de Software** é aberta a janela de notificação a informar o utilizador sobre o reinício. Por predefinição, o reinício ocorre após 90 minutos. Pode modificar a hora de reinício configurando [as definições de cliente](/sccm/core/clients/deploy/configure-client-settings). Definições para o comportamento de reinício se encontram no [reinício do computador](/sccm/core/clients/deploy/about-client-settings#computer-restart) separador das definições predefinidas.


### <a name="try-it-out"></a>Experimente!
Experimente concluir as seguintes tarefas e, em seguida, envie-nos **comentários** do **home page** separador do friso para nos informar como correu:
1.  Implementar uma aplicação ou Atualize para um dispositivo que irá exigir que o dispositivo reiniciar para concluir a instalação.
2.  Localize o dispositivo no **ativos e compatibilidade** > **dispositivos** nó da consola e confirme apresenta **Sim** no **pendente de reinício** coluna. Pode demorar até 20 minutos para que o estado de reinício pendente de mensagens em fila para serem refletidas na consola do.
3.  Monitorize o dispositivo para confirmar que a notificação do Centro de Software abre e que o dispositivo foi reiniciado com êxito.


## <a name="software-center-customization"></a>Personalização de centro de software
<!-- 1351224 -->
Pode adicionar enterprise elementos de imagem corporativa e especificar a visibilidade dos separadores no Centro de Software. Pode adicionar o seu nome de empresa específica do Centro de Software, definir um tema de cor de configuração de centro de Software, defina um logótipo de empresa e definir os separadores visíveis para os dispositivos cliente.

### <a name="customize-software-center"></a>Personalizar o Centro de Software

Para modificar o Centro de Software:

1. No **do Configuration Manager** consola, escolha **administração** > **as definições de cliente**. Clique na sua instância de definição de cliente pretendidos.
2. No **home page** separador o **propriedades** grupo, escolha **propriedades**.
3. No **predefinições** diálogo caixa, escolha **Centro de Software**.
4. Selecione **Sim** para **Selecione as novas definições para especificar as informações da empresa** para ativar as definições de personalização do Centro de Software.
5. Tipo sua **nome da empresa**.
6. Selecione o **cor esquema no Centro de Software**.
7. Clique em **procurar** para navegar para o logótipo no Centro de Software. O logótipo tem de ser um JPEG ou PNG de 400 x 100 pixéis com um tamanho máximo de 750 KB.
8. Selecione **Sim** para tornar os separadores visível no Centro de Software para dispositivos cliente. Pelo menos um separador tem de estar visível:

    -  Ativar o separador aplicações
    -  Ativar o separador de atualizações
    -  Ativar o separador de sistemas operativos
    -  Ativar o separador de estado da instalação
    -  Ativar o separador de conformidade do dispositivo
    -  Ativar o separador Opções

### <a name="next-steps"></a>Passos seguintes

Para saber mais sobre a gestão de aplicações no Configuration Manager, consulte o artigo [introdução à gestão de aplicações no System Center Configuration Manager](\sccm\apps\understand\introduction-to-application-management).

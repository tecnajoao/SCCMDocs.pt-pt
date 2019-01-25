---
title: Technical Preview 1708
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis na versão Technical Preview 1708 do System Center Configuration Manager.
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 5f135ab9389ba50e12d5f4fa81c046a873a74b30
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897785"
---
# <a name="capabilities-in-technical-preview-1708-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1708 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1708. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para a utilização de um técnico de pré-visualização, como atualizar entre as versões e como fornecer comentários sobre os recursos de uma technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos neste Technical Preview:**
- **Atualização para a versão 1708 pré-visualização falha quando tem um servidor de site em modo passivo**. Quando executar a versão de pré-visualização 1706 ou versão 1707 e ter uma [servidor do site primário em modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), tem de desinstalar o servidor do site de modo passivo antes de poder atualizar o site de pré-visualização com êxito para a versão 1708. Pode reinstalar o servidor do site de modo passivo após a versão 1708 de execução do seu site.

  Para desinstalar o servidor do site de modo passivo:
  1. Na consola, aceda a **Administration** > **descrição geral** > **configuração do Site** > **servidores e sites Funções do sistema**e, em seguida, selecione o servidor de site de modo passivo.
  2. Na **funções do sistema de sites** painel, clique direito na **servidor do Site** função e, em seguida, escolha **remover função**.
  3. Faça duplo clique no servidor do site de modo passivo e, em seguida, escolha **eliminar**.
  4. Depois de desinstala o servidor do site, no servidor do site primário active reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.




**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Melhorias para especificar parâmetros de script ao implantar scripts do PowerShell do Configuration Manager
<!-- 1236459 -->

A partir da configuração e posteriores 1706 de Manager, pode [criar e executar scripts do PowerShell da consola do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).

Na [versão 1707 de pré-visualização técnica](/sccm/core/get-started/capabilities-in-technical-preview-1707#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager), podemos expandidos nesta capacidade para permitir que o Configuration Manager a ler parâmetros do script.

Esta pré-visualização técnica, podemos expandiu a capacidade de parâmetros de script para detectar quais parâmetros são obrigatórios, e que são opcional e pedido que introduza esses.

### <a name="try-it-out"></a>Experimente!

1. Siga as instruções para [criar e executar scripts do PowerShell da consola do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).
2. No novo **parâmetros de Script** página do **Assistente de criação de Script**, escolha um parâmetro e, em seguida, edite os valores.
O assistente exibe quais parâmetros são obrigatórios, e que são opcional.
4. Quando tiver concluído a edição de parâmetros, conclua o assistente.

Quando o script é executado, ele usará quaisquer valores de parâmetro que configurou. Se não tiver configurado um parâmetro obrigatório, o utilizador final será solicitado a fornecer o parâmetro quando o script é executado.

## <a name="management-insights"></a>Informações de gestão
<!-- 1353967 --> Agora, pode obter informações sobre o estado atual do seu ambiente com base na análise de dados na base de dados do site. Insights ajudá-lo para melhor compreender o seu ambiente e tome medidas com base nas informações. Reveja as informações de gestão na consola do Configuration Manager no **Administration** > **informações de gestão** > **todas as informações**. Nesta versão, as informações seguintes estão agora disponíveis:

- **Aplicações sem implementações**: Lista as aplicações no seu ambiente que não têm implementações ativas. Isto ajuda a localizar e eliminar aplicações não utilizadas para simplificar a lista de aplicações apresentadas na consola do.
- **Esvaziar coleções**: Lista as coleções no seu ambiente que não têm membros. Pode eliminar estas coleções para simplificar a lista de coleções apresentadas quando implementar objetos, por exemplo.


## <a name="restart-computers-from-the-configuration-manager-console"></a>Reinicie os computadores a partir da consola do Configuration Manager   
<!-- 1356283 --> Começando com esta versão, pode utilizar a consola do Configuration Manager para identificar os dispositivos de cliente que requerem um reinício e, em seguida, utilize uma ação de notificação de cliente para reiniciá-las.

Para identificar dispositivos que tenham um reinício pendente, aceda a **ativos e compatibilidade** > **dispositivos** e selecionar uma coleção com os dispositivos que possam necessitar de um reinício. Depois de selecionar uma coleção pode ver o estado de cada dispositivo no painel de detalhes numa nova coluna chamada **pendente de reinício**. Cada dispositivo tem um valor de **Sim**, ou **não**.

Para criar a notificação de cliente para reiniciar um dispositivo:
1.  Localize o dispositivo que pretende reiniciar no nó dispositivos da consola.
2.  Com o botão direito no dispositivo, selecione **notificação do cliente**e, em seguida, selecione **reiniciar**. Esta ação abre uma janela de informações sobre o reinício. Clique em **OK** para confirmar o pedido de reinício.

Quando a notificação é recebida por um cliente, um **Centro de Software** é aberta a janela de notificação para informar o utilizador sobre o reinício. Por predefinição, o reinício ocorre depois de 90 minutos. Pode modificar a hora de reinício configurando [definições de cliente](/sccm/core/clients/deploy/configure-client-settings). Definições para o comportamento de reinício se encontram no [reiniciar o computador](/sccm/core/clients/deploy/about-client-settings#computer-restart) separador das definições padrão.


### <a name="try-it-out"></a>Experimente!
Experimente concluir as seguintes tarefas e, em seguida, envie-nos **comentários** partir do **home page** separador do friso para nos informar como correu:
1.  Implementar uma aplicação ou Atualize para um dispositivo que irá exigir que o dispositivo seja reiniciado para concluir a instalação.
2.  Localize o dispositivo na **ativos e compatibilidade** > **dispositivos** nó da consola e confirme que é apresentada **Sim** no **pendente de reinício**  coluna. Pode demorar até 20 minutos para que o estado pendente de reinício sejam refletidas na consola do.
3.  Monitorize o dispositivo para confirmar que a notificação de centro de Software é aberto e que o dispositivo com êxito for reiniciado.


## <a name="software-center-customization"></a>Personalização do Centro de software
<!-- 1351224 --> Pode adicionar elementos de marca corporativa e especificar a visibilidade dos separadores no Centro de Software. Pode adicionar o seu nome de empresa específico do Centro de Software, defina um tema de cores de configuração do Centro de Software, defina um logótipo de empresa e definir as guias visíveis para os dispositivos de cliente.

### <a name="customize-software-center"></a>Personalizar o Centro de Software

Para modificar o Centro de Software:

1. Na **Configuration Manager** da consola, escolha **administração** > **as definições de cliente**. Clique na sua instância de definição de cliente pretendido.
2. Sobre o **home page** separador o **propriedades** grupo, selecione **propriedades**.
3. Na **predefinições** caixa de diálogo caixa, escolha **Centro de Software**.
4. Selecione **Sim** ao **selecione definições para especificar as informações da empresa** para ativar as definições de personalização do Centro de Software.
5. Tipo de sua **nome da empresa**.
6. Selecione seu **esquema para o Centro de Software de cor**.
7. Clique em **procurar** para navegar para o seu logótipo para o Centro de Software. O logótipo tem de ser um JPEG ou PNG de 400 x 100 pixéis com um tamanho máximo de 750 KB.
8. Selecione **Sim** para tornar os guias visíveis no Centro de Software para dispositivos cliente. Pelo menos um separador tem de estar visível:

    -  Ativar separador aplicações
    -  Ativar separador atualizações
    -  Ativar separador Sistemos operativos
    -  Ativar separador de estado da instalação
    -  Ativar separador conformidade de dispositivo
    -  Ativar separador Opções

### <a name="next-steps"></a>Passos seguintes

Para saber mais sobre a gestão de aplicações no Configuration Manager, veja [introdução à gestão de aplicações no System Center Configuration Manager](/sccm/apps/understand/introduction-to-application-management).

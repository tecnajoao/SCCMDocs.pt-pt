---
title: "Pré-visualização técnica 1801 | Microsoft Docs"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades disponíveis na versão de pré-visualização técnica 1801 para o System Center Configuration Manager."
ms.custom: na
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: f4be3ffe817392bf8fefdcf4e481c739778025ff
ms.sourcegitcommit: db9978135d7a6455d83dbe4a5175af2bdeaeafd8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/22/2018
---
# <a name="capabilities-in-technical-preview-1801-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1801 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1801. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. 

Reveja [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview) antes de instalar esta versão do technical preview. Esse artigo familiarizes, com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como os seus comentários.     


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
<!--sms 489412-->


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->



## <a name="create-phased-deployments"></a>Criar implementações faseadas
<!-- 1357405 -->
Implementações faseadas automatizam uma coordenada, sequenciada implementação de software sem criar múltiplas implementações. Nesta versão do Technical Preview, o Assistente de implementação faseada pode ser concluído para sequências de tarefas na consola de administração. No entanto, as implementações não são criadas. 

### <a name="try-it-out"></a>Experimente!  
  Experimente concluir as tarefas. Em seguida, enviar **comentários** do **home page** separador do Friso nos informar como correu.
 
**Criar uma implementação faseada para uma sequência de tarefas** </br>
1. No **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.
2. Faça duplo clique na sequência de tarefas existente e selecione **criar implementação fases**. 
3. No **geral** separador, atribua a implementação faseada um nome, descrição (opcional) e selecione **criar automaticamente as fases de piloto e de produção predefinido**. 
4. Preencher o **piloto coleção** e **coleção de produção** campos. Selecione **seguinte**.
5. No **definições** separador, escolha uma opção para cada uma das definições de agendamento e selecione **seguinte** quando concluir. 
6. No **fases** separador, editar qualquer das fases, se necessário, em seguida, clique em **seguinte**.
7. Confirme as suas seleções no **resumo** separador, em seguida, clique em **seguinte** para continuar.

## <a name="co-management-reporting"></a>Relatórios de gestão conjunta
<!-- 1356648 -->
Se estiver a utilizar o [gestão conjunta](/sccm/core/clients/manage/co-management-overview) capacidades, agora, pode ver um dashboard com informações sobre a gestão conjunta no seu ambiente. Na consola do Configuration Manager, navegue para o **monitorização** área de trabalho, expanda **atualizar preparação**e selecione o **gestão conjunta** dashboard. O dashboard inclui os seguintes mosaicos:
- **Dispositivos geridos conjuntamente**: a percentagem de dispositivos no seu ambiente que tiver ativado para a gestão conjunta
- **Distribuição de SO**: a repartição dos sistemas operativos (SO) por versão. Este gráfico utiliza os agrupamentos seguintes:
   - Windows 7 & 8.x
   - Windows 10 menor 1709
   - Windows 10 1709 e acima
  > [!NOTE] 
  > Windows 10, versão 1709 e posterior, é um pré-requisito para a gestão conjunta
- **Estado de gestão conjunta**: a repartição de dispositivo com êxito ou falha nas seguintes categorias:
   - Concluído com sucesso, híbrida do Azure AD associados
   - Concluído com sucesso, do Azure AD associado
   - Falha de: Falhada de inscrição automática
- **Transição de carga de trabalho**: um gráfico de barras que mostra o número de dispositivos é transitado para o Microsoft Intune para as cargas de trabalho disponíveis três: 
   - Políticas de conformidade
   - Acesso a recursos
   - Atualização do Windows para empresas

### <a name="prerequisites"></a>Pré-requisitos
- O computador que executa a consola do Configuration Manager requer o Internet Explorer 9 ou posterior.



## <a name="improvements-to-automatic-deployment-rule-evaluation-schedule"></a>Melhoramentos à agenda de avaliação da regra de implementação automática
<!-- 1357133 -->
Com base no seu [comentários de voz do utilizador](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling), agora pode agendar avaliação da regra (ADR) de implementação automática para o deslocamento de um dia base. Por exemplo, um desvio igual a dois dias após a segunda Terça-feira do mês avalia a regra na quinta-feira. 

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as tarefas. Em seguida, enviar **comentários** do **home page** separador do Friso nos informar como correu. <br/>

**Criar uma agenda personalizada que avalia e o desvio ADR a partir de um dia base** </br>
1.  No **biblioteca de Software** área de trabalho, expanda **atualizações de Software**e selecione **regras de implementação automática**.
2. Clique com o botão direito no **regras de implementação automática** e escolha **criar regra de implementação automática**. 
3. Siga as instruções para concluir a **geral**, **definições de implementação**, e **atualizações de Software** separadores. 
4. No **agendamento de avaliação** separador, selecione **executar a regra com base numa agenda** e **personalizar**.
5. Para a agenda personalizada, selecione **mensal** e colocada numa base por dia, tais como a segunda Terça-feira. 
6. Verifique **deslocamento (dias)** e o número de dias, em seguida, para o deslocamento **OK** quando terminar.  
7. Concluir o **criar Assistente de regra de implementação automática**. 



## <a name="reassign-distribution-point"></a>Reatribuir o ponto de distribuição
<!-- 1306937 -->
Muitos clientes têm infraestruturas de grandes dimensões do Configuration Manager e reduzindo a sites primários ou secundários para simplificar o respetivo ambiente. Tem de manter pontos de distribuição em localizações de sucursais para servir conteúdo para clientes geridos. Estes pontos de distribuição, muitas vezes, contenham vários terabytes ou mais dos conteúdos. Este conteúdo é dispendioso em termos de largura de banda de hora e a rede para distribuir a estes servidores remotos. 

Esta funcionalidade permite-lhe reatribuir um ponto de distribuição para outro site primário sem redistribuir o conteúdo. Esta ação atualiza a atribuição de sistema de site enquanto a persistência de todo o conteúdo no servidor. Se precisar de reatribuir múltiplos pontos de distribuição, primeiro efetuar esta ação num ponto de distribuição único, prosseguindo em seguida servidores adicionais um cada vez.

> [!IMPORTANT]
> O servidor de sistema de sites só pode alojar a função de ponto de distribuição. Se o servidor de sistema de sites aloja outra função de servidor do Configuration Manager, tais como o ponto de migração de estado, não é possível reatribuir o ponto de distribuição. Não é possível reatribuir um ponto de distribuição na nuvem. 

Esta opção não está funcional com esta versão devido ao limite de pré-visualização técnica de um único site primário. Considere o cenário e, em seguida, envie **comentários** do **home page** separador do Friso, sobre as capacidades desta ação.
1. Na consola do Configuration Manager, vá para o **administração** área de trabalho e selecione o **pontos de distribuição** nós.
2. O ponto de distribuição de destino com o botão direito e selecione **ponto de distribuição de reatribuir**. 
  ![Reatribuir pontos de distribuição](media/1306937-reassign-dp.png)
3. Selecione o servidor do site e o código do site ao qual pretende reatribuir este ponto de distribuição. 
  ![Selecione um servidor de Site](media/1306937-select-site.png)



## <a name="improvements-to-hardware-inventory"></a>Melhoramentos ao inventário de hardware
<!-- 1357389 -->
Para classes adicionadas recentemente, os comprimentos de cadeia mais de 255 caracteres podem ser especificados para propriedades de inventário de hardware que não são chaves.

### <a name="try-it-out"></a>Experimente!  
Experimente concluir as tarefas. Em seguida, enviar **comentários** do **home page** separador do Friso nos informar como correu.<br/>

1. No **administração** área de trabalho, clique em **as definições de cliente** Realce um dispositivo de cliente para editar, clique com botão direito, em seguida, selecione a definição **propriedades**. 
2. Selecione **inventário de Hardware**, em seguida, **definir Classes**, e **adicionar**.
3. Clique em de **Connect** botão.
4. Preencha **nome do computador**, **espaço de nomes WMI**, selecione **recursiva** se for necessário. Forneça as credenciais, se for necessário para estabelecer a ligação. Clique em **Connect** para ver as classes de espaço de nomes.
5. Selecione uma nova classe e clique em **editar**.
6. Alterar o **comprimento** pelo menos uma propriedade que é uma cadeia, que não sejam key, ser maior que 255. Clique em **OK**. 
7. Certifique-se de que a propriedade editada está selecionada para **adicionar classe de inventário de Hardware** e clique em **OK**. 
8. Recolha inventário de hardware com a classe recentemente adicionada, que contém uma propriedade superior a 255 carateres de comprimento. 



## <a name="improvements-to-client-settings-for-software-center"></a>Melhoramentos às definições de cliente no Centro de Software
<!-- 1351224 & 1355146 -->
Nesta versão do Technical Preview, foram introduzidas melhorias para personalização do Centro de Software com as definições de cliente. 

1. As definições de cliente no Centro de Software tem agora um **personalizar** botão.
2. Foi adicionada uma pré-visualização para mostrar o aspeto na faixa do Centro de Software.<!--1351224-->
    - Se um logótipo não estiver seleccionado, a pré-visualização mostra o texto do nome de empresa e cor.
    - Se um logótipo estiver selecionado, a pré-visualização mostra o logotipo e a empresa texto do nome.  
3.  **Ocultar aplicações não aprovadas no Centro de Software** é uma nova definição no Centro de Software. Quando esta opção estiver ativada, as aplicações disponíveis de utilizador que necessitem de aprovação estão ocultas no Centro de Software.<!--1355146-->

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as tarefas. Em seguida, enviar **comentários** do **home page** separador do Friso nos informar como correu.

1. No **administração** área de trabalho, clique em **as definições de cliente**. Selecione uma definição de dispositivo do cliente para editar. Faça duplo clique no mesmo, em seguida, selecione **propriedades** , em seguida, **Centro de Software**.
2.  Clique em de **personalizar** botão. Experimente as definições de personalização diferentes, incluindo a pré-visualização.
3. Ativar a definição **Ocultar aplicações não aprovadas no Centro de Software**. Observe as alterações no Centro de Software. 



## <a name="new-settings-for-windows-defender-application-guard"></a>Novas definições de proteção de aplicações do Windows Defender
<!-- 1356256 -->
Para Windows 10 versão 1709 e dispositivos posteriores, existem duas novas anfitrião interação definições para [Guard de aplicação do Windows Defender](/sccm/protect/deploy-use/create-deploy-application-guard-policy). 
1. Web sites podem ser dado acesso ao processador de gráficos virtuais do anfitrião. 
2. Podem ser persistente ficheiros transferidos no interior do contentor no anfitrião. </br>



## <a name="improvements-to-run-scripts"></a>Melhoramentos para executar Scripts
<!-- 1236459 -->
O [ **executar Scripts** funcionalidade](/sccm/apps/deploy-use/create-deploy-scripts) agora permite-lhe importar e executar scripts PowerShell assinados. 
- Para manter a integridade de script, os scripts assinados tem de ser importados em vez de copiar/colar. 
- Não não possível editar os scripts assinados importados após a importação.
    
>[!IMPORTANT]
>Nesta pré-visualização técnica, existem dois limitações temporárias.
>- Os scripts só podem ser importados para a funcionalidade de executar Scripts e não podem ser editados diretamente a partir da consola.
>- Scripts importados com uma codificação de Unicode não pode ser apresentado na consola do incorretamente. O script será executado ainda como originalmente escrito.





## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre instalar ou atualizar o ramo de pré-visualização técnica, consulte [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    

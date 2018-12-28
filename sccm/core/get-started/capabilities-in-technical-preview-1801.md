---
title: Pré-visualização técnica 1801 | Documentos da Microsoft
titleSuffix: Configuration Manager
description: Saiba mais sobre funcionalidades disponíveis na versão 1801 pré-visualização técnica do System Center Configuration Manager.
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 135fc21cf122650e70eedf5e87873c93f08d4907
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417647"
---
# <a name="capabilities-in-technical-preview-1801-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1801 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1801. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. 

Revisão [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview) antes de instalar esta versão do technical preview. Nesse artigo familiariza com os requisitos gerais e limitações para a utilização de uma technical preview, como ao atualizar entre versões e como fornecer comentários.     


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
  <!--sms 489412-->


**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

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
<!-- 1357405 --> As implementações faseadas automatizam uma implementação coordenada e sequenciada de software sem criar várias implementações. Nesta versão do Technical Preview, o Assistente de implementação pode ser concluído para sequências de tarefas na consola de administração. No entanto, as implementações não são criadas. 

### <a name="try-it-out"></a>Experimente!  
  Experimente concluir as tarefas. Em seguida, envie **comentários** da **home page** separador do Friso nos informar como correu.
 
**Criar uma implementação faseada para uma sequência de tarefas** </br>
1. Na **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.
2. Com o botão direito na sequência de tarefas existente e selecione **criar implementação faseada**. 
3. Sobre o **gerais** separador, dê um nome, descrição (opcional), à implementação faseada e selecione **criar automaticamente as fases de piloto e de produção predefinido**. 
4. Preencher o **coleção de projetos-piloto** e **coleção de produção** campos. Selecione **Seguinte**.
5. Sobre o **definições** separador, escolher uma opção para cada uma das definições de agendamento e selecione **próxima** quando terminar. 
6. Sobre o **fases** separador, edite qualquer uma das fases se for necessário, em seguida, clique em **próxima**.
7. Confirme as suas seleções no **resumo** separador, em seguida, clique em **próxima** para continuar.

## <a name="co-management-reporting"></a>Relatório de cogestão
<!-- 1356648 --> Se estiver a utilizar o [cogestão](/sccm/core/clients/manage/co-management-overview) capacidades, pode agora visualizar um dashboard com informações sobre a cogestão no seu ambiente. Na consola do Configuration Manager, navegue para o **monitorização** área de trabalho, expanda **preparação**e selecione o **cogestão** dashboard. O dashboard inclui os seguintes mosaicos:
- **Dispositivos cogeridos**: a percentagem de dispositivos no seu ambiente que tiver ativado para a cogestão
- **Distribuição do sistema operacional**: a divisão de sistemas operativos (SO) por versão. Este gráfico utiliza os seguintes agrupamentos:
  - Windows 7 & 8.x
  - Windows 10 inferior a 1709
  - Windows 10 1709 e superior
    > [!NOTE] 
    > Windows 10, versão 1709 ou posterior, é um pré-requisito para a cogestão
- **Estado de cogestão**: a divisão de êxito de dispositivo ou a falha nas seguintes categorias:
   - Êxito, Azure AD híbrido associado
   - Êxito, associados ao Azure AD
   - Falha de: Inscrição automática falhou
- **Transição da carga de trabalho**: um gráfico de barras que mostra o número de dispositivos que transitado para o Microsoft Intune para as cargas de trabalho disponíveis três: 
   - Políticas de conformidade
   - Acesso a recursos
   - Windows Update para empresas

### <a name="prerequisites"></a>Pré-requisitos
- O computador que executa a consola do Configuration Manager requer o Internet Explorer 9 ou posterior.



## <a name="improvements-to-automatic-deployment-rule-evaluation-schedule"></a>Melhorias à agenda de avaliação da regra de implementação automática
<!-- 1357133 --> Com base no seu [comentários da voz do utilizador](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling), já pode agendar avaliação de regra (ADR) de implementação automática desfasamento de um dia base. Por exemplo, um desvio de dois dias após a segunda Terça-feira do mês avalia a regra na quinta-feira. 

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as tarefas. Em seguida, envie **comentários** da **home page** separador do Friso nos informar como correu. <br/>

**Criar uma agenda personalizada que é avaliada e o deslocamento de regras de implementação automática de um dia base** </br>
1.  Na **biblioteca de Software** área de trabalho, expanda **atualizações de Software**e selecione **regras de implementação automática**.
2. Com o botão direito no **regras de implementação automática** e escolha **criar regra de implementação automática**. 
3. Siga as instruções para concluir a **gerais**, **definições de implementação**, e **atualizações de Software** separadores. 
4. Sobre o **agenda de avaliação** separador, selecione **executar a regra com base numa agenda** e **personalizar**.
5. Para a agenda personalizada, selecione **mensal** e colocar num dia base, como a segunda Terça-feira. 
6. Verifique **desfasamento (dias)** e o número de dias, em seguida, para o deslocamento **OK** quando terminar.  
7. Conclua o resto dos **criar Assistente de regra de implementação automática**. 



## <a name="reassign-distribution-point"></a>Reatribuir o ponto de distribuição
<!-- 1306937 --> Muitos clientes têm de grandes infra-estruturas de Configuration Manager e reduzindo os sites primários ou secundários para simplificar o seu ambiente. Eles ainda precisam manter os pontos de distribuição nas localizações das sucursais para servir de conteúdo para clientes gerenciados. Esses pontos de distribuição geralmente contêm vários terabytes, ou mais dos conteúdos. Este conteúdo é dispendioso em termos de largura de banda de rede e de tempo para distribuir a estes servidores remotos. 

Esta funcionalidade permite-lhe reatribuir um ponto de distribuição para outro site principal sem redistribuir o conteúdo. Esta ação atualiza a atribuição de sistema do site e a persistência de todo o conteúdo no servidor. Se precisa de reatribuir vários pontos de distribuição, primeiro efetuar esta ação num único ponto de distribuição e, em seguida, continue com servidores adicionais, um por vez.

> [!IMPORTANT]
> O servidor de sistema de sites só pode alojar a função de ponto de distribuição. Se o servidor de sistema de sites aloja outra função de servidor do Configuration Manager, tais como o ponto de migração de estado, não é possível reatribuir o ponto de distribuição. Não é possível reatribuir um ponto de distribuição de nuvem. 

Esta opção não está funcional com esta versão devido ao limite de pré-visualização técnica de um único site primário. Considere o cenário e, em seguida, envie **comentários** partir do **home page** separador do Friso, sobre os recursos desta ação.
1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho e selecione o **pontos de distribuição** nó.
2. O ponto de distribuição de destino com o botão direito e selecione **reatribuir ponto de distribuição**. 
  ![Reatribuir ponto de distribuição](media/1306937-reassign-dp.png)
3. Selecione o servidor do site e o código do site ao qual pretende reatribuir este ponto de distribuição. 
  ![Selecione um servidor de Site](media/1306937-select-site.png)



## <a name="improvements-to-hardware-inventory"></a>Melhorias ao inventário de hardware
<!-- 1357389 --> Para as classes adicionadas recentemente, superiores a 255 carateres de comprimentos de cadeia de caracteres podem ser especificados para as propriedades de inventário de hardware que não sejam chaves.

### <a name="try-it-out"></a>Experimente!  
Experimente concluir as tarefas. Em seguida, envie **comentários** da **home page** separador do Friso nos informar como correu.<br/>

1. Na **administração** área de trabalho, clique em **definições de cliente** realçar um dispositivo de cliente na definição de editar, clique com botão direito e selecione **propriedades**. 
2. Selecione **inventário de Hardware**, em seguida, **definir Classes**, e **adicionar**.
3. Clique nas **Connect** botão.
4. Preencha **nome do computador**, **espaço de nomes WMI**, selecione **recursiva** se for necessário. Forneça as credenciais se necessário, para ligar. Clique em **Connect** para ver as classes de espaço de nomes.
5. Selecione uma nova classe, em seguida, clique em **editar**.
6. Alteração da **comprimento** pelo menos uma propriedade que seja uma cadeia de caracteres, que não seja a chave, para ser superior a 255. Clique em **OK**. 
7. Certifique-se de que a propriedade editada está selecionada para **adicionar classe de inventário de Hardware** e clique em **OK**. 
8. Recolha inventário de hardware com a classe recentemente adicionada, que contém uma propriedade superior a 255 carateres de comprimento. 



## <a name="improvements-to-client-settings-for-software-center"></a>Melhoramentos às definições de cliente para o Centro de Software
<!-- 1351224 & 1355146 --> Nesta versão do Technical Preview, foram feitos aprimoramentos para personalização do Centro de Software nas definições de cliente. 

1. Definições de cliente para o Centro de Software agora tem um **personalizar** botão.
2. Foi adicionada uma pré-visualização para mostrar a aparência da faixa de centro de Software.<!--1351224-->
    - Se um logótipo não estiver selecionado, a pré-visualização mostra o texto do nome da empresa e a cor.
    - Se for selecionado um logótipo, a pré-visualização mostra o logotipo e a empresa texto do nome.  
3.  **Ocultar aplicações não aprovadas no Centro de Software** é uma nova definição para o Centro de Software. Quando esta opção está ativada, os aplicativos disponíveis de usuário que exigem a aprovação estão ocultos no Centro de Software.<!--1355146-->

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as tarefas. Em seguida, envie **comentários** da **home page** separador do Friso nos informar como correu.

1. Na **Administration** área de trabalho, clique em **definições de cliente**. Selecione uma definição de dispositivo do cliente para editar. Com o botão direito nele, em seguida, selecione **propriedades** , em seguida, **Centro de Software**.
2.  Clique nas **personalizar** botão. Experimente as definições de personalização diferentes, incluindo a pré-visualização.
3. Ativar a definição **Ocultar aplicações não aprovadas no Centro de Software**. Observe as alterações no Centro de Software. 



## <a name="new-settings-for-windows-defender-application-guard"></a>Novas definições para o Windows Defender Application Guard
<!-- 1356256 --> Para Windows 10 versão 1709 ou dispositivos posteriores, existem duas configurações de interação anfitrião novo para [Windows Defender Application Guard](/sccm/protect/deploy-use/create-deploy-application-guard-policy). 
1. Web sites podem ser dado acesso ao processador de gráficos virtual do anfitrião. 
2. Os ficheiros transferidos dentro do contentor podem ser mantidos no anfitrião. </br>



## <a name="improvements-to-run-scripts"></a>Melhorias para executar Scripts
<!-- 1236459 --> O [ **executar Scripts** funcionalidade](/sccm/apps/deploy-use/create-deploy-scripts) agora permite-lhe importar e executar scripts do PowerShell assinados. 
- Para manter a integridade de script, os scripts assinados tem de ser importados em vez de usar copiar/colar. 
- Não não possível editar scripts assinados importados após a importação.
    
>[!IMPORTANT]
>Esta pré-visualização técnica, existem duas limitações temporárias.
>- Scripts apenas podem ser importadas para a funcionalidade de executar Scripts e não podem ser editadas diretamente a partir da consola.
>- Scripts importados com uma codificação de não-Unicode podem ser apresentado na consola do incorretamente. O script continuarão sendo executados como originalmente escrito.





## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre a instalação ou a atualizar o ramo de pré-visualização técnica, veja [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    

---
title: Technical Preview 1803
titleSuffix: Configuration Manager
description: Saiba mais sobre novas funcionalidades disponíveis na versão 1803 do Configuration Manager Technical Preview.
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 672257141c0672a76b89ee9d78184d2a4230280f
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898363"
---
# <a name="capabilities-in-technical-preview-1803-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview versão 1803 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview no Configuration Manager, versão 1803. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica. 

Reveja os [Technical Preview](/sccm/core/get-started/technical-preview) artigo antes de instalar esta atualização. Nesse artigo familiariza com os requisitos gerais e limitações para a utilização de uma technical preview, como ao atualizar entre versões e como fornecer comentários.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**Seguem-se os novos recursos, que pode experimentar com esta versão.**  



 
## <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Distribuição de extração os pontos de distribuição da nuvem de suporte de pontos como origem  
<!--1321554--> Muitos clientes utilizam [pontos de distribuição de extração](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point) remoto em ou filiais, o que transferir conteúdo de um ponto de distribuição de origem na WAN. Se seus escritórios remotos tem uma melhor conexão à internet ou para reduzir a carga nos seus links WAN, agora, pode utilizar um [ponto de distribuição da nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) no Microsoft Azure como origem. Ao adicionar uma origem no **ponto de distribuição de extração** separador Propriedades do ponto de distribuição, qualquer ponto de distribuição de nuvem no site é agora listado como um ponto de distribuição disponíveis. O comportamento de ambas as funções de sistema de sites permanece o mesmo caso contrário. 

### <a name="prerequisites"></a>Pré-requisitos
- O ponto de distribuição de extração tem acesso à internet para comunicar com o Microsoft Azure.
- O conteúdo tem de ser distribuído ao ponto de distribuição de nuvem de origem.

> [!Note]  
> Esta funcionalidade de incorrer em custos à sua subscrição do Azure para a saída de rede e de armazenamento de dados. Para obter mais informações, consulte a [custo de utilização de distribuição baseado na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#BKMK_CloudDPCost).



## <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Suporte de transferência parcial na cache de elemento de rede de cliente para reduzir a utilização de WAN
<!--1357346--> Origens de cache ponto a ponto do cliente agora podem dividir o conteúdo em partes. Estas peças minimizam a transferência de rede para reduzir a utilização da WAN. O ponto de gestão fornece controlo mais detalhado das partes de conteúdo. Ele tenta eliminar mais do que uma transferência do conteúdo do mesmo por grupo de limites. 

### <a name="example-scenario"></a>Cenário de exemplo
A Contoso tiver um único site primário com dois grupos de limites: Sede (Sedes) e sucursal. Existe uma relação de contingência de 30 minutos entre os grupos de limites. O ponto de gestão e o ponto de distribuição para o site são apenas em limites do HQ. O local de filial não tem nenhum ponto de distribuição local. Dois dos quatro clientes da sucursal são configurados como origens de cache ponto a ponto. 

![Diagrama de configuração de rede, tal como descrito para o cenário de exemplo](media/1357346-peer-cache-source-parts.png)

1. O direcionamento de uma implementação com o conteúdo para todos os quatro clientes na sucursal. Distribuídas apenas o conteúdo ao ponto de distribuição.
2. Client3 e Client4 não tem uma origem local para a implementação. O ponto de gestão instrui os clientes de espera de 30 minutos antes de reverter para o grupo de limites remoto.
3. Client1 (PCS1) é a primeira origem de cache ponto a ponto para atualizar a política com o ponto de gestão. Porque este cliente está ativado como uma origem de cache ponto a ponto, o ponto de gestão instrui-lo para iniciar imediatamente o download parte A partir do ponto de distribuição.  
4. Quando Client2 (PCS2) entra em contacto com o ponto de gestão, como parte A já está em curso, mas não ainda concluído, o ponto de gestão instrui-lo para iniciar imediatamente a baixar a parte B do ponto de distribuição.
5. Conclusão da transferência de parte A PCS1 e notifica imediatamente o ponto de gestão. Como parte de B já está em curso, mas não ainda concluído, o ponto de gestão instrui-lo para iniciar a transferência de parte C do ponto de distribuição.
6. PCS2 conclusão da transferência de parte B e notifica imediatamente o ponto de gestão. O ponto de gestão instrui-lo para iniciar a transferência de parte D do ponto de distribuição. 
7. PCS1 conclusão da transferência de parte C e notifica imediatamente o ponto de gestão. O ponto de gestão informa o-lo de que existem não existem mais partes do ponto de distribuição remoto. O ponto de gestão instrui a transferir a parte B de seu elemento de rede local, PCS2.
8. Este processo continua até que ambas as origens de cache ponto a ponto do cliente tem todas as partes uns dos outros. O ponto de gestão dá prioridade partes do ponto de distribuição remoto antes de instruindo as origens de cache ponto a ponto para transferir partes de elementos locais. 
9. Client3 é o primeiro a atualizar a política após o período de contingência de 30 minutos expira. Agora ele verifica novamente com o ponto de gestão, que informa o cliente de novas fontes de locais. Em vez de transferirem o conteúdo na totalidade do ponto de distribuição na WAN, transfere o conteúdo na totalidade de uma das origens de cache ponto a ponto do cliente. Os clientes priorizar as origens do elemento de rede local. 

> [!Note]  
> Se o número de origens de cache ponto a ponto do cliente é superior ao número de partes de conteúdo, em seguida, o ponto de gestão instrui as origens de cache ponto a ponto adicional a aguardar para contingência como um cliente normal. 


### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie **comentários** da **home page** separador do Friso nos informar como correu.

1. Configurar [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) e [configurar o peering entre origens de cache](/sccm/core/plan-design/hierarchy/client-peer-cache) por normal.
2. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione **Sites**. Clique em **definições de hierarquia** na faixa de opções. 
3. Sobre o **gerais** separador, ative a opção de **configurar origens de cache ponto a ponto de cliente para dividir o conteúdo em partes**. 
4. Crie uma implementação necessária com o conteúdo.  

   > [!Note]  
   > Esta funcionalidade só funciona quando o cliente transfere conteúdo em segundo plano, tal como com uma implementação necessária. Downloads de sob demanda, como quando o usuário instala uma implementação disponível no Centro de Software, se comporta como de costume.  

1. Para vê-los a lidar com a transferência de conteúdo em partes, examine o **ContentTransferManager.log** na origem da cache ponto a ponto do cliente e o **MP_Location.log** no ponto de gestão.  
 



## <a name="maintenance-windows-in-software-center"></a>Janelas de manutenção no Centro de Software
<!--1358131--> Centro de software agora mostra a próxima janela de manutenção agendada. No separador Estado da instalação, alterne da exibição de todos para futuras. Apresenta o intervalo de tempo e a lista de implementações agendadas. A lista está em branco se não houver nenhum janelas de manutenção futura. 

![Centro de software que mostra a lista de implementações futuras no separador Estado da instalação](media/1358131-software-center-maintenance-windows.png)


## <a name="custom-tab-for-webpage-in-software-center"></a>Separador personalizado para a página Web no Centro de Software
<!--1358132--> Agora, pode criar um separador personalizado para abrir uma página Web no Centro de Software. Esta funcionalidade permite-lhe mostrar o conteúdo aos seus utilizadores finais de forma consistente e confiável. A lista seguinte inclui alguns exemplos:
- Contactar TI: informações sobre como contatar da sua organização departamento de TI
- Centro de suporte IT: IT Self-serviços ações como pesquisar uma base de dados de conhecimento ou abrir um pedido de suporte.
- Documentação do utilizador final: artigos para os utilizadores na sua organização em vários tópicos de TI como usar aplicativos ou atualizar para o Windows 10.


### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie **comentários** da **home page** separador do Friso nos informar como correu.

1. Na consola do Configuration Manager, **administração** área de trabalho **definições de cliente** nó, abra a **predefinições de cliente** política.
2. Selecione o **Centro de Software** grupo.
3. Para **definições do Centro de Software**, clique em **personalizar**.
4. Mude para o **separadores** separador.
5. Ativar a opção para **especificar um separador personalizado para o Centro de Software**.
    1. Introduza um nome na **nome do separador** campo de texto. Este nome é o que apresenta ao utilizador no Centro de Software.
    2. Introduza um URL válido no **URL de conteúdo** campo de texto. Este URL é o conteúdo que é o Centro de Software apresentada quando os utilizadores clicarem neste separador.

> [!Tip]  
> Centro de software utiliza componentes do Internet Explorer para o processamento da página da web.

## <a name="enable-third-party-software-update-support-on-clients"></a>Ativar o suporte de atualização de software de terceiros nos clientes

Agora pode ativar a configuração de clientes do Configuration Manager para atualizações de software de terceiros. Quando **ativar as atualizações de software de terceiros** para as propriedades de componente SUP, o SUP irá transferir o certificado de assinatura utilizado pelo WSUS para atualizações de terceiros. <!--1357605-->

Selecionando **ativar as atualizações de software de terceiros** nas definições de cliente faz o seguinte: 
- No cliente, ele define a política para "Permitir com sessão iniciada atualizações para uma localização do serviço do Microsoft update de intranet" 
- Instala o certificado de assinatura para o arquivo do Editor confiável no cliente. 

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie **comentários** da **home page** separador do Friso nos informar como correu.

1. No site superior na hierarquia do Configuration Manager, vá para o **administração** nó, expanda **configuração do Site**, em seguida, **Sites**.
2. Com o botão direito no seu servidor de site superior e selecione **configurar componentes do Site** , em seguida, **ponto de atualização de Software**.
3. Clique nas **atualizações de terceiros** separador e verificar **ativar as atualizações de software de terceiros**.
4. Open **definições de cliente** e aceda às definições para **atualizações de Software**.
5. Certifique-se **ativar as atualizações de software de terceiros** está definida como **Sim**.

## <a name="enable-copypaste-of-asset-details-from-monitoring-views"></a>Ativar copiar/colar dos detalhes do recurso de vistas de monitorização
Como resultado de sua [comentários da voz do utilizador](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20234866-allow-us-to-copy-information-out-of-the-asset-det) agora pode ativar a funcionalidade de copiar/colar no painel de detalhes de ativo em vistas de monitorização de estado de implementação e distribuição.  <!--1357552-->

## <a name="scap-extensions"></a>Extensões SCAP
A versão de pré-lançamento das extensões do SCAP está disponível na pasta CD. Latest SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi. Esta versão de pré-lançamento das extensões SCAP pode ser instalado em quaisquer versões atualmente suportadas do ramo atual do Configuration Manager e LTSB 1606. Para obter mais informações, consulte [extensões sobre o SCAP Security Content Automation Protocol ()](/sccm/compliance/plan-design/scap/about-scap).



## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre a instalação ou a atualizar o ramo de pré-visualização técnica, veja [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    

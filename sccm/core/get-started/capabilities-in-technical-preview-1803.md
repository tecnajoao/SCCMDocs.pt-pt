---
title: Pré-visualização técnica 1803
titleSuffix: Configuration Manager
description: Saiba mais sobre as novas funcionalidades disponíveis na versão 1803 Configuration Manager Technical Preview.
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f3c200fe699f85c195e41fc2b395a3d710b1788a
ms.sourcegitcommit: d3863a9b34f9925515cabe9a290a6c733e10108b
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/04/2018
---
# <a name="capabilities-in-technical-preview-1803-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1803 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview para o Configuration Manager, versão 1803. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica. 

Reveja o [Technical Preview](/sccm/core/get-started/technical-preview) artigo antes de instalar esta atualização. Esse artigo familiarizes, com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como os seus comentários.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  



 
## <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Distribuição de solicitação os pontos de distribuição da nuvem de suporte de pontos como origem  
<!--1321554-->
Utilizam muitos clientes [pontos de distribuição de solicitação](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point) em remoto ou de sucursais transfiram conteúdo de um ponto de distribuição de origem na WAN. Se os seus escritórios remotos tem uma ligação à internet melhor, ou para reduzir a carga no seu ligações WAN, agora, pode utilizar um [ponto de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) no Microsoft Azure como origem. Quando adicionar uma origem no **ponto de distribuição de solicitação** separador Propriedades do ponto de distribuição, qualquer ponto de distribuição em nuvem no site está agora listado como um ponto de distribuição disponíveis. O comportamento de ambas as funções de sistema de sites permanece igual caso contrário. 

### <a name="prerequisites"></a>Pré-requisitos
- O ponto de distribuição de solicitação tem acesso à internet para comunicar com o Microsoft Azure.
- O conteúdo deve ser distribuído ao ponto de distribuição de nuvem de origem.

> [!Note]  
> Esta funcionalidade de pagar a sua subscrição do Azure para a saída de rede e de armazenamento de dados. Para obter mais informações, consulte o [custo de utilização da distribuição baseada na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#BKMK_CloudDPCost).



## <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Suporte de transferência parcial na cache ponto a ponto do cliente para reduzir a utilização de WAN
<!--1357346-->
Origens de cache ponto a ponto de cliente podem agora dividir o conteúdo em partes. Estas partes minimizar a transferência de rede para reduzir a utilização da WAN. O ponto de gestão fornece controlo mais detalhado das peças conteúdos. Tentar eliminar mais do que uma transferência do conteúdo mesmo por grupo de limites. 

### <a name="example-scenario"></a>Cenário de exemplo
Contoso tem um único site primário com dois grupos de limites: Sede (HQ) e o escritório de sucursal. Há uma relação de contingência de 30 minutos entre os grupos de limites. O ponto de gestão e o ponto de distribuição para o site estão apenas num limite de HQ. Localização do escritório de sucursal não tem nenhum ponto de distribuição local. Dois dos quatro clientes na sucursal estão configurados como origens de cache ponto a ponto. 

![Diagrama da configuração de rede, tal como descrito para o cenário de exemplo](media/1357346-peer-cache-source-parts.png)

1. Uma implementação com conteúdos para todos os quatro clientes no escritório de sucursal de destino. Apenas a distribuir o conteúdo ao ponto de distribuição.
2. Client3 e Client4 não dispõe de uma origem local para a implementação. O ponto de gestão instrui os clientes de espera de 30 minutos antes de reverter para o grupo de limites remoto.
3. Client1 (PCS1) é a origem de cache ponto a ponto primeiro para atualizar a política com o ponto de gestão. Porque este cliente está ativado como uma origem de cache ponto a ponto, o ponto de gestão dá instruções ao-o para iniciar imediatamente a transferir parte A partir do ponto de distribuição.  
4. Quando Client2 (PCS2) entra em contacto com o ponto de gestão, como A parte já está em curso, mas não ainda foi concluída, o ponto de gestão dá instruções ao-o para iniciar imediatamente a transferir peça B do ponto de distribuição.
5. PCS1 conclusão da transferência de uma parte e imediatamente notifica o ponto de gestão. Como parte de B já está em curso, mas não ainda foi concluída, o ponto de gestão dá instruções ao-o para iniciar a transferência parte C do ponto de distribuição.
6. PCS2 conclusão da transferência parte B e imediatamente notifica o ponto de gestão. O ponto de gestão dá instruções ao-o para iniciar a transferência parte D do ponto de distribuição. 
7. PCS1 conclusão da transferência parte C e imediatamente notifica o ponto de gestão. O ponto de gestão informa o-lo de que existem não existem mais partes do ponto de distribuição remoto. O ponto de gestão dá instruções ao-la para transferir peça B do respetivo elemento de rede local, PCS2.
8. Este processo continua até ambas as origens de cache ponto a ponto de cliente têm todas as partes uns dos outros. O ponto de gestão dá prioridade à partes do ponto de distribuição remoto antes que dá instruções para as origens de cache ponto a ponto para transferir as partes de elementos de rede locais. 
9. Client3 é o primeiro a atualizar a política depois de contingência do período de 30 minutos. Agora verifica com o ponto de gestão, que informa o cliente do novo origens locais. Em vez de transferirem o conteúdo completo do ponto de distribuição na WAN, transfere o conteúdo completo de uma das origens de cache ponto a ponto do cliente. Os clientes atribuir prioridades a origens de elemento de rede local. 

> [!Note]  
> Se o número de origens de cache ponto a ponto de cliente é superior ao número de partes de conteúdo, o ponto de gestão instrui as origens de cache ponto a ponto adicional de espera para contingência como um cliente normal. 


### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar **comentários** do **home page** separador do Friso nos informar como correu.

1. Configurar [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) e [elemento origens de cache](/sccm/core/plan-design/hierarchy/client-peer-cache) por normal.
2. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **configuração do Site**e selecione **Sites**. Clique em **definições de hierarquia** no Friso. 
3. No **geral** separador, ative a opção para **configurar origens de cache ponto a ponto de cliente para dividir o conteúdo em partes**. 
4. Crie uma implementação necessária com conteúdo.  

   > [!Note]  
   > Esta funcionalidade só funciona quando o cliente transfere conteúdo em segundo plano, tal como com uma implementação necessária. Transferências da pedido, tal como quando o utilizador instala uma implementação disponível no Centro de Software, comporta-se como habitualmente.  

1. Para vê-los a transferência de conteúdos em partes de processamento, examine o **ContentTransferManager.log** na origem de cache ponto a ponto do cliente e o **MP_Location.log** no ponto de gestão.  
 



## <a name="maintenance-windows-in-software-center"></a>Janelas de manutenção no Centro de Software
<!--1358131-->
Centro de software agora apresenta a próxima janela de manutenção agendada. No separador Estado da instalação, mude a vista de todos os para Upcoming. Apresenta o intervalo de tempo e a lista de implementações que estão agendadas. A lista está em branco, se existirem sem janelas de manutenção futura. 

![Centro de software que mostra a lista de implementações futuras no separador Estado da instalação](media/1358131-software-center-maintenance-windows.png)


## <a name="custom-tab-for-webpage-in-software-center"></a>Separador personalizado para a página Web no Centro de Software
<!--1358132-->
Agora, pode criar um separador personalizado para abrir uma página Web no Centro de Software. Esta funcionalidade permite-lhe mostrar conteúdo aos seus utilizadores finais de forma consistente e fiável. A lista seguinte inclui alguns exemplos:
- Contactar TI: informações sobre como contactar a sua organização departamento de TI
- Centro de suporte IT: IT self-service ações como a procura de uma base de dados de conhecimento ou abrir um pedido de suporte.
- Documentação do utilizador final: artigos para utilizadores na sua organização em vários tópicos IT, tais como utilizar aplicações ou atualizar para o Windows 10.


### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar **comentários** do **home page** separador do Friso nos informar como correu.

1. Na consola do Configuration Manager, **administração** área de trabalho, **as definições de cliente** , a abertura de nó de **predefinições de cliente** política.
2. Selecione o **Centro de Software** grupo.
3. Para **definições do Centro de Software**, clique em **personalizar**.
4. Mudar para o **separadores** separador.
5. Ativar a opção para **especificar um separador no Centro de Software personalizado**.
    1. Introduza um nome no **nome do separador** campo de texto. Este nome é o que apresenta ao utilizador no Centro de Software.
    2. Introduza um URL válido no **URL conteúdo** campo de texto. Este URL é o conteúdo que é o Centro de Software apresentada quando os utilizadores clicam neste separador.

> [!Tip]  
> Centro de software utiliza componentes do Internet Explorer para composição da página web.

## <a name="enable-third-party-software-update-support-on-clients"></a>Ativar o suporte de atualização de software de terceiros em clientes

Agora, pode ativar a configuração de clientes do Configuration Manager para atualizações de software de terceiros. Quando lhe **ativar atualizações de software de terceiros** para as propriedades de componente SUP o SUP irá transferir o certificado de assinatura utilizado pelo WSUS para atualizações de terceiros. <!--1357605-->

Selecionar **ativar atualizações de software de terceiros** nas definições de cliente faz o seguinte: 
- No cliente, define a política para 'Permitir assinado atualizações para uma localização do serviço do Microsoft update de intranet' 
- Instala o certificado de assinatura para o arquivo de publicador fidedigna no cliente. 

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar **comentários** do **home page** separador do Friso nos informar como correu.

1. No site superior na hierarquia do Configuration Manager, vá para o **administração** nó, expanda **configuração do Site**, em seguida, **Sites**.
2. Faça duplo clique no seu servidor de site superior e selecionar **configurar componentes do Site** , em seguida, **ponto de atualização de Software**.
3. Clique em de **atualizações de terceiros** separador e verifique **ativar atualizações de software de terceiros**.
4. Abra **as definições de cliente** e aceda às definições do **atualizações de Software**.
5. Certifique-se **ativar atualizações de software de terceiros** está definido como **Sim**.

## <a name="enable-copypaste-of-asset-details-from-monitoring-views"></a>Permitir copiar/colar de detalhes do ativo de vistas de monitorização
Como resultado de sua [comentários de voz do utilizador](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20234866-allow-us-to-copy-information-out-of-the-asset-det) agora, pode ativar a funcionalidade copiar/colar no painel de detalhes de ativo do Estado de implementação e distribuição de vistas de monitorização.  <!--1357552-->

## <a name="scap-extensions"></a>Extensões SCAP
A versão de pré-lançamento extensões SCAP está disponível na pasta CD. Latest em SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi. Esta versão de pré-lançamento das extensões SCAP pode ser instalado em quaisquer versões atualmente suportadas do ramo atual do Configuration Manager e LTSB 1606. Para obter mais informações, consulte [extensões sobre o SCAP Security Content Automation Protocol ()](/sccm/compliance/plan-design/scap/about-scap).



## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre instalar ou atualizar o ramo de pré-visualização técnica, consulte [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    

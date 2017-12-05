---
title: Componentes do site
titleSuffix: Configuration Manager
description: "Saiba como configurar componentes do site para modificar o comportamento das funções do sistema de sites e relatórios de estado de site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
caps.latest.revision: "9"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 4c5e6d4587f79eb52e9295d2641f985520738ebe
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="site-components-for-system-center-configuration-manager"></a>Componentes do site para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Em cada site do System Center Configuration Manager, pode configurar componentes do site para modificar o comportamento das funções do sistema de sites e relatórios de estado de site. Configurações de componentes do site aplicam-se a um site e a cada instância de uma função de sistema de sites aplicáveis no site.  

## <a name="about-site-components"></a>Acerca dos componentes do site  
 A maioria das opções para os vários componentes do site são facilmente compreensíveis quando visualizadas na consola do Configuration Manager. No entanto, os detalhes seguintes podem ajudar a explicar algumas das configurações mais complexas ou direcioná-lo para conteúdo adicional que explicam-los.  

### <a name="software-distribution"></a>Distribuição de software  

-   **Definições de distribuição de conteúdo:**  Pode especificar as definições que modificam a forma como o servidor do site transfere conteúdo para pontos de distribuição. Quando aumenta os valores que utiliza para as definições de distribuição simultânea, a distribuição de conteúdo pode utilizar mais largura de banda de rede.  

-   **Conta de acesso de rede:**  Para obter informações sobre como configurar e utilizar a conta de acesso de rede, consulte [conta de acesso à rede](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA).  

### <a name="software-update-point"></a>Ponto de atualização de Software  

-   Para obter informações sobre as opções de configuração para o componente de ponto de atualização de software, consulte [instalar um ponto de atualização de software](../../../../sum/get-started/install-a-software-update-point.md).  

### <a name="management-point"></a>Ponto de gestão  

-   **Pontos de gestão:** Pode configurar o site para publicar informações sobre pontos de gestão de serviços de domínio do Active Directory.  

     Clientes do Configuration Manager utilizam pontos de gestão para localizar os serviços e para localizar informações do site, tais como a associação ao grupo de limites e as opções de seleção de certificados de PKI. Os clientes também utilizam pontos de gestão para localizar outros pontos de gestão no site, bem como pontos de distribuição a partir das quais transferir software. Pontos de gestão também ajudam os clientes para concluir a atribuição de site e para transferir a política de cliente e carregar as informações de cliente.  

     Porque o método mais seguro para os clientes localizarem pontos de gestão consiste em publicá-los nos serviços de domínio do Active Directory, será normalmente sempre selecionar todos os pontos de gestão de funcionamento para publicar nos serviços de domínio do Active Directory. No entanto, este método de localização de serviço requer o seguinte seja verdadeiro:

     - O esquema é expandido para o Configuration Manager.
     - Não existe um **System Management** contentor, com permissões de segurança apropriado para o servidor de site publicar neste contentor.
     - Site do Configuration Manager é configurado para publicar nos serviços de domínio do Active Directory.
     - Os clientes pertencem à mesma floresta do Active Directory como floresta do servidor do site.  

     Quando os clientes da intranet não podem utilizar serviços de domínio do Active Directory para localizar pontos de gestão, utilize [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns) em vez disso, a publicação.  

 Para obter informações gerais sobre a localização de serviço, consulte [compreender a forma como os clientes localizam os recursos de site e os serviços do System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   **Publicar pontos de gestão de intranet selecionados no DNS:** Especifique esta opção quando os clientes da intranet não é possível localizar pontos de gestão de serviços de domínio do Active Directory. Em vez disso, se utilizar um registo de recursos de localização de serviço DNS (SRV RR) para localizar um ponto de gestão do respetivo site atribuído.  

    Para o Configuration Manager para publicar os pontos de gestão de intranet no DNS, as seguintes condições devem ser cumpridas:  

    -   Os servidores DNS possuem uma versão de BIND 8.1.2 ou posterior.  

    -   Os servidores DNS estão configurados para atualizações automáticas e suportam registos de recursos de localização de serviço.  

    -   Os nomes de domínio completamente qualificado especificado (FQDN) para os pontos de gestão no Configuration Manager têm entradas de anfitrião (registos A ou AAA) no DNS.  

    > [!WARNING]  
    >  Para os clientes localizarem pontos de gestão que são publicados no DNS, é necessário atribuir clientes a um site específico (vez utilizam a atribuição automática de sites). Configure estes clientes para utilizar o código do site com o sufixo de domínio do respetivo ponto de gestão. Para obter mais informações, consulte [pontos de gestão Locating](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points) no [como atribuir clientes a um site no System Center Configuration Manager](/sccm/core/clients/deploy/assign-clients-to-a-site).  

     Se a clientes do Configuration Manager não é possível utilizar os serviços de domínio do Active Directory ou o DNS para localizar pontos de gestão na intranet, utilize [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). O primeiro ponto de gestão que está instalado para o site é automaticamente publicado no WINS quando é configurada para aceitar ligações de cliente HTTP na intranet.  

### <a name="status-reporting"></a>Relatórios de estado  

-   Estas definições configurar diretamente o nível de detalhe que está incluído nos relatórios de estado dos sites e clientes.  

### <a name="email-notification"></a>Notificação por e-mail  

-   Especifique a conta e o e-mail detalhes do servidor para ativar o Configuration Manager para enviar notificações por e-mail para alertas.  

### <a name="collection-membership-evaluation"></a>Avaliação da associação da coleção  

-   Utilize esta tarefa para definir a frequência da avaliação incremental da associação da coleção. A avaliação incremental atualiza uma associação da coleção apenas com recursos novos ou alterados.  

### <a name="edit-the-site-components-at-a-site"></a>Editar os componentes do site num site  

Utilize os seguintes passos para editar os componentes do site:

1.  Na consola do Configuration Manager, clique em **administração** > **configuração do Site** > **Sites**e, em seguida, selecione o site que tem os componentes do site que pretende configurar.  

2.  No **home page** separador o **definições** , clique em **configurar componentes do Site**. Em seguida, selecione o componente do site que pretende configurar.  

##  <a name="BKMK_ServiceMgr"></a> Utilizar o Gestor do Serviço do Configuration Manager para gerir componentes do site  
Pode utilizar o Gestor do serviço do Configuration Manager para controlar os serviços do Configuration Manager e ver o estado de qualquer serviço do Configuration Manager ou o thread de trabalho (coletivamente definidos como componentes do Configuration Manager). Compreenda o seguinte sobre componentes do Configuration Manager:  

-   Componentes podem executar em qualquer sistema de sites.  

-   Os componentes são geridos da mesma forma que gerir serviços no Windows. Pode iniciar, parar, pausar, retomar ou consultar componentes do Configuration Manager.  

Um serviço do Configuration Manager é executado quando tem uma tarefa para executar (normalmente, quando um ficheiro de configuração é escrito na pasta a receber de um componente). Se necessitar de identificar o componente envolvido numa operação, pode utilizar o Gestor do serviço do Configuration Manager para manipular vários serviços e threads. Em seguida, pode ver a alteração resultante no comportamento do Configuration Manager. Por exemplo, pode parar serviços do Configuration Manager um cada vez até é eliminada uma determinada resposta. Ao fazê-lo, poderá identificar o serviço responsável pelo comportamento.  

> [!TIP]  
>  O procedimento seguinte pode ser utilizado para manipular a operação do componente do Configuration Manager.  

### <a name="use-the-configuration-manager-service-manager"></a>Utilize o Service Manager do Configuration Manager  

1.  Na consola do Configuration Manager, clique em **monitorização** >  **estado do sistema**e, em seguida, clique em **estado do componente**.  

2.  No **home page** separador o **componente** , clique em **iniciar**. Em seguida, selecione **do serviço do Configuration Manager**.  

3.  Quando o Gestor do Serviço do Configuration Manager for aberto, estabeleça a ligação ao site que pretende gerir.  

     Se não encontrar o site que pretende gerir, clique em **Site**, clique em **Ligar**e, em seguida, introduza o nome do servidor de sites do site correto.  

4.  Expanda o site e navegue para **Componentes** ou **Servidores**, consoante o local onde os componentes que quer gerir estiverem localizados.  

5.  No painel direito, selecione um ou mais componentes. Em seguida, no **componente** menu, clique em **consulta** para atualizar o estado da seleção.  

6.  Após a atualização do Estado do componente, utilize uma das quatro opções baseadas em ação no **componente** menu para modificar a operação do componente. Após solicitar uma ação, deve consultar o componente para apresentar o novo estado do componente.  

7.  Feche o Configuration Manager Service Manager quando tiver terminado a modificação do Estado operacional dos componentes.  

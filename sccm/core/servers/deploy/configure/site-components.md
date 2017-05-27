---
title: Componentes do site do Configuration Manager | Documentos do Microsoft
description: "Saiba como configurar componentes do site para modificar o comportamento das funções do sistema de sites e relatórios de estado de site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 1b9e49da1a5bbfca93fe683b82d2c0056a22cc1f
ms.openlocfilehash: 83550fbf0ef1f9adb0bb2c51a4f3c26a7500d352
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="site-components-for-system-center-configuration-manager"></a>Componentes do site para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Em cada site do System Center Configuration Manager, pode configurar componentes do site para modificar o comportamento das funções do sistema de sites e relatórios de estado de site. Configurações de componente do site aplicam-se a um site e a cada instância de uma função do sistema de sites aplicável no site.  

## <a name="about-site-components"></a>Acerca dos componentes do site  
 A maioria das opções para os vários componentes do site são facilmente compreensíveis quando visualizado na consola do Configuration Manager. No entanto, os seguintes detalhes podem ajudar a explicar algumas das configurações mais complexas ou direcioná-lo para o conteúdo adicional que explicam-los.  

### <a name="software-distribution"></a>Distribuição de software  

-   **Definições de distribuição de conteúdo:**  Pode especificar as definições que modificar a forma como o servidor do site transfere o conteúdo para pontos de distribuição. Quando aumenta os valores que utiliza para as definições de distribuição simultânea, a distribuição de conteúdo pode utilizar mais largura de banda de rede.  

-   **Conta de acesso à rede:**  Para obter informações sobre como configurar e utilizar a conta de acesso à rede, consulte o artigo [conta de acesso à rede](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA).  

### <a name="software-update-point"></a>Ponto de atualização de Software  

-   Para obter informações sobre opções de configuração para o componente de ponto de atualização de software, consulte o artigo [instalar um ponto de atualização de software](../../../../sum/get-started/install-a-software-update-point.md).  

### <a name="management-point"></a>Ponto de gestão  

-   **Pontos de gestão:** Pode configurar o site para publicar as informações sobre os pontos de gestão para serviços de domínio do Active Directory.  

     Clientes do Configuration Manager utilizam pontos de gestão para localizar serviços e para localizar informações do site, tais como a associação de grupo de limites e opções de seleção de certificado PKI. Os clientes também utilizam pontos de gestão para localizar outros pontos de gestão no site, bem como pontos de distribuição para transferir software. Pontos de gestão também ajudam os clientes para concluir a atribuição de site e para transferir a política de cliente e carregar informações de cliente.  

     Uma vez que o método mais seguro para os clientes localizarem pontos de gestão consiste em publicá-los nos serviços de domínio do Active Directory, normalmente sempre selecionar todos os pontos de gestão a funcionar para publicar nos serviços de domínio do Active Directory. No entanto, este método de localização de serviço requer o seguinte procedimento para ser verdadeiras:

     - O esquema é expandido para o Configuration Manager.
     - Existe um **System Management** contentor, com permissões de segurança apropriados para o servidor do site publicar neste contentor.
     - Site do Configuration Manager está configurado para publicar nos serviços de domínio do Active Directory.
     - Os clientes de pertencer à mesma floresta do Active Directory que floresta do servidor de site.  

     Quando os clientes da intranet não é possível utilizar serviços de domínio do Active Directory para localizar pontos de gestão, utilize [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns) publicação em vez disso.  

 Para obter informações gerais sobre a localização de serviço, consulte o artigo [compreender como os clientes localizam os recursos do site e os serviços do System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   **Publicar os pontos de gestão de intranet selecionados no DNS:** Especifique esta opção quando os clientes na intranet não é possível localizar pontos de gestão a partir de serviços de domínio do Active Directory. Em vez disso, podem utilizar um registo de recursos de localização de serviço DNS (SRV RR) para localizar um ponto de gestão do respetivo site atribuído.  

    Para o Configuration Manager para publicar pontos de gestão de intranet no DNS, devem ser cumpridas todas as condições seguintes:  

    -   Os servidores DNS possuem uma versão de BIND 8.1.2 ou posterior.  

    -   Os servidores DNS estão configurados para atualizações automáticas e suportam registos de recursos de localização de serviço.  

    -   Os nomes de domínio completamente qualificado especificado (FQDN) para os pontos de gestão no Configuration Manager têm entradas de anfitrião (registos A ou AAA) no DNS.  

    > [!WARNING]  
    >  Para os clientes localizarem pontos de gestão que são publicados no DNS, é necessário atribuir os clientes a um site específico (em vez de utilizar atribuição automática de sites). Configure estes clientes para utilizarem o código de site com o sufixo de domínio do respetivo ponto de gestão. Para obter mais informações, consulte o artigo [pontos de gestão Locating](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points) no [como atribuir clientes a um site no System Center Configuration Manager](/sccm/core/clients/deploy/assign-clients-to-a-site).  

     Se a clientes do Configuration Manager não é possível utilizar os serviços de domínio do Active Directory ou o DNS para localizar pontos de gestão na intranet, utilize [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). O primeiro ponto de gestão que está instalado para o site é automaticamente publicado no WINS quando é configurado para aceitar ligações de cliente HTTP na intranet.  

### <a name="status-reporting"></a>Relatórios de estado  

-   Estas definições configure diretamente o nível de detalhe que está incluído nos relatórios de estado a partir de sites e clientes.  

### <a name="email-notification"></a>Notificação por correio eletrónico  

-   Especifique a conta e o e-mail detalhes do servidor para permitir que o Configuration Manager para enviar notificações por correio eletrónico para alertas.  

### <a name="collection-membership-evaluation"></a>Avaliação da associação da coleção  

-   Utilize esta tarefa para definir a frequência da avaliação incremental da associação da coleção. A avaliação incremental atualiza uma associação da coleção apenas com recursos novos ou alterados.  

### <a name="edit-the-site-components-at-a-site"></a>Editar os componentes do site num site  

Utilize os seguintes passos para editar os componentes do site:

1.  Na consola do Configuration Manager, clique em **administração** > **configuração do Site** > **Sites**e, em seguida, selecione o site que tem os componentes do site que pretende configurar.  

2.  No **base** separador o **definições** grupo, clique em **configurar componentes do Site**. Em seguida, selecione o componente do site que pretende configurar.  

##  <a name="BKMK_ServiceMgr"></a> Utilizar o Gestor do Serviço do Configuration Manager para gerir componentes do site  
Pode utilizar o Gestor de serviço do Configuration Manager para controlar os serviços do Configuration Manager e ver o estado de qualquer serviço do Configuration Manager ou o thread de trabalho (coletivamente definidos como componentes do Configuration Manager). Compreenda o seguinte sobre componentes do Configuration Manager:  

-   Componentes podem executar qualquer sistema de sites.  

-   Os componentes são geridos da mesma forma que gere serviços no Windows. Pode iniciar, parar, interromper, retomar ou consultar componentes do Configuration Manager.  

Um serviço do Configuration Manager é executado quando existe uma tarefa executar (normalmente, quando um ficheiro de configuração é escrito na pasta a receber de um componente). Se tiver de identificar o componente envolvido numa operação, pode utilizar o Gestor de serviço do Configuration Manager para manipular vários serviços e threads. Em seguida, pode ver a alteração resultante no comportamento do Configuration Manager. Por exemplo, pode parar serviços do Configuration Manager um de cada vez, até é eliminada uma determinada resposta. Ao fazê-lo, poderá identificar o serviço responsável pelo comportamento.  

> [!TIP]  
>  O seguinte procedimento pode ser utilizado para manipular a operação do componente do Configuration Manager.  

### <a name="use-the-configuration-manager-service-manager"></a>Utilize o Gestor de serviço do Configuration Manager  

1.  Na consola do Configuration Manager, clique em **monitorização** >  **estado do sistema**e, em seguida, clique em **estado do componente**.  

2.  No **base** separador o **componente** grupo, clique em **iniciar**. Em seguida, selecione **do serviço do Configuration Manager**.  

3.  Quando o Gestor do Serviço do Configuration Manager for aberto, estabeleça a ligação ao site que pretende gerir.  

     Se não encontrar o site que pretende gerir, clique em **Site**, clique em **Ligar**e, em seguida, introduza o nome do servidor de sites do site correto.  

4.  Expanda o site e navegue para **Componentes** ou **Servidores**, consoante o local onde os componentes que quer gerir estiverem localizados.  

5.  No painel direito, selecione um ou mais componentes. Em seguida, no **componente** menu, clique em **consulta** para atualizar o estado da sua seleção.  

6.  Após a atualização do Estado do componente, utilize uma das quatro opções com base em ação no **componente** menu para modificar operação o componente. Após solicitar uma ação, deve consultar o componente para apresentar o novo estado do componente.  

7.  Feche o Gestor de serviço do Configuration Manager quando tiver terminado de modificar o estado operacional dos componentes.  


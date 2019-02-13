---
title: Componentes do site
titleSuffix: Configuration Manager
description: Saiba como configurar componentes do site para modificar o comportamento das funções do sistema de sites e relatórios de estado de site.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: af4d3319e94d8dd673f597e4df4dde3e73e15653
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129056"
---
# <a name="site-components-for-configuration-manager"></a>Componentes do site do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para cada site do Configuration Manager, pode configurar componentes do site para modificar o comportamento das funções do sistema de sites e relatórios de estado de site. Configurações de componente do site aplicam-se a um site e a cada instância de uma função de sistema de sites aplicável no site.  

Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó. Selecione um site. Na **configurações** grupo da faixa de opções, escolha **configurar componentes do Site**. Selecione uma das seguintes opções:

- [Distribuição de software](#software-distribution)  
- [Ponto de atualização de software](#software-update-point)  
- [Ponto de gestão](#management-point)  
- [Relatórios de estado](#status-reporting)  
- [Notificação por e-mail](#email-notification)
- [Avaliação da associação da coleção](#bkmk_colleval)


## <a name="about-site-components"></a>Acerca dos componentes do site  

 A maioria das opções para os vários componentes do site são facilmente compreensíveis quando visualizadas na consola do Configuration Manager. No entanto, os detalhes seguintes podem ajudar a explicar algumas das configurações mais complexas ou direcioná-lo para conteúdo adicional.  

> [!Note]  
> As opções disponíveis para alguns componentes variam se seleciona o site de administração central, um site primário ou um site secundário. Alguns componentes não estão disponíveis em todos os para determinados tipos de sites.  



### <a name="software-distribution"></a>Distribuição de software  

#### <a name="content-distribution-settings"></a>Definições de distribuição de conteúdo
Sobre o **gerais** separador, especifique as definições que modificam a forma como o servidor do site transfere conteúdo para os respetivos pontos de distribuição. Quando aumenta os valores que utiliza para as definições de distribuição simultânea, a distribuição de conteúdo pode utilizar mais largura de banda de rede.  

#### <a name="pull-distribution-point"></a>Ponto de distribuição de extração
Para obter mais informações, consulte [utilizar um ponto de distribuição de extração](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

#### <a name="network-access-account"></a>Conta de acesso à rede
Para obter mais informações, consulte [conta de acesso à rede](/sccm/core/plan-design/hierarchy/accounts#network-access-account).  


### <a name="software-update-point"></a>Ponto de atualização de software  

Para obter mais informações, consulte [instale um ponto de atualização de software](/sccm/sum/get-started/install-a-software-update-point).  


### <a name="management-point"></a>Ponto de gestão  

Sobre o **gerais** separador, configurar o site para publicar informações sobre os seus pontos de gestão de serviços de domínio do Active Directory.  

Clientes do Configuration Manager utilizam pontos de gestão para localizar serviços e para localizar informações do site, tais como associação de grupo de limites e opções de seleção de certificado PKI. Os clientes também utilizam pontos de gestão para localizar outros pontos de gestão no site, bem como pontos de distribuição a partir dos quais transferir software. Pontos de gestão também ajudam os clientes para concluir a atribuição de site e para transferir a política de cliente e carregar as informações de cliente.  

O método mais seguro para os clientes localizarem pontos de gestão consiste em publicá-los nos serviços de domínio do Active Directory. Este método de localização de serviço requer o seguinte seja verdadeiro:

- O esquema é expandido para o Configuration Manager.
- Há uma **System Management** contentor, com permissões de segurança adequados para o servidor de site para publicar para este contentor.
- Site do Configuration Manager está configurado para publicar nos serviços de domínio do Active Directory.
- Os clientes pertencem à mesma floresta do Active Directory como floresta do servidor do site.  

Quando os clientes da intranet não podem utilizar serviços de domínio do Active Directory para localizar pontos de gestão, utilize [publicação de DNS](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services#bkmk_dns).  

Para obter informações gerais sobre a localização de serviço, consulte [compreender como os clientes localizam os recursos de site e os serviços](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services).  


#### <a name="publish-selected-intranet-management-points-in-dns"></a>Publicar pontos de gestão de intranet selecionados no DNS
Especifique esta opção quando os clientes da intranet não é possível localizar pontos de gestão de serviços de domínio do Active Directory. Em vez disso, eles podem utilizar um registo de recursos de localização de serviço DNS (SRV RR) para localizar um ponto de gestão no respetivo site atribuído.  

Para o Configuration Manager para publicar pontos de gestão de intranet no DNS, todas as condições seguintes têm de ser cumpridas:  

-   Os servidores DNS possuem uma versão de BIND 8.1.2 ou posterior.  

-   Os servidores DNS estão configurados para atualizações automáticas e suportam registos de recursos de localização de serviço.  

-   Os nomes de domínio completamente qualificado especificado (FQDN) para os pontos de gestão no Configuration Manager tem entradas de anfitrião (registos A ou AAA) no DNS.  

> [!WARNING]  
>  Para os clientes localizarem pontos de gestão que são publicados no DNS, deve atribuir os clientes a um site específico (em vez de utilizar a atribuição automática de sites). Configure estes clientes para utilizar o código do site com o sufixo de domínio do seu ponto de gestão. Para obter mais informações, consulte [localizar pontos de gestão](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points).  

Se a clientes do Configuration Manager não é possível utilizar os serviços de domínio do Active Directory ou o DNS para localizar pontos de gestão na intranet, utilize [WINS](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services#bkmk_wins). O primeiro ponto de gestão que está instalado para o site é automaticamente publicado no WINS quando tiver configurado para aceitar ligações de cliente HTTP na intranet.  


### <a name="status-reporting"></a>Relatórios de estado  

Estas definições configurar diretamente o nível de detalhe que está incluído nos relatórios de estado dos sites e clientes.  


### <a name="email-notification"></a>Notificação por e-mail  

Especifica detalhes do servidor de e-mail e de conta para ativar o Configuration Manager para enviar notificações por e-mail para alertas.  

Para obter mais informações, consulte [utilizar alertas e o estado do sistema](/sccm/core/servers/manage/use-alerts-and-the-status-system).


### <a name="bkmk_colleval"></a> Avaliação da associação da coleção  

Usar esse componente para definir a frequência avaliação incremental da associação da coleção. A avaliação incremental atualiza uma associação da coleção apenas com recursos novos ou alterados.  

Para obter mais informações, consulte [melhores práticas para coleções](/sccm/core/clients/manage/collections/best-practices-for-collections).



##  <a name="BKMK_ServiceMgr"></a> Utilizar o Gestor do Serviço do Configuration Manager para gerir componentes do site  

Pode utilizar o Gestor de serviço do Configuration Manager para controlar os serviços do Configuration Manager e para ver o estado de qualquer serviço do Configuration Manager ou o thread de trabalho. Estes serviços e threads são coletivamente definidos como componentes do Configuration Manager. Compreenda as seguintes instruções sobre os componentes do Configuration Manager:  

-   Componentes podem executar em qualquer sistema de sites.  

-   Os componentes são geridos da mesma forma que gerencie serviços no Windows. Pode iniciar, parar, pausar, retomar ou consultar componentes do Configuration Manager.  

Um serviço do Configuration Manager é executado quando há algo para executar. Esta ação é, normalmente, quando um ficheiro de configuração é escrito na caixa de entrada de um componente. 


### <a name="use-the-configuration-manager-service-manager"></a>Utilizar o Gestor de serviço do Configuration Manager  

1.  Na consola do Configuration Manager, vá para o **monitorização** área de trabalho, expanda **estado do sistema**e selecione o **estado do componente** nó.  

2.  Na **componente** grupo da faixa de opções, selecione **iniciar**e, em seguida, escolha **Configuration Manager Service Manager**.  

3.  Quando o Gestor do Serviço do Configuration Manager for aberto, estabeleça a ligação ao site que pretende gerir.  

     Se não vir o site que pretende gerir, vá para o **Site** menu e selecione **Connect**. Em seguida, introduza o nome do servidor do site do site correto.  

4.  Expanda o site e navegue para **Componentes** ou **Servidores**, consoante o local onde os componentes que quer gerir estiverem localizados.  

5.  No painel direito, selecione um ou mais componentes. Em seguida, sobre o **componente** menu, selecione **consulta** para atualizar o estado da seleção.  

6.  Após atualização do Estado do componente, utilize uma das quatro opções com base em ação no **componente** menu para modificar a operação do componente. Após solicitar uma ação, deve consultar o componente para apresentar o novo estado do componente.  

7.  Feche o Gestor de serviço do Configuration Manager quando tiver terminado a modificação do Estado operacional dos componentes.  

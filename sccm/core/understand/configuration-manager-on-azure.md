---
title: Configuration Manager no Azure
description: Informações sobre como utilizar o Configuration Manager no ambiente do Azure.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d24257d8-8136-47f4-8e0d-34021356dc37
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 985b439a9f74f92a68b1e1c70e4cca0580b819c0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126799"
---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Perguntas mais frequentes do Configuration Manager no Azure - com frequência
*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As seguintes perguntas e respostas podem ajudar a compreender quando deve utilizar e como configurar o Configuration Manager no Microsoft Azure.

## <a name="general-questions"></a>Perguntas gerais
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>Minha empresa está a tentar mover como muitos servidores físicos quanto possível para o Microsoft Azure, pode mover servidores do Configuration Manager para o Azure?
Certamente, isso é um cenário suportado.  Ver [suporte para ambientes de Virtualização do System Center Configuration Manager](/sccm/core/plan-design/configs/support-for-virtualization-environments).

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>Ótimo! Meu ambiente requer vários sites. Todos os sites primários subordinados estará no Azure com o site de administração central ou no local? E os sites secundários?
Comunicações de site a site (baseados em ficheiros e replicação de base de dados) se beneficia da proximidade alojado no Azure. No entanto, todos os clientes relacionados com o tráfego seria remoto a partir de servidores de site e sistemas de sites. Se utilizar uma ligação de rede rápida e fiável entre o Azure e a sua intranet com um plano de dados ilimitados, o alojamento de toda a sua infraestrutura no Azure é uma opção.

No entanto, se usar um plano de dados limitados e largura de banda disponível ou custo é uma preocupação, ou a ligação de rede entre o Azure e a sua intranet não é rápida ou pode não ser confiável, em seguida, considere colocar sites específicos (e sistemas de sites) no local e, em seguida, utilizar o controlos de largura de banda incorporados no Configuration Manager.

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>Está a ter o Configuration Manager no Azure um cenário SaaS (Software como serviço)?
Não é um IaaS (infraestrutura como serviço) porque hospeda os servidores de infraestrutura do Configuration Manager em máquinas virtuais do Azure.

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>Quais áreas devem eu presto atenção ao considerar uma mudança de minha infraestrutura do Configuration Manager para o Azure?
Ótima pergunta, aqui estão as áreas que são mais importantes quando nessa tomada de decisão, cada um é explorado detalhadamente numa seção à parte deste tópico:
1.  Rede
2.  Disponibilidade
3.  Desempenho
4.  Custo
5.  Experiência de utilizador

## <a name="networking"></a>Rede
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>E quanto ao sistema de rede requisitos, devo usar ExpressRoute ou de um Gateway de VPN do Azure?
Funcionamento em rede é uma decisão muito importante. Velocidades de rede e a latência podem afetar a funcionalidade entre o servidor do site e sistemas de sites remotos e qualquer comunicação do cliente para os sistemas de sites. Nossa recomendação é utilizar o ExpressRoute. Mas não existe nenhuma limitação do Configuration Manager para parar de utilizar o Gateway de VPN do Azure. Deve examinar cuidadosamente os seus requisitos (desempenho, aplicação de patches, distribuição de software, implementação do sistema operativo) desta infraestrutura e, em seguida, decidir se. Alguns aspetos a considerar para cada solução incluem:

- **ExpressRoute** (recomendado)
  - Extensão natural do seu datacenter (pode ligar vários centros de dados)
  - Ligações privadas entre os datacenters do Azure e a sua infraestrutura
  - Não passam pela Internet pública
  - Oferece fiabilidade, velocidades rápidas, uma latência mais baixa, alta segurança
  - Ofertas até velocidades de 10 Gbps e opções do plano de dados ilimitados
- **Gateway de VPN**
  - VPNs de site-para-site/ponto a site
  - Tráfego passa pela Internet pública
  - Utiliza o protocolo (IPsec Internet Security) e troca de chaves de Internet (IKE)

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>O ExpressRoute tem muitas opções diferentes, como ilimitado versus velocidade com tráfego limitado, diferentes opções e o suplemento premium. Qual devo escolher?
As opções que selecionar dependem do cenário que estiver a implementar e quanto dados que pretende distribuir. A transferência de dados do Configuration Manager pode ser controlada entre servidores de site e pontos de distribuição, mas não pode ser controlada a comunicação de servidor do site de servidor do site.   Quando utiliza um plano de dados limitados, colocar sites específicos (e sistemas de sites) no local e utilizar [controlos de largura de banda incorporada do Configuration Manager](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management) podem ajudar a controlar o custo de utilização do Azure.

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>O que sobre os requisitos de instalação, como domínios do Active Directory? Eu ainda preciso associar meus servidores de site a um domínio do Active Directory?
Sim. Ao mover para o Azure, o [configurações suportadas](/sccm/core/plan-design/configs/supported-configurations) permanecem os mesmos, incluindo os requisitos do Active Directory para a instalação do Configuration Manager.

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>Eu entendo a necessidade de associar meus servidores de site a um domínio do Active Directory, mas posso utilizar o Azure Active Directory?
Não, o Azure Active Directory não é suportado neste momento. Os servidores de sites ainda têm de ser membros de um [domínio do Active Directory do Windows](/sccm/core/plan-design/configs/support-for-active-directory-domains).



## <a name="availability"></a>Disponibilidade
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>Um dos motivos pelos quais que estou mudando infraestrutura para o Azure é a promessa de elevada disponibilidade. Pode tirar partido das opções de elevada disponibilidade, como conjuntos de disponibilidade de VM do Azure para VMs que usarei para o Configuration Manager?
Sim! Conjuntos de disponibilidade da VM do Azure podem ser utilizados para funções de sistema de sites redundantes, como pontos de distribuição ou pontos de gestão.

Também pode usá-los para os servidores de site do Configuration Manager. Por exemplo, sites de administração central e sites primários podem ser todos no mesmo conjunto de disponibilidade que pode ajudar a garantir que não são reiniciados ao mesmo tempo.

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>Como posso fazer meu banco de dados altamente disponíveis? Pode utilizar a base de dados do Azure SQL? Ou, tenho de utilizar o Microsoft SQL Server numa VM?
Tem de utilizar o Microsoft SQL Server numa VM. O Configuration Manager não suporta o servidor SQL do Azure neste momento. Mas pode usar as funcionalidades, como a grupos de Disponibilidade AlwaysOn para o servidor SQL. [Grupos de Disponibilidade AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database) são recomendados e são suportadas oficialmente a partir da versão 1602 do Configuration Manager.

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>Pode utilizar balanceadores de carga do Azure com funções de sistema de sites, como pontos de gestão ou de pontos de atualização de software?
Enquanto o Configuration Manager não foi testado com balanceadores de carga do Azure, se a funcionalidade é transparente para a aplicação, não deve ter quaisquer efeitos adversos sobre as operações normais.


## <a name="performance"></a>Desempenho
### <a name="what-factors-affect-performance-in-this-scenario"></a>Quais os fatores que afetam o desempenho nesse cenário?
[Tamanho da VM do Azure e o tipo](https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs), VM do Azure (armazenamento premium é recomendado, especialmente para o SQL Server) de discos, funcionamento em rede a latência e velocidade são as áreas mais importantes.

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>Então, diga-me mais sobre máquinas virtuais do Azure; que VMs de tamanho devo utilizar?
Em geral, o poder de computação (CPU e memória) têm de preencher os [hardware recomendado para o System Center Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware). Mas existem algumas diferenças entre o hardware do computador regular e as VMs do Azure, especialmente quando se trata os discos estes uso de VMs.  Qual tamanho de VMs que utilizar depende do tamanho do seu ambiente, mas aqui estão algumas recomendações:
- Para implementações de produção de qualquer tamanho significativo, recomendamos "**S**" classe VMs do Azure. Isso é porque podem tirar partido de discos de armazenamento Premium.  Classe de "S" não utilização de VMs do armazenamento de BLOBs e em geral será não cumprem os requisitos de desempenho necessários para uma experiência de produção aceitáveis.
- Vários discos de armazenamento Premium devem ser utilizados para um maior dimensionamento e distribuídos no console de gerenciamento de disco do Windows para o IOPS máximo.  
- Recomendamos que utilize o melhor ou premium vários discos durante a implementação do site inicial (como P30, em vez de P20 e 2xP30 num volume repartido em vez de 1xP30). Em seguida, se seu site precisar mais tarde a incrementação no tamanho da VM devido a uma carga adicional, pode tirar partido de CPU e memória que fornece um maior tamanho de VM adicionais. Também terá discos já que pode aproveitar o IOPS débito adicional, que permite o maior tamanho da VM.



As tabelas seguintes listam as contagens de inicial do disco sugeridos para utilizar em sites primários e de administração central para várias instalações de tamanho:

**Base de dados localizadas conjuntamente site** -site de administração central ou primário com a base de dados no servidor do site:

| Clientes de ambiente de trabalho    |Tamanho recomendado da VM|Discos recomendados|
|--------------------|-------------------|-----------------|
|**Até 25 mil**       |   DS4_V2          |2xP30 (repartidos)  |
|**mil de 25 a 50 mil**      |   DS13_V2         |2xP30 (repartidos)  |
|**k de 50 a 100 mil**     |   DS14_V2         |3xP30 (repartidos)  |


**Base de dados do site remoto** -site de administração central ou primário com a base de dados do site num servidor remoto:

| Clientes de ambiente de trabalho    |Tamanho recomendado da VM|Discos recomendados |
|--------------------|-------------------|------------------|
|**Até 25 mil**       | Servidor do site: F4S </br>Servidor de base de dados: DS12_V2 | Servidor do site: 1xP30 </br>Servidor de base de dados: 2xP30 (repartidos)  |
|**mil de 25 a 50 mil**      | Servidor do site: F4S </br>Servidor de base de dados: DS13_V2 | Servidor do site: 1xP30 </br>Servidor de base de dados: 2xP30 (repartidos)   |
|**k de 50 a 100 mil**     | Servidor do site: F8S </br>Servidor de base de dados: DS14_V2 | Servidor do site: 2xP30 (repartidos)   </br>Servidor de base de dados: 3xP30 (repartidos)   |

O código a seguir mostra um exemplo de configuração para clientes de k de 50 a 100 mil em DS14_V2 com discos de 3xP30 num volume repartido com separado lógico volumes para o Configuration Manager instale e ficheiros de base de dados: ![VM)disks](media/vm_disks.png)  



## <a name="user-experience"></a>Experiência de utilizador
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>Mencionou que a experiência do usuário é uma das principais áreas de importância, por que não é?
As decisões que tomar para funcionamento em rede, disponibilidade, desempenho e, em que coloque os servidores de sites do Configuration Manager podem afetar os seus utilizadores diretamente. Acreditamos que uma mudança para o Azure deve ser transparente aos seus utilizadores para que eles não experienciar uma alteração nas suas interações diárias com o Configuration Manager.

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>OK, posso obtê-lo. Estou a planear instalar um único site primário autónomo numa máquina virtual do Azure e quero para se certificar de que os meus custos são baixos. Deve colocar sistemas de sites (remotos) (como pontos de atualização de pontos de gestão, pontos de distribuição e software) em máquinas virtuais do Azure também ou no local?
Exceto para a comunicação entre o servidor do site e um ponto de distribuição, estas comunicações de servidor para servidor num site podem ocorrer em qualquer altura e não utilizam mecanismos para controlar a utilização de largura de banda de rede. Uma vez que não é possível controlar a comunicação entre sistemas de sites, os custos associados estas comunicações devem ser considerados.

Velocidades de rede e latência são ainda outros fatores a serem também considerados. Redes lentas ou pouco fiáveis poderiam afetar a funcionalidade entre o servidor de site e sistemas de sites remotos, como também qualquer comunicação do cliente para os sistemas de sites. Também deve ser considerado o número de clientes geridos que utilizam um sistema de sites específico, bem como as funcionalidades que utiliza ativamente.
Em geral, pode aproveitar as orientações normal que diz respeito à WAN links e sistemas de sites como ponto de partida. O ideal é que o débito de rede que selecione e recebe entre o Azure e a sua intranet serão consistente com uma WAN, que é bem conectada com uma rede rápida.

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>E quanto a distribuição de conteúdo e a gestão de conteúdos? Devem ser de pontos de distribuição padrão no Azure ou no local e devo utilizar o BranchCache ou pontos de distribuição de extração no local? Ou eu fazer uso exclusivo dos pontos de distribuição de Cloud?
A abordagem de gerenciamento de conteúdo é muito as mesmas que nos servidores de site e sistemas de sites.
- Se utilizar uma ligação de rede rápida e fiável entre o Azure e a sua intranet com um plano de dados ilimitados, que hospeda os pontos de distribuição padrão no Azure pode ser uma opção.
-  Se usar um custo de largura de banda e de plano de dados limitados é uma preocupação ou a ligação de rede entre o Azure e a sua intranet não é rápida ou pode não ser confiável, em seguida, pode considerar outras abordagens. Estes incluem a localização padrão ou pontos de distribuição de extração no local, bem como utilizar o BranchCache. A utilização de pontos de distribuição baseado na nuvem também é uma opção, mas existem alguns limites sobre os tipos de conteúdo suportados (por exemplo, sem suporte para pacotes de atualizações de software).

> [!NOTE]
>  Se é necessário o suporte PXE, tem de utilizar pontos de distribuição no local (standard ou pull) para responder a pedidos de arranque. [O WDS não é atualmente suportado para ser executada em VMs do Azure](https://technet.microsoft.com/library/hh831764(v=ws.11).aspx).


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>Embora eu esteja OK com as limitações de pontos de distribuição baseado na nuvem, não quero colocar meu ponto de gestão numa rede de Perímetro, apesar de este procedimento é necessário para suportar os meus clientes baseados na Internet. Tenho de quaisquer outras opções?
Sim! Com o Configuration Manager versão 1610, Introduzimos o [Gateway de gestão da nuvem](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) como uma funcionalidade de pré-lançamento. (Esta funcionalidade apareceu pela primeira vez na versão de pré-visualização técnica 1606 como o [serviço de Proxy de nuvem](/sccm/core/get-started/capabilities-in-technical-preview-1606#a-namecloudproxyacloud-proxy-service-for-managing-clients-on-the-internet)).

O **Gateway de gestão da nuvem** fornece uma forma simples de gerir clientes do Configuration Manager na Internet. O serviço, o que é implementado no Microsoft Azure e requer uma subscrição do Azure, liga-se à sua infraestrutura do Configuration Manager no local com uma nova função chamada o ponto de conector do gateway de gestão na cloud. Depois de ter implementado e configurado, os clientes podem acessar funções de sistema no local do Configuration Manager de sites, independentemente de se eles estão conectados à rede interna privada ou na Internet.

Pode começar a utilizar o gateway de gestão na cloud no seu ambiente e envie-nos comentários para que isso melhor. Para obter informações sobre as funcionalidades de pré-lançamento, consulte [utilizar as funcionalidades de pré-lançamento de atualizações](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkprereleasea-use-pre-release-features-from-updates).

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>Também ouvi dizer que tenha outro novo recurso chamado de Cache ponto a ponto introduzida como um recurso de versão de pré-lançamento na versão 1610. Isso é diferente de BranchCache? Qual devo escolher?
Sim, totalmente diferente. [Configurar o peering em Cache](/sccm/core/plan-design/hierarchy/client-peer-cache) é uma tecnologia de Configuration Manager nativo de 100% em que o BranchCache é uma funcionalidade do Windows. Ambos podem ser úteis para; BranchCache utiliza uma difusão para localizar o conteúdo necessário ao passo que a Cache ponto a ponto utiliza gestores de configuração normal de distribuição fluxo de trabalho e o limite de definições de grupo.

Pode configurar qualquer cliente para que seja uma origem de Cache ponto a ponto. Em seguida, quando os pontos de gestão fornecem informações sobre localizações de origem de conteúdo de clientes, eles fornecem detalhes sobre os pontos de distribuição e quaisquer origens de Cache ponto a ponto com o conteúdo que o cliente requer.


## <a name="cost"></a>Custo
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>OK saber um pouco sobre o custo. Será uma solução económica para mim?
Difícil dizer desde cada ambiente é diferente. A melhor coisa a fazer é seu ambiente com o Microsoft Azure, Calculadora de preços de custos:  https://azure.microsoft.com/pricing/calculator/

## <a name="additional-resources"></a>Recursos adicionais
**Conceitos básicos:** http://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Tipos de máquina VM do Azure:**
 - Tamanhos de máquinas do Azure: https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs/  
 - Preços de VM: http://azure.microsoft.com/pricing/details/virtual-machines/  
 - Os preços de armazenamento: http://azure.microsoft.com/pricing/details/storage/

**Considerações de desempenho de disco:**    
 - Introdução de disco Premium:  http://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
 - Informações de disco Premium-se: http://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
 - Coleção útil de gráficos do máximo tamanhos e desempenho destina-se para o armazenamento: https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
 - Introdução de outro + alguns dados de acesso esporádico uber pau sobre como o armazenamento Premium funciona por trás de bastidores:  http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**Disponibilidade:**
 - Tempo de atividade de IaaS do Azure SLAS de classe: https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
 - Explicou de conjuntos de disponibilidade: https://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability/

**Conectividade:**
 - Express route vs. Azure VPN: http://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
 - Express Route preços: http://azure.microsoft.com/pricing/details/expressroute/
 - Mais informações sobre o Expressroute: http://azure.microsoft.com/documentation/articles/expressroute-introduction/

 

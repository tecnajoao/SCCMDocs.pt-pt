---
title: "Gestor de configuração no Azure | Documentos do Microsoft"
description: "Informações sobre como utilizar o Gestor de configuração num ambiente do Azure."
ms.custom: na
ms.date: 03/27/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: article
ms.assetid: d24257d8-8136-47f4-8e0d-34021356dc37
caps.latest.revision: 2
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 5276ad999fc871496d79e6efff34d5edc6335380
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Do Configuration Manager no Azure - perguntas mais frequentes
*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As seguintes perguntas e respostas podem ajudar a compreender quando utilizar e como configurar o Configuration Manager no Microsoft Azure.

## <a name="general-questions"></a>Perguntas gerais
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>A minha empresa está a tentar mover como vários servidores físicos possível para o Microsoft Azure, pode posso mover servidores do Configuration Manager para o Azure?
Certamente, este é um cenário suportado.  Consulte o artigo [suporte para ambientes de Virtualização do System Center Configuration Manager](/sccm/core/plan-design/configs/support-for-virtualization-environments).

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>Ótimo! O meu ambiente requer vários sites. Todos os sites primários subordinados estará no Azure com o site de administração central ou no local? E sites secundários?
Comunicações de site a site (baseados em ficheiros e replicação de base de dados) beneficia de proximidade de que está a ser alojados no Azure. No entanto, todos os clientes relacionados com o tráfego seria remoto de servidores de site e sistemas de sites. Se utilizar uma ligação de rede rápida e fiável entre o Azure e a sua intranet com um plano de dados ilimitado, que aloja todos os sua infraestrutura no Azure é uma opção.

No entanto, se utilizar um plano de dados com tráfego limitado e largura de banda disponível ou custo for uma preocupação, ou a ligação de rede entre o Azure e a sua intranet não é rápida ou pode ser pouco fiável, em seguida, considere colocar sites específicos (e sistemas de sites) no local e, em seguida, utilize os controlos de largura de banda incorporados para o Configuration Manager.

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>Está a ter do Configuration Manager no Azure um cenário de SaaS (Software como um serviço)?
Não é um IaaS (infraestrutura como serviço) porque que aloja os servidores de infraestrutura do Configuration Manager em máquinas virtuais do Azure.

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>Quais são as áreas deverá posso prestar atenção quando considerar uma deslocação da minha infraestrutura do Configuration Manager para o Azure?
Excelente pergunta, aqui estão as áreas que são mais importantes quando efetuar esta decisão, cada um é explorar uma secção separada deste tópico:
1.    Rede
2.    Disponibilidade
3.    Desempenho
4.    Custo
5.    Experiência de utilizador

## <a name="networking"></a>Rede
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>E sobre os requisitos de rede devo utilizar ExpressRoute ou um Gateway de VPN do Azure?
Funcionamento em rede é uma decisão muito importante. Velocidades de rede e latência podem afetar a funcionalidade entre o servidor do site e sistemas de sites remotos e qualquer comunicação de cliente para os sistemas de sites. A nossa recomendação relativamente consiste em utilizar ExpressRoute. Mas não existe nenhum limitação do Configuration Manager para impedi-lo de utilizar o Gateway de VPN do Azure. Deve Reveja com atenção os requisitos de (desempenho, aplicação de patches, distribuição de software, implementação de sistemas operativos) a partir do facto da infraestrutura e, em seguida, tornar a sua decisão. Alguns aspetos a considerar para cada solução incluem:

 - **ExpressRoute** (recomendado)
  - Extensão natural ao seu centro de dados (pode juntar distintos vários centros de dados)
  - Privada ligações entre centros de dados do Azure e a sua infraestrutura
  - Não aceda através da Internet pública
  - Oferece fiabilidade, velocidades rápidas, uma latência inferior, alta segurança
  - Ofertas até 10gbps velocidades e opções de plano de dados ilimitado
 - **Gateway VPN**
  - Site-a-site/ponto-a-site VPNs
  - Tráfego vai através da Internet pública
  - Utiliza a segurança do protocolo Internet (IPsec) e a troca de chaves de Internet (IKE)

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>ExpressRoute tem muitas opções diferentes, como ilimitado vs. a velocidade com tráfego limitado, diferentes opções e suplemento premium. Que devo escolher?
As opções que selecionar dependem o cenário que estiver a implementar e quanto dados que pretende distribuir. A transferência de dados do Configuration Manager pode ser controlada entre servidores do site e pontos de distribuição, mas não podem ser controlada comunicações de servidor de site de servidor do site.   Quando utiliza um plano de dados com tráfego limitado, colocar sites específicos (e sistemas de sites) no local e utilizar [controlos de largura de banda incorporadas do Configuration Manager](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management) podem ajudar a controlar o custo de utilização do Azure.

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>Acerca dos requisitos de instalação, como os domínios do Active Directory? Ainda necessito de associar meus servidores do site ao domínio do Active Directory?
Sim. Quando move para o Azure, o [configurações suportadas](/sccm/core/plan-design/configs/supported-configurations) de permanecer a mesma, incluindo os requisitos do Active Directory para a instalação do Configuration Manager.

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>Compreendo a necessidade de associar meus servidores do site a um domínio do Active Directory, mas posso utilizar o Azure Active Directory?
Não, do Azure Active Directory não é suportado neste momento. Os servidores de site ainda têm de ser membros de um [domínio do Active Directory do Windows](/sccm/core/plan-design/configs/support-for-active-directory-domains).



## <a name="availability"></a>Disponibilidade
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>Uma das razões que estou a mover a infraestrutura Azure é a promessa de elevada disponibilidade. Pode demorar partido das opções de elevada disponibilidade, como conjuntos de disponibilidade de VM do Azure para VMs que serão utilizados para o Configuration Manager?
Sim! Conjuntos de disponibilidade de VM Azure podem ser utilizados para funções de sistema de sites redundantes como pontos de distribuição ou pontos de gestão.

Também pode utilizá-los para os servidores de site do Configuration Manager. Por exemplo, sites de administração central e sites primários podem estar no mesmo conjunto de disponibilidade que pode ajudar a garantir que não são reiniciados ao mesmo tempo.

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>Como posso tornar o minha base de dados altamente disponível? Pode utilizar a base de dados do Azure SQL? Ou, é necessário utilizar o Microsoft SQL Server numa VM?
Tem de utilizar o Microsoft SQL Server numa VM. O Configuration Manager não suporta o Azure SQL Server neste momento. Mas pode utilizar remoto através da como grupos de Disponibilidade AlwaysOn para o SQL server. [Grupos de Disponibilidade AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database) são recomendadas e é oficialmente suportado começando na versão 1602 do Configuration Manager.

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>Pode utilizar balanceadores de carga Azure com funções de sistema de sites, como pontos de gestão ou de pontos de atualização de software?
Enquanto o Configuration Manager não foi testado com balanceadores de carga do Azure, se a funcionalidade é transparente para a aplicação, não deve ter quaisquer efeitos adversos operações normais.


## <a name="performance"></a>Desempenho
### <a name="what-factors-affect-performance-in-this-scenario"></a>Que fatores afetam o desempenho neste cenário?
[Tamanho da VM do Azure e o tipo](https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs), VM do Azure discos (armazenamento premium é recomendado, especialmente para o SQL Server), funcionamento em rede latência e velocidade são as áreas mais importantes.

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>Por isso, mais informações sobre máquinas virtuais do Azure; as VMs de tamanho devo utilizar?
Em geral, o power de computação (CPU e memória) necessário satisfazer o [recomendado hardware para o System Center Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware). No entanto, existem algumas diferenças entre o hardware do computador normal e VMs do Azure, especialmente quando chegar o discos Utilize estes VMs.  Que tamanho VMs utiliza depende do tamanho do seu ambiente, mas eis algumas recomendações:
- Para implementações de produção de qualquer tamanho significativo Recomendamos "**S**" classe VMs do Azure. Isto acontece porque pode tirar partido dos discos de armazenamento Premium.  Classe de não "S" utilização de VMs armazenamento de BLOBs e em geral não irá cumprir os requisitos de desempenho necessários para uma experiência de produção aceitável.
- Vários discos de armazenamento Premium devem ser utilizados para escala superior e repartidos (striped) na consola de gestão de discos do Windows para o IOPS máximo.  
- Recomendamos que utilize melhor ou premium vários discos durante a implementação de site inicial (como P30 em vez de P20 e 2xP30 num volume repartidos (striped) em vez de 1xP30). Em seguida, se o site precisar mais tarde a conhecer melhor o tamanho da VM devido a carga adicional, pode tirar partido da CPU e memória que fornece um maior tamanho da VM adicionais. Também tem de discos já num local que pode tomar partido do débito IOPS adicional que permite o maior tamanho da VM.



As tabelas seguintes listam as contagens de inicial do disco sugerido utilize em sites primários e de administração central para várias instalações de tamanho:

**Base de dados colocalizadas site** -site de administração central ou principal com a base de dados do site no servidor do site:

| Clientes de ambiente de trabalho    |Tamanho da VM recomendado|Discos recomendados|
|--------------------|-------------------|-----------------|
|**Até 25k**       |   DS4_V2          |2xP30 (repartidos (striped))  |
|**k de 25 para 50k**      |   DS13_V2         |2xP30 (repartidos (striped))  |
|**k de 50 a 100k**     |   DS14_V2         |3xP30 (repartidos (striped))  |


**Base de dados do site remoto** -site de administração central ou principal com a base de dados do site num servidor remoto:

| Clientes de ambiente de trabalho    |Tamanho da VM recomendado|Discos recomendados |
|--------------------|-------------------|------------------|
|**Até 25k**       | Servidor do site: F4S </br>Servidor de base de dados: DS12_V2 | Servidor do site: 1xP30 </br>Servidor de base de dados: 2xP30 (repartidos (striped))  |
|**k de 25 para 50k**      | Servidor do site: F4S </br>Servidor de base de dados: DS13_V2 | Servidor do site: 1xP30 </br>Servidor de base de dados: 2xP30 (repartidos (striped))   |
|**k de 50 a 100k**     | Servidor do site: F8S </br>Servidor de base de dados: DS14_V2 | Servidor do site: 2xP30 (repartidos (striped))   </br>Servidor de base de dados: 3xP30 (repartidos (striped))   |

O seguinte mostra um exemplo de configuração para clientes de k de 50 a 100k em DS14_V2 com discos de 3xP30 num volume repartidos (striped) com separado lógica volumes para o Configuration Manager instalar e ficheiros de base de dados:  ![Discos de VM)](media/vm_disks.png)  



## <a name="user-experience"></a>Experiência de utilizador
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>Mencionar a experiência de utilizador é uma das áreas principais de importância, por que motivo é que?
As decisões que efetua na rede, disponibilidade, desempenho, e onde colocar os servidores de site do Configuration Manager podem afetar os utilizadores diretamente. Se considerar que uma mudança para o Azure deve ser transparente para os seus utilizadores para que não registam uma alteração na respetiva diárias interações com o Configuration Manager.

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>OK, posso obtê-lo. Planear a instalar um único site primário autónomo na máquina virtual do Azure e quiser certificar-se de que os meus custos são baixos. Deve colocar sistemas de sites (remota) (como pontos de atualização de software, os pontos de distribuição e pontos de gestão) em máquinas virtuais do Azure bem ou no local?
Exceto para comunicação entre o servidor do site e um ponto de distribuição, estas comunicações de servidor para servidor num site podem ocorrer em qualquer altura e não utilizam mecanismos para controlar a utilização da largura de banda de rede. Uma vez que não é possível controlar a comunicação entre sistemas de sites, devem ser considerados quaisquer custos associados estas comunicações.

Velocidades de rede e latência são ainda outros fatores a considerar bem. Redes lentas ou pouco fiáveis podem afetar a funcionalidade entre o servidor de site e sistemas de sites remotos que bem qualquer comunicação de cliente para os sistemas de sites. Também deve ser considerado o número de clientes geridos que utilize um sistema de sites, bem como as funcionalidades que utiliza ativamente.
Em geral, pode tirar partido das orientações normal à medida que se relaciona com ligações WAN e sistemas de sites como um ponto de partida. Idealmente, o débito de rede que seleciona e recebe entre o Azure e a sua intranet serão consistente com uma WAN que está com boas ligações com uma rede rápida.

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>E distribuição de conteúdo e gestão de conteúdo? Devem ser de pontos de distribuição padrão no Azure ou no local e devo utilizar o BranchCache ou pontos de distribuição de solicitação no local? Ou posso fazer utilização exclusiva de pontos de distribuição de nuvem?
A abordagem de gestão de conteúdo é muito iguais aos servidores do site e sistemas de sites.
- Se utilizar uma ligação de rede rápida e fiável entre o Azure e a sua intranet com um plano de dados ilimitado, que está a alojar pontos de distribuição padrão no Azure pode ser uma opção.
-  Se utilizar um custo de plano e a largura de banda de dados medidos for uma preocupação ou a ligação de rede entre o Azure e a sua intranet não é rápida ou pode ser pouco fiável, em seguida, poderá considerar outras abordagens. Estes incluem localizar padrão ou pontos de distribuição de solicitação no local, bem como a utilizar o BranchCache. A utilização de pontos de distribuição baseado na nuvem é também uma opção, mas existem alguns limites para os tipos de conteúdo suportado (por exemplo, sem suporte para pacotes de atualizações de software).

> [!NOTE]
>  Se for necessário suporte PXE, tem de utilizar pontos de distribuição no local (padrão ou solicitação) para responder a pedidos de arranque. [O WDS não é atualmente suportado para executar em VMs do Azure](https://technet.microsoft.com/library/hh831764(v=ws.11).aspx).


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>Enquanto estiver OK com as limitações de pontos de distribuição baseado na nuvem, não pretendo colocar o meu ponto de gestão no DMZ apesar de que é necessário para suportar os meus clientes baseados na Internet. É necessário quaisquer outras opções?
Sim! Com 1610 de versão do Configuration Manager, introduzimos a [nuvem Management Gateway](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) como uma funcionalidade pré-lançamento. (Esta funcionalidade pela primeira vez apareceu na versão de pré-visualização técnica 1606 como o [serviço de nuvem do Proxy](/sccm/core/get-started/capabilities-in-technical-preview-1606#a-namecloudproxyacloud-proxy-service-for-managing-clients-on-the-internet)).

O **nuvem Management Gateway** fornece uma forma simples de gerir clientes do Configuration Manager na Internet. O serviço, que é implementado para o Microsoft Azure e necessita de uma subscrição do Azure, liga-se para a infraestrutura do Configuration Manager no local com uma nova função de denominado o ponto de conector do gateway de gestão na nuvem. Depois de ter implementado e configurado, os clientes podem aceder funções do sistema de sites no local do Configuration Manager independentemente de se se estiver ligados à rede privada interna ou na Internet.

Pode começar a utilizar o gateway de gestão da nuvem no seu ambiente e fornecer comentários para tornar isto melhor. Para obter informações sobre a versão de pré-lançamento funcionalidades, consulte o artigo [utilizar funcionalidades de pré-lançamento das atualizações da](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkprereleasea-use-pre-release-features-from-updates).

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>Também posso ouvido tiver outra funcionalidade nova chamada ponto a ponto Cache introduzido como uma funcionalidade pré-lançamento na versão 1610. Que é diferente do BranchCache? Qual devo escolher?
Sim, completamente diferente. [Elemento Cache](/sccm/core/plan-design/hierarchy/client-peer-cache) é uma tecnologia do Configuration Manager nativo 100% em que o BranchCache é uma funcionalidade do Windows. Tanto podem ser útil por si; O BranchCache utiliza uma difusão para localizar o conteúdo necessário enquanto que a cache de elementos da utiliza gestores de configuração normal de distribuição fluxo de trabalho e limites definições do grupo.

Pode configurar qualquer cliente seja uma origem de Cache ponto a ponto. Em seguida, quando os pontos de gestão permitem aos clientes informações sobre localizações de origem de conteúdo, fornecem detalhes sobre os pontos de distribuição e quaisquer origens de Cache ponto a ponto que possuem o conteúdo que o cliente requer.


## <a name="cost"></a>Custo
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>OK notificar-me um pouco sobre o custo. Esta será uma solução económica para mim?
Disco rígido dizer desde cada ambiente é diferente. A melhor solução é para o ambiente, utilizando o Microsoft Azure preços Calculadora de custos: https://azure.microsoft.com/pricing/calculator/

## <a name="additional-resources"></a>Recursos adicionais
**Noções básicas:** http://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Tipos de máquina VM do Azure:**
 - Azure tamanhos das máquinas: https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs/  
 - Preços de VM: http://azure.microsoft.com/pricing/details/virtual-machines/  
 - Preços de armazenamento: http://azure.microsoft.com/pricing/details/storage/

**Considerações de desempenho de disco:**    
 - Introdução de disco Premium: http://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
 - Informações de disco Premium mais profunda: http://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
 - Destina-se a coleção útil de gráficos para máximo tamanhos e desempenho para o armazenamento: https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
 - Aqui outra + algumas interessantes como funciona o armazenamento Premium atrás o abrange os dados uber-linguagem mais técnica: http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**Disponibilidade:**
 - Do Azure IaaS período de atividade SLA: https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
 - Conjuntos de disponibilidade explicados: https://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability/

**Conectividade:**
 - Express rota vs. Azure VPN: http://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
 - Express rota preços: http://azure.microsoft.com/pricing/details/expressroute/
 - Mais informações sobre rápida rota: http://azure.microsoft.com/documentation/articles/expressroute-introduction/

 


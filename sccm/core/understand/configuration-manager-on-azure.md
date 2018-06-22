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
ms.openlocfilehash: 2b952e76fc21e3190430cdf34cb4a264918fd199
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342601"
---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Perguntas mais frequentes do Configuration Manager no Azure - frequentemente
*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As seguintes perguntas e respostas podem ajudar a compreender quando utilizar e como configurar o Configuration Manager no Microsoft Azure.

## <a name="general-questions"></a>Perguntas gerais
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>A minha empresa está a tentar mover como de vários servidores físicos quanto possível para o Microsoft Azure, pode posso mover servidores do Configuration Manager para o Azure?
Certamente, este é um cenário suportado.  Consulte [suporte para ambientes de Virtualização do System Center Configuration Manager](/sccm/core/plan-design/configs/support-for-virtualization-environments).

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>Ótimo! A minha ambiente requer vários sites. Todos os sites primários subordinados estará no Azure com o site de administração central ou no local? O que sobre sites secundários?
Comunicações de site para site (baseados em ficheiros e replicação de base de dados) beneficia de proximidade de que está a ser alojado no Azure. No entanto, todos os clientes relacionados com o tráfego seria remoto de servidores de site e sistemas de sites. Se utilizar uma ligação de rede rápida e fiável entre o Azure e a sua intranet com um plano de dados ilimitados, alojamento toda a infraestrutura no Azure é uma opção.

No entanto, se utilizar um plano de dados limitados e largura de banda disponível ou custo for uma preocupação, ou a ligação de rede entre o Azure e a sua intranet não é rápida ou pode ser pouco fiável, em seguida, considere colocar sites específicos (e os sistemas de sites) no local e, em seguida, utilize os controlos de largura de banda incorporados no Configuration Manager.

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>Está a ter do Configuration Manager no Azure um cenário de SaaS (Software como serviço)?
Não, é um IaaS (infraestrutura como serviço) porque alojam os servidores de infraestrutura do Configuration Manager em máquinas virtuais do Azure.

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>As áreas deve posso prestar atenção à quando considerar uma mudança da minha infraestrutura do Configuration Manager para o Azure?
Excelente pergunta, seguem-se as áreas que são mais importantes quando efetuar esta decisão, cada um é explorou numa secção separada deste tópico:
1.  Rede
2.  Disponibilidade
3.  Desempenho
4.  Custo
5.  Experiência de utilizador

## <a name="networking"></a>Rede
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>O que sobre os requisitos de rede devo utilizar ExpressRoute ou de um Gateway de VPN do Azure?
Funcionamento em rede é uma decisão muito importante. Velocidades de rede e a latência podem afetar a funcionalidade entre o servidor do site e sistemas de sites remotos e qualquer comunicação do cliente com os sistemas de sites. A nossa recomendação é utilizar o ExpressRoute. Mas não existe nenhuma limitação do Configuration Manager para impedi-lo de utilizar o Gateway de VPN do Azure. Deve verificar com atenção os seus requisitos (desempenho, a aplicação de patches, distribuição de software, implementação do sistema operativo) desta infraestrutura e, em seguida, decidir se. Alguns aspetos a considerar para cada solução incluem:

 - **ExpressRoute** (recomendado)
  - Extensão natural ao seu centro de dados (pode juntar em conjunto vários centros de dados)
  - Ligações privadas entre os datacenters do Azure e a sua infraestrutura
  - Não é aceite através da Internet pública
  - Oferece fiabilidade, velocidades rápidas, latência inferior, alta segurança
  - Ofertas até 10gbps velocidades e as opções do plano de dados ilimitados
 - **Gateway de VPN**
  - Site-site/ponto-a-site VPNs
  - Tráfego que passa através da Internet pública
  - Utiliza a segurança de protocolo de Internet (IPsec) e troca de chaves de Internet (IKE)

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>O ExpressRoute tem muitas opções diferentes, como ilimitados vs. as opções de velocidade limitados, diferentes e suplemento premium. Que devo escolher?
As opções que selecionar dependem do cenário a que se estiver a implementar e quanto dados que pretende distribuir. A transferência de dados do Configuration Manager pode ser controlada entre servidores de site e pontos de distribuição, mas não podem ser controlada comunicações de servidor de site do servidor do site.   Quando utiliza um plano de dados limitados, colocar sites específicos (e os sistemas de sites) no local e utilizar [controlos de largura de banda incorporadas do Configuration Manager](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management) pode ajudar a controlar o custo de utilização do Azure.

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>O que sobre os requisitos de instalação, como os domínios do Active Directory? É ainda necessário associar os meus servidores de site para um domínio do Active Directory?
Sim. Ao mover para o Azure, o [configurações suportadas](/sccm/core/plan-design/configs/supported-configurations) permanecer o mesmo, incluindo requisitos do Active Directory para a instalação do Configuration Manager.

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>Posso compreender a necessidade de associar os meus servidores de site a um domínio do Active Directory, mas posso utilizar o Azure Active Directory?
Não, o Azure Active Directory não é suportado neste momento. Os servidores de sites ainda tem de ser membros de um [domínio do Active Directory do Windows](/sccm/core/plan-design/configs/support-for-active-directory-domains).



## <a name="availability"></a>Disponibilidade
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>Uma das razões que estou a mover a infraestrutura para o Azure é a promessa de elevada disponibilidade. Pode demorar partido das opções de elevada disponibilidade como conjuntos de disponibilidade de VM do Azure para as VMs que irá utilizar o para o Configuration Manager?
Sim! Conjuntos de disponibilidade de VM do Azure podem ser utilizados para funções de sistema de sites redundante como pontos de distribuição ou pontos de gestão.

Também pode utilizá-los para os servidores de site do Configuration Manager. Por exemplo, os sites de administração central e sites primários podem estar no mesmo conjunto de disponibilidade que pode ajudar a garantir que não são reiniciados em simultâneo.

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>Como posso tornar o meu base de dados de elevada disponibilidade? Pode utilizar SQL Database do Azure? Ou, é necessário utilizar o Microsoft SQL Server numa VM?
Terá de utilizar o Microsoft SQL Server numa VM. O Configuration Manager não suporta o Azure SQL Server neste momento. Mas pode utilizar funcionalidades como grupos de Disponibilidade AlwaysOn para o SQL server. [Grupos de Disponibilidade AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database) são recomendadas e oficialmente são suportados a partir da versão 1602 do Configuration Manager.

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>Pode utilizar balanceadores de carga do Azure com funções de sistema de sites, como pontos de gestão ou de pontos de atualização de software?
Enquanto o Configuration Manager não foi testado com balanceadores de carga do Azure, se a funcionalidade é transparente para a aplicação, não deve ter quaisquer efeitos adversos em operações normais.


## <a name="performance"></a>Desempenho
### <a name="what-factors-affect-performance-in-this-scenario"></a>Os fatores que afetam o desempenho neste cenário?
[Tamanho da VM do Azure e o tipo](https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs), VM do Azure (armazenamento premium é recomendado, especialmente para o SQL Server) de discos, funcionamento em rede latência e velocidade são as áreas mais importantes.

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>Por isso, mais informações sobre máquinas virtuais do Azure; as VMs de tamanho devo utilizar?
Em geral, a capacidade de computação (CPU e memória) têm de preencher o [recomendado hardware para o System Center Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware). Mas existem algumas diferenças entre o hardware do computador regular e as VMs do Azure, especialmente quando se trata os discos Utilize estas VMs.  Que tamanho VMs utilizar depende do tamanho do seu ambiente, mas seguem-se algumas recomendações:
- Para implementações de produção de qualquer tamanho significativo Recomendamos "**S**" classe VMs do Azure. Isto acontece porque pode tirar partido dos discos de armazenamento Premium.  Classe de "S" não VMs utilizar armazenamento de BLOBs e em geral será cumpre os requisitos de desempenho necessários para uma experiência de produção aceitável.
- Vários discos de armazenamento Premium devem ser utilizados para uma escala maior e repartidos na consola de gestão de discos do Windows para o IOPS máximo.  
- Recomendamos que utilize melhor ou premium vários discos durante a implementação de site inicial (por exemplo, P30 em vez de P20 e 2xP30 num volume repartido em vez de 1xP30). Em seguida, se o site tiver mais tarde atualizem o tamanho da VM devido a carga adicional, pode tirar partido da CPU e memória que fornece um maior tamanho da VM adicionais. Também tem de discos já no local que pode tirar partido do débito IOPS adicional que permite que o maior tamanho da VM.



As tabelas seguintes listam as contagens de sugeridos inicial do disco para utilizar em sites primários e de administração central para várias instalações de tamanho:

**Base de dados localizadas conjuntamente site** -site de administração central ou primário com a base de dados do site no servidor do site:

| Clientes de ambiente de trabalho    |Tamanho VM recomendado|Discos recomendados|
|--------------------|-------------------|-----------------|
|**Até 25k**       |   DS4_V2          |2xP30 (repartidos)  |
|**25k para 50k**      |   DS13_V2         |2xP30 (repartidos)  |
|**k de k de 50 a 100**     |   DS14_V2         |3xP30 (repartidos)  |


**Base de dados do site remoto** -site de administração central ou primário com a base de dados do site num servidor remoto:

| Clientes de ambiente de trabalho    |Tamanho VM recomendado|Discos recomendados |
|--------------------|-------------------|------------------|
|**Até 25k**       | Servidor do site: F4S </br>Servidor de base de dados: DS12_V2 | Servidor do site: 1xP30 </br>Servidor de base de dados: 2xP30 (repartidos)  |
|**25k para 50k**      | Servidor do site: F4S </br>Servidor de base de dados: DS13_V2 | Servidor do site: 1xP30 </br>Servidor de base de dados: 2xP30 (repartidos)   |
|**k de k de 50 a 100**     | Servidor do site: F8S </br>Servidor de base de dados: DS14_V2 | Servidor do site: 2xP30 (repartidos)   </br>Servidor de base de dados: 3xP30 (repartidos)   |

O seguinte mostra um exemplo de configuração para clientes de k de 50 a 100k em DS14_V2 com discos 3xP30 num volume repartido com separado lógica volumes do Configuration Manager instale e ficheiros de base de dados: ![Discos VM)](media/vm_disks.png)  



## <a name="user-experience"></a>Experiência de utilizador
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>Mencionar a experiência de utilizador é um dos principais áreas de importância, por que motivo é que?
As decisões tomar nas redes, disponibilidade, desempenho e onde colocar os servidores de site do Configuration Manager podem afetar os utilizadores diretamente. Acreditamos que uma mudança para o Azure deve ser transparente para os seus utilizadores para que não registam uma alteração na respetiva interações diárias com o Configuration Manager.

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>OK, posso obtê-lo. Planear a instalar um único site primário autónomo numa máquina virtual do Azure e pretender certificar-se de que a minha custos são baixos. Deve colocar os sistemas de sites (remotos) (como pontos de atualização de software, os pontos de distribuição e pontos de gestão) em máquinas virtuais do Azure, bem como ou no local?
Com exceção da comunicação do servidor do site para um ponto de distribuição, estas comunicações de servidor para servidor num site podem ocorrer em qualquer altura e não utilizam mecanismos para controlar a utilização de largura de banda de rede. Porque não é possível controlar a comunicação entre sistemas de sites, devem ser considerados quaisquer custos associados a estas comunicações.

Velocidades de rede e latência são ainda outros fatores a considerar bem. Redes lentas ou pouco fiáveis pode afetar a funcionalidade entre o servidor do site e sistemas de site remoto como bem qualquer comunicação do cliente com os sistemas de sites. Também deve ser considerado o número de clientes geridos que utilize um sistema de site especificado, bem como as funcionalidades que utiliza ativamente.
Em geral, pode tirar partido de normais como se relaciona com ligações WAN e sistemas de sites como ponto de partida. Idealmente, o débito de rede que selecione e receber entre o Azure e a sua intranet será consistente com uma WAN, que é bem ligada com uma rede rápida.

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>O que sobre a distribuição de conteúdo e gestão de conteúdos? Devem ser de pontos de distribuição padrão no Azure ou no local e deve posso utilizar o BranchCache ou pontos de distribuição de solicitação no local? Ou deverá eu fizer a utilização exclusiva de pontos de distribuição em nuvem?
A abordagem de gestão de conteúdo é muito as mesmas que nos servidores de site e sistemas de sites.
- Se utilizar uma ligação de rede rápida e fiável entre o Azure e a sua intranet com um plano de dados ilimitados, que alojam pontos de distribuição padrão no Azure pode ser uma opção.
-  Se utilizar um custo de plano e a largura de banda de dados limitados for uma preocupação ou a ligação de rede entre o Azure e a sua intranet não é rápida ou pode ser pouco fiável, em seguida, poderá considerar outras abordagens. Estes incluem localizar padrão ou pontos de distribuição de solicitação no local, bem como utilizar o BranchCache. A utilização de pontos de distribuição baseado na nuvem também uma opção, mas existem algumas limites nos tipos de conteúdo suportados (por exemplo, não existe suporte para pacotes de atualizações de software).

> [!NOTE]
>  Se é necessário o suporte PXE, tem de utilizar pontos de distribuição no local (padrão ou solicitação) para responder a pedidos de arranque. [O WDS não é atualmente suportado para ser executada em VMs do Azure](https://technet.microsoft.com/library/hh831764(v=ws.11).aspx).


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>Enquanto sou OK com as limitações de pontos de distribuição baseado na nuvem, não pretendo colocar os meus ponto de gestão no DMZ, apesar do que é necessário para suportar os meus clientes baseados na Internet. É necessário quaisquer outras opções?
Sim! Com 1610 de versão do Configuration Manager, introduzimos a [Gateway de gestão de nuvem](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) como uma funcionalidade de pré-lançamento. (Esta funcionalidade primeiro apareceu na versão de pré-visualização técnica 1606 como o [serviço de Proxy de nuvem](/sccm/core/get-started/capabilities-in-technical-preview-1606#a-namecloudproxyacloud-proxy-service-for-managing-clients-on-the-internet)).

O **Gateway de gestão de nuvem** fornece uma forma simples de gerir clientes do Configuration Manager na Internet. O serviço, que é implementado no Microsoft Azure e requer uma subscrição do Azure, liga-se à sua infraestrutura do Configuration Manager no local através de uma nova função de chamar o ponto de conector de gateway de gestão de nuvem. Depois de ter implementado e configurado, os clientes podem aceder funções do sistema de sites no local do Configuration Manager, independentemente de se estão ligados à rede privada interna ou na Internet.

Pode começar a utilizar o gateway de gestão de nuvem no seu ambiente e envie-nos comentários para tornar esta melhor. Para obter informações sobre as funcionalidades de pré-lançamento, consulte [utilizar as funcionalidades de pré-lançamento das atualizações da](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkprereleasea-use-pre-release-features-from-updates).

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>Posso falar também se tem outra funcionalidade nova denominada a Cache ponto a ponto apresentado como sendo uma funcionalidade de pré-lançamento versão 1610. Que é diferente do BranchCache? Qual delas devo escolher?
Sim, completamente diferente. [Elemento de Cache](/sccm/core/plan-design/hierarchy/client-peer-cache) é uma tecnologia do Configuration Manager nativo 100%, onde o BranchCache é uma funcionalidade do Windows. Ambos podem ser úteis para si; O BranchCache utiliza a difusão para localizar o conteúdo necessário, enquanto que a Cache ponto a ponto utiliza gestores de configuração normal de distribuição fluxo de trabalho e o limite de definições do grupo.

Pode configurar qualquer cliente para que seja uma origem de Cache ponto a ponto. Em seguida, quando pontos de gestão fornecem informações sobre localizações de origem de conteúdo de clientes, fornecem detalhes sobre os pontos de distribuição e quaisquer origens de Cache ponto a ponto que possuem o conteúdo que o cliente requer.


## <a name="cost"></a>Custo
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>OK Informe-me um pouco sobre o custo. Isto poderá ter uma solução económica para mim?
Disco rígido indicar desde cada ambiente é diferente. A melhor coisa a fazer é para o ambiente de utilizar o Microsoft Azure Calculadora de preços:  https://azure.microsoft.com/pricing/calculator/

## <a name="additional-resources"></a>Recursos adicionais
**Noções básicas:** http://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Tipos de máquina VM do Azure:**
 - Tamanhos de máquina do Azure: https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs/  
 - Preços de VM: http://azure.microsoft.com/pricing/details/virtual-machines/  
 - Preços do Storage: http://azure.microsoft.com/pricing/details/storage/

**Considerações de desempenho de disco:**    
 - Introdução do disco Premium:  http://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
 - Informações de disco Premium quanto mais abaixo: http://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
 - Destina-se à mão coleção dos gráficos máximo tamanhos e desempenho para o armazenamento: https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
 - Introdução outra + algumas esporádico dados uber geek em como funciona o Premium Storage atrás bastidores:  http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**Disponibilidade:**
 - Do tempo de atividade de IaaS do Azure SLA: https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
 - Conjuntos de disponibilidade, encontrará uma explicação sobre: https://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability/

**Conectividade:**
 - Express route vs. VPN do Azure: http://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
 - Express Route preços: http://azure.microsoft.com/pricing/details/expressroute/
 - Mais informações sobre o Expressroute: http://azure.microsoft.com/documentation/articles/expressroute-introduction/

 

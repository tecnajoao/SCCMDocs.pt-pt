---
title: Otimizar a entrega de atualização do Windows 10
titleSuffix: Configuration Manager
description: Saiba como utilizar o Configuration Manager para gerir o conteúdo da atualização para se manter atual com o Windows 10.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7e445cd6e49617afde6f8acf043eeb4c707e1480
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/19/2018
ms.locfileid: "36261029"
---
# <a name="optimize-windows-10-update-delivery-with-configuration-manager"></a>Otimizar a entrega de atualização do Windows 10 com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramo atual)*

Para muitos clientes, um caminho com êxito para obter e permanecendo atual com o Windows 10 atualizações mensais começa com uma estratégia de boa distribuição de conteúdo com o Configuration Manager. O tamanho das atualizações de qualidade de mensal pode ser das causas de preocupação para organizações grandes. Existem alguns tecnologias disponíveis que foram concebidas para ajudar a reduzir a carga de rede e largura de banda para otimizar a entrega de atualização. Este artigo explica estas tecnologias, compara-os e fornece recomendações para o ajudar a tomar decisões sobre qual a utilizar.  
 
Windows 10 fornece vários tipos de atualizações. Para obter mais informações, consulte [atualizar os tipos de atualização do Windows para empresas](https://docs.microsoft.com/windows/deployment/update/waas-manage-updates-wufb#update-types). Este artigo incida no Windows 10 *qualidade* atualizações com o Configuration Manager. 


## <a name="express-update-delivery"></a>Expressar a entrega de atualização

Transferências de atualização de qualidade do Windows 10 podem ser elevadas. Cada pacote contém todas as correções lançadas anteriormente para garantir consistência e na simplicidade. Microsoft foi capaz de reduzir o tamanho do conteúdo de atualização do Windows 10 que cada cliente transfere com uma funcionalidade denominada rápida. Express é utilizado atualmente pelo milhões de dispositivos de receber atualizações diretamente a partir do serviço do Windows Update e reduz significativamente o tamanho de transferência. Este benefício também está disponível para clientes cujos clientes diretamente não transferem a partir do serviço do Windows Update. 

O Configuration Manager foi adicionado suporte para [ficheiros de instalação rápida](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates) das atualizações de qualidade do Windows 10 na versão 1702. No entanto, para a melhor experiência é recomendado que utilize o Configuration Manager versão 1802 ou posterior. Para obter o melhor desempenho em velocidades de transferência, também é recomendável que utilize o Windows 10, versão 1703 ou posterior. 

> [!NOTE]  
> O conteúdo de versão expresso é consideravelmente maior do que a versão completa do ficheiro. Um ficheiro de instalação rápida contém todas as possíveis variações para cada ficheiro tem significou para atualizar. Como resultado, a quantidade necessária de espaço em disco aumenta para as atualizações na origem do pacote de atualização e nos pontos de distribuição quando ativar o suporte rápido no Configuration Manager. Apesar do requisito de espaço em disco nos pontos de distribuição aumenta, diminui o tamanho do conteúdo que os clientes transferir estes pontos de distribuição. Os clientes transferem apenas os bits necessitam (deltas), mas não a atualização de toda.



## <a name="peer-to-peer-content-distribution"></a>Distribuição de conteúdo ponto-a-ponto

Apesar dos clientes transferem apenas as partes do conteúdo que necessitam, fim de acelerar a atualizações do Windows no seu ambiente através da utilização de distribuição de conteúdo ponto-a-ponto. Tirar partido dos elementos de rede como uma origem de transferência para atualizações de qualidade pode ser vantajoso para ambientes onde pontos de distribuição local não estão presentes em escritórios remotos. Este comportamento impede a necessidade de todos os clientes transfiram conteúdos a partir de um ponto de distribuição remoto numa ligação WAN lenta. Utilizar os elementos de rede também pode ser vantajoso quando os clientes de contingência para o serviço Windows Update. Apenas um elemento de rede é necessário para transferir conteúdos de atualização a partir da nuvem antes de o tornar disponível para outros dispositivos.

O Configuration Manager suporta muitas tecnologias ponto-a-ponto, incluindo o seguinte:
- Otimização de entrega do Windows
- Cache ponto a ponto do Configuration Manager
- BranchCache do Windows  

As secções seguintes fornecem mais informações sobre estas tecnologias.


### <a name="windows-delivery-optimization"></a>Otimização de entrega do Windows

[Otimização de entrega](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) é o principal de transferência tecnologia e ponto-a-ponto distribuição método incorporado no Windows 10. Clientes Windows 10 podem obter conteúdos de outros dispositivos na sua rede local que transferir as mesmas atualizações. Utilizar o [opções do Windows disponíveis para a otimização de entrega](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#delivery-optimization-options), pode configurar os clientes em grupos. Este agrupamento permite que a sua organização identificar dispositivos candidatos possivelmente o melhor para satisfazer os pedidos de ponto a ponto. Otimização de entrega reduz significativamente a largura de banda global que é utilizada para manter os dispositivos atualizados ao acelerar o tempo de transferência.

> [!NOTE]  
> Otimização de entrega é uma solução de nuvem gerido. Acesso à Internet para o serviço de nuvem de otimização de entrega é um requisito para utilizar a funcionalidade de ponto a ponto.  

Para obter os melhores resultados, poderá ser necessário definir a otimização de entrega [transferir modo](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#download-mode) para **grupo (2)** e definir *os IDs de grupo*. No modo de grupo, peering pode cruzada sub-redes internas entre os dispositivos que pertencem ao mesmo grupo, incluindo dispositivos em escritórios remotos. Utilize o [opção de ID do grupo](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#select-the-source-of-group-ids) para criar o seu próprio grupo personalizado independentemente domínios e sites do AD DS. O modo de transferência de grupo é a opção recomendada na maioria das organizações procura para alcançar a otimização de largura de banda melhor com otimização de entrega.

Configurar manualmente estes IDs de grupo é um desafio quando os clientes sejam acedidas remotamente em redes diferentes. O Configuration Manager versão 1802 adicionada uma nova funcionalidade para simplificar a gestão deste processo por [integrar os grupos de limites com otimização de entrega](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization). Quando um cliente é reativado, sua para o respetivo ponto de gestão para obter as políticas e fornece as informações de grupo de limites e de rede. O Configuration Manager cria um ID exclusivo para cada grupo de limites. O site utiliza informações de localização do cliente para configurar automaticamente o ID do grupo de otimização de entrega do cliente com o ID de limites do Configuration Manager. Quando o cliente fizer roaming para outro grupo de limites, é sua para o respetivo ponto de gestão e é automaticamente reconfigurado com um ID de grupo de limites. Esta integração, otimização de entrega podem utilizar as informações de grupo de limites do Configuration Manager para localizar um elemento de rede a partir das quais transferir as atualizações.


### <a name="configuration-manager-peer-cache"></a>Cache ponto a ponto do Configuration Manager

[Elemento de cache](/sccm/core/plan-design/hierarchy/client-peer-cache) é uma funcionalidade do Configuration Manager que permite que os clientes partilhar com outros conteúdos de clientes diretamente a partir da respetiva cache local do Configuration Manager. Cache ponto a ponto não substitui a utilização de outra soluções como o Windows BranchCache a colocação em cache ponto a ponto. Funciona em conjunto com-los para fornecer mais opções para expandir as soluções de implementação de conteúdos tradicionais, como pontos de distribuição. Cache ponto a ponto não confie em BranchCache. Se não ativar ou utilizar o BranchCache, cache ponto a ponto ainda funciona.

> [!NOTE]  
> Os clientes só podem transferir conteúdo de clientes de cache ponto a ponto que se encontrem no respetivo grupo de limites atuais.  


### <a name="windows-branchcache"></a>BranchCache do Windows
[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) é uma tecnologia de otimização de largura de banda no Windows. Cada cliente tem uma cache e age como uma origem de conteúdo alternativo. Dispositivos na mesma rede podem solicitar este conteúdo. [O Configuration Manager podem utilizar o BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache) para permitir que os elementos de rede para o conteúdo de origem umas das outras versus sempre ter de contactar um ponto de distribuição. Utilizar o BranchCache, os ficheiros são colocadas em cache em cada cliente individuais e outros clientes podem obtê-las conforme necessário. Esta abordagem distribui a cache, em vez de ter um único ponto de recuperação. Este comportamento guarda uma quantidade significativa da largura de banda, reduzindo o tempo para que os clientes recebem o conteúdo pedido. 



## <a name="selecting-the-right-peer-caching-technology"></a>Selecionar o elemento à direita tecnologia a colocação em cache

Selecionar o elemento de rede adequado a tecnologia de ficheiros de instalação rápida a colocação em cache depende do seu ambiente e requisitos. Apesar do Configuration Manager suporta todas as tecnologias ponto a ponto acima, deve utilizar o que fazer mais sentido para o seu ambiente. Para a maioria dos clientes, pressupondo que os clientes podem satisfazer os requisitos de internet para a otimização de entrega, o elemento incorporado do Windows 10 a colocação em cache com otimização de entrega deve ser suficiente. Se os clientes não cumpram estes requisitos de internet, considere utilizar a funcionalidade de cache ponto a ponto do Configuration Manager. Se estiver atualmente a utilizar o BranchCache com o Configuration Manager e cumpre todas as suas necessidades, em seguida, rápidos ficheiros com o BranchCache podem ser a opção adequada para si. 

### <a name="peer-cache-comparison-chart"></a>Gráfico de comparação de cache ponto a ponto


| Funcionalidade  | Otimização de entrega  | Cache ponto a ponto  | BranchCache  |
|---------|---------|---------|---------|
| Suportada entre sub-redes | Sim | Sim | Não |
| Limitação de largura de banda | Sim (nativo) | Sim (através de BITS) | Sim (através de BITS) |
| Suporte de conteúdo parcial | Sim | Apenas para Office 365 e atualizações rápidas | Sim |
| Tamanho da cache no controlo de disco | Sim | Sim | Sim |
| Deteção de uma origem ponto a ponto | Automática | Manual (agente de cliente definição) | Automática |
| Deteção de ponto a ponto | Através do serviço de nuvem de otimização de entrega (requer acesso à internet) | Através do ponto de gestão (com base nos grupos de limites do cliente) | Difusão |
| Relatórios | Sim (utilizando o Microsoft Operations Management Suite) | Dashboard de origens de dados de cliente do ConfigMgr | Dashboard de origens de dados de cliente do ConfigMgr |
| Controlo de utilização WAN | Sim (nativo, que pode ser controlado através de definições de política de grupo) | Grupos de limites | Suporte de sub-rede apenas |
| Tipos de conteúdo suportados | -Express atualizações (através do ConfigMgr)</br> -As atualizações de segurança e Windows</br> -Controladores</br> -Aplicações da loja Windows</br> -Loja Windows para as aplicações da empresa | Todos os tipos de conteúdo do ConfigMgr, incluindo as imagens de transferido em [do Windows PE](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic) | Todos os tipos de conteúdo do ConfigMgr, exceto as imagens |
| Gestão através do ConfigMgr | Parcial (agente de cliente definição) | Sim (agente de cliente definição) | Sim (agente de cliente definição) |



## <a name="conclusion"></a>Conclusão

A Microsoft recomenda que otimizar a entrega de atualização de qualidade do Windows 10 com o Configuration Manager com ficheiros de instalação rápida e um elemento de colocação em cache tecnologia, conforme necessário. Esta abordagem deve aliviar os desafios associados a dispositivos Windows 10 transferir conteúdo grande para instalar atualizações de qualidade. Também é recomendável manter os dispositivos Windows 10 atual ao implementar atualizações de qualidade de cada mês. Esta prática reduz o delta do conteúdo de atualização de qualidade necessário pelos dispositivos de cada mês. Reduzir este conteúdo delta faz com que as transferências de tamanho mais pequenas de pontos de distribuição ou as origens de ponto a ponto. 

Devido à natureza dos ficheiros de instalação rápida, tamanho do conteúdo é consideravelmente maior do que o conteúdo do ficheiro de completo tradicional. Este tamanho resulta em mais tempos de transferência de atualização do serviço do Windows Update para o servidor de site do Configuration Manager. Também aumenta a quantidade de espaço em disco necessário para ambos os sites servidor e pontos de distribuição. O total de tempo necessário para transferir e distribuir atualizações de qualidade pode ser mais longo. No entanto, as vantagens do lado do dispositivo devem ser considerável durante a transferência e instalação de atualizações de qualidade pelos dispositivos Windows 10.

Se fala do lado do servidor de atualizações de tamanho maior é identificar bloqueadores a adoção de suporte rápida, mas os benefícios do lado do dispositivo são críticos para o seu negócio e o ambiente, a Microsoft recomenda que utilize [Windows Update for Business](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10) com o Configuration Manager. Atualização do Windows para empresas fornece todos os benefícios do express sem a necessidade de transferir, armazenar e distribuir os ficheiros de instalação rápida em todo o seu ambiente. Os clientes transferem conteúdo diretamente a partir do serviço do Windows Update, deste modo, pode continuar a utilizar a otimização de entrega.



## <a name="bkmk_faq"></a> Perguntas mais frequentes

#### <a name="how-do-windows-express-downloads-work-with-configuration-manager"></a>Como é que Windows express transferências trabalho com o Configuration Manager?

Os Windows update agent (WUA) pedidos express conteúdo primeiro. Se não conseguir instalar a atualização rápida, pode reverter para a atualização de ficheiro completo.  

1. O cliente do Configuration Manager indica WUA para transferir o conteúdo da atualização. Quando o WUA inicia uma transferência rápida, transfere primeiro um stub (por exemplo, `Windows10.0-KB1234567-<platform>-express.cab`), que faz parte do pacote rápido.  

2. WUA passa Este stub para o Windows update installer, baseado em componentes (CBS) de manutenção. CBS utiliza o stub para fazer um inventário local, comparar deltas de ficheiros nos dispositivos com o que é necessária para obter a versão mais recente do ficheiro a ser oferecido.  

3. Em seguida, CBS pede-lhe WUA para transferir os intervalos necessários a partir de um ou mais ficheiros .psf rápida.  

4. Otimização de entrega coordena com o Configuration Manager e transfere os intervalos de um ponto de distribuição local ou elementos, se disponível. Se a otimização de entrega estiver desativada, o serviço de transferência inteligente em segundo plano (BITS) é utilizado da mesma forma com o Configuration Manager em coordenação origens de cache ponto a ponto. Otimização de entrega ou BITS transmite os intervalos para WUA, que disponibiliza-los CBS aplicam-se e instalar.  


#### <a name="why-are-the-express-files-psf-so-large-when-stored-on-configuration-manager-peer-sources-in-the-ccmcache-folder"></a>Por que razão são tão elevado quando armazenados em origens de ponto a ponto do Configuration Manager na pasta ccmcache os ficheiros rápidos (.psf)?

Os ficheiros rápidos (.psf) são ficheiros dispersos. Para determinar o espaço real que está a ser utilizado no disco pelo ficheiro, verifique o **tamanho do disco** propriedade do ficheiro. O tamanho na propriedade de disco deve ser significativamente menor do que o valor de tamanho.  


#### <a name="does-configuration-manager-support-express-installation-files-with-windows-10-feature-updates"></a>O Configuration Manager suporta ficheiros de instalação rápida com atualizações de funcionalidade do Windows 10?

Não, Configuration Manager atualmente só suporta ficheiros de instalação rápida com atualizações de qualidade do Windows 10.  


#### <a name="how-much-disk-space-is-needed-per-quality-update-on-the-site-server-and-distribution-points"></a>Quanto espaço em disco é necessário por atualização de qualidade nos pontos de servidor e a distribuição de sites?

Depende. Para cada atualização de qualidade, a versão completa do ficheiro e rápida da atualização estão armazenados nos servidores. Atualizações de qualidade do Windows 10 são cumulativas, pelo que o tamanho desses ficheiros aumenta de cada mês. Planear um mínimo de 5 GB por atualizações por idioma. 


#### <a name="do-configuration-manager-clients-still-benefit-from-express-installation-files-when-falling-back-to-the-windows-update-service"></a>Clientes do Configuration Manager ainda beneficiar de ficheiros de instalação rápida ao reverter para o serviço Windows Update?

Sim. Se utilizar a opção de implementação de atualização de software seguinte, em seguida, os clientes ainda utilizam atualizações rápidas e a otimização de entrega quando revertem para o serviço em nuvem:  

**Se as atualizações de software não estão disponíveis no ponto de distribuição na atual, vizinho ou site grupos, transferir o conteúdo das Updates da Microsoft**


#### <a name="why-is-express-file-content-not-downloaded-for-existing-updates-after-i-enable-express-file-support"></a>Por que motivo o conteúdo do ficheiro rápida não é transferido para atualizações existentes depois de ativar o suporte de ficheiros rápida? 

As alterações apenas em vigor para novas atualizações sincronizadas e implementado depois de ativar o suporte.


#### <a name="is-there-any-way-to-see-how-much-content-is-downloaded-from-peers-using-delivery-optimization"></a>Existe qualquer forma de ver a quantidade conteúdo é transferido a partir através da otimização de entrega de elementos de rede?
Windows 10, versão 1703 (e posterior) inclui dois novos cmdlets do PowerShell, **Get-DeliveryOptimizationPerfSnap** e **Get-DeliveryOptimizationStatus**. Estes cmdlets fornecem mais ampla de utilização de otimização de entrega e a cache. Para obter mais informações, consulte [cmdlets Windows PowerShell para a análise da utilização](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#windows-powershell-cmdlets-for-analyzing-usage)


#### <a name="how-do-clients-communicate-with-delivery-optimization-over-the-network"></a>Como os clientes comunicam com otimização de entrega através da rede?
Para obter mais informações sobre as portas de rede, os requisitos de proxy e os nomes de anfitrião para firewalls, consulte [perguntas mais frequentes para a otimização de entrega](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).


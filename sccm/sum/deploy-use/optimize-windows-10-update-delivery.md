---
title: Otimizar a entrega de atualizações do Windows 10
titleSuffix: Configuration Manager
description: Saiba como utilizar o Configuration Manager para gerir o conteúdo da atualização para se manter atualizado com o Windows 10.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92ac9cbfd8b4c68a818a3988c0ce1f3ec26a2215
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139175"
---
# <a name="optimize-windows-10-update-delivery-with-configuration-manager"></a>Otimize a entrega de atualização do Windows 10 com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramo atual)*

Para muitos clientes, um caminho com êxito para a obtenção e mantendo-se atualizado com o Windows 10 atualizações mensais começa com uma estratégia de distribuição de conteúdo bom com o Configuration Manager. O tamanho das atualizações de qualidade mensal pode ser motivo de preocupação para grandes organizações. Há algumas tecnologias disponíveis que têm a finalidade de ajudar a reduzir a carga de rede e largura de banda para otimizar a entrega de atualização. Este artigo explica essas tecnologias, compara-os e fornece recomendações para o ajudar a tomar decisões sobre qual usar.  
 
Windows 10 fornece vários tipos de atualizações. Para obter mais informações, consulte [atualizar tipos no Windows Update para empresas](https://docs.microsoft.com/windows/deployment/update/waas-manage-updates-wufb#update-types). Este artigo se concentra no Windows 10 *qualidade* atualizações com o Configuration Manager. 


## <a name="express-update-delivery"></a>Expressar a entrega de atualização

Downloads de atualização de qualidade do Windows 10 podem ser grandes. Cada pacote contém todas as correções lançadas anteriormente para garantir a consistência e a simplicidade. A Microsoft conseguiu reduzir o tamanho do conteúdo de atualização do Windows 10 que transfere a cada cliente com um recurso chamado express. Express é usado atualmente por milhões de dispositivos que receber atualizações diretamente a partir do serviço do Windows Update e reduz significativamente o tamanho do download. Este benefício também está disponível para clientes cujos clientes não transferirem diretamente do serviço Windows Update. 

O Configuration Manager foi adicionado suporte para [ficheiros de instalação rápida](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates) de atualizações de qualidade do Windows 10 na versão 1702. No entanto, a melhor experiência é recomendado que utilize o Configuration Manager versão 1802 ou posterior. Para obter o melhor desempenho em velocidades de download, também é recomendado que utilize o Windows 10, versão 1703 ou posterior. 

> [!NOTE]  
> O conteúdo de versão express é consideravelmente maior do que a versão completa do ficheiro. Um ficheiro de instalação rápida contém todas as variações possíveis para cada ficheiro tem a função de atualização. Como resultado, a quantidade necessária de espaço em disco aumenta para atualizações na origem do pacote de atualização e nos pontos de distribuição quando ativar o suporte expresso no Configuration Manager. Embora o requisito de espaço em disco nos pontos de distribuição aumenta, diminui o tamanho do conteúdo que os clientes transferem a partir desses pontos de distribuição. Os clientes transferem apenas os bits que exigem (deltas), mas não a atualização de toda.



## <a name="peer-to-peer-content-distribution"></a>Distribuição de conteúdo do ponto-a-ponto

Apesar dos clientes transferem apenas as partes do conteúdo que eles precisam, agilizar a atualizações do Windows no seu ambiente utilizando a distribuição de conteúdo ponto-a-ponto. Tirar partido dos itens de mesmo nível, como uma origem de transferência para as atualizações de qualidade pode ser vantajoso para ambientes onde os pontos de distribuição local não estão presentes em escritórios remotos. Este comportamento impede a necessidade de todos os clientes transfiram conteúdos a partir de um ponto de distribuição remoto num link WAN lento. Usar elementos de rede também pode ser benéfico quando contingência para o serviço de atualização do Windows. Apenas um elemento de rede é necessário para transferir conteúdos de atualização a partir da cloud antes de disponibilizá-lo para outros dispositivos.

O Configuration Manager suporta muitas tecnologias de ponto-a-ponto, incluindo o seguinte:
- Otimização da entrega do Windows
- Cache de elemento de rede do Configuration Manager
- BranchCache do Windows  

As secções seguintes fornecem mais informações sobre essas tecnologias.


### <a name="windows-delivery-optimization"></a>Otimização da entrega do Windows

[Otimização da entrega](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) é a principal tecnologia e ponto-a-ponto distribuição método download incorporado ao Windows 10. Os clientes do Windows 10 podem obter o conteúdo de outros dispositivos na sua rede local que transferir as mesmas atualizações. Utilizar o [opções de Windows disponíveis para a otimização de entrega](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#delivery-optimization-options), pode configurar os clientes em grupos. Este agrupamento permite que a sua organização a identificar os dispositivos, possivelmente, são os melhores candidatos para satisfazer os pedidos de ponto-a-ponto. Otimização da entrega reduz significativamente a largura de banda geral que é utilizada para manter os dispositivos atualizados ao acelerar o tempo de transferência.

> [!NOTE]  
> Otimização da entrega é uma solução gerida na cloud. Acesso à Internet para o serviço de nuvem de Otimização da entrega é um requisito para utilizar a sua funcionalidade de ponto-a-ponto.  

Para obter melhores resultados, poderá ter de definir a otimização de entrega [modo de transferência](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#download-mode) ao **grupo (2)** e defina *IDs de grupo*. No modo de grupo, peering pode cruzar sub-redes internas entre os dispositivos que pertencem ao mesmo grupo, incluindo os dispositivos em escritórios remotos. Utilize o [opção de ID de grupo](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#select-the-source-of-group-ids) para criar seu próprio grupo personalizado, independentemente dos domínios e sites de AD DS. Modo de transferência de grupo é a opção recomendada na maioria das organizações que procuram para alcançar a melhor otimização de largura de banda com a otimização de entrega.

Configurar manualmente estes IDs de grupo é um desafio quando os clientes de mensagens em fila sejam acedidas remotamente em redes diferentes. O Configuration Manager versão 1802 adicionou uma nova funcionalidade para simplificar a gestão deste processo por [a integração de grupos de limites com otimização de entrega](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization). Quando um cliente torna-se ativo, ele se comunica com o ponto de gestão para obter as políticas e fornece as informações de grupo de limites de rede e. O Configuration Manager cria uma ID exclusiva para cada grupo de limites. O site utiliza informações de localização do cliente para configurar automaticamente o ID de grupo de otimização de entrega do cliente com o ID de limite do Configuration Manager. Quando o cliente fizer roaming para outro grupo de limites, ele se comunica com o ponto de gestão e é automaticamente reconfigurado com um novo ID de grupo de limites. Com esta integração, a Otimização da entrega pode utilizar as informações do grupo de limites do Configuration Manager para localizar um elemento de rede a partir do qual pretende transferir atualizações.


### <a name="configuration-manager-peer-cache"></a>Cache de elemento de rede do Configuration Manager

[Configurar o peering em cache](/sccm/core/plan-design/hierarchy/client-peer-cache) é uma funcionalidade do Configuration Manager que permite que os clientes partilhem com outros conteúdos de clientes diretamente a partir de seu cache local do Configuration Manager. Cache ponto a ponto não substitui a utilização de outra soluções, como o Windows BranchCache a colocação em cache de ponto a ponto. Ele funciona em conjunto com-los para fornecer mais opções para estender as soluções de implementação de conteúdos tradicionais, como pontos de distribuição. Cache ponto a ponto não contam com BranchCache. Se não ativar ou utilizar o BranchCache, cache ponto a ponto ainda funciona.

> [!NOTE]  
> Os clientes só podem transferir conteúdo de clientes de cache ponto a ponto que estão no seu grupo de limites atual.  


### <a name="windows-branchcache"></a>BranchCache do Windows
[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) é uma tecnologia de otimização de largura de banda no Windows. Cada cliente tem um cache e atue como uma origem alternativa para o conteúdo. Dispositivos na mesma rede podem solicitar este conteúdo. [O Gestor de configuração pode utilizar o BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache) para permitir que os colegas para conteúdo de origem uns dos outros versus sempre ter de contactar um ponto de distribuição. Utilizar o BranchCache, ficheiros são colocados em cache em cada cliente individual, e outros clientes podem obtê-las conforme necessário. Essa abordagem distribui o cache, em vez de ter um único ponto de recuperação. Este comportamento economiza uma quantidade significativa de largura de banda, reduzindo o tempo para que os clientes recebem o conteúdo solicitado. 



## <a name="selecting-the-right-peer-caching-technology"></a>Selecionar o elemento de rede certo a tecnologia de colocação em cache

Selecionar o elemento de rede certo tecnologia para ficheiros de instalação rápida de colocação em cache depende do seu ambiente e requisitos. Mesmo que o Configuration Manager suporta todas as tecnologias de ponto-a-ponto acima, deve usar as pessoas que fazem mais sentido para o seu ambiente. Para a maioria dos clientes, partindo do princípio de que os clientes podem satisfazer os requisitos de internet para a otimização de entrega, a Windows 10 incorporada ponto a ponto colocação em cache com otimização de entrega deve ser suficiente. Se seus clientes não é possível cumprir estes requisitos de internet, considere utilizar a funcionalidade de cache ponto a ponto do Configuration Manager. Se estiver atualmente a utilizar o BranchCache com o Configuration Manager e ele atende a todas as suas necessidades, em seguida, arquivos express com o BranchCache podem ser a opção certa para. 

### <a name="peer-cache-comparison-chart"></a>Gráfico de comparação de cache ponto a ponto


| Funcionalidade  | Otimização da entrega  | Cache ponto a ponto  | BranchCache  |
|---------|---------|---------|---------|
| Suportado em sub-redes | Sim | Sim | Não |
| Limitação de largura de banda | Sim (nativo) | Sim (através do BITS) | Sim (através do BITS) |
| Suporte de conteúdo parcial | Sim | Apenas para Office 365 e atualizações rápidas | Sim |
| Tamanho da cache no controle de disco | Sim | Sim | Sim |
| Deteção de uma origem ponto a ponto | automática | Manual (definição do agente cliente) | automática |
| Descoberta de mesmo nível | Por meio do serviço de nuvem de Otimização da entrega (requer acesso à internet) | Através do ponto de gestão (com base em grupos de limites do cliente) | Multicast |
| Relatórios | Sim (com o Windows Analytics) | Dashboard de origens de dados de cliente do ConfigMgr | Dashboard de origens de dados de cliente do ConfigMgr |
| Controlo de utilização WAN | Sim (nativo, que pode ser controlado através das definições de política de grupo) | Grupos de limites | Apenas suporte de sub-rede |
| Tipos de conteúdo suportados | -Express atualizações (por meio do ConfigMgr)</br> -Windows e atualizações de segurança</br> -Drivers</br> -Aplicações Windows Store</br> -Windows Store para aplicações empresariais | Todos os tipos de conteúdo do ConfigMgr, incluindo as imagens baixadas na [Windows PE](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic) | Todos os tipos de conteúdo do ConfigMgr, exceto imagens |
| Gestão através do ConfigMgr | Parcial (definição do agente cliente) | Sim (definição do agente cliente) | Sim (definição do agente cliente) |



## <a name="conclusion"></a>Conclusão

A Microsoft recomenda que Otimize a entrega de atualizações de qualidade de Windows 10 com o Configuration Manager com ficheiros de instalação rápida e uma ponto a ponto, tecnologia, a colocação em cache conforme necessário. Essa abordagem deve minimizar os desafios associados a dispositivos Windows 10 a transferir conteúdo de grande para a instalação de atualizações de qualidade. Também é recomendável a manter os dispositivos Windows 10 atual ao implementar atualizações de qualidade de cada mês. Esta prática reduz o delta de conteúdo de atualização de qualidade necessário por dispositivos de cada mês. Reduzir este conteúdo delta faz com que significa transferências mais pequenas tamanho dos pontos de distribuição ou origens de ponto a ponto. 

Devido à natureza dos ficheiros de instalação rápida, o tamanho do conteúdo é consideravelmente maior do que o conteúdo do ficheiro de completo tradicional. Este tamanho resulta em mais tempos de transferência de atualização do serviço Windows Update para o servidor de site do Configuration Manager. Também aumenta a quantidade de espaço em disco necessário para ambos os os site server e pontos de distribuição. Tempo total necessário para baixar e distribuir atualizações de qualidade pode ser mais tempo. No entanto, os benefícios do lado do dispositivo devem ser perceptíveis durante a transferência e instalação de atualizações de qualidade pelos dispositivos Windows 10.

Se as compensações do lado do servidor de atualizações de tamanho maior são fatores que impedem a para a adoção do suporte express, mas os benefícios do lado do dispositivo são fundamentais para a sua empresa e o ambiente, a Microsoft recomenda que use [Windows Update para empresas](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10) com o Configuration Manager. Windows Update para empresas fornece todos os benefícios do express sem a necessidade de transferir, armazenar e distribuir os arquivos de instalação rápida em todo o seu ambiente. Os clientes transferem conteúdo diretamente a partir do serviço do Windows Update, portanto, pode continuar a utilizar Otimização da entrega.



## <a name="bkmk_faq"></a> Perguntas mais frequentes

#### <a name="how-do-windows-express-downloads-work-with-configuration-manager"></a>Como é que Windows express os downloads do trabalho com o Configuration Manager?

Os Windows agent (WUA) pedidos express conteúdo de atualização em primeiro lugar. Se não conseguir instalar a atualização rápida, pode reverter para a atualização completa do ficheiro.  

1. O cliente do Configuration Manager informa ao WUA para transferir o conteúdo da atualização. Quando o WUA inicia uma transferência rápida, primeiro transfere um stub (por exemplo, `Windows10.0-KB1234567-<platform>-express.cab`), que é parte do pacote do express.  

2. WUA passa Este stub para o instalador de atualização do Windows, baseado em componentes (CBS) de manutenção. CBS utiliza o stub para fazer um inventário local, comparando os deltas de arquivo nos dispositivos com o que é necessário para obter a versão mais recente do ficheiro a ser oferecido.  

3. CBS, em seguida, pede WUA para transferir os intervalos necessários a partir de um ou mais ficheiros express .psf.  

4. Otimização da entrega coordena com o Configuration Manager e transfere os intervalos de um ponto de distribuição local ou elementos se estiver disponível. Se a Otimização da entrega estiver desativada, o serviço de transferência inteligente em segundo plano (BITS) é utilizado da mesma forma com o Configuration Manager coordenar origens da cache ponto a ponto. Otimização da entrega ou BITS transmite os intervalos para WUA, que disponibiliza-os para CBS aplicam-se e instalar.  


#### <a name="why-are-the-express-files-psf-so-large-when-stored-on-configuration-manager-peer-sources-in-the-ccmcache-folder"></a>Por que os ficheiros express (.psf) são tão grandes, quando armazenada em origens de ponto a ponto do Configuration Manager na pasta ccmcache?

Os ficheiros express (.psf) são ficheiros dispersos. Para determinar o espaço real a ser utilizado no disco pelo ficheiro, verifique os **tamanho no disco** propriedade do ficheiro. O tamanho na propriedade do disco deve ser consideravelmente menor do que o valor de tamanho.  


#### <a name="does-configuration-manager-support-express-installation-files-with-windows-10-feature-updates"></a>O Configuration Manager suporta ficheiros de instalação rápida com atualizações de funcionalidades do Windows 10?

Não, o Configuration Manager atualmente apenas suporta ficheiros de instalação rápida com atualizações de qualidade do Windows 10.  


#### <a name="how-much-disk-space-is-needed-per-quality-update-on-the-site-server-and-distribution-points"></a>Quanto espaço em disco é necessário por atualização de qualidade nos pontos de distribuição e o servidor de site?

Depende. Para cada atualização de qualidade, a versão completa do ficheiro e rápida da atualização são armazenados nos servidores. As atualizações de qualidade do Windows 10 são cumulativas, pelo que o tamanho desses ficheiros aumenta a cada mês. Planear um mínimo de 5 GB por atualização por idioma. 


#### <a name="do-configuration-manager-clients-still-benefit-from-express-installation-files-when-falling-back-to-the-windows-update-service"></a>Clientes do Configuration Manager continua a beneficiar os ficheiros de instalação rápida ao reverter para o serviço de atualização do Windows?

Sim. Se utilizar a opção de implementação de atualização de software seguintes, em seguida, os clientes ainda utilizam express atualizações e a otimização de entrega quando os clientes revertem para o serviço em nuvem:  

**Se as atualizações de software não estão disponíveis no ponto de distribuição na atual, vizinho ou do site de grupos, transfira o conteúdo do Microsoft Updates**


#### <a name="why-is-express-file-content-not-downloaded-for-existing-updates-after-i-enable-express-file-support"></a>Por que o conteúdo do ficheiro express não é transferido para atualizações existentes depois de ativar o suporte a arquivo express? 

As alterações apenas em vigor para novas atualizações sincronizadas e implementado depois de ativar o suporte.


#### <a name="is-there-any-way-to-see-how-much-content-is-downloaded-from-peers-using-delivery-optimization"></a>Existe alguma forma para ver a quantidade de conteúdo é transferido a partir de elementos de rede com otimização de entrega?
Windows 10, versão 1703 (e posterior) inclui dois novos cmdlets do PowerShell, **Get-DeliveryOptimizationPerfSnap** e **Get-DeliveryOptimizationStatus**. Estes cmdlets fornecem mais informações sobre a utilização de otimização de entrega e a cache. Para obter mais informações, consulte [cmdlets do Windows PowerShell para analisar a utilização](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#windows-powershell-cmdlets-for-analyzing-usage)


#### <a name="how-do-clients-communicate-with-delivery-optimization-over-the-network"></a>Como os clientes comunicam com otimização de entrega através da rede?
Para obter mais informações sobre as portas de rede, requisitos de proxy e nomes de anfitriões para firewalls, consulte [FAQs sobre a Otimização da entrega](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).


---
title: CMG FAQ
description: Utilize este artigo para responder a perguntas mais frequentes sobre sobre o gateway de gestão de nuvem
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: 8615b28735165650a0ec25e3d3114263835803d6
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Perguntas mais frequentes sobre o gateway de gestão de nuvem

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo responde às perguntas frequentes sobre o gateway de gestão de nuvem. Para obter mais informações, consulte [plano para gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="frequently-asked-questions"></a>Perguntas mais frequentes

### <a name="what-certificates-do-i-need"></a>Certificados de que preciso?

Para obter mais informações, consulte [certificados para o gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).


### <a name="do-i-need-azure-expressroute"></a>É necessário Azure ExpressRoute?

[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) permite-lhe expandir a sua rede no local para a nuvem da Microsoft. ExpressRoute ou outras essas ligações de rede virtual não são necessários para o gateway de gestão de nuvem do Configuration Manager. A estrutura do gateway de gestão na nuvem permite que os clientes baseados na internet comunicam através do serviço do Azure para sistemas de sites no local com nenhuma configuração de rede adicionais. Para obter mais informações, consulte [planear para o gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)

Se a sua organização utilizar o ExpressRoute, é melhor prática de segurança isolar a subscrição do Azure para o gateway de gestão de nuvem. Esta configuração assegura que o serviço de gateway de gestão de nuvem não está ligado acidentalmente desta forma. Para obter mais informações, consulte [segurança e privacidade para o gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway).


### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>É necessário manter as máquinas virtuais do Azure?

Não é necessária nenhuma manutenção. A estrutura do gateway de gestão de nuvem utiliza a plataforma do Azure como um serviço (PaaS). Utilizar a subscrição que está a fornecer, o Configuration Manager cria o necessárias máquinas virtuais (VMs), armazenamento e redes. Azure protege e atualiza a máquina virtual. Estas VMs não são uma parte do seu ambiente no local, como é o caso de infraestrutura como serviço (IaaS). O gateway de gestão de nuvem é uma PaaS que expande o seu ambiente do Configuration Manager para a nuvem. 


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Já estiver a utilizar IBCM. Se adicionar CMG, como os clientes se comportarão?

Se já implementado [gestão de clientes baseados na internet](/sccm/core/clients/manage/plan-internet-based-client-management) (IBCM), também pode implementar o gateway de gestão de nuvem. Os clientes recebem a política para ambos os serviços. Como são utilizados em roaming para a internet, estes aleatoriamente selecionem e utilizam um destes serviços baseados na internet.


## <a name="next-steps"></a>Passos seguintes

- [Planear o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Configurar o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Certificados para o gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Segurança e privacidade para o gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Tamanho da gestão do gateway de nuvem e números de escala](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
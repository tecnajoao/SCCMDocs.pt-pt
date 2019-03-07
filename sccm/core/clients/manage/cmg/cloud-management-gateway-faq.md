---
title: FAQ DO CMG
description: Utilize este artigo para responder a perguntas mais frequentes sobre sobre o gateway de gestão da nuvem
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4cbb9b37c951c490c1f2245f089fa22707f4c220
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558019"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Perguntas mais frequentes sobre o gateway de gestão da cloud

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo responde as perguntas mais frequentes sobre o gateway de gestão na cloud. Para obter mais informações, consulte [plano para o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="frequently-asked-questions"></a>Perguntas mais frequentes

### <a name="what-certificates-do-i-need"></a>Quais certificados é necessário?

Para obter mais informações, consulte [certificados para o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).


### <a name="do-i-need-azure-expressroute"></a>Preciso que o Azure ExpressRoute?

[O Azure ExpressRoute](/azure/expressroute/expressroute-introduction) permite-lhe expandir a sua rede no local para a cloud da Microsoft. ExpressRoute ou outros tais conexões de rede virtual não são necessários para o gateway de gestão de nuvem do Configuration Manager. O design do gateway de gestão na cloud permite que os clientes baseados na internet comuniquem através do serviço do Azure para sistemas de sites no local sem qualquer configuração de rede adicional. Para obter mais informações, consulte [planear para o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)

Se sua organização utiliza o ExpressRoute, é recomendado de segurança isolar a subscrição do Azure para o gateway de gestão na cloud. Esta configuração torna-se de que o serviço de gateway de gestão de cloud acidentalmente não está ligado dessa maneira. Para obter mais informações, consulte [segurança e privacidade para o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway).


### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>É necessário manter as máquinas virtuais do Azure?

Sem manutenção é necessária. O design do gateway de gestão na cloud utiliza a plataforma do Azure como um serviço (PaaS). Utilizar a subscrição que é fornecer, o Configuration Manager cria o necessárias máquinas virtuais (VMs), armazenamento e rede. O Azure protege e atualiza a máquina virtual. Estas VMs não são uma parte do seu ambiente no local, assim como acontece com a infraestrutura como serviço (IaaS). O gateway de gestão da cloud é uma PaaS que estende o ambiente do Configuration Manager para a cloud. 

### <a name="how-can-i-ensure-service-continuity-during-service-updates"></a>Como garantir a continuidade do serviço durante as atualizações de serviço?

Através do dimensionamento CMG para incluir duas ou mais instâncias, automaticamente se beneficiar da atualização de domínios no Azure. Ver [como atualizar um serviço em nuvem](/azure/cloud-services/cloud-services-update-azure-service).


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Já estou usando IBCM. Se eu adicionar CMG, como os clientes a se comportar?

Se já implementado [gestão de clientes baseados na internet](/sccm/core/clients/manage/plan-internet-based-client-management) (IBCM), também pode implementar o gateway de gestão na cloud. Os clientes recebem a política para ambos os serviços. Como são utilizados em roaming para a internet, eles aleatoriamente selecione e utilizam um destes serviços baseados na internet.


### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-subscription-as-the-subscription-that-hosts-the-cmg-cloud-service"></a>As contas de utilizador tem de estar na mesma subscrição do Azure que a subscrição que anfitriões CMG serviço em nuvem?
<!--SCCMDocs-pr issue #2873--> Se o ambiente tiver mais de uma subscrição, pode implementar CMG para qualquer subscrição que pode hospedar serviços cloud do Azure. 

Essa pergunta é comum nos seguintes cenários:  

- Quando tiver teste distinto e ambientes de produção do Active Directory e o Azure AD, mas um único e centralizada a hospedagem de subscrição do Azure  

- A utilização do Azure cresceu orgânica entre as diferentes equipes  

Quando estiver a utilizar uma implementação do Resource Manager, integrar o Azure AD associado de inquilino. Esta ligação permite ao Configuration Manager para autenticar para o Azure para criar, implementar e gerir o CMG.  

Se estiver a utilizar autenticação do Azure AD para os utilizadores e dispositivos geridos através do CMG, carregar esse inquilino do Azure AD. Para obter mais informações sobre os serviços do Azure para gestão na cloud, consulte [dos serviços do Azure configurar](/sccm/core/servers/deploy/configure/azure-services-wizard). Quando carregar cada inquilino do Azure AD, uma única CMG pode fornecer autenticação do Azure AD para vários inquilinos, independentemente da localização de alojamento.



## <a name="next-steps"></a>Passos seguintes

- [Planear o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Configurar o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Certificados para o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Segurança e privacidade para o gateway de gestão na cloud ](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Tamanho do gateway de gestão da cloud e dimensione números](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)

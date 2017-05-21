---
title: "Utilizar serviços em nuvem com o Configuration Manager | Documentos do Microsoft"
description: Aprovisionar recursos de nuvem para o System Center Configuration Manager para completar a sua infraestrutura no local.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0d7ddd48cc4e75b12f893e686b847d66058441e1
ms.openlocfilehash: 52f7c63d155d5c34f0f12e13020767dec1867dab
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="use-cloud-services-with-system-center-configuration-manager"></a>Utilizar serviços cloud com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager suporta várias opções baseado na nuvem. Estas podem complementar a sua infraestrutura no local e podem ajudar a resolver problemas de empresas, como:  

-   Como gerir BYOD (através do Intune para gestão de dispositivos móveis).  

-   Como fornecer recursos conteúdos aos clientes isolados ou recursos na intranet, fora da sua firewall empresarial (utilizando pontos de distribuição baseado na nuvem).  

-   Como ampliar infraestrutura ao hardware físico não está disponível ou não é colocado logicamente para suportar as suas necessidades (através da utilização de máquinas virtuais do Microsoft Azure).  

Embora o aprovisionamento de recursos de nuvem não é algo que tem de fazer antes da implementação do Configuration Manager, pode ser vantajoso compreender estas opções antes de a evoluir muito distante num plano de estrutura de hierarquia. A utilização de recursos de nuvem poderá poupar dinheiro e a hora, ao resolver problemas de empresas que infraestrutura no local não é possível.  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Recursos baseados em nuvem, que pode utilizar com o Configuration Manager  
 Uma vez que cada opção tem requisitos diferentes, investigue cada um mais detalhadamente para compreender os pré-requisitos exclusivos, limitações e possibilidade de custos adicionais com base na utilização.  

-   Para obter informações sobre pontos de distribuição baseado na nuvem, consulte o artigo [instalar pontos de distribuição baseado na nuvem](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure).

-   Para obter mais informações sobre o Azure, consulte o artigo [Azure](http://go.microsoft.com/fwlink/p/?LinkId=262965) na biblioteca da MSDN.  

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Máquinas virtuais do Azure (por infraestrutura baseada na nuvem)  
 Suporta o do Configuration Manager utilizando a computadores que são executados em máquinas virtuais no Azure, tal como quando é executado no local na rede da sua empresa físico. Pode utilizar máquinas virtuais do Azure nos seguintes cenários:  

-   **Cenário 1:** Pode executar o Configuration Manager numa máquina virtual e utilizá-lo a gerir os clientes instalados no outras máquinas virtuais.  

-   **Cenário 2:** Pode executar o Configuration Manager numa máquina virtual e utilizá-la para gerir clientes que não estão em execução no Azure.  

-   **Cenário 3:** Pode executar diferentes funções de sistema de sites do Configuration Manager em máquinas virtuais, durante a execução de outras funções na sua rede empresarial física (com conectividade de rede adequada para comunicações).  

Os mesmos requisitos de redes, sistemas operativos e os requisitos de hardware que se aplicam ao instalar o Configuration Manager na sua rede empresarial físico também se aplicam a instalação do Configuration Manager no Azure.  

Uma subscrição do Azure é necessário para utilizar máquinas virtuais do Azure. Implicar custos com base no número de máquinas virtuais que utiliza, as respetivas configuração e utilização de recursos baseados em nuvem.  

Além disso, sites do Configuration Manager e os clientes que são executados em máquinas virtuais do Azure estão sujeitos os mesmos requisitos de licença que instalações no local.  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Serviços do Azure (para os pontos de distribuição baseado na nuvem)  
 Pode utilizar um serviço do Azure para alojar um ponto de distribuição do Configuration Manager, que é designado por um ponto de distribuição baseado na nuvem chamado. Pode [utilizar um ponto de distribuição baseado na nuvem com o System Center Configuration Manager](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) juntamente com os pontos de distribuição no local e os pontos de distribuição implementada em máquinas virtuais do Azure.  

 Isto é diferente de utilizar uma máquina virtual do Azure, na qual implementa uma função de sistema de sites. Pontos de distribuição baseado na nuvem:  

-   É executado como um serviço no Azure, não numa máquina virtual.  

-   Dimensione automaticamente para satisfazer o aumento dos pedidos de conteúdo a partir de clientes.  

-   Suporte de clientes na Internet e intranet.  

É necessária uma subscrição do Azure para utilizar o Azure para alojar pontos de distribuição. Incorrer tarifas com base na quantidade de dados transferidos para e do serviço.  

### <a name="microsoft-intune-for-mobile-device-management"></a>Microsoft Intune (gestão de dispositivos móveis)  
 Pode integrar com o Configuration Manager para ativar a gestão de dispositivos utilizando o serviço Intune a sua subscrição do Microsoft Intune. Esta integração:  

-   Chama-se uma configuração híbrida, e expande o Configuration Manager (ou o Intune, consoante a sua perspetiva) para suportar uma grande variedade de dispositivos.  

-   Requer a função de sistema de sites do Microsoft Intune Connector.  

-   Requer que tenha uma subscrição do Intune separada com licenças suficientes para os dispositivos que irá gerir com o Intune.  

Embora o Intune utiliza o Azure, não necessita que configure independentemente do Azure, nem são sujeito a custos adicionais para além de que a subscrição do Intune.  

### <a name="additional-configuration-manager-capabilities"></a>Capacidades adicionais do Configuration Manager  
 Algumas funcionalidades do Configuration Manager podem ligar para serviços baseados na nuvem, como:  

-   Windows Server Update Services (WSUS).  

-   A nuvem de serviço do Configuration Manager, para transferir atualizações para o Configuration Manager.  

Estas capacidades adicionais não requerem que tenha uma subscrição do Azure. Não tem de configurar ligações específicas, certificados ou serviços na nuvem. Em vez disso, estes são geridos automaticamente pelo Configuration Manager para si. Tudo o que precisa de fazer é Certifique-se os sistemas de sites aplicável e dispositivos podem aceder aos URLs baseado na Internet.  

##  <a name="BKMK_CloudSec"></a>Segurança para serviços baseados na nuvem  
 O Configuration Manager utiliza certificados para aprovisionar e aceder ao conteúdo do Azure e para gerir os serviços que utiliza. O Configuration Manager encripta os dados que armazena no Azure, mas não introduz segurança adicional nem dados controlos para além dos fornecidos pelo Azure.  

 Para mais informações, consulte os detalhes para os cenários de recurso diferente baseado na nuvem. Também pode ver os tópicos seguintes para segurança do Azure:  

-   [Azure: Compreender a gestão de conta de segurança no Azure](http://go.microsoft.com/fwlink/p/?LinkId=262968)  

-   [Descrição geral da segurança do Azure](http://go.microsoft.com/fwlink/p/?LinkId=262970)  

-   [Get Past Crossroads a segurança na migração para a sua nuvem](http://go.microsoft.com/fwlink/p/?LinkId=262971)  

-   [Segurança de dados no Azure parte 1 de 2](http://go.microsoft.com/fwlink/p/?LinkId=262974)  


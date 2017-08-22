---
title: "Utilizar serviços em nuvem com o Configuration Manager | Microsoft Docs"
description: Aprovisionar a recursos de nuvem para o System Center Configuration Manager, para complementar a sua infraestrutura no local.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 52f7c63d155d5c34f0f12e13020767dec1867dab
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="use-cloud-services-with-system-center-configuration-manager"></a>Utilizar serviços cloud com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager suporta várias opções baseadas na nuvem. Estes podem completam a sua infraestrutura no local e podem ajudar a resolver problemas empresariais, como:  

-   Como gerir BYOD (utilizando o Intune para gestão de dispositivos móveis).  

-   Como fornecer recursos de conteúdo aos clientes isolados ou recursos na intranet, fora da sua firewall empresarial (utilizando pontos de distribuição baseado na nuvem).  

-   Como ampliar a infraestrutura quando não está disponível hardware físico, ou não está colocado logicamente para suportar as suas necessidades (através da utilização de máquinas virtuais do Microsoft Azure).  

Embora o aprovisionamento de recursos na nuvem não seja algo que deverá fazer antes de implementar o Configuration Manager, pode ser vantajoso compreender estas opções antes de evoluir demasiado num plano de estrutura de hierarquia. A utilização de recursos de nuvem poderá poupar dinheiro e tempo, ao resolver problemas empresariais que infraestrutura no local não é possível.  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Recursos baseados na nuvem, que pode utilizar com o Configuration Manager  
 Uma vez que cada opção tem requisitos diferentes, investigue cada um mais detalhadamente para compreender os pré-requisitos exclusivos, limitações e possibilidade de custos adicionais com base na utilização.  

-   Para obter informações sobre pontos de distribuição baseado na nuvem, consulte [instalar pontos de distribuição baseado na nuvem](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure).

-   Para obter mais informações sobre o Azure, consulte [Azure](http://go.microsoft.com/fwlink/p/?LinkId=262965) na biblioteca da MSDN.  

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Máquinas virtuais do Azure (para a infraestrutura baseada na nuvem)  
 O Configuration Manager suporta através de computadores que são executados em máquinas virtuais no Azure, tal como é executado no local dentro da sua rede empresarial física. Pode utilizar máquinas virtuais do Azure nos seguintes cenários:  

-   **Cenário 1:** Pode executar o Configuration Manager numa máquina virtual e utilizá-lo para gerir clientes instalados noutras máquinas virtuais.  

-   **Cenário 2:** Pode executar o Configuration Manager numa máquina virtual e utilizá-lo para gerir clientes que não estão em execução no Azure.  

-   **Cenário 3:** Pode executar diferentes funções do sistema de sites do Configuration Manager em máquinas virtuais, enquanto executa outras funções na sua rede empresarial física (com conectividade de rede adequada a comunicações).  

Os mesmos requisitos para redes, sistemas operativos e requisitos de hardware aplicáveis à instalação do Configuration Manager na sua rede empresarial física também são aplicáveis à instalação do Configuration Manager no Azure.  

É necessária uma subscrição do Azure para utilizar máquinas virtuais do Azure. Pode implicar custos com base no número de máquinas virtuais que utiliza, respetiva configuração e utilização de recursos baseados na nuvem.  

Além disso, sites do Configuration Manager e os clientes que são executados em máquinas virtuais do Azure estão sujeitos os mesmos requisitos de licença que as instalações no local.  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Serviços do Azure (para pontos de distribuição baseados na nuvem)  
 Pode utilizar um serviço do Azure para alojar um ponto de distribuição do Configuration Manager, que é chamado um ponto de distribuição baseado na nuvem chamado. Pode [utilizar um ponto de distribuição baseado na nuvem com o System Center Configuration Manager](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) juntamente com pontos de distribuição no local e pontos de distribuição implementados em máquinas virtuais do Azure.  

 Isto é diferente de utilizar uma máquina virtual do Azure, na qual implementa uma função de sistema de sites. Pontos de distribuição baseado na nuvem:  

-   Execute como um serviço no Azure, não numa máquina virtual.  

-   Automaticamente dimensionada para satisfazer os pedidos de conteúdo maior de clientes.  

-   Suporte de clientes na Internet e intranet.  

É necessária uma subscrição do Azure para utilizar o Azure para alojar pontos de distribuição. Pode implicar custos com base na quantidade de dados transferidos para e do serviço.  

### <a name="microsoft-intune-for-mobile-device-management"></a>Microsoft Intune (para gestão de dispositivos móveis)  
 Pode integrar com o Configuration Manager para ativar a gestão de dispositivos ao utilizar o serviço do Intune a sua subscrição do Microsoft Intune. Esta integração:  

-   É denominada configuração híbrida, e expande o Configuration Manager (ou o Intune, dependendo da sua perspetiva) para suportar uma grande variedade de dispositivos.  

-   Requer a função de sistema de sites do Microsoft Intune Connector.  

-   Requer que tenha uma subscrição separada do Intune com licenças suficientes para os dispositivos que irá gerir com o Intune.  

Apesar do Intune utiliza o Azure, que não é necessário para configurar o Azure independentemente, nem está sujeito a custos adicionais além da subscrição do Intune.  

### <a name="additional-configuration-manager-capabilities"></a>Capacidades adicionais do Configuration Manager  
 Algumas capacidades do Configuration Manager podem ligar a serviços baseados na nuvem, como:  

-   Windows Server Update Services (WSUS).  

-   A nuvem de serviço do Configuration Manager, para transferir atualizações para o Configuration Manager.  

Estas capacidades adicionais não requerem que tenha uma subscrição do Azure. Não tem de configurar ligações específicas, certificados ou serviços na nuvem. Em vez disso, são geridas automaticamente pelo Configuration Manager para si. Tudo o que precisa de fazer é Certifique-se de sistemas de sites aplicáveis e dispositivos podem aceder os URLs baseado na Internet.  

##  <a name="BKMK_CloudSec"></a>Segurança para serviços baseados na nuvem  
 Configuration Manager utiliza certificados para aprovisionar e aceder ao conteúdo do Azure e para gerir os serviços que utiliza. O Configuration Manager encripta os dados que armazena no Azure, mas não introduz segurança adicional nem dados controlos para além dos fornecidos pelo Azure.  

 Para obter mais informações, consulte os detalhes para os cenários de diferentes recursos baseados na nuvem. Também pode ver os seguintes tópicos para segurança do Azure:  

-   [Azure: Noções sobre a gestão de conta de segurança no Azure](http://go.microsoft.com/fwlink/p/?LinkId=262968)  

-   [Descrição geral de segurança do Azure](http://go.microsoft.com/fwlink/p/?LinkId=262970)  

-   [Get Past Crossroads a segurança na migração para a sua nuvem](http://go.microsoft.com/fwlink/p/?LinkId=262971)  

-   [Segurança de dados no Azure parte 1 de 2](http://go.microsoft.com/fwlink/p/?LinkId=262974)  

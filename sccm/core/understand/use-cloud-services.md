---
title: Utilizar os serviços cloud para complementar a infraestrutura no local
titleSuffix: Configuration Manager
description: Aprovisionar recursos de nuvem do System Center Configuration Manager, para complementar a sua infraestrutura no local.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe4e1c83f4079e0df959563ac8209a98983b8d90
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132460"
---
# <a name="use-cloud-services-with-system-center-configuration-manager"></a>Utilizar serviços cloud com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager suporta várias opções baseadas na nuvem. Estas podem complementar a sua infraestrutura no local e podem ajudar a resolver problemas empresariais, como:  

-   Como gerir BYOD (ao utilizar o Intune para gestão de dispositivos móveis).  

-   Como fornecer recursos de conteúdo aos clientes isolados ou recursos na intranet, fora da sua firewall empresarial (utilizando pontos de distribuição baseado na nuvem).  

-   Como ampliar a infraestrutura quando não está disponível hardware físico, ou não é colocado logicamente para suportar as suas necessidades (ao utilizar as máquinas virtuais do Microsoft Azure).  

Embora o aprovisionamento de recursos de cloud não é algo que deverá fazer antes de implementar o Configuration Manager, pode ser vantajoso compreender estas opções antes de evoluir demasiado num plano de estrutura de hierarquia. A utilização de recursos da nuvem poderá poupar dinheiro e tempo, ao resolver problemas empresariais que a infraestrutura no local não é possível.  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Recursos baseados na nuvem, que pode utilizar com o Configuration Manager  
 Uma vez que cada opção tem requisitos diferentes, investigue cada um mais detalhadamente para compreender os pré-requisitos exclusivos, limitações e possibilidade de custos adicionais com base na utilização.  

-   Para informações sobre pontos de distribuição baseado na nuvem, consulte [instalar pontos de distribuição baseado na nuvem](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure).

-   Para obter mais informações sobre o Azure, consulte [Azure](http://go.microsoft.com/fwlink/p/?LinkId=262965) na biblioteca MSDN.  

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Máquinas virtuais do Azure (para a infraestrutura baseada na nuvem)  
 Do Configuration Manager suporta a utilização de computadores que são executados em máquinas virtuais no Azure, tal como é executado no local dentro da sua rede empresarial física. Pode utilizar máquinas virtuais do Azure nos seguintes cenários:  

-   **Cenário 1:** Pode executar o Configuration Manager numa máquina virtual e utilizá-lo para gerir clientes instalados noutras máquinas virtuais.  

-   **Cenário 2:** Pode executar o Configuration Manager numa máquina virtual e utilizá-lo para gerir clientes que não estão em execução no Azure.  

-   **Cenário 3:** Pode executar diferentes funções de sistema de sites do Configuration Manager em máquinas virtuais, enquanto executa outras funções na sua rede empresarial física (com conectividade de rede adequada a comunicações).  

Os mesmos requisitos para redes, sistemas operativos e requisitos de hardware aplicáveis à instalação do Configuration Manager na sua rede empresarial física também se aplicam à instalação do Configuration Manager no Azure.  

Uma subscrição do Azure é necessário para utilizar máquinas virtuais do Azure. Pode implicar encargos com base no número de máquinas virtuais que utiliza, configuração e utilização de recursos baseados na nuvem.  

Além disso, sites do Configuration Manager e os clientes que são executados em máquinas virtuais do Azure estão sujeitos aos mesmos requisitos de licença que as instalações no local.  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Serviços do Azure (para pontos de distribuição baseado na nuvem)  
 Pode utilizar um serviço do Azure para alojar um ponto de distribuição do Configuration Manager, que é chamado de um ponto de distribuição baseado na nuvem chamado. Pode [utilizar um ponto de distribuição baseado na nuvem com o System Center Configuration Manager](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) juntamente com pontos de distribuição no local e pontos de distribuição implementados em máquinas virtuais do Azure.  

 Isto é diferente de utilizar uma máquina virtual do Azure, na qual implementa uma função de sistema de sites. Pontos de distribuição baseado na nuvem:  

-   Execute como um serviço no Azure, não numa máquina virtual.  

-   Dimensione automaticamente para satisfazer o aumento dos pedidos de conteúdo de clientes.  

-   Suportar clientes na Internet e intranet.  

Uma subscrição do Azure é necessário para utilizar o Azure para alojar pontos de distribuição. Pode implicar encargos com base na quantidade de dados transferidos de e para o serviço.  

### <a name="microsoft-intune-for-mobile-device-management"></a>Microsoft Intune (gestão de dispositivos móveis)  
 Pode integrar a sua subscrição do Microsoft Intune com o Configuration Manager para ativar a gestão de dispositivos com o serviço do Intune. Esta integração:  

-   É denominada configuração híbrida, e se estende o Configuration Manager (ou o Intune, consoante a sua perspetiva) para suportar uma grande variedade de dispositivos.  

-   Requer a função de sistema de sites do Microsoft Intune Connector.  

-   Requer que tenha uma subscrição separada do Intune com licenças suficientes para os dispositivos que pretende gerir com o Intune.  

Embora o Intune utiliza o Azure, não requer que configure independentemente o Azure, nem está sujeito a custos adicionais para além do que a subscrição do Intune.  

### <a name="additional-configuration-manager-capabilities"></a>Capacidades adicionais do Configuration Manager  
 Algumas funcionalidades do Configuration Manager podem ligar a serviços baseados na nuvem, como:  

-   Windows Server Update Services (WSUS).  

-   A cloud de serviço do Configuration Manager, para transferir atualizações para o Configuration Manager.  

Estas capacidades adicionais não requerem que tenha uma subscrição do Azure. Não é preciso configurar ligações específicas, certificados ou serviços na cloud. Em vez disso, eles são geridos automaticamente pelo Configuration Manager para. Tudo o que precisa fazer é garantir que os sistemas de sites aplicáveis e os dispositivos podem aceder as URLs baseado na Internet.  

##  <a name="BKMK_CloudSec"></a> Segurança para serviços baseados na nuvem  
 Configuration Manager utiliza certificados para aprovisionar e aceder ao conteúdo do Azure e para gerir os serviços que utilizar. O Configuration Manager encripta os dados que armazena no Azure, mas não introduz segurança adicional nem dados controlos para além dos fornecidos pelo Azure.  

 Para obter mais informações, consulte os detalhes para os cenários de recursos diferente com base na cloud. Também pode ver os seguintes tópicos para segurança do Azure:  

-   [Azure: Compreender a gestão de conta de segurança no Azure](http://go.microsoft.com/fwlink/p/?LinkId=262968)  

-   [Descrição geral da segurança do Azure](http://go.microsoft.com/fwlink/p/?LinkId=262970)  

-   [Ultrapassar o Crossroads de segurança na migração para a Cloud](http://go.microsoft.com/fwlink/p/?LinkId=262971)  

-   [Segurança de dados no Azure parte 1 de 2](http://go.microsoft.com/fwlink/p/?LinkId=262974)  

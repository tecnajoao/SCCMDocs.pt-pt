---
title: Escolher uma solução de gestão de dispositivos
titleSuffix: Configuration Manager
description: Saiba mais sobre as soluções que o Configuration Manager oferece para a gestão de PCs, servidores e dispositivos.
ms.date: 01/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2b396ad5955227494511355f6efdb88ecd901110
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120836"
---
# <a name="choose-a-device-management-solution-for-configuration-manager"></a>Escolher uma solução de gestão de dispositivos para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager oferece diferentes soluções para o gerenciamento de PCs, servidores e dispositivos. Escolha a solução certa para a sua organização. Basear a sua decisão nas plataformas de dispositivos, que tem de gerir e a funcionalidade de gestão necessário.  


> [!Important]  
> A partir de 14 de Agosto de 2018, gestão de dispositivos móveis híbrida é um [funcionalidade preterida](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para obter mais informações, consulte [o que é a MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  
<!-- SCCMDocs issue 1197 -->



## <a name="overview"></a>Descrição Geral

Este artigo abrange as seguintes soluções de gestão de dispositivos de quatro: 
- [Cliente do Configuration Manager](#bkmk_sccm)
- [Gestão de dispositivos móveis (MDM) com o Configuration Manager no local](#bkmk_opmdm)
- [Cogestão com o Microsoft Intune](#bkmk_intune)
- [Microsoft Exchange](#bkmk_opmdm)

Pode utilizar estas soluções de gestão de dispositivos individualmente ou em combinação entre si. Por exemplo, pode utilizar a abordagem de gestão baseada no cliente para gerir computadores e servidores na sua organização e também utilizar a cogestão para gerir computadores portáteis baseado na internet. Ao combinar abordagens desta forma, pode cobrir todas as suas necessidades de gestão do dispositivo.  

O artigo também inclui duas tabelas que comparam as soluções de gestão pelos seguintes fatores: 
- [Compare por plataformas suportadas](#bkmk_comp1)
- [Comparar funcionalidades de gestão](#bkmk_comp2)


### <a name="bkmk_sccm"></a> Cliente do Configuration Manager  

Esta opção requer a instalação do cliente do Configuration Manager em dispositivos. Fornece a maior parte das funcionalidades de gestão de PCs, servidores e outros dispositivos no seu ambiente. 

Para obter mais informações, consulte [métodos de instalação de cliente](/sccm/core/clients/deploy/plan/client-installation-methods).  


### <a name="bkmk_opmdm"></a> MDM no local  

Esta opção utiliza as capacidades de gestão de dispositivos incorporadas ao Windows 10. Embora não tão completa em como gestão baseada no cliente, a gestão de dispositivos móveis no local fornece uma abordagem mais ligeira à gestão. Ele usa recursos do Configuration Manager no local para gerir dispositivos.  

Para obter mais informações, consulte [gerir dispositivos móveis com a infraestrutura no local](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  


### <a name="bkmk_comanage"></a> Cogestão com o Microsoft Intune

A cogestão é uma das formas de ligar a sua implementação do Configuration Manager existente para a cloud do Microsoft 365 primárias. Permite-lhe ao mesmo tempo gerir dispositivos Windows 10 com o Configuration Manager e o Microsoft Intune. A cogestão permite que anexe na cloud de seu investimento existente no Configuration Manager ao adicionar novas funcionalidades. 

Para obter mais informações, consulte [o que é a cogestão?](/sccm/comanage/overview).  


### <a name="bkmk_exchange"></a> Microsoft Exchange  

Esta opção utiliza o conector do Exchange Server para ligar vários servidores do Exchange para o Configuration Manager. Isso centraliza a gestão de dispositivos que pode ligar ao Exchange ActiveSync. Pode configurar funcionalidades de gestão de dispositivos móveis do Exchange da consola do Configuration Manager. Recursos de exemplo incluem o apagamento remoto de dispositivo e o controlo de definições para vários servidores do Exchange.

Para obter mais informações, consulte [gerir dispositivos móveis com o Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



## <a name="bkmk_comp1"></a> Comparar soluções de plataformas suportadas  

|Plataforma|Cliente do Configuration Manager|MDM no local|Configuration Manager com o Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Android| | |Sim|  
|iOS| | |Sim|  
|Mac OS X|Sim| |Sim|  
|UNIX/Linux|Sim| |Sim|  
|Windows 10|Sim|Sim|Sim|  
|Windows 10 Mobile| |Sim|Sim|  
|Windows (versões anteriores)|Sim| |Sim|  
|Windows Server|Sim| |Sim|  
|Windows CE|Sim (com cliente legacy de dispositivo móvel)| |Sim|  
|Windows Embedded|Sim| | |  
|Windows Mobile| | |Sim|  

Para obter uma lista completa das plataformas suportadas, consulte [sistemas operativos suportados por clientes e dispositivos para o System Center Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md).

A Microsoft recomenda utilizar o Intune para gerir dispositivos móveis Android, iOS e Windows 10. Para obter mais informações, consulte [o que é o Microsoft Intune?](https://docs.microsoft.com/intune/what-is-intune)



##  <a name="bkmk_comp2"></a> Compare as soluções por uma funcionalidade de gestão  

|Funcionalidade de gestão|Cliente do Configuration Manager|MDM no local|Configuration Manager com o Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Segurança da infraestrutura de chaves públicas (PKI) entre o dispositivo móvel e o Configuration Manager (utiliza a autenticação mútua e o SSL para encriptar transferências de dados)|Sim|Sim| |  
|Instalação do cliente|Sim| | |  
|Suporte através da internet|Sim| | |  
|Deteção|Sim| |Sim|  
|Inventário de Hardware|Sim|Sim|Sim|  
|Inventário de software|Sim| |Sim|  
|Definições|Sim|Sim|Sim|  
|Implementação de software|Sim|Sim| |  
|Monitorizar com ponto de estado de contingência|Sim| | |  
|Ligações a pontos de gestão|Sim|Sim| |  
|Ligações a pontos de distribuição|Sim|Sim| |  
|O bloco do Configuration Manager|Sim|Sim| |  
|Quarentena e bloqueio a partir do Exchange Server (e o Configuration Manager)| | |Sim|  
|Eliminação remota| |Sim|Sim|  



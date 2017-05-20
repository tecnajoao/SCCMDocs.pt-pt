---
title: "Escolha uma solução de gestão do dispositivo - Gestor de configuração | Documentos do Microsoft"
description: "Saiba mais sobre as soluções que disponibiliza o System Center Configuration Manager para gerir PCs, servidores e dispositivos."
ms.custom: na
ms.date: 12/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
caps.latest.revision: 14
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 3eb48942c1259d2aa1b3c200fad73b39b11c0b8c
ms.openlocfilehash: 9989ea1bf4cb74a6286ebae9de7614ed622de5b6
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>Escolher uma solução de gestão de dispositivos para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager (também conhecido como ConfgMgr ou SCCM) oferece soluções diferentes para gerir PCs, servidores e dispositivos. Pode escolher a solução que é mais adequada para si, com base nas plataformas de dispositivo que tem de gerir e a funcionalidade de gestão que terá de.  


##  <a name="overview-of-device-management-solutions"></a>Descrição geral de soluções de gestão de dispositivos  
 Este artigo abrange quatro soluções de gestão de dispositivos: a aplicação de cliente do Configuration Manager, na infraestrutura no local do Configuration Manager, Microsoft Intune e Exchange. O artigo concludes com duas tabelas que comparam as soluções de gestão, uma com base no [suportados plataformas de dispositivos móveis](#compare-device-management-solutions-based-on-supported-mobile-device-platforms)e outra com base no [funcionalidade de gestão](#compare-mobile-device-management-solutions-based-on-management-functionality).


###  <a name="manage-devices-with-the-configuration-manager-client"></a>Gerir dispositivos com o cliente do Configuration Manager  

Esta opção, que requer a instalação da aplicação de cliente do Configuration Manager nos dispositivos, fornece a maioria das funcionalidades para gerir PCs, servidores e outros dispositivos no seu ambiente. Para obter mais informações, consulte o artigo [métodos de instalação de cliente no System Center Configuration Manager](/sccm/core/clients/deploy/plan/client-installation-methods).  

###  <a name="manage-devices-with-on-premises-configuration-manager-infrastructure"></a>Gerir dispositivos com a infraestrutura do Configuration Manager no local  

Esta opção utiliza as capacidades de gestão de dispositivos contempla os sistemas operativos dos algumas plataformas de dispositivo. Enquanto não como todas as funcionalidades como a gestão baseadas no cliente, gestão de dispositivos móveis no local fornece uma abordagem de toque mais clara para a gestão através da utilização de recursos no local do Configuration Manager para alcançar e gerir dispositivos. Tenha em atenção que esta opção é atualmente suportada apenas para dispositivos Windows 10 PCs e Windows 10 Mobile.  

Para obter mais informações, consulte o artigo [gerir dispositivos móveis com a infraestrutura no local no System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

###  <a name="manage-devices-with-microsoft-intune-hybrid"></a>Gerir dispositivos com o Microsoft Intune (híbrido)  

Esta opção utiliza o Microsoft Intune para inscrever e gerir dispositivos, em vez de utilizar recursos de no local do Configuration Manager. Apesar do Intune gere os dispositivos, aceder às suas tarefas de gestão na consola do Configuration Manager. Esta opção suporta todos os sistemas de operativos de dispositivos móveis principais, incluindo o Windows 10 Mobile, Windows Phone, iOS, Mac OS X e Android. Também fornece gestão para os computadores Windows 8.1 e Windows 10 na sua organização.  

Para obter mais informações, veja [Gestão de dispositivos móveis (MDM) híbrida com o System Center Configuration Manager e o Microsoft Intune](../../mdm/understand/hybrid-mobile-device-management.md).  

###  <a name="manage-devices-with-microsoft-exchange"></a>Gerir dispositivos com o Microsoft Exchange  

Esta opção utiliza o conector do Exchange Server para ligar vários servidores do Exchange para o Configuration Manager. Isto centralizes gestão de dispositivos que pode ligar ao Exchange ActiveSync. Pode configurar funcionalidades de gestão de dispositivos móveis do Exchange, como eliminação remota do dispositivo e o controlo de definições para vários servidores do Exchange, a partir da consola do Configuration Manager.  

Para obter mais informações, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

Pode utilizar estas soluções de gestão de dispositivos, isoladamente ou combinados entre si. Por exemplo, pode utilizar a abordagem de gestão baseados no cliente para gerir computadores e servidores na sua organização e também utilizar o Intune para gerir dispositivos móveis. Por combinando abordagens desta forma, podem abranger todas as suas necessidades de gestão de dispositivos a partir da consola do Configuration Manager.  

## <a name="compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a>Comparar soluções de gestão de dispositivos com base nas plataformas de dispositivos móveis suportados  

|Plataforma|Com o cliente do Configuration Manager|Gestor de configuração com o Microsoft Intune (híbrido)|No\-local gestão de dispositivos móveis|Configuration Manager com o Exchange|  
|--------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Android||Sim||Sim|  
|iOS||Sim||Sim|  
|Mac OS X|Sim|||Sim|  
|UNIX/Linux|Sim|||Sim|  
|Windows 10|Sim|Sim|Sim|Sim|  
|Windows 10 Mobile||Sim|Sim|Sim|  
|Windows (versões anteriores)|Sim|Sim||Sim|  
|Windows CE|Sim (com cliente legacy de dispositivo móvel)|||Sim|  
|Windows Embedded|Sim||||  
|Windows Phone||Sim||Sim|  
|Windows Server|Sim|||Sim|  

 Para obter uma lista completa das plataformas suportadas, consulte o artigo [sistemas operativos suportados para os clientes e dispositivos para o System Center Configuration Manager](configs\supported-operating-systems-for-clients-and-devices.md).

##  <a name="bkmk_comp2"></a> Comparar soluções de gestão de dispositivos com base na funcionalidade de gestão  

|Funcionalidade de gestão|Com o cliente do Configuration Manager|Gestor de configuração com o Microsoft Intune (híbrido)|No\-local gestão de dispositivos móveis|Configuration Manager com o Exchange|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Segurança da infraestrutura de chaves públicas (PKI) entre o dispositivo móvel e o Configuration Manager (utiliza a autenticação mútua e o SSL para encriptar transferências de dados)|Sim|Sim|Sim||  
|Instalação do cliente|Sim||||  
|Suporte através da Internet|Sim||||  
|Deteção|Sim|||Sim|  
|Inventário de Hardware|Sim|Sim|Sim|Sim|  
|Inventário de software|Sim|||Sim|  
|Definições|Sim|Sim|Sim|Sim|  
|Implementação de software|Sim|Sim|Sim||  
|Monitorizar com ponto de estado de contingência|Sim||||  
|Ligações a pontos de gestão|Sim||Sim||  
|Ligações a pontos de distribuição|Sim||Sim||  
|Bloco do Configuration Manager|Sim|Sim|Sim||  
|Quarentena e bloqueio a partir do Exchange Server (e do Configuration Manager)||||Sim|  
|Eliminação remota| |Sim|Sim|Sim|  


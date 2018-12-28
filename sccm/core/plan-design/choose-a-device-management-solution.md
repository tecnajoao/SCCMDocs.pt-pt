---
title: 'Escolher uma solução de gestão de dispositivos '
titleSuffix: Configuration Manager
description: Saiba mais sobre as soluções que o System Center Configuration Manager oferece para a gestão de PCs, servidores e dispositivos.
ms.date: 12/08/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a520e4e43ca2d7de080272c213c5768cbd284501
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415845"
---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>Escolher uma solução de gestão de dispositivos para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager (também conhecido como o ConfigMgr ou o SCCM) oferece diferentes soluções para o gerenciamento de PCs, servidores e dispositivos. Pode escolher a solução certa para si, com base em plataformas de dispositivos, que tem de gerir e a funcionalidade de gestão que necessária.  


##  <a name="overview-of-device-management-solutions"></a>Descrição geral das soluções de gestão de dispositivos  
 Este artigo abrange quatro soluções de gestão de dispositivos: a aplicação de cliente do Configuration Manager, a infraestrutura do Configuration Manager no local, o Microsoft Intune e o Exchange. O artigo conclui com duas tabelas que comparam as soluções de gestão, um com base na [plataformas de dispositivos móveis suportadas](#compare-device-management-solutions-based-on-supported-mobile-device-platforms)e outro com base nos [funcionalidade de gestão](#compare-mobile-device-management-solutions-based-on-management-functionality).


###  <a name="manage-devices-with-the-configuration-manager-client"></a>Gerir dispositivos com o cliente do Configuration Manager  

Esta opção, o que requer a instalação da aplicação de cliente do Configuration Manager nos dispositivos, fornece a maior parte das funcionalidades para o gerenciamento de PCs, servidores e outros dispositivos no seu ambiente. Para obter mais informações, consulte [métodos de instalação de cliente no System Center Configuration Manager](/sccm/core/clients/deploy/plan/client-installation-methods).  

###  <a name="manage-devices-with-on-premises-configuration-manager-infrastructure"></a>Gerir dispositivos com a infraestrutura do Configuration Manager no local  

Esta opção utiliza as capacidades de gestão de dispositivos incorporadas nos sistemas operativos de algumas plataformas de dispositivos. Embora não tão completa em como a gestão baseada no cliente, gestão de dispositivos móveis no local fornece uma abordagem mais ligeira à gestão através da utilização de recursos do Configuration Manager no local para aceder e gerir dispositivos. Tenha em atenção que esta opção é atualmente suportada apenas para dispositivos Windows 10 PCs e Windows 10 Mobile.  

Para obter mais informações, consulte [gerir dispositivos móveis com a infraestrutura no local no System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

###  <a name="manage-devices-with-microsoft-intune-hybrid"></a>Gerir dispositivos com o Microsoft Intune (híbrido)  

Esta opção utiliza o Microsoft Intune para inscrever e gerir dispositivos, em vez de usar os recursos do Configuration Manager no local. Apesar do Intune gere os dispositivos, acessar as tarefas de gestão na consola do Configuration Manager. Esta opção suporta todos os sistemas de operativos de dispositivos móveis principais, incluindo o Windows 10 Mobile, Windows Phone, iOS, Mac OS X e Android. Também fornece gestão para os computadores Windows 8.1 e Windows 10 na sua organização.  

Para obter mais informações, veja [Gestão de dispositivos móveis (MDM) híbrida com o System Center Configuration Manager e o Microsoft Intune](../../mdm/understand/hybrid-mobile-device-management.md).  

###  <a name="manage-devices-with-microsoft-exchange"></a>Gerir dispositivos com o Microsoft Exchange  

Esta opção utiliza o conector do Exchange Server para ligar vários servidores do Exchange para o Configuration Manager. Isso centraliza a gestão de dispositivos que pode ligar ao Exchange ActiveSync. Pode configurar funcionalidades de gestão de dispositivos móveis do Exchange, como apagamento remoto de dispositivo e o controlo de definições para vários servidores do Exchange, da consola do Configuration Manager.  

Para obter mais informações, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

Pode utilizar estas soluções de gestão de dispositivos individualmente ou em combinação entre si. Por exemplo, pode utilizar a abordagem de gestão baseada no cliente para gerir computadores e servidores na sua organização e também utilizar o Intune para gerir dispositivos móveis. Ao combinar abordagens desta forma, pode cobrir todas as suas necessidades de gestão de dispositivos da consola do Configuration Manager.  

## <a name="compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a>Compare as soluções de gestão de dispositivos com base nas plataformas de dispositivos móveis suportadas  

|Plataforma|Com o cliente do Configuration Manager|Configuration Manager com o Microsoft Intune (híbrido)|No\-no local a gestão de dispositivos móveis|Configuration Manager com o Exchange|  
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

 Para obter uma lista completa das plataformas suportadas, consulte [sistemas operativos suportados por clientes e dispositivos para o System Center Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md).

##  <a name="bkmk_comp2"></a> Comparar soluções de gestão de dispositivos com base na funcionalidade de gestão  

|Funcionalidade de gestão|Com o cliente do Configuration Manager|Configuration Manager com o Microsoft Intune (híbrido)|No\-no local a gestão de dispositivos móveis|Configuration Manager com o Exchange|  
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
|O bloco do Configuration Manager|Sim|Sim|Sim||  
|Quarentena e bloqueio a partir do Exchange Server (e o Configuration Manager)||||Sim|  
|Eliminação remota| |Sim|Sim|Sim|  

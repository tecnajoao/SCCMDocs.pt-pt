---
title: Funcionalidades e capacidades
titleSuffix: Configuration Manager
description: "Saiba mais sobre as principais capacidades de gestão do System Center Configuration Manager."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
caps.latest.revision: "18"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: c9b6720d08260c7a2a06e0ccc525228e5089b279
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="features-and-capabilities-of-system-center-configuration-manager"></a>Funcionalidades e capacidades removidas do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Seguem-se as principais capacidades de gestão do System Center Configuration Manager. Cada capacidade tem os seus pré-requisitos e as capacidades que pretender utilizar podem influenciar a estrutura e implementação da sua hierarquia do Configuration Manager. Por exemplo, se pretender implementar software em dispositivos na sua hierarquia, tem de instalar a função de sistema de sites de ponto de distribuição.  

 Para obter mais informações sobre como planear e instalar o Configuration Manager para suportar estas capacidades de gestão no seu ambiente, consulte [preparar para o System Center Configuration Manager](../../../core/plan-design/get-ready.md).  

 **Gestão de aplicações**  

 Fornece um conjunto de ferramentas e recursos que o podem ajudar a criar, gerir, implementar e monitorizar aplicações numa gama de diferentes dispositivos que gere. Além disso, o Configuration Manager fornece ferramentas que ajudam a proteger os dados da sua empresa em aplicações do utilizador. Consulte [introdução à gestão de aplicações](/sccm/apps/understand/introduction-to-application-management).

 **Acesso a recursos da empresa**  

 Fornece um conjunto de ferramentas e recursos que lhe permite conceder aos utilizadores da organização acesso a dados e aplicações de localizações remotas. Essas ferramentas incluem perfis Wi-Fi, perfis VPN, perfis de certificado e acesso condicional ao Exchange e ao SharePoint online. Consulte [proteger dados e o site de infraestrutura com o System Center Configuration Manager](../../../protect/understand/protect-data-and-site-infrastructure.md) e [gerir o acesso a serviços no System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-services.md).  

 **Definições de compatibilidade**  

 Fornece um conjunto de ferramentas e recursos que podem ajudar a avaliar, controlar e remediar a compatibilidade de configuração de dispositivos de cliente na empresa. Além disso, pode utilizar as definições de compatibilidade para configurar uma variedade de definições de segurança e funcionalidades nos dispositivos que gere. Consulte [garantir a compatibilidade do dispositivo com o System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

 **Endpoint Protection**  

 Fornece segurança, proteção antimalware e gestão da Firewall do Windows para os computadores da empresa. Consulte [Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

 **Inventário**  

 Fornece um conjunto de ferramentas para ajudar a identificar e monitorizar ativos:  

-   **Inventário de hardware**: Recolhe informações detalhadas sobre o hardware dos dispositivos na sua empresa. Consulte [introdução ao inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-hardware-inventory.md).  

-   **Inventário de software**: Recolhe e comunica informações sobre os ficheiros que estão armazenados nos computadores cliente na sua organização. Consulte [introdução ao inventário de software no System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-software-inventory.md).  

-   **Asset Intelligence**: Fornece ferramentas para recolher dados de inventário e monitorizar a utilização de licenças de software na sua empresa. Consulte [introdução ao Asset Intelligence no System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

**Gestão de dispositivos móveis com o Microsoft Intune**  

 Pode utilizar o Configuration Manager para gerir iOS, Android (incluindo Samsung KNOX Standard), Windows Phone e dispositivos Windows com o serviço Microsoft Intune através da Internet.

 Apesar de utilizar o serviço do Intune, as tarefas de gestão são concluídas com a serviço ligação ponto função sistema de sites disponível através da consola do Configuration Manager. Consulte [gestão híbrida de dispositivos móveis (MDM) com o System Center Configuration Manager e o Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

 **Gestão de dispositivos móveis no local**  

 Inscreve e gere PCs e dispositivos móveis utilizando no local do Configuration Manager gestão e infraestrutura funcionalidades incorporadas nas plataformas de dispositivos (em vez de depender de um cliente do Configuration Manager instalado em separado). Atualmente, suporta a gestão de dispositivos Windows 10 Enterprise e Windows 10 Mobile. Consulte [gerir dispositivos móveis com a infraestrutura no local no System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Implementação do sistema operativo**  

 Fornece uma ferramenta para criar imagens do sistema operativo. Em seguida, pode utilizar estas imagens para implementar os sistemas operativos em computadores, através de PXE de arranque ou suportes de dados, tais como um conjunto de CD, DVD ou USB unidades flash. Tenha em atenção que isto aplica-se a computadores que são geridos pelo Configuration Manager, bem como computadores não geridos. Consulte [introdução à implementação do sistema operativo no System Center Configuration Manager](../../../osd/understand/introduction-to-operating-system-deployment.md).  

 **Gestão de energia**  

 Fornece um conjunto de ferramentas e recursos que pode utilizar para gerir e monitorizar o consumo de energia dos computadores cliente na empresa. Consulte [introdução à gestão de energia no System Center Configuration Manager](../../../core/clients/manage/power/introduction-to-power-management.md).  

 **Consultas**  

 Fornece uma ferramenta para obter informações sobre os recursos da hierarquia e informações sobre os dados do inventário e as mensagens de estado. Em seguida, pode utilizar estas informações para relatórios ou para definir coleções de dispositivos ou utilizadores para definições de configuração e implementação de software. Consulte [introdução às consultas no System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md).  

 **Perfis de ligação remota**  

 Fornece um conjunto de ferramentas e recursos para ajudar a criar, implementar e monitorizar as definições de ligação remota para dispositivos na sua organização. Ao implementar estas definições, estará a minimizar o esforço necessário por parte dos utilizadores liguem aos seus computadores na rede empresarial. Consulte [trabalhar com perfis de ligação remota no System Center Configuration Manager](/sccm/compliance/deploy-use/create-remote-connection-profiles).  

 **Itens de configuração de perfis e dados do utilizador**  

 Utilizador dados e perfis de itens de configuração no Configuration Manager contém definições que gerem o redirecionamento de pastas, ficheiros offline e perfis itinerantes em computadores que executam o Windows 8 e posterior para utilizadores na sua hierarquia. Consulte [trabalhar com dados e perfis de itens de configuração utilizador no System Center Configuration Manager](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  

 **Controlo remoto**  

 Fornece ferramentas para administrar remotamente computadores cliente da consola do Configuration Manager. Consulte [introdução ao controlo remoto no System Center Configuration Manager](../../../core/clients/manage/remote-control/introduction-to-remote-control.md).  

 **Relatórios**  

 Fornece um conjunto de ferramentas e recursos que ajudam a utilizam as capacidades avançadas de relatórios do SQL Server Reporting Services na consola do Configuration Manager. Consulte [introdução aos relatórios no System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md).  

 **Medição de software**  

 Fornece ferramentas para monitorizar e recolher dados de utilização de software dos clientes do Configuration Manager. Veja [Monitorizar a utilização da aplicação com a medição de software no System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

 **Atualizações de software**  

 Fornece um conjunto de ferramentas e recursos que podem ajudar a gerir, implementar e monitorizar atualizações de software na empresa. Consulte [introdução ao software atualizações no System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction).  

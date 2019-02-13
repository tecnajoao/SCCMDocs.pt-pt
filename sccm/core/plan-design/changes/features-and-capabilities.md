---
title: Funcionalidades e capacidades
titleSuffix: Configuration Manager
description: Saiba mais sobre as principais capacidades de gestão do System Center Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 235355dff634bab09ef7be65645dbb32c5b86cf9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133719"
---
# <a name="features-and-capabilities-of-system-center-configuration-manager"></a>Funcionalidades e capacidades removidas do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Seguem-se as principais capacidades de gestão do System Center Configuration Manager. Cada capacidade tem os seus pré-requisitos e as capacidades que pretender utilizar podem influenciar o design e a implementação da sua hierarquia do Configuration Manager. Por exemplo, se pretender implementar software nos dispositivos na sua hierarquia, tem de instalar a função de sistema de sites de ponto de distribuição.  

 Para obter mais informações sobre como planear e instalar o Configuration Manager para suportar estas capacidades de gestão no seu ambiente, consulte [preparar-se para o System Center Configuration Manager](../../../core/plan-design/get-ready.md).  

 **Gestão de aplicações**  

 Fornece um conjunto de ferramentas e recursos que o podem ajudar a criar, gerir, implementar e monitorizar aplicações numa gama de diferentes dispositivos que gere. Além disso, o Configuration Manager fornece ferramentas que o ajudam a proteger dados da sua empresa em aplicações do utilizador. Ver [introdução à gestão de aplicações](/sccm/apps/understand/introduction-to-application-management).

 **Acesso a recursos da empresa**  

 Fornece um conjunto de ferramentas e recursos que lhe permite conceder aos utilizadores da organização acesso a dados e aplicações de localizações remotas. Essas ferramentas incluem perfis Wi-Fi, perfis VPN, perfis de certificado e acesso condicional ao Exchange e ao SharePoint online. Ver [proteger dados e do site infraestrutura com o System Center Configuration Manager](../../../protect/understand/protect-data-and-site-infrastructure.md) e [gerir o acesso a serviços no System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-services.md).  

 **Definições de compatibilidade**  

 Fornece um conjunto de ferramentas e recursos que podem ajudar a avaliar, controlar e remediar a compatibilidade de configuração de dispositivos de cliente na empresa. Além disso, pode utilizar as definições de compatibilidade para configurar uma variedade de funcionalidades e definições de segurança nos dispositivos que gere. Ver [garantir a conformidade de dispositivo com o System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

 **Endpoint Protection**  

 Fornece segurança, proteção antimalware e gestão da Firewall do Windows para os computadores da empresa. Ver [Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

 **Inventário**  

 Fornece um conjunto de ferramentas para ajudar a identificar e monitorizar ativos:  

-   **Inventário de hardware**: Recolhe informações detalhadas sobre o hardware de dispositivos na sua empresa. Ver [introdução ao inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-hardware-inventory.md).  

-   **Inventário de software**: Recolhe e comunica informações sobre os ficheiros que estão armazenados nos computadores cliente na sua organização. Ver [introdução ao inventário de software no System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-software-inventory.md).  

-   **Do Asset Intelligence**: Fornece ferramentas para recolher dados de inventário e monitorizar a utilização de licenças de software na sua empresa. Ver [introdução ao Asset Intelligence no System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

**Gestão de dispositivos móveis com o Microsoft Intune**  

 Pode utilizar o Configuration Manager para gerir dispositivos iOS, Android (incluindo Samsung KNOX Standard), Windows Phone e Windows com o serviço Microsoft Intune através da Internet.

 Apesar de utilizar o serviço do Intune, tarefas de gestão são concluídas com a serviço função ponto de ligação site system disponível através da consola do Configuration Manager. Ver [gestão de dispositivos móveis (MDM) híbrida com o System Center Configuration Manager e o Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

 **Gestão de dispositivos móveis no local**  

 Inscreve e gere PCs e dispositivos móveis utilizando no local do Configuration Manager infraestrutura e gestão das funcionalidades incorporadas nas plataformas dos dispositivos (em vez de depender de um cliente do Configuration Manager instalado em separado). Atualmente, suporta a gestão de dispositivos Windows 10 Enterprise e Windows 10 Mobile. Ver [gerir dispositivos móveis com a infraestrutura no local no System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Implementação do sistema operativo**  

 Fornece uma ferramenta para criar imagens do sistema operativo. Em seguida, pode utilizar estas imagens para implantar os sistemas operativos em computadores, utilizando o PXE o arranque ou suportes de dados, como um conjunto de CD, DVD ou USB de unidades flash. Tenha em atenção que isto se aplica a computadores que são geridos pelo Configuration Manager, bem como computadores não geridos. Ver [introdução à implementação do sistema operativo no System Center Configuration Manager](../../../osd/understand/introduction-to-operating-system-deployment.md).  

 **Gestão de energia**  

 Fornece um conjunto de ferramentas e recursos que pode utilizar para gerir e monitorizar o consumo de energia dos computadores cliente na empresa. Ver [introdução à gestão de energia no System Center Configuration Manager](../../../core/clients/manage/power/introduction-to-power-management.md).  

 **Consultas**  

 Fornece uma ferramenta para obter informações sobre os recursos da hierarquia e informações sobre os dados do inventário e as mensagens de estado. Em seguida, pode usar essas informações para os relatórios ou para definir coleções de dispositivos ou utilizadores para as definições de configuração e implementação de software. Ver [introdução às consultas no System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md).  

 **Perfis de ligação remota**  

 Fornece um conjunto de ferramentas e recursos para ajudá-lo a criar, implementar e monitorizar as definições de ligação remota para dispositivos na sua organização. Ao implementar estas definições, estará a minimizar o esforço necessário por utilizadores para se ligar aos seus computadores na rede empresarial. Ver [trabalhar com perfis de ligação remota no System Center Configuration Manager](/sccm/compliance/deploy-use/create-remote-connection-profiles).  

 **Itens de configuração de perfis e dados do utilizador**  

 Utilizador de perfis e dados de itens de configuração no Configuration Manager contêm definições que gerem o redirecionamento de pastas, ficheiros offline e perfis itinerantes em computadores que executam o Windows 8 e posterior para utilizadores na sua hierarquia. Ver [trabalhar com utilizador de perfis e dados de itens de configuração no System Center Configuration Manager](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  

 **Controlo remoto**  

 Fornece ferramentas para administrar remotamente computadores cliente da consola do Configuration Manager. Ver [introdução ao controlo remoto no System Center Configuration Manager](../../../core/clients/manage/remote-control/introduction-to-remote-control.md).  

 **Relatórios**  

 Fornece um conjunto de ferramentas e recursos que o ajudam a utilizar as capacidades avançadas de relatórios do SQL Server Reporting Services na consola do Configuration Manager. Ver [introdução aos relatórios no System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md).  

 **Medição de software**  

 Fornece ferramentas para monitorizar e recolher dados de utilização do software de clientes do Configuration Manager. Veja [Monitorizar a utilização da aplicação com a medição de software no System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

 **Atualizações de software**  

 Fornece um conjunto de ferramentas e recursos que podem ajudar a gerir, implementar e monitorizar atualizações de software na empresa. Ver [introdução ao software de atualizações no System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction).  

---
title: "Introdução à gestão de energia | Documentos do Microsoft"
description: "Obter uma introdução à gestão de energia no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ddff2a7-99eb-4ef8-b969-f3f7f24053db
caps.latest.revision: 4
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: f46c9479021c814b1102d72c7d493f21a7243bf1
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="introduction-to-power-management-in-system-center-configuration-manager"></a>Introdução à gestão de energia no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Gestão de energia no System Center Configuration Manager endereços a necessidade que muitas organizações têm a monitorizar e reduzir o consumo de energia dos respetivos computadores. A funcionalidade tira partido das funcionalidades de gestão de energia incorporadas no Windows para aplicar definições relevantes e consistentes aos computadores da organização. Pode aplicar diferentes definições de energia aos computadores durante as horas de expediente e fora do expediente. Por exemplo, pode pretender aplicar um esquema de energia mais restritivo aos computadores durante as horas de expediente. Nos casos em que os computadores tenham de estar sempre ligados, pode impedir que as definições de gestão de energia sejam aplicadas.  

 Gestão de energia no Configuration Manager inclui vários relatórios para o ajudar a analisar o computador e o consumo de energia as definições de energia na sua organização. Também pode utilizar os relatórios para ajudar a resolver problemas relacionados com a gestão de energia.  

 Para um fluxo de trabalho detalhado sobre como configurar e utilizar a gestão de energia, consulte o artigo [lista de verificação de administrador para gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

> [!IMPORTANT]  
>  Gestão de energia do Configuration Manager não é suportada em máquinas virtuais. Não pode aplicar esquemas de energia a máquinas virtuais, nem reportar os dados de energia dos mesmos.  

## <a name="the-power-management-workflow"></a>Fluxo de trabalho de gestão de energia  
 Utilize os seguintes três fases para planear e implementar gestão de energia no Configuration Manager.  

### <a name="monitoring-and-planning-phase"></a>Fase de monitorização e planeamento  
 Gestão de energia utiliza o inventário de hardware do Configuration Manager para recolher dados sobre as definições de utilização e a eficiência de computador de computadores no site. Existem vários relatórios que pode utilizar para analisar estes dados e determinar as definições de gestão de energia ideais para os computadores. Por exemplo, durante a fasee de monitorização e planeamento do fluxo de trabalho de gestão de energia, pode criar coleções baseadas nos dados incluídos no relatório **Capacidades de Energia** e utilizar esses dados para identificar os computadores sem capacidade de gestão de energia. Em seguida, pode excluir esses computadores da gestão de energia.  

> [!IMPORTANT]  
>  Não aplique esquemas de energia aos computadores no seu site até recolher e analisar os dados de energia dos computadores cliente. Se aplicar novas definições de gestão de energia aos computadores sem examinar primeiro as definições existentes, isto pode representar um aumento do consumo de energia.  

### <a name="enforcement-phase"></a>Fase de imposição  
 A gestão de energia permite criar esquemas de energia que pode aplicar às coleções de computadores no seu site. Estes esquemas de energia configuram as definições de gestão de energia do Windows nos computadores. Pode utilizar os esquemas de energia que são incluídos com o Configuration Manager, ou pode configurar o seu próprio esquemas de energia personalizado. Pode utilizar os dados de energia recolhidos durante a fase de monitorização e planeamento como uma linha de base para o ajudar a avaliar a poupança de energia depois de aplicar um esquema de energia aos computadores. Para obter mais informações, consulte o artigo [lista de verificação de administrador para gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

### <a name="compliance-phase"></a>Fase de conformidade  
 Na fase de conformidade, pode executar relatórios que ajudam a avaliar a utilização de energia e a poupança de energia na sua organização. Também pode executar relatórios que descrevam os melhoramentos como CO2 gerado por computadores. Também estão disponíveis relatórios que ajudam a validar que as definições de energia foram aplicadas corretamente aos computadores e a resolver problemas relacionados com a funcionalidade de gestão de energia.  


---
title: Introdução à gestão de energia
titleSuffix: Configuration Manager
description: Obtenha uma introdução à gestão de energia no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3ddff2a7-99eb-4ef8-b969-f3f7f24053db
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: adf410b2cfdb45b3f01ac48c53d324b678689cda
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="introduction-to-power-management-in-system-center-configuration-manager"></a>Introdução à gestão de energia no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Gestão de energia no System Center Configuration Manager aborda a necessidade que muitas organizações têm de monitorizar e reduzir o consumo de energia dos respetivos computadores. A funcionalidade tira partido das funcionalidades de gestão de energia incorporadas no Windows para aplicar definições relevantes e consistentes aos computadores da organização. Pode aplicar diferentes definições de energia aos computadores durante as horas de expediente e fora do expediente. Por exemplo, pode pretender aplicar um esquema de energia mais restritivo aos computadores durante as horas de expediente. Nos casos em que os computadores tenham de estar sempre ligados, pode impedir que as definições de gestão de energia sejam aplicadas.  

 Gestão de energia no Configuration Manager inclui vários relatórios para o ajudar a analisar as definições de energia de computador e o consumo de energia na sua organização. Também pode utilizar os relatórios para ajudar a resolver problemas relacionados com a gestão de energia.  

 Para um fluxo de trabalho detalhado sobre como configurar e utilizar a gestão de energia, consulte [lista de verificação de administrador para gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

> [!IMPORTANT]  
>  Gestão de energia do Configuration Manager não é suportada em máquinas virtuais. Não pode aplicar esquemas de energia a máquinas virtuais, nem reportar os dados de energia dos mesmos.  

## <a name="the-power-management-workflow"></a>Fluxo de trabalho de gestão de energia  
 Utilize os seguintes três fases para planear e implementar a gestão de energia no Configuration Manager.  

### <a name="monitoring-and-planning-phase"></a>Fase de monitorização e planeamento  
 Gestão de energia utiliza o inventário de hardware do Configuration Manager para recolher dados sobre definições de energia e a utilização do computador para computadores do site. Existem vários relatórios que pode utilizar para analisar estes dados e determinar as definições de gestão de energia ideais para os computadores. Por exemplo, durante a fasee de monitorização e planeamento do fluxo de trabalho de gestão de energia, pode criar coleções baseadas nos dados incluídos no relatório **Capacidades de Energia** e utilizar esses dados para identificar os computadores sem capacidade de gestão de energia. Em seguida, pode excluir esses computadores da gestão de energia.  

> [!IMPORTANT]  
>  Não aplique esquemas de energia aos computadores no seu site até recolher e analisar os dados de energia dos computadores cliente. Se aplicar novas definições de gestão de energia aos computadores sem examinar primeiro as definições existentes, isto pode representar um aumento do consumo de energia.  

### <a name="enforcement-phase"></a>Fase de imposição  
 A gestão de energia permite criar esquemas de energia que pode aplicar às coleções de computadores no seu site. Estes esquemas de energia configuram as definições de gestão de energia do Windows nos computadores. Pode utilizar os esquemas de energia que estão incluídos com o Configuration Manager, ou pode configurar os seus próprios esquemas de energia personalizados. Pode utilizar os dados de energia recolhidos durante a fase de monitorização e planeamento como uma linha de base para o ajudar a avaliar a poupança de energia depois de aplicar um esquema de energia aos computadores. Para obter mais informações, consulte [lista de verificação de administrador para gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

### <a name="compliance-phase"></a>Fase de conformidade  
 Na fase de conformidade, pode executar relatórios que ajudam a avaliar a utilização de energia e a poupança de energia na sua organização. Também pode executar relatórios que descrevam os melhoramentos na quantidade de CO2 geradas por computadores. Também estão disponíveis relatórios que ajudam a validar que as definições de energia foram aplicadas corretamente aos computadores e a resolver problemas relacionados com a funcionalidade de gestão de energia.  

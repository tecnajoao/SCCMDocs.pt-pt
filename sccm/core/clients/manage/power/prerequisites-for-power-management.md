---
title: "Pré-requisitos para gestão de energia | Microsoft Docs"
description: "Obter os pré-requisitos para a gestão de energia no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
caps.latest.revision: "4"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 5247bf1ce5b04264bc0d3e04c5de7f98300905c9
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/15/2017
---
# <a name="prerequisites-for-power-management-in-system-center-configuration-manager"></a>Pré-requisitos para gestão de energia no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Gestão de energia no System Center Configuration Manager tem dependências externas e dependências no produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  
 A tabela seguinte lista as dependências externas ao Configuration Manager para utilizar a gestão de energia.  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Os computadores cliente devem ter capacidade para suportar os estados de energia necessários|Para utilizar todas as funcionalidades de gestão de energia, os computadores cliente devem ser capazes de suportar as ações do modo de suspensão, hibernação, reativação da suspensão e reativação da hibernação. Pode utilizar o relatório **Funções de Energia** para determinar se os computadores podem suportar estas ações. Para obter mais informações, consulte [relatório capacidades de energia](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) no tópico [como monitorizar e planear a gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  
 A tabela seguinte lista as dependências do Configuration Manager para utilizar a gestão de energia.  

|Dependência|Mais informações|  
|----------------|----------------------|  
|A gestão de energia deve ser ativada antes de criar e monitorizar os esquemas de energia.|Para obter informações sobre como ativar e configurar a gestão de energia, consulte [configurar gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Ponto do Reporting Services|Deve configurar um ponto do sistema de reporte antes de poder visualizar relatórios de gestão de energia. Para obter mais informações, veja [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  

---
title: "Pré-requisitos para gestão de energia | Documentos do Microsoft"
description: "Obter os pré-requisitos para a gestão de energia no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
caps.latest.revision: 4
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 711ef491899846b86bfed0355ac7fd0f9d509c4f
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="prerequisites-for-power-management-in-system-center-configuration-manager"></a>Pré-requisitos para gestão de energia no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Gestão de energia no System Center Configuration Manager tem dependências externas e dependências contidas no produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  
 A tabela seguinte lista as dependências externas ao Configuration Manager para utilizar a gestão de energia.  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Os computadores cliente devem ter capacidade para suportar os estados de energia necessários|Para utilizar todas as funcionalidades de gestão de energia, os computadores cliente devem ser capazes de suportar as ações do modo de suspensão, hibernação, reativação da suspensão e reativação da hibernação. Pode utilizar o relatório **Funções de Energia** para determinar se os computadores podem suportar estas ações. Para obter mais informações, consulte o artigo [relatório capacidades de energia](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) no tópico [como a monitorizar e planear a gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  
 A tabela seguinte lista as dependências do Configuration Manager para utilizar a gestão de energia.  

|Dependência|Mais informações|  
|----------------|----------------------|  
|A gestão de energia deve ser ativada antes de criar e monitorizar os esquemas de energia.|Para obter informações sobre como ativar e configurar a gestão de energia, consulte o artigo [configurar gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Ponto do Reporting Services|Deve configurar um ponto do sistema de reporte antes de poder visualizar relatórios de gestão de energia. Para obter mais informações, veja [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  


---
title: Pré-requisitos para gestão de energia
titleSuffix: Configuration Manager
description: Obtenha as pré-requisitos para gestão de energia no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e965c9abede80bac488cfba0759d4f9e33974fb
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125811"
---
# <a name="prerequisites-for-power-management-in-system-center-configuration-manager"></a>Pré-requisitos para gestão de energia no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Gestão de energia no System Center Configuration Manager tem dependências externas e dependências no produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  
 A tabela seguinte lista as dependências externas ao Configuration Manager para utilizar a gestão de energia.  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Os computadores cliente devem ter capacidade para suportar os estados de energia necessários|Para utilizar todas as funcionalidades de gestão de energia, os computadores cliente devem ser capazes de suportar as ações do modo de suspensão, hibernação, reativação da suspensão e reativação da hibernação. Pode utilizar o relatório **Funções de Energia** para determinar se os computadores podem suportar estas ações. Para obter mais informações, consulte [relatório de capacidades de energia](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) no tópico [como monitorizar e planear a gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  
 A tabela seguinte lista as dependências do Configuration Manager para utilizar a gestão de energia.  

|Dependência|Mais Informações|  
|----------------|----------------------|  
|A gestão de energia deve ser ativada antes de criar e monitorizar os esquemas de energia.|Para obter informações sobre como ativar e configurar a gestão de energia, consulte [configurar a gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Ponto do Reporting Services|Deve configurar um ponto do sistema de reporte antes de poder visualizar relatórios de gestão de energia. Para obter mais informações, veja [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  

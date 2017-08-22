---
title: "Pré-requisitos para relatórios | Microsoft Docs"
description: "Compreenda as várias dependências que afetam a sua utilização de relatórios no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 2e624eb2ea061a4eb7d92365410fada335640224
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-reporting-in-system-center-configuration-manager"></a>Pré-requisitos para relatórios no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Relatórios no System Center Configuration Manager tem dependências externas e dependências no produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  
 A tabela seguinte lista as dependências externas dos relatórios.  

|Pré-requisito|Mais informações|  
|------------------|----------------------|  
|Serviços de Relatórios do SQL Server|Antes de poder utilizar relatórios no Configuration Manager, tem de instalar e configurar o SQL Server Reporting Services.<br /><br /> Para obter informações sobre o planeamento e implementação do Reporting Services no seu ambiente, consulte a secção [Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=212032) do SQL Server 2008 Books Online.|  
|Dependências da função do sistema de sites para os computadores que executem o ponto do Reporting Services.|[Configurações suportadas para o System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Dependências internas do Configuration Manager  
 A tabela seguinte lista as dependências dos relatórios no Configuration Manager.  

|Pré-requisito|Mais informações|  
|------------------|----------------------|  
|Ponto do Reporting Services|Função de sistema de sites do ponto deve ser configurada antes de poder utilizar relatórios no Configuration Manager do Reporting Services. Para obter mais informações sobre como instalar e configurar um ponto do Reporting Services, consulte [configurar relatórios no System Center Configuration Manager](../../../core/servers/manage/configuring-reporting.md).|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>Versões suportadas do SQL Server para o Ponto do Reporting Services  
 A base de dados do Reporting Services pode ser instalada na instância predefinida ou numa instância nomeada de uma instalação do SQL Server de 64 bits. A instância do SQL Server pode estar colocalizada com o servidor do sistema de sites ou encontrar-se num computador remoto.  

 A tabela seguinte lista as versões do SQL Server suportadas pelo ponto do Reporting Services.  

|Versão do SQL Server|Ponto do Reporting Services|  
|------------------------|------------------------------|  
|SQL Server 2008 SP2 com pelo menos a atualização cumulativa 9<br /><br /> -Padrão<br />-Enterprise<br />-O Centro de dados|Sim|  
|SQL Server 2008 SP3 com pelo menos a atualização cumulativa 4<br /><br /> -Padrão<br />-Enterprise<br />-O Centro de dados|Sim|  
|SQL Server 2008 R2 com SP1 e com pelo menos a atualização cumulativa 6<br /><br /> -Padrão<br />-Enterprise<br />-O Centro de dados|Sim|  
|SQL Server 2008 R2 com SP2<br /><br /> -Padrão<br />-Enterprise<br />-O Centro de dados|Sim|  
|SQL Server Express 2008 R2 com SP1 e com pelo menos a atualização cumulativa 4|Não Suportado|  
|SQL Server Express 2008 R2 com SP2|Não Suportado|  
|SQL Server 2012 com pelo menos a atualização cumulativa 2<br /><br /> -Padrão<br />-Enterprise|Sim|  
|SQL Server 2012 com SP1 sem atualização cumulativa mínima<br /><br /> -Padrão<br />-Enterprise|Sim|  
|SQL Server 2014<br /><br /> -Padrão<br />-Enterprise|Sim|
|SQL Server 2016<br /><br /> -Padrão<br />-Enterprise|Sim|
|SQL Server 2016 com SP1<br /><br /> -Padrão<br />-Enterprise|Sim|
## <a name="next-steps"></a>Passos seguintes
[Operações e manutenção de relatórios](operations-and-maintenance-for-reporting.md)

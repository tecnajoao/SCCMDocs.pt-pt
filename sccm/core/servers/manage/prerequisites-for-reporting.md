---
title: "Pré-requisitos para relatórios"
titleSuffix: Configuration Manager
description: "Compreenda as várias dependências que afetam a sua utilização de relatórios no System Center Configuration Manager."
ms.custom: na
ms.date: 01/29/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
caps.latest.revision: 
caps.handback.revision: 
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 3feafa8a20bedfba381c29a5d7fe80a47517b6ab
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/01/2018
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

|Pré-requisito|Obter mais informações|  
|------------------|----------------------|  
|Ponto do Reporting Services|Função de sistema de sites do ponto deve ser configurada antes de poder utilizar relatórios no Configuration Manager do Reporting Services. Para obter mais informações sobre como instalar e configurar um ponto do Reporting Services, consulte [configurar relatórios no System Center Configuration Manager](../../../core/servers/manage/configuring-reporting.md).|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>Versões suportadas do SQL Server para o Ponto do Reporting Services  
 A base de dados do Reporting Services pode ser instalada na instância predefinida ou numa instância nomeada de uma instalação do SQL Server de 64 bits. A instância do SQL Server pode estar colocalizada com o servidor do sistema de sites ou encontrar-se num computador remoto.  

 A tabela seguinte lista as versões do SQL Server suportadas pelo ponto do Reporting Services.  

|Versão do SQL Server|Ponto do Reporting Services|  
|------------------------|------------------------------|
|SQL Server 2017 com um mínimo de atualização cumulativa 2<br /><br /> -   Standard<br />-   Enterprise|Sim, a partir do Configuration Manager versão 1710|  
|SQL Server 2016 com SP1<br /><br /> -   Standard<br />-   Enterprise|Sim| 
|SQL Server 2016<br /><br /> -   Standard<br />-   Enterprise|Sim|
|SQL Server 2014 com SP2<br /><br /> -   Standard<br />-   Enterprise|Sim|
|SQL Server 2014 com SP1<br /><br /> -   Standard<br />-   Enterprise|Sim|
|SQL Server 2012 com SP4 <br /><br /> -   Standard<br />-   Enterprise|Sim|  
|SQL Server 2012 com SP3 <br /><br /> -   Standard<br />-   Enterprise|Sim|  
|SQL Server 2008 R2 with SP3<br /><br /> -   Standard<br />-   Enterprise<br />-O Centro de dados|Sim, para as versões suportadas do Configuration Manager antes de 1702.|  
|SQL Server Express 2008 R2 com SP3|Não Suportado| 




## <a name="next-steps"></a>Passos seguintes
[Operações e manutenção de relatórios](operations-and-maintenance-for-reporting.md)

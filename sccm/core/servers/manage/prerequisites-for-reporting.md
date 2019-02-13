---
title: Pré-requisitos para geração de relatórios
titleSuffix: Configuration Manager
description: Compreenda as várias dependências que têm impacto sobre a utilização de relatórios no System Center Configuration Manager.
ms.date: 01/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 612056861b896d8c7c271e60e0bb6b78fcbd106e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123268"
---
# <a name="prerequisites-for-reporting-in-system-center-configuration-manager"></a>Pré-requisitos para relatórios no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Relatórios no System Center Configuration Manager tem dependências externas e dependências no produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  
 A tabela seguinte lista as dependências externas dos relatórios.  

|Pré-requisito|Mais informações|  
|------------------|----------------------|  
|Serviços de Relatórios do SQL Server|Antes de poder utilizar relatórios no Configuration Manager, tem de instalar e configurar o SQL Server Reporting Services.<br /><br /> Para obter informações sobre o planeamento e implementação do Reporting Services no seu ambiente, consulte a secção [Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=212032) do SQL Server 2008 Books Online.|  
|Dependências da função do sistema de sites para os computadores que executem o ponto do Reporting Services.|[Configurações suportadas do System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Dependências internas do Configuration Manager  
 A tabela seguinte lista as dependências dos relatórios no Configuration Manager.  

|Pré-requisito|Mais informações|  
|------------------|----------------------|  
|Ponto do Reporting Services|Do ponto de função de sistema de sites tem de ser configurada antes de poder utilizar relatórios no Configuration Manager reporting services. Para obter mais informações sobre como instalar e configurar um ponto do reporting services, consulte [configurar relatórios no System Center Configuration Manager](../../../core/servers/manage/configuring-reporting.md).|  

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
|SQL Server 2008 R2 com SP3<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|Sim, para versões suportadas do Configuration Manager antes de 1702.|  
|SQL Server Express 2008 R2 com SP3|Não Suportado| 




## <a name="next-steps"></a>Passos seguintes
[Operações e manutenção de relatórios](operations-and-maintenance-for-reporting.md)

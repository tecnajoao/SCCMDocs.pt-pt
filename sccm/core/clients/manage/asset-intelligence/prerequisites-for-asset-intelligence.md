---
title: Pré-requisitos do Asset Intelligence
titleSuffix: Configuration Manager
description: Obter os pré-requisitos para o Asset Intelligence no System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 23ab4f94-7bfe-436e-8a6a-029409a2730c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b8e7477f8a5b837327640f78656070579fad23a8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32335311"
---
# <a name="prerequisites-for-asset-intelligence-in-system-center-configuration-manager"></a>Pré-requisitos para o Asset Intelligence no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Asset Intelligence no System Center Configuration Manager tem dependências externas e dependências no produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  
 A tabela seguinte fornece as dependências para o Asset Intelligence externas ao Configuration Manager.  

|Dependência|Mais Informações|  
|----------------|----------------------|  
|Pré-requisitos da Auditoria de Eventos de Início de Sessão Bem-sucedidos|Quatro relatórios do Asset Intelligence apresentam informações recolhidas a partir de registos de eventos de Segurança do Windows nos computadores cliente. Se as definições de registo de eventos de Segurança não estiverem configuradas para registar todos os eventos de início de sessão bem-sucedidos, estes relatórios não contêm dados, mesmo que esteja ativada a classe adequada de relatórios de inventário de hardware.<br /><br /> Os relatórios do Asset Intelligence seguintes dependem das informações de registo de eventos de Segurança do Windows recolhidas:<br /><br /> -Hardware 03A - utilizadores primários do computador<br />-Hardware 03B - computadores para um utilizador principal da consola específico<br />-Hardware 04A - partilhados (multiutilizador) de computadores<br />-Hardware 05A - utilizadores de consola num computador específico<br /><br /> Para ativar o Agente do Cliente de Inventário de Hardware para inventariar as informações necessárias para suportar estes relatórios, primeiro tem de modificar as definições de registo de eventos de Segurança do Windows nos clientes para registar todos os eventos de início de sessão bem-sucedidos e ativar a classe de relatório de inventário de hardware **SMS_SystemConsoleUser** . Para obter mais informações sobre como modificar as definições de registo de eventos de segurança para registar todos os eventos de início de sessão bem-sucedidos, consulte [ativar a auditoria de eventos de início de sessão bem-sucedidos](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableSuccessLogonEvents).|  

> [!NOTE]  
>  A classe de relatórios de inventário de hardware **SMS_SystemConsoleUser** retém os dados de eventos de início de sessão bem-sucedidos durante apenas os últimos 90 dias do registo de eventos de Segurança, independentemente da duração do registo. Se o registo de eventos de Segurança tiver menos de 90 dias de dados, é lido todo o registo.  

## <a name="dependencies-internal-to-configuration-manager"></a>Dependências Internas do Configuration Manager  
 A tabela seguinte fornece as dependências para o Asset Intelligence internas do Configuration Manager.  

|Dependência|Mais Informações|  
|----------------|----------------------|  
|Pré-requisitos do Agente do Cliente|Os relatórios do Asset Intelligence dependem das informações do cliente obtidas através de relatórios de inventário de hardware e software do cliente. Para obter as informações necessárias para todos os relatórios do Asset Intelligence, têm de estar ativados os seguintes agentes do cliente:<br /><br /> -Agente do cliente de inventário de hardware<br />-Agente de cliente de medição de software|  
|Dependências do Agente do Cliente de Inventário de Hardware|Para recolher os dados de inventário necessários para alguns relatórios do Asset Intelligence, o Agente do Cliente de Inventário de Hardware tem de estar ativado. Além disso, algumas classes de relatórios de inventário de hardware de que os relatórios do Asset Intelligence dependem têm de estar ativadas nos computadores de servidor do site primário.<br /><br /> Para obter informações sobre como ativar o agente de cliente de inventário de Hardware, consulte [como expandir o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).|  
|Dependências do Agente do Cliente de Medição de Software|Vários relatórios de software do Asset Intelligence dependem do Agente do Cliente de Medição de Software para fornecer dados. Para obter informações sobre como ativar o agente de cliente de medição de Software, consulte [monitorizar a utilização de aplicação com a medição de software no System Center Configuration Manager](../../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).<br /><br /> Os relatórios do Asset Intelligence seguintes dependem do Agente do Cliente de Medição de Software para fornecer dados:<br /><br /> -Software 07A - executáveis utilizados recentemente por número de computadores<br />-Software 07B - computadores recentemente que utilizaram um executável especificado<br />-Software 07c - executáveis utilizados recentemente num computador específico<br />-Software 08A - executáveis utilizados recentemente por número de utilizadores<br />-Software 08B - utilizadores que recentemente utilizaram um executável especificado<br />-Software 08c - executáveis utilizados recentemente por um utilizador especificado|  
|Pré-requisitos da Classe de Relatórios de Inventário de Hardware do Asset Intelligence|No Gestor de configuração de relatórios do Asset Intelligence dependem de classes de relatório de inventário de hardware específico. Até as classes de relatórios de inventário de hardware estarem ativadas e os clientes terem reportado o inventário de hardware com base nestas classes, os relatórios do Asset Intelligence associados não irão conter nenhuns dados. Pode ativar as classes de relatórios de inventário de hardware seguintes para suportar os requisitos de relatórios do Asset Intelligence:<br /><br /> -SMS_SystemConsoleUsage<sup>1</sup><br />-SMS_SystemConsoleUser<sup>1</sup><br />-SMS_InstalledSoftware<br />-SMS_AutoStartSoftware<br />-SMS_BrowserHelperObject<br />-Win32_USBDevice<br />-SMS_InstalledExecutable<br />-SMS_SoftwareShortcut<br />-SoftwareLicensingService<br />-SoftwareLicensingProduct<br />-SMS_SoftwareTag<br /><br /> <sup>1</sup> Por predefinição, as classes de relatórios de inventário de hardware do Asset Intelligence **SMS_SystemConsoleUsage** e **SMS_SystemConsoleUser** estão ativadas.<br /><br /> Pode editar o inventário de hardware do Asset Intelligence, classes na consola do Configuration Manager, de relatório no **ativos e compatibilidade** área de trabalho, ao clicar no **do Asset Intelligence** nós. Para obter mais informações, consulte o [inventário de hardware do Asset Intelligence ativar classes de relatório](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence) secção o [configurar do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md) tópico.|  
|Ponto do Reporting Services|A função do sistema de sites do ponto do Reporting Services tem de ser instalada para que os relatórios de atualização de software possam ser apresentados. Para mais informações sobre como criar um ponto do Reporting Services, consulte [Configurar Relatórios no Configuration Manager](http://go.microsoft.com/fwlink/p/?LinkId=232661).|  

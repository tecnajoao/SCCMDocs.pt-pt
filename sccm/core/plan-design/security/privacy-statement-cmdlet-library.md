---
title: Declaração de privacidade do Configuration Manager cmdletlLibrary
description: Saiba mais sobre como a Microsoft recolhe e utiliza dados relacionados com a biblioteca de cmdlets do System Center Configuration Manager.
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bb48f192146a3c0d4bbbe6f005dda537db871da7
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415488"
---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>Declaração de privacidade do System Center Configuration Manager – biblioteca de cmdlets do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Esta declaração de privacidade cobre as funcionalidades para a Biblioteca de Cmdlets do System Center Configuration Manager.  

## <a name="usage-data"></a>Dados de utilização  

#### <a name="what-this-feature-does"></a>O que faz esta funcionalidade   

A biblioteca de cmdlets do System Center Configuration Manager permite-lhe gerir uma hierarquia do Configuration Manager utilizando cmdlets do Windows PowerShell e scripts. A biblioteca de cmdlets recolhe informações sobre como utilizar os cmdlets na biblioteca para identificar tendências e padrões de utilização. A biblioteca de cmdlets também recolhe os tipos e números de erros que recebe quando utiliza os cmdlets.  

#### <a name="information-collected-processed-or-transmitted"></a>Informações recolhidas, processadas ou transmitidas
   
Os dados de utilização recolhidos incluem a iniciar, parar e terminação de cmdlets, a execução de cmdlets preteridos e métricas de atividade para operações de fornecedor de SMS relacionadas com os cmdlets. Estas informações não não identificativas. Informações de erro recolhidas incluem erros que retornam cmdlets e detalhes do erro para erros de exceção. Alguns relatórios de detalhes do erro podem inadvertidamente incluir identificadores individuais, como um número de série para um dispositivo que está ligado ao seu computador. A biblioteca de cmdlets filtra e torna anónimas informações nos relatórios de erros para remover identificadores individuais antes da transmissão à Microsoft.  

#### <a name="use-of-information"></a>Utilização de informações
   
A Microsoft utiliza estas informações para melhorar a qualidade, segurança e integridade dos produtos e serviços que oferecem.  

#### <a name="choicecontrol"></a>Escolha/controlo   

Esta funcionalidade de dados de utilização está ativada por predefinição. A biblioteca de cmdlets do System Center Configuration Manager tem duas chaves do Registro que controlam esta funcionalidade.  

 Para optar ativamente por não, defina estes valores de chave de registo de dois. Elas são para cada um dos fornecedores de rastreio de eventos para Windows (ETW):  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (opta ativamente por dados de utilização para o fornecedor de unidade)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.cmdlets:CeipLevel=0 (opta ativamente por dados de utilização para os cmdlets)  

  Alterações às definições de dados de utilização são específicas para o computador em que são introduzidas.  


## <a name="next-steps"></a>Passos seguintes

[Documentação do System Center Configuration Manager a biblioteca de cmdlets](https://docs.microsoft.com/powershell/sccm/configurationmanager/).   

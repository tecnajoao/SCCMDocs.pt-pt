---
title: Declaração de privacidade do Configuration Manager cmdletlLibrary
description: Saiba mais sobre como a Microsoft recolhe e utiliza os dados relacionados com a biblioteca de cmdlets do System Center Configuration Manager.
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: ''
caps.handback.revision: ''
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 0ed94de1fc4782539baed0f1589cebf69c0f2219
ms.sourcegitcommit: a19e12d5c3198764901d44f4df7c60eb542e765f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/28/2018
---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>Declaração de privacidade do System Center Configuration Manager - biblioteca de cmdlets do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Esta declaração de privacidade cobre as funcionalidades para a Biblioteca de Cmdlets do System Center Configuration Manager.  

## <a name="usage-data"></a>Dados de utilização  

#### <a name="what-this-feature-does"></a>O que faz esta funcionalidade   

A biblioteca de cmdlets do System Center Configuration Manager permite-lhe gerir uma hierarquia do Configuration Manager utilizando cmdlets do Windows PowerShell e scripts. A biblioteca de cmdlets recolhe informações sobre como utilizar os cmdlets na biblioteca para identificar tendências e padrões de utilização. A biblioteca de cmdlets recolhe também os tipos e o número de erros que recebe quando utilizar os cmdlets.  

#### <a name="information-collected-processed-or-transmitted"></a>Informações recolhidas, processadas ou transmitidas
   
Os dados de utilização recolhidas incluem iniciar, parar e terminação de cmdlets, a execução de cmdlets preteridos e métricas de atividade para operações de fornecedor de SMS que estão relacionados com os cmdlets. Estas informações não não identificativas. Informações de erro recolhidas incluem erros que devolvam os cmdlets e detalhes do erro para erros de exceção. Alguns relatórios de detalhe do erro podem inadvertidamente incluir identificadores individuais, como um número de série para um dispositivo que está ligado ao seu computador. A biblioteca de cmdlets filtra e torna anónimas informações nos relatórios de erros para remover identificadores individuais antes da transmissão à Microsoft.  

#### <a name="use-of-information"></a>Utilização de informações
   
A Microsoft utiliza estas informações para melhorar a qualidade, segurança e integridade dos produtos e serviços oferecem.  

#### <a name="choicecontrol"></a>Escolha/controlo   

Esta funcionalidade de dados de utilização está ativada por predefinição. A biblioteca de cmdlets do System Center Configuration Manager tem duas chaves de registo que controlam esta funcionalidade.  

 Totalmente ativamente, defina estes valores de chave de dois registo. São para cada um dos fornecedores de rastreio de eventos para o Windows (ETW):  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (evita dados de utilização para o fornecedor de unidade)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.cmdlets:CeipLevel=0 (evita dados de utilização para os cmdlets)  

 Alterações às definições de dados de utilização são específicas para o computador onde está a efetuar.  


## <a name="next-steps"></a>Passos seguintes

[Documentação de biblioteca de cmdlets do System Center Configuration Manager do sistema](https://docs.microsoft.com/powershell/sccm/configurationmanager/).   

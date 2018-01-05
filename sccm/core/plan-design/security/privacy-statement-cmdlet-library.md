---
title: "Declaração de privacidade do Configuration Manager cmdletlLibrary"
description: Saiba mais sobre como a Microsoft recolhe e utiliza os dados relacionados com a biblioteca de cmdlets do System Center Configuration Manager.
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: "5"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: f4f018721aa09f7e8bd42b9e74552c0d34e0f5a9
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/04/2018
---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>Declaração de privacidade do System Center Configuration Manager - biblioteca de cmdlets do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Esta declaração de privacidade cobre as funcionalidades para a Biblioteca de Cmdlets do System Center Configuration Manager.  

## <a name="usage-data"></a>Dados de utilização  
 **O que faz esta funcionalidade:**   
A biblioteca de cmdlets do System Center Configuration Manager permite-lhe gerir uma hierarquia do Configuration Manager utilizando cmdlets do Windows PowerShell e scripts. A biblioteca de cmdlets recolhe informações sobre como utilizar os cmdlets na biblioteca para identificar tendências e padrões de utilização. A biblioteca de cmdlets recolhe também os tipos e o número de erros que encontrar ao utilizar os cmdlets.  

 **Informações recolhidas, processadas ou transmitidas:**   
Os dados de utilização recolhidos incluem início, paragem e terminação de cmdlets, em execução de cmdlets preteridos e métricas de atividade para operações de fornecedor do Systems Management Server (SMS) que estão relacionados com os cmdlets. Esta informação não é identificativa.  Informações de erro recolhidas incluem erros que devolvam os cmdlets e detalhes do erro para erros de exceção. Alguns relatórios de detalhe do erro podem inadvertidamente conter identificadores individuais, como um número de série para um dispositivo que está ligado ao seu computador. A biblioteca de cmdlets filtra e torna anónimas informações nos relatórios de erros para remover identificadores individuais antes da transmissão à Microsoft.  

 **Utilização de informações:**   
Estas informações são utilizadas para melhorar a qualidade, segurança e integridade dos produtos e serviços que oferecemos.  

 **Escolha/controlo:**   
Esta funcionalidade de dados de utilização está ativada por predefinição. A biblioteca de cmdlets do System Center Configuration Manager tem duas chaves de registo que controlam esta funcionalidade.  

 Para optar ativamente por não participar, tem de definir estes dois valores de chave de registo, um para cada um dos fornecedores do Rastreio de Eventos para o Windows (ETW):  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (opta ativamente por não participar nos Dados de Utilização para o fornecedor de unidade)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (opta ativamente por não participar nos Dados de Utilização para os cmdlets)  

 As alterações às definições de Dados de Utilização são específicas do computador em que são introduzidas.  

 Para obter mais informações sobre como configurar dados de utilização (coleção), consulte o [documentação da biblioteca de cmdlets do System Center Configuration Manager](https://technet.microsoft.com/en-us/library/dn958404.aspx).   

---
title: "Declaração de privacidade do System Center Configuration Manager - do Configuration Manager cmdletlLibrary | Documentos do Microsoft"
description: Saiba mais sobre como a Microsoft recolhe e utiliza dados relacionados com a biblioteca de cmdlet do System Center Configuration Manager.
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
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 3d6799ad46e0fe69333aba0662f18c9153c17bda
ms.openlocfilehash: 3936075555cc0bb370ea6e42c7e720b864d565f7
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>Declaração de privacidade do System Center Configuration Manager - biblioteca de cmdlet do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Esta declaração de privacidade cobre as funcionalidades para a Biblioteca de Cmdlets do System Center Configuration Manager.  

## <a name="usage-data"></a>Dados de utilização  
 **O que faz esta funcionalidade:**   
A biblioteca de cmdlet do System Center Configuration Manager permite-lhe gerir uma hierarquia do Configuration Manager, utilizando cmdlets do Windows PowerShell e scripts. A biblioteca de cmdlet recolhe informações sobre como utilizar os cmdlets na biblioteca para identificar tendências e padrões de utilização. A biblioteca de cmdlet também recolherá os tipos e o número de erros que encontrar ao utilizar os cmdlets.  

 **Informações recolhidas, processadas ou transmitidas:**   
Os dados de utilização recolhidas incluem iniciar, parar e a terminar de cmdlets, execução de cmdlets preteridos e métricas de atividade para operações de fornecedor do Systems Management Server (SMS) que estão relacionados com os cmdlets. Esta informação não é identificativa.  Informações de erros recolhidos incluem erros que devolvem os cmdlets e detalhes do erro para erros de exceção. Alguns relatórios de detalhe do erro podem inadvertidamente conter identificadores individuais, como um número de série de um dispositivo que está ligado ao seu computador. A biblioteca de cmdlet filtros e anonymizes informações nos relatórios de erros para remover individuais identificadores antes da transmissão à Microsoft.  

 **Utilização das informações:**   
Utilizamos estas informações para melhorar a qualidade, segurança e integridade dos produtos e serviços que Microsoft oferece.  

 **Escolha/controlo:**   
Esta funcionalidade de dados de utilização é ativada por predefinição. A biblioteca de cmdlet do System Center Configuration Manager tem duas chaves de registo que controlam esta funcionalidade.  

 Para optar ativamente por não participar, tem de definir estes dois valores de chave de registo, um para cada um dos fornecedores do Rastreio de Eventos para o Windows (ETW):  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (opta ativamente por não participar nos Dados de Utilização para o fornecedor de unidade)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (opta ativamente por não participar nos Dados de Utilização para os cmdlets)  

 As alterações às definições de Dados de Utilização são específicas do computador em que são introduzidas.  

 Para mais informações sobre como configurar dados de utilização (coleção), consulte o [documentação de biblioteca do System Center Configuration Manager Cmdlet](https://technet.microsoft.com/en-us/library/dn958404.aspx).   


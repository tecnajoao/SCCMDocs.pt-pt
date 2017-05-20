---
title: "Serviços de componentes de cliente do UNIX/Linux e comandos | Documentos do Microsoft"
description: "Saiba mais sobre serviços de componentes e comandos nos clientes Linux e UNIX no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: 89668f3e2e0a3e2e0178e5b2c91b2508f583649f
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="linux-and-unix-clients-component-services-and-commands-for-system-center-configuration-manager"></a>Serviços de componentes de clientes Linux e UNIX e comandos para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 A tabela seguinte identifica os serviços do componente de cliente do cliente do Configuration Manager para Linux e UNIX.  

|Nome de ficheiro|Mais informações|  
|---------------|----------------------|  
|ccmexec.bin|Este serviço é equivalente ao serviço ccmexc em clientes baseados em Windows. É responsável por todas as comunicações com funções de sistema de sites do Configuration Manager e também comunica com o serviço de omiserver para recolher o inventário de hardware de computador local.<br /><br /> Para obter uma lista de argumentos de linha de comandos suportados, execute **ccmexec -h**|  
|omiserver.bin|Este serviço é o servidor CIM. O servidor CIM proporciona uma arquitetura para módulos de software incorporáveis, denominados fornecedores. Os fornecedores interagem com os recursos informáticos Linux e UNIX e recolhem os dados do inventário de hardware. Por exemplo, o **fornecedor de processos** para um computador Linux recolhe os dados associados aos processos do sistema operativo Linux.|  

 As tabelas seguintes listam os comandos que pode utilizar para iniciar, parar ou reiniciar os serviços do cliente (ccmexec.bin e omiserver.bin) em cada versão do Linux ou do UNIX. Quando iniciar ou parar o serviço ccmexec, o serviço omiserver também é iniciado ou parado.  

|Sistema operativo|Comandos|  
|----------------------|--------------|  
|Agente Universal<br /><br /> RHEL 4 e SLES 9|Iniciar: **/etc/init d/ccmexecd start**<br /><br /> Parar: **/etc/init d/ccmexecd stop**<br /><br /> Reiniciar: **/etc/init d/ccmexecd restart**|  
|Solaris 9|Iniciar: **/etc/init d/ccmexecd start**<br /><br /> Parar: **/etc/init d/ccmexecd stop**<br /><br /> Reiniciar: **/etc/init d/ccmexecd restart**|  
|Solaris 10|Iniciar:<br /><br /> **svcadm ativar -s svc: / gestão/aplicação/omiserver**<br /><br /> **svcadm ativar -s svc: / gestão/aplicação/ccmexecd**<br /><br /> Parar:<br /><br /> **svcadm desativar -s svc: / gestão/aplicação/ccmexecd**<br /><br /> **svcadm desativar -s svc: / gestão/aplicação/omiserver**|  
|Solaris 11|Iniciar:<br /><br /> **svcadm ativar -s svc: / gestão/aplicação/omiserver**<br /><br /> **svcadm ativar -s svc: / gestão/aplicação/ccmexecd**<br /><br /> Parar:<br /><br /> **svcadm desativar -s svc: / gestão/aplicação/ccmexecd**<br /><br /> **svcadm desativar -s svc: / gestão/aplicação/omiserver**|  
|AIX|Iniciar:<br /><br /> **startsrc -s omiserver**<br /><br /> **startsrc -s ccmexec**<br /><br /> Parar:<br /><br /> **stopsrc -s ccmexec**<br /><br /> **stopsrc -s omiserver**|  
|HP-UX|Iniciar: **/sbin/init.d/ccmexecd start**<br /><br /> Parar: **/sbin/init.d/ccmexecd stop**<br /><br /> Reiniciar: **/sbin/init.d/ccmexecd restart**|  

---
title: "Introdução de coleções | Documentos do Microsoft"
description: "Obter uma introdução à utilização coleções no System Center Configuration Manager."
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
caps.latest.revision: 8
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9c5d1e48b76392beaf54b5377c69b648537e86f8
ms.openlocfilehash: 547d231d48ccbc8241e9f1f8f71e3750b266b73e
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="introduction-to-collections-in-system-center-configuration-manager"></a>Introdução às coleções no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Coleções ajudam a organizar recursos em unidades geríveis. Pode criar coleções para que correspondam às suas necessidades de gestão do cliente e para efetuarem operações nos vários recursos de uma só vez. 

A maioria das tarefas de gestão dependem ou necessitar de utilizar uma ou mais coleções. Apesar de poder utilizar a coleção incorporada de todos os sistemas, utilizá-lo para tarefas de gestão não é uma melhor prática. Crie coleções personalizadas para identificar mais especificamente os dispositivos ou utilizadores para uma tarefa.  

 Coleções incorporadas e personalizadas aparecem no **coleções de utilizadores** e **coleções de dispositivos** nós a **ativos e compatibilidade** área de trabalho na consola do Configuration Manager.  

 Coleções que visualizou recentemente aparecem no **utilizadores** nó e, no **dispositivos** nó o **ativos e compatibilidade** área de trabalho.  

Aqui estão alguns exemplos de utilização de coleção:  

|Operação|Exemplo|  
|---------|-------|  
|Agrupar recursos|Pode criar coleções que recursos de grupo com base na hierarquia da sua organização.<br /><br /> Por exemplo, foi possível criar uma coleção de todos os computadores no "Londres sede" Active Directory unidade organizacional (UO). Para obter mais informações sobre como criar este tipo de coleção, consulte o artigo [como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> Pode utilizar a esta coleção para operações de como configurar definições de Endpoint Protection, configurar as definições de gestão de energia do dispositivo ou instalar o cliente do Configuration Manager.|  
|[Implementação da aplicação]|Pode criar uma coleção de todos os computadores que não tem instalado o Microsoft Office 2013 e, em seguida, implementá-la a todos os computadores nessa coleção.<br /><br /> Também pode utilizar os requisitos da aplicação para efetuar esta tarefa. Para obter mais informações, veja [Como criar aplicações com o System Center Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|[Gerir definições de cliente](../../../../core/clients/deploy/about-client-settings.md)|Embora as predefinições de cliente no Configuration Manager sejam aplicadas a todos os dispositivos e todos os utilizadores, pode criar definições de cliente personalizadas e aplicáveis a uma coleção de dispositivos ou a uma coleção de utilizadores.<br /><br /> Por exemplo, se pretender que o controlo remoto para estar disponível em todos os mas alguns dispositivos, configure as predefinições de cliente para permitir o controlo remoto e, em seguida, configurar definições de cliente personalizadas que não permitir o controlo remoto e implementar aos aplicados para a coleção de clientes excecional. |  
|[Gestão de energia](../power/introduction-to-power-management.md)|Pode configurar as definições de energia específico por coleção.|  
|[Administração baseada em funções](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|Utilize coleções para controlar que grupos de utilizadores têm acesso à funcionalidade vários na consola do Configuration Manager.|  
|[Janelas de manutenção](../../../../core/clients/manage/collections/use-maintenance-windows.md)|Com janelas de manutenção pode definir um período de tempo quando várias operações do Configuration Manager podem ser executadas em membros de uma coleção de dispositivos. |  


## <a name="collection-types-in-configuration-manager"></a>Tipos de coleções no Configuration Manager  
 O Configuration Manager possui as coleções incorporadas para operações comuns e também pode criar coleções personalizadas.   

### <a name="built-in-collections"></a>Coleções incorporadas  
 Por predefinição, o Configuration Manager inclui as seguintes coleções, não podem ser modificadas.  

|**Nome da coleção**|Descrição|  
|-------------------------|-----------------|  
|**Todos os Grupos de Utilizadores**|Contém os grupos de utilizadores que são detetados com a Deteção de Grupos de Segurança do Active Directory.|  
|**Todos os Utilizadores**|Contém os utilizadores que são detetados com a Deteção de Utilizadores do Active Directory.|  
|**Todos os Utilizadores e Grupos de Utilizadores**|Contém as coleções Todos os Utilizadores e Todos os Grupos de Utilizadores. Esta coleção contém o maior âmbito do utilizador e recursos de grupo do utilizador.|  
|**Todos os Clientes de Servidor e de Ambiente de Trabalho**|Contém os dispositivos de servidor e de ambiente de trabalho que tenham o cliente do Configuration Manager instalado. A associação é mantida pela Deteção Heartbeat.|  
|**Todos os Dispositivos Móveis**|Contém os dispositivos móveis que são geridos pelo Configuration Manager. A associação é restrita a esses dispositivos móveis atribuídos com êxito a um site ou detetados pelo conector do Exchange Server.|  
|**Todos os Sistemas**|Contém todos os ambiente de trabalho e clientes de servidor, todos os dispositivos móveis e as coleções de todos os computadores desconhecidos e todos os dispositivos móveis inscritos pelo Microsoft Intune. Esta coleção contém o âmbito maior de recursos do dispositivo.|  
|**Todos os Computadores Desconhecidos**|Contém os registos de computadores genéricos para várias plataformas de computadores. Pode utilizar esta coleção para implementar um sistema operativo ao utilizar uma sequência de tarefas e arranque PXE, suportes de dados de arranque ou suportes de dados pré-configurados.|  

### <a name="custom-collections"></a>Coleções personalizadas  
 Quando cria uma coleção personalizada no Configuration Manager, a associação a essa coleção é determinada por uma ou mais regras de coleção, conforme descrito em [como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md). 



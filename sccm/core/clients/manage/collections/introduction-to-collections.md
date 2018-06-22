---
title: Introdução de coleções
titleSuffix: Configuration Manager
description: Obtenha uma introdução à utilização de coleções no System Center Configuration Manager.
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 48a0788d83ffcd7a373f5f73ee675b62508a6d86
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32333591"
---
# <a name="introduction-to-collections-in-system-center-configuration-manager"></a>Introdução às coleções no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Coleções ajudam-na organizar recursos em unidades geríveis. Pode criar coleções para corresponder as suas necessidades de gestão de cliente e para efetuar operações em vários recursos de uma só vez. 

A maioria das tarefas de gestão dependem ou exigir a utilização de um ou mais coleções. Apesar de poder utilizar a coleção incorporada de todos os sistemas, utilizá-la para tarefas de gestão não é uma melhor prática. Crie coleções personalizadas para identificar mais especificamente os dispositivos ou utilizadores para uma tarefa.  

 Coleções incorporadas e personalizadas aparecem no **coleções de utilizadores** e **coleções de dispositivos** nós a **ativos e compatibilidade** área de trabalho na consola do Configuration Manager.  

 Coleções que visualizou recentemente aparecem no **utilizadores** nó e, no **dispositivos** no nó de **ativos e compatibilidade** área de trabalho.  

Seguem-se alguns exemplos de utilização de coleção:  

|Operação|Exemplo|  
|---------|-------|  
|Agrupar recursos|Pode criar coleções do grupo de recursos com base na hierarquia da sua organização.<br /><br /> Por exemplo, pode criar uma coleção de todos os computadores no "Sede de Londres" Active Directory unidade organizacional (UO). Para obter mais informações sobre como criar este tipo de coleção, consulte [como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> Pode utilizar esta coleção para operações como configurar definições do Endpoint Protection, configurar definições de gestão de energia do dispositivo ou instalar o cliente do Configuration Manager.|  
|[Implementação de aplicação]|Pode criar uma coleção de todos os computadores que têm instalado o Microsoft Office 2013 e, em seguida, implementá-la a todos os computadores nessa coleção.<br /><br /> Também pode utilizar os requisitos da aplicação para efetuar esta tarefa. Para obter mais informações, veja [Como criar aplicações com o System Center Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|[Gerir definições de cliente](../../../../core/clients/deploy/about-client-settings.md)|Embora as predefinições de cliente no Configuration Manager sejam aplicadas a todos os dispositivos e todos os utilizadores, pode criar definições de cliente personalizadas e aplicáveis a uma coleção de dispositivos ou a uma coleção de utilizadores.<br /><br /> Por exemplo, se pretender que o controlo remoto para estar disponível em todos ou alguns dispositivos, configure as predefinições de cliente para permitir o controlo remoto e, em seguida, configurar definições de cliente personalizadas que não permitir o controlo remoto e implementá-los para a coleção de clientes excecionais. |  
|[Gestão de energia](../power/introduction-to-power-management.md)|Pode configurar as definições de energia específico por coleção.|  
|[Administração baseada em funções](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|Utilize coleções para controlar quais os grupos de utilizadores têm acesso a várias funcionalidades na consola do Configuration Manager.|  
|[Janelas de manutenção](../../../../core/clients/manage/collections/use-maintenance-windows.md)|Com janelas de manutenção, pode definir um período de tempo quando podem ser executadas várias operações do Configuration Manager em membros de uma coleção de dispositivos. |  


## <a name="collection-types-in-configuration-manager"></a>Tipos de coleções no Configuration Manager  
 O Configuration Manager possui as coleções incorporadas para operações comuns e também pode criar coleções personalizadas.   

### <a name="built-in-collections"></a>Coleções incorporadas  
 Por predefinição, o Configuration Manager inclui as seguintes coleções, não podem ser modificadas.  

|**Nome da coleção**|Descrição|  
|-------------------------|-----------------|  
|**Todos os Grupos de Utilizadores**|Contém os grupos de utilizadores que são detetados com a Deteção de Grupos de Segurança do Active Directory.|  
|**Todos os Utilizadores**|Contém os utilizadores que são detetados com a Deteção de Utilizadores do Active Directory.|  
|**Todos os Utilizadores e Grupos de Utilizadores**|Contém as coleções Todos os Utilizadores e Todos os Grupos de Utilizadores. Esta coleção contém o maior âmbito de utilizador e de recursos de grupo do utilizador.|  
|**Todos os Clientes de Servidor e de Ambiente de Trabalho**|Contém os dispositivos de servidor e de ambiente de trabalho que tenham o cliente do Configuration Manager instalado. A associação é mantida pela Deteção Heartbeat.|  
|**Todos os Dispositivos Móveis**|Contém os dispositivos móveis que são geridos pelo Configuration Manager. A associação é restrita a esses dispositivos móveis atribuídos com êxito a um site ou detetados pelo conector do Exchange Server.|  
|**Todos os Sistemas**|Contém o ambiente de trabalho de todas as e clientes de servidor, todos os dispositivos móveis e as coleções todos os computadores desconhecidos e todos os dispositivos móveis que são inscritos pelo Microsoft Intune. Esta coleção contém o maior âmbito de recursos dos dispositivos.|  
|**Todos os Computadores Desconhecidos**|Contém os registos de computadores genéricos para várias plataformas de computadores. Pode utilizar esta coleção para implementar um sistema operativo ao utilizar uma sequência de tarefas e arranque PXE, suportes de dados de arranque ou suportes de dados pré-configurados.|  

### <a name="custom-collections"></a>Coleções personalizadas  
 Quando cria uma coleção personalizada no Configuration Manager, a associação a essa coleção é determinada por uma ou mais regras de coleção, conforme descrito em [como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md). 


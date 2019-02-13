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
ms.collection: M365-identity-device-management
ms.openlocfilehash: b9b995d0abfc3f14dce35e0aec70ac25b2ca2853
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138947"
---
# <a name="introduction-to-collections-in-system-center-configuration-manager"></a>Introdução às coleções no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Coleções de ajudar a organizar recursos em unidades geríveis. Pode criar coleções de acordo com suas necessidades de gerenciamento de cliente e para realizar operações em vários recursos de uma só vez. 

A maioria das tarefas de gestão dependem ou requerer a utilização de uma ou mais coleções. Apesar de poder utilizar a coleção incorporada de todos os sistemas, utilizá-lo para tarefas de gestão não é uma prática recomendada. Crie coleções personalizadas para identificar mais especificamente os dispositivos ou utilizadores para uma tarefa.  

 As coleções incorporadas e personalizadas aparecem na **coleções de utilizadores** e **coleções de dispositivos** nós o **ativos e compatibilidade** área de trabalho no Configuration Manager Console.  

 As coleções que visualizou recentemente aparecem no **usuários** nó e, no **dispositivos** nó o **ativos e compatibilidade** área de trabalho.  

Aqui estão alguns exemplos de utilização de coleção:  

|Operação|Exemplo|  
|---------|-------|  
|Agrupar recursos|Pode criar coleções do grupo de recursos com base na hierarquia da sua organização.<br /><br /> Por exemplo, pode criar uma coleção de todos os computadores no "Sede de Londres" Active Directory unidade organizacional (UO). Para obter mais informações sobre como criar este tipo de coleção, consulte [como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> Pode utilizar esta coleção para operações como configurar definições do Endpoint Protection, configurar definições de gestão de energia do dispositivo ou instalar o cliente do Configuration Manager.|  
|[Implementação da aplicação]|Pode criar uma coleção de todos os computadores que não tem instalado o Microsoft Office 2013 e, em seguida, implementá-la para todos os computadores nessa coleção.<br /><br /> Também pode utilizar os requisitos da aplicação para efetuar esta tarefa. Para obter mais informações, veja [Como criar aplicações com o System Center Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|[Gerir definições de cliente](../../../../core/clients/deploy/about-client-settings.md)|Embora as predefinições de cliente no Configuration Manager sejam aplicadas a todos os dispositivos e todos os utilizadores, pode criar definições de cliente personalizadas e aplicáveis a uma coleção de dispositivos ou a uma coleção de utilizadores.<br /><br /> Por exemplo, se pretender que o controlo remoto para estar disponível em todos ou alguns dispositivos, configurar as predefinições de cliente para permitir o controlo remoto e, em seguida, configurar definições de cliente personalizadas que não permitir o controlo remoto e implementá-los para a coleção de excepcional clientes. |  
|[Gestão de energia](../power/introduction-to-power-management.md)|Pode configurar as definições de energia específicas por coleção.|  
|[Administração baseada em funções](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|Utilize coleções para controlar quais grupos de usuários têm acesso a várias funcionalidades na consola do Configuration Manager.|  
|[Janelas de manutenção](../../../../core/clients/manage/collections/use-maintenance-windows.md)|Com janelas de manutenção, pode definir um período de tempo quando podem ser executadas várias operações do Configuration Manager em membros de uma coleção de dispositivos. |  


## <a name="collection-types-in-configuration-manager"></a>Tipos de coleções no Configuration Manager  
 O Configuration Manager possui as coleções incorporadas para operações comuns, e também pode criar coleções personalizadas.   

### <a name="built-in-collections"></a>Coleções incorporadas  
 Por predefinição, o Configuration Manager inclui as seguintes coleções, o que não podem ser modificadas.  

|**Nome da coleção**|Descrição|  
|-------------------------|-----------------|  
|**Todos os Grupos de Utilizadores**|Contém os grupos de utilizadores que são detetados com a Deteção de Grupos de Segurança do Active Directory.|  
|**Todos os Utilizadores**|Contém os utilizadores que são detetados com a Deteção de Utilizadores do Active Directory.|  
|**Todos os Utilizadores e Grupos de Utilizadores**|Contém as coleções Todos os Utilizadores e Todos os Grupos de Utilizadores. Esta coleção contém o maior âmbito de utilizador e grupo de recursos do utilizador.|  
|**Todos os Clientes de Servidor e de Ambiente de Trabalho**|Contém os dispositivos de servidor e de ambiente de trabalho que tenham o cliente do Configuration Manager instalado. A associação é mantida pela Deteção Heartbeat.|  
|**Todos os Dispositivos Móveis**|Contém os dispositivos móveis que são geridos pelo Configuration Manager. A associação é restrita a esses dispositivos móveis atribuídos com êxito a um site ou detetados pelo conector do Exchange Server.|  
|**Todos os Sistemas**|Contém a área de trabalho de todas as e clientes de servidor, a todos os dispositivos móveis e as coleções de todos os computadores desconhecidos e todos os dispositivos móveis inscritos pelo Microsoft Intune. Esta coleção contém o maior âmbito de recursos dos dispositivos.|  
|**Todos os Computadores Desconhecidos**|Contém os registos de computadores genéricos para várias plataformas de computadores. Pode utilizar esta coleção para implementar um sistema operativo ao utilizar uma sequência de tarefas e arranque PXE, suportes de dados de arranque ou suportes de dados pré-configurados.|  

### <a name="custom-collections"></a>Coleções personalizadas  
 Quando cria uma coleção personalizada no Configuration Manager, a associação essa coleção é determinada por uma ou mais regras de coleção, conforme descrito em [como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md). 


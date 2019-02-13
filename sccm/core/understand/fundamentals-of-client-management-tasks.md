---
title: Noções básicas da gestão de cliente
titleSuffix: Configuration Manager
description: Conheça as tarefas que executar para gerir clientes do System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 468d21123e6a4166957b7dcc8cda614a78d2366e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136403"
---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>Noções básicas de tarefas de gestão de cliente do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois de instalar os clientes do System Center Configuration Manager, existem várias tarefas que executar para gerir os clientes.  Algumas das tarefas são executadas a partir da consola do Configuration Manager. Outras tarefas são executadas a partir da aplicação de cliente do Configuration Manager. A aplicação de cliente do Configuration Manager é instalada com o software de cliente do Configuration Manager.

## <a name="configuration-manager-console-tasks"></a>Tarefas da consola do Configuration Manager
 Na consola do Configuration Manager, pode efetuar várias tarefas de gestão de clientes:  

-   Implementar aplicações, atualizações de software, scripts de manutenção e sistemas operativos. Configurar a instalação de uma data e hora específicas, que o software disponível para os utilizadores instalarem quando eles são solicitados ou configurar aplicações para serem desinstaladas.  

-   Ajudar a proteger os computadores contra software maligno e ameaças à segurança, e receber notificações quando forem detetados problemas.  

-   Configure definições de configuração de cliente que pretende monitorizar e remediar em caso de está em conformidade.  

-   Recolher informações do inventário de hardware e software, o que inclui a monitorização e a reconciliação das informações de licença da Microsoft.  

-   Resolver problemas de computadores utilizando o controlo remoto.  

-   Implementar definições de gestão de energia para gerir e monitorizar o consumo de energia dos computadores.  

Consola do Configuration Manager monitoriza as tarefas anteriores em tempo real. Informações de notificação e o estado para cada tarefa estão disponíveis na consola do Configuration Manager. Para capturar dados e tendências históricas, utilize as capacidades de relatório integradas do SQL Server Reporting Services. Os clientes enviam detalhes para o site como o estado do cliente.  Informações de estado do cliente fornecem dados sobre o estado de funcionamento do cliente e a atividade do cliente e são apresentadas na consola ou utilizando relatórios incorporados do Configuration Manager. Estes dados ajudam a identificar computadores que não estão a responder e, em alguns casos, problemas são remediados automaticamente.  

 Para mais informações sobre tarefas de gestão de clientes, veja  [Como gerir os clientes no System Center Configuration Manager](../../core/clients/manage/manage-clients.md) e [Como gerir os clientes para servidores Linux e UNIX no System Center Configuration Manager](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Para obter mais informações sobre como utilizar relatórios, consulte   
            [Introdução aos relatórios no System Center Configuration Manager](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="configuration-manager-client-application"></a>Aplicação de cliente do Configuration Manager  
 Ao instalar o software de cliente do Configuration Manager, a aplicação de cliente do Configuration Manager está instalada demasiado. Ao contrário do Centro de Software, a aplicação de cliente do Configuration Manager foi projetada para o suporte técnico e não para o utilizador final. Algumas opções de configuração requerem permissões administrativas locais e a maioria das opções requer conhecimentos técnicos sobre o funcionamento da aplicação de cliente do Configuration Manager. Pode utilizar esta aplicação para efetuar as seguintes tarefas num cliente:  

-   Ver propriedades sobre o cliente, como o número de compilação, o respetivo site atribuído, a gestão de ponto no qual está a comunicar e, se o cliente está a utilizar um certificado de infraestrutura de chaves públicas (PKI) ou um certificado autoassinado.  

-   Confirme que o cliente transferiu com êxito uma política de cliente depois do cliente é instalado pela primeira vez. Confirme também que as definições de cliente são ativadas ou desativadas conforme previsto, de acordo com as definições de cliente que estão configuradas na consola do Configuration Manager.  

-   Inicie ações do cliente. Por exemplo, transferir a política de cliente se Ocorreu uma alteração de configuração recentes na consola do Configuration Manager e não pretende esperar até que a próxima hora de agendada.  

-   Atribuir um cliente a um site do Configuration Manager ou tentar localizar um site manualmente. Em seguida, especifique o sufixo de sistema de nomes de domínio (DNS) para pontos de gestão que publicam no DNS.  

-   Configure a cache do cliente que armazena temporariamente os ficheiros. Em seguida, elimine ficheiros na cache se necessitar de mais espaço em disco para instalar software.  

-   Configurar as definições da gestão de clientes baseada na Internet.  

-   Ver linhas de base de configuração que foram implementadas no cliente, iniciar a avaliação de compatibilidade e ver relatórios de compatibilidade.  

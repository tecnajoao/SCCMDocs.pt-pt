---
title: Noções básicas de gestão do cliente
titleSuffix: Configuration Manager
description: Saiba mais sobre as tarefas que executar para gerir clientes do System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e517b345340619055b03df22638ec0b491c13d40
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>Noções básicas de tarefas de gestão de cliente do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois de instalar os clientes do System Center Configuration Manager, existem várias tarefas que executar para gerir os clientes.  Algumas das tarefas são executadas a partir da consola do Configuration Manager. Outras tarefas são executadas a partir da aplicação de cliente do Configuration Manager. A aplicação de cliente do Configuration Manager é instalada com o software de cliente do Configuration Manager.

## <a name="configuration-manager-console-tasks"></a>Tarefas da consola do Configuration Manager
 Na consola do Configuration Manager, pode efetuar várias tarefas de gestão de clientes:  

-   Implementar aplicações, atualizações de software, scripts de manutenção e sistemas operativos. Configurar a instalação de uma data e hora específicas, disponibilizar o software para os utilizadores instalarem quando forem necessários ou configurar aplicações para serem desinstaladas.  

-   Ajudar a proteger os computadores contra software maligno e ameaças à segurança, e receber notificações quando forem detetados problemas.  

-   Configure as definições de configuração de cliente que pretende monitorizar e retificar em caso de está em conformidade.  

-   Recolher informações do inventário de hardware e software, o que inclui a monitorização e a reconciliação das informações de licença da Microsoft.  

-   Resolver problemas de computadores utilizando o controlo remoto.  

-   Implementar definições de gestão de energia para gerir e monitorizar o consumo de energia dos computadores.  

Consola do Configuration Manager monitoriza as tarefas anteriores em tempo real. Notificação e informações de estado para cada tarefa estão disponíveis na consola do Configuration Manager. Para capturar os dados e tendências históricas, utilize as capacidades de relatório integradas do SQL Server Reporting Services. Os clientes enviam detalhes para o site como o estado do cliente.  Informações de estado do cliente fornecem dados sobre o estado de funcionamento do cliente e a atividade do cliente e são apresentadas na consola ou utilizando relatórios incorporados para o Configuration Manager. Estes dados ajudam a identificar computadores que não estão a responder e em alguns casos, problemas são remediados automaticamente.  

 Para mais informações sobre tarefas de gestão de clientes, veja [Como gerir os clientes no System Center Configuration Manager](../../core/clients/manage/manage-clients.md) e [Como gerir os clientes para servidores Linux e UNIX no System Center Configuration Manager](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Para obter mais informações sobre como utilizar relatórios, consulte   
            [Introdução aos relatórios no System Center Configuration Manager](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="configuration-manager-client-application"></a>Aplicação de cliente do Configuration Manager  
 Quando instalar o software de cliente do Configuration Manager, a aplicação de cliente do Configuration Manager está instalada demasiado. Ao contrário do Centro de Software, a aplicação de cliente do Configuration Manager foi concebida para o suporte técnico, em vez do utilizador final. Algumas opções de configuração requerem permissões administrativas locais e a maioria das opções requer conhecimentos técnicos sobre o funcionamento da aplicação de cliente do Configuration Manager. Pode utilizar esta aplicação para efetuar as seguintes tarefas num cliente:  

-   Ver propriedades sobre o cliente, como o número de compilação, o respetivo site atribuído, a gestão do ponto de está a comunicar com e se o cliente está a utilizar um certificado de infraestrutura de chaves públicas (PKI) ou um certificado autoassinado.  

-   Certifique-se de que o cliente transferiu com êxito uma política de cliente depois do cliente é instalado pela primeira vez. Confirme que as definições de cliente estão ativadas ou desativadas conforme previsto, de acordo com as definições de cliente que estão configuradas na consola do Configuration Manager.  

-   Inicie ações do cliente. Por exemplo, transferir a política de cliente se tiver ocorrido alguma alteração recente à configuração na consola do Configuration Manager, e não pretender aguardar até a próxima hora agendada.  

-   Atribuir um cliente a um site do Configuration Manager ou tentar localizar um site manualmente. Em seguida, especifique o sufixo de sistema de nomes de domínio (DNS) para pontos de gestão que publicam no DNS.  

-   Configure a cache do cliente que armazena temporariamente os ficheiros. Em seguida, elimine ficheiros na cache se necessitar de mais espaço em disco para instalar o software.  

-   Configurar as definições da gestão de clientes baseada na Internet.  

-   Ver linhas de base de configuração que foram implementadas no cliente, iniciar a avaliação de compatibilidade e ver relatórios de compatibilidade.  

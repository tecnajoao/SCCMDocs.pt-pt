---
title: Ferramentas do Configuration Manager
titleSuffix: Configuration Manager
description: Saiba mais sobre as ferramentas para ajudar a gerir e resolver problemas relacionados com a infraestrutura do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1479524f08f17aa59f6e7dc771253a4fb6720189
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131137"
---
# <a name="configuration-manager-tools"></a>Ferramentas do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As ferramentas do Configuration Manager incluem [baseada no cliente](#client-tools) e [ferramentas baseadas em servidor](#server-tools). Utilize estas ferramentas para ajudar a dar suporte e resolução de problemas de sua infraestrutura do Configuration Manager. 

A partir do Configuration Manager versão 1806, essas ferramentas estão incluídas no `CD.Latest\SMSSETUP\Tools` pasta no servidor do site. Não é necessária nenhuma instalação adicional.<!--1357145--> Utilize estas versões das ferramentas com o Configuration Manager versão 1806 e posterior.

Todos os sistemas de operativos Windows listados como suportado clientes [sistemas operativos suportados por clientes e dispositivos](https://docs.microsoft.com/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) são suportadas para utilização com essas ferramentas.

> [!Note]  
> O [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/en-us/download/details.aspx?id=50012) ainda está disponível no Microsoft Download Center. Para o Configuration Manager versão 1806 e posterior, utilize as versões das ferramentas do CD. Pasta mais recente no servidor do site. Algumas ferramentas estavam anteriormente no Kit de ferramentas, mas não incluído na versão 1806. Essas ferramentas legadas já não são suportadas.


## <a name="client-tools"></a>Ferramentas de cliente

- [CMTrace](/sccm/core/support/cmtrace): Ver, monitorizar e analisar ficheiros de registo do Configuration Manager  

- [Cliente espião](/sccm/core/support/clispy): Resolver problemas relacionados com a distribuição de software, inventário e medição

- [Ferramenta de monitoramento de implementação](/sccm/core/support/deployment-monitoring-tool): Resolver problemas de aplicações, atualizações e implementações de linha de base  

- [Política espião](/sccm/core/support/policy-spy): Atribuições de política do Vista  

- [Ferramenta de visualização de energia](/sccm/core/support/power-viewer-tool): Ver o estado da funcionalidade de gestão de energia  

- [Enviar a ferramenta de agendamento](/sccm/core/support/send-schedule-tool): Agendas de Acionador e avaliações de linhas de base de configuração  

> [!Note]  
> A pasta de ClientTools também inclui o ficheiro Microsoft.Diagnostics.Tracing.EventSource.dll. Várias ferramentas de cliente requerem esta biblioteca. Não é possível usá-lo diretamente.  


## <a name="server-tools"></a>Ferramentas do servidor

- [Gestor de filas de trabalho de DP](/sccm/core/support/dp-job-manager): Soluciona problemas em tarefas de distribuição de conteúdo para pontos de distribuição  

- [Visualizador de avaliação de coleção](/sccm/core/support/ceviewer): Ver detalhes de avaliação de coleção  

- [Explorador de biblioteca de conteúdos](/sccm/core/support/content-library-explorer): Ver o conteúdo do arquivo de instância única biblioteca de conteúdos  

- [Biblioteca de transferência de conteúdo](/sccm/core/support/content-library-transfer): Transfere conteúdos a biblioteca de unidades  

- [Ferramenta de propriedade de conteúdo](/sccm/core/support/content-ownership-tool): Propriedade de alterações de pacotes órfãos. Esses pacotes existem no site sem um servidor de site proprietário.  

- [Administração baseada em funções e a ferramenta de auditoria](/sccm/core/support/rbaviewer): Ajuda os administradores de configuração de funções de auditoria  

- [Execute a ferramenta de resumo de medidor](/sccm/core/support/run-meter-summ): Executar tarefa de resumo de medição e analisar dados de medição

> [!Note]  
> A pasta de ServerTools também inclui os seguintes ficheiros 
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll. 
>
> Várias ferramentas de servidor requerem dessas bibliotecas. Não é possível usá-los diretamente.  



## <a name="other-tools"></a>Outras ferramentas

- [Ferramenta de limpeza da biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool): Uso **ContentLibraryCleanup.exe** no `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` para remover o conteúdo órfão a partir de um ponto de distribuição.  

- [Ferramenta manutenção da hierarquia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe): Uso **Preinst.exe** no `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` pasta partilhada no servidor do site para passar os comandos para o componente de Gestor da hierarquia.  

- [Ferramenta de reposição de atualizações](/sccm/core/servers/manage/update-reset-tool): Uso **CMUpdateReset.exe** no `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` para corrigir os problemas quando as atualizações na consola tem problemas ao transferir ou replicar.  

- [Ferramenta de ligação de serviço](/sccm/core/servers/manage/use-the-service-connection-tool): Uso **ServiceConnectionTool.exe** no `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` para manter o seu site atualizado quando o ponto de ligação de serviço está offline.  

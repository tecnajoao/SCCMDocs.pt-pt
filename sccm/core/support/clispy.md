---
title: Espião do Cliente
titleSuffix: Configuration Manager
description: Utilize espião de cliente para resolver problemas de distribuição de software, inventário e medição de software nos clientes do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b90628e4f1e4a1405c90d17fc43628df00070978
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123387"
---
# <a name="client-spy"></a>Espião do Cliente

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Espião do cliente é um da [ferramentas do Configuration Manager](/sccm/core/support/tools). É uma ferramenta de resolução de problemas de distribuição de software, inventário e medição de software nos clientes do Configuration Manager. 

A maioria das informações obtidas pela ferramenta pertence às implementações de software:
- Todas as implementações de software atual 
- Histórico de distribuição de software
- A configuração de cache do cliente
- Itens em cache
- Implementações necessárias pendentes
- Implementações disponíveis  

Também apresenta as seguintes informações de inventário
- O data do ciclo de inventário mais recente
- A última data de relatório
- Versão de principal e secundária de inventário de software
- Recolha de ficheiros
- Inventário de Hardware
- Recolha IDMIF
- Registos de dados de deteção (DDR) 

Regras de medição de software também são exibidas. 

> [!Note]   
> Para melhorar o desempenho, a ferramenta só recolhe informações para cada guia quando selecioná-lo. Da mesma forma, quando clica em **atualizar**, ele só atualiza as informações para o separador atualmente exibido.



## <a name="usage"></a>Utilização


### <a name="tools-menu"></a>Menu Ferramentas

As ações seguintes estão disponíveis no **ferramentas** menu:  

#### <a name="connect"></a>Ligar
Obter as informações num computador diferente.  

- Por predefinição, a ferramenta Exibe informações do computador atual. 

- Ligue-se de utilizar o nome do computador remoto, o nome de utilizador e a palavra-passe para a conta. A ferramenta faz uma ligação para o IPC$ partilhar no computador remoto. Elimina a ligação quando a ferramenta é encerrado ou ligar a outro computador.  

- Ele requer uma conta com credenciais suficientes para obter as informações.  

- Se não especificar um nome de utilizador e palavra-passe, o cliente Spy utiliza o contexto de segurança do utilizador atualmente com sessão iniciada para tentar estabelecer a ligação.  

- Quando se liga a um computador remoto, todas as guias exibidas mostram informações do computador remoto.

#### <a name="software-distribution"></a>Distribuição de software
Apresenta o [distribuição de Software](#software-distribution) separadores e oculta os outros guias. Por predefinição, o cliente espião apresenta os separadores de distribuição de Software.

#### <a name="inventory"></a>Inventário
Apresenta o separador de inventário e oculta os outros guias.

#### <a name="software-metering"></a>Medição de Software
Apresenta o separador de medição de Software e oculta os outros guias.

#### <a name="save-current-tab-to-file"></a>Guardar ficheiro separador atual
Guarda as informações no separador atualmente exibido num arquivo de texto que especificar. 

#### <a name="save-all-tabs-to-file"></a>Guarde todos os separadores no ficheiro
Guarda as informações em todos os separadores num arquivo de texto que especificar. Ela salva apenas informações que pode ver a sua conta.



## <a name="software-distribution-tab"></a>Guia de distribuição de software

Configure as definições nas quatro seguintes guias:
- [Solicitações de execução de distribuição de software](#bkmk_exec-requests)
- [Histórico de distribuição de software](#bkmk_history)
- [Informações de Cache de distribuição de software](#bkmk_cache-info)
- [Distribuição de software pendentes de execuções](#bkmk_pending-exec)


### <a name="bkmk_exec-requests"></a> Solicitações de execução de distribuição de software

Este separador apresenta todas as implementações existentes, incluindo a ambas as implementações direcionadas de dispositivo e utilizador.

Cada item da árvore no separador de solicitações de execução de distribuição de Software contém os seguintes quatro atributos:
- ID do anúncio. Este valor pode estar em branco, caso se trate de uma implementação de disponibilidade. 
- ID do pacote 
- Nome do programa 
- Utilizador. Isso pode ser o utilizador-alvo SID ou o SID do utilizador que iniciou o pedido. Se ambos estiverem pedidos de sistema, o utilizador apresentado é o sistema. 

Para cada solicitação de execução, ele também apresenta as seguintes informações numa estrutura de subárvore:
- Nome do programa 
- ID do pacote 
- Nome do Pacote 
- Hora de criação do pedido 
- Estado 
- Estado de execução, se o estado está em execução 
- Contexto de execução (utilizador ou administrador) 
- Histórico de estado (êxito, falha ou NotRun) 
- LastRunTime (Never, se ainda não foi executado o programa) 
- RetryCount, se o estado é WaitingRetry 
- ContentAccess (Repetir contagem, se o estado é WaitingRetry) 
- FailureCode, se o estado é WaitingRetry 
- FailureReason, se o estado é WaitingRetry 

Se precisar do pedido de conteúdo, o estado é WaitingContent. O separador de informações de Cache de distribuição de Software mostra os detalhes para este pedido de transferência.

Se o pedido de execução é um pedido de transferência, também apresenta o número de bytes transferidos.

> [!Note]   
> Ele usa ícones diferentes para diferentes Estados de um pedido de execução.


### <a name="bkmk_history"></a> Histórico de distribuição de software

Este separador contém informações sobre todos os programas de execução anterior. Essas informações são armazenadas no Registro.

As ramificações principais dessa árvore são os históricos de utilizador diferente, incluindo o sistema. Apresenta uma subárvore contendo a lista de pacotes a partir do qual os programas tenham sido executados para cada utilizador. 

O nome de ID e o pacote do pacote para cada subárvore de pacote apresenta uma lista de programas que foram executados. Apresenta os seguintes atributos para cada: 
- Nome do programa
- Estado de execução
- Hora da última execução
- Código de falha
- Motivo da falha  

O código de falha e o motivo da falha são em branco quando um programa foi executado com êxito.


### <a name="bkmk_cache-info"></a> Informações de Cache de distribuição de software

#### <a name="cache-config"></a>Cache Config
Contém informações sobre a cache do cliente do Configuration Manager. Estas informações incluem a localização da cache, o tamanho da cache, e se ele está atualmente em utilização. 

#### <a name="cached-items"></a>Itens em cache
Contém uma subárvore de todos os itens atualmente na cache. Cada item da árvore inclui as seguintes informações sobre cada item: 
- Localização do item (pasta) na cache
- Estado atual
- ID do pacote
- Nome do pacote
- Versão do pacote
- Tamanho do pacote
- Contagem de referência atual
- Hora da última referenciada (UTC)  

#### <a name="downloading-items"></a>Transferência de itens
Estes são os itens que o cliente está a transferir. Cada um deles mostra as mesmas informações apresentadas pelos itens em cache e o número de quilobytes transferido. 


### <a name="bkmk_pending-exec"></a> Distribuição de software pendentes de execuções

Este separador contém informações que explica em detalhe as implementações necessárias últimas e futuras e uma lista de implementações disponíveis.

Cada ramificação de árvore destina-se a cada conta de utilizador com as implementações disponíveis, incluindo o sistema.

Para cada utilizador, uma árvore de sub-rotina contém os seguintes três itens:  

#### <a name="mandatory-advertisements-with-future-executions"></a>Anúncios obrigatórios determinam com execuções futuras
Estes são os anúncios obrigatórios determinam que ainda têm programas restantes para ser executado. Estes podem ser qualquer um dos recorrente, uma única vez, ou vários anúncios de agenda. Cada um apresenta o ID de anúncio, a próxima hora de execução e a agenda em que o anúncio é executado. 

#### <a name="optional-advertisements"></a>Anúncios opcionais
Apresenta uma lista de todos os anúncios que são publicadas. Ele também exibe detalhes como ID de anúncio, o nome do programa e o nome do pacote para cada um. 

#### <a name="past-mandatory-advertisements-with-no-future-scheduled-executions"></a>Nos últimos anúncios obrigatórios determinam com nenhuma futuro agendada de execuções
Esta é uma lista de anúncios que existem no cliente que não tenham nenhum futuros programas agendados para ser executada. O ID de anúncio, o nome do pacote e o nome do programa são apresentados. Um item de subárvore é apresentado para todos os anúncios que são opcionais.

> [!Note]  
> Informações do nome do pacote só estão disponíveis para pacotes que tenham anunciados as políticas associadas aos mesmos no computador a ser visualizado. Pacotes que já não têm políticas disponíveis associadas a eles exibir a mensagem "Pacote nome já não são disponíveis".  



## <a name="inventory-tab"></a>Separador inventário

Há apenas um guia que contém informações de inventário. A árvore principal contém os seguintes cinco itens:  

- **Inventário de software**: Contém a data em que o último ciclo iniciado, a data do último relatório e as versões principais e secundárias do último relatório.  

- **Recolha de ficheiros**: Contém a data em que o último ciclo iniciado, a data do último relatório e as versões principais e secundárias do último relatório.  

- **Inventário de hardware**: Contém a data em que o último ciclo iniciado, a data do último relatório e as versões principais e secundárias do último relatório.  

- **Recolha IDMIF**: Contém a data em que o último ciclo iniciado, a data do último relatório e as versões principais e secundárias do último relatório.  

- **DDR**: Contém a data em que o último ciclo iniciado, a data do último relatório e as versões principais e secundárias do último relatório. As informações de DDR também são apresentadas numa subárvore.



## <a name="software-metering-tab"></a>Separador de medição de software

Este separador apresenta informações como uma subárvore e inclui todas as regras de medição de software. Ela exibe cada regra como um nó, o que ele identifica pelo ID de ficheiro nome e a regra. Expanda cada nó na árvore e ver as seguintes informações:
- Nome de ficheiro do Explorer 
- Nome do ficheiro original
- ID de regra
- Versão do ficheiro
- Linguagem



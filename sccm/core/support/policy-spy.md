---
title: Espião de Política
titleSuffix: Configuration Manager
description: Utilize espião de política para ver e resolver problemas relacionados com o sistema de política em clientes do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1012ec24-27d9-4193-8236-918d283c7448
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 740dda5c41c28e1648eb24e75fe24a2e22784f3b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129109"
---
# <a name="policy-spy"></a>Espião de Política

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Espião de política é uma da [ferramentas do Configuration Manager](/sccm/core/support/tools). É uma ferramenta para ver e resolver problemas do sistema de política em clientes do Configuration Manager. Execute **PolicySpy.exe** para abrir a interface do usuário. Para obter mais informações sobre a utilização da linha de comandos, consulte [sintaxe de linha de comando](#bkmk_policyspy-syntax).

> [!Important]  
> Espião de política de executar como administrador. Se não o fizer **executar como administrador**, verá o seguinte erro das informações de cliente de:  
> `There is no client installed on this machine. Connection to client policy failed with error 80041003`


## <a name="bkmk_policyspy-syntax"></a> Sintaxe da linha de comandos

Política espião destina-se principalmente para uso por meio de sua interface do usuário. Ela fornece opções de linha de comando limitadas para oferecer suporte a automatização e processamento em lotes.

`PolicySpy.exe [/export <ExportFilename> [<computername>]]`

### <a name="option-export"></a>Opção: `/export`
Esta opção exporta silenciosamente a política do computador local ou remoto. `<ExportFilename>` é o nome de ficheiro ao qual a ferramenta salva o XML exportado política. Se especificar o `<computername>` opção, a política de espião exporta a política do computador em vez do computador local.

> [!Note]  
> Esta opção da linha de comandos não fornece uma forma de especificar as credenciais do utilizador. Para utilizar credenciais alternativas para aceder a um computador remoto, utilize o **runas** comando para abrir uma nova linha de comando com as credenciais de segurança necessário.  


## <a name="usage"></a>Utilização

### <a name="tools-menu"></a>Menu Ferramentas

As ações seguintes estão disponíveis no **ferramentas** menu:  

- **Abrir remoto**: Liga-se para a política de cliente do Configuration Manager num computador remoto. Utilize a caixa de diálogo Connect para obter o nome do computador remoto e as credenciais de utilizador opcional. Se a ligação falhar, ele exibe informações de erro no painel de informações do cliente. Se a ligação falhar novamente, tente ligar-se ao selecionar **Atualize** sobre o **editar** menu, ou pressionando F5.  

- **Abrir ficheiro**: Abre um ficheiro de exportação de política (XML) criado pelos **Exportar política** opção. A ferramenta exibe a política exportada exatamente da mesma como uma política em direto. Desativa a algumas funcionalidades que só se aplicam quando se liga a um cliente real.  

- **Atribuições de máquina do pedido**: Aciona um pedido de existência de atribuições de política de computador no computador de destino. Esta funcionalidade está desativada quando a visualização exportados política.  

- **Avaliar política de computador**: Aciona uma avaliação de políticas de computador no computador de destino. Esta funcionalidade está desativada quando visualizar uma política de exportado.  

- **Atribuições de utilizador do pedido**: Aciona um pedido de existência de atribuições de política de utilizador para o utilizador tem atualmente sessão iniciada. Esta funcionalidade só está disponível quando visualiza uma política no computador local.  

- **Avaliar política de utilizador**: Aciona uma avaliação de políticas de utilizador para o utilizador tem atualmente sessão iniciada. Esta funcionalidade só está disponível quando visualiza uma política no computador local.  

- **Política de reposição de**: Remove todas as políticas de não-padrão e repõe os cookies de política para o site. Em seguida, aciona uma solicitação de atribuições de política de computador. Esta funcionalidade está desativada quando visualizar uma política de exportado.  

- **Exportar política**: Exporta a política do computador de destino para um arquivo XML. Ver este ficheiro em qualquer computador com a política de espião. Para abrir o ficheiro de exportação, selecione **abrir o ficheiro** sobre o **ferramentas** menu. Esta funcionalidade está desativada quando visualizar uma política de exportado.  


### <a name="edit-menu"></a>Menu Editar

As ações seguintes estão disponíveis no **editar** menu:  

- **Delete**: Elimina a instância selecionada no painel de resultados. Esta ação só é suportada para instâncias de política. Se tentar eliminar nada além de instâncias de política, a ferramenta exibe uma mensagem de erro. Esta funcionalidade está desativada quando visualizar uma política de exportado.  

- **Atualizar**: Atualiza todos os resultados para ver as informações mais recentes. Todos os nós da árvore que são expandidos antes de atualizar automaticamente são expandidos mais tarde. Se espião de política não foi ligado com êxito a política do computador de destino, ele tenta estabelecer ligação novamente. Esta funcionalidade está desativada quando visualizar uma política de exportado.  

- **Limpar eventos**: Limpa todos os itens do separador de eventos.  



## <a name="results-pane"></a>Painel de resultados

O painel de resultados apresenta vistas diferentes do sistema de política no computador de destino. Aceda a esses modos de exibição clicando em um dos seguintes quatro separadores: 
- [Actual](#bkmk_policyspy-actual)
- [Pedido](#bkmk_policyspy-requested)
- [Predefinição](#bkmk_policyspy-default)
- [eventos](#bkmk_policyspy-events)


### <a name="bkmk_policyspy-actual"></a> Real

Este separador apresenta a política atual do cliente. A política atual determina o comportamento de um cliente e o comportamento dos seus agentes de cliente, tais como distribuição de software e inventário. A guia exibe resultados num formato de árvore com um nó de raiz para o espaço de nomes de computador e cada espaço de nomes de utilizador específico. Expanda um nó de espaço de nomes a apresentar uma lista de classes. Expanda uma classe para apresentar uma lista das suas instâncias. A lista de classe inclui apenas as classes que tenham instâncias.


### <a name="bkmk_policyspy-requested"></a> Pedido

Este separador apresenta as atribuições de política que o cliente obtido a partir do respetivo site atribuído. A guia exibe resultados em formato de árvore com um nó de raiz para o espaço de nomes de computador e cada espaço de nomes de utilizador específico. Expandir um nó de espaço de nomes apresenta os seguintes nós:  

- **Configuração**: Apresenta uma lista de classes de configuração derivadas de CCM_Policy_Config, que inclui o objeto de política, as atribuições e outros.  

- **Definições**: Apresenta todas as definições de Active Directory geradas pelas políticas. As definições são apresentadas sob o nó de configuração. 

> [!Note]   
> Várias instâncias podem existir com o mesmo nome porque o cliente ainda não intercaladas estas definições de um conjunto final resultante. Política espião apresenta instâncias neste nó usando as propriedades de RealKey em vez das chaves de política verdadeiro. Correlacione essas instâncias para o conjunto resultante apresentado no separador real.  


### <a name="bkmk_policyspy-default"></a> Default

Este separador apresenta as mesmas informações que o **pedida** separador. Ele também inclui o conteúdo dos namespaces DefaultMachine e DefaultUser.


### <a name="bkmk_policyspy-events"></a> eventos

Este separador apresenta os eventos de agente de política à medida que acontecem. O modo de exibição cria uma subscrição de evento do WMI para todos os eventos derivado de CCM_PolicyAgent_Event. A exibição mostra um máximo de 200 eventos. Remove os eventos mais antigos da parte superior da lista, conforme necessário. Se selecionar o último item na lista, a lista avança automaticamente para baixo conforme adiciona novos eventos. Caso contrário, a exibição mantém sua posição atual e terá de deslocar para baixo ou prima a tecla de fim para ver os novos eventos. Esta vista está sempre vazia quando visualizar uma política de exportado.



## <a name="client-info-pane"></a>Painel de informações do cliente
O painel de informações do cliente apresenta uma lista de propriedades para o computador de destino. Apresenta as seguintes propriedades, se disponível:  
- Nome
- ID
- Versão
- Site
- MP atribuído
- MP residente
- MP do proxy
- Estado do proxy



## <a name="details-pane"></a>Painel de detalhes
O painel de detalhes mostra informações detalhadas sobre a seleção atual. Se nenhuma seleção estiver ativa, ele exibe informações sobre a política espião em si, incluindo a versão. Caso contrário, ele exibe uma representação de gerir formato MOF (Object) do item selecionado.

Política espião usa sua própria rotina de MOF geração para criar uma exibição HTML mais amigável do que o MOF de texto sem formatação gerado pelo WMI. Este comportamento permite espião de política adicionar os seguintes recursos para tornar o MOF mais legíveis:  

- Realce de sintaxe  

- Objetos recuados e matrizes  

- Propriedades são dispostas em grupos locais e do sistema herdado. Por padrão, ele fecha o sistema e herdadas de grupos. Pode ver de imediato as propriedades, na verdade, usa a instância.  

- Copie o MOF ou copiar texto sem formatação MOF para a área de transferência. Esta funcionalidade é útil para colar o MOF em outros aplicativos chamando diretamente a ferramenta MofComp.  

Para instâncias de objetos de política derivam CCM_Policy_Policy, o painel de detalhes apresenta a política de corpo abaixo o MOF que exibe. Se o cliente não tiver transferido o corpo de política, a política de espião exibe um hiperlink. Clique na ligação para transferir o corpo de política diretamente a partir do ponto de gestão do cliente. Se a ferramenta downloads com êxito o corpo de política, ele substitui o hiperlink com o conteúdo de resposta. Caso contrário, política de espião atualiza a exibição que indica que o pedido falhou.


---
title: Referência à IU do Support Center
titleSuffix: Configuration Manager
description: Saiba como utilizar as ferramentas do Centro de suporte.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 41cdebfe-b595-40aa-a385-32e0746255ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 970d2fbf69a7c4c91a55cadf5d420988b2207ca2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131103"
---
# <a name="support-center-user-interface-reference"></a>Referência de interface de usuário do Centro de suporte

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo é uma referência que descreve as interfaces de utilizador (IU) das ferramentas do Centro de suporte:
- Centro de Suporte
- Visualizador de Log do Centro de suporte
- Support Center Viewer



## <a name="support-center-reference"></a>Referência do Centro de suporte

Esta secção descreve a interface do usuário para o **Support Center** ferramenta. 
- [Menu da janela](#bkmk_support-window)  
- [Separador PáginaL principal](#bkmk_support-home)  
- [Separador do cliente](#bkmk_support-client)  
- [Separador política](#bkmk_support-policy)  
- [Separador conteúdo](#bkmk_support-content)  
- [Separador inventário](#bkmk_support-inventory)  
- [Guia de resolução de problemas](#bkmk_support-troubleshoot)  
- [Separador registos](#bkmk_support-logs)  


### <a name="bkmk_support-window"></a> Menu da janela

No canto superior esquerdo da janela do Centro de suporte, selecione a seta na caixa de azul para abrir esse menu.

#### <a name="local-machine-connection"></a>Ligação ao computador local
Centro de suporte reúne os arquivos de log e efetua a resolução de problemas no cliente que está a executar o Support Center.

#### <a name="remote-connection"></a>Ligação remota
Estabelece uma ligação remota com outro cliente de Configuration Manager. Depois de ligar, o Support Center reúne os ficheiros de registo e efetua a resolução de problemas no cliente ao qual está ligado.

#### <a name="about"></a>sobre
Fornece informações sobre o Support Center.

#### <a name="options"></a>Opções
Na **opções** caixa de diálogo, pode:
- Reduzir o movimento dos elementos da interface do usuário animados  
- Alterar a predefinição guardar a localização para os ficheiros de pacote de dados  
- Alterar a localização dos ficheiros temporários    
- Repor os avisos. Todas as mensagens de aviso que anteriormente suprimidos novamente apresentadas quando acionadas.  
- Repor o caminho de ficheiro temporário na sua predefinição, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenter`

#### <a name="exit"></a>Sair
Fechar o Centro de suporte.



### <a name="bkmk_support-home"></a> Separador PáginaL principal

#### <a name="collect-selected-data"></a>Recolher dados selecionados
Centro de suporte recolhe informações de cliente do Configuration Manager. Por predefinição, recolhe os seguintes tipos:
- Ficheiros de registo
- Recoletor de configuração do cliente
- Sistema Operativo

Para recolher outros tipos de informações, selecione a caixa de verificação junto ao nome desse tipo.

Selecione o menu pendente na parte inferior a **recolher dados selecionados** botão na faixa de opções e selecione **recolher todos os dados**. Esta ação recolhe o conjunto completo de dados de estado do cliente.

Embora o Support Center está a recolher dados, selecione **Cancelar coleção** interrompê-lo.

#### <a name="data-types"></a>Tipos de dados
Quando seleciona a caixa de verificação para uma opção, o Support Center recolhe esse tipo de dados da próxima vez que selecione **recolher dados selecionados**. Estão disponíveis os seguintes tipos:  

- **Ficheiros de registo**: Ficheiros de registo de cliente incluindo registos de configuração  

- **Política**: Coleção de política de cliente  

- **Certificados**: Informações de chaves públicas para certificados de cliente. Centro de suporte não recolhe as chaves privadas do certificado.  

- **Recoletor de configuração do cliente**: Informações de cliente do Configuration Manager. Não é possível desativar este tipo de dados.  

- **Registo de cliente**: Recolhe informações de configuração de cliente a partir do registo. Centro de suporte só recolhe informações de registo do Configuration Manager.  

- **WMI cliente**: Informações de configuração de cliente do WMI. Centro de suporte não recolhe a política de cliente.  

- **Resolução de problemas**: Dados de resolução de problemas em tempo real para ajudar a diagnosticar problemas comuns de clientes com o Active Directory, pontos de gestão, redes, atribuições de políticas e registo.  

    > [!NOTE]  
    > Este tipo de dados não é suportado quando estabelecer uma ligação remota a outro cliente.  

- **Informações de depuração**: Efetue a depuração de despejo do cliente e os processos relacionados. Informações de depuração podem ser grandes. Permitir que esta opção apenas quando a resolução de problemas com o desempenho do cliente.  

    > [!WARNING]  
    > Recolher informações de depuração fará com que os pacotes de dados fique demasiado grande (em alguns casos, várias centenas de MB).  
    >  
    > Depurar despejos contêm Maio conter informações confidenciais, incluindo palavras-passe, segredos criptográficos ou dados de utilizador. Informações de depuração só devem ser recolhidas sob recomendação do pessoal de Support da Microsoft. Pacotes de dados que contenham informações de depuração devem ser processados cuidadosamente para protegê-los contra acesso não autorizado.  
    >  
    > Este tipo de dados não é suportado quando estabelecer uma ligação remota a outro cliente.  

- **Sistema operativo**: Recolhe informações de configuração sobre o computador local. Estes dados incluem informações sobre a instalação, adaptadores de rede e configuração do serviço de sistema do Windows. Não é possível desativar este tipo de dados.  



### <a name="bkmk_support-client"></a> Separador do cliente

#### <a name="load-or-refresh"></a>Carregar ou atualizar
Centro de suporte carrega ou atualiza os detalhes para o cliente do Configuration Manager.

#### <a name="control-client-agent-service"></a>Serviço de agente de cliente de controlo
Execute uma das seguintes ações sobre o serviço de agente de cliente (ccmexec) de Configuration Manager no cliente ligado:  

- **Reiniciar cliente**  

    > [!IMPORTANT]  
    > Se o serviço de agente de cliente não reiniciado com êxito, o cliente não é gerido pelo Configuration Manager até que o serviço for iniciado.  

- **Iniciar o cliente do**  

- **Parar cliente**  

    > [!IMPORTANT]  
    > O cliente não é gerido pelo Configuration Manager até que o serviço for iniciado.  

#### <a name="properties"></a>Propriedades
Quando carrega os detalhes do cliente, o Support Center mostra as seguintes propriedades:  

- **ID de cliente**: Um identificador exclusivo do Configuration Manager utiliza para identificar o cliente  

- **ID de hardware**: Um identificador exclusivo do Configuration Manager utiliza para identificar o hardware de cliente  

- **Aprovado**: Indica se o cliente é aprovado no Configuration Manager  

- **Estado de registo**: Indica se o cliente está registado com o Configuration Manager  

- **Internet-facing**: Indica se o cliente está na internet  

- **Versão**: O número de versão de cliente do Configuration Manager instalado  

- **Código do site**: O código do site para o site primário ao qual o cliente é atribuído  

- **Atribuído MP**: O nome de domínio completamente qualificado (FQDN) do cliente do ponto de gestão atualmente atribuído  

- **MP residente**: O FQDN do ponto de gestão residente  

- **MP do proxy**: O nome de anfitrião ou o FQDN da gestão de proxy do ponto (se existir)  

- **Código do Site de proxy**: O código do site para o site secundário (se existir)  

- **Estado do proxy**: O estado do ponto de gestão do proxy do cliente do Configuration Manager. Por exemplo, **Active Directory** ou **pendente**.  



### <a name="bkmk_support-policy"></a> Separador política

Utilizar as ações neste separador, em vez do antigo [PolicySpy](/sccm/core/support/policy-spy) ferramenta.

#### <a name="load-policy"></a>Carregar política
Esta opção varia consoante o modo de exibição:

- **Carregar política real**: Selecione **real** na vista de grupo e, em seguida, selecione esta opção no grupo de política. Centro de suporte carrega a política de cliente que selecionou atualmente.  

- **Carregar política pedida**: Selecione **pedida** na vista de grupo e, em seguida, selecione esta opção no grupo de política. Centro de suporte carrega a política pedida do cliente.  

- **Carregar política predefinida**: Selecione **predefinido** na vista de grupo e, em seguida, selecione esta opção no grupo de política. Centro de suporte carrega a política predefinida para este cliente.  

Selecione a lista pendente na parte inferior deste botão para obter opções adicionais:

- **Carregar ou atualizar tudo**: Carrega ou atualiza real, pedida e política predefinida ao mesmo tempo.  

#### <a name="actual-view"></a>Modo de exibição real
Abre a vista de política real

#### <a name="requested-view"></a>Vista pedida
Abre a vista de política pedida

#### <a name="default-view"></a>Modo de exibição padrão
Abre a vista de política predefinida. (Esta política é o que dispositivos obtém ao instalar o cliente do Configuration Manager).

#### <a name="request-and-evaluate-policy"></a>Pedir e avaliar política
Centro de suporte solicita a política de cliente a partir do ponto de gestão e, em seguida, avalia essa política no cliente.

Selecione a lista pendente na parte inferior deste botão para obter opções adicionais:  

- **Pedir política**: Centro de suporte solicita a política de cliente do ponto de gestão.  

- **Avaliar política**: Centro de suporte avalia a política de cliente no cliente.  

- **Repor política para predefinição**: Centro de suporte informa ao cliente do Configuration Manager para reaplicar a política predefinida. Remove todas as políticas de computador e utilizador no cliente.  

#### <a name="listen-for-policy-events"></a>Escutar eventos de políticas
Centro de suporte escuta eventos de políticas. Selecione esta opção novamente para desativar a escutar eventos de políticas. Para ver **eventos política**, selecione a seta na parte inferior neste guia. 

#### <a name="clear-events"></a>Eventos de limpeza
Centro de suporte Limpa quaisquer eventos de política.



### <a name="bkmk_support-content"></a> Separador conteúdo

Ver conteúdo no cliente, incluindo armazenados em cache o conteúdo. Monitorize o progresso das implementações de atualizações e aplicações de software. 

#### <a name="load-or-refresh"></a>Carregar ou atualizar
*Aplica-se para os modos de exibição de conteúdo e Cache*

Centro de suporte carrega ou atualiza a lista de conteúdo atualmente no cliente.

#### <a name="invoke-trigger"></a>Invocar acionador
Os seguintes itens neste menu uma ação de cliente relacionadas com conteúdo do pedido:  

- **Serviços de localização**  

    - **Atualizar localizações de conteúdo**: Atualiza os pontos de distribuição utilizados por quaisquer transferências de conteúdo ativas.  

    - **Atualizar pontos de gestão**: Atualiza a lista interna de pontos de gestão utilizado pelo cliente.  

    - **Pedidos de conteúdo de tempo limite**: Se quaisquer pedidos de localização de conteúdo tem de estar em execução há demasiado tempo, esta ação deixa o pedido.  

  - **Avaliação de implementação de aplicação**: Inicia uma tarefa que avalia aplicações implementadas.  

  - **Avaliação da implementação de atualizações de software**: Inicia uma tarefa que avalia atualizações de software implementadas.  

  - **Análise da origem de atualizações de software**: Inicia uma tarefa que analisa as localizações de origem das atualizações.  

  - **Atualização da lista de origem Windows Installer**: Inicia uma tarefa que atualiza a localização de origem para instalações do Windows Installer (MSI).  

#### <a name="content-view"></a>Vista de conteúdo
Ver aplicações, pacotes e atualizações carregados no cliente. Quando seleciona uma aplicação, pacote ou atualização, pode ver detalhes sobre esse conteúdo. Para alguns aplicativos, também pode efetuar as seguintes ações:  

 - **Atualizar**: Atualize a vista de detalhes  

 - **Certifique-se ou transferir**: Certifique-se de que um aplicativo está disponível para download  

 - **Instalar**: Instalar a aplicação  

 - **Desinstalar**: Desinstalar a aplicação  

#### <a name="cache-view"></a>Vista de cache
Ver a configuração da cache do cliente e detalhes sobre o conteúdo da cache. Quando liga o Centro de suporte a um cliente local, AC também fazer as seguintes ações:  

 - Para alterar a localização da cache, selecione **alterar** junto a **localização da Cache** campo.  

 - Para ajustar o tamanho da cache, selecione **alteração** junto a **tamanho da Cache** campo.  

 - Para limpar a cache do cliente, selecione **desmarque** junto a **Cache em utilização** campo.  

Esta vista mostra as seguintes propriedades:  

 - **Localização**: A localização de cada pasta de cache. Selecione a ligação para abrir a pasta no Explorador do Windows.   
 - **ID de conteúdo**  
 - **Cache ID**  
 - **Size**  
 - **Última referenciada**: Esta propriedade é a data quando o cliente pela última vez ler ou escreveu a este item na cache.  

#### <a name="monitoring-view"></a>Vista de monitorização
Selecione **Monitor** para ver o progresso de ativo de software atualizações e aplicações implementações de atualizações. Esta vista mostra as mensagens de estado geradas a partir da aplicação e mensagens de eventos do WMI de atualizações de software.

Para cada evento, a exibição mostra as seguintes propriedades:  

 - **Tempo**: O tempo que o cliente gerou o evento  
 - **Tipo de tópico**: O tipo de mensagem de estado  
 - **ID de tópico**: ID da mensagem de estado, utilizada para mapear para eventos em ficheiros de registo  
 - **Tipo de ID de tópico**: O subtipo da mensagem de estado  
 - **ID de estado**: O resultado da ação que estiver a monitorizar  
 - **Detalhes** e **dados de eventos**: Mais informações sobre as mensagens de estado apresentadas nesta vista. Detalhes do Estado, às vezes, podem estar em branco.  



### <a name="bkmk_support-inventory"></a> Separador inventário

#### <a name="load-or-refresh"></a>Carregar ou atualizar
Centro de suporte carrega ou atualiza a lista de inventário de cliente para a vista atualmente selecionada.

#### <a name="invoke-trigger"></a>Invocar acionador

> [!Note]  
> Para tarefas diferentes do **ciclo de relatório de medição de Software**:  
> - Se solicitar que a tarefa quando outra tarefa de inventário já está em execução, o cliente coloca na fila da nova tarefa para ser executado depois de terminar a tarefa atual e outras tarefas em fila.  
> - Acompanhar o progresso da tarefa na **Inventoryagent**.  

Os seguintes itens neste menu solicitam uma ação de cliente relacionadas com o inventário:  

 - **O ciclo de recolha de dados de deteção (heartbeat)**: Aciona a tarefa de cliente utilizada para recolher informações de deteção de dispositivos  

 - **Ciclo de recolha de ficheiros**: Aciona a tarefa de cliente utilizada para recolher ficheiros locais  

 - **Ciclo de inventário de hardware**: Aciona a tarefa de cliente utilizada para recolher dados de inventário de hardware  

 - **Ciclo de recolha IDMIF**: Aciona a tarefa de cliente utilizada para recolher dados IDMIF  

 - **Ciclo de inventário de software**: Aciona a tarefa de cliente utilizada para recolher dados de inventário de software  

 - **Ciclo de relatório de medição de software**: Aciona a tarefa de cliente utilizada para criar um relatório de medição de software e enviá-lo para o ponto de gestão. Acompanhar o progresso desta tarefa na **Swmtrreportgen**.

 - **Enviar mensagens de estado de não enviadas na fila**: Aciona a tarefa de cliente para esvaziar a fila de mensagens de estado.

 - **Avançadas**  
     - **Ciclo de inventário de hardware (ressincronização completa)**  
     - **Ciclo de inventário de software (ressincronização completa)**  


#### <a name="views"></a>Vistas
Se uma funcionalidade não está ativada, a vista não apresenta todos os dados. 

- **Estado**: Mostrar os conjuntos de dados de inventário de que cliente recolheu  

- **DDR**: Informações sobre os dados de deteção de cliente recolhidos do cliente  

- **HINV**: Informações sobre os dados de inventário de hardware recolhidos do cliente  

- **SINV**: Informações sobre os dados de inventário de software recolhidos do cliente  

- **Recolha de ficheiros**: Informações sobre os ficheiros recolhidos do cliente  

- **IDMIF**: Informações sobre os dados IDMIF e NOIDMIF recolhidos do cliente  

- **Medição**: Informações sobre o dados recolhidos do cliente de medição de software  



### <a name="bkmk_support-troubleshoot"></a> Guia de resolução de problemas

Resolver alguns dos problemas mais comuns com clientes do Configuration Manager:  
- Problemas com o Active Directory  
- Sistema de rede do Windows  
- Configuration Manager   
    - Pontos de gestão  
    - Atribuição de política  
    - Registo  


> [!NOTE]  
> Este separador não está disponível quando se liga a um cliente remoto do Configuration Manager.


#### <a name="start"></a>Iniciar,
Inicia o cliente de resolução de problemas

- **Active Directory**: Publicado de consulta o Active Directory para obter informações de site do Configuration Manager  
- **MPCERTIFICATE**: Obtém os certificados de ponto de gestão  
- **MPLIST**: Obtém uma lista de pontos de gestão  
- **MPKEYINFORMATION**: Obtém informações da chave criptográfica gestão ponto  
- **Funcionamento em rede**: Resolve problemas de rede  
- **Atribuições de política**: Obtém atribuições de políticas  
- **Registo**: Verifica se o cliente está registado com o site  

#### <a name="view-selected-log"></a>Ver registo selecionado
Depois de selecionar uma linha no separador Resolução de problemas, selecione a ação para ver o ficheiro de registo.

#### <a name="keep-previous-results"></a>Manter resultados anteriores
Se o cliente de resolução de problemas e, em seguida, quer tentar novamente a resolução de problemas, escolha esta opção para manter os resultados da sua primeira tentativa. Caso contrário, o Support Center substitui ficheiros de registo de resolução de problemas anteriores.



### <a name="bkmk_support-logs"></a> Separador registos

Esta secção lista os itens no **registos** separador da ferramenta Support Center. 

Este separador é quase idêntico da **Log Viewer** ferramenta. O **Log Viewer** ferramenta não inclui o **configurar o registo do cliente** e **grupos de registos** funcionalidades descritas nesta secção. O [referência do Support Center Log Viewer](#bkmk_log-viewer) seção detalha as outras opções disponíveis neste separador.

#### <a name="configure-client-logging"></a>Configurar registo do cliente

Defina as seguintes opções: 
- **Nível de registo de cliente**: Verbosidade de registo e o tamanho do ficheiro  
- **Contagem de ficheiro máximo**: Permitir que mais de um ficheiro de registo de um determinado tipo  
- **Tamanho máximo do ficheiro**: O tamanho em bytes de qualquer ficheiro de registo antes do cliente cria um novo registo  

> [!NOTE]  
> Se definir esses valores muito baixo, o cliente não poderá iniciar quaisquer informações úteis. Se definir o valor demasiado alto, os registos de cliente podem consumir grandes quantidades de armazenamento.  

#### <a name="log-groups"></a>Grupos de registos

Em vez de selecionar manualmente os ficheiros de registo utilizando o **abrir registos** botão, utilize esta lista de baixo para abrir todos os ficheiros de registo associados com as seguintes áreas de funcionalidade: 
- **Gestão de configuração pretendida**
- **Inventário**
- **Distribuição de Software**
- **Atualizações de Software**
- **Gestão de Aplicações**
- **Política**
- **Registo de clientes**
- **Implementação do Sistema Operativo**


## <a name="bkmk_log-viewer"></a> Referência do Support Center Log Viewer

Esta secção descreve a interface do usuário para o **Support Center Log Viewer** ferramenta. 

- [Menu da janela](#bkmk_log-window)  
- [Separador PáginaL principal](#bkmk_log-home)  

O **Log Viewer** ferramenta é quase idêntica do **registos** separador de **Centro de suporte**. O **Log Viewer** ferramenta não inclui as opções para **configurar o registo do cliente** e **grupos de registos**.


### <a name="bkmk_log-window"></a> Menu da janela

No canto superior esquerdo da janela do Support Center Log Viewer, selecione a seta na caixa de azul para abrir esse menu.

#### <a name="open-logs"></a>Abrir registos
Navegue até à localização dos ficheiros de registo para abrir. 

#### <a name="options"></a>Opções
Na **opções** caixa de diálogo, pode:
- Reduzir o movimento dos elementos da interface do usuário animados  
- Registe-se do Log Viewer, como a aplicação predefinida para ficheiros de registo com as extensões de ficheiro. log e. lo _  
- Repor os avisos. Todas as mensagens de aviso que anteriormente suprimidos novamente apresentadas quando acionadas.  

#### <a name="about"></a>sobre
Mostra informações sobre o Support Center Log Viewer

#### <a name="close"></a>Fechar
Fechar Support Center Log Viewer


### <a name="bkmk_log-home"></a> Separador PáginaL principal

#### <a name="open-logs"></a>Abrir registos 
Centro de suporte solicita que selecione um ou mais ficheiros de registo para abrir.

Selecione o menu pendente na parte inferior a **abrir registos** botão na faixa de opções e selecione uma das seguintes opções adicionais: 
- **Abrir registos na vista atual**: Abre-se os ficheiros de registo selecionado na vista atual  
- **Abrir registos numa nova janela**: Abre-se os ficheiros de registo selecionado numa nova **Log Viewer** janela  

#### <a name="close-and-clear-logs"></a>Fechar e limpar registos
Fecha quaisquer ficheiros de registo abertos. Limpa quaisquer entradas de ficheiro de registo apresentadas da janela. Centro de suporte não são apresentados nestas entradas no futuro.

Selecione na lista pendente na parte inferior a **fechar e limpar registos** botão na faixa de opções e selecione uma das seguintes opções adicionais: 
- **Limpar todas as entradas**: Limpa quaisquer entradas de ficheiro de registo apresentadas da janela. Centro de suporte não são apresentados nestas entradas no futuro.  
- **Fechar todos os registos**: Fecha todos os ficheiros registo abertos  

#### <a name="find"></a>Localizar
Abre o **encontrar** caixa de diálogo. Introduza uma cadeia a procurar. Para evitar correspondências em cadeias curtas em outras cadeias de caracteres, pode optar por corresponder palavras inteiras. Também pode optar por fazer uma correspondência de maiúsculas e minúsculas para a cadeia de caracteres.

#### <a name="find-next"></a>Localizar seguinte
Depois de encontrar uma correspondência para a cadeia de caracteres que está a procurar, esta opção leva-o para a correspondência seguinte.

#### <a name="find-previous"></a>Localizar anterior
Depois de encontrar duas ou mais correspondências para a cadeia que está a procurar, esta opção leva-o para a correspondência anterior.

#### <a name="options"></a>Opções

- **Atualização em direto**: Monitorize um ficheiro de registo atualmente aberto para que as alterações. Esta funcionalidade não funciona em vários arquivos de log estão abertos. Por predefinição, esta opção encontra-se ativada.  

- **Rolagem automática**: Se também tiver escolhido o **atualização em direto** opção, esta opção automaticamente se desloca a vista de registo para mostrar entradas adicionadas recentemente. Esta funcionalidade não funciona em vários arquivos de log estão abertos. Por predefinição, esta opção encontra-se ativada.  

- **Mostrar detalhes**: Quando seleciona uma mensagem de ficheiro de registo, na parte inferior do **registos** separador apresenta os detalhes da mensagem de ficheiro de registo. Por predefinição, esta opção encontra-se ativada.  

- **Filtro Rápido**: Filtre as mensagens de ficheiro de registo em todos os ficheiros de registo abertos para localizar uma cadeia específica. Pode filtrar por texto de registo, nome do componente e ID de thread. Para localizar mensagens de registo semelhantes, faça duplo clique numa mensagem de registo e selecione **filtro Rápido** no texto de registo.  

- **Moldar texto de registo**: Encapsule mensagens longas e com várias linhas para caber numa única coluna. Este comportamento torna mais fácil de ler essas mensagens. Por predefinição, esta opção encontra-se ativada.  

- **Exibição de entrada de registos não processados**: Exibe linhas de registos não processadas.  

- **Filtros avançados**: Abra o **filtros avançados** caixa de diálogo. Para obter mais informações, consulte [os filtros de ficheiro de registo avançados](#bkmk_adv-filters).  

- **Ligações de código de erro**: Códigos de erro no texto de registo são destacados e clicável. Por predefinição, esta opção encontra-se ativada.  

#### <a name="error-lookup"></a>Pesquisa de erros
Introduza um código de erro para pesquisar esse código de erro nos ficheiros de registo atualmente abertos. Utilize os seguintes formatos de código de erro:
 - **número inteiro de 32 bits (assinado)**: Por exemplo, `-2147024891`  
 - **número inteiro de 32 bits (sem sinal)**: Por exemplo, `2147942405`  
 - **hexadecimal de 32 bits**: Por exemplo, `0x80070005`  

#### <a name="decode-certificate"></a>Descodificar certificado
Na **certificado de Decodificação** diálogo caixa, cole o valor do certificado serializado para qualquer certificado no cliente. Encontre este valor no Registro, nos ficheiros de registo ou no WMI. Selecione **processo** para ver detalhes e informações gerais sobre o certificado. Estas informações incluem o seu caminho de certificação. Selecione **exportar** para exportar o certificado como um **. cer** ficheiro.



## <a name="bkmk_adv-filters"></a> Filtros de ficheiro de registo avançados

Os filtros de ficheiro de registo avançados permitem incluir, excluir ou realçar cadeias específicas. Essas cadeias de caracteres podem ocorrer num ficheiro de registo ou grupo de ficheiros de registo ao observar as entradas de ficheiros de registo. Utilizar pesquisas de com carateres universais ao criar um filtro. Quando tiver uma combinação útil de filtros, guarde-as como um *filtrar o conjunto*. 

Os filtros de ficheiro de registo avançados substituem os filtros rápidos. Utilizar ambos em conjunto, mas filtros rápidos apenas são aplicáveis aos dados de registo apresentadas. Filtros avançados determinam os dados inicialmente apresentadas antes de qualquer TI aplica-se quaisquer filtros rápidos.

Na caixa de diálogo filtros avançados, pode criar conjuntos de filtros complexos. Estes filtrar conjuntos de pesquisa para cadeias de caracteres em muitos componentes do ficheiro de registo. Estes componentes incluem mensagens, threads, níveis de registo e componentes. Um conjunto de filtros contém várias instruções de filtros que utilizar para incluir, excluir ou realçar mensagens de ficheiro de registo. Um filtro define uma coluna do ficheiro de registo para procurar dentro de um operador e um valor. O valor pode conter expressões regulares, como o *universais* caráter `*`.


### <a name="add-a-filter"></a>Adicionar um filtro

1. Na **Log Viewer** janela, ou no Centro de suporte **registos** separador, selecione **filtros avançados**.  

2. Na caixa de diálogo filtros avançados, selecione **adicionar**. Em seguida, selecione uma das seguintes opções para tomar decisões sobre as entradas de registo correspondentes ao filtro:  
    - **Incluir**  
    - **Excluir**  
    - **Realçar**  

3. Na **configuração do filtro avançado** caixa de diálogo, escolha uma coluna e um operador:  

    - **Coluna**: Escolha onde pretende pesquisar cadeias correspondentes ao filtro:  

         - **O texto de registo**: Pesquisar no texto de um ficheiro de registo  

         - **Gravidade de registo**: Pesquisa de registos com um nível de gravidade específico. Defina estes níveis de gravidade no **valor** campo.  

         - **Componente**: Procurar por um componente específico por nome  

         - **ID da thread**: Procure mensagens de registo com um ID de thread específico  

         - **Ficheiro de origem**: Procure mensagens de registo que ocorrem no ficheiro de registo específico  

    - **Operador**: Escolha um operador para o seu filtro  

4. Introduza um valor a filtrar no **valor** campo. Se o valor contiver expressões regulares, selecione **ativar a correspondência de expressões regulares**.  


### <a name="manage-filter-sets"></a>Gerir conjuntos de filtros

  - Para editar um filtro, selecione o filtro e, em seguida, selecione **editar**.  

  - Para eliminar um filtro, selecione o filtro e, em seguida, selecione **eliminar**.  

  - Para limpar todos os filtros, selecione **limpar**.  

  - Para guardar o conjunto de filtros atual, selecione **Guardar filtros**. Em seguida, guarde o filtro como um **.filterset** ficheiro.  

  - Para carregar um conjunto de filtros guardado, selecione **carregar filtros**. Em seguida, navegue até um guardado anteriormente **.filterset** ficheiro.  



## <a name="bkmk_viewer"></a> Referência do Support Center Viewer

Esta secção descreve a interface de utilizador (IU) para o Configuration Manager **Support Center Viewer** ferramenta. Os separadores disponíveis variam consoante o conteúdo do pacote de solução de problemas. O [menu de janela](#bkmk_viewer-window) e [separador Base](#bkmk_viewer-home) Mostrar por predefinição.
- [Menu da janela](#bkmk_viewer-window)
- [Separador PáginaL principal](#bkmk_viewer-home)
- [Separador de configuração](#bkmk_viewer-config)
- [Separador registos](#bkmk_viewer-logs)
- [Separador informações de depuração](#bkmk_viewer-debug)
- [Separador WMI](#bkmk_viewer-wmi)
- [Separador registo](#bkmk_viewer-registry)
- [Separador política](#bkmk_viewer-policy)
- [Separador certificados](#bkmk_viewer-certs)
- [Guia de resolução de problemas](#bkmk_viewer-troubleshoot)


### <a name="bkmk_viewer-window"></a> Menu da janela

No canto superior esquerdo da janela do Support Center Viewer, selecione a seta na caixa de azul para abrir esse menu.

#### <a name="open-bundle"></a>Abrir pacote
Navegue até à localização de um pacote de dados criada pelo centro de suporte.

#### <a name="about"></a>sobre
Mostra informações sobre o Support Center Viewer.

#### <a name="options"></a>Opções
Na **opções** caixa de diálogo, pode:
- Reduzir o movimento dos elementos da interface do usuário animados  
- Alterar a localização dos ficheiros temporários    
- Repor os avisos. Todas as mensagens de aviso que anteriormente suprimidos novamente apresentadas quando acionadas.  
- Repor o caminho de ficheiro temporário na sua predefinição, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenterViewer`  


#### <a name="exit"></a>Sair
Sai do Support Center Viewer


### <a name="bkmk_viewer-home"></a> Separador PáginaL principal

#### <a name="open-bundle"></a>Abrir pacote
Navegue até à localização de um pacote de dados criada pelo centro de suporte.

#### <a name="open-log-file"></a>Abrir o ficheiro de registo
Selecione um ou mais ficheiros de registo para abrir.

#### <a name="decode-certificate"></a>Descodificar certificado
Na **certificado de Decodificação** diálogo caixa, cole o valor do certificado serializado para qualquer certificado no cliente. Encontre este valor no Registro, nos ficheiros de registo ou no WMI. Selecione **processo** para ver detalhes e informações gerais sobre o certificado. Estas informações incluem o seu caminho de certificação. Selecione **exportar** para exportar o certificado como um **. cer** ficheiro.


### <a name="bkmk_viewer-config"></a> Separador de configuração

O **configuração** separador da ferramenta Support Center Viewer fornece as seguintes vistas usando dados recuperados de provedores de WMI:

#### <a name="client"></a>Cliente
Esta vista apresenta as mesmas informações apresentadas na **cliente** separador do Support Center.

#### <a name="operating-system"></a>Sistema Operativo
Detalhes de sistema de operativo do cliente. Ele usa o [Win32_OperatingSystem](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-operatingsystem) classe.

#### <a name="computer"></a>Computador
Detalhes para o computador cliente. Ele usa o [Win32_OperatingSystem](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-operatingsystem) classe.

#### <a name="services"></a>Serviços
Detalhes de serviços em execução no computador cliente. Ele usa o [Win32_Service](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-service) classe.

#### <a name="network-adapters"></a>Adaptadores de rede
Detalhes dos adaptadores de rede instalados no computador cliente. Ele usa o [Win32_NetworkAdapterConfiguration](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-networkadapterconfiguration) classe.


### <a name="bkmk_viewer-logs"></a> Separador registos

O **registos** separador mostra uma lista de ficheiros de registo incluídos no pacote. Cada linha neste separador fornece o caminho, o nome e o tamanho do ficheiro de registo. 

#### <a name="open"></a>Abrir
Depois de selecionar um ficheiro de registo, seleciona este botão para abrir o **Log Viewer**. Ele fornece um subconjunto da funcionalidade vista no separador registos do Centro de suporte.

#### <a name="decode-certificate"></a>Descodificar certificado
Na **certificado de Decodificação** diálogo caixa, cole o valor do certificado serializado para qualquer certificado no cliente. Encontre este valor no Registro, nos ficheiros de registo ou no WMI. Selecione **processo** para ver detalhes e informações gerais sobre o certificado. Estas informações incluem o seu caminho de certificação. Selecione **exportar** para exportar o certificado como um **. cer** ficheiro.


### <a name="bkmk_viewer-debug"></a> Separador informações de depuração

Cada linha neste separador fornece detalhes sobre a depuração os ficheiros de informação que estão disponíveis para exportar. Utilize este separador para exportar ficheiros de informação de depuração (. dmp) para análise adicional. Esta análise utiliza uma ferramenta de depuração, como o WinDbg. 

> [!WARNING]  
> Informações do Estado da depuração Maio conter informações confidenciais, incluindo palavras-passe, segredos criptográficos ou dados de utilizador. Apenas recolher informações de depuração sob recomendação do pessoal de Support da Microsoft. Pacotes de dados que contenham informações de depuração devem ser processados cuidadosamente para protegê-los contra acesso não autorizado.  

#### <a name="export"></a>Exportar
Guarde uma cópia do arquivo de despejo de depuração selecionado.


### <a name="bkmk_viewer-wmi"></a> Separador WMI

Este separador mostra o conjunto de dados WMI de cliente do Configuration Manager que inclua o pacote de dados. 

#### <a name="find"></a>Localizar
Abre a caixa de diálogo Localizar, que tem as seguintes funcionalidades:  

- **Encontre o que**: Introduza uma cadeia de caracteres para procurar no conjunto de dados WMI. Ele suporta carateres universais.  

- **Examinar**: Escolha se pretende procurar dentro de um conjunto de dados do WMI para uma correspondência **nome de classe ou instância**, **propriedade**, ou **valor**.  

- **Corresponder só cadeia completa**: Por predefinição, caixa de diálogo Localizar pesquisará cadeias que contêm a cadeia de caracteres para o qual está à procura. Selecione esta caixa de verificação para localizar apenas cadeias que são uma correspondência exata com a cadeia de caracteres que forneceu.  

#### <a name="find-next"></a>Localizar seguinte
Este botão abre a instância seguinte da cadeia fornecida na caixa de diálogo Localizar no conjunto de dados WMI.

#### <a name="decode-certificate"></a>Descodificar certificado
Na **certificado de Decodificação** diálogo caixa, cole o valor do certificado serializado para qualquer certificado no cliente. Encontre este valor no Registro, nos ficheiros de registo ou no WMI. Selecione **processo** para ver detalhes e informações gerais sobre o certificado. Estas informações incluem o seu caminho de certificação. Selecione **exportar** para exportar o certificado como um **. cer** ficheiro.


### <a name="bkmk_viewer-registry"></a> Separador registo

Utilize o **Registro** separador para ver os dados de registo incluídos no pacote de dados e exportar esses dados para análise adicional.

#### <a name="export"></a>Exportar
Guarde uma cópia da chave do Registro e subchaves que selecionou como um ficheiro de registo (. reg).

#### <a name="find"></a>Localizar
Abre a caixa de diálogo Localizar, que tem as seguintes funcionalidades:  

- **Encontre o que**: Introduza uma cadeia de caracteres para procurar no conjunto de dados WMI. Ele suporta carateres universais.  

- **Examinar**: Escolha se pretende procurar dentro de um conjunto de dados do WMI para uma correspondência **nome de classe ou instância**, **propriedade**, ou **valor**.  

- **Corresponder só cadeia completa**: Por predefinição, caixa de diálogo Localizar pesquisará cadeias que contêm a cadeia de caracteres para o qual está à procura. Selecione esta caixa de verificação para localizar apenas cadeias que são uma correspondência exata com a cadeia de caracteres que forneceu.  

#### <a name="find-next"></a>Localizar seguinte
Este botão abre a instância seguinte da cadeia fornecida na caixa de diálogo Localizar no conjunto de dados WMI.

#### <a name="decode-certificate"></a>Descodificar certificado
Na **certificado de Decodificação** diálogo caixa, cole o valor do certificado serializado para qualquer certificado no cliente. Encontre este valor no Registro, nos ficheiros de registo ou no WMI. Selecione **processo** para ver detalhes e informações gerais sobre o certificado. Estas informações incluem o seu caminho de certificação. Selecione **exportar** para exportar o certificado como um **. cer** ficheiro.


### <a name="bkmk_viewer-policy"></a> Separador política

O **política** separador é utilizado para ver os dados de política incluídos no pacote de dados. 

#### <a name="find"></a>Localizar
Abre a caixa de diálogo Localizar, que tem as seguintes funcionalidades:  

- **Encontre o que**: Introduza uma cadeia de caracteres para procurar no conjunto de dados WMI. Ele suporta carateres universais.  

- **Examinar**: Escolha se pretende procurar dentro de um conjunto de dados do WMI para uma correspondência **nome de classe ou instância**, **propriedade**, ou **valor**.  

- **Corresponder só cadeia completa**: Por predefinição, caixa de diálogo Localizar pesquisará cadeias que contêm a cadeia de caracteres para o qual está à procura. Selecione esta caixa de verificação para localizar apenas cadeias que são uma correspondência exata com a cadeia de caracteres que forneceu.  

#### <a name="find-next"></a>Localizar seguinte
Este botão abre a instância seguinte da cadeia fornecida na caixa de diálogo Localizar no conjunto de dados WMI.

#### <a name="decode-certificate"></a>Descodificar certificado
Na **certificado de Decodificação** diálogo caixa, cole o valor do certificado serializado para qualquer certificado no cliente. Encontre este valor no Registro, nos ficheiros de registo ou no WMI. Selecione **processo** para ver detalhes e informações gerais sobre o certificado. Estas informações incluem o seu caminho de certificação. Selecione **exportar** para exportar o certificado como um **. cer** ficheiro.


### <a name="bkmk_viewer-certs"></a> Separador certificados

O **certificados** separador é utilizado para ver os certificados incluídos no pacote de dados e exportá-los.

#### <a name="view-certificate"></a>Ver certificado
Mostra informações sobre um certificado selecionado.

#### <a name="export"></a>Exportar
É aberto um **guardar como** caixa de diálogo para guardar uma cópia do certificado que selecionou.


### <a name="bkmk_viewer-troubleshoot"></a> Guia de resolução de problemas

Utilize o **resolução de problemas** separador para ver os arquivos de log criados usando a guia de resolução de problemas de centro de suporte.

#### <a name="view-log"></a>Ver registo
Depois de selecionar uma linha a **resolução de problemas** separador, selecione esta opção para ver o ficheiro de registo com o Log Viewer.

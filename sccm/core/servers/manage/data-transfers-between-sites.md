---
title: Transferências de dados
titleSuffix: Configuration Manager
description: Saiba como o Configuration Manager move dados entre sites e como pode gerir a transferência dos dados na sua rede.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 39ae7c931b2d69199dc2c24cbb1bf9ae804a04b4
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123193"
---
# <a name="data-transfers-between-sites-in-system-center-configuration-manager"></a>Transferência de dados entre sites no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O System Center Configuration Manager utiliza **replicação de ficheiros** e **replicação de base de dados** para transferir tipos diferentes de informações entre sites. Saiba mais sobre como o Configuration Manager move dados entre sites e como pode gerir a transferência de dados na sua rede.  


## <a name="bkmk_fileroute"></a> File-based replication  
O Configuration Manager utiliza a replicação de ficheiros para transferir dados baseados em ficheiros entre sites na sua hierarquia. Estes dados incluem aplicações e pacotes que pretende implementar em pontos de distribuição em sites subordinados e os registos de dados de deteção não processados que são transferidos para sites principais e, em seguida, processados.  

Comunicação baseada em ficheiros entre sites utiliza o **Server Message Block** protocolo (SMB) na porta de TCP/IP 445. Pode especificar o modo de impulso e de limitação de largura de banda para controlar a quantidade de dados transferidos através da rede e pode utilizar agendas para controlar quando enviar dados através da rede.  

### <a name="bkmk_routes"></a> Rotas de replicação de ficheiros  
As informações seguintes podem ajudá-lo a configurar e utilizar rotas de replicação de ficheiros.  

#### <a name="file-replication-route"></a>Rota de replicação de ficheiros

Cada rota de replicação de ficheiros identifica um site de destino para que os dados de ficheiros podem ser transferidos. Cada site suporta uma rota de replicação de ficheiros para um site de destino específico.  

Pode alterar as seguintes definições para rotas de replicação de ficheiros:  

-  **Conta de replicação de ficheiros**. Esta conta liga-se ao site de destino e escreve dados desse site **SMS_Site** partilhar. Os dados escritos nesta partilha são processados pelo site recetor. Por predefinição, quando um site é adicionado à hierarquia, o Configuration Manager atribui a conta de computador do servidor de site do novo site como conta de replicação de ficheiros. Esta conta é então adicionada ao site de destino **SMS_SiteToSiteConnection_&lt;Sitecode\>**  grupo, um grupo local no computador que concede acesso à partilha SMS_Site. Pode alterar esta conta para uma conta de utilizador do Windows. Se alterar a conta, certifique-se de que adiciona a nova conta do site de destino **SMS_SiteToSiteConnection_&lt;Sitecode\>**  grupo.  

    > [!NOTE]  
    >  Os sites secundários utilizam sempre a conta de computador do servidor do site secundário como a **Conta de Replicação de Ficheiros**.  

-  **Agenda**. Pode definir a agenda para cada rota de replicação de ficheiros restringir o tipo de dados e a hora de dados de transferência para o site de destino.  
-  **Limites de velocidade**. Pode especificar os limites de velocidade para cada rota de replicação de ficheiros controlar a largura de banda de rede que é utilizada quando o site transfere dados para o site de destino:  

    -  Utilize o **Modo de impulsos** para especificar o tamanho dos blocos de dados que são enviados para o site de destino. Também pode especificar um atraso de tempo entre o envio de cada bloco de dados. Utilize esta opção quando tiver de enviar dados através de uma ligação de rede muito pouca largura de banda para o site de destino. Por exemplo, poderá ter limitações para enviar 1 KB de dados a cada cinco segundos, mas não 1 KB a cada três segundos, independentemente da velocidade da ligação ou da respetiva utilização num determinado momento.
    -  Utilize **Limitado a velocidades máximas de transferência por hora** para que um site envie dados para um site de destino utilizando apenas a percentagem de tempo especificada. Quando utilizar esta opção, o Configuration Manager não identifica a largura de banda disponível da rede, mas em vez disso, divide o tempo que pode enviar dados em frações de tempo. Em seguida, os dados são enviados num curto bloco de tempo, o que é seguido de blocos de dados não são enviados do tempo. Por exemplo, se a velocidade máxima for definida como **50%**, Configuration Manager transmite dados durante um período de tempo seguido por um período de tempo quando não são enviados dados igual. A quantidade real de dados ou o tamanho do bloco de dados, não é gerido. Em vez disso, apenas é gerida a quantidade de tempo durante a qual são enviados dados.  

        > [!CAUTION]  
        > Por predefinição, um site pode utilizar até três **envios simultâneos** para transferir dados para um site de destino. Quando são ativados limites de velocidade numa rota de replicação de dados, o número de **envios simultâneos** para enviar dados para esse site é limitado a um. Isto aplica-se mesmo quando o **Limite de largura de banda disponível (%)** é definido como **100%**. Por exemplo, se utilizar as predefinições para o remetente, isso reduz a taxa de transferência para o site de destino para ser um terço da capacidade predefinida.  

-  É possível configurar uma rota de replicação de ficheiros entre dois sites secundários para encaminhar conteúdo baseado em ficheiros entre esses sites.  

Para gerir um rota de replicação de ficheiros, o **administração** área de trabalho, expanda o **configuração da hierarquia** nó e, em seguida, selecione **replicação de ficheiros**.  

#### <a name="sender"></a>Remetente

Cada site tem um remetente. O remetente gere a ligação de rede de um site para um site de destino e pode estabelecer ligações a múltiplos sites ao mesmo tempo. Para ligar a um site, o remetente utiliza a rota de replicação de ficheiros para o site para identificar a conta utilizada para estabelecer a ligação de rede. O remetente também utiliza esta conta para escrever dados na partilha SMS_Site do site de destino.  

Por predefinição, o remetente escreve dados num site de destino através de múltiplos **envios simultâneos**, normalmente referidos como threads. Cada envio simultâneo, ou thread, pode transferir um objeto baseado em ficheiros diferente para o site de destino. Por predefinição, quando o remetente começa a enviar um objeto, continua a escrever blocos de dados nesse objeto até que todo o objeto seja enviado. Depois de terem sido enviados todos os dados de um objeto, pode começar a ser enviado um novo objeto nesse thread.  

Pode alterar as seguintes definições para um remetente:  

-  **Envios simultâneos**. Por predefinição, cada site utiliza cinco envios simultâneos, estando três disponíveis para utilização quando são enviados dados para qualquer site de destino. Quando aumenta este número, pode aumentar o débito de dados entre sites, porque o Configuration Manager pode Transfira mais ficheiros ao mesmo tempo. Aumentar este número também aumenta a necessidade de largura de banda de rede entre sites.  

-  **Definições de repetição**. Por predefinição, cada site tentará novamente uma ligação problemática duas vezes, com um atraso de um minuto entre tentativas de ligação. Pode modificar o número de tentativas de ligação efetuada pelo site e durante quanto tempo a aguardar entre tentativas.  

Para gerir o remetente de um site, no **Administration** área de trabalho, expanda o **configuração do Site** nó, selecione o **Sites** nó e, em seguida, selecione  **Propriedades** para o site que pretende gerir. Selecione o **remetente** separador para alterar as definições do remetente.  

## <a name="bkmk_dbrep"></a> Database replication  
Replicação de base de dados do Configuration Manager utiliza o SQL Server para transferir dados e intercalar as alterações efetuadas numa base de dados do site com as informações armazenadas na base de dados de outros sites na hierarquia. Tenha em atenção o seguinte sobre a replicação de base de dados:

-  Todos os sites partilhem as mesmas informações.  
-  Quando instala um site numa hierarquia, replicação de base de dados automaticamente é estabelecida entre o novo local e o respetivo site principal designado.  
-  Quando concluir a instalação do site, replicação de base de dados é iniciada automaticamente.  

Quando adiciona um novo site para uma hierarquia, o Configuration Manager cria uma base de dados genérica no novo site. Em seguida, o site principal cria um instantâneo dos dados relevantes na respetiva base de dados e, em seguida, transfere o instantâneo para o novo site através da replicação baseada em ficheiros. O novo site utiliza, em seguida, o programa de cópia do SQL Server em massa (BCP) para carregar as informações na respetiva cópia local da base de dados do Configuration Manager. Após o carregamento do instantâneo, cada site efetua a replicação de base de dados com outro site.  

Para replicar dados entre sites, o Configuration Manager utiliza o seu próprio serviço de replicação de base de dados. O serviço de replicação de base de dados utiliza o registo para monitorizar a base de dados do local site para que as alterações de alterações do SQL Server e, em seguida, replica as alterações para outros sites utilizando o SQL Server Service Broker (SSB). Por predefinição, este processo utiliza a porta de TCP/IP 4022.  

O Configuration Manager agrupa dados que replicam através da replicação de base de dados em grupos de replicação diferentes. Tenha em atenção o seguinte sobre grupos de replicação:

-  Cada grupo de replicação tem uma agenda de replicação separada e fixa que determina a frequência com que as alterações dos dados no grupo são replicadas para outros sites.  

     Por exemplo, uma alteração para uma configuração de administração baseada em funções replica rapidamente para outros sites para se certificar de que estas alterações são impostas assim que possível. Enquanto isso, uma alteração de configuração de prioridade mais baixa, como um pedido para instalar um novo site secundário, replica com menos urgência. Pode demorar vários minutos para um novo pedido de site chegar ao site primário de destino.  

-   Pode modificar as seguintes definições para a replicação de base de dados:  

    -  **Ligações de replicação de base de dados**. Controlar quando tráfego específico atravessa a rede.  
    -  **Vistas distribuídas**. Alterar as definições para ligações de replicação através do qual pedidos efetuados num site de administração central para dados de site selecionados podem acessar os dados de site diretamente a partir da base de dados num site primário subordinado.  
    -  **Agendas**. Especifique quando é utilizada uma ligação de replicação e, quando são replicados diferentes tipos de dados do site.  
    -  **Resumo**. Alterar as definições de resumo sobre o tráfego de rede que atravessa as ligações de replicação de dados. Resumo ocorre a cada 15 minutos, por predefinição e é utilizado em relatórios para a replicação de base de dados.  
    -  **Limiares de replicação de base de dados**. Definem quando as ligações são comunicadas como degradadas ou falhadas. Também pode configurar quando o Configuration Manager gera alertas sobre ligações de replicação que têm um Estado degradado ou falhado.  

O Configuration Manager classifica os dados que replica através da replicação de base de dados como um **dados globais** ou **dados do site**. Quando ocorre a replicação da base de dados, as alterações aos dados globais e aos dados de site são transferidas através da ligação da replicação de base de dados. Dados globais podem replicar para um site principal ou subordinado. Dados do site são replicados apenas para um site principal. Um terceiro tipo de dados, dados locais, não é replicado para outros sites. Dados locais são informações que não são necessárias para outros sites. Tenha em atenção o seguinte sobre tipos de dados:  

-  **Dados globais**. Dados globais referem-se a objetos criados pelo administrador que são replicados para todos os sites na hierarquia, apesar dos sites secundários receberem apenas um subconjunto de dados globais, como dados de global proxy. Dados globais incluem implementações de software, atualizações de software, definições de coleção e âmbitos de segurança da administração baseada em funções. Os administradores podem criar dados globais em sites de administração central e sites primários.  
-  **Dados do site**. Dados do site refere-se a informações operacionais que sites primários do Configuration Manager e os clientes que criar o relatório para sites primários. Os dados do site replicam para o site de administração central, mas não para outros sites primários. Dados do site incluem dados de inventário de hardware, mensagens de estado, alertas e os resultados de coleções baseadas em consulta. Dados do site só são visualizáveis no site de administração central e no site primário de origem dos dados. Os dados do site apenas podem ser modificados no site primário onde foram criados.  

     Todos os dados do site são replicados para o site de administração central. O site de administração central executa a administração e relatórios para a hierarquia de sites inteiro.  

As secções seguintes detalham as definições que podem ser alteradas para gerir a replicação de base de dados.  

### <a name="bkmk_Dblinks"></a> Ligações de replicação de base de dados  
Quando instala um novo site numa hierarquia, o Configuration Manager cria automaticamente uma ligação de replicação de base de dados entre o site principal e o novo site. É criada uma ligação de única para ligar os dois sites.  

Pode alterar as definições para cada ligação de replicação de base de dados para ajudar a controlar a transferência de dados através da ligação de replicação. Cada ligação de replicação suporta configurações separadas. Os controlos para ligações de replicação de base de dados incluem o seguinte:  

-  Pare a replicação dos dados de site selecionados de um site primário para o site de administração central, para que o site de administração central pode aceder a estes dados diretamente do banco de dados do site primário.  
-  Agende os dados de site selecionados para transferir a partir de um site primário subordinado para o site de administração central.
-  Defina as definições que determinam quando uma ligação de replicação de base de dados tem um Estado degradado ou falhado.
-  Especifique quando aumentar alertas para uma ligação de replicação falhou.
-  Especifique a frequência com que o Configuration Manager resume os dados sobre o tráfego de replicação que utiliza a ligação de replicação. Estes dados são utilizados em relatórios.

Configurar uma ligação de replicação de base de dados, na consola do Configuration Manager, o **replicação de base de dados** nó, editar as propriedades para a ligação. Este nó aparece no **monitorização** área de trabalho e, no **administração** área de trabalho, no **configuração da hierarquia** nó. Pode editar uma ligação de replicação a partir do site principal ou do site subordinado da ligação de replicação.  

> [!TIP]  
> Pode editar ligações de replicação de base de dados a partir do nó **Replicação de Base de Dados** em qualquer uma das áreas de trabalho. No entanto, quando utiliza a **replicação de base de dados** nó a **monitorização** área de trabalho, também pode ver o estado de replicação de base de dados para ligações de replicação e aceder o analisador de ligações de replicação ferramenta para ajudar a investigar problemas com a replicação de base de dados.  

Para obter informações sobre como configurar ligações de replicação, veja [Controlos de Replicação de Base de Dados de Site](#BKMK_DBRepControls). Para obter mais informações sobre como monitorizar a replicação, consulte [como monitorizar o estado de replicação e ligações de replicação de base de dados](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) no [monitorizar a infraestrutura de hierarquia e replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) tópico.  

Utilize as informações nas secções seguintes para ajudar a planear para ligações de replicação de base de dados.  

### <a name="bkmk_distviews"></a> Vistas distribuídas  
Através de vistas distribuídas, pedidos efetuados num site de administração central para selecionar acesso a dados do site esses dados de site diretamente a partir da base de dados num site primário subordinado. O acesso direto substitui a necessidade de replicar esses dados de site do site primário para o site de administração central. Uma vez que cada ligação de replicação é independente de outras ligações de replicação, pode utilizar as vistas distribuídas de apenas as ligações de replicação que escolher. Não é possível utilizar as vistas distribuídas entre um site primário e um site secundário.  

As vistas distribuídas podem fornecer as seguintes vantagens:  

-  Reduzir a carga de CPU para processar alterações de base de dados no site de administração central e sites primários
-  Reduzir a quantidade de dados transferidos através da rede para o site de administração central
-  Melhorar o desempenho do SQL server que aloja a base de dados do site de administração central
-  Reduzir o espaço em disco utilizado pela base de dados no site de administração central

Considere utilizar as vistas distribuídas quando um site primário é próximos ao site de administração central na rede e os dois sites estão sempre ativos e sempre ligado. Isto acontece porque as vistas distribuídas substituem a replicação dos dados selecionados entre os sites com ligações diretas entre os SQL servers em cada site. Uma conexão direta é feita sempre que é efetuado um pedido para estes dados no site de administração central. Normalmente, pedidos de dados permitidos para as vistas distribuídas são efetuados quando executa relatórios ou consultas, quando Exibe informações no Explorador de recursos e avaliação da coleção em coleções que incluem regras baseadas em dados do site.  

Por predefinição, as vistas distribuídas estão desativadas para cada ligação de replicação. Quando ativar as vistas distribuídas para uma ligação de replicação, selecione os dados do site que não irão replicar para o site de administração central através dessa ligação. O site de administração central acede a estes dados diretamente a partir de base de dados do site primário subordinado que partilha a ligação. Pode configurar os seguintes tipos de dados de site para vistas distribuídas:  

-  Dados de inventário de hardware a partir de clientes
-  Dados de inventário de software e medição de clientes
-  Mensagens de estado de clientes, do site primário e de todos os sites secundários

Operacionalmente, as vistas distribuídas são invisíveis a um utilizador administrativo que visualiza dados na consola do Configuration Manager ou nos relatórios. Quando é efetuado um pedido de dados que é permitido para vistas distribuídas, o SQL server que aloja a base de dados para o site de administração central diretamente acede ao SQL server do site primário subordinado para obter as informações. Por exemplo, utilize uma consola do Configuration Manager no site de administração central para pedir informações sobre o inventário de hardware a partir de dois sites e apenas um site tem inventário de hardware ativado para uma vista distribuída. As informações de inventário para clientes a partir do site que não está configurado para vistas distribuídas são obtidas da base de dados no site de administração central. As informações de inventário para clientes do site que está configurado para vistas distribuídas são acedidas a partir da base de dados do site primário subordinado. Esta informação é apresentada na consola do Configuration Manager ou num relatório sem identificar a origem.  

Desde que uma ligação de replicação tem um tipo de dados permitidos para vistas distribuídas, o site primário subordinado não replica os dados para o site de administração central. Assim que desativar as vistas distribuídas para um tipo de dados, o filho primário site retoma a replicação dos dados para o site de administração central como parte da replicação de dados normais. No entanto, antes destes dados ficarem disponíveis no site de administração central, os grupos de replicação que têm este tipo de dados tem de reinicializar entre o site primário e o site de administração central. Da mesma forma, depois de desinstalar um site primário que possui as vistas distribuídas ativadas, o site de administração central tem de concluir reinicialização dos respetivos dados para poder aceder a dados que estavam ativados para vistas distribuídas no site de administração central.  

> [!IMPORTANT]  
> Quando utiliza vistas distribuídas em qualquer ligação de replicação na hierarquia do site, tem de desativar as vistas distribuídas para todas as ligações de replicação antes de desinstalar qualquer site primário. Para obter mais informações, veja [Desinstalar um site primário configurado com vistas distribuídas](../../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#BKMK_UninstallPrimaryDistViews).  

#### <a name="prerequisites-and-limitations-for-distributed-views"></a>Pré-requisitos e limitações das vistas distribuídas  

-  Pode utilizar as vistas distribuídas apenas em ligações de replicação entre um site de administração central e um site primário.
- O site de administração central tem de utilizar uma edição Enterprise do SQL Server. O site primário não tem este requisito.
-  O site de administração central pode ter apenas uma instância do fornecedor de SMS instalado e essa instância tem de estar instalada no servidor de base de dados do site. Isto é necessário para suportar a autenticação Kerberos necessária para que o SQL server no site de administração central pode aceder ao SQL server no site primário subordinado. Não existem limites para o fornecedor de SMS no site primário subordinado.
-  O site de administração central só pode ter um ponto do SQL Server Reporting Services instalado e este tem de estar localizado no servidor da base de dados do site. Isto é necessário para suportar a autenticação Kerberos necessária para ativar o SQL server no site de administração central para aceder ao SQL server no site primário subordinado.
-  A base de dados do site não pode estar alojada num cluster do SQL Server.
-  A base de dados do site não pode ser alojada num grupo de disponibilidade Always On do SQL Server.
-  A conta de computador do servidor da base de dados do site de administração central requer permissões de leitura para a base de dados do site primário.

> [!IMPORTANT]  
>  As vistas distribuídas e agendas de replicação dos dados são configurações mutuamente exclusivas para uma ligação de replicação de base de dados.  

### <a name="BKMK_schedules"></a> Agendar transferências de dados de site em ligações de replicação de base de dados  
Para ajudar a controlar a largura de banda de rede que é utilizada para replicar dados de site de um site primário subordinado para o respetivo site de administração central, pode agendar quando é utilizada uma ligação de replicação e especificar quando são replicados diferentes tipos de dados. Pode controlar quando as mensagens de estado, os dados de inventário e de medição são replicados pelo site primário. As ligações de replicação de base de dados de sites secundários não suportam agendas para dados de sites. Não é possível agendar a transferência de dados globais.  

Quando configura uma agenda de ligação de replicação de base de dados, pode restringir a transferência de dados de site selecionados do site primário para o site de administração central e pode configurar diferentes horas para replicar diferentes tipos de dados de site.  

> [!IMPORTANT]  
> As vistas distribuídas e agendas de replicação dos dados são configurações mutuamente exclusivas para uma ligação de replicação de base de dados.  

### <a name="BKMK_SummarizeDBReplication"></a> Resumo do tráfego de replicação de base de dados  
Cada site resume periodicamente os dados sobre o tráfego de rede que atravessa as ligações de replicação de base de dados para o site. Dados resumidos são utilizados em relatórios para a replicação de base de dados. Ambos os sites numa ligação de replicação resumem o tráfego de rede que atravessa a ligação de replicação. O resumo de dados é efetuado pelo SQL Server que aloja a base de dados do site. Depois de dados são resumidos, as informações são replicadas para outros sites como dados globais.  

Por predefinição, o resumo ocorre a cada 15 minutos. Para modificar a frequência do resumo para o tráfego de rede, nas propriedades de ligação de replicação de base de dados, editar a **intervalo de resumo**. A frequência do resumo afeta as informações visualizadas em relatórios sobre a replicação de base de dados. Pode escolher um intervalo de entre 5 minutos e 60 minutos. Quando aumenta a frequência do resumo, aumenta a carga de processamento no SQL server em cada site na ligação de replicação.  

### <a name="BKMK_DBRepThresholds"></a> Limiares de replicação de base de dados  
Os limiares de replicação de base de dados definem quando o estado de uma ligação de replicação de base de dados é comunicado como degradado ou falhado. Por predefinição, uma ligação está definida para o estado degradado quando qualquer grupo de replicação de uma falha ao concluir a replicação para um período de 12 tentativas consecutivas. A ligação ser definida para o status de falha quando qualquer grupo de replicação não consegue replicar ocorrem consecutivamente 24 tentativas.  

Pode especificar valores personalizados a otimizar quando o Configuration Manager comunica uma ligação de replicação como degradada ou falhada. Adjusting quando os relatórios do Configuration Manager, cada Estado de ligações de replicação de base de dados pode ajudá-lo com precisão monitorizar o estado de funcionamento da replicação de base de dados em suas ligações de replicação de base de dados.  

Como é possível que um ou alguns grupos de replicação a falhar replicar, enquanto outros grupos de replicação continuam a replicar com êxito, planeie uma revisão do Estado de replicação de uma ligação de replicação quando comunica um Estado degradado pela primeira vez. Se ocorrerem atrasos recorrentes em grupos de replicação específicos e estes atrasos não apresentarem um problema ou sempre que a ligação de rede entre os sites tiver pouca largura de banda disponível, considere modificar os valores de tentativa do estado degradado ou falhado da ligação. Quando aumenta o número de tentativas antes da ligação está definida como degradado ou falhado, pode eliminar os avisos falsos para problemas conhecidos e controlar com mais precisão o estado da ligação.  

Além disso, considere o intervalo de sincronização de replicação para cada grupo de replicação compreender a frequência com que ocorre a replicação desse grupo. Para ver o **intervalo de sincronização** dos grupos de replicação, no **monitorização** área de trabalho, no **replicação de base de dados** nó, selecione o  **Detalhes da replicação** separador de uma ligação de replicação.  

Para obter mais informações sobre como monitorizar a replicação de base de dados, incluindo como ver o estado de replicação, consulte [como monitorizar o estado de replicação e ligações de replicação de base de dados](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) no [monitorizar hierarquia e infraestrutura de replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) tópico.  

Para obter informações sobre como configurar limiares de replicação de base de dados, consulte [controlos de replicação de base de dados do Site](#BKMK_DBRepControls).  

## <a name="BKMK_DBRepControls"></a> Controlos de replicação de base de dados do site  
Pode alterar as definições para cada base de dados do site para ajudar a controlar a largura de banda de rede utilizada para a replicação de base de dados. As definições são aplicadas apenas a base de dados do site em que configura as definições. As definições são sempre utilizadas quando o site replica dados através da replicação de base de dados para outro site.  

Seguem-se os controlos de replicação que pode modificar para cada base de dados do site:  

-  Altere a porta do SSB.  
-  Configure o período de tempo de espera antes de falhas de replicação acionam o site reinicialize a respetiva cópia da base de dados do site.  
-  Configure uma base de dados de sites para comprimir os dados que este replica por replicação da base de dados. Os dados são comprimidos apenas para transferência entre sites e não para armazenamento na base de dados de sites de qualquer um dos sites.  

Para alterar as definições para os controlos de replicação para uma base de dados do site, na consola do Configuration Manager, no **replicação de base de dados** nó, edite as propriedades da base de dados do site. Este nó aparece por baixo do nó **Configuração da Hierarquia** , na área de trabalho **Administração** , e também aparece na área de trabalho **Monitorização**. Para editar as propriedades da base de dados do site, selecione a ligação de replicação entre os sites e, em seguida, abra **propriedades de base de dados principal** ou **propriedades de base de dados subordinada**.  

> [!TIP]  
> Pode configurar os controlos de replicação de base de dados no nó **Replicação de Base de Dados** em ambas as áreas de trabalho. No entanto, quando utiliza a **replicação de base de dados** nó a **monitorização** área de trabalho, também pode ver o estado de replicação de base de dados de uma ligação de replicação e aceder o analisador de ligações de replicação ferramenta para ajudar a investigar problemas com a replicação.  

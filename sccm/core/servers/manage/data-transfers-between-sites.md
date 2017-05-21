---
title: "As transferências de dados | Documentos do Microsoft"
description: "Saiba como o Configuration Manager move os dados entre sites e como pode gerir a transferência dos dados através da rede."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
caps.latest.revision: 12
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: bfe77a45b5f781611c343e06d1289add7abd2dfb
ms.openlocfilehash: bf0fdc8d4b4a72760b2cfb91231378a17df01594
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="data-transfers-between-sites-in-system-center-configuration-manager"></a>Transferência de dados entre sites no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager utiliza **replicação baseada em ficheiros** e **replicação de base de dados** para transferir tipos diferentes de informações entre sites. Saiba mais sobre como o Configuration Manager move os dados entre sites e como pode gerir a transferência de dados através da rede.  


## <a name="bkmk_fileroute"></a> File-based replication  
O Configuration Manager utiliza a replicação baseada em ficheiros para transferir dados baseados em ficheiros entre sites na hierarquia. Estes dados incluem as aplicações e pacotes que pretende implementar em pontos de distribuição em sites subordinados e registos de dados de deteção não processados que são transferidos para sites principais e, em seguida, processados.  

Comunicação baseada em ficheiros entre sites utiliza o **bloco de mensagem de servidor** protocolo (SMB) na porta de TCP/IP 445. Pode especificar o modo de impulso e de limitação de largura de banda para controlar a quantidade de dados transferidos através da rede e pode utilizar as agendas para controlar o momento do envio de dados através da rede.  

### <a name="bkmk_routes"></a> Rotas de replicação de ficheiros  
As seguintes informações podem ajudar a configurar e utilizar rotas de replicação.  

#### <a name="file-replication-route"></a>Rota de replicação

Cada rota de replicação de ficheiros identifica um site de destino para os quais podem ser transferidos dados baseados em ficheiros. Cada site suporta uma rota de replicação a um site de destino específico.  

Pode alterar as seguintes definições para rotas de replicação:  

-  **Conta de replicação de ficheiros**. Esta conta estabelece ligação ao site de destino e escreve dados desse site **SMS_Site** partilhar. Os dados escritos nesta partilha são processados pelo site recetor. Por predefinição, quando um site é adicionado à hierarquia, o Configuration Manager atribui a conta de computador do novo site servidor do site como essa conta de replicação de ficheiros de sites. Esta conta é então adicionada para o site de destino **sms_sitetositeconnection _&lt;Sitecode\>**  grupo, um grupo local no computador que concede acesso à partilha SMS_Site. Pode alterar esta conta para uma conta de utilizador do Windows. Se alterar a conta, certifique-se de que adiciona a nova conta para o site de destino **sms_sitetositeconnection _&lt;Sitecode\>**  grupo.  

    > [!NOTE]  
    >  Os sites secundários utilizam sempre a conta de computador do servidor do site secundário como a **Conta de Replicação de Ficheiros**.  

-  **Agenda**. Pode definir a agenda para cada rota de replicação de ficheiros restringir o tipo de dados e a hora quando podem ser transferidos dados para o site de destino.  
-  **Limites de velocidade**. Pode especificar os limites de velocidade para cada rota de replicação de ficheiros controlar a largura de banda de rede que é utilizada quando o site transfere dados para o site de destino:  

    -  Utilize o **Modo de impulsos** para especificar o tamanho dos blocos de dados que são enviados para o site de destino. Também pode especificar um atraso de tempo entre o envio de cada bloco de dados. Utilize esta opção quando tiver de enviar dados através de uma ligação de rede de muito baixa largura de banda para o site de destino. Por exemplo, poderá ter limitações para enviar 1 KB de dados a cada cinco segundos, mas não 1 KB a cada três segundos, independentemente da velocidade da ligação ou da respetiva utilização num determinado momento.
    -  Utilize **Limitado a velocidades máximas de transferência por hora** para que um site envie dados para um site de destino utilizando apenas a percentagem de tempo especificada. Quando utilizar esta opção, o Configuration Manager não identifica a largura de banda disponível da rede, mas em vez disso, divide o tempo que pode enviar dados em frações de tempo. Em seguida, os dados são enviados num curto bloco de tempo, o que é seguido de blocos de tempo quando não são enviados dados. Por exemplo, se a velocidade máxima for definida **50%**, Configuration Manager transmite dados durante um período de tempo seguido por um período de tempo quando são enviados sem dados igual. A quantidade real de dados ou o tamanho do bloco de dados, não é gerido. Em vez disso, apenas é gerida a quantidade de tempo durante a qual são enviados dados.  

        > [!CAUTION]  
        > Por predefinição, um site pode utilizar até três **envios simultâneos** para transferir dados para um site de destino. Quando são ativados limites de velocidade numa rota de replicação de dados, o número de **envios simultâneos** para enviar dados para esse site é limitado a um. Isto aplica-se mesmo quando o **Limite de largura de banda disponível (%)** é definido como **100%**. Por exemplo, se utilizar as predefinições para o remetente, isto reduz a velocidade de transferência para o site de destino para um terço-da capacidade predefinida.  

-  É possível configurar uma rota de replicação de ficheiros entre dois sites secundários para encaminhar conteúdo baseado em ficheiros entre esses sites.  

Para gerir uma rota de replicação de ficheiros, o **administração** área de trabalho, expanda o **configuração da hierarquia** nó e, em seguida, selecione **replicação de ficheiros**.  

#### <a name="sender"></a>Remetente

Cada site tem um remetente. O remetente gere a ligação de rede de um site para um site de destino e pode estabelecer ligações a múltiplos sites ao mesmo tempo. Para ligar a um site, o remetente utiliza a rota de replicação de ficheiros para o site para identificar a conta utilizada para estabelecer a ligação de rede. O remetente também utiliza esta conta para escrever dados na partilha SMS_Site do site de destino.  

Por predefinição, o remetente escreve dados num site de destino através de múltiplos **envios simultâneos**, normalmente referidos como threads. Cada envio simultâneo, ou thread, pode transferir um objeto baseado em ficheiros diferente para o site de destino. Por predefinição, quando o remetente começa a enviar um objeto, continua a escrever blocos de dados nesse objeto até que todo o objeto seja enviado. Depois de terem sido enviados todos os dados de um objeto, pode começar a ser enviado um novo objeto nesse thread.  

Pode alterar as seguintes definições para um remetente:  

-  **Limite de envios simultâneos**. Por predefinição, cada site utiliza cinco envios simultâneos, estando três disponíveis para utilização quando são enviados dados para qualquer site de destino. Quando aumenta este número, pode aumentar o débito de dados entre sites uma vez que o Configuration Manager pode Transfira mais ficheiros ao mesmo tempo. Aumentar este número também aumenta a necessidade de largura de banda de rede entre sites.  

-  **Definições de repetição**. Por predefinição, cada site tentará novamente de uma ligação problemática duas vezes, com um atraso de um minuto entre tentativas de ligação. Pode modificar o número de tentativas de ligação faz com que o site, e o intervalo de tempo entre tentativas.  

Para gerir o remetente de um site, o **administração** área de trabalho, expanda o **configuração do Site** nó, selecione o **Sites** nó e, em seguida, selecione **propriedades** para o site que pretende gerir. Selecione o **remetente** separador para alterar as definições do remetente.  

## <a name="bkmk_dbrep"></a> Database replication  
Replicação de base de dados do Configuration Manager utiliza o SQL Server para transferir dados e intercalar as alterações efetuadas numa base de dados do site com as informações armazenadas na base de dados noutros sites da hierarquia. Tenha em atenção o seguinte sobre a replicação de base de dados:

-  Todos os sites partilhem as mesmas informações.  
-  Quando instala um site numa hierarquia, replicação de base de dados é automaticamente estabelecida entre o novo site e o respetivo site principal designado.  
-  Quando for concluída a instalação do site, replicação de base de dados é iniciada automaticamente.  

Quando adiciona um novo site para uma hierarquia, o Configuration Manager cria uma base de dados genérica no novo site. Em seguida, o site principal cria um instantâneo dos dados relevantes na respetiva base de dados e, em seguida, transfere o instantâneo para o novo site através da replicação baseada em ficheiros. O novo site utiliza, em seguida, o programa cópia do SQL Server em massa (BCP) para carregar as informações na respetiva cópia local da base de dados do Configuration Manager. Após o carregamento do instantâneo, cada site efetua a replicação de base de dados com outro site.  

Para replicar dados entre sites, o Configuration Manager utiliza o seu próprio serviço de replicação de base de dados. O serviço de replicação de base de dados utiliza para monitorizar a base de dados do local site para que as alterações de registo de alterações do SQL Server e, em seguida, replica as alterações para outros sites utilizando o SQL Server Service Broker (SSB). Por predefinição, este processo utiliza a porta de TCP/IP 4022.  

O Configuration Manager agrupa dados que replicam através da replicação de base de dados em grupos de replicação diferentes. Tenha em atenção o seguinte sobre grupos de replicação:

-  Cada grupo de replicação tem uma agenda de replicação separada e fixa que determina a frequência com que as alterações dos dados no grupo são replicadas para outros sites.  

     Por exemplo, uma alteração para uma configuração de administração baseada em funções replica rapidamente para outros sites para assegurar que estas alterações são impostas assim que possível. Entretanto, uma alteração da configuração de prioridade mais baixa, tal como um pedido para instalar um novo site secundário, replica com menos urgência. Pode demorar alguns minutos para um novo pedido de site para chegar ao site primário de destino.  

-   Pode modificar as seguintes definições para replicação de base de dados:  

    -  **Ligações de replicação de base de dados**. Controlar quando é que tráfego específico atravessa a rede.  
    -  **Vistas distribuídas**. Alterar as definições de ligações de replicação através do qual que pedidos feitos num site de administração central para dados de site selecionados podem aceder a esses dados de site diretamente a partir da base de dados de um site primário subordinado.  
    -  **Agendas**. Especifique quando é utilizada uma ligação de replicação e, quando são replicados diferentes tipos de dados do site.  
    -  **Resumo**. Alterar as definições de resumo de dados sobre o tráfego de rede que atravessa as ligações de replicação. Resumo ocorre a cada 15 minutos, por predefinição e é utilizado em relatórios para a replicação de base de dados.  
    -  **Limiares de replicação de base de dados**. Definir quando ligações são comunicadas como degradado ou falhado. Também pode configurar quando o Configuration Manager gera alertas sobre ligações de replicação que têm um Estado degradado ou falhado.  

O Configuration Manager classifica os dados que replica através da replicação de base de dados como **dados globais** ou **dados do site**. Quando ocorre a replicação da base de dados, as alterações aos dados globais e aos dados de site são transferidas através da ligação da replicação de base de dados. Replicação dos dados globais para um site principal ou subordinado. Dados do site são replicados apenas para um site principal. Um terceiro tipo de dados, dados locais não é replicado para outros sites. Dados locais são informações que não são necessárias para outros sites. Tenha em atenção o seguinte sobre tipos de dados:  

-  **Dados globais**. Dados globais referem-se a objetos criados administrador que são replicados para todos os sites da hierarquia, apesar dos sites secundários receberem apenas um subconjunto de dados globais, como dados de global proxy. Dados globais incluem implementações de software, atualizações de software, definições de coleção e âmbitos de segurança da administração baseada em funções. Os administradores podem criar dados globais em sites de administração central e sites primários.  
-  **Dados do site**. Dados do site refere-se a informações operacionais que sites primários do Configuration Manager e os clientes que criar relatório para sites primários. Os dados do site replicam para o site de administração central, mas não para outros sites primários. Dados do site abrangem dados de inventário de hardware, mensagens de estado, alertas e os resultados de coleções baseadas em consulta. Dados do site só são visualizáveis no site de administração central e no site primário onde os dados têm origem. Os dados do site apenas podem ser modificados no site primário onde foram criados.  

     Todos os dados do site replicam para o site de administração central. O site de administração central efetua administração e relatórios para a hierarquia de sites inteira.  

As secções seguintes descrevem pormenorizadamente as definições que pode alterar para gerir a replicação de base de dados.  

### <a name="bkmk_Dblinks"></a> Ligações de replicação de base de dados  
Quando instala um novo site numa hierarquia, o Configuration Manager cria automaticamente uma ligação de replicação de base de dados entre o site principal e o novo site. É criada uma única ligação para ligar os dois sites.  

Pode alterar as definições para cada ligação de replicação de base de dados para o ajudar a controlar a transferência de dados através da ligação de replicação. Cada ligação de replicação suporta configurações separadas. Os controlos para ligações de replicação de base de dados incluem o seguinte:  

-  Pare a replicação dos dados de site selecionados de um site primário para o site de administração central, para que o site de administração central pode aceder a estes dados diretamente a partir da base de dados do site primário.  
-  Agende a dados de site selecionados para transferir a partir de um site primário subordinado para o site de administração central.
-  Defina as definições que determinam quando uma ligação de replicação de base de dados tem um Estado degradado ou falhado.
-  Especifique quando aumentar alertas para uma ligação de replicação falhada.
-  Especifique a frequência do Configuration Manager resume os dados sobre o tráfego de replicação que utiliza a ligação de replicação. Estes dados são utilizados em relatórios.

Configurar uma ligação de replicação de base de dados, na consola do Configuration Manager, o **replicação de base de dados** nó, editar as propriedades da ligação. Este nó aparece no **monitorização** área de trabalho e no **administração** área de trabalho, no **configuração da hierarquia** nó. Pode editar uma ligação de replicação a partir do site principal ou do site subordinado da ligação de replicação.  

> [!TIP]  
> Pode editar ligações de replicação de base de dados a partir do nó **Replicação de Base de Dados** em qualquer uma das áreas de trabalho. No entanto, quando utiliza o **replicação de base de dados** nó o **monitorização** área de trabalho, também pode ver o estado da replicação de base de dados para ligações de replicação e aceder a ferramenta Analisador de ligações de replicação para ajudar a investigar problemas com a replicação de base de dados.  

Para obter informações sobre como configurar ligações de replicação, veja [Controlos de Replicação de Base de Dados de Site](#BKMK_DBRepControls). Para obter mais informações sobre como monitorizar a replicação, consulte o artigo [como monitorizar o estado de replicação e de ligações de replicação de base de dados](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) no [monitorizar a infraestrutura hierarquia e replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) tópico.  

Utilize as informações nas secções seguintes para ajudar a planear ligações de replicação de base de dados.  

### <a name="bkmk_distviews"></a> Vistas distribuídas  
Através de vistas distribuídas, que pedidos feitos num site de administração central para selecionar acesso a dados do site esses dados de site diretamente a partir da base de dados de um site primário subordinado. O acesso direto substitui a necessidade de replicar os dados de site do site primário para o site de administração central. Uma vez que cada ligação de replicação é independente de outras ligações de replicação, pode utilizar as vistas distribuídas de apenas ligações de replicação que escolher. Não é possível utilizar as vistas distribuídas entre um site primário e um site secundário.  

As vistas distribuídas podem fornecer as seguintes vantagens:  

-  Reduzir a carga de CPU para processar alterações de base de dados no site de administração central e sites primários
-  Reduzir a quantidade de dados transferidos através da rede para o site de administração central
-  Melhorar o desempenho do SQL server que aloja a base de dados do site de administração central
-  Reduzir o espaço em disco utilizado pela base de dados no site de administração central

Considere utilizar as vistas distribuídas quando um site primário estiver numa perto do site de administração central na rede e os dois sites estão sempre e sempre ligado. Isto acontece porque as vistas distribuídas substituem a replicação dos dados selecionados entre os sites com ligações diretas entre os SQL servers em cada site. Uma ligação direta é estabelecida sempre que é efetuado um pedido para estes dados no site de administração central. Normalmente, os pedidos de dados que poderá ativar para vistas distribuídas são efetuados quando executa relatórios ou consultas, quando visualiza informações no Explorador de recursos e por avaliação da coleção em coleções que incluem regras baseadas nos dados de site.  

Por predefinição, as vistas distribuídas estão desativadas para cada ligação de replicação. Quando ativar as vistas distribuídas para uma ligação de replicação, seleciona os dados de site que não serão replicado para o site de administração central ao longo dessa ligação. O site de administração central acede a estes dados diretamente a partir da base de dados do site primário subordinado que partilha a ligação. Pode configurar os seguintes tipos de dados de site para vistas distribuídas:  

-  Dados de inventário de hardware a partir de clientes
-  Dados de inventário de software e medição de clientes
-  Mensagens de estado de clientes, do site primário e de todos os sites secundários

Operacionalmente, as vistas distribuídas são invisíveis ao utilizador administrativo que visualiza dados na consola do Configuration Manager ou em relatórios. Quando é efetuado um pedido de dados que estão ativados para vistas distribuídas, o SQL server que aloja diretamente a base de dados para o site de administração central acede ao SQL server do site primário subordinado para obter as informações. Por exemplo, utilize uma consola do Configuration Manager no site de administração central para pedir informações sobre o inventário de hardware a partir de dois sites e apenas um site tem inventário de hardware ativado para uma vista distribuída. As informações de inventário para clientes a partir do site que não está configurado para vistas distribuídas são obtidas da base de dados no site de administração central. As informações de inventário para clientes do site que está configurado para vistas distribuídas são acedidas a partir da base de dados do site primário subordinado. Esta informação aparece na consola do Configuration Manager ou num relatório sem identificar a origem.  

Desde que a ligação de replicação possua um tipo de dados ativados para vistas distribuídas, o site primário subordinado não replicar os dados para o site de administração central. Assim que desativa as vistas distribuídas para um tipo de dados, o site subordinado principal site retoma a replicação dos dados para o site de administração central como parte da replicação de dados normal. No entanto, antes destes dados ficarem disponíveis no site de administração central, os grupos de replicação que tenham estes dados têm de ser reinicializados entre o site primário e o site de administração central. Da mesma forma, depois de desinstalar um site primário que possui as vistas distribuídas ativadas, o site de administração central tem de concluir a reinicialização dos respetivos dados para poder aceder a dados que estavam ativados para vistas distribuídas no site de administração central.  

> [!IMPORTANT]  
> Quando utiliza vistas distribuídas em qualquer ligação de replicação na hierarquia do site, tem de desativar as vistas distribuídas para todas as ligações de replicação antes de desinstalar qualquer site primário. Para obter mais informações, veja [Desinstalar um site primário configurado com vistas distribuídas](../../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#BKMK_UninstallPrimaryDistViews).  

#### <a name="prerequisites-and-limitations-for-distributed-views"></a>Pré-requisitos e limitações das vistas distribuídas  

-  Pode utilizar as vistas distribuídas apenas nas ligações de replicação entre um site de administração central e um site primário.
- O site de administração central tem de utilizar uma edição Enterprise do SQL Server. O site primário não tem este requisito.
-  O site de administração central pode ter apenas uma instância do fornecedor de SMS instalado e essa instância tem de estar instalada no servidor de base de dados do site. Isto é necessário para suportar a autenticação Kerberos necessária para que o SQL server no site de administração central pode aceder ao SQL server no site primário subordinado. Não existem limites para o fornecedor de SMS no site primário subordinado.
-  O site de administração central só pode ter um ponto do SQL Server Reporting Services instalado e este tem de estar localizado no servidor da base de dados do site. Isto é necessário para suportar a autenticação Kerberos necessária para ativar o SQL server no site de administração central para aceder ao SQL server no site primário subordinado.
-  A base de dados do site não pode estar alojada num cluster do SQL Server.
-  A base de dados do site não pode estar alojada num grupo de disponibilidade SQL Server Always On.
-  A conta de computador do servidor da base de dados do site de administração central necessita de permissões de leitura para a base de dados do site primário.

> [!IMPORTANT]  
>  As vistas distribuídas e agendas de replicação dos dados são mutuamente exclusivas definições para uma ligação de replicação de base de dados.  

### <a name="BKMK_schedules"></a> Agendar transferências de dados de site em ligações de replicação de base de dados  
Para ajudar a controlar a largura de banda de rede que é utilizada para replicar dados de site de um site primário subordinado para o respetivo site de administração central, pode agendar quando é utilizada uma ligação de replicação e especificar quando são replicados diferentes tipos de dados. Pode controlar quando as mensagens de estado, os dados de inventário e de medição são replicados pelo site primário. As ligações de replicação de base de dados de sites secundários não suportam agendas para dados de sites. Não é possível agendar a transferência de dados globais.  

Quando configura uma agenda de ligação de replicação de base de dados, pode restringir a transferência de dados de site selecionados do site primário para o site de administração central e pode configurar diferentes horas para replicar diferentes tipos de dados de site.  

> [!IMPORTANT]  
> As vistas distribuídas e agendas de replicação dos dados são configurações mutuamente exclusivas para uma ligação de replicação de base de dados.  

### <a name="BKMK_SummarizeDBReplication"></a> Resumo do tráfego de replicação de base de dados  
Cada site resume periodicamente os dados sobre o tráfego de rede que atravessa as ligações de replicação de base de dados para o site. Dados resumidos são utilizados em relatórios para a replicação de base de dados. Ambos os sites numa ligação de replicação resumem o tráfego de rede que atravessa a ligação de replicação. O resumo de dados é efetuado pelo SQL Server que aloja a base de dados do site. Depois dos dados são resumidos, as informações são replicadas para outros sites como dados globais.  

Por predefinição, o resumo ocorre a cada 15 minutos. Para modificar a frequência do resumo do tráfego de rede, nas propriedades de ligação de replicação de base de dados, edite o **intervalo de resumo**. A frequência do resumo afeta as informações que vê na relatórios sobre a replicação de base de dados. Pode escolher um intervalo de entre 5 minutos e 60 minutos. Quando aumenta a frequência do resumo, aumenta a carga de processamento no SQL server em cada site na ligação de replicação.  

### <a name="BKMK_DBRepThresholds"></a>Limiares de replicação de base de dados  
Os limiares de replicação de base de dados definem quando o estado de uma ligação de replicação de base de dados é comunicado como degradado ou falhado. Por predefinição, uma ligação é definida para o estado degradado quando qualquer grupo de replicação de uma falha ao concluir a replicação durante um período de ocorrem consecutivamente 12 tentativas. A ligação é definida para o estado de falha quando qualquer grupo de replicação não consegue ocorrem consecutivamente 24 tentativas.  

Pode especificar valores personalizados para otimizar a quando o Configuration Manager apresenta uma ligação de replicação degradada ou falhada. Adjusting quando o Configuration Manager comunica cada Estado para as ligações de replicação de base de dados pode ajudá-lo com precisão monitorizar o estado de funcionamento da replicação de base de dados em todas as ligações de replicação de base de dados.  

Porque é possível para os grupos de replicação de uma ou algumas falharem enquanto outros grupos de replicação continuam a replicar com êxito, planeie a revisão do Estado de replicação de uma ligação de replicação quando esta comunica um Estado de degradada pela primeira vez. Se ocorrerem atrasos recorrentes em grupos de replicação específicos e estes atrasos não apresentarem um problema ou sempre que a ligação de rede entre os sites tiver pouca largura de banda disponível, considere modificar os valores de tentativa do estado degradado ou falhado da ligação. Quando aumenta o número de tentativas antes da ligação é definida como degradada ou falhada, pode eliminar os avisos falsos para problemas conhecidos e controlar com maior precisão o estado da ligação.  

Além disso, considere o intervalo de sincronização de replicação para cada grupo de replicação para compreender com que frequência ocorre a replicação desse grupo. Para ver o **intervalo de sincronização** para os grupos de replicação, no **monitorização** área de trabalho, no **replicação de base de dados** nó, selecione o **detalhes da replicação** separador de uma ligação de replicação.  

Para mais informações sobre como monitorizar a replicação de base de dados, incluindo como visualizar o estado de replicação, consulte o artigo [como monitorizar o estado de replicação e de ligações de replicação de base de dados](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) no [monitorizar a infraestrutura hierarquia e replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) tópico.  

Para obter informações sobre como configurar limiares de replicação de base de dados, consulte o artigo [controlos de replicação de base de dados do Site](#BKMK_DBRepControls).  

## <a name="BKMK_DBRepControls"></a> Controlos de replicação de base de dados do site  
Pode alterar as definições de cada base de dados do site para ajudar a controlar a largura de banda de rede utilizada para replicação de base de dados. As definições são aplicadas apenas para a base de dados do site em que configura as definições. As definições são sempre utilizadas quando o site replica dados através da replicação de base de dados para outro site.  

Seguem-se os controlos de replicação que pode modificar para cada base de dados do site:  

-  Altere a porta do SSB.  
-  Configure o período de tempo de espera antes de falhas de replicação acionar o site reinicialize a respetiva cópia da base de dados do site.  
-  Configure uma base de dados de sites para comprimir os dados que este replica por replicação da base de dados. Os dados são comprimidos apenas para transferência entre sites e não para armazenamento na base de dados de sites de qualquer um dos sites.  

Para alterar as definições para os controlos de replicação para uma base de dados do site, na consola do Configuration Manager, no **replicação de base de dados** nó, editar as propriedades da base de dados do site. Este nó aparece por baixo do nó **Configuração da Hierarquia** , na área de trabalho **Administração** , e também aparece na área de trabalho **Monitorização**. Para editar as propriedades da base de dados do site, selecione a ligação de replicação entre os sites e, em seguida, abra **propriedades de base de dados principal** ou **propriedades de base de dados subordinada**.  

> [!TIP]  
> Pode configurar os controlos de replicação de base de dados no nó **Replicação de Base de Dados** em ambas as áreas de trabalho. No entanto, quando utiliza o **replicação de base de dados** nó o **monitorização** área de trabalho, também pode ver o estado da replicação de base de dados de uma ligação de replicação e aceder a ferramenta Analisador de ligações de replicação para ajudar a investigar problemas com a replicação.  


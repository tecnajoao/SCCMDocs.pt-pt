---
title: Alertas e o sistema de estado
titleSuffix: Configuration Manager
description: "Configurar alertas e utilizar o sistema de estado para manter-se informado sobre o estado da implementação do Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7341cc6e-9e08-41e4-bcc6-6c1ff12e85ca
caps.latest.revision: "10"
author: mstewart
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 21ef1ddce1167acc253f52daba5cdd9f9e8e0a12
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="use-alerts-and-the-status-system-for-system-center-configuration-manager"></a>Utilizar alertas e o sistema de estado para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Configurar alertas e utilizar o sistema de estado incorporado para manter-se informado sobre o estado da implementação do System Center Configuration Manager.  


##  <a name="bkmk_Status"></a> Sistema de estado  
 Todos os componentes do site principal geram mensagens de estado que fornecem comentários sobre as operações de site e de hierarquia.    Estas informações podem mantê-lo informado sobre o estado de funcionamento dos diferentes processos do site. Pode otimizar o sistema de alerta para ignorar o ruído de problemas conhecidos, ao aumentar a visibilidade inicial para outros problemas que poderão requerer a sua atenção.  

 Por predefinição, o sistema de estado do Configuration Manager funciona sem configuração, utilizando as definições adequadas para a maior parte dos ambientes. No entanto, é possível configurar o seguinte:  

-   **Summarizers de estado:** Pode editar o estado alterar summarizers em cada site para controlar a frequência das mensagens de estado que geram um indicador de estado para os quatro summarizers seguintes:  

    -   Summarizer de Implementação da Aplicação  

    -   Summarizer de Estatísticas da Aplicação  

    -   Status Summarizer de Componentes  

    -   Summarizer de Estado do Sistema de Sites  

-   **Regras de filtro de estado:** Pode criar novas regras de Filtro Estado, modificar a prioridade de regras, desativar ou ativar regras e eliminar regras não utilizadas em cada site.  

    > [!NOTE]  
    >  As regras do filtro de estado não suportam a utilização de variáveis de ambiente para executar comandos externos.  

-   **Relatórios de Estado:** Pode configurar o servidor e relatórios de componente de cliente para modificar a forma como as mensagens de estado são comunicadas ao sistema de estado do Configuration Manager e especificam para onde são enviadas mensagens de estado.  

    > [!WARNING]  
    >  Uma vez que as predefinições dos relatórios são adequadas para a maior parte dos ambientes, altere-as com cuidado. Quando aumenta o nível dos relatórios ao escolher a todos os detalhes de estado, pode aumentar a quantidade de mensagens de estado para ser de relatório de estado processados que aumenta a carga de processamento no site do Configuration Manager. Se diminuir o nível dos relatórios de estado, poderá limitar a utilidade dos summarizers de estado.  

Uma vez que o sistema de estado mantém configurações separadas para cada site, é necessário editar cada site individualmente.  

###  <a name="bkmk_configstatus"></a> Procedimentos para configurar o sistema de estado  

##### <a name="to-configure-status-summarizers"></a>Para configurar summarizers de estado  

1.  Na consola do Configuration Manager, navegue para **administração** > **configuração do Site** >**Sites**e, em seguida, selecione o site para o qual pretende configurar o sistema de estado.  

2.  No separador **Home Page** , no grupo **Definições** , clique em **Summarizers de Estado**.  

3.  Na caixa de diálogo **Summarizers de Estado** , selecione o summarizer que pretende configurar e clique em **Editar** para abrir as propriedades desse summarizer. Se estiver a editar os summarizers Implementação da Aplicação ou Estatísticas da Aplicação, avance para o passo 5. Se estiver a editar o Estado do Componente, avance para o passo 6. Se estiver a editar o summarizer Estado do Sistema de Sites, avance para o passo 7.  

4.  Utilize os passos seguintes depois de abrir a página de propriedades do Summarizer de Implementação da Aplicação ou do Summarizer de Estatísticas da Aplicação:  

    1.  No separador **Geral** da página de propriedades dos summarizers, configure os intervalos de resumo e clique em **OK** para fechar a página de propriedades.  

    2.  Clique em **OK** para fechar a caixa de diálogo **Resumidores de Estado** e concluir este procedimento.  

5.  Utilize os passos seguintes depois de abrir as páginas de propriedades do Summarizer de Estado do Componente:  

    1.  No **geral** separador da página de propriedades dos summarizers, configure os valores replicação e de limiar.  

    2.  No separador **Limiares** , selecione o **Tipo de mensagem** que pretende configurar e clique no nome de um componente na lista **Limiares** .  

    3.  Na caixa de diálogo **Propriedades do Limiar de Estado** , edite os valores dos limiares de aviso e crítico e, em seguida, clique em **OK**.  

    4.  Repita os passos 6.b e 6.c conforme necessário e, quando tiver terminado, clique em **OK** para fechar as propriedades do summarizer.  

    5.  Clique em **OK** para fechar a caixa de diálogo **Resumidores de Estado** e concluir este procedimento.  

6.  Utilize os passos seguintes depois de abrir as páginas de propriedades do Summarizer de Estado do Sistema de Sites:  

    1.  No **geral** separador da página de propriedades dos summarizers, configure os valores de replicação e de agendamento.  

    2.  No separador **Limiares** , especifique os valores dos **Limiares predefinidos** para configurar limiares predefinidos para a apresentação dos estados críticos e de aviso.  

    3.  Para editar os valores de **Objetos de armazenamento**específicos, selecione o objeto na lista **Limiares específicos** e, em seguida, clique no botão **Propriedades** para aceder e editar os limiares de aviso e crítico dos objetos de armazenamento. Clique em **OK** para fechar as propriedades dos objetos de armazenamento.  

    4.  Para criar um novo objeto de armazenamento, clique no botão **Criar Objeto** e especifique os valores dos objetos de armazenamento. Clique em **OK** para fechar as propriedades dos objetos.  

    5.  Para eliminar um objeto de armazenamento, selecione o objeto e clique no botão **Eliminar** .  

    6.  Repita os passos 7 7 conforme necessário. Quando tiver terminado, clique em **OK** para fechar as propriedades do summarizer.  

    7.  Clique em **OK** para fechar a caixa de diálogo **Resumidores de Estado** e concluir este procedimento.  

##### <a name="to-create-a-status-filter-rule"></a>Para criar uma regra do filtro de estado  

1.  Na consola do Configuration Manager, navegue para **administração** > **configuração do Site** >**Sites**e, em seguida, selecione o site onde pretende configurar o sistema de estado.  

2.  No separador **Home Page** , no grupo **Definições** , clique em **Regras do Filtro de Estado**. É aberta a caixa de diálogo **Regras do Filtro de Estado** .  

3.  Clique em **Criar**.  

4.  No **Assistente de Criação de Regra de Filtro de Estado**, na página **Geral** , especifique um nome para a nova regra do filtro de estado e os critérios de correspondência de mensagens para a regra e, em seguida, clique em **Seguinte**.  

5.  Na página **Ações** , especifique as ações a executar quando uma mensagem de estado corresponde à regra de filtro e clique em **Seguinte**.  

6.  Na página **Resumo** , reveja os detalhes da nova regra e, em seguida, conclua o assistente.  

    > [!NOTE]  
    >  Apenas o Configuration Manager requer que a nova regra de filtro de estado tem um nome. Se a regra for criada mas não forem especificados quaisquer critérios para processar mensagens de estado, a regra do filtro de estado não terá qualquer efeito. Este comportamento permite criar e organizar regras antes de configurar os critérios do filtro de estado para cada regra.  

##### <a name="to-modify-or-delete-a-status-filter-rule"></a>Para modificar ou eliminar uma regra do filtro de estado  

1.  Na consola do Configuration Manager, navegue para **administração** > **configuração do Site** >**Sites**e, em seguida, selecione o site onde pretende configurar o sistema de estado.  

2.  No separador **Home Page** , no grupo **Definições** , clique em **Regras do Filtro de Estado**.  

3.  Na caixa de diálogo **Regras do Filtro de Estado** , selecione a regra que pretende modificar e execute uma das seguintes ações:  

    -   Clique em **Aumentar Prioridade** ou em **Diminuir Prioridade** para alterar a ordem de processamento da regra do filtro de estado. Em seguida, selecione outra ação ou vá para o passo 8 deste procedimento para concluir esta tarefa.  

    -   Clique em **Desativar** ou em **Ativar** para alterar o estado da regra. Depois de alterar o estado da regra, selecione outra ação ou vá para o passo 8 deste procedimento para concluir esta tarefa.  

    -   Clique em **Eliminar** se pretender eliminar a regra do filtro de estado deste site e, em seguida, clique em **Sim** para confirmar a ação. Depois de eliminar uma regra, selecione outra ação ou vá para o passo 8 deste procedimento para concluir esta tarefa.  

    -   Clique em **Editar** se pretender alterar os critérios para a regra da mensagem de estado e avance para o passo 5 deste procedimento.  

4.  No separador **Geral** da caixa de diálogo das propriedades da regra do filtro de estado, modifique a regra e os critérios de correspondência de mensagens.  

5.  No separador **Ações** , modifique as ações a executar quando uma mensagem de estado corresponde à regra de filtro.  

6.  Clique em **OK** para guardar as alterações.  

7.  Clique em **OK** para fechar a caixa de diálogo **Regras do Filtro de Estado** .  

##### <a name="to-configure-status-reporting"></a>Para configurar relatórios de estado  

1.  Na consola do Configuration Manager, navegue para **administração** > **configuração do Site** > **Sites**e, em seguida, selecione o site onde pretende configurar o sistema de estado.  

2.  No separador **Home Page** , no grupo **Definições** , clique em **Configurar Componentes do Site**e selecione **Relatórios de Estado**.  

3.  Na caixa de diálogo **Propriedades do Componente de Relatórios de Estado** , especifique as mensagens de estado do componente de servidor e de cliente que pretende comunicar ou registar:  

    1.  Configurar **relatório** para enviar mensagens de estado para o sistema de mensagens de estado do Configuration Manager.  

    2.  Configurar **Registo** para escrever o tipo e a gravidade das mensagens de estado para o registo de eventos do Windows.  

4.  Clique em **OK**.  

###  <a name="BKMK_MonitorSystemStatus"></a> Monitorizar o estado do sistema do Configuration Manager  
 **Estado do sistema** no Configuration Manager fornece uma descrição geral das operações gerais de sites e site de operações do servidor da sua hierarquia. Pode revelar problemas operacionais para servidores do sistema de sites ou componentes e pode utilizar o estado do sistema para rever detalhes específicos de diferentes operações do Configuration Manager. Monitorizar o estado do sistema de **estado do sistema** o nó do **monitorização** área de trabalho na consola do Configuration Manager.  

 A maioria das funções de sistema de sites do Configuration Manager e componentes geram mensagens de estado. Os detalhes das mensagens de estado são registados no registo operacional de cada cliente, mas também são enviados para a base de dados do site, onde são resumidos e apresentados num rollup geral do estado de funcionamento de cada componente ou sistema de sites. Estes rollups de mensagens de estado fornecem detalhes de informações de operações regulares, avisos e detalhes de erros. Pode configurar os limiares em que os avisos ou erros são ativados e otimizar o sistema para assegurar que a informação de rollup ignora problemas conhecidos que não sejam relevantes para si e chama a atenção para problemas graves nos servidores ou para operações de componentes que pretenda investigar.  

 O estado do sistema é replicado para outros sites numa hierarquia como dados do site, não como dados globais. Isto significa que só pode ver o estado para o site ao qual se liga a consola do Configuration Manager e todos os sites subordinados abaixo desse site. Por conseguinte, considere ligar a consola do Configuration Manager para o site de nível superior da hierarquia quando visualizar o estado do sistema.  

 Utilize a tabela seguinte para identificar as diferentes vistas de estado do sistema e quando utilizar cada uma delas.  

|Nó|Mais informações|  
|----------|----------------------|  
|Estado do Site|Utilize este nó para ver um rollup do estado de cada sistema de sites para rever o estado de funcionamento de cada servidor do sistema de sites. O estado de funcionamento do sistema de sites é determinado por limiares configurados para cada site no **Summarizer de Estado do Sistema de Sites**.<br /><br /> É possível ver as mensagens de estado de cada sistema de sites, definir limiares para mensagens de estado e gerir a operação dos componentes nos sistemas de sites através do **Gestor do Serviço do Configuration Manager**.|  
|Estado do Componente|Utilize este nó para ver um rollup do Estado de cada componente do Configuration Manager para rever o estado de funcionamento operacional do componente. O estado de funcionamento do componente do site é determinado por limiares configurados para cada site no **Summarizer de Estado do Componente**.<br /><br /> É possível ver as mensagens de estado de cada componente, definir limiares para mensagens de estado e gerir a operação de componentes através do **Gestor do Serviço do Configuration Manager**.|  
|Registos em Conflito|Utilize este nó para ver mensagens de estado sobre clientes que poderão ter registos em conflito.<br /><br /> O Configuration Manager utiliza o ID de hardware para tentar identificar clientes que possam ser duplicados e alertá-lo para os registos em conflito. Por exemplo, se tiver de reinstalar um computador, o ID de hardware será o mesmo, mas o GUID que o Configuration Manager utiliza poderá ter sido alterado.|  
|Consultas de Mensagens de Estado|Utilize este nó para consultar mensagens de estado de eventos específicos e detalhes relacionados. É possível utilizar consultas de mensagens de estado para localizar as mensagens de estado relacionadas com eventos específicos.<br /><br /> Muitas vezes, pode utilizar consultas de mensagens de estado para identificar quando um componente específico, a operação ou o objecto do Gestor de configuração foi modificado e a conta que foi utilizada para efetuar a modificação. Por exemplo, pode executar a consulta incorporada para **Coleções Criadas, Modificadas ou Eliminadas** para identificar quando uma coleção específica foi criada e a conta de utilizador utilizada para criar a coleção.|  

####  <a name="bkmk_managestatus"></a> Gerir o estado do site e o estado do componente  
 Utilize as informações seguintes para gerir o estado do site e o estado do componente:  

-   Para configurar limiares para o sistema de estado, consulte [Procedimentos para configurar o sistema de estado](#bkmk_configstatus).  

-   Para gerir componentes individuais no Configuration Manager, utilize o **do serviço do Configuration Manager**.  

####  <a name="bkmk_view"></a> Ver mensagens de estado  
 É possível ver as mensagens de estado para componentes e servidores de sistema de sites individuais.  

 Para ver mensagens de estado na consola do Configuration Manager, selecione um componente ou servidor do sistema de site específico e, em seguida, clique em **Mostrar mensagens**. Ao visualizar mensagens, é possível selecionar a visualização de tipos de mensagens específicos ou mensagens de um período de tempo específico, bem como filtrar os resultados com base em detalhes das mensagens de estado.  

##  <a name="bkmk_Alerts"></a> Alertas  
 O Configuration Manager alertas são geradas por algumas operações quando ocorre uma condição específica.  

-   Normalmente, os alertas são gerados quando ocorre um erro que é necessário resolver  

-   Os alertas podem também ser gerados para o avisar de que existe uma condição, para que possa continuar a monitorizar a situação  

-   Alguns alertas são configurados por si, tais como alertas para o Endpoint Protection e o estado do cliente , enquanto outros alertas são configuradas automaticamente  

-   Pode configurar subscrições de alertas, que podem então enviar detalhes por e-mail, melhorando a deteção de problemas chave  

 Utilize a tabela seguinte para obter informações sobre como configurar alertas e subscrições de alertas no Configuration Manager:  


|Ação|Mais Informações|  
|------------|----------------------|  
|Configurar alertas de Endpoint Protection para uma coleção|Consulte **como configurar alertas para o Endpoint Protection no Configuration Manager** no [configurar o Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md)|  
|Configurar alertas de estado do cliente para uma coleção|Consulte [como configurar o estado do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md).|  
|Gerir alertas do Configuration Manager|Consulte a secção [Management tasks for alerts](#BKMK_Manage) deste tópico.|  
|Configurar subscrições de e-mail para alertas|Consulte a secção [Management tasks for alerts](#BKMK_Manage) deste tópico.|  
|Monitorizar alertas|Consulte a secção [Monitorizar alertas](#BKMK_MonitorAlerts)|  

###  <a name="BKMK_Manage"></a> Management tasks for alerts  

##### <a name="to-manage-general-alerts"></a>Para gerir alertas gerais  

1.  Na consola do Configuration Manager, navegue para **monitorização** > **alertas**e, em seguida, selecione uma tarefa de gestão.  

  Utilize a tabela seguinte para obter mais informações sobre as tarefas de gestão que podem necessitar de algumas informações antes de as selecionar.  

|Tarefa de gestão|Detalhes|  
    |---------------------|-------------|  
    |**Configure**|Abre o  *&lt;nome do alerta*\>**propriedades** caixa de diálogo onde pode modificar o nome, a gravidade e os limiares do alerta selecionado. Se alterar a gravidade do alerta, esta configuração afeta a forma como os alertas são apresentados na consola do Configuration Manager.|  
    |**Editar Comentário**|Introduza um comentário para os alertas selecionados. Estes comentários são apresentados com o alerta na consola do Configuration Manager.|  
    |**Adiar**|Suspende a monitorização do alerta até que a data especificada seja atingida. Nessa altura, o estado do alerta é atualizado.<br /><br /> Só é possível adiar um alerta quando o mesmo está ativado.|  
    |**Criar subscrição**|Abre a caixa de diálogo **Nova Subscrição** , onde pode criar uma subscrição de e-mail para o alerta selecionado.|  

##### <a name="to-configure-endpoint-protection-alerts-for-a-collection"></a>Para configurar alertas do Endpoint Protection para uma coleção  

1.  pendente  

##### <a name="to-configure-client-status-alerts-for-a-collection"></a>Para configurar alertas de estado do cliente para uma coleção  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** >   **coleções de dispositivos**.  

2.  Na lista **Coleções de Dispositivos** , selecione a coleção para a qual pretende configurar alertas e, no separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

    > [!NOTE]  
    >  Não é possível configurar alertas de coleções de utilizadores.  

3.  No **alertas** separador do  *&lt;nome da coleção*\>**propriedades** caixa de diálogo, clique em **adicionar**.  

    > [!NOTE]  
    >  O separador **Alertas** só está visível se a função de segurança a que o utilizador está associado tiver permissões para alertas.  

4.  Na caixa de diálogo **Adicionar Novos Alertas da Coleção** , escolha os alertas que pretende que sejam gerados quando os limites do estado do cliente são inferiores a um valor específico e, em seguida, clique em **OK**.  

5.  Na lista **Condições** do separador **Alertas** , selecione cada um dos alertas do estado do cliente e especifique as informações seguintes.  

    -   **Nome do alerta** - aceite o nome predefinido ou introduza um novo nome para o alerta.  

    -   **Gravidade do alerta** – na lista pendente, escolha o nível de alerta que será apresentado na consola do Configuration Manager.  

    -   **Emitir um alerta** -especifique a percentagem de limiar do alerta.  

6.  Clique em **OK** para fechar o  *&lt;nome da coleção*\>**propriedades** caixa de diálogo.  

##### <a name="to-configure-email-notification-for-alerts"></a>Para configurar notificações por e-mail para os alertas  

1.  Na consola do Configuration Manager, navegue para **monitorização** > **alertas** > **subscrições**.  

2.  No separador **Home Page** , no grupo **Criar** , clique em **Configurar Notificação por Correio Eletrónico**.  

3.  Na caixa de diálogo **Propriedades do Componente de Notificação por E-mail** , especifique as seguintes informações:  

    -   **Ativar notificação por e-mail para alertas**: Selecione esta caixa de verificação para ativar o Configuration Manager para utilizar um servidor SMTP para enviar alertas por e-mail.  

    -   **FQDN ou endereço IP do servidor SMTP para enviar alertas por e-mail**: Introduza o nome de domínio completamente qualificado (FQDN) ou endereço IP e a porta SMTP do servidor de e-mail que pretende utilizar para estes alertas.  

    -   **Conta de ligação do servidor SMTP**: Especifique o método de autenticação para o Configuration Manager para utilizar para ligar ao servidor de e-mail.  

    -   **Endereço do remetente para enviar alertas por e-mail**: Especifique o endereço de e-mail a partir da qual são enviados e-mails de alerta.  

    -   **Testar servidor SMTP**: Envia um e-mail de teste para o endereço de e-mail especificado no **endereço do remetente para enviar alertas por e-mail**.  

4.  Clique em **OK** para guardar as definições e fechar a caixa de diálogo **Propriedades dos Componentes das Definições de E-mail** .  

##### <a name="to-subscribe-to-email-alerts"></a>Para subscrever alertas por e-mail  

1.  Na consola do Configuration Manager, navegue para **monitorização** > **alertas**.  

2.  Selecione um alerta e, em seguida, no separador **Home Page** , no grupo **Subscrição** , clique em **Criar subscrição**.  

3.  Na caixa de diálogo **Nova Subscrição** , especifique as seguintes informações:  

    -   **Nome**: Introduza um nome para identificar a subscrição de correio eletrónico. Pode utilizar até 255 carateres.  

    -   **Endereço de correio eletrónico**: Introduza os endereços de e-mail que pretende que o alerta seja enviado. Pode separar os vários endereços de e-mail com ponto e vírgula.  

    -   **Idioma do e-mail**: Na lista, especifique o idioma do e-mail.  

4.  Clique em **OK** para fechar a caixa de diálogo **Nova Subscrição** e para criar a subscrição de e-mail.  

    > [!NOTE]  
    >  Pode eliminar e editar subscrições na área de trabalho **Monitorização** , expandindo o nó **Alertas** e, em seguida, clique no nó **Subscrições** .  

###  <a name="BKMK_MonitorAlerts"></a> Monitorizar alertas  
 Para ver alertas, utilize o nó **Alertas** da área de trabalho **Monitorização** . Os alertas têm um dos seguintes estados de alerta:  

-   **Nunca ativado**: A condição do alerta não foi cumprida.  

-   **Active Directory**: A condição do alerta foi cumprida.  

-   **Cancelado**: A condição de um alerta ativo já não for cumprida. Este estado indica que a condição que causou o alerta está agora resolvida.  

-   **Adiada**: Um utilizador administrativo configurou o Configuration Manager para avaliar o estado do alerta posteriormente.  

-   **Desativado**: O alerta foi desativado por um utilizador administrativo. Quando um alerta está neste estado, o Configuration Manager atualiza o alerta mesmo que o estado do alerta se altere.  

 Pode efetuar uma das seguintes ações quando o Configuration Manager gera um alerta:  

-   Resolver a condição que causou o alerta, por exemplo, resolver um problema de rede ou um problema de configuração que gerou o alerta. Depois do Configuration Manager detetar que já não existe o problema, o estado de alerta alterado para **Cancelar**.  

-   Se o alerta é um problema conhecido, pode adiar o alerta durante um período de tempo específico. Nessa altura, o Configuration Manager atualiza o alerta para o estado atual.  

     Apenas é possível adiar um alerta quando está ativo.  

-   Pode editar o **Comentário** de um alerta para que outros utilizadores administrativos possam ver que tem conhecimento do alerta. Por exemplo, pode identificar no comentário a forma de resolver a condição, fornecer informações sobre o estado atual da condição ou explicar por que motivo adiou o alerta.  

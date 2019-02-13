---
title: Monitor de replicação
titleSuffix: Configuration Manager
description: Saiba como monitorizar a infraestrutura e operações no Configuration Manager utilizando a área de trabalho de monitorização na consola do.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3fab4d67-8d2a-45ce-8b06-471280102cf6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7a9fcf06630c76fc3e1123fa56861c4de224521
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129379"
---
# <a name="monitor-hierarchy-and-replication-infrastructure-in-system-center-configuration-manager"></a>Monitorizar a infraestrutura de hierarquia e replicação no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para monitorizar a infraestrutura e operações no System Center Configuration Manager, utilize o **monitorização** área de trabalho na consola do Configuration Manager.  

> [!NOTE]  
>  A exceção a esta localização é a Migração, que é monitorizada diretamente no nó **Migração** da área de trabalho **Administração** . Para obter mais informações, veja [Operações de migração para o System Center Configuration Manager](../../../core/migration/operations-for-migration.md).  

 Além de utilizar a consola do Configuration Manager para monitorização, pode utilizar os relatórios do Configuration Manager ou ver ficheiros de registo do Configuration Manager para componentes do Configuration Manager. Para obter informações sobre relatórios, veja [Os relatórios do System Center Configuration Manager](../../../core/servers/manage/reporting.md). Para obter informações sobre ficheiros de registo, veja [Ficheiros de registo no System Center Configuration Manager](../../../core/plan-design/hierarchy/log-files.md).  

 Quando monitorizar sites, procure sinais que indiquem problemas que exijam uma ação da sua parte. Por exemplo:  

-   Uma acumulação de ficheiros em servidores de site e sistemas de sites.  

-   Mensagens de estado que indiquem um erro ou um problema.  

-   Falha de comunicações intra-site.  

-   Mensagens de erro e aviso no registo de eventos do sistema dos servidores.  

-   Mensagens de erro e aviso no registo de erros do Microsoft SQL Server.  

-   Sites ou clientes que não comuniquem há muito tempo.  

-   Resposta lenta da base de dados do SQL Server.  

-   Sinais de falha de hardware.  

Para minimizar o risco de falha de um site, se as tarefas de monitorização revelarem sinais de problemas, investigue a origem do problema e corrija-o logo que seja possível.  



##  <a name="BKMK_MonintorMgmtTasks"></a> Monitorizar tarefas de gestão comuns do Configuration Manager  
 O Configuration Manager fornece monitorização incorporada a partir da consola do Configuration Manager. É possível monitorizar muitas tarefas, incluindo as relacionadas com atualizações de software, gestão de energia e a implementação de conteúdo na hierarquia.  

 Utilize as seguintes informações para ajudar a monitorizar tarefas comuns do Configuration Manager:  

 **Alertas**  
   Veja [Monitorizar alertas](../../../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorAlerts) em [Utilizar alertas e o sistema de estado para o System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Definições de Compatibilidade**  
   Veja [Como monitorizar as definições de compatibilidade no System Center Configuration Manager](../../../compliance/deploy-use/monitor-compliance-settings.md).  

 **Implementação de Conteúdos**  
   Para obter informações gerais sobre a monitorização de conteúdo, veja [Gerir conteúdo e a infraestrutura de conteúdo do System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

Para obter informações sobre a monitorização de tipos de implementação de conteúdos específicos:
-   Para monitorizar Aplicações, veja [Monitorizar aplicações com o System Center Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

-   Para monitorizar Pacotes e Programas, veja Como gerir pacotes e programas   em [Pacotes e programas no System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

**Endpoint Protection**  
   Veja [Como monitorizar o Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md).  

**Monitorizar a Gestão de Energia**  
 Veja [Como monitorizar e planear a gestão de energia no System Center Configuration Manager](../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

**Monitorizar a Medição de Software**  
Veja [Monitorizar a utilização da aplicação com a medição de software no System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

**Monitorizar Atualizações de Software**  
 Ver [monitorizar atualizações de software no System Center Configuration Manager](../../../sum/deploy-use/monitor-software-updates.md).  


##  <a name="BKMK_MonitorInfrastructure"></a> Monitorizar a infraestrutura de hierarquia do Configuration Manager  
O Configuration Manager fornece vários métodos para monitorizar o estado e as operações da sua hierarquia. Pode verificar o estado do sistema de sites de toda a hierarquia, monitorizar a replicação entre sites a partir de uma hierarquia de sites ou uma vista geográfica, monitorizar ligações de replicação entre sites para replicação de bases de dados e utilizar a ferramenta Analisador de Ligações de Replicação para remediar problemas de replicação.  

###  <a name="BKMK_SH_Node"></a> Acerca do nó Hierarquia do Site  
O **hierarquia de sites** nó da **monitorização** área de trabalho fornece uma descrição geral do seu Gestor de configuração de ligações de hierarquia e entre sites. Pode utilizar duas vistas:  

-   **Diagrama de hierarquia**: Esta vista apresenta a hierarquia como um mapa de topologia que foi simplificado para mostrar apenas as informações essenciais.  

-   **Vista geográfica**: Esta vista apresenta os sites num mapa geográfico que mostra as localizações de sites que configurar.  

Utilize o nó **Hierarquia do Site** para monitorizar o estado de funcionamento de cada site e as ligações de replicação entre sites, bem como a relação dos mesmos com fatores externos, como uma localização geográfica.  

Porque o estado do site e entre sites ligar Estado replicar dados do site e de dados não globais, quando se liga a consola do Configuration Manager para um site primário subordinado, não pode ver o estado de site ou uma ligação de outros sites primários ou sites secundários subordinados. Por exemplo, numa hierarquia com múltiplos sites primários, quando a consola do Configuration Manager se liga a um site primário, pode ver o estado de sites secundários subordinados, o site primário e o site de administração central, mas não é possível ver o estado de outros nós da hierarquia abaixo do site de administração central.  

 Utilize o comando **Configurar Definições** para controlar a forma como o ecrã da hierarquia de sites é apresentado. Configurações para o **hierarquia de sites** nó que fizer quando a consola do Configuration Manager está ligada a um site serão replicadas para todos os outros sites.  

#### <a name="hierarchy-diagram"></a>Diagrama de Hierarquia  
 O diagrama da hierarquia apresenta os sites num mapa de topologia. Nesta vista, pode selecionar um site e ver um resumo das mensagens de estado desse site, explorar para ver mensagens de estado e aceder à caixa de diálogo **Propriedades** dos sites.  

 Além disso, pode colocar em pausa o ponteiro do mouse num link de site ou a replicação entre sites para ver o estado de alto nível para esse objeto. Porque o estado da ligação de replicação não é replicado globalmente, numa hierarquia com vários sites primários, tem de ligar a consola do Configuration Manager para o site de administração central para ver os detalhes de ligação de replicação entre todos os sites.  

 As seguintes opções modificam o diagrama da hierarquia:  

-   **Grupos**: Pode configurar o número de sites primários e sites secundários que acionam uma alteração na apresentação do diagrama da hierarquia que combine os sites num único objeto. Quando os sites são combinados num único objeto, verá o número total de sites e um rollup de alto nível de mensagens de estado e estado do site. As configurações de grupos não afetam a vista geográfica.  

-   **Sites Favoritos**: Pode especificar sites individuais como um site favorito. Um ícone de estrela identifica um site favorito no diagrama da hierarquia. Os sites favoritos não são combinados com outros sites quando utiliza grupos e são sempre apresentados individualmente.  

#### <a name="geographical-view"></a>Vista Geográfica  
 A vista geográfica apresenta a localização de cada site num mapa geográfico. Só são apresentados os sites que configurar com uma localização. Quando seleciona um site nesta vista, são apresentadas as ligações de replicação a sites principais ou subordinados. Ao contrário da vista de diagrama da hierarquia, não pode visualizar detalhes de mensagens de estado ou de ligações de replicação do site nesta vista.  

> [!NOTE]  
>  Para utilizar a vista geográfica, o computador ao qual a consola liga o Configuration Manager tem de ter o Internet Explorer instalado e ser capaz de aceder aos mapas Bing utilizando o protocolo HTTP.  

A opção seguinte modifica a vista geográfica.  

-   **Localização do site**: Pode especificar uma localização geográfica para cada site. Pode especificar a localização como uma morada, o nome de um local, o nome de uma cidade por exemplo, ou pelas coordenadas de latitude e longitude. Por exemplo, para utilizar a latitude e longitude de Redmond, Washington, especificaria **N 47 40 26.3572 W 122 7 17.4432** como a localização do site. Não precisa de especificar os símbolos para os graus, minutos ou segundos da longitude e da latitude. O Configuration Manager utiliza o mapas Bing para apresentar a localização na vista geográfica. Isto oferece a opção de visualizar a hierarquia em relação a uma localização geográfica, o que pode fornecer informações aprofundadas sobre problemas regionais que possam afetar sites específicos ou a replicação entre sites.  

     Quando especificar uma localização, pode utilizar a caixa **Localização** para procurar um site específico na hierarquia. Com o site selecionado, introduza a localização como o nome de uma cidade ou morada na coluna **Localização** . O Configuration Manager utiliza o mapas Bing para resolver a localização.  

###  <a name="BKMK_MonitorRepLinksAndStatuss"></a> Como monitorizar ligações de replicação de base de dados e o estado de replicação  
 Além dos detalhes de alto nível acessíveis a partir do nó **Hierarquia do Site** na área de trabalho **Monitorização** . Também pode monitorizar os detalhes de replicação de base de dados quando utiliza o nó **Replicação de Base de Dados** na área de trabalho **Monitorização** . Partir do **replicação de base de dados** , pode monitorizar o estado de ligações de replicação entre sites e os detalhes de inicialização e os detalhes de replicação para grupos de replicação no site ao qual a consola do Configuration Manager está ligado.  

> [!TIP]  
>  Embora também seja apresentado um nó **Replicação de Base de Dados** no nó **Configuração da Hierarquia** da área de trabalho **Administração** , não pode ver o estado da replicação de ligações de replicação de base de dados a partir dessa localização.  

####  <a name="BKMK_MonitorReplicationLinks"></a> Estado da ligação de replicação  
A replicação de base de dados entre sites envolve a replicação de vários conjuntos de informações, denominados grupos de replicação. Cada grupo de replicação é replicado com diferentes prioridades de replicação. Por predefinição, não é possível modificar os dados contidos num grupo de replicação e a frequência da replicação.  

 Quando uma ligação de replicação está ativa e não tem um estado de falha ou degradação, todos os grupos de replicação são replicados atempadamente. Quando a replicação de um ou mais grupos de replicação não é concluída no período de tempo previsto, a ligação é apresentada como degradada. As ligações degradadas podem funcionar, mas deve monitorizá-las para se certificar de que devolvem um estado ativo; caso contrário, investigue-as para assegurar que não ocorre degradação ou falhas de replicação adicionais.  

 Para cada ligação de replicação, pode especificar o número de vezes que um grupo de replicação não replicado com êxito tenta a replicação novamente antes de o estado da ligação ser definido como degradado ou falhado. Mesmo que apenas um grupo de replicação não seja replicado com êxito, o estado da ligação é definido como degradado ou falhado porque um grupo de replicação não concluiu a replicação no número de tentativas especificado. Para obter informações sobre os limiares de replicação, veja a secção [Limiares de Replicação de Base de Dados](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds) em [Transferência de dados entre sites no System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md).  

 Utilize as informações da tabela que se segue para compreender o estado de ligações de replicação que pode exigir investigação adicional.  

|Descrição da ligação|Mais informações|  
|----------------------|----------------------|  
|**A ligação está ativa**|Não foram detetados problemas e existe comunicação através da ligação.|  
|**A ligação está degradada**|A replicação funciona, mas pelo menos um objeto ou grupo de replicação está atrasado. Monitorize as ligações que estejam neste estado e procure nas informações de ambos os sites da ligação indicações de que a ligação poderá falhar.<br /><br /> Uma ligação também pode apresentar um estado degradado quando o site que recebe dados replicados não consegue consolidar rapidamente os dados na base de dados. Isto pode acontecer quando são replicados grandes volumes de dados. Por exemplo, se implementar uma atualização de software em muitos computadores, o site principal da ligação poderá demorar algum tempo a processar o volume de dados que é replicado. Um atraso do processamento no site principal pode fazer com que o estado da ligação seja definido como degradado até o site principal conseguir processar com êxito os dados acumulados.|  
|**A ligação falhou**|A replicação não funciona. É possível que uma ligação de replicação possa recuperar sem qualquer ação adicional. Pode utilizar o Analisador de Ligações de Replicação para investigar e ajudar a remediar uma replicação nesta ligação.<br /><br /> Este estado também pode indicar um problema na rede física entre o site principal e o subordinado na ligação de replicação.|  

 Quando um site principal estiver a ser atualizado para um novo service pack e visualizar o estado da ligação a partir do site subordinado, o estado da ligação será apresentado como ativo. Após a atualização, até o site subordinado ter o mesmo service pack do site principal, o estado da ligação será apresentado como ativo quando visualizado a partir do site principal e como em configuração quando visualizado a partir do site subordinado.  

####  <a name="BKMK_MonitorReplicationStatus"></a> Estado de replicação  
 Pode utilizar o nó **Replicação de Base de Dados** da área de trabalho **Monitorização** para ver o estado da replicação de uma ligação de replicação e ver detalhes sobre a base de dados do site em cada site na ligação de replicação. Também pode ver detalhes sobre grupos de replicação. Para ver detalhes, selecione uma ligação de replicação e, em seguida, selecione o separador adequado para o estado de replicação que pretende visualizar. Seguem-se detalhes sobre os diferentes separadores do estado de replicação.  

 **Resumo**  
 Veja informações de alto nível sobre a replicação de dados de site e dados globais entre os dois sites de uma ligação.  

 Também pode clicar em **Ver relatórios de histórico de tráfego de dados** para ver um relatório que mostra detalhes sobre a largura de banda de rede utilizada pela replicação na ligação de replicação.  

 **Site Principal**  
 Relativamente ao site principal de uma ligação de replicação, veja detalhes sobre a base de dados, incluindo:  

-   Portas da firewall para o SQL Server  

-   Espaço livre em disco  

-   Localizações de ficheiros de base de dados  

-   Certificados  

**Site Subordinado**  
 Relativamente ao site subordinado de uma ligação de replicação, veja detalhes sobre a base de dados, incluindo:  

-   Portas da firewall para o SQL Server  

-   Espaço livre em disco  

-   Localizações de ficheiros de base de dados  

-   Certificados  

**Detalhes da inicialização**    
 Veja o estado de inicialização de grupos de replicação que são replicados através da ligação de replicação. Estas informações podem ajudar a identificar se a inicialização de dados de replicação está em curso ou falhou.  

 Além disso, pode utilizar estas informações para identificar quando um site pode estar no modo de interoperabilidade. Modo de interoperabilidade ocorre quando o site subordinado não executa a mesma versão do Configuration Manager do site principal.  

**Detalhes da replicação**    
 Visualize o estado de replicação para cada grupo de replicação que replica na ligação. Utilize estas informações para ajudar a identificar problemas ou atrasos na replicação de dados específicos e determinar os limiares de replicação de base de dados adequados para essa ligação. Para obter informações sobre os limiares de replicação de base de dados, veja a secção [Limiares de Replicação de Base de Dados](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds) em [Transferência de dados entre sites no System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md).  

> [!TIP]  
>  Os grupos de replicação de dados do site são enviados apenas do site subordinado para o site principal. Os grupos de replicação de dados globais são replicados em ambas as direções.  

###  <a name="BKMK_RLA"></a> Acerca do Analisador de Ligações de Replicação  
 O Configuration Manager inclui **analisador de ligações de replicação** que utilizar para analisar e reparar problemas de replicação. É possível utilizar o Analisador de Ligações de Replicação para remediar falhas da ligação de replicação quando a replicação falha e quando a replicação deixa de funcionar mas ainda não foi reportada como falhada. Pode ser utilizado o analisador de ligações de replicação para remediar problemas de replicação entre os seguintes computadores na hierarquia do Configuration Manager (a direção da falha da replicação não é importante):  

-   Entre um servidor do site e o servidor de base de dados do site.  

-   Entre um servidor de base de dados do site de sites e o computador de base de dados outro site de sites (replicação entre sites).  

Pode executar o analisador de ligações de replicação na consola do Configuration Manager ou num prompt de comando:  

-   Para executar na consola do Configuration Manager: Na **monitorização** área de trabalho, clique no **replicação de base de dados** nó, selecione a ligação de replicação que pretende analisar, e, em seguida, no **replicação de base de dados** grupo sobre o **home page** separador, selecione **analisador de ligações de replicação**.  

-   Para executar uma linha de comandos, escreva o seguinte comando: **%path%\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe &lt;FQDNdoservidordesitedeorigem\> &lt;FQDN do servidor de site de destino\>**  

Quando o Analisador de Ligações de Replicação é executado, deteta problemas através da utilização de um conjunto de regras de diagnóstico e verificações. Quando a ferramenta é executada, é possível ver os problemas que a ferramenta identifica. Quando as instruções para resolver um problema são conhecidas, estas são apresentadas. Se o Analisador de Ligações de Replicação puder remediar automaticamente um problema, essa opção é apresentada. Após a conclusão do analisador de ligações de replicação, este guarda os resultados no seguinte relatório baseado em XML e um ficheiro de registo no ambiente de trabalho do utilizador que executa a ferramenta:  

-   ReplicationAnalysis.xml  

-   ReplicationLinkAnalysis.log  

Quando o Analisador de Ligações de Replicação é executado, para os seguintes serviços enquanto efetua a remediação de alguns problemas e reinicia esses serviços quando a remediação estiver concluída:  

-   SMS_SITE_COMPONENT_MANAGER  

-   SMS_EXECUTIVE  

Se o Analisador de Ligações de Replicação não conseguir concluir a remediação, reveja o servidor do site e reinicie esses serviços caso estejam parados.  

As ações de investigação e de remediação bem-sucedidas e falhadas são registadas para fornecer detalhes adicionais que não são apresentados na interface da ferramenta.  

**Pré-requisitos para utilizar o Analisador de Ligações de Replicação:**  

-   A conta utilizada para executar o Analisador de Ligações de Replicação deve ter direitos de administrador local em cada computador que esteja envolvido na ligação de replicação. A conta não necessita de uma função de segurança da administração baseada em funções específicas. Por conseguinte, um utilizador administrativo com acesso para o **replicação de base de dados** nó pode executar a ferramenta na consola do Configuration Manager ou um administrador de sistema com direitos suficientes em cada computador pode executar a ferramenta num comando linha de comandos.  

-   A conta utilizada para executar o Analisador de Ligações de Replicação tem de ter direitos de administrador do sistema em cada base de dados do SQL Server que esteja envolvida na ligação de replicação.  

**Problemas conhecidos do Analisador de Ligações de Replicação:**  

-   Com o lançamento do System Center Configuration Manager versão 1511, o analisador de ligações de replicação gera erros de certificado do SQL Server Service Broker para sites primários atualizados a partir do System Center 2012 Configuration Manager. Isso é devido a alterações nos nomes dos certificados introduzidos com a versão 1511 para o qual o analisador de ligações de replicação ainda não tenha sido atualizado. Estes erros podem ser ignorados com segurança.  

###  <a name="BKMK_ProcsforMonitoringReplication"></a> Procedimentos para monitorizar a replicação de base de dados  

##### <a name="to-monitor-high-level-site-to-site-database-replication-status"></a>Para monitorizar o estado de replicação de alto nível base de dados do site a site    
1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na área de trabalho **Monitorização** , clique em **Hierarquia do Site** para abrir a vista **Diagrama da Hierarquia** .  

3.  Coloque brevemente o ponteiro do rato sobre a linha entre os dois sites para ver o estado da replicação de dados global e de site para estes sites.  

##### <a name="to-monitor-the-replication-status-for-a-replication-link"></a>Para monitorizar o estado de replicação para uma ligação de replicação    
1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na área de trabalho **Monitorização** , clique em **Replicação de Base de Dados**e selecione a ligação de replicação para a ligação que pretende monitorizar. Em seguida, na área de trabalho, selecione o separador adequado para ver outros detalhes do estado de replicação dessa ligação.  

---
title: Lista de verificação para 1810
titleSuffix: Configuration Manager
description: Saiba mais sobre as ações a efetuar antes de atualizar para o Configuration Manager versão 1810.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b87ac054-9b37-4725-a3f3-2340cfb10bff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: efce5242c5de148d6922144af27f47a267b3c6c3
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52458332"
---
# <a name="checklist-for-installing-update-1810-for-configuration-manager"></a>Lista de verificação para instalar a atualização 1810 para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando utiliza o ramo atual do Configuration Manager, pode instalar a atualização na consola para a versão 1810 para atualizar a sua hierarquia de uma versão anterior. <!-- baseline only statement: (Because version 1802 is also available as [baseline media](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions), you can use the installation media to install the first site of a new hierarchy.)-->

Para obter a atualização de versão 1810, tem de utilizar um ponto de ligação de serviço no site de nível superior da sua hierarquia. Esta função de sistema de sites pode estar no modo online ou offline. Depois da hierarquia transfere o pacote de atualização da Microsoft, encontrá-lo na consola do. Na **Administration** área de trabalho, selecione a **atualizações e manutenção** nó.

-   Quando a atualização é listada como **disponível**, está pronta para instalar a atualização. Antes de instalar a versão 1810, reveja as seguintes informações [sobre a instalação da atualização 1810](#about-installing-update-1810) e o [lista de verificação](#checklist) para configurações de fazer antes de iniciar a atualização.

-   Se a atualização indicará **transferir** e não alterar, reveja o **hman. log** e **dmpdownloader. log** erros.

    -   O dmpdownloader. log pode indicar que o processo de dmpdownloader está a aguardar um intervalo antes de a verificação de atualizações. Para reiniciar o download dos arquivos de redistribuição da atualização, reinicie o **SMS_Executive** serviço no servidor do site.

    -   Outro problema comum de download ocorre quando transferências a partir de impedir que as definições do servidor proxy http://silverlight.dlservice.microsoft.com e http://download.microsoft.com.

Para obter mais informações sobre como instalar atualizações, consulte [atualizações e manutenção na consola](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Para obter mais informações sobre as versões atuais do ramo, consulte [versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines).



## <a name="about-installing-update-1810"></a>Sobre a instalação de atualização 1810

#### <a name="sites"></a>Sites
Instalar atualização 1810 no site de nível superior da sua hierarquia. Inicie a instalação do seu site de administração central ou a partir de seu site primário autónomo. Após a atualização é instalada no site de nível superior, os sites subordinados têm o seguinte comportamento de atualização:

-   Os sites primários subordinados instalam a atualização automaticamente depois do site de administração central concluir a instalação da atualização. Pode utilizar janelas de serviço para controlar quando um site instala a atualização. Para obter mais informações, consulte [manutenção do windows para servidores de site](/sccm/core/servers/manage/service-windows).

-   Atualize manualmente cada site secundário a partir da consola do Configuration Manager depois do site principal primário concluir a instalação da atualização. Não é suportada a atualização automática de servidores de site secundário.

#### <a name="site-system-roles"></a>Funções do sistema de sites
Quando um servidor do site instala a atualização, ele atualiza automaticamente todas as funções de sistema do site. Estas funções são no servidor do site ou instalado em servidores remotos. Antes de instalar a atualização, certifique-se de que cada servidor de sistema de sites cumpre os pré-requisitos atuais para a nova versão de atualização.

#### <a name="configuration-manager-consoles"></a>Consolas do Configuration Manager   
Na primeira vez que utiliza uma consola do Configuration Manager após a atualização foi concluída, lhe for pedido que Atualize a consola. Também pode executar a configuração do Configuration Manager no computador que aloja a consola e escolha a opção para atualizar a consola. Instale a atualização para o console logo que possível. Para obter mais informações, consulte [instalar a consola do Configuration Manager](/sccm/core/servers/deploy/install/install-consoles).

> [!IMPORTANT]  
> Quando instala uma atualização no site de administração central, tenha em atenção as seguintes limitações e atrasos que existem até que todos os sites primários subordinados também concluir a instalação da atualização:    
> - **As atualizações de cliente** não iniciar. Isto inclui as atualizações automáticas de clientes e clientes de pré-produção. Além disso, não é possível promover clientes de pré-produção para produção até que o último site seja concluída a instalação da atualização. Após o site última concluir a instalação da atualização, as atualizações de cliente serão iniciada com base em suas opções de configuração.   
> - **Novos recursos** ativa com a atualização não estão disponíveis. Este procedimento impede que a replicação de dados relacionados com essa funcionalidade sejam enviados para um site que ainda não instalou o suporte para essa funcionalidade. Afinal de contas, os sites primários instalar a atualização, a funcionalidade estará disponível para utilização.   
> - **Ligações de replicação** entre o site de administração central e filho sites primários são apresentadas como não atualizada. Isto apresenta no estado de instalação do pacote de atualização como estado concluído com aviso para a inicialização da replicação de monitorização. No nó de monitorização da consola, isso indicará *ligação está a ser configurada*.


## <a name="checklist"></a>Lista de verificação

#### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>Todos os sites executam uma versão suportada do Configuration Manager  
Cada servidor do site na hierarquia tem de executar a mesma versão do Configuration Manager antes de começar a instalação de atualização 1810. Para atualizar para 1810, tem de utilizar a versão 1710, 1802 ou 1806.

#### <a name="review-the-status-of-your-product-licensing"></a>Rever o estado do seu Licenciamento do produto 
Tem de ter um contrato de Software Assurance (SA) ativo ou direitos de subscrição equivalente para instalar esta atualização. Quando atualizar o site, o **Licensing** página apresenta a opção para confirmar sua **data de expiração do Software Assurance**.

Este valor é opcional. Pode especificar como um lembrete conveniente da data de validade de licença. Esta data é visível quando instalar atualizações futuras. Este valor já pode ter anteriormente especificado durante a configuração ou instalação de uma atualização. Também pode especificar este valor na consola do Configuration Manager. Na **Administration** área de trabalho, expanda **configuração do Site**e selecione **Sites**. Clique em **definições de hierarquia** no Friso e, mude para o **licenciamento** separador.

Para obter mais informações, consulte [licenciamento e ramificações](/sccm/core/understand/learn-more-editions).

#### <a name="review-microsoft-net-versions"></a>Reveja as versões de .NET da Microsoft 
Quando um site instala esta atualização, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Quando este pré-requisito já não estiver instalado, a instalação do site-lo em cada servidor que aloja uma das seguintes funções do sistema de sites:

-   Ponto de gestão
-   Ponto de ligação de serviço
-   Ponto proxy de registo
-   Ponto de inscrição

Esta instalação pode colocar o servidor de sistema de sites num reinício pendente estado e o relatório de erros para o Visualizador de estado do componente do Configuration Manager. Além disso, as aplicações de .NET no servidor de podem ocorrer falhas aleatórias até que o servidor seja reiniciado.

Para obter mais informações, consulte [Site e pré-requisitos de sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

#### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>Consultar a versão do Windows ADK para Windows 10
Deve ser suportada a versão do Windows 10 Assessment and Deployment Kit (ADK) para 1810 de versão do Configuration Manager. Para obter mais informações sobre as versões suportadas do Windows ADK, consulte [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk). Se precisar de atualizar o Windows ADK, faça-o antes de iniciar a atualização do Configuration Manager. Esta ordem torna-se de que as imagens de arranque predefinidas são automaticamente atualizadas para a versão mais recente do Windows PE. Quaisquer imagens de arranque personalizadas de atualizar manualmente depois de atualizar o site.

Se atualizar o site antes de atualizar o Windows ADK, consulte [atualizar pontos de distribuição com a imagem de arranque](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image).

#### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>Analise o estado do site e da hierarquia para problemas por resolver 
Uma atualização de site pode falhar devido a problemas operacionais existentes. Antes de atualizar um site, resolva todos os problemas operacionais para os seguintes sistemas:  
- O servidor do site  
- O servidor de base de dados do site  
- Funções do sistema de sites remoto em outros servidores   

Para obter mais informações, consulte [utilizar alertas e o estado do sistema](/sccm/core/servers/manage/use-alerts-and-the-status-system).

#### <a name="review-file-and-data-replication-between-sites"></a>Rever a replicação de ficheiros e dados entre sites   
Certificar-se de que esse ficheiro e replicação de base de dados entre sites está operacional e atualizada. Atrasos ou registos de segurança em qualquer um podem impedir que uma atualização uniforme e bem-sucedida. Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização.

Para obter mais informações, consulte [sobre o analisador de ligações de replicação](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA).

#### <a name="install-all-applicable-critical-windows-updates"></a>Instalar todas as atualizações críticas aplicáveis a Windows
Antes de instalar uma atualização para o Configuration Manager, instale quaisquer atualizações críticas do sistema operacional para cada sistema de sites aplicável. Esses servidores incluem o servidor do site, servidor de base de dados do site e funções de sistema de sites remoto. Se uma atualização que instalar necessitar de um reinício, reinicie os servidores de aplicáveis antes de iniciar a atualização.

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Desativar réplicas de base de dados para pontos de gestão em sites primários   
O Configuration Manager não é possível atualizar com êxito um site primário que tenha uma réplica de base de dados para pontos de gestão ativada. Antes de instalar uma atualização para o Configuration Manager, desative a replicação de base de dados.

Para obter mais informações, consulte [réplicas para pontos de gestão de base de dados](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

#### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>Conjunto de grupos de Disponibilidade AlwaysOn do SQL Server para ativação pós-falha manual   
Se utilizar um grupo de disponibilidade, certifique-se de que o grupo de disponibilidade está definido para ativação pós-falha manual antes de iniciar a instalação da atualização. Depois do site tem de ser atualizado, pode restaurar a ativação pós-falha para ser automática. Para obter mais informações, consulte [SQL Server AlwaysOn para uma base de dados do site](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

#### <a name="disable-site-maintenance-tasks-at-each-site"></a>Desativar tarefas de manutenção do site em cada site
Antes de instalar a atualização, desative as tarefas de manutenção do site que possam ser executadas durante o tempo que o processo de atualização estiver ativo. Por exemplo, mas não limitado a:

-   Servidor do Site de Reserva
-   Eliminar Operações de Cliente Desatualizadas
-   Eliminar Dados de Deteção Desatualizados

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desativar uma tarefa, registe o agendamento da tarefa para que possa restaurar a respetiva configuração após a atualização foi instalada.

Para obter mais informações, consulte [tarefas de manutenção](/sccm/core/servers/manage/maintenance-tasks) e [referência das tarefas de manutenção de](/sccm/core/servers/manage/reference-for-maintenance-tasks).

#### <a name="temporarily-stop-any-antivirus-software"></a>Parar temporariamente a qualquer software antivírus 
Antes de atualizar um site, pare o software antivírus em servidores do Configuration Manager. <!--SMS.503481--> 

#### <a name="create-a-backup-of-the-site-database"></a>Criar uma cópia de segurança da base de dados do site 
Antes de atualizar um site, criar cópias de segurança da base de dados do site no site de administração central e sites primários. Esta cópia de segurança torna-se de que tem uma cópia de segurança para recuperação após desastre.

Para obter mais informações, consulte [cópia de segurança e recuperação](/sccm/protect/understand/backup-and-recovery).

#### <a name="plan-for-client-piloting"></a>Plano para a criação de pilotos de cliente   
Quando instala uma atualização que atualiza o cliente, pode testar essa nova atualização de cliente em pré-produção antes de implementar e atualizar todos os clientes ativos. Para tirar partido desta opção, tem de configurar o seu site para suportar as atualizações automáticas para pré-produção antes de iniciar a instalação da atualização.

Para obter mais informações, consulte [atualizar os clientes](/sccm/core/clients/manage/upgrade/upgrade-clients) e [como testar as atualizações de cliente numa coleção de pré-produção](/sccm/core/clients/manage/upgrade/test-client-upgrades).

#### <a name="plan-to-use-service-windows"></a>Planear a utilização de janelas de serviço   
Para definir um período durante as atualizações a um site de servidor de pode ser instalado, utilize as janelas de serviço. Eles podem ajudar a controlar quando os sites na hierarquia instalam a atualização. Para obter mais informações, consulte [manutenção do windows para servidores de site](/sccm/core/servers/manage/service-windows).

#### <a name="review-supported-extensions"></a>Extensões de revisão suportado
<!--SCCMdocs#587--> Se expandir o Configuration Manager com outros produtos da Microsoft ou Microsoft parceiros, confirme que esses produtos oferecem suporte a versão 1810. Contacte o fornecedor de produto para obter estas informações. Por exemplo, consulte o Microsoft Deployment Toolkit [notas de versão](/sccm/mdt/release-notes).

#### <a name="run-the-setup-prerequisite-checker"></a>Executar o Verificador de pré-requisitos de configuração   
Quando a atualização é listada na consola do como **disponível,** independente pode executar o Verificador de pré-requisitos antes de instalar a atualização. (Quando instalar a atualização no site, verificador de pré-requisitos é executado novamente.)

Para executar uma verificação de pré-requisitos a partir da consola, vá para o **Administration** área de trabalho e selecione **atualizações e manutenção**. Selecione o **Configuration Manager 1810** pacote de atualização e clique em **executar verificação de pré-requisitos** na faixa de opções.

Para obter mais informações, consulte a secção para **executar o Verificador de pré-requisitos antes de instalar uma atualização** na [antes de instalar uma atualização na consola](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall).

> [!IMPORTANT]  
> Quando o Verificador de pré-requisitos é executado, o processo atualiza alguns ficheiros de origem do produto que são utilizados para tarefas de manutenção do site. Portanto, depois de executar o Verificador de pré-requisitos, mas antes de instalar a atualização, se tiver de realizar uma tarefa de manutenção do site, execute **Setupwpf.exe** (configuração do Configuration Manager) partir do CD. Pasta mais recente no servidor do site.

#### <a name="update-sites"></a>Atualizar sites   
Agora, está pronto para iniciar a instalação da atualização para a sua hierarquia. Para obter mais informações sobre como instalar a atualização, consulte [instalar atualizações na consola](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

Planeia instalar a atualização fora do horário comercial normal. Determine quando o processo terá o mínimo efeito nas suas operações comerciais. Instalar a atualização e as respetivas ações reinstalar os componentes do site e funções de sistema de sites.

Para obter mais informações, consulte [atualizações do Configuration Manager](/sccm/core/servers/manage/updates).



## <a name="post-update-checklist"></a>Lista de verificação de pós-atualização

Depois do site atualiza, utilize a lista de verificação seguinte para concluir tarefas e configurações comuns.


#### <a name="confirm-version-and-restart-if-necessary"></a>Confirmar a versão e reiniciar (se necessário)
Certifique-se de que cada servidor do site e a função do sistema de sites foi atualizado para versão 1810. Na consola, adicione a **versão** coluna para o **Sites** e **pontos de distribuição** nós o **administração** área de trabalho. Quando for necessário, uma função de sistema do site reinstala automaticamente ao atualizar para a nova versão. 

Considere reiniciar os sistemas de site remoto que não foi atualizado com êxito à primeira. Reveja a infraestrutura de sites e certifique-se de que servidores do site aplicáveis e os servidores de sistema de sites remoto reiniciaram com êxito. Normalmente, os servidores do site reinicie apenas quando o Configuration Manager instala .NET como um pré-requisito para uma função de sistema de sites.


#### <a name="confirm-site-to-site-replication-is-active"></a>Confirmar a replicação de site a site está ativa
Na consola do Configuration Manager, aceda às localizações seguintes para ver o estado e certifique-se de que a replicação está ativa:  

-   **Monitorização** área de trabalho **hierarquia do Site** nó  

-   **Monitorização** área de trabalho **replicação de base de dados** nó  

Para obter mais informações, consulte os artigos seguintes:  
- [Monitorizar a infraestrutura de hierarquia e replicação](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure)
- [Acerca do Analisador de Ligações de Replicação](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA)  


#### <a name="update-configuration-manager-consoles"></a>Atualizar consolas do Configuration Manager
Atualize todas as consolas remotas do Configuration Manager para a mesma versão. Lhe for pedido para atualizar a consola quando:  

-   Abra a consola.  

-   Ir para um novo nó na consola do.  


#### <a name="reconfigure-database-replicas-for-management-points"></a>Reconfigurar réplicas de base de dados para pontos de gestão
Depois de atualizar um site primário, reconfigure a réplica de base de dados para pontos de gestão que foram desinstaladas antes da atualização do site. Para obter mais informações, consulte [réplicas para pontos de gestão de base de dados](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  


#### <a name="reconfigure-any-disabled-maintenance-tasks"></a>Reconfigure as tarefas de manutenção desativado
Se tiver desativado a base de dados [tarefas de manutenção](/sccm/core/servers/manage/maintenance-tasks) num site antes de instalar a atualização, reconfigure essas tarefas. Utilize as definições que se encontravam em vigor antes da atualização.  


#### <a name="update-clients"></a>Atualizar clientes
Atualize clientes com o plano que criou, especialmente se tiver configurado um piloto antes de instalar a atualização do cliente. Para obter mais informações, consulte [como atualizar clientes para computadores Windows](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers).  


#### <a name="third-party-extensions"></a>Extensões de terceiros
Se utilizar quaisquer extensões para o Configuration Manager, atualizá-los para a versão mais recente para suportar 1810 de versão do Configuration Manager. 


#### <a name="update-custom-boot-images-and-media"></a>Atualizar imagens de arranque personalizadas e suporte de dados
<!--SCCMDocs issue 775-->

Utilizar o **atualizar pontos de distribuição** ação para qualquer imagem de arranque que utiliza, quer se trate de um padrão ou a imagem de arranque personalizada. Esta ação torna-se de que os clientes podem utilizar a versão mais recente. Mesmo se não existir uma nova versão do Windows ADK, os componentes do cliente do Configuration Manager podem ser alterados com uma atualização. Se não os atualizar imagens de arranque e suportes de dados, as implementações de sequência de tarefas podem falhar em dispositivos. 

Quando atualizar o site, o Configuration Manager atualiza automaticamente os *predefinição* imagens de arranque. Não distribuir automaticamente o conteúdo atualizado a pontos de distribuição. Utilize o **atualizar pontos de distribuição** ação nas imagens de arranque específica quando estiver pronto para distribuir esse conteúdo na sua rede. 

Depois de atualizar o site, atualizar manualmente qualquer *personalizado* imagens de arranque. Esta ação atualiza a imagem de arranque com os componentes de cliente mais recente, se necessário, opcionalmente, recarrega-lo com a versão atual do Windows PE e redistribui o conteúdo aos pontos de distribuição. 

Para obter mais informações, consulte [atualizar pontos de distribuição com a imagem de arranque](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image). 
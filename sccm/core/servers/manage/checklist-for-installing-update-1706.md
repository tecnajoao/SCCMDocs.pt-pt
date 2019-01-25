---
title: Lista de verificação para 1706
titleSuffix: Configuration Manager
description: Saiba mais sobre as ações a efetuar antes de atualizar para o System Center Configuration Manager versão 1706.
ms.date: 12/19/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7def067e-845c-4db3-9d56-fa1dcf2fd7c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 004ac9fa331b4e698ae9ad3699c8d717b1d95a3e
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897666"
---
# <a name="checklist-for-installing-update-1706-for-system-center-configuration-manager"></a>Lista de verificação para instalar a atualização 1706 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando utiliza o ramo atual do System Center Configuration Manager, pode instalar a atualização na consola para a versão 1706 para atualizar a sua hierarquia de uma versão anterior.

Para obter a atualização de versão 1706, tem de utilizar uma função de sistema de sites de ponto de ligação de serviço no site de nível superior da sua hierarquia. Isso pode ser no modo online ou offline. Depois da hierarquia transfere o pacote de atualização da Microsoft, pode encontrá-lo na consola em **Administration &gt; descrição geral &gt; serviços Cloud &gt; atualizações e manutenção**.

-   Quando a atualização é listada como **disponível**, está pronta para instalar a atualização. Antes de instalar a versão 1706, reveja as seguintes informações [sobre como instalar a atualização 1706](#about-installing-update-1706) e o [lista de verificação](#checklist) para configurações de fazer antes de iniciar a atualização.

-   Se a atualização indicará **transferir** e não alterar, reveja o **hman. log** e **dmpdownloader. log** erros.

    -   Se o dmpdownloader. log indica o processo de dmpdownloader está em modo de suspensão e aguardar por um intervalo antes de a verificação de atualizações, pode reiniciar o **SMS_Executive** serviço no servidor do site para reiniciar o download da atualização ficheiros de redistribuição.

    -   Outro problema comum de download ocorre quando transferências a partir de impedir que as definições do servidor proxy <http://silverlight.dlservice.microsoft.com> e <http://download.microsoft.com>.

Para obter mais informações sobre como instalar atualizações, consulte [atualizações e manutenção na consola](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Para obter informações sobre as versões do ramo atual, consulte [versões de linha de base e de atualização](/sccm/core/servers/manage/updates#bkmk_Baselines) na [atualiza para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="about-installing-update-1706"></a>Sobre como instalar a atualização 1706

**Sites:**  
Instalar a atualização 1706 no site de nível superior da sua hierarquia. Isto significa que inicia a instalação do seu site de administração central, se tiver uma, ou a partir de seu site primário autónomo. Após a atualização é instalada no site de nível superior, os sites subordinados têm o seguinte comportamento de atualização:

-   Os sites primários subordinados instalam a atualização automaticamente depois do site de administração central concluir a instalação da atualização. Pode utilizar janelas de serviço para controlar quando um site instala a atualização. Para obter mais informações, consulte [manutenção do windows para servidores de site](/sccm/core/servers/manage/service-windows).

-   Tem de atualizar manualmente cada site secundário a partir da consola do Configuration Manager depois do site principal primário concluir a instalação da atualização. A atualização automática dos servidores de site secundários não é suportada.

**Funções de sistema de sites:**  
Quando um servidor do site instala a atualização, as funções de sistema de sites que estão instaladas no computador do servidor do site e que estão instalados em computadores remotos, automaticamente atualizadas. Antes de instalar a atualização, certifique-se de que cada servidor de sistema de sites cumpre os pré-requisitos para a operação com a nova versão de atualização.

**Consolas do Configuration Manager:**   
Na primeira vez que utiliza uma consola do Configuration Manager após a atualização foi concluída, será solicitado que Atualize a consola. Para fazer isso, tem de executar a configuração do Configuration Manager no computador que aloja a consola e, em seguida, escolha a opção para atualizar a consola. Recomendamos que não adie a instalação da atualização na consola.

> [!IMPORTANT]  
> Quando instala uma atualização no site de administração central, tenha em atenção as seguintes limitações e atrasos que existem até que todos os sites primários subordinados também concluir a instalação da atualização:    
> - **As atualizações de cliente** não iniciar. Isto inclui as atualizações automáticas de clientes e clientes de pré-produção. Além disso, não é possível promover clientes de pré-produção para produção até que o último site seja concluída a instalação da atualização. Após o site última concluir a instalação da atualização, as atualizações de cliente serão iniciada com base em suas opções de configuração.   
> - **Novos recursos** ativa com a atualização não estão disponíveis. Este procedimento impede que a replicação de dados relacionados com essa funcionalidade sejam enviados para um site que ainda não instalou o suporte para essa funcionalidade. Afinal de contas, os sites primários instalar a atualização, a funcionalidade estará disponível para utilização.   
> - **Ligações de replicação** entre o site de administração central e filho sites primários são apresentadas como não atualizada. Isto apresenta no estado de instalação do pacote de atualização como estado concluído com aviso para a inicialização da replicação de monitorização. No nó de monitorização da consola, isso indicará *ligação está a ser configurada*.


## <a name="checklist"></a>Lista de verificação

**Certifique-se de que todos os sites executam uma versão do System Center Configuration Manager que suporta atualizações para 1706:**   
Cada servidor do site na hierarquia tem de executar a mesma versão do System Center Configuration Manager antes de começar a instalação de atualização 1706. Para atualizar para 1706, tem de utilizar a versão 1606, 1610 ou 1702.

**Rever o estado do seu Software Assurance ou ter direitos equivalentes de subscrição:**   
Tem de ter um contrato de Software Assurance (SA) ativo para instalar a atualização 1706. Ao instalar esta atualização, o **Licensing** separador apresenta a opção para confirmar sua **data de expiração do Software Assurance**.

Este é um valor opcional que pode ser especificado como um lembrete conveniente da data de validade de licença. Esta data é visível quando instalar atualizações futuras. Pode ter especificado anteriormente este valor durante a configuração ou instalação de uma atualização ou utilizando o **Licensing** separador da **definições de hierarquia**, da consola do Configuration Manager.

Para obter mais informações, consulte [ramificações para o System Center Configuration Manager e de licenciamento](/sccm/core/understand/learn-more-editions).

**Rever instaladas as versões de Microsoft .NET nos servidores do sistema de sites:**  Quando um site instala esta atualização, o Configuration Manager instala automaticamente o .NET Framework 4.5.2 em cada computador que aloja uma das seguintes funções do sistema de site quando o .NET Framework 4.5 ou posterior ainda não estiver instalado:

-   Ponto proxy de registo
-   Ponto de inscrição
-   Ponto de gestão
-   Ponto de ligação de serviço

Esta instalação pode colocar o servidor de sistema de sites num reinício pendente estado e o relatório de erros para o Visualizador de estado do componente do Configuration Manager. Além disso, as aplicações de .NET no servidor de podem ocorrer falhas aleatórias até que o servidor seja reiniciado.

Para obter mais informações, consulte [Site e pré-requisitos de sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

**Consultar a versão do Windows Assessment and Deployment Kit (ADK) para o Windows 10** o Windows 10 ADK deve ser a versão 1703 ou posterior. (Para obter mais informações sobre as versões suportadas do Windows ADK, consulte [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).) Se tem de atualizar o Windows ADK, faça-o antes de iniciar a atualização do Configuration Manager. Isto garante que as imagens de arranque predefinidas são automaticamente atualizadas para a versão mais recente do Windows PE. (Imagens de arranque personalizadas têm de ser atualizadas manualmente.)

Se atualizar o site antes de atualizar o Windows ADK, consulte [atualizar pontos de distribuição com a imagem de arranque](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image) aprimoramentos para este processo na versão 1706 de versão do Configuration Manager.

**Analise o estado do site e da hierarquia e certifique-se de que não existem não existem problemas por resolver:**  Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, o servidor de base de dados do site e funções de sistema de sites que são instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.

Para obter mais informações, consulte [utilizar alertas e o estado do sistema do System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system).

**Reveja os replicação de ficheiros e dados entre sites:**   
Certifique-se esse ficheiro e a replicação de base de dados entre sites está operacional e atualizada. Atrasos ou registos de segurança em qualquer um podem impedir que uma atualização uniforme e bem-sucedida.
Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização.

Para obter mais informações, consulte [sobre o analisador de ligações de replicação](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) no [monitorizar a infraestrutura hierarquia e replicação no System Center Configuration Manager](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure)   tópico.

**Instale todas as atualizações críticas aplicáveis para sistemas operativos em computadores que alojam o site, o servidor de base de dados do site e funções de sistema de sites remoto:**  Antes de instalar uma atualização para o Configuration Manager, instale quaisquer atualizações críticas para cada sistema de sites aplicável. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização.

**Desative réplicas de base de dados para pontos de gestão em sites primários:**   
O Configuration Manager não é possível atualizar com êxito um site primário que tenha uma réplica de base de dados para pontos de gestão ativada. Desative a replicação de base de dados antes de instalar uma atualização para o Configuration Manager.

Para obter mais informações, veja [Réplicas de bases de dados para pontos de gestão do System Center Configuration Manager](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

**Definir grupos de Disponibilidade AlwaysOn do SQL Server para ativação pós-falha manual:**   
Se utilizar um grupo de disponibilidade, certifique-se de que o grupo de disponibilidade está definido para ativação pós-falha manual antes de iniciar a instalação da atualização. Depois do site tem de ser atualizado, pode restaurar a ativação pós-falha para ser automática. Para obter mais informações, consulte [SQL Server AlwaysOn para uma base de dados do site](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

**Reconfigure os pontos de atualização de software que utilizem NLB:**   
O Configuration Manager não é possível atualizar um site que utiliza uma cluster (NLB) para alojar pontos de atualização de software de balanceamento de carga de rede.

Se utilizar NLB clusters para pontos de atualização de software, utilize o Windows PowerShell para remover o cluster NLB.
Para obter mais informações, consulte [planear atualizações de software no System Center Configuration Manager](/sccm/sum/plan-design/plan-for-software-updates).

**Desative todas as tarefas de manutenção do site em cada site durante a instalação da atualização nesse site:**   
Antes de instalar a atualização, desative as tarefas de manutenção do site que possam ser executadas durante o tempo que o processo de atualização estiver ativo. Estas incluem as seguintes, entre outras:

-   Servidor do Site de Reserva
-   Eliminar Operações de Cliente Desatualizadas
-   Eliminar Dados de Deteção Desatualizados

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desativar uma tarefa, registe o agendamento da tarefa para que possa restaurar a respetiva configuração após a atualização foi instalada.

Para obter mais informações, consulte [tarefas de manutenção para o System Center Configuration Manager](/sccm/core/servers/manage/maintenance-tasks) e [tarefas de manutenção para o System Center Configuration Manager](/sccm/core/servers/manage/reference-for-maintenance-tasks).

**Pare temporariamente a qualquer software antivírus em servidores do System Center Configuration Manager:** Antes de atualizar um site, certifique-se de que parou o software antivírus em servidores do Configuration Manager. <!--SMS.503481--> 

**Crie uma cópia de segurança da base de dados do site no site de administração central e sites primários:**  Antes de atualizar um site, criar cópias de segurança da base de dados do site para se certificar de que tem uma cópia de segurança para recuperação após desastre.

Para obter mais informações, consulte [cópia de segurança e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

**Planear a criação de pilotos de cliente:**   
Quando instala uma atualização que atualiza o cliente, pode testar essa nova atualização de cliente em pré-produção antes de implementar e atualizar todos os clientes ativos.

Para tirar partido desta opção, tem de configurar o seu site para suportar as atualizações automáticas para pré-produção antes de iniciar a instalação da atualização.

Para obter mais informações, consulte [atualizar os clientes no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients) e [como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/test-client-upgrades).

**Planear a utilização de janelas de serviço para controlar quando os servidores do site instalam atualizações:**   
Utilize janelas de serviço para definir um período durante as atualizações a um site de servidor de pode ser instalado.

Isto pode ajudar a controlar quando os sites na hierarquia instalam a atualização. Para obter mais informações, consulte [manutenção do windows para servidores de site](/sccm/core/servers/manage/service-windows).

**Execute o Verificador de pré-requisitos de configuração:**   
Quando a atualização é listada na consola do como **disponível,** independente pode executar o Verificador de pré-requisitos antes de instalar a atualização. (Quando instalar a atualização no site, verificador de pré-requisitos é executado novamente.)

Para executar uma verificação de pré-requisitos a partir da consola, aceda a **administração > Descrição geral > Serviços Cloud > atualizações e manutenção.** Em seguida, clique com botão direito **pacote de atualização do Configuration Manager 1706**e, em seguida, escolha **executar verificação de pré-requisitos**.

Para obter mais informações sobre como iniciar e, em seguida, monitorizar a verificação de pré-requisitos, consulte **passo 3: Executar o Verificador de pré-requisitos antes de instalar uma atualização** no tópico [instalar atualizações na consola do System Center Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

> [!IMPORTANT]  
> Quando o Verificador de pré-requisitos é executado independentemente ou como parte de uma instalação de atualização, o processo atualiza alguns ficheiros de origem do produto que são utilizados para tarefas de manutenção do site. Portanto, depois de executar o Verificador de pré-requisitos, mas antes de instalar a atualização, se tiver de realizar uma tarefa de manutenção do site, execute **Setupwpf.exe** (configuração do Configuration Manager) partir do CD. Pasta mais recente no servidor do site.

**Atualizar sites:**   
Agora está pronto para iniciar a instalação de atualização para a sua hierarquia. Para obter mais informações sobre como instalar a atualização, consulte [instalar atualizações na consola.](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)

Recomendamos que planeie instalar a atualização fora do horário comercial normal para cada site quando o processo de instalação da atualização e respetivas ações para reinstalar os componentes do site e as funções de sistema de sites irão ter o mínimo efeito nas operações comerciais.

Para obter mais informações, consulte [atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="post-update-checklist"></a>Lista de verificação de atualização de postagem
Reveja as seguintes ações a efetuar depois de concluída a instalação da atualização.
1. Certifique-se de que a replicação de site a site está ativa. Na consola, ver **monitorização** > **hierarquia do Site**, e **monitorização** > **replicação de base de dados**indicações de problemas e confirmação de que as ligações de replicação estão ativas.
2. Certifique-se de que cada servidor do site e a função do sistema de sites foi atualizado para versão 1706. Na consola, pode adicionar a coluna opcional **versão** para a apresentação de alguns nós incluindo **Sites** e **pontos de distribuição**.

   Quando for necessário, uma função de sistema de sites irá reinstalar automaticamente ao atualizar para a nova versão. Considere reiniciar os sistemas de site remoto que não atualizar com êxito.
3. Reconfigure réplicas de base de dados para pontos de gestão em sites primários que desativou antes de iniciar a atualização.
4. Reconfigure tarefas de manutenção de base de dados que desativou antes de iniciar a atualização.
5. Se tiver configurado um piloto antes de instalar a atualização de cliente, atualize os clientes com o plano que criou.

## <a name="known-issues"></a>Problemas conhecidos 
Depois de atualizar para versão 1706, sempre que o SMS_Executive começa a seguinte mensagem de estado de aviso é criado pelo SMS_CERTIFICATE_MANAGER:
-    Microsoft SQL Server relatou gravidade 515, da mensagem do SQL 16: [23000] [515] [Microsoft] [SQL Server Native Client 11.0][SQL] [SQL Server] não é possível inserir o valor NULL na coluna "RowVersion", tabela 'CM_GF1.dbo.AAD_SecretChange_Notify'; coluna não permite valores NULL. Falha de INSERT.

Esta mensagem pode ser ignorada.  Isso ocorre quando não existem serviços cloud foram configurados para utilização antes de atualizar para a versão 1706. Este problema será resolvido numa versão futura.

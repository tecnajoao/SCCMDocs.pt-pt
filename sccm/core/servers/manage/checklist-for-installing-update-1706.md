---
title: "Lista de verificação para 1706"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as ações a efetuar antes de atualizar o System Center Configuration Manager versão 1706."
ms.custom: na
ms.date: 07/31/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7def067e-845c-4db3-9d56-fa1dcf2fd7c7
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8bfaef2b19449cf6fe1487b32cffcdb5731f1602
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="checklist-for-installing-update-1706-for-system-center-configuration-manager"></a>Lista de verificação para instalar a atualização 1706 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando utiliza o ramo atual do System Center Configuration Manager, pode instalar a atualização na consola para a versão 1706 ao atualizar a sua hierarquia de uma versão anterior.

Para obter a atualização para a versão 1706, tem de utilizar uma função de sistema de sites de ponto de ligação de serviço no site de nível superior da sua hierarquia. Isto pode ser no modo online ou offline. Após a sua hierarquia transfere o pacote de atualização da Microsoft, pode encontrá-lo na consola em **administração &gt; descrição geral &gt; serviços em nuvem &gt; atualizações e manutenção**.

-   Quando a atualização está listada como **disponível**, a atualização está pronta para instalar. Antes de instalar a versão 1706, reveja as seguintes informações [sobre a instalação de atualização 1706](#about-installing-update-1706) e [lista de verificação](#checklist) para configurações para se certificar antes de iniciar a atualização.

-   Se a atualização é apresentado como **transferir** e não alterar, reveja o **hman.log** e **dmpdownloader.log** erros.

    -   Se o ficheiro dmpdownloader.log indica o processo de dmpdownloader está em modo de suspensão e aguardar por um intervalo antes de procurar atualizações, pode reiniciar o **SMS_Executive** serviço no servidor do site para reiniciar a transferência de ficheiros de redistribuição a atualização.

    -   Outro problema comum verificado pela transferência ocorre quando as definições do servidor proxy impediram transferências do <http://silverlight.dlservice.microsoft.com> e <http://download.microsoft.com>.

Para obter mais informações sobre a instalação de atualizações, consulte [na consola atualizações e manutenção](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Para obter informações sobre as versões do ramo atual, consulte [versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines) no [atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="about-installing-update-1706"></a>Sobre a instalação de atualização 1706

**Sites:**  
Instalar a atualização 1706 no site de nível superior da sua hierarquia. Isto significa que inicia a instalação do seu site de administração central, se tiver uma, ou do seu site primário autónomo. Após a atualização é instalada no site de nível superior, os sites subordinados têm o seguinte comportamento da atualização:

-   Os sites primários subordinados instalam a atualização automaticamente depois do site de administração central concluir a instalação da atualização. Pode utilizar janelas de serviço para controlar quando um site instala a atualização. Para obter mais informações, consulte [windows para servidores de site do serviço](/sccm/core/servers/manage/service-windows).

-   Tem de atualizar manualmente cada site secundário a partir da consola do Configuration Manager depois do site primário principal concluída a instalação da atualização. A atualização automática dos servidores de site secundários não é suportada.

**Funções de sistema de sites:**  
Quando um servidor do site instala a atualização, as funções de sistema de sites que estão instaladas no computador do servidor do site e os que são instaladas em computadores remotos, automaticamente atualizadas. Antes de instalar a atualização, certifique-se de que cada servidor do sistema de sites cumpre os pré-requisitos para a operação com a nova versão de atualização.

**Consolas do Configuration Manager:**   
Na primeira vez que utiliza uma consola do Configuration Manager após a atualização estiver concluída, será solicitado Atualize a consola. Para tal, tem de executar a configuração do Configuration Manager no computador que aloja a consola e, em seguida, escolha a opção para atualizar a consola. Recomendamos que não adie a instalação da atualização na consola.

> [!IMPORTANT]  
> Quando instala uma atualização no site de administração central, tenha em atenção as seguintes limitações e atrasos que existem até que todos os sites primários subordinados também concluir a instalação da atualização:    
> - **As atualizações de cliente** não iniciar. Isto inclui atualizações automáticas de clientes e os clientes de pré-produção. Além disso, não é possível promover os clientes de pré-produção para produção, até que o último site seja concluída a instalação da atualização. Depois do último site concluir a instalação da atualização, as atualizações de cliente vai começar com base nas opções de configuração.   
> - **Novas funcionalidades** ativar com a atualização não estão disponíveis. Este procedimento impede que a replicação dos dados relacionados com a funcionalidade do que está a ser enviados para um site que ainda não instalou o suporte para essa funcionalidade. Após todos os sites primários instalam a atualização, a funcionalidade estará disponível para utilização.   
> - **Ligações de replicação** entre o site de administração central e subordinados sites primários são apresentadas como não atualizado. Esta ação apresenta no estado de instalação do pacote de atualização como o estado concluído com o aviso de inicialização da replicação de monitorização. No nó de monitorização da consola, este é apresentado conforme *ligação está a ser configurada*.


## <a name="checklist"></a>Lista de verificação

**Certifique-se de que todos os sites executem uma versão do System Center Configuration Manager que suporta a atualização para 1706:**   
Cada servidor do site na hierarquia tem de executar a mesma versão do System Center Configuration Manager antes de poder iniciar a instalação da atualização 1706. Para atualizar para 1706, tem de utilizar a versão 1606, 1610 ou 1702.

**Rever o estado do seu Software Assurance ou direitos equivalentes de subscrição:**   
Tem de ter um contrato de Software Assurance (SA) de Active Directory ao instalar a atualização 1706. Quando instalar esta atualização, o **licenciamento** separador apresenta a opção para confirmar a sua **data de expiração do Software Assurance**.

Este é um valor opcional que pode especificar como um lembrete conveniente da sua data de expiração de licença. Esta data está visível quando instalar atualizações futuras. Pode ter anteriormente especificado este valor durante a configuração ou a instalação de uma atualização, ou utilizando o **licenciamento** separador do **definições de hierarquia**, da consola do Configuration Manager.

Para obter mais informações, consulte [licenciamento e ramos para o System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

**Revisão instaladas as versões do Microsoft .NET em servidores do sistema de sites:** Quando um site instala esta atualização, o Configuration Manager instala automaticamente o .NET Framework 4.5.2 em cada computador que aloja uma das seguintes funções do sistema de site quando o .NET Framework 4.5 ou posterior não está já instalada:

-   Ponto proxy de registo
-   Ponto de inscrição
-   Ponto de gestão
-   Ponto de ligação de serviço

Esta instalação pode colocar o servidor de sistema de sites no reinício pendente erros de estado e relatórios para o Visualizador de estado do componente do Configuration Manager. Além disso, as aplicações de .NET no servidor podem ocorrer falhas aleatórias até que o servidor seja reiniciado.

Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

**Consultar a versão do Windows Assessment and Deployment Kit (ADK) para Windows 10** o Windows 10 ADK devem ser versão 1703 ou posterior. (Para obter mais informações sobre as versões suportadas do Windows ADK, consulte [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).) Se tem de atualizar o Windows ADK, faça-o antes de começar a atualização do Configuration Manager. Isto garante que as imagens de arranque predefinidas são automaticamente atualizadas para a versão mais recente do Windows PE. (Imagens de arranque personalizadas têm de ser atualizadas manualmente.)

Se atualizar o site antes de atualizar o Windows ADK, consulte [atualizar pontos de distribuição com a imagem de arranque](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image) para melhoramentos para este processo no Configuration Manager versão 1706.

**Rever o estado de site e da hierarquia e certifique-se de que existem não existem problemas por resolver:** Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, o servidor de base de dados do site e funções de sistema de sites que são instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.

Para obter mais informações, veja [Utilizar alertas e o sistema de estado para o System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system).

**Reveja o ficheiro e dados de replicação entre sites:**   
Certifique-se de que o ficheiro e a replicação de base de dados entre sites está operacional e atual. Os atrasos ou os registos de segurança no podem impedir uma atualização com êxito, uniforme.
Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização.

Para obter mais informações, consulte [sobre o analisador do Link de replicação](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) no [monitorizar a infraestrutura hierarquia e replicação no System Center Configuration Manager](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure) tópico.

**Instale todas as atualizações críticas aplicáveis para sistemas operativos em computadores que alojam o site, o servidor de base de dados do site e as funções do sistema de sites remoto:** Antes de instalar uma atualização para o Configuration Manager, instale quaisquer atualizações críticas para cada sistema de sites aplicáveis. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização.

**Desative réplicas de base de dados para pontos de gestão em sites primários:**   
O Configuration Manager não é possível atualizar com êxito um site primário que tenha uma réplica de base de dados para pontos de gestão ativada. Desative a replicação de base de dados antes de instalar uma atualização para o Configuration Manager.

Para obter mais informações, veja [Réplicas de bases de dados para pontos de gestão do System Center Configuration Manager](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

**Definir grupos de Disponibilidade AlwaysOn do SQL Server para ativação pós-falha manual:**   
Se utilizar um grupo de disponibilidade, certifique-se de que o grupo de disponibilidade está definido para ativação pós-falha manual antes de iniciar a instalação da atualização. Depois do site foi atualizado, pode restaurar a ativação pós-falha para ser automática. Para obter mais informações consulte [SQL Server AlwaysOn para uma base de dados do site](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

**Reconfigure os pontos de atualização de software que utilizem NLB:**   
O Configuration Manager não é possível atualizar um site que utiliza uma cluster (NLB) para alojar pontos de atualização de software de balanceamento de carga na rede.

Se utilizar NLB clusters para pontos de atualização de software, utilize o Windows PowerShell para remover o cluster NLB.
Para obter mais informações, veja [Planear atualizações de software no System Center Configuration Manager](/sccm/sum/plan-design/plan-for-software-updates).

**Desative todas as tarefas de manutenção do site em cada site durante a instalação da atualização desse site:**   
Antes de instalar a atualização, desative as tarefas de manutenção do site que possam ser executadas enquanto o que o processo de atualização estiver ativo. Estas incluem as seguintes, entre outras:

-   Servidor do Site de Reserva
-   Eliminar Operações de Cliente Desatualizadas
-   Eliminar Dados de Deteção Desatualizados

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desativar uma tarefa, registe o agendamento da tarefa para que possa restaurar a respetiva configuração após a atualização foi instalada.

Para obter mais informações, consulte [tarefas de manutenção do System Center Configuration Manager](/sccm/core/servers/manage/maintenance-tasks) e [tarefas de referência para a manutenção do System Center Configuration Manager](/sccm/core/servers/manage/reference-for-maintenance-tasks).

**Crie uma cópia de segurança da base de dados do site no site de administração central e sites primários:** Antes de atualizar um site, uma cópia de segurança da base de dados do site para se certificar de que tem uma cópia de segurança a utilizar para recuperação após desastre.

Para obter mais informações, consulte [cópia de segurança e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

**Planear testes de implementação de cliente:**   
Quando instala uma atualização que atualiza o cliente, pode testar essa nova atualização de cliente em pré-produção antes de implementar e atualiza todos os clientes ativos.

Para tirar partido desta opção, tem de configurar o seu site para suportar as atualizações automáticas para pré-produção antes de iniciar a instalação da atualização.

Para obter mais informações, consulte [atualizar clientes no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients) e [como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/test-client-upgrades).

**Planear a utilização de janelas de serviço para controlar quando os servidores do site instalam atualizações:**   
Utilize as janelas de serviço para definir um período de durante as atualizações a um site o servidor pode ser instalado.

Isto pode ajudar a controlar quando os sites na hierarquia instalam a atualização. Para obter mais informações, consulte [windows para servidores de site do serviço](/sccm/core/servers/manage/service-windows).

**Execute o Verificador de pré-requisitos do programa de configuração:**   
Quando a atualização está listada na consola do como **disponível,** independentemente pode executar o Verificador de pré-requisitos antes de instalar a atualização. (Quando instalar a atualização no site, o Verificador de pré-requisitos é executado novamente.)

Para executar uma verificação de pré-requisitos a partir da consola, aceda a **administração > Descrição geral > Serviços Cloud > atualizações e manutenção.** Em seguida, clique com botão direito **pacote de atualização do Configuration Manager 1706**e, em seguida, escolha **executar verificação de pré-requisitos**.

Para obter mais informações sobre como iniciar e, em seguida, monitorizar a verificação de pré-requisitos, consulte **passo 3: Executar o Verificador de pré-requisitos antes de instalar uma atualização** no tópico [instalar atualizações na consola do System Center Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

> [!IMPORTANT]  
> Quando o Verificador de pré-requisitos é executado independentemente ou como parte de uma instalação de atualização, o processo atualiza alguns ficheiros de origem do produto que são utilizados para tarefas de manutenção do site. Por conseguinte, depois de executar o Verificador de pré-requisitos, mas antes a instalar a atualização, se tiver de executar uma tarefa de manutenção do site, execute **Setupwpf.exe** (configuração do Configuration Manager) partir do CD. Pasta mais recente no servidor do site.

**Atualizar sites:**   
Agora está pronto para iniciar a instalação da atualização para a sua hierarquia. Para obter mais informações sobre como instalar a atualização, consulte [instalar atualizações na consola.](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)

Recomendamos que planeia instalar a atualização fora do horário comercial normal para cada site quando o processo de instalação da atualização e as respetivas ações para reinstalar os componentes do site e funções de sistema de sites irão ter o mínimo efeito nas suas operações de negócio.

Para obter mais informações, veja [Atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="post-update-checklist"></a>Lista de verificação de atualização de POST
Reveja as ações seguintes a efetuar depois de concluída a instalação da atualização.
1.  Certifique-se de que a replicação site a site está ativa. Na consola, ver **monitorização** > **hierarquia do Site**, e **monitorização** > **replicação de base de dados** indicações de problemas ou a confirmação de que as ligações de replicação estão ativas.
2.  Certifique-se de que cada servidor do site e a função do sistema de sites foi atualizado para a versão 1706. Na consola, pode adicionar a coluna opcional **versão** para a apresentação de alguns nós incluindo **Sites** e **pontos de distribuição**.

 Quando for necessário, uma função de sistema do site irá reinstalar automaticamente para atualizar para a nova versão. Considere reiniciar sistemas de sites remotos que não atualizar com êxito.
3.  Reconfigure réplicas de base de dados para pontos de gestão em sites primários que desativou antes de iniciar a atualização.
4.  Reconfigure tarefas de manutenção de base de dados que desativou antes de iniciar a atualização.
5.  Se tiver configurado o teste de implementação no antes de instalar a atualização de cliente, atualize clientes pelo plano que criou.

## <a name="known-issues"></a>Problemas conhecidos 
Depois de atualizar para versão 1706, é criada sempre que o SMS_Executive inicia a seguinte mensagem de estado de aviso pelo SMS_CERTIFICATE_MANAGER:
-    Microsoft SQL Server comunicou a gravidade 515, da mensagem do SQL 16: [23000] [515] [Microsoft] [SQL Server Native cliente 11.0] [SQL Server] não é possível inserir o valor NULL na coluna 'RowVersion', tabela 'CM_GF1.dbo.AAD_SecretChange_Notify'; coluna não permite valores nulos. Falha de INSERT.

Esta mensagem pode ser ignorada.  -Ocorre quando não existem serviços em nuvem foram configurados para ser utilizada antes de atualizar para a versão 1706. Este problema será resolvido numa versão futura.

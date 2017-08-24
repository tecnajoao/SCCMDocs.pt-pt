---
title: "Atualizações na consola | Microsoft Docs"
description: "System Center Configuration Manager sincroniza com a nuvem da Microsoft para obter atualizações que pode instalar a consola."
ms.custom: na
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
caps.latest.revision: "36"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 2bbc8935bee306ed0bc312cc43b8f5374a8df7ff
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Instalar atualizações na consola para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager sincroniza com o serviço de nuvem da Microsoft para obter atualizações. Em seguida, pode instalar estas atualizações a partir da consola do Configuration Manager.

## <a name="get-available-updates"></a>Obter as atualizações disponíveis
Apenas as atualizações aplicáveis à sua infraestrutura e versão são transferidas e disponibilizadas na sua hierarquia. Esta sincronização pode ser automática ou manual, dependendo de como configurar o ponto de ligação de serviço para a sua hierarquia:

-   No **modo online**, o ponto de ligação de serviço liga automaticamente ao serviço em nuvem da Microsoft e transfere as atualizações aplicáveis.  

     Por predefinição, o Configuration Manager verifica a existência de novas atualizações a cada 24 horas. Pode também verificar atualizações imediatamente escolhendo **procurar atualizações** no **administração** > **atualizações e manutenção** nó da consola do Configuration Manager. (Antes da versão 1702, este nó foi em **administração** > **serviços em nuvem**.)

-   No **modo offline**, o ponto de ligação de serviço não liga ao serviço de nuvem da Microsoft. Para transferir e, em seguida, importar as atualizações disponíveis, [utilizar a ferramenta de ligação de serviço do System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

> [!NOTE]  
>   Pode importar correções fora de banda para a consola. Para tal, utilize o [ferramenta de registo de atualização](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes). Estas correções fora de banda completam as atualizações que obtém ao sincronizar com o serviço Microsoft Cloud.


Depois de sincronizar as atualizações, pode visualizá-las na consola do Configuration Manager, acedendo ao **administração** > **atualizações e manutenção** nó:  

-   As atualizações não instaladas são apresentadas como **Disponível**.

-   As atualizações instaladas são apresentadas como **Instalada**.  É apresentada apenas a atualização instalada mais recentemente. Pode escolher o **histórico** botão no friso para anteriormente ver atualizações instaladas.



Antes de configurar o ponto de ligação de serviço, compreenda e planeie as utilizações adicionais. As seguintes utilizações podem afetar a forma como configura esta função de sistema de sites:  

-   O ponto de ligação de serviço é utilizado para carregar as informações de utilização sobre o seu site. Estas informações ajudam o serviço em nuvem da Microsoft a identificar as atualizações que estão disponíveis para a versão atual da sua infraestrutura. Para obter mais informações, consulte [diagnósticos e dados de utilização para o System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

-   O ponto de ligação de serviço é utilizado para gerir dispositivos com o Microsoft Intune e utilizando a gestão de dispositivos móveis no local do Configuration Manager. Para obter mais informações, consulte [gestão híbrida de dispositivos móveis (MDM) com o System Center Configuration Manager e o Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

Para melhor compreender o que acontece quando as atualizações são transferidas, consulte:  

-   [Fluxograma - transferir atualizações para o System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md)

-   [Fluxograma - replicação de atualização para o System Center Configuration Manager](../../../core/servers/manage/update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Atribuir permissões para ver e gerir as atualizações e funcionalidades
Para ver as atualizações na consola, um utilizador tem de ter uma função de segurança da administração baseada em funções que inclua a classe de segurança **pacotes de atualização**. Esta classe concede acesso para ver e gerir as atualizações na consola do Configuration Manager.    

**Sobre a classe Pacotes de atualização:**  
Por predefinição, **Pacotes de atualização** (SMS_CM_Updatepackages) faz parte dos seguintes direitos de acesso incorporados nas permissões listadas:
 -  **Administrador Total** com permissões de **Modificação** e **Leitura** :
    -   Um utilizador com esta função de segurança e acesso para o **todos os** âmbito de segurança pode ver e instalar atualizações. O utilizador também pode ativar funcionalidades durante a instalação e ativar funcionalidades individuais, depois de instalada a atualização.
    - Um utilizador com esta função de segurança e acesso para o **predefinido** âmbito de segurança pode ver e instalar atualizações. O utilizador também pode ativar funcionalidades durante a instalação e ver funcionalidades após uma atualização está instalada. Mas este utilizador não é possível ativar as funcionalidades, depois de instalada a atualização.

- **Analista só de leitura** com permissões de **Leitura** :
  -  Um utilizador com esta função de segurança e acesso para o **predefinido** âmbito pode ver as atualizações, mas não instalá-los. Este utilizador também pode ver as funcionalidades depois de uma atualização foi instalado mas não é possível ativá-los.

**Permissões necessárias para as atualizações e manutenção:**   
  - Utilize uma conta à qual esteja atribuído um direito de acesso que inclua a classe **Pacotes de atualização** com as permissões de **Modificação** e **Leitura** .
  - O âmbito **Predefinição** tem de ser atribuído à conta.

**Permissões para visualizar apenas atualizações**:
  - Utilize uma conta à qual esteja atribuído um direito de acesso que inclua a classe **Pacotes de atualização** apenas com a permissão de **Leitura** .
  - O âmbito **Predefinição** tem de ser atribuído à conta.

**Permissões necessárias para ativar funcionalidades após as atualizações são instaladas:**
  -  Utilize uma conta à qual esteja atribuído um direito de acesso que inclua a classe **Pacotes de atualização** com as permissões de **Modificação** e **Leitura** .
  -  O âmbito **Tudo** tem de ser atribuído à conta.



##  <a name="bkmk_beforeinstall"></a> Antes de instalar uma atualização na consola  
 Reveja os seguintes passos antes de instalar uma atualização a partir da consola do Configuration Manager.  

###  <a name="bkmk_step1"></a>Passo 1: Reveja a lista de verificação de atualização  
Reveja a lista de verificação de atualizações aplicável para ações a efetuar antes de iniciar a atualização:

- Atualizar para 1606: Consulte [1606 de atualizar a lista de verificação para instalar](../../../core/servers/manage/checklist-for-installing-update-1606.md).  

- Atualizar para 1610 de qualquer um dos 1606: Consulte [atualizar a lista de verificação para instalar 1610](../../../core/servers/manage/checklist-for-installing-update-1610.md).  

- Atualizar para 1702 1606 ou 1610: Consulte [atualizar a lista de verificação para instalar 1702](../../../core/servers/manage/checklist-for-installing-update-1702.md).

<!-- Removed as update guidance 6/6/2017. The Test DB Upgrade details are no longer recommended nor required. They live on in a new topic for customers who still want to use them. -->

###  <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a>Passo 2: Executar o Verificador de pré-requisitos antes de instalar uma atualização  
Antes de instalar uma atualização, considere executar a verificação de pré-requisitos para essa atualização. Se executar o pré-requisito antes de instalar uma atualização:  

-   Os ficheiros de atualização são replicados para outros sites antes de instalar a atualização.  

-   A verificação de pré-requisitos é executado automaticamente novo quando optar por instalar a atualização.  

Mais tarde, quando instala a atualização, pode configurar a atualização para ignorar os avisos de verificação de pré-requisitos.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Para executar o verificador de pré-requisitos antes de instalar uma atualização  

1.  Na consola do Configuration Manager, vá para **administração** > **atualizações e manutenção**.   

2.  Faça duplo clique no pacote de atualização que pretende executar a verificação de pré-requisitos.  

3.  Escolha **Executar verificação de pré-requisitos**.  

     Quando executar a verificação de pré-requisitos, o conteúdo da atualização é replicado para sites subordinados.  Pode ver o ficheiro distmgr.log no site de servidor para confirmar que o conteúdo é a replicado com êxito.  

4.  Para ver os resultados da verificação, na consola do Configuration Manager, vá para **monitorização** > **atualizações e manutenção estado** e procure o estado dos pré-requisitos. Também pode ver o ConfigMgrPrereq.log no servidor do site para obter mais detalhes.  



##  <a name="bkmk_install"></a> Instalar atualizações na consola  
 Quando estiver pronto para instalar as atualizações a partir da consola do Configuration Manager, começar com o site de nível superior da hierarquia. Este é o site de administração central ou um site primário autónomo.  

 Recomendamos que instale a atualização fora do horário comercial normal para cada site minimizar o efeito nas operações de negócio. Isto acontece porque a instalação da atualização pode incluir ações como reinstalar os componentes do site e funções de sistema do site.  

-   Os sites primários subordinados iniciam a atualização automaticamente, após o site de administração central concluir a instalação da atualização. Este é o predefinido e recomendado processo. No entanto, pode utilizar [windows para servidores de site do serviço](/sccm/core/servers/manage/service-windows) para controlar quando um site primário instala as atualizações.  

-   Atualize manualmente os sites secundários a partir da consola do Configuration Manager depois de concluída a atualização do site primário principal. A atualização automática dos servidores de site secundários não é suportada.  

-   Quando utiliza uma consola do Configuration Manager depois do site é atualizado, lhe for pedido para atualizar a consola.  

-  Depois do servidor do site concluir a instalação de uma atualização com êxito, atualiza automaticamente todas as funções de sistema de sites aplicáveis.  É a advertência apenas para pontos de distribuição. Ao instalar uma atualização, todos os pontos de distribuição não reinstalar e ficam offline para atualizar ao mesmo tempo. Em vez disso, o servidor de site utiliza as definições de distribuição de conteúdo do site para distribuir a atualização para um subconjunto dos pontos de distribuição de cada vez. O resultado é que alguns pontos de distribuição ficam offline para instalar a atualização. Pontos de distribuição que não ter sido iniciada atualizar ou que concluiu a atualização permanecerem online e é capaz de fornecer conteúdo aos clientes.


###  <a name="bkmk_overview"></a> Descrição geral da instalação da atualização na consola  
**1. Quando inicia a instalação da atualização**  
É-lhe apresentado o Assistente de Atualizações, que apresenta uma lista de áreas de produto a cuja atualização se refere.  

-   Na página **Geral** do assistente, pode configurar **Avisos de pré-requisitos**.  
      -   Os erros de pré-requisitos interrompem sempre a instalação da atualização. Corrija os erros antes de pode repetir a instalação da atualização com êxito. Veja [Repetir a instalação de uma atualização falhada](#bkmk_retry) para obter mais informações.  

    -   Os avisos de pré-requisitos também podem interromper a instalação da atualização. Corrija os avisos antes de repetir a instalação da atualização. Para obter mais informações, consulte [repetir a instalação de uma atualização falhada](#bkmk_retry).  
    -   A opção **ignorar quaisquer avisos de verificação de pré-requisitos e instalar esta atualização independentemente requisitos em falta** define uma condição para a instalação da atualização que ignora os avisos de pré-requisitos. Isto permite que a instalação da atualização continuar. Se não selecionar esta opção, a instalação da atualização para quando for detetado um aviso. A menos que executou anteriormente a verificação de pré-requisitos e os avisos de pré-requisitos fixos para um site, não é recomendada a utilização desta opção.  

      Em ambos os **administração** e **monitorização** áreas de trabalho, as atualizações e manutenção nó inclui um botão no Friso denominado **ignorar os avisos de pré-requisitos**. Este botão fica disponível quando um pacote de atualização não é possível concluir a instalação devido a avisos de verificação de pré-requisitos. Por exemplo, instalar uma atualização sem utilizar a opção para ignorar os avisos de pré-requisitos (no Assistente para atualizações). Interrompe a instalação da atualização com o estado de aviso de pré-requisitos, mas sem erros. Mais tarde, pode escolher **ignorar os avisos de pré-requisitos** a partir do friso para acionar uma continuação automática que da instalação de atualização que ignora os avisos de pré-requisitos. Quando utiliza esta opção, a instalação da atualização continua automaticamente após alguns minutos.



-   Quando uma atualização se refere ao cliente do Configuration Manager, é-lhe apresentada a opção para testar a atualização do cliente com um conjunto limitado de clientes. Para obter mais informações, consulte [como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**2. Durante a instalação da atualização**  
Como parte da instalação da atualização do Configuration Manager:  

-   Reinstala os componentes afetados, como as funções do sistema de site ou consola do Configuration Manager.  

-   Gere as atualizações para clientes com base nas seleções que efetuou para testes de implementação de cliente e para [atualizações automáticas de cliente](https://technet.microsoft.com/library/mt627885.aspx).  

-   Não reiniciar os servidores de sistema de sites como parte da atualização, exceto se .NET estiver instalado como parte de um pré-requisito de funções de sistema do site.  

> [!TIP]  
>  Quando as atualizações são instaladas, atualizações do Configuration Manager também CD. Pasta mais recente. Esta pasta é utilizada durante uma recuperação de site.  

**3. Monitorizar o progresso das atualizações de instalação**  
Utilize o seguinte procedimento para monitorizar o progresso:  

-   Na consola do Configuration Manager: **Administração** > **atualizações e manutenção** nós. Este nó mostra o estado da instalação para todos os pacotes de atualização.


-   Na consola do Configuration Manager: **Monitorização** > **descrição geral** > **atualizações e manutenção estado** nós. Este nó mostra o estado da instalação de apenas o pacote de atualização que está atualmente a ser instalado.  

    A instalação do pacote de atualização é reduzida para as seguintes fases para facilitar a monitorização. Para cada fase, detalhes adicionais incluem o ficheiro de registo para ver para obter mais informações:  
    -   **Transferir** (nesta fase aplica-se apenas para o site de nível superior em que o site de ponto de ligação de serviço está instalado.)   

    -   **Replicação**   

    -   **Verificação de Pré-requisitos**   

    -   **Instalação**    

    -   **Após a instalação** ([tarefas de pós-instalação](#post-installation-tasks) disponíveis a partir versão 1610.)  

-   Pode ver o **CMUpdate.log** ficheiros  **&lt;ConfigMgr_Installation_Directory > \Logs**  

**4. Quando a instalação da atualização é concluída**  
Após a instalação da primeira atualização do site ser concluída:  

-   Os sites primários subordinados instalam a atualização automaticamente. Não é necessária mais nenhuma ação.  

-   Os sites secundários têm de ser manualmente atualizados da consola do Configuration Manager.
> [!TIP]
> Embora a versão de um site secundário não for apresentado na consola, pode utilizar o SDK do Gestor de configuração para confirmar a versão de um site. Consulte [SMS_Site servidor WMI classe](https://technet.microsoft.com/library/hh442832(CMSDK.16).aspx).


-   Até que todos os sites da hierarquia tenham sido atualizados para a nova versão, a hierarquia funciona num modo com versões mistas. Para obter mais informações, veja [Interoperabilidade entre diferentes versões do System Center Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

**5.   Atualizar consolas do Configuration Manager**  
Depois de um site de administração central ou site primário, cada consola do Configuration Manager que liga a esse site tem também de atualizar. Ser-lhe-á pedido para atualizar uma consola:  

-   Quando abrir a consola.  

-   Quando acede a um novo nó numa consola aberta.  

Recomendamos que instale a atualização imediatamente.  

Quando a atualização da consola estiver concluída, pode verificar se a versão da consola e do site está correta. Aceda a **sobre o System Center Configuration Manager** no canto superior esquerdo da consola.  

###  <a name="bkmk_toptier"></a> Para iniciar a instalação da atualização no site de nível superior  
No site de nível superior da hierarquia, na consola do Configuration Manager aceda a **administração** > **atualizações e manutenção**, selecione um **disponível** atualizar e, em seguida, clique em **Instalar pacote de atualizações**.  

###  <a name="bkmk_secondary"></a> Para iniciar a instalação da atualização num site secundário  
Depois de atualizações de site primário principal de um site secundário, pode atualizar o site secundário a partir da consola do Configuration Manager.  Para tal, utilize o **Assistente para Atualizar Site Secundário**.  

1.  Na consola do Configuration Manager, vá para **administração** > **configuração do Site** > **Sites**, selecione o site que pretende atualizar e, em seguida, na home page do separador, no **Site** grupo, escolha **atualizar**.  

2.  Clique em **Sim** para iniciar a atualização do site secundário.  

Para monitorizar a instalação da atualização num site secundário, selecione o servidor de site secundário. Em seguida, no **home page** separador o **Site** grupo, escolha **Mostrar estado da instalação**. Também pode adicionar a coluna **Versão** ao ecrã da consola, de modo a que possa ver a versão de cada site secundário.  

Depois de um site secundário com êxito as atualizações, se o estado na consola do não atualiza ou sugere falhou a atualização, utilizam o **repetir a instalação** opção. Esta opção não reinstalar a atualização de um site secundário que instalar com êxito a atualização, mas que força a consola para atualizar o estado.

### <a name="post-installation-tasks"></a>Tarefas de pós-instalação
A partir da versão 1610, pode ver informações sobre as tarefas de pós-instalação.

Quando um site instala uma atualização, existem várias tarefas que não é possível iniciar até após a conclusão da atualização instalação no servidor do site. Segue-se uma lista das tarefas de instalação post que são críticos para as operações de hierarquia e site. Uma vez que são críticos, são ativamente monitorizadas. Tarefas adicionais que não são monitorizadas diretamente incluem a reinstalação de funções de sistema de sites. Para ver o estado das tarefas de instalação post crítico, selecione **após a instalação** tarefas ao monitorizar a instalação da atualização para um site.

Nem todas as tarefas concluírem imediatamente. Algumas tarefas não iniciada até a cada site concluir a instalação da atualização. Por conseguinte, novas funcionalidades que seria de esperar podem sofrer um atraso de até concluírem estas tarefas. Por exemplo, porque ativar novas funcionalidades não é iniciado até que todos os sites concluir a instalação da atualização, as novas funcionalidades podem não estar visíveis durante algum tempo.

As tarefas de pós-instalação incluem:

-   **Instalar o serviço SMS_EXECUTIVE**
  -   Serviço crítico que é executado no servidor do site.
  -   Reinstalação deste serviço deve ser concluído rapidamente.


-   **Instalar o componente SMS_DATABASE_NOTIFICATION_MONITOR**
  -   Thread do componente de críticos do site do serviço SMS_EXECUTIVE.
  -   Reinstalação deste serviço deve ser concluído rapidamente.


-   **Instalar o componente SMS_HIERARCHY_MANAGER**
  -   Componente de críticos do site que é executado no servidor do site.
  -   Responsável por reinstalar funções do sistema de sites em servidores de sistema de sites.  Não apresentar o estado para reinstalação de função do sistema de sites individuais.
  -   Reinstalação deste serviço deve ser concluído rapidamente.


-   **Instalar o componente SMS_REPLICATION_CONFIGURATION_MONITOR**
  -   Componente de críticos do site que é executado no servidor do site.
  -   Reinstalação deste serviço deve ser concluído rapidamente.


-   **Instalar o componente SMS_POLICY_PROVIDER**
  -   Componente de críticos do site que é executado apenas em sites primários.
  -   Reinstalação deste serviço deve ser concluído rapidamente.


-   **Monitorizar a inicialização da replicação**   
  -   Esta ação apresenta apenas o site de administração central e sites primários subordinados.
  -   O SMS_REPLICATION_CONFIGURATION_MONITOR dependente.
  -   Deve ser concluído rapidamente.


-   **Atualizar o pacote de pré-produção do cliente do Configuration Manager**    
  -   Esta ação apresenta, mesmo quando cliente de pré-produção (também denominada cliente testes de implementação no) não está ativado para utilização.
  -   Não é iniciado até que todos os sites na hierarquia de concluir a instalação da atualização.


-   **Pasta de atualização do cliente no servidor do Site**
  -   Não é apresentado se utilizar o cliente em pré-produção.  
  -   Deve ser concluído rapidamente.


-   **Atualizar o pacote de cliente do Configuration Manager**
  -   Não é apresentado se utilizar o cliente em pré-produção.  
  -   Acaba de apenas depois de todos os sites instalam a atualização.  


-   **Ativar funcionalidades**
  -   Esta ação apresenta apenas no site de nível superior da hierarquia.
  -   Não é iniciado até que todos os sites na hierarquia de concluir a instalação da atualização.
  -   Funcionalidades individuais não são apresentadas.


##  <a name="bkmk_retry"></a> Repetir a instalação de uma atualização falhada  
Quando a instalação de uma atualização falhar, reveja os comentários na consola para identificar resoluções de avisos e erros. Também pode ver o ConfigMgrPrereq.log no servidor do site para obter mais detalhes. Antes de repetir a instalação de uma atualização, é necessário corrigir os erros e deve corrigir os avisos.  

> [!TIP]  
> Se uma atualização tem problemas de transferir ou replicar, pode utilizar o [ferramenta de reposição de atualização](/sccm/core/servers/manage/update-reset-tool). Esta ferramenta é disponíveis a partir dos sites que executam a versão 1706 ou posterior. 

Quando estiver pronto para repetir a instalação de uma atualização, selecione a atualização falhada e, em seguida, escolha uma opção aplicável. O comportamento de tentativas de instalação de atualização depende do nó onde deve começar a repetição e a opção de repetição que utilizar.  

1.  **Repetir a instalação para a hierarquia:**  
Pode repetir a instalação de uma atualização para toda a hierarquia quando a atualização se encontra num dos seguintes estados:  

    -   Verificação de pré-requisitos passou com um ou mais avisos, e a opção para ignorar os avisos de verificação de pré-requisitos não foi definida no Assistente de atualização. (Valor da atualização para **ignorar aviso de pré** no **atualizações e manutenção** é nó **não**.)   
    -   Falha no pré-requisito    
    -   Falha na instalação
    -   Falha na replicação do conteúdo para o site   

    Aceda a **administração** > **atualizações e manutenção**, selecione a atualização e, em seguida, escolha uma das seguintes opções:  

    -   **Repita** - quando executar **repita** partir deste nó, a instalação da atualização é iniciada novamente e automaticamente ignora os avisos de pré-requisitos. Conteúdo para a atualização também novamente replica se replicação tenha falhado anteriormente.
    - **Ignorar os avisos de pré-requisitos** -a partir da versão 1606, se parar devido a um aviso de instalar a atualização, pode então escolher **ignorar os avisos de pré-requisitos**. Esta ação permite continuar a instalação da atualização (após alguns minutos) e utiliza a opção para ignorar avisos de pré-requisitos.   

2.  **Repetir a instalação para o site:**  
 Pode repetir a instalação de uma atualização num site específico quando a atualização se encontra num dos seguintes estados:  

    -   Verificação de pré-requisitos passou com um ou mais avisos, e a opção para ignorar os avisos de verificação de pré-requisitos não foi definida no Assistente de atualização. (O valor das atualizações para **ignorar aviso de pré-requisitos** do nó atualizações e manutenção é **não**.)  
    -   Falha no pré-requisito    
    -   Falha na instalação    

    Aceda a **monitorização** > **descrição geral** > **estado de manutenção do Site**, selecione a atualização e, em seguida, clique das seguintes opções:

       - **Repita** - quando executar **repita** partir deste nó, reiniciar a instalação da atualização apenas nesse site. Ao contrário de execução **repita** do **atualizações e manutenção** nó, esta repetição ignora os avisos de pré-requisitos.
       -    **Ignorar os avisos de pré-requisitos** -a partir da versão 1606, se parar devido a um aviso de instalar a atualização, pode, em seguida, clicar em **ignorar os avisos de pré-requisitos**. Esta ação permite continuar a instalação da atualização (após alguns minutos) e utiliza a opção para ignorar avisos de pré-requisitos.

##  <a name="bkmk_after"></a> Após uma site instalar uma atualização  
Utilize a lista de verificação seguinte para concluir tarefas comuns e as configurações que são efetuadas após um site é atualizado.   

**Confirme a replicação do site para site está ativa:** Na consola do Configuration Manager, vá para as localizações seguintes para ver o estado e certifique-se de que a replicação está ativa:  

-   **Monitorização** > **Descrição geral** > **Hierarquia do Site**  

-   **Monitorização** > **Descrição geral** > **Replicação de Base de Dados**  

Para obter mais informações, consulte [monitorizar a infraestrutura hierarquia e replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) e [sobre o analisador do Link de replicação](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Confirme que os servidores de site e servidores do sistema de sites remoto reiniciaram (se necessário):** Reveja a infraestrutura de sites e certifique-se de que os servidores de sistema de sites e servidores de sites aplicáveis tem reiniciado com êxito. Normalmente, os servidores do site reiniciar apenas quando o Configuration Manager instala .NET como um pré-requisito para uma função de sistema de sites.  

 **Atualize consolas do Configuration Manager autónomo:** Certifique-se de que todas as consolas remotas do Configuration Manager estão a atualização para a mesma versão. Ser-lhe-á pedido para atualizar a consola quando:  

-   Ir para um novo nó na consola do.  

-   Abra a consola.

**Reconfigure réplicas de base de dados para pontos de gestão em sites primários:** Se utilizar réplicas de base de dados para pontos de gestão em sites primários, tem de desinstalar as réplicas de base de dados antes de atualizar o site. Após atualizar um site primário, reconfigure a réplica da base de dados para pontos de gestão. Para obter mais informações, veja [Réplicas de bases de dados para pontos de gestão do System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigure as tarefas de manutenção de base de dados que desativou antes da atualização:** Se tiver desativado a base de dados [tarefas de manutenção](../../../core/servers/manage/maintenance-tasks.md) num site antes de instalar a atualização, reconfigure essas tarefas no site. Utilize as mesmas definições que se encontravam em vigor antes da atualização.  

**Atualize clientes:** Para informações, consulte [como atualizar clientes em computadores Windows no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

**Configurações adicionais:** Reveja as alterações efetuadas antes de iniciar a atualização e, em seguida, restaure essas configurações para sites e da hierarquia.  

##  <a name="bkmk_options"></a> Ativar funcionalidades opcionais de atualizações  
Quando uma atualização inclui um ou mais funcionalidades opcionais, terá a oportunidade de ativar essas funcionalidades na sua hierarquia.  Pode ativar funcionalidades quando instala a atualização, ou pode regressar à consola do mais tarde e ativar as funcionalidades opcionais.

Para ver as funcionalidades disponíveis e o respetivo estado, na consola navegue para **administração** > **atualizações e manutenção** > **funcionalidades**.

Quando uma funcionalidade não é opcional, é instalado automaticamente e não for apresentada a **funcionalidades** nós.  


Quando ativa uma funcionalidade nova ou a funcionalidade de pré-lançamento, o Gestor da hierarquia do Configuration Manager (HMAN) tem de processar a alteração para que essa funcionalidade fica disponível. O processamento da alteração, muitas vezes, é imediato, mas pode demorar até 30 minutos a concluir, consoante o ciclo de processamento de HMAN. Após a alteração é processada, tem de reiniciar a consola antes de poder visualizar a nova IU relacionados com essa funcionalidade.


##  <a name="bkmk_prerelease"></a> Utilizar as funcionalidades da versão de pré-lançamento de atualizações
Funcionalidades de pré-lançamento estão incluídas no ramo atual para um teste antecipado num ambiente de produção. Pode utilizar estas funcionalidades no seu ambiente de produção, mas não são considerados produção pronto. Saiba mais sobre [funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features), incluindo como ativá-los no seu ambiente.             


## <a name="known-issues"></a>Problemas conhecidos

###  <a name="bkmk_faq"></a>Por que motivo não vejo determinadas atualizações na consola?  
 Se não conseguir localizar uma atualização específica a consola depois de uma sincronização com êxito com o serviço de nuvem da Microsoft, tal poderá acontecer porque:  

-   A atualização requer uma configuração que a sua infraestrutura não utiliza ou a versão atual do produto não cumpre um pré-requisito para receber a atualização.  

     Se achar que tem as configurações necessárias e pré-requisitos para uma atualização em falta, confirme que o ponto de ligação de serviço está no modo online. Em seguida, utilize o **procurar atualizações** opção o **atualizações e manutenção** nó para forçar uma verificação.  Se estiver no modo offline, tem de utilizar a ferramenta de ligação de serviço para sincronizar manualmente com o serviço em nuvem.  

-   A conta não possui as permissões corretas de administração baseada em funções para ver as atualizações na consola do Configuration Manager.

    Veja [Permissões para gerir atualizações de](../../../core/servers/manage/install-in-console-updates.md#assign-permissions-to-view-and-manage-updates-and-features) neste tópico para obter informações sobre as permissões necessárias para ver atualizações e ativar funcionalidades a partir da consola.

### <a name="why-do-i-see-two-updates-for-version-1610"></a>Por que razão vejo duas atualizações para a versão 1610?
Ao visualizar as atualizações na consola, poderá ver duas atualizações a instalar a versão 1610. Estas atualizações tem datas diferentes. Ambos são apresentadas quando uma das seguintes condições for verdadeira:   
-   Instalou uma versão anterior (como 1606) após a disponibilização de versão 1610

-   A hierarquia executa a versão 1511 ou 1602 e não tenham conseguido transferir a versão 1606

Existem dois atualização versões para versão 1610 porque esta atualização foi lançada novamente depois de algumas alterações secundárias para algumas binários de ficheiro foram efetuadas. Estas alterações não afetam a funcionalidade do Configuration Manager ou a atualização.

Quando ambas as atualizações estão disponíveis na consola do seu, recomendamos que instale a atualização com a data mais recente. No entanto, porque as atualizações de fornecem a mesma funcionalidade, quando já tiver instalado uma delas não é necessário efetuar qualquer ação adicional.
-   Se tiver instalado anteriormente a atualização anterior, não tem de instalar a atualização com a data mais recente. No entanto, se instalar a atualização depois de instalar a primeira atualização mais recente, irão atualizar os binários em questão. Não ocorre nenhuma alteração adicional e não existem ações adicionais da sua parte são necessárias.

-   Se instalou anteriormente a atualização mais recente e, em seguida, instale a atualização com a data mais antiga, não é necessária nenhuma ação adicional. Isto acontece porque os binários da mais recentes já instalado não são substituídos por esses mesmos binários de atualização original.

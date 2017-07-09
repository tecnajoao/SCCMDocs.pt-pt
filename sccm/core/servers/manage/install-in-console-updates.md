---
title: "As atualizações no console | Microsoft Docs"
description: "System Center Configuration Manager será sincronizado com a nuvem da Microsoft para obter atualizações, que você pode instalar o console."
ms.custom: na
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 3619a73d3a39659de927e1711a7ec81de9918064
ms.openlocfilehash: 34ddb646137aaf1160d850ba7c1e0109f467225d
ms.contentlocale: pt-pt
ms.lasthandoff: 06/13/2017


---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Instalar atualizações na consola para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

System Center Configuration Manager sincroniza com o serviço de nuvem da Microsoft para obter atualizações. Em seguida, você pode instalar essas atualizações de dentro do console do Configuration Manager.

## <a name="get-available-updates"></a>Obter as atualizações disponíveis
Apenas as atualizações aplicáveis à sua infraestrutura e versão são transferidas e disponibilizadas na sua hierarquia. A sincronização pode ser automático ou manual, dependendo de como você configura o ponto de conexão de serviço para sua hierarquia:

-   No **modo online**, o ponto de ligação de serviço liga automaticamente ao serviço em nuvem da Microsoft e transfere as atualizações aplicáveis.  

     Por padrão, o Configuration Manager procura novas atualizações a cada 24 horas. Você também pode verificar as atualizações imediatamente escolhendo **verificar se há atualizações** no **administração** > **atualizações e manutenção** nó do console do Configuration Manager. (Antes da versão 1702, esse nó foi em **administração** > **serviços de nuvem**.)

-   Em **modo offline**, o ponto de conexão de serviço não se conecta ao serviço de nuvem da Microsoft. Para baixar e importar as atualizações disponíveis, [usar a ferramenta de Conexão de serviço para o System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

> [!NOTE]  
>   Você pode importar correções fora de banda para o console. Para fazer isso, use o [Update Registration Tool](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes). Essas correções fora de banda complementam as atualizações que você obtém quando você sincronizar com o serviço Microsoft Cloud.


Depois de sincronizar atualizações, você pode exibi-los no console do Configuration Manager, vá para o **administração** > **atualizações e manutenção** nó:  

-   As atualizações não instaladas são apresentadas como **Disponível**.

-   As atualizações instaladas são apresentadas como **Instalada**.  Somente a atualização instalada mais recentemente é mostrada. Você pode escolher o **histórico** atualizações instaladas do botão na faixa de opções para exibir anteriormente.



Antes de configurar o ponto de conexão de serviço, entenda e planeje seus usos adicionais. Os seguintes usos podem afetar como você configurar essa função do sistema de site:  

-   O ponto de ligação de serviço é utilizado para carregar as informações de utilização sobre o seu site. Estas informações ajudam o serviço em nuvem da Microsoft a identificar as atualizações que estão disponíveis para a versão atual da sua infraestrutura. Para obter mais informações, consulte [diagnóstico e dados para o System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

-   O ponto de conexão de serviço é usado para gerenciar dispositivos com Microsoft Intune e usando o gerenciamento de dispositivo móvel local do Configuration Manager. Para obter mais informações, consulte [gerenciamento de dispositivo móvel (MDM) híbrido com o System Center Configuration Manager e o Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

Para entender melhor o que acontece quando as atualizações são baixadas, consulte:  

-   [Fluxograma — baixar atualizações para o System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md)

-   [Fluxograma — replicação de atualização para o System Center Configuration Manager](../../../core/servers/manage/update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Atribuir permissões para exibir e gerenciar os recursos e atualizações
Para exibir as atualizações no console, um usuário deve ter uma função de segurança de administração baseada em função que inclua a classe de segurança **pacotes de atualização de**. Essa classe concede acesso para exibir e gerenciar atualizações no console do Configuration Manager.    

**Sobre a classe Pacotes de atualização:**  
Por predefinição, **Pacotes de atualização** (SMS_CM_Updatepackages) faz parte dos seguintes direitos de acesso incorporados nas permissões listadas:
 -  **Administrador Total** com permissões de **Modificação** e **Leitura** :
    -   Um usuário com essa função de segurança e acesso para o **todos os** escopo de segurança pode exibir e instalar atualizações. O usuário também pode habilitar recursos durante a instalação e habilitar recursos individuais após a atualização está instalada.
    - Um usuário com essa função de segurança e acesso para o **padrão** escopo de segurança pode exibir e instalar atualizações. O usuário também pode habilitar recursos durante a instalação e exibir recursos após uma atualização está instalada. Mas esse usuário não é possível habilitar os recursos após a atualização é instalada.

- **Analista só de leitura** com permissões de **Leitura** :
  -  Um usuário com essa função de segurança e acesso para o **padrão** escopo pode exibir atualizações, mas não instalá-los. Esse usuário também pode exibir recursos após uma atualização foi instalado, mas não é possível habilitá-los.

**Permissões necessárias para atualizações e manutenção:**   
  - Utilize uma conta à qual esteja atribuído um direito de acesso que inclua a classe **Pacotes de atualização** com as permissões de **Modificação** e **Leitura** .
  - O âmbito **Predefinição** tem de ser atribuído à conta.

**Permissões para exibir somente atualizações**:
  - Utilize uma conta à qual esteja atribuído um direito de acesso que inclua a classe **Pacotes de atualização** apenas com a permissão de **Leitura** .
  - O âmbito **Predefinição** tem de ser atribuído à conta.

**Permissões necessárias para habilitar recursos após as atualizações são instaladas:**
  -  Utilize uma conta à qual esteja atribuído um direito de acesso que inclua a classe **Pacotes de atualização** com as permissões de **Modificação** e **Leitura** .
  -  O âmbito **Tudo** tem de ser atribuído à conta.



##  <a name="bkmk_beforeinstall"></a> Antes de instalar uma atualização na consola  
 Examine as etapas a seguir antes de instalar uma atualização de dentro do console do Configuration Manager.  

###  <a name="bkmk_step1"></a>Etapa 1: Examine a lista de verificação de atualização  
Examine a lista de verificação de atualização aplicável para ações a serem tomadas antes de iniciar a atualização:

- Atualizar para a 1606: Consulte [lista de verificação para instalar a atualização 1606](../../../core/servers/manage/checklist-for-installing-update-1606.md).  

- Atualizar para 1610 de qualquer 1606: Consulte [lista de verificação para instalar atualização 1610](../../../core/servers/manage/checklist-for-installing-update-1610.md).  

- Atualize para 1702 da 1606 ou 1610: Consulte [lista de verificação para instalar atualização 1702](../../../core/servers/manage/checklist-for-installing-update-1702.md).

<!-- Removed as update guidance 6/6/2017. The Test DB Upgrade details are no longer recommended nor required. They live on in a new topic for customers who still want to use them. -->

###  <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a>Etapa 2: Executar o verificador de pré-requisitos antes de instalar uma atualização  
Antes de instalar uma atualização, considere executar a verificação de pré-requisitos para essa atualização. Se executar o pré-requisito antes de instalar uma atualização:  

-   Os arquivos de atualização serão replicados para outros sites antes de instalar a atualização.  

-   A verificação de pré-requisitos é executado automaticamente novamente quando você optar por instalar a atualização.  

Posteriormente, quando você instala a atualização, você pode configurar a atualização para ignorar os avisos de verificação de pré-requisitos.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Para executar o verificador de pré-requisitos antes de instalar uma atualização  

1.  No console do Configuration Manager, vá para **administração** > **atualizações e manutenção**.   

2.  Clique com botão direito no pacote de atualizações que você deseja executar a verificação de pré-requisitos.  

3.  Escolha **Executar verificação de pré-requisitos**.  

     Quando executar a verificação de pré-requisitos, o conteúdo da atualização é replicado para sites subordinados.  Você pode exibir o distmgr.log no site do servidor para confirmar que o conteúdo replica com êxito.  

4.  Para exibir os resultados da verificação, no console do Configuration Manager, vá para **monitoramento** > **atualizações e manutenção de Status** e procure o status do pré-requisito. Também pode ver o ConfigMgrPrereq.log no servidor do site para obter mais detalhes.  



##  <a name="bkmk_install"></a> Instalar atualizações na consola  
 Quando você estiver pronto para instalar atualizações do console do Configuration Manager, você começar com o site de nível superior da sua hierarquia. Este é o site de administração central ou um site primário autónomo.  

 É recomendável que você instale a atualização fora do horário comercial normal de cada site minimizar os efeitos nas operações corporativas. Isso ocorre porque a instalação da atualização pode incluir ações como reinstalar os componentes do site e funções do sistema de site.  

-   Os sites primários subordinados iniciam a atualização automaticamente, após o site de administração central concluir a instalação da atualização. Este é o padrão e recomendado de processo. No entanto, você pode usar [serviço windows para servidores de site](/sccm/core/servers/manage/service-windows) para controlar quando um site primário instala atualizações.  

-   Atualize manualmente os sites secundários de dentro do console do Configuration Manager após a conclusão da atualização do site pai primário. A atualização automática dos servidores de site secundários não é suportada.  

-   Quando você usa um console do Configuration Manager depois que o site é atualizado, você precisará atualizar o console.  

-  Depois que o servidor do site concluir com êxito a instalação de uma atualização, ela atualiza automaticamente todas as funções de sistema de site aplicável.  A única limitação é para pontos de distribuição. Ao instalar uma atualização, todos os pontos de distribuição não reinstale e ficar offline para atualizar ao mesmo tempo. Em vez disso, o servidor de site usa configurações de distribuição de conteúdo do site para distribuir a atualização para um subconjunto de pontos de distribuição por vez. O resultado é que apenas alguns pontos de distribuição ficar off-line para instalar a atualização. Pontos de distribuição que não começaram a atualização ou que concluiu a atualização permanecem online e é capaz de fornecer conteúdo aos clientes.


###  <a name="bkmk_overview"></a> Descrição geral da instalação da atualização na consola  
**1. Quando a instalação da atualização começa**  
É-lhe apresentado o Assistente de Atualizações, que apresenta uma lista de áreas de produto a cuja atualização se refere.  

-   Na página **Geral** do assistente, pode configurar **Avisos de pré-requisitos**.  
      -   Os erros de pré-requisitos interrompem sempre a instalação da atualização. Corrija os erros antes de você pode tentar novamente com êxito a instalação da atualização. Veja [Repetir a instalação de uma atualização falhada](#bkmk_retry) para obter mais informações.  

    -   Os avisos de pré-requisitos também podem interromper a instalação da atualização. Corrigi avisos antes de tentar novamente a instalação da atualização. Para obter mais informações, consulte [repetir a instalação de uma atualização com falha](#bkmk_retry).  
    -   A opção **ignorar os avisos de verificação de pré-requisitos e instalar essa atualização, independentemente dos requisitos ausentes** define uma condição para a instalação da atualização que ignora os avisos de pré-requisito. Isso permite que a instalação da atualização continuar. Se você não selecionar essa opção, a instalação de atualização para quando um aviso for encontrado. A menos que você tenha executado anteriormente a verificação de pré-requisitos e os avisos de pré-requisito fixos para um site, não recomendamos o uso dessa opção.  

      Em ambos os **administração** e **monitoramento** espaços de trabalho, as nó atualizações e manutenção inclui um botão na faixa de opções chamado **Ignorar avisos de pré-requisito**. Este botão fica disponível quando um pacote de atualização falha ao concluir a instalação devido a avisos de verificação de pré-requisitos. Por exemplo, instalar uma atualização sem usar a opção para ignorar os avisos de pré-requisito (de dentro do Assistente de atualizações). Interrompe a instalação da atualização com um estado de aviso de pré-requisito, mas sem erros. Mais tarde você pode escolher **Ignorar avisos de pré-requisito** na faixa de opções para disparar uma continuação automática da instalação de atualização que ignora os avisos de pré-requisito. Quando você usa essa opção, a instalação da atualização continua automaticamente depois de alguns minutos.



-   Quando uma atualização se aplica ao cliente do Configuration Manager, você tem a opção para testar a atualização do cliente com um conjunto limitado de clientes. Para obter mais informações, consulte [como testar atualizações do cliente em uma coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**2. Durante a instalação da atualização**  
Como parte da instalação da atualização, o Configuration Manager:  

-   Reinstala todos os componentes afetados, como funções de sistema de site ou o console do Configuration Manager.  

-   Gerencia as atualizações para os clientes com base nas seleções feitas para o piloto do cliente e para [atualizações automáticas do cliente](https://technet.microsoft.com/library/mt627885.aspx).  

-   Não reiniciará os servidores de sistema de site como parte da atualização, a menos que o .NET é instalado como parte de um pré-requisito de funções de sistema de site.  

> [!TIP]  
>  Quando as atualizações são instaladas, o Configuration Manager também atualiza o CD. Pasta mais recente. Essa pasta é usada durante a recuperação de site.  

**3. Monitorar o andamento de atualizações durante a instalação**  
Utilize o seguinte procedimento para monitorizar o progresso:  

-   No console do Configuration Manager: **Administração** > **atualizações e manutenção** nó. Este nó mostra o estado da instalação para todos os pacotes de atualização.


-   No console do Configuration Manager: **Monitoramento** > **visão geral** > **atualizações e manutenção de Status** nó. Esse nó mostra o status da instalação de apenas o pacote de atualização que está sendo instalado.  

    A instalação do pacote de atualização é dividida para as seguintes fases para facilitar o monitoramento. Para cada fase, detalhes adicionais incluem o arquivo de log para exibir para obter mais informações:  
    -   **Baixar** (nesta fase aplica-se somente para o site de nível superior em que o site de ponto de conexão de serviço é instalado.)   

    -   **Replicação**   

    -   **Verificação de Pré-requisitos**   

    -   **Instalação**    

    -   **Pós-instalação** ([tarefas pós-instalação](#post-installation-tasks) disponíveis a partir versão 1610.)  

-   Você pode exibir o **CMUpdate.log** arquivo  **&lt;ConfigMgr_Installation_Directory > \Logs**  

**4. Ao concluir a instalação da atualização**  
Após a instalação da primeira atualização do site ser concluída:  

-   Os sites primários filho instalam a atualização automaticamente. Não é necessária mais nenhuma ação.  

-   Sites secundários devem ser atualizados manualmente de dentro do console do Configuration Manager.
> [!TIP]
> Embora a versão de um site secundário não for exibido no console, você pode usar o SDK do Configuration Manager para confirmar a versão do site. Consulte [SMS_Site servidor WMI classe](https://technet.microsoft.com/library/hh442832(CMSDK.16).aspx).


-   Até que todos os sites da hierarquia tenham sido atualizados para a nova versão, a hierarquia funciona num modo com versões mistas. Para obter mais informações, veja [Interoperabilidade entre diferentes versões do System Center Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

**5.   Atualizar consoles do Configuration Manager**  
Depois de um site de administração central ou site primário, cada console do Configuration Manager que se conecta a esse site também deve atualizar. Ser-lhe-á pedido para atualizar uma consola:  

-   Quando você abre o console.  

-   Quando você vá para um novo nó em um console aberto.  

É recomendável que você instale a atualização imediatamente.  

Quando a atualização da consola estiver concluída, pode verificar se a versão da consola e do site está correta. Vá para **sobre o System Center Configuration Manager** no canto superior esquerdo do console.  

###  <a name="bkmk_toptier"></a> Para iniciar a instalação da atualização no site de nível superior  
No site de nível superior da sua hierarquia, no console do Configuration Manager, vá para **administração** > **atualizações e manutenção**, selecione um **disponível** atualizar e, em seguida, clique em **instalar pacote de atualização**.  

###  <a name="bkmk_secondary"></a> Para iniciar a instalação da atualização num site secundário  
Depois de atualizações de site primário do pai do site secundário, você pode atualizar o site secundário de dentro do console do Configuration Manager.  Para tal, utilize o **Assistente para Atualizar Site Secundário**.  

1.  No console do Configuration Manager, vá para **administração** > **configuração do Site** > **Sites**, selecione o site que você deseja atualizar e, em seguida, em que a página inicial do guia, no **Site** de grupo, escolha **atualizar**.  

2.  Clique em **Sim** para iniciar a atualização do site secundário.  

Para monitorar a instalação da atualização em um site secundário, selecione o servidor do site secundário. Em seguida, no **início** guia o **Site** de grupo, escolha **Mostrar Status da instalação**. Também pode adicionar a coluna **Versão** ao ecrã da consola, de modo a que possa ver a versão de cada site secundário.  

Depois de um site secundário com êxito atualizações, se o status no console não atualiza ou sugere a falha na atualização, usam o **Repetir instalação** opção. Essa opção não reinstalar a atualização de um site secundário que instalou com êxito a atualização, mas obriga o console para atualizar o status.

### <a name="post-installation-tasks"></a>Tarefas pós-instalação
A partir da versão 1610, você pode exibir informações sobre tarefas pós-instalação.

Quando um site instalar uma atualização, há várias tarefas que não é possível iniciar até após a conclusão da instalação no servidor do site de atualização. A seguir está uma lista de tarefas de pós-instalação que são essenciais para operações do site e hierarquia. Porque eles são essenciais, eles são monitorados ativamente. Tarefas adicionais que não são diretamente monitoradas incluem a reinstalação de funções do sistema de site. Para exibir o status de tarefas de pós-instalação críticos, selecione **instalação lançar** tarefa enquanto monitora a instalação da atualização para um site.

Nem todas as tarefas concluída imediatamente. Algumas tarefas não serão iniciados até a conclusão da instalação da atualização de cada site. Portanto, a nova funcionalidade, você pode esperar que pode ser atrasada até concluem essas tarefas. Por exemplo, como ativar novos recursos não inicia até que todos os sites concluir a instalação da atualização, novos recursos podem não ser visíveis por algum tempo.

As tarefas pós-instalação incluem:

-   **Instalar o serviço SMS_EXECUTIVE**
  -   Serviços fundamentais, que é executado no servidor do site.
  -   Reinstalação do serviço deve ser concluída rapidamente.


-   **Instalar o componente SMS_DATABASE_NOTIFICATION_MONITOR**
  -   Thread de componente do site essencial do serviço SMS_EXECUTIVE.
  -   Reinstalação do serviço deve ser concluída rapidamente.


-   **Instalar o componente SMS_HIERARCHY_MANAGER**
  -   Componente crítico de site que é executado no servidor do site.
  -   Responsável por reinstalar as funções do sistema de site nos servidores de sistema de site.  Não exibe status para reinstalação de função do sistema de sites individuais.
  -   Reinstalação do serviço deve ser concluída rapidamente.


-   **Instalar o componente SMS_REPLICATION_CONFIGURATION_MONITOR**
  -   Componente crítico de site que é executado no servidor do site.
  -   Reinstalação do serviço deve ser concluída rapidamente.


-   **Instalar o componente SMS_POLICY_PROVIDER**
  -   Componente crítico de site que é executado somente em sites primários.
  -   Reinstalação do serviço deve ser concluída rapidamente.


-   **Monitoramento de inicialização de replicação**   
  -   Isso exibe a apenas o site de administração central e sites primários filho.
  -   Dependente de SMS_REPLICATION_CONFIGURATION_MONITOR.
  -   Deve ser concluída rapidamente.


-   **Atualizando o pacote de pré-produção do cliente do Configuration Manager**    
  -   Isso exibe até mesmo ao cliente de pré-produção (também chamado de piloto do cliente) não está habilitado para uso.
  -   Não é iniciado até que todos os sites na hierarquia de concluir a instalação da atualização.


-   **Atualizar a pasta do cliente no servidor do Site**
  -   Isso não será exibido se você usar o cliente de pré-produção.  
  -   Deve ser concluída rapidamente.


-   **Pacote de atualização do cliente do Configuration Manager**
  -   Isso não será exibido se você usar o cliente de pré-produção.  
  -   Termina somente depois que todos os sites instalam a atualização.  


-   **Ativar recursos**
  -   Isso exibe apenas no site de nível superior da hierarquia.
  -   Não é iniciado até que todos os sites na hierarquia de concluir a instalação da atualização.
  -   Os recursos individuais não são exibidos.


##  <a name="bkmk_retry"></a> Repetir a instalação de uma atualização falhada  
Quando a ser instalado uma atualização falha, revise os comentários no console para identificar as resoluções para erros e avisos. Também pode ver o ConfigMgrPrereq.log no servidor do site para obter mais detalhes. Antes de tentar novamente a instalação de uma atualização, você deve corrigir erros e avisos deve ser corrigidas.  

Quando você estiver pronto para repetir a instalação de uma atualização, selecione a atualização com falha e, em seguida, escolha uma opção aplicável. O comportamento de repetição de instalação da atualização depende do nó em que você inicia a repetição e a opção de repetição que você usa.  

1.  **Repetir a instalação para a hierarquia:**  
Pode repetir a instalação de uma atualização para toda a hierarquia quando a atualização se encontra num dos seguintes estados:  

    -   Verificação de pré-requisitos aprovada com um ou mais avisos, e a opção de ignorar os avisos de verificação de pré-requisitos não foi definida no Assistente de atualização. (Valor da atualização para **Ignorar aviso de pré-requisito** no **atualizações e manutenção** nó é **não**.)   
    -   Falha no pré-requisito    
    -   Falha na instalação
    -   Falha na replicação do conteúdo para o site   

    Vá para **administração** > **atualizações e manutenção**, selecione a atualização e, em seguida, escolha uma das seguintes opções:  

    -   **Repita** - quando você executar **novamente** deste nó, a instalação da atualização for iniciada novamente e ignorará automaticamente os avisos de pré-requisito. Conteúdo da atualização também novamente replica replicação falhado anteriormente.
    - **Ignorar avisos de pré-requisito** -começando com a versão 1606, se a instalação da atualização será interrompido devido a um aviso, você pode escolher **Ignorar avisos de pré-requisito**. Esta ação permite continuar a instalação da atualização (após alguns minutos) e utiliza a opção para ignorar avisos de pré-requisitos.   

2.  **Repetir a instalação para o site:**  
 Pode repetir a instalação de uma atualização num site específico quando a atualização se encontra num dos seguintes estados:  

    -   Verificação de pré-requisitos aprovada com um ou mais avisos, e a opção de ignorar os avisos de verificação de pré-requisitos não foi definida no Assistente de atualização. (O valor das atualizações para **Ignorar aviso de pré-requisito** no nó atualizações e manutenção é **não**.)  
    -   Falha no pré-requisito    
    -   Falha na instalação    

    Vá para **monitoramento** > **visão geral** > **Status de manutenção do Site**, selecione a atualização e, em seguida, clique em uma das seguintes opções:

       - **Repita** - quando você executar **novamente** deste nó, reiniciar a instalação da atualização somente desse site. Ao contrário de execução **novamente** do **atualizações e manutenção** nó, essa repetição não ignora os avisos de pré-requisito.
       -    **Ignorar avisos de pré-requisito** -começando com a versão 1606, se a instalação da atualização será interrompido devido a um aviso, você pode clicar em **Ignorar avisos de pré-requisito**. Esta ação permite continuar a instalação da atualização (após alguns minutos) e utiliza a opção para ignorar avisos de pré-requisitos.

##  <a name="bkmk_after"></a> Após uma site instalar uma atualização  
Use a seguinte lista de verificação para concluir tarefas comuns e configurações que são feitas após a atualização do site.   

**Confirme a replicação site a site está ativa:** No console do Configuration Manager, acesse os locais a seguir para exibir o status e certifique-se de que a replicação está ativa:  

-   **Monitorização** > **Descrição geral** > **Hierarquia do Site**  

-   **Monitorização** > **Descrição geral** > **Replicação de Base de Dados**  

Para obter mais informações, consulte [monitorar replicação de infraestrutura de hierarquia e no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) e [sobre o Replication Link Analyzer](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Certifique-se de que os servidores de site e servidores do sistema de site remoto foram reiniciados (se necessário):** Analise a infraestrutura de site e certifique-se de que os servidores de site aplicável e servidores do sistema de site foram reiniciados com êxito. Normalmente, os servidores de site reinicie somente quando o Configuration Manager instala o .NET como um pré-requisito para uma função de sistema de site.  

 **Atualize consoles autônomos do Configuration Manager:** Certifique-se de que todos os consoles remotos do Configuration Manager estão atualize para a mesma versão. Ser-lhe-á pedido para atualizar a consola quando:  

-   Vá para um novo nó no console do.  

-   Abra o console.

**Reconfigure réplicas de banco de dados para pontos de gerenciamento em sites primários:** Se você usar réplicas de banco de dados para pontos de gerenciamento em sites primários, você deve desinstalar as réplicas de banco de dados antes de atualizar o site. Após atualizar um site primário, reconfigure a réplica da base de dados para pontos de gestão. Para obter mais informações, veja [Réplicas de bases de dados para pontos de gestão do System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigure quaisquer tarefas de manutenção de banco de dados desabilitadas antes da atualização:** Se você tiver desabilitado [tarefas de manutenção](../../../core/servers/manage/maintenance-tasks.md) em um site antes de instalar a atualização, reconfigure-no site. Use as mesmas configurações que estavam em vigor antes da atualização.  

**Atualize clientes:** Para obter informações, consulte [como atualizar clientes para computadores Windows no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

**Configurações adicionais:** Revise as alterações feitas antes de iniciar a atualização e, em seguida, restaure essas configurações em seus sites e hierarquia.  

##  <a name="bkmk_options"></a> Ativar funcionalidades opcionais de atualizações  
Quando uma atualização inclui um ou mais recursos opcionais, você terá a oportunidade de habilitar esses recursos em sua hierarquia.  Você pode habilitar recursos quando a instalação da atualização, ou você pode retornar ao console posteriormente e habilitar os recursos opcionais.

Para exibir os recursos disponíveis e seus status, no console, navegue até **administração** > **atualizações e manutenção** > **recursos**.

Quando um recurso não é opcional, ele é instalado automaticamente e não aparece no **recursos** nó.  


Quando você habilita um novo recurso ou o recurso de pré-lançamento, o Gerenciador de hierarquia do Configuration Manager (HMAN) deve processar a alteração antes que esse recurso se torne disponível. Processamento da alteração geralmente é imediato, mas pode levar até 30 minutos para ser concluída, dependendo do ciclo de processamento HMAN. Depois que a alteração é processada, você deve reiniciar o console antes de exibir a nova interface do usuário relacionado a esse recurso.


##  <a name="bkmk_prerelease"></a> Utilizar as funcionalidades da versão de pré-lançamento de atualizações
Recursos de pré-lançamento são incluídos na ramificação atual para testes iniciais em um ambiente de produção. Você pode usar esses recursos em seu ambiente de produção, mas eles não são considerados produção pronto. Saiba mais sobre [recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features), inclusive como habilitá-las em seu ambiente.             


## <a name="known-issues"></a>Problemas conhecidos

###  <a name="bkmk_faq"></a>Por que eu não vejo determinadas atualizações em Meu console?  
 Se você não encontrar uma atualização específica em seu console após uma sincronização bem-sucedida com o serviço de nuvem da Microsoft, isso pode ser porque:  

-   A atualização requer uma configuração que a sua infraestrutura não utiliza ou a versão atual do produto não cumpre um pré-requisito para receber a atualização.  

     Se você acredita que você tenha as configurações necessárias e pré-requisitos para uma atualização ausente, confirme que o ponto de conexão de serviço está no modo online. Em seguida, use o **verificar se há atualizações** opção o **atualizações e manutenção** nó para forçar uma verificação.  Se estiver no modo offline, tem de utilizar a ferramenta de ligação de serviço para sincronizar manualmente com o serviço em nuvem.  

-   Sua conta não tem as permissões de administração corretas baseadas em função para exibir as atualizações no console do Configuration Manager.

    Veja [Permissões para gerir atualizações de](../../../core/servers/manage/install-in-console-updates.md#assign-permissions-to-view-and-manage-updates-and-features) neste tópico para obter informações sobre as permissões necessárias para ver atualizações e ativar funcionalidades a partir da consola.

### <a name="why-do-i-see-two-updates-for-version-1610"></a>Por que vejo duas atualizações para a versão 1610?
Ao exibir as atualizações no console, você poderá ver duas atualizações para instalar a versão 1610. Essas atualizações têm datas diferentes. Ambos são exibidos quando uma das seguintes condições for verdadeira:   
-   Você instalou uma versão anterior (como 1606) após a versão 1610 se tornaram disponível

-   Sua hierarquia executa a versão 1511 ou 1602 e não foram capazes de baixar a versão 1606

Não há atualização duas versões para a versão 1610 porque esta atualização foi lançada novamente após algumas pequenas alterações para alguns binários do arquivo foram feitas. Essas alterações não afetam a funcionalidade do Configuration Manager ou a atualização.

Quando ambas as atualizações estão disponíveis no console do, é recomendável que você instale a atualização com a data mais recente. No entanto, porque ambas as atualizações fornecem a mesma funcionalidade, quando você já tiver instalado um deles não precisa tomar uma ação adicional.
-   Se você tiver instalado a atualização anterior, você não precisa instalar a atualização com a data mais recente. No entanto, se você instalar a atualização mais recente depois de instalar a primeira atualização, atualizará os binários em questão. Não ocorre nenhuma alteração adicional, e nenhuma ação adicional de sua parte é necessários.

-   Se você instalou a atualização mais recente e, em seguida, instale a atualização com a data mais antiga, nenhuma ação adicional é necessária. Isso ocorre porque os binários mais recentes que você já instalou não são substituídos por esses mesmos binários da atualização original.


---
title: "As atualizações de consola | Documentos do Microsoft"
description: "System Center Configuration Manager sincroniza com a nuvem da Microsoft para obter atualizações que pode instalar a consola."
ms.custom: na
ms.date: 4/7/2017
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
ms.sourcegitcommit: d94acac84f052a01de9d9c9f65f237c0006c45b8
ms.openlocfilehash: 29a55948a1897e1345ba14ec685b9288a844feaa
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Instalar atualizações na consola para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager sincroniza com o serviço de nuvem da Microsoft para obter atualizações. Em seguida, pode instalar estas atualizações a partir da consola do Configuration Manager.

## <a name="get-available-updates"></a>Obter as atualizações disponíveis
Apenas as atualizações aplicáveis à sua infraestrutura e versão são transferidas e disponibilizadas na sua hierarquia. Esta sincronização pode ser automático ou manual, dependendo de como configurar o ponto de ligação de serviço para a hierarquia:

-   No **modo online**, o ponto de ligação de serviço liga automaticamente ao serviço em nuvem da Microsoft e transfere as atualizações aplicáveis.  

     Por predefinição, o Configuration Manager verifica a existência de novas atualizações a cada 24 horas. Também pode verificar existência de atualizações imediatamente escolhendo **procurar atualizações** no **administração** > **atualizações e a manutenção** nó da consola do Configuration Manager. (Antes da versão 1702, este nó foi em **administração** > **serviços em nuvem**.)

-   No **modo offline**, o ponto de ligação de serviço não ligar o serviço de nuvem da Microsoft. Tem manualmente [utilizar a ferramenta de ligação de serviço para o System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md) para transferir e, em seguida, importar as atualizações disponíveis.  

> [!NOTE]  
>  Para além das atualizações que obtém quando efetuar a sincronização com o serviço de nuvem Microsoft, fora de banda correções que são instalados utilizando o [ferramenta de atualização de registo](http://technet.microsoft.com/library/mt691544.aspx) também são importados para a consola, onde pode, em seguida, selecioná-los para instalar.  

Após as atualizações são sincronizadas pode visualizá-los na consola do Configuration Manager ao aceder a **administração** > **atualizações e a manutenção** nó:  

-   As atualizações não instaladas são apresentadas como **Disponível**.

-   As atualizações instaladas são apresentadas como **Instalada**.  É apresentada apenas a atualização instalada mais recentemente. Pode escolher o **histórico** botão no friso para anteriormente a ver atualizações instaladas.



Antes de configurar o ponto de ligação de serviço, compreender e utiliza o plano para o respetivo adicionais. As seguintes utilizações podem afetar a forma como configurar esta função do sistema de sites:  

-   O ponto de ligação de serviço é utilizado para carregar as informações de utilização sobre o seu site. Estas informações ajudam o serviço em nuvem da Microsoft a identificar as atualizações que estão disponíveis para a versão atual da sua infraestrutura. Para obter mais informações, consulte o artigo [diagnósticos e dados de utilização para o System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

-   O ponto de ligação de serviço é utilizado para gerir dispositivos com o Microsoft Intune e utilizar a gestão de dispositivos móveis no local do Configuration Manager. Para obter mais informações, consulte o artigo [gestão de dispositivos móveis (MDM) híbrida com o System Center Configuration Manager e o Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

Para melhor compreender o que acontece quando as atualizações são transferidas, consulte:  

-   [Fluxograma - transferência de atualizações para o System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md)

-   [Fluxograma - replicação de atualização para o System Center Configuration Manager](../../../core/servers/manage/update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Atribuir permissões para ver e gerir as atualizações e funcionalidades
Para ver as atualizações na consola, um utilizador tem de ser atribuído uma função de segurança de administração baseada em funções que inclui a classe de segurança com o nome **atualizar pacotes**. Esta classe concede acesso para ver e gerir as atualizações na consola do Configuration Manager.    

**Sobre a classe Pacotes de atualização:**  
Por predefinição, **Pacotes de atualização** (SMS_CM_Updatepackages) faz parte dos seguintes direitos de acesso incorporados nas permissões listadas:
 -  **Administrador Total** com permissões de **Modificação** e **Leitura** :
    -   Um utilizador com esta função de segurança e acesso ao **todos os** âmbito de segurança pode ver atualizações, instalar atualizações e ativar funcionalidades durante a instalação e ativar funcionalidades individuais após a atualização é instalada.
    - Um utilizador com esta função de segurança e acesso ao **predefinido** âmbito de segurança pode ver atualizações, instalar atualizações e ativar funcionalidades durante a instalação e ver funcionalidades depois de instalar uma atualização. Mas este utilizador não é possível ativar as funcionalidades após a atualização é instalada.

- **Analista só de leitura** com permissões de **Leitura** :
  -  Um utilizador com esta função de segurança e acesso ao **predefinido** âmbito pode ver atualizações, mas não instalá-los. Este utilizador também pode ver funcionalidades após uma atualização tem instalada, mas não é possível ativá-las.

**Permissões necessárias para as atualizações e manutenção:**   
  - Utilize uma conta à qual esteja atribuído um direito de acesso que inclua a classe **Pacotes de atualização** com as permissões de **Modificação** e **Leitura** .
  - O âmbito **Predefinição** tem de ser atribuído à conta.

**Permissoins para apenas ver as atualizações**:
  - Utilize uma conta à qual esteja atribuído um direito de acesso que inclua a classe **Pacotes de atualização** apenas com a permissão de **Leitura** .
  - O âmbito **Predefinição** tem de ser atribuído à conta.

**As permissões necessárias para ativar funcionalidades após as atualizações são instaladas:**
  -  Utilize uma conta à qual esteja atribuído um direito de acesso que inclua a classe **Pacotes de atualização** com as permissões de **Modificação** e **Leitura** .
  -  O âmbito **Tudo** tem de ser atribuído à conta.






##  <a name="bkmk_beforeinstall"></a> Antes de instalar uma atualização na consola  
 Reveja os seguintes passos antes de instalar uma atualização a partir da consola do Configuration Manager.  

###  <a name="bkmk_step1"></a>Passo 1: Reveja a lista de verificação de atualização  
Reveja a lista de verificação de atualização aplicável para ações a efetuar antes de iniciar a atualização:

- Atualizar para 1606: Consulte o artigo [lista de verificação para instalar atualizar 1606](../../../core/servers/manage/checklist-for-installing-update-1606.md).  

- Atualizar para 1610 a partir de qualquer um dos 1606: Consulte o artigo [lista de verificação para instalar atualizar 1610](../../../core/servers/manage/checklist-for-installing-update-1610.md).  

- Atualizar para 1702 1606 ou 1610: Consulte o artigo [lista de verificação para instalar atualizar 1702](../../../core/servers/manage/checklist-for-installing-update-1702.md).

###  <a name="bkmk_step2"></a>Passo 2: Teste a atualização de base de dados antes de instalar uma atualização  
As informações neste passo aplica-se apenas quando estiver a instalar um *atualizar* para um site do System Center Configuration Manager. Se for *atualizar* um site do System Center 2012 Configuration Manager para System Center Configuration Manager, consulte o artigo [testar a atualização de base de dados do site](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#a-namebkmktesta-test-the-site-database-upgrade).

Antes de instalar uma atualização de novo na hierarquia, como atualizar 1610, pode testar a atualização da sua base de dados do site. O nome da opção da linha de comandos que utilizar para testar a instalação de uma atualização para uma cópia de segurança da sua base de dados do site é **testdbupgrade**.  

Se instalar uma atualização falhar, não deverá efetuar uma recuperação do site. Em vez disso, pode tentar novamente a instalação da atualização. Assim, embora o teste da atualização da base de dados é menos crítico que se encontrava em versões anteriores do produto, como o System Center 2012 Configuration Manager, recomendamos-lo.


#### <a name="to-run-testdbupgrade-before-installing-an-update"></a>Para executar testdbupgrade antes de instalar uma atualização  

1.  Obter um conjunto de ficheiros de origem a partir de **CD. Mais recente** pasta de um site que executa a versão que pretende atualizar. Isto poderá exigir a primeira instalação de um site num laboratório ou testar ambiente que é executado dessa versão do System Center Configuration Manager.  

     O **CD. Mais recente** pasta para um site tem os ficheiros de origem para essa versão. Tem de utilizar estes ficheiros de origem para executar o teste de atualização da sua base de dados do site. Para obter mais informações, veja [The CD.Latest folder for System Center Configuration Manager (A pasta CD.Latest do System Center Configuration Manager)](../../../core/servers/manage/the-cd.latest-folder.md).  

     Por exemplo, se o seu site for executada versão 1606 e pretende atualizar para 1610, tem de obter um CD. Pasta mais recente a partir de um site que já foi atualizado para a versão 1610. Normalmente, pode instalar um site novo e temporário num laboratório e atualizar que para a versão 1610 para criar o CD. Pasta mais recente com os ficheiros necessários.  

2.  Copie o CD. Pasta mais recente para uma localização na instância do SQL Server que será utilizada para executar o teste da atualização da base de dados.

3.  Criar uma cópia de segurança da base de dados do site que pretende testar a atualização e, em seguida, restaurar uma cópia dessa base de dados para uma instância do SQL Server que não aloje um site do Configuration Manager. O SQL Server instnace tem de utilizar a mesma edição do SQL Server como a base de dados do site.  

4.  Após restaurar a cópia da base de dados, execute **configuração** a partir do CD. Pasta mais recente que copiou do seu ambiente de laboratório ou de testes. Ao executar a Configuração, utilize a opção da linha de comandos **/TESTDBUPGRADE** . Se a instância do SQL Server que aloja a cópia da base de dados não for a instância predefinida, terá de fornecer também os argumentos da linha de comandos para identificar a instância que aloja a cópia da base de dados do site.  

     Por exemplo, suponha que pretende atualizar uma base de dados do site com o nome de base de dados SMS_ABC. Restaura uma cópia desta base de dados do site para uma instância suportada do SQL Server com o nome de instância DBTest. Para testar uma atualização desta cópia da base de dados do site, utilize a seguinte linha de comandos: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     Pode encontrar Setup.exe na seguinte localização do suporte de dados de origem para o System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

5.  Na instância do SQL Server em que executou o teste da atualização da base de dados, monitorize o progresso e êxito no ficheiro ConfigMgrSetup.log, na raiz da unidade do sistema.  

     Se o teste da atualização falhar, corrija eventuais problemas relacionados com a falha de atualização de base de dados de site, crie uma nova cópia de segurança da base de dados do site e, em seguida, testar a atualização da nova cópia da base de dados do site.  

     Após a conclusão do processo com êxito, poderá eliminar a cópia da base de dados.  

    > [!NOTE]  
    >  O restauro da cópia da base de dados do site utilizada para o teste da atualização não é suportado para utilização como base de dados de qualquer site.  

###  <a name="bkmk_step3"></a>Passo 3: Executar o Verificador de pré-requisitos antes de instalar uma atualização  
Antes de instalar uma atualização, considere executar a verificação de pré-requisitos para essa atualização. Se executar o pré-requisito antes de instalar uma atualização:  

-   Os ficheiros de atualização são replicados para outros sites antes de instalar a atualização.  

-   A verificação de pré-requisitos será executada automaticamente novamente quando optar por instalar a atualização.  

Mais tarde, quando instala a atualização, tem a opção para configurar a atualização a ignorar avisos de verificação de pré-requisitos.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Para executar o verificador de pré-requisitos antes de instalar uma atualização  

1.  Na consola do Configuration Manager, aceda a **administração** > **atualizações e a manutenção**.   

2.  Clique com o botão direito do rato no pacote de atualização para o qual pretende executar a verificação de pré-requisitos.  

3.  Escolha **Executar verificação de pré-requisitos**.  

     Quando executar a verificação de pré-requisitos, o conteúdo da atualização é replicado para sites subordinados.  Pode ver o distmgr no site do servidor para confirmar que o conteúdo é replicado com êxito.  

4.  Para ver os resultados da verificação, na consola do Configuration Manager, aceda ao **monitorização** > **atualizações e o estado de manutenção** e procure o estado de pré-requisitos. Também pode ver o ConfigMgrPrereq.log no servidor do site para obter mais detalhes.  



##  <a name="bkmk_install"></a> Instalar atualizações na consola  
 Quando estiver pronto para instalar atualizações a partir da consola do Configuration Manager, comece com o site de nível superior da hierarquia. Este é o site de administração central ou um site primário autónomo.  

 Recomendamos que planeie instalar a atualização fora do horário comercial normal para cada site. O processo de instalação da atualização e as respetivas ações para reinstalar os componentes do site e funções de sistema de sites terão o efeito, pelo menos, nas suas operações de negócio.  

-   Os sites primários subordinados iniciam a atualização automaticamente, após o site de administração central concluir a instalação da atualização. Este é o predefinido e recomendado processo. No entanto, pode utilizar [windows dos servidores do site do serviço](/sccm/core/servers/manage/service-windows) para controlar quando um site primário instala as atualizações.  

-   Tem de atualizar manualmente os sites secundários a partir da consola do Configuration Manager após a conclusão da atualização do site primário principal. A atualização automática dos servidores de site secundários não é suportada.  

-   Quando utiliza uma consola do Configuration Manager após o site é atualizado, lhe for pedido para atualizar a consola.  

-  Depois do servidor do site concluir a instalação de uma atualização com êxito, atualiza automaticamente todas as funções de sistema de sites aplicável.  O caveat apenas a esta destina-se a pontos de distribuição. Ao instalar uma atualização, todos os pontos de distribuição não reinstale e ficam offline para atualizar ao mesmo tempo. Em vez disso, o servidor de site utiliza as definições de distribuição de conteúdo do site para distribuir a atualização a um subconjunto dos pontos de distribuição de cada vez. O resultado é que alguns pontos de distribuição ficam offline para instalar a atualização. Isto permite que os pontos de distribuição que ainda não tiver começado atualizar ou que concluiu a atualização para permanecer online e poderá fornecer conteúdo aos clientes.


###  <a name="bkmk_overview"></a> Descrição geral da instalação da atualização na consola  
**1. Quando inicia a instalação da atualização**  
É-lhe apresentado o Assistente de Atualizações, que apresenta uma lista de áreas de produto a cuja atualização se refere.  

-   Na página **Geral** do assistente, pode configurar **Avisos de pré-requisitos**.  
      -   Os erros de pré-requisitos interrompem sempre a instalação da atualização. É necessário corrigir erros antes de pode repetir a instalação da atualização com êxito. Veja [Repetir a instalação de uma atualização falhada](#bkmk_retry) para obter mais informações.  

    -   Os avisos de pré-requisitos também podem interromper a instalação da atualização. Deve corrigir avisos antes de repetir a instalação da atualização. Veja [Repetir a instalação de uma atualização falhada](#bkmk_retry) para obter mais informações.  
    -   Selecionar a opção **ignorar avisos de verificação de pré-requisitos e instalar esta atualização, independentemente de requisitos em falta**, define uma condição para a instalação da atualização que ignora os avisos de pré-requisitos. Isto permite que a instalação da atualização continuar. Se não selecionar esta opção, a instalação da atualização irá parar quando for detetado um aviso. A menos que tenha sido executada anteriormente a verificação de pré-requisitos e os avisos de pré-requisitos fixos para um site, não é recomendada a utilização desta opção.  

      Em ambos os **administração** e **monitorização** as áreas de trabalho, as atualizações e manutenção nó inclui um botão no friso com o nome **ignorar os avisos de pré-requisitos**. Este botão fica disponível quando um pacote de atualização não consegue concluir a instalação devido a avisos de verificação de pré-requisitos. Por exemplo, se instalar uma atualização sem utilizar a opção para ignorar os avisos de pré-requisitos (a partir no Assistente para atualizações), e que Atualize deixa de instalação com um Estado de aviso de pré-requisitos, mas não existem erros, pode escolher mais tarde **ignorar os avisos de pré-requisitos** a partir do friso para acionar uma continuação automática dessa instalação de atualização, em seguida, ignora os avisos de pré-requisitos. Quando utiliza esta opção, a instalação da atualização continua automaticamente após alguns minutos.



-   Quando uma atualização aplica-se para o cliente do Configuration Manager, é apresentada com a opção para testar a atualização do cliente com um conjunto limitado de clientes. Para obter mais informações, consulte o artigo [como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**2. Durante a instalação da atualização**  
Como parte da instalação de atualização do Configuration Manager:  

-   Reinstala quaisquer componentes afetados, como funções do sistema de site ou consola do Configuration Manager.  

-   Gere as atualizações para clientes com base nas seleções que efetuou para cliente piloting e para [atualizações automáticas de cliente](https://technet.microsoft.com/library/mt627885.aspx).  

-   Não terá de reiniciar os servidores de sistema de sites como parte da atualização (exceto se .NET é instalado como parte de um pré-requisito de funções de sistema de sites).  

> [!TIP]  
>  Quando as atualizações são instaladas, o Configuration Manager também atualiza o CD. Pasta mais recente. Esta pasta é utilizada durante uma recuperação do site.  

**3. Monitorizar o progresso das atualizações de forma elas podem instalá**  
Utilize o seguinte procedimento para monitorizar o progresso:  

-   Na consola do Configuration Manager: **Administração** > **atualizações e a manutenção** nó. Este nó mostra o estado da instalação para todos os pacotes de atualização.


-   Na consola do Configuration Manager: **Monitorização** > **descrição geral** > **atualizações e o estado de manutenção** nó. Este nó mostra o estado de instalação de apenas o pacote de atualização que está atualmente a ser instalado.  

  A instalação do pacote de atualização é reduzida para as seguintes fases, para facilitar a monitorização. Para cada fase, detalhes adicionais incluem o ficheiro de registo para ver para obter mais informações.:  
    -   **Transferir** (esta fase aplica-se apenas para o site de nível superior onde a função de sistema de sites de ponto de ligação de serviço é instalada.)
    -   **Replicação**
    -   **Verificação de Pré-requisitos**
    -   **Instalação**
    -   **Publicar instalação** (esta fase é disponíveis a partir versão 1610).

-   Pode ver o **CMUpdate.log** de ficheiros no  **&lt;ConfigMgr_Installation_Directory > \Logs**  

**4. Quando concluir a instalação da atualização**  
Após a instalação da primeira atualização do site ser concluída:  

-   Os sites primários subordinados irão instalar a atualização automaticamente. Não é necessária mais nenhuma ação.  

-   Os sites secundários tem de ser atualizados manualmente a partir da consola do Configuration Manager.
> [!TIP]
> Apesar da versão de um site secundário não apresentados na consola, pode utilizar o SDK do Gestor de configuração para confirmar a versão de um site. Consulte o artigo [SMS_Site servidor WMI classe](https://technet.microsoft.com/library/hh442832(CMSDK.16).aspx).


-   Até que todos os sites da hierarquia tenham sido atualizados para a nova versão, a hierarquia funciona num modo com versões mistas. Para obter mais informações, veja [Interoperabilidade entre diferentes versões do System Center Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

**5.   Atualizar consolas do Configuration Manager**  
Depois de um site de administração central ou de atualizações de sites primário, cada consola do Configuration Manager que liga a esse site tem também de atualizar. Ser-lhe-á pedido para atualizar uma consola:  

-   Quando abre a consola.  

-   Quando acede a um novo nó numa consola aberta.  

Recomendamos que instale a atualização imediatamente.  

Quando a atualização da consola estiver concluída, pode verificar se a versão da consola e do site está correta. Aceda a **sobre o System Center Configuration Manager** no canto superior esquerdo da consola.  

###  <a name="bkmk_toptier"></a> Para iniciar a instalação da atualização no site de nível superior  
No site de nível superior da hierarquia, na consola do Configuration Manager vá para **administração** > **atualizações e a manutenção**, selecione um **disponível** atualizar e, em seguida, clique em **instalar o pacote de atualização**.  

###  <a name="bkmk_secondary"></a> Para iniciar a instalação da atualização num site secundário  
Depois de um site primário do elemento principal de sites secundários for atualizado, em seguida, pode atualizar o site secundário a partir da consola do Configuration Manager.  Para tal, utilize o **Assistente para Atualizar Site Secundário**.  

1.  Na consola do Configuration Manager, aceda a **administração** > **configuração do Site** > **Sites**, selecione o site que pretende atualizar e, em seguida, na casa separador, no **Site** grupo, selecione **atualizar**.  

2.  Clique em **Sim** para iniciar a atualização do site secundário.  

Para monitorizar a instalação da atualização num site secundário, selecione o servidor de site secundário. Em seguida, no **base** separador o **Site** grupo, selecione **Mostrar estado da instalação**. Também pode adicionar a coluna **Versão** ao ecrã da consola, de modo a que possa ver a versão de cada site secundário.  

Depois de um site secundário é atualizado com êxito, se o estado na consola do não é atualizado ou sugere a atualização já falhou, pode utilizar o **tente instalar novamente** opção. Esta opção não reinstalar a atualização de um site secundário que instalou com êxito a atualização, mas irá forçar a consola para atualizar o estado.


##  <a name="bkmk_retry"></a> Repetir a instalação de uma atualização falhada  
Quando uma atualização falha ser instalada, reveja os comentários na consola, para identificar resoluções avisos e erros. Também pode ver o ConfigMgrPrereq.log no servidor do site para obter mais detalhes. Antes de repetir a instalação de uma atualização, deve corrigir os erros e deve resolver os avisos.  

Quando estiver pronto para tentar novamente a instalação de uma atualização, selecione a atualização falha e, em seguida, escolha uma opção aplicável. O comportamento de repetição de instalação de atualização depende do nó onde começar a repetição e a opção de repetição que utilizar.  

1.  **Repetir a instalação para a hierarquia:**  
Pode repetir a instalação de uma atualização para toda a hierarquia quando a atualização se encontra num dos seguintes estados:  

    -   Verificação de pré-requisitos foi passada com avisos de um ou mais, e a opção para ignorar avisos de verificação de pré-requisitos não foi definida no Assistente de atualização. (Valor da atualização para **ignorar aviso de pré-requisitos** no **atualizações e a servir** nó é **não**.)   
    -   Falha no pré-requisito    
    -   Falha na instalação
    -   Falha na replicação do conteúdo para o site   

    Aceda a **administração** > **atualizações e a manutenção**, selecione a atualização e, em seguida, escolha um dos seguintes procedimentos:  

    -   **Repita** - ao executar **repita** a partir de neste nó, a atualização instalar for iniciada novamente e será automaticamente ignorar os avisos de pré-requisitos. Também irá replicar novamente o conteúdo para a atualização se a replicação tiver falhado anteriormente.
    - **Ignorar os avisos de pré-requisitos** -a partir do versão 1606, se a atualização instalar deixa devido a um aviso, pode então escolher **ignorar os avisos de pré-requisitos**. Esta ação permite continuar a instalação da atualização (após alguns minutos) e utiliza a opção para ignorar avisos de pré-requisitos.   

2.  **Repetir a instalação para o site:**  
 Pode repetir a instalação de uma atualização num site específico quando a atualização se encontra num dos seguintes estados:  

    -   Verificação de pré-requisitos foi passada com avisos de um ou mais, e a opção para ignorar avisos de verificação de pré-requisitos não foi definida no Assistente de atualização (o valor para as atualizações **ignorar aviso de pré-requisitos** as atualizações e o nó manutenção é **não**.)  
    -   Falha no pré-requisito    
    -   Falha na instalação    

    Aceda a **Monitorização** > **Descrição geral** > **Estado de Manutenção do Site**, selecione a atualização e, em seguida, clique numa das seguintes opções:

       - **Repita** - ao executar **repita** a partir deste nó que reinicie a instalação da atualização apenas nesse site. Ao contrário de execução **repita** a partir de **atualizações e a manutenção** nó, este repetição não ignorar os avisos de pré-requisitos.
       -    **Ignorar os avisos de pré-requisitos** -a partir do versão 1606, se a atualização instalar deixa devido a um aviso, pode, em seguida, clicar em **ignorar os avisos de pré-requisitos**. Esta ação permite continuar a instalação da atualização (após alguns minutos) e utiliza a opção para ignorar avisos de pré-requisitos.

##  <a name="bkmk_after"></a> Após uma site instalar uma atualização  
Utilize a lista de verificação seguinte para concluir tarefas e configurações que são efetuadas após um site é atualizado comuns.   

**Confirme a replicação de site para site está ativa:** Na consola do Configuration Manager, aceda às seguintes localizações para ver o estado e certifique-se de que a replicação está ativa:  

-   **Monitorização** > **Descrição geral** > **Hierarquia do Site**  

-   **Monitorização** > **Descrição geral** > **Replicação de Base de Dados**  

Para obter mais informações, consulte o artigo [monitorizar a infraestrutura hierarquia e replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) e [sobre o analisador de ligações de replicação](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Confirme que os servidores de sites e servidores do sistema de sites remoto tem reiniciado (se necessário):** Reveja a sua infraestrutura de sites e certifique-se de que os servidores de sites aplicável e servidores de sistema de sites (remotos a partir do servidor do site) ser reiniciado com êxito.  Normalmente, isto é esperado apenas quando o Configuration Manager .NET é instalado como um pré-requisito de uma função de sistema de sites.  

 **Atualize consolas do Configuration Manager autónomo:** Certifique-se de que todas as consolas remotas do Configuration Manager estão a atualização para a mesma versão. Ser-lhe-á pedido para atualizar a consola quando:  

-   Ir para um novo nó na consola.  

-   Abra a consola.

**Reconfigure réplicas de base de dados para pontos de gestão em sites primários:** Se utilizar réplicas de base de dados para pontos de gestão em sites primários, tem de desinstalar as réplicas de base de dados antes de atualizar o site. Após atualizar um site primário, reconfigure a réplica da base de dados para pontos de gestão. Para obter mais informações, veja [Réplicas de bases de dados para pontos de gestão do System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigure as tarefas de manutenção de base de dados desativadas antes da atualização:** Se tiver desativado a base de dados [tarefas de manutenção para o System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) num site antes da atualização, reconfigure essas tarefas no site. Utilize as mesmas definições que se encontravam em vigor antes da atualização.  

**Atualize os clientes:** Para obter informações sobre como atualizar clientes existentes e sobre como instalar novos clientes, veja [Como atualizar clientes em computadores Windows no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

**Configurações adicionais:** Rever as alterações efetuadas antes de iniciar a atualização e, em seguida, restaurar essas configurações para sites e da hierarquia.  

##  <a name="bkmk_options"></a> Ativar funcionalidades opcionais de atualizações  
Quando instala uma atualização que inclui uma ou mais funcionalidades opcionais, terá a oportunidade de ativar essas funcionalidades na sua hierarquia.  Pode por isso, a hora que a atualização é instalada, ou pode volte mais tarde para a consola e ativar as funcionalidades opcionais.

Para ver o estado e funcionalidades disponíveis, na consola de navegar para **administração** > **atualizações e a manutenção** > **funcionalidades**.

Quando uma funcionalidade não é opcional, este é instalado automaticamente e não for apresentada a **funcionalidades** nó.  


Quando ativa uma nova funcionalidade ou a versão de pré-lançamento funcionalidade, o Gestor da hierarquia do Configuration Manager (HMAN) tem de processar a alteração para que essa funcionalidade fica disponível. Processamento da alteração é frequentemente imediato, mas pode demorar até 30 minutos a concluir, dependendo do ciclo de processamento de HMAN. Após a alteração é processada, é necessário reiniciar a consola antes de poder visualizar a nova IU relacionados com essa funcionalidade.


##  <a name="bkmk_prerelease"></a> Utilizar as funcionalidades da versão de pré-lançamento de atualizações
Funcionalidades da versão de pré-lançamento são funcionalidades que estão incluídas no ramo atual para iniciais de teste num ambiente de produção. Estas funcionalidades devem não ser consideradas produção pronto, mas podem ser utilizadas no seu ambiente de produção. Para obter mais informações sobre as funcionalidades da versão de pré-lançamento, incluindo como ativá-las no seu ambiente, consulte o artigo [funcionalidades da versão de pré-lançamento](/sccm/core/servers/manage/pre-release-features).             


## <a name="known-issues"></a>Problemas conhecidos

###  <a name="bkmk_faq"></a>Por que motivo não vejo determinadas atualizações na minha consola?  
 Se não conseguir localizar uma atualização específica (ou quaisquer atualizações) a consola depois de uma sincronização com êxito com o serviço de nuvem Microsoft, tal poderá acontecer porque:  

-   A atualização requer uma configuração que a sua infraestrutura não utiliza ou a versão atual do produto não cumpre um pré-requisito para receber a atualização.  

     Se achar que tem as configurações necessárias ou a corresponder aos outros pré-requisitos para uma atualização em falta, certifique-se de que o ponto de ligação de serviço está no modo online. Em seguida, utilize o **procurar atualizações** opção o **atualizações e a manutenção** nó para forçar uma verificação.  Se estiver no modo offline, tem de utilizar a ferramenta de ligação de serviço para sincronizar manualmente com o serviço em nuvem.  

-   A conta não possui as permissões de administração baseada em funções correta para ver as atualizações na consola do Configuration Manager.

    Veja [Permissões para gerir atualizações de](../../../core/servers/manage/install-in-console-updates.md#assign-permissions-to-view-and-manage-updates-and-features) neste tópico para obter informações sobre as permissões necessárias para ver atualizações e ativar funcionalidades a partir da consola.

### <a name="why-do-i-see-two-updates-for-version-1610"></a>Por que razão vejo duas atualizações para a versão 1610
Quando as atualizações a ver na consola, poderá ver dois atualizações a instalar a versão 1610. Estas atualizações tem datas diferentes. Isto acontece quando um dos seguintes é verdadeiro:   
-    Instalou uma versão anterior (como 1606) após a disponibilização de versão 1610

-    Hierarquia executa versão 1511 ou 1602 e não foram capazes de transferir a versão 1606

Existem dois atualização versões para a versão 1610 porque esta atualização foi lançada novamente após alguns pequenas alterações para alguns binários de ficheiro foram efetuadas. Estas alterações não afetam a funcionalidade do Configuration Manager ou a atualização.

Quando ambas as atualizações estão disponíveis na sua consola, recomendamos que instale a atualização com a data mais recente. No entanto, uma vez que ambas as atualizações fornecem a mesma funcionalidade, se já instalou uma delas não é necessário efetuar qualquer ação adicional.
-    Se tiver instalado anteriormente a atualização anterior, não é necessário instalar a atualização com a data mais recente. No entanto, se instalar a atualização mais recente depois de ter instalada a atualização primeiro, irão atualizar os binários em questão, mas sem alterações adicionais ocorre e não existem ações adicionais da sua parte são necessárias.

-    Se anteriormente instalada a atualização mais recente e, em seguida, instale a atualização com a data mais antiga, é necessária nenhuma ação adicional. Isto acontece porque os binários da mais recentes já instalou não serão substituídos por essas binários mesmos a partir da atualização original.


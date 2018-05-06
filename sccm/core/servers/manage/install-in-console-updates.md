---
title: Atualizações na consola
titleSuffix: Configuration Manager
description: Instalar atualizações para o Configuration Manager a partir da nuvem da Microsoft
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9edf02333ec4ce272e69a896ed22e97fa6de0955
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Instalar atualizações na consola para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager sincroniza com o serviço de nuvem da Microsoft para obter atualizações. Em seguida, pode instalar estas atualizações a partir da consola do Configuration Manager.

## <a name="get-available-updates"></a>Obter as atualizações disponíveis
Apenas as atualizações aplicáveis à sua infraestrutura e versão são transferidas e disponibilizadas na sua hierarquia. Esta sincronização pode ser automática ou manual, dependendo de como configurar o ponto de ligação de serviço para a sua hierarquia:

-   No **modo online**, o ponto de ligação de serviço liga automaticamente ao serviço em nuvem da Microsoft e transfere as atualizações aplicáveis.  

     Por predefinição, o Configuration Manager verifica a existência de novas atualizações a cada 24 horas. Pode também verificar atualizações imediatamente escolhendo **procurar atualizações** no **administração** > **atualizações e manutenção** nó da consola do Configuration Manager. 

-   No **modo offline**, o ponto de ligação de serviço não liga ao serviço de nuvem da Microsoft. Para transferir e, em seguida, importar as atualizações disponíveis, [utilizar a ferramenta de ligação de serviço](../../../core/servers/manage/use-the-service-connection-tool.md).  

> [!NOTE]  
>   Pode importar correções fora de banda para a consola. Para tal, utilize o [ferramenta de registo de atualização](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes). Estas correções fora de banda completam as atualizações que obtém ao sincronizar com o serviço de nuvem da Microsoft.


Depois de sincronizar as atualizações, pode visualizá-las na consola do Configuration Manager, acedendo ao **administração** > **atualizações e manutenção** nó:  

-   As atualizações não instaladas são apresentadas como **Disponível**.

-   As atualizações instaladas são apresentadas como **Instalada**. É apresentada apenas a atualização instalada mais recentemente. Pode escolher o **histórico** botão no friso para anteriormente ver atualizações instaladas.



Antes de configurar o ponto de ligação de serviço, compreenda e planeie as utilizações adicionais. As seguintes utilizações podem afetar a forma como configura esta função de sistema de sites:  

-   O ponto de ligação de serviço é utilizado para carregar as informações de utilização sobre o seu site. Estas informações ajudam o serviço em nuvem da Microsoft a identificar as atualizações que estão disponíveis para a versão atual da sua infraestrutura. Para obter mais informações, consulte [diagnósticos e dados de utilização](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

-   O ponto de ligação de serviço é utilizado para gerir dispositivos com o Microsoft Intune e utilizando a gestão de dispositivos móveis no local do Configuration Manager. Para obter mais informações, veja [Gestão de dispositivos móveis (MDM) híbrida com o System Center Configuration Manager e o Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

Para melhor compreender o que acontece quando as atualizações são transferidas, consulte:  

-   [Fluxograma - transferir atualizações para o System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md)

-   [Fluxograma - replicação de atualização para o System Center Configuration Manager](../../../core/servers/manage/update-replication-flowchart.md)  



## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Atribuir permissões para ver e gerir as atualizações e funcionalidades
Para ver as atualizações na consola, um utilizador tem de ter uma função de segurança da administração baseada em funções que inclua a classe de segurança **pacotes de atualização**. Esta classe concede acesso para ver e gerir as atualizações na consola do Configuration Manager.    

#### <a name="about-the-update-packages-class"></a>Sobre a classe de pacotes de atualização   
Por predefinição, o **pacotes de atualização** classe (SMS_CM_Updatepackages) faz parte das seguintes funções de segurança incorporadas com as permissões listadas:
 -  **Administrador Total** com permissões de **Modificação** e **Leitura** :
    -   Um utilizador com esta função de segurança e acesso para o **todos os** âmbito de segurança pode ver e instalar atualizações. O utilizador também pode ativar funcionalidades durante a instalação e ativar funcionalidades individuais, depois de instalada a atualização.
    - Um utilizador com esta função de segurança e acesso para o **predefinido** âmbito de segurança pode ver e instalar atualizações. O utilizador também pode ativar funcionalidades durante a instalação e ver funcionalidades após uma atualização está instalada. Mas este utilizador não é possível ativar as funcionalidades, depois de instalada a atualização.

- **Analista só de leitura** com permissões de **Leitura** :
  -  Um utilizador com esta função de segurança e acesso para o **predefinido** âmbito pode ver as atualizações, mas não instalá-los. Este utilizador também pode ver as funcionalidades depois de uma atualização foi instalado mas não é possível ativá-los.

#### <a name="permissions-required-for-updates-and-servicing"></a>Permissões necessárias para as atualizações e manutenção   
  - Utilize uma conta à qual esteja atribuído um direito de acesso que inclua a classe **Pacotes de atualização** com as permissões de **Modificação** e **Leitura** .
  - O âmbito **Predefinição** tem de ser atribuído à conta.

#### <a name="permissions-to-only-view-updates"></a>Permissões para visualizar apenas atualizações   
  - Utilizar uma conta que está atribuída uma função de segurança que inclui o **pacotes de atualização** apenas de classe com o **leitura** permissão.
  - O âmbito **Predefinição** tem de ser atribuído à conta.

#### <a name="permissions-required-to-enable-features-after-updates-are-installed"></a>Permissões necessárias para ativar funcionalidades após as atualizações são instaladas   
  -  Utilize uma conta à qual esteja atribuído um direito de acesso que inclua a classe **Pacotes de atualização** com as permissões de **Modificação** e **Leitura** .
  -  O âmbito **Tudo** tem de ser atribuído à conta.



##  <a name="bkmk_beforeinstall"></a> Antes de instalar uma atualização na consola  
 Reveja os seguintes passos antes de instalar uma atualização a partir da consola do Configuration Manager.  

###  <a name="bkmk_step1"></a> Passo 1: Reveja a lista de verificação de atualização  
Reveja a lista de verificação de atualizações aplicável para ações a efetuar antes de iniciar a atualização:

- [Lista de verificação para instalar a atualização 1706](../../../core/servers/manage/checklist-for-installing-update-1706.md)  

- [Lista de verificação para instalar a atualização 1710](../../../core/servers/manage/checklist-for-installing-update-1710.md)  

- [Lista de verificação para instalar a atualização 1802](../../../core/servers/manage/checklist-for-installing-update-1802.md)


###  <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a>Passo 2: Executar o Verificador de pré-requisitos antes de instalar uma atualização  
Antes de instalar uma atualização, considere executar a verificação de pré-requisitos para essa atualização. Se executar o pré-requisito antes de instalar uma atualização:  

-   Os ficheiros de atualização são replicados para outros sites antes de instalar a atualização.  

-   A verificação de pré-requisitos é executado automaticamente novo quando optar por instalar a atualização.  

> [!NOTE]   
> Quando iniciar uma verificação de pré-requisitos e, em seguida, ver o estado, o **instalação** fase parece estar ativo, no entanto, não é, na verdade, instalar a atualização. Para executar a verificação de pré-requisitos, o processo de atualização extrai o pacote da biblioteca de conteúdos e coloca-o para uma pasta de transição onde as verificações de pré-requisitos atuais podem ser acedidas. Este processo mesmo executa quando instala uma atualização. Por este motivo, a instalação mostra como "Em curso". Apenas o *pacote de atualização de extrair* passo é apresentado na categoria de instalação.  

Mais tarde, quando instala a atualização, pode configurar a atualização para ignorar os avisos de verificação de pré-requisitos.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Para executar o verificador de pré-requisitos antes de instalar uma atualização  

1.  Na consola do Configuration Manager, vá para **administração** > **atualizações e manutenção**.   

2.  Faça duplo clique no pacote de atualização que pretende executar a verificação de pré-requisitos.  

3.  Escolha **Executar verificação de pré-requisitos**.  

     Quando executar a verificação de pré-requisitos, o conteúdo da atualização é replicado para sites subordinados. Pode ver o ficheiro distmgr.log no site de servidor para confirmar que o conteúdo é a replicado com êxito.  

4.  Para ver os resultados da verificação, na consola do Configuration Manager, vá para **monitorização** > **atualizações e manutenção estado** e procure o estado dos pré-requisitos. Também pode ver o ConfigMgrPrereq.log no servidor do site para obter mais detalhes.  



##  <a name="bkmk_install"></a> Instalar atualizações na consola  
 Quando estiver pronto para instalar as atualizações a partir da consola do Configuration Manager, começar com o site de nível superior da hierarquia. Este site é o site de administração central ou um site primário autónomo.  

 Recomendamos que instale a atualização fora do horário comercial normal para cada site minimizar o efeito nas operações de negócio. Esta recomendação é porque a instalação da atualização pode incluir ações como reinstalar os componentes do site e funções de sistema do site.  

-   Os sites primários subordinados iniciam a atualização automaticamente, após o site de administração central concluir a instalação da atualização. Este processo é por predefinição e recomendado. No entanto, pode utilizar [windows para servidores de site do serviço](/sccm/core/servers/manage/service-windows) para controlar quando um site primário instala as atualizações.  

-   Atualize manualmente os sites secundários a partir da consola do Configuration Manager depois de concluída a atualização do site primário principal. A atualização automática dos servidores de site secundários não é suportada.  

-   Quando utiliza uma consola do Configuration Manager depois do site é atualizado, lhe for pedido para atualizar a consola.  

-  Depois do servidor do site concluir a instalação de uma atualização com êxito, atualiza automaticamente todas as funções de sistema de sites aplicáveis. É a advertência apenas para pontos de distribuição. Ao instalar uma atualização, todos os pontos de distribuição não reinstalar e ficam offline para atualizar ao mesmo tempo. Em vez disso, o servidor de site utiliza as definições de distribuição de conteúdo do site para distribuir a atualização para um subconjunto dos pontos de distribuição de cada vez. O resultado é que alguns pontos de distribuição ficam offline para instalar a atualização. Pontos de distribuição que não ter sido iniciada atualizar ou que concluiu a atualização permanecerem online e é capaz de fornecer conteúdo aos clientes.


###  <a name="bkmk_overview"></a> Descrição geral da instalação da atualização na consola  
#### <a name="1-when-the-update-installation-starts"></a>1. Quando a instalação da atualização é iniciada  
É-lhe apresentado o Assistente de Atualizações, que apresenta uma lista de áreas de produto a cuja atualização se refere.  

-   Na página **Geral** do assistente, pode configurar **Avisos de pré-requisitos**.  
    -   Os erros de pré-requisitos interrompem sempre a instalação da atualização. Corrija os erros antes de pode repetir a instalação da atualização com êxito. Para obter mais informações, consulte [repetir a instalação de uma atualização falhada](#bkmk_retry).  

    -   Os avisos de pré-requisitos também podem interromper a instalação da atualização. Corrija os avisos antes de repetir a instalação da atualização. Para obter mais informações, consulte [repetir a instalação de uma atualização falhada](#bkmk_retry).  
    -   **Ignorar quaisquer avisos de verificação de pré-requisitos e instalar esta atualização independentemente requisitos em falta**: define uma condição para a instalação da atualização ignorar os avisos de pré-requisitos. Esta opção permite a instalação da atualização continuar. Se não selecionar esta opção, a instalação da atualização para quando for detetado um aviso. A menos que executou anteriormente a verificação de pré-requisitos e os avisos de pré-requisitos fixos para um site, não é recomendada a utilização desta opção.  

      Em ambos os **administração** e **monitorização** áreas de trabalho, as atualizações e manutenção nó inclui um botão no Friso denominado **ignorar os avisos de pré-requisitos**. Este botão fica disponível quando um pacote de atualização não é possível concluir a instalação devido a avisos de verificação de pré-requisitos. Por exemplo, instalar uma atualização sem utilizar a opção para ignorar os avisos de pré-requisitos (no Assistente para atualizações). Interrompe a instalação da atualização com o estado de aviso de pré-requisitos, mas sem erros. Mais tarde, pode escolher **ignorar os avisos de pré-requisitos** a partir do friso para acionar uma continuação automática que da instalação de atualização que ignora os avisos de pré-requisitos. Quando utiliza esta opção, a instalação da atualização continua automaticamente após alguns minutos.



-   Quando uma atualização se refere ao cliente do Configuration Manager, é-lhe apresentada a opção para testar a atualização do cliente com um conjunto limitado de clientes. Para obter mais informações, consulte [como testar as atualizações de cliente numa coleção de pré-produção](../../../core/clients/manage/upgrade/test-client-upgrades.md).  


#### <a name="2-during-the-update-installation"></a>2. Durante a instalação da atualização  
Como parte da instalação da atualização do Configuration Manager:  

-   Reinstala os componentes afetados, como as funções do sistema de site ou consola do Configuration Manager.  

-   Gere as atualizações para clientes com base nas seleções que efetuou para testes de implementação de cliente e para [atualizações automáticas de cliente](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade).  

-   Não reiniciar os servidores de sistema de sites como parte da atualização, exceto se .NET estiver instalado como parte de um pré-requisito de funções de sistema do site.  

> [!TIP]  
>  Quando as atualizações são instaladas, atualizações do Configuration Manager também CD. Pasta mais recente. Esta pasta é utilizada durante uma recuperação de site.  


#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. Monitorizar o progresso das atualizações à medida que são instaladas  
Utilize o seguinte procedimento para monitorizar o progresso:  

-   Na consola do Configuration Manager: **Administração** > **atualizações e manutenção** nós. Este nó mostra o estado da instalação para todos os pacotes de atualização.


-   Na consola do Configuration Manager: **Monitorização** > **descrição geral** > **atualizações e manutenção estado** nós. Este nó mostra o estado da instalação de apenas o pacote de atualização que está atualmente a ser instalado.  

    A instalação do pacote de atualização é reduzida para as seguintes fases para facilitar a monitorização. Para cada fase, detalhes adicionais incluem o ficheiro de registo para ver para obter mais informações:  
    -   **Transferir** (nesta fase aplica-se apenas para o site de nível superior em que o site de ponto de ligação de serviço está instalado.)   

    -   **Replicação**   

    -   **Verificação de Pré-requisitos**   

    -   **Instalação**    

    -   **Após a instalação** – para obter mais informações, consulte [publicar tarefas de instalação](#post-installation-tasks).  

-   Pode ver o **CMUpdate.log** ficheiros  **&lt;ConfigMgr_Installation_Directory > \Logs**  


#### <a name="4-when-the-update-installation-completes"></a>4. Quando a instalação da atualização é concluída  
Após a instalação da primeira atualização do site ser concluída:  

-   Os sites primários subordinados instalam a atualização automaticamente. Não é necessária mais nenhuma ação.  

-   Os sites secundários têm de ser manualmente atualizados da consola do Configuration Manager.
> [!TIP]
> Embora a versão de um site secundário não for apresentado na consola, pode utilizar o SDK do Gestor de configuração para confirmar a versão de um site. Consulte [SMS_Site servidor WMI classe](/sccm/develop/reference/core/servers/configure/sms_site-server-wmi-class).


-   Até que todos os sites da hierarquia tenham sido atualizados para a nova versão, a hierarquia funciona num modo com versões mistas. Para obter mais informações, consulte [interoperabilidade entre diferentes versões do Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  


#### <a name="5-update-configuration-manager-consoles"></a>5. Atualizar consolas do Configuration Manager  
Depois de um site de administração central ou site primário, cada consola do Configuration Manager que liga a esse site tem também de atualizar. Ser-lhe-á pedido para atualizar uma consola:  

-   Quando abrir a consola

-   Quando acede a um novo nó numa consola aberta

Recomendamos que instale a atualização imediatamente.  

Quando a atualização da consola estiver concluída, pode verificar se a versão da consola e do site está correta. Aceda a **sobre o System Center Configuration Manager** no canto superior esquerdo da consola.  

 > [!Note]  
 > A partir de versão 1802, a versão da consola agora é ligeiramente diferente da versão do site. A versão secundária da consola agora corresponde à versão de lançamento do Configuration Manager. Por exemplo, no Configuration Manager versão 1802 a versão do site inicial é 5.0.8634.1000 e a versão da consola inicial é 5. **1802**.1082.1700. A compilação (1082) e números de revisão (1700) podem ser alteradas com correções futuras para a versão de 1802.



###  <a name="bkmk_toptier"></a> Para iniciar a instalação da atualização no site de nível superior  
No site de nível superior da hierarquia, na consola do Configuration Manager aceda a **administração** > **atualizações e manutenção**, selecione um **disponível** atualizar e, em seguida, clique em **Instalar pacote de atualizações**.  


###  <a name="bkmk_secondary"></a> Para iniciar a instalação da atualização num site secundário  
Depois de atualizações de site primário principal de um site secundário, pode atualizar o site secundário a partir da consola do Configuration Manager. Para tal, utilize o **Assistente para Atualizar Site Secundário**.  

1.  Na consola do Configuration Manager, vá para **administração** > **configuração do Site** > **Sites**, selecione o site que pretende atualizar e, em seguida, na home page do separador, no **Site** grupo, escolha **atualizar**.  

2.  Clique em **Sim** para iniciar a atualização do site secundário.  

Para monitorizar a instalação da atualização num site secundário, selecione o servidor de site secundário. Em seguida, no **home page** separador o **Site** grupo, escolha **Mostrar estado da instalação**. Também pode adicionar a coluna **Versão** ao ecrã da consola, de modo a que possa ver a versão de cada site secundário.  

Depois de um site secundário com êxito as atualizações, se o estado na consola do não atualiza ou sugere falhou a atualização, utilizam o **repetir a instalação** opção. Esta opção não reinstalar a atualização de um site secundário que instalar com êxito a atualização, mas que força a consola para atualizar o estado.


### <a name="post-installation-tasks"></a>Tarefas de pós-instalação
Quando um site instala uma atualização, existem várias tarefas que não é possível iniciar até após a conclusão da atualização instalação no servidor do site. Segue-se uma lista das tarefas de instalação post que são críticos para as operações de hierarquia e site. Uma vez que são críticos, são ativamente monitorizadas. Tarefas adicionais que não são monitorizadas diretamente incluem a reinstalação de funções de sistema de sites. Para ver o estado das tarefas de instalação post crítico, selecione **após a instalação** tarefas ao monitorizar a instalação da atualização para um site.

Nem todas as tarefas concluírem imediatamente. Algumas tarefas não iniciada até a cada site concluir a instalação da atualização. Novas funcionalidades que seria de esperar podem sofrer um atraso de até concluírem estas tarefas. Ativar novas funcionalidades não comece até que todos os sites concluir a instalação da atualização, pelo que as novas funcionalidades podem não estar visíveis durante algum tempo.

As tarefas de pós-instalação incluem:

-   **Instalar o serviço SMS_EXECUTIVE**
  -   Serviço crítico que é executado no servidor do site.
  -   Reinstalação deste serviço deve ser concluído rapidamente.


-   **Instalar o componente SMS_DATABASE_NOTIFICATION_MONITOR**
  -   Thread do componente de críticos do site do serviço SMS_EXECUTIVE.
  -   Reinstalação deste serviço deve ser concluído rapidamente.


-   **Instalar o componente SMS_HIERARCHY_MANAGER**
  -   Componente de críticos do site que é executado no servidor do site.
  -   Responsável por reinstalar funções do sistema de sites em servidores de sistema de sites. Não apresentar o estado para reinstalação de função do sistema de sites individuais.
  -   Reinstalação deste serviço deve ser concluído rapidamente.


-   **Instalar o componente SMS_REPLICATION_CONFIGURATION_MONITOR**
  -   Componente de críticos do site que é executado no servidor do site.
  -   Reinstalação deste serviço deve ser concluído rapidamente.


-   **Instalar o componente SMS_POLICY_PROVIDER**
  -   Componente de críticos do site que é executado apenas em sites primários.
  -   Reinstalação deste serviço deve ser concluído rapidamente.


-   **Monitorizar a inicialização da replicação**   
  -   Esta tarefa apenas mostra o site de administração central e sites primários subordinados.
  -   O SMS_REPLICATION_CONFIGURATION_MONITOR dependente.
  -   Deve ser concluído rapidamente.


-   **Atualizar o pacote de pré-produção do cliente do Configuration Manager**    
  -   Esta tarefa apresenta, mesmo quando o cliente de pré-produção (também denominada cliente testes de implementação no) não está ativada para utilização.
  -   Não inicie até que todos os sites na hierarquia de concluir a instalação da atualização.


-   **Pasta de atualização do cliente no servidor do Site**
  -   Esta tarefa não apresenta se utilizar o cliente em pré-produção.  
  -   Deve ser concluído rapidamente.


-   **Atualizar o pacote de cliente do Configuration Manager**
  -   Esta tarefa não apresenta se utilizar o cliente em pré-produção.  
  -   Acaba de apenas depois de todos os sites instalam a atualização.  


-   **Ativar funcionalidades**
  -   Esta tarefa apresenta apenas no site de nível superior da hierarquia.
  -   Não inicie até que todos os sites na hierarquia de concluir a instalação da atualização.
  -   Funcionalidades individuais não são apresentadas.



##  <a name="bkmk_retry"></a> Repetir a instalação de uma atualização falhada  
Quando a instalação de uma atualização falhar, reveja os comentários na consola para identificar resoluções de avisos e erros. Também pode ver o ConfigMgrPrereq.log no servidor do site para obter mais detalhes. Antes de repetir a instalação de uma atualização, é necessário corrigir os erros e deve corrigir os avisos.  

> [!TIP]  
> Se uma atualização tem problemas de transferir ou replicar, pode utilizar o [ferramenta de reposição de atualização](/sccm/core/servers/manage/update-reset-tool). 

Quando estiver pronto para repetir a instalação de uma atualização, selecione a atualização falhada e, em seguida, escolha uma opção aplicável. O comportamento de tentativas de instalação de atualização depende do nó onde deve começar a repetição e a opção de repetição que utilizar.  

#### <a name="retry-installation-for-the-hierarchy"></a>Repetir a instalação para a hierarquia
Pode repetir a instalação de uma atualização para toda a hierarquia quando a atualização se encontra num dos seguintes estados:  

  -   Verificações de pré-requisitos passaram com um ou mais avisos, e a opção para ignorar os avisos de verificação de pré-requisitos não foi definida no Assistente de atualização. (Valor da atualização para **ignorar aviso de pré** no **atualizações e manutenção** é nó **não**.)   
  -   Falha no pré-requisito    
  -   Falha na instalação
  -   Falha na replicação do conteúdo para o site   

Aceda a **administração** > **atualizações e manutenção**, selecione a atualização e, em seguida, escolha uma das seguintes opções:  

  -   **Repita** - quando executar **repita** partir deste nó, a instalação da atualização é iniciada novamente e automaticamente ignora os avisos de pré-requisitos. Conteúdo para a atualização também novamente replica se replicação tenha falhado anteriormente.
  - **Ignorar os avisos de pré-requisitos** - se a atualização instalar interrompe devido a um aviso, em seguida, pode escolher **ignorar os avisos de pré-requisitos**. Esta ação permite continuar a instalação da atualização (após alguns minutos) e utiliza a opção para ignorar avisos de pré-requisitos.   

#### <a name="retry-installation-for-the-site"></a>Repetir a instalação para o site  
 Pode repetir a instalação de uma atualização num site específico quando a atualização se encontra num dos seguintes estados:  

  -   Verificações de pré-requisitos passaram com um ou mais avisos, e a opção para ignorar os avisos de verificação de pré-requisitos não foi definida no Assistente de atualização. (O valor das atualizações para **ignorar aviso de pré-requisitos** do nó atualizações e manutenção é **não**.)  
  -   Falha no pré-requisito    
  -   Falha na instalação    

Aceda a **monitorização** > **descrição geral** > **estado de manutenção do Site**, selecione a atualização e, em seguida, clique das seguintes opções:

  - **Repita** - quando executar **repita** partir deste nó, reiniciar a instalação da atualização apenas nesse site. Ao contrário de execução **repita** do **atualizações e manutenção** nó, esta repetição ignora os avisos de pré-requisitos.
  - **Ignorar os avisos de pré-requisitos** -se a atualização instalar interrompe devido a um aviso, em seguida, pode clicar **ignorar os avisos de pré-requisitos**. Esta ação permite continuar a instalação da atualização (após alguns minutos) e utiliza a opção para ignorar avisos de pré-requisitos.



##  <a name="bkmk_after"></a> Após uma site instalar uma atualização  
Utilize a lista de verificação seguinte para concluir tarefas comuns e as configurações que são efetuadas após um site é atualizado.   

**Confirme a replicação do site para site está ativa:** Na consola do Configuration Manager, vá para as localizações seguintes para ver o estado e certifique-se de que a replicação está ativa:  

-   **Monitorização** > **Descrição geral** > **Hierarquia do Site**  

-   **Monitorização** > **Descrição geral** > **Replicação de Base de Dados**  

Para obter mais informações, consulte [monitorizar a infraestrutura de hierarquia e replicação](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) e [sobre o analisador do Link de replicação](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Confirme que os servidores de site e servidores do sistema de sites remoto reiniciaram (se necessário):** Reveja a infraestrutura de sites e certifique-se de que os servidores de sistema de sites e servidores de sites aplicáveis tem reiniciado com êxito. Normalmente, os servidores do site reiniciar apenas quando o Configuration Manager instala .NET como um pré-requisito para uma função de sistema de sites.  

 **Atualize consolas do Configuration Manager autónomo:** Certifique-se de que todas as consolas remotas do Configuration Manager estão a atualização para a mesma versão. Ser-lhe-á pedido para atualizar a consola quando:  

-   Ir para um novo nó na consola do.  

-   Abra a consola.

**Reconfigure réplicas de base de dados para pontos de gestão em sites primários:** Se utilizar réplicas de base de dados para pontos de gestão em sites primários, tem de desinstalar as réplicas de base de dados antes de atualizar o site. Após atualizar um site primário, reconfigure a réplica da base de dados para pontos de gestão. Para obter mais informações, consulte [réplicas para pontos de gestão de base de dados](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigure as tarefas de manutenção de base de dados que desativou antes da atualização:** Se tiver desativado a base de dados [tarefas de manutenção](../../../core/servers/manage/maintenance-tasks.md) num site antes de instalar a atualização, reconfigure essas tarefas no site. Utilize as mesmas definições que se encontravam em vigor antes da atualização.  

**Atualize clientes:** Para informações, consulte [como atualizar clientes em computadores Windows](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

**Configurações adicionais:** Reveja as alterações efetuadas antes de iniciar a atualização e, em seguida, restaure essas configurações para sites e da hierarquia.  



##  <a name="bkmk_options"></a> Ativar funcionalidades opcionais de atualizações  
Quando uma atualização inclui um ou mais funcionalidades opcionais, terá a oportunidade de ativar essas funcionalidades na sua hierarquia. Pode ativar funcionalidades quando instala a atualização, ou poderá regressar à consola posteriormente para ativar as funcionalidades opcionais.

Para ver as funcionalidades disponíveis e o respetivo estado, na consola navegue para **administração** > **atualizações e manutenção** > **funcionalidades**.

Quando uma funcionalidade não é opcional, é instalado automaticamente. Não aparecem no **funcionalidades** nós.  

> [!Important]  
> Numa hierarquia multilocal, só pode ativar funcionalidades opcionais ou a versão de pré-lançamento do site de administração central. Este comportamento garante que existem não existem conflitos entre a hierarquia. <!--507197-->
 

Quando ativa uma funcionalidade nova ou a funcionalidade de pré-lançamento, o Gestor da hierarquia do Configuration Manager (HMAN) tem de processar a alteração para que essa funcionalidade fica disponível. O processamento da alteração, muitas vezes, é imediato, mas pode demorar até 30 minutos a concluir, consoante o ciclo de processamento de HMAN. Após a alteração é processada, tem de reiniciar a consola antes de poder visualizar novos nós relacionados com essa funcionalidade.

#### <a name="list-of-optional-features"></a>Lista de funcionalidades opcionais
As seguintes funcionalidades são opcionais na versão mais recente do Configuration Manager:<!--505213-->  
- [Acesso condicional para PCs geridos](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)  <!--1191496-->
- [O Passport for Work](/sccm/protect/deploy-use/windows-hello-for-business-settings) (também conhecido como *Windows Hello para empresas*) <!--1245704-->
- [VPN para Windows 10](/sccm/protect/deploy-use/vpn-profiles) <!--1283610-->
- [Política do Windows Defender exploram proteção](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468-->
- [Conector do Microsoft Operations Management Suite (OMS)](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) <!--1258052-->
- [Criar PFX](/sccm/protect/deploy-use/introduction-to-certificate-profiles) <!--1321368-->
- [A Cache do cliente](/sccm/core/plan-design/hierarchy/client-peer-cache) <!--1101436-->
- [Ponto de serviço do armazém de dados](/sccm/core/servers/manage/data-warehouse) <!--1277922-->
- [Gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) <!--1101764-->
- [Atualizações de controladores superfície](/sccm/sum/get-started/configure-classifications-and-products) <!--1098490-->
- [Sequência conteúdo previamente a colocação em cache de tarefas](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) <!--1021244-->
- [Executar o passo de sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence) <!--1261338-->
- [Criar e executar scripts](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459-->
- [Avaliação de atestado de estado de funcionamento do dispositivo para as políticas de conformidade de acesso condicional](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616-->
- [Aprovar pedidos de aplicações para os utilizadores por dispositivo](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) <!--1357015-->  


> [!Tip]  
> Para mais informações sobre as funcionalidades que necessitam de consentimento para ativar, consulte [funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  
> Para obter mais informações sobre as funcionalidades que só estão disponíveis no ramo pré-visualização técnica, consulte [Technical Preview](/sccm/core/get-started/technical-preview).



##  <a name="bkmk_prerelease"></a> Utilizar as funcionalidades da versão de pré-lançamento de atualizações
Funcionalidades de pré-lançamento estão incluídas no ramo atual para um teste antecipado num ambiente de produção. Pode utilizar estas funcionalidades no seu ambiente de produção, mas não são considerados produção pronto. Saiba mais sobre [funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features), incluindo como ativá-los no seu ambiente.             



## <a name="frequently-asked-questions"></a>Perguntas mais frequentes

###  <a name="bkmk_faq"></a> Por que motivo não vejo determinadas atualizações na consola?  
 Se não conseguir localizar uma atualização específica a consola depois de uma sincronização com êxito com o serviço de nuvem da Microsoft, este comportamento pode ser devido a um dos seguintes motivos:  

-   A atualização requer uma configuração que a sua infraestrutura não utiliza ou a versão atual do produto não cumpre um pré-requisito para receber a atualização.  

     Se achar que tem as configurações necessárias e pré-requisitos para uma atualização em falta, confirme que o ponto de ligação de serviço está no modo online. Em seguida, utilize o **procurar atualizações** opção o **atualizações e manutenção** nó para forçar uma verificação. Se estiver no modo offline, tem de utilizar a ferramenta de ligação de serviço para sincronizar manualmente com o serviço em nuvem.  

-   A conta não possui as permissões corretas de administração baseada em funções para ver as atualizações na consola do Configuration Manager.

    Veja [Permissões para gerir atualizações de](../../../core/servers/manage/install-in-console-updates.md#assign-permissions-to-view-and-manage-updates-and-features) neste tópico para obter informações sobre as permissões necessárias para ver atualizações e ativar funcionalidades a partir da consola.


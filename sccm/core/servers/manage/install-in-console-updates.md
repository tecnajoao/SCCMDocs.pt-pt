---
title: Atualizações na consola
titleSuffix: Configuration Manager
description: Instalar atualizações para o Configuration Manager da cloud da Microsoft
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ea03f3a91d086a3528047ac6fcd18ff09b03537
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385563"
---
# <a name="install-in-console-updates-for-configuration-manager"></a>Instalar atualizações na consola do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager sincroniza com o serviço de nuvem da Microsoft para obter atualizações. Em seguida, instale estas atualizações a partir da consola do Configuration Manager.



## <a name="get-available-updates"></a>Obter as atualizações disponíveis

O site transfere apenas as atualizações aplicáveis à sua infraestrutura e versão. Esta sincronização pode ser automática ou manual, dependendo de como configurar o ponto de ligação de serviço para a hierarquia:

-   No **modo online**, o ponto de ligação de serviço liga automaticamente ao serviço em nuvem da Microsoft e transfere as atualizações aplicáveis.  

     Por predefinição, o Configuration Manager verifica a existência de novas atualizações a cada 24 horas. Verificar manualmente as atualizações na consola do Configuration Manager. Vá para o **administração** área de trabalho, selecione a **atualizações e manutenção** nó e clique em **procurar atualizações** na faixa de opções.  

-   Na **modo offline**, o ponto de ligação do serviço não liga ao serviço de nuvem da Microsoft. Para transferir e, em seguida, importar as atualizações disponíveis, [utilizar a ferramenta de ligação de serviço](/sccm/core/servers/manage/use-the-service-connection-tool).  

> [!NOTE]  
> Se necessário, importe correções fora de banda para a consola. Para tal, utilize o [ferramenta de registo de atualização](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes). Essas correções fora de banda complementam as atualizações que obtém ao sincronizar com o serviço de nuvem da Microsoft.  


Depois de sincronizar as atualizações, visualizá-los na consola do Configuration Manager. Vá para o **Administration** área de trabalho e selecione o **atualizações e manutenção** nó.  

-   As atualizações que ainda não instalou apresentadas como **disponível**.  

-   As atualizações que instalou o apresentadas como **instalada**. É apresentada apenas a atualização instalada mais recentemente. Clique nas **histórico** atualizações instaladas do botão da faixa de opções para ver anteriormente.  


Antes de configurar o ponto de ligação de serviço, compreenda e planeie as utilizações adicionais. As seguintes utilizações podem afetar como configura esta função de sistema de sites:  

-   O site utiliza o ponto de ligação de serviço para carregar informações de utilização sobre o seu site. Estas informações ajudam o serviço em nuvem da Microsoft a identificar as atualizações que estão disponíveis para a versão atual da sua infraestrutura. Para obter mais informações, consulte [diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  

-   O site utiliza o ponto de ligação de serviço para gerir dispositivos com o Microsoft Intune e a utilizar a gestão de dispositivos móveis no local do Configuration Manager. Para obter mais informações, consulte [gestão de dispositivos móveis híbridos (MDM)](/sccm/mdm/understand/hybrid-mobile-device-management).  

Para compreender melhor o que acontece quando as atualizações são transferidas, veja os fluxogramas seguintes:  

-   [Fluxograma – Transferir atualizações](/sccm/core/servers/manage/download-updates-flowchart)  

-   [Fluxograma – Atualizar replicação](/sccm/core/servers/manage/update-replication-flowchart)  



## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Atribuir permissões para ver e gerir atualizações e funcionalidades

Para ver as atualizações na consola, um utilizador tem de ter uma função de segurança de administração baseada em funções que inclua a classe de segurança **pacotes de atualização**. Essa classe concede acesso para ver e gerir atualizações na consola do Configuration Manager.    


#### <a name="about-the-update-packages-class"></a>Sobre a classe de pacotes de atualização   
Por predefinição, o **pacotes de atualização** classe (SMS_CM_Updatepackages) faz parte das seguintes funções de segurança incorporadas com as permissões listadas:  

-  **Administrador Total** com permissões de **Modificação** e **Leitura** :  

    -   Um utilizador com esta função de segurança e acesso para o **todos os** âmbito de segurança pode ver e instalar atualizações. O utilizador também pode ativar funcionalidades durante a instalação e ativar funcionalidades individuais após as atualizações do site.  

    - Um utilizador com esta função de segurança e acesso para o **predefinido** âmbito de segurança pode ver e instalar atualizações. O utilizador também pode ativar funcionalidades durante a instalação e ver funcionalidades após as atualizações do site. Mas este utilizador não é possível ativar as funcionalidades após as atualizações do site.  

- **Analista só de leitura** com permissões de **Leitura** :  

  -  Um utilizador com esta função de segurança e acesso para o **predefinido** âmbito pode ver atualizações, mas não instalá-los. Este utilizador também pode ver funcionalidades após as atualizações do site, mas não é possível ativá-las.  


#### <a name="permissions-required-for-updates-and-servicing"></a>Permissões necessárias para as atualizações e manutenção   
- Utilizar uma conta para que atribua uma função de segurança que inclui a **pacotes de atualização** classe com ambos **modificar** e **leitura** permissões.  

- Atribua a conta para o **predefinido** âmbito.  

#### <a name="permissions-to-only-view-updates"></a>Permissões para ver apenas as atualizações   
- Utilizar uma conta para que atribua uma função de segurança que inclui a **pacotes de atualização** apenas de classe com o **leitura** permissão.  

- Atribua a conta para o **predefinido** âmbito.  

#### <a name="permissions-required-to-enable-features-after-the-site-updates"></a>Permissões necessárias para ativar funcionalidades após as atualizações do site   
-  Utilizar uma conta para que atribua uma função de segurança que inclui a **pacotes de atualização** classe com ambos **modificar** e **leitura** permissões.  

-  Atribua a conta para o **todos os** âmbito.  



##  <a name="bkmk_beforeinstall"></a> Antes de instalar uma atualização na consola  

Reveja os seguintes passos antes de instalar uma atualização a partir da consola do Configuration Manager.  


###  <a name="bkmk_step1"></a> Passo 1: Reveja a lista de verificação de atualização  

Reveja a lista de verificação de atualizações aplicável para ações a efetuar antes de iniciar a atualização:

- [Lista de verificação para instalar a atualização 1806](/sccm/core/servers/manage/checklist-for-installing-update-1806)  

- [Lista de verificação para instalar a atualização 1802](/sccm/core/servers/manage/checklist-for-installing-update-1802)

- [Lista de verificação para instalar a atualização 1710](/sccm/core/servers/manage/checklist-for-installing-update-1710)  


###  <a name="bkmk_step2"></a> Passo 2: Executar o Verificador de pré-requisitos antes de instalar uma atualização  

Antes de instalar uma atualização, considere executar a verificação de pré-requisitos para essa atualização. Se executar o pré-requisito antes de instalar uma atualização:  

-   O site replica os ficheiros de atualização para outros sites antes de instalar a atualização.  

-   Quando optar por instalar a atualização, a verificação de pré-requisitos é executado automaticamente novamente.  

> [!NOTE]   
> Quando iniciar uma verificação de pré-requisitos e, em seguida, ver o estado, o **instalação** fase parece ser o Active Directory. No entanto, o site, na verdade, não é instalar a atualização. Para executar a verificação de pré-requisitos, o processo de atualização extrai o pacote da biblioteca de conteúdos. Em seguida, coloca o pacote para uma pasta de teste onde ele pode acessar as verificações de pré-requisitos atuais. Quando instala uma atualização, esse mesmo processo é executado. Este comportamento é por isso que a fase de instalação é apresentado como **em curso**. Apenas os *pacote de atualização de extrair* passo é mostrado na categoria de instalação.  

Mais tarde, quando instalar a atualização, pode configurar a atualização para ignorar os avisos de verificação de pré-requisitos.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Para executar o verificador de pré-requisitos antes de instalar uma atualização  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho e selecione o **atualizações e manutenção** nó.   

2.  Selecione o pacote de atualização para o qual pretende executar a verificação de pré-requisitos.  

3.  Clique em **executar verificação de pré-requisitos** na faixa de opções.  

     Quando executar a verificação de pré-requisitos, o conteúdo da atualização é replicado para sites subordinados. Ver os **distmgr** no site do servidor para confirmar que o conteúdo é replicado com êxito.  

4.  Para ver os resultados da verificação de pré-requisitos:  

    1. Na consola do Configuration Manager, vá para o **monitorização** área de trabalho.  

    2. Selecione o **atualizações e estado de manutenção** nó e procure o estado dos pré-requisitos.  

    3. Para obter mais informações, consulte a **Configmgrprereq** no servidor do site.  



##  <a name="bkmk_install"></a> Instalar atualizações na consola  

Quando estiver pronto para instalar atualizações a partir da consola do Configuration Manager, começar com o site de nível superior da sua hierarquia. Este site é o site de administração central ou um site primário autónomo.  

Instale a atualização fora do horário comercial normal para cada site minimizar o efeito nas operações de negócio. A instalação da atualização pode incluir ações como reinstalar os componentes do site e as funções de sistema de sites.  

-   Sites primários subordinados iniciam automaticamente a atualização depois do site de administração central concluir a instalação da atualização. Este processo é por predefinição e recomendado. Para controlar quando um site primário instala as atualizações, use [manutenção do windows para servidores de site](/sccm/core/servers/manage/service-windows).  

-   Depois de concluída a atualização do site primário principal, atualize sites secundários a partir da consola do Configuration Manager manualmente. Não é suportada a atualização automática de servidores de site secundário.  

-   Quando utiliza uma consola do Configuration Manager depois do site é atualizado, lhe for pedido para atualizar a consola.  

-  Depois do servidor do site concluir a instalação de uma atualização com êxito, ele atualiza automaticamente todas as funções de sistema de sites aplicável. No entanto, todos os pontos de distribuição não reinstalar e ficam offline para atualizar, ao mesmo tempo. Em vez disso, o servidor de site utiliza as definições de distribuição de conteúdo do site para distribuir a atualização para um subconjunto dos pontos de distribuição ao mesmo tempo. O resultado é que apenas alguns pontos de distribuição ficam offline para instalar a atualização. Pontos de distribuição que ainda não começou atualizar ou que concluiu a atualização permanecem online e capaz de fornecer conteúdo aos clientes.


###  <a name="bkmk_overview"></a> Descrição geral da instalação da atualização na consola  

#### <a name="1-when-the-update-installation-starts"></a>1. Quando a instalação da atualização é iniciada  
É apresentada com o Assistente de atualizações que apresenta uma lista das áreas de produto que a atualização se aplica a.  

-   Sobre o **gerais** página do assistente, configure **avisos de pré-requisitos** conforme necessário:  

    -   Os erros de pré-requisitos interrompem sempre a instalação da atualização. Corrigi erros antes de pode tentar novamente a instalação da atualização com êxito. Para obter mais informações, consulte [repetir a instalação de uma atualização falhada](#bkmk_retry).  

    -   Os avisos de pré-requisitos também podem interromper a instalação da atualização. Corrigi avisos antes de repetir a instalação da atualização. Para obter mais informações, consulte [repetir a instalação de uma atualização falhada](#bkmk_retry).  

    -   **Ignorar quaisquer avisos de verificação de pré-requisitos e instalar esta atualização independentemente de requisitos em falta**: Defina uma condição para a instalação da atualização ignorar avisos de pré-requisitos. Esta opção permite a instalação da atualização continuar. Se não selecionar esta opção, a instalação de atualização para quando o processo encontra um aviso. A menos que executou anteriormente a verificação de pré-requisitos e os avisos de pré-requisitos fixos para um site, não utilize esta opção.  

      Em ambos os **Administration** e **monitorização** áreas de trabalho, as atualizações e manutenção de nó inclui um botão da faixa de opções com o nome **ignorar avisos de pré-requisitos**. Este botão fica disponível quando um pacote de atualização não consegue concluir a instalação devido a avisos de verificação de pré-requisitos. Por exemplo, instalar uma atualização sem utilizar a opção para ignorar avisos de pré-requisitos (do Assistente de atualizações). A instalação de atualização para com o estado de aviso de pré-requisitos, mas sem erros. Mais tarde, clique em **ignorar avisos de pré-requisitos** na faixa de opções. Esta ação aciona uma continuação automática da instalação, atualização que ignora os avisos de pré-requisitos. Quando utiliza esta opção, a instalação da atualização continua automaticamente após alguns minutos.  


-   Quando uma atualização aplica-se para o cliente do Configuration Manager, optar por testar a atualização do cliente com um conjunto limitado de clientes. Para obter mais informações, consulte [como testar as atualizações de cliente numa coleção de pré-produção](/sccm/core/clients/manage/upgrade/test-client-upgrades).  


#### <a name="2-during-the-update-installation"></a>2. Durante a instalação da atualização  
Como parte da instalação da atualização, o Configuration Manager efetua as seguintes ações:  

-   Reinstala os componentes afetados, como funções de sistema de sites ou a consola do Configuration Manager.  

-   Gere as atualizações para clientes com base nas seleções que fez para criação de pilotos de cliente e para [atualizações automáticas de clientes](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade).  

-   Em geral os servidores do sistema de sites não precisam de reiniciar como parte da atualização. Se uma função utiliza o .NET e o pacote de atualizações desse componente de pré-requisito, em seguida, pode reiniciar o sistema de sites.  

> [!TIP]  
>  Quando instalar atualizações do Configuration Manager, o site também atualiza o CD. Pasta mais recente. Para obter mais informações, consulte [The CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder).  


#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. Monitorizar o progresso das atualizações à medida que são instaladas  
Utilize os seguintes passos para monitorizar o progresso:  

-   Na consola do Configuration Manager, vá para o **Administration** área de trabalho e selecione o **atualizações e manutenção** nó. Este nó mostra o estado da instalação para todos os pacotes de atualização.  

-   Na consola do Configuration Manager, vá para o **monitorização** área de trabalho e selecione o **atualizações e estado de manutenção** nó. Este nó mostra o estado da instalação de apenas o atual pacote de atualização que está a instalar o site.  

    A instalação da atualização é dividida em várias fases para uma monitorização mais fácil. Para cada um dos seguintes fases, detalhes adicionais no estado de instalação incluem o ficheiro de registo para ver para obter mais informações:  

    -   **Transferir**: Nesta fase aplica-se apenas ao site de nível superior com o ponto de ligação de serviço.   

    -   **Replicação**   

    -   **Verificação de Pré-requisitos**   

    -   **Instalação**    

    -   **Pós-instalação**: Para obter mais informações, consulte [publicar tarefas de instalação](#post-installation-tasks).  

-   Ver os **cmupdate. log** do ficheiro no `<ConfigMgr_Installation_Directory>\Logs` no servidor do site.  


#### <a name="4-when-the-update-installation-completes"></a>4. Quando a instalação da atualização é concluída  
Após a instalação da primeira atualização do site ser concluída:  

-   Os sites primários subordinados instalam a atualização automaticamente. Não é necessária mais nenhuma ação.  

-   Atualize manualmente os sites secundários a partir da consola do Configuration Manager. Para obter mais informações, consulte [iniciar a instalação de atualização num site secundário](#bkmk_secondary).  

-   Até que todos os sites da hierarquia tenham sido atualizados para a nova versão, a hierarquia funciona num modo com versões mistas. Para obter mais informações, consulte [interoperabilidade entre diferentes versões](/sccm/core/plan-design/hierarchy/interoperability-between-different-versions).  


#### <a name="5-update-configuration-manager-consoles"></a>5. Atualizar consolas do Configuration Manager  
Depois de um site de administração central ou site primário, cada consola do Configuration Manager que liga ao site tem também de atualizar. Lhe for pedido para atualizar uma consola:  

-   Quando abrir a consola  

-   Quando passa para um novo nó numa consola aberta  

Atualize a consola imediatamente após as atualizações do site.  

Depois de concluída a atualização da consola, verifique se que as versões de consola e do site estão corretas. Aceda a **sobre o System Center Configuration Manager** no canto superior esquerdo da consola.  

 > [!Note]  
 > A partir da versão 1802, a versão da consola agora é um pouco diferente da versão de site. A versão secundária da consola agora corresponde à versão de lançamento do Configuration Manager. Por exemplo, no Configuration Manager versão 1802 a versão do site inicial é 5.0.8634.1000 e a versão da consola inicial é 5. **1802**.1082.1700. A compilação (1082) e números de revisão (1700) podem ser alteradas com correções futuras, para a versão 1802.



###  <a name="bkmk_toptier"></a> Para iniciar a instalação de atualização no site de nível superior  

Site de nível superior da hierarquia, na consola do Configuration Manager, vá para o **Administration** área de trabalho e selecione o **atualizações e manutenção** nó. Selecione uma atualização com o estado da **disponível**e, em seguida, clique em **Instalar pacote de atualizações** na faixa de opções.  


###  <a name="bkmk_secondary"></a> Para iniciar a instalação da atualização num site secundário  

Depois de atualizações de site primário principal de um site secundário, atualize o site secundário a partir da consola do Configuration Manager. Para tal, utilize o **Assistente para Atualizar Site Secundário**.  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó. Selecione o site secundário que pretende atualizar e, em seguida, clique em **atualizar** na faixa de opções.  

2.  Clique em **Sim** para iniciar a atualização do site secundário.  

Para monitorizar a instalação da atualização num site secundário, selecione o site secundário e clique em **Mostrar estado da instalação** na faixa de opções. Adicionar também a **versão** coluna para o nó de Sites para que possa ver a versão de cada site secundário.  

Em alguns casos, o estado na consola do não atualiza ou sugere que a atualização falhou. Após a atualização com êxito de um site secundário, utilize o **repetir a instalação** opção. Esta opção não reinstalar a atualização para um site secundário com êxito instalado a atualização, mas a força da consola para atualizar o estado.


### <a name="post-installation-tasks"></a>Tarefas de pós-instalação

Quando um site instala uma atualização, existem várias tarefas que não é possível iniciar até após a atualização de concluir a instalação no servidor do site. Esta lista inclui as tarefas de pós-instalação que são críticas para operações de site e da hierarquia. Uma vez que são importantes, está ativamente monitorados. Tarefas adicionais que não são diretamente monitorizadas incluem a reinstalação do funções do sistema de sites. Para ver o estado das tarefas de pós-instalação críticas, selecione o **pós-instalação** tarefa ao monitorizar a instalação da atualização para um site.

Nem todas as tarefas são concluídas imediatamente. Algumas tarefas não são iniciados até cada site concluir a instalação da atualização. Nova funcionalidade, que pode esperar pode ser atrasada até concluírem estas tarefas. Não começa a ativar novas funcionalidades até que todos os sites concluir a instalação da atualização, para que os novos recursos podem não estar visíveis durante algum tempo.

As tarefas de pós-instalação incluem:

-   **Instalar o serviço SMS_EXECUTIVE**
  -   Críticos de serviço que é executado no servidor do site.
  -   Reinstalação deste serviço deverá ser concluída rapidamente.


-   **Instalar o componente SMS_DATABASE_NOTIFICATION_MONITOR**
  -   Thread do componente de críticos do site do serviço SMS_EXECUTIVE.
  -   Reinstalação deste serviço deverá ser concluída rapidamente.


-   **Instalar o componente SMS_HIERARCHY_MANAGER**
  -   Componente de site essencial que é executado no servidor do site.
  -   Responsável de reinstalação de funções nos servidores de sistema de sites. Não apresenta o estado para reinstalação de função do sistema de sites individuais.
  -   Reinstalação deste serviço deverá ser concluída rapidamente.


-   **Instalar o componente SMS_REPLICATION_CONFIGURATION_MONITOR**
  -   Componente de site essencial que é executado no servidor do site.
  -   Reinstalação deste serviço deverá ser concluída rapidamente.


-   **Instalar o componente SMS_POLICY_PROVIDER**
  -   Componente de site essencial que é executado apenas em sites primários.
  -   Reinstalação deste serviço deverá ser concluída rapidamente.


-   **Monitorização de inicialização da replicação**   
  -   Esta tarefa apresenta apenas no site de administração central e sites primários subordinados.
  -   Dependendo do SMS_REPLICATION_CONFIGURATION_MONITOR.
  -   Deve concluir rapidamente.


-   **A atualizar o pacote de pré-produção do cliente do Configuration Manager**    
  -   Esta tarefa apresenta até mesmo quando o cliente de pré-produção (também chamado de criação de pilotos de cliente) não está ativada para utilização.
  -   Não começa até que todos os sites na hierarquia de concluir a instalação da atualização.


-   **A atualizar a pasta Client no servidor do Site**
  -   Esta tarefa não exibe se utilizar o cliente em pré-produção.  
  -   Deve concluir rapidamente.


-   **A atualizar o pacote de cliente do Configuration Manager**
  -   Esta tarefa não exibe se utilizar o cliente em pré-produção.  
  -   Conclusão da apenas depois de todos os sites de instalar a atualização.  


-   **A ativar funcionalidades**
  -   Esta tarefa apresenta apenas no site de nível superior da hierarquia.
  -   Não começa até que todos os sites na hierarquia de concluir a instalação da atualização.
  -   Funcionalidades individuais não são apresentadas.



##  <a name="bkmk_retry"></a> Repetir a instalação de uma atualização falhada  

Quando a instalação de uma atualização falhar, reveja os comentários na consola para identificar resoluções de avisos e erros. Para obter mais detalhes, veja a **Configmgrprereq** no servidor do site. Antes de repetir a instalação de uma atualização, tem de corrigir erros e deve resolver os avisos.  

> [!TIP]  
> Se uma atualização tiver problemas a transferir ou replicar, utilize o [ferramenta de reposição de atualizações](/sccm/core/servers/manage/update-reset-tool).  

Quando estiver pronto para tentar novamente a instalação de uma atualização, selecione a atualização falhada e, em seguida, escolha uma opção aplicável. O comportamento de repetição de instalação da atualização depende do nó onde começar a repetição e a opção de repetição que utilizar.  

#### <a name="retry-installation-for-the-hierarchy"></a>Repetir a instalação para a hierarquia
Repetir a instalação de uma atualização para toda a hierarquia quando a atualização se encontra dos seguintes Estados:  

  -   Verificações de pré-requisitos passaram com um ou mais avisos, e a opção para ignorar os avisos de verificação de pré-requisitos não foi definida no Assistente de atualização. (Valor da atualização para o **ignorar aviso de pré-requisitos** no **atualizações e manutenção** é o nó **não**.)   

  -   Falha no pré-requisito    

  -   Falha na instalação  

  -   Falha na replicação do conteúdo para o site   

Vá para o **Administration** área de trabalho e selecione o **atualizações e manutenção** nó. Selecione a atualização e, em seguida, escolha uma das seguintes opções:  

  -   **Repita**: Quando **repita** partir **atualizações e manutenção**, a instalação da atualização é iniciada novamente e automaticamente ignora os avisos de pré-requisitos. Se a replicação de conteúdo falhado anteriormente, o conteúdo para a atualização replica novamente.  

  - **Ignorar avisos de pré-requisitos**: Se a instalação da atualização parar devido a um aviso, em seguida, pode escolher **ignorar avisos de pré-requisitos**. Esta ação permite a instalação da atualização para continuar após alguns minutos e utiliza a opção para ignorar avisos de pré-requisitos.   

#### <a name="retry-installation-for-the-site"></a>Repetir a instalação para o site  
Repetir a instalação de uma atualização num site específico quando a atualização se encontra dos seguintes Estados:  

  -   Verificações de pré-requisitos passaram com um ou mais avisos, e a opção para ignorar os avisos de verificação de pré-requisitos não foi definida no Assistente de atualização. (O valor das atualizações para **ignorar aviso de pré-requisitos** as atualizações e manutenção nó é **não**.)  

  -   Falha no pré-requisito    

  -   Falha na instalação    

Vá para o **monitorização** área de trabalho e selecione o **estado de manutenção do Site** nó. Selecione a atualização e, em seguida, clique das seguintes opções:  

  - **Repita**: Quando **repita** partir **estado de manutenção do Site**, reiniciar a instalação da atualização apenas nesse site. Ao contrário da execução **repita** partir do **atualizações e manutenção** nó, esta repetição não ignora os avisos de pré-requisitos.  

  - **Ignorar avisos de pré-requisitos**: Se a instalação da atualização parar devido a um aviso, pode, em seguida, clique em **ignorar avisos de pré-requisitos**. Esta ação permite a instalação da atualização para continuar após alguns minutos e utiliza a opção para ignorar avisos de pré-requisitos.  



##  <a name="bkmk_after"></a> Após uma site instalar uma atualização  

Utilize a lista de verificação seguinte para concluir tarefas comuns e as configurações que são efetuadas após atualizar um site.   

#### <a name="confirm-site-to-site-replication-is-active"></a>Confirmar a replicação de site a site está ativa
Na consola do Configuration Manager, aceda às localizações seguintes para ver o estado e certifique-se de que a replicação está ativa:  

-   **Monitorização** área de trabalho **hierarquia do Site** nó  

-   **Monitorização** área de trabalho **replicação de base de dados** nó  

Para obter mais informações, consulte os artigos seguintes:  
- [Monitorizar a infraestrutura de hierarquia e replicação](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure)
- [Sobre o analisador de ligações de replicação](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA)  

#### <a name="confirm-that-servers-restarted-if-necessary"></a>Confirme que os servidores reiniciado (se necessário) 
Reveja a infraestrutura de sites e certifique-se de que servidores do site aplicáveis e os servidores de sistema de sites remoto reiniciaram com êxito. Normalmente, os servidores do site reinicie apenas quando o Configuration Manager instala .NET como um pré-requisito para uma função de sistema de sites.  

#### <a name="update-standalone-configuration-manager-consoles"></a>Atualizar consolas do Configuration Manager autónomo
Atualize todas as consolas remotas do Configuration Manager para a mesma versão. Lhe for pedido para atualizar a consola quando:  

-   Ir para um novo nó na consola do.  

-   Abra a consola.  

#### <a name="reconfigure-database-replicas-for-management-points"></a>Reconfigurar réplicas de base de dados para pontos de gestão
Se utilizar réplicas de base de dados para pontos de gestão em sites primários, desinstale as réplicas de base de dados antes de atualizar o site. Após atualizar um site primário, reconfigure a réplica da base de dados para pontos de gestão. Para obter mais informações, consulte [réplicas para pontos de gestão de base de dados](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  

#### <a name="reconfigure-any-disabled-maintenance-tasks"></a>Reconfigure as tarefas de manutenção desativado
Se tiver desativado a base de dados [tarefas de manutenção](/sccm/core/servers/manage/maintenance-tasks) num site antes de instalar a atualização, reconfigure essas tarefas no site. Utilize as definições que se encontravam em vigor antes da atualização.  

#### <a name="upgrade-clients"></a>Atualização dos clientes
Para obter informações, consulte [como atualizar clientes para computadores Windows](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers).  

#### <a name="additional-configurations"></a>Configurações adicionais
Reveja as alterações feitas antes de iniciar a atualização e, em seguida, restaure essas configurações para sites e da hierarquia.  



##  <a name="bkmk_options"></a> Ativar funcionalidades opcionais de atualizações  

Quando uma atualização inclui um ou mais funcionalidades opcionais, terá a oportunidade de ativar essas funcionalidades na sua hierarquia. Habilitar recursos quando instala a atualização ou regressar à consola mais tarde para ativar as funcionalidades opcionais.

Para ver os recursos disponíveis e o respetivo estado, na consola do Ir para o **Administration** área de trabalho, expanda **atualizações e manutenção**e selecione o **funcionalidades** nó.

Quando um recurso não é opcional, é instalada automaticamente. Ele não aparece no **funcionalidades** nó.  

> [!Important]  
> Numa hierarquia multilocal, ative funcionalidades opcionais ou de pré-lançamento apenas do site de administração central. Esse comportamento garante que não existam conflitos entre a hierarquia. <!--507197-->
 

Quando ativa a uma nova função ou funcionalidade de pré-lançamento, o Gestor da hierarquia do Configuration Manager (HMAN) têm de processar a alteração para que esse recurso fica disponível. Processamento da alteração, muitas vezes, é imediato. Consoante o HMAN ciclo de processamento, pode demorar até 30 minutos a concluir. Após a alteração é processada, reinicie a consola antes de poder utilizar a funcionalidade.

#### <a name="list-of-optional-features"></a>Lista de funcionalidades opcionais
As seguintes funcionalidades são opcionais na versão mais recente do Configuration Manager:<!--505213-->  

<!--Note to include in target articles

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

-->

- [Disponibilidade elevada do servidor de site](/sccm/core/servers/deploy/configure/site-server-high-availability)<!--1128774-->
- [Atualizações de software de terceiros](/sccm/sum/deploy-use/third-party-software-updates)<!--1357605,1352101,1358714-->
- [Aprovar pedidos de aplicações para utilizadores por dispositivo](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) <!--1357015-->  
- [Suporte para Cisco AnyConnect 4.0.07x e posteriores para iOS](/sccm/mdm/deploy-use/create-vpn-profiles)<!--1357393-->
- [Avaliação de atestado de estado de funcionamento do dispositivo para políticas de conformidade para acesso condicional](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616-->
- [Criar e executar scripts](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459-->
- [Executar o passo de sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence) <!--1261338-->
- [Sequência conteúdo colocação em pré-cache de tarefas](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) <!--1021244-->
- [Atualizações de controlador do Surface](/sccm/sum/get-started/configure-classifications-and-products) <!--1098490-->
- [Gateway de gestão na cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) <!--1101764-->
- [Ponto de serviço do armazém de dados](/sccm/core/servers/manage/data-warehouse) <!--1277922-->
- [Cache ponto a ponto do cliente](/sccm/core/plan-design/hierarchy/client-peer-cache) <!--1101436-->
- [Criação de PFX](/sccm/protect/deploy-use/introduction-to-certificate-profiles) <!--1321368-->
- [Conector do Microsoft Operations Management Suite (OMS)](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) <!--1258052-->
- [Política do Windows Defender Exploit Guard](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468-->
- [VPN para Windows 10](/sccm/protect/deploy-use/vpn-profiles) <!--1283610-->
- [O Passport for Work](/sccm/protect/deploy-use/windows-hello-for-business-settings) (também conhecido como *Windows Hello para empresas*) <!--1245704-->
- [Acesso condicional para PCs gerenciados](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)  <!--1191496-->


> [!Tip]  
> Para obter mais informações sobre as funcionalidades que requerem o consentimento para ativar, consulte [funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  
> 
> Para obter mais informações sobre as funcionalidades que só estão disponíveis no ramo de pré-visualização técnica, veja [Technical Preview](/sccm/core/get-started/technical-preview).



##  <a name="bkmk_prerelease"></a> Utilizar as funcionalidades da versão de pré-lançamento de atualizações

O ramo atual inclui funcionalidades de pré-lançamento para um teste antecipado num ambiente de produção. Para obter mais informações, consulte [funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features).



## <a name="bkmk_faq"></a> Perguntas mais frequentes

###  <a name="why-dont-i-see-certain-updates-in-my-console"></a>Por que motivo não vejo determinadas atualizações na consola?  

Se não conseguir encontrar uma atualização específica na sua consola depois de uma sincronização com êxito com o serviço de nuvem da Microsoft, este comportamento pode ser devido a uma das seguintes razões:  

-   A atualização requer uma configuração de que sua infraestrutura não utiliza ou sua versão atual do produto não cumpre um pré-requisito para receber a atualização.  

     Se acha que tem as configurações necessárias e pré-requisitos para uma atualização em falta, certifique-se que o ponto de ligação de serviço está no modo online. Em seguida, utilize o **procurar atualizações** opção a **atualizações e manutenção** nó para forçar uma verificação. Se o ponto de ligação de serviço está no modo offline, utilize a ferramenta de ligação de serviço para sincronizar manualmente com o serviço em nuvem.  

-   A conta não possui as permissões corretas de administração baseada em funções para ver as atualizações na consola do Configuration Manager. Para obter mais informações, consulte [permissões para gerir atualizações](#assign-permissions-to-view-and-manage-updates-and-features).  


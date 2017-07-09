---
title: "Atualização para o System Center Configuration Manager | Microsoft Docs"
description: "Conhecer as etapas para executar uma atualização in-loco bem-sucedida de um site e hierarquia que executa o System Center 2012 Configuration Manager."
ms.custom: na
ms.date: 6/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
caps.latest.revision: 21
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 3619a73d3a39659de927e1711a7ec81de9918064
ms.openlocfilehash: 1166b739e1e8d667172d97883f484fdbc3a142c1
ms.contentlocale: pt-pt
ms.lasthandoff: 06/13/2017


---
# <a name="upgrade-to-system-center-configuration-manager"></a>Atualizar para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Você pode executar uma atualização para atualização in-loco para o System Center Configuration Manager de um site e hierarquia que executa o System Center 2012 Configuration Manager.  

 Antes de atualizar do System Center 2012 Configuration Manager, você deve preparar sites, o que exige que você remova configurações específicas que podem impedir uma atualização bem-sucedida e, em seguida, execute a sequência de atualização quando mais de um único site envolvido.  

 > [!TIP]
 > Ao gerenciar o site do System Center Configuration Manager e infraestrutura de hierarquia, os termos de *atualização*, *atualizar*, e *instalar* são usados para descrever os três conceitos separados. Para saber como cada termo é usado, consulte [sobre atualização, atualização e instalação](/sccm/core/understand/upgrade-update-install).

##  <a name="bkmk_path"></a> Caminhos de atualização no local  

**Atualizar para a versão 1702**   
Quando você tiver a mídia de linha de base de 1702 de versão, você pode atualizar o seguinte para uma versão totalmente licenciada do System Center Configuration Manager versão 1702:   
-     Uma instalação de avaliação do System Center Configuration Manager versão 1702
-     System Center 2012 Configuration Manager com Service Pack 1
-     System Center 2012 Configuration Manager com Service Pack 2
-     System Center 2012 R2 Configuration Manager
-     System Center 2012 R2 Configuration Manager com Service Pack 1

**Atualizar para a versão 1606**  
No dia 15 de dezembro de 2016, a mídia de linha de base para a versão 1606 foi disponibilizada para adicionar suporte para cenários adicionais de atualização. Esta nova versão oferece suporte a atualização das seguintes maneiras para uma versão totalmente licenciada do System Center Configuration Manager versão 1606:  
-   Uma instalação de avaliação do System Center Configuration Manager versão 1606
-   Uma instalação do release candidate do System Center Configuration Manager  
-   System Center 2012 Configuration Manager com Service Pack 1  
-   System Center 2012 Configuration Manager com Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center 2012 R2 Configuration Manager com Service Pack 1  

Se você usar a mídia de linha de base 1606 versão baixada antes de 15 de dezembro de 2016, você pode atualizar apenas o seguinte para uma versão totalmente licenciada do System Center Configuration Manager versão 1606:
-   Uma instalação de avaliação do System Center Configuration Manager versão 1606
-   System Center 2012 Configuration Manager com Service Pack 2
-   System Center 2012 R2 Configuration Manager com Service Pack 1

<!-- Version 1511 has now dropped out of support
**Upgrade to version 1511**  
When you have version 1511 baseline media, you can upgrade the following to a fully licensed  version of System Center Configuration Manager version 1511:  
-   An evaluation install of System Center Configuration Manager version 1511
-   A release candidate install of System Center Configuration Manager  
-   System Center 2012 Configuration Manager with Service Pack 1  
-   System Center 2012 Configuration Manager with Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center 2012 R2 Configuration Manager with Service Pack 1  
-->


> [!TIP]  
>  Quando você atualiza de uma versão do System Center 2012 Configuration Manager para a ramificação atual, você poderá simplificar o processo de atualização. Para obter mais informações, consulte o seguinte:  
>   
>  -   A secção [Versões de linha de base e de atualização](../../../../core/servers/manage/updates.md#bkmk_Baselines) em [Atualizações para o System Center Configuration Manager](../../../../core/servers/manage/updates.md)  
>  -   [O CD. Pasta mais recente para o System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md)  

 **As seguintes ações não são suportadas:**  
-   Não há suporte para atualizar uma visualização técnica do System Center Configuration Manager para uma instalação totalmente licenciada.  Uma versão de Technical Preview só pode atualizar para uma versão posterior do Technical Preview.  

-   Não há suporte para a migração de uma Technical Preview para uma versão totalmente licenciada.  

##  <a name="bkmk_checklist"></a> Listas de verificação de atualização  
 As listas de verificação a seguir podem ajudá-lo a planejar uma atualização bem-sucedida para o System Center Configuration Manager.  

### <a name="before-you-upgrade"></a>Antes da atualização  

**Revisar seu ambiente do System Center 2012 Configuration Manager** e resolver problemas como detalhado no KB4018655: [Clientes do Configuration Manager reinstale a cada cinco horas devido a uma tarefa recorrente de repetição e pode causar uma atualização de cliente inadvertida](https://support.microsoft.com/help/4018655).

**Certifique-se de que o ambiente computacional atende às configurações com suporte** que são necessárias para atualizar para o System Center Configuration Manager:  

Reveja os sistemas operativos de servidor utilizados para alojar funções do sistema de sites:  

-   Alguns sistemas operacionais mais antigos com suporte do System Center 2012 Configuration Manager não são suportados pelo System Center Configuration Manager, e funções do sistema de site nesses sistemas operacionais devem ser realocadas ou removidas antes da atualização. Examine o [sistemas operacionais com suporte para servidores de sistema de Site](../../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md) documentação.   
-   O verificador de pré-requisitos para o Configuration Manager não verifica os pré-requisitos para funções do sistema de site no servidor do site ou em sistemas de site remoto  

Reveja os pré-requisitos necessários de cada computador que aloje uma função do sistema de sites:  

-   Por exemplo, para implantar um sistema operacional, o System Center Configuration Manager usa o Windows 10 Kit de avaliação e implantação (Windows ADK). Antes de executar o Programa de Configuração, tem de transferir e instalar o Windows 10 ADK no servidor do site e em cada computador que execute uma instância do Fornecedor de SMS.  

Para obter informações gerais sobre as plataformas suportadas e configurações de pré-requisitos, veja [Configurações suportadas do System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md).  

Para obter informações sobre como usar o Windows ADK com o Configuration Manager, consulte [requisitos de infraestrutura para implantação de sistema operacional no System Center Configuration Manager](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

**Examine o status do site e hierarquia e verifique se há problemas não resolvidos:**  
Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, do servidor da base de dados do site e de funções de sistema de sites que se encontrem instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.  

**Instale todas as atualizações críticas aplicáveis para sistemas operacionais em computadores que hospedam o site, o servidor de banco de dados do site e funções do sistema de site remoto:**  
Antes de atualizar um site, instale as atualizações críticas em cada sistema de sites aplicável. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização do service pack.  

Para obter mais informações, consulte [Windows Update](http://go.microsoft.com/fwlink/p/?LinkId=105851).  

**Desinstale as funções de sistema de site não tem suportadas pelo System Center Configuration Manager:**  
As seguintes funções de sistema de site não são mais usadas no System Center Configuration Manager e devem ser desinstaladas antes da atualização do System Center 2012 Configuration Manager:  

-   Ponto de Gestão Fora de Banda  
-   Ponto de Validação do Estado de Funcionamento do Sistema  

**Desabilite as réplicas de banco de dados para pontos de gerenciamento em sites primários:**  
Gerenciador de configuração não é possível atualizar um site primário que tenha uma réplica de banco de dados para pontos de gerenciamento habilitado com êxito. Desative a replicação de base de dados antes de:  

-   Criar uma cópia de segurança da base de dados do site para testar a atualização da base de dados  
-   Atualizar o site de produção para o System Center Configuration Manager  

Para obter mais informações, consulte o seguinte:  
-   System Center 2012 Configuration Manager:  [Configurar réplicas de banco de dados para pontos de gerenciamento](https://technet.microsoft.com/library/hh846234.aspx)  
-   System Center Configuration Manager: [Réplicas de banco de dados para pontos de gerenciamento do System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)  

**Reconfigure pontos de atualização de software que usam NLBs:**  
Gerenciador de configuração não pode atualizar um site que usa um cluster de balanceamento de carga de rede (NLB) para hospedar pontos de atualização de software.  

Se utilizar clusters de NLB em pontos de atualização de software, utilize o PowerShell para remover o cluster de NLB. (Não começando com o System Center 2012 Configuration Manager SP1, havia nenhuma opção no console do Configuration Manager para configurar um cluster NLB)  

**Desabilite todas as tarefas de manutenção de site em cada site para a duração da atualização do site:**  
Antes de atualizar para o System Center Configuration Manager, desabilite qualquer tarefa de manutenção de site que possam ser executadas durante o tempo que o processo de atualização está ativo. Estas incluem as seguintes, entre outras:  

-   Servidor do Site de Reserva  
-   Eliminar Operações de Cliente Desatualizadas  
-   Eliminar Dados de Deteção Desatualizados  

Se uma tarefa de manutenção de base de dados do site for executada durante o processo de atualização, a atualização do site poderá falhar.  

Antes de desativar uma tarefa, registe a agenda da tarefa para que possa restaurar a respetiva configuração uma vez concluída a atualização do site.  

Para obter mais informações sobre tarefas de manutenção do site, consulte:  

-   System Center 2012 Configuration Manager:  [Planejando tarefas de manutenção do Configuration Manager](https://technet.microsoft.com/library/gg712686.aspx)  
-   System Center Configuration Manager:  [Referência para tarefas de manutenção para o System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md)  

**Execute o Verificador de Pré-requisitos da Configuração**:  
Antes de atualizar um site, pode executar o **Verificador de Pré-requisitos** independentemente da Configuração para confirmar que o site cumpre os pré-requisitos. Posteriormente, quando você atualiza o site, o verificador de pré-requisitos é executado novamente.  

Se você usar a mídia de linha de base para a versão 1606 da versão de outubro de 2016, a verificação de pré-requisitos independente avalia o site para atualização para o Branch atual e a longo prazo manutenção LTSB (Branch) do System Center Configuration Manage. Porque não há suporte para alguns recursos de LTSB, você poderá ver entradas na *ConfigMgrPrereq.log* que são semelhante à seguinte:
 - INFO: O site é uma edição LTSB.
 - Função do sistema de site sem suporte 'Ponto de sincronização do Asset Intelligence' para a edição de LTSB;    Erro;    Configuration Manager detectou que o 'ponto de sincronização do Asset Intelligence' está instalado. Não há suporte para a inteligência de ativos na edição LTSB. Você deve desinstalar a função de sistema de site do ponto de sincronização do Asset Intelligence antes de continuar.

Se você pretende atualizar para o Branch atual, erros para a edição de LTSB podem ser ignorados. Elas se aplicam apenas se você pretende atualizar para o LTSB.

Posteriormente, quando você executa a instalação do Configuration Manager para fazer a atualização, a verificação de pré-requisitos executar novamente e avaliar o seu site com base na ramificação do System Center Configuration Manager você optar por instalar (ramificação atual ou LTSB). Se você optar por atualizar para a ramificação atual, a verificação de recursos que não há suporte para o LTSB não são executados.

Para obter mais informações, consulte o [Verificador de pré-requisitos](/sccm/core/servers/deploy/install/prerequisite-checker) e [List of Prerequisite Checks for System Center Configuration Manager](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

**Baixe arquivos de pré-requisitos e arquivos redistribuíveis para o System Center Configuration Manager:**    
Use **Downloader de instalação** para baixar arquivos de pré-requisitos redistribuíveis, pacotes de idiomas e as atualizações de produto mais recentes para o System Center Configuration Manager.  

Para obter informações, consulte [Downloader de instalação](/sccm/core/servers/deploy/install/setup-downloader).  

**Planeie a gestão do servidor e dos idiomas de cliente**:  
Quando atualiza um site, a atualização do site instala apenas as versões do pacote de idiomas que selecionar durante a atualização.  

-   O Programa de Configuração analisa a configuração de idioma atual do site e, em seguida, identifica os pacotes de idiomas que estão disponíveis na pasta onde armazenou os ficheiros de pré-requisitos previamente transferidos.  
-   Em seguida, poderá confirmar a seleção dos pacotes de idiomas atuais do servidor e dos clientes, ou alterar as seleções de forma a adicionar ou remover o suporte para idiomas.  
-   Apenas pode selecionar os pacotes de idiomas que estão disponíveis quando executa o Programa de Configuração (os quais obtém juntamente com os ficheiros dos pré-requisitos que transfere).  

> [!NOTE]  
>  Você não pode usar os pacotes de idiomas do System Center 2012 Configuration Manager para habilitar idiomas para um site do System Center Configuration Manager.  

Para obter mais informações sobre pacotes de idiomas, consulte [pacotes de idiomas no System Center Configuration Manager](../../../../core/servers/deploy/install/language-packs.md).  

**Reveja as considerações sobre as atualizações de sites**:  
Ao atualizar um site, algumas funcionalidades e configurações são repostas para uma configuração predefinida. Para o ajudar a preparar-se para estas e outras alterações relacionadas, reveja a informação disponível em  [Considerações sobre atualizações](#bkmk_considerations).  

**Crie um backup do banco de dados do site no site de administração central e sites primários:**  
Antes de atualizar um site, efetue uma cópia de segurança da base de dados do site para garantir que poderá utilizar uma cópia de segurança válida em caso de recuperação de desastres.  

Consulte [Backup e recuperação para o System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md).  

**Cópia de segurança de um ficheiro Configuration.mof personalizado**:  
Se utilizar um ficheiro Configuration.mof personalizado para definir as classes de dados que utiliza com o inventário de hardware, crie uma cópia de segurança deste ficheiro antes de atualizar o site. Em seguida, após a atualização, restaure este ficheiro para o seu site. Para obter mais informações sobre como usar esse arquivo, consulte [como estender o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

**Teste o processo de atualização de banco de dados em uma cópia do backup do banco de dados mais recente do site:**  
Antes de atualizar um site de administração central do Configuration Manager ou um site primário, teste o processo de atualização da base de dados do site numa cópia da base de dados do site.  

-   Deve testar o processo de atualização da base de dados do site porque, ao atualizar um site, a base de dados do mesmo pode ser modificada  
-   Embora não seja necessário testar a atualização da base de dados, o teste pode identificar problemas da atualização antes que a base de dados de produção seja afetada  
-   Uma atualização da base de dados do site efetuada incorretamente pode deixar a base de dados do site inoperável, podendo ser necessário efetuar uma recuperação do site de forma a restaurar o funcionamento  
-   Embora a base de dados do site seja partilhada entre os sites de uma hierarquia, planeie o teste da base de dados em cada site aplicável antes de atualizar esse site  
-   Se utiliza réplicas de bases de dados para pontos de gestão num site primário, desative a replicação antes de criar a cópia de segurança da base de dados do site  

Configuration Manager não oferece suporte o backup de sites secundários nem o teste de atualização de um banco de dados do site secundário.  

A execução de um teste de atualização da base de dados na base de dados do site de produção não é suportada. Tal procedimento atualiza a base de dados do site, podendo fazer com que este deixe de funcionar.  

Para obter mais informações, veja [Testar a atualização da base de dados do site](#bkmk_test).  

**Reinicie o servidor do site e cada computador que hospeda uma função de sistema de site**:  
Isso é feito para garantir que existe há ações pendentes de uma instalação recente de atualizações ou de pré-requisitos e é um processo interno específico da empresa.  

**Atualizar sites**:  
Iniciando no site de nível superior na hierarquia, execute Setup.exe da mídia de origem do System Center Configuration Manager.  

Após a atualização do site de nível superior, pode começar a atualização de cada site subordinado. Conclua a atualização de cada site antes de iniciar a atualização do site seguinte  

Até que todos os sites em sua hierarquia sejam atualizados para o System Center Configuration Manager, a hierarquia opera em um modo com versões mistas.  

Para obter informações sobre como executar a atualização, consulte [atualizar sites](#bkmk_upgrade).  

### <a name="after-you-upgrade"></a>Depois da atualização  
**Atualizar consoles autônomos do Configuration Manager**:  
Por padrão, quando você atualiza um site de administração central ou site primário, a instalação também atualiza o console do Configuration Manager está instalado no servidor do site. No entanto, tem de atualizar manualmente cada consola que esteja instalada num computador que não seja o servidor do site.  

> [!TIP]  
>  Feche cada consola aberta antes de iniciar a atualização.  

Para obter mais informações, veja [Instalar consolas do System Center Configuration Manager](../../../../core/servers/deploy/install/install-consoles.md).  

**Reconfigure réplicas de banco de dados para pontos de gerenciamento em sites primários:**  
Se utilizar réplicas de base de dados para pontos de gestão em sites primários, necessitará de desinstalar as réplicas de base de dados antes de atualizar o site. Após atualizar um site primário, reconfigure a réplica da base de dados para pontos de gestão.   
Para obter mais informações, veja [Réplicas de bases de dados para pontos de gestão do System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigure quaisquer tarefas de manutenção de banco de dados desabilitadas antes da atualização:**  
Se tiver desativado [tarefas de manutenção da base de dados para o System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md) num site antes da atualização, reconfigure essas tarefas no site com as definições que estavam aplicadas antes da atualização do site.  

**Atualizar clientes**:  
Depois que todos os seus sites de atualização para o System Center Configuration Manager, planeje a atualização de clientes.  

Ao atualizar um cliente, o software atual do cliente é desinstalado e é instalada a nova versão do software de cliente. Para atualizar os clientes, pode utilizar qualquer método suportado pelo Configuration Manager.  

> [!TIP]  
>  Ao atualizar o site de nível superior de uma hierarquia, também é atualizado o pacote de instalação de cliente de cada ponto de distribuição da hierarquia. Ao atualizar um site primário, o pacote de atualização de cliente disponível nesse site primário é atualizado.  

Para obter informações sobre como atualizar clientes existentes e sobre como instalar novos clientes, veja [Como atualizar clientes em computadores Windows no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

##  <a name="bkmk_considerations"></a> Considerações sobre atualizações  
**Ações automáticas**:  
Quando você atualiza para o System Center Configuration Manager, as seguintes ações ocorrem automaticamente:  

-   O site efetua uma reposição do site, a qual inclui uma reinstalação de todas as funções do sistema de sites.  
-   Caso o site seja o site de nível superior de uma hierarquia, atualizará o pacote de instalação de cliente em todos os pontos de distribuição da hierarquia. O site também atualiza as imagens de arranque predefinidas para utilizar a nova versão do Windows PE incluída no Windows Assessment and Deployment Kit 10. No entanto, a atualização não atualiza suportes de dados existentes para utilização com implementação de imagens.  
-   Caso o site seja um site primário, atualizará o pacote de atualização de cliente para esse site.  

**Ações manuais do usuário administrativo após uma atualização**   
Depois de atualizar um site, certifique-se de que as seguintes ações são executadas:  

-   Certifique-se de que os clientes atribuídos a cada site primário atualizam e instalam o software de cliente da nova versão  
-   Atualizar cada console do Configuration Manager que se conecta ao site e que são executados em um computador remoto do servidor do site  
-   Nos sites primários onde utiliza réplicas de bases de dados para pontos de gestão, reconfigure as réplicas de base de dados  
-   Depois da atualização do site, tem de atualizar manualmente os suportes de dados físicos, tais como ficheiros ISO para CD e DVD ou pens USB, ou suportes de dados pré-configurados utilizados para implementações do Windows To Go ou fornecidos a fornecedores de hardware. Embora a atualização do site atualize as imagens de inicialização padrão, não é possível atualizar esses arquivos de mídia ou dispositivos usados externos ao Configuration Manager  
-   Planeie a atualização de imagens de arranque não predefinidas quando não precisa da versão original (mais antiga) do Windows PE.  

**Ações que afetam configurações e definições**   
Quando um site é atualizado para o System Center Configuration Manager, algumas definições e configurações não permanecem após a atualização ou são definidas para uma nova configuração padrão. A tabela seguinte inclui as definições que não são mantidas ou que são alteradas, bem como informações que o ajudam a efetuar o planeamento das mesmas durante a atualização de sites:  

-   **Centro de Software:**  
    Os seguintes itens do Centro de Software são repostos nos valores predefinidos:  
    -   A opção**Informação de trabalho** é reposta para um horário de expediente das **5h00** às **22h00** Monday às Friday.  
    -   O valor de **Manutenção do computador** é definido como **Suspender as atividades do Centro de Software quando o computador estiver em modo de apresentação**.  
    -   O valor de **Controlo remoto** é definido com o valor existente nas definições de cliente que foram atribuídas ao computador.  
-   **Agendamentos de resumo de atualização de software:**  
     Os agendamentos de resumo personalizados para atualizações de software ou grupos de atualizações de software são repostos no valor predefinido de 1 hora. Após a conclusão da atualização, reponha os valores de resumo personalizados na frequência pretendida.  

##  <a name="bkmk_test"></a> Testar a atualização da base de dados do site  
As informações a seguir se aplica somente quando você estiver atualizando uma versão anterior, como o System Center 2012 Configuration Manager para o System Center Configuration Manager.

Antes de atualizar um site, teste uma cópia do banco de dados do site para a atualização.  

Para testar o banco de dados para uma atualização, primeiro restaure uma cópia do banco de dados do site para uma instância do SQL Server que não hospede um site do Configuration Manager. A versão do SQL Server que você pode usar para hospedar a cópia do banco de dados deve ser uma versão do SQL Server que a versão do Configuration Manager oferece suporte a que é a origem da cópia do banco de dados.  

Em seguida, depois de restaurar o banco de dados do site, no computador do SQL Server, execute a instalação do Configuration Manager da pasta de mídia de origem para o System Center Configuration Manager com o **/TESTDBUPGRADE** opção de linha de comando.  

-   Para obter informações sobre como criar e restaurar uma cópia de segurança da base de dados do site, veja [Opções da linha de comandos para Configuração](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  
-   Para obter informações sobre a opção da linha de comandos **/TESTDBUPGRADE**, veja a tabela da secção [Opções da linha de comandos para Configuração](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  
-   Para obter informações sobre as versões suportadas do SQL Server, veja o tópico [Suporte para versões do SQL Server para o System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

> [!TIP]  
>  Se você integrar o Microsoft Intune com o Configuration Manager:  
>   
>  Quando executa um teste de atualização da base de dados numa cópia da base de dados do site com 5 ou mais dias, poderá receber uma das seguintes mensagens:  
>   
>  -   AVISO: A atualização forçará uma sincronização completa para a nuvem.  
>  -   ERRO: Atualização do banco de dados forçará uma sincronização completa para a nuvem.  
>   
> Ambos podem ser ignoradas durante o teste de uma atualização de banco de dados, pois elas não indicam uma falha ou problema com a atualização de teste. Em vez disso, eles indicam que, durante a atualização real, dados do **nuvem** grupo de replicação de banco de dados pode ser sincronizados com o Microsoft Intune.  

Utilize o seguinte procedimento em cada site de administração central e site primário que pretenda atualizar.  

#### <a name="to-test-a-site-database-for-upgrade"></a>Para testar uma base de dados do site para atualização  

1.  Faça uma cópia do banco de dados do site e, em seguida, restaure essa cópia para uma instância do SQL Server que usa a mesma edição do banco de dados do site e que não hospede um site do Configuration Manager. Por exemplo, se a base de dados do site for executada numa instância da edição Enterprise do SQL Server, certifique-se de que restaura a base de dados para uma instância do SQL Server que também execute a edição Enterprise do SQL Server.  

2.  Depois de restaurar a cópia do banco de dados, execute a instalação da mídia de origem para o System Center Configuration Manager. Ao executar a Configuração, utilize a opção da linha de comandos **/TESTDBUPGRADE** . Se a instância do SQL Server que aloja a cópia da base de dados não for a instância predefinida, terá de fornecer também os argumentos da linha de comandos para identificar a instância que aloja a cópia da base de dados do site.  

     Por exemplo, planeia atualizar uma base de dados do site denominada SMS_ABC. Restaura uma cópia desta base de dados do site para uma instância suportada do SQL Server com o nome de instância DBTest. Para testar uma atualização dessa cópia do banco de dados do site, use a seguinte linha de comando: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     Você pode encontrar o Setup.exe no seguinte local na mídia de origem para o System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

3.  Na instância do SQL Server em que executou o teste da atualização da base de dados, monitorize o progresso e êxito do ficheiro ConfigMgrSetup.log, na raiz da unidade do sistema:  

    -   Se o teste da atualização falhar, resolva eventuais problemas relacionados com a falha da atualização da base de dados do site, crie uma nova cópia de segurança da base de dados do site e teste a atualização da nova cópia da base de dados do site.  
    -   Após a conclusão do processo com êxito, poderá eliminar a cópia da base de dados.  

        > [!NOTE]  
        >  O restauro da cópia da base de dados do site utilizada para o teste da atualização não é suportado para utilização como base de dados de qualquer site.  

Após atualizar com êxito uma cópia do banco de dados do site, prossiga com a atualização de site do Configuration Manager e seu banco de dados do site.  

##  <a name="bkmk_upgrade"></a> Atualizar sites  
Depois de concluir as configurações de pré-atualização do seu site, teste a atualização de dados do site em uma cópia do banco de dados e baixar arquivos de pré-requisitos e pacotes de idiomas para a versão do service pack que planeja instalar, você está pronto para atualizar seu site do Configuration Manager.  

Ao atualizar um site numa hierarquia, deverá atualizar primeiro o site de nível superior da hierarquia. Este site de nível superior é um site de administração central ou um site primário autónomo. Após a conclusão da atualização de um site de administração central, será possível atualizar os sites primários subordinados pela ordem que entender. Depois de atualizar um site primário, você pode atualizar sites secundários do filho do site ou atualizar sites primários adicionais antes de atualizar quaisquer sites secundários.  

Para atualizar um site de administração central ou site primário, execute o programa de instalação da mídia de origem do System Center Configuration Manager. No entanto, não deverá executar o Programa de Configuração para atualizar sites secundários. Em vez disso, você deve usar o console do Configuration Manager para atualizar um site secundário após concluir a atualização do seu site pai primário.  

Antes de atualizar um site, feche o console do Configuration Manager está instalado no servidor do site até após a atualização do site. Além disso, feche cada console do Configuration Manager que é executado em computadores diferentes do servidor do site. Poderá voltar a ligar a consola após a conclusão da atualização do site. No entanto, até você atualizar um console do Configuration Manager para a nova versão do Configuration Manager, esse console não poderá exibir alguns objetos e informações que estão disponíveis na nova versão do Configuration Manager.  

Use os procedimentos a seguir para atualizar sites do Configuration Manager:  

#### <a name="to-upgrade-a-central-administration-site-or-primary-site"></a>Para atualizar um site de administração central ou site primário  

1.  Certifique-se de que o utilizador que executa o Programa de Configuração possui os seguintes direitos de segurança:  

    -   Direitos de Administrador Local no computador do servidor de site.  
    -   Direitos de Administrador Local no servidor da base de dados do site remoto, se for remoto.    </br></br>

2.  No computador do servidor do site, abra o Windows Explorer e navegue para  **&lt;ConfigMgSourceMedia\>\SMSSETUP\BIN\X64**.  

3.  Faça duplo clique em **Setup.exe**. Abre o Assistente de instalação do Configuration Manager.  

4.  Na página **Antes de Começar** , clique em **Seguinte**.  

5.  Na página **Introdução** , selecione **Atualizar este site do Configuration Manager**e clique em **Seguinte**.  

6.  Na página **Chave de Produto** , clique em **Seguinte**.  

     Se você instalou anteriormente a avaliação do Configuration Manager, você pode selecionar **instalar a edição licenciada deste produto**e, em seguida, insira a chave do produto para a instalação completa do Configuration Manager para converter o site para a versão completa.  

     Começando com a versão de outubro de 2016 da mídia versão 1606 da linha de base para o System Center Configuration Manager, você pode especificar a data de validade do seu contrato de Software Assurance. Você também tem a opção de especificar o **data de expiração do Software Assurance** do seu contrato de licença como um lembrete conveniente dessa data. Se você não inserir isso durante a instalação, você pode especificá-lo mais tarde no console do Configuration Manager.

     >  [!NOTE]   
     >  Microsoft não valida a data de validade inserido e não usará essa data para validação de licença.  Em vez disso, você pode usá-lo como um lembrete de data de expiração. Isso é útil porque o Configuration Manager periodicamente verifica se há novas atualizações de software oferecido online e o status de licença do software assurance deve ser atualizado para ser qualificado para usar essas atualizações adicionais.    

     Para obter mais informações, consulte [licenciamento e ramificações para o System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

7.  Na página **Termos de Licenciamento para Software Microsoft** , leia e aceite os termos de licenciamento e clique em **Seguinte**.  

8.  Na página **Licenças de Pré-requisitos** , leia e aceite os termos de licenciamento do software de pré-requisito e clique em **Seguinte**. O programa de configuração transfere e instala automaticamente o software em sistemas de sites ou clientes, quando necessário. Tem de selecionar todas as caixas de verificação para avançar para a página seguinte.  

9. Na página **Transferências de Pré-requisitos** , especifique se a Configuração deverá transferir os ficheiros redistribuíveis de pré-requisitos, pacotes de idiomas e atualizações de produto mais recentes a partir da Internet ou utilizar ficheiros transferidos anteriormente, e clique em **Seguinte**. Se tiver transferido anteriormente os ficheiros através do Dispositivo de Transferência da Configuração, selecione **Utilizar ficheiros anteriormente transferidos** e especifique a pasta para transferência. Para obter mais informações, consulte [Downloader de instalação](/sccm/core/servers/deploy/install/setup-downloader).

    > [!NOTE]  
    >  Quando utilizar ficheiros transferidos anteriormente, verifique se o caminho para a pasta de transferência contém a versão mais recente dos ficheiros.  

10. Na página **Seleção do Idioma do Servidor** , veja a lista de idiomas atualmente instalados para o site. Selecione os idiomas adicionais que estão disponíveis nesse site para o Configuration Manager console e relatórios, ou limpe os idiomas que você não deseja oferecer suporte nesse site e, em seguida, clique em **próximo**. Por predefinição, está seleccionado o inglês e não pode ser removido.  

    > [!IMPORTANT]  
    >  Cada versão do Configuration Manager não pode usar pacotes de idiomas de uma versão anterior do Configuration Manager. Para habilitar o suporte para um idioma em um site do Configuration Manager que você atualizar, você deve usar a versão do pacote de idiomas da nova versão. Por exemplo, durante a atualização do System Center 2012 Configuration Manager para o System Center Configuration Manager, se a versão do System Center Configuration Manager de um pacote de idiomas não estiver disponível com os arquivos de pré-requisitos baixados, suporte para o idioma não pode ser instalado.  

11. Na página **Seleção do Idioma do Cliente** , veja a lista de idiomas atualmente instalados para o site. Selecione idiomas adicionais disponíveis neste site para computadores cliente ou desmarque os idiomas que já não seja necessário suportar no site. Especifique se pretende ativar todos os idiomas de cliente para clientes de dispositivos móveis e clique em **Seguinte**. Por predefinição, está seleccionado o inglês e não pode ser removido.  

    > [!IMPORTANT]  
    >  Cada versão do Configuration Manager não pode usar pacotes de idiomas de uma versão anterior do Configuration Manager. Para habilitar o suporte para um idioma em um site do Configuration Manager que você atualizar, você deve usar a versão do pacote de idiomas da nova versão. Por exemplo, durante a atualização do System Center 2012 Configuration Manager para o System Center Configuration Manager, se a versão do System Center Configuration Manager de um pacote de idiomas não estiver disponível com os arquivos de pré-requisitos baixados, suporte para o idioma não pode ser instalado.  

12. Na página **Resumo de Definições** , clique em **Seguinte** para iniciar o Verificador de Pré-requisitos para verificar a prontidão do servidor para a atualização do site.  

13. Se não forem listados problemas na página **Verificação da Instalação de Pré-requisitos** , clique em **Seguinte** para atualizar o site e as funções do sistema de sites. Quando o Verificador de Pré-requisitos detetar um problema, clique num item da lista para obter detalhes sobre como resolver o problema. Antes de continuar a Configuração, resolva todos os itens da lista com estado de **Erro** . Depois de resolver o problema, clique em **Executar Verificação** para reiniciar a verificação de pré-requisitos. Pode também abrir o ficheiro ConfigMgrPrereq.log na raiz da unidade do sistema para rever os resultados do Verificador de Pré-requisitos. O ficheiro de registo pode conter informações adicionais que não são apresentadas na interface de utilizador. Para obter uma lista de regras de pré-requisitos de instalação e descrições, consulte [Verificador de pré-requisito](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

Na página **Atualizar** , a Configuração apresenta o estado do progresso global. Quando o Programa de Configuração concluir a instalação do servidor do site principal e do sistema de sites, pode fechar o assistente. A configuração do site continua em segundo plano.  

#### <a name="to-upgrade-a-secondary-site"></a>Para atualizar um site secundário  

1.  Certifique-se de que o utilizador administrativo que executa o Programa de Configuração possui os seguintes direitos de segurança:  

    -   Direitos de Administrador Local no computador do site secundário  
    -   Administrador de Infraestrutura ou um direito de acesso de Administrador Total no site primário principal  
    -   Direitos de administrador de sistema (AS) na base de dados do site secundário  
    </br>
2.  Na consola do Configuration Manager, clique em **Administração**.  

3.  Na área de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.  

4.  Selecione o site secundário que pretende atualizar e, no separador **Home Page** , no grupo **Site** , clique em **Atualizar**.  

5.  Clique em **Sim** para confirmar a decisão e iniciar a atualização do site secundário.  

A atualização do site secundário continuará em segundo plano. Depois que a atualização for concluída, você pode confirmar o status no console do Configuration Manager. Para confirmar o estado, selecione o servidor do site secundário e, no separador **Home Page** , no grupo **Site** , clique em **Mostrar Estado da Instalação**.  

##  <a name="BKMK_PostUpgrade"></a> Efetuar tarefas pós-atualização  
Após atualizar um site para um novo Service Pack, poderá ter de executar tarefas adicionais para concluir a atualização ou reconfigurar o site. Essas tarefas podem incluir a atualização de clientes do Configuration Manager ou de consoles do Configuration Manager, reabilitar réplicas de banco de dados para pontos de gerenciamento ou restaurar as configurações para a funcionalidade do Configuration Manager que você usar e que não persiste após a atualização do service pack.  

**Problemas conhecidos para sites secundários:**  
- **Quando você atualizar para a versão 1511:** Para garantir que os clientes em sites secundários podem localizar o ponto de gerenciamento do site secundário (ponto de gerenciamento proxy), adicione manualmente o ponto de gerenciamento para grupos de limites que também incluem os pontos de distribuição no site secundário.  

- **Quando você atualizar para a versão 1606 ou posterior:** Pontos de gerenciamento proxy são automaticamente adicionados a grupos de limites que incluem pontos de distribuição no site secundário.


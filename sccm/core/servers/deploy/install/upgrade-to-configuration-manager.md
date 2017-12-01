---
title: Atualizar para o System Center Configuration Manager
description: "Saiba os passos para executar uma atualização no local com êxito a partir de um site e hierarquia que executa o System Center 2012 Configuration Manager."
ms.custom: na
ms.date: 6/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
caps.latest.revision: "21"
author: mstewart
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 49a356ac1777c971d997a2109328001d750d15b0
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="upgrade-to-system-center-configuration-manager"></a>Atualizar para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode executar uma atualização no local a atualização para System Center Configuration Manager de um site e hierarquia que executa o System Center 2012 Configuration Manager.  

 Antes de atualizar do System Center 2012 Configuration Manager, tem de preparar sites que requer a remoção de configurações específicas que podem impedir uma atualização com êxito e, em seguida, siga a sequência de atualização quando mais do que um único site está envolvida.  

 > [!TIP]
 > Ao gerir o site do System Center Configuration Manager e a infraestrutura de hierarquia, os termos de licenciamento *atualizar*, *atualizar*, e *instalar* são utilizados para descrever três conceitos diferentes. Para saber como cada termo é utilizado, consulte [sobre a atualização, atualização e instalação](/sccm/core/understand/upgrade-update-install).

##  <a name="bkmk_path"></a> Caminhos de atualização no local  

**Atualize para versão 1702**   
Quando tiver versão 1702 da linha de base de dados, pode atualizar o seguinte para uma versão totalmente licenciada do System Center Configuration Manager versão 1702:   
-     Uma instalação de avaliação do System Center Configuration Manager versão 1702
-     System Center 2012 Configuration Manager sem Service Pack 1
-     System Center 2012 Configuration Manager sem Service Pack 2
-     System Center 2012 R2 Configuration Manager
-     System Center 2012 R2 Configuration Manager sem Service Pack 1

**Atualize para versão 1606**  
No dia 15 de Dezembro de 2016, o suporte de dados de linha de base para a versão 1606 foi rereleased para adicionar suporte para cenários de atualização adicionais. Esta nova versão suporta a atualização dos seguintes procedimentos para uma versão totalmente licenciada do System Center Configuration Manager versão 1606 de:  
-   Uma instalação de avaliação do System Center Configuration Manager versão 1606
-   Uma instalação de release candidate do System Center Configuration Manager  
-   System Center 2012 Configuration Manager sem Service Pack 1  
-   System Center 2012 Configuration Manager sem Service Pack 2  
-   System Center 2012 R2 Configuration Manager sem service Pack
-   System Center 2012 R2 Configuration Manager sem Service Pack 1  

Se utilizar o suporte de dados de linha de base 1606 versão transferido antes do dia 15 de Dezembro de 2016, pode atualizar apenas o seguinte para uma versão totalmente licenciada do System Center Configuration Manager versão 1606 de:
-   Uma instalação de avaliação do System Center Configuration Manager versão 1606
-   System Center 2012 Configuration Manager sem Service Pack 2
-   System Center 2012 R2 Configuration Manager sem Service Pack 1

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
>  Ao atualizar a partir de uma versão do System Center 2012 Configuration Manager Current Branch, poderá simplificar o processo de atualização. Para obter mais informações, consulte o seguinte:  
>   
>  -   A secção [Versões de linha de base e de atualização](../../../../core/servers/manage/updates.md#bkmk_Baselines) em [Atualizações para o System Center Configuration Manager](../../../../core/servers/manage/updates.md)  
>  -   [CD. Pasta mais recente para o System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md)  

 **As seguintes ações não são suportadas:**  
-   Não é suportada para atualizar uma versão de pré-visualização técnica do System Center Configuration Manager para uma instalação totalmente licenciada.  Uma versão de Technical Preview só pode atualizar para uma versão posterior do Technical Preview.  

-   A migração de um Technical Preview para uma versão totalmente licenciada não é suportada.  

##  <a name="bkmk_checklist"></a> Listas de verificação de atualização  
 As listas de verificação seguintes podem ajudar a planear uma atualização com êxito para o System Center Configuration Manager.  

### <a name="before-you-upgrade"></a>Antes da atualização  

**Reveja o seu ambiente do System Center 2012 Configuration Manager** e resolver problemas conforme detalhado no KB4018655: [Clientes do Configuration Manager reinstale a cada cinco horas devido a uma tarefa de repetição periódica e pode provocar uma atualização de cliente inadvertida](https://support.microsoft.com/help/4018655).

**Certifique-se de que o ambiente informático satisfaz as configurações suportadas** que são necessárias para atualizar para o System Center Configuration Manager:  

Reveja os sistemas operativos de servidor utilizados para alojar funções do sistema de sites:  

-   Alguns sistemas operativos suportados pelo System Center 2012 Configuration Manager não são suportados pelo System Center Configuration Manager e funções de sistema de sites nesses sistemas operativos têm de ser relocalizadas ou removidas antes da atualização. Reveja o [sistemas operativos suportados pelo servidores do sistema de sites](../../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md) documentação.   
-   Verificador de pré-requisitos para o Configuration Manager não verificar os pré-requisitos de funções de sistema de sites no servidor do site ou nos sistemas de sites remoto  

Reveja os pré-requisitos necessários de cada computador que aloje uma função do sistema de sites:  

-   Por exemplo, para implementar um sistema operativo, System Center Configuration Manager utiliza o Windows 10 Assessment and Deployment Kit (Windows ADK). Antes de executar o Programa de Configuração, tem de transferir e instalar o Windows 10 ADK no servidor do site e em cada computador que execute uma instância do Fornecedor de SMS.  

Para obter informações gerais sobre as plataformas suportadas e configurações de pré-requisitos, veja [Configurações suportadas do System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md).  

Para obter informações sobre como utilizar o Windows ADK com o Configuration Manager, consulte [requisitos de infraestrutura de implementação do sistema operativo no System Center Configuration Manager](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

**Rever o estado de site e da hierarquia e certifique-se de que existem não existem problemas por resolver:**  
Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, do servidor da base de dados do site e de funções de sistema de sites que se encontrem instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.  

**Instale todas as atualizações críticas aplicáveis para sistemas operativos em computadores que alojam o site, o servidor de base de dados do site e as funções do sistema de sites remoto:**  
Antes de atualizar um site, instale as atualizações críticas em cada sistema de sites aplicável. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização do service pack.  

Para obter mais informações, consulte [Windows Update](http://go.microsoft.com/fwlink/p/?LinkId=105851).  

**Desinstale as funções de sistema de sites não suportadas pelo System Center Configuration Manager:**  
As seguintes funções do sistema de sites já não são utilizadas no System Center Configuration Manager e tem de ser desinstaladas antes de atualizar do System Center 2012 Configuration Manager:  

-   Ponto de Gestão Fora de Banda  
-   Ponto de Validação do Estado de Funcionamento do Sistema  

**Desative réplicas de base de dados para pontos de gestão em sites primários:**  
O Configuration Manager não é possível atualizar com êxito um site primário que tenha uma réplica de base de dados para pontos de gestão ativada. Desative a replicação de base de dados antes de:  

-   Criar uma cópia de segurança da base de dados do site para testar a atualização da base de dados  
-   Atualizar o site de produção para o System Center Configuration Manager  

Para obter mais informações, consulte o seguinte:  
-   System Center 2012 Configuration Manager:  [Configurar réplicas de base de dados para pontos de gestão](https://technet.microsoft.com/library/hh846234.aspx)  
-   O System Center Configuration Manager: [Réplicas de base de dados para pontos de gestão do System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)  

**Reconfigure os pontos de atualização de software que utilizem NLB:**  
O Configuration Manager não consegue atualizar um site que utiliza um cluster de balanceamento de carga na rede (NLB) para alojar pontos de atualização de software.  

Se utilizar clusters de NLB em pontos de atualização de software, utilize o PowerShell para remover o cluster de NLB. (A partir do System Center 2012 Configuration Manager SP1, não havia nenhuma opção na consola do Configuration Manager para configurar um cluster NLB)  

**Desative todas as tarefas de manutenção do site em cada site durante a atualização desse site:**  
Antes de atualizar para o System Center Configuration Manager, desative as tarefas de manutenção do site que possam ser executadas enquanto o que o processo de atualização estiver ativo. Estas incluem as seguintes, entre outras:  

-   Servidor do Site de Reserva  
-   Eliminar Operações de Cliente Desatualizadas  
-   Eliminar Dados de Deteção Desatualizados  

Se uma tarefa de manutenção de base de dados do site for executada durante o processo de atualização, a atualização do site poderá falhar.  

Antes de desativar uma tarefa, registe a agenda da tarefa para que possa restaurar a respetiva configuração uma vez concluída a atualização do site.  

Para obter mais informações sobre tarefas de manutenção do site, consulte:  

-   System Center 2012 Configuration Manager:  [Planear tarefas de manutenção para o Configuration Manager](https://technet.microsoft.com/library/gg712686.aspx)  
-   O System Center Configuration Manager:  [Referência das tarefas de manutenção do System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md)  

**Execute o Verificador de Pré-requisitos da Configuração**:  
Antes de atualizar um site, pode executar o **Verificador de Pré-requisitos** independentemente da Configuração para confirmar que o site cumpre os pré-requisitos. Mais tarde, quando atualizar o site, o Verificador de pré-requisitos é executado novamente.  

Se utilizar o suporte de dados de linha de base para a versão 1606 a partir da versão de Outubro de 2016, a verificação de pré-requisitos independente avalia o site para atualizar para o ramo atual e a longo prazo Servicing Branch (LTSB) do System Center Configuration gerir. Porque algumas funcionalidades não são suportadas pelo LTSB, poderá ver entradas no *ConfigMgrPrereq.log* que são semelhante ao seguinte:
 - INFO: O site é uma edição de LTSB.
 - Função de sistema de sites não suportada 'Ponto de sincronização do Asset Intelligence' para a edição de LTSB;    Erro;    Configuration Manager detetou que o 'ponto de sincronização do Asset Intelligence' está instalado. Asset Intelligence não é suportado na edição LTSB. Tem de desinstalar a função de sistema de sites do ponto de sincronização do Asset Intelligence antes de poder continuar.

Se pretender atualizar para o ramo atual, o erros para a edição de LTSB podem ser ignorados. Apenas aplicam-se de que pretende atualizar para o LTSB.

Mais tarde, quando executar a configuração do Configuration Manager para efetuar a atualização, a verificação de pré-requisitos irá executar novamente e avaliar o seu site com base no ramo do System Center Configuration Manager optar por instalar (ramo atual, ou LTSB). Se optar por atualizar para o ramo atual, a verificação de funcionalidades que não são suportadas pelo LTSB não são executadas.

Para obter mais informações, consulte o [Verificador de pré-requisitos](/sccm/core/servers/deploy/install/prerequisite-checker) e [lista de pré-requisitos verifica para o System Center Configuration Manager](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

**Transfira os ficheiros de pré-requisitos e os ficheiros redistribuíveis para o System Center Configuration Manager:**    
Utilize **dispositivo de transferência da configuração** para transferir os ficheiros redistribuíveis de pré-requisitos, pacotes de idiomas e as atualizações de produto mais recentes para o System Center Configuration Manager.  

Para informações, consulte [dispositivo de transferência da configuração](/sccm/core/servers/deploy/install/setup-downloader).  

**Planeie a gestão do servidor e dos idiomas de cliente**:  
Quando atualiza um site, a atualização do site instala apenas as versões do pacote de idiomas que selecionar durante a atualização.  

-   O Programa de Configuração analisa a configuração de idioma atual do site e, em seguida, identifica os pacotes de idiomas que estão disponíveis na pasta onde armazenou os ficheiros de pré-requisitos previamente transferidos.  
-   Em seguida, poderá confirmar a seleção dos pacotes de idiomas atuais do servidor e dos clientes, ou alterar as seleções de forma a adicionar ou remover o suporte para idiomas.  
-   Apenas pode selecionar os pacotes de idiomas que estão disponíveis quando executa o Programa de Configuração (os quais obtém juntamente com os ficheiros dos pré-requisitos que transfere).  

> [!NOTE]  
>  Não é possível utilizar pacotes de idiomas do System Center 2012 Configuration Manager para ativar idiomas num site do System Center Configuration Manager.  

Para obter mais informações sobre pacotes de idiomas, consulte [pacotes de idiomas no System Center Configuration Manager](../../../../core/servers/deploy/install/language-packs.md).  

**Reveja as considerações sobre as atualizações de sites**:  
Ao atualizar um site, algumas funcionalidades e configurações são repostas para uma configuração predefinida. Para o ajudar a preparar-se para estas e outras alterações relacionadas, reveja a informação disponível em  [Considerações sobre atualizações](#bkmk_considerations).  

**Crie uma cópia de segurança da base de dados do site no site de administração central e sites primários:**  
Antes de atualizar um site, efetue uma cópia de segurança da base de dados do site para garantir que poderá utilizar uma cópia de segurança válida em caso de recuperação de desastres.  

Consulte [cópia de segurança e recuperação para o System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md).  

**Cópia de segurança de um ficheiro Configuration.mof personalizado**:  
Se utilizar um ficheiro Configuration.mof personalizado para definir as classes de dados que utiliza com o inventário de hardware, crie uma cópia de segurança deste ficheiro antes de atualizar o site. Em seguida, após a atualização, restaure este ficheiro para o seu site. Para obter mais informações sobre como utilizar este ficheiro consulte [como expandir o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

**Teste o processo de atualização de base de dados numa cópia da cópia de segurança de base de dados site mais recente:**  
Antes de atualizar um site de administração central do Configuration Manager ou um site primário, teste o processo de atualização da base de dados do site numa cópia da base de dados do site.  

-   Deve testar o processo de atualização da base de dados do site porque, ao atualizar um site, a base de dados do mesmo pode ser modificada  
-   Embora não seja necessário testar a atualização da base de dados, o teste pode identificar problemas da atualização antes que a base de dados de produção seja afetada  
-   Uma atualização da base de dados do site efetuada incorretamente pode deixar a base de dados do site inoperável, podendo ser necessário efetuar uma recuperação do site de forma a restaurar o funcionamento  
-   Embora a base de dados do site seja partilhada entre os sites de uma hierarquia, planeie o teste da base de dados em cada site aplicável antes de atualizar esse site  
-   Se utiliza réplicas de bases de dados para pontos de gestão num site primário, desative a replicação antes de criar a cópia de segurança da base de dados do site  

O Configuration Manager não suporta a cópia de segurança dos sites secundários nem o teste da atualização de uma base de dados do site secundário.  

A execução de um teste de atualização da base de dados na base de dados do site de produção não é suportada. Tal procedimento atualiza a base de dados do site, podendo fazer com que este deixe de funcionar.  

Para obter mais informações, veja [Testar a atualização da base de dados do site](#bkmk_test).  

**Reinicie o servidor de site e cada computador que aloje uma função de sistema de sites**:  
Isto é feito para se certificar de que existe existem ações pendentes de uma instalação recente de atualizações ou de pré-requisitos e é um processo interno específico da empresa.  

**Atualizar sites**:  
Começando no site de nível superior na hierarquia, execute Setup.exe a partir do suporte de dados de origem do System Center Configuration Manager.  

Após a atualização do site de nível superior, pode começar a atualização de cada site subordinado. Conclua a atualização de cada site antes de iniciar a atualização do site seguinte  

Até que todos os sites na sua hierarquia atualizam para o System Center Configuration Manager, a hierarquia funciona num modo com versões mistas.  

Para obter informações sobre como executar a atualização, consulte [atualizar sites](#bkmk_upgrade).  

### <a name="after-you-upgrade"></a>Depois da atualização  
**Atualizar consolas do Configuration Manager autónomo**:  
Por predefinição, quando atualizar um site de administração central ou site primário, a instalação também atualiza as consola do Configuration Manager que está instalada no servidor do site. No entanto, tem de atualizar manualmente cada consola que esteja instalada num computador que não seja o servidor do site.  

> [!TIP]  
>  Feche cada consola aberta antes de iniciar a atualização.  

Para obter mais informações, veja [Instalar consolas do System Center Configuration Manager](../../../../core/servers/deploy/install/install-consoles.md).  

**Reconfigure réplicas de base de dados para pontos de gestão em sites primários:**  
Se utilizar réplicas de base de dados para pontos de gestão em sites primários, necessitará de desinstalar as réplicas de base de dados antes de atualizar o site. Após atualizar um site primário, reconfigure a réplica da base de dados para pontos de gestão.   
Para obter mais informações, veja [Réplicas de bases de dados para pontos de gestão do System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigure as tarefas de manutenção de base de dados desativadas antes da atualização:**  
Se tiver desativado [tarefas de manutenção da base de dados para o System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md) num site antes da atualização, reconfigure essas tarefas no site com as definições que estavam aplicadas antes da atualização do site.  

**Atualizar clientes**:  
Depois de todos os seus sites atualizam para o System Center Configuration Manager, planeie a atualização dos clientes.  

Ao atualizar um cliente, o software atual do cliente é desinstalado e é instalada a nova versão do software de cliente. Para atualizar os clientes, pode utilizar qualquer método suportado pelo Configuration Manager.  

> [!TIP]  
>  Ao atualizar o site de nível superior de uma hierarquia, também é atualizado o pacote de instalação de cliente de cada ponto de distribuição da hierarquia. Ao atualizar um site primário, o pacote de atualização de cliente disponível nesse site primário é atualizado.  

Para obter informações sobre como atualizar clientes existentes e sobre como instalar novos clientes, veja [Como atualizar clientes em computadores Windows no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

##  <a name="bkmk_considerations"></a> Considerações sobre atualizações  
**Ações automáticas**:  
Quando atualizar para o System Center Configuration Manager, as seguintes ações ocorrem automaticamente:  

-   O site efetua uma reposição do site, a qual inclui uma reinstalação de todas as funções do sistema de sites.  
-   Caso o site seja o site de nível superior de uma hierarquia, atualizará o pacote de instalação de cliente em todos os pontos de distribuição da hierarquia. O site também atualiza as imagens de arranque predefinidas para utilizar a nova versão do Windows PE incluída no Windows Assessment and Deployment Kit 10. No entanto, a atualização não atualiza suportes de dados existentes para utilização com implementação de imagens.  
-   Caso o site seja um site primário, atualizará o pacote de atualização de cliente para esse site.  

**Ações manuais para o utilizador administrativo após uma atualização**   
Depois de atualizar um site, certifique-se de que as seguintes ações são efetuadas:  

-   Certifique-se de que os clientes atribuídos a cada site primário atualizam e instalam o software de cliente da nova versão  
-   Atualizar cada consola do Configuration Manager que liga ao site e que é executado no computador que esteja remoto a partir do servidor do site  
-   Nos sites primários onde utiliza réplicas de bases de dados para pontos de gestão, reconfigure as réplicas de base de dados  
-   Depois da atualização do site, tem de atualizar manualmente os suportes de dados físicos, tais como ficheiros ISO para CD e DVD ou pens USB, ou suportes de dados pré-configurados utilizados para implementações do Windows To Go ou fornecidos a fornecedores de hardware. Embora a atualização do site atualiza as imagens de arranque predefinidas, não pode atualizar estes ficheiros de suporte de dados ou dispositivos utilizados externamente em relação ao Configuration Manager  
-   Planeie a atualização de imagens de arranque não predefinidas quando não precisa da versão original (mais antiga) do Windows PE.  

**Ações que afetam configurações e definições**   
Quando um site é atualizado para o System Center Configuration Manager, algumas configurações e definições não são mantidas após a atualização ou são definidas para uma nova configuração predefinida. A tabela seguinte inclui as definições que não são mantidas ou que são alteradas, bem como informações que o ajudam a efetuar o planeamento das mesmas durante a atualização de sites:  

-   **Centro de Software:**  
    Os seguintes itens do Centro de Software são repostos nos valores predefinidos:  
    -   A opção**Informação de trabalho** é reposta para um horário de expediente das **5h00** às **22h00** Monday às Friday.  
    -   O valor de **Manutenção do computador** é definido como **Suspender as atividades do Centro de Software quando o computador estiver em modo de apresentação**.  
    -   O valor de **Controlo remoto** é definido com o valor existente nas definições de cliente que foram atribuídas ao computador.  
-   **Agendamentos de resumo de atualização de software:**  
     Os agendamentos de resumo personalizados para atualizações de software ou grupos de atualizações de software são repostos no valor predefinido de 1 hora. Após a conclusão da atualização, reponha os valores de resumo personalizados na frequência pretendida.  

##  <a name="bkmk_test"></a> Testar a atualização da base de dados do site  
As seguintes informações aplicam-se apenas quando estiver a atualizar uma versão anterior, como o System Center 2012 Configuration Manager para o System Center Configuration Manager.

Antes de atualizar um site, teste uma cópia da base de dados desse site para a atualização.  

Para testar a base de dados para uma atualização, restaure primeiro uma cópia da base de dados do site para uma instância do SQL Server que não aloje um site do Configuration Manager. A versão do SQL Server que utiliza para alojar a cópia da base de dados tem de ser uma versão do SQL Server que suporta a origem da cópia da base de dados que é a versão do Configuration Manager.  

Em seguida, depois de restaurar a base de dados do site, no computador do SQL Server, execute a configuração do Configuration Manager da pasta de suporte de dados de origem para o System Center Configuration Manager com o **/testdbupgrade.** opção da linha de comandos.  

-   Para obter informações sobre como criar e restaurar uma cópia de segurança da base de dados do site, veja [Opções da linha de comandos para Configuração](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  
-   Para obter informações sobre a opção da linha de comandos **/TESTDBUPGRADE**, veja a tabela da secção [Opções da linha de comandos para Configuração](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  
-   Para obter informações sobre as versões suportadas do SQL Server, veja o tópico [Suporte para versões do SQL Server para o System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

> [!TIP]  
>  Se integrar o Microsoft Intune com o Configuration Manager:  
>   
>  Quando executa um teste de atualização da base de dados numa cópia da base de dados do site com 5 ou mais dias, poderá receber uma das seguintes mensagens:  
>   
>  -   AVISO: Atualização irá forçar a sincronização completa com a nuvem.  
>  -   ERRO: Atualização de base de dados irá forçar a sincronização completa com a nuvem.  
>   
> Ambos podem ser ignoradas durante o teste de uma atualização de base de dados que não indicam uma falha ou um problema com o teste da atualização. Em vez disso, indicam que, durante a atualização real, dados a partir de **nuvem** grupo de replicação de base de dados poderão ser sincronizados com o Microsoft Intune.  

Utilize o seguinte procedimento em cada site de administração central e site primário que pretenda atualizar.  

#### <a name="to-test-a-site-database-for-upgrade"></a>Para testar uma base de dados do site para atualização  

1.  Faça uma cópia da base de dados do site e, em seguida, restaure-a para uma instância do SQL Server que utilize a mesma edição que a base de dados do site e que não aloje um site do Configuration Manager. Por exemplo, se a base de dados do site for executada numa instância da edição Enterprise do SQL Server, certifique-se de que restaura a base de dados para uma instância do SQL Server que também execute a edição Enterprise do SQL Server.  

2.  Depois de restaurar a cópia da base de dados, execute a configuração do suporte de dados de origem para o System Center Configuration Manager. Ao executar a Configuração, utilize a opção da linha de comandos **/TESTDBUPGRADE** . Se a instância do SQL Server que aloja a cópia da base de dados não for a instância predefinida, terá de fornecer também os argumentos da linha de comandos para identificar a instância que aloja a cópia da base de dados do site.  

     Por exemplo, planeia atualizar uma base de dados do site denominada SMS_ABC. Restaura uma cópia desta base de dados do site para uma instância suportada do SQL Server com o nome de instância DBTest. Para testar uma atualização desta cópia da base de dados do site, use a seguinte linha de comandos: **Setup.exe /testdbupgrade. DBtest\CM_ABC**  

     Pode encontrar o Setup.exe na seguinte localização no suporte de dados de origem para o System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

3.  Na instância do SQL Server em que executou o teste da atualização da base de dados, monitorize o progresso e êxito do ficheiro ConfigMgrSetup.log, na raiz da unidade do sistema:  

    -   Se o teste da atualização falhar, resolva eventuais problemas relacionados com a falha da atualização da base de dados do site, crie uma nova cópia de segurança da base de dados do site e teste a atualização da nova cópia da base de dados do site.  
    -   Após a conclusão do processo com êxito, poderá eliminar a cópia da base de dados.  

        > [!NOTE]  
        >  O restauro da cópia da base de dados do site utilizada para o teste da atualização não é suportado para utilização como base de dados de qualquer site.  

Depois de atualizar com êxito uma cópia da base de dados do site, prossiga com a atualização do site do Configuration Manager e a respetiva base de dados do site.  

##  <a name="bkmk_upgrade"></a> Atualizar sites  
Depois de concluir as configurações de pré-atualização para o seu site, testar a atualização da base de dados do site numa cópia da base de dados e transferir ficheiros de pré-requisitos e pacotes de idiomas da versão do service pack que planeia instalar, estará pronto atualizar o seu site do Configuration Manager.  

Ao atualizar um site numa hierarquia, deverá atualizar primeiro o site de nível superior da hierarquia. Este site de nível superior é um site de administração central ou um site primário autónomo. Após a conclusão da atualização de um site de administração central, será possível atualizar os sites primários subordinados pela ordem que entender. Depois de atualizar um site primário, pode atualizar os sites secundários subordinados desse site ou atualizar sites primários adicionais antes de atualizar quaisquer sites secundários.  

Para atualizar um site de administração central ou site primário, executar a configuração do suporte de dados de origem do System Center Configuration Manager. No entanto, não deverá executar o Programa de Configuração para atualizar sites secundários. Em alternativa, utilize a consola do Configuration Manager para atualizar um site secundário após concluir a atualização do respetivo site primário principal.  

Antes de atualizar um site, feche a consola do Configuration Manager que está instalada no servidor de site até que a atualização do site esteja concluída. Além disso, feche cada consola do Configuration Manager que é executada em computadores que não seja o servidor do site. Poderá voltar a ligar a consola após a conclusão da atualização do site. No entanto, enquanto não atualizar uma consola do Configuration Manager para a nova versão do Configuration Manager, essa consola não é possível apresentar alguns objetos e informações que estão disponíveis na nova versão do Configuration Manager.  

Utilize os procedimentos seguintes para atualizar sites do Configuration Manager:  

#### <a name="to-upgrade-a-central-administration-site-or-primary-site"></a>Para atualizar um site de administração central ou site primário  

1.  Certifique-se de que o utilizador que executa o Programa de Configuração possui os seguintes direitos de segurança:  

    -   Direitos de Administrador Local no computador do servidor de site.  
    -   Direitos de Administrador Local no servidor da base de dados do site remoto, se for remoto.    </br></br>

2.  No computador do servidor do site, abra o Explorador do Windows e navegue para  **&lt;ConfigMgSourceMedia\>\SMSSETUP\BIN\X64**.  

3.  Faça duplo clique em **Setup.exe**. É aberto o Assistente de configuração do Configuration Manager.  

4.  Na página **Antes de Começar** , clique em **Seguinte**.  

5.  Na página **Introdução** , selecione **Atualizar este site do Configuration Manager**e clique em **Seguinte**.  

6.  Na página **Chave de Produto** , clique em **Seguinte**.  

     Se instalou anteriormente a avaliação do Configuration Manager, pode selecionar **instalar a edição licenciada deste produto**e, em seguida, introduza a chave de produto para a instalação completa do Configuration Manager para converter o site para a versão completa.  

     Começando com a versão de Outubro de 2016 do suporte de dados de linha de base do versão 1606 para o System Center Configuration Manager, pode especificar a data de expiração do seu contrato de Software Assurance. Também tem a opção de especificar o **data de expiração do Software Assurance** do seu contrato de licenciamento em como um lembrete para si conveniente dessa data. Se não introduzir este durante a configuração, pode especificá-la mais tarde a partir da consola do Configuration Manager.

     >  [!NOTE]   
     >  Microsoft não valida a data de expiração introduzido e não utilize esta data para validação da licença.  Em vez disso, pode utilizá-lo como um lembrete da sua data de expiração. Isto é útil porque o Configuration Manager periodicamente verifica a existência de novas atualizações de software disponibilizadas online e o estado de licença do software assurance deve ser atual para serem elegíveis para utilizar estas atualizações adicionais.    

     Para obter mais informações, consulte [licenciamento e ramos para o System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

7.  Na página **Termos de Licenciamento para Software Microsoft** , leia e aceite os termos de licenciamento e clique em **Seguinte**.  

8.  Na página **Licenças de Pré-requisitos** , leia e aceite os termos de licenciamento do software de pré-requisito e clique em **Seguinte**. O programa de configuração transfere e instala automaticamente o software em sistemas de sites ou clientes, quando necessário. Tem de selecionar todas as caixas de verificação para avançar para a página seguinte.  

9. Na página **Transferências de Pré-requisitos** , especifique se a Configuração deverá transferir os ficheiros redistribuíveis de pré-requisitos, pacotes de idiomas e atualizações de produto mais recentes a partir da Internet ou utilizar ficheiros transferidos anteriormente, e clique em **Seguinte**. Se tiver transferido anteriormente os ficheiros através do Dispositivo de Transferência da Configuração, selecione **Utilizar ficheiros anteriormente transferidos** e especifique a pasta para transferência. Para obter mais informações, consulte [dispositivo de transferência da configuração](/sccm/core/servers/deploy/install/setup-downloader).

    > [!NOTE]  
    >  Quando utilizar ficheiros transferidos anteriormente, verifique se o caminho para a pasta de transferência contém a versão mais recente dos ficheiros.  

10. Na página **Seleção do Idioma do Servidor** , veja a lista de idiomas atualmente instalados para o site. Selecione idiomas adicionais disponíveis neste site para a consola do Configuration Manager e para relatórios ou desmarque os idiomas que já não é necessário suportar no site e, em seguida, clique em **seguinte**. Por predefinição, está seleccionado o inglês e não pode ser removido.  

    > [!IMPORTANT]  
    >  Cada versão do Configuration Manager não é possível utilizar pacotes de idiomas de uma versão anterior do Configuration Manager. Para ativar o suporte para um idioma num site do Configuration Manager que atualizar, tem de utilizar a versão do pacote de idiomas dessa nova versão. Para o exemplo, durante a atualização do System Center 2012 Configuration Manager para System Center Configuration Manager, se a versão do System Center Configuration Manager de um pacote de idiomas não está disponível com os ficheiros de pré-requisitos que transferir, suporte para esse idioma não pode ser instalado.  

11. Na página **Seleção do Idioma do Cliente** , veja a lista de idiomas atualmente instalados para o site. Selecione idiomas adicionais disponíveis neste site para computadores cliente ou desmarque os idiomas que já não seja necessário suportar no site. Especifique se pretende ativar todos os idiomas de cliente para clientes de dispositivos móveis e clique em **Seguinte**. Por predefinição, está seleccionado o inglês e não pode ser removido.  

    > [!IMPORTANT]  
    >  Cada versão do Configuration Manager não é possível utilizar pacotes de idiomas de uma versão anterior do Configuration Manager. Para ativar o suporte para um idioma num site do Configuration Manager que atualizar, tem de utilizar a versão do pacote de idiomas dessa nova versão. Para o exemplo, durante a atualização do System Center 2012 Configuration Manager para System Center Configuration Manager, se a versão do System Center Configuration Manager de um pacote de idiomas não está disponível com os ficheiros de pré-requisitos que transferir, suporte para esse idioma não pode ser instalado.  

12. Na página **Resumo de Definições** , clique em **Seguinte** para iniciar o Verificador de Pré-requisitos para verificar a prontidão do servidor para a atualização do site.  

13. Se não forem listados problemas na página **Verificação da Instalação de Pré-requisitos** , clique em **Seguinte** para atualizar o site e as funções do sistema de sites. Quando o Verificador de Pré-requisitos detetar um problema, clique num item da lista para obter detalhes sobre como resolver o problema. Antes de continuar a Configuração, resolva todos os itens da lista com estado de **Erro** . Depois de resolver o problema, clique em **Executar Verificação** para reiniciar a verificação de pré-requisitos. Pode também abrir o ficheiro ConfigMgrPrereq.log na raiz da unidade do sistema para rever os resultados do Verificador de Pré-requisitos. O ficheiro de registo pode conter informações adicionais que não são apresentadas na interface de utilizador. Para obter uma lista de regras de pré-requisitos de instalação e as descrições, consulte [verificador](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

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

A atualização do site secundário continuará em segundo plano. Após a conclusão da atualização, pode confirmar o estado na consola do Configuration Manager. Para confirmar o estado, selecione o servidor do site secundário e, no separador **Home Page** , no grupo **Site** , clique em **Mostrar Estado da Instalação**.  

##  <a name="BKMK_PostUpgrade"></a> Efetuar tarefas pós-atualização  
Após atualizar um site para um novo Service Pack, poderá ter de executar tarefas adicionais para concluir a atualização ou reconfigurar o site. Estas tarefas podem incluir a atualização de clientes do Configuration Manager ou de consolas do Configuration Manager, voltando a reativar réplicas de base de dados para pontos de gestão ou o restauro de definições para a funcionalidade do Configuration Manager que utilize e que não sejam mantidas após a atualização do pacote de serviço.  

**Problemas conhecidos para sites secundários:**  
- **Ao atualizar a versão 1511:** Para garantir que os clientes em sites secundários pode localizar o ponto de gestão do site secundário (ponto de gestão do proxy), adicione manualmente o ponto de gestão para grupos de limites que incluam também os pontos de distribuição no site secundário.  

- **Ao atualizar a versão 1606 ou posterior:** Pontos de gestão do proxy são automaticamente adicionados a grupos de limites que incluam pontos de distribuição no site secundário.

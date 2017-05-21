---
title: "Assistente de configuração | Documentos do Microsoft"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f809c9327db9f298168674add2d09820fdecd1b8
ms.openlocfilehash: 14b4172ad713a3981b8a5abe182405e271d78c26
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="use-the-setup-wizard-to-install-system-center-configuration-manager-sites"></a>Utilize o Assistente de configuração para instalar sites do Configuration Manager do System Center

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Para instalar um novo site do System Center Configuration Manager utilizando uma interface de utilizador assistidas, utilize o Assistente de configuração do Configuration Manager (setup.exe). O assistente suporta a instalação de um site primário ou site de administração central. Também é utilizar o Assistente para [atualizar uma instalação de avaliação](../../../../core/servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install.md) do Configuration Manager para uma instalação completamente licenciada. Quando não pretender utilizar o assistente, em vez disso, pode utilizar um [script de instalação](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md) e executa uma instalação autónoma da linha de comandos.

Para instalar um site secundário, tem de instalar o site a partir da consola do Configuration Manager. Os sites secundários não suportam uma instalação com script de linha de comandos.

## <a name="bkmk_primary"></a>Instalar um site de administração central ou site primário
Utilize o procedimento seguinte para instalar um site de administração central ou um site primário ou para atualizar um site de avaliação para um site do Configuration Manager completamente licenciada.   

Antes de iniciar a instalação do site, estar familiarizado com os detalhes nos seguintes artigos:
 -  [Preparar a instalação de sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md)
 -  [Pré-requisitos de instalação de sites](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md)

Se estiver a instalar um site de administração central como parte de um cenário de expansão do site, reveja o [expandir um site primário autónomo](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) secção deste tópico antes de utilizar o procedimento seguinte.

### <a name="bkmk_installpri"></a>Para instalar um site primário ou de administração central

1.  No computador onde pretende instalar o site, execute  **&lt;InstallationMedia\>\SMSSETUP\BIN\X64\Setup.exe** para iniciar o **Assistente de configuração do System Center Configuration Manager**.  

    > [!NOTE]  
    > Quando instalar um site de administração central para expandir um site primário autónomo ou a instalar um novo site primário subordinado numa hierarquia existente, tem de utilizar o suporte de instalação (ficheiros de origem) que corresponde à versão do site existente ou sites. Se instalou as atualizações na consola que alteraram a versão dos sites anteriormente instalados, não utilize o suporte de dados de instalação original. Em alternativa, utilize ficheiros de origem a partir de [CD. Pasta mais recente](../../../../core/servers/manage/the-cd.latest-folder.md) de um site atualizado. O Configuration Manager requer a utilização de ficheiros de origem que corresponde à versão do site existente que o novo site serão ligados.  

2.  No **antes de começar** página, selecione **seguinte**.  

3.  No **introdução** página, selecione o tipo de site que pretende instalar:  

    -   **Site de administração central**, como o primeiro site numa nova hierarquia ou ao expandir um site primário autónomo:  

        Selecione **instalar um site de administração central do Configuration Manager**.  

         Durante o passo posterior deste procedimento, é-lhe oferecida a opção para instalar um site de administração central como o primeiro site numa nova hierarquia ou para instalar um site de administração central para expandir um site primário autónomo.  

    -    **Site primário**, como um site primário autónomo que é o primeiro site numa nova hierarquia ou um site primário subordinado:  

        Selecione **instalar um site primário do Configuration Manager**.  

        > [!TIP]  
        > Normalmente, pode selecionar apenas a opção **utilizar opções de instalação típicas para um site primário autónomo** quando pretende instalar um site primário autónomo num ambiente de teste. Quando seleciona esta opção, a configuração:  

        > -   Configura automaticamente o site como um site primário autónomo.  
        > -   Utiliza um caminho de instalação predefinido.  
        > -   Utiliza uma instalação local da instância predefinida do SQL Server para a base de dados do site.  
        > -   Instala um ponto de gestão e um ponto de distribuição no computador do servidor do site.  
        > -   Configura o site com o inglês e o idioma de apresentação do sistema operativo no servidor do site primário se corresponde a um dos idiomas que o Configuration Manager suporta.  

4.  No **chave de produto** página:
    - Escolha se pretende instalar o Configuration Manager como uma edição de avaliação ou uma edição licenciada.  

      -   Se selecionar uma edição licenciada, introduza a sua chave de produto e escolha **seguinte**.  

      -   Se selecionar uma edição de avaliação, selecionar **seguinte**. (Pode atualizar uma instalação de avaliação para uma instalação completa mais tarde.)  
    - Iniciar com o lançamento de 2016 de Outubro de suportes de dados de linha de base de 1606 de versão para o System Center Configuration Manager, pode especificar a data de expiração do seu contrato do Software Assurance de. Nesta página, tem a opção para especificar o **data de expiração de Software Assurance** do seu contrato de licenciamento, como um lembrete para si conveniente dessa data. Se não introduzir esta durante a configuração, pode especificar mais tarde a partir da consola do Configuration Manager.

      > [!NOTE]   
      > Microsoft não valida a data de expiração que introduziu e não irá utilizar esta data para a validação de licença. Em vez disso, pode utilizá-lo como um lembrete da data de validade. Isto é útil porque o Configuration Manager verifica periodicamente a existência de novas atualizações de software oferecidas online — e o estado da licença de software assurance deve ser atual, de modo a que é elegível para utilizar estas atualizações adicionais.    

      Para obter mais informações, consulte o artigo [licenciamento e ramos para o System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

5.  No **termos de licenciamento de Software Microsoft** página, leia e aceite os termos de licenciamento.  

6.  No **licenças de pré-requisito** página, leia e aceite os termos de licenciamento para o software de pré-requisito. A configuração transfere e instala automaticamente o software em sistemas de sites ou clientes quando é obrigatório. Todas as caixas tem de verificar antes de poder continuar para a página seguinte.  

7.  No **transferências de pré-requisitos** página, especifique se a configuração deverá transferir os ficheiros redistribuíveis de pré-requisitos a partir da Internet ou utilizar ficheiros anteriormente transferidos:  

    -   Se pretender que o programa de configuração para transferir os ficheiros neste momento, selecionar **transferir ficheiros necessários** e especifique uma localização para armazenar os ficheiros.  

    -   Se tiver transferido anteriormente os ficheiros utilizando [dispositivo de transferência da configuração](../../../../core/servers/deploy/install/setup-downloader.md), selecione **utilizar ficheiros anteriormente transferidos** e especifique a pasta de transferência.  

        > [!TIP]  
        > Se utilizar ficheiros transferidos anteriormente, certifique-se de que o caminho para a pasta de transferência contém a versão mais recente dos ficheiros.  

8.  No **seleção do idioma do servidor** página, selecione os idiomas que estão disponíveis para a consola do Configuration Manager e para relatórios. (O inglês está selecionado por predefinição e não pode ser removido.)  

9. No **seleção do idioma do cliente** página, selecione os idiomas que estão disponíveis para os computadores cliente e especifique se pretende ativar todos os idiomas de cliente para clientes de dispositivos móveis. (O inglês está selecionado por predefinição e não pode ser removido.)  

    > [!IMPORTANT]  
    > Quando utiliza um site de administração central, certifique-se de que os idiomas de cliente que é configurado no site de administração central incluem todos os idiomas de cliente configurados em cada site primário subordinado. Isto acontece porque os clientes que instale a partir de um ponto de distribuição têm acesso para os idiomas de cliente no site de nível superior, enquanto os clientes que instale a partir de um ponto de gestão têm acesso para os idiomas de cliente a partir do respetivo site primário atribuído.  

10. No **definições de instalação e Site** página, especifique as seguintes opções para o novo site que estiver a instalar:  

    -   **Código do site:** [Cada código de site numa hierarquia têm de ser exclusivo](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_sitecodes) e composto por três dígitos de alfanuméricos (À Z) e de 0 a 9. Como o código do site é utilizado em nomes de pastas, não utilize nomes reservados ao Windows para o site, incluindo:    
        -   AUX  
        -   CON    
        -   NUL    
        -   PRN    
        -   SMS  

        > [!NOTE]  
        > A configuração não verifica se o código do site que especificou já está a ser utilizado ou se tiver um nome reservado.  

    -   **Nome do site:** Cada site requer este nome amigável, que pode ajudar a identificar o site.  

    -   **Pasta de instalação:** Este é o caminho da pasta para a instalação do Configuration Manager. Não é possível alterar a localização após a instalação do site. Além disso, o caminho não pode conter carateres Unicode ou espaços à direita.  

11. No **instalação do Site** página, utilize a seguinte opção que corresponde ao seu cenário:  

    -   **Estou a instalar um site de administração central:**  

         No **instalação do Site de Administração Central** página, selecione **instalar como o primeiro site numa nova hierarquia**e, em seguida, escolha **seguinte** para continuar.  

    -   **Estou a expandir um primário autónomo para uma hierarquia com um site de administração central:**  

         No **instalação do Site de Administração Central** página, selecione **expandir um primário autónomo existente para uma hierarquia**, especifique o FQDN do servidor do site primário autónomo e, em seguida, selecione **seguinte** para continuar.  

         O suporte de dados que utilizar para instalar o novo site de administração central tem de corresponder à versão do site primário.  

    -   **Estou a instalar um site primário autónomo:**  

         No **instalação do Site primário** página, selecione **instalar o site primário como um site autónomo**e, em seguida, escolha **seguinte**.  

    -   **Estou a instalar um site primário subordinado:**  

         No **instalação do Site primário** página, selecione **associar o site primário para uma hierarquia existente**, especifique o FQDN para o site de administração central e, em seguida, selecione **seguinte**.  

12. No **informações da base de dados** página, especifique as seguintes informações:  

    -   **Nome do SQL Server (FQDN):** Por predefinição, está definida para o computador de servidor do site.  

    -   **Nome da instância:** Por predefinição, este está em branco. Utiliza a instância predefinida do SQL Server no computador do servidor de site.  

    -   **Nome da base de dados:** Por predefinição, está definida como CM_&lt;Sitecode\>. Está livre utilizar um nome diferente que especificar.  

    -   **A porta do Service Broker:** Por predefinição, está definida como utilizar a porta do SQL Server Service Broker (SSB) predefinida de 4022. SQL Server utiliza-o para comunicar diretamente com a base de dados noutros sites.  

13. Na segunda **informações da base de dados** página, pode especificar localizações de não predefinido para o ficheiro de dados do SQL Server e o ficheiro de registo do SQL Server para a base de dados do site:  

    -   Localizações de ficheiro predefinido para o SQL Server são fornecidas.  

    -   A opção para especificar localizações de ficheiros não predefinido não está disponível quando utiliza um cluster do SQL Server.  

    -   O Verificador de pré-requisitos não executa uma verificação de espaço livre em disco para não predefinido localizações de ficheiros.  

14. No **definições do fornecedor de SMS** página, especifique o FQDN para o servidor onde pretende instalar o fornecedor de SMS.  

    -   Por predefinição, o servidor de site é especificado.  

    -   Após a instalação do site, pode configurar fornecedores de SMS adicionais.  

15. No **definições de comunicação de cliente** página, escolha se pretende configurar todos os sistemas de sites para aceitar apenas comunicações HTTPS de clientes ou o método de comunicação seja configurado para cada função do sistema de sites.  

    Quando seleciona **todas as funções de sistema de sites apenas aceitam comunicações HTTPS de clientes**, o computador cliente tem de ter um certificado PKI válido para autenticação de cliente. Para mais informações sobre os requisitos dos certificados PKI, consulte o artigo [requisitos de certificados PKI para o Configuration Manager](https://technet.microsoft.com/library/gg699362.aspx).  

    > [!NOTE]  
    > Este passo só se aplica quando instala um site primário. Se estiver a instalar um site de administração central, ignore este passo.  

16. No **funções do sistema de sites** página, selecione se pretende instalar um ponto de gestão ou um ponto de distribuição. Para cada função que opta por ter instalada pelo programa de configuração:  

    -   Tem de introduzir o **FQDN** para o computador que irá alojar a função e escolha o cliente do método de ligação que o servidor irá suportar (HTTP ou HTTPS).  

    -   Se tiver selecionado **todas as funções de sistema de sites apenas aceitam comunicações HTTPS de clientes** na página anterior, as definições de ligação de cliente são automaticamente configuradas para HTTPS e não podem ser alteradas a menos que Retroceda e altere a definição.  

    > [!NOTE]  
    > Este passo só se aplica quando instala um site primário. Se estiver a instalar um site de administração central, ignore este passo.  

    > [!NOTE]  
    > Para instalar funções do sistema de sites, a configuração utiliza o **conta de instalação do sistema de sites**. Por predefinição, esta opção utiliza conta de computador do site primário. Esta conta tem de ser um administrador local no computador remoto para instalar a função de sistema de sites. Se esta conta não possui as permissões necessárias, desmarque as funções de sistema de sites e instalá-las mais tarde a partir da consola do Configuration Manager, depois de configurar contas adicionais a utilizar como contas de instalação do sistema de sites.  

17. No **dados de utilização** página, reveja as informações sobre os dados que a Microsoft recolhe e, em seguida, selecione **seguinte**.  

18. O **programa de configuração de ponto de ligação de serviço** página apenas está disponível durante a configuração:  

    -   Quando estiver a instalar um site primário autónomo.  

    -   Quando estiver a instalar um site de administração central.  

    > [!NOTE]  
    > Se estiver a instalar um site primário subordinado, ignore este passo (esta página não está disponível).  

     Se estiver a instalar um site de administração central como parte de um cenário de expansão do site e esta função já está instalada no site primário autónomo, tem de desinstalar esta função do site primário autónomo. Apenas uma instância desta função é permitida numa hierarquia — e apenas é permitida no site de nível superior da hierarquia.  

     Depois de selecionar uma configuração para o **ponto de ligação de serviço**, escolha **seguinte**. (Após a conclusão da configuração, pode alterar esta configuração a partir da consola do Configuration Manager).  

19. No **resumo das definições de** página, reveja as definições que selecionou. Quando estiver pronto, escolher **seguinte** para iniciar o Verificador de pré-requisitos.  

20. No **a verificação dos pré-requisitos de instalação** estão listados na página quaisquer problemas que podem ser identificados.  

    -   Quando o Verificador de pré-requisitos detetar um problema, escolha um item na lista para obter detalhes sobre como resolver o problema.  

    -   Tem de resolver cada item com o estado de **falhou** antes de continuar para instalar o site. Itens com o estado de **aviso** deve ser resolvido, mas não bloqueiam a instalação do site.  

    -   Depois de resolver problemas, escolha **executar verificação** voltar a executar o Verificador de pré-requisitos.  

     Quando o Verificador de pré-requisitos é executada e não verifica recebe um **falhada** Estado, pode escolher **começar a instalar** para iniciar a instalação de site.  

    > [!TIP]  
    > Para além do feedback que é fornecido no assistente, pode encontrar informações adicionais sobre problemas de pré-requisitos quando visualiza o **Configmgrprereq** ficheiro na raiz da unidade de sistema do computador onde está a instalar. Para obter uma lista de regras de pré-requisitos de instalação e as descrições, consulte o artigo [lista das verificações de pré-requisitos para o System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

21. No **instalação** página, o programa de configuração apresenta o estado da instalação. Quando a instalação de servidor do site principal estiver concluída, terá a opção de **fechar** o Assistente de instalação. Ao fechar o assistente, a instalação e configurações de site inicial continuam em segundo plano.  

    -   Pode ligar uma consola do Configuration Manager para o site antes da configuração está concluída. Esta consola é ligada como só de leitura e permite-lhe ver objetos e definições, mas não é possível introduzir edições.  

    -   Após a conclusão da configuração, poderá ligar uma consola que pode editar os objetos e definições.  


## <a name="bkmk_expand"></a>Expandir um site primário autónomo
Se tiver instalado um site primário autónomo como primeiro site, terá a opção mais tarde para expandir o site para uma hierarquia maior instalando um site de administração central.   

Quando expande um site primário autónomo, é instalar um novo site de administração central, que utiliza a base de dados do site primário autónomo existente como uma referência. Após instala o novo site de administração central, o site primário autónomo é funciona como um site primário subordinado.

-   Apenas um site primário autónomo pode ser expandido para uma nova hierarquia.  

-   Apenas um site primário autónomo pode ser expandido para uma hierarquia específica. Não é possível utilizar esta opção para associar os sites primários autónomos adicionais para a mesma hierarquia. Em vez disso, utilize a migração para migrar dados a partir de uma hierarquia para outra.  

-   Depois de expandir um site autónomo numa hierarquia com um site de administração central, pode adicionar sites primários subordinados de subordinados adicionais.  

-   Para remover um site primário a partir de uma hierarquia com um site de administração central, terá de desinstalar o site primário.  

Para expandir o site, pode utilizar o Assistente de configuração do System Center Configuration Manager para instalar um novo site de administração central com as seguintes advertências:  

-   Tem de instalar o site de administração central utilizando a mesma versão do Configuration Manager como o site primário autónomo.  

-   No **introdução** página no Assistente de configuração, selecionar a opção para instalar um site de administração central. Uma fase posterior da configuração, irá escolher uma opção para expandir um site primário autónomo existente.  

-   Quando configura o **seleção do idioma do cliente** página para o novo site de administração central, tem de selecionar os mesmos idiomas de cliente que estão configurados para o site primário autónomo que está a expandir.  

-   No **instalação do Site** página, selecionar a opção para expandir o site primário autónomo.  

Para expandir um site primário autónomo, consulte o [pré-requisitos para expandir um site](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand)e, em seguida, utilize o procedimento  *[para instalar um site primário ou de administração central](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_installpri)*, anteriormente neste artigo.


## <a name="bkmk_secondary"></a>Instalar um site secundário
 Utilize a consola do Configuration Manager para instalar um site secundário.  

-   Se não estiver ligada a consola utilizada para o site primário que será o site principal para o novo site secundário, o comando para instalar o site irá ser replicado para o site primário correto.  

-   Antes de iniciar a instalação do site, certifique-se de que a conta de utilizador tem as permissões de pré-requisitos e, se o computador que alojará o novo site secundário cumpre todos os pré-requisitos para utilização como um servidor de site secundário.  

-   Quando instala o site secundário, o Configuration Manager configura o novo site para utilizar as portas de comunicação de cliente que estão configuradas no site primário principal.  

### <a name="bkmk_installsecondary"></a>Para instalar um site secundário  


1.  Na consola do Configuration Manager, navegue para **administração** > **configuração do Site** > **Sites**. Selecione o site que será o site primário principal do novo site secundário.  

2.  Escolher **Criar Site secundário** para iniciar o **Assistente para criar sites secundários**.  

3.  No **antes de começar** página, confirme se o site primário que se encontra listado é o site que pretende ser o elemento principal do novo site secundário. Em seguida, escolha **seguinte**.  

4.  No **geral** página, especifique o seguinte:  

    -   **Código do site**: Cada código de site numa hierarquia tem de ser exclusivo e composto por três dígitos de alfanuméricos (À Z) e de 0 a 9. Como o código do site é utilizado em nomes de pastas, não utilize nomes reservados ao Windows para o site, incluindo:  

        -   AUX    
        -   CON    
        -   NUL    
        -   PRN  
        -   SMS  

       > [!NOTE]  
       > A configuração não verifica se o código do site que especificou já está a ser utilizado ou se é um nome reservado.  

    -   **Nome do servidor de site**: Este é o FQDN do servidor onde instalar o novo site secundário.  

    -   **Nome do site**: Cada site requer este nome amigável, que pode ajudar a identificar o site.  

    -   **Pasta de instalação**: Este é o caminho da pasta para a instalação do Configuration Manager. Não é possível alterar a localização após a instalação do site. O caminho não pode conter carateres Unicode ou espaços à direita.  

    > [!IMPORTANT]  
    > Depois de especificar os detalhes desta página, pode escolher **resumo** para utilizar as predefinições para o resto das opções de site secundário e, para ir diretamente para o **resumo** página do assistente.  

    > -   Utilize esta opção apenas quando estiver familiarizado com as predefinições neste assistente e são as definições que pretende utilizar.  
    > -   Grupos de limites não estão associados com o ponto de distribuição quando utiliza as predefinições. Por conseguinte, até configurar grupos de limites que incluem o servidor de site secundário, os clientes não irão utilizar o ponto de distribuição que está instalado neste site secundário como localização de origem de conteúdo.  

5.  No **ficheiros de origem de instalação** página, selecione a forma como o computador do site secundário obtém ficheiros de origem para instalar o site.  

     Quando utilizar ficheiros de origem que são armazenados na rede ou armazenados no computador do site secundário:  

    -   A localização do ficheiro de origem tem de incluir uma pasta denominada **Redist** que inclui todos os ficheiros que foram anteriormente transferidos utilizando o dispositivo de transferência da configuração.  

    -   Se nenhum dos ficheiros a partir de **Redist** não estão disponíveis, a configuração irá falhar ao instalar o site secundário.  

    -   A conta de computador do computador do site secundário tem de ter **leitura** permissões para a origem de pasta e a partilha de ficheiros.  

6.  No **definições do SQL Server** página, especifique a versão do SQL Server para utilizar e, em seguida, configure as definições relacionadas.  

    > [!NOTE]  
    > Programa de configuração não valida as informações introduzidas nesta página antes de iniciar a instalação. Antes de continuar, verifique estas definições.  

     **Instalar e configurar uma cópia local do SQL Server Express no computador do site secundário**  

    -   **Porta de serviço do SQL Server**: Especifique a porta do serviço do SQL Server para o SQL Server Express deverá utilizar. A porta de serviço normalmente é configurada para utilizar a porta TCP 1433, mas pode configurar outra porta.  

    -   **Porta do SQL Server Broker**: Especifique a porta do SQL Server Service Broker (SSB) do SQL Server Express deverá utilizar. O Mediador de serviço normalmente é configurado para utilizar a porta TCP 4022, mas pode configurar uma porta diferente. Tem de especificar uma porta válida que nenhum outro site ou serviço está a utilizar e que estão a bloquear o sem restrições de firewall.  

    > [!IMPORTANT]  
    > Quando Configuration Manager instala o SQL Server Express, instala o SQL Server Express 2012 sem nenhum service pack:  

    > -   Para o site secundário serão suportadas, depois de instalar, tem de atualizar o SQL Server Express 2012 para [uma versão suportada](/sccm/core/plan-design/configs/support-for-sql-server-versions#bkmk_SQLVersions).
    > -   Além disso, se a nova instalação do site secundário não for concluída, mas primeiro conclui a instalação do SQL Server Express 2012, tem de atualizar essa instância do SQL Server Express antes do Configuration Manager com êxito pode tentar novamente a instalação do site secundário.  

     **Utilizar uma instância existente do SQL Server**  

    -   **FQDN do SQL Server**: Reveja o FQDN para o computador executar o SQL Server. Tem de utilizar um servidor local com o SQL Server para alojar a base de dados do site secundário e não é possível modificar esta definição.  

    -   **Instância do SQL Server**: Especifique a instância do SQL Server para utilizar como a base de dados do site secundário. Esta opção deixe em branco para utilizar a instância predefinida.  

    -   **Nome de base de dados do site do ConfigMgr**: Especifique o nome a utilizar para a base de dados do site secundário.  

    -   **Porta do SQL Server Broker**: Especifique a porta do SQL Server Service Broker (SSB) do SQL Server a utilizar. Tem de especificar uma porta válida que nenhum outro site ou serviço está a utilizar e que não existem restrições de firewall bloquear.  

    > [!TIP]  
    > Consulte o artigo [versões suportadas do SQL Server](../../../../core/plan-design/configs/support-for-sql-server-versions.md) para obter uma lista das versões do SQL Server que suporta o System Center Configuration Manager.  

7.  No **ponto de distribuição** página, configure definições para o ponto de distribuição que irá ser instalado num servidor do site secundário.  

     **Definições necessárias:**  

    -   **Especifique a forma como os dispositivos cliente comunicam com o ponto de distribuição**: Escolha entre HTTP e HTTPS.  

    -   **Criar um certificado autoassinado ou importar um certificado de cliente PKI**: Escolha entre utilizar um certificado autoassinado (o que permite-lhe também permitir ligações anónimas dos clientes do Configuration Manager para a biblioteca de conteúdos) ou importar um certificado a partir do seu PKI.  

         O certificado é utilizado para autenticar o ponto de distribuição para um ponto de gestão antes do ponto de distribuição envia mensagens de estado.  

         Para obter informações sobre os requisitos de certificados, consulte o artigo [requisitos de certificados PKI para o Configuration Manager](https://technet.microsoft.com/library/gg699362.aspx).  

    **Definições opcionais:**  

    -   **Instalar e configurar o IIS se exigido pelo Configuration Manager**: Selecione esta definição para permitir que o Configuration Manager instalar e configurar serviços de informação Internet (IIS) no servidor, se ainda não esteja instalada. O IIS tem de ser instalado em todos os pontos de distribuição.  

        > [!NOTE]  
        > Embora esta definição é opcional, o IIS tem de ser instalado no servidor antes de um ponto de distribuição pode ser instalado com êxito.  

    -   **Ativar e configurar o BranchCache para este ponto de distribuição**.  

    -   **Descrição**. Esta é uma descrição amigável para o ponto de distribuição para o ajudar a reconhecê-lo.  

    -   **Ativar conteúdo pré-configurado para este ponto de distribuição**.  

8.  No **definições de unidade** página, especifique as definições de unidade para o ponto de distribuição do site secundário.  

     Pode configurar até duas unidades de disco para a biblioteca de conteúdos e duas unidades de disco para a partilha de pacote. No entanto, o Configuration Manager possa utilizar unidades adicionais quando as duas primeiras atingem a reserva do espaço na unidade configurada. O **definições de unidade** página é onde pode configura a prioridade para as unidades de disco e a quantidade de espaço livre em disco que deverá permanecer disponível em cada unidade de disco.  

    -   **Unidade (MB) de reserva do espaço**: O valor que configurar para esta definição determina a quantidade de espaço livre numa unidade antes do Configuration Manager escolher uma unidade diferente e continuar o processo de cópia para essa unidade. Ficheiros de conteúdo podem abranger várias unidades.  

    -   **Localizações de conteúdo**: Especifique as localizações de conteúdos para a partilha de biblioteca e do pacote de conteúdo. O Configuration Manager copia conteúdo para a localização de conteúdos primária até a quantidade de espaço livre atingir o valor especificado para **reserva de espaço na unidade (MB)**.

     Por predefinição, as localizações de conteúdo estão definidas como **automática**. A localização de conteúdo principal está definida para a unidade de disco que tem mais espaço de disco no momento da instalação. A localização secundária é definida para a unidade de disco que tenha mais disco espaço livre após a unidade principal. Quando as unidades principais e secundárias atingem a reserva do espaço na unidade, o Configuration Manager seleciona uma outra unidade disponível com mais disco espaço livre e continua o processo de cópia.  

9. No **a validação de conteúdo** página, especifique se pretende validar a integridade dos ficheiros de conteúdo no ponto de distribuição.  

    -   Quando ativa a validação de conteúdos com base numa agenda, Configuration Manager inicia o processo à hora agendada e todo o conteúdo no ponto de distribuição é verificado.  

    -   Também pode configurar o **prioridade da validação de conteúdo**.  

    -   Para ver os resultados do processo de validação de conteúdo, na consola do Configuration Manager, navegue para **monitorização** > **estado da distribuição** > **estado do conteúdo**. É apresentado o conteúdo de cada tipo de pacote (por exemplo, aplicação, pacote de atualização de Software e imagem de arranque).  

10. No **grupos de limites** página, gerir os grupos de limites que é atribuído este ponto de distribuição para:  

    -   Durante a implementação de conteúdos, os clientes tem de ser um grupo de limites que esteja associado com o ponto de distribuição a utilizar como localização de origem para o conteúdo.  

    -   Pode selecionar o **permitir a localização de origem de contingência para conteúdo** opção para permitir que os clientes fora destes grupos de limites recorram à contingência e utilizem o ponto de distribuição como localização de origem de conteúdo quando pontos de distribuição preferenciais não estejam disponíveis.  

     Para obter informações sobre pontos de distribuição preferenciais, consulte o [os conceitos fundamentais para gestão de conteúdo](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) tópico.  

11. No **resumo** página, verifique as definições e, em seguida, selecione **seguinte** para instalar o site secundário. Quando o assistente apresenta o **conclusão** página, pode fechar o assistente. A instalação do site secundário continuará em segundo plano.  


### <a name="bkmk_verify"></a>Para verificar o estado de instalação do site secundário  

1.  Na consola do Configuration Manager, navegue para **administração** > **configuração do Site** > **Sites**.  

2.  Selecione o servidor de site secundário que estiver a instalar e, em seguida, selecione **Mostrar estado da instalação**.  

    > [!TIP]  
    > Quando instala mais do que um site secundário cada vez, o Verificador de pré-requisitos é executada relativamente a um único site, uma vez e tem de concluir a um site antes de iniciar a verificação do site seguinte.  


---
title: "Assistente de configuração | Microsoft Docs"
ms.custom: na
ms.date: 7/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 678f1b35fe6f7649dacb766f7c671f4ec8ea1435
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="use-the-setup-wizard-to-install-system-center-configuration-manager-sites"></a>Utilize o Assistente de configuração para instalar sites do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Para instalar um novo site do System Center Configuration Manager, utilizando uma interface de utilizador orientada, utilize o Assistente de configuração do Configuration Manager (setup.exe). O assistente suporta a instalação de um site primário ou site de administração central. Também é utilizar o Assistente para [atualizar uma instalação de avaliação](../../../../core/servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install.md) do Configuration Manager para uma instalação totalmente licenciada. Quando não quiser utilizar o assistente, em vez disso, pode utilizar um [script de instalação](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md) e execute uma instalação autónoma de linha de comandos.

Para instalar um site secundário, tem de instalar o site a partir da consola do Configuration Manager. Os sites secundários não suportam uma instalação com script da linha de comandos.

## <a name="bkmk_primary"></a>Instalar um site de administração central ou site primário
Utilize o procedimento seguinte para instalar um site de administração central ou um site primário ou para atualizar um site de avaliação para um site totalmente licenciada do Configuration Manager.   

Antes de iniciar a instalação do site, deve estar familiarizado com os detalhes nos seguintes artigos:
 -  [Preparar a instalação de sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md)
 -  [Pré-requisitos para instalar sites](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md)

Se estiver a instalar um site de administração central como parte de um cenário de expansão do site, reveja o [expandir um site primário autónomo](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) secção deste tópico antes de utilizar o procedimento seguinte.

### <a name="bkmk_installpri"></a>Para instalar um site primário ou de administração central

1.  No computador onde pretende instalar o site, execute  **&lt;InstallationMedia\>\SMSSETUP\BIN\X64\Setup.exe** para iniciar o **Assistente de configuração do System Center Configuration Manager**.  

    > [!NOTE]  
    > Quando instalar um site de administração central para expandir num site primário autónomo ou instalar um novo site primário subordinado numa hierarquia existente, tem de utilizar o suporte de instalação (ficheiros de origem) que corresponde à versão do site existente ou sites. Se instalou atualizações na consola que alteraram a versão dos sites anteriormente instalados, não utilize o suporte de dados de instalação original. Em alternativa, utilize ficheiros de origem do [CD. Pasta mais recente](../../../../core/servers/manage/the-cd.latest-folder.md) de um site atualizado. O Configuration Manager requer a utilização de ficheiros de origem que corresponde à versão do site existente que o novo site irá ligar ao.  

2.  No **antes de começar** página, escolha **seguinte**.  

3.  No **introdução** página, selecione o tipo de site que pretende instalar:  

    -   **Site de administração central**, como o primeiro site numa nova hierarquia ou ao expandir um site primário autónomo:  

        Selecione **instalar um site de administração central do Configuration Manager**.  

         Durante o passo posterior deste procedimento, é-lhe dada a opção para instalar um site de administração central como o primeiro site numa nova hierarquia ou para instalar um site de administração central para expandir num site primário autónomo.  

    -    **Site primário**, como um site primário autónomo que é o primeiro site numa nova hierarquia, ou um subordinado principal:  

        Selecione **instalar um site primário do Configuration Manager**.  

        > [!TIP]  
        > Normalmente, apenas seleciona a opção **utilizar opções de instalação típicas para um site primário autónomo** quando pretende instalar um site primário autónomo num ambiente de teste. Quando seleciona esta opção, a configuração:  

        > -   Configura automaticamente o site como um site primário autónomo.  
        > -   Utiliza um caminho de instalação predefinido.  
        > -   Utiliza uma instalação local da instância predefinida do SQL Server para a base de dados do site.  
        > -   Instala um ponto de gestão e um ponto de distribuição no computador do servidor do site.  
        > -   Configura o site com inglês e o idioma de apresentação do sistema operativo no servidor do site primário se corresponder a um dos idiomas que suporte do Configuration Manager.  

4.  No **chave de produto** página:
    - Escolha se pretende instalar o Configuration Manager como uma edição de avaliação ou uma edição licenciada.  

      -   Se selecionar uma edição licenciada, introduza a chave de produto e escolha **seguinte**.  

      -   Se selecionar uma edição de avaliação, escolha **seguinte**. (Pode atualizar uma instalação de avaliação para uma instalação completa mais tarde.)  
    - Começando com a versão de Outubro de 2016 da versão 1606 da linha de base de dados para o System Center Configuration Manager, pode especificar a data de expiração do seu contrato de Software Assurance. Nesta página, tem a opção para especificar o **data de expiração do Software Assurance** do seu contrato de licenciamento em como um lembrete para si conveniente dessa data. Se não introduzir este durante a configuração, pode especificá-la mais tarde a partir da consola do Configuration Manager.

      > [!NOTE]   
      > Microsoft não a validar a data de expiração que introduziu e não as utilizaremos esta data para validação da licença. Em vez disso, pode utilizá-lo como um lembrete da sua data de expiração. Isto é útil porque o Configuration Manager verifica periodicamente para novas atualizações de software disponibilizadas online — e o estado de licença do software assurance deve ser atual, de modo a que está elegível para utilizar estas atualizações adicionais.    

      Para obter mais informações, consulte [licenciamento e ramos para o System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

5.  No **termos de licenciamento de Software Microsoft** página, leia e aceite os termos de licenciamento.  

6.  No **licenças de pré-requisito** página, leia e aceite os termos de licenciamento para software de pré-requisito. A configuração transfere e instala automaticamente o software em sistemas de sites ou clientes quando tem necessário. Tem de verificar todas as caixas de antes de poder continuar para a página seguinte.  

7.  No **as transferências de pré-requisitos** página, especifique se a configuração deverá transferir os ficheiros redistribuíveis de pré-requisitos a partir da Internet ou utilizar ficheiros anteriormente transferidos:  

    -   Se pretender que o programa de configuração para transferir os ficheiros neste momento, selecione **transferir ficheiros necessários** e especifique uma localização para armazenar os ficheiros.  

    -   Se tiver transferido anteriormente os ficheiros utilizando [dispositivo de transferência da configuração](../../../../core/servers/deploy/install/setup-downloader.md), selecione **utilizar ficheiros anteriormente transferidos** e especifique a pasta de transferência.  

        > [!TIP]  
        > Se utilizar ficheiros anteriormente transferidos, certifique-se de que o caminho para a pasta de transferência contém a versão mais recente dos ficheiros.  

8.  No **seleção de idioma do servidor** página, selecione os idiomas que estão disponíveis para a consola do Configuration Manager e para relatórios. (O inglês está selecionado por predefinição e não pode ser removido.)  

9. No **seleção de idioma do cliente** página, selecione os idiomas que estão disponíveis para os computadores cliente e especifique se pretende ativar todos os idiomas de cliente para clientes de dispositivos móveis. (O inglês está selecionado por predefinição e não pode ser removido.)  

    > [!IMPORTANT]  
    > Quando utiliza um site de administração central, certifique-se de que configurou no site de administração central de idiomas de cliente incluem todos os idiomas de cliente que configurou em cada site primário subordinado. Isto acontece porque os clientes que instale a partir de um ponto de distribuição têm acesso para os idiomas de cliente do site de nível superior, enquanto os clientes que instale a partir de um ponto de gestão tem acesso para os idiomas de cliente do respetivo site primário atribuído.  

10. No **definições de instalação e Site** página, especifique as seguintes opções para o novo site que estiver a instalar:  

    -   **Código do site:** [Cada código do site numa hierarquia têm de ser exclusivo](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_sitecodes) e composto por três dígitos alfanuméricos (da A z) e de 0 a 9. Uma vez que o código de site é utilizado em nomes de pastas, não utilize nomes reservados ao Windows para o site, incluindo:    
        -   AUX  
        -   CON    
        -   NUL    
        -   PRN    
        -   SMS  

        > [!NOTE]  
        > A configuração não verifica se o código do site que especificou já está a ser utilizado ou se tiver um nome reservado.  

    -   **Nome do site:** Cada site requer este nome amigável, que pode ajudar a identificar o site.  

    -   **Pasta de instalação:** Este é o caminho da pasta para a instalação do Configuration Manager. Não é possível alterar a localização após a instalação do site. Além disso, o caminho não pode conter carateres Unicode nem espaços à direita.  

11. No **instalação de Site** página, utilize a opção seguinte que corresponda ao seu cenário:  

    -   **Estou a instalar um site de administração central:**  

         No **instalação do Site de Administração Central** página, selecione **instalar como o primeiro site numa nova hierarquia**e, em seguida, escolha **seguinte** para continuar.  

    -   **Estou a expandir um site primário autónomo numa hierarquia com um site de administração central:**  

         No **instalação do Site de Administração Central** página, selecione **expandir um site primário autónomo existente numa hierarquia**, especifique o FQDN do servidor do site primário autónomo e, em seguida, escolha **seguinte** para continuar.  

         O suporte de dados que utilizar para instalar o novo site de administração central tem de corresponder à versão do site primário.  

    -   **Estou a instalar um site primário autónomo:**  

         No **instalação do Site primário** página, selecione **instalar o site primário como um site autónomo**e, em seguida, escolha **seguinte**.  

    -   **Estou a instalar um site primário subordinado:**  

         No **instalação do Site primário** página, selecione **associar o site primário para uma hierarquia existente**, especifique o FQDN para o site de administração central e, em seguida, escolha **seguinte**.  

12. No **informações da base de dados** página, especifique as seguintes informações:  

    -   **Nome do SQL Server (FQDN):** Por predefinição, está definida para ser o computador do servidor do site.

     Se utilizar uma porta personalizada, adicione essa porta para o FQDN do SQL Server. Para tal, siga o FQDN do servidor sequel com uma vírgula e, em seguida, o número de porta.   Por exemplo, para o servidor *SQLServer1.fabrikam.com*, utilize o seguinte procedimento para especificar a porta *1551*:  **SQLServer1.fabrikam.com, 1551**

    -   **Nome da instância:** Por predefinição, este está em branco. Utiliza a instância predefinida do SQL Server no computador do servidor do site.  

    -   **Nome da base de dados:** Por predefinição, está definida como CM_&lt;Sitecode\>. Está a utilizar um nome diferente que especificar.  

    -   **A porta do Service Broker:** Por predefinição, está definida para utilizar a porta do SQL Server Service Broker (SSB) predefinida de 4022. SQL Server utiliza-o para comunicar diretamente com a base de dados do site de outros sites.  

13. Na segunda **informações da base de dados** página, pode especificar localizações não predefinidas para o ficheiro de dados do SQL Server e o ficheiro de registo do SQL Server para a base de dados do site:  

    -   São fornecidas localizações predefinidas de ficheiros para o SQL Server.  

    -   A opção para especificar localizações de ficheiros não predefinidas não está disponível quando utiliza um cluster do SQL Server.  

    -   O Verificador de pré-requisitos não executa uma verificação de espaço livre em disco para não predefinidas localizações de ficheiros.  

14. No **as definições do fornecedor de SMS** página, especifique o FQDN para o servidor onde pretende instalar o fornecedor de SMS.  

    -   Por predefinição, o servidor de site é especificado.  

    -   Após a instalação do site, pode configurar fornecedores de SMS adicionais.  

15. No **definições de comunicação de cliente** página, escolha se pretende configurar todos os sistemas de sites para aceitar apenas comunicações HTTPS de clientes ou o método de comunicação seja configurado para cada função do sistema de sites.  

    Quando seleciona **todas as funções de sistema de site aceitam apenas comunicação HTTPS dos clientes**, o computador cliente tem de ter um certificado PKI válido para autenticação de cliente. Para obter mais informações sobre os requisitos de certificado PKI, consulte [requisitos de certificado PKI para o Configuration Manager](https://technet.microsoft.com/library/gg699362.aspx).  

    > [!NOTE]  
    > Este passo só se aplica quando instala um site primário. Se estiver a instalar um site de administração central, ignore este passo.  

16. No **funções do sistema de sites** página, escolha se pretende instalar um ponto de gestão ou ponto de distribuição. Para cada função que optar por instalar através da configuração:  

    -   Tem de introduzir o **FQDN** para o computador que irá alojar a função e escolha o cliente do método de ligação que o servidor irá suportar (HTTP ou HTTPS).  

    -   Se tiver selecionado **todas as funções de sistema de site aceitam apenas comunicação HTTPS dos clientes** na página anterior, as definições de ligação de cliente são automaticamente configuradas para HTTPS em não podem ser alteradas a menos que Retroceda e altere a definição.  

    > [!NOTE]  
    > Este passo só se aplica quando instala um site primário. Se estiver a instalar um site de administração central, ignore este passo.  

    > [!NOTE]  
    > Para instalar funções do sistema de sites, a configuração utiliza o **conta de instalação do sistema de sites**. Por predefinição, esta utiliza a conta de computador do site primário. Esta conta tem de ser um administrador local num computador remoto para instalar a função de sistema de sites. Se esta conta não possui as permissões necessárias, desmarque as funções de sistema de sites e instalar mais tarde a partir da consola do Configuration Manager, depois de configurar contas adicionais para utilizar como contas de instalação de sistema do site.  

17. No **dados de utilização** página, reveja as informações sobre os dados que a Microsoft recolhe e, em seguida, escolha **seguinte**.  

18. O **programa de configuração de ponto de ligação de serviço** página apenas está disponível durante a configuração:  

    -   Quando estiver a instalar um site primário autónomo.  

    -   Quando estiver a instalar um site de administração central.  

    > [!NOTE]  
    > Se estiver a instalar um site primário subordinado, ignore este passo (esta página não está disponível).  

     Se estiver a instalar um site de administração central como parte de um cenário de expansão do site e esta função já está instalada no site primário autónomo, tem de desinstalar esta função do site primário autónomo. Apenas uma instância desta função é permitida numa hierarquia — e só é permitida no site de nível superior da hierarquia.  

     Depois de selecionar uma configuração para o **ponto de ligação de serviço**, escolha **seguinte**. (Após a conclusão da configuração, pode alterar esta configuração a partir da consola do Configuration Manager).  

19. No **resumo de definições** página, reveja as definições que selecionou. Quando estiver pronto, selecione **seguinte** para iniciar o Verificador de pré-requisitos.  

20. No **a verificação dos pré-requisitos de instalação** página, quaisquer problemas que podem ser identificados estão listados.  

    -   Quando o Verificador de pré-requisitos detetar um problema, escolha um item na lista para obter detalhes sobre como resolver o problema.  

    -   Tem de resolver cada item com o estado **falha** antes de continuar a instalar o site. Itens com o estado **aviso** devem ser resolvidos, mas não bloqueiam a instalação do site.  

    -   Depois de resolver problemas, escolha **executar verificação** para voltar a executar o Verificador de pré-requisitos.  

     Quando executa o Verificador de pré-requisitos e não as verificações de recebem um **falha** Estado, pode escolher **Iniciar instalação** para iniciar a instalação de site.  

    > [!TIP]  
    > Além dos comentários que é fornecido no assistente, pode encontrar informações adicionais sobre problemas de pré-requisitos ao visualizar o **ConfigMgrPrereq.log** ficheiro na raiz da unidade de sistema do computador que está a instalar. Para obter uma lista de regras de pré-requisitos de instalação e as descrições, consulte [lista de verificações de pré-requisitos para o System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

21. No **instalação** página, o programa de configuração apresenta o estado da instalação. Quando a instalação de servidor do site principal estiver concluída, terá a opção de **fechar** o Assistente de instalação. Quando fechar o assistente, a instalação e configurações de site inicial continuam em segundo plano.  

    -   Pode ligar uma consola do Configuration Manager para o site antes da configuração está concluída. Esta consola liga como só de leitura e permite-lhe ver objetos e definições, mas não é possível introduzir edições.  

    -   Após a conclusão da configuração, poderá ligar uma consola que possa editar objetos e definições.  


## <a name="bkmk_expand"></a>Expandir um site primário autónomo
Quando tiver instalado um site primário autónomo como primeiro site, tem a opção mais tarde para expandir esse site para uma hierarquia maior instalando um site de administração central.   

Quando expande um site primário autónomo, instala um novo site de administração central que utiliza a base de dados do site primário autónomo existente como referência. Depois de instala o novo site de administração central, o site primário autónomo funciona como um site primário subordinado.

-   Apenas um site primário autónomo pode ser expandido para uma nova hierarquia.  

-   Apenas um site primário autónomo pode ser expandido para uma hierarquia específica. Não é possível utilizar esta opção para associar sites primários autónomos adicionais na mesma hierarquia. Em vez disso, utilize a migração para migrar dados de uma hierarquia para outra.  

-   Depois de expandir um site autónomo numa hierarquia com um site de administração central, pode adicionar sites primários subordinados adicionais.  

-   Para remover um site primário de uma hierarquia com um site de administração central, tem de desinstalar o site primário.  

Para expandir o site, utilize o Assistente de configuração do System Center Configuration Manager para instalar um novo site de administração central com os seguintes avisos:  

-   Tem de instalar o site de administração central utilizando a mesma versão do Configuration Manager como site primário autónomo.  

-   No **introdução** página do Assistente de configuração, selecionar a opção para instalar um site de administração central. Uma fase posterior da configuração, irá escolher uma opção para expandir um site primário autónomo existente.  

-   Quando configura o **seleção de idioma do cliente** página para o novo site de administração central, tem de selecionar os mesmos idiomas de cliente que estão configurados para o site primário autónomo que está a expandir.  

-   No **instalação de Site** página, selecione a opção para expandir o site primário autónomo.  

Para expandir um site primário autónomo, consulte o [pré-requisitos para expandir um site](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand)e, em seguida, utilize o procedimento  *[para instalar um site de administração central ou primário](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_installpri)*, anteriormente neste artigo.


## <a name="bkmk_secondary"></a>Instalar um site secundário
 Utilize a consola do Configuration Manager para instalar um site secundário.  

-   Se a consola que utiliza não está ligada ao site primário que será o site principal para o novo site secundário, o comando para instalar o site será replicado para o site primário correto.  

-   Antes de iniciar a instalação do site, certifique-se de que a conta de utilizador tem as permissões de pré-requisitos e, se o computador que irá alojar o novo site secundário cumpre todos os pré-requisitos para utilização como um servidor de site secundário.  

-   Quando instala o site secundário, o Configuration Manager configura o novo site para utilizar as portas de comunicação de cliente que estão configuradas no site primário principal.  

### <a name="bkmk_installsecondary"></a>Para instalar um site secundário  


1.  Na consola do Configuration Manager, navegue até à **administração** > **configuração do Site** > **Sites**. Selecione o site que será o site primário principal do novo site secundário.  

2.  Escolha **Criar Site secundário** para iniciar o **criar Assistente de Site secundário**.  

3.  No **antes de começar** página, confirme se o site primário apresentado é o site que pretende ser o elemento principal do novo site secundário. Em seguida, escolha **seguinte**.  

4.  No **geral** página, especifique o seguinte:  

    -   **Código do site**: Cada código do site numa hierarquia tem de ser exclusivo e composto por três dígitos alfanuméricos (da A z) e de 0 a 9. Uma vez que o código de site é utilizado em nomes de pastas, não utilize nomes reservados ao Windows para o site, incluindo:  

        -   AUX    
        -   CON    
        -   NUL    
        -   PRN  
        -   SMS  

       > [!NOTE]  
       > A configuração não verifica se o código do site que especificou já está a ser utilizado ou se é um nome reservado.  

    -   **Nome do servidor de site**: Este é o FQDN do servidor onde irá instalar o novo site secundário.  

    -   **Nome do site**: Cada site requer este nome amigável, que pode ajudar a identificar o site.  

    -   **Pasta de instalação**: Este é o caminho da pasta para a instalação do Configuration Manager. Não é possível alterar a localização após a instalação do site. O caminho não pode conter carateres Unicode nem espaços à direita.  

    > [!IMPORTANT]  
    > Depois de especificar detalhes nesta página, pode escolher **resumo** para utilizar as predefinições para o resto das opções do site secundário e para ir diretamente para o **resumo** página do assistente.  

    > -   Utilize esta opção apenas quando estiver familiarizado com as predefinições neste assistente e, se forem as definições que pretende utilizar.  
    > -   Grupos de limites não estão associados com o ponto de distribuição quando utiliza as predefinições. Por conseguinte, até configurar grupos de limites que incluem o servidor de site secundário, os clientes não utilizam o ponto de distribuição que está instalado neste site secundário como uma localização de origem de conteúdo.  

5.  No **ficheiros de origem de instalação** página, escolha como o computador do site secundário obtém os ficheiros de origem para instalar o site.  

     Quando utiliza ficheiros de origem que estão armazenados na rede ou armazenados no computador do site secundário:  

    -   A localização do ficheiro de origem tem de incluir uma pasta denominada **Redist** que inclui todos os ficheiros que foram anteriormente transferidos utilizando o programa de configuração.  

    -   Se qualquer um dos ficheiros da **Redist** não estão disponíveis, a configuração não irá instalar o site secundário.  

    -   A conta de computador do site secundário tem de ter **leitura** permissões para a origem de pasta e partilha de ficheiros.  

6.  No **definições do SQL Server** página, especifique a versão do SQL Server para utilizar e, em seguida, configure as definições relacionadas.  

    > [!NOTE]  
    > A configuração não valida as informações que introduzir nesta página antes de iniciar a instalação. Antes de continuar, verifique estas definições.  

     **Instalar e configurar uma cópia local do SQL Server Express no computador do site secundário**  

    -   **Porta do SQL Server Service**: Especifique a porta do serviço do SQL Server para o SQL Server Express utilizar. A porta de serviço normalmente é configurada para utilizar a porta TCP 1433, mas pode configurar outra porta.  

    -   **Porta do SQL Server Broker**: Especifique a porta do SQL Server Service Broker (SSB) para o SQL Server Express utilizar. O Mediador de serviço normalmente é configurado para utilizar a porta TCP 4022, mas pode configurar uma porta diferente. Tem de especificar uma porta válida que nenhum outro site ou serviço está a utilizar e que estão a bloquear o sem restrições de firewall.  

    > [!IMPORTANT]  
    > Quando o Configuration Manager instala o SQL Server Express, instala o SQL Server Express 2012 sem service Pack:  

    > -   Para o site secundário seja suportado, após a instalação, tem de atualizar o SQL Server Express 2012 para [uma versão suportada](/sccm/core/plan-design/configs/support-for-sql-server-versions#bkmk_SQLVersions).
    > -   Além disso, se a nova instalação de site secundário não for concluída, mas a instalação do SQL Server Express 2012, tem de atualizar essa instância do SQL Server Express antes do Configuration Manager com êxito pode repetir a instalação de site secundário.  

     **Utilizar uma instância existente do SQL Server**  

    -   **FQDN do SQL Server**: Reveja o FQDN para o computador a executar o SQL Server. Tem de utilizar um servidor local a executar o SQL Server para alojar a base de dados do site secundário e não é possível modificar esta definição.  

    -   **Instância do SQL Server**: Especifique a instância do SQL Server para utilizar como a base de dados do site secundário. Deixe esta opção em branco para utilizar a instância predefinida.  

    -   **Nome de base de dados do site do ConfigMgr**: Especifique o nome a utilizar para a base de dados do site secundário.  

    -   **Porta do SQL Server Broker**: Especifique a porta do SQL Server Service Broker (SSB) para o SQL Server utilizar. Tem de especificar uma porta válida que nenhum outro site ou serviço está a utilizar e que não existem restrições de firewall bloquear.  

    > [!TIP]  
    > Consulte [versões do SQL Server suportada](../../../../core/plan-design/configs/support-for-sql-server-versions.md) para obter uma lista das versões do SQL Server que suporta o System Center Configuration Manager.  

7.  No **ponto de distribuição** página, configure as definições do ponto de distribuição que irá ser instalado num servidor do site secundário.  

     **Definições necessárias:**  

    -   **Especifique a forma como os dispositivos cliente comunicam com o ponto de distribuição**: Escolha entre HTTP e HTTPS.  

    -   **Criar um certificado autoassinado ou importar um certificado de cliente PKI**: Escolha entre utilizar um certificado autoassinado (que lhe permite também permitir ligações anónimas de clientes do Configuration Manager para a biblioteca de conteúdos) ou importar um certificado a partir da sua PKI.  

         O certificado é utilizado para autenticar o ponto de distribuição para um ponto de gestão antes do ponto de distribuição envia mensagens de estado.  

         Para obter informações sobre os requisitos de certificados, consulte [requisitos de certificado PKI para o Configuration Manager](https://technet.microsoft.com/library/gg699362.aspx).  

    **Definições opcionais:**  

    -   **Instalar e configurar o IIS se exigido pelo Configuration Manager**: Selecione esta definição para permitir que o Configuration Manager instale e configure serviços de informação Internet (IIS) no servidor se ainda não estiver instalado. IIS tem de ser instalado em todos os pontos de distribuição.  

        > [!NOTE]  
        > Embora esta definição é opcional, IIS tem de estar instalado no servidor para que um ponto de distribuição possa ser instalado com êxito.  

    -   **Ativar e configurar o BranchCache para este ponto de distribuição**.  

    -   **Descrição**. Esta é uma descrição amigável do ponto de distribuição para o ajudar a reconhecê-lo.  

    -   **Ativar conteúdo pré-configurado para este ponto de distribuição**.  

8.  No **definições de unidade** página, especifique as definições de unidade para o ponto de distribuição do site secundário.  

     Pode configurar até duas unidades de disco para a biblioteca de conteúdos e duas unidades de disco para a partilha de pacote. No entanto, o Configuration Manager possa utilizar unidades adicionais quando as duas primeiras atingem a reserva do espaço de unidade configurada. O **definições de unidade** página é onde configura a prioridade das unidades de disco e a quantidade de espaço livre que deverá permanecer disponível em cada unidade de disco.  

    -   **(MB) de reserva do espaço na unidade**: O valor que configurar para esta definição determina a quantidade de espaço livre numa unidade antes do Configuration Manager escolher uma unidade diferente e continuar o processo de cópia para essa unidade. Ficheiros de conteúdo podem abranger várias unidades.  

    -   **Localizações de conteúdo**: Especifique as localizações de conteúdos para a partilha de biblioteca e o pacote de conteúdos. O Configuration Manager copia os conteúdos para localização de conteúdos primária até a quantidade de espaço livre atinge o valor especificado para **reserva de espaço na unidade (MB)**.

     Por predefinição, as localizações de conteúdo estão definidas como **automática**. A localização de conteúdos primária está definida para a unidade de disco que tem mais espaço de disco no momento de instalação. A localização secundária é definida para a unidade de disco que tenha mais disco espaço livre após a unidade principal. Quando as unidades principais e secundárias atingem a reserva do espaço na unidade, o Configuration Manager seleciona uma outra unidade disponível com mais disco espaço livre e continua o processo de cópia.  

9. No **validação de conteúdo** página, especifique se pretende validar a integridade dos ficheiros de conteúdo no ponto de distribuição.  

    -   Quando ativar a validação de conteúdo com base numa agenda, o Configuration Manager iniciará o processo à hora agendada e todo o conteúdo no ponto de distribuição é verificado.  

    -   Também pode configurar o **prioridade de validação de conteúdo**.  

    -   Para ver os resultados do processo de validação de conteúdo, na consola do Configuration Manager, navegue até à **monitorização** > **estado da distribuição** > **estado do conteúdo**. O conteúdo para cada tipo de pacote (por exemplo, aplicação, pacote de atualização de Software e imagem de arranque) é apresentado.  

10. No **grupos de limites** página, gira os grupos de limites que este ponto de distribuição está atribuído a:  

    -   Durante a implementação de conteúdos, os clientes tem de ser um grupo de limites que estão associados com o ponto de distribuição para utilizá-la como uma localização de origem para o conteúdo.  

    -   Pode selecionar o **permitir a localização de origem de contingência para conteúdo** opção para permitir que os clientes fora destes grupos de limites recorram à contingência e utilizem o ponto de distribuição como localização de origem para o conteúdo quando não existem pontos de distribuição preferenciais disponíveis.  

     Para obter informações sobre pontos de distribuição preferenciais, consulte o [conceitos fundamentais da gestão de conteúdos](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) tópico.  

11. No **resumo** página, verifique as definições e, em seguida, escolha **seguinte** para instalar o site secundário. Quando o assistente apresentar a **conclusão** página, pode fechar o assistente. A instalação do site secundário continua em segundo plano.  


### <a name="bkmk_verify"></a>Para verificar o estado de instalação de site secundário  

1.  Na consola do Configuration Manager, navegue até à **administração** > **configuração do Site** > **Sites**.  

2.  Selecione o servidor de site secundário que estiver a instalar e, em seguida, escolha **Mostrar estado da instalação**.  

    > [!TIP]  
    > Quando instalar mais do que um site secundário de uma vez, o Verificador de pré-requisitos é executada relativamente a um único site um momento e tem de concluir um site antes de iniciar a verificação do site seguinte.  

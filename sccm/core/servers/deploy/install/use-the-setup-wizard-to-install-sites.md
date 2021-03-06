---
title: Assistente de configuração
titleSuffix: Configuration Manager
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 67c82a884a5d3df3b1e61e1f9f2c109ff2b7fef6
ms.sourcegitcommit: af8693048e6706ffda72572374f56e0bc7dfce2c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/11/2019
ms.locfileid: "57737331"
---
# <a name="use-the-setup-wizard-to-install-configuration-manager-sites"></a>Utilize o Assistente de configuração para instalar sites do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para instalar um novo site do Configuration Manager utilizando uma interface de utilizador interativa, utilize o Assistente de configuração do Configuration Manager (setup.exe). O assistente suporta a instalação de um site primário ou site de administração central. Também é usar o Assistente para [atualizar uma instalação de avaliação](/sccm/core/servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install) do Configuration Manager para uma instalação totalmente licenciada. Quando não quiser utilizar o assistente, em vez disso, pode utilizar um [script de instalação](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites) e executar uma instalação autónoma de linha de comandos.

Instale um site secundário a partir da consola do Configuration Manager. Os sites secundários não suportam uma instalação com script de linha de comandos.



## <a name="bkmk_primary"></a> Instalar uma administração central ou site primário

Utilize o procedimento seguinte para instalar um site de administração central ou um site primário. Também usá-lo para atualizar um site de avaliação para um site totalmente licenciada do Configuration Manager.   

Antes de iniciar a instalação do site, estar familiarizados com os detalhes nos seguintes artigos:
- [Preparar a instalação de sites](/sccm/core/servers/deploy/install/prepare-to-install-sites)
- [Pré-requisitos para instalar sites](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites)

Se estiver a instalar um site de administração central como parte de um cenário de expansão do site, reveja [expandir um site primário autónomo](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_expand) antes de utilizar o procedimento seguinte.

### <a name="bkmk_installpri"></a> Processo para instalar um site de administração central ou primário

1. No computador onde pretende instalar o site, execute `<InstallationMedia>\SMSSETUP\BIN\X64\Setup.exe` para iniciar o **Assistente de configuração do System Center Configuration Manager**.  

    > [!NOTE]  
    > Quando instala um site de administração central para expandir um site primário autónomo, ou instale um novo site primário subordinado numa hierarquia existente, utilize o suporte de instalação (arquivos de origem) que correspondem à versão do site existente ou sites. Se instalou atualizações na consola que alteraram a versão dos sites anteriormente instalados, não utilize o suporte de dados de instalação original. Em vez disso, utilizar ficheiros de origem do [CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder) de um site atualizado. Configuration Manager requer a utilização de ficheiros de origem que correspondem à versão do site existente que seu novo site irá ligar.  

2. Sobre o **antes de começar** página, selecione **próxima**.  

3. Sobre o **introdução ao** , selecione o tipo de site que pretende instalar:  

    - **Site de administração central**, como o primeiro site numa nova hierarquia ou ao expandir um site primário autónomo:  

        Selecione **instala um site de administração central do Configuration Manager**.  

        Durante um passo posterior deste procedimento, está dada a opção para instalar um site de administração central como o primeiro site numa nova hierarquia ou para instalar um site de administração central para expandir num site primário autónomo.  

    - **Site primário**, como um site primário autónomo que é o primeiro site numa nova hierarquia ou como um filho primário:  

        Selecione **instalar um site primário do Configuration Manager**.  

        > [!TIP]  
        > Normalmente, apenas selecionar a opção **utilizar opções de instalação típicas para um site primário autónomo** quando pretende instalar um site primário autónomo num ambiente de teste. Quando seleciona esta opção, o programa de configuração faz as seguintes ações:  
        > 
        > - Configura automaticamente o site como um site primário autónomo.  
        > - Utiliza um caminho de instalação predefinido.  
        > - Utiliza uma instalação local da instância predefinida do SQL Server para a base de dados do site.  
        > - Instala um ponto de gestão e um ponto de distribuição no computador do servidor do site.  
        > - Configura o site com inglês e o idioma de apresentação do SO no servidor do site primário se corresponder a um dos idiomas que o Configuration Manager suporta.  

4. Sobre o **chave de produto** página:  

    - Escolha se pretende instalar o Configuration Manager como uma edição de avaliação ou uma edição licenciada.  

        - Se selecionar uma edição licenciada, introduza a sua chave de produto e escolha **seguinte**.  

        - Se selecionar uma edição de avaliação, escolha **seguinte**. (Pode atualizar uma instalação de avaliação para uma instalação completa mais tarde.)  

    - Também pode especificar a **data de expiração do Software Assurance** do seu contrato de licenciamento. É um lembrete conveniente dessa data. Se não introduzir esta data durante a configuração, pode especificá-lo mais tarde a partir da consola do Configuration Manager.  

        > [!NOTE]   
        > Microsoft não será validado a data de expiração que introduziu e não utilizar esta data para validação da licença. Pode usá-lo como um lembrete da data de validade. Esta data é útil porque o Configuration Manager verifica periodicamente a existência de novas atualizações de software disponibilizadas online. O estado de licença do software assurance deve ser atual para que está qualificado para utilizar estas atualizações adicionais.    

    Para obter mais informações, consulte [licenciamento e ramificações](/sccm/core/understand/learn-more-editions).  

5. Sobre o **termos de licenciamento de Software Microsoft** página, leia e aceite os termos de licença.  

6. Sobre o **licenças de pré-requisito** página, leia e aceite os termos de licenciamento do software de pré-requisito. A configuração transfere e instala automaticamente o software em sistemas de sites ou clientes quando necessário. Aceite todos os termos antes de continuar para a página seguinte.  

7. Sobre o **transferências de pré-requisitos** página, especifique se a configuração deverá transferir os ficheiros redistribuíveis de pré-requisitos a partir da internet ou utilizar ficheiros anteriormente transferidos:  

    - Se pretender que o programa de configuração para transferir os ficheiros neste momento, selecione **transferir ficheiros necessários**. Em seguida, especifique uma localização para armazenar os ficheiros.  

    - Se tiver transferido anteriormente os ficheiros utilizando [programa de configuração](/sccm/core/servers/deploy/install/setup-downloader), selecione **utilizar ficheiros anteriormente transferidos**. Em seguida, especifique a pasta de transferência.  

        > [!TIP]  
        > Se utilizar ficheiros anteriormente transferidos, certifique-se de que o caminho para a pasta de transferência contém a versão mais recente dos ficheiros.  

8. Sobre o **seleção de idioma do servidor** página, selecione os idiomas que estão disponíveis para a consola do Configuration Manager e para relatórios. (O inglês está selecionado por predefinição e não pode ser removido.) Para obter mais informações, consulte [pacotes de idiomas](/sccm/core/servers/deploy/install/language-packs).  

9. Sobre o **seleção de idioma do cliente** , selecione os idiomas que estão disponíveis para computadores cliente. Também especifica se pretende ativar todos os idiomas de cliente para clientes de dispositivos móveis. (O inglês está selecionado por predefinição e não pode ser removido.)  

    > [!IMPORTANT]  
    > Quando utiliza um site de administração central, certifique-se de que configurou no site de administração central de idiomas de cliente incluem todos os idiomas de cliente configurados em cada site primário subordinado. Os clientes que instalar a partir de um ponto de distribuição tem acesso para os idiomas de cliente a partir do site de nível superior, enquanto os clientes que instalar a partir de um ponto de gestão têm acesso para os idiomas de cliente a partir do site primário atribuído.  

10. Sobre o **definições de instalação e Site** , especifique as seguintes definições para o novo site que estiver a instalar:  

    - **Código do site**: [Cada código do site numa hierarquia tem de ser exclusivo](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_sitecodes). Utilize três dígitos de alfanuméricos: R por meio de Z e de 0 a 9. Como o código do site é utilizado em nomes de pastas, não utilize nomes reservados ao Windows, incluindo:    
        - AUX  
        - CON    
        - NUL    
        - PRN    
        - SMS  

        > [!NOTE]  
        > A configuração não verifica se o código do site que especificou já está em utilização ou se é um nome reservado.  

    - **Nome do site**: Cada site requer este nome amigável, que pode ajudá-lo a identificar o site.  

    - **Pasta de instalação**: Esta pasta é o caminho para a instalação do Configuration Manager. Não é possível alterar a localização após a instalação do site. O caminho não pode conter carateres Unicode nem espaços à direita.  

11. Sobre o **instalação do Site** página, utilize a opção seguinte que corresponda ao seu cenário:  

    - **Estou a instalar um site de administração central:**  

        Sobre o **instalação do Site de Administração Central** página, selecione **instalar como o primeiro site numa nova hierarquia**e, em seguida, escolha **seguinte** para continuar.  

    - **Estou a expandir um site primário autónomo para uma hierarquia com um site de administração central:**  

        Sobre o **instalação do Site de Administração Central** página, selecione **expandir um site primário autónomo existente para uma hierarquia**. Em seguida, especifique o FQDN do servidor do site primário autónomo e escolha **seguinte** para continuar.  

        O suporte de dados que utilizar para instalar o novo site de administração central tem de corresponder à versão do site primário.  

    - **Estou a instalar um site primário autónomo:**  

        Sobre o **instalação do Site primário** página, selecione **instalar o site primário como um site autónomo**e, em seguida, escolha **seguinte**.  

    - **Estou a instalar um site primário subordinado:**  

        Sobre o **instalação do Site primário** página, selecione **associar o site primário para uma hierarquia existente**. Em seguida, especifique o FQDN para o site de administração central e escolha **seguinte**.  

12. Sobre o **informações da base de dados** , especifique as seguintes informações:  

    - **Nome do SQL Server (FQDN)**: Por predefinição, este valor é definido como computador do servidor do site.  

        Se utilizar uma porta personalizada, adicione essa porta para o FQDN do SQL Server. Siga o FQDN do SQL Server com uma vírgula e, em seguida, o número de porta. Por exemplo, para o servidor *SQLServer1.fabrikam.com*, utilize o seguinte procedimento para especificar a porta *1551*: `SQLServer1.fabrikam.com,1551`  

    - **Nome da instância**: Por predefinição, este valor está em branco. Ele usa a instância predefinida do SQL no computador do servidor do site.  

    - **Nome da base de dados**: Por predefinição, este valor é definido como `CM_<Sitecode>`. Pode personalizar este valor.  

    - **Porta do Service Broker**: Por predefinição, este valor é definido para utilizar a porta do SQL Server Service Broker (SSB) predefinida de 4022. SQL utiliza-o para comunicar diretamente com a base de dados de outros sites.  

13. No segundo **informações da base de dados** página, pode especificar localizações personalizadas para o ficheiro de dados do SQL Server e o ficheiro de registo do SQL Server para a base de dados do site:  

    - Por predefinição, utiliza localizações predefinidas de ficheiros para o SQL Server.  

    - Quando utiliza um cluster do SQL Server, a opção para especificar localizações de ficheiros personalizados não está disponível.  

    - O Verificador de pré-requisitos não executa uma verificação de espaço livre em disco para localizações de ficheiros personalizadas.  

14. Sobre o **definições do fornecedor de SMS** página, especifique o FQDN para o servidor onde pretende instalar o fornecedor de SMS.  

    - Por predefinição, especifica o servidor do site.  

    - Após a instalação do site, pode configurar fornecedores de SMS adicionais. Para obter mais informações, consulte [planear o fornecedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).  

15. Sobre o **definições de comunicação de cliente** página, escolha se pretende configurar todos os sistemas de sites para aceitar apenas comunicações HTTPS de clientes ou para o método de comunicação para ser configurado para cada função de sistema de sites.  

    Quando seleciona **todas as funções de sistema de site aceitam apenas comunicação HTTPS dos clientes**, o computador cliente tem de ter um certificado PKI válido para autenticação de cliente. Para obter mais informações, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

    > [!NOTE]  
    > Este passo aplica-se apenas ao instalar um site primário. Se estiver a instalar um site de administração central, ignore este passo.  

16. Sobre o **funções do sistema de sites** página, escolha se pretende instalar um ponto de gestão ou ponto de distribuição. Para cada função que optar por instalar através da configuração:  

    - Introduza o **FQDN** para o servidor que irá alojar a função. Em seguida, escolha o cliente do método de ligação que o servidor irá suportar: HTTP ou HTTPS.  

    - Se tiver selecionado **todas as funções de sistema de site aceitam apenas comunicação HTTPS dos clientes** na página anterior, as definições de ligação de cliente são automaticamente configuradas para HTTPS. Não é possível alterar esta definição, a menos que voltar à página anterior.  

    > [!NOTE]  
    > Este passo aplica-se apenas ao instalar um site primário. Se estiver a instalar um site de administração central, ignore este passo.  

    > [!NOTE]  
    > Para instalar funções do sistema de sites, a configuração utiliza a **conta de instalação do sistema de sites**. Por predefinição, esta utiliza a conta de computador do site primário. Esta conta tem de ser um administrador local num computador remoto para instalar a função de sistema de sites. Se esta conta não tiver as permissões necessárias, desmarque as funções de sistema de sites e instale-los mais tarde a partir da consola do Configuration Manager, depois de configurar contas adicionais para utilizar como contas de instalação do sistema de site. Para obter mais informações, consulte [contas](/sccm/core/plan-design/hierarchy/accounts#site-system-installation-account).  

17. Sobre o **dados de utilização** página, reveja as informações sobre os dados que a Microsoft recolhe e, em seguida, escolha **próxima**. Para obter mais informações, consulte [diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  

18. O **configuração do ponto de ligação de serviço** página só está disponível durante os seguintes cenários:  

    - Quando estiver a instalar um site primário autónomo.  

    - Quando estiver a instalar um site de administração central.  

    > [!NOTE]  
    > Se estiver a instalar um site primário subordinado, ignore este passo.  

     Se estiver a instalar um site de administração central como parte de um cenário de expansão do site e esta função já está instalada no site primário autónomo, primeiro Desinstale esta função do site primário autónomo. Apenas uma instância desta função é permitida numa hierarquia e só é suportada no site de nível superior da hierarquia.  

     Depois de selecionar uma configuração para o **ponto de ligação de serviço**, escolha **próxima**. Depois de concluída a configuração, pode alterar esta configuração a partir da consola do Configuration Manager. Para obter mais informações, consulte [sobre o ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point).  

19. Sobre o **resumo de definições** , reveja a configuração que selecionou. Quando estiver pronto, escolha **seguinte** para iniciar o Verificador de pré-requisitos.  

20. Sobre o **verificação de instalação de pré-requisitos** página, ele apresenta uma lista de quaisquer problemas que possa identificar o Verificador de.  

    - Quando o Verificador de pré-requisitos encontra um problema, escolha um item na lista para obter detalhes sobre como resolver o problema.  

    - Antes de poder continuar a instalar o site, resolva **falhada** itens. Também deve resolver os itens com o estado **aviso**, mas eles não bloqueiam a instalação do site.  

    - Depois de resolver problemas, escolha **executar verificação** voltar a executar o Verificador de pré-requisitos.  

        Quando o Verificador de pré-requisitos é executado e nenhuma verificação receber uma **falhada** Estado, pode escolher **Iniciar instalação** para iniciar a instalação de site.  

    > [!TIP]  
    > Além dos comentários que fornece o assistente, pode encontrar informações adicionais sobre problemas de pré-requisitos no **Configmgrprereq** ficheiro. É na raiz da unidade de sistema do computador no qual está a instalar o site. Para obter mais informações, consulte [lista de verificações de pré-requisitos](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

21. Sobre o **instalação** página, o programa de configuração apresenta o estado de instalação. Quando a instalação de servidor do site principal estiver concluída, pode **fechar** o Assistente de instalação. Quando fecha o assistente, a instalação e configurações de site inicial continuam em segundo plano.  

    - Pode ligar uma consola do Configuration Manager para o site antes da configuração está concluída. Esta consola liga como só de leitura e permite ver objetos e definições, mas não é possível modificar nada.  

    - Após a conclusão da configuração, pode ligar uma consola que possa editar objetos e definições.  



## <a name="bkmk_expand"></a> Expandir um site primário autónomo

Quando instalar um site primário autónomo como primeiro site, terá a opção mais tarde para expandir esse site para uma hierarquia maior instalando um site de administração central.   

Quando expande um site primário autónomo, instala um novo site de administração central que utiliza a base de dados do site primário autónomo existente como referência. Após a instalação do novo site de administração central, site primário autónomo funciona como um site primário subordinado.

- Apenas pode expandir um site primário autónomo para uma nova hierarquia.  

- Só é possível expandir um site primário autónomo para uma hierarquia específica. Não é possível utilizar esta opção para associar sites primários autónomos adicionais na mesma hierarquia. Em vez disso, utilize o Assistente de migração para migrar dados de uma hierarquia para outra. Para obter mais informações, consulte [migrar dados entre hierarquias](/sccm/core/migration/migrate-data-between-hierarchies).  

- Depois de expandir um site autónomo numa hierarquia com um site de administração central, pode adicionar sites primários subordinados adicionais.  

- Para remover um site primário de uma hierarquia com um site de administração central, primeiro de desinstalar o site primário.  


Para expandir o site, utilize o Assistente de configuração do Configuration Manager para instalar um novo site de administração central com os seguintes avisos:  

- Instale o site de administração central, utilizando a mesma versão do Configuration Manager como site primário autónomo.  

- Sobre o **introdução ao** página do Assistente de configuração, selecione a opção para instalar um site de administração central. Numa fase posterior da configuração, que vai escolher uma opção para expandir um site primário autónomo existente.  

- Quando configura a **seleção de idioma do cliente** para o novo site de administração central, selecione os mesmos idiomas de cliente que estão configurados para o site primário autónomo que está a expandir.  

- Sobre o **instalação do Site** página, selecione a opção para expandir o site primário autónomo.  


Para expandir um site primário autónomo, consulte a [pré-requisitos para expandir um site](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand). Em seguida, utilize o procedimento [para instalar um site de administração central ou primário](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_installpri) no início deste artigo.




## <a name="bkmk_secondary"></a> Instalar um site secundário

Utilize a consola do Configuration Manager para instalar um site secundário.  

- Se a consola que utilizar não está ligada ao site primário que será o site principal para o novo site secundário, o comando para instalar o site é replicado para o site primário correto.  

- Antes de iniciar a instalação do site, certifique-se de que a sua conta de utilizador tem as permissões de pré-requisitos. Além disso, certifique-se de que o servidor que irá alojar o novo site secundário cumpre todos os pré-requisitos para utilização como um servidor de site secundário.  

- Quando instala o site secundário, o Configuration Manager configura o novo site para utilizar as portas de comunicação de cliente que estão configuradas no site primário principal.  


### <a name="bkmk_installsecondary"></a> Processo para instalar um site secundário  

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó. Selecione o site que será o site primário principal do novo site secundário.  

2. Para iniciar o **Assistente para criar sites secundários**, escolha **Criar Site secundário** na faixa de opções.  

3. Sobre o **antes de começar** página, confirme que o site primário que está listado é o site que pretende que seja o principal do novo site secundário. Em seguida, escolha **seguinte**.  

4. Na página **Geral** , especifique as seguintes definições:  

    - **Código do site**: Cada código do site numa hierarquia tem de ser exclusivo. Utilize três dígitos de alfanuméricos: R por meio de Z e de 0 a 9. Como o código do site é utilizado em nomes de pastas, não utilize nomes reservados ao Windows, incluindo:  

        - AUX    
        - CON    
        - NUL    
        - PRN  
        - SMS  

    > [!NOTE]  
    > A configuração não verifica se o código do site que especificou já está em utilização ou se é um nome reservado.  

    - **Nome do servidor de site**: Este valor é o FQDN do servidor onde irá instalar o novo site secundário.  

    - **Nome do site**: Cada site requer este nome amigável, que pode ajudá-lo a identificar o site.  

    - **Pasta de instalação**: Esta pasta é o caminho para a instalação do Configuration Manager. Não é possível alterar a localização após a instalação do site. O caminho não pode conter carateres Unicode nem espaços à direita.  

    > [!IMPORTANT]  
    > Depois de especificar detalhes nesta página, pode escolher **resumo** para ir diretamente para o **resumo** página do assistente. Esta ação utiliza as predefinições para o resto das opções de site secundário.  
    > 
    > - Utilize esta opção apenas quando estiver familiarizado com as predefinições neste assistente, e eles são as definições que pretende utilizar.  
    > - Quando utiliza as predefinições, grupos de limites não são associados ao ponto de distribuição. Até configurar grupos de limites que incluem o servidor de site secundário, os clientes não utilizam o ponto de distribuição que está instalado neste site secundário como uma localização de origem de conteúdo.  

5. Sobre o **ficheiros de origem de instalação** página, selecione como o computador do site secundário obtém os ficheiros de origem para instalar o site.  

    Quando utiliza o CD. Ficheiros de origem mais recente que são partilhados na rede ou copiados localmente para o servidor de site secundário de destino:  

    - **Versão 1802 e anterior**

        - O CD. Localização do ficheiro de origem mais recente inclui uma pasta denominada **Redist**. Mover isso **Redist** pasta como uma subpasta sob a **SMSSETUP** pasta.  

            > [!Note]  
            > Se ocorrerem erros de falta de correspondência do hash durante a configuração, atualize o **Redist** pasta. Utilize o [programa de configuração](/sccm/core/servers/deploy/install/setup-downloader) para obter os ficheiros mais recentes. Para todos os ficheiros que fazem com que um erro de falta de correspondência do hash, também copiá-los de atualizada **Redist** pasta para o **SMSSETUP\BIN\X64** pasta. 

    - **Versão 1806 e posterior**<!-- SCCMDocs-pr issue 3164 -->

        - O CD. Localização do ficheiro de origem mais recente inclui uma pasta denominada **Redist**. Mover isso **Redist** pasta como uma subpasta sob a **SMSSETUP** pasta.  

        - Copie os seguintes ficheiros dos **Redist** pasta para o **SMSSETUP\BIN\X64** pasta:   
            - SharedManagementObjects.msi
            - SQLSysClrTypes.msi
            - sqlncli.msi

    - Se qualquer um dos arquivos provenientes **Redist** não estão disponíveis, a configuração não consegue instalar o site secundário.  

    - A conta de computador do servidor do site secundário tem de ter **leitura** permissões para a origem de pasta e partilha de ficheiros.  

6. Sobre o **definições do SQL Server** página, especifique a versão do SQL Server para utilizar e, em seguida, configure as definições relacionadas.  

    > [!NOTE]  
    > A configuração não valida as informações que introduzir nesta página antes de iniciar a instalação. Antes de continuar, verifique se estas definições.  

    - **Instalar e configurar uma cópia local do SQL Express no computador do site secundário**  

        - **Porta de serviço do SQL Server**: Especifique a porta de serviço do SQL Server para SQL Server Express utilizar. A porta do serviço normalmente é configurada para utilizar a porta TCP 1433, mas pode configurar outra porta.  

        - **Porta do SQL Server Broker**: Especifique a porta do SQL Server Service Broker (SSB) para o SQL Server Express utilizar. O Service Broker normalmente é configurado para utilizar a porta TCP 4022, mas pode configurar uma porta diferente. Especifique uma porta válida que nenhum outro site ou serviço está a utilizar e que estão a bloquear o sem restrições de firewall.  

    - **Utilizar uma instância existente do SQL Server**  

        - **FQDN do SQL Server**: Reveja o FQDN para o computador a executar o SQL Server. Tem de utilizar um servidor local com o SQL Server para alojar a base de dados do site secundário e não pode modificar esta definição.  

        - **Instância do SQL Server**: Especifique a instância do SQL Server para utilizar como a base de dados do site secundário. Deixe esta opção em branco para utilizar a instância predefinida.  

        - **Nome de base de dados do site do ConfigMgr**: Especifique o nome a utilizar para a base de dados do site secundário.  

        - **Porta do SQL Server Broker**: Especifique a porta do SQL Server Service Broker (SSB) para o SQL Server utilizar. Especifique uma porta válida que nenhum outro site ou serviço está a utilizar e que não existem restrições de firewall bloquear.  

    > [!TIP]  
    > Para obter uma lista das versões do SQL Server que suporta o System Center Configuration Manager, consulte [versões do SQL Server suportada](/sccm/core/plan-design/configs/support-for-sql-server-versions).  

7. Sobre o **ponto de distribuição** página, configure definições para o ponto de distribuição que será instalado no servidor do site secundário.  

    - **Definições necessárias:**  

        - **Especifique a forma como os dispositivos cliente comunicam com o ponto de distribuição**: Escolha entre HTTP e HTTPS.  

        - **Criar um certificado autoassinado ou importar um certificado de cliente PKI**: Escolha entre utilizar um certificado autoassinado ou importar um certificado em sua PKI. Um certificado autoassinado permite também permitir ligações anónimas de clientes do Configuration Manager para a biblioteca de conteúdos. O certificado é utilizado para autenticar o ponto de distribuição para um ponto de gestão antes do ponto de distribuição envia mensagens de estado. Para obter mais informações, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

    - **Definições opcionais:**  

        - **Instalar e configurar o IIS se exigido pelo Configuration Manager**: Selecione esta definição para permitir que o Configuration Manager instalar e configurar serviços de informação Internet (IIS) no servidor, se ainda não estiver instalado. IIS é necessário em todos os pontos de distribuição.  

            > [!NOTE]  
            > Embora esta definição é opcional, IIS tem de ser instalado no servidor para que um ponto de distribuição possa ser instalado com êxito.  

        - **Ativar e configurar a BranchCache deste ponto de distribuição**  

        - **Descrição**: Este valor é uma descrição amigável para o ponto de distribuição para o ajudar a reconhecê-lo.  

        - **Ativar conteúdo pré-configurado para este ponto de distribuição**  

8. Sobre o **definições de unidade** , especifique as definições de unidade para o ponto de distribuição do site secundário.  

    Pode configurar até duas unidades de disco para a biblioteca de conteúdos e duas unidades de disco para a partilha de pacote. No entanto, o Configuration Manager possa utilizar unidades adicionais quando as duas primeiras atingem a reserva do espaço na unidade configurada. O **definições de unidade** página é onde configurar a prioridade para as unidades de disco e a quantidade de espaço livre em disco para permanecer em cada unidade de disco.  

    - **(MB) de reserva de espaço na unidade**: O valor que configurar para esta definição determina a quantidade de espaço livre numa unidade antes do Configuration Manager escolher uma unidade diferente e continuar o processo de cópia para essa unidade. Ficheiros de conteúdo podem abranger várias unidades.  

    - **Localizações de conteúdo**: Especifique as localizações de conteúdos para a partilha de biblioteca e o pacote de conteúdo. O Configuration Manager copia os conteúdos para localização de conteúdos primária até a quantidade de espaço livre atingir o valor especificado para **reserva de espaço na unidade (MB)**.  

    Por predefinição, as localizações de conteúdo estão definidas como **automática**. A localização de conteúdos primária está definida para a unidade de disco que tem mais espaço de disco no momento da instalação. A localização secundária está definida para a unidade de disco que tenha mais disco espaço livre após a unidade principal. Quando as unidades principais e secundárias atingem a reserva de espaço da unidade, o Configuration Manager seleciona a outra unidade disponível com o espaço de disco mais livre e continuar o processo de cópia.  

9. Sobre o **validação de conteúdo** página, especifique se pretende validar a integridade dos ficheiros de conteúdo no ponto de distribuição.  

    - Quando ativa a validação de conteúdos com base numa agenda, o Configuration Manager inicia o processo à hora agendada. Todo o conteúdo no ponto de distribuição é verificado.  

    - Também pode configurar o **prioridade da validação de conteúdo**.  

    - Para ver os resultados do processo de validação de conteúdo, na consola do Configuration Manager, vá para o **monitorização** área de trabalho, expanda **estado de distribuição**e selecione o **conteúdo Estado** nó. Ele exibe o conteúdo para cada tipo de pacote. Esses tipos incluem aplicações, pacotes de atualização de software e imagens de arranque.  

10. Sobre o **grupos de limites** página, gerir os grupos de limites que este ponto de distribuição está atribuído a:  

    - Durante a implementação de conteúdos, os clientes devem ser num grupo de limites que está associada o utilizá-la como uma localização de origem para o conteúdo do ponto de distribuição.  

    - Pode selecionar o **permitir a localização de origem de contingência para conteúdo** opção para permitir que os clientes fora destes grupos de limites recorram à contingência e utilizem o ponto de distribuição como uma localização de origem de conteúdo quando não houver pontos de distribuição preferenciais está disponível.  

        Para obter mais informações, consulte a [conceitos fundamentais da gestão de conteúdos](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).  

11. Sobre o **resumo** página, verifique as definições e, em seguida, escolha **próxima** para instalar o site secundário. Quando o assistente apresentar a **conclusão** página, pode fechar o assistente. A instalação de site secundário continua em segundo plano.  


### <a name="bkmk_verify"></a> Como verificar o estado de instalação do site secundário  

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó.  

2. Selecione o site secundário que estiver a instalar e, em seguida, escolha **Mostrar estado da instalação** na faixa de opções.  

    > [!TIP]  
    > Ao instalar mais do que um site secundário ao mesmo tempo, o Verificador de pré-requisitos é executado em relação a um único site ao mesmo tempo. Ele tem de concluir a um site antes de iniciar a verificação do site seguinte.  


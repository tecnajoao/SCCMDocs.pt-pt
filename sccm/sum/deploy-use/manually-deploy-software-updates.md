---

title: "Implantar manualmente atualizações de software | Microsoft Docs"
description: "Para implantar atualizações manualmente, selecione atualizações no console do Configuration Manager e implantá-los, ou adicionar manualmente atualizações a um grupo de atualização e implantar o grupo."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.translationtype: Machine Translation
ms.sourcegitcommit: c6ee0ed635ab81b5e454e3cd85637ff3e20dbb34
ms.openlocfilehash: 2a0d5f12b99689749833c109d4fa399f99451d8a
ms.contentlocale: pt-pt
ms.lasthandoff: 06/08/2017


---

#  <a name="BKMK_ManualDeploy"></a> Implementar manualmente atualizações de software  

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

 Uma implantação de atualização de software manual é o processo de selecionar atualizações de software do console do Configuration Manager e iniciar manualmente o processo de implantação. Ou, pode adicionar atualizações de software selecionadas a um grupo de atualizações e, em seguida, implementar manualmente o grupo de atualizações. Normalmente, utilizará a implementação manual para atualizar os seus dispositivos cliente com atualizações de software necessárias antes de criar ADRs que irão gerir as implementações mensais de atualização de software em curso. Também utilizará um método manual para implementar atualizações de software fora de banda. Se você precisar de ajuda para determinar qual implantação método é ideal para você, consulte [implantar atualizações de software](deploy-software-updates.md).

 As seções a seguir fornecem as etapas para implantar manualmente atualizações de software.  

##  <a name="BKMK_1SearchCriteria"></a>Etapa 1: Especificar critérios de pesquisa para atualizações de software  
 Potencialmente, existem milhares de atualizações de software exibidas no console do Configuration Manager. O primeiro passo no fluxo de trabalho para implementar manualmente atualizações de software consiste em identificar as atualizações de software que pretende implementar. Por exemplo, pode fornecer critérios para obter todas as atualizações de software que são necessárias em mais de 50 dispositivos cliente e que têm uma classificação de atualização de software **Segurança** ou **Crítica** .  

> [!IMPORTANT]  
>  O número máximo de atualizações de software que podem ser incluídas numa única implementação de atualização de software é 1000.  

#### <a name="to-specify-search-criteria-for-software-updates"></a>Para especificar critérios de procura para atualizações de software  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho Biblioteca de Software, expanda **Atualizações de Software**e clique em **Todas as Atualizações de Software**. As atualizações de software sincronizadas são apresentadas.  

    > [!NOTE]  
    >  Sobre o **todas as atualizações de Software** nó, o Configuration Manager exibe somente atualizações de software com um **crítico** e **segurança** classificação e que foram liberadas nos últimos 30 dias.  

3.  No painel de procura, filtre para identificar as atualizações de software de que necessita, utilizando um ou ambos dos seguintes passos:  

    -   Na caixa de texto de pesquisa, escreva uma cadeia de procura que irá filtrar as atualizações de software. Por exemplo, escreva o ID do artigo ou o ID do boletim para uma atualização de software específica ou introduza uma cadeia que aparecerá no título de diversas atualizações de software.  

    -   Clique em **Adicionar Critérios**, selecione os critérios que pretende utilizar para filtrar atualizações de software, clique em **Adicionar**e forneça os valores para os critérios.  

4.  Clique em **Procurar** para filtrar as atualizações de software.  

    > [!TIP]  
    >  Tem a opção de guardar os critérios do filtro no separador **Procurar** e no grupo **Guardar** .  

##  <a name="BKMK_2UpdateGroup"></a>Etapa 2: Criar um grupo de atualização de software que contém as atualizações de software  
 Os grupos de atualizações de software fornecem um método eficaz para organizar as atualizações de software em preparação para implementação. Você pode adicionar manualmente atualizações de software a um grupo de atualização de software ou o Configuration Manager podem adicionar automaticamente as atualizações de software a um grupo de atualização de software novo ou existente usando uma ADR. Utilize os seguintes procedimentos para adicionar manualmente atualizações de software a um novo grupo de atualizações de software.  

#### <a name="to-manually-add-software-updates-to-a-new-software-update-group"></a>Para adicionar manualmente atualizações de software a um novo grupo de atualizações de software  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho Biblioteca de Software, clique em **Atualizações de Software**.  

3.  Selecione as atualizações de software que pretende adicionar ao novo grupo de atualização de software.  

4.  No separador **Home Page** , no grupo **Atualizar** , clique em **Criar Grupo de Atualização de Software**.  

5.  Especifique o nome para o grupo de atualizações de software e, opcionalmente, forneça uma descrição. Utilize um nome e uma descrição que forneçam informações suficientes para determinar qual o tipo de atualizações de software que fazem parte do grupo de atualizações de software. Para continuar, clique em **Criar**.  

6.  Clique no nó **Grupos de Atualização de Software** para apresentar o novo grupo de atualizações de software.  

7.  Selecione o grupo de atualização de software e, no separador **Home Page** , no grupo **Atualizar** , clique em **Mostrar Membros** para apresentar uma lista das atualizações de software que estão incluídas no grupo.  

##  <a name="BKMK_3DownloadContent"></a>Etapa 3: Baixar o conteúdo para o grupo de atualização de software  
 Opcionalmente, antes de implementar as atualizações de software, pode transferir o conteúdo para as atualizações de software que estão incluídas no grupo de atualizações de software. Pode escolher proceder desta forma para que possa verificar que o conteúdo está disponível nos pontos de distribuição antes de implementar as atualizações de software. Isto ajudará a evitar quaisquer problemas inesperados com o fornecimento de conteúdo. Pode ignorar este passo e o conteúdo será transferido e copiado para os pontos de distribuição como parte do processo de implementação. Utilize o seguinte procedimento para transferir o conteúdo para atualizações de software no grupo de atualizações de software.  



#### <a name="to-download-content-for-the-software-update-group"></a>Para transferir conteúdo para o grupo de atualizações de software
[!INCLUDE[downloadupdates](..\includes\downloadupdates.md)]
<!--- 1.  In the Configuration Manager console, click **Software Library**.  

2.  In the Software Library workspace, expand **Software Updates**, and click **Software Update Groups**.  

3.  Select the software update group for which you want to download content.  

4.  On the **Home** tab, in the **Update Group** group, click **Download**. The **Download Software Updates Wizard** opens.  

5.  On the **Deployment Package** page, configure the following settings:  

    1.  **Select deployment package**: Select this setting to use an existing deployment package for the software updates in the deployment.  

        > [!NOTE]  
        >  Software updates that have already been downloaded to the selected deployment package are not downloaded again.  

    2.  **Create a new deployment package**: Select this setting to create a new deployment package for the software updates in the deployment. Configure the following settings:  

        -   **Name**: Specifies the name of the deployment package. This must be a unique name that describes the package content. It is limited to 50 characters.  

        -   **Description**: Specifies the description of the deployment package. The package description provides information about the package contents and is limited to 127 characters.  

        -   **Package source**: Specifies the location of the software update source files.  Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  

            > [!NOTE]  
            >  The deployment package source location that you specify cannot be used by another software deployment package.  

            > [!IMPORTANT]  
            >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  

            > [!IMPORTANT]  
            >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  

     Click **Next**.  

6.  On the Distribution Points page, select the distribution points or distribution point groups that are used to host the software update files defined in the new deployment package, and then click **Next**.  

7.  On the Distribution Settings page, specify the following settings:  

    -   **Distribution priority**: Use this setting to specify the distribution priority for the deployment package. The distribution priority applies when the deployment package is sent to distribution points at child sites. Distribution packages are sent in priority order: **High**, **Medium**, or **Low**. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority. By default, packages are sent using **Medium** priority.  

    -   **Distribute the content for this package to preferred distribution points**: Use this setting to enable on-demand content distribution to preferred distribution points. When this setting is enabled, the management point creates a trigger for the distribution manager to distribute the content to all preferred distribution points when a client requests the content for the package and the content is not available on any preferred distribution points. For more information about preferred distribution points and on-demand content, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  

    -   **Prestaged distribution point settings**: Use this setting to specify how you want to distribute content to prestaged distribution points. Choose one of the following options:  

        -   **Automatically download content when packages are assigned to distribution points**: Use this setting to ignore the prestage settings and distribute content to the distribution point.  

        -   **Download only content changes to the distribution point**: Use this setting to prestage the initial content to the distribution point, and then distribute content changes to the distribution point.  

        -   **Manually copy the content in this package to the distribution point**: Use this setting to always prestage content on the distribution point. This is the default setting.  

         For more information about prestaging content to distribution points, see [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

     Click **Next**.  

8.  On the Download Location page, specify location that Configuration Manager will use to download the software update source files. As needed, use the following options:  

    -   **Download software updates from the Internet**: Select this setting to download the software updates from the location on the Internet. This is the default setting.  

    -   **Download software updates from a location on the local network**: Select this setting to download software updates from a local folder or shared network folder. Use this setting when the computer running the wizard does not have Internet access.  

        > [!NOTE]  
        >  When you use this setting, download the software updates from any computer with Internet access, and then copy the software updates to a location on the local network that is accessible from the computer running the wizard.  

     Click **Next**.  

9. On the Language Selection page, specify the languages for which the selected software updates are to be downloaded, and then click **Next**. Configuration Manager downloads the software updates only if they are available in the selected languages. Software updates that are not language-specific are always downloaded.  

10. On the Summary page, verify the settings that you selected in the wizard, and then click **Next** to download the software updates.  

11. On the Completion page, verify that the software updates were successfully downloaded, and then click **Close**. --->

#### <a name="to-monitor-content-status"></a>Para monitorizar o estado do conteúdo
1. Para monitorar o status do conteúdo das atualizações de software, clique em **monitoramento** no console do Configuration Manager.  

2. Na área de trabalho Monitorização, expanda **Estado da Distribuição**e clique em **Estado do Conteúdo**.  

3. Selecione o pacote de atualização de software que identificou anteriormente para transferir as atualizações de software do grupo de atualização de software.  

4. No separador **Home Page** , no grupo **Conteúdo** , clique em **Ver Estado**.  

##  <a name="BKMK_4DeployUpdateGroup"></a>Etapa 4: Implantar o grupo de atualização de software  
 Após identificar as atualizações de software que tenciona implementar e adicioná-las a um grupo de atualização de software, poderá implementar manualmente as atualizações de software do grupo de atualização de software. Utilize o seguinte procedimento para implementar manualmente as atualizações de software de um grupo de atualização de software.  

#### <a name="to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Para implementar manualmente as atualizações de software de um grupo de atualização de software  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho Biblioteca de Software, expanda **Atualizações de Software**e clique em **Grupos de Atualização de Software**.  

3.  Selecione o grupo de atualização de software que pretende implementar.  

4.  No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**. É aberto o **Assistente de Implementação de Atualização de Software** .  

5.  Na página Geral, configure as seguintes definições:  

    -   **Nome**: Especifique o nome para a implantação. A implantação deve ter um nome exclusivo que descreva a finalidade da implantação e diferencie-a de outras implantações no site do Configuration Manager. Por padrão, o Configuration Manager fornece automaticamente um nome para a implantação no seguinte formato: **Atualizações de Software da Microsoft -** <*data*><*tempo*>  

    -   **Descrição**: Especifique uma descrição para a implantação. A descrição fornece uma visão geral da implementação e qualquer outra informação relevante que ajude a identificar e diferenciar a implantação, entre outras no site do Configuration Manager. O campo de descrição é opcional, tem um limite de 256 caracteres e está em branco por predefinição.  

    -   **Grupo de atualização de Software/atualização de software**: Verifique se o grupo de atualização de software exibido ou a atualização de software está correta.  

    -   **Selecione o modelo de implantação**: Especifique se deseja aplicar um modelo de implantação salvo anteriormente. Pode configurar um modelo de implementação para incluir várias propriedades comuns de implementação de atualizações de software e, em seguida, aplicar o modelo para implementar atualizações de software subsequentes com a garantia de consistência entre implementações semelhantes e poupança de tempo.  

    -   **Coleção**: Especifique a coleção para a implantação, conforme aplicável. Os membros da coleção recebem as atualizações de software definidas na implementação.  

6.  Na página Definições de Implementação, configure as seguintes definições:  

    -   **Tipo de implantação**: Especifique o tipo de implantação para a implantação de atualização de software. Selecione **Necessário** para criar uma implementação de atualização de software obrigatória através da qual as atualizações de software são automaticamente instaladas nos clientes antes de um prazo de instalação configurado. Selecione **Disponível** para criar uma implementação de atualização de software opcional que estará disponível para ser instalada pelos utilizadores a partir do Centro de Software.  

        > [!IMPORTANT]  
        >  Após criar a implementação de atualização de software, não poderá alterar o tipo de implementação mais tarde.  

        > [!NOTE]  
        >  Um grupo de atualização de software implementado como **Obrigatório** será transferido em segundo plano e irá cumprir as definições de BITS, se estiverem configuradas.  
        > No entanto, os grupos de atualização de software implementados como **Disponível** serão transferidos em primeiro plano e irão ignorar as definições de BITS.  

    -   **Usar Wake-on-LAN para ativar clientes para implantações obrigatórias**: Especifique se deseja habilitar o Wake On LAN no prazo para enviar pacotes de ativação para computadores que exigem uma ou mais atualizações de software na implantação. Todos os computadores que se encontrarem no modo de suspensão na data limite de instalação serão reativados de modo a dar início à instalação da atualização de software. Os clientes que se encontrem no modo de suspensão e que não necessitem de quaisquer atualizações de software no âmbito da implementação não serão iniciados. Por predefinição, esta definição não está ativada e só estará disponível se **Tipo de implementação** estiver definido como **Necessário**.  

        > [!WARNING]  
        >  Para poder utilizar esta opção, os computadores e redes terão de estar configurados para Reativação por LAN.  

    -   **Nível de detalhe**: Especifique o nível de detalhe para as mensagens de estado são relatadas pelos computadores cliente.  

7.  Na página Agendamento, configure as seguintes definições:  

    -   **Avaliação do agendamento**: Especifique se o tempo disponível e os prazos de instalação são avaliados de acordo com a UTC ou horário local do computador que executa o console do Configuration Manager.  

        > [!NOTE]  
        >  Quando você seleciona a hora local e, em seguida, selecione **assim que possível** para o **tempo disponível do Software** ou **prazo de instalação**, a hora atual no computador que executa o console do Configuration Manager é usado para avaliar quando as atualizações estiverem disponíveis ou quando eles são instalados em um cliente. Se o cliente tiver um fuso horário diferente, estas ações irão ocorrer quando a hora do cliente corresponder à hora de avaliação.  

    -   **Tempo disponível do software**: Selecione uma das configurações a seguir para especificar quando as atualizações de software estarão disponíveis aos clientes:  

        -   **Assim que possível**: Selecione esta configuração para disponibilizar as atualizações de software na implantação aos clientes assim que possível. Quando a implementação é criada, a política de cliente é atualizada, os clientes são notificados sobre a implementação durante o respetivo ciclo seguinte de consulta de política de cliente e, em seguida, as atualizações de software são disponibilizadas para instalação.  

        -   **Horário específico**: Selecione esta configuração para disponibilizar as atualizações de software na implantação aos clientes em uma determinada data e hora. Quando a implementação é criada, a política de cliente é atualizada e os clientes são notificados da implementação durante o respetivo ciclo seguinte de consulta de política de cliente. No entanto, as atualizações de software da implementação não estarão disponíveis para instalação antes da data e hora especificadas.  

    -   **Prazo de instalação**: Selecione uma das configurações a seguir para especificar o prazo de instalação das atualizações de software na implantação.  

        > [!NOTE]  
        >  Só pode configurar a definição do prazo de instalação se **Tipo de implementação** estiver definido como **Necessário** na página Definições de Implementação.  

        -   **Assim que possível**: Selecione esta configuração para instalar automaticamente as atualizações de software na implantação assim que possível.  

        -   **Horário específico**: Selecione esta configuração para instalar automaticamente as atualizações de software na implantação em uma data e hora específicas.  

        > [!NOTE]  
        >  O prazo instalação real corresponderá à hora específica que configurar, acrescida de um período de tempo aleatório de até 2 horas. Desta forma, reduzirá o impacto potencial da instalação das atualizações de software da implementação ao mesmo tempo em todos os computadores cliente da coleção de destino.  
        >   
        >  Pode configurar a definição de cliente **Agente do Computador** , **Desativar a aleatoriedade de prazos** para desativar o atraso de aleatoriedade da instalação para as atualizações de software necessárias. Para obter mais informações, veja [Agente do Computador](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8.  Na página Experiência de Utilizador, configure as seguintes definições:  

    -   **Notificações de usuário**: Especifique se deseja exibir notificações das atualizações de software no Centro de Software no computador cliente no configurado **tempo disponível do Software** e se deseja exibir as notificações de usuário nos computadores cliente. Se **Tipo de implementação** estiver definido como **Disponível** na página Definições de Implementação, não poderá selecionar **Ocultar no Centro de Software e em todas as notificações**.  

    -   **Comportamento do prazo**: * disponível apenas quando **tipo de implantação** * é definido como **necessário** *na página Configurações de implantação.*   
    Especifique o comportamento que deve ocorrer quando o prazo é alcançado para a implantação de atualização de software. Especifique se pretende instalar as atualizações de software da implementação. Especifique também se pretende reiniciar o sistema após a instalação da atualização de software, independentemente de uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção, consulte [como usar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento de reinício de dispositivo**: * disponível apenas quando **tipo de implantação** * é definido como **necessário** *na página Configurações de implantação.*    
    Especifique se deseja suprimir uma reinicialização do sistema em servidores e estações de trabalho depois que as atualizações de software são instaladas e uma reinicialização do sistema é necessária para concluir a instalação.  

        > [!IMPORTANT]  
        >  A supressão dos reinícios de sistema pode ser útil em ambientes de servidor ou em casos em que não pretenda que os computadores que instalam as atualizações de software sejam reiniciados por predefinição. No entanto, este método pode deixar os computadores num estado não seguro, enquanto que um reinício forçado ajudará a assegurar a conclusão imediata da instalação da atualização de software.

    -   **Tratamento de dispositivos Windows Embedded com filtro de gravação**: Quando você implanta atualizações de software para dispositivos Windows Embedded habilitados com filtro de gravação, você pode especificar para instalar a atualização de software na sobreposição temporária e que as alterações sejam confirmação mais tarde ou confirmar as alterações no prazo da instalação ou durante uma janela de manutenção. Ao consolidar alterações no momento da instalação ou durante uma janela de manutenção, será necessário um reinício para que as alterações sejam mantidas no dispositivo.  

        > [!NOTE]  
        >  Ao implementar uma atualização de software num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada.  

    - **Comportamento de reavaliação de implantação após a reinicialização de atualizações de software**: A partir do Configuration Manager versão 1606, selecione essa configuração para configurar implantações de atualizações de software para que os clientes executem uma verificação de conformidade de atualizações de software imediatamente depois que um cliente instala o software de atualizações e reinicia. Isto permite ao cliente verificar a existência de atualizações de software adicionais que se tornam aplicáveis após o cliente ser reiniciado e, em seguida, instalá-las (e ficam em conformidade) durante a mesma janela de manutenção.

9. Na página alertas, configure como Configuration Manager e o System Center Operations Manager irão gerar alertas para essa implantação. Só poderá configurar alertas quando o **Tipo de implementação** está definido como **Necessário** na página Definições de Implementação.  

    > [!NOTE]  
    >  Pode rever os alertas de atualizações de software recentes a partir do nó **Atualizações de Software** da área de trabalho **Biblioteca de Software** .  

10. Na página Definições de Transferência, configure as seguintes definições:  

    - Especifique se o cliente irá transferir e instalar as atualizações de software quando estiver ligado a uma rede lenta ou estiver a utilizar uma localização de conteúdos de contingência.  

    - Especifique se pretende que o cliente transfira e instale as atualizações de software a partir de um ponto de distribuição de contingência quando o conteúdo das atualizações de software não estiver disponível num ponto de distribuição preferencial.  

    - **Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede**: Especifique se deseja habilitar o uso do BranchCache para downloads de conteúdo. Para obter mais informações sobre o BranchCache, consulte [os conceitos fundamentais do gerenciamento de conteúdo](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Se as atualizações de software não estão disponíveis no ponto de distribuição no atual, vizinho ou site grupos, fazer download de conteúdo de Microsoft Updates**: Selecione esta configuração para os clientes que estão conectados para as intranet devem baixar atualizações de software do Microsoft Update se as atualizações de software não estão disponíveis nos pontos de distribuição. Clientes baseados na Internet sempre podem ir para o Microsoft Update para o conteúdo de atualizações de software.

    - Especifique se pretende permitir que os clientes efetuem a transferência após um prazo de instalação se estiverem a utilizar ligações à Internet com tráfego limitado. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à Internet com tráfego limitado.  

    > [!NOTE]  
    >  Os clientes solicitam a localização de conteúdo a partir de um ponto de gestão para as atualizações de software de uma implementação. O comportamento de transferência dependerá do modo como tiver configurado o ponto de distribuição, o pacote de implementação e as definições nesta página. Para obter mais informações, veja [Cenários de localização da origem de conteúdo](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. Se você executou [etapa 3: Baixar o conteúdo para o grupo de atualização de software](#BKMK_3DownloadContent), as páginas pacote de implantação, pontos de distribuição e seleção de idioma não são exibidas, e você pode ignorar a etapa 15 do assistente.  

    > [!IMPORTANT]  
    >  As atualizações de software que tenham sido anteriormente transferidas para a biblioteca de conteúdos do servidor do site não serão transferidas novamente. Tal não acontecerá, mesmo que crie um novo pacote de implementação para as atualizações de software. Se já tiverem sido transferidas anteriormente todas as atualizações de software, o assistente avançará para a página **Seleção de Idioma** (passo 15).  

12. Na página Pacote de Implementação, selecione um pacote de implementação existente ou configure as seguintes definições para especificar um novo pacote de implementação:  

    1.  **Nome**: Especifique o nome do pacote de implantação. Tem de ser um nome exclusivo que descreva o conteúdo do pacote. Está limitado a 50 carateres.  

    2.  **Descrição**: Especifique uma descrição que fornece informações sobre o pacote de implantação. A descrição está limitada a 127 caracteres.  

    3.  **Origem do pacote**: Especifique o local dos arquivos de origem de atualização de software.  Escreva um caminho de rede para a localização de origem, como, por exemplo, **\\\server\sharename\path**ou clique em **Procurar** para procurar a localização de rede. Antes de continuar para a página seguinte, terá de criar a pasta partilhada para os ficheiros de origem do pacote de implementação.  

        > [!NOTE]  
        >  A localização de origem do pacote de implementação que especificar não poderá ser utilizada por outro pacote de implementação de software.  

        > [!IMPORTANT]  
        >  Tanto a conta de computador do Fornecedor de SMS, como o utilizador que executar o assistente para transferir as atualizações de software, têm de ter permissões NTFS de **Escrita** na localização de transferência. Deverá restringir cuidadosamente o acesso à localização de transferência para reduzir o risco de adulteração dos ficheiros de origem de atualização de software por parte de atacantes.  

        > [!IMPORTANT]  
        >  Você pode alterar o local de origem do pacote nas propriedades do pacote de implantação depois que o Configuration Manager cria o pacote de implantação. Mas se o fizer, terá primeiro de copiar o conteúdo da origem inicial do pacote para a nova localização de origem do pacote.  

    4.  **Prioridade de envio**: Especifique a prioridade de envio do pacote de implantação. Configuration Manager usa a prioridade de envio do pacote de implantação quando envia o pacote para pontos de distribuição. Pacotes de implantação são enviados na ordem de prioridade: Alta, média ou baixa. Os pacotes com prioridades idênticas são enviados pela ordem em que foram criados. Se não existirem tarefas pendentes, o pacote será processado de imediato, independentemente da sua prioridade.  

13. Na página Pontos de Distribuição, especifique os pontos de distribuição ou grupos de pontos de distribuição que irão alojar os ficheiros de atualização de software. Para obter mais informações sobre os pontos de distribuição, veja [Configurações de pontos de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

14. Na página Localização de Transferência, especifique se pretende transferir os ficheiros de atualização de software a partir da Internet ou da rede local. Configure as seguintes definições:  

    -   **Baixar atualizações de software da Internet**: Selecione esta configuração para baixar as atualizações de software de um local específico na Internet. Esta definição está ativada por predefinição.  

    -   **Baixar atualizações de software de um local na rede local**: Selecione esta configuração para baixar as atualizações de software de uma pasta local ou uma pasta de rede compartilhada. Esta definição é útil se o computador que executa o assistente não tiver acesso à Internet. As atualizações de software serão provisoriamente transferidas a partir de qualquer computador que tenha acesso à Internet e armazenadas numa localização da rede local para posterior acesso para efeitos de instalação.  

15. Na página Seleção de Idioma, selecione os idiomas para os quais serão transferidas as atualizações de software selecionadas. As atualizações de software apenas são transferidas se estiverem disponíveis nos idiomas selecionados. As atualizações de software que não sejam específicas do idioma serão sempre transferidas. Por predefinição, o assistente seleciona os idiomas que tiver configurado nas propriedades do ponto de atualização de software. Terá de estar selecionado pelo menos um idioma para que possa prosseguir para a página seguinte. Se selecionar apenas idiomas que não sejam suportados por uma atualização de software, a transferência da atualização de software não será concluída com êxito.  

16. Reveja as definições na página Resumo. Para guardar as definições num modelo de implementação, clique em **Guardar Como Modelo**, introduza um nome, selecione as definições que pretende incluir no modelo e, em seguida, clique em **Guardar**. Para alterar uma definição configurada, clique na página do assistente associada e altere a definição.  

    > [!WARNING]  
    >  O nome do modelo pode incluir carateres ASCII alfanuméricos, bem como **\\** (barra invertida) ou **‘** (plica).  

17. Clique em **Seguinte** para implementar a atualização de software.  

 Depois de concluir o assistente, o Configuration Manager downloads de atualizações de software para a biblioteca de conteúdo no servidor do site, distribui as atualizações de software para os pontos de distribuição configurados e depois implanta o software atualizar grupo para clientes na coleção de destino. Para obter mais informações sobre o processo de implementação, veja [Processo de implementação de atualizações de software](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Passos seguintes
[Monitorizar atualizações de software](monitor-software-updates.md)


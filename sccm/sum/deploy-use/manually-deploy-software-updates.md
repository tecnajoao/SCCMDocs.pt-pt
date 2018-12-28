---
title: Implementar manualmente atualizações de software
titleSuffix: Configuration Manager
description: Crie manualmente as implementações de software para obter os seus clientes atualizados com atualizações de software necessárias, ou para implementar atualizações fora de banda.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: aae0951ddf32ce1d58a29b034acef96b55ab85a0
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53414808"
---
# <a name="manually-deploy-software-updates"></a>Implementar manualmente atualizações de software  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma implementação de atualização de manual software é o processo de selecionar atualizações de software a partir da consola do Configuration Manager e iniciar manualmente o processo de implantação. Ou adicionar atualizações de software selecionadas a um grupo de atualização e, em seguida, implementar manualmente o grupo de atualizações. Geralmente usa as implementações manuais para obter os seus clientes atualizados com atualizações de software necessárias. Em seguida, utilizar regras de implementação automática (ADR) para gerir implementações de atualização de software mensais em curso. Utilize também este método manual para implementar atualizações de software fora de banda. Para obter mais informações sobre qual implementação método é adequado para si, consulte [implementar atualizações de software](deploy-software-updates.md).



##  <a name="BKMK_1SearchCriteria"></a> Passo 1: Especificar critérios de procura para atualizações de software  

Consoante as combinações de produtos e classificações que sincroniza o seu site, existem potencialmente milhares de atualizações de software apresentadas na consola do Configuration Manager. O primeiro passo no fluxo de trabalho para implementar manualmente atualizações de software consiste em identificar as atualizações de software que pretende implementar. Por exemplo, Mostrar todas as atualizações de software necessárias em mais de 50 dispositivos de cliente com um **Security** ou **crítico** classificação.  

> [!IMPORTANT]  
>  Uma implementação de atualização de software tem um limite de 1000 atualizações de software.  

### <a name="process-to-specify-search-criteria-for-software-updates"></a>Processo para especificar critérios de pesquisa para atualizações de software  

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **atualizações de Software**e clique em **todas as atualizações de Software**. Este nó apresenta todas as atualizações de software sincronizadas.  

    > [!NOTE]  
    >  O **todas as atualizações de Software** nó apresenta apenas atualizações de software com uma **crítico** e **segurança** classificação que tenham sido publicadas nos últimos 30 dias.  

2.  No painel de pesquisa, filtre para identificar as atualizações de software que precisa. Utilize uma ou ambas das seguintes opções:  

    -   Na caixa de texto de pesquisa, escreva uma cadeia de pesquisa que filtra as atualizações de software. Por exemplo, escreva o artigo ou ID do boletim para uma atualização de software. Ou introduza uma cadeia de caracteres que aparece no título de diversas atualizações de software.  

    -   Clique em **adicionar critérios**e selecione os critérios para filtrar atualizações de software. Clique em **adicionar**e, em seguida, forneça os valores para os critérios.  

3.  Clique em **Procurar** para filtrar as atualizações de software.  

    > [!TIP]  
    >  Guarde os critérios de filtro utilizados com frequência. No Friso, clique na opção para **guardar pesquisa atual**. Obter pesquisas anteriores ao clicar em **pesquisas guardadas**.   



##  <a name="BKMK_2UpdateGroup"></a> Passo 2: Criar um grupo de atualização de software que contém as atualizações de software   

Grupos de atualização de software permitem-lhe organizar as atualizações de software em preparação para implantação. Utilize o procedimento seguinte para adicionar manualmente atualizações de software a um novo grupo de atualização de software.  

### <a name="process-to-manually-add-software-updates-to-a-new-software-update-group"></a>Processo para adicionar manualmente atualizações de software a um novo grupo de atualização de software  

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho e selecione **atualizações de Software**. Selecione as atualizações de software pretendido.  

2.  Clique em **criar grupo de atualizações de Software** na faixa de opções.  

3.  Especifique o nome para o grupo de atualizações de software e, opcionalmente, forneça uma descrição. Utilize um nome e descrição que forneçam informações suficientes para que possa determinar que tipo de atualizações estão no grupo de atualização de software. Clique em **Criar**.  

4.  Selecione o **grupos de atualização de Software** nó e selecione o novo grupo de atualização de software. Para ver a lista de atualizações do grupo, clique em **Mostrar membros** na faixa de opções.  



##  <a name="BKMK_3DownloadContent"></a> Passo 3: Transferir o conteúdo para o grupo de atualizações de software  

Antes de implementar as atualizações de software, transferir o conteúdo para as atualizações de software no grupo de atualização de software. Este passo permite-lhe verificar que o conteúdo está disponível nos pontos de distribuição antes de implementar as atualizações de software. Ele também ajuda a evitar quaisquer problemas inesperados com a distribuição de conteúdo. Se ignorar este passo, como parte do processo de implantação o site transfere o conteúdo e distribui para os pontos de distribuição. Utilize o seguinte procedimento para transferir o conteúdo para atualizações de software no grupo de atualizações de software.  


### <a name="process-to-download-content-for-the-software-update-group"></a>Processo para transferir conteúdo para o grupo de atualizações de software
[!INCLUDE [downloadupdates](../includes/downloadupdates.md)]

### <a name="process-to-monitor-content-status"></a>Processo para monitorizar o estado do conteúdo
1. Para monitorizar o estado do conteúdo das atualizações de software, vá para o **monitorização** área de trabalho na consola do Configuration Manager. Expanda **estado de distribuição**e, em seguida, selecione a **estado do conteúdo** nó.  

2. Selecione o pacote de atualização de software que identificou anteriormente para transferir as atualizações de software do grupo de atualização de software.  

3. Clique em **ver o estado** na faixa de opções.  



##  <a name="BKMK_4DeployUpdateGroup"></a> Passo 4: Implementar o grupo de atualização de software  

Depois de determinar as atualizações que pretende implementar e adicioná-los a um grupo de atualização de software, implemente manualmente o grupo de atualizações de software.  

### <a name="process-to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Processo para implementar manualmente as atualizações de software de um grupo de atualização de software  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **atualizações de Software**e selecione o **grupos de atualização de Software** nó.  

2. Selecione o grupo de atualização de software que pretende implementar. Clique em **Deploy** na faixa de opções.   

3. Sobre o **gerais** página do Assistente de atualizações de Software implementar, configurar as seguintes definições:  

   -   **Nome**: Especifique o nome para a implementação. A implementação tem de ter um nome exclusivo que descreve a sua finalidade e distinga de outras implementações do site. Este campo de nome tem um limite de 256 carateres. Por predefinição, o Configuration Manager disponibiliza automaticamente um nome para a implementação no seguinte formato: `Microsoft Software Updates - YYYY-MM-DD <time>`  

   -   **Descrição**: Especifique uma descrição para a implementação. A descrição é opcional, mas fornece uma descrição geral da implantação. Inclua outras informações relevantes que ajudem a identificar e diferenciá-lo entre outras, no site. O campo de descrição tem um limite de 256 carateres e tem um valor em branco por predefinição.  

   -   **Grupo de atualizações de Software/atualização de software**: Certifique-se de que o grupo de atualização de software apresentados ou atualização de software está correta.  

   -   **Selecione o modelo de implementação**: Especifique se pretende aplicar um modelo de implementação anteriormente guardado. Configure um modelo de implementação para guardar as propriedades de implementação de atualização de software comuns. Em seguida, aplica o modelo ao implementar atualizações de software no futuro. Estes modelos economizar tempo e ajudam a garantir a consistência entre implementações semelhantes.  

   -   **Coleção**: Especifique a coleção para a implementação. Dispositivos da coleção recebem as atualizações de software nesta implementação.  

4. Sobre o **definições de implementação** página, configure as seguintes definições:  

   -   **Tipo de implementação**: Especifique o tipo de implementação para a implementação de atualização de software.  

       > [!IMPORTANT]  
       >  Depois de criar a implementação de atualização de software, não é possível alterar o tipo de implementação.  

        - Selecione **necessário** para criar uma implementação de atualização de software obrigatórias. As atualizações de software são automaticamente instaladas nos clientes antes do prazo de instalação que configurar.  

        - Selecione **disponível** para criar uma implementação de atualização de software opcional. Esta implementação está disponível para os usuários instalem a partir do Centro de Software.  

       > [!NOTE]  
       >  Ao implementar um grupo de atualização de software como **necessário**, os clientes transferir o conteúdo em segundo plano e irá cumprir as definições de BITS, se configurado.  
       > 
       > Para atualização de software implementados como de grupos **disponível**, os clientes transfiram conteúdos em primeiro plano e ignorar as definições de BITS.  

   -   **Usar o Wake-on-LAN para reativar os clientes para as implementações necessárias**: Especifica se pretende ativar a reativação por LAN na data limite. Reativação por LAN envia pacotes de reativação para computadores que necessitem de uma ou mais atualizações de software na implementação. O site é reativado por todos os computadores que estejam no modo de suspensão quando for atingido o prazo de instalação, pelo que pode iniciar a instalação. Os clientes que estejam no modo de suspensão e que não necessitam de quaisquer atualizações de software na implementação não são iniciados. Por predefinição, esta definição não está ativada. Só está disponível para **necessário** implementações. Antes de utilizar esta opção, configure computadores e redes para reativação por LAN. Para obter mais informações, consulte [como configurar a reativação por LAN](/sccm/core/clients/deploy/configure-wake-on-lan).  

   -   **Nível de detalhe**: Especifique o nível de detalhe para as mensagens de estado que os clientes reportam ao site.  

5. Sobre o **agendamento** página, configure as seguintes definições:  

   -   **Avaliação da agenda**: Especifique o tempo que o Configuration Manager avalia o tempo disponível e o prazo de instalação. Opte por utilizar Hora Universal Coordenada (UTC) ou na hora local do computador que executa a consola do Configuration Manager.  

       - Quando seleciona **hora local do cliente** aqui e, em seguida, selecione **logo que possível** para o **hora de disponibilização do Software**, a hora atual no computador com o Consola do Configuration Manager é utilizada para avaliar se as atualizações estiverem disponíveis. Este comportamento é o mesmo com o **prazo de instalação** e a hora quando as atualizações são instaladas num cliente. Se o cliente estiver num fuso horário diferente, estas ações ocorrem quando a hora do cliente atinge o tempo de avaliação.  

   -   **Hora de disponibilização do software**: Selecione uma das seguintes definições para especificar quando as atualizações de software são disponibilizadas aos clientes:  

       -   **Assim que possível**: Disponibiliza as atualizações de software na implementação aos clientes logo que possível. Quando criar a implementação com esta definição selecionada, o Configuration Manager atualiza a política de cliente. A política de cliente próximo ciclo de consulta, os clientes estarão informados da implementação e as atualizações de software estão disponíveis para instalação.  

       -   **Hora específica**: Torna as atualizações de software incluídas na implementação aos clientes numa data e hora específicas. Quando criar a implementação com esta definição ativada, o Configuration Manager atualiza a política de cliente. A política de cliente próximo ciclo de consulta, os clientes estarão informados da implementação. No entanto, as atualizações de software na implementação não estão disponíveis para instalação após a data e hora configuradas.  

   -   **Prazo de instalação**: Estas opções só estão disponíveis para **necessário** implementações. Selecione uma das seguintes definições para especificar o prazo de instalação das atualizações de software da implementação  

       -   **Assim que possível**: Selecione esta definição para instalar automaticamente as atualizações de software na implementação logo que possível.  

       -   **Hora específica**: Selecione esta definição para instalar automaticamente as atualizações de software da implementação numa hora e data específicas.  

           - O prazo da instalação real é apresentada acrescida além de um período de tempo aleatório de até duas horas. O recurso aleatório reduz o impacto potencial de clientes na coleção de instalação de atualizações na implementação ao mesmo tempo.   

           - Para desativar o atraso de aleatoriedade da instalação de atualizações de software necessárias, configure o definição de cliente **desativar a aleatoriedade de prazos** no **agente do computador** grupo. Para obter mais informações, consulte [definições do agente do computador cliente](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

   -  **Trasar imposição para esta implementação, de acordo com as preferências do usuário, até o período de tolerância definido nas definições de cliente**: Ative esta definição dar aos utilizadores mais tempo para instalar atualizações de software necessárias para além do prazo.  

       - Este comportamento é normalmente exigido quando um computador estiver desativado para muito tempo e tem de instalar várias atualizações de software ou aplicativos. Por exemplo, quando um usuário retorna de férias, têm de aguardar por muito tempo, pois o cliente instala implementações em atraso.  

       - Configure este período de tolerância com a propriedade **período de tolerância para a imposição de após a implementação do prazo (horas)** nas definições do cliente. Para obter mais informações, consulte a [agente do computador](/sccm/core/clients/deploy/about-client-settings#computer-agent) secção. O período de tolerância de imposição aplica-se a todas as implementações com esta opção ativada e direcionadas para dispositivos em que implementou também a definição de cliente.  

       - Após o prazo, o cliente instala as atualizações de software na primeira janela não comerciais, que o utilizador configurado, até esse período de tolerância. No entanto, o utilizador ainda pode abrir o Centro de Software e instalar as atualizações de software em qualquer altura. Assim que o período de tolerância expirar, imposição reverte para o comportamento normal para implementações em atraso.  

6. Sobre o **experiência de utilizador** página, configure as seguintes definições:  

   -   **Notificações do utilizador**: Especifique se pretende apresentar a notificação no Centro de Software em configurada **hora de disponibilização do Software**. Esta definição controla se é necessário notificar os utilizadores nos computadores cliente. Para **disponível** implementações, não é possível selecionar a opção de **ocultar no Centro de Software e em todas as notificações**.  

   -   **Comportamento do prazo**: Esta definição só é configurável para **necessário** implementações. Especifica os comportamentos para quando o software atualizar implementação atingir o prazo de fora de quaisquer janelas de manutenção definida. As opções incluem se pretende instalar as atualizações de software e se pretende executar um sistema de reinício após a instalação. Para obter mais informações sobre janelas de manutenção, consulte [como utilizar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).  

   -   **Comportamento do reinício do dispositivo**: Esta definição só é configurável para **necessário** implementações. Especifique se pretende suprimir um reinício de sistema nos servidores e estações de trabalho se uma reinicialização é necessária para concluir a instalação da atualização.  

       > [!WARNING]  
       >  A supressão dos reinícios de sistema pode ser útil em ambientes de servidor, ou quando não quiser que os computadores de destino sejam reiniciados por predefinição. No entanto, este método pode deixar computadores num Estado não seguro. Permitir que um ajuda de reinício forçado garantir conclusão imediata da instalação de atualização de software.  

   -   **Processamento para dispositivos Windows Embedded do filtro de escrita**: Esta definição controla o comportamento de instalação em dispositivos Windows Embedded que estão ativados com um filtro de escrita. Escolha a opção para consolidar as alterações no prazo de instalação ou durante uma janela de manutenção. Quando seleciona esta opção, é necessário um reinício e as alterações sejam mantidas no dispositivo. Caso contrário, a atualização é instalada, aplicada na sobreposição temporária e confirmada posteriormente.  

       -  Ao implementar uma atualização de software num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada.  

   - **Comportamento de reavaliação de implementação após o reinício de atualizações de software**: Selecione esta definição para configurar as implementações de atualizações de software para que os clientes executem uma análise de compatibilidade de atualizações de software imediatamente após um cliente, instala as atualizações de software e reinicializações. Esta definição permite que o cliente Verifique a existência de atualizações adicionais que se tornam aplicáveis após o cliente é reiniciado, em seguida, instala-os durante a mesma janela de manutenção.  

7. Sobre o **alertas** página, configure a forma como o Configuration Manager gera alertas para esta implementação. Alertas do Configuration Manager de atualizações de software recente de revisão da **atualizações de Software** nó da **biblioteca de Software** área de trabalho. Se também estiver a utilizar o System Center Operations Manager, configure os seus alertas também. Apenas configurar alertas para **necessário** implementações.  

8. Sobre o **definições de transferência** página, configure as seguintes definições:  

    > [!NOTE]  
    >  Os clientes solicitam a localização de conteúdo a partir de um ponto de gestão para as atualizações de software de uma implementação. O comportamento de transferência dependerá de como configurou o ponto de distribuição, o pacote de implementação e as definições nesta página.  

    - Especifique se os clientes devem transferir e instalar as atualizações quando estiverem a utilizar um ponto de distribuição de um vizinho ou os grupos de limites de site padrão.  

    - Especifique se os clientes devem transferir e instalar as atualizações a partir de um ponto de distribuição no grupo de limite predefinido do site, quando o conteúdo para o software das atualizações não está disponível num ponto de distribuição no atual ou os grupos de limites de vizinho.  

    - **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**: Especifique se pretende ativar a utilização do BranchCache para transferências de conteúdos. Para obter mais informações, consulte [BranchCache](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#branchcache). A partir da versão 1802, BranchCache está sempre ativada nos clientes. Esta definição for removida, como os clientes utilizam o BranchCache, se o ponto de distribuição suportar.  

    - **Se as atualizações de software não estão disponíveis no ponto de distribuição na atual, vizinho ou do site de grupos de limite, transfira o conteúdo do Microsoft Updates**: Selecione esta definição para que os clientes ligados à intranet transferir atualizações de software do Microsoft Update, se as atualizações não estão disponíveis em pontos de distribuição. Clientes baseados na Internet sempre aceder ao Microsoft Update para atualizações de software, conteúdas.

    - Especifique se pretende permitir que os clientes transfiram após um prazo de instalação quando estiverem a utilizar de ligações à internet limitadas. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando estiver numa ligação limitada.  

9. Sobre o **pacote de implementação** página, selecione uma das seguintes opções:  

    > [!Note]  
    > Se já realizou [passo 3: Transferir o conteúdo para o grupo de atualizações de software](#BKMK_3DownloadContent), em seguida, o assistente não apresenta o **pacote de implementação**, **pontos de distribuição**, e **deseleçãodeidioma** páginas. Avance para o [resumo](#bkmk_summary) página do assistente.  
    > 
    >  Atualizações de software que tenham sido anteriormente transferidas para a biblioteca de conteúdos no servidor do site não são transferidas novamente. Este comportamento é verdadeiro, mesmo quando cria um novo pacote de implementação das atualizações de software. Se já tiverem sido transferidas todas as atualizações de software, o assistente avançará para a [resumo](#bkmk_summary) página.  

    - **Selecione um pacote de implementação**: Adicione estas atualizações a um pacote de implementação existente.  

    - **Criar um novo pacote de implementação**: Adicione estas atualizações para um novo pacote de implementação. Configure as seguintes definições adicionais:  

        -  **Nome**: Especifique o nome do pacote de implementação. Utilize um nome exclusivo que descreve o conteúdo do pacote. É limitado a 50 carateres.  

        -  **Descrição**: Especifique uma descrição que disponibilize informações sobre o pacote de implementação. A descrição opcional é limitada a 127 carateres.  

        -  **Origem do pacote**: Especifique a localização dos ficheiros de origem de atualização de software. Escreva um caminho de rede para a localização de origem, por exemplo, `\\server\sharename\path`, ou clique em **procurar** para procurar a localização de rede. Crie a pasta partilhada para os ficheiros de origem do pacote de implementação antes de continuar para a página seguinte.  

            - Não é possível utilizar a localização especificada como a fonte de outro pacote de implementação de software.  

            - Pode alterar a localização de origem do pacote nas propriedades do pacote de implementação depois do Configuration Manager cria o pacote de implementação. Se o fizer, primeiro copie o conteúdo da origem do pacote original para a nova localização de origem do pacote.  

            -  A conta de computador do fornecedor de SMS e o utilizador que está a executar o Assistente para transferir as atualizações de software terão de ter **escrever** permissões para a localização de transferência. Restringir o acesso à localização de transferência. Esta restrição reduz o risco dos atacantes adulterar os ficheiros de origem de atualização de software.  

        -  **Prioridade de envio**: Especifique a prioridade de envio para o pacote de implementação. O Configuration Manager utiliza essa prioridade quando envia o pacote para pontos de distribuição. Pacotes de implementação são enviados por ordem de prioridade: elevada, média ou baixa. Os pacotes com prioridades idênticas são enviados pela ordem em que foram criados. Se não houver nenhum registo de segurança, o pacote de processos imediatamente, independentemente de sua prioridade.  

        - **Ativar a replicação diferencial de binários**: Ative esta definição para minimizar o tráfego de rede entre sites. Replicação diferencial binária (BDR) apenas atualiza o conteúdo que foi alterado no pacote, em vez de atualizar o conteúdo do pacote inteiro. Para obter mais informações, consulte [replicação de diferencial binário](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#binary-differential-replication).  

    - **Nenhum pacote de implementação**: A partir da versão 1806, implemente atualizações de software em dispositivos sem primeiro baixar e distribuir conteúdo para pontos de distribuição. Esta definição é benéfica ao lidar com conteúdo da atualização extremamente grandes. Também usá-lo quando pretender que sempre clientes a obter o conteúdo do serviço de nuvem do Microsoft Update. Os clientes neste cenário também podem transferir o conteúdo de elementos que já tenham o conteúdo necessário. O cliente continua a gerir a transferência do conteúdo, o Configuration Manager, portanto, pode utilizar a funcionalidade de cache ponto a ponto do Configuration Manager ou outras tecnologias, como a Otimização da entrega. Esta funcionalidade suporta qualquer tipo de atualização suportado pela gestão de atualizações de software do Configuration Manager, incluindo o Windows e atualizações do Office.<!--1357933-->  

10. Sobre o **pontos de distribuição** página, especifique os pontos de distribuição ou grupos para alojar o software de ficheiros de atualização de ponto de distribuição. Para obter mais informações sobre os pontos de distribuição, veja [Configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_configs).  

    > [!Note]  
    > Se já realizou [passo 3: Transferir o conteúdo para o grupo de atualizações de software](#BKMK_3DownloadContent), em seguida, o assistente não apresenta o **pacote de implementação**, **pontos de distribuição**, e **deseleçãodeidioma** páginas. Avance para o [resumo](#bkmk_summary) página do assistente.  

11. Sobre o **localização de transferência** página, especifique se pretende transferir os ficheiros de atualização de software da internet ou da rede local. Configure as seguintes definições:  

    -   **Transferir atualizações de software a partir da internet**: Selecione esta definição para transferir as atualizações de software a partir de uma localização especificada na internet. Esta definição está ativada por predefinição.  

    -   **Transferir atualizações de software a partir de uma localização na rede local**: Selecione esta definição para transferir as atualizações de software a partir de um diretório local ou uma pasta compartilhada. Esta definição é útil quando o computador que executa o assistente não tem acesso à internet. Qualquer computador com acesso à internet provisoriamente pode transferir as atualizações de software. Em seguida, armazená-las numa localização na rede local que seja acessível ao computador que executa o assistente.  

12. Sobre o **seleção de idioma** , selecione os idiomas para o qual o site transfere as atualizações de software selecionadas. O site transfere apenas essas atualizações se elas estão disponíveis nos idiomas selecionados. Atualizações de software que não são específicas do idioma serão sempre transferidas. Por predefinição, o assistente seleciona os idiomas que configurou nas propriedades do ponto de atualização de software. Terá de estar selecionado pelo menos um idioma para que possa prosseguir para a página seguinte. Se selecionar apenas idiomas que não suporta uma atualização de software, o download falha para a atualização.  

    > [!Note]  
    > Se já realizou [passo 3: Transferir o conteúdo para o grupo de atualizações de software](#BKMK_3DownloadContent), em seguida, o assistente não apresenta o **pacote de implementação**, **pontos de distribuição**, e **deseleçãodeidioma** páginas. Avance para o [resumo](#bkmk_summary) página do assistente.  

13. <a name="bkmk_summary"></a> Sobre o **resumo** , reveja as definições. Para guardar as definições de um modelo de implementação, clique em **guardar como modelo**. Introduza um nome e selecione as definições que pretende incluir no modelo, em seguida, clique em **guardar**. Para alterar uma definição configurada, clique na página do assistente associada e altere a definição.  

    -  O nome do modelo pode consistir em carateres ASCII alfanuméricos, bem como `\` (barra invertida) ou `'` (plica).  

14. Clique em **Seguinte** para implementar a atualização de software.  

    Depois de concluir o assistente, o Configuration Manager transfere as atualizações de software para a biblioteca de conteúdos no servidor do site. Em seguida, distribui o conteúdo para pontos de distribuição configurados e implementa o grupo de atualizações de software a clientes da coleção de destino. Para obter mais informações sobre o processo de implementação, veja [Processo de implementação de atualizações de software](/sum/understand/software-updates-introduction#BKMK_DeploymentProcess).  



## <a name="next-steps"></a>Passos seguintes
[Monitorizar atualizações de software](monitor-software-updates.md)

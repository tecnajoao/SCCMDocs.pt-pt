---
title: Implementar automaticamente atualizações de software
titleSuffix: Configuration Manager
description: Implemente automaticamente atualizações de software ao utilizar regras de implementação automática (ADR).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 10/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.collection: M365-identity-device-management
ms.openlocfilehash: c42cfb2b973084efc897c8f313e58541164d3fa2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123489"
---
#  <a name="automatically-deploy-software-updates"></a>Implementar automaticamente atualizações de software  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize uma regra de implementação automática (ADR) em vez de adicionar novas atualizações a um grupo de atualização de software existente. Normalmente, utiliza ADRs para implementar atualizações de software mensais (também conhecido como atualizações de "Patch Terça") e para gerir atualizações de definições do Endpoint Protection. Se precisar de ajuda para determinar qual implementação de método é adequado para si, consulte [implementar atualizações de software](deploy-software-updates.md).


##  <a name="BKMK_CreateAutomaticDeploymentRule"></a> Criar uma regra de implementação automática (ADR)  
Aprovar e implementar atualizações de software utilizando uma ADR automaticamente. A regra pode adicionar atualizações de software a um novo grupo de atualização de software sempre que as execuções de regra ou adicionar atualizações de software a um grupo existente. Quando uma regra for executada e adiciona as atualizações de software a um grupo existente, a regra remove todas as atualizações do grupo. Em seguida, adiciona ao grupo as atualizações que cumprem os critérios definidos por si. 

> [!WARNING]  
>  Antes de criar uma ADR pela primeira vez, certifique-se de que o site foi concluída a sincronização de atualizações de software. Este passo é importante quando executa o Configuration Manager com um idioma diferente do inglês. Classificações de atualização de software são apresentadas em inglês antes da primeira sincronização e, em seguida, apresentadas nos idiomas localizados, após a conclusão da sincronização de atualizações de software. As regras que criar antes de sincronizar as atualizações podem não funcionar corretamente após a sincronização porque a cadeia de texto pode não corresponder de software.  


### <a name="bkmk_adr-process"></a> Processo para criar uma ADR  

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **atualizações de Software**e selecione o **regras de implementação automática** nó.  

2.  No Friso, clique em **criar regra de implementação automática**.  

3.  Sobre o **gerais** página de criar regra de Assistente de implementação automática, configure as seguintes definições:  

    -   **Nome**: Especifique o nome para a ADR. O nome tem de ser exclusivo, ajudam a descrever a finalidade da regra e identificá-la de outras pessoas no site do Configuration Manager.  

    -   **Descrição**: Especifique uma descrição para a ADR. A descrição deve fornecer uma visão geral da regra de implementação e outras informações relevantes que ajudem a distinguir a regra de outras pessoas. O campo de descrição é opcional, tem um limite de 256 caracteres e está em branco por predefinição.  

    -   **Modelo**: Selecione um modelo de implementação para especificar se pretende aplicar tinha guardado as configurações de regras de implementação automática. Configure um modelo de implementação que contém várias propriedades comuns de atualização de implementação que pode utilizar ao criar ADRs adicionais. Estes modelos economizar tempo e ajudam a garantir a consistência entre implementações semelhantes. Selecione a partir de um dos seguintes modelos de implementação de atualização de software incorporados:  

         - O modelo **Patch Terça** fornece definições comuns a utilizar quando implementa atualizações de software num ciclo mensal.  

         - O **atualizações de cliente do Office 365** modelo fornece definições comuns a utilizar ao implementar atualizações para os clientes do Office 365 Pro Plus.  

         - O **SCEP e atualizações de antivírus do Windows Defender** modelo fornece definições comuns a utilizar quando implementa atualizações de definições do Endpoint Protection.  

    -   **Coleção**: Especifica a coleção de destino a ser utilizada para a implementação. Os membros da coleção recebem as atualizações de software definidas na implementação.  

    -   Especifique se pretende adicionar atualizações de software a um grupo de atualização de software novo ou existente. Na maioria dos casos, optar por criar um novo grupo de atualização de software quando a execução da ADR. Se a regra é executada com base numa agenda mais agressiva, poderá optar por utilizar um grupo existente. Por exemplo, se executar a regra diariamente para atualizações de definições, pode adicionar as atualizações de software a um grupo de atualização de software existente.  

    -   **Ativar a implementação após a execução desta regra**: Especifique se pretende ativar a implementação de atualização de software após a execução da ADR. Considere as seguintes opções para esta definição:  

        -   Quando ativar a implementação, as atualizações que cumpram os critérios definidos da regra são adicionadas a um grupo de atualização de software. O conteúdo de atualização de software é transferido conforme necessário. O conteúdo é copiado para pontos de distribuição especificados e as atualizações são implementadas para os clientes da coleção de destino.  

        -   Quando não ativar a implementação, as atualizações que cumpram os critérios definidos da regra são adicionadas a um grupo de atualização de software. O conteúdo de implementação da atualização de software é baixado, conforme necessário e distribuído aos pontos de distribuição especificado. O site cria uma implementação desativada no grupo de atualização de software para impedir que as atualizações que está a ser implementadas em clientes. Esta opção fornece tempo para se preparar para implementar as atualizações, verifique se as atualizações que cumprem os critérios são adequadas e, em seguida, ativar a implementação.  

4.  Sobre o **definições de implementação** página, configure as seguintes definições:  

    -   **Utilizar a reativação por LAN para reativar os clientes para as implementações necessárias**: Especifica se pretende ativar a reativação por LAN na data limite. Reativação por LAN envia pacotes de reativação para computadores que necessitem de uma ou mais atualizações de software na implementação. O site é reativado por todos os computadores que estejam no modo de suspensão quando for atingido o prazo de instalação, pelo que pode iniciar a instalação. Os clientes que estejam no modo de suspensão e que não necessitam de quaisquer atualizações de software na implementação não são iniciados. Por predefinição, esta definição não está ativada. Antes de utilizar esta opção, configure computadores e redes para reativação por LAN. Para obter mais informações, consulte [como configurar a reativação por LAN](/sccm/core/clients/deploy/configure-wake-on-lan).  

    -   **Nível de detalhe**: Especifique o nível de detalhe para as mensagens de estado que são enviadas pelos clientes.  

        > [!IMPORTANT]  
        >  Quando implementa atualizações de definição, defina o nível de detalhe para **apenas erros** para que o cliente envie uma mensagem de estado apenas quando não for uma atualização de definição. Caso contrário, o cliente comunica um grande número de mensagens de estado que podem afetar o desempenho do servidor de site.  

    -   **Definição de termos de licença**: Especifique se pretende implementar automaticamente atualizações de software com termos de licenciamento associados. Algumas atualizações de software incluem termos de licenciamento. Quando implementar automaticamente atualizações de software, os termos de licenciamento não são apresentados e não há uma opção para aceitar os termos de licença. Opte por implementar automaticamente todas as atualizações de software, independentemente de um termo de licenciamento associados, ou apenas implementar as atualizações que não tenham termos de licenciamento associados.  

         - Para rever os termos de licença para uma atualização de software, selecione a atualização de software no **todas as atualizações de Software** nó da **biblioteca de Software** área de trabalho. No Friso, clique em **rever licenciamento**.    

         - Para encontrar atualizações de software com termos de licenciamento associados, adicione a **termos de licenciamento** coluna para o painel de resultados na **todas as atualizações de Software** nó. Clique no cabeçalho da coluna ordenar pelas atualizações de software com termos de licenciamento.  

5.  Sobre o **atualizações de Software** página, configure os critérios para as atualizações de software que a ADR são obtidas e adicionadas ao grupo de atualização de software.  

     - O limite para as atualizações de software na ADR é de 1000 atualizações de software.  

     - Se for necessário, filtre o tamanho do conteúdo para atualizações de software nas regras de implementação automática. Para obter mais informações, consulte [Configuration Manager e a manutenção simplificada de Windows inferiores nível sistemas de operativos](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).  

     - A partir da versão 1806, uma propriedade de filtro para **arquitetura** está agora disponível. Utilize este filtro para excluri arquiteturas como Itanium e ARM64 que são menos comuns. Lembre-se de que existem aplicativos de 32 bits (x86) e componentes em execução em sistemas de 64 bits (x64). A menos que tem a certeza de que não precisa x86, ativá-la também de ao escolher x64.<!--1322266-->  


6.  Sobre o **agenda de avaliação** página, especifique se pretende ativar a ADR executar com base numa agenda. Se estiver ativada, clique em **Personalizar** para definir a agenda periódica.  

    - A configuração de hora de início para a agenda baseia-se na hora local do computador que executa a consola do Configuration Manager.  

    - A avaliação da ADR pode ser executada, no máximo, três vezes por dia.  

    - Nunca, defina a agenda de avaliação com uma frequência que exceda a agenda de sincronização de atualizações de software. Esta página apresenta o agendamento da sincronização de ponto de atualização de software para ajudar a determinar a frequência da agenda de avaliação.  
    
    - Para executar manualmente a ADR, selecione a regra no **regra de implementação automática** nó do console e, em seguida, clique **executar agora** na faixa de opções.  
    
       > [!NOTE]  
       > A partir da versão 1802, ADRs podem ser agendadas para avaliar o desvio de um dia base. Por exemplo, se Patch Terça-feira, na verdade, se na quarta-feira para, defina a agenda de avaliação para a segunda Terça-feira do deslocamento de mês por um dia.<!--1357133-->  
       >  
       > Durante o agendamento de avaliação com um desvio durante a última semana do mês, se escolher um deslocamento que continua no mês seguinte, o site de agenda de avaliação para o último dia do mês.<!--506731-->  
       >  
       > ![Deslocamento de agenda de avaliação personalizada ADR do dia base](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  Sobre o **agenda de implementação** página, configure as seguintes definições:  

    -   **Avaliação da agenda**: Especifique o tempo que o Configuration Manager avalia o tempo disponível e o prazo de instalação. Opte por utilizar Hora Universal Coordenada (UTC) ou na hora local do computador que executa a consola do Configuration Manager.  

          - Quando seleciona **hora local do cliente** aqui e, em seguida, selecione **logo que possível** para o **hora de disponibilização do Software**, a hora atual no computador com o Consola do Configuration Manager é utilizada para avaliar se as atualizações estiverem disponíveis. Este comportamento é o mesmo com o **prazo de instalação** e a hora quando as atualizações são instaladas num cliente. Se o cliente estiver num fuso horário diferente, estas ações ocorrem quando a hora do cliente atinge o tempo de avaliação.  

    -   **Hora de disponibilização do software**: Selecione uma das seguintes definições para especificar quando as atualizações de software são disponibilizadas aos clientes:  

        -   **Assim que possível**: Disponibiliza as atualizações de software na implementação aos clientes logo que possível. Quando criar a implementação com esta definição selecionada, o Configuration Manager atualiza a política de cliente. A política de cliente próximo ciclo de consulta, os clientes estarão informados da implementação e as atualizações de software estão disponíveis para instalação.  

        -   **Hora específica**: Torna as atualizações de software incluídas na implementação aos clientes numa data e hora específicas. Quando criar a implementação com esta definição ativada, o Configuration Manager atualiza a política de cliente. A política de cliente próximo ciclo de consulta, os clientes estarão informados da implementação. No entanto, as atualizações de software na implementação não estão disponíveis para instalação após a data e hora configuradas.  

    -   **Prazo de instalação**: Selecione uma das seguintes definições para especificar o prazo de instalação das atualizações de software da implementação:  

        -   **Assim que possível**: Selecione esta definição para instalar automaticamente as atualizações de software na implementação logo que possível.  

        -   **Hora específica**: Selecione esta definição para instalar automaticamente as atualizações de software da implementação numa hora e data específicas. O Configuration Manager determina o prazo de instalação de atualizações de software ao adicionar configurada **hora específica** intervalo para o **hora de disponibilização do Software**.  

             - O prazo da instalação real é apresentada acrescida além de um período de tempo aleatório de até duas horas. O recurso aleatório reduz o impacto potencial de clientes na coleção de instalação de atualizações na implementação ao mesmo tempo.  

             - Para desativar o atraso de aleatoriedade da instalação de atualizações de software necessárias, configure o definição de cliente **desativar a aleatoriedade de prazos** no **agente do computador** grupo. Para obter mais informações, consulte [definições do agente do computador cliente](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

    -  **Trasar imposição para esta implementação, de acordo com as preferências do usuário, até o período de tolerância definido nas definições de cliente**: Ative esta definição dar aos utilizadores mais tempo para instalar atualizações de software necessárias para além do prazo.  

        - Este comportamento é normalmente exigido quando um computador estiver desativado para muito tempo e tem de instalar várias atualizações de software ou aplicativos. Por exemplo, quando um usuário retorna de férias, têm de aguardar por muito tempo, pois o cliente instala implementações em atraso.  

        - Configure este período de tolerância com a propriedade **período de tolerância para a imposição de após a implementação do prazo (horas)** nas definições do cliente. Para obter mais informações, consulte a [agente do computador](/sccm/core/clients/deploy/about-client-settings#computer-agent) secção. O período de tolerância de imposição aplica-se a todas as implementações com esta opção ativada e direcionadas para dispositivos em que implementou também a definição de cliente.  

        - Após o prazo, o cliente instala as atualizações de software na primeira janela não comerciais, que o utilizador configurado, até esse período de tolerância. No entanto, o utilizador ainda pode abrir o Centro de Software e instalar as atualizações de software em qualquer altura. Assim que o período de tolerância expirar, imposição reverte para o comportamento normal para implementações em atraso.  

8. Sobre o **experiência de utilizador** página, configure as seguintes definições:  

    -   **Notificações do utilizador**: Especifique se pretende apresentar a notificação no Centro de Software em configurada **hora de disponibilização do Software**. Esta definição controla se é necessário notificar os utilizadores nos clientes.  

    -   **Comportamento do prazo**: Especifica os comportamentos para quando o software atualizar implementação atingir o prazo de fora de quaisquer janelas de manutenção definida. As opções incluem se pretende instalar as atualizações de software e se pretende executar um sistema de reinício após a instalação. Para obter mais informações sobre janelas de manutenção, consulte [como utilizar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).  
        
        > [!Note]
        > Isto aplica-se apenas quando a janela de manutenção é configurada para o dispositivo de cliente. Se nenhuma janela de manutenção é definida no dispositivo, a atualização da instalação e reinício será sempre acontece após o prazo.

    -   **Comportamento do reinício do dispositivo**: Especifique se pretende suprimir um reinício de sistema nos servidores e estações de trabalho se uma reinicialização é necessária para concluir a instalação da atualização.  

        > [!WARNING]  
        >  A supressão dos reinícios de sistema pode ser útil em ambientes de servidor, ou quando não quiser que os computadores de destino sejam reiniciados por predefinição. No entanto, este método pode deixar computadores num Estado não seguro. Permitir que um ajuda de reinício forçado garantir conclusão imediata da instalação de atualização de software.  

    -   **Processamento para dispositivos Windows Embedded do filtro de escrita**: Esta definição controla o comportamento de instalação em dispositivos Windows Embedded que estão ativados com um filtro de escrita. Escolha a opção para consolidar as alterações no prazo de instalação ou durante uma janela de manutenção. Quando seleciona esta opção, é necessário um reinício e as alterações sejam mantidas no dispositivo. Caso contrário, a atualização é instalada, aplicada na sobreposição temporária e confirmada posteriormente.  

           -  Ao implementar uma atualização de software num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada.  

    - **Comportamento de reavaliação de implementação após o reinício de atualizações de software**: Selecione esta definição para configurar as implementações de atualizações de software para que os clientes executem uma análise de compatibilidade de atualizações de software imediatamente após um cliente, instala as atualizações de software e reinicializações. Esta definição permite que o cliente Verifique a existência de atualizações adicionais que se tornam aplicáveis após o cliente é reiniciado, em seguida, instala-os durante a mesma janela de manutenção.  

9. Sobre o **alertas** página, configure a forma como o Configuration Manager gera alertas para esta implementação. Alertas do Configuration Manager de atualizações de software recente de revisão da **atualizações de Software** nó da **biblioteca de Software** área de trabalho. Se também estiver a utilizar o System Center Operations Manager, configure os seus alertas também.  

10. Sobre o **definições de transferência** página, configure as seguintes definições:  

    - Especifique se os clientes devem transferir e instalar as atualizações quando estiverem a utilizar um ponto de distribuição de um vizinho ou os grupos de limites de site padrão.  

    - Especifique se os clientes devem transferir e instalar as atualizações a partir de um ponto de distribuição no grupo de limite predefinido do site, quando o conteúdo para o software das atualizações não está disponível num ponto de distribuição no atual ou os grupos de limites de vizinho.  

    - **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**: Especifique se pretende ativar a utilização do BranchCache para transferências de conteúdos. Para obter mais informações, consulte [BranchCache](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#branchcache). A partir da versão 1802, BranchCache está sempre ativada nos clientes. Esta definição for removida, como os clientes utilizam o BranchCache, se o ponto de distribuição suportar.  

    - **Se as atualizações de software não estão disponíveis no ponto de distribuição na atual, vizinho ou do site de grupos de limite, transfira o conteúdo do Microsoft Updates**: Selecione esta definição para que os clientes ligados à intranet transferir atualizações de software do Microsoft Update, se as atualizações não estão disponíveis em pontos de distribuição. Clientes baseados na Internet sempre aceder ao Microsoft Update para atualizações de software, conteúdas.  

    - Especifique se pretende permitir que os clientes transfiram após um prazo de instalação quando estiverem a utilizar de ligações à internet limitadas. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando estiver numa ligação limitada.  

    > [!NOTE]  
    >  Os clientes solicitam a localização de conteúdo a partir de um ponto de gestão para as atualizações de software de uma implementação. O comportamento de transferência dependerá de como configurou o ponto de distribuição, o pacote de implementação e as definições nesta página.   

11. Sobre o **pacote de implementação** página, selecione uma das seguintes opções:  

    - **Selecione um pacote de implementação**: Adicione estas atualizações a um pacote de implementação existente.  

    - **Criar um novo pacote de implementação**: Adicione estas atualizações para um novo pacote de implementação. Configure as seguintes definições adicionais:  

        -  **Nome**: Especifique o nome do pacote de implementação. Utilize um nome exclusivo que descreve o conteúdo do pacote. É limitado a 50 carateres.  

        -  **Descrição**: Especifique uma descrição que disponibilize informações sobre o pacote de implementação. A descrição opcional é limitada a 127 carateres.  

        -  **Origem do pacote**: Especifica a localização dos ficheiros de origem de atualização do software. Escreva um caminho de rede para a localização de origem, por exemplo, `\\server\sharename\path`, ou clique em **procurar** para procurar a localização de rede. Crie a pasta partilhada para os ficheiros de origem do pacote de implementação antes de prosseguir para a página seguinte.  

            - Não é possível utilizar a localização especificada como a fonte de outro pacote de implementação de software.  

            - Pode alterar a localização de origem do pacote nas propriedades do pacote de implementação depois do Configuration Manager cria o pacote de implementação. Se o fizer, primeiro copie o conteúdo da origem do pacote original para a nova localização de origem do pacote.  

            -  A conta de computador do fornecedor de SMS e o utilizador que está a executar o Assistente para transferir as atualizações de software terão de ter **escrever** permissões para a localização de transferência. Restringir o acesso à localização de transferência. Esta restrição reduz o risco dos atacantes adulterar os ficheiros de origem de atualização de software.  

        -  **Prioridade de envio**: Especifique a prioridade de envio para o pacote de implementação. O Configuration Manager utiliza essa prioridade quando envia o pacote para pontos de distribuição. Pacotes de implementação são enviados por ordem de prioridade: elevada, média ou baixa. Os pacotes com prioridades idênticas são enviados pela ordem em que foram criados. Se não houver nenhum registo de segurança, o pacote de processos imediatamente, independentemente de sua prioridade.  

        - **Ativar a replicação diferencial de binários**: Ative esta definição para minimizar o tráfego de rede entre sites. Replicação diferencial binária (BDR) apenas atualiza o conteúdo que foi alterado no pacote, em vez de atualizar o conteúdo do pacote inteiro. Para obter mais informações, consulte [replicação de diferencial binário](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#binary-differential-replication).  

    - **Nenhum pacote de implementação**: A partir da versão 1806, implemente atualizações de software em dispositivos sem primeiro baixar e distribuir conteúdo para pontos de distribuição. Esta definição é benéfica ao lidar com conteúdo da atualização extremamente grandes. Também usá-lo quando pretender que sempre clientes a obter o conteúdo do serviço de nuvem do Microsoft Update. Os clientes neste cenário também podem transferir o conteúdo de elementos que já tenham o conteúdo necessário. O cliente continua a gerir a transferência do conteúdo, o Configuration Manager, portanto, pode utilizar a funcionalidade de cache ponto a ponto do Configuration Manager ou outras tecnologias, como a Otimização da entrega. Esta funcionalidade suporta qualquer tipo de atualização suportado pela gestão de atualizações de software do Configuration Manager, incluindo o Windows e atualizações do Office.<!--1357933-->  

        > [!Note]  
        > Esta opção é apenas para novas regras de implementação automática. Não é possível modificar as regras existentes com esta definição.<!--SCCMDocs issue 741-->  

12. Sobre o **pontos de distribuição** página, especifique os pontos de distribuição ou grupos para alojar o software de ficheiros de atualização de ponto de distribuição. Para obter mais informações sobre os pontos de distribuição, veja [Configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_configs). Esta página apenas está disponível ao criar um novo pacote de implementação da atualização de software.  
  

13. Sobre o **localização de transferência** página, especifique se pretende transferir os ficheiros de atualização de software da internet ou da rede local. Configure as seguintes definições:  

    -   **Transferir atualizações de software a partir da internet**: Selecione esta definição para transferir as atualizações de software a partir de uma localização especificada na internet. Esta definição está ativada por predefinição.  

    -   **Transferir atualizações de software a partir de uma localização na rede local**: Selecione esta definição para transferir as atualizações de software a partir de um diretório local ou uma pasta compartilhada. Esta definição é útil quando o computador que executa o assistente não tem acesso à internet. Qualquer computador com acesso à internet provisoriamente pode transferir as atualizações de software. Em seguida, armazená-las numa localização na rede local que seja acessível ao computador que executa o assistente.  

14. Sobre o **seleção de idioma** , selecione os idiomas para o qual o site transfere as atualizações de software selecionadas. O site transfere apenas essas atualizações se elas estão disponíveis nos idiomas selecionados. Atualizações de software que não são específicas do idioma serão sempre transferidas. Por predefinição, o assistente seleciona os idiomas que configurou nas propriedades do ponto de atualização de software. Terá de estar selecionado pelo menos um idioma para que possa prosseguir para a página seguinte. Se selecionar apenas idiomas que não suporta uma atualização de software, o download falha para a atualização.  

15. Na página **Resumo** , reveja as definições. Para guardar as definições de um modelo de implementação, clique em **guardar como modelo**. Introduza um nome e selecione as definições que pretende incluir no modelo, em seguida, clique em **guardar**. Para alterar uma definição configurada, clique na página do assistente associada e altere a definição.  

    -  O nome do modelo pode consistir em carateres ASCII alfanuméricos, bem como `\` (barra invertida) ou `'` (plica).  

16. Clique em **Seguinte** para criar a ADR.  

Depois de concluir o assistente, a execução da ADR. Ele adiciona as atualizações de software que cumprem os critérios especificados a um grupo de atualização de software. Em seguida, a ADR transfere as atualizações para a biblioteca de conteúdos no servidor do site e os distribui aos pontos de distribuição configurados. A ADR, em seguida, implementa o grupo de atualizações de software a clientes da coleção de destino.  



##  <a name="BKMK_AddDeploymentToADR"></a> Adicionar uma nova implementação a uma ADR existente  

Depois de criar uma ADR, adicione implementações adicionais para a regra. Esta ação ajuda a gerir a complexidade da implantação de atualizações de diferentes para diferentes coleções. Cada nova implementação tem acesso a todas as funcionalidades e à experiência de monitorização da implementação.  


### <a name="process-to-add-a-new-deployment-to-an-existing-adr"></a>Processo para adicionar uma nova implementação a uma ADR existente  

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **atualizações de Software**, selecione o **regras de implementação automática** nó e, em seguida, selecione a regra pretendida.  

2.  No Friso, clique em **adicionar implementação**.   

3.  Sobre o **coleção** página do Assistente para adicionar implementação, configure as definições disponíveis da mesma forma como o **geral** página de criar regra de Assistente de implementação automática. Para obter mais informações, consulte a seção anterior sobre o [processo para criar uma ADR](#bkmk_adr-process). O resto do Assistente para adicionar implementação inclui as seguintes páginas, também de coincidir com descrições detalhadas acima:  

     - Definições de implementação
     - Agenda de implementação
     - Experiência de utilizador
     - Alertas
     - Transferir definições  

Implementações também podem ser adicionadas por meio de programação utilizando cmdlets do Windows PowerShell. Para obter uma descrição completa da utilização deste método, consulte [New-CMSoftwareUpdateDeployment](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmsoftwareupdatedeployment) .

Para obter mais informações sobre o processo de implementação, veja [Processo de implementação de atualizações de software](/sccm/sum/understand/software-updates-introduction#BKMK_DeploymentProcess).


## <a name="next-steps"></a>Passos seguintes
[Monitorizar atualizações de software](monitor-software-updates.md)

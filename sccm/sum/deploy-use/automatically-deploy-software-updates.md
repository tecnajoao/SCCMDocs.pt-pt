---
title: Implementar automaticamente atualizações de software
titleSuffix: Configuration Manager
description: Implemente automaticamente atualizações de software ao adicionar novas atualizações a um grupo de atualização que está associada a uma implementação ativa, ou utilizando ADRs.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: 3b267e122370cc12ecec2f42dcb1dfc62c45fe63
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
#  <a name="BKMK_AutoDeploy"></a> Implementar automaticamente atualizações de software  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Pode utilizar uma regra de implementação automática (ADR) em vez de adicionar novas atualizações a um grupo de atualização de software existente. Normalmente, utilizará ADRs mensalmente implementar atualizações de software (conhecidas como Patch Terça-feira atualizações) e para gerir atualizações de definições. Se precisar de ajuda para determinar que implementação de método é mais adequado para si, consulte [implementar atualizações de software](deploy-software-updates.md).

<!--##  <a name="BKMK_AddUpdatesToExistingGroup"></a> Add software updates to a deployed update group  
After you create and deploy a software update group, you can add software updates to the update group and they will be automatically deployed.  

> [!IMPORTANT]  
>  When you add software updates to an existing software update group that has already been deployed, it might take several minutes before the additional software updates are added to the deployment.  

Use the following procedure to add software updates to an existing update group.  

#### To add software updates to an existing software update group  

1.  In the Configuration Manager console, navigate to **Software Library** > **Overview** > **Software Updates**.  

2.  Select the software updates that are to be added to the new software update group.  

3.  On the **Home** tab, in the **Update** group, click **Edit Membership**.  

4.  Select the software update group to which you want to add the software updates as members.  

5.  Click the **Software Update Groups** node to display the software update group.  

6.  Click the software update group, and in the **Home** tab, in the **Update** group, click **Show Members** to display a list of the software updates in the group.  --mstewart this is already doc'd on the SUG page. -->

##  <a name="BKMK_CreateAutomaticDeploymentRule"></a> Criar uma regra de implementação automática (ADR)  
Pode aprovar e implementar automaticamente atualizações de software utilizando uma ADR. Pode fazer com que a regra adicione atualizações de software a um novo grupo de atualização de software de cada vez que a regra for executada ou adicionar atualizações de software a um grupo existente. Quando uma regra for executada e adiciona as atualizações de software a um grupo existente, a regra remove todas as atualizações do grupo e, em seguida, adiciona as atualizações que cumprem os critérios que definiu para o grupo. 

> [!WARNING]  
>  Antes de criar uma ADR pela primeira vez, certifique-se de que a sincronização de atualizações de software foi concluída no site. Isto é importante quando executar o Configuration Manager com um idioma diferente do inglês porque classificações de atualizações de software são apresentadas em inglês antes da primeira sincronização e, em seguida, no idioma localizado após a atualização de software a conclusão da sincronização. As regras que tiver criado antes de sincronizar as atualizações de software poderão não funcionar corretamente após a sincronização devido à discrepância da cadeia de texto.  

 Utilize o procedimento seguinte para criar uma ADR.  

#### <a name="to-create-an-adr"></a>Para criar uma ADR  

1.  Na consola do Configuration Manager, navegue até à **biblioteca de Software** **descrição geral** > **atualizações de Software** > **regras de implementação automática**.  

2.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Regra de Implementação Automática**. O Assistente de Criação de Regra de Implementação Automática abre.  

3.  Na página **Geral** , configure as seguintes definições:  

    -   **Nome**: Especifique o nome para a ADR. O nome tem de ser exclusivo e deve descrever o objetivo da regra além de distingui-la de outras no site do Configuration Manager.  

    -   **Descrição**: Especifique uma descrição para a ADR. A descrição deve disponibilizar uma descrição geral da regra de implementação e outras informações relevantes que ajudem a distinguir a regra de outras. O campo de descrição é opcional, tem um limite de 256 caracteres e está em branco por predefinição.  

    -   **Selecione o modelo de implementação**: Especifique se pretende aplicar um modelo de implementação anteriormente guardado. Pode configurar um modelo de implementação que contém várias propriedades comuns de atualização de implementação que podem ser utilizadas ao criar ADRs. Estes modelos ajudam a assegurar a consistência entre implementações semelhantes e a poupar tempo.  

         - Pode selecionar entre os modelos de implementação de atualizações de software incorporados a partir do Assistente de Criação de Regra de Implementação Automática. O modelo **Atualizações de Definição** fornece definições comuns a utilizar quando implementa atualizações de software de definições. O modelo **Patch Terça** fornece definições comuns a utilizar quando implementa atualizações de software num ciclo mensal.  

    -   **Coleção**: Especifica a coleção de destino a ser utilizado para a implementação. Os membros da coleção recebem as atualizações de software definidas na implementação.  

    -   Especifique se pretende adicionar atualizações de software a um grupo de atualização de software novo ou existente. Na maioria dos casos, optará provavelmente por criar um novo grupo de atualizações de software quando a ADR for executada. No entanto, poderá optar por utilizar um grupo existente se a regra for executada com base numa agenda mais intensiva. Por exemplo, se pretender executar a regra diariamente para atualizações de definições, poderá adicionar as atualizações de software a um grupo de atualização de software existente.  

    -   **Ativar a implementação após a execução desta regra**: Especifique se pretende ativar a implementação de atualização de software após a execução da ADR. Relativamente a esta especificação, considere os seguintes procedimentos:  

        -   Quando ativar a implementação, as atualizações que cumprem os critérios definidos da regra são adicionadas a um grupo de atualização de software. O conteúdo da atualização de software é transferido conforme necessário. O conteúdo é copiado para pontos de distribuição especificados e as atualizações são implementadas para os clientes na coleção de destino.  

        -   Quando ativar a implementação, as atualizações que cumprem os critérios definidos da regra são adicionadas a um grupo de atualização de software. A política de implementação de atualizações de software está configurada. No entanto, as atualizações não são transferidas ou implementadas nos clientes. Esta situação disponibiliza o tempo para se preparar para implementar as atualizações, certifique-se de que as atualizações que cumprem os critérios são adequadas e, em seguida, ativar a implementação numa altura posterior.  

4.  Na página Definições de Implementação, configure as seguintes definições:  

    -   **Utilizar a reativação por LAN para reativar os clientes para as implementações necessárias**: Especifica se pretende ativar a reativação por LAN na data limite para o envio de pacotes de reativação para computadores que necessitem de uma ou mais atualizações de software na implementação. Todos os computadores que estejam no modo de suspensão na hora de prazo de instalação irão ser reativados para que pode iniciar a instalação. Os clientes que se encontrem no modo de suspensão e que não necessitem de quaisquer atualizações de software no âmbito da implementação não serão iniciados. Por predefinição, esta definição não está ativada. Para poder utilizar esta opção, necessita de configurar os computadores e as redes para a Reativação por LAN. 

    -   **Nível de detalhe**: Especifique o nível de detalhe para as mensagens de estado que são enviadas pelos computadores cliente.  

        > [!IMPORTANT]  
        >  Ao implementar atualizações de definição, defina o nível de detalhe para **apenas erros** para que o cliente envie uma mensagem de estado apenas quando não for uma atualização de definição. Caso contrário, o cliente enviará um elevado número de mensagens de estado, o que poderá afetar o desempenho do servidor do site.  

    -   **Definição de termos de licença**: Especifique se pretende implementar automaticamente atualizações de software com termos de licenciamento associados. Algumas atualizações de software incluem termos de licenciamento, por exemplo um pacote de serviço. Ao implementar atualizações de software automaticamente, os termos de licenciamento não são apresentados e não haverá a opção de aceitação dos termos de licenciamento. Pode optar por implementar automaticamente todas as atualizações de software, independentemente de termos de licenciamento associados, ou apenas implementar as atualizações que não tenham termos de licenciamento associados.  
        - Para rever os termos de licenciamento de uma atualização de software, pode selecionar a atualização de software no **todas as atualizações de Software** o nó do **biblioteca de Software** área de trabalho. No **home page** separador o **atualização** , clique em **revisão licença**.    
        - Para encontrar atualizações de software com termos de licenciamento associados, pode adicionar o **termos de licenciamento** coluna para o painel de resultados no **todas as atualizações de Software** nós. Clique no cabeçalho da coluna ordenar segundo as atualizações de software com termos de licenciamento.  

5.  Na página Atualizações de Software, configure os critérios para as atualizações de software que são obtidas e adicionadas pela ADR ao grupo de atualizações de software. O limite para as atualizações de software na ADR é de 1000 atualizações de software. Se for necessário, pode filtrar o tamanho do conteúdo para atualizações de software nas regras de implementação automática. Para obter mais informações, consulte [do Configuration Manager e simplificada manutenção do Windows em baixo nível de sistemas operativos](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).


6.  Na página Agenda de Avaliação, especifique se pretende ativar a execução da ADR com base numa agenda. Se estiver ativada, clique em **Personalizar** para definir a agenda periódica. A configuração da hora de início da agenda baseia-se na hora local do computador que executa a consola do Configuration Manager.
    - A configuração da hora de início da agenda baseia-se na hora local do computador que executa a consola do Configuration Manager.
    - A avaliação da ADR pode ser executada, no máximo, três vezes por dia.
    - Nunca defina a agenda de avaliação com uma frequência que exceda a agenda de sincronização de atualizações de software. A agenda de sincronização de ponto de atualização de software é apresentada para o ajudar a determinar a frequência da agenda de avaliação. 
    - Para executar manualmente a ADR, selecione a regra e, em seguida, clique em **Executar agora** no separador **Home Page** do grupo **Regra de Implementação Automática** .
    
       > [!NOTE]  
       >A partir do Configuration Manager versão 1802, ADRs podem ser agendadas para avaliar o desvio de um dia base. Ou seja, se patch Terça-feira, na verdade, em que recai o quarta-feira por si, pode ser definido o agendamento de avaliação para a segunda Terça-feira da desvio mês por um dia. <!--1357133-->
       > - Durante o agendamento de avaliação para ocorrer com um desvio igual durante a última semana do mês, a avaliação será agendada para o último dia do mês se o deslocamento escolhido capacidade excedida para o mês seguinte. <!--506731-->

       > ![Desvio de agenda de avaliação personalizado ADR do dia de base](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  Na página Agenda de Implementação, configure as seguintes definições:  

    -   **Avaliação da agenda**: Especifique se o Configuration Manager avalia o tempo disponível e tempos de prazo de instalação utilizando a hora UTC ou na hora local do computador que executa a consola do Configuration Manager.  
         - Quando selecionar a hora local e, em seguida, selecione **logo que possível** para o **hora de disponibilização do Software** ou **prazo de instalação**, a hora atual da execução de computador, a consola do Configuration Manager é utilizada para calcular quando estão disponíveis atualizações ou quando são instaladas num cliente. Se o cliente tiver um fuso horário diferente, estas ações irão ocorrer quando a hora do cliente corresponder à hora de avaliação.  

    -   **Hora de disponibilização do software**: Selecione uma das seguintes definições para especificar quando as atualizações de software são disponibilizadas aos clientes:  

        -   **Logo que possível**: Faz com que as atualizações de software que estão incluídas na implementação aos computadores cliente logo que possível. Quando criar a implementação com esta definição selecionada, o Configuration Manager atualiza a política de cliente. A política de cliente seguinte ciclo de consulta, os clientes ficarão informados da implementação e poderão obter as atualizações disponíveis para instalação.  

        -   **Hora específica**: Faz com que as atualizações de software incluídas na implementação aos computadores cliente numa hora e data específicas. Quando criar a implementação com esta definição ativada, o Configuration Manager atualiza a política de cliente. Em seguida, durante o ciclo de consulta seguinte da política de cliente, os clientes estarão informados da implementação. No entanto, as atualizações de software da implementação não ficarão disponíveis para instalação antes da data e hora configuradas.  

    -   **Prazo de instalação**: Selecione uma das seguintes definições para especificar o prazo de instalação para as atualizações de software da implementação:  

        -   **Logo que possível**: Selecione esta definição para instalar automaticamente as atualizações de software na implementação logo que possível.  

        -   **Hora específica**: Selecione esta definição para instalar automaticamente as atualizações de software na implementação numa hora e data específicas. O Configuration Manager determina o prazo de instalação de atualizações de software adicionando configurada **hora específica** intervalo para o **hora de disponibilização do Software**.  

            - A hora do prazo instalação real é o apresentada acrescida de um período de tempo aleatório de cópia de segurança duas horas. Os prazos reduz o impacto potencial dos computadores cliente na coleção de instalação de atualizações na implementação ao mesmo tempo.  
          
             - Pode configurar a definição de cliente **Agente do Computador** , **Desativar a aleatoriedade de prazos** para desativar o atraso de aleatoriedade da instalação para as atualizações de software necessárias. Para obter mais informações, veja [Agente do Computador](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8. Na página Experiência de Utilizador, configure as seguintes definições:  

    -   **As notificações de utilizador**: Especifique se pretende apresentar a notificação de atualizações de software no Centro de Software no computador cliente à configurada **hora de disponibilização do Software** e se pretende apresentar as notificações de utilizador nos computadores cliente.  

    -   **Comportamento do prazo**: Especifique o comportamento a adotar quando é atingido o prazo para a implementação de atualização de software. Especifique se pretende instalar as atualizações de software da implementação. Especifique também se pretende reiniciar o sistema após a instalação da atualização de software, independentemente de uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção, consulte [como utilizar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento de reinício do dispositivo**: Especifique se pretende suprimir um reinício de sistema nos servidores e estações de trabalho se um reinício é necessário para concluir a instalação da atualização.  

        > [!WARNING]  
        >  A supressão dos reinícios de sistema pode ser útil em ambientes de servidor ou em casos em que não pretenda que os computadores que instalam as atualizações de software sejam reiniciados por predefinição. No entanto, este método pode deixar os computadores num estado não seguro, enquanto que um reinício forçado ajudará a assegurar a conclusão imediata da instalação da atualização de software.  

    -   **Para dispositivos Windows Embedded de processamento do filtro de escrita**: Quando implementa atualizações de software em dispositivos Windows Embedded que tenham o filtro de escrita ativado, pode especificar a instalar a atualização de software na sobreposição temporária e ou confirmar as alterações mais tarde ou por confirmar as alterações no prazo de instalação ou durante uma janela de manutenção. Ao consolidar alterações no momento da instalação ou durante uma janela de manutenção, será necessário um reinício para que as alterações sejam mantidas no dispositivo.  

           -  Ao implementar uma atualização de software num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada.  

    - **Comportamento de reavaliação de implementação após o reinício de atualizações de software**: Selecione esta definição para configurar as implementações de atualizações de software para que os clientes executem uma análise de compatibilidade de atualizações de software imediatamente após um cliente, instala as atualizações de software e o reinício. Esta definição permite que o cliente Verifique a existência de atualizações adicionais que se tornam aplicáveis após o cliente é reiniciado, em seguida, instala-los durante a mesma janela de manutenção.

9. Na página alertas, configure o Configuration Manager e o System Center Operations Manager gerarão alertas para esta implementação. Pode rever os alertas de atualizações de software recentes a partir do nó **Atualizações de Software** da área de trabalho **Biblioteca de Software** .  

10. Na página Definições de Transferência, configure as seguintes definições:  

    - Especifique se os clientes devem transferir e instalar as atualizações quando estão ligados a uma rede lenta ou utilizar uma localização de conteúdo de contingência.  

    - Especifique se pretende que os clientes transferir e instalar as atualizações de software a partir de um ponto de distribuição de contingência quando o conteúdo para as atualizações de software não está disponível num ponto de distribuição preferencial.  

    - **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**: Especifique se pretende ativar a utilização do BranchCache para as transferências de conteúdos. Para obter mais informações sobre o BranchCache, veja [Conceitos para a gestão de conteúdos](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Se as atualizações de software não estão disponíveis no ponto de distribuição na atual, vizinho ou site grupos, transferir conteúdo do Microsoft Updates**: Selecione esta definição para que os clientes de intranet ligada transferir as atualizações de software do Microsoft Update caso as atualizações não estejam disponíveis nos pontos de distribuição. Os clientes baseados na Internet podem sempre aceder ao Microsoft Update para o conteúdo de atualizações de software.

    - Especifique se pretende permitir que os clientes efetuem a transferência após um prazo de instalação se estiverem a utilizar ligações à Internet com tráfego limitado. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à Internet com tráfego limitado.  

    > [!NOTE]  
    >  Os clientes solicitam a localização de conteúdo a partir de um ponto de gestão para as atualizações de software de uma implementação. O comportamento de transferência dependerá da forma como tiver configurado o ponto de distribuição, o pacote de implementação e as definições desta página. Para obter mais informações, veja [Cenários de localização da origem de conteúdo](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. Na página Pacote de Implementação, selecione um pacote de implementação existente ou configure as seguintes definições para criar um novo pacote de implementação:  

    1.  **Nome**: Especifique o nome do pacote de implementação. Utilize um nome exclusivo que descreva o conteúdo do pacote. Está limitado a 50 carateres.  

    2.  **Descrição**: Especifique uma descrição que disponibilize informações sobre o pacote de implementação. A descrição está limitada a 127 caracteres.  

    3.  **Origem do pacote**: Especifica a localização dos ficheiros de origem de atualização de software.  Escreva um caminho de rede para a localização de origem, como, por exemplo, **\\\server\sharename\path**ou clique em **Procurar** para procurar a localização de rede. Crie a pasta partilhada para os ficheiros de origem do pacote de implementação antes de continuar para a página seguinte.  

        - A localização de origem do pacote de implementação especificada não pode ser utilizada por outro pacote de implementação de software.
        - Pode alterar a localização de origem do pacote nas propriedades do pacote de implementação, após o Configuration Manager cria o pacote de implementação. Mas se o fizer, terá primeiro de copiar o conteúdo da origem do pacote original para a nova localização de origem do pacote  
        -  Tanto a conta de computador do Fornecedor de SMS, como o utilizador que executar o assistente para transferir as atualizações de software, têm de ter permissões NTFS de **Escrita** na localização de transferência. Deverá restringir cuidadosamente o acesso à localização de transferência para reduzir o risco de adulteração dos ficheiros de origem de atualização de software por parte de atacantes.  
       

    4.  **Prioridade de envio**: Especifique a prioridade de envio para o pacote de implementação. O Configuration Manager utiliza a prioridade de envio para o pacote de implementação quando enviar o pacote para pontos de distribuição. Pacotes de implementação são enviados por ordem de prioridade: Alta, média ou baixa. Os pacotes com prioridades idênticas são enviados pela ordem em que foram criados. Se não existirem tarefas pendentes, o pacote será processado de imediato, independentemente da sua prioridade.  

12. Na página Pontos de Distribuição, especifique os pontos de distribuição ou grupos de pontos de distribuição que irão alojar os ficheiros de atualização de software. Para obter mais informações sobre os pontos de distribuição, veja [Configurações de pontos de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Esta página apenas está disponível ao criar um novo pacote de implementação da atualização de software.
  

13. Na página Localização de Transferência, especifique se pretende transferir os ficheiros de atualização de software a partir da Internet ou da rede local. Configure as seguintes definições:  

    -   **Transferir atualizações de software a partir da Internet**: Selecione esta definição para transferir as atualizações de software a partir de uma localização especificada na Internet. Esta definição está ativada por predefinição.  

    -   **Transferir atualizações de software a partir de uma localização na rede local**: Selecione esta definição para transferir as atualizações de software a partir de um diretório local ou uma pasta partilhada. Esta definição é útil se o computador que executa o assistente não tiver acesso à Internet. Qualquer computador que disponha de acesso à Internet poderá transferir provisoriamente as atualizações de software e guardá-las numa localização da rede local que esteja acessível ao computador que executa o assistente.  

14. Na página Seleção de Idioma, selecione os idiomas para os quais serão transferidas as atualizações de software selecionadas. As atualizações de software apenas são transferidas se estiverem disponíveis nos idiomas selecionados. As atualizações de software que não sejam específicas do idioma serão sempre transferidas. Por predefinição, o assistente seleciona os idiomas que tiver configurado nas propriedades do ponto de atualização de software. Terá de estar selecionado pelo menos um idioma para que possa prosseguir para a página seguinte. Se selecionar apenas idiomas que não são suportados por uma atualização de software, a transferência falhará para a atualização.  

15. Reveja as definições na página Resumo. Para guardar as definições de um modelo de implementação, clique em **guardar como modelo**. Introduza um nome e selecione as definições que pretende incluir no modelo, em seguida, clique em **guardar**. Para alterar uma definição configurada, clique na página do assistente associada e altere a definição.  
    -  O nome do modelo pode incluir carateres ASCII alfanuméricos, bem como **\\** (barra invertida) ou **‘** (plica).  

16. Clique em **Seguinte** para criar a ADR.  

 Depois de concluir o assistente, a ADR será executada. Irá adicionar as atualizações de software que cumprem os critérios especificados a um grupo de atualização de software. Em seguida, a ADR transfere as atualizações para a biblioteca de conteúdos no servidor do site e distribui-las para os pontos de distribuição configurados. A ADR, em seguida, implementa o grupo de atualização de software a clientes da coleção de destino.  

##  <a name="BKMK_AddDeploymentToADR"></a> Adicionar uma nova implementação a uma ADR existente  
 Depois de criar uma ADR, pode adicionar mais implementações à regra. Isto pode ajudá-lo a gerir a complexidade da implementação de diferentes atualizações em diferentes coleções. Cada nova implementação tem acesso a todas as funcionalidades e à experiência de monitorização da implementação.  

#### <a name="to-add-a-new-deployment-to-an-existing-adr"></a>Para adicionar uma nova implementação a uma ADR existente  

1.  Na consola do Configuration Manager, navegue até à **biblioteca de Software** > **descrição geral** > **atualizações de Software** > **regras de implementação automática**e, em seguida, selecione a regra pretendida.  

2.  No separador **Home Page** , no grupo **Regra de Implementação Automática** , clique em **Adicionar Implementação**. O Assistente para Adicionar Implementação abre.  

3.  Na página **Coleção** , configure as seguintes definições:  

    -   **Coleção**: Especifica a coleção de destino a ser utilizado para a implementação. Os membros da coleção recebem as atualizações de software definidas na implementação.  

    -   **Ativar a implementação após a execução desta regra**: Especifique se pretende ativar a implementação de atualização de software após a execução da ADR. Relativamente a esta especificação, considere os seguintes procedimentos:  

        -   Quando ativar a implementação, as atualizações que cumprem os critérios definidos da regra são adicionadas a um grupo de atualização de software. O conteúdo da atualização de software é transferido conforme necessário. O conteúdo é copiado para pontos de distribuição especificados e as atualizações são implementadas para os clientes na coleção de destino.  

        -  Quando ativar a implementação, as atualizações que cumprem os critérios definidos da regra são adicionadas a um grupo de atualização de software. A política de implementação de atualizações de software está configurada. No entanto, as atualizações não são transferidas ou implementadas nos clientes. Esta situação disponibiliza o tempo para se preparar para implementar as atualizações, certifique-se de que as atualizações que cumprem os critérios são adequadas e, em seguida, ativar a implementação numa altura posterior.  

4.  Na página Definições de Implementação, configure as seguintes definições:  

    -   **Utilizar a reativação por LAN para reativar os clientes para as implementações necessárias**: Especifica se pretende ativar a reativação por LAN na data limite para o envio de pacotes de reativação para computadores que necessitem de uma ou mais atualizações de software na implementação. Todos os computadores que estejam no modo de suspensão na hora de prazo de instalação irão ser reativados para que pode iniciar a instalação. Os clientes que se encontrem no modo de suspensão e que não necessitem de quaisquer atualizações de software no âmbito da implementação não serão iniciados. Por predefinição, esta definição não está ativada. Para poder utilizar esta opção, necessita de configurar os computadores e as redes para a Reativação por LAN.  

    -   **Nível de detalhe**: Especifique o nível de detalhe para as mensagens de estado que são enviadas pelos computadores cliente.  

        > [!IMPORTANT]  
        >  Ao implementar atualizações de definições, defina o nível de detalhe como **Apenas erros** para que o cliente apenas envie uma mensagem de estado quando não for possível entregar uma atualização de definições ao cliente. Caso contrário, o cliente enviará um elevado número de mensagens de estado, o que poderá afetar o desempenho do servidor do site.  

5.  Na página Agenda de Implementação, configure as seguintes definições:  

    -   **Avaliação da agenda**: Especifique se o Configuration Manager avalia o tempo disponível e tempos de prazo de instalação utilizando a hora UTC ou na hora local do computador que executa a consola do Configuration Manager.  

           -  Quando selecionar a hora local e, em seguida, selecione **logo que possível** para o **hora de disponibilização do Software** ou **prazo de instalação**, a hora atual da execução de computador, a consola do Configuration Manager é utilizada para calcular quando estão disponíveis atualizações ou quando são instaladas num cliente. Se o cliente tiver um fuso horário diferente, estas ações irão ocorrer quando a hora do cliente corresponder à hora de avaliação.  

    -   **Hora de disponibilização do software**: Selecione uma das seguintes definições para especificar quando as atualizações de software são disponibilizadas aos clientes:  

        -   **Logo que possível**: Selecione esta definição para disponibilizar as atualizações de software que estão incluídas na implementação aos computadores cliente logo que possível. Quando criar a implementação com esta definição selecionada, o Configuration Manager atualiza a política de cliente. A política de cliente seguinte ciclo de consulta, os clientes ficarão informados da implementação e poderão obter as atualizações disponíveis para instalação.  

        -   **Hora específica**: Faz com que as atualizações de software incluídas na implementação aos computadores cliente numa hora e data específicas. Quando criar a implementação com esta definição ativada, o Configuration Manager atualiza a política de cliente. Em seguida, durante o ciclo de consulta seguinte da política de cliente, os clientes estarão informados da implementação. No entanto, as atualizações de software da implementação não ficarão disponíveis para instalação antes da data e hora configuradas. 

    -   **Prazo de instalação**: Selecione uma das seguintes definições para especificar o prazo de instalação para as atualizações de software da implementação:  

        -   **Logo que possível**: Selecione esta definição para instalar automaticamente as atualizações de software na implementação logo que possível.  

        -   **Hora específica**: Selecione esta definição para instalar automaticamente as atualizações de software na implementação numa hora e data específicas. O Configuration Manager determina o prazo de instalação de atualizações de software adicionando configurada **hora específica** intervalo para o **hora de disponibilização do Software**.  

               - A hora do prazo instalação real é o apresentada acrescida de um período de tempo aleatório de cópia de segurança duas horas. Isto reduz o impacto potencial dos computadores cliente na coleção de instalação de atualizações na implementação ao mesmo tempo.  
              - Pode configurar a definição de cliente **Agente do Computador** , **Desativar a aleatoriedade de prazos** para desativar o atraso de aleatoriedade da instalação para as atualizações de software necessárias. Para obter mais informações, veja [Agente do Computador](../../core/clients/deploy/about-client-settings.md#computer-agent).  

6.  Na página Experiência de Utilizador, configure as seguintes definições:  

    -   **As notificações de utilizador**: Especifique se pretende apresentar a notificação de atualizações de software no Centro de Software no computador cliente à configurada **hora de disponibilização do Software** e se pretende apresentar as notificações de utilizador nos computadores cliente.  

    -   **Comportamento do prazo**: Especifique o comportamento a adotar quando é atingido o prazo para a implementação de atualização de software. Especifique se pretende instalar as atualizações de software da implementação. Especifique também se pretende reiniciar o sistema após a instalação da atualização de software, independentemente de uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção, consulte [como utilizar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento de reinício do dispositivo**: Especifique se pretende suprimir um reinício de sistema nos servidores e estações de trabalho se um reinício é necessário para concluir a instalação da atualização.  
 
           > [!WARNING]  
           >  A supressão dos reinícios de sistema pode ser útil em ambientes de servidor ou em casos em que não pretenda que os computadores que instalam as atualizações de software sejam reiniciados por predefinição. No entanto, este método pode deixar os computadores num estado não seguro, enquanto que um reinício forçado ajudará a assegurar a conclusão imediata da instalação da atualização de software.  

    - **Para dispositivos Windows Embedded de processamento do filtro de escrita**: Quando implementa atualizações de software em dispositivos Windows Embedded que tenham o filtro de escrita ativado, pode especificar a instalar a atualização de software na sobreposição temporária e ou confirmar as alterações mais tarde ou por confirmar as alterações no prazo de instalação ou durante uma janela de manutenção. Ao consolidar alterações no momento da instalação ou durante uma janela de manutenção, será necessário um reinício para que as alterações sejam mantidas no dispositivo.  

        - Ao implementar uma atualização de software num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada.  

7.  Na página alertas, configure o Configuration Manager e o System Center Operations Manager gerarão alertas para esta implementação. Pode rever os alertas de atualizações de software recentes a partir do nó **Atualizações de Software** da área de trabalho **Biblioteca de Software** .  

8. Na página Definições de Transferência, configure as seguintes definições:  

    - Especifique se os clientes devem transferir e instalar as atualizações de software quando estão ligados a uma rede lenta ou utilizar uma localização de conteúdo de contingência.  

    - Especifique se pretende que o cliente transfira e instale as atualizações de software a partir de um ponto de distribuição de contingência quando o conteúdo das atualizações de software não estiver disponível num ponto de distribuição preferencial.  

    - **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**: Especifique se pretende ativar a utilização do BranchCache para as transferências de conteúdos. Para obter mais informações sobre o BranchCache, veja [Conceitos para a gestão de conteúdos](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Se as atualizações de software não estão disponíveis no ponto de distribuição na atual, vizinho ou site grupos, transferir conteúdo do Microsoft Updates**: Selecione esta definição para que os clientes de intranet ligada transferir as atualizações de software do Microsoft Update caso as atualizações não estejam disponíveis nos pontos de distribuição. Os clientes baseados na Internet podem sempre aceder ao Microsoft Update para o conteúdo de atualizações de software.

    - Especifique se pretende permitir que os clientes efetuem a transferência após um prazo de instalação se estiverem a utilizar ligações à Internet com tráfego limitado. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à Internet com tráfego limitado.  

    > [!NOTE]  
    > Os clientes solicitam a localização de conteúdo a partir de um ponto de gestão para as atualizações de software de uma implementação. O comportamento de transferência dependerá da forma como tiver configurado o ponto de distribuição, o pacote de implementação e as definições desta página. Para obter mais informações, veja [Cenários de localização da origem de conteúdo](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

Para obter mais informações sobre o processo de implementação, veja [Processo de implementação de atualizações de software](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Passos seguintes
[Monitorizar atualizações de software](monitor-software-updates.md)

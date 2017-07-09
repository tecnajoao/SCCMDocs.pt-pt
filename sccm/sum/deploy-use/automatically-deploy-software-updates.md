---
title: "Implantar automaticamente atualizações de software | Microsoft Docs"
description: "Implante automaticamente atualizações de software adicionando novas atualizações a um grupo de atualização que está associado a uma implantação ativa ou usando ADRs."
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
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.translationtype: Machine Translation
ms.sourcegitcommit: c6ee0ed635ab81b5e454e3cd85637ff3e20dbb34
ms.openlocfilehash: 804a9d7a32cfbdb498c6748c5d99a1874261c231
ms.contentlocale: pt-pt
ms.lasthandoff: 06/08/2017

---

#  <a name="BKMK_AutoDeploy"></a> Implementar automaticamente atualizações de software  

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

 Você pode implantar automaticamente atualizações de software adicionando novas atualizações de software a um grupo de atualização associado a uma implantação ativa ou você pode usar uma implantação automática ADR (regra). Normalmente, você usará ADRs mensal implantar atualizações de software (geralmente conhecidas como atualizações de terça-feira de Patch) e para gerenciar atualizações de definição. Se você precisar de ajuda para determinar qual implantação método é ideal para você, consulte [implantar atualizações de software](deploy-software-updates.md)

##  <a name="BKMK_AddUpdatesToExistingGroup"></a> Adicionar atualizações de software a um grupo de atualização implementado  
Depois de criar e implantar um grupo de atualização de software, você pode adicionar atualizações de software para o grupo de atualização e elas serão implantadas automaticamente.  

> [!IMPORTANT]  
>  Quando adicionar atualizações de software a um grupo de atualização de software existente que já tenha sido implementado, as atualizações de software adicionais poderão demorar alguns minutos a serem adicionadas à implementação.  

Utilize o seguinte procedimento para adicionar atualizações de software a um grupo de atualização existente.  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>Para adicionar atualizações de software a um grupo de atualização de software existente  

1.  No console do Configuration Manager, navegue até **biblioteca de Software** > **visão geral** > **atualizações de Software**.  

2.  Selecione as atualizações de software que pretende adicionar ao novo grupo de atualização de software.  

3.  No separador **Home Page** , no grupo **Atualizar** , clique em **Editar Associação**.  

4.  Selecione o grupo de atualização de software ao qual pretende adicionar as atualizações de software como membros.  

5.  Clique no nó **Grupos de Atualização de Software** para apresentar o grupo de atualização de software.  

6.  Clique no grupo de atualização de software e, no separador **Home Page** , no grupo **Atualizar** , clique em **Mostrar Membros** para ver uma lista das atualizações de software do grupo.  

##  <a name="BKMK_CreateAutomaticDeploymentRule"></a> Criar uma regra de implementação automática (ADR)  
Pode aprovar e implementar automaticamente atualizações de software utilizando uma ADR. Pode fazer com que a regra adicione atualizações de software a um novo grupo de atualização de software de cada vez que a regra for executada ou adicionar atualizações de software a um grupo existente. Quando uma regra for executada e adicionar atualizações de software a um grupo existente, a regra remove todas as atualizações de software do grupo e, em seguida, adiciona as atualizações de software que cumprem os critérios que definiu para o grupo. Para executar uma ADR para localizar atualizações de software recentemente publicadas todos os dias e implementá-las nos clientes, por exemplo, tem de escolher a opção para criar um novo grupo de atualizações de software em vez de adicionar as atualizações de software a um grupo existente.  

> [!WARNING]  
>  Antes de criar uma ADR pela primeira vez, certifique-se de que a sincronização de atualizações de software foi concluída no site. Isso é particularmente importante quando você executa do Configuration Manager com um idioma diferente do inglês, porque classificações de atualização de software são exibidas em inglês antes da primeira sincronização e, em seguida, são exibidas no idioma localizado após a conclusão da sincronização de atualização de software. As regras que tiver criado antes de sincronizar as atualizações de software poderão não funcionar corretamente após a sincronização devido à discrepância da cadeia de texto.  

 Utilize o procedimento seguinte para criar uma ADR.  

#### <a name="to-create-an-adr"></a>Para criar uma ADR  

1.  No console do Configuration Manager, navegue até **biblioteca de Software** **visão geral** > **atualizações de Software** > **regras de implantação automática**.  

2.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Regra de Implementação Automática**. O Assistente de Criação de Regra de Implementação Automática abre.  

3.  Na página **Geral** , configure as seguintes definições:  

    -   **Nome**: Especifique o nome para a ADR. O nome deve ser exclusivo, ajudam a descrever a finalidade da regra e identificá-lo de outros usuários no site do Configuration Manager.  

    -   **Descrição**: Especifique uma descrição para a ADR. A descrição deve fornecer uma visão geral da regra de implantação e qualquer outra informação relevante que ajude a identificar e diferenciá-la entre outras no site do Configuration Manager. O campo de descrição é opcional, tem um limite de 256 caracteres e está em branco por predefinição.  

    -   **Selecione o modelo de implantação**: Especifique se deseja aplicar um modelo de implantação salvo anteriormente. Pode configurar um modelo de implementação para incluir várias propriedades comuns de implementação da atualização de software que podem ser utilizadas ao criar ADRs. Estes modelos ajudam a assegurar a consistência entre implementações semelhantes e a poupar tempo.  

         Pode selecionar entre os modelos de implementação de atualizações de software incorporados a partir do Assistente de Criação de Regra de Implementação Automática. O modelo **Atualizações de Definição** fornece definições comuns a utilizar quando implementa atualizações de software de definições. O modelo **Patch Terça** fornece definições comuns a utilizar quando implementa atualizações de software num ciclo mensal.  

    -   **Coleção**: Especifica a coleção de destino a ser usado para a implantação. Os membros da coleção recebem as atualizações de software definidas na implementação.  

    -   Especifique se pretende adicionar atualizações de software a um grupo de atualização de software novo ou existente. Na maioria dos casos, optará provavelmente por criar um novo grupo de atualizações de software quando a ADR for executada. No entanto, poderá optar por utilizar um grupo existente se a regra for executada com base numa agenda mais intensiva. Por exemplo, se pretender executar a regra diariamente para atualizações de definições, poderá adicionar as atualizações de software a um grupo de atualização de software existente.  

    -   **Habilitar a implantação após esta regra é executada**: Especifique se deseja habilitar a implantação de atualização de software após a execução da ADR. Relativamente a esta especificação deverá ter em conta os seguintes aspetos:  

        -   Quando ativar a implementação, as atualizações de software que cumpram os critérios definidos na regra são adicionadas a um grupo de atualização de software, os conteúdos de atualização de software são transferidos, se necessário, os conteúdos são copiados para os pontos de distribuição especificados e as atualizações de software são implementadas nos clientes da coleção de destino.  

        -   Se não ativar a implementação, as atualizações de software que cumpram os critérios definidos na regra são adicionadas a um grupo de atualização de software e a política de implementação de atualizações de software é configurada, mas as atualizações de software não são transferidas ou implementadas nos clientes. Esta situação disponibiliza o tempo necessário à preparação da implementação das atualizações de software, à confirmação de que as atualizações de software que cumprem os critérios são adequadas e, posteriormente, à ativação da implementação para um momento futuro.  

4.  Na página Definições de Implementação, configure as seguintes definições:  

    -   **Usar Wake-on-LAN para ativar clientes para implantações obrigatórias**: Especifica se deseja habilitar o Wake On LAN no prazo para enviar pacotes de ativação para computadores que exigem uma ou mais atualizações de software na implantação. Todos os computadores que se encontrem em modo de suspensão durante o prazo previsto para a instalação serão reativados para que a instalação da atualização de software possa ser iniciada. Os clientes que se encontrem no modo de suspensão e que não necessitem de quaisquer atualizações de software no âmbito da implementação não serão iniciados. Por predefinição, esta definição não está ativada.  

        > [!WARNING]  
        >  Para poder utilizar esta opção, necessita de configurar os computadores e as redes para a Reativação por LAN.  

    -   **Nível de detalhe**: Especifique o nível de detalhe para as mensagens de estado são relatadas pelos computadores cliente.  

        > [!IMPORTANT]  
        >  Ao implementar atualizações de definições, defina o nível de detalhe como **Apenas erros** para que o cliente apenas envie uma mensagem de estado quando não for possível entregar uma atualização de definições ao cliente. Caso contrário, o cliente enviará um elevado número de mensagens de estado, o que poderá afetar o desempenho do servidor do site.  

    -   **Configuração dos termos da licença**: Especifique se deseja implantar automaticamente atualizações de software com os termos de licença associados. Algumas atualizações de software incluem termos de licenciamento, por exemplo um pacote de serviço. Ao implementar atualizações de software automaticamente, os termos de licenciamento não são apresentados e não haverá a opção de aceitação dos termos de licenciamento. Pode optar por implementar automaticamente todas as atualizações de software, independentemente dos termos de licenciamento associados, ou implementar apenas as atualizações de software que não tenham termos de licenciamento associados.  

        > [!NOTE]  
        >  Para rever os termos de licenciamento de uma atualização de software, pode selecionar a atualização de software no nó **Todas as Atualizações de Software** da área de trabalho **Biblioteca de Software** e, em seguida, no separador **Home Page** , no grupo **Atualizar** , clique em **Rever Licenciamento**.  
        >   
        >  Para localizar as atualizações de software que tenham termos de licenciamento associados, adicione a coluna **Termos de Licenciamento** à coluna de resultados do nó **Todas as Atualizações de Software** e, em seguida, clique no título da coluna para ordenar pelas atualizações de software que tenham termos de licenciamento.  

5.  Na página Atualizações de Software, configure os critérios para as atualizações de software que são obtidas e adicionadas pela ADR ao grupo de atualizações de software.  

    > [!IMPORTANT]  
    >  O limite para as atualizações de software na ADR é de 1000 atualizações de software. Para certificar-se de que os critérios que especifica nesta página obtêm menos de 1000 atualizações de software, considere definir os mesmos critérios no nó **Todas as Atualizações de Software** da área de trabalho **Biblioteca de Software** .  

    > [!NOTE]
    > A partir do Configuration Manager versão 1610, você pode filtrar o tamanho do conteúdo para atualizações de software em regras de implantação automática. Por exemplo, você pode definir o **conteúdo tamanho (KB)** filtrar para **< 2048** apenas baixar atualizações de software que são menores que 2 MB. Usar este filtro impede que as atualizações de software grandes baixando automaticamente para melhor suporte simplificado Windows quando a largura de banda de rede está limitada de serviço de nível inferior. Para obter detalhes, consulte [do Configuration Manager e simplificado serviço do Windows em busca sistemas operacionais de nível](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

6.  Na página Agenda de Avaliação, especifique se pretende ativar a execução da ADR com base numa agenda. Se estiver ativada, clique em **Personalizar** para definir a agenda periódica.  

    > [!IMPORTANT]  
    >  A agenda de sincronização do ponto de atualização de software é apresentada para ajudá-lo a determinar a frequência da agenda de avaliação. Nunca deverá definir uma agenda de avaliação com uma frequência que exceda a da agenda de sincronização de atualizações de software. A configuração do horário de início da agenda baseia-se na hora local do computador que executa o console do Configuration Manager.  

    > [!NOTE]  
    >  Para executar manualmente a ADR, selecione a regra e, em seguida, clique em **Executar agora** no separador **Home Page** do grupo **Regra de Implementação Automática** . Antes de executar manualmente a ADR, certifique-se de que a sincronização de atualizações de software foi executada desde a última vez que executou a regra.  

    > [!IMPORTANT]  
    >  A avaliação da ADR pode ser executada, no máximo, três vezes por dia.  

7.  Na página Agenda de Implementação, configure as seguintes definições:  

    -   **Avaliação do agendamento**: Especifique se o Configuration Manager avalia o tempo disponível e os prazos de instalação usando UTC ou horário local do computador que executa o console do Configuration Manager.  

        > [!NOTE]  
        >  Quando você seleciona a hora local e, em seguida, selecione **assim que possível** para o **tempo disponível do Software** ou **prazo de instalação**, a hora atual no computador que executa o console do Configuration Manager é usado para avaliar quando as atualizações estiverem disponíveis ou quando eles são instalados em um cliente. Se o cliente tiver um fuso horário diferente, estas ações irão ocorrer quando a hora do cliente corresponder à hora de avaliação.  

    -   **Tempo disponível do software**: Selecione uma das configurações a seguir para especificar quando as atualizações de software estão disponíveis para clientes:  

        -   **Assim que possível**: Selecione esta configuração para disponibilizar as atualizações de software que são incluídas na implantação aos computadores cliente assim que possível. Quando você cria a implantação com essa configuração selecionada, o Configuration Manager atualiza a política do cliente. Em seguida, durante o ciclo seguinte de consulta da política de cliente, os clientes ficarão informados da implementação e poderão obter as atualizações que estiverem disponíveis para instalação.  

        -   **Horário específico**: Selecione esta configuração para disponibilizar as atualizações de software incluídas na implantação aos computadores cliente em uma data e hora específicas. Quando você cria a implantação com essa configuração habilitada, o Configuration Manager atualiza a política do cliente. Em seguida, durante o ciclo de consulta seguinte da política de cliente, os clientes estarão informados da implementação. No entanto, as atualizações de software da implementação não ficarão disponíveis para instalação antes da data e hora configuradas.  

    -   **Prazo de instalação**: Selecione uma das configurações a seguir para especificar o prazo de instalação das atualizações de software na implantação:  

        -   **Assim que possível**: Selecione esta configuração para instalar automaticamente as atualizações de software na implantação assim que possível.  

        -   **Horário específico**: Selecione esta configuração para instalar automaticamente as atualizações de software na implantação em uma data e hora específicas. O Configuration Manager determina o prazo para instalar as atualizações de software, adicionando configurado **tempo específico** intervalo para o **tempo disponível do Software**.  

        > [!NOTE]  
        >  A hora real do prazo de instalação corresponde à hora apresentada acrescida de um período de tempo aleatório de até 2 horas. Desta forma, reduzirá o impacto potencial da instalação das atualizações de software da implementação ao mesmo tempo em todos os computadores cliente da coleção de destino.  
        >   
        >  Pode configurar a definição de cliente **Agente do Computador** , **Desativar a aleatoriedade de prazos** para desativar o atraso de aleatoriedade da instalação para as atualizações de software necessárias. Para obter mais informações, veja [Agente do Computador](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8. Na página Experiência de Utilizador, configure as seguintes definições:  

    -   **Notificações de usuário**: Especifique se deseja exibir notificações das atualizações de software no Centro de Software no computador cliente no configurado **tempo disponível do Software** e se deseja exibir as notificações de usuário nos computadores cliente.  

    -   **Comportamento do prazo**: Especifique o comportamento que deve ocorrer quando o prazo é alcançado para a implantação de atualização de software. Especifique se pretende instalar as atualizações de software da implementação. Especifique também se pretende reiniciar o sistema após a instalação da atualização de software, independentemente de uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção, consulte [como usar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento de reinício de dispositivo**: Especifique se deseja suprimir uma reinicialização do sistema em servidores e estações de trabalho depois que as atualizações de software são instaladas e uma reinicialização do sistema é necessária para concluir a instalação.  

        > [!IMPORTANT]  
        >  A supressão dos reinícios de sistema pode ser útil em ambientes de servidor ou em casos em que não pretenda que os computadores que instalam as atualizações de software sejam reiniciados por predefinição. No entanto, este método pode deixar os computadores num estado não seguro, enquanto que um reinício forçado ajudará a assegurar a conclusão imediata da instalação da atualização de software.  

    -   **Tratamento de dispositivos Windows Embedded com filtro de gravação**: Quando você implanta atualizações de software para dispositivos Windows Embedded habilitados com filtro de gravação, você pode especificar para instalar a atualização de software na sobreposição temporária e que as alterações sejam confirmação mais tarde ou confirmar as alterações no prazo da instalação ou durante uma janela de manutenção. Ao consolidar alterações no momento da instalação ou durante uma janela de manutenção, será necessário um reinício para que as alterações sejam mantidas no dispositivo.  

        > [!NOTE]  
        >  Ao implementar uma atualização de software num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada.  

    - **Comportamento de reavaliação de implantação após a reinicialização de atualizações de software**: A partir do Configuration Manager versão 1606, selecione essa configuração para configurar implantações de atualizações de software para que os clientes executem uma verificação de conformidade de atualizações de software imediatamente depois que um cliente instala o software de atualizações e reinicia. Isto permite ao cliente verificar a existência de atualizações de software adicionais que se tornam aplicáveis após o cliente ser reiniciado e, em seguida, instalá-las (e ficam em conformidade) durante a mesma janela de manutenção.

9. Na página alertas, configure como Configuration Manager e o System Center Operations Manager irão gerar alertas para essa implantação.  

    > [!NOTE]  
    >  Pode rever os alertas de atualizações de software recentes a partir do nó **Atualizações de Software** da área de trabalho **Biblioteca de Software** .  

10. Na página Definições de Transferência, configure as seguintes definições:  

    - Especifique se o cliente irá transferir e instalar as atualizações de software quando estiver ligado a uma rede lenta ou estiver a utilizar uma localização de conteúdos de contingência.  

    - Especifique se pretende que o cliente transfira e instale as atualizações de software a partir de um ponto de distribuição de contingência quando o conteúdo das atualizações de software não estiver disponível num ponto de distribuição preferencial.  

    - **Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede**: Especifique se deseja habilitar o uso do BranchCache para downloads de conteúdo. Para obter mais informações sobre o BranchCache, veja [Conceitos para a gestão de conteúdos](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Se as atualizações de software não estão disponíveis no ponto de distribuição no atual, vizinho ou site grupos, fazer download de conteúdo de Microsoft Updates**: Selecione esta configuração para os clientes que estão conectados para as intranet devem baixar atualizações de software do Microsoft Update se as atualizações de software não estão disponíveis nos pontos de distribuição. Clientes baseados na Internet sempre podem ir para o Microsoft Update para o conteúdo de atualizações de software.

    - Especifique se pretende permitir que os clientes efetuem a transferência após um prazo de instalação se estiverem a utilizar ligações à Internet com tráfego limitado. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à Internet com tráfego limitado.  

    > [!NOTE]  
    >  Os clientes solicitam a localização de conteúdo a partir de um ponto de gestão para as atualizações de software de uma implementação. O comportamento de transferência dependerá da forma como tiver configurado o ponto de distribuição, o pacote de implementação e as definições desta página. Para obter mais informações, veja [Cenários de localização da origem de conteúdo](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. Na página Pacote de Implementação, selecione um pacote de implementação existente ou configure as seguintes definições para criar um novo pacote de implementação:  

    1.  **Nome**: Especifique o nome do pacote de implantação. Tem de ser um nome exclusivo que descreva o conteúdo do pacote. Está limitado a 50 carateres.  

    2.  **Descrição**: Especifique uma descrição que fornece informações sobre o pacote de implantação. A descrição está limitada a 127 caracteres.  

    3.  **Origem do pacote**: Especifica o local dos arquivos de origem de atualização de software.  Escreva um caminho de rede para a localização de origem, como, por exemplo, **\\\server\sharename\path**ou clique em **Procurar** para procurar a localização de rede. Antes de continuar para a página seguinte, terá de criar a pasta partilhada para os ficheiros de origem do pacote de implementação.  

        > [!NOTE]  
        >  A localização de origem do pacote de implementação que especificar não poderá ser utilizada por outro pacote de implementação de software.  

        > [!IMPORTANT]  
        >  Tanto a conta de computador do Fornecedor de SMS, como o utilizador que executar o assistente para transferir as atualizações de software, têm de ter permissões NTFS de **Escrita** na localização de transferência. Deverá restringir cuidadosamente o acesso à localização de transferência para reduzir o risco de adulteração dos ficheiros de origem de atualização de software por parte de atacantes.  

        > [!IMPORTANT]  
        >  Você pode alterar o local de origem do pacote nas propriedades do pacote de implantação depois que o Configuration Manager cria o pacote de implantação. Mas se o fizer, terá primeiro de copiar o conteúdo da origem inicial do pacote para a nova localização de origem do pacote.  

    4.  **Prioridade de envio**: Especifique a prioridade de envio do pacote de implantação. Configuration Manager usa a prioridade de envio do pacote de implantação quando envia o pacote para pontos de distribuição. Pacotes de implantação são enviados na ordem de prioridade: Alta, média ou baixa. Os pacotes com prioridades idênticas são enviados pela ordem em que foram criados. Se não existirem tarefas pendentes, o pacote será processado de imediato, independentemente da sua prioridade.  

12. Na página Pontos de Distribuição, especifique os pontos de distribuição ou grupos de pontos de distribuição que irão alojar os ficheiros de atualização de software. Para obter mais informações sobre os pontos de distribuição, veja [Configurações de pontos de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!NOTE]  
    >  Esta página apenas está disponível ao criar um novo pacote de implementação da atualização de software.  

13. Na página Localização de Transferência, especifique se pretende transferir os ficheiros de atualização de software a partir da Internet ou da rede local. Configure as seguintes definições:  

    -   **Baixar atualizações de software da Internet**: Selecione esta configuração para baixar as atualizações de software de um local específico na Internet. Esta definição está ativada por predefinição.  

    -   **Baixar atualizações de software de um local na rede local**: Selecione esta configuração para baixar as atualizações de software de um diretório local ou pasta compartilhada. Esta definição é útil se o computador que executa o assistente não tiver acesso à Internet. Qualquer computador que disponha de acesso à Internet poderá transferir provisoriamente as atualizações de software e guardá-las numa localização da rede local que esteja acessível ao computador que executa o assistente.  

14. Na página Seleção de Idioma, selecione os idiomas para os quais serão transferidas as atualizações de software selecionadas. As atualizações de software apenas são transferidas se estiverem disponíveis nos idiomas selecionados. As atualizações de software que não sejam específicas do idioma serão sempre transferidas. Por predefinição, o assistente seleciona os idiomas que tiver configurado nas propriedades do ponto de atualização de software. Terá de estar selecionado pelo menos um idioma para que possa prosseguir para a página seguinte. Se selecionar apenas idiomas que não sejam suportados por uma atualização de software, a transferência da atualização de software não será concluída com êxito.  

15. Reveja as definições na página Resumo. Para guardar as definições num modelo de implementação, clique em **Guardar Como Modelo**, introduza um nome, selecione as definições que pretende incluir no modelo e, em seguida, clique em **Guardar**. Para alterar uma definição configurada, clique na página do assistente associada e altere a definição.  

    > [!NOTE]  
    >  O nome do modelo pode incluir carateres ASCII alfanuméricos, bem como **\\** (barra invertida) ou **‘** (plica).  

16. Clique em **Seguinte** para criar a ADR.  

 Depois de concluir o assistente, a ADR será executada. Esta irá adicionar as atualizações de software que cumpram os critérios especificados a um grupo de atualização de software, transferir as atualizações de software para a biblioteca de conteúdos do servidor do site, distribuir as atualizações de software aos pontos de distribuição configurados e, em seguida, implementar o grupo de atualização de software nos clientes da coleção de destino.  

##  <a name="BKMK_AddDeploymentToADR"></a> Adicionar uma nova implementação a uma ADR existente  
 Depois de criar uma ADR, pode adicionar mais implementações à regra. Isto pode ajudá-lo a gerir a complexidade da implementação de diferentes atualizações em diferentes coleções. Cada nova implementação tem acesso a todas as funcionalidades e à experiência de monitorização da implementação.  

#### <a name="to-add-a-new-deployment-to-an-existing-adr"></a>Para adicionar uma nova implementação a uma ADR existente  

1.  No console do Configuration Manager, navegue até **biblioteca de Software** > **visão geral** > **atualizações de Software** > **regras de implantação automática**e, em seguida, selecione a regra desejada.  

2.  No separador **Home Page** , no grupo **Regra de Implementação Automática** , clique em **Adicionar Implementação**. O Assistente para Adicionar Implementação abre.  

3.  Na página **Coleção** , configure as seguintes definições:  

    -   **Coleção**: Especifica a coleção de destino a ser usado para a implantação. Os membros da coleção recebem as atualizações de software definidas na implementação.  

    -   **Habilitar a implantação após esta regra é executada**: Especifique se deseja habilitar a implantação de atualização de software após a execução da ADR. Relativamente a esta especificação deverá ter em conta os seguintes aspetos:  

        -   Quando ativar a implementação, as atualizações de software que cumpram os critérios definidos na regra são adicionadas a um grupo de atualização de software, os conteúdos de atualização de software são transferidos, se necessário, os conteúdos são copiados para os pontos de distribuição especificados e as atualizações de software são implementadas nos clientes da coleção de destino.  

        -   Se não ativar a implementação, as atualizações de software que cumpram os critérios definidos na regra são adicionadas a um grupo de atualização de software e a política de implementação de atualizações de software é configurada, mas as atualizações de software não são transferidas ou implementadas nos clientes. Esta situação disponibiliza o tempo necessário à preparação da implementação das atualizações de software, à confirmação de que as atualizações de software que cumprem os critérios são adequadas e, posteriormente, à ativação da implementação para um momento futuro.  

4.  Na página Definições de Implementação, configure as seguintes definições:  

    -   **Usar Wake-on-LAN para ativar clientes para implantações obrigatórias**: Especifica se deseja habilitar o Wake On LAN no prazo para enviar pacotes de ativação para computadores que exigem uma ou mais atualizações de software na implantação. Todos os computadores que se encontrem em modo de suspensão durante o prazo previsto para a instalação serão reativados para que a instalação da atualização de software possa ser iniciada. Os clientes que se encontrem no modo de suspensão e que não necessitem de quaisquer atualizações de software no âmbito da implementação não serão iniciados. Por predefinição, esta definição não está ativada.  

        > [!WARNING]  
        >  Para poder utilizar esta opção, necessita de configurar os computadores e as redes para a Reativação por LAN.  

    -   **Nível de detalhe**: Especifique o nível de detalhe para as mensagens de estado são relatadas pelos computadores cliente.  

        > [!IMPORTANT]  
        >  Ao implementar atualizações de definições, defina o nível de detalhe como **Apenas erros** para que o cliente apenas envie uma mensagem de estado quando não for possível entregar uma atualização de definições ao cliente. Caso contrário, o cliente enviará um elevado número de mensagens de estado, o que poderá afetar o desempenho do servidor do site.  

5.  Na página Agenda de Implementação, configure as seguintes definições:  

    -   **Avaliação do agendamento**: Especifique se o Configuration Manager avalia o tempo disponível e os prazos de instalação usando UTC ou horário local do computador que executa o console do Configuration Manager.  

        > [!NOTE]  
        >  Quando você seleciona a hora local e, em seguida, selecione **assim que possível** para o **tempo disponível do Software** ou **prazo de instalação**, a hora atual no computador que executa o console do Configuration Manager é usado para avaliar quando as atualizações estiverem disponíveis ou quando eles são instalados em um cliente. Se o cliente tiver um fuso horário diferente, estas ações irão ocorrer quando a hora do cliente corresponder à hora de avaliação.  

    -   **Tempo disponível do software**: Selecione uma das configurações a seguir para especificar quando as atualizações de software estão disponíveis para clientes:  

        -   **Assim que possível**: Selecione esta configuração para disponibilizar as atualizações de software que são incluídas na implantação aos computadores cliente assim que possível. Quando você cria a implantação com essa configuração selecionada, o Configuration Manager atualiza a política do cliente. Em seguida, durante o ciclo seguinte de consulta da política de cliente, os clientes ficarão informados da implementação e poderão obter as atualizações que estiverem disponíveis para instalação.  

        -   **Horário específico**: Selecione esta configuração para disponibilizar as atualizações de software incluídas na implantação aos computadores cliente em uma data e hora específicas. Quando você cria a implantação com essa configuração habilitada, o Configuration Manager atualiza a política do cliente. Em seguida, durante o ciclo de consulta seguinte da política de cliente, os clientes estarão informados da implementação. No entanto, as atualizações de software da implementação não ficarão disponíveis para instalação antes da data e hora configuradas.  

    -   **Prazo de instalação**: Selecione uma das configurações a seguir para especificar o prazo de instalação das atualizações de software na implantação:  

        -   **Assim que possível**: Selecione esta configuração para instalar automaticamente as atualizações de software na implantação assim que possível.  

        -   **Horário específico**: Selecione esta configuração para instalar automaticamente as atualizações de software na implantação em uma data e hora específicas. O Configuration Manager determina o prazo para instalar as atualizações de software, adicionando configurado **tempo específico** intervalo para o **tempo disponível do Software**.  

        > [!NOTE]  
        >  A hora real do prazo de instalação corresponde à hora apresentada acrescida de um período de tempo aleatório de até 2 horas. Desta forma, reduzirá o impacto potencial da instalação das atualizações de software da implementação ao mesmo tempo em todos os computadores cliente da coleção de destino.  
        >   
        >  Pode configurar a definição de cliente **Agente do Computador** , **Desativar a aleatoriedade de prazos** para desativar o atraso de aleatoriedade da instalação para as atualizações de software necessárias. Para obter mais informações, veja [Agente do Computador](../../core/clients/deploy/about-client-settings.md#computer-agent).  

6.  Na página Experiência de Utilizador, configure as seguintes definições:  

    -   **Notificações de usuário**: Especifique se deseja exibir notificações das atualizações de software no Centro de Software no computador cliente no configurado **tempo disponível do Software** e se deseja exibir as notificações de usuário nos computadores cliente.  

    -   **Comportamento do prazo**: Especifique o comportamento que deve ocorrer quando o prazo é alcançado para a implantação de atualização de software. Especifique se pretende instalar as atualizações de software da implementação. Especifique também se pretende reiniciar o sistema após a instalação da atualização de software, independentemente de uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção, consulte [como usar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento de reinício de dispositivo**: Especifique se deseja suprimir uma reinicialização do sistema em servidores e estações de trabalho depois que as atualizações de software são instaladas e uma reinicialização do sistema é necessária para concluir a instalação.  

        > [!IMPORTANT]  
        >  A supressão dos reinícios de sistema pode ser útil em ambientes de servidor ou em casos em que não pretenda que os computadores que instalam as atualizações de software sejam reiniciados por predefinição. No entanto, este método pode deixar os computadores num estado não seguro, enquanto que um reinício forçado ajudará a assegurar a conclusão imediata da instalação da atualização de software.  

    -   **Tratamento de dispositivos Windows Embedded com filtro de gravação**: Quando você implanta atualizações de software para dispositivos Windows Embedded habilitados com filtro de gravação, você pode especificar para instalar a atualização de software na sobreposição temporária e que as alterações sejam confirmação mais tarde ou confirmar as alterações no prazo da instalação ou durante uma janela de manutenção. Ao consolidar alterações no momento da instalação ou durante uma janela de manutenção, será necessário um reinício para que as alterações sejam mantidas no dispositivo.  

        > [!NOTE]  
        >  Ao implementar uma atualização de software num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada.  

7.  Na página alertas, configure como Configuration Manager e o System Center Operations Manager irão gerar alertas para essa implantação.  

    > [!WARNING]  
    >  Pode rever os alertas de atualizações de software recentes a partir do nó **Atualizações de Software** da área de trabalho **Biblioteca de Software** .  

8. Na página Definições de Transferência, configure as seguintes definições:  

    - Especifique se o cliente irá transferir e instalar as atualizações de software quando estiver ligado a uma rede lenta ou estiver a utilizar uma localização de conteúdos de contingência.  

    - Especifique se pretende que o cliente transfira e instale as atualizações de software a partir de um ponto de distribuição de contingência quando o conteúdo das atualizações de software não estiver disponível num ponto de distribuição preferencial.  

    - **Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede**: Especifique se deseja habilitar o uso do BranchCache para downloads de conteúdo. Para obter mais informações sobre o BranchCache, veja [Conceitos para a gestão de conteúdos](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Se as atualizações de software não estão disponíveis no ponto de distribuição no atual, vizinho ou site grupos, fazer download de conteúdo de Microsoft Updates**: Selecione esta configuração para os clientes que estão conectados para as intranet devem baixar atualizações de software do Microsoft Update se as atualizações de software não estão disponíveis nos pontos de distribuição. Clientes baseados na Internet sempre podem ir para o Microsoft Update para o conteúdo de atualizações de software.

    - Especifique se pretende permitir que os clientes efetuem a transferência após um prazo de instalação se estiverem a utilizar ligações à Internet com tráfego limitado. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à Internet com tráfego limitado.  

    > [!NOTE]  
    > Os clientes solicitam a localização de conteúdo a partir de um ponto de gestão para as atualizações de software de uma implementação. O comportamento de transferência dependerá da forma como tiver configurado o ponto de distribuição, o pacote de implementação e as definições desta página. Para obter mais informações, veja [Cenários de localização da origem de conteúdo](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

Para obter mais informações sobre o processo de implementação, veja [Processo de implementação de atualizações de software](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Passos seguintes
[Monitorizar atualizações de software](monitor-software-updates.md)


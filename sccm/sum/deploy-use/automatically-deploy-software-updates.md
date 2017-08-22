---
title: "Implementar automaticamente atualizações de software | Microsoft Docs"
description: "Implemente automaticamente atualizações de software ao adicionar novas atualizações a um grupo de atualização que está associada a uma implementação ativa, ou utilizando ADRs."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: 804a9d7a32cfbdb498c6748c5d99a1874261c231
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_AutoDeploy"></a> Implementar automaticamente atualizações de software  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Pode implementar automaticamente atualizações de software ao adicionar novas atualizações de software a um grupo de atualização associado uma implementação ativa, ou pode utilizar uma regra de implementação automática (ADR). Normalmente, utilizará ADRs mensalmente implementar atualizações de software (geralmente conhecidas como Patch Terça-feira atualizações) e para gerir atualizações de definições. Se precisar de ajuda para determinar que implementação de método é mais adequado para si, consulte [implementar atualizações de software](deploy-software-updates.md)

##  <a name="BKMK_AddUpdatesToExistingGroup"></a> Adicionar atualizações de software a um grupo de atualização implementado  
Depois de criar e implementar um grupo de atualização de software, pode adicionar atualizações de software ao grupo de atualização e estas serão automaticamente implementadas.  

> [!IMPORTANT]  
>  Quando adicionar atualizações de software a um grupo de atualização de software existente que já tenha sido implementado, as atualizações de software adicionais poderão demorar alguns minutos a serem adicionadas à implementação.  

Utilize o seguinte procedimento para adicionar atualizações de software a um grupo de atualização existente.  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>Para adicionar atualizações de software a um grupo de atualização de software existente  

1.  Na consola do Configuration Manager, navegue até à **biblioteca de Software** > **descrição geral** > **atualizações de Software**.  

2.  Selecione as atualizações de software que pretende adicionar ao novo grupo de atualização de software.  

3.  No separador **Home Page** , no grupo **Atualizar** , clique em **Editar Associação**.  

4.  Selecione o grupo de atualização de software ao qual pretende adicionar as atualizações de software como membros.  

5.  Clique no nó **Grupos de Atualização de Software** para apresentar o grupo de atualização de software.  

6.  Clique no grupo de atualização de software e, no separador **Home Page** , no grupo **Atualizar** , clique em **Mostrar Membros** para ver uma lista das atualizações de software do grupo.  

##  <a name="BKMK_CreateAutomaticDeploymentRule"></a> Criar uma regra de implementação automática (ADR)  
Pode aprovar e implementar automaticamente atualizações de software utilizando uma ADR. Pode fazer com que a regra adicione atualizações de software a um novo grupo de atualização de software de cada vez que a regra for executada ou adicionar atualizações de software a um grupo existente. Quando uma regra for executada e adicionar atualizações de software a um grupo existente, a regra remove todas as atualizações de software do grupo e, em seguida, adiciona as atualizações de software que cumprem os critérios que definiu para o grupo. Para executar uma ADR para localizar atualizações de software recentemente publicadas todos os dias e implementá-las nos clientes, por exemplo, tem de escolher a opção para criar um novo grupo de atualizações de software em vez de adicionar as atualizações de software a um grupo existente.  

> [!WARNING]  
>  Antes de criar uma ADR pela primeira vez, certifique-se de que a sincronização de atualizações de software foi concluída no site. Isto é especialmente importante quando executar o Configuration Manager com um idioma diferente do inglês porque classificações de atualizações de software são apresentadas em inglês antes da primeira sincronização e, em seguida, no idioma localizado após a conclusão da sincronização de atualizações de software. As regras que tiver criado antes de sincronizar as atualizações de software poderão não funcionar corretamente após a sincronização devido à discrepância da cadeia de texto.  

 Utilize o procedimento seguinte para criar uma ADR.  

#### <a name="to-create-an-adr"></a>Para criar uma ADR  

1.  Na consola do Configuration Manager, navegue até à **biblioteca de Software** **descrição geral** > **atualizações de Software** > **regras de implementação automática**.  

2.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Regra de Implementação Automática**. O Assistente de Criação de Regra de Implementação Automática abre.  

3.  Na página **Geral** , configure as seguintes definições:  

    -   **Nome**: Especifique o nome para a ADR. O nome tem de ser exclusivo e deve descrever o objetivo da regra além de distingui-la de outras no site do Configuration Manager.  

    -   **Descrição**: Especifique uma descrição para a ADR. A descrição deve disponibilizar uma descrição geral da regra de implementação e outras informações relevantes que ajudem a identificar e distinguir a regra das restantes no site do Configuration Manager. O campo de descrição é opcional, tem um limite de 256 caracteres e está em branco por predefinição.  

    -   **Selecione o modelo de implementação**: Especifique se pretende aplicar um modelo de implementação anteriormente guardado. Pode configurar um modelo de implementação para incluir várias propriedades comuns de implementação da atualização de software que podem ser utilizadas ao criar ADRs. Estes modelos ajudam a assegurar a consistência entre implementações semelhantes e a poupar tempo.  

         Pode selecionar entre os modelos de implementação de atualizações de software incorporados a partir do Assistente de Criação de Regra de Implementação Automática. O modelo **Atualizações de Definição** fornece definições comuns a utilizar quando implementa atualizações de software de definições. O modelo **Patch Terça** fornece definições comuns a utilizar quando implementa atualizações de software num ciclo mensal.  

    -   **Coleção**: Especifica a coleção de destino a ser utilizado para a implementação. Os membros da coleção recebem as atualizações de software definidas na implementação.  

    -   Especifique se pretende adicionar atualizações de software a um grupo de atualização de software novo ou existente. Na maioria dos casos, optará provavelmente por criar um novo grupo de atualizações de software quando a ADR for executada. No entanto, poderá optar por utilizar um grupo existente se a regra for executada com base numa agenda mais intensiva. Por exemplo, se pretender executar a regra diariamente para atualizações de definições, poderá adicionar as atualizações de software a um grupo de atualização de software existente.  

    -   **Ativar a implementação após a execução desta regra**: Especifique se pretende ativar a implementação de atualização de software após a execução da ADR. Relativamente a esta especificação deverá ter em conta os seguintes aspetos:  

        -   Quando ativar a implementação, as atualizações de software que cumpram os critérios definidos na regra são adicionadas a um grupo de atualização de software, os conteúdos de atualização de software são transferidos, se necessário, os conteúdos são copiados para os pontos de distribuição especificados e as atualizações de software são implementadas nos clientes da coleção de destino.  

        -   Se não ativar a implementação, as atualizações de software que cumpram os critérios definidos na regra são adicionadas a um grupo de atualização de software e a política de implementação de atualizações de software é configurada, mas as atualizações de software não são transferidas ou implementadas nos clientes. Esta situação disponibiliza o tempo necessário à preparação da implementação das atualizações de software, à confirmação de que as atualizações de software que cumprem os critérios são adequadas e, posteriormente, à ativação da implementação para um momento futuro.  

4.  Na página Definições de Implementação, configure as seguintes definições:  

    -   **Utilizar a reativação por LAN para reativar os clientes para as implementações necessárias**: Especifica se pretende ativar a reativação por LAN na data limite para o envio de pacotes de reativação para computadores que necessitem de uma ou mais atualizações de software na implementação. Todos os computadores que se encontrem em modo de suspensão durante o prazo previsto para a instalação serão reativados para que a instalação da atualização de software possa ser iniciada. Os clientes que se encontrem no modo de suspensão e que não necessitem de quaisquer atualizações de software no âmbito da implementação não serão iniciados. Por predefinição, esta definição não está ativada.  

        > [!WARNING]  
        >  Para poder utilizar esta opção, necessita de configurar os computadores e as redes para a Reativação por LAN.  

    -   **Nível de detalhe**: Especifique o nível de detalhe para as mensagens de estado que são enviadas pelos computadores cliente.  

        > [!IMPORTANT]  
        >  Ao implementar atualizações de definições, defina o nível de detalhe como **Apenas erros** para que o cliente apenas envie uma mensagem de estado quando não for possível entregar uma atualização de definições ao cliente. Caso contrário, o cliente enviará um elevado número de mensagens de estado, o que poderá afetar o desempenho do servidor do site.  

    -   **Definição de termos de licença**: Especifique se pretende implementar automaticamente atualizações de software com termos de licenciamento associados. Algumas atualizações de software incluem termos de licenciamento, por exemplo um pacote de serviço. Ao implementar atualizações de software automaticamente, os termos de licenciamento não são apresentados e não haverá a opção de aceitação dos termos de licenciamento. Pode optar por implementar automaticamente todas as atualizações de software, independentemente dos termos de licenciamento associados, ou implementar apenas as atualizações de software que não tenham termos de licenciamento associados.  

        > [!NOTE]  
        >  Para rever os termos de licenciamento de uma atualização de software, pode selecionar a atualização de software no nó **Todas as Atualizações de Software** da área de trabalho **Biblioteca de Software** e, em seguida, no separador **Home Page** , no grupo **Atualizar** , clique em **Rever Licenciamento**.  
        >   
        >  Para localizar as atualizações de software que tenham termos de licenciamento associados, adicione a coluna **Termos de Licenciamento** à coluna de resultados do nó **Todas as Atualizações de Software** e, em seguida, clique no título da coluna para ordenar pelas atualizações de software que tenham termos de licenciamento.  

5.  Na página Atualizações de Software, configure os critérios para as atualizações de software que são obtidas e adicionadas pela ADR ao grupo de atualizações de software.  

    > [!IMPORTANT]  
    >  O limite para as atualizações de software na ADR é de 1000 atualizações de software. Para certificar-se de que os critérios que especifica nesta página obtêm menos de 1000 atualizações de software, considere definir os mesmos critérios no nó **Todas as Atualizações de Software** da área de trabalho **Biblioteca de Software** .  

    > [!NOTE]
    > A partir do Configuration Manager versão 1610, pode filtrar o tamanho do conteúdo para atualizações de software nas regras de implementação automática. Por exemplo, pode definir o **conteúdo tamanho (KB)** filtrar para **< 2048** para transferir apenas atualizações de software que são inferior a 2 MB. Utilizar este filtro impede que as atualizações de software grande automaticamente a transferência para um melhor suporte simplificado Windows quando a largura de banda de rede é limitada de manutenção de nível inferior. Para obter mais informações, consulte [do Configuration Manager e simplificada manutenção do Windows em baixo nível de sistemas operativos](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

6.  Na página Agenda de Avaliação, especifique se pretende ativar a execução da ADR com base numa agenda. Se estiver ativada, clique em **Personalizar** para definir a agenda periódica.  

    > [!IMPORTANT]  
    >  A agenda de sincronização do ponto de atualização de software é apresentada para ajudá-lo a determinar a frequência da agenda de avaliação. Nunca deverá definir uma agenda de avaliação com uma frequência que exceda a da agenda de sincronização de atualizações de software. A configuração da hora de início da agenda baseia-se na hora local do computador que executa a consola do Configuration Manager.  

    > [!NOTE]  
    >  Para executar manualmente a ADR, selecione a regra e, em seguida, clique em **Executar agora** no separador **Home Page** do grupo **Regra de Implementação Automática** . Antes de executar manualmente a ADR, certifique-se de que a sincronização de atualizações de software foi executada desde a última vez que executou a regra.  

    > [!IMPORTANT]  
    >  A avaliação da ADR pode ser executada, no máximo, três vezes por dia.  

7.  Na página Agenda de Implementação, configure as seguintes definições:  

    -   **Avaliação da agenda**: Especifique se o Configuration Manager avalia o tempo disponível e tempos de prazo de instalação utilizando a hora UTC ou na hora local do computador que executa a consola do Configuration Manager.  

        > [!NOTE]  
        >  Quando selecionar a hora local e, em seguida, selecione **logo que possível** para o **hora de disponibilização do Software** ou **prazo de instalação**, a hora atual da execução de computador, a consola do Configuration Manager é utilizada para calcular quando estão disponíveis atualizações ou quando são instaladas num cliente. Se o cliente tiver um fuso horário diferente, estas ações irão ocorrer quando a hora do cliente corresponder à hora de avaliação.  

    -   **Hora de disponibilização do software**: Selecione uma das seguintes definições para especificar quando as atualizações de software são disponibilizadas aos clientes:  

        -   **Logo que possível**: Selecione esta definição para disponibilizar as atualizações de software que estão incluídas na implementação aos computadores cliente logo que possível. Quando criar a implementação com esta definição selecionada, o Configuration Manager atualiza a política de cliente. Em seguida, durante o ciclo seguinte de consulta da política de cliente, os clientes ficarão informados da implementação e poderão obter as atualizações que estiverem disponíveis para instalação.  

        -   **Hora específica**: Selecione esta definição para disponibilizar as atualizações de software que estão incluídas na implementação aos computadores cliente numa hora e data específicas. Quando criar a implementação com esta definição ativada, o Configuration Manager atualiza a política de cliente. Em seguida, durante o ciclo de consulta seguinte da política de cliente, os clientes estarão informados da implementação. No entanto, as atualizações de software da implementação não ficarão disponíveis para instalação antes da data e hora configuradas.  

    -   **Prazo de instalação**: Selecione uma das seguintes definições para especificar o prazo de instalação para as atualizações de software da implementação:  

        -   **Logo que possível**: Selecione esta definição para instalar automaticamente as atualizações de software na implementação logo que possível.  

        -   **Hora específica**: Selecione esta definição para instalar automaticamente as atualizações de software na implementação numa hora e data específicas. O Configuration Manager determina o prazo de instalação de atualizações de software adicionando configurada **hora específica** intervalo para o **hora de disponibilização do Software**.  

        > [!NOTE]  
        >  A hora real do prazo de instalação corresponde à hora apresentada acrescida de um período de tempo aleatório de até 2 horas. Desta forma, reduzirá o impacto potencial da instalação das atualizações de software da implementação ao mesmo tempo em todos os computadores cliente da coleção de destino.  
        >   
        >  Pode configurar a definição de cliente **Agente do Computador** , **Desativar a aleatoriedade de prazos** para desativar o atraso de aleatoriedade da instalação para as atualizações de software necessárias. Para obter mais informações, veja [Agente do Computador](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8. Na página Experiência de Utilizador, configure as seguintes definições:  

    -   **As notificações de utilizador**: Especifique se pretende apresentar a notificação de atualizações de software no Centro de Software no computador cliente à configurada **hora de disponibilização do Software** e se pretende apresentar as notificações de utilizador nos computadores cliente.  

    -   **Comportamento do prazo**: Especifique o comportamento a adotar quando é atingido o prazo para a implementação de atualização de software. Especifique se pretende instalar as atualizações de software da implementação. Especifique também se pretende reiniciar o sistema após a instalação da atualização de software, independentemente de uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção, consulte [como utilizar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento de reinício do dispositivo**: Especifique se pretende suprimir um reinício do sistema em servidores e estações de trabalho após as atualizações de software estão instaladas e reiniciar o sistema é necessário para concluir a instalação.  

        > [!IMPORTANT]  
        >  A supressão dos reinícios de sistema pode ser útil em ambientes de servidor ou em casos em que não pretenda que os computadores que instalam as atualizações de software sejam reiniciados por predefinição. No entanto, este método pode deixar os computadores num estado não seguro, enquanto que um reinício forçado ajudará a assegurar a conclusão imediata da instalação da atualização de software.  

    -   **Para dispositivos Windows Embedded de processamento do filtro de escrita**: Quando implementa atualizações de software em dispositivos Windows Embedded que tenham o filtro de escrita ativado, pode especificar a instalar a atualização de software na sobreposição temporária e ou confirmar as alterações mais tarde ou por confirmar as alterações no prazo de instalação ou durante uma janela de manutenção. Ao consolidar alterações no momento da instalação ou durante uma janela de manutenção, será necessário um reinício para que as alterações sejam mantidas no dispositivo.  

        > [!NOTE]  
        >  Ao implementar uma atualização de software num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada.  

    - **Comportamento de reavaliação de implementação após o reinício de atualizações de software**: A partir do Configuration Manager versão 1606, selecione esta definição para configurar as implementações de atualizações de software para que os clientes executem uma análise de compatibilidade de atualizações de software imediatamente após um cliente instalar o software, atualizações e reinicia. Isto permite ao cliente verificar a existência de atualizações de software adicionais que se tornam aplicáveis após o cliente ser reiniciado e, em seguida, instalá-las (e ficam em conformidade) durante a mesma janela de manutenção.

9. Na página alertas, configure o Configuration Manager e o System Center Operations Manager gerarão alertas para esta implementação.  

    > [!NOTE]  
    >  Pode rever os alertas de atualizações de software recentes a partir do nó **Atualizações de Software** da área de trabalho **Biblioteca de Software** .  

10. Na página Definições de Transferência, configure as seguintes definições:  

    - Especifique se o cliente irá transferir e instalar as atualizações de software quando estiver ligado a uma rede lenta ou estiver a utilizar uma localização de conteúdos de contingência.  

    - Especifique se pretende que o cliente transfira e instale as atualizações de software a partir de um ponto de distribuição de contingência quando o conteúdo das atualizações de software não estiver disponível num ponto de distribuição preferencial.  

    - **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**: Especifique se pretende ativar a utilização do BranchCache para as transferências de conteúdos. Para obter mais informações sobre o BranchCache, veja [Conceitos para a gestão de conteúdos](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Se as atualizações de software não estão disponíveis no ponto de distribuição na atual, vizinho ou site grupos, transferir conteúdo do Microsoft Updates**: Selecione esta definição para que os clientes que estão ligados as intranet transferir as atualizações de software do Microsoft Update caso as atualizações de software não estejam disponíveis nos pontos de distribuição. Os clientes baseados na Internet podem sempre aceder ao Microsoft Update para o conteúdo de atualizações de software.

    - Especifique se pretende permitir que os clientes efetuem a transferência após um prazo de instalação se estiverem a utilizar ligações à Internet com tráfego limitado. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à Internet com tráfego limitado.  

    > [!NOTE]  
    >  Os clientes solicitam a localização de conteúdo a partir de um ponto de gestão para as atualizações de software de uma implementação. O comportamento de transferência dependerá da forma como tiver configurado o ponto de distribuição, o pacote de implementação e as definições desta página. Para obter mais informações, veja [Cenários de localização da origem de conteúdo](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. Na página Pacote de Implementação, selecione um pacote de implementação existente ou configure as seguintes definições para criar um novo pacote de implementação:  

    1.  **Nome**: Especifique o nome do pacote de implementação. Tem de ser um nome exclusivo que descreva o conteúdo do pacote. Está limitado a 50 carateres.  

    2.  **Descrição**: Especifique uma descrição que disponibilize informações sobre o pacote de implementação. A descrição está limitada a 127 caracteres.  

    3.  **Origem do pacote**: Especifica a localização dos ficheiros de origem de atualização de software.  Escreva um caminho de rede para a localização de origem, como, por exemplo, **\\\server\sharename\path**ou clique em **Procurar** para procurar a localização de rede. Antes de continuar para a página seguinte, terá de criar a pasta partilhada para os ficheiros de origem do pacote de implementação.  

        > [!NOTE]  
        >  A localização de origem do pacote de implementação que especificar não poderá ser utilizada por outro pacote de implementação de software.  

        > [!IMPORTANT]  
        >  Tanto a conta de computador do Fornecedor de SMS, como o utilizador que executar o assistente para transferir as atualizações de software, têm de ter permissões NTFS de **Escrita** na localização de transferência. Deverá restringir cuidadosamente o acesso à localização de transferência para reduzir o risco de adulteração dos ficheiros de origem de atualização de software por parte de atacantes.  

        > [!IMPORTANT]  
        >  Pode alterar a localização de origem do pacote nas propriedades do pacote de implementação, após o Configuration Manager cria o pacote de implementação. Mas se o fizer, terá primeiro de copiar o conteúdo da origem inicial do pacote para a nova localização de origem do pacote.  

    4.  **Prioridade de envio**: Especifique a prioridade de envio para o pacote de implementação. O Configuration Manager utiliza a prioridade de envio para o pacote de implementação quando enviar o pacote para pontos de distribuição. Pacotes de implementação são enviados por ordem de prioridade: Alta, média ou baixa. Os pacotes com prioridades idênticas são enviados pela ordem em que foram criados. Se não existirem tarefas pendentes, o pacote será processado de imediato, independentemente da sua prioridade.  

12. Na página Pontos de Distribuição, especifique os pontos de distribuição ou grupos de pontos de distribuição que irão alojar os ficheiros de atualização de software. Para obter mais informações sobre os pontos de distribuição, veja [Configurações de pontos de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!NOTE]  
    >  Esta página apenas está disponível ao criar um novo pacote de implementação da atualização de software.  

13. Na página Localização de Transferência, especifique se pretende transferir os ficheiros de atualização de software a partir da Internet ou da rede local. Configure as seguintes definições:  

    -   **Transferir atualizações de software a partir da Internet**: Selecione esta definição para transferir as atualizações de software a partir de uma localização especificada na Internet. Esta definição está ativada por predefinição.  

    -   **Transferir atualizações de software a partir de uma localização na rede local**: Selecione esta definição para transferir as atualizações de software a partir de um diretório local ou uma pasta partilhada. Esta definição é útil se o computador que executa o assistente não tiver acesso à Internet. Qualquer computador que disponha de acesso à Internet poderá transferir provisoriamente as atualizações de software e guardá-las numa localização da rede local que esteja acessível ao computador que executa o assistente.  

14. Na página Seleção de Idioma, selecione os idiomas para os quais serão transferidas as atualizações de software selecionadas. As atualizações de software apenas são transferidas se estiverem disponíveis nos idiomas selecionados. As atualizações de software que não sejam específicas do idioma serão sempre transferidas. Por predefinição, o assistente seleciona os idiomas que tiver configurado nas propriedades do ponto de atualização de software. Terá de estar selecionado pelo menos um idioma para que possa prosseguir para a página seguinte. Se selecionar apenas idiomas que não sejam suportados por uma atualização de software, a transferência da atualização de software não será concluída com êxito.  

15. Reveja as definições na página Resumo. Para guardar as definições num modelo de implementação, clique em **Guardar Como Modelo**, introduza um nome, selecione as definições que pretende incluir no modelo e, em seguida, clique em **Guardar**. Para alterar uma definição configurada, clique na página do assistente associada e altere a definição.  

    > [!NOTE]  
    >  O nome do modelo pode incluir carateres ASCII alfanuméricos, bem como **\\** (barra invertida) ou **‘** (plica).  

16. Clique em **Seguinte** para criar a ADR.  

 Depois de concluir o assistente, a ADR será executada. Esta irá adicionar as atualizações de software que cumpram os critérios especificados a um grupo de atualização de software, transferir as atualizações de software para a biblioteca de conteúdos do servidor do site, distribuir as atualizações de software aos pontos de distribuição configurados e, em seguida, implementar o grupo de atualização de software nos clientes da coleção de destino.  

##  <a name="BKMK_AddDeploymentToADR"></a> Adicionar uma nova implementação a uma ADR existente  
 Depois de criar uma ADR, pode adicionar mais implementações à regra. Isto pode ajudá-lo a gerir a complexidade da implementação de diferentes atualizações em diferentes coleções. Cada nova implementação tem acesso a todas as funcionalidades e à experiência de monitorização da implementação.  

#### <a name="to-add-a-new-deployment-to-an-existing-adr"></a>Para adicionar uma nova implementação a uma ADR existente  

1.  Na consola do Configuration Manager, navegue até à **biblioteca de Software** > **descrição geral** > **atualizações de Software** > **regras de implementação automática**e, em seguida, selecione a regra pretendida.  

2.  No separador **Home Page** , no grupo **Regra de Implementação Automática** , clique em **Adicionar Implementação**. O Assistente para Adicionar Implementação abre.  

3.  Na página **Coleção** , configure as seguintes definições:  

    -   **Coleção**: Especifica a coleção de destino a ser utilizado para a implementação. Os membros da coleção recebem as atualizações de software definidas na implementação.  

    -   **Ativar a implementação após a execução desta regra**: Especifique se pretende ativar a implementação de atualização de software após a execução da ADR. Relativamente a esta especificação deverá ter em conta os seguintes aspetos:  

        -   Quando ativar a implementação, as atualizações de software que cumpram os critérios definidos na regra são adicionadas a um grupo de atualização de software, os conteúdos de atualização de software são transferidos, se necessário, os conteúdos são copiados para os pontos de distribuição especificados e as atualizações de software são implementadas nos clientes da coleção de destino.  

        -   Se não ativar a implementação, as atualizações de software que cumpram os critérios definidos na regra são adicionadas a um grupo de atualização de software e a política de implementação de atualizações de software é configurada, mas as atualizações de software não são transferidas ou implementadas nos clientes. Esta situação disponibiliza o tempo necessário à preparação da implementação das atualizações de software, à confirmação de que as atualizações de software que cumprem os critérios são adequadas e, posteriormente, à ativação da implementação para um momento futuro.  

4.  Na página Definições de Implementação, configure as seguintes definições:  

    -   **Utilizar a reativação por LAN para reativar os clientes para as implementações necessárias**: Especifica se pretende ativar a reativação por LAN na data limite para o envio de pacotes de reativação para computadores que necessitem de uma ou mais atualizações de software na implementação. Todos os computadores que se encontrem em modo de suspensão durante o prazo previsto para a instalação serão reativados para que a instalação da atualização de software possa ser iniciada. Os clientes que se encontrem no modo de suspensão e que não necessitem de quaisquer atualizações de software no âmbito da implementação não serão iniciados. Por predefinição, esta definição não está ativada.  

        > [!WARNING]  
        >  Para poder utilizar esta opção, necessita de configurar os computadores e as redes para a Reativação por LAN.  

    -   **Nível de detalhe**: Especifique o nível de detalhe para as mensagens de estado que são enviadas pelos computadores cliente.  

        > [!IMPORTANT]  
        >  Ao implementar atualizações de definições, defina o nível de detalhe como **Apenas erros** para que o cliente apenas envie uma mensagem de estado quando não for possível entregar uma atualização de definições ao cliente. Caso contrário, o cliente enviará um elevado número de mensagens de estado, o que poderá afetar o desempenho do servidor do site.  

5.  Na página Agenda de Implementação, configure as seguintes definições:  

    -   **Avaliação da agenda**: Especifique se o Configuration Manager avalia o tempo disponível e tempos de prazo de instalação utilizando a hora UTC ou na hora local do computador que executa a consola do Configuration Manager.  

        > [!NOTE]  
        >  Quando selecionar a hora local e, em seguida, selecione **logo que possível** para o **hora de disponibilização do Software** ou **prazo de instalação**, a hora atual da execução de computador, a consola do Configuration Manager é utilizada para calcular quando estão disponíveis atualizações ou quando são instaladas num cliente. Se o cliente tiver um fuso horário diferente, estas ações irão ocorrer quando a hora do cliente corresponder à hora de avaliação.  

    -   **Hora de disponibilização do software**: Selecione uma das seguintes definições para especificar quando as atualizações de software são disponibilizadas aos clientes:  

        -   **Logo que possível**: Selecione esta definição para disponibilizar as atualizações de software que estão incluídas na implementação aos computadores cliente logo que possível. Quando criar a implementação com esta definição selecionada, o Configuration Manager atualiza a política de cliente. Em seguida, durante o ciclo seguinte de consulta da política de cliente, os clientes ficarão informados da implementação e poderão obter as atualizações que estiverem disponíveis para instalação.  

        -   **Hora específica**: Selecione esta definição para disponibilizar as atualizações de software que estão incluídas na implementação aos computadores cliente numa hora e data específicas. Quando criar a implementação com esta definição ativada, o Configuration Manager atualiza a política de cliente. Em seguida, durante o ciclo de consulta seguinte da política de cliente, os clientes estarão informados da implementação. No entanto, as atualizações de software da implementação não ficarão disponíveis para instalação antes da data e hora configuradas.  

    -   **Prazo de instalação**: Selecione uma das seguintes definições para especificar o prazo de instalação para as atualizações de software da implementação:  

        -   **Logo que possível**: Selecione esta definição para instalar automaticamente as atualizações de software na implementação logo que possível.  

        -   **Hora específica**: Selecione esta definição para instalar automaticamente as atualizações de software na implementação numa hora e data específicas. O Configuration Manager determina o prazo de instalação de atualizações de software adicionando configurada **hora específica** intervalo para o **hora de disponibilização do Software**.  

        > [!NOTE]  
        >  A hora real do prazo de instalação corresponde à hora apresentada acrescida de um período de tempo aleatório de até 2 horas. Desta forma, reduzirá o impacto potencial da instalação das atualizações de software da implementação ao mesmo tempo em todos os computadores cliente da coleção de destino.  
        >   
        >  Pode configurar a definição de cliente **Agente do Computador** , **Desativar a aleatoriedade de prazos** para desativar o atraso de aleatoriedade da instalação para as atualizações de software necessárias. Para obter mais informações, veja [Agente do Computador](../../core/clients/deploy/about-client-settings.md#computer-agent).  

6.  Na página Experiência de Utilizador, configure as seguintes definições:  

    -   **As notificações de utilizador**: Especifique se pretende apresentar a notificação de atualizações de software no Centro de Software no computador cliente à configurada **hora de disponibilização do Software** e se pretende apresentar as notificações de utilizador nos computadores cliente.  

    -   **Comportamento do prazo**: Especifique o comportamento a adotar quando é atingido o prazo para a implementação de atualização de software. Especifique se pretende instalar as atualizações de software da implementação. Especifique também se pretende reiniciar o sistema após a instalação da atualização de software, independentemente de uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção, consulte [como utilizar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento de reinício do dispositivo**: Especifique se pretende suprimir um reinício do sistema em servidores e estações de trabalho após as atualizações de software estão instaladas e reiniciar o sistema é necessário para concluir a instalação.  

        > [!IMPORTANT]  
        >  A supressão dos reinícios de sistema pode ser útil em ambientes de servidor ou em casos em que não pretenda que os computadores que instalam as atualizações de software sejam reiniciados por predefinição. No entanto, este método pode deixar os computadores num estado não seguro, enquanto que um reinício forçado ajudará a assegurar a conclusão imediata da instalação da atualização de software.  

    -   **Para dispositivos Windows Embedded de processamento do filtro de escrita**: Quando implementa atualizações de software em dispositivos Windows Embedded que tenham o filtro de escrita ativado, pode especificar a instalar a atualização de software na sobreposição temporária e ou confirmar as alterações mais tarde ou por confirmar as alterações no prazo de instalação ou durante uma janela de manutenção. Ao consolidar alterações no momento da instalação ou durante uma janela de manutenção, será necessário um reinício para que as alterações sejam mantidas no dispositivo.  

        > [!NOTE]  
        >  Ao implementar uma atualização de software num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada.  

7.  Na página alertas, configure o Configuration Manager e o System Center Operations Manager gerarão alertas para esta implementação.  

    > [!WARNING]  
    >  Pode rever os alertas de atualizações de software recentes a partir do nó **Atualizações de Software** da área de trabalho **Biblioteca de Software** .  

8. Na página Definições de Transferência, configure as seguintes definições:  

    - Especifique se o cliente irá transferir e instalar as atualizações de software quando estiver ligado a uma rede lenta ou estiver a utilizar uma localização de conteúdos de contingência.  

    - Especifique se pretende que o cliente transfira e instale as atualizações de software a partir de um ponto de distribuição de contingência quando o conteúdo das atualizações de software não estiver disponível num ponto de distribuição preferencial.  

    - **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**: Especifique se pretende ativar a utilização do BranchCache para as transferências de conteúdos. Para obter mais informações sobre o BranchCache, veja [Conceitos para a gestão de conteúdos](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Se as atualizações de software não estão disponíveis no ponto de distribuição na atual, vizinho ou site grupos, transferir conteúdo do Microsoft Updates**: Selecione esta definição para que os clientes que estão ligados as intranet transferir as atualizações de software do Microsoft Update caso as atualizações de software não estejam disponíveis nos pontos de distribuição. Os clientes baseados na Internet podem sempre aceder ao Microsoft Update para o conteúdo de atualizações de software.

    - Especifique se pretende permitir que os clientes efetuem a transferência após um prazo de instalação se estiverem a utilizar ligações à Internet com tráfego limitado. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à Internet com tráfego limitado.  

    > [!NOTE]  
    > Os clientes solicitam a localização de conteúdo a partir de um ponto de gestão para as atualizações de software de uma implementação. O comportamento de transferência dependerá da forma como tiver configurado o ponto de distribuição, o pacote de implementação e as definições desta página. Para obter mais informações, veja [Cenários de localização da origem de conteúdo](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

Para obter mais informações sobre o processo de implementação, veja [Processo de implementação de atualizações de software](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Passos seguintes
[Monitorizar atualizações de software](monitor-software-updates.md)

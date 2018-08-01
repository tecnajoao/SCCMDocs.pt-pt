1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho e selecione o **atualizações de Software** nó.  

2.  Escolha a atualização de software a transferir utilizando um dos seguintes métodos:  

    -   Selecione um ou mais grupos de atualização de software dos **grupos de atualização de Software** nó. Em seguida, clique em **transferir** na faixa de opções.  

    -   Selecione um ou mais atualizações de software a partir **todas as atualizações de Software** nó. Em seguida, clique em **transferir** na faixa de opções.  

        > [!NOTE]  
        >  Na **todas as atualizações de Software** nó, o Configuration Manager apresenta apenas as atualizações de software com uma **crítico** e **segurança** classificação que tenham sido publicadas na últimos 30 dias.  

        > [!TIP]  
        >  Clique em **adicionar critérios** para filtrar as atualizações de software que são apresentadas na **todas as atualizações de Software** nó. Critérios de procura de Save que, muitas vezes, utilizar e, em seguida, gerir procuras guardadas no **pesquisa** separador.  


3.  Sobre o **pacote de implementação** página do Assistente de atualizações de Software transfira, configure as seguintes definições:  

    -  **Selecionar pacote de implementação**: Escolha esta definição para selecionar um pacote de implementação existente para as atualizações de software incluídas na implementação.  

        > [!NOTE]  
        >  Atualizações de software que o site já tenha transferido para o pacote de implementação selecionado não transferidas novamente.  

    -  **Criar um novo pacote de implementação**: Selecione esta definição para criar um novo pacote de implementação para as atualizações de software na implementação. Configure as seguintes definições:  

        -   **Nome**: Especifica o nome do pacote de implementação. O pacote deverá ter um nome exclusivo que descreva resumidamente o conteúdo do pacote. É limitado a 50 carateres.  

        -   **Descrição**: Especifique uma descrição que disponibilize informações sobre o pacote de implementação. A descrição opcional é limitada a 127 carateres.    

        -   **Origem do pacote**: Especifica a localização dos ficheiros de origem de atualização do software. Escreva um caminho de rede para a localização de origem, por exemplo, `\\server\sharename\path`, ou clique em **procurar** para procurar a localização de rede. Crie a pasta partilhada para os ficheiros de origem do pacote de implementação antes de prosseguir para a página seguinte.  

             - Não é possível utilizar a localização especificada como a fonte de outro pacote de implementação de software.  

             - Pode alterar a localização de origem do pacote nas propriedades do pacote de implementação depois do Configuration Manager cria o pacote de implementação. Se o fizer, primeiro copie o conteúdo da origem do pacote original para a nova localização de origem do pacote.  

             -  A conta de computador do fornecedor de SMS e o utilizador que está a executar o Assistente para transferir as atualizações de software terão de ter **escrever** permissões para a localização de transferência. Restringir o acesso à localização de transferência. Esta restrição reduz o risco dos atacantes adulterar os ficheiros de origem de atualização de software.  

        - **Ativar a replicação diferencial de binários**: Ative esta definição para minimizar o tráfego de rede entre sites. Replicação diferencial binária (BDR) apenas atualiza o conteúdo que foi alterado no pacote, em vez de atualizar o conteúdo do pacote inteiro. Para obter mais informações, consulte [replicação de diferencial binário](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#binary-differential-replication).  

4.  Sobre o **pontos de distribuição** página, especifique os pontos de distribuição ou grupos para alojar o software de ficheiros de atualização de ponto de distribuição. Para obter mais informações sobre os pontos de distribuição, veja [Configurações de pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_configs). Esta página apenas está disponível ao criar um novo pacote de implementação da atualização de software.  

5.  O **definições de distribuição** página está disponível apenas quando cria um novo pacote de implementação de atualização de software. Especifique as seguintes definições:  

    -   **Prioridade de distribuição**: Utilize esta definição para especificar a prioridade de distribuição para o pacote de implementação. A prioridade de distribuição aplica-se quando o pacote de implementação é enviado para pontos de distribuição em sites subordinados. Pacotes de implementação são enviados por ordem de prioridade: elevada, média ou baixa. Os pacotes com prioridades idênticas são enviados pela ordem em que foram criados. Se não houver nenhum registo de segurança, o pacote de processos imediatamente, independentemente de sua prioridade. Por predefinição, o site envia pacotes com **médio** prioridade.  

    -   **Ativar para distribuição a pedido**: Utilize esta definição para ativar a pedido conteúdos distribuição para pontos de distribuição configurados para esta funcionalidade e no grupo de limite atual do cliente. Quando ativa esta definição, o ponto de gestão cria um acionador para a distribuição manager distribua o conteúdo por todos esses pontos de distribuição quando um cliente solicita o conteúdo do pacote e o conteúdo não está disponível. Para obter mais informações, consulte [distribuição de conteúdo a pedido](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#on-demand-content-distribution).  

    -   **Pré-configurado as definições do ponto de distribuição**: Utilize esta definição para especificar como pretende distribuir conteúdo para pontos de distribuição pré-configurados. Escolha uma das seguintes opções:  

        -   **Transferir o conteúdo automaticamente quando os pacotes são atribuídos aos pontos de distribuição**: Utilize esta definição para ignorar as definições pré-configuradas e distribuir conteúdo para o ponto de distribuição.   

        -   **Transferir apenas alterações de conteúdo para o ponto de distribuição**: Utilize esta definição para pré-configurar o conteúdo inicial para o ponto de distribuição e, em seguida, distribuir as alterações de conteúdo ao ponto de distribuição.  

        -   **Copiar manualmente o conteúdo deste pacote para o ponto de distribuição**: Utilize esta definição para pré-configurar sempre o conteúdo no ponto de distribuição. Esta opção é a predefinição.  

        Para obter mais informações sobre a pré-configuração de conteúdo para pontos de distribuição, veja [Utilizar conteúdo pré-configurado](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  


6.  Sobre o **localização de transferência** , especifique a localização que o Configuration Manager utiliza para baixar o software atualizar ficheiros de origem. Utilize uma das seguintes opções:  

    -   **Transferir atualizações de software a partir da Internet**: Selecione esta definição para transferir as atualizações de software a partir da localização na internet. Esta opção é a predefinição.  

    -   **Transferir atualizações de software a partir de uma localização na minha rede**: Selecione esta definição para transferir as atualizações de software a partir de um diretório local ou uma pasta compartilhada. Esta definição é útil quando o computador que executa o assistente não tem acesso à internet. Qualquer computador com acesso à internet provisoriamente pode transferir as atualizações de software. Em seguida, armazená-las numa localização na rede local que seja acessível ao computador que executa o assistente.  


7.  Sobre o **seleção de idioma** , selecione os idiomas para o qual o site transfere as atualizações de software selecionadas. O site transfere apenas essas atualizações se elas estão disponíveis nos idiomas selecionados. Atualizações de software que não são específicas do idioma serão sempre transferidas. Por predefinição, o assistente seleciona os idiomas que configurou nas propriedades do ponto de atualização de software. Terá de estar selecionado pelo menos um idioma para que possa prosseguir para a página seguinte. Se selecionar apenas idiomas que não suporta uma atualização de software, o download falha para a atualização.  

8. Sobre o **resumo** página, verifique as definições que selecionou no assistente e, em seguida, clique em **seguinte** para baixar o software de atualizações.  

9. Sobre o **conclusão** página, certifique-se de que as atualizações de software foram transferidas com êxito e, em seguida, clique em **fechar**.  

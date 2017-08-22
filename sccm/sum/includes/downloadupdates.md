1.  Na consola do Configuration Manager, navegue até à **biblioteca de Software** > **atualizações de Software**.  

2.  Escolha a atualização de software a transferir utilizando um dos seguintes métodos:  

    -   Selecione um ou mais grupos de atualização de software a partir de **Grupos de Atualização de Software**e, em seguida, no separador **Home Page** , no grupo **Grupo de Atualização** , clique em **Transferir**.  

    -   Selecione uma ou mais atualizações de software a partir de **Todas as Atualizações de Software**e, em seguida, no separador **Home Page** , no grupo **Atualização** , clique em **Transferir**.  

        > [!NOTE]  
        >  No **todas as atualizações de Software** nó, o Configuration Manager apresenta apenas as atualizações de software com uma **crítico** e **segurança** classificação que tenham sido publicadas nos últimos 30 dias.  

        > [!TIP]  
        >  Clique em **Adicionar Critérios** para filtrar as atualizações de software que são apresentadas no nó **Todas as Atualizações de Software** , guarde os critérios de pesquisa que utiliza com maior frequência e faça a gestão das procuras guardadas no separador **Procurar** .  

         É aberto o **Assistente Transferir Atualizações de Software** .  

3.  Na página **Pacote de Implementação** , configure as definições seguintes:  

    1.  **Selecionar pacote de implementação**: Escolha esta definição para selecionar um pacote de implementação existente para as atualizações de software incluídas na implementação.  

        > [!NOTE]  
        >  As atualizações de software que já tenham sido transferidas para o pacote de implementação selecionado não serão transferidas novamente.  

    2.  **Criar um novo pacote de implementação**: Selecione esta definição para criar um novo pacote de implementação para as atualizações de software incluídas na implementação. Configure as seguintes definições:  

        -   **Nome**: Especifica o nome do pacote de implementação. O pacote deverá ter um nome exclusivo que descreva resumidamente o conteúdo do pacote.  Está limitado a 50 carateres.  

        -   **Descrição**: Especifica a descrição do pacote de implementação. A descrição do pacote fornece informações sobre o conteúdo do pacote e está limitada a 127 carateres.  

        -   **Origem do pacote**: Especifica a localização dos ficheiros de origem de atualização de software. Escreva um caminho de rede para a localização de origem, como, por exemplo, **\\\server\sharename\path**ou clique em **Procurar** para procurar a localização de rede. Antes de continuar para a página seguinte, terá de criar a pasta partilhada para os ficheiros de origem do pacote de implementação.  

            > [!NOTE]  
            >  A localização de origem do pacote de implementação que especificar não poderá ser utilizada por outro pacote de implementação de software.  

            > [!IMPORTANT]  
            >  Tanto a conta de computador do Fornecedor de SMS, como o utilizador que executar o assistente para transferir as atualizações de software, têm de ter permissões NTFS de **Escrita** na localização de transferência. Deverá restringir cuidadosamente o acesso à localização de transferência para reduzir o risco de adulteração dos ficheiros de origem de atualização de software por parte de atacantes.  

            > [!IMPORTANT]  
            >  Pode alterar a localização de origem do pacote nas propriedades do pacote de implementação, após o Configuration Manager cria o pacote de implementação. Mas se o fizer, terá primeiro de copiar o conteúdo da origem inicial do pacote para a nova localização de origem do pacote.  

     Clique em **Seguinte**.  

4.  No **pontos de distribuição** página, especifique os pontos de distribuição ou grupos de pontos de distribuição que irão alojar os ficheiros de atualização de software e, em seguida, clique em **seguinte**. Para obter mais informações sobre os pontos de distribuição, veja [Configurações de pontos de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!NOTE]  
    >  A página Pontos de Distribuição apenas estará disponível quando criar um novo pacote de implementação de atualização de software.  

6.  No **definições de distribuição** página, especifique as seguintes definições:  

    -   **Prioridade de distribuição**: Utilize esta definição para especificar a prioridade de distribuição para o pacote de implementação. A prioridade de distribuição aplica-se quando o pacote de implementação é enviado para pontos de distribuição em sites subordinados. Pacotes de implementação são enviados por ordem de prioridade: **Elevada**, **média**, ou **baixa**. Os pacotes com prioridades idênticas são enviados pela ordem em que foram criados. Se não existirem tarefas pendentes, o pacote será processado de imediato, independentemente da sua prioridade. Por predefinição, os pacotes são enviados com a prioridade **Média** .  

    -   **Distribuir o conteúdo do pacote para pontos de distribuição preferenciais**: Utilize esta definição para ativar a distribuição de conteúdo a pedido para pontos de distribuição preferenciais. Quando esta definição é ativada, o ponto de gestão cria um acionador para que o gestor de distribuição distribua o conteúdo por todos os pontos de distribuição preferidos quando um cliente solicita o conteúdo para o pacote e o conteúdo não está disponível em quaisquer pontos de distribuição preferidos. Para obter mais informações sobre os pontos de distribuição preferenciais e conteúdo a pedido, veja [Cenários de localização da origem de conteúdo](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

    -   **Definições de ponto de distribuição pré-configurados**: Utilize esta definição para especificar como pretende distribuir conteúdo para pontos de distribuição pré-configurados. Escolha uma das seguintes opções:  

        -   **Transferir o conteúdo automaticamente quando os pacotes são atribuídos aos pontos de distribuição**: Utilize esta definição para ignorar as definições pré-configuradas e distribuir conteúdo ao ponto de distribuição.  

        -   **Transferir apenas alterações de conteúdo para o ponto de distribuição**: Utilize esta definição para pré-configurar o conteúdo inicial para o ponto de distribuição e, em seguida, distribuir as alterações de conteúdo ao ponto de distribuição.  

        -   **Copiar manualmente o conteúdo deste pacote para o ponto de distribuição**: Utilize esta definição para pré-configurar sempre o conteúdo no ponto de distribuição. Esta é a predefinição.  

         Para obter mais informações sobre a pré-configuração de conteúdo para pontos de distribuição, veja [Utilizar conteúdo pré-configurado](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

     Clique em **Seguinte**.  

6.  No **localização de transferência** página, especifique a localização do Configuration Manager irá utilizar para transferir os ficheiros de origem de atualização de software. Se necessário, utilize as seguintes opções:  

    -   **Transferir atualizações de software a partir da Internet**: Selecione esta definição para transferir as atualizações de software a partir da localização na Internet. Esta é a predefinição.  

    -   **Transferir atualizações de software a partir de uma localização na rede local**: Selecione esta definição para transferir atualizações de software a partir de uma pasta local ou a pasta de rede partilhada. Utilize esta definição se o computador que estiver a executar o assistente não tiver acesso à Internet.  

        > [!NOTE]  
        >  Se utilizar esta definição, transfira as atualizações de software a partir de qualquer computador que tenha acesso à Internet e copie as atualizações de software para uma localização na rede local que esteja acessível ao computador que estiver a executar o assistente.  

     Clique em **Seguinte**.  

7.  No **seleção de idioma** página, especifique os idiomas para os quais as atualizações de software selecionadas serão transferidas e, em seguida, clique em **seguinte**. O Configuration Manager transfere as atualizações de software apenas se estiverem disponíveis nos idiomas selecionados. As atualizações de software que não sejam específicas do idioma serão sempre transferidas.  

8. No **resumo** página, verifique as definições que selecionou no assistente e, em seguida, clique em **seguinte** para transferir o software de atualizações.  

9. No **conclusão** página, certifique-se de que as atualizações de software foram transferidas com êxito e, em seguida, clique em **fechar**.  

---
title: "Implementar conteúdo | Documentos do Microsoft"
description: "Depois de instalar pontos de distribuição para o System Center Configuration Manager, eis como pode começar a implementar o conteúdo aos mesmos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d50dcca0-4419-449d-a487-73abcadf328f
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: 36b08285ef78d0acb9ba9c44abe2d57e311d44b3
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="deploy-and-manage-content-for-system-center-configuration-manager"></a>Implementar e gerir conteúdo para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois de instalar pontos de distribuição para o System Center Configuration Manager, pode começar a implementar o conteúdo aos mesmos. Normalmente, as transferências de conteúdo para pontos de distribuição através da rede, mas outras opções para obter conteúdo aos pontos de distribuição existe. Depois de transfere conteúdo para um ponto de distribuição, pode atualizar, redistribuir, remover e validar que o conteúdo em pontos de distribuição.  

##  <a name="bkmk_distribute"></a>Distribuir conteúdo  
 Normalmente, pode distribuir conteúdo para pontos de distribuição para que esteja disponível para computadores cliente. (A exceção é quando utiliza a distribuição de conteúdo a pedido para uma implementação específica.)  Quando distribui conteúdo, o Configuration Manager armazena ficheiros de conteúdo de um pacote e, em seguida, distribui o pacote ao ponto de distribuição. Os tipos de conteúdo que podem ser distribuídos, incluem:  

-   Tipos de implementação de aplicação  

-   Pacotes  

-   Pacotes de implementação  

-   Pacotes de controladores  

-   Imagens de sistema operativo  

-   Instaladores do sistema operativo  

-   Imagens de arranque  

-   Sequências de tarefas  

Quando cria um pacote que contém ficheiros de origem, tal como uma aplicação tipo ou na implementação de pacote de implementação, o site no qual o pacote é criado torna-se o proprietário do site para a origem de conteúdo do pacote. Gestor de configuração copia os ficheiros de origem do caminho de ficheiro de origem que especificou para o objeto à biblioteca de conteúdos no servidor do site que é proprietário da origem de conteúdo do pacote.  Em seguida, o Configuration Manager replica as informações para sites adicionais. (Consulte [a biblioteca de conteúdos](../../../../core/plan-design/hierarchy/the-content-library.md) para obter mais informações sobre este assunto.)  

Utilize o seguinte procedimento para distribuir conteúdo para pontos de distribuição.  

#### <a name="to-distribute-content-on-distribution-points"></a>Para distribuir conteúdo em pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No **biblioteca de Software** área de trabalho, selecione um dos seguintes passos para o tipo de conteúdo que pretende distribuir:  

    -   **Aplicações**: Expanda **gestão de aplicações** > **aplicações**e, em seguida, selecione as aplicações que pretende distribuir.  

    -   **Pacotes**: Expanda **gestão de aplicações** >  **pacotes**e, em seguida, selecione os pacotes que pretende distribuir.  

    -   **Pacotes de implementação**: Expanda **atualizações de Software** >  **pacotes de implementação**e, em seguida, selecione os pacotes de implementação que pretende distribuir.  

    -   **Pacotes de controladores**: Expanda **sistemas operativos** >  **pacotes de controladores**e, em seguida, selecione os pacotes de controladores que pretende distribuir.  

    -   **Imagens do sistema operativo**: Expanda **sistemas operativos** >  **imagens do sistema operativo**e, em seguida, selecione as imagens de sistema operativo que pretende distribuir.  

    -   **Instaladores do sistema operativo**: Expanda **sistemas operativos** > **instaladores do sistema operativo**e, em seguida, selecione os instaladores do sistema operativo que pretende distribuir.  

    -   **Imagens de arranque**: Expanda **sistemas operativos** >  **imagens de arranque**e, em seguida, selecione as imagens de arranque que pretende distribuir.  

    -   **As sequências de tarefas**: Expanda **sistemas operativos** >  **sequências de tarefas**e, em seguida, selecione a sequência de tarefas que pretende distribuir. Embora as sequências de tarefas não tenham conteúdos, têm associadas, as dependências de conteúdos que são distribuídas.  

        > [!NOTE]  
        >  Se modificar a sequência de tarefas, necessitará de redistribuir o conteúdo.  

3.  No separador **Início** , no grupo **Implementação** , clique em **Distribuir Conteúdo** É aberto o Assistente para distribuir conteúdos.  

4.  No **geral** página, verifique se que os conteúdos apresentados correspondem aos conteúdos que pretende distribuir, escolha se pretende que o Configuration Manager para detetar as dependências de conteúdos que estão associadas a conteúdos selecionados e adicione as dependências à distribuição e, em seguida, clique em **seguinte**.  

    > [!NOTE]  
    >  Tem a opção para configurar o **detetar dependências de conteúdo associado e adicioná-las a esta distribuição** definição apenas para o tipo de conteúdo de aplicação. Configuration Manager configura automaticamente esta definição para sequências de tarefas e não pode ser modificado.  

5.  No **conteúdo** separador, caso seja apresentado, verifique se que os conteúdos apresentados correspondem aos conteúdos que pretende distribuir e, em seguida, clique em **seguinte**.  

    > [!NOTE]  
    >  O **conteúdo** página é apresentada apenas quando o **detetar dependências de conteúdo associado e adicioná-las a esta distribuição** definição está selecionada no **geral** página do assistente.  

6.  No **destino do conteúdo** página, clique em **adicionar**, escolha uma das seguintes opções e, em seguida, siga o passo associado:  

    -   **Coleções**: Selecione **coleções de utilizadores** ou **coleções de dispositivos**, clique na coleção associada um ou mais grupos de pontos de distribuição e, em seguida, clique em **OK**.  

        > [!NOTE]  
        >  São apresentadas apenas as coleções que estão associadas um grupo de pontos de distribuição. Para obter mais informações sobre como associar coleções a grupos de pontos de distribuição, consulte o artigo [gerir grupos de pontos de distribuição](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) no [instalar e configurar pontos de distribuição para o System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) tópico.  

    -   **Ponto de distribuição**: Selecione um ponto de distribuição existente e, em seguida, clique em **OK**. Pontos de distribuição que tenham anteriormente recebido o conteúdo não são apresentados.  

    -   **Grupo de pontos de distribuição**: Selecione um grupo de ponto de distribuição existente e, em seguida, clique em **OK**. Grupos de pontos de distribuição que tenham anteriormente recebido o conteúdo não são apresentados.  

    Quando acabar de adicionar destinos de conteúdo, clique em **seguinte**.  

7.  No **resumo** página, reveja as definições de distribuição antes de continuar. Para distribuir o conteúdo aos destinos selecionados, clique em **seguinte**.  

8.  O **progresso** página apresenta o progresso da distribuição.  

9. O **confirmação** página é apresentada se o conteúdo foi atribuído com êxito aos pontos. Para monitorizar a distribuição de conteúdos, consulte o artigo [monitorizar o conteúdo ter distribuídas com o System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

##  <a name="bkmk_prestage"></a>Utilize conteúdo pré-configurado  
 Pode pré-configurar ficheiros de conteúdo para aplicações e tipos de pacote:  

-   Na consola do Configuration Manager, pode selecionar o conteúdo necessário e, em seguida, utilizar o **criar Assistente de ficheiro de conteúdo pré-configurado** para criar um ficheiro de conteúdo comprimido e pré-configurado que contém os ficheiros e metadados associados para o conteúdo que selecionou.  

-   Em seguida, pode importar manualmente os conteúdos para um servidor do site, site secundário ou ponto de distribuição.  

-   Quando importar o ficheiro de conteúdo pré-configurado num servidor do site, os ficheiros de conteúdos são adicionados à biblioteca de conteúdos no servidor do site e em seguida, registados na base de dados do servidor do site.  

-   Quando importar o ficheiro de conteúdo pré-configurado num ponto de distribuição, os ficheiros de conteúdos são adicionados à biblioteca de conteúdos no ponto de distribuição e uma mensagem de estado é enviada para o servidor de site que informa o site que o conteúdo está disponível no ponto de distribuição.  

**Limitações e considerações para conteúdo pré-configurado:**  

-   **Quando o ponto de distribuição estiver localizado no servidor do site**, não ative o ponto de distribuição para conteúdo pré-configurado. Em alternativa, utilize o procedimento descrito no [como pré-configurar conteúdo num ponto de distribuição num servidor do site](#bkmk_dpsiteserver).  

-   **Quando o ponto de distribuição é configurado como um ponto de distribuição de solicitação**, não ative o ponto de distribuição para conteúdo pré-configurado. A configuração de conteúdo pré-configurado para um ponto de distribuição substitui a configuração de ponto de distribuição de solicitação. Um ponto de distribuição de solicitação que esteja configurado para conteúdos pré-configurados não solicitará conteúdos a partir do ponto de distribuição de origem e não receberá conteúdos a partir do servidor do site.  

-   **A biblioteca de conteúdos tem de ser criada no ponto de distribuição para que possa pré-configurar conteúdos para o ponto de distribuição**. Distribua os conteúdos através da rede, pelo menos, uma vez antes de pré-configurar os conteúdos para o ponto de distribuição.  

-   **Quando pré-configura conteúdos para um pacote com um caminho de origem do pacote extenso** (por exemplo, mais de 140 caracteres), a ferramenta da linha de comandos extrair conteúdos poderá falhar com êxito a extração dos conteúdos desse pacote para a biblioteca de conteúdos.  

Para obter informações sobre quando pré-configurar ficheiros de conteúdo, consulte o artigo *pré-configurado conteúdo* no [gerir a largura de banda de rede para a gestão de conteúdo](/sccm/core/plan-design/hierarchy/manage-network-bandwidth) tópico.  

Utilize as secções seguintes para pré-configurar os conteúdos.  

###  <a name="BKMK_CreatePrestagedContentFile"></a>Passo 1: Criar um ficheiro de conteúdo pré-configurado  
 Pode criar um ficheiro de conteúdo comprimido e pré-configurado que contém os ficheiros e metadados associados para o conteúdo que selecionou na consola do Configuration Manager. Utilize o procedimento seguinte para criar um ficheiro de conteúdo pré-configurado.  

##### <a name="to-create-a-prestaged-content-file"></a>Para criar um ficheiro de conteúdo pré-configurado  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No **biblioteca de Software** área de trabalho, selecione um dos seguintes passos para o tipo de conteúdo que pretende pré-configurar:  

    -   **Aplicações**: Expanda **gestão de aplicações**, clique em **aplicações**e, em seguida, selecione as aplicações que pretende pré-configurar.  

    -   **Pacotes**: Expanda **gestão de aplicações**, clique em **pacotes**e, em seguida, selecione os pacotes que pretende pré-configurar.  

    -   **Pacotes de controladores**: Expanda **sistemas operativos**, clique em **pacotes de controladores**e, em seguida, selecione os pacotes de controladores que pretende pré-configurar.  

    -   **Imagens do sistema operativo**: Expanda **sistemas operativos**, clique em **imagens do sistema operativo**e, em seguida, selecione as imagens de sistema operativo que pretende pré-configurar.  

    -   **Instaladores do sistema operativo**: Expanda **sistemas operativos**, clique em **instaladores do sistema operativo**e, em seguida, selecione os instaladores do sistema operativo que pretende pré-configurar.  

    -   **Imagens de arranque**: Expanda **sistemas operativos**, clique em **imagens de arranque**e, em seguida, selecione as imagens de arranque que pretende pré-configurar.  

    -   **As sequências de tarefas**: Expanda **sistemas operativos**, clique em **sequências de tarefas**e, em seguida, selecione a sequência de tarefas que pretende pré-configurar.  

3.  No **base** separador o **implementação** grupo, clique em **criar ficheiro de conteúdo de pré-configurar**. Abre-se a criar ficheiro Assistente para conteúdo pré-configurado.  

    > [!NOTE]  
    >  **Para aplicações:** No **base** separador o **aplicação** grupo, clique em **criar pré-configurado ficheiro de conteúdo**.  
    >   
    >  **Para pacotes:** No **base** separador o &lt; *PackageName*> grupo, clique em **criar pré-configurado ficheiro de conteúdo**.  

4.  No **geral** página, clique em **procurar**, escolha a localização de ficheiro de conteúdo pré-configurado, especifique um nome para o ficheiro e, em seguida, clique em **guardar**. Utilize este ficheiro de conteúdo pré-configurado em servidores de sites primários, servidores de sites secundários ou pontos de distribuição para importar o conteúdo e metadados.  

5.  Para aplicações, selecione **exportar todas as dependências** para que o Configuration Manager detete e adicione as dependências associadas à aplicação para o ficheiro de conteúdo pré-configurado. Por predefinição, esta definição está selecionada.  

6.  No **comentários do administrador**, introduza comentários opcionais sobre o ficheiro de conteúdo pré-configurado e, em seguida, clique em **seguinte**.  

7.  No **conteúdo** página, verifique se os conteúdos apresentados correspondem aos conteúdos que pretende adicionar ao ficheiro de conteúdo pré-configurado e, em seguida, clique em **seguinte**.  

8.  No **localizações de conteúdo** página, especifique os pontos de distribuição a partir do qual obter os ficheiros de conteúdo para o ficheiro de conteúdo pré-configurado. Pode selecionar mais do que um ponto de distribuição para obter o conteúdo. Os pontos de distribuição são listados na secção de localizações de conteúdo. O **conteúdo** coluna apresenta quantos selecionado dos pacotes ou aplicações estão disponíveis em cada ponto de distribuição. Configuration Manager começa com o primeiro ponto de distribuição na lista para obter o conteúdo selecionado e, em seguida, avança para baixo na lista para obter os restantes conteúdos necessários para o ficheiro de conteúdo pré-configurado. Clique em **mover para cima** ou **mover para baixo** para alterar a ordem de prioridade dos pontos de distribuição. Se os pontos de distribuição na lista não contiverem todo o conteúdo selecionado, necessitará de adicionar pontos de distribuição para a lista que contenham o conteúdo ou sair do assistente, distribuir o conteúdo para, pelo menos, um ponto de distribuição e, em seguida, reinicie o assistente.  

9. No **resumo** página, confirme os detalhes. Pode regressar às páginas anteriores para e faça alterações. Clique em **seguinte** para criar o ficheiro de conteúdo pré-configurado.  

10. O **progresso** página apresenta o conteúdo que está a ser adicionado ao ficheiro de conteúdo pré-configurado.  

11. No **conclusão** página, certifique-se de que o ficheiro de conteúdo pré-configurado foi criado com êxito e, em seguida, clique em **fechar**.  

###  <a name="BKMK_AssignContentToDistributionPoint"></a>Passo 2: Atribuir o conteúdo a pontos de distribuição  
 Depois de pré-configurar o ficheiro de conteúdo, atribua o conteúdo para pontos de distribuição.  

> [!NOTE]  
>  Quando utilizar um ficheiro de conteúdo pré-configurado para recuperar a biblioteca de conteúdos num servidor do site e necessitar de pré-configurar os ficheiros de conteúdo num ponto de distribuição, pode ignorar este procedimento.  

 Utilize o seguinte procedimento para atribuir o conteúdo do ficheiro de conteúdo pré-configurado para pontos de distribuição.  

> [!IMPORTANT]  
>  Certifique-se de que os pontos de distribuição que pretende pré-configurar estão configurado como pontos de distribuição pré-configurados ou que o conteúdo é distribuído aos pontos de distribuição através da rede.  

##### <a name="to-assign-the-content-to-distribution-points"></a>Para atribuir o conteúdo para pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No **biblioteca de Software** área de trabalho, selecione um dos seguintes passos para o tipo de conteúdo que selecionou quando criou o ficheiro de conteúdo pré-configurado:  

    -   **Aplicações**: Expanda **gestão de aplicações**, clique em **aplicações**e, em seguida, selecione as aplicações que pré-configurou.  

    -   **Pacotes**: Expanda **gestão de aplicações**, clique em **pacotes**e, em seguida, selecione os pacotes que pré-configurou.  

    -   **Pacotes de implementação**: Expanda **atualizações de Software**, clique em **pacotes de implementação**e, em seguida, selecione os pacotes de implementação que pré-configurou.  

    -   **Pacotes de controladores**: Expanda **sistemas operativos**, clique em **pacotes de controladores**e, em seguida, selecione os pacotes de controladores que pré-configurou.  

    -   **Imagens do sistema operativo**: Expanda **sistemas operativos**, clique em **imagens do sistema operativo**e, em seguida, selecione as imagens de sistemas operativos que pré-configurou.  

    -   **Instaladores do sistema operativo**: Expanda **sistemas operativos**, clique em **instaladores do sistema operativo**e, em seguida, selecione os instaladores do sistema operativo que pré-configurou.  

    -   **Imagens de arranque**: Expanda **sistemas operativos**, clique em **imagens de arranque**e, em seguida, selecione as imagens de arranque que pré-configurou.  

3.  No separador **Início** , no grupo **Implementação** , clique em **Distribuir Conteúdo** É aberto o Assistente para distribuir conteúdos.  

4.  No **geral** página, verifique se que os conteúdos apresentados correspondem aos conteúdos que pré-configurou, escolha se pretende que o Configuration Manager para detetar as dependências de conteúdos que estão associadas a conteúdos selecionados e adicione as dependências à distribuição e, em seguida, clique em **seguinte**.  

    > [!NOTE]  
    >  Tem a opção para configurar o **detetar dependências de conteúdo associado e adicioná-las a esta distribuição** definição apenas para o tipo de conteúdo de aplicação. Configuration Manager configura automaticamente esta definição para sequências de tarefas e não pode ser modificado.  

5.  No **conteúdo** página, caso seja apresentado, verifique se que os conteúdos apresentados correspondem aos conteúdos que pretende distribuir e, em seguida, clique em **seguinte**.  

    > [!NOTE]  
    >  O **conteúdo** página é apresentada apenas quando o **detetar dependências de conteúdo associado e adicioná-las a esta distribuição** definição está selecionada no **geral** página do assistente.  

6.  No **destino do conteúdo** página, clique em **adicionar**, escolha um dos seguintes itens que incluem os pontos de distribuição a pré-configurar e, em seguida, siga o passo associado:  

    -   **Coleções**: Selecione **coleções de utilizadores** ou **coleções de dispositivos**, clique na coleção associada um ou mais grupos de pontos de distribuição e, em seguida, clique em **OK**.  

        > [!NOTE]  
        >  São apresentadas apenas as coleções que estão associadas um grupo de pontos de distribuição.  Para obter mais informações, consulte o artigo [gerir grupos de pontos de distribuição](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) no [instalar e configurar pontos de distribuição para o System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) tópico.  

    -   **Ponto de distribuição**: Selecione um ponto de distribuição existente e, em seguida, clique em **OK**. Pontos de distribuição que tenham anteriormente recebido o conteúdo não são apresentados.  

    -   **Grupo de pontos de distribuição**: Selecione um grupo de ponto de distribuição existente e, em seguida, clique em **OK**. Grupos de pontos de distribuição que tenham anteriormente recebido o conteúdo não são apresentados.  

    Quando acabar de adicionar destinos de conteúdo, clique em **seguinte**.  

7.  No **resumo** página, reveja as definições de distribuição antes de continuar. Para distribuir o conteúdo aos destinos selecionados, clique em **seguinte**.  

8.  O **progresso** página apresenta o progresso da distribuição.  

9. O **confirmação** página é apresentada se ou não o conteúdo foi atribuído com êxito aos pontos de distribuição. Para monitorizar a distribuição de conteúdos, consulte o artigo [monitorizar o conteúdo ter distribuídas com o System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

###  <a name="BKMK_ExportContentFromPrestagedContentFile"></a>Passo 3: Extrair o conteúdo do ficheiro de conteúdo pré-configurado  
 Depois de criar o ficheiro de conteúdo pré-configurado e atribuir o conteúdo a pontos de distribuição, poderá extrair os ficheiros de conteúdo à biblioteca de conteúdos no ponto de servidor ou para a distribuição de sites. Normalmente, pode ter copiado o ficheiro de conteúdo pré-configurado para uma unidade portátil como uma unidade USB, ou ter burned conteúdo suportes de dados como um DVD e tenha disponível na localização do site servidor ou ponto de distribuição que necessite do conteúdo.  

 Utilize o procedimento seguinte para exportar manualmente os ficheiros de conteúdo a partir do ficheiro de conteúdo pré-configurado utilizando a ferramenta da linha de comandos extrair conteúdo.  

> [!IMPORTANT]  
>  Quando executa a ferramenta da linha de comandos extrair conteúdo, a ferramenta cria um ficheiro temporário à medida que cria o ficheiro de conteúdo pré-configurado. Em seguida, o ficheiro é copiado para a pasta de destino e o ficheiro temporário é eliminado. Tem de ter espaço suficiente em disco para este ficheiro temporário ou o processo de falha. O ficheiro temporário é criado na seguinte localização:  
>   
>  -   O ficheiro temporário é criado na mesma pasta que especificar como a pasta de destino para o ficheiro de conteúdo pré-configurado.  

> [!IMPORTANT]  
>  O utilizador que executa a ferramenta da linha de comandos extrair conteúdo tem de ter **administrador** direitos no computador a partir do qual está a extrair os conteúdos pré-configurados.  

##### <a name="to-extract-the-content-files-from-the-prestaged-content-file"></a>Para extrair os ficheiros de conteúdo do ficheiro de conteúdo pré-configurado  

1.  Copie o ficheiro de conteúdo pré-configurado para o computador a partir do qual pretende extrair o conteúdo.  

2.  Copie a ferramenta da linha de comandos extrair conteúdo de &lt; *ConfigMgrInstallationPath*> \bin\\&lt;*plataforma*> para o computador a partir do qual pretende extrair o ficheiro de conteúdo pré-configurado.  

3.  Abra a linha de comandos e navegue para a localização da pasta do ficheiro de conteúdo pré-configurado e da ferramenta extrair conteúdo.  

    > [!NOTE]  
    >  Pode extrair um ou mais ficheiros de conteúdo num servidor do site, servidor de site secundário ou ponto de distribuição pré-configurados.  

4.  Tipo de **extractcontent /p:**&lt;*Localficheiropreconfigurado*>**\\**&lt;*PrestagedFileName*> **/S** para importar um ficheiro individual.  

     Tipo de **extractcontent /p:**&lt;*Localficheiropreconfigurado*> **/S** importar todos os ficheiros pré-configurados numa pasta especificada.  

     Por exemplo, digite **extractcontent /P:D:\PrestagedFiles\MyPrestagedFile.pkgx /S** onde `D:\PrestagedFiles\` corresponde a Localficheiropreconfigurado, `MyPrestagedFile.pkgx` corresponde ao nome do ficheiro pré-configurado e `/S` informa o Configuration Manager para apenas extrair os conteúdos ficheiros que são mais recentes do que está atualmente no ponto de distribuição.  

     Se extrair o ficheiro de conteúdo pré-configurado num servidor do site, os ficheiros de conteúdos são adicionados à biblioteca de conteúdos no servidor do site e a disponibilidade dos conteúdos será registada na base de dados do servidor do site. Ao exportar o ficheiro de conteúdo pré-configurado num ponto de distribuição, os ficheiros de conteúdos são adicionados à biblioteca de conteúdos no ponto de distribuição, o ponto de distribuição envia uma mensagem de estado para o servidor de site primário principal e, em seguida, a disponibilidade dos conteúdos será registada na base de dados do site.  

    > [!IMPORTANT]  
    >  No cenário seguinte, tem de atualizar o conteúdo que extraiu de um ficheiro de conteúdo pré-configurado quando o conteúdo for atualizado para uma nova versão:  
    >   
    >  1.  Criar um ficheiro de conteúdo pré-configurado para a versão 1 de um pacote.  
    >  2.  Atualizar os ficheiros de origem do pacote com a versão 2.  
    >  3.  Extrair o ficheiro de conteúdo pré-configurado (versão 1 do pacote) num ponto de distribuição.  
    >   
    > O Configuration Manager não distribui automaticamente versão 2 do pacote ao ponto de distribuição. Tem de criar um novo ficheiro de conteúdo pré-configurado que contém a nova versão do ficheiro e, em seguida, extrair os conteúdos, atualizar o ponto de distribuição para distribuir os ficheiros que tenham sido alterados ou redistribuir os ficheiros do pacote.  

###  <a name="bkmk_dpsiteserver"></a>Como pré-configurar conteúdo num ponto de distribuição num servidor do site  
 Quando um ponto de distribuição é instalado num servidor do site, tem de utilizar o procedimento seguinte para pré-configurar com sucesso o conteúdo. Isto acontece porque os ficheiros de conteúdo já estão na biblioteca de conteúdos.  

 Quando o ponto de distribuição não está preparado para pré-configurar o conteúdo ou quando o ponto de distribuição não estiver localizado num servidor de sites, consulte o [conteúdo pré-configurado utilize](#bkmk_prestage) deste tópico.  

##### <a name="to-prestage-content-on-distribution-points-located-on-a-site-server"></a>Para pré-configurar conteúdo em pontos de distribuição localizados num servidor do site  

1.  Utilize os seguintes passos para verificar se o ponto de distribuição não está ativado para conteúdo pré-configurado.  

    1.  Na consola do Configuration Manager, clique em **Administração**.  

    2.  No **administração** área de trabalho, clique em **pontos de distribuição**e, em seguida, selecione o ponto de distribuição que esteja localizado no servidor do site.  

    3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

    4.  No **geral** separador, certifique-se de que o **ativar conteúdo pré-configurado para este ponto de distribuição** caixa de verificação não estiver selecionada.  

2.  Criar ficheiro de conteúdo pré-configurado utilizando a [passo 1: Criar um ficheiro de conteúdo pré-configurado](#BKMK_CreatePrestagedContentFile) deste tópico.  

3.  Atribua o conteúdo ao ponto de distribuição utilizando o [passo 2: Atribuir o conteúdo a pontos de distribuição](#BKMK_AssignContentToDistributionPoint) deste tópico.  

4.  No servidor do site, extrair o conteúdo do ficheiro de conteúdo pré-configurado utilizando a [passo 3: Extrair o conteúdo do ficheiro de conteúdo pré-configurado](#BKMK_ExportContentFromPrestagedContentFile) deste tópico.  

    > [!NOTE]  
    >  Quando o ponto de distribuição estiver num site secundário, aguarde pelo menos 10 minutos e, em seguida, ao utilizar uma consola do Configuration Manager que está ligada ao site primário principal, atribua o conteúdo ao ponto de distribuição no site secundário.  

##  <a name="bkmk_manage"></a>Gerir o conteúdo que tenha distribuídos  
 Tem as seguintes opções de gestão de conteúdo:  
 - [Atualizar conteúdo](#update-content)
 - [Redistribuir conteúdos](#redistribute-content)
 - [Remover o conteúdo](#remove-content)
 - [Validar conteúdo](#validate-content)

### <a name="update-content"></a>Atualizar conteúdo
Quando a localização do ficheiro de origem para uma implementação é atualizada ao adicionar novos ficheiros ou substituir ficheiros existentes com uma versão mais recente, pode atualizar os ficheiros de conteúdo em pontos de distribuição utilizando o **atualizar pontos de distribuição** ou **atualizar conteúdos** ação:  
-   Os ficheiros de conteúdos são copiados do caminho de ficheiro de origem para a biblioteca de conteúdos no site que é proprietário da origem de conteúdo do pacote  
-   A versão do pacote é incrementada  
-   As atualizações de pontos de cada instância da biblioteca de conteúdos em servidores do site e distribuição com apenas os ficheiros que foram alterados  

> [!WARNING]  
>  A versão do pacote de aplicações será sempre 1. Quando atualizar o conteúdo de um tipo de implementação de aplicação, o Configuration Manager cria um novo ID de conteúdo para o tipo de implementação e o pacote referenciará o novo ID de conteúdo.  

#### <a name="to-update-content-on-distribution-points"></a>Para atualizar conteúdos nos pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No **biblioteca de Software** área de trabalho, selecione um dos seguintes passos para o tipo de conteúdo que pretende distribuir:  

    -   **Aplicações**: Expanda **gestão de aplicações** > **aplicações**e, em seguida, selecione as aplicações que pretende distribuir. Clique na **tipos de implementação** separador e, em seguida, selecione o tipo de implementação que pretende atualizar.  

    -   **Pacotes**: Expanda **gestão de aplicações** > **pacotes**e, em seguida, selecione os pacotes que pretende atualizar.  

    -   **Pacotes de implementação**: Expanda **atualizações de Software** > **pacotes de implementação**e, em seguida, selecione os pacotes de implementação que pretende atualizar.  

    -   **Pacotes de controladores**: Expanda **sistemas operativos** > **pacotes de controladores**e, em seguida, selecione os pacotes de controladores que pretende atualizar.  

    -   **Imagens do sistema operativo**: Expanda **sistemas operativos** > **imagens do sistema operativo**e, em seguida, selecione as imagens de sistema operativo que pretende atualizar.  

    -   **Instaladores do sistema operativo**: Expanda **sistemas operativos** > **instaladores do sistema operativo**e, em seguida, selecione os instaladores do sistema operativo que pretende atualizar.  

    -   **Imagens de arranque**: Expanda **sistemas operativos** >  **imagens de arranque**e, em seguida, selecione as imagens de arranque que pretende atualizar.  

3.  No **base** separador o **implementação** grupo, clique em **atualizar pontos de distribuição**e, em seguida, clique em **OK** para confirmar que pretende atualizar o conteúdo.  

    > [!NOTE]  
    >  Para atualizar conteúdos de aplicações, clique a **tipos de implementação** separador, faça duplo clique no tipo de implementação, clique em **atualizar conteúdos**e, em seguida, clique em **OK** para confirmar que pretende atualizar o conteúdo.  

    > [!NOTE]  
    >  Quando atualizar o conteúdo para imagens de arranque, é aberto o Assistente para gerir pontos de distribuição. Reveja as informações no **resumo** página e, em seguida, conclua o Assistente para atualizar o conteúdo.  

### <a name="redistribute-content"></a>Redistribuir conteúdos
Pode redistribuir um pacote para copiar todos os ficheiros de conteúdos do pacote para pontos de distribuição ou grupos de pontos de distribuição e substituindo os ficheiros existentes.  

 Utilize esta operação para reparar ficheiros de conteúdo no pacote ou reenviar o conteúdo quando ocorre uma falha de distribuição inicial. Pode redistribuir um pacote a partir de:  

-   Propriedades do pacote  
-   Propriedades do ponto de distribuição  
-   Propriedades do grupo de ponto de distribuição.  


#### <a name="to-redistribute-content-from-package-properties"></a>Para redistribuir conteúdos a partir das propriedades do pacote  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No **biblioteca de Software** área de trabalho, selecione um dos seguintes passos para o tipo de conteúdo que pretende distribuir:  

    -   **Aplicações**: Expanda **gestão de aplicações** >  **aplicações**e, em seguida, selecione a aplicação que pretende redistribuir.  

    -   **Pacotes**: Expanda **gestão de aplicações** > **pacotes**e, em seguida, selecione o pacote que pretende redistribuir.  

    -   **Pacotes de implementação**: Expanda **atualizações de Software** >  **pacotes de implementação**e, em seguida, selecione o pacote de implementação que pretende redistribuir.  

    -   **Pacotes de controladores**: Expanda **sistemas operativos** > **pacotes de controladores**e, em seguida, selecione o pacote de controladores que pretende redistribuir.  

    -   **Imagens do sistema operativo**: Expanda **sistemas operativos** > **imagens do sistema operativo**e, em seguida, selecione a imagem de sistema operativo que pretende redistribuir.  

    -   **Instaladores do sistema operativo**: Expanda **sistemas operativos** > **instaladores do sistema operativo**e, em seguida, selecione os instaladores do sistema operativo que pretende redistribuir.  

    -   **Imagens de arranque**: Expanda **sistemas operativos** >  **imagens de arranque**e, em seguida, selecione a imagem de arranque que pretende redistribuir.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique na **localizações de conteúdo** separador, selecione o ponto de distribuição ou grupo de pontos de distribuição nos quais pretende redistribuir o conteúdos, clique em **redistribuir**e, em seguida, clique em **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-properties"></a>Para redistribuir conteúdos a partir das propriedades do ponto de distribuição  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No **administração** área de trabalho, clique em **pontos de distribuição**e, em seguida, selecione o ponto de distribuição nos quais pretende redistribuir o conteúdo.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique na **conteúdo** separador, selecione o conteúdo a redistribuir, clique em **redistribuir**e, em seguida, clique em **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-group-properties"></a>Para redistribuir conteúdos a partir das propriedades do grupo de ponto de distribuição  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No **administração** área de trabalho, clique em **grupos de pontos de distribuição**e, em seguida, selecione o grupo de pontos de distribuição nos quais pretende redistribuir o conteúdo.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique na **conteúdo** separador, selecione o conteúdo a redistribuir, clique em **redistribuir**e, em seguida, clique em **OK**.  

    > [!IMPORTANT]  
    >  O conteúdo do pacote é redistribuído a todos os pontos de distribuição do grupo de pontos de distribuição.  


#### <a name="use-the-sdk-to-force-replication-of-content"></a>Utilize o SDK para forçar a replicação de conteúdo
Pode utilizar o **RetryContentReplication** método de classe do Windows Management Instrumentation (WMI) do SDK do Configuration Manager para forçar o Gestor de distribuição para copiar o conteúdo na localização de origem para a biblioteca de conteúdos.  

Só utilize este método para forçar a replicação quando necessitará de redistribuir conteúdo após estivesse problemas com a replicação normal do conteúdo (normalmente confirmado utilizando o nó de monitorização da consola).   

Para mais informações sobre esta opção SDK, consulte o artigo [RetryContentReplication método na classe SMS_CM_UpdatePackages](https://msdn.microsoft.com/library/mt762092(CMSDK.16).aspx) no MSDN. Microsoft.com.

### <a name="remove-content"></a>Remover o conteúdo
Quando já não necessitam de conteúdo em pontos de distribuição, pode remover os ficheiros de conteúdo no ponto de distribuição.  

-   Propriedades do pacote  
-   Propriedades do ponto de distribuição  
-   Propriedades do grupo de ponto de distribuição.  

No entanto, quando o conteúdo estiver associado a outro pacote que tenha sido distribuído ao mesmo ponto de distribuição, não é possível remover o conteúdo.  

#### <a name="to-remove-package-content-files-from-distribution-points"></a>Para remover ficheiros de conteúdo de pacotes a partir de pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No **biblioteca de Software** área de trabalho, selecione um dos seguintes passos para o tipo de conteúdo que pretende eliminar:  

    -   **Aplicações**: Expanda **gestão de aplicações** > **aplicações**e, em seguida, selecione a aplicação que pretende remover.  

    -   **Pacotes**: Expanda **gestão de aplicações** > **pacotes**e, em seguida, selecione o pacote que pretende remover.  

    -   **Pacotes de implementação**: Expanda **atualizações de Software** > **pacotes de implementação**e, em seguida, selecione o pacote de implementação que pretende remover.  

    -   **Pacotes de controladores**: Expanda **sistemas operativos** > **pacotes de controladores**e, em seguida, selecione o pacote de controladores que pretende remover.  

    -   **Imagens do sistema operativo**: Expanda **sistemas operativos** > **imagens do sistema operativo**e, em seguida, selecione a imagem de sistema operativo que pretende remover.  

    -   **Instaladores do sistema operativo**: Expanda **sistemas operativos** > **instaladores do sistema operativo**e, em seguida, selecione os instaladores do sistema operativo que pretende remover.  

    -   **Imagens de arranque**: Expanda **sistemas operativos** > **imagens de arranque**e, em seguida, selecione a imagem de arranque que pretende remover.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique na **localizações de conteúdo** separador, selecione o ponto de distribuição ou grupo de pontos de distribuição a partir do qual pretende remover conteúdo, clique em **remover**e, em seguida, clique em **OK**.  

#### <a name="to-remove-package-content-from-distribution-point-properties"></a>Para remover conteúdo do pacote a partir das propriedades do ponto de distribuição  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No **administração** área de trabalho, clique em **pontos de distribuição**e, em seguida, selecione o ponto de distribuição em que pretende eliminar o conteúdo.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique na **conteúdo** separador, selecione o conteúdo a remover, clique em **remover**e, em seguida, clique em **OK**.  

#### <a name="to-remove-content-from-distribution-point-group-properties"></a>Para remover o conteúdo das propriedades do grupo de ponto de distribuição  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No **administração** área de trabalho, clique em **grupos de pontos de distribuição**e, em seguida, selecione o grupo de pontos de distribuição em que pretende remover conteúdos.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique na **conteúdo** separador, selecione o conteúdo a remover, clique em **remover**e, em seguida, clique em **OK**.  


### <a name="validate-content"></a>Validar conteúdo
O processo de validação de conteúdos verifica a integridade dos ficheiros de conteúdos em pontos de distribuição. Pode ativar a validação de conteúdos com base numa agenda ou iniciar manualmente a validação de conteúdos a partir das propriedades de pontos de distribuição e pacotes.  

 Quando o processo de validação de conteúdos é iniciado, o Gestor de configuração verifica os ficheiros de conteúdo em pontos de distribuição e se o hash do ficheiro for inesperado para os ficheiros no ponto de distribuição, o Configuration Manager cria uma mensagem de estado que poderá consultar no **monitorização** área de trabalho.  

 Para obter mais informações sobre como configurar a agenda de validação de conteúdos, consulte o artigo [configurações de pontos de distribuição](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs) no [instalar e configurar pontos de distribuição para o System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) tópico.  


#### <a name="to-initiate-content-validation-for-all-content-on-a-distribution-point"></a>Para iniciar a validação de conteúdos para todos os conteúdos de um ponto de distribuição  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No **administração** área de trabalho, clique em **pontos de distribuição**e, em seguida, selecione o ponto de distribuição em que pretende validar conteúdo.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  No **conteúdo** separador, selecione o pacote em que pretende validar o conteúdos, clique em **validar**, clique em **OK**e, em seguida, clique em **OK**. O processo de validação de conteúdos é iniciado para o pacote no ponto de distribuição.  

5.  Para ver os resultados do processo de validação de conteúdo, no **monitorização** área de trabalho, expanda **estado da distribuição**e clique na **estado do conteúdo** nó. É apresentado o conteúdo de cada tipo de pacote (por exemplo, aplicação, pacote de atualização de Software e imagem de arranque). Para obter mais informações sobre como monitorizar o estado do conteúdo, consulte o artigo [monitorizar o conteúdo ter distribuídas com o System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

#### <a name="to-initiate-content-validation-for-a-package"></a>Para iniciar a validação de conteúdos para um pacote  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No **biblioteca de Software** área de trabalho, selecione um dos seguintes passos para o tipo de conteúdo que pretende validar:  

    -   **Aplicações**: Expanda **gestão de aplicações** > **aplicações**e, em seguida, selecione a aplicação que pretende validar.  

    -   **Pacotes**: Expanda **gestão de aplicações** > **pacotes**e, em seguida, selecione o pacote que pretende validar.  

    -   **Pacotes de implementação**: Expanda **atualizações de Software** > **pacotes de implementação**e, em seguida, selecione o pacote de implementação que pretende validar.  

    -   **Pacotes de controladores**: Expanda **sistemas operativos** > **pacotes de controladores**e, em seguida, selecione o pacote de controladores que pretende validar.  

    -   **Imagens do sistema operativo**: Expanda **sistemas operativos** > **imagens do sistema operativo**e, em seguida, selecione a imagem de sistema operativo que pretende validar.  

    -   **Instaladores do sistema operativo**: Expanda **sistemas operativos** >  **instaladores do sistema operativo**e, em seguida, selecione os instaladores do sistema operativo que pretende validar.  

    -   **Imagens de arranque**: Expanda **sistemas operativos** > **imagens de arranque**e, em seguida, selecione a imagem de arranque que pretende pré-configurar.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  No **localizações de conteúdo** separador, selecione o ponto de distribuição ou grupo de pontos de distribuição na qual pretende validar o conteúdos, clique em **validar**, clique em **OK**e, em seguida, clique em **OK**. O processo de validação de conteúdos é iniciado para o conteúdo no ponto de distribuição selecionado ou grupo de pontos de distribuição.  

5.  Para ver os resultados do processo de validação de conteúdo, no **monitorização** área de trabalho, expanda **estado da distribuição**e clique na **estado do conteúdo** nó. É apresentado o conteúdo de cada tipo de pacote (por exemplo, aplicação, pacote de atualização de Software e imagem de arranque). Para obter mais informações sobre como monitorizar o estado do conteúdo, consulte o artigo [monitorizar o conteúdo ter distribuídas com o System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

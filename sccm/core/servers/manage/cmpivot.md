---
title: CMPivot para dados em tempo real
titleSuffix: Configuration Manager
description: Saiba como utilizar CMPivot no Configuration Manager para clientes de consulta em tempo real.
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2527639e3a0370c4e18d5e6030fc3a26a10c6d21
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120202"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>CMPivot para dados em tempo real no Configuration Manager

<!--1358456-->

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager sempre forneceu um armazenamento centralizado grandes de dados de dispositivo, que os clientes utilizam para fins de relatórios. O site recolhe, normalmente, estes dados numa base semanal. A partir da versão 1806, CMPivot é um novo utilitário de na consola, que agora fornece acesso ao Estado em tempo real de dispositivos no seu ambiente. Ele imediatamente, executa uma consulta em todos os dispositivos atualmente ligados na coleção de destino e retorna os resultados. Em seguida, filtrar e agrupar estes dados na ferramenta. Ao fornecer dados em tempo real de clientes online, pode mais rapidamente responder às perguntas sobre, resolver problemas e responder a incidentes de segurança.

Por exemplo, no [mitigar vulnerabilidades de canal de lado a execução especulativa](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), um dos requisitos é atualizar o BIOS do sistema. Pode utilizar CMPivot para consultar rapidamente nas informações de BIOS do sistema e encontrar os clientes que não estão em conformidade.



## <a name="prerequisites"></a>Pré-requisitos

Os seguintes componentes são necessários para utilizar CMPivot:

- Atualize os dispositivos de destino para a versão mais recente do cliente do Configuration Manager.  

- As necessidades de administrador do Configuration Manager a **leitura** permissão na **Scripts do SMS** objeto, o **executar Scripts** permissão no **coleção** e o escopo de predefinição. O **executor de Scripts** função tem estas permissões, que não é criado por predefinição. Para obter mais informações sobre como criar esta função de segurança personalizadas, consulte [funções de segurança para os scripts](/sccm/apps/deploy-use/create-deploy-scripts#bkmk_ScriptRoles).  

- Para recolher dados para as entidades a seguir, os clientes de destino requerem o PowerShell versão 5.0:  
    - Administradores
    - Ligação
    - IPConfig
    - SMBConfig 



## <a name="limitations"></a>Limitações

- Numa hierarquia, ligue a consola do Configuration Manager para uma *site primário* para executar CMPivot. O **CMPivot iniciar** ação não aparece na consola, quando está ligado a um site de administração central.  

- CMPivot devolve apenas dados de clientes ligados ao site atual.  

- Se uma coleção contém dispositivos de outro site, os resultados de CMPivot são apenas a partir de dispositivos no site atual.  

- Não é possível personalizar propriedades de entidade, colunas de resultados ou ações em dispositivos.  

- Apenas uma instância de CMPivot pode executar ao mesmo tempo num computador que está a executar a consola do Configuration Manager.  

- Na versão 1806, a consulta para o **administradores** entidade só funciona se o grupo é o nome "Administradores". Ele não funciona se o nome do grupo está localizado. Por exemplo, "Administrateurs" em francês.<!--SCCMDocs issue 759-->  



## <a name="start-cmpivot"></a>Iniciar CMPivot

1. Na consola do Configuration Manager, ligue para o site primário. Vá para o **ativos e compatibilidade** área de trabalho e selecione o **coleções de dispositivos** nó. Selecione uma coleção de destino e clique em **CMPivot iniciar** na faixa de opções para iniciar a ferramenta.  

    > [!Tip]  
    > Se não vir esta opção, veja as seguintes configurações:  
    > 
    > - Certifique-se com um administrador do site que a conta tem as permissões necessárias. Para obter mais informações, consulte [pré-requisitos](#prerequisites).  
    > 
    > - Ligue a consola para uma *site primário*.  

2. A interface fornece mais informações sobre como utilizar a ferramenta.  

     - Manualmente introduza cadeias de consulta na parte superior, ou clique nas ligações na documentação do inline.  

     - Clique da **entidades** para adicioná-lo para a cadeia de consulta.  

     - As ligações para **operadores de tabela**, **funções de agregação**, e **funções escalares** abrir documentação de referência de idioma no navegador da web. O mesmo idioma de consulta que utiliza o CMPivot [do Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/).  

3. Mantenha a janela de CMPivot aberta para ver resultados de clientes. Quando fechar a janela de CMPivot, a sessão seja concluída.  

    > [!Note]  
    > Se a consulta foi enviada, em seguida, os clientes ainda enviar uma resposta de mensagem de estado para o servidor.  



## <a name="how-to-use-cmpivot"></a>Como utilizar CMPivot

![Exemplo de janela CMPivot](media/1358456-cmpivot-sample.png)

A janela de CMPivot contém os seguintes elementos:  

1. A coleção que CMPivot atualmente destinos é na barra de título na parte superior e, na barra de estado na parte inferior da janela. Por exemplo, **todos os sistemas** na captura de ecrã acima.  

2. O painel nas listas do esquerda a **entidades** que estão disponíveis nos clientes. Algumas entidades dependem no WMI, enquanto outros utilizam o PowerShell para obter dados dos clientes.   

    - Com o botão direito uma entidade para as seguintes ações:  

       - **Inserir**: Adicione a entidade para a consulta na posição atual do cursor. A consulta não é executado automaticamente. Esta ação é o padrão quando clicar duas vezes uma entidade. Utilize esta ação ao criar uma consulta.  

       - **Consultar todos**: Execute uma consulta para esta entidade, incluindo todas as propriedades. Utilize esta ação para consultar rapidamente para uma única entidade.  

       - **Consulta pelo dispositivo**: Executar uma consulta para esta entidade e agrupar os resultados. Por exemplo, `Disk | summarize dcount( Device ) by Name`  

    - Expanda uma entidade para ver as propriedades específicas disponíveis para cada entidade. Clique duas vezes numa propriedade para adicioná-lo para a consulta na posição atual do cursor.  

3. O **home page** separador mostra informações gerais sobre CMPivot, incluindo links para exemplos de consultas e a documentação associada.  

4. O **consulta** guia exibe o painel de consulta, o painel de resultados e a barra de status. O separador de consulta está selecionado no exemplo de captura de ecrã acima.  

5. O painel de consulta é onde pode cria ou escreva uma consulta seja executada em clientes na coleção.  

    - Um subconjunto da mesma linguagem de consulta como utiliza o CMPivot [do Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/).  

    - Cortar, copiar ou cole o conteúdo no painel de consulta.  

    - Por predefinição, este painel utiliza IntelliSense. Por exemplo, se começa a digitar `D`, o IntelliSense sugere todas as entidades que começam com essa letra. Selecione uma opção e pressione Tab para inseri-lo. Escreva um caráter de pipe e um espaço `| `, e, em seguida, o IntelliSense sugere todos os operadores de tabela. Inserir `summarize` e insira um espaço e o IntelliSense sugere todas as funções de agregação. Para obter mais informações sobre esses operadores e funções, clique nas **home page** separador CMPivot.  

    - O painel de consulta também fornece as seguintes opções:  

        - Execute a consulta.  

        - Mova para trás e para frente na lista de histórico de consultas.  

        - Crie uma coleção de associação direta.  

        - Exporte os resultados da consulta para CSV ou a área de transferência.  

6. O painel de resultados apresenta os dados retornados por clientes ativos para a consulta.  

   - As colunas disponíveis variam com base na entidade e a consulta.  

   - Clique num nome de coluna para ordenar os resultados por essa propriedade.  

   - Com o botão direito em qualquer nome de coluna para agrupar os resultados pelas mesmas informações nessa coluna ou ordenar os resultados.  

   - Clique com o botão direito no nome de um dispositivo para realizar as seguintes ações adicionais no dispositivo:  

      - **Utilize também a**: Consulta para outra entidade neste dispositivo.  

      - **Executar Script**: Inicie o Assistente de executar o Script para executar um script do PowerShell existente neste dispositivo. Para obter mais informações, consulte [executar um script](/sccm/apps/deploy-use/create-deploy-scripts#run-a-script).  

      - **Controlo remoto**: Inicie uma sessão de controlo de remoto do Configuration Manager neste dispositivo. Para obter mais informações, consulte [como administrar remotamente um computador de cliente Windows](/sccm/core/clients/manage/remote-control/remotely-administer-a-windows-client-computer).  

      - **Explorador de recursos**: Inicie o Explorador de recursos do Configuration Manager para este dispositivo. Para obter mais informações, consulte [ver o inventário de hardware](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory) ou [ver o inventário de software](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory).  

   - Clique com o botão direito em qualquer célula do dispositivo não para efetuar as seguintes ações adicionais:  

     - **Cópia**: Copie o texto da célula na área de transferência.  

     - **Mostrar os dispositivos com**: Consulta para dispositivos com este valor para esta propriedade. Por exemplo, a partir dos resultados da `OS` consultar, selecione esta opção numa célula na linha da versão: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **Mostrar dispositivos sem**: Consulta para dispositivos sem este valor para esta propriedade. Por exemplo, a partir dos resultados da `OS` consultar, selecione esta opção numa célula na linha da versão: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **Bing-**: Inicie o navegador da web padrão para www.bing.com com este valor como a cadeia de consulta.  

   - Clique em qualquer texto associado à hiperligação para dinamizar o modo de exibição nessas informações específicas.  

   - O painel de resultados não mostra mais de 20 000 linhas. O ajuste a consulta para filtrar ainda mais os dados ou reiniciar CMPivot numa coleção de menor.  

7. Na barra de estado mostra as seguintes informações (da esquerda para a direita):  

   - O estado da consulta atual para a coleção de destino. Este estado inclui:  
     - O número de clientes ativos que concluir a consulta (3)  
     - O número total de clientes (5)  
     - O número de clientes offline (2)  
     - Os clientes que devolveu um erro (0)  

       Por exemplo: `Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - O ID da operação de cliente. Por exemplo: `id(16780221)`  

   - A coleção atual. Por exemplo: `PM_Team_Machines`  

   - O número total de linhas no painel de resultados. Por exemplo, `1 objects`  



## <a name="example-scenarios"></a>Cenários de exemplo

As secções seguintes fornecem exemplos de como pode utilizar CMPivot no seu ambiente:


### <a name="example-1-stop-a-running-service"></a>Exemplo 1: Parar um serviço em execução

O administrador de segurança pede-lhe para parar e desativar o serviço pesquisador de computadores mais depressa possível em todos os dispositivos do departamento de contabilidade. Iniciar CMPivot numa coleção para todos os dispositivos na gestão de contas e selecione **consultar todos** sobre o **serviço** entidade. 

`Service`

Como os resultados são apresentados, com o botão direito no **Name** coluna e selecione **Agrupar por**. 

`Service | summarize dcount( Device ) by Name`

Na linha do **Browser** serviço, clicar no número associado à hiperligação na **dcount_** coluna. 

`Service | where (Name == 'Browser') | summarize count() by Device`

Selecionar vários todos os dispositivos, com o botão direito a seleção e escolha **executar Script**. Esta ação inicia o Assistente de executar o Script, em que executa um script existente que tiver para parar e desativar um serviço. Com CMPivot responde rapidamente a incidente de segurança para todos os computadores Active Directory, ver os resultados no Assistente de executar o Script. Então seguimento para criar uma linha de base de configuração para remediar outros computadores na coleção, à medida que ficam Active Directory no futuro. 

![Exemplo de CMPivot para o serviço de Browser e a ação de Script de executar](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>Exemplo 2: Proativamente resolver falhas de aplicações  

Para ser proativo com a manutenção operacional, uma vez por semana CMPivot é executado em relação a uma coleção de servidores que gerir e selecione **consultar todas** sobre o **AppCrash** entidade. Com o botão direito a **FileName** coluna e selecione **ordenação ascendente**. Um dispositivo devolve resultados de sete para sqlsqm.exe com um carimbo cerca UTC+03:00 todos os dias. Selecione o nome do arquivo em uma das linhas, faça duplo clique nele e selecione **Bing-**. Navegação nos resultados da pesquisa no navegador da web, encontrar um artigo de suporte da Microsoft para este problema com mais informações e resolução. 


### <a name="example-3-bios-version"></a>Exemplo 3: Versão do BIOS

Para [mitigar vulnerabilidades de canal de lado a execução especulativa](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), um dos requisitos é atualizar o BIOS do sistema. Começar com uma consulta para o **BIOS** entidade. Em seguida, **Agrupar por** a **versão** propriedade. Em seguida, um valor específico, como "LENOVO - 1140", com o botão direito e selecione **mostrar os dispositivos com**.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Exemplo 4: Espaço livre em disco

Precisa armazenar temporariamente um arquivo grande num servidor de ficheiros de rede, mas não tem a certeza qual deles tem capacidade suficiente. Iniciar CMPivot em relação a uma coleção de servidores de ficheiros e consultar a **disco** entidade. Modifique a consulta para CMPivot voltar rapidamente uma lista de servidores Active Directory com dados do armazenamento em tempo real:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`



## <a name="inside-cmpivot"></a>CMPivot interior

CMPivot envia consultas para clientes que utilizam o Gestor de configuração "canal rápido". Este canal de comunicação do servidor para cliente também é utilizado por outros recursos, tais como ações de notificação do cliente, o estado do cliente e o Endpoint Protection. Os clientes devolverão resultados através do sistema de mensagem de estado da mesma forma rápida. Mensagens de estado de são temporariamente armazenadas na base de dados. 

As consultas e os resultados são todos somente texto. As entidades **InstallSoftware** e **processo** retorna algumas dos maiores conjuntos de resultados. Durante os testes de desempenho, o maior tamanho de ficheiro de mensagem de estado de um cliente para estas consultas foi inferior a **1 KB**. Dimensionado para um ambiente de grandes dimensões com 50 000 clientes do Active Directory, esta consulta única geraria inferior a 50 MB de dados através da rede.  

Uma consulta exceder o tempo limite após uma hora. Por exemplo, uma coleção tem 500 dispositivos, e 450 dos clientes estão atualmente online. Esses dispositivos ativos recebem a consulta e devolvem os resultados quase imediatamente. Se deixar a janela de CMPivot aberto, como os outros 50 clientes ficam online, eles também recebem a consulta e devolvem resultados. 

>[!TIP]
> CMPivot interations são registadas para os ficheiros de registo seguinte:
>
> **Lado do servidor:**
> - SmsProv.log
> - bgbServer.log
> - StateSys.log
>
> **Lado do cliente:**
> - CcmNotificationAgent.log
> - Scripts.log
> - StateMessage.log
>
> Para obter mais informações, consulte [ficheiros de registo](/sccm/core/plan-design/hierarchy/log-files).


## <a name="see-also"></a>Consulte também
[Criar e executar scripts do PowerShell](/sccm/apps/deploy-use/create-deploy-scripts)

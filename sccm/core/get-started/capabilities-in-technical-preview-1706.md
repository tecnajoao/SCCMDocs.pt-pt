---
title: "Visualização técnica 1706 | Microsoft Docs"
description: "Saiba mais sobre os recursos disponíveis na versão de visualização técnica 1706 para o System Center Configuration Manager."
ms.custom: na
ms.date: 06/30/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6f9e6e93fce95666503907010a5c253158c5de7c
ms.openlocfilehash: d45f504dfe0a4c7852b0e2c8ff60d54005346c02
ms.contentlocale: pt-pt
ms.lasthandoff: 07/07/2017

---
# <a name="capabilities-in-technical-preview-1706-for-system-center-configuration-manager"></a>Recursos no Technical Preview 1706 do System Center Configuration Manager.

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos que estão disponíveis na visualização técnica para o System Center Configuration Manager, versão 1706. Você pode instalar esta versão para atualizar e adicionar novos recursos ao seu site do Configuration Manager technical preview. Antes de instalar esta versão da visualização técnica, analise [visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para usar uma visualização técnica, como atualizar entre versões e como fornecer comentários sobre os recursos em uma visualização técnica.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos nesta visualização técnica:**

-   **Mover o ponto de distribuição** -as opções no console para mover um ponto de distribuição entre sites não podem ser usadas com esta versão devido ao limite de visualização técnica de um único site primário.

-   **Configurações de conformidade do dispositivo** -comportamento oposto podem ocorrer durante as duas das novas configurações de conformidade do dispositivo:
    - **Bloquear a depuração de USB no dispositivo**
    - **Bloco de aplicativos de fontes desconhecidas**

        Por exemplo, se o conjunto de administradores **depuração de USB do bloco no dispositivo** para **true**, todos os dispositivos que não têm a depuração de USB habilitado são marcados como não compatíveis.

**A seguir estão os novos recursos, que você pode experimentar com esta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improved-boundary-groups-for-software-update-points"></a>Grupos de limites aprimorada para pontos de atualização de software
<!-- 1324591 -->
Esta versão inclui aperfeiçoamentos para o funcionam dos pontos de atualização de software com grupos de limites. O exemplo a seguir resume o novo comportamento de fallback:
-   Fallback para pontos de atualização de software agora usa um tempo configurável para fallback para grupos de limites de vizinho, com um tempo mínimo de 120 minutos.

-   Independentemente da configuração de fallback, um cliente tenta acessar o último ponto de atualização de software que ele usado para 120 minutos. Após a falha ao acessar o servidor para 120 minutos, o cliente verifica seu pool de pontos de atualização de software disponíveis, em seguida, para que ele possa encontrar um novo.

  -   Todos os pontos de atualização de software no grupo de limite atual do cliente são adicionados ao pool do cliente imediatamente.

  -   Como um cliente tenta usar seu servidor original para 120 minutos antes de atingir uma nova, sem servidores adicionais são contatados até depois de duas horas.

  -   Se o fallback para um grupo de vizinho estiver configurado para o mínimo de 120 minutos, pontos de atualização de software do grupo de limite vizinho será parte do pool do cliente de servidores disponíveis.

-   Após a falha ao alcançar o servidor original por duas horas, o cliente muda para um ciclo mais curto para entrar em contato com um novo ponto de atualização de software.

    Isso significa que se um cliente não conseguir se conectar com um novo servidor, ele seleciona o próximo servidor a partir do pool de servidores disponíveis e rapidamente tenta contatar um.

  -   Esse ciclo continua até que o cliente se conecta a um software de atualização de ponto que pode ser usado.
  -   Até que o cliente encontrar um ponto de atualização de software, servidores adicionais são adicionados ao pool de servidores disponíveis quando o tempo de fallback para cada grupo de limites de vizinho for atendido.

Para obter mais informações, consulte [pontos de atualização de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) o tópico de grupos de limites para a ramificação atual.


## <a name="site-server-role-high-availability"></a>Disponibilidade alta da função de servidor de site
<!-- 1128774 -->
Alta disponibilidade para a função de servidor de site é uma solução com base do Configuration Manager para instalar um servidor de site primário adicional no *passivo* modo. O servidor do site de modo passivo Além disso é o servidor de site primário existente que está em *Active* modo. Um servidor do site de modo passivo está disponível para uso imediato, quando necessário.

Um servidor de site primário no modo passivo:
-   Usa o mesmo banco de dados do site como o servidor do site ativo.
-   Recebe uma cópia da biblioteca de conteúdo de servidores de site ativo, que é mantida em sincronia.
-   Não gravar dados no banco de dados do site enquanto ele está em modo passivo.
-   Não suporta instalação ou remoção de funções do sistema de site opcional desde que ele está em modo passivo.

Para tornar o servidor do site de modo passivo seu servidor do site de modo ativo, manualmente promovê-lo. Isso alterna o servidor de site ativo para ser o servidor do site passivo. As funções de sistema de site que estão disponíveis no servidor de modo ativo original permanecem disponíveis, desde que o computador está acessível. Somente a função de servidor de site é alternada entre o modo ativo e passivo.

Para instalar um servidor do site de modo passivo, você deve usar o **criar Assistente de servidor de sistema de Site** para configurar um novo servidor do site com um tipo de **servidor do site primário** e um modo de **passivo**. O assistente, em seguida, executa a instalação do Configuration Manager no servidor especificado para instalar o novo servidor do site no modo passivo. Após a conclusão da instalação, o servidor do site de modo ativo mantém o servidor do site de modo passivo e sua biblioteca de conteúdo em sincronia com as alterações ou configurações que você faz para o servidor do site ativo.

### <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações
-   Um único servidor do site no modo passivo é suportado em cada site primário.

-   O servidor do site no modo passivo pode ser local ou baseado em nuvem no Azure.

-   Os servidores do site de modo passivo e modo ativo devem ser do mesmo domínio.

-   O modo ativo e os servidores do site de modo passivo devem usar o mesmo site banco de dados, que deve ser remoto dos computadores de cada servidor do site.

    -   O SQL Server que hospeda o banco de dados pode usar uma instância padrão, chamado de instância, o cluster do SQL Server ou um grupo de disponibilidade AlwaysOn.

    -   O servidor do site no modo passivo é configurado para usar o mesmo banco de dados do site como o servidor do site de modo ativo. No entanto, o servidor do site de modo passivo não usa esse banco de dados até depois que ele é promovido para o modo ativo.

-   O computador que executará o servidor do site de modo passivo:

    -   Deve atender a [pré-requisitos para instalar um site primário](https://docs.microsoft.com/en-us/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).

    -   Usando arquivos de origem que correspondem à versão do servidor do site de modo ativo é instalado.

    -   Não é possível ter uma função de sistema de site de qualquer site antes de instalar o site de modo passivo.

-   Os computadores de servidor do site de modo ativo e passivo podem executar diferentes sistemas operacionais ou versões de service pack, desde que ambos permanecem suportados pela versão do Configuration Manager.

-   Promoção do servidor do site de modo passivo para o servidor de modo ativo é manual. Não há nenhum failover automático.

-   Funções do sistema de site podem ser instaladas somente no servidor do site que está no modo ativo.

    -   Um servidor do site no modo ativo dá suporte a todas as funções de sistema de site. Você não pode instalar funções do sistema de site no servidor quando ele estiver no modo passivo.

    -   Funções de sistema de site que usam um banco de dados (como o ponto de relatório) devem ter o banco de dados em um servidor remoto do modo ativo e servidores do site de modo passivo.

    -   O SMS_Provider não instalar no servidor do site no modo passivo. Como você deve se conectar a um SMS_Provider para o site para promover manualmente o servidor do site de modo passivo para o modo ativo, é recomendável [instalar pelo menos uma instância adicional do provedor](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider) em um computador adicional.

**Problema conhecido**:   
Com esta versão, **Status** para as seguintes condições são exibidas no console do como valores numéricos em vez de texto legível:
-   131071 – Falha na instalação do servidor de site
-   720895 – Falha na desinstalação de função de servidor site
-   851967 – falha no Failover

### <a name="add-a-site-server-in-passive-mode"></a>Adicionar um servidor de site no modo passivo
1.  No console, vá para **administração** > **configuração do Site** > **Sites** e iniciar o [Adicionar Assistente de funções de sistema de Site](/sccm/core/servers/deploy/configure/install-site-system-roles). Você também pode usar o **criar Assistente de servidor de sistema de Site**.

2.  Sobre o **geral** página, especifique o servidor que hospedará o servidor do site de modo passivo. O servidor especificado não pode hospedar outras funções do sistema de site antes de instalar um servidor do site no modo passivo.

3.  Sobre o **seleção de função do sistema** , selecione apenas **servidor do site primário no modo passivo**.

4.  Para concluir o assistente, você deve fornecer as seguintes informações que são usadas para executar a instalação e instalar a função de servidor de site no servidor especificado:
    -   Optar por copiar os arquivos de instalação do servidor do site ativo para o novo servidor do site de modo passivo ou especifique um caminho para um local que contém o conteúdo do servidor site ativo **CD. Última** pasta.

    -   Especifique o mesmo servidor de banco de dados do site e o nome do banco de dados usado pelo servidor do site de modo ativo.

5.  Em seguida, o Configuration Manager instala o servidor do site no modo passivo no servidor especificado.

Status de instalação detalhadas, acesse **administração** > **configuração do Site** > **Sites**.
-   Exibe o status do servidor do site no modo passivo como **instalando**.

-   Selecione o servidor e, em seguida, clique em **Mostrar Status** abrir **Status de instalação do servidor de Site** para obter mais informações.



### <a name="promote-the-passive-mode-site-server-to-active-mode"></a>Promover o servidor do site de modo passivo para o modo ativo
Quando você quiser alterar o servidor de site de modo passivo para o modo ativo, faça isso o **nós** painel **administração** > **configuração do Site** > **Sites**. Desde que você pode acessar uma instância do SMS_Provider, você pode acessar o site para fazer essa alteração.
1.  No **nós** painel do console do Configuration Manager, selecione o servidor do site no modo passivo e, em seguida, na faixa de opções, escolha **promover para ativo**.

2.  Simples **Status** para o servidor que você está promovendo exibe no **nós** painel como **promoção**.

3.  Depois que a promoção for concluída, o **Status** coluna mostra **Okey** para novo *Active* servidor do site de modo e para o novo *passivo* servidor de site do modo.

4.  Em **administração** > **configuração do Site** > **Sites**, o nome do servidor do site primário agora exibe o nome do novo *Active* servidor de site do modo.
Para o status detalhado, vá para **monitoramento** > **Status do servidor de Site**.
    -   O **modo** coluna identifica qual servidor *Active* ou *passivo*.

    -   Ao promover um servidor de modo passivo para o modo ativo, selecione o servidor de site que você está promovendo como ativo e, em seguida, escolha **Mostrar Status** na faixa de opções. Isso abre o **Status de promoção do servidor de Site** janela que exibe detalhes adicionais sobre o processo.

Quando um servidor do site no modo ativo muda para o modo passivo, somente a função de sistema de site é feita passiva. Todas as outras funções de sistema de site que estão instaladas no computador permanecem ativas e acessível aos clientes.


### <a name="daily-monitoring"></a>Monitoramento diário
Quando você tiver um site primário no modo passivo, monitore-diariamente para garantir que ele permaneça em sincronia com o servidor do site de modo ativo e pronto para uso. Para fazer isso, vá para **monitoramento** > **Status do servidor de Site**. Aqui você pode exibir o modo ativo e os servidores do site de modo passivo.

O **resumo** guia:
-   O **modo** coluna identifica qual servidor está ativo ou passivo.
-   O **Status** listas de colunas **Okey** quando o servidor de modo passivo está em sincronia com o servidor de modo ativo.
-   Para exibir detalhes adicionais sobre o estado de sincronização de conteúdo, clique em **Mostrar status** do estado de sincronização de conteúdo. Isso abre a guia de biblioteca de conteúdo em que você pode tentar corrigir problemas de sincronização de conteúdo.

O **biblioteca de conteúdo** guia:
-   Exibição de **estado** para conteúdo que sincroniza do servidor do site ativo para o servidor do site de modo passivo.
-   Você pode selecionar o conteúdo com um estado de **falha**e, em seguida, escolha **sincronizar itens selecionados** na faixa de opções. Essa ação tenta ressincronizar esse conteúdo de origem do conteúdo para o servidor do site de modo passivo. Durante a recuperação, o estado exibe como **em andamento**, e quando ele está em sincronizado, ele exibe como **sucesso**.

### <a name="try-it-out"></a>Experimente!
Tente concluir as seguintes tarefas e, em seguida, envie-nos **comentários** do **início** guia da faixa de opções para nos contar como ela funcionou:
-   Posso instalar um site primário no modo passivo.
-   Posso usar o console para promover o servidor do site de modo passivo para tornar o servidor do site de modo ativo e confirme a alteração do status de ambos os servidores de site.


## <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Incluir relação de confiança para arquivos e pastas específicos em uma política de proteção do dispositivo
<!-- 1324676 -->
Nesta versão, adicionamos mais recursos para [Device Guard](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) gerenciamento de política

Agora você pode adicionar opcionalmente a relação de confiança para arquivos específicos para pastas em uma política de proteção do dispositivo. Isso permite que você:

1.  Solucionar problemas com comportamentos do instalador gerenciado
2.  Aplicativos de linha de negócios de confiança que não podem ser implantados com o Configuration Manager
3.  Confie em aplicativos que estão incluídos em uma imagem de implantação de sistema operacional.

### <a name="try-it-out"></a>Experimente!

1.  Enquanto você estiver criando uma política de proteção do dispositivo, na guia inclusões do Assistente para criar o Device Guard política, clique em **adicionar**.
2.  No **Adicionar arquivo confiável ou pasta** caixa de diálogo, especifique informações sobre o arquivo ou pasta que você deseja confiar. Você pode especificar um caminho de arquivo ou pasta local ou se conectar a um dispositivo remoto ao qual você tem permissão para se conectar e especifique um caminho de arquivo ou pasta em que o dispositivo.
3.  Conclua o assistente.


## <a name="hide-task-sequence-progress"></a>Ocultar o andamento da sequência de tarefas
<!-- 1354291 -->
Nesta versão, você pode controlar quando o andamento da sequência de tarefas é exibido aos usuários finais por meio de uma nova variável. Na sequência de tarefas, use o **definir variável de sequência de tarefas** etapa para definir o valor para o **TSDisableProgressUI** variável para ocultar ou exibir o andamento da sequência de tarefas. Você pode usar a etapa Definir variável de sequência de tarefas várias vezes em uma sequência de tarefas para alterar o valor da variável. Isso permite ocultar ou exibir o andamento da sequência de tarefas em diferentes seções da sequência de tarefas.

#### <a name="to-hide-task-sequence-progress"></a>Para ocultar o andamento da sequência de tarefas
No editor de sequência de tarefas, use o [definir variável de sequência de tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) etapa para definir o valor da **TSDisableProgressUI** variável para **True** para ocultar o andamento da sequência de tarefas.

#### <a name="to-display-task-sequence-progress"></a>Para exibir o andamento da sequência de tarefas
No editor de sequência de tarefas, use o [definir variável de sequência de tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) etapa para definir o valor da **TSDisableProgressUI** variável para **False** para exibir o andamento da sequência de tarefas.

## <a name="specify-a-different-content-location-for-install-content-and-uninstall-content"></a>Especificar um local de conteúdo diferente para o conteúdo de instalar e desinstalar o conteúdo
<!-- 1097546 -->
No Configuration Manager atualmente, você especificar o local de instalação que contém os arquivos de instalação para um aplicativo. Quando você especificar um local de instalação, isso também é usado como o local de desinstalação para o conteúdo do aplicativo.
Com base nos seus comentários, quando você deseja desinstalar um aplicativo implantado e o conteúdo do aplicativo não está no computador cliente, em seguida, o cliente baixará todos os arquivos de instalação do aplicativo novamente antes do aplicativo é desinstalado.
Para resolver esse problema, agora você pode especificar os dois uma instalação de conteúdo local e um recurso opcional desinstalar o local do conteúdo. Além disso, você pode optar por não especificar um local de conteúdo de desinstalação.

### <a name="try-it-out"></a>Experimente!

1. Nas propriedades de tipo de implantação de um aplicativo, clique no **conteúdo** guia.
2. Configurar o **conteúdo local de instalação** como normal.
3. Para **desinstalar as configurações do conteúdo**, escolha um dos seguintes:
    - **Mesmo que instalar conteúdo** -será usado o mesmo local do conteúdo, independentemente de se você estiver instalando ou desinstalando o aplicativo.
    - **Nenhum conteúdo de desinstalação** -Escolha esta opção se você não quiser fornecer um local de conteúdo de desinstalação para o aplicativo.
    - **Diferente do conteúdo da instalação** -Escolha esta opção se você deseja especificar um local de conteúdo de desinstalação é diferente do local de conteúdo de instalação.
5. Se você selecionou **difere do conteúdo de instalação**, procurar ou digite o local do conteúdo de aplicativo que será usado para desinstalar o aplicativo.
6. Clique em **Okey** para fechar a caixa de diálogo de propriedades de tipo de implantação.


## <a name="accessibility-improvements"></a>Aprimoramentos de acessibilidade  
<!--1253000 -->
Essa visualização apresenta vários aprimoramentos para o [recursos de acessibilidade](/sccm/core/understand/accessibility-features) no console do Configuration Manager. Estas atualizações incluem:     

**Novos atalhos de teclado para movimentar-se o console:**
-   CTRL + M - define se concentrar no painel principal (central).
-   CTRL + T - define o destaque o nó superior no painel de navegação. Se o foco já estiver nesse painel, o foco é definido para o último nó que você visitou.
-   CTRL + I - define o destaque para a barra de navegação de trilha abaixo da faixa de opções.
-   CTRL + L - define o destaque o **pesquisa** campo, quando disponível.
-   CTRL + D - define o destaque o painel de detalhes, quando disponível.
-   ALT – altera o foco para dentro e fora da faixa de opções.

**Melhorias gerais:**
-   Melhorar a navegação no painel de navegação quando você digita as letras de um nome de nó.
-   Navegação de teclado por meio do modo de exibição principal e a faixa de opções agora são circulares.
-   Agora, a navegação pelo teclado no painel de detalhes é circular. Para retornar para o painel ou o objeto anterior, use Ctrl + D, em seguida, Shift + TAB.
-   Depois de atualizar um modo de exibição do espaço de trabalho, o foco é definido para o painel principal do espaço de trabalho.
-   Corrigido um problema para permitir que os leitores de tela de anunciar os nomes dos itens de lista.
-   Adicionado nomes acessíveis para vários controles na página que permite que os leitores de tela de anunciar informações importantes.


## <a name="changes-to-the-azure-services-wizard-to-support-upgrade-readiness"></a>Alterações para o Assistente de serviços do Azure para oferecer suporte a preparação para atualização
<!-- 1353331 -->
A partir desta versão, use o Assistente de serviços do Azure para configurar uma conexão do Configuration Manager para [atualizar preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics). O uso do assistente simplifica a configuração do conector usando um assistente comuns de serviços do Azure relacionados.   

Embora o método para configurar a conexão foi alterado, pré-requisitos para a conexão e como você pode usar preparação para atualização permanecem inalterados.   

### <a name="prerequisites-for-upgrade-readiness"></a>Pré-requisitos para a preparação para atualização
Os pré-requisitos para uma [conexão para preparação de atualização](/sccm/core/clients/manage/upgrade/upgrade-analytics#create-a-connection-to-upgrade-readiness) são as mesmas detalhadas para a atual ramificação do Configuration Manager. Eles são repetidos aqui por conveniência:  

**Pré-requisitos**
-   Para adicionar a conexão, o seu ambiente do Configuration Manager deve primeiro configurar uma [ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) em uma [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation). Quando você adiciona a conexão ao seu ambiente, ele também instalará o Microsoft Monitoring Agent no computador que executa essa função do sistema de site.
-   Registrar o Configuration Manager como uma ferramenta de gerenciamento "Aplicativo Web e/ou API Web" e obter o [ID do cliente do registro](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
-   Crie uma chave de cliente para a ferramenta de gerenciamento registrados no Active Directory do Azure.
-   No Portal de gerenciamento do Azure, forneça o aplicativo web registrado com permissão para acessar o OMS, conforme descrito em [fornecem o Configuration Manager com permissões para OMS](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

> [!IMPORTANT]       
> Ao configurar a permissão para acessar o OMS, certifique-se de escolher o **Colaborador** função e atribua a ela permissões para o grupo de recursos do aplicativo registrado.

Depois que os pré-requisitos estiverem configurados, você está pronto para usar o Assistente para criar a conexão.

### <a name="use-the-azure-services-wizard-to-configure-upgrade-readiness"></a>Use o Assistente de serviços do Azure para configurar a preparação para atualização
1.  No console, vá para **administração** > **visão geral** > **serviços de nuvem** > **serviços do Azure**e, em seguida, escolha **configurar os serviços do Azure** do **início** guia da faixa de opções, para iniciar o **Assistente serviços Azure**.

2.  Sobre o **serviços do Azure** página, selecione o **conector de preparação de atualização**e, em seguida, clique em **próximo**.

3.  Sobre o **aplicativo** , especifique seu **ambiente do Azure** (technical preview oferece suporte somente a nuvem pública). Em seguida, clique em **importação** para abrir o **importar aplicativos** janela.

4.  No **importar aplicativos** janela, especifique os detalhes de um aplicativo web que já existe no AD do Azure.
    -   Forneça um nome amigável para o nome do locatário do AD do Azure. Em seguida, especifique a ID de locatário, o nome do aplicativo, a ID do cliente, a chave secreta para o aplicativo web do Azure e o URI de ID do aplicativo.
    -   Clique em **verificar**e se for bem-sucedido, clique em **Okey** para continuar.

5.   Sobre o **configuração** página, especifique a assinatura, o grupo de recursos e o espaço de trabalho de análise do Windows que deseja usar com esta conexão para preparação de atualização.  

6.  Clique em **próximo** para ir para o **resumo** página e, em seguida, conclua o Assistente para criar a conexão.


## <a name="new-client-settings-for-cloud-services"></a>Novas configurações de cliente para serviços de nuvem
<!-- 1319883 -->

Nesta versão, adicionamos duas novas configurações de cliente do Configuration Manager. Você encontrará esses no **serviços de nuvem** seção.  Essas configurações fornecem os seguintes recursos:

- Controlar quais clientes do Configuration Manager podem acessar um gateway de gerenciamento de nuvem é configurada.
- Registre automaticamente os clientes Windows 10 ingressados no domínio do Configuration Manager com o Active Directory do Azure.

Essas novas configurações ajudam você a realizar os recursos descritos no [1705 do Configuration Manager Technical Preview](/sccm/core/get-started/capabilities-in-technical-preview-1705#new-capabilities-for-azure-ad-and-cloud-management).

### <a name="before-you-start"></a>Antes de começar

Você deve ter instalado e configurado o Azure AD Connect entre o Active Directory no local e seu locatário do AD do Azure.

Se você remover a conexão, os dispositivos não são cancelados, mas nenhum novo dispositivo será registrado.

### <a name="try-it-out"></a>Experimente!

1. Configure a seguinte seção de configurações (encontradas nos serviços de nuvem) cliente usando as informações em [como definir as configurações de cliente](/sccm/core/clients/deploy/configure-client-settings).
    -   **Registrar automaticamente os novos dispositivos de ingressados no domínio do Windows 10 com o Azure Active Directory** – defina como **Sim** (padrão), ou **não**.
    -   **Habilitar clientes para usar um gateway de gerenciamento de nuvem** – defina como **Sim** (padrão), ou **não**.
2.  Implante as configurações do cliente na coleção necessária de dispositivos.

Para confirmar que o dispositivo está unido ao AD do Azure, execute o comando **dsregcmd.exe /status** em uma janela de prompt de comando. O **AzureAdjoined** campo nos resultados mostrarão **Sim** se o dispositivo está unido do AD do Azure.

## <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Criar e executar scripts do PowerShell do console do Configuration Manager
<!-- 1236459 -->

No Configuration Manager, você pode implantar scripts para os dispositivos de cliente usando pacotes e programas. Esse technical preview, adicionamos a nova funcionalidade que permite que você execute as seguintes ações:

- Importar Scripts do PowerShell para o Configuration Manager
- Editar os scripts do console do Configuration Manager (para scripts não assinados apenas)
- Scripts de marca como aprovado ou negado, para melhorar a segurança
- Executar scripts em coleções de computadores de cliente do Windows e de locais gerenciados PCs com Windows. Você não implantar scripts, em vez disso, eles são executados em tempo real em dispositivos cliente.
- Examine os resultados retornados pelo script no console do Configuration Manager.


### <a name="prerequisites"></a>Pré-requisitos

Para usar scripts, você deve ser um membro da função de segurança apropriado do Configuration Manager.

- **Para importar e criar scripts** -sua conta deve ter **criar** permissões para **SMS Scripts** no **Gerenciador de configurações de conformidade** função de segurança.
- **Para aprovar ou negar scripts** -sua conta deve ter **aprovar** permissões para **SMS Scripts** no **Gerenciador de configurações de conformidade** função de segurança.
- **Para executar scripts** -sua conta deve ter **Executar Script** permissões para **coleções** no **Gerenciador de configurações de conformidade** função de segurança.

Para obter mais informações sobre funções de segurança do Configuration Manager, consulte [conceitos básicos da administração baseada em função](/sccm/core/understand/fundamentals-of-role-based-administration).

Por padrão, os usuários não é possível aprovar um script que criou. Como scripts são poderoso e versátil e podem ser implantados em vários dispositivos, apresentamos um novo conceito de fornecer a capacidade de separar as funções entre a pessoa que os autores de script e a pessoa que aprova o script. Isso fornece um nível adicional de segurança contra a execução de um script sem supervisão. Você pode desativar esta aprovação secundária, para facilitar o teste, especialmente durante a versão de visualização técnica.

Para permitir que os usuários aprovem seus próprios scripts:

1. Na consola do Configuration Manager, clique em **Administração**.
2. Na área de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.
3. Na lista de sites, escolha o seu site e, em seguida, no **início** guia o **Sites** de grupo, clique em **configurações da hierarquia**.
4. No **geral** guia do **propriedades de configurações de hierarquia** caixa de diálogo caixa, desmarque a caixa de seleção **não permitem que os autores de script aprovar seus próprios scripts**.


### <a name="try-it-out"></a>Experimente!

#### <a name="import-and-edit-a-script"></a>Importar e editar um script

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. No **biblioteca de Software** espaço de trabalho, clique em **Scripts**.
3. No **início** guia o **criar** de grupo, clique em **criar Script**.
4. No **Script** página do **criar Script** assistente, configure o seguinte:
    - **Nome do script** -Insira um nome para o script. Embora você possa criar vários scripts com o mesmo nome, isso tornará mais difícil localizar o script que é necessário no console do Configuration Manager.
    - **Linguagem de script** - atualmente, apenas **PowerShell** scripts têm suporte.
    - **Importação** -importar um script do PowerShell para o console. O script é exibido no **Script** campo.
    - **Limpar** -remove o script atual a partir de **Script** campo.
    - **Script** -exibe o script importado no momento. Você pode editar o script neste campo conforme necessário.
5. Conclua o assistente. O novo script é exibido no **Script** lista com um status de **aguardando aprovação**. Antes de executar esse script em dispositivos cliente, você deve aprová-lo.


#### <a name="approve-or-deny-a-script"></a>Aprovar ou negar um script



Antes de executar um script, ele deve ser aprovado. Para aprovar um script:

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. No **biblioteca de Software** espaço de trabalho, clique em **Scripts**.
3. No **Script** , escolha o script que você deseja aprovar ou negar e, em seguida, no **início** guia o **Script** de grupo, clique em **aprovar/Deny**.
4. No **aprovar ou negar script** caixa de diálogo, **aprovar**, ou **Deny** o script e, opcionalmente, insira um comentário sobre a sua decisão. Se você negar um script, ele não pode ser executado em dispositivos cliente.
5. Conclua o assistente. No **Script** lista, você verá o **estado de aprovação** alteração de coluna dependendo da ação executada.

#### <a name="run-a-script"></a>Executar um script

Depois que um script tiver sido aprovado, ela pode ser executada em uma coleção que você escolher.

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2. Na área de trabalho **Ativos e Compatibilidade** , clique em **Coleções de Dispositivos**.
3. No **coleções de dispositivos** lista, clique na coleção de dispositivos nos quais você deseja executar o script.
3. No **início** guia o **todos os sistemas** de grupo, clique em **Executar Script**.
4. No **Script** página do **Executar Script** assistente, escolha um script na lista. Somente scripts aprovados são mostrados. Clique em **próximo**e, em seguida, conclua o assistente.

#### <a name="monitor-a-script"></a>Monitorar um script

Depois de executar um script para os dispositivos cliente, use este procedimento para monitorar o sucesso da operação.

1. No console do Configuration Manager, clique em **monitoramento**.
2. No **monitoramento** espaço de trabalho, clique em **resultados do Script**.
3. No **resultados do Script** lista, que você exibir os resultados para cada script executado em dispositivos cliente. Um código de saída do script **0**, geralmente indica que o script foi executado com êxito.

## <a name="pxe-network-boot-support-for-ipv6"></a>Suporte de inicialização de rede do PXE para IPv6
<!-- 1269793 -->
Agora você pode habilitar o suporte de inicialização de rede do PXE para IPv6 iniciar uma implantação de sistema operacional da sequência de tarefas. Quando você usa essa configuração, os pontos de distribuição habilitados para PXE oferecerá suporte IPv4 e IPv6. Essa opção não exige que o WDS e interromperá o WDS, se ele estiver presente.

#### <a name="to-enable-pxe-boot-support-for-ipv6"></a>Para habilitar o suporte de inicialização PXE para IPv6
Use o procedimento a seguir para habilitar a opção para suporte a IPv6 para PXE.

1. No console do Configuration Manager, vá para **administração** > **visão geral** > **pontos de distribuição**e clique em **propriedades** para pontos de distribuição habilitados para PXE.
2. Sobre o **PXE** guia, selecione **suporte a IPv6** para habilitar o suporte a IPv6 para PXE.

## <a name="manage-microsoft-surface-driver-updates"></a>Gerenciar atualizações de driver do Microsoft Surface
<!-- 1098490 -->
Agora você pode usar o Configuration Manager para gerenciar atualizações de driver do Microsoft Surface.

### <a name="prerequisites"></a>Pré-requisitos
Todos os pontos de atualização de software devem executar o Windows Server 2016.

### <a name="try-it-out"></a>Experimente!
Tente concluir as seguintes tarefas e, em seguida, envie-nos **comentários** do **início** guia da faixa de opções para nos contar como ela funcionou:
1. Habilite a sincronização para os drivers da Microsoft Surface. Use o procedimento [Configurar classificação e produtos](/sccm/sum/get-started/configure-classifications-and-products) e selecione **drivers incluem Microsoft Surface e atualizações de firmware** no **classificações** guia para permitir que drivers de superfície.
2. [Sincronizar os drivers da Microsoft Surface](/sccm/sum/get-started/synchronize-software-updates.md).
3. [Implantar pacotes de drivers Microsoft Surface sincronizados](/sccm/sum/deploy-use/deploy-software-updates)

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configurar o Windows Update para políticas de adiamento de negócios
<!-- 1290890 -->
Agora você pode configurar políticas de adiamento de atualizações de recurso do Windows 10 ou qualidade atualizações para o Windows 10 dispositivos gerenciados diretamente pelo Windows Update para empresas. Você pode gerenciar as políticas de adiamento no novo **Windows Update para políticas de negócios** nó **biblioteca de Software** > **serviço do Windows 10**.

### <a name="prerequisites"></a>Pré-requisitos
Dispositivos Windows 10 gerenciados pelo Windows Update para empresas devem ter conectividade com a Internet.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Para criar uma atualização do Windows para a política de adiamento de negócios
1. Em **biblioteca de Software** > **serviço do Windows 10** > **Windows Update para políticas de negócios**
2. No **início** guia o **criar** grupo, selecione **criar o Windows Update para política de negócios** para abrir o Windows Update criar Assistente de política de negócios.
3. Sobre o **geral** , forneça um nome e uma descrição para a política.
4. No **políticas de adiamento** página, defina se deseja adiar ou pausar atualizações do recurso.    
    Atualizações de recurso são geralmente novos recursos do Windows. Depois de configurar o **nível de preparação de Branch** configuração, você pode definir se e por quanto tempo, deseja adiar a receber atualizações do recurso após a disponibilidade da Microsoft.
    - **Nível de preparação de branch**: Defina a ramificação para a qual o dispositivo receberá atualizações do Windows (ramificação atual ou da ramificação atual para negócios).
    - **Período de adiamento (dias)**:  Especifique o número de dias para os quais as atualizações de recurso serão adiadas. Você pode adiar a receber essas atualizações de recurso por um período de 180 dias a partir de seu lançamento.
    - **Pausar atualizações de recursos iniciando**: Selecione se deve pausar dispositivos recebam atualizações de recursos por um período de até 60 dias desde o momento você pausar as atualizações. Depois que o máximo de dias passaram, funcionalidade pausar automaticamente irá expirar e o dispositivo verificará as atualizações do Windows para as atualizações aplicáveis. Após essa verificação, você pode pausar as atualizações novamente. Você pode retomar o recurso de atualizações, desmarcando a caixa de seleção.   
5. Escolha se deseja adiar ou pausar atualizações de qualidade.     
    Atualizações de qualidade são geralmente correções e aprimoramentos para a funcionalidade existente do Windows e são geralmente publicadas primeira terça-feira de cada mês, que podem ser liberadas a qualquer momento pela Microsoft. Você pode definir se e por quanto tempo, deseja adiar a receber atualizações de qualidade após sua disponibilidade.
    - **Período de adiamento (dias)**: Especifique o número de dias para os quais as atualizações de recurso serão adiadas. Você pode adiar a receber essas atualizações de recurso por um período de 180 dias a partir de seu lançamento.
    - **Pausar atualizações qualidade iniciando**: Selecione se deve pausar dispositivos de atualizações de qualidade de recebimento por um período de até 35 dias desde o momento você pausar as atualizações. Depois que o máximo de dias passaram, funcionalidade pausar automaticamente irá expirar e o dispositivo verificará as atualizações do Windows para as atualizações aplicáveis. Após essa verificação, você pode pausar as atualizações novamente. Você pode retomar qualidade atualizações desmarcando a caixa de seleção.
6. Selecione **instalar as atualizações de outros Microsoft Products** para habilitar a configuração de diretiva de grupo que verifique as configurações de adiamento aplicáveis ao Microsoft Update, bem como as atualizações do Windows.
7. Selecione **inclua drivers com o Windows Update** para atualizar automaticamente os drivers do Windows Updates. Se você desmarcar essa configuração, atualizações de driver não são baixadas do Windows Update.
8. Conclua o Assistente para criar a nova política de adiamento.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Para implantar uma atualização do Windows para a política de adiamento de negócios
1. Em **biblioteca de Software** > **serviço do Windows 10** > **Windows Update para políticas de negócios**
2. No **início** guia o **implantação** grupo, selecione **implantar o Windows Update para política de negócios**.
3. Configure as seguintes definições:
    - **Política de configuração para implantar**: Selecione a atualização do Windows para a política de negócios que você deseja implantar.
    - **Coleção**: Clique em **procurar** para selecionar a coleção onde você deseja implantar a política.
    - **Corrigir regras não compatíveis quando suportadas**: Selecione esta opção para corrigir automaticamente quaisquer regras não compatíveis para o Windows Management Instrumentation (WMI), o registro, scripts e todas as configurações para dispositivos móveis registrados pelo Configuration Manager.
    - **Permitir correção fora da janela de manutenção**: Se uma janela de manutenção tiver sido configurada para a coleção na qual você está implantando a diretiva, habilite esta opção Permitir que as configurações de conformidade corrijam o valor fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [como usar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).
    - **Gerar um alerta**: Configura um alerta que será gerado se a conformidade de linha de base de configuração for menor que uma porcentagem especificada por uma data e hora especificadas. Também pode especificar se pretende que seja enviado um alerta para o System Center Operations Manager.
    - **Atraso aleatório (horas)**: Especifica uma janela de atraso para evitar o processamento excessivo no serviço de registro de dispositivo de rede. O valor padrão é 64 horas.
    - **Agenda**: Especifique o agendamento de avaliação de conformidade pelo qual o perfil implantado é avaliado nos computadores cliente. O agendamento pode ser simples ou personalizado. O perfil é avaliado por computadores cliente quando o utilizador inicia sessão.
4.  Conclua o Assistente para implantar o perfil.



## <a name="support-for-entrust-certification-authorities"></a>Suporte para autoridades de certificação Entrust
<!-- 1350740 -->
Agora, o Configuration Manager dá suporte a autoridades de certificação Entrust; Isso permite o fornecimento de certificado PFX para dispositivos registrados no Microsoft Intune.

Você pode configurar Entrust como a autoridade de certificação quando adicionar a função do ponto de registro de certificado no Configuration Manager. Ao adicionar um novo perfil de certificado que emite os certificados PFX, você pode selecionar um Microsoft ou Entrust autoridade de certificação.

**Problema conhecido**: Na visualização técnica 1706, os certificados PFX não são emitidos para autoridades de certificação da Microsoft. Isso não afeta os certificados PFX importados ou perfis SCEP.


## <a name="cisco-ipsec-support-for-macos-vpn-profiles"></a>Suporte para perfis VPN macOS Cisco (IPsec)
<!-- 1321367 -->

Você pode criar um macOS perfil VPN com a Cisco (IPsec) como o tipo de conexão. Para obter mais informações, consulte [criar perfis de VPN](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).


## <a name="new-windows-configuration-item-settings"></a>Novas definições de item de configuração do Windows
<!-- 1354715 -->

Nesta versão, adicionamos as seguintes novas configurações que você pode usar itens de configuração do Windows:

### <a name="password"></a>Palavra-passe

- **Criptografia de dispositivo**

### <a name="device"></a>Dispositivo

- **Modificação das configurações de região (somente no desktop)**
- **Modificação das configurações de energia e modo de suspensão**
- **Modificação das configurações de idioma**
- **Modificação de tempo do sistema**
- **Modificação do nome de dispositivo**

### <a name="store"></a>Arquivo

- **Atualização automática de aplicativos da store**
- **Usar armazenamento particular**
- **Inicialização do aplicativo originado de armazenamento**

### <a name="microsoft-edge"></a>Microsoft Edge

- **Bloquear o acesso para aproximadamente: sinalizadores**
- **Substituição de prompt SmartScreen**
- **Substituição de prompt SmartScreen para arquivos**
- **Endereço IP do localhost WebRTC**
- **Mecanismo de pesquisa padrão**
- **URL de XML OpenSearch**
- **Home Pages (somente no desktop)**

Para obter mais informações sobre as configurações de conformidade, consulte [garantir a conformidade do dispositivo](/sccm/compliance/understand/ensure-device-compliance).


## <a name="new-device-compliance-policy-rules"></a>Novas regras de política de conformidade do dispositivo

* **Tipo de senha necessária**. Especifique se o usuário deve criar uma senha alfanumérica ou uma senha numérica. Para senhas alfanuméricas, você também especificar o número mínimo de conjuntos de caracteres que a senha deve ter. Os quatro conjuntos de caracteres são: Letras minúsculas, letras maiusculas, símbolos e números.

    **Suporte para:**
    * Windows Phone 8+
    * Windows 8.1 +
    * iOS 6+
<br></br>
* **Depuração de USB do bloco no dispositivo**. Você não precisa definir essas configurações, como a depuração de USB já está desabilitado no Android para dispositivos de trabalho.

    **Suporte para:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Impedir que aplicativos de fontes desconhecidas**. Exigir que dispositivos impeçam a instalação de aplicativos de fontes desconhecidas. Você não precisa definir essa configuração, como Android para dispositivos de trabalho sempre restringir a instalação de fontes desconhecidas.

    **Suporte para:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Exigir verificação de ameaças em aplicativos**. Essa configuração especifica que o recurso de aplicativos Verifique se está habilitado no dispositivo.

    **Suporte para:**
    * Android 4.2 por meio de 4.4
    * Samsung KNOX Standard 4.0+

Consulte [criar e implantar uma política de conformidade do dispositivo](https://docs.microsoft.com/sccm/mdm/deploy-use/create-compliance-policy) para experimentar as novas regras de conformidade do dispositivo.

## <a name="new-mobile-application-management-policy-settings"></a>Novas configurações de política de gerenciamento de aplicativos móveis
Começando com esta versão, você pode usar três novas configurações de política do aplicativo móvel (MAM) de gerenciamento:

- **Bloquear captura de tela (somente para dispositivos Android):** Especifica que as funcionalidades de captura de ecrã do dispositivo estão bloqueadas durante a utilização desta aplicação.

- **Desabilite sincronização do contato:** Impede que o aplicativo salvando dados para o aplicativo nativo de contatos no dispositivo.

- **Desabilite a impressão:** Impede que o aplicativo de dados de escola ou trabalho de impressão.

Consulte [proteger aplicativos usando políticas de proteção de aplicativos no Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para testar as novas configurações de política de proteção do aplicativo.

## <a name="android-and-ios-enrollment-restrictions"></a>Restrições de registro do Android e iOS
<!-- 1290826 -->
A partir desta versão, administradores agora podem especificar que os usuários não podem registrar dispositivos Android ou iOS pessoais em seu ambiente híbrido. Isso permite que você limite registrado dispositivos declaradas previamente, dispositivos da empresa ou dispositivos iOS registrados somente com o programa de registro do dispositivo.

### <a name="try-it-out"></a>Experimente
1. Na consola do Configuration Manager, na área de trabalho **Administração** , aceda a **Serviços Cloud** > **Subscrição do Microsoft Intune**.
2. No **início** guia o **assinatura** de grupo, escolha **configurar plataformas** e, em seguida, selecione **Android** ou **iOS**.
3. Selecione **bloco de dispositivos de propriedade pessoal**.

## <a name="android-for-work-application-management-policy-for-copy-paste"></a>Android para a política de gerenciamento de aplicativos de trabalho para copiar e colar
Nós atualizamos as descrições de configuração para o Android para o trabalho de itens de configuração para o **Permitir compartilhamento de dados entre trabalho e perfil pessoal**.

|Antes da 1706 Technical Preview | Novo nome de opção | Comportamento|
|-|-|-|
|Impedir que qualquer compartilhamento entre limites| Compartilhamento restrições padrão| Trabalho para pessoal: Padrão (esperado a ser bloqueada em todas as versões) <br>Pessoal para trabalho: Padrão (permitido em 6.x+, bloqueado no 5. x)|
|Sem restrições|   Aplicativos no perfil pessoal podem lidar com solicitações de perfil de trabalho de compartilhamento| Trabalho para pessoal: Permitido  <br>Pessoal para trabalho: Permitido|
|Aplicativos no perfil de trabalho podem lidar com solicitações de perfil pessoal de compartilhamento |Aplicativos no perfil de trabalho podem lidar com solicitações de perfil pessoal de compartilhamento |Trabalho para pessoal: Predefinição<br>Pessoal para trabalho: Permitido<br>(Só é útil em 5. x, onde o pessoal para o trabalho está bloqueado)|

Nenhuma dessas opções impedir o comportamento de copiar e colar diretamente. Adicionamos uma configuração personalizada para o serviço e o aplicativo de Portal da empresa 1704 que pode ser configurado para impedir a copiar e colar. Isso pode ser definido por meio do URI personalizado.

-   OMA-URI: ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
-   Tipo de valor: Booleano

Definir DisallowCrossProfileCopyPaste como true impede que o comportamento de copiar e colar entre perfis de trabalho e do Android para trabalho pessoal.

### <a name="try-it-out"></a>Experimente
1. No console do Configuration Manager, selecione **ativos e conformidade** > **visão geral** > **as configurações de conformidade** > **itens de configuração**.
2. Escolha **criar** para criar um novo item de configuração e especificar **nome** e **Android para trabalho**.
3. O dispositivo definir grupos para configurar, selecione **perfil de trabalho**e escolha **próximo**.
4. Selecione o valor para **Permitir compartilhamento de dados entre perfis pessoais e de trabalho**e, em seguida, conclua o assistente.

## <a name="device-health-attestation-assessment-for-compliance-policies-for-conditional-access"></a>Avaliação de atestado de integridade do dispositivo para políticas de conformidade para acesso condicional
<!-- 1097546 -->
Começar com esta versão, você pode usar o status de atestado de integridade do dispositivo como uma regra de política de conformidade para acesso condicional aos recursos da empresa.

### <a name="try-it-out"></a>Experimente
Selecione uma regra de atestado de integridade do dispositivo como parte de uma avaliação de política de conformidade.


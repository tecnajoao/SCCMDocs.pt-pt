---
title: Pré-visualização técnica 1706
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis na versão de pré-visualização técnica 1706 para o System Center Configuration Manager.
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2c6ceabc3a3f01ce541d4fbcdeaec5ae3db76c61
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342924"
---
# <a name="capabilities-in-technical-preview-1706-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1706 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1706. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos neste Technical Preview:**

-   **Move o ponto de distribuição** -não não possível utilizar as opções na consola para mover um ponto de distribuição entre sites com esta versão devido ao limite de pré-visualização técnica de um único site primário.

-   **As definições de compatibilidade do dispositivo** -podem ocorrer comportamento oposto ao utilizar as duas das novas definições de conformidade do dispositivo:
    - **Bloquear a depuração USB no dispositivo**
    - **Impedir as aplicações de origens desconhecidas**

        Por exemplo, se definir admins **depuração USB de bloco no dispositivo** para **verdadeiro**, todos os dispositivos que não têm a depuração de USB ativada são marcados como não conformes.

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improved-boundary-groups-for-software-update-points"></a>Grupos de limites melhorada para pontos de atualização de software
<!-- 1324591 -->
Esta versão inclui melhoramentos para como funcionam os pontos de atualização de software com grupos de limites. O seguinte resume o novo comportamento de contingência:
-   Agora, a contingência para pontos de atualização de software utiliza um período de tempo configurável para contingência aos grupos de limites de vizinho, com um tempo mínimo de 120 minutos.

-   Independentemente da configuração de contingência, um cliente tenta contactar o último ponto de atualização de software que é utilizado para 120 minutos. Após a conseguir aceder esse servidor para 120 minutos, o cliente procurará em seguida o conjunto de pontos de atualização de software disponíveis, para que possa encontrar um novo.

  -   Todos os pontos de atualização de software no grupo de limites atual do cliente são adicionados ao agrupamento do cliente imediatamente.

  -   Porque um cliente tenta utilizar o respetivo servidor original para 120 minutos antes de pesquisa um novo, não existem servidores adicionais são contactados até depois de ter decorrido duas horas.

  -   Se a contingência para um grupo de elementos vizinhos está configurada para o mínimo de 120 minutos, pontos de atualização de software desse grupo de limites de vizinho fará parte do conjunto do cliente de servidores disponíveis.

-   Depois de conseguir contactar o respetivo servidor original de duas horas, o cliente muda para um ciclo mais curto para contactar um ponto de atualização de software novo.

    Isto significa que o se um cliente não conseguir estabelecer ligação com um novo servidor, rapidamente seleciona o servidor seguinte do seu agrupamento de servidores disponíveis e tentará entrar em contacto de um.

  -   Este ciclo continua até o cliente se liga a um software que pode utilizar de ponto de atualização.
  -   Até que o cliente localiza um ponto de atualização de software, servidores adicionais são adicionados ao agrupamento de servidores disponíveis quando o tempo de contingência para cada grupo de limites de vizinho for satisfeito.

Para obter mais informações, consulte [pontos de atualização de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) o tópico de grupos de limites para o ramo atual.


## <a name="site-server-role-high-availability"></a>Disponibilidade elevada de função do servidor de site
<!-- 1128774 -->
Elevada disponibilidade para a função de servidor do site é uma solução de baseado no Gestor de configuração para instalar um servidor de site primário adicional no *passivo* modo. O servidor de site de modo passivo Ademais é ao seu servidor de site primário existente que está a ser *Active Directory* modo. Um servidor de site de modo passivo está disponível para utilização imediata, quando necessário.

Um servidor de site primário em modo passivo:
-   Utiliza a mesma base de dados do site como o servidor do site do Active Directory.
-   Recebe uma cópia do site do Active Directory servidores biblioteca de conteúdos, que, em seguida, é guardada sincronizada.
-   Não escrever dados na base de dados do site, desde que está no modo passivo.
-   Não suporta a instalação ou remoção das funções do sistema de sites opcionais, desde que está no modo passivo.

Para tornar o servidor de site do Active Directory de modo de servidor do site de modo passivo, manualmente promovê-lo. Isto muda o servidor do site do Active Directory para o servidor de site passiva. As funções de sistema de sites que estão disponíveis no servidor original do Active Directory de modo permanecem disponíveis desde que o computador está acessível. Apenas a função de servidor do site é mudada entre o modo de ativo e passivo.

Para instalar um servidor de site de modo passivo, utilize o **criar Assistente de servidor de sistema de Site** para configurar um novo servidor de site com um tipo de **servidor do site primário** e um modo de **passivo**. O assistente, em seguida, executa a configuração do Configuration Manager no servidor especificado para instalar o novo servidor de site no modo passivo. Após a instalação estiver concluída, o servidor de site do Active Directory de modo mantém o servidor do site de modo passivo e respetiva biblioteca de conteúdos sincronizadas com as alterações ou as configurações que efetuar ao servidor do site ativa.

### <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações
-   Um único servidor de sites no modo passivo é suportado em cada site primário.

-   O servidor do site no modo passivo pode estar no local ou baseado na nuvem no Azure.

-   O modo de Active Directory e a servidores de sites de modo passivo devem estar no mesmo domínio.

-   O modo de Active Directory e a servidores de sites de modo passivo tem de utilizar a mesma base de dados, que tem de ser remota dos computadores de cada servidor de site.

    -   O SQL Server que aloja a base de dados pode utilizar uma instância predefinida, com o nome de instância, o cluster do SQL Server ou o sempre no grupo de disponibilidade.

    -   O servidor do site no modo passivo está configurado para utilizar a mesma base de dados do site do servidor do site de modo de Active Directory. No entanto, o servidor do site de modo passivo não utiliza a base de dados até depois-é promovido para o modo de Active Directory.

-   O computador que irá executar o servidor do site de modo passivo:

    -   Tem de cumprir os [pré-requisitos para instalar um site primário](https://docs.microsoft.com/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).

    -   Instala ficheiros de origem que corresponde à versão do servidor do site de Active Directory de modo a utilizar.

    -   Não pode ter uma função de sistema de sites a partir de qualquer site antes de instalar o site de modo passivo.

-   Os computadores de servidor de sites de modo passivo e Active Directory podem executar sistemas operativos diferentes ou versões de service pack, desde que ambas as permanecem suportadas pela versão do Configuration Manager.

-   O servidor do site de modo passivo para o servidor do Active Directory de modo a promoção é manual. Não há nenhum ativação pós-falha automática.

-   Funções do sistema de sites podem ser instaladas apenas no servidor do site que está no modo de Active Directory.

    -   Um servidor de site no modo de Active Directory suporta todas as funções de sistema de sites. Não é possível instalar funções do sistema de sites no servidor quando estiver no modo passivo.

    -   Funções de sistema de sites que utilizam uma base de dados (por exemplo, o ponto de Reporting Services) tem de ter a base de dados num servidor remoto do tanto o modo Active Directory e servidores de sites de modo passivo.

    -   O SMS_Provider não instalar no servidor do site no modo passivo. Uma vez que tem de ligar a um SMS_Provider para o site para promover manualmente o servidor do site de modo passivo para o modo de Active Directory, recomendamos [instalar pelo menos uma instância adicional do fornecedor de](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider) num computador adicional.

**Problema de conhecido**:   
Com esta versão, **estado** para as seguintes condições são apresentados na consola do como valores de numérico em vez de texto legível:
-   131071 – falha na instalação do servidor de site
-   720895 – falha na desinstalação de função de servidor site
-   851967 – falha na ativação pós-falha

### <a name="add-a-site-server-in-passive-mode"></a>Adicionar um servidor de site no modo passivo
1.  Na consola, aceda a **administração** > **configuração do Site** > **Sites** e iniciar o [Adicionar Assistente de funções de sistema de Site](/sccm/core/servers/deploy/configure/install-site-system-roles). Também pode utilizar o **criar Assistente de servidor de sistema de Site**.

2.  No **geral** página, especifique o servidor que irá alojar o servidor de site de modo passivo. O servidor que especificar não é possível alojar quaisquer funções de sistema de sites antes de instalar um servidor de site no modo passivo.

3.  No **seleção da função do sistema** página, selecione apenas **servidor do site primário em modo passivo**.

4.  Para concluir o assistente, tem de fornecer as seguintes informações que são utilizadas para executar a configuração e instalar a função de servidor do site no servidor especificado:
    -   Optar por copiar os ficheiros de instalação do servidor do site do Active Directory para o novo servidor de site de modo passivo, ou especifique um caminho para uma localização que contém o conteúdo do servidor do site do Active Directory **CD. Mais recente** pasta.

    -   Especifique o mesmo servidor de base de dados do site e o nome de base de dados como utilizadas pelo servidor de site do Active Directory de modo.

5.  Em seguida, o Configuration Manager instala o servidor do site no modo passivo no servidor especificado.

Para o estado de instalação de detalhado, aceda a **administração** > **configuração do Site** > **Sites**.
-   Apresenta o estado para o servidor de site em modo passivo como **instalar**.

-   Selecione o servidor e, em seguida, clique em **Mostrar estado** para abrir **estado de instalação do servidor de Site** para informações mais detalhadas.



### <a name="promote-the-passive-mode-site-server-to-active-mode"></a>Promover o servidor de site de modo passivo para o modo de Active Directory
Quando pretender alterar o servidor de site de modo passivo para o modo de Active Directory, fazê-lo do **nós** painel **administração** > **configuração do Site** > **Sites**. Desde que pode aceder a uma instância do SMS_Provider, pode aceder ao site para fazer esta alteração.
1.  No **nós** painel da consola do Configuration Manager, selecione o servidor do site no modo passivo e, em seguida, a partir do Friso, escolha **promover para ativo**.

2.  O simples **estado** para o servidor que está a promover apresenta na **nós** painel como **promoção**.

3.  Depois de concluída, a promoção de **estado** coluna mostra **OK** para ambas as novas *Active Directory* servidor do site de modo e para o novo *passivo* servidor do site de modo.

4.  No **administração** > **configuração do Site** > **Sites**, o nome do servidor do site primário agora apresenta o nome do novo *Active Directory* servidor do site de modo.
Para o estado detalhado, aceda a **monitorização** > **estado do servidor de Site**.
    -   O **modo** coluna identifica que servidor *Active Directory* ou *passivo*.

    -   Ao promover um servidor de modo passivo para o modo de Active Directory, selecione o servidor de site que está a promover ao Active Directory e, em seguida, escolha **Mostrar estado** a partir do Friso. Esta ação abre o **estado de promoção de servidor do Site** janela que apresenta detalhes adicionais sobre o processo.

Quando um servidor de site no modo de Active Directory passa para o modo passivo, apenas a função de sistema de sites é efetuada passiva. Todas as outras funções do sistema de sites que estão instaladas nesse computador permanecem acessíveis para os clientes e Active Directory.


### <a name="daily-monitoring"></a>Diariamente monitorização
Quando tiver um site primário em modo passivo, monitorize-diárias para garantir que continua a ser sincronizado com o servidor de site do Active Directory de modo e pronto a utilizar. Para fazê-lo, aceda a **monitorização** > **estado do servidor de Site**. Aqui pode ver o modo de Active Directory e a servidores de sites de modo passivo.

O **resumo** separador:
-   O **modo** coluna identifica o servidor está ativo ou passivo.
-   O **estado** listas de coluna **OK** quando o servidor de modo passivo estiver sincronizado com o servidor de modo de Active Directory.
-   Para ver detalhes adicionais sobre o estado da sincronização de conteúdo, clique em **Mostrar estado** do Estado de sincronização de conteúdo. Esta ação abre o separador de biblioteca de conteúdos onde pode tentar para corrigir problemas de sincronização de conteúdo.

O **biblioteca de conteúdos** separador:
-   Ver o **estado** para conteúdo que sincroniza a partir do servidor de site do Active Directory para o servidor de site de modo passivo.
-   Pode selecionar o conteúdo com um Estado de **falha**e, em seguida, escolha **sincronizar os itens selecionados** a partir do Friso. Esta ação tenta ressincronizar esse conteúdo a partir da origem de conteúdo para o servidor de site de modo passivo. Durante a recuperação, o estado apresentado como **em curso**, e quando é sincronizado, é apresentado como **êxito**.

### <a name="try-it-out"></a>Experimente!
Experimente concluir as seguintes tarefas e, em seguida, envie-nos **comentários** do **home page** separador do friso para nos informar como correu:
-   Pode instalar um site primário em modo passivo.
-   Posso pode utilizar a consola para promover o servidor de site de modo passivo para tornar o servidor de site do Active Directory de modo e confirmar a alteração do Estado de ambos os servidores de site.


## <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Incluir confiança para pastas e ficheiros específicos numa política de proteção de dispositivos
<!-- 1324676 -->
Nesta versão, adicionámos mais capacidades para [Device Guard](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) gestão de políticas

Opcionalmente, agora pode adicionar o confiança para ficheiros específicos para pastas numa política Device Guard. Isto permite-lhe:

1.  Ultrapassar problemas com os comportamentos de instalador gerido
2.  Aplicações de linha de negócio de confiança que não não possível implementar com o Configuration Manager
3.  As aplicações que estão incluídas numa imagem de implementação do sistema operativo de confiança.

### <a name="try-it-out"></a>Experimente!

1.  Enquanto estiver a criar uma política de Device Guard, no separador as inclusões Device Guard criar Assistente de política, clique em **adicionar**.
2.  No **adicionar confiança de ficheiro ou pasta** diálogo caixa, especifique informações sobre o ficheiro ou pasta que pretende confiança. Pode especificar um caminho de ficheiro ou pasta local ou ligar a um dispositivo remoto para o qual tem permissão para ligar e especifique um caminho de ficheiro ou pasta em que o dispositivo.
3.  Conclua o assistente.


## <a name="hide-task-sequence-progress"></a>Ocultar o progresso da sequência de tarefas
<!-- 1354291 -->
Nesta versão, pode controlar quando o progresso da sequência de tarefas é apresentado aos utilizadores finais através da utilização de uma nova variável. Na sua sequência de tarefas, utilize o **definir variável da sequência de tarefas** passo para definir o valor para o **TSDisableProgressUI** variável para ocultar ou mostrar progresso da sequência de tarefas. Pode utilizar o passo Definir variável da sequência de tarefas múltiplas vezes numa sequência de tarefas para alterar o valor da variável. Isto permite-lhe ocultar ou mostrar progresso da sequência de tarefas nas secções diferentes da sequência de tarefas.

#### <a name="to-hide-task-sequence-progress"></a>Para ocultar o progresso da sequência de tarefas
No editor de sequência de tarefas, utilize o [definir variável da sequência de tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) passo para definir o valor da **TSDisableProgressUI** variável à **verdadeiro** para ocultar o progresso da sequência de tarefas.

#### <a name="to-display-task-sequence-progress"></a>Para apresentar o progresso da sequência de tarefas
No editor de sequência de tarefas, utilize o [definir variável da sequência de tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) passo para definir o valor da **TSDisableProgressUI** variável à **falso** para apresentar o progresso da sequência de tarefas.

## <a name="specify-a-different-content-location-for-install-content-and-uninstall-content"></a>Especificar uma localização de conteúdo diferente para o conteúdo de instalação e desinstalação de conteúdo
<!-- 1097546 -->
No Configuration Manager hoje em dia, especificar a localização de instalação que contém os ficheiros de configuração para uma aplicação. Quando especificar uma localização de instalação, este também é utilizado como a localização de desinstalação para o conteúdo da aplicação.
Com base nos seus comentários, quando pretender desinstalar uma aplicação implementada, e o conteúdo da aplicação não se encontra no computador cliente, em seguida, o cliente irá transferir todos os ficheiros de configuração de aplicação novamente antes da aplicação é desinstalada.
Para resolver este problema, pode agora especificar ambos os uma instalação de conteúdo de localização e opcional desinstalar a localização de conteúdo. Além disso, pode optar por não especificar uma localização de conteúdo de desinstalação.

### <a name="try-it-out"></a>Experimente!

1. Nas propriedades do tipo de implementação de uma aplicação, clique em de **conteúdo** separador.
2. Configurar o **localização de conteúdo de instalação** como normal.
3. Para **desinstalar definições de conteúdo**, escolha um dos seguintes:
    - **Igual à instalar conteúdo** -será utilizada a mesma localização de conteúdo, independentemente se estiver a instalar ou desinstalar a aplicação.
    - **Nenhum conteúdo de desinstalação** -Escolha esta opção se não quiser fornecer uma localização de conteúdo de desinstalação da aplicação.
    - **Diferente do conteúdo de instalação** -Escolha esta opção se pretender especificar uma localização de conteúdo de desinstalação é diferente da localização de conteúdo de instalação.
5. Se tiver selecionado **Different do conteúdo de instalação**, navegue para ou introduza a localização do conteúdo de aplicação que será utilizado para desinstalar a aplicação.
6. Clique em **OK** para fechar a caixa de diálogo de propriedades de tipo de implementação.


## <a name="accessibility-improvements"></a>Melhoramentos de acessibilidade  
<!--1253000 -->
Esta pré-visualização disponibiliza vários melhoramentos para o [funcionalidades de acessibilidade](/sccm/core/understand/accessibility-features) na consola do Configuration Manager. Estas atualizações incluem:     

**Novos atalhos de teclado para mover-se a consola:**
-   CTRL + M - conjuntos focar-se no painel principal (central).
-   CTRL + T - o foco de conjuntos para o nó superior do painel de navegação. Se o foco já foi nesse painel, o foco está definido para o último nó que é visitada.
-   CTRL + I - foco define a barra de trilho, abaixo do Friso.
-   CTRL + L - foco de conjuntos para o **pesquisa** campo, quando disponível.
-   CTRL + D - foco de conjuntos para o painel de detalhes, quando disponível.
-   ALT – foco de alterações que entra e sai do Friso.

**Melhoramentos gerais:**
-   Melhorado navegação no painel de navegação quando escreva as letras de um nome de nó.
-   Navegação do teclado através da vista principal e o Friso estão agora circular.
-   Agora é circular navegação do teclado no painel de detalhes. Para voltar para o objeto anterior ou painel, utilize Ctrl + D, em seguida, Shift + SEPARADOR.
-   Depois de atualizar uma vista da área de trabalho, o foco está definido para o painel principal da área de trabalho.
-   Foi corrigido um problema ao ativar leitores de ecrã anunciar os nomes dos itens de lista.
-   Foram adicionados nomes acessíveis para vários controlos na página que permite aos leitores de ecrã anunciar informações importantes.


## <a name="changes-to-the-azure-services-wizard-to-support-upgrade-readiness"></a>Alterações ao Assistente de serviços do Azure para suportar a preparação de atualização
<!-- 1353331 -->
A partir desta versão, utilize o Assistente de serviços do Azure para configurar uma ligação do Configuration Manager para [atualizar preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics). A utilização do assistente simplifica a configuração do conector utilizando um assistente comuns para serviços do Azure relacionados.   

Embora o método para configurar a ligação foi alterada, pré-requisitos para a ligação e como utilizar atualizar preparação permanecem inalterados.   

### <a name="prerequisites-for-upgrade-readiness"></a>Pré-requisitos para a preparação da atualização
Os pré-requisitos para um [ligação para atualizar preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics#create-a-connection-to-upgrade-readiness) são iguais às detalhadas para a atual filial do Configuration Manager. São repetidos aqui para sua comodidade:  

**Pré-requisitos**
-   Para poder adicionar a ligação, o ambiente do Configuration Manager primeiro tem de configurar um [ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) num [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation). Quando adicionar a ligação ao seu ambiente, este irá também instalar o Microsoft Monitoring Agent no computador que executa esta função de sistema de sites.
-   Registe o Configuration Manager como uma ferramenta de gestão "Aplicação Web e/ou API Web" e obter o [ID de cliente deste registo](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
-   Crie uma chave de cliente para a ferramenta de gestão registado no Azure Active Directory.
-   No Portal de gestão do Azure, forneça a aplicação web registado com permissão para aceder à OMS, conforme descrito em [fornecer do Configuration Manager com permissões para OMS](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

> [!IMPORTANT]       
> Quando configurar permissões para aceder à OMS, lembre-se de que escolha o **contribuinte** função e atribua-lhe as permissões para o grupo de recursos da aplicação registada.

Depois dos pré-requisitos estiverem configurados, está pronto para utilizar o Assistente para criar a ligação.

### <a name="use-the-azure-services-wizard-to-configure-upgrade-readiness"></a>Utilize o Assistente de serviços do Azure para configurar a preparação de atualização
1.  Na consola, aceda a **administração** > **descrição geral** > **serviços em nuvem** > **serviços do Azure**e, em seguida, escolha **configurar os serviços do Azure** do **home page** separador do Friso, para iniciar o **Assistente de serviços do Azure**.

2.  No **serviços do Azure** página, selecione o **conector de preparação de atualização**e, em seguida, clique em **seguinte**.

3.  No **aplicação** página, especifique o **ambiente do Azure** (technical preview suporta apenas na nuvem pública). Em seguida, clique em **importação** para abrir o **importar aplicações** janela.

4.  No **importar aplicações** janela, especifique os detalhes para uma aplicação web que já existe no seu Azure AD.
    -   Forneça um nome amigável para o nome de inquilino do Azure AD. Em seguida, especifique o ID do inquilino, o nome da aplicação, ID de cliente, chave secreta para a aplicação web do Azure e o URI de ID de aplicação.
    -   Clique em **verifique**e se tiver êxito, clique em **OK** para continuar.

5.   No **configuração** página, especifique a subscrição, o grupo de recursos e a área de análise do Windows que pretende utilizar com esta ligação para atualizar preparação.  

6.  Clique em **seguinte** para ir para o **resumo** página e, em seguida, conclua o Assistente para criar a ligação.


## <a name="new-client-settings-for-cloud-services"></a>Novas definições de cliente para serviços em nuvem
<!-- 1319883 -->

Nesta versão, adicionámos duas novas definições de cliente do Configuration Manager. Encontrará estes no **serviços em nuvem** secção.  Estas definições proporcionam-lhe as seguintes capacidades:

- Controlo que os clientes do Configuration Manager podem aceder a um gateway de gestão de nuvem configurado.
- Os clientes do Configuration Manager associado a um domínio Windows 10 ser registado automaticamente no Azure Active Directory.

Estas novas definições de ajudam a realizar as funcionalidades descritas o [1705 do Configuration Manager Technical Preview](/sccm/core/get-started/capabilities-in-technical-preview-1705#new-capabilities-for-azure-ad-and-cloud-management).

### <a name="before-you-start"></a>Antes de começar

Tem de ter instalado e configurado o Azure AD Connect entre o Active Directory no local e de inquilino do Azure AD.

Se remover a ligação, os dispositivos não são não registados, mas não novos dispositivos irão registar.

### <a name="try-it-out"></a>Experimente!

1. Configurar a secção de definições (que se encontra nos serviços de nuvem) do cliente utilizando as informações [como configurar as definições de cliente](/sccm/core/clients/deploy/configure-client-settings).
    -   **Registar automaticamente novos dispositivos do Windows 10 associados a um domínio com o Azure Active Directory** – definido como **Sim** (predefinição), ou **não**.
    -   **Permitir que os clientes utilizar um gateway de gestão de nuvem** – definido como **Sim** (predefinição), ou **não**.
2.  Implemente as definições de cliente na coleção de dispositivos necessária.

Para confirmar que o dispositivo é associado para o Azure AD, execute o comando **dsregcmd.exe /status** numa janela de linha de comandos. O **AzureAdjoined** campo nos resultados da mostrará **Sim** se o dispositivo estiver do Azure AD associado.

## <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Criar e executar scripts do PowerShell a partir da consola do Configuration Manager
<!-- 1236459 -->

No Configuration Manager, pode implementar scripts de utilização de pacotes e programas em dispositivos cliente. Esta pré-visualização técnica, adicionámos novas funcionalidades que lhe permite efetuar as seguintes ações:

- Importar Scripts do PowerShell para o Configuration Manager
- Editar os scripts a partir da consola do Configuration Manager (para apenas scripts não assinados)
- Scripts de marca como aprovado ou negado, para melhorar a segurança
- Executar scripts em coleções de computadores de cliente do Windows e no local geridos Windows PCs. Não implementa scripts, em vez disso, são sejam executados em tempo real nos dispositivos cliente.
- Examine os resultados devolvidos pelo script na consola do Configuration Manager.


### <a name="prerequisites"></a>Pré-requisitos

Para utilizar scripts, tem de ser um membro da função de segurança adequado do Configuration Manager.

- **Para importar e criar scripts** -a conta tem de ter **criar** permissões para **SMS Scripts** no **administrador total** função de segurança.
- **Para aprovar ou negar scripts** -a conta tem de ter **aprovar** permissões para **SMS Scripts** no **administrador total** função de segurança.
- **Para executar scripts** -a conta tem de ter **executar Script** permissões para **coleções** no **Gestor de definições de compatibilidade** função de segurança.

Para mais informações sobre funções de segurança do Configuration Manager, consulte [Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).

Por predefinição, os utilizadores não podem aprovar um script que tenham criado. Uma vez que os scripts são poderosa, versátil e podem ser implementados em vários dispositivos, tiver introduzimos um novo conceito de fornecer a capacidade de separar as funções entre a pessoa que autores o script e de que a pessoa que aprove o script. Isto proporciona o nível adicional de segurança contra a execução de um script sem supervisão. Pode desativar esta aprovação secundária, para facilitar a testar, particularmente durante a versão de pré-visualização técnica.

Para permitir aos utilizadores aprovar os seus próprios scripts:

1. Na consola do Configuration Manager, clique em **Administração**.
2. Na área de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.
3. Na lista de sites, selecione o site e, em seguida, no **home page** separador o **Sites** , clique em **definições de hierarquia**.
4. No **geral** separador do **propriedades de definições de hierarquia** diálogo caixa, desmarque a caixa de verificação **não permitir autores de script aprovar os seus próprios scripts**.


### <a name="try-it-out"></a>Experimente!

#### <a name="import-and-edit-a-script"></a>Importar e editar um script

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. No **biblioteca de Software** área de trabalho, clique em **Scripts**.
3. No **home page** separador o **criar** , clique em **criar Script**.
4. No **Script** página do **criar Script** assistente, configure o seguinte:
    - **Nome do script** -introduza um nome para o script. Embora possa criar vários scripts com o mesmo nome, Isto fará mais difícil localizar o script que terá na consola do Configuration Manager.
    - **Idioma de script** - atualmente, apenas **PowerShell** scripts são suportados.
    - **Importar** -importar um script do PowerShell para a consola. O script é apresentado no **Script** campo.
    - **Limpar** -remove o script atual do **Script** campo.
    - **Script** -apresenta o script atualmente importado. Pode editar o script neste campo, conforme necessário.
5. Conclua o assistente. O novo script é apresentado no **Script** lista com um Estado de **aguardar aprovação**. Antes de poder executar este script nos dispositivos cliente, terá de o aprovar.


#### <a name="approve-or-deny-a-script"></a>Aprovar ou recusar um script



Antes de poder executar um script, deve ser aprovado. Para aprovar um script:

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. No **biblioteca de Software** área de trabalho, clique em **Scripts**.
3. No **Script** lista, selecione o script que pretende aprovar ou recusar e, em seguida, no **home page** separador o **Script** , clique em **aprovar/negação**.
4. No **aprovar ou negar o script** caixa de diálogo, **aprovar**, ou **negar** o script e, opcionalmente, introduza um comentário sobre a sua decisão. Se negar um script, não pode ser executado nos dispositivos cliente.
5. Conclua o assistente. No **Script** lista, verá o **estado de aprovação** alteração de coluna consoante a ação que demorou.

#### <a name="run-a-script"></a>Executar um script

Quando um script for aprovado, podem ser executada em relação a uma coleção que escolher.

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2. Na área de trabalho **Ativos e Compatibilidade** , clique em **Coleções de Dispositivos**.
3. No **coleções de dispositivos** lista, clique na coleção de dispositivos nos quais pretende executar o script.
3. No **home page** separador o **todos os sistemas** , clique em **executar Script**.
4. No **Script** página do **executar Script** assistente, escolha um script da lista. Apenas aprovados scripts são apresentados. Clique em **seguinte**e, em seguida, conclua o assistente.

#### <a name="monitor-a-script"></a>Monitorizar um script

Depois de executar um script em dispositivos cliente, utilize este procedimento para monitorizar o êxito da operação.

1. Na consola do Configuration Manager, clique em **monitorização**.
2. No **monitorização** área de trabalho, clique em **resultados de Script**.
3. No **resultados de Script** lista, poderá ver os resultados para cada script executado nos dispositivos cliente. Um código de saída do script de **0**, geralmente, indica que o script é executado com êxito.

## <a name="pxe-network-boot-support-for-ipv6"></a>Suporte de arranque de rede do PXE para IPv6
<!-- 1269793 -->
Agora, pode ativar o suporte de arranque de rede do PXE para IPv6 iniciar uma implementação de sistema operativo de sequência de tarefas. Quando utiliza esta definição, os pontos de distribuição com PXE ativado irão suportar IPv4 e IPv6. Esta opção não necessita de WDS e deixarão o WDS se estiver presente.

#### <a name="to-enable-pxe-boot-support-for-ipv6"></a>Para ativar o suporte de arranque PXE para IPv6
Utilize o procedimento seguinte para ativar a opção de suporte de IPv6 para PXE.

1. Na consola do Configuration Manager, vá para **administração** > **descrição geral** > **pontos de distribuição**e clique em **propriedades** para pontos de distribuição com PXE ativado.
2. No **PXE** separador, selecione **suportar IPv6** para ativar o suporte de IPv6 para PXE.

## <a name="manage-microsoft-surface-driver-updates"></a>Gerir atualizações de controladores Microsoft Surface
<!-- 1098490 -->
Agora, pode utilizar o Configuration Manager para gerir atualizações de controladores Microsoft Surface.

### <a name="prerequisites"></a>Pré-requisitos
Todos os pontos de atualização de software devem executar o Windows Server 2016.

### <a name="try-it-out"></a>Experimente!
Experimente concluir as seguintes tarefas e, em seguida, envie-nos **comentários** do **home page** separador do friso para nos informar como correu:
1. Ative a sincronização para o Microsoft Surface. Utilize o procedimento no [configurar classificação e produtos](/sccm/sum/get-started/configure-classifications-and-products) e selecione **incluem o Microsoft Surface controladores e as atualizações de firmware** no **classificações** separador para ativar a superfície controladores.
2. [Sincronizar os controladores Microsoft Surface](/sccm/sum/get-started/synchronize-software-updates.md).
3. [Implementar controladores de Microsoft Surface sincronizadas](/sccm/sum/deploy-use/deploy-software-updates)

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configurar o Windows Update para as políticas de diferimento por de negócio
<!-- 1290890 -->
Agora, pode configurar políticas de diferimento por para atualizações de funcionalidade do Windows 10 ou qualidade atualizações para o Windows 10 dispositivos geridos diretamente pelo Windows Update for Business. Pode gerir as políticas de diferimento por na nova **Windows Update para as políticas de negócio** nó **biblioteca de Software** > **manutenção do Windows 10**.

### <a name="prerequisites"></a>Pré-requisitos
Dispositivos Windows 10 geridos pelo Windows Update para empresas tem de ter conectividade à Internet.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Para criar uma atualização do Windows para a política de diferimento por de negócio
1. No **biblioteca de Software** > **manutenção do Windows 10** > **Windows Update para as políticas de negócio**
2. No **home page** separador o **criar** grupo, selecione **criar Windows Update para empresas política** para abrir o Windows Update criar para o Assistente de política de negócio.
3. No **geral** , indique um nome e descrição para a política.
4. No **diferimento por políticas** página, configure se pretende diferir ou colocar em pausa as atualizações de funcionalidade.    
    Atualizações de funcionalidade são geralmente novas funcionalidades do Windows. Depois de configurar o **sucursal nível de preparação** , em seguida, pode definir se e para o período de tempo, gostaria diferir atualizações de funcionalidades a seguir a respetiva disponibilidade da Microsoft a receber.
    - **Nível de preparação de sucursal**: Defina o ramo para o qual o dispositivo irá receber atualizações do Windows (Current Branch ou Current Branch for Business).
    - **Período de diferimento por (dias)**:  Especifique o número de dias para o qual vai ser diferidas atualizações de funcionalidade. Pode diferir receber estas atualizações de funcionalidade durante um período de 180 dias a partir da respetiva versão.
    - **Iniciar de atualizações de funcionalidades de pausa**: Selecione se para colocar em pausa dispositivos de receber atualizações de funcionalidade durante um período de 60 dias desde o momento em coloque em pausa as atualizações. Após ter passado o máximo de dias, a funcionalidade de pausa automaticamente irá expirar e o dispositivo irá analisar as atualizações do Windows para detetar atualizações aplicáveis. Seguir esta análise, pode colocar em pausa as atualizações de novo. Pode unpause atualizações de funcionalidade desmarcando a caixa de verificação.   
5. Escolha se pretende diferir ou atualizações de qualidade de colocar em pausa.     
    Atualizações de qualidade são, geralmente, correções e melhoramentos a funcionalidades existentes do Windows e, normalmente, são publicadas primeira Terça-feira de cada mês, que podem ser libertadas em qualquer altura ao Microsoft. Pode definir se e para o período de tempo, gostaria diferir atualizações de qualidade após a respetiva disponibilidade a receber.
    - **Período de diferimento por (dias)**: Especifique o número de dias para o qual vai ser diferidas atualizações de funcionalidade. Pode diferir receber estas atualizações de funcionalidade durante um período de 180 dias a partir da respetiva versão.
    - **Iniciar de atualizações de qualidade de pausa**: Selecione se para colocar em pausa dispositivos a partir da qualidade a receber atualizações durante um período de 35 dias desde o momento em coloque em pausa as atualizações. Após ter passado o máximo de dias, a funcionalidade de pausa automaticamente irá expirar e o dispositivo irá analisar as atualizações do Windows para detetar atualizações aplicáveis. Seguir esta análise, pode colocar em pausa as atualizações de novo. Pode unpause qualidade atualizações ao desmarcar a caixa de verificação.
6. Selecione **instalar atualizações a partir de outros Microsoft Products** para ativar a definição de política de grupo que as definições de diferimento por aplicável ao Microsoft Update, bem como as atualizações do Windows.
7. Selecione **incluir controladores com o Windows Update** para atualizar automaticamente os controladores de atualizações do Windows. Se desmarcar esta definição, as atualizações de controladores não são transferidas atualizações do Windows.
8. Conclua o Assistente para criar a nova política de diferimento por.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Implementar uma atualização do Windows para a política de diferimento por de negócio
1. No **biblioteca de Software** > **manutenção do Windows 10** > **Windows Update para as políticas de negócio**
2. No **home page** separador o **implementação** grupo, selecione **implementar o Windows Update para empresas política**.
3. Configure as seguintes definições:
    - **Política de configuração para implementar**: Selecione a atualização do Windows para a política de negócio que gostaria de implementar.
    - **Coleção**: Clique em **procurar** para selecionar a coleção onde pretende implementar a política.
    - **Remediar regras incompatíveis quando suportado**: Selecione esta opção para retificar automaticamente quaisquer regras não compatíveis para o Windows Management Instrumentation (WMI), o registo, scripts e todas as definições para dispositivos móveis que são inscritos pelo Configuration Manager.
    - **Permitir remediação fora da janela de manutenção**: Se uma janela de manutenção tiver sido configurada para a coleção à qual está a implementar a política, ative esta opção para que as definições de conformidade retifiquem o valor fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [como utilizar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).
    - **Gerar um alerta**: Configura um alerta que é gerado se a compatibilidade da linha de base de configuração for inferior a uma percentagem especificada por uma data e hora especificadas. Também pode especificar se pretende que seja enviado um alerta para o System Center Operations Manager.
    - **Atraso aleatório (horas)**: Especifica uma janela de atraso para evitar processamento excessivo no serviço de inscrição de dispositivos de rede. O valor predefinido é 64 horas.
    - **Agenda**: Especifique o agendamento de avaliação de compatibilidade através do qual o perfil implementado é avaliado nos computadores cliente. O agendamento pode ser simples ou personalizado. O perfil é avaliado por computadores cliente quando o utilizador inicia sessão.
4.  Conclua o Assistente para implementar o perfil.



## <a name="support-for-entrust-certification-authorities"></a>Suporte para Entrust autoridades de certificação
<!-- 1350740 -->
O Configuration Manager suporta agora autoridades de certificação Entrust; Isto permite que a entrega de certificado PFX para dispositivos inscritos no Microsoft Intune.

Pode configurar Entrust como a autoridade de certificação quando adicionar uma função de ponto de registo de certificados no Configuration Manager. Ao adicionar um novo perfil de certificado que emite certificados PFX, pode selecionar um Microsoft ou Entrust autoridade de certificação.

**Problema de conhecido**: No 1706 technical preview, os certificados PFX não são emitidos para autoridades de certificação da Microsoft. Isto não afeta os certificados PFX importados ou perfis SCEP.


## <a name="cisco-ipsec-support-for-ios-vpn-profiles"></a>Suporte de Cisco (IPsec) para perfis VPN do iOS
<!-- 1321367 -->

Pode criar um iOS perfil da VPN com o Cisco (IPsec) como o tipo de ligação. Para obter mais informações, consulte [criar perfis VPN](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).


## <a name="new-windows-configuration-item-settings"></a>Novas definições de item de configuração do Windows
<!-- 1354715 -->

Nesta versão, adicionámos as seguintes definições novas, que pode utilizar itens de configuração do Windows:

### <a name="password"></a>Palavra-passe

- **Encriptação de dispositivos**

### <a name="device"></a>Dispositivo

- **Modificação de definições de região (apenas ambiente de trabalho)**
- **Modificação de definições de energia e o modo de suspensão**
- **Modificação das definições de idioma**
- **Modificação de hora do sistema**
- **Modificação de nome de dispositivo**

### <a name="store"></a>Arquivo

- **As aplicações da loja de atualização automática**
- **Utilizar apenas o arquivo privado**
- **Armazenar iniciação da aplicação teve origem**

### <a name="microsoft-edge"></a>Microsoft Edge

- **Bloquear o acesso ao sobre: sinalizadores**
- **Substituição de linha de comandos do SmartScreen**
- **Substituição de linha de comandos SmartScreen de ficheiros**
- **Endereço IP localhost WebRTC**
- **Motor de busca predefinido**
- **URL de OpenSearch XML**
- **Homepages (apenas ambiente de trabalho)**

Para mais informações sobre as definições de compatibilidade, consulte [garantir a conformidade de dispositivo](/sccm/compliance/understand/ensure-device-compliance).


## <a name="new-device-compliance-policy-rules"></a>Novas regras de política de conformidade de dispositivo

* **Tipo de palavra-passe obrigatório**. Especifique se o utilizador tem de criar uma palavra-passe alfanumérica ou uma palavra-passe numérico. Palavras-passe alfanuméricos, também especificar o número mínimo de conjuntos de carateres que a palavra-passe tem de ter. Os quatro conjuntos de carateres são: Letras minúsculas, maiúsculas, símbolos e números.

    **Suportado no:**
    * Windows Phone 8+
    * Windows 8.1 +
    * iOS 6+
<br></br>
* **Depuração USB de bloco no dispositivo**. Não é necessário configurar esta definições como a depuração USB já está desativada no Android para dispositivos de trabalho.

    **Suportado no:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Impedir que as aplicações a partir de origens desconhecidas**. Exigir que os dispositivos impeçam a instalação de aplicações a partir de origens desconhecidas. Não é necessário configurar esta definição, tal como Android, para dispositivos de trabalho sempre restringir a instalação a partir de origens desconhecidas.

    **Suportado no:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Necessária análise de ameaças nas aplicações**. Esta definição especifica que a funcionalidade de aplicações de Verifique está ativada no dispositivo.

    **Suportado no:**
    * Android 4.2 através de 4.4
    * Samsung KNOX Standard 4.0+

Consulte [criar e implementar uma política de conformidade do dispositivo](https://docs.microsoft.com/sccm/mdm/deploy-use/create-compliance-policy) para experimentar as novas regras de conformidade do dispositivo.

## <a name="new-mobile-application-management-policy-settings"></a>Novas definições de política de gestão de aplicações móveis
A partir desta versão, pode utilizar três novas aplicações móveis (MAM) definições de política:

- **Bloquear captura de ecrã (apenas dispositivos Android):** Especifica que as funcionalidades de captura de ecrã do dispositivo estão bloqueadas durante a utilização desta aplicação.

- **Desative a sincronização de contactos:** Impede a aplicação de guardar os dados para a aplicação de contactos nativa no dispositivo.

- **Desative a impressão:** Impede que a aplicação de trabalho de impressão ou dados escola.

Consulte [proteger aplicações ao utilizar políticas de proteção de aplicações no Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para experimentar as novas definições de política de proteção de aplicação.

## <a name="android-and-ios-enrollment-restrictions"></a>Restrições de inscrição do Android e iOS
<!-- 1290826 -->
A partir desta versão, admins pode agora especificar que os utilizadores não é possível inscrever dispositivos Android ou iOS pessoais no respetivo ambiente híbrido. Isto permite-lhe limite inscritos dispositivos predeclared, dispositivos pertencentes à empresa ou os dispositivos iOS inscritos com o programa de inscrição de dispositivos apenas.

### <a name="try-it-out"></a>Experimente
1. Na consola do Configuration Manager, na área de trabalho **Administração** , aceda a **Serviços Cloud** > **Subscrição do Microsoft Intune**.
2. No **home page** separador o **subscrição** grupo, escolha **configurar plataformas** e, em seguida, selecione **Android** ou **iOS**.
3. Selecione **bloco pessoal dispositivos pertencentes à empresa**.

## <a name="android-for-work-application-management-policy-for-copy-paste"></a>Android para a política de gestão de aplicações de trabalho para copiar-colar
Iremos foi atualizado com as descrições de definição para Android para itens de configuração de trabalho para o **permitir partilha de dados entre a vida profissional e a pessoal perfil**.

|Antes de pré-visualização técnica 1706 | Novo nome de opção | Comportamento|
|-|-|-|
|Impedir a qualquer partilha através de limites| Predefinição restrições de partilha| Trabalho ao pessoal: Predefinição (esperada até ser bloqueado em todas as versões) <br>Pessoal para trabalho: Predefinido (permitido 6.x+, bloqueada no 5. x)|
|Sem restrições|   Aplicações pessoais perfil podem processar pedidos de perfil de trabalho de partilha| Trabalho ao pessoal: Permitido  <br>Pessoal para trabalho: Permitido|
|As aplicações no perfil de trabalho podem processar pedidos de perfil de pessoal de partilha |As aplicações no perfil de trabalho podem processar pedidos de perfil de pessoal de partilha |Trabalho ao pessoal: Predefinição<br>Pessoal para trabalho: Permitido<br>(Apenas é útil em 5. x onde pessoal para o trabalho está bloqueado)|

Nenhuma destas opções diretamente impedir o comportamento de copiar-colar. Foi adicionada uma definição personalizada para o serviço e a aplicação Portal da empresa em 1704 que podem ser configurados para impedir a copiar-colar. Isto pode ser definido através de URI personalizada.

-   OMA-URI: ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
-   Tipo de valor: Booleano

Definição DisallowCrossProfileCopyPaste para verdadeiro impede o comportamento de copiar-colar entre Android para trabalho pessoal e perfis de trabalho.

### <a name="try-it-out"></a>Experimente
1. Na consola do Configuration Manager, selecione **ativos e compatibilidade** > **descrição geral** > **as definições de compatibilidade** > **itens de configuração**.
2. Escolha **criar** para criar um novo item de configuração e especificar **nome** e **Android para trabalho**.
3. No dispositivo grupos para configurar a definição, selecione **trabalho perfil**e escolha **seguinte**.
4. Selecione o valor para **permitir partilha de dados entre a vida profissional e a pessoais perfis**e, em seguida, conclua o assistente.

## <a name="device-health-attestation-assessment-for-compliance-policies-for-conditional-access"></a>Avaliação de atestado de estado de funcionamento do dispositivo para as políticas de conformidade de acesso condicional
<!-- 1097546 -->
A partir desta versão, pode utilizar o estado de atestado de estado de funcionamento do dispositivo como uma regra de política de conformidade de acesso condicional aos recursos da empresa.

### <a name="try-it-out"></a>Experimente
Selecione uma regra de atestado de estado de funcionamento do dispositivo como parte de uma avaliação da política de conformidade.

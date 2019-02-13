---
title: Technical Preview 1706
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis na versão 1706 Technical Preview do System Center Configuration Manager.
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 251a614aebce244edddfe362a5f7119ca9dd0c87
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132511"
---
# <a name="capabilities-in-technical-preview-1706-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1706 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1706. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para a utilização de um técnico de pré-visualização, como atualizar entre as versões e como fornecer comentários sobre os recursos de uma technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos neste Technical Preview:**

-   **Move o ponto de distribuição** -as opções na consola para mover um ponto de distribuição entre sites, não podem ser utilizadas com esta versão devido ao limite de pré-visualização técnica de um único site primário.

-   **Definições de conformidade do dispositivo** -podem ocorrer comportamento oposto ao utilizar as duas das novas definições de conformidade de dispositivo:
    - **Bloquear a depuração de USB no dispositivo**
    - **Bloquear aplicações de origens desconhecidas**

        Por exemplo, se os administradores de definir **depuração de USB de bloco no dispositivo** ao **verdadeiro**, todos os dispositivos que não têm a depuração de USB ativada são marcados como não conforme.

**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improved-boundary-groups-for-software-update-points"></a>Grupos de limites melhorada para os pontos de atualização de software
<!-- 1324591 --> Esta versão inclui melhoramentos para como os pontos de atualização de software trabalham com grupos de limites. Os itens abaixo resumem o novo comportamento de contingência:
- Agora, a contingência para pontos de atualização de software utiliza um horário configurável para contingência para grupos de limites de vizinho, com um tempo mínimo de 120 minutos.

- Independentemente da configuração de contingência, um cliente tenta contactar o último ponto de atualização de software, utilizada para 120 minutos. Depois de a conseguir chegar a esse servidor para 120 minutos, o cliente verifica, em seguida, seu pool de pontos de atualização de software disponíveis, para que ele possa encontrar um novo.

  -   Todos os pontos de atualização de software no grupo de limite atual do cliente são adicionados ao agrupamento do cliente imediatamente.

  -   Uma vez que um cliente tenta utilizar o respetivo servidor original para 120 minutos antes de contactar um novo, não existem servidores adicionais são contactados até depois de ter decorrido duas horas.

  -   Se a contingência para um grupo de vizinho está configurada para o mínimo de 120 minutos, pontos de atualização de software desse grupo de limite vizinho fará parte do conjunto do cliente de servidores disponíveis.

- Depois de a conseguir contactar o respetivo servidor original de duas horas, o cliente muda para um ciclo mais curto para entrar em contato com um novo ponto de atualização de software.

  Isso significa que se um cliente não conseguir estabelecer ligação com um novo servidor, ele, rapidamente, seleciona o próximo servidor a partir do seu pool de servidores disponíveis e tenta contactar o que um.

  -   Este ciclo continuará até o cliente se liga a um software, pode servir de ponto de atualização.
  -   Até que o cliente localiza um ponto de atualização de software, os servidores adicionais são adicionados ao agrupamento de servidores disponíveis quando o tempo de contingência para cada grupo de limite vizinho é cumprido.

Para obter mais informações, consulte [pontos de atualização de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) o tópico de grupos de limites para o ramo atual.


## <a name="site-server-role-high-availability"></a>Disponibilidade elevada de função do servidor de site
<!-- 1128774 --> Elevada disponibilidade para a função de servidor do site é uma solução de Configuration Manager com base para instalar um servidor de site primário adicional no *passivo* modo. O servidor de site de modo passivo além disso é ao seu servidor de site primário existente que esteja no *Active Directory* modo. Um servidor de site de modo passivo está disponível para uso imediato, quando necessário.

Um servidor de site primário em modo passivo:
-   Utiliza o mesmo banco de dados do site como seu servidor do site do Active Directory.
-   Recebe uma cópia da biblioteca de conteúdos da servidores do site ativa, que é, então, mantida em sincronia.
-   Não escrever dados na base de dados do site, desde que ele está no modo passivo.
-   Não suporta a instalação ou remoção de funções do sistema de sites opcionais, desde que ele está no modo passivo.

Para tornar seu servidor de site do Active Directory de modo de servidor do site de modo passivo, manualmente promovê-lo. Esse procedimento alterna o servidor do site ativo deve ser o servidor de site passivo. As funções de sistema de sites que estão disponíveis no servidor de modo ativo original permanecem disponíveis, desde que esse computador está acessível. Apenas a função de servidor do site é mudou entre o modo de ativo e passivo.

Para instalar um servidor de site de modo passivo, utilize o **criar Assistente de servidor de sistema de sites** para configurar um novo servidor de site com um tipo de **servidor do site primário** e um modo de **passivo**. O assistente, em seguida, executa a configuração do Configuration Manager no servidor especificado para instalar o novo servidor de site em modo passivo. Após a instalação estiver concluída, o servidor de site do Active Directory de modo mantém em sincronia com as alterações ou as configurações que fizer para o servidor do site do Active Directory do servidor do site de modo passivo e a respetiva biblioteca de conteúdos.

### <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações
-   Um servidor de site único em modo passivo é suportado em cada site primário.

-   O servidor do site em modo passivo pode estar no local ou com base na cloud no Azure.

-   O modo de Active Directory e servidores de site de modo passivo devem estar no mesmo domínio.

-   O modo de Active Directory e servidores de site de modo passivo tem de utilizar a mesma base de dados, que tem de ser remota dos computadores de cada servidor do site.

    -   O SQL Server que aloja a base de dados pode utilizar uma instância predefinida, com o nome instância, o cluster do SQL Server ou um grupo de Disponibilidade AlwaysOn.

    -   O servidor do site em modo passivo está configurado para utilizar a mesma base de dados do site que o servidor de site de modo ativo. No entanto, o servidor do site de modo passivo não utiliza essa base de dados até depois que ele é promovido para o modo ativo.

-   O computador que executar o servidor do site de modo passivo:

    -   Tem de cumprir os [pré-requisitos para instalar um site primário](https://docs.microsoft.com/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).

    -   Instalações usando arquivos de origem que correspondem à versão do servidor do site de modo ativo.

    -   Não pode ter uma função de sistema de sites a partir de qualquer site antes de instalar o site de modo passivo.

-   Os computadores de servidor de site ativo e passivo de modo podem executar vários sistemas operativos ou de versões de service pack, desde que os dois ser suportados pela versão do Configuration Manager.

-   Promoção do servidor do site de modo passivo para o servidor de modo ativo é manual. Não há nenhuma ativação pós-falha automática.

-   Funções de sistema de sites podem ser instaladas apenas no servidor do site que está no modo ativo.

    -   Um servidor de sites no modo de Active Directory suporta todas as funções de sistema de sites. Não é possível instalar funções do sistema de sites no servidor quando estiver no modo passivo.

    -   Funções de sistema de sites que utilizam uma base de dados (como o ponto do reporting) tem de ter essa base de dados num servidor remoto do tanto o modo de Active Directory e servidores de site de modo passivo.

    -   O SMS_Provider não instala no servidor do site em modo passivo. Uma vez que tem de ligar a um SMS_Provider para o site para promover manualmente o servidor de site de modo passivo para o modo ativo, recomendamos [instalar pelo menos uma instância adicional do fornecedor de](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider) num computador adicional.

**Problema conhecido**:   
Com esta versão, **estado** para as seguintes condições são apresentados na consola do como valores numéricos em vez de texto legível:
-   131071 – falha na instalação de servidor de site
-   720895 – falha na desinstalação de função de servidor de site
-   851967 – falha na ativação pós-falha

### <a name="add-a-site-server-in-passive-mode"></a>Adicionar um servidor de site em modo passivo
1.  Na consola, aceda a **Administration** > **configuração do Site** > **Sites** e iniciar o [Adicionar Assistente de funções de sistema de sites ](/sccm/core/servers/deploy/configure/install-site-system-roles). Também pode utilizar o **criar Assistente de servidor de sistema de sites**.

2.  Sobre o **gerais** página, especifique o servidor que alojará o servidor do site de modo passivo. O servidor que especificar não é possível alojar quaisquer funções de sistema de sites antes de instalar um servidor de site em modo passivo.

3.  Sobre o **seleção da função do sistema** , selecione apenas **servidor de site primário em modo passivo**.

4.  Para concluir o assistente, tem de fornecer as seguintes informações que são utilizadas para executar a configuração e instalar a função de servidor do site no servidor especificado:
    -   Optar por copiar os ficheiros de instalação do servidor do site do Active Directory para o novo servidor de site de modo passivo ou especifique um caminho para uma localização que contém o conteúdo do servidor do site ativo **CD. Mais recente** pasta.

    -   Especifique o mesmo servidor de base de dados do site e o nome de base de dados como utilizado pelo servidor do site de modo ativo.

5.  Em seguida, o Configuration Manager instala o servidor do site em modo passivo no servidor especificado.

Para o estado de instalação detalhadas, aceda a **Administration** > **configuração do Site** > **Sites**.
-   O estado para o servidor de site em modo passivo indicará **instalando**.

-   Selecione o servidor e, em seguida, clique em **Mostrar estado** para abrir **estado de instalação do servidor de Site** para obter mais informações.



### <a name="promote-the-passive-mode-site-server-to-active-mode"></a>Promover o servidor de site de modo passivo para o modo ativo
Quando quiser alterar o servidor de site de modo passivo para o modo ativo, fazê-lo a **nós** painel na **administração** > **configuração do Site**  >  **Sites**. Desde que pode acessar uma instância do SMS_Provider, pode acessar o site para fazer esta alteração.
1.  Na **nós** painel da consola do Configuration Manager, selecione o servidor do site em modo passivo e, em seguida, no Friso e escolha **promover para ativo**.

2.  Simples **Status** para o servidor que está a promover apresenta no **nós** painel como **promover**.

3.  Após a promoção estiver concluída, o **estado** coluna mostra **OK** tanto a nova *Active Directory* servidor do site de modo e para o novo *passivo* servidor do site de modo.

4.  Na **Administration** > **configuração do Site** > **Sites**, o nome do servidor do site primário agora apresenta o nome do novo *Active Directory* servidor do site de modo.
Para o estado detalhado, aceda a **monitorização** > **estado do servidor de Site**.
    -   O **modo** coluna identifica qual servidor é *Active* ou *passivo*.

    -   E promover um servidor de modo passivo para o modo ativo, selecione o servidor de sites que está a promover para ativo e, em seguida, escolha **Mostrar estado** a partir do Friso. Esta ação abre o **estado de promoção de servidor do Site** janela que apresenta detalhes adicionais sobre o processo.

Quando um servidor de site no modo ativo muda ao longo de modo passivo, apenas a função de sistema de sites é feita passiva. Todas as outras funções do sistema de site instaladas nesse computador permanecem acessíveis aos clientes e Active Directory.


### <a name="daily-monitoring"></a>Monitorização diariamente
Quando tiver um site primário em modo passivo, monitorizá-lo de diário para garantir que continua a ser sincronizado com o servidor do site de modo ativo e prontas a utilizar. Para tal, aceda a **monitorização** > **estado do servidor de Site**. Aqui pode ver o modo de Active Directory e servidores de site de modo passivo.

O **resumo** separador:
-   O **modo** coluna identifica qual servidor está ativa ou passiva.
-   O **Status** listas de coluna **OK** quando o servidor de modo passivo está em sincronização com o servidor de modo ativo.
-   Para ver detalhes adicionais sobre o estado da sincronização de conteúdo, clique em **Mostrar estado** do Estado de sincronização de conteúdo. Esta ação abre o separador de biblioteca de conteúdos em que pode experimentar para corrigir problemas de sincronização de conteúdo.

O **biblioteca de conteúdos** separador:
-   Ver os **estado** para conteúdo que sincroniza a partir do servidor do site ativo para o servidor de site de modo passivo.
-   Pode selecionar o conteúdo com um Estado de **falhada**e, em seguida, escolha **sincronizar itens selecionados** a partir do Friso. Esta ação tenta ressincronizar a esse conteúdo de origem do conteúdo para o servidor de site de modo passivo. Durante a recuperação, o estado indicará **em curso**, e quando ele está em sincronização, é apresentado como **êxito**.

### <a name="try-it-out"></a>Experimente!
Experimente concluir as seguintes tarefas e, em seguida, envie-nos **comentários** partir do **home page** separador do friso para nos informar como correu:
-   Posso instalar um site primário em modo passivo.
-   Posso utilizar a consola para promover o servidor de site de modo passivo para o tornar o servidor do site de modo ativo e confirmar a alteração de estado para ambos os servidores de site.


## <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Incluir a fidedignidade para ficheiros específicos e pastas numa política de Device Guard
<!-- 1324676 --> Nesta versão, adicionámos mais capacidades para [Device Guard](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) gestão de políticas

Agora pode adicionar opcionalmente confiança em arquivos específicos para pastas de uma política do Device Guard. Isto permite-lhe:

1.  Resolver problemas com os comportamentos de instalador gerido
2.  Confiar em aplicações de linha de negócio que não não possível implementar com o Configuration Manager
3.  Confie em aplicações que estão incluídas numa imagem de implantação do sistema operativo.

### <a name="try-it-out"></a>Experimente!

1.  Enquanto estiver a criar uma política do Device Guard, na guia as inclusões do Assistente de política de criar o Device Guard, clique em **adicionar**.
2.  Na **adicionar ficheiro fidedigno ou pasta** diálogo caixa, especifique informações sobre o ficheiro ou pasta que deseja confiar. Pode especificar um caminho de ficheiro ou pasta local ou ligar a um dispositivo remoto para o qual tem permissão para se ligar e especifique um caminho de ficheiro ou pasta em que o dispositivo.
3.  Conclua o assistente.


## <a name="hide-task-sequence-progress"></a>Ocultar o progresso da sequência de tarefas
<!-- 1354291 --> Nesta versão, pode controlar quando o progresso da sequência de tarefas é apresentado aos utilizadores finais através de uma nova variável. Na sua sequência de tarefas, utilize o **definir variável da sequência de tarefas** passo para definir o valor para o **TSDisableProgressUI** variável para ocultar ou exibir o progresso da sequência de tarefas. Pode utilizar o passo Definir variável da sequência de tarefas múltiplas vezes numa sequência de tarefas para alterar o valor da variável. Isso permite ocultar ou exibir o progresso da sequência de tarefas em diferentes seções da sequência de tarefas.

#### <a name="to-hide-task-sequence-progress"></a>Para ocultar o progresso da sequência de tarefas
No editor de sequência de tarefas, utilize o [definir variável da sequência de tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) passo para definir o valor da **TSDisableProgressUI** variável à **verdadeiro** para ocultar o progresso da sequência de tarefas.

#### <a name="to-display-task-sequence-progress"></a>Para exibir o progresso da sequência de tarefas
No editor de sequência de tarefas, utilize o [definir variável da sequência de tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) passo para definir o valor da **TSDisableProgressUI** variável à **False** para exibir o progresso da sequência de tarefas.

## <a name="specify-a-different-content-location-for-install-content-and-uninstall-content"></a>Especifique uma localização de conteúdo diferente para o conteúdo de instalação e conteúdo de desinstalação
<!-- 1097546 --> No Configuration Manager hoje em dia, especificar a localização de instalação que contém os ficheiros de configuração para uma aplicação. Quando especificar uma localização de instalação, isso também é utilizado como a localização de desinstalação para o conteúdo da aplicação.
Com base no seu feedback, quando pretender desinstalar uma aplicação implementada, e o conteúdo da aplicação não está no computador cliente, em seguida, o cliente irá transferir todos os ficheiros de configuração de aplicação novamente antes da aplicação é desinstalada.
Para resolver este problema, pode agora especificar tanto uma instalação de conteúdo de localização de conteúdo de desinstalação de localização e opcional. Além disso, pode optar por não especificar uma localização de conteúdo de desinstalação.

### <a name="try-it-out"></a>Experimente!

1. Nas propriedades de tipo de implementação de uma aplicação, clique nas **conteúdo** separador.
2. Configurar o **localização de conteúdo de instalação** normalmente.
3. Para **definições de conteúdo de desinstalação**, escolha um dos seguintes:
    - **Mesmo como instalar o conteúdo** -será utilizada a mesma localização do conteúdo, independentemente se estiver a instalar ou desinstalar a aplicação.
    - **Nenhum conteúdo de desinstalação** -Escolha esta opção se não pretende fornecer uma localização de conteúdo de desinstalação da aplicação.
    - **Diferente do conteúdo de instalação** -Escolha esta opção se pretender especificar uma localização de conteúdo de desinstalação diferente da localização de conteúdo de instalação.
5. Se tiver selecionado **diferentes do conteúdo de instalação**, navegue para ou introduza a localização do conteúdo do aplicativo que será utilizado para desinstalar a aplicação.
6. Clique em **OK** para fechar a caixa de diálogo de propriedades de tipo de implementação.


## <a name="accessibility-improvements"></a>Melhorias de acessibilidade  
<!--1253000 --> Esta pré-visualização apresenta vários aprimoramentos para o [funcionalidades de acessibilidade](/sccm/core/understand/accessibility-features) na consola do Configuration Manager. Estas atualizações incluem:     

**Novos atalhos de teclado para mover-se a consola:**
-   CTRL + M - conjuntos de concentrar-se no painel principal (central).
-   CTRL + T - o foco de conjuntos para o nó superior no painel de navegação. Se o foco já foi nesse painel, o foco está definido para o último nó que visitou.
-   CTRL + I - foco conjuntos para a barra de navegação estrutural, abaixo da faixa de opções.
-   CTRL + L - o foco de conjuntos para o **pesquisa** campo, quando disponível.
-   CTRL + D. o-foco de conjuntos ao painel de detalhes, quando disponível.
-   ALT – o foco de alterações e sair da faixa de opções.

**Melhoramentos gerais:**
-   Melhorada a navegação no painel de navegação quando o utilizador escreve as letras de um nome de nó.
-   Navegação do teclado por meio de exibição principal e a faixa de opções são agora circular.
-   Navegação do teclado no painel de detalhes é agora circular. Para voltar para o objeto anterior ou o painel, utilize Ctrl + D, em seguida, Shift + SEPARADOR.
-   Depois de atualizar uma exibição de área de trabalho, o foco está definido para o painel principal da área de trabalho.
-   Foi corrigido um problema para permitir que os leitores de ecrã de anunciar os nomes de itens de lista.
-   Foi adicionados nomes acessíveis para vários controles na página que permite que os leitores de ecrã de anunciar a informações importantes.


## <a name="changes-to-the-azure-services-wizard-to-support-upgrade-readiness"></a>Alterações ao Assistente de serviços do Azure para oferecer suporte a preparação de atualizações
<!-- 1353331 --> A partir desta versão, utilize o Assistente de serviços do Azure para configurar uma ligação do Configuration Manager para [preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics). A utilização do assistente simplifica a configuração do conector utilizando um assistente comuns para serviços do Azure relacionados.   

Embora o método para configurar a ligação foi alterado, pré-requisitos para a ligação e como utilizar a preparação de atualizações permanecem inalterados.   

### <a name="prerequisites-for-upgrade-readiness"></a>Pré-requisitos para a preparação da atualização
As pré-requisitos para um [ligação para o Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics#create-a-connection-to-upgrade-readiness) são iguais às detalhadas para o atual ramo do Configuration Manager. Eles são reproduzidos aqui para sua comodidade:  

**Pré-requisitos**
-   Para adicionar a ligação, o ambiente do Configuration Manager tem de configurar uma [ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) num [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation). Ao adicionar a ligação ao seu ambiente, ele irá também instalar o Microsoft Monitoring Agent no computador com esta função de sistema de sites.
-   Registe-se do Configuration Manager como uma ferramenta de gestão "Aplicação Web e/ou API Web" e obter o [ID de cliente desse Registro](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
-   Crie uma chave de cliente para a ferramenta de gestão registado no Azure Active Directory.
-   No Portal de gestão do Azure, forneça a aplicação web registada com permissão para aceder ao OMS, conforme descrito em [fornecer o Configuration Manager com permissões para OMS](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

> [!IMPORTANT]       
> Ao configurar a permissão para aceder ao OMS, certifique-se de que escolha a **contribuinte** função e atribua-as permissões para o grupo de recursos da aplicação registada.

Depois dos pré-requisitos estão configurados, está pronto para utilizar o Assistente para criar a ligação.

### <a name="use-the-azure-services-wizard-to-configure-upgrade-readiness"></a>Utilize o Assistente de serviços do Azure para configurar a preparação de atualizações
1.  Na consola, aceda a **Administration** > **descrição geral** > **serviços Cloud** > **osserviçosdoAzure**e, em seguida, escolha **configurar os serviços do Azure** da **home page** separador do Friso, para iniciar o **Assistente de serviços do Azure**.

2.  Na **dos serviços do Azure** página, selecione a **conector de preparação de atualização**e, em seguida, clique em **seguinte**.

3.  Sobre o **aplicação** , especifique seu **ambiente do Azure** (technical preview oferece suporte apenas a Cloud pública). Em seguida, clique em **importação** para abrir o **importar aplicações** janela.

4.  Na **importar aplicações** janela, especifique os detalhes para uma aplicação web que já existe no seu Azure AD.
    -   Forneça um nome amigável para o nome de inquilino do Azure AD. Em seguida, especifique o ID de inquilino, o nome da aplicação, ID de cliente, chave secreta para a aplicação web do Azure e o URI de ID de aplicação.
    -   Clique em **Verifique se**e se tiver êxito, clique em **OK** para continuar.

5.   Sobre o **configuração** , especifique a subscrição, grupo de recursos e as área de trabalho de análise do Windows que pretende utilizar com esta ligação para a preparação de atualizações.  

6.  Clique em **próxima** Ir para o **resumo** página e, em seguida, conclua o Assistente para criar a ligação.


## <a name="new-client-settings-for-cloud-services"></a>Novas definições de cliente para serviços em nuvem
<!-- 1319883 -->

Nesta versão, adicionámos duas novas definições de cliente do Configuration Manager. Encontrará no **serviços Cloud** secção.  Estas definições dão-lhe as seguintes capacidades:

- Controlo que clientes do Configuration Manager podem aceder a um gateway de gestão de cloud configurado.
- Registe-se automaticamente os clientes do Configuration Manager associado a um domínio Windows 10 com o Azure Active Directory.

Estas novas definições de ajudá-lo a realizar as funcionalidades descritas a [1705 do Configuration Manager Technical Preview](/sccm/core/get-started/capabilities-in-technical-preview-1705#new-capabilities-for-azure-ad-and-cloud-management).

### <a name="before-you-start"></a>Antes de começar

Tem de ter instalado e configurado o Azure AD Connect entre seu Active Directory no local e de inquilino do Azure AD.

Se remover a ligação, os dispositivos não são não registados, mas não existem dispositivos novos serão registados.

### <a name="try-it-out"></a>Experimente!

1. Configurar a seguinte secção de definições (que se encontra nos serviços Cloud) de cliente utilizando as informações em [como configurar as definições de cliente](/sccm/core/clients/deploy/configure-client-settings).
    -   **Registar automaticamente novos dispositivos associados a um domínio do Windows 10 com o Azure Active Directory** – definido como **Sim** (predefinição), ou **não**.
    -   **Permitir que os clientes utilizar um gateway de gestão na cloud** – definido como **Sim** (predefinição), ou **não**.
2.  Implemente as definições de cliente na coleção necessária de dispositivos.

Para confirmar que o dispositivo está associado ao Azure AD, execute o comando **dsregcmd.exe /status** numa janela de linha de comandos. O **AzureAdjoined** campo nos resultados da mostrará **Sim** se o dispositivo estiver associado ao Azure AD.

## <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Criar e executar scripts do PowerShell a partir da consola do Configuration Manager
<!-- 1236459 -->

No Configuration Manager, pode implementar scripts em dispositivos de cliente através de pacotes e programas. Este technical preview, adicionámos novas funcionalidades que lhe oferece as seguintes ações:

- Importar Scripts do PowerShell para o Configuration Manager
- Editar os scripts a partir da consola do Configuration Manager (para apenas scripts não assinados)
- Scripts de Mark como aprovado ou negado, para melhorar a segurança
- Executar scripts em coleções de PCs de cliente do Windows e no local geridos Windows PCs. Não precisa implementar scripts, em vez disso, estas são executadas em tempo real nos dispositivos cliente.
- Examine os resultados devolvidos pelo script na consola do Configuration Manager.


### <a name="prerequisites"></a>Pré-requisitos

Uso de scripts, tem de ser membro da função de segurança adequado do Configuration Manager.

- **Para importar e criar scripts** -sua conta tem de ter **Create** permissões para **Scripts de SMS** no **administrador total** função de segurança.
- **Para aprovar ou negar scripts** -a conta tem de ter **aprovar** permissões para **Scripts de SMS** no **administrador total** função de segurança.
- **A execução de scripts** -a conta tem de ter **executar Script** permissões para **coleções** no **Gestor de definições de conformidade** função de segurança.

Para obter mais informações sobre funções de segurança do Configuration Manager, consulte [Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).

Por predefinição, os utilizadores não podem aprovar um script que tenham criado. Uma vez que os scripts são poderosas, versátil e podem ser implementadas para o número de dispositivos, introduzimos um novo conceito de fornecer a capacidade de separar as funções entre a pessoa que os autores de script e a pessoa que aprova o script. Isso fornece um nível adicional de segurança contra a execução de um script sem supervisão. Pode desativar esta aprovação secundária, para facilitar o teste, particularmente durante o lançamento de pré-visualização técnica.

Para permitir aos utilizadores aprovar os próprios scripts:

1. Na consola do Configuration Manager, clique em **Administração**.
2. Na área de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.
3. Na lista de sites, escolha o seu site e, em seguida, no **home page** separador a **Sites** , clique em **definições de hierarquia**.
4. Na **gerais** separador da **propriedades de definições de hierarquia** caixa de diálogo caixa, desmarque a caixa de verificação **não permitir que os autores de script aprovar os próprios scripts**.


### <a name="try-it-out"></a>Experimente!

#### <a name="import-and-edit-a-script"></a>Importar e editar um script

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. Na **biblioteca de Software** área de trabalho, clique em **Scripts**.
3. Sobre o **home page** separador a **criar** , clique em **criar Script**.
4. Sobre o **Script** página do **criar Script de** assistente, configure o seguinte:
    - **Nome do script** -introduza um nome para o script. Embora possa criar vários scripts com o mesmo nome, isso tornará mais difícil para que possa encontrar o script que precisa na consola do Configuration Manager.
    - **Linguagem de script** - atualmente, só **PowerShell** scripts são suportados.
    - **Importar** -importar um script do PowerShell para a consola. O script é apresentado na **Script** campo.
    - **Limpar** -remove o script atual a partir de **Script** campo.
    - **Script** -apresenta o script atualmente importado. Pode editar o script neste campo, se necessário.
5. Conclua o assistente. O script novo é apresentado na **Script** lista com o estado **aguardar aprovação**. Antes de poder executar este script nos dispositivos cliente, terá de o aprovar.


#### <a name="approve-or-deny-a-script"></a>Aprovar ou recusar um script



Antes de poder executar um script, tem de ser aprovado. Para aprovar um script:

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. Na **biblioteca de Software** área de trabalho, clique em **Scripts**.
3. Na **Script** lista, selecione o script que pretende aprovar ou negar e, em seguida, no **home page** separador o **Script** , clique em **aprovar/negar**.
4. Na **aprovar ou recusar scriipt** caixa de diálogo **aprovar**, ou **negar** o script e, opcionalmente, introduza um comentário sobre sua decisão. Se negar um script, não pode ser executado nos dispositivos cliente.
5. Conclua o assistente. Na **Script** listar, verá o **estado de aprovação** alteração de coluna consoante a ação que realizar.

#### <a name="run-a-script"></a>Executar um script

Assim que um script for aprovado, ele pode ser executado numa coleção que escolheu.

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2. Na área de trabalho **Ativos e Compatibilidade** , clique em **Coleções de Dispositivos**.
3. Na **coleções de dispositivos** lista, clique na coleção de dispositivos em que pretende executar o script.
3. Sobre o **home page** separador a **todos os sistemas** , clique em **executar Script**.
4. Sobre o **Script** página do **executar Script** assistente, escolher um script a partir da lista. Apenas os scripts aprovados são apresentados. Clique em **seguinte**e, em seguida, conclua o assistente.

#### <a name="monitor-a-script"></a>Monitorizar um script

Depois de executar um script em dispositivos cliente, utilize este procedimento para monitorizar o êxito da operação.

1. Na consola do Configuration Manager, clique em **monitorização**.
2. Na **monitorização** área de trabalho, clique em **os resultados do Script**.
3. Na **os resultados do Script** lista, exibir os resultados para cada script tiver executado nos dispositivos cliente. Um código de saída do script **0**, normalmente indica que o script foi executado com êxito.

## <a name="pxe-network-boot-support-for-ipv6"></a>Suporte de arranque de rede PXE para IPv6
<!-- 1269793 --> Agora pode ativar o suporte de arranque de rede PXE para IPv6 iniciar uma implementação de sistema operativo de sequência de tarefas. Quando utiliza esta definição, os pontos de distribuição com PXE ativado irão suportar IPv4 e IPv6. Esta opção não necessita de WDS e deixará de WDS se estiver presente.

#### <a name="to-enable-pxe-boot-support-for-ipv6"></a>Para ativar o suporte de arranque PXE para IPv6
Utilize o procedimento seguinte para ativar a opção para suporte de IPv6 para PXE.

1. Na consola do Configuration Manager, aceda a **Administration** > **descrição geral** > **pontos de distribuição**e clique em  **Propriedades** para pontos de distribuição com PXE ativado.
2. Sobre o **PXE** separador, selecione **suporte IPv6** para ativar o suporte de IPv6 para PXE.

## <a name="manage-microsoft-surface-driver-updates"></a>Gerir atualizações de controladores do Microsoft Surface
<!-- 1098490 --> Agora, pode utilizar o Configuration Manager para gerir atualizações de controladores do Microsoft Surface.

### <a name="prerequisites"></a>Pré-requisitos
Todos os pontos de atualização de software devem executar o Windows Server 2016.

### <a name="try-it-out"></a>Experimente!
Experimente concluir as seguintes tarefas e, em seguida, envie-nos **comentários** partir do **home page** separador do friso para nos informar como correu:
1. Ative a sincronização para controladores do Microsoft Surface. Utilize o procedimento [configurar a classificação e produtos](/sccm/sum/get-started/configure-classifications-and-products) e selecione **drivers de incluir o Microsoft Surface e atualizações de firmware** no **classificações** separador para Ative controladores superfície.
2. [Sincronizar os controladores do Microsoft Surface](/sccm/sum/get-started/synchronize-software-updates.md).
3. [Implementar controladores sincronizados do Microsoft Surface](/sccm/sum/deploy-use/deploy-software-updates)

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configurar a atualização do Windows para políticas de diferimento de negócios
<!-- 1290890 --> Agora, pode configurar políticas de diferimento para atualizações de funcionalidades do Windows 10 ou atualizações de qualidade para o Windows 10 dispositivos geridos diretamente pelo Windows Update para empresas. Pode gerir as políticas de diferimento no novo **Windows Update para políticas de negócio** no nó **biblioteca de Software** > **manutenção do Windows 10**.

### <a name="prerequisites"></a>Pré-requisitos
Dispositivos Windows 10 geridos pelo Windows Update para empresas tem de ter conectividade à Internet.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Para criar uma atualização do Windows para a política de diferimento de negócio
1. Na **biblioteca de Software** > **manutenção do Windows 10** > **Windows Update para políticas de negócio**
2. Sobre o **home page** separador a **criar** grupo, selecione **criar Windows política Update para empresas** para abrir a atualização do Windows criar para o Assistente de política de negócios.
3. Sobre o **gerais** , indique um nome e descrição para a política.
4. Sobre o **políticas de diferimento** página, configure se pretende diferir ou colocar em pausa atualizações de funcionalidades.    
    As atualizações de funcionalidade são, geralmente, novas funcionalidades do Windows. Depois de configurar o **ramificar o nível de preparação** definir, em seguida, pode definir se, e durante quanto tempo, gostaria de diferir a receção de atualizações de funcionalidades após a sua disponibilidade da Microsoft.
    - **Nível de preparação para filiais**: Defina o ramo para o qual o dispositivo irá receber atualizações do Windows (Current Branch ou Current Branch for Business).
    - **Período de diferimento (dias)**:  Especifique o número de dias de diferimento para que as atualizações de funcionalidade. Pode diferir a receção destas atualizações de funcionalidades durante um período de 180 dias após seu lançamento.
    - **A partir de atualizações de funcionalidades em pausa**: Selecione se colocar em pausa dispositivos recebam atualizações de funcionalidades durante um período de 60 dias desde o momento em que colocar em pausa as atualizações. Após ter passado o máximo de dias, a funcionalidade de pausa irá automaticamente expirar e o dispositivo irá procurar atualizações do Windows para detetar atualizações aplicáveis. Após esta procura, pode colocar as atualizações em pausa novamente. Pode unpause atualizações de funcionalidades ao desmarcar a caixa de verificação.   
5. Escolha se pretende diferir ou colocar em pausa as atualizações de qualidade.     
    As atualizações de qualidade são, geralmente, correções e melhorias às funcionalidades existentes do Windows e, normalmente, são publicadas na primeira Terça-feira de cada mês, embora possam ser lançadas em qualquer altura pela Microsoft. Pode definir se, e durante quanto tempo, gostaria de diferir a receção de atualizações de qualidade, após a sua disponibilidade.
    - **Período de diferimento (dias)**: Especifique o número de dias de diferimento para que as atualizações de funcionalidade. Pode diferir a receção destas atualizações de funcionalidades durante um período de 180 dias após seu lançamento.
    - **A partir de atualizações de qualidade em pausa**: Selecione se colocar em pausa a receção de atualizações de qualidade de dispositivos durante um período máximo de 35 dias desde o momento em que colocar em pausa as atualizações. Após ter passado o máximo de dias, a funcionalidade de pausa irá automaticamente expirar e o dispositivo irá procurar atualizações do Windows para detetar atualizações aplicáveis. Após esta procura, pode colocar as atualizações em pausa novamente. Pode unpause as atualizações de qualidade ao desmarcar a caixa de verificação.
6. Selecione **instalar atualizações a partir de outros Products Microsoft** para ativar a definição de política de grupo que tornam as definições de suspensão aplicáveis ao Microsoft Update, bem como as atualizações do Windows.
7. Selecione **incluir drivers com o Windows Update** para atualizar automaticamente os controladores de atualizações do Windows. Se desmarcar esta definição, as atualizações de controladores não são transferidas de atualizações do Windows.
8. Conclua o Assistente para criar a nova política de diferimento.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Implementar uma atualização do Windows para a política de diferimento de negócio
1. Na **biblioteca de Software** > **manutenção do Windows 10** > **Windows Update para políticas de negócio**
2. Sobre o **home page** separador a **implantação** grupo, selecione **implementar Windows política Update para empresas**.
3. Configure as seguintes definições:
    - **Política de configuração para implementar**: Selecione a atualização do Windows para a política de negócios que gostaria de implementar.
    - **Coleção**: Clique em **procurar** para selecionar a coleção onde pretende implementar a política.
    - **Remediar regras incompatíveis quando suportado**: Selecione esta opção para retificar automaticamente quaisquer regras não compatíveis com o Windows Management Instrumentation (WMI), o registro, scripts e todas as definições para dispositivos móveis inscritos pelo Configuration Manager.
    - **Permitir remediação fora da janela de manutenção**: Se uma janela de manutenção tiver sido configurada para a coleção que pretende implementar a política, ative esta opção para que as definições de conformidade retifiquem o valor fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [como utilizar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).
    - **Gerar um alerta**: Configura um alerta que é gerado se a compatibilidade da linha de base de configuração for inferior a uma percentagem especificada até uma data especificada e a hora. Também pode especificar se pretende que seja enviado um alerta para o System Center Operations Manager.
    - **Atraso aleatório (horas)**: Especifica uma janela de atraso para evitar processamento excessivo no serviço de inscrição de dispositivos de rede. O valor predefinido é de 64 horas.
    - **Agenda**: Especifique o agendamento de avaliação de compatibilidade através do qual o perfil implementado é avaliado nos computadores cliente. O agendamento pode ser simples ou personalizado. O perfil é avaliado por computadores cliente quando o utilizador inicia sessão.
4.  Conclua o Assistente para implementar o perfil.



## <a name="support-for-entrust-certification-authorities"></a>Suporte para autoridades de certificação da Entrust
<!-- 1350740 --> O Configuration Manager suporta agora a autoridades de certificação da Entrust; Isso habilita a entrega de certificado PFX para dispositivos inscritos no Microsoft Intune.

Pode configurar a Entrust como a autoridade de certificação, ao adicionar uma função de ponto de registo de certificados no Configuration Manager. Ao adicionar um novo perfil de certificado que emite certificados PFX, pode selecionar autoridade de certificação de um Microsoft ou da Entrust.

**Problema conhecido**: No 1706 technical preview, os certificados PFX não são emitidos para autoridades de certificação da Microsoft. Isto não afeta os certificados PFX importados ou perfis de SCEP.


## <a name="cisco-ipsec-support-for-ios-vpn-profiles"></a>Suporte do Cisco (IPsec) para perfis VPN de iOS
<!-- 1321367 -->

Pode criar um iOS perfil da VPN com o Cisco (IPsec) como o tipo de ligação. Para obter mais informações, consulte [criar perfis VPN](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).


## <a name="new-windows-configuration-item-settings"></a>Novas definições de item de configuração do Windows
<!-- 1354715 -->

Nesta versão, adicionámos as seguintes definições novas, que pode usar em itens de configuração do Windows:

### <a name="password"></a>Palavra-passe

- **Encriptação de dispositivos**

### <a name="device"></a>Dispositivo

- **Modificação das definições de região (apenas ambiente de trabalho)**
- **Modificação das definições de energia e suspensão**
- **Modificação de definições de idioma**
- **Modificação da hora do sistema**
- **Modificação do nome do dispositivo**

### <a name="store"></a>Arquivo

- **Atualização automática de aplicações da loja**
- **Utilizar apenas loja privada**
- **Lançamento de aplicação originado pela Store**

### <a name="microsoft-edge"></a>Microsoft Edge

- **Bloquear o acesso a about: flags**
- **Substituição do pedido SmartScreen**
- **Substituição do pedido SmartScreen para ficheiros**
- **Endereço IP de localhost do WebRTC**
- **Motor de busca predefinido**
- **URL XML do OpenSearch**
- **Home Pages (apenas ambiente de trabalho)**

Para obter mais informações sobre as definições de compatibilidade, consulte [garantir a conformidade de dispositivo](/sccm/compliance/understand/ensure-device-compliance).


## <a name="new-device-compliance-policy-rules"></a>Novas regras de política de conformidade de dispositivo

* **Tipo de palavra-passe obrigatório**. Especifique se o utilizador tem de criar uma palavra-passe de alfanumérica ou de uma palavra-passe numérica. Para as palavras-passe de alfanuméricas, também especificar o número mínimo de conjuntos de carateres que a palavra-passe tem de ter. Os quatro conjuntos de carateres são: Letras em minúsculas, letras maiúsculas, símbolos e números.

    **Suportado no:**
    * Windows Phone 8+
    * Windows 8.1+
    * iOS 6+
<br></br>
* **Depuração de USB de bloco no dispositivo**. Não é necessário configurar esta definição, como a depuração USB já se encontra desativada em dispositivos Android para dispositivos de trabalho.

    **Suportado no:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Bloquear aplicações de origens desconhecidas**. Exigir que os dispositivos impeçam a instalação de aplicações de origens desconhecidas. Não tem de configurar esta definição como dispositivos Android for Work restringem sempre a instalação de origens desconhecidas.

    **Suportado no:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Exigir análise de ameaças nas aplicações**. Esta definição especifica que a funcionalidade de aplicações Verifique se está ativada no dispositivo.

    **Suportado no:**
    * Android 4.2 a 4.4 através de
    * Samsung KNOX Standard 4.0+

Ver [criar e implementar uma política de conformidade do dispositivo](https://docs.microsoft.com/sccm/mdm/deploy-use/create-compliance-policy) para experimentar as novas regras de conformidade do dispositivo.

## <a name="new-mobile-application-management-policy-settings"></a>Novas definições de política de gestão de aplicações móveis
A partir desta versão, pode utilizar três novas definições de política do aplicações móveis (MAM) de gestão:

- **Bloquear captura de ecrã (apenas dispositivos Android):** Especifica que as funcionalidades de captura de ecrã do dispositivo estão bloqueadas durante a utilização desta aplicação.

- **Desative sincronização de contactos:** Impede que a aplicação de guardar os dados na aplicação nativa contactos no dispositivo.

- **Desative a impressão:** Impede que a aplicação de trabalho de impressão dados escolares ou profissionais.

Ver [proteger aplicações através de políticas de proteção de aplicações no Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para experimentar as novas definições de política de proteção de aplicações.

## <a name="android-and-ios-enrollment-restrictions"></a>Restrições de inscrição de Android e iOS
<!-- 1290826 --> Começando com esta versão, os administradores podem agora especificar que os utilizadores podem inscrever dispositivos Android ou iOS pessoais nos respetivos ambientes híbridos. Isso permite que limite inscritos dispositivos pré-declarados pretencentes, dispositivos pertencentes à empresa ou dispositivos iOS inscritos com o programa de inscrição de dispositivos apenas.

### <a name="try-it-out"></a>Experimentar
1. Na consola do Configuration Manager, na área de trabalho **Administração** , aceda a **Serviços Cloud** > **Subscrição do Microsoft Intune**.
2. Sobre o **home page** separador a **subscrição** de grupo, selecione **configurar plataformas** e, em seguida, selecione **Android** ou **iOS** .
3. Selecione **bloquear dispositivos pessoais**.

## <a name="android-for-work-application-management-policy-for-copy-paste"></a>Android para a política de gestão de aplicações de trabalho para copiar-colar
Atualizámos as descrições de configuração para Android para trabalho itens de configuração para o **permitir a partilha de dados entre o perfil profissional e pessoal**.

|Antes de pré-visualização técnica 1706 | Novo nome de opção | Comportamento|
|-|-|-|
|Impedir qualquer partilha entre limites| Restrições de partilha predefinidas| Trabalho para pessoal: Predefinição (esperada até ser bloqueado em todas as versões) <br>Pessoal para work: Predefinido (6.x+ permitido, bloqueado no 5.x)|
|Sem restrições|   As aplicações no perfil pessoal podem processar a pedidos de partilha do perfil de trabalho| Trabalho para pessoal: Permitido  <br>Pessoal para work: Permitido|
|As aplicações no perfil de trabalho podem processar pedidos de partilha do perfil pessoal |As aplicações no perfil de trabalho podem processar pedidos de partilha do perfil pessoal |Trabalho para pessoal: Predefinição<br>Pessoal para work: Permitido<br>(Só será útil no 5.x onde pessoal para o trabalho é bloqueado)|

Nenhuma destas opções diretamente impedir comportamento copiar / colar. Adicionámos uma definição personalizada para o serviço e a aplicação Portal da empresa na versão 1704 que pode ser configurado para impedir que copiar-colar. Isto pode ser definido por meio de URI personalizada.

-   OMA-URI:  ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
-   Tipo de valor: Booleano

Configuração DisallowCrossProfileCopyPaste como true impede que o comportamento de copiar / colar entre o Android for Work pessoa e perfis de trabalho.

### <a name="try-it-out"></a>Experimentar
1. Na consola do Configuration Manager, selecione **ativos e compatibilidade** > **descrição geral** > **as definições de compatibilidade**  >  **Itens de configuração**.
2. Escolher **Create** para criar um novo item de configuração e especificar **nome** e **Android for Work**.
3. No dispositivo grupos para configurar a definição, selecione **perfil de trabalho**e escolha **próxima**.
4. Selecione o valor para **permitir a partilha de dados entre perfis pessoais e de trabalho**e, em seguida, conclua o assistente.

## <a name="device-health-attestation-assessment-for-compliance-policies-for-conditional-access"></a>Avaliação de atestado de estado de funcionamento do dispositivo para políticas de conformidade para acesso condicional
<!-- 1097546 --> Começando com esta versão, pode usar o estado de atestado de estado de funcionamento do dispositivo como uma regra de política de conformidade para o acesso condicional aos recursos da empresa.

### <a name="try-it-out"></a>Experimentar
Selecione uma regra de atestado de estado de funcionamento do dispositivo como parte de uma avaliação da política de conformidade.

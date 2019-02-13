---
title: Elevada disponibilidade do servidor do site
titleSuffix: Configuration Manager
description: Como configurar a elevada disponibilidade para o servidor de site do Configuration Manager, adicionando um servidor de site de modo passivo.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: be12cfe29ff470f2f577bab2c685695ae5770bae
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131426"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Site elevada disponibilidade do servidor no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1128774-->

A partir do Configuration Manager versão 1806, elevada disponibilidade para a função de servidor do site é uma solução com base no Configuration Manager para instalar um servidor de sites adicionais na *passivo* modo. O servidor do site em modo passivo além disso é o servidor de site existente que esteja no *Active Directory* modo. Um servidor de site em modo passivo está disponível para uso imediato, quando necessário. Incluir este servidor de sites adicionais como parte de seu design geral para tornar o serviço do Configuration Manager [elevada disponibilidade](/sccm/core/servers/deploy/configure/high-availability-options).  

Um servidor do site em modo passivo:
- Utiliza o mesmo banco de dados do site como seu servidor do site no modo ativo.
- Não escrever dados na base de dados do site quando estiver no modo passivo.
- Utiliza a mesma biblioteca de conteúdos como seu servidor do site no modo ativo.

Para tornar o servidor do site em modo passivo fique ativo, manualmente *promover* -lo. Esta ação muda o servidor do site no modo ativo deve ser o servidor de site em modo passivo. As funções de sistema de sites que estão disponíveis no servidor de modo ativo original permanecem disponíveis, desde que esse computador está acessível. Apenas a função de servidor do site é alternava entre os modos de ativos e passivos.

> [!Note]  
> O Configuration Manager não permite esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para mais informações, consulte [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).



## <a name="prerequisites"></a>Pré-requisitos

- O servidor do site em modo passivo pode estar no local ou com base na cloud no Azure.  
    > [!Note]  
    > Um servidor de site com base na cloud em modo passivo utiliza a infraestrutura do Azure como um serviço (IaaS). Para obter mais informações, veja os artigos seguintes:  
    > - [Máquinas virtuais do Azure (para a infraestrutura baseada na nuvem)](/sccm/core/understand/use-cloud-services#azure-virtual-machines-for-cloud-based-infrastructure)
    > - [Perguntas frequentes para o Configuration Manager no Azure](/sccm/core/understand/configuration-manager-on-azure)  

- Ambos os servidores de site têm de ser associados ao mesmo domínio do Active Directory.  

- O site é um site primário autónomo. 

- Ambos os servidores do site tem de utilizar a mesma base de dados, que tem de ser remota a cada servidor do site.  

     - Ambos a necessidade de servidores de sites **sysadmin** permissões na instância do SQL Server que aloja a base de dados do site.

     - O SQL Server que aloja a base de dados do site pode utilizar uma instância predefinida, instância, nomeada [cluster do SQL Server](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database), ou uma [SQL Server Always On do grupo de disponibilidade](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).  

     - O servidor do site em modo passivo está configurado para utilizar a mesma base de dados do site que o servidor de site no modo ativo. Só lê o servidor do site em modo passivo da base de dados. Não escrever na base de dados até depois que ele é promovido para o modo ativo.  

- A biblioteca de conteúdos do site tem de ser numa partilha de rede remota. Ambos os servidores do site tem permissões de controlo total para a partilha e o respetivo conteúdo. Para obter mais informações, consulte [biblioteca de conteúdos de gerir](/sccm/core/plan-design/hierarchy/the-content-library#manage-content-library).<!--1357525-->  

    - O servidor do site não pode ter a função de ponto de distribuição. O ponto de distribuição também utiliza a biblioteca de conteúdos e esta função não suporta uma biblioteca de conteúdos remota. Depois de mover a biblioteca de conteúdos, não é possível adicionar a função de ponto de distribuição para o servidor do site.  

- O servidor do site em modo passivo:  

     - Tem de cumprir os [pré-requisitos para instalar um site primário](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).  

     - Tem de ter sua conta de computador do grupo de administradores local no servidor do site no modo ativo.<!--516036-->

     - Instalações usando arquivos de origem que correspondem à versão do servidor do site no modo ativo.  

     - Não pode ter uma função de sistema de sites a partir de qualquer site antes de instalar o servidor do site numa função de modo passivo.  

- Ambos os servidores de site podem executar OS diferentes ou versões de service pack, desde que ambos estejam [suportados pelo Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  



## <a name="limitations"></a>Limitações
- Um servidor de site único em modo passivo é suportado em cada site primário.  

- Um servidor de site em modo passivo não é suportado numa hierarquia. Uma hierarquia inclui um site de administração central e um site primário subordinado. Crie apenas um servidor de site em modo passivo num site primário autónomo.<!--1358224-->

- Um servidor de site em modo passivo não é suportado num site secundário.<!--SCCMDocs issue 680-->  

- Promoção do servidor do site em modo passivo para o modo ativo é manual. Não há nenhuma ativação pós-falha automática.  

- Não não possível instalar funções do sistema de sites no novo servidor antes de adicionar o servidor do site em modo passivo.  

    > [!Note]  
    > Após a instalação do servidor do site em modo passivo, pode adicionar funções adicionais conforme necessário. Por exemplo, o fornecedor de SMS ou um ponto de gestão num site primário.  

- Para funções, como o ponto do reporting que utilizam uma base de dados, aloje a base de dados num servidor que seja remoto de ambos os servidores de site.  

- O fornecedor de SMS não for instalado no servidor do site em modo passivo. Ligar a um fornecedor do site para promover manualmente o servidor de site em modo passivo para o modo ativo. Instale, pelo menos, uma instância adicional do fornecedor de noutro servidor. Para obter mais informações, consulte [planear o fornecedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).  

- Consola do Configuration Manager não for instalado automaticamente no servidor do site em modo passivo.  



## <a name="add-a-site-server-in-passive-mode"></a>Adicionar um servidor de site em modo passivo

Para obter mais informações sobre o processo geral da adição de funções, consulte [instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles).

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**, selecione o **Sites** nó e clique em **criar Servidor de sistema do site** na faixa de opções.   

2. Sobre o **gerais** página do Site System Server Assistente para criar, especifique o servidor a alojar o servidor do site em modo passivo. O servidor que especificar não é possível alojar quaisquer funções de sistema de sites antes de instalar um servidor de site em modo passivo.  

3. Sobre o **seleção da função do sistema** , selecione apenas **servidor de Site em modo passivo**.  

    > [!Note]  
    > O assistente efetua as seguintes verificações de pré-requisitos inicial nesta página:  
    > - O servidor selecionado não é um servidor de site secundário
    > - O servidor selecionado não está já um servidor de site em modo passivo
    > - Biblioteca de conteúdos do site estiver numa localização remota  
    >  
    > Se estes pré-requisitos inicial verifica falhar, não é possível continuar após esta página do assistente.  

4. Sobre o **servidor de Site em modo passivo** , indique as informações seguintes, que são utilizadas para executar a configuração e instalar a função de servidor do site no servidor especificado:

     - Escolha uma das seguintes opções:  

         - **Copiar ficheiros de origem de instalação através da rede do servidor do site no modo ativo**: Esta opção cria um pacote compactado e envia-os para o novo servidor do site.  

         - **Utilize os ficheiros de origem disponíveis na seguinte localização no servidor do site em modo passivo**: Por exemplo, um caminho local para a qual já copiados os ficheiros de origem. Certifique-se de que este conteúdo é a mesma versão que o servidor do site no modo ativo.  

         - (*Recomendado*) **utilizar os ficheiros de origem disponíveis na seguinte localização de rede**: Especifique o caminho diretamente para o conteúdo do **CD. Mais recente** pasta do servidor do site no modo ativo. Por exemplo, `\\Server\SMS_ABC\CD.Latest` em que "*Server*" é o nome do servidor do site no modo ativo, e "*ABC*" é o código do site.  

     - Especifique o caminho local no qual pretende instalar o Configuration Manager no novo servidor do site. Por exemplo: `C:\Program Files\Configuration Manager`  

5. Conclua o assistente. Em seguida, o Configuration Manager instala o servidor do site em modo passivo no servidor especificado.

Para o estado de instalação detalhadas, na consola do Ir para o **monitorização** área de trabalho e selecione o **estado do servidor de Site** nó. O estado para o servidor de site em modo passivo indicará **instalando**. Para obter informações mais detalhadas, selecione o servidor e clique em **Mostrar estado**. Esta ação abre a janela de estado de instalação de servidor do Site. Quando o processo estiver concluído, o estado mostra **OK** para ambos os servidores.   

Para obter mais informações sobre o processo de configuração, consulte [fluxograma - configurar um servidor de site em modo passivo](/sccm/core/servers/deploy/configure/passive-site-server-flowchart).

Depois de adicionar um servidor de site em modo passivo, ver ambos os servidores de site no **nós** separador a **Sites** nó da consola. 

Todos os componentes de servidor de site do Configuration Manager estão em modo de espera no servidor do site em modo passivo. Os serviços do Windows ainda estão em execução.



## <a name="site-server-promotion"></a>Promoção de servidor do site  

Da mesma forma, tal como acontece com cópia de segurança e recuperação, planejar e praticar seu processo de alteração de servidores de site. No seu plano de promoção, considere os seguintes pontos:  

- Ponha em prática uma promoção planeada, em que ambos os servidores de site estão online. Também ponha em prática uma ativação pós-falha não planeada, a forçar a desligar ou encerrar o servidor de site no modo ativo.  

- Determine seus processos operacionais durante a ativação pós-falha e o que se comunicar com outros administradores do Configuration Manager.  

- Antes de uma promoção planeada:  

    - Verifique o estado geral do site e componentes do site. Certifique-se de que tudo o que está em bom estado como normal para o seu ambiente.  

    - Verifique o estado do conteúdo para todos os pacotes ativamente replicar entre sites.  

    - Não inicie as tarefas novas de distribuição de conteúdo. 

        > [!Note]  
        > Se a replicação de ficheiros entre sites está em curso durante a ativação pós-falha, o novo servidor de site poderá não receber o arquivo replicado. Se isto acontecer, redistribuir o conteúdo de software após o novo servidor do site está ativo.<!--515436-->  


### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>Processo para promover o servidor de site em modo passivo para o modo ativo

Esta secção descreve como alterar o servidor do site em modo passivo para o modo ativo. Para aceder ao site e efetuar esta alteração, terá de conseguir aceder uma instância do fornecedor de SMS. Para obter mais informações, consulte [utilizar vários fornecedores de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#BKMK_MultiSMSProv).  

> [!Important]  
> Por predefinição, apenas o servidor de site original tem a função de fornecedor de SMS. Se este servidor estiver offline, não é possível ligar ao site que nenhum fornecedor estiver disponível. Ao adicionar o servidor do site em modo passivo, não é adicionado automaticamente o fornecedor de SMS. Adicione pelo menos uma função de fornecedor de SMS adicional para o seu site para um serviço de elevada disponibilidade.  

> [!Tip]  
> Consola do Configuration Manager solicita a lista de fornecedores de SMS disponível do WMI no servidor do site. Ao instalar múltiplos fornecedores de SMS num site, o site atribui aleatoriamente cada novo pedido de ligação para um fornecedor de SMS instalado. Não é possível especificar a localização do fornecedor de SMS a utilizar para uma sessão de ligação específica. Se a consola não consegue ligar ao site porque o servidor de site atual está offline, especifique o servidor do site na janela de ligação de Site.  

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó. Selecione o site e, em seguida, mude para o **nós** separador. Selecione o servidor de site em modo passivo e, em seguida, clique em **promover para ativo** na faixa de opções. Clique em **Sim** para confirmar e continuar.   
  
2. Atualize o nó de consola. O **Status** coluna para o servidor que está a promover exibe na **nós** separador como **promover**.  

3. Após a promoção estiver concluída, o **Status** coluna mostra **OK** para ambos os o novo servidor do site no modo ativo e para o novo servidor de site em modo passivo. O **nome do servidor** coluna para o site agora apresenta o nome do novo servidor do site no modo ativo.

Para o estado detalhado, vá para o **monitorização** área de trabalho e selecione o **estado do servidor de Site** nó. O **modo** coluna identifica qual servidor é *Active* ou *passivo*. Quando promove um servidor de modo passivo para o modo ativo, selecione o servidor de sites que está a promover para ativo e, em seguida, escolha **Mostrar estado** a partir do Friso. Esta ação abre a janela de estado de promoção de servidor do Site que apresenta detalhes adicionais sobre o processo.

Quando um servidor de site no modo ativo muda ao longo de modo passivo, apenas a função de sistema de sites é feita passiva. Todas as outras funções do sistema de site instaladas nesse computador permanecem acessíveis aos clientes e Active Directory.

Para obter mais informações sobre o *planeada* processo de promoção, consulte [fluxograma - promover o servidor do site (planejado)](/sccm/core/servers/deploy/configure/promote-site-server-flowchart).


### <a name="unplanned-failover"></a>Ativação pós-falha não planeada

Se o servidor do site atual no modo ativo estiver offline, o servidor do site para promoção tenta contactar o servidor de site atual no modo ativo durante 30 minutos. Se o servidor offline voltar antes desta data, é notificado com êxito e a alteração continua normalmente. Caso contrário, o servidor do site para promoção atualiza a forçar a configuração do site para que ela seja o Active Directory. Se o servidor offline voltar após esse período, ele primeiro verifica o estado atual da base de dados do site. Em seguida, prossegue com despromover próprio para o servidor do site em modo passivo.

Durante 30 minutos a aguardar período, o site não tem nenhum servidor de site no modo ativo. Os clientes ainda comunicar com funções com clientes como pontos de gestão, pontos de atualização de software e pontos de distribuição. Os utilizadores podem instalar o software que já tenha sido implementado. Administração de sites não é possível neste período de tempo. Para obter mais informações, consulte [impactos de falha do Site](/sccm/core/servers/manage/site-failure-impacts).  

Se o servidor offline está danificado, de modo que ele não é possível retornar, elimine este servidor de site a partir da consola. Em seguida, crie um novo servidor de site em modo passivo para restaurar um serviço de elevada disponibilidade. 

Para obter mais informações sobre o *não planeada* processo de ativação pós-falha, consulte [fluxograma - promover o servidor do site (não planeado)](/sccm/core/servers/deploy/configure/promote-site-server-unplanned-flowchart).


### <a name="additional-tasks-after-site-server-promotion"></a>Tarefas adicionais após a promoção de servidor do site  

Após mudar a servidores de site, não tem de executar a maioria das outras tarefas conforme necessário quando [a recuperar um site](/sccm/core/servers/manage/recover-sites#post-recovery-tasks). Por exemplo, não precisa de reposição de palavras-passe ou voltar a ligar a sua subscrição do Microsoft Intune.

As etapas a seguir poderão ser necessárias se for necessário no seu ambiente:  

- Se importar certificados PKI para pontos de distribuição, importe novamente o certificado para servidores afetados. Para obter mais informações, consulte [gerar novamente os certificados para pontos de distribuição](/sccm/core/servers/manage/recover-sites#regenerate-the-certificates-for-distribution-points).  

- Se integrar o Gestor de configuração com a Microsoft Store para empresas, reconfigure essa ligação. Para obter mais informações, consulte [gerir aplicações a partir da Microsoft Store para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).  



## <a name="daily-monitoring"></a>Monitorização diariamente

Quando tiver um servidor de site em modo passivo, monitorizá-la diariamente. Certifique-se de que o estado permanece OK e está pronto a utilizar. Na consola do Configuration Manager, vá para o **monitorização** área de trabalho e selecione o **estado do servidor de Site** nó. Ver os servidores de site e o respetivo estado atual. Veja também o estado no **administração** área de trabalho. Expanda **configuração do Site**e selecione o **Sites** nó. Selecione o site e, em seguida, mude para o **nós** separador. 

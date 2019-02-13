---
title: Implementar aplicações virtuais App-V
titleSuffix: Configuration Manager
description: Veja as considerações que deve levar em conta quando criar e implementar aplicações virtuais.
ms.date: 03/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ddcad9f2-a542-4079-83ca-007d7cb44995
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b151b93bf0dfa067c2b85860e2c0119922a17cd2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130297"
---
# <a name="deploy-app-v-virtual-applications-with-system-center-configuration-manager"></a>Implementar aplicações virtuais do App-V com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramo atual)*

Quando utilizar o Configuration Manager para gerir aplicações virtuais, beneficia das vantagens seguintes:  

-   Uma infraestrutura de gestão único  

-   Escalabilidade, implementação e funcionalidades de distribuição de conteúdo, como coleções e afinidade dispositivo / utilizador  

-   Funcionalidades de gestão de aplicação avançada  

-   Implementação do sistema operativo, inventário de hardware e software, medição de software e asset intelligence para suportar aplicações virtuais  

Para obter mais informações sobre como criar e sequenciar aplicações com o Microsoft Application Virtualization (App-V), consulte [Application Virtualization](https://technet.microsoft.com/library/cc843848.aspx) na Biblioteca TechNet.  

Para além de outros requisitos do System Center Configuration Manager e procedimentos para criar uma aplicação, deve levar em conta as seguintes considerações ao criar e implementar aplicações virtuais:

-   Para implementar aplicações virtuais em computadores, tem de ter o cliente do Configuration Manager e o cliente de App-V instalado nos seus computadores. Os dispositivos cliente podem incluir computadores de secretária e portáteis e clientes VDI (Infraestrutura de Ambiente de Trabalho Virtual). O software do Configuration Manager e o cliente de App-V funcionam em conjunto para fornecer, localizar e iniciar pacotes de aplicações virtuais. O cliente do Configuration Manager gerencia a entrega de pacotes de aplicações virtuais para o cliente de App-V. O Cliente de App-V executa a aplicação virtual no cliente.  

-   Para implementar uma aplicação virtual, terá de criar primeiro a aplicação virtual utilizando o Sequenciador do Application Virtualization (App-V). O sequenciador monitoriza o processo de instalação e configuração para uma aplicação e regista a informação que é necessária para que a aplicação seja executada num ambiente virtual. Também pode utilizar o sequenciador para definir quais arquivos e configurações aplicáveis a todos os utilizadores e que os usuários de configurações podem personalizar.  

-   Quando sequencia uma aplicação, tem de guardar o pacote para uma localização do Configuration Manager pode aceder. Em seguida, pode criar uma implementação da aplicação que contém esta aplicação virtual.  

-   O Configuration Manager não suporta a utilização da funcionalidade partilhada de cache só de leitura do App-V 4.6.  

-   O Configuration Manager suporta a funcionalidade de Store de conteúdo partilhado no App-V 5.  

-   Quando cria um tipo de implementação para uma aplicação virtual, o Configuration Manager cria o tipo de implementação utilizando o conteúdo do ficheiro de manifesto do aplicativo. Este é um arquivo XML que tem informações sobre a aplicação virtual. Além disso, o Configuration Manager cria requisitos para o tipo de implementação com base no conteúdo do ficheiro App-V. OSD com informações sobre os sistemas operativos suportados para a aplicação virtual.  

-   Para implementar aplicações virtuais no Configuration Manager, computadores cliente têm de ter no mínimo o App-V 4.6 SP1 ou uma versão posterior do cliente instalado.  

-   Antes de poder implementar com êxito aplicações virtuais, tem de atualizar o cliente de App-V com a correção descrita no artigo da Base de dados de conhecimento [2645225](https://support.microsoft.com/kb/2645225).  

-   Quando utiliza grupos de ligação no App-V 5.0, as suas aplicações virtuais implementadas podem partilhar o mesmo sistema de ficheiros e registo nos computadores cliente. Contrariamente às aplicações virtuais padrão, estas aplicações podem partilhar dados entre si. Além disso, os grupos de ligação preservam as definições do utilizador para as aplicações que contêm. Ambientes virtuais App-V no Configuration Manager são utilizados para configurar grupos de ligação em computadores cliente. Os ambientes virtuais são criados ou alterados em computadores cliente quando a aplicação é instalada ou quando os clientes avaliam as aplicações instaladas. Pode atribuir prioridades a estas aplicações para que, quando várias aplicações tentam alterar o valor de um sistema ou registo de ficheiros, tenha precedência a aplicação com a prioridade mais alta. Para obter mais informações, consulte [ambientes virtuais App-V criar](../../apps/deploy-use/create-app-v-virtual-environments.md).  

##  <a name="supported-app-v-versions"></a>Versões suportadas do App-V  
 O Configuration Manager suporta as seguintes versões do App-v:  

-   **App-V 4.6**: Para utilizar aplicações virtuais no Configuration Manager, computadores cliente tem de ter o cliente de App-V 4.6 SP1, App-V 4.6 SP2 ou App-V 4.6 SP3 instalado.  

     Antes de poder implementar com êxito aplicações virtuais, tem também de atualizar o cliente de App-V 4.6 SP1 com a correção descrita no artigo da Base de dados de conhecimento [2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322).  

-   **App-V 5, App-V 5.0 SP1, App-V 5.0 SP2, App-V 5.0 SP3 e App-V 5.1**: Para o App-V 5.0 SP2, tem de instalar [pacote de correções 5](https://support.microsoft.com/en-us/kb/2963211) ou utilizar o App-V 5.0 SP3.  
-   **App-V 5.2**: Isso é incorporado ao Windows 10 Education (1607 e posterior), o Windows 10 Enterprise (1607 e posterior) e o Windows Server 2016.

Para obter mais informações sobre o App-V no Windows 10, consulte os seguintes tópicos:

- [O que há de novo no App-V](https://technet.microsoft.com/itpro/windows/manage/appv-about-appv)
- [Introdução ao App-V para Windows 10](https://technet.microsoft.com/itpro/windows/manage/appv-getting-started)
- [Atualizar para o App-V para Windows 10, de uma instalação existente](https://technet.microsoft.com/itpro/windows/manage/appv-upgrading-to-app-v-for-windows-10-from-an-existing-installation)

##  <a name="steps-to-manage-app-v-virtual-applications"></a>Passos para gerir aplicações virtuais App-V  
 Para gerir aplicações virtuais App-V, siga estes passos:  

1.   **Sequência**: Sequenciamento é o processo de conversão de uma aplicação numa aplicação virtual utilizando o sequenciador do App-V.

2.   **Criar**: Utilize o Assistente para criar tipo de implementação para importar a aplicação sequenciada para um tipo de implementação do Configuration Manager que, em seguida, pode adicionar a uma aplicação. Também pode criar ambientes virtuais que permitam a partilha de definições por várias aplicações virtuais.

3.   **Distribuir**: A distribuição é o processo de disponibilizar aplicações App-V em pontos de distribuição do Configuration Manager.

4.   **Implementar**: Implementação é o processo de disponibilizar a aplicação em computadores cliente. Isso é chamado de publicação e streaming numa infraestrutura completa de App-V.  

##  <a name="configuration-manager-virtual-application-delivery-methods"></a>Métodos de entrega de aplicações virtuais do Configuration Manager  
O Configuration Manager suporta dois métodos de fornecimento de aplicações virtuais aos clientes: transmissão em fluxo de entrega e fornecimento local (transferir e executar).

Ao decidir o método de entrega a utilizar, compare o requisito de espaço em disco reduzida para entrega de transmissão em fluxo com a disponibilidade garantida das aplicações de App-V no fornecimento local. O maior espaço em disco necessário no cliente para a entrega local poderá ser preferível para a transmissão em fluxo da entrega, para que os utilizadores tenham sempre a aplicação disponível a partir de qualquer localização.  

###  <a name="streaming-delivery"></a>Entrega de transmissão em fluxo
Quando utilizar o Configuration Manager para gerir o cliente de App-V, suporta a transmissão em fluxo de aplicações virtuais através de HTTP ou HTTPS a partir de um ponto de distribuição. Transmissão em fluxo por HTTP ou HTTPS está ativada por predefinição e está configurado na caixa de diálogo de propriedades do ponto de distribuição. Quando implementa uma aplicação virtual em computadores cliente e um utilizador executa a aplicação virtual, o cliente do Configuration Manager contacta um ponto de gestão para determinar o ponto de distribuição a utilizar. Em seguida, o aplicativo é transmitido a partir do ponto de distribuição.  

Use as informações desta tabela para ajudar a decidir se a entrega de transmissão em fluxo é o melhor método de entrega para:

|Vantagens|Desvantagens|  
|----------------|-------------------|  
|Este método utiliza protocolos de rede padrão para a transmissão em fluxo de conteúdo de pacotes a partir de pontos de distribuição.<br /><br /> Os atalhos de programa para aplicações virtuais invocam uma ligação ao ponto de distribuição para que o fornecimento da aplicação virtual seja a pedido.<br /><br /> Este método funciona bem para clientes com ligações de banda larga aos pontos de distribuição.<br /><br /> As aplicações virtuais atualizadas distribuídas por toda a empresa são disponibilizadas quando os clientes recebem a política que os informa de que a versão atual foi substituída e os clientes transferem apenas as alterações relativamente à versão anterior.<br /><br /> As permissões de acesso são definidas no ponto de distribuição para impedir que os utilizadores acedam a aplicações ou pacotes não autorizados.|As aplicações virtuais não são transmitidas em fluxo até que o utilizador execute a aplicação pela primeira vez. Neste cenário, um utilizador pode receber atalhos de programa para aplicações virtuais e, em seguida, desligar da rede antes de executar as aplicações virtuais pela primeira vez. Se o utilizador tentar executar a aplicação virtual enquanto o cliente estiver offline, o usuário vê um erro e não é possível executar o aplicativo virtualizado porque um ponto de distribuição do Configuration Manager não está disponível para transmitir o aplicativo. A aplicação não estará disponível até o utilizador voltar a ligar à rede e executar a aplicação.<br /><br /> Para evitar isto, pode utilizar o método de entrega local para entregar aplicações virtuais a clientes ou pode ativar a gestão de clientes baseada na Internet para a entrega por transmissão em fluxo.|  

###  <a name="local-delivery-download-and-execute"></a>Fornecimento local (transferir e executar)  
Transferir e executar é a abordagem mais comum, ao utilizar o Gestor de configuração uma vez que esta abordagem imita de perto como os outros formatos de aplicação são entregues com o Configuration Manager. Quando utiliza o método de entrega local, o cliente do Configuration Manager transfere primeiro o pacote de aplicação virtual completo para a cache de cliente do Configuration Manager. O Gestor de configuração, em seguida, instrui o cliente de App-V para transmitir o aplicativo de cache do Configuration Manager para a cache de App-V. Se implementar uma aplicação virtual em computadores cliente e o respetivo conteúdo não está no cache do App-V, o cliente de App-V transmite o conteúdo da aplicação da cache do cliente do Configuration Manager para a cache de App-V e, em seguida, executa a aplicação. Depois da aplicação é executada com êxito, pode definir o cliente do Configuration Manager para eliminar versões antigas do pacote no próximo ciclo de eliminação ou para as manter na cache do cliente do Configuration Manager. Manter o conteúdo localmente aproveitar as vantagens de entrega de conteúdos do pacote de métodos de otimização, como o BranchCache e PeerCache.

Use as informações desta tabela para ajudar a decidir se o fornecimento local é o melhor método de entrega para:   

|Vantagens|Desvantagens|  
|----------------|-------------------|  
|A funcionalidade de ponto de distribuição padrão é utilizada para transferir o pacote utilizando o Serviço de Transferência Inteligente em Segundo Plano (BITS).<br /><br /> Conteúdo do pacote de aplicação virtual é fornecido localmente ao cliente. Isso significa que os utilizadores podem ser executado-los quando o computador não está ligado à rede.<br /><br /> Este método é adequado para ligações de rede lentas ou pouco fiáveis e para computadores que ligam à rede ocasionalmente.<br /><br /> Configuration Manager utiliza a compressão de diferencial remota (RDC) para enviar aos clientes apenas os bytes dos ficheiros que foram alterados quando o conteúdo do pacote de aplicação virtual é atualizado. O cliente do Configuration Manager utiliza a RDC para criar uma nova versão de um pacote de aplicação virtual com base na versão atual do pacote e nas alterações enviadas ao cliente.<br /><br /> Este método proporciona aplicações resilientes a utilizadores móveis ou utilizadores desligados. Os administradores podem optar por manter o pacote na cache do Configuration Manager após a entrega, se a aplicação virtual tiver sido implementada com uma ação de instalação. O pacote na cache do cliente do Configuration Manager serve como uma origem de transmissão em fluxo local e fiável para o cliente de App-V extraia o pacote para a sua cache.|Espaço em disco que é igual ao dobro do tamanho do pacote de aplicação virtual é necessário no cliente quando a aplicação virtual é mantida na cache do Configuration Manager.|  

###  <a name="deployment-from-an-image"></a>Implementação a partir de uma imagem

Também é possível pré-instalar aplicações virtuais num computador e, em seguida, criar uma imagem desse computador para implementação noutros. Mas se o pacote de aplicação virtual tiver sido criado noutro site, a replicação delta binária não será utilizada para transferir atualizações para a aplicação. Esta opção pode ser útil numa infraestrutura de ambiente de trabalho virtual, quando pretender que as aplicações estejam disponíveis imediatamente em vez de as transferir após o utilizador iniciar sessão.    

##  <a name="migrating-from-an-app-v-infrastructure-to-a-configuration-manager-and-app-v-infrastructure"></a>Migrar de uma infraestrutura de App-V para uma infraestrutura do Configuration Manager e App-V  
Utilize a tabela seguinte para ajudar a planear uma migração de uma infraestrutura de App-V existente para o gerenciamento de aplicativos virtuais com o Configuration Manager.  

|Passo|Mais informações|  
|----------|----------------------|  
|Examine as aplicações virtuais atuais para escolher as aplicações que pretende migrar para a sua infraestrutura do Configuration Manager.|Não existem informações adicionais.|  
|Avaliar os utilizadores e os dispositivos em que as aplicações virtuais serão implementadas.|Crie coleções do Configuration Manager para agrupar os utilizadores e dispositivos para os quais pretende implementar as aplicações virtuais. Ver [introdução às coleções](/sccm/core/clients/manage/collections/introduction-to-collections).|  
|Migre grupos de ligação do App-V 5 para ambientes virtuais do Configuration Manager.|Consulte a [grupos de ligação de migrar o App-V 5 para ambientes virtuais do Configuration Manager](/sccm/apps/get-started/deploying-app-v-virtual-applications#migrate-app-v-5-connection-groups-to-configuration-manager-virtual-environments) deste tópico.|  
|Investigar para descobrir se qualquer uma das suas aplicações virtuais existem como aplicações completas na sua infraestrutura do Configuration Manager.|Para facilitar a gestão, pode adicionar a aplicação virtual como um novo tipo de implementação à aplicação completa existente. Ver [criem aplicativos](../../apps/deploy-use/create-applications.md).|  
|Criar aplicações para substituir os pacotes de App-V existentes.|Ver [introdução à gestão de aplicações](/sccm/apps/understand/introduction-to-application-management) e [criar aplicativos](../../apps/deploy-use/create-applications.md).|  
|O Configuration Manager começa a gerir aplicações virtuais num cliente após a primeira implementação de uma aplicação virtual. Depois disso, o Configuration Manager tem de gerir todas as aplicações de App-V no computador.|Não existem informações adicionais.|  
|Distribuir o conteúdo pelos pontos de distribuição adequados para ativar o fornecimento local de aplicações.|Ver [gerir a infraestrutura de conteúdo e conteúda](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Implemente a aplicação para clientes do Configuration Manager.<br /><br /> Se a aplicação de App-V foi criada com uma versão anterior do sequenciador que não cria um ficheiro de manifesto XML, pode abri-lo e guardá-lo numa versão mais recente do sequencer para criar o ficheiro. Este ficheiro é necessário para implementar aplicações virtuais com o Configuration Manager.<br /><br /> App-V suporta os pacotes de aplicações virtuais que são criados com a versão SoftGrid 4.1 SP1 ou 4.2 do sequencer.<br /><br /> Se as aplicações já tiverem sido instaladas localmente, terá de desinstalá-las antes de implementar uma versão virtual da aplicação.|Ver [implementar aplicações](../../apps/deploy-use/deploy-applications.md).|  
|System Center Configuration Manager já não suporta a utilização de pacotes e programas que contêm aplicações virtuais. Ao migrar para o System Center Configuration Manager do Configuration Manager 2007, o Configuration Manager converte estes pacotes em aplicações.<br /><br /> Anúncios do Configuration Manager 2007 são convertidos nos seguintes tipos de implementação:<br /><br /> – Migração de pacotes de App-V sem anúncio:  Um tipo de implementação que utiliza as predefinições de tipo de implementação.<br /><br /> – Migração de pacotes de App-V com um anúncio: Um tipo de implementação que utiliza as mesmas definições que o <br />                Anúncio do Configuration Manager 2007.<br /><br /> – Migração de pacotes de App-V com vários anúncios: Um tipo de implementação, para cada <br />                Anúncio do Configuration Manager 2007, que utiliza as definições do anúncio respetivo.|Ver [planear a migração de objetos do Configuration Manager para o System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md).|  

##  <a name="migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>Migrar grupos de ligação do App-V 5 para ambientes virtuais do Configuration Manager  
Ambientes virtuais App-V no Configuration Manager permitem às aplicações virtuais que tenha implementado partilhar o mesmo sistema de ficheiros e registo nos computadores cliente. Isto significa que, contrariamente às aplicações virtuais padrão, estas aplicações podem partilhar dados entre si. Os ambientes virtuais são criados ou alterados em computadores cliente quando a aplicação é instalada ou quando os clientes avaliam as aplicações instaladas. Ambientes virtuais são semelhantes aos grupos de ligação no App-V 5 autónomo.  

Quando migrar grupos de ligação do App-V 5 autónomo para ambientes virtuais do Configuration Manager, tem de garantir que o Configuration Manager gere corretamente os grupos de ligação que já existem nos computadores cliente e que o ambiente do utilizador esses grupos de ligação é preservado.  

Para converter grupos de ligação do App-V 5 para ambientes virtuais do Configuration Manager:  

1.  Crie aplicações do Configuration Manager para todas as aplicações que existiam no App-V.  

2.  Implemente as aplicações para utilizadores e dispositivos com um objetivo de implementação de **Necessário**. As implementações para utilizadores tem de ser implementadas para os mesmos utilizadores que utilizaram a aplicação no App-V. As implementações para computadores tem de ser implementadas nos mesmos computadores que tinham a aplicação no App-V.  

3.  Depois de concluída a implementação, crie ambientes virtuais que correspondam aos grupos de ligação publicados no App-V autónomos. O ambiente virtual tem de ter os mesmos pacotes (especificamente, tipos de implementação de App-V 5) na mesma ordem.  

Para obter informações sobre como criar um ambiente virtual de App-V, consulte [como criar ambientes virtuais App-V](../../apps/deploy-use/create-app-v-virtual-environments.md).  

Em alternativa, pode eliminar todos os grupos de ligação do cliente de App-V antes de começar a implementar aplicações com o Configuration Manager. Mas as definições que os utilizadores podem guardar nos grupos de ligação do App-V serão perdidas.  

##  <a name="dynamic-suite-composition-in-app-v-46"></a>Dynamic Suite Composition no App-V 4.6  
Dynamic Suite Composition é uma funcionalidade que permite que defina um pacote de aplicação virtual como tendo uma dependência noutro pacote de aplicação virtual. Quando a aplicação é executada, o Cliente de App-V aloja o pacote primário e o pacote dependente no mesmo ambiente virtual para a aplicação.  

Para poder utilizar esta funcionalidade com o Configuration Manager, ambos os pacotes tem de ser implementados e registados com o cliente de App-V. Para garantir que a conteúdo do pacote dependente é alojado localmente no computador cliente, configurar a implementação da aplicação para entrega local (transferir e executar).  

Para mais informações sobre o Dynamic Suite Composition no App-V, consulte a documentação do App-V.  

##  <a name="converting-app-v-46-applications-to-app-v-5-applications"></a>Converter aplicações App-V 5 em aplicações App-V 4.6  
O formato do pacote de aplicações foi alterado entre App-V 4.6 e App-V 5. As aplicações sequenciadas ao utilizar o App-V 4.6 já não são suportadas. Mas o App-V 5 tem uma ferramenta Conversora de pacotes que pode utilizar para converter aplicações. Para obter mais informações, consulte a [documentação do App-V 5](http://technet.microsoft.com/library/jj713472.aspx).  

Utilize os seguintes passos para converter aplicações App-V 4.6 em aplicações App-V 5:  

1.  Converter ou resequence os pacotes de App-V 4.6 para o formato do App-V 5.  

2.  Implemente o Cliente de App-V 5 em computadores da hierarquia.  

3.  Crie novas aplicações que contêm tipos de implementação para as aplicações App-V 5 e crie regras de substituição para substituir as aplicações 4.6 App-V.  

4.  Crie ambientes virtuais conforme necessário.  

5.  Implemente as novas aplicações App-V 5 nos computadores.  

##  <a name="user-and-deployment-configuration-files"></a>Ficheiros de configuração de utilizador e de implementação  
Ficheiros de configuração de implementação e de utilizador tem as definições que controlam a forma como um aplicativo se comporta. Pode utilizar estes ficheiros para alterar as definições da aplicação sem resequencing o aplicativo.  

Uma aplicação App-V 5 normal pode conter os seguintes ficheiros:  

-   Um ficheiro de pacote (. appv) de aplicação  

-   Um ficheiro de configuração do utilizador  

-   Um ficheiro de configuração de implementação  

O ficheiro de configuração do utilizador tem as definições que se aplicam apenas ao utilizador com sessão iniciada. Pode, por exemplo, editar os ficheiros de configuração para alterar as informações sobre o atalho da aplicação que irá ser implementada para utilizadores. Também pode criar uma aplicação do Configuration Manager com vários tipos de implementação. Cada tipo de implementação pode conter um ficheiro de configuração de utilizador diferente e utilizar regras de requisitos para garantir que estão instalados nos utilizadores relevantes.  

O ficheiro de configuração de implementação tem definições que se aplicam ao computador, como definições de registo. O ficheiro também pode ter definições de utilizador que são aplicadas a todos os utilizadores.  

Se pretender implementar aplicações virtuais do App-V 5 com o Configuration Manager, todos os três arquivos tem de estar presentes na mesma pasta quando criar o tipo de implementação de App-V 5. Se existirem vários ficheiros na pasta, o Configuration Manager irá utilizar o mais recente.  

Para obter mais informações, consulte a [documentação do App-V 5](http://technet.microsoft.com/library/jj713466.aspx).  

##  <a name="app-v-local-interaction"></a>Interação local de App-V  
Em alguns cenários de implementação de aplicação, os aplicativos são instalados localmente nos computadores cliente e outras aplicações são implementadas como aplicações virtuais no mesmo computador cliente. Por predefinição, as aplicações que foram instaladas localmente não conseguem ver nem comunicar diretamente com aplicações virtualizadas. Isso é o comportamento previsto do isolamento de aplicativos que fornece o App-V. Interação local é uma funcionalidade do cliente de App-V que pode ativar para cada aplicação para permitir que aplicativos instalados localmente, que são executados num computador cliente possam ver e comunicar com aplicações virtualizadas. Configuration Manager e App-V suportam totalmente a interação local.  

Para obter mais informações sobre a funcionalidade de interação local de App-V, consulte a documentação do App-V.  

##  <a name="app-v-5-shared-content-store"></a>Store de conteúdo partilhado do App-V 5  
O Configuration Manager suporta a funcionalidade de App-V 5 partilhou conteúdo Store. Para mais informações, consulte [Planear a Loja de Conteúdo Partilhado (SCS) do App-V 5.0](http://technet.microsoft.com/library/jj713431.aspx).  

##  <a name="monitoring-virtual-applications"></a>Monitorizar aplicações virtuais  

### <a name="virtual-application-reports"></a>Relatórios de aplicações virtuais  
Pode utilizar os seguintes relatórios para monitorizar a App-V no seu ambiente do Configuration Manager:  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|Resultados do Ambiente Virtual de App-V|Mostra informações sobre um ambiente virtual selecionado que está num estado especificado para uma coleção selecionada (apenas App-V 5).|  
|Resultados do Ambiente Virtual de App-V Para Ativo|Mostra informações sobre um ambiente virtual selecionado para um ativo especificado e quaisquer tipos de implementação para o ambiente virtual selecionado (apenas App-V 5).|  
|Estado do Ambiente Virtual de App-V|Mostra informações de conformidade para um ambiente virtual selecionado para uma coleção selecionada. O **retidos** coluna este relatório mostra os ativos em que um ambiente virtual que foi anteriormente configurado já não é aplicável, sendo contudo retido para manter as definições de utilizador nas aplicações executadas no ambiente virtual ( Apenas App-V 5).|  
|Computadores com uma aplicação virtual específica|Mostra um resumo de computadores que têm o atalho do App-V especificado que o Application Virtualization Management Sequencer criado (apenas App-V 4.6).|  
|Computadores com um pacote específico de aplicação virtual|Mostra uma lista de computadores com o App-V aplicação pacote especificado instalado (apenas App-V 4.6).|  
|Contar todas as instâncias de pacotes de aplicação virtual|Mostra uma contagem de todos os detetado pacotes de aplicações do App-V (apenas App-V 4.6).|  
|Contar todas as instâncias de aplicações virtuais|Mostra uma contagem de todos os detetadas aplicações de App-V (apenas App-V 4.6).|  

### <a name="log-files"></a>Ficheiros de registo  
O Configuration Manager regista informações sobre implementações de aplicações virtuais nos ficheiros de registo. Para obter informações sobre o registo de ficheiros que aplicativos virtuais e a utilização de gestão de aplicações do Configuration Manager, consulte [ficheiros de registo no System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md).  

Para Windows Vista, Windows 7 e Windows 8, pode encontrar registos para o cliente de App-V no C:\ProgramData\Microsoft\Application Virtualization Client.  

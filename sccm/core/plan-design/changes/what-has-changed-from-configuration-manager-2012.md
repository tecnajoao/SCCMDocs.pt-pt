---
title: 'Alterações do Configuration Manager 2012 '
description: Identifica as alterações e novas capacidades do System Center Configuration Manager em comparação com o System Center 2012 Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a58e5924fc34bad514ca6f01bb23aa84443705c6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="what39s-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>O que&#39;s alteradas no System Center Configuration Manager, do System Center 2012 Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 O ramo atual do System Center Configuration Manager apresenta alterações importantes do System Center 2012 Configuration Manager. Este tópico identifica as alterações significativas e novas capacidades na versão de linha de base 1511 do System Center Configuration Manager. Para saber mais sobre as alterações introduzidas nas atualizações subsequentes do System Center Configuration Manager, consulte [Novidades no System Center Configuration Manager versões incrementais](/sccm/core/plan-design/changes/whats-new-incremental-versions).



 A versão de Dezembro de 2015 do System Center Configuration Manager (versão 1511) estava a edição inicial do produto de Gestor de configuração atual da Microsoft. Normalmente, é referido como ramo atual do System Center Configuration Manager. *O ramo atual* indica que esta é uma versão que suporte atualizações incrementais ao produto. Também fornece uma forma para distinguir entre esta versão e sobre versões anteriores do Configuration Manager.  

 O System Center Configuration Manager:  

-   Não utilize um identificador de ano ou produto no nome do produto, ao contrário das versões anteriores, tais como o Configuration Manager 2007 ou o System Center 2012 Configuration Manager.

-   Suporta atualizações incrementais, no produto, também designado por versões de atualização. A versão inicial tinha a versão 1511. As versões subsequentes são lançadas várias vezes um ano como atualizações na consola, como a versão 1710.
-   É instalado utilizando uma versão de linha de base. Durante a 1511 a versão de linha de base original, linha de base são lançadas novas versões também ocasionalmente, como 1802. Versões de linha de base podem ser utilizadas para instalar um novo site do System Center Configuration Manager e a hierarquia ou para atualizar a partir de uma versão suportada do Configuration Manager 2012.




##  <a name="bkmk_updates"></a> Atualizações na consola para o Configuration Manager  
 O System Center Configuration Manager utiliza um método de manutenção na consola denominado **atualizações e manutenção** que torna mais fácil localizar e instalar atualizações recomendadas.  

 Algumas versões só estão disponíveis como atualizações para sites existentes (de dentro do Gestor de configuração da consola) e não pode ser utilizado para instalar novos sites do Configuration Manager.   
Por exemplo, a atualização 1710 só está disponível a partir da consola do Configuration Manager. É utilizado para atualizar um site que já está a executar uma versão do System Center Configuration Manager.

Periodicamente, uma versão de atualização também for lançada como uma nova versão de linha de base (como a atualização 1802). Este tipo de atualização pode ser utilizado para instalar uma nova hierarquia, sem a necessidade de começar com uma versão mais antiga de linha de base (por exemplo, a versão 1511) e atualizar o caminho para a versão mais atual.


Para obter mais informações sobre como utilizar as atualizações, consulte [atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md).  
Para obter mais informações sobre baslines, consulte [versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions).

##  <a name="bkmk_servicepoint"></a> Nova função de sistema de sites: ponto de ligação de serviço  
 O **conector do Microsoft Intune** é substituído por uma nova função de sistema de sites que ativa funcionalidades adicionais, o **ponto de ligação de serviço**. O ponto de ligação de serviço:  

-   Substitui o conector do Microsoft Intune quando integrar o Intune com a gestão de dispositivos móveis no local do System Center Configuration Manager.  

-   É utilizado como um ponto de contacto para dispositivos que gere.  

-   Carrega dados de utilização sobre a implementação para o serviço de nuvem da Microsoft.  

-   Faz com que as atualizações aplicáveis à sua implementação disponível a partir da consola do Configuration Manager.  

Esta função de sistema de sites suporta os modos online e offline da operação. Para obter mais informações, veja [Sobre o ponto de ligação de serviço no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

##  <a name="bkmk_usage"></a> Recolha de dados de utilização  
 System Center Configuration Manager recolhe dados de utilização sobre os sites e a infraestrutura. Estas informações são compiladas e submetidas para o serviço de nuvem da Microsoft pelo ponto de ligação de serviço. É necessário para ativar a transferir atualizações para a sua implementação, que se aplicam à versão do Configuration Manager utilizar o Configuration Manager. Quando configurar o ponto de ligação de serviço, pode especificar o nível de dados que são recolhidos e se estes são submetidos automaticamente (modo online) ou manualmente (modo offline).  

 Para obter mais informações, consulte [níveis de dados de utilização e definições](../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

##  <a name="bkmk_AMT"></a> Suporte para Active Management Technology (AMT) da Intel  
 Com o System Center Configuration Manager, o suporte nativo para computadores baseados em AMT da consola do Configuration Manager foi removido. Computadores baseados em AMT continuam a ser completamente geridos quando utiliza o [suplemento Intel SCS para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). O suplemento permite que aceder às funcionalidades mais recentes para gerir a AMT, ao remover as limitações introduzidas até que o Configuration Manager pudesse incorporar essas alterações.  

A remoção de AMT integrada para o System Center Configuration Manager inclui a gestão fora de banda. A função de sistema de sites de ponto de gestão fora de banda já não é utilizada nem está disponível.  

Tenha em atenção que a gestão fora de banda no System Center 2012 Configuration Manager não é afetada por esta alteração.

##  <a name="bkmk_out"></a> Funcionalidades preteridas  
 Algumas funcionalidades, como nativo [suporte para Intel Active Management Technology (AMT)](#bkmk_AMT) com base em computadores, são removidas da consola do Configuration Manager. Outras funcionalidades, como a proteção de acesso à rede, foram removidas completamente. Além disso, alguns produtos Microsoft mais antigos como o Windows Vista, Windows Server 2008 e o SQL Server 2008, já não são suportados.  

 Para obter uma lista das funcionalidades preteridas, consulte [removidas e preteridas itens para o System Center Configuration Manager](../../../core/plan-design/changes/deprecated/removed-and-deprecated.md).  

 Para obter detalhes sobre os produtos suportados, sistemas operativos e configurações, consulte [configurações suportadas para o System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md).  

## <a name="client-deployment"></a>Implementação de clientes  
 System Center Configuration Manager apresenta uma nova funcionalidade para testar novas versões de cliente do Configuration Manager antes de atualizar o resto do site com o novo software. Pode configurar uma coleção de pré-produção na qual pode implementar um piloto um novo cliente. Quando estiver satisfeito com o novo software de cliente em pré-produção, pode promover o cliente para atualizar automaticamente o resto do site com a nova versão.  

 Para obter mais informações sobre como testar clientes, consulte [como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

## <a name="operating-system-deployment"></a>Implementação do sistema operativo  

Tenha em atenção as seguintes alterações à implementação de sistema operativo:

-   No Assistente de sequência de tarefas criar, **atualizar um sistema operativo a partir do pacote de atualização**, um novo tipo de sequência de tarefas está disponível. Cria os passos para atualizar computadores a partir do Windows 7, Windows 8 ou Windows 8.1 para o Windows 10. Para obter mais informações, veja [Atualizar o Windows para a versão mais recente com o System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   A Cache Ponto a Ponto do Windows PE está agora disponível quando implementa sistemas operativos. Computadores que executam uma sequência de tarefas para implementar um sistema operativo podem utilizar a Cache do Windows PE para obter conteúdo de um elemento de rede local (uma origem ponto a ponto cache), em vez de transferirem conteúdo de um ponto de distribuição. Isto ajuda a minimizar o tráfego da rede alargada (WAN) em cenários de uma sucursal onde não existe um ponto de distribuição local. Para obter mais informações, veja [Preparar a cache ponto a ponto do Windows PE para reduzir o tráfego WAN no System Center Configuration Manager](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).  

-   Agora, pode ver o estado do Windows como um serviço no seu ambiente. Também pode criar planos de manutenção para anéis de implementação do formulário e certifique-se de que os computadores ramo atuais do Windows 10 são mantidos atualizados quando são lançadas novas compilações. Além disso, pode ver alertas quando os clientes do Windows 10 estiverem prestes o fim de suporte para a respetiva compilação de Current Branch (CB) ou Current Branch for Business (CBB). Para obter mais informações, veja [Gerir o Windows como um serviço com o System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

## <a name="application-management"></a>Gestão de aplicações  

Tenha em atenção as seguintes alterações à gestão de aplicações:

-   O System Center Configuration Manager permite-lhe implementar aplicações da plataforma Universal do Windows (UWP) para dispositivos com Windows 10 e posterior. Veja [Criar aplicações Windows com o System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Centro de software tem um aspeto novo e moderno. As aplicações que antes apenas eram no catálogo de aplicações (aplicações disponíveis ao utilizador) agora apresentadas no Centro de Software no separador aplicações. Isto torna estas implementações mais detetável e torna desnecessário para os utilizadores fazer referência ao catálogo de aplicações. Adicionalmente, já não é necessário um browser com Silverlight. Veja [Planear e configurar a gestão de aplicações no System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   O novo Windows Installer através do tipo de aplicação MDM permite criar e implementar aplicações baseadas no Windows Installer em PCs inscritos que estejam a executar o Windows 10. Veja [Criar aplicações Windows com o System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Quando cria uma aplicação para uma aplicação iOS interna, só tem de especificar o ficheiro de instalador (. IPA) para a aplicação. Já não tem de especificar um ficheiro de lista de propriedades (.plist) correspondente. Veja [Criar aplicações iOS com o System Center Configuration Manager](../../../apps/get-started/creating-ios-applications.md).  

-   No Configuration Manager 2012, para especificar uma ligação para uma aplicação na loja Windows, foi ou especificar a ligação diretamente ou navegar para um computador remoto que tivesse a aplicação instalada. No System Center Configuration Manager, ainda pode introduzir diretamente a ligação, mas agora, em vez de navegar para um computador de referência, pode procurar o arquivo para a aplicação diretamente a partir da consola do Configuration Manager.  

## <a name="software-updates"></a>Atualizações de software  

Tenha em atenção as seguintes alterações para atualizações de software:

-   System Center Configuration Manager pode agora detetar a diferença entre os métodos de gestão de atualização de software para computadores. Especificamente, é capaz de distinguir entre um computador Windows 10 que liga ao Windows Update for Business (WUfB) para a gestão de atualização de software e um computador ligado ao Windows Server Update Services (WSUS) para a gestão de atualização de software. O **UseWUServer** atributo é novo e Especifica se o computador é gerido com o WUfB. Pode utilizar esta definição numa coleção para remover estes computadores da gestão de atualizações de software. Para obter mais informações, veja [Integração com o Windows Update for Business no Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   Agora pode agendar e executar a tarefa de limpeza do WSUS a partir da consola do Configuration Manager. No **componente de ponto de atualização de Software** propriedades, quando seleciona a executar a tarefa de limpeza do WSUS, será executada na próxima sincronização de atualizações de software. O atualizações são definidas para um Estado de recusado no servidor WSUS e o Windows Update Agent nos computadores de software expiradas já não irá analisar estas atualizações de software. Para obter mais informações, veja [Agendar e executar a tarefa de limpeza do WSUS](../../../sum/deploy-use/software-updates-maintenance.md).  

## <a name="compliance-settings"></a>Definições de compatibilidade  

Tenha em atenção as seguintes alterações às definições de conformidade:

-   O System Center Configuration Manager melhora o fluxo de trabalho para a criação de itens de configuração. Agora, quando cria um item de configuração e seleciona as plataformas suportadas, apenas estão disponíveis as definições relevantes para essa plataforma. Veja [Introdução às definições de compatibilidade no System Center Configuration Manager](../../../compliance/get-started/get-started-with-compliance-settings.md).  

-   O **Criar Item de configuração** assistente agora torna mais fácil escolher o tipo de item de configuração que pretende criar. Além disso, estão disponíveis itens de configuração novos e atualizados para:  

    -   Dispositivos do Windows 10 geridos com o cliente do Configuration Manager.  

    -   Dispositivos do Mac OS X geridos com o cliente do Configuration Manager.  

    -   Ambiente de trabalho e o servidor de computadores Windows geridos com o cliente do Configuration Manager.  

    -   Dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do Configuration Manager.  

    -   Dispositivos Windows Phone geridos sem o cliente do Configuration Manager.  

    -   dispositivos iOS e Mac OS X geridos sem o cliente do Configuration Manager.  

    -   Android e Samsung KNOX Standard dispositivos geridos sem o cliente do Configuration Manager.  

 Veja [Como criar itens de configuração no System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items.md).  

-   Suporte para gerir definições nos computadores de Mac OS X que são inscritos com o Microsoft Intune ou geridos com o cliente do Configuration Manager. Veja [Como criar itens de configuração para os dispositivos iOS e Mac OS X geridos sem o cliente System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md).  

## <a name="protect-data-and-site-infrastructure"></a>Proteger os dados e a infraestrutura do site  
System Center Configuration Manager permite-lhe integrar com o Windows Hello para empresas (anteriormente o Microsoft Passport for Work). Windows Hello para empresas é um início de sessão método alternativo que utiliza o Active Directory ou uma conta do Azure Active Directory, para substituir uma palavra-passe, um smart card ou um smart card virtual em dispositivos com Windows 10. Veja [Definições do Windows Hello para Empresas no System Center Configuration Manager](../../../protect/deploy-use/windows-hello-for-business-settings.md).

## <a name="mobile-device-management-with-microsoft-intune"></a>Gestão de dispositivos móveis com o Microsoft Intune  
 O System Center Configuration Manager apresenta melhoramentos à experiência de gestão de dispositivos móveis, incluindo:  

-   Colocar um limite no número de dispositivos um utilizador pode inscrever.  

-   Especificar termos e condições de utilizadores do Portal da empresa têm de aceitar antes de poderem inscrever ou utilizar a aplicação.  

-   Adicionar uma função de Gestor de inscrição de dispositivos para ajudar a gerir um grande número de dispositivos.  

Para obter mais informações sobre as capacidades de gestão de dispositivos móveis com o Configuration Manager e o Intune, consulte [gestão híbrida de dispositivos móveis (MDM) com o System Center Configuration Manager e o Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

## <a name="on-premises-mobile-device-management"></a>Gestão de Dispositivos Móveis no Local  
 Agora pode gerir dispositivos móveis ao utilizar a infraestrutura do Configuration Manager no local. Todos os dados de gestão e gestão de dispositivos é processados no local e não faz parte do Microsoft Intune ou outros serviços em nuvem. Este tipo de gestão de dispositivos não requer o software de cliente. Gestor de configuração gere dispositivos com as capacidades incorporadas em sistemas de operativos de dispositivos.  

 Para obter mais informações, consulte [gerir dispositivos móveis com a infraestrutura no local no System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

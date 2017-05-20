---
title: "As alterações a partir do Configuration Manager 2012 | Documentos do Microsoft "
description: "Identifica as alterações e as novas funcionalidades do System Center Configuration Manager em comparação com o System Center 2012 Configuration Manager."
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
caps.latest.revision: 51
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 90775fcf2549080a43e9c1606caa79d9eb90a89c
ms.openlocfilehash: 0a3eb93a99533a1569d8f72ca01d6dfcdc75da20
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="what39s-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>O que &#39; s mudou no System Center Configuration Manager, a partir do System Center 2012 Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 O ramo atual do System Center Configuration Manager apresenta alterações importantes a partir do System Center 2012 Configuration Manager. Este tópico identifica as alterações significativas e novas capacidades de encontrar na versão de linha de base 1511 do System Center Configuration Manager. Para saber mais sobre as alterações introduzidas no atualizações subsequentes para o System Center Configuration Manager, consulte o artigo [o que há de novo no System Center Configuration Manager versões incrementais](/sccm/core/plan-design/changes/whats-new-incremental-versions).



 A versão de Dezembro de 2015 do System Center Configuration Manager (versão 1511) estava a edição inicial do produto do Configuration Manager atual da Microsoft. Este é normalmente denominado como ramo atual do System Center Configuration Manager. *Ramo atual* indica esta é uma versão que suporte atualizações incrementais para o produto. Fornece também uma forma de distinguir entre esta versão e versões anteriores do Configuration Manager.  

 O System Center Configuration Manager:  

-   Não utilize um identificador de ano ou produto no nome do produto, ao contrário das versões anteriores, tais como do Configuration Manager 2007 ou o System Center 2012 Configuration Manager.

-   Suporta atualizações incrementais, no produto, também designado por versões de atualização. A edição inicial foi versão 1511. Versões subsequentes são lançadas várias vezes um ano como atualizações de na consola, como versão 1610.
-   É instalado utilizando uma versão de linha de base. Enquanto 1511 estava a versão original do plano base, o novas versões de linha de base também são lançadas ocasionalmente, como 1702. Versões de linha de base podem ser utilizadas para instalar um novo site do System Center Configuration Manager e da hierarquia ou para atualizar a partir de uma versão suportada do Configuration Manager 2012.




##  <a name="bkmk_updates"></a> Atualizações na consola para o Configuration Manager  
 System Center Configuration Manager utiliza um método de serviço na consola denominado **atualizações e a manutenção** que torna mais fácil localizar e instalar as atualizações recomendadas.  

 Algumas versões só estão disponíveis como atualizações para sites existentes (a partir do Gestor de configuração da consola) e não pode ser utilizado para instalar novos sites do Configuration Manager.   
Por exemplo, a atualização 1610 só está disponível a partir da consola do Configuration Manager. É utilizado para atualizar um site que já é executada uma versão do System Center Configuration Manager.

Periodicamente, também for lançada uma versão de atualização como uma nova versão do plano base (como atualizar 1702). Este tipo de atualização pode ser utilizado para instalar uma nova hierarquia, sem ser necessário para iniciar com uma versão antiga do plano base (como 1511) e atualizar a sua forma para a versão mais atual.


Para obter mais informações sobre a utilização de atualizações, consulte o artigo [atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md).  
Para mais informações sobre baslines, consulte o artigo [versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions).

##  <a name="bkmk_servicepoint"></a>Nova função de sistema de sites: ponto de ligação de serviço  
 O **conector do Microsoft Intune** é substituído por uma nova função de sistema de sites que ativa a funcionalidade adicional, o **ponto de ligação de serviço**. O ponto de ligação de serviço:  

-   Substitui o conector do Microsoft Intune quando integrar o Intune com a gestão de dispositivos móveis no local System Center Configuration Manager.  

-   É utilizado como um ponto de contacto para dispositivos que gere.  

-   Carregamentos de dados de utilização sobre a implementação para o serviço de nuvem da Microsoft.  

-   Faz com que as atualizações aplicáveis à sua implementação disponível a partir da consola do Configuration Manager.  

Esta função do sistema de sites suporta online e offline modos de funcionamento. Para obter mais informações, veja [Sobre o ponto de ligação de serviço no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

##  <a name="bkmk_usage"></a> Recolha de dados de utilização  
 System Center Configuration Manager recolhe dados de utilização sobre os sites e a infraestrutura. Esta informação é compilada e submetida para o serviço de nuvem Microsoft pelo ponto de ligação de serviço. É necessário para permitir a transferência de atualizações para a implementação que se aplicam para a versão do Configuration Manager utilizar o Configuration Manager. Quando configurar o ponto de ligação de serviço, pode especificar ambos o nível de dados que são recolhidos e se esta é submetida automaticamente (modo online) ou manualmente (modo offline).  

 Para obter mais informações, consulte o artigo [níveis de dados de utilização e definições](../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

##  <a name="bkmk_AMT"></a> Suporte para Active Management Technology (AMT) da Intel  
 Com o System Center Configuration Manager, suporte nativo para computadores baseados em AMT a partir da consola do Configuration Manager foi removido. Computadores baseados em AMT continuam a ser completamente geridos quando utiliza o [Intel SCS suplemento para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). O suplemento lhe fornece que acesso às funcionalidades mais recentes para gerir AMT, ao remover limitações introduzidas até que o Configuration Manager foi possível incorporar essas alterações.  

A remoção das integrada AMT para o System Center Configuration Manager inclui a gestão fora de banda. A função de sistema de sites de ponto de gestão fora de banda já não está a ser utilizado, nem disponível.  

Tenha em atenção que a gestão fora de banda no System Center 2012 Configuration Manager não é afetada por esta alteração.

##  <a name="bkmk_out"></a> Funcionalidades preteridas  
 Algumas funcionalidades, como nativo [suporte para AMT Intel Active Management Technology ()](#bkmk_AMT) em computadores, são removidos da consola do Configuration Manager. Outras funcionalidades, como a proteção de acesso à rede, são removidas completamente. Além disso, alguns produtos Microsoft mais antigos como o Windows Vista, Windows Server 2008 e o SQL Server 2008, já não são suportados.  

 Para obter uma lista de funcionalidades preteridas, consulte o artigo [Removed e funcionalidades preteridas para o System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

 Para obter detalhes sobre os produtos suportados, sistemas operativos e configurações, consulte o artigo [configurações suportadas para o System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md).  

## <a name="client-deployment"></a>Implementação de clientes  
 System Center Configuration Manager apresenta uma nova funcionalidade para novas versões de cliente do Configuration Manager antes de atualizar o resto do site com o novo software de teste. Pode configurar uma coleção de pré-produção em que a implementação piloto um novo cliente. Assim que estiver satisfeito com o novo software de cliente na pré-produção, pode promover o cliente atualizar automaticamente o resto do site com a nova versão.  

 Para obter mais informações sobre como testar os clientes, consulte o artigo [como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

## <a name="operating-system-deployment"></a>Implementação do sistema operativo  

Tenha em atenção as seguintes alterações à implementação do sistema operativo:

-   No Assistente de sequência de tarefas criar, **atualizar um sistema operativo a partir do pacote de atualização**, um novo tipo de sequência de tarefas está disponível. Cria os passos para atualizar computadores a partir do Windows 7, Windows 8 ou Windows 8.1, Windows 10. Para obter mais informações, veja [Atualizar o Windows para a versão mais recente com o System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   A Cache Ponto a Ponto do Windows PE está agora disponível quando implementa sistemas operativos. Os computadores que executam uma sequência de tarefas para implementar um sistema operativo podem utilizar a Cache de elemento de rede do Windows PE para obter conteúdos a partir de um elemento da rede local (um elemento de rede cache origem), em vez de transferir conteúdo a partir de um ponto de distribuição. Isto ajuda a minimizar o tráfego da rede alargada (WAN) em cenários de uma sucursal onde não existe um ponto de distribuição local. Para obter mais informações, veja [Preparar a cache ponto a ponto do Windows PE para reduzir o tráfego WAN no System Center Configuration Manager](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).  

-   Agora pode ver o estado do Windows como um serviço no seu ambiente. Também pode criar o plano de manutenção para anéis de implementação do formulário e garantir que os computadores da sucursal atuais do Windows 10 são atualizados quando são lançadas compilações de novo. Além disso, pode ver os alertas quando os clientes Windows 10 são perto do fim do suporte para as respetivas compilação do ramo atual (CB) ou ramo atual para empresas (CBB). Para obter mais informações, veja [Gerir o Windows como um serviço com o System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

## <a name="application-management"></a>Gestão de aplicações  

Tenha em atenção as seguintes alterações à gestão de aplicações:

-   System Center Configuration Manager permite-lhe implementar aplicações de plataforma de Windows Universal (UWP) dispositivos que executam o Windows 10 e posterior. Veja [Criar aplicações Windows com o System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Centro de software tem um aspeto moderno e novo. As aplicações que anteriormente apenas aparecem no catálogo de aplicações (aplicações disponíveis para o utilizador) agora são apresentados no Centro de Software em separador de aplicações. Isto torna estas implementações mais detetável e torna desnecessárias para os utilizadores para se referir ao catálogo de aplicações. Adicionalmente, já não é necessário um browser com Silverlight. Veja [Planear e configurar a gestão de aplicações no System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   O novo Windows Installer através do tipo de aplicação MDM permite criar e implementar aplicações baseadas no Windows Installer em PCs inscritos que estejam a executar o Windows 10. Veja [Criar aplicações Windows com o System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Quando cria uma aplicação para uma aplicação iOS internas, só tem de especificar o ficheiro de instalador (. IPA) para a aplicação. Já não tem de especificar um ficheiro de lista de propriedades (.plist) correspondente. Veja [Criar aplicações iOS com o System Center Configuration Manager](../../../apps/get-started/creating-ios-applications.md).  

-   No Configuration Manager 2012, para especificar uma ligação para uma aplicação na loja Windows, pode especificar a ligação diretamente ou procurar num computador remoto que tinham a aplicação instalada. No System Center Configuration Manager, ainda pode introduzir diretamente na ligação, mas agora, em vez de navegar para um computador de referência, pode procurar o arquivo para a aplicação diretamente a partir da consola do Configuration Manager.  

## <a name="software-updates"></a>Atualizações de software  

Tenha em atenção as seguintes alterações às atualizações de software:

-   System Center Configuration Manager consegue atualmente detetar a diferença entre os métodos de gestão de atualização de software para computadores. Especificamente, pode distinguir entre um computador com Windows 10 que liga ao Windows Update para empresas (WUfB) para a gestão de atualização de software e um computador está ligado ao Windows Server Update Services (WSUS) para a gestão de atualização de software. O **UseWUServer** atributo é novo e Especifica se o computador for gerido com WUfB. Pode utilizar esta definição numa coleção para remover estes computadores da gestão de atualizações de software. Para obter mais informações, veja [Integração com o Windows Update for Business no Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   Agora pode agendar e executar a tarefa de limpeza WSUS a partir da consola do Configuration Manager. No **componente de ponto de atualização de Software** propriedades, ao selecionar para executar a tarefa de limpeza do WSUS, será executada na próxima sincronização de atualizações de software. O atualizações são definidas para um Estado de recusou-se no servidor WSUS e o Windows Update Agent nos computadores de software expiradas já não analisarão a estas atualizações de software. Para obter mais informações, veja [Agendar e executar a tarefa de limpeza do WSUS](../../../sum/deploy-use/software-updates-maintenance.md).  

## <a name="compliance-settings"></a>Definições de compatibilidade  

Tenha em atenção as seguintes alterações para as definições de compatibilidade:

-   System Center Configuration Manager melhora o fluxo de trabalho para criar itens de configuração. Agora, quando cria um item de configuração e seleciona as plataformas suportadas, apenas estão disponíveis as definições relevantes para essa plataforma. Veja [Introdução às definições de compatibilidade no System Center Configuration Manager](../../../compliance/get-started/get-started-with-compliance-settings.md).  

-   O **Criar Item de configuração** assistente agora torna mais fácil escolher o tipo de item de configuração que pretende criar. Além disso, estão disponíveis itens de configuração novos e atualizados para:  

    -   Dispositivos Windows 10 geridos com o cliente do Configuration Manager.  

    -   Dispositivos de Mac OS X geridos com o cliente do Configuration Manager.  

    -   Ambiente de trabalho e o servidor de computadores Windows geridos com o cliente do Configuration Manager.  

    -   Dispositivos Windows 8.1 e Windows 10 geridos sem cliente do Configuration Manager.  

    -   Dispositivos Windows Phone geridos sem cliente do Configuration Manager.  

    -   Mac OS X dispositivos iOS e geridos sem cliente do Configuration Manager.  

    -   Android e Samsung KNOX Standard dispositivos geridos sem cliente do Configuration Manager.  

 Veja [Como criar itens de configuração no System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items.md).  

-   Suporte para gerir definições nos computadores de Mac OS X que ambos estão inscritos com o Microsoft Intune ou geridos com o cliente do Configuration Manager. Veja [Como criar itens de configuração para os dispositivos iOS e Mac OS X geridos sem o cliente System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md).  

## <a name="protect-data-and-site-infrastructure"></a>Proteger os dados e a infraestrutura do site  
System Center Configuration Manager permite-lhe integrar com o Windows Hello para empresas (anteriormente o Microsoft Passport para trabalhar). Windows Hello para empresas é um início de sessão do método alternativo que utiliza o Active Directory ou uma conta do Azure Active Directory, para substituir uma palavra-passe, smart card ou smart card virtual em dispositivos com o Windows 10. Veja [Definições do Windows Hello para Empresas no System Center Configuration Manager](../../../protect/deploy-use/windows-hello-for-business-settings.md).

## <a name="mobile-device-management-with-microsoft-intune"></a>Gestão de dispositivos móveis com o Microsoft Intune  
 System Center Configuration Manager apresenta melhoramentos à experiência de gestão de dispositivos móveis, incluindo:  

-   Colocar um limite no número de dispositivos um utilizador pode inscrever.  

-   Especificar os utilizadores de termos e condições do Portal da empresa tem de aceitar antes de serem podem inscrever ou utilizar a aplicação.  

-   Adicionar uma função de Gestor de inscrição de dispositivos para ajudar a gerir um grande número de dispositivos.  

Para mais informações sobre funcionalidades de gestão de dispositivos móveis com o Configuration Manager e o Intune, consulte o artigo [gestão de dispositivos móveis (MDM) híbrida com o System Center Configuration Manager e o Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

## <a name="on-premises-mobile-device-management"></a>Gestão de Dispositivos Móveis no Local  
 Já pode gerir dispositivos móveis utilizando a infraestrutura do Configuration Manager no local. Todos os dados de gestão e gestão de dispositivos são processado no local, e não faz parte do Microsoft Intune ou outros serviços em nuvem. Este tipo de gestão de dispositivos não necessita de software de cliente. O Configuration Manager gere dispositivos com capacidades que são criadas para os sistemas operativos de dispositivo.  

 Para obter mais informações, consulte o artigo [gerir dispositivos móveis com a infraestrutura no local no System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).


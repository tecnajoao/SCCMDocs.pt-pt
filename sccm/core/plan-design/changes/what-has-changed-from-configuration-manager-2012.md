---
title: Alterações a partir do Configuration Manager 2012
description: Identifica as alterações e novos recursos do System Center Configuration Manager em comparação com o System Center 2012 Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bd275406a95507441e6b60167c7658a7c5dfccf9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136369"
---
# <a name="whats-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>Alterações no System Center Configuration Manager em relação ao System Center 2012 Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O current branch do Configuration Manager introduz alterações importantes em relação ao System Center 2012 Configuration Manager. Este artigo identifica alterações significativas e novas capacidades encontradas na versão de linha de base 1511 do System Center Configuration Manager. Para saber mais sobre as alterações introduzidas nas atualizações subsequentes para o System Center Configuration Manager, veja [quais são as novidades nas versões incrementais do System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).

A versão de Dezembro de 2015 do System Center Configuration Manager (versão 1511) estava na versão inicial do produto do Configuration Manager atual da Microsoft. Normalmente, é referido como ramo atual do System Center Configuration Manager. *Ramo atual* indica esta versão suporta atualizações incrementais ao produto. Ele também fornece uma forma de distinguir entre esta versão e versões anteriores do Configuration Manager.  

System Center Configuration Manager:  

- Não usa um identificador de ano ou produto no nome do produto, ao contrário das versões anteriores, como o Configuration Manager 2007 ou o System Center 2012 Configuration Manager.  

- Suporta atualizações incrementais, no produto, também designadas por versões de atualização. A versão inicial foi a versão 1511. Versões subsequentes são lançadas várias vezes ao ano como atualizações na consola, como a versão 1710.  

- É instalado com uma versão de linha de base. Durante a versão 1511 a versão de linha de base original, o novas versões de linha de base também são lançadas periodicamente, como 1802. Versões de linha de base podem ser utilizadas para instalar um novo site do System Center Configuration Manager e da hierarquia ou para atualizar a partir de uma versão suportada do Configuration Manager 2012.  



##  <a name="bkmk_updates"></a> Atualizações na consola para o Configuration Manager  

O System Center Configuration Manager utiliza um método de manutenção na consola denominado **atualizações e manutenção** torna mais fácil de localizar e instalar atualizações recomendadas.  

Algumas versões só estão disponíveis como atualizações para sites existentes (dentro do Configuration Manager consola) e não pode ser utilizado para instalar novos sites do Configuration Manager. Por exemplo, a atualização 1710 só está disponível a partir da consola do Configuration Manager. Ele é usado para atualizar um site que já executa uma versão do System Center Configuration Manager.

Periodicamente, uma versão de atualização também é lançada como uma nova versão de linha de base (como a atualização 1802). Esse tipo de atualização pode ser utilizado para instalar uma nova hierarquia, sem a necessidade de começar com uma versão de linha de base mais antiga (como a versão 1511) e atualizar o seu caminho para a versão mais atual.


Para obter mais informações sobre a utilização de atualizações, consulte [atualizações do Configuration Manager](/sccm/core/servers/manage/updates).  
Para obter mais informações sobre linhas de base, consulte [versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions).



##  <a name="bkmk_servicepoint"></a> Nova função de sistema de sites: ponto de ligação de serviço  

O **conector do Microsoft Intune** é substituído por uma nova função de sistema de sites que ativa funcionalidades adicionais, o **ponto de ligação de serviço**. O ponto de ligação de serviço:  

- Substitui o conector do Microsoft Intune quando integrar o Intune com a gestão de dispositivos móveis do System Center Configuration Manager no local.  

- É utilizado como um ponto de contato para dispositivos que gere.  

- Carrega dados de utilização sobre a implementação para o serviço cloud da Microsoft.  

- Disponibiliza atualizações que se aplicam à sua implementação disponível a partir da consola do Configuration Manager.  

Esta função de sistema de sites suporta tanto online quanto offline modos de operação. Para obter mais informações, consulte [sobre o ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point).  



##  <a name="bkmk_usage"></a> Recolha de dados de utilização  

O Configuration Manager recolhe dados de utilização sobre os sites e a infraestrutura. Estas informações são compiladas e submetidas para o serviço cloud da Microsoft pelo ponto de ligação de serviço. É obrigatório para ativar o Gestor de configuração para transferir atualizações para a sua implementação, que se aplicam para a versão do Configuration Manager que utilizar. Quando configurar o ponto de ligação de serviço, pode especificar o nível de dados que são recolhidos e se os dados são submetidos automaticamente (modo online) ou manualmente (modo offline).  

Para obter mais informações, consulte [diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  



##  <a name="bkmk_AMT"></a> Suporte para Active Management Technology (AMT) da Intel  

Ramo atual do Gestor de configuração remove o suporte nativo para computadores baseados em AMT partir da consola do Configuration Manager. Computadores baseados em AMT continuam a ser completamente geridos quando utiliza a [suplemento Intel SCS para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). O suplemento permite que aceder às funcionalidades mais recentes para gerir a AMT, ao mesmo tempo que elimina as limitações introduzidas até que o Configuration Manager pudesse incorporar essas alterações.  

A remoção da AMT integrada para o Configuration Manager inclui a gestão fora de banda. A função de sistema de sites de ponto de gestão fora de banda já não está disponível.  

> [!Note]   
> Gestão fora de banda no System Center 2012 Configuration Manager não é afetada por esta alteração.  



##  <a name="bkmk_out"></a> Funcionalidades preteridas  

Algumas funcionalidades, como nativo [suporte para Intel Active Management Technology (AMT)](#bkmk_AMT) computadores baseados em, são removidas da consola do Configuration Manager. Outros recursos, como proteção de acesso à rede, foram removidos por completo. Além disso, alguns produtos Microsoft mais antigos, como o Windows Vista, Windows Server 2008 e SQL Server 2008, já não são suportados.  

Para obter uma lista das funcionalidades preteridas, consulte [removidas e preteridas itens](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).  

Para obter detalhes sobre os produtos suportados, sistemas operativos e configurações, consulte [configurações suportadas](/sccm/core/plan-design/configs/supported-configurations).  



## <a name="client-deployment"></a>Implementação de clientes  

O Configuration Manager apresenta uma nova funcionalidade para testar novas versões de cliente do Configuration Manager antes de atualizar o resto do site com o novo software. Pode configurar uma coleção de pré-produção na qual vai criar um piloto de um novo cliente. Quando estiver satisfeito com o novo software de cliente em pré-produção, pode promover o cliente para atualizar automaticamente o resto do site com a nova versão.  

Para obter mais informações sobre como testar clientes, consulte [como testar as atualizações de cliente numa coleção de pré-produção](/sccm/core/clients/manage/upgrade/test-client-upgrades).  



## <a name="os-deployment"></a>Implementação de SO  

Tenha em atenção as seguintes alterações para a implantação de sistemas operacionais:

- No Assistente de sequência de tarefas criar, um novo tipo de sequência de tarefas está disponível: **Atualizar um sistema operativo a partir do pacote de atualização**. Ele cria os passos para atualizar computadores a partir do Windows 7, Windows 8 ou Windows 8.1 para o Windows 10. Para obter mais informações, consulte [atualizar o Windows para a versão mais recente](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version).  

- Cache de ponto a ponto do Windows PE está agora disponível ao implementar sistemas operativos. Computadores que executam uma sequência de tarefas para implementar um sistema operacional podem utilizar a cache de ponto a ponto do Windows PE para obter conteúdo de uma origem de cache ponto a ponto, em vez de transferirem conteúdo de um ponto de distribuição. Este comportamento ajuda a minimizar a WAN de tráfego em cenários de sucursais onde não existe nenhum ponto de distribuição local. Para obter mais informações, consulte [cache ponto a ponto de preparar o Windows PE para reduzir o tráfego WAN](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).  

- Agora pode ver o estado do Windows como um serviço no seu ambiente. Também pode criar planos de manutenção para formar anéis de implementação e certifique-se de que computadores do Windows 10 current branch são mantidas atualizadas quando são lançadas novas compilações. Além disso, pode ver alertas quando os clientes do Windows 10 estão perto do fim do suporte para a respetiva compilação. Para obter mais informações, consulte [gerir o Windows como um serviço](/sccm/osd/deploy-use/manage-windows-as-a-service).  



## <a name="application-management"></a>Gestão de aplicações  

Tenha em atenção as seguintes alterações à gestão de aplicações:

- O Configuration Manager permite-lhe implementar aplicações de plataforma Universal do Windows (UWP) para dispositivos com Windows 10 e posterior. Para obter mais informações, consulte [aplicativos Windows criar](/sccm/apps/get-started/creating-windows-applications).  

- Centro de software tem um aspeto novo e moderno. Aplicações disponíveis ao utilizador que antes apenas eram no catálogo de aplicações agora aparecem no Centro de Software no separador aplicações. Esse comportamento faz com que estas implementações mais detectáveis e torna desnecessária para os utilizadores fazer referência ao catálogo de aplicações. Além disso, já não é necessário um browser com capacidade para Silverlight. Para obter mais informações, consulte [planear e configurar a gestão de aplicações](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

- O novo Windows Installer através do tipo de aplicação MDM permite criar e implementar aplicações baseadas no Windows Installer em PCs inscritos que estejam a executar o Windows 10. Para obter mais informações, consulte [aplicativos Windows criar](/sccm/apps/get-started/creating-windows-applications).  

- Quando cria uma aplicação para uma aplicação iOS interna, só tem de especificar o ficheiro de instalador (. IPA) para a aplicação. Já não tem de especificar um ficheiro de lista de propriedades (.plist) correspondente. Ver [criar aplicações iOS](/sccm/apps/get-started/creating-ios-applications).  

- No Configuration Manager 2012, para especificar uma ligação para uma aplicação da Windows Store, poderia ou especificar a ligação diretamente ou navegar para um computador remoto que tivesse a aplicação instalada. No ramo atual do Configuration Manager, ainda pode introduzir diretamente a ligação, mas agora, em vez de navegar para um computador de referência, pode procurar na loja para a aplicação diretamente a partir da consola do Configuration Manager.  



## <a name="software-updates"></a>Atualizações de software  

Tenha em atenção as seguintes alterações às atualizações de software:

- O Configuration Manager agora pode detetar a diferença entre métodos de gestão de atualização de software para computadores. Especificamente, ele é capaz de distinguir entre um computador Windows 10 que liga ao Windows Update for Business (WUfB) e um computador ligados ao WSUS. O **UseWUServer** atributo é novo e Especifica se o computador é gerido com o WUfB. Pode utilizar esta definição numa coleção para remover estes computadores da gestão de atualizações de software. Para obter mais informações, veja [Integration with Windows Update for Business in Windows 10 (Integração com o Windows Update for Business no Windows 10)](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10).  

- Agora pode agendar e executar a tarefa de limpeza WSUS a partir da consola do Configuration Manager. Na **componente de ponto de atualização de Software** propriedades, quando optar por executar a tarefa de limpeza do WSUS, ele é executado na próxima sincronização de atualizações de software. O software expiradas que atualizações estão definidas para um Estado de recusado no servidor do WSUS e o Windows Update Agent nos computadores já não verifica estas atualizações de software. Para obter mais informações, veja [Agendar e executar a tarefa de limpeza do WSUS](/sccm/sum/deploy-use/software-updates-maintenance).  



## <a name="compliance-settings"></a>Definições de compatibilidade  

Tenha em atenção as seguintes alterações às definições de conformidade:

- Gestor de configuração melhora o fluxo de trabalho para a criação de itens de configuração. Agora, quando cria um item de configuração e seleciona as plataformas suportadas, apenas estão disponíveis as definições relevantes para essa plataforma. Ver [introdução às definições de conformidade](/sccm/compliance/get-started/get-started-with-compliance-settings).  

- O **Criar Item de configuração** assistente agora torna mais fácil escolher o tipo de item de configuração que pretende criar. Além disso, estão disponíveis itens de configuração novos e atualizados para:  

    - Dispositivos Windows 10 geridos com o cliente do Configuration Manager  

    - Dispositivos Mac OS X geridos com o cliente do Configuration Manager  

    - Computadores de secretária e servidor do Windows geridos com o cliente do Configuration Manager  

    - Dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do Configuration Manager  

    - Dispositivos Windows Phone geridos sem o cliente do Configuration Manager  

    - dispositivos iOS e Mac OS X geridos sem o cliente do Configuration Manager  

    - Android e Samsung KNOX Standard dispositivos geridos sem o cliente do Configuration Manager  
  
    Para obter mais informações, consulte [como criar itens de configuração](/sccm/compliance/deploy-use/create-configuration-items).  

- Suporte para gerir definições nos computadores de Mac OS X que são inscritos com o Microsoft Intune ou geridos com o cliente do Configuration Manager. Ver [como criar itens de configuração para iOS e dispositivos Mac OS X geridos sem o cliente de Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client).  



## <a name="on-premises-mobile-device-management"></a>Gestão de dispositivos móveis no local  

Agora pode gerir dispositivos móveis ao utilizar a infraestrutura do Configuration Manager no local. Todos os dados de gestão de dispositivos e são processados no local e não faz parte do Microsoft Intune ou outros serviços em nuvem. Este tipo de gestão de dispositivos não requer o software de cliente. O Configuration Manager gere dispositivos com a funcionalidade que está incorporada no SO do dispositivo.  

Para obter mais informações, consulte [gerir dispositivos móveis com a infraestrutura no local](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).

---
title: Novidades na versão 1806
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas funcionalidades introduzidas na versão 1806 do Configuration Manager current branch.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cb0d5d1982bb0b109b83f30f1101ddd50316d53e
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55073038"
---
# <a name="whats-new-in-version-1806-of-configuration-manager-current-branch"></a>O que há de novo na versão 1806 do Configuration Manager current branch

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Atualize 1806 para o ramo atual do Configuration Manager está disponível como uma atualização na consola. Aplica esta atualização de sites que executam a versão 1706, 1710 ou 1802. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

Reveja sempre a lista de verificação mais recente para instalar esta atualização. Para obter mais informações, consulte [lista de verificação para a instalação de atualização 1806](/sccm/core/servers/manage/checklist-for-installing-update-1806). Depois de atualizar um site, reveja também os [lista de verificação de pós-atualização](/sccm/core/servers/manage/checklist-for-installing-update-1806#post-update-checklist).

<!--
> [!Important]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
-->

As secções seguintes fornecem detalhes sobre as alterações e novos recursos na versão 1806 do Configuration Manager current branch.  



## <a name="deprecated-features-and-operating-systems"></a>Funcionalidades preteridas e sistemas operativos

Saiba mais sobre as alterações de suporte antes de eles são implementados no [removidas e preteridas itens](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

A partir de 14 de Agosto de 2018, a funcionalidade de gestão de dispositivos móveis híbrida foi preterida. Para obter mais informações, consulte [o que é a MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  

<!--
Version 1806 drops support for the following products:
-->



## <a name="site-infrastructure"></a>Infraestrutura do site

### <a name="cmpivot"></a>CMPivot
<!--1358456--> O Configuration Manager sempre forneceu um armazenamento centralizado grandes de dados de dispositivo, que os clientes utilizam para fins de relatórios. O site recolhe, normalmente, estes dados numa base semanal. CMPivot é um novo utilitário de na consola, que agora fornece acesso ao Estado em tempo real de dispositivos no seu ambiente. Ele imediatamente, executa uma consulta em todos os dispositivos atualmente ligados na coleção de destino e retorna os resultados. Pode, em seguida, filtrar e agrupar estes dados na ferramenta. Ao fornecer dados em tempo real de clientes online, pode mais rapidamente responder às perguntas sobre, resolver problemas e responder a incidentes de segurança. 

Para obter mais informações, consulte [CMPivot](/sccm/core/servers/manage/cmpivot).  


### <a name="site-server-high-availability"></a>Elevada disponibilidade do servidor do site
<!--1128774--> Elevada disponibilidade para uma função de servidor do site primário autónomo é uma solução com base no Configuration Manager para instalar um servidor de sites adicionais em modo passivo. É o servidor do site em modo passivo, além de seu servidor de site existente que está no modo ativo. Um servidor de site em modo passivo está disponível para uso imediato, quando necessário. 

Para obter mais informações, veja os artigos seguintes: 
- [Elevada disponibilidade do servidor do site](/sccm/core/servers/deploy/configure/site-server-high-availability) 
- [Fluxograma - configurar um servidor de site em modo passivo](/sccm/core/servers/deploy/configure/passive-site-server-flowchart)
- [Fluxograma – Promover o servidor do site (planeado)](/sccm/core/servers/deploy/configure/promote-site-server-flowchart)
- [Fluxograma – Promover o servidor do site (não planeado)](/sccm/core/servers/deploy/configure/promote-site-server-unplanned-flowchart)


### <a name="improvements-to-management-insights"></a>Melhorias às informações de gestão
Esta versão inclui as seguintes melhorias às informações de gestão:  

- Algumas informações de gestão tem agora a opção de adotar uma ação. Esta ação está navegando até o nó associado na consola ou que mostra uma vista baseada em consulta filtrada.<!--1357930-->  

- Um novo grupo para manutenção pró-ativa está disponível com seis novas regras, que ajudam a realçar potenciais problemas de configuração para evitar por meio de conservação regular.<!--1352184-->  

Para obter mais informações, consulte [informações de gestão](/sccm/core/servers/manage/management-insights).


### <a name="configuration-manager-tools"></a>Ferramentas do Configuration Manager
<!--1357145--> As ferramentas de servidor e cliente do Configuration Manager agora estão incluídas no servidor. Encontrá-los no `CD.Latest\SMSSETUP\Tools` pasta no servidor do site. Não são necessárias mais necessária a instalação. 

Para obter mais informações, consulte [ferramentas do Configuration Manager](/sccm/core/support/tools).


### <a name="exclude-active-directory-containers-from-discovery"></a>Excluir contentores do Active Directory da deteção
<!--1358143--> Para reduzir o número de objetos detetados, exclua contentores específicos de deteção de sistemas do Active Directory. 

Para obter mais informações, consulte [configurar a deteção de sistema do Active Directory](/sccm/core/servers/deploy/configure/configure-discovery-methods#bkmk_config-adsd).



## <a name="content-management"></a>Gerenciamento de conteúdo

### <a name="configure-a-remote-content-library-for-the-site-server"></a>Configurar uma biblioteca de conteúdos remota para o servidor do site
<!--1357525--> Para configurar a elevada de disponibilidade no servidor do site ou para libertar espaço no disco rígido no seu administração central ou servidores de site primário, reposicionar a biblioteca de conteúdos para outra localização de armazenamento. Mova a biblioteca de conteúdos para outra unidade no servidor do site, um servidor separado ou discos tolerante a falhas na rede de armazenamento (SAN). 

Para obter mais informações, veja os artigos seguintes: 
- [A biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/the-content-library)
- [Fluxograma – Gerir a biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/manage-content-library-flowchart)


### <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Suporte de ponto de distribuição de nuvem para o Azure Resource Manager
<!--1322209--> Ao criar um ponto de distribuição de nuvem, o assistente fornece agora a opção para criar uma **do Azure Resource Manager deployment**. O Azure Resource Manager é uma plataforma moderna para o gerenciamento de todos os recursos de solução como uma única entidade, chamada de um grupo de recursos. Ao implementar um ponto de distribuição de nuvem com o Azure Resource Manager, o site utiliza o Azure Active Directory para autenticar e criar os recursos da cloud necessários. Esta implementação reestruturação não exige o certificado de gestão clássico do Azure. 

A documentação de funcionalidades para o ponto de distribuição de nuvem também é revista e avançada. Para obter mais informações, veja os artigos seguintes:
- [Utilizar um ponto de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)   
- [Instalar um ponto de distribuição de nuvem](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)  


### <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Distribuição de extração os pontos de distribuição da nuvem de suporte de pontos como origem  
<!--1321554--> Muitos clientes utilizam pontos de distribuição de extração no remoto ou filiais, o que transferir conteúdo de um ponto de distribuição de origem na WAN. Se seus escritórios remotos tem uma ligação melhor para a internet ou para reduzir a carga de seus links WAN, agora pode utilizar um ponto de distribuição de nuvem no Microsoft Azure como origem. Ao adicionar uma origem no **ponto de distribuição de extração** separador Propriedades do ponto de distribuição, qualquer ponto de distribuição de nuvem no site é agora listado como um ponto de distribuição disponíveis. O comportamento de ambas as funções de sistema de sites permanece o mesmo caso contrário. 

Para obter mais informações, consulte [utilizar pontos de distribuição de extração](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).


### <a name="enable-distribution-points-to-use-network-congestion-control"></a>Ativar pontos de distribuição para utilizar o controlo de congestionamento de rede
<!--1358112--> Windows baixa Extra atraso em segundo plano transporte (LEDBAT) é uma funcionalidade do Windows Server para o ajudar a gerir as transferências de rede em segundo plano. Para pontos de distribuição em execução em versões suportadas do Windows Server, ative uma opção para o ajudar a ajustar o tráfego de rede. Os clientes utilizam apenas a largura de banda de rede quando estiver disponível. 

Para obter mais informações, consulte [Windows LEDBAT](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#windows-ledbat).


### <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Suporte de transferência parcial na cache de elemento de rede de cliente para reduzir a utilização de WAN
<!--1357346--> Origens de cache ponto a ponto do cliente agora podem dividir o conteúdo em partes. Estas peças minimizam a transferência de rede para reduzir a utilização da WAN. O ponto de gestão fornece controlo mais detalhado das partes de conteúdo. Ele tenta eliminar mais do que uma transferência do conteúdo do mesmo por grupo de limites. 

Para obter mais informações, consulte [suporte de transferência parcial](/sccm/core/plan-design/hierarchy/client-peer-cache#bkmk_parts). 


### <a name="boundary-group-options-for-peer-downloads"></a>Opções de grupos de limites para configurar o peering downloads
<!--1356193--> Agora, os grupos de limites incluem definições adicionais para lhe dar mais controle sobre a distribuição de conteúdo no seu ambiente. Esta versão adiciona as seguintes opções:  

- **Permitir transferências de ponto a ponto neste grupo de limites**: O ponto de gestão fornece aos clientes uma lista de localizações de conteúdo que inclui a origens de ponto a ponto. Esta definição também afeta a aplicar os IDs de grupo para a otimização de entrega.  

- **Durante downloads de ponto a ponto, utilize apenas colegas dentro da mesma sub-rede**: O ponto de gestão inclui apenas as origens de mesmo nível de lista de localização de conteúdo que estão na mesma sub-rede que o cliente.  

Para obter mais informações, consulte [opções de grupos de limites para as transferências de ponto a ponto](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions).


### <a name="improvement-to-peer-cache-source-location-status"></a>Melhoria para o estado de localização de origem de cache ponto a ponto
<!--SCCMDocs issue 850--> O Configuration Manager é mais eficiente para determinar se tem a ganhar mobilidade uma origem de cache ponto a ponto para outra localização. Esse comportamento faz-se de que o ponto de gestão oferece-la como uma origem de conteúdo aos clientes na nova localização e não a localização antiga. Se estiver a utilizar a funcionalidade de cache ponto a ponto com roaming origens da cache ponto a ponto, depois de atualizar o site para a versão 1806, também Atualize todas as origens de cache ponto a ponto para a versão mais recente do cliente. O ponto de gestão não inclui estas origens de cache ponto a ponto na lista de localizações de conteúdo antes de serem actualizadas para, pelo menos, versão 1806.

Para obter mais informações, consulte [os requisitos para a cache ponto a ponto](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements).



<!-- ## Migration  -->



## <a name="client-management"></a>Gestão de clientes

### <a name="improvement-to-client-push-security"></a>Melhoria de segurança de push de cliente
<!--1358204--> Ao usar o método de push de cliente de instalar o cliente do Configuration Manager, o site agora pode exigir a autenticação mútua do Kerberos. Esta melhoria ajuda a proteger a comunicação entre o servidor e o cliente. 

Para obter mais informações, consulte [como instalar clientes com a instalação push do cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).


### <a name="bkmk_ehttp"></a> Sistema de sites HTTP avançado
<!--1356889,1358228--> Utilizar a comunicação HTTPS é recomendada para todos os caminhos de comunicação do Configuration Manager, mas pode ser um desafio para alguns clientes devido à sobrecarga de gerenciamento de certificados PKI. A introdução do Azure Active Directory integration (Azure AD) reduz alguns, mas nem todos os requisitos de certificado. 

Esta versão inclui melhoramentos para a forma como os clientes comunicam com sistemas de sites. Nas propriedades de sites, **comunicação do computador cliente** separador, selecione a opção para **HTTPS ou HTTP**e, em seguida, ative a nova opção para **certificados gerados utilize o Gestor de configuração sistemas de sites para HTTP**. Esta funcionalidade é uma [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features).

Para obter mais informações, consulte [avançada HTTP](/sccm/core/plan-design/hierarchy/enhanced-http).


### <a name="azure-ad-device-identity"></a>Identidade de dispositivo do Azure AD 
<!--1358460--> Uma [Azure AD associado](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices) ou [dispositivo do Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices) sem um Azure AD utilizador com sessão iniciada pode comunicar de forma segura com o respetivo site atribuído. A identidade de dispositivo com base na cloud agora é suficiente para se autenticar com o ponto de gestão e CMG.  

Para obter mais informações, consulte [avançada HTTP](/sccm/core/plan-design/hierarchy/enhanced-http).


### <a name="cmtrace-installed-with-client"></a>CMTrace instalado com o cliente
<!--1357971--> Agora, o ferramenta de visualização de registos de CMTrace é instalado automaticamente, juntamente com o cliente do Configuration Manager. Este é adicionado ao diretório de instalação do cliente, que, por predefinição, é `%WinDir%\ccm\cmtrace.exe`. 

Para obter mais informações, consulte [CMTrace](/sccm/core/support/cmtrace).


### <a name="cloud-management-dashboard"></a>Dashboard de gestão da cloud
<!--1358461--> O novo dashboard de gestão de cloud fornece uma visão centralizada para utilização de gateway (CMG) de gestão na cloud. Quando o site está integrado com o Azure AD, também apresenta dados sobre os utilizadores da nuvem e dispositivos.   

Esta funcionalidade também inclui a **analisador de ligação do CMG** para a verificação em tempo real ajudar a resolução de problemas. O utilitário na consola verifica o estado atual do serviço e o canal de comunicação através da ligação do CMG aponte para pontos de gestão que permitam o tráfego CMG. 

Para obter mais informações, consulte as secções seguintes a [Monitor CMG](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway) artigo:  
- [Dashboard de gestão da cloud](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway#cloud-management-dashboard)  
- [Analisador da ligação](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway#connection-analyzer)  


### <a name="improvements-to-cloud-management-gateway"></a>Melhorias para a cloud do gateway de gestão

Versão 1806 inclui os seguintes aprimoramentos para o gateway de gestão da cloud (CMG):

#### <a name="simplified-client-bootstrap-command-line"></a>Linha de comando de arranque de configuração simplificada do cliente
<!--1358215--> Ao instalar o cliente do Configuration Manager na internet através de um CMG, da linha de comandos agora necessita de menos propriedades. Esta melhoria reduz o tamanho da linha de comandos utilizada no Microsoft Intune ao se preparar para a cogestão. 

Para obter mais informações, consulte [como preparar os dispositivos baseados na internet para a cogestão](/sccm/comanage/how-to-prepare-win10#install-the-configuration-manager-client).

#### <a name="download-content-from-a-cmg"></a>Transferir conteúdo de um CMG
<!--1358651--> Anteriormente, era necessário implementar um ponto de distribuição de nuvem e CMG como funções separadas. Um CMG também agora pode servir conteúdo aos clientes. Esta funcionalidade reduz os certificados necessários e o custo das VMs do Azure. 

Para obter mais informações, consulte [modificar um CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).

#### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Certificado de raiz fidedigna não é necessário com o Azure AD
<!--503899--> Quando cria um CMG, já não tem de fornecer um [certificado de raiz fidedigna](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-trusted-root-certificate-to-clients) na página Definições. Este certificado não necessárias ao utilizar o Azure Active Directory (Azure AD) para autenticação de cliente, mas utilizado para ser necessário no assistente. Se estiver a utilizar certificados de autenticação de cliente PKI, em seguida, ainda tem de adicionar um certificado de raiz fidedigna para CMG.



## <a name="co-management"></a>Cogestão

### <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Política MDM de sincronização do Microsoft Intune para um dispositivo cogerido
<!--1357377--> Quando alterna uma carga de trabalho de cogestão, os dispositivos cogeridos sincronizar automaticamente políticas MDM do Microsoft Intune. Esta sincronização ocorre também quando inicia o **transferir política do computador** ação de notificações do cliente na consola do Configuration Manager. 

Para obter mais informações, consulte [como mudar cargas de trabalho do Configuration Manager para o Intune](/sccm/comanage/how-to-switch-workloads).


### <a name="transition-new-workloads-to-intune-using-co-management"></a>Transição novas cargas de trabalho para o Intune através de cogestão
As seguintes cargas de trabalho podem agora fazer a transição do Configuration Manager para o Intune depois de ativar a cogestão:  

- **Configuração do dispositivo**<!--1357903-->: Esta carga de trabalho permite-lhe utilizar o Intune para implementar políticas MDM, enquanto continua a utilizar o Configuration Manager para implantar aplicativos.  

- **Office 365**<!--1357841-->: Os dispositivos não instalar do Office 365 implementações do Configuration Manager.  

- **Aplicações móveis**<!--1357892-->: Todas as aplicações disponíveis implementadas a partir do Intune estão disponíveis no Portal da empresa. Aplicações que implementa a partir do Configuration Manager estão disponíveis no Centro de Software. Esta funcionalidade é uma [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  

Para fazer a transição estas cargas de trabalho, vá para a página de propriedades de cogestão e mova a barra de controlo de deslize de carga de trabalho do Configuration Manager para **piloto** ou **todos os**. 

Para obter mais informações, consulte [cogestão para dispositivos Windows 10](/sccm/comanage/overview).


### <a name="support-for-multiple-hierarchies-to-one-intune-tenant"></a>Suporte para várias hierarquias para um inquilino do Intune
<!--1357944--> Alguns clientes têm várias hierarquias do Configuration Manager e pretendem consolidar no futuro para um único inquilino para o Azure Active Directory e o Microsoft Intune. Cogestão agora oferece suporte a ligar mais de um ambiente do Configuration Manager ao mesmo inquilino do Intune.

Para obter mais informações, consulte [pré-requisitos de cogestão](/sccm/comanage/overview#prerequisites).
 


## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Configurar as definições do Windows Defender SmartScreen para o Microsoft Edge
<!--1353701--> A política de definições de conformidade do Microsoft Edge browser adiciona as seguintes três definições para o Windows Defender SmartScreen: 
- Permite ao SmartScreen
- Os utilizadores podem substituir a linha de comandos do SmartScreen para sites
- Os utilizadores podem substituir a linha de comandos do SmartScreen para ficheiros

Para obter mais informações, consulte [definições de configurar o Microsoft Edge](/sccm/compliance/deploy-use/browser-profiles).


### <a name="scap-extensions"></a>Extensões SCAP
<!--1357552--> Converter os conteúdos de conteúdo automatização SCAP (Security Protocol) para linhas de base de definições de conformidade e gerar relatórios SCAP com uma extensão da consola. Esta funcionalidade também inclui um novo dashboard para visualizar a conformidade do cliente, bem como a conformidade de regra XCCDF. 

Para obter mais informações, consulte [extensões sobre SCAP](/sccm/compliance/plan-design/scap/about-scap).



## <a name="application-management"></a>Gestão de aplicações

### <a name="phased-deployment-of-applications"></a>Implementação faseada de aplicações
<!--1358147--> Crie uma implementação faseada para uma aplicação. As implementações faseadas permitem-lhe organizar uma implementação coordenada e sequenciada de software com base em critérios personalizáveis e grupos. Por exemplo, implementar a aplicação para uma coleção piloto e, em seguida, continuar automaticamente a implementação com base nos critérios de sucesso. 

Para obter mais informações, veja os artigos seguintes:  

- [Criar uma implementação faseada](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Gerir e monitorizar as implementações faseadas](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  


### <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Aprovisionar os pacotes de aplicações do Windows para todos os utilizadores num dispositivo
<!--1358310--> Aprovisione uma aplicação com um pacote de aplicação do Windows para todos os utilizadores do dispositivo. Um exemplo comum deste cenário é aprovisionar uma aplicação a partir da Microsoft Store para empresas e educação, como o Minecraft: Edição de educação, para todos os dispositivos utilizados pelos alunos de uma instituição de ensino. Anteriormente, o Configuration Manager apenas suportada a instalar estas aplicações por utilizador. Depois de iniciar sessão para um novo dispositivo, um estudante teria de espera para aceder a uma aplicação. Agora, quando a aplicação é aprovisionada no dispositivo para todos os utilizadores, eles podem ser produtivos mais rapidamente. 

Para obter mais informações, consulte [aplicativos Windows criar](/sccm/apps/get-started/creating-windows-applications#bkmk_provision).


### <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integração de ferramenta de personalização do Office com o instalador do Office 365
<!--1358149--> A ferramenta de personalização do Office está agora integrada com o instalador do Office 365 na consola do Configuration Manager. Ao criar uma implementação para o Office 365, configure de forma dinâmica as definições de capacidade de gestão mais recentes do Office. Quando eles lançar novas compilações do Office 365 a Microsoft atualiza a ferramenta de personalização do Office. Esta integração permite-lhe tirar partido das novas definições de capacidade de gerenciamento no Office 365, assim que eles estão disponíveis. 

Para obter mais informações, consulte [aplicações do Office 365/implementar](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps).


### <a name="support-for-new-windows-app-package-formats"></a>Suporte para novos formatos de pacote de aplicação Windows
<!--1357427--> O Configuration Manager suporta agora a implementação de novo pacote de aplicação do Windows 10 (.msix) e formatos de pacote (.msixbundle) da aplicação. 

Para obter mais informações, consulte [aplicativos Windows criar](/sccm/apps/get-started/creating-windows-applications#bkmk_general).


### <a name="uninstall-application-on-approval-revocation"></a>Desinstalar a aplicação mediante a revogação de aprovação
<!--1357891--> Esse comportamento foi alterado quando revogar a aprovação de um aplicativo. Agora quando negar o pedido para a aplicação, o cliente desinstala a aplicação do dispositivo do utilizador. Esse comportamento requer que ative a [funcionalidade opcional](https://docs.microsoft.com/en-us/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **aprovar pedidos de aplicações para utilizadores por dispositivo**. 

Para obter mais informações, consulte [implementar aplicações](/sccm/apps/deploy-use/deploy-applications#bkmk_approval).


### <a name="package-conversion-manager"></a>Gestor de conversão de pacotes 
<!--1357861--> Gestor de conversão de pacotes agora é uma ferramenta integrada que lhe permite converter pacotes de legado para o Configuration Manager aplicativos do ramo atual. Em seguida, pode utilizar funcionalidades de aplicativos, como dependências, regras de requisitos e afinidade dispositivo / utilizador.

Para obter mais informações, consulte [Package Conversion Manager](/sccm/apps/pcm/package-conversion-manager).



## <a name="os-deployment"></a>Implementação de SO

### <a name="improvements-to-phased-deployments"></a>Melhorias para as implementações faseadas

Esta versão inclui as seguintes melhorias para as implementações faseadas:  

#### <a name="create-a-phased-deployment-with-manually-configured-phases"></a>Criar uma implementação faseada com fases configurados manualmente
<!--1358148--> Para uma sequência de tarefas, agora de configurar manualmente as fases ao criar uma implementação faseada. Adicionar fases adicionais até 10 do **fases** separador do Assistente para criar implementação por fases. Ainda automaticamente pode criar uma implementação de duas fases predefinida. 

Para obter mais informações, consulte [criar uma implementação faseada com fases configurados manualmente](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence#bkmk_manual).

#### <a name="phased-deployment-status"></a>Estado de implementação por fases
<!--1358577--> As implementações faseadas agora tem uma experiência de monitorização nativa. Do **implementações** nó a **monitorização** área de trabalho, selecione uma implementação faseada e, em seguida, clique em **estado da implementação por fases** na faixa de opções. 

Para obter mais informações, consulte [gerir e monitorizar implementações de faseada](/sccm/osd/deploy-use/manage-monitor-phased-deployments).  

#### <a name="gradual-rollout-during-phased-deployments"></a>Implementação gradual durante as implementações faseadas
<!--1358578--> Durante uma implementação faseada, a implementação de cada fase pode agora acontecer gradualmente. Este comportamento ajuda a mitigar o risco de problemas de implantação e diminui a carga na rede causada pela distribuição de conteúdo aos clientes. O site pode gradualmente disponibilizar o software dependendo da configuração para cada fase. Todos os clientes numa fase têm um prazo em relação ao tempo que o software é disponibilizado. A janela de tempo entre o tempo disponível e o prazo é o mesmo para todos os clientes numa fase. 

Para obter mais informações, consulte [fase definições](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence#bkmk_settings).  


### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Melhoramentos à sequência de tarefas de atualização in-loco do Windows 10
<!--1358500--> O modelo de sequência de tarefas padrão para a atualização in-loco do Windows 10 inclui, agora, outro grupo novo com as ações recomendadas para adicionar no caso do processo de atualização falha. Estas ações facilitam a resolução de problemas. Uma dessas ferramentas é o Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). É uma ferramenta de diagnóstico de autónomo para obter detalhes sobre o motivo pelo qual uma atualização do Windows 10 foi concluída com êxito. 

Para obter mais informações, consulte [criar uma sequência de tarefas para atualizar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-on-failure).


### <a name="improvements-to-pxe-enabled-distribution-points"></a>Melhorias aos pontos de distribuição com PXE ativado
<!--1357580--> Sobre o **PXE** separador de propriedades do ponto de distribuição, verificação **ativar um dispositivo de resposta PXE sem o serviço de implementação do Windows**. Esta nova opção permite que um dispositivo de resposta do PXE no ponto de distribuição, o que não exige o Windows Deployment Services (WDS). Uma vez que o WDS não é necessário, o ponto de distribuição com PXE ativado pode ser um cliente ou servidor de sistema operacional, incluindo o Windows Server Core. Este novo serviço de resposta do PXE oferece suporte ao IPv6 e também melhora a flexibilidade de pontos de distribuição com PXE ativado em escritórios remotos. 

Para obter mais informações, consulte [ativar o PXE no ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).


### <a name="network-access-account-not-required-for-some-scenarios"></a>Conta de acesso de rede não é necessária para alguns cenários
<!--1358278,1358279--> O [sistema de sites HTTP avançada](#bkmk_ehttp) funcionalidade também remove algumas dependências na conta de acesso de rede. Quando ativa a nova opção de site para **sistemas de sites de certificados gerados pelo utilize o Gestor de configuração para HTTP**, os seguintes cenários não precisam de uma conta de acesso de rede para transferir o conteúdo de um ponto de distribuição:  

- Sequências de tarefas em execução a partir do suporte de dados ou PXE
- Sequências de tarefas em execução a partir do Centro de Software  

Estas sequências de tarefas podem ser para a implementação do sistema operacional ou personalizado. Também é suportada para computadores de grupo de trabalho.

Para obter mais informações, consulte [sequências de tarefas e a rede aceder à conta](/sccm/osd/plan-design/planning-considerations-for-automating-tasks#BKMK_TSNetworkAccessAccount).


### <a name="other-improvements-to-os-deployment"></a>Outras melhorias para implementação do SO

#### <a name="mask-sensitive-data-stored-in-task-sequence-variables"></a>Mascarar dados confidenciais armazenados em variáveis de sequência de tarefas
 <!--1358330--> Na **Set Task Sequence Variable** passo, selecione a opção nova para **não apresentar este valor**. 

 Para obter mais informações, consulte [Set Task Sequence Variable](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable). 

#### <a name="mask-program-name-during-run-command-step-of-a-task-sequence"></a>Nome do programa de máscara durante a executar o comando passo de sequência de tarefas
 <!--1358493--> Para impedir que os dados potencialmente confidenciais sejam apresentadas ou com sessão iniciada, a configurar a variável de sequência de tarefas **OSDDoNotLogCommand**.  

 Para obter mais informações, consulte [variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#OSDDoNotLogCommand). 

#### <a name="task-sequence-variable-for-dism-parameters-when-installing-drivers"></a>Variável de sequência de tarefas para os parâmetros do DISM ao instalar controladores
 <!--516679/2840016--> Para especificar parâmetros de linha de comandos adicionais para o DISM, utilize a nova variável de sequência de tarefas **OSDInstallDriversAdditionalOptions**. 

 Para obter mais informações, consulte [variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#OSDInstallDriversAdditionalOptions). 

#### <a name="option-to-use-full-disk-encryption"></a>Opção para utilizar a encriptação de disco completa
 <!--SCCMDocs-pr issue 2671--> Tanto o **ativar BitLocker** e **provisão prévia do BitLocker** passos agora incluem uma opção para **utilizar encriptação de disco completa**. Por predefinição, estes passos criptografar o espaço utilizado na unidade. Este comportamento predefinido é recomendado, pois é mais rápido e eficiente. 

 Para obter mais informações, consulte [ativar BitLocker](/sccm/osd/understand/task-sequence-steps#BKMK_EnableBitLocker) e [provisão prévia do BitLocker](/sccm/osd/understand/task-sequence-steps#BKMK_PreProvisionBitLocker). 

#### <a name="client-provisioning-mode-isnt-enabled-with-windows-10-upgrade-compatibility-scan"></a>Modo de aprovisionamento de cliente não está ativado com a análise de compatibilidade da atualização do Windows 10
 <!--SCCMDocs-pr issue 2812--> Agora quando ativa a opção para **análise de compatibilidade de executar a configuração do Windows sem iniciar a atualização**, o **atualizar sistema operativo** passo de sequência de tarefas não coloca o cliente do Configuration Manager no modo de aprovisionamento.

 Para obter mais informações, consulte [atualizar sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).

#### <a name="revised-documentation-for-task-sequence-variables"></a>Documentação revisada para variáveis de sequência de tarefas
 Dois novos artigos estão agora disponíveis para compreender as variáveis de sequência de tarefas:  

 - [Como utilizar variáveis de sequência de tarefas](/sccm/osd/understand/using-task-sequence-variables) é um novo artigo que descreve os diferentes tipos de variáveis, métodos para definir as variáveis e como aceder aos mesmos.  

 - [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables) é uma referência para tarefas disponíveis todas as variáveis de sequência. Este artigo combina os artigos anteriores, o que separada variáveis incorporadas das variáveis de ação. 



## <a name="software-center"></a>Software Center

> [!Important]  
> Para tirar partido das novas funcionalidades do Configuration Manager, primeiro de atualizar os clientes para a versão mais recente. Enquanto a nova funcionalidade surge na consola do Configuration Manager ao atualizar a consola e do site, o cenário completo não é funcional até que a versão do cliente também é a versão mais recente.


### <a name="software-center-infrastructure-improvements"></a>Melhorias na infraestrutura de centro de software
<!--1358309--> Funções de catálogo de aplicações já não são necessárias para apresentar as aplicações disponíveis para o utilizador no Centro de Software. Esta alteração ajuda a reduzir a infraestrutura de servidor necessária para fornecer aplicativos aos usuários. Centro de software baseia-se agora no ponto de gestão para obter essa informação, que ajuda a escala de ambientes de maior melhor ao atribuir-lhes [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).

Para obter mais informações, consulte [configurar o Centro de Software](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex)  

> [!Note]  
> Os catálogo site web e de ponto de serviço ponto funções da aplicação já não estão *necessária* no 1806, mas ainda assim *suportado* funções. 
> 
> O **experiência de usuário do Silverlight** para o site do catálogo de aplicativos ponto já não é suportado. Para obter mais informações, consulte [funcionalidades removidas e preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  


### <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Especifique a visibilidade da ligação de site do catálogo de aplicações no Centro de Software
<!--1358214--> Utilizar definições de cliente para controlar se a ligação para **abrir o web site do catálogo de aplicações** é apresentado na **estado da instalação** nó do Centro de Software.  

Para obter mais informações, consulte [definições de cliente do Centro de Software](/sccm/core/clients/deploy/about-client-settings#software-center).

> [!Note]  
> O **experiência de usuário do Silverlight** para o site do catálogo de aplicativos ponto já não é suportado. Para obter mais informações, consulte [funcionalidades removidas e preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  


### <a name="custom-tab-for-webpage-in-software-center"></a>Separador personalizado para a página Web no Centro de Software
<!--1358132--> Utilize as definições de cliente para criar um separador personalizado para abrir uma página Web no Centro de Software. Esta funcionalidade permite-lhe mostrar o conteúdo aos seus utilizadores finais de forma consistente e confiável. A lista seguinte inclui alguns exemplos:  

- Contactar TI: informações sobre como contatar da sua organização departamento de TI  

- Centro de suporte IT: IT Self-serviços ações como pesquisar uma base de dados de conhecimento ou abrir um pedido de suporte.  

- Documentação do utilizador final: artigos para os utilizadores na sua organização em vários tópicos de TI como usar aplicativos ou atualizar para o Windows 10.  

Para obter mais informações, consulte [definições de cliente do Centro de Software](/sccm/core/clients/deploy/about-client-settings#software-center) e o [guia de utilizador do Centro de Software](/sccm/core/understand/software-center).


### <a name="maintenance-windows-in-software-center"></a>Janelas de manutenção no Centro de Software
<!--1358131--> Centro de software agora mostra a próxima janela de manutenção agendada. No separador Estado da instalação, alterne da exibição de todos para futuras. Apresenta o intervalo de tempo e a lista de implementações agendadas. Se não houver nenhum janelas de manutenção futura, a lista está em branco. 

Para obter mais informações, consulte [como utilizar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows) e o [guia de utilizador do Centro de Software](/sccm/core/understand/software-center).



## <a name="software-updates"></a>Atualizações de software

### <a name="third-party-software-updates"></a>Atualizações de software de terceiros
<!--1357605, 1352101, 1358714--> Atualizações de software de terceiros permitem-lhe subscrever catálogos de parceiros na consola do Configuration Manager e publicar as atualizações no WSUS. Poderá então implementar essas atualizações com o processo de gestão de atualizações de software existente. 

Para obter mais informações, consulte [ativar as atualizações de terceiros](/sccm/sum/deploy-use/third-party-software-updates).


### <a name="deploy-software-updates-without-content"></a>Implementar atualizações de software sem conteúdo
<!--1357933--> Implemente atualizações de software em dispositivos sem primeiro baixar e distribuir conteúdo para pontos de distribuição. Esta funcionalidade é benéfica ao lidar com conteúdo da atualização extremamente grandes ou quando pretender que sempre clientes a obter o conteúdo do serviço de nuvem do Microsoft Update. Os clientes neste cenário também podem transferir o conteúdo de elementos que já tenham o conteúdo necessário. O cliente continua a gerir a transferência do conteúdo, o Configuration Manager, portanto, pode utilizar a funcionalidade de cache ponto a ponto do Configuration Manager ou outras tecnologias, como a Otimização da entrega. Esta funcionalidade suporta qualquer tipo de atualização suportado pela gestão de atualizações de software do Configuration Manager, incluindo o Windows e atualizações do Office. 

Para obter mais informações, consulte a **sem pacote de implementação** opção quando [implementar manualmente atualizações de software](/sccm/sum/deploy-use/manually-deploy-software-updates) ou [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates).


### <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrar regras de implementação automática pela arquitetura de atualização de software
 <!--1322266--> Agora pode filtrar regras de implementação automática (ADR) para excluri arquiteturas como Itanium e ARM64. Sobre o **atualizações de Software** página de criar regra de Assistente de implementação automática, o **arquitetura** filtro de propriedade está agora disponível. 

Para obter mais informações, consulte [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates).


### <a name="improved-wsus-maintenance"></a>Manutenção WSUS melhorada 
<!--1357898--> O Assistente de limpeza do WSUS agora recusa atualizações que estão a expirou, de acordo com as regras de substituição definidas em Propriedades de componente do ponto de atualização de software. 

Para obter mais informações, consulte [manutenção de atualizações de Software](/sccm/sum/deploy-use/software-updates-maintenance).



## <a name="reporting"></a>Relatórios

### <a name="new-software-updates-compliance-report"></a>Novo relatório de conformidade de atualizações de software
<!--1357775--> Visualizar relatórios para atualizações de software conformidade tradicionalmente inclui os dados de clientes que ainda não recentemente a contactar o site. Um novo relatório, **conformidade 9 - estado de funcionamento geral e a conformidade**, permite-lhe filtrar os resultados de compatibilidade para um grupo de atualização de software específico por clientes de "integridade". Este relatório mostra o estado de conformidade mais realista dos clientes ativos no seu ambiente. 

Para obter mais informações, consulte [relatórios de atualizações de Software](/sccm/sum/deploy-use/monitor-software-updates#BKMK_SUReports).



## <a name="inventory"></a>Inventário

### <a name="bkmk_bigint"></a> Melhoria para o inventário de hardware para valores inteiros grandes
<!--1357880--> Inventário de hardware anteriormente tinha um limite para números inteiros maiores do que 4,294,967,296 (2 ^ 32). Este limite foi atingido para atributos, como tamanhos de disco rígido em bytes. O ponto de gestão não processar os valores de número inteiro acima desse limite, portanto, nenhum valor foi armazenado na base de dados. Agora, nesta versão, o limite foi aumentado para 18,446,744,073,709,551,616 (2 ^ 64). 

Para obter mais informações, consulte [utilização de valores de número inteiro grande](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory#bkmk_bigint).


### <a name="hardware-inventory-default-unit-revision"></a>Revisão de unidade de padrão de inventário de hardware
<!--514442--> Na [Configuration Manager versão 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#site-infrastructure), a unidade de padrão utilizada nas vistas de geração de relatórios muitos mudou de megabytes (MB) a gigabytes (GB). Devido a [melhorias ao inventário de hardware para valores inteiros grandes](#bkmk_bigint), e com base nos comentários dos clientes, esta unidade padrão é agora MB novamente.



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## <a name="configuration-manager-console"></a>Consola do Configuration Manager

### <a name="product-lifecycle-dashboard"></a>Dashboard de ciclo de vida do produto
<!--1319632--> O dashboard de ciclo de vida do produto mostra o estado da Microsoft Lifecycle Policy para produtos Microsoft instalados nos dispositivos geridos com o Configuration Manager. Ele também fornece informações sobre os produtos da Microsoft no seu ambiente, o estado de capacidade de suporte e datas de término do suporte. Utilize o dashboard para compreender a disponibilidade de suporte para cada produto. Estas informações ajudam a planear quando atualizar os produtos da Microsoft utilizar antes de seu suporte terminará a atual for atingido.   

Para obter mais informações, consulte [dashboard de ciclo de vida do produto](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard).


### <a name="copy-asset-details-from-monitoring-views"></a>Copiar detalhes do ativo de vistas de monitorização
<!--1357856--> As seguintes áreas do **monitorização** suportam agora de área de trabalho copiar texto:  

- Na **implementações** nó, selecione uma implementação e clique em **Ver estado**. Na **detalhes do ativo** painel de vista de estado de implementação, selecione um ou mais dispositivos.  

- Expanda a **estado de distribuição** nó e selecione **estado do conteúdo**. Selecione uma parte do software e clique em **ver o estado**. Na **detalhes do ativo** painel de vista de estado do conteúdo, selecione um ou mais pontos de distribuição. 

O elemento com o botão direito e selecione **cópia**. Esta ação copia dos recursos selecionados como uma lista delimitada por vírgulas que inclui todos os detalhes. O atalho de teclado **CTRL** + **C** também funciona nesses modos de exibição. 

Para obter mais informações, consulte [consola melhorias na versão 1806](/sccm/core/servers/manage/admin-console#console-improvements-in-version-1806).


### <a name="improvements-to-the-surface-dashboard"></a>Aprimoramentos no painel do Surface
<!--1358654--> Esta versão inclui as seguintes melhorias para o painel do Surface:  

- O painel do Surface apresenta agora uma lista de dispositivos relevantes quando seleciona as secções do gráfico específico:  

   - Clicar no **por cento de dispositivos Surface** mosaico abre-se uma lista de dispositivos Surface.  

   - Clicar numa barra no **principais cinco versões de Firmware** mosaico abre-se uma lista de dispositivos Surface com essa versão de firmware específico.  

- Ao visualizar estas listas de dispositivo a partir do painel do Surface, faça duplo clique de um dispositivo para realizar ações comuns.  

Para obter mais informações, consulte [painel do Surface](/sccm/core/clients/manage/surface-device-dashboard).


### <a name="view-the-currently-signed-on-user-for-a-device"></a>Ver o utilizador atualmente com sessão iniciado para um dispositivo
<!--1358202--> Agora, por predefinição o **dispositivos** nó da **ativos e compatibilidade** área de trabalho apresenta uma coluna para o **atualmente com sessão iniciada no utilizador**. Ele também exibe para qualquer lista de dispositivos específicos da coleção. Este valor é as mais atual a [estado do cliente](/sccm/core/clients/manage/monitor-clients#bkmk_indStatus). Quando o utilizador inicia-se, o cliente limpa este valor. Se nenhum utilizador estará inscrito, o valor está em branco. 

Para obter mais informações, consulte [consola melhorias na versão 1806](/sccm/core/servers/manage/admin-console#console-improvements-in-version-1806).


### <a name="submit-feedback-from-the-configuration-manager-console"></a>Enviar comentários a partir da consola do Configuration Manager  
<!--1357542-->

Envie um sorriso! Pode agora diretamente informar a equipa do Configuration Manager sobre as suas experiências. Envio de comentários é fácil partir da consola do Configuration Manager. Queremos ouvir todos os seus comentários: elogios, os problemas e sugestões. Na consola do Configuration Manager, clique no botão de sorriso no canto superior direito acima do Friso. Estes comentários vai diretamente para a equipe de produto da Microsoft para o Configuration Manager. Embora ainda seja suportada através do Hub de comentários do Windows 10, é recomendado que utilize o mecanismo de comentários na consola.  

Para obter mais informações, consulte [consola melhorias na versão 1806](/sccm/core/servers/manage/admin-console#console-improvements-in-version-1806) e [comentários sobre o produto](/sccm/core/understand/find-help#BKMK_1806Feedback).



## <a name="other-updates"></a>Outras atualizações

Além das novas funcionalidades, esta versão também inclui alterações adicionais, como correções de erros. Para obter mais informações, consulte [resumo das alterações no ramo atual do Configuration Manager, versão 1806](https://support.microsoft.com/help/4459701).

Para obter mais informações sobre as alterações aos cmdlets do Windows PowerShell para o Configuration Manager, consulte [notas de versão do PowerShell 1806](https://docs.microsoft.com/powershell/sccm/1806_release_notes?view=sccm-ps).

O update rollup seguintes (4462978) está disponível na consola a partir de 24 de Outubro de 2018: [Update rollup para o ramo atual do Configuration Manager, versão 1806](https://support.microsoft.com/help/4462978).


### <a name="hotfixes"></a>Correções

As seguintes correções adicionais estão disponíveis para resolver problemas específicos:

| ID | Título | Date | In-console |
|---------|---------|---------|---------|
| [4346645](https://support.microsoft.com/help/4346645) | Atualização do System Center Configuration Manager versão 1806, primeira vaga | 31 de Agosto de 2018 | Sim |
| [4465865](https://support.microsoft.com/help/4465865) | Não transferir as atualizações de software no ambiente do Configuration Manager se o WSUS está desligado<br><br>Esta atualização também está a ser o update rollup (4462978) | 01 de Outubro de 2018 | Sim |
| [4471892](https://support.microsoft.com/help/4471892) | Dispositivo de resposta PXE não funciona nas sub-redes 1806 do Configuration Manager | 23 de Novembro de 2018 | Não |



## <a name="next-steps"></a>Passos seguintes

Quando estiver pronto para instalar esta versão, consulte [instalação de atualizações para o Configuration Manager](/sccm/core/servers/manage/updates) e [lista de verificação para a instalação de atualização 1806](/sccm/core/servers/manage/checklist-for-installing-update-1806).

> [!TIP]  
> Para instalar um novo site, utilize uma versão de linha de base do Configuration Manager.  
>
>  Saiba mais sobre:    
>   - [Instalar novos sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Versões de linha de base e de atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Para problemas conhecidos e significativos, consulte a [notas de versão](/sccm/core/servers/deploy/install/release-notes).

Depois de atualizar um site, reveja também os [lista de verificação de pós-atualização](/sccm/core/servers/manage/checklist-for-installing-update-1806#post-update-checklist).

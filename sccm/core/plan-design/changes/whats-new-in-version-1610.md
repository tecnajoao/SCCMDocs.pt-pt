---
title: Nova versão 1610
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas funcionalidades introduzidas na versão 1610 do System Center Configuration Manager.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: cb9b19c95caaf914fa1cbf040258c30ede2dc54a
ms.sourcegitcommit: fe279229a90fdc8cddbb13c7ffdbbb22af0e25ef
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47229318"
---
# <a name="what39s-new-in-version-1610-of-system-center-configuration-manager"></a>O que&#39;s novo na versão 1610 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Atualize versão 1610 para o ramo atual do System Center Configuration Manager está disponível como uma atualização na consola para sites anteriormente instalados com a versão 1511, versão 1602 ou 1606.


> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de linha de base do Configuration Manager.  
>  Saiba mais sobre:    
>  -   [Instalar novos sites](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [Instalar atualizações em sites](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [Versões de linha de base e de atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As secções seguintes fornecem detalhes sobre alterações e novas funcionalidades introduzidas na versão 1610 do Configuration Manager.  


## <a name="in-console-monitoring-of-update-installation-status"></a>Monitorização de estado de instalação da atualização na consola  
Partir da versão 1610, quando instalar um pacote de atualização e monitorizar a instalação na consola, há uma nova fase: **Pós-instalação**. Esta fase inclui o estado para tarefas como reiniciar serviços-chave e inicialização de monitoração da replicação. (Esta fase não está disponível na consola após as atualizações de site para a versão 1610). Para obter mais informações sobre o estado de instalação de atualização, consulte [instalar atualizações na consola](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).


## <a name="exclude-clients-from-automatic-upgrade"></a>Excluir clientes da atualização automática
Pode impedir que os clientes do Windows a ser atualizados com novas versões do software de cliente. Para tal, incluem-se os computadores cliente numa coleção especificada a serem excluídos da atualização. Os clientes na coleção excluída ignoram pedidos para atualizar o software de cliente.  Para obter mais informações, consulte [Windows excluir os clientes de atualizações](../../clients/manage/upgrade/exclude-clients-windows.md).


## <a name="improvements-for-boundary-groups"></a>Melhorias de grupos de limites
Versão 1610 introduz alterações importantes para grupos de limites e como eles funcionam com pontos de distribuição. Estas alterações podem simplificar o design da sua infraestrutura de conteúdo, dando-lhe mais controlo sobre como e quando os pontos de contingência de clientes para distribuição adicionais de pesquisa como localizações de origem de conteúdo. Isto inclui pontos de distribuição baseado na nuvem e no local.
Esses aprimoramentos substituem os conceitos e comportamentos que pode estar familiarizado com (como configurar pontos de distribuição para ser rápido ou lento). O novo modelo deve ser mais fácil de configurar e manter. Essas alterações também preparar a base para futuras alterações que irão melhorar a outras funções de sistema de sites, associar a grupos de limites.

Quando atualizar para versão 1610, a atualização converte as configurações de grupo de limite atual de acordo com o novo modelo para que estas alterações não incomodar suas configurações de distribuição de conteúdo existente.

Para obter mais informações, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#a-namebkmkboundarygroupsa-boundary-groups).


## <a name="peer-cache-for-content-distribution-to-clients"></a>Cache ponto a ponto de distribuição de conteúdo para clientes
Desde a versão 1610, o cliente **Cache ponto a ponto** ajuda-o a gerir a implementação de conteúdo para clientes em localizações remotas. Cache ponto a ponto é uma solução incorporada do Configuration Manager para os clientes partilhem conteúdos com outros clientes, diretamente a partir da respetiva cache local.

Depois de implementar as definições de cliente que permitem a Cache ponto a ponto para uma coleção, os membros dessa coleção podem agir como uma origem de conteúdo de ponto a ponto para outros clientes no mesmo grupo de limites.

Também pode utilizar a nova **origens de dados do cliente** dashboard para compreender a utilização de fontes de conteúdo de Cache ponto a ponto no seu ambiente.

> [!TIP]  
> Com a versão 1610, a Cache ponto a ponto e o dashboard de origens de dados do cliente são funcionalidades de pré-lançamento. Para ativá-las, consulte [utilizar as funcionalidades de pré-lançamento de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

Para obter mais informações, consulte [Cache ponto a ponto para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache), e [dashboard de origens de dados do cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrar vários pontos de distribuição partilhado, ao mesmo tempo
Agora, pode utilizar a opção para **reatribuir ponto de distribuição** para que o processo do Configuration Manager em paralelo a reatribuição de até 50 pontos de distribuição partilhados ao mesmo tempo. Antes desta versão, os pontos de distribuição reatribuída foram processado um de cada vez. Para obter mais informações, consulte [migrar vários pontos de distribuição partilhado, ao mesmo tempo](/sccm/core/migration/planning-a-content-deployment-migration-strategy#migrate-multiple-shared-distribution-points-at-the-same-time).

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Gateway de gestão na cloud para gestão de clientes baseados na Internet

Gateway de gestão da nuvem fornece uma forma simples de gerir clientes do Configuration Manager na Internet. O serviço de gateway de gestão na cloud, que é implementado no Microsoft Azure e requer uma subscrição do Azure, liga-se à sua infraestrutura do Configuration Manager no local com uma nova função chamada o ponto de ligação do gateway de gestão na cloud. Assim que tiver totalmente implementado e configurado, os clientes podem comunicar com funções de sistema de sites no local do Configuration Manager e os pontos de distribuição baseado na nuvem, independentemente de se eles estão conectados à rede interna privada ou na Internet. Para obter mais informações e para ver como o gateway de gestão da nuvem se compara com gestão de clientes baseados na Internet, consulte [gerir clientes na Internet](/sccm/core/clients/manage/manage-clients-internet).

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Melhoramentos à Política de Atualização de Edição do Windows 10
Nesta versão, foram efetuadas as seguintes melhorias para este tipo de política:

- Agora, pode utilizar a política de atualização de edição com PCs Windows 10 que executam o cliente de Configuration Manager, além de PCs do Windows 10 inscritos com o Microsoft Intune.
- Pode atualizar do Windows 10 Professional para qualquer uma das plataformas no assistente que são compatíveis com seu hardware.

## <a name="manage-hardware-identifiers"></a>Gerir os identificadores de hardware
Agora pode fornecer uma lista de IDs do Configuration Manager deve ignorar para fins de registo de cliente e arranque PXE de hardware. Existem dois problemas comuns que ajuda a endereço:

1. Muitos dispositivos, como o 3 Surface Pro, não incluem uma porta Ethernet carregar. Um adaptador USB para Ethernet é geralmente utilizado para estabelecer uma ligação com fios com o objetivo de implementar um sistema operativo. No entanto, devido ao custo e a usabilidade geral, estas são, muitas vezes, adaptadores partilhados. Como o endereço MAC deste adaptador é utilizado para identificar o dispositivo, a reutilizar o adaptador torna-se problemático sem ações de administrador adicionais entre cada implementação. Agora no Configuration Manager versão 1610, pode excluir o endereço MAC deste adaptador para que possa ser facilmente reutilizado neste cenário.
2. O ID SMBIOS deve para ser um identificador exclusivo de hardware, mas alguns dispositivos de hardware de especialidade baseiam-se com IDs duplicados. Este problema pode não ser tão comum quanto o cenário de adaptador USB para Ethernet, Acabei de descrever, mas pode resolver o problema, utilizando a lista de identificações de hardware excluídas.

Para obter detalhes, consulte [identificadores de hardware duplicados gerir](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers).

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Aprimoramentos na Windows Store para integração de negócios com o Configuration Manager
Alterações nesta versão:
- Anteriormente, só pode implementar aplicações gratuitas da Windows Store para empresas. Gestor de configuração agora adicionalmente suporta a implementação de online pago licenciado aplicações (para dispositivos inscritos no Intune).
- Agora pode iniciar uma sincronização imediata entre o Windows Store para empresas e o Configuration Manager.
- Agora pode modificar a chave secreta do cliente que obteve do Azure Active Directory.
- Pode eliminar uma subscrição para o arquivo.

Para obter detalhes, consulte [gerir aplicações a partir da Windows Store para empresas com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).


## <a name="policy-sync-for-intune-enrolled-devices"></a>Sincronização de política para dispositivos inscritos no Intune
Agora pode pedir uma sincronização de política para um dispositivo de inscritos no Intune a partir da consola do Configuration Manager, em vez de terem de pedir uma sincronização a partir da aplicação Portal da empresa no próprio dispositivo. Informações de estado do pedido de sincronização estão disponíveis como uma nova coluna em modos de exibição do dispositivo, chamado **estado de sincronização de remoto**. As informações também estão disponíveis na secção de dados de deteção do **propriedades** caixa de diálogo para cada dispositivo.
Para obter detalhes, consulte [remotamente sincronizar política nos dispositivos inscritos no Intune a partir da consola do Configuration Manager](/sccm/mdm/deploy-use/sync-intune-device).


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Utilize as definições de compatibilidade para configurar definições do Windows Defender
Agora pode configurar definições de cliente do Windows Defender em computadores Windows 10 inscritos no Intune com itens de configuração na consola do Configuration Manager.
Para obter detalhes, consulte a **o Windows Defender** secção [criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client).



## <a name="general-improvements-to-software-center"></a>Melhoramentos gerais ao centro de Software
- Os utilizadores agora podem pedir aplicações a partir do Centro de Software, bem como o catálogo de aplicações.
- Melhorias para ajudar os utilizadores a compreender qual software é novo e relevantes.

## <a name="new-columns-in-device-collection-views"></a>Novas colunas nas vistas de coleção de dispositivos
Agora pode exibir colunas para **IMEI** e **número de série** (para dispositivos iOS) em vistas de coleção de dispositivos.
Para obter mais detalhes, consulte [pré-declarar dispositivos com números de série IMEI ou iOS](https://docs.microsoft.com/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id).

## <a name="customizable-branding-for-software-center-dialogs"></a>Personalizável para caixas de diálogo do Centro de Software de imagem corporativa
Imagem corporativa personalizada para o Centro de Software foi introduzida no Configuration Manager versão 1602. Na versão 1610, essa imagem corporativa abranger agora todas as caixas de diálogo associado para fornecer uma experiência mais consistente aos utilizadores do Centro de Software.

Imagem corporativa personalizada para o Centro de Software é aplicada, de acordo com as seguintes regras:

- Se a função de servidor de sites do ponto de Web site do catálogo de aplicações não está instalada, o Centro de Software apresenta o nome da organização especificado na **agente do computador** definição do cliente **nome da organização apresentada no Centro de software**. Para obter instruções, consulte [como configurar as definições de cliente](../../clients/deploy/configure-client-settings.md).

- Se a função de servidor de sites do ponto de Web site do catálogo de aplicações estiver instalada, o Centro de Software apresenta o nome da organização e a cor especificados nas propriedades de função do servidor de ponto de site catálogo de aplicações Web site. Para obter mais informações, consulte [opções de configuração do ponto de Web sites do catálogo de aplicações](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#Application-Catalog-website-point).

- Se uma subscrição do Microsoft Intune é configurada e ligada ao ambiente do Configuration Manager, em seguida, o Centro de Software apresenta o nome da organização, a cor e o logótipo da empresa especificados nas propriedades de subscrição do Intune. Para obter mais informações, veja [Configurar a Subscrição do Microsoft Intune](/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Período de tolerância de imposição para implementações de atualizações de aplicações e de software
Em alguns casos, pode querer dar aos utilizadores mais tempo para implementações de aplicações é necessária instalação ou atualização de software para além de quaisquer prazos que configurou. Por exemplo, isso poderá ser necessário quando um computador foi desativado por um longo período de tempo e de que necessita instalar um grande número de implementações de aplicação ou atualização. Por exemplo, se um utilizador final acabou de voltar de férias, poderá ter de aguardar por um longo enquanto como aplicação em atraso implementações estão instaladas. Para ajudar a resolver este problema, agora pode definir um período de tolerância de imposição ao implementar as definições de cliente do Configuration Manager para uma coleção. 

Para configurar o período de tolerância, efetue as seguintes ações:
1.      Sobre o **agente do computador** página de definições de cliente, configurar a nova propriedade **período de tolerância para a imposição de após a implementação do prazo (horas)** com um valor entre **1** e **120** horas.
2.      Numa nova implementação de aplicação necessária, ou nas propriedades de uma implementação existente, sobre o **agendamento** , selecione a caixa de verificação **Trasar imposição para esta implementação, de acordo com as preferências do usuário, até o período de tolerância definido nas definições de cliente**. Todas as implementações que tenham esta caixa de verificação selecionada e são direcionadas para os dispositivos em que implementou também o definição de cliente utilizará o período de tolerância de imposição.

Se configurar um período de tolerância de imposição e selecione a caixa de verificação, assim que for atingido o prazo de instalação do aplicativo, será instalado na primeira janela não comerciais que o utilizador configurado até esse período de tolerância. No entanto, o utilizador ainda pode abrir o Centro de Software e instalar a aplicação a qualquer momento que desejarem. Assim que o período de tolerância expirar, imposição reverte para o comportamento normal para implementações em atraso. Foram adicionadas opções similares para o Assistente de implementação de atualizações de software, o Assistente de regras de implementação automática e páginas de propriedades.



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>Funcionalidade aprimorada nas caixas de diálogo sobre o software necessário
Quando um utilizador recebe o software necessário, do **suspender e lembrar-me:** definir, podem selecionar da lista pendente seguinte de valores: 
- **Mais tarde**. Especifica que as notificações estão agendadas com base nas definições de notificação configuradas nas definições do agente de cliente.
- **Corrigido tempo**. Especifica que a notificação será agendada para apresentar novamente após a hora selecionada (por exemplo, em 30 minutos).

![Página de agente do computador nas definições do agente de cliente](media/client-notification-settings.png)

O tempo máximo suspender baseia-se nos valores de notificação configurados nas definições de agente do cliente. Por exemplo, se o **implementação prazo superior a 24 horas, lembrar os usuários a cada (horas)** definição no computador agente página estiver configurada para dez horas e é mais de 24 horas antes do prazo, o utilizador irá ver um conjunto de suspender Opções de cópia de segurança para mas nunca maiores do que 10 horas. À medida que o prazo aproxima, menos opções estão disponíveis, consistente com as definições de agente do cliente relevantes para cada componente da linha da tempo de implementação.

Além disso, para uma implementação de alto risco, como uma sequência de tarefas que implementa um sistema operativo, a experiência de notificação do utilizador é agora mais intrusiva. Em vez de uma notificação de barra de tarefas transitório, sempre que o utilizador é notificado de que a manutenção crítica do software é necessária, um caixa de diálogo, como o seguinte é apresentado no computador do usuário:

![Caixa de diálogo de Software necessária](media/client-toast-notification.png)


Para obter mais informações:
- [Definições para gerir implementações de alto risco](../../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Como configurar as definições do cliente](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Dashboard de atualizações de software
Utilizar o novo dashboard de atualizações de software para ver o atual estado de conformidade de dispositivos na sua organização e analisar rapidamente os dados para ver os dispositivos que estão em risco. Para ver o dashboard, navegue até **monitorização** > **descrição geral** > **segurança** > **atualizações de Software Dashboard**.

Para obter detalhes, consulte [monitorizar atualizações de software](/sccm/sum/deploy-use/monitor-software-updates).


## <a name="improvements-to-the-application-request-process"></a>Melhorias ao processo de pedido de aplicação
Depois que tiver aprovado uma aplicação para a instalação, em seguida, pode optar por negar o pedido ao clicar em **negar** na consola do Configuration Manager. Anteriormente, este botão era indisponíveis após a aprovação.

Esta ação não faz com que o aplicativo para ser desinstaladas da todos os dispositivos. No entanto, ele parar que os utilizadores instalem novas cópias da aplicação do Centro de Software.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrar por tamanho do conteúdo nas regras de implementação automática
Agora pode filtrar o tamanho do conteúdo para atualizações de software nas regras de implementação automática. Por exemplo, para transferir apenas atualizações de software que são mais pequenas do que 2 MB, pode definir o **conteúdo tamanho (KB)** filtrar para **< 2048**. Utilizar este filtro impede que as atualizações de software grandes sejam transferidas automaticamente, que oferece suporte à melhor simplificado de nível baixo de manutenção quando a largura de banda de rede do Windows. Para obter detalhes, consulte:
- [Configuration Manager e o Windows simplificada, manutenção em baixo nível sistemas de operativos](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)
- [Implementar atualizações de software automaticamente](/sccm/sum/deploy-use/automatically-deploy-software-updates)

Para configurar o **conteúdo tamanho (KB)** campo, efetue um dos seguintes procedimentos:
- Quando cria uma regra de implementação automática, no Assistente Criar regra de implementação automática, vá para o **atualizações de Software** página.
- Nas propriedades de uma regra de implementação automática existente, vá para o **atualizações de Software** separador.

## <a name="office-365-client-management-dashboard"></a>Dashboard de gestão de clientes do Office 365
O dashboard de gestão de clientes do Office 365 está agora disponível na consola do Configuration Manager. Para ver o dashboard, aceda a **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**.

O dashboard apresenta gráficos para o seguinte:

- Número de clientes do Office 365
- Versões de cliente do Office 365
- Idiomas de cliente do Office 365
- Canais de cliente do Office 365     

Para obter detalhes, consulte [atualizações de gerir o Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Passos de sequência de tarefas para gerir o BIOS para conversão de UEFI
Agora pode personalizar uma sequência de tarefas de implementação do sistema operativo com uma nova variável, TSUEFIDrive, para que o **reiniciar o computador** passo irá preparar uma partição FAT32 na unidade de disco rígida para a transição para UEFI. O procedimento seguinte fornece um exemplo de como pode criar passos de sequência de tarefas para preparar o disco rígido para o BIOS para conversão de UEFI. Para obter detalhes, consulte [passos para gerir o BIOS para conversão de UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion).

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>Melhorias para o passo de sequência de tarefas: Prepare ConfigMgr Client for Capture  
O passo preparar ConfigMgr Client agora removerá completamente o cliente do Configuration Manager, em vez de apenas remover informações de chave. Quando a sequência de tarefas implementa a imagem de sistema operativo capturada, ele instalará um novo cliente de Configuration Manager cada vez. Para obter detalhes, consulte [passos de sequência de tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture).



## <a name="intune-compliance-policy-charts"></a>Gráficos de política de conformidade do Intune
Agora pode obter uma vista rápida da conformidade geral dos dispositivos e os principais motivos pelos quais de não conformidade, usando novos gráficos no **monitorização** área de trabalho na consola do Configuration Manager. Pode clicar numa seção no gráfico para desagregar para obter uma lista dos dispositivos dessa categoria. Para obter detalhes, consulte [monitorizar a política de conformidade](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy).


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>Integração do lookout para implementações híbridas proteger dispositivos iOS e Android
Microsoft está a integrar a solução de proteção da Lookout contra ameaças móveis para proteger dispositivos iOS e Android móveis através da deteção de software maligno, aplicações de risco e muito mais, nos dispositivos. Solução da lookout ajuda a determinar o nível de ameaça, o que é configurável. Pode criar uma regra de política de conformidade no System Center Configuration Manager, para determinar a conformidade do dispositivo com base na avaliação de riscos pelo Lookout. Utilizar políticas de acesso condicional, pode permitir ou bloquear o acesso aos recursos da empresa com base no estado de conformidade do dispositivo. Para saber mais sobre a integração e como ele funciona, veja [gerir o acesso com base em riscos de aplicações, redes e dispositivos](/sccm/protect/deploy-use/manage-access-based-on-device-network-app-risk).

Os utilizadores de dispositivos em não conformidade iOS serão solicitados a inscrever. Elas serão necessárias para instalar o Lookout for Work aplicação nos respetivos dispositivos, ativar a aplicação e corrigir as ameaças comunicadas no Lookout for Work a aplicação obter acesso aos dados da empresa. Saiba como [configurar e implementar o Lookout for Work apps](/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps).



## <a name="new-compliance-settings-for-configuration-items"></a>Novas definições de conformidade para itens de configuração
Existem muitas definições novas, que pode usar nos seus itens de configuração para várias plataformas de dispositivos. Estas são as definições que já existiam no Microsoft Intune numa configuração autónoma e estão agora disponíveis ao utilizar o Intune com o Configuration Manager.
Para obter detalhes, consulte [itens de configuração para dispositivos geridos sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/configuration-items-for-devices-managed-without-the-client).

### <a name="new-settings-for-android-devices"></a>Novas definições para dispositivos Android
#### <a name="password-settings"></a>Definições de palavra-passe
- **Memorizar histórico de palavras-passe**
- **Permitir impressões digitais desbloquear**

#### <a name="security-settings"></a>Definições de segurança
- **Encriptação obrigatória nos cartões de armazenamento**
- **Permitir captura de ecrã**
- **Permitir submissão de dados de diagnóstico**

#### <a name="browser-settings"></a>Definições do browser
- **Permitir browser**
- **Permitir Preenchimento automático**
- **Permitir Bloqueador de pop-up**
- **Permitir cookies**
- **Permitir scripting ativo**

#### <a name="app-settings"></a>Definições da aplicação
- **Permitir loja do Google Play**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo
- **Permitir armazenamento amovível**
- **Permitir tethering Wi-Fi**
- **Permitir geolocalização**
- **Permitir NFC**
- **Permitir Bluetooth**
- **Permitir roaming de voz**
- **Permitir roaming de dados**
- **Permitir mensagens SMS/MMS**
- **Permitir Assistente de voz**
- **Permitir marcação por voz**
- **Permitir copiar e colar**

### <a name="new-settings-for-ios-devices"></a>Novas definições para dispositivos iOS
#### <a name="password-settings"></a>Definições de palavra-passe
- **Número de carateres complexos necessários na palavra-passe**
- **Permitir palavras-passe simples**
- **Minutos de inatividade antes da palavra-passe é necessária**
- **Memorizar histórico de palavras-passe**

### <a name="new-settings-for-mac-os-x-devices"></a>Novas definições para dispositivos Mac OS X
#### <a name="password-settings"></a>Definições de palavra-passe
- **Número de carateres complexos necessários na palavra-passe**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavras-passe**
- **Minutos de inatividade antes da proteção de ecrã ser ativada**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Novas definições para dispositivos Windows 10 Desktop e Mobile
#### <a name="password-settings"></a>Definições de palavra-passe
- **Número mínimo de conjuntos de carateres**
- **Memorizar histórico de palavras-passe**
- **Exigir uma palavra-passe quando o dispositivo regressa de um estado inativo**

#### <a name="security-settings"></a>Definições de segurança
- **Exigir encriptação no dispositivo móvel**
- **Permitir anular inscrições manualmente**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo
- **Permitir VPN pela rede móvel**
- **Permitir roaming de VPN por rede móvel**
- **Permitir reposição do telefone**
- **Permitir ligação USB**
- **Permitir Cortana**
- **Permitir notificações do Centro de ação**

### <a name="new-settings-for-windows-10-team-devices"></a>Novas definições para dispositivos Windows 10 Team
#### <a name="device-settings"></a>Definições do dispositivo
- **Ativar as informações operacionais do Azure**
- **Ativar projeção sem fios Miracast**
- **Escolher as informações de reunião apresentadas no ecrã de boas-vindos**
- **URL de imagem de fundo do ecrã de bloqueio**

### <a name="new-settings-for-windows-81-devices"></a>Novas definições para dispositivos Windows 8.1
#### <a name="applicability-settings"></a>Definições de aplicabilidade
- **Aplicar todas as configurações para o Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe
- **Tipo de palavra-passe necessária**
- **Número mínimo de conjuntos de carateres**
- **Comprimento mínimo da palavra-passe**
- **Número de falhas de início de sessão consecutivas a permitir antes do dispositivo ser apagado**
- **Minutos de inatividade antes do ecrã se desligar**
- **Expiração de palavra-passe (dias)**
- **Memorizar histórico de palavras-passe**
- **Impedir a reutilização de palavras-passe anteriores**
- **Permitir palavra-passe de imagem e PIN**

#### <a name="browser-settings"></a>Definições do browser
- **Permitir deteção automática de rede intranet**

### <a name="new-settings-for-windows-phone-81-devices"></a>Novas definições para dispositivos Windows Phone 8.1
#### <a name="applicability-settings"></a>Definições de aplicabilidade
- **Aplicar todas as configurações para o Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe
- **Número mínimo de conjuntos de carateres**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavras-passe**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo
- **Permitir ligação automática a hotspots Wi-Fi**

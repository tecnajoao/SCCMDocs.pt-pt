---
title: "Nova versão 1610 | Documentos do Microsoft"
description: "Obter informações sobre as alterações e novas capacidades de introduzida na versão 1610 do System Center Configuration Manager."
ms.custom: na
ms.date: 11/23/2016
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
caps.latest.revision: 40
author: Brenduns
ms.author: brenduns
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
ms.translationtype: Machine Translation
ms.sourcegitcommit: 831d8a66c827d246069c7415cdce7a7c4bb95b33
ms.openlocfilehash: 19e3099773f887129374413482702de3f4b0a36f
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="what39s-new-in-version-1610-of-system-center-configuration-manager"></a>O que &#39; s Novidades na versão 1610 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Atualize 1610 para ramo atual do System Center Configuration Manager está disponível como uma atualização na consola de sites instaladas anteriormente com a versão 1511, 1602 ou 1606.


> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de linha de base do Configuration Manager.  
>  Saiba mais sobre:    
>  -   [Instalar novos sites](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [Instalação de atualizações de sites](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As secções seguintes fornecem detalhes sobre as alterações e funcionalidades novas, introduzidas na versão 1610 do Configuration Manager.  


## <a name="in-console-monitoring-of-update-installation-status"></a>A monitorização do Estado de instalação da atualização na consola  
Iniciar com a versão 1610, quando é instalado um pacote de atualização e monitorizar a instalação na consola, existe uma nova fase: **Publicar instalação**. Esta fase inclui o estado para tarefas como reiniciar os serviços principais e de inicialização de monitorização de replicação. (Esta fase não está disponível na consola até após as atualizações de sites para versão 1610.) Para obter mais informações sobre o estado de instalação de atualização, consulte o artigo [instalar atualizações em consola](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).


## <a name="exclude-clients-from-automatic-upgrade"></a>Excluir os clientes da atualização automática
Pode excluir clientes Windows de introdução atualizado com novas versões do software de cliente. Para fazer isto, incluem os computadores cliente numa coleção especificada que serão excluídas da atualização. Os clientes na coleção de excluídas ignoram pedidos para atualizar o software de cliente.  Para obter mais informações, consulte o artigo [Windows excluir os clientes de atualizações](../../clients/manage/upgrade/exclude-clients-windows.md).


## <a name="improvements-for-boundary-groups"></a>Melhoramentos na cópia de grupos de limites
Versão 1610 introduz alterações importantes para os grupos de limites e como funcionam com pontos de distribuição. Estas alterações podem simplificar a estrutura da sua infraestrutura de conteúdo, ao dando-lhe mais controlo sobre como e quando pontos como localizações de origem de conteúdo de contingência de clientes para pesquisar distribuição adicionais. Isto inclui no local e os pontos de distribuição baseado na nuvem.
Estes melhoramentos substituem conceitos e comportamentos que poderá estar familiarizado com (como configurar pontos de distribuição para ser rápida ou lenta). O novo modelo deve ser mais fácil de configurar e manter. Estas alterações também dispor as bases para que as alterações futuras que irão melhorar a outras funções de sistema do site que efetuada a associação a grupos de limites.

Quando atualizar para versão 1610, a atualização converte das configurações de grupo de limites atuais para ajustar o novo modelo de modo a que estas alterações não incomodar as configurações de distribuição de conteúdo existente.

Para obter mais informações, consulte o artigo [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#a-namebkmkboundarygroupsa-boundary-groups).


## <a name="peer-cache-for-content-distribution-to-clients"></a>Cache ponto a ponto de distribuição de conteúdo para clientes
Início com a versão 1610, do cliente **cache de elementos da** ajuda-o a gerir a implementação de conteúdo para clientes em localizações remotas. Cache de elementos da é uma solução de Configuration Manager incorporados para os clientes partilhem conteúdos com outros clientes, diretamente a partir da respetiva cache local.

Depois de implementar as definições de cliente que permitem Cache ponto a ponto para uma coleção, os membros da coleção de que podem agir como uma origem de conteúdo ponto a ponto para outros clientes no mesmo grupo de limites.

Também pode utilizar a nova **origens de dados de cliente** dashboard para compreender a utilização de origens de conteúdo de Cache de elemento de rede no seu ambiente.

> [!TIP]  
> Com a versão 1610, Cache ponto a ponto e o dashboard de origens de dados do cliente são funcionalidades da versão de pré-lançamento. Para ativá-las, consulte o artigo [utilizar funcionalidades de pré-lançamento das atualizações da](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

Para obter mais informações, consulte o artigo [Cache ponto a ponto para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache), e [dashboard de origens de dados de cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrar vários pontos de distribuição partilhado ao mesmo tempo
Agora pode utilizar a opção de **ponto de distribuição de reatribuir** para que o processo do Configuration Manager em paralelo reatribuição de até 50 pontos de distribuição partilhados ao mesmo tempo. Esta versão, os pontos de distribuição reatribuídas foram processado um de cada vez. Para obter mais informações, consulte o artigo [migrar vários pontos de distribuição partilhado ao mesmo tempo](/sccm/core/migration/planning-a-content-deployment-migration-strategy#migrate-multiple-shared-distribution-points-at-the-same-time).

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Gateway de gestão da nuvem para a gestão de clientes baseados na Internet

Gateway de gestão na nuvem fornece uma forma simples de gerir clientes do Configuration Manager na Internet. O serviço de gateway de gestão na nuvem, que é implementado para o Microsoft Azure e necessita de uma subscrição do Azure, liga-se para a infraestrutura do Configuration Manager no local com uma nova função de denominado o ponto de ligação do gateway de gestão na nuvem. Assim que tiver completamente implementados e configurados, os clientes podem comunicar com funções de sistema de sites no local do Configuration Manager e os pontos de distribuição baseado na nuvem, independentemente de se estão ligados à rede privada interna ou na Internet. Para obter mais informações e para ver como o gateway de gestão da nuvem se compara com gestão de clientes baseados na Internet, consulte [gerir clientes na Internet](/sccm/core/clients/manage/manage-clients-internet).

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Melhoramentos à Política de Atualização de Edição do Windows 10
Nesta versão, as seguintes melhorias foram efetuadas para este tipo de política:

- Agora, pode utilizar a política de atualização de edição com o Windows 10 PCs que executam o cliente do Configuration Manager, além do Windows 10 PCs que estão inscritos com o Microsoft Intune.
- Pode atualizar a partir do Windows 10 Professional a qualquer uma das plataformas no Assistente de que são compatíveis com o hardware.

## <a name="manage-hardware-identifiers"></a>Gerir identificadores de hardware
Agora pode fornecer uma lista de IDs do Configuration Manager deve ignorar para efeitos de registo de arranque e de cliente PXE de hardware. Existem dois problemas comuns que isto ajuda a endereço:

1. Vários dispositivos, como as 3 Surface Pro, não incluem uma porta Ethernet carregar. Um adaptador USB para Ethernet é geralmente utilizado para estabelecer uma ligação com fios com o objetivo de implementar um sistema operativo. No entanto, devido um custo e facilidade de utilização geral, estas são muitas vezes adaptadores partilhados. Como o endereço MAC deste adaptador é utilizado para identificar o dispositivo, reutilizar o adaptador fica problemáticas sem ações adicionais administrador entre cada implementação. Agora no Configuration Manager versão 1610, pode excluir o endereço MAC deste adaptador de modo a que possa ser reutilizado facilmente neste cenário.
2. O ID de SMBIOS deveria para ser um identificador de hardware exclusivos, mas alguns dispositivos de hardware specialty são criados com IDs duplicados. Este problema poderá não ser tão comuns, como o cenário de placa de USB para Ethernet apenas descrito, mas pode também abordá-lo utilizando a lista de IDs de hardware excluídos.

Para obter mais detalhes, consulte o artigo [identificadores de hardware duplicados gerir](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers).

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Melhoramentos à loja Windows para a integração de negócio com o Configuration Manager
Alterações nesta versão:
- Anteriormente, apenas pode implementar aplicações gratuitas da loja Windows para empresas. Gestor de configuração agora adicionalmente suporta implementar pago online licenciadas aplicações (para dispositivos do Intune inscritos apenas).
- Agora pode iniciar uma sincronização imediata entre a loja Windows para empresas e do Configuration Manager.
- Agora pode modificar a chave de segredo de cliente obtidas a partir do Azure Active Directory.
- Pode eliminar uma subscrição para a loja.

Para obter mais detalhes, consulte o artigo [gerir aplicações na loja Windows para empresas com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).


## <a name="policy-sync-for-intune-enrolled-devices"></a>Sincronização de política para dispositivos inscritos do Intune
Agora pode pedir uma sincronização de política para um dispositivo inscrito o Intune a partir da consola do Configuration Manager, em vez de necessário especificá-las pedir uma sincronização da aplicação Portal da empresa no dispositivo automaticamente. Informações de estado do pedido de sincronização estão disponíveis como uma nova coluna em vistas de dispositivo, denominado **estado da sincronização de remoto**. As informações também estão disponíveis na secção de dados de deteção do **propriedades** caixa de diálogo para cada dispositivo.
Para obter mais detalhes, consulte o artigo [remotamente sincronizar política em dispositivos inscritos do Intune a partir da consola do Configuration Manager](/sccm/mdm/deploy-use/sync-intune-device).


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Utilize as definições de compatibilidade para configurar definições do Windows Defender
Agora pode configurar as definições de cliente do Windows Defender em computadores Windows 10 inscritos Intune através da utilização de itens de configuração na consola do Configuration Manager.
Para obter detalhes, consulte o **Windows Defender** secção [criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client).



## <a name="general-improvements-to-software-center"></a>Melhoramentos gerais ao centro de Software
- Os utilizadores agora podem solicitar aplicações a partir do Centro de Software, bem como o catálogo de aplicações.
- Melhoramentos para ajudar os utilizadores a compreender a qual o software é novas e relevantes.

## <a name="new-columns-in-device-collection-views"></a>Novas colunas nas vistas de coleção de dispositivos
Agora pode apresentar as colunas para **IMEI** e **número de série** (para dispositivos iOS) nas vistas de coleção do dispositivo.
Para obter mais detalhes, consulte o artigo [Predeclare dispositivos com números de série IMEI ou iOS](https://docs.microsoft.com/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id).

## <a name="customizable-branding-for-software-center-dialogs"></a>Personalizáveis para caixas de diálogo do Centro de Software de imagem corporativa
Imagem corporativa personalizada para o Centro de Software foi introduzida no Configuration Manager versão 1602. Na versão 1610, essa imagem corporativa agora os todas as caixas de diálogo associados para fornecer uma experiência mais consistente aos utilizadores do Centro de Software.

Imagem corporativa personalizada para o Centro de Software é aplicada, de acordo com as seguintes regras:

- Se a função de servidor de sites do ponto de Web site do catálogo de aplicações não está instalada, em seguida, o Centro de Software apresenta o nome da organização especificado no **agente do computador** definição de cliente **nome da organização apresentada no Centro de Software**. Para obter instruções, consulte o artigo [como configurar as definições de cliente](../../clients/deploy/configure-client-settings.md).

- Se estiver instalada a função de servidor de sites do ponto de Web site do catálogo de aplicações, Centro de Software apresenta o nome da organização e a cor especificado nas propriedades de função de servidor de site do catálogo de aplicações Web site ponto. Para obter mais informações, consulte o artigo [opções de configuração de ponto de Web site do catálogo de aplicações](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#Application-Catalog-website-point).

- Se uma subscrição do Microsoft Intune é configurada e ligada ao ambiente do Configuration Manager, em seguida, o Centro de Software apresenta o nome da organização, cor e o logótipo da empresa especificado nas propriedades de subscrição do Intune. Para obter mais informações, veja [Configurar a Subscrição do Microsoft Intune](/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Período de tolerância de imposição para implementações de atualizações de aplicações e de software
Em alguns casos, poderá querer conceder aos utilizadores mais tempo a instale necessário implementações de aplicações ou atualizações de software para além de qualquer prazos que configura. Por exemplo, isto poderá ser necessário quando um computador foi desativado por um determinado período de tempo e tem de instalar um grande número de implementações de aplicação ou atualização. Por exemplo, se um utilizador final apenas tiver devolvido de férias, poderá ter de aguardar por uma longa enquanto como uma aplicação em atraso implementações estão instaladas. Para ajudar a resolver este problema, agora pode definir um período de tolerância de imposição implementando definições de cliente do Configuration Manager a uma coleção. 

Para configurar o período de tolerância, execute as ações seguintes:
1.      No **agente do computador** página de definições de cliente, configure a nova propriedade **período de tolerância para imposição após a implementação do prazo (horas)** com um valor entre **1** e **120** horas.
2.      Uma nova implementação de aplicações necessárias, ou nas propriedades de uma implementação existente, no **agendamento** página, selecione a caixa de verificação **atrasar a imposição desta implementação, de acordo com as preferências do utilizador, até o período de tolerância definido nas definições de cliente**. Todas as implementações que tenham esta caixa de verificação selecionada e são direcionadas para dispositivos em que também implementada o definição de cliente, irão utilizar o período de tolerância de imposição.

Se configurar um período de tolerância de imposição e selecione a caixa de verificação, assim que for atingido o prazo de instalação da aplicação, este será instalado na primeira janela de negócio não que o utilizador configurado até esse período de tolerância. No entanto, o utilizador ainda pode abrir o Centro de Software e instalar a aplicação em qualquer altura que queiram. Depois do período de tolerância expirar, a imposição reverte para comportamento normal para implementações em atraso. Foram adicionadas opções semelhantes ao Assistente de regras de implementação automática, o Assistente de implementação de atualizações de software e páginas de propriedades.



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>Melhoria da funcionalidade nas caixas de diálogo sobre o software necessário
WWhen um utilizador recebe software necessário, a partir de **suspender e avisar-me:** definição, podem selecionar a partir da seguinte na lista pendente de valores: 
- **Mais tarde**. Especifica se as notificações estão agendadas baseada nas definições de notificação configuradas nas definições do agente de cliente.
- **Corrigido tempo**. Especifica que a notificação será agendada para apresentar novamente após o tempo selecionado (por exemplo, em 30 minutos).

![Página de agente de computador nas definições do agente de cliente](media/client-notification-settings.png)

O tempo máximo premir suspender é baseado nos valores de notificação configurados nas definições de agente do cliente. Por exemplo, se o **implementação prazo superior a 24 horas, lembrar utilizadores cada (horas)** definição no computador agente página está configurada para 10 horas e é mais do que 24 horas antes do prazo, o utilizador veria um conjunto de opções de premir suspender até mas nunca maior que 10 horas. Como se aproximar do prazo, a menos opções estão disponíveis e consistente com as definições de agente do cliente relevantes para cada componente da linha de tempo de implementação.

Além disso, para uma implementação de alto risco, tal como uma sequência de tarefas que implementa um sistema operativo, a experiência de notificação do utilizador está agora mais intrusivo. Em vez de uma notificação da barra de tarefas transitório sempre que o utilizador será notificado que manutenção crítica do software é necessária, um caixa de diálogo, tais como a seguinte apresenta no computador do utilizador:

![Caixa de diálogo de Software necessária](media/client-toast-notification.png)


Para obter mais informações:
- [Definições para gerir implementações de alto risco](../../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Como configurar as definições de cliente](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Dashboard de atualizações de software
Utilize o dashboard de atualizações de software novo para ver o estado atual de compatibilidade dos dispositivos na sua organização e analisar rapidamente os dados para ver quais os dispositivos que estão em risco. Para ver o dashboard, navegue para **monitorização** > **descrição geral** > **segurança** > **Dashboard de atualizações de Software**.

Para obter mais detalhes, consulte o artigo [monitorizar atualizações de software](/sccm/sum/deploy-use/monitor-software-updates).


## <a name="improvements-to-the-application-request-process"></a>Melhoramentos para o processo de pedido de aplicação
Depois de aprovou uma aplicação para a instalação, pode escolher subsequentemente negar o pedido clicando **negar** na consola do Configuration Manager. Anteriormente, este botão era indisponíveis, após a aprovação.

Esta ação não fazem com que a aplicação ser desinstalada a partir de todos os dispositivos. No entanto,-impedir os utilizadores de instalar novo cópias da aplicação a partir do Centro de Software.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrar por tamanho do conteúdo nas regras de implementação automática
Agora pode filtrar o tamanho do conteúdo para atualizações de software nas regras de implementação automática. Por exemplo, para transferir apenas as atualizações de software que são mais pequenas do que 2 MB, pode definir o **conteúdo tamanho (KB)** filtro para **< 2048**. Utilizar este filtro impede que as atualizações de software grande transferir automaticamente, que melhor suporte simplificado Windows de nível de manutenção quando a largura de banda de rede é limitada. Para obter mais detalhes, consulte:
- [O Configuration Manager e Windows simplificado manutenção em baixo nível sistemas operativos](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)
- [Implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates)

Para configurar o **conteúdo tamanho (KB)** de campo, efetue um dos seguintes procedimentos:
- Quando cria uma regra de implementação automática, no Assistente Criar regra de implementação automática, aceda ao **atualizações de Software** página.
- Nas propriedades para uma regra de implementação automática existente, vá para o **atualizações de Software** separador.

## <a name="office-365-client-management-dashboard"></a>Dashboard de gestão de clientes do Office 365
O dashboard de gestão de clientes do Office 365 está agora disponível na consola do Configuration Manager. Para ver o dashboard, aceda a **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**.

O dashboard apresenta gráficos para os seguintes:

- Número de clientes do Office 365
- Versões de cliente do Office 365
- Idiomas de cliente do Office 365
- Canais de cliente do Office 365     

Para obter mais detalhes, consulte o artigo [atualizações gerir Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Passos de sequência de tarefas para gerir BIOS para conversão de UEFI
Agora pode personalizar uma sequência de tarefas de implementação do sistema operativo com uma nova variável, TSUEFIDrive, para que o **reiniciar o computador** passo será preparar uma partição FAT32 no disco rígido para transição para UEFI. O procedimento seguinte fornece um exemplo de como pode criar os passos de sequência de tarefas para preparar o disco rígido para o BIOS para conversão de UEFI. Para obter mais detalhes, consulte o artigo [tarefas passos de sequência para gerir BIOS para conversão de UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion).

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>Melhoramentos para o passo de sequência de tarefas: Prepare ConfigMgr Client for Capture  
O passo de preparar ConfigMgr Client agora irá remover completamente o cliente do Configuration Manager, em vez de apenas remoção de informações da chave. Quando a sequência de tarefas, implementa a imagem de sistema operativo capturada, irá instalar um novo cliente de Configuration Manager cada vez. Para obter mais detalhes, consulte o artigo [passos de sequência de tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture).



## <a name="intune-compliance-policy-charts"></a>Gráficos de política de conformidade do Intune
Agora pode obter uma vista rápida de conformidade geral dos dispositivos e o início entre as razões para não conformidade, através de gráficos novo no **monitorização** área de trabalho na consola do Configuration Manager. Pode clicar numa secção do gráfico para descer uma lista dos dispositivos dessa categoria. Para obter mais detalhes, consulte o artigo [monitorizar a política de conformidade](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy).


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>Integração de atento para implementações híbridas proteger os dispositivos iOS e Android
Microsoft é integrar com a solução de proteção de ameaça móvel do atento a proteger dispositivos móveis Android e iOS através da deteção de software maligno, aplicações arriscadas e muito mais, nos dispositivos. Solução do atento ajuda a determinar o nível de ameaças, qual é configurável. Pode criar uma regra de política de conformidade no System Center Configuration Manager, para determinar a compatibilidade do dispositivo com base na avaliação de riscos pelo atento. Utilizar políticas de acesso condicional, pode permitir ou bloquear o acesso aos recursos da empresa com base no estado de conformidade do dispositivo. Para saber mais sobre a integração e como funciona, consulte o artigo [gerir o acesso com base no dispositivo, rede e o risco de aplicação](/sccm/protect/deploy-use/manage-access-based-on-device-network-app-risk).

Os utilizadores de dispositivos não compatíveis iOS serão solicitados que registe. Estarão necessários para instalar o atento para a aplicação de trabalho nos respetivos dispositivos, ativar a aplicação e retificar ameaças comunicadas no atento para aplicação de trabalho obter acesso aos dados da empresa. Saiba como [configurar e implementar atento para aplicações de trabalho](/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps).



## <a name="new-compliance-settings-for-configuration-items"></a>Novas definições de compatibilidade para itens de configuração
Existem muitas novas definições que pode utilizar nos seus itens de configuração de várias plataformas de dispositivo. Estas são as definições que anteriormente existiam no Microsoft Intune numa configuração isolada e estão agora disponíveis ao utilizar o Intune com o Configuration Manager.
Para obter mais detalhes, consulte o artigo [itens de configuração para dispositivos geridos sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/configuration-items-for-devices-managed-without-the-client).

### <a name="new-settings-for-android-devices"></a>Novas definições para dispositivos Android
#### <a name="password-settings"></a>Definições de palavra-passe
- **Memorizar histórico de palavra-passe**
- **Permitir desbloqueio desbloquear**

#### <a name="security-settings"></a>Definições de segurança
- **Encriptação obrigatória nos cartões de armazenamento**
- **Permitir captura de ecrã**
- **Permitir submissão de dados de diagnóstico**

#### <a name="browser-settings"></a>Definições do browser
- **Permitir browser**
- **Permitir Preenchimento automático**
- **Permitir Bloqueador de janelas pop-up**
- **Permitir cookies**
- **Permitir scripting ativo**

#### <a name="app-settings"></a>Definições da aplicação
- **Permitir loja do Google Play**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo
- **Permitir armazenamento amovível**
- **Permitir partilha de Wi-Fi**
- **Permitir geolocalização**
- **Permitir NFC**
- **Permitir Bluetooth**
- **Permitir chamadas em roaming**
- **Permitir roaming de dados**
- **Permitir mensagens SMS/MMS**
- **Permitir Assistente de voz**
- **Permitir marcação por voz**
- **Permitir copiar e colar**

### <a name="new-settings-for-ios-devices"></a>Novas definições para dispositivos iOS
#### <a name="password-settings"></a>Definições de palavra-passe
- **Número de carateres complexos necessários na palavra-passe**
- **Permitir palavras-passe simples**
- **Minutos de inatividade antes da palavra-passe é exigida**
- **Memorizar histórico de palavra-passe**

### <a name="new-settings-for-mac-os-x-devices"></a>Novas definições para dispositivos de Mac OS X
#### <a name="password-settings"></a>Definições de palavra-passe
- **Número de carateres complexos necessários na palavra-passe**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavra-passe**
- **Minutos de inatividade antes de screensaver ativa**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Novas definições para dispositivos móveis e de ambiente de trabalho do Windows 10
#### <a name="password-settings"></a>Definições de palavra-passe
- **Número mínimo de conjuntos de carateres**
- **Memorizar histórico de palavra-passe**
- **Exigir uma palavra-passe quando o dispositivo devolve a partir de um estado inativo**

#### <a name="security-settings"></a>Definições de segurança
- **Encriptação obrigatória no dispositivo móvel**
- **Permitir manual unenrollment**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo
- **Permitir VPN por rede móvel**
- **Permitir roaming de VPN por rede móvel**
- **Permitir a reposição de telefone**
- **Permitir ligação USB**
- **Permitir Cortana**
- **Permitir notificações do Centro de ação**

### <a name="new-settings-for-windows-10-team-devices"></a>Novas definições para dispositivos Windows 10 Team
#### <a name="device-settings"></a>Definições do dispositivo
- **Ativar as informações operacionais do Azure**
- **Ativar Miracast sem fios projeção**
- **Escolha as informações de reunião apresentadas no ecrã de boas-vindas**
- **URL da imagem de fundo Lockscreen**

### <a name="new-settings-for-windows-81-devices"></a>Novas definições para dispositivos Windows 8.1
#### <a name="applicability-settings"></a>Definições de aplicabilidade
- **Aplicar todas as configurações do Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe
- **Tipo de palavra-passe obrigatório**
- **Número mínimo de conjuntos de carateres**
- **Comprimento mínimo da palavra-passe**
- **Número de falhas de início de sessão consecutivas a permitir antes do dispositivo ser apagado**
- **Minutos de inatividade antes do ecrã se desligar**
- **Expiração de palavra-passe (dias)**
- **Memorizar histórico de palavra-passe**
- **Impedir a reutilização de palavras-passe anteriores**
- **Permitir palavra-passe de imagem e PIN**

#### <a name="browser-settings"></a>Definições do browser
- **Permitir deteção automática de rede intranet**

### <a name="new-settings-for-windows-phone-81-devices"></a>Novas definições para dispositivos Windows Phone 8.1
#### <a name="applicability-settings"></a>Definições de aplicabilidade
- **Aplicar todas as configurações do Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe
- **Número mínimo de conjuntos de carateres**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavra-passe**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo
- **Permitir ligação automática a hotspots Wi-Fi**


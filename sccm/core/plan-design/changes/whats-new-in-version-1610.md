---
title: "Nova versão 1610 | Microsoft Docs"
description: "Obter informações sobre as alterações e novas funcionalidades introduzidas na versão 1610 do System Center Configuration Manager."
ms.custom: na
ms.date: 11/23/2016
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
caps.latest.revision: "40"
author: Brenduns
ms.author: brenduns
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 8b80f4d14eafa4cbbfb083178a118bc0e71f4019
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="what39s-new-in-version-1610-of-system-center-configuration-manager"></a>O que &#39; s novidade na versão 1610 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Atualize 1610 para o ramo atual do System Center Configuration Manager está disponível como uma atualização na consola para sites anteriormente instalados com a versão 1511, versão 1602 ou 1606.


> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de linha de base do Configuration Manager.  
>  Saiba mais sobre:    
>  -   [Instalar novos sites](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [Instalar atualizações em sites](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As secções seguintes fornecem detalhes sobre as alterações e novas funcionalidades introduzidas na versão 1610 do Configuration Manager.  


## <a name="in-console-monitoring-of-update-installation-status"></a>Monitorização de estado de instalação da atualização na consola  
A partir da versão 1610, quando é instalado um pacote de atualização e monitorizar a instalação na consola, não há uma fase de novo: **Após a instalação**. Esta fase inclui o estado de tarefas, como reiniciar os serviços de chaves e a inicialização da monitorização de replicação. (Nesta fase não está disponível na consola até após as atualizações de site para a versão 1610.) Para obter mais informações sobre o estado de instalação de atualização, consulte [instalar atualizações na consola](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).


## <a name="exclude-clients-from-automatic-upgrade"></a>Excluir os clientes da atualização automática
Pode excluir os clientes do Windows de introdução atualizado com novas versões do software de cliente. Para tal, inclua os computadores cliente numa coleção especificada que serão excluídas da atualização. Os clientes na coleção excluída ignorar pedidos para atualizar o software de cliente.  Para obter mais informações, consulte [Windows excluir os clientes de atualizações](../../clients/manage/upgrade/exclude-clients-windows.md).


## <a name="improvements-for-boundary-groups"></a>Melhoramentos para os grupos de limites
Versão 1610 introduz alterações importantes para os grupos de limites e como funcionam com pontos de distribuição. Estas alterações podem simplificar a estrutura da sua infraestrutura de conteúdo, ao dando-lhe mais controlo sobre como e quando os pontos de contingência de clientes para procurar distribuição adicionais como localizações de origem de conteúdo. Isto inclui pontos de distribuição baseado na nuvem e no local.
Estas melhorias substituem conceitos e comportamentos que poderá estar familiarizado com (como configurar pontos de distribuição para ser rápida ou lenta). O novo modelo deve ser mais fácil de configurar e manter. Estas alterações também apresentar a base para as alterações futuras que irá melhorar outras funções de sistema de sites, que associar a grupos de limites.

Quando atualizar para versão 1610, a atualização converte das configurações de grupo de limites atuais para ajustar o novo modelo de modo a que estas alterações não disturb as configurações de distribuição de conteúdo existente.

Para obter mais informações, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#a-namebkmkboundarygroupsa-boundary-groups).


## <a name="peer-cache-for-content-distribution-to-clients"></a>Cache ponto a ponto de distribuição de conteúdo para clientes
Início com a versão 1610, cliente **Cache ponto a ponto** ajuda-o a gerir a implementação de conteúdo para clientes em localizações remotas. A Cache é uma solução incorporada do Configuration Manager para os clientes partilhem conteúdos com outros clientes, diretamente a partir da respetiva cache local.

Depois de implementar as definições de cliente que permitem a Cache ponto a ponto numa coleção, os membros dessa coleção podem agir como uma origem de conteúdo ponto a ponto para outros clientes no mesmo grupo de limites.

Também pode utilizar o novo **origens de dados de cliente** dashboard para compreender a utilização de origens de conteúdo de Cache ponto a ponto no seu ambiente.

> [!TIP]  
> Com a versão 1610, a Cache ponto a ponto e o dashboard de origens de dados de cliente são funcionalidades de pré-lançamento. Para ativá-los, consulte o artigo [utilizar as funcionalidades de pré-lançamento das atualizações da](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

Para obter mais informações, consulte [Cache ponto a ponto para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache), e [dashboard de origens de dados de cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrar vários pontos de distribuição partilhado ao mesmo tempo
Agora, pode utilizar a opção de **ponto de distribuição de reatribuir** para que o processo do Configuration Manager em paralelo a reatribuição de até 50 pontos de distribuição partilhados ao mesmo tempo. Antes desta versão, os pontos de distribuição reatribuídas foram processado um de cada vez. Para obter mais informações, consulte [migrar vários pontos de distribuição partilhado ao mesmo tempo](/sccm/core/migration/planning-a-content-deployment-migration-strategy#migrate-multiple-shared-distribution-points-at-the-same-time).

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Gateway de gestão de nuvem para a gestão de clientes baseados na Internet

Gateway de gestão de nuvem fornece uma forma simples de gerir clientes do Configuration Manager na Internet. O serviço de gateway de gestão de nuvem, que é implementado no Microsoft Azure e requer uma subscrição do Azure, liga-se à sua infraestrutura do Configuration Manager no local através de uma nova função de chamar o ponto de ligação de gateway de gestão de nuvem. Assim que tiver completamente implementado e configurado, os clientes podem comunicar com funções de sistema de sites no local do Configuration Manager e os pontos de distribuição baseados na nuvem, independentemente se estão ligados à rede privada interna ou na Internet. Para obter mais informações e para ver como o gateway de gestão de nuvem compara com gestão de clientes baseados na Internet, consulte [gerir clientes na Internet](/sccm/core/clients/manage/manage-clients-internet).

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Melhoramentos à Política de Atualização de Edição do Windows 10
Nesta versão, foram efetuadas as seguintes melhorias para este tipo de política:

- Agora, pode utilizar a política de atualização de edição com PCs Windows 10 que executam o cliente do Configuration Manager, para além dos PCs Windows 10 que são inscritos com o Microsoft Intune.
- Pode atualizar do Windows 10 Professional para qualquer uma das plataformas no Assistente de que são compatíveis com o seu hardware.

## <a name="manage-hardware-identifiers"></a>Gerir os identificadores de hardware
Agora pode fornecer uma lista de IDs deve ignorar do Configuration Manager para fins de registo de cliente e de arranque PXE de hardware. Existem dois problemas comuns que ajuda a endereço:

1. Vários dispositivos, como o 3 Surface Pro, não incluam uma porta Ethernet carregar. Um adaptador USB para Ethernet é geralmente utilizado para estabelecer uma ligação com fios para fins de implementar um sistema operativo. No entanto, devido ao custo e a facilidade de utilização geral, estas são, muitas vezes, adaptadores partilhados. Como o endereço MAC deste adaptador é utilizado para identificar o dispositivo, a reutilizar o adaptador torna-se problemático sem ações adicionais administrador entre cada implementação. Agora no Configuration Manager versão 1610, pode excluir o endereço MAC deste adaptador para que possa ser facilmente reutilizado neste cenário.
2. O ID de SMBIOS deveria para ser um identificador de hardware exclusivos, mas alguns dispositivos de hardware specialty são criados com IDs duplicados. Este problema poderá não estar como comuns, como o cenário de adaptador de USB para Ethernet apenas descrito, mas pode resolvê-lo utilizando a lista de IDs de hardware excluídos.

Para obter mais informações, consulte [identificadores de hardware duplicados gerir](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers).

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Melhoramentos à loja Windows para integração de negócios com o Configuration Manager
Alterações nesta versão:
- Anteriormente, só foi possível implementar aplicações gratuitas da loja Windows para empresas. Gestor de configuração agora adicionalmente suporta a implementação de paga online licenciado aplicações (apenas para dispositivos inscritos no Intune).
- Agora, pode iniciar uma sincronização imediata entre a loja Windows para empresas e o Configuration Manager.
- Agora pode modificar a chave secreta do cliente que obteve do Azure Active Directory.
- Pode eliminar uma subscrição para o arquivo.

Para obter mais informações, consulte [gerir aplicações da loja Windows para empresas com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).


## <a name="policy-sync-for-intune-enrolled-devices"></a>Sincronização de política para dispositivos inscritos no Intune
Agora pode pedir uma sincronização de política para um dispositivo inscritos no Intune a partir da consola do Configuration Manager, em vez de que necessita pedir uma sincronização da aplicação Portal da empresa nos dispositivos de. Informações de estado de pedido de sincronização estão disponíveis como uma nova coluna nas vistas de dispositivo, denominado **estado de sincronização remoto**. As informações também estão disponíveis na secção de dados de deteção do **propriedades** caixa de diálogo para cada dispositivo.
Para obter mais informações, consulte [remotamente sincronizar política nos dispositivos inscritos no Intune a partir da consola do Configuration Manager](/sccm/mdm/deploy-use/sync-intune-device).


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Utilize as definições de compatibilidade para configurar definições do Windows Defender
Agora, pode configurar as definições de cliente do Windows Defender em computadores Windows 10 inscritos no Intune através da utilização de itens de configuração na consola do Configuration Manager.
Para obter mais informações, consulte o **Windows Defender** secção [criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client).



## <a name="general-improvements-to-software-center"></a>Melhoramentos gerais ao centro de Software
- Os utilizadores agora podem pedir aplicações a partir do Centro de Software, bem como o catálogo de aplicações.
- Melhoramentos para ajudar os utilizadores a compreender o tipo de software é novo e relevantes.

## <a name="new-columns-in-device-collection-views"></a>Novas colunas nas vistas de coleção de dispositivos
Agora pode apresentar colunas para **IMEI** e **número de série** (para dispositivos iOS) em vistas de coleção do dispositivo.
Para obter mais detalhes, consulte [pré-declarar dispositivos com números de série iOS ou IMEI](https://docs.microsoft.com/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id).

## <a name="customizable-branding-for-software-center-dialogs"></a>Personalizável de imagem corporativa para caixas de diálogo do Centro de Software
Uma imagem corporativa personalizado para o Centro de Software introduzida no Configuration Manager versão 1602. Na versão 1610, essa imagem corporativa abranger agora todas as caixas de diálogo associada para fornecer uma experiência mais consistente para utilizadores do Centro de Software.

Uma imagem corporativa personalizado para o Centro de Software é aplicada, de acordo com as seguintes regras:

- Se a função de servidor de sites do ponto de Web site do catálogo de aplicações não está instalada, em seguida, o Centro de Software apresenta o nome da organização especificado no **agente do computador** definição de cliente **nome da organização apresentada no Centro de Software**. Para obter instruções, consulte [como configurar as definições de cliente](../../clients/deploy/configure-client-settings.md).

- Se estiver instalada a função de servidor de sites do ponto de Web site do catálogo de aplicações, Centro de Software apresenta o nome da organização e a cor especificados nas propriedades de função do servidor de ponto de sites catálogo de aplicações Web site. Para obter mais informações, consulte [opções de configuração para o ponto de Web site do catálogo de aplicações](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#Application-Catalog-website-point).

- Se uma subscrição do Microsoft Intune estiver configurada e ligada ao ambiente do Configuration Manager, em seguida, o Centro de Software apresenta o nome da organização, a cor e o logótipo da empresa especificados nas propriedades de subscrição do Intune. Para obter mais informações, veja [Configurar a Subscrição do Microsoft Intune](/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Período de tolerância de imposição para implementações de atualizações de aplicações e de software
Em alguns casos, pode querer dar aos utilizadores mais tempo para as implementações de aplicações de instalação necessária ou atualizações de software para além de qualquer prazos que configurou. Por exemplo, isto poderá ser necessário quando um computador foi desativado por um longo período de tempo e tem de instalar um grande número de implementações de aplicação ou atualização. Por exemplo, se um utilizador final tiver apenas devolvido de férias, poderá ter de aguardar algum enquanto como uma aplicação em atraso implementações estão instaladas. Para ajudar a resolver este problema, agora pode definir um período de tolerância de imposição ao implementar as definições de cliente do Configuration Manager para uma coleção. 

Para configurar o período de tolerância, efetuar as seguintes ações:
1.      No **agente do computador** página de definições de cliente, configure a nova propriedade **período de tolerância para a imposição após a implementação do prazo (horas)** com um valor entre **1** e **120** horas.
2.      Uma nova implementação de aplicação necessária, ou nas propriedades de uma implementação existente, no **agendamento** página, selecione a caixa de verificação **atrasar imposição para esta implementação, de acordo com as preferências do utilizador, até ao período de tolerância definido nas definições de cliente**. Todas as implementações que tenham esta caixa de verificação selecionada e são direcionadas para os dispositivos nos quais tiver implementado também o definição de cliente utilizará o período de tolerância de imposição.

Se configurar um período de tolerância de imposição e selecione a caixa de verificação, assim que for atingido o prazo de instalação da aplicação, será instalado na primeira janela de empresa-empresa que o utilizador configurado até esse período de tolerância. No entanto, o utilizador pode ainda abrir o Centro de Software e instalar a aplicação em qualquer altura em que pretende. Depois do período de tolerância expirar, imposição reverte para o comportamento normal para implementações em atraso. Foram adicionadas opções semelhantes para o Assistente de implementação de atualizações de software, o Assistente de regras de implementação automática e páginas de propriedades.



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>Funcionalidade melhorada nas caixas de diálogo sobre o software necessário
Quando um utilizador recebe o software necessário, do **Snooze e avisar-me Depois:** definição, podem selecionar a partir da seguinte na lista pendente de valores: 
- **Mais tarde**. Especifica que as notificações são agendadas baseada nas definições de notificação configuradas nas definições do agente de cliente.
- **Corrigido tempo**. Especifica que a notificação será agendada para apresentar novamente após a hora selecionada (por exemplo, no 30 minutos).

![Página de agente do computador nas definições do agente de cliente](media/client-notification-settings.png)

O tempo de suspensão máxima é com base nos valores de notificação configurados nas definições do agente do cliente. Por exemplo, se o **implementação prazo superior a 24 horas, lembrar utilizadores cada (horas)** definição no computador agente página está configurada para 10 horas e é mais de 24 horas antes do prazo, o utilizador pretende ver um conjunto de opções de suspensão até mas nunca superior a 10 horas. Como se aproxima do prazo, menos opções estão disponíveis, consistente com as definições de agente do cliente relevantes para cada componente da linha cronológica de implementação.

Além disso, para uma implementação de alto risco, como uma sequência de tarefas que implementa um sistema operativo, a experiência de notificação do utilizador é agora mais intrusivo. Em vez de uma notificação de barra de tarefas transitório, sempre que o utilizador é notificado de que a manutenção crítica do software é necessária, um caixa de diálogo, tais como a apresenta seguintes no computador do utilizador:

![Caixa de diálogo de Software necessária](media/client-toast-notification.png)


Para obter mais informações:
- [Definições para gerir implementações de alto risco](../../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Como configurar as definições do cliente](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Dashboard de atualizações de software
Utilize o dashboard de atualizações de software novo para ver o estado atual de compatibilidade dos dispositivos na sua organização e analisar rapidamente os dados para ver os dispositivos que estão em risco. Para ver o dashboard, navegue até à **monitorização** > **descrição geral** > **segurança** > **Dashboard de atualizações de Software**.

Para obter mais informações, consulte [monitorizar atualizações de software](/sccm/sum/deploy-use/monitor-software-updates).


## <a name="improvements-to-the-application-request-process"></a>Melhoramentos ao processo de pedido de aplicação
Depois de aprovar uma aplicação para a instalação, pode, subsequentemente, optar por negar o pedido ao clicar em **negar** na consola do Configuration Manager. Anteriormente, este botão era a cinzento após a aprovação.

Esta ação não irá causar a aplicação a ser desinstalados a partir de qualquer dispositivo. No entanto, este impedir que os utilizadores de instalar novas cópias da aplicação a partir do Centro de Software.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrar pelo tamanho do conteúdo nas regras de implementação automática
Agora pode filtrar o tamanho do conteúdo para atualizações de software nas regras de implementação automática. Por exemplo, para transferir apenas atualizações de software que são inferior a 2 MB, pode definir o **conteúdo tamanho (KB)** filtrar para **< 2048**. Utilizar este filtro impede que as atualizações de software grande transferir automaticamente, que suporta melhor simplificado de nível baixo de manutenção quando a largura de banda de rede do Windows. Para obter mais informações, consulte:
- [Gestor de configuração e manutenção do Windows simplificada em baixo nível sistemas operativos](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)
- [Implementar atualizações de software automaticamente](/sccm/sum/deploy-use/automatically-deploy-software-updates)

Para configurar o **conteúdo tamanho (KB)** campo, efetue um dos seguintes:
- Quando cria uma regra de implementação automática, o Assistente Criar regra de implementação automática, vá para o **atualizações de Software** página.
- Nas propriedades de uma regra de implementação automática existente, vá para o **atualizações de Software** separador.

## <a name="office-365-client-management-dashboard"></a>Dashboard de gestão de clientes do Office 365
O dashboard de gestão de clientes do Office 365 está agora disponível na consola do Configuration Manager. Para ver o dashboard, aceda a **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**.

O dashboard apresenta gráficos para o seguinte:

- Número de clientes do Office 365
- Versões de cliente do Office 365
- Idiomas de cliente do Office 365
- Canais de cliente do Office 365     

Para obter mais informações, consulte [de atualizações de gerir o Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Passos de sequência de tarefas para gerir o BIOS para conversão de UEFI
Agora pode personalizar uma sequência de tarefas de implementação do sistema operativo com uma nova variável, TSUEFIDrive, para que o **reiniciar o computador** passo irá preparar uma partição FAT32 no disco rígido para transição para UEFI. O procedimento seguinte fornece um exemplo de como pode criar os passos de sequência de tarefas para preparar a unidade de disco rígido para o BIOS para conversão de UEFI. Para obter mais informações, consulte [para gerir o BIOS para conversão de UEFI, os passos de sequência de tarefas](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion).

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>Melhoramentos para o passo de sequência de tarefas: Prepare ConfigMgr Client for Capture  
O passo de preparar ConfigMgr Client agora removerá totalmente o cliente do Configuration Manager, em vez de apenas remover informações de chave. Quando a sequência de tarefas, implementa a imagem do sistema operativo capturada, este irá instalar um novo cliente de Configuration Manager cada vez. Para obter mais informações, consulte [passos de sequência de tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture).



## <a name="intune-compliance-policy-charts"></a>Gráficos de política de conformidade do Intune
Agora pode obter uma vista rápida de conformidade geral dos dispositivos e, na parte superior motivos pelos quais da não conformidade, utilizando o novo gráficos sob o **monitorização** área de trabalho na consola do Configuration Manager. Pode clicar uma secção do gráfico para desagregar para obter uma lista dos dispositivos dessa categoria. Para obter mais informações, consulte [monitorizar a política de conformidade](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy).


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>Integração de lookout para implementações híbridas proteger dispositivos iOS e Android
Microsoft é integrar a solução de proteção do Lookout ameaça móveis para proteger dispositivos iOS e Android móveis através da deteção de software maligno, aplicações arriscadas e muito mais, nos dispositivos. Solução do lookout ajuda a determinar o nível de ameaças, que é configurável. Pode criar uma regra de política de conformidade no System Center Configuration Manager, para determinar a compatibilidade do dispositivo com base na avaliação de riscos Lookout. Utilizar políticas de acesso condicional, pode permitir ou bloquear o acesso aos recursos da empresa com base no estado de conformidade do dispositivo. Para saber mais sobre a integração e como funciona, consulte [gerir acesso com base no dispositivo, rede e o risco de aplicação](/sccm/protect/deploy-use/manage-access-based-on-device-network-app-risk).

Os utilizadores de dispositivos não conformes iOS serão solicitados a inscrição. Estejam necessários para instalar o Lookout para a aplicação de trabalho nos respetivos dispositivos, ativar a aplicação e remedeie ameaças comunicadas no Lookout para aplicação de trabalho para obterem acesso aos dados da empresa. Saiba como [configurar e implementar o Lookout para aplicações de trabalho](/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps).



## <a name="new-compliance-settings-for-configuration-items"></a>Novas definições de conformidade para itens de configuração
Existem várias novas definições, que pode utilizar os itens de configuração para várias plataformas de dispositivos. Estas são as definições que existiam no Microsoft Intune numa configuração autónoma e anteriormente estão agora disponíveis ao utilizar o Intune com o Configuration Manager.
Para obter mais informações, consulte [itens de configuração para dispositivos geridos sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/configuration-items-for-devices-managed-without-the-client).

### <a name="new-settings-for-android-devices"></a>Novas definições para dispositivos Android
#### <a name="password-settings"></a>Definições de palavra-passe
- **Memorizar histórico de palavra-passe**
- **Permitir impressões digitais desbloquear**

#### <a name="security-settings"></a>Definições de segurança
- **Exigir encriptação em cartões de armazenamento**
- **Permitir captura de ecrã**
- **Permitir submissão de dados de diagnóstico**

#### <a name="browser-settings"></a>Definições do browser
- **Permitir browser**
- **Permitir Preenchimento automático**
- **Permitir Bloqueador de janelas de pop-up**
- **Permitir cookies**
- **Permitir scripting ativo**

#### <a name="app-settings"></a>Definições de aplicação
- **Permitir loja do Google Play**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo
- **Permitir armazenamento amovível**
- **Permitir tethering Wi-Fi**
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

### <a name="new-settings-for-mac-os-x-devices"></a>Novas definições para dispositivos Mac OS X
#### <a name="password-settings"></a>Definições de palavra-passe
- **Número de carateres complexos necessários na palavra-passe**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavra-passe**
- **Minutos de inatividade antes da proteção de ecrã ser ativada**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Novas definições para dispositivos Windows 10 Desktop e Mobile
#### <a name="password-settings"></a>Definições de palavra-passe
- **Número mínimo de conjuntos de carateres**
- **Memorizar histórico de palavra-passe**
- **Exigir uma palavra-passe quando o dispositivo regressa de um estado inativo**

#### <a name="security-settings"></a>Definições de segurança
- **Encriptação obrigatória no dispositivo móvel**
- **Permitir anular inscrições**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo
- **Permitir VPN sobre redes móveis**
- **Permitir roaming do VPN sobre redes móveis**
- **Permitir reposição do telefone**
- **Permitir ligação USB**
- **Permitir Cortana**
- **Permitir notificações de centro de ação**

### <a name="new-settings-for-windows-10-team-devices"></a>Novas definições para dispositivos Windows 10 Team
#### <a name="device-settings"></a>Definições do dispositivo
- **Ativar a informações operacionais do Azure**
- **Ativar projeção sem fios Miracast**
- **Escolha as informações de reunião apresentadas no ecrã de boas-vindas**
- **URL de imagem de fundo do ecrã de bloqueio**

### <a name="new-settings-for-windows-81-devices"></a>Novas definições para dispositivos Windows 8.1
#### <a name="applicability-settings"></a>Definições de aplicabilidade
- **Aplicar todas as configurações ao Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe
- **Tipo de palavra-passe obrigatório**
- **Número mínimo de conjuntos de carateres**
- **Comprimento mínimo da palavra-passe**
- **Número de falhas de início de sessão repetidas permitidas antes do dispositivo ser apagado**
- **Minutos de inatividade antes do ecrã se desligar**
- **Expiração da palavra-passe (dias)**
- **Memorizar histórico de palavra-passe**
- **Impedir a reutilização de palavras-passe anteriores**
- **Permitir palavra-passe de imagem e PIN**

#### <a name="browser-settings"></a>Definições do browser
- **Permitir deteção automática de rede intranet**

### <a name="new-settings-for-windows-phone-81-devices"></a>Novas definições para dispositivos Windows Phone 8.1
#### <a name="applicability-settings"></a>Definições de aplicabilidade
- **Aplicar todas as configurações ao Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe
- **Número mínimo de conjuntos de carateres**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavra-passe**

#### <a name="device-capability-settings"></a>Definições de capacidade de dispositivo
- **Permitir ligação automática a hotspots Wi-Fi**

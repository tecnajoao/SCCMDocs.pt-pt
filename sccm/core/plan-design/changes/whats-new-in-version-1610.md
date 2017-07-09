---
title: "Nova versão 1610 | Microsoft Docs"
description: "Obter detalhes sobre as alterações e novos recursos introduzidos na versão 1610 do System Center Configuration Manager."
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
ms.sourcegitcommit: db673277d1cc2d24e8dba2439b2b1891c883ebd0
ms.openlocfilehash: 8b80f4d14eafa4cbbfb083178a118bc0e71f4019
ms.contentlocale: pt-pt
ms.lasthandoff: 06/16/2017

---
# <a name="what39s-new-in-version-1610-of-system-center-configuration-manager"></a>O que &#39; s novo na versão 1610 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Atualize 1610 para a ramificação atual do System Center Configuration Manager está disponível como uma atualização no console para sites previamente instalados que executam a versão 1511, 1602 ou 1606.


> [!TIP]  
> Para instalar um novo site, você deve usar uma versão de linha de base do Configuration Manager.  
>  Saiba mais sobre:    
>  -   [Instalar novos sites](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [Instalar atualizações em sites](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As seções a seguir fornecem detalhes sobre as alterações e novos recursos introduzidos na versão 1610 do Configuration Manager.  


## <a name="in-console-monitoring-of-update-installation-status"></a>No console de monitoramento do status de instalação de atualização  
Começando com a versão 1610, quando você instala um pacote de atualização e monitorar a instalação no console do, há uma nova fase: **Pós-instalação**. Esta fase inclui o status de tarefas como reiniciar os serviços de chave e inicialização de monitoramento da replicação. (Essa fase não está disponível no console até após as atualizações do site para a versão 1610.) Para obter mais informações sobre o status de instalação de atualização, consulte [instalar atualizações no console](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).


## <a name="exclude-clients-from-automatic-upgrade"></a>Excluir os clientes da atualização automática
Você pode excluir os clientes do Windows de ser atualizado com novas versões do software cliente. Para fazer isso, você pode incluir os computadores cliente em uma coleção especificada a ser excluído da atualização. Clientes na coleção excluída ignoram solicitações para atualizar o software cliente.  Para obter mais informações, consulte [clientes Windows excluir de atualizações](../../clients/manage/upgrade/exclude-clients-windows.md).


## <a name="improvements-for-boundary-groups"></a>Aprimoramentos para grupos de limites
A versão 1610 introduz alterações importantes para grupos de limites e como elas funcionam com pontos de distribuição. Essas alterações podem simplificar o design de sua infraestrutura de conteúdo, dando a você mais controle sobre como e quando pontos de fallback de clientes para distribuição adicionais de pesquisa como locais de origem de conteúdo. Isso inclui locais e pontos de distribuição baseado em nuvem.
Esses aprimoramentos substitua conceitos e comportamentos, que você pode estar familiarizado com (como configurar pontos de distribuição para ser rápida ou lenta). O novo modelo deve ser mais fácil de configurar e manter. Essas alterações também definir as bases para alterações futuras que melhoram a outras funções do sistema de site associado a grupos de limites.

Quando você atualizar para a versão 1610, a atualização converte suas configurações de grupo de limite atual de acordo com o novo modelo para que essas alterações não interfira forma suas configurações de distribuição de conteúdo existente.

Para obter mais informações, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#a-namebkmkboundarygroupsa-boundary-groups).


## <a name="peer-cache-for-content-distribution-to-clients"></a>Cache de sistemas pares para distribuição de conteúdo para clientes
Começando com a versão 1610, o cliente **Cache par** ajuda você a gerenciar a implantação de conteúdo para clientes em locais remotos. Cache de mesmo nível é uma solução interna do Configuration Manager para que os clientes compartilhem conteúdo com outros clientes diretamente do seu cache local.

Depois de implantar configurações de cliente que habilitar o Cache de mesmo nível em uma coleção, membros da coleção podem agir como uma fonte de conteúdo de sistemas pares para outros clientes no mesmo grupo de limites.

Você também pode usar o novo **fontes de dados do cliente** painel para entender o uso de fontes de conteúdo de Cache de mesmo nível no seu ambiente.

> [!TIP]  
> Com a versão 1610, Cache de mesmo nível e o painel de fontes de dados do cliente são recursos de pré-lançamento. Para habilitá-las, consulte [usar recursos de pré-lançamento de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

Para obter mais informações, consulte [Cache par para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache), e [painel fontes de dados do cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrar vários pontos de distribuição compartilhados ao mesmo tempo
Agora você pode usar a opção de **reatribuir ponto de distribuição** para que o processo do Configuration Manager em paralelo a reatribuição de até 50 pontos de distribuição compartilhados ao mesmo tempo. Antes desta versão, os pontos de distribuição reatribuídos foram processados um de cada vez. Para obter mais informações, consulte [migrar vários pontos de distribuição compartilhados ao mesmo tempo](/sccm/core/migration/planning-a-content-deployment-migration-strategy#migrate-multiple-shared-distribution-points-at-the-same-time).

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Gateway de gerenciamento de nuvem para o gerenciamento de clientes baseados na Internet

Gateway de gerenciamento de nuvem fornece uma maneira simple de gerenciar clientes do Configuration Manager na Internet. O serviço de gateway de gerenciamento de nuvem, que é implantado no Microsoft Azure e requer uma assinatura do Azure, conecta-se à sua infraestrutura do Configuration Manager local usando uma nova função chamada o ponto de conexão de gateway de gerenciamento de nuvem. Depois que ele foi totalmente implantado e configurado, os clientes podem se comunicar com funções de sistema de site do Configuration Manager local e pontos de distribuição baseado em nuvem, independentemente se eles estão conectados à rede interna privada ou na Internet. Para obter mais informações e ver como o gateway de gerenciamento de nuvem compara com o gerenciamento de clientes baseados na Internet, consulte [gerenciar clientes na Internet](/sccm/core/clients/manage/manage-clients-internet).

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Melhoramentos à Política de Atualização de Edição do Windows 10
Nesta versão, as seguintes melhorias foram feitas para este tipo de política:

- Agora você pode usar a política de atualização de edição com computadores com Windows 10 que executam o cliente do Configuration Manager, além de PCs com Windows 10 registrados com o Microsoft Intune.
- Você pode atualizar do Windows 10 Professional para qualquer uma das plataformas que são compatíveis com o hardware no assistente.

## <a name="manage-hardware-identifiers"></a>Gerenciar os identificadores de hardware
Agora você pode fornecer uma lista de IDs devem ignorar o Configuration Manager para fins de registro de cliente e de inicialização PXE de hardware. Há dois problemas comuns que isso ajuda a:

1. Muitos dispositivos, como 3 o Surface Pro, não incluem uma porta Ethernet integrada. Um adaptador USB-Ethernet geralmente é usado para estabelecer uma conexão com fio com a finalidade de implantar um sistema operacional. No entanto, devido ao custo e facilidade de uso geral, eles costumam adaptadores compartilhados. Como o endereço MAC desse adaptador é usado para identificar o dispositivo, reutilizar o adaptador se torna problemático sem ação adicional do administrador entre cada implantação. Agora no Configuration Manager versão 1610, você pode excluir o endereço MAC desse adaptador para que ele pode ser facilmente reutilizado neste cenário.
2. A ID de SMBIOS deve para ser um identificador de hardware exclusiva, mas alguns dispositivos de hardware especializado criados com IDs duplicadas. Esse problema pode não ser tão comum quanto o cenário do adaptador USB-Ethernet acabamos de descrever, mas você poderá solucioná-lo usando a lista de IDs de hardware excluídos.

Para obter detalhes, consulte [identificadores de hardware duplicadas gerenciar](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers).

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Aprimoramentos da Windows Store para a integração de negócios com o Configuration Manager
Alterações nesta versão:
- Anteriormente, você só pode implantar aplicativos gratuitos da Windows Store para empresas. Gerenciador de configuração agora Além disso oferece suporte à implantação paga online licenciado aplicativos (registrados no Intune somente para dispositivos).
- Agora você pode iniciar uma sincronização imediata entre a Windows Store para empresas e o Configuration Manager.
- Agora você pode modificar a chave secreta do cliente que você obteve do Active Directory do Azure.
- Você pode excluir uma assinatura para o repositório.

Para obter detalhes, consulte [gerenciar aplicativos da Windows Store para empresas com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).


## <a name="policy-sync-for-intune-enrolled-devices"></a>Sincronização de política para dispositivos registrados pelo Intune
Agora você pode solicitar uma sincronização de política para um dispositivo registrado pelo Intune no console do Configuration Manager, em vez de precisar solicitar uma sincronização do aplicativo Portal da empresa no dispositivo. Informações de estado de solicitação de sincronização estão disponíveis como uma nova coluna em modos de exibição do dispositivo, chamado **estado de sincronização remoto**. As informações também estão disponíveis na seção de dados de descoberta do **propriedades** caixa de diálogo para cada dispositivo.
Para obter detalhes, consulte [sincronizar remotamente a diretiva em dispositivos registrados pelo Intune no console do Configuration Manager](/sccm/mdm/deploy-use/sync-intune-device).


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Use as configurações de conformidade para definir as configurações do Windows Defender
Agora você pode configurar as configurações de cliente do Windows Defender em computadores registrados pelo Intune Windows 10 usando os itens de configuração no console do Configuration Manager.
Para obter detalhes, consulte o **Windows Defender** seção [criar itens de configuração para dispositivos Windows 8.1 e Windows 10 gerenciados sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client).



## <a name="general-improvements-to-software-center"></a>Aperfeiçoamentos gerais no Centro de Software
- Os usuários agora podem solicitar aplicativos do Centro de Software, bem como o catálogo de aplicativos.
- Melhorias para ajudar os usuários a entender o software que é novo e relevante.

## <a name="new-columns-in-device-collection-views"></a>Novas colunas nas exibições de coleção de dispositivo
Agora você pode exibir as colunas para **IMEI** e **número de série** (para dispositivos iOS) em exibições de coleção do dispositivo.
Para obter mais detalhes, consulte [pré-declarar dispositivos com números de série do iOS ou IMEI](https://docs.microsoft.com/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id).

## <a name="customizable-branding-for-software-center-dialogs"></a>Personalizável de identidade visual para caixas de diálogo do Centro de Software
Identidade visual personalizada para o Centro de Software foi introduzido no Configuration Manager versão 1602. Na versão 1610, essa marca é estendido para todas as caixas de diálogo associada para oferecer uma experiência mais consistente aos usuários do Centro de Software.

Identidade visual personalizada para o Centro de Software é aplicada de acordo com as regras a seguir:

- Se a função de servidor de site do catálogo de aplicativos site ponto não está instalada, o Centro de Software exibe o nome da organização especificado no **computador agente** configuração do cliente **nome da organização exibido no Centro de Software**. Para obter instruções, consulte [como definir as configurações de cliente](../../clients/deploy/configure-client-settings.md).

- Se a função de servidor de site do catálogo de aplicativos site ponto estiver instalada, o Centro de Software exibe o nome da organização e a cor especificado nas propriedades de função de servidor de site de catálogo de aplicativos site ponto. Para obter mais informações, consulte [opções de configuração de ponto de sites do catálogo de aplicativos](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#Application-Catalog-website-point).

- Se uma assinatura Microsoft Intune está configurada e conectada ao ambiente do Configuration Manager, em seguida, o Centro de Software exibe o nome da organização, a cor e o logotipo da empresa especificado nas propriedades de assinatura do Intune. Para obter mais informações, veja [Configurar a Subscrição do Microsoft Intune](/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Período de tolerância de imposição para implementações de atualizações de aplicações e de software
Em alguns casos, você talvez queira dar aos usuários mais tempo para implantações de aplicativo de instalação necessários ou atualizações de software, além de qualquer prazos que você configurar. Por exemplo, isso pode ser necessário quando um computador foi desligado por um longo período de tempo e precisa instalar um grande número de implantações de aplicativo ou atualização. Por exemplo, se um usuário final apenas foi retornado de férias, eles talvez precise aguardar um longo enquanto como aplicativo vencido implantações são instaladas. Para ajudar a resolver esse problema, agora você pode definir um período de cortesia de imposição Implantando as configurações de cliente do Configuration Manager para uma coleção. 

Para configurar o período de cortesia, execute as seguintes ações:
1.      Sobre o **agente de computador** página de configurações do cliente, configure a nova propriedade **período de cortesia para imposição após a implantação do prazo (horas)** com um valor entre **1** e **120** horas.
2.      Em uma nova implantação de aplicativo necessário ou nas propriedades de uma implantação existente, no **agendamento** , marque a caixa de seleção **atrase a imposição dessa implantação de acordo com as preferências do usuário, até o período de carência definido nas configurações do cliente**. Todas as implantações que têm a caixa de seleção e são destinadas a dispositivos aos quais você implantou o configuração do cliente, também usará o período de cortesia de imposição.

Se você configurar um período de cortesia de imposição e selecione a caixa de seleção, quando o prazo de instalação do aplicativo é atingido, ele será instalado na primeira janela de negócios não que o usuário configurado até esse período de carência. No entanto, o usuário ainda pode abrir o Centro de Software e instalar o aplicativo a qualquer momento que desejarem. Quando o período de cortesia expirar, imposição será revertido para o comportamento normal para implantações vencidas. Opções similares foram adicionadas para o Assistente de implantação de atualizações de software, Assistente de implantação automática de regras e as páginas de propriedades.



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>Funcionalidade aprimorada em caixas de diálogo sobre o software necessário
Quando um usuário recebe o software necessário, do **adiar e lembrar-me:** configuração, pode selecionar na lista a seguir lista suspensa de valores: 
- **Mais tarde**. Especifica que as notificações são agendadas com base nas configurações de notificação configuradas nas configurações do agente de cliente.
- **Tempo fixo**. Especifica que a notificação será agendada para ser exibida novamente após o tempo selecionado (por exemplo, em 30 minutos).

![Página de agente de computador nas configurações do agente de cliente](media/client-notification-settings.png)

O tempo máximo de suspensão se baseia nos valores de notificação configurados nas configurações do agente do cliente. Por exemplo, se o **implantação prazo superior a 24 horas, lembrar usuários cada (horas)** configuração no computador agente página está configurada para 10 horas e é mais de 24 horas antes do prazo, o usuário vê um conjunto de opções de suspensão até, mas nunca maior que 10 horas. Conforme o prazo se aproxima, menos opções estão disponíveis, consistente com as configurações de agente cliente relevantes para cada componente da linha do tempo de implantação.

Além disso, para uma implantação de alto risco, como uma sequência de tarefas que implanta um sistema operacional, a experiência de notificação do usuário agora é mais intrusiva. Em vez de uma notificação transitória da barra de tarefas, cada vez que o usuário será notificado de que a manutenção de softwares críticos é necessária, um caixa de diálogo, como a seguinte será exibida no computador do usuário:

![Caixa de diálogo de Software necessária](media/client-toast-notification.png)


Para obter mais informações:
- [Configurações para gerenciar implantações de alto risco](../../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Como configurar as definições do cliente](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Painel de atualizações de software
Use o novo painel de atualizações de software para exibir o status atual de conformidade de dispositivos em sua organização e analisar rapidamente os dados para ver quais dispositivos estão em risco. Para exibir o painel, navegue até **monitoramento** > **visão geral** > **segurança** > **painel de atualizações de Software**.

Para obter detalhes, consulte [monitorar atualizações de software](/sccm/sum/deploy-use/monitor-software-updates).


## <a name="improvements-to-the-application-request-process"></a>Aprimoramentos para o processo de solicitação do aplicativo
Depois de você aprovar um aplicativo para a instalação, você pode escolher subsequentemente para negar a solicitação clicando **Deny** no console do Configuration Manager. Anteriormente, esse botão foi desabilitado após a aprovação.

Esta ação não faz com que o aplicativo ser desinstalado dos dispositivos. No entanto, ele impedir que os usuários instalem novas cópias do aplicativo do Centro de Software.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrar por tamanho do conteúdo nas regras de implantação automática
Agora você pode filtrar o tamanho do conteúdo para atualizações de software em regras de implantação automática. Por exemplo, para baixar apenas as atualizações de software que são menores que 2 MB, você pode definir o **conteúdo tamanho (KB)** filtrar para **< 2048**. Usar este filtro impede que atualizações de software grandes baixando automaticamente, que dá suporte a melhor simplificado Windows quando a largura de banda de rede está limitada de serviço de nível inferior. Para obter detalhes, consulte:
- [O Configuration Manager e o serviço do Windows simplificado em sistemas de operacionais de nível](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)
- [Implementar atualizações de software automaticamente](/sccm/sum/deploy-use/automatically-deploy-software-updates)

Para configurar o **conteúdo tamanho (KB)** campo, faça o seguinte:
- Quando você cria uma regra de implantação automática, no Assistente Criar regra de implantação automática, vá para o **atualizações de Software** página.
- Nas propriedades de uma regra de implantação automática existente, vá para o **atualizações de Software** guia.

## <a name="office-365-client-management-dashboard"></a>Painel de gerenciamento de clientes do Office 365
O painel de gerenciamento de cliente do Office 365 agora está disponível no console do Configuration Manager. Para exibir o painel de controle, vá para **biblioteca de Software** > **visão geral** > **gerenciamento de cliente do Office 365**.

O painel exibe gráficos para o seguinte:

- Número de clientes do Office 365
- Versões de cliente do Office 365
- Idiomas do cliente Office 365
- Canais de cliente do Office 365     

Para obter detalhes, consulte [atualizações de gerenciar o Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Etapas de sequência de tarefas para gerenciar o BIOS para conversão de UEFI
Agora você pode personalizar uma sequência de tarefas de implantação de sistema operacional com uma nova variável, TSUEFIDrive, para que o **Reiniciar computador** etapa será preparar uma partição FAT32 no disco rígido para transição para UEFI. O procedimento a seguir fornece um exemplo de como você pode criar etapas de sequência de tarefas para preparar o disco rígido para o BIOS a conversão de UEFI. Para obter detalhes, consulte [etapas para gerenciar o BIOS para conversão de UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion).

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>Melhorias para a etapa de sequência de tarefas: Prepare ConfigMgr Client for Capture  
A etapa preparar cliente ConfigMgr agora remover completamente o cliente do Configuration Manager, em vez de apenas remover informações de chave. Quando a sequência de tarefas implanta a imagem capturada do sistema operacional, ele instalará um novo cliente do Configuration Manager cada vez. Para obter detalhes, consulte [etapas da sequência de tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture).



## <a name="intune-compliance-policy-charts"></a>Gráficos de política de conformidade do Intune
Agora você pode obter uma visão geral de conformidade geral para os dispositivos e os principais motivos para não conformidade, usando novos gráficos sob o **monitoramento** espaço de trabalho no console do Configuration Manager. Você pode clicar em uma seção do gráfico para fazer drill down até uma lista de dispositivos nessa categoria. Para obter detalhes, consulte [monitorar a política de conformidade](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy).


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>Integração de bloqueio para implementações híbridas proteger dispositivos iOS e Android
Microsoft é integrando a solução de proteção de ameaças móveis do bloqueio para proteger dispositivos móveis Android e iOS pela detecção de malware, aplicativos arriscados e muito mais em dispositivos. Solução de alerta ajuda a determinar o nível de ameaça, que é configurável. Você pode criar uma regra de política de conformidade no System Center Configuration Manager para determinar a conformidade do dispositivo com base na avaliação de riscos por consulta. Usando políticas de acesso condicional, você pode permitir ou bloquear o acesso aos recursos da empresa com base no status de conformidade do dispositivo. Para saber mais sobre a integração e como ele funciona, consulte [gerenciar acesso com base em risco de aplicativos, rede e dispositivo](/sccm/protect/deploy-use/manage-access-based-on-device-network-app-risk).

Usuários de dispositivos iOS não compatíveis serão solicitados para registrar. Eles serão necessários para instalar o bloqueio para trabalho de aplicativo em seus dispositivos, ative o aplicativo e corrigir ameaças relatadas no alerta para o aplicativo de trabalho obter acesso aos dados da empresa. Saiba como [configurar e implantar o bloqueio para aplicativos de trabalho](/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps).



## <a name="new-compliance-settings-for-configuration-items"></a>Novas configurações de conformidade para itens de configuração
Há muitas novas configurações, que você pode usar em seus itens de configuração para várias plataformas de dispositivo. Essas são configurações que anteriormente estavam no Microsoft Intune em uma configuração autônoma e agora estão disponíveis quando você usar o Intune com o Configuration Manager.
Para obter detalhes, consulte [itens de configuração para dispositivos gerenciados sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/configuration-items-for-devices-managed-without-the-client).

### <a name="new-settings-for-android-devices"></a>Novas configurações para dispositivos Android
#### <a name="password-settings"></a>Configurações de senha
- **Lembrar histórico de senha**
- **Permitir a impressão digital desbloquear**

#### <a name="security-settings"></a>Definições de segurança
- **Exigir criptografia em cartões de armazenamento**
- **Permitir captura de tela**
- **Permitir envio de dados de diagnóstico**

#### <a name="browser-settings"></a>Configurações do navegador
- **Permitir navegador da web**
- **Permitir preenchimento automático**
- **Permitir Bloqueador de pop-up**
- **Permitir cookies**
- **Permitir script ativo**

#### <a name="app-settings"></a>Configurações do aplicativo
- **Permitir loja Google Play**

#### <a name="device-capability-settings"></a>Configurações de funcionalidade do dispositivo
- **Permitir armazenamento removível**
- **Permitir compartilhamento de Internet por Wi-Fi**
- **Permitir localização geográfica**
- **Permitir NFC**
- **Permitir Bluetooth**
- **Permitir roaming de voz**
- **Permitir roaming de dados**
- **Permitir mensagens SMS/MMS**
- **Permitir assistência de voz**
- **Permitir discagem de voz**
- **Permitir copiar e colar**

### <a name="new-settings-for-ios-devices"></a>Novas configurações para dispositivos iOS
#### <a name="password-settings"></a>Configurações de senha
- **Número de caracteres complexos necessários na senha**
- **Permitir palavras-passe simples**
- **Minutos de inatividade antes que a senha é necessária**
- **Lembrar histórico de senha**

### <a name="new-settings-for-mac-os-x-devices"></a>Novas configurações para dispositivos Mac OS X
#### <a name="password-settings"></a>Configurações de senha
- **Número de caracteres complexos necessários na senha**
- **Permitir palavras-passe simples**
- **Lembrar histórico de senha**
- **Minutos de inatividade antes do protetor de tela seja ativado**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Novas configurações para dispositivos Windows 10 Desktop e Mobile
#### <a name="password-settings"></a>Configurações de senha
- **Número mínimo de conjuntos de caracteres**
- **Lembrar histórico de senha**
- **Exigir uma senha quando o dispositivo retorna do estado ocioso**

#### <a name="security-settings"></a>Definições de segurança
- **Exigir criptografia no dispositivo móvel**
- **Permitir cancelamento de registro manual**

#### <a name="device-capability-settings"></a>Configurações de funcionalidade do dispositivo
- **Permitir VPN por celular**
- **Permitir roaming de VPN por celular**
- **Permitir redefinição de telefone**
- **Permitir conexão USB**
- **Permitir Cortana**
- **Permitir notificações da Central de ações**

### <a name="new-settings-for-windows-10-team-devices"></a>Novas configurações para dispositivos Windows 10 Team
#### <a name="device-settings"></a>Configurações do dispositivo
- **Habilitar Insights operacionais do Azure**
- **Habilitar projeção sem fio Miracast**
- **Escolha as informações da reunião exibidas na tela de boas-vinda**
- **URL de imagem de plano de fundo de bloqueio**

### <a name="new-settings-for-windows-81-devices"></a>Novas configurações para dispositivos Windows 8.1
#### <a name="applicability-settings"></a>Configurações de aplicabilidade
- **Aplicar todas as configurações para o Windows 10**

#### <a name="password-settings"></a>Configurações de senha
- **Tipo de senha necessária**
- **Número mínimo de conjuntos de caracteres**
- **Comprimento mínimo da senha**
- **Número de falhas de entrada repetidas permitido antes do dispositivo ser apagado**
- **Minutos de inatividade antes da tela desligar**
- **Expiração da senha (dias)**
- **Lembrar histórico de senha**
- **Evitar a reutilização de senhas anteriores**
- **Permitir senha de imagem e PIN**

#### <a name="browser-settings"></a>Configurações do navegador
- **Permitir detecção automática de rede intranet**

### <a name="new-settings-for-windows-phone-81-devices"></a>Novas configurações para dispositivos Windows Phone 8.1
#### <a name="applicability-settings"></a>Configurações de aplicabilidade
- **Aplicar todas as configurações para o Windows 10**

#### <a name="password-settings"></a>Configurações de senha
- **Número mínimo de conjuntos de caracteres**
- **Permitir palavras-passe simples**
- **Lembrar histórico de senha**

#### <a name="device-capability-settings"></a>Configurações de funcionalidade do dispositivo
- **Permitir conexão automática liberar pontos de acesso Wi-Fi**


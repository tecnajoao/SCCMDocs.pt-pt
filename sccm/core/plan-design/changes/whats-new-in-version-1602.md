---
title: Novidades na versão 1602
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas funcionalidades introduzidas na versão 1602 do System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: c6d085fd33513a32207a3b9acfdfe6fe91657a88
ms.sourcegitcommit: 2cc635835709fb8d86cdb63ea34233b36c94d4d8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/20/2018
ms.locfileid: "52259051"
---
# <a name="what39s-new-in-version-1602-of-system-center-configuration-manager"></a>O que&#39;s novo na versão 1602 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Para o System Center Configuration Manager só está disponível como uma atualização na consola para sites anteriormente instalados com a versão 1511 a atualização 1602. A versão 1511 é a versão de linha de base inicial, que utilizar para instalar novos sites do Configuration Manager.  


> [!TIP]  
>  Saiba mais sobre:  
>   
>   -   [Instalar novos sites](/sccm/core/servers/deploy/install) (usando uma versão de linha de base como a versão 1511)  
>   -   [Instalar atualizações em sites](/sccm/core/servers/manage/updates) (como a atualização 1602)  

 As secções seguintes fornecem detalhes sobre alterações e novas funcionalidades introduzidas na versão 1602 do Configuration Manager.  

## <a name="site-infrastructure"></a>Infraestrutura do site  

###  <a name="bkmk_UpgradeOS"></a> Atualizar de no local o sistema operativo de servidores de sites que executam o Windows Server 2008 R2  
 Sites do Configuration Manager que executam a versão 1602 ou posterior suportam a atualização no local do site servidores sistema operativo do Windows Server 2008 R2 para o Windows Server 2012 R2.  

> [!WARNING]  
>  Antes de atualizar para o Windows Server 2012 R2, tem de desinstalar o WSUS 3.2 do servidor.  
>   
>  Para obter informações sobre este passo crítico, consulte a secção "Funcionalidade nova e alterada" em [descrição geral do Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx), na documentação do Windows Server.  

 Para atualizar um servidor, utilize os procedimentos de atualização do Windows Server 2012 R2. Não é necessário executar um Gestor de configuração de restauro do servidor de site após a atualização. Para saber quais são os procedimentos de atualização, veja [Opções de Atualização do Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) na documentação do Windows Server.  

###  <a name="bkmk_AOAG"></a> Grupos de Disponibilidade AlwaysOn do SQL Server  
 Utilize grupos de Disponibilidade AlwaysOn do SQL Server para alojar a base de dados do site em sites primários e o site de administração central como uma solução de elevada disponibilidade e recuperação após desastre.  

 Para obter detalhes, consulte [SQL Server AlwaysOn para uma base de dados do site de elevada disponibilidade para o System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

## <a name="operating-system-deployment"></a>Implementação do sistema operativo  

### <a name="windows-10-servicing"></a>Manutenção do Windows 10  
 Os seguintes melhoramentos para a manutenção do Windows 10 foram adicionados na versão 1602 do Configuration Manager versão:  

-   Novas opções de filtro estão disponíveis para planos que permitem-lhe filtrar por de manutenção **linguagem**, **necessário**, e **Title**. Apenas as atualizações que cumprem os critérios especificados serão adicionadas à implementação associada.  

-   Quando seleciona a **atualizações** sincronização de atualizações de classificação de software, é apresentado um aviso. Este aviso permite-lhe saber que [correção 3095113](https://support.microsoft.com/kb/3095113) para Windows Server Update Services (WSUS) 4.0 é necessária antes de pode sincronizar com êxito as atualizações de software e para a manutenção do Windows 10 funcionar corretamente. A mensagem de aviso, pode aceder ao artigo da base de dados de conhecimento associado.  

-   Windows 10 disponíveis agora, as atualizações apenas são apresentadas no **manutenção do Windows 10** \ **todas as atualizações do Windows 10** nó da consola do Configuration Manager. Estas atualizações já não aparecem no **atualizações de Software** \ **todas as atualizações de Software** nó da consola.  

-   Um plano de manutenção é considerado uma implementação de alto risco e o **selecionar coleção** janela exibe apenas as coleções personalizadas que cumprem as definições de verificação de implementação que estão configuradas nas propriedades do site. Para mais informações, consulte [Settings to manage high-risk deployments for System Center Configuration Manager](../../../protect/understand/settings-to-manage-high-risk-deployments.md).  

-   Os utilizadores que iniciar um pacote de atualização do Windows 10 agora recebem uma mensagem que eles irão atualizar o sistema operativo.  

## <a name="application-management"></a>Gestão de aplicações  

### <a name="ios-app-configuration-policies"></a>Políticas de configuração de aplicações iOS  
 Utilize políticas de configuração de aplicação do Configuration Manager para disponibilizar definições que poderão ser necessárias quando o utilizador executar uma aplicação iOS. Por exemplo, uma aplicação pode requerer que o utilizador especifique um número de porta personalizado, idioma, as definições de segurança ou definições de imagem corporativa (por exemplo, um logótipo de empresa). Se estas definições forem introduzidas incorretamente, isso pode aumentar a carga sobre o suporte técnico e também tornar mais lenta a adoção de novas aplicações.  

 Políticas de configuração de aplicação podem ajudar a eliminar estes problemas, permitindo-lhe implementar estas definições aos utilizadores de uma política, antes de executarem a aplicação. As definições são então fornecidas automaticamente e o utilizador não tem de efetuar qualquer ação. Para obter detalhes, consulte [configurar aplicações iOS com políticas de configuração de aplicações no System Center Configuration Manager](../../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).  

### <a name="manage-volume-purchased-ios-apps"></a>Gerir aplicações iOS adquiridas em volume  
 O Configuration Manager pode ajudá-lo a implementar e gerir aplicações compradas em volume do Apple Volume Purchase Program (VPP). Configuration Manager importa as informações da licença a partir da app store e controla o número de licenças utilizou.  

 Para obter detalhes, consulte [gerir aplicações de iOS compradas em volume com o System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).  

### <a name="automatic-creation-of-office-mobile-apps"></a>Criação automática de aplicações móveis do Office  
 Quando atualizar para a versão 1602 a partir da versão 1511, o Configuration Manager cria automaticamente as seguintes aplicações móveis do Microsoft Office para Android e iOS:  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (apenas iOS)  

-   Microsoft Outlook  

Encontrará destas aplicações na **aplicativos** nó da consola do Configuration Manager.  

 Para obter mais informações sobre a implementação de aplicações, consulte [como implementar aplicações com o System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

## <a name="software-updates"></a>Atualizações de software  

### <a name="manage-office-365-client-updates"></a>Gerir atualizações de cliente do Office 365  
 O System Center Configuration Manager tem a capacidade para gerir atualizações de cliente do Office 365 com o fluxo de trabalho de gestão de atualização de software. Para obter mais informações, consulte [com o System Center Configuration Manager de atualizações de gerir o Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).  

## <a name="compliance-settings"></a>Definições de compatibilidade  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>Definições de conformidade para dispositivos Windows 10 Team  
 Foram adicionadas novas definições para o **Windows 8.1 e Windows 10** item de configuração. Estas definições ajudam a controlar dispositivos que executem o Windows 10 Team, como um dispositivo Surface Hub.  

 Para obter detalhes, consulte [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Definições do modo de local público para dispositivos Android Samsung KNOX Standard  
 Modo de local público permite-lhe bloquear um dispositivo para que apenas determinadas funcionalidades funcionem. Por exemplo, pode permitir que um dispositivo execute apenas uma aplicação gerida que especificar ou pode desativar os botões de volume num dispositivo. Estas definições podem ser utilizadas para um modelo de demonstração de um dispositivo ou um dispositivo de desempenhar apenas uma função, como um dispositivo de ponto de venda. No Configuration Manager, pode agora especificar definições do modo de local público para dispositivos Samsung KNOX Standard.  

 Para obter detalhes, consulte [como criar itens de configuração para dispositivos Android e Samsung KNOX Standard gerido sem o cliente do System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).  

## <a name="conditional-access"></a>Acesso condicional  

### <a name="conditional-access-for-pcs-managed-by-system-center-configuration-manager"></a>Acesso condicional para PCs geridos pelo System Center Configuration Manager  
 Anteriormente a esta versão, para configurar o acesso condicional para um PC, o PC ou tinha de estar inscritos no Intune ou tinha que ser um PC associado a um domínio. Começando com a atualização 1602, o acesso condicional para PCs geridos pelo System Center Configuration manager é suportado. Para os computadores que são geridos pelo System Center Configuration Manager, pode restringir o acesso ao Exchange Online e SharePoint Online apenas a dispositivos que estão em conformidade com as políticas de conformidade que definir.  

 Para obter detalhes, consulte [gerir o acesso aos serviços do O365 para PCs geridos pelo System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  

### <a name="restricting-access-based-on-the-health-of-devices"></a>Restringir o acesso com base no estado de funcionamento de dispositivos  
 Agora pode restringir o acesso ao e-mail e aos serviços do Office 365 com base no estado de funcionamento de dispositivos, conforme comunicado pelo serviço de atestado de estado de funcionamento. Além disso, os dispositivos geridos pelo Intune são incluídos nos relatórios de estado de funcionamento do dispositivo.  

 Consola do Configuration Manager apresenta uma nova regra de conformidade que lhe permite especificar se os dispositivos devem ser permitidos ou bloqueado o acesso com base no respetivo estado de funcionamento. Para obter detalhes sobre o serviço de atestado de estado de funcionamento e como o estado de funcionamento de dispositivos é reportado no Intune, consulte [atestado de estado de funcionamento do System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="new-compliance-policy-rules"></a>Novas regras de política de conformidade  
 Foram adicionadas novas regras de política de conformidade, como as atualizações automáticas e exigir uma palavra-passe para desbloquear os dispositivos, para suportar os requisitos de segurança melhores.

 Para obter mais detalhes, consulte [políticas de conformidade no System Center Configuration Manager](../../../protect/deploy-use/device-compliance-policies.md).  

### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>Certifique-se de que os dispositivos inscritos e em conformidade tenham sempre acesso ao Exchange no local  
 Quando seleciona a opção seguinte, os dispositivos inscritos no Intune e em conformidade com as políticas de conformidade têm permissão para aceder ao Exchange no local: **Substituição da regra predefinida - permitir sempre aos dispositivos em conformidade para o acesso do Exchange no local e inscritos no Intune:**. Esta regra está disponível na **página geral** da **configurar Assistente de política de acesso condicional** para o Exchange no local.

 Esta regra substitui a regra predefinida, o que significa que mesmo que defina a regra predefinida para colocar em quarentena ou bloquear o acesso, inscritos e em conformidade com dispositivos ainda será possível aceder ao Exchange no local. Utilize esta definição se pretender que inscritos e dispositivos em conformidade tenham sempre acesso ao e-mail através do Exchange no local.   

 Para instruções detalhadas, consulte [gerir o acesso ao e-mail no System Center Configuration Manager](../../../protect/deploy-use/manage-email-access.md).  

## <a name="client-management"></a>Gestão de clientes  

### <a name="client-online-status"></a>Estado online do cliente  
 Um novo estado de clientes está disponível para monitorização, se um computador está online ou não. Um computador é considerado online se estiver ligado ao respetivo ponto de gestão atribuído. Para indicar que o computador está online, o cliente envia mensagens do tipo ping para o ponto de gestão. Se o ponto de gestão não receber uma mensagem após 5 minutos, o cliente é considerado offline.  

 Para obter detalhes, consulte [como monitorizar clientes no System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Atualizar a política de computador e utilizador de PC do Centro de Software  
 Uma nova opção **política de sincronização**, foi adicionado à **opções** > **manutenção do computador** página do Centro de Software que faz com que o PC atualize seu Política de computador e utilizador do Configuration Manager.  

### <a name="software-center-branding-changes"></a>Alterações de imagem corporativa do Centro de software  
 Pode alterar a cor, o nome da organização e o ícone que são apresentados no Centro de Software. Estas definições são aplicadas de acordo com as seguintes regras:  

- Se a função de servidor de sites do ponto de Web site do catálogo de aplicações não está instalada, o Centro de Software apresenta o nome da organização especificado na **agente do computador** cliente chamada **nome da organização apresentada no Centro de software**.  

- Se a função de servidor de sites do ponto de Web site do catálogo de aplicações estiver instalada, o Centro de Software apresenta o nome da organização e a cor especificados nas propriedades da função de servidor de site de ponto de Web site de catálogo de aplicações.  

- Se uma subscrição do Microsoft Intune é configurada e ligada ao ambiente do Configuration Manager, em seguida, o Centro de Software apresenta o nome da organização, a cor e o logótipo da empresa especificados nas propriedades de subscrição do Intune.  

### <a name="health-attestation"></a>Atestado de estado de funcionamento  
 Os administradores podem ver o estado do atestado de estado de funcionamento do dispositivo do Windows 10 na consola do Configuration Manager. Isto está disponível para o Configuration Manager, bem como do Configuration Manager com o Microsoft Intune. O atestado de estado de funcionamento permite ao administrador garantir que os computadores cliente têm as seguintes configurações fidedignas de BIOS, TPM e software de arranque ativadas:  

-   Antimalware de início antecipado  

-   BitLocker  

-   Arranque seguro  

-   Integridade do código  

Para obter detalhes, consulte [atestado de estado de funcionamento do System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Melhoramentos às definições de antimalware do Endpoint Protection  
 a atualização 1602 adiciona as seguintes definições novas de política antimalware do Endpoint Protection para o Windows Defender:  

-   Proteção em tempo real: Bloquear aplicações potencialmente indesejáveis ao transferir, antes da instalação.  

-   Definições de análise: Analise unidades de rede mapeadas durante uma análise completa.  

-   Definições de submissão de ficheiros de exemplo automática:  

     O motor antimalware pode solicitar os ficheiros de exemplo para ser enviado à Microsoft para análise adicional. Por predefinição, será sempre apresentado um aviso antes de enviar esses exemplos. Os administradores podem agora gerir as seguintes definições para configurar este comportamento:  

    -   Avançado: Ative a submissão automática de ficheiros ajudar a determinar se certos itens detetados são maliciosos.  

    -   Avançado: Permitir aos utilizadores modificar definições de submissão de ficheiros de exemplo automática.  

    Além disso, na secção "Definições de exclusão" da política de antimalware de proteção de ponto final, o existente **excluir ficheiros e pastas** definição agora permite exclusões de dispositivos.  

Para obter detalhes, consulte [como criar e implementar políticas antimalware do Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-antimalware-policies.md).  

## <a name="mobile-device-management"></a>Gestão de dispositivos móveis  

### <a name="ios-activation-lock"></a>Bloqueio de ativação do iOS  
 O Configuration Manager pode ajudar a gerir o bloqueio de ativação, uma funcionalidade do veja iOS a minha aplicação do iPhone para iOS 7.1 e dispositivos posteriores. O Bloqueio de Ativação é ativado automaticamente ao utilizar a aplicação Encontrar o Meu iPhone num dispositivo. Depois de estar ativado, o Apple ID e a palavra-passe do utilizador têm de ser introduzidos primeiro para que qualquer pessoa possa:  

-   Desative encontrar o meu iPhone.  

-   Apagar o dispositivo.  

-   Reative o dispositivo.  

O Configuration Manager pode pedir o estado de bloqueio de ativação de dispositivos supervisionados e não supervisionados que executam o iOS 7.1 e posterior. Para dispositivos supervisionados, o Configuration Manager pode obter o código de desativação do bloqueio de ativação e enviá-lo diretamente no dispositivo.  

 Para obter detalhes, consulte [ajudar a proteger dispositivos iOS com o bloqueio de ativação desativando no System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock).  

### <a name="monitor-terms-and-conditions-deployments"></a>Monitorizar implementações de termos e condições  
 Pode monitorizar implementações de termos e condições na consola do Configuration Manager.  

 Selecione a implementação de termos e condições da lista de implementações. A área de resumo mostra as estatísticas seguintes:  

-   **Em conformidade**: Os utilizadores aceitaram a versão mais recente dos termos e condições.  

-   **Erro**  

-   **Em não conformidades**: Os utilizadores aceitaram uma versão dos termos e condições, mas não a versão mais recente.  

-   **Desconhecido**: Os utilizadores nunca aceitaram os termos e condições, incluindo as pessoas sem um dispositivo inscrito.  

---
title: "Novidade na versão 1602"
titleSuffix: Configuraton Manager
description: "Obter informações sobre as alterações e novas funcionalidades introduzidas na versão 1602 do System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
caps.latest.revision: "3"
author: mestew
ms.author: mstewart
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: a9d6d0f4dcf2b57c21d54e35fb3f61668d2cbea3
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="what39s-new-in-version-1602-of-system-center-configuration-manager"></a>O que &#39; s novidade na versão 1602 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Atualize para o System Center Configuration Manager só está disponível como uma atualização na consola para sites anteriormente instalados com a versão 1511 a 1602. A versão 1511 é a versão de linha de base inicial, que utiliza para instalar novos sites do Configuration Manager.  


> [!TIP]  
>  Saiba mais sobre:  
>   
>   -   [Instalar novos sites](/sccm/core/servers/deploy/install) (utilizando uma versão de linha de base como a versão 1511)  
>   -   [Instalar atualizações em sites](/sccm/core/servers/manage/updates) (como a atualização 1602)  

 As secções seguintes fornecem detalhes sobre as alterações e novas funcionalidades introduzidas na versão 1602 do Configuration Manager.  

## <a name="site-infrastructure"></a>Infraestrutura de sites  

###  <a name="bkmk_UpgradeOS"></a>No local atualizar o sistema operativo de servidores de sites que executam o Windows Server 2008 R2  
 Os sites do Configuration Manager com a versão 1602 ou posterior suportam a atualização no local do sistema de sites servidores operativo do Windows Server 2008 R2 para o Windows Server 2012 R2.  

> [!WARNING]  
>  Antes de atualizar para o Windows Server 2012 R2, tem de desinstalar o WSUS 3.2 a partir do servidor.  
>   
>  Para obter informações sobre este passo crítico, consulte a secção "Funcionalidades novas e alteradas" [descrição geral do Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx), na documentação do Windows Server.  

 Para atualizar um servidor, utilize os procedimentos de atualização do Windows Server 2012 R2. Não é necessário executar o restauro do servidor de site após a atualização do Configuration Manager. Para saber quais são os procedimentos de atualização, veja [Opções de Atualização do Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) na documentação do Windows Server.  

###  <a name="bkmk_AOAG"></a>Grupos de Disponibilidade AlwaysOn do SQL Server  
 Utilize grupos de Disponibilidade AlwaysOn do SQL Server para alojar a base de dados do site em sites primários e o site de administração central como uma solução de elevada disponibilidade e recuperação após desastre.  

 Para obter mais informações, consulte [SQL Server AlwaysOn para uma base de dados do site de elevada disponibilidade para o System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

## <a name="operating-system-deployment"></a>Implementação do sistema operativo  

### <a name="windows-10-servicing"></a>Manutenção do Windows 10  
 Os seguintes melhoramentos para a manutenção do Windows 10 foram adicionados na versão 1602 do Configuration Manager versão:  

-   Novas opções de filtro estão disponíveis para a manutenção planos que permitem-lhe filtrar **idioma**, **necessário**, e **título**. Apenas as atualizações que cumprem os critérios especificados serão adicionadas à implementação associada.  

-   Quando seleciona o **atualizações** sincronização de atualizações de classificação de recursos de software, é apresentado um aviso. Este aviso permite-lhe saber que [correção 3095113](https://support.microsoft.com/kb/3095113) para Windows Server Update Services (WSUS) 4.0 é necessário antes de pode sincronizar as atualizações de software com êxito e a manutenção do Windows 10 funcionar corretamente. A mensagem de aviso, pode aceder ao artigo da base de dados de conhecimento associado.  

-   Windows 10 disponíveis agora, as atualizações apenas são apresentadas no **manutenção do Windows 10** \ **todas as atualizações do Windows 10** nós da consola do Configuration Manager. Estas atualizações já não aparecem no **atualizações de Software** \ **todas as atualizações de Software** nós da consola.  

-   Um plano de manutenção é considerado uma implementação de alto risco e o **selecionar coleção** janela apresenta apenas as coleções personalizadas que cumprem as definições de verificação de implementação que estão configuradas nas propriedades do site. Para obter mais informações, veja [Definições para gerir implementações de alto risco para o System Center Configuration Manager](../../../protect/understand/settings-to-manage-high-risk-deployments.md).  

-   Os utilizadores que começar agora um pacote de atualização do Windows 10 recebem uma mensagem que que actualizará o sistema operativo.  

## <a name="application-management"></a>Gestão de aplicações  

### <a name="ios-app-configuration-policies"></a>Políticas de configuração de aplicações iOS  
 Utilize políticas de configuração de aplicação do Configuration Manager para fornecer definições que poderão ser necessárias quando o utilizador executa uma aplicação iOS. Por exemplo, uma aplicação poderá requerer que o utilizador especifique um número de porta personalizado, idioma, definições de segurança ou definições de imagem corporativa (como um logótipo de empresa). Se estas definições forem introduzidas incorretamente, isto pode aumentar a carga sobre o suporte técnico e também tornar mais lenta a adoção de novas aplicações.  

 Políticas de configuração de aplicação podem ajudar a eliminar estes problemas, permitindo-lhe implementar estas definições em utilizadores de uma política, antes que executar a aplicação. As definições são então fornecidas automaticamente e o utilizador não tem de efetuar qualquer ação. Para obter mais informações, consulte [configurar aplicações iOS com políticas de configuração de aplicações no System Center Configuration Manager](../../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).  

### <a name="manage-volume-purchased-ios-apps"></a>Gerir aplicações iOS adquiridas em volume  
 O Configuration Manager pode ajudar a implementar e gerir aplicações adquiridas em volume da Apple Volume-Purchase Program (VPP). Configuration Manager importa as informações da licença da loja de aplicações e controla a quantidade de licenças utilizou.  

 Para obter mais informações, consulte [gerir aplicações iOS compradas em volume com o System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).  

### <a name="automatic-creation-of-office-mobile-apps"></a>Criação automática de aplicações móveis do Office  
 Quando atualizar para a versão 1602 da versão 1511, o Configuration Manager cria automaticamente as seguintes aplicações móveis do Microsoft Office para Android e iOS:  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (apenas iOS)  

-   Microsoft Outlook  

Poderá encontrar estas aplicações o **aplicações** nó da consola do Configuration Manager.  

 Para obter mais informações sobre como implementar aplicações, consulte [como implementar aplicações com o System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

## <a name="software-updates"></a>Atualizações de software  

### <a name="manage-office-365-client-updates"></a>Gerir atualizações de cliente do Office 365  
 O System Center Configuration Manager tem a capacidade para gerir atualizações de cliente do Office 365, utilizando o fluxo de trabalho de gestão de atualização de software. Para obter mais informações, consulte [gerir o Office 365 ProPlus atualizações com o System Center Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates).  

## <a name="compliance-settings"></a>Definições de compatibilidade  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>Definições de compatibilidade para dispositivos que executam o Windows 10 Team  
 Foram adicionadas novas definições para o **Windows 8.1 e Windows 10** item de configuração. Estas definições ajudam a controlar dispositivos que executem o Windows 10 Team, tais como um dispositivo Surface Hub.  

 Para obter mais informações, consulte [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Definições do modo de local público para dispositivos Android Samsung KNOX Standard  
 Modo de local público permite-lhe bloquear um dispositivo para que apenas determinadas funcionalidades funcionem. Por exemplo, pode permitir que um dispositivo execute apenas uma aplicação gerida que especificar ou pode desativar os botões de volume num dispositivo. Estas definições podem ser utilizadas para um modelo de demonstração de um dispositivo ou um dispositivo com a finalidade de desempenhar apenas uma função, como um dispositivo de ponto de venda. No Configuration Manager, pode agora especificar definições do modo de local público para dispositivos Samsung KNOX Standard.  

 Para obter mais informações, consulte [como criar itens de configuração para dispositivos Android e Samsung KNOX Standard geridos sem o cliente do System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).  

## <a name="conditional-access"></a>Acesso condicional  

### <a name="conditional-access-for-pcs-managed-by-system-center-configuration-manager"></a>Acesso condicional para PCs geridos pelo System Center Configuration Manager  
 Incorrectas nesta versão, para configurar o acesso condicional para PC, o PC tinha de estar inscritos no Intune ou que tiveram de ser um PC associado a um domínio. Começando com a atualização 1602, o acesso condicional para PCs geridos pelo System Center Configuration manager é suportado. Para os computadores que são geridos pelo System Center Configuration Manager, pode restringir o acesso ao Exchange Online e SharePoint Online apenas a dispositivos conformes com as políticas de conformidade definidas.  

 Para obter mais informações, consulte [gerir o acesso aos serviços do O365 para PCs geridos pelo System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  

### <a name="restricting-access-based-on-the-health-of-devices"></a>Restringir o acesso com base no estado de funcionamento de dispositivos  
 Agora pode restringir o acesso ao e-mail e 0ffice 365 aos serviços com base no estado de funcionamento dos dispositivos, conforme comunicado pelo serviço de atestado do Estado de funcionamento. Além disso, os dispositivos geridos pelo Intune são incluídos nos relatórios de estado de funcionamento do dispositivo.  

 Consola do Configuration Manager inclui uma nova regra de compatibilidade, que permite-lhe especificar se os dispositivos devem ser permitidos ou bloqueados acesso com base no respetivo estado de funcionamento. Para obter detalhes sobre o serviço de atestado de estado de funcionamento e sobre como o estado de funcionamento de dispositivos é reportado no Intune, consulte [atestado de estado de funcionamento para o System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="new-compliance-policy-rules"></a>Novas regras de política de conformidade  
 Foram adicionadas novas regras de política de conformidade, como as atualizações automáticas e exigir uma palavra-passe para desbloquear dispositivos, para suportar os requisitos de segurança melhores.

 Para obter mais detalhes, consulte [políticas de conformidade de dispositivos no System Center Configuration Manager](../../../protect/deploy-use/device-compliance-policies.md).  

### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>Certifique-se de que os dispositivos inscritos e compatíveis tenham sempre acesso ao Exchange no local  
 Quando seleciona a opção seguinte, os dispositivos inscritos no Intune e em conformidade com as políticas de conformidade estão autorizados a aceder ao Exchange no local: **Substituição da regra predefinida - permitir sempre inscritos no Intune e dispositivos conformes ao Exchange no local de acesso:**. Esta regra está disponível na **página ' Geral '** do **configurar Assistente de política de acesso condicional** para o Exchange no local.

 Esta regra substitui a regra predefinida, o que significa que mesmo que defina a regra predefinida para colocar em quarentena ou bloquear o acesso, inscritos e conformes ainda será capazes de aceder ao Exchange no local. Utilize esta definição quando quiser inscrito e os dispositivos compatíveis tenham sempre acesso ao e-mail através do Exchange no local.   

 Para instruções detalhadas, consulte [gerir o acesso ao e-mail no System Center Configuration Manager](../../../protect/deploy-use/manage-email-access.md).  

## <a name="client-management"></a>Gestão de clientes  

### <a name="client-online-status"></a>Estado online do cliente  
 Um novo estado de clientes está disponível para monitorização se um computador está online ou não. Um computador é considerado online se estiver ligado ao respetivo ponto de gestão atribuído. Para indicar que o computador está online, o cliente envia mensagens do tipo ping ao ponto de gestão. Se o ponto de gestão não receber uma mensagem após 5 minutos, o cliente é considerado offline.  

 Para obter mais informações, consulte [como monitorizar clientes no System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Atualizar a política de computador e utilizador de PC do Centro de Software  
 Uma nova opção **sincronizar política**, foi adicionada para o **opções** > **manutenção do computador** página do Centro de Software que faz com que o PC Atualize o Gestor de configuração de política de computador e utilizador.  

### <a name="software-center-branding-changes"></a>Alterações de imagem corporativa do Centro de software  
 Pode alterar a cor, o nome da organização e o ícone que são apresentados no Centro de Software. Estas definições são aplicadas de acordo com as seguintes regras:  

- Se a função de servidor de sites do ponto de Web site do catálogo de aplicações não está instalada, em seguida, o Centro de Software apresenta o nome da organização especificado no **agente do computador** chamado de definição de cliente **nome da organização apresentada no Centro de Software**.  

- Se a função de servidor de sites do ponto de Web site do catálogo de aplicações estiver instalada, em seguida, o Centro de Software apresenta o nome da organização e cor especificados nas propriedades da função de servidor de site de ponto de Web site de catálogo de aplicações.  

- Se uma subscrição do Microsoft Intune estiver configurada e ligada ao ambiente do Configuration Manager, em seguida, o Centro de Software apresenta o nome da organização, a cor e o logótipo da empresa especificados nas propriedades de subscrição do Intune.  

### <a name="health-attestation"></a>Atestado de estado de funcionamento  
 Os administradores podem ver o estado do atestado de estado de funcionamento de dispositivo do Windows 10 na consola do Configuration Manager. Isto está disponível para o Configuration Manager, bem como do Configuration Manager com o Microsoft Intune. O atestado de estado de funcionamento permite ao administrador garantir que os computadores cliente têm as seguintes configurações fidedignas de BIOS, TPM e software de arranque ativadas:  

-   Antimalware de início antecipado  

-   BitLocker  

-   Arranque seguro  

-   Integridade do código  

Para obter mais informações, consulte [atestado de estado de funcionamento para o System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Melhoramentos às definições de antimalware do Endpoint Protection  
 1602 adiciona as seguintes definições novas de política antimalware do Endpoint Protection para o Windows Defender:  

-   Proteção em tempo real: Bloquear aplicações potencialmente indesejáveis ao transferir, antes da instalação.  

-   Definições de análise: Analise unidades de rede mapeadas durante uma análise completa.  

-   Definições de submissão de ficheiros de exemplo automática:  

     O motor antimalware pode solicitar exemplos de ficheiros para serem enviados à Microsoft para análise adicional. Por predefinição, será sempre apresentado um aviso antes de enviar esses exemplos. Os administradores podem agora gerir as seguintes definições para configurar este comportamento:  

    -   Avançado: Ative a submissão automática de ficheiros ajudar a Microsoft a determinar se certos itens detetados são maliciosos.  

    -   Avançado: Permita aos utilizadores modificar definições de submissão de ficheiros de exemplo automática.  

    Além disso, na secção "Definições de exclusão" da política de antimalware de proteção de ponto final, o existente **excluir ficheiros e pastas** definição agora permite exclusões de dispositivos.  

Para obter mais informações, consulte [como criar e implementar políticas antimalware do Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-antimalware-policies.md).  

## <a name="mobile-device-management"></a>Gestão de dispositivos móveis  

### <a name="ios-activation-lock"></a>Bloqueio de ativação de iOS  
 O Configuration Manager pode ajudar a gerir o bloqueio de ativação, uma funcionalidade de encontrar iOS a minha aplicação iPhone para iOS 7.1 ou dispositivos posteriores. O Bloqueio de Ativação é ativado automaticamente ao utilizar a aplicação Encontrar o Meu iPhone num dispositivo. Depois de estar ativado, o Apple ID e a palavra-passe do utilizador têm de ser introduzidos primeiro para que qualquer pessoa possa:  

-   Desative encontrar o meu iPhone.  

-   Apagar o dispositivo.  

-   Reative o dispositivo.  

O Configuration Manager pode pedir o estado de bloqueio de ativação de dispositivos supervisionados e não supervisionados que executam o iOS 7.1 e posterior. Para dispositivos supervisionados, o Configuration Manager pode obter o código de desativação do bloqueio de ativação e enviá-lo diretamente para o dispositivo.  

 Para obter mais informações, consulte [ajudar a proteger dispositivos iOS com o bloqueio de ativação desativando no System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock).  

### <a name="monitor-terms-and-conditions-deployments"></a>Monitorizar implementações de termos e condições  
 Pode monitorizar implementações de termos e condições na consola do Configuration Manager.  

 Selecione a implementação de termos e condições da lista de implementações. A área de resumo mostra as estatísticas seguintes:  

-   **Em conformidade**: Os utilizadores aceitaram a versão mais recente dos termos e condições.  

-   **Erro**  

-   **Não compatível**: Os utilizadores aceitaram uma versão dos termos e condições, mas não a versão mais recente.  

-   **Desconhecido**: Os utilizadores nunca aceitaram os termos e condições, incluindo as pessoas sem um dispositivo inscrito.  

---
title: "Novo no System Center Configuration Manager versão 1602 | Documentos do Microsoft"
description: "Obter informações sobre as alterações e novas capacidades introduzidas na versão 1602 do System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 9a548f43625a907173e7b967d26356bd80f1c5d9
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="what39s-new-in-version-1602-of-system-center-configuration-manager"></a>O que &#39; s Novidades na versão 1602 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Atualize 1602 para o System Center Configuration Manager só está disponível como uma atualização na consola de sites instaladas anteriormente com a versão 1511. Versão 1511 é a versão de linha de base inicial, que utiliza para instalar novos sites do Configuration Manager.  


> [!TIP]  
>  Saiba mais sobre:  
>   
>   -   [Instalar novos sites](/sccm/core/servers/deploy/install) (utilizando uma versão de linha de base como 1511)  
>   -   [Instalar atualizações em sites](/sccm/core/servers/manage/updates) (como atualizar 1602)  

 As secções seguintes fornecem detalhes sobre as alterações e funcionalidades novas, introduzidas na versão 1602 do Configuration Manager.  

## <a name="site-infrastructure"></a>Infraestrutura de sites  

###  <a name="bkmk_UpgradeOS"></a>No local de atualizar o sistema operativo de servidores de sites que executam o Windows Server 2008 R2  
 Sites do Configuration Manager que são executados versão 1602 ou posteriores suportam a atualização no local do sistema de sites servidores operativo a partir do Windows Server 2008 R2 para o Windows Server 2012 R2.  

> [!WARNING]  
>  Antes de atualizar para o Windows Server 2012 R2, tem de desinstalar 3,2 de WSUS a partir do servidor.  
>   
>  Para obter informações sobre este passo crítico, consulte a secção "Novas e alteradas" [descrição geral do Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx), na documentação do Windows Server.  

 Para atualizar um servidor, utilize os procedimentos de atualização do Windows Server 2012 R2. Não é necessário executar o restauro de servidor de site após a atualização do Configuration Manager. Para saber quais são os procedimentos de atualização, veja [Opções de Atualização do Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) na documentação do Windows Server.  

###  <a name="bkmk_AOAG"></a>Grupos de Disponibilidade AlwaysOn do SQL Server  
 Utilize grupos de Disponibilidade AlwaysOn do SQL Server para alojar a base de dados do site em sites primários e o site de administração central como uma solução de elevada disponibilidade e recuperação de desastres.  

 Para obter mais detalhes, consulte o artigo [SQL Server AlwaysOn numa base de dados do site elevada para o System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

## <a name="operating-system-deployment"></a>Implementação do sistema operativo  

### <a name="windows-10-servicing"></a>Manutenção do Windows 10  
 Foram adicionadas as seguintes melhorias para a manutenção do Windows 10 1602 de versão do Configuration Manager:  

-   Novas opções de filtro estão disponíveis para a manutenção planos que permitem-lhe filtrar **idioma**, **necessário**, e **título**. Apenas as atualizações que cumprem os critérios especificados serão adicionadas à implementação associada.  

-   Quando seleciona o **atualizações** sincronização de atualizações de classificação de software, é apresentado um aviso. Este aviso permite-lhe saber que [correção 3095113](https://support.microsoft.com/kb/3095113) para Windows Server Update Services (WSUS) 4.0 é necessário pode sincronizar as atualizações de software com êxito e a manutenção de 10 de Windows funcionem corretamente. A partir da mensagem de aviso, pode ir para o artigo da base de dados de conhecimento associados.  

-   Disponível Windows 10 agora atualiza apenas visualização no **manutenção do Windows 10** \ **todas as atualizações do Windows 10** nó da consola do Configuration Manager. Estas atualizações já não aparecerá no **atualizações de Software** \ **todas as atualizações de Software** nó da consola.  

-   Um plano de manutenção é considerado uma implementação de alto risco e o **selecionar coleção** janela apresenta apenas as coleções personalizadas que cumprem as definições de verificação de implementação que estão configuradas nas propriedades do site. Para obter mais informações, veja [Definições para gerir implementações de alto risco para o System Center Configuration Manager](../../../protect/understand/settings-to-manage-high-risk-deployments.md).  

-   Os utilizadores que começar agora um pacote de atualização do Windows 10 recebem uma mensagem que que actualizará o sistema operativo.  

## <a name="application-management"></a>Gestão de aplicações  

### <a name="ios-app-configuration-policies"></a>Políticas de configuração de aplicações iOS  
 Utilize políticas de configuração de aplicação do Configuration Manager para fornecer definições que poderão ser necessárias quando o utilizador executa uma aplicação iOS. Por exemplo, uma aplicação pode necessitar de utilizador especificar um número de porta personalizada, idioma, as definições de segurança ou definições de imagem corporativa (como um logótipo de empresa). Se estas definições são introduzidas incorretamente, isto pode aumentar a carga sobre o suporte técnico e também atrasar a adoção de novas aplicações.  

 Políticas de configuração de aplicação podem ajudar a eliminar estes problemas, permitindo-lhe implementar estas definições para os utilizadores numa política, antes de poderem executam a aplicação. As definições, em seguida, são fornecidas automaticamente e o utilizador não necessita de efetuar qualquer ação. Para obter mais detalhes, consulte o artigo [configurar aplicações iOS com as políticas de configuração da aplicação no System Center Configuration Manager](../../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).  

### <a name="manage-volume-purchased-ios-apps"></a>Gerir aplicações iOS adquiridas em volume  
 Gestor de configuração podem ajudar a implementar e gerir as aplicações que comprou no volume a partir do programa de compra de Volume do Apple (VPP). Configuration Manager importa as informações da licença a partir da app store e controla o número das licenças que utilizou.  

 Para obter mais detalhes, consulte o artigo [gerir as aplicações iOS adquirido o volume com o System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).  

### <a name="automatic-creation-of-office-mobile-apps"></a>Criação automática de aplicações móveis do Office  
 Quando atualizar para versão 1602 de 1511, o Configuration Manager cria automaticamente as seguintes aplicações móveis do Microsoft Office para Android e iOS:  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (apenas iOS)  

-   Microsoft Outlook  

Encontrará estas aplicações no **aplicações** nó da consola do Configuration Manager.  

 Para obter mais informações sobre a implementação de aplicações, consulte o artigo [como implementar aplicações com o System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

## <a name="software-updates"></a>Atualizações de software  

### <a name="manage-office-365-client-updates"></a>Gerir atualizações de cliente do Office 365  
 System Center Configuration Manager tem a capacidade para gerir atualizações de cliente do Office 365 utilizando o fluxo de trabalho de gestão de atualização de software. Para obter mais informações, consulte o artigo [gerir Office 365 ProPlus atualizações com o System Center Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates).  

## <a name="compliance-settings"></a>Definições de compatibilidade  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>Definições de compatibilidade para dispositivos que executam o Windows 10 Team  
 Foram adicionadas novas definições para o **Windows 8.1 e Windows 10** item de configuração. Estas definições ajudá-lo a executar o Windows 10 Team, tal como um dispositivo de superfície Hub de dispositivos de controlo.  

 Para obter mais detalhes, consulte o artigo [como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos sem o cliente do System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Definições do modo de local público para dispositivos Android Samsung KNOX Standard  
 Modo de local público permite-lhe bloquear um dispositivo para que apenas determinadas funcionalidades funcionam. Por exemplo, pode permitir que um dispositivo execute apenas uma aplicação gerida que especificar ou pode desativar os botões de volume num dispositivo. Estas definições podem ser utilizadas para um modelo de demonstração de um dispositivo ou um dispositivo com a finalidade de desempenhar apenas uma função, tal como um dispositivo de ponto de venda. No Configuration Manager, pode agora especificar as definições do modo de local público para dispositivos Samsung KNOX Standard.  

 Para obter mais detalhes, consulte o artigo [como criar itens de configuração para dispositivos Android e Samsung KNOX Standard geridos sem o cliente do System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).  

## <a name="conditional-access"></a>Acesso condicional  

### <a name="conditional-access-for-pcs-managed-by-system-center-configuration-manager"></a>Acesso condicional para PCs gerido pelo System Center Configuration Manager  
 Anterior nesta versão, para configurar o acesso condicional para um PC, o PC ou teve de ser inscritos no Intune ou teve de ser um PC associado a um domínio. Acesso condicional para PCs gerido pelo System Center Configuration manager a partir da atualização 1602, é suportado. Para os seus PCs que são geridos pelo System Center Configuration Manager, pode restringir o acesso ao Exchange Online e SharePoint Online apenas para dispositivos que são compatíveis com as políticas de conformidade que definir.  

 Para obter mais detalhes, consulte o artigo [gerir o acesso aos serviços do Office 365 para PCs geridos pelo System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  

### <a name="restricting-access-based-on-the-health-of-devices"></a>Restringir o acesso com base no estado de funcionamento de dispositivos  
 Agora pode restringir o acesso ao e-mail e 0ffice 365 serviços com base no estado de funcionamento de dispositivos, conforme comunicado pelo serviço de integridade de atestado. Além disso, os dispositivos geridos pelo Intune são incluídos nos relatórios de estado de funcionamento do dispositivo.  

 Consola do Configuration Manager oferece uma nova regra de compatibilidade, que permite-lhe especificar se os dispositivos devem ser permitidos ou bloquear o acesso com base no respetivo estado de funcionamento. Para obter detalhes sobre o serviço de integridade de atestado e como é reportado o estado de funcionamento de dispositivos no Intune, consulte o artigo [atestado de estado de funcionamento para o System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="new-compliance-policy-rules"></a>Novas regras de política de conformidade  
 Foram adicionadas novas regras de política de conformidade, como as atualizações automáticas e que requerem uma palavra-passe para desbloquear os dispositivos, para suportar melhor requisitos de segurança.

 Para obter mais detalhes, consulte o artigo [políticas de conformidade do dispositivo no System Center Configuration Manager](../../../protect/deploy-use/device-compliance-policies.md).  

### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>Certifique-se de dispositivos inscritos e de conformidade têm sempre acesso ao Exchange no local  
 Ao dar a seguinte opção, os dispositivos inscritos no Intune e em conformidade com as políticas de conformidade, estão autorizados a aceder ao Exchange no local: **Predefinição Ignorar regra - permitir sempre inscritos do Intune e dispositivos compatíveis para aceder ao Exchange no local:**. Esta regra está disponível no **página geral** do **configurar Assistente de política de acesso condicional** para Exchange no local.

 Esta regra substitui a regra predefinida, o que significa que mesmo se definir a regra predefinida para acesso à quarentena ou bloco, inscritos e dispositivos compatíveis com continuará a poder aceder ao Exchange no local. Utilize esta definição quando pretender inscritos e dispositivos compatíveis para ter sempre acesso ao e-mail através do Exchange no local.   

 Para instruções detalhadas, consulte o artigo [gerir o acesso correio eletrónico no System Center Configuration Manager](../../../protect/deploy-use/manage-email-access.md).  

## <a name="client-management"></a>Gestão de clientes  

### <a name="client-online-status"></a>Estado online do cliente  
 Um novo estado de clientes está disponível para monitorização, se um computador está online ou não. Um computador é considerado online se esta está ligada ao ponto de gestão atribuído. Para indicar que o computador está online, o cliente envia mensagens de como o ping ao ponto de gestão. Se o ponto de gestão não receber uma mensagem 5 minutos, o cliente é considerado offline.  

 Para obter mais detalhes, consulte o artigo [como monitorizar clientes no System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Atualizar PC política de computador e utilizador a partir do Centro de Software  
 Uma nova opção **política de sincronização**, foi adicionado à **opções** > **manutenção do computador** página do Centro de Software que faz com que o PC para atualizar o Configuration Manager política máquina e utilizador.  

### <a name="software-center-branding-changes"></a>Alterações de imagem corporativa do Centro de software  
 Pode alterar a cor, o nome da organização e o ícone que aparecem no Centro de Software. Estas definições são aplicadas de acordo com as seguintes regras:  

- Se a função de servidor de sites do ponto de Web site do catálogo de aplicações não está instalada, em seguida, o Centro de Software apresenta o nome da organização especificado no **agente do computador** cliente denominadas **nome da organização apresentada no Centro de Software**.  

- Se estiver instalada a função de servidor de sites do ponto de Web site do catálogo de aplicações, Centro de Software apresenta o nome da organização e a cor especificado nas propriedades da função de servidor de sites de ponto de Web site de catálogo de aplicações.  

- Se uma subscrição do Microsoft Intune é configurada e ligada ao ambiente do Configuration Manager, em seguida, o Centro de Software apresenta o nome da organização, cor e o logótipo da empresa especificado nas propriedades de subscrição do Intune.  

### <a name="health-attestation"></a>Atestado de estado de funcionamento  
 Os administradores podem ver o estado de atestado de estado de funcionamento de dispositivo do Windows 10 na consola do Configuration Manager. Isto está disponível para o Configuration Manager, bem como do Configuration Manager com o Microsoft Intune. O atestado de estado de funcionamento permite ao administrador garantir que os computadores cliente têm as seguintes configurações fidedignas de BIOS, TPM e software de arranque ativadas:  

-   Início antecipado antimalware  

-   BitLocker  

-   Arranque seguro  

-   Integridade do código  

Para obter mais detalhes, consulte o artigo [atestado de estado de funcionamento para o System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Foram introduzidos melhoramentos nas definições de proteção contra software maligno do Endpoint Protection  
 1602 adiciona as seguintes novas definições na política de proteção contra software maligno do Endpoint Protection do Windows Defender:  

-   Proteção em tempo real: Bloquear aplicações potencialmente indesejável no transferência, antes da instalação.  

-   Analise as definições: Analise unidades de rede mapeadas durante uma análise completa.  

-   Definições de submissão de exemplos de ficheiros de exemplo automática:  

     O motor de proteção contra software maligno pode solicitar exemplos de ficheiros para serem enviados para a Microsoft para análise adicional. Por predefinição, será sempre apresentado um aviso antes de enviar esses exemplos. Os administradores podem agora gerir as seguintes definições para configurar este comportamento:  

    -   Avançado: Ative a submissão automática de ficheiro ajudar a Microsoft a determinar se certos itens detetados maliciosos.  

    -   Avançado: Permitir que os utilizadores modificar as definições de submissão de ficheiro de exemplo automática.  

    Além disso, na secção "Definições de exclusão" as política de proteção contra software maligno do endpoint protection, existentes **excluir pastas e ficheiros** agora a definição permite exclusões de dispositivo.  

Para obter mais detalhes, consulte o artigo [como criar e implementar políticas de proteção contra software maligno do Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-antimalware-policies.md).  

## <a name="mobile-device-management"></a>Gestão de dispositivos móveis  

### <a name="ios-activation-lock"></a>iOS bloqueio de ativação  
 Do Configuration Manager pode ajudar a gerir o iOS bloqueio de ativação, uma funcionalidade do encontrar a minha aplicação iPhone para iOS 7.1 ou posterior. O Bloqueio de Ativação é ativado automaticamente ao utilizar a aplicação Encontrar o Meu iPhone num dispositivo. Depois de estar ativado, o Apple ID e a palavra-passe do utilizador têm de ser introduzidos primeiro para que qualquer pessoa possa:  

-   Desative a localizar o meu iPhone.  

-   Apagar o dispositivo.  

-   Reativar o dispositivo.  

O Configuration Manager podem pedir o estado de bloqueio de ativação dos supervisionado e unsupervised dispositivos que executam o iOS 7.1 e posterior. Para dispositivos supervisionados, o Configuration Manager pode obter o código de omissão de bloqueio de ativação e emiti-lo diretamente para o dispositivo.  

 Para obter mais detalhes, consulte o artigo [ajudar a proteger os dispositivos com o bloqueio de ativação ignorar no System Center Configuration Manager de iOS](/sccm/mdm/deploy-use/manage-ios-activation-lock).  

### <a name="monitor-terms-and-conditions-deployments"></a>Monitorizar as implementações de termos e condições  
 É possível monitorizar implementações de termos e condições na consola do Configuration Manager.  

 Selecione a implementação de termos e condições da lista de implementações. A área de resumo mostra as estatísticas do seguinte:  

-   **Compatível**: Os utilizadores aceitaram a versão mais recente dos termos e condições.  

-   **Erro**  

-   **Não compatível**: Os utilizadores aceitaram uma versão dos termos e condições, mas não a versão mais recente.  

-   **Desconhecido**: Os utilizadores nunca este aceitou os termos e condições, incluindo pessoas sem um dispositivo inscrito.  


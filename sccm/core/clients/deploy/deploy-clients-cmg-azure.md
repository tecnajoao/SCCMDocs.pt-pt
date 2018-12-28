---
title: Instalar o cliente com o Azure AD
titleSuffix: Configuration Manager
description: Instale e atribua o cliente do Configuration Manager em dispositivos Windows 10 com o Azure Active Directory para autenticação
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b722187a895a71b4195200354180cdbc8b2813e6
ms.sourcegitcommit: 12b71da551350c99c5916df3629e33e31040db15
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/17/2018
ms.locfileid: "53530919"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação

Para instalar o cliente do Configuration Manager em dispositivos Windows 10 com a autenticação do Azure AD, integre o Configuration Manager com o Azure Active Directory (Azure AD). Os clientes podem estar na intranet comunique diretamente com um ponto de gestão que suporte HTTPS ou qualquer ponto de gestão num site ativada para HTTP avançada. Eles também podem ser baseados na internet comunicam através de CMG ou com um ponto de gestão baseado na Internet. Este processo utiliza o Azure AD para autenticar clientes para o site do Configuration Manager. O Azure AD substitui a necessidade de configurar e utilizar certificados de autenticação de cliente.



## <a name="before-you-begin"></a>Antes de começar

- Um inquilino do Azure AD é um pré-requisito  

- Requisitos de dispositivo:  

    - Windows 10  

    - Associados ao Azure AD, cloud pura associados a um domínio ou híbrido do Azure AD associado  

- Requisitos de utilizador:  

    - O utilizador com sessão iniciada tem de ser uma identidade do Azure AD.   

    - Se o utilizador é uma identidade federada ou sincronizada, tem de utilizar o Configuration Manager [deteção de utilizadores do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) , bem como [deteção de utilizadores do Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc). Para obter mais informações sobre identidades híbridas, consulte [definir uma estratégia de adoção de identidade híbrida](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->  

- Além do [pré-requisitos existentes](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012MPpreq) para a função de sistema de sites do ponto de gestão, também permitem **ASP.NET 4.5** neste servidor. Inclua quaisquer outras opções selecionadas automaticamente ao ativar o ASP.NET 4.5.  

- Determine se o ponto de gestão tem de HTTPS. Para obter mais informações, consulte [ativar o ponto de gestão para HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  

- Configurar opcionalmente um [gateway de gestão da nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (CMG) para implementar clientes baseados na internet. Para clientes no local que autenticar com o Azure AD, não é necessário um CMG.  


## <a name="configure-azure-services-for-cloud-management"></a>Configurar os serviços do Azure para gestão na Cloud

Ligar o seu site do Configuration Manager para o Azure AD como o primeiro passo. Para obter detalhes sobre este processo, consulte [dos serviços do Azure configurar](/sccm/core/servers/deploy/configure/azure-services-wizard). Criar uma ligação para o **gestão na Cloud** serviço.

Ativar [do Azure AD User Discovery](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc) como parte da adesão ao **gestão de Cloud**. 

Depois de concluir estas ações, o seu site do Configuration Manager está ligada ao Azure AD. 



## <a name="configure-client-settings"></a>Configurar definições de cliente

Estas definições de cliente ajudam a associação com o Windows 10 dispositivos com o Azure AD. Também permitem que os clientes baseados na internet utilizem o ponto de distribuição CMG e na cloud.

1.  Configure as seguintes definições de cliente no **serviços Cloud** secção através das informações nas [como configurar as definições de cliente](/sccm/core/clients/deploy/configure-client-settings).  

    - **Permitir o acesso ao ponto de distribuição da nuvem**: Ative esta definição para ajudar a obter o conteúdo necessário para instalar o cliente do Configuration Manager os dispositivos baseados na internet. Se o conteúdo não está disponível no ponto de distribuição de nuvem, o dispositivo pode obter o conteúdo do CMG. O arranque de instalação de cliente tentará novamente o ponto de distribuição de cloud de quatro horas antes de retrocede para CMG.<!--495533-->  

    - **Registar automaticamente novos dispositivos associados a um domínio do Windows 10 com o Azure Active Directory**: Defina como **Sim** ou **não**. A predefinição é **Sim**. Esse comportamento também é o padrão no Windows 10, versão 1709.

    - **Permitir que os clientes utilizar um gateway de gestão na cloud** – definido como **Sim** (predefinição), ou **não**.  

2.  Implemente as definições de cliente na coleção necessária de dispositivos. Não implemente estas definições em coleções de utilizadores.

Para confirmar que o dispositivo estiver associado ao Azure AD, execute `dsregcmd.exe /status` numa linha de comandos. O **AzureAdjoined** campo no mostra resultados **Sim** se o dispositivo estiver associado ao AD do Azure.



## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Instalar e registar o cliente utilizando a identidade do Azure AD

Para instalar manualmente o cliente utilizando a identidade do Azure AD, reveja o processo geral na [como instalar clientes manualmente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual). 

 > [!Note]  
 > O dispositivo precisa de acesso à internet para contactar o Azure AD, mas não precisa de ser baseado na internet. 

O exemplo seguinte mostra a estrutura geral da linha de comandos: `ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

Para obter mais informações, consulte [das propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties).

As propriedades CCMHOSTNAME e /mp, especifique um dos seguintes, consoante o cenário:
- Ponto de gestão no local. Especifique apenas a propriedade /mp. O CCMHOSTNAME não é necessária.
- Gateway de gestão na cloud
- Ponto de gestão baseado na Internet propriedade SMSMP o Especifica o local ou o ponto de gestão baseado na internet.

Este exemplo utiliza um gateway de gestão na cloud. Ele substitui os valores de exemplo para cada propriedade: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

Para automatizar a instalação de cliente com a identidade do Azure AD através do Microsoft Intune, veja o processo para [dispositivos de preparar o Windows 10 para a cogestão](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).



## <a name="next-steps"></a>Passos seguintes

Depois de concluído, pode continuar a [monitorizar e gerir clientes](/sccm/core/clients/manage/monitor-clients).

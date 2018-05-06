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
ms.openlocfilehash: 91ebb0c35687b231a6f08b7bc92cccb83cf0e602
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação

Para instalar o cliente do Configuration Manager em dispositivos Windows 10 através da autenticação do Azure AD, integre o Configuration Manager com o Azure Active Directory (Azure AD). Os clientes podem estar na intranet comunique diretamente com um ponto de gestão ativado para HTTPS. Também podem ser baseados na internet comunicar através de CMG ou com um ponto de gestão baseado na internet. Este processo utiliza o Azure AD para autenticar clientes para o site do Configuration Manager. Azure AD substitui a necessidade de configurar e utilizar certificados de autenticação de cliente.



## <a name="before-you-begin"></a>Antes de começar

- Um inquilino do Azure AD é um pré-requisito  

- Requisitos de dispositivo:  

    - Windows 10  

    - Associado para o Azure AD, nuvem pura associados a um domínio ou híbrida do Azure associada ao AD  

- Requisitos de utilizador:  

    - O utilizador com sessão iniciada tem de ser uma identidade do Azure AD.   

    - Se o utilizador é uma identidade federada ou sincronizada, tem de utilizar o Configuration Manager [deteção de utilizadores do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) , bem como [deteção de utilizadores do Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc). Para obter mais informações sobre as identidades híbridas, consulte [definir uma estratégia de adoção de identidade híbrida](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->  

- Para além de [pré-requisitos existentes](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012MPpreq) para a função de sistema de sites do ponto de gestão, também de ativar **ASP.NET 4.5** neste servidor. Inclua quaisquer outras opções selecionadas automaticamente ao ativar o ASP.NET 4.5.  

- Configure todos os pontos de gestão para o modo HTTPS. Para obter mais informações, consulte [requisitos dos certificados PKI](/sccm/core/plan-design/network/pki-certificate-requirements) e [implementar o certificado de servidor web para sistemas de sites que executam o IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  
    - Se estiver a utilizar o gateway de gestão de nuvem, em seguida, apenas terá de configurar HTTPS para pontos de gestão que ativar para o gateway de gestão de nuvem.
    - Se estiver a implementar os clientes da intranet através da autenticação baseada em tokens do AD do Azure, em seguida, todos os pontos de gestão que estes clientes podem contactar tem de estar ativados para HTTPS. 

- Configure opcionalmente um [gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (CMG) para implementar clientes baseados na internet. Para clientes no local que autenticar com o Azure AD, não precisa de um CMG.  


## <a name="configure-azure-services-for-cloud-management"></a>Configurar os serviços do Azure para a gestão de nuvem

Ligar o seu site do Configuration Manager para o Azure AD como o primeiro passo. Para obter detalhes sobre este processo, consulte [serviços do Azure configurar](/sccm/core/servers/deploy/configure/azure-services-wizard). Criar uma ligação para o **gestão de nuvem** serviço.

Ativar [do Azure AD User Discovery](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc) como parte da integração do **gestão de nuvem**. 

Depois de concluir estas ações, o site do Configuration Manager está ligado ao Azure AD. 



## <a name="configure-client-settings"></a>Configurar definições de cliente

Estas definições de cliente ajudam a adesão ao Windows 10 dispositivos com o Azure AD. Permitem que também, os clientes baseados na internet utilizar o ponto de distribuição CMG e na nuvem.

1.  Configure as seguintes definições de cliente no **serviços em nuvem** secção utilizando as informações [como configurar as definições de cliente](/sccm/core/clients/deploy/configure-client-settings).  

    - **Permitir o acesso ao ponto de distribuição de nuvem**: Ative esta definição ajudar a dispositivos baseados na internet, obter o conteúdo necessário para instalar o cliente do Configuration Manager. Se o conteúdo não está disponível no ponto de distribuição de nuvem, o dispositivo pode obter o conteúdo do CMG. O arranque de instalação de cliente tentará novamente o ponto de distribuição em nuvem para quatro horas antes de retrocede para o CMG.<!--495533-->  

    - **Registar automaticamente novos dispositivos do Windows 10 associados a um domínio com o Azure Active Directory**: Definido como **Sim** ou **não**. A predefinição é **Sim**. Este comportamento também é a predefinição no Windows 10, versão 1709.

    - **Permitir que os clientes utilizar um gateway de gestão de nuvem** – definido como **Sim** (predefinição), ou **não**.  

2.  Implemente as definições de cliente na coleção de dispositivos necessária. Não implemente estas definições em coleções de utilizadores.

Para confirmar que o dispositivo é associado para o Azure AD, execute `dsregcmd.exe /status` numa linha de comandos. O **AzureAdjoined** campo no mostra resultados **Sim** se o dispositivo estiver associado a um AD do Azure.



## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Instalar e registar o cliente utilizando a identidade do Azure AD

Para instalar manualmente o cliente utilizando a identidade do Azure AD, reveja o processo geral na [como instalar clientes manualmente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual). 

 > [!Note]  
 > O dispositivo precisa de acesso à internet para contactar o Azure AD, mas não tem de ser baseado na internet. 

O exemplo seguinte mostra a estrutura geral da linha de comandos: `ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

Para obter mais informações, consulte [as propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties).

As propriedades CCMHOSTNAME e /mp especificam um dos seguintes, consoante o cenário:
- Ponto de gestão no local. Especifique apenas a propriedade /mp. O CCMHOSTNAME não é necessária.
- Gateway de gestão de nuvem
- Especifica o ponto de gestão baseado na Internet propriedade SMSMP o no local ou ponto de gestão baseado na internet.

Este exemplo utiliza um gateway de gestão de nuvem. -Substitui os valores de exemplo para cada propriedade: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

Para automatizar a instalação de cliente através da identidade do Azure AD através do Microsoft Intune, consulte o processo para [dispositivos de preparar o Windows 10 para gestão conjunta](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).



## <a name="next-steps"></a>Passos seguintes

Depois de concluído, pode continuar a [monitorizar e gerir clientes](/sccm/core/clients/manage/monitor-clients).

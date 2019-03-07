---
title: Instalar o cliente com o Azure AD
titleSuffix: Configuration Manager
description: Instale e atribua o cliente do Configuration Manager em dispositivos Windows 10 com o Azure Active Directory para autenticação
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b45c5938e9c1980802055bd73d5fd7e71122fc2a
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558121"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação

Para instalar o cliente do Configuration Manager em dispositivos Windows 10 com a autenticação do Azure AD, integre o Configuration Manager com o Azure Active Directory (Azure AD). Os clientes podem estar na intranet comunique diretamente com um ponto de gestão que suporte HTTPS ou qualquer ponto de gestão num site ativada para HTTP avançada. Eles também podem ser baseados na internet comunicam através de CMG ou com um ponto de gestão baseado na Internet. Este processo utiliza o Azure AD para autenticar clientes para o site do Configuration Manager. O Azure AD substitui a necessidade de configurar e utilizar certificados de autenticação de cliente.

Configurar o Azure AD pode ser mais fácil para alguns clientes do que a configuração de uma infraestrutura de chaves públicas para autenticação baseada em certificado. Existem recursos que exigem que integre o site para o Azure AD, mas não requerem necessariamente os clientes ser associado ao AD do Azure.<!-- SCCMDocs issue 1259 --> Para obter mais informações, veja os artigos seguintes:
- [Plano para o Azure Active Directory](/sccm/core/plan-design/security/plan-for-security#bkmk_planazuread)
- [Utilizar o Azure AD para a cogestão](/sccm/comanage/quickstart-hybrid-aad)



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

A partir da versão 1810, o site publica adicionais do Azure informações de AD para o gateway de gestão da cloud (CMG). Um cliente do Azure AD associado obtém essas informações de CMG, durante o processo de ccmsetup, utilizar o mesmo inquilino ao qual está associado. Este comportamento ainda mais simplifica a instalação do cliente num ambiente com mais do que um inquilino do Azure AD. Agora, as propriedades de ccmsetup necessárias apenas duas são **CCMHOSTNAME** e **SMSSiteCode**.<!--3607731-->

Para automatizar a instalação de cliente com a identidade do Azure AD através do Microsoft Intune, consulte [como preparar os dispositivos baseados na internet para a cogestão](/sccm/comanage/how-to-prepare-win10#install-the-configuration-manager-client).



## <a name="next-steps"></a>Passos seguintes

Depois de concluído, pode continuar a [monitorizar e gerir clientes](/sccm/core/clients/manage/monitor-clients).

---
title: Instale e atribua o cliente a partir da internet
titleSuffix: Configuration Manager
description: Instale e atribua o cliente do System Center Configuration Manager a partir da internet.
ms.custom: na
ms.date: 8/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: "14"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 2ef7580f94864094e9420eb0f5a5c5b4dc9d6d24
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação

Pode utilizar os serviços de nuvem do Configuration Manager com o Azure AD para suportar os cenários seguintes:

- Instalar o cliente do Configuration Manager em dispositivos Windows 10 através da internet e manualmente que atribuir a um site do Configuration Manager (requer a função de sistema de sites de gateway de gestão de nuvem).
- Utilize o Azure AD para autenticar clientes para aceder aos seus sites do Configuration Manager. Azure AD substitui a necessidade de configurar e utilizar certificados de autenticação de cliente.
- Deteção de utilizadores do Azure AD para o site para utilizar em coleções e outras operações do Configuration Manager.

Utilize os seguintes passos para realizar esta tarefa:

- **Passo 1: Configurar a aplicação de serviços do Azure nos serviços de nuvem do Configuration Manager e configurar a deteção de utilizador do Azure AD**
- **Passo 2: Configurar o Gateway de gestão de nuvem** (opcional para clientes no local)
- **Passo 3: Configurar definições de cliente para associar os dispositivos Windows 10 com o Azure AD e permitir que os clientes utilizar o Gateway de gestão de nuvem**
- **Passo 4: Instalar e registar o cliente do Configuration Manager utilizando a identidade do Active Directory do Azure**


## <a name="before-you-start"></a>Antes de começar

- Tem de ter um inquilino do Azure AD.
- Os seus dispositivos tem de executar Windows 10, ser do Azure AD associado e de ter sessão iniciada com uma identidade do Azure AD. Os clientes também podem ser associado a um além para o Azure AD associada ao domínio).
- Para além de [pré-requisitos existentes](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) para função de sistema de sites do ponto de gestão, deve adicionalmente garantir que **ASP.NET 4.5** (e quaisquer outras opções selecionadas automaticamente) estão ativados no computador que aloja esta função de sistema de sites.
- Para utilizar o Configuration Manager para implementar o cliente:
    - Se pretender utilizar o Azure AD para autenticar em vez de certificados de cliente, configure, pelo menos, um ponto de gestão para o modo HTTPS.
        Se estiver a utilizar certificados de cliente em vez do Gateway de gestão de nuvem, um ponto de gestão HTTPS é opcional mas recomendado. Se estiver a utilizar Azure AD para autenticar, se para no local ou clientes de Internet, é necessário o ponto de gestão HTTPS.
    - Configure um Gateway de gestão de nuvem, se pretender implementar os clientes de Internet. Para clientes no local, que estão a autenticar com o Azure AD, não terá de configurar o Gateway de gestão de nuvem.


## <a name="step-1-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Passo 1: Configurar a aplicação de serviços do Azure nos serviços de nuvem do Configuration Manager

Esta ação liga o site do Configuration Manager para o Azure AD e é um pré-requisito para todas as outras operações nesta secção. 

Deteção de utilizadores do Azure AD é configurada como parte da *gestão de nuvem*. O procedimento para o fazer é detalhado passo **6** do procedimento [criar a aplicação web do Azure para utilização com o Configuration Manager](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp) no tópico *serviços do Azure configurar para utilização com o Configuration Manager*.
    
Depois de concluir o procedimento, ligou o seu site do Configuration Manager para o Azure AD. 

## <a name="step-2-set-up-the-cloud-management-gateway"></a>Passo 2: Configurar o Gateway de gestão de nuvem

Configure o Gateway de gestão de nuvem para o ajudar a ativar cenários de gestão de nuvem descritos neste tópico. Encontrar ajuda nos seguintes tópicos: 

- [Planear para o gateway de gestão de nuvem no Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway).
- [Configurar o gateway de gestão de nuvem para o Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway).
- [Gateway de gestão de nuvem de monitor no Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway).

## <a name="step-3-configure-client-settings-to-join-windows-10-devices-with-azure-ad-and-enable-clients-to-use-the-cloud-management-gateway"></a>Passo 3: Configurar definições de cliente para associar os dispositivos Windows 10 com o Azure AD e permitir que os clientes utilizar o Gateway de gestão de nuvem

1.  Configure as seguintes definições de cliente (localizado no **serviços em nuvem**) secção utilizando as informações [como configurar as definições de cliente](/sccm/core/clients/deploy/configure-client-settings).
    - **Permitir o acesso ao ponto de distribuição de nuvem** -ative esta definição para ajudar a dispositivos baseados na Internet para obter o conteúdo necessário para instalar o cliente do Configuration Manager. Se o conteúdo não está disponível no ponto de distribuição de nuvem, o dispositivo pode obter o conteúdo de um ponto de gestão ligado para o gateway de gestão de nuvem.
    - **Registar automaticamente novos dispositivos do Windows 10 associados a um domínio com o Azure Active Directory** – definido como **Sim** (predefinição), ou **não**.
    - **Permitir que os clientes utilizar um gateway de gestão de nuvem** – definido como **Sim** (predefinição), ou **não**.
2.  Implemente as definições de cliente na coleção de dispositivos necessária. Não implemente estas definições em coleções de utilizadores.

Para confirmar que o dispositivo é associado para o Azure AD, execute o comando **dsregcmd.exe /status** numa janela de linha de comandos. O **AzureAdjoined** campo no mostra resultados **Sim** se o dispositivo estiver do Azure AD associado.


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>Passo 4: Instalar e registar o cliente do Configuration Manager utilizando a identidade do Active Directory do Azure

Para instalar o cliente, utilize as instruções no [como implementar clientes em computadores Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) utilizando a seguinte linha de comandos de instalação: 

**ccmsetup.exe /mp &#58; https://contoso.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode = DFD SMSMP = https://SCCMDFPSS.contoso.corp.contoso.com AADTENANTID = 72F988BF-86F1-41AF-91AB-2D7CD011DB47 AADTENANTNAME = contoso AADCLIENTAPPID = bef323b3-042f-41a6-907a-f9faf0d17026 AADRESOURCEURI = https://contososerver**

- **/MP** – origem da transferência. Pode definir para CMG se arranque de configuração de internet.
- **CCMHOSTNAME:** O nome do seu ponto de gestão de Internet. Pode encontrá-lo executando **gwmi - espaço de nomes root\ccm\locationservices-classe SMS_ActiveMPCandidate** numa linha de comandos num cliente gerido.
- **SMSSiteCode:** O código do site do site do Configuration Manager.
- **SMSMP:** O nome do seu ponto de gestão de pesquisa – o ponto de gestão pode ser na sua intranet.
- **AADTENANTID:**, **AADTENANTNAME:** O ID e nome do inquilino do Azure AD ligado para o Configuration Manager. Pode encontrar isto executando dsregcmd.exe /status numa linha de comandos num Azure AD associada ao dispositivo.
- **AADCLIENTAPPID:** O ID de aplicação de cliente do Azure AD. Para ajudar a encontrar isto, consulte [portal de utilização para criar um Azure Active Directory principal de serviço e aplicação que pode aceder aos recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri:** O identificador URI da aplicação de servidor integradas do Azure AD. Para obter mais informações, consulte [serviços do Azure configurar para utilização com o Configuration Manager](/sccm/core/servers/deploy/configure/azure-services-wizard).




## <a name="next-steps"></a>Passos seguintes

Depois de concluído, pode continuar a [monitorizar e gerir clientes](/sccm/core/clients/manage/monitor-clients).

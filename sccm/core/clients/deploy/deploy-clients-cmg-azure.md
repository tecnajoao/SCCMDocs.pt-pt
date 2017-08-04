---
title: Instale e atribua o cliente a partir da internet | Microsoft Docs
description: Instale e atribua o cliente do System Center Configuration Manager a partir da internet.
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: 14
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: MT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: f604557d208b2dda9dc1c6b4c4d27d896d47695e
ms.contentlocale: pt-pt
ms.lasthandoff: 07/29/2017

---

# <a name="install-and-assign-configuration-manager-clients-from-the-internet-using-azure-ad-for-authentication"></a>Instale e atribua os clientes do Configuration Manager através da Internet com o Azure AD para autenticação

Pode utilizar os serviços de nuvem do Configuration Manager com o Azure AD para suportar os cenários seguintes:

- Instalar o cliente do Configuration Manager a partir da internet e que o atribua a um site do Configuration Manager (requer a função de sistema de sites de gateway de gestão de nuvem) manualmente.
- Utilize o Azure AD para autenticar clientes na Internet para aceder os sites do Configuration Manager. Azure AD substitui a necessidade de configurar e utilizar certificados de autenticação de cliente.
- Deteção de utilizadores do Azure AD para o site para utilizar em coleções e outras operações do Configuration Manager.

Utilize os seguintes passos para realizar esta tarefa:

- **Passo 1: Configurar o Gateway de gestão de nuvem**
- **Passo 2: Configurar a aplicação de serviços do Azure nos serviços de nuvem do Configuration Manager**
- **Passo 3: Configurar definições de cliente para registar dispositivos Windows 10 com o Azure AD**
- **Passo 4: Instalar e registar o cliente do Configuration Manager utilizando a identidade do Active Directory do Azure**


## <a name="before-you-start"></a>Antes de começar

- Tem de ter um inquilino do Azure AD.
- Os seus dispositivos tem de executar o Windows 10 e ser do Azure AD associado. Os clientes também podem ser associado a um além para o Azure AD associada ao domínio).
- Para além de [pré-requisitos existentes](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) para função de sistema de sites do ponto de gestão, deve adicionalmente garantir que **ASP.NET 4.5** (e quaisquer outras opções selecionadas automaticamente) estão ativados no computador que aloja esta função de sistema de sites.
- Para utilizar o Configuration Manager para implementar o cliente:
    - Configure pelo menos um ponto de gestão para o modo HTTPS.
    - Configure um Gateway de gestão de nuvem.

## <a name="step-1-set-up-the-cloud-management-gateway"></a>Passo 1: Configurar o Gateway de gestão de nuvem

Configure o Gateway de gestão de nuvem para permitir que os clientes aceder ao site do Configuration Manager através da internet sem a utilização de certificados. Encontrar ajuda nos seguintes tópicos: 

- [Planear para o gateway de gestão de nuvem no Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway).
- [Configurar o gateway de gestão de nuvem para o Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway).
- [Gateway de gestão de nuvem de monitor no Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway).

## <a name="step-2-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Passo 2: Configurar a aplicação de serviços do Azure nos serviços de nuvem do Configuration Manager

Esta ação liga o site do Configuration Manager para o Azure AD e é um pré-requisito para todas as outras operações nesta secção. 

Deteção de utilizadores do Azure AD é configurada como parte da *gestão de nuvem*. O procedimento para o fazer é detalhado passo **6** do procedimento [criar a aplicação web do Azure para utilização com o Configuration Manager](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp) no tópico *serviços do Azure configurar para utilização com o Configuration Manager*.
    
Depois de concluir o procedimento, ligou o seu site do Configuration Manager para o Azure AD. 

## <a name="step-3-configure-client-settings-to-register-windows-10-devices-with-azure-ad"></a>Passo 3: Configurar definições de cliente para registar dispositivos Windows 10 com o Azure AD

1.  Configurar a secção de definições (que se encontra nos serviços de nuvem) do cliente utilizando as informações [como configurar as definições de cliente](/sccm/core/clients/deploy/configure-client-settings).
    - **Registar automaticamente novos dispositivos do Windows 10 associados a um domínio com o Azure Active Directory** – definido como **Sim** (predefinição), ou **não**.
    - **Permitir que os clientes utilizar um gateway de gestão de nuvem** – definido como **Sim** (predefinição), ou **não**.
2.  Implemente as definições de cliente na coleção de dispositivos necessária.

Para confirmar que o dispositivo é associado para o Azure AD, execute o comando **dsregcmd.exe /status** numa janela de linha de comandos. O **AzureAdjoined** campo no mostra resultados **Sim** se o dispositivo estiver do Azure AD associado.


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>Passo 4: Instalar e registar o cliente do Configuration Manager utilizando a identidade do Active Directory do Azure

Antes de começar, certifique-se de que os ficheiros de origem de instalação do cliente são armazenados localmente no dispositivo para o qual pretende instalar o cliente. Em seguida, utilize as instruções no [como implementar clientes em computadores Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) utilizando a seguinte linha de comandos de instalação: 

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode = HEC AADTENANTID = 780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME = contoso AADCLIENTAPPID = AADRESOURCEURI = https://contososerver**

- **/ /Nocrlcheck:** Se na nuvem ou ponto de gestão de gateway de gestão utiliza um certificado de servidor não público, em seguida, o cliente poderá não ser capaz de alcançar a localização da CRL.
- **/ Origem:** Pasta local: Localização dos ficheiros de instalação de cliente.
- **CCMHOSTNAME:** O nome do seu ponto de gestão de Internet. Pode encontrá-lo executando **gwmi - espaço de nomes root\ccm\locationservices-classe SMS_ActiveMPCandidate** numa linha de comandos num cliente gerido.
- **SMSMP:** O nome do seu ponto de gestão de pesquisa – o ponto de gestão pode ser na sua intranet.
- **SMSSiteCode:** O código do site do site do Configuration Manager.
- **AADTENANTID:**, **AADTENANTNAME:** O ID e nome do inquilino do Azure AD ligado para o Configuration Manager. Pode encontrar isto executando dsregcmd.exe /status numa linha de comandos num Azure AD associada ao dispositivo.
- **AADCLIENTAPPID:** O ID de aplicação de cliente do Azure AD. Para ajudar a encontrar isto, consulte [portal de utilização para criar um Azure Active Directory principal de serviço e aplicação que pode aceder aos recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri:** O identificador URI da aplicação de servidor integradas do Azure AD.


## <a name="next-steps"></a>Passos seguintes

Depois de concluído, pode continuar a [monitorizar e gerir clientes](/sccm/core/clients/manage/monitor-clients).


---
title: Utilizar o Azure AD para a cogestão
titleSuffix: Configuration Manager
description: Com o Azure AD pode tirar partido do maior produtividade para os utilizadores e a segurança para os seus recursos em ambientes de cloud e no local
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3b773c0bfe8cd0f8253a67ac96f5a0113b7206c0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135707"
---
# <a name="use-azure-ad-for-co-management"></a>Utilizar o Azure AD para a cogestão

Na cloud, a identidade é o novo plano de controlo. Azure Active Directory (Azure AD) permite-lhe ligar os seus utilizadores, dispositivos e aplicações em ambientes de cloud e no local. Registar os seus dispositivos com o Azure AD permite-lhe melhorar a produtividade para os seus utilizadores e de segurança para os seus recursos. Ter dispositivos no Azure AD é a base para a cogestão e acesso condicional com base no dispositivo. 

Para obter mais informações sobre o acesso condicional com base no dispositivo, consulte [como: Exigir que os dispositivos geridos para aceder à aplicação de cloud com o acesso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)

No vídeo seguinte, gerente de programas sênior Sandeep Deo e produto de marketing manager abordar a Adam Harbour e demonstração do Azure AD para a cogestão:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

O Azure AD fornece duas opções para dispositivos pertencentes à empresa para se adequar às necessidades da sua organização:  

- **Dispositivos associados ao AD Azure**: Associar os dispositivos Windows 10 ao Azure AD sem a necessidade de associá-las ao seu Active Directory no local  

    - Suporta o Windows 10

    - Configurar sem a necessidade de qualquer configuração adicional para seus ambientes no local  

    - Ao ativar a algumas configurações no Azure AD, pode ativar os seus utilizadores associar dispositivos ao Azure AD através da experiência de configuração do Windows (OOBE)  

    - Para obter mais informações, consulte [como: Planear a implementação de associação do Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  

- **Híbrido do Azure dispositivo associado ao AD**: Junte-se os dispositivos associados a um domínio existentes para o Azure AD  

    - Suporta o Windows 10, Windows 8.1 e Windows 7

    - Configurar com afirmações do AD FS ou o Azure AD Connect  

    - Para o Windows 10 a associação acontece no contexto do computador, para que os utilizadores não têm de efetuar passos adicionais  

    - Para obter mais informações, consulte [como planear a sua implementação híbrida do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)  

As duas opções fornecem funcionalidade semelhante para os utilizadores. É flexível para que escolha uma com base nas suas necessidades. Por exemplo, pode [aceder aos seus recursos no local](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso) das máquinas associado ao AD do Azure, embora eles não estão associados ao Active Directory. 

Pode associar dispositivos ao Azure AD em vários ambientes, quer sua [método de autenticação](https://docs.microsoft.com/azure/security/azure-ad-choose-authn). Por exemplo, autenticação federada ou autenticação na nuvem. 

Se já tiver um Active Directory no local, é simples configurar qualquer uma das opções. 



## <a name="benefits"></a>Benefícios

Associação de dispositivos para o Azure AD fornece as seguintes vantagens para a sua organização:

#### <a name="single-sign-on-to-cloud-resources"></a>Início de sessão único a recursos na cloud
Em dispositivos associados ao Azure AD, obtenha uma experiência integrada aceder a quaisquer recursos na cloud ou no local. Depois de iniciar sessão a uma máquina do Windows que está associada ao Azure AD, tem de início de sessão único para todas as aplicações sem as instruções de início de sessão adicionais.  

#### <a name="windows-hello-for-business"></a>Windows Hello para Empresas
Windows Hello para empresas traz uma autenticação segura sem palavra-passe para o Windows 10. Ao aderir ao seus dispositivos com o Azure AD, pode ativar o Windows Hello para empresas em seu utilizador de base para os recursos na cloud e no local. Windows Hello para empresas, elimina o problema de memorizar palavras-passe complexas ou inadvertidamente expô-los. O processo de início de sessão é simples e seguro. 

Para obter mais informações, consulte [Windows Hello para empresas](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

#### <a name="device-based-conditional-access"></a>Acesso condicional baseado no dispositivo
Ative o acesso condicional com base no estado do dispositivo para proteger melhor os dados da sua organização. Acesso condicional com base no dispositivo requer um dispositivo gerido. Este dispositivo tem de ser um dispositivo em conformidade ou de uma mistura de dispositivos no Azure AD associado. Para dispositivos associados ao AD do Azure, terá do Intune para marcar dispositivos como estando em conformidade. Mas para híbrido do Azure dispositivos associados ao AD, o estado do dispositivo em si é usado para avaliar o acesso condicional. Cogestão fornece-lhe a vantagem adicional de avaliação de conformidade através do Intune para híbrido do Azure dispositivos associados ao AD. Esta funcionalidade torna-se de que a configuração do dispositivo estiver intacta. 

Para obter mais informações sobre o acesso condicional com base no dispositivo, consulte [como: Exigir que os dispositivos geridos para aceder à aplicação de cloud com o acesso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).  

#### <a name="automatic-device-licensing"></a>Licenciamento de dispositivos automática
Todos os dispositivos Windows 10 associados ao Azure AD percorrer as verificações de licença. Estas verificações permitem-lhe automaticamente o atualizar do Pro para a empresa por meio da nuvem da Microsoft. Ao remover a subscrição relevante do usuário, o dispositivo desatualize automaticamente sua licença. Esta funcionalidade fornece um único painel de controlo para gerir licenças do Windows, sem quaisquer processos complicadas ou sistemas no local.

#### <a name="self-service-functionality"></a>Funcionalidade de autoatendimento
Funcionalidade self-service inclui a reposição de palavra-passe self-service e a chave de recuperação do BitLocker. O Azure AD também fornece opções diretas para repor a palavra-passe ou chaves de recuperação do BitLocker de acesso. Pode utilizar o Azure AD para repor a palavra-passe diretamente a partir do ecrã de bloqueio do Windows, em vez de num browser. Estas funcionalidades reduzem o atrito para utilizadores e ajudar a reduzir os custos de suporte técnico para a sua organização.  

Para obter mais informações, consulte [início rápido: Reposição de palavra-passe self-service](https://docs.microsoft.com/azure/active-directory/authentication/quickstart-sspr).

#### <a name="enterprise-state-roaming"></a>Roaming de estado empresarial
Todos os dispositivos associados ao Azure AD podem sincronizar as definições para a cloud. Todos os dispositivos aos quais um utilizador inicia sessão no sincronizações todas as suas definições para uma experiência mais produtiva.  



## <a name="value-proposition"></a>Proposta de valor

Associar os seus dispositivos com o Azure AD através de qualquer um dos métodos acelera a sua transformação digital. Ele permite mais funcionalidade fornecida pelo Microsoft 365. Terá melhores experiências e terá maior segurança para os seus dados. 

O Azure AD fornece várias opções para facilitar seu trabalho carregar, por exemplo:

- Gerir todas as identidades de dispositivos na sua organização a partir de um único local  

- Reduza os custos de suporte técnico ao ativar a reposição de palavra-passe self-service. Em seguida, os utilizadores pode repor a palavra-passe de ecrã de bloqueio do Windows 10 no seu dispositivo em qualquer altura.  



## <a name="configure"></a>Configurar

Se já tiver um ambiente do Active Directory no local e pretender associar os dispositivos associados a um domínio ao Azure AD, híbrido do Azure de configurar dispositivos associados ao AD. Para obter mais informações, [como planear a sua implementação híbrida do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan). 

O Configuration Manager possui um definição de cliente [automaticamente registar novos dispositivos associados a um domínio do Windows 10 no Azure AD](/sccm/core/clients/deploy/about-client-settings#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory). Para obter mais informações sobre como configurar as definições de cliente, consulte [como configurar as definições de cliente](/sccm/core/clients/deploy/configure-client-settings).

Se quiser configurar o Azure AD-associação para os seus dispositivos sem também associá-los ao seu domínio no local, reveja as considerações para o Azure associação AD no seu ambiente. Depois de decidir ficar com a associação do Azure AD, tem muitas opções para implantá-lo com base nas necessidades da sua organização. Para obter mais informações, veja os artigos seguintes:
- [Como: Planear a implementação de associação do Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  
- [Compreender as opções de aprovisionamento](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)  


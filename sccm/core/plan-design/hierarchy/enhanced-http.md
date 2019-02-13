---
title: HTTP avançado
titleSuffix: Configuration Manager
description: Utilize autenticação moderna para proteger a comunicação de cliente sem a necessidade de certificados PKI.
ms.date: 10/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2b8d9c3480c86b282c9780395980625f86ee82e6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156928"
---
# <a name="enhanced-http"></a>HTTP avançado

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1356889,1358460-->

> [!Tip]  
> Esse recurso foi introduzido pela primeira vez na versão 1806 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1810, esta funcionalidade já não é uma funcionalidade de pré-lançamento.  


A Microsoft recomenda utilizar comunicações HTTPS para todos os caminhos de comunicação do Configuration Manager, mas é um desafio para alguns clientes devido à sobrecarga de gerenciamento de certificados PKI. A introdução do Azure Active Directory integration (Azure AD) reduz alguns, mas nem todos os requisitos de certificado. 

O Configuration Manager versão 1806 inclui melhorias à forma como os clientes comunicam com sistemas de sites. Existem dois objetivos principais para esses aprimoramentos:  

- Pode proteger a comunicação de cliente confidenciais sem a necessidade de certificados de autenticação de servidor PKI.  

- Os clientes com segurança podem aceder a conteúdo de pontos de distribuição sem a necessidade de uma conta de acesso à rede, o certificado PKI de cliente e a autenticação do Windows.  

> [!Note]  
> Os certificados PKI ainda são uma opção válida para os clientes com os seguintes requisitos:   
> - Todas as comunicações de cliente é efetuada através de HTTPS  
> - Controle avançado da infraestrutura de assinatura  


## <a name="bkmk_scenario"></a> Cenários

Os cenários seguintes se beneficiar desses aprimoramentos:  


### <a name="bkmk_scenario1"></a> Cenário 1: Cliente para ponto de gestão
<!--1356889-->

[Dispositivos associados ao AD Azure](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices) pode comunicar com um ponto de gestão configurado para HTTP. O servidor de site gera um certificado para o ponto de gestão que lhe permite comunicar através de um canal seguro.   

> [!Note]  
> Este comportamento é alterado do Configuration Manager versão do ramo atual 1802, que requer um ponto de gestão que suporte HTTPS para clientes do Azure AD associado comunicam através de um gateway de gestão na cloud. Para obter mais informações, consulte [ativar o ponto de gestão para HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  


### <a name="bkmk_scenario2"></a> Cenário 2: Cliente para ponto de distribuição
<!--1358228-->

Um grupo de trabalho ou o cliente do Azure associados ao AD pode autenticar e transfiram conteúdo através de um canal seguro de um ponto de distribuição configurado para HTTP. Esses tipos de dispositivos também podem autenticar e transferir conteúdo de um ponto de distribuição configurado para HTTPS sem a necessidade de um certificado PKI no cliente. É um desafio para adicionar um certificado de autenticação de cliente a um grupo de trabalho ou o cliente do Azure AD associado.

Este comportamento inclui cenários de implementação do sistema operacional com uma sequência de tarefas em execução a partir do suporte de dados, o PXE ou o Centro de Software. Para obter mais informações, consulte [conta de acesso à rede](/sccm/core/plan-design/hierarchy/accounts#network-access-account).<!--1358278-->


### <a name="bkmk_scenario3"></a> Cenário 3: Identidade de dispositivo do Azure AD 
<!--1358460-->

Azure AD associado ou [dispositivos do Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices) sem um Azure AD utilizador com sessão iniciada pode comunicar de forma segura com o respetivo site atribuído. A identidade de dispositivo com base na cloud agora é suficiente para se autenticar com o ponto de gestão e CMG para cenários de TI centradas em dispositivo. (Um token de usuário é ainda necessário para cenários de centrada no utilizador.)  


## <a name="prerequisites"></a>Pré-requisitos  

- Um ponto de gestão configurado para ligações de cliente HTTP. Defina esta opção no **gerais** separador de propriedades de função do sistema de sites.  

- Um ponto de distribuição configurado para ligações de cliente HTTP. Defina esta opção no **gerais** separador de propriedades de função do sistema de sites. Não ative a opção para **permitir a ligação anónima dos clientes**.  

- Carregar o site para o Azure AD para gestão na cloud.  

    - Se já tiver cumprido este pré-requisito para o seu site, tem de atualizar a aplicação do Azure AD. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **serviços Cloud**e selecione **inquilinos do Azure Active Directory do**. Selecione o inquilino do Azure AD, selecione a aplicação web no **aplicativos** painel e, em seguida, selecione **atualização da definição de aplicação** na faixa de opções.  

- *Para [cenário 3](#bkmk_scenario3) apenas*: Um cliente com o Windows 10 versão 1803 ou posterior e associado ao Azure AD. 



## <a name="configure-the-site"></a>Configurar o site

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó. Selecione o site e escolha **propriedades** na faixa de opções.  

2. Mude para o **comunicação do computador cliente** separador. Selecione a opção para **HTTPS ou HTTP** e, em seguida, ative a opção para **sistemas de sites de certificados gerados pelo utilize o Gestor de configuração para HTTP**.  

> [!Tip]
> Aguarde até 30 minutos para o ponto de gestão receber e configurar o novo certificado do site.

Pode ver estes certificados na consola do Configuration Manager. Vá para o **administração** área de trabalho, expanda **Security**e selecione o **certificados** nó. Procure o **SMS emitir** certificado de raiz, bem como os certificados de função de servidor de site emitidos por raiz emissora de SMS.

Para obter mais informações sobre como o cliente comunica com o ponto de gestão e o ponto de distribuição com esta configuração, consulte [comunicações de clientes para sistemas de sites e serviços](/sccm/core/plan-design/hierarchy/communications-between-endpoints#Planning_Client_to_Site_System).



## <a name="see-also"></a>Consulte também
- [Plano de segurança](/sccm/core/plan-design/security/plan-for-security)  

- [Segurança e privacidade para clientes do Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Configurar a segurança](/sccm/core/plan-design/security/configure-security)  

- [Comunicação entre pontos de extremidade](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  


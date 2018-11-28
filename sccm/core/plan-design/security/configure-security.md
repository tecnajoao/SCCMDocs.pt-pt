---
title: Configurar a segurança
titleSuffix: Configuration Manager
description: Configure opções relacionadas com segurança para o Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d1aaf6db583d9749dda3be14cfd06acbff19b093
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456095"
---
# <a name="configure-security-in-configuration-manager"></a>Configurar a segurança no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as informações neste artigo para ajudar a configurar as opções relacionadas com a segurança para o Configuration Manager. Ela abrange as seguintes opções de segurança:
- [Comunicação do computador cliente](#BKMK_ConfigureClientPKI) para certificados PKI de cliente  
- [Assinatura e encriptação](#BKMK_ConfigureSigningEncryption)  
- [Administração baseada em funções](#BKMK_ConfigureRBA)  
- [Gerir contas](#BKMK_ManageAccounts)  
- [Configurar o Azure Active Directory](#bkmk_azuread)  
- [Configurar a autenticação de fornecedor de SMS](#bkmk_auth)  



##  <a name="BKMK_ConfigureClientPKI"></a> Configurar definições para certificados PKI de cliente  

Se pretender utilizar certificados da infraestrutura de chaves públicas (PKI) para ligações de cliente aos sistemas de sites que utilizam os Serviços de Informação Internet (IIS), utilize o seguinte procedimento para configurar as definições destes certificados.  

#### <a name="to-configure-client-pki-certificate-settings"></a>Para configurar as definições de certificados PKI de cliente  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó. Selecione o site primário a configurar.  

2.  No Friso, selecione **propriedades**. Em seguida, mude para o **comunicação do computador cliente** separador.  

    Este separador apenas está disponível num site primário. Se não vir a **comunicação do computador cliente** separador, certifique-se de que não está ligado a um site de administração central ou um site secundário.  

3.  Selecione as definições para os sistemas de sites que utilizam IIS.  

    - **Apenas HTTPS**: Os clientes que estão atribuídos ao site sempre utilizar um certificado PKI de cliente ao estabelecerem ligações aos sistemas de sites que utilizam IIS.  

    - **HTTPS ou HTTP**: Não precisa que os clientes utilizem certificados PKI.  

    - **Sistemas de sites de certificados gerados pelo utilize o Gestor de configuração para HTTP**: Para obter mais informações sobre esta definição, consulte [avançada HTTP](/sccm/core/plan-design/hierarchy/enhanced-http).  

4.  Selecione as definições para computadores cliente.  

    - **Utilizar um certificado cliente PKI (capacidade de autenticação de cliente) quando estiverem disponíveis**: Se tiver escolhido o **HTTPS ou HTTP** definição do servidor do site, selecione esta opção para utilizar um cliente certificado PKI para ligações HTTP. O cliente utiliza este certificado em vez de um certificado autoassinado para se autenticar perante os sistemas de site. Se escolheu **apenas HTTPS**, esta opção será automaticamente escolhida.  

    Quando mais do que um certificado de cliente PKI válido está disponível num cliente, escolha **modificar** para configurar os métodos de seleção de certificado de cliente.  

    Para mais informações sobre o método de seleção de certificados de cliente, consulte [Planning for PKI client certificate selection](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForClientCertificateSelection).  

    - **Os clientes verificam a lista de revogação de certificados (CRL) para sistemas de sites**: Ative esta definição para clientes verificar a CRL da sua organização para certificados revogados.  

    Para mais informações sobre a verificação CRL para clientes, consulte [Planning for PKI certificate revocation](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs).  

5.  Para importar, visualizar e eliminar os certificados de autoridades de certificação de raiz fidedigna, escolha **definir**.  

    Para obter mais informações, consulte [planear a PKI fidedigna de certificados de raiz e os lista de emissores de certificados](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRootCAs).  


Repita este procedimento para todos os sites primários da hierarquia.  



##  <a name="BKMK_ConfigureSigningEncryption"></a> Configurar a assinatura e encriptação  

Configure as definições de assinatura e encriptação mais seguras para os sistemas de site que todos os clientes do site possam suportar. Estas definições são especialmente importantes quando permitir que os clientes comuniquem com os sistemas de site utilizando certificados autoassinados através de HTTP.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Para configurar a assinatura e encriptação para um site  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó. Selecione o site primário a configurar.  

2.  No Friso, selecione **propriedades**e, em seguida, mude para o **assinatura e encriptação** separador.  

    Este separador apenas está disponível num site primário. Se não vir a **assinatura e encriptação** separador, certifique-se de que não está ligado a um site de administração central ou um site secundário.  

3.  Configure as opções de assinatura e encriptação para os clientes comuniquem com o site.  

    - **Exigir assinatura**: Os clientes assinar dados antes de enviar para o ponto de gestão.  

    - **Exigir SHA-256**: Os clientes utilizam o algoritmo SHA-256, quando a assinatura de dados.  

    > [!WARNING]  
    >  Não **exigir SHA-256** sem primeiro confirmar que todos os clientes suportar este algoritmo hash. Esses clientes incluem aqueles que possam ser atribuídos ao site no futuro.  
    >   
    >  Se escolher esta opção e os clientes com certificados autoassinados não suportam SHA-256, o Configuration Manager rejeita-los. O componente SMS_MP_CONTROL_MANAGER regista o ID de mensagem 5443.  

    - **Utilize a encriptação**: Os clientes para encriptar mensagens de estado e dados de inventário do cliente antes de enviar para o ponto de gestão. Eles usam o algoritmo 3DES.  

Repita este procedimento para todos os sites primários da hierarquia.  



##  <a name="BKMK_ConfigureRBA"></a> Configurar a administração baseada em funções  

A administração baseada em funções combina funções de segurança, âmbitos de segurança e coleções atribuídas para definir o âmbito administrativo de cada utilizador administrativo. Um âmbito inclui os objetos que um utilizador pode ver na consola e as tarefas relacionadas com esses objetos que têm permissão para o fazer. As configurações de administração baseadas em funções são aplicadas em cada site de uma hierarquia.  

Para obter mais informações, consulte [configurar a administração baseada em funções](/sccm/core/servers/deploy/configure/configure-role-based-administration). Este artigo detalha as seguintes ações:  

- Criar funções de segurança personalizadas  

- Configurar funções de segurança  

- Configurar âmbitos de segurança para um objeto  

- Configurar coleções para gerir a segurança  

- Criar um novo utilizador administrativo  

- Modificar o âmbito administrativo de um utilizador administrativo  

> [!IMPORTANT]  
>  O seu próprio âmbito administrativo define os objetos e definições que pode atribuir ao configurar a administração baseada em funções para outro utilizador administrativo. Para obter informações sobre o planeamento da administração baseada em funções, consulte [Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).  



##  <a name="BKMK_ManageAccounts"></a> Gerir contas utilizadas pelo Configuration Manager  

O Configuration Manager suporta contas do Windows para muitas tarefas diferentes e utiliza. Para ver as contas que estão configuradas para diferentes tarefas e para gerir a palavra-passe utilizadas pelo Configuration Manager para cada conta, utilize o seguinte procedimento:  

#### <a name="to-manage-accounts-that-configuration-manager-uses"></a>Para gerir contas utilizadas pelo Configuration Manager  

1.  Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **Security**e, em seguida, selecione o **contas** nó.  

2.  Para alterar a palavra-passe para uma conta, selecione a conta na lista. Em seguida, escolha **propriedades** na faixa de opções.  

3.  Escolher **definir** para abrir o **conta de utilizador do Windows** caixa de diálogo. Especifique a palavra-passe nova para o Configuration Manager para utilizar para esta conta.  

    > [!NOTE]  
    >  A palavra-passe que especificar tem de corresponder à palavra-passe desta conta no Active Directory.  

Para obter mais informações, consulte [contas utilizadas no Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).



##  <a name="bkmk_azuread"></a> Configurar o Azure Active Directory

Integre o Configuration Manager com o Azure Active Directory (Azure AD) para simplificar e seu ambiente de cloud os. Ative o site e os clientes para autenticar com o Azure AD. Para obter mais informações, consulte a **gestão na Cloud** serviço na [dos serviços do Azure configurar](/sccm/core/servers/deploy/configure/azure-services-wizard).



## <a name="bkmk_auth"></a> Configurar a autenticação de fornecedor de SMS

A partir da versão 1810, pode especificar o nível mínimo de autenticação para os administradores aceder a sites do Configuration Manager. Esta funcionalidade aplica os administradores para iniciar sessão no Windows com o nível necessário. Para obter mais informações, consulte [planear o fornecedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth). <!--1357013-->  



## <a name="see-also"></a>Consulte também

- [Plano de segurança](/sccm/core/plan-design/security/plan-for-security)  

- [Segurança e privacidade para clientes do Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Comunicação entre pontos de extremidade](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

- [Referência técnica de controlos criptográficos](/sccm/core/plan-design/security/cryptographic-controls-tehnical-reference)  

- [Requisitos do certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements)  

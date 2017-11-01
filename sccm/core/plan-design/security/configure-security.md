---
title: "Configurar a segurança"
titleSuffix: Configuration Manager
description: "Configure opções relacionadas com segurança para o System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 94699e41291b7e1c7072962595aa71384b03f27b
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="configure-security-in-system-center-configuration-manager"></a>Configurar a segurança no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as informações neste artigo para o ajudar a configurar opções relacionadas com segurança para o System Center Configuration Manager.  

##  <a name="BKMK_ConfigureClientPKI"></a> Configurar definições para certificados PKI de cliente  
Se pretender utilizar certificados da infraestrutura de chaves públicas (PKI) para ligações de cliente aos sistemas de sites que utilizam os Serviços de Informação Internet (IIS), utilize o seguinte procedimento para configurar as definições destes certificados.  

#### <a name="to-configure-client-pki-certificate-settings"></a>Para configurar as definições de certificados PKI de cliente  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **configuração do Site**, escolha **Sites**e, em seguida, selecione o site primário a configurar.  

3.  No **home page** separador o **propriedades** grupo, escolha **propriedades**e, em seguida, escolha o **comunicação com o computador cliente** separador.  

    Este separador apenas está disponível num site primário. Se o separador **Comunicação com o Computador Cliente** não for apresentado, verifique se não se encontra ligado a um site de administração central ou a um site secundário.  

4.  Escolha **apenas HTTPS** quando quiser que os clientes atribuídos ao site utilizem sempre um certificado PKI de cliente ao estabelecerem ligações aos sistemas de sites que utilizam IIS. Em alternativa, escolha **HTTPS ou HTTP** quando não precisar que os clientes utilizem certificados PKI.  

5.  Se tiver escolhido **HTTPS ou HTTP**, escolha **utilizar um certificado cliente PKI (capacidade de autenticação de cliente) se estiver disponível** quando pretender utilizar um certificado PKI de cliente para ligações HTTP. O cliente utiliza este certificado em vez de um certificado autoassinado para se autenticar perante os sistemas de site. Esta opção é automaticamente escolhida se escolher **apenas HTTPS**.  

    Quando os clientes são detetados como estando na Internet ou estão configurados para gestão de clientes apenas na Internet, utilizam sempre um certificado PKI de cliente.  

6.  Escolha **modificar** para configurar o seu método de seleção de clientes preferido para quando mais do que uma válido certificado PKI de cliente estiver disponível num cliente e, em seguida, escolha **OK**.  

    Para obter mais informações sobre o método de seleção de certificados de cliente, consulte [planear a seleção de certificado de cliente PKI](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

7.  Selecione ou desmarque a caixa de verificação para que os clientes verifiquem a lista de Revogação de Certificados (CRL).  

    Para mais informações sobre CRL a verificação de clientes, consulte [planear a revogação de certificados PKI](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).  

8.  Se tiver de especificar certificados de autoridade (AC) de certificação de raiz fidedigna para os clientes, escolha **definir**, importe os ficheiros de certificado de AC de raiz e, em seguida, escolha **OK**.  

    Para obter mais informações sobre esta definição, consulte [planear os certificados PKI de raiz fidedigna e a lista de emissores de certificados](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRootCAs).  

9. Escolha **OK** para fechar a caixa de diálogo de propriedades para o site.  

Repita este procedimento para todos os sites primários da hierarquia.  

##  <a name="BKMK_ConfigureSigningEncryption"></a>Configurar a assinatura e encriptação  
Configure as definições de assinatura e encriptação mais seguras para os sistemas de site que todos os clientes do site possam suportar. Estas definições são especialmente importantes quando permitir que os clientes comuniquem com os sistemas de site utilizando certificados autoassinados através de HTTP.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Para configurar a assinatura e encriptação para um site  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **configuração do Site**, escolha **Sites**e, em seguida, selecione o site primário a configurar.  

3.  No **home page** separador o **propriedades** grupo, escolha **propriedades**e, em seguida, escolha o **assinatura e encriptação** separador.  

    Este separador apenas está disponível num site primário. Se o separador **Assinatura e Encriptação** não for apresentado, verifique se não se encontra ligado a um site de administração central ou a um site secundário.  

4.  Configurar as opções de assinatura e encriptação pretendidas e, em seguida, escolha **OK**.  

    > [!WARNING]  
    >  Não escolher **exigir SHA-256** sem verificar primeiro se todos os clientes que possam ser atribuídos ao site podem suportar este algoritmo hash ou têm um certificado de autenticação de cliente PKI válido. Poderá ter de instalar atualizações ou correções nos clientes para suportarem SHA-256. Por exemplo, os computadores com o Windows Server 2003 SP2 têm de instalar uma correção que é mencionada no [artigo KB 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666).  
    >   
    >  Se escolher esta opção e os clientes não puderem suportar SHA-256 e utilizarem certificados autoassinados, o Configuration Manager rejeita-los. Neste cenário, o componente SMS_MP_CONTROL_MANAGER regista o ID de mensagem 5443.  

5.  Escolha **OK** para fechar o **propriedades** caixa de diálogo para o site.  

Repita este procedimento para todos os sites primários da hierarquia.  

##  <a name="BKMK_ConfigureRBA"></a> Configurar a administração baseada em funções  
A administração baseada em funções combina funções de segurança, âmbitos de segurança e coleções atribuídas para definir o âmbito administrativo de cada utilizador administrativo. Um âmbito administrativo inclui os objetos que um utilizador administrativo pode ver na consola do Configuration Manager e as tarefas relacionadas com esses objetos que o utilizador administrativo tem permissão para efetuar. As configurações de administração baseadas em funções são aplicadas em cada site de uma hierarquia.  

As hiperligações seguintes são as secções relevantes do [configurar a administração baseada em funções para o System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md) artigo:  

-   [Criar funções de segurança personalizadas](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)  

-   [Configurar funções de segurança](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole)  

-   [Configurar âmbitos de segurança para um objeto](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope)  

-   [Configurar coleções para gerir a segurança](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl)  

-   [Criar um novo utilizador administrativo](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_Create_AdminUser)  

-   [Modificar o âmbito administrativo de um utilizador administrativo](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser)  

> [!IMPORTANT]  
>  O seu próprio âmbito administrativo define os objetos e definições que pode atribuir ao configurar a administração baseada em funções para outro utilizador administrativo. Para obter informações sobre o planeamento da administração baseada em funções, consulte [Noções básicas da administração baseada em funções para o System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md).  

##  <a name="BKMK_ManageAccounts"></a> Gerir contas utilizadas pelo Configuration Manager  
O Configuration Manager suporta contas do Windows para muitas tarefas diferentes e utiliza.  

Utilize o procedimento seguinte para contas de vista que estão configuradas para diferentes tarefas e para gerir a palavra-passe utilizadas pelo Configuration Manager para cada conta.  

#### <a name="to-manage-accounts-that-are-used-by-configuration-manager"></a>Para gerir contas utilizadas pelo Configuration Manager  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **segurança**e, em seguida, escolha **contas** para ver as contas que estão configuradas para o Configuration Manager.  

3.  Para alterar a palavra-passe para uma conta que está configurada para o Configuration Manager, selecione a conta.  

4.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

5.  Escolha **definir** para abrir o **conta de utilizador do Windows** diálogo caixa e especifique a palavra-passe para o Configuration Manager para utilizar para a conta de novo.  

    > [!NOTE]  
    >  A palavra-passe que especificar tem de corresponder à palavra-passe especificada para a conta em Utilizadores e Computadores do Active Directory.  

6.  Escolha **OK** para concluir o procedimento.  

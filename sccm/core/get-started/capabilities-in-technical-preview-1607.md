---
title: Funcionalidades no Technical Preview 1607
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1607."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
caps.latest.revision: "11"
author: erikje
ms.author: erikje
manager: angrobe
ms.openlocfilehash: e69bee88aa4afccbaee055b058ad0a3e68a0e180
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="capabilities-in-technical-preview-1607-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1607 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1607. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão do technical preview, reveja o tópico introdutórias, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="dmp_edition"></a>Política de atualização de melhoramentos para a edição do Windows 10

Nesta versão, as seguintes melhorias foram efetuadas a esta política:

* Agora, pode utilizar a política de atualização de edição com PCs Windows 10 com o Configuration Manager de cliente para além de Windows 10 PCs inscritos com o Microsoft Intune.
* Pode atualizar do Windows 10 Professional para qualquer uma das plataformas no Assistente de que são compatíveis com o seu hardware.

[Leia mais sobre a política de atualização de edição do Windows 10](/sccm/compliance/deploy-use/upgrade-windows-version)

### <a name="try-it-out"></a>Experimente!

1. Utilize as informações de [existente tópico de política de atualização de edição](/sccm/compliance/deploy-use/upgrade-windows-version) para criar uma política de atualização de edição.
2. Aplicar esta política para Windows 10 PC com o cliente do Configuration Manager.
Assim que a política atingir um PC Windows de destino, o PC será reiniciado dentro de duas horas para aplicar a atualização. Atualmente não pode suprimir este reinício. Certifique-se de informar os utilizadores nos quais implementou a política ou agendar a política a executar os utilizadores fora do horário de trabalho.

### <a name="known-issue-with-this-release"></a>Problema conhecido com esta versão
Nas definições de cliente do Configuration Manager, poderá ver as definições para **de atualização de edição**. Nesta versão, estas definições não estão funcionais. Utilize as instruções especificadas acima para atualizar o Windows 10 para uma versão mais recente.

## <a name="customizable-branding-for-software-center-dialogs"></a>Imagem Corporativa Personalizável para Caixas de Diálogo do Centro de Software

Uma imagem corporativa personalizado para o Centro de Software introduzida no Configuration Manager versão 1602. Na versão de pré-visualização técnica 1607, essa imagem corporativa abranger agora todas as caixas de diálogo associada e notificações da barra de tarefas para fornecer uma experiência mais consistente para utilizadores do Centro de Software.

### <a name="try-it-out"></a>Experimente!

Uma imagem corporativa personalizado para o Centro de Software é aplicada, de acordo com as seguintes regras:

1. Se a função de servidor de sites do ponto de Web site do catálogo de aplicações não está instalada, em seguida, o Centro de Software apresentará o nome da organização especificado no **agente do computador** definição de cliente **nome da organização apresentada no Centro de Software**. Para obter instruções, consulte [como configurar as definições de cliente](../../core/clients/deploy/configure-client-settings.md).

2. Se a função de servidor de sites do ponto de Web site do catálogo de aplicações estiver instalada, em seguida, o Centro de Software apresentará o nome da organização e a cor especificados nas propriedades de função do servidor de ponto de sites catálogo de aplicações Web site. Para obter mais informações, consulte [opções de configuração para o ponto de Web site do catálogo de aplicações](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

3. Se uma subscrição do Microsoft Intune estiver configurada e ligada ao ambiente do Configuration Manager, em seguida, o Centro de Software apresentará o nome da organização, o logótipo de cor e da empresa especificados nas propriedades de subscrição do Intune. Para obter mais informações, consulte [configurar a subscrição do Microsoft Intune](/mdm/deploy-use/configure-intune-subscription).

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>Implementações iniciadas por utilizar o mesmo adaptador de rede para vários PXE
Na versão de pré-visualização técnica 1607, quando utiliza um adaptador de ethernet de a imagem de vários dispositivos (por exemplo, um adaptador USB ethernet que utiliza em vários dispositivos), pode ativar uma nova definição que permite-lhe introduzir identificadores de hardware para os adaptadores de ethernet. Gestor de configuração ignora os identificadores de hardware na lista quando efetuar uma instalação de PXE e para o registo de cliente.

Para obter mais informações sobre este problema, consulte o [blogue de equipa do suporte de OSD do Configuration Manager](https://blogs.technet.microsoft.com/system_center_configuration_manager_operating_system_deployment_support_blog/2015/08/27/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in-system-center-configuration-manger-osd/).  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>Ativar a funcionalidade para gerir os identificadores de hardware duplicados  
1. Na consola do Configuration Manager, vá para **administração** > **descrição geral** > **serviços em nuvem** > **atualizações e manutenção** > **funcionalidades**.
2. No painel de visualização, selecione **identificadores de hardware duplicados gerir**.
3. No **home page** separador o **funcionalidades** , clique em **ativar**.

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Adicionar identificadores de hardware para o Configuration Manager para ignorar  
1. Na consola do Configuration Manager, vá para **administração** > **descrição geral** > **configuração do Site** > **Sites**.
2. No separador **Home Page** , no grupo **Sites** , clique em **Definições de Hierarquia**.
3. Vá para o **aprovação do cliente e registos em conflito** separador.
4. Clique em **adicionar** no **duplicado identificadores de hardware** secção para adicionar os identificadores de hardware novo.

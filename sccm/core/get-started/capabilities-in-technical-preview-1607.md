---
title: "Capacidades na pré-visualização técnica 1607 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1607."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
caps.latest.revision: 11
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 1b9e49da1a5bbfca93fe683b82d2c0056a22cc1f
ms.openlocfilehash: 4717e0f8eef01501fb5b5790e855c476c1ca4590
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1607-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1607 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1607. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="dmp_edition"></a>Melhoramentos para a edição do Windows 10 atualizar política

Nesta versão, as seguintes melhorias foram efetuadas a esta política:

* Agora, pode utilizar a política de atualização de edição com o Windows 10 PCs que executam o Configuration Manager de cliente para além de PCs do Windows 10 inscritos com o Microsoft Intune.
* Pode atualizar a partir do Windows 10 Professional a qualquer uma das plataformas no Assistente de que são compatíveis com o hardware.

[Leia mais sobre a política de atualização de edição do Windows 10](/sccm/compliance/deploy-use/upgrade-windows-version)

### <a name="try-it-out"></a>Experimente!

1. Utilize as informações de [existente tópico de política de atualização de edição](/sccm/compliance/deploy-use/upgrade-windows-version) para criar uma política de atualização de edição.
2. Aplicar esta política para um PC com Windows 10 executa o cliente do Configuration Manager.
Assim que a política atingir um PC Windows de destino, o PC será reiniciado dentro de duas horas para aplicar a atualização. Atualmente não pode suprimir este reinício. Certifique-se informar os utilizadores para os quais implementar a política, ou agendar a política para executar os utilizadores fora do horário de trabalho.

### <a name="known-issue-with-this-release"></a>Problemas conhecidos com esta versão
Nas definições de cliente do Configuration Manager, poderá ver as definições para **edição atualizar**. Nesta versão, estas definições não estão funcionais. Utilize as instruções indicadas acima ao atualizar o Windows 10 para uma versão mais recente.

## <a name="customizable-branding-for-software-center-dialogs"></a>Imagem Corporativa Personalizável para Caixas de Diálogo do Centro de Software

Imagem corporativa personalizada para o Centro de Software foi introduzida no Configuration Manager versão 1602. Na versão de pré-visualização técnica 1607, essa imagem corporativa agora os todas as caixas de diálogo associados e notificações de barra de tarefas para fornecer uma experiência mais consistente aos utilizadores do Centro de Software.

### <a name="try-it-out"></a>Experimente!

Imagem corporativa personalizada para o Centro de Software é aplicada, de acordo com as seguintes regras:

1. Se a função de servidor de sites do ponto de Web site do catálogo de aplicações não está instalada, em seguida, o Centro de Software apresentará o nome da organização especificado no **agente do computador** definição de cliente **nome da organização apresentada no Centro de Software**. Para obter instruções, consulte o artigo [como configurar as definições de cliente](../../core/clients/deploy/configure-client-settings.md).

2. Se a função de servidor de sites do ponto de Web site do catálogo de aplicações é instalada, em seguida, o Centro de Software apresentará o nome da organização e a cor especificado nas propriedades de função de servidor de site do catálogo de aplicações Web site ponto. Para obter mais informações, consulte o artigo [opções de configuração de ponto de Web site do catálogo de aplicações](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

3. Se uma subscrição do Microsoft Intune é configurada e ligada ao ambiente do Configuration Manager, em seguida, o Centro de Software apresentará o nome da organização, cor e a empresa logótipo especificado nas propriedades de subscrição do Intune. Para obter mais informações, consulte o artigo [configurar a subscrição do Microsoft Intune](/mdm/deploy-use/configure-intune-subscription).

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>Implementações iniciadas por utilizar o mesmo adaptador de rede para vários PXE
Na versão de pré-visualização técnica 1607, ao utilizar uma placa ethernet para a imagem de vários dispositivos (por exemplo, um adaptador USB ethernet que utiliza em vários dispositivos), pode ativar uma nova definição que permite-lhe introduzir identificadores de hardware para os adaptadores ethernet. Gestor de configuração ignora os identificadores de hardware na lista ao efetuar uma instalação de PXE e para o registo de cliente.

Para mais informações sobre este problema, consulte o [blogue de equipa de suporte do Configuration Manager OSD](https://blogs.technet.microsoft.com/system_center_configuration_manager_operating_system_deployment_support_blog/2015/08/27/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in-system-center-configuration-manger-osd/).  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>Ativar a funcionalidade Gerir os identificadores de hardware duplicados  
1. Na consola do Configuration Manager, aceda a **administração** > **descrição geral** > **serviços em nuvem** > **atualizações e a manutenção** > **funcionalidades**.
2. No painel de visualização, selecione **identificadores de hardware duplicados gerir**.
3. No **base** separador o **funcionalidades** grupo, clique em **ativar**.

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Adicionar identificadores de hardware para o Configuration Manager para ignorar  
1. Na consola do Configuration Manager, aceda a **administração** > **descrição geral** > **configuração do Site** > **Sites**.
2. No separador **Home Page** , no grupo **Sites** , clique em **Definições de Hierarquia**.
3. Aceda ao **aprovação do cliente e registos em conflito** separador.
4. Clique em **adicionar** no **duplicar identificadores de hardware** secção para adicionar os identificadores de hardware novo.


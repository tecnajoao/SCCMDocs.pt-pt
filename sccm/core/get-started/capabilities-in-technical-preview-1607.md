---
title: Funcionalidades no Technical Preview 1607
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1607.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: b3fb33191f8ae5a33876603e1a3d94ee2ac80860
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896571"
---
# <a name="capabilities-in-technical-preview-1607-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1607 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1607. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.    


**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

## <a name="dmp_edition"></a>Política de atualização de melhorias para a edição Windows 10

Nesta versão, foram efetuadas as seguintes melhorias para esta política:

* Agora, pode utilizar a política de atualização de edição com PCs Windows 10 que execute o Gestor de configuração de cliente para além dos Windows 10 PCs inscritos com o Microsoft Intune.
* Pode atualizar do Windows 10 Professional para qualquer uma das plataformas no assistente que são compatíveis com seu hardware.

[Leia mais sobre a política de atualização de edição do Windows 10](/sccm/compliance/deploy-use/upgrade-windows-version)

### <a name="try-it-out"></a>Experimente!

1. Utilize as informações no [tópico de política de atualização de edição existente](/sccm/compliance/deploy-use/upgrade-windows-version) para criar uma política de atualização de edição.
2. Aplicar esta política para PCs Windows 10 com o cliente do Configuration Manager.
Assim que a política atingir um PC Windows de destino, o PC será reiniciado dentro de duas horas para aplicar a atualização. Atualmente não pode suprimir este reinício. Certifique-se de informar os utilizadores nos quais implementou a política ou agendar a política para executar os usuários fora do horário de trabalho.

### <a name="known-issue-with-this-release"></a>Problema conhecido com esta versão
Nas definições de cliente do Configuration Manager, poderá ver as definições para **atualização de edição**. Nesta versão, estas definições não estão funcionais. Utilize as instruções acima indicadas para atualizar o Windows 10 para uma versão mais recente.

## <a name="customizable-branding-for-software-center-dialogs"></a>Imagem Corporativa Personalizável para Caixas de Diálogo do Centro de Software

Imagem corporativa personalizada para o Centro de Software foi introduzida no Configuration Manager versão 1602. Na versão de pré-visualização técnica 1607, essa imagem corporativa abranger agora todas as caixas de diálogo associada e notificações da barra de tarefas para fornecer uma experiência mais consistente aos utilizadores do Centro de Software.

### <a name="try-it-out"></a>Experimente!

Imagem corporativa personalizada para o Centro de Software é aplicada, de acordo com as seguintes regras:

1. Se a função de servidor de sites do ponto de Web site do catálogo de aplicações não está instalada, o Centro de Software apresentará o nome da organização especificado na **agente do computador** definição do cliente **nome da organização apresentada no Centro de software**. Para obter instruções, consulte [como configurar as definições de cliente](../../core/clients/deploy/configure-client-settings.md).

2. Se a função de servidor de sites do ponto de Web site do catálogo de aplicações estiver instalada, em seguida, o Centro de Software apresentará o nome da organização e a cor especificados nas propriedades de função do servidor de ponto de site catálogo de aplicações Web site. Para obter mais informações, consulte [opções de configuração do ponto de Web sites do catálogo de aplicações](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

3. Se uma subscrição do Microsoft Intune é configurada e ligada ao ambiente do Configuration Manager, em seguida, o Centro de Software apresentará o nome da organização, o logótipo de cor e da empresa especificados nas propriedades de subscrição do Intune. Para obter mais informações, consulte [configurar a subscrição do Microsoft Intune](/mdm/deploy-use/configure-intune-subscription).

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>Implementações iniciadas por utilizar o mesmo adaptador de rede para vários PXE
Na versão de pré-visualização técnica 1607, quando utiliza um adaptador de ethernet para vários dispositivos (por exemplo, um adaptador de ethernet USB que utilizar em vários dispositivos) de imagem, pode ativar uma nova definição que permite-lhe introduzir identificadores de hardware para os adaptadores de ethernet. Gestor de configuração ignora os identificadores de hardware na lista ao efetuar uma instalação de PXE e para o registo de cliente.

Para obter mais informações sobre este problema, consulte a [blogue da equipa do suporte do Configuration Manager OSD](https://blogs.technet.microsoft.com/system_center_configuration_manager_operating_system_deployment_support_blog/2015/08/27/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in-system-center-configuration-manger-osd/).  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>Ativar a funcionalidade Gerir os identificadores de hardware duplicados  
1. Na consola do Configuration Manager, aceda a **Administration** > **descrição geral** > **serviços Cloud**  >  **Atualizações e manutenção** > **funcionalidades**.
2. No painel de visualização, selecione **identificadores de hardware duplicados gerir**.
3. Sobre o **home page** separador o **funcionalidades** , clique em **ativar**.

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Adicionar identificadores de hardware para o Configuration Manager para ignorar  
1. Na consola do Configuration Manager, aceda a **Administration** > **descrição geral** > **configuração do Site**  >  **Sites**.
2. No separador **Home Page** , no grupo **Sites** , clique em **Definições de Hierarquia**.
3. Vá para o **aprovação do cliente e registos em conflito** separador.
4. Clique em **Add** no **duplicar identificadores de hardware** secção para adicionar novos identificadores de hardware.

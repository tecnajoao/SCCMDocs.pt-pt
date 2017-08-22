---
title: "Atualizar dispositivos Windows para uma versão diferente com o Configuration Manager | Microsoft Docs"
description: "Atualize automaticamente os dispositivos que executem o ambiente de trabalho do Windows 10, Windows 10 Mobile ou Windows 10 Holographic para uma edição diferente com o Configuration Manager."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: cd8c644d07dab0010dc211df8ce4f2dc6e1fa7ae
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>Atualizar dispositivos Windows com a política de atualização de edição no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


O System Center Configuration Manager **política de atualização de edição** permite-lhe atualizar automaticamente os dispositivos que executam uma das seguintes versões do Windows 10 para uma edição diferente:

- Windows 10 Desktop
- Windows 10 Mobile
<!-- - Windows 10 Holographic -->

São suportados os seguintes caminhos de atualização:

- A partir do Windows 10 Pro para Windows 10 Enterprise
- Na home page do Windows 10 para Windows 10 Education
- Do Windows 10 Mobile para Windows 10 Enterprise móveis
<!-- - From Windows 10 Holographic Pro to Windows 10 Holographic Enterprise -->

Os dispositivos tem de ser inscritos no Microsoft Intune ou executar o software de cliente do Configuration Manager. Esta política não é atualmente compatível com computadores que são geridos pela MDM no local.

## <a name="before-you-start"></a>Antes de começar  
 Antes de começar a atualizar dispositivos para a versão mais recente, irá necessitar de um dos seguintes:  

-   Uma chave de produto válida para instalar a nova versão do Windows em todos os dispositivos de destino com a política (para sistemas operativos de ambiente de trabalho)  

-   Um ficheiro de licenciamento da Microsoft que contém as informações de licenciamento para instalar a nova versão do Windows em todos os dispositivos de destino com a política (para Windows 10 Mobile<!-- and Windows 10 Holographic-->).

- Para criar e implementar este tipo de política, deve foi atribuído o Gestor de configuração **administrador total** função de segurança.

## <a name="configure-the-edition-upgrade-policy"></a>Configurar a política de atualização de edição  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **as definições de compatibilidade** > **atualização de edição do Windows 10**.  

3.  No separador **Início** , no grupo **Criar** , clique em **Criar Política de Atualização de Edição**.  

4.  Clique em **Criar Política**.  

5.  Na página **Geral** do **Assistente para Criar Política de Atualização de Edição**, especifique as seguintes informações:  

    -   **Nome** - introduza um nome para a política de atualização de edição.  

    -   **Descrição** (opcional) - opcionalmente, introduza uma descrição para a política que o ajude a identificá-la na consola do Intune.  

    -   **SKU para atualizar dispositivo para** – na lista pendente, selecione a versão do Windows 10 Desktop, <!-- Windows 10 Holographic,--> ou Windows 10 Mobile que pretende atualizar os dispositivos visados.  

    -   **Informações de licenciamento** - selecione um dos seguintes:  

        -   **Chave de Produto** - introduza uma chave de produto válida do Windows 10 que será utilizada para atualizar os dispositivos de destino com sistemas operativos do Windows 10 Desktop.  

            > [!NOTE]  
            >  Depois de criar uma política que contém uma chave de produto, já não será possível editar a chave de produto. Isto deve-se ao facto de a chave ficar obscurecida por razões de segurança. Para alterar a chave de produto, tem de introduzir novamente a chave completa.  

        -   **Ficheiro de licenciamento** -clique em **procurar** para selecionar um ficheiro de licenciamento válido no formato XML que será utilizado para atualizar os dispositivos de destino que executam <!--Windows 10 Holographic and -->sistemas de operativos do Windows 10 Mobile.  

6.  Conclua o assistente.  

A nova política é apresentada no nó **Atualização de Edição do Windows 10** da área de trabalho **Ativos e Compatibilidade** .  

## <a name="deploy-the-edition-upgrade-policy"></a>Implementar a política de atualização de edição  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **as definições de compatibilidade** > **atualização de edição do Windows 10**.  

3.  Selecione a política de atualização de edição do Windows 10 que pretende implementar e, em seguida, no separador **Início** no grupo **Implementação** , clique em **Implementar**.  

4.  No **implementar o Windows 10 de atualização de edição** diálogo caixa, selecione a coleção à qual pretende implementar a política e o agendamento através do qual a política será avaliada e, em seguida, clique em **OK**. Para PCs geridos com o cliente do Configuration Manager, tem de implementar a política para uma coleção de dispositivos. Para PCs que estão inscritos no Intune, pode implementar a política a um utilizador ou uma coleção de dispositivos. 



## <a name="next-steps"></a>Passos seguintes

Ao monitorizar a implementação que acabou de criar o **implementações** o nó do **monitorização** área de trabalho, poderá ver erros que possam indicar a implementação foi bem-sucedido, como:
- **Não aplicável a este dispositivo**
- **Falha na conversão do tipo de dados**

Estes erros não significam que falhou a implementação. Certifique-se no PC de destino que a atualização efetuada com êxito.

Depois da política atinge um PC Windows de destino e é avaliada, este será reiniciado dentro de duas horas para aplicar a atualização. Certifique-se de informar os utilizadores nos quais implementou a política ou agendar a política a executar os utilizadores fora do horário de trabalho.

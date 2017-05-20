---
title: "Atualizar dispositivos Windows para uma versão diferente com o Configuration Manager | Documentos do Microsoft"
description: "Atualize automaticamente os dispositivos que executem o ambiente de trabalho do Windows 10, Windows 10 Mobile ou o Windows 10 Holographic para uma edição diferente com o Configuration Manager."
ms.custom: na
ms.date: 04/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
caps.latest.revision: 8
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 4eee9731a4a27328c47c0d15931cab28cf520a18
ms.openlocfilehash: cfde0a43947013bbd3a1093688cee19fe309fd03
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---

# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>Atualizar dispositivos Windows com a política de atualização de edição no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


O System Center Configuration Manager **edição atualizar política** permite-lhe automaticamente atualização dispositivos que executam uma das seguintes versões do Windows 10 para uma edição diferente:

- Windows 10 Desktop
- Windows 10 Mobile
- Windows 10 Holographic

Os seguintes caminhos de atualização são suportados:

- A partir do Windows 10 Pro para o Windows 10 Enterprise
- A partir da home page do Windows 10 para educação Windows 10
- A partir do Windows 10 Mobile para Windows 10 Enterprise móveis
- A partir do Windows 10 Holographic Pro para o Windows 10 Holographic Enterprise

Os dispositivos têm de ser inscrito no Microsoft Intune ou executar o software de cliente do Configuration Manager. Esta política não é atualmente compatível com PCs que são geridos pela MDM no local.

## <a name="before-you-start"></a>Antes de começar  
 Antes de começar a atualizar dispositivos para a versão mais recente, irá necessitar de um dos seguintes:  

-   Uma chave de produto válida para instalar a nova versão do Windows em todos os dispositivos de destino com a política (para sistemas operativos de ambiente de trabalho)  

-   Um ficheiro de licenciamento da Microsoft que contém as informações de licenciamento para instalar a nova versão do Windows em todos os dispositivos de destino com a política (para Windows 10 Mobile e Windows 10 Holographic).

- Para criar e implementar este tipo de política, que tem sido atribuiu o Configuration Manager **administrador total** função de segurança.

## <a name="configure-the-edition-upgrade-policy"></a>Configurar a política de atualização de edição  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **atualizar de edição do Windows 10**.  

3.  No separador **Início** , no grupo **Criar** , clique em **Criar Política de Atualização de Edição**.  

4.  Clique em **Criar Política**.  

5.  Na página **Geral** do **Assistente para Criar Política de Atualização de Edição**, especifique as seguintes informações:  

    -   **Nome** - introduza um nome para a política de atualização de edição.  

    -   **Descrição** (opcional) - opcionalmente, introduza uma descrição para a política que o ajude a identificá-la na consola do Intune.  

    -   **SKU para atualizar dispositivo para** – na lista pendente, selecione a versão do Windows 10 Desktop, do Windows 10 Holographic ou do Windows 10 Mobile para a qual pretende atualizar os dispositivos de destino.  

    -   **Informações de licenciamento** - selecione um dos seguintes:  

        -   **Chave de Produto** - introduza uma chave de produto válida do Windows 10 que será utilizada para atualizar os dispositivos de destino com sistemas operativos do Windows 10 Desktop.  

            > [!NOTE]  
            >  Depois de criar uma política que contém uma chave de produto, já não será possível editar a chave de produto. Isto deve-se ao facto de a chave ficar obscurecida por razões de segurança. Para alterar a chave de produto, tem de introduzir novamente a chave completa.  

        -   **Ficheiro de Licenciamento** - clique em **Procurar** para selecionar um ficheiro de licenciamento válido no formato XML que será utilizado para atualizar os dispositivos de destino com sistemas operativos do Windows 10 Holographic e do Windows 10 Mobile.  

6.  Conclua o assistente.  

A nova política é apresentada no nó **Atualização de Edição do Windows 10** da área de trabalho **Ativos e Compatibilidade** .  

## <a name="deploy-the-edition-upgrade-policy"></a>Implementar a política de atualização de edição  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **atualizar de edição do Windows 10**.  

3.  Selecione a política de atualização de edição do Windows 10 que pretende implementar e, em seguida, no separador **Início** no grupo **Implementação** , clique em **Implementar**.  

4.  No **implementar o Windows 10 edição atualizar** diálogo caixa, selecione a coleção à qual pretende implementar a política e a agenda pela qual a política será avaliada e, em seguida, clique em **OK**. Para PCs que são geridos com o cliente do Configuration Manager, tem de implementar a política para uma coleção de dispositivos. Para PCs que estão inscritos com o Intune, pode implementar a política para uma coleção de dispositivos ou utilizadores. 

É possível monitorizar a implementação que acabou de criar através do nó **Implementações** da área de trabalho **Monitorização** .  

 Depois da política de atinge um PC com Windows visado e é avaliada, será reiniciada no prazo de duas horas para aplicar a atualização. Certifique-se informar os utilizadores para os quais implementar a política, ou agendar a política para executar os utilizadores fora do horário de trabalho.


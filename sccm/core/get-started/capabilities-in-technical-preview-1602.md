---
title: Funcionalidades no Technical Preview 1602
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1602."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
caps.latest.revision: "6"
author: erikje
ms.author: erikje
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: 7771a57323857fa47688d98af499389194972000
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="capabilities-in-technical-preview-1602-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1602 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1602. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja o tópico introdutórias, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.  

 Seguem-se novas funcionalidades que pode experimentar com esta versão.  

##  <a name="BKMK_MDM"></a>Melhorias na gestão de dispositivos móveis  

### <a name="ios-activation-lock"></a>Bloqueio de ativação de iOS  
 O System Center Configuration Manager pode ajudá-lo a gerir o Bloqueio de Ativação do iOS, uma funcionalidade da aplicação Encontrar iPhone para iOS 7.1 e dispositivos posteriores. O Bloqueio de Ativação é ativado automaticamente ao utilizar a aplicação Encontrar o Meu iPhone num dispositivo. Depois de estar ativado, o Apple ID e a palavra-passe do utilizador têm de ser introduzidos primeiro para que qualquer pessoa possa:  

-   Desativar a aplicação Encontrar o Meu iPhone  

-   Apagar o dispositivo  

-   Reativar o dispositivo  

 O Configuration Manager pode pedir o estado de bloqueio de ativação de dispositivos supervisionados e não supervisionados que executam o iOS 7.1 e posterior. Para dispositivos supervisionados, o Intune pode obter o código de desativação do Bloqueio de Ativação e enviá-lo diretamente para o dispositivo.  

 Para obter mais informações, consulte [ajudar a proteger dispositivos iOS com o bloqueio de ativação desativando para o Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock)  

##  <a name="BKMK_SC1601"></a>Melhoramentos ao centro de Software na versão 1602  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Atualizar a política de computador e utilizador de PC do Centro de Software  
 Uma nova opção **sincronizar política** foi adicionado para o **opções** > **manutenção do computador** página do Centro de Software que faz com que o PC Atualize o Gestor de configuração de política de computador e utilizador.  

##  <a name="BKMK_Win10Servicing"></a>Melhoramentos à manutenção do Windows 10  
 Na versão 1602 Technical Preview, foram adicionados os seguintes melhoramentos para a manutenção do Windows 10:  

-   Novas opções de filtro para planos de manutenção.  Agora, pode filtrar para **idioma**, **necessário**, e **título**. Apenas as atualizações que cumprem os critérios especificados serão adicionadas à implementação associada.  

-   Quando seleciona o **atualizações** sincronização de atualizações de classificação de recursos de software, é apresentada uma caixa de diálogo de aviso para informá-lo nesse WSUS [correção 3095113](https://support.microsoft.com/kb/3095113) é necessário para sincronizar as atualizações de software com êxito e para a manutenção do Windows 10 funcionar corretamente.  Na caixa de diálogo, pode ir para o artigo da base de dados de conhecimento para a correção.  

-   Windows 10 disponíveis agora, as atualizações apenas são apresentadas no **manutenção do Windows 10** \ **todas as atualizações do Windows 10** nós da consola do Configuration Manager. Estas atualizações já não aparecem no **atualizações de Software** \ **todas as atualizações de Software** nós.  

-   Os utilizadores finais que iniciam um pacote de atualização do Windows 10 serão apresentados uma caixa de diálogo que permite-lhes saber que actualizará o sistema operativo.  

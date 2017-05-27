---
title: "Capacidades na pré-visualização técnica 1602 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1602."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 2354f885aaf69683004ad78f0e1978e78fee9145
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1602-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1602 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1602. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.  

 Seguem-se novas funcionalidades que pode experimentar com esta versão.  

##  <a name="BKMK_MDM"></a>Melhorias na gestão de dispositivos móveis  

### <a name="ios-activation-lock"></a>iOS bloqueio de ativação  
 O System Center Configuration Manager pode ajudá-lo a gerir o Bloqueio de Ativação do iOS, uma funcionalidade da aplicação Encontrar iPhone para iOS 7.1 e dispositivos posteriores. O Bloqueio de Ativação é ativado automaticamente ao utilizar a aplicação Encontrar o Meu iPhone num dispositivo. Depois de estar ativado, o Apple ID e a palavra-passe do utilizador têm de ser introduzidos primeiro para que qualquer pessoa possa:  

-   Desativar a aplicação Encontrar o Meu iPhone  

-   Apagar o dispositivo  

-   Reativar o dispositivo  

 O Configuration Manager podem pedir o estado de bloqueio de ativação dos supervisionado e unsupervised dispositivos que executam o iOS 7.1 e posterior. Para dispositivos supervisionados, o Intune pode obter o código de desativação do Bloqueio de Ativação e enviá-lo diretamente para o dispositivo.  

 Para obter mais detalhes, consulte o artigo [ajudar a proteger os dispositivos com o bloqueio de ativação ignorar para o Configuration Manager de iOS](/sccm/mdm/deploy-use/manage-ios-activation-lock)  

##  <a name="BKMK_SC1601"></a>Melhorias efetuadas ao centro de Software na versão 1602  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Atualizar PC política de computador e utilizador a partir do Centro de Software  
 Uma nova opção **política de sincronização** foi adicionado à **opções** > **manutenção do computador** página do Centro de Software que faz com que o PC para atualizar Gestor de configuração. é a política de computador e utilizador.  

##  <a name="BKMK_Win10Servicing"></a>Melhorias na manutenção do Windows 10  
 A pré-visualização técnica do 1602 adicionámos os seguintes melhoramentos para a manutenção do Windows 10:  

-   Novas opções de filtro para planos de manutenção.  Agora pode filtrar por **idioma**, **necessário**, e **título**. Apenas as atualizações que cumprem os critérios especificados serão adicionadas à implementação associada.  

-   Quando seleciona o **atualizações** sincronização de atualizações de classificação de software, é apresentada uma caixa de diálogo de aviso para informá-lo desse WSUS [correção 3095113](https://support.microsoft.com/kb/3095113) é necessário para sincronizar com êxito atualizações de software e para a manutenção de 10 de Windows funcionem corretamente.  A partir da caixa de diálogo, pode ir para o artigo da base de dados de conhecimento para a correção.  

-   Disponível Windows 10 agora atualiza apenas visualização no **manutenção do Windows 10** \ **todas as atualizações do Windows 10** nó da consola do Configuration Manager. Estas atualizações já não aparecerá no **atualizações de Software** \ **todas as atualizações de Software** nó.  

-   Os utilizadores finais que inicie um pacote de atualização do Windows 10 ser á uma caixa de diálogo que lhe permita saber que actualizará o sistema operativo.  


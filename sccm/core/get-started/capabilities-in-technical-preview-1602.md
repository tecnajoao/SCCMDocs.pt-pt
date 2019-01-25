---
title: Funcionalidades no Technical Preview 1602
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1602.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ff8ad1debf053c75d5c62f8a12169060ddcead85
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898465"
---
# <a name="capabilities-in-technical-preview-1602-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1602 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1602. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.  

 Seguem-se os novos recursos, que pode experimentar com esta versão.  

##  <a name="BKMK_MDM"></a> Melhorias na gestão de dispositivos móveis  

### <a name="ios-activation-lock"></a>Bloqueio de ativação do iOS  
 O System Center Configuration Manager pode ajudá-lo a gerir o Bloqueio de Ativação do iOS, uma funcionalidade da aplicação Encontrar iPhone para iOS 7.1 e dispositivos posteriores. O Bloqueio de Ativação é ativado automaticamente ao utilizar a aplicação Encontrar o Meu iPhone num dispositivo. Depois de estar ativado, o Apple ID e a palavra-passe do utilizador têm de ser introduzidos primeiro para que qualquer pessoa possa:  

- Desativar a aplicação Encontrar o Meu iPhone  

- Apagar o dispositivo  

- Reativar o dispositivo  

  O Configuration Manager pode pedir o estado de bloqueio de ativação de dispositivos supervisionados e não supervisionados que executam o iOS 7.1 e posterior. Para dispositivos supervisionados, o Intune pode obter o código de desativação do Bloqueio de Ativação e enviá-lo diretamente para o dispositivo.  

  Para obter detalhes, consulte [ajudar a proteger dispositivos iOS com o bloqueio de ativação desativando o para o Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock)  

##  <a name="BKMK_SC1601"></a> Melhoramentos ao centro de Software na versão 1602  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Atualizar a política de computador e utilizador de PC do Centro de Software  
 Uma nova opção **política de sincronização** foi adicionada à **opções** > **manutenção do computador** página do Centro de Software que faz com que o PC para atualizá-la do Política de computador e utilizador do Configuration Manager.  

##  <a name="BKMK_Win10Servicing"></a> Melhoramentos à manutenção do Windows 10  
 No 1602 Technical Preview, foram adicionados os seguintes melhoramentos para a manutenção do Windows 10:  

-   Novas opções de filtro para planos de manutenção.  Agora pode filtrar por **linguagem**, **necessário**, e **Title**. Apenas as atualizações que cumprem os critérios especificados serão adicionadas à implementação associada.  

-   Quando seleciona a **atualizações** sincronização de atualizações de classificação de software, uma caixa de diálogo de aviso é apresentada a informá-lo que WSUS [correção 3095113](https://support.microsoft.com/kb/3095113) é necessário para sincronizar com êxito atualizações de software e para a manutenção do Windows 10 funcionar corretamente.  Na caixa de diálogo, pode aceder ao artigo da base de dados de conhecimento para a correção.  

-   Windows 10 disponíveis agora, as atualizações apenas são apresentadas no **manutenção do Windows 10** \ **todas as atualizações do Windows 10** nó da consola do Configuration Manager. Estas atualizações já não aparecem no **atualizações de Software** \ **todas as atualizações de Software** nó.  

-   Serão solicitados aos utilizadores finais que iniciam um pacote de atualização do Windows 10 com uma caixa de diálogo que permite-lhes saber que vão atualizar o sistema operativo.  

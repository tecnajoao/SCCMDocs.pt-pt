---
title: "Atualizar as instalações de avaliação | Documentos do Microsoft"
description: "Saiba como atualizar uma instalação de avaliação para uma instalação completa do System Center Configuration Manager."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: d1bf0fdc3e735eb31492476fd46f008620150c0b
ms.openlocfilehash: 8f951805c2fc25059965c15c94934c0f8546735c
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="upgrade-an-evaluation-installation-of-system-center-configuration-manager-to-a-full-installation"></a>Atualizar uma instalação de avaliação do System Center Configuration Manager para uma instalação completa

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Se tiver instalado o System Center Configuration Manager como uma versão de avaliação, após o prazo de 180 dias, a consola do Configuration Manager torna-se só de leitura até ativar o produto a partir de **manutenção do Site** página no programa de configuração. Em qualquer altura antes ou depois do período de 180 dias, tem a opção para atualizar uma instalação de avaliação para uma instalação completa.  

> [!NOTE]  
>  Quando liga uma consola do Configuration Manager para uma instalação de avaliação do Configuration Manager, na barra de título da consola apresenta o número de dias remanescentes até que a instalação de avaliação expire. O número de dias não é automaticamente atualizado e apenas são atualizados quando fizer uma nova ligação a um site.  

 Pode atualizar os seguintes sites que executarem uma instalação de avaliação:  

-   Site de administração central  
-   Site primário  

Dado que os sites secundários não são processados como instalações de avaliação, não será necessário modificar um site secundário após o respetivo site primário principal ser atualizado para uma instalação completa.  

Pré-requisitos para atualizar uma versão de avaliação para uma versão licenciada:  

-   Tem de ter um produto válida a utilizar durante a atualização.  
-   A conta tem de ter **administrador** direitos no computador onde a instalação do site.  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>Para atualizar uma versão de avaliação do Configuration Manager para uma versão licenciada  

1.  No servidor do site, execute **Setup.exe** (programa de configuração do Configuration Manager) da pasta de instalação do Configuration Manager (**%path%\BIN\X64**). Tem de executar a cópia do programa de configuração que esteja localizada no servidor do site na pasta Configuration Manager, porque as opções de manutenção do site não estão disponíveis quando executa a configuração a partir do suporte de instalação.  
2.  No **antes de começar** página, selecione **seguinte**.  
3.  No **introdução** página, selecione **executar a manutenção do site ou repor este Site**e, em seguida, selecione **seguinte**.  
4.  No **manutenção do Site** página, selecione **atualizar a edição de avaliação para uma edição licenciada**, introduza uma chave de produto válida e, em seguida, selecione **seguinte**.  
5.  No **termos de licenciamento de Software Microsoft** página, leia e aceite os termos de licença e, em seguida, selecione **seguinte**.  
6.  No **configuração** página, selecione **fechar** para concluir o assistente.  

    > [!NOTE]  
    >  Na barra de título de uma consola do Configuration Manager que permanece ligada ao site a atualizar pode indicar que o site ainda é uma versão de avaliação até voltar a ligar a consola ao site.  


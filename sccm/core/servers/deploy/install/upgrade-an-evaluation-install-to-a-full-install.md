---
title: Instalação de avaliação de atualização
titleSuffix: Configuration Manager
description: Saiba como atualizar uma instalação de avaliação para uma instalação completa do System Center Configuration Manager.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b1bbce9f3ca7a1a6cf9c199677b33e34d9be109c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32335920"
---
# <a name="upgrade-an-evaluation-installation-of-system-center-configuration-manager-to-a-full-installation"></a>Atualizar uma instalação de avaliação do System Center Configuration Manager para uma instalação completa

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Se tiver instalado o System Center Configuration Manager como uma versão de avaliação, após o prazo de 180 dias, a consola do Configuration Manager torna-se só de leitura até ativar o produto do **manutenção do Site** página na configuração. Em qualquer altura antes ou após o período de 180 dias, terá a opção para atualizar uma instalação de avaliação para uma instalação completa.  

> [!NOTE]  
>  Quando ligar uma consola do Configuration Manager para uma instalação de avaliação do Configuration Manager, na barra de título da consola mostra o número de dias remanescentes até que a instalação de avaliação expire. O número de dias não é automaticamente atualizado e apenas atualizações quando efetuar uma nova ligação a um site.  

 Pode atualizar os sites seguintes que executam uma instalação de avaliação:  

-   Site de administração central  
-   Site primário  

Porque os sites secundários não são processados como instalações de avaliação, não terá de modificar um site secundário após a atualização do site primário principal para uma instalação completa.  

Pré-requisitos para atualizar uma versão de avaliação para uma versão licenciada:  

-   Tem de ter um produto válido para utilizar durante a atualização.  
-   A conta tem de ter **administrador** direitos no computador onde a instalação do site.  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>Para atualizar uma versão de avaliação do Configuration Manager para uma versão licenciada  

1.  No servidor do site, execute **Setup.exe** (configuração do Configuration Manager) da pasta de instalação do Configuration Manager (**%path%\BIN\X64**). Tem de executar a cópia do programa de configuração que está localizado no servidor do site na pasta Configuration Manager, porque as opções de manutenção do site não estão disponíveis quando executa a configuração do suporte de dados de instalação.  
2.  No **antes de começar** página, selecione **seguinte**.  
3.  No **introdução** página, selecione **executar a manutenção do site ou repor o Site**e, em seguida, selecione **seguinte**.  
4.  No **manutenção do Site** página, selecione **atualizar a edição de avaliação para uma edição licenciada**, introduza uma chave de produto válida e, em seguida, selecione **seguinte**.  
5.  No **termos de licenciamento de Software Microsoft** página, leia e aceite os termos de licenciamento e, em seguida, selecione **seguinte**.  
6.  No **configuração** página, selecione **fechar** para concluir o assistente.  

    > [!NOTE]  
    >  A barra de título da consola do Configuration Manager que permanecem ligada ao site que atualizar pode indicar que o site ainda é uma versão de avaliação até voltar a ligar a consola ao site.  

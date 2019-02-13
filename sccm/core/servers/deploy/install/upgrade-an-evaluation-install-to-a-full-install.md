---
title: Instalações de avaliação de atualização
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
ms.collection: M365-identity-device-management
ms.openlocfilehash: f9cb58d1a697cd26bfefc8081d8705f09e818194
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128920"
---
# <a name="upgrade-an-evaluation-installation-of-system-center-configuration-manager-to-a-full-installation"></a>Atualizar uma instalação de avaliação do System Center Configuration Manager para uma instalação completa

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Se tiver instalado o System Center Configuration Manager como uma versão de avaliação, após 180 dias, a consola do Configuration Manager torna-se só de leitura enquanto não for ativado o produto a partir da **manutenção do Site** página no programa de configuração. Em qualquer altura antes ou após o período de 180 dias, tem a opção para atualizar uma instalação de avaliação para uma instalação completa.  

> [!NOTE]  
>  Quando se liga uma consola do Configuration Manager para uma instalação de avaliação do Configuration Manager, a barra de título da consola mostra o número de dias remanescentes até que a instalação de avaliação expire. O número de dias não é automaticamente atualizado e apenas atualiza quando fizer uma nova ligação a um site.  

 Pode atualizar os seguintes sites que executam uma instalação de avaliação:  

-   Site de administração central  
-   Site primário  

Uma vez que os sites secundários não são tratados como instalações de avaliação, não é necessário modificar um site secundário após a atualização do site primário principal para uma instalação completa.  

Pré-requisitos para atualizar uma versão de avaliação para uma versão licenciada:  

-   Tem de ter um produto válido para utilizar durante a atualização.  
-   Sua conta tem de ter **administrador** direitos no computador em que a instalação do site.  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>Para atualizar uma versão de avaliação do Configuration Manager para uma versão licenciada  

1.  No servidor do site, execute **Setup.exe** (configuração do Configuration Manager) da pasta de instalação do Configuration Manager (**%path%\BIN\X64**). Tem de executar a cópia da configuração que se encontra no servidor do site na pasta Configuration Manager, porque as opções de manutenção do site não estão disponíveis quando executa a configuração da mídia de instalação.  
2.  Sobre o **antes de começar** página, selecione **próxima**.  
3.  Sobre o **introdução** página, selecione **executar a manutenção do site ou repor o Site**e, em seguida, selecione **seguinte**.  
4.  Sobre o **manutenção do Site** página, selecione **atualizar a edição de avaliação para uma edição licenciada**, introduza uma chave de produto válida e, em seguida, selecione **seguinte**.  
5.  Sobre o **termos de licenciamento de Software do Microsoft** página, leia e aceite os termos de licença e, em seguida, selecione **próxima**.  
6.  Sobre o **Configuration** página, selecione **fechar** para concluir o assistente.  

    > [!NOTE]  
    >  A barra de título de uma consola do Configuration Manager que permanece ligada ao site que atualizar pode indicar que o site ainda é uma versão de avaliação até voltar a ligar a consola ao site.  

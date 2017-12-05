---
title: "Gerir implementações de alto risco"
titleSuffix: Configuration Manager
description: "Saiba como configurar as definições do site no System Center Configuration Manager, para o avisar admins se criarem uma implementação de alto risco."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
caps.latest.revision: "6"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 96855503183c1f9a3b51c5861ca661089f3c2994
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="settings-to-manage-high-risk-deployments-for-system-center-configuration-manager"></a>Definições para gerir implementações de alto risco para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Com o System Center Configuration Manager pode configurar as definições do site que irão avisar os administradores se criarem uma implementação de sequência de tarefas de alto risco. Uma implementação de alto risco é:  

-   Uma implementação instalada automaticamente  

-   Tem a probabilidade de causar resultados indesejados  

 Por exemplo, uma sequência de tarefas que tenha um objetivo **necessário** que implementa um sistema operativo é considerada de alto risco.  

 Para reduzir o risco de uma implementação de alto risco indesejada, pode configurar limites de tamanho nestas definições de verificação de implementação:  

-   **Limites de tamanho de coleção**: Oculte coleções com mais clientes que o limite quando cria uma implementação.  

    -   **Tamanho predefinido**: Esta definição oculta coleções, por predefinição, com mais clientes que o limite quando cria uma implementação. Pode ainda ver estas coleções quando criar a implementação, mas estas estão ocultadas por predefinição. O valor predefinido é 100. Introduza um valor de 0 para ignorar esta definição.  

    -   **Tamanho máximo**: Esta definição oculta sempre coleções com mais clientes que o limite quando cria uma implementação. O valor predefinido é 0, o qual ignora esta definição. O valor **Tamanho máximo** tem de ser superior ao valor **Tamanho predefinido** .  

     Por exemplo, definir **tamanho predefinido** a 100 e o **tamanho máximo** a 1000. Quando cria uma implementação de alto risco, a **selecionar coleção** janela só apresentará as coleções que contenham menos de 100 clientes. Se desmarcar a **ocultar coleções com um membro contagem maiores que o siteâ€™ configuração de tamanho mínimo de s** definição, a janela apresentará as coleções que contenham menos de 1 000 clientes.  

-   **Coleções com servidores de sistema de sites**: Bloquear implementações ou exigir verificação antes da criação da implementação, quando a coleção de destino contém um computador com uma função de sistema de sites. Quando uma implementação é bloqueada, tem de selecionar uma coleção diferente que cumpra os critérios de verificação de implementação.  

> [!NOTE]  
>  As implementações de alto risco são sempre limitadas a coleções personalizadas, coleções criadas por si e a coleção incorporada **Computadores Desconhecidos** . Quando cria uma implementação de alto risco, não é possível selecionar uma coleção incorporada como **Todos os Sistemas**.  

### <a name="to-configure-deployment-verification-for-a-site"></a>Para configurar a verificação de implementação para um site  

1.  Na consola do Configuration Manager, escolha **administração** >**configuração do Site** > **Sites**e, em seguida, selecione o site primário a configurar.  

2.  No **home page** separador o **propriedades** grupo, escolha **propriedades**e, em seguida, escolha o **verificação de implementação** separador.  

3.  Depois de definir as configurações que pretende utilizar, escolha **OK** para guardar a configuração.  

### <a name="see-also"></a>Consulte também  
 [Configurar sites e hierarquias do System Center Configuration Manager](../../core/servers/deploy/configure/configure-sites-and-hierarchies.md)

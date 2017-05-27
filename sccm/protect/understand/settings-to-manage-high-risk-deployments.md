---
title: "Gerir implementações de alto risco | Documentos do Microsoft"
description: "Saiba como configurar definições do site no System Center Configuration Manager, para o avisar os administradores se criam uma implementação de alto risco."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 8b5564f39f07a67a3c9278379ed59ca415603d21
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="settings-to-manage-high-risk-deployments-for-system-center-configuration-manager"></a>Definições para gerir implementações de alto risco para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Com o System Center Configuration Manager pode configurar definições do site que irão avisar os administradores que se criam uma implementação de sequência de tarefas de alto risco. Uma implementação de alto risco é:  

-   Uma implementação instalada automaticamente  

-   Tem a probabilidade de causar resultados indesejados  

 Por exemplo, uma sequência de tarefas que tem um objetivo de **obrigatório** que implementa um sistema operativo é considerada de alto risco.  

 Para reduzir o risco de uma implementação de alto risco indesejado, pode configurar limites de tamanho estas definições de verificação de implementação:  

-   **Limites de tamanho de coleção**: Oculte coleções que contêm mais clientes que o limite ao criar uma implementação.  

    -   **Predefinição de tamanho**: Esta definição oculta coleções, por predefinição, com mais clientes que o limite ao criar uma implementação. Continua a poder ver estas coleções ao criar a implementação, mas eles estão ocultos por predefinição. O valor predefinido é 100. Introduza um valor de 0 para ignorar esta definição.  

    -   **Tamanho máximo**: Esta definição sempre oculta coleções com clientes mais do que o limite ao criar uma implementação. O valor predefinido é 0, o qual ignora esta definição. O valor **Tamanho máximo** tem de ser superior ao valor **Tamanho predefinido** .  

     Por exemplo, definir **predefinido tamanho** a 100 e a **tamanho máximo** a 1000. Quando cria uma implementação de alto risco, o **selecionar coleção** janela só serão apresentadas coleções que contenham menos de 100 clientes. Se desmarcar a **ocultar coleções com um membro contam maiores do que € o siteâ™ configuração de tamanho mínimo de s** definição, a janela será apresentada coleções que contenham menos de 1000 clientes.  

-   **Coleções com servidores do sistema de sites**: Bloquear implementações ou requer verificação antes da criação da implementação, quando a coleção de destino contém um computador com uma função de sistema de sites. Quando uma implementação é bloqueada, tem de selecionar uma coleção diferente que cumpra os critérios de verificação de implementação.  

> [!NOTE]  
>  As implementações de alto risco são sempre limitadas a coleções personalizadas, coleções criadas por si e a coleção incorporada **Computadores Desconhecidos** . Quando cria uma implementação de alto risco, não é possível selecionar uma coleção incorporada como **Todos os Sistemas**.  

### <a name="to-configure-deployment-verification-for-a-site"></a>Para configurar a verificação de implementação para um site  

1.  Na consola do Configuration Manager, escolha **administração** >**configuração do Site** > **Sites**e, em seguida, selecione o site primário a configurar.  

2.  No **base** separador o **propriedades** grupo, selecione **propriedades**e, em seguida, escolha o **verificação de implementação** separador.  

3.  Depois de definir configurações que pretende utilizar, selecione **OK** para guardar a configuração.  

### <a name="see-also"></a>Consulte também  
 [Configurar sites e hierarquias do System Center Configuration Manager](../../core/servers/deploy/configure/configure-sites-and-hierarchies.md)


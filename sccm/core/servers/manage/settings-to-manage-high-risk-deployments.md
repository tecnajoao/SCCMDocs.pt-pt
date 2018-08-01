---
title: Gerir implementações de alto risco
titleSuffix: Configuration Manager
description: Saiba como configurar definições de site de verificação de implementação no Configuration Manager para o avisar os administradores se criarem uma implementação de alto risco.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ab2203b948887a94577826573ccdf3376637eca2
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386879"
---
# <a name="settings-to-manage-high-risk-deployments-for-configuration-manager"></a>Definições para gerir implementações de alto risco para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Com o Configuration Manager, pode configurar definições de site de verificação de implementação. Estas definições avisar os administradores se criarem uma implementação de sequência de tarefas de alto risco. Uma implementação de alto risco é:  

-   Uma implementação que é instalada automaticamente  

-   Tem a probabilidade de causar resultados indesejados  

Por exemplo, uma sequência de tarefas com um objetivo de **necessário** que implemente um sistema operativo é considerada de alto risco.  

Para reduzir o risco de uma implementação de alto risco indesejada, pode configurar limites de tamanho estas definições de verificação de implementação:  

-   **Limites de tamanho de coleção**: Quando cria uma implementação, oculte coleções que incluem a mais clientes que o limite.  

     -   **Tamanho predefinido**: Quando cria uma implementação, esta definição oculta coleções por padrão, que incluem a mais clientes que este limite. Ainda pode ver estas coleções quando criar a implementação, mas eles estão oculta por predefinição. O valor predefinido é **100**. Para ignorar esta definição, introduza um valor de **0**.  

     -   **Tamanho máximo**: Quando cria uma implementação, sempre esta definição oculta coleções com mais clientes que este limite. O valor predefinido é **0**, que ignora esta definição. O valor **Tamanho máximo** tem de ser superior ao valor **Tamanho predefinido** .  

     Por exemplo, defina **tamanho predefinido** para 100 e o **tamanho máximo** a 1000. Quando cria uma implementação de alto risco, o **selecionar coleção** janela apresenta apenas as coleções que incluem menos de 100 clientes. Se desmarcar a definição para **ocultar coleções com um membro contagem superiores à configuração de tamanho mínimo do site**, a janela apresenta as coleções que incluem menos de 1 000 clientes.  

-   **Coleções com servidores de sistema de sites**: Quando a coleção de destino inclui um computador com uma função de sistema de sites, permite bloquear implementações ou exigir verificação antes de criar a implementação. Quando uma implementação é bloqueada, selecione uma coleção diferente que cumpra os critérios de verificação de implementação para continuar a criação da implementação.  

> [!NOTE]  
>  As implementações de alto risco são sempre limitadas a coleções personalizadas, coleções criadas por si e à coleção incorporada **Computadores Desconhecidos** . Quando cria uma implementação de alto risco, não é possível selecionar uma coleção incorporada, como **todos os sistemas**.  

### <a name="configure-deployment-verification-for-a-site"></a>Configurar a verificação de implementação para um site  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**, selecione **Sites**e, em seguida, selecione o site primário a configurar .  

2.  Clique em **propriedades** no Friso e, em seguida, mude para o **verificação de implementação** separador.  

3.  Depois de definir as configurações que pretende utilizar, clique em **OK** para guardar a configuração.  


### <a name="see-also"></a>Consulte também  
 [Configurar sites e hierarquias](/sccm/core/servers/deploy/configure/configure-sites-and-hierarchies)

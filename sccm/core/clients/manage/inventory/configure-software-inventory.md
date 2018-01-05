---
title: "Configurar o inventário de software"
titleSuffix: Configuration Manager
description: "Configurar o inventário de software e excluir pastas do inventário de software no Configuration Manager."
ms.custom: na
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: afddcef2caab6e1af0aacdac91366fa430f21d85
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/04/2018
---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Como configurar inventário de software no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este procedimento configura as predefinições de cliente para inventário de software e aplica-se a todos os computadores na sua hierarquia. Se pretender aplicar estas definições apenas a alguns computadores, crie uma definição de cliente de dispositivo personalizada e atribua-a uma coleção. Para obter mais informações sobre como criar definições personalizadas de dispositivos, consulte [como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).   

## <a name="to-configure-software-inventory"></a>Para configurar o inventário de software  

1.  Na consola do Configuration Manager, escolha **administração** > **as definições de cliente****predefinições de cliente**.  

4.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

5.  No **predefinições** diálogo caixa, escolha **inventário de Software**.  

6.  Na lista **Definições do Dispositivo** , configure os seguintes valores:  

    -   **Ativar inventário de software nos clientes** - na lista pendente, selecione **verdadeiro**.  

    -   **Agendar software ficheiros e inventário coleção agenda** - configura o intervalo no qual os clientes recolhem inventário de software e ficheiros.   

7.  Configure as definições de cliente de que necessita. O [inventário de Software](../../../../core/clients/deploy/about-client-settings.md#software-inventory) secção o [sobre definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) artigo tem uma lista das definições de cliente.  

 Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, veja [Como gerir clientes no System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

 > [!TIP]  
        >   O código de erro 80041006 na inventoryprovider.log significa que o fornecedor WMI de memória esgotada. Ou seja, atingiu o limite de quota de memória para um fornecedor e o fornecedor de inventário não pode continuar.
Neste caso, o agente de inventário cria um relatório com 0 entradas pelo que não existem itens de inventário são reportados. <br/>
Uma solução possíveis para este erro seria reduzir o âmbito da coleção de inventário de software. Em circunstâncias quando ocorrer o erro depois de limitar o âmbito de inventário, aumentando a [MemoryPerHost](https://blogs.technet.microsoft.com/askperf/2008/09/16/memory-and-handle-quotas-in-the-wmi-provider-service/) propriedade definida no [_ProviderHostQuotaConfiguration](https://msdn.microsoft.com/library/aa394671) classe pode fornecer uma solução.

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>Excluir pastas do inventário de software  

1.  Utilizando o Notepad.exe, crie um ficheiro vazio designado **Skpswi.dat**.  

2.  Clique com botão direito do **Skpswi.dat** do ficheiro e clique em **propriedades**. Nas propriedades do ficheiro do ficheiro Skpswi.dat, selecione o atributo **Oculto** .  

3.  Coloque o ficheiro **Skpswi.dat** na raiz de cada unidade de disco rígido cliente ou estrutura de pasta que pretenda excluir do inventário de software.  

> [!NOTE]  
>  O inventário de software só irá fazer de novo um inventário da unidade de cliente se este ficheiro for eliminado da unidade no computador cliente.
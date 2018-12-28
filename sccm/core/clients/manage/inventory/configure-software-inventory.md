---
title: Configurar o inventário de software
titleSuffix: Configuration Manager
description: Configurar o inventário de software e excluir pastas do inventário de software no Configuration Manager.
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0e3b6e1ab2962cec7891501ec6b19f081631e187
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421132"
---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Como configurar inventário de software no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este procedimento configura as predefinições de cliente para inventário de software e aplica-se a todos os computadores na sua hierarquia. Se pretender aplicar estas definições apenas a alguns computadores, crie uma definição de cliente de dispositivo personalizada e atribua-a uma coleção. Para obter mais informações sobre como criar definições personalizadas de dispositivos, consulte [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md)   

## <a name="to-configure-software-inventory"></a>Para configurar o inventário de software  

1. Na consola do Configuration Manager, escolha **Administration** > **definições de cliente****predefinições de cliente**.    

2. Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

3. Na **predefinições** caixa de diálogo caixa, escolha **inventário de Software**.  

4. Na lista **Definições do Dispositivo** , configure os seguintes valores:  

   -   **Ativar inventário de software nos clientes** – na lista pendente, selecione **True**.  

   -   **Ficheiros e inventário agendar software coleção** – configura o intervalo no qual os clientes recolhem inventário de software e ficheiros.   

5. Configure as definições de cliente de que necessita. O [inventário de Software](../../../../core/clients/deploy/about-client-settings.md#software-inventory) secção a [sobre definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) artigo tem uma lista das definições de cliente.  

   Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, consulte [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

   > [!TIP]
   >   O código de erro 80041006 na inventoryprovider.log significa que o provedor WMI é a memória esgotada. Ou seja, foi atingido o limite de quota de memória de um fornecedor e o fornecedor de inventário não é possível continuar.
   > Neste caso, o agente de inventário cria um relatório com 0 entradas para que não existem itens de inventário são comunicadas. <br/>
   > Uma solução possível para este erro seria reduzir o âmbito da coleção de inventário de software. Em circunstâncias quando o erro ocorrer depois de limitar o escopo de inventário, aumentando a [MemoryPerHost](https://blogs.technet.microsoft.com/askperf/2008/09/16/memory-and-handle-quotas-in-the-wmi-provider-service/) propriedade definida no [_ProviderHostQuotaConfiguration](https://msdn.microsoft.com/library/aa394671) classe pode fornecer uma solução.

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>Excluir pastas do inventário de software  

1.  Utilizando o Notepad.exe, crie um ficheiro vazio designado **Skpswi.dat**.  

2.  Com o botão direito a **skpswi** do ficheiro e clique em **propriedades**. Nas propriedades do ficheiro do ficheiro Skpswi.dat, selecione o atributo **Oculto** .  

3.  Coloque o ficheiro **Skpswi.dat** na raiz de cada unidade de disco rígido cliente ou estrutura de pasta que pretenda excluir do inventário de software.  

> [!NOTE]  
>  O inventário de software só irá fazer de novo um inventário da unidade de cliente se este ficheiro for eliminado da unidade no computador cliente.
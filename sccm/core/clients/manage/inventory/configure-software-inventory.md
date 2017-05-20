---
title: "Configurar o inventário de software | Documentos do Microsoft"
description: "Configurar o inventário de software e excluir pastas a partir do inventário de software no Configuration Manager."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
caps.latest.revision: 5
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9c5d1e48b76392beaf54b5377c69b648537e86f8
ms.openlocfilehash: e60cec71c425e5e42d450cbeee366528d4b42405
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Como configurar inventário de software no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Este procedimento configura as predefinições de cliente para inventário de software e aplica-se a todos os computadores na sua hierarquia. Se pretender aplicar estas definições para apenas alguns computadores, crie uma definição de cliente de dispositivo personalizada e atribua-a para uma coleção que contém os computadores que pretende utilizar o inventário de software. Para obter mais informações sobre como criar definições personalizadas do dispositivo, consulte o artigo [como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

## <a name="to-configure-software-inventory"></a>Para configurar o inventário de software  

1.  Na consola do Configuration Manager, escolha **administração** > **definições de cliente****predefinições de cliente**.    

4.  No **base** separador o **propriedades** grupo, selecione **propriedades**.  

5.  No **predefinições** diálogo caixa, selecione **inventário de Software**.  

6.  Na lista **Definições do Dispositivo** , configure os seguintes valores:  

    -   **Ativar inventário de software nos clientes** – na lista pendente, selecione **verdadeiro**.  

    -   **Agenda de coleção de agenda software ficheiros e inventário** - configura o intervalo no qual inventário de software recolher de clientes e ficheiros.   

7.  Configure as definições de cliente de que necessita. Para obter uma lista de definições de cliente de inventário de software que pode configurar, consulte o [inventário de Software](../../../../core/clients/deploy/about-client-settings.md#software-inventory) secção a [sobre definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) tópico.  

 Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, veja [Como gerir clientes no System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  


## <a name="to-exclude-folders-from-software-inventory"></a>Excluir pastas do inventário de software  

1.  Utilizando o Notepad.exe, crie um ficheiro vazio designado **Skpswi.dat**.  

2.  Clique com o botão direito do rato no ficheiro **Skpswi.dat** e clique em **Propriedades**. Nas propriedades do ficheiro do ficheiro Skpswi.dat, selecione o atributo **Oculto** .  

3.  Coloque o ficheiro **Skpswi.dat** na raiz de cada unidade de disco rígido cliente ou estrutura de pasta que pretenda excluir do inventário de software.  

> [!NOTE]  
>  O inventário de software só irá fazer de novo um inventário da unidade de cliente se este ficheiro for eliminado da unidade no computador cliente.

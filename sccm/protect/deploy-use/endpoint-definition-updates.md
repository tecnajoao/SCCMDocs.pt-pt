---

title: Configurar o Endpoint Protection | Documentos do Microsoft
description: "Aprenda a selecionar e configurar os métodos com o Endpoint Protection no System Center Configuration Manager, para manter as definições antimalware atualizada nos computadores cliente."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 537dd2a7-4e44-4877-b8dd-5e1499407f8d
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 017bd5b899b364fc832c721d63cc7dbad0a11671
ms.openlocfilehash: b5da7900a4f8e2f330c4dcb2cac00b45099bd909
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017



---

#  <a name="configure-definition-updates-for-endpoint-protection"></a>Configurar atualizações de definições do Endpoint Protection  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Com o Endpoint Protection no System Center Configuration Manager, pode utilizar qualquer um dos diversos métodos para manter as definições antimalware atualizada nos computadores cliente na sua hierarquia. As informações contidas neste tópico podem ajudá-lo a selecionar e a configurar estes métodos.

 Para atualizar as definições de antimalware, pode utilizar um ou mais dos seguintes métodos:

-   [Atualizações distribuídas do Configuration Manager](endpoint-definitions-configmgr.md) -este método utiliza atualizações de software do Configuration Manager para fornecer atualizações de definições e de motor a computadores na sua hierarquia.

-   [Atualizações distribuídas a partir do Windows Server Update Services (WSUS)](endpoint-definitions-wsus.md) -este método utiliza a infraestrutura do WSUS para fornecer atualizações de definições e de motor a computadores.

-   [Atualizações distribuídas do Microsoft Update](endpoint-definitions-microsoft-updates.md) -este método permite aos computadores para se ligar diretamente ao Microsoft Update para transferir as atualizações de definições e de motor. Este método pode ser útil para computadores que não são muitas vezes ligados à rede empresarial.

-   [Atualizações distribuídas do Microsoft Malware Protection Center](endpoint-definitions-protection-center.md) -este método irão transferir atualizações de definições do Microsoft Malware Protection Center.

-   [Atualizações a partir de partilhas de ficheiros UNC](endpoint-definitions-network.md) -com este método, pode guardar as atualizações de definições e de motor mais recentes para uma partilha na rede. Em seguida, os clientes podem aceder à rede para instalar as atualizações.

 Pode configurar várias origens de atualização de definições e controlar a ordem pela qual são avaliadas e aplicadas. Isto é feito na caixa de diálogo **Configurar Origens de Atualização da Definição** quando cria uma política antimalware.

> [!IMPORTANT]
>  Para Windows 10 PCs, tem de configurar o Endpoint Protection para atualizar as definições de software maligno do Windows Defender.

## <a name="how-to-configure-definition-update-sources"></a>Como Configurar Origens de Atualização de Definições
 Utilize o procedimento seguinte para configurar as origens de atualização de definições para utilizar para cada política antimalware.

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.

2.  Na área de trabalho **Ativos e Compatibilidade** , expanda **Endpoint Protection**e clique em **Políticas Antimalware**.

3.  Abra a página de propriedades da **Política Antimalware Predefinida** ou crie uma nova política antimalware. Para obter mais informações sobre como criar políticas antimalware, consulte o artigo [como criar e implementar políticas de proteção contra software maligno do Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).

4.  Na secção **Atualizações da definição** da caixa de diálogo de propriedades de antimalware, clique em **Definir Origem**.

5.  Na caixa de diálogo **Configurar Origens de Atualização da Definição** , selecione as origens a utilizar para atualizações de definições. Pode clicar em **Para cima** ou **Para baixo** para modificar a ordem pela qual estas origens são utilizadas.

6.  Clique em **OK** para fechar a caixa de diálogo **Configurar Origens de Atualização da Definição** .

## <a name="configure-endpoint-protection-definitions"></a>Configurar definições do Endpoint Protection

-   [Atualizações distribuídas do Configuration Manager](endpoint-definitions-configmgr.md) -este método utiliza atualizações de software do Configuration Manager para fornecer atualizações de definições e de motor a computadores na sua hierarquia.

-   [Atualizações distribuídas a partir do Windows Server Update Services (WSUS)](endpoint-definitions-wsus.md) -este método utiliza a infraestrutura do WSUS para fornecer atualizações de definições e de motor a computadores.

-   [Atualizações distribuídas do Microsoft Update](endpoint-definitions-microsoft-updates.md) -este método permite aos computadores para se ligar diretamente ao Microsoft Update para transferir as atualizações de definições e de motor. Este método pode ser útil para computadores que não são muitas vezes ligados à rede empresarial.

-   Atualizações distribuídas do Microsoft Malware Protection Center - este método irão transferir atualizações de definições do Microsoft Malware Protection Center.

-   [Atualizações a partir de partilhas de ficheiros UNC](endpoint-definitions-network.md) -com este método, pode guardar as atualizações de definições e de motor mais recentes para uma partilha na rede. Em seguida, os clientes podem aceder à rede para instalar as atualizações.

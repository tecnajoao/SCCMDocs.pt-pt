---
title: Configurar alertas do Endpoint Protection | Documentos do Microsoft
description: Saiba como configurar alertas do Endpoint Protection no System Center Configuration Manager.
ms.custom: na
ms.date: 03/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 7f4329b289b606dee5bf31aad8207de52667229f
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---

#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Configurar alertas para o Endpoint Protection no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Pode configurar alertas do Endpoint Protection no Microsoft System Center Configuration Manager para notificar os utilizadores administrativos quando eventos específicos, tais como infeções de software maligno, ocorrem na sua hierarquia. Apresentam notificações no dashboard do Endpoint Protection na consola do Configuration Manager no **alertas** nó do **monitorização** área de trabalho, ou pode ser enviado por correio eletrónico para os utilizadores especificados.

 Utilize os seguintes passos e procedimentos suplementares neste tópico para configurar alertas do Endpoint Protection no Configuration Manager.

> [!IMPORTANT]
>  Tem de ter o **impor a segurança** permissão para coleções para configurar alertas do Endpoint Protection.

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Passos para configurar alertas para o Endpoint Protection no Configuration Manager

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Coleções de Dispositivos**.

3.  Na lista **Coleções de Dispositivos** , selecione a coleção para a qual pretende configurar alertas e, no separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.

    > [!NOTE]
    >  Não é possível configurar alertas de coleções de utilizadores.

4.  No **alertas** separador do *< nome da coleção\>***propriedades** caixa de diálogo, selecione **ver esta coleção no dashboard do Endpoint Protection** se pretender ver os detalhes acerca das operações de proteção contra software maligno para esta coleção no **monitorização** área de trabalho da consola do Configuration Manager.

    > [!NOTE]
    >  Esta opção não está disponível para a coleção **Todos os Sistemas** .

5.  No **alertas** separador do *< nome da coleção\>***propriedades** caixa de diálogo, clique em **adicionar**.

6.  No **adicionar novos alertas de coleção** caixa de diálogo a **gerar um alerta quando estas condições aplicam-se** secção, selecione os alertas que pretende que o Configuration Manager para gerar quando ocorrerem os eventos de Endpoint Protection especificados e, em seguida, clique em **OK**.

7.  No **condições** lista do **alertas** separador, selecione cada alerta de Endpoint Protection e, em seguida, especifique as seguintes informações:

    -   **Nome do alerta** - aceite o nome predefinido ou introduza um novo nome para o alerta.

    -   **Gravidade do alerta** - na lista, selecione o nível de alerta para apresentar na consola do Configuration Manager.

8.  Consoante o alerta que selecionou, especifique as seguintes informações adicionais:

    -   **Deteção de software maligno** -este alerta é gerado se for detetado malware em qualquer computador na coleção que monitorizar. O **limiar de deteção de software maligno** Especifica os níveis de deteção de software maligno no qual este alerta é gerado:

        -   **Alta - todas as deteções de Trojans** -é gerado o alerta quando existem um ou mais computadores na coleção especificada onde qualquer software maligno é detetado, independentemente da qual o cliente do Endpoint Protection demora a ação.

        -   **Média - detetado, ação pendente** - é gerado o alerta quando existe um ou mais computadores na coleção especificada nos quais é detetado software maligno, e tem de remover manualmente o software maligno.

        -   **Baixa - detetado, ainda ativo** -é gerado o alerta quando existem um ou mais computadores na coleção especificada no qual o software maligno é detetado e ainda estão ativo.

    -   **Ataque de software maligno** -este alerta é gerado se especificada é detetado software maligno numa percentagem especificada de computadores na coleção que monitorizar.

        -   **Percentagem de computadores com software maligno detetado** -é gerado o alerta quando a percentagem de computadores com software maligno detetado na coleção excede a percentagem que especificar. Especifique uma percentagem de **1** a **99**.

            > [!NOTE]
            >  O valor de percentagem baseia-se no número de computadores na coleção, mas exclui os computadores que não tenham um cliente do Configuration Manager instalado. Inclui computadores que ainda não tenham o cliente do Endpoint Protection instalado.

    -   **Deteção de software maligno repetido** -este alerta é gerado se for detetado software maligno específico mais de um número de vezes ao longo de um número especificado de horas nos computadores na coleção que monitorizar especificado. Especifique as seguintes informações para configurar este alerta:

        -   **Número de vezes que o software maligno foi detetado:** - O alerta é gerado quando o mesmo software maligno for detetado em computadores na coleção mais do que o número de vezes especificado. Especifique um número de **2** a **32**.

        -   **Intervalo de deteção (horas):** Especifique o intervalo de deteção (em horas) em que o número de deteções de software maligno deve ocorrer. Especifique um número de **1** a **168**.

    -   **Deteção de múltiplo software maligno** - este alerta é gerado se mais do que um número especificado de tipos de software maligno é detetado através de um número especificado de horas em computadores na coleção que monitorizar. Especifique as seguintes informações para configurar este alerta:

        -   **Número de tipos de software maligno detetados:** É gerado o alerta quando o número especificado de tipos de software maligno diferentes forem detetado em computadores na coleção. Especifique um número de **2** a **32**.

        -   **Intervalo de deteção (horas):** Especifique o intervalo de deteção, em horas, na qual o número de deteções de software maligno deve ocorrer. Especifique um número de **1** a **168**.

9. Clique em **OK** para fechar o *< nome da coleção\>***propriedades** caixa de diálogo.  

## <a name="alert-for-outdated-malware-client"></a>Alerta de cliente de software maligno Desatualizadas

A partir do Configuration Manager versão 1702, pode configurar um alerta para garantir que os clientes de Endpoint Protection não estão desatualizados. Agora pode ver **versão de cliente de proteção contra software maligno** e **estado de implementação do Endpoint Protection** acedendo **ativos e compatibilidade** > **descrição geral** > **dispositivos** > **todos os computadores de secretária e servir os clientes**. Para verificar a existência de um alerta, ver **alertas** no **monitorização** área de trabalho. Se mais de 20% dos clientes geridos estiver a executar uma versão expirada do software de proteção contra software maligno, a versão de cliente de proteção contra software maligno é desatualizada é apresentado o alerta. Este alerta não aparece no **monitorização** > **descrição geral** separador. Para atualizar clientes antimalware expirada, ative atualizações de software para clientes de proteção contra software maligno.

Para configurar a percentagem com que é gerado o alerta, expanda **monitorização** > **alertas** > **todos os alertas**, faça duplo clique **clientes de proteção contra software maligno desatualizados** e modificar o **emitir um alerta se a percentagem de clientes geridos com uma versão desatualizada do cliente de proteção contra software maligno é mais do que** opção.

> [!div class="button"]
[Passo seguinte >](endpoint-definition-updates.md)

> [!div class="button"]
[Segurança >](endpoint-protection-site-role.md)


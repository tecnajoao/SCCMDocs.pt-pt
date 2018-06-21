---
title: Configurar alertas do Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como configurar alertas do Endpoint Protection no System Center Configuration Manager.
ms.date: 03/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 275ce06520174adf10100b77a8034620b072c93f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348672"
---
#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Configurar alertas para o Endpoint Protection no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Pode configurar alertas do Endpoint Protection no Microsoft System Center Configuration Manager para notificar os utilizadores administrativos quando ocorrem eventos específicos, como uma infeção de software maligno na sua hierarquia. As notificações são apresentadas no dashboard do Endpoint Protection na consola do Configuration Manager no **alertas** o nó do **monitorização** área de trabalho, ou podem ser enviados por e-mail para os utilizadores especificados.

 Utilize os seguintes passos e os procedimentos suplementares descritos neste tópico para configurar alertas para o Endpoint Protection no Configuration Manager.

> [!IMPORTANT]
>  Tem de ter o **impor segurança** permissão para coleções para configurar alertas do Endpoint Protection.

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Passos para configurar alertas para o Endpoint Protection no Configuration Manager

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Coleções de Dispositivos**.

3.  Na lista **Coleções de Dispositivos** , selecione a coleção para a qual pretende configurar alertas e, no separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.

    > [!NOTE]
    >  Não é possível configurar alertas de coleções de utilizadores.

4.  No **alertas** separador do *<nome da coleção\>***propriedades** caixa de diálogo, selecione **ver esta coleção no dashboard do Endpoint Protection** se pretende ver detalhes sobre operações antimalware relativas a esta coleção no **monitorização** área de trabalho da consola do Configuration Manager.

    > [!NOTE]
    >  Esta opção não está disponível para a coleção **Todos os Sistemas** .

5.  No **alertas** separador do *<nome da coleção\>***propriedades** caixa de diálogo, clique em **adicionar**.

6.  No **adicionar novos alertas da coleção** caixa de diálogo a **gerar um alerta quando estas condições se aplicarem** secção, selecione os alertas que pretende que o Configuration Manager para gerar quando ocorrem eventos de Endpoint Protection especificados e, em seguida, clique em **OK**.

7.  No **condições** lista do **alertas** separador, selecione cada alerta de Endpoint Protection e, em seguida, especifique as seguintes informações:

    -   **Nome do alerta** - aceite o nome predefinido ou introduza um novo nome para o alerta.

    -   **Gravidade do alerta** - na lista, selecione o nível de alerta a apresentar na consola do Configuration Manager.

8.  Dependendo do alerta que selecionar, especifique as seguintes informações adicionais:

    -   **Deteção de software maligno** -este alerta é gerado se for detetado software maligno em qualquer computador na coleção que monitoriza. O **limiar de deteção de software maligno** Especifica os níveis de deteção de software maligno em que este alerta é gerado:

        -   **Elevado - todas as deteções** -o alerta é gerado quando existe um ou mais computadores na coleção especificada nos quais qualquer software maligno é detetado, independentemente da ação demora o cliente do Endpoint Protection.

        -   **Médio – detetado, ação pendente** - o alerta é gerado quando existe um ou mais computadores na coleção especificada nos quais é detetado software maligno, e tem de remover manualmente o software maligno.

        -   **Baixa – detetado, ainda ativo** -o alerta é gerado quando existe um ou mais computadores na coleção especificada que software maligno é detetado e ainda está ativo.

    -   **Surto de software maligno** -este alerta é gerado se for especificada é detetado software maligno numa percentagem especificada de computadores na coleção que monitoriza.

        -   **Percentagem de computadores com software maligno detetado** -o alerta é gerado quando a percentagem de computadores com software maligno detetado na coleção excede a percentagem que especificar. Especifique uma percentagem de **1** a **99**.

            > [!NOTE]
            >  O valor de percentagem baseia-se no número de computadores na coleção, mas exclui os computadores que não tenham um cliente de Configuration Manager instalado. Inclui computadores que ainda não tenham o cliente do Endpoint Protection instalado.

    -   **Deteção de software maligno repetido** -este alerta é gerado se for detetado software maligno específico mais de um número especificado de vezes ao longo de um número especificado de horas nos computadores na coleção que monitoriza. Especifique as seguintes informações para configurar este alerta:

        -   **Número de vezes que o software maligno foi detetado:** - O alerta é gerado quando o mesmo software maligno for detetado em computadores na coleção mais do que o número de vezes especificado. Especifique um número de **2** a **32**.

        -   **Intervalo de deteção (horas):** Especifique o intervalo de deteção (em horas) em que o número de deteções de software maligno tem de ocorrer. Especifique um número de **1** a **168**.

    -   **Deteção de software maligno de vários** - este alerta é gerado se mais do que um número especificado de tipos de software maligno é detetado através de um número especificado de horas nos computadores na coleção que monitoriza. Especifique as seguintes informações para configurar este alerta:

        -   **Número de tipos de software maligno detetado:** O alerta é gerado quando o número especificado de tipos de outro software maligno for detetado nos computadores na coleção. Especifique um número de **2** a **32**.

        -   **Intervalo de deteção (horas):** Especifique o intervalo de deteção, em horas, em que o número de deteções de software maligno tem de ocorrer. Especifique um número de **1** a **168**.

9. Clique em **OK** para fechar o *<nome da coleção\>***propriedades** caixa de diálogo.  

## <a name="alert-for-outdated-malware-client"></a>Alerta de cliente de software maligno Desatualizadas

A partir do Configuration Manager versão 1702, pode configurar um alerta para garantir que os clientes de Endpoint Protection não estão desatualizados. Agora, pode ver **versão de cliente Antimalware** e **estado de implementação do Endpoint Protection** acedendo **ativos e compatibilidade** > **descrição geral** > **dispositivos** > **todos os ambientes de trabalho e a servir clientes**. Verificar a existência de um alerta, ver **alertas** no **monitorização** área de trabalho. Se mais de 20% dos clientes geridos estão em execução uma versão do antimalware software expirada, a versão de cliente Antimalware está desactualizada é apresentado o alerta. Este alerta não aparecer no **monitorização** > **descrição geral** separador. Para atualizar os clientes de antimalware expirada, ative atualizações de software para clientes de antimalware.

Para configurar a percentagem em que o alerta é gerado, expanda **monitorização** > **alertas** > **todos os alertas**, faça duplo clique em **Antimalware clientes desatualizados** e modificar o **emitir um alerta se a percentagem de clientes geridos com uma versão desatualizada do cliente antimalware é mais do que** opção.

> [!div class="button"]
[Passo seguinte >](endpoint-definition-updates.md)

> [!div class="button"]
[Volta >](endpoint-protection-site-role.md)

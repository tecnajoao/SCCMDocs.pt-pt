---
title: "Configurar a reativação por LAN | Documentos do Microsoft"
description: "Selecione as definições de reativação por LAN no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
caps.latest.revision: 7
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: 9c920651ba1dc6e0a28df458d28956126ddbaff0
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="how-to-configure-wake-on-lan-in-system-center-configuration-manager"></a>Como configurar a reativação por LAN no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Especifique reativação por LAN as definições para o System Center Configuration Manager quando pretender reativar computadores em estado de suspensão para instalar o software necessário, tal como atualizações de software, aplicações, sequências de tarefas e programas.

Pode complementar a reativação por LAN utilizando as definições de cliente de proxy de reativação. No entanto, para utilizar o proxy de reativação, deve primeiro ativar a reativação por LAN para o site e especificar **utilizar apenas pacotes de reativação** e **Unicast** opção para a reativação método de transmissão de reativação por LAN. Esta solução de reativação também suporta ligações ad-hoc, como uma ligação de ambiente de trabalho remoto.

Utilize o primeiro procedimento para configurar um site primário para reativação por LAN. Em seguida, utilize o segundo procedimento para configurar as definições de cliente de proxy de reativação. Este segundo procedimento configura as predefinições de cliente para que as definições de proxy de reativação aplicar a todos os computadores na hierarquia. Se pretender que estas definições aplicam-se a apenas computadores selecionados, crie uma definição de dispositivo personalizada e atribua-a para uma coleção que contém os computadores que pretende configurar para o proxy de reativação. Para obter mais informações sobre como criar definições de cliente personalizadas, veja [Como configurar as definições do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

Um computador que recebe as definições de cliente de proxy de reativação, provavelmente, irá interromper a ligação de rede de 1 a 3 segundos. Isto ocorre porque o cliente tem de repor a placa de interface de rede para ativar o controlador de proxy de reativação no mesmo.

> [!WARNING]
> Para evitar uma interrupção inesperada dos serviços de rede, avalie primeiro o proxy de reativação numa infraestrutura de rede isolada e representativa. Em seguida, utilize definições personalizadas de cliente para expandir o teste para um grupo selecionado de computadores de várias sub-redes. Para obter mais informações sobre como reativar o proxy, consulte o artigo [planear como reativar clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).

## <a name="to-configure-wake-on-lan-for-a-site"></a>Para configurar a reativação por LAN para um site

1. Na consola do Configuration Manager, aceda a **administração > Configuração do Site > Sites**.
2. Clique no site primário a configurar e, em seguida, clique em **propriedades**.
3. Clique na **reativação por LAN** separador e configure as opções que sejam necessárias para este site. Para suportar o proxy de reativação, certifique-se de que seleciona **utilizar apenas pacotes de reativação** e **Unicast**. Para obter mais informações, consulte o artigo [planear como reativar clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Clique em **OK** e repita o procedimento para todos os sites primários na hierarquia.

## <a name="to-configure-wake-up-proxy-client-settings"></a>Para configurar definições de cliente de proxy de reativação

1. Na consola do Configuration Manager, aceda a **administração > definições de cliente**.
2. Clique em **predefinições de cliente**e, em seguida, clique em **propriedades**.
3. Selecione **gestão de energia** e, em seguida, escolha **Sim** para **ativar o proxy de reativação**.
4. Reveja e se for necessário, configure as outras definições de proxy de reativação. Para obter mais informações sobre estas definições Consulte [Power as definições de gestão](../../../core/clients/deploy/about-client-settings.md#power-management).
5. Clique em **OK** para fechar a caixa de diálogo e, em seguida, clique em **OK** para fechar a caixa de diálogo de predefinições de cliente.

Pode utilizar os seguintes relatórios de reativação por LAN para monitorizar a instalação e configuração de proxy de reativação:

- Resumo do estado de implementação do proxy de reativação
- Detalhes do estado de implementação do proxy de reativação

> [!TIP]
> Para testar o funcionamento do proxy de reativação, teste uma ligação a um computador em modo de suspensão. Por exemplo, ligar para uma pasta partilhada desse computador ou tente ligar-se ao computador utilizando o ambiente de trabalho remoto. Se utilizar o acesso direto, verifique se os prefixos IPv6 funcionam com os mesmos testes de um computador em modo de suspensão, que está atualmente na Internet.


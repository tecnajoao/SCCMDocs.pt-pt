---
title: Configurar a Wake on LAN
titleSuffix: Configuration Manager
description: Selecione as definições de reativação por LAN no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e8e486cd2aad20e9ae0017abed3bb776768c3182
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138743"
---
# <a name="how-to-configure-wake-on-lan-in-system-center-configuration-manager"></a>Como configurar a reativação por LAN no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Especifica reativação nas definições de rede local para o System Center Configuration Manager, quando deseja para que os computadores fora do Estado de suspensão para instalar o software necessário, como atualizações de software, aplicações, sequências de tarefas e programas.

Pode complementar a reativação por LAN utilizando as definições de cliente de proxy de reativação. No entanto, para utilizar um proxy de reativação, tem primeiro de ativar reativação por LAN para o site e especificar **utilizar apenas pacotes de reativação** e o **Unicast** opção para a reativação no método de transmissão de LAN. Esta solução de reativação também suporta ligações ad-hoc, como uma conexão de área de trabalho remota.

Utilize o primeiro procedimento para configurar um site primário para Wake on LAN. Em seguida, utilize o segundo procedimento para configurar as definições de cliente de proxy de reativação. Este segundo procedimento configura as predefinições de cliente para as definições de proxy de reativação aplicar a todos os computadores na hierarquia. Se pretender que estas definições se apliquem apenas a computadores selecionados, crie uma definição personalizada do dispositivo e atribua-a numa coleção que contenha os computadores que pretende configurar para um proxy de reativação. Para obter mais informações sobre como criar definições de cliente personalizadas, veja [Como configurar as definições do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

Um computador que recebe as definições de cliente de proxy de reativação provavelmente irá colocar em pausa a conexão de rede de 1 a 3 segundos. Isto ocorre porque o cliente tem de repor a placa de interface de rede para permitir que o driver de um proxy de reativação no mesmo.

> [!WARNING]
> Para evitar uma interrupção inesperada dos serviços de rede, avalie primeiro o proxy de reativação numa infraestrutura de rede isolada e representativa. Em seguida, utilize definições personalizadas de cliente para expandir o teste para um grupo selecionado de computadores de várias sub-redes. Para obter mais informações sobre o funcionamento do proxy de reativação, consulte [planear como reativar clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).

## <a name="to-configure-wake-on-lan-for-a-site"></a>Para configurar a reativação por LAN para um site

1. Na consola do Configuration Manager, aceda a **administração > Configuração do Site > Sites**.
2. Clique no site primário a configurar e, em seguida, clique em **propriedades**.
3. Clique nas **reativação por LAN** separador e configurar as opções de que necessita para este site. Para suportar o proxy de reativação, certifique-se de que seleciona **utilizar apenas pacotes de reativação** e **Unicast**. Para obter mais informações, consulte [planear como reativar clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Clique em **OK** e repita o procedimento para todos os sites primários na hierarquia.

## <a name="to-configure-wake-up-proxy-client-settings"></a>Configurar as definições de cliente de proxy de reativação

1. Na consola do Configuration Manager, aceda a **administração > definições de cliente**.
2. Clique em **predefinições de cliente**e, em seguida, clique em **propriedades**.
3. Selecione **gestão de energia** e, em seguida, escolha **Sim** para **ativar o proxy de reativação**.
4. Reveja e, se necessário, configure as outras definições de proxy de reativação. Para obter mais informações sobre estas definições, consulte [definições de gestão de energia](../../../core/clients/deploy/about-client-settings.md#power-management).
5. Clique em **OK** para fechar a caixa de diálogo e, em seguida, clique em **OK** para fechar a caixa de diálogo de predefinições de cliente.

Pode utilizar os seguintes relatórios de reativação por LAN para monitorizar a instalação e configuração de proxy de reativação:

- Resumo do estado de implementação do proxy de reativação
- Detalhes do estado de implementação do proxy de reativação

> [!TIP]
> Para testar se o funcionamento do proxy de reativação, teste uma ligação a um computador em modo de suspensão. Por exemplo, ligar a uma pasta compartilhada nesse computador, ou tente ligar-se ao computador utilizando o ambiente de trabalho remoto. Se utilizar o acesso direto, verifique que os prefixos IPv6 funcionam com os mesmos testes de um computador em modo de suspensão, que está atualmente na Internet.

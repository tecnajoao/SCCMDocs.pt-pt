---
title: Ações de não conformidade
titleSuffix: Configuration Manager
description: Saiba como configurar as ações de não conformidade com o Configuration Manager
ms.date: 11/10/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be17e1f2b5c3fec02cdd6fc5f89aee9319c4dbb4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="set-up-actions-for-non-compliance"></a>Configurar as ações de não conformidade

O **as ações de não conformidade** permitem-lhe configurar uma sequência ordenada de tempo das ações que são aplicadas aos dispositivos que deixarem de estar em conformidade. Por exemplo, poderá pode enviar correio electrónico para o utilizador final de dispositivos não conformes e/ou marcar os dispositivos não conformes.

## <a name="before-you-begin"></a>Antes de começar

> [!IMPORTANT]
> Tem de ter a política de conformidade de dispositivo, pelo menos, um criado para configurar as ações de não conformidade.

Estas são as ações suportadas da não conformidade:

- Envie um e-mail para o utilizador final
- Marcar dispositivos não conformes

### <a name="send-e-mail-to-end-user"></a>Envie um e-mail para o utilizador final

Pode escolher a partir de modelos de e-mail predefinido pré-criadas ou criar uma notificação de e-mail totalmente personalizados. Configuration Manager fornece personalização do assunto, corpo da mensagem, incluindo o logótipo da empresa, informações de contacto e os destinatários adicionais.

### <a name="mark-devices-non-compliant"></a>Marcar dispositivos não conformes

Pode determinar o agendamento num número de dias que o dispositivo deve ser impedido de aceder a recursos empresariais. Isto pode dever-se imediatamente, mas também pode permitir ao utilizador um período de tolerância para estar em conformidade com as políticas de conformidade do dispositivo.

### <a name="supported-platforms"></a>Plataformas suportadas

Suportado pelo [todas as plataformas geridos através do Intune](https://docs.microsoft.com/intune/supported-devices-browsers).

## <a name="to-add-an-email-template"></a>Para adicionar um modelo de correio eletrónico

O Configuration Manager fornece modelos de correio eletrónico, mas também pode criar os seus próprios. O modelo de correio eletrónico é utilizado mais tarde no processo de criação de ações de não conformidade para comunicar com os utilizadores.

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade**.

2. No **ativos e compatibilidade** área de trabalho, expanda **as definições de compatibilidade**e, em seguida, escolha **modelos de notificação de conformidade**.

3. No **home page** separador o **criar modelo de notificação de conformidade**.

4. Tem de introduzir as seguintes informações: um. Nome: Nome do modelo de correio eletrónico.
    b. De: Endereço de correio eletrónico a enviar a notificação de correio eletrónico.
    c. Requerente: Um assunto que explica a notificação de correio eletrónico a enviar.
    d. Corpo da mensagem: Obter mais detalhes sobre a notificação de correio eletrónico.

    > [!TIP] 
    > Também pode incluir **cabeçalho de correio electrónico** com o logótipo da empresa e rodapé de E-mail que pode incluir o nome da empresa e informações de contacto. Também pode ser editada nas propriedades de que a subscrição do Intune.

5. Clique em **OK** para guardar o novo modelo de correio electrónico.

6. No **ação adicionar** página, pode selecionar o novo modelo de correio eletrónico da lista.

7. Depois de selecionar o modelo de correio electrónico, clique em **OK**.

## <a name="to-create-actions-for-non-compliance"></a>Para criar as ações de não conformidade

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade**.

2. No **ativos e compatibilidade** área de trabalho, expanda **as definições de compatibilidade**e, em seguida, escolha **políticas de conformidade**.

3. No **home page** separador o **criar** grupo, escolha **criar política de conformidade**.

4. Selecione o **plataformas suportadas** que pretende e clique em **seguinte** duas vezes. Pode ignorar o **regras** página.

5. No **ações de não conformidade** página, defina o que acontece quando um dispositivo se tornar não conforme, clique em **novo**.
6. Pode escolher duas opções: **Envie um e-mail para o utilizador final** ou **dispositivo marca incompatíveis**.

7. Se selecionar **enviar correio eletrónico para o utilizador final**, tem de introduzir o seguinte: um. **Período de tolerância (em dias):** Pode introduzir 0-365 dias.
    b. **Os destinatários adicionais (através de correio eletrónico)** c. **Selecione o modelo de mensagem:** Pode escolher os modelos de e-mail predefinido ou personalizados aqueles que adicionou.
    
    > [!TIP] 
    > Também pode adicionar um novo modelo de correio electrónico ao adicionar o **enviar correio eletrónico para o utilizador final** ação clicando **novo:** de **ação adicionar** página.

8. Se selecionar **dispositivo marca incompatíveis**, tem de introduzir o seguinte: um. **Período de tolerância (em dias):** Pode introduzir 0-365 dias.

9. Depois de escolher a ação e introduzir as definições para o mesmo, clique em **seguinte** duas vezes, em seguida, **fechar**.



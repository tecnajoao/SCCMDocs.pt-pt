---
title: Ações de não conformidade
titleSuffix: Configuration Manager
description: Saiba como configurar as ações de não conformidade com o Configuration Manager
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b6a974d1cca4f97cbcf41a0cf644f545cec4b37d
ms.sourcegitcommit: 7eebd112a9862bf98359c1914bb0c86affc5dbc0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/22/2018
ms.locfileid: "42589506"
---
# <a name="set-up-actions-for-non-compliance"></a>Configurar as ações de não conformidade

O **ações de não conformidade** permitem-lhe configurar uma sequência cronológica de ações que são aplicadas aos dispositivos que estão fora de conformidade. Por exemplo, enviar emails para o utilizador final de dispositivos não conformes e marcar os dispositivos não conformes.



## <a name="before-you-begin"></a>Antes de começar

> [!IMPORTANT]  
> Para configurar as ações de não conformidade, primeiro de criar pelo menos uma política de conformidade.  

Estas são as ações suportadas de não conformidade:

- Enviar e-mail ao utilizador final
- Marcar os dispositivos não conformes

### <a name="send-e-mail-to-end-user"></a>Enviar e-mail ao utilizador final

Escolha a partir de modelos de e-mail predefinidos pré-criados ou criar uma notificação de e-mail totalmente personalizada. O Configuration Manager permite personalizar o assunto, corpo da mensagem, incluindo o logótipo da empresa, informações de contacto e os destinatários adicionais.

### <a name="mark-devices-non-compliant"></a>Marcar os dispositivos não conformes

Determine um número de dias em que o dispositivo deve ser impedido de aceder a recursos empresariais. Esta ação pode ser imediata, mas pode também dar ao utilizador um período de tolerância para estar em conformidade com as políticas de conformidade do dispositivo.

### <a name="supported-platforms"></a>Plataformas suportadas

Suportado pelo [todas as plataformas geridos através do Intune](https://docs.microsoft.com/intune/supported-devices-browsers).



## <a name="to-add-an-email-template"></a>Para adicionar um modelo de e-mail

O Configuration Manager fornece modelos de e-mail, mas também pode criar seus próprios. O modelo de correio electrónico é utilizado mais tarde no processo de criação de ações de não conformidade para comunicar com os utilizadores.

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade**.  

2. Na **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**e, em seguida, escolha **modelos de notificação de conformidade**.  

3. Sobre o **home page** separador a **criar modelo de notificação de conformidade**.  

4. Introduza as seguintes informações:  

    a. **Nome**: Nome do modelo de correio eletrónico  

    > [!Note]  
    > O **partir** campo é preenchido automaticamente com um endereço de e-mail de resposta não da Microsoft.<!--SCCMDocs issue 652-->  

    c. **Assunto**: Um assunto que explica a notificação de email a ser enviada  

    d. **Corpo da mensagem**: Obter mais detalhes sobre a notificação de correio electrónico  

    > [!TIP]  
    > Também pode incluir **cabeçalho de email** com o logótipo da empresa, e **rodapé do E-mail**, que pode incluir o nome da sua organização e informações de contacto. Também edite essas informações nas propriedades de que a subscrição do Intune.  

5. Clique em **OK** para guardar o novo modelo de correio electrónico.  

6. Sobre o **adicionar ação** , selecione o novo modelo de correio electrónico a partir da lista.  

7. Depois de selecionar o modelo de correio electrónico, clique em **OK**.  



## <a name="to-create-actions-for-non-compliance"></a>Para criar ações de não conformidade

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade**.  

2. Na **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**e, em seguida, escolha **políticas de conformidade**.  

3. Sobre o **home page** separador a **criar** de grupo, escolha **criar política de conformidade**.  

4. Selecione o **plataformas suportadas** que pretende e clique em **próxima** duas vezes. Pode ignorar o **regras** página.  

5. Sobre o **ações de não conformidade** página, para definir o que acontece quando um dispositivo deixa de ser não compatível, clique em **New**.  

6. Pode escolher duas opções: **Enviar e-mail ao utilizador final** ou **Marcar dispositivos como não conformes**.  

7. Se selecionou **enviar e-mail ao utilizador final**, introduza os seguintes detalhes:  

    a. **Período de tolerância (em dias):** Insira um número de dias de 0 a 365  

    b. **Destinatários adicionais (por email)**  

    c. **Selecione o modelo de mensagem:** Escolha um modelo de e-mail predefinido ou um modelo personalizado que criou.  
    
    > [!TIP]   
    > Também pode adicionar um novo modelo de correio electrónico ao adicionar o **enviar e-mail ao utilizador final** ação clicando **New** partir o **adicionar ação** página.  

8. Se selecionou **Marcar dispositivos como não conformes**, introduza os seguintes detalhes:  

    a. **Período de tolerância (em dias):** Insira um número de dias de 0 a 365  

9. Conclua o assistente.  


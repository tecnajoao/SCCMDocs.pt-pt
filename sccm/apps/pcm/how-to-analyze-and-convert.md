---
title: Como analisar e converter pacotes
titleSuffix: Configuration Manager
description: Saiba como analisar e converter pacotes com o Package Conversion Manager no Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f3bf1737-827d-48fa-8bb1-f48fe71afe0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 50ec232c9f5b007ef7a139cbe7894c333b6eed63
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137886"
---
# <a name="how-to-analyze-and-convert-packages-with-package-conversion-manager"></a>Como analisar e converter pacotes com o Gestor de conversão de pacotes

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1357861-->

Antes de poder converter um pacote, analisá-lo primeiro. Consoante os resultados da análise, em seguida, pode fazer uma das seguintes tarefas:

- **Converter** o pacote para uma aplicação. Sobre o **pacote** lista na consola, o estado de preparação apresenta **automática**.  

- **Corrigir e converter** o pacote, anexar coleções e criar condições globais. Sobre o **pacote** lista na consola, o estado de preparação apresenta **automática**.  

- **Corrigir e converter** o pacote. Sobre o **pacote** lista na consola, o estado de preparação apresenta **Manual**.  

- Deixe não converta o pacote. Sobre o **pacote** lista na consola, o estado de preparação apresenta **não aplicável**.  



## <a name="bkmk_analyze"></a> Como analisar pacotes

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho. Expanda **gestão de aplicações**e selecione o **pacotes** nó.  

2. Selecione o pacote para converter. Na **home page** separador do Friso, no **conversão do pacote** grupo, selecione **analisar pacote**. Gestor de conversão de pacotes analisa o pacote.  

3. Para ver o estado de preparação do pacote, adicione a **preparação** coluna à lista de pacotes. O estado de preparação do pacote determina a ação seguinte:  

    - **Automática**: [Como converter pacotes](#bkmk_convert)  

        Para além disso, anexar coleções e criar condições globais com uma **automática** estado de preparação, consulte [como corrigir e converter pacotes](#bkmk_fix).  

    - **Manual**: [Como corrigir e converter pacotes](#bkmk_fix)

    - **Não aplicável**: Este pacote está em falta um programa ou de conteúdo necessário. Adicione qualquer conteúdo ou programas em falta e repita a análise. Ou deixá-la no estado de não convertido e continuar a implementá-lo como um pacote.  



## <a name="bkmk_convert"></a> Como converter pacotes

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho. Expanda **gestão de aplicações**e selecione o **pacotes** nó.  

2. Selecione o pacote para converter com um Estado de preparação **automática**. Sobre o **home page** separador do Friso, na **conversão de pacote** grupo, selecione **converter pacote**. A converter pacote para o Assistente de aplicativo é aberto.  

3. A converter pacote para o Assistente de aplicação, reveja a lista de pacotes selecionados. Remover todos os pacotes que não pretende converter e selecione **OK**. Gestor de conversão de pacotes converte o pacote. A janela de conversão completa lista o estado de conversão de novos aplicativos.  

    > [!Note]  
    > Quando converte um pacote, o site regista a data e hora da conversão como hora UTC.  

4. Siga as instruções na janela. Selecione **ver aplicativos** ou **fechar**.  



## <a name="bkmk_fix"></a> Como corrigir e converter pacotes

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho. Expanda **gestão de aplicações**e selecione o **pacotes** nó.  

2. Selecionar um pacote com um Estado de preparação **Manual** ou **automática**. Sobre o **home page** separador do Friso, na **conversão de pacote** grupo, selecione **corrigir e converter**.  

3. No Assistente de conversão de pacote, reveja as informações sobre o **seleção de pacote** página, observar o **itens a corrigir**. Em seguida, selecione **seguinte**.  

4. Sobre o **revisão de dependência** página, reveja se o pacote for dependente de outros pacotes listados e, em seguida, selecione **próxima**.  

    > [!Note]  
    > Se ainda não convertido qualquer um dos pacotes dependentes listados, comece por converter esses pacotes. Em seguida, reinicie o processo de conversão de pacote.  
    >  
    > Se uma dependência não é necessária, elimine-o, ou ignorá-lo e continuar o processo de conversão.  

5. Sobre o **tipo de implementação** , reveja os tipos de implementação para a nova aplicação. Alterar as prioridades ou eliminar os tipos de implementação.  

6. Se qualquer um dos novos tipos de implementação não tem um método de deteção associado, o **método de deteção** coluna exibe um ícone de aviso. Conclua as seguintes ações:  

    1. Selecione **Editar método de deteção**.  

    2. Selecione **Adicionar**.  

    3. Na caixa de diálogo de regra de deteção, especifique um **tipo de definição**.  

    4. Para o tipo de definição especificada, introduza as informações adicionais necessárias para a regra de deteção.  

    5. Selecione **OK**. Se necessário, repita este processo para adicionar vários métodos de deteção para cada tipo de implementação.  

    6. Selecione **OK**. Verifique se o **método de deteção** coluna exibe um ícone para confirmar se um método de deteção foi especificado corretamente.  

7. Selecione **Seguinte**.  

8. Sobre o **seleção de requisitos** , reveja os tipos de implementação do novo aplicativo. Selecione um tipo de implementação e reveja os requisitos para esse tipo de implementação.  

    > [!Note]  
    > O assistente apresenta apenas os requisitos que converte do Gestor de conversão de pacotes. Ele não se converte todas as consultas WQL em coleções de dispositivos aos requisitos.  

9. Adicione requisitos para um tipo de implementação selecionado, se necessário.  

10. Selecione **Seguinte**.  

11. Conclua o Assistente para criar a aplicação.  

    > [!Note]  
    > Quando converte um pacote, o site regista a data e hora da conversão como hora UTC.  



## <a name="bkmk_monitor"></a> Monitor

Vá para o **monitorização** área de trabalho da consola do Configuration Manager e selecione **estado de conversão de pacote**. Este dashboard mostra o estado geral de análise e conversão de pacotes no site. Uma nova tarefa em segundo plano automaticamente resume os dados de análise.

> [!Tip]  
> Gestor de conversão de pacotes integrado com o Configuration Manager não exige que agendar uma análise de pacotes. Esta ação é processada pela tarefa de resumo integrada.

![Captura de ecrã do dashboard de estado de conversão de pacote de exemplo](media/1357861-pcm-dashboard.png)

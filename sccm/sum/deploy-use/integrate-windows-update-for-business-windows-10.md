---
title: Integração com o Windows Update for Business no Windows 10
titleSuffix: Configuration Manager
description: Utilizar o Windows Update para empresas para manter os dispositivos baseados no Windows 10 na sua organização atualizados para dispositivos ligados ao serviço Windows Update.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.collection: M365-identity-device-management
ms.openlocfilehash: 456e4537e7c397063c50422e8c408dc5d688af04
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121579"
---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>Integração com o Windows Update for Business no Windows 10

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Windows Update for Business (WUfB) permite-lhe manter os dispositivos baseados no Windows 10 na sua organização sempre atualizados com as mais recentes defesas de segurança e os recursos do Windows quando estes dispositivos se ligam diretamente ao serviço Windows Update (WU). O Configuration Manager pode diferenciar computadores Windows 10 que utilizam o WUfB e o WSUS para obter as atualizações de software.  

 Algumas funcionalidades do Configuration Manager já não estão disponíveis quando os clientes do Configuration Manager estão configurados para receber atualizações do WU, que inclui o WUfB ou Windows Insiders:  

-   Relatórios de conformidade do Windows Update:  

    -   O Configuration Manager não terá conhecimento das atualizações publicadas no WU. Clientes do Configuration Manager configurados para receber atualizações do WU apresentarão **desconhecido** para estas atualizações na consola do Configuration Manager.  

    -   Resolução de problemas de estado de conformidade geral é difícil porque **desconhecido** estado foi apenas para os clientes que não tinham comunicado o estado da análise do WSUS. Agora também inclui os clientes do Configuration Manager que recebem atualizações do WU.  

    -   Acesso condicional (para recursos da empresa) com base no estado de conformidade de atualização não funcionará conforme esperado nos clientes que recebem atualizações do WU, porque estes nunca iriam cumprir a conformidade do Configuration Manager.  

    -   A conformidade das Atualizações de Definições faz parte dos relatórios de conformidade de atualização gerais e também não funcionará conforme esperado.  A conformidade das atualizações de definições também faz parte da avaliação de acesso condicional  

-   Em geral relatórios de Endpoint Protection para o Defender baseados no estado de conformidade de atualização não retornará resultados precisos devido aos dados de análise em falta.  

-   Não será capaz de implantar as atualizações da Microsoft, como o Office, IE e Visual Studio para os clientes que estão ligados ao WUfB para receber atualizações do Configuration Manager.  

-   Não será capaz de implantar o 3º atualizações de terceiros publicadas no WSUS e geridas através do Gestor de configuração para clientes que estão ligados ao WUfB para receber atualizações do Configuration Manager.  

-   Implementação de cliente completa do Configuration Manager que utiliza a infraestrutura de atualizações de software não irá funcionar para clientes que estão ligados ao WUfB para receber atualizações.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Identificar os clientes que utilizam o WUfB para Windows 10 atualizações  
 Utilize o procedimento seguinte para identificar os clientes que utilizam o WUfB para obter atualizações do Windows 10. Em seguida, configurar estes clientes para parar de utilizar o WSUS para obter atualizações e implementar uma definição para desativar o fluxo de trabalho de atualizações de software para estes clientes de agente de cliente.  

 **Pré-requisitos**  

-   Clientes com Windows 10 Desktop Pro ou Windows 10 Enterprise Edition, versão 1511 ou posterior  

-   O[Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) é implementado e os clientes utilizam o WUfB para obter atualizações do Windows 10.  

#### <a name="to-identify-clients-that-use-wufb"></a>Para identificar os clientes que utilizam o WUfB  

1.  Desative o agente de atualização do Windows, de modo que não faça análises no WSUS, se tiver sido ativado previamente. A chave de registo seguinte pode ser definida para indicar se o computador está a analisar no WSUS ou no Windows Update.  Quando o valor é 2, não está a analisar no WSUS.  
    - **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**

2.  Existe um novo atributo, **UseWUServer**, sob o **Windows Update** nó no Explorador de recursos do Configuration Manager.  

3.  Crie uma coleção com base no atributo **UseWUServer** para todos os computadores ligados através de WUfB para obter atualizações e melhoramentos.  

4.  Crie uma definição para desativar o fluxo de trabalho de atualização de software do agente de cliente. Implemente a definição para a coleção de computadores que estejam ligados diretamente ao WUfB.  

5.  Os computadores que são geridos através de WUfB apresentará **desconhecido** o estado de conformidade e estes não serão considerados parte da percentagem de conformidade geral.  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configurar a atualização do Windows para políticas de diferimento de negócios
<!-- 1290890 --> A partir do Configuration Manager versão 1706, pode configurar políticas de diferimento para atualizações de funcionalidades do Windows 10 ou atualizações de qualidade para o Windows 10 dispositivos geridos diretamente pelo Windows Update para empresas. Pode gerir as políticas de diferimento no novo **Windows Update para políticas de negócio** no nó **biblioteca de Software** > **manutenção do Windows 10**.

>[!NOTE] 
>A partir do Configuration Manager versão 1802, pode definir políticas de diferimento para Windows Insider. <!--507201-->Para obter mais informações sobre o programa Windows Insider, consulte [introdução ao programa Windows Insider para empresas](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business).

### <a name="prerequisites"></a>Pré-requisitos
-   Windows 10 versão 1703 ou posterior
-   Dispositivos Windows 10 geridos pelo Windows Update para empresas tem de ter conectividade à Internet

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Para criar uma atualização do Windows para a política de diferimento de negócio
1. Na **biblioteca de Software** > **manutenção do Windows 10** > **Windows Update para políticas de negócio**
2. Sobre o **home page** separador a **criar** grupo, selecione **criar Windows política Update para empresas** para abrir a atualização do Windows criar para o Assistente de política de negócios.
3. Sobre o **gerais** , indique um nome e descrição para a política.
4. Sobre o **políticas de diferimento** página, configure se pretende diferir ou colocar em pausa atualizações de funcionalidades. As atualizações de funcionalidade são, geralmente, novas funcionalidades do Windows. Depois de configurar o **ramificar o nível de preparação** definir, em seguida, pode definir se, e durante quanto tempo, gostaria de diferir a receção de atualizações de funcionalidades após a sua disponibilidade da Microsoft.
    - **Nível de preparação para filiais**: Defina o ramo para o qual o dispositivo irá receber atualizações do Windows (Current Branch ou Current Branch for Business).
    - **Período de diferimento (dias)**:  Especifique o número de dias de diferimento para que as atualizações de funcionalidade. Pode diferir a receção destas atualizações de funcionalidades durante um período de 365 dias a partir do seu lançamento.
    - **A partir de atualizações de funcionalidades em pausa**: Selecione se colocar em pausa dispositivos recebam atualizações de funcionalidades durante um período de 60 dias desde o momento em que colocar em pausa as atualizações. Após ter passado o máximo de dias, a funcionalidade de pausa irá automaticamente expirar e o dispositivo irá procurar atualizações do Windows para detetar atualizações aplicáveis. Após esta procura, pode colocar as atualizações em pausa novamente. Pode unpause atualizações de funcionalidades ao desmarcar a caixa de verificação.   
5. Escolha se pretende diferir ou colocar em pausa as atualizações de qualidade. As atualizações de qualidade são, geralmente, correções e melhorias às funcionalidades existentes do Windows e, normalmente, são publicadas na primeira Terça-feira de cada mês, embora possam ser lançadas em qualquer altura pela Microsoft. Pode definir se, e durante quanto tempo, gostaria de diferir a receção de atualizações de qualidade, após a sua disponibilidade.
    - **Período de diferimento (dias)**: Especifique o número de dias de diferimento para que as atualizações de qualidade. Pode diferir a receção destas atualizações de qualidade durante um período de 30 dias a partir do seu lançamento.
    - **A partir de atualizações de qualidade em pausa**: Selecione se colocar em pausa a receção de atualizações de qualidade de dispositivos durante um período máximo de 35 dias desde o momento em que colocar em pausa as atualizações. Após ter passado o máximo de dias, a funcionalidade de pausa irá automaticamente expirar e o dispositivo irá procurar atualizações do Windows para detetar atualizações aplicáveis. Após esta procura, pode colocar as atualizações em pausa novamente. Pode unpause as atualizações de qualidade ao desmarcar a caixa de verificação.
6. Selecione **instalar atualizações a partir de outros Products Microsoft** para ativar a definição de política de grupo que tornam as definições de suspensão aplicáveis ao Microsoft Update, bem como as atualizações do Windows.
7. Selecione **incluir drivers com o Windows Update** para atualizar automaticamente os controladores de atualizações do Windows. Se desmarcar esta definição, as atualizações de controladores não são transferidas de atualizações do Windows.
8. Conclua o Assistente para criar a nova política de diferimento.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Implementar uma atualização do Windows para a política de diferimento de negócio
1. Na **biblioteca de Software** > **manutenção do Windows 10** > **Windows Update para políticas de negócio**
2. Sobre o **home page** separador a **implantação** grupo, selecione **implementar Windows política Update para empresas**.
3. Configure as seguintes definições:
    - **Política de configuração para implementar**: Selecione a atualização do Windows para a política de negócios que gostaria de implementar.
    - **Coleção**: Clique em **procurar** para selecionar a coleção onde pretende implementar a política.
    - **Remediar regras incompatíveis quando suportado**: Selecione esta opção para retificar automaticamente quaisquer regras não compatíveis com o Windows Management Instrumentation (WMI), o registro, scripts e todas as definições para dispositivos móveis inscritos pelo Configuration Manager.
    - **Permitir remediação fora da janela de manutenção**: Se uma janela de manutenção tiver sido configurada para a coleção que pretende implementar a política, ative esta opção para que as definições de conformidade retifiquem o valor fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [como utilizar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).
    - **Gerar um alerta**: Configura um alerta que é gerado se a compatibilidade da linha de base de configuração for inferior a uma percentagem especificada até uma data especificada e a hora. Também pode especificar se pretende que seja enviado um alerta para o System Center Operations Manager.
    - **Atraso aleatório (horas)**: Especifica uma janela de atraso para evitar processamento excessivo no serviço de inscrição de dispositivos de rede. O valor predefinido é de 64 horas.
    - **Agenda**: Especifique o agendamento de avaliação de compatibilidade através do qual o perfil implementado é avaliado nos computadores cliente. O agendamento pode ser simples ou personalizado. O perfil é avaliado por computadores cliente quando o utilizador inicia sessão.
4.  Conclua o Assistente para implementar o perfil.

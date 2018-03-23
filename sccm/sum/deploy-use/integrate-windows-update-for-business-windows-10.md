---
title: Integração com o Windows Update for Business no Windows 10
titleSuffix: Configuration Manager
description: Utilize o Windows Update para empresas para manter os dispositivos baseados no Windows 10 na sua organização atualizados para os dispositivos ligados ao serviço Windows Update.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology:
- configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: e27e5f043af28b74369f21d19e5b20e19572213a
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>Integração com o Windows Update for Business no Windows 10

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Windows Update for Business (WUfB) permite-lhe manter os dispositivos baseados no Windows 10 na sua organização sempre atualizados com as mais recentes defesas de segurança e funcionalidades do Windows quando estes dispositivos se ligam diretamente ao serviço Windows Update (WU). O Configuration Manager é capaz de distinguir entre computadores Windows 10 que utilizam o WUfB e o WSUS para obter as atualizações de software.  

 Algumas funcionalidades do Configuration Manager já não estão disponíveis quando os clientes do Configuration Manager estão configurados para receber atualizações do WU, que inclui o WUfB ou Windows Insiders:  

-   Relatórios de conformidade do Windows Update:  

    -   O Configuration Manager será conhecimento das atualizações que são publicadas no WU. Clientes do Configuration Manager configurados para receber atualizações do WU apresentarão **desconhecido** para estas atualizações na consola do Configuration Manager.  

    -   Resolução de problemas de estado de conformidade geral é difícil porque **desconhecido** estado era apenas para os clientes que não tinham comunicado o estado de análise novamente a partir do WSUS. Agora inclui também os clientes do Configuration Manager que recebem atualizações do WU.  

    -   Acesso condicional (para recursos da empresa) com base no estado de conformidade de atualização não funcionará conforme esperado para clientes que recebem atualizações do WU, porque estes nunca iriam cumprir a conformidade do Configuration Manager.  

    -   A conformidade das Atualizações de Definições faz parte dos relatórios de conformidade de atualização gerais e também não funcionará conforme esperado.  A conformidade das atualizações de definições também faz parte da avaliação de acesso condicional  

-   Em geral reporting Endpoint Protection para o Defender baseados no estado de conformidade de atualização não devolverão resultados precisos devido aos dados de análise em falta.  

-   O Configuration Manager não poderá implementar atualizações da Microsoft, tais como Office, IE e Visual Studio para clientes que estejam ligados ao WUfB para receber atualizações.  

-   O Configuration Manager não poderá implementar atualizações de terceiros 3rd que são publicadas no WSUS e geridas através do Gestor de configuração para clientes que estejam ligados ao WUfB para receber atualizações.  

-   Implementação de cliente completa do Configuration Manager que utiliza a infraestrutura de atualizações de software não irá funcionar para clientes que estão ligados ao WUfB para receber atualizações.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Identificar clientes que utilizam o WUfB para Windows 10 atualizações  
 Utilize o procedimento seguinte para identificar os clientes que utilizam o WUfB para obter atualizações do Windows 10 e atualizações. Em seguida, configurar estes clientes para deixar de utilizar o WSUS para obter atualizações e implementar uma definição para desativar o fluxo de trabalho de atualizações de software para estes clientes de agente de cliente.  

 **Pré-requisitos**  

-   Clientes com Windows 10 Desktop Pro ou Windows 10 Enterprise Edition, versão 1511 ou posterior  

-   O[Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) é implementado e os clientes utilizam o WUfB para obter atualizações do Windows 10.  

#### <a name="to-identify-clients-that-use-wufb"></a>Para identificar os clientes que utilizam o WUfB  

1.  Desative o agente do Windows Update para que não faça análises no WSUS, se tiver sido ativado anteriormente. A seguinte chave de registo pode ser definida para indicar se o computador está a analisar no WSUS ou no Windows Update.  Quando o valor é 2, não está a analisar no WSUS.  
    - **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**

2.  Há um novo atributo **UseWUServer**, sob o **Windows Update** nó no Explorador de recursos do Configuration Manager.  

3.  Crie uma coleção com base no atributo **UseWUServer** para todos os computadores ligados através de WUfB para obter atualizações e melhoramentos.  

4.  Crie uma definição para desativar o fluxo de trabalho de atualização de software do agente de cliente. Implemente a definição para a coleção de computadores que estejam ligados diretamente ao WUfB.  

5.  Os computadores que são geridos através de WUfB apresentará **desconhecido** estado de conformidade e não serão contados como parte da percentagem de conformidade geral.  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configurar o Windows Update para as políticas de diferimento por de negócio
<!-- 1290890 -->
A partir do Configuration Manager versão 1706, pode configurar políticas de diferimento por para atualizações de funcionalidade do Windows 10 ou qualidade atualizações para o Windows 10 dispositivos geridos diretamente pelo Windows Update for Business. Pode gerir as políticas de diferimento por na nova **Windows Update para as políticas de negócio** nó **biblioteca de Software** > **manutenção do Windows 10**.

>[!NOTE] 
>A partir do Configuration Manager versão 1802, pode definir políticas de diferimento por para Windows Insider. <!--507201-->Para obter mais informações sobre o programa Windows Insider, consulte [começar a utilizar o programa Windows Insider para empresas](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business).

### <a name="prerequisites"></a>Pré-requisitos
Dispositivos Windows 10 geridos pelo Windows Update para empresas tem de ter conectividade à Internet.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Para criar uma atualização do Windows para a política de diferimento por de negócio
1. No **biblioteca de Software** > **manutenção do Windows 10** > **Windows Update para as políticas de negócio**
2. No **home page** separador o **criar** grupo, selecione **criar Windows Update para empresas política** para abrir o Windows Update criar para o Assistente de política de negócio.
3. No **geral** , indique um nome e descrição para a política.
4. No **diferimento por políticas** página, configure se pretende diferir ou colocar em pausa as atualizações de funcionalidade. Atualizações de funcionalidade são geralmente novas funcionalidades do Windows. Depois de configurar o **sucursal nível de preparação** , em seguida, pode definir se e para o período de tempo, gostaria diferir atualizações de funcionalidades a seguir a respetiva disponibilidade da Microsoft a receber.
    - **Nível de preparação de sucursal**: Defina o ramo para o qual o dispositivo irá receber atualizações do Windows (Current Branch ou Current Branch for Business).
    - **Período de diferimento por (dias)**:  Especifique o número de dias para o qual vai ser diferidas atualizações de funcionalidade. Pode diferir receber estas atualizações de funcionalidade durante um período de 180 dias a partir da respetiva versão.
    - **Iniciar de atualizações de funcionalidades de pausa**: Selecione se para colocar em pausa dispositivos de receber atualizações de funcionalidade durante um período de 60 dias desde o momento em coloque em pausa as atualizações. Após ter passado o máximo de dias, a funcionalidade de pausa automaticamente irá expirar e o dispositivo irá analisar as atualizações do Windows para detetar atualizações aplicáveis. Seguir esta análise, pode colocar em pausa as atualizações de novo. Pode unpause atualizações de funcionalidade desmarcando a caixa de verificação.   
5. Escolha se pretende diferir ou atualizações de qualidade de colocar em pausa. Atualizações de qualidade são, geralmente, correções e melhoramentos a funcionalidades existentes do Windows e, normalmente, são publicadas primeira Terça-feira de cada mês, que podem ser libertadas em qualquer altura ao Microsoft. Pode definir se e para o período de tempo, gostaria diferir atualizações de qualidade após a respetiva disponibilidade a receber.
    - **Período de diferimento por (dias)**: Especifique o número de dias para o qual vai ser diferidas atualizações de funcionalidade. Pode diferir receber estas atualizações de funcionalidade durante um período de 180 dias a partir da respetiva versão.
    - **Iniciar de atualizações de qualidade de pausa**: Selecione se para colocar em pausa dispositivos a partir da qualidade a receber atualizações durante um período de 35 dias desde o momento em coloque em pausa as atualizações. Após ter passado o máximo de dias, a funcionalidade de pausa automaticamente irá expirar e o dispositivo irá analisar as atualizações do Windows para detetar atualizações aplicáveis. Seguir esta análise, pode colocar em pausa as atualizações de novo. Pode unpause qualidade atualizações ao desmarcar a caixa de verificação.
6. Selecione **instalar atualizações a partir de outros Microsoft Products** para ativar a definição de política de grupo que as definições de diferimento por aplicável ao Microsoft Update, bem como as atualizações do Windows.
7. Selecione **incluir controladores com o Windows Update** para atualizar automaticamente os controladores de atualizações do Windows. Se desmarcar esta definição, as atualizações de controladores não são transferidas atualizações do Windows.
8. Conclua o Assistente para criar a nova política de diferimento por.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Implementar uma atualização do Windows para a política de diferimento por de negócio
1. No **biblioteca de Software** > **manutenção do Windows 10** > **Windows Update para as políticas de negócio**
2. No **home page** separador o **implementação** grupo, selecione **implementar o Windows Update para empresas política**.
3. Configure as seguintes definições:
    - **Política de configuração para implementar**: Selecione a atualização do Windows para a política de negócio que gostaria de implementar.
    - **Coleção**: Clique em **procurar** para selecionar a coleção onde pretende implementar a política.
    - **Remediar regras incompatíveis quando suportado**: Selecione esta opção para retificar automaticamente quaisquer regras não compatíveis para o Windows Management Instrumentation (WMI), o registo, scripts e todas as definições para dispositivos móveis que são inscritos pelo Configuration Manager.
    - **Permitir remediação fora da janela de manutenção**: Se uma janela de manutenção tiver sido configurada para a coleção à qual está a implementar a política, ative esta opção para que as definições de conformidade retifiquem o valor fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [como utilizar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).
    - **Gerar um alerta**: Configura um alerta que é gerado se a compatibilidade da linha de base de configuração for inferior a uma percentagem especificada por uma data e hora especificadas. Também pode especificar se pretende que seja enviado um alerta para o System Center Operations Manager.
    - **Atraso aleatório (horas)**: Especifica uma janela de atraso para evitar processamento excessivo no serviço de inscrição de dispositivos de rede. O valor predefinido é 64 horas.
    - **Agenda**: Especifique o agendamento de avaliação de compatibilidade através do qual o perfil implementado é avaliado nos computadores cliente. O agendamento pode ser simples ou personalizado. O perfil é avaliado por computadores cliente quando o utilizador inicia sessão.
4.  Conclua o Assistente para implementar o perfil.

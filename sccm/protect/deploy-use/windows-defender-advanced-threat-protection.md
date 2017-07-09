---
title: O Windows Defender Advanced Threat Protection | Microsoft Docs
description: "Saiba como gerenciar e monitorar o Windows Defender Advanced Threat Protection, um novo serviço que ajuda as empresas a responder a ataques avançados."
ms.custom: na
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
caps.latest.revision: 5
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0ebda27c0f3848615346c2ecf1ab8b9bb9ab6f0d
ms.openlocfilehash: 6c3b67278fa587c137a29e174e277fb0f15872c8
ms.contentlocale: pt-pt
ms.lasthandoff: 05/26/2017

---
# <a name="windows-defender-advanced-threat-protection"></a>O Windows Defender Advanced Threat Protection

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

A partir da versão 1606 do Configuration Manager (ramificação atual), proteção de ponto de extremidade pode ajudar a gerenciar e monitorar o Windows Defender Advanced Threat Protection (ATP. Windows Defender ATP é um novo serviço que ajuda as empresas a detectar, investigar e responder a ataques avançados em suas redes.  Saiba mais sobre [Windows Defender ATP](http://aka.ms/technet-wdatp). Políticas do Configuration Manager podem ajudar você a integrar e monitor gerenciados Windows 10, versão 1607 (compilação 14328) ou posterior.

Windows Defender ATP é um serviço no [Central de segurança do Windows](https://securitycenter.windows.com). Adicionando e implantando um arquivo de configuração de integração de cliente, Configuration Manager pode monitorar o status de implantação e a integridade do agente do Windows Defender ATP. Somente há suporte para o Windows Defender ATP em computadores que executam o cliente do Configuration Manager. Não há suporte para o gerenciamento de dispositivos móveis locais e computadores gerenciados por MDM do Intune híbrido.

 **Pré-requisitos**  

-   Assinatura do serviço online Windows Defender Advanced Threat Protection  
-   Computadores clientes que executam o Windows 10, versão 1607 e posterior  
-   Computadores clientes executando a versão de 1610 do Configuration Manager ou posterior do agente cliente

## <a name="how-to-create-an-onboarding-configuration-file"></a>Como criar um arquivo de configuração de integração  

 1.  Faça logon o [serviço online Windows Defender ATP](https://securitycenter.windows.com/)   

 2.  Clique no **gerenciamento de ponto de extremidade** item de menu.  

 3.  Selecione **versão 1606 do System Center Configuration Manager (ramificação atual)** e clique em **pacote de Download**.  

 4.  Baixe o arquivo do arquivo compactado (. zip) e extraia o conteúdo.

> [!IMPORTANT]
> O arquivo de configuração do Windows Defender ATP contém informações confidenciais que devem ser mantidas seguras.

## <a name="onboard-devices-for-windows-defender-atp"></a>Dispositivos integrados para Windows Defender ATP  

1.  No console do Configuration Manager, navegue **ativos e conformidade** > **visão geral** > **Endpoint Protection** > **políticas do Windows Defender ATP** e clique em **criar o Windows Defender ATP política**. O Assistente de política do Windows Defender ATP é aberto.  

2.  Tipo de **nome** e **descrição** para a política do Windows Defender ATP e selecione **integração**. Clique em **Seguinte**.  

3.  **Procurar** para o arquivo de configuração fornecido pelo locatário de serviço de nuvem do Windows Defender ATP da sua organização. Clique em **Seguinte**.  

4.  Especifique os exemplos de arquivos que são coletados e compartilhados de dispositivos gerenciados para análise.  

    -   **Nenhum**   

    -   **Todos os tipos de arquivo**  

     Clique em **Seguinte**.  

5.  Revise o resumo e conclua o assistente.  

6.  Agora você pode implantar a política do Windows Defender ATP para computadores cliente gerenciados clicando **implantar**.  

## <a name="monitor-windows-defender-atp"></a>Monitorar o Windows Defender ATP  

1.  No console do Configuration Manager, navegue **monitoramento** > **visão geral** > **segurança** e, em seguida, clique em **Windows Defender ATP**.  

2.  Examine o painel do Windows Defender Advanced Threat Protection.  

    -   **Status da implantação de agente do Windows Defender** – o número e a porcentagem de computadores cliente gerenciados qualificados active incorporada de política do Windows Defender ATP  

    -   **Integridade do agente do Windows Defender ATP** – porcentagem de computadores cliente comunicando o status para o agente do Windows Defender ATP  

        -   **Íntegro** -funcionando corretamente  

        -   **Inativo** -nenhum dado enviado ao serviço durante o período de tempo  

        -   **Estado do agente** -o serviço de sistema para o agente no Windows não está em execução  

        -   **Não estar incorporado** - diretiva foi aplicada, mas o agente não informou carregar política  


## <a name="how-to-create-and-deploy-an-offboarding-configuration-file"></a>Como criar e implantar um arquivo de configuração de cancelamento  

1.  Faça logon o [serviço online Windows Defender ATP](https://securitycenter.windows.com/)   

2.  Clique no **gerenciamento de ponto de extremidade** item de menu.  

3.  Selecione **versão 1606 do System Center Configuration Manager (ramificação atual)** e clique em **cancelamento de ponto de extremidade**.  

4.  Baixe o arquivo do arquivo compactado (. zip) e extraia o conteúdo. Arquivos de cancelamento são válidos por 30 dias.

5.  No console do Configuration Manager, navegue **ativos e conformidade** > **visão geral** > **Endpoint Protection** > **políticas do Windows Defender ATP** e clique em **criar o Windows Defender ATP política**. O Assistente de política do Windows Defender ATP é aberto.  

6.  Tipo de **nome** e **descrição** para a política do Windows Defender ATP e selecione **cancelamento**. Clique em **Seguinte**.  

7.  **Procurar** para o arquivo de configuração fornecido pelo locatário de serviço de nuvem do Windows Defender ATP da sua organização. Clique em **Seguinte**.  

8.  Revise o resumo e conclua o assistente.  

9.  Agora você pode implantar a política do Windows Defender ATP para computadores cliente gerenciados clicando **implantar**.  

> [!IMPORTANT]
> Os arquivos de configuração do Windows Defender ATP contém informações confidenciais que devem ser mantidas seguras.

[Proteção Avançada Contra Ameaças do Windows Defender](https://technet.microsoft.com/itpro/windows/keep-secure/windows-defender-advanced-threat-protection)

[Solucionar problemas de integração do Windows Defender Advanced Threat Protection](https://technet.microsoft.com/itpro/windows/keep-secure/troubleshoot-onboarding-windows-defender-advanced-threat-protection)


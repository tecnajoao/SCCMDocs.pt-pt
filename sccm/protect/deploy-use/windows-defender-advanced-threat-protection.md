---
title: O Windows Defender Advanced Threat Protection | Microsoft Docs
description: "Saiba como gerir e monitorizar o Windows Defender avançadas Threat Protection, um novo serviço que ajuda as empresas responder a ataques avançados."
ms.custom: na
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
caps.latest.revision: "5"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 6c3b67278fa587c137a29e174e277fb0f15872c8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="windows-defender-advanced-threat-protection"></a>O Windows Defender Advanced Threat Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir da versão 1606 do Configuration Manager (ramo atual), Endpoint Protection pode ajudar a gerir e monitorizar o Windows Defender Advanced Threat Protection (ATP. Windows Defender ATP é um novo serviço que o irão ajudar as empresas para detetar, analisar e responder a ataques avançados nas respetivas redes.  Saiba mais sobre [Windows Defender ATP](http://aka.ms/technet-wdatp). Políticas do Gestor de configuração podem ajudá-lo com a sua integração e monitor geridos Windows 10, versão 1607 (criar 14328) ou posterior.

Windows Defender ATP é um serviço no [Centro de segurança do Windows](https://securitycenter.windows.com). Ao adicionar e implementar um ficheiro de configuração de integração do cliente, o Configuration Manager pode monitorizar o estado de implementação e funcionamento de agente do Windows Defender ATP. Windows Defender ATP só é suportada em computadores que executam o cliente do Configuration Manager. Gestão de dispositivos móveis no local e a computadores de geridos por MDM híbrida do Intune não são suportados.

 **Pré-requisitos**  

-   Subscrição do serviço online do Windows Defender Advanced Threat Protection  
-   Computadores de clientes com o Windows 10, versão 1607 e posterior  
-   Computadores de clientes com a versão do Configuration Manager 1610 ou posterior do agente do cliente

## <a name="how-to-create-an-onboarding-configuration-file"></a>Como criar um ficheiro de configuração de integração  

 1.  Início de sessão para o [serviço online do Windows Defender ATP](https://securitycenter.windows.com/)   

 2.  Clique em de **Endpoint gestão** item de menu.  

 3.  Selecione **System Center Configuration Manager (ramo atual) versão 1606** e clique em **pacote de transferência**.  

 4.  Transfira o ficheiro de arquivo comprimido (. zip) e extraia os conteúdos.

> [!IMPORTANT]
> O ficheiro de configuração do Windows Defender ATP contém informações confidenciais que devem ser mantidas seguras.

## <a name="onboard-devices-for-windows-defender-atp"></a>Carregar dispositivos para o Windows Defender ATP  

1.  Na consola do Configuration Manager, navegue **ativos e compatibilidade** > **descrição geral** > **Endpoint Protection** > **Windows Defender ATP políticas** e clique em **criar Windows Defender ATP Policy**. É aberto o Assistente de política do Windows Defender ATP.  

2.  Tipo de **nome** e **Descrição** para o Windows Defender ATP policy selecione **integração**. Clique em **Seguinte**.  

3.  **Procurar** para o ficheiro de configuração fornecido pelo inquilino de serviço de nuvem de Windows Defender ATP da sua organização. Clique em **Seguinte**.  

4.  Especifique os exemplos de ficheiros que são recolhidos e partilhados a partir dos dispositivos geridos para análise.  

    -   **Nenhum**   

    -   **Todos os tipos de ficheiro**  

     Clique em **Seguinte**.  

5.  Reveja o resumo e conclua o assistente.  

6.  Agora pode implementar a política Windows Defender ATP para os computadores cliente geridos clicando **implementar**.  

## <a name="monitor-windows-defender-atp"></a>Monitorizar o Windows Defender ATP  

1.  Na consola do Configuration Manager, navegue **monitorização** > **descrição geral** > **segurança** e, em seguida, clique em **Windows Defender ATP**.  

2.  Reveja o dashboard do Windows Defender Advanced Threat Protection.  

    -   **Estado de implementação de agente do Windows Defender** – o número e a percentagem de computadores elegíveis cliente gerido com o Active Directory integrado de política Windows Defender ATP  

    -   **Estado de funcionamento do agente do Windows Defender ATP** – percentagem de clientes de computador a comunicar o estado para os respetivos agente do Windows Defender ATP  

        -   **Bom estado de funcionamento** -a funcionar corretamente  

        -   **Inativa** -não existem dados enviados ao serviço durante o período de tempo  

        -   **Estado do agente** -o serviço de sistema para o agente do Windows não está em execução  

        -   **Não integrado** - foi aplicada a política, mas o agente não comunicou carregar política  


## <a name="how-to-create-and-deploy-an-offboarding-configuration-file"></a>Como criar e implementar um ficheiro de configuração de exclusão  

1.  Início de sessão para o [serviço online do Windows Defender ATP](https://securitycenter.windows.com/)   

2.  Clique em de **Endpoint gestão** item de menu.  

3.  Selecione **System Center Configuration Manager (ramo atual) versão 1606** e clique em **exclusão de ponto final**.  

4.  Transfira o ficheiro de arquivo comprimido (. zip) e extraia os conteúdos. Exclusão de ficheiros são válidos durante 30 dias.

5.  Na consola do Configuration Manager, navegue **ativos e compatibilidade** > **descrição geral** > **Endpoint Protection** > **Windows Defender ATP políticas** e clique em **criar Windows Defender ATP Policy**. É aberto o Assistente de política do Windows Defender ATP.  

6.  Tipo de **nome** e **Descrição** para o Windows Defender ATP policy selecione **exclusão**. Clique em **Seguinte**.  

7.  **Procurar** para o ficheiro de configuração fornecido pelo inquilino de serviço de nuvem de Windows Defender ATP da sua organização. Clique em **Seguinte**.  

8.  Reveja o resumo e conclua o assistente.  

9.  Agora pode implementar a política Windows Defender ATP para os computadores cliente geridos clicando **implementar**.  

> [!IMPORTANT]
> Os ficheiros de configuração do Windows Defender ATP contém informações confidenciais que devem ser mantidas seguras.

[Proteção Avançada Contra Ameaças do Windows Defender](https://technet.microsoft.com/itpro/windows/keep-secure/windows-defender-advanced-threat-protection)

[Resolver problemas de integração do Windows Defender Advanced Threat Protection](https://technet.microsoft.com/itpro/windows/keep-secure/troubleshoot-onboarding-windows-defender-advanced-threat-protection)

---
title: "O Windows Defender avançadas ameaça proteção | Documentos do Microsoft"
description: "Saiba como gerir e monitorizar o Windows Defender avançadas ameaça Protection, um novo serviço que o ajuda a responder a ataques avançadas de empresas."
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
ms.sourcegitcommit: 8f4ec982a54cf3cefef310268a54850e70e2e63a
ms.openlocfilehash: 237dc9cbccb973720a633490f096aed4bc16d183
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="windows-defender-advanced-threat-protection"></a>O Windows Defender avançadas proteção ameaça

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir da versão 1606 do Configuration Manager (ramo atual), Endpoint Protection pode ajudar a gerir e monitorizar o Windows Defender avançadas ameaça Protection (ATP. Windows Defender ATP é um novo serviço que o irá ajudar empresas para detetar, analisar e responder a ataques avançadas nos redes deles.  Saiba mais sobre [Windows Defender ATP](http://aka.ms/technet-wdatp). As políticas do Configuration Manager podem ajudá-lo carregar e monitor geridos versão 1607 (criar 14328) do Windows 10 ou posterior.

Windows Defender ATP é um serviço no [Centro de segurança do Windows](https://securitycenter.windows.com). Ao adicionar e implementar um ficheiro de configuração de integração do cliente, do Configuration Manager pode monitorizar o estado de implementação e estado de funcionamento de agente de Windows Defender ATP. Windows Defender ATP só é suportada em PCs a executar o cliente do Configuration Manager. Gestão de dispositivos móveis no local e a computadores de geridos por MDM híbrido do Intune não são suportados.

 **Pré-requisitos**  

-   Subscrição do serviço do Windows Defender avançadas ameaça proteção online  

-   Clientes que executam o Windows 10, versão 1607 e posterior  

## <a name="how-to-create-an-onboarding-configuration-file"></a>Como criar um ficheiro de configuração de integração  

 1.  Início de sessão para o [serviço online do Windows Defender ATP](https://securitycenter.windows.com/)   

 2.  Clique no **Endpoint gestão** item de menu.  

 3.  Selecione **versão do System Center Configuration Manager (ramo atual) 1606** e clique em **transferir o pacote**.  

 4.  Transfira o ficheiro de arquivo comprimido (. zip) e extrair os conteúdos.

> [!IMPORTANT]
> O ficheiro de configuração do Windows Defender ATP contém informações confidenciais que devam ser mantidas seguras.

## <a name="onboard-devices-for-windows-defender-atp"></a>Carregar dispositivos para Windows Defender ATP  

1.  Na consola do Configuration Manager, navegue **ativos e compatibilidade** > **descrição geral** > **Endpoint Protection** > **Windows Defender ATP políticas** e clique em **criar Windows Defender ATP política**. O Assistente de política do Windows Defender ATP abre.  

2.  Tipo de **nome** e **Descrição** para a política do Windows Defender ATP e selecione **integração**. Clique em **Seguinte**.  

3.  **Procurar** ao ficheiro de configuração fornecido pelo inquilino do serviço de nuvem de Windows Defender ATP da sua organização. Clique em **Seguinte**.  

4.  Especifique os exemplos de ficheiros que são recolhidos e partilhados a partir de dispositivos geridos para análise.  

    -   **Nenhum**   

    -   **Todos os tipos de ficheiro**  

     Clique em **Seguinte**.  

5.  Reveja o resumo e conclua o assistente.  

6.  Agora pode implementar a política do Windows Defender ATP para computadores de cliente geridos clicando **implementar**.  

## <a name="monitor-windows-defender-atp"></a>Monitorizar o Windows Defender ATP  

1.  Na consola do Configuration Manager, navegue **monitorização** > **descrição geral** > **segurança** e, em seguida, clique em **Windows Defender ATP**.  

2.  Reveja o dashboard de proteção de ameaça avançada do Windows Defender.  

    -   **Estado de implementação de agente do Windows Defender** – o número e a percentagem de computadores elegíveis cliente gerido com o Active Directory onboarded de política do Windows Defender ATP  

    -   **Estado de funcionamento do agente do Windows Defender ATP** – percentagem de clientes de computador a comunicar o estado para o agente do Windows Defender ATP  

        -   **Bom estado de funcionamento** -a funcionar corretamente  

        -   **Inativo** -não existem dados enviados ao serviço durante o período de tempo  

        -   **Estado do agente** -o serviço de sistema para o agente do Windows não está em execução  

        -   **Não onboarded** - foi aplicada a política, mas o agente não comunicou carregar política  


## <a name="how-to-create-and-deploy-an-offboarding-configuration-file"></a>Como criar e implementar um ficheiro de configuração offboarding  

1.  Início de sessão para o [serviço online do Windows Defender ATP](https://securitycenter.windows.com/)   

2.  Clique no **Endpoint gestão** item de menu.  

3.  Selecione **versão do System Center Configuration Manager (ramo atual) 1606** e clique em **Endpoint offboarding**.  

4.  Transfira o ficheiro de arquivo comprimido (. zip) e extrair os conteúdos. Ficheiros de Offboarding são válidos nos últimos 30 dias.

5.  Na consola do Configuration Manager, navegue **ativos e compatibilidade** > **descrição geral** > **Endpoint Protection** > **Windows Defender ATP políticas** e clique em **criar Windows Defender ATP política**. O Assistente de política do Windows Defender ATP abre.  

6.  Tipo de **nome** e **Descrição** para a política do Windows Defender ATP e selecione **Offboarding**. Clique em **Seguinte**.  

7.  **Procurar** ao ficheiro de configuração fornecido pelo inquilino do serviço de nuvem de Windows Defender ATP da sua organização. Clique em **Seguinte**.  

8.  Reveja o resumo e conclua o assistente.  

9.  Agora pode implementar a política do Windows Defender ATP para computadores de cliente geridos clicando **implementar**.  

> [!IMPORTANT]
> Os ficheiros de configuração do Windows Defender ATP contém informações confidenciais que devam ser mantidas seguras.

[O Windows Defender avançadas proteção ameaça](https://technet.microsoft.com/itpro/windows/keep-secure/windows-defender-advanced-threat-protection)

[Resolver problemas de ativação da proteção de ameaça avançada do Windows Defender](https://technet.microsoft.com/itpro/windows/keep-secure/troubleshoot-onboarding-windows-defender-advanced-threat-protection)


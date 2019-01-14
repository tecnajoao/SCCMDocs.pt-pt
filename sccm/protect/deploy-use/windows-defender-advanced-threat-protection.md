---
title: Proteção Avançada Contra Ameaças do Windows Defender
titleSuffix: Configuration Manager
description: Saiba como gerir e monitorizar o Windows Defender proteção avançada contra ameaças, um novo serviço que ajuda as empresas a responder a ataques avançados.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f474db6768204403978eb188c3dbd138e34035d4
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422798"
---
# <a name="windows-defender-advanced-threat-protection"></a>Proteção Avançada Contra Ameaças do Windows Defender

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir da versão 1606 do Configuration Manager (ramo atual), Endpoint Protection pode ajudar a gerir e monitorizar [proteção de ameaças avançada do Windows Defender (ATP)](http://aka.ms/technet-wdatp). Windows Defender ATP ajuda as empresas a detetar, investigar e responder a ataques avançados em suas redes.  As políticas do Configuration Manager ou o Microsoft Intune podem ajudá-lo a integrar e monitor geridos com o Windows 10, versão 1607 (build 14328) ou posterior.

Windows Defender ATP é um serviço no [Centro de segurança do Windows Defender](https://securitycenter.windows.com). Ao adicionar e implementar um ficheiro de configuração de integração do cliente, o Configuration Manager pode monitorizar o estado da implementação e funcionamento de agente do Windows Defender ATP. Windows Defender ATP é suportado em PCs com o cliente do Configuration Manager ou gerido pelo Microsoft Intune, mas a computadores de geridos por MDM híbrida do Intune não são suportados.

 **Pré-requisitos**  

-   Subscrição do serviço online da proteção de ameaças avançada do Windows Defender  
-   Computadores de clientes que executam o Windows 10, versão 1607 e posterior  
-   Computadores de clientes que executam a versão 1610 do Configuration Manager ou posterior do agente do cliente ou geridos pelo Microsoft Intune

## <a name="how-to-create-an-onboarding-configuration-file"></a>Como criar um arquivo de configuração de integração  

 1.  Início de sessão para o [serviço online do Windows Defender ATP](https://securitycenter.windows.com/)   

 2.  Clique nas **ponto final de gestão** item de menu.  

 3.  Selecione **System Center Configuration Manager (ramo atual) versão 1606** e clique em **pacote de transferência**.  

 4.  Transfira o ficheiro de arquivo morto compactado (. zip) e extraia o conteúdo.

> [!IMPORTANT]
> O ficheiro de configuração do Windows Defender ATP contém informações confidenciais que devem ser mantidas seguras.

## <a name="onboard-devices-for-windows-defender-atp"></a>Carregar dispositivos para o Windows Defender ATP  

1. Na consola do Configuration Manager, navegue até **ativos e compatibilidade** > **descrição geral** > **Endpoint Protection**  >  **Políticas do Windows Defender ATP** e clique em **criar o Windows Defender ATP política**. É aberto o Assistente de política do Windows Defender ATP.  

2. Tipo de **Name** e **Descrição** para a política do Windows Defender ATP e selecione **integração**. Clique em **Seguinte**.  

3. **Procurar** ao arquivo de configuração fornecido pelo inquilino de serviço cloud da sua organização do Windows Defender ATP. Clique em **Seguinte**.  

4. Especifique os exemplos de ficheiros que são recolhidos e partilhados dos dispositivos geridos para análise.  

   - **Nenhum**   

   - **Todos os tipos de ficheiro**  

     Clique em **Seguinte**.  

5. Reveja o resumo e conclua o assistente.  

6. Agora pode implementar a política do Windows Defender ATP para computadores de cliente geridos ao clicar em **Deploy**.  

## <a name="monitor-windows-defender-atp"></a>Monitorizar o Windows Defender ATP  

1.  Na consola do Configuration Manager, navegue até **monitorização** > **descrição geral** > **segurança** e, em seguida, clique em **Windows Defender ATP**.  

2.  Reveja o dashboard de proteção de ameaças avançada do Windows Defender.  

    -   **Estado de implementação de agente do Windows Defender** – o número e percentagem de computadores de cliente gerenciado elegíveis com o Active Directory integrado de política do Windows Defender ATP  

    -   **Estado de funcionamento do agente do Windows Defender ATP** – porcentagem de computadores cliente comunicar o estado para o agente do Windows Defender ATP  

        -   **Bom estado de funcionamento** -a funcionar corretamente  

        -   **Inativo** -não existem dados enviados para o serviço durante o período de tempo  

        -   **Estado do agente** -o serviço de sistema para o agente no Windows não está em execução  

        -   **Não incluído** - política foi aplicada, mas o agente não comunicou carregar política  


## <a name="how-to-create-and-deploy-an-offboarding-configuration-file"></a>Como criar e implantar um arquivo de configuração de exclusão  

1.  Início de sessão para o [serviço online do Windows Defender ATP](https://securitycenter.windows.com/)   

2.  Clique nas **ponto final de gestão** item de menu.  

3.  Selecione **System Center Configuration Manager (ramo atual) versão 1606** e clique em **exclusão de ponto final**.  

4.  Transfira o ficheiro de arquivo morto compactado (. zip) e extraia o conteúdo. Ficheiros de exclusão são válidos durante 30 dias.

5.  Na consola do Configuration Manager, navegue até **ativos e compatibilidade** > **descrição geral** > **Endpoint Protection**  >  **Políticas do Windows Defender ATP** e clique em **criar o Windows Defender ATP política**. É aberto o Assistente de política do Windows Defender ATP.  

6.  Tipo de **Name** e **Descrição** para a política do Windows Defender ATP e selecione **exclusão**. Clique em **Seguinte**.  

7.  **Procurar** ao arquivo de configuração fornecido pelo inquilino de serviço cloud da sua organização do Windows Defender ATP. Clique em **Seguinte**.  

8.  Reveja o resumo e conclua o assistente.  

9.  Agora pode implementar a política do Windows Defender ATP para computadores de cliente geridos ao clicar em **Deploy**.  

> [!IMPORTANT]
> Os ficheiros de configuração do Windows Defender ATP contém informações confidenciais que devem ser mantidas seguras.

[Proteção Avançada Contra Ameaças do Windows Defender](https://technet.microsoft.com/itpro/windows/keep-secure/windows-defender-advanced-threat-protection)

[Resolver problemas de integração de proteção de ameaças avançada do Windows Defender](https://technet.microsoft.com/itpro/windows/keep-secure/troubleshoot-onboarding-windows-defender-advanced-threat-protection)

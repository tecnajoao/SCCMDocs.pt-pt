---
title: Criar e implementar uma política do Windows Defender Application Guard
titleSuffix: Configuration Manager
description: Criar e implementar a política do Windows Defender Application Guard.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6446fed2d48fc6428bdc3fbc7a24f728c206dc7
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132426"
---
# <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Criar e implementar a política do Windows Defender Application Guard 
*Aplica-se a: System Center Configuration Manager (ramo atual)* 
 <!-- 1351960 --> pode criar e implementar [do Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) políticas ao utilizar a proteção de ponto final do Configuration Manager . Estas políticas ajudam a proteger os seus utilizadores ao abrir sites não confiáveis no contentor isolado seguro que não está acessível por outras partes do sistema operativo.

## <a name="prerequisites"></a>Pré-requisitos

Para criar e implementar uma política do Windows Defender Application Guard, tem de utilizar atualização do Windows 10 Fall criador (1709). Além disso, os dispositivos Windows 10 nos quais implementou a política devem ser configurados com uma política de isolamento de rede. Para obter mais informações, consulte a [descrição geral do Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview). 


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Crie uma política e para procurar as definições disponíveis:

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade**.
2. Na **ativos e compatibilidade** área de trabalho, escolha **descrição geral** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Na **home page** separador a **Create** , clique em **criar política Windows Defender Application Guard**.
4. Utilizar o [artigo](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) como uma referência, pode procurar e configurar as definições disponíveis. O Configuration Manager permite-lhe definir determinadas definições de política ver [definições de interação do anfitrião](#BKMK_HIS) e [o comportamento do aplicativo](#BKMK_AppB).
5. Sobre o **definição de rede** página, especifique a identidade empresarial e defina o limite da rede empresarial.

    > [!NOTE]
    > Windows 10 PCs armazenar apenas uma lista de isolamento de rede no cliente. Pode criar dois tipos diferentes de listas de isolamento de rede e implementá-las para o cliente:
    >
    >  - uma do Windows Information Protection
    >  - uma do Windows Defender Application Guard
    >
    > Se implementar ambas as políticas, essas listas de isolamento de rede tem de corresponder. Se implementar listas que não correspondem para o mesmo cliente, a implementação irá falhar. Para obter mais informações, consulte a [documentação de Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
    > 
    > 

6. Quando tiver terminado, conclua o assistente e implementar a política para um ou mais dispositivos do Windows 10 1709.

### <a name="bkmk_HIS"></a> Definições de interação de anfitrião
Configura as interações entre dispositivos anfitrião e o contentor do Application Guard. Antes do Configuration Manager versão 1802, ambos os comportamento e o host a interação do aplicativo eram sob o **definições** separador.

- **Área de transferência** - sob definições antes do Configuration Manager 1802
    - Tipo de conteúdo permitido
        - Texto
        - Imagens
- **Impressão:**
    - Ativar a impressão para XPS
    - Ativar a impressão para PDF
    - Ativar a impressão para impressoras locais
    - Ativar a impressão para impressoras de rede
- **Gráficos:** (a partir do Configuration Manager versão 1802)
    - Acesso de processador de gráficos virtual
- **Ficheiros:** (a partir do Configuration Manager versão 1802)
    - Guardar ficheiros transferidos para alojar

### <a name="bkmk_ABS"></a> Definições de comportamento da aplicação
Configura o comportamento da aplicação dentro da sessão Application Guard. Antes do Configuration Manager versão 1802, ambos os comportamento e o host a interação do aplicativo eram sob o **definições** separador.

- **Conteúdo:**
   - Sites de Enterprise podem carregar conteúdo não empresarial, como plug-ins de terceiros.
- **Outros:**
    - Reter dados do browser gerados pelo utilizador
    - Auditar eventos de segurança na sessão isolada do application guard



## <a name="next-steps"></a>Passos seguintes
Para ler mais sobre o Windows Defender Application Guard: [Visão geral do Windows Defender Application Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview).
[FAQ do Windows Defender Application Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard).

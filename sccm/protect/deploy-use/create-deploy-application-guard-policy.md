---
title: Criar e implementar uma política de proteção de aplicações do Windows Defender
titleSuffix: Configuraton Manager
description: Criar e implementar a política de proteção de aplicações do Windows Defender.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e7f0a1ccb71abb2fec27e0430bd4195dc85aceae
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348077"
---
# <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Criar e implementar a política de proteção de aplicações do Windows Defender 
*Aplica-se a: O System Center Configuration Manager (ramo atual)*
<!-- 1351960 -->
Pode criar e implementar [Guard de aplicação do Windows Defender](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) políticas utilizando o endpoint protection do Configuration Manager. Estas políticas ajudam a proteger os seus utilizadores abrindo não fidedignos web sites num contentor isolado seguro que não pode ser acedido por outras partes do sistema operativo.

## <a name="prerequisites"></a>Pré-requisitos

Para criar e implementar uma política de proteção de aplicações do Windows Defender, tem de utilizar atualização do Windows 10, enquadram-se criador (1709). Além disso, os dispositivos Windows 10 nos quais implementou a política tem de ser configurados com uma política de isolamento de rede. Para obter mais informações, consulte o [descrição geral da proteção de aplicações do Windows Defender](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview). 


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Crie uma política de e para procurar as definições disponíveis:

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade**.
2. No **ativos e compatibilidade** área de trabalho, escolha **descrição geral** > **Endpoint Protection** > **Guard de aplicação do Windows Defender**.
3. No **home page** separador o **criar** , clique em **criar Windows Defender Guard política aplicações**.
4. Utilizar o [artigo](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) como uma referência, pode procurar e configurar as definições disponíveis. O Configuration Manager permite-lhe definir determinadas definições de política Consulte [interação definições de anfitrião](#BKMK_HIS) e [comportamento da aplicação](#BKMK_AppB).
5. No **definição de rede** página, especifique a identidade empresarial e definir o limite da rede empresarial.

    > [!NOTE]
    > Windows 10 PCs armazenar apenas uma lista de isolamento de rede no cliente. Pode criar dois tipos diferentes de listas de isolamento de rede e implementá-las para o cliente:
    >
    >  - um Windows Information Protection
    >  - um da proteção de aplicações do Windows Defender
    >
    > Se implementar ambas as políticas, estas listas de isolamento de rede tem de corresponder. Se implementar listas não correspondem ao cliente mesmo, a implementação irá falhar. Para obter mais informações, consulte o [documentação de Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
    > 
    > 

6. Quando tiver terminado, conclua o assistente e implementar a política para um ou mais dispositivos do Windows 10 1709.

### <a name="bkmk_HIS"></a> Definições de interação do anfitrião
Configura as interações entre os dispositivos de anfitrião e o contentor de proteção da aplicação. Antes do Configuration Manager versão 1802, ambos os interação de comportamento e o anfitrião de aplicação foram sob o **definições** separador.

- **Área de transferência** - sob definições antes 1802 do Configuration Manager
    - Tipo de conteúdo permitido
        - Texto
        - Imagens
- **Impressão:**
    - Permitir a impressão por para XPS
    - Permitir a impressão por para PDF
    - Permitir a impressão pela impressoras locais
    - Permitir a impressão por para impressoras de rede
- **Gráficos:** (a partir do Configuration Manager versão 1802)
    - Acesso de processador de gráficos virtuais
- **Ficheiros:** (a partir do Configuration Manager versão 1802)
    - Guardar os ficheiros transferidos para o anfitrião

### <a name="bkmk_ABS"></a> Definições de comportamento da aplicação
Configura o comportamento da aplicação no interior da sessão de proteção da aplicação. Antes do Configuration Manager versão 1802, ambos os interação de comportamento e o anfitrião de aplicação foram sob o **definições** separador.

- **Conteúdo:**
   - Sites de Enterprise podem carregar o conteúdo não empresariais, tais como o plug-ins de terceiros.
- **Outras:**
    - Manter os dados de browser gerados pelo utilizador
    - Eventos de auditoria de segurança na sessão de proteção de aplicação isolado



## <a name="next-steps"></a>Passos seguintes
Para ler mais sobre a proteção de aplicações do Windows Defender: [Descrição geral do Windows Defender aplicações Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview).
[Proteção de aplicações do Windows Defender FAQ](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard).

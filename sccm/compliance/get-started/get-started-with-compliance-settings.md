---
title: Introdução às definições de compatibilidade
titleSuffix: Configuration Manager
description: Saiba mais sobre conceitos principais e como funcionam as definições de compatibilidade
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
caps.latest.revision: ''
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a8f672d4d92db8f1bd6e19c4a483b5b3107ad703
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="get-started-with-compliance-settings-in-system-center-configuration-manager"></a>Introdução às definições de compatibilidade no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de criar as definições de compatibilidade do Configuration Manager, saiba mais sobre conceitos principais e compreender como funcionam.  



## <a name="how-compliance-settings-work"></a>Como funcionam as definições de compatibilidade  
 As definições de compatibilidade permitem-lhe gerir a configuração e a compatibilidade dos clientes na sua organização.  

 Os itens de configuração enquadram-se em duas categorias principais:  

-   **Definições para dispositivos que são geridos com o cliente do Configuration Manager** - normalmente, dispositivos nos quais instalou software de cliente do Configuration Manager permitem-lhe gerir o dispositivo.  

-   **Definições para dispositivos que são geridos sem o cliente do Configuration Manager** - normalmente, dispositivos que são geridos com o Microsoft Intune ou com a gestão de dispositivos no local do Configuration Manager.  



## <a name="what-devices-are-supported"></a>Quais são os dispositivos suportados?  

| Tipo de Dispositivo | Mais informações |  
|------------|----------------------|  
| PCs Windows (com o cliente do Configuration Manager) | Crie itens de configuração personalizada para avaliar a objetos, tais como chaves de registo, ficheiros e atributos do Active Directory.<br /><br /> Quando utiliza o tipo de item de configuração do Windows 10, selecione as definições numa lista predefinida. |  
| PCs Windows (inscritos com o Microsoft Intune) | Selecione as definições numa lista predefinida. |  
| dispositivos iOS (inscritos com o Microsoft Intune) | Selecione as definições numa lista predefinida. |  
| Dispositivos Android (inscritos com o Microsoft Intune) | Selecione as definições numa lista predefinida. |  
| Dispositivos Windows Phone (inscritos com o Microsoft Intune) | Selecione as definições numa lista predefinida. |  
| Computadores MAC (com o cliente do Configuration Manager) | Crie itens de configuração personalizada para avaliar a objetos, tais como macOS preferências e resultados devolvidos por um script. |  
| Computadores MAC (inscritos com o Microsoft Intune) | Selecione as definições numa lista predefinida. |  



## <a name="what-is-a-configuration-item"></a>O que é um item de configuração?  
 Um item de configuração é um contentor que armazena informações específicas. As informações que configurar dependem do tipo de item de configuração. Itens de configuração podem incluir as seguintes informações:

-   **Informações do método de deteção** é apenas para o Windows itens de configuração que contêm as definições da aplicação. Deteta se uma aplicação é instalada. Esta deteção utiliza o ficheiro do Windows installer para a aplicação ou através de um script personalizado.  

-   **Definições** representam as condições comerciais ou técnicas para avaliar a compatibilidade nos dispositivos cliente. Configurar uma nova definição ou navegar para uma definição existente num computador de referência.  

-   **Regras de compatibilidade** especificar as condições que definem a compatibilidade de uma definição de item de configuração. Antes do cliente avalia uma definição de compatibilidade, tem de ter, pelo menos, uma regra de compatibilidade. Algumas definições remediar os valores não compatíveis. Criar novas regras ou navegar para uma definição existente em qualquer item de configuração e selecionadas regras no mesmo.  

-   **Plataformas suportadas** são as plataformas de dispositivos, definir em que o cliente avalia a compatibilidade dos itens de configuração. Se implementar um item de configuração para um dispositivo que não se encontra na lista de plataformas suportadas, não avaliar a compatibilidade.  



## <a name="what-is-a-configuration-baseline"></a>O que é uma linha de base da configuração?  
 Defina uma linha de base de configuração que inclua os itens de configuração a avaliar. Também pode inclua as definições e regras que descrevem o nível de compatibilidade necessário. Importe estes dados de configuração de pacotes de configuração do Configuration Manager. Microsoft e outros fornecedores definem estes pacotes de configuração. Ou criar novos itens de configuração e linhas de base de configuração.  

 Depois de definir uma linha de base de configuração, implementá-la para o utilizador e coleções de dispositivos. O cliente avalia, em seguida, as definições de linha de base para compatibilidade com base numa agenda. Pode implementar mais do que uma linha de base de configuração para dispositivos. Este granularidade proporciona maior controlo da conformidade. 

 Os dispositivos cliente avaliam a compatibilidade em relação a cada linha de base da configuração implementada e comunicam imediatamente os resultados ao site, utilizando mensagens de estado. Se um dispositivo está atualmente desligado da rede, mas transferir a linha de base de configuração, avalia ainda conformidade dos itens de configuração. Quando voltar a ser ligado, envia as informações de compatibilidade.  

### <a name="monitoring-configuration-baselines"></a>Linhas de base de configuração de monitorização
- Monitorizar os resultados da avaliação de compatibilidade na consola do Configuration Manager, sob o **monitorização** área de trabalho, no **implementações** nó. Por exemplo:
    - Causas comuns de não conformidade
    - Erros
    - O número de dispositivos e utilizadores afectados
- Execute relatórios de definições de compatibilidade com detalhes adicionais. Por exemplo:
    - Os dispositivos que são compatíveis ou incompatíveis
    - O elemento de linha de base de configuração está a causar um computador para estar em não conformidade
- Ver os resultados da avaliação de compatibilidade de computadores com Windows com o cliente do Configuration Manager. Abra o **do Configuration Manager** painel de controlo e mude para o **configurações** separador.  



## <a name="user-data-and-profiles-configuration-items"></a>Itens de configuração de dados e perfis de utilizador  
 Itens de configuração de perfis e dados de utilizador incluem definições que controlam a forma como gerem os utilizadores em computadores que executam o Windows 8 e posterior:  
   - Redirecionamento de pastas
   - Ficheiros offline
   - Perfis itinerantes  

Implemente estes itens de configuração em coleções de utilizadores. Monitorizar a compatibilidade do **monitorização** nós da consola do Configuration Manager. Ao contrário de outros itens de configuração, não adicioná-los para linhas de base de configuração antes de implementá-las. Implementá-las clicando diretamente **implementar** no Friso.  

 Para obter mais informações, consulte [criar itens de configuração de perfis e dados de utilizador](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  



## <a name="remote-connection-profiles"></a>Perfis de ligação remota  
 Os perfis de ligação remota fornecem um conjunto de ferramentas e recursos para ajudar a criar, implementar e monitorizar as definições de ligação remota. Ao implementar estas definições para dispositivos, estará a minimizar o esforço que os utilizadores finais necessitam para ligar os seus computadores à rede empresarial.  

Para obter mais informações, consulte [criar perfis de ligação remota](/sccm/compliance/deploy-use/create-remote-connection-profiles).  



## <a name="windows-edition-upgrade"></a>Atualização de edição do Windows
A política de atualização de edição atualiza automaticamente os dispositivos que executem determinadas versões do Windows 10 para uma edição mais recente. Esta política oferece um novo produto chave de ficheiro ou de licença que consome o dispositivo para atualizar.

Para obter mais informações, consulte [dispositivos de atualizar o Windows com a edição de atualização de política](/sccm/compliance/deploy-use/upgrade-windows-version)



## <a name="microsoft-edge-browser-profiles"></a>Perfis de browser Microsoft Edge
<!-- 1357310 -->
A partir de versão 1802, para os clientes que utilizam o [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) web browser em clientes Windows 10, crie uma política de definições de compatibilidade para configurar várias definições do Microsoft Edge. 

Para obter mais informações, consulte [perfis de browser Microsoft Edge](/sccm/compliance/deploy-use/browser-profiles).


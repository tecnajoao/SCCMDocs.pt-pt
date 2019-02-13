---
title: Introdução às definições de conformidade
titleSuffix: Configuration Manager
description: Saiba mais sobre conceitos-chave e como funcionam as definições de conformidade
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4e85b6886947fe0ac720f5840dcefd91a441d3e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130950"
---
# <a name="get-started-with-compliance-settings-in-system-center-configuration-manager"></a>Introdução às definições de compatibilidade no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de criar as definições de compatibilidade do Configuration Manager, saiba mais sobre conceitos-chave e entender como elas funcionam.  



## <a name="how-compliance-settings-work"></a>Como funcionam as definições de conformidade  
 Definições de compatibilidade permitem-lhe gerir a configuração e a conformidade de clientes na sua organização.  

 Os itens de configuração enquadram-se em duas categorias principais:  

-   **Definições para dispositivos que são geridos com o cliente do Configuration Manager** - normalmente, dispositivos, no qual instalou o software de cliente do Configuration Manager permitem-lhe gerir o dispositivo.  

-   **Definições para dispositivos geridos sem o cliente do Configuration Manager** - normalmente, dispositivos geridos com o Microsoft Intune ou gestão de dispositivos do Configuration Manager no local.  



## <a name="what-devices-are-supported"></a>Quais são os dispositivos suportados?  

| Tipo de Dispositivo | Mais informações |  
|------------|----------------------|  
| PCs Windows (com o cliente do Configuration Manager) | Crie itens de configuração personalizada para avaliar a objetos, tais como chaves de registo, ficheiros e atributos do Active Directory.<br /><br /> Quando utiliza o tipo de item de configuração do Windows 10, selecione as definições de uma lista predefinida. |  
| PCs Windows (inscritos com o Microsoft Intune) | Selecione as definições de uma lista predefinida. |  
| dispositivos iOS (inscritos com o Microsoft Intune) | Selecione as definições de uma lista predefinida. |  
| Dispositivos Android (inscritos com o Microsoft Intune) | Selecione as definições de uma lista predefinida. |  
| Dispositivos Windows Phone (inscritos com o Microsoft Intune) | Selecione as definições de uma lista predefinida. |  
| Computadores MAC (com o cliente do Configuration Manager) | Crie itens de configuração personalizada para avaliar a objetos, como preferências de macOS e os resultados devolvidos por um script. |  
| Computadores MAC (inscritos com o Microsoft Intune) | Selecione as definições de uma lista predefinida. |  



## <a name="what-is-a-configuration-item"></a>O que é um item de configuração?  
 Um item de configuração é um contentor que armazena informações específicas. As informações que configurar dependem do tipo de item de configuração. Itens de configuração podem incluir as seguintes informações:

-   **Informações de método de deteção** é apenas para Windows, os itens de configuração que contêm as definições da aplicação. Detetar se uma aplicação é instalada. Esta deteção utiliza o ficheiro de instalador do Windows para a aplicação ou através de um script personalizado.  

-   **Definições** representam as condições comerciais ou técnicas para avaliar a compatibilidade nos dispositivos cliente. Configurar uma nova definição ou navegar para uma definição existente num computador de referência.  

-   **Regras de conformidade** Especifica as condições que definem a compatibilidade de um item de configuração. Antes do cliente avalia uma definição de conformidade, tem de ter, pelo menos, uma regra de compatibilidade. Algumas definições remediar os valores não conformes. Criar novas regras ou navegar para uma definição existente em qualquer item de configuração e selecionadas as regras no mesmo.  

-   **Plataformas suportadas** são as plataformas de dispositivo, define no qual o cliente avalia a conformidade dos itens de configuração. Se implementar um item de configuração para um dispositivo que não esteja na lista de plataformas suportadas, não avalia a conformidade.  



## <a name="what-is-a-configuration-baseline"></a>O que é uma linha de base da configuração?  
 Defina uma linha de base de configuração que inclui os itens de configuração a avaliar. Também pode inclua as definições e regras que descrevem o nível de compatibilidade necessário. Importe estes dados de configuração de pacotes de configuração do Configuration Manager. Microsoft e outros fornecedores definem estes pacotes de configuração. Ou criar novos itens de configuração e linhas de base de configuração.  

 Depois de definir uma linha de base de configuração, implementá-la e coleções de dispositivos do utilizador. O cliente, em seguida, avalia as definições de linha de base para conformidade com base numa agenda. Pode implementar mais do que uma linha de base de configuração para dispositivos. Este granularidade oferece maior controle de conformidade. 

 Os dispositivos cliente avaliam a compatibilidade em relação a cada linha de base da configuração implementada e comunicam imediatamente os resultados ao site, utilizando mensagens de estado. Se um dispositivo está atualmente desligado da rede, mas transferido a linha de base de configuração, ele ainda avalia a conformidade dos itens de configuração. Envia as informações de compatibilidade quando voltar a ser ligado.  

### <a name="monitoring-configuration-baselines"></a>Linhas de base de configuração de monitorização
- Monitorizar os resultados da avaliação de compatibilidade na consola do Configuration Manager, no **monitorização** área de trabalho, na **implementações** nó. Por exemplo:
    - Causas comuns de não conformidade
    - Erros
    - O número de dispositivos e utilizadores afetados
- Execute relatórios de definições de conformidade com detalhes adicionais. Por exemplo:
    - Os dispositivos que estão em conformidade ou não conformes
    - O elemento de linha de base de configuração está a causar um computador para estar em não conformidade
- Ver resultados de avaliação de compatibilidade dos computadores Windows, o cliente do Configuration Manager. Abra o **Configuration Manager** painel de controlo e mude para o **configurações** separador.  



## <a name="user-data-and-profiles-configuration-items"></a>Itens de configuração de dados e perfis de utilizador  
 Itens de configuração para os dados de utilizador e perfis incluem definições que controlam como gerem os utilizadores em computadores que executam o Windows 8 e posterior:  
   - Redirecionamento de pastas
   - Ficheiros offline
   - Perfis itinerantes  

Implemente esses itens de configuração em coleções de utilizadores. Monitorizar a compatibilidade do **monitorização** nó da consola do Configuration Manager. Ao contrário de outros itens de configuração, não adicioná-los às linhas de base de configuração antes de implementá-las. Implementá-las diretamente ao clicar em **Deploy** na faixa de opções.  

 Para obter mais informações, consulte [criar perfis e dados de utilizador de itens de configuração](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  



## <a name="remote-connection-profiles"></a>Perfis de ligação remota  
 Perfis de ligação remota fornecem um conjunto de ferramentas e recursos para o ajudar a criar, implementar e monitorizar as definições de ligação remota. Ao implementar estas definições para dispositivos, estará a minimizar o esforço do utilizador final necessário para ligar os seus computadores à rede empresarial.  

Para obter mais informações, consulte [criar perfis de ligação remota](/sccm/compliance/deploy-use/create-remote-connection-profiles).  



## <a name="windows-edition-upgrade"></a>Atualização de edição do Windows
A política de atualização de edição atualiza automaticamente os dispositivos que executam algumas versões do Windows 10 para uma edição mais recente. Esta política fornece um novo produto chave ou ficheiro de licença que o dispositivo consuma a atualização.

Para obter mais informações, consulte [dispositivos de atualizar o Windows com a edição de política de atualização](/sccm/compliance/deploy-use/upgrade-windows-version)



## <a name="microsoft-edge-browser-profiles"></a>Perfis de browser do Microsoft Edge
<!-- 1357310 --> A partir da versão 1802, para os clientes que utilizam o [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) web browser em clientes Windows 10, criar uma política de definições de compatibilidade para configurar várias definições do Microsoft Edge. 

Para obter mais informações, consulte [perfis de browser do Microsoft Edge](/sccm/compliance/deploy-use/browser-profiles).


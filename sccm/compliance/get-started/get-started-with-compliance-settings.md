---
title: "Introdução às definições de compatibilidade | Microsoft Docs"
description: "Saiba como as definições de compatibilidade funcionam no System Center Configuration Manager. Também saber mais sobre conceitos principais que terá de conhecer."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
caps.latest.revision: "11"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: b9f997caf5ca4753f95ab2e2cf680bdac40d29b7
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/15/2017
---
# <a name="get-started-with-compliance-settings-in-system-center-configuration-manager"></a>Introdução às definições de compatibilidade no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de começar a criar itens de configuração do System Center Configuration Manager, deve rever este tópico para compreender como funcionam as definições de compatibilidade e para saber mais sobre os conceitos principais que terá de conhecer.  

## <a name="how-compliance-settings-works"></a>Como funcionam as definições de compatibilidade  
 As definições de compatibilidade permitem-lhe gerir a configuração e conformidade de servidores, computadores portáteis, computadores de secretária e dispositivos móveis na sua organização.  

 Os itens de configuração enquadram-se em duas categorias principais:  

-   **Definições para dispositivos que são geridos com o cliente do Configuration Manager** - normalmente, dispositivos nos quais instalou software de cliente do Configuration Manager permitem-lhe gerir o dispositivo.  

-   **Definições para dispositivos que são geridos sem o cliente do Configuration Manager** - normalmente, dispositivos que são geridos com o Microsoft Intune ou com a gestão de dispositivos no local do Configuration Manager.  

## <a name="what-devices-are-supported"></a>Quais são os dispositivos suportados?  


|Tipo de Dispositivo|Mais informações|  
|------------|----------------------|  
|PCs Windows (com o cliente do Configuration Manager)|Permite criar itens de configuração personalizados que permitem avaliar itens, como chaves de registo, ficheiros e atributos do Active Directory.<br /><br /> Ao utilizar o tipo de item de configuração do Windows 10, selecione as definições que pretende numa lista predefinida.|  
|PCs Windows (inscritos com o Microsoft Intune)|Selecione as definições que pretende numa lista predefinida.|  
|dispositivos iOS (inscritos com o Microsoft Intune)|Selecione as definições que pretende numa lista predefinida.|  
|Dispositivos Android (inscritos com o Microsoft Intune)|Selecione as definições que pretende numa lista predefinida.|  
|Dispositivos Windows Phone (inscritos com o Microsoft Intune)|Selecione as definições que pretende numa lista predefinida.|  
|Computadores MAC (com o cliente do Configuration Manager)|Permite criar itens de configuração personalizados que permitem avaliar itens, como os valores de preferência (lista de propriedades) do Mac OS X e os resultados devolvidos por um script.|  
|Computadores MAC (inscritos com o Microsoft Intune)|Selecione as definições que pretende numa lista predefinida.|  

## <a name="what-is-a-configuration-item"></a>O que é um item de configuração?  
 Um item de configuração pode ser considerado como um contentor que armazena as seguintes informações (as informações que configurar irão depender do tipo de item de configuração):  

-   **Informações de método de deteção** (para itens de configuração do Windows que contêm apenas as definições da aplicação) - permite detetar se uma aplicação é instalada através da deteção do ficheiro de instalador do Windows para a aplicação ou através de um script personalizado.  

-   **Definições** - as definições representam as condições empresariais ou técnicas utilizadas para avaliar a compatibilidade nos dispositivos cliente. Pode configurar uma nova definição ou navegar para uma definição existente num computador de referência.  

-   **Regras de compatibilidade** - as regras de compatibilidade especificam as condições que definem a compatibilidade da definição de um item de configuração. Antes de poder ser avaliada a compatibilidade de uma definição, tem de ter, pelo menos, uma regra de compatibilidade. Algumas definições de script permitem remediar os valores considerados não conformes. Pode criar novas regras ou navegar para uma definição existente em qualquer item de configuração para selecionar regras no mesmo.  

-   **Plataformas suportadas** - são as plataformas dos dispositivos onde define que a compatibilidade do item de configuração será avaliada. Se implementar um item de configuração num dispositivo que não esteja na lista de plataformas suportadas, a compatibilidade não será avaliada.  

## <a name="what-is-a-configuration-baseline"></a>O que é uma linha de base da configuração?  
 A compatibilidade é avaliada através da definição de uma linha de base da configuração, que contém os itens de configuração que pretende avaliar e as definições e regras que descrevem o nível de compatibilidade necessário. Pode importar estes dados de configuração da web no Microsoft System Center Configuration Manager pacotes de configuração como melhores práticas que são definidas pela Microsoft e outros fornecedores, no Configuration Manager e que, em seguida, importar para o Configuration Manager. Em alternativa, pode criar novos itens de configuração e linhas de base da configuração.  

 Depois de uma linha de base da configuração estar definida, pode implementá-la em utilizadores e dispositivos através de coleções e avaliar as definições de compatibilidade com base num agendamento. Os dispositivos podem ter várias linhas base de configuração implementadas nos respetivos computadores. Isto permite um elevado nível de controlo.  

 Os dispositivos cliente avaliam a compatibilidade em relação a cada linha de base da configuração implementada e comunicam imediatamente os resultados ao site, utilizando mensagens de estado. Se um dispositivo cliente não estiver atualmente ligado à rede, mas tiver transferido os itens de configuração que são referenciados numa linha de base de configuração implementada, a compatibilidade da linha de base da configuração é avaliada. As informações de compatibilidade são enviadas no restabelecimento de ligação.  

 Pode monitorizar os resultados da compatibilidade da avaliação da linha de base de configuração a **implementações** no nó de **monitorização** área de trabalho na consola do Configuration Manager para visualizar as causas mais comuns de incompatibilidade, erros e o número de utilizadores e dispositivos que são afetados. Também pode executar relatórios de definições de conformidade para localizar detalhes adicionais, como os dispositivos que estão em conformidade ou não conformes, e o elemento de linha de base da configuração que está a tornar um computador não conforme. Pode também ver resultados da avaliação de compatibilidade dos computadores Windows com o software de cliente do Configuration Manager utilizando o **configurações** separador **do Configuration Manager** no painel de controlo.  

## <a name="user-data-and-profiles-configuration-items"></a>Itens de configuração de dados e perfis de utilizador  
 Itens de configuração de perfis e dados de utilizador contêm definições que controlam a forma como os utilizadores na sua hierarquia gerem o redirecionamento de pastas, ficheiros offline e perfis itinerantes em computadores que executam o Windows 8 e posterior. Pode implementá-las em coleções de utilizadores e, em seguida, monitorizar a compatibilidade do **monitorização** nós da consola do Configuration Manager. Ao contrário de outros itens de configuração, estes não são adicionados às linhas de base de configuração antes de implementá-los. Pode implementá-los diretamente com a caixa de diálogo **Implementar Item de Configuração de Dados e Perfis de Utilizador** .  

 Para obter mais informações, consulte [criar itens de configuração de perfis e dados de utilizador](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  

## <a name="remote-connection-profiles"></a>Perfis de ligação remota  
 Os perfis de ligação remota fornecem um conjunto de ferramentas e recursos para o ajudar a criar, implementar e monitorizar as definições de ligação remota para dispositivos na sua organização. Ao implementar essas definições, minimiza o esforço de que os utilizadores finais necessitam para ligarem aos seus computadores na rede da empresa.  

Para obter mais informações, consulte [criar perfis de ligação remota](/sccm/compliance/deploy-use/create-remote-connection-profiles).  

## <a name="windows-edition-upgrade"></a>Atualização de edição do Windows
A política de atualização de edição permite atualizar automaticamente dispositivos que executem determinadas versões do Windows 10 para uma edição mais recente, fornecendo um novo ficheiro de chave ou de licença de produto.

Para obter mais informações, consulte [dispositivos de atualizar o Windows com a edição de atualização de política](/sccm/compliance/deploy-use/upgrade-windows-version)

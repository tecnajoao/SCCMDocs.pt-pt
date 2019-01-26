---
title: Análise de área de trabalho
titleSuffix: Configuration Manager
description: Uma descrição geral do serviço de análise de ambiente de trabalho integrado com o Configuration Manager.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 64bc7e3df4554886544a64d96ecacd310208313b
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55073400"
---
# <a name="what-is-desktop-analytics"></a>O que é a análise de ambiente de trabalho?

> [!Note]  
> Estas informações se relaciona com o serviço de pré-visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft faz não oferece quaisquer garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

A análise de área de trabalho é um serviço baseado na nuvem que se integra com o Configuration Manager. O serviço fornece informações e inteligência para que possa tomar decisões mais informadas sobre a preparação de atualização dos seus clientes Windows e do Office. Ele combina os dados da sua organização com dados agregados de milhões de dispositivos ligados a serviços cloud da Microsoft. 

Utilize a análise de área de trabalho com o Configuration Manager para:  

- Criar um inventário de aplicações em execução na sua organização  

- Avaliar a compatibilidade de aplicação com as últimas atualizações de funcionalidade do Windows 10 e Office 365 ProPlus  

- Identificar problemas de compatibilidade e receber sugestões de atenuação com base nas informações de dados de capacidade de cloud  

- Criar grupos pilotos que representam o estado da aplicação e do controlador inteiro num conjunto mínimo de dispositivos  

- Implementar o Windows 10 e Office 365 ProPlus a dispositivos de pilotos e geridos de produção  

![Captura de ecrã da home page do ambiente de trabalho de análise no portal do Azure](media/portal-home.png)

> [!Note]  
> A análise de área de trabalho é um sucessor do Windows Analytics. O *Windows Analytics* service inclui a preparação de atualizações, a conformidade de atualizações e estado de funcionamento do dispositivo. 
> 
> Todos esses recursos são combinados do *Analytics de ambiente de trabalho* serviço. Análise de área de trabalho também está mais fortemente integrado com o Configuration Manager e inclui o Windows e Office. 



## <a name="benefits"></a>Benefícios

Muitos clientes têm desafios com a introdução e mantendo-se atualizado com o Windows 10 e o Office 365 ProPlus. O principal desafio é o teste de aplicativos. Este processo é normalmente manual. Ele é um processo demorado para os administradores de TI e os proprietários da aplicação analisar continuamente a aplicativos existentes. Em seguida, corrigir quaisquer problemas que surgem. 

Análise de área de trabalho fornece as seguintes vantagens:

- **Inventário de dispositivos e software**: Inventário dos principais fatores, tais como aplicações, suplementos, macros e versões do Office e do Windows.  

- **Criar um piloto de identificação**: Identificação de menor conjunto de dispositivos que fornecem a cobertura mais ampla de fatores. Ele se concentra nos fatores mais importantes para um piloto de atualizações do Windows e do Office e atualizações. Certificar-se de que o projeto piloto estar mais êxito permite-lhe avançar com mais rapidez e confiança para implementações ampla na produção.  

- **A identificação do problema**: Utilizar dados de mercado agregados, juntamente com dados do seu ambiente, o serviço prevê potencial emite para obter e mantendo-se atualizado com o Windows e Office. Em seguida, sugere possíveis atenuações.  

- **Integração do Configuration Manager**: O serviço cloud – possibilita a sua infraestrutura no local existente. Utilize esta análise de dados e para implementar e gerir o Windows e Office nos seus dispositivos.  



## <a name="prerequisites"></a>Pré-requisitos

Para utilizar a análise de ambiente de trabalho, certifique-se de que seu ambiente cumpre os seguintes pré-requisitos. 


### <a name="technical"></a>Técnica

- Uma subscrição do Azure Active Directory  

    - **Administrador de empresa** permissões no Azure  

- Configuration Manager, versão 1810 com update rollup 4486457 ou posterior. Para obter mais informações, consulte [atualizar o Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    - **Administrador total** função no Configuration Manager  

- Dispositivos que executam o Windows 7, Windows 8.1 ou Windows 10  

    - Instale as atualizações mais recentes. Para obter mais informações, consulte [atualizar os dispositivos](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - Dispositivos também tem de ter o cliente do Configuration Manager, versão 1810 com update rollup 4486457 ou posterior. Para obter mais informações, consulte [atualizar o Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

- Dados de diagnóstico do Windows. Para obter mais informações, veja os artigos seguintes:  

    - [Níveis de dados de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)  

    - [Privacidade do ambiente de trabalho do Analytics](/sccm/desktop-analytics/privacy)  

- Conectividade de rede de dispositivos para a nuvem pública da Microsoft. Para obter mais informações, consulte [como ativar a partilha de dados](/sccm/desktop-analytics/enable-data-sharing)  


### <a name="licensing"></a>Licensing

A maioria dos recursos no ambiente de trabalho Analytics não necessitam de quaisquer licenças adicionais ou subscrições. Quando configurado corretamente, uso de análise de ambiente de trabalho não incorrem em quaisquer custos do Azure. 

Para aceder a informações de estado de funcionamento do Windows ou para exportar dados, existem requisitos de licença adicionais. Se não tiver uma das seguintes subscrições, pode ainda configurar e utilizar a análise de ambiente de trabalho, mas não estão licenciados para utilizar as informações de estado de funcionamento do Windows ou para exportar os dados:

- Windows 10 Enterprise ou Windows 10 Education: por dispositivo com Software Assurance ativo  

- Windows 10 Enterprise E3 ou E5: subscrição por dispositivo ou por utilizador (incluída no Microsoft 365 F1, E3 ou E5)  

- Windows 10 Education A3 ou A5 (incluído no Microsoft 365 educação A3 ou A5)  

- Windows Virtual Desktop Access E3 ou E5: por dispositivo da subscrição por utilizador  

> [!Note]  
> Para licenças por dispositivo, não é necessário que ativar cada dispositivo com uma licença. Apenas tem licenças suficientes para dispositivos inscritos no ambiente de trabalho de análise.  


<!-- 
## Top task
> *Optional*  
> *An effective way to structure your overview article is to create an H2 for the top customer tasks and describe how the product/service helps customers with that task.*  
> *Create a new H2 for each task you list.*  
 -->



## <a name="next-steps"></a>Passos seguintes

O tutorial seguinte fornece um guia passo a passo de introdução à análise de ambiente de trabalho e do Configuration Manager:  

- [Implementar o Office 365 para um piloto](/sccm/desktop-analytics/tutorial-office-365)  

<!-- for future
- [Deploy Windows 10 to a pilot](/sccm/desktop-analytics/tutorial-windows)  
-->

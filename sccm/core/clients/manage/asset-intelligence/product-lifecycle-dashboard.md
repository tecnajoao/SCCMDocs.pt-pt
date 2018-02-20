---
title: Dashboard de ciclo de vida do produto
titleSuffix: Configuration Manager
description: "Obter informações sobre o dashboard de ciclo de vida do produto no System Center Configuration Manager."
ms.custom: na
ms.date: 02/13/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: cfc54c1beb92d0102897f77ce3c287cc0ef9e0f4
ms.sourcegitcommit: fbd4a9d2fa8ed4ddd3a0fecc4a2ec4fc0ccc3d0c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/19/2018
---
# <a name="use-the-product-lifecycle-dashboard-to-manage-microsoft-lifecycle-policy-in-system-center-configuration-manager"></a>Utilize o Dashboard de ciclo de vida do produto para gerir a política de ciclo de vida da Microsoft no System Center Configuration Manager

Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Começando com [versão Technical Preview 1802](/sccm/core/get-started/capabilities-in-technical-preview-1802), pode utilizar o dashboard do ciclo de vida do Gestor de configuração do produto. O dashboard apresenta o estado da política de ciclo de vida de produto de Microsoft para produtos da Microsoft instalado nos dispositivos geridos com o Configuration Manager. O dashboard fornece informações sobre os produtos da Microsoft no seu ambiente, o estado de Suportabilidade e datas de fim de suporte. Pode utilizar o dashboard para compreender a disponibilidade de suporte para cada produto. Ajudar a planear quando atualizar produtos da Microsoft utiliza antes do respetivo fim de suporte atual for atingido.  

Para obter mais informações sobre a política de ciclo de vida do produto Microsoft, consulte [Microsoft Lifecycle Policy](https://support.microsoft.com/en-us/lifecycle).

## <a name="prerequisites"></a>Pré-requisitos 

 Para ver dados no dashboard do ciclo de vida do produto, é necessário o seguinte: 
- Internet Explorer 9 ou posterior tem de estar instalado no computador que executa a consola do Configuration Manager. 
- Um ponto do Reporting Services é necessário para a funcionalidade de hiperligação no dashboard, uma vez que possam ligar a um relatório do SQL Server Reporting Services (SSRS). Para obter mais informações, veja [Relatórios no System Center Configuration Manager](/sccm/core/servers/manage/reporting). 
- O ponto de sincronização do Asset Intelligence tem de ser configurado e sincronizado. Para obter mais informações, consulte [configurar do Asset Intelligence no System Center Configuration Manager](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).

Os dados no dashboard dependem do ponto de sincronização do Asset Intelligence instalado. O dashboard utiliza o catálogo do Asset Intelligence como metadados para títulos de produtos. Os metadados são comparados aos dados de inventário na sua hierarquia. 

>[!NOTE]
>Se estiver a configurar o ponto de serviço do Asset Intelligence pela primeira vez, certifique-se de que [ativar classes de inventário de hardware do Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence#BKMK_EnableAssetIntelligence). O dashboard de ciclo de vida está dependente essas classes de inventário de hardware do Asset Intelligence e irão não apresentar dados até que os clientes tenham analisado e devolvido o inventário de hardware.  

## <a name="use-the-microsoft-product-lifecycle-dashboard"></a>Utilize o dashboard de ciclo de vida do Microsoft produto

Com base nos dados de inventário recolhidos a partir de dispositivos geridos, o dashboard apresenta informações sobre todos os produtos atuais. No entanto, as informações apresentadas para sistemas operativos e o SQL Server estão limitadas às seguintes versões:

- Windows Server 2008 e posterior
- Windows XP e posterior
- SQL Server 2008 e posterior

Para aceder ao dashboard do ciclo de vida na consola do Configuration Manager, aceda a **ativos e compatibilidade** > **do Asset Intelligence** > **ciclo de vida do produto** .

>[!NOTE]
>Os dados no dashboard baseia-se na consola do Configuration Manager liga-se ao site. Se a consola liga o site de nível superior, pode ver os dados em toda a hierarquia. Quando estiver ligado a um site primário subordinado, mostra apenas dados a partir desse site.

### <a name="product-lifecycle-dashboard"></a>Dashboard de ciclo de vida do produto

![Dashboard de ciclo de vida do produto](/sccm/core/clients/manage/asset-intelligence/media/product-lifecycle-dashboard.png)

O dashboard tem os seguintes mosaicos: 
- **Principais cinco produtos passado fim-de-vida:** Este mosaico é uma vista de dados consolidado dos produtos já depois do respetivo fim-de-vida encontrado no seu ambiente. O gráfico mostra o software instalado que está expirado quando comparado com o ciclo de vida de suporte para sistemas operativos e produtos de servidor do SQL Server.  
- **Principais cinco produtos prestes a fim de vida:** Este mosaico é uma vista de dados consolidado de produtos que estão prestes a fim de vida nos próximos seis meses encontrados no seu ambiente. O gráfico mostra o software instalado que está dentro de seis meses de fim-de-vida quando comparado com o ciclo de vida de suporte para sistemas operativos e produtos de servidor do SQL Server.
- **Dados de ciclo de vida de produtos instalados:** Este mosaico proporciona uma ideia geral de quando um produto passa de suportado para o estado expirado. O gráfico fornece uma repartição do número de clientes em que o produto está instalado, o estado de disponibilidade de suporte, juntamente com uma ligação para obter mais informações sobre os passos a tomar. As informações seguintes estão incluídas no gráfico:     
    - Suporta o tempo restante
    - Número num ambiente 
    - Data de fim de suporte de base
    - Data de fim do suporte alargado
    - Passos seguintes 

>[!IMPORTANT]
>As informações apresentadas neste dashboard são fornecidas para sua comodidade e apenas para utilização interna na empresa. Não deverá confiar apenas nestas informações para confirmar a compatibilidade. Lembre-se de que verifica a exatidão das informações fornecidas para si, juntamente com a disponibilidade das informações de suporte, visitando https://support.microsoft.com/en-us/lifecycle.

## <a name="reporting"></a>Relatórios
Os novos relatórios seguintes são adicionados sob a categoria **ciclo de vida do produto**:
- **Descrição geral do ciclo de vida de produto de gerais:** Ver uma lista dos ciclos de vida do produto. É possível filtrar a lista por nome de produto e dias de expiração definable pelo utilizador. 
- **Computadores com um produto de software específica:** Ver uma lista de computadores nos quais é detetado um produto especificado.
- **Lista de produtos expiradas encontrado na organização:** Veja detalhes de produtos no seu ambiente que tenham expirado ciclo de vida de datas. 
- **Lista de computadores com produtos expirados na organização:** Computadores de vista que tenham expirado produtos nos mesmos. Pode filtrar este relatório por nome de produto.

## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre instalar ou atualizar o ramo de pré-visualização técnica, consulte [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).  


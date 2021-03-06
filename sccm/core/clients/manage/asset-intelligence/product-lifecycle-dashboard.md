---
title: Dashboard de ciclo de vida do produto
titleSuffix: Configuration Manager
description: Ver a Microsoft Lifecycle Policy com o dashboard de ciclo de vida do produto no Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 716c5218eafaf6297292fdd852589b7327e2ecaa
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120033"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>Gerir política de ciclo de vida da Microsoft com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir da versão 1806, pode utilizar o dashboard de ciclo de vida do produto do Configuration Manager para ver a Policy Lifecycle de Microsoft. O dashboard apresenta o estado da Microsoft Lifecycle Policy para produtos Microsoft instalados nos dispositivos geridos com o Configuration Manager. Ele também fornece informações sobre os produtos da Microsoft no seu ambiente, o estado de capacidade de suporte e datas de término do suporte. Utilize o dashboard para compreender a disponibilidade de suporte para cada produto. Estas informações ajudam a planear quando atualizar os produtos da Microsoft utilizar antes de seu suporte terminará a atual for atingido.  

Para obter mais informações, consulte a [Microsoft Lifecycle Policy](https://support.microsoft.com/lifecycle).

A partir da versão 1810, o dashboard inclui informações para o System Center 2012 Configuration Manager e versões posteriores.<!--1358702-->  



## <a name="prerequisites"></a>Pré-requisitos 

 Para ver dados no dashboard do ciclo de vida do produto, os seguintes componentes são necessários:  

- Internet Explorer 9 ou posterior tem de estar instalado no computador que executa a consola do Configuration Manager.  

- Um ponto do reporting services é necessário para a funcionalidade de hyperlink no dashboard. As ligações do dashboard para relatórios do SQL Server Reporting Services (SSRS). Para obter mais informações, consulte [relatórios no Configuration Manager](/sccm/core/servers/manage/reporting).  

- O ponto de sincronização do asset intelligence tem de ser configurado e sincronizado. O dashboard utiliza o catálogo do asset intelligence como metadados para os títulos dos produtos. Os metadados são comparados aos dados de inventário na sua hierarquia. Para obter mais informações, consulte [configurar o asset intelligence no Configuration Manager](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  

     > [!NOTE]  
     > Se estiver a configurar o ponto de serviço do asset intelligence pela primeira vez, certifique-se de que [ativar classes de inventário de hardware do asset intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence#BKMK_EnableAssetIntelligence). O dashboard do ciclo de vida depende essas classes de inventário de hardware do asset intelligence. O dashboard não são apresentados dados até que os clientes tenham analisado e devolvido o inventário de hardware.  



## <a name="use-the-product-lifecycle-dashboard"></a>Utilize o dashboard de ciclo de vida do produto

Com base nos dados de inventário que do site recolhe dos dispositivos geridos, o dashboard apresenta informações sobre todos os produtos atuais. No entanto, as informações apresentadas para sistemas operativos e o SQL Server estão limitadas às seguintes versões:

- Windows Server 2008 e versões posterior
- Windows XP e versões posteriores
- SQL Server 2008 e versões posterior

Para aceder ao dashboard do ciclo de vida na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho, expanda **Asset Intelligence**e selecione o **dociclodevidadoproduto** nó.

> [!NOTE]  
> Os dados no dashboard baseia-se no site da que consola do Configuration Manager liga-se ao. Se a consola liga ao seu site de nível superior, verá dados para toda a hierarquia. Quando ligado a um site primário subordinado, mostra apenas os dados desse site.

### <a name="product-lifecycle-dashboard"></a>Dashboard de ciclo de vida do produto

![Captura de ecrã do dashboard de ciclo de vida do produto na consola do](media/product-lifecycle-dashboard.png)

Alterar a vista ao selecionar uma das seguintes opções do **categoria de produto** lista:  
- **Todos os**: Ver todos os produtos em conjunto  
- **Windows Client**: Ver versões de sistema operacional cliente Windows  
- **Windows Server**: Ver as versões de SO do servidor do Windows  
- **Base de dados**: Ver versões do SQL Server  
- **O Configuration Manager**: A partir da versão 1810, ver versões do Configuration Manager  

O dashboard tem os seguintes mosaicos:  

- **Principais cinco produtos anteriores a fim de vida**: Este mosaico é uma vista de dados consolidado de produtos encontrado no seu ambiente após a final da vida. O gráfico mostra o software instalado que expirou quando comparado com o ciclo de vida do suporte de sistemas operacionais e produtos do SQL server.  

- **Principais cinco produtos perto do final da vida**: Este mosaico é uma vista de dados consolidado de produtos encontrado no seu ambiente que estão prestes a fim de vida no seguintes dezoito meses. O gráfico mostra o software instalado que está dentro do dezoito meses de fim-de-vida quando comparado com o ciclo de vida do suporte de sistemas operacionais e produtos do SQL server.  

- **Dados de ciclo de vida de produtos instalados**: Este mosaico fornece uma ideia geral de quando um produto faz a transição de suportado para o estado expirado. O gráfico mostra uma análise detalhada do número de clientes em que o produto está instalado, o estado de disponibilidade de suporte e uma ligação para saber mais sobre os passos seguintes para tirar. As seguintes informações estão incluídas no gráfico:     
    - Tempo restante do suporte
    - Número no ambiente 
    - Data de fim do suporte de principal
    - Data de fim do suporte alargado
    - Passos seguintes  

> [!IMPORTANT]  
> As informações apresentadas neste dashboard são fornecidas para sua comodidade e apenas para uso interno na sua empresa. Não deverá confiar apenas nestas informações para confirmar a conformidade. Certifique-se de que verifica a exatidão das informações fornecidas, juntamente com a disponibilidade das informações de suporte ao visitar a [Microsoft Lifecycle Policy](https://support.microsoft.com/lifecycle).  



## <a name="reporting"></a>Relatórios

Relatórios adicionais também estão disponíveis. Na consola do Configuration Manager, vá para o **monitorização** área de trabalho, expanda **Reporting**e expanda **relatórios**. Os novos relatórios seguintes são adicionados na categoria **Asset Intelligence**:  

- **Ciclo de vida 01A – computadores com um produto de software específico**: Ver uma lista de computadores nos quais é detetado um produto especificado.  

- **Ciclo de vida 02A – lista de computadores com produtos na organização de expirado**: Ver os computadores que já passaram da validade produtos nos mesmos. Pode filtrar este relatório por nome de produto.

- **Ciclo de vida 03A – lista de produtos expirados encontrados na organização**: Ver detalhes dos produtos no seu ambiente que já passaram da validade ciclo de vida de datas.  

- **Ciclo de vida 04A – descrição geral do ciclo de vida de produto de geral**: Ver uma lista dos ciclos de vida do produto. Filtre a lista por nome do produto e os dias de expiração.  

- **Ciclo de vida 05A - dashboard de ciclo de vida do produto**: A partir da versão 1810, este relatório inclui informações semelhantes, como o dashboard na consola. Selecione uma categoria para ver a contagem de produtos no seu ambiente e os dias de suporte restantes.  

Para obter mais informações, consulte [lista de relatórios](/sccm/core/servers/manage/list-of-reports#asset-intelligence).<!--SCCMDocs issue 997-->  

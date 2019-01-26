---
title: Ambiente de trabalho privacidade de dados de análise
titleSuffix: Configuration Manager
description: Análise de área de trabalho tem o compromisso de privacidade de dados do cliente
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 0f1bafe2dc6aa33484e7a85010218afbe95f981a
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55073387"
---
# <a name="desktop-analytics-data-privacy"></a>Ambiente de trabalho privacidade de dados de análise

Análise de área de trabalho é totalmente comprometido com a privacidade de dados do cliente, focalizando esses princípios:

- **Transparência:** Iremos documentar totalmente os eventos de diagnóstico do Windows. Reveja-os com equipes de segurança e conformidade da sua empresa. O Visualizador de dados de diagnóstico do Windows permite que veja dados de diagnóstico enviados a partir de um determinado dispositivo. Para obter mais informações, consulte [descrição geral de Visualizador de dados de diagnóstico](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Controlo:** Controlar o nível de dados de diagnóstico para partilhar com a Microsoft. Windows 10, versão 1709, adiciona uma nova política para limitar os dados de diagnóstico melhorados para o mínimo exigido pelo ambiente de trabalho de análise.  

- **Segurança:** Microsoft protege os dados com segurança forte e encriptação.  

- **Confiança:** A Microsoft a análise de área de trabalho suporta [declaração de privacidade](https://privacy.microsoft.com/privacystatement) e [termos de serviço Online](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).  



## <a name="diagnostic-data-flow"></a>Fluxo de dados de diagnóstico

A ilustração seguinte mostra os dados de diagnóstico como fluxos a partir de dispositivos individuais através do serviço de dados de diagnóstico, armazenamento do Azure Log Analytics e a sua área de trabalho do Log Analytics:

![Diagrama que ilustra o fluxo de dados de diagnóstico de dispositivos](media/da-data-flow-v1.png)

1. Inicie sessão no portal do Azure e carregar para análise de ambiente de trabalho. Criar a aplicação do Azure AD para estabelecer ligação com o Configuration Manager. Quando configurar o ambiente de trabalho de análise, vai criar uma área de trabalho do Log Analytics do Azure no local de sua preferência.  

2. Ligar o Configuration Manager e inscrever dispositivos  

    1. Configurar o serviço de cloud de análise de ambiente de trabalho no Configuration Manager com os detalhes da aplicação do Azure AD.  

    2. Em 15 minutos, o Configuration Manager sincroniza coleções de dispositivos e planos de implementações com a análise de ambiente de trabalho. Este processo é repete a cada hora.  

    3. O Configuration Manager define o ID comercial, de nível de dados de diagnóstico e de outras definições para os dispositivos da coleção de destino. Esta configuração especifica os dispositivos a aparecer na sua área de trabalho de análise de ambiente de trabalho.  

    4. Implementar atualizações de compatibilidade para todos os dispositivos de destino. Opcionalmente, implementa o analisador de estado de funcionamento da aplicação e o Office Readiness Toolkit para um conjunto representativo dos dispositivos. Essas ferramentas fornecem mais informações na linha personalizada de aplicativos de negócios e macros do Office.  

3. Os dispositivos enviam dados de diagnóstico para os serviços de gestão de dados de diagnóstico Microsoft para Windows e o Office. Este serviço é hospedado nos Estados Unidos.  

4. Todos os dias, a Microsoft produz um instantâneo de informações com foco em IT. Este instantâneo combina os dados de diagnóstico do Windows e Office pela sua entrada para os dispositivos inscritos. Este processo ocorre no armazenamento transitório, o que é usado somente pela análise de ambiente de trabalho. O armazenamento transitório está alojado em datacenters da Microsoft nos Estados Unidos. Os instantâneos são separados pelo ID comercial.  

5. Os instantâneos, em seguida, são copiados para a área de trabalho do Log Analytics do Azure adequada.  

6. Análise de área de trabalho armazena os dados introduzidos no armazenamento do Azure Log Analytics. Estas configurações incluem planos de implantação e decisões de recurso para atualização e de importância.  


<!-- ![Diagram illustrating flow of diagnostic data from devices](media/wa-data-flow-v1.png)

1. Devices send diagnostic data to the Microsoft Diagnostic Data Management service. This service is hosted in the United States.  

2. Set up and enrollment  

    1. You create an Azure Log Analytics workspace when you set up Desktop Analytics. You choose the location and copy the commercial ID. This ID identifies your workspace.  
    
    2. When you connect Configuration Manager to Desktop Analytics, it sets the commercial ID on the devices in your target collection. This configuration specifies the devices to appear in your workspace.  

3. Each day Microsoft produces a "snapshot" of IT-focused insights for each workspace in the Diagnostic Data Management service.  

4. These snapshots are copied to transient storage, which is only used by Desktop Analytics. The transient storage is hosted in Microsoft data centers in the United States. The snapshots are segregated by commercial ID.  

5. The snapshots are then copied to the appropriate Azure Log Analytics workspace.  

6. Desktop Analytics stores your configurations in Analytics Azure storage. These configurations include deployment plans and asset upgrade decisions.  
-->


## <a name="other-resources"></a>Outros recursos

Para obter mais informações sobre os aspetos de privacidade relacionadas, consulte os artigos seguintes:

- [Windows 10 e o GDPR para tomadores de decisão de TI](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurar dados de diagnóstico do Windows na sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Eventos de dados de diagnóstico de appraiser do Windows 7, Windows 8 e Windows 8.1 e de campos](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Windows 10, versão 1809 básicos nível Windows eventos de diagnóstico e campos](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Windows 10, versão 1709 avançada eventos de dados de diagnóstico e de campos utilizados pelo ambiente de trabalho Analytics](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [Descrição geral do Visualizador de dados de diagnóstico](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Termos de licenciamento e a documentação](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Segurança e privacidade em centros de dados do Microsoft Azure](https://azure.microsoft.com/global-infrastructure/)  

- [Confiança na cloud fidedigna](https://azure.microsoft.com/overview/trusted-cloud/)  

- [Centro de fidedignidade](https://www.microsoft.com/trustcenter)  



## <a name="faq"></a>FAQ

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>Análise de ambiente de trabalho podem ser utilizado sem uma ligação de cliente direto ao serviço de gestão de dados da Microsoft?
Não, todo o serviço com tecnologia Windows dados de diagnóstico, que requer que os dispositivos têm esta conectividade direta.


### <a name="can-i-choose-the-data-center-location"></a>Pode escolher a localização do Datacenter?

Para o Log Analytics do Azure: Sim, quando configurar a análise de ambiente de trabalho e criar a área de trabalho do Log Analytics.

Para o serviço de gestão de dados da Microsoft e análise de armazenamento do Azure: Não, estes dois serviços estão alojados nos Estados Unidos.


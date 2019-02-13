---
title: Sincronizar dados com o Log Analytics
titleSuffix: Configuration Manager
description: Sincronizar dados do Configuration Manager para o Azure Log Analytics.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9b3ba4c5179069e5443beaf1b7f733c797cfd680
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156530"
---
#  <a name="sync-data-from-configuration-manager-to-azure-log-analytics"></a>Sincronizar dados do Configuration Manager para o Azure Log Analytics

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1258052--> Utilize o **Assistente de serviços do Azure** para configurar uma ligação do Configuration Manager para o serviço de cloud do Azure Log Analytics. Esta ligação sincroniza os dados de coleção de dispositivos para o Log Analytics. 

> [!Note]  
> O Configuration Manager não permite esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

> [!TIP]
> A partir do Configuration Manager 1802, o conector do Log Analytics já não é uma funcionalidade de pré-lançamento. Para obter mais informações, consulte [utilizar as funcionalidades de pré-lançamento de atualizações](/sccm/core/servers/manage/pre-release-features).



## <a name="prerequisites-for-the-log-analytics-connector"></a>Pré-requisitos para o conector do Log Analytics

> [!Note]  
> Este artigo refere-se para o *conector do Log Analytics*, que era anteriormente denominado o *conector OMS*. Não existe nenhuma diferença funcional. Para obter mais informações, consulte [gestão do Azure - monitorização](https://docs.microsoft.com/azure/monitoring/#operations-management-suite).  

- Antes de instalar o conector do Log Analytics no Configuration Manager, forneça o Configuration Manager com permissões. Concessão *acesso de contribuinte* para o Azure *grupo de recursos* que contém a área de trabalho do Log Analytics. Para obter mais informações, consulte [fornecer o Configuration Manager com permissões para o Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics).  

- Instalar o conector do Log Analytics no computador que aloja o [ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) no modo online.  

- Instale um agente de monitorização da Microsoft para o Log Analytics no ponto de ligação de serviço com o conector. Configure este agente e o conector para utilizar a mesma área de trabalho do Log Analytics. Para obter mais informações sobre como instalar este agente, consulte [transfira e instale o agente](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent).  

- Depois de instalar o conector e o agente, configure o Log Analytics a utilizar dados do Configuration Manager. Para obter mais informações, consulte [coleções do Gestor de configuração da importação](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections).  



## <a name="configure-the-connection-to-log-analytics"></a>Configurar a ligação para o Log Analytics

Utilize o **Assistente de serviços do Azure** para configurar uma ligação do Configuration Manager para o serviço de cloud do Azure Log Analytics. Para obter mais informações e detalhes desse processo, consulte [dos serviços do Azure configurar](https://docs.microsoft.com/sccm/core/servers/deploy/configure/azure-services-wizard). Selecione a opção no Assistente para o **conector OMS**. 

> [!Note]  
> Este artigo refere-se para o *conector do Log Analytics*, que era anteriormente denominado o *conector OMS*. Não existe nenhuma diferença funcional. Para obter mais informações, consulte [gestão do Azure - monitorização](https://docs.microsoft.com/azure/monitoring/#operations-management-suite).  

Se fizemos todos os outros procedimentos com êxito, em seguida, as informações sobre o **configuração da ligação** ecrã é apresentado automaticamente depois de importar a aplicação web. Informações para as definições de ligação devem ser apresentado em sua **subscrição do Azure**, **grupo de recursos do Azure**, e **área de trabalho do Operations Management Suite**.

O assistente liga ao serviço do Log Analytics utilizando as informações que tenha de entrada. Selecione as coleções de dispositivos que pretende sincronizar com o serviço em nuvem e, em seguida, clique em **adicionar**.


## <a name="verify-the-connector-properties"></a>Verifique as propriedades do conector

Depois de ligar o Configuration Manager ao Log Analytics, ver as propriedades da ligação para adicionar ou remover coleções. 

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **serviços Cloud**e selecione o **dos serviços do Azure** nó.  

2. Selecione a ligação do Log Analytics. No Friso, selecione **propriedades**.  

A página de propriedades tem os seguintes dois separadores:  

#### <a name="azure-active-directory"></a>Azure Active Directory
Este separador mostra os seguintes atributos: 
- **Tenant**  
- **ID de cliente**  
- **Expiração da chave secreta do cliente**  

Certifique-se também de que a chave secreta do cliente expira.

#### <a name="connection-properties"></a>Propriedades de ligação
Este separador mostra os seguintes atributos: 
- **Subscrição do Azure**  
- **Grupo de recursos do Azure**  
- **Área de trabalho do log Analytics**  

Ela também mostra a lista de **coleções de dispositivos**. Utilize o **Add** e **remover** botões para modificar as coleções a sincronizar.

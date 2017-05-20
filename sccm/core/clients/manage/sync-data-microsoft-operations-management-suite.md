---
title: "Sincronizar dados | Documentos do Microsoft | O conjunto de aplicações do Microsoft Operations gestão "
description: "Sincronizar dados do System Center Configuration Manager para o conjunto de aplicações do Microsoft Operations gestão."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: 9
author: arob98
ms.author: angrobe
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 3acfaa2cf8c64ece5cef65b80372067336d6a815
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---


# <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Sincronizar os dados do Configuration Manager para o conjunto de aplicações de gestão do Microsoft Operations


*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar o conector do Microsoft Operations gestão Suite (OMS) para sincronizar os dados, tais como coleções a partir do System Center Configuration Manager para análise do registo OMS no Microsoft Azure. Isto torna visíveis na OMS dados de implementação do Configuration Manager.
> [!TIP]
> O conector OMS é uma funcionalidade pré-lançamento. Para obter mais informações, consulte o artigo [utilizar funcionalidades de pré-lançamento das atualizações da](/sccm/core/servers/manage/pre-release-features).

A partir da versão 1702, pode utilizar o conector OMS para ligar a uma área de trabalho OMS que se encontra na nuvem do Microsoft Azure para a administração pública. Isto requer que a modificar um ficheiro de configuração antes de instalar o conector OMS. Consulte o artigo [utilizar o conector OMS com a nuvem do Azure para a administração pública](#fairfaxconfig) neste tópico.

## <a name="prerequisites"></a>Pré-requisitos
- Antes de instalar o conector OMS no Configuration Manager, tem de fornecer do Configuration Manager com permissões para OMS. Especificamente, tem de conceder *acesso contribuinte* para o Azure *grupo de recursos* que contém a área de trabalho OMS registo Analytics. Os procedimentos para fazê-lo estão documentados no conteúdo de análise de registo. Consulte o artigo [fornecer do Configuration Manager com permissões para OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) na documentação do OMS.

- O conector OMS tem de estar instalado no computador que aloja um [ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) que está a [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

  Se ligou OMS a um site primário autónomo e pretende adicionar um site de administração central ao seu ambiente, tem de eliminar a ligação atual e, em seguida, reconfigure o conector no novo site de administração central.

- Tem de instalar um agente de monitorização da Microsoft para OMS instalado no ponto de ligação de serviço juntamente com o conector OMS.  O agente e o conector OMS tem de ser configurados para utilizar o mesmo **OMS área de trabalho**. Para instalar o agente, consulte o artigo [transferir e instalar o agente](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) na documentação do OMS.

- Depois de instalar o conector e o agente, tem de configurar OMS para utilizar dados do Configuration Manager.  Para fazê-lo, no Portal do OMS [coleções importação Configuration Manager](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections).



## <a name="install-the-oms-connector"></a>Instalar o conector OMS  
1. Na consola do Configuration Manager, configure o [hierarquia para utilizar funcionalidades da versão de pré-lançamento](/sccm/core/servers/manage/pre-release-features)e, em seguida, ativar a utilização do conector OMS.  

2. Em seguida, aceda ao **administração** > **serviços em nuvem** > **OMS conector**. No Friso, clique em "Criar ligação ao conjunto de aplicações de gestão de operações". Esta ação abre o **ligação ao Assistente de conjunto de aplicações de gestão de operação**. Selecione **seguinte**.  


3.    No **geral** página, confirme que tem as seguintes informações, então selecione **seguinte**.  
  - Registado do Configuration Manager como uma ferramenta de gestão "Web aplicação and/or Web API" e que tem o [ID de cliente a partir deste registo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).  
  - Criar uma chave de cliente para a ferramenta de gestão registado no Azure Active Directory.  

  - No Portal de gestão do Azure, fornecidos da aplicação web registado com permissão para aceder à OMS, conforme descrito em [fornecer do Configuration Manager com permissões para OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms).  

4.    No **do Azure Active Directory** página, configure as definições de ligação para OMS, fornecendo o **inquilino**, **ID de cliente**, e **chave de segredo do cliente**, em seguida, selecione **seguinte**.  

5.    No **configuração da ligação OMS** página, indique as definições de ligação preenchendo a sua **subscrição do Azure**, **grupo de recursos Azure**, e **área de trabalho de conjunto de aplicações de gestão de operações**.  A área de trabalho tem de corresponder à área de trabalho que está configurada para o agente de gestão da Microsoft que está instalado no ponto de ligação de serviço.  

6.    Verifique as definições de ligação no **resumo** página, em seguida, selecione **seguinte**. O **progresso** página irá mostrar o estado da ligação, em seguida, deve **concluída**.

Depois de ligação do Configuration Manager a OMS, pode adicionar ou remover coleções e ver as propriedades da ligação OMS.

## <a name="verify-the-oms-connector-properties"></a>Verifique se as propriedades do conector OMS
1.    Na consola do Configuration Manager, aceda a **administração** > **serviços em nuvem**e, em seguida, selecione **OMS conector** para abrir o **OMS ligação * * página**.
2.    Dentro desta página, existem dois separadores:
  - **Do Azure Active Directory:**   
    Este separador mostra o **inquilino**, **ID de cliente**, **expiração de chave secreta cliente**, e permite-lhe verificar a sua chave de segredo do cliente expirou.

  - **Propriedades da ligação OMS:**  
    Este separador mostra o **subscrição do Azure**, **grupo de recursos Azure**, **área de trabalho do Operations Management Suite**e uma lista de **coleções de dispositivos que o conjunto de aplicações do Operations Management pode obter dados para**. Utilize o **adicionar** e **remover** botões para modificar as coleções são permitidos.

## <a name="fairfaxconfig"></a> Utilizar o conector OMS com a nuvem do Azure para a administração pública


1.  Em qualquer computador que tenha a consola do Configuration Manager instalada, edite o ficheiro de configuração seguinte para apontar para a nuvem para a administração pública:  ***&lt;Caminho de instalação do CM > \AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **Edições:**

    Altere o valor para o nome da definição *FairFaxArmResourceID* para ser igual a "https://management.usgovcloudapi.net/"

   - **Original:** 
      &lt;nome da definição = serializeAs "FairFaxArmResourceId" = "Cadeia" >   
      &lt;valor > &lt; /value >   
      &lt;/ definição >

   - **Editadas:**     
      &lt;nome da definição = serializeAs "FairFaxArmResourceId" = "Cadeia" > &lt;valor > https://management.usgovcloudapi.net/ &lt; /value >  
      &lt;/ definição >

  Altere o valor para o nome da definição *FairFaxAuthorityResource* para ser igual a "https://login.microsoftonline.com/"

  - **Original:** &lt;nome da definição = serializeAs "FairFaxAuthorityResource" = "Cadeia" >   
    &lt;valor > &lt; /value >

    - **Editadas:** &lt;nome da definição = serializeAs "FairFaxAuthorityResource" = "Cadeia" >   
    &lt;valor > https://login.microsoftonline.com/ &lt; /value >

2.    Depois de guardar o ficheiro com as alterações de dois, reiniciar a consola do Configuration Manager no mesmo computador e, em seguida, utilize essa consola para instalar o conector OMS. Para instalar o conector, utilize as informações no [sincronizar dados do Configuration Manager para o conjunto de aplicações de gestão do Microsoft Operations](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)e selecione o **área de trabalho do Operations Management Suite** que esteja na nuvem do Microsoft Azure para a administração pública.

3.    Após instala o conector OMS, a ligação para a nuvem para a administração pública está disponível quando utiliza qualquer consola que liga ao site.


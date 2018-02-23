---
title: 'Sincronizar os dados no Microsoft Operations Management Suite '
titleSuffix: Configuration Manager
description: Sincronizar os dados do System Center Configuration Manager no Microsoft Operations Management Suite.
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: 
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 5cb0ffd29f1b3de110101093a6644335a8167108
ms.sourcegitcommit: 45ff3ffa040eada5656b17f47dcabd3c637bdb60
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/23/2018
---
#  <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Sincronizar os dados do Configuration Manager para o Microsoft Operations Management Suite

Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar o **Assistente de serviços do Azure** para configurar a ligação do Configuration Manager para o serviço de nuvem do Operations Management Suite (OMS). O assistente a partir da versão 1706, substitui o anteriores fluxos de trabalho para configurar esta ligação. Para versões anteriores, consulte [sincronizar os dados do Configuration Manager para o Microsoft Operations Management Suite (1702 e anterior)](#Sync-data-from-Configuration-Manager-to-the-Microsoft-Operations-Management-Suite-(1702-and-earlier)).

-   O assistente é utilizado para configurar os serviços em nuvem para o Configuration Manager, como o OMS, Microsoft Store para empresas e no Azure Active Directory (Azure AD).  

-   O Configuration Manager liga-se ao OMS para funcionalidades como [Log Analytics](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite), ou [atualizar preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics).

## <a name="prerequisites-for-the-oms-connector"></a>Pré-requisitos para o conector do OMS
Pré-requisitos para configurar uma ligação ao OMS são iguais às [documentados para a versão do ramo atual 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites). Essas informações são repetidas aqui:  

-   Antes de instalar o conector do OMS no Configuration Manager, tem de fornecer do Configuration Manager com permissões ao OMS. Especificamente, tem de conceder *acesso contribuinte* para o Azure *grupo de recursos* que contém a área de trabalho de análise de registos do OMS. Os procedimentos para fazê-lo estão documentados no conteúdo de análise de registos. Consulte [fornecer do Configuration Manager com permissões para OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) na documentação do OMS.

-   O conector do OMS tem de estar instalado no computador que aloja um [ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) que está a ser [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

-   Tem de instalar um agente de monitorização da Microsoft para OMS instalado no ponto de ligação de serviço juntamente com o conector do OMS. O agente e o conector do OMS tem de ser configurados para utilizar o mesmo **área de trabalho OMS**. Para instalar o agente, consulte [transferir e instalar o agente](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) na documentação do OMS.
-   Depois de instalar o conector e o agente, tem de configurar o OMS para utilizar os dados do Configuration Manager. Para tal, no Portal do OMS, [Gestor de configuração importar coleções](/azure/log-analytics/log-analytics-sccm#import-collections).

## <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Utilize o Assistente de serviços do Azure para configurar a ligação ao OMS

1.  Na consola, aceda a **administração** > **descrição geral** > **serviços em nuvem** > **serviços do Azure**e, em seguida, escolha **configurar os serviços do Azure** do **home page** separador do Friso, para iniciar o **Assistente de serviços do Azure**.

2.  No **serviços do Azure** página, selecione o serviço de nuvem operação Management Suite. Forneça um nome amigável para o **nome do serviço do Azure** e uma descrição opcional e, em seguida, clique em **seguinte**.

3.  No **aplicação** página, especifique o seu ambiente do Azure (technical preview suporta apenas na nuvem pública). Em seguida, clique em **procurar** para abrir a janela de aplicação de servidor.

4.  Selecione uma aplicação web:

    -   **Importar**: Para utilizar uma aplicação web que já existe na sua subscrição do Azure, clique em **importação**. Forneça um nome amigável para a aplicação e de inquilino e, em seguida, especifique o ID do inquilino, ID de cliente e a chave secreta para a aplicação web do Azure que pretende utilizar o Configuration Manager. Depois de **verifique** informações, clique em **OK** para continuar.   

    > [!NOTE]   
    > Quando configura o OMS com esta pré-visualização, OMS só suporta o *importar* função para uma aplicação web. Criar uma nova aplicação web não é suportada. Da mesma forma, não é possível reutilizar uma aplicação existente para OMS.

5.  Se lhe conseguido todos os outros procedimentos com êxito, em seguida, as informações no **configuração da ligação OMS** ecrã serão apresentadas automaticamente nesta página. As informações para as definições de ligação devem aparecer para sua **subscrição do Azure**, **grupo de recursos do Azure**, e **área de trabalho do Operations Management Suite**.

6.  O assistente liga ao serviço do OMS utilizando as informações que tenha de entrada. Selecione as coleções de dispositivos que pretende sincronizar com o OMS e, em seguida, clique em **adicionar**.

7.  Verifique as definições de ligação no **resumo** ecrã, em seguida, selecione **seguinte**. O **progresso** ecrã mostra o estado da ligação, em seguida, deve **concluída**.

8.  Depois de concluir o assistente, a consola do Configuration Manager mostra que configurou **operação Management Suite** como um **o tipo de serviço de nuvem**.

## <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite-1702-and-earlier"></a>Sincronizar os dados do Configuration Manager para o Microsoft Operations Management Suite (1702 e anterior)


Aplica-se a: System Center Configuration Manager (versões anteriores e 1702)*

Pode utilizar o conector do Microsoft Operations Management Suite (OMS) para sincronizar os dados, tais como as coleções do System Center Configuration Manager para análise de registos do OMS no Microsoft Azure. Isto torna visíveis na OMS dados da implementação do Configuration Manager.
> [!TIP]
> O conector do OMS é uma funcionalidade de pré-lançamento. Para obter mais informações, consulte [utilizar as funcionalidades de pré-lançamento das atualizações da](/sccm/core/servers/manage/pre-release-features).

A partir da versão 1702, pode utilizar o conector do OMS para ligar a uma área de trabalho do OMS que não está na nuvem do Microsoft Azure Government. Isto requer a modificar um ficheiro de configuração antes de instalar o conector do OMS. Consulte [utilizar o conector do OMS com a nuvem do Azure Government](#fairfaxconfig) neste tópico.

### <a name="prerequisites"></a>Pré-requisitos
- Antes de instalar o conector do OMS no Configuration Manager, tem de fornecer do Configuration Manager com permissões ao OMS. Especificamente, tem de conceder *acesso contribuinte* para o Azure *grupo de recursos* que contém a área de trabalho de análise de registos do OMS. Os procedimentos para fazê-lo estão documentados no conteúdo de análise de registos. Consulte [fornecer do Configuration Manager com permissões para OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) na documentação do OMS.

- O conector do OMS tem de estar instalado no computador que aloja um [ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) que está a ser [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

  Se tiver estabelecido ligação OMS a um site primário autónomo e se pretende adicionar um site de administração central ao seu ambiente, tem de eliminar a ligação atual e, em seguida, reconfigurar o conector no novo site de administração central.

- Tem de instalar um agente de monitorização da Microsoft para OMS instalado no ponto de ligação de serviço juntamente com o conector do OMS.  O agente e o conector do OMS tem de ser configurados para utilizar o mesmo **área de trabalho OMS**. Para instalar o agente, consulte [transferir e instalar o agente](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) na documentação do OMS.

- Depois de instalar o conector e o agente, tem de configurar o OMS para utilizar os dados do Configuration Manager.  Para tal, no Portal do OMS, [Gestor de configuração importar coleções](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections).



### <a name="install-the-oms-connector"></a>Instalar o conector do OMS  
1. Na consola do Configuration Manager, configure o [hierarquia a utilizar funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features)e, em seguida, ativar a utilização do conector do OMS.  
0
2. Em seguida, vá para o **administração** > **serviços em nuvem** > **OMS conector**. No Friso, clique em "Criar a ligação ao Operations Management Suite". Esta ação abre o **ligação ao Assistente de operação Management Suite**. Selecione **seguinte**.  


3.  No **geral** página, confirme que tem as seguintes informações e selecione **seguinte**.  
  - Registado do Configuration Manager como uma ferramenta de gestão "Aplicação Web e/ou API Web" e que tem o [ID de cliente deste registo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).  
  - Criar uma chave de cliente para a ferramenta de gestão registado no Azure Active Directory.  

  - No Portal de gestão do Azure, fornecida a aplicação web registado com permissão para aceder à OMS, conforme descrito em [fornecer do Configuration Manager com permissões para OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms).  

4.  No **do Azure Active Directory** página, configure as definições de ligação para o OMS, fornecendo o **inquilino**, **ID de cliente**, e **chave secreta do cliente**, em seguida, selecione **seguinte**.  

5.  No **configuração da ligação OMS** , indique as definições de ligação ao preencher a **subscrição do Azure**, **grupo de recursos do Azure**, e **área de trabalho do Operations Management Suite**.  A área de trabalho tem de corresponder à área de trabalho que está configurada para o agente de gestão da Microsoft que está instalado no ponto de ligação de serviço.  

6.  Verifique as definições de ligação no **resumo** página, em seguida, selecione **seguinte**. O **progresso** página irá mostrar o estado da ligação, em seguida, deve **concluída**.

Depois de ligação do Configuration Manager para OMS, pode adicionar ou remover coleções e ver as propriedades da ligação OMS.

### <a name="verify-the-oms-connector-properties"></a>Verifique as propriedades de conector do OMS
1.  Na consola do Configuration Manager, vá para **administração** > **serviços em nuvem**e, em seguida, selecione **OMS conector** para abrir o **OMS Página de ligação**.
2.  Dentro desta página, existem dois separadores:
  - **Azure Active Directory:**   
    Este separador mostra o **inquilino**, **ID de cliente**, **expiração chave secreta de cliente**, e permite-lhe verificar a chave secreta de cliente expirou.

  - **Propriedades de ligação do OMS:**  
    Este separador mostra o **subscrição do Azure**, **grupo de recursos do Azure**, **área de trabalho do Operations Management Suite**e uma lista de **coleções de dispositivos que o Operations Management Suite pode obter os dados para**. Utilize o **adicionar** e **remover** botões para modificar as coleções são permitidos.

### <a name="fairfaxconfig"> </a> Utilizar o conector do OMS com a nuvem do Azure Government


1.  Em qualquer computador que tenha a consola do Configuration Manager instalada, edite o ficheiro de configuração seguintes para apontar para a nuvem pública:  ***&lt;Caminho de instalação do CM > \AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **Edições:**

    Altere o valor para o nome da definição *FairFaxArmResourceID* para ser igual a "https://management.usgovcloudapi.net/"

   - **Original:** &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
      &lt;value>&lt;/value>   
      &lt;/setting>

   - **Editadas:**     
      &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value>https://management.usgovcloudapi.net/&lt;/value>  
      &lt;/setting>

  Altere o valor para o nome da definição *FairFaxAuthorityResource* para ser igual a "https://login.microsoftonline.us/"

  - **Original:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>&lt;/value>

    - **Editadas:** &lt;nome da definição = "FairFaxAuthorityResource" serializeAs = "Cadeia" >   
    &lt;value>https://login.microsoftonline.us/&lt;/value>

2.  Depois de guardar o ficheiro com as duas alterações, reiniciar a consola do Configuration Manager no mesmo computador e, em seguida, utilize essa consola para instalar o conector do OMS. Para instalar o conector, utilize as informações em [sincronizar os dados do Configuration Manager para o Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)e selecione o **área de trabalho do Operations Management Suite** que não está na nuvem do Microsoft Azure Government.

3.  Depois de instala o conector do OMS, a ligação para a nuvem do Governo dos EUA está disponível quando utiliza qualquer consola que liga ao site.

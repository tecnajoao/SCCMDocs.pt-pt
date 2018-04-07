---
title: Preparação para a atualização
titleSuffix: System Center Configuration Manager
description: Integre com o Configuration Manager de preparação de atualização. Aceder a dados de compatibilidade da atualização na consola do administrador. Dispositivos de destino para a atualização ou correção.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology:
- configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 96f20c3559ac08cb4c5a16d1d33b74c63a02e4b7
ms.sourcegitcommit: f0bfd9fa0ec5b416f0ea2beee889b94e2ad9c97d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/06/2018
---
# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>Integrar a preparação de atualização com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Preparação de atualização (anteriormente, análise de atualização) é uma parte [Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics) que lhe permite avaliar e analisar a preparação de dispositivos no seu ambiente para uma atualização para o Windows 10. Pode configurar a versão específica. Preparação de atualização pode ser integrada com o Configuration Manager para aceder aos dados de compatibilidade de atualização de cliente na consola de administração do Configuration Manager. Conseguir dispositivos de destino para a atualização ou remediação utilizando dinâmicas coleções criadas com base nos dados.

Preparação de atualização é uma solução que é executado no [Operations Management Suite (OMS)](/azure/operations-management-suite/operations-management-suite-overview). Pode ler mais sobre a preparação de atualização no [gerir o Windows atualiza com atualização preparação](/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness).

<!--
>[!WARNING]
>For Upgrade Readiness to function within Configuration Manager, you must upgrade to Configuration Manager version 1802. The Upgrade Readiness Connector will no longer function in Configuration Manager versions earlier than 1802. 
SMS.507205 Pulled 4/5/18 -->


## <a name="configure-clients"></a>Configurar os clientes

Preparação de atualização, como todas as soluções de análise do Windows, baseia-se em dados de telemetria do Windows. Ordem de atualizar a preparação receber dados de telemetria suficiente, devem ser satisfeitos os seguintes pré-requisitos:

- Todos os clientes têm de ser configurados com um **comercial chave de ID**. 
- Clientes Windows 10 têm de ter configurada para comunicar a telemetria de nível básica, pelo menos, a telemetria.
-  Os clientes com versões anteriores no Windows tem de ter instalado de KBs específicos conforme descrito em [começar a atualizar preparação](/windows/deployment/upgrade/upgrade-readiness-get-started#deploy-the-compatibility-update-and-related-kbs). Também têm de ter telemetria ativada no **as definições de cliente**.

Chave de ID comercial e telemetria do Windows podem ser configuradas no **as definições de cliente**. Para obter mais informações, consulte [utilize Windows Analytics com o Configuration Manager](../monitor-windows-analytics.md).

>[!NOTE]
>Se ocorrerem problemas com a preparação de atualização não receber dados de telemetria dos dispositivos no seu ambiente, conforme esperado, em seguida, alguns destes problemas podem ser resolvidos utilizando o [script de implementação de preparação de atualização](/windows/deployment/upgrade/upgrade-readiness-deployment-script). No entanto, na maioria dos ambientes, implementar KBs corretos, configurar comercial chave de ID e a telemetria no **as definições de cliente** deve ser suficiente.

## <a name="connect-configuration-manager-to-upgrade-readiness"></a>Ligar a preparação para a atualização do Configuration Manager

A partir da versão do ramo atual 1706, o [Assistente de serviços do Azure](../../../servers/deploy/configure/azure-services-wizard.md) é utilizado para simplificar o processo de configuração de serviços do Azure a utilizar com o Configuration Manager. Para ligar o Configuration Manager com um registo de aplicações do Azure AD do tipo do atualizar preparação *aplicação Web / API* tem de ser criada no [portal do Azure](https://portal.azure.com). Para ler mais informações sobre como criar um registo de aplicação, consulte [registar a aplicação com o seu inquilino do Azure Active Directory](/azure/active-directory/active-directory-app-registration). No **portal do Azure**, também terá de conceder a sua aplicação web recentemente registado *contribuinte* permissões no grupo de recursos que contém a área de trabalho do OMS que aloja os seus dados de preparação de atualização. O **Assistente de serviços do Azure** irá utilizar este registo de aplicação para permitir que o Configuration Manager para comunicar de forma segura com o Azure AD e liga a infraestrutura para os dados de preparação de atualização.

>[!IMPORTANT]
>*Contribuidor* devem ser concedidas permissões para a aplicação, por oposição a uma identidade de utilizador do Azure AD. Isto acontece porque é a aplicação registada e não um utilizador do Azure AD que acede os dados em nome da sua infraestrutura do Configuration Manager. Para conceder as permissões, terá de procurar o nome do registo de aplicação no **adicionar utilizadores** área ao atribuir a permissão. O mesmo processo que tem de ser seguido quando [fornecer do Configuration Manager permissões ao OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) para ligações ao [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm). Estes passos devem ser concluídos antes do registo de aplicação é importado para o Configuration Manager com o *Assistente de serviços do Azure*.

### <a name="use-the-azure-wizard-to-create-the-connection"></a>Utilize o Assistente do Azure para criar a ligação

Siga as instruções em [serviços do Azure configurar para utilização com o Configuration Manager](../../../servers/deploy/configure/azure-services-wizard.md) para criar uma ligação a preparação de atualização ao importar o registo de aplicação web que criou acima. 

No *configuração* página, os são os seguintes valores pré-preenchidos se a importação de aplicação web foi concluída com êxito e as permissões corretas são atribuídas no **portal do Azure**. 
-  Subscrições do Azure
-  Grupo de recursos do Azure
-  Área de trabalho de análise do Windows

Mais do que um grupo de recursos ou a área de trabalho estará disponível apenas se o Azure AD registado aplicação web tem *contribuinte* permissões em mais do que um grupo de recursos ou se o grupo de recursos selecionado tem mais do que uma área de trabalho do OMS.
 
## <a name="view-and-use-upgrade-readiness-information-in-configuration-manager"></a>Ver e utilizar informações de preparação de atualização no Configuration Manager

Depois de ter integrado preparação de atualização com o Configuration Manager, pode ver a análise de preparação de atualização dos clientes.

1. Na consola do Configuration Manager, escolha **monitorização** > **descrição geral** > **atualizar preparação**.
2. Reveja os dados, que incluem o estado de preparação de atualização e a percentagem de dispositivos do Windows que estão a denunciar telemetria.
3. Pode filtrar o dashboard para ver os dados para dispositivos em coleções específicas.
4. Pode ver os dispositivos num estado específico de preparação e criar uma coleção dinâmica para os dispositivos para que possa atualizar esses dispositivos se pronto ou, tome medidas para remedias dispositivos que estão bloqueados no atualizar.

## <a name="using-the-upgrade-readiness-connector-version-1702-and-earlier"></a>Utilizar o conector de preparação atualizar (versão 1702 e anterior)

No Configuration Manager versão 1702 ou anterior, um conjunto diferente de passos e requisitos são necessários para criar uma ligação a preparação de atualização.

### <a name="prerequisites"></a>Pré-requisitos

- Para poder adicionar a ligação, o ambiente do Configuration Manager primeiro tem de configurar um [ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) num [modo online](https://azure.microsoft.com/documentation/articles/resource-group-create-service-principal-portal/). Quando adicionar a ligação ao seu ambiente, este irá também instalar o Microsoft Monitoring Agent no computador que executa esta função de sistema de sites.
- Registe o Configuration Manager como uma ferramenta de gestão "Aplicação Web e/ou API Web" e obter o [ID de cliente deste registo](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Crie uma chave de cliente para a ferramenta de gestão registado no Azure Active Directory.
- No portal do Azure, forneça a aplicação web registado com permissão para aceder à OMS, conforme descrito em [fornecer do Configuration Manager com permissões para OMS](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

    > [!IMPORTANT]
    > Quando configurar permissões para aceder à OMS, lembre-se de que escolha o **contribuinte** função e atribua-lhe as permissões para o grupo de recursos da aplicação registada.

### <a name="create-the-connection"></a>Criar a ligação

1.  Na consola do Configuration Manager, escolha **administração** > **serviços em nuvem** > **conector de preparação de atualização** > **criar ligação para atualizar análise** para iniciar o **Adicionar Assistente de ligação de análise de atualização**.
3.  No **do Azure Active Directory** ecrã, forneça **inquilino**, **ID de cliente**, e **chave secreta do cliente**, em seguida, selecione **seguinte**.
4.  No **atualizar preparação** ecrã, forneça as definições de ligação ao preencher a **subscrição do Azure**, **grupo de recursos do Azure**, e **área de trabalho do Operations Management Suite**.
5.  Verifique as definições de ligação no **resumo** ecrã, em seguida, selecione **seguinte**.

    > [!NOTE]
    > Preparação de atualização tem de ligar para o site de nível superior na sua hierarquia. Se ligar a preparação de atualização para um site primário autónomo e, em seguida, adicionar um site de administração central ao seu ambiente, tem de eliminar e recriar a ligação do OMS dentro da nova hierarquia.

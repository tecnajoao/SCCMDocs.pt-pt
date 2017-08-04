---
title: "Preparação para a atualização | O System Center Configuration Manager"
description: "Integre com o Configuration Manager de preparação de atualização. Aceder a dados de compatibilidade da atualização na consola do administrador. Dispositivos de destino para a atualização ou correção."
keywords: 
author: mattbriggs
ms.author: mabrigg
manager: angerobe
ms.date: 7/31/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.translationtype: MT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: b1f4cd4a6f19a02d2b2dc3f9a841aeeb2a1403dd
ms.contentlocale: pt-pt
ms.lasthandoff: 07/29/2017

---

# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>Integrar a preparação de atualização com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Preparação de atualização (anteriormente, análise de atualização) permite-lhe avaliar e analisar a preparação do dispositivo com o Windows 10. Integre com o Configuration Manager para aceder aos dados de compatibilidade de atualização de cliente na consola de administração do Configuration Manager de preparação de atualização. É capaz de dispositivos de destino para a atualização ou correção da lista de dispositivos.

Preparação de atualização é uma solução no Microsoft Operations Management Suite (OMS). Pode ler mais sobre a preparação de atualização no [começar a atualizar preparação](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).

## <a name="configure-clients"></a>Configurar os clientes

Existem vários passos de configuração que terá de executar para assegurar que os clientes podem fornecer dados a preparação de atualização:

-  Configurar definições de telemetria de cliente conforme descrito em [telemetria de configurar o Windows na sua organização](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).
-  Instalar KBs descritos no * implementar a atualização de compatibilidade e KBs relacionados * secção [começar a preparação de atualização](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).

    > [!NOTE]
    > Pode transferir um script para automatizar muitas das tarefas de configuração de cliente. Consulte o *executar o script de implementação de preparação de atualização* secção [começar a atualizar preparação](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness) para obter informações sobre o script.

## <a name="connect-to-upgrade-readiness"></a>Ligar a preparação para a atualização

### <a name="prerequisites"></a>Pré-requisitos

O Assistente de serviços do Azure a partir da versão do ramo atual 1706, é utilizado para simplificar o processo de configuração de serviços do Azure que utiliza com o Configuration Manager. Para utilizar o assistente, terá de configurar uma aplicação web do Azure. Para obter mais informações, consulte, [Assistente de serviços do Azure](/sccm/core/servers/deploy/configureazure-services-wizard).

### <a name="use-the-azure-wizard-to-create-the-connection"></a>Utilize o Assistente do Azure para criar a ligação

1.  No **administração** área de trabalho da consola do Configuration Manager, expanda **serviços em nuvem**e, em seguida, clique em **serviços do Azure**.
2.  No **home page** separador o **serviços do Azure** , clique em **configurar os serviços do Azure**.
3.  Escreva um nome amigável na página de serviços do Azure. Também pode escrever uma descrição. Em seguida, selecione **conector de preparação de atualização** e clique em **seguinte**.
4.  Especifique o seu ambiente do Azure na página da aplicação. Clique em **procurar** para configurar uma aplicação de servidor.
5.  Clique em **importação** para ligar à sua aplicação Web no Azure.
    -  Tipo de **nome de inquilino do Azure AD**.
    -  Tipo de **ID de inquilino do Azure AD**.
    -  Tipo de **nome da aplicação**.
    -  Tipo de **ID de cliente**.
    -  Tipo de **chave secreta**.
    -  Selecione a data de **expiração de chave de segredo** data.
    -  Escreva qualquer URL para o **URI de ID de aplicação**.
    -  Clique em **verifique**e, em seguida, clique em **OK**.

6.  Especifique a ligação a preparação de atualização na página de configuração. Selecione os seguintes valores:  
    -  Subscrições do Azure
    -  Grupo de recursos do Azure
    -  Área de trabalho de análise do Windows
8.  Clique em **Seguinte**. Pode rever a ligação na página de resumo. 

## <a name="complete-upgrade-readiness-tasks"></a>Concluir as tarefas de preparação de atualização  

Depois de ter de criar a ligação, efetuar estas tarefas, conforme descrito em [começar a atualizar preparação](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).  

1. Adicione o serviço de UpgradeReadiness à área de trabalho do OMS.  
2. Gerar um ID comercial.  
3. Subscreve a preparação para a atualização.   

## <a name="use-the-upgrade-readiness-deployment-script"></a>Utilize o script de implementação de preparação de atualização  

Pode automatizar muitas das tarefas de preparação de atualização e resolver problemas de dados de partilha problemas com o Microsoft **script de implementação de preparação de atualização**.  
O script de implementação de preparação de atualização faz o seguinte:  

- Define a chave de ID comercial + CommercialDataOptIn + RequestAllAppraiserVersions chaves.  
- Verifica se os computadores de utilizador podem enviar dados à Microsoft.  
- Verifica se o computador tem um reinício pendente.   
- Verifica se a versão mais recente da BDC pacote 10.0.x está instalado (requer 10.0.14913 ou versões posteriores).  
- Se estiver ativada, transforma em modo verboso para a resolução de problemas.  
- Inicia a recolha de dados de telemetria que necessita de Microsoft para avaliar a preparação de atualização da sua organização.  
- Se estiver ativada, apresenta o progresso do script numa janela cmd. Isto dá-lhe visibilidade para problemas (êxito ou falha de cada passo) e/ou escreve no ficheiro de registo.  

## <a name="to-run-the-upgrade-readiness-deployment-script"></a>Para executar o script de implementação de preparação de atualização:  

1. Transferir o [script de implementação de preparação de atualização](https://go.microsoft.com/fwlink/?LinkID=822966&clcid=0x409) e extrair UpgradeReadiness.zip. Os ficheiros no **diagnóstico** pasta são necessários apenas se pretender executar o script no modo de resolução de problemas.  
2. Edite estes parâmetros em RunConfig.bat:  
- Localização de armazenamento para as informações de registo. Exemplo: % SystemDrive%\URDiagnostics. Pode armazenar informações de registo na partilha de ficheiros remota ou um diretório local. Se o script é bloqueado de criar o ficheiro de registo para o caminho fornecido, cria os ficheiros de registo na unidade com o diretório do Windows.  
- Chave de ID comercial.  
- Por predefinição, o script envia informações de registo para a consola e o ficheiro de registo. Para alterar o comportamento predefinido, utilize uma das seguintes opções:  
    - logMode = 0 registos para apenas a consola  
    - logMode = 1 registo para o ficheiro e a consola do  
    - logMode = 2 registo apenas de ficheiros  
    - Para resolver problemas, defina **isVerboseLogging** para **$true** para gerar informações de registo que podem ajudar a diagnosticar problemas. Por predefinição, **isVerboseLogging** está definido como **$false**. Certifique-se de que a pasta de diagnóstico é instalada no mesmo diretório que o script a utilizar este modo.  
    - Notificar os utilizadores se de que precisam para reiniciar os respetivos computadores. Por predefinição, está definida para desativado.  

3. Depois de concluir a edição parâmetros RunConfig.bat, execute o script como um administrador.  


## <a name="view-microsoft-upgrade-readiness-properties-in-configuration-manager"></a>Ver propriedades de preparação de atualização da Microsoft no Configuration Manager  

1.  Na consola do Configuration Manager, navegue até à **serviços em nuvem**, em seguida, escolha **OMS conector** para abrir o **propriedades de ligação do OMS** página.  

2.  Dentro desta página, existem dois separadores:
  * O **do Azure Active Directory** separador mostra o **inquilino**, **ID de cliente**, **expiração chave secreta de cliente**, e permite-lhe **verifique** sua **chave secreta do cliente** se tiver expirado.
  * O **atualizar preparação** separador mostra o **subscrição do Azure**, **grupo de recursos do Azure**, e **área de trabalho do Operations Management Suite**.

## <a name="view-and-use-the-upgrade-information"></a>Ver e utilizar as informações de atualização

Depois de ter integrado preparação de atualização com o Configuration Manager, pode ver a análise de preparação de atualização dos clientes e, em seguida, a ação.

1. Na consola do Configuration Manager, escolha **monitorização** > **descrição geral** > **atualizar preparação**.
2. Reveja os dados, que incluem o estado de preparação de atualização e a percentagem de dispositivos do Windows que estão a denunciar telemetria.
3. Pode filtrar o dashboard para ver os dados para dispositivos em coleções específicas.
4. Pode ver os dispositivos num estado específico de preparação e criar uma coleção dinâmica para os dispositivos para que possa atualizar esses dispositivos se pronto ou, efetue uma ação para colocá-los para um Estado de preparação.

## <a name="create-a-connection-to-upgrade-readiness-1702-and-earlier"></a>Criar uma ligação a preparação de atualização (1702 e anterior)

Antes do 1706 ramo do Configuration Manager, para criar uma ligação para atualizar preparação necessários os seguintes passos.

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


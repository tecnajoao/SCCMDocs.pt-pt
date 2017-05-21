---
title: "Preparação para a atualização | O System Center Configuration Manager"
description: "Integre com o Configuration Manager de preparação para atualização. Aceder a dados de atualização de compatibilidade na consola de administração. Dispositivos de destino para a atualização ou a remediação."
keywords: 
author: brenduns
ms.author: brenduns
manager: angerobe
ms.date: 3/1/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.translationtype: Machine Translation
ms.sourcegitcommit: dcbcd57b95f304f007e92ebe2b9aeefb4b579662
ms.openlocfilehash: 986d0446209f6e7eac1b681066d1b2e2305e1975
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---

# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>Integrar com o System Center Configuration Manager de preparação para atualização
Preparação para atualização (anteriormente, análises de atualização) permite-lhe avaliar e analisar a compatibilidade com o Windows 10 e preparação do dispositivo para permitir que as atualizações mais facilmente e mais suaves. Integre com o Configuration Manager para aceder a dados de compatibilidade de atualização de cliente na consola de administração do Configuration Manager de preparação para atualização. Em seguida, poderá para dispositivos de destino para a atualização ou a remediação da lista dispositivo.

Preparação para atualização é uma solução no Microsoft Operations gestão Suite (OMS). Pode ler mais sobre a preparação para atualização na [introdução ao atualizar preparação](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).

## <a name="configure-clients"></a>Configurar os clientes

Existem vários passos de configuração que tem de executar para assegurar que os seus clientes podem fornecer dados para atualizar preparação:

-  Configurar definições de telemetria do cliente conforme descrito em [telemetria configurar janelas na sua organização](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).
-  Instalar KBs descritos no * implementar a atualização de compatibilidade e KBs relacionados * secção [introdução ao atualizar preparação](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).

    > [!NOTE]
    > Pode transferir um script para automatizar muitas das tarefas de configuração de clientes. Consulte o *executar o script de implementação de atualização preparação* secção [introdução ao atualizar preparação](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness) para obter informações sobre o script.

## <a name="create-a-connection-to-upgrade-readiness"></a>Criar uma ligação a preparação para atualização

### <a name="prerequisites"></a>Pré-requisitos

- Para adicionar a ligação, o ambiente do Configuration Manager tem primeiro de configurar um [ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) num [modo online](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/). Quando adicionar a ligação ao seu ambiente, irá também instalar o Microsoft Monitoring Agent na máquina de execução desta função de sistema de sites.
- Registar o Configuration Manager como uma ferramenta de gestão "Web aplicação and/or Web API" e obtenha o [ID de cliente a partir deste registo](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Crie uma chave de cliente para a ferramenta de gestão registado no Azure Active Directory.
- No Portal de gestão do Azure, forneça a aplicação web registado com permissão para aceder à OMS, conforme descrito em [fornecer do Configuration Manager com permissões para OMS](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

    > [!IMPORTANT]
    > Ao configurar a permissão para aceder à OMS, certifique-se de que escolher o **contribuinte** função e atribua-as permissões para o grupo de recursos da aplicação registado.

### <a name="create-the-connection"></a>Criar a ligação

1.  Na consola do Configuration Manager, escolha **administração** > **serviços em nuvem** > **atualizar conector preparação** > **criar ligação para atualizar Analytics** para iniciar o **Adicionar Assistente de ligação de análise de atualização**.
3.  No **do Azure Active Directory** ecrã, forneça **inquilino**, **ID de cliente**, e **chave de segredo do cliente**, em seguida, selecione **seguinte**.
4.  No **atualizar preparação** ecrã, indique as definições de ligação preenchendo a sua **subscrição do Azure**, **grupo de recursos Azure**, e **área de trabalho do conjunto de aplicações do Operations Management**.
5.  Verifique as definições de ligação no **resumo** ecrã, em seguida, selecione **seguinte**.

    > [!NOTE]
    > Atualizar preparação tem de ligar para o site de nível superior na sua hierarquia. Se ligar a preparação de atualizar para um site primário autónomo e, em seguida, adicionar um site de administração central ao seu ambiente, tem de eliminar e recriar a ligação de OMS dentro da nova hierarquia.

### <a name="complete-upgrade-readiness-tasks"></a>Tarefas de preparação para atualização concluídas  

Depois de ter de criar a ligação no Configuration Manager, efetuar estas tarefas, conforme descrito em [introdução ao atualizar preparação](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).  

1. Adicione o serviço de UpgradeReadiness à área de trabalho OMS.  
2. Gerar um ID comercial.  
3. Subscreva a preparação para a atualização.   

## <a name="use-the-upgrade-readiness-deployment-script"></a>Utilizar o script de implementação de preparação para atualização  

Pode automatizar muitas das tarefas de preparação para atualização e resolver problemas com o Microsoft de partilha de dados **script de implementação de atualização preparação**.  
O script de implementação de atualização preparação faz o seguinte:  

- Define a chave de ID comercial + CommercialDataOptIn + RequestAllAppraiserVersions chaves.  
- Verifica se os computadores de utilizador podem enviar dados à Microsoft.  
- Verifica se o computador tem um reinício pendente.   
- Verifica se a versão mais recente da BDC pacote 10.0.x está instalado (requer 10.0.14913 ou versões posteriores).  
- Se estiver ativada, ativa o modo verboso para a resolução de problemas.  
- Inicia a recolha de dados de telemetria que necessita de Microsoft para avaliar a preparação de atualização da sua organização.  
- Se estiver ativada, apresenta o progresso do script numa janela cmd, fornecer-lhe visibilidade sobre problemas (êxito ou falha de cada passo) e/ou escreve no ficheiro de registo.  

### <a name="to-run-the-upgrade-readiness-deployment-script"></a>Para executar o script de implementação de preparação para atualização:  

1. Transferir o [script de implementação de atualização preparação](https://go.microsoft.com/fwlink/?LinkID=822966&clcid=0x409) e extrair UpgradeReadiness.zip. Os ficheiros de **Diagnostics** pasta são necessários apenas se pretender executar o script no modo de resolução de problemas.  
2. Edite estes parâmetros no RunConfig.bat:  
- Localização do armazenamento de informações de registo. Exemplo: % SystemDrive%\URDiagnostics. Pode armazenar informações de registo na partilha de ficheiros remota ou um diretório local. Se o script é bloqueado de criar o ficheiro de registo para o caminho indicado, cria os ficheiros de registo na unidade com o diretório do Windows.  
- Chave de ID comercial.  
- Por predefinição, o script envia as informações de registo para a consola e o ficheiro de registo. Para alterar o comportamento predefinido, utilize uma das seguintes opções:  
    - logMode = 0 registo e a consola só  
    - logMode = 1 registo para o ficheiro e a consola  
    - logMode = 2 registo apenas de ficheiro  
    - Para resolução de problemas, definir **isVerboseLogging** para **$true** para gerar informações de registo que podem ajudar a diagnosticar problemas. Por predefinição, **isVerboseLogging** está definido como **$false**. Certifique-se de que a pasta de diagnóstico está instalada no mesmo diretório como o script a utilizar este modo.  
    - Notificar os utilizadores caso seja necessário reiniciar os respetivos computadores. Por predefinição, está definida como desativado.  

3. Depois de terminar de editar os parâmetros RunConfig.bat, execute o script como um administrador.  


## <a name="view-microsoft-upgrade-readiness-properties-in-configuration-manager"></a>Ver propriedades de preparação de atualização da Microsoft no Configuration Manager  

1.  Na consola do Configuration Manager, navegue para **serviços em nuvem**, em seguida, escolha **OMS conector** para abrir o **propriedades da ligação OMS** página.  

2.  Dentro desta página, existem dois separadores:
  * O **do Azure Active Directory** separador mostra o **inquilino**, **ID de cliente**, **expiração de chave de segredo do cliente**, e permite-lhe **verificar** seu **chave de segredo do cliente** se esta tiver expirado.
  * O **atualizar preparação** separador mostra o **subscrição do Azure**, **grupo de recursos Azure**, e **área de trabalho do conjunto de aplicações do Operations Management**.

## <a name="view-and-use-the-upgrade-information"></a>Ver e utilizar as informações de atualização

Depois de integrou preparação atualizar com o Configuration Manager, pode ver a análise de preparação de atualização dos seus clientes e, em seguida, tome as medidas.

1. Na consola do Configuration Manager, escolha **monitorização** > **descrição geral** > **atualizar preparação**.
2. Reveja os dados, que inclui o estado de preparação para atualização e a percentagem de dispositivos do Windows que estão a denunciar telemetria.
3. Pode filtrar o dashboard para ver os dados para dispositivos em coleções específicas.
4. Pode ver os dispositivos num estado específico de preparação e criar uma coleção dinâmica para os dispositivos para que possam atualizar esses dispositivos se pronto ou, tome medidas para colocá-los para um Estado de preparação.


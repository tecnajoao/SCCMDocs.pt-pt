---
title: Atualizar a disponibilidade
titleSuffix: Configuration Manager
description: Integre com o Configuration Manager para aceder a dispositivos Windows 10 compatibilidade da atualização dados e de destino para a atualização ou correção de preparação de atualizações.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/04/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 0ba5a484fe11185b46125de0d8764bce153f577d
ms.sourcegitcommit: a2ecd84d93f431ee77848134386fec14031aed6a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/29/2019
ms.locfileid: "55230856"
---
# <a name="integrate-upgrade-readiness-with-configuration-manager"></a>Integrar a preparação da atualização com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Preparação para atualização faz parte [Windows Analytics](https://docs.microsoft.com/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness). Permite-lhe avaliar e analisar a preparação de dispositivos no seu ambiente para uma atualização para Windows 10. Integre a preparação de atualizações com o Configuration Manager para aceder aos dados de compatibilidade da atualização de cliente na consola do Configuration Manager. Em seguida, utilize estes dados para criar coleções e dispositivos na atualização ou correção de destino.



## <a name="configure-clients"></a>Configurar os clientes

Preparação da atualização depende dos dados de análise do Windows. Por ordem para a preparação de atualizações de mensagens em fila receber dados suficientes, configure os seguintes pré-requisitos:

- Configurar todos os clientes com um *chave do ID comercial*  

- Configurar os clientes do Windows 10 para o Windows Analytics reportar dados de nível básicos, pelo menos  

- Para clientes que executam o Windows 7 ou 8.1:  

    - Instalar as atualizações, conforme descrito em [introdução à preparação de atualizações](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started#deploy-the-compatibility-update-and-related-kbs)  

    - Ativar as definições de cliente do Windows Analytics  

Configure estas definições com as definições de cliente do Configuration Manager. Para obter mais informações, consulte [utilize o Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics).

> [!NOTE]  
> Implementar as atualizações corretas de pré-requisitos e configurar as definições de cliente devem ser suficientes na maioria dos ambientes. Se ocorrerem problemas com a preparação de atualizações de mensagens em fila não receber dados a partir de dispositivos no seu ambiente, então alguns desses problemas podem ser resolvidos utilizando o [script de implementação de preparação de atualizações](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-deployment-script). 



## <a name="connect-configuration-manager-to-upgrade-readiness"></a>Ligar o Configuration Manager à preparação de atualizações

Utilizar o [Assistente de serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para simplificar o processo de configuração de serviços do Azure que utiliza com o Configuration Manager. Para ligar o Configuration Manager com a preparação, crie um registo de aplicações do Azure Active Directory (Azure AD) do tipo *aplicação Web / API* no [portal do Azure](https://portal.azure.com). Para obter mais informações sobre como criar um registo de aplicações, consulte [registar a sua aplicação no seu inquilino do Azure AD](/azure/active-directory/active-directory-app-registration). 

No portal do Azure, concede permissões à sua aplicação web recentemente registado ao seguir:
- *Leitor* permissões para o grupo de recursos que contém a área de trabalho do Log Analytics com os seus dados de preparação de atualizações
- *Contribuinte* permissões para a área de trabalho do Log Analytics que aloja os seus dados de preparação de atualizações

O Assistente de serviços do Azure utiliza este registo de aplicações para permitir que o Configuration Manager para comunicar de forma segura com o Azure AD e ligar a sua infraestrutura para os seus dados de preparação de atualizações.

> [!IMPORTANT]  
> Conceder permissões de aplicação em si, não para uma identidade de utilizador do Azure AD. É o aplicativo registrado, que acessa os dados em nome da sua infraestrutura do Configuration Manager. Para conceder as permissões, procure o nome do registo de aplicações no **adicionar utilizadores** área ao atribuir a permissão. 
> 
> Este processo é igual ao indicar o Configuration Manager com permissões para o Log Analytics. Estes passos devem ser concluídos antes do registo de aplicações é importado para o Configuration Manager com o *Assistente de serviços do Azure*.
> 
> Para obter mais informações, consulte [ligar o Configuration Manager ao Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm).


### <a name="use-the-azure-wizard-to-create-the-connection"></a>Utilize o Assistente do Azure para criar a ligação

Siga as instruções em [dos serviços do Azure configurar](/sccm/core/servers/deploy/configure/azure-services-wizard) para criar uma ligação para o Upgrade Readiness ao importar o registo de aplicações web que criou acima. 

Se a importação de aplicação web foi concluída com êxito e as permissões corretas são atribuídas no portal do Azure, o *configuração* página preenche antecipadamente os seguintes valores:   
-  Subscrições do Azure  
-  Grupo de recursos do Azure  
-  Área de trabalho do Windows Analytics  

Mais de um grupo de recursos ou área de trabalho está disponível nas seguintes circunstâncias: 
- Se a aplicação web do Azure AD registado tem *contribuinte* permissões em mais de um grupo de recursos   
- Se o grupo de recursos selecionado tem mais do que uma área de trabalho do Log Analytics  



## <a name="view-and-use-upgrade-readiness-information-in-configuration-manager"></a>Ver e utilizar informações de preparação de atualizações no Configuration Manager

Depois de ter integrado preparação de atualizações com o Configuration Manager, pode ver a análise de preparação de atualização dos seus clientes.

1. Na consola do Configuration Manager, vá para o **monitorização** área de trabalho e selecione o **preparação** nó.  

2. Reveja os dados. Por exemplo:  
    - O estado de preparação da atualização  
    - A percentagem de dispositivos do Windows que são dados de relatórios  

3. Filtre o dashboard para ver os dados para dispositivos em coleções específicas.  

4. Ver os dispositivos no estado de preparação específico e, em seguida, criar uma coleção dinâmica para esses dispositivos. Em seguida, utilizar essa coleção para atualizar esses dispositivos, ou tomar medidas para remediar os dispositivos que estão num estado bloqueado.  

> [!Note]  
> O site sincroniza dados com a preparação de atualizações uma vez por semana.<!--SCCMDocs issue 732--> Para acionar manualmente a sincronização:
> 1. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **serviços Cloud**e selecione o **dos serviços do Azure** nó.  
> 2. Selecione a ligação de preparação de atualizações a partir da lista.  
> 3. No Friso, selecione a opção para sincronizar.  



## <a name="next-steps"></a>Passos seguintes

- [Atualize o Windows para a versão mais recente](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)  
- [Criar uma sequência de tarefas para atualizar um SO](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)  
- [Criar implementações faseadas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)  

---
title: Como implementar o piloto
titleSuffix: Configuration Manager
description: Um guia de procedimentos de implantação para um grupo piloto de análise de ambiente de trabalho.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3a1f1d02a7a2dc71ddc34912e281b27dc3eff9ed
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55073373"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Como implementar o piloto com a análise de ambiente de trabalho

> [!Note]  
> Estas informações se relaciona com o serviço de pré-visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft faz não oferece quaisquer garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Uma das vantagens da análise de ambiente de trabalho é ajudar a identificar o conjunto mais pequeno de dispositivos que fornecem a cobertura mais ampla de fatores. Ele se concentra nos fatores mais importantes para um piloto de atualizações do Windows e do Office e atualizações. Certificar-se de que o projeto piloto estar mais êxito permite-lhe mover com mais rapidez e confiança para implementações ampla na produção.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]



## <a name="address-issues"></a>Resolver problemas

Utilize o portal de análise de ambiente de trabalho para revisar quaisquer problemas reportados com recursos que podem bloquear a sua implementação. Em seguida, aprovar, rejeitar ou modificar a correção sugerida. Todos os itens devem ser marcados **pronto** ou **pronto (com a remediação)** antes de inicia a implantação piloto. 

1. Ir para o portal de análise de ambiente de trabalho e selecione **planos de implantação** no grupo gerenciar.  

2. Abra um plano de implantação, selecionando o seu nome.  

3. Selecione **preparar piloto** no grupo de preparação do menu de plano de implementação.  

4. Sobre o **aplicações** separador, reveja as aplicações que precisam de sua entrada.  

5. Para cada aplicação, selecione o nome da aplicação. No painel de informações, consulte a recomendação e selecione o decisão de atualização. Se escolher **não revisto** ou **não é possível**, em seguida, a análise de ambiente de trabalho não inclui os dispositivos com esta aplicação na implantação piloto.  

6. Repita esta revisão para outros ativos.  




## <a name="create-software"></a>Criar software

Antes de poder implementar o Windows ou do Office, primeiro crie os objetos de software no Configuration Manager.

- [Aplicação do Office 365 ProPlus](https://docs.microsoft.com/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)  

- [Sequência de tarefas de atualização in-loco do Windows 10](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)



## <a name="deploy-to-pilot-devices"></a>Implementar em dispositivos pilotos

O Configuration Manager utiliza os dados da análise de ambiente de trabalho para criar uma coleção para a implantação piloto. Não implemente a sequência de aplicativo ou uma tarefa através de uma implementação tradicional. Utilize o procedimento seguinte para criar uma implementação integrada de análise de ambiente de trabalho:

1. Na consola do Configuration Manager, vá para o **biblioteca de Software**, expanda **manutenção de análise de ambiente de trabalho**e selecione o **planos de implantação** nó.  

2. Selecione o seu plano de implementação e, em seguida, selecione **detalhes do plano de implementação** na faixa de opções.  

3. Na **criar um piloto do estado** mosaico, selecione um dos seguintes tipos de objeto da lista pendente:  

    - **Aplicação** para o Office 365 ProPlus  

    - **Sequência de tarefas** para o Windows 10  
  
   Selecione **implementar**. Esta ação inicia o Assistente para implementar Software para o tipo de objeto selecionado. 


Para obter mais informações, veja os artigos seguintes:  

- [Implementar uma aplicação](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy)  

- [Implementar uma sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)  


Se o seu plano de implementação do Windows 10 e Office 365, repita este processo para criar uma segunda implementação. Por exemplo, se for a primeira implementação para a sequência de tarefas, crie uma segunda implementação para a aplicação.



## <a name="monitor"></a>Monitor

### <a name="configuration-manager-console"></a>Consola do Configuration Manager

Implementação de utilize o Gestor de configuração como qualquer outra implementação de sequência de aplicativo e a tarefa de monitorização da mesma. Para obter mais informações, veja os artigos seguintes:  

- [Monitorizar aplicação da consola do Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console)  

- [Monitorizar implementações de SO](/sccm/osd/deploy-use/monitor-operating-system-deployments)  


### <a name="desktop-analytics-portal"></a>Ambiente de trabalho do portal da análise

Utilize o portal de análise de ambiente de trabalho para ver o estado de qualquer plano de implementação. Selecione o plano de implantação e, em seguida, selecione **descrição geral do plano**. 

![Captura de ecrã de descrição geral do plano de implantação no ambiente de trabalho de análise](media/deployment-plan-overview.png)

Selecione o **piloto** mosaico. Resume o estado atual da implantação piloto. Este mosaico também apresenta dados para o número de dispositivos não iniciados, em curso, concluído, ou problemas a devolver.

Todos os dispositivos a comunicar erros ou outros problemas também estão listados na área de detalhes do projeto-piloto para a direita. Para obter detalhes sobre o problema relatado, selecione **revisão**. Esta ação altera a exibição para o **estado de implementação** página

O **estado de implementação** página apresenta uma lista de dispositivos nas seguintes categorias:

- Não iniciadas
- Em curso
- Concluída
- Necessita de atenção - dispositivos
- Necessita de atenção - problemas

O **necessita de atenção** categorias mostram as mesmas informações, mas classificada de forma diferente.

Selecione uma lista específica de qualquer vista para obter mais detalhes sobre o problema detetado.

Como resolver estes problemas de implementação, o dashboard continua Mostrar o progresso de dispositivos. Ele atualiza à medida que os dispositivos movidos de **requer atenção** ao **concluído**.



## <a name="next-steps"></a>Passos seguintes

Permitir que a execução piloto durante um período de tempo para recolher dados operacionais. Incentive os utilizadores de dispositivos pilotos para testar aplicações, suplementos e macros. 

Quando a implementação piloto atende a seus critérios de êxito, vá para o artigo seguinte para implementar na produção.
> [!div class="nextstepaction"]  
> [Implementar em produção](/sccm/desktop-analytics/deploy-prod)  

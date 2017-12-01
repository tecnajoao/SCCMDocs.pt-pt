---
title: "Ponto de distribuição de solicitação"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as configurações e limitações para utilizar um ponto de distribuição de extração com o System Center Configuration Manager."
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
caps.latest.revision: "9"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: ea8eead4706472a02f216b432ea9f2e6bdf23f66
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="use-a-pull-distribution-point-with-system-center-configuration-manager"></a>Utilizar um ponto de distribuição de solicitação com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Um ponto de distribuição de solicitação para o System Center Configuration Manager é um ponto de distribuição padrão que obtém o conteúdo distribuído, transferindo-a partir de uma localização de origem, como um cliente, em vez de ter o conteúdo instalado no mesmo servidor do site.  

 Quando implementar o conteúdo para um grande número de pontos de distribuição num site, os pontos de distribuição de solicitação podem ajudar a reduzir a carga de processamento no servidor do site e a velocidade da transferência do conteúdo para cada ponto de distribuição. Esta eficiência deve-se ao descarregamento do processo de transferência dos conteúdos para cada ponto de distribuição a partir do processo do gestor de distribuição do servidor de sites.  

-   Configurar pontos de distribuição individuais para serem pontos de distribuição de solicitação.  

-   Para cada ponto de distribuição de extração, tem de especificar um ou mais pontos de distribuição origem partir da qual pode obter implementações (um ponto de distribuição de solicitação apenas pode obter conteúdo de um ponto de distribuição que está especificado como um ponto de distribuição de origem).  

-   Quando distribui conteúdo para um ponto de distribuição de solicitação, o servidor do site notifica o ponto de distribuição de solicitação, que, em seguida, inicia a transferência do conteúdo de um ponto de distribuição de origem. Cada ponto de distribuição de extração gere individualmente a transferência do conteúdo, transferindo-o a partir de um ponto de distribuição que já tenha uma cópia do mesmo.  

Os pontos de distribuição de solicitação suportam as mesmas configurações e funcionalidades como pontos de distribuição normais do Configuration Manager. Por exemplo, um ponto de distribuição que esteja configurado como um ponto de distribuição de solicitação suporta a utilização de configurações multicast e PXE, validação de conteúdos e distribuição de conteúdos a pedido. Um ponto de distribuição de solicitação suporta comunicações HTTP ou HTTPS com os clientes, suporta as mesmas opções de certificados que outros pontos de distribuição e pode ser gerido individualmente ou como membro de um grupo de pontos de distribuição.  

> [!IMPORTANT]
> Embora um ponto de distribuição de extração suporte comunicações por HTTP e HTTPS, quando utilizar o Configuration Manager, só poderá especificar pontos de distribuição de origem que estão configurados para HTTP. Pode utilizar o SDK do Configuration Manager para especificar um ponto de distribuição de origem que esteja configurado para HTTPS.  

 **A seguinte sequência de eventos ocorre sempre que é distribuído conteúdo a um ponto de distribuição de extração:**  

-   Logo que o conteúdo tenha sido distribuído a um ponto de distribuição de solicitação, o Gestor de Transferência do servidor de sites consulta a base de dados do site para confirmar se os conteúdos estão disponíveis no ponto de distribuição de origem. Se não for possível confirmar que os conteúdos se encontram num ponto de distribuição de origem para o ponto de distribuição de solicitação, a verificação será repetida a cada 20 minutos até que os conteúdos estejam disponíveis.  

-   Quando o Gestor de Transferência de Pacote confirmar que os conteúdos estão disponíveis, notificará o ponto de distribuição de solicitação para que proceda à transferência dos mesmos. Quando o ponto de distribuição de solicitação receber esta notificação, tentará transferir os conteúdos a partir dos respetivos pontos de distribuição de origem.  

-   Quando o ponto de distribuição de solicitação concluir a transferência dos conteúdos, enviará esse estado ao ponto de gestão. No entanto, se após 60 minutos este estado não foi recebido, o Gestor de transferência do pacote reativado e verifica com o ponto de distribuição de extração para confirmar se o ponto de distribuição de solicitação transferiu o conteúdo. Se a transferência do conteúdo estiver em curso, o Gestor de Transferência de Pacotes permanecerá suspenso durante 60 minutos antes de voltar a consultar o ponto de distribuição de extração. Este ciclo continuará até o ponto de distribuição de extração concluir a transferência do conteúdo.  

**Pode configurar um ponto de distribuição de extração** quando instala o ponto de distribuição ou, depois de o ter instalado, editando as propriedades da função do sistema de sites do ponto de distribuição.  

**Pode remover a configuração para um ponto de distribuição de solicitação** editando as propriedades do ponto de distribuição. Quando remover a configuração de ponto de distribuição de solicitação, o ponto de distribuição devolve operações normais, e o servidor do site gere conteúdo futuro transfere para o ponto de distribuição.  

## <a name="limitations-for-pull-distribution-points"></a>Limitações para pontos de distribuição de extração  

-   Um ponto de distribuição baseado na nuvem não pode ser configurado como um ponto de distribuição de solicitação.  

-   Um ponto de distribuição num servidor de sites não pode ser configurado como um ponto de distribuição de solicitação.  

-   **A configuração de conteúdo pré-configurado substitui a configuração de ponto de distribuição de extração**. Um ponto de distribuição de solicitação que esteja configurado para conteúdos pré-configurados aguarda os conteúdos. Não solicita os conteúdos do ponto de distribuição de origem e, como uma distribuição padrão ponto que tenha a configuração de conteúdo pré-configurado, recebe os conteúdos do servidor do site.  

-   **Um ponto de distribuição de extração não utiliza configurações de limites de velocidade** ao transferir conteúdo. Se configurar um ponto de distribuição previamente instalado para funcionar como um ponto de distribuição de solicitação, as configurações de limites de velocidade serão guardadas, mas não utilizadas. Se posteriormente remover a configuração de ponto de distribuição de solicitação, as configurações de limite de velocidade estão implementadas conforme anteriormente configuradas.  

    > [!NOTE]  
    >  Quando um ponto de distribuição é configurado como um ponto de distribuição de solicitação, o separador **Limites de Velocidade** não está visível nas propriedades do ponto de distribuição.  

-   Um ponto de distribuição de extração não utiliza as **Definições de repetição** para a distribuição de conteúdo. A opção**Definições de Repetição** pode ser configurada no âmbito das **Propriedades do Componente de Distribuição de Software** de cada site. Para ver ou configurar estas propriedades, no **administração** área de trabalho da consola do Configuration Manager, expanda **configuração do Site**e, em seguida, selecione **Sites**. Em seguida, no painel de resultados, selecione um site e, em seguida, no **home page** separador, selecione **configurar componentes do Site**. Por fim, selecione **distribuição de Software**.  

-   Para transferir conteúdos a partir de uma origem ponto de distribuição numa floresta remota, o computador que aloja o ponto de distribuição de solicitação tem de ter um cliente de Configuration Manager instalado. Uma conta de acesso de rede que tenha acesso ao ponto de distribuição de origem tem de ser configurada para utilização.  

-   Num computador que está configurado como uma distribuição de solicitação ponto e que é executado um cliente do Configuration Manager, a versão do cliente tem de ser a mesma versão que o site do Configuration Manager que instala o ponto de distribuição de solicitação. Este é um requisito para o ponto de distribuição de solicitação para utilizar um CCMFramework que é comum para o ponto de distribuição de solicitação e o cliente do Configuration Manager.  

## <a name="about-source-distribution-points"></a>Acerca dos pontos de distribuição de origem  
 Quando configurar um ponto de distribuição de extração, tem de especificar um ou mais pontos de distribuição de origem:  

-   Apenas são apresentados os pontos de distribuição que se qualifiquem como pontos de distribuição de origem.  

-   Um ponto de distribuição de solicitação pode ser especificado como um ponto de distribuição de origem para outro ponto de distribuição de solicitação.  

-   Apenas os pontos de distribuição que suportem HTTP podem ser especificados como pontos de distribuição de origem quando utilizar o Configuration Manager.  

-   Pode utilizar o SDK do Configuration Manager para especificar um ponto de distribuição de origem que esteja configurado para HTTPS. Para utilizar um ponto de distribuição de origem que esteja configurado para HTTPS, o ponto de distribuição de solicitação tem de estar localizado conjuntamente num computador que executa o cliente do Configuration Manager.  

A cada ponto de distribuição de uma lista de pontos de distribuição de origem de pontos de distribuição de extração pode ser atribuída uma prioridade:  

-   Pode atribuir uma prioridade diferente a cada ponto de distribuição de origem ou atribuir a mesma prioridade a vários pontos de distribuição de origem.  

-   A prioridade determina a ordem pela qual o ponto de distribuição de solicitação solicita os conteúdos a partir dos respetivos pontos de distribuição de origem.  

-   Inicialmente, os pontos de distribuição de solicitação contactam um ponto de distribuição de origem com o valor de prioridade mais baixo.  Caso existam vários pontos de distribuição de origem com a mesma prioridade, o ponto de distribuição de solicitação seleciona de forma não determinística um dos pontos de distribuição de origem que partilhem essa prioridade.  

-   Quando o conteúdo não estiver disponível numa origem selecionada, o ponto de distribuição de extração tenta, em seguida, transferir o conteúdo a partir de outro ponto de distribuição com a mesma prioridade.  

-   Se nenhum dos pontos de distribuição com uma prioridade atribuída tiver o conteúdo, o ponto de distribuição de solicitação tenta transferir o conteúdo a partir de um ponto de distribuição que tenha uma prioridade atribuída com o próximo valor mais elevado, até que o conteúdo esteja localizado ou o ponto de distribuição de solicitação permaneça suspenso durante 30 minutos antes de iniciar novamente o processo.  

Quando um ponto de distribuição de extração transfere conteúdo de um ponto de distribuição de origem, esse ponto de distribuição de extração é contabilizado como um cliente na coluna **Acessos de Clientes (Exclusivos)** do relatório **Resumo de utilização do ponto de distribuição** .  

 Por predefinição, um ponto de distribuição de extração utiliza a respetiva **conta de computador** para transferir conteúdo a partir de um ponto de distribuição de origem. No entanto, quando as transferências de ponto de distribuição de solicitação de conteúdo de um ponto de distribuição de origem que esteja numa floresta remota, o ponto de distribuição de solicitação utiliza sempre a conta de acesso de rede. Este processo requer que o computador tem o cliente do Configuration Manager instalado e de que a conta de acesso de rede está configurada para utilização e de que tem acesso ao ponto de distribuição de origem.  

## <a name="about-content-transfers"></a>Acerca das transferências de conteúdo  
 Para gerir a transferência de conteúdo, os pontos de distribuição de solicitação utilizam o **CCMFramework** componente do software de cliente do Configuration Manager.  

-   Esta estrutura é instalada pelo **Pulldp.msi** quando configurar o ponto de distribuição para um ponto de distribuição de solicitação. A estrutura não necessita do cliente do Configuration Manager.  

-   Após a instalação do ponto de distribuição de solicitação, o serviço CCMExec do computador do ponto de distribuição tem de estar operacional para que o ponto de distribuição de solicitação funcione.  

-   Quando o ponto de distribuição de extração transferir conteúdo, transferirá o conteúdo utilizando o **Serviço de Transferência Inteligente em Segundo Plano** (BITS) e regista as respetivas operações nos ficheiros **datatransferservice.log** e **pulldp.log** no computador do ponto de distribuição.  

## <a name="see-also"></a>Consulte também  
 [Conceitos fundamentais da gestão de conteúdos no System Center Configuration Manager](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   

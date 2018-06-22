---
title: Ponto de distribuição de solicitação
titleSuffix: Configuration Manager
description: Saiba mais sobre as configurações e limitações para utilizar um ponto de distribuição de extração com o System Center Configuration Manager.
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d6d6f68e913d261a5a23db85707ea0c9ac965cbd
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339143"
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

-   Quando o Gestor de Transferência de Pacote confirmar que os conteúdos estão disponíveis, notificará o ponto de distribuição de solicitação para que proceda à transferência dos mesmos. Se esta falha de notificação, tentará novamente com base no componente de distribuição de Software **definições de repetição** para pontos de distribuição de solicitação. Quando o ponto de distribuição de solicitação receber esta notificação, tentará transferir os conteúdos a partir dos respetivos pontos de distribuição de origem.  

-   Enquanto o ponto de distribuição de solicitação transfere o conteúdo do Gestor de transferência do pacote irá consultar o estado com base no componente de distribuição de Software **estado da consulta definições** para pontos de distribuição de solicitação.  Quando o ponto de distribuição de extração concluir a transferência de conteúdos, enviará esse Estado ao ponto de gestão.

**Pode configurar um ponto de distribuição de extração** quando instala o ponto de distribuição ou, depois de o ter instalado, editando as propriedades da função do sistema de sites do ponto de distribuição.  

**Pode remover a configuração para um ponto de distribuição de solicitação** editando as propriedades do ponto de distribuição. Quando remover a configuração de ponto de distribuição de solicitação, o ponto de distribuição devolve operações normais, e o servidor do site gere conteúdo futuro transfere para o ponto de distribuição.  

## <a name="to-configure-software-distribution-component-for-pull-distribution-points"></a>Para configurar o componente de distribuição de Software para pontos de distribuição de solicitação

1.  Na consola do Configuration Manager, escolha **administração** > **Sites**.  

2.  Selecione o site pretendida e selecione **configurar componentes do Site** > **distribuição de Software**

3. Selecione o **ponto de distribuição de solicitação** separador.  

4.  No **definições de repetição** lista, configure os seguintes valores:  

    -   **Número de tentativas** -o número de vezes que o Gestor de transferência do pacote tentar notificar o ponto de distribuição de solicitação para transferir o conteúdo.  Se este número for excedido o Gestor de transferência do pacote irá cancelar a transferência.

    -   **Atraso antes de repetir (minutos)** -o número de minutos que o Gestor de transferência do pacote irá aguardar entre tentativas. 

5.  No **estado da consulta definições** lista, configure os seguintes valores:  

    -   **Número de inquérito** -o número de vezes que o Gestor de transferência do pacote entra em contacto com o ponto de distribuição de extração para obter o estado da tarefa.  Se este número for excedido antes da conclusão da tarefa do Gestor de transferência de pacotes cancelará a transferência.

    -   **Atraso antes de repetir (minutos)** -o número de minutos que o Gestor de transferência do pacote irá aguardar entre tentativas. 
    
    > [!NOTE]  
    >  Quando o Gestor de transferência do pacote cancela uma tarefa porque foi excedido o número de tentativas de consulta do Estado do ponto de distribuição de solicitação irá continuar a transferir o conteúdo.  Quando terminar, a mensagem de estado adequado será enviada para o Gestor de transferência do pacote e a consola irá refletir o estado de novo.
    
## <a name="limitations-for-pull-distribution-points"></a>Limitações para pontos de distribuição de extração  

-   Um ponto de distribuição baseado na nuvem não pode ser configurado como um ponto de distribuição de solicitação.  

-   Um ponto de distribuição num servidor de sites não pode ser configurado como um ponto de distribuição de solicitação.  

-   **A configuração de conteúdo pré-configurado substitui a configuração de ponto de distribuição de extração**. Um ponto de distribuição de solicitação que esteja configurado para conteúdos pré-configurados aguarda os conteúdos. Não solicita os conteúdos do ponto de distribuição de origem e, como uma distribuição padrão ponto que tenha a configuração de conteúdo pré-configurado, recebe os conteúdos do servidor do site.  

-   **Um ponto de distribuição de solicitação não utiliza configurações de limites de agenda ou a taxa de** ao transferir conteúdo. Se configurar um ponto de distribuição anteriormente instalado para ser um ponto de distribuição de solicitação, configurações de limites de agenda e velocidade serão guardadas, mas não utilizadas. Se posteriormente remover a configuração de ponto de distribuição de solicitação, as configurações de limite de agenda e velocidade são implementadas conforme anteriormente configuradas.  

    > [!NOTE]  
    >  Quando um ponto de distribuição é configurado como um ponto de distribuição de solicitação, o **agenda** e **limites de velocidade** separadores não estão visíveis nas propriedades do ponto de distribuição.  

-   Pontos de distribuição de solicitação não utilizam as definições de **geral** separador do **propriedades do componente de distribuição de Software** para cada site.  Isto inclui o **distribuição simultânea** e **repetição Multicast** definição.  Utilize o **ponto de distribuição de solicitação** separador para configurar definições para os pontos de distribuição de solicitação.

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
<!--sms.503672 -Clarified BITS use-->
-   Quando o ponto de distribuição de solicitação transfere conteúdos, transfere a utilizar o **Background Intelligent Transfer Service** (BITS) incorporado no sistema operativo Windows. A funcionalidade de extensão de servidor IIS de BITS opcional para ser instalada não necessita de um ponto de distribuição de solicitação.

-  O ponto de distribuição de solicitação regista a conclusão da operação no **datatransferservice.log** e **pulldp.log** no computador do ponto de distribuição.

## <a name="see-also"></a>Consulte também  
 [Conceitos fundamentais da gestão de conteúdos no System Center Configuration Manager](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   

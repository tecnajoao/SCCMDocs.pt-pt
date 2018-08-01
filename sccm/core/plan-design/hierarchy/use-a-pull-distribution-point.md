---
title: Ponto de distribuição de extração
titleSuffix: Configuration Manager
description: Saiba mais sobre as configurações e limitações da utilização de um ponto de distribuição de solicitação com o Configuration Manager."
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 008da23a6fedf1666a29754dc41a47c61f8bfbda
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384237"
---
# <a name="use-a-pull-distribution-point-with-configuration-manager"></a>Utilizar um ponto de distribuição de solicitação com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Quando distribui conteúdo a um ponto de distribuição padrão na consola do Configuration Manager, o servidor do site envia por push o conteúdo ao ponto de distribuição. Um ponto de distribuição de extração obtém conteúdo, transferindo-a partir de uma localização de origem, como um cliente.  

Quando distribui conteúdo por muitos pontos de distribuição, pontos de distribuição de extração que ajudam a reduzir a carga de processamento no servidor do site. Eles também acelera a transferência de conteúdo para cada servidor. Normalmente o componente do Gestor de distribuição no servidor do site envia conteúdo para cada ponto de distribuição. Em vez disso, o site descarrega o processo de transferência dos conteúdos para os pontos de distribuição de extração.  

Configurar pontos de distribuição individuais para serem pontos de distribuição de extração. Para cada ponto de distribuição de extração, especifique um ou mais pontos de distribuição origem do qual ele pode obter o conteúdo. Um ponto de distribuição de extração apenas pode transferir o conteúdo de um ponto de distribuição que especificar como um ponto de distribuição de origem. 

Quando distribui conteúdo a um ponto de distribuição de extração na consola, o servidor do site envia uma notificação. O ponto de distribuição de extração transfere o conteúdo de um ponto de distribuição de origem. Um ponto de distribuição de extração gere a transferência de conteúdo ao transferir a partir de um ponto de distribuição que já tenha uma cópia do conteúdo.  

Os pontos de distribuição de extração suportam as mesmas configurações e funcionalidade como pontos de distribuição típico. Por exemplo, um ponto de distribuição de extração suporta: 
- Configurações de multicast e PXE
- Validação de conteúdos
- Distribuição de conteúdo a pedido
- Comunicações HTTP ou HTTPS de clientes
- O mesmo certificado opções como outros pontos de distribuição
- Gerir individualmente ou como membro de um grupo de pontos de distribuição  

> [!IMPORTANT]  
> Embora um ponto de distribuição de extração suporte comunicações por HTTP e HTTPS, quando utilizar a consola do Configuration Manager, só pode especificar pontos de distribuição de origem que estejam configurados para HTTP. Pode utilizar o SDK do Configuration Manager para especificar um ponto de distribuição de origem que esteja configurado para HTTPS.  

Configure um ponto de distribuição de solicitação quando instala o ponto de distribuição. Depois de criar um ponto de distribuição, configure-o como uma distribuição de solicitação editando as propriedades da função de ponto. Para obter mais informações sobre como ativar um ponto de distribuição como um ponto de distribuição de extração, consulte [ponto de distribuição de extração](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pull-distribution-point).  

Remova a configuração para um ponto de distribuição de solicitação editando as propriedades do ponto de distribuição. Quando remover a configuração como um ponto de distribuição de solicitação, ele retorna a operação normal. O servidor do site gere futuras transferências de conteúdo ao ponto de distribuição.  



### <a name="distribution-process"></a>Processo de distribuição

Quando distribui conteúdo a um ponto de distribuição de extração, ocorre a seguinte sequência de eventos:

-   Quando distribui conteúdo para um ponto de distribuição de extração na consola, o componente do Gestor de transferência no servidor do site verifica a base de dados do site para confirmar se o conteúdo está disponível num ponto de distribuição de origem. Se não for possível confirmar que o conteúdo está num ponto de distribuição de origem para o ponto de distribuição de extração, repete a verificação a cada 20 minutos até que o conteúdo está disponível.  

-   Quando o Gestor de Transferência de Pacote confirmar que os conteúdos estão disponíveis, notificará o ponto de distribuição de solicitação para que proceda à transferência dos mesmos. Se esta notificação falhar, ele tentará novamente com base no componente de distribuição de Software **definições de repetição** para pontos de distribuição de extração. Quando o ponto de distribuição de solicitação recebe esta notificação, tentará transferir o conteúdo a partir dos respetivos pontos de distribuição de origem.  

-   Embora o ponto de distribuição de extração transfere o conteúdo, o Gestor de transferência do pacote de consulta o estado com base no componente de distribuição de Software **estado de definições de consulta** para pontos de distribuição de extração.  Quando o ponto de distribuição de extração concluir a transferência de conteúdos, enviará esse Estado ao ponto de gestão.  



## <a name="configure-site-component-settings"></a>Configurar as definições de componentes do site

Quando utiliza um ponto de distribuição de extração, reveja e configure as seguintes definições de componente do site:  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó.  

2.  Selecione o site. No Friso, clique em **configurar componentes do Site**e selecione **distribuição de Software**.  

3. Mude para o **ponto de distribuição de extração** separador.  

4.  Na **definições de repetição** de grupo, reveja os seguintes valores:  

    -   **Número de tentativas**: O número de vezes que o Gestor de transferência de pacote tentar notificar o ponto de distribuição de extração para transferir o conteúdo. Depois de tentar este número de vezes, o Gestor de transferência de pacotes cancela a transferência. Este valor é 30 por predefinição.  

    -   **Atraso entre repetições (minutos) antes de**: O número de minutos que o Gestor de transferência do pacote tem de aguardar entre tentativas. Este valor é de 20 por predefinição.  

5.  Na **estado de definições de consulta** de grupo, reveja os seguintes valores:  

    -   **Número de inquéritos**: O número de vezes que o Gestor de transferência de pacote entra em contacto com o ponto de distribuição de extração para obter o estado da tarefa. Se tentar este número de vezes antes da tarefa é concluída, o Gestor de transferência de pacotes cancela a transferência. Este valor é 72 por predefinição.   

    -   **Atraso entre repetições (minutos) antes de**: O número de minutos que o Gestor de transferência do pacote tem de aguardar entre tentativas. Este valor é de 60 por predefinição.   
    
    > [!NOTE]  
    >  Quando o Gestor de transferência do pacote de cancelar uma tarefa, porque excede o número de tentativas de consulta, o ponto de distribuição de extração continua a transferência do conteúdo. Quando terminar, o ponto de distribuição de extração envia a mensagem de estado adequado e a consola reflete o estado de novo.  
    


## <a name="limitations"></a>Limitações 

-   Não é possível configurar um ponto de distribuição de nuvem como um ponto de distribuição de extração.  

-   Não é possível configurar a função de ponto de distribuição num servidor do site como um ponto de distribuição de extração.  

-   A configuração de conteúdo pré-configurado substitui a configuração de ponto de distribuição de extração. Se ativar a opção para **ativar conteúdo pré-configurado para este ponto de distribuição** num ponto de distribuição de solicitação, ele aguarda o conteúdo. Ele não solicita os conteúdos do ponto de distribuição de origem. Como um ponto de distribuição padrão habilitado para pré-configurado conteúdo, ele não recebe conteúdo do servidor do site. Para obter mais informações, consulte [conteúdo pré-configurado](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).  

-   Um ponto de distribuição de extração não utiliza configurações de limite de agendamento ou taxa. Quando configurar um ponto de distribuição anteriormente instalado para ser um ponto de distribuição de extração, configurações de limites de agendamento e a taxa de serão guardadas, mas não utilizadas. Posteriormente, se remover a configuração de ponto de distribuição de solicitação, as configurações de limite de agendamento e a taxa de são implementadas conforme anteriormente configuradas.  

    > [!NOTE]  
    >  O **agenda** e **limites de velocidade** separadores não estão visíveis nas propriedades do ponto de distribuição.  

-   Pontos de distribuição de extração não utilizam as definições do **gerais** separador da **propriedades do componente de distribuição de Software** para cada site. Estas definições incluem **distribuição simultânea** e **repetições Multicast**.  

-   Para transferir o conteúdo de um ponto de distribuição de origem numa floresta remota, instale o cliente do Configuration Manager no ponto de distribuição de extração. Também configure uma conta de acesso de rede que pode aceder ao ponto de distribuição de origem. A partir da versão 1806, se habilitar a opção de site para **sistemas de sites de certificados gerados pelo utilize o Gestor de configuração para HTTP**, em seguida, não precisa de uma conta de acesso de rede.<!--1358228-->  

-   Se o ponto de distribuição de extração também for um cliente do Configuration Manager, a versão do cliente tem de ser o mesmo que o site do Configuration Manager que instala o ponto de distribuição de extração. O ponto de distribuição de extração utiliza um CCMFramework comum ao ponto de distribuição de solicitação e o cliente do Configuration Manager.  



## <a name="about-source-distribution-points"></a>Acerca dos pontos de distribuição de origem  

Quando configurar o ponto de distribuição de extração, especifica um ou mais pontos de distribuição de origem:  

-   O assistente apresenta apenas os pontos de distribuição elegíveis para serem pontos de distribuição de origem.  

-   Um ponto de distribuição de solicitação pode ser especificado como um ponto de distribuição de origem para outro ponto de distribuição de solicitação.  

-   Apenas os pontos de distribuição que suportem HTTP podem ser especificados como pontos de distribuição de origem, quando utilizar a consola do Configuration Manager.  

-   Utilize o SDK do Configuration Manager para especificar um ponto de distribuição de origem que esteja configurado para HTTPS. Para utilizar um ponto de distribuição de origem que esteja configurado para HTTPS, instale o cliente do Configuration Manager no ponto de distribuição de extração.  

-   A partir da versão 1806, se seus escritórios remotos tenham uma melhor conexão à internet ou para reduzir a carga no seu links WAN, utilizam um [ponto de distribuição da nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) no Microsoft Azure como origem. O ponto de distribuição de extração tem acesso à internet para comunicar com o Microsoft Azure. O conteúdo tem de ser distribuído ao ponto de distribuição de nuvem de origem.<!--1321554-->  

    > [!Note]  
    > Esta funcionalidade de incorrer em custos à sua subscrição do Azure para a saída de rede e de armazenamento de dados. Para obter mais informações, consulte a [custo de utilização de um ponto de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_cost).  


> [!Tip]  
> Quando um ponto de distribuição de extração transfere conteúdo de um ponto de distribuição de origem, esse ponto de distribuição de extração é contabilizado como um cliente na coluna **Acessos de Clientes (Exclusivos)** do relatório **Resumo de utilização do ponto de distribuição** .  


### <a name="source-priorities"></a>Prioridades de origem

-   Atribuir uma prioridade diferente para cada ponto de distribuição de origem ou o atribuir a origem de vários pontos de distribuição para a mesma prioridade.  

-   A prioridade determina a ordem em que o ponto de distribuição de solicitação solicita conteúdo a partir dos respetivos pontos de distribuição de origem.  

-   Inicialmente, os pontos de distribuição de solicitação contactam um ponto de distribuição de origem com o valor de prioridade mais baixo. Se existirem vários pontos de distribuição de origem com a mesma prioridade, o ponto de distribuição de solicitação seleciona aleatoriamente uma das origens com a prioridade.  

-   Se o conteúdo não estiver disponível numa origem selecionada, o ponto de distribuição de extração tenta, em seguida, transferir o conteúdo a partir de outro ponto de distribuição com a mesma prioridade.  

-   Se nenhum dos pontos de distribuição com uma prioridade atribuída tiver o conteúdo, o ponto de distribuição de solicitação tenta transferir o conteúdo de um ponto de distribuição de origem com o nível de prioridade seguinte. Esta pesquisa ele continua até que o conteúdo está localizado.   

- Se nenhum dos pontos de distribuição de origem atribuído possuem o conteúdo, o ponto de distribuição de extração tem de aguardar durante 30 minutos e, em seguida, inicia o processo novamente.  



## <a name="inside-the-pull-distribution-point"></a>Dentro do ponto de distribuição de extração 

-   Para gerir a transferência de conteúdo, os pontos de distribuição de extração utilizam o **CCMFramework** componente. O cliente do Configuration Manager inclui este componente.  

-   Quando ativar o ponto de distribuição de solicitação, a instalação do site **pulldp**. Este instalador também adiciona o componente CCMFramework. O framework não precisa de cliente do Configuration Manager.  

-   Depois do ponto de distribuição de extração é instalado, ele usa principalmente o **CCMExec** serviço à função.  

-   Quando o ponto de distribuição de extração transferir conteúdo, ele usa o **serviço de transferência inteligente em segundo plano** (BITS) incorporadas no Windows. Um ponto de distribuição de extração, não precisa que instale a extensão de BITS para o servidor de IIS.<!--sms.503672 -Clarified BITS use-->

-  Para obter detalhes operacionais, consulte os seguintes arquivos de log no ponto de distribuição de extração:  
    - **Datatransferservice. log**
    - **Pulldp**



## <a name="see-also"></a>Consulte também  
 [Conceitos fundamentais da gestão de conteúdos](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   

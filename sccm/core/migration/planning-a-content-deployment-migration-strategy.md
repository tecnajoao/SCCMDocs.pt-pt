---
title: "Migrar conteúdo | Documentos do Microsoft"
description: "Utilize pontos de distribuição para gerir conteúdo enquanto a migrar dados para uma hierarquia de destino do System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 66f7759c-6272-4116-aad7-0d05db1d46cd
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 468673581e0464fab21397c472b76708b8a5438b
ms.openlocfilehash: 25619d91522193178e0415f649ca4b34c94ecc89
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="plan-a-content-deployment-migration-strategy-in-system-center-configuration-manager"></a>Planear uma estratégia de migração de implementação de conteúdos no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Enquanto ativamente migrar dados para uma hierarquia de destino do System Center Configuration Manager, os clientes do Configuration Manager em hierarquias de origem e de destino podem manter o acesso a conteúdo que tenha implementado na hierarquia de origem. Também pode utilizar a migração para atualizar ou reatribuir pontos de distribuição da hierarquia de origem para se tornarem pontos de distribuição na hierarquia de destino. Quando partilha e atualiza ou reatribui um ponto de distribuição, esta estratégia pode ajudar a evitar a reimplementação de conteúdo em novos servidores na hierarquia de destino para os clientes migrados.  

Apesar de poder recriar e distribuir conteúdo na hierarquia de destino, também pode utilizar as seguintes opções para gerir este conteúdo:  

-   Partilhar os pontos de distribuição na hierarquia de origem com clientes da hierarquia de destino.  

-   Atualize pontos de distribuição autónomos do Configuration Manager 2007 ou do Configuration Manager 2007 sites secundários na hierarquia de origem para se tornarem pontos de distribuição na hierarquia de destino.  

-   Reatribua pontos de distribuição a partir de uma hierarquia de origem do System Center Configuration Manager para um site na hierarquia de destino.  

Utilize as secções seguintes para planear a implementação de conteúdo durante a migração:  

-   [Partilhar pontos de distribuição entre hierarquias de origem e destino](#About_Shared_DPs_in_Migration)  

-   [Planear a atualização de pontos de distribuição partilhados do Configuration Manager 2007](#Planning_to_Upgrade_DPs)  

    -   [Processo de atualização de pontos de distribuição](#BKIMK_UpgradeProcess)  

    -   [Planear a atualização de sites secundários do Configuration Manager 2007](#BKMK_UpgradeSS)  

-   [Plano para reatribuir os pontos de distribuição do System Center Configuration Manager](#BKMK_ReassignDistPoint)  

    -   [Processo de reatribuição de pontos de distribuição](#BKMK_ReassignProcess)  

-   [Propriedade do conteúdo após a migração de conteúdo](#About_Migrating_Content)  

##  <a name="About_Shared_DPs_in_Migration"></a> Partilhar pontos de distribuição entre hierarquias de origem e destino  
Durante a migração, pode partilhar pontos de distribuição de uma hierarquia de origem com a hierarquia de destino. Pode utilizar pontos de distribuição partilhados para disponibilizar imediatamente conteúdo que tenha migrado de uma hierarquia de origem a clientes da hierarquia de destino, sem ter de recriar esse conteúdo e distribui-lo pelos novos pontos de distribuição na hierarquia de destino. Quando os clientes da hierarquia de destino pedirem conteúdo implementado em pontos de distribuição que partilhou, os pontos de distribuição partilhados poderão ser oferecidos aos clientes como localizações de conteúdo válidas.  

 Além de ser uma localização válida de conteúdos para clientes na hierarquia de destino enquanto a migração da hierarquia de origem continua ativa, é possível atualizar ou reatribuir um ponto de distribuição à hierarquia de destino. Pode atualizar pontos de distribuição partilhados do Configuration Manager 2007 e reatribuir pontos de distribuição partilhados do System Center 2012 Configuration Manager. Quando atualiza ou reatribui um ponto de distribuição partilhado, este é removido da hierarquia de origem e passa a ser um ponto de distribuição da hierarquia de destino. Depois de atualizar ou reatribuir um ponto de distribuição partilhado, pode continuar a utilizá-lo na hierarquia de destino após a conclusão da migração a partir da hierarquia de origem. Para mais informações sobre como atualizar um ponto de distribuição partilhado, consulte o artigo [pontos de distribuição partilhados do plano para atualização do Configuration Manager 2007](#Planning_to_Upgrade_DPs). Para mais informações sobre como reatribuir um ponto de distribuição partilhado, consulte o artigo [planear a reatribuição de pontos de distribuição System Center Configuration Manager](#BKMK_ReassignDistPoint).  

 Pode optar por partilhar pontos de distribuição de qualquer site de origem da hierarquia de origem. Quando partilha pontos de distribuição para um site de origem, os sites secundários subordinados são partilhados em cada ponto de distribuição elegíveis desse site primário e de cada um dos sites primários. Para ser elegível para ser um ponto de distribuição partilhado, o servidor de sistema de sites que aloja o ponto de distribuição tem de ser configurado com um nome de domínio completamente qualificado (FQDN). Quaisquer pontos de distribuição que estão configurados com um nome NetBIOS serão ignorados.  

> [!TIP]  
>  Do Configuration Manager 2007 não necessita de configurar um FQDN para servidores de sistema de sites.  

Utilize as informações seguintes para planear pontos de distribuição partilhados:  

-   Os pontos de distribuição que partilhar têm de cumprir os pré-requisitos para pontos de distribuição partilhados. Para mais informações sobre estes pré-requisitos, consulte o artigo [necessário configurações para migração](../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) no [os pré-requisitos da migração no System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

-   A ação de partilha de ponto de distribuição é uma definição ao nível do site que partilha todos os pontos de distribuição elegíveis de um site de origem e de quaisquer sites secundários subordinados diretos. Não é possível selecionar pontos de distribuição individuais para partilhar quando ativa a partilha de pontos de distribuição.  

-   Os clientes da hierarquia de destino podem receber informações de localizações de conteúdo relativas a pacotes distribuídos aos pontos de distribuição partilhados a partir da hierarquia de origem. Pontos de distribuição a partir de uma hierarquia de origem do Configuration Manager 2007, isto inclui pontos de distribuição secundários, pontos de distribuição em partilhas de servidor e pontos de distribuição padrão.  

    > [!WARNING]  
    >  Se alterar a hierarquia de origem, os pontos de distribuição partilhados a partir da hierarquia de origem original deixam de estar disponíveis e não será possível oferecê-los como localizações de conteúdo a clientes da hierarquia de destino. Se reconfigurar a migração para utilizar a hierarquia de origem original, os pontos de distribuição partilhados anteriormente serão restaurados como servidores de localização de conteúdo válidos.  

-   Quando migra um pacote alojado num ponto de distribuição partilhado, a versão do pacote tem de permanecer a mesma nas hierarquias de origem e de destino. Quando a versão de um pacote não é a mesma nas hierarquias de origem e de destino, os clientes da hierarquia de destino não conseguem obter esse conteúdo do ponto de distribuição partilhado. Consequentemente, se atualizar um pacote na hierarquia de origem, terá de migrar novamente os dados do pacote para que os clientes da hierarquia de destino possam obter esse conteúdo de um ponto de distribuição partilhado.  

    > [!NOTE]  
    >  Quando visualiza detalhes de um pacote alojado num distribuição partilhado ponto, o número de pacotes apresentados como **pacotes alojados migrados** no site de origem **pontos de distribuição partilhados** separador não é atualizado até à conclusão do ciclo de recolha de dados seguinte.  

-   Pode ver pontos de distribuição partilhados e as respetivas propriedades no **hierarquia de origem** nó do **administração** área de trabalho na consola do Configuration Manager que liga à hierarquia de destino.  

-   Não é possível utilizar um ponto de distribuição partilhados a partir de uma hierarquia de origem do Configuration Manager 2007 para alojar pacotes do Microsoft Application Virtualization (App-V). Os pacotes de App-V têm de ser migrados e convertidos para serem utilizados pelos clientes na hierarquia de destino. No entanto, pode utilizar um ponto de distribuição partilhados a partir de uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager para alojar pacotes de App-V para clientes de uma hierarquia de destino.  

-   Quando partilha um ponto de distribuição protegido de uma hierarquia de origem do Configuration Manager 2007, a hierarquia de destino cria um grupo de limites que inclui as localizações de rede protegidas do ponto de distribuição. Não é possível alterar este grupo de limites na hierarquia de destino. No entanto, se alterar as informações de limites protegidos para o ponto de distribuição na hierarquia de origem do Configuration Manager 2007, essa alteração será refletida na hierarquia de destino após a conclusão do próximo ciclo de recolha de dados.  

    > [!NOTE]  
    >  Sites do Configuration Manager do System Center 2012 e System Center Configuration Manager utilizam o conceito de pontos de distribuição preferenciais, em vez de pontos de distribuição protegidos. Esta condição só se aplica a pontos de distribuição partilhados a partir de sites de origem do Configuration Manager 2007.  

Os pontos de distribuição elegíveis não são visíveis na consola do Configuration Manager antes de partilhar pontos de distribuição a partir de um site de origem. Depois de partilhar pontos de distribuição, apenas os pontos de distribuição partilhados com êxito são listados.  

Depois de ter partilhado pontos de distribuição, pode alterar a configuração de qualquer ponto de distribuição partilhado na hierarquia de origem. As alterações efetuadas à configuração de um ponto de distribuição são refletidas na hierarquia de destino após os ciclo de recolha de dados seguinte. Os pontos de distribuição que tenha atualizado para serem elegíveis para partilha são partilhados automaticamente, enquanto aqueles que já não são elegíveis deixam de ser partilhados. Por exemplo, poderá ter um ponto de distribuição que não está configurado com um FQDN de intranet e não foi inicialmente partilhado com a hierarquia de destino. Depois de configurar o FQDN para esse ponto de distribuição, o ciclo de recolha de dados seguintes identifica esta configuração e o ponto de distribuição é partilhado com a hierarquia de destino.  

##  <a name="Planning_to_Upgrade_DPs"></a>Planear a atualização de pontos de distribuição partilhados do Configuration Manager 2007  
Quando migra a partir de uma hierarquia de origem do Configuration Manager 2007, pode atualizar um ponto de distribuição partilhado para o tornar um ponto de distribuição do System Center Configuration Manager. Pode atualizar os pontos de distribuição em sites primários e sites secundários. O processo de atualização remove o ponto de distribuição da hierarquia do Configuration Manager 2007 e faz com que um servidor de sistema de sites na hierarquia de destino. Este processo também copia o conteúdo existente no ponto de distribuição para uma nova localização no computador do ponto de distribuição. Em seguida, o processo de atualização modifica a cópia do conteúdo para criar o single instance store para utilização com a implementação de conteúdos na hierarquia de destino. Por conseguinte, quando atualiza um ponto de distribuição, não é necessário redistribuir os conteúdos migrados que se encontravam alojados no ponto de distribuição do Configuration Manager 2007.  

Depois do Configuration Manager converte o conteúdo no single instance store, o Configuration Manager elimina o conteúdo de origem original no computador do ponto de distribuição para libertar espaço em disco. O Configuration Manager não utiliza a localização de conteúdo de origem original.  

Nem todos os pontos de distribuição do Configuration Manager 2007 que pode partilhar são elegíveis para atualização para o System Center Configuration Manager. Para ser elegível para atualização, um ponto de distribuição do Configuration Manager 2007 tem de cumprir as condições para atualização. Estas condições incluem o servidor de sistema do site no qual o ponto de distribuição está instalado e aponte o tipo de distribuição do Configuration Manager 2007 que está instalado. Por exemplo, não é possível atualizar qualquer tipo de ponto de distribuição que esteja instalado no computador do servidor do site num site primário, mas pode atualizar um ponto de distribuição padrão que esteja instalado no computador do servidor do site num site secundário.  

> [!NOTE]  
>  Pode atualizar apenas do Configuration Manager 2007 pontos de distribuição partilhado que se encontrem num computador que executa uma versão do sistema operativo que é suportada para pontos de distribuição na hierarquia de destino. Por exemplo, embora possa partilhar um ponto de distribuição do Configuration Manager 2007 que estiver num computador que executa o Windows Vista, é possível atualizar este ponto de distribuição partilhado porque o sistema operativo não é suportado pelo System Center Configuration Manager para utilização como um ponto de distribuição.  

A tabela seguinte lista as localizações suportadas para cada tipo de ponto de distribuição do Configuration Manager 2007 que pode atualizar.  

|Tipo de ponto de distribuição|Ponto de distribuição num computador do sistema de sites diferente do servidor do site|Ponto de distribuição num computador do sistema de sites diferente do servidor do site e que aloja outras funções de sistema de sites|Ponto de distribuição no servidor de um site secundário|  
|--------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------|  
|Ponto de distribuição padrão|Sim|Não|Sim|  
|Ponto de distribuição em partilhas de servidor<sup>1</sup>|Sim|Não|Não|  
|Ponto de distribuição secundário|Sim|Não|Não|  

 <sup>1</sup> system Center Configuration Manager não suporta partilhas de servidor para sistemas de sites, mas suporta a atualização de um ponto de distribuição do Configuration Manager 2007 que se encontre numa partilha de servidor. Quando atualiza um ponto de distribuição do Configuration Manager 2007 que se encontre numa partilha de servidor, o tipo de ponto de distribuição é automaticamente convertido num servidor e tem de selecionar a unidade no computador do ponto de distribuição que irá armazenar o single instance store de conteúdo.  

> [!WARNING]  
>  Antes de atualizar um ponto de distribuição secundário, desinstale o software de cliente do Configuration Manager 2007. Quando atualiza um ponto de distribuição do ramo que tem o software de cliente do Configuration Manager 2007 instalado, o conteúdo que foi anteriormente implementado no computador é removido do computador e a atualização do ponto de distribuição falha.  

Para identificar os pontos de distribuição que são elegíveis para atualização na consola do Configuration Manager no **hierarquia de origem** nó, selecione um site de origem e, em seguida, selecione o **pontos de distribuição partilhados** separador. Os pontos de distribuição elegíveis apresentam **Sim** na coluna **Elegível para Atualização** .  

Ao atualizar um ponto de distribuição que está instalado no servidor do site secundário do Configuration Manager 2007, o site secundário é desinstalado da hierarquia de origem. Embora este cenário seja designado uma atualização de site secundário, apenas se aplica à função de ponto de distribuição do sistema de sites. Por conseguinte, o site secundário não é atualizado e, em vez disso, é desinstalado. Esta opção deixa um ponto de distribuição da hierarquia de destino no computador que era o servidor do site secundário. Se pretender atualizar o ponto de distribuição num site secundário, consulte o artigo [planear atualizar sites secundários do Configuration Manager 2007](#BKMK_UpgradeSS) neste tópico.  

###  <a name="BKIMK_UpgradeProcess"></a> Processo de atualização de pontos de distribuição  
Pode utilizar a consola do Configuration Manager para atualizar os pontos de distribuição do Configuration Manager 2007 que tenha partilhado com a hierarquia de destino. Quando atualiza um ponto de distribuição partilhado, o ponto de distribuição é desinstalado do site do Configuration Manager 2007. Em seguida, é instalado como um ponto de distribuição que esteja anexado a um site primário ou secundário que esteja especificado na hierarquia de destino. O processo de atualização cria uma cópia do conteúdo migrado que é armazenada no ponto de distribuição e, em seguida, converte esta cópia para o arquivo de conteúdos de instância única. Quando o Configuration Manager converte um pacote para o arquivo de conteúdos de instância única, elimina esse pacote a partir da partilha smspkg LOCALIZADA no computador do ponto de distribuição, a menos que o pacote tenha um ou mais anúncios que estão definidos como **executar programa a partir do ponto de distribuição**.  

Para atualizar o ponto de distribuição, o Configuration Manager utiliza o **conta de acesso do Site de origem** que está configurada para recolher dados a partir do fornecedor de SMS do site de origem. Embora esta conta apenas necessite **leitura** permissão para objetos de site recolher dados do site de origem, tem também de ter **eliminar** e **modificar** permissão para o **Site** classe para remover com sucesso o ponto de distribuição do site do Configuration Manager 2007 durante a atualização.  

> [!NOTE]  
>  O Configuration Manager pode converter os conteúdos para o arquivo de instância única apenas um ponto de distribuição cada vez. Ao configurar atualizações de vários pontos de distribuição, os pontos de distribuição são colocados em fila para atualização e processados um de cada vez.  

Antes de atualizar um ponto de distribuição partilhado, certifique-se de que todos os conteúdos implementados no ponto de distribuição são migrados. Os conteúdos que não migrar antes de atualizar o ponto de distribuição não estarão disponíveis na hierarquia de destino após a atualização. Quando atualiza um ponto de distribuição, o conteúdo dos pacotes migrados é convertido para um formato compatível com o arquivo de instância única da hierarquia de destino.  

Para atualizar um ponto de distribuição a partir da consola do Configuration Manager, o servidor de sistema de sites do Configuration Manager 2007 tem de cumprir as seguintes condições:  

-   A configuração e a localização do ponto de distribuição deverão ser elegíveis para atualização.  

-   O computador de ponto de distribuição tem de ter espaço suficiente em disco para os conteúdos possam ser convertidos do formato de armazenamento de conteúdos do Configuration Manager 2007 para o formato de arquivo de instância única. Esta conversão necessita de um espaço em disco disponível equivalente ao tamanho do pacote mais volumoso que se encontra armazenado no ponto de distribuição.  

-   O computador do ponto de distribuição deverá estar a executar uma versão de sistema operativo que seja suportada como ponto de distribuição na hierarquia de destino.  

    > [!NOTE]  
    >  Quando o Configuration Manager verifica a elegibilidade de um ponto de distribuição para atualização, não valida a versão do sistema operativo do computador do ponto de distribuição.  

Para atualizar um ponto de distribuição no **administração** área de trabalho, expanda **migração**, expanda o **hierarquia de origem** nó e, em seguida, selecione o site que tem a distribuição ponto que pretende atualizar. Em seguida, no separador **Pontos de Distribuição Partilhados** do painel de detalhes, selecione o ponto de distribuição que pretende atualizar.  

Poderá confirmar que o ponto de distribuição está preparado para atualização verificando o estado da coluna **Elegível para Reatribuição** .  Em seguida, no Configuration Manager consola Friso, no **pontos de distribuição** separador o **ponto de distribuição** grupo, selecione **reatribuir**. Este procedimento abre um assistente que utilizar para concluir a atualização do ponto de distribuição.  

Ao atualizar um ponto de distribuição partilhado, deverá atribuir o ponto de distribuição a um site primário ou a um site secundário da sua preferência na hierarquia de destino. Após o ponto de distribuição estiver atualizado, gerir o ponto de distribuição como uma distribuição ponto na hierarquia de destino como qualquer outro ponto de distribuição.  

Pode monitorizar o progresso de uma atualização do ponto de distribuição na consola do Configuration Manager, selecionando o **migração de pontos de distribuição** nó sob o **migração** nó do **administração** área de trabalho. Também pode ver as informações do **Migmctrl.log** no servidor do site de administração central da hierarquia de destino, ou no **distmgr.log** do servidor do site na hierarquia de destino que gere o ponto de distribuição atualizado.  

> [!NOTE]  
>  Quando atualiza um ponto de distribuição à hierarquia de destino, a função de sistema de sites de ponto de distribuição é removida do site de origem do Configuration Manager 2007. No entanto, os pacotes que foram enviadas para o ponto de distribuição não sejam atualizados na hierarquia do Configuration Manager 2007. Na consola do Configuration Manager 2007, os pacotes que tinham sido enviados para o ponto de distribuição continuam a indicar o computador do sistema de sites como uma distribuição ponto com um **tipo** de **desconhecido**. As atualizações subsequentes do pacote no Configuration Manager 2007 resultarão na comunicação Distribution Manager erros no distmgr desse site quando o site tentar atualizar o pacote do sistema de sites desconhecido.  

Se optar por não atualizar um ponto de distribuição partilhado, é possível instalar um ponto de distribuição da hierarquia de destino num ponto de distribuição do Configuration Manager 2007 anterior. Antes de poder instalar o novo ponto de distribuição, primeiro deve desinstalar todas as funções de sistema de sites do Configuration Manager 2007 a partir do computador do ponto de distribuição. Isto inclui o site do Configuration Manager 2007 se se tratar de computador do servidor do site. Quando desinstala um ponto de distribuição do Configuration Manager 2007, o conteúdo que foi implementado para o ponto de distribuição não é eliminado do computador.  

###  <a name="BKMK_UpgradeSS"></a>Planear a atualização de sites secundários do Configuration Manager 2007  
 Ao utilizar a migração para atualizar um ponto de distribuição partilhado que esteja alojado num servidor do site secundário do Configuration Manager 2007, o Configuration Manager atualiza a função do sistema de sites ponto de distribuição para ser um ponto de distribuição na hierarquia de destino. Também desinstala o site secundário da hierarquia de origem. O resultado é um ponto de distribuição do System Center Configuration Manager, mas nenhum site secundário.  

 Para um ponto de distribuição no computador do servidor de site para ser elegível para atualização do Configuration Manager tem de conseguir desinstalar o site secundário e cada uma das funções de sistema de sites nesse computador. Normalmente, um ponto de distribuição partilhado numa partilha de servidor do Configuration Manager 2007 é elegível para atualização. No entanto, se existir uma partilha de servidor no servidor do site secundário, o site secundário e os pontos de distribuição partilhados nesse computador não serão elegíveis para atualização. Isto acontece porque a partilha do servidor é tratada como um objeto de sistema de sites adicionais quando o processo tenta desinstalar o site secundário e este processo não é possível instalar este objeto. Neste cenário, poderá ativar um ponto de distribuição padrão no servidor de site secundário e, em seguida, redistribuir os conteúdos a esse ponto de distribuição padrão. Este processo não utiliza largura de banda de rede, e quando tiver terminado, pode desinstalar o ponto de distribuição na partilha do servidor, remover a partilha do servidor e, em seguida, atualizar o ponto de distribuição e o site secundário.  

 Antes de atualizar um ponto de distribuição partilhado, analise a configuração de ponto de distribuição no Configuration Manager 2007 para evitar a atualização de um ponto de distribuição num site secundário que pretenda continuar a utilizar com o Configuration Manager 2007. Esta é uma boa prática, uma vez depois de atualizar um ponto de distribuição partilhado que se encontra no servidor do site secundário, o servidor de sistema de sites é removido da hierarquia do Configuration Manager 2007 e já não está disponível para utilização nessa hierarquia. Quando o site secundário for removido, quaisquer pontos de distribuição restantes nesse site secundário ficarão órfãos. Isto significa que deixam de ser geridos a partir do Configuration Manager 2007 e já não são partilhados ou elegíveis para atualização.  

> [!WARNING]  
>  Quando visualiza pontos de distribuição partilhados na consola do Configuration Manager, não existe nenhuma indicação explícita de que é um ponto de distribuição partilhado num servidor de sistema de sites remoto ou no servidor do site secundário.  

 Quando tiver um site secundário numa localização de rede remota que seja principalmente utilizada para controlar a implementação de conteúdos nessa localização remota, considere atualizar os sites secundários que tenham um ponto de distribuição partilhado. Uma vez que pode configurar o controlo de largura de banda quando distribui conteúdo por um ponto de distribuição do System Center Configuration Manager, muitas vezes, pode atualizar um site secundário para um ponto de distribuição, configurar o ponto de distribuição para os controlos de largura de banda e evitar a instalação de um site secundário nessa localização de rede da hierarquia de destino.  

 O processo para atualizar um ponto de distribuição partilhado num servidor de site secundário é igual a qualquer outra atualização do ponto de distribuição partilhados. Conteúdos são copiados e convertidos para o arquivo de instância única utilizado pela hierarquia de destino. No entanto, quando atualiza um ponto de distribuição partilhado que se encontra no servidor do site secundário, o processo de atualização também desinstalará o ponto de gestão (caso exista) e, em seguida, desinstala o site secundário do servidor. O resultado é que o site secundário é removido da hierarquia do Configuration Manager 2007. Para desinstalar o site secundário, o Configuration Manager utiliza a conta que está configurada para recolher dados do site de origem.  

 Durante a atualização, existe um atraso entre quando o site secundário do Configuration Manager 2007 é desinstalado e o início da instalação do ponto de distribuição na hierarquia de destino. O ciclo de recolha de dados determina este atraso de até quatro horas. O atraso destina-se reservar tempo para o site secundário desinstalar antes do início da instalação do novo ponto de distribuição.  

 Para mais informações sobre como atualizar um ponto de distribuição partilhado, consulte o artigo [pontos de distribuição partilhados do plano para atualização do Configuration Manager 2007](#Planning_to_Upgrade_DPs).  

##  <a name="BKMK_ReassignDistPoint"></a>Plano para reatribuir os pontos de distribuição do System Center Configuration Manager  
 Quando migra a partir de uma versão suportada do System Center 2012 Configuration Manager para uma hierarquia com a mesma versão, poderá reatribuir um ponto de distribuição partilhados a partir da hierarquia de origem a um site na hierarquia de destino. É como o conceito de atualização de um ponto de distribuição do Configuration Manager 2007 para se tornar um ponto de distribuição na hierarquia de destino. Pode reatribuir os pontos de distribuição de sites primários e sites secundários. A ação para reatribuir um ponto de distribuição remove o ponto de distribuição da hierarquia de origem e converte o computador e o respetivo ponto de distribuição de um servidor de sistema de sites do site que selecionar na hierarquia de destino.  

 Ao reatribuir um ponto de distribuição, não necessita de redistribuir os conteúdos migrados que se encontravam alojados no ponto de distribuição do site de origem. Além disso, ao contrário da atualização de um ponto de distribuição do Configuration Manager 2007, reatribuição de um ponto de distribuição não necessita de espaço em disco adicional no computador do ponto de distribuição. Isto acontece porque a partir do System Center 2012 Configuration Manager, os pontos de distribuição utilizam o formato de arquivo de instância única para o conteúdo. Os conteúdos no computador do ponto de distribuição não necessitam de ser convertidos quando o ponto de distribuição é reatribuído entre hierarquias.  

 Para um ponto de distribuição do System Center 2012 Configuration Manager ser elegível para reatribuição, deverão satisfazer os seguintes critérios:  

-   Um ponto de distribuição partilhado tem de ser instalado num computador que não o do servidor do site.  

-   Um ponto de distribuição partilhado não pode ser localizado conjuntamente com quaisquer funções adicionais do sistema de sites.  

Para identificar os pontos de distribuição que são elegíveis para reatribuição na consola do Configuration Manager no **hierarquia de origem** nó, selecione um site de origem e, em seguida, selecione o **pontos de distribuição partilhados** separador. Pontos de distribuição elegível apresentam **Sim** no **elegíveis para reatribuição** coluna (esta coluna era designada **elegível para atualização** anteriores ao System Center 2012 R2 Configuration Manager).  

###  <a name="BKMK_ReassignProcess"></a> Processo de reatribuição de pontos de distribuição  
 Pode utilizar a consola do Configuration Manager para reatribuir os pontos de distribuição que tenha partilhado a partir de uma hierarquia de origem ativa. Quando reatribui um ponto de distribuição partilhado, o ponto de distribuição é desinstalado do site de origem e, em seguida, instalado como um ponto de distribuição que esteja anexado a um site primário ou secundário que esteja especificado na hierarquia de destino.  

 Para reatribuir o ponto de distribuição, a hierarquia de destino utiliza a conta de acesso do Site de origem que está configurada para recolher dados a partir do fornecedor de SMS do site de origem. Para obter informações sobre as permissões necessárias e pré-requisitos adicionais, consulte o artigo [os pré-requisitos da migração no System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrar vários pontos de distribuição partilhado ao mesmo tempo
A partir da versão 1610, pode utilizar **ponto de distribuição reatribuir** para que o processo do Configuration Manager em paralelo reatribuição de até 50 pontos de distribuição partilhados ao mesmo tempo. Isto inclui pontos de distribuição partilhados a partir de sites de origem suportada que executam:  
- Configuration Manager 2007
- System Center 2012 Configuration Manager
- System Center 2012 R2 Configuration Manager
- O System Center Configuration Manager (ramo atual)

Quando reatribuir pontos de distribuição, cada ponto de distribuição tem ser elegível para ser atualizado ou reatribuído. O nome da ação e o processo envolvidos (atualização ou reatribuição) depende do executa o site de origem que versão do Configuration Manager. Os resultados de fim para ambas as ações são o mesmo: o ponto de distribuição é atribuído a um dos seus sites secundários atual com o respetivo conteúdo no local.

Antes da versão 1610, Configuration Manager foi possível processar apenas um ponto de distribuição cada vez. Agora pode reatribuir os pontos de distribuição tantos que quiser com as seguintes advertências:  
- Apesar de não for possível pontos de distribuição SelecçõesMúltiplas para ser reatribuídas, quando tiver colocadas em fila de mais do que um, o Configuration Manager será processado-los paralelamente, em vez de aguardar para concluir uma antes de iniciar a próxima.  
- Por predefinição, até 50 distribuição pontos são processados paralelamente cada vez. Após a conclusão, a reatribuição do primeiro ponto de distribuição do Configuration Manager irá começar a processar o 51st e assim sucessivamente.  
- Quando utilizar o SDK do Configuration Manager, pode alterar **SharedDPImportThreadLimit** para ajustar o número reatribuídas de pontos de distribuição do Configuration Manager pode processar em paralelo.


##  <a name="About_Migrating_Content"></a>Atribuir propriedade dos conteúdos após a migração de conteúdo  
 Ao migrar conteúdo para implementações,necessita de atribuir o objeto do conteúdo a um site da hierarquia de destino. Em seguida, este site torna-se o proprietário desse conteúdo na hierarquia de destino. Embora o site de nível superior da hierarquia de destino seja o site que migra os metadados do conteúdo, é o site atribuído que utiliza ficheiros de origem originais para obter os conteúdos através da rede.  

 Para reduzir ao mínimo a largura de banda de rede que é utilizada para migrar os conteúdos, pondere transferir a propriedade dos conteúdos para um site da hierarquia de destino que esteja num local próximo da rede da localização dos conteúdos na hierarquia de origem. Dado que as informações sobre os conteúdos da hierarquia de destino são partilhadas globalmente, ficarão disponíveis em todos os sites.  

 Embora as informações sobre o conteúdo sejam partilhadas para todos os sites utilizando a replicação de base de dados, qualquer conteúdo atribuído a um site primário e, em seguida, implementar a distribuição pontos noutros sites primários transferências através da replicação baseada em ficheiros. Esta transferência é encaminhada através do site de administração central e, em seguida, para o site primário adicional. Pode diminuir as transferências de dados em redes com pouca largura de banda centralizar os pacotes que pretende distribuir por vários sites primários antes ou durante a migração quando atribui um site como proprietário dos conteúdos.


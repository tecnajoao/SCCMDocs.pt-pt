---
title: Cache ponto a ponto do cliente
titleSuffix: Configuration Manager
description: Utilize a cache ponto a ponto do cliente para localizações de origem durante a implantação de conteúdo com o Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c3dc6189f73b939f632581a8b50f05a72310111d
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/23/2018
ms.locfileid: "42756001"
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Cache ponto a ponto para clientes do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1101436--> Utilize a cache ponto a ponto para o ajudar a gerir a implementação de conteúdo para clientes em localizações remotas. Cache ponto a ponto é uma solução incorporada do Configuration Manager que permite que os clientes partilhem conteúdos com outros clientes diretamente a partir da respetiva cache local.   

> [!Note]  
> O Configuration Manager não permite esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  



## <a name="overview"></a>Descrição Geral

Definições de:  

- **Cliente de cache ponto a ponto**: Qualquer cliente de Configuration Manager que transfere o conteúdo de um elemento de rede  

- **Origem de cache ponto a ponto**: Um cliente do Configuration Manager que ativar para a cache ponto a ponto e que tem o conteúdo para partilhar com outros clientes  

Utilize as definições de cliente para permitir que os clientes para a origem de cache ponto a ponto. Não precisa de permitir que os clientes de cache ponto a ponto. Quando ativar os clientes de origens de cache ponto a ponto, o ponto de gestão inclui-las na lista de origens de localização de conteúdo.<!--510397--> Para obter mais informações sobre este processo, consulte [operações](#operations).  

Uma origem de cache ponto a ponto tem de ser membro do grupo de limites atual do cliente de cache ponto a ponto. O ponto de gestão não inclui origens da cache ponto a ponto de um grupo de limite vizinho na lista de fontes de conteúdo, que ele fornece ao cliente. Incluir apenas os pontos de distribuição de um grupo de limite vizinho. Para obter mais informações sobre grupos de limites atuais e vizinhança, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).<!--SCCMDocs issue 685-->  

O cliente do Configuration Manager utiliza a cache ponto a ponto para atender a outros clientes de todos os tipos de conteúdo na cache. Este conteúdo inclui ficheiros do Office 365 e ficheiros de instalação rápida.<!--SMS.500850-->  

Cache ponto a ponto não substitui a utilização de outras soluções, como o Windows BranchCache ou Otimização da entrega. Cache ponto a ponto funciona, juntamente com outras soluções. Essas tecnologias lhe dar mais opções para estender as soluções de implementação de conteúdos tradicionais, como pontos de distribuição. Cache ponto a ponto é uma solução personalizada com nenhuma dependência do BranchCache. Se não ativar ou utilizar o BranchCache, cache ponto a ponto ainda funciona.  

  > [!Note]  
  > A partir da versão 1802, Windows BranchCache está sempre ativada nos implementações. A definição para **permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede** é removido.<!--SCCMDocs issue 539--> Se o ponto de distribuição suporta e está ativada nas definições do cliente, os clientes utilizam o BranchCache. Para obter mais informações, consulte [configurar o BranchCache](/sccm/core/clients/deploy/about-client-settings#configure-branchcache).<!--SCCMDocs issue 735-->   



## <a name="operations"></a>Operações

Para ativar a cache ponto a ponto, implementar o [definições de cliente](#bkmk_settings) a uma coleção. Em seguida, os membros dessa coleção atuam como uma origem de cache ponto a ponto para outros clientes no mesmo grupo de limites.  

 -  Um cliente que funciona como uma origem de conteúdo do elemento de rede envia uma lista de conteúdo em cache disponível para o ponto de gestão.  

 -  Outro cliente no mesmo grupo de limites faz um pedido de localização de conteúdo ao ponto de gestão. O servidor devolve a lista de possível fontes de conteúdo. Esta lista inclui cada origem de cache ponto a ponto que tem o conteúdo e está online. Ele também inclui os pontos de distribuição e em outros locais de origem de conteúdo nesse grupo de limites. Para obter mais informações, consulte [prioridade de origem de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#content-source-priority).  

 -  Como sempre, o cliente que está a procurar o conteúdo seleciona uma origem na lista fornecida. O cliente tenta, em seguida obter o conteúdo.  

> [!NOTE]  
> Se o cliente reverterá para um grupo de limite vizinho para o conteúdo, o ponto de gestão não adiciona as origens de cache ponto a ponto do grupo de limite vizinho à lista de potenciais localizações de origem de conteúdo.  

Escolha apenas os clientes mais indicados como origens de cache ponto a ponto. Avalie a adequação de cliente com base em atributos como tipo de chassi, espaço em disco e conectividade de rede. Para obter mais informações que podem ajudar a selecionar os melhores clientes a utilizar para a cache ponto a ponto, consulte [este blog por um consultor da Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).


### <a name="limited-access-to-a-peer-cache-source"></a>Acesso limitado a uma origem de cache ponto a ponto  

Uma origem de cache ponto a ponto rejeita pedidos de conteúdo, quando ele cumpre qualquer uma das seguintes condições no momento que um item de mesmo nível solicita o conteúdo:  

  -  Modo de pouca bateria  

  -  Carga do processador excede 80%  

  -  E/s de disco tem um *AvgDiskQueueLength* que excede a 10  

  -  Não existem ligações não é mais disponíveis para o computador  

> [!Tip]  
> Configurar estas definições com o servidor de configuração classe WMI de cliente para a funcionalidade de origem do elemento de rede (*SMS_WinPEPeerCacheConfig*) no SDK do Configuration Manager.  

Quando a origem de cache ponto a ponto rejeita um pedido para o conteúdo, o cliente de cache ponto a ponto continua procurar o ressarcimento de conteúdo a partir de sua lista de localizações de origem de conteúdo.   



## <a name="requirements"></a>Requisitos

- Todas as versões do Windows listadas como suportado no oferece suporte a cache ponto a ponto [sistemas operativos suportados por clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices). Sistemas de operativos não Windows não são suportados como origens de cache ponto a ponto ou clientes de cache ponto a ponto.  

- Uma origem de cache ponto a ponto tem de ser um cliente de Configuration Manager associado a um domínio. No entanto, um cliente que não está associado a um domínio pode obter o conteúdo de uma origem de cache de elemento de rede associados a um domínio.  

- Os clientes só podem transferir conteúdo a partir de origens de cache ponto a ponto no respetivo grupo de limites atual.  

- R [conta de acesso de rede](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account) não é necessário com a seguinte exceção:  

    - Configure uma conta de acesso de rede no site, quando um cliente de cache com capacidade de ponto a ponto executada uma sequência de tarefas a partir do Centro de Software e é reiniciado para uma imagem de arranque. Quando o dispositivo estiver no Windows PE, ele usa a conta de acesso de rede para obter o conteúdo de origem de cache ponto a ponto.  

    - Quando for necessário, a origem de cache ponto a ponto utiliza a conta de acesso de rede para autenticar pedidos de transferência de colegas. Esta conta requer permissões de utilizador de domínio apenas para essa finalidade.  

- Submissão de deteção de heartbeat do cliente última determina o limite atual de uma origem de cache ponto a ponto. Um cliente fizer roaming para um grupo de limites diferentes ainda pode ser um membro do respetivo grupo de limites antigo para fins de cache ponto a ponto. Este comportamento resulta num cliente a ser oferecido um elemento de origem de cache que não esteja na respetiva localização de rede imediata. Não permitir que os clientes de roaming como uma origem de cache ponto a ponto.<!--SCCMDocs issue 641-->  

- Antes de tentar transferir conteúdo, o cliente de cache ponto a ponto primeiro valida que a origem de cache ponto a ponto está online.<!--sms.498675--> Essa validação ocorre via o "canal rápido" para a notificação de cliente, que utiliza a porta TCP 10123.<!--511673-->  

> [!Note]  
> Para tirar partido das novas funcionalidades do Configuration Manager, primeiro de atualizar os clientes para a versão mais recente. Enquanto a nova funcionalidade surge na consola do Configuration Manager ao atualizar a consola e do site, o cenário completo não é funcional até que a versão do cliente também é a versão mais recente.  



## <a name="bkmk_settings"></a> Definições de cliente de cache ponto a ponto

Para obter mais informações sobre as definições de cliente de cache ponto a ponto, consulte [definições de cache do cliente](/sccm/core/clients/deploy/about-client-settings#client-cache-settings). 

Para obter mais informações sobre como configurar estas definições, consulte [como configurar as definições de cliente](/sccm/core/clients/deploy/configure-client-settings).

No elemento de rede habilitados em cache os clientes que utilizam o Firewall do Windows, o Configuration Manager configura as portas de firewall que especificou nas definições do cliente.



## <a name="bkmk_parts"></a> Suporte de transferência parcial
<!--1357346--> A partir da versão 1806, origens de cache ponto a ponto do cliente agora podem dividir o conteúdo em partes. Estas peças minimizam a transferência de rede para reduzir a utilização da WAN. O ponto de gestão fornece controlo mais detalhado das partes de conteúdo. Ele tenta eliminar mais do que uma transferência do conteúdo do mesmo por grupo de limites. 


### <a name="example-scenario"></a>Cenário de exemplo

A Contoso tiver um único site primário com dois grupos de limites: Sede (Sedes) e sucursal. Existe uma relação de contingência de 30 minutos entre os grupos de limites. O ponto de gestão e o ponto de distribuição para o site são apenas em limites do HQ. O local de filial não tem nenhum ponto de distribuição local. Dois dos quatro clientes da sucursal são configurados como origens de cache ponto a ponto. 

![Diagrama de configuração de rede, tal como descrito para o cenário de exemplo](media/1357346-peer-cache-source-parts.png)

1. O direcionamento de uma implementação com o conteúdo para todos os quatro clientes na sucursal. Distribuídas apenas o conteúdo ao ponto de distribuição.  

2. Client3 e Client4 não tem uma origem local para a implementação. O ponto de gestão instrui os clientes de espera de 30 minutos antes de reverter para o grupo de limites remoto.  

3. Client1 (PCS1) é a primeira origem de cache ponto a ponto para atualizar a política com o ponto de gestão. Porque este cliente está ativado como uma origem de cache ponto a ponto, o ponto de gestão instrui-lo para iniciar imediatamente o download parte A partir do ponto de distribuição.  

4. Quando Client2 (PCS2) entra em contacto com o ponto de gestão, como parte A já está em curso, mas não ainda concluído, o ponto de gestão instrui-lo para iniciar imediatamente a baixar a parte B do ponto de distribuição.  

5. Conclusão da transferência de parte A PCS1 e notifica imediatamente o ponto de gestão. Como parte de B já está em curso, mas não ainda concluído, o ponto de gestão instrui-lo para iniciar a transferência de parte C do ponto de distribuição.  

6. PCS2 conclusão da transferência de parte B e notifica imediatamente o ponto de gestão. O ponto de gestão instrui-lo para iniciar a transferência de parte D do ponto de distribuição.  

7. PCS1 conclusão da transferência de parte C e notifica imediatamente o ponto de gestão. O ponto de gestão informa o-lo de que existem não existem mais partes do ponto de distribuição remoto. O ponto de gestão instrui a transferir a parte B de seu elemento de rede local, PCS2.  

8. Este processo continua até que ambas as origens de cache ponto a ponto do cliente tem todas as partes uns dos outros. O ponto de gestão dá prioridade partes do ponto de distribuição remoto antes de instruindo as origens de cache ponto a ponto para transferir partes de elementos locais.  

9. Client3 é o primeiro a atualizar a política após o período de contingência de 30 minutos expira. Agora ele verifica novamente com o ponto de gestão, que informa o cliente de novas fontes de locais. Em vez de transferirem o conteúdo na totalidade do ponto de distribuição na WAN, transfere o conteúdo na totalidade de uma das origens de cache ponto a ponto do cliente. Os clientes priorizar as origens do elemento de rede local. 

> [!Note]  
> Se o número de origens de cache ponto a ponto do cliente é superior ao número de partes de conteúdo, em seguida, o ponto de gestão instrui as origens de cache ponto a ponto adicional a aguardar para contingência como um cliente normal. 


### <a name="configure-partial-download"></a>Configurar a transferência parcial

1. Configurar [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) e origens de cache ponto a ponto por normal.  

2. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione **Sites**. Clique em **definições de hierarquia** na faixa de opções.  

3. Sobre o **gerais** separador, ative a opção de **configurar origens de cache ponto a ponto de cliente para dividir o conteúdo em partes**.  

4. Crie uma implementação necessária com o conteúdo.  

   > [!Note]  
   > Esta funcionalidade só funciona quando o cliente transfere conteúdo em segundo plano, tal como com uma implementação necessária. Downloads de sob demanda, como quando o usuário instala uma implementação disponível no Centro de Software, se comporta como de costume.  

Para vê-los a lidar com a transferência de conteúdo em partes, examine o **ContentTransferManager.log** na origem da cache ponto a ponto do cliente e o **MP_Location.log** no ponto de gestão.  



## <a name="guidance-for-cache-management"></a>Orientações para a gestão de cache
<!--510645--> Cache ponto a ponto se baseia em cache do cliente do Configuration Manager para partilhar conteúdo. Considere os seguintes pontos para gerir a cache do cliente no seu ambiente:  

- Não é a cache do cliente do Configuration Manager, como a biblioteca de conteúdos num ponto de distribuição. Ao gerir o conteúdo que distribui para um ponto de distribuição, o cliente do Configuration Manager gerencia automaticamente o conteúdo em seu cache. Existem definições e métodos para ajudar a controlar o conteúdo que está no cache de uma origem de cache ponto a ponto. Para obter mais informações, consulte [configurar a cache do cliente para clientes do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache).  

- Tamanho da normal cache e a manutenção se aplica a origens de cache ponto a ponto. Para obter mais informações, consulte [configurar o tamanho da cache do cliente](/sccm/core/clients/deploy/about-client-settings#configure-client-cache-size). Considere o tamanho do maior conteúdo tal como a atualização de SO de pacotes ou ficheiros de atualização rápida do Windows 10. Compare sua necessidade para este conteúdo contra o espaço em disco disponível em origens de cache ponto a ponto.  

- O cliente de origem de cache ponto a ponto atualiza a última hora referenciada de conteúdo na cache do quando transfere-o um elemento de rede. O cliente utiliza este timestamp quando ele mantém automaticamente seu cache, primeiro a remover o conteúdo mais antigo. Para que ele deve esperar para remover o conteúdo que configurar o peering entre clientes de cache mais frequentemente transferir, se houver.  

- Se necessário, durante uma sequência de tarefas de implementação do sistema operacional, utilize o **SMSTSPreserveContent** variável para manter conteúdo na cache do cliente. Para obter mais informações, consulte [variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSPreserveContent).  

- Se necessário, ao criar o seguinte software, utilize a opção para **manter conteúdo na cache do cliente**:  
    - Aplicações
    - Pacotes
    - Imagens do sistema operacional
    - Pacotes de atualização do SO
    - Imagens de arranque



## <a name="monitoring"></a>Monitorização   

Para ajudar a compreender a utilização da cache ponto a ponto, veja a **origens de dados do cliente** dashboard. Para obter mais informações, consulte [dashboard de origens de dados do cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

Também utilizar relatórios para ver a utilização de cache ponto a ponto. Na consola, vá para o **monitorização** área de trabalho, expanda **Reporting**e selecione o **relatórios** nó. Os relatórios seguintes todas têm um tipo de **conteúdo de distribuição de Software**:  

1.  **Configurar o peering entre a rejeição de conteúdo de origem da cache**: A frequência com que as origens de cache ponto a ponto num grupo de limites rejeitam um pedido de conteúdo.  

    > [!Note]  
    > **Problema conhecido**<!--486652-->: Quando fazer busca detalhada nos resultados como *MaxCPULoad* ou *MaxDiskIO*, poderá receber um erro que indica o relatório ou não é possível obter detalhes. Para contornar este problema, utilize os outros dois relatórios que mostram diretamente os resultados.  

2. **Configurar o peering entre a rejeição de conteúdo de origem da cache por condição**: Mostra os detalhes de rejeição para um tipo de grupo ou de rejeição de limite especificado. 

    > [!Note]  
    > **Problema conhecido**<!--486652-->: Não é possível selecionar a partir de parâmetros disponíveis e em vez disso, tem de introduzi-los manualmente. Introduza os valores para *nome do grupo de limites* e *tipo de rejeição* como visto no **configurar o peering entre a rejeição de conteúdo de origem da cache** relatório. Por exemplo, para *tipo de rejeição* poderá introduzir *MaxCPULoad* ou *MaxDiskIO*.  

3. **Configurar o peering em detalhes de rejeição do conteúdo da origem de cache**: Mostre o conteúdo que o cliente foi a pedir quando rejeitado.  

    > [!Note]  
    > **Problema conhecido**<!--486652-->: Não é possível selecionar a partir de parâmetros disponíveis e em vez disso, tem de introduzi-los manualmente. Introduza o valor para *tipo de rejeição* tal como apresentado no **configurar o peering entre a rejeição de conteúdo de origem da cache** relatório. Em seguida, introduza o *ID de recurso* para a origem de conteúdo que deseja obter mais informações. 
    > 
    > Para localizar o ID de recurso da origem de conteúdo:  
    > 
    > 1. Encontrar o nome de computador que é apresentado como o *origem de cache ponto a ponto* nos resultados da **configurar o peering entre a rejeição de conteúdo de origem da cache por condição** relatório.  
    > 
    > 2. Vá para o **ativos e compatibilidade** área de trabalho, selecione a **dispositivos** nó e procure o nome do computador. Utilize o valor da coluna de ID de recurso.  


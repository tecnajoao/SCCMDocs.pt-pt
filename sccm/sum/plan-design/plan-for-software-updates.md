---
title: Planear atualizações de software
titleSuffix: Configuration Manager
description: Um plano para a infraestrutura de ponto de atualização de software é essencial antes de utilizar as atualizações de software num ambiente de produção do Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.collection: M365-identity-device-management
ms.openlocfilehash: a4100bca2f1cd1f770c2e739ec229dc020d5d8d8
ms.sourcegitcommit: 5f17355f954b9d9e10325c0e9854a9d582dec777
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/21/2019
ms.locfileid: "58329588"
---
# <a name="plan-for-software-updates-in-configuration-manager"></a>Planear atualizações de software no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de utilizar as atualizações de software num ambiente de produção do Configuration Manager, é importante, a percorrer o processo de planejamento. Ter um bom plano para a infraestrutura de ponto de atualização de software é a chave para uma implementação de atualizações de software bem-sucedido.



## <a name="capacity-planning-recommendations-for-software-updates"></a>Recomendações de planeamento da capacidade para atualizações de software  

Esta seção inclui os seguintes subtópicos:  
- [Planeamento da capacidade para o ponto de atualização de software](#BKMK_SUMCapacity)
- [Planejamento de capacidade do software de objetos de atualizações](#bkmk_sum-capacity-obj)  


Utilize as seguintes recomendações como uma linha de base. Esta linha de base ajuda-o a determinar as informações para a capacidade de atualizações de software de planeamento que são adequadas para a sua organização. Os requisitos de capacidade real podem variar das recomendações apresentadas neste artigo, consoante os seguintes critérios: 
- Seu ambiente de rede específico
- Sistema de sites de ponto do hardware que utiliza para alojar a atualização de software
- O número de clientes geridos
- As outras funções do sistema de site instaladas no servidor  


###  <a name="BKMK_SUMCapacity"></a> Planeamento da capacidade para o ponto de atualização de software  

O número de clientes suportados depende da versão do Windows Server Update Services (WSUS) que é executado no ponto de atualização de software. Também depende se a função de sistema de sites de ponto de atualização de software coexiste com uma outra função de sistema de sites:  

-   O ponto de atualização de software consegue suportar até 25.000 clientes, quando o WSUS é executado no servidor de ponto de atualização de software e o ponto de atualização de software coexiste com uma outra função de sistema de sites.  

-   O ponto de atualização de software consegue suportar até 150.000 clientes quando um servidor remoto cumpre os requisitos do WSUS, é utilizado o WSUS com o Configuration Manager e configure as seguintes definições:

    Agrupamentos de aplicações do IIS:
    - Aumente o comprimento da fila WsusPool para 2000
    - Aumentar o limite de memória privada WsusPool x4 vezes, ou definir como 0 (ilimitado). Por exemplo, se o limite predefinido é 1,843,200 KB, aumentá-la para 7,372,800. Para obter mais informações, consulte esta [mensagem de blogue de equipa de suporte do Configuration Manager](https://blogs.technet.microsoft.com/configurationmgr/2015/03/23/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/).  

    Para obter mais informações sobre os requisitos de hardware para o ponto de atualização de software, consulte [hardware para sistemas de sites recomendado](/sccm/core/plan-design/configs/recommended-hardware#a-namebkmkscalesiesystemsa-site-systems).  


### <a name="bkmk_sum-capacity-obj"></a> Planejamento de capacidade do software de objetos de atualizações  

Utilize as seguintes informações de capacidade para planear para objetos de atualizações de software:  

#### <a name="limit-of-1000-software-updates-in-a-deployment"></a>Limite de 1000 atualizações de software numa implementação  
Limite o número de atualizações de software a 1000 para cada implementação de atualização de software. Quando cria uma regra de implementação automática (ADR), especifique os critérios que limita o número de atualizações de software. O ADR falha quando os critérios especificados devolve mais de 1000 atualizações de software. Verificar o estado da ADR do **regras de implementação automática** nó na consola do Configuration Manager. Ao implementar manualmente atualizações de software, não selecione mais de 1000 atualizações para implementar.  

Também limitam o número de atualizações de software a 1000 numa linha de base de configuração. Para obter mais informações, consulte [criar linhas de base de configuração](/sccm/compliance/deploy-use/create-configuration-baselines).



##  <a name="BKMK_SUPInfrastructure"></a> Determinar a infraestrutura do ponto de atualização de software  

Esta seção inclui os seguintes subtópicos:    
- [Lista de pontos de atualização de software](#BKMK_SUPList)
- [Mudança do ponto de atualização de software](#BKMK_SUPSwitching)
- [Mudar manualmente clientes para um novo ponto de atualização de software](#BKMK_ManuallySwitchSUPs)
- [Pontos de atualização de software numa floresta não fidedigna](#BKMK_SUP_CrossForest)
- [Utilizar um servidor WSUS existente como origem de sincronização no site de nível superior](#BKMK_WSUSSyncSource)
- [Ponto de atualização de software num site secundário](#BKMK_SUPSecSite)  
- [Plano para clientes baseados na internet](#bkmk_internet-clients)  
- [Planear o conteúdo de atualização de software](#bkmk_content)  
- [Planear atualizações de terceiros](#bkmk_thirdparty)  


O site de administração central e todos os sites primários subordinados têm de ter um ponto de atualização de software. Quando planear a infraestrutura de ponto de atualização de software de, determine as seguintes dependências:
 - Onde instalar o ponto de atualização de software para o site  
 - Que sites necessitam de um ponto de atualização de software que aceita comunicações de clientes baseados na internet
 - Se precisa de um software de ponto de atualização no sites secundários  

> [!IMPORTANT]  
>  Para obter mais informações sobre as dependências internas e externas que são necessários para atualizações de software, consulte [pré-requisitos para atualizações de software](prerequisites-for-software-updates.md).  

Adicione vários pontos de atualização de software num site primário do Configuration Manager para fornecer tolerância a falhas. O design de ativação pós-falha do ponto de atualização de software é diferente do que o modelo de aleatoriedade puro que é utilizado na conceção para pontos de gestão. Ao contrário do design de pontos de gestão, existem cliente e rede custos de desempenho no design de ponto de atualização de software quando os clientes mudarem para um novo ponto de atualização de software. Quando o cliente muda para um novo servidor WSUS para analisar a existência de atualizações de software, o resultado é um aumento do tamanho do catálogo e exigências associadas do lado do cliente e a nível do desempenho da rede. Por conseguinte, o cliente preserva a afinidade com o último ponto de atualização de software do qual foi analisado com êxito.  

O primeiro ponto de atualização de software que instalar num site principal é a origem de sincronização para todos os pontos de atualização de software adicionais que adicionar no site primário. Depois de adicionar pontos de atualização de software e iniciar a sincronização, ver o estado dos pontos de atualização de software e da origem de sincronização a **estado de sincronização de ponto de atualização de Software** nó o  **Monitorização** área de trabalho.  

Quando existe uma falha de ponto de atualização de software configurado como origem de sincronização para o site, remova manualmente a função com falha. Em seguida, selecione um novo ponto de atualização de software para utilizar como origem de sincronização. Para obter mais informações, consulte [remover a função de sistema de sites de ponto de atualização de software](../get-started/remove-a-software-update-point.md).  


###  <a name="BKMK_SUPList"></a> Lista de pontos de atualização de software  

O Configuration Manager fornece ao cliente uma lista de ponto de atualização de software nos seguintes cenários:  

- Um novo cliente recebe a política para ativar as atualizações de software  

- Um cliente não é possível contactar o respetivo ponto de atualização de software atribuído e precisa de mudar para outra  

O cliente seleciona aleatoriamente um ponto de atualização de software a partir da lista. Ele dá prioridade os pontos de atualização de software na mesma floresta. O Configuration Manager fornece aos clientes uma lista diferente, dependendo do tipo de cliente:  

-   **Clientes baseados na intranet**: Receba uma lista de pontos de atualização de software que pode configurar para permitir ligações apenas a partir da intranet, ou uma lista de pontos de atualização de software que permitem ligações de cliente de internet e intranet.  

-   **Clientes baseados na Internet**: Receba uma lista de pontos de atualização de software que pode configurar para permitir ligações apenas a partir da internet, ou uma lista de pontos de atualização de software que permitem ligações de cliente de internet e intranet.  


###  <a name="BKMK_SUPSwitching"></a> Mudança do ponto de atualização de software  

> [!NOTE]  
> Os clientes utilizam grupos de limites para localizar um ponto de atualização de software novo. Se o ponto de atualização de software atual já não estiver acessível, eles também utilizam grupos de limites de contingência e encontrar um novo. Adicione pontos de atualização de software individuais aos grupos de limites diferentes para controlar quais os servidores em que um cliente pode encontrar. Para obter mais informações, consulte [pontos de atualização de Software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points).  

Se tiver vários pontos de atualização de software num site, e um deles falha ou fica indisponível, os clientes estabelecerão para um ponto de atualização de software diferentes. Com este servidor novo, os clientes continuam a analisar as mais recentes atualizações de software. Quando um cliente pela primeira vez é atribuído um ponto de atualização de software, esta permanece atribuída para que software de ponto de atualização, a menos que a falha na análise.  

A análise da existência de atualizações de software pode falhar com uma série de diferentes códigos de erro de repetições e não repetições. Quando a análise falha com um código de erro de repetição, o cliente inicia um processo de repetição para procurar as atualizações de software no ponto de atualização de software. As condições de alto nível que resultam num código de erro de repetição são normalmente causadas porque o servidor WSUS está indisponível ou porque está temporariamente sobrecarregado. Quando o cliente não consegue verificar a existência de atualizações de software, ele usa o seguinte processo:  

1.  O cliente verifica a existência de atualizações de software:  
    - Na respetiva hora agendada
    - Quando é manualmente executado a partir do painel de controlo no cliente
    - Quando é manualmente executado a partir da consola do Configuration Manager através de uma ação de notificação do cliente
    - Quando é executado a partir de um método do SDK do Configuration Manager  

2.  Se a análise falhar, o cliente aguarda 30 minutos para repetir a análise. Ele usa o mesmo ponto de atualização de software.  

3.  O cliente tenta novamente um mínimo de quatro vezes a cada 30 minutos. Após a quarta falha, e depois de aguardar dois minutos adicionais, o cliente se move para o próximo ponto de atualização de software na respetiva lista.  

4.  O cliente se repetir esse processo com o novo ponto de atualização de software. Após uma análise com êxito, o cliente continua ligar ao ponto de atualização de software novo.  

A lista seguinte fornece informações adicionais a serem considerados para a repetição de ponto de atualização de software e a alternância de cenários:  

-   Se um cliente está desligado da intranet e não consegue verificar a existência de atualizações de software, não muda para outro ponto de atualização de software. Esta falha é esperada, porque o cliente não é possível aceder à rede interna ou um ponto de atualização de software que permite ligações a partir da intranet. O cliente do Configuration Manager determina a disponibilidade do ponto de atualização de software de intranet.  

-   Se estiver gerenciando clientes na internet e tiver configurado a vários pontos de atualização de software para aceitar comunicações de clientes na internet, o processo de mudança segue o processo de repetição padrão descrito anteriormente.  

-   Se o processo de análise é iniciado, mas o cliente está desativado antes da análise estiver concluída, ele não é considerado uma falha da análise e ele não conta como uma das quatro tentativas de repetição.  

Quando o Configuration Manager recebe qualquer um dos seguintes códigos de erro do Windows Update Agent, o cliente tenta repetir a ligação:  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

Para procurar o significado de um código de erro, converter o código de erro decimal para hexadecimal e procure o valor hexadecimal de um site, tais como o [Windows Update Agent - Wiki de códigos de erro](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx). Por exemplo, o código de erro decimal 2149842970 é 8024001A hexadecimal, o que significa que não foi definido WU_E_POLICY_NOT_SET um valor de política.  


###  <a name="BKMK_ManuallySwitchSUPs"></a> Mudar manualmente clientes para um novo ponto de atualização de software

Do ponto de clientes do Gestor de configuração do comutador para uma nova atualização de software quando existirem problemas com o ponto de atualização de software ativo. Esta alteração só acontece quando um cliente recebe vários pontos de atualização de software a partir de um ponto de gestão.

> [!IMPORTANT]    
> Quando alterna dispositivos para utilizar um novo servidor, os dispositivos utilizam contingência para encontrar esse servidor novo. Antes de começar esta alteração, reveja as configurações do grupo de limites para se certificar de que seus pontos de atualização de software estão os grupos de limites correto. Para obter mais informações, consulte [pontos de atualização de Software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points).  
>
> Mudar para um novo ponto de atualização de software gera o tráfego de rede adicional. A quantidade de tráfego depende as definições de configuração do WSUS, por exemplo, o sincronizados classificações e produtos ou utilização de uma base de dados partilhada do WSUS. Se pretender mudar de vários dispositivos, considere fazê-lo durante as janelas de manutenção. Este tempo reduz o impacto para a sua rede quando os clientes analisar com o novo ponto de atualização de software.  

#### <a name="process-to-switch-software-update-points"></a>Processo para mudar pontos de atualização de software  
Inicie esta alteração numa coleção de dispositivos. Quando acionado, os clientes procurar outro ponto de atualização de software na análise seguinte.  

1.  Na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho e selecione o **coleções de dispositivos** nó.  

2.  Selecione a coleção de destino. Na **home page** separador do Friso, no **coleção** , clique em **notificação do cliente**e, em seguida, clique em **mudar para o ponto de atualização de Software seguinte**.  


###  <a name="BKMK_SUP_CrossForest"></a> Pontos de atualização de software numa floresta não fidedigna  

Criar um ou mais softwares para atualizar pontos de um site para suportar clientes numa floresta não fidedigna. Para adicionar um ponto de atualização de software noutra floresta, instalar e configurar um servidor WSUS nessa floresta. Em seguida, inicie o Assistente para adicionar um servidor de site do Configuration Manager com a função de sistema de sites de ponto de atualização de software. No assistente, configure as seguintes definições para ligar com êxito ao WSUS na floresta não fidedigna:  

-   Especifique um **conta de instalação do sistema de Site** que pode aceder ao servidor WSUS na floresta não fidedigna.  

-   Especifique um **conta de ligação ao servidor WSUS** para ligar ao servidor WSUS.  

Por exemplo, dispõe de um site principal na floresta A com pontos de atualização de software (SUP01 e SUP02). Para o mesmo site primário, tem também dois pontos de atualização de software (SUP03 e SUP04) na floresta B. Quando mudar para o próximo ponto de atualização de software, os clientes priorizar os servidores da mesma floresta.  


###  <a name="BKMK_WSUSSyncSource"></a> Utilizar um servidor WSUS existente como origem de sincronização no site de nível superior  

Normalmente, o site de nível superior na sua hierarquia está configurado para sincronizar metadados de atualizações de software com o Microsoft Update. Quando a política de segurança organizacional não permite o site de nível superior aceder à internet, configure a origem de sincronização para o site de nível superior para utilizar um servidor WSUS existente. Este servidor WSUS não está na sua hierarquia do Configuration Manager. Por exemplo, tiver um servidor WSUS numa rede ligada à internet (DMZ), mas o site de nível superior estiver numa rede interna sem acesso à internet. Configure o servidor WSUS no DMZ como origem de sincronização para metadados de atualizações de software. Configure o servidor WSUS na rede de Perímetro para sincronizar atualizações de software com os mesmos critérios que precisa no Configuration Manager. Caso contrário, o site de nível superior poderá não sincronizar as atualizações de software que espera. Quando instala o ponto de atualização de software, configure uma conta de ligação do servidor WSUS. Esta conta tem acesso ao servidor WSUS no DMZ. Também pode confirme que a firewall permite tráfego para as portas adequadas. Para obter mais informações, consulte a [portas utilizadas pelo ponto de atualização de software para a origem de sincronização](/sccm/core/plan-design/hierarchy/ports#BKMK_PortsSUP-WSUS).  


###  <a name="BKMK_SUPSecSite"></a> Ponto de atualização de software num site secundário  

O ponto de atualização de software é opcional num site secundário. Instale o ponto de atualização de software apenas um num site secundário. Quando um ponto de atualização de software não estiver instalado no site secundário, dispositivos dentro dos limites de um site secundário utilizam um ponto de atualização de software no site primário atribuído. Geralmente instala um ponto de atualização de software num site secundário quando limitou a largura de banda entre os dispositivos no site secundário e os pontos de atualização de software no site primário principal. Também pode utilizar esta configuração quando o ponto de atualização de software no site primário se aproxima do limite de capacidade. Depois de instalar com êxito e configurar um ponto de atualização de software no site secundário, uma política ao nível do site é atualizada para clientes e, se começa a usar o novo ponto de atualização de software.  


### <a name="bkmk_internet-clients"></a> Plano para clientes baseados na internet

Quando tiver de gerir dispositivos que se movem fora da sua rede para a internet, desenvolva um plano para saber como gerir atualizações de software nestes dispositivos. O Configuration Manager suporta várias tecnologias para este cenário. Utilize um ou uma combinação conforme necessário para cumprir os requisitos da sua organização.

#### <a name="cloud-management-gateway"></a>Gateway de gestão na cloud
Criar um gateway de gestão na cloud no Microsoft Azure e ativar pelo menos um ponto de atualização de software no local permitir o tráfego de clientes baseados na internet. Como os clientes se movem para a internet, eles continuar a verificar em relação a seus pontos de atualização de software. Todos os clientes baseados na internet obtêm sempre o conteúdo do serviço de nuvem do Microsoft Update utilização. 

Para obter mais informações, consulte [planear para o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

#### <a name="internet-based-client-management"></a>Gestão de clientes baseada na Internet
Colocar um ponto de atualização de software numa rede de acesso à internet e ativá-la permitir o tráfego de clientes baseados na internet. Como os clientes se movem para a internet, eles mudarem para este ponto de atualização de software para verificação. Todos os clientes baseados na internet obtêm sempre o conteúdo do serviço de nuvem do Microsoft Update utilização.

Para obter mais informações sobre as vantagens e desvantagens da gestão de clientes baseados na internet, consulte [gerir clientes na internet](/sccm/core/clients/manage/manage-clients-internet).

#### <a name="windows-update-for-business"></a>Windows Update para empresas
Windows Update para empresas permite-lhe manter os dispositivos Windows 10 sempre atualizados com as atualizações de funcionalidade e qualidade mais recente. Estes dispositivos se ligam diretamente para o serviço de nuvem do Windows Update. O Configuration Manager pode diferenciar computadores Windows 10 que utilizam o WUfB e o WSUS para obter as atualizações de software.

Para obter mais informações, consulte [integração com o Windows Update para empresas](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10).


### <a name="bkmk_content"></a> Planear o conteúdo de atualização de software

Os clientes precisam de transferir os ficheiros de conteúdo para atualizações de software para instalá-los. O Configuration Manager fornece várias tecnologias para suportar a gestão e entrega deste conteúdo. Ou configurar as implementações de atualização de software para permitir ou precisar que os clientes obtêm conteúdo diretamente a partir do serviço de cloud do Microsoft Update.

#### <a name="download-and-distribute-content"></a>Baixar e distribuir conteúdo 
Por predefinição, o processo de gestão de atualizações de software no Configuration Manager utiliza as funcionalidades de gestão de conteúdos incorporados. Estas funcionalidades incluem a biblioteca de conteúdos do arquivo de instância única centralizado e o design distribuído da função de sistema de sites de ponto de distribuição. Utilize estas funcionalidades quando baixar e distribuir pacotes de implementação de atualização de software. 

Para obter mais informações, consulte [transferir atualizações de software](/sccm/sum/deploy-use/download-software-updates).

#### <a name="manage-express-installation-files-for-windows-10"></a>Gerir ficheiros de instalação rápida para o Windows 10
O Configuration Manager suporta a utilização de ficheiros de instalação rápida para atualizações do Windows 10. Ficheiros de atualização rápida e tecnologias de suporte, como a Otimização da entrega podem ajudar a reduzir o impacto de rede de grandes arquivos de conteúdo aos clientes a transferir. 

Para obter mais informações, consulte [entrega de atualização do Windows 10 otimizar](/sccm/sum/deploy-use/optimize-windows-10-update-delivery).

#### <a name="clients-download-content-from-the-internet"></a>Os clientes transferem conteúdo a partir da internet
Quando implementar atualizações de software em clientes, configure a implementação para os clientes transferirem o conteúdo do serviço de nuvem do Microsoft Update. Quando os clientes não conseguem transferir conteúdo a partir de outra origem de conteúdo, eles ainda podem transferir o conteúdo da internet. 

A partir da versão 1806, não precisa de criar um pacote de implementação ao implementar atualizações de software. Quando seleciona a **sem pacote de implementação** opção, os clientes podem ainda o transferem conteúdo de fontes locais se estiver disponível, mas normalmente transferir do serviço do Microsoft Update.<!--1357933-->

Clientes baseados na Internet transferem sempre os conteúdos do serviço de nuvem do Microsoft Update. Não distribua pacotes de implementação de atualização de software para um ponto de distribuição de nuvem. É-lhe cobrado para o armazenamento com o ponto de distribuição de nuvem, mas os clientes não baixar esses pacotes. 


### <a name="bkmk_thirdparty"></a> Planear atualizações de terceiros
O Configuration Manager integra-se com o WSUS, que suporta nativamente as atualizações de software publicadas pela Microsoft. A maioria dos clientes utilize outros aplicativos de terceiros que também precisam de atualizações. Existem várias opções a considerar para manter as aplicações de terceiros atualizadas.

#### <a name="supersede-applications-to-update"></a>Substituir aplicações para atualizar
Utilize uma relação de substituição com a funcionalidade de gestão de aplicações no Configuration Manager para atualizar ou substituir as aplicações existentes. Quando uma aplicação é substituída, especifique um novo tipo de implementação para substituir o tipo de implementação da aplicação substituída. Também pode decida se atualizar ou desinstalar a aplicação substituída antes da aplicação substituta está instalado.

Para obter mais informações, consulte [rever e substituir aplicações](/sccm/apps/deploy-use/revise-and-supersede-applications).

#### <a name="third-party-software-updates"></a>Atualizações de software de terceiros
A partir da versão 1806, utilize o **catálogos de atualização de Software de terceiros** nó na consola do Configuration Manager para subscrever catálogos de terceiros, publicar suas atualizações para o seu ponto de atualização de software e, em seguida, implementá-las em clientes.<!--1352101-->

Para obter mais informações, consulte [atualizações de software de terceiros](/sccm/sum/deploy-use/third-party-software-updates).

#### <a name="system-center-updates-publisher"></a>System Center Updates Publisher
System Center Updates Publisher (SCUP) é uma ferramenta autónoma que permite que fornecedores independentes de software ou desenvolvedores de aplicativos de linha de negócio gerir as atualizações personalizadas. Estas atualizações incluem os que têm dependências, como drivers e pacotes de atualizações.

Para obter mais informações, consulte [System Center Updates Publisher](/sccm/sum/tools/updates-publisher).



##  <a name="BKMK_SUPInstallation"></a> Planear a instalação do ponto de atualização de software  

Esta seção inclui os seguintes subtópicos:  
- [Requisitos do ponto de atualização de software](#BKMK_SUPSystemRequirements)
- [Planear a instalação do WSUS](#BKMK_PlanningForWSUS)
- [Configurar firewalls](#BKMK_ConfigureFirewalls)  


Esta seção fornece informações sobre os passos a efetuar para planear e preparar para a instalação de ponto de atualização de software com êxito. Antes de criar uma função de sistema de sites para o ponto de atualização de software no Configuration Manager, existem vários requisitos a serem considerados. Os requisitos específicos dependem de sua infraestrutura do Configuration Manager. Quando configurar o ponto de atualização de software para comunicar através de HTTPS, esta secção é especialmente importante consultar. Suporte HTTPS servidores exigem passos adicionais para funcionarem corretamente.  

###  <a name="BKMK_SUPSystemRequirements"></a> Requisitos do ponto de atualização de software  

Instale a função de ponto de atualização de software num sistema de sites que cumpra os requisitos mínimos para o WSUS e as configurações suportadas para sistemas de sites do Configuration Manager.  

-   Para obter mais informações sobre os requisitos mínimos para a função de servidor do WSUS no Windows Server, consulte [rever considerações e requisitos de sistema](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#BKMK_1.1).  

-   Para obter mais informações sobre as configurações suportadas para sistemas de sites do Configuration Manager, consulte [Site e pré-requisitos de sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  


###  <a name="BKMK_PlanningForWSUS"></a> Planear a instalação do WSUS  

Instale uma versão suportada do WSUS em todos os servidores de sistema de sites que configurar para a função de ponto de atualização de software. Quando não instala o ponto de atualização de software no servidor do site, instale a consola de administração do WSUS no servidor do site. Este componente permite que o servidor do site comunicar com o WSUS que é executado no ponto de atualização de software.  

Quando utilizar o WSUS no Windows Server 2012 ou posterior, configurar permissões adicionais para permitir a **Configuration Manager dos WSUS** componente no Configuration Manager para estabelecer ligação ao WSUS. Este componente efetua verificações periódicas do Estado de funcionamento. Escolha uma das seguintes opções para configurar a permissão necessária:  

-   Adicionar a conta **SYSTEM** ao grupo **Administradores WSUS**  

-   Adicionar a **NT AUTHORITY\SYSTEM** conta como um utilizador da base de dados do WSUS (SUSDB). Configure um mínimo de associação de função de base de dados do serviço Web.  
  
Para obter mais informações sobre como instalar o WSUS no Windows Server, consulte [instalar a função de servidor WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/1-install-the-wsus-server-role).  

Se instalar mais do que um ponto de atualização de software num site primário, utilize a mesma base de dados do WSUS para cada ponto de atualização de software localizado na mesma floresta do Active Directory. Partilhar o mesmo banco de dados melhora o desempenho quando os clientes mudarem para um novo ponto de atualização de software. Para obter mais informações, consulte [utilizar uma base de dados WSUS partilhada para pontos de atualização de software](/sccm/sum/plan-design/software-updates-best-practices#bkmk_shared-susdb).  


####  <a name="BKMK_CustomWebSite"></a> Configurar o WSUS para utilizar um Web site personalizado  
Quando instala o WSUS, pode optar por utilizar o Web site predefinido existente do IIS ou criar um Web site personalizado do WSUS. Crie um Web site personalizado para o WSUS para que o IIS aloje os serviços WSUS num Web site virtual dedicado. Caso contrário, ele compartilha o mesmo Web site que é utilizado por outros sistemas de sites do Configuration Manager ou aplicações. Esta configuração é especialmente necessária ao instalar a função de ponto de atualização de software no servidor do site. Quando executar o WSUS no Windows Server 2012 ou posterior, o WSUS é configurado por predefinição para utilizar a porta 8530 para HTTP e a porta 8531 para HTTPS. Especifique um site de ponto de atualização destas portas quando cria o software.  


####  <a name="BKMK_WSUSInfrastructure"></a> Utilizar uma infraestrutura do WSUS existente  
Selecione um servidor WSUS que estava ativo no seu ambiente antes de instalar o Configuration Manager como um ponto de atualização de software. Quando é configurado o ponto de atualização de software, especifique as definições de sincronização. Configuration Manager estabelece ligação ao servidor WSUS que é executado no servidor de ponto de atualização de software e configura o WSUS com as mesmas definições. 

Antes de configurar o servidor como um ponto de atualização de software, compare a respetiva configuração para produtos e classificações com as definições do Gestor de configuração. Se sincronizar o servidor WSUS existente antes de configurá-lo como um ponto de atualização de software e as listas de produtos e classificações são diferentes, sincroniza todos os metadados de atualizações de software, independentemente das definições configuradas. Este comportamento resulta em metadados de atualizações de software inesperados na base de dados do site. 

Identificar o mesmo comportamento quando adicionar produtos ou classificações diretamente na consola de administração do WSUS e, em seguida, iniciar de imediato a uma sincronização. Por predefinição, a cada hora do Configuration Manager liga ao WSUS e repõe as definições que tenham sido modificadas fora do Configuration Manager. As atualizações de software que não cumprem os produtos e classificações especificados nas definições de sincronização são definidas como expiradas. Em seguida, são removidos da base de dados do site.  

Quando um servidor WSUS é configurado como um ponto de atualização de software, já não pode utilizá-lo como um servidor WSUS autónomo. Se precisar de um servidor WSUS autónomos separados que não seja gerido pelo Configuration Manager, configure-o num servidor diferente.  

####  <a name="BKMK_WSUSAsReplica"></a> Configurar o WSUS como servidor de réplica  
Quando adiciona a função de ponto de atualização de software num servidor do site primário, não é possível utilizar um servidor WSUS que está configurado como uma réplica. Quando o servidor WSUS é configurado como uma réplica, Gestor de configuração não consegue configurar o servidor WSUS e a sincronização do WSUS falha. O primeiro ponto de atualização de software que instalar num site primário será o ponto de atualização de software predefinido. Os pontos de atualização de software adicionais no site serão configurados como réplicas do ponto de atualização de software predefinido.  

####  <a name="BKMK_WSUSandSSL"></a> Decidir se pretende configurar o WSUS para utilizar SSL  
Utilize o protocolo SSL para ajudar a proteger o ponto de atualização de software. O WSUS utiliza SSL para autenticar computadores cliente e servidores WSUS a jusante para o servidor WSUS. O WSUS também utiliza SSL para encriptar os metadados de atualização de software. Quando optar por proteger o WSUS com SSL, prepare o servidor WSUS antes de instalar o ponto de atualização de software. Para obter mais informações, consulte a [configurar o SSL no servidor WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#bkmk_2.5.ConfigSSL) artigo na documentação para o WSUS. 

Quando instalar e configurar o ponto de atualização de software, selecione a opção para **ativar as comunicações SSL para o servidor WSUS**. Caso contrário, o Configuration Manager configura o WSUS para não utilizar SSL. Quando ativar o SSL num ponto de atualização de software, também configure quaisquer pontos de atualização de software em sites subordinados para utilizar SSL.  


###  <a name="BKMK_ConfigureFirewalls"></a> Configurar firewalls  

O ponto de atualização de software num site de administração central do Configuration Manager se comunica com o WSUS no ponto de atualização de software. WSUS se comunica com a origem de sincronização para sincronizar os metadados de atualizações de software. Pontos de atualização de software num site subordinado comunicam com o ponto de atualização de software no site principal. Quando existe mais do que um ponto de atualização de software num site primário, os pontos de atualização de software adicional se comunicar com o ponto de atualização de software predefinido. A função predefinida é o primeiro ponto de atualização de software que está instalado no site.  

Poderá ter de configurar a firewall para permitir o tráfego HTTP ou HTTPS que utiliza o WSUS nos seguintes cenários: 
- Entre o ponto de atualização de software e a internet
- Entre um ponto de atualização de software e a respetiva origem de sincronização a montante
- Entre os pontos de atualização de software adicionais  

A ligação ao Microsoft Update é sempre configurada para utilizar a porta 80 para HTTP e a porta 443 para HTTPS. Utilize uma porta personalizada para a ligação do WSUS no ponto de atualização de software num site subordinado ao WSUS no ponto de atualização de software no site principal. Quando a política de segurança não permite a ligação, utilize a exportar e importar o método de sincronização. Para obter mais informações, consulte a [origem de sincronização](#BKMK_SyncSource) secção deste artigo. Para obter mais informações sobre as portas que o WSUS utiliza, consulte [como determinar as definições de porta utilizadas pelo WSUS no Configuration Manager](../get-started/install-a-software-update-point.md#wsus-settings).  


#### <a name="restrict-access-to-specific-domains"></a>Restringir o acesso a domínios específicos  
Se sua organização não permitir as portas e protocolos estejam abertos a todos os endereços na firewall entre o ponto de atualização de software ativo e a internet, restringir o acesso aos seguintes domínios, de modo a que o WSUS e as atualizações automáticas possam comunicar com Microsoft Update:  

-   `http://windowsupdate.microsoft.com`  

-   `http://*.windowsupdate.microsoft.com`  

-   `https://*.windowsupdate.microsoft.com`  

-   `http://*.update.microsoft.com`  

-   `https://*.update.microsoft.com`  

-   `http://*.windowsupdate.com`  

-   `http://download.windowsupdate.com`  

-   `http://download.microsoft.com`  

-   `http://*.download.windowsupdate.com`  

-   `http://test.stats.update.microsoft.com`  

-   `http://ntservicepack.microsoft.com`  

Poderá ter de adicionar os endereços abaixo à firewall que está localizada entre os dois sistemas nos seguintes casos de sites: 
- Se os sites subordinados têm um ponto de atualização de software 
- Se existir um ponto de atualização dos software remoto ativo baseado na internet num site

  **Ponto de atualização de software no site subordinado**  

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  



##  <a name="BKMK_SyncSettings"></a> Planear as definições de sincronização  

Esta seção inclui os seguintes subtópicos:  
- [Origem de sincronização](#BKMK_SyncSource)
- [Agenda de sincronização](#BKMK_SyncSchedule)
- [Classificações de atualizações](#BKMK_UpdateClassifications)
- [Produtos](#BKMK_UpdateProducts)
- [Regras de substituição](#BKMK_SupersedenceRules)
- [Idiomas](#BKMK_UpdateLanguages)  


Sincronização de atualizações de software no Configuration Manager transfere os metadados de atualizações de software com base nos critérios que configurou. Site de nível superior na sua hierarquia sincroniza atualizações de software do Microsoft Update. Tem a opção para configurar o ponto de atualização de software no site de nível superior para sincronizar com um servidor WSUS existente, não na hierarquia do Configuration Manager. Os sites subordinados principais sincronizam os metadados de atualizações de software a partir do ponto de atualização de software no site de administração central. Antes de instalar e configurar um ponto de atualização de software, utilize esta secção para planear as definições de sincronização.  


###  <a name="BKMK_SyncSource"></a> Origem de sincronização  

As definições da origem de sincronização para o ponto de atualização de software, especifique a localização para onde o ponto de atualização de software obtém metadados de atualizações de software. Também especifica se o processo de sincronização cria eventos de relatório WSUS.  

-   **Origem de sincronização**: Por predefinição, o ponto de atualização de software no site de nível superior configura a origem de sincronização para o Microsoft Update. Tem a opção de sincronizar o site de nível superior com um servidor WSUS existente. O ponto de atualização de software num site primário subordinado configura a origem de sincronização como o software de ponto de atualização no site de administração central.  

    -  O primeiro ponto de atualização de software que instalar num site primário, que é o ponto de atualização de software predefinido, sincroniza com o site de administração central. Os pontos de atualização de software adicionais no site primário sincronizam-se com o ponto de atualização de software predefinido no site primário.  

    - Quando um ponto de atualização de software estiver desligado do Microsoft Update ou do servidor de atualização a montante, configure a origem de sincronização não se sincronizar com uma origem de sincronização configurada. Em vez disso, configure-o para utilizar a exportação e importação da função do **WSUSUtil** ferramenta para sincronizar atualizações de software. Para obter mais informações, veja [Sincronizar atualizações de software a partir de um ponto de atualização de software desligado](../get-started/synchronize-software-updates-disconnected.md).  

-   **Eventos de relatório WSUS:** O Windows Update Agent nos computadores cliente pode criar mensagens de eventos para os relatórios WSUS. Estes eventos não são utilizados pelo Configuration Manager. Portanto, a opção **não criar eventos de relatório WSUS**, está selecionada por predefinição. Quando esses eventos não são criados, o único momento em que o cliente deve se conectar ao servidor WSUS é durante a avaliação de atualização de software e conformidade verificações. Se estes eventos forem necessários para relatórios fora do Configuration Manager, modificar esta definição para criar eventos de relatório WSUS.  


###  <a name="BKMK_SyncSchedule"></a> Agenda de sincronização  

Configure a agenda de sincronização apenas no ponto de atualização de software no site de nível superior na hierarquia do Configuration Manager. Quando configura a agenda de sincronização, o ponto de atualização de software sincroniza-se com a origem de sincronização à data e à hora que especificar. A agenda personalizada permite-lhe sincronizar atualizações de software para otimizar o seu ambiente. Considere as necessidades de desempenho do servidor WSUS, servidor de sites e rede. Por exemplo, 2:00 uma vez por semana. Em alternativa, iniciar manualmente a sincronização no site de nível superior utilizando a **sincronização de atualizações de Software** ação a partir do **todas as atualizações de Software** ou **grupos de atualização de Software**  nós na consola do Configuration Manager.  

> [!TIP]  
>  Agende a sincronização de atualizações de software para ser executada através de uma hora que é adequada para o seu ambiente. Um cenário comum é definir a agenda de sincronização para ser executada logo após o lançamento de atualização regular de software da Microsoft na segunda Terça-feira de cada mês. Este dia é normalmente denominado *Patch Terça-feira*. Se utilizar o Configuration Manager para fornecer a definição do Endpoint Protection e o Windows Defender e atualizações de mecanismos, considere a definir a agenda de sincronização para ser executada diariamente.  

Depois do ponto de atualização de software sincroniza com êxito, envia um pedido de sincronização para sites subordinados. Se tiver um site primário pontos de atualização de software adicional, envia um pedido de sincronização para cada ponto de atualização de software. Este processo é repetido em todos os sites na hierarquia.  


###  <a name="BKMK_UpdateClassifications"></a> Classificações de atualizações  

Cada atualização de software é definida com uma classificação de atualização que ajuda a organizar os diferentes tipos de atualizações. Durante o processo de sincronização, o site sincroniza os metadados para as classificações especificadas. 

O Configuration Manager suporta a sincronização das seguintes classificações de atualização:  

-   **Atualizações críticas**: Uma atualização amplamente lançada para um problema específico que corrige um erro crítico não relacionado com segurança.  

-   **Atualizações de definições**: Uma atualização para vírus ou outros ficheiros de definição.  

-   **Pacotes de funcionalidades**: Novas funcionalidades do produto que são distribuídas fora de uma versão de produto e que normalmente estão incluídas na próxima versão completa do produto.  

-   **Atualizações de segurança**: Uma atualização amplamente lançada para um problema específico do produto, relacionadas com segurança.  

-   **Service Packs**: Um conjunto cumulativo de correções que são aplicadas a um aplicativo ou sistema operacional. Estas correções incluem atualizações de segurança, atualizações críticas e atualizações de software.  

-   **Ferramentas**: Um utilitário ou funcionalidade que ajuda a efetuar uma ou mais tarefas.  

-   **Rollups de atualizações**: Um conjunto cumulativo de correções que estão agrupadas para facilitar a implementação. Estas correções incluem atualizações de segurança, atualizações críticas e atualizações de software. Um rollup de atualizações resolve geralmente uma área específica, tal como segurança ou um componente de produto.  

-   **Atualizações**: Uma atualização para uma aplicação ou ficheiro que está atualmente instalado.  

-   **Atualizações**: Uma atualização de funcionalidades para uma nova versão do Windows 10.  

Configure as definições de classificação de atualização apenas no site de nível superior. As definições de classificação de atualização não estão configuradas no ponto de atualização de software em sites subordinados porque os metadados de atualizações de software são replicados desde o site de nível superior. Quando selecionar as classificações de atualização, tenha em atenção quanto mais classificações selecionar, mais tempo demorará a sincronizar os metadados de atualizações de software.  

> [!WARNING]  
>  Como procedimento recomendado, desmarque todas as classificações antes de sincronizar pela primeira vez. Após a sincronização inicial, selecione as classificações pretendidas e, em seguida, volte a executar a sincronização.  


###  <a name="BKMK_UpdateProducts"></a> Produtos  

Os metadados para cada atualização de software definem um ou mais produtos aos quais se aplica a atualização. Um produto é uma edição específica de um aplicativo ou sistema operacional. Um exemplo de um produto é o Microsoft Windows 10. Uma família de produtos é a base SO ou a aplicação da qual derivam os produtos individuais. Um exemplo de uma família de produtos é o Microsoft Windows, dos quais o Windows 10 e Windows Server 2016 são membros. Selecione uma família de produtos ou produtos individuais dentro de uma família de produtos.  

Quando as atualizações de software se aplicam a vários produtos e, pelo menos um dos produtos é selecionado para sincronização, todos os produtos aparecerão na consola do Configuration Manager, mesmo se alguns produtos não foram selecionados. Por exemplo, apenas selecionar o produto do Windows Server 2012. Se uma atualização de software se aplicar ao Windows Server 2012 e Windows Server 2012 Datacenter Edition, ambos os produtos são a base de dados do site.  

Configure as definições de produto apenas no site de nível superior. As definições do produto não estão configuradas no ponto de atualização de software para sites subordinados porque os metadados de atualizações de software são replicados desde o site de nível superior. Quantos mais produtos selecionar, mais tempo demorará a sincronizar os metadados de atualizações de software.  

> [!IMPORTANT]  
>  Gestor de configuração armazena uma lista de produtos e famílias de produtos que escolher quando instalar pela primeira vez o ponto de atualização de software. Produtos e famílias de produtos que são lançadas após o lançamento do Configuration Manager podem não estar disponíveis para seleção até concluir a sincronização. O processo de sincronização atualiza a lista de produtos disponíveis e famílias de produtos a partir da qual pode escolher. Desmarque todos os produtos antes de sincronizar as atualizações de software pela primeira vez. Após a sincronização inicial, selecione os produtos desejados e, em seguida, volte a executar a sincronização.  


###  <a name="BKMK_SupersedenceRules"></a> Regras de substituição  

Normalmente, uma atualização de software que substitui outra atualização de software executa uma ou mais das seguintes ações:  

-   Melhora ou atualiza a correção que foi fornecida por uma ou mais atualizações publicadas anteriormente.  

-   Melhora a eficiência do pacote de arquivo atualização substituída, que é instalado nos clientes se a atualização é aprovada para instalação. Por exemplo, a atualização substituída poderá conter ficheiros que já não são relevantes para a correção ou para os sistemas operativos que são suportados pela nova atualização. Esses ficheiros não estão incluídos no pacote de ficheiros de substituição da atualização.  

-   Atualiza as versões mais recentes de um produto. Por outras palavras, atualiza versões que já não são aplicáveis a versões ou configurações antigas de um produto. As atualizações também podem substituir outras atualizações se tiverem sido efetuadas modificações para expandir o suporte de idiomas. Por exemplo, uma versão mais recente de uma atualização de produto do Microsoft Office poderá remover o suporte para um SO mais antigo, mas poderá acrescentar suporte adicional para novos idiomas na versão de atualização inicial.  

Nas propriedades para o software de ponto de atualização, especificar que as atualizações de software substituídas expiram de imediato. Esta definição evita que sejam sejam incluídas nas novas implementações. Ele também sinaliza as implementações existentes para indicar que contêm uma ou mais atualizações de software expiradas. Em alternativa, especificar um período de tempo antes das atualizações de software substituídas expiram. Esta ação permite-lhe continuar a implementá-las. 

Considere os seguintes cenários em que poderá ser necessário implementar uma atualização de software substituída:  

-   Uma atualização de software substituída suporta apenas as versões mais recentes de um sistema operacional. Alguns dos seus computadores clientes executam versões anteriores do sistema operacional.  

-   Uma atualização de software substituta tem aplicabilidade mais restrita que a atualização de software que substitui. Este comportamento tornaria inadequada para alguns clientes.  

-   Se atualizar um software de substituição não foi aprovada para implementação no seu ambiente de produção.  

    > [!NOTE]  
    > - Antes do Configuration Manager versão 1806, quando o Configuration Manager define uma atualização de software substituídas, tal como **expirado**, ele não define a atualização **recusada** no WSUS. Os clientes continuam a verificar a existência de uma atualização expirada até que a atualização será recusada manualmente ou através de um script personalizado.  Depois de 1806 de versão do Configuration Manager, Configuration Manager também será recusar as atualizações substituídas no WSUS. Para obter mais informações sobre a tarefa de limpeza do WSUS, consulte [manutenção de atualizações de Software](/sccm/sum/deploy-use/software-updates-maintenance).
    > - Partir 1810 de versão do Gestor de configuração, pode especificar o comportamento de regras de substituições de **funcionalidade de actualizações** separadamente do **não funcionalidade actualizações**.

###  <a name="BKMK_UpdateLanguages"></a> Idiomas  

As definições de idioma para o ponto de atualização de software permitem-lhe configurar: 
- Os idiomas para os quais os detalhes de resumo (metadados de atualizações de software) estão sincronizados para atualizações de software  
- Idiomas de ficheiro que são transferidos para atualizações de software de atualizações de software  

#### <a name="software-update-file"></a>Ficheiro de atualização de software  
Configurar idiomas para o **o ficheiro de atualização de Software** definição nas propriedades para o ponto de atualização de software. Esta definição proporciona os idiomas predefinidos que estão disponíveis quando são transferidas atualizações num site. Modificar os idiomas que estão selecionados, por predefinição, cada vez que as atualizações de software são transferidas ou implementadas. Durante o processo de transferência, os ficheiros de atualização de software dos idiomas configurados são transferidos para a localização da origem do pacote de implementação se os ficheiros de atualização de software estiverem disponíveis no idioma selecionado. Em seguida, são copiados para a biblioteca de conteúdos no servidor do site. Em seguida, estão distribuídos aos pontos de distribuição que estão configurados para o pacote.  

Configure as definições de idioma do ficheiro de atualização de software com os idiomas que são mais frequentemente utilizados no seu ambiente. Por exemplo, os clientes no seu site utilizam principalmente inglês e japonês para Windows ou aplicações. Existem outros idiomas que são utilizados no site. Selecione apenas para inglês e japonês na **o ficheiro de atualização de Software** coluna ao transferir ou ao implementar a atualização de software. Esta ação permite-lhe utilizar as predefinições no **seleção de idioma** página dos assistentes de implementação e transferência. Esta ação também impede que o ficheiros de atualização desnecessários a ser transferido. Configure esta definição em cada ponto de atualização de software na hierarquia do Configuration Manager.  

#### <a name="summary-details"></a>Detalhes de resumo  
Durante o processo de sincronização, as informações dos detalhes de resumo (metadados de atualizações de software) são atualizadas para as atualizações de software nos idiomas especificados. Os metadados fornecem informações sobre a atualização de software, por exemplo:
- Nome
- Descrição
- Produtos que suporta a atualização
- Classificação da atualização
- ID do artigo
- URL de transferência
- Regras de aplicabilidade

Configure as definições de detalhes do resumo apenas no site de nível superior. Os detalhes de resumo não estão configurados no ponto de atualização de software em sites subordinados porque os metadados de atualizações de software são replicados do site de administração central utilizando a replicação baseada em ficheiros. Ao selecionar os idiomas de detalhes de resumo, selecione apenas os idiomas de que necessita no seu ambiente. Quanto mais idiomas forem selecionados, mais tempo demorará a sincronização dos metadados de atualizações de software. O Configuration Manager apresenta os metadados de atualizações de software na região do sistema operacional no qual a consola do Configuration Manager é executado. Se as propriedades localizadas das atualizações de software não estão disponíveis na região deste sistema operacional, de atualizações de software apresenta informações em inglês.  

> [!IMPORTANT]  
>  Selecione todos os idiomas de detalhes de resumo que precisa. Quando o ponto de atualização de software no site de nível superior sincroniza com a origem de sincronização, os idiomas de detalhes de resumo selecionados determinam os metadados de atualizações de software que obtém. Se modificar os idiomas de detalhes de resumo após a sincronização executou, pelo menos, uma vez, obtém os metadados de atualizações de software para os idiomas de detalhes de resumo modificados apenas para atualizações de software novas ou atualizadas. As atualizações de software que já foram sincronizadas não forem atualizadas com novos metadados para os idiomas modificados, a menos que exista uma alteração para a atualização de software na origem de sincronização.  



##  <a name="BKMK_MaintenanceWindow"></a> Planear uma janela de manutenção de atualizações de software  

Adicione uma janela de manutenção dedicada para a instalação de atualizações de software. Esta ação permite-lhe configurar uma janela de manutenção geral e uma janela de manutenção diferente para atualizações de software. Quando configurar uma janela de manutenção geral e a janela de manutenção de atualizações de software, os clientes instalam atualizações de software apenas durante a janela de manutenção de atualizações de software. 

A partir do Configuration Manager versão 1810, pode alterar este comportamento e permitir que as atualizações de software instalar durante uma janela de manutenção geral. Para obter mais informações sobre esta definição de cliente, consulte [definições de cliente de atualizações de Software](/sccm/core/clients/deploy/about-client-settings#bkmk_SUMMaint).

Para obter mais informações sobre janelas de manutenção, consulte [como utilizar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  


##  <a name="BKMK_RestartOptions"></a> Opções de reinício para clientes do Windows 10 após a instalação de atualizações de software

Quando uma atualização de software que requeira um reinício é implementada e instalada com o Configuration Manager, o cliente as agendas de um reinício pendente e exibe uma caixa de diálogo de reinício.

Quando existe um reinício pendente para uma atualização de software do Configuration Manager, a opção para **atualizar e reiniciar** e **atualizar e encerrar** está disponível em computadores Windows 10 nas opções de energia do Windows. Depois de utilizar uma destas opções, a caixa de diálogo de reinício não exibe depois do computador for reiniciado.



## <a name="next-steps"></a>Passos seguintes
Depois de planear atualizações de software, consulte [gestão de atualizações de preparação para a software](../get-started/prepare-for-software-updates-management.md).  

Para obter mais informações sobre a gestão do Windows como um serviço, consulte [Noções básicas do Configuration Manager como um serviço e o Windows como um serviço](/sccm/core/understand/configuration-manager-and-windows-as-service).

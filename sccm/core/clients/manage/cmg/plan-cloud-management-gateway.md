---
title: Plano para gateway de gestão de nuvem
titleSuffix: Configuration Manager
description: Planear e estruturar o gateway de gestão de nuvem (CMG) para simplificar a gestão de clientes baseados na internet.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e5274398b1a53b5a8dce8b854bccbe0e0d92081
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Planear para o gateway de gestão de nuvem no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*
 
<!--1101764-->
O gateway de gestão de nuvem (CMG) fornece uma forma simples de gerir clientes do Configuration Manager na internet. Ao implementar o CMG como um serviço em nuvem no Microsoft Azure, pode gerir clientes tradicionais que se movem na internet sem uma infraestrutura adicional. Também não precisa de expor a sua infraestrutura no local para a internet. 

> [!Tip]  
> Esta funcionalidade foi introduzida pela primeira vez na versão 1610 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1802, esta funcionalidade já não é uma funcionalidade de pré-lançamento.  


> [!Note]  
> O Configuration Manager não ativar esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Depois de estabelecer os pré-requisitos, criação de CMG é composta pelos seguintes três passos na consola do Configuration Manager:
1. Implemente o serviço de nuvem CMG no Azure.
2. Adicione a função de ponto de ligação de CMG. 
3. Configure o site e as funções de site para o serviço. Assim que implementado e configurado, os clientes aceder perfeitamente no local funções de site independentemente estiverem na intranet ou à internet.

Este artigo fornece o conhecimento para saber mais sobre o CMG, estrutura como se enquadra no seu ambiente, e planear a implementação. 



## <a name="scenarios"></a>Cenários 

Existem vários cenários para o qual um CMG é vantajoso. Os cenários seguintes são algumas das mais comuns:  

- Gerir clientes Windows tradicionais com a identidade de associados a um domínio do Active Directory. Estes clientes incluem o Windows 7, Windows 8.1 e Windows 10. Utiliza certificados PKI para proteger o canal de comunicação. Atividades de gestão incluem:  
    - As atualizações de software e do endpoint protection
    - Estado de cliente e de inventário
    - Definições de compatibilidade
    - Distribuição de software no dispositivo
    - Sequência de tarefas de atualização no local do Windows 10 (a partir da versão 1802)

- Gerir clientes do Windows 10 tradicionais com a identidade moderna, híbrido ou na nuvem pura associados a um domínio com o Azure Active Directory (Azure AD). Os clientes utilizam o Azure AD para autenticar em vez de certificados PKI. Utilizar o Azure AD é mais simples de configurar, configurar e manter a sistemas PKI mais complexos. Atividades de gestão são os mesmos que o primeiro cenário, bem como:  
    - Distribuição de software para o utilizador  

- Instale o cliente de Configuration Manager em dispositivos Windows 10 através da internet. Utilizar o Azure AD permite ao dispositivo para se autenticar CMG para o registo de cliente e a atribuição. Pode instalar o cliente manualmente, ou utilizando outro método de distribuição de software, como o Microsoft Intune.  

- Novo dispositivo de aprovisionamento com a gestão de conjunta. Não é necessária para a gestão conjunta CMG. Ajuda a concluir um cenário de ponto a ponto para novos dispositivos que envolvem AutoPilot do Windows, do Azure AD, Microsoft Intune e Configuration Manager.  

### <a name="specific-use-cases"></a>Casos de utilização específicos
Entre estes cenários podem ser aplicadas os seguintes casos de utilização do dispositivo específico:

- Dispositivos de roaming, tais como computadores portáteis  

- Remoto/ramo office dispositivos são menos dispendioso e mais eficiente para gerir através de internet que através de uma WAN ou através de uma VPN.  

- Fusões e aquisições, onde poderá ser mais fácil associar dispositivos ao Azure AD e gerir através de um CMG.  

> [!Important]
> Por predefinição, todos os clientes recebem a política para um CMG e começar a utilizar o mesmo que ficarem baseado na internet. Consoante o caso de cenário e a utilização que aplica-se a sua organização, poderá ter de utilização do âmbito do CMG. Para obter mais informações, consulte o [permitir que os clientes utilizar um gateway de gestão de nuvem](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway) definição de cliente.


## <a name="topology-design"></a>Estrutura de topologia

### <a name="cmg-components"></a>Componentes CMG
Implementação e a operação do CMG inclui os seguintes componentes:  

- O **o serviço em nuvem CMG** no Azure efetua a autenticação e reencaminha os pedidos de cliente do Configuration Manager para o ponto de ligação CMG.  
 
- O **ponto de ligação de CMG** uma ligação consistente e de elevado desempenho da rede no local para o serviço CMG do Azure ativa a função do sistema de sites. Também publica definições CMG, incluindo as definições de segurança e informações de ligação. O ponto de ligação CMG reencaminha os pedidos de cliente do CMG para funções no local, de acordo com os mapeamentos de URL.

- O [ **ponto de ligação de serviço** ](/sccm/core/servers/deploy/configure/about-the-service-connection-point) função do sistema de site executa o componente Gestor do serviço em nuvem, que processa todas as tarefas de implementação de CMG. Além disso, monitoriza e comunica informações de estado de funcionamento e o registo de serviço do Azure AD. Certifique-se de que o ponto de ligação de serviço está no [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).  

- O **ponto de gestão** pedidos de cliente por normal de serviços de função de sistema do site.  

- O **ponto de atualização de software** pedidos de cliente por normal de serviços de função de sistema do site.  

- **Os clientes baseados na Internet** ligar ao CMG aceder a componentes no local do Configuration Manager.

- O CMG utiliza um **baseada em certificado HTTPS** serviço para o ajudar a proteger a comunicação de rede com clientes web.  

- Utilização de clientes baseados na Internet **PKI certificados ou do Azure AD** para autenticação e identidade.  

- A [ **ponto de distribuição de nuvem** ](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) fornece o conteúdo para os clientes baseados na internet, conforme necessário.  


### <a name="azure-resource-manager"></a>O Azure Resource Manager
<!-- 1324735 -->
A partir de versão 1802, pode criar o CMG utilizando um **implementação Azure Resource Manager**. [O Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para gerir todos os recursos de solução como uma única entidade, chamada um [grupo de recursos](/azure/azure-resource-manager/resource-group-overview#resource-groups). Quando implementar CMG com o Azure Resource Manager, o site utiliza o Azure Active Directory (Azure AD) para autenticar e criar os recursos de nuvem necessário. Esta implementação modernized não necessita que o certificado de gestão do Azure clássico.  

O assistente CMG ainda fornece a opção para um **implementação de serviço clássico** a utilizar um certificado de gestão do Azure. Para simplificar a implementação e gestão de recursos, é recomendável utilizar o modelo de implementação Azure Resource Manager para todas as instâncias CMG novo. Se for possível, volte a implementar instâncias CMG através do Gestor de recursos existentes. Para obter mais informações, consulte [modificar um CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).

> [!IMPORTANT]  
> Esta capacidade não ative o suporte para fornecedores de serviços de nuvem do Azure (CSP). A implementação de CMG com o Azure Resource Manager continua a utilizar o serviço de nuvem clássico, que não suporta o CSP. Para obter mais informações, consulte [serviços do Azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services). 


### <a name="hierarchy-design"></a>Estrutura de hierarquia

Crie o CMG no site de nível superior da sua hierarquia. Se isto é um site de administração central, em seguida, crie pontos de ligação de CMG em sites primários subordinados. O componente de Gestor do serviço de nuvem está no ponto de ligação de serviço, que também seja no site de administração central. Esta estrutura pode partilhar o serviço em diferentes sites primários se for necessário.

Pode criar vários serviços CMG no Azure e pode criar vários pontos de ligação de CMG. Vários pontos de ligação de CMG fornecem balanceamento de carga do tráfego de cliente do CMG para as funções no local. Para reduzir a latência de rede, atribua o CMG associado à mesma região geográfica do site primário.

 > [!Note]  
 > Os clientes baseados na Internet e o CMG não enquadram-se em qualquer grupo de limites.

Outros fatores, tais como o número de clientes para gerir, também afetam a estrutura CMG. Para obter mais informações, consulte [desempenho e dimensionamento](#performance-and-scale).

#### <a name="example-1-standalone-primary-site"></a>Exemplo 1: um site primário autónomo

Contoso tem um site primário autónomo num datacenter no local na sede em Nova Iorque cidade. 
- É possível criar um CMG na região do Azure do Leste-nos para reduzir a latência de rede. 
- Se criarem dois pontos de ligação de CMG, ambos ligado ao serviço CMG único.  

Como os clientes se movem para a internet, comunicam com o CMG na região do Azure do Leste dos EUA. O CMG reencaminha esta comunicação através de ambos os pontos de ligação CMG.

#### <a name="example-2-hierarchy-with-site-specific-cmg"></a>Exemplo 2: hierarquia com CMG específicas

Quarta café tem um site de administração central num datacenter no local na sede em Seattle. Um site primário está no mesmo centro de dados e o outro site primário é no seu escritório principal alfabetos no Paris. 
- No site de administração central, se criarem dois serviços CMG:
     - Um CMG na região do Azure do Oeste-nos.
     - Um CMG na região do Azure de Europa Ocidental.
- No site primário com base em Seattle, é criar um ponto de ligação de CMG ligado para o Oeste nos CMG.
- No site primário com base em Paris, é criar um ponto de ligação de CMG ligado CMG de Europa Ocidental.

Como os clientes baseados em Seattle se movem para a internet, comunicam com o CMG na região do Azure do Oeste-nos. O CMG reencaminha ao ponto de ligação com base em Seattle CMG desta comunicação.

Da mesma forma, como os clientes baseados em Paris se movem para a internet, comunicam com o CMG na região do Azure de Europa Ocidental. O CMG reencaminha ao ponto de ligação com base em Paris CMG desta comunicação. Quando os utilizadores com base em Paris viajam para sede da empresa em Seattle, os respetivos computadores continuam a comunicar com o CMG na região do Azure de Europa Ocidental. 

 > [!Note]  
 > Quarta café considerado criar outro ponto de ligação de CMG no site primário com base em Paris ligado para o Oeste nos CMG. Os clientes baseados em Paris, em seguida, seriam utilizar ambos os CMGs, independentemente da respetiva localização. Embora esta configuração ajuda-o tráfego de balanceamento de carga e fornecer redundância de serviço, também pode causar atrasos quando os clientes baseados em Paris comunicam com CMG baseado em E.U.A. Clientes do Configuration Manager não estão atualmente em consideração os respetivos região geográfica, pelo que não preferir um CMG geograficamente próximo. Os clientes utilizam aleatoriamente um CMG disponível.



## <a name="requirements"></a>Requisitos

- Um **subscrição do Azure** para alojar o CMG.  

    - Um **administrador do Azure** necessita participar na criação inicial de determinados componentes, consoante a sua estrutura. Esta pessoa não necessita de permissões no Configuration Manager.  

- Pelo menos um Windows server local para alojar o **ponto de ligação de CMG**. Pode localizar conjuntamente esta função com outras funções de sistema de sites do Configuration Manager.  

- O **ponto de ligação de serviço** tem de constar [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).   

- A [ **certificado de autenticação de servidor** ](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate) para o CMG.  

- Se utilizar o método de implementação clássico do Azure, tem de utilizar um [ **certificado de gestão do Azure**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#azure-management-certificate).  

    > [!TIP]  
    > A partir do Configuration Manager versão 1802, utilizando o **do Azure Resource Manager** modelo de implementação é recomendado. Não requer este certificado de gestão.  

- **Outros certificados** poderá ser necessário, consoante o seu modelo de autenticação e a versão de SO de cliente. Para obter mais informações, consulte [certificados CMG](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).  

    - A partir de versão 1802, tem de configurar todos os ativada CMG [ **pontos de gestão para utilizar HTTPS**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https).  

- Integração com **do Azure AD** poderão ser necessárias para clientes Windows 10. Para obter mais informações, consulte [serviços do Azure configurar](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- Os clientes têm de utilizar **IPv4**.  



## <a name="specifications"></a>Especificações

- Todas as versões do Windows listadas no [sistemas operativos suportados para os clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) são suportadas para CMG.  

- CMG suporta apenas os software e de ponto de atualização ponto funções de gestão.  

- CMG não suporta clientes só comunicam com endereços IPv6.<!--495606-->  

- Pontos de atualização de software utilizando um balanceador de carga de rede não funcionam com CMG. <!--505311-->  

- A partir de versão 1802, implementações de CMG utilizando o modelo de recursos do Azure não ative o suporte para fornecedores de serviços de nuvem do Azure (CSP). A implementação de CMG com o Azure Resource Manager continua a utilizar o serviço de nuvem clássico, que não suporta o CSP. Para obter mais informações, consulte [serviços do Azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services)  


### <a name="support-for-configuration-manager-features"></a>Suporte para funcionalidades do Configuration Manager
A tabela seguinte lista o suporte CMG para funcionalidades do Configuration Manager:


|Funcionalidade  |Suporte  |
|---------|---------|
| Atualizações de software     | ![Suportado](media/green_check.png) |
| Proteção de ponto final     | ![Suportado](media/green_check.png) |
| Inventário de hardware e software     | ![Suportado](media/green_check.png) |
| Estado do cliente e notificações     | ![Suportado](media/green_check.png) |
| Executar scripts     | ![Suportado](media/green_check.png) |
| Definições de compatibilidade     | ![Suportado](media/green_check.png) |
| Instalação de cliente</br>(com a integração do AD do Azure)     | ![Suportado](media/green_check.png)  (1706) |
| Distribuição de software (direcionados dispositivo)     | ![Suportado](media/green_check.png) |
| Distribuição de software (direcionados ao utilizador, necessária)</br>(com a integração do AD do Azure)     | ![Suportado](media/green_check.png)  (1710) |
| Distribuição de software (direcionados ao utilizador, disponível)</br>([todos os requisitos](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)) | ![Suportado](media/green_check.png)  (1802) |
| Sequência de tarefas de atualização no local do Windows 10     | ![Suportado](media/green_check.png)  (1802) |
| Qualquer outro cenário de sequência de tarefas     | ![Não suportado](media/Red_X.png) |
| Instalação push do cliente     | ![Não suportado](media/Red_X.png) |
| Atribuição automática de site     | ![Não suportado](media/Red_X.png) |
| Catálogo de aplicações     | ![Não suportado](media/Red_X.png) |
| Pedidos de aprovação de software     | ![Não suportado](media/Red_X.png) |
| Consola do Configuration Manager     | ![Não suportado](media/Red_X.png) |
| Ferramentas remotas     | ![Não suportado](media/Red_X.png) |
| Relatórios Web site     | ![Não suportado](media/Red_X.png) |
| Reativação por LAN     | ![Não suportado](media/Red_X.png) |
| Clientes Mac, Linux e UNIX     | ![Não suportado](media/Red_X.png) |
| Cache ponto a ponto     | ![Não suportado](media/Red_X.png) |
| MDM no local     | ![Não suportado](media/Red_X.png) |


|Chave|
|--|
|![Suportado](media/green_check.png) = Esta funcionalidade é suportada com CMG por todas as versões suportadas do Configuration Manager  |
|![Suportado](media/green_check.png) (*YYMM*) = esta funcionalidade é suportada com CMG a partir da versão *YYMM* do Configuration Manager  |
|![Não suportado](media/Red_X.png) = Esta funcionalidade não é suportada com CMG |



## <a name="cost"></a>Custo

>[!IMPORTANT]  
>Informação do custo que se segue para estimar apenas a fins. O ambiente pode ter outras variáveis que afetam o custo global de CMG a utilizar.

CMG utiliza os seguintes componentes do Azure, que implicar custos para a conta de subscrição do Azure:

#### <a name="virtual-machine"></a>Máquina virtual

- CMG utiliza Cloud Services do Azure como plataforma como serviço (PaaS). Este serviço utiliza as máquinas virtuais (VMs) que implicar custos de computação.  

- No Configuration Manager versão 1706, CMG utiliza uma VM A2 padrão.  

- A partir do Configuration Manager versão 1710, CMG utiliza uma VM de V2 A2 padrão.  

- Selecione a quantas instâncias VM suportam o CMG. Um é a predefinição e 16 é o número máximo. Este número é definido quando criar o CMG e pode ser alterado posteriormente para dimensionar o serviço conforme necessário.

- Para obter mais informações sobre quantas VMs tem de suportar os seus clientes, consulte [desempenho e dimensionamento](#performance-and-scale).

- Consulte o [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/) para ajudar a determinar os custos de potenciais.

    > [!NOTE]  
    > Os custos de máquina virtual variam consoante a região.

#### <a name="outbound-data-transfer"></a>Transferência de dados de saída

- Os encargos baseados nos dados que fluem fora do Azure (saída ou transferir). Os fluxos de dados no Azure são livres (entrada ou carregamento). Fluxos de dados CMG fora do Azure incluem a política de cliente, as notificações do cliente e respostas de clientes reencaminhadas pelo CMG para o site. Essas respostas incluem relatórios de inventário, mensagens de estado e estado de conformidade.  

- Mesmo sem quaisquer clientes que comuniquem com um CMG, alguma comunicação em segundo plano faz com que o tráfego de rede entre o CMG e o site no local.  

- Ver o **transferência de dados de saída (GB)** na consola do Configuration Manager. Para obter mais informações, consulte [monitorizar clientes no CMG](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway).  

- Consulte o [largura de banda do Azure, os detalhes de preços](https://azure.microsoft.com/pricing/details/bandwidth/) para ajudar a determinar os custos de potenciais. Transferência de dados de preço é camada. Mais de utilizar, o menor paga por gigabyte.  

- *Para estimar apenas a fins de*, esperar aproximadamente 100 300 MB por cliente por mês para clientes baseados na internet. A estimativa inferior destina-se uma configuração de cliente predefinida. A estimativa superior destina-se uma configuração mais agressiva do cliente. A utilização real pode variar consoante o modo como configurar definições de cliente.  

   > [!NOTE]  
   > Efetuar outras ações, como a implementação de atualizações de software ou aplicações, aumenta a quantidade de transferência de dados de saída a partir do Azure.

#### <a name="content-storage"></a>Armazenamento de conteúdos

- Os clientes baseados na Internet obtêm conteúdos de atualização de software do Microsoft Windows Update, sem encargos. Não distribuir pacotes de atualização de conteúdo de atualização da Microsoft para um ponto de distribuição na nuvem, caso contrário, pode implicar custos da saída de dados e armazenamento.  

- Para qualquer outro conteúdo necessário, tal como aplicações ou atualizações de software de terceiros, tem de distribuir um ponto de distribuição baseado na nuvem. Atualmente, o CMG suporta apenas o ponto de distribuição baseados na nuvem para a enviar conteúdo para clientes.  

- Para obter mais informações, consulte o custo de utilização [distribuição baseados na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution).  

#### <a name="other-costs"></a>Outros custos

- Cada serviço em nuvem tem um endereço IP dinâmico. Cada CMG distinto utiliza um novo endereço IP dinâmico. Adicionar VMs adicionais por CMG não aumenta estes endereços.  



## <a name="performance-and-scale"></a>Desempenho e dimensionamento

Para obter mais informações sobre dimensionamento CMG, consulte [números de tamanho e a escala](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg).

As seguintes recomendações podem ajudar a melhorar o desempenho de CMG:

- Se possível, configure o CMG, CMG ponto de ligação e o servidor de site do Configuration Manager na mesma região de rede para reduzir a latência.  

- Atualmente, a ligação entre o cliente do Configuration Manager e o CMG não é com suporte para a região.  

- Para elevada disponibilidade do serviço, crie, pelo menos, dois serviços CMG e dois pontos de ligação de CMG por site.  

- Escala CMG para suportar mais clientes ao adicionar mais instâncias VM. O Balanceador de carga do Azure controla ligações de cliente com o serviço.  

- Crie mais pontos de ligação de CMG distribuir a carga entre elas. O CMG distribui o tráfego para os respetivos pontos de ligação CMG ligação em round robin.  

- Quando o CMG está sob uma carga elevada devido a mais do que o número de clientes suportado, processa os pedidos ainda, mas pode existir atraso.  


> [!Note]  
> Enquanto o Configuration Manager não possui nenhum disco rígido limite no número de clientes para um ponto de ligação CMG, o Windows Server tem um predefinição máximo dinâmica intervalo de portas TCP de 16,384. Se um site do Configuration Manager gere 16.384 mais clientes com um único ponto de ligação de CMG, tem de aumentar o limite de Windows Server. Todos os clientes de manter um canal para notificações do cliente, que mantém uma porta aberta no ponto de ligação de CMG. Para obter mais informações sobre como utilizar o comando netsh para aumentar este limite, consulte [artigo Microsoft Support 929851](https://support.microsoft.com/help/929851).



## <a name="ports-and-data-flow"></a>Fluxo de dados e portas

Não é necessário abrir as portas de entrada à sua rede no local. O ponto de ligação de serviço e o ponto de ligação de CMG iniciam todas as comunicações com o Azure e o CMG. Estas funções de sistema de duas sites tem de ser capazes de criar ligações de saída para a nuvem da Microsoft. O ponto de ligação de serviço implementa e monitoriza o serviço do Azure, deste modo, tem de ser modo online. O ponto de ligação de CMG liga ao CMG para gerir a comunicação entre as funções de sistema de sites CMG e no local.

O diagrama seguinte é um fluxo de dados básicas, conceptual para o CMG: ![Fluxo de dados CMG](media/cmg-data-flow.png)
   1. O ponto de ligação de serviço liga-se no Azure através da porta HTTPS 443. Autentica com o Azure AD ou o certificado de gestão do Azure. O ponto de ligação de serviço implementa CMG no Azure. O CMG cria o serviço de nuvem HTTPS utilizando o certificado de autenticação de servidor.  

   2. O ponto de ligação de CMG liga ao CMG no Azure através de TCP TLS ou HTTPS. Mantém a ligação aberta e baseia-se o canal de comunicação bidirecional futura.   

   3. O cliente liga-se a CMG através da porta HTTPS 443. Autentica com o Azure AD ou o certificado de autenticação de cliente.  

   4. O CMG reencaminha a comunicação de cliente através da ligação ao ponto de ligação CMG no local existente. Não precisa de abrir portas de firewall de entrada.  

   5. O ponto de ligação CMG reencaminha a comunicação de cliente para o ponto de gestão no local e o ponto de atualização de software.  

### <a name="required-ports"></a>Portas necessárias
Esta tabela lista as portas de rede necessários e os protocolos. O *cliente* é o dispositivo inicia a ligação, a necessidade de uma porta de saída. O *servidor* o dispositivo de aceitar a ligação, a necessidade de uma porta de entrada. 

| Cliente  | Protocol | Porta  | Servidor  | Descrição  |
|---------|---------|---------|---------|---------|
| Ponto de ligação de serviço     | HTTPS | 443        | Azure        | Implementação de CMG |
| Ponto de ligação de CMG     |  TCP-TLS | 10140-10155        | Serviço CMG        | Preferencial protocolo para criar o canal CMG <sup>1</sup> |
| Ponto de ligação de CMG     | HTTPS | 443        | Serviço CMG       | Contingência para criar o canal CMG para apenas uma instância VM<sup>2</sup> |
| Ponto de ligação de CMG     |  HTTPS   | 10124-10139     | Serviço CMG       | Contingência para criar o canal CMG para duas ou mais instâncias VM<sup>3</sup> |
| Cliente     |  HTTPS | 443         | CMG        | Comunicação de cliente geral |
| Ponto de ligação de CMG      | HTTPS ou HTTP | 443 ou 80         | Ponto de gestão</br>(versão 1706 ou 1710) | O tráfego no local, porta depende da configuração de ponto de gestão |
| Ponto de ligação de CMG      | HTTPS | 443      | Ponto de gestão</br>(versão 1802) | O tráfego no local tem de ser HTTPS |
| Ponto de ligação de CMG      | HTTPS ou HTTP | 443 ou 80         | Ponto de atualização de software | O tráfego no local, porta depende da configuração do ponto de atualização de software |

<sup>1</sup> ponto de ligação de CMG o primeiro tenta estabelecer uma ligação de TCP TLS longa duração com cada instância de CMG VM. Liga-se para a primeira instância VM na porta 10140. A segunda instância VM utiliza a porta 10141, até sixteenth na porta 10155. Uma ligação de TCP TLS efetua o melhor, mas não suporta a proxy de internet. Se o ponto de ligação CMG não é possível ligar através de TCP-TLS, em seguida, retrocede para HTTPS<sup>2</sup>.  

<sup>2</sup> se o ponto de ligação CMG não consegue ligar ao CMG através de TCP TLS<sup>1</sup>, estabelece ligação ao balanceador de carga de rede do Azure através de HTTPS 443 apenas uma instância de VM.  

<sup>3</sup> se existirem dois ou mais instâncias VM, o ponto de ligação CMG utiliza HTTPS 10124 para a primeira instância VM, não de HTTPS 443. Liga-se para a segunda instância VM em HTTPS 10125, até sixteenth na porta HTTPS 10139.


### <a name="internet-access-requirements"></a>Requisitos de acesso à Internet

O sistema de sites do ponto de ligação CMG suporta a utilização de um proxy web. Para obter mais informações sobre como configurar esta função para um proxy, consulte [suporte para o servidor Proxy](/sccm/core/plan-design/network/proxy-server-support#to-set-up-the-proxy-server-for-a-site-system-server). O ponto de ligação CMG necessita de conectividade para os seguintes pontos finais:  

- Os pontos finais do Azure são diferentes por ambiente consoante a configuração. O Configuration Manager armazene estes pontos finais na base de dados do site. Consulta o **AzureEnvironments** tabela no SQL Server para obter a lista de pontos finais do Azure.  

- ServiceManagementEndpoint (https://management.core.windows.net/)  

- StorageEndpoint (core.windows.net)  

- Para o Azure AD token obtenção através da consola do Configuration Manager e do cliente: ActiveDirectoryEndpoint (https://login.microsoftonline.com/)  

- Para deteção de utilizadores do Azure AD: Gráfico do AAD (de ponto finalhttps://graph.windows.net/)  



## <a name="next-steps"></a>Passos seguintes

- [Certificados para o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Segurança e privacidade para o gateway de gestão na cloud ](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Tamanho da gestão do gateway de nuvem e números de escala](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
- [Perguntas mais frequentes sobre o gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Configurar o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)

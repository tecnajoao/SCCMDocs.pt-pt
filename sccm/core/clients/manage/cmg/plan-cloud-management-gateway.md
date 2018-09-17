---
title: Plano para o gateway de gestão da cloud
titleSuffix: Configuration Manager
description: Planear e estruturar o gateway de gestão da cloud (CMG) para simplificar a gestão de clientes baseados na internet.
ms.date: 09/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9b25b7a5b7df42dc83bec18d38b44c7807e6dc1a
ms.sourcegitcommit: 2badee2b63ae63687795250e298f463474063100
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/14/2018
ms.locfileid: "45601131"
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Plano para o gateway de gestão de nuvem no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*
 
<!--1101764--> O gateway de gestão da cloud (CMG) fornece uma forma simples de gerir clientes do Configuration Manager na internet. Ao implementar o CMG como um serviço em nuvem no Microsoft Azure, pode gerir clientes tradicionais que se movem na internet sem infraestrutura adicional. Também não precisa expor a sua infraestrutura no local para a internet. 

> [!Tip]  
> Esse recurso foi introduzido pela primeira vez na versão 1610 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1802, esta funcionalidade já não é uma funcionalidade de pré-lançamento.  


> [!Note]  
> O Configuration Manager não permite esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Depois de estabelecer os pré-requisitos, criar CMG inclui os seguintes três passos na consola do Configuration Manager:
1. Implemente o serviço de nuvem do CMG para o Azure.
2. Adicione a função de ponto de ligação do CMG. 
3. Configure o site e as funções de site para o serviço. Depois de implementado e configurado, os clientes acessem locais funções de sites, independentemente se estão na intranet ou na internet.

Este artigo fornece o conhecimento básico para saber mais sobre o CMG, design, como ela se encaixa no seu ambiente, e planear a implementação. 



## <a name="scenarios"></a>Cenários 

Existem vários cenários para os quais um CMG é vantajoso. Os cenários seguintes são algumas das mais comuns:  

- Gerir clientes tradicionais do Windows com a identidade de associados a um domínio do Active Directory. Esses clientes incluem o Windows 7, Windows 8.1 e Windows 10. Utiliza certificados PKI para proteger o canal de comunicação. Atividades de gestão incluem:  
    - Atualizações de software e o endpoint protection
    - Estado de inventário e de cliente
    - Definições de compatibilidade
    - Distribuição de software no dispositivo
    - Sequência de tarefas de atualização in-loco do Windows 10 (a partir da versão 1802)

- Gerir clientes tradicionais do Windows 10 com a identidade modernos, híbrido ou na cloud pura associados a um domínio com o Azure Active Directory (Azure AD). Os clientes utilizam o Azure AD para autenticar em vez de certificados PKI. Utilizar o Azure AD é mais simples de configurar, configurar e manter do que os sistemas PKI mais complexos. Atividades de gestão são os mesmos que o primeiro cenário, bem como:  
    - Distribuição de software para o utilizador  

- Instale o cliente de Configuration Manager em dispositivos Windows 10 através da internet. Utilizar o Azure AD permite ao dispositivo autenticar para o CMG para o registo de cliente e atribuição. Pode instalar o cliente manualmente, ou utilizar outro método de distribuição de software, como o Microsoft Intune.  

- Novo dispositivo de aprovisionamento com a cogestão. CMG não é necessária para a cogestão. Ele ajuda a concluir um cenário de ponta a ponta para novos dispositivos que envolvem Windows AutoPilot, do Azure AD, o Microsoft Intune e Configuration Manager.  

### <a name="specific-use-cases"></a>Casos de uso específico
Entre estes cenários poderão aplicar-se os seguintes casos de utilização do dispositivo específico:

- Dispositivos móveis, tais como computadores portáteis  

- Dispositivos de office remoto/filial que são menos dispendioso e mais eficiente para gerenciar através de internet que numa WAN ou através de uma VPN.  

- Fusões e aquisições, onde pode ser mais fácil associar dispositivos ao Azure AD e gerir através de um CMG.  

> [!Important]
> Por predefinição, todos os clientes recebem a política para um CMG e começar a utilizar quando se tornam baseado na internet. Consoante o caso de cenário e a utilização aplica-se a sua organização, poderá ter a utilização do âmbito das CMG. Para obter mais informações, consulte a [permitir que os clientes utilizar um gateway de gestão da cloud](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway) definição de cliente.


## <a name="topology-design"></a>Design da topologia

### <a name="cmg-components"></a>Componentes CMG
Implantação e operação do CMG inclui os seguintes componentes:  

- O **serviço de nuvem do CMG** no Azure autentica e reencaminha os pedidos de cliente do Configuration Manager para o ponto de ligação do CMG.  
 
- O **ponto de ligação CMG** função do sistema de sites permite que uma conexão consistente e de elevado desempenho da rede no local para o serviço CMG no Azure. Também publica as definições para o CMG, incluindo as definições de segurança e informações de ligação. O ponto de ligação do CMG reencaminha os pedidos de cliente do CMG para funções no local, de acordo com os mapeamentos de URL.

- O [ **ponto de ligação de serviço** ](/sccm/core/servers/deploy/configure/about-the-service-connection-point) função do sistema de sites é executado o componente Gestor do serviço cloud, que manipula todas as tarefas de implementação do CMG. Além disso, monitoriza e comunica informações de estado de funcionamento e o registo de serviço do Azure AD. Certifique-se de que o ponto de ligação de serviço está no [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).  

- O **ponto de gestão** pedidos de cliente por normal dos serviços de função do sistema de sites.  

- O **ponto de atualização de software** pedidos de cliente por normal dos serviços de função do sistema de sites.  

- **Clientes baseados na Internet** ligar ao CMG para componentes do acesso no local do Configuration Manager.

- O CMG utiliza um **baseada em certificado HTTPS** serviço para o ajudar a proteger a comunicação de rede com os clientes web.  

- Utilização de clientes baseados na Internet **PKI certificados ou o Azure AD** para identidade e autenticação.  

- R [ **ponto de distribuição da nuvem** ](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) fornece conteúdo a clientes baseados na internet, conforme necessário.  

    - A partir da versão 1806, um CMG também pode servir conteúdo aos clientes. Esta funcionalidade reduz os certificados necessários e o custo das VMs do Azure. Para obter mais informações, consulte [modificar um CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).<!--1358651-->  


### <a name="azure-resource-manager"></a>O Azure Resource Manager
<!-- 1324735 --> A partir da versão 1802, pode criar o CMG com um **do Azure Resource Manager deployment**. [O Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para o gerenciamento de todos os recursos de solução como uma única entidade, chamada um [grupo de recursos](/azure/azure-resource-manager/resource-group-overview#resource-groups). Quando implementa o CMG com o Azure Resource Manager, o site utiliza o Azure Active Directory (Azure AD) para autenticar e criar os recursos da cloud necessários. Esta implementação reestruturação não exige o certificado de gestão clássico do Azure.  

O assistente CMG ainda fornece a opção para um **implementação de serviço clássico** a utilizar um certificado de gestão do Azure. Para simplificar a implementação e gestão de recursos, é recomendado utilizar o modelo de implementação Azure Resource Manager para todas as novas instâncias do CMG. Se possível, volte a implementar instâncias CMG existentes através do Resource Manager. Para obter mais informações, consulte [modificar um CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).

> [!IMPORTANT]  
> Esta capacidade não ativa o suporte para fornecedores de serviços de Cloud do Azure (CSP). A implementação do CMG com o Azure Resource Manager continua a utilizar o serviço cloud clássico, que não suporta o CSP. Para obter mais informações, consulte [serviços do Azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services). 


### <a name="hierarchy-design"></a>Estrutura de hierarquia

Crie CMG no site de nível superior da sua hierarquia. Se isto é um site de administração central, em seguida, crie pontos de ligação do CMG em sites primários subordinados. É o componente de Gestor do serviço de nuvem no ponto de ligação de serviço, que também é no site de administração central. Esse design pode partilhar o serviço em diferentes sites primários se for necessário.

Pode criar vários serviços CMG no Azure e pode criar vários pontos de ligação do CMG. Vários pontos de ligação do CMG fornecem balanceamento de carga do tráfego de cliente do CMG para as funções no local. Para reduzir a latência de rede, atribua CMG associado à mesma região geográfica que o site primário.

 > [!Note]  
 > Clientes baseados na Internet e o CMG se encontra em nenhum grupo de limites.

Outros fatores, como o número de clientes para gerir, o impacto sobre o design do CMG. Para obter mais informações, consulte [desempenho e dimensionamento](#performance-and-scale).

#### <a name="example-1-standalone-primary-site"></a>Exemplo 1: site primário autónomo

A Contoso tiver um site primário de autónoma num datacenter no local na sede na cidade de nova York. 
- Eles criam uma CMG na região do Azure do Leste-nos para reduzir a latência de rede. 
- Eles criaram dois pontos de ligação do CMG, vinculados ao serviço CMG único.  

Como os clientes se movem para a internet, comunicam-se com o CMG na região do Azure do Leste-nos. O CMG reencaminha esta comunicação através de ambos os pontos de ligação do CMG.

#### <a name="example-2-hierarchy-with-site-specific-cmg"></a>Exemplo 2: hierarquia com CMG específicas do site

Café quarto tem um site de administração central num datacenter no local na sede em Seattle. Um site primário está no mesmo datacenter, e o outro site primário está no seu sede Européia em Paris. 
- No site de administração central, eles criaram dois serviços CMG:
     - Um CMG na região do Azure do Oeste-nos.
     - Um CMG na região do Azure de Europa Ocidental.
- No site primário com base em Seattle, eles criam um ponto de ligação do CMG ligado para o Oeste nos CMG.
- No site primário com base em Paris, eles criam um ponto de ligação do CMG ligado ao CMG de Europa Ocidental.

Como os clientes baseados em Seattle se movem para a internet, comunicam-se com o CMG na região do Azure do Oeste-nos. Por sua vez encaminha a CMG esta comunicação para o ponto de ligação do CMG com base em Seattle.

Da mesma forma, como os clientes baseados em Paris se movem para a internet, comunicam com o CMG na região do Azure de Europa Ocidental. Por sua vez encaminha a CMG esta comunicação para o ponto de ligação do CMG com base em Paris. Quando os utilizadores com base em Paris viajam para sede da empresa em Seattle, seus computadores continuam a comunicar com o CMG na região do Azure de Europa Ocidental. 

 > [!Note]  
 > Quarto café considerado criar outro ponto de ligação do CMG no site primário com base em Paris ligado para o Oeste nos CMG. Clientes baseados em Paris, em seguida, utilizar ambos os CMGs, independentemente da respetiva localização. Embora esta configuração ajuda a tráfego de balanceamento de carga e fornecer redundância de serviço, poderá também causar atrasos quando os clientes baseados em Paris comunicam com o CMG baseadas nos E.U.A. Clientes do Configuration Manager não têm atualmente conhecimento da sua região geográfica, para que não prefere um CMG que está geograficamente mais próximo. Os clientes utilizam aleatoriamente um CMG disponível.



## <a name="requirements"></a>Requisitos

- Uma **subscrição do Azure** para alojar o CMG.  

    - Uma **administrador do Azure** tem de participar na criação inicial de determinados componentes, dependendo de seu design. Essa pessoa não requer permissões no Configuration Manager.  

- Pelo menos um servidor no local Windows para alojar o **ponto de ligação CMG**. Pode colocalize a esta função com outras funções de sistema de sites do Configuration Manager.  

- O **ponto de ligação de serviço** tem de constar [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).   

- R [ **certificado de autenticação de servidor** ](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate) para CMG.  

- Se utilizar o método de implementação clássica do Azure, tem de utilizar um [ **certificado de gestão do Azure**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#azure-management-certificate).  

    > [!TIP]  
    > A partir do Configuration Manager versão 1802, utilizando o **do Azure Resource Manager** modelo de implementação é recomendado. Não requer este certificado de gestão.  

- **Outros certificados** podem ser necessários, dependendo de seu modelo de autenticação e a versão de SO de cliente. Para obter mais informações, consulte [certificados CMG](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).  

    - A partir da versão 1802, tem de configurar todos os habilitados para CMG [ **pontos de gestão para utilizar HTTPS**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https).  

- Integração com o **do Azure AD** poderá ser necessária para os clientes do Windows 10. Para obter mais informações, consulte [dos serviços do Azure configurar](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- Os clientes têm de utilizar **IPv4**.  



## <a name="specifications"></a>Especificações

- Todas as versões do Windows listadas na [sistemas operativos suportados por clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) são suportadas para CMG.  

- CMG suporta apenas os software e de ponto de atualização de ponto de funções de gestão.  

- CMG não suporta clientes que só comunicam com endereços IPv6.<!--495606-->  

- Pontos de atualização de software com um balanceador de carga de rede não funcionam com CMG. <!--505311-->  

- A partir da versão 1802, implementações de CMG com o modelo de recursos do Azure não ative o suporte para fornecedores de serviços de Cloud do Azure (CSP). A implementação do CMG com o Azure Resource Manager continua a utilizar o serviço de cloud clássica, o que não suporta o CSP. Para obter mais informações, consulte [serviços do Azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services)  


### <a name="support-for-configuration-manager-features"></a>Suporte para funcionalidades do Configuration Manager
A tabela seguinte lista o suporte CMG para recursos do Configuration Manager:


|Funcionalidade  |Suporte  |
|---------|---------|
| Atualizações de software     | ![Suportado](media/green_check.png) |
| Proteção de ponto final     | ![Suportado](media/green_check.png) |
| Inventário de hardware e software     | ![Suportado](media/green_check.png) |
| Estado do cliente e notificações     | ![Suportado](media/green_check.png) |
| Executar scripts     | ![Suportado](media/green_check.png) |
| Definições de compatibilidade     | ![Suportado](media/green_check.png) |
| Instalação de cliente<br>(com a integração do Azure AD)     | ![Suportado](media/green_check.png)  (1706) |
| Distribuição de software (dispositivo-direcionado)     | ![Suportado](media/green_check.png) |
| Distribuição de software (utilizador direcionado, obrigatória)<br>(com a integração do Azure AD)     | ![Suportado](media/green_check.png)  (1710) |
| Distribuição de software (direcionado ao usuário, disponível)<br>([todos os requisitos](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)) | ![Suportado](media/green_check.png)  (1802) |
| Sequência de tarefas de atualização in-loco do Windows 10     | ![Suportado](media/green_check.png)  (1802) |
| CMPivot     | ![Suportado](media/green_check.png)  (1806) |
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
|![Suportado](media/green_check.png) (*YYMM*) = esta funcionalidade é suportada com a partir da versão do CMG *YYMM* do Configuration Manager  |
|![Não suportado](media/Red_X.png) = Esta funcionalidade não é suportada com CMG |



## <a name="cost"></a>Custo

>[!IMPORTANT]  
>A seguinte informação sobre o custo é para estimar apenas para fins. Seu ambiente pode ter outras variáveis que afetam o custo geral da utilização do CMG.

CMG utiliza os seguintes componentes do Azure, que implicar custos à conta de subscrição do Azure:

#### <a name="virtual-machine"></a>Máquina virtual

- CMG utiliza os serviços Cloud do Azure como plataforma como serviço (PaaS). Este serviço utiliza as máquinas virtuais (VMs) que incorrem em custos de computação.  

- No Configuration Manager versão 1706, CMG utiliza uma VM A2 padrão.  

- A partir do Configuration Manager versão 1710, CMG utiliza uma VM de V2 A2 padrão.  

- Selecionar de CMG de suporte de quantas instâncias VM. Uma é a predefinição e 16 é o máximo. Este número é definido quando criar CMG e pode ser alterado posteriormente para dimensionar o serviço, conforme necessário.

- Para obter mais informações sobre o número de VMs tem de suportar os seus clientes, consulte [desempenho e dimensionamento](#performance-and-scale).

- Consulte a [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/) para ajudar a determinar os custos potenciais.

    > [!NOTE]  
    > Os custos de máquina virtual variam consoante a região.

#### <a name="outbound-data-transfer"></a>Transferência de dados de saída

- Os encargos baseiam-se nos dados transmitidos fora do Azure (saída ou transferir). Quaisquer fluxos de dados para o Azure são gratuitos (entrada ou carregamento). Fluxos de dados do CMG fora do Azure incluem a política para o cliente, notificações de cliente e as respostas de clientes reencaminhadas pelo CMG para o site. Essas respostas incluem relatórios de inventário, mensagens de estado e estado de conformidade.  

- Mesmo sem quaisquer clientes que comuniquem com um CMG, alguma comunicação em segundo plano faz com que o tráfego de rede entre o CMG e o site no local.  

- Ver os **transferência de dados de saída (GB)** na consola do Configuration Manager. Para obter mais informações, consulte [monitorizar clientes no CMG](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway).  

- Consulte a [largura de banda do Azure, os detalhes dos preços](https://azure.microsoft.com/pricing/details/bandwidth/) para ajudar a determinar os custos potenciais. Preços para dados de transferência está em camadas. Quanto mais usa, quanto menos paga por gigabyte.  

- *Para estimar apenas para fins*, esperar aproximadamente 300 de 100 MB por cliente por mês para clientes baseados na internet. A estimativa inferior destina-se uma configuração de cliente predefinida. A estimativa superior destina-se uma configuração de cliente mais agressiva. Sua utilização real pode variar dependendo de como configurar definições de cliente.  

   > [!NOTE]  
   > Efetuar outras ações, como a implementação de atualizações de software ou aplicações, aumenta a quantidade de transferência de dados de saída do Azure.

#### <a name="content-storage"></a>Armazenamento de conteúdo

- Clientes baseados na Internet obtém conteúdos de atualização de software Microsoft do Windows Update, sem encargos. Não distribuir pacotes de atualização de conteúdos do Microsoft update para um ponto de distribuição de nuvem, caso contrário, podem incorrer em custos de saída de armazenamento e dados.  

- Para qualquer outro conteúdo necessário, tais como aplicações ou atualizações de software de terceiros, tem de distribuir um ponto de distribuição de nuvem. Atualmente, o CMG suporta apenas o ponto de distribuição de nuvem para enviar conteúdo para os clientes.  

- Para obter mais informações, consulte o custo de utilização [pontos de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_cost).  

- A partir da versão 1806, um CMG também pode servir conteúdo aos clientes. Esta funcionalidade reduz os certificados necessários e o custo das VMs do Azure. Para obter mais informações, consulte [modificar um CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).<!--1358651-->  


#### <a name="other-costs"></a>Outros custos

- Cada serviço em nuvem tem um endereço IP dinâmico. Cada CMG distinto usa um novo endereço IP dinâmico. Adicionar VMs adicionais por CMG não aumenta estes endereços.  



## <a name="performance-and-scale"></a>Desempenho e dimensionamento

Para obter mais informações sobre o dimensionamento do CMG, consulte [tamanho e números da escala](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg).

As seguintes recomendações podem ajudar a melhorar o desempenho do CMG:

- Se possível, configure o CMG, CMG ponto de ligação e o servidor de site do Configuration Manager na mesma região da rede para reduzir a latência.  

- Atualmente, a ligação entre o cliente de Configuration Manager e o CMG não está com suporte para a região.  

- Para elevada disponibilidade do serviço, crie, pelo menos, dois serviços CMG e dois pontos de ligação CMG por site.  

- Dimensione o CMG para suportar mais clientes ao adicionar mais instâncias VM. O Balanceador de carga do Azure controla as ligações de cliente ao serviço.  

- Crie mais pontos de ligação CMG para distribuir a carga entre eles. O CMG distribui o tráfego para os respetivos pontos de ligação CMG ao ligar de forma round robin.  

- Quando o CMG está sob carga elevada devido a mais do que o número suportado de clientes, processa pedidos ainda, mas poderá haver atraso.  


> [!Note]  
> Enquanto o Configuration Manager não possui nenhum limite restritivo no número de clientes para um ponto de ligação do CMG, o Windows Server tem um intervalo de porta dinâmica da TCP máximo do padrão de 16,384. Se a um site do Configuration Manager gerir mais de 16.384 clientes com um único ponto de ligação do CMG, tem de aumentar o limite do Windows Server. Todos os clientes de manter um canal para notificações de cliente, que contém uma porta aberta no ponto de ligação CMG. Para obter mais informações sobre como utilizar o comando netsh para aumentar este limite, consulte [artigo do Microsoft Support 929851](https://support.microsoft.com/help/929851).



## <a name="ports-and-data-flow"></a>Fluxo de dados e de portas

Não precisa abrir nenhuma porta de entrada à sua rede no local. O ponto de ligação de serviço e o ponto de ligação CMG iniciam todas as comunicações com o Azure e o CMG. Estas funções de sistema de duas sites tem de ser capazes de criar ligações de saída para a cloud da Microsoft. O ponto de ligação de serviço implementa e monitoriza o serviço no Azure, assim, tem de ser modo online. O ponto de ligação do CMG se conecta ao CMG para gerir a comunicação entre as funções de sistema de sites CMG e no local.

O diagrama a seguir é um fluxo de dados basic, conceitual para CMG: ![Fluxo de dados do CMG](media/cmg-data-flow.png)
   1. O ponto de ligação de serviço liga ao Azure através da porta HTTPS 443. Autentica com o Azure AD ou o certificado de gestão do Azure. O ponto de ligação de serviço implementa o CMG no Azure. O CMG cria o serviço de nuvem HTTPS utilizando o certificado de autenticação de servidor.  

   2. O ponto de ligação do CMG liga-se ao CMG no Azure através de TCP-TLS ou HTTPS. Ele mantém a conexão aberta e baseia-se o canal de comunicação bidirecional futuras.   

   3. O cliente se conecta ao CMG através da porta HTTPS 443. Autentica com o Azure AD ou o certificado de autenticação de cliente.  

   4. O CMG reencaminha a comunicação de cliente através da ligação existente para o ponto de ligação do CMG no local. Não precisa de abrir portas de firewall de entrada.  

   5. O ponto de ligação do CMG reencaminha a comunicação de cliente para o ponto de gestão no local e o ponto de atualização de software.  

### <a name="required-ports"></a>Portas necessárias
Esta tabela lista os protocolos e portas de rede necessária. O *cliente* é o dispositivo inicia a ligação, que requerem uma porta de saída. O *servidor* é o dispositivo de aceitar a ligação, que requerem uma porta de entrada. 

| Cliente  | Protocol | Porta  | Servidor  | Descrição  |
|---------|---------|---------|---------|---------|
| Ponto de ligação de serviço     | HTTPS | 443        | Azure        | Implementação do CMG |
| Ponto de ligação CMG     |  TCP-TLS | 10140-10155        | Serviço CMG        | Preferência de protocolo para criar o canal CMG <sup>1</sup> |
| Ponto de ligação CMG     | HTTPS | 443        | Serviço CMG       | Contingência para criar o canal CMG para apenas uma instância VM<sup>2</sup> |
| Ponto de ligação CMG     |  HTTPS   | 10124-10139     | Serviço CMG       | Contingência para criar o canal CMG para duas ou mais instâncias VM<sup>3</sup> |
| Cliente     |  HTTPS | 443         | CMG        | Comunicação de cliente geral |
| Ponto de ligação CMG      | HTTPS ou HTTP | 443 ou 80         | Ponto de gestão<br>(versão 1706 ou 1710) | Tráfego no local, porta depende da configuração do ponto de gestão |
| Ponto de ligação CMG      | HTTPS | 443      | Ponto de gestão<br>(versão 1802) | Tráfego no local tem de ser HTTPS |
| Ponto de ligação CMG      | HTTPS ou HTTP | 443 ou 80         | Ponto de atualização de software | Tráfego no local, porta depende da configuração de ponto de atualização de software |

<sup>1</sup> ponto de ligação CMG o primeiro tenta estabelecer uma ligação de TCP-TLS vida útil longa com cada instância de VM do CMG. Ele se conecta à primeira instância VM na porta 10140. A segunda instância VM utiliza a porta 10141, até o 16th na porta 10155. Uma conexão TCP TLS efetua o melhor, mas ele não dá suporte a proxy de internet. Se o ponto de ligação do CMG não é possível ligar através de TCP-TLS, em seguida, vai para HTTPS<sup>2</sup>.  

<sup>2</sup> se o ponto de ligação do CMG não consegue ligar ao CMG via TCP-TLS<sup>1</sup>, ele liga-se ao balanceador de carga de rede do Azure através de HTTPS 443 apenas para uma instância de VM.  

<sup>3</sup> se existirem dois ou mais instâncias VM, o ponto de ligação do CMG utiliza HTTPS 10124 para a primeira instância VM, não HTTPS 443. Liga-se para a segunda instância VM em HTTPS 10125, até o 16th na porta HTTPS 10139.


### <a name="internet-access-requirements"></a>Requisitos de acesso à Internet

O sistema de sites do ponto de ligação CMG suporta a utilização de um proxy web. Para obter mais informações sobre como configurar esta função para um proxy, consulte [suporte de servidor de Proxy](/sccm/core/plan-design/network/proxy-server-support#to-set-up-the-proxy-server-for-a-site-system-server). O ponto de ligação do CMG exige conectividade com os seguintes pontos finais:  

- Os pontos finais do Azure são diferentes por ambiente, dependendo da configuração. Gestor de configuração armazena estes pontos finais da base de dados do site. Consulta a **AzureEnvironments** tabela no SQL Server para a lista de pontos finais do Azure.  

- ServiceManagementEndpoint (https://management.core.windows.net/)  

- StorageEndpoint (core.windows.net)  

- Para o Azure AD token obtenção pela consola do Configuration Manager e do cliente: ActiveDirectoryEndpoint (https://login.microsoftonline.com/)  

- Para deteção de utilizadores do Azure AD: Gráfico do AAD (de ponto final https://graph.windows.net/)   



## <a name="next-steps"></a>Passos seguintes

- [Certificados para o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Segurança e privacidade para o gateway de gestão na cloud ](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Tamanho do gateway de gestão da cloud e dimensione números](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
- [Perguntas mais frequentes sobre o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Configurar o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)

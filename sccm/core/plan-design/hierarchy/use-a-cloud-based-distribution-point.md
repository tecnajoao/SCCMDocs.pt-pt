---
title: Ponto de distribuição de nuvem
titleSuffix: Configuration Manager
description: Planear e estruturar para distribuição de conteúdo de software através do Microsoft Azure com pontos de distribuição de nuvem no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0c41fddef794049456529d9577275a21668717f5
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385461"
---
# <a name="use-a-cloud-distribution-point-in-configuration-manager"></a>Utilizar um ponto de distribuição de nuvem no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Um ponto de distribuição de nuvem é um ponto de distribuição do Configuration Manager que está hospedado como plataforma-como-serviço (PaaS) no Microsoft Azure. Este serviço suporta os seguintes cenários:  

- Fornecer conteúdo de software a clientes baseados na internet sem infraestrutura no local adicional  

- O sistema de distribuição de conteúdo de ativação na cloud  

- Reduzir a necessidade de pontos de distribuição tradicionais  


Este artigo ajuda-o a saber mais sobre o ponto de distribuição na nuvem, o plano para a sua utilização e sua implementação de design. Ele inclui as secções seguintes:
- [Recursos e benefícios](#bkmk_features)
- [Design da topologia](#bkmk_topology)
- [Requisitos](#bkmk_requirements)
- [Especificações](#bkmk_spec)
- [Custo](#bkmk_cost)
- [Desempenho e dimensionamento](#bkmk_perf)
- [Fluxo de dados e de portas](#bkmk_dataflow)
- [Certificados](#bkmk_certs)
- [Perguntas mais frequentes (FAQ)](#bkmk_faq)



## <a name="bkmk_features"></a> Recursos e benefícios

### <a name="features"></a>Funcionalidades

O ponto de distribuição em nuvem oferece suporte a vários recursos que também são oferecidos pelos pontos de distribuição no local:  

-   Gerir pontos de distribuição de nuvem individualmente ou como membros da distribuição de grupos de pontos.  

-   Utilizar um ponto de distribuição de nuvem como uma localização de conteúdo de contingência  

-   Suporta clientes baseados na internet e intranet  


### <a name="benefits"></a>Benefícios

O ponto de distribuição de nuvem fornece os seguintes benefícios adicionais:  

-   O site criptografa o conteúdo antes de os enviar para o ponto de distribuição de nuvem no Azure.  

-   Para atender às mudanças na procura para pedidos de conteúdo por clientes, dimensione manualmente o serviço em nuvem no Azure. Esta ação não requer que instalar e aprovisionar pontos de distribuição adicionais no Configuration Manager.  

-   Suporta a transferência do conteúdo dos clientes configurados para outras tecnologias de conteúdo, como o Windows BranchCache e fornecedores de conteúdo alternativos.  

-   A partir da versão 1806, utilize pontos de distribuição de nuvem como localizações de origem para os pontos de distribuição de extração.  


## <a name="bkmk_topology"></a> Design da topologia

Implantação e operação do ponto de distribuição em nuvem inclui os seguintes componentes:  

- R **serviço em nuvem** no Azure. O site distribui conteúdo para este serviço, que armazena no armazenamento na cloud do Azure. O ponto de gestão fornece aos clientes esta localização de conteúdo, na lista de origens disponíveis conforme apropriado.  

- R **ponto de gestão** pedidos de cliente por normal dos serviços de função do sistema de sites.  

    - Clientes no local, normalmente, utilizem um ponto de gestão no local.  

    - Clientes baseados na Internet ou utilizam um [gateway de gestão na cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway), ou uma [ponto de gestão baseado na internet](/sccm/core/clients/manage/plan-internet-based-client-management).  

- O ponto de distribuição de nuvem utiliza uma **baseada em certificado HTTPS** serviço para o ajudar a proteger a comunicação de rede com os clientes web. Os clientes têm de confiar este certificado.  


### <a name="azure-resource-manager"></a>O Azure Resource Manager
<!--1322209--> A partir da versão 1806, criar um através de ponto de distribuição do cloud uma **do Azure Resource Manager deployment**. [O Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para o gerenciamento de todos os recursos de solução como uma única entidade, chamada um [grupo de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Ao implementar um ponto de distribuição de nuvem com o Azure Resource Manager, o site utiliza o Azure Active Directory (Azure AD) para autenticar e criar os recursos da cloud necessários. Esta implementação reestruturação não exige o certificado de gestão clássico do Azure.  

O Assistente de ponto de distribuição de nuvem ainda fornece a opção para um **implementação de serviço clássico** a utilizar um certificado de gestão do Azure. Para simplificar a implementação e gestão de recursos, a Microsoft recomenda a utilizar o modelo de implementação Azure Resource Manager para todos os novos pontos de distribuição de nuvem. Se possível, volte a implementar pontos de distribuição existentes na cloud através do Resource Manager.

O Configuration Manager não migrar pontos de distribuição de cloud clássica existentes para o modelo de implementação Azure Resource Manager. Criar nova nuvem pontos de distribuição com implementações do Azure Resource Manager e, em seguida, remova os pontos de distribuição de cloud clássica. 

> [!IMPORTANT]  
> Esta funcionalidade não ative o suporte para fornecedores de serviços de Cloud do Azure (CSP). A implementação de ponto de distribuição em nuvem com o Azure Resource Manager continua a utilizar o serviço de cloud clássica, o que não suporta o CSP. Para obter mais informações, consulte [serviços do Azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  


### <a name="hierarchy-design"></a>Estrutura de hierarquia

Quando cria o ponto de distribuição de nuvem depende os clientes que precisam de aceder o conteúdo. A partir da versão 1806, existem três tipos de pontos de distribuição de nuvem:  

- Implementação de serviço clássico: Crie este tipo de apenas um site primário.  

- Implementação do Gestor de recursos do Azure: Crie este tipo num site primário ou site de administração central.  

- O gateway de gestão na cloud também pode servir conteúdo aos clientes. Esta funcionalidade reduz os certificados necessários e o custo das VMs do Azure. Para obter mais informações, consulte [planear para o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).<!--1358651-->  


Para determinar se deve incluir os pontos de distribuição de nuvem em grupos de limites, considere os seguintes comportamentos:  

- Clientes baseados na Internet não contam com grupos de limites. Eles apenas utilizam pontos de distribuição de acesso à internet ou pontos de distribuição de nuvem. Se estiver a utilizar apenas os pontos de distribuição de nuvem para atender a esses tipos de clientes, em seguida, não precisa para incluí-los em grupos de limites.  

- Se pretender que os clientes na sua rede interna a utilizar um ponto de distribuição de nuvem, em seguida, ele precisa estar no mesmo grupo de limites que os clientes. Os clientes priorizar pontos de distribuição em nuvem pela última vez na sua lista de fontes de conteúdo, porque não existe um custo associado a transferir conteúdo fora do Azure. Portanto, um ponto de distribuição de nuvem é normalmente utilizado como uma origem de contingência para clientes baseados na intranet. Se pretender que um design de cloud-first, design, em seguida, os grupos de limites para cumprir este requisito de negócio. Para obter mais informações, consulte [configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).  


Apesar de o instalar pontos de distribuição de nuvem em regiões específicas do Azure, os clientes não estão cientes das regiões do Azure. Eles selecionam aleatoriamente um ponto de distribuição de nuvem. Se instalar pontos de distribuição de nuvem em várias regiões e um cliente recebe mais do que um na lista de localização de conteúdo, o cliente poderá não utilizar um ponto de distribuição de nuvem da mesma região do Azure.  


### <a name="backup-and-recovery"></a>Cópia de segurança e recuperação  

Quando utiliza um ponto de distribuição em nuvem na sua hierarquia, utilize as seguintes informações para ajudar a planear a cópia de segurança e recuperação:  

- Quando utiliza a **servidor do Site de cópia de segurança** tarefa de manutenção, o Configuration Manager inclui automaticamente as configurações para o ponto de distribuição de nuvem.  

- Faça uma cópia de segurança e guarde uma cópia do certificado de autenticação de servidor. Se utilizar a implementação do serviço clássico no Azure, também faça uma cópia de segurança e guarde uma cópia do certificado de gestão do Azure. Ao restaurar o site primário do Configuration Manager para um servidor diferente, tem de reimportar os certificados.  



##  <a name="bkmk_requirements"></a> Requisitos

- É necessário um **subscrição do Azure** para hospedar o serviço.  

    - Uma **administrador do Azure** tem de participar na criação inicial de determinados componentes, dependendo de seu design. Essa pessoa não requer permissões no Configuration Manager.  

- O servidor de site requer **acesso à internet** para implementar e gerir o serviço em nuvem.  

- Se utilizar o método de implementação clássica do Azure, terá uma **certificado de gestão do Azure**. Para obter mais informações, consulte a [certificados](#bkmk_certs) secção abaixo.   

    > [!TIP]  
    > A partir do Configuration Manager versão 1806, utilize o **do Azure Resource Manager** modelo de implementação. Ele não requer este certificado de gestão.  

- Se utilizar o **do Azure Resource Manager** método de implementação, integrar com o Configuration Manager [do Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Deteção de utilizadores do Azure AD não é necessária.  

- R **certificado de autenticação de servidor**. Para obter mais informações, consulte a [certificados](#bkmk_certs) secção abaixo.  

    - Para reduzir a complexidade, a Microsoft recomenda a utilização de um fornecedor do certificado público para o certificado de autenticação de servidor. Ao fazê-lo, terá também uma **alias de DNS CNAME** resolver o nome do serviço cloud, os clientes.  

- Definir o definição de cliente **permitir o acesso a pontos de distribuição de nuvem**ao **Sim** no **serviços Cloud** grupo. Por predefinição, este valor está definido como **Não**.  

- Os dispositivos de cliente requerem **conectividade à internet**e tem de utilizar **IPv4**.  



## <a name="bkmk_spec"></a> Especificações

- O ponto de distribuição de nuvem suporta todas as versões do Windows listadas na [sistemas operativos suportados por clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).  

- Um administrador distribui os seguintes tipos de conteúdo de software suportado:  
    - Aplicações
    - Pacotes
    - Pacotes de atualização do SO
    - Atualizações de software de terceiros  

    > [!Important]  
    > Embora a consola do Configuration Manager não bloqueia a distribuição de atualizações de software da Microsoft para um ponto de distribuição de nuvem, está pagando os custos do Azure para armazenar o conteúdo que os clientes não utilizam. Clientes baseados na Internet sempre obtém conteúdos de atualização de software Microsoft do serviço de nuvem do Microsoft Update. Não distribua atualizações de software da Microsoft para um ponto de distribuição de nuvem.    

- A partir da versão 1806, configure um ponto de distribuição de extração para utilizar um ponto de distribuição de nuvem como uma origem. Para obter mais informações, consulte [sobre pontos de distribuição de origem](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point#about-source-distribution-points).<!--1321554-->  


### <a name="deployment-settings"></a>Definições da implementação

- Quando implementa uma sequência de tarefas com a opção para **transferir o conteúdo localmente quando necessário para executar a sequência de tarefas**, o ponto de gestão não inclui um ponto de distribuição de nuvem como uma localização de conteúdo. Implementar a sequência de tarefas com a opção para **transferir todo o conteúdo localmente antes de iniciar a sequência de tarefas** para os clientes utilizem um ponto de distribuição de nuvem.  

- Um ponto de distribuição na nuvem não suporta implementações de pacote com a opção para **executar programa a partir do ponto de distribuição**. Utilize a opção de implementação para **transferir conteúdo do ponto de distribuição e executar localmente**.  


### <a name="limitations"></a>Limitações  

- Não é possível utilizar um ponto de distribuição de cloud para implementações de capacidade multicast ou de PXE.  

- Um ponto de distribuição na nuvem não suporta aplicações de transmissão em fluxo do App-V.  

- Não é possível [pré-configurar conteúdo](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent) num ponto de distribuição na nuvem. O Gestor de distribuição do site primário que gere o ponto de distribuição na nuvem transfere todo o conteúdo.  

- Não é possível configurar um ponto de distribuição de nuvem como um ponto de distribuição de extração.  



##  <a name="bkmk_cost"></a> Custo   
<!--501018-->
> [!IMPORTANT]  
> A seguinte informação sobre o custo é para estimar apenas para fins. Seu ambiente pode ter outras variáveis que afetam o custo geral da utilização de um ponto de distribuição de nuvem.  

O Configuration Manager inclui as seguintes opções para ajudar a controlar os custos e monitorizar o acesso de dados:  

- Controlar e monitorizar a quantidade de conteúdo que armazena num serviço cloud. Para obter mais informações, consulte [pontos de distribuição de nuvem de Monitor](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure#bkmk_monitor).  

- Configure o Configuration Manager para o alertar quando os limiares para transferências do cliente atingirem ou ultrapassarem o limites mensais. Para obter mais informações, consulte [alertas de limiar de transferência de dados](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure#bkmk_alerts).   

- Para ajudar a reduzir o número de transferências de dados a partir de pontos de distribuição de nuvem pelos clientes, utilize um do elemento de rede seguinte tecnologias de colocação em cache:  
    - Cache de elemento de rede do Configuration Manager
    - BranchCache do Windows
    - Otimização da entrega do Windows 10  

   Para obter mais informações, consulte [conceitos fundamentais da gestão de conteúdos](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).   


### <a name="components"></a>Componentes

Um ponto de distribuição de nuvem utiliza os seguintes componentes do Azure, que implicar custos à conta de subscrição do Azure:  

> [!Tip]  
> A partir da versão 1806, o gateway de gestão na cloud também pode servir conteúdo aos clientes. Esta funcionalidade reduz o custo por meio da consolidação as VMs do Azure. Para obter mais informações, consulte [de custos para o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#cost).  

#### <a name="virtual-machine"></a>Máquina virtual
- O ponto de distribuição de nuvem utiliza os serviços Cloud do Azure como plataforma como serviço (PaaS). Este serviço utiliza as máquinas virtuais (VMs) que incorrem em custos de computação.  

- Cada serviço de ponto de distribuição em nuvem utiliza duas VMs de A0 padrão.  

- Consulte a [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/) para ajudar a determinar os custos potenciais.

    > [!NOTE]  
    > Os custos de máquina virtual variam consoante a região.

#### <a name="outbound-data-transfer"></a>Transferência de dados de saída
- Quaisquer fluxos de dados no Azure são gratuitos (entrada ou carregamento). Distribuição de conteúdo do site para o ponto de distribuição em nuvem está a carregar para o Azure.  

- Os encargos baseiam-se nos dados transmitidos fora do Azure (saída ou transferir). Fluxos de dados do cloud distribuição ponto fora do Azure consistem em que os clientes transferem conteúdo de software.  

- Para obter mais informações, consulte [pontos de distribuição de nuvem de Monitor](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure#bkmk_monitor).  

- Consulte a [largura de banda do Azure, os detalhes dos preços](https://azure.microsoft.com/pricing/details/bandwidth/) para ajudar a determinar os custos potenciais. Preços para dados de transferência está em camadas. Quanto mais usa, quanto menos paga por gigabyte.  

#### <a name="content-storage"></a>Armazenamento de conteúdo
- Clientes baseados na Internet obtém conteúdos de atualização de software Microsoft do serviço de nuvem do Microsoft Update, sem qualquer custo. Não distribua pacotes de implementação de atualização de software com atualizações de software da Microsoft para um ponto de distribuição de nuvem. Caso contrário, irá incorrer em custos de armazenamento de dados para o conteúdo que os clientes nunca utilizam.  

- Pontos de distribuição de nuvem utilizam o armazenamento de BLOBs padrão seguintes, consoante o modelo de implementação:  

    - Implementação clássica utiliza o Azure armazenamento georredundante (GRS). Para obter mais informações, consulte [armazenamento georredundante](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs).  

    - Uma implementação do Azure Resource Manager utilizar do Azure-armazenamento localmente redundante (LRS). Esta alteração reduz o custo da conta de armazenamento. A implementação clássica não estava a utilizar as funcionalidades adicionais do GRS. Para obter mais informações, consulte [armazenamento localmente redundante](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs).  

#### <a name="other-costs"></a>Outros custos
- Cada serviço em nuvem tem um endereço IP dinâmico. Cada ponto de distribuição de nuvem distintas usa um novo endereço IP dinâmico. Adicionar VMs adicionais por serviço cloud não aumenta estes endereços.  



##  <a name="bkmk_dataflow"></a> Fluxo de dados e de portas   

Existem dois fluxos de dados principal para o ponto de distribuição de nuvem:  

- O servidor de sites liga ao Azure para configurar o serviço de ponto de distribuição em nuvem  

- Um cliente liga-se ao ponto de distribuição em nuvem para transferir conteúdo  


### <a name="site-server-to-azure"></a>Servidor do site para o Azure

Não precisa abrir nenhuma porta de entrada à sua rede no local. O servidor do site inicia todas as comunicações com o Azure e o ponto de distribuição de cloud para implementar, atualizar e gerir o serviço em nuvem. O servidor do site tem de ser capaz de criar ligações de saída para a cloud da Microsoft. Esta ação equivale a instalar a função de sistema de sites de ponto de distribuição num site específico.  


### <a name="client-to-cloud-distribution-point"></a>Cliente para ponto de distribuição da nuvem

Não precisa abrir nenhuma porta de entrada à sua rede no local. Clientes baseados na Internet comunicam diretamente com o serviço do Azure. Os clientes na sua rede interna que utilizam um ponto de distribuição de nuvem tem de ser capazes de ligar a cloud da Microsoft. 

Para obter mais informações sobre o quando os clientes baseados na intranet utilizam um ponto de distribuição de nuvem e de prioridade de localização de conteúdo, consulte [prioridade de origem de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#content-source-priority).

Quando um cliente utiliza um ponto de distribuição de nuvem como uma localização de conteúdo:  

1. O ponto de gestão atribui o cliente um token de acesso, juntamente com a lista de fontes de conteúdo. Este token é válido durante 24 horas e oferece o acesso de cliente para o ponto de distribuição de nuvem.  

2. O ponto de gestão responde ao pedido de localização do cliente com o **FQDN de serviço** de ponto de distribuição de nuvem. Esta propriedade é igual ao nome comum do certificado de autenticação de servidor.  

    Se estiver a utilizar o seu nome de domínio, por exemplo, WallaceFalls.contoso.com, em seguida, o cliente tenta primeiro resolver este FQDN. É necessário um alias CNAME no DNS de acesso à internet do seu domínio para que os clientes resolver o nome de serviço do Azure, por exemplo: WallaceFalls.cloudapp.net.  

3. Em seguida o cliente resolve o nome do serviço do Azure, por exemplo, WallaceFalls.cloudapp.net, para um endereço IP válido. Esta resposta deve ser processada do Azure DNS.  

4. O cliente liga-se ao ponto de distribuição de nuvem. Carga do Azure equilibra a ligação a uma das instâncias de VM. O cliente autentica-se automaticamente com o token de acesso.  

5. O ponto de distribuição de nuvem efetua a autenticação de token de acesso do cliente e, em seguida, atribui o cliente a localização exata do conteúdo no armazenamento do Azure.  

6. Se o cliente confia no certificado de autenticação de servidor do ponto de distribuição de nuvem, ele se conecta ao armazenamento do Azure para transferir o conteúdo. 



##  <a name="bkmk_perf"></a> Desempenho e dimensionamento   
<!--494872-->

Como com qualquer distribuição ponto de design, considere os seguintes fatores:  
- Número de ligações de cliente simultâneas
- O tamanho do conteúdo que os clientes transferem
- O período de tempo permitido para cumprir os requisitos comerciais 

Dependendo da sua [design da topologia](#bkmk_topology), se os clientes têm a opção de mais do que um ponto de distribuição de nuvem para qualquer conteúdo determinado, em seguida, eles naturalmente tornar aleatórios entre esses serviços cloud. Se distribuir apenas um determinado conteúdo a um ponto de distribuição de nuvem única e um grande número de clientes por tentar transferir este conteúdo ao mesmo tempo, esta atividade coloca carga superior nesse ponto de distribuição de nuvem única. Adicionar um ponto de distribuição de nuvem adicional inclui também um serviço de armazenamento do Azure separadas. Para obter mais informações sobre como o cliente comunica com os componentes de ponto de distribuição de nuvem e o conteúdo de downloads, consulte [fluxo de dados e de portas](#bkmk_dataflow).  

O ponto de distribuição de nuvem utiliza duas VMs do Azure como o front-end para o armazenamento do Azure. Esta implementação padrão atende às necessidades da maioria dos clientes. Em algumas circunstâncias extremas, com um grande número de ligações de cliente em simultâneo (por exemplo, 150 000 clientes), a capacidade de processamento das VMs do Azure não é possível acompanhar os pedidos de cliente. Não pode redimensionar as VMs do Azure utilizada para o ponto de distribuição de nuvem. Embora não é possível configurar o número de instâncias VM para o ponto de distribuição de nuvem no Configuration Manager, se necessário, reconfigure o serviço em nuvem no portal do Azure. Manualmente adicionar mais instâncias VM ou configurar o serviço para dimensionar automaticamente. 

> [!Important]  
> Ao atualizar do Configuration Manager, o site reimplementa o serviço em nuvem. Se reconfigurar manualmente o serviço em nuvem no portal do Azure, repõe o número de instâncias para a predefinição de dois.  

O serviço de armazenamento do Azure suporta 500 pedidos por segundo para um único arquivo. Testes de desempenho de um ponto de distribuição de nuvem única suportada a distribuição de um único ficheiro de 100 MB a 50 000 clientes em 24 horas.<!--512106-->  



##  <a name="bkmk_certs"></a> Certificados  

Consoante a sua estrutura de ponto de distribuição de nuvem, é necessário um ou mais certificados digitais.  


### <a name="azure-management-certificate"></a>Certificado de gestão do Azure

*Este certificado é necessário para implementações de serviços clássico. Não é necessário para implementações do Azure Resource Manager.*

Se utilizar o método de implementação clássica do Azure, terá uma **certificado de gestão do Azure**. Para obter mais informações, consulte a [certificado de gestão do Azure](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#azure-management-certificate) secção do artigo de certificados de gateway de gestão na cloud. Servidor de site do Configuration Manager utiliza este certificado para autenticar com o Azure para criar e gerir a implementação clássica.  

> [!TIP]  
> A partir do Configuration Manager versão 1806, utilize o **do Azure Resource Manager** modelo de implementação. Ele não requer este certificado de gestão.  

Para reduzir a complexidade, utilize o mesmo certificado de gestão do Azure para todas as implementações clássicas de pontos de distribuição de nuvem e gateways de gestão da cloud, entre subscrições de contas do Azure e todos os sites do Configuration Manager.


### <a name="server-authentication-certificate"></a>Certificado de autenticação de servidor

*Este certificado é necessário para todas as implementações de ponto de distribuição de nuvem.*

Para obter mais informações, consulte [certificado de autenticação de servidor CMG](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate)e as subsecções seguintes, conforme necessário:  
- Certificado de raiz fidedigna do CMG para clientes
- Certificado de autenticação de servidor emitido por fornecedor público
- Certificado de autenticação de servidor emitido por enterprise PKI

O ponto de distribuição de nuvem utiliza este tipo de certificado da mesma forma que o gateway de gestão na cloud. Os clientes também precisam de confiar este certificado. Para reduzir a complexidade, a Microsoft recomenda a utilização de um certificado emitido por um fornecedor público. 

A menos que utilize um certificado de caráter universal, não reutilize o mesmo certificado. Cada instância do ponto de distribuição de nuvem e o gateway de gestão de cloud requer um certificado de autenticação de servidor exclusivo. 

Para obter mais informações sobre como criar este certificado de uma PKI, consulte [implementar o certificado de serviço para pontos de distribuição de nuvem](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012).  



##  <a name="bkmk_faq"></a> Perguntas mais frequentes (FAQ)   

### <a name="does-a-client-need-a-certificate-to-download-content-from-a-cloud-distribution-point"></a>Um cliente precisa de um certificado para transferir conteúdo de um ponto de distribuição em nuvem?

Um certificado de autenticação de cliente não é necessário. O cliente tem de confiar no certificado de autenticação de servidor utilizado pelo ponto de distribuição de nuvem. Se este certificado é emitido por um fornecedor do certificado público, em seguida, a maioria dos dispositivos do Windows já incluem certificados de raiz fidedigna para esses provedores. Se emitido um certificado de autenticação de servidor de PKI da sua organização, em seguida, os clientes tem de confiar nos certificados emissoras em toda a cadeia. Esta cadeia inclui a autoridade de certificação de raiz e quaisquer autoridades de certificação intermediárias. Consoante o seu design PKI, este certificado pode introduzir complexidade adicional para a implementação de ponto de distribuição de nuvem. Para evitar essa complexidade, a Microsoft recomenda a utilização de um provedor de certificado público que seus clientes já confiam.  


### <a name="can-my-on-premises-clients-use-a-cloud-distribution-point"></a>Meus clientes no local podem utilizar um ponto de distribuição em nuvem?

Sim. Se pretender que os clientes na sua rede interna a utilizar um ponto de distribuição de nuvem, em seguida, ele precisa estar no mesmo grupo de limites que os clientes. Os clientes priorizar pontos de distribuição em nuvem pela última vez na sua lista de fontes de conteúdo, porque não existe um custo associado a transferir conteúdo fora do Azure. Portanto, um ponto de distribuição de nuvem é normalmente utilizado como uma origem de contingência para clientes baseados na intranet. Se pretender que um design de nuvem em primeiro lugar, em seguida, de design seus grupos de limites em conformidade. Para obter mais informações, consulte [configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).  


### <a name="do-i-need-azure-expressroute"></a>Preciso que o Azure ExpressRoute?

[O Azure ExpressRoute](/azure/expressroute/expressroute-introduction) permite-lhe expandir a sua rede no local para a cloud da Microsoft. ExpressRoute ou outros tais conexões de rede virtual não são necessários para o ponto de distribuição de nuvem do Configuration Manager.  

Se a sua organização utiliza o ExpressRoute, isole a subscrição do Azure para o ponto de distribuição de nuvem da subscrição que utiliza o ExpressRoute. Esta configuração garante que o ponto de distribuição de nuvem acidentalmente não está ligado dessa maneira.  


### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>É necessário manter as máquinas virtuais do Azure?

Sem manutenção é necessária. O design do ponto de distribuição de nuvem utiliza a plataforma do Azure como um serviço (PaaS). Utilizar a subscrição que é fornecer, o Configuration Manager cria necessário VMs, armazenamento e rede. O Azure protege e atualiza as máquinas virtuais. Estas VMs não são uma parte do seu ambiente no local, assim como acontece com a infraestrutura como serviço (IaaS). O ponto de distribuição de nuvem é uma PaaS que estende o ambiente do Configuration Manager para a cloud. Para obter mais informações, consulte [vantagens de segurança de um modelo de serviço de nuvem de PaaS](https://docs.microsoft.com/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model).  


### <a name="does-the-cloud-distribution-point-use-azure-cdn"></a>O ponto de distribuição de nuvem usa a CDN do Azure?

Rede de entrega de conteúdos (CDN) do Azure é uma solução global para o fornecimento rápido de conteúdo de largura de banda alta ao colocar em cache o conteúdo em nós físicos estrategicamente colocados em todo o mundo. Para obter mais informações, consulte [o que é o Azure CDN?](https://docs.microsoft.com/azure/cdn/cdn-overview).

Atualmente, o ponto de distribuição de nuvem do Configuration Manager não suporta da CDN do Azure.



## <a name="next-steps"></a>Passos seguintes
[Instalar pontos de distribuição de nuvem](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)

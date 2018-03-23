---
title: Planear para o gateway de gestão de nuvem
titleSuffix: Configuration Manager
description: ''
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 051d3fcba379aec83ea7c4dc1e407b3d3e774e12
ms.sourcegitcommit: d03e4dee92a31dd214c528e895379f6013b7de82
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Planear para o gateway de gestão de nuvem no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir da versão 1610, o gateway de gestão de nuvem fornece uma forma simples de gerir clientes do Configuration Manager na Internet. O serviço de gateway de gestão de nuvem é implementado no Microsoft Azure e requer uma subscrição do Azure. Estabelece ligação à sua infraestrutura do Configuration Manager no local através de uma nova função de chamar o ponto de conector de gateway de gestão de nuvem. Assim que implementado e configurado, os clientes poderão aceder a funções de sistema de sites no local do Configuration Manager, independentemente se estão contidos no privada interna rede ou na Internet.

> [!TIP]  
> Introduzido com a versão 1610, o gateway de gestão de nuvem é uma funcionalidade de pré-lançamento. Para ativá-la, consulte o artigo [utilizar as funcionalidades de pré-lançamento das atualizações da](/sccm/core/servers/manage/pre-release-features).

Utilize a consola do Configuration Manager para implementar o serviço no Azure, adicionar a função de ponto de conector de gateway de gestão de nuvem e configurar funções de sistema de sites para permitir tráfego de gateway de gestão de nuvem. Gateway de gestão de nuvem só suporta atualmente os software e de ponto de atualização ponto funções de gestão.

São necessários certificados de cliente e certificados de Secure Socket Layer (SSL) para autenticar computadores e encriptar comunicações entre as diferentes camadas do serviço. Computadores cliente recebem normalmente um certificado de cliente através da imposição de política de grupo. Para encriptar o tráfego entre clientes e servidor de sistema de sites que alojam as funções, terá de criar um certificado SSL personalizado da AC. Também tem de configurar um certificado de gestão no Azure que permite ao Configuration Manager para implementar o serviço de gateway de gestão de nuvem.

## <a name="requirements-for-cloud-management-gateway"></a>Requisitos do gateway de gestão de nuvem

-    Sistema de sites que executa o conector de gateway de gestão de nuvem para clientes baseados na Internet utilizar.

-   Certificados SSL personalizados da AC interna - utilizado para encriptar a comunicação entre os computadores cliente e autenticar a identidade do serviço de gateway de gestão de nuvem.

-   Subscrição do Azure para serviços em nuvem.

-   Certificado de gestão do Azure - utilizado para autenticar o Configuration Manager com o Azure.

## <a name="specifications-for-cloud-management-gateway"></a>Especificações para o gateway de gestão de nuvem

- Cada instância do gateway de gestão de nuvem suporta 4 000 clientes.
- Recomendamos que crie, pelo menos, duas instâncias do gateway de gestão de nuvem para melhorar a disponibilidade.
- Gateway de gestão de nuvem suporta apenas os software e de ponto de atualização ponto funções de gestão.
-   As seguintes funcionalidades no Configuration Manager não são atualmente suportadas para o gateway de gestão de nuvem:

    -   Instalação push do cliente
    -   Atribuição automática de site
    -   Catálogo de aplicações (incluindo pedidos de aprovação de software)
    -   Implementação completa do sistema operativo (OSD)
    -   Sequências de tarefas (todos)
    -   Consola do Configuration Manager
    -   Ferramentas remotas
    -   Relatórios Web site
    -   Reativação por LAN
    -   Clientes Mac, Linux e UNIX
    -   O Azure Resource Manager
    -   Cache ponto a ponto
    -   Gestão de Dispositivos Móveis no Local

## <a name="cost-of-cloud-management-gateway"></a>Custo de gateway de gestão de nuvem

>[!IMPORTANT]
>Informação do custo que se segue para estimar apenas a fins. O ambiente, poderá ter outras variáveis que afetam o custo global de utilizar o gateway de gestão de nuvem.

Gateway de gestão de nuvem utiliza a seguinte funcionalidade Microsoft Azure, o que implica os encargos para a conta de subscrição do Azure:

-   Máquina virtual

    -   Gateway de gestão na nuvem atualmente requer um padrão\_A2 máquina. Ao criar o serviço, pode selecionar quantas VMs para suportar o serviço (um é a predefinição).

    -   Para estimar apenas a fins, esperar que um único do Azure Standard\_máquina virtual de A2 pode suportar aproximadamente 2.000 simultâneos baseado na Internet clientes.

    -   Consulte o [Calculadora de preços do Azure](https://azure.microsoft.com/en-us/pricing/calculator/) para ajudar a determinar os custos de potenciais.

      >[!NOTE]
      >Os custos de máquina virtual variam consoante a região.

-   Transferência de dados de saída

    -   São cobradas taxas de dados que fluem fora de serviço. Consulte o [largura de banda do Azure, os detalhes de preços](https://azure.microsoft.com/pricing/details/bandwidth/) para ajudar a determinar os custos de potenciais.

    -   Para estimar apenas a fins, espere aproximadamente 100 MB por cliente por mês para clientes baseados na Internet fazer atualizações da política a cada hora.

    >[!NOTE]
    > Efetuar outras ações suportadas através do gateway de gestão de nuvem (por exemplo, a implementação de atualizações de software ou aplicações) irá aumentar a quantidade de transferência de dados de saída a partir do Azure.

-   Armazenamento de conteúdos

    -   Os clientes baseados na Internet geridos com o gateway de gestão de nuvem irão obter conteúdos de atualização de software do Windows Update, sem encargos.

    -   Qualquer outro conteúdo necessário (por exemplo, aplicações) têm de ser distribuído para um ponto de distribuição baseado na nuvem. Atualmente, o gateway de gestão de nuvem suporta apenas o ponto de distribuição em nuvem para a enviar conteúdo para clientes.

    - Consulte o custo de utilização um [distribuição baseados na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution) para obter mais detalhes.

## <a name="frequently-asked-questions-about-the-cloud-management-gateway-cmg"></a>Perguntas mais frequentes sobre o gateway de gestão de nuvem (CMG)

### <a name="why-use-the-cloud-management-gateway"></a>Porquê utilizar o gateway de gestão da nuvem?

Utilize esta função para simplificar a gestão de clientes baseada na Internet em três passos a partir da consola do Configuration Manager.

1. Implementar o CMG no Azure com o [criar Gateway de gestão de nuvem](/sccm/core/clients/manage/setup-cloud-management-gateway) assistente.
2. Configurar o [ponto de ligação de gateway de gestão de nuvem](/sccm/core/servers/deploy/configure/install-site-system-roles) função do sistema de sites.
3. [Configurar funções para o tráfego de gateway de gestão de nuvem](/sccm/core/clients/manage/setup-cloud-management-gateway#step-7-configure-roles-for-cloud-management-gateway-traffic), como o ponto de gestão e atualização de software ponto.

### <a name="how-does-the-cloud-management-gateway-work"></a>Como funciona o gateway de gestão da nuvem?

- O ponto de ligação de gateway de gestão de nuvem permite uma ligação consistente e de elevado desempenho através da Internet para o gateway de gestão de nuvem.
- O Configuration Manager publica definições CMG, incluindo as definições de segurança e informações de ligação.
- O CMG autentica e reencaminha os pedidos de cliente do Configuration Manager para o ponto de ligação de gateway de gestão de nuvem. Estes pedidos são reencaminhados para funções na rede da empresa, de acordo com os mapeamentos de URL.

### <a name="how-is-the-cloud-management-gateway-deployed"></a>Como é implementar o gateway de gestão da nuvem?

O componente de Gestor do serviço de nuvem no ponto de ligação de serviço processa todas as tarefas de implementação de CMG. Além disso, monitoriza e comunica informações de estado de funcionamento e o registo de serviço do Azure AD. Certifique-se de que o ponto de ligação de serviço está no [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).

#### <a name="certificate-requirements"></a>Requisitos de certificados

Terá dos seguintes certificados para proteger o CMG:

- **Certificado de gestão** -Isto pode ser qualquer certificado, incluindo certificados autoassinados. Pode utilizar um certificado público carregado para o Azure AD ou um [PFX com chave privada](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) importados para o Configuration Manager para autenticar com o Azure AD.
- **Certificado do serviço Web** -Recomendamos que utilize um certificado de AC público ganhar confiança nativa pelos clientes. Crie o CName na entidade de registo DNS pública. Certificados de caráter universal não são suportados.
- **Certificados de raiz/SubCA carregar para CMG** -CMG o tem completa a validação da cadeia no certificados PKI de cliente. Se utilizar uma AC empresarial para emitir certificados PKI de cliente e os respetivos raiz ou AC subordinada não está disponível na internet, tem carregá-lo para o CMG.

#### <a name="deployment-process"></a>Processo de implementação

Existem duas fases para a implementação:

- Implementar o serviço em nuvem
    - Carregar o [esquema de definição de serviço do Azure](https://msdn.microsoft.com/library/azure/ee758711.aspx) ficheiro (. csdef)
    - Carregar o [esquema de configuração do serviço de Azure](https://msdn.microsoft.com/library/azure/ee758710.aspx) ficheiro (. cscfg).
- Configurar o componente CMG no seu servidor do Azure AD e os pontos finais, processadores HTTP e serviços nos serviços de informações Internet (IIS)

Se alterar a configuração de CMG, uma implementação de configuração é iniciada para o CMG.

### <a name="where-do-i-set-up-the-cloud-management-gateway"></a>Onde posso configurar o gateway de gestão da nuvem?
Pode criar o gateway de gestão de nuvem no site de nível superior da sua hierarquia. Se isto é um site de administração central, em seguida, pode criar pontos de ligação de CMG em sites primários subordinados.

### <a name="how-does-the-cloud-management-gateway-help-ensure-security"></a>Como é que o gateway de gestão de nuvem ajuda a garantir a segurança?

O CMG ajuda a garantir a segurança das seguintes formas:

- Aceita e gere ligações a partir de pontos de ligação de CMG, incluindo a autenticação de SSL mútua utilizando certificados internos e os IDs de ligação.
- Aceita e encaminha os pedidos de cliente
    - Pré-autentica ligações, utilizando SSL mútua no certificado PKI de cliente.
    - A lista de fidedignidade de certificados verifica a raiz do certificado PKI de cliente. Pode especificar esta definição no cliente comunicar as definições nas propriedades do site. Também efetua a validação do mesma como ponto de gestão para o cliente.
    - Valida URLs recebidos
    - Filtros receberam URLs para verificar se qualquer ponto de ligação CMG ligação pode processar o pedido de URL.  
    - Verifica a verificação de comprimento do conteúdo para cada ponto final de publicação.
    - Utiliza o round-robin para equilibrar entre CMG pontos de ligação do mesmo site.

- Protege o ponto de ligação CMG
    - Baseia-se consistente ligações HTTP/TCP para todas as instâncias virtuais CMG a ligação. Verifica e mantém as ligações a cada minuto.
    - Autentica mutuamente autenticação de SSL com CMG utilizando certificados internos.
    - Pedidos HTTP de reencaminhamentos com base nos mapeamentos de URL.
    - Relatórios de estado de ligação para mostrar o estado de funcionamento do serviço de administração.
    - Relatório de tráfego de ponto final de relatórios por ponto final a cada cinco minutos.

- Proteger a publicação ponto final do Configuration Manager com clientes funções, como o ponto de gestão e o software update ponto anfitrião pontos finais no IIS para servir pedidos do cliente. Cada ponto final publicado para o CMG tem um mapeamento de URL.
O URL externo for um cliente utiliza para comunicar com o CMG.
O URL interno é o ponto de ligação de CMG utilizado para reencaminhar pedidos de servidor interno.

#### <a name="example"></a>Exemplo:
Quando ativar o tráfego de CMG num ponto de gestão, o Configuration Manager cria um conjunto de mapeamentos de URL internamente para cada servidor de ponto de gestão, como ccm_system, ccm_incoming e sms_mp.
O URL externo para o ponto final ccm_system de ponto de gestão aspeto que poderá ter **https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System**.
O URL é exclusivo para cada ponto de gestão. O cliente do Configuration Manager, em seguida, PUT o CMG ativado o nome do pacote de gestão como **<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>** na respetiva lista de pontos de gestão de internet.
Todos os URLs externos publicados são carregados para o CMG automaticamente, em seguida, CMG é capaz de fazer a filtragem de URL. Todos os mapeamentos de URL é replicado para o ponto de ligação de CMG para que possa reencaminhar para servidores internos, de acordo com o cliente solicitar o URL externo.

### <a name="what-ports-are-used-by-the-cloud-management-gateway"></a>As portas que são utilizadas pelo gateway de gestão na nuvem?

- Nenhuma porta de entrada é necessária para a rede no local. Implementação de CMG criará um bunch em CMG automaticamente.
- Para além de 443, algumas portas de saída são necessários pelo ponto de ligação de CMG.

|||||
|-|-|-|-|
|Fluxo de dados|Servidor|Portas de servidor|Cliente|
|Implementação de CMG|Azure|443|Ponto de ligação de serviço do Configuration Manager|
|Criar o canal CMG|CMG|Instância VM: 1 porta: 443<br>Instância VM: N (N > = 2 e N < = 16) portas: 10124~N 10140~N|Ponto de ligação de CMG|
|Cliente CMG|CMG|443|Cliente|
|Conector CMG à função de site (atualmente pontos de gestão e pontos de atualização de software)|Função de site|Protocolo/portas configuradas na função de site|Ponto de ligação de CMG|

### <a name="how-can-you-improve-performance-of-the-cloud-management-gateway"></a>Como pode melhorar o desempenho do gateway de gestão na nuvem?

- Se possível, configure o CMG, CMG ponto de ligação e o servidor de site do Configuration Manager na mesma região de rede para reduzir a latência.
- Atualmente, a ligação entre o cliente do Configuration Manager e o CMG não é com suporte para a região.
- Para obter elevada disponibilidade, recomendamos que, pelo menos, duas instâncias virtuais o CMG e dois pontos de ligação de CMG por site
- Pode dimensionar o CMG para suportar mais clientes ao adicionar mais instâncias VM. São com pelo balanceador de carga do Azure AD de balanceamento de carga.
- Crie mais pontos de ligação de CMG distribuir a carga entre elas. O CMG será round-robin o tráfego para os respetivos pontos de ligação CMG ligação.
- Número de cliente de suporte por instância de CMG VM é 6k na versão 1702. Quando o canal CMG está sob carga elevada, o pedido irá ainda ser processado, mas poderá demorar mais do que o normal.

### <a name="how-can-you-monitor-the-cloud-management-gateway"></a>Como pode monitorizar o gateway de gestão da nuvem?

Para resolução de problemas de implementação, utilize **CloudMgr.log** e **CMGSetup.log**.
Para resolver problemas com o estado de funcionamento do serviço, utilize **CMGService.log** e **SMS_CLOUD_PROXYCONNECTOR.log**.
Para resolver problemas com o tráfego de cliente, utilize **CMGHttpHandler.log**, **CMGService.Log**, e **SMS_CLOUD_PROXYCONNECTOR.log**.

Para obter uma lista de todos os ficheiros de registo relacionados com CMG, consulte [ficheiros de registo no Configuration Manager](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)

## <a name="next-steps"></a>Passos seguintes

[Configurar o gateway de gestão na cloud](setup-cloud-management-gateway.md)

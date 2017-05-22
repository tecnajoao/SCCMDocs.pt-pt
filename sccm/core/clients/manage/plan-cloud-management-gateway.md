---
title: "Planear o gateway de gestão da nuvem | Documentos do Microsoft"
description: 
ms.date: 05/16/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: ae60eb25383f4bd07faaa1265185a471ee79b1e9
ms.openlocfilehash: b1295891a5567e64b901c79100c2971e526dc874
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---

# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Plano para o gateway de gestão de nuvem no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Gateway de gestão de nuvem a partir na versão 1610, fornece uma forma simples de gerir clientes do Configuration Manager na Internet. O serviço em nuvem management gateway é implementado para o Microsoft Azure e requer uma subscrição do Azure. Liga-se para a infraestrutura do Configuration Manager no local com uma nova função de denominado o ponto de conector do gateway de gestão na nuvem. Assim que implementados e configurados, os clientes irão ser capazes de aceder às funções de sistema de sites no local do Configuration Manager, independentemente de se estiverem na privada interna rede ou na Internet.

Utilize a consola do Configuration Manager para implementar o serviço para o Azure, adicione a função de ponto de conector de gateway de gestão de nuvem e configurar funções de sistema de sites para permitir tráfego de gateway de gestão de nuvem. Atualmente o gateway de gestão na nuvem suporta apenas os software e de ponto de atualização ponto funções de gestão.

São necessário para autenticar computadores e encriptar comunicações entre as diferentes camadas do serviço de certificados de cliente e certificados de Secure Socket Layer (SSL). Computadores cliente, normalmente, recebem um certificado de cliente através de imposição de política de grupo. Para encriptar o tráfego entre clientes e que aloja as funções de servidor do sistema de sites, terá de criar um certificado SSL personalizado a partir da AC. Também tem de configurar um certificado de gestão no Azure que permite ao Configuration Manager para implementar o serviço de gateway de gestão de nuvem.

## <a name="requirements-for-cloud-management-gateway"></a>Requisitos para o gateway de gestão da nuvem

-   Computadores cliente e o servidor de sistema de sites com o ponto de conector do gateway de gestão na nuvem.

-   Certificados SSL personalizados a partir da AC interna - utilizado para encriptar a comunicação a partir de computadores cliente e autenticar a identidade do serviço de gateway de gestão de nuvem.

-   Subscrição do Azure para serviços em nuvem.

-   Certificado de gestão do Azure – utilizado para autenticar o Configuration Manager com o Azure.

## <a name="specifications-for-cloud-management-gateway"></a>Especificações para o gateway de gestão da nuvem

- Cada instância do gateway de gestão na nuvem suporta 4.000 clientes.
- Recomendamos que crie, pelo menos, duas instâncias do gateway de gestão da nuvem para melhorar a disponibilidade.
- Gateway de gestão na nuvem suporta apenas os software e de ponto de atualização ponto funções de gestão.
-   As seguintes funcionalidades no Configuration Manager não são atualmente suportadas para o gateway de gestão da nuvem:

    -   Implementação de clientes
    -   Atribuição automática de site
    -   Políticas de utilizador
    -   Catálogo de aplicações (incluindo pedidos de aprovação de software)
    -   Implementação de todo o sistema operativo (OSD)
    -   Consola do Configuration Manager
    -   Ferramentas remotas
    -   Relatórios Web site
    -   Reativação por LAN
    -   Clientes Mac, Linux e UNIX
    -   Gestor de recursos do Azure
    -   Cache ponto a ponto
    -   Gestão de Dispositivos Móveis no Local

## <a name="cost-of-cloud-management-gateway"></a>Custo do gateway de gestão da nuvem

>[!IMPORTANT]
>As informações de custo fornecidas abaixo destina-se apenas a efeitos a estimar. O ambiente pode ter outras variáveis que afetam o custo geral da utilização do gateway de gestão da nuvem.

Gateway de gestão da nuvem utiliza a seguinte funcionalidade Microsoft Azure, o que implica encargos para a conta de subscrição do Azure:

-   Máquina virtual

    -   Gateway de gestão de nuvem atualmente requer uma norma\_máquina virtual de A2. Ao criar o serviço, pode selecionar quantos VMs para suportar o serviço (um é a predefinição).

    -   Para estimar apenas a efeitos, esperar que uma única Azure padrão\_máquina virtual de A2 pode suportar aproximadamente 2.000 simultâneos baseado na Internet clientes.

    -   Consulte o [Azure Calculadora escalão de preço](https://azure.microsoft.com/en-us/pricing/calculator/) para ajudar a determinar os custos potenciais.

      >[!NOTE]
      >Os custos de máquina virtual variam consoante a região.

-   Transferência de dados de saída

    -   Encargos são suportados com dados que fluem do serviço. Consulte o [largura de banda Azure detalhes de preço](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) para ajudar a determinar os custos potenciais.

    -   Para estimar apenas a efeitos, espere aproximadamente 100 MB por cliente por mês de clientes baseados na Internet ao executar a política atualizada a cada hora.

    >[!NOTE]
    > Realizar outras ações suportadas através do gateway de gestão da nuvem (por exemplo, a implementação de atualizações de software ou aplicações) irá aumentar a quantidade de transferência de dados de saída do Azure.

-   Armazenamento de conteúdos

    -   Os clientes baseados na Internet geridos com gateway de gestão da nuvem irão obter conteúdos de atualização de software a partir do Windows Update em nenhum gratuitas.

    -   Qualquer outro conteúdo necessário (por exemplo, aplicações) deve ser distribuído para um ponto de distribuição baseado na nuvem. Atualmente, o management gateway na nuvem suporta apenas o ponto de distribuição em nuvem para enviar conteúdo para clientes.

    - Consulte o custo de utilização um [de distribuição baseado na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution) para obter mais detalhes.

## <a name="next-steps"></a>Passos seguintes

[Configurar o gateway de gestão da nuvem](setup-cloud-management-gateway.md)


## <a name="frequently-asked-questions-about-the-cloud-management-gateway-cmg"></a>Perguntas mais frequentes sobre o Gateway de gestão de nuvem (CMG)

### <a name="why-use-the-cloud-management-gateway"></a>Porquê utilizar o gateway de gestão da nuvem?

Utilize esta função para simplificar a gestão de clientes baseada na Internet em três passos a partir da consola do Configuration Manager.

1. Implementar o CMG Azure com o [criar nuvem Management Gateway](/sccm/core/clients/manage/setup-cloud-management-gateway) assistente.
2. Configurar o [ponto de ligação de gateway de gestão da nuvem](/sccm/core/servers/deploy/configure/install-site-system-roles) função do sistema de sites.
3. [Configurar funções para o tráfego de gateway de gestão de nuvem](/sccm/core/clients/manage/setup-cloud-management-gateway#step-7-configure-roles-for-cloud-management-gateway-traffic), como o ponto de gestão e atualização de software ponto.

### <a name="how-does-the-cloud-management-gateway-work"></a>Como funciona o gateway de gestão da nuvem?

- O ponto de ligação do gateway de gestão na nuvem permite uma ligação de consistente e elevado desempenho a partir da Internet para o gateway de gestão da nuvem.
- O Configuration Manager publica definições CMG incluindo as definições de segurança e informações de ligação.
- O CMG autentica e reencaminha pedidos de cliente do Configuration Manager para o ponto de ligação do gateway de gestão na nuvem. Estes pedidos são reencaminhados para funções na rede empresarial, de acordo com os mapeamentos de URL.

### <a name="how-is-the-cloud-management-gateway-deployed"></a>Como é implementado o gateway de gestão da nuvem?

O componente do Gestor de serviço em nuvem no ponto de ligação de serviço processa todas as tarefas de implementação de CMG. Além disso, monitoriza e os relatórios de informações de estado de funcionamento e o registo do serviço do Azure AD.

#### <a name="certificate-requirements"></a>Requisitos de certificados

Terá de seguir os seguintes certificados para proteger o CMG:

- **Certificado de gestão** -Isto pode ser qualquer certificado, incluindo certificados autoassinados. Pode utilizar um certificado público carregado para o Azure AD ou uma [PFX com a chave privada](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) importados para o Configuration Manager para autenticar com o Azure AD. 
- **Certificado do serviço Web** -Recomendamos que utilize um certificado de AC pública para ganhar confiança nativa pelos clientes. O CName tem de ser criadas no público registar DNS. Certificados universais não são suportados.
- **Certificados de raiz/SubCA carregar para CMG** -CMG o tem de efetuar a validação da cadeia no certificados PKI de cliente completo. Se utilizar uma AC empresarial para emitir os certificados PKI de cliente e os respetivos raiz ou a AC subordinada não está disponível na internet, tem carregá-lo para o CMG.

#### <a name="deployment-process"></a>Processo de implementação

Existem duas fases para a implementação:

- Implementar o serviço de nuvem
    - Carregar o [esquema de definição de serviço do Azure](https://msdn.microsoft.com/library/azure/ee758711.aspx) ficheiro (csdef)
    - Carregar o [esquema de configuração do serviço Azure](https://msdn.microsoft.com/library/azure/ee758710.aspx) ficheiro (. cscfg).
- Configurar o componente CMG no servidor do Azure AD e configure os pontos finais, processadores de HTTP e serviços nos serviços de informação Internet (IIS)

Se alterar a configuração de CMG, uma implementação de configuração é iniciada para o CMG.

### <a name="how-does-the-cloud-management-gateway-help-ensure-security"></a>Como é que o gateway de gestão da nuvem ajudar a garantir a segurança?

O CMG ajuda a garantir a segurança das seguintes formas:

- Aceitar e gere ligações a partir de pontos de ligação de CMG incluindo autenticação mútua do SSL através de certificados internos e IDs de ligação.
- Aceitar e reencaminha pedidos de cliente
    - Pré-autentica ligações através de SSL mútua do certificado PKI de cliente.
    - A lista fidedigna de certificados verifica a raiz do certificado PKI de cliente. Pode especificar esta definição no cliente do comunicar definições nas propriedades do site. Também efetua a mesma validação como ponto de gestão para o cliente.
    - Valida URLs recebidos
    - Filtros recebido URLs para verificar se qualquer ponto de ligação CMG ligação pode processar o pedido de URL.  
    - Verifica a verificação de comprimento do conteúdo para cada ponto final de publicação.
    - Utiliza 'round robin' para carregar o equilíbrio entre CMG pontos de ligação do mesmo site.

- Além de proteger o ponto de ligação CMG
    - Baseia-se das ligações HTTP/TCP consistentes para todas as instâncias virtuais do CMG a ligação. Verifica e mantém ligações cada minuto.
    - Mutuamente autheticates autenticação de SSL com CMG utilizando certificados internos.
    - Pedidos HTTP de reencaminhamentos baseiem mapeamentos de URL.
    - Relatórios de estado da ligação para mostrar o estado de funcionamento do serviço de administração.
    - Relatório de tráfego de ponto final de relatórios por ponto final de cada 5 minutos.

- Protege o cliente do Configuration Manager endpoint publicação opostas funções, como o ponto de gestão e o software atualização ponto anfitrião pontos finais no IIS para pedidos de cliente do serviço. Cada ponto final publicado a CMG tem um mapeamento de URL.
O URL externo é o cliente utiliza para comunicar com o CMG.
O URL interno é o ponto de ligação de CMG utilizado para reencaminhar pedidos para o servidor interno. 

#### <a name="example"></a>Exemplo:
Quando ativar o tráfego CMG num ponto de gestão, o Configuration Manager cria um conjunto de mapeamentos de URL internamente para cada servidor de ponto de gestão, como ccm_system, ccm_incoming e sms_mp.
O URL externo para o ponto final ccm_system de ponto de gestão poderá ser semelhante **https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System**. O URL é exclusivo para cada ponto de gestão. O cliente do Configuration Manager, em seguida, coloca o CMG ativada nome MP como ** <CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID> ** na respetiva lista de pontos de gestão de internet. Todos os URLs externos publicados são carregados automaticamente para o CMG, em seguida, CMG é capaz de fazer a filtragem do URL. Todos os mapeamentos de URL replicam para o ponto de ligação CMG, de modo que pode reencaminhar para servidores internos de acordo com o cliente solicitar externa do URL.

### <a name="what-ports-are-used-by-the-cloud-management-gateway"></a>Quais as portas são utilizadas pelo management gateway na nuvem? 

- Não existem portas de entrada necessárias na rede local. Implementação de CMG criará um bunch em CMG automaticamente. 
- Para além de 443, são necessários alguns portas saídas pelo ponto de ligação de CMG.

|||||
|-|-|-|-|
|Fluxo de dados|Servidor|Portas de servidor|Cliente|
|Implementação de CMG|Azure|443|Ponto de ligação de serviço do Configuration Manager|
|Criar canal CMG|CMG|Instância VM: 1 porta: 443<br>Instância VM: N (N > = 2 e N < = 16) portas: 10124 ~ N 10140 ~ N|Ponto de ligação de CMG|
|Cliente CMG|CMG|443|Cliente|
|Conector CMG à função de site (atualmente pontos de gestão e pontos de atualização de software)|Função de site|Protocolo/portas configuradas na função do site|Ponto de ligação CMG|

### <a name="how-can-you-improve-performance-of-the-cloud-management-gateway"></a>Como melhorar o desempenho do gateway de gestão na nuvem?

- Se possível, configure o CMG, ponto de ligação CMG e o servidor do site do Configuration Manager na mesma região para reduzir a latência de rede.
- Atualmente, a ligação entre o cliente do Configuration Manager e o CMG não está ciente de região.
- Para obter a elevada disponibilidade, recomendamos que, pelo menos, 2 instâncias virtuais do CMG e dois pontos de ligação de CMG por site 
- Pode ampliar CMG para suportar mais clientes ao adicionar mais instâncias VM. São com pelo balanceador de carga do Azure AD de balanceamento de carga.
- Crie mais pontos de ligação de CMG distribuam carga entre elas. O CMG irá 'round robin' o tráfego aos pontos de ligação de CMG ligação.
- Número de cliente de suporte por instância de CMG VM é 6k na versão 1702. Quando o canal CMG é em caso de carga elevado, o pedido ainda ser processado, mas poderá demorar mais do que normal.

### <a name="how-can-you-monitor-the-cloud-management-gateway"></a>Como é que pode monitorizar o gateway de gestão da nuvem?

Para resolução de problemas de implementação, utilize **Cloudmgr** e **CMGSetup.log**.
Para resolver problemas de funcionamento do serviço, utilize **CMGService.log** e **SMS_CLOUD_PROXYCONNECTOR.log**.
Para resolução de problemas de tráfego de cliente, utilize **CMGHttpHandler.log**, **CMGService.Log**, e **SMS_CLOUD_PROXYCONNECTOR.log**.

Para obter uma lista de todos os ficheiros de registo relacionadas com a CMG, consulte o artigo [ficheiros de registo no Configuration Manager](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)



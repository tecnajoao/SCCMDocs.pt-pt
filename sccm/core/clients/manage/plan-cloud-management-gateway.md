---
title: Planejar para o gateway de gerenciamento de nuvem | Microsoft Docs
description: 
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: c6ee0ed635ab81b5e454e3cd85637ff3e20dbb34
ms.openlocfilehash: a7380ae781447880ffcba0778694ea62e10c4889
ms.contentlocale: pt-pt
ms.lasthandoff: 06/08/2017

---

# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Plano para o gateway de gerenciamento de nuvem no Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Começando na versão 1610, o gateway de gerenciamento de nuvem fornece uma maneira simple de gerenciar clientes do Configuration Manager na Internet. O serviço de gateway de gerenciamento de nuvem é implantado no Microsoft Azure e requer uma assinatura do Azure. Ele se conecta à sua infraestrutura do Configuration Manager local usando uma nova função chamada o ponto de conector de gateway de gerenciamento de nuvem. Depois de implantado e configurado, os clientes poderão acessar o local do Configuration Manager site funções do sistema, independentemente de eles estarem em interno privado rede ou na Internet.

> [!TIP]  
> Introduzida com a versão 1610, o gateway de gerenciamento de nuvem é um recurso de pré-lançamento. Para habilitá-lo, consulte [usar recursos de pré-lançamento de atualizações](/sccm/core/servers/manage/pre-release-features).

Use o console do Configuration Manager para implantar o serviço do Azure, adicione a função do ponto de conector do gateway de gerenciamento de nuvem e configurar funções de sistema de site para permitir o tráfego de gateway de gerenciamento de nuvem. Gateway de gerenciamento de nuvem atualmente suporta apenas as ponto e software update point funções de gerenciamento.

Certificados de cliente e certificados de Secure Socket Layer (SSL) são necessários para autenticar computadores e criptografar as comunicações entre as diferentes camadas do serviço. Normalmente, os computadores cliente recebem um certificado de cliente por meio da imposição de política de grupo. Para criptografar o tráfego entre clientes e servidor de sistema de site hospeda as funções, você precisa criar um certificado SSL personalizado da autoridade de certificação. Você também precisa configurar um certificado de gerenciamento no Azure que permite que o Configuration Manager para implantar o serviço de gateway de gerenciamento de nuvem.

## <a name="requirements-for-cloud-management-gateway"></a>Requisitos do gateway de gerenciamento de nuvem

-   Computadores cliente e o servidor de sistema de site que executa o ponto de conector de gateway de gerenciamento de nuvem.

-   Certificados SSL personalizados da autoridade de certificação interna - usado para criptografar a comunicação de computadores cliente e autenticar a identidade do serviço de gateway de gerenciamento de nuvem.

-   Assinatura do Azure para serviços de nuvem.

-   Certificado de gerenciamento do Azure - usado para autenticar o Configuration Manager com o Azure.

## <a name="specifications-for-cloud-management-gateway"></a>Especificações do gateway de gerenciamento de nuvem

- Cada instância do gateway de gerenciamento de nuvem oferece suporte a 4.000 clientes.
- É recomendável que você crie pelo menos duas instâncias de gateway de gerenciamento de nuvem para melhorar a disponibilidade.
- Gateway de gerenciamento de nuvem só oferece suporte a funções do ponto de atualização de gerenciamento ponto e software.
-   Os seguintes recursos no Configuration Manager estão atualmente não há suportados para o gateway de gerenciamento de nuvem:

    -   Implementação de clientes
    -   Atribuição automática de site
    -   Políticas de usuário
    -   Catálogo de aplicativos (incluindo solicitações de aprovação de software)
    -   Implantação completa do sistema operacional (OSD)
    -   Consola do Configuration Manager
    -   Ferramentas remotas
    -   Site de relatórios
    -   Reativação por LAN
    -   Clientes Mac, Linux e UNIX
    -   Gerenciador de recursos do Azure
    -   Cache de mesmo nível
    -   Gestão de Dispositivos Móveis no Local

## <a name="cost-of-cloud-management-gateway"></a>Custo de gateway de gerenciamento de nuvem

>[!IMPORTANT]
>As informações de custo fornecidas abaixo são para calcular a apenas para fins. Seu ambiente pode ter outras variáveis que afetam o custo geral do uso de gateway de gerenciamento de nuvem.

Gateway de gerenciamento de nuvem usa a seguinte funcionalidade do Microsoft Azure, que resulta em encargos para a conta de assinatura do Azure:

-   Máquina virtual

    -   Gateway de gerenciamento de nuvem atualmente requer um padrão\_A2 VM. Ao criar o serviço, você pode selecionar quantas máquinas virtuais para o suporte para o serviço (um é o padrão).

    -   Para calcular a apenas para fins de esperar que um único padrão do Azure\_A2 VM pode oferecer suporte a aproximadamente 2.000 baseado na Internet clientes simultâneos.

    -   Consulte o [Calculadora de preços do Azure](https://azure.microsoft.com/en-us/pricing/calculator/) para ajudar a determinar os custos potenciais.

      >[!NOTE]
      >Custos de máquina virtual variam por região.

-   Transferência de dados de saída

    -   As cobranças incorrem para dados que fluem do serviço. Consulte o [largura de banda do Azure, detalhes de preços](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) para ajudar a determinar os custos potenciais.

    -   Para calcular a apenas para fins, Espere aproximadamente 100 MB por cliente por mês para clientes baseados na Internet, fazer atualizações de política a cada hora.

    >[!NOTE]
    > Executar outras ações com suporte por meio do gateway de gerenciamento de nuvem (por exemplo, implantar atualizações de software ou aplicativos) aumenta a quantidade de transferência de dados de saída do Azure.

-   Armazenamento de conteúdo

    -   Clientes baseados na Internet gerenciados com o gateway de gerenciamento de nuvem obterá o conteúdo de atualização de software do Windows Update sem custo adicional.

    -   Qualquer outro conteúdo necessário (por exemplo, aplicativos) deve ser distribuído para um ponto de distribuição baseado em nuvem. Atualmente, o gateway de gerenciamento de nuvem oferece suporte a apenas o ponto de distribuição de nuvem para enviar conteúdo para clientes.

    - Consulte o custo de usar um [distribuição com base em nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution) para obter mais detalhes.

## <a name="frequently-asked-questions-about-the-cloud-management-gateway-cmg"></a>Perguntas frequentes sobre o Gateway de gerenciamento de nuvem (CMG)

### <a name="why-use-the-cloud-management-gateway"></a>Por que usar o gateway de gerenciamento de nuvem?

Use esta função para simplificar o gerenciamento de clientes baseados na Internet em três etapas do console do Configuration Manager.

1. Implantar o CMG no Azure usando o [criar Gateway de gerenciamento de nuvem](/sccm/core/clients/manage/setup-cloud-management-gateway) assistente.
2. Configurar o [ponto de conexão de gateway de gerenciamento de nuvem](/sccm/core/servers/deploy/configure/install-site-system-roles) função do sistema de site.
3. [Configurar funções para o tráfego de gateway de gerenciamento de nuvem](/sccm/core/clients/manage/setup-cloud-management-gateway#step-7-configure-roles-for-cloud-management-gateway-traffic), como o ponto de gerenciamento e o software de ponto de atualização.

### <a name="how-does-the-cloud-management-gateway-work"></a>Como funciona o gateway de gerenciamento de nuvem?

- O ponto de conexão de gateway de gerenciamento de nuvem permite que uma conexão da Internet em consistente e de alto desempenho para o gateway de gerenciamento de nuvem.
- Configuration Manager publica as configurações para o CMG incluindo as configurações de segurança e informações de conexão.
- O CMG autentica e encaminha as solicitações de cliente do Configuration Manager para o ponto de conexão de gateway de gerenciamento de nuvem. Essas solicitações são encaminhadas para funções na rede corporativa de acordo com os mapeamentos de URL.

### <a name="how-is-the-cloud-management-gateway-deployed"></a>Como o gateway de gerenciamento de nuvem é implantado?

O componente de Gerenciador de serviço de nuvem no ponto de conexão de serviço lida com todas as tarefas de implantação CMG. Além disso, ele monitora e relata informações de integridade e o log de serviço do AD do Azure.

#### <a name="certificate-requirements"></a>Requisitos de certificados

Você precisará dos seguintes certificados para proteger o CMG:

- **Certificado de gerenciamento** -isso pode ser qualquer certificado, incluindo certificados autoassinados. Você pode usar um certificado público carregado para o Azure AD ou um [PFX com chave privada](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) importados para o Configuration Manager para autenticar com o AD do Azure.
- **Certificado de serviço Web** -é recomendável que você usar um certificado de autoridade de certificação pública para ganhar confiança nativo pelos clientes. O CName precisa ser criado na registar DNS público. Não há suporte para certificados de caractere curinga.
- **Carregar certificados de raiz/SubCA CMG** -CMG o precisa completo a validação da cadeia de certificados de PKI do cliente. Se você usar uma autoridade de certificação corporativa para emitir certificados PKI de cliente e sua raiz ou autoridade de certificação subordinada não está disponível na internet, em seguida, você deve carregá-lo a CMG.

#### <a name="deployment-process"></a>Processo de implantação

Há duas fases de implantação:

- Implantar o serviço de nuvem
    - Carregue seu [esquema de definição de serviço do Azure](https://msdn.microsoft.com/library/azure/ee758711.aspx) arquivo (csdef)
    - Carregue seu [esquema de configuração de serviço do Azure](https://msdn.microsoft.com/library/azure/ee758710.aspx) arquivo (cscfg).
- Configurar o componente CMG no seu servidor do AD do Azure e configurar pontos de extremidade, manipuladores HTTP e serviços nos serviços de informações da Internet (IIS)

Se você alterar a configuração do CMG, uma implantação de configuração é iniciada para o CMG.

### <a name="how-does-the-cloud-management-gateway-help-ensure-security"></a>Como o gateway de gerenciamento de nuvem ajuda a garantir a segurança?

O CMG ajuda a garantir a segurança das seguintes maneiras:

- Aceita e gerencia conexões de pontos de conexão CMG incluindo autenticação mútua de SSL usando certificados internos e IDs de conexão.
- Aceita e encaminha as solicitações de cliente
    - Pré-autentica as conexões usando SSL mútua no certificado PKI de cliente.
    - Lista de certificados confiáveis verifica a raiz do certificado PKI do cliente. Você pode especificar essa configuração no cliente se comunicar configurações nas propriedades do site. Também executa a mesma validação como ponto de gerenciamento para o cliente.
    - Valida URLs recebidas
    - Filtros recebeu URLs para verificar se qualquer ponto de conexão CMG conexão pode atender à solicitação de URL.  
    - Verifica a seleção de comprimento de conteúdo para cada ponto de extremidade de publicação.
    - Usa 'round-robin' para carregar o equilíbrio entre os pontos de conexão CMG do mesmo site.

- Protege o ponto de conexão CMG
    - Cria conexões de HTTP/TCP consistentes para todas as instâncias virtuais do CMG a conexão. Verifica e mantém conexões a cada minuto.
    - Mutuamente autheticates autenticação SSL com CMG usando certificados internos.
    - Encaminha HTTP solicitações com base nos mapeamentos de URL.
    - Relata o status de conexão para mostrar o status de integridade do serviço de administração.
    - Relatório de tráfego de ponto de extremidade de relatórios por ponto de extremidade a cada 5 minutos.

- Proteger o cliente do Configuration Manager endpoint publicação voltados para funções como o ponto de gerenciamento e software update ponto host pontos de extremidade no IIS para atender a solicitações de cliente. Cada ponto de extremidade publicado para o CMG tem um mapeamento de URL.
A URL externa é aquele em que o cliente usa para se comunicar com o CMG.
A URL interna é o ponto de conexão de CMG usado para encaminhar solicitações para o servidor interno.

#### <a name="example"></a>Exemplo:
Quando você habilita o tráfego CMG em um ponto de gerenciamento, o Configuration Manager cria um conjunto de mapeamentos de URL internamente para cada servidor de ponto de gerenciamento, como ccm_system, ccm_incoming e sms_mp.
A URL externa para o ponto de extremidade de ccm_system de ponto de gerenciamento pode parecer **https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System**.
A URL é exclusiva para cada ponto de gerenciamento. Em seguida, o cliente do Configuration Manager coloca o CMG habilitado o nome do pacote de gerenciamento como  **<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>**  em sua lista de pontos de gerenciamento da internet.
Todas as URLs externas publicados são carregados automaticamente para o CMG CMG é capaz de fazer a filtragem de URL. Todo o mapeamento de URL replica para o ponto de conexão CMG para que se possa encaminhar para servidores internos de acordo com a URL externa de solicitação de cliente.

### <a name="what-ports-are-used-by-the-cloud-management-gateway"></a>Quais portas são usadas pelo gateway de gerenciamento de nuvem?

- Nenhuma porta de entrada necessária na rede local. Implantação de CMG criar um grupo no CMG automaticamente.
- Além de 443, algumas portas de saída são necessários para o ponto de conexão CMG.

|||||
|-|-|-|-|
|Fluxo de dados|Servidor|Portas do servidor|Cliente|
|Implantação de CMG|Azure|443|Ponto de conexão de serviço do Configuration Manager|
|Criar o canal CMG|CMG|Instância VM: 1 porta: 443<br>Instância VM: N (N > = 2 e N < = 16) portas: 10124 ~ N 10140 ~ N|Ponto de Conexão CMG|
|Cliente CMG|CMG|443|Cliente|
|Conector CMG a função de site (pontos de gerenciamento no momento e pontos de atualização de software)|Função do site|Protocolo/portas configuradas na função do site|Ponto de conexão CMG|

### <a name="how-can-you-improve-performance-of-the-cloud-management-gateway"></a>Como você pode melhorar o desempenho do gateway de gerenciamento de nuvem?

- Se possível, configure o CMG, ponto de conexão CMG e o servidor de site do Configuration Manager na mesma região para reduzir a latência de rede.
- No momento, a conexão entre o cliente do Configuration Manager e o CMG não está ciente de região.
- Para obter alta disponibilidade, recomendamos pelo menos 2 instâncias virtuais do CMG e dois pontos de conexão CMG por site
- Você pode dimensionar o CMG para dar suporte a mais clientes adicionando mais instâncias VM. Eles têm a carga balanceada pelo Balanceador de carga do AD do Azure.
- Crie mais pontos de conexão CMG para distribuir a carga entre eles. O CMG será 'round-robin' o tráfego para os pontos de conexão CMG conexão.
- Número de cliente de suporte por instância CMG VM é 6k na versão 1702. Quando o canal CMG está sob carga alta, a solicitação ainda será tratada, mas pode levar mais tempo do que o normal.

### <a name="how-can-you-monitor-the-cloud-management-gateway"></a>Como você pode monitorar o gateway de gerenciamento de nuvem?

Para solucionar problemas de implantação, use **CloudMgr.log** e **CMGSetup.log**.
Para solucionar problemas de integridade do serviço, use **CMGService.log** e **SMS_CLOUD_PROXYCONNECTOR.log**.
Para solucionar problemas de tráfego do cliente, use **CMGHttpHandler.log**, **CMGService.Log**, e **SMS_CLOUD_PROXYCONNECTOR.log**.

Para obter uma lista de todos os arquivos de log relacionadas ao CMG, consulte [arquivos de Log no Configuration Manager](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)

## <a name="next-steps"></a>Passos seguintes

[Configurar o gateway de gestão na cloud](setup-cloud-management-gateway.md)


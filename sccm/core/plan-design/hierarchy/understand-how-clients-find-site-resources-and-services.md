---
title: Encontre recursos de site
titleSuffix: Configuration Manager
description: Saiba como e quando os clientes do System Center Configuration Manager utilizam a localização de serviço para localizar os recursos de site.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9cf206bfb0774ee1d45c70e2a0c890a2f157ad65
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127189"
---
# <a name="learn-how-clients-find-site-resources-and-services-for-system-center-configuration-manager"></a>Saiba como os clientes localizam os recursos de site e os serviços do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Clientes do System Center Configuration Manager utilizam um processo chamado *localização do serviço* para localizar o sistema de sites, servidores com que possam comunicar e que fornecem serviços que os clientes são direcionados para utilizar. Noções básicas sobre como e quando os clientes utilizam a localização de serviço para localizar os recursos de site pode ajudá-lo a configurar os sites para suportar tarefas de cliente com êxito. Estas configurações podem exigir que o site interaja com configurações de domínio e de rede, como serviços de domínio do Active Directory (AD DS) e DNS. Ou pode necessitam que configure alternativas mais complexas.  

 Exemplos de funções de sistema de sites que fornecem serviços incluem:

 - O principal servidor sistema de sites para clientes.
 - O ponto de gestão.
 - Servidores de sistema de sites adicionais que o cliente pode comunicar com, como pontos de atualização de software e de pontos de distribuição.  



##  <a name="bkmk_fund"></a> Fundamentals of service location  
 Um cliente avalia a respetiva localização de rede atual, preferência de protocolo de comunicação e site atribuído quando está a utilizar a localização do serviço para localizar um ponto de gestão que este possa comunicar com.  

 **Um cliente comunica com um ponto de gestão para:**  
-   Transferir informações sobre outros pontos de gestão para o site, para que possa criar uma lista de pontos de gestão conhecidos (conhecida como a *lista MP*) para os ciclos de localização de serviço futuras.  
-   Carregar detalhes de configuração, como inventário e estado.  
-   Transferir uma política que define as configurações no cliente e pode informar o cliente de software que pode ou tem de instalar e outras tarefas relacionadas.  
-   Pedido de informações adicionais sobre de sites de funções de sistema que fornecem serviços que o cliente tiver sido configurado para utilizar. Os exemplos incluem pontos de distribuição de software que pode instalar o cliente ou do ponto de atualização de software da qual obter atualizações.  

**Um cliente do Configuration Manager faz um pedido de localização de serviço:**  
-   Cada 25 horas de operação contínua.  
-   Quando o cliente Deteta uma alteração na sua configuração de rede ou localização.  
-   Quando o **ccmexec.exe** serviço no computador (o serviço de cliente do principal) é iniciado.  
-   Quando o cliente tem de localizar uma função de sistema de sites que fornece um serviço necessário.  

**Quando um cliente está a tentar localizar os servidores que alojam funções do sistema de sites**, ele usa a localização de serviço para localizar uma função de sistema de sites que suporta o protocolo do cliente (HTTP ou HTTPS). Por predefinição, os clientes utilizam o método mais seguro disponível para eles. Tenha em consideração o seguinte:  

-   Para utilizar HTTPS, tem de ter uma infraestrutura de chaves públicas (PKI) e instalar certificados PKI nos clientes e servidores. Para obter mais informações sobre o certificado PKI, veja [Requisitos de Certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

-   Ao implementar uma função do sistema de sites que utiliza Serviços de Informação Internet (IIS) e suporta comunicações de clientes, tem de especificar se os clientes ligam ao sistema de sites através de HTTP ou HTTPS. Se utilizar HTTP, também tem de considerar as opções de assinatura e encriptação. Para obter mais informações, consulte [planear a assinatura e encriptação](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) no [planear a segurança no System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md).  

##  <a name="BKMK_Plan_Service_Location"></a> Localização do serviço e como os clientes determinam o seu ponto de gestão atribuído  
Quando um cliente é atribuído pela primeira vez a um site primário, seleciona um ponto de gestão predefinido para esse site. Os sites primários suportam vários pontos de gestão, e cada cliente identifica de forma independente um ponto de gestão como ponto de gestão predefinido. Este ponto de gestão predefinido torna-se, em seguida, o ponto de gestão atribuído desse cliente. (Também pode utilizar os comandos de instalação de cliente para definir o ponto de gestão atribuído para um cliente quando é instalado.)  

Um cliente seleciona um ponto de gestão para comunicar com base nas atuais localização e o limite de grupo configurações de rede do cliente. Muito embora tenha um ponto de gestão atribuído, este pode não ser o ponto de gestão que o cliente utiliza.  

   > [!NOTE]  
   >  Um cliente utiliza sempre o ponto de gestão atribuído para mensagens de registo e determinadas mensagens de política, mesmo quando são enviadas outras comunicações para um ponto de gestão local ou de proxy.

Pode utilizar pontos de gestão preferenciais. Pontos de gestão preferenciais são pontos de gestão do site atribuído de um cliente que estão associados um grupo de limites que o cliente está a utilizar para localizar servidores do sistema de sites. Associação de um ponto de gestão preferenciais com um limite de grupo como um servidor de sistema de sites é semelhante a como pontos de distribuição ou pontos de migração de estado estão associados um grupo de limites. Se ativar pontos de gestão preferenciais para a hierarquia, quando um cliente utilizar um ponto de gestão a partir do site atribuído, este tentará utilizar um ponto de gestão preferencial antes de utilizar outros pontos de gestão a partir do site atribuído.  

Também pode utilizar as informações a [afinidade do ponto de gestão](http://blogs.technet.com/b/jchalfant/archive/2014/09/22/management-point-affinity-added-in-configmgr-2012-r2-cu3.aspx) blog em TechNet.com para configurar a afinidade do ponto de gestão. Substituições de afinidade de ponto de gestão o comportamento predefinido de gestão atribuído aponta e permite que o cliente utilizam um ou mais pontos de gestão específico.  

Sempre que precisa de contactar um ponto de gestão, o cliente verifica a lista MP, que armazena localmente no Windows Management Instrumentation (WMI). O cliente cria uma lista MP inicial quando é instalado. O cliente, em seguida, atualiza periodicamente a lista com detalhes sobre cada ponto de gestão na hierarquia.  

Quando o cliente não é possível localizar um ponto de gestão válido na respetiva lista MP, as seguintes origens de localização de serviço, este procura por ordem, até encontrar um ponto de gestão que pode utilizar:  

1.  Ponto de gestão  
2.  AD DS  
3.  DNS  
4.  WINS  

Depois de um cliente localiza e contacta um ponto de gestão com êxito, transfere a lista atual de pontos de gestão que estão disponíveis na hierarquia e atualiza a lista MP local. O mesmo aplica-se a clientes com um domínio associado e aos que não têm.  

Por exemplo, quando um cliente de Configuration Manager que está na Internet liga a um ponto de gestão baseado na Internet, o ponto de gestão envia esse cliente uma lista de pontos de gestão baseado na Internet disponíveis no site. Do mesmo modo, os clientes com um domínio associado ou em grupos de trabalho também recebem uma lista dos pontos de utilização que podem utilizar.  

Um cliente que não está configurado para a Internet não é fornecido a pontos de gestão com acesso à-apenas na Internet. Os clientes de grupo de trabalho configurados para a Internet comunicam apenas com pontos de gestão de acesso à Internet.  

##  <a name="BKMK_MPList"></a> A lista MP  
A lista MP é a origem de localização de serviço preferencial para um cliente, porque se trata de uma lista prioritária de pontos de gestão que o cliente identificou anteriormente. Esta lista é ordenada por cada cliente com base na respetiva localização de rede quando o cliente atualiza a lista e, em seguida, é armazenada localmente no cliente no WMI.  

### <a name="building-the-initial-mp-list"></a>Criar a lista MP inicial  
Durante a instalação do cliente, as seguintes regras são utilizadas para criar a lista de pacote de gestão inicial do cliente:  

-   A lista inicial inclui pontos de gestão especificados durante a instalação de cliente (ao utilizar o **SMSMP**= ou **/MP** opção).  
-   O cliente consulta o AD DS para pontos de gestão publicados. Para ser identificado no AD DS, o ponto de gestão tem de ser do site atribuído do cliente, e tem de ser a mesma versão de produto que o cliente.  
-   Se nenhum ponto de gestão foi especificado durante a instalação de cliente e o esquema do Active Directory não estiver expandido, o cliente verifica DNS e WINS para pontos de gestão publicados.  
-   Quando o cliente cria a lista inicial, informações sobre alguns pontos de gestão na hierarquia poderão não ser conhecidas.  

### <a name="organizing-the-mp-list"></a>Organizar a lista MP  
Os clientes organizam a sua lista de pontos de gestão, utilizando as seguintes classificações:  

-   **Proxy**: Um ponto de gestão num site secundário.  
-   **Local**: Qualquer ponto de gestão que esteja associado à localização de rede atual do cliente, como definido pelos limites do site. Tenha em atenção as seguintes informações sobre limites:
    -   Quando um cliente pertence a mais de um grupo de limites, a lista de pontos de gestão locais é determinada a partir da união de todos os limites que incluem a localização de rede atual do cliente.  
    -   Pontos de gestão local, normalmente, são um subconjunto de um cliente atribuído pontos de gestão, a menos que o cliente está num local de rede que está associado a outro site com pontos de gestão que fazem a manutenção de seus grupos de limites.   


-   **Atribuído**: Qualquer ponto de gestão ou seja um sistema de site para site atribuído do cliente.  

Pode utilizar pontos de gestão preferenciais. Pontos de gestão num site que não estão associadas um grupo de limites ou que não estão num grupo de limites associado à localização de rede atual do cliente, não são considerados preferenciais. Que serão utilizados quando o cliente não é possível identificar um ponto de gestão preferencial disponível.  

### <a name="selecting-a-management-point-to-use"></a>Selecionar um ponto de gestão a utilizar  
Em comunicações típicas, um cliente tenta utilizar uma utilização de um ponto de gestão a partir das classificações pela seguinte ordem, com base na localização de rede do cliente:  

1.  Proxy  
2.  Localização  
3.  Atribuídos  

No entanto, o cliente utiliza sempre o ponto de gestão atribuído para o registo de mensagens e determinadas políticas de mensagens, mesmo quando são enviadas outras comunicações para um ponto de gestão local ou de um proxy.  

Em cada classificação (proxy, local ou atribuída), o cliente tenta utilizar um ponto de gestão com base nas preferências, pela seguinte ordem:  

1.  Compatível com HTTPS numa floresta local ou fidedigna (quando o cliente está configurado para comunicação HTTPS)  
2.  Não compatível com do HTTPS numa floresta local ou fidedigna (quando o cliente está configurado para comunicação HTTPS)  
3.  Compatível com HTTP numa floresta local ou fidedigna  
4.  Compatível com HTTP não numa floresta local ou fidedigna  

Do conjunto de pontos de gestão ordenados por preferências, o cliente tenta utilizar o primeiro ponto de gestão na lista. Esta lista ordenada de pontos de gestão é aleatória e não pode ser ordenada. A ordem da lista pode mudar sempre que o cliente atualizar a respetiva lista MP.  

Quando um cliente não consegue estabelecer contacto com o primeiro ponto de gestão, tentará cada ponto de gestão na respetiva lista. Tentará cada ponto de gestão preferencial na classificação antes de tentar os pontos de gestão não preferenciais. Se um cliente não é possível comunicar com qualquer ponto de gestão na classificação com êxito, este tenta contactar um ponto de gestão preferencial da próxima classificação e assim por diante, até encontrar um ponto de gestão a utilizar.  

Depois de um cliente estabelecer comunicação com um ponto de gestão, ele continua a utilizar o mesmo ponto de gestão até que:  

-   passaram-se a 25 horas.  
-   O cliente não consegue comunicar com o ponto de gestão para cinco tentativas durante um período de 10 minutos.

Em seguida, o cliente seleciona aleatoriamente um novo ponto de gestão a utilizar.  

##  <a name="bkmk_ad"></a> Active Directory  
Os clientes que têm um domínio associado podem utilizar o AD DS para a localização de serviços. Isto requer que os sites [publiquem dados no Active Directory](http://technet.microsoft.com/library/hh696543.aspx).  

Um cliente pode utilizar o AD DS para a localização de serviço quando todas as condições seguintes forem verdadeiras:  

-   O Active Directory [esquema tiver sido expandido](https://technet.microsoft.com/library/mt345589.aspx) ou foi expandido para o System Center 2012 Configuration Manager.  
-   O [floresta do Active Directory está configurada para publicar](http://technet.microsoft.com/library/hh696542.aspx), e sites do Configuration Manager estão configurados para publicar.  
-   O computador cliente é membro de um domínio do Active Directory e consegue aceder a um servidor de catálogo global.  

Se um cliente não é possível localizar um ponto de gestão para utilizar para a localização de serviço do AD DS, este tenta utilizar o DNS.  

##  <a name="bkmk_dns"></a> DNS  
Os clientes na intranet podem utilizar o DNS para localização de serviços. Isto requer que, pelo menos, um site numa hierarquia publique informações sobre os pontos de gestão no DNS.  

Considere a utilização do DNS para localização de serviços quando se verificar qualquer das seguintes condições:
-   Esquema do AD DS não é expandido para suportar o Configuration Manager.
-   Os clientes da intranet estão localizados numa floresta que não está ativada para publicação do Configuration Manager.  
-   Tem clientes que se encontram em computadores do grupo de trabalho, não estando configurados para gestão de clientes apenas na Internet. (Um cliente de grupo de trabalho configurado para a Internet apenas comunicarem com os pontos de gestão de acesso à Internet e não irá utilizar o DNS para localização de serviços).  
-   Pode [configurar clientes para encontrar pontos de gestão do DNS](http://technet.microsoft.com/library/gg682055).  

Quando um site publica registos de localização de serviços para pontos de gestão no DNS:  

-   A publicação é aplicável apenas a pontos de gestão que aceitem ligações de clientes a partir da Internet.  
-   A publicação adiciona um registo de recurso de localização de serviços (SRV RR) na zona DNS do computador do ponto de gestão. Tem de existir uma entrada de anfitrião correspondente no DNS desse computador.  

Por predefinição, os clientes associados a um domínio procuram o DNS para os registos de ponto de gestão de domínio local do cliente. Pode configurar uma propriedade de cliente que especifique um sufixo de domínio para um domínio que tenha informações publicadas no DNS do ponto de gestão.  

Para obter mais informações sobre como configurar a propriedade de cliente do sufixo DNS, consulte [como configurar computadores cliente para localizar pontos de gestão através de publicação de DNS no System Center Configuration Manager](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

Se um cliente não é possível localizar um ponto de gestão para utilizar para a localização de serviço do DNS, este tenta utilizar o WINS.  

### <a name="publish-management-points-to-dns"></a>Publicar pontos de gestão no DNS  
Para publicar pontos de gestão no DNS, terão de se verificar as duas condições seguintes:  

-   Os servidores de DNS suportam registos de recursos de localização de serviço, utilizando a versão 8.1.2 ou superior do BIND.  
-   Os FQDNs da intranet especificados para os pontos de gestão no Configuration Manager tem entradas de anfitrião (por exemplo, registos) no DNS.  

> [!IMPORTANT]  
>  Publicação de DNS do Configuration Manager não suporta um espaço de nomes não contíguo. Se tiver um espaço de nomes não contíguo, pode publicar pontos de gestão no DNS manualmente ou utilize um dos outros serviço localização métodos documentados nesta secção.  

**Se os servidores DNS suportarem atualizações automáticas**, pode configurar o Configuration Manager para publicar automaticamente pontos de gestão na intranet no DNS ou poderá publicar manualmente estes registos no DNS. Quando os pontos de gestão são publicados no DNS, o respetivo FQDN da intranet e número de porta são publicados no registo de localização de serviço (SRV). Configure a publicação DNS num site nas propriedades de componente do ponto de gestão do site. Para obter mais informações, consulte  [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

**Quando a zona DNS está definida como "Apenas seguro" para as atualizações dinâmicas**, apenas o primeiro ponto de gestão para publicar no DNS pode fazer com êxito com as permissões predefinidas.

Se apenas um ponto de gestão com êxito pode publicar e alterar o respetivo registo de DNS e o servidor de ponto de gestão está em bom estado, os clientes podem obter a lista de pacote de gestão completa do que gestão ponto e, em seguida, localize o respetivo ponto de gestão preferenciais.


**Se os servidores DNS não suportarem atualizações automáticas, mas suportarem registos de localização de serviço**, poderá publicar manualmente os pontos de gestão no DNS. Para tal, terá de especificar manualmente o registo de recursos de localização de serviço (SRV RR) no DNS.  

O Configuration Manager suporta RFC 2782 para registos de localização de serviço. Estes registos têm o seguinte formato: *_Service._Proto.Name TTL classe SRV prioridade importância porta destino*  

Para publicar um ponto de gestão para o Configuration Manager, especifique os seguintes valores:  

-   **_Service**: Introduza **mssms_mp**_&lt;sitecode\>, onde &lt;sitecode\> é o código do site do ponto de gestão.  
-   **._Proto**: Especifique **. TCP**.  
-   **.Name**: Introduza o sufixo DNS do ponto de gestão, por exemplo **contoso.com**.  
-   **TTL**: Introduza **14400**, que corresponde a quatro horas.  
-   **classe**: Especifique **IN** (em conformidade com RFC 1035).  
-   **Prioridade**: O Configuration Manager não utiliza este campo.
-   **Peso**: O Configuration Manager não utiliza este campo.  
-   **Porta**: Introduza o número de porta que utiliza o ponto de gestão, por exemplo **80** para HTTP e **443** para HTTPS.  

    > [!NOTE]  
    >  A porta do registo SRV deve corresponder a porta de comunicação que utiliza o ponto de gestão. Por predefinição, isto é **80** para comunicação HTTP e **443** para comunicação HTTPS.  

-   **Destino**: Introduza o FQDN especificado para o sistema de sites que está configurado com a função de site do ponto de gestão de intranet.  

Se utilizar o DNS do Windows Server, poderá utilizar o procedimento seguinte para introduzir este registo DNS para pontos de gestão da intranet. Se utilizar outra implementação para DNS, utilize as informações desta secção relativas aos valores dos campos e consulte a documentação do DNS para adaptar este procedimento.  

##### <a name="to-configure-automatic-publishing"></a>Para configurar a publicação automática:  

1.  Na consola do Configuration Manager, expanda **Administration** > **configuração do Site** > **Sites**.  

2.  Selecione o seu site e, em seguida, escolha **configurar componentes do Site**.  

3.  Escolher **ponto de gestão**.  

4.  Selecione os pontos de gestão que pretende publicar. (Esta seleção aplica-se à publicação no AD DS e DNS.)  

5.  Selecione a caixa para publicar no DNS. Esta caixa:  

    -   Permite-lhe selecionar os pontos de gestão para publicar no DNS.  

    -   Não configure a publicação no AD DS.  

##### <a name="to-manually-publish-management-points-to-dns-on-windows-server"></a>Para publicar manualmente pontos de gestão no DNS no Windows Server  

1.  Na consola do Configuration Manager, especifique os FQDNs dos sistemas de sites da intranet.  

2.  Na consola de gestão de DNS, selecione a zona DNS do computador do ponto de gestão.  

3.  Verifique se existe um registo de anfitrião (A ou AAAA) para o FQDN da intranet do sistema de sites. Se o registo não existir, crie-o.  

4.  Ao utilizar o **novos outros registos** opção, escolha **localização de serviço (SRV)** no **tipo de registo de recurso** caixa de diálogo caixa, escolha **criar registo**, introduza as seguintes informações e, em seguida, escolha **feito**:  

    -   **Domínio**: Se necessário, introduza o sufixo DNS do ponto de gestão, por exemplo **contoso.com**.  
    -   **Serviço**: Tipo **mssms_mp**_&lt;sitecode\>, onde &lt;sitecode\> é o código do site do ponto de gestão.  
    -   **Protocolo**: Type **_tcp**.  
    -   **Prioridade**: O Configuration Manager não utiliza este campo.  
    -   **Peso**: O Configuration Manager não utiliza este campo.  
    -   **Porta**: Introduza o número de porta que utiliza o ponto de gestão, por exemplo **80** para HTTP e **443** para HTTPS.  

        > [!NOTE]  
        >  A porta do registo SRV deve corresponder a porta de comunicação que utiliza o ponto de gestão. Por predefinição, isto é **80** para comunicação HTTP e **443** para comunicação HTTPS.  

    -   **Anfitrião que oferece este serviço**: Introduza o FQDN especificado para o sistema de sites que está configurado com a função de site do ponto de gestão de intranet.  

Repita estes passos para cada ponto de gestão da intranet que pretenda publicar no DNS.  

##  <a name="bkmk_wins"></a> WINS  
Se os outros mecanismos de localização de serviço falharem, os clientes poderão encontrar um ponto de gestão inicial consultando o WINS.  

Por predefinição, um site primário publica no WINS o primeiro ponto de gestão no site que está configurado para HTTP e o primeiro ponto de gestão que esteja configurado para HTTPS.  

Se não pretender que os clientes encontrem um ponto de gestão HTTP no WINS, configure-os com a propriedade CCMSetup.exe Client.msi **SMSDIRECTORYLOOKUP=NOWINS**.  

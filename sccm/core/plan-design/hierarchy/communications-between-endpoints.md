---
title: "As comunicações entre os pontos finais | Documentos do Microsoft"
description: "Saiba mais sobre como os componentes e sistemas de sites do Configuration Manager do System Center comunicarem através de uma rede."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2ac9f98dc7b455d3b72d794d4311863186ed53ef
ms.openlocfilehash: cd94f9ccc7e196b30e5dc7ae9368d073b7cff5d2
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="communications-between-endpoints-in-system-center-configuration-manager"></a>Comunicações entre pontos finais no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


##  <a name="Planning_Intra-site_Com"></a> Comunicações entre sistemas de sites num site  
 Quando os sistemas de site do Configuration Manager ou componentes comunicam através da rede para outros sistemas de sites ou componentes do Configuration Manager no site, utilizam um dos seguintes protocolos, dependendo de como configurar o site:  

-   Bloco de mensagem de servidor (SMB)  

-   HTTP  

-   HTTPS  

À exceção da comunicação do servidor do site para um ponto de distribuição, as comunicações de servidor para servidor num site podem ocorrer a qualquer hora e não utilizam mecanismos para controlar a largura de banda de rede. Uma vez que não é possível controlar a comunicação entre sistemas de sites, certifique-se de que instala servidores do sistema de sites em localizações com redes com boas ligações e rápidas.  

Para ajudar a gerir a transferência de conteúdo do servidor do site para pontos de distribuição:  

-   Configure o ponto de distribuição para o controlo da largura de banda de rede e o agendamento. Estes controlos assemelham-se as configurações que são utilizadas por endereços entre sites e, muitas vezes, pode utilizar esta configuração em vez de instalar outro site do Configuration Manager quando a transferência de conteúdo para localizações de rede remotas é a sua consideração em termos de largura de banda principal.  

-   Pode instalar um ponto de distribuição como um ponto de distribuição pré-configurado. Um ponto de distribuição pré-configurado permite-lhe utilizar o conteúdo que é manualmente colocado no servidor do ponto de distribuição e remove o requisito de transferir ficheiros de conteúdo através da rede.  

Para obter mais informações, consulte o artigo [gerir a largura de banda de rede para a gestão de conteúdo](manage-network-bandwidth.md).


##  <a name="Planning_Client_to_Site_System"></a> Comunicações de clientes para sistemas e serviços do site  
Os clientes iniciam a comunicação com funções do sistema de sites, serviços de domínio do Active Directory e os serviços online. Para ativar estas comunicações, as firewalls têm de permitir o tráfego de rede entre clientes e o ponto final das suas comunicações. Os pontos finais incluem:  

-   **Ponto de Web site do catálogo de aplicações**: Suporta comunicações HTTP e HTTPS

-   **Recursos baseados em nuvem**: Inclui o Microsoft Azure e o Microsoft Intune  

-   **Módulo de política do Configuration Manager (NDES)**: Suporta comunicações HTTP e HTTPS

-   **Pontos de distribuição**: Suporta HTTP e HTTPS e comunicação HTTPS, é necessário por pontos de distribuição baseado na nuvem  

-   **Ponto de estado de contingência**: Suporta comunicações HTTP  

-   **Ponto de gestão**: Suporta comunicações HTTP e HTTPS  

-   **Microsoft Update**  

-   **Pontos de atualização de software** : Suporta comunicações HTTP e HTTPS  

-   **Ponto de migração de estado**: Suporta comunicações HTTP e HTTPS  

-   **Vários serviços de domínio**  

Para que um cliente possa comunicar com uma função de sistema de sites, o cliente utiliza a localização de serviço para encontrar uma função de sistema de sites que suporte o protocolo do cliente (HTTP ou HTTPS). Por predefinição, os clientes utilizam o método mais seguro que esteja disponível para os mesmos:  

-   Para utilizar HTTPS, tem de ter uma infraestrutura de chaves públicas (PKI) e instalar certificados PKI nos clientes e servidores. Para obter mais informações sobre o certificado PKI, veja [Requisitos de Certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

-   Ao implementar uma função do sistema de sites que utiliza Serviços de Informação Internet (IIS) e suporta comunicações de clientes, tem de especificar se os clientes ligam ao sistema de sites através de HTTP ou HTTPS. Se utilizar HTTP, também tem de considerar as opções de assinatura e encriptação. Para obter mais informações, consulte o artigo [planear a assinatura e encriptação](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) no [planear a segurança no System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md).  

Para obter informações sobre a localização de serviços pelos clientes, veja [Compreender a forma como os clientes localizam os recursos e os serviços do site no System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

Para obter detalhes sobre portas e protocolos utilizados pelos clientes quando comunicam com estes pontos finais, consulte o artigo [portas utilizadas no System Center Configuration Manager](../../../core/plan-design/hierarchy/ports.md).  

###  <a name="BKMK_clientspan"></a> Considerações sobre comunicações do cliente a partir da Internet ou uma floresta não fidedigna  
As seguintes funções de sistema de sites instaladas nos sites primários suportam ligações de clientes que se encontram em localizações não fidedignas, como a Internet ou numa floresta não fidedigna. (Os sites secundários não suportam ligações de cliente a partir de localizações não fidedignas):  

-   Ponto de site do Catálogo de Aplicações  

-   Módulo de Política do Configuration Manager  

-   Ponto de distribuição (os pontos de distribuição baseados na nuvem precisam de HTTPS)  

-   Ponto proxy de registo  

-   Ponto de estado de contingência  

-   Ponto de gestão  

-   Ponto de atualização de Software  

**Sobre os sistemas de sites com acesso à Internet:**   
Não existe qualquer requisito de fidedignidade entre a floresta do cliente e do servidor de sistema do site. No entanto, quando a floresta que contém um sistema de sites com acesso à Internet confia na floresta que contém as contas de utilizador, esta configuração suporta políticas baseadas no utilizador para dispositivos na Internet quando ativa a **política de cliente** definição de cliente **ativar pedidos da política de utilizador dos clientes Internet**.  

Por exemplo, as configurações seguintes ilustram quando a gestão de clientes baseada na Internet suporta políticas de utilizador para dispositivos na Internet:  

-   O ponto de gestão baseado na Internet encontra-se na rede de perímetro em que reside um controlador de domínio para autenticar o utilizador e uma firewall intermediária permite pacotes do Active Directory.  

-   A conta de utilizador encontra-se na Floresta A (a intranet) e o ponto de gestão baseado na Internet encontra-se na Floresta B (a rede de perímetro). A Floresta B confia na Floresta A e uma firewall intermediária permite os pacotes de autenticação.  

-   A conta de utilizador e o ponto de gestão baseado na Internet encontram-se na Floresta A (a intranet). O ponto de gestão é publicado na Internet através de um servidor Web proxy (como o Forefront Threat Management Gateway).  

> [!NOTE]  
>  Se a autenticação Kerberos falhar, será automaticamente tentada a autenticação NTLM.  

Como mostra o exemplo anterior, é possível colocar sistemas de sites baseados na Internet na intranet quando estes forem publicados na Internet utilizando um servidor Web proxy, tal como o ISA Server ou o Forefront Threat Management Gateway. Estes sistemas de sites podem ser configurados para ligação de cliente a partir da Internet apenas, ou para ligações de cliente provenientes da Internet e intranet. Quando utiliza um servidor web proxy, pode configurá-lo para segura Sockets Layer (SSL) protocolo de bridge SSL (mais segura) ou o protocolo de túnel SSL da seguinte forma:  

-   **Protocolo de bridge SSL para SSL:**   
    A configuração recomendada quando utiliza servidores Web proxy para a gestão de clientes baseados na Internet é o protocolo de bridge SSL para SSL, que utiliza a terminação de SSL com a autenticação de SSL. Os computadores cliente têm de ser autenticados utilizando a autenticação de computador e os clientes antigos do dispositivo móvel são autenticados utilizando a autenticação de utilizador. Dispositivos móveis que são inscritos pelo Configuration Manager não suportam o protocolo de bridge SSL.  

     A vantagem da terminação de SSL no servidor Web proxy é que os pacotes da Internet são sujeitos a inspeção antes de serem encaminhados para a rede interna. O servidor Web proxy autentica a ligação do cliente, termina-a e, em seguida, abre uma nova ligação autenticada para os sistemas de sites baseados na Internet. Quando os clientes do Configuration Manager utilizam um servidor web proxy, a identidade do cliente (GUID do cliente) está contida em segurança no payload do pacote para que o ponto de gestão não considere o servidor web proxy como o cliente. Protocolo de bridge não é suportado no Configuration Manager com HTTP para HTTPS ou de HTTPS para HTTP.  

-   **Protocolo de túnel**:   
    Se o servidor web proxy não suporta os requisitos para o protocolo de bridge SSL ou se pretende configurar o suporte de Internet para dispositivos móveis inscritos pelo Configuration Manager, a utilização de túnel SSL também é suportada. É uma opção menos segura porque os pacotes SSL da Internet são encaminhados para os sistemas de sites sem a terminação de SSL, não podendo ser, assim, inspecionados quanto a conteúdo malicioso. Quando utiliza o protocolo de túnel SSL, não existem requisitos de certificado para o servidor Web proxy.  

##  <a name="Plan_Com_X-Forest"></a> Comunicação entre florestas do Active Directory  
System Center Configuration Manager suporta sites e hierarquias que abrangem florestas do Active Directory.  

O Configuration Manager também suporta computadores de domínio que não estejam na mesma floresta do Active Directory que o servidor do site e computadores que estão em grupos de trabalho:  

-   **Para suportar computadores de domínio localizados numa floresta que não seja considerada fidedigna pela floresta do servidor do site**, pode:  

    -   Instalar funções do sistema de sites nessa floresta não fidedigna, com a opção de publicar informações do site nessa floresta do Active Directory  

    -   Gerir estes computadores como se fossem computadores de grupo de trabalho.  

  Quando instala servidores do sistema de sites numa floresta do Active Directory não fidedigna, a comunicação de cliente-servidor a partir de clientes dessa floresta é mantida dentro dessa floresta e do Configuration Manager pode autenticar o computador utilizando Kerberos. Quando publicar informações do site na floresta do cliente, os clientes beneficiar das funcionalidades ao obter informações de site, tais como uma lista dos pontos de gestão disponíveis, a partir da respetiva floresta do Active Directory, em vez de transferir estas informações a partir do respetivo ponto de gestão atribuído.  

  > [!NOTE]  
  >  Para gerir os dispositivos que se encontrem na Internet, pode instalar funções de sistema de sites baseadas na Internet na sua rede de perímetro desde que os servidores do sistema de sites se encontrem numa floresta do Active Directory. Este cenário não requer uma fidedignidade bidirecional entre a rede de perímetro e a floresta do servidor de site.  

-   **Para suportar computadores num grupo de trabalho**, tem de:  

    -   Aprovar manualmente os computadores do grupo de trabalho quando utilizam ligações de cliente HTTP para as funções do sistema de sites. Isto acontece porque o Configuration Manager não pode autenticar estes computadores através de Kerberos.  

    -   Configurar a Conta de Acesso à Rede para que estes computadores possam receber conteúdos dos pontos de distribuição.  

    -   Fornecer um mecanismo alternativo para que os clientes do grupo de trabalho localizem pontos de gestão. Pode utilizar a publicação de DNS, WINS, ou pode atribuir diretamente um ponto de gestão. Isto acontece porque estes clientes não conseguem obter as informações do site dos Serviços de Domínio do Active Directory.  

    Recursos relacionados nesta biblioteca de conteúdos:  

    -   [Gerir registos em conflito para clientes do Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

    -   [Conta de acesso à rede](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

    -   [Como instalar clientes do Configuration Manager em computadores de grupo de trabalho](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

###  <a name="bkmk_span"></a> Cenários para suportar um site ou uma hierarquia que abranja vários domínios e florestas  

#### <a name="communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Comunicação entre sites numa hierarquia que abranja florestas  
Este cenário requer uma fidedignidade de floresta bidirecional que suporte a autenticação Kerberos.  Se não tem uma fidedignidade de floresta bidirecional que suporte a autenticação Kerberos, em seguida, o Configuration Manager não suporta um site subordinado na floresta remota.  

 **O Configuration Manager suporta a instalação de um site subordinado numa floresta remota que possua a fidedignidade bidirecional necessária com a floresta do site principal**  

-   Por exemplo, pode colocar um site secundário noutra floresta do respetivo site primário principal, desde que a fidedignidade necessária exista.  

> [!NOTE]  
>  Um site subordinado pode ser site primário (em que o site de administração central é o site principal) ou um site secundário.  

Comunicação entre sites no Configuration Manager utiliza a replicação de base de dados e transferências de ficheiros. Quando instala um site, tem de especificar uma conta com o qual vai instalar o site no servidor designado. Esta conta também estabelece e mantém a comunicação entre sites.  

Após o site ter sido instalado com êxito e ter iniciado transferências baseadas em ficheiros e a replicação de base de dados, não será necessária qualquer configuração adicional para a comunicação com o site.  

**Se existir uma fidedignidade de floresta bidirecional, o Configuration Manager não requer quaisquer passos de configuração adicionais.**  

Por predefinição, quando instala um novo site como subordinado de outro site, o Configuration Manager configura o seguinte:  

-   Uma rota de replicação entre sites, baseada em ficheiros em cada site que utiliza a conta do computador servidor de sites. O Configuration Manager adiciona a conta de computador de cada computador para o **SMS_SiteToSiteConnection_&lt;sitecode\>**  grupo no computador de destino.  

-   A replicação de base de dados entre o SQL Server de cada site.  

É também necessário definir as seguintes configurações:  

-   As firewalls e dispositivos de rede tem de permitir os pacotes de rede exigidos pelo Configuration Manager.  

-   A resolução de nomes tem de funcionar entre as florestas.  

-   Para instalar um site ou função do sistema de sites, terá de especificar uma conta com permissões de administrador local no computador especificado.  

#### <a name="communication-in-a-site-that-spans-forests"></a>Comunicação num site que abranja florestas  
Este cenário não requer uma fidedignidade de floresta bidirecional.  

**Os sites primários suportam a instalação de funções do sistema de sites em computadores em florestas remotas**.  

-   O ponto de serviço Web do Catálogo de Aplicações é a única exceção.  Apenas é suportado na mesma floresta do servidor do site.  

-   Se uma função do sistema de sites aceitar ligações a partir da Internet, como uma melhor prática de segurança, instale as funções do sistema de sites numa localização onde o limite da floresta forneça proteção ao servidor do site (por exemplo, numa rede de perímetro).  

**Para instalar uma função do sistema de sites num computador numa floresta não fidedigna:**  

-   Tem de especificar um **conta de instalação do sistema de sites**, que é utilizado para instalar a função de sistema de sites. (Esta conta tem de ter credenciais administrativas locais para estabelecer ligação ao.) Em seguida, instale funções do sistema de sites no computador especificado.  

-   Tem de selecionar a opção de sistema de sites **Exigir que o servidor do site inicie ligações a este sistema de sites**. Isto requer que o servidor do site estabeleça ligações ao servidor do sistema de sites para transferir dados. Isto impede que o computador na localização não fidedigna estabeleça contacto com o servidor do site que está no interior da rede fidedigna. Estas ligações utilizam a **Conta de Instalação do Sistema de Sites**.  

**Ao utilizar uma função do sistema de sites que foi instalada numa floresta não fidedigna,** as firewalls têm de permitir o tráfego de rede, mesmo quando o servidor do site inicia a transferência dos dados.  

Além disso, as seguintes funções do sistema de sites requerem acesso direto à base de dados do site. Por conseguinte, as firewalls têm de permitir tráfego aplicável das florestas não fidedignas para SQL Server do site:  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de Endpoint Protection  

-   Ponto de inscrição  

-   Ponto de gestão  

-   Ponto do sistema de reporte  

-   Ponto de migração de estado  

Para obter mais informações, consulte o artigo [portas utilizadas no System Center Configuration Manager](../../../core/plan-design/hierarchy/ports.md).  

**Pode ser necessário configurar o acesso à função do sistema de sites para a base de dados do site:**  

As funções do sistema de sites do ponto de gestão e do ponto de registo estabelecem ligação à base de dados do site.  

-   Por predefinição, quando estas funções de sistema de sites são instaladas, do Configuration Manager configura a conta de computador do novo servidor do sistema de sites como conta de ligação para a função de sistema de sites e, em seguida, adiciona a conta à função adequada para a base de dados de SQL Server.  

-   Ao instalar estas funções do sistema de sites num domínio não fidedigno, terá de configurar a conta de ligação da função do sistema de sites para permitir que a função do sistema de sites obtenha informações da base de dados.  

Se configurar uma conta de utilizador de domínio como conta de ligação para estas funções do sistema de sites, certifique-se de que a conta de utilizador de domínio possui acesso adequado à base de dados do SQL Server nesse site:  

-   Ponto de gestão: **Conta de ligação de base de dados do ponto de gestão**  

-   Ponto de registo: **Conta de ligação de ponto de inscrição**  

Ao planear funções do sistema de sites noutras florestas, considere as seguintes informações adicionais:  

-   Se executar a Firewall do Windows, configure os perfis de firewall aplicáveis para transmitirem comunicações entre o servidor de base de dados do site e os computadores que são instalados com funções do sistema de sites remoto. Para obter informações sobre perfis de firewall, consulte o artigo [Noções sobre perfis de firewall](http://go.microsoft.com/fwlink/p/?LinkId=233629).  

-   Se o ponto de gestão baseado na Internet confiar na floresta que contém as contas de utilizador, são suportadas políticas de utilizador. Se não existir qualquer fidedignidade, só são suportadas políticas de computador.  

#### <a name="communication-between-clients-and-site-system-roles-when-the-clients-are-not-in-the-same-active-directory-forest-as-their-site-server"></a>Comunicação entre clientes e funções do sistema de sites quando os clientes não estão na mesma floresta do Active Directory que o respetivo servidor de site  
O Configuration Manager suporta os seguintes cenários para clientes que não estejam na mesma floresta que o seu servidor do site:  

-   Existe uma fidedignidade de floresta bidirecional entre a floresta do cliente e a floresta do servidor do site.  

-   O servidor de funções de sistema de sites está localizado na mesma floresta que o cliente.  

-   O cliente é num computador do domínio que não tenha uma floresta bidirecional fidedignidade com o servidor do site e do site as funções do sistema não estão instaladas na floresta do cliente.  

-   O cliente se encontre num computador de grupo de trabalho.  

Os clientes num computador associado a um domínio podem utilizar serviços de domínio do Active Directory para localização de serviços quando o respetivo site é publicado na sua floresta do Active Directory.  

Para publicar informações do site noutra floresta do Active Directory, tem de:  

-   Especificar primeiro a floresta, ativando em seguida a publicação nessa floresta no nó **Florestas do Active Directory** da área de trabalho **Administração** .  

-   Configurar cada site para publicar os respetivos dados nos Serviços de Domínio do Active Directory. Esta configuração permite aos clientes dessa floresta obter as informações de site e localizar pontos de gestão. Para clientes que não é possível utilizar serviços de domínio do Active Directory para localização de serviços, pode utilizar DNS, WINS ou o cliente do ponto de gestão atribuído.  

###  <a name="bkmk_xchange"></a> Colocar o conector do Exchange Server numa floresta remota  
Para suportar este cenário, certifique-se de que a resolução de nomes funciona entre as florestas (por exemplo, configurando reencaminhamentos de DNS) e quando configurar o conector do Exchange Server, especifique o FQDN da intranet do Exchange Server. Para obter mais informações, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  


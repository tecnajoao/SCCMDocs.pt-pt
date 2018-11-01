---
title: Comunicações entre pontos finais
titleSuffix: Configuration Manager
description: Saiba como os componentes e sistemas de sites do Configuration Manager comunicam através de uma rede.
ms.date: 10/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ce3353d9cc139da53a655f50144c3816b1a4a355
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411379"
---
# <a name="communications-between-endpoints-in-configuration-manager"></a>Comunicações entre pontos finais no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo descreve como os sistemas de sites do Configuration Manager e clientes comunicam na sua rede. Ele inclui as secções seguintes:  

- [Comunicações entre sistemas de sites num site](#Planning_Intra-site_Com)  
    - [Servidor do site para o ponto de distribuição](#bkmk_site2dp)  

- [Comunicações de clientes para sistemas e serviços do site](#Planning_Client_to_Site_System)  
    - [Cliente para comunicação de ponto de gestão](#bkmk_client2mp)  
    - [Cliente para comunicação de ponto de distribuição](#bkmk_client2dp)  
    - [Considerações sobre comunicações do cliente a partir da internet ou numa floresta não fidedigna](#BKMK_clientspan)  
    - [Sobre sistemas de sites com acesso à internet](#bkmk_internetfacing)  

- [Comunicação entre florestas do Active Directory](#Plan_Com_X-Forest)  
    - [Suportar computadores de domínio numa floresta que não seja considerada fidedigna pela floresta do seu servidor de site](#bkmk_noforesttrust)  
    - [Suportar computadores num grupo de trabalho](#bkmk_workgroup)  
    - [Cenários para suportar um site ou uma hierarquia que abranja vários domínios e florestas](#bkmk_span)  



##  <a name="Planning_Intra-site_Com"></a> Comunicações entre sistemas de sites num site  

 Quando os sistemas de sites do Configuration Manager ou componentes comunicam através da rede a outros sistemas de sites ou componentes do site, utilizam um dos protocolos seguintes, dependendo de como configurar o site:  

-   Bloco de mensagem de servidor (SMB)  

-   HTTP  

-   HTTPS  

À exceção da comunicação do servidor do site para um ponto de distribuição, as comunicações de servidor para servidor num site podem ocorrer em qualquer altura. Estas comunicações não utilizam mecanismos para controlar a largura de banda de rede. Uma vez que não é possível controlar a comunicação entre sistemas de sites, certifique-se de que instala servidores do sistema de sites em locais que têm redes bem conectadas e rápidas.  


### <a name="bkmk_site2dp"></a> Servidor do site para o ponto de distribuição 

Para ajudar a gerir a transferência de conteúdo do servidor do site para pontos de distribuição, utilize as seguintes estratégias:  

-   Configure o ponto de distribuição para o controlo da largura de banda de rede e o agendamento. Estes controlos assemelham-se as configurações que são utilizadas por endereços entre sites. Utilize esta configuração em vez de instalar outro site do Configuration Manager, quando a transferência de conteúdo para localizações de rede remotas é sua consideração de largura de banda principal.  

-   Pode instalar um ponto de distribuição como um ponto de distribuição pré-configurado. Um ponto de distribuição pré-configurado permite-lhe utilizar o conteúdo que é manualmente colocado no servidor do ponto de distribuição e remove o requisito de transferir ficheiros de conteúdo através da rede.  

Para obter mais informações, consulte [gerir a largura de banda de rede para gestão de conteúdos](manage-network-bandwidth.md).



##  <a name="Planning_Client_to_Site_System"></a> Comunicações de clientes para sistemas e serviços do site  

Os clientes iniciam a comunicação para funções de sistema de sites, serviços de domínio do Active Directory e serviços online. Para ativar estas comunicações, firewalls têm de permitir o tráfego de rede entre clientes e o ponto final de suas comunicações. Para obter mais informações sobre as portas e protocolos utilizados pelos clientes quando comunicam com estes pontos finais, consulte [portas utilizadas no Configuration Manager](/sccm/core/plan-design/hierarchy/ports).  

Antes de um cliente pode comunicar com uma função de sistema de sites, o cliente utiliza a localização de serviço para localizar uma função que suporta o protocolo do cliente (HTTP ou HTTPS). Por predefinição, os clientes utilizam o método mais seguro disponível para eles. Para obter mais informações, consulte [compreender como os clientes localizam os recursos de site e os serviços](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services).  

Para utilizar HTTPS, configure uma das seguintes opções:  

- Utilize uma infraestrutura de chaves públicas (PKI) e instalar certificados PKI nos clientes e servidores. Para obter informações sobre como utilizar certificados, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

- A partir da versão 1806, configurar o site para **sistemas de sites de certificados gerados pelo utilize o Gestor de configuração para HTTP**. Para obter mais informações, consulte [avançada HTTP](/sccm/core/plan-design/hierarchy/enhanced-http).  

Ao implementar uma função do sistema de sites que utiliza Serviços de Informação Internet (IIS) e suporta comunicações de clientes, tem de especificar se os clientes ligam ao sistema de sites através de HTTP ou HTTPS. Se utilizar HTTP, também tem de considerar as opções de assinatura e encriptação. Para obter mais informações, consulte [planear a assinatura e encriptação](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForSigningEncryption).  


### <a name="bkmk_client2mp"></a> Cliente para comunicação de ponto de gestão

Existem duas fases, quando um cliente comunica com um ponto de gestão: autenticação (transporte) e a autorização (mensagens). Este processo varia de acordo com os seguintes fatores: 
- Configuração do site: HTTP, HTTPS ou HTTP avançado
- Configuração do ponto de gestão: HTTPS apenas ou permite o HTTP ou HTTPS
- Identidade de dispositivo para cenários de TI centradas em dispositivo
- Identidade de utilizador para cenários centrada no utilizador

Utilize a seguinte tabela para compreender como este processo funciona:  

| Tipo de pacote de gestão  | Autenticação de cliente  | Autorização de cliente<br>Identidade de dispositivo  | Autorização de cliente<br>Identidade do utilizador  |
|----------|---------|---------|---------|
| HTTP     | Anónimo<br>Com HTTP avançada, o site verifica se o Azure AD *usuário* ou *dispositivo* token. | Pedido de localização: Anónimo<br>Pacote de cliente: Anónimo<br>Registo, utilizando um dos seguintes métodos para provar a identidade de dispositivo:<br> -Anônima (aprovação manual)<br> -Autenticação Windows-integrado<br> -As do azure AD *dispositivo* token (HTTP avançada)<br>Após o registo, o cliente utiliza a assinatura provar a identidade de dispositivo da mensagem | Para cenários de centrada no utilizador, através de um dos seguintes métodos para provar a identidade de utilizador:<br> -Autenticação Windows-integrado<br> -As do azure AD *utilizador* token (HTTP avançada) |
| HTTPS    | Através de um dos seguintes métodos:<br> -Certificado PKI<br> -Autenticação Windows-integrado<br> -As do azure AD *usuário* ou *dispositivo* token | Pedido de localização: Anónimo<br>Pacote de cliente: Anónimo<br>Registo, utilizando um dos seguintes métodos para provar a identidade de dispositivo:<br> -Anônima (aprovação manual)<br> -Autenticação Windows-integrado<br> -Certificado PKI<br> -As do azure AD *usuário* ou *dispositivo* token<br>Após o registo, o cliente utiliza a assinatura provar a identidade de dispositivo da mensagem | Para cenários de centrada no utilizador, através de um dos seguintes métodos para provar a identidade de utilizador:<br> -Autenticação Windows-integrado<br> -As do azure AD *utilizador* token |

> [!Tip]  
> Para obter mais informações sobre a configuração do ponto de gestão para tipos de identidade de dispositivo diferentes e com o gateway de gestão de nuvem, consulte [ativar o ponto de gestão para HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  


### <a name="bkmk_client2dp"></a> Cliente para comunicação de ponto de distribuição

Quando um cliente comunica com um ponto de distribuição, apenas tem de autenticar antes de transferir o conteúdo. Utilize a seguinte tabela para compreender como este processo funciona:


| Tipo de ponto de distribuição  | Autenticação de cliente  |
|----------|---------|
| HTTP     | -Anónimo, se permitido<br>-Autenticação Windows-integrado com a conta de computador ou a conta de acesso de rede<br> -Token de acesso conteúdo (HTTP avançada) |
| HTTPS    | -Certificado PKI<br> -Autenticação Windows-integrado com a conta de computador ou a conta de acesso de rede<br> -Token de acesso conteúdo |


###  <a name="BKMK_clientspan"></a> Considerações sobre comunicações do cliente a partir da internet ou numa floresta não fidedigna  

As seguintes funções de sistema de sites instaladas nos sites primários suportam ligações de clientes que se encontram em localizações não fidedignas, como a internet ou numa floresta não fidedigna. (Os sites secundários não suportam ligações de cliente a partir de localizações não fidedignas). 

-   Ponto de Web site do catálogo de aplicações  

-   Módulo de política do Configuration Manager (NDES) 

-   Ponto de distribuição   

-   Ponto de distribuição baseado na nuvem (requer HTTPS)

-   Ponto proxy de registo  

-   Ponto de estado de contingência  

-   Ponto de gestão  

-   Ponto de atualização de software  

-   Gateway de gestão na cloud (requer HTTPS)


### <a name="bkmk_internetfacing"></a> Sobre sistemas de sites com acesso à internet

> [!Note]  
> A secção seguinte é sobre cenários de gestão de clientes baseada na internet. Não se aplica a cenários de gateway de gestão na cloud. Para obter mais informações, consulte [gerir clientes na internet](/sccm/core/clients/manage/manage-clients-internet).  

Não existe nenhum requisito de fidedignidade entre a floresta de um cliente e que o servidor de sistema de sites. No entanto, quando a floresta que contenha um sistema de sites com acesso à internet confia na floresta que contém as contas de utilizador, esta configuração suporta políticas baseadas no utilizador para dispositivos na internet quando ativa a **política de cliente** definição de cliente **ativar pedidos da política de utilizador dos clientes internet**.  

Por exemplo, as configurações seguintes ilustram quando a gestão de clientes baseados na internet suporta políticas de utilizador para dispositivos na internet:  

-   O ponto de gestão baseado na internet é na rede de perímetro em que um controlador de domínio só de leitura reside para autenticar o utilizador e uma firewall intermediária permite pacotes do Active Directory.  

-   A conta de utilizador é na floresta A (a intranet) e o ponto de gestão baseado na internet é na floresta B (a rede de perímetro). A Floresta B confia na Floresta A e uma firewall intermediária permite os pacotes de autenticação.  

-   A conta de utilizador e o ponto de gestão baseado na internet são na floresta A (a intranet). O ponto de gestão é publicado na internet ao utilizar um servidor web proxy (como o Forefront Threat Management Gateway).  

> [!NOTE]  
>  Se a autenticação Kerberos falhar, será automaticamente tentada a autenticação NTLM.  

Como mostra o exemplo anterior, é possível colocar sistemas de sites baseados na internet na intranet quando eles estão publicados na internet ao utilizar um servidor de proxy da web. Estes sistemas de sites podem ser configurados para ligação de cliente a partir da internet apenas, ou para ligações de cliente da internet e intranet. Quando utilizar um servidor web proxy, pode configurá-lo para bridge de Secure Sockets Layer (SSL) para SSL (mais seguro) ou o protocolo de túnel SSL da seguinte forma:  

-   **Protocolo de bridge SSL para SSL:**   
    A configuração recomendada quando utiliza servidores web proxy para gestão de clientes baseados na internet é o protocolo de bridge para SSL, que utiliza a terminação de SSL com autenticação SSL. Os computadores cliente têm de ser autenticados utilizando a autenticação de computador e os clientes antigos do dispositivo móvel são autenticados utilizando a autenticação de utilizador. Dispositivos móveis inscritos pelo Configuration Manager não suportam o protocolo de bridge SSL.  

     A vantagem da terminação de SSL no servidor web proxy é que os pacotes da internet são sujeitos a inspeção antes de eles são reencaminhados para a rede interna. O servidor web proxy autentica a ligação do cliente, termina- e, em seguida, abre uma nova ligação autenticada para os sistemas de sites baseados na internet. Quando os clientes do Configuration Manager utilizarem um servidor web proxy, a identidade do cliente (GUID do cliente) está contida em segurança no payload do pacote, para que o ponto de gestão não considere o servidor de web de proxy é o cliente. Protocolo de bridge não é suportado no Configuration Manager com HTTP para HTTPS ou de HTTPS para HTTP.  

-   **Protocolo de túnel**:   
    Se seu servidor web proxy não suporta os requisitos de protocolo de bridge SSL ou se pretende configurar o suporte de internet para dispositivos móveis inscritos pelo Configuration Manager, protocolo de túnel SSL também é suportado. É uma opção menos segura porque os pacotes SSL da internet são reencaminhados para os sistemas de sites sem terminação de SSL, para que não é possível inspecioná-los relativamente a conteúdo malicioso. Quando utiliza o protocolo de túnel SSL, não existem requisitos de certificado para o servidor Web proxy.  



##  <a name="Plan_Com_X-Forest"></a> Comunicação entre florestas do Active Directory  

O Configuration Manager suporta sites e hierarquias que abrangem florestas do Active Directory. Também suporta computadores de domínio que não estão na mesma floresta do Active Directory que o servidor do site e computadores que estão em grupos de trabalho.  


### <a name="bkmk_noforesttrust"></a> Suportar computadores de domínio numa floresta que não seja considerada fidedigna pela floresta do seu servidor de site 

-   Instalar funções do sistema de sites nessa floresta não fidedigna, com a opção de publicar informações do site nessa floresta do Active Directory  

-   Gerir os computadores como se fossem computadores de grupo de trabalho  

Ao instalar servidores do sistema de sites numa floresta do Active Directory não fidedigna, a comunicação de cliente-servidor dos clientes nessa floresta é mantida dentro dessa floresta e do Configuration Manager pode autenticar o computador utilizando Kerberos. Quando publicar informações do site na floresta do cliente, os clientes beneficiarão da recuperando informações de site, como uma lista de pontos de gestão disponíveis, de sua floresta do Active Directory, em vez de transferir a partir do lhes foi atribuído ponto de gestão.  

> [!NOTE]  
>  Se pretender gerir dispositivos que estão na internet, pode instalar funções do sistema de sites baseados na internet na sua rede de perímetro, quando os servidores de sistema de sites estão numa floresta do Active Directory. Este cenário não requer uma fidedignidade bidirecional entre a rede de perímetro e a floresta do servidor do site.  


### <a name="bkmk_workgroup"></a> Suportar computadores num grupo de trabalho  

-   Aprovar manualmente os computadores do grupo de trabalho quando utilizam ligações de cliente HTTP para as funções do sistema de sites. O Configuration Manager não pode autenticar estes computadores através de Kerberos.  

-   Configurar a Conta de Acesso à Rede para que estes computadores possam receber conteúdos dos pontos de distribuição.  

-   Fornecer um mecanismo alternativo para que os clientes do grupo de trabalho localizem pontos de gestão. Utilizar a publicação de DNS, WINS, ou atribuir diretamente um ponto de gestão. Estes clientes não é possível obter as informações do site dos serviços de domínio do Active Directory.  

Para obter mais informações, consulte os artigos seguintes:  

-   [Gerir registos em conflito](/sccm/core/clients/manage/manage-clients#BKMK_ConflictingRecords)  

-   [Conta de acesso de rede](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#accounts-used-for-content-management)  

-   [Como instalar clientes do Configuration Manager em computadores de grupo de trabalho](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientWorkgroup)  


###  <a name="bkmk_span"></a> Cenários para suportar um site ou uma hierarquia que abranja vários domínios e florestas  

#### <a name="scenario-1-communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Cenário 1: Comunicação entre sites numa hierarquia que abranja florestas  
Este cenário requer uma fidedignidade de floresta bidirecional que suporte a autenticação Kerberos.  Se não tiver uma fidedignidade de floresta bidirecional que suporte a autenticação Kerberos, o Configuration Manager não suporta um site subordinado na floresta remota.  

O Configuration Manager suporta a instalação de um site subordinado numa floresta remota que possua a fidedignidade bidirecional necessária com a floresta do site principal. Por exemplo, pode colocar um site secundário noutra floresta do respetivo site primário principal, desde que a fidedignidade necessária exista.  

> [!NOTE]  
>  Um site subordinado pode ser um site primário (em que o site de administração central é o site principal) ou um site secundário.  

Comunicação entre sites no Configuration Manager utiliza a replicação de base de dados e transferências de ficheiros. Quando instala um site, tem de especificar uma conta com que pretende instalar o site no servidor designado. Esta conta também estabelece e mantém a comunicação entre sites. Depois do site instala e inicia a transferências de ficheiros e replicação de base de dados com êxito, não tem qualquer configuração adicional para comunicação com o site.  

Se existir uma fidedignidade de floresta bidirecional, o Configuration Manager não requer quaisquer passos de configuração adicionais.  

Por predefinição, quando instala um novo site subordinado, o Configuration Manager configura os seguintes componentes:  

-   Uma rota de replicação entre sites, baseada em ficheiros em cada site que utiliza a conta do computador servidor de sites. A conta de computador de cada computador para o Configuration Manager acrescenta o **SMS_SiteToSiteConnection_&lt;sitecode\>**  grupo no computador de destino.  

-   Replicação de base de dados entre os SQL Servers em cada site.  

Também defina as seguintes configurações:  

-   Firewalls intervenientes e dispositivos de rede tem de permitir os pacotes de rede exigidos pelo Configuration Manager.  

-   A resolução de nomes tem de funcionar entre as florestas.  

-   Para instalar um site ou função do sistema de sites, terá de especificar uma conta com permissões de administrador local no computador especificado.  

#### <a name="scenario-2-communication-in-a-site-that-spans-forests"></a>Cenário 2: Comunicação num site que abranja florestas  
Este cenário não requer uma fidedignidade de floresta bidirecional.  

Sites primários suportam a instalação de funções de sistema de sites em computadores em florestas remotas.  

-   O ponto de serviço Web do Catálogo de Aplicações é a única exceção.  Só é suportado na mesma floresta que o servidor do site.  

-   Se uma função de sistema de sites aceita ligações a partir da internet, como prática recomendada de segurança, instale as funções de sistema de sites num local em que o limite da floresta forneça proteção para o servidor de site (por exemplo, numa rede de perímetro).  

Para instalar uma função do sistema de sites num computador numa floresta não fidedigna:  

- Especifique um **conta de instalação do sistema de sites**, que o site utiliza para instalar a função de sistema de sites. (Esta conta tem de ter credenciais administrativas locais para estabelecer ligação ao.) Em seguida, instale funções do sistema de site no computador especificado.  

- Selecionar a opção de sistema de sites **exigir que o servidor do site inicie ligações a este sistema de sites**. Esta definição necessita que o servidor do site estabeleça ligações ao servidor de sistema de sites para transferir dados. Esta configuração impede que o computador na localização não fidedigna estabeleça contacto com o servidor do site que está dentro da rede fidedigna. Estas ligações utilizam a **Conta de Instalação do Sistema de Sites**.  

Para utilizar uma função de sistema de sites que foi instalada numa floresta não fidedigna, firewalls têm de permitir o tráfego de rede, mesmo quando o servidor do site inicia a transferência de dados.  

Além disso, as seguintes funções do sistema de sites requerem acesso direto à base de dados do site. Por conseguinte, firewalls têm de permitir tráfego aplicável das florestas não fidedignas para o SQL Server do site:  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de Endpoint Protection  

-   Ponto de inscrição  

-   Ponto de gestão  

-   Ponto do sistema de reporte  

-   Ponto de Migração de Estado  

Para obter mais informações, consulte [portas utilizadas no Configuration Manager](/sccm/core/plan-design/hierarchy/ports).  

Poderá ter de configurar o acesso de ponto de gestão ponto e a inscrição, a base de dados do site.

-   Por predefinição, quando instalar estas funções, o Configuration Manager configura a conta de computador do novo servidor do sistema de sites como conta de ligação para a função de sistema de sites. Em seguida, adiciona a conta à função adequada para a base de dados de SQL Server.  

-   Ao instalar estas funções de sistema de sites num domínio não fidedigno, configure a conta da ligação de função de sistema de sites para ativar a função de sistema de sites obter informações da base de dados.  

Se configurar uma conta de utilizador de domínio para a conta de ligação para estas funções de sistema de sites, certifique-se de que a conta de utilizador de domínio possui acesso adequado à base de dados do SQL Server nesse site:  

-   Ponto de gestão: **Conta de ligação de base de dados do ponto de gestão**  

-   Ponto de registo: **Conta de ligação de ponto de inscrição**  

Ao planear funções do sistema de sites noutras florestas, considere as seguintes informações adicionais:  

-   Se executar o Windows Firewall, configure os perfis de firewall aplicáveis para transmitirem comunicações entre o servidor de base de dados do site e os computadores que são instalados com funções do sistema de sites remoto.   

-   Quando o ponto de gestão baseado na internet confiar na floresta que contém as contas de utilizador, são suportadas políticas de utilizador. Se não existir qualquer fidedignidade, só são suportadas políticas de computador.  

#### <a name="scenario-3-communication-between-clients-and-site-system-roles-when-the-clients-arent-in-the-same-active-directory-forest-as-their-site-server"></a>Cenário 3: Comunicação entre clientes e funções de sistema de sites quando os clientes não estão na mesma floresta do Active Directory que o respetivo servidor de site  
O Configuration Manager suporta os seguintes cenários para clientes que não estão na mesma floresta do respetivo servidor de site:  

-   Existe uma fidedignidade de floresta bidirecional entre a floresta do cliente e a floresta do servidor do site.  

-   O servidor de função do sistema de sites está localizado na mesma floresta que o cliente.  

-   O cliente está num computador de domínio que não tem uma floresta bidirecional de confiança com o servidor do site e do site de funções do sistema não estão instaladas na floresta do cliente.  

-   O cliente se encontre num computador de grupo de trabalho.  

Os clientes num computador associado a um domínio podem utilizar serviços de domínio do Active Directory para localização de serviços quando o respetivo site for publicado na sua floresta do Active Directory.  

Para publicar informações do site noutra floresta do Active Directory:  

-   Especificar primeiro a floresta, ativando em seguida a publicação nessa floresta no nó **Florestas do Active Directory** da área de trabalho **Administração** .  

-   Configurar cada site para publicar os respetivos dados nos Serviços de Domínio do Active Directory. Esta configuração permite aos clientes dessa floresta obter as informações de site e localizar pontos de gestão. Para clientes que não é possível utilizar os serviços de domínio do Active Directory para localização de serviços, pode utilizar o DNS, WINS, ou ponto de gestão atribuído do cliente.  


####  <a name="bkmk_xchange"></a> Cenário 4: Colocar o conector do Exchange Server numa floresta remota  

Para suportar este cenário, certifique-se de que a resolução de nomes funciona entre as florestas. Por exemplo, configurando reencaminhamentos de DNS. Quando configurar o conector do Exchange Server, especifique o FQDN do servidor do Exchange da intranet. Para obter mais informações, consulte [gerir dispositivos móveis com o Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



## <a name="see-also"></a>Consulte também

- [Plano de segurança](/sccm/core/plan-design/security/plan-for-security)  

- [Segurança e privacidade para clientes do Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  


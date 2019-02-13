---
title: Opções de função de sistema do site
titleSuffix: Configuration Manager
description: Consulte este artigo para obter detalhes sobre funções de sistema de sites do Configuration Manager que não são necessariamente auto-explicativos.
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 209e09ba11de851a1275211364af3cee930737d0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131545"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Opções de configuração para funções de sistema de sites no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A maioria das opções de configuração para funções de sistema de sites do Configuration Manager são facilmente compreensíveis ou são explicadas nas caixas de assistente ou a caixa de diálogo, quando configurá-las. As secções seguintes explicam as funções de sistema de sites cujas definições poderão necessitar de informações adicionais.  



##  <a name="BKMK_ApplicationCatalog_Website"></a> Ponto de Web site do catálogo de aplicações  

> [!Note]  
> A partir da versão 1806, o ponto de Web site do catálogo de aplicações não se encontra *necessária*, mas ainda *suportado*. Para obter mais informações, consulte [configurar o Centro de Software](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).  
> 
> O **experiência de usuário do Silverlight** para o site do catálogo de aplicativos ponto já não é suportado. Para obter mais informações, consulte [funcionalidades removidas e preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

 Para obter mais informações sobre como configurar o ponto de sites do catálogo de aplicações, consulte [planear e configurar a gestão de aplicações](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

 #### <a name="client-connections"></a>Ligações de cliente
 Selecione **HTTPS** para utilizar a definição de ligação mais segura e para verificar se os clientes ligam a partir da internet. Esta opção requer um certificado PKI no servidor para a autenticação de servidor para clientes e para encriptação de dados através de Secure Socket Layer (SSL). Para obter mais informações, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Para um exemplo de implementação do certificado de servidor e informações sobre como configurá-lo nos serviços de informação Internet (IIS), consulte [implementar o certificado de servidor web para sistemas de sites que executam o IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  

 #### <a name="add-application-catalog-website-to-trusted-sites-zone"></a>Adicionar Web site do catálogo de aplicações à zona de sites fidedignos  
 Esta mensagem mostra o valor predefinida as definições de cliente se o **catálogo de aplicações adicionar Web site à zona de sites fidedignos do Internet Explorer** definição do cliente está atualmente configurado para **verdadeiro** ou **False**. Se utilizou as definições de cliente personalizadas para configurar esta definição, ative esta definição.  

 Se este sistema de sites está configurado para um nome de domínio completamente qualificado (FQDN) e o Web site não está na zona sites fidedignos do Internet Explorer, aos utilizadores que introduzam credenciais quando se ligam ao catálogo de aplicações.  

 #### <a name="organization-name"></a>Nome da organização  

 Introduza o nome que os utilizadores veem no catálogo de aplicações. Estas informações de imagem corporativa ajudam os utilizadores a identificar este Web site como uma origem fidedigna.  



##  <a name="BKMK_ApplicationCatalog_WebService"></a> Ponto de serviço da web de catálogo de aplicações  

> [!Note]  
> A partir da versão 1806, ponto de serviço web do catálogo de aplicações não se encontra *necessária*, mas ainda *suportado*. Para obter mais informações, consulte [configurar o Centro de Software](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).  

 Para obter mais informações sobre como configurar o ponto de serviço web do catálogo de aplicações, consulte [planear e configurar a gestão de aplicações](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

 #### <a name="https"></a>HTTPS

 Selecione **HTTPS** para autenticar o site do catálogo de aplicações aponta para este ponto de serviço web do catálogo de aplicações. Esta opção requer um certificado PKI nos servidores que executem o ponto de sites do catálogo de aplicações para a autenticação de servidor e para encriptação de dados através de SSL. Para obter mais informações, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Para um exemplo de implementação do certificado de servidor e informações sobre como configurá-lo nos serviços de informação Internet (IIS), consulte [implementar o certificado de servidor web para sistemas de sites que executam o IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_CertificateRegistrationPoint"></a> Ponto de registo de certificados  

 Para obter mais informações sobre como configurar o ponto de registo de certificados, consulte [introdução aos perfis de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  



##  <a name="BKMK_Distribution_Point"></a> Ponto de distribuição  

 Para obter mais informações sobre como configurar o ponto de distribuição para implementação de conteúdos, consulte [gerir a infraestrutura de conteúdo e conteúda](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

 Para obter mais informações sobre como configurar o ponto de distribuição para implementações de PXE, consulte [utilizar o PXE para implementar o Windows na rede](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  

 Para obter mais informações sobre como configurar o ponto de distribuição para implementações por multicast, consulte [utilizar multicast para implementar o Windows através da rede](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).  

 #### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>Instalar e configurar o IIS se exigido pelo Configuration Manager
 Selecione esta opção para permitir que o Configuration Manager instalar e configurar IIS no sistema de sites se ainda não estiver instalado. O IIS tem de ser instalado em todos os pontos de distribuição e tem de selecionar esta definição para continuar no assistente.  

 #### <a name="site-system-installation-account"></a>Conta de Instalação de Sistema de Sites
 Para pontos de distribuição que estão instalados no servidor do site, apenas a conta de computador do servidor do site é suportada para utilização como conta de instalação do sistema de sites. Para obter mais informações, consulte [contas](/sccm/core/plan-design/hierarchy/accounts#site-system-installation-account).  

 #### <a name="create-a-self-signed-certificate-or-import-a-pki-client-certificate"></a>Criar um certificado autoassinado ou importar um certificado PKI de cliente
 Este certificado tem duas finalidades:  

1.  Autentica o ponto de distribuição para um ponto de gestão antes do ponto de distribuição envia mensagens de estado.  

2.  Quando **ativar suporte PXE para clientes** é selecionado, o certificado é enviado para os computadores para o arranque PXE. Utilizarem este certificado para ligar a um ponto de gestão durante a implementação do sistema operacional.  

Quando todos os pontos de gestão no site estão configurados para HTTP, crie um certificado autoassinado. Quando os pontos de gestão estão configurados para HTTPS, importe um certificado de cliente PKI.  

Para importar o certificado, navegue para um ficheiro de Public-Key Cryptography Standards #12 (PKCS #12) que tem um certificado PKI com os seguintes requisitos para o Configuration Manager:  

-   Utilização prevista deve incluir a autenticação de cliente.  

-   A chave privada tem de ser definida para ser exportada.  

Não existem não requisitos específicos para o nome do requerente do certificado ou nome alternativo do requerente (SAN). Pode utilizar o mesmo certificado para vários pontos de distribuição.  

Para obter mais informações sobre os requisitos de certificado, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements). 

Para um exemplo de implementação deste certificado, consulte [implementar o certificado de cliente para pontos de distribuição](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012).  

#### <a name="enable-this-distribution-point-for-prestaged-content"></a>Ativar conteúdo pré-configurado para este ponto de distribuição
Selecione esta caixa de verificação para ativar o ponto de distribuição para conteúdo pré-configurado. Quando ativa esta opção, pode configurar o comportamento de distribuição quando distribuir conteúdos. Pode escolher se pré-configurar sempre o conteúdo no ponto de distribuição, pré-configurar o conteúdo inicial para o pacote, mas utilizar o processo normal de distribuição de conteúdo para atualizações ao conteúdo ou utilize sempre o processo normal de distribuição de conteúdo para o conteúdo no pacote. Para obter mais informações, consulte [conteúdo pré-configurado](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).  

#### <a name="boundary-groups"></a>Grupos de limites
 Pode associar grupos de limites para um ponto de distribuição. Durante a implementação de conteúdos, os clientes devem ser num grupo de limites que estão associado com o ponto de distribuição para utilizá-la como uma localização de origem para o conteúdo. Configure as relações entre grupos de limites que verificar quando um cliente pode começar a pesquisar grupos de limites adicionais para localizações de origem de conteúdo válida. Para obter mais informações, consulte [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).



##  <a name="BKMK_Enrollment_Point"></a> Ponto de registo  

Pontos de registo que são utilizados para instalar computadores macOS e inscrever dispositivos que gere com a gestão de dispositivos móveis no local. Para obter mais informações, veja os artigos seguintes:  

-   [Como implementar clientes em Macs](/sccm/core/clients/deploy/deploy-clients-to-macs)  

-   [Como os utilizadores inscrevem dispositivos com o MDM no local](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm)  

#### <a name="allowed-connections"></a>Ligações permitidas
 A definição de HTTPS é selecionada automaticamente e requer um certificado PKI no servidor para a autenticação de servidor para o ponto proxy de registo, a autenticação de servidor para o ponto de serviço fora de banda e a encriptação dos dados através de SSL. Para obter mais informações, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Para um exemplo de implementação do certificado de servidor e informações sobre como configurá-lo no IIS, consulte [implementar o certificado de servidor web para sistemas de sites que executam o IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_Enrollment_Proxy_Point"></a> Ponto proxy de registo  

Para obter mais informações sobre como configurar um ponto de proxy de inscrição para dispositivos móveis, consulte [como os utilizadores inscrevem dispositivos com o MDM no local](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm).  

#### <a name="client-connections"></a>Ligações de cliente
 A definição de HTTPS é selecionada automaticamente. Ele requer os seguintes certificados PKI no servidor: 
- Para a autenticação de servidor para dispositivos móveis e computadores Mac que inscreve com o Configuration Manager 
- Para encriptação de dados através de Secure Sockets Layer (SSL)

Para obter mais informações sobre os requisitos de certificado, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Para um exemplo de implementação do certificado de servidor e informações sobre como configurá-lo no IIS, consulte [implementar o certificado de servidor web para sistemas de sites que executam o IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_Fallback_Status_Point"></a> Ponto de estado de contingência  

#### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>Número de mensagens de estado e o intervalo de limitação (em segundos)
As predefinições para estas opções são 10 000 mensagens de estado e 3.600 segundos para o intervalo de limitação. Embora estas definições são suficientes para a maioria das circunstâncias, poderá ter de alterá-los quando ambas as condições seguintes forem verdadeiras:  

-   O ponto de estado de contingência aceita ligações apenas a partir da intranet.  

-   Utilizar o ponto de estado de contingência durante uma implementação de implementação do cliente de muitos computadores.  

Neste cenário, um fluxo contínuo de mensagens de estado pode criar um registo de segurança de mensagens de estado que provoca utilização elevada do processador no servidor do site por um período tolerável. Além disso, poderá não ver as informações atualizadas sobre a implementação de cliente na consola do Configuration Manager e nos relatórios de implementação do cliente.  

Estas definições de ponto de estado de contingência destinam-se para configurar mensagens de estado que são geradas durante a implementação do cliente. As definições não são concebidas para ser definida para problemas de comunicação de cliente, como quando os clientes na internet não é possível ligar ao respetivo ponto de gestão baseado na internet. Uma vez que o ponto de estado de contingência não é possível aplicar estas definições apenas para as mensagens de estado que são geradas durante a implementação do cliente, não configure estas definições se o ponto de estado de contingência aceita ligações a partir da internet.  

Cada computador que instala o cliente do Configuration Manager com êxito envia as mensagens de estado de quatro seguintes para o ponto de estado de contingência:  

-   Implementação de cliente iniciada  

-   Implementação de cliente concluída com êxito  

-   Atribuição de cliente iniciada  

-   Atribuição de cliente com êxito  

Computadores que não pode ser instalado ou que atribuir o cliente do Configuration Manager enviam mensagens de estado adicionais.  

Por exemplo, se implementar o cliente do Configuration Manager em 20.000 computadores, a implementação poderá enviar 80.000 mensagens de estado para o ponto de estado de contingência. Uma vez que a configuração de limitação predefinida permite 10.000 mensagens de estado para ser enviada para o ponto de estado de contingência a cada 3.600 segundos (1 hora), as mensagens de estado podem ficar pendentes no ponto de estado de contingência. Considere também a largura de banda de rede disponível entre o ponto de estado de contingência e o servidor do site e o poder de processamento do servidor do site para processar muitas mensagens de estado.  

Para ajudar a evitar estes problemas, considere um aumento no número de mensagens de estado e um decréscimo no intervalo de limitação.  

Repor os valores de limitação para o ponto de estado de contingência se uma das seguintes condições for verdadeira:  

-   Calcular a que os valores de limitação atuais são superiores ao necessário para processar mensagens de estado do ponto de estado de contingência.  

-   Achar que as definições de limitação atuais criam utilização elevada do processador no servidor do site.  

Não altere as definições para as definições de limitação do ponto de estado de contingência, a menos que compreenda as consequências. Por exemplo, quando aumenta as definições de limitação para alta, o uso do processador no servidor do site pode aumentar a alta, que pode atrasar todas as operações do site.  

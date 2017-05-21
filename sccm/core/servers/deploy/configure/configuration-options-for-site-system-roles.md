---
title: "Opções de função de sistema de sites | Documentos do Microsoft"
description: "Consulte este artigo para obter detalhes sobre funções de sistema de sites do Configuration Manager que não são necessariamente facilmente compreensíveis."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: fff93794afdfa9f890b1f06d6c330d8cffc5796c
ms.openlocfilehash: b4db5d86cc0ed020ed176feb2e8f1f9dc51a2280
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="configuration-options-for-site-system-roles-for-system-center-configuration-manager"></a>Opções de configuração para funções do sistema de sites do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A maioria das opções de configuração para funções de sistema de sites do System Center Configuration Manager são facilmente compreensíveis ou são explicadas nas caixas de assistente ou a caixa de diálogo, quando configura-os. As secções seguintes explicam funções de sistema de sites cujas definições poderão necessitar de informações adicionais.  

##  <a name="BKMK_ApplicationCatalog_Website"></a>Ponto de Web site do catálogo de aplicações  
 Para obter informações sobre como configurar o ponto de Web site do catálogo de aplicações para o catálogo de aplicações, consulte o artigo [planear e configurar a gestão de aplicações no System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **Ligações de cliente**  

 Selecione **HTTPS** para utilizar a definição de ligação mais segura e para verificar se os clientes ligam a partir da Internet. Esta opção requer um certificado PKI no servidor para autenticação de servidor a clientes e para encriptação de dados através de Secure Socket Layer (SSL). Para mais informações sobre os requisitos de certificados, consulte o artigo [requisitos de certificados PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para um exemplo de implementação do certificado de servidor e informações sobre como configurá-lo nos serviços de informação Internet (IIS), consulte o *implementar o certificado de servidor Web para sistemas de sites que executam o IIS* secção [exemplo passo a passo de implementação de PKI certificados para o System Center Configuration Manager: Autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

 **Adicionar Web site do catálogo de aplicações à zona de sites fidedignos**  

 Esta mensagem mostra o valor na predefinição definições de cliente se o **Web site do catálogo de aplicações de adicionar à zona de sites fidedignos do Internet Explorer** definição de cliente está atualmente configurado para **verdadeiro** ou **falso**. Se utilizou definições personalizadas de cliente para configurar esta definição, tem de verificar este valor manualmente.  

 Se este sistema de sites estiver configurado para um nome de domínio completamente qualificado (FQDN) e o Web site não está na zona sites fidedignos no Internet Explorer, os utilizadores serão pedidos credenciais quando se ligam ao catálogo de aplicações.  

 **Nome da organização**  

 Introduza o nome que os utilizadores visualizam no catálogo de aplicações. Estas informações de imagem corporativa ajudam os utilizadores a identificar este Web site como uma origem fidedigna.  

##  <a name="BKMK_ApplicationCatalog_WebService"></a>Ponto de serviço da web de catálogo de aplicações  
 Para obter informações sobre como configurar o ponto de serviço web do catálogo de aplicações para o catálogo de aplicações, consulte o artigo [planear e configurar a gestão de aplicações no System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **HTTPS**  

 Selecione **HTTPS** para autenticar o Web site do catálogo de aplicações pontos para este ponto de serviço web do catálogo de aplicações.  Esta opção requer um certificado PKI nos servidores que executem o ponto de Web site do catálogo de aplicações para autenticação de servidor e para encriptação de dados através de SSL. Para mais informações sobre os requisitos de certificados, consulte o artigo [requisitos de certificados PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para um exemplo de implementação do certificado de servidor e informações sobre como configurá-lo no IIS, consulte o *implementar o certificado de servidor Web para sistemas de sites que executam o IIS* secção [exemplo passo a passo de implementação de PKI certificados para o System Center Configuration Manager: Autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="BKMK_CertificateRegistrationPoint"></a>Ponto de registo de certificados  
 Para mais informações sobre como configurar o ponto de registo de certificados, consulte o artigo [introdução aos perfis de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

##  <a name="BKMK_Distribution_Point"></a>Ponto de distribuição  
 Para mais informações sobre como configurar o ponto de distribuição para implementação de conteúdos, consulte o artigo [gerir a infraestrutura do conteúdo e conteúda para o System Center Configuration Manager](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Para mais informações sobre como configurar o ponto de distribuição para implementações de PXE, consulte o artigo [utilizar PXE para implementar o Windows através da rede com o System Center Configuration Manager](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Para obter informações sobre como configurar o ponto de distribuição para implementações por multicast, consulte o artigo [utilize o multicast para implementar o Windows através da rede com o System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 **Instalar e configurar o IIS se exigido pelo Configuration Manager**  
 Selecione esta opção para permitir que o Configuration Manager instalar e configurar o IIS no sistema de sites se não estiver já instalado. O IIS tem de ser instalado em todos os pontos de distribuição e tem de selecionar esta definição para o assistente continuar.  

 **Conta de instalação do sistema de sites**  
 Pontos de distribuição que estão instalados num servidor do site, apenas a conta de computador do servidor do site é suportada para utilização como conta de instalação do sistema de sites.  

 **Criar um certificado autoassinado ou importar um certificado PKI de cliente**  
 Este certificado tem duas finalidades:  

1.  Autentica o ponto de distribuição para um ponto de gestão antes do ponto de distribuição envia mensagens de estado.  

2.  Quando **ativar suporte PXE para clientes** é selecionado, o certificado é enviado para computadores que efetuar um arranque PXE para que se possam ligar a um ponto de gestão durante a implementação do sistema operativo.  

Quando todos os pontos de gestão no site estão configurados para HTTP, crie um certificado autoassinado. Quando os pontos de gestão estão configurados para HTTPS, importe um certificado de cliente PKI.  

Para importar o certificado, navegue para um ficheiro de Public-Key Cryptography Standards #12 (PKCS #12) que tenha um certificado PKI com os seguintes requisitos para o Configuration Manager:  

-   A utilização prevista deve incluir a autenticação de cliente.  

-   A chave privada tem de ser configurada para ser exportada.  

Não não existem requisitos específicos para o nome de requerente do certificado ou nome alternativo do requerente (SAN), e pode utilizar o mesmo certificado para vários pontos de distribuição.  

Para mais informações sobre os requisitos de certificados, consulte o artigo [requisitos de certificados PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md). Para um exemplo de implementação deste certificado, consulte o *implementar o certificado de cliente para pontos de distribuição* secção [exemplo passo a passo de implementação de PKI certificados para o System Center Configuration Manager: Autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

**Ativar conteúdo pré-configurado para este ponto de distribuição**  
Selecione esta caixa de verificação para ativar o ponto de distribuição para conteúdo pré-configurado. Quando esta caixa de verificação estiver selecionada, pode configurar o comportamento de distribuição quando distribuir conteúdos. Pode escolher se lhe pré-configurar sempre os conteúdos no ponto de distribuição, pré-configura o conteúdo inicial do pacote, mas utilize o processo normal de distribuição de conteúdo para atualizações de conteúdo ou utilize sempre o processo normal de distribuição de conteúdo para o conteúdo do pacote.  

**Grupos de limites**  
 Pode associar grupos de limites para um ponto de distribuição. Durante a implementação de conteúdos, os clientes tem de ser um grupo de limites que esteja associado com o ponto de distribuição a utilizar como localização de origem para o conteúdo.
 - **Antes da versão 1610**, pode verificar o **permitir a localização de origem de contingência para conteúdo** caixa de verificação para permitir que os clientes fora destes limites grupos revertam e utilizem o ponto de distribuição como localização de origem de conteúdo quando não houver outros pontos de distribuição estão disponíveis.
 - **Iniciar com a versão 1610**, já não pode configurar **permitir a localização de origem de contingência para conteúdo**.  Em vez disso, configure as relações entre grupos de limites que verifiquem quando um cliente pode começar a procurar grupos de limites adicionais para localizações de origem de conteúdo válida.

##  <a name="BKMK_Enrollment_Point"></a>Ponto de inscrição  
Pontos de registo são utilizados para instalar computadores Mac e inscrever dispositivos que gere com gestão de dispositivos móveis no local. Para obter mais informações, consulte o seguinte:  

-   [Como implementar clientes Macs no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md)  

-   [Como os utilizadores inscrevem os dispositivos com gestão de dispositivos móveis no local no System Center Configuration Manager](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

**Ligações permitidas**  
 A definição de HTTPS é selecionada automaticamente e requer um certificado PKI no servidor para autenticação de servidor para o ponto proxy de registo, a autenticação de servidor para o ponto de serviço fora de banda e a encriptação de dados através de SSL. Para mais informações sobre os requisitos de certificados, consulte o artigo [requisitos de certificados PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para um exemplo de implementação do certificado de servidor e informações sobre como configurá-lo no IIS, consulte o *implementar o certificado de servidor Web para sistemas de sites que executam o IIS* secção [exemplo passo a passo de implementação de PKI certificados para o System Center Configuration Manager: Autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="BKMK_Enrollment_Proxy_Point"></a>Ponto proxy de registo  
Para mais informações sobre como configurar um ponto de proxy de inscrição para dispositivos móveis, consulte o artigo [como os utilizadores inscrevem os dispositivos com gestão de dispositivos móveis no local no System Center Configuration Manager](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

**Ligações de cliente**  
 A definição de HTTPS é selecionada automaticamente e requer um certificado PKI no servidor para autenticação de servidor para dispositivos móveis e computadores Mac que são inscritos pelo Configuration Manager e para encriptação de dados através de Secure Sockets Layer (SSL). Para mais informações sobre os requisitos de certificados, consulte o artigo [requisitos de certificados PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Para um exemplo de implementação do certificado de servidor e informações sobre como configurá-lo no IIS, consulte o *implementar o certificado de servidor Web para sistemas de sites que executam o IIS* secção [exemplo passo a passo de implementação de PKI certificados para o System Center Configuration Manager: Autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="BKMK_Fallback_Status_Point"></a>Ponto de estado de contingência  
**Número de mensagens de estado** e **intervalo de limitação (em segundos)**  
Embora as predefinições para estas opções (10.000 mensagens de estado e 3.600 segundos para o intervalo de limitação) sejam suficientes para a maior parte das circunstâncias, poderá ter de alterar quando as duas condições seguintes forem verdadeiras:  

-   O ponto de estado de contingência aceita ligações apenas a partir da intranet.  

-   Utilizar o ponto de estado de contingência durante uma fase de rollout de implementação de cliente para muitos computadores.  

Neste cenário, um fluxo contínuo de mensagens de estado pode criar um registo de segurança de mensagens de estado que provoca utilização elevada unidade de processamento central (CPU) no servidor do site durante um período prolongado. Além disso, não poderá ver informações atualizadas sobre a implementação de cliente na consola do Configuration Manager e nos relatórios de implementação de cliente.  

Estas definições de ponto de estado de contingência destinam-se para configurar mensagens de estado que são geradas durante a implementação do cliente. As definições não se destinam a ser configurada para problemas de comunicação de cliente, como quando os clientes na Internet não consegue ligar ao respetivo ponto de gestão baseado na Internet. Uma vez que o ponto de estado de contingência não consegue aplicar estas definições apenas para as mensagens de estado que são geradas durante a implementação do cliente, não configure estas definições quando o ponto de estado de contingência aceita ligações da Internet.  

Cada computador que instala com êxito o cliente do System Center 2012 Configuration Manager envia as seguintes mensagens de estado de quatro para o ponto de estado de contingência:  

-   Implementação de cliente iniciada  

-   Implementação de cliente concluída com êxito  

-   Atribuição de cliente iniciada  

-   Atribuição de cliente com êxito  

Os computadores que não pode ser instalado ou que atribuir o cliente do Configuration Manager enviam mensagens de estado adicionais.  

Por exemplo, se implementar o cliente do Configuration Manager em 20.000 computadores, a implementação poderá enviar 80.000 mensagens de estado para o ponto de estado de contingência. Porque a configuração de limitação predefinida permite 10.000 mensagens de estado para ser enviada para o ponto de estado de contingência a cada 3.600 segundos (1 hora), mensagens de estado podem ficar pendentes no ponto de estado de contingência. Tem também de considerar a largura de banda de rede disponível entre o ponto de estado de contingência e o servidor do site e a capacidade de processamento do servidor do site para processar muitas mensagens de estado.  

Para ajudar a evitar estes problemas, considere um aumento no número de mensagens de estado e uma redução no intervalo de limitação.  

Reponha os valores de limitação para o ponto de estado de contingência, se uma das seguintes condições for verdadeira:  

-   Calcular a que os valores de limitação atuais são superiores ao necessário para processar mensagens de estado do ponto de estado de contingência.  

-   Acha que as definições de limitação atuais criam utilização elevada da CPU no servidor do site.  

Não altere as definições para as definições de limitação do ponto de estado de contingência, a menos que compreenda as consequências. Por exemplo, quando aumenta as definições de limitação para um valor elevado, a utilização da CPU no servidor do site pode aumentar para um valor elevado, que operações mais lentas todos os sites.  


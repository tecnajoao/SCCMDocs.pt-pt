---
title: "Planear a segurança no System Center Configuration Manager | Documentos do Microsoft"
description: "Obter melhores práticas e outras informações sobre a segurança no System Center Configuration Manager."
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
caps.latest.revision: 6
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 6145cb69c69dba1eb1b9842079ee1a33686bb18a
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="plan-for-security-in-system-center-configuration-manager"></a>Planear a segurança no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

##  <a name="BKMK_PlanningForCertificates"></a>Planear certificados (autoassinados e PKI)  
 O Configuration Manager utiliza uma combinação de certificados autoassinados e certificados de infraestrutura de chaves públicas (PKI).  

 Como melhor prática de segurança, utilize certificados PKI sempre que possível. Para mais informações sobre os requisitos dos certificados PKI, consulte o artigo [requisitos de certificados PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md). Quando Configuration Manager pedidos de certificados PKI, tal como durante a inscrição de dispositivos móveis e o aprovisionamento de Intel Active Management Technology (AMT), tem de utilizar serviços de domínio do Active Directory e uma autoridade de certificação empresarial. Para todos os outros certificados PKI, tem de implementar e geri-los de forma independente do Configuration Manager.  

 Certificados PKI também são necessários quando os computadores cliente ligam a sistemas de sites baseados na Internet, e é recomendado que utilize certificados PKI quando os clientes ligam aos sistemas de sites que executam os serviços de informação Internet (IIS). Para mais informações sobre a comunicação do cliente, consulte o artigo [como configurar as portas de comunicação de clientes no System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

 Quando utiliza PKI, pode utilizar também IPsec para ajudar a proteger as comunicações servidor-servidor entre sistemas de sites num site, entre sites e para outra transferência de dados entre computadores. Implementação de IPsec é independente do Configuration Manager.  

 O Configuration Manager pode gerar automaticamente certificados autoassinados quando não estão disponíveis certificados PKI e alguns certificados no Configuration Manager são sempre autoassinados. Na maioria dos casos, o Configuration Manager gere automaticamente os certificados autoassinados e não tem qualquer ação adicional. Uma exceção possível é o certificado de assinatura do servidor do site. O certificado de assinatura do servidor do site é sempre autoassinado e assegura que as políticas de cliente que os clientes transferem a partir do ponto de gestão foram enviadas pelo servidor do site e que não foram adulteradas.  

### <a name="plan-for-the-site-server-signing-certificate-self-signed"></a>Planear sites assinatura do certificado do servidor (autoassinado)  
 Os clientes em segurança podem obter uma cópia do certificado de assinatura do servidor de site a partir de serviços de domínio do Active Directory e da instalação push do cliente. Se os clientes não é possível obter uma cópia do certificado de assinatura do servidor de site por um destes mecanismos, como procedimento recomendado de segurança, instale uma cópia do certificado de assinatura do servidor de site quando instalar o cliente. Isto é especialmente importante se a primeira comunicação do cliente com o site é a partir da Internet, dado que o ponto de gestão está ligado a uma rede não fidedigna e, por isso, vulnerável a ataques. Se não efetuar este passo adicional, os clientes transferirão automaticamente uma cópia do certificado de assinatura do servidor do site a partir do ponto de gestão.  

 Os cenários de quando os clientes não é possível obter com segurança uma cópia do certificado de servidor do site incluem o seguinte:  

-   O cliente não é instalado utilizando a instalação push de cliente e qualquer uma das seguintes condições é verdadeira:  

    -   Esquema do Active Directory não estiver expandido para o Configuration Manager.  

    -   O site do cliente não está publicado para serviços de domínio do Active Directory.  

    -   O cliente pertence a uma floresta ou um grupo de trabalho não fidedigno.  

-   O cliente é instalado quando está na Internet.  

##### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>Para instalar clientes com uma cópia do certificado de assinatura do servidor do site  

1.  Localize o certificado de assinatura de servidor de site no servidor de site primário do cliente. O certificado é armazenado no **SMS** arquivo de certificados e tem o nome do requerente **servidor do Site** e o nome amigável, **certificado de assinatura do servidor do Site**.  

2.  Exporte o certificado sem a chave privada, guarde o ficheiro de forma segura e aceda ao mesmo apenas a partir de um canal protegido, por exemplo, utilizando a assinatura de bloco de mensagem de servidor (SMB) ou IPsec.  

3.  Instalar o cliente utilizando a propriedade de Client. msi, **SMSSIGNCERT =***&lt;nome completo do ficheiro e caminho\>*, com CCMSetup.exe.  

###  <a name="BKMK_PlanningForCRLs"></a>Planear a revogação de certificados PKI  
Quando utilizar certificados PKI com o Configuration Manager, planeie como e quando os clientes e servidores irão utilizar uma lista de revogação de certificados (CRL) para confirmar o certificado no computador que efetuar a ligação. A CRL é um ficheiro que cria uma autoridade de certificação (AC) e sinais e tem uma lista dos certificados de que a AC emitidos mas revogados. Um administrador de AC pode revogar certificados, por exemplo, se um certificado emitido está saiba ou suspeite ficar comprometida.  

> [!IMPORTANT]  
>  Como a localização da CRL é adicionada a um certificado quando problemas de uma AC, certifique-se de que planeia da CRL antes de implementar quaisquer certificados PKI que irá utilizar o Configuration Manager.  

Por predefinição, IIS verifica sempre a existência de certificados de cliente na CRL e não é possível alterar esta configuração no Configuration Manager. Por predefinição, os clientes do Configuration Manager verificam sempre a existência de sistemas de sites na CRL. Pode desativar esta definição especificando uma propriedade de site e especificando uma propriedade de CCMSetup. Quando gere computadores baseados em Intel AMT fora de banda, também pode ativar a verificação CRL para o ponto de serviço fora de banda e para computadores que executam a consola de gestão fora de banda.  

Computadores que utilizam a verificação de revogação de certificados, mas não é possível localizar a CRL, comportar-se como se todos os certificados na cadeia de certificação estivessem revogados, uma vez que não é possível verificar as respetivas ausência da lista. Neste cenário, todas as ligações que necessitem de certificados e utilizem uma CRL falharão.  

A verificação da CRL sempre que é utilizado um certificado oferece mais segurança contra a utilização de um certificado revogado, mas provoca um atraso de ligação e processamento adicional no cliente. Esta verificação de segurança adicional é mais necessária quando os clientes se encontram na Internet ou numa rede não fidedigna.  

Consulte os seus administradores PKI antes de decidir se clientes do Configuration Manager tem de verificar a CRL e, em seguida, considere manter esta opção ativada no Configuration Manager quando as duas condições seguintes forem verdadeiras:  

-   A sua infraestrutura PKI suporta uma CRL e esta está publicada onde todos os clientes do Configuration Manager possam localizar. Lembre-se de que estes poderão incluir clientes na Internet, se estiver a utilizar a gestão de clientes baseados na Internet, e clientes em florestas não fidedignas.  

-   O requisito de verificação da CRL em cada ligação a um sistema de sites que está configurado para utilizar um certificado PKI é maior do que o requisito de ligações mais rápidas, processamento eficientes no cliente e o risco dos clientes não conseguirem ligar a servidores se não conseguirem localizar a CRL.  

###  <a name="BKMK_PlanningForRootCAs"></a>Planear o PKI fidedignos certificados e a lista de emissores de certificados de raiz  
Se os sistemas de sites do IIS utilizarem certificados PKI de cliente para autenticação de clientes por HTTP ou autenticação e encriptação de clientes por HTTPS, poderá ter de importar certificados de AC de raiz como uma propriedade de site. Aqui estão os dois cenários:  

-   Implementar sistemas operativos utilizando o Gestor de configuração e os pontos de gestão só aceitam ligações de cliente HTTPS.  

-   Utiliza certificados PKI de cliente que não encadeiam num certificado de autoridade de certificação (AC) de raiz considerado fidedigno pelos pontos de gestão.  

    > [!NOTE]  
    >  Quando emite certificados PKI de cliente a partir da mesma hierarquia de AC que emite os certificados de servidor utilizados para os pontos de gestão, não é necessário especificar este certificado de AC de raiz. No entanto, se utilizar várias hierarquias de AC e não tiver a certeza se são mutuamente fidedignas, importe a AC de raiz para a hierarquia de AC dos clientes.  

Se tiver de importar certificados de AC de raiz para o Configuration Manager, exporte-os partir da AC emissora ou do computador cliente. Se exportar o certificado a partir da AC emissora e esta também for a AC de raiz, certifique-se de que a chave privada não é exportada. Armazene o ficheiro de certificado exportado numa localização segura para impedir a adulteração. Tem de ser capaz de aceder ao ficheiro quando configurar o site. Se aceder ao ficheiro através da rede, certifique-se de que a comunicação é protegida contra adulteração utilizando a assinatura SMB ou IPsec.  

Se qualquer certificado de AC de raiz que importar for renovado, terá de importar o certificado renovado.  

Estes certificados de AC de raiz importados e o certificado de AC de raiz de cada ponto de gestão criam a lista de emissores de certificados que utilizam computadores do Configuration Manager da seguinte forma:  

-   Quando os clientes ligam a pontos de gestão, o ponto de gestão verifica se o certificado de cliente encadeia numa raiz fidedigna certificado na lista de emissores de certificados do site. Caso não encadeie, o certificado é rejeitado e a ligação PKI falha.  

-   Quando os clientes selecionam um certificado PKI e tem uma lista de emissores de certificados, selecionarão um certificado de cliente que encadeie num certificado de raiz fidedigna na lista de emissores de certificados. Se não existir nenhuma correspondência, o cliente não selecionará um certificado PKI. Para mais informações sobre o processo de certificado de cliente, consulte o [planear a seleção de certificado PKI de cliente](#BKMK_PlanningForClientCertificateSelection) secção neste artigo.  

Independentemente da configuração do site, também poderá ter de importar um certificado de AC de raiz quando inscrever dispositivos móveis, inscrever computadores Mac e configurar os computadores baseados em Intel AMT para redes sem fios.  

###  <a name="BKMK_PlanningForClientCertificateSelection"></a>Planear a seleção de certificado PKI de cliente  
 Se os sistemas de sites do IIS utilizarem certificados PKI de cliente para autenticação de cliente por HTTP ou de autenticação de cliente e encriptação por HTTPS, planeie como clientes Windows irão selecionar o certificado a utilizar para o Configuration Manager.  

> [!NOTE]  
>  Alguns dispositivos não suportam um método de seleção de certificado. Em vez disso, selecionarão automaticamente o primeiro certificado que satisfaz os requisitos de certificado. Por exemplo, os clientes em computadores Mac e dispositivos móveis não suportam um método de seleção de certificado.  

Em muitos casos, a configuração e o comportamento predefinidos serão suficientes. O cliente do Configuration Manager em computadores Windows filtra vários certificados utilizando estes critérios pela seguinte ordem:  

1.  A lista de emissores de certificados: O certificado encadeia numa AC que seja considerada fidedigna pelo ponto de gestão de raiz.  

2.  O certificado está no arquivo de certificados predefinido **Pessoal**.  

3.  O certificado é válido, não foi revogado e não expirou. A verificação da validade verifica que a chave privada é acessível e que o certificado não foi criado com um modelo de certificado de versão 3, que não é compatível com o Configuration Manager.  

4.  O certificado tem capacidade de autenticação de cliente ou foi emitido para o nome do computador.  

5.  O certificado tem o período de validade mais longo.  

Os clientes podem ser configurados para utilizar a lista de emissores de certificados com os seguintes mecanismos:  

-   Está publicada como informações de site do Configuration Manager para serviços de domínio do Active Directory.  

-   Os clientes são instalados utilizando a instalação push de cliente.  

-   Os clientes transferem-na a partir do ponto de gestão depois de atribuídos com êxito ao respetivo site.  

-   É especificada durante a instalação de cliente como uma propriedade de Client. msi do CCMSetup de CCMCERTISSUERS.  

Os clientes que não tiverem a lista de emissores de certificados quando forem instalados pela primeira vez e ainda não estiverem atribuídos ao site ignorar esta verificação. Quando os clientes tiverem a lista de emissores de certificados e não tiverem um certificado PKI de cliente que encadeie num certificado de raiz fidedigna na lista de emissores de certificados, seleção de certificado falhará, e os clientes não avançarão com os restantes critérios de seleção de certificado.  

Na maioria dos casos, o cliente do Configuration Manager identifica corretamente um certificado PKI exclusivo e adequado. No entanto, quando não for este o caso, em vez de selecionar o certificado com base na capacidade de autenticação de cliente, pode configurar dois métodos de seleção alternativos:  

-   Uma correspondência parcial no nome de Requerente do certificado de cliente. Esta é uma correspondência não sensível a maiúsculas e minúsculas adequada se estiver a utilizar o nome de domínio completamente qualificado (FQDN) de um computador no campo do requerente e pretender que a seleção de certificado seja baseada no sufixo de domínio, por exemplo **contoso.com**. No entanto, pode utilizar este método de seleção para identificar qualquer cadeia de carateres sequenciais no nome de Requerente do certificado que o diferencie de outros no arquivo de certificados do cliente.  

    > [!NOTE]  
    >  Não é possível utilizar a correspondência de cadeia parcial com o nome alternativo do requerente (SAN) como definição do site. Apesar de ser possível especificar uma correspondência de cadeia parcial para o SAN utilizando o CCMSetup, esta será substituída pelas propriedades do site nos cenários seguintes:  
    >   
    >  -   Os clientes obtém informações do site que estão publicadas nos Serviços de Domínio do Active Directory.  
    > -   Os clientes são instalados utilizando a instalação push do cliente.  
    >   
    >  Utilize uma correspondência parcial de cadeia no SAN apenas quando instalar clientes manualmente e quando estes não obterem informações do site a partir de serviços de domínio do Active Directory. Por exemplo, estas condições aplicam-se a clientes apenas de Internet.  

-   Uma correspondência nos valores do atributo do nome do requerente do certificado do cliente ou nos valores do atributo do nome alternativo do requerente (SAN). Esta é uma correspondência de maiúsculas e minúsculas adequada se estiver a utilizar um X500 nome único X500 ou identificadores de objetos equivalentes (OIDs) em conformidade com RFC 3280 e pretende que a seleção de certificado se baseie nos valores do atributo. É possível especificar apenas os atributos e os respetivos valores necessários para identificar ou validar exclusivamente o certificado e distinguir o certificado de outros num arquivo de certificados.  

A tabela seguinte mostra os valores de atributo que o Configuration Manager suporta para os critérios de seleção de certificado de cliente.  

|Atributo OID|Atributo de nome único|Definição do atributo|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Componente do domínio|  
|1.2.840.113549.1.9.1|E ou E-mail|Endereço de e-mail|  
|2.5.4.3|CN|Nome comum|  
|2.5.4.4|SN|Nome do requerente|  
|2.5.4.5|SERIALNUMBER|Número de série|  
|2.5.4.6|C|Código de país|  
|2.5.4.7|L|Localidade|  
|2.5.4.8|S ou ST|Nome do estado ou distrito|  
|2.5.4.9|STREET|Morada|  
|2.5.4.10|O|Nome da organização|  
|2.5.4.11|OU|Unidade organizacional|  
|2.5.4.12|T ou Title|Título|  
|2.5.4.42|G ou GN ou GivenName|Nome próprio|  
|2.5.4.43|I ou Initials|Iniciais|  
|2.5.29.17|(sem valor)|Nome Alternativo do Requerente|  

Se forem localizados mais do que um certificado apropriado após os critérios de seleção, é possível substituir a configuração predefinida para selecionar o certificado que tenha o período de validade mais longo e em vez disso, especificar que não está selecionado nenhum certificado. Neste cenário, o cliente não poderá ser capaz de comunicar com sistemas de sites do IIS com um certificado PKI. O cliente envia uma mensagem de erro ao respetivo ponto de estado de contingência atribuído para alerta de falha na seleção do certificado para que possam alterar ou refinar os seus critérios de seleção de certificado. Em seguida, o comportamento do cliente depende se a falha de ligação falha através de HTTPS ou HTTP:  

-   Se a falha de ligação Ocorreu através de HTTPS: O cliente tentará ligar através de HTTP e utiliza o certificado autoatribuído do cliente.  

-   Se a falha de ligação Ocorreu através de HTTP: O cliente tenta estabelecer novamente a ligação através de HTTP utilizando o certificado de cliente autoatribuído.  

Para ajudar a identificar um certificado de cliente PKI único, também pode especificar um arquivo personalizado, diferente da predefinição de **pessoal** no **computador** armazenar. No entanto, tem de criar este arquivo independentemente do Configuration Manager e deve estar preparado para implementar certificados neste arquivo personalizado e renová-los antes de expira o período de validade.  

Para obter informações sobre como configurar as definições para certificados de cliente, consulte o [configurar as definições para certificados PKI de cliente](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) secção a [configurar a segurança no System Center Configuration Manager](../../../core/plan-design/security/configure-security.md) artigo.  

###  <a name="BKMK_PlanningForPKITransition"></a>Planear uma estratégia de transição para certificados PKI e gestão de clientes baseados na Internet  
As opções de configuração flexíveis no Configuration Manager permitem-lhe gradualmente transição de clientes e o site para utilizar certificados PKI para ajudar a pontos finais de cliente segura. Certificados PKI proporcionam uma maior segurança e permitem-lhe gerir os clientes de Internet.  

Devido ao número de opções de configuração e opções no Configuration Manager, não existe nenhuma forma única de transição de um site para que todos os clientes utilizem ligações HTTPS. No entanto, pode seguir estes passos como orientação:  

1.  Instalar o site do Configuration Manager e configurá-lo para que os sistemas de sites aceitam ligações de cliente através de HTTPS e HTTP.  

2.  Configurar o **comunicação com o computador cliente** separador nas propriedades do site para que o **definições do sistema de Site** é **HTTP ou HTTPS**e selecione **certificado de cliente PKI de utilização (capacidade de autenticação de cliente) se estiver disponível**.  Para obter mais informações, consulte o [configurar definições para certificados PKI de cliente](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) secção a [configurar a segurança no System Center Configuration Manager](../../../core/plan-design/security/configure-security.md) artigo.  

3.  Efetue uma implementação PKI para os certificados de cliente. Para um exemplo de implementação, consulte o *implementar o cliente certificado para computadores com o Windows* secção a [exemplo passo a passo de implementação de PKI certificados para o System Center Configuration Manager: Autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates) artigo.  

4.  Instale clientes utilizando o método de instalação push do cliente. Para obter mais informações, consulte o [como instalar clientes do Configuration Manager utilizando a emissão de cliente](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush) secção a [como implementar clientes em computadores com Windows no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md) artigo.  

5.  Monitorizar a implementação do cliente e o estado utilizando os relatórios e as informações na consola do Configuration Manager.  

6.  Verifique quantos clientes estão a utilizar um certificado PKI de cliente visualizando a coluna **Certificado de Cliente** na área de trabalho **Ativos e Compatibilidade** , nó **Dispositivos** .  

     Também é possível implementar a ferramenta de avaliação de preparação do Configuration Manager HTTPS (**cmHttpsReadiness.exe**) em computadores e utilizar os relatórios para ver como quantos computadores podem utilizar uma PKI de cliente de certificado com o Configuration Manager.  

    > [!NOTE]  
    >  Quando o cliente do Configuration Manager está instalado, o **cmHttpsReadiness.exe** ferramenta é instalada no *% windir %***\ccm.** pasta. Quando executa esta ferramenta em clientes, é possível especificar as seguintes opções:  
    >   
    >  -   / Arquivo:&lt;nome\>  
    > -   / Emissores:&lt;lista\>  
    > -   / Critérios:&lt;critérios\>  
    > -   /SelectFirstCert  
    >   
    >  Estas opções mapeiam as propriedades Client.msi **CCMCERTSTORE**, **CCMCERTISSUERS**, **CCMCERTSEL**, e **CCMFIRSTCERT** , respetivamente. Para mais informações sobre estas opções, consulte o artigo [acerca das propriedades de instalação de cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

7.  Quando tem a certeza de que suficiente clientes estão a utilizar o respetivo certificado PKI de cliente para autenticação através de HTTP, siga estes passos:  

    1.  Implemente um certificado de servidor Web PKI para um servidor membro que vai executar um ponto de gestão adicional para o site e configurar esse certificado no IIS. Para obter mais informações, consulte o *implementar o certificado de servidor Web para sistemas de sites que executam o IIS* secção a [exemplo passo a passo de implementação de PKI certificados para o System Center Configuration Manager: Autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates) artigo.  

    2.  Instale a função do ponto de gestão neste servidor e configure a opção **Ligações de cliente** nas propriedades do ponto de gestão para **HTTPS**.  

8.  Monitorize e certifique-se de que os clientes que tenham um certificado PKI utilizam o novo ponto de gestão utilizando HTTPS. É possível utilizar contadores de registo ou desempenho do IIS para verificar isto.  

9. Reconfigure as outras funções do sistema de site para utilizar ligações de cliente HTTPS. Se pretender gerir clientes na Internet, certifique-se de que os sistemas de sites possuem um FQDN de Internet e configure os pontos de gestão e os pontos de distribuição individuais para aceitarem ligações de cliente a partir da Internet.  

    > [!IMPORTANT]  
    >  Antes de configurar funções do sistema de sites para aceitar ligações a partir da Internet, reveja as informações de planeamento e a pré-requisitos para gestão de clientes baseados na Internet. Para obter mais informações, consulte o artigo [as comunicações entre os pontos finais no System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

10. Expanda a implementação do certificado PKI para clientes e sistemas de sites que executam o IIS e configure as funções de sistema de sites para ligações de cliente HTTPS e ligações de Internet, conforme necessário.  

11. Para garantir a máxima segurança: Se tiver a certeza de que todos os clientes estão a utilizar um certificado PKI de cliente para autenticação e encriptação, altere as propriedades de site para utilizar apenas HTTPS.  

 Se seguir este plano para introduzir gradualmente os certificados PKI, primeiro para autenticação apenas por HTTP e, em seguida, para autenticação e encriptação por HTTPS, reduz o risco dos clientes se tornarem não geridos. Além disso, beneficia da mais elevada segurança que suporte do Configuration Manager.  

##  <a name="BKMK_PlanningForRTK"></a>Planear a chave de raiz fidedigna  
Fidedigna do Configuration Manager a chave de raiz fornece um mecanismo para clientes do Configuration Manager verificar que os sistemas de sites pertencem à respetiva hierarquia. Cada servidor de site gera uma chave de troca de site para comunicar com outros sites. A chave de troca de site do site de nível superior na hierarquia chama-se chave de raiz fidedigna.  

A função da chave de raiz fidedigna no Configuration Manager for parecido com um certificado de raiz numa infraestrutura de chave pública na qual que nada assinado pela chave privada da chave de raiz fidedigna é fidedigno descendente da hierarquia. Por exemplo, assinando o certificado de ponto de gestão com a chave privada de raiz fidedigna do par de chaves e fazendo uma cópia da chave pública do par de chaves de raiz fidedigna disponíveis para os clientes, possível os clientes diferenciarem entre os pontos de gestão que existem na respetiva hierarquia e pontos de gestão que não existem na respetiva hierarquia. Os clientes utilizam o Windows Management Instrumentation (WMI) para armazenar uma cópia da chave de raiz fidedigna no **root\ccm\locationservices** espaço de nomes.  

É possível os clientes obterem automaticamente a cópia pública da chave de raiz fidedigna através de dois mecanismos:  

-   Esquema do Active Directory é expandido para o Configuration Manager, o site esteja publicado nos serviços de domínio do Active e os clientes podem obter estas informações do site a partir de um servidor de catálogo global.  

-   Os clientes são instalados utilizando a instalação push de cliente.  

Se não for possível os clientes obterem a chave de raiz fidedigna através de um destes mecanismos, os clientes confiam na chave de raiz fidedigna que é fornecida pelo primeiro ponto de gestão com o qual comunicam. Neste cenário, um cliente poderia ser redirecionado para o ponto de gestão de um atacante onde receberia política do ponto de gestão de adesão. Provavelmente, esta seria a ação de um atacante sofisticado e a sua ocorrência seria possível apenas por um período de tempo limitado antes de o cliente obter a chave de raiz fidedigna de um ponto de gestão válido. No entanto, para reduzir o risco de um atacante redirecionar clientes para um ponto de gestão não autorizado, pode aprovisionar previamente os clientes com a chave de raiz fidedigna.  

Utilize os seguintes procedimentos para pré-aprovisionar e verificar a chave de raiz fidedigna para um cliente do Configuration Manager:  

-   Pré-Aprovisione um cliente com a chave de raiz fidedigna utilizando um ficheiro.  

-   Pré-Aprovisione um cliente com a chave de raiz fidedigna sem utilizar um ficheiro.  

-   Verifique a chave de raiz fidedigna num cliente.  

> [!NOTE]  
>  Não é necessário pré-aprovisionar um cliente utilizando a chave de raiz fidedigna se que podem obtê-lo a partir de serviços de domínio do Active Directory ou são instalados utilizando push de cliente. Além disso, não é necessário pré-aprovisionar os clientes se estes utilizarem a comunicação por HTTPS para pontos de gestão porque confiança é estabelecida pela certificados PKI.  

Pode remover a chave de raiz fidedigna de um cliente utilizando a propriedade de Client. msi, **RESETKEYINFORMATION = TRUE**, com CCMSetup.exe. Para substituir a chave de raiz fidedigna, reinstale o cliente em conjunto com a nova chave de raiz fidedigna, por exemplo, utilizando a instalação push do cliente ou especificando a propriedade Client.msi **SMSPublicRootKey** através do CCMSetup.exe.  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a>Para pré-aprovisionar um cliente com a chave de raiz fidedigna utilizando um ficheiro  

1.  No editor de texto, abra o ficheiro,  *&lt;directory do Configuration Manager\>***\bin\mobileclient.tcf**.  

2.  Localize a entrada **SMSPublicRootKey =**, copie a chave dessa linha e feche o ficheiro sem guardar alterações.  

3.  Criar um novo ficheiro de texto e cole as informações da chave que copiou do ficheiro mobileclient.  

4.  Guarde o ficheiro e coloque-o numa localização onde todos os computadores possam aceder, mas onde o ficheiro esteja protegido para impedir a adulteração.  

5.  Instalar o cliente utilizando um método de instalação que aceite propriedades Client. msi e especifique a propriedade de Client. msi, **SMSROOTKEYPATH =***&lt;nome completo do ficheiro e caminho\>*.  

    > [!IMPORTANT]  
    >  Quando especificar a chave de raiz fidedigna para segurança adicional durante a instalação do cliente, também tem de especificar o código do site utilizando a propriedade de Client. msi, **SMSSITECODE =&lt;código do site\>**.  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a>Para pré-aprovisionar um cliente com a chave de raiz fidedigna sem utilizar um ficheiro  

1.  No editor de texto, abra o ficheiro,  *&lt;directory do Configuration Manager\>***\bin\mobileclient.tcf**.  

2.  Localize a entrada, SMSPublicRootKey =, tenha em atenção a chave dessa linha ou copiá-lo para a área de transferência e, em seguida, feche o ficheiro sem guardar alterações.  

3.  Instalar o cliente utilizando um método de instalação que aceite propriedades Client. msi e especifique a propriedade de Client. msi, **SMSPublicRootKey =***&lt;chave\>*, onde  *&lt;chave\>*  é a cadeia que copiou de mobileclient.  

    > [!IMPORTANT]  
    >  Quando especificar a chave de raiz fidedigna para segurança adicional durante a instalação do cliente, também tem de especificar o código do site utilizando a propriedade de Client. msi, **SMSSITECODE =&lt;código do site\>**.  

#### <a name="to-verify-the-trusted-root-key-on-a-client"></a>Para verificar a chave de raiz fidedigna num cliente  

1.  No **iniciar** menu, selecione **executar**e, em seguida, introduza **Wbemtest**.  

2.  No **recurso de teste do Windows Management Instrumentation** diálogo caixa, selecione **ligar**.  

3.  No **ligar** caixa de diálogo a **espaço de nomes** caixa, introduza **root\ccm\locationservices**e, em seguida, escolha **ligar**.  

4.  No **recurso de teste do Windows Management Instrumentation** caixa de diálogo a **IWbemServices** secção, escolha **Enum Classes**.  

5.  No **informações sobre a superclasse** diálogo caixa, selecione **recursiva**e, em seguida, escolha **OK**.  

6.  Na janela **Resultados da Consulta** , desloque até ao final da lista e depois faça duplo clique em **TrustedRootKey ()**.  

7.  No **editor de objetos TrustedRootKey** diálogo caixa, selecione **instâncias**.  

8.  Na nova **resultado da consulta** janela que mostra as instâncias de **TrustedRootKey**, faça duplo clique **TrustedRootKey = @**.  

9. No **editor de objetos TrustedRootKey = @** caixa de diálogo a **propriedades** secção, desloque para baixo para **TrustedRootKey CIM_STRING**. A cadeia na coluna da direita é a chave de raiz fidedigna. Certifique-se de que corresponde a **SMSPublicRootKey** valor no ficheiro,  *&lt;directory do Configuration Manager\>***\bin\mobileclient.tcf**.  

##  <a name="BKMK_PlanningForSigningEncryption"></a>Planear a assinatura e encriptação  
 Quando utiliza certificados PKI para todas as comunicações de cliente, não é necessário planear a assinatura e encriptação para ajudar a proteger a comunicação de dados de cliente. No entanto, se configurar sistemas de sites que executam o IIS para permitir ligações de cliente HTTP, tem de decidir como ajudar a proteger a comunicação de cliente para o site.  

 Para ajudar a proteger os dados que os clientes enviam para os pontos de gestão, é possível requerer dados sejam assinados. Além disso, é possível requerer que todos os dados assinados de clientes que utilizam HTTP sejam assinados utilizando o algoritmo SHA-256. Embora esta definição seja mais segura, não ative esta opção a não ser que todos os clientes suportem SHA-256. Muitos sistemas operativos suportam SHA-256 nativamente, mas os sistemas operativos mais antigos poderão necessitar de uma atualização ou correção. Por exemplo, os computadores com o Windows Server 2003 SP2 têm de instalar uma correção que é mencionada no [artigo KB 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666).  

 Enquanto a assinatura ajuda a proteger os dados contra adulteração, a encriptação ajuda a proteger os dados contra a divulgação de informações. Pode ativar a encriptação 3DES para os dados de inventário e as mensagens de estado que os clientes enviam para os pontos de gestão do site. Não é necessário instalar qualquer atualização nos clientes para suportarem esta opção, mas tenha em atenção a utilização adicional da CPU que será necessária nos clientes e o ponto de gestão para efetuar a encriptação e desencriptação.  

 Para mais informações sobre como configurar as definições para assinatura e encriptação, consulte o [configurar a assinatura e encriptação](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption) secção a [configurar a segurança no System Center Configuration Manager](../../../core/plan-design/security/configure-security.md) artigo.  

##  <a name="BKMK_PlanningForRBA"></a>Planear a administração baseada em funções  
 Para obter estas informações, consulte o artigo [Noções básicas da administração baseada em funções para o System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md).  

### <a name="see-also"></a>Consulte também
[Referência técnica controlos criptográficos para o System Center Configuration Manager](../../../protect/deploy-use/cryptographic-controls-technical-reference.md).  


---
title: "Planear a segurança"
titleSuffix: Configuration Manager
description: "Obter as melhores práticas e outras informações sobre a segurança no System Center Configuration Manager."
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
caps.latest.revision: "6"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 8f63d1b762b296cb6b6aa56480a5cddf7a3249dc
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="plan-for-security-in-system-center-configuration-manager"></a>Planear a segurança no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

##  <a name="BKMK_PlanningForCertificates"></a>Planear certificados (autoassinados e PKI)  
 O Configuration Manager utiliza uma combinação de certificados autoassinados e certificados de infraestrutura de chaves públicas (PKI).  

 Como melhor prática de segurança, utilize certificados PKI sempre que possível. Para mais informações sobre requisitos de certificado PKI, consulte [requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md). Quando o Configuration Manager pedidos de certificados PKI, tal como durante a inscrição de dispositivos móveis e o aprovisionamento do Intel Active Management Technology (AMT), tem de utilizar serviços de domínio do Active Directory e uma autoridade de certificação empresarial. Para todos os outros certificados PKI, tem de implementar e geri-los de forma independente do Configuration Manager.  

 Certificados PKI também são necessários quando os computadores cliente se ligar a sistemas de sites baseados na Internet e recomendamos que utilize certificados PKI quando os clientes ligam aos sistemas de sites que executam os serviços de informação Internet (IIS). Para obter mais informações sobre a comunicação de cliente, consulte [como configurar portas de comunicação de cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

 Quando utilizar uma PKI, também pode utilizar IPsec para ajudar a proteger a comunicação de servidor para servidor entre sistemas de sites num site, entre locais e para outra transferência de dados entre computadores. Implementação de IPsec não é independente do Configuration Manager.  

 O Configuration Manager pode gerar automaticamente certificados autoassinados quando não estão disponíveis certificados PKI e alguns certificados no Configuration Manager são sempre autoassinados. Na maioria dos casos, o Configuration Manager gere automaticamente os certificados autoassinados e não precisa de tomar medidas adicionais. Uma exceção possível é o certificado de assinatura do servidor do site. O certificado de assinatura do servidor do site é sempre autoassinado e assegura que as políticas de cliente que os clientes transferem a partir do ponto de gestão foram enviadas pelo servidor do site e que não foram adulteradas.  

### <a name="plan-for-the-site-server-signing-certificate-self-signed"></a>Planear o servidor certificado de assinatura site (autoassinado)  
 Os clientes em segurança podem obter uma cópia do certificado de assinatura do servidor de site do Active Directory Domain Services e da instalação push do cliente. Se os clientes não é possível obter uma cópia do certificado de assinatura do servidor de site por um destes mecanismos, como melhor prática de segurança, instale uma cópia do certificado de assinatura do servidor de site quando instala o cliente. Isto é especialmente importante se comunicação primeiro do cliente com o site é a partir da Internet, porque o ponto de gestão está ligado a uma rede não fidedigna e, por isso, vulnerável a ataques. Se não efetuar este passo adicional, os clientes transferirão automaticamente uma cópia do certificado de assinatura do servidor do site a partir do ponto de gestão.  

 Cenários de quando os clientes de forma segura não é possível obter uma cópia do certificado de servidor de site incluem o seguinte:  

-   O cliente não é instalado utilizando a instalação push de cliente e qualquer uma das seguintes condições é verdadeira:  

    -   O esquema do Active Directory não estiver expandido para o Configuration Manager.  

    -   O site do cliente não está publicado para serviços de domínio do Active Directory.  

    -   O cliente pertence a uma floresta ou um grupo de trabalho não fidedigno.  

-   O cliente é instalado quando está na Internet.  

##### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>Para instalar clientes com uma cópia do certificado de assinatura do servidor do site  

1.  Localize o certificado de assinatura de servidor de site no servidor de site primário do cliente. O certificado é armazenado no **SMS** arquivo de certificados e tem o nome do requerente **servidor do Site** e o nome amigável, **certificado de assinatura do servidor do Site**.  

2.  Exportar o certificado sem a chave privada, guarde o ficheiro de forma segura e aceder ao mesmo apenas a partir de um canal protegido, por exemplo, utilizando a assinatura do bloco de mensagem de servidor (SMB) ou IPsec.  

3.  Instalar o cliente utilizando a propriedade de Client.msi **SMSSIGNCERT =***&lt;nome de ficheiro e caminho completo\>*, com o CCMSetup.exe.  

###  <a name="BKMK_PlanningForCRLs"></a>Plano de revogação de certificados PKI  
Quando utiliza certificados PKI com o Configuration Manager, planeie como e quando os clientes e servidores irão utilizar uma lista de revogação de certificados (CRL) para verificar o certificado no computador de ligação. A CRL é um ficheiro que cria uma autoridade de certificação (AC) e inicia e tem uma lista de certificados de AC tem de ser emitido mas revogado. Um administrador de AC pode revogar certificados, por exemplo, se um certificado emitido está saiba ou suspeite ficar comprometida.  

> [!IMPORTANT]  
>  Como a localização da CRL é adicionada a um certificado quando uma AC emite-lo, certifique-se de que planeia a CRL antes de implementar quaisquer certificados PKI que irá utilizar o Configuration Manager.  

Por predefinição, o IIS verifica sempre a CRL para certificados de cliente, e não é possível alterar esta configuração no Configuration Manager. Por predefinição, clientes do Configuration Manager sempre a existência de sistemas de sites na CRL. Pode desativar esta definição especificando uma propriedade de site e especificando uma propriedade de CCMSetup. Quando gerir computadores baseados em Intel AMT fora de banda, também pode ativar a verificação CRL para o ponto de serviço fora de banda e para computadores que executam a consola de gestão fora de banda.  

Computadores que utilizam a verificação de revogação do certificado, mas não é possível localizar a CRL, comportar-se como se todos os certificados na cadeia de certificação estivessem revogados, porque não é possível verificar a sua ausência da lista. Neste cenário, todas as ligações que necessitem de certificados e utilizem uma CRL falharão.  

A verificação da CRL sempre que é utilizado um certificado oferece mais segurança contra a utilização de um certificado revogado, mas provoca um atraso de ligação e processamento adicional no cliente. Esta verificação de segurança adicional é mais necessária quando os clientes se encontram na Internet ou numa rede não fidedigna.  

Consulte os seus administradores PKI antes de decidir se clientes do Configuration Manager tem de verificar a CRL e, em seguida, considere manter esta opção ativada no Configuration Manager quando ambas as condições seguintes forem verdadeiras:  

-   A sua infraestrutura PKI suporta uma CRL e esta está publicada onde todos os clientes do Configuration Manager possam localizar. Lembre-se de que estes poderão incluir clientes na Internet, se estiver a utilizar a gestão de clientes baseados na Internet, e clientes em florestas não fidedignas.  

-   O requisito de verificação da CRL para cada ligação a um sistema de sites que está configurado para utilizar um certificado PKI é maior do que o requisito de ligações mais rápidas, processamento eficientes no cliente e o risco dos clientes não conseguirem ligar a servidores se não conseguirem localizar a CRL.  

###  <a name="BKMK_PlanningForRootCAs"></a>Planear a PKI fidedigno certificados e a lista de emissores de certificados de raiz  
Se os sistemas de sites do IIS utilizarem certificados PKI de cliente para autenticação de clientes por HTTP ou autenticação e encriptação de clientes por HTTPS, poderá ter de importar certificados de AC de raiz como uma propriedade de site. Seguem-se os dois cenários:  

-   Implementar sistemas operativos utilizando o Gestor de configuração e os pontos de gestão só aceitam ligações de cliente HTTPS.  

-   Utiliza certificados PKI de cliente que não encadeiam num certificado de autoridade de certificação (AC) de raiz considerado fidedigno pelos pontos de gestão.  

    > [!NOTE]  
    >  Quando emite certificados PKI de cliente a partir da mesma hierarquia de AC que emite os certificados de servidor utilizados para os pontos de gestão, não é necessário especificar este certificado de AC de raiz. No entanto, se utilizar várias hierarquias de AC e tem a não certeza se eles confiam uns nos outros, importe a AC de raiz para a hierarquia de AC dos clientes.  

Se tiver de importar certificados de AC de raiz para o Configuration Manager, exportá-las a partir da AC emissora ou do computador cliente. Se exportar o certificado a partir da AC emissora e esta também for a AC de raiz, certifique-se de que a chave privada não é exportada. Armazene o ficheiro de certificado exportado numa localização segura para impedir a adulteração. Tem de ser capazes de aceder ao ficheiro quando configurar o site. Se aceder ao ficheiro através da rede, certifique-se de que a comunicação é protegida contra adulteração utilizando a assinatura SMB ou IPsec.  

Se qualquer certificado da AC de raiz que importar for renovado, terá de importar o certificado renovado.  

Estes certificados de AC de raiz importados e o certificado de AC de raiz de cada ponto de gestão criam a lista de emissores de certificados que utilizam computadores do Configuration Manager das seguintes formas:  

-   Quando os clientes ligam a pontos de gestão, o ponto de gestão verifica que o certificado de cliente encadeia a uma raiz fidedigna de certificados na lista de emissores de certificados do site. Caso não encadeie, o certificado é rejeitado e a ligação PKI falha.  

-   Quando os clientes selecionam um certificado PKI e tem uma lista de emissores de certificados, selecionarão um certificado de cliente que encadeie num certificado de raiz fidedigna na lista de emissores de certificados. Se não existir nenhuma correspondência, o cliente não selecionará um certificado PKI. Para obter mais informações sobre o processo de certificado de cliente, consulte o [planear a seleção de certificado de cliente PKI](#BKMK_PlanningForClientCertificateSelection) secção deste artigo.  

Independentemente da configuração do site, também poderá ter de importar um certificado de AC de raiz quando inscrever dispositivos móveis, inscrever computadores Mac e configurar computadores baseados em Intel AMT para redes sem fios.  

###  <a name="BKMK_PlanningForClientCertificateSelection"></a>Planear a seleção de certificado de cliente PKI  
 Se os sistemas de site do IIS utilizar certificados PKI de cliente para autenticação de cliente de encriptação e autenticação de cliente por HTTP ou através de HTTPS, planeie como clientes do Windows irão selecionar o certificado a utilizar para o Configuration Manager.  

> [!NOTE]  
>  Alguns dispositivos não suportam um método de seleção de certificado. Em vez disso, se selecionarem automaticamente o primeiro certificado que satisfaz os requisitos de certificado. Por exemplo, os clientes em computadores Mac e dispositivos móveis não suportam um método de seleção de certificado.  

Em muitos casos, a configuração e o comportamento predefinidos serão suficientes. O cliente do Configuration Manager em computadores Windows filtra vários certificados utilizando estes critérios pela seguinte ordem:  

1.  A lista de emissores de certificados: O certificado encadeie a uma AC de raiz que seja considerada fidedigna pelo ponto de gestão.  

2.  O certificado está no arquivo de certificados predefinido **Pessoal**.  

3.  O certificado é válido, não foi revogado e não expirou. A verificação da validade verifica que a chave privada é acessível e que o certificado não foi criado com um modelo de certificado de versão 3, que não é compatível com o Configuration Manager.  

4.  O certificado tem capacidade de autenticação de cliente ou foi emitido para o nome do computador.  

5.  O certificado tem o período de validade mais longo.  

Os clientes podem ser configurados para utilizar a lista de emissores de certificados com os seguintes mecanismos:  

-   Está publicada como informações de site do Configuration Manager para serviços de domínio do Active Directory.  

-   Os clientes são instalados utilizando a instalação push de cliente.  

-   Os clientes transferem-na a partir do ponto de gestão depois de atribuídos com êxito ao respetivo site.  

-   É especificada durante a instalação de cliente como uma propriedade de client.msi do CCMSetup de CCMCERTISSUERS.  

Clientes que não têm a lista de emissores de certificados quando são instalados pela primeira vez e ainda não estão atribuídos ao site ignorar esta verificação. Quando os clientes tiverem a lista de emissores de certificados e é necessário um certificado PKI que encadeie a um certificado de raiz fidedigna na lista de emissores de certificados, seleção de certificado falhará e os clientes não avançarão com os outros critérios de seleção de certificado.  

Na maioria dos casos, o cliente do Configuration Manager identifica corretamente um certificado PKI exclusivo e adequado. No entanto, quando este é não as maiúsculas e minúsculas, em vez de selecionar o certificado com base na capacidade de autenticação de cliente, que pode configurar dois métodos de seleção alternativos:  

-   Uma correspondência parcial no nome de Requerente do certificado de cliente. Esta é uma correspondência não sensível a maiúsculas e minúsculas adequada se estiver a utilizar o nome de domínio completamente qualificado (FQDN) de um computador no campo do requerente e pretender que a seleção de certificado seja baseada no sufixo de domínio, por exemplo **contoso.com**. No entanto, pode utilizar este método de seleção para identificar qualquer cadeia de carateres sequenciais no nome de Requerente do certificado que o diferencie de outros no arquivo de certificados do cliente.  

    > [!NOTE]  
    >  Não é possível utilizar a correspondência de cadeia parcial com o nome alternativo do requerente (SAN) como definição do site. Apesar de ser possível especificar uma correspondência de cadeia parcial para o SAN utilizando o CCMSetup, esta será substituída pelas propriedades do site nos cenários seguintes:  
    >   
    >  -   Os clientes obtém informações do site que estão publicadas nos Serviços de Domínio do Active Directory.  
    > -   Os clientes são instalados utilizando a instalação push do cliente.  
    >   
    >  Utilize uma correspondência parcial de cadeia no SAN apenas quando instalar clientes manualmente e quando estes não obterem informações do site do Active Directory Domain Services. Por exemplo, estas condições aplicam-se a clientes apenas de Internet.  

-   Uma correspondência nos valores do atributo do nome do requerente do certificado do cliente ou nos valores do atributo do nome alternativo do requerente (SAN). Esta é uma correspondência de maiúsculas e minúsculas adequada se estiver a utilizar um X500 único nome, ou equivalente identificadores de objetos (OIDs) em conformidade com RFC 3280 e pretende que a seleção de certificado com base nos valores do atributo. É possível especificar apenas os atributos e os respetivos valores necessários para identificar ou validar exclusivamente o certificado e distinguir o certificado de outros num arquivo de certificados.  

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

Se encontra-se mais do que um certificado apropriado após os critérios de seleção, pode substituir a configuração predefinida para selecionar o certificado com o período de validade mais longo e, em vez disso, especificar que não está selecionado nenhum certificado. Neste cenário, o cliente não poderá comunicar com sistemas de sites do IIS com um certificado PKI. O cliente envia uma mensagem de erro para o respetivo ponto de estado de contingência atribuído para alerta de falha de seleção de certificado para que possa alterar ou refinar os critérios de seleção de certificado. Em seguida, o comportamento do cliente depende se a falha de ligação falha através de HTTPS ou HTTP:  

-   Se a falha de ligação Ocorreu através de HTTPS: O cliente tenta ligar através de HTTP e utiliza o certificado autoassinado do cliente.  

-   Se a falha de ligação Ocorreu através de HTTP: O cliente tenta estabelecer novamente a ligação através de HTTP utilizando o certificado autoassinado do cliente.  

Para ajudar a identificar um certificado de cliente PKI único, também pode especificar um arquivo personalizado, diferente da predefinição de **pessoais** no **computador** armazenar. No entanto, tem de criar este arquivo independentemente do Configuration Manager e tem de poder implementar certificados neste arquivo personalizado e renová-los antes do período de validade.  

Para obter informações sobre como configurar as definições para certificados de cliente, consulte o [configurar definições para certificados PKI de cliente](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) secção o [configurar a segurança no System Center Configuration Manager](../../../core/plan-design/security/configure-security.md) artigo.  

###  <a name="BKMK_PlanningForPKITransition"></a>Planear uma estratégia de transição para certificados PKI e gestão de clientes baseados na Internet  
As opções de configuração flexíveis no Configuration Manager permitem-lhe gradualmente transição de clientes e o site para utilizar certificados PKI para ajudar a pontos finais de cliente seguras. Os certificados PKI proporcionam uma maior segurança e permitem-lhe gerir os clientes de Internet.  

Devido ao número de opções de configuração e de escolhas no Configuration Manager, não há nenhuma única forma de transição de um site, para que todos os clientes utilizem ligações HTTPS. No entanto, pode seguir estes passos como orientação:  

1.  Instalar o site do Configuration Manager e configure-o para que os sistemas de sites aceitam ligações de cliente através de HTTPS e HTTP.  

2.  Configurar o **comunicação com o computador cliente** separador nas propriedades do site, por isso, o **definições do sistema de Site** é **HTTP ou HTTPS**e selecione **certificado de cliente PKI de utilização (capacidade de autenticação de cliente) se estiver disponível**.  Para obter mais informações, consulte o [configurar definições para certificados PKI de cliente](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) secção o [configurar a segurança no System Center Configuration Manager](../../../core/plan-design/security/configure-security.md) artigo.  

3.  Efetue uma implementação PKI para os certificados de cliente. Para um exemplo de implementação, consulte o *implementar o cliente certificados para computadores com o Windows* secção o [exemplo passo a passo de implementação da PKI certificados para o System Center Configuration Manager: Autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates) artigo.  

4.  Instale clientes utilizando o método de instalação push do cliente. Para obter mais informações, consulte o [como instalar clientes do Configuration Manager utilizando a emissão de cliente](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush) secção o [como implementar clientes em computadores Windows no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md) artigo.  

5.  Monitorizar a implementação do cliente e o estado utilizando os relatórios e as informações na consola do Configuration Manager.  

6.  Verifique quantos clientes estão a utilizar um certificado PKI de cliente visualizando a coluna **Certificado de Cliente** na área de trabalho **Ativos e Compatibilidade** , nó **Dispositivos** .  

     Também pode implementar a ferramenta de avaliação de preparação do HTTPS do Configuration Manager (**cmHttpsReadiness.exe**) em computadores e utilizar os relatórios para verificar quantos computadores podem utilizar um PKI de cliente de certificado com o Configuration Manager.  

    > [!NOTE]  
    >  Quando o cliente do Configuration Manager está instalado, o **cmHttpsReadiness.exe** ferramenta está instalada no *% windir %***\ccm.** pasta. Quando executa esta ferramenta em clientes, é possível especificar as seguintes opções:  
    >   
    >  -   / Arquivo:&lt;nome\>  
    > -   / Emissores:&lt;lista\>  
    > -   / Critérios:&lt;critérios\>  
    > -   /SelectFirstCert  
    >   
    >  Estas opções mapeiam as propriedades Client.msi **CCMCERTSTORE**, **CCMCERTISSUERS**, **CCMCERTSEL**, e **CCMFIRSTCERT** , respetivamente. Para obter mais informações sobre estas opções, consulte [acerca das propriedades de instalação de cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

7.  Quando tiver a certeza de que suficiente clientes são com êxito utilizando o respetivo certificado PKI de cliente para autenticação através de HTTP, siga estes passos:  

    1.  Implemente um certificado de servidor Web PKI para um servidor membro que vai executar um ponto de gestão adicional para o site e configurar esse certificado no IIS. Para obter mais informações, consulte o *implementar o certificado de servidor Web para sistemas de sites que executam o IIS* secção o [exemplo passo a passo de implementação da PKI certificados para o System Center Configuration Manager: Autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates) artigo.  

    2.  Instale a função do ponto de gestão neste servidor e configure a opção **Ligações de cliente** nas propriedades do ponto de gestão para **HTTPS**.  

8.  Monitorize e certifique-se de que os clientes que tenham um certificado PKI utilizam o novo ponto de gestão utilizando HTTPS. É possível utilizar contadores de registo ou desempenho do IIS para verificar isto.  

9. Reconfigure as outras funções do sistema de site para utilizar ligações de cliente HTTPS. Se pretender gerir clientes na Internet, certifique-se de que os sistemas de sites possuem um FQDN de Internet e configure os pontos de gestão e os pontos de distribuição individuais para aceitarem ligações de cliente a partir da Internet.  

    > [!IMPORTANT]  
    >  Antes de configurar funções de sistema de sites para aceitar ligações a partir da Internet, reveja as informações de planeamento e os pré-requisitos para a gestão de clientes baseada na Internet. Para obter mais informações, consulte [comunicações entre pontos finais no System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

10. Expanda a implementação do certificado PKI para clientes e sistemas de sites que executam o IIS e configurar as funções de sistema de sites para ligações de cliente HTTPS e ligações de Internet, conforme necessário.  

11. Para máxima segurança: Quando tiver a certeza de que todos os clientes estão a utilizar um certificado PKI de cliente para autenticação e encriptação, altere as propriedades de site para utilizar apenas HTTPS.  

 Quando seguir este plano para introduzir gradualmente os certificados PKI, primeiro para autenticação apenas por HTTP e, em seguida, para autenticação e encriptação através de HTTPS, reduz o risco de que os clientes deixarão de ser geridos. Além disso, beneficia da mais elevada segurança que suporte do Configuration Manager.  

##  <a name="BKMK_PlanningForRTK"></a>Plano para a chave de raiz fidedigna  
Fidedigna do Configuration Manager a chave de raiz fornece um mecanismo para clientes do Configuration Manager verificar que os sistemas de sites pertencem à respetiva hierarquia. Cada servidor de site gera uma chave de troca de site para comunicar com outros sites. A chave de troca de site do site de nível superior na hierarquia chama-se chave de raiz fidedigna.  

A função da chave de raiz fidedigna no Configuration Manager assemelha-se um certificado de raiz numa infraestrutura de chave pública em que algo assinado pela chave privada da chave de raiz fidedigna é fidedigno a hierarquia. Por exemplo, ao inscrever o certificado de ponto de gestão com a chave privada do par de chaves de raiz fidedigna e fazendo uma cópia da chave pública do par de chaves de raiz fidedigna disponíveis para os clientes, possível os clientes diferenciarem entre os pontos de gestão que estão na respetiva hierarquia e pontos de gestão que não estão na respetiva hierarquia. Os clientes utilizam o Windows Management Instrumentation (WMI) para armazenar uma cópia da chave de raiz fidedigna no **root\ccm\locationservices** espaço de nomes.  

É possível os clientes obterem automaticamente a cópia pública da chave de raiz fidedigna através de dois mecanismos:  

-   O esquema do Active Directory é expandido para o Configuration Manager, o site é publicado para serviços de domínio do Active Directory e os clientes podem obter estas informações de site a partir de um servidor de catálogo global.  

-   Os clientes são instalados utilizando a instalação push de cliente.  

Se não for possível os clientes obterem a chave de raiz fidedigna através de um destes mecanismos, os clientes confiam na chave de raiz fidedigna que é fornecida pelo primeiro ponto de gestão com o qual comunicam. Neste cenário, um cliente poderia ser redirecionado para o ponto de gestão de um atacante onde receberia política partir do ponto de gestão não autorizado. Provavelmente, esta seria a ação de um atacante sofisticado e a sua ocorrência seria possível apenas por um período de tempo limitado antes de o cliente obter a chave de raiz fidedigna de um ponto de gestão válido. No entanto, para reduzir este risco de um atacante direcionar clientes para um ponto de gestão não autorizado, é possível pré-aprovisionar os clientes com a chave de raiz fidedigna.  

Utilize os seguintes procedimentos para pré-aprovisionar e verificar a chave de raiz fidedigna para um cliente de Configuration Manager:  

-   Pré-Aprovisione um cliente com a chave de raiz fidedigna utilizando um ficheiro.  

-   Pré-Aprovisione um cliente com a chave de raiz fidedigna sem utilizar um ficheiro.  

-   Verifique a chave de raiz fidedigna num cliente.  

> [!NOTE]  
>  Não é necessário pré-aprovisionar um cliente utilizando a chave de raiz fidedigna, se, podem obter este do serviços de domínio do Active Directory ou são instalados utilizando push de cliente. Além disso, não é necessário pré-aprovisionar os clientes ao utilizarem a comunicação por HTTPS para pontos de gestão porque a confiança é estabelecida pela certificados PKI.  

Pode remover a chave de raiz fidedigna a partir de um cliente utilizando a propriedade de Client.msi **RESETKEYINFORMATION = TRUE**, com o CCMSetup.exe. Para substituir a chave de raiz fidedigna, reinstale o cliente em conjunto com a nova chave de raiz fidedigna, por exemplo, utilizando a instalação push do cliente ou especificando a propriedade Client.msi **SMSPublicRootKey** através do CCMSetup.exe.  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a>Para pré-aprovisionar um cliente com a chave de raiz fidedigna utilizando um ficheiro  

1.  Num editor de texto, abra o ficheiro,  *&lt;diretório do Configuration Manager\>***\bin\mobileclient.tcf**.  

2.  Localize a entrada, **SMSPublicRootKey =**, copie a chave dessa linha e feche o ficheiro sem quaisquer alterações.  

3.  Criar um novo ficheiro de texto e cole as informações da chave que copiou do ficheiro mobileclient.tcf.  

4.  Guarde o ficheiro e coloque-o numa localização onde todos os computadores podem aceder ao mesmo, mas onde o ficheiro está protegido para impedir a adulteração.  

5.  Instalar o cliente utilizando um método de instalação que aceite propriedades Client.msi e especifique a propriedade de Client.msi **SMSROOTKEYPATH =***&lt;nome de ficheiro e caminho completo\>*.  

    > [!IMPORTANT]  
    >  Quando especificar a chave de raiz fidedigna para segurança adicional durante a instalação de cliente, também tem de especificar o código do site utilizando a propriedade de Client.msi **SMSSITECODE =&lt;código do site\>**.  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a>Para pré-aprovisionar um cliente com a chave de raiz fidedigna sem utilizar um ficheiro  

1.  Num editor de texto, abra o ficheiro,  *&lt;diretório do Configuration Manager\>***\bin\mobileclient.tcf**.  

2.  Localize a entrada, SMSPublicRootKey =, anote a chave dessa linha ou copie-a para a área de transferência e, em seguida, feche o ficheiro sem quaisquer alterações.  

3.  Instalar o cliente utilizando um método de instalação que aceite propriedades Client.msi e especifique a propriedade de Client.msi **SMSPublicRootKey =***&lt;chave\>*, onde  *&lt;chave\>*  é a cadeia que copiou de mobileclient.tcf.  

    > [!IMPORTANT]  
    >  Quando especificar a chave de raiz fidedigna para segurança adicional durante a instalação de cliente, também tem de especificar o código do site utilizando a propriedade de Client.msi **SMSSITECODE =&lt;código do site\>**.  

#### <a name="to-verify-the-trusted-root-key-on-a-client"></a>Para verificar a chave de raiz fidedigna num cliente  

1.  No **iniciar** menu, escolha **executar**e, em seguida, introduza **Wbemtest**.  

2.  No **o recurso de teste do Windows Management Instrumentation** diálogo caixa, escolha **Connect**.  

3.  No **Connect** caixa de diálogo a **espaço de nomes** box, introduza **root\ccm\locationservices**e, em seguida, escolha **Connect**.  

4.  No **o recurso de teste do Windows Management Instrumentation** caixa de diálogo a **IWbemServices** secção, escolha **Enum Classes**.  

5.  No **informações sobre a superclasse** diálogo caixa, escolha **recursiva**e, em seguida, escolha **OK**.  

6.  Na janela **Resultados da Consulta** , desloque até ao final da lista e depois faça duplo clique em **TrustedRootKey ()**.  

7.  No **editor de objetos TrustedRootKey** diálogo caixa, escolha **instâncias**.  

8.  Na nova **resultado da consulta** janela que apresenta as instâncias de **TrustedRootKey**, faça duplo clique em **TrustedRootKey = @**.  

9. No **editor de objetos TrustedRootKey = @** caixa de diálogo a **propriedades** secção, desloque para baixo até **TrustedRootKey CIM_STRING**. A cadeia na coluna da direita é a chave de raiz fidedigna. Certifique-se de que corresponde à **SMSPublicRootKey** valor no ficheiro,  *&lt;diretório do Configuration Manager\>***\bin\mobileclient.tcf**.  

##  <a name="BKMK_PlanningForSigningEncryption"></a>Plano para assinatura e encriptação  
 Quando utiliza certificados PKI para todas as comunicações de cliente, não é necessário planear a assinatura e encriptação para ajudar a proteger a comunicação de dados de cliente. No entanto, se configurar sistemas de sites que executam o IIS para permitir ligações de cliente HTTP, tem de decidir como ajudar a proteger a comunicação de cliente para o site.  

 Para ajudar a proteger os dados que os clientes enviam para os pontos de gestão, pode solicitar dados sejam assinados. Além disso, é possível requerer que todos os dados assinados de clientes que utilizam HTTP sejam assinados utilizando o algoritmo SHA-256. Embora esta definição seja mais segura, não ative esta opção a não ser que todos os clientes suportem SHA-256. Muitos sistemas operativos suportam SHA-256 nativamente, mas os sistemas operativos mais antigos poderão necessitar de uma atualização ou correção. Por exemplo, os computadores com o Windows Server 2003 SP2 têm de instalar uma correção que é mencionada no [artigo KB 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666).  

 Enquanto a assinatura ajuda a proteger os dados contra adulteração, a encriptação ajuda a proteger os dados contra a divulgação de informações. Pode ativar a encriptação 3DES para os dados de inventário e as mensagens de estado que os clientes enviam para os pontos de gestão do site. Não é necessário instalar quaisquer atualizações nos clientes para suportarem esta opção, mas tenha em atenção a utilização da CPU adicional, que será necessária nos clientes e o ponto de gestão para efetuar a encriptação e desencriptação.  

 Para obter mais informações sobre como configurar as definições de assinatura e encriptação, consulte o [configurar assinatura e encriptação](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption) secção o [configurar a segurança no System Center Configuration Manager](../../../core/plan-design/security/configure-security.md) artigo.  

##  <a name="BKMK_PlanningForRBA"></a>Planear a administração baseada em funções  
 Para obter estas informações, consulte [Noções básicas da administração baseada em funções para o System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md).  

### <a name="see-also"></a>Consulte também
[Referência técnica de controlos criptográficos para o System Center Configuration Manager](../../../protect/deploy-use/cryptographic-controls-technical-reference.md).  

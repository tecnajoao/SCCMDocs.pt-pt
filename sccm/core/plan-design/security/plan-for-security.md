---
title: Planear a segurança de
titleSuffix: Configuration Manager
description: Obter as melhores práticas e outras informações sobre a segurança no Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 237a21346665af404850276b12b0f1ca32fc5f6e
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54250821"
---
# <a name="plan-for-security-in-configuration-manager"></a>Planear a segurança no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo descreve os conceitos que deve considerar quando planear a segurança com a implementação do Configuration Manager. Ele inclui as secções seguintes:  

- [Planear certificados (autoassinados e PKI)](#BKMK_PlanningForCertificates)  
    - [Criptografia: Certificados de próxima geração (CNG)](#bkmk_plan-cng)  
    - [HTTP avançado](#bkmk_plan-ehttp)  
    - [Certificados do CMG e CDP](#bkmk_plan-cmgcdp)  
    - [O servidor do site (autoassinado) do certificado de assinatura](#bkmk_plansitesign)  
    - [Revogação de certificados PKI](#BKMK_PlanningForCRLs)  
    - [Os certificados de raiz fidedigna de PKI e os emissores de certificados](#BKMK_PlanningForRootCAs)  
    - [Seleção de certificado de cliente PKI](#BKMK_PlanningForClientCertificateSelection)  
    - [Uma estratégia de transição para certificados PKI e gestão de clientes baseados na internet](#BKMK_PlanningForPKITransition)  

- [Plano para a chave de raiz fidedigna](#BKMK_PlanningForRTK)  

- [Plano para assinatura e encriptação](#BKMK_PlanningForSigningEncryption)  

- [Planear a administração baseada em funções](#BKMK_PlanningForRBA)  

- [Plano para o Azure Active Directory](#bkmk_planazuread)  

- [Plano para a autenticação de fornecedor de SMS](#bkmk_auth)



##  <a name="BKMK_PlanningForCertificates"></a> Planear certificados (autoassinados e PKI)  

 O Configuration Manager utiliza uma combinação de certificados autoassinados e certificados de infraestrutura de chaves públicas (PKI).  

 Utilize certificados PKI sempre que possível. Para obter mais informações, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements). Quando o Configuration Manager solicita certificados PKI durante a inscrição de dispositivos móveis, tem de utilizar os serviços de domínio do Active Directory e uma autoridade de certificação empresarial. Para todos os outros certificados PKI, implementar e geri-los forma independente do Configuration Manager. 

 Certificados PKI são necessários quando computadores cliente ligam aos sistemas de sites baseados na internet. Alguns cenários com o gateway de gestão na cloud e o ponto de distribuição de nuvem também necessitam de certificados PKI. Para obter mais informações, consulte [gerir clientes na internet](/sccm/core/clients/manage/manage-clients-internet).

 Quando utilizar uma PKI, também pode usar IPsec para ajudar a proteger a comunicação de servidor-para-servidor entre sistemas de sites num site, entre sites e outras transferências de dados entre computadores. Implementação do IPsec é independente do Configuration Manager.  

 Quando os certificados PKI não estão disponíveis, o Configuration Manager gera automaticamente certificados autoassinados. Alguns certificados no Configuration Manager são sempre autoassinados. Na maioria dos casos, o Configuration Manager gere automaticamente os certificados autoassinados e não precisa de tomar medidas adicionais. Um exemplo é o certificado de assinatura do servidor de site. Este certificado é sempre autoassinado. Torna-se de que as políticas que os clientes transferem a partir do ponto de gestão foram enviadas pelo servidor do site e não foram adulteradas.  


### <a name="bkmk_plan-cng"></a> Criptografia: Certificados de próxima geração (CNG)  

 O Configuration Manager suporta Cryptography: Próxima certificados de geração (CNG). Clientes do Configuration Manager podem utilizar o certificado de autenticação de cliente PKI com chave privada no fornecedor de armazenamento de chaves do CNG (KSP). Com o suporte KSP, clientes do Configuration Manager suportam a chave de privada baseada em hardware, como o KSP de TPM para certificados de autenticação de cliente PKI. Para obter mais informações, consulte [descrição geral de certificados CNG](/sccm/core/plan-design/network/cng-certificates-overview).


### <a name="bkmk_plan-ehttp"></a> HTTP avançado  

 Através de HTTPS communication é recomendada para todos os caminhos de comunicação do Configuration Manager, mas é difícil para alguns clientes devido à sobrecarga de gerenciamento de certificados PKI. A introdução do Azure Active Directory integration (Azure AD) reduz alguns, mas nem todos os requisitos de certificado. A partir da versão 1806, pode habilitar o site para utilizar **avançada HTTP**. Esta configuração suporta HTTPS nos sistemas de sites utilizando uma combinação de certificados autoassinados e o Azure AD. Ele não requer o PKI. Para obter mais informações, consulte [avançada HTTP](/sccm/core/plan-design/hierarchy/enhanced-http).  


### <a name="bkmk_plan-cmgcdp"></a> Certificados do CMG e CDP

Gestão de clientes na internet através do gateway de gestão na cloud (CMG) e do ponto de distribuição em nuvem (CDP) requer a utilização de certificados. O número e tipo de certificados varia de acordo com seus cenários específicos. Para obter mais informações, veja os artigos seguintes:
- [Certificados para o gateway de gestão da nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)  
- [Certificados para o ponto de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_certs)  


### <a name="bkmk_plansitesign"></a> Plano para o certificado assinatura de servidor de site (autoassinado)  

 Os clientes com segurança podem obter uma cópia do certificado de assinatura do servidor de site de serviços de domínio do Active Directory e de instalação push do cliente. Se os clientes não é possível obter uma cópia deste certificado por um destes mecanismos, instale-o ao instalar o cliente. Este processo é especialmente importante se a comunicação de primeiro o cliente com o site está com um ponto de gestão baseado na internet. Uma vez que este servidor está ligado à rede não fidedigna, é mais vulnerável a ataques. Se não efetuar este passo adicional, os clientes transferirão automaticamente uma cópia do certificado de assinatura do servidor de site do ponto de gestão.  

 Clientes de forma segura não é possível obter uma cópia do certificado de servidor de site nos seguintes cenários:  

 - Não instale o cliente utilizando a instalação push do cliente, e:  

    - Ainda não tiver expandido o esquema do Active Directory para o Configuration Manager.  

    - Ainda não o publicou o site do cliente para serviços de domínio do Active Directory.  

    - O cliente pertence a uma floresta ou um grupo de trabalho não fidedigno.  

 - Estiver a utilizar gestão de clientes baseados na internet e instalar o cliente quando estiver na internet.  

#### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>Para instalar clientes com uma cópia do certificado de assinatura do servidor do site  

1.  Localize o certificado no servidor do site primário de assinatura do servidor de site. O certificado é armazenado no **SMS** loja do Windows de certificado. Ele tem o nome do requerente **servidor do Site** e o nome amigável, **certificado de assinatura do servidor do Site**.  

2.  Exportar o certificado sem a chave privada, guarde o ficheiro de forma segura e acessá-lo apenas a partir de um canal protegido.  

3.  Instale o cliente, utilizando a propriedade de Client. msi seguintes: `SMSSIGNCERT=<full path and file name>`  


###  <a name="BKMK_PlanningForCRLs"></a> Plano de revogação de certificados PKI  

Quando utiliza certificados PKI com o Configuration Manager, planear a utilização de uma lista de revogação de certificados (CRL). Dispositivos utilizam a CRL para verificar o certificado no computador de ligação. A CRL é um ficheiro que uma autoridade de certificação (AC) cria e inicia sessão. Ele tem uma lista de certificados de AC emitidos, mas revogados. Quando um administrador de certificado revoga os certificados, a sua impressão digital é adicionada à CRL. Por exemplo, se um certificado emitido é saiba ou suspeite que ser comprometidos.

> [!IMPORTANT]  
>  Uma vez que a localização da CRL é adicionada a um certificado quando a ser emitido por uma AC, certifique-se de que planeia a CRL antes de implementar quaisquer certificados PKI utilizadas pelo Configuration Manager.  

IIS verifica sempre a CRL para certificados de cliente e não é possível alterar esta configuração no Configuration Manager. Por predefinição, os clientes do Configuration Manager sempre verificação da CRL em sistemas de sites. Desative esta definição especificando uma propriedade de site e especificando uma propriedade de CCMSetup.  

Computadores que utilizam a verificação de revogação de certificado, mas não é possível localizar a CRL se comporte como se todos os certificados na cadeia de certificação são revogados. Este comportamento é que eles não é possível verificar se os certificados estão na lista de revogação de certificados. Neste cenário, todas as ligações falharem que necessitam de certificados e incluir a verificação CRL. Ao validar o seu CRL está acessível ao navegar para a localização de http, é importante observar que o cliente do Configuration Manager é executado como sistema LOCAL. Por conseguinte, o teste de acessibilidade CRL com um navegador da web em execução no contexto de utilizador podem ter êxito, no entanto a conta de computador pode estar bloqueada quando a tentativa de estabelecer uma ligação http para o mesmo URL de CRL devido a web interno filtragem de solução. O URL de CRL em qualquer filtragem de soluções de web de lista de permissões pode ser necessária nessa situação.

A verificação da CRL sempre que é utilizado um certificado oferece mais segurança contra a utilização de um certificado que foi revogado. Embora ele introduz um atraso de ligação e o processamento adicional no cliente. Sua organização poderá exigir esta verificação de segurança adicionais para os clientes na internet ou numa rede não fidedigna.  

Consulte os administradores de PKI antes de decidir se os clientes do Configuration Manager tem de verificar a CRL. Em seguida, considere manter esta opção ativada no Configuration Manager quando ambas as condições seguintes forem verdadeiras:  

-   Sua infraestrutura PKI suporta uma CRL e esta está publicada onde todos os clientes do Configuration Manager possam localizar. Estes clientes podem incluir dispositivos na internet e aqueles em florestas não fidedignas.  

-   O requisito de verificação da CRL para cada ligação a um sistema de sites que está configurado para utilizar um certificado PKI é maior do que os seguintes requisitos:  
    - Ligações mais rápidas  
    - Processamento eficiente no cliente  
    - O risco dos clientes não conseguirem ligar a servidores se não conseguirem localizar a CRL  


###  <a name="BKMK_PlanningForRootCAs"></a> Planear para o PKI fidedigno certificados e a lista de emissores de certificados de raiz  

Se seus sistemas de site do IIS utilizarem certificados PKI de cliente para autenticação de cliente através de HTTP, ou para autenticação de cliente e encriptação através de HTTPS, poderá ter de importar certificados de AC de raiz como uma propriedade de site. Seguem-se os dois cenários:  

-   Implementar sistemas operativos utilizando o Gestor de configuração e os pontos de gestão só aceitam ligações de cliente HTTPS.  

-   Utilize certificados PKI de cliente que não encadeiam num certificado de raiz que a gestão de pontos de confiança.  

    > [!NOTE]  
    >  Quando o cliente, emitir certificados PKI da mesma hierarquia de AC que emite os certificados de servidor que utiliza para pontos de gestão, não tem de especificar este certificado de AC de raiz. No entanto, se utilizar várias hierarquias de AC e não tiver a certeza se são mutuamente fidedignas, importe a AC de raiz para a hierarquia de AC dos clientes.  

Se tiver de importar os certificados de AC de raiz para o Configuration Manager, exportá-las a partir da AC emissora ou de um computador cliente. Se exportar o certificado da AC emissora, que também é a AC de raiz, certifique-se de que não exportar a chave privada. Store o ficheiro de certificado exportado numa localização segura para impedir a adulteração. Precisa de acesso para o ficheiro quando configurar o site. Se aceder ao ficheiro através da rede, certifique-se de que a comunicação é protegida contra adulteração utilizando o IPsec.  

Se qualquer certificado de AC de raiz que importar for renovado, tem de importar o certificado renovado.  

Estes certificados de AC de raiz importados e o certificado de AC de raiz de cada ponto de gestão criar a lista de emissores de certificados que utilizam do Configuration Manager computadores das seguintes formas:  

-   Quando os clientes ligam a pontos de gestão, verifica se o ponto de gestão que o certificado de cliente seja ligado a um certificado de raiz fidedigna na lista de emissores de certificados do site. Se não, o certificado é rejeitado e a ligação PKI falha.  

-   Quando os clientes selecionam um certificado PKI e tem uma lista de emissores de certificados, selecionarão um certificado cliente que encadeie num certificado de raiz fidedigna na lista de emissores de certificados. Se não houver nenhuma correspondência, o cliente não selecionar um certificado PKI. Para obter mais informações, consulte [planear a seleção de certificado de cliente PKI](#BKMK_PlanningForClientCertificateSelection).  


###  <a name="BKMK_PlanningForClientCertificateSelection"></a> Planear a seleção de certificado de cliente PKI  

 Se seus sistemas de site do IIS utilizarem certificados PKI de cliente para autenticação de cliente por HTTP ou para autenticação de cliente e encriptação através de HTTPS, planeie como clientes de Windows selecionam o certificado a utilizar para o Configuration Manager.  

> [!NOTE]  
>  Alguns dispositivos não suportam um método de seleção de certificado. Em vez disso, eles selecionarem automaticamente o primeiro certificado que satisfaz os requisitos de certificado. Por exemplo, os clientes em computadores Mac e dispositivos móveis não suportam um método de seleção de certificado.  

Em muitos casos, a configuração predefinida e o comportamento é suficiente. O cliente do Configuration Manager em computadores Windows filtra vários certificados utilizando estes critérios pela seguinte ordem:  

1.  A lista de emissores de certificados: O certificado encadeia numa AC que seja considerada fidedigna pelo ponto de gestão de raiz.  

2.  O certificado está no arquivo de certificados predefinido **Pessoal**.  

3.  O certificado é válido, não foi revogado e não expirou. A verificação da validade também verifica que a chave privada está acessível.  

4.  O certificado tem capacidade de autenticação de cliente ou foi emitido para o nome do computador.  

5.  O certificado tem o período de validade mais longo.  

Configure clientes para utilizar a lista de emissores de certificados utilizando os seguintes mecanismos:  

-   Publique-o com informações de site do Configuration Manager para serviços de domínio do Active Directory.  

-   Instale clientes utilizando a instalação push do cliente.  

-   Os clientes transferem-a partir do ponto de gestão depois que estiverem atribuídos com êxito para o respetivo site.  

-   Especificá-lo durante a instalação de cliente como uma propriedade de Client. msi do CCMSetup de CCMCERTISSUERS.  

Clientes que não têm a lista de emissores de certificados quando estiver instalados pela primeira vez e ainda não estão atribuídos ao site ignorar esta verificação. Quando os clientes tiverem a lista de emissores de certificados e não tem uma PKI de cliente que encadeie num certificado de raiz fidedigna na lista de emissores de certificados de certificado, a seleção de certificado falhará. Os clientes não continuam com os outros critérios de seleção de certificado.  

Na maioria dos casos, o cliente do Configuration Manager identifica corretamente um certificado PKI exclusivo e adequado. No entanto, quando esse comportamento não é o caso, em vez de selecionar o certificado com base na capacidade de autenticação de cliente, pode configurar dois métodos de seleção alternativos:  

- Uma correspondência de cadeia parcial no nome de requerente do certificado de cliente. Esse método é uma correspondência de maiúsculas e minúsculas. É apropriado se estiver a utilizar o nome de domínio completamente qualificado (FQDN) de um computador no campo do requerente e pretender que a seleção de certificado seja baseada no sufixo de domínio, por exemplo **contoso.com**. No entanto, pode utilizar este método de seleção para identificar qualquer cadeia de carateres sequenciais no nome do requerente do certificado que diferencia o certificado de outros no arquivo de certificados de cliente.  

  > [!NOTE]
  >  Não é possível utilizar a correspondência de cadeia parcial com o nome alternativo do requerente (SAN) como uma definição de site. Embora possa especificar uma correspondência de cadeia parcial para o SAN utilizando o CCMSetup, esta vai ser substituída por propriedades de sites nos seguintes cenários:  
  > 
  > - Os clientes obterem informações do site que são publicadas para serviços de domínio do Active Directory.  
  >   -   Os clientes são instalados utilizando a instalação push do cliente.  
  > 
  >   Utilize uma correspondência de cadeia parcial na SAN, apenas quando instalar clientes manualmente e quando eles não obter informações a partir de serviços de domínio do Active Directory. Por exemplo, estas condições aplicam-se a clientes apenas na internet.  

- Uma correspondência em valores de atributo de nome de requerente de certificado de cliente ou os valores de atributo do requerente (SAN) de nome alternativo. Esse método é uma correspondência de maiúsculas e minúsculas. É adequado se estiver a utilizar um X500 único nome ou identificadores de objeto equivalente (OIDs) em conformidade com RFC 3280 e pretende que a seleção de certificado para ser com base nos valores do atributo. É possível especificar apenas os atributos e os respetivos valores necessários para identificar ou validar exclusivamente o certificado e distinguir o certificado de outros num arquivo de certificados.  

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

Se mais de um certificado apropriado está localizado depois dos critérios de seleção são aplicados, é possível substituir a configuração predefinida para selecionar o certificado com o período de validade mais longo e em vez disso, especificar que nenhum certificado está selecionado. Neste cenário, o cliente não conseguir comunicar com sistemas de sites do IIS com um certificado PKI. O cliente envia uma mensagem de erro para o respetivo ponto de estado de contingência atribuído para alertá-lo sobre a falha de seleção de certificado para que possa alterar ou refinar seus critérios de seleção de certificado. Em seguida, o comportamento do cliente depende se a falha de ligação falha através de HTTPS ou HTTP:  

-   Se a falha de ligação Ocorreu através de HTTPS: O cliente tenta estabelecer ligação através de HTTP e utiliza o certificado autoassinado do cliente.  

-   Se a falha de ligação Ocorreu através de HTTP: O cliente tenta estabelecer uma ligação novamente através de HTTP utilizando o certificado autoassinado do cliente.  

Para ajudar a identificar um certificado de cliente PKI único, também pode especificar um arquivo personalizado, diferente da predefinição de **pessoais** no **computador** armazenar. No entanto, tem de criar este arquivo de forma independente do Configuration Manager. Tem de ser capaz de implementar certificados neste arquivo personalizado e renová-los antes do período de validade expira.  

Para obter mais informações, consulte [configurar definições para certificados PKI de cliente](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureClientPKI).  


###  <a name="BKMK_PlanningForPKITransition"></a> Planear uma estratégia de transição para certificados PKI e gestão de clientes baseados na internet  

As opções de configuração flexíveis no Configuration Manager permitem-lhe gradualmente clientes de transição e o site para utilizar certificados PKI para o ajudar a pontos finais de cliente seguras. Certificados PKI fornecem uma maior segurança e permitem-lhe gerir os clientes de internet.  

Devido ao número de opções de configuração e opções no Configuration Manager, não há nenhuma forma única de transição de um site para que todos os clientes utilizem ligações HTTPS. No entanto, pode seguir estes passos como orientação:  

1. Instalar o site do Configuration Manager e configure-o para que os sistemas de sites aceitam ligações de cliente através de HTTPS e HTTP.  

2. Configurar o **comunicação do computador cliente** separador Propriedades do site até que o **definições do sistema de sites** é **HTTP ou HTTPS**e selecione **PKI de utilização certificado de cliente (capacidade de autenticação de cliente) quando estiverem disponíveis**.  Para obter mais informações, consulte [configurar definições para certificados PKI de cliente](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureClientPKI).  

3. Efetue uma implementação PKI para os certificados de cliente. Para um exemplo de implementação, consulte [implementar o certificado de cliente para computadores Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).  

4. Instale clientes utilizando o método de instalação push do cliente. Para obter mais informações, consulte a [como instalar clientes do Configuration Manager utilizando push de cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).  

5. Monitorizar a implementação de cliente e o estado com as informações e relatórios na consola do Configuration Manager.  

6. Verifique quantos clientes estão a utilizar um certificado PKI de cliente visualizando a coluna **Certificado de Cliente** na área de trabalho **Ativos e Compatibilidade** , nó **Dispositivos** .  

    Também pode implementar a ferramenta de avaliação de preparação do HTTPS do Configuration Manager (**cmHttpsReadiness.exe**) aos computadores. Em seguida, utilize os relatórios para verificar quantos computadores podem utilizar um certificado PKI de cliente com o Configuration Manager.  

   > [!NOTE]
   >  Quando instala o cliente do Configuration Manager, instala o **CMHttpsReadiness.exe** ferramenta no `%windir%\CCM` pasta. As seguintes opções da linha de comandos estão disponíveis quando executar essa ferramenta:  
   > 
   > - `/Store:<name>`: Esta opção é igual a **CCMCERTSTORE** propriedade Client. msi  
   > - `/Issuers:<list>`: Esta opção é igual a **CCMCERTISSUERS** propriedade Client. msi    
   > - `/Criteria:<criteria>`: Esta opção é igual a **CCMCERTSEL** propriedade Client. msi    
   > - `/SelectFirstCert`: Esta opção é igual a **CCMFIRSTCERT** propriedade Client. msi    
   > 
   >   Para obter mais informações, consulte [acerca das propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties).  

7. Quando tiver certeza de que suficiente clientes estão com êxito a utilizar o certificado PKI de cliente para autenticação através de HTTP, siga estes passos:  

   1.  Implementar um certificado de servidor web PKI para um servidor membro que executa um ponto de gestão adicional para o site e configurar esse certificado no IIS. Para obter mais informações, consulte [implementar o certificado de servidor web para sistemas de sites que executam o IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  

   2.  Instale a função do ponto de gestão neste servidor e configure a opção **Ligações de cliente** nas propriedades do ponto de gestão para **HTTPS**.  

8. Monitorize e certifique-se de que os clientes que tenham um certificado PKI utilizam o novo ponto de gestão utilizando HTTPS. Pode utilizar o registo do IIS ou contadores de desempenho para verificar.  

9. Reconfigure as outras funções do sistema de site para utilizar ligações de cliente HTTPS. Se pretender gerir clientes na internet, certifique-se de que os sistemas de sites têm um FQDN de internet. Configure pontos de gestão individual e pontos de distribuição para aceitar ligações de cliente a partir da internet.  

    > [!IMPORTANT]  
    >  Antes de configurar funções de sistema de sites para aceitar ligações a partir da internet, reveja as informações de planeamento e a pré-requisitos para gestão de clientes baseados na internet. Para obter mais informações, consulte [comunicações entre pontos finais](/sccm/core/plan-design/hierarchy/communications-between-endpoints).  

10. Expanda a implementação do certificado PKI para clientes e sistemas de sites que executam o IIS. Configure as funções de sistema de sites para ligações de cliente HTTPS e ligações de internet, conforme necessário.  

11. Para garantir a máxima segurança: Quando tiver certeza de que todos os clientes estão a utilizar um certificado PKI de cliente para autenticação e encriptação, altere as propriedades de site para utilizar apenas HTTPS.  

    Este plano primeiro apresenta os certificados PKI para autenticação apenas por HTTP e, em seguida, para autenticação e encriptação por HTTPS. Quando seguir este plano para introduzir gradualmente os estes certificados, é reduzir o risco de que os clientes se tornar não geridos. Também beneficiará da mais elevada segurança suportado pelo Configuration Manager.  

##  <a name="BKMK_PlanningForRTK"></a> Plano para a chave de raiz fidedigna  

 Fidedigna do Configuration Manager a chave de raiz fornece um mecanismo para clientes do Configuration Manager verificar o site sistemas pertencem à respetiva hierarquia. Cada servidor de site gera uma chave de troca de site para comunicar com outros sites. A chave de troca de site do site de nível superior na hierarquia chama-se chave de raiz fidedigna.  

 A função da chave de raiz fidedigna no Configuration Manager é semelhante a um certificado de raiz numa infraestrutura de chave pública. Nada assinado pela chave privada da chave de raiz fidedigna é fidedigno a hierarquia. Os clientes armazenam uma cópia da chave de raiz fidedigna do site no **root\ccm\locationservices** espaço de nomes WMI. 

 Por exemplo, o site emite um certificado para o ponto de gestão, que será iniciada com a chave privada da chave de raiz fidedigna. O site de partilha, com os clientes, a chave pública da respetiva chave de raiz fidedigna. Em seguida, os clientes podem diferenciar entre pontos de gestão que estão na respetiva hierarquia e pontos de gestão que não estão na respetiva hierarquia.   

 Os clientes obterem automaticamente a cópia pública da chave de raiz fidedigna através de dois mecanismos:  

- Expandir o esquema do Active Directory para o Configuration Manager e publicar o site de serviços de domínio do Active Directory. Em seguida, os clientes obter estas informações de site de um servidor de catálogo global. Para obter mais informações, consulte [preparar o Active Directory para publicação de site](/sccm/core/plan-design/network/extend-the-active-directory-schema).  

- Ao instalar os clientes que utilizam o método de instalação push do cliente. Para obter mais informações, consulte [instalação push do cliente](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation).  

  Se os clientes não é possível obter a chave de raiz fidedigna utilizando um destes mecanismos, que confiam a chave de raiz fidedigna que é fornecida pelo primeiro ponto de gestão com que comunicar. Neste cenário, um cliente poderia ser redirecionado para o ponto de gestão de um atacante onde receberia a política de ponto de gestão não autorizado. Esta ação requer que um atacante sofisticado. Este ataque está limitado a curto período de tempo antes do cliente obtém a chave de raiz fidedigna a partir de um ponto de gestão válido. Para reduzir o risco de um atacante redirecionar clientes para um ponto de gestão não autorizado, pré-Aprovisione os clientes com a chave de raiz fidedigna.  

  Utilize os seguintes procedimentos para pré-aprovisionar e verificar a chave de raiz fidedigna para um cliente do Configuration Manager:  

- [Pré-Aprovisione um cliente com a chave de raiz fidedigna utilizando um ficheiro](#bkmk_trk-provision-file)  

- [Pré-Aprovisione um cliente com a chave de raiz fidedigna sem utilizar um ficheiro](#bkmk_trk-provision-nofile)  

- [Certifique-se a chave de raiz fidedigna num cliente](#bkmk_trk-verify)  

- [Remova ou substitua a chave de raiz fidedigna](#bkmk_trk-reset)  

  > [!NOTE]  
  > Se os clientes podem obter a chave de raiz fidedigna dos serviços de domínio do Active Directory ou a instalação push do cliente, não precisa de aprovisionar previamente. 
  > 
  > Quando os clientes utilizam comunicações HTTPS para pontos de gestão, não precisa de aprovisionar previamente a chave de raiz fidedigna. Eles estabelecerem confiança, os certificados PKI.  


### <a name="bkmk_trk-provision-file"></a> Pré-Aprovisione um cliente com a chave de raiz fidedigna utilizando um ficheiro  

1.  No servidor do site, abra o ficheiro seguinte num editor de texto: `<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Localize a entrada **SMSPublicRootKey =**. Copie a chave dessa linha e feche o ficheiro sem quaisquer alterações.  

3.  Crie um novo ficheiro de texto e cole as informações da chave que copiou do ficheiro mobileclient tcf.  

4.  Guarde o ficheiro numa localização onde o todos os computadores podem acessá-lo, mas onde o ficheiro está protegido contra adulteração.  

5.  Instale o cliente utilizando um método de instalação que aceite propriedades Client. msi. Especifica a seguinte propriedade: `SMSROOTKEYPATH=<full path and file name>`  

    > [!IMPORTANT]  
    >  Quando especificar a chave de raiz fidedigna durante a instalação de cliente, também de especificar o código do site. Utilize a seguinte propriedade de Client. msi: `SMSSITECODE=<site code>`   


### <a name="bkmk_trk-provision-nofile"></a> Pré-Aprovisione um cliente com a chave de raiz fidedigna sem utilizar um ficheiro  

1.  No servidor do site, abra o ficheiro seguinte num editor de texto: `<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Localize a entrada **SMSPublicRootKey =**. Copie a chave dessa linha e feche o ficheiro sem quaisquer alterações.  

3.  Instale o cliente utilizando um método de instalação que aceite propriedades Client. msi. Especificar a seguinte propriedade de Client. msi: `SMSPublicRootKey=<key>` onde `<key>` é a cadeia que copiou de mobileclient.  

    > [!IMPORTANT]  
    >  Quando especificar a chave de raiz fidedigna durante a instalação de cliente, também de especificar o código do site. Utilize a seguinte propriedade de Client. msi: `SMSSITECODE=<site code>`   


### <a name="bkmk_trk-verify"></a> Certifique-se a chave de raiz fidedigna num cliente  

1. Abra a consola do Windows PowerShell como administrador.  

2. Execute o seguinte comando:  

``` PowerShell
 (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
```

A cadeia de caracteres retornada é a chave de raiz fidedigna. Certifique-se de que corresponde da **SMSPublicRootKey** valor no ficheiro mobileclient tcf no servidor do site.  


### <a name="bkmk_trk-reset"></a> Remova ou substitua a chave de raiz fidedigna  

 Remover a chave de raiz fidedigna de um cliente, utilizando a propriedade de Client. msi **RESETKEYINFORMATION = TRUE**. 

 Para substituir a chave de raiz fidedigna, reinstale o cliente, juntamente com a nova chave de raiz fidedigna. Por exemplo, utilizar o push do cliente, ou especificar a propriedade de Client. msi **SMSPublicRootKey**.  

 Para obter mais informações sobre estas propriedades de instalação, consulte [sobre parâmetros de instalação de cliente e as propriedades](/sccm/core/clients/deploy/about-client-installation-properties).



##  <a name="BKMK_PlanningForSigningEncryption"></a> Plano para assinatura e encriptação  
 
 Quando utiliza certificados PKI para todas as comunicações de cliente, não precisa de planear a assinatura e encriptação ajudar a comunicação de dados do cliente seguros. Se configurar sistemas de sites que executam o IIS para permitir ligações de cliente HTTP, decida como ajudar a proteger a comunicação de cliente para o site.  

 Para ajudar a proteger os dados que os clientes enviam para os pontos de gestão, pode precisar que os clientes assinar os dados. Também pode exigir o algoritmo SHA-256 para assinar. Esta configuração é mais seguro, mas não exigem SHA-256, a menos que todos os clientes suportam. Muitos sistemas operativos suportam nativamente o esse algoritmo, mas os sistemas operativos mais antigos podem exigir uma atualização ou correção. 

 Enquanto o ajuda a assinatura protege os dados contra adulteração, a criptografia ajuda a proteger os dados contra divulgação de informações. Pode ativar a encriptação 3DES para os dados de inventário e as mensagens de estado que os clientes enviam para os pontos de gestão do site. Não tem de instalar quaisquer atualizações nos clientes para suportar esta opção. Os clientes e os pontos de gestão requerem a utilização adicional da CPU para encriptação e desencriptação.  

 Para obter mais informações sobre como configurar as definições para assinatura e encriptação, consulte [configurar a assinatura e encriptação](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureSigningEncryption).  



##  <a name="BKMK_PlanningForRBA"></a> Planear a administração baseada em funções  

 Para obter mais informações, consulte [Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).  



## <a name="bkmk_planazuread"></a> Plano para o Azure Active Directory

 O Configuration Manager integra-se com o Azure Active Directory (Azure AD) para ativar o site e os clientes utilizem autenticação moderna. Integração do seu site com o Azure AD suporta os seguintes cenários do Configuration Manager:

**Cliente**  

- [Gerir clientes na internet através do gateway de gestão da cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#scenarios)  

- [Gerir dispositivos associados a um domínio de cloud](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

- [Cogestão](/sccm/comanage/overview)  

- [Implementar aplicações disponíveis ao utilizador](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)  

- [Microsoft Store online para aplicações de negócio](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)  

- Reduza os requisitos de infraestrutura. Por exemplo, [Centro de Software utilizando o ponto de gestão](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex) em vez do catálogo de aplicações  

- [Gerir aplicações do Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates)  


**servidor**  

- [Preparação para atualização](/sccm/core/clients/manage/upgrade-readiness)  

- [Análise do Windows](/sccm/core/clients/manage/monitor-windows-analytics)  

- [Log Analytics do Azure](/sccm/core/clients/manage/sync-data-log-analytics)  

- [Hub de Comunidade](/sccm/core/get-started/capabilities-in-technical-preview-1807#bkmk_hub)  

- [Ponto de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

- [Deteção de utilizadores](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  


 Para obter mais informações sobre como ligar o seu site para o Azure AD, consulte [dos serviços do Azure configurar](/sccm/core/servers/deploy/configure/azure-services-wizard).


 Para obter mais informações sobre o Azure AD, consulte [documentação do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).



## <a name="bkmk_auth"></a> Plano para a autenticação de fornecedor de SMS
<!--1357013--> 

A partir da versão 1810, pode especificar o nível mínimo de autenticação para os administradores aceder a sites do Configuration Manager. Esta funcionalidade aplica os administradores para iniciar sessão no Windows com o nível necessário. Aplica-se a todos os componentes que aceder ao fornecedor de SMS. Por exemplo, a consola do Configuration Manager, os métodos SDK e cmdlets do Windows PowerShell. 

Esta configuração é uma definição ao nível da hierarquia. Antes de alterar esta definição, certifique-se de que todos os administradores do Configuration Manager podem iniciar sessão no Windows com o nível de autenticação necessária. 

Os seguintes níveis estão disponíveis:

- **Autenticação do Windows**: Exigir a autenticação com credenciais de domínio do Active Directory.   

- **Autenticação de certificados**: Exigir a autenticação com um certificado válido emitido por uma autoridade de certificação fidedigna PKI.  

- **Windows Hello para autenticação de negócios**: Exigir a autenticação com a autenticação de dois fatores forte, que está associada a um dispositivo e utiliza a biometria ou um PIN.  

Para obter mais informações, consulte [planear o fornecedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth). 



## <a name="see-also"></a>Consulte também
- [Segurança e privacidade para clientes do Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Configurar a segurança](/sccm/core/plan-design/security/configure-security)  

- [Comunicação entre pontos de extremidade](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

- [Referência técnica de controlos criptográficos](/sccm/core/plan-design/security/cryptographic-controls-tehnical-reference)  

- [Requisitos do certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements)  


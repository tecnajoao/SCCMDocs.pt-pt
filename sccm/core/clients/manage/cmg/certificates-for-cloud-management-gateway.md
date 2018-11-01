---
title: Certificados CMG
description: Saiba mais sobre os diferentes certificados digitais para utilizar com o gateway de gestão na cloud.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 10/24/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: 121b3840ea4f61f4789c5d6c21ab857cb091e199
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411311"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Certificados para o gateway de gestão da nuvem

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Consoante o cenário que utiliza para gerir clientes na internet com o gateway de gestão da cloud (CMG), é necessário um ou mais dos seguintes certificados digitais:  

- [Certificado de autenticação de servidor CMG](#bkmk_serverauth)  
    - [Certificado de raiz fidedigna do CMG para clientes](#bkmk_cmgroot)  
    - [Certificado de autenticação de servidor emitido por fornecedor público](#bkmk_serverauthpublic)  
    - [Certificado de autenticação de servidor emitido por enterprise PKI](#bkmk_serverauthpki)  

- [Certificado de gestão do Azure](#bkmk_azuremgmt)  

- [Certificado de autenticação de cliente](#bkmk_clientauth)  
    - [Certificado de raiz fidedigna do cliente para CMG](#bkmk_clientroot)  

- [Ativar o ponto de gestão para HTTPS](#bkmk_mphttps)  


Para obter mais informações sobre os diferentes cenários, consulte [plano para o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


### <a name="general-information"></a>Informações gerais
<!--SCCMDocs issue #779--> Certificados para o gateway de gestão na nuvem suportam as seguintes configurações:  

- **comprimento de chave de 4096 bits**  

- A partir da versão 1710, o suporte para fornecedores de armazenamento de chaves para chaves privadas do certificado. Para obter mais informações, consulte [descrição geral de certificados CNG](/sccm/core/plan-design/network/cng-certificates-overview).  

- A partir da versão 1802, ao configurar o Windows com a seguinte política: **Criptografia de sistema: Utilizar algoritmos compatíveis com FIPS para encriptação, hash e assinatura**  

- A partir da versão 1802, suporte para **TLS 1.2**. Para obter mais informações, consulte [referência técnica de controlos criptográficos utilizados](/sccm/core/plan-design/security/cryptographic-controls-technical-reference#about-ssl-vulnerabilities).  



## <a name="bkmk_serverauth"></a> Certificado de autenticação de servidor CMG

*Este certificado é necessário em todos os cenários.*

Este certificado é fornecer ao criar CMG na consola do Configuration Manager.

O CMG cria um serviço HTTPS para o qual se ligar a clientes baseados na internet. O servidor requer um certificado de autenticação de servidor para criar o canal seguro. Adquirir um certificado para esta finalidade de um fornecedor de público ou enviá-lo a partir da sua infraestrutura de chaves públicas (PKI). Para obter mais informações, consulte [certificado de raiz fidedigna do CMG para clientes](#cmg-trusted-root-certificate-to-clients).

 > [!TIP]
 > Este certificado requer um nome globalmente exclusivo para identificar o serviço no Azure. Antes de solicitar um certificado, confirme que o nome de domínio do Azure pretendido é exclusivo. Por exemplo, *GraniteFalls.CloudApp.Net*. Inicie sessão para o [portal do Microsoft Azure](https://portal.azure.com). Selecione **criar um recurso**, escolha a **computação** categoria, em seguida, selecione **serviço em nuvem**. Na **nome DNS** campo, escreva o prefixo pretendido, por exemplo *GraniteFalls*. A interface reflete se o nome de domínio está disponível ou já em utilização por outro serviço. Não criar o serviço no portal, basta usar este processo para verificar a disponibilidade de nome. 
  
 > [!NOTE]
 > A partir da versão 1802, o certificado de autenticação de servidor CMG suporta carateres universais. Alguns autoridades de certificação emitem certificados através de um caráter universal para o nome do anfitrião. Por exemplo,  **\*. contoso.com**. Algumas organizações utilizam certificados de caráter universal para simplificar seu PKI e reduzir os custos de manutenção.<!--491233-->  
 > 
 > Para obter mais informações sobre como utilizar um certificado de caráter universal com um CMG, consulte [configurar uma CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#set-up-a-cmg).<!--SCCMDocs issue #565-->  


### <a name="bkmk_cmgroot"></a> Certificado de raiz fidedigna do CMG para clientes

Os clientes têm de confiar no certificado de autenticação de servidor do CMG. Existem dois métodos para realizar esta demonstração de confiança: 

- Utilize um certificado de um fornecedor do certificado público e globalmente confiáveis. Por exemplo, mas não limitado a, DigiCert, Thawte ou VeriSign. Os clientes do Windows incluem autoridades de certificação de raiz fidedigna (AC) desses provedores. Ao utilizar um certificado de autenticação de servidor emitido por um destes fornecedores, os clientes automaticamente confiam nele.  

- Utilize um certificado emitido por uma AC empresarial da sua infraestrutura de chaves públicas (PKI). A maioria das implementações de PKI de empresa adicionar AC de raiz fidedigna para os clientes do Windows. Por exemplo, através dos serviços de certificados do Active Directory com a política de grupo. Se emitir o servidor CMG certificado de autenticação por uma AC que seus clientes automaticamente não confiam, adicione o certificado da AC de raiz fidedigna para clientes baseados na internet.  

    - Também pode utilizar perfis de certificado do Configuration Manager para provisionar certificados em clientes. Para obter mais informações, consulte [introdução aos perfis de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

> [!Note]  
> A partir da versão 1806, quando cria um CMG, já não tem de fornecer um certificado de raiz fidedigna na página Definições. Este certificado não necessárias ao utilizar o Azure Active Directory (Azure AD) para autenticação de cliente, mas utilizado para ser necessário no assistente. Se estiver a utilizar certificados de autenticação de cliente PKI, em seguida, ainda tem de adicionar um certificado de raiz fidedigna para CMG.<!--SCCMDocs-pr issue #2872-->  


### <a name="bkmk_serverauthpublic"></a> Certificado de autenticação de servidor emitido por fornecedor público

Um fornecedor de certificados de terceiros não é possível criar um certificado para CloudApp.net, à medida que o domínio pertence à Microsoft. Só pode obter um certificado emitido para um domínio que possui. O principal motivo para adquirir um certificado de um fornecedor de terceiros é que os clientes confiam já certificado de raiz desse fornecedor.

Utilize o seguinte processo para criar um alias de DNS:

1. Crie um registo de nome canónico (CNAME) no DNS público da sua organização. Este registo cria um alias para CMG para um nome amigável que utilize o certificado público.

    Por exemplo, Contoso nomeia seus CMG **GraniteFalls**, que se torna **GraniteFalls.CloudApp.Net** no Azure. Na público contoso.com espaço de nomes DNS da Contoso, o administrador DNS cria um novo registo CNAME **GraniteFalls.Contoso.com** para o nome de anfitrião real **GraniteFalls.CloudApp.net**.  

2. Pedir um certificado de autenticação de servidor do fornecedor público com o nome comum (CN) de CNAME alias.
Por exemplo, a Contoso utiliza **GraniteFalls.Contoso.com** para o CN do certificado.  

3. Crie CMG na consola do Configuration Manager utilizando este certificado. Sobre o **definições** página do assistente Gateway de gestão na Cloud criar:   

    - Ao adicionar o certificado de servidor para este serviço cloud (partir **ficheiro de certificado**), o assistente extrai o nome de anfitrião do certificado CN como o nome do serviço.  

    - Ele anexa, em seguida, esse nome de anfitrião para **cloudapp.net**, ou **usgovcloudapp.net** da cloud do Azure US Government, como o FQDN de serviço para criar o serviço no Azure.  

    - Por exemplo, quando Contoso cria o CMG, o Configuration Manager extrai o nome do anfitrião **GraniteFalls** do CN do certificado. O serviço real, como o Azure cria **GraniteFalls.CloudApp.net**.  

Quando cria a instância CMG no Configuration Manager, enquanto o certificado tem GraniteFalls.Contoso.com, Configuration Manager apenas extrai o nome do anfitrião, por exemplo: GraniteFalls. Ele acrescenta este nome de anfitrião para CloudApp.net, o que requer o Azure ao criar um serviço em nuvem. O CNAME, alias no espaço de nomes DNS para o seu domínio, Contoso.com, em conjunto mapeia estes dois FQDNs. Configuration Manager fornece aos clientes uma política para aceder a este CMG, o mapeamento de DNS junta-lo para que eles podem aceder de forma segura o serviço no Azure.<!--SCCMDocs issue #565-->  


### <a name="bkmk_serverauthpki"></a> Certificado de autenticação de servidor emitido por enterprise PKI

Crie um certificado SSL personalizado para CMG o igual de um ponto de distribuição de nuvem. Siga as instruções para [implementar o certificado de serviço para pontos de distribuição baseado na nuvem](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012) mas efetue os seguintes procedimentos de forma diferente:

- Quando pedir o certificado de servidor web personalizado, fornece um FQDN para o nome comum do certificado. Este nome pode ser um nome de domínio público que é proprietário ou pode utilizar o domínio cloudapp.net. Se utilizar o seu próprio domínio público, consulte o processo acima para criar um alias de DNS no DNS público da sua organização.  

- Ao utilizar o domínio cloudapp.net público para o certificado de servidor web do CMG:  

    - No cloud pública do Azure, utilize um nome que termina em **cloudapp.net**  

    - Utilizar um nome que termina em **usgovcloudapp.net** para a cloud do Azure US Government  



## <a name="bkmk_azuremgmt"></a> Certificado de gestão do Azure

*Este certificado é necessário para implementações de serviços clássico. Não é necessário para implementações do Azure Resource Manager.*

Este certificado no portal do Azure e fornecer ao criar CMG na consola do Configuration Manager.

Para criar CMG no Azure, a ligação de serviço do Configuration Manager ponto precisa primeiro autenticar para a sua subscrição do Azure. Quando utilizar uma implementação de serviço clássico, utiliza o certificado de gestão do Azure para esta autenticação. Um administrador do Azure carrega este certificado para a sua subscrição. Quando cria o CMG na consola do Configuration Manager, fornece este certificado.

Para obter mais informações e instruções sobre como carregar um certificado de gestão, veja os artigos seguintes na documentação do Azure:

- [Serviços cloud e gestão de certificados](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [Carregar um certificado de gestão de serviço do Azure](https://docs.microsoft.com/azure/azure-api-management-certs)  

> [!IMPORTANT]
> Certifique-se copiar o ID de subscrição associado ao certificado de gestão. Utilizá-lo para a criação de CMG na consola do Configuration Manager.



## <a name="bkmk_clientauth"></a> Certificado de autenticação de cliente

*Este certificado é necessário para clientes baseados na internet com o Windows 7, Windows 8.1 e dispositivos Windows 10 não associados ao Azure Active Directory (Azure AD). Também é necessário no ponto de ligação CMG. Não é necessário para clientes do Windows 10 associados ao Azure AD.*

Os clientes utilizam este certificado para autenticar com o CMG. Dispositivos Windows 10 que são híbrido ou na cloud associados a um domínio não requerem este certificado, porque utilizam o Azure AD para autenticar.

Aprovisione este certificado fora do contexto do Configuration Manager. Por exemplo, pode utilize os serviços de certificados do Active Directory e a política de grupo para emitir certificados de autenticação de cliente. Para obter mais informações, consulte [implementar o certificado de cliente para computadores Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).

O ponto de ligação do CMG requer este certificado em segurança reencaminhar pedidos de cliente para um ponto de gestão HTTPS. Se estiver a utilizar o Azure AD ou avançado HTTP, este certificado não é necessário. Para obter mais informações, consulte [ativar o ponto de gestão para HTTPS](#bkmk_mphttps).


### <a name="bkmk_clientroot"></a> Certificado de raiz fidedigna do cliente para CMG

*Este certificado é necessário quando utilizar certificados de autenticação de cliente. Quando todos os clientes utilizarem o Azure AD para autenticação, este certificado não é necessário.* 

Este certificado é fornecer ao criar CMG na consola do Configuration Manager.

O CMG têm de confiar os certificados de autenticação de cliente. Para realizar esta confiança, fornecem a cadeia de certificados de raiz fidedigna. Pode especificar duas AC de raiz fidedigna e quatro CAs (subordinada) intermediárias. 


#### <a name="export-the-client-certificates-trusted-root"></a>Exportar de raiz fidedigna do certificado de cliente

Depois de emitir um certificado de autenticação de cliente para um computador, utilize este processo nesse computador para exportar a raiz fidedigna.

1.  Abra o menu Iniciar. Escreva "executar" para abrir a janela de execução. Abra `mmc`.  

2.  No menu ficheiro, escolha **Adicionar/Remover Snap-in...** .  

3.  Na caixa de diálogo Adicionar ou Remover Snap-ins, selecione **certificados**, em seguida, selecione **Add**.  

    a. Na caixa de diálogo snap-in de certificados, selecione **conta de computador**, em seguida, selecione **próxima**.  

    b. Na caixa de diálogo Selecionar computador, selecione **computador Local**, em seguida, selecione **concluir**.  

    c. Na caixa de diálogo Adicionar ou Remover Snap-ins, selecione **OK**.  

4.  Expanda **certificados**, expanda **pessoais**e selecione **certificados**.  

5.  Selecione um certificado cujo objetivo pretendido é **autenticação de cliente**.  

    a. No menu ação, selecione **aberto**.  

    b. Vá para o **caminho de certificação** separador.  

    c. Selecione o certificado seguinte na cadeia e selecione **Ver certificado**.  

6.  Na caixa de diálogo certificado novo, vá para o **detalhes** separador. Selecione **copiar para ficheiro...** .  

7.  Concluir o Assistente para exportar certificados utilizando o formato de certificado do predefinido, **binário codificado DER X.509 (. CER)**. Torne a nota do nome e localização do certificado exportado.  

8. Exporte todos os certificados no caminho de certificação do certificado de autenticação de cliente original. Tome nota dos quais certificados exportados são CAs intermediárias e quais são as ACs de raiz fidedigna.  



## <a name="bkmk_mphttps"></a> Ativar o ponto de gestão para HTTPS

Aprovisione este certificado fora do contexto do Configuration Manager. Por exemplo, utilize os serviços de certificados do Active Directory e a política de grupo para emitir um certificado de servidor web. Para obter mais informações, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements) e [implementar o certificado de servidor web para sistemas de sites que executam o IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).


- Na versão 1706 ou 1710, quando gerir clientes tradicionais com locais identidade a utilizar um certificado de autenticação de cliente, este certificado é recomendado mas não obrigatório.  

- Na versão 1710, quando a gestão de clientes do Windows 10 associados ao Azure AD, este certificado é necessário para pontos de gestão.  

- Este certificado a partir da versão 1802, é necessário em todos os cenários. Apenas os pontos de gestão que ativar para CMG tem de ser HTTPS. Esta alteração no comportamento fornece melhor suporte para autenticação baseada em tokens do AD do Azure.  

- A partir da versão 1806, quando o site a utilizar a opção de **sistemas de sites de certificados gerados pelo utilize o Gestor de configuração para HTTP**, o ponto de gestão pode ser HTTP. Para obter mais informações, consulte [avançada HTTP](/sccm/core/plan-design/hierarchy/enhanced-http).

### <a name="management-point-client-connection-mode-summary"></a>Modo de ligação de cliente resumo do ponto de gestão
Estas tabelas resumem se necessita que o ponto de gestão HTTP ou HTTPS, dependendo do tipo de versão de cliente e o site.

#### <a name="for-internet-based-clients-communicating-with-the-cloud-management-gateway"></a>Para clientes baseados na internet ao comunicar com o gateway de gestão da nuvem
Configure um ponto de gestão no local para permitir ligações a partir do CMG com o modo de ligação de cliente seguinte:

| Tipo de cliente   | 1706        | 1710        | 1802        | 1806        |
|------------------|-------------|-------------|-------------|-------------|
| Grupo de trabalho        | HTTP, HTTPS | HTTP, HTTPS | HTTPS       | E HTTP<sup>[tenha em atenção 1](#bkmk_note1)</sup>, HTTPS |
| Associado a um domínio do AD | HTTP, HTTPS | HTTP, HTTPS | HTTPS       | E HTTP<sup>[tenha em atenção 1](#bkmk_note1)</sup>, HTTPS |
| Azure AD associado  | HTTPS       | HTTPS       | HTTPS       | E-HTTP, HTTPS |
| Associado a um híbrido    | HTTP, HTTPS | HTTP, HTTPS | HTTPS       | E-HTTP, HTTPS |

<a name="bkmk_note1"></a> 

> [!Note]  
> **Tenha em atenção 1**: Esta configuração requer que o cliente tem um [certificado de autenticação de cliente](#bkmk_clientauth)e apenas suporta cenários de TI centradas em dispositivo.  

#### <a name="for-on-premises-clients-communicating-with-the-on-premises-management-point"></a>Para clientes no local ao comunicar com o ponto de gestão no local
Configure um ponto de gestão no local com o modo de ligação de cliente seguinte:

| Tipo de cliente   | 1706        | 1710        | 1802        | 1806        |
|------------------|-------------|-------------|-------------|-------------|
| Grupo de trabalho        | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS |
| Associado a um domínio do AD | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS |
| Azure AD associado  | HTTPS       | HTTPS       | HTTPS       | HTTPS       |
| Associado a um híbrido    | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS |

> [!Note]  
> Na versão 1806, os clientes associados a um domínio do AD suportam ambos os cenários de dispositivo - e centrada no utilizador comunicar com um ponto de gestão HTTP ou HTTPS.  
> 
> Clientes de associados ao AD e associados a um híbrido do Azure podem comunicar através de HTTP para cenários de TI centradas em dispositivo, mas precisa E HTTP ou HTTPS para ativar cenários centrada no utilizador. Caso contrário, eles se comportam da mesma forma como os clientes de grupo de trabalho.  


#### <a name="legend-of-terms"></a>Legenda de termos
- *Grupo de Trabalho*: O dispositivo não esteja associado a um domínio ou do Azure AD, mas tem um [certificado de autenticação de cliente](#bkmk_clientauth)  
- *Associado a um domínio do AD*: Associar o dispositivo a um domínio do Active Directory no local  
- *Azure AD associado*: Também conhecido como cloud associados a um domínio, associar o dispositivo a um inquilino do Azure Active Directory  
- *Híbrido associou*: Associar o dispositivo a um domínio do Active Directory e um inquilino do Azure AD  
- *HTTP*: Nas propriedades do ponto de gestão, defina o cliente ligações para **HTTP**  
- *HTTPS*: Nas propriedades do ponto de gestão, defina o cliente ligações para **HTTPS**  
- *E HTTP*: Nas propriedades do site, separador de comunicação do computador cliente, definir o site de definições do sistema para **HTTPS ou HTTP**, e ativar a opção para **desistemasdesitesdecertificadosgeradospeloutilizeoGestordeconfiguraçãoparaHTTP**. Configurar o ponto de gestão para HTTP ou HTTPS.  



## <a name="next-steps"></a>Passos seguintes

- [Configurar o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  

- [Perguntas mais frequentes sobre o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)  

- [Segurança e privacidade para o gateway de gestão na cloud ](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)  

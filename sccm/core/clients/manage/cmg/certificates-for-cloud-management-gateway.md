---
title: CMG certificados
description: Saiba mais sobre os certificados digitais diferentes para utilizar com o gateway de gestão de nuvem.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: fbae44d1344dd36d3c0a6faf2e50727dfa830ba0
ms.sourcegitcommit: 8060ea520fb08629e1d5f249daffe825536673a5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/08/2018
ms.locfileid: "35232375"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Certificados para o gateway de gestão de nuvem

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Consoante o cenário que utiliza para gerir clientes na internet com o gateway de gestão de nuvem (CMG), precisa de um ou mais certificados digitais. Para obter mais informações sobre os diferentes cenários, consulte [plano para gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="cmg-server-authentication-certificate"></a>Certificado de autenticação de servidor CMG

*Este certificado é necessário em todos os cenários.*

Este certificado é fornecer ao criar o CMG na consola do Configuration Manager.

O CMG cria um serviço HTTPS ao qual ligam clientes baseados na internet. O servidor requer um certificado de autenticação de servidor para criar o canal seguro. Adquirir um certificado para o efeito de um fornecedor público ou enviá-lo a partir da sua infraestrutura de chaves públicas (PKI). Para obter mais informações, consulte [certificado de raiz fidedigna CMG aos clientes](#cmg-trusted-root-certificate-to-clients).

 > [!TIP]
 > Este certificado requer um nome globalmente exclusivo para identificar o serviço do Azure. Antes de pedir um certificado, confirme que o nome de domínio do Azure pretendido é exclusivo. Por exemplo, *GraniteFalls.CloudApp.Net*. Inicie sessão no [portal do Microsoft Azure](https://portal.azure.com). Clique em **crie um recurso**, selecione o **computação** categoria, em seguida, clique em **serviço em nuvem**. No **nome DNS** campo, escreva o prefixo pretendido, por exemplo *GraniteFalls*. A interface reflete se o nome de domínio está disponível ou já se encontra em utilização por outro serviço. Não criar o serviço no portal, basta utilizar este processo para verificar a disponibilidade do nome. 
  
 > [!NOTE]
 > A partir de versão 1802, o certificado de autenticação de servidor CMG suporta carateres universais. Alguns autoridades de certificação emitem certificados através de um caráter universal para o nome do anfitrião. Por exemplo,  **\*. contoso.com**. Algumas organizações utilizam certificados de caráter universal para simplificar o seu PKI e reduzir os custos de manutenção.
 <!--491233-->


### <a name="cmg-trusted-root-certificate-to-clients"></a>Certificado de raiz fidedigna CMG para clientes

Clientes tem de confiar no certificado de autenticação de servidor CMG. Existem dois métodos para realizar esta confiança:
- Utilize um certificado de um fornecedor de certificado pública e globalmente fidedignas. Por exemplo, mas não limitado a, DigiCert, Thawte ou VeriSign. Clientes Windows incluem autoridades de certificação de raiz fidedigna (AC) destes fornecedores. Ao utilizar um certificado de autenticação de servidor emitido por um destes fornecedores, os clientes automaticamente confiam nele. 
- Utilize um certificado emitido por uma AC empresarial da sua infraestrutura de chaves públicas (PKI). A maioria das implementações de PKI de empresa adicionar ACs de raiz fidedigna para clientes do Windows. Por exemplo, utilizando os serviços de certificados do Active Directory com a política de grupo. Se emitir o servidor CMG certificado de autenticação de uma AC que os clientes não confiam automaticamente, terá de adicionar o certificado da AC de raiz fidedigna para os clientes baseados na internet.
    - Também pode utilizar perfis de certificado do Configuration Manager para aprovisionar certificados em clientes. Para obter mais informações, consulte [introdução aos perfis de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).

### <a name="server-authentication-certificate-issued-by-public-provider"></a>Certificado de autenticação de servidor emitido por fornecedor público

Quando utiliza este método, os clientes automaticamente confiam no certificado e não precisa de criar um certificado personalizado por si. Com o domínio cloudapp.net, o Configuration Manager cria o serviço no Azure. Um fornecedor de certificação pública não é possível emitir para si um certificado com este nome. Utilize o seguinte processo para criar um alias de DNS:

1. Crie um registo de nome canónico (CNAME) no DNS público da sua organização. Este registo cria um alias para CMG para um nome amigável que utilizam o certificado público.
Por exemplo, Contoso nomes os respetivos CMG **GraniteFalls**, que passa a ser **GraniteFalls.CloudApp.Net** no Azure. O administrador DNS público contoso.com espaço de nomes DNS da Contoso, cria um novo registo CNAME para **GraniteFalls.Contoso.com** para o nome de anfitrião real, **GraniteFalls.CloudApp.net**.
2. Pedir um certificado de autenticação de servidor a partir de um fornecedor público com o nome comum (CN) do CNAME alias de.
Por exemplo, a Contoso utiliza **GraniteFalls.Contoso.com** para o CN do certificado.
3. Crie o CMG na consola do Configuration Manager utilizando este certificado. No **definições** página do assistente criar uma nuvem gestão Gateway: 
    - Ao adicionar o certificado de servidor para este serviço em nuvem (de **ficheiro de certificado**), o assistente extrai o nome de anfitrião do certificado CN como o nome do serviço. 
    - -Acrescenta, em seguida, esse nome de anfitrião para **cloudapp.net**, ou **usgovcloudapp.net** para a nuvem do Azure US Government, como o FQDN de serviço para criar o serviço no Azure.
    - Por exemplo, quando Contoso cria o CMG, o Configuration Manager extrai o nome de anfitrião **GraniteFalls** do CN do certificado. O serviço real como o Azure cria **GraniteFalls.CloudApp.net**.

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a>Certificado de autenticação de servidor emitido por enterprise PKI

Crie um certificado SSL personalizado para o CMG o igual para um ponto de distribuição na nuvem. Siga as instruções para [implementar o certificado de serviço para pontos de distribuição baseado na nuvem](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012) mas efetue os seguintes procedimentos de forma diferente:

- Quando pedir o certificado de servidor web personalizado, fornece um FQDN para o nome comum do certificado. Para utilizar o CMG na nuvem pública do Azure, utilize um nome que termina em **cloudapp.net**, ou **usgovcloudapp.net** para a nuvem do Azure US Government.



## <a name="azure-management-certificate"></a>Certificado de gestão do Azure

*Este certificado é necessário para implementações de serviço clássico. Não é necessário para implementações do Azure Resource Manager.*

Forneça este certificado no portal do Azure e ao criar o CMG na consola do Configuration Manager.

Para criar o CMG no Azure, a ligação de serviço do Configuration Manager ponto tem de primeiro autenticar para a sua subscrição do Azure. Quando utilizar uma implementação de serviço clássico, utiliza o certificado de gestão do Azure para esta autenticação. Um administrador do Azure carrega este certificado para a sua subscrição. Quando cria o CMG na consola do Configuration Manager, forneça este certificado.

Para obter mais informações e instruções sobre como carregar um certificado de gestão, consulte os artigos seguintes na documentação do Azure:

- [Serviços em nuvem e certificados de gestão](/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)

- [Carregar um certificado de gestão de serviço do Azure](/azure/azure-api-management-certs)

> [!IMPORTANT]
> Certifique-se ao copiar o ID de subscrição associado o certificado de gestão. Utilizá-la para criar o CMG na consola do Configuration Manager.



## <a name="client-authentication-certificate"></a>Certificado de autenticação de cliente

*Este certificado é necessário para clientes baseados na internet com o Windows 7, Windows 8.1 e dispositivos Windows 10 não associados ao Azure Active Directory (Azure AD). Também é necessário no ponto de ligação de CMG. Não é necessário para clientes Windows 10 associados ao Azure AD.*

Os clientes utilizam este certificado para autenticar com o CMG. Dispositivos Windows 10 que são híbrido ou na nuvem associados a um domínio não requerem este certificado, porque utilizam do Azure AD para autenticar.

Aprovisione este certificado fora do contexto do Configuration Manager. Por exemplo, pode utilize os serviços de certificados do Active Directory e a política de grupo para emitir certificados de autenticação de cliente. Para obter mais informações, consulte [implementar o certificado de cliente para computadores Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).


### <a name="client-trusted-root-certificate-to-cmg"></a>Certificado de raiz fidedigna do cliente para CMG

*Este certificado é necessário quando utilizar certificados de autenticação de cliente. Quando todos os clientes utilizam o Azure AD para autenticação, este certificado não é necessário.* 

Este certificado é fornecer ao criar o CMG na consola do Configuration Manager.

O CMG têm de confiar os certificados de autenticação de cliente. Para realizar esta confiança, forneça a cadeia de certificados de raiz fidedigna. Pode especificar dois ACs de raiz fidedigna e quatro ACs (subordinadas) intermediária. 


#### <a name="export-the-client-certificates-trusted-root"></a>Exportar a raiz fidedigna do certificado de cliente

Depois de emitir um certificado de autenticação de cliente para um computador, utilize este processo nesse computador, para exportar a raiz fidedigna.

1.  Abra o menu Iniciar. Escreva "executar" para abrir a janela de execução. Abra **mmc**. 

2.  No menu ficheiro, escolha **Adicionar/Remover Snap-in...** .

3.  Na caixa de diálogo Adicionar ou Remover Snap-ins, selecione **certificados**, em seguida, clique em **adicionar**. 
    a. Na caixa de diálogo snap-in certificados, selecione **conta de computador**, em seguida, clique em **seguinte**. 
    b. Na caixa de diálogo Selecionar computador, selecione **computador Local**, em seguida, clique em **concluir**. 
    c. Na caixa de diálogo Adicionar ou Remover Snap-ins, clique em **OK**.

4.  Expanda **certificados**, expanda **pessoais**e selecione **certificados**.

5.  Selecione um certificado cujo objetivo pretendido é **autenticação de cliente**. 
    a. No menu ação, selecione **abra**. 
    b. Mudar para o **caminho de certificação** separador. c. Selecione o certificado seguinte da cadeia de cópia de segurança e clique em **Ver certificado**.

6.  Nesta caixa de diálogo para o certificado novo comutador para a **detalhes** separador. Clique em **copiar para ficheiro...** .

7.  Conclua o Assistente para exportar certificados utilizando o formato de certificado predefinido, **x. 509 binário codificado de DER (. CER)**. Tome nota do nome e localização do certificado exportado.

8. Exporte todos os certificados no caminho de certificação do certificado de autenticação de cliente original. Anote que os certificados exportados são ACs intermediárias e aqueles são ACs de raiz fidedigna.



## <a name="enable-management-point-for-https"></a>Ativar o ponto de gestão para HTTPS

*Requisitos de certificado*
- Em versões 1706 ou 1710, quando gerir clientes tradicionais no local utilizando um certificado de autenticação de cliente de identidade, este certificado é recomendado, mas não é necessária.
- Na versão 1710, quando gerir clientes do Windows 10 associado para o Azure AD, este certificado é necessário para pontos de gestão. 
- Este certificado a partir de versão 1802, é necessário em todos os cenários. Apenas os pontos de gestão que ativar para CMG tem de ser HTTPS. Esta alteração no comportamento fornece um melhor suporte para autenticação baseada em tokens do AD do Azure. 

Aprovisione este certificado fora do contexto do Configuration Manager. Por exemplo, utilize os serviços de certificados do Active Directory e a política de grupo para emitir um certificado de servidor web. Para obter mais informações, consulte [requisitos dos certificados PKI](/sccm/core/plan-design/network/pki-certificate-requirements) e [implementar o certificado de servidor web para sistemas de sites que executam o IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).



## <a name="next-steps"></a>Passos seguintes

- [Configurar o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Perguntas mais frequentes sobre o gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Segurança e privacidade para o gateway de gestão na cloud ](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)

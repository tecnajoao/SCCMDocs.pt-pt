---
title: Certificados CMG
description: Saiba mais sobre os diferentes certificados digitais para utilizar com o gateway de gestão na cloud.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: 02a830d10263164e26902247856f999523092c76
ms.sourcegitcommit: a849dab9333ebac799812624d6155f2a96b523ca
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/10/2018
ms.locfileid: "42586305"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Certificados para o gateway de gestão da nuvem

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Consoante o cenário que utiliza para gerir clientes na internet com o gateway de gestão da cloud (CMG), precisa de um ou mais certificados digitais. Para obter mais informações sobre os diferentes cenários, consulte [plano para o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="cmg-server-authentication-certificate"></a>Certificado de autenticação de servidor CMG

*Este certificado é necessário em todos os cenários.*

Este certificado é fornecer ao criar CMG na consola do Configuration Manager.

O CMG cria um serviço HTTPS para o qual se ligar a clientes baseados na internet. O servidor requer um certificado de autenticação de servidor para criar o canal seguro. Comprar um certificado para esta finalidade de um fornecedor de público ou enviá-lo a partir da sua infraestrutura de chaves públicas (PKI). Para obter mais informações, consulte [certificado de raiz fidedigna do CMG para clientes](#cmg-trusted-root-certificate-to-clients).

 > [!TIP]
 > Este certificado requer um nome globalmente exclusivo para identificar o serviço no Azure. Antes de solicitar um certificado, confirme que o nome de domínio do Azure pretendido é exclusivo. Por exemplo, *GraniteFalls.CloudApp.Net*. Inicie sessão para o [portal do Microsoft Azure](https://portal.azure.com). Clique em **criar um recurso**, selecione a **computação** categoria, em seguida, clique em **serviço em nuvem**. Na **nome DNS** campo, escreva o prefixo pretendido, por exemplo *GraniteFalls*. A interface reflete se o nome de domínio está disponível ou já em utilização por outro serviço. Não criar o serviço no portal, basta usar este processo para verificar a disponibilidade de nome. 
  
 > [!NOTE]
 > A partir da versão 1802, o certificado de autenticação de servidor CMG suporta carateres universais. Alguns autoridades de certificação emitem certificados através de um caráter universal para o nome do anfitrião. Por exemplo,  **\*. contoso.com**. Algumas organizações utilizam certificados de caráter universal para simplificar seu PKI e reduzir os custos de manutenção.
 <!--491233-->


### <a name="cmg-trusted-root-certificate-to-clients"></a>Certificado de raiz fidedigna do CMG para clientes

Os clientes têm de confiar no certificado de autenticação de servidor do CMG. Existem dois métodos para realizar esta demonstração de confiança:
- Utilize um certificado de um fornecedor do certificado público e globalmente confiáveis. Por exemplo, mas não limitado a, DigiCert, Thawte ou VeriSign. Os clientes do Windows incluem autoridades de certificação de raiz fidedigna (AC) desses provedores. Ao utilizar um certificado de autenticação de servidor emitido por um destes fornecedores, os clientes automaticamente confiam nele. 
- Utilize um certificado emitido por uma AC empresarial da sua infraestrutura de chaves públicas (PKI). A maioria das implementações de PKI de empresa adicionar AC de raiz fidedigna para os clientes do Windows. Por exemplo, através dos serviços de certificados do Active Directory com a política de grupo. Se emitir o servidor CMG certificado de autenticação por uma AC não seja fidedigna automaticamente os seus clientes, terá de adicionar o certificado da AC de raiz fidedigna para os clientes baseados na internet.
    - Também pode utilizar perfis de certificado do Configuration Manager para provisionar certificados em clientes. Para obter mais informações, consulte [introdução aos perfis de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).

### <a name="server-authentication-certificate-issued-by-public-provider"></a>Certificado de autenticação de servidor emitido por fornecedor público

Quando utiliza este método, os clientes confiem automaticamente o certificado e não precisa de criar um certificado personalizado por conta própria. Com o domínio cloudapp.net, o Configuration Manager cria o serviço no Azure. Um fornecedor do certificado público não é possível emitir para um certificado com este nome. Utilize o seguinte processo para criar um alias de DNS:

1. Crie um registo de nome canónico (CNAME) no DNS público da sua organização. Este registo cria um alias para CMG para um nome amigável que utilize o certificado público.
Por exemplo, Contoso nomeia seus CMG **GraniteFalls**, que se torna **GraniteFalls.CloudApp.Net** no Azure. Na público contoso.com espaço de nomes DNS da Contoso, o administrador DNS cria um novo registo CNAME **GraniteFalls.Contoso.com** para o nome de anfitrião real **GraniteFalls.CloudApp.net**.
2. Pedir um certificado de autenticação de servidor do fornecedor público com o nome comum (CN) de CNAME alias.
Por exemplo, a Contoso utiliza **GraniteFalls.Contoso.com** para o CN do certificado.
3. Crie CMG na consola do Configuration Manager utilizando este certificado. Sobre o **definições** página do assistente Gateway de gestão na Cloud criar: 
    - Ao adicionar o certificado de servidor para este serviço cloud (partir **ficheiro de certificado**), o assistente extrai o nome de anfitrião do certificado CN como o nome do serviço. 
    - Ele anexa, em seguida, esse nome de anfitrião para **cloudapp.net**, ou **usgovcloudapp.net** da cloud do Azure US Government, como o FQDN de serviço para criar o serviço no Azure.
    - Por exemplo, quando Contoso cria o CMG, o Configuration Manager extrai o nome do anfitrião **GraniteFalls** do CN do certificado. O serviço real, como o Azure cria **GraniteFalls.CloudApp.net**.

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a>Certificado de autenticação de servidor emitido por enterprise PKI

Crie um certificado SSL personalizado para CMG o igual de um ponto de distribuição de nuvem. Siga as instruções para [implementar o certificado de serviço para pontos de distribuição baseado na nuvem](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012) mas efetue os seguintes procedimentos de forma diferente:

- Quando pedir o certificado de servidor web personalizado, fornece um FQDN para o nome comum do certificado. Isso pode ser um nome de domínio público que é proprietário ou pode aproveitar o domínio cloudapp.net. Se utilizar o seu próprio domínio público, consulte o processo acima para criar um alias de DNS no DNS público da sua organização.
- Quando utilizar o domínio cloudapp.net público para o certificado de servidor web do CMG, na cloud pública do Azure, utilizar um nome que termina em **cloudapp.net** ou **usgovcloudapp.net** para a cloud do Azure US Government.



## <a name="azure-management-certificate"></a>Certificado de gestão do Azure

*Este certificado é necessário para implementações de serviços clássico. Não é necessário para implementações do Azure Resource Manager.*

Este certificado no portal do Azure e fornecer ao criar CMG na consola do Configuration Manager.

Para criar CMG no Azure, a ligação de serviço do Configuration Manager ponto precisa primeiro autenticar para a sua subscrição do Azure. Quando utilizar uma implementação de serviço clássico, utiliza o certificado de gestão do Azure para esta autenticação. Um administrador do Azure carrega este certificado para a sua subscrição. Quando cria o CMG na consola do Configuration Manager, fornece este certificado.

Para obter mais informações e instruções sobre como carregar um certificado de gestão, veja os artigos seguintes na documentação do Azure:

- [Serviços cloud e gestão de certificados](/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)

- [Carregar um certificado de gestão de serviço do Azure](/azure/azure-api-management-certs)

> [!IMPORTANT]
> Certifique-se copiar o ID de subscrição associado ao certificado de gestão. Utilizá-lo para a criação de CMG na consola do Configuration Manager.



## <a name="client-authentication-certificate"></a>Certificado de autenticação de cliente

*Este certificado é necessário para clientes baseados na internet com o Windows 7, Windows 8.1 e dispositivos Windows 10 não associados ao Azure Active Directory (Azure AD). Também é necessário no ponto de ligação CMG. Não é necessário para clientes do Windows 10 associados ao Azure AD.*

Os clientes utilizam este certificado para autenticar com o CMG. Dispositivos Windows 10 que são híbrido ou na cloud associados a um domínio não requerem este certificado, porque utilizam o Azure AD para autenticar.

Aprovisione este certificado fora do contexto do Configuration Manager. Por exemplo, pode utilize os serviços de certificados do Active Directory e a política de grupo para emitir certificados de autenticação de cliente. Para obter mais informações, consulte [implementar o certificado de cliente para computadores Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).


### <a name="client-trusted-root-certificate-to-cmg"></a>Certificado de raiz fidedigna do cliente para CMG

*Este certificado é necessário quando utilizar certificados de autenticação de cliente. Quando todos os clientes utilizarem o Azure AD para autenticação, este certificado não é necessário.* 

Este certificado é fornecer ao criar CMG na consola do Configuration Manager.

O CMG têm de confiar os certificados de autenticação de cliente. Para realizar esta confiança, fornecem a cadeia de certificados de raiz fidedigna. Pode especificar duas AC de raiz fidedigna e quatro CAs (subordinada) intermediárias. 


#### <a name="export-the-client-certificates-trusted-root"></a>Exportar de raiz fidedigna do certificado de cliente

Depois de emitir um certificado de autenticação de cliente para um computador, utilize este processo nesse computador para exportar a raiz fidedigna.

1.  Abra o menu Iniciar. Escreva "executar" para abrir a janela de execução. Open **mmc**. 

2.  No menu ficheiro, escolha **Adicionar/Remover Snap-in...** .

3.  Na caixa de diálogo Adicionar ou Remover Snap-ins, selecione **certificados**, em seguida, clique em **Add**. 
    a. Na caixa de diálogo snap-in de certificados, selecione **conta de computador**, em seguida, clique em **próxima**. 
    b. Na caixa de diálogo Selecionar computador, selecione **computador Local**, em seguida, clique em **concluir**. 
    c. Na caixa de diálogo Adicionar ou Remover Snap-ins, clique em **OK**.

4.  Expanda **certificados**, expanda **pessoais**e selecione **certificados**.

5.  Selecione um certificado cujo objetivo pretendido é **autenticação de cliente**. 
    a. No menu ação, selecione **aberto**. 
    b. Mude para o **caminho de certificação** separador. c. Selecione o certificado seguinte na cadeia e clique em **Ver certificado**.

6.  Na caixa de diálogo certificado novo, mude para o **detalhes** separador. Clique em **copiar para ficheiro...** .

7.  Concluir o Assistente para exportar certificados utilizando o formato de certificado do predefinido, **binário codificado DER X.509 (. CER)**. Torne a nota do nome e localização do certificado exportado.

8. Exporte todos os certificados no caminho de certificação do certificado de autenticação de cliente original. Tome nota dos quais certificados exportados são CAs intermediárias e quais são as ACs de raiz fidedigna.



## <a name="enable-management-point-for-https"></a>Ativar o ponto de gestão para HTTPS

*Requisitos de certificado*
- Na versão 1706 ou 1710, quando gerir clientes tradicionais com locais identidade a utilizar um certificado de autenticação de cliente, este certificado é recomendado mas não obrigatório.
- Na versão 1710, quando a gestão de clientes do Windows 10 associados ao Azure AD, este certificado é necessário para pontos de gestão. 
- Este certificado a partir da versão 1802, é necessário em todos os cenários. Apenas os pontos de gestão que ativar para CMG tem de ser HTTPS. Esta alteração no comportamento fornece melhor suporte para autenticação baseada em tokens do AD do Azure. 

Aprovisione este certificado fora do contexto do Configuration Manager. Por exemplo, utilize os serviços de certificados do Active Directory e a política de grupo para emitir um certificado de servidor web. Para obter mais informações, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements) e [implementar o certificado de servidor web para sistemas de sites que executam o IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).



## <a name="next-steps"></a>Passos seguintes

- [Configurar o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Perguntas mais frequentes sobre o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Segurança e privacidade para o gateway de gestão na cloud ](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)

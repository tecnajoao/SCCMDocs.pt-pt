---
title: CMG segurança e privacidade
description: Saiba mais sobre as diretrizes e recomendações de segurança e privacidade com o gateway de gestão de nuvem.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971
ms.openlocfilehash: a850ea32fc06718c66d117702fb0a4bf1113a74c
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="security-and-privacy-for-the-cloud-management-gateway"></a>Segurança e privacidade para o gateway de gestão de nuvem

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo inclui a segurança e informações de privacidade para o gateway de gestão de nuvem do Configuration Manager (CMG). Para obter mais informações, consulte [planear para o gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).

## <a name="cmg-security-details"></a>Detalhes de segurança CMG
- O CMG aceita e gere ligações de CMG pontos de ligação. Utiliza a autenticação SSL mútua com certificados e os IDs de ligação.
- O CMG aceita e reencaminha os pedidos de cliente utilizando os seguintes métodos:
    - Pré-autentica ligações, utilizando SSL mútua com o certificado de autenticação de clientes baseada na PKI ou do Azure AD. 
      - IIS nas instâncias de CMG VM verifica o caminho do certificado com base no certificado de raiz fidedigna (s) carregado para o CMG.
      - IIS na instância de VM também verifica a revogação de certificados de cliente, se estiver ativada. Para obter mais informações, consulte [publicar a lista de revogação de certificados](#bkmk_crl).
    - A lista de fidedignidade de certificados verifica a raiz do certificado de autenticação de cliente. Também executa a validação do mesma como ponto de gestão para o cliente. Para obter mais informações, consulte [reveja entradas na lista de fidedignidade de certificados do site](#bkmk_ctl).
    - Valida e filtros de pedidos de cliente (URL) para verificar se a qualquer ponto de ligação CMG pode processar o pedido.  
    - Verifica o comprimento do conteúdo para cada ponto final de publicação.
    - Utiliza o comportamento de round robin para pontos de ligação do balanceamento de carga CMG no mesmo site.
- O ponto de ligação CMG utiliza os seguintes métodos:
    - Baseia-se ligações de HTTPS/TCP consistentes para todas as instâncias VM do CMG. Este verifica e mantém estas ligações a cada minuto.
    - Utiliza a autenticação mútua do SSL com CMG utilizando certificados.
    - Reencaminha os pedidos de cliente com base nos mapeamentos de URL.
    - Relatórios de estado de ligação para mostrar o estado de funcionamento do serviço na consola do.
    - Tráfego de relatórios por ponto final de cada cinco minutos.

### <a name="configuration-manager-client-facing-roles"></a>Funções de orientado para o cliente do Configuration Manager
A atualização de software e de ponto de gestão anfitrião pontos finais do ponto no IIS para servir pedidos do cliente. O CMG não expõe todos os pontos finais internos. Cada ponto final publicado para o CMG tem um mapeamento de URL.
  - O URL externo for um cliente utiliza para comunicar com o CMG.
  - O URL interno é o ponto de ligação de CMG utilizado para reencaminhar pedidos de servidor interno.

#### <a name="url-mapping-example"></a>Exemplo de mapeamento de URL
Quando ativar o tráfego de CMG num ponto de gestão, o Configuration Manager cria um conjunto de mapeamentos de URL para cada servidor de ponto de gestão interno. Por exemplo: ccm_system, ccm_incoming e sms_mp. O URL externo para o ponto final ccm_system de ponto de gestão pode ter o seguinte aspeto:  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
O URL é exclusivo para cada ponto de gestão. O cliente do Configuration Manager, em seguida, coloca o nome do ponto de gestão ativado para CMG na respetiva lista de pontos de gestão de internet. Este nome é aspeto:  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
O site carrega automaticamente todos os URLs externos publicados para o CMG. Este comportamento permite CMG fazer a filtragem de URL. Repliquem todos os mapeamentos de URL para o ponto de ligação CMG. Em seguida, encaminha a comunicação para servidores internos, de acordo com o URL externo no pedido do cliente.



## <a name="security-guidance-for-cmg"></a>Orientações de segurança para CMG


<a name="bkmk_crl"></a>

### <a name="publish-the-certificate-revocation-list"></a>Publicar a lista de revogação de certificados

Publica a lista de revogação de certificados do PKI (CRL) para clientes baseados na internet aceder. Quando implementar um CMG com PKI, configurar o serviço para **verificar a revogação de certificado de cliente** no separador Definições. Esta definição configura o serviço para utilizar uma lista de revogação de certificados publicados (CRL). Para obter mais informações, consulte [planear a revogação de certificados PKI](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs).



<a name="bkmk_ctl"></a>

### <a name="review-entries-in-the-sites-certificate-trust-list"></a>Reveja as entradas na lista de fidedignidade de certificados do site
<!--503739-->
Cada site do Configuration Manager inclui uma lista de autoridades de certificação de raiz fidedigna, a lista de fidedignidade de certificados (CTL). Ver e modificar a lista acedendo à área de trabalho administração, expanda configuração do Site e selecionar Sites. Selecione um site e clique em propriedades no Friso. Mudar para o separador comunicação com o computador cliente e, em seguida, clique em **definir** em autoridades de certificação de raiz fidedigna.
 
Utilize uma CTL mais restritiva para um site com um CMG utilizando a autenticação de cliente PKI. Caso contrário, os clientes com certificados de autenticação de cliente emitidos por qualquer raiz fidedigna que já existe no ponto de gestão são automaticamente aceites para o registo de cliente.

Este subconjunto proporciona os administradores de com mais controlo sobre segurança. A CTL restringe o servidor para aceitar apenas os certificados de cliente que são emitidos a partir de autoridades de certificação na CTL. Por exemplo, o Windows é fornecido com um número de certificados de autoridade (AC) de certificação de terceiros conhecidas, como VeriSign e a Thawte. Por predefinição, o computador que executa o IIS confianças certificados que se encadeiam estas ACs bem conhecidos. Sem configurar o IIS com uma CTL, qualquer computador que tenha um certificado de cliente emitido por estas ACs são aceites como um cliente válido do Configuration Manager. Se configurar o IIS com uma CTL que não inclua estas ACs, ligações de cliente serão recusadas se o certificado encadear estas ACs. 


<!--486209-->


<!-- ## Privacy information for CMG -->


## <a name="next-steps"></a>Passos seguintes

- [Planear o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Configurar o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Perguntas mais frequentes sobre o gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Certificados para o gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)

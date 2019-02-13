---
title: CMG de segurança e privacidade
description: Saiba mais sobre as orientações e recomendações de segurança e privacidade com o gateway de gestão na cloud.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971
ms.collection: M365-identity-device-management
ms.openlocfilehash: 013d00fd7c207df45b0f6b7910283c3e8b60b44d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137175"
---
# <a name="security-and-privacy-for-the-cloud-management-gateway"></a>Segurança e privacidade para o gateway de gestão da nuvem

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo inclui a segurança e informações de privacidade para o gateway de gestão do Configuration Manager na cloud (CMG). Para obter mais informações, consulte [planear para o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).

## <a name="cmg-security-details"></a>Detalhes de segurança do CMG
- O CMG aceita e gere ligações a partir de pontos de ligação do CMG. Ele usa a autenticação SSL mútua com certificados e IDs de ligação.
- O CMG aceita e reencaminha os pedidos de cliente através dos seguintes métodos:
    - Pré-autentica ligações através de SSL mútua com o certificado de autenticação de clientes baseada na PKI ou do Azure AD. 
      - O IIS nas instâncias de VM de CMG verifica se o caminho de certificado com base no certificado de raiz fidedigna (s) carregado para o CMG.
      - IIS na instância de VM também verifica a revogação de certificados de cliente, se estiver ativada. Para obter mais informações, consulte [publicar a lista de revogação de certificados](#bkmk_crl).
    - A lista de confiança de certificados verifica a raiz do certificado de autenticação de cliente. Também realiza a validação mesmo que o ponto de gestão para o cliente. Para obter mais informações, consulte [reveja as entradas na lista de confiança de certificados do site](#bkmk_ctl).
    - Valida e filtros de pedidos de cliente (URLs) para verificar se a qualquer ponto de ligação do CMG pode responder ao pedido.  
    - Verifica o comprimento do conteúdo para cada ponto de final de publicação.
    - Utiliza o comportamento de round robin para pontos de ligação do CMG de balanceamento de carga no mesmo site.
- O ponto de ligação do CMG utiliza os seguintes métodos:
    - Baseia-se as ligações HTTPS/TCP consistentes em todas as instâncias VM do CMG. Ele verifica e mantém estas ligações a cada minuto.
    - Utiliza a autenticação mútua de SSL com o CMG com certificados.
    - Por sua vez encaminha os pedidos de cliente com base nos mapeamentos de URL.
    - Estado da ligação de relatórios para mostrar o estado de funcionamento do serviço na consola do.
    - Tráfego de relatórios por ponto final a cada cinco minutos.

### <a name="configuration-manager-client-facing-roles"></a>Funções de com clientes do Configuration Manager
A atualização de software e de ponto de gestão anfitrião pontos finais do ponto no IIS para pedidos de cliente do serviço. O CMG não expõe todos os pontos de extremidade internos. Cada ponto de extremidade publicado para CMG tem um mapeamento de URL.
  - O URL externo é o cliente utiliza para comunicar com o CMG.
  - O URL interno é o ponto de ligação do CMG usado para encaminhar pedidos para o servidor interno.

#### <a name="url-mapping-example"></a>Exemplo de mapeamento de URL
Quando ativar o tráfego CMG no ponto de gestão, o Configuration Manager cria um conjunto interno de mapeamentos de URL para cada servidor de ponto de gestão. Por exemplo: ccm_system, ccm_incoming e sms_mp. O URL externo para o ponto final de ccm_system de ponto de gestão pode ter o seguinte aspeto:  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
O URL é exclusivo para cada ponto de gestão. O cliente do Configuration Manager, em seguida, coloca o nome do ponto de gestão ativado para CMG em sua lista de pontos de gestão de internet. Este nome é semelhante a:  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
O site carrega automaticamente todos os URLs externos publicados para CMG. Este comportamento permite que o CMG fazer a filtragem de URL. Todos os mapeamentos de URL replicar para o ponto de ligação do CMG. Em seguida, encaminha a comunicação para servidores internos, de acordo com o URL externo no pedido de cliente.



## <a name="security-guidance-for-cmg"></a>Orientações de segurança para CMG


<a name="bkmk_crl"></a>

### <a name="publish-the-certificate-revocation-list"></a>Publicar a lista de revogação de certificados

Publicar a lista de revogação de certificados de sua PKI (CRL) para clientes baseados na internet aceder. Ao implementar um CMG com PKI, configurar o serviço para **verificar revogação de certificados de cliente** no separador Definições. Esta definição configura o serviço para utilizar uma lista de revogação de certificados publicados (CRL). Para obter mais informações, consulte [planear a revogação de certificados PKI](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs).



<a name="bkmk_ctl"></a>

### <a name="review-entries-in-the-sites-certificate-trust-list"></a>Reveja as entradas na lista de confiança de certificados do site
<!--503739--> Cada site do Configuration Manager inclui uma lista de autoridades de certificação de raiz fidedigna, a lista de confiança de certificados (CTL). Ver e modificar a lista ao aceder à área de trabalho administração, expanda configuração do Site e selecione Sites. Selecione um site e clique em propriedades na faixa de opções. Mude para o separador de comunicação do computador cliente e, em seguida, clique em **definir** em autoridades de certificação de raiz fidedigna.
 
Utilize uma CTL mais restritiva para um site com um CMG com a autenticação de cliente PKI. Caso contrário, os clientes com certificados de autenticação de cliente emitidos por qualquer de raiz fidedigna que já existe no ponto de gestão são automaticamente aceites para o registo de cliente.

Este subconjunto proporciona aos administradores mais controle sobre segurança. A CTL restringe o servidor para apenas aceitar certificados de cliente que são emitidos pelas autoridades de certificação na CTL. Por exemplo, o Windows é fornecido com um número de certificados de autoridade (CA) de certificação de terceiros conhecidas, como VeriSign e a Thawte. Por predefinição, o computador que executa o IIS confianças certificados que se encadeiam essas CAs conhecidas. Sem configurar o IIS com uma CTL, qualquer computador que tenha um certificado de cliente emitido por estas ACs é aceite como um cliente válido do Configuration Manager. Se configurar o IIS com uma CTL que não inclua estas ACs, ligações de cliente serão recusadas se o certificado encadear estas ACs. 


<!--486209-->


<!-- ## Privacy information for CMG -->


## <a name="next-steps"></a>Passos seguintes

- [Planear o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Configurar o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Perguntas mais frequentes sobre o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Certificados para o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)

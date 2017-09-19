---
title: Preparar para implementar o software de cliente para Macs | Microsoft Docs
description: "Tarefas de configuração antes de implementar o cliente do Configuration Manager em Mac."
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
caps.latest.revision: "12"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 06dd4afe94c97b1ffd7d136666fddc623933fcd6
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/15/2017
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Preparar para implementar o software de cliente para Macs

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Siga estes passos para se certificar de que está pronto para [implementar o cliente do Configuration Manager em computadores Mac](/sccm/core/clients/deploy/deploy-clients-to-macs). 

## <a name="mac-prerequisites"></a>Pré-requisitos de MAC

O pacote de instalação de cliente de Mac não é fornecido com o suporte de dados do Configuration Manager. Transferir o **clientes para sistemas operativos adicionais** do [Centro de transferências da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

**Versões suportadas:**  

-   **Mac OS X 10.6** (Snow Leopard) 

-   **Mac OS X 10.7** (Lion) 

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.9** (Mavericks)  

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)  

## <a name="certificate-requirements"></a>Requisitos de certificados
Instalação de cliente e gestão para computadores Mac necessita de certificados de infraestrutura de chaves públicas (PKI). Os certificados PKI protegem a comunicação entre os computadores Mac e o site do Configuration Manager utilizando a autenticação mútua e das transferências de dados encriptados. O Configuration Manager pode pedir e instalar um certificado de cliente do utilizador através da utilização dos serviços de certificados da Microsoft com uma autoridade de certificação (AC) empresarial e os Configuration Manager inscrição inscrição e de ponto de proxy ponto site funções de sistema. Em alternativa, pode pedir e instalar um certificado de computador independentemente do Configuration Manager se o certificado cumprir os requisitos para o Configuration Manager.   
  
Os clientes do Configuration Manager Mac sempre efetuam a verificação de revogação do certificado. Não é possível desativar esta função.  
  
Se os clientes Mac não conseguirem confirmar o estado de revogação de certificado para um certificado de servidor porque não é possível localizar a CRL, eles não poderá ligar com êxito aos sistemas de sites do Configuration Manager. Especialmente para os clientes Mac numa floresta estranha para a autoridade de certificação emissora, verifique a estrutura da CRL para garantir que os clientes Mac conseguem localizar e ligar a um ponto de distribuição de CRL (CDP) para ligar servidores do sistema de sites.  

Antes de instalar o cliente do Configuration Manager num computador Mac, decida como instalar o certificado de cliente:  

-   Utilize o Gestor de configuração de inscrição utilizando o [ferramenta CMEnroll](/sccm/core/clients/deploy/deploy-clients-to-macs#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). O processo de inscrição não suporta a renovação automática de certificados, pelo que terá de reinscrever os computadores Mac antes que o certificado instalado expire.  

-   [Utilize um método de pedido e instalação de certificado que seja independente do Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager).  

Para obter mais informações sobre o requisito de certificado de cliente Mac e outros certificados PKI que são necessários para suportar computadores Mac, consulte [requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

Os clientes Mac são automaticamente atribuídos ao site do Configuration Manager que os gere. Os clientes Mac são instalados como clientes apenas de Internet, mesmo que a comunicação seja limitada à intranet. Esta configuração de cliente significa que estes clientes irão comunicar com as funções de sistema de sites (pontos de gestão e pontos de distribuição) no respetivo site atribuído quando estas funções de sistema de sites forem configuradas para permitirem ligações de cliente a partir da Internet. Os computadores Mac não comunicam com as funções do sistema de sites fora do respetivo site atribuído.  

> [!IMPORTANT]  
>  O cliente do Configuration Manager Mac não pode ser utilizado para ligar a um ponto de gestão que está configurado para utilizar um [réplica de base de dados](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  


## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Implementar um certificado de servidor web nos servidores de sistema de sites  
Se não tem estes sistemas de site, implemente um certificado de servidor web para os computadores que têm estas funções de sistema de sites:  

-   Ponto de gestão  

-   Ponto de distribuição  

-   Ponto de inscrição  

-   Ponto proxy de registo  

O certificado de servidor Web tem de conter o FQDN de Internet que se encontra especificado nas propriedades do sistema de sites. O servidor não tem de estar acessível a partir da Internet para suportar computadores Mac. Se não necessitar de gestão de clientes baseados na Internet, pode especificar o valor do FQDN de intranet para o FQDN de Internet.  

Especifique o valor de FQDN de Internet de um sistema de sites no certificado de servidor web para o ponto de gestão, o ponto de distribuição e o ponto de proxy de inscrição. 

Para um exemplo de implementação que cria e instala este certificado de servidor web, consulte o [implementar o certificado de servidor Web para sistemas de sites que executam o IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Implementar um certificado de autenticação de cliente nos servidores de sistema de sites  
 Se não tem estes sistemas de site, implemente um certificado de autenticação de cliente para computadores que alojam estas funções de sistema de sites:  

-   Ponto de gestão  

-   Ponto de distribuição  

 Para um exemplo de implementação que cria e instala o certificado de cliente para pontos de gestão, consulte o [implementar o cliente certificados para computadores com o Windows](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)  

 Para um exemplo de implementação que cria e instala o certificado de cliente para pontos de distribuição, consulte o [implementar o certificado de cliente para pontos de distribuição](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

>[!IMPORTANT]
>  Para implementar o cliente para dispositivos que executem macOS Sierra, o nome do requerente do certificado de ponto de gestão tem de ser configurado corretamente, por exemplo, utilizando o FQDN do servidor de ponto de gestão.

## <a name="prepare-the-client-certificate-template-for-macs"></a>Preparar o cliente do modelo de certificado para Macs  

 O modelo de certificado tem de ter permissões de **Leitura** e de **Inscrição** para a conta de utilizador que irá inscrever o certificado no computador Mac.  

 Consulte [implementar o certificado de cliente para computadores Mac](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  

## <a name="configure-the-management-point-and-distribution-point"></a>Configurar o ponto de gestão e o ponto de distribuição  
 Configure pontos de gestão para as seguintes opções:  

-   HTTPS  

-   Permite ao cliente ligações da Internet. Este valor de configuração é necessário para gerir computadores Mac. No entanto, não significa que os servidores de sistema de sites tenham de estar acessíveis a partir da Internet.  

-   Permitir que os dispositivos móveis e computadores Mac utilizem este ponto de gestão  

 Apesar dos pontos de distribuição não serem necessários para instalar o cliente, tem de configurar pontos de distribuição para permitir ligações a partir da Internet de cliente se pretender implementar software nestes computadores após a instalação do cliente.  

 
### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Para configurar pontos de gestão e pontos de distribuição para suportar Macs  

Antes de iniciar este procedimento, certifique-se de que o servidor do sistema de sites que executa o ponto de gestão e o ponto de distribuição está configurado com um FQDN de Internet. Se estes servidores não suportarem a gestão de clientes baseados na Internet, pode especificar o FQDN de intranet como o valor de FQDN de Internet. 

As funções de sistema de sites tem de ser um site primário.  


1.  Na consola do Configuration Manager, escolha **administração** > **configuração do Site** > **servidores e funções de sistema de sites**e, em seguida, selecione o servidor que tenha as funções do sistema de site correta.  

3.  No painel de detalhes, faça duplo clique **ponto de gestão**, escolha **propriedades da função**e, no **propriedades do ponto de gestão** diálogo caixa, configure estas opções:  

    1.  Escolha **HTTPS**.  

    2.  Escolha **permitir ligações de cliente apenas à Internet** ou **permitir ligações de cliente de Internet e intranet**. Estas opções necessitam de um Internet ou o FQDN da intranet.  

    3.  Escolha **permitir dispositivos móveis e computadores Mac utilizem este ponto de gestão**.  

4.  No painel de detalhes, faça duplo clique **ponto de distribuição**, escolha **propriedades da função**e, no **propriedades do ponto de distribuição** diálogo caixa, configure estas opções:  

    -   Escolha **HTTPS**.  

    -   Escolha **permitir ligações de cliente apenas à Internet** ou **permitir ligações de cliente de Internet e intranet**. Estas opções necessitam de um Internet ou o FQDN da intranet.  

    -   Escolha **importar certificado**, procure o ficheiro de certificado de ponto de distribuição de cliente exportado e, em seguida, especifique a palavra-passe.  

5.  Repita os passos 2 a 4 para todos os pontos de gestão e pontos de distribuição em sites primários que irá utilizar com Macs.  

## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Configurar o ponto de proxy de inscrição e o ponto de inscrição  
 Tem de instalar ambas as funções de sistema de sites no mesmo site, mas não tem de as instalar no mesmo servidor de sistema de sites ou na mesma floresta do Active Directory.  

 Para obter mais informações sobre o posicionamento de funções de sistema de sites e considerações, consulte [funções do sistema de sites](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) no [planear servidores de sistema de sites e funções de sistema de sites para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 Estes procedimentos configuram as funções de sistema de sites para suportar computadores Mac.   

-   [Novo servidor do sistema de sites](#new-site-system-server)  

-   [Servidor do sistema de sites existente](#existing-site-system-server)  

###  <a name="new-site-system-server"></a>Novo servidor do sistema de sites  

1.  Na consola do Configuration Manager, escolha **administração** >  **configuração do Site** > **servidores e funções de sistema de sites**  

3.  No **home page** separador o **criar** grupo, escolha **criar servidor do sistema de sites**.  

4.  No **geral** página, especifique as definições gerais para o sistema de sites.  Certifique-se de que especifica um valor para o FQDN de Internet. Se o servidor não estar acessível a partir da Internet, utilize o FQDN da intranet.  

5.  No **seleção da função do sistema** página, selecione **ponto proxy de registo** e **ponto de registo** da lista de funções disponíveis.  

6.  No **ponto Proxy de registo** página, reveja as definições e efetue as alterações necessárias.  

7.  No **definições do ponto de inscrição** página, reveja as definições e efetue as alterações necessárias. Em seguida, conclua o assistente.  

### <a name="existing-site-system-server"></a>Servidor do sistema de sites existente  

1.  Na consola do Configuration Manager, escolha **administração** >  **configuração do Site** > **servidores e funções de sistema de sites**e, em seguida, selecione o servidor que pretende utilizar para suportar Macs.  

3.  No **home page** separador o **criar** grupo, escolha **adicionar funções do sistema de sites**.  

4.  Na página **Geral** , especifique as definições gerais do sistema de sites e clique em **Seguinte**. Certifique-se de que especifica um valor para o FQDN de Internet. Se o servidor não estar acessível a partir da Internet, utilize o FQDN da intranet.   

5.  No **seleção da função do sistema** página, escolha **ponto proxy de registo** e **ponto de registo** da lista de funções disponíveis.  

6.  No **ponto Proxy de registo** página, reveja as definições e efetue as alterações necessárias.  

7.  No **definições do ponto de inscrição** página, reveja as definições e efetue as alterações necessárias. Em seguida, conclua o assistente.  

## <a name="install-the-reporting-services-point"></a>Instalar o ponto do reporting services  
 [Instalar o ponto do reporting services](../../../core/servers/manage/configuring-reporting.md) se pretender executar relatórios para Macs.  

### <a name="next-steps"></a>Passos seguintes

[Implementar o cliente do Configuration Manager em computadores Mac](/sccm/core/clients/deploy/deploy-clients-to-macs).  
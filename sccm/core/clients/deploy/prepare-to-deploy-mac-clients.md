---
title: Preparar para implementar o cliente para os Macs
titleSuffix: Configuration Manager
description: Tarefas de configuração antes de implantar o cliente do Configuration Manager para os Macs.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a7fc0a7ca3dd6974d1c97445d69b8f6032e81835
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52455908"
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Preparar a implementação de software de cliente para os Macs

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Siga estes passos para se certificar de que está pronto para [implementar o cliente do Configuration Manager em computadores Mac](/sccm/core/clients/deploy/deploy-clients-to-macs).



## <a name="mac-prerequisites"></a>Pré-requisitos de MAC

O pacote de instalação de cliente de Mac não é fornecido com o suporte de dados do Configuration Manager. Transfira o **clientes para sistemas operativos adicionais** partir o [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184).  

Para obter a lista de versões suportadas, consulte [sistemas operativos suportados por clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#mac-computers).



## <a name="certificate-requirements"></a>Requisitos de certificados

Instalação do cliente e gestão de computadores Mac necessita de certificados de infraestrutura de chaves públicas (PKI). Certificados PKI protegem a comunicação entre os computadores Mac e o site do Configuration Manager utilizando a autenticação mútua e transferências de dados encriptados. O Configuration Manager pode pedir e instalar um certificado de cliente do utilizador. Ele usa os serviços de certificados com uma autoridade de certificação empresarial e o ponto de registo do Configuration Manager e o ponto proxy de registo. Também pode pedir e instalar um certificado de computador independentemente do Configuration Manager. Este certificado tem de cumprir os requisitos de certificado do Configuration Manager.  

Os clientes do Configuration Manager Mac sempre verificar revogação de certificados. Não é possível desativar esta função.  

Se os clientes Mac não é possível localizar a lista de revogação de certificados (CRL), eles não é possível ligar a sistemas de sites do Configuration Manager. Especialmente para os clientes Mac numa floresta diferente para a autoridade de certificação emissora, verifique a estrutura da CRL. Certifique-se de que os clientes Mac podem localizar e transferir uma CRL.  

Antes de instalar o cliente do Configuration Manager num computador Mac, decida como instalar o certificado de cliente:  

-   Utilize o Gestor de configuração a inscrição através do [ferramenta CMEnroll](/sccm/core/clients/deploy/deploy-clients-to-macs#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). O processo de inscrição não suporta a renovação automática. Voltar a inscrever computadores Mac antes do certificado expira.  

-   [Utilizar um método de pedido e instalação de certificado independente do Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager).  

Para obter mais informações sobre os requisitos de certificado de cliente Mac, consulte [requisitos de certificado PKI para o Configuration Manager](/sccm/core/plan-design/network/pki-certificate-requirements).  

Os clientes Mac são automaticamente atribuídos ao site do Configuration Manager que os gere. Os clientes Mac são instalados como clientes apenas na internet, mesmo que a comunicação é limitada à intranet. Esta configuração significa que comunicam com pontos de gestão de acesso à internet e os pontos de distribuição no respetivo site atribuído. Computadores Mac não comunicam com sistemas de sites fora do respetivo site atribuído.  

> [!IMPORTANT]  
>  O cliente do Configuration Manager para macOS não pode ser utilizado para ligar a um ponto de gestão que está configurado para utilizar um [réplica de base de dados](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  



## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Implementar um certificado de servidor web nos servidores do sistema de sites  

Se estes sistemas de sites não o tiver, implemente um certificado de servidor web para os computadores que têm estas funções de sistema de sites:  

-   Ponto de gestão  

-   Ponto de distribuição  

-   Ponto de inscrição  

-   Ponto proxy de registo  

O certificado de servidor web tem de incluir o FQDN especificado nas propriedades do sistema de sites da internet. O servidor não tem de ser acessível a partir da internet para suportar computadores Mac. Se não necessitar de gestão de clientes baseados na internet, pode especificar o valor FQDN de intranet para o FQDN de internet.  

Especifique o valor de FQDN de internet do sistema de site no certificado do servidor web para o ponto de gestão, o ponto de distribuição e o ponto de proxy de registo.

Para obter mais informações de um exemplo de implementação, consulte [implementar o certificado de servidor web para sistemas de sites que executam o IIS](/sccm/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Implementar um certificado de autenticação de cliente para servidores do sistema de sites  

Se estes sistemas de sites não o tiver, implemente um certificado de autenticação de cliente para os computadores que alojam estas funções de sistema de sites:  

-   Ponto de gestão  

-   Ponto de distribuição  

Para um exemplo de implementação que cria e instala o certificado de cliente para pontos de gestão, consulte a [implementar o certificado de cliente para computadores Windows](/sccm/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).  

Para um exemplo de implementação que cria e instala o certificado de cliente para pontos de distribuição, consulte a [implementar o certificado de cliente para pontos de distribuição](/sccm/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012).  

> [!IMPORTANT]  
>  Para implementar o cliente em dispositivos com macOS Sierra, o nome do requerente do certificado de ponto de gestão tem de ser configurado corretamente. Por exemplo, utilize o FQDN do servidor de ponto de gestão.  



## <a name="prepare-the-client-certificate-template-for-macs"></a>Preparar o cliente do modelo de certificado para os Macs  

O modelo de certificado tem de ter **leitura** e **inscrever** permissões para a conta de utilizador que inscreva o certificado no computador Mac.  

Para obter mais informações, consulte [implementar o certificado de cliente para computadores Mac](/sccm/plan-design/network/example-deployment-of-pki-certificates#BKMK_MacClient_SP1).  



## <a name="configure-the-management-point-and-distribution-point"></a>Configurar o ponto de gestão e o ponto de distribuição  

Configure pontos de gestão para as seguintes opções:  

-   HTTPS  

-   Permita ligações a partir da internet de cliente. Este valor de configuração é necessário para gerir computadores Mac. No entanto, isso não significa que os servidores de sistema de sites tem de ser acessíveis a partir da internet.  

-   Permitir que os dispositivos móveis e computadores Mac utilizem este ponto de gestão  

Pontos de distribuição não são necessários para instalar o cliente para Mac. Se pretender implementar software nestes computadores depois de instalar o cliente, configure pontos de distribuição para permitir ligações de cliente a partir da internet.  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Para configurar pontos de gestão e pontos de distribuição para suportar Macs  

Antes de iniciar este procedimento, certifique-se configurar o ponto de gestão e o ponto de distribuição com um FQDN de internet. Se estes servidores não suportam a gestão de clientes baseados na internet, especifique o FQDN de intranet como o FQDN de internet valor.

As funções de sistema de sites tem de ser um site primário.  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **servidores e funções de sistema de sites** nó. Em seguida, selecione o servidor com as funções do sistema de site certo.  

2.  No painel de detalhes, selecione o **ponto de gestão** função e selecione **propriedades** na faixa de opções. Na **propriedades do ponto de gestão** janela, configurar estas opções:  

    1.  Escolher **HTTPS**.  

    2.  Escolher **permitir ligações de cliente apenas de internet** ou **permitir ligações de cliente a intranet e internet**. Estas opções requerem uma internet ou o FQDN da intranet.  

    3.  Escolher **permitir que dispositivos móveis e computadores Mac utilizem este ponto de gestão**.  

    4. Selecione **OK** para guardar esta configuração.  

3.  No painel de detalhes do nó de servidor e funções de sistema de sites, selecione o **ponto de distribuição** função e selecione **propriedades** na faixa de opções. Na **propriedades do ponto de distribuição** janela, configurar estas opções:  

    -   Escolher **HTTPS**.  

    -   Escolher **permitir ligações de cliente apenas de internet** ou **permitir ligações de cliente a intranet e internet**. Estas opções requerem uma internet ou o FQDN da intranet.  

    -   Escolher **importar certificado**, procure o ficheiro de certificado de ponto de distribuição de cliente exportado e, em seguida, especifique a palavra-passe.  

4.  Repita este procedimento para todos os pontos de gestão e pontos de distribuição em sites primários que gerem os computadores Mac.  



## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Configurar o ponto de proxy de registo e o ponto de inscrição  

Instale ambas as funções no mesmo site. Não tem de instalá-los no mesmo servidor de sistema do site ou na mesma floresta do Active Directory.  

Para obter mais informações sobre o posicionamento de funções de sistema de sites e considerações, consulte [funções do sistema de sites](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles#bkmk_planroles).  

Estes procedimentos configuram as funções de sistema de sites para suportar computadores Mac:   

-   [Novo servidor de sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles#to-install-site-system-roles-on-a-new-site-system-server)  

-   [Servidor de sistema de sites existente](/sccm/core/servers/deploy/configure/install-site-system-roles#bkmk_Install)    

Em ambos os casos, sobre o **seleção da função do sistema** página, selecione **ponto proxy de registo** e **ponto de registo** na lista de funções disponíveis.  



## <a name="install-the-reporting-services-point"></a>Instalar o ponto do reporting services  

Para obter mais informações, consulte [instalar o ponto do reporting services](/sccm/core/servers/manage/configuring-reporting).  



## <a name="next-steps"></a>Passos seguintes

[Implementar o cliente do Configuration Manager em computadores Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)  

---
title: Bloqueio de clientes | Microsoft Docs
description: "Bloquear o acesso de cliente para segurança do sistema utilizando o System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54ef5fbb-521d-4ca5-a1c5-61e6f538d71e
caps.latest.revision: "8"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: b1d191485308a49c50f48e4b3a89c2fb96940d28
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/15/2017
---
# <a name="determine-whether-to-block-clients-in-system-center-configuration-manager"></a>Determinar se deve bloquear clientes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Se um computador cliente ou dispositivo móvel cliente já não é fidedigno, pode bloquear o cliente na consola do System Center 2012 Configuration Manager. Os clientes bloqueados são rejeitados pela infraestrutura do Configuration Manager para que não conseguem comunicar com sistemas de sites para transferir políticas, carregar dados de inventário ou enviar mensagens de estado.  

 O cliente deve ser bloqueado e desbloqueado a partir do site atribuído e não de um site secundário ou de um site de administração central.  

> [!IMPORTANT]  
>  Embora o bloqueio no Configuration Manager pode ajudar a proteger o site do Configuration Manager, não depender desta funcionalidade para proteger o site contra dispositivos móveis ou computadores não fidedignos se permitir que os clientes comuniquem com sistemas de sites através de HTTP, porque um cliente bloqueado pode passem o site com um novo autoassinado certificado e hardware ID. Em vez disso, utilize a funcionalidade de bloqueio para bloquear suportes de dados de arranque perdidos ou comprometidos, que utiliza para implementar sistemas operativos, e quando os sistemas de sites aceitam ligações de cliente por HTTPS.  

 Os clientes que acedem ao site utilizando o certificado de Proxy ISV não podem ser bloqueados. Para obter mais informações sobre o certificado de ISV Proxy, consulte o System Center Configuration Manager Software Development Kit (SDK).  

 Se os seus sistemas do site aceitarem ligações de cliente por HTTPS e a sua infraestrutura de chaves públicas (PKI) suportar uma lista de revogação de certificados (CRL), considere sempre a revogação de certificados como a primeira linha de defesa contra certificados potencialmente comprometidos. Bloqueio de clientes no Configuration Manager oferece uma segunda linha de defesa para proteger a hierarquia.  

##  <a name="BKMK_Block_vs_CRL"></a> Considerações para bloquear clientes  

-   Esta opção está disponível para ligações de cliente por HTTP e HTTPS, mas tem segurança limitada quando os clientes ligam aos sistemas do site por HTTP.  

-   Os utilizadores administrativos do Configuration Manager têm autoridade para bloquear um cliente e a ação é executada na consola do Configuration Manager.  

-   Comunicação do cliente é rejeitada da hierarquia do Configuration Manager apenas.  

    > [!NOTE]  
    >  O mesmo cliente pode registar de outra hierarquia do Configuration Manager.  

-   O cliente é imediatamente bloqueado no site do Configuration Manager.  

-   Ajuda a proteger os sistemas do site contra computadores e dispositivos móveis potencialmente comprometidos.  

## <a name="considerations-for-using-certificate-revocation"></a>Considerações sobre como utilizar a revogação de certificados  

-   Esta opção está disponível para ligações de cliente do Windows por HTTPS se a infraestrutura de chaves públicas suportar uma lista de revogação de certificados (CRL).  

     Os clientes Mac efetuam sempre a verificação CRL e esta funcionalidade não pode ser desativada.  

     Embora os clientes de dispositivos móveis não utilizem listas de revogação de certificados para verificar os certificados para os sistemas de sites, os certificados podem ser revogados e verificados pelo Configuration Manager.  

-   Os administradores da infraestrutura de chave pública tem autoridade para revogar um certificado e a ação é executada fora da consola do Configuration Manager.  

-   A comunicação do cliente a partir de qualquer computador ou dispositivo móvel que requeira este certificado de cliente pode ser rejeitada.  

-   É provável que haja um atraso entre a revogação de um certificado e a transferência pelos sistemas do site da lista de revogação de certificados (CRL) modificada.  

-   Para muitas implementações de PKI, este atraso pode demorar um dia ou mais. Por exemplo, nos Serviços de Certificados do Active Directory, o período de validade predefinido é uma semana para uma CRL completa e um dia para uma CRL de diferenças.  

-   Ajuda a proteger os sistemas do site e os clientes contra computadores e dispositivos móveis potencialmente comprometidos.  

    > [!NOTE]  
    >  É possível proteger ainda mais os sistemas do site que executam o IIS contra clientes desconhecidos, configurando uma lista fidedigna de certificados (CTL) no IIS.  

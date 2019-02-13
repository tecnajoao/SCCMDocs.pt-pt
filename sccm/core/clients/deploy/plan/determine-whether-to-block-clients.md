---
title: Bloqueio de clientes
titleSuffix: Configuration Manager
description: Bloquear o acesso de cliente para segurança do sistema com o System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 54ef5fbb-521d-4ca5-a1c5-61e6f538d71e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a90e100c242514eb2526e16bb68e379a2326572f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136920"
---
# <a name="determine-whether-to-block-clients-in-system-center-configuration-manager"></a>Determinar se deve bloquear clientes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Se um computador cliente ou dispositivo móvel cliente já não é fidedigno, pode bloquear o cliente na consola do System Center 2012 Configuration Manager. Os clientes bloqueados são rejeitados pela infraestrutura do Configuration Manager para que não conseguirem comunicar com sistemas de sites para transferir a política, carregar dados de inventário ou enviar mensagens de estado.  

 O cliente deve ser bloqueado e desbloqueado a partir do site atribuído e não de um site secundário ou de um site de administração central.  

> [!IMPORTANT]  
>  Embora o bloqueio no Configuration Manager pode ajudar a proteger o site do Configuration Manager, não confiar nesta funcionalidade para proteger o site a partir de dispositivos móveis ou computadores não fidedignos se permitir que os clientes comuniquem com sistemas de sites através de HTTP, porque um cliente bloqueado poderia voltar a participar do site com um novo autoassinado certificado e hardware ID. Em vez disso, utilize a funcionalidade de bloqueio para bloquear suportes de dados de arranque perdidos ou comprometidos, que utiliza para implementar sistemas operativos, e quando os sistemas de sites aceitam ligações de cliente por HTTPS.  

 Os clientes que acedem ao site utilizando o certificado de Proxy ISV não podem ser bloqueados. Para obter mais informações sobre o certificado de ISV Proxy, consulte o System Center Configuration Manager Software Development Kit (SDK).  

 Se os seus sistemas do site aceitarem ligações de cliente por HTTPS e a sua infraestrutura de chaves públicas (PKI) suportar uma lista de revogação de certificados (CRL), considere sempre a revogação de certificados como a primeira linha de defesa contra certificados potencialmente comprometidos. Bloqueio de clientes no Configuration Manager oferece uma segunda linha de defesa para proteger a hierarquia.  

##  <a name="BKMK_Block_vs_CRL"></a> Considerações para bloquear clientes  

-   Esta opção está disponível para ligações de cliente por HTTP e HTTPS, mas tem segurança limitada quando os clientes ligam aos sistemas do site por HTTP.  

-   Gestor de configuração de utilizadores administrativos têm autoridade para bloquear um cliente e a ação é executada na consola do Configuration Manager.  

-   Comunicação do cliente é rejeitada de apenas a hierarquia do Configuration Manager.  

    > [!NOTE]  
    >  O mesmo cliente podia registrar com uma hierarquia diferente do Configuration Manager.  

-   O cliente é imediatamente bloqueado no site do Configuration Manager.  

-   Ajuda a proteger os sistemas do site contra computadores e dispositivos móveis potencialmente comprometidos.  

## <a name="considerations-for-using-certificate-revocation"></a>Considerações sobre como utilizar a revogação de certificados  

-   Esta opção está disponível para ligações de cliente do Windows por HTTPS se a infraestrutura de chaves públicas suportar uma lista de revogação de certificados (CRL).  

     Os clientes Mac efetuam sempre a verificação CRL e esta funcionalidade não pode ser desativada.  

     Embora os clientes de dispositivos móveis não utilizar listas de revogação de certificados para verificar os certificados para sistemas de sites, seus certificados podem ser revogados e verificados pelo Configuration Manager.  

-   Os administradores de infraestrutura de chaves públicas têm autoridade para revogar um certificado e a ação é executada fora da consola do Configuration Manager.  

-   A comunicação do cliente a partir de qualquer computador ou dispositivo móvel que requeira este certificado de cliente pode ser rejeitada.  

-   É provável que haja um atraso entre a revogação de um certificado e a transferência pelos sistemas do site da lista de revogação de certificados (CRL) modificada.  

-   Para muitas implementações de PKI, este atraso pode demorar um dia ou mais. Por exemplo, nos Serviços de Certificados do Active Directory, o período de validade predefinido é uma semana para uma CRL completa e um dia para uma CRL de diferenças.  

-   Ajuda a proteger os sistemas do site e os clientes contra computadores e dispositivos móveis potencialmente comprometidos.  

    > [!NOTE]  
    >  É possível proteger ainda mais os sistemas do site que executam o IIS contra clientes desconhecidos, configurando uma lista fidedigna de certificados (CTL) no IIS.  

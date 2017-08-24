---
title: "Suportado domínios do Active Directory | Microsoft Docs"
description: "Obter os requisitos para a associação de um sistema de site do System Center Configuration Manager num domínio do Active Directory."
ms.custom: na
ms.date: 3/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 2654ab4eaaaf6a4bf3bd7dca9908e7033647dc2c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="supported-active-directory-domains-for-system-center-configuration-manager"></a>Domínios do Active Directory suportados para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Todos os sistemas de site do System Center Configuration Manager tem de ser membros de um domínio do Windows Server Active Directory suportado. Computadores de cliente do Configuration Manager podem ser membros do domínio ou membros do grupo de trabalho.  

 **Requisitos e limitações:**  

-   Associação ao domínio aplica-se a sistemas de sites que suportam a gestão de clientes baseada na Internet numa rede de perímetro (também conhecido como um DMZ, zona desmilitarizada e sub-rede filtrada).  

-   Não é suportado para alterar as seguintes opções para um computador que aloje uma função de sistema de sites:  

    -   Associação ao domínio  

    -   Nome do domínio  

    -   Nome do computador  

Tem de desinstalar a função de sistema de sites (incluindo o site se for um servidor do site) antes de efetuar estas alterações.  

**São suportados domínios com os seguintes níveis funcionais de domínio:**  
- Windows Server 2016

- Windows Server 2012 R2  

- Windows Server 2012

- Windows Server 2008 R2

- Windows Server 2008  







##  <a name="bkmk_Disjoint"></a> Espaço de nomes não contíguo  
O Configuration Manager suporta instalar sistemas de sites e clientes num domínio que tenha um espaço de nomes não contíguo.  

Um cenário de espaço de nomes não contíguo é uma em que o sufixo de sistema de nomes de domínio (DNS) primário de um computador não corresponde ao nome de domínio DNS do Active Directory onde reside nesse computador. O computador que utiliza o sufixo DNS primário que não corresponde ao possui correspondências é denominado não contíguo. Outro cenário espaço de nomes não contíguo ocorre se o nome de domínio NetBIOS de um controlador de domínio não corresponde ao nome de domínio DNS do Active Directory.  

A seguinte tabela identifica os cenários suportados de um espaço de nomes não contíguo.  

|Cenário|Mais informações|  
|--------------|----------------------|  
|**Cenário 1:**<br /><br /> O sufixo DNS primário do controlador de domínio difere do nome de domínio DNS do Active Directory. Os computadores que são membros do domínio podem estar não contíguos ou contíguos.|Neste cenário, o sufixo DNS primário do controlador de domínio difere do nome de domínio do Active Directory. O controlador de domínio está não contíguo neste cenário. Os computadores que são membros do domínio, como servidores de sites e computadores, podem ter um sufixo DNS primário que corresponda ao sufixo DNS primário do controlador de domínio ou ao nome de domínio DNS do Active Directory.|  
|**Cenário 2:**<br /><br /> Um computador membro num domínio do Active Directory é não contíguo, apesar de o controlador de domínio ser contíguo.|Neste cenário, o sufixo DNS primário de um computador membro no qual é instalado um sistema de sites difere do nome de domínio do Active Directory, apesar de o sufixo DNS primário do controlador de domínio ser o mesmo que o nome de domínio DNS do Active Directory. Neste cenário, tem um controlador de domínio que é contíguo e um computador membro que é não contíguo. Computadores de membro que executem o cliente do Configuration Manager podem ter um sufixo DNS primário que corresponda ao sufixo DNS principal do servidor do sistema de sites não contíguo ou corresponde ao nome de domínio DNS do Active Directory.|  

 Para permitir que um computador aceda a controladores de domínio que sejam não contíguos, tem de alterar o atributo do Active Directory **msDS-AllowedDNSSuffixes** no contentor de objetos do domínio. Tem de adicionar ambos os sufixos DNS para o atributo.  

 Além disso, para se certificar de que a lista de pesquisa de sufixos DNS contém todos os os espaços de nomes DNS que são implementados na sua organização, tem de configurar a lista de pesquisa para cada computador no domínio que é não contíguo. Certifique-se de que inclui o seguinte na lista de espaços de nomes: o sufixo DNS primário do controlador de domínio, o nome de domínio DNS e quaisquer espaços de nomes adicionais para outros servidores que o Configuration Manager podem interagir com. Pode utilizar a consola de Gestão de Políticas de Grupo para configurar a **Lista de Pesquisa de Sufixos DNS (Sistema de Nomes de Domínio)** .  

> [!IMPORTANT]  
>  Quando referenciar um computador no Configuration Manager, introduza o computador utilizando o respetivo sufixo DNS primário. Este sufixo deve corresponder ao nome completamente qualificado domínio que está registado como o **dnsHostName** atributo no domínio do Active Directory e o nome do Principal de serviço que estão associados com o sistema.  

##  <a name="bkmk_SLD"></a> Domínios de etiqueta única  
 O Configuration Manager suporta sistemas de sites e clientes num domínio de etiqueta única quando são cumpridos os seguintes critérios:  

-   O domínio de etiqueta única nos serviços de domínio do Active Directory tem de ser configurado com um espaço de nomes DNS não contíguo que tenha um domínio de nível superior válido.  

     **Por exemplo:** O domínio de etiqueta única da Contoso está configurado para ter um espaço de nomes não contíguo no DNS de contoso.com. Por conseguinte, quando especificar o sufixo DNS no Configuration Manager para um computador no domínio da Contoso, especifique "Contoso.com" e não "Contoso".  

-   As ligações de componente modelo DCOM (Distributed Object) entre servidores de sites no contexto do sistema tem de ser concluída com êxito utilizando a autenticação Kerberos.  

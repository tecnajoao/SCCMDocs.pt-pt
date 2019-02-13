---
title: Domínios do Active Directory suportados
titleSuffix: Configuration Manager
description: Obtenha os requisitos para a associação de um sistema de sites do System Center Configuration Manager num domínio do Active Directory.
ms.date: 9/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2babdf726d468d27d0fe2ab37ad99a101adbb74c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129566"
---
# <a name="supported-active-directory-domains-for-system-center-configuration-manager"></a>Domínios do Active Directory suportados para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Todos os sistemas de sites do System Center Configuration Manager têm de ser membros de um domínio do Active Directory do Windows Server suportado. Computadores de cliente do Configuration Manager podem ser membros do domínio ou membros do grupo de trabalho.  

 **Requisitos e limitações:**  

-   Associação ao domínio aplica-se aos sistemas de sites que suportam a gestão de clientes baseada na Internet numa rede de perímetro (também conhecido como um DMZ, zona desmilitarizada e sub-rede filtrada).  

-   Não é suportada para alterar as seguintes opções para um computador que aloje uma função de sistema de sites:  

    -   Associação ao domínio *(Isto inclui a remoção de um sistema de sites do domínio e, em seguida, rejoining mesmo domínio.)*

    -   Nome do domínio  

    -   Nome do computador  

Tem de desinstalar a função de sistema de sites (incluindo o site se for um servidor de site) antes de efetuar estas alterações.  

**São suportados domínios com os seguintes níveis funcionais de domínio:**  
- Windows Server 2016

- Windows Server 2012 R2  

- Windows Server 2012

- Windows Server 2008 R2

- Windows Server 2008  







##  <a name="bkmk_Disjoint"></a> Espaço de nomes não contíguo  
O Configuration Manager suporta a instalação de sistemas de sites e clientes num domínio que tenha um espaço de nomes não contíguo.  

Um cenário de espaço de nomes não contíguo é-um em que o sufixo de sistema de nomes de domínio (DNS) primário de um computador não corresponde ao nome de domínio DNS do Active Directory onde reside nesse computador. O computador que utiliza o sufixo DNS primário que não corresponde ao é conhecido como não contíguo. Outro cenário de espaço de nomes não contíguo ocorre se o nome de domínio NetBIOS de um controlador de domínio não corresponde ao nome de domínio DNS do Active Directory.  

A seguinte tabela identifica os cenários suportados de um espaço de nomes não contíguo.  

|Cenário|Mais informações|  
|--------------|----------------------|  
|**Cenário 1:**<br /><br /> O sufixo DNS primário do controlador de domínio difere do nome de domínio DNS do Active Directory. Os computadores que são membros do domínio podem estar não contíguos ou contíguos.|Neste cenário, o sufixo DNS primário do controlador de domínio difere do nome de domínio do Active Directory. O controlador de domínio está não contíguo neste cenário. Os computadores que são membros do domínio, como servidores de sites e computadores, podem ter um sufixo DNS primário que corresponda ao sufixo DNS primário do controlador de domínio ou ao nome de domínio DNS do Active Directory.|  
|**Cenário 2:**<br /><br /> Um computador membro num domínio do Active Directory é não contíguo, apesar de o controlador de domínio ser contíguo.|Neste cenário, o sufixo DNS primário de um computador membro no qual é instalado um sistema de sites difere do nome de domínio do Active Directory, apesar de o sufixo DNS primário do controlador de domínio ser o mesmo que o nome de domínio DNS do Active Directory. Neste cenário, tem um controlador de domínio que é contíguo e um computador membro que é não contíguo. Computadores de membro que executem o cliente do Configuration Manager podem ter um sufixo DNS primário que corresponda ao sufixo DNS primário do servidor do sistema de sites não contíguo ou ao nome de domínio DNS do Active Directory.|  

 Para permitir que um computador aceda a controladores de domínio que sejam não contíguos, tem de alterar o atributo do Active Directory **msDS-AllowedDNSSuffixes** no contentor de objetos do domínio. Tem de adicionar ambos os sufixos DNS para o atributo.  

 Além disso, para certificar-se de que a lista de pesquisa de sufixos DNS contém todos os espaços de nomes DNS que são implementados na organização, tem de configurar a lista de pesquisa para cada computador no domínio que seja não contíguo. Certifique-se de que inclui o seguinte na lista de espaços de nomes: o sufixo DNS primário do controlador de domínio e quaisquer espaços de nomes adicionais para outros servidores que o Configuration Manager poderá interagir com o nome de domínio DNS. Pode utilizar a consola de Gestão de Políticas de Grupo para configurar a **Lista de Pesquisa de Sufixos DNS (Sistema de Nomes de Domínio)** .  

> [!IMPORTANT]  
>  Quando referencia um computador no Configuration Manager, introduza o computador utilizando o respetivo sufixo DNS primário. Este sufixo deve corresponder ao nome completamente qualificado domínio que está registado como o **dnsHostName** atributo no domínio do Active Directory e o nome do Principal de serviço que estão associados com o sistema.  

##  <a name="bkmk_SLD"></a> Domínios de etiqueta única  
 O Configuration Manager suporta sistemas de sites e clientes num domínio de etiqueta única quando são cumpridos os seguintes critérios:  

-   O domínio de etiqueta única nos serviços de domínio do Active Directory tem de ser configurado com um espaço de nomes DNS não contíguo que tenha um domínio de nível superior válido.  

     **Por exemplo:** O domínio de etiqueta única da Contoso está configurado para ter um espaço de nomes não contíguo no DNS de contoso.com. Por conseguinte, quando especificar o sufixo DNS no Configuration Manager para um computador no domínio da Contoso, especifique "Contoso.com" e não "Contoso".  

-   As ligações de distribuídas componente objeto de modelo (DCOM) entre os servidores de site no contexto do sistema tem de ser concluída com êxito utilizando a autenticação Kerberos.  

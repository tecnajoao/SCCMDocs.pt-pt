---
title: Configurar o Endpoint Protection
titleSuffix: Configuration Manager
description: "Saiba como configurar o Configuration Manager para atualizar e distribuir definições de software maligno para o Windows Defender."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 5f005e7cd9c396fcf7e02aafefcb34c37ddab901
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="configure-endpoint-protection"></a>Configurar o Endpoint Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de poder utilizar o Endpoint Protection para gerir a segurança e software maligno em computadores de cliente do Configuration Manager, tem de efetuar os passos de configuração detalhados neste tópico.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Como Configurar o Endpoint Protection no Configuration Manager  
 Endpoint Protection no Configuration Manager tem dependências externas e dependências no produto.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Passos para configurar o Endpoint Protection no Configuration Manager  
 Utilize a tabela seguinte para obter os passos, detalhes e mais informações sobre como configurar o Endpoint Protection.  

> [!IMPORTANT]  
>  Se gerir o endpoint protection para computadores Windows 10, tem de configurar o Configuration Manager para atualizar e distribuir definições de software maligno para o Windows Defender. O Windows Defender está incluído no Windows 10, mas SCEPInstall ainda tem de ser as definições de cliente instalado e personalizadas para o Endpoint Protection (**passo 5** abaixo) ainda são necessárias.  

|Passos|Detalhes|  
|-----------|-------------|  
|**Passo 1:** [Criar uma função de sistema de sites de ponto de Endpoint Protection](endpoint-protection-site-role.md)|A função de sistema de sites de ponto do Endpoint Protection tem de ser instalada antes de poder utilizar o Endpoint Protection. Tem de ser instalada apenas num servidor do sistema de sites e tem de ser instalada na parte superior da hierarquia num site de administração central ou num site primário autónomo. |  
|**Passo 2:** [Configurar alertas para o Endpoint Protection](endpoint-configure-alerts.md)|Os alertas informam o administrador quando ocorreram eventos específicos, tal como uma infeção de software maligno. Os alertas são apresentados no nó **Alertas** da área de trabalho **Monitorização** ou, opcionalmente, podem ser enviados por e-mail para utilizadores especificados. |  
|**Passo 3:** [Configurar origens de atualização de definição para clientes de Endpoint Protection](endpoint-definition-updates.md)|Endpoint Protection pode ser configurado para utilizar várias origens para transferir atualizações de definições. |  
|**Passo 4:** [Configurar a política antimalware predefinida e criar políticas antimalware personalizadas](endpoint-antimalware-policies.md)|A política antimalware predefinida é aplicada quando o cliente do Endpoint Protection está instalado. As políticas personalizadas que tiver implementado são aplicadas por predefinição num período de 60 minutos após implementar o cliente. Certifique-se de que configurou políticas antimalware antes de implementar o cliente do Endpoint Protection. |  
|**Passo 5:** [Configurar definições personalizadas de cliente do Endpoint Protection](endpoint-protection-configure-client.md)|Utilize definições personalizadas de cliente para configurar definições de Endpoint Protection para coleções de computadores na sua hierarquia.<br /><br /> Nota: Não configure as predefinições de cliente do Endpoint Protection, exceto se tiver a certeza de que pretende estas definições aplicadas a todos os computadores na sua hierarquia. |  

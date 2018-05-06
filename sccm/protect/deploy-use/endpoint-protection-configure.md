---
title: Configurar o Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como configurar o Configuration Manager para atualizar e distribuir definições de software maligno para o Windows Defender.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9dc5c79588c8d5211139f0614491d80ba7597f49
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="configure-endpoint-protection"></a>Configurar o Endpoint Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de poder utilizar o Endpoint Protection para gerir a segurança e software maligno em computadores de cliente do Configuration Manager, tem de efetuar os passos de configuração detalhados neste artigo.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Como Configurar o Endpoint Protection no Configuration Manager  
 Endpoint Protection no Configuration Manager tem dependências externas e dependências no produto.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Passos para configurar o Endpoint Protection no Configuration Manager  
 Utilize a tabela seguinte para obter os passos, detalhes e mais informações sobre como configurar o Endpoint Protection.  

> [!IMPORTANT]  
>  Se gerir o endpoint protection para computadores Windows 10, tem de configurar o Configuration Manager para atualizar e distribuir definições de software maligno para o Windows Defender. O Windows Defender está incluído no Windows 10, mas SCEPInstall ainda tem de ser as definições de cliente instalado e personalizadas para o Endpoint Protection (**passo 5** abaixo) ainda são necessárias. </br> </br>
> A partir do Configuration Manager 1802, dispositivos Windows 10 não é necessário ter o agente do Endpoint Protection (SCEPInstall) instalado. Se já estiver instalado em dispositivos Windows 10, o Configuration Manager não removê-lo. Os administradores podem remover o agente do Endpoint Protection em dispositivos Windows 10 que estejam a executar, pelo menos, a versão do cliente 1802. SCEPInstall.exe ainda pode estar presente nos C:\Windows\ccmsetup algumas máquinas, mas não deve ser transferido em novas instalações de cliente. Definições de cliente personalizadas para o Endpoint Protection (**passo 5** abaixo) ainda são necessárias. <!--503654-->

|Passos|Detalhes|  
|-----------|-------------|  
|**Passo 1:** [Criar uma função de sistema de sites de ponto de Endpoint Protection](endpoint-protection-site-role.md)|A função de sistema de sites de ponto do Endpoint Protection tem de ser instalada antes de poder utilizar o Endpoint Protection. Tem de ser instalada apenas num servidor do sistema de sites e tem de ser instalada na parte superior da hierarquia num site de administração central ou num site primário autónomo. |  
|**Passo 2:** [Configurar alertas para o Endpoint Protection](endpoint-configure-alerts.md)|Os alertas informam o administrador quando ocorreram eventos específicos, tal como uma infeção de software maligno. Os alertas são apresentados no nó **Alertas** da área de trabalho **Monitorização** ou, opcionalmente, podem ser enviados por e-mail para utilizadores especificados. |  
|**Passo 3:** [Configurar origens de atualização de definição para clientes de Endpoint Protection](endpoint-definition-updates.md)|Endpoint Protection pode ser configurado para utilizar várias origens para transferir atualizações de definições. |  
|**Passo 4:** [Configurar a política antimalware predefinida e criar políticas antimalware personalizadas](endpoint-antimalware-policies.md)|A política antimalware predefinida é aplicada quando o cliente do Endpoint Protection está instalado. As políticas personalizadas que tiver implementado são aplicadas por predefinição num período de 60 minutos após implementar o cliente. Certifique-se de que configurou políticas antimalware antes de implementar o cliente do Endpoint Protection. |  
|**Passo 5:** [Configurar definições personalizadas de cliente do Endpoint Protection](endpoint-protection-configure-client.md)|Utilize definições personalizadas de cliente para configurar definições de Endpoint Protection para coleções de computadores na sua hierarquia.<br /><br /> Nota: Não configure as predefinições de cliente do Endpoint Protection, exceto se tiver a certeza de que pretende estas definições aplicadas a todos os computadores na sua hierarquia. |  

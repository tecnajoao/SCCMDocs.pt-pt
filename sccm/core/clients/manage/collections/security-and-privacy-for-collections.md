---
title: "Coleções de segurança e privacidade | Documentos do Microsoft"
description: "Obter melhores práticas de segurança e privacidade no coleções no System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
caps.latest.revision: 5
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9c5d1e48b76392beaf54b5377c69b648537e86f8
ms.openlocfilehash: 0cade975e96220e193db1de92816f97cd253532d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="security-and-privacy-for-collections-in-system-center-configuration-manager"></a>Segurança e privacidade para coleções no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém melhores práticas de segurança e informações de privacidade para coleções no System Center Configuration Manager.  

 Não existe nenhum informações de privacidade especificamente para coleções no Configuration Manager. As coleções são contentores de recursos, tais como utilizadores e dispositivos. Associação à coleção depende frequentemente das informações que o Configuration Manager recolhe durante o funcionamento normal. Por exemplo, através da utilização de informações de recursos que tenham sido recolhidas pela deteção ou inventário, uma coleção pode ser configurada para conter os dispositivos que cumprem critérios específicos. As coleções também podem basear-se nas informações de estado atuais para operações de gestão de clientes, tais como implementação de software e verificação de compatibilidade. Além destas coleções baseadas em consultas, os utilizadores administrativos também podem adicionar recursos a coleções.  

 Para obter mais informações sobre coleções, consulte o artigo [introdução às coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md). Para obter mais informações sobre as melhores práticas de segurança e informações de privacidade para operações do Configuration Manager que pode ser utilizado para configurar a associação da coleção, consulte [melhores práticas de segurança e informações de privacidade para o System Center Configuration Manager](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md).  

## <a name="security-best-practices-for-collections"></a>Melhores Práticas de Segurança para Coleções  
 Utilize a melhor prática de segurança seguinte para coleções.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Sempre que exportar ou importar uma coleção utilizando um ficheiro no formato MOF (Managed Object Format) guardada numa localização de rede, proteja a localização e o canal de rede.|Restringe quem pode aceder à pasta de rede.<br /><br /> Utilize a assinatura SMB (Server Message Block) ou a segurança IPsec entre a localização de rede e o servidor do site para impedir que um atacante adultere os dados da coleção exportados. Utilize IPsec para encriptar os dados na rede para evitar a divulgação de informações.|  

### <a name="security-issues-for-collections"></a>Problemas de Segurança para Coleções  
 As coleções têm os seguintes problemas de segurança:  

-   Se utilizar variáveis de coleção, os administradores locais podem ler informações potencialmente confidenciais.  

     As variáveis de coleção podem ser utilizadas quando implementar um sistema operativo.  


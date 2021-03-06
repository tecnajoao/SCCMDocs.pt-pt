---
title: Coleções de segurança e privacidade
titleSuffix: Configuration Manager
description: Obtenha as práticas recomendadas para segurança e privacidade em coleções no System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e1de6835b3096d8747258461b5e0013bc6e87028
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138794"
---
# <a name="security-and-privacy-for-collections-in-system-center-configuration-manager"></a>Segurança e privacidade para coleções no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém melhores práticas de segurança e informações de privacidade para coleções no System Center Configuration Manager.  

 Não existe nenhuma informação de privacidade especificamente para coleções no Configuration Manager. As coleções são contentores de recursos, tais como utilizadores e dispositivos. Associação a coleções depende frequentemente as informações que o Configuration Manager, recolhe durante o funcionamento normal. Por exemplo, através da utilização de informações de recursos que tenham sido recolhidas pela deteção ou inventário, uma coleção pode ser configurada para conter os dispositivos que cumprem critérios específicos. As coleções também podem basear-se nas informações de estado atuais para operações de gestão de clientes, tais como implementação de software e verificação de compatibilidade. Além destas coleções baseadas em consultas, os utilizadores administrativos também podem adicionar recursos a coleções.  

 Para obter mais informações sobre as coleções, consulte [introdução às coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md). Para obter mais informações sobre as melhores práticas de segurança e informações de privacidade para operações do Configuration Manager que pode ser utilizado para configurar a associação da coleção, consulte [melhores práticas de segurança e informações de privacidade para o System Center O Configuration Manager](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md).  

## <a name="security-best-practices-for-collections"></a>Melhores Práticas de Segurança para Coleções  
 Utilize a melhor prática de segurança seguinte para coleções.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Sempre que exportar ou importar uma coleção utilizando um ficheiro no formato MOF (Managed Object Format) guardada numa localização de rede, proteja a localização e o canal de rede.|Restringe quem pode aceder à pasta de rede.<br /><br /> Utilize a assinatura SMB (Server Message Block) ou a segurança IPsec entre a localização de rede e o servidor do site para impedir que um atacante adultere os dados da coleção exportados. Utilize IPsec para encriptar os dados na rede para evitar a divulgação de informações.|  

### <a name="security-issues-for-collections"></a>Problemas de Segurança para Coleções  
 As coleções têm os seguintes problemas de segurança:  

-   Se utilizar variáveis de coleção, os administradores locais podem ler informações potencialmente confidenciais.  

     As variáveis de coleção podem ser utilizadas quando implementar um sistema operativo.  

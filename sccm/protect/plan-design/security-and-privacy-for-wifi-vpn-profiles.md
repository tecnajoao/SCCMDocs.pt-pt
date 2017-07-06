---
title: "Perfis de Wi-Fi e VPN segurança e privacidade | Documentos do Microsoft"
description: "Saiba mais sobre a segurança melhores práticas para gerir perfis Wi-Fi e VPN dos dispositivos no System Center Configuration Manager."
ms.custom: na
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
caps.latest.revision: 4
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 8a5dc7361da34f3e6b926acd35c72c0c0767ce70
ms.openlocfilehash: 6d1d0a393a2ce614ae5f819475bd47b05e699b45
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Segurança e privacidade para perfis de Wi-Fi e VPN no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

##  <a name="security-best-practices-for-wi-fi--and-vpn-profiles"></a>Melhores práticas de segurança para perfis da VPN e Wi-Fi  
 Utilize os seguintes procedimentos recomendados de segurança ao gerir perfis Wi-Fi e VPN dos dispositivos.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Sempre que possível, escolha as opções mais seguras que a sua Wi-Fi e VPN infraestrutura e sistemas operativos cliente suportem.|Perfis VPN e Wi-Fi fornecem um método prático para distribuir e gerir as definições de Wi-Fi e VPN suportadas pelos seus dispositivos já centralmente. Gestor de configuração não adiciona Wi-Fi ou a funcionalidade VPN.<br /><br /> Identifique, implemente e siga os procedimentos de segurança eventualmente recomendados para os dispositivos e para a infraestrutura.|  

## <a name="privacy-information-for-wi-fi-profiles"></a>Informações de Privacidade para Perfis Wi-Fi  
 Pode utilizar perfis de Wi-Fi e VPN para configurar dispositivos cliente para estabelecer ligação ao Wi-Fi e servidores VPN e, em seguida, avaliar se esses dispositivos se tornam compatíveis após a aplicação dos perfis. O ponto de gestão envia as informações de compatibilidade para o servidor do site e as informações são armazenadas na base de dados do site. As informações são encriptadas quando os dispositivos as enviam para o ponto de gestão, mas não são armazenadas em formato encriptado na base de dados do site. A base de dados conserva as informações até que sejam eliminadas pela tarefa de manutenção do site **Eliminar Dados de Gestão de Configuração Desatualizados** . O intervalo de eliminação predefinido é 90 dias, mas pode alterá-lo. As informações de conformidade não são enviadas à Microsoft.  

 Por predefinição, dispositivos não avaliam os perfis VPN e Wi-Fi. Além disso, tem de configurar os perfis e, em seguida, implementá-los nos utilizadores.  

 Antes de configurar perfis VPN ou de Wi-Fi, considere os requisitos de privacidade.  

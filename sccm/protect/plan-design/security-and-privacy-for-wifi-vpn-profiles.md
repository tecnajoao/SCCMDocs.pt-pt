---
title: Privacidade e segurança de perfil de Wi-Fi e VPN
titleSuffix: Configuration Manager
description: Saiba mais sobre a segurança melhores práticas para gerir perfis de Wi-Fi e VPN para dispositivos no System Center Configuration Manager.
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: be81ff80f0da01916e2ec21a8ba1c7fe48fb8062
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142328"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Segurança e privacidade para perfis de Wi-Fi e VPN no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

##  <a name="security-best-practices-for-wi-fi--and-vpn-profiles"></a>Melhores práticas de segurança para Wi-Fi e perfis VPN  
 Utilize as seguintes práticas recomendadas de segurança ao gerir perfis de Wi-Fi e VPN para dispositivos.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Sempre que possível, escolha as opções mais seguras que pode oferecer suporte a seu Wi-Fi e VPN infraestrutura e sistemas operativos cliente.|Perfis VPN e Wi-Fi fornecem um método prático para distribuir e gerir as definições de VPN e Wi-Fi já suportadas pelos seus dispositivos centralmente. Gestor de configuração não adiciona Wi-Fi ou a funcionalidade VPN.<br /><br /> Identifique, implemente e siga os procedimentos de segurança eventualmente recomendados para os dispositivos e para a infraestrutura.|  

## <a name="privacy-information-for-wi-fi-profiles"></a>Informações de Privacidade para Perfis Wi-Fi  
 Pode utilizar perfis de Wi-Fi e VPN para configurar dispositivos de cliente para ligar a servidores VPN e Wi-Fi e, em seguida, avalie se esses dispositivos ficam em conformidade após a aplicação dos perfis. O ponto de gestão envia as informações de compatibilidade para o servidor do site e as informações são armazenadas na base de dados do site. As informações são encriptadas quando os dispositivos as enviam para o ponto de gestão, mas não são armazenadas em formato encriptado na base de dados do site. A base de dados conserva as informações até que sejam eliminadas pela tarefa de manutenção do site **Eliminar Dados de Gestão de Configuração Desatualizados** . O intervalo de eliminação predefinido é 90 dias, mas pode alterá-lo. As informações de conformidade não são enviadas à Microsoft.  

 Por predefinição, os dispositivos não avaliam perfis VPN e Wi-Fi. Além disso, tem de configurar os perfis e, em seguida, implementá-las aos utilizadores.  

 Antes de configurar Wi-Fi ou perfis VPN, considere os requisitos de privacidade.  

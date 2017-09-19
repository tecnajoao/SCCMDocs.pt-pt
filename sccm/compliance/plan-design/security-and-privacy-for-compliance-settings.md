---
title: "Segurança e privacidade para definições de compatibilidade | Microsoft Docs"
description: "Saiba mais sobre a segurança melhores práticas para definições de compatibilidade no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1c409244-6778-4970-a99c-d2508c9cf62b
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: f38e03ffac6d3472bbef9c3b78e4c0e1f7cde598
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/15/2017
---
# <a name="security-and-privacy-for-compliance-settings-in-system-center-configuration-manager"></a>Segurança e privacidade para definições de compatibilidade no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


## <a name="security-best-practices-for-compliance-settings"></a>Procedimentos recomendados de segurança para definições de compatibilidade  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Não monitorize dados confidenciais.|Para ajudar a evitar a divulgação de informações, não configure os itens de configuração para monitorizar informações potencialmente confidenciais.|  
|Não configure regras de conformidade que utilizem dados passíveis de serem modificados por utilizadores finais.|Se criar uma regra de compatibilidade com base em dados que os utilizadores podem modificar, como definições de registo para opções de configuração, os resultados de compatibilidade não serão fiáveis.|  
|Importe pacotes de configuração do Microsoft System Center e outros dados de configuração de origens externas apenas se tiverem uma assinatura digital válida de um fabricante fidedigno.|Os dados de configuração publicados podem ser assinados digitalmente para que possa verificar a origem da publicação e certificar-se de que os dados não foram adulterados. Se a verificação da assinatura digital falhar, é apresentado um aviso e é-lhe perguntado se pretende continuar com a importação. Não importe dados não assinados se não conseguir verificar a origem e a integridade dos dados.|  
|Implemente controlos de acesso para proteger computadores de referência.|Certifique-se de que quando um utilizador administrativo configura uma definição de registo ou de sistema de ficheiros navegando para um computador de referência, o computador de referência não tinha sido comprometido.|  
|Proteja o canal de comunicação ao navegar para um computador de referência.|Para impedir a adulteração dos dados quando é transferido através da rede, utilize a segurança de protocolo de Internet (IPsec) ou bloco de mensagem de servidor (SMB) entre o computador que executa a consola do Configuration Manager e o computador de referência.|  
|Restrinja e monitorize os utilizadores administrativos a quem é concedida a função de segurança baseada em funções de Gestor de Definições de Conformidade.|Os utilizadores administrativos a quem é concedida a função **Gestor de Definições de Compatibilidade** podem implementar itens de configuração em todos os dispositivos e em todos os utilizadores na hierarquia. Os itens de configuração podem ser muito eficientes e podem incluir, por exemplo, scripts e reconfiguração do registo.|  

## <a name="privacy-information-for-compliance-settings"></a>Informações de privacidade para definições de compatibilidade  
 Pode utilizar definições de compatibilidade para avaliar se os dispositivos cliente são compatíveis com os itens de configuração que implementar em linhas de base de configuração. Algumas definições podem ser remediadas automaticamente se não forem compatíveis. As informações de conformidade são enviadas para o servidor do site pelo ponto de gestão e armazenadas na base de dados do site. As informações são encriptadas quando os dispositivos as enviam para o ponto de gestão, mas não são armazenadas em formato encriptado na base de dados do site. As informações são retidas na base de dados até que a tarefa de manutenção do site **Eliminar Dados de Gestão de Configuração Desatualizados** as elimine todos os 90 dias. Pode configurar o intervalo de eliminação. As informações de conformidade não são enviadas à Microsoft.  

 Por predefinição, os dispositivos não avaliam as definições de compatibilidade. Além disso, tem de configurar os itens de configuração e as linhas de base de configuração e, em seguida, implementá-los nos dispositivos.  

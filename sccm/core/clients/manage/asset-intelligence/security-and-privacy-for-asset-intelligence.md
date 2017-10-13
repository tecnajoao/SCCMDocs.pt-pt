---
title: "Privacidade do Asset Intelligence segurança | Microsoft Docs"
description: "Obter informações de segurança e privacidade do Asset Intelligence no System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d0c6f7a0-dcae-4e6d-aa28-35d464d97ff7
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: b12054cce52e2b83715a083d78a62e06b5127a2f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-asset-intelligence-in-system-center-configuration-manager"></a>Segurança e privacidade do Asset Intelligence no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém informações de privacidade do Asset Intelligence no System Center Configuration Manager e de segurança.  

##  <a name="BKMK_Security_AI"></a> Melhores práticas de segurança do Asset Intelligence  
 Utilize as seguintes melhores práticas de segurança quando utilizar o Asset Intelligence.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Quando importar um ficheiro de licença (ficheiro de Licenciamento em Volume da Microsoft ou um ficheiro da Declaração de Licença Geral), proteja o canal de comunicação e de ficheiros.|Utilize permissões do sistema de ficheiros NTFS para garantir que apenas os utilizadores autorizados podem aceder aos ficheiros de licença e utilizar a assinatura SMB (Server Message Block) para assegurar a integridade dos dados quando é transferido para o servidor do site durante o processo de importação.|  
|Utilize o princípio do menor número de permissões para importar os ficheiros de licença.|Utilize a administração baseada em funções para conceder a permissão Gerir Asset Intelligence para o utilizador administrativo que importa os ficheiros de licença. A função incorporada do Gestor do Asset Intelligence inclui esta permissão.|  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Informações de privacidade para o Asset Intelligence  
 Asset Intelligence expande as capacidades de inventário do Configuration Manager para fornecer um nível mais elevado de visibilidade de ativos na empresa. A recolha de informações do Asset Intelligence não está ativada automaticamente. Pode ativar as classes de relatório de inventário de hardware para modificar o tipo de informações recolhidas. Para obter mais informações, consulte [configurar do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Informações do Asset Intelligence são armazenadas na base de dados do Configuration Manager da mesma forma como as informações de inventário. Quando os clientes estabelecem ligação aos pontos de gestão utilizando HTTPS, os dados são sempre encriptados durante a transferência para o ponto de gestão. Quando os clientes estabelecem ligação ao HTTP, pode configurar a transferência de dados de inventário para serem assinados e encriptados. Os dados de inventário não são armazenados em formato encriptado na base de dados. As informações são retidas na base de dados até que a tarefa de manutenção do site **Eliminar Histórico de Inventário Desatualizado** a elimine todos os 90 dias. Pode configurar o intervalo de eliminação.  

 O Asset Intelligence não envia informações sobre utilizadores e computadores nem sobre a utilização de licenças para a Microsoft. Pode optar por enviar pedidos do System Center Online para categorização, o que significa que pode identificar um ou mais títulos de software que não estejam categorizados e enviá-los para o System Center Online para pesquisa e categorização. Após o carregamento de um título de software, os investigadores da Microsoft identificam, categorizam e disponibilizam estes conhecimentos a todos os utilizadores que utilizam o serviço online. Deve estar ciente das seguintes implicações de privacidade quando submete informações para o System Center Online:  

-   O carregamento aplica-se apenas a informações de título de software genérico (nome, publicador e assim sucessivamente) que optar por enviar para o System Center Online. As informações de inventário não são enviadas com um carregamento.  

-   O carregamento nunca ocorre de forma automática e o sistema não foi concebido para automatizar esta tarefa. Deve selecionar e aprovar manualmente o carregamento de cada título de software.  

-   Uma caixa de diálogo mostra exatamente os dados que vão ser carregados, antes do processo de carregamento ser iniciado.  

-   As informações de licença não são enviadas à Microsoft. As informações de licença são armazenadas numa área separada da base de dados do Configuration Manager e não é possível enviar à Microsoft.  

-   Os títulos de software carregados passam a ser públicos, na medida em que o conhecimento dessa aplicação e a respetiva categorização passam a fazer parte integrante do catálogo do System Center Online Asset Intelligence, podendo assim ser transferidos por outros consumidores do catálogo.  

-   A origem do título de software não está registada no catálogo do Asset Intelligence e não é disponibilizada para outros clientes. No entanto, deve certificar-se de que não carregou quaisquer títulos de aplicações que contenham informações privadas.  

-   Não é possível resgatar os dados carregados.  

 Antes de configurar a recolha de dados do Asset Intelligence e decidir se pretende enviar informações para o System Center Online, tenha em consideração os requisitos de privacidade da sua empresa.  

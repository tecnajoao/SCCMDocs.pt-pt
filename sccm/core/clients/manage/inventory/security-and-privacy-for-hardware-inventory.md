---
title: "Privacidade de segurança de inventário de hardware"
titleSuffix: Configuration Manager
description: "Obter informações de segurança e privacidade para inventário de hardware no System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62e20d86-db6d-4a1f-b14a-905a9de31698
caps.latest.revision: "6"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: d08bae2cceada5393e58bf8ad2e4a603277f5dfc
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="security-and-privacy-for-hardware-inventory-in-system-center-configuration-manager"></a>Segurança e privacidade para o inventário de hardware no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém informações de segurança e privacidade para inventário de hardware no System Center Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Melhores práticas de segurança para o inventário de hardware  
 Utilize as seguintes melhores práticas de segurança para quando recolher os dados de inventário de hardware a partir de clientes:  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Assinar e encriptar dados de inventário|Quando os clientes comunicam com pontos de gestão através de HTTPS, todos os dados enviados são encriptados com SSL. No entanto, quando os computadores cliente utilizam HTTP para comunicar com pontos de gestão na intranet, os dados de inventário de cliente e os ficheiros recolhidos podem ser enviados não estando assinados nem encriptados. Certifique-se de que o site está configurado para exigir assinatura e utilizar encriptação. Além disso, se os clientes suportarem o algoritmo SHA-256, selecione a opção para exigir SHA-256.|  
|Não recolher ficheiros IDMIF e NOIDMIF em ambientes de alta segurança|Pode utilizar a recolha de ficheiros IDMIF e NOIDMIF para expandir a recolha de inventário de hardware. Quando for necessário, o Configuration Manager cria novas tabelas ou modifica as tabelas existentes na base de dados do Configuration Manager para acomodar as propriedades em ficheiros IDMIF e NOIDMIF. No entanto, o Configuration Manager não valida ficheiros IDMIF e NOIDMIF, pelo que estes ficheiros podem ser utilizados para alterar as tabelas que pretende alteradas. Os dados válidos podem ser substituídos por dados inválidos. Além disso, foi possível adicionar grandes quantidades de dados e o processamento de dados pode provocar atrasos em todas as funções do Configuration Manager. Para mitigar estes riscos, configure a definição do cliente de inventário de hardware **Recolher ficheiros MIF** como **Nenhum**.|  

### <a name="security-issues-for-hardware-inventory"></a>Problemas de segurança para inventário de hardware  
 Recolher o inventário expõe potenciais vulnerabilidades. Os atacantes podem efetuar as seguintes tarefas:  

-   Enviar dados inválidos, que serão aceites pelo ponto de gestão mesmo quando a definição de cliente de inventário de software está desativada e a recolha de ficheiros não está ativada.  

-   Enviar excessivamente grandes quantidades de dados num único ficheiro e em muitos ficheiros, o que poderá provocar denial of service.  

-   Aceder às informações de inventário que é transferido para o Configuration Manager.  

 Uma vez que um utilizador com privilégios administrativos locais pode enviar quaisquer informações como dados de inventário, considere os dados de inventário recolhidos pelo Configuration Manager como autoritativos.  

 O inventário de hardware está ativado por predefinição como uma definição de cliente.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Informações de privacidade para inventário de hardware  
 Inventário de hardware permite-lhe obter as informações que são armazenadas no registo e no WMI em clientes do Configuration Manager. O inventário de software permite-lhe detetar todos os ficheiros de um tipo especificado ou recolher todos os ficheiros especificados a partir dos clientes. O Asset Intelligence melhora as capacidades de inventário ao expandir o inventário de hardware e software e ao adicionar novas funcionalidades de gestão de licenças.  

 O inventário de hardware está ativado por predefinição como uma definição de cliente e as informações da WMI recolhidas são determinadas pelas opções que selecionar. O inventário de software está ativado por predefinição, mas os ficheiros não são recolhidos por predefinição. A recolha de dados do Asset Intelligence é ativada automaticamente, embora possa selecionar as classes de relatório de inventário de hardware a ativar.  

 As informações de inventário não são enviadas à Microsoft. Informações de inventário são armazenadas na base de dados do Configuration Manager. Quando os clientes utilizam HTTPS para ligar a pontos de gestão, os dados de inventário enviados para o site são encriptados durante a transferência. Se os clientes utilizarem HTTP para ligar a pontos de gestão, terá a opção para ativar a encriptação de inventário. Os dados de inventário não são armazenados em formato encriptado na base de dados. As informações são retidas na base de dados até serem eliminadas pelas tarefas de manutenção do site **Eliminar Histórico de Inventário Desatualizado** ou **Eliminar Ficheiros Recolhidos Desatualizados** todos os 90 dias. Pode configurar o intervalo de eliminação.  

 Antes de configurar o inventário de hardware, o inventário de software, a recolha de ficheiros ou a recolha de dados do Asset Intelligence, considere os requisitos de privacidade.  

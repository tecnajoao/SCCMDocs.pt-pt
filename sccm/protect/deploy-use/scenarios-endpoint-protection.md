---
title: "Cenário Endpoint Protection protege os computadores contra software maligno | Documentos do Microsoft"
description: Saiba como implementar o Endpoint Protection no Configuration Manager para proteger os computadores contra ataques de software maligno.
ms.custom: na
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
caps.latest.revision: 8
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: af0aafb4b7209d840676d16723509f399c662aad
ms.openlocfilehash: b98684d44874ff246e4d675039c6e443aee82a62
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---

# <a name="example-scenario-using-system-center-endpoint-protection-to-protect-computers-from-malware-in-system-center-configuration-manager"></a>Cenário de exemplo: Utilizar o System Center Endpoint Protection para proteger os computadores contra software maligno no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico fornece um cenário de exemplo de como implementar Endpoint Protection no Configuration Manager para proteger os computadores de uma organização contra ataques de software maligno.  

 João é o administrador do Configuration Manager no Woodgrove Bank. O banco utiliza atualmente o System Center Endpoint Protection para proteger os computadores contra ataques de software maligno. Além disso, o banco utiliza a Política de Grupo do Windows para assegurar que a Firewall do Windows está ativada em todos os computadores da empresa e que os utilizadores são notificados quando esta bloqueia um programa novo.  

 João foi-lhe pedido para atualizar o software de proteção contra software maligno do Woodgrove Bank para o System Center Endpoint Protection, para que o banco possam beneficiam das funcionalidades de proteção contra software maligno mais recentes e ser capaz de gerir centralmente a solução antimalware a partir da consola do Configuration Manager. Esta implementação tem os seguintes requisitos:  

-   Utilize o Configuration Manager para gerir as definições de Firewall do Windows que sejam atualmente geridas pela política de grupo.  

-   Atualizações de software de utilizar o Gestor de configuração para transferir as definições de software maligno para computadores. Se as atualizações de software não estiverem disponíveis, por exemplo, se o computador não estiver ligado à rede empresarial, os computadores têm de transferir as atualizações das definições a partir do Microsoft Update.  

-   Computadores dos utilizadores tem de efetuar uma análise rápida de malware todos os dias. No entanto, os servidores têm de efetuar uma análise completa todos os sábados, fora do horário comercial, à 1:00.  

-   Enviar um alerta por e-mail sempre que ocorrer qualquer um dos seguintes eventos:  

    -   É detetado software maligno num computador  

    -   A mesma ameaça de software maligno é detetada em mais de cinco por cento dos computadores  

    -   A mesma ameaça de software maligno é detetada mais de cinco vezes em qualquer período de 24 horas  

    -   São detetados mais de três tipos diferentes de software maligno em qualquer período de 24 horas  

-   Desinstalar a solução antimalware existente.  

 Em seguida, o João efetua os seguintes passos para implementar o Endpoint Protection:  

##  <a name="steps-to-implement-endpoint-protection"></a>Passos para implementar o Endpoint Protection  

|Processo|Referência|  
|-------------|---------------|  
|João consulta as informações disponíveis sobre os conceitos básicos para o Endpoint Protection no Configuration Manager.|Para obter informações gerais sobre o Endpoint Protection, consulte o artigo [Endpoint Protection no System Center Configuration Manager](endpoint-protection.md).|  
|João consulta e implementa os pré-requisitos necessários para utilizar o Endpoint Protection.|Para obter informações sobre os pré-requisitos para o Endpoint Protection, consulte o artigo [planeamento para o Endpoint Protection](../plan-design/planning-for-endpoint-protection.md).|  
|João instala a função de sistema de sites do Endpoint Protection no servidor do sistema de sites de uma só, na parte superior da hierarquia do Banco Woodgrove.|Para obter mais informações sobre como instalar a função de sistema de sites do Endpoint Protection, consulte "Pré-requisitos" em [configurar o Endpoint Protection](configure-endpoint-protection.md).|  
|O João configura o Configuration Manager para utilizar um servidor SMTP para enviar alertas de correio eletrónico.<br /><br /> **Nota:** Tem de configurar um servidor SMTP apenas se pretender ser notificado por correio eletrónico quando é gerado um alerta de Endpoint Protection.|Para obter mais informações, consulte o artigo [configurar alertas no Endpoint Protection](endpoint-configure-alerts.md).|  
|João cria uma coleção de dispositivos que contém todos os computadores e servidores para instalar o cliente do Endpoint Protection. Chama a esta coleção **todos os computadores protegidos pelo Endpoint Protection**.<br /><br /> **Dica:** Não é possível configurar alertas de coleções de utilizadores.|Para mais informações sobre como criar coleções, consulte o artigo [como criar coleções no System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md)|  
|Configura os seguintes alertas para a coleção: <br /><br />1) **é detetado software maligno**: O João configura uma gravidade de alerta de **crítico**. <br /><br />2) **o mesmo tipo de software maligno é detetado num número de computadores** : O João configura uma gravidade de alerta de **crítico** e especifica que será gerado o alerta quando mais de 5 por cento dos computadores têm software maligno detetado. <br /><br />3) **o mesmo tipo de software maligno é detetado repetidamente no intervalo especificado num computador**: O João configura uma gravidade de alerta de **crítico** e especifica que o alerta será gerado quando software maligno é detetado mais de 5 vezes num período de 24 horas. <br /><br />4) **vários tipos de malware são detetados no mesmo computador no intervalo especificado**: O João configura uma gravidade de alerta de **crítico** e especifica que será gerado o alerta quando mais de 3 tipos de software maligno são gerados num período de 24 horas.<br /><br /> O valor para **gravidade do alerta** indica o nível de alerta que será apresentado na consola do Configuration Manager e alertas que ele recebe numa mensagem de e-mail.<br /><br /> Além disso, seleciona a opção **ver esta coleção no dashboard do Endpoint Protection** para que ele possa monitorizar os alertas na consola do Configuration Manager.|Consulte "Configurar alertas para o Endpoint Protection" no [configurar o Endpoint Protection no System Center Configuration Manager](endpoint-configure-alerts.md).|  
|O João configura as atualizações de software do Configuration Manager para transferir e implementar atualizações de definições três vezes por dia, utilizando uma regra de implementação automática.|Para mais informações, consulte a secção "Utilizando o Configuration Manager atualizações para entregar definição atualizações de Software" [utilize o Gestor de configuração de atualizações de software para fornecer atualizações de definições](endpoint-definitions-configmgr.md).|  
|O João examina as definições da política antimalware predefinida, a qual contém definições de segurança recomendadas pela Microsoft. Para os computadores fazerem uma análise rápida diária, altera as seguintes definições:<br /><br /> 1) **executar uma análise rápida diária nos computadores cliente**: **Yes**.<br /><br /> 2) **agendar hora da análise rápida diária**:  **9:00:00**.<br /><br /> O João repara que a opção **Atualizações distribuídas do Microsoft Update** está selecionada como origem de atualização de definições por predefinição, Esta satisfaz o requisito de negócio que computadores transferem definições a partir do Microsoft Update quando não é possível recebe atualizações de software do Configuration Manager.|Consulte o artigo [como criar e implementar políticas de proteção contra software maligno do Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|O João cria uma coleção que contém apenas os servidores do Banco Woodgrove com o nome **Servidores do Banco Woodgrove**.|Consulte [Como criar coleções no System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md)|  
|O João cria uma política antimalware personalizada com o nome **Política de Servidor do Banco Woodgrove**. Só adiciona as definições para **Análises agendadas** e faz as seguintes alterações:<br /><br /> **Tipo de análise**:  **Completa**<br /><br /> **Analisar dia**:  **Sábado**<br /><br /> **Análise de tempo**: **1:00 AM**<br /><br /> **Executar uma análise rápida diária nos computadores cliente**:  **No**.|Consulte o artigo [como criar e implementar políticas de proteção contra software maligno do Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|O João implementa a política antimalware personalizada **Política de Servidor do Banco Woodgrove** na coleção **Servidores do Banco Woodgrove** .|Consulte "para implementar uma política antimalware em computadores de cliente" [como criar e implementar políticas de proteção contra software maligno do Endpoint Protection](endpoint-antimalware-policies.md) tópico.|  
|João cria um novo conjunto de cliente personalizadas, definições do dispositivo para o Endpoint Protection e os nomes destas **definições do Endpoint Protection do Woodgrove Bank**.<br /><br /> **Nota:** Se não pretender instalar e ativar o Endpoint Protection em todos os clientes da hierarquia, certifique-se de que as opções **cliente de gerir o Endpoint Protection nos computadores cliente** e **cliente de instalar o Endpoint Protection nos computadores cliente** estão ambas configuradas como **não** nas predefinições do cliente.|Para obter mais informações, consulte o artigo [configurar definições personalizadas do cliente do Endpoint Protection](endpoint-protection-configure-client.md).|  
|Configura as definições seguintes para o Endpoint Protection:<br /><br /> **Gerir o cliente do Endpoint Protection nos computadores cliente**:  **Sim**<br /><br /> Esta definição e valor assegura que qualquer cliente existente do Endpoint Protection está instalado torna-se a gerido pelo Configuration Manager.<br /><br /> **Instalar o cliente do Endpoint Protection nos computadores cliente**:  **Yes**.<br /><br /> **Automaticamente remover antimalware software anteriormente instalado antes da instalação do Endpoint Protection**:  **Yes**.<br /><br /> Esta definição e valor satisfaz os requisitos comerciais que o software antimalware existente é removido antes de Endpoint Protection está instalado e ativado.|Para obter mais informações, consulte o artigo [configurar definições personalizadas do cliente do Endpoint Protection](endpoint-protection-configure-client.md).|  
|João implementa o **definições do Endpoint Protection do Woodgrove Bank** definições de cliente para o **todos os computadores protegidos pelo Endpoint Protection** coleção.|Consulte "Configurar definições de cliente personalizadas para o Endpoint Protection" no [configurar o Endpoint Protection no Configuration Manager](endpoint-antimalware-policies.md).|  
|O João utiliza o Assistente da Criação da Política de Firewall do Windows para criar uma política ao configurar as seguintes definições para o perfil de domínio:<br /><br /> 1) **ativar a Firewall do Windows**: **Sim**<br /><br /> 2)<br />                    **Notificar o utilizador quando a Firewall do Windows bloquear um programa novo**: **Sim**|Consulte o artigo [como criar e implementar políticas de Firewall do Windows para o Endpoint Protection no System Center Configuration Manager](../../protect/deploy-use/create-windows-firewall-policies.md)|  
|João implementar a nova política de firewall para a coleção **todos os computadores protegidos pelo Endpoint Protection** criado anteriormente.|Consulte "para implementar uma política de Firewall do Windows" no [como criar e implementar políticas de Firewall do Windows para o Endpoint Protection no System Center Configuration Manager](create-windows-firewall-policies.md)|  
|João utiliza as tarefas de gestão disponíveis para o Endpoint Protection para gerir a proteção contra software maligno e políticas de Firewall do Windows, efetuar análises a pedido de computadores quando for necessário, forçar computadores para transferir as definições mais recentes e para especificar qualquer mais ações a efetuar quando é detetado software maligno.|Consulte o artigo [como gerir políticas antimalware e firewall definições do Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-firewall.md)|  
|João utiliza os seguintes métodos para monitorizar o estado do Endpoint Protection e as ações que são executadas pelo Endpoint Protection:<br /><br /> 1) através da utilização de **Estado Endpoint Protection** nó **segurança** no **monitorização** área de trabalho.<br /><br /> 2) através da utilização de **Endpoint Protection** nó o **ativos e compatibilidade** área de trabalho.<br /><br /> 3), utilizando o Configuration Manager incorporadas relatórios.|Consulte o artigo [como monitorizar o Endpoint Protection no System Center Configuration Manager](monitor-endpoint-protection.md)|  

 João relatórios uma implementação efetuada com êxito do Endpoint Protection ao seu diretor e confirma que os computadores do Woodgrove Bank estão agora protegidos a partir da proteção contra software maligno, consoante os requisitos de negócio que ele foi atribuído.


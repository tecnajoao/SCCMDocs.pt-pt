---
title: Proteger os computadores contra software maligno
titleSuffix: Configuration Manager
description: Saiba como implementar o Endpoint Protection no Configuration Manager para proteger os computadores contra ataques de malware.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
author: aczechowski
ms.author: aaroncz
manager: doubeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9eeb219cc681aa50ea671833efc72014a1ccfd4a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137733"
---
# <a name="example-scenario-use-endpoint-protection-to-protect-computers-from-malware"></a>Cenário exemplo: Utilizar o Endpoint Protection para proteger os computadores contra software maligno

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo fornece um cenário de exemplo para implementar o Endpoint Protection no Configuration Manager para proteger os computadores na sua organização contra ataques de malware.  



## <a name="scenario-overview"></a>Descrição geral do cenário

John é o administrador do Configuration Manager no Woodgrove Bank. O banco utiliza atualmente o System Center Endpoint Protection para proteger os computadores contra ataques de malware. Além disso, o banco utiliza a Política de Grupo do Windows para assegurar que a Firewall do Windows está ativada em todos os computadores da empresa e que os utilizadores são notificados quando esta bloqueia um programa novo.  

Foi pedido ao João para atualizar o software antimalware do Banco Woodgrove para o System Center Endpoint Protection para que o banco possa beneficiar das funcionalidades de antimalware mais recentes e conseguir gerir centralmente a solução antimalware do Configuration Manager Console. 


## <a name="business-requirements"></a>Requisitos de negócios

Esta implementação tem os seguintes requisitos:  

- Utilize o Configuration Manager para gerir as definições da Firewall do Windows atualmente geridos pela política de grupo.  

- Utilize o Gestor de configuração as atualizações de software para transferir as definições de software maligno para computadores. Se as atualizações de software não estiverem disponíveis, por exemplo, se o computador não estiver ligado à rede empresarial, os computadores têm de transferir as atualizações das definições a partir do Microsoft Update.  

- Os computadores dos usuários tem de efetuar uma análise rápida de software maligno todos os dias. No entanto, os servidores têm de efetuar uma análise completa todos os sábados, fora do horário comercial, à 1:00.  

- Enviar um alerta por e-mail sempre que ocorrer qualquer um dos seguintes eventos:  

  -   É detetado software maligno num computador  

  -   A mesma ameaça de software maligno é detetada em mais de cinco por cento dos computadores  

  -   A mesma ameaça de software maligno é detetada mais de 5 vezes em qualquer período de 24 horas  

  -   Mais de 3 tipos diferentes de software maligno são detetados em qualquer período de 24 horas  

  Em seguida, o João executa os seguintes passos para implementar o Endpoint Protection:  



##  <a name="steps-to-implement-endpoint-protection"></a>Passos para implementar o Endpoint Protection  

|Processo|Referência|  
|-------------|---------------|  
|João consulta as informações disponíveis sobre os conceitos básicos para o Endpoint Protection no Configuration Manager.|Para obter informações gerais sobre o Endpoint Protection, consulte [Endpoint Protection no System Center Configuration Manager](endpoint-protection.md).|  
|João consulta e implementa os pré-requisitos necessários para utilizar o Endpoint Protection.|Para obter informações sobre os pré-requisitos para o Endpoint Protection, consulte [planear o Endpoint Protection](../plan-design/planning-for-endpoint-protection.md).|  
|O João instala a função de sistema de sites do Endpoint Protection no servidor do sistema de sites de uma só, na parte superior da hierarquia do Banco Woodgrove.|Para obter mais informações sobre como instalar a função de sistema de sites do Endpoint Protection, consulte "Pré-requisitos" em [configurar o Endpoint Protection](configure-endpoint-protection.md).|  
|O João configura o Configuration Manager para utilizar um servidor SMTP para enviar alertas por e-mail.<br /><br /> **Nota:** Tem de configurar um servidor SMTP apenas se quiser ser notificado por e-mail quando é gerado um alerta de Endpoint Protection.|Para obter mais informações, consulte [configurar alertas no Endpoint Protection](endpoint-configure-alerts.md).|  
|O João cria uma coleção de dispositivos que contém todos os computadores e servidores para instalar o cliente do Endpoint Protection. Chama a esta coleção **todos os computadores protegidos pelo Endpoint Protection**.<br /><br /> **Sugestão:** Não é possível configurar alertas de coleções de utilizadores.|Para obter mais informações sobre como criar coleções, consulte [como criar coleções no System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md)|  
|Configura os seguintes alertas para a coleção: <br /><br />1) **é detetado software maligno**: O João configura uma gravidade de alerta **crítico**. <br /><br />2) **o mesmo tipo de software maligno for detetado em vários computadores**: O João configura uma gravidade de alerta **crítico** e especifica que o alerta será gerado quando mais de 5 por cento dos computadores têm software maligno detetado. <br /><br />3) **o mesmo tipo de software maligno é detetado repetidamente no intervalo especificado num computador**: O João configura uma gravidade de alerta **crítico** e especifica que o alerta será gerado quando software maligno for detetado mais de 5 vezes num período de 24 horas. <br /><br />4) **vários tipos de malware são detetados no mesmo computador no intervalo especificado**: O João configura uma gravidade de alerta **crítico** e especifica que o alerta será gerado quando mais de 3 tipos de malware são gerados num período de 24 horas.<br /><br /> O valor para **gravidade do alerta** indica o nível de alerta que será apresentado na consola do Configuration Manager e nos alertas que o João recebe numa mensagem de e-mail.<br /><br /> Além disso, seleciona a opção **ver esta coleção no dashboard do Endpoint Protection** para que ele possa monitorar os alertas na consola do Configuration Manager.|Consulte "Configurar alertas para o Endpoint Protection" na [configurar o Endpoint Protection no System Center Configuration Manager](endpoint-configure-alerts.md).|  
|O João configura as atualizações de software do Configuration Manager para transferir e implementar atualizações de definições três vezes por dia, utilizando uma regra de implementação automática.|Para obter mais informações, consulte a secção de "Usando Configuration Manager Software atualizações para fornecer atualizações de definições" na [utilize o Gestor de configuração de atualizações de software para fornecer atualizações de definições](endpoint-definitions-configmgr.md).|  
|O João examina as definições da política antimalware predefinida, a qual contém definições de segurança recomendadas pela Microsoft. Para os computadores fazerem uma análise rápida diária, altera as seguintes definições:<br /><br /> 1) **executar uma análise rápida diária nos computadores cliente**: **Sim**.<br /><br /> 2) **agendar hora da análise rápida diária**:  **9:00**.<br /><br /> O João repara que a opção **Atualizações distribuídas do Microsoft Update** está selecionada como origem de atualização de definições por predefinição, Isso cumpre o requisito de negócio que os computadores transferem definições do Microsoft Update quando não conseguirem receber atualizações de software do Configuration Manager.|Consulte [Como criar e implementar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|O João cria uma coleção que contém apenas os servidores do Banco Woodgrove com o nome **Servidores do Banco Woodgrove**.|Consulte [Como criar coleções no System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md)|  
|O João cria uma política antimalware personalizada com o nome **Política de Servidor do Banco Woodgrove**. Só adiciona as definições para **Análises agendadas** e faz as seguintes alterações:<br /><br /> **Tipo de análise**:  **Completa**<br /><br /> **Dia da análise**:  **Sábado**<br /><br /> **Hora da análise**: **1:00**<br /><br /> **Executar uma análise rápida diária nos computadores cliente**:  **Não**.|Consulte [Como criar e implementar políticas antimalware para o Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|O João implementa a política antimalware personalizada **Política de Servidor do Banco Woodgrove** na coleção **Servidores do Banco Woodgrove** .|Consulte "para implementar uma política antimalware em computadores cliente" [como criar e implementar políticas antimalware do Endpoint Protection](endpoint-antimalware-policies.md) artigo.|  
|O João cria um novo conjunto de cliente personalizadas, definições do dispositivo para o Endpoint Protection e atribui **definições de proteção de ponto final do Woodgrove Bank**.<br /><br /> **Nota:** Se não pretender instalar e ativar o Endpoint Protection em todos os clientes na sua hierarquia, certifique-se de que as opções **cliente gerir o Endpoint Protection nos computadores cliente** e **cliente de instalar o Endpoint Protection em computadores cliente** estão configuradas como **não** nas predefinições do cliente.|Para obter mais informações, consulte [configurar definições de cliente personalizadas para o Endpoint Protection](endpoint-protection-configure-client.md).|  
|Configura as definições seguintes para o Endpoint Protection:<br /><br /> **Gerir o cliente do Endpoint Protection nos computadores cliente**:  **Sim**<br /><br /> Esta definição e valor garante que qualquer cliente do Endpoint Protection existente que está instalado fica gerido pelo Configuration Manager.<br /><br /> **Instalar o cliente do Endpoint Protection nos computadores cliente**:  **Sim**.</br></br>**Tenha em atenção** a partir do Configuration Manager 1802, dispositivos Windows 10 não precisa de ter instalado o agente de proteção de ponto final. Se já estiver instalado em dispositivos Windows 10, do Configuration Manager não removê-lo. Os administradores podem remover o agente do Endpoint Protection em dispositivos Windows 10 que estejam a executar, pelo menos, a versão 1802 do cliente.|Para obter mais informações, consulte [configurar definições de cliente personalizadas para o Endpoint Protection](endpoint-protection-configure-client.md).|  
|João implementa a **definições de Endpoint Protection do Banco Woodgrove** definições de cliente para o **todos os computadores protegidos pelo Endpoint Protection** coleção.|Consulte "Configurar definições de cliente personalizadas para o Endpoint Protection" na [configurar o Endpoint Protection no Configuration Manager](endpoint-antimalware-policies.md).|  
|O João utiliza o Assistente da Criação da Política de Firewall do Windows para criar uma política ao configurar as seguintes definições para o perfil de domínio:<br /><br /> 1) **ativar a Firewall do Windows**: **Sim**<br /><br /> 2)<br />                    **Notificar o utilizador quando a Firewall do Windows bloquear um programa novo**: **Sim**|Consulte [como criar e implementar políticas de Firewall do Windows para o Endpoint Protection no System Center Configuration Manager](../../protect/deploy-use/create-windows-firewall-policies.md)|  
|O João implementa a nova política de firewall na coleção **todos os computadores protegidos pelo Endpoint Protection** que criou anteriormente.|Consulte "para implementar uma política de Firewall do Windows" no [como criar e implementar políticas de Firewall do Windows para o Endpoint Protection no System Center Configuration Manager](create-windows-firewall-policies.md)|  
|João utiliza as tarefas de gestão disponíveis para o Endpoint Protection para gerir antimalware e as políticas de Firewall do Windows, executar análises a pedido dos computadores quando for necessário, forçar computadores a transferir as definições mais recentes e especificar ações adicionais a tomar quando é detetado software maligno.|Consulte [como gerir políticas antimalware e definições para o Endpoint Protection no System Center Configuration Manager da firewall](endpoint-antimalware-firewall.md)|  
|O João utiliza os seguintes métodos para monitorizar o estado do Endpoint Protection e as ações efetuadas pelo Endpoint Protection:<br /><br /> 1) ao utilizar o **estado do Endpoint Protection** no nó **Security** no **monitorização** área de trabalho.<br /><br /> 2) ao utilizar o **Endpoint Protection** nó a **ativos e compatibilidade** área de trabalho.<br /><br /> 3), utilizando o Gestor de configuração integrados relatórios.|Consulte [como monitorizar o Endpoint Protection no System Center Configuration Manager](monitor-endpoint-protection.md)|  

 John relatórios de uma implementação bem-sucedida do Endpoint Protection para seu gerente e confirma que os computadores no Banco Woodgrove estão agora protegidos contra antimalware, de acordo com os requisitos empresariais que lhe foram transmitidos.

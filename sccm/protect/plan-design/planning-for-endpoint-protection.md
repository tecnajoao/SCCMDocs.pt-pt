---
title: Planear para o Endpoint Protection
titleSuffix: Configuration Manager
ms.custom: na
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 7610bbd3-a67f-4a09-8115-e35d40d43b42
caps.latest.revision: "16"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 3ffb112dc1aaf71162b0f706f5c07fb6d08e47f9
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="planning-for-endpoint-protection-in-system-center-configuration-manager"></a>Planear o Endpoint Protection no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Endpoint Protection no System Center Configuration Manager permite-lhe gerir políticas antimalware e de segurança da Firewall do Windows para computadores cliente na sua hierarquia do Configuration Manager.  

> [!IMPORTANT]  
>  Tem de estar licenciados para utilizar o Endpoint Protection para gerir clientes na sua hierarquia do Configuration Manager.  

Quando utilizar o Endpoint Protection com o Configuration Manager, tem as seguintes vantagens:  

-   Configurar políticas antimalware, definições de Firewall do Windows e gerir o Windows Defender Advanced Threat Protection em grupos selecionados de computadores  

-   Utilize o Gestor de configuração de atualizações de software para transferir os ficheiros de definição de antimalware mais recentes para manter os computadores cliente atualizados  

-   Enviar notificações por e-mail, utilizar a monitorização na consola e ver relatórios para manter os utilizadores administrativos informados quando for detetado software maligno em computadores cliente  

Computadores Windows 10 não requerem qualquer cliente adicional para gestão do endpoint protection. No Windows 8.1 e anteriores computadores, o Endpoint Protection instala o próprio cliente, para além do cliente do Configuration Manager. O cliente do Endpoint Protection tem as seguintes capacidades:  

-   Deteção e remediação de software maligno e spyware  

-   Deteção e remediação de rootkit  

-   Avaliação de vulnerabilidades críticas e atualizações automáticas de definições e de motor  

-   Deteção de vulnerabilidades de rede através do Sistema de Inspeção de Rede  

-   Integração com o serviço de proteção de nuvem para reportar software maligno à Microsoft. Ao aderir a este serviço, o Windows Defender ou o cliente do Endpoint Protection pode transferir as definições mais recentes do Centro de proteção contra software maligno quando é detetado software maligno não identificado num computador.  

> [!NOTE]  
>  O cliente do Endpoint Protection pode ser instalado num servidor que executa o Hyper-V e máquinas virtuais de convidados com sistemas operativos suportados. Para impedir a utilização excessiva da CPU, as ações do Endpoint Protection tem um atraso aleatório, incorporado para serviços não são executados em simultâneo.  

  Além disso, o Endpoint Protection no Configuration Manager permite-lhe gerir as definições da Firewall do Windows na consola do Configuration Manager.  

 [Cenário de exemplo: Utilizar o System Center Endpoint Protection para proteger os computadores contra software maligno no System Center Configuration Manager](../deploy-use/scenarios-endpoint-protection.md) mostra como poderia configurar e gerir o Endpoint Protection e Firewall do Windows.  

## <a name="managing-malware-with-endpoint-protection"></a>Gerir o Software Maligno com o Endpoint Protection  

Endpoint Protection no Configuration Manager permite-lhe criar políticas de antimalware que contêm definições para configurações de cliente do Endpoint Protection. Em seguida, pode implementar estas políticas antimalware nos computadores cliente e monitorizá-las no **estado do Endpoint Protection** no nó de **monitorização** área de trabalho, ou utilizando relatórios do Configuration Manager.  

 Informações adicionais:  

-   [Criar e implementar políticas antimalware do Endpoint Protection no System Center Configuration Manager](../deploy-use/endpoint-antimalware-policies.md) - criar, implementar e monitorizar políticas antimalware com uma lista das definições que pode configurar  

-   [Monitorizar o Endpoint Protection no System Center Configuration Manager](../deploy-use/monitor-endpoint-protection.md) -monitorizar relatórios de atividade, computadores cliente infetados e muito mais.   

-   [Gerir políticas antimalware e definições do Endpoint Protection no System Center Configuration Manager de firewall](../deploy-use/endpoint-antimalware-firewall.md) -é possível alterar a prioridade de política para [antimalware](../deploy-use/endpoint-antimalware-firewall.md#manage-antimalware-policies) ou [firewall](../deploy-use/endpoint-antimalware-firewall.md#manage-windows-firewall-policies), [remediar o software maligno encontrado nos computadores cliente](../deploy-use/endpoint-antimalware-firewall.md#remediate-detected-malware)e outras tarefas

## <a name="managing-windows-firewall-with-endpoint-protection"></a>Gerir a Firewall do Windows com o Endpoint Protection  
 Endpoint Protection no Configuration Manager disponibiliza gestão básica da Firewall do Windows nos computadores cliente. Para cada perfil de rede, pode configurar as seguintes definições:  

-   Ativar ou desativar a Firewall do Windows.  

-   Bloquear as ligações recebidas, incluindo as que se encontram na lista de programas permitidos.  

-   Notificar o utilizador quando a Firewall do Windows bloquear um programa novo.  

> [!NOTE]  
>  O Endpoint Protection suporta apenas a gestão da Firewall do Windows.  

  Para obter mais informações sobre como criar e implementar políticas de Firewall do Windows para o Endpoint Protection, consulte [como criar e implementar políticas de Firewall do Windows para o Endpoint Protection no System Center Configuration Manager](../deploy-use/create-windows-firewall-policies.md).  

## <a name="windows-defender-advanced-threat-protection"></a>O Windows Defender Advanced Threat Protection

A partir da versão 1606 do Configuration Manager (ramo atual), Endpoint Protection pode ajudar a gerir e monitorizar o Windows Defender Advanced Threat Protection (ATP). Windows Defender ATP é um novo serviço que o irão ajudar as empresas para detetar, analisar e responder a ataques avançados nas respetivas redes. Consulte [o Windows Defender Advanced Threat Protection](../deploy-use/windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Fluxo de Trabalho do Endpoint Protection  
 Utilize o diagrama a seguir para ajudar a compreender o fluxo de trabalho para implementar o Endpoint Protection na sua hierarquia do Configuration Manager.  

 ![Fluxo de Trabalho do Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Cliente do Endpoint Protection para Computadores Mac e Servidores Linux  
 O System Center inclui um cliente do Endpoint Protection para Linux e para computadores Mac. Estes clientes não são fornecidos com o Configuration Manager; em vez disso, tem de transferir os seguintes produtos a partir de [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

> [!IMPORTANT]  
>  Tem de ser um cliente de Licenciamento em Volume da Microsoft para transferir os ficheiros de instalação do Endpoint Protection para Linux e Mac.  

 Estes produtos não podem ser geridos a partir da consola do Configuration Manager. No entanto, um pacote de gestão do System Center Operations Manager é fornecido com os ficheiros de instalação, permitindo gerir o cliente para Linux ao utilizar o Operations Manager.  

 Para mais informações sobre como instalar e gerir os clientes do Endpoint Protection para computadores Linux e Mac, utilize a documentação que acompanha estes produtos, que está localizada na pasta **Documentação** .

## <a name="best-practices-for-endpoint-protection-in-configuration-manager"></a>Exemplos de Melhores Práticas para o Endpoint Protection no Configuration Manager  
 Utilize as seguintes melhores práticas no Endpoint Protection do System Center 2012 Configuration Manager.  

### <a name="configure-custom-client-settings-for-endpoint-protection"></a>Configurar definições personalizadas de cliente do Endpoint Protection  
 Ao configurar as definições de cliente do Endpoint Protection, utilize as predefinições de cliente porque estas aplicam definições a todos os computadores na sua hierarquia. Em vez disso, configure definições de cliente personalizadas e atribua estas definições a coleções de computadores na sua hierarquia.  

 Ao configurar definições de cliente personalizadas, pode:  

-   Personalizar as definições de antimalware e de segurança para diferentes partes da organização.  
-   Teste os efeitos da execução do Endpoint Protection num pequeno grupo de computadores antes de implementar em toda a hierarquia.  
-   Adicione mais clientes à coleção ao longo do tempo para fasear a implementação do cliente Endpoint Protection.  

### <a name="distributing-definition-updates-by-using-software-updates"></a>Distribuir atualizações de definições ao utilizar atualizações de software  
 Se estiver a utilizar as atualizações de software do Configuration Manager para distribuir atualizações de definições, considere colocar as atualizações de definições num pacote que não contenha outras atualizações de software. Esta opção mantém o tamanho do pacote de atualizações de definições mais pequeno, permitindo-lhe replicar para pontos de distribuição mais rapidamente.

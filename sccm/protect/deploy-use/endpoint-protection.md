---
title: Endpoint Protection
titleSuffix: Configuration Manager
description: "Saiba como gerir políticas antimalware e de segurança da Firewall do Windows para computadores cliente na sua hierarquia do Configuration Manager."
ms.custom: na
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3f8d0d7934a539729793cd0307d6fa5d3e31bf3a
ms.sourcegitcommit: fbde417e3c3002898bd216a7e110e725ae269893
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2018
---
# <a name="endpoint-protection"></a>Endpoint Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Proteção de ponto final gere as políticas antimalware e de segurança da Firewall do Windows para computadores cliente na sua hierarquia do Configuration Manager.  

> [!IMPORTANT]  
>  Tem de estar licenciados para utilizar o Endpoint Protection para gerir clientes na sua hierarquia do Configuration Manager.  

 Quando utilizar o Endpoint Protection com o Configuration Manager, tem as seguintes vantagens:  

-   Configurar políticas antimalware, definições de Firewall do Windows e gerir o Windows Defender Advanced Threat Protection em grupos selecionados de computadores  
-   Utilize o Gestor de configuração de atualizações de software para transferir os ficheiros de definição de antimalware mais recentes para manter os computadores cliente atualizados  
-   Enviar notificações por e-mail, utilizar a monitorização na consola e ver relatórios. Estas ações informam os utilizadores administrativos quando é detetado software maligno em computadores cliente.  

Começando com computadores Windows 10 e Windows Server 2016, o Windows Defender já está instalado. Para estes sistemas operativos, um cliente de gestão para o Windows Defender é instalado quando instala o cliente do Configuration Manager. No Windows 8.1 e anteriores computadores, o cliente do Endpoint Protection está instalado com o cliente do Configuration Manager. O Windows Defender e o cliente do Endpoint Protection tem as seguintes funcionalidades:  

-   Deteção e remediação de software maligno e spyware  
-   Deteção e remediação de rootkit  
-   Avaliação de vulnerabilidades críticas e atualizações automáticas de definições e de motor  
-   Deteção de vulnerabilidades de rede através do Sistema de Inspeção de Rede  
-   Integração com o serviço de proteção de nuvem para reportar software maligno à Microsoft. Ao aderir a este serviço, o cliente do Endpoint Protection ou o Windows Defender transfere as definições mais recentes do Centro de proteção contra software maligno quando é detetado software maligno não identificado num computador.  

> [!NOTE]  
>  O cliente do Endpoint Protection pode ser instalado num servidor que executa o Hyper-V e máquinas virtuais de convidados com sistemas operativos suportados. Para impedir a utilização excessiva da CPU, as ações do Endpoint Protection tem um atraso aleatório incorporado, para que os serviços de proteção não são executados em simultâneo.  

 Além disso, pode gerir definições do Firewall do Windows com o Endpoint Protection na consola do Configuration Manager.  

 [Cenário de exemplo: Utilizar o System Center Endpoint Protection para proteger os computadores contra software maligno no System Center Configuration Manager](scenarios-endpoint-protection.md) Endpoint Protection e Firewall do Windows.  


## <a name="managing-malware-with-endpoint-protection"></a>Gerir o Software Maligno com o Endpoint Protection  
 Endpoint Protection no Configuration Manager permite-lhe criar políticas de antimalware que contêm definições para configurações de cliente do Endpoint Protection. Implemente estas políticas antimalware nos computadores cliente. Em seguida, monitorizar a conformidade no **estado do Endpoint Protection** nó **segurança** no **monitorização** área de trabalho. Também utilizar relatórios de Endpoint Protection no **relatórios** nós.  

 Informações adicionais:  

-   [Como criar e implementar políticas antimalware do Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md) - criar, implementar e monitorizar políticas antimalware com uma lista das definições que pode configurar  

-   [Como monitorizar o Endpoint Protection no System Center Configuration Manager](monitor-endpoint-protection.md) -monitorizar relatórios de atividade, computadores cliente infetados e muito mais.  

-   [Como gerir políticas antimalware e definições do Endpoint Protection no System Center Configuration Manager de firewall](endpoint-antimalware-firewall.md) -remediar o software maligno encontrado nos computadores cliente  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Gerir a Firewall do Windows com o Endpoint Protection  
 Endpoint Protection no Configuration Manager disponibiliza gestão básica da Firewall do Windows nos computadores cliente. Para cada perfil de rede, pode configurar as seguintes definições:  

-   Ativar ou desativar a Firewall do Windows.  

-   Bloquear as ligações recebidas, incluindo as que se encontram na lista de programas permitidos.  

-   Notificar o utilizador quando a Firewall do Windows bloquear um programa novo.  

> [!NOTE]  
>  O Endpoint Protection suporta apenas a gestão da Firewall do Windows.  


 Para obter mais informações, consulte [como criar e implementar políticas de Firewall do Windows para o Endpoint Protection](create-windows-firewall-policies.md).  


## <a name="windows-defender-advanced-threat-protection"></a>O Windows Defender Advanced Threat Protection

Proteção de ponto final gere e monitoriza o Windows Defender Advanced Threat Protection (ATP). O serviço do Windows Defender ATP ajuda as empresas detetar, investigar e responder a ataques avançados na rede empresarial. Para obter mais informações, consulte [Windows Defender Advanced Threat Protection](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Fluxo de Trabalho do Endpoint Protection  
 Utilize o diagrama a seguir para ajudar a compreender o fluxo de trabalho para implementar o Endpoint Protection na sua hierarquia do Configuration Manager.  

 ![Fluxo de Trabalho do Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)  

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Cliente do Endpoint Protection para Computadores Mac e Servidores Linux  
 System Center Endpoint Protection inclui um cliente do Endpoint Protection para Linux e para computadores Mac. Estes clientes não são fornecidos com o Configuration Manager; em vez disso, tem de transferir os seguintes produtos a partir de [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

-   O System Center Endpoint Protection para Mac  

-   O System Center Endpoint Protection para Linux  


> [!IMPORTANT]  
>  Tem de ser um cliente de Licenciamento em Volume da Microsoft para transferir os ficheiros de instalação do Endpoint Protection para Linux e Mac.  

 Estes produtos não podem ser geridos a partir da consola do Configuration Manager. No entanto, um pacote de gestão do System Center Operations Manager é fornecido com os ficheiros de instalação, permitindo gerir o cliente para Linux ao utilizar o Operations Manager.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Como instalar o cliente do Endpoint Protection para computadores Mac e servidores Linux

Utilize os seguintes passos para transferir o ficheiro de imagem que contém o software de cliente do Endpoint Protection e a documentação para computadores Mac e servidores Linux.
1. Iniciar sessão para o [Centro de serviço de licenciamento em Volume da Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. Selecione o **transfere e chaves** separador no topo do Web site.
3. Filtro no produto **System Center Endpoint Protection (ramo atual)**.
4. Clique em ligação para **transferir**
5. Clique em **Continuar**. Deverá ver vários ficheiros, incluindo um com o nome: **System Center Endpoint Protection (ramo atual - versão 1606) para o SO Linux e Macintosh SO Multilanguage 32/64 bit 1878 MB ISO**.
6. Para transferir o ficheiro, clique no ícone de seta. O nome de ficheiro é **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050. ISO**.

A atualização de Janeiro de 2018 (X21 67050) inclui as seguintes versões:

- System Center Endpoint Protection para Mac 4.5.32.0 (suporte para macOS 10.13 Sierra elevada)
- O System Center Endpoint Protection para Linux 4.5.20.0 

 Para obter mais informações sobre como instalar e gerir os clientes de Endpoint Protection para computadores Linux e Mac, utilize a documentação que acompanha estes produtos. Esta documentação do produto está a ser o **documentação** pasta da. Ficheiro ISO.

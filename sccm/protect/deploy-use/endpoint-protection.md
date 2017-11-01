---
title: Endpoint Protection
titleSuffix: Configuration Manager
description: "Saiba como gerir políticas antimalware e de segurança da Firewall do Windows para computadores cliente na sua hierarquia do Configuration Manager."
ms.custom: na
ms.date: 02/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
caps.latest.revision: "11"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 308c69f4631a1bcc28f7d8460a4aa3abb02f0650
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="endpoint-protection"></a>Endpoint Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Endpoint Protection no System Center Configuration Manager permite-lhe gerir políticas antimalware e de segurança da Firewall do Windows para computadores cliente na sua hierarquia do Configuration Manager.  

> [!IMPORTANT]  
>  Tem de estar licenciados para utilizar o Endpoint Protection para gerir clientes na sua hierarquia do Configuration Manager.  

 Quando utilizar o Endpoint Protection com o Configuration Manager, tem as seguintes vantagens:  

-   Configurar políticas antimalware, definições de Firewall do Windows e gerir o Windows Defender Advanced Threat Protection em grupos selecionados de computadores  
-   Utilize o Gestor de configuração de atualizações de software para transferir os ficheiros de definição de antimalware mais recentes para manter os computadores cliente atualizados  
-   Enviar notificações por e-mail, utilizar a monitorização na consola e ver relatórios para manter os utilizadores administrativos informados quando for detetado software maligno em computadores cliente  

Começando com computadores Windows 10 e Windows Server 2016, o Windows Defender já está instalado. Para estes sistemas operativos, um cliente de gestão para o Windows Defender é instalado quando instala o cliente do Configuration Manager. No Windows 8.1 e anteriores computadores, o cliente do Endpoint Protection está instalado com o cliente do Configuration Manager. O Windows Defender e o cliente do Endpoint Protection tem as seguintes funcionalidades:  

-   Deteção e remediação de software maligno e spyware  
-   Deteção e remediação de rootkit  
-   Avaliação de vulnerabilidades críticas e atualizações automáticas de definições e de motor  
-   Deteção de vulnerabilidades de rede através do Sistema de Inspeção de Rede  
-   Integração com o serviço de proteção de nuvem para reportar software maligno à Microsoft. Ao aderir a este serviço, o cliente do Endpoint Protection ou o Windows Defender pode transferir as definições mais recentes a partir do Centro Microsoft de Proteção Contra Software Maligno quando é detetado software maligno não identificado num computador.  

> [!NOTE]  
>  O cliente do Endpoint Protection pode ser instalado num servidor que executa o Hyper-V e máquinas virtuais de convidados com sistemas operativos suportados. Para impedir a utilização excessiva da CPU, as ações do Endpoint Protection tem um atraso aleatório incorporado, para que os serviços de proteção não são executados em simultâneo.  

 Além disso, o Endpoint Protection no Configuration Manager permite-lhe gerir as definições da Firewall do Windows na consola do Configuration Manager.  

 [Cenário de exemplo: Utilizar o System Center Endpoint Protection para proteger os computadores contra software maligno no System Center Configuration Manager](scenarios-endpoint-protection.md) Endpoint Protection e Firewall do Windows.  


## <a name="managing-malware-with-endpoint-protection"></a>Gerir o Software Maligno com o Endpoint Protection  
 Endpoint Protection no Configuration Manager permite-lhe criar políticas de antimalware que contêm definições para configurações de cliente do Endpoint Protection. Em seguida, pode implementar estas políticas antimalware nos computadores cliente e monitorizá-las no **estado do Endpoint Protection** nó **segurança** no **monitorização** área de trabalho, ou utilizando relatórios do Configuration Manager.  

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


 Para obter mais informações sobre como criar e implementar políticas de Firewall do Windows para o Endpoint Protection, consulte [como criar e implementar políticas de Firewall do Windows para o Endpoint Protection no System Center Configuration Manager](create-windows-firewall-policies.md).  


## <a name="windows-defender-advanced-threat-protection"></a>O Windows Defender Advanced Threat Protection

A partir da versão 1606 do Configuration Manager (ramo atual), Endpoint Protection pode ajudar a gerir e monitorizar o Windows Defender Advanced Threat Protection (ATP). Windows Defender ATP é um novo serviço que o irão ajudar as empresas para detetar, analisar e responder a ataques avançados nas respetivas redes. Consulte [o Windows Defender Advanced Threat Protection](windows-defender-advanced-threat-protection.md).

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
1. Início de sessão para o [Centro de serviço de licenciamento em Volume da Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. Selecione o **transfere e chaves** separador no topo do Web site.
3. Filtro no produto **System Center Endpoint Protection (ramo atual)**.
4. Clique em ligação para **transferir**
5. Clique em **Continuar**. Deverá ver vários ficheiros, incluindo um com o nome: **System Center Endpoint Protection (ramo atual - versão 1606) para o SO Linux e Macintosh SO Multilanguage 32/64 bit 1579 MB ISO**.
6. Clique no ícone de seta para transferir o ficheiro. O nome de ficheiro é **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-2_EptProt_Lin_Mac_MLF_X21-44498. ISO**.

Este Julho atualização 2017 (X21 44498) inclui o seguinte:

- System Center Endpoint Protection para Mac 4.5.28.1 (certificado de instalação atualizados)
- System Center Endpoint Protection para Linux 4.5.18.0 (novos pacotes de idiomas)
- System Center Endpoint Protection para Linux documentação (revista orientações sobre a proteção em tempo real)

 Para mais informações sobre como instalar e gerir os clientes do Endpoint Protection para computadores Linux e Mac, utilize a documentação que acompanha estes produtos, que está localizada na pasta **Documentação** .

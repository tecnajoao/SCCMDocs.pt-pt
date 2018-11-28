---
title: Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como gerir políticas antimalware e a segurança da Firewall do Windows para clientes.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3e8c6cb33032b0c4283f3e35cbfa7b68535751ea
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456112"
---
# <a name="endpoint-protection"></a>Endpoint Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Proteção de ponto final gere políticas antimalware e segurança da Firewall do Windows para computadores cliente na sua hierarquia do Configuration Manager.  

> [!IMPORTANT]  
>  Têm de estar licenciados para utilizar o Endpoint Protection para gerir clientes na sua hierarquia do Configuration Manager.  

 Quando utilizar o Endpoint Protection com o Configuration Manager, tem as seguintes vantagens:  

-   Configurar políticas de antimalware, definições da Firewall do Windows e gerir o Windows Defender proteção avançada contra ameaças em grupos de computadores selecionados  
-   Utilize o Gestor de configuração de atualizações de software para transferir os ficheiros de definição de antimalware mais recentes para manter os computadores cliente atualizados  
-   Enviar notificações por e-mail, utilizar a monitorização na consola e ver relatórios. Estas ações informam os utilizadores administrativos quando é detetado software maligno em computadores cliente.  

A partir de computadores Windows 10 e Windows Server 2016, Windows Defender já está instalado. Para estes sistemas operativos, um cliente de gestão para o Windows Defender é instalado quando instala o cliente do Configuration Manager. No Windows 8.1 e computadores anteriores, o cliente do Endpoint Protection é instalado com o cliente do Configuration Manager. O Windows Defender e o cliente do Endpoint Protection tem as seguintes funcionalidades:  

-   Deteção e remediação de software maligno e spyware  
-   Deteção e remediação de rootkit  
-   Avaliação de vulnerabilidades críticas e atualizações automáticas de definições e de motor  
-   Deteção de vulnerabilidades de rede através do Sistema de Inspeção de Rede  
-   Integração com o serviço de proteção de Cloud para reportar software maligno à Microsoft. Ao aderir a este serviço, o cliente do Endpoint Protection ou o Windows Defender transfere as definições mais recentes do Malware Protection Center quando software maligno não identificado é detetado num computador.  

> [!NOTE]  
>  O cliente do Endpoint Protection pode ser instalado num servidor que executa o Hyper-V e em máquinas de virtuais de convidados com sistemas operativos suportados. Para impedir a utilização excessiva da CPU, ações do Endpoint Protection tem um atraso aleatório incorporado, para que os serviços de proteção não sejam executadas simultaneamente.  

 Além disso, pode gerir definições do Firewall do Windows com o Endpoint Protection na consola do Configuration Manager.  

 [Cenário exemplo: Usando o System Center Endpoint Protection para proteger os computadores contra software maligno no System Center Configuration Manager](scenarios-endpoint-protection.md) Endpoint Protection e Firewall do Windows.  


## <a name="managing-malware-with-endpoint-protection"></a>Gerir o Software Maligno com o Endpoint Protection  
 Endpoint Protection no Configuration Manager permite-lhe criar políticas de antimalware que contêm as definições para configurações de cliente do Endpoint Protection. Implemente estas políticas antimalware em computadores cliente. Em seguida, monitorizar a conformidade no **estado do Endpoint Protection** no nó **segurança** no **monitorização** área de trabalho. Use também os relatórios de Endpoint Protection do **relatórios** nó.  

 Informações adicionais:  

-   [Como criar e implementar políticas antimalware do Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md) – criar, implementar e monitorizar políticas antimalware com uma lista das definições que pode configurar  

-   [Como monitorizar o Endpoint Protection no System Center Configuration Manager](monitor-endpoint-protection.md) -monitorizar relatórios de atividade, computadores cliente infetados e muito mais.  

-   [Como gerir políticas antimalware e definições para o Endpoint Protection no System Center Configuration Manager da firewall](endpoint-antimalware-firewall.md) -remediar o software maligno encontrado nos computadores cliente  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Gerir a Firewall do Windows com o Endpoint Protection  
 Endpoint Protection no Configuration Manager fornece gestão básica do Firewall do Windows em computadores cliente. Para cada perfil de rede, pode configurar as seguintes definições:  

-   Ativar ou desativar a Firewall do Windows.  

-   Bloquear as ligações recebidas, incluindo as que se encontram na lista de programas permitidos.  

-   Notificar o utilizador quando a Firewall do Windows bloquear um programa novo.  

> [!NOTE]  
>  O Endpoint Protection suporta apenas a gestão da Firewall do Windows.  


 Para obter mais informações, consulte [como criar e implementar políticas de Firewall do Windows para o Endpoint Protection](create-windows-firewall-policies.md).  


## <a name="windows-defender-advanced-threat-protection"></a>Proteção Avançada Contra Ameaças do Windows Defender

Endpoint Protection gerencia e monitora a proteção de ameaças avançada do Windows Defender (ATP). O serviço do Windows Defender ATP ajuda as empresas a detetar, investigar e responder a ataques avançados na rede empresarial. Para obter mais informações, consulte [a proteção de ameaças avançada do Windows Defender](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Fluxo de Trabalho do Endpoint Protection  
 Utilize o diagrama a seguir para ajudar a compreender o fluxo de trabalho para implementar o Endpoint Protection na sua hierarquia do Configuration Manager.  

 ![Fluxo de Trabalho do Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)  



## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Cliente do Endpoint Protection para Computadores Mac e Servidores Linux  

> [!Important]  
> Suporte para o System Center Endpoint Protection (SCEP) para Mac e Linux (todas as versões) termina a 31 de Dezembro de 2018. Disponibilidade da nova definição de vírus para o SCEP para Mac e o SCEP para Linux pode ser interrompida após o fim do suporte. Para obter mais informações, consulte [final de mensagem de blogue de suporte](https://go.microsoft.com/fwlink/?linkid=870182).  

 System Center Endpoint Protection inclui um cliente do Endpoint Protection para Linux e para computadores Mac. Estes clientes não são fornecidos com o Configuration Manager. Transferir os seguintes produtos a partir da [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx):  

-   O System Center Endpoint Protection para Mac  

-   O System Center Endpoint Protection para Linux  


> [!Note]  
>  Tem de ser um cliente de Licenciamento em Volume da Microsoft para transferir os ficheiros de instalação do Endpoint Protection para Linux e Mac.  

 Estes produtos não podem ser geridos a partir da consola do Configuration Manager. Um pacote de gestão do System Center Operations Manager é fornecido com os ficheiros de instalação que permite-lhe gerir o cliente para Linux.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Como obter o cliente do Endpoint Protection para computadores Mac e servidores Linux

Utilize os seguintes passos para transferir o ficheiro de imagem que contém o software de cliente do Endpoint Protection e a documentação para computadores Mac e servidores Linux.
1. Inicie sessão para o [Centro de atendimento de licenciamento em Volume da Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. Selecione o **Downloads e chaves** separador na parte superior do Web site.
3. Filtro no produto **System Center Endpoint Protection (ramo atual)**.
4. Clique em ligação para **transferir**
5. Clique em **Continuar**. Verá vários arquivos, incluindo um denominado: **System Center Endpoint Protection (ramo atual - versão 1606) para o SO Linux e Macintosh SO Multilíngüe 32/64 bit 1878 MB ISO**.
6. Para transferir o ficheiro, clique no ícone de seta. O nome de ficheiro é **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050. ISO**.

A atualização de Janeiro de 2018 (X21 67050) inclui as seguintes versões:

- System Center Endpoint Protection para Mac 4.5.32.0 (suporte para macOS 10.13 High Sierra)
- O System Center Endpoint Protection para Linux 4.5.20.0 

 Para obter mais informações sobre como instalar e gerir os clientes de Endpoint Protection para computadores Linux e Mac, utilize a documentação que acompanha estes produtos. Esta documentação de produto é no **documentação** pasta da. Ficheiro ISO.

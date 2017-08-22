---
title: "Definições de firewall e a porta de cliente do Windows | Microsoft Docs"
description: "Selecione a Firewall do Windows e definições de porta para clientes no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dce4b640-c92f-401a-9873-ce9aa9262014
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 79686514efcba344c4babc3d3be03b48adca7132
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="windows-firewall-and-port-settings-for-clients-in-system-center-configuration-manager"></a>Firewall do Windows e definições de porta para clientes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os computadores cliente no System Center Configuration Manager que executam a Firewall do Windows, muitas vezes, necessitam que sejam configuradas exceções para permitir a comunicação com o respetivo site. As exceções que é necessário configurar dependem das funcionalidades de gestão que utiliza com o cliente do Configuration Manager.  

 Utilize as secções seguintes para identificar estas funcionalidades de gestão e para mais informações sobre como configurar a Firewall do Windows para estas exceções.  

##  <a name="BKMK_ModifyingWindowsFirewall"></a> Modificar as Portas e Programas Permitidos pela Firewall do Windows  
 Utilize o procedimento seguinte para modificar as portas e programas na Firewall do Windows para o cliente do Configuration Manager.  

#### <a name="to-modify-the-ports-and-programs-permitted-by-windows-firewall"></a>Para modificar as portas e programas permitidos pela Firewall do Windows  

1.  No computador que executa a Firewall do Windows, abra o Painel de Controlo.  

2.  Clique com o botão direito do rato em **Firewall do Windows**e, em seguida, clique em **Abrir**.  

3.  Configure as exceções necessárias e as portas e programas personalizados de que necessita.  

## <a name="programs-and-ports-that-configuration-manager-requires"></a>Programas e Portas Requeridos pelo Configuration Manager  
 As seguintes funcionalidades do Configuration Manager requerem exceções na Firewall do Windows:  

### <a name="queries"></a>Consultas  
 Se executar a consola do Configuration Manager num computador que executa a Firewall do Windows, as consultas falhar na primeira vez que forem executadas e o sistema operativo apresenta uma caixa de diálogo a perguntar se pretende desbloquear statview.exe. Se desbloquear statview.exe, as consultas posteriores serão executadas sem erros. Também pode adicionar manualmente Statview.exe à lista de programas e serviços no separador **Exceções** da Firewall do Windows antes de executar uma consulta.  

### <a name="client-push-installation"></a>Instalação Push do Cliente  
 Para utilizar a instalação push de cliente para instalar o cliente do Configuration Manager, adicione o seguinte como exceções à Firewall do Windows:  

-   Saída e entrada: **Ficheiro de partilha e impressoras**  

-   Entrada: **Windows Management Instrumentation (WMI)**  

### <a name="client-installation-by-using-group-policy"></a>Instalação de Cliente Utilizando a Política de Grupo  
 Para utilizar a política de grupo para instalar o cliente do Configuration Manager, adicione **impressora partilha de ficheiros e** como uma exceção à Firewall do Windows.  

### <a name="client-requests"></a>Pedidos de Cliente  
 Para computadores de cliente comunicar com sistemas de sites do Configuration Manager, adicione o seguinte como exceções à Firewall do Windows:  

 Saída: A porta TCP **80** (para comunicação HTTP)  

 Saída: A porta TCP **443** (para comunicação HTTPS)  

> [!IMPORTANT]  
>  Estes são os números de porta predefinidos que podem ser alterados no Configuration Manager. Para obter mais informações, consulte como [como configurar portas de comunicação de cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md). Se os valores predefinidos destas portas tiverem sido alterados, também deve configurar exceções correspondentes na Firewall do Windows.  

### <a name="client-notification"></a>Notificação de cliente  
 Para o ponto de gestão notificar os computadores cliente sobre uma ação que tem de executar quando um utilizador administrativo seleciona uma ação de cliente na consola do Configuration Manager, tal como transferirem a política de computador ou iniciar uma análise de malware, adicione o seguinte como uma exceção à Firewall do Windows:  

 Saída: A porta TCP **10123**  

 Se esta comunicação não funcionar, o Configuration Manager automaticamente utilizará o existente ponto de gestão de clientes comunicação porta da HTTP ou HTTPS:  

 Saída: A porta TCP **80** (para comunicação HTTP)  

 Saída: A porta TCP **443** (para comunicação HTTPS)  

> [!IMPORTANT]  
>  Estes são os números de porta predefinidos que podem ser alterados no Configuration Manager. Para obter mais informações, consulte [como configurar portas de comunicação de cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md). Se os valores predefinidos destas portas tiverem sido alterados, também deve configurar exceções correspondentes na Firewall do Windows.  

### <a name="remote-control"></a>Controlo Remoto  
 Para utilizar o controlo remoto do Configuration Manager, permita a seguinte porta:  

-   Entrada: A porta TCP**2701**  

### <a name="remote-assistance-and-remote-desktop"></a>Assistência Remota e Ambiente de Trabalho Remoto  
 Para iniciar a assistência remota da consola do Configuration Manager, adicione o programa personalizado **Helpsvc.exe** e a porta de entrada personalizada TCP **135** à lista de permitidos serviços e programas na Firewall do Windows no computador cliente. Deve também permitir **Assistência Remota** e **Ambiente de Trabalho Remoto**. Se iniciar a Assistência Remota a partir do computador cliente, a Firewall do Windows configura e permite automaticamente **Assistência Remota** e **Ambiente de Trabalho Remoto**.  

### <a name="wake-up-proxy"></a>Proxy de Reativação  
 Se ativar a definição de cliente do proxy de reativação, um novo serviço com a designação Proxy de Reativação do ConfigMgr utiliza um protocolo ponto a ponto para verificar se outros computadores estão ativos na sub-rede e ativa-os se for necessário. Esta comunicação utiliza as seguintes portas:  

 Saída: Porta UDP **25536**  

 Saída: Porta UDP **9**  

 Estes são os números de porta predefinidos que podem ser alterados no Configuration Manager utilizando o **gestão de energia** definições de clientes de **número de porta de proxy de reativação (UDP)** e **o número de porta de reativação por LAN (UDP)**. Se especificar o **gestão de energia**: **Exceção de Firewall do Windows para proxy de reativação** cliente definição, estas portas são configuradas automaticamente na Firewall do Windows para clientes. No entanto, se os clientes executarem uma firewall diferente, tem de configurar manualmente as exceções para estes números de porta.  

 Além destas portas, o proxy de reativação também utiliza mensagens de pedido de eco de ICMP (Internet Control Message Protocol) de um computador cliente para outro computador cliente. Esta comunicação é utilizada para confirmar se o outro computador cliente está ativo na rede. Por vezes, o ICMP é também referido como comandos ping de TCP/IP.  

 Para obter mais informações sobre o proxy de reativação, consulte [planear como reativar os clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

### <a name="windows-event-viewer-windows-performance-monitor-and-windows-diagnostics"></a>Visualizador de Eventos do Windows, Monitor de Desempenho do Windows e Diagnóstico do Windows  
 Para aceder ao Visualizador de eventos do Windows, o Monitor de desempenho do Windows e diagnóstico do Windows a partir da consola do Configuration Manager, ative **impressora partilha de ficheiros e** como uma exceção na Firewall do Windows.  

## <a name="ports-used-during-configuration-manager-client-deployment"></a>Portas Utilizadas Durante a Implementação do Cliente do Configuration Manager  
 As tabelas seguintes listam as portas que são utilizadas durante o processo de instalação do cliente.  

> [!IMPORTANT]  
>  Se existir uma firewall entre os servidores do sistema de sites e o computador cliente, confirme se a firewall permite tráfego para as portas que são necessárias para o método de instalação do cliente que selecionou. Por exemplo, as firewalls impedem frequentemente que a instalação push seja bem sucedida porque bloqueiam o Bloco de Mensagem de Servidor (SMB) e as Chamadas de Procedimento Remoto (RPC). Neste cenário, utilize um método diferente de instalação do cliente, tal como a instalação manual (com CCMSetup.exe) ou a instalação do cliente baseada na Política de Grupo. Estes métodos alternativos de instalação do cliente não necessitam de SMB ou RPC.  

 Para obter informações sobre como configurar a Firewall do Windows no computador cliente, consulte [Modificar as Portas e Programas Permitidos pela Firewall do Windows](#BKMK_ModifyingWindowsFirewall).  

### <a name="ports-that-are-used-for-all-installation-methods"></a>Portas que são utilizadas para todos os métodos de instalação  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol) do computador cliente para um ponto de estado de contingência, quando está atribuído um ponto de estado de contingência ao cliente.|--|80 (Ver nota 1, **Porta Alternativa Disponível**)|  

### <a name="ports-that-are-used-with-client-push-installation"></a>Portas que são utilizadas com a instalação push do cliente  
 Além das portas listadas na tabela a seguir, a instalação push do cliente também utiliza mensagens de pedido de eco ICMP (Internet Control Message Protocol) do servidor do site para o computador cliente para confirmar se este está disponível na rede. Por vezes, o ICMP é também referido como comandos ping de TCP/IP. O ICMP não tem um número de protocolo UDP ou TCP e, por isso, não está listado na tabela a seguir. No entanto, quaisquer dispositivos de rede intervenientes, tais como firewalls, devem permitir tráfego ICMP para que a instalação push do cliente seja bem sucedida.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB) entre o servidor do site e o computador cliente.|--|445|  
|Mapeador de pontos finais RPC entre o servidor do site e o computador cliente.|135|135|  
|Portas dinâmicas RPC entre o servidor do site e o computador cliente.|--|DINÂMICO|  
|Protocolo HTTP (Hypertext Transfer Protocol) do computador cliente para um ponto de gestão quando a ligação é efetuada através de HTTP.|--|80 (Ver nota 1, **Porta Alternativa Disponível**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol) do computador cliente para um ponto de gestão quando a ligação é efetuada através de HTTPS.|--|443 (Ver nota 1, **Porta Alternativa Disponível**)|  

### <a name="ports-that-are-used-with-software-update-point-based-installation"></a>Portas que são utilizadas com a instalação baseada em ponto de atualização de software  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol) do computador cliente para o ponto de atualização de software.|--|80 ou 8530 (Ver nota 2, **Windows Server Update Services**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol) do computador cliente para o ponto de atualização de software.|--|443 ou 8531 (Ver nota 2, **Windows Server Update Services**)|  
|Bloco de mensagem de servidor (SMB) entre o servidor de origem e o computador cliente quando especificar a propriedade da linha de comandos CCMSetup **/Source:&lt;caminho\>**.|--|445|  

### <a name="ports-that-are-used-with-group-policy-based-installation"></a>Portas que são utilizadas com a instalação baseada na Política de Grupo  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol) do computador cliente para um ponto de gestão quando a ligação é efetuada através de HTTP.|--|80 (Ver nota 1, **Porta Alternativa Disponível**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol) do computador cliente para um ponto de gestão quando a ligação é efetuada através de HTTPS.|--|443 (Ver nota 1, **Porta Alternativa Disponível**)|  
|Bloco de mensagem de servidor (SMB) entre o servidor de origem e o computador cliente quando especificar a propriedade da linha de comandos CCMSetup **/Source:&lt;caminho\>**.|--|445|  

### <a name="ports-that-are-used-with-manual-installation-and-logon-script-based-installation"></a>Portas que são utilizadas com a instalação manual e com a instalação baseada em scripts de início de sessão  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB) entre o computador cliente e uma partilha de rede a partir da qual o CCMSetup.exe é executado.<br /><br /> Quando instalar o Configuration Manager, os ficheiros de origem de instalação do cliente são copiados e automaticamente partilhados a partir de  *&lt;Caminhodainstalação\>*pasta \Client nos pontos de gestão. No entanto, pode copiar esses ficheiros e criar uma nova partilha em qualquer computador na rede. Em alternativa, pode eliminar este tráfego de rede executando o CCMSetup.exe localmente, por exemplo, utilizando um suporte de dados amovível.|--|445|  
|Protocolo HTTP (Hypertext Transfer) do computador cliente para um ponto de gestão quando a ligação é efetuada através de HTTP e não especificar a propriedade da linha de comandos CCMSetup **/Source:&lt;caminho\>**.|--|80 (Ver nota 1, **Porta Alternativa Disponível**)|  
|Secure Hypertext Transfer Protocol (HTTPS) do computador cliente para um ponto de gestão quando a ligação é efetuada através de HTTPS e não especificar a propriedade da linha de comandos CCMSetup **/Source:&lt;caminho\>**.|--|443 (Ver nota 1, **Porta Alternativa Disponível**)|  
|Bloco de mensagem de servidor (SMB) entre o servidor de origem e o computador cliente quando especificar a propriedade da linha de comandos CCMSetup **/Source:&lt;caminho\>**.|--|445|  

### <a name="ports-that-are-used-with-software-distribution-based-installation"></a>Portas que são utilizadas com a instalação baseada em distribuição de software  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB) entre o ponto de distribuição e o computador cliente.|--|445|  
|Protocolo HTTP (Hypertext Transfer Protocol) do computador cliente para um ponto de distribuição quando a ligação é efetuada através de HTTP.|--|80 (Ver nota 1, **Porta Alternativa Disponível**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol) do computador cliente para um ponto de distribuição quando a ligação é efetuada através de HTTPS.|--|443 (Ver nota 1, **Porta Alternativa Disponível**)|  

## <a name="notes"></a>Notas  
 **1 porta alternativa disponível** no Configuration Manager, pode definir uma porta alternativa para este valor. Se tiver sido definida uma porta personalizada, substitua-a quando definir as informações de filtro IP para políticas IPsec ou para configurar firewalls.  

 **2 Windows Server Update Services** É possível instalar o Windows Server Update Service (WSUS) no Web site predefinido (porta 80) ou num Web site personalizado (porta 8530).  

 Após a instalação, é possível alterar a porta. Não é necessário utilizar o mesmo número de porta ao longo da hierarquia do site.  

 Se a porta HTTP for 80, a porta HTTPS tem de ser 443.  

 Se a porta HTTP for qualquer outra, a porta HTTPS tem de ser 1 superior. Por exemplo, 8530 e 8531.

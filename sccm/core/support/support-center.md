---
title: Centro de Suporte
titleSuffix: Configuration Manager
description: Resolver problemas de clientes do Configuration Manager com o Centro de suporte.
ms.date: 01/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 828edc3c90b4dd93f4d86772b863816bbc8c9130
ms.sourcegitcommit: 013ca76d5a3c07306de7b5bfd985b0289d1be599
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/31/2019
ms.locfileid: "55482423"
---
# <a name="support-center-for-configuration-manager"></a>Centro de suporte para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1357489--> A partir da versão 1810, utilize o Centro de suporte para o cliente de resolução de problemas, o registo em tempo real, visualização ou capturar o estado de um computador de cliente do Configuration Manager para análise posterior. Centro de suporte é uma ferramenta única para consolidar administrador muitas ferramentas de resolução de problemas. 



## <a name="about"></a>sobre 

Tem como objetivo reduzir os desafios e frustração ao resolver problemas com computadores de cliente do Configuration Manager Support Center. Anteriormente, ao trabalhar com suporte para o endereço de um problema com clientes do Configuration Manager, terá de recolher manualmente ficheiros de registo e outras informações para ajudar a resolver o problema. Foi fácil esquecer acidentalmente um ficheiro de registo crucial, causando dores de cabeça adicionais para si e ao pessoal de suporte que está trabalhando com.

Utilize o Centro de suporte para simplificar a experiência de suporte. Permite-lhe:

 - Crie um pacote de solução de problemas (ficheiro. zip) que contém os ficheiros de registo de cliente do Configuration Manager. Em seguida, tem um único arquivo para enviar para o pessoal de suporte.  

 - Ficheiros de registo de cliente do Configuration Manager de modo de exibição, certificados, as definições de registo, informações de depuração, políticas de cliente.  

 - Diagnóstico em tempo real de inventário (substitui ContentSpy), a política (substitui PolicySpy) e a cache do cliente.  


### <a name="support-center-viewer"></a>Support Center viewer

Centro de suporte inclui o Support Center Viewer, uma ferramenta que suporta a utilização de pessoal para abrir o pacote de ficheiros que criar com o Support Center. Recoletor de dados do Support Center recolhe e empacota registos de diagnóstico de um cliente de Configuration Manager local ou remoto. Para ver os pacotes de recoletor de dados, utilize a aplicação de Visualizador.


### <a name="support-center-log-file-viewer"></a>Visualizador de arquivos de log do Centro de suporte

Centro de suporte inclui um Visualizador de log modernos. Essa ferramenta substitui a ferramenta CMTrace. OneTrace fornece uma interface personalizável com suporte para windows encaixáveis e guias. Ele tem uma camada de apresentação rápida e pode carregar ficheiros de registo grandes em segundos.


### <a name="powershell-cmdlets"></a>Cmdlets do PowerShell

Support Center também inclui [cmdlets do Windows PowerShell](https://go.microsoft.com/fwlink/?linkid=397830). Utilize estes cmdlets para criar uma ligação remota a outro cliente do Configuration Manager, para configurar as opções de recolha de dados e iniciar a recolha de dados.



## <a name="prerequisites"></a>Pré-requisitos

Instale os seguintes componentes no servidor ou computador de cliente no qual instala o Support Center:

- Uma versão do SO suportada pelo Configuration Manager. Para obter mais informações, consulte [versões de SO suportado por clientes](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices). Centro de suporte não suporta dispositivos móveis.  

- .NET framework 4.5.2 é necessário no computador em que executa o Centro de suporte e os respetivos componentes.  



## <a name="install"></a>Instalar

Localizar o instalador do Support Center no servidor do site no seguinte caminho: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

Depois de instalá-lo, localize os seguintes itens no menu Iniciar no **Microsoft System Center** grupo:  
- Support Center (ConfigMgrSupportCenter.exe)  
- Visualizador de arquivos de Log do Centro de suporte (CMLogViewer.exe)  
- Support Center Viewer (ConfigMgrSupportCenterViewer.exe)  



## <a name="known-issues"></a>Problemas conhecidos 

#### <a name="remote-connections-must-include-computer-name-or-domain-as-part-of-the-user-name"></a>Ligações remotas têm de incluir o nome de computador ou o domínio como parte do nome do utilizador
Se ligar a um cliente remoto a partir do Centro de suporte, tem de fornecer o nome da máquina ou o nome de domínio da conta de utilizador ao estabelecer a ligação. Se usar um nome de computador ou o nome de domínio (por exemplo, `.\administrator`), a ligação tiver êxito, mas o Support Center não recolhe dados do cliente. 

Para evitar este problema, utilize os seguintes formatos de nome de utilizador para ligar a um cliente remoto: 
- `ComputerName\UserName`  
- `DomainName\UserName`  

#### <a name="scripted-server-message-block-connections-to-remote-clients-might-require-removal"></a>Ligações do script do server message block a clientes remotos podem requerer remoção
Ao ligar a clientes remotos com o [New-CMMachineConnection](https://go.microsoft.com/fwlink/p/?linkid=390542) cmdlet do PowerShell, o Support Center cria uma ligação ao servidor message block (SMB) para cada cliente remoto. Mantém as ligações depois de concluir a recolha de dados. Para evitar exceder o número máximo de ligações remotas para o Windows, utilize o `net use` comando para ver o conjunto ativo no momento de ligações remotas. Em seguida, desative todas as ligações desnecessárias utilizando o seguinte comando: `net use <connection_name> /d` 
onde `<connection_name>` é o nome da ligação remota.

#### <a name="application-deployment-evaluation-cycle-request-isnt-sent-correctly-to-remote-machines"></a>Pedido de ciclo de avaliação de implementação de aplicações não está enviado corretamente para máquinas remotas
<!--2849356--> No Centro de suporte, se selecionar **avaliação de implementação de aplicação** partir a **Invoke acionador** ação no **conteúdo** guia, esta ação inicia uma tarefa que avalia aplicações implementadas. Se estiver ligado a um cliente local, ele avalia as implementações de aplicações do computador e utilizador. No entanto, se estiver ligado a um cliente remoto, apenas avalia as implementações de aplicações de máquina.


## <a name="next-steps"></a>Passos seguintes

[Início rápido do Centro de suporte](/sccm/core/support/support-center-quickstart)

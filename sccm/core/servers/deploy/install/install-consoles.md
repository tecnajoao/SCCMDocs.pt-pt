---
title: Instalar a consola
titleSuffix: Configuration Manager
description: Instale a consola do Configuration Manager para ligar a um site de administração central ou site primário.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f17e479ef6b285cdb70960471dced73e83af520c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339439"
---
# <a name="install-the-system-center-configuration-manager-console"></a>Instalar a consola do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os administradores utilizar a consola do Configuration Manager para gerir o ambiente do Configuration Manager. Cada consola do Configuration Manager pode ligar a um site de administração central ou a um site primário. Não é possível ligar uma consola do Configuration Manager para um site secundário.

> [!NOTE]  
>  Um administrador vê objetos na consola com base nas permissões atribuídas à conta de utilizador. Para obter mais informações sobre a administração baseada em funções, consulte [Noções básicas da administração baseada em funções](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Quando instala o servidor do site, pode instalar a consola do Configuration Manager ao mesmo tempo. Para instalar o consola separado da instalação do servidor do site, execute o instalador autónomo.  

 Utilize os procedimentos seguintes para instalar a consola do Configuration Manager, utilizando o instalador autónomo.  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>Para instalar a consola do Configuration Manager, utilizando o Assistente de configuração  

1.  Certifique-se de que cumpre estes requisitos:  

    -  Tiver local **administrador** direitos no computador de destino para a consola.  

    -   Tiver **leitura** ficheiros de instalação da consola de permissões para a localização do Configuration Manager.  

2.  Ir para uma destas localizações:  

    -   No servidor do site, aceda a: `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   Do suporte de dados de origem do Configuration Manager, aceda a: `<Configuration Manager source files>\Smssetup\Bin\I386`  

    > [!TIP]  
    >  Como melhor prática, inicie o programa de instalação de consola do Configuration Manager de um servidor de site, em vez do suporte de dados de instalação do System Center Configuration Manager. Quando instala um servidor de site, copia os ficheiros de instalação de consola do Configuration Manager e pacotes de idiomas suportados para o site para o **tools\consolesetup.** subpasta. Instalar a consola do Configuration Manager a partir do suporte de instalação do sempre instalada a versão inglesa. Este comportamento ocorre mesmo que o servidor de site suporta idiomas diferentes ou SO de computador de destino está definido para um idioma diferente. Opcionalmente, pode copiar o **ConsoleSetup** pasta para uma localização alternativa para iniciar a instalação.

3.  Para abrir o Assistente de configuração de consola do Configuration Manager, faça duplo clique **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Instale sempre a consola do Configuration Manager utilizando **consolesetup.exe**. Apesar de poder instalar a consola do Configuration Manager ao executar adminconsole.msi, este método não é executado pré-requisitos ou de verificações de dependência. A instalação não poderá instalar corretamente.  

4.  No assistente, selecione **seguinte**.  

5.  No **servidor do Site** página, introduza o nome de domínio completamente qualificado (FQDN) do servidor do site ao qual se liga a consola do Configuration Manager.  

6.  No **pasta de instalação** página, introduza a pasta de instalação da consola do Configuration Manager. O caminho da pasta não pode conter espaços à direita nem carateres Unicode.  

7.  No **programa de melhoramento da experiência do cliente** página, selecione se pretende associar o programa de melhoramento da experiência do cliente (PMEC).  
    > [!Note]  
    > A partir do Configuration Manager versão 1802 a funcionalidade CEIP é removida do produto.

8.  No **pronto para instalar** página, selecione **instalar** para instalar a consola do Configuration Manager.  



## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>Para instalar a consola do Configuration Manager numa linha de comandos  

1.  No servidor no qual instalar a consola do Configuration Manager, abra uma janela da linha de comandos e aceda a uma das seguintes localizações:  

    -   `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    > [!TIP]  
    >  Instalar a consola do Configuration Manager numa linha de comandos sempre instalada a versão inglesa. Este comportamento ocorre, mesmo se SO o computador de destino estiver definido para um idioma diferente. Para instalar a consola do Configuration Manager num idioma diferente do inglês, deve [instalar a consola do Configuration Manager, utilizando o Assistente de configuração](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  Na linha de comandos, escreva **consolesetup.exe**. Escolha uma das seguintes opções da linha de comandos:  

|  Opção da linha de comandos     | Descrição     |
  |-------------|-------------|
  |/q|Instala a consola do Gestor de configuração automática. O **EnableSQM**, **TargetDir**, e **DefaultSiteServerName** opções são necessárias quando utiliza esta opção.|  
  |/uninstall|Desinstala a consola do Configuration Manager. Especificar esta opção primeiro quando a utilizar com o **/q** opção.|  
  |LangPackDir|Especifica o caminho para a pasta que contém os ficheiros de idioma. Pode utilizar **dispositivo de transferência da configuração** para transferir os ficheiros de idioma. Se utilizar esta opção, a configuração procurará a pasta de idioma na pasta atual. Se a pasta de idioma não for encontrada, o programa de configuração continua a instalar apenas inglês. Para obter mais informações, consulte [dispositivo de transferência da configuração](setup-downloader.md).|  
  |TargetDir|Especifica a pasta de instalação para instalar a consola do Configuration Manager. Esta opção é necessária quando utiliza o **/q** opção.|  
  |EnableSQM|Especifica se pretende associar o programa de melhoramento da experiência do cliente (PMEC). Utilize um valor de **1** para aderir ao CEIP e um valor de **0** não participar no programa. Esta opção é necessária quando utiliza o **/q** opção.</br></br>Nota: A partir do Configuration Manager versão 1802 a funcionalidade CEIP é removida do produto.|  
  |DefaultSiteServerName|Especifica o FQDN do servidor do site ao qual a consola liga quando é aberta. Esta opção é necessária quando utiliza o **/q** opção.|  


  ### <a name="examples"></a>Exemplos

  -  `consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com`  

  -  `consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr Console" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com`  

  -  `consolesetup.exe /uninstall /q`  

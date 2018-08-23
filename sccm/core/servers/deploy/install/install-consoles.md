---
title: Instalar consola
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
ms.openlocfilehash: a8d1d0a727f0a4ad4a2bfc25141f7e2982494080
ms.sourcegitcommit: b596d944e49f3c4912c6ca91915ed1418c17a1a2
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/16/2018
ms.locfileid: "42586225"
---
# <a name="install-the-system-center-configuration-manager-console"></a>Instalar a consola do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os administradores de utilizam a consola do Configuration Manager para gerir o ambiente do Configuration Manager. Cada consola do Configuration Manager pode ligar a um site de administração central ou a um site primário. Não é possível ligar uma consola do Configuration Manager para um site secundário.

> [!NOTE]  
>  Um administrador vê objetos na consola de com base nas permissões atribuídas à conta de utilizador. Para obter mais informações sobre a administração baseada em funções, consulte [Noções básicas da administração baseada em funções](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Quando instala o servidor do site, pode instalar a consola do Configuration Manager ao mesmo tempo. Para instalar separadas da consola da instalação de servidor do site, execute o instalador autônomo.  

 Utilize os procedimentos seguintes para instalar a consola do Configuration Manager, utilizando o instalador autônomo.  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>Para instalar a consola do Configuration Manager, utilizando o Assistente de configuração  

1.  Certifique-se de que cumpre estes requisitos:  

    -  Tem locais **administrador** direitos no computador de destino para a consola.  

    -   Tiver **leitura** ficheiros de instalação da consola de permissões para a localização do Configuration Manager.  

2.  Aceda a um desses locais:  

    -   No servidor do site, aceda a: `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   A partir do suporte de dados de origem do Configuration Manager, aceda a: `<Configuration Manager source files>\Smssetup\Bin\I386`  

    > [!TIP]  
    >  Como melhor prática, inicie o instalador de consola do Configuration Manager de um servidor de site, em vez do suporte de dados de instalação do System Center Configuration Manager. Ao instalar um servidor de site, ele copia os ficheiros de instalação de consola do Configuration Manager e pacotes de idioma suportados para o site para o **tools\consolesetup.** subpasta. Instalar a consola do Configuration Manager da mídia de instalação sempre instala a versão em inglês. Este comportamento acontece mesmo que o servidor do site suporta idiomas diferentes, ou o SO do computador de destino está definido como um idioma diferente. Opcionalmente, pode copiar o **ConsoleSetup** pasta para uma localização alternativa para iniciar a instalação.

3.  Para abrir o Assistente de configuração de consola do Configuration Manager, faça duplo clique em **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Sempre instalar a consola do Configuration Manager, utilizando **consolesetup.exe**. Embora possa instalar a consola do Configuration Manager ao executar adminconsole, esse método não executa os pré-requisitos ou verificações de dependência. A instalação poderá não ser instalado corretamente.  

4.  No assistente, selecione **seguinte**.  

5.  Sobre o **servidor do Site** página, introduza o nome de domínio completamente qualificado (FQDN) do servidor do site ao qual se liga a consola do Configuration Manager.  

6.  Sobre o **pasta de instalação** página, introduza a pasta de instalação da consola do Configuration Manager. O caminho da pasta não pode conter espaços ou carateres Unicode.  

7.  Sobre o **programa de melhoramento da experiência do cliente** , selecione se pretende aderir o programa de melhoramento da experiência do cliente (PMEC).  
    > [!Note]  
    > A partir do Configuration Manager versão 1802 a funcionalidade CEIP é removida do produto.

8.  Sobre o **pronto para instalar** página, selecione **instalar** para instalar a consola do Configuration Manager.  



## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>Para instalar a consola do Configuration Manager numa linha de comandos  

1.  No servidor do qual instala a consola do Configuration Manager, abra uma janela da linha de comando e aceder a uma das seguintes localizações:  

    -   `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    > [!TIP]  
    >  Instalar a consola do Configuration Manager num prompt de comando sempre instala a versão em inglês. Este comportamento acontece mesmo que o SO do computador de destino está definido como um idioma diferente. Para instalar a consola do Configuration Manager num idioma diferente do inglês, deve [instalar a consola do Configuration Manager utilizando o Assistente de configuração](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  No prompt de comando, digite **consolesetup.exe**. Escolha entre as seguintes opções da linha de comandos:  

|  Opção da linha de comandos     | Descrição     |
  |-------------|-------------|
  |/q|Instala a consola do Gestor de configuração automática. O **Defaultsiteservername**, **TargetDir**, e **DefaultSiteServerName** opções são necessárias quando utiliza esta opção.|  
  |/uninstall|Desinstala a consola do Configuration Manager. Especificar esta opção primeiro quando usá-lo com o **/q** opção.|  
  |LangPackDir|Especifica o caminho para a pasta que contém os ficheiros de idioma. Pode usar **programa de configuração** para transferir os ficheiros de idioma. Se não utilizar esta opção, a configuração procurará a pasta de idioma na pasta atual. Se a pasta de idioma não for encontrada, o programa de configuração continua a instalar apenas o inglês. Para obter mais informações, consulte [programa de configuração](setup-downloader.md).|  
  |TargetDir|Especifica a pasta de instalação para instalar a consola do Configuration Manager. Esta opção é necessária quando utiliza a **/q** opção.|  
  |EnableSQM|Especifica se pretende aderir o programa de melhoramento da experiência do cliente (PMEC). Utilizar o valor **1** para aderir ao CEIP e um valor de **0** não aderir ao programa. Esta opção é necessária quando utiliza a **/q** opção.</br></br>Nota: A partir do Configuration Manager versão 1802 a funcionalidade CEIP é removida do produto.  Utilizar o parâmetro fará com que a instalação falha.|  
  |DefaultSiteServerName|Especifica o FQDN do servidor do site ao qual se liga a consola quando é aberta. Esta opção é necessária quando utiliza a **/q** opção.|  


  ### <a name="examples"></a>Exemplos
  **Para a versão 1802 e mais recente não inclua o parâmetro Defaultsiteservername**
  -  `ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

  -  `ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com EnableSQM=1  LangPackDir=C:\Downloads\ConfigMgr`  

  -  `ConsoleSetup.exe /uninstall /q`  

---
title: Instalar a consola
titleSuffix: Configuration Manager
description: "Leia sobre como instalar a consola do Configuration Manager para ligar a um site de administração central ou site primário."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: "3"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: ca1c62fc6034b33380d9075c4f5430954537781f
ms.sourcegitcommit: e121d8d3dd82b9f2dde2cb5206cbee602ab8e107
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/17/2018
---
# <a name="install-the-system-center-configuration-manager-console"></a>Instalar a consola do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os administradores de utilizam a consola do System Center Configuration Manager para gerir o ambiente do Configuration Manager. Cada consola do Configuration Manager pode ligar a um site de administração central ou a um site primário. Não é possível ligar uma consola do Configuration Manager para um site secundário.

> [!NOTE]  
>  Que objetos que está a executar a consola do administrador vê dependem as permissões que são atribuídas à conta de utilizador. Para obter mais informações sobre a administração baseada em funções, consulte [Noções básicas da administração baseada em funções para o System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Pode instalar a consola do Configuration Manager durante a instalação do servidor de site através do Assistente de configuração ou pode executar uma aplicação de instalação autónoma que utiliza o Assistente de configuração.  

 Utilize o procedimento seguinte para instalar uma consola do Configuration Manager utilizando a aplicação autónoma.  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>Para instalar a consola do Configuration Manager, utilizando o Assistente de configuração  

1.  Certifique-se de que cumpre estes requisitos:  

    -  Tiver **Administrador Local** direitos no computador no qual a consola será executada.  

    -   Tiver **leitura** ficheiros de instalação da consola de permissões para a localização do Configuration Manager.  

2.  Ir para uma destas localizações:  

    -   No servidor do site, aceda a  **< *caminho de instalação do servidor de site do Configuration Manager*> \Tools\ConsoleSetup**.  

    -   Do suporte de dados de origem do Configuration Manager, aceda a  **< *ficheiros de origem do Configuration Manager*> \Smssetup\Bin\I386**.  

    > [!TIP]  
    >  Como melhor prática, inicie a instalação da consola do Configuration Manager de um servidor de site, em vez do suporte de dados de instalação do System Center Configuration Manager. O método de instalação do servidor de site copia os ficheiros de instalação de consola do Configuration Manager e pacotes de idiomas suportados para o site para o **tools\consolesetup.** subpasta. Instalar a consola do Configuration Manager a partir do suporte de instalação do sempre instalada a versão inglesa, independentemente dos idiomas suportados no servidor do site ou as definições de idioma do sistema operativo que está em execução no computador. Opcionalmente, pode copiar o **ConsoleSetup** pasta para uma localização alternativa para iniciar a instalação.

3.  Para abrir o Assistente de configuração de consola do Configuration Manager, faça duplo clique **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Instale sempre a consola do Configuration Manager utilizando consolesetup.exe. Embora a consola do Configuration Manager pode ser instalada através da execução de adminconsole.msi, este método não executa os pré-requisitos ou dependências verificações e a instalação poderá não ser instalados correctamente.  

4.  No assistente, selecione **seguinte**.  

5.  No **servidor do Site** página, introduza o nome de domínio completamente qualificado (FQDN) do servidor do site ao qual a consola do Configuration Manager irá ligar.  

6.  No **pasta de instalação** página, introduza a pasta de instalação da consola do Configuration Manager. O caminho da pasta não pode conter espaços à direita nem carateres Unicode.  

7.  No **programa de melhoramento da experiência do cliente** página, selecione se pretende associar o programa de melhoramento da experiência do cliente (PMEC).  

8.  No **pronto para instalar** página, selecione **instalar** para instalar a consola do Configuration Manager.  

## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>Para instalar a consola do Configuration Manager numa linha de comandos  

1.  No servidor do qual instala a consola do Configuration Manager, abra uma janela da linha de comandos e aceda a uma das seguintes localizações:  

    -   **<*Caminho de instalação do servidor de site do Configuration Manager*> \Tools\ConsoleSetup**  

    -   **<*Suporte de instalação do Configuration Manager*> \SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  Quando instalar a consola do Configuration Manager numa linha de comandos, a versão inglesa é sempre instalada, independentemente da definição de idioma do sistema operativo que está em execução no computador. Para instalar a consola do Configuration Manager num idioma diferente do inglês, deve [instalar a consola do Configuration Manager, utilizando o Assistente de configuração](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  Na linha de comandos, escreva **consolesetup.exe**. Escolha uma das seguintes opções da linha de comandos.  

|  Opção da linha de comandos     | Descrição     |
  | :------------- | :------------- |
  |/q|Instala a consola do Gestor de configuração automática. O **EnableSQM**, **TargetDir**, e **DefaultSiteServerName** opções são necessárias quando utiliza esta opção.|  
  |/uninstall|Desinstala a consola do Configuration Manager. Tem de especificar esta opção primeiro quando a utilizar com o **/q** opção.|  
  |LangPackDir|Especifica o caminho para a pasta que contém os ficheiros de idioma. Pode utilizar **dispositivo de transferência da configuração** para transferir os ficheiros de idioma. Se utilizar esta opção, a configuração procurará a pasta de idioma na pasta atual. Se a pasta de idioma não for encontrada, o programa de configuração continua a instalar apenas inglês. Para obter mais informações, consulte [dispositivo de transferência da configuração](setup-downloader.md).|  
  |TargetDir|Especifica a pasta de instalação para instalar a consola do Configuration Manager. Esta opção é necessária quando utiliza o **/q** opção.|  
  |EnableSQM|Especifica se pretende associar o programa de melhoramento da experiência do cliente (PMEC). Utilize um valor de **1** para aderir ao CEIP e um valor de **0** não participar no programa. Esta opção é necessária quando utiliza o **/q** opção.|  
  |DefaultSiteServerName|Especifica o FQDN do servidor do site ao qual a consola liga quando é aberta. Esta opção é necessária quando utiliza o **/q** opção.|  


  **Exemplos:**

  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr Console" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  

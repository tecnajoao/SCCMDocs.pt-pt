---
title: "Instalação da linha de comandos | Documentos do Microsoft"
description: "Saiba como executar a configuração do System Center Configuration Manager numa linha de comandos para uma variedade das instalações de site."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: fefa5f3aa12d82b66a251cf0525475496e1e35cf
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="use-a-command-line-to-install-system-center-configuration-manager-sites"></a>Utilizar uma linha de comandos para instalar sites do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Pode executar o programa de configuração do System Center Configuration Manager numa linha de comandos para instalar uma variedade de tipos de site.

## <a name="supported-tasks-for-command-line-installations"></a>Tarefas suportadas para instalações da linha de comandos
 Este método de executar a configuração suporta a instalação do site seguinte e tarefas de manutenção do site:

-   **Instalar um site de administração central ou site primário a partir de uma linha de comandos**  
  Vista [opções da linha de comandos para a configuração](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

-  **Modificar os idiomas em utilização num site de administração central ou site primário**  
    Para modificar os idiomas que estão instalados num site a partir de uma linha de comandos (incluindo idiomas para dispositivos móveis), tem de:  

     -   Execute a configuração a partir de  **&lt;ConfigMgrInstallationPath\>\bin\x64.** no servidor do site,
     -   Utilize o **/MANAGELANGS** opção da linha de comandos,
     -   Especifique um ficheiro de script de idioma que especifica os idiomas que pretende adicionar ou remover,  

    Por exemplo, utilize a seguinte sintaxe de comando: **setupwpf.exe /MANAGELANGS &lt;ficheiro de script de idioma\>**  

    Para criar o ficheiro de script de idioma, utilize as informações no [opções de linha de comandos para gerir idiomas](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)  

-  **Utilizar um ficheiro de script de instalação para as instalações de site automática ou recuperação de site**  
    Pode executar a configuração a partir de uma linha de comandos, utilizando um script de instalação e executar uma instalação de site automática. Também pode utilizar esta opção para recuperar um site.    

    Para utilizar um script com a configuração:  

    -   Executar a configuração com a opção de linha de comandos **/SCRIPT** e especifique um ficheiro de script.  

    -   O ficheiro de script deve ser configurado com as chaves necessárias e valores.  

    Para a instalação automática de um site de administração central ou site primário, o ficheiro de script tem de ter as seguintes secções:  

    -   Identificação    
    -   Opções    
    -   SQLConfigOptions    
      -   HierarchyOptions    
    -   CloudConnectorOptions   

    Para recuperar um site, tem também de incluir as seguintes secções do ficheiro de script:  

    -   Identificação  
    -   Recuperação

Para obter mais informações sobre a cópia de segurança e recuperação, consulte o [chaves de ficheiro de script de recuperação de site automática](../../../../protect/understand/backup-and-recovery.md#BKMK_UnattendedSiteRecoveryKeys) no [cópia de segurança e recuperação no Configuration Manager](../../../../protect/understand/backup-and-recovery.md) tópico.  

Para obter uma lista de chaves e valores para utilizar um ficheiro de script de instalação automática, consulte o artigo [chaves de ficheiro de script de configuração automática](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended).  

## <a name="about-the-command-line-script-file"></a>Sobre o ficheiro de script da linha de comandos  
 Para instalações automáticas do Configuration Manager, pode executar a configuração com a opção da linha de comandos **/SCRIPT**e especifique um ficheiro de script que contém as opções de instalação. As seguintes tarefas são suportadas através deste método:  

-   Instalar um site de administração central  
-   Instalar um site primário  
-   Instalar uma consola do configuration Manager  
-   Recuperar um site  

> [!NOTE]  
>  Não é possível utilizar o ficheiro de script automático para atualizar um site de avaliação para uma instalação licenciada do Configuration Manager.  

### <a name="the-cdlatest-key-name"></a>O nome da chave CDLatest
Quando utiliza suportes de dados a partir do CD. Instalar pasta mais recente para ser executada com um script das seguintes opções de instalação de quatro, o script tem de incluir o **CDLatest** chave com um valor de **1**:
- Instalar um novo site de administração central
- Instalar um novo site primário
- Recuperar um site de administração central
- Recuperar um site primário 

Este valor não é suportado para utilização com o suporte de instalação que que obtém a partir do site de licenciamento em Volume da Microsoft.
Consulte o artigo [opções da linha de comandos](/sccm/core/servers/deploy/install/command-line-options-for-setup) para obter informações sobre como utilizar este nome da chave no ficheiro de script.



### <a name="create-the-script"></a>Criar o script
O script de instalação é criado automaticamente quando é [executar a configuração para instalar um site utilizando a interface de utilizador](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  Quando confirma as definições no **resumo** acontece de página do assistente, o seguinte:  

-   A configuração cria o script **%TEMP%\ConfigMgrAutoSave.ini**.  Pode mudar o nome este ficheiro antes, utilizá-lo, mas têm de reter a extensão de ficheiro. ini.  
-   O script de instalação automática contém as definições que selecionou no assistente.  
-   Após a criação do script, pode modificar o script para instalar outros sites na hierarquia.  
-   Em seguida, pode utilizar este script para efetuar uma configuração automática do Configuration Manager.  

Este ficheiro de script fornece as mesmas informações pedidas pelo Assistente de configuração de, exceto que não existem não existem predefinições.   
Tem de especificar todos os valores para as chaves de configuração que se aplicam ao tipo de instalação que está a utilizar.   

Quando a configuração cria o script de instalação automática, este é preenchido com o valor de chave de produto que introduziu durante a configuração. Isto pode ser uma chave de produto válida, ou **EVAL** ao instalar uma versão de avaliação do Configuration Manager. O valor da chave de produto no script está preenchido para que pode concluir a verificação de pré-requisitos.   

Quando a configuração iniciar a instalação do site real, o script criado automaticamente é novamente gravado para limpar o valor da chave de produto no script criado. Antes de utilizar o script para a instalação automática de um novo site, pode editar o script para fornecer uma chave de produto válida ou especificar uma instalação de avaliação do Configuration Manager.  

### <a name="section-names-key-names-and-values"></a>Nomes de secções, nomes de chaves e valores
O script contém nomes de secções, nomes de chaves e valores. Tenha em atenção as seguintes informações:
-   Nomes de chaves de secção necessários variam consoante o tipo de instalação que está a processar scripts.
-   A ordem das chaves dentro das secções e a ordem das secções no ficheiro não são importantes.     
-   As chaves não são maiúsculas e minúsculas.  
-   Quando está a fornecer valores para as chaves, o nome da chave deve ser seguido um sinal de igual (=) e o valor da chave.    

> [!TIP]  
>  Para ver o conjunto completo de opções, consulte o artigo [opções da linha de comandos para configuração e scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="use-the-script-setup-command-line-option"></a>Utilize a opção da linha de comandos /SCRIPT de configuração

-   Tem de utilizar um ficheiro de script de configuração e especificar o nome de ficheiro após a **/SCRIPT** opção da linha de comandos. Tenha em atenção as seguintes informações:   
    -   O nome do ficheiro tem de ter o **. ini** extensão de nome de ficheiro.  
    -   Quando referenciar o ficheiro de script de configuração na linha de comando, tem de fornecer o caminho completo para o ficheiro. Por exemplo, se o ficheiro de inicialização da configuração tiver o nome e é armazenado na pasta C:\Setup, a linha de comandos, escreva: **configuração/script c:\setup\setup.ini**.  

-   A conta que executa a configuração tem de ter **administrador** direitos no computador. Quando executar a configuração com o script automático, abra a janela de linha de comandos, utilizando o **executar como administrador** opção.   


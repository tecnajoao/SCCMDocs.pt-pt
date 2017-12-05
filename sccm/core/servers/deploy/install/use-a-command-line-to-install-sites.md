---
title: "Instalação da linha de comandos"
titleSuffix: Configuration Manager
description: "Saiba como executar o programa de configuração do System Center Configuration Manager numa linha de comandos para uma variedade de instalações de site."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
caps.latest.revision: "3"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 430fb636a3e40323d222376c6af210a4a17e470f
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="use-a-command-line-to-install-system-center-configuration-manager-sites"></a>Utilize uma linha de comandos para instalar sites do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Pode executar o programa de configuração do System Center Configuration Manager na linha de comandos para instalar uma variedade de tipos de site.

## <a name="supported-tasks-for-command-line-installations"></a>Tarefas suportadas para instalações da linha de comandos
 Este método de executar a configuração suporta a instalação de site seguinte e tarefas de manutenção do site:

-   **Instalar um site de administração central ou site primário numa linha de comandos**  
  Vista [opções da linha de comandos para configuração](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

-  **Modificar os idiomas em utilização num site de administração central ou site primário**  
    Para modificar os idiomas que estão instalados num site a partir de uma linha de comandos (incluindo idiomas para dispositivos móveis), tem de:  

     -   Execute a configuração de  **&lt;Caminhodeinstalaçãodoconfigmgr\>\Bin\X64** no servidor do site,
     -   Utilize o **/MANAGELANGS** opção da linha de comandos,
     -   Especificar um ficheiro de script de idioma que especifica os idiomas que pretende adicionar ou remover,  

    Por exemplo, utilize a seguinte sintaxe de comando: **setupwpf.exe /MANAGELANGS &lt;ficheiro de script de idioma\>**  

    Para criar o ficheiro de script de idioma, utilize as informações em [opções de linha de comandos para gerir idiomas](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)  

-  **Utilizar um ficheiro de script de instalação para instalações de site automáticas ou recuperação de sites**  
    Pode executar a configuração numa linha de comandos, utilizando um script de instalação e o utilizador executar uma instalação automática de site. Também pode utilizar esta opção para recuperar um site.    

    Para utilizar um script com a configuração:  

    -   Execute a configuração com a opção da linha de comandos **/SCRIPT** e especifique um ficheiro de script.  

    -   O ficheiro de script tem de ser configurado com chaves e valores necessários.  

    Para uma instalação autónoma de um site de administração central ou site primário, o ficheiro de script tem de ter as seguintes secções:  

    -   Identificação    
    -   Opções    
    -   SQLConfigOptions    
      -   HierarchyOptions    
    -   CloudConnectorOptions   

    Para recuperar um site, também tem de incluir as seguintes secções do ficheiro de script:  

    -   Identificação  
    -   Recuperação

Para obter mais informações, consulte [recuperação automática de site do Configuration Manager](/sccm/protect/understand/unattended-recovery).  

Para obter uma lista de chaves e valores a utilizar um ficheiro de script de instalação automática, consulte [chaves de ficheiro de script de configuração automática](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended).  

## <a name="about-the-command-line-script-file"></a>Sobre o ficheiro de script da linha de comandos  
 Para instalações automáticas do Configuration Manager, pode executar a configuração com a opção da linha de comandos **/SCRIPT**e especifique um ficheiro de script que contenha opções de instalação. As seguintes tarefas são suportadas através deste método:  

-   Instalar um site de administração central  
-   Instalar um site primário  
-   Instalar uma consola do configuration Manager  
-   Recuperar um site  

> [!NOTE]  
>  Não é possível utilizar o ficheiro de script automático para atualizar um site de avaliação para uma instalação licenciada do Configuration Manager.  

### <a name="the-cdlatest-key-name"></a>O nome da chave CDLatest
Quando utiliza suportes de dados de CD. Instalar pasta mais recente para executar um script das seguintes opções de quatro instalação, o script tem de incluir o **CDLatest** chave com um valor de **1**:
- Instalar um novo site de administração central
- Instalar um novo site primário
- Recuperar um site de administração central
- Recuperar um site primário

Este valor não é suportado para utilização com suporte de dados de instalação que que obtém a partir do site de licenciamento em Volume da Microsoft.
Consulte [opções da linha de comandos](/sccm/core/servers/deploy/install/command-line-options-for-setup) para obter informações sobre como utilizar este nome da chave no ficheiro de script.



### <a name="create-the-script"></a>Criar o script
O script de instalação é criado automaticamente quando é [executar a configuração para instalar um site utilizando a interface de utilizador](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  Quando confirmar as definições no **resumo** acontece de página do assistente, o seguinte:  

-   A configuração cria o script **%TEMP%\ConfigMgrAutoSave.ini**.  Pode mudar o nome deste ficheiro antes de a utilizar, mas tem de manter a extensão de ficheiro. ini.  
-   O script de instalação automática contém as definições que selecionou no assistente.  
-   Após a criação do script, pode modificar o script para instalar outros sites na hierarquia.  
-   Em seguida, pode utilizar este script para efetuar uma configuração automática do Configuration Manager.  

Este ficheiro de script fornece as mesmas informações que o Assistente de configuração solicita, exceto que existem não existem predefinições.   
Tem de especificar todos os valores para as chaves de configuração que se aplicam ao tipo de instalação que está a utilizar.   

Quando a configuração cria o script de instalação autónoma, este é preenchido com o valor de chave de produto que introduziu durante a configuração. Isto pode ser uma chave de produto válida ou **EVAL** ao instalar uma versão de avaliação do Configuration Manager. O valor de chave de produto no script está preenchido para que possa concluir a verificação de pré-requisitos.   

Quando a configuração iniciar a instalação do site real, o script criado automaticamente é novamente gravado para limpar o valor de chave de produto no script que cria. Antes de utilizar o script para uma instalação autónoma de um site novo, pode editar o script para fornecer uma chave de produto válida ou especificar uma instalação de avaliação do Configuration Manager.  

### <a name="section-names-key-names-and-values"></a>Nomes de secções, nomes de chaves e valores
O script contém nomes de secções, nomes de chaves e valores. Tenha em atenção as seguintes informações:
-   Os nomes de chaves de secção necessários variam consoante o tipo de instalação que está a processar scripts.
-   A ordem das chaves dentro das secções e a ordem das secções no ficheiro não são importantes.     
-   As chaves não são maiúsculas e minúsculas.  
-   Quando fornece valores para chaves, o nome da chave tem de ser seguido por um sinal de igual (=) e o valor da chave.    

> [!TIP]  
>  Para ver o conjunto completo de opções, consulte [opções da linha de comandos para configuração e scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="use-the-script-setup-command-line-option"></a>Utilize a opção da linha de comandos /SCRIPT de configuração

-   Tem de utilizar um ficheiro de script de configuração e especificar o nome de ficheiro após o **/SCRIPT** opção da linha de comandos. Tenha em atenção as seguintes informações:   
    -   O nome do ficheiro tem de ter o **. ini** extensão de nome de ficheiro.  
    -   Quando referenciar o ficheiro de script de configuração na linha de comandos, tem de fornecer o caminho completo para o ficheiro. Por exemplo, se o ficheiro de inicialização da configuração tiver o nome Setup.ini e estiver armazenado na pasta C:\Setup, na linha de comandos, escreva: **o programa de configuração/script c:\setup\setup.ini**.  

-   A conta que executa a configuração tem de ter **administrador** direitos no computador. Quando executar a configuração com o script automático, abra a janela de linha de comandos, utilizando o **executar como administrador** opção.   

---
title: "Instalação de linha de comando | Microsoft Docs"
description: "Saiba como executar a instalação do System Center Configuration Manager em um prompt de comando para uma variedade de instalações do site."
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
ms.sourcegitcommit: f7cd9c71287d62c9f5d36e2f032bc2a6065572ae
ms.openlocfilehash: 8ff48b08d1abb7481592c0ea076d4efa15c3d8ee
ms.contentlocale: pt-pt
ms.lasthandoff: 06/06/2017

---
# <a name="use-a-command-line-to-install-system-center-configuration-manager-sites"></a>Usar uma linha de comando para instalar sites do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

 Você pode executar a instalação do System Center Configuration Manager em um prompt de comando para instalar uma variedade de tipos de site.

## <a name="supported-tasks-for-command-line-installations"></a>Tarefas com suporte para instalações de linha de comando
 Esse método de instalação oferece suporte a tarefas de manutenção do site e após a instalação de site:

-   **Instalar um site de administração central ou site primário de um prompt de comando**  
  Exibição [opções de linha de comando para instalação](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

-  **Modificar os idiomas em uso em um site de administração central ou site primário**  
    Para modificar os idiomas que estão instalados em um site em um prompt de comando (incluindo idiomas para dispositivos móveis), você deve:  

     -   Execute a instalação do  **&lt;ConfigMgrInstallationPath\>\Bin\X64** no servidor do site,
     -   Use o **/MANAGELANGS** opção de linha de comando
     -   Especifique um arquivo de script de idioma que especifica os idiomas que você deseja adicionar ou remover  

    Por exemplo, use a seguinte sintaxe de comando: **setupwpf.exe /MANAGELANGS &lt;arquivo de script de idioma\>**  

    Para criar o arquivo de script de idioma, use as informações em [opções de linha de comando para gerenciar idiomas](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)  

-  **Usar um arquivo de script de instalação para instalações autônomas de site ou a recuperação de site**  
    Você pode executar a instalação em um prompt de comando usando um script de instalação e executar uma instalação autônoma do site. Você também pode usar essa opção para recuperar um site.    

    Para usar um script com a instalação:  

    -   Execute a instalação com a opção de linha de comando **/SCRIPT** e especifique um arquivo de script.  

    -   O arquivo de script deve ser configurado com os valores e chaves necessárias.  

    Para uma instalação autônoma de um site de administração central ou site primário, o arquivo de script deve ter as seguintes seções:  

    -   Identificação    
    -   Opções    
    -   SQLConfigOptions    
      -   HierarchyOptions    
    -   CloudConnectorOptions   

    Para recuperar um site, você também deve incluir as seguintes seções do arquivo de script:  

    -   Identificação  
    -   Recuperação

Para obter mais informações, consulte [recuperação autônoma do site do Configuration Manager](/sccm/protect/understand/unattended-recovery).  

Para obter uma lista de chaves e valores a serem usados em um arquivo de script de instalação autônoma, consulte [chaves de arquivo de script de instalação autônoma](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended).  

## <a name="about-the-command-line-script-file"></a>Sobre o arquivo de script de linha de comando  
 Para instalações autônomas do Configuration Manager, você pode executar a instalação com a opção de linha de comando **/SCRIPT**e especificar um arquivo de script que contém opções de instalação. As tarefas a seguir têm suporte usando esse método:  

-   Instalar um site de administração central  
-   Instalar um site primário  
-   Instalar um console do configuration Manager  
-   Recuperar um site  

> [!NOTE]  
>  Você não pode usar o arquivo de script autônomo para atualizar um site de avaliação para uma instalação licenciada do Configuration Manager.  

### <a name="the-cdlatest-key-name"></a>O nome da chave CDLatest
Quando você usa mídia a partir do CD. Instalar a pasta mais recente para executar um script das seguintes opções de instalação de quatro, o script deve incluir o **CDLatest** chave com um valor de **1**:
- Instalar um novo site de administração central
- Instalar um novo site primário
- Recuperar um site de administração central
- Recuperar um site primário

Esse valor não é suportado para uso com a mídia de instalação que você obtém do site de licença de Volume da Microsoft.
Consulte [opções de linha de comando](/sccm/core/servers/deploy/install/command-line-options-for-setup) para obter informações sobre como usar esse nome de chave no arquivo de script.



### <a name="create-the-script"></a>Criar o script
O script de instalação é automaticamente criado quando você [execute a instalação para instalar um site usando a interface do usuário](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  Quando você confirma as configurações no **resumo** página do assistente, o seguinte acontece:  

-   A instalação cria o script **%TEMP%\ConfigMgrAutoSave.ini**.  Você pode renomear esse arquivo antes de você usá-lo, mas ele deve manter a extensão de arquivo. ini.  
-   O script de instalação autônoma contém as configurações que você selecionou no assistente.  
-   Depois que o script é criado, você pode modificar o script para instalar outros sites na sua hierarquia.  
-   Você pode usar esse script para executar uma instalação autônoma do Configuration Manager.  

Esse arquivo de script fornece as mesmas informações que o Assistente de instalação solicita, exceto que não há nenhuma configuração padrão.   
Você deve especificar todos os valores para as chaves de instalação que se aplicam ao tipo de instalação que você está usando.   

Quando a instalação cria o script de instalação autônoma, ele é preenchido com o valor de chave de produto inserido durante a instalação. Isso pode ser uma chave de produto válida, ou **EVAL** quando você instala uma versão de avaliação do Configuration Manager. O valor de chave do produto no script é preenchido para que possa concluir a verificação de pré-requisitos.   

Quando a instalação inicia a instalação real do site, o script criado automaticamente é gravado para novamente limpar o valor de chave do produto no script que ele cria. Antes de usar o script para uma instalação autônoma de um novo site, você pode editar o script para fornecer uma chave de produto válida ou especificar uma instalação de avaliação do Configuration Manager.  

### <a name="section-names-key-names-and-values"></a>Os nomes de seção, nomes de chave e valores
O script contém nomes de secções, nomes de chaves e valores. Observe as seguintes informações:
-   Nomes de chave da seção necessários variam dependendo do tipo de instalação que você está criando scripts.
-   A ordem das chaves dentro das seções e a ordem das seções dentro do arquivo não é importantes.     
-   As chaves não diferenciam maiusculas de minúsculas.  
-   Quando você fornece valores para chaves, o nome da chave deve ser seguido por um sinal de igual (=) e o valor da chave.    

> [!TIP]  
>  Para exibir o conjunto completo de opções, consulte [opções de linha de comando para instalação e scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="use-the-script-setup-command-line-option"></a>Use a opção de linha de comando de instalação /SCRIPT

-   Você deve usar um arquivo de script de instalação e especifique o nome do arquivo após o **/SCRIPT** opção de linha de comando de instalação. Observe as seguintes informações:   
    -   O nome do arquivo deve ter o **. ini** extensão de nome de arquivo.  
    -   Quando você referenciar o arquivo de script de instalação no prompt de comando, você deve fornecer o caminho completo para o arquivo. Por exemplo, se o arquivo de inicialização de instalação for nomeado como Setup.ini e é armazenado na pasta C:\Setup, no prompt de comando, digite: **de instalação /script c:\setup\setup.ini**.  

-   A conta que executa a instalação deve ter **administrador** direitos no computador. Quando você executar a instalação com o script autônomo, abra a janela de Prompt de comando usando o **executar como administrador** opção.   


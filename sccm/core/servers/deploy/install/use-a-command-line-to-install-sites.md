---
title: Instalação da linha de comandos
titleSuffix: Configuration Manager
description: Saiba como executar a configuração do System Center Configuration Manager num prompt de comando para uma variedade de instalações de site.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 293517d3c01366e07507a56c1973069ae1e308af
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138998"
---
# <a name="use-a-command-line-to-install-system-center-configuration-manager-sites"></a>Utilize uma linha de comandos para instalar sites do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Pode executar a configuração do System Center Configuration Manager num prompt de comando para instalar uma variedade de tipos de site.

## <a name="supported-tasks-for-command-line-installations"></a>Tarefas suportadas para instalações da linha de comandos
 Este método de executar a configuração suporta a instalação do site seguinte e tarefas de manutenção do site:

- **Instalar um site de administração central ou site primário a partir de um prompt de comando**  
  Vista [opções da linha de comandos para configuração](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

- **Modificar os idiomas em utilização num site de administração central ou site primário**  
   Para modificar os idiomas que estão instalados num site a partir de um prompt de comando (incluindo idiomas para dispositivos móveis), tem de:  

  - Execute a configuração partir  **&lt;Caminhodeinstalaçãodoconfigmgr\>\Bin\X64** no servidor do site,
  - Utilize o **/MANAGELANGS** opção da linha de comandos,
  - Especificar um ficheiro de script de idioma que especifica os idiomas que pretende adicionar ou remover,  

    Por exemplo, utilize a seguinte sintaxe de comando: **setupwpf.exe /MANAGELANGS &lt;ficheiro de script de idioma\>**  

    Para criar o ficheiro de script de idioma, utilize as informações em [opções de linha de comandos para gerir idiomas](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)  

- **Utilizar um ficheiro de script de instalação para instalações de site automáticas ou recuperação de site**  
   Pode executar a configuração numa linha de comandos, utilizando um script de instalação e executar uma instalação automática de site. Também pode utilizar esta opção para recuperar um site.    

   Para utilizar um script com a configuração:  

  - Execute a configuração com a opção de linha de comandos **/script** e especifique um ficheiro de script.  

  - O ficheiro de script tem de ser configurado com chaves e valores necessários.  

    Para uma instalação automática de um site de administração central ou site primário, o ficheiro de script tem de ter as seguintes secções:  

  - Identificação    
  - Opções    
  - SQLConfigOptions    
    -   HierarchyOptions    
  - CloudConnectorOptions   

    Para recuperar um site, tem também de incluir as seguintes secções do ficheiro de script:  

  - Identificação  
  - Recuperação

Para obter mais informações, consulte [recuperação de site automática para o Configuration Manager](/sccm/protect/understand/unattended-recovery).  

Para obter uma lista de chaves e valores a utilizar num ficheiro de script de instalação automática, consulte [chaves de ficheiro de script de instalação autônoma](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended).  

## <a name="about-the-command-line-script-file"></a>Sobre o ficheiro de script de linha de comandos  
 Para instalações automáticas do Configuration Manager, pode executar a configuração com a opção da linha de comandos **/script**e especificar um ficheiro de script que contém as opções de instalação. Ao utilizar este método, são suportadas as seguintes tarefas:  

-   Instalar um site de administração central  
-   Instalar um site primário  
-   Instalar uma consola do configuration Manager  
-   Recuperar um site  

> [!NOTE]  
>  Não é possível utilizar o ficheiro de script automático para atualizar um site de avaliação para uma instalação licenciada do Configuration Manager.  

### <a name="the-cdlatest-key-name"></a>O nome da chave CDLatest
Quando utiliza multimédia a partir do CD. Pasta mais recente para executar um script instalar das seguintes opções de instalação de quatro, o script tem de incluir o **CDLatest** chave com um valor de **1**:
- Instalar um novo site de administração central
- Instalar um novo site primário
- Recuperar um site de administração central
- Recuperar um site primário

Este valor não é suportado para utilização com o suporte de dados de instalação que obtém a partir do site de licenciamento em Volume da Microsoft.
Ver [opções da linha de comandos](/sccm/core/servers/deploy/install/command-line-options-for-setup) para obter informações sobre como utilizar este nome da chave no ficheiro de script.



### <a name="create-the-script"></a>Criar o script
O script de instalação é criado automaticamente quando [execute a configuração para instalar um site utilizando a interface do usuário](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  Quando confirmar as definições na **resumo** acontece de página do assistente, o seguinte:  

-   Configuração cria o script **%TEMP%\ConfigMgrAutoSave.ini**.  Pode renomear esse arquivo antes de usá-lo, mas tem de manter a extensão de ficheiro. ini.  
-   O script de instalação automática contém as definições que selecionou no assistente.  
-   Depois de criar o script, pode modificar o script para instalar outros sites na sua hierarquia.  
-   Em seguida, pode utilizar este script para efetuar uma configuração automática do Configuration Manager.  

Este ficheiro de script fornece as mesmas informações que o Assistente de configuração solicita, mas existem não existem predefinições.   
Tem de especificar todos os valores para as chaves de configuração que se aplicam ao tipo de instalação que está a utilizar.   

Quando a instalação cria o script de instalação automática, ele é preenchido com o valor de chave de produto que introduziu durante a configuração. Isso pode ser uma chave de produto válida, ou **EVAL** ao instalar uma versão de avaliação do Configuration Manager. O valor de chave de produto no script é preenchido, de modo a que pode concluir a verificação de pré-requisitos.   

Quando a configuração iniciar a instalação do site real, o script criado automaticamente é novamente gravado para limpar o valor de chave de produto no script que cria. Antes de utilizar o script para uma instalação automática de um novo site, pode editar o script para fornecer uma chave de produto válida ou especificar uma instalação de avaliação do Configuration Manager.  

### <a name="section-names-key-names-and-values"></a>Nomes de secções, nomes de chaves e valores
O script contém nomes de secções, nomes de chaves e valores. Tenha em atenção as seguintes informações:
-   Nomes de chaves de secção necessários variam consoante o tipo de instalação que está a processar scripts.
-   A ordem das chaves nas secções e a ordem das secções no ficheiro não são importantes.     
-   As chaves não diferenciam maiúsculas de minúsculas.  
-   Quando fornece valores para chaves, o nome da chave tem seguido de um sinal de igual (=) e o valor da chave.    

> [!TIP]  
>  Para ver o conjunto completo de opções, consulte [opções da linha de comandos para configuração e scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="use-the-script-setup-command-line-option"></a>Utilize a opção de linha de comandos /SCRIPT de configuração

-   Tem de utilizar um ficheiro de script de configuração e especifique o nome de ficheiro depois do **/script** opção da linha de comandos de configuração. Tenha em atenção as seguintes informações:   
    -   O nome do ficheiro tem de ter o **. ini** extensão de nome de ficheiro.  
    -   Quando especifica o ficheiro de script de configuração no prompt de comando, tem de fornecer o caminho completo para o ficheiro. Por exemplo, se o ficheiro de inicialização do programa de configuração com o nome Setup. ini e é armazenado na pasta C:\Setup, na linha de comandos, escreva: **de configuração /script c:\setup\setup.ini**.  

-   A conta que executa a configuração tem de ter **administrador** direitos no computador. Quando executar a configuração com o script automático, abra a janela de linha de comandos, utilizando o **executar como administrador** opção.   

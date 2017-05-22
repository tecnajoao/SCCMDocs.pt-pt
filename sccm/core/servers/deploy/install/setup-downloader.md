---
title: "Dispositivo de transferência da configuração | Documentos do Microsoft"
description: "Saiba mais sobre esta aplicação autónoma concebida para assegurar que a instalação de site utiliza versões atuais dos ficheiros de instalação de chave."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 34e24deb90a39bf655a2e24d16cdbe07528e6193
ms.openlocfilehash: b72148ecc16141843178cbd220fe021fab8be992
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="setup-downloader-for-system-center-configuration-manager"></a>Dispositivo de transferência da configuração para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de executar a configuração para instalar ou atualizar um site do System Center Configuration Manager, pode utilizar a aplicação de autónomo do programa de configuração da versão do Configuration Manager que pretende instalar para transferir ficheiros de configuração atualizados.  

Utilização de ficheiros de configuração atualizados assegura que a instalação de site utiliza versões atuais dos ficheiros de instalação de chave. No oveview:   
-   Quando utiliza o dispositivo de transferência da configuração para transferir os ficheiros antes de iniciar a configuração, é especificar uma pasta que contém os ficheiros.  
-   A conta utilizada para executar o programa de configuração tem de ter **controlo total** permissões para a pasta de transferência.  
-   Quando executar a configuração para instalar ou atualizar um site, pode direcionar-o para utilizar esta cópia local dos ficheiros que anteriormente transferidos. Isto impede que o formulário de configuração ter de se ligar à Microsoft quando iniciar a instalação do site ou a atualização.  
-   Pode utilizar a mesma cópia local dos ficheiros de configuração para as instalações de site subsequentes ou atualizações.  

Os seguintes tipos de ficheiros são transferidos na íntegra pelo dispositivo de transferência da configuração:  
-   Ficheiros redistribuíveis dos pré-requisitos necessários  
-   Pacotes de idiomas  
-   As atualizações mais recentes do produto para a configuração  

Tem duas opções para executar o programa de configuração:
- Executar a aplicação com a interface de utilizador
- Para opções da linha de comandos, executadas a aplicação de uma linha de comandos


## <a name="run-setup-downloader-with-the-user-interface"></a>Execute o programa de configuração com a interface de utilizador  

1.  Num computador que tenha acesso à Internet, abra o Explorador do Windows e aceda ao  **&lt;ConfigMgrInstallationMedia\>\smssetup\bin\x64.**.  

2.  Para abrir o dispositivo de transferência da configuração, faça duplo clique **Setupdl.exe**.   

3. Especifique o caminho para a pasta que irá alojar os ficheiros de instalação atualizados e, em seguida, clique em **transferir**. Dispositivo de transferência da configuração verifica os ficheiros que estão atualmente na pasta de transferência. Transfere apenas os ficheiros que estão em falta ou que são mais recentes que ficheiros existentes. Dispositivo de transferência da configuração cria subpastas para idiomas transferidos e outras subpastas necessárias.  

4.  Para rever os resultados da transferência, abra o **configmgrsetup. log** ficheiro no diretório de raiz da unidade C.  .  

## <a name="run-setup-downloader-from-a-command-prompt"></a>Executar o programa de configuração a partir de uma linha de comandos  

1.  Na janela de linha de comandos, vá a  **&lt;* suporte de instalação do Configuration Manager*\>\SMSSETUP\BIN\X64**.   

2.  Para abrir o dispositivo de transferência da configuração, execute **Setupdl.exe**.

    Pode utilizar as seguintes opções da linha de comandos com **Setupdl.exe**:   

    -   **/ VERIFICAR**: Utilize esta opção para verificar os ficheiros na pasta de transferência, que inclui os ficheiros de idioma. Reveja o ficheiro configmgrsetup. log no diretório de raiz da unidade C para obter uma lista de ficheiros que estão desatualizados. Não são transferidos ficheiros quando utilizar esta opção.  

    -   **/ VERIFYLANG**: Utilize esta opção para verificar os ficheiros de idioma na pasta de transferência. Reveja o ficheiro configmgrsetup. log no diretório de raiz da unidade C para obter uma lista de ficheiros de idioma que estão desatualizados.

    -   **/LANG**: Utilize esta opção para transferir apenas os ficheiros de idioma para a pasta de transferência.  

    -   **/NOUI**: Utilize esta opção para iniciar o dispositivo de transferência da configuração sem apresentar a interface de utilizador. Quando utilizar esta opção, tem de especificar o **transferir caminho** como parte do comando na linha de comando.  

    -   **&lt;DownloadPath\>**: Pode especificar o caminho para a pasta de transferência para iniciar automaticamente a verificação ou processo de transferência. Tem de especificar o caminho de transferência quando utilizar o **/noui.** opção. Se não especificar um caminho de transferência, tem de especificar o caminho quando o dispositivo de transferência da configuração é apresentada. Dispositivo de transferência da configuração cria a pasta se não existir.  

    Comandos de exemplo:

    -   **setupd &lt;DownloadPath\>**  

        -   Dispositivo de transferência da configuração é iniciado, verifica os ficheiros na pasta de transferência e, em seguida, transfere apenas os ficheiros que estão em falta ou que tenham versões mais recentes que ficheiros existentes.     

    -   **setupdl /VERIFY &lt;DownloadPath\>**  

        -   Dispositivo de transferência da configuração é iniciado e verifica os ficheiros na pasta de transferência especificado.  

    -   **setupdl /noui. &lt;DownloadPath\>**  

        -   Dispositivo de transferência da configuração é iniciado, verifica os ficheiros na pasta de transferência e, em seguida, transfere apenas os ficheiros que estão em falta ou que são mais recentes do que os ficheiros existentes.  

    -   **setupdl /LANG &lt;DownloadPath\>**  

        -   Dispositivo de transferência da configuração é iniciado, verifica os ficheiros de idioma na pasta de transferência e, em seguida, transfere apenas os ficheiros de idioma que estão em falta ou que são mais recentes do que os ficheiros existentes.  

    -   **setupdl /VERIFY**  

        -   Configuração é iniciado de dispositivo de transferência e, em seguida, tem de especificar o caminho para a pasta de transferência. Em seguida, depois de clicar em **verificar**, dispositivo de transferência da configuração verifica os ficheiros na pasta de transferência.  

3.  Para rever os resultados da transferência, abra o **configmgrsetup. log** ficheiro no diretório de raiz da unidade C.


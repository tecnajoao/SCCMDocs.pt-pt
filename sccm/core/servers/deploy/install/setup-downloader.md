---
title: Dispositivo de transferência da configuração
titleSuffix: Configuration Manager
description: Saiba mais sobre esta aplicação autónoma concebida para garantir que a instalação do site utiliza as versões atuais dos ficheiros de instalação de chave.
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: abfad38e0c02ff6c0af8d4c9c47bdeed7598e513
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129753"
---
# <a name="setup-downloader-for-system-center-configuration-manager"></a>Dispositivo de transferência da configuração do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de executar a configuração para instalar ou atualizar um site do System Center Configuration Manager, pode utilizar a aplicação autónoma do programa de configuração da versão do Configuration Manager que pretende instalar para transferir ficheiros de configuração atualizados.  

Utilizar ficheiros de configuração atualizados garante que a instalação do site usa as versões atuais dos ficheiros de instalação de chave. No oveview:   
-   Quando utilizar o dispositivo de transferência da configuração para transferir ficheiros antes de iniciar a configuração, especifique uma pasta que contém os ficheiros.  
-   A conta que utiliza para executar o programa de configuração tem de ter **controlo total** permissões para a pasta de transferência.  
-   Quando executar a configuração para instalar ou atualizar um site, pode direcionar o mesmo para utilizar esta cópia local dos ficheiros que transferiu anteriormente. Isto impede que o formulário de configuração ter de se ligar à Microsoft ao iniciar a instalação do site ou a atualização.  
-   Pode utilizar a mesma cópia local dos ficheiros de configuração para o site subsequentes instalações ou atualizações.  

Os seguintes tipos de ficheiros são transferidos pelo dispositivo de transferência da configuração:  
-   Ficheiros redistribuíveis de pré-requisitos necessários  
-   Pacotes de idiomas  
-   As atualizações mais recentes do produto para a configuração  

Tem duas opções para executar o programa de configuração:
- Executar a aplicação com a interface do usuário
- Para obter opções da linha de comandos, executadas o aplicativo num prompt de comando


## <a name="run-setup-downloader-with-the-user-interface"></a>Executar o programa de configuração com a interface do usuário  

1.  Num computador com acesso à Internet, abra o Explorador do Windows e aceda a  **&lt;Suportededadosdeinstalaçãodoconfigmgr\>\SMSSETUP\BIN\X64**.  

2.  Para abrir o dispositivo de transferência da configuração, faça duplo clique em **Setupdl.exe**.   

3. Especifique o caminho para a pasta que irá alojar os ficheiros de instalação atualizados e, em seguida, clique em **transferir**. Dispositivo de transferência da configuração verifica os ficheiros que estão atualmente na pasta de transferência. Transfere apenas os ficheiros que estão em falta ou que são mais recentes do que os arquivos existentes. Dispositivo de transferência da configuração cria subpastas para idiomas transferidos e outras subpastas necessárias.  

4.  Para rever os resultados da transferência, abra a **configmgrsetup. log** ficheiro no diretório de raiz da unidade C.  .  

## <a name="run-setup-downloader-from-a-command-prompt"></a>Executar o programa de configuração numa linha de comandos  

1.  Na janela de comandos, aceda a  **&lt; *mídia de instalação do Configuration Manager*\>\SMSSETUP\BIN\X64**.   

2.  Para abrir o dispositivo de transferência da configuração, execute **Setupdl.exe**.

    Pode utilizar as seguintes opções da linha de comandos com **Setupdl.exe**:   

    -   **/VERIFY**: Utilize esta opção para verificar os ficheiros na pasta de transferência, que incluem ficheiros de idioma. Reveja o ficheiro configmgrsetup. log no diretório de raiz da unidade C para obter uma lista de ficheiros que estão desatualizados. Não são transferidos ficheiros quando utilizar esta opção.  

    -   **/VERIFYLANG**: Utilize esta opção para verificar os ficheiros de idioma na pasta de transferência. Reveja o ficheiro configmgrsetup. log no diretório de raiz da unidade C para obter uma lista de ficheiros de idioma que estão desatualizados.

    -   **/LANG**: Utilize esta opção para transferir apenas os ficheiros de idioma para a pasta de transferência.  

    -   **/NOUI**: Utilize esta opção para iniciar o dispositivo de transferência da configuração sem apresentar a interface do usuário. Quando utilizar esta opção, tem de especificar o **caminho de transferência** como parte do comando no prompt de comando.  

    -   **&lt;DownloadPath\>**: Pode especificar o caminho para a pasta de transferência para iniciar automaticamente a verificação ou processo de transferência. Tem de especificar o caminho de transferência quando utilizar o **/NOUI** opção. Se não especificar um caminho de transferência, tem de especificar o caminho quando o dispositivo de transferência da configuração abre. Dispositivo de transferência da configuração cria a pasta se não existir.  

    Comandos de exemplo:

    -   **setupdl &lt;DownloadPath\>**  

        -   Dispositivo de transferência da configuração é iniciado, verifica os ficheiros na pasta de transferência especificada e transfere apenas os ficheiros que estão em falta ou que tenham versões mais recentes que existentes.     

    -   **setupdl /VERIFY &lt;DownloadPath\>**  

        -   Dispositivo de transferência da configuração é iniciado e verifica os ficheiros na pasta de transferência.  

    -   **setupdl /NOUI &lt;DownloadPath\>**  

        -   Dispositivo de transferência da configuração é iniciado, verifica os ficheiros na pasta de transferência especificada e transfere apenas os ficheiros que estão em falta ou que são mais recentes do que os existentes.  

    -   **setupdl /LANG &lt;Caminhodatransferência\>**  

        -   Dispositivo de transferência da configuração é iniciado, verifica os ficheiros de idioma na pasta de transferência especificada e transfere apenas os ficheiros de idioma que estão em falta ou que são mais recentes do que os existentes.  

    -   **setupdl /VERIFY**  

        -   Configuração é iniciado de transferência e, em seguida, tem de especificar o caminho para a pasta de transferência. Em seguida, depois de clicar em **Verifique se**, dispositivo de transferência da configuração verifica os ficheiros na pasta de transferência.  

3.  Para rever os resultados da transferência, abra a **configmgrsetup. log** ficheiro no diretório de raiz da unidade C.

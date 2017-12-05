---
title: "Dispositivo de transferência da configuração"
titleSuffix: Configuration Manager
description: "Leia sobre esta aplicação autónoma concebida para garantir que a instalação de site utiliza as versões atuais dos ficheiros de instalação chave."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
caps.latest.revision: "3"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: dec591ac845b6c54421197099e56d7a4a86783ae
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="setup-downloader-for-system-center-configuration-manager"></a>Dispositivo de transferência da configuração do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de executar a configuração para instalar ou atualizar um site do System Center Configuration Manager, pode utilizar a aplicação autónoma do programa de configuração da versão do Configuration Manager que pretende instalar para transferir ficheiros de configuração atualizados.  

Utilizar ficheiros de configuração atualizados garante que a instalação de site utiliza as versões atuais dos ficheiros de instalação chave. No oveview:   
-   Quando utilizar o dispositivo de transferência da configuração para transferir ficheiros antes de iniciar a configuração, especifique uma pasta que contém os ficheiros.  
-   A conta utilizada para executar o programa de configuração tem de ter **controlo total** permissões para a pasta de transferência.  
-   Quando executar a configuração para instalar ou atualizar um site, pode direcionar o mesmo para utilizar esta cópia local dos ficheiros que transferiu anteriormente. Isto impede que o formulário da configuração terem de se ligar à Microsoft quando iniciar a instalação do site ou a atualização.  
-   Pode utilizar a mesma cópia local dos ficheiros de configuração para o site subsequentes instalações ou atualizações.  

Os seguintes tipos de ficheiros são transferidos pelo dispositivo de transferência da configuração:  
-   Ficheiros redistribuíveis dos pré-requisitos necessários  
-   Pacotes de idiomas  
-   As atualizações mais recentes do produto para a configuração  

Tem duas opções para executar o programa de configuração:
- Executar a aplicação com a interface de utilizador
- Para obter opções da linha de comandos, executadas a aplicação numa linha de comandos


## <a name="run-setup-downloader-with-the-user-interface"></a>Execute o programa de configuração com a interface de utilizador  

1.  Num computador que tenha acesso à Internet, abra o Explorador do Windows e aceda a  **&lt;Suportededadosdeinstalaçãodoconfigmgr\>\SMSSETUP\BIN\X64**.  

2.  Para abrir o dispositivo de transferência da configuração, faça duplo clique **Setupdl.exe**.   

3. Especifique o caminho para a pasta que irá alojar os ficheiros de instalação atualizados e, em seguida, clique em **transferir**. Dispositivo de transferência da configuração verifica os ficheiros que estão atualmente na pasta de transferência. Transfere apenas os ficheiros que estão em falta ou que são mais recentes do que os ficheiros existentes. Dispositivo de transferência da configuração cria subpastas para idiomas transferidos e outras subpastas necessárias.  

4.  Para rever os resultados da transferência, abra o **ConfigMgrSetup.log** ficheiro no diretório de raiz da unidade C.  .  

## <a name="run-setup-downloader-from-a-command-prompt"></a>Executar o programa de configuração numa linha de comandos  

1.  Na janela de linha de comandos, vá para  **&lt;* suporte de instalação do Configuration Manager*\>\SMSSETUP\BIN\X64**.   

2.  Para abrir o dispositivo de transferência da configuração, execute **Setupdl.exe**.

    Pode utilizar as seguintes opções da linha de comandos com **Setupdl.exe**:   

    -   **/ VERIFICAR**: Utilize esta opção para verificar os ficheiros na pasta de transferência, que incluem ficheiros de idioma. Reveja o ficheiro do ficheiro configmgrsetup.log, localizado no diretório de raiz da unidade C para obter uma lista de ficheiros que estão desatualizados. Não são transferidos ficheiros quando utiliza esta opção.  

    -   **/ VERIFYLANG**: Utilize esta opção para verificar os ficheiros de idioma na pasta de transferência. Reveja o ficheiro do ficheiro configmgrsetup.log, localizado no diretório de raiz da unidade C para obter uma lista de ficheiros de idioma que estão desatualizados.

    -   **/ LANG**: Utilize esta opção para transferir os ficheiros de idioma para a pasta de transferência.  

    -   **/SEMIU**: Utilize esta opção para iniciar o dispositivo de transferência da configuração sem apresentar a interface de utilizador. Quando utilizar esta opção, tem de especificar o **caminho de transferência** como parte do comando na linha de comandos.  

    -   **&lt;Caminhodatransferência\>**: Pode especificar o caminho para a pasta de transferência para iniciar automaticamente a verificação ou processo de transferência. Tem de especificar o caminho de transferência quando utilizar o **/NOUI** opção. Se não especificar um caminho de transferência, tem de especificar o caminho quando o dispositivo de transferência da configuração abre. Dispositivo de transferência da configuração cria uma pasta, se não existir.  

    Comandos de exemplo:

    -   **setupd &lt;Caminhodatransferência\>**  

        -   Dispositivo de transferência da configuração é iniciado, verifica os ficheiros na pasta de transferência especificada e, em seguida, transfere apenas os ficheiros que estão em falta ou que tenham versões mais recentes de ficheiros existentes.     

    -   **setupdl /VERIFY &lt;Caminhodatransferência\>**  

        -   Dispositivo de transferência da configuração é iniciado e verifica os ficheiros na pasta de transferência especificada.  

    -   **setupdl /NOUI &lt;Caminhodatransferência\>**  

        -   Dispositivo de transferência da configuração é iniciado, verifica os ficheiros na pasta de transferência especificada e, em seguida, transfere apenas os ficheiros que estão em falta ou que são mais recentes do que os ficheiros existentes.  

    -   **setupdl /LANG &lt;Caminhodatransferência\>**  

        -   Dispositivo de transferência da configuração é iniciado, verifica os ficheiros de idioma na pasta de transferência especificada e, em seguida, transfere apenas os ficheiros de idioma que estão em falta ou que são mais recentes do que os ficheiros existentes.  

    -   **setupdl /VERIFY**  

        -   Configuração é iniciado de dispositivo de transferência e, em seguida, tem de especificar o caminho para a pasta de transferência. Em seguida, depois de clicar em **verifique**, o dispositivo de transferência da configuração verifica os ficheiros na pasta de transferência.  

3.  Para rever os resultados da transferência, abra o **ConfigMgrSetup.log** ficheiro no diretório de raiz da unidade C.

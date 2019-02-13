---
title: Atualizar os clientes de Linux e UNIX
titleSuffix: Configuration Manager
description: Atualize um cliente num servidor Linux ou UNIX no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c71d58b247620be08dfbd1244deda5e513890376
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141583"
---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Como atualizar clientes para servidores Linux e UNIX no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode atualizar a versão do cliente para Linux e UNIX num computador para uma versão mais recente do cliente, sem desinstalar previamente o cliente atual. Para fazer isso, instale o novo pacote de instalação de cliente no computador, ao utilizar o **- keepdb** propriedade da linha de comandos. Quando o cliente para Linux e UNIX é instalado, substitui dados existentes do cliente pelos novos ficheiros do cliente. No entanto, o **- keepdb** propriedade da linha de comandos direciona o processo de instalação para reter o identificador exclusivo clientes (GUID), base de dados local das informações e o arquivo de certificados. Esta informação é seguidamente utilizada pela nova instalação do cliente.  

 Por exemplo, tem um computador RHEL5 x64 que executa o cliente a partir da versão original do cliente do Configuration Manager para Linux e UNIX. Para atualizar este cliente para a versão de cliente da atualização cumulativa 1, execute manualmente o **instale** script para instalar o pacote de cliente aplicável a partir da atualização cumulativa 1, com a adição do **- keepdb**comutador da linha de comandos. Consulte a seguinte linha de comandos de exemplo:  

`./install -mp <hostname\> -sitecode <code\> -keepdb ccm-Universal-x64.<build\>.tar`  



## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Como utilizar uma Implementação de Software para Atualizar o Cliente em Servidores Linux e UNIX  
 Pode utilizar uma implementação de software para atualizar o cliente do UNIX para uma nova versão do cliente. No entanto, o cliente do Configuration Manager não é possível executar diretamente o script de instalação para instalar o cliente novo porque a instalação de um novo cliente primeiro tem de desinstalar o cliente atual. Esta ação terminaria o processo de cliente do Configuration Manager que executa o script de instalação, antes de inicia a instalação do cliente novo. Para utilizar com êxito uma implementação de software para instalar o novo cliente, tem de agendar a instalação para iniciar num momento futuro e para ser executado pelo capacidades de agendamento incorporadas do sistema operacional.  

 Utilize uma implementação de software para o primeiro de copiar os ficheiros para o novo pacote de instalação de cliente para o computador cliente. Em seguida, implementar e executar um script para agendar o processo de instalação do cliente. O script usa incorporada do sistema operacional **em** comando para atrasar o início. Quando o script é executado, sua operação é gerida pelo sistema operativo cliente e não o cliente de Configuration Manager no computador. Este comportamento permite que a linha de comandos chamada pelo script desinstale primeiro o cliente do Configuration Manager e, em seguida, instalar o cliente novo. Estas ações concluir o processo de atualização de cliente no computador Linux ou UNIX. Depois de concluída a atualização, o cliente atualizado permanecerá gerido pelo Configuration Manager.  

 Utilize o procedimento seguinte para o ajudar a configurar uma implementação de software para atualizar o cliente para Linux e UNIX. Os seguintes passos e exemplos atualizam um computador RHEL5 x64 que executa a versão inicial do cliente para a versão de cliente da atualização cumulativa 1.  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Para utilizar uma implementação de software para atualizar o cliente em servidores Linux e UNIX  

1. Copie o novo pacote de instalação de cliente para o computador que executa o cliente do Configuration Manager para atualizar.  

    Por exemplo, colocar o pacote de instalação de cliente e instalar o script da atualização cumulativa 1 na seguinte localização no computador cliente: **/tmp/patch**  

2. Crie um script para gerir a atualização do cliente do Configuration Manager. Em seguida, coloque uma cópia do script na mesma pasta no computador cliente que os ficheiros de instalação de cliente do passo 1.  

    O script não requer um nome específico. Tem de conter linhas de comandos suficientes para utilizar os ficheiros de instalação de cliente de uma pasta local no computador cliente e para instalar o pacote de instalação do cliente, utilizando o **- keepdb** propriedade da linha de comandos. Utilizar o **- keepdb** propriedade da linha de comandos para manter o identificador exclusivo do cliente atual para utilização pelo cliente novo que está a instalar.  

    Por exemplo, criar um script chamado **upgrade.sh** que contém as seguintes linhas:  

   ```  
   #!/bin/sh  
   #  
   /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

   ```  

    Em seguida, copie-o para o **/tmp/patch** pasta no computador cliente.

3. Utilize a implementação de software para que cada cliente utilize o comando **at** incorporado nos computadores para executar o script **upgrade.sh** com um pequeno atraso antes de executar o script.  

    Por exemplo, utilize a seguinte linha de comando para executar o script: **em -f /tmp/upgrade.sh – m agora + 5 minutos**  

   Depois de o cliente agendar com êxito a execução do script **upgrade.sh** , o cliente envia uma mensagem de estado que indica que a implementação de software foi concluída com êxito. No entanto, a instalação atual do cliente é então gerida pelo computador, depois do atraso. Depois de concluída a atualização do cliente, valide a instalação ao rever o ficheiro **/var/opt/microsoft/scxcm.log** no computador cliente. Confirmar a instalação do cliente e ao comunicar com o site ao ver os detalhes do cliente no **dispositivos** nó da **ativos e compatibilidade** área de trabalho na consola do Configuration Manager.  

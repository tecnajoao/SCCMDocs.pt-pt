---
title: 'Atualizar clientes macOS '
titleSuffix: Configuration Manager
description: Atualize clientes em computadores Mac no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fb0ef52bc3359e1b31b2e2237a87e58bf671bcb7
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/19/2018
ms.locfileid: "36260841"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-system-center-configuration-manager"></a>Como atualizar clientes em computadores Mac no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Siga os passos de alto nível descritos abaixo para atualizar o cliente para computadores Mac utilizando uma aplicação do System Center Configuration Manager. Em alternativa, pode transferir os ficheiros de instalação do cliente Mac, copiá-los para uma localização de rede partilhada ou uma pasta local do computador Mac e, em seguida, instruir os utilizadores para executarem manualmente a instalação.  

> [!NOTE]  
>  Antes de executar estes passos, certifique-se de que o computador Mac cumpre os pré-requisitos. Consulte [sistemas operativos suportados para computadores Mac](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

## <a name="step-1-download-the-latest-mac-client-installation-file-from-the-microsoft-download-center"></a>Passo 1: Transferir o ficheiro de instalação de cliente Mac mais recente do Microsoft Download Center  
 O cliente de Mac para o Configuration Manager não é fornecido no suporte de instalação do Configuration Manager e tem de ser transferido do Microsoft Download Center. Os ficheiros de instalação do cliente Mac estão contidos num ficheiro Windows Installer com o nome ConfigmgrMacClient.msi.  

 Pode transferir este ficheiro a partir do [Centro de Transferências da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=525184).  

## <a name="step-2-run-the-downloaded-installation-file-to-create-the-mac-client-installation-file"></a>Passo 2: Execute o ficheiro de instalação transferido para criar o ficheiro de instalação de cliente Mac  
 Num computador com o Windows, execute o **ConfigmgrMacClient.msi** transferido para descompactar o ficheiro de instalação do cliente Mac, com o nome **Macclient.dmg**. Por predefinição, este ficheiro pode ser localizado na pasta **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client** do computador com Windows após a descompactação dos ficheiros.  

## <a name="step-3-extract-the-client-installation-files"></a>Passo 3: Extraia os ficheiros de instalação de cliente  
 Copie o ficheiro de Macclient.dmg numa partilha de rede ou numa pasta local de um computador Mac. Em seguida, no computador Mac, monte e abra o ficheiro Macclient.dmg e copie os ficheiros numa pasta do computador Mac.  

## <a name="step-4-create-a-cmmac-file-that-can-be-used-to-create-an-application"></a>Passo 4: Criar um ficheiro. cmmac que pode ser utilizado para criar uma aplicação  

1.  Utilize a ferramenta **CMAppUtil** (localizada na pasta **Ferramentas** dos ficheiros de instalação do cliente Mac) para criar um ficheiro .cmmac a partir do pacote de instalação do cliente. Este ficheiro será utilizado para criar a aplicação do Configuration Manager.  

2.  Copie o novo ficheiro **Cmclient.pkg** ficheiro para uma localização que esteja disponível no computador que está a executar a consola do Configuration Manager.  

 Para obter mais informações, consulte o [procedimentos suplementares para criar e implementar aplicações para computadores Mac](/sccm/apps/get-started/creating-mac-computer-applications#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers).  

## <a name="step-5-create-and-deploy-an-application-containing-the-mac-client-files"></a>**Passo 5:** Criar e implementar uma aplicação que contém os ficheiros de cliente Mac  

1.  Na consola do Configuration Manager, crie uma aplicação a **Cmclient.pkg** ficheiro que contém os ficheiros de instalação de cliente.  

2.  Implemente esta aplicação nos computadores Mac da sua hierarquia.  

 Para obter mais informações, consulte [aplicações para computadores Mac criar com o System Center Configuration Manager](../../../../apps/get-started/creating-mac-computer-applications.md).  

## <a name="step-6-users-install-the-latest-client"></a>Passo 6: Os utilizadores instalam o cliente mais recente  
 Serão solicitados aos utilizadores dos clientes Mac se uma atualização do cliente do Configuration Manager está disponível e tem de estar instalada. Depois de instalarem o cliente, os utilizadores têm de reiniciar o computador Mac.  

 Depois de reiniciar o computador, o Assistente de Inscrição do Computador é executado automaticamente para solicitar um novo certificado de utilizador. O Assistente de inscrição de computador será executado automaticamente apenas no momento da instalação do cliente SCCM primeiro. E não será possível executar novamente se tentar atualizar o cliente com um instalador de novo mais tarde, uma vez que já tem um certificado de utilizador válido. 

 Se não utilizar a inscrição do Gestor de configuração, mas instalar o certificado de cliente independentemente do Configuration Manager, consulte [configurar o cliente atualizado para utilizar um certificado existente](#BKMK_UpgradingClient_MachineEnrollment).  

##  <a name="BKMK_UpgradingClient_MachineEnrollment"></a> Configure the upgraded client to use an existing certificate  
 Efetue o seguinte procedimento para evitar a execução do Assistente de Inscrição do Computador e para configurar o cliente atualizado para utilizar um certificado de cliente existente.  

-   Na consola do Configuration Manager, crie um item de configuração do tipo **Mac OS X**.  

-   Adicione uma definição a este item de configuração com o tipo de definição **Script**.  

-   Adicione o script seguinte à definição:  

    ```  
    #!/bin/sh  
    echo "Starting script\n"  
    echo "Changing directory to MAC Client\n"  
    cd /Users/Administrator/Desktop/'MAC Client'/  
    echo "Import root cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
    echo "Using openssl to convert pfx to a crt\n"  
    /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
    echo "Adding trust to root cert\n"  
    /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
    echo "Import client cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
    echo "Executing ccmclient with MP\n"  
    sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
    echo "Editing Plist file\n"  
    sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
    echo "Changing directory to CCM\n"  
    cd /Library/'Application Support'/Microsoft/CCM/  
    echo "Making connection to the server\n"  
    sudo open ./CCMClient  
    echo "Ending Script\n"  
    exit  

    ```  

-   Adicione o item de configuração para uma linha de base de configuração e, em seguida, implementar a linha de base de configuração para todos os computadores Mac que instalam um certificado independentemente do Configuration Manager.  

 Para obter mais informações sobre como criar e implementar itens de configuração para computadores Mac, consulte [como criar itens de configuração para dispositivos Mac OS X geridos com o cliente do System Center Configuration Manager](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) e [como implementar linhas de base de configuração no System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md).  

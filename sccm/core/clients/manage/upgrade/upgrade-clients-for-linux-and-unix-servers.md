---
itle: 'Upgrade clients | Microsoft Docs | Linux UNIX '
description: Atualize um cliente num servidor Linux ou UNIX no System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: 394ba7c236c05cc90a3d7f99eb6146b15d620f11
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Como atualizar clientes para servidores Linux e UNIX no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode atualizar a versão do cliente para Linux e UNIX num computador para uma versão mais recente do cliente, sem desinstalar previamente o cliente atual. Para o fazer, instale o novo pacote de instalação de cliente no computador, ao utilizar a propriedade **-keepdb** da linha de comandos. Quando o cliente para Linux e UNIX é instalado, substitui dados existentes do cliente pelos novos ficheiros do cliente. No entanto, o **- keepdb** propriedade de linha de comandos direciona o processo de instalação para manter o clientes Identificador exclusivo (GUID), base de dados local das informações e arquivo de certificados. Esta informação é seguidamente utilizada pela nova instalação do cliente.  

 Por exemplo, tem um computador RHEL5 x64 que executa o cliente a partir da versão original do cliente do Configuration Manager para Linux e UNIX. Para atualizar este cliente para a versão do cliente a partir da atualização cumulativa 1, executar manualmente o **instalar** script para instalar o pacote de cliente aplicáveis a partir da atualização cumulativa 1, com a adição do **- keepdb** comutador de linha de comandos. A linha de comandos que utiliza é semelhante ao seguinte: **. / Instalar pacote de gestão - < nome de anfitrião\> - sitecode < código\> - keepdb ccm-Universal-x64. < construir\>.tar**  

## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Como utilizar uma Implementação de Software para Atualizar o Cliente em Servidores Linux e UNIX  
 Pode utilizar uma implementação de software para atualizar o cliente do UNIX para uma nova versão do cliente. No entanto, o cliente do System Center Configuration Manager diretamente não é possível executar o script de instalação para instalar o cliente novo porque a instalação de um novo cliente primeiro tem de desinstalar o cliente atual. Isto iria terminar o processo de cliente de Configuration Manager que executa o script de instalação antes de começa a instalação do cliente novo. Para utilizar com êxito uma implementação de software para instalar o cliente novo, tem de agendar a instalação para iniciar um momento futuro e para ser executado por capacidades de agendamento incorporadas do sistema operativo.  

 Para tal, utilize uma implementação de software para, primeiro, copiar os ficheiros para o novo pacote de instalação do cliente para o computador cliente e, em seguida, implementar e executar um script para agendar o processo de instalação do cliente. O script utiliza incorporados do sistema operativo **em** comando para atrasar o início. Em seguida, quando o script é executado, a conclusão da operação é gerido pelo sistema operativo cliente e não o cliente do Configuration Manager no computador. Isto permite que a linha de comandos chamada pelo script para o primeiro de desinstalar o cliente do Configuration Manager e, em seguida, instalar o cliente novo, concluir o processo de atualização do cliente no computador Linux ou UNIX. Após a conclusão da atualização, o cliente atualizado permanecerá gerido pelo Configuration Manager.  

 Utilize o procedimento seguinte para o ajudar a configurar uma implementação de software para atualizar o cliente para Linux e UNIX. Os seguintes passos e exemplos atualizam um computador RHEL5 x64 que executa a versão inicial do cliente para a versão de cliente da atualização cumulativa 1.  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Para utilizar uma implementação de software para atualizar o cliente em servidores Linux e UNIX  

1.  Copie o novo ficheiro de pacote de instalação de cliente para o computador que executa o cliente do Configuration Manager que pretende atualizar.  

     Por exemplo, poderá colocar o pacote de instalação de cliente e instalar o script da atualização cumulativa 1 na seguinte localização do computador cliente: **/tmp/PATCH**  

2.  Criar um script para gerir a atualização do cliente do Configuration Manager e, em seguida, coloque uma cópia do script na mesma pasta no computador cliente que os ficheiros de instalação de cliente a partir do passo 1.  

     O script não necessita de um nome específico, mas tem de conter as linhas de comandos suficientes para utilizar os ficheiros de instalação de cliente a partir de uma pasta local no computador cliente e para instalar o pacote de instalação de cliente utilizando o **- keepdb** propriedade de linha de comandos. Utilizar o **- keepdb** propriedade de linha de comandos para manter o identificador exclusivo do cliente atual para utilização pelo cliente novo que está a instalar.  

     Por exemplo, crie um script com o nome **upgrade.sh** que contenha as linhas seguintes e, em seguida, copie-o para a pasta **/tmp/PATCH** no computador cliente:  

    ```  
    #!/bin/sh  
    #  
    /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

    ```  

3.  Utilize a implementação de software para que cada cliente utilize o comando **at** incorporado nos computadores para executar o script **upgrade.sh** com um pequeno atraso antes de executar o script.  

     Por exemplo, utilize a seguinte linha de comandos para executar o script: **em -f /tmp/upgrade.sh -m agora + 5 minutos**  

 Depois de o cliente agendar com êxito a execução do script **upgrade.sh** , o cliente envia uma mensagem de estado que indica que a implementação de software foi concluída com êxito. No entanto, a instalação atual do cliente é então gerida pelo computador, depois do atraso. Depois de concluída a atualização do cliente, valide a instalação ao rever o ficheiro **/var/opt/microsoft/scxcm.log** no computador cliente. Além disso, pode confirmar que o cliente é instalado e a comunicar com o site através da visualização dos detalhes do cliente no **dispositivos** nó do **ativos e compatibilidade** área de trabalho na consola do Configuration Manager.  


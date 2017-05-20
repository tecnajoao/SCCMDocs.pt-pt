---
title: "Ferramenta de ligação do serviço | Documentos do Microsoft"
description: "Saiba mais sobre esta ferramenta que permite-lhe ligar ao serviço de nuvem do Configuration Manager para carregar manualmente as informações de utilização."
ms.custom: na
ms.date: 4/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
caps.latest.revision: 11
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 32f7fc4ef9c8e8d3c2ec8eeaf9a3174bad992ffb
ms.openlocfilehash: 0da80521bf223a765c3731f8ad59623d85a4c9fa
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="use-the-service-connection-tool-for-system-center-configuration-manager"></a>Utilize a Ferramenta de Ligação de Serviço no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize o **ferramenta de ligação de serviço** quando o ponto de ligação de serviço está no modo offline, ou quando os servidores de sistema de sites do Configuration Manager não estiverem ligados à Internet. A ferramenta pode ajudar a manter o seu site atualizado com as atualizações mais recentes do Configuration Manager.  

Quando for executada, a ferramenta manualmente estabelece ligação ao serviço de nuvem do Configuration Manager para carregar as informações de utilização para a hierarquia e para transferir atualizações. O carregamento dos dados de utilização é necessário para permitir ao serviço em nuvem fornecer as atualizações corretas para a sua implementação.  

## <a name="prerequisites-for-using-the-service-connection-tool"></a>Pré-requisitos para utilizar a ferramenta de ligação de serviço
Seguem-se os pré-requisitos e os problemas conhecidos.

**Pré-requisitos:**

-   Ter um ponto de ligação de serviço instalado e definido como **Offline, ligação a pedido**.  

-   A ferramenta tem de ser executada a partir de uma linha de comandos.  

-   Cada computador onde a ferramenta é executada (o computador do ponto de ligação de serviço e o computador que está ligado à Internet) tem de ser um sistema de x64 bits e tem de ter os seguintes elementos instalados:  

    -   Os ficheiros do **Visual C++ Redistributable** , tanto x86 como x64.   Por predefinição, o Configuration Manager instala o x64 versão no computador que aloja o ponto de ligação de serviço.  

         Para transferir uma cópia dos ficheiros do Visual C++, visite a página [Visual C++ Redistributable Packages for Visual Studio 2013](http://www.microsoft.com/download/details.aspx?id=40784) no Centro de Transferências da Microsoft.  

    -   .NET Framework 4.5.2 ou posterior.  

-   A conta que utiliza para executar a ferramenta tem de ter:
    -   Permissões de**administrador local** no computador que aloja o ponto de ligação de serviço (onde a ferramenta é executada).
    -   Permissões de**Leitura** para a base de dados do site.  



-   É necessário uma pen USB com espaço livre suficiente para armazenar ficheiros e atualizações ou outro método para transferir ficheiros entre o computador do ponto de ligação de serviço e o computador que tem acesso à Internet. (Este cenário pressupõe que o site e os computadores geridos não têm uma ligação direta à Internet).  



## <a name="use-the-service-connection-tool"></a>Utilizar a ferramenta de ligação de serviços  

 Pode encontrar a ferramenta de ligação de serviço (**serviceconnectiontool.exe**), no suporte de instalação do Configuration Manager no **%path%\smssetup\tools\ServiceConnectionTool** pasta. Utilize sempre a ferramenta de ligação de serviço que corresponde à versão do Configuration Manager que utilizar.


 Neste procedimento, os exemplos da linha de comandos utilizam os seguintes nomes de ficheiros e localizações de pastas (não é necessário utilizar estes caminhos e nomes de ficheiros e, em vez disso, pode utilizar alternativas que correspondam ao seu ambiente e preferências):  

-   O caminho para um Stick USB onde os dados são armazenados para transferência entre servidores:  **D:\USB\\**  

-   O nome do ficheiro. cab que contém dados exportados a partir do seu site: **UsageData.cab**  

-   O nome da pasta vazia onde serão armazenadas transferidas atualizações para o Configuration Manager para transferência entre servidores: **UpdatePacks**  

No computador que aloja o ponto de ligação de serviço:  

-   Abra uma linha de comandos com privilégios administrativos e, em seguida, mude de diretório para a localização que contém **serviceconnectiontool.exe**.  

     Por predefinição, pode encontrar esta ferramenta no suporte de instalação do Configuration Manager no **%path%\smssetup\tools\ServiceConnectionTool** pasta. Todos os ficheiros nesta pasta têm de estar na mesma pasta para que a ferramenta de ligação de serviço funcione.  

Ao executar o seguinte comando, a ferramenta prepara um ficheiro. cab que contém informações de utilização e copia-as para a localização que especificar. Os dados no ficheiro. cab baseiam-se no nível de dados de utilização de diagnóstico que o seu site estiver configurado para recolher. (veja [Dados de diagnóstico e de utilização para o System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)).  Execute o seguinte comando para criar o ficheiro. cab:  

-   **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

Também terá da copiar a pasta ServiceConnectionTool com todo o conteúdo para a unidade USB ou pode disponibilizá-la no computador que irá utilizar para os passos 3 e 4.  

### <a name="overview"></a>Descrição Geral
**Existem três passos principais para utilizar a ferramenta de ligação de serviço:**  

1.  **Preparar**:  Este passo é executado no computador que aloja o ponto de ligação de serviço. Quando é executada a ferramenta de que coloca os dados de utilização de um ficheiro. cab e armazena-a numa unidade USB (ou localização de transferência alternativo especificar).  

2.  **Ligar**: Para este passo de executar a ferramenta num computador remoto que liga à Internet para que possa carregar os dados de utilização e, em seguida, transferir atualizações.  

3.  **Importar**: Este passo é executado no computador que aloja o ponto de ligação de serviço. Quando for executada, a ferramenta importa que transferiu e adiciona-os para o seu site para que possa, em seguida, ver e instalar as atualizações a partir da consola do Configuration Manager.  

A partir da versão 1606, quando ligar à Microsoft, pode carregar vários ficheiros .cab ao mesmo tempo (cada um deles a partir de uma hierarquia diferente) e especificar um servidor proxy e um utilizador para o servidor proxy.   

**Para carregar vários ficheiros .cab:**
 -  Coloque cada ficheiro .cab que exportar de hierarquias separadas na mesma pasta. O nome de cada ficheiro tem de ser exclusivo e pode mudar o nomes do mesmo manualmente, se necessário.
 -  Em seguida, ao executar o comando para carregar dados para a Microsoft, especifique a pasta que contém os ficheiros .cab. (Antes da atualização 1606, só podia carregar dados de uma única hierarquia de cada vez e a ferramenta necessários para especificar o nome do ficheiro .cab na pasta.)
 -  Mais tarde, quando executar a tarefa de importação no ponto de ligação de serviço de uma hierarquia, a ferramenta só importa automaticamente os dados para essa hierarquia.  

**Para especificar um servidor proxy:**  
Pode utilizar os seguintes parâmetros opcionais para especificar um servidor proxy (mais informações sobre como utilizar estes parâmetros estão disponíveis na secção Parâmetros de linha de comandos deste tópico):
  - **-proxyserveruri [FQDN_of_proxy_sever]**  Utilize este parâmetro para especificar o servidor proxy a utilizar para esta ligação.
  -  **-proxyusername [username]**  Utilize este parâmetro quando tiver de especificar um utilizador para o servidor proxy.



### <a name="to-use-the-service-connection-tool"></a>Para utilizar a ferramenta de ligação de serviço  

1.  No computador que aloja o ponto de ligação de serviço:  

    -   Abra uma linha de comandos com privilégios administrativos e, em seguida, mude de diretório para a localização que contém **serviceconnectiontool.exe**.   

2.  Execute o seguinte comando para que a ferramenta prepare um ficheiro .cab que contém informações de utilização e o copie para a localização que especificar:  

    -   **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

    Se for carregar ficheiros .cab a partir de mais do que uma hierarquia em simultâneo, cada ficheiro .cab na pasta tem de ter um nome exclusivo. Pode mudar o nome dos ficheiros que adicionar à pasta manualmente.

    Se pretender ver as informações de utilização recolhidas para serem carregadas para o serviço em nuvem do Configuration Manager, execute o comando seguinte para exportar os mesmos dados como um ficheiro .csv que pode ver, em seguida, com uma aplicação como o Excel:  

    -   **serviceconnectiontool.exe -export -dest D:\USB\UsageData.csv**  

3.  Quando o passo de preparação estiver concluído, coloque a pen USB (ou transfira os dados exportados através de outro método) num computador que tenha acesso à Internet.  

4.  No computador com acesso à Internet, abra uma linha de comandos com privilégios administrativos e, em seguida, mude de diretório para a localização que contém uma cópia da ferramenta  **serviceconnectiontool.exe** e os ficheiros adicionais dessa pasta.  

5.  Execute o seguinte comando para iniciar o carregamento de informações de utilização e a transferência de atualizações para o Configuration Manager:  

    -   **serviceconnectiontool.exe-ligar - usagedatasrc D:\USB - updatepackdest D:\USB\UpdatePacks**

    Para obter mais exemplos desta linha de comandos, veja a secção [Opções de linha de comandos](../../../core/servers/manage/use-the-service-connection-tool.md#bkmk_cmd) mais à frente neste tópico.

    > [!NOTE]  
    >  Quando executa a linha de comandos para ligar ao serviço em nuvem do Configuration Manager, poderá ocorrer um erro semelhante ao seguinte:  
    >   
    >  -   Exceção não processada: System.UnauthorizedAccessException:  
    >   
    >      O acesso ao caminho "C:\  
    >     Users\br\AppData\Local\Temp\extractmanifestcab\95F8A562.sql" foi negado.  
    >   
    > Este erro pode ser ignorado com segurança e pode fechar a janela de erro e continuar.  

6.  Após a conclusão da transferência das atualizações para o Configuration Manager, coloque a unidade USB (ou transfira os dados exportados através de outro método) no computador que aloja o ponto de ligação de serviço.  

7.  No computador que aloja o ponto de ligação de serviço, abra uma linha de comandos com privilégios administrativos, mude de diretório para a localização que contém **serviceconnectiontool.exe**e execute o seguinte comando:  

    -   **serviceconnectiontool.exe -import -updatepacksrc D:\USB\UpdatePacks**  

8.  Quando a importação estiver concluída, pode fechar a linha de comandos. (Apenas são importadas atualizações para a hierarquia aplicável).  

9. Abra a consola do Configuration Manager e navegue para **administração** > **atualizações e a manutenção**. As atualizações que foram importadas estão agora disponíveis para instalação. (Antes da versão 1702, atualizações e a manutenção foi em **administração** > **serviços em nuvem**.)

 Para obter informações sobre como instalar atualizações, veja [Instalar atualizações na consola para o System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md).  

## <a name="bkmk_cmd"></a> Opções de linha de comandos  
 Para ver informações de ajuda relativas à ferramenta de ponto de ligação de serviço, abra a linha de comandos para a pasta que contém a ferramenta e execute o comando:  **serviceconnectiontool.exe**.  

|Opções da linha de comandos|Detalhes|  
|---------------------------|-------------|  
|**-prepare -usagedatadest [drive:][path][filename.cab]**|Este comando armazena os dados de utilização atuais num ficheiro .cab.<br /><br /> Execute este comando como **Administrador local** no servidor que aloja o ponto de ligação de serviço.<br /><br /> Exemplo:   **-prepare -usagedatadest D:\USB\Usagedata.cab**|    
|**-connect -usagedatasrc [unidade:][caminho] -updatepackdest [unidade:][caminho] -proxyserveruri [FQDN do servidor proxy] -proxyusername [nome de utilizador]** <br /> <br /> Se utilizar uma versão do Configuration Manager anterior à versão 1606, tem de especificar o nome do ficheiro .cab e não pode utilizar as opções para um servidor proxy.  Os parâmetros de comando suportados são: <br /> **-connect -usagedatasrc [unidade:][caminho][nome do ficheiro] -updatepackdest [unidade:][caminho]** |Este comando liga ao serviço em nuvem do Configuration Manager para carregar os ficheiros .cab de dados de utilização a partir da localização especificada e para transferir os pacotes de atualização disponíveis e conteúdo da consola. As opções para servidores proxy são opcionais.<br /><br /> Execute este comando como **administrador local** num computador que possa ser ligado à Internet.<br /><br /> Exemplo de ligação sem um servidor proxy: **-connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks** <br /><br /> Exemplo de ligação ao utilizar um servidor proxy: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itgproxy.redmond.corp.microsoft.com -proxyusername Meg** <br /><br /> Se utilizar uma versão anterior à versão 1606, tem de especificar um nome de ficheiro para o ficheiro .cab e não pode especificar um servidor proxy. Utilize a seguinte linha de comandos de exemplo: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks**|      
|**-import -updatepacksrc [drive:][path]**|Este comando importa os pacotes de atualizações e o conteúdo da consola que transferiu anteriormente para a consola do Configuration Manager.<br /><br /> Execute este comando como **Administrador local** no servidor que aloja o ponto de ligação de serviço.<br /><br /> Exemplo:  **-import -updatepacksrc D:\USB\UpdatePacks**|  
|**-export -dest [drive:][path][filename.csv]**|Este comando exporta dados de utilização para um ficheiro .csv, que poderá ver em seguida.<br /><br /> Execute este comando como **Administrador local** no servidor que aloja o ponto de ligação de serviço.<br /><br /> Exemplo: **-export -dest D:\USB\usagedata.csv**|  

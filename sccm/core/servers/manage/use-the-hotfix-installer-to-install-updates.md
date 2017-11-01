---
title: "Instalador de correções"
titleSuffix: Configuration Manager
description: "Determinar quando e como instalar atualizações através de instalador de correções para o Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3058277-c597-4dac-86d1-41b6f7e62b36
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 2ffb5c913a6863de3dbf1415961bb6987033b6ea
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="use-the-hotfix-installer-to-install-updates-for-system-center-configuration-manager"></a>Utilize o Instalador de Correções para instalar atualizações no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Algumas atualizações do System Center Configuration Manager não estão disponíveis no serviço em nuvem Microsoft e só são obtidas fora de banda. Um exemplo é uma correção de versão limitada para resolver um problema específico.   
Quando tem de instalar uma atualização (ou correção) que recebe da Microsoft, e essa atualização tem um nome de ficheiro que termina com a extensão **.exe** (não **update.exe**), utilize o instalador de correções que está incluído com a transferência dessa correção para instalar a atualização diretamente para o servidor de site do Configuration Manager.  

 Se o ficheiro de correção tiver a **. update.exe** extensão de ficheiro, consulte [utilizar a ferramenta de registo de atualização para importar correções para o System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

> [!NOTE]  
>  Este tópico fornece orientações gerais sobre como instalar correções que atualizam o System Center Configuration Manager. Para obter detalhes sobre uma atualização específica, consulte o artigo correspondente na Base de Dados de Conhecimento (KB), no Suporte da Microsoft.  

##  <a name="bkmk_Overview"></a>Descrição geral de correções para o Configuration Manager  
 Correções para o Configuration Manager são semelhantes às de outros produtos Microsoft, como o SQL Server, contêm uma correção individual ou um pacote (uma agregação de correções) e são descritas num artigo da Base de dados de Conhecimento Microsoft.  

 As atualizações individuais incluem uma única atualização focada para uma versão específica do Configuration Manager.  
Pacotes atualizados incluem várias atualizações para uma versão específica do Configuration Manager.  
Quando uma atualização é um pacote, não é possível instalar atualizações individuais a partir desse pacote.  

 Se planear criar implementações para instalar atualizações em computadores adicionais, terá de instalar o pacote de atualização num servidor do site de administração central ou num servidor do site primário.  

 Quando executa o pacote de atualização, ocorrerá o seguinte:  

-   Extrai os ficheiros de atualização para cada componente aplicável a partir do pacote de atualização.  

-   Inicia um assistente que o orienta ao longo de um processo para configurar as atualizações e opções de implementação para as atualizações.  

-   Depois de concluir o assistente, as atualizações do pacote aplicáveis ao servidor do site são instaladas no mesmo.  

O assistente cria também implementações que poderá utilizar para instalar as atualizações em computadores adicionais. O utilizador implementa as atualizações em computadores adicionais ao utilizar um método de implementação suportado, como um pacote de implementação de software ou o Microsoft System Center Updates Publisher 2011.  

 Quando o assistente é executado, é criado um ficheiro **.cab** no servidor do site para ser utilizado com o Updates Publisher 2011. Opcionalmente, pode configurar o assistente para também criar um ou mais pacotes para a implementação de software. Pode utilizar estas implementações para instalar atualizações de componentes, tais como clientes ou a consola do Configuration Manager. Também pode instalar atualizações manualmente em computadores que executem o cliente do Configuration Manager.  

 Os seguintes três grupos no Configuration Manager podem ser atualizados:  

-   O Configuration Manager funções de servidor, que incluem:  

    -   Site de administração central  

    -   Site primário  

    -   Site Secundário  

    -   Fornecedor de SMS Remoto  

-   Consola do Configuration Manager  

-   Cliente do Configuration Manager  

> [!NOTE]  
>  **Atualizações para funções do sistema de sites** (incluindo atualizações para a base de dados do site e pontos de distribuição baseado na nuvem) são instaladas como parte da atualização de servidores de sites e serviços pelo Gestor de componentes do site.  
>   
>  No entanto, os pontos de distribuição de solicitação de atualizações são servidos pelo Gestor de distribuição em vez do Gestor de componentes do site.  

 Cada pacote de atualização para o Configuration Manager é um ficheiro de .exe extração automática (SFX) que contém os ficheiros que são necessários para instalar a atualização nos componentes aplicáveis do Configuration Manager. Normalmente, o ficheiro SFX pode conter os seguintes ficheiros:  

|Ficheiro|Detalhes|  
|----------|-------------|  
|&lt;Versão do produto\>- QFE-KB&lt;ID do artigo KB\>-&lt;plataforma\>-&lt;idioma\>.exe|Este é o ficheiro de atualização. A linha de comandos para este ficheiro é gerida por Updatesetup.exe.<br /><br /> Por exemplo:<br />CM1511RTM-QFE-KB123456-X 64-ENU.exe|  
|Updatesetup.exe|Este invólucro .msi gere a instalação do pacote de atualização.<br /><br /> Ao executar a atualização, o Updatesetup.exe deteta o idioma de apresentação do computador em que é executado. Por predefinição, a interface de utilizador da atualização encontra-se em inglês. No entanto, quando o idioma de apresentação é suportado, a interface de utilizador é apresentada no idioma local do computador.|  
|License_&lt;idioma\>.rtf|Quando aplicável, cada atualização contém um ou mais ficheiros de licença para os idiomas suportados.|  
|&lt;Produto & tipodeatualização >-&lt;versão do produto\>-&lt;ID do artigo KB\>-&lt;plataforma\>. msp|Quando a atualização é aplicável à consola do Configuration Manager ou clientes, o pacote de atualização inclui ficheiros de patch (. msp) separados do Windows Installer.<br /><br /> Por exemplo:<br /><br /> **Atualização da consola do Configuration Manager:** ConfigMgr1511 AdminUI-KB1234567 i386.msp<br /><br /> **Atualização do cliente:** ConfigMgr1511-cliente KB1234567 i386.msp<br />ConfigMgr1511-cliente KB1234567 x64.msp|  

 Por predefinição, o pacote de atualização regista as ações num ficheiro .log no servidor do site. O ficheiro de registo tem o mesmo nome que o pacote de atualização e é escrito na pasta **%SystemRoot%/Temp** .  

 Quando executa o pacote de atualização, é extraído um ficheiro para uma pasta temporária com o mesmo nome que o pacote de atualização e, em seguida, Updatesetup.exe é executado. Updatesetup.exe inicia a atualização de Software para o Configuration Manager &lt;versão do produto\> &lt;número da BDC\> assistente.  

 Como aplicável ao âmbito da atualização, o assistente cria uma série de pastas sob a pasta de instalação do System Center Configuration Manager no servidor do site. A estrutura de pastas é semelhante à seguinte:   
 **\\\\&lt;Nome do servidor\>\SMS_&lt;código do Site\>\Hotfix\\&lt;número da BDC\>\\&lt;atualizar tipo\>\\&lt;plataforma\>**.  

 A tabela seguinte fornece detalhes sobre as pastas na estrutura de pastas:  

|Nome da pasta|Mais informações|  
|-----------------|----------------------|  
|&lt;Nome do servidor\>|Este é o nome do servidor do site em que executou o pacote de atualização.|  
|SMS _&lt;código do Site\>|Este é o nome da partilha da pasta de instalação do Configuration Manager.|  
|&lt;Número da KB\>|Este é o número de ID do artigo da Base de Dados de Conhecimento relativo a este pacote de atualização.|  
|&lt;Tipo de atualização\>|Estes são os tipos de atualizações do Configuration Manager. O assistente cria uma pasta separada para cada tipo de atualização contido no pacote de atualização. Os nomes das pastas representam os tipos de atualização. Estas definições incluem o seguinte:<br /><br /> **Servidor**: Inclui atualizações para servidores de sites, servidores de base de dados do site e computadores que executam o fornecedor de SMS.<br /><br /> **Cliente**: Inclui atualizações para o cliente do Configuration Manager.<br /><br /> **AdminConsole**: Inclui atualizações para a consola do Configuration Manager<br /><br /> Para além dos tipos de atualização anteriores, o assistente cria uma pasta denominada **SCUP**. Esta pasta não representa um tipo de atualização. Em vez disso, contém o ficheiro .cab para o Updates Publisher.|  
|&lt;Plataforma\>|Esta é uma pasta específica da plataforma. Contém os ficheiros de atualização específicos de um tipo de processador.  Estas pastas incluem:<br /><br />-x64<br /><br /> -I386|  

##  <a name="bkmk_Install"></a> Como instalar atualizações  
 Para instalar atualizações, terá primeiro de instalar o pacote de atualização num servidor do site. Ao instalar um pacote de atualizações, este inicia um assistente de instalação para essa atualização. Este assistente faz o seguinte:  

-   Extrai os ficheiros de atualização  

-   Ajuda-o a configurar as implementações  

-   Instala as atualizações aplicáveis nos componentes de servidor do computador local  

Depois de instalar o pacote de atualização num servidor do site, poderá atualizar componentes adicionais para o Configuration Manager. A tabela seguinte descreve as ações de atualização destes diversos componentes:  

|Componente|Instruções|  
|---------------|------------------|  
|Servidor do site|Implementar as atualizações num servidor de site remoto quando não optar por instalar o pacote de atualização diretamente nesse servidor de site remoto.|  
|Base de dados do site|Em servidores de site remotos, implemente as atualizações do servidor que incluam uma atualização da base de dados do site se não instalar o pacote de atualização diretamente nesse servidor de site remoto.|  
|Consola do Configuration Manager|Após a instalação inicial da consola do Configuration Manager, poderá instalar atualizações para a consola do Configuration Manager em cada computador que executa a consola. Não é possível modificar os ficheiros de instalação de consola do Configuration Manager para aplicar as atualizações durante a instalação inicial da consola.|  
|Fornecedor de SMS Remoto|Instale atualizações para cada instância do Fornecedor de SMS que seja executada num computador que não o servidor do site onde instalou o pacote de atualização.|  
|Clientes do Configuration Manager|Após a instalação inicial do cliente do Configuration Manager, poderá instalar atualizações para o cliente do Configuration Manager em cada computador que executa o cliente.|  

> [!NOTE]  
>  Pode implementar atualizações apenas a computadores que executam o cliente do Configuration Manager.  

 Se reinstalar um cliente, a consola do Configuration Manager ou o fornecedor de SMS, terá também de reinstalar as atualizações desses componentes.  

 Utilize as informações nas secções seguintes para instalar atualizações de cada um dos componentes do Configuration Manager.  

###  <a name="bkmk_servers"></a> Atualizar servidores  
 As atualizações de servidores podem incluir atualizações de **sites**, da **site database**e de computadores que executem uma instância do **Fornecedor de SMS**:  

####  <a name="bkmk_site"></a>Atualizar um site  
 Para atualizar um site do Configuration Manager, pode instalar o pacote de atualização diretamente no servidor do site ou implementar as atualizações para um servidor de site após instalar o pacote de atualização noutro site.  

 Ao instalar uma atualização num servidor de site, o processo de instalação da atualização gere as ações adicionais necessárias para aplicar a atualização, tais como atualizar as funções do sistema de sites. A exceção a este procedimento é a base de dados do site. A secção seguinte contém informações sobre como atualizar a base de dados do site.  

####  <a name="bkmk_database"></a>Atualizar uma base de dados do site  
 Para atualizar a base de dados do site, o processo de instalação executa um ficheiro chamado **update.sql** na base de dados do site. Poderá configurar o processo de atualização para atualizar automaticamente a base de dados do site ou optar por atualizar manualmente a base de dados do site, mais tarde.  

 **Atualização automática da base de dados do Site**  

 Quando instala o pacote de atualização num servidor do site, pode optar por atualizar automaticamente a base de dados do site quando a atualização do servidor está instalada. Esta decisão aplica-se apenas ao servidor do site onde instalou o pacote de atualização e não é aplicável a implementações criadas para instalar as atualizações em servidores de site remoto.  

> [!NOTE]  
>  Quando optar por atualizar automaticamente a base de dados do site, o processo de atualizações de uma base de dados independentemente se a base de dados está localizada no servidor do site ou num computador remoto.  

> [!IMPORTANT]  
>  Antes de atualizar a base de dados do site, crie uma cópia de segurança da base de dados do site. Não é possível desinstalar uma atualização da base de dados do site. Para obter informações sobre como criar uma cópia de segurança para o Configuration Manager, consulte [cópia de segurança e recuperação para o System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

 **Atualização manual da base de dados do Site**  

 Se optar por não atualizar automaticamente a base de dados do site quando instala o pacote de atualização no servidor do site, a atualização do servidor não modificar a base de dados no servidor do site onde é executado o pacote de atualização. No entanto, as implementações que utilizam o pacote criado para a implementação de software ou que instala sempre atualizam a base de dados do site.  

> [!WARNING]  
>  Quando a atualização inclui atualizações para o servidor do site e a base de dados do site, a atualização não é funcional até concluir a atualização para o servidor do site e a base de dados do site. Até a atualização é aplicada para a base de dados do site, o site estará num Estado não suportado.  

 **Para atualizar manualmente uma base de dados do site:**  

1.  No servidor do site parar o serviço SMS_SITE_COMPONENT_MANAGER e, em seguida, pare o serviço SMS_EXECUTIVE.  

2.  Feche a consola do Configuration Manager.  

3.  Execute o script de atualização com o nome **update.sql** na base de dados desse site. Para obter informações sobre como executar um script para atualizar uma base de dados do SQL Server, consulte a documentação para a versão do SQL Server que utilizar para o servidor de base de dados do site.  

4.  Reinicie os serviços que foram interrompidos nos passos anteriores.  

5.  Quando o pacote de atualização é instalado, extrairá **update.sql** na seguinte localização no servidor do site:  **\\\\&lt;Nome do servidor\>\SMS_&lt;código do Site\>\Hotfix\\&lt;número da BDC\>\update.sql**  

####  <a name="bkmk_provider"></a>Atualizar um computador que executa o fornecedor de SMS  
 Depois de instalar um pacote de atualização que inclui atualizações para o fornecedor de SMS, terá de implementar a atualização em cada computador que executa o fornecedor de SMS. A única exceção é a instância do Fornecedor de SMS instalada anteriormente no servidor do site onde instalou o pacote de atualizações. A instância local do fornecedor de SMS no servidor do site é atualizada quando instala o pacote de atualização.  

 Se remover e, em seguida, reinstalar o fornecedor de SMS num computador, tem de reinstalar a atualização para o fornecedor de SMS nesse computador.  

###  <a name="BKMK_clients"></a>Atualizar clientes  
 Quando instala uma atualização que inclui atualizações para o cliente do Configuration Manager, é-lhe apresentada a opção para atualizar automaticamente os clientes com a instalação da atualização ou atualizar manualmente os clientes numa altura posterior. Para obter mais informações sobre a atualização automática de clientes, veja [Como atualizar clientes em computadores Windows](https://technet.microsoft.com/library/mt627885.aspx).  

 Pode implementar atualizações com o Updates Publisher ou um pacote de implementação de software, ou pode optar por instalar manualmente a atualização em cada cliente. Para obter mais informações sobre como utilizar implementações para instalar atualizações, veja a secção [Implementar atualizações para o Configuration Manager](#BKMK_Deploy) deste tópico.  

> [!IMPORTANT]  
>  Quando instalar atualizações de clientes e o pacote de atualização incluir atualizações de servidores, lembre-se de que também instala as atualizações de servidor no site primário ao qual os clientes são atribuídos.  

Para instalar manualmente a atualização do cliente, em cada cliente de Configuration Manager, tem de executar **Msiexec.exe** e referenciar o ficheiro. msp de atualização de cliente específico da plataforma.  

 Por exemplo, pode utilizar a seguinte linha de comandos para uma atualização do cliente. Esta linha de comandos executa o MSIEXEC no computador cliente e referencia o ficheiro. msp que o pacote de atualização extraiu no servidor do site: **msiexec.exe /p \\ \\ &lt;ServerName\>\SMS_&lt;SiteCode\>\Hotfix\\&lt;número da BDC\>\Client\\&lt;plataforma\>\\&lt;\\<ServerName>\sms_<sitecode>\hotfix\<KB\> /L\*v &lt;logfile\>REINSTALLMODE = mous REINSTALL = ALL**  

###  <a name="BKMK_console"></a>Atualizar consolas do Configuration Manager  
 Para atualizar uma consola do Configuration Manager, tem de instalar a atualização no computador que executa a consola depois de concluída a instalação da consola.  

> [!IMPORTANT]  
>  Quando instalar atualizações para a consola do Configuration Manager e o pacote de atualização incluir atualizações de servidores, lembre-se de que também instala as atualizações de servidor no site que utiliza com a consola do Configuration Manager.  

Se o computador que atualizar executar o cliente do Configuration Manager:  

-   Pode utilizar uma implementação para instalar a atualização. Para obter mais informações sobre como utilizar implementações para instalar atualizações, veja a secção [Implementar atualizações para o Configuration Manager](#BKMK_Deploy) deste tópico.  

-   Se tiver iniciado sessão diretamente no computador cliente, pode executar a instalação interativamente.  

-   Pode instalar manualmente a atualização em cada computador. Para instalar manualmente a atualização da consola do Configuration Manager, em cada computador que executa a consola do Configuration Manager, pode executar o Msiexec.exe e referenciar o ficheiro. msp de atualização de consola do Configuration Manager.  

Por exemplo, pode utilizar a seguinte linha de comandos para atualizar uma consola do Configuration Manager. Esta linha de comandos executa o MSIEXEC no computador e referencia o ficheiro. msp que o pacote de atualização extraiu no servidor do site: **msiexec.exe /p \\ \\ &lt;ServerName\>\SMS_&lt;SiteCode\>\Hotfix\\&lt;número da BDC\>\AdminConsole\\&lt;plataforma\>\\&lt;\\<ServerName>\sms_<sitecode>\hotfix\<KB\> /L\*v &lt;logfile\>REINSTALLMODE = mous REINSTALL = ALL**  

##  <a name="BKMK_Deploy"></a> Implementar atualizações para o Configuration Manager  
 Depois de instalar o pacote de atualização num servidor do site, pode utilizar um dos três métodos seguintes para implementar atualizações noutros computadores.  

###  <a name="BKMK_DeploySCUP"></a>Utilizar o Updates Publisher 2011 para instalar atualizações  
 Quando instala o pacote de atualização num servidor do site, a instalação do assistente cria um ficheiro de catálogo para o Updates Publisher que pode utilizar para implementar as atualizações nos computadores aplicáveis. O assistente cria sempre este catálogo, mesmo quando o utilizador seleciona a opção **Utilizar pacote e programa para implementar esta atualização**.  

 O catálogo para o Updates Publisher é designado **SCUPCatalog.cab** e pode ser encontrado na seguinte localização no computador onde é executado o pacote de atualização: **\\\\&lt;ServerName\>\SMS_&lt;SiteCode\>\Hotfix\\&lt;número da BDC\>\SCUP\SCUPCatalog.cab**  

> [!IMPORTANT]  
>  Porque o ficheiro SCUPCatalog.cab é criado utilizando caminhos específicos para o servidor do site onde está instalado o pacote de atualização, não pode ser utilizado noutros servidores de site.  

 Depois de concluído o assistente, pode importar o catálogo para o Updates Publisher e, em seguida, utilizar atualizações de software do Configuration Manager para implementar as atualizações. Para obter informações sobre o Updates Publisher, consulte [Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkID=83449) na Biblioteca TechNet do System Center 2012.  

 Utilize o procedimento seguinte para importar o ficheiro SCUPCatalog.cab para o Updates Publisher e publicar as atualizações.  

##### <a name="to-import-the-updates-to-updates-publisher-2011"></a>Para importar as atualizações para o Updates Publisher 2011  

1.  Inicie a consola do Updates Publisher e clique em **importação**.  

2.  No **tipo de importação** página a importar as atualizações de catálogo do Assistente de Software, selecione **especifique o caminho para o catálogo a importar**e, em seguida, especifique o ficheiro SCUPCatalog.cab.  

3.  Clique em **seguinte**e, em seguida, clique em **seguinte** novamente.  

4.  No **aviso de segurança - validação de catálogo** caixa de diálogo, clique em **aceitar**. Feche o assistente depois de estar concluído.  

5.  Na consola do Updates Publisher, selecione a atualização que pretende implementar e, em seguida, clique em **publicar**.  

6.  No **opções de publicação** página a publicar Software do Assistente de atualizações, selecione **conteúdo completo**e, em seguida, clique em **seguinte**.  

7.  Conclua o Assistente para publicar as atualizações.  

###  <a name="BKMK_DeploySWDist"></a>Utilizar a implementação de software para instalar atualizações  
 Quando instala o pacote de atualização no servidor do site de um site primário ou site de administração central, pode configurar a instalação do Assistente para criar pacotes de atualização para implementação de software. Em seguida, pode implementar cada pacote para uma coleção de computadores que pretende atualizar.  

 Para criar um pacote de implementação de software, o **configurar implementação da atualização de Software** página do assistente, selecione a caixa de verificação para a atualização de cada tipo de pacote que pretende atualizar. Os tipos disponíveis podem incluir servidores, consolas do Configuration Manager e os clientes. É criado um pacote separado para cada tipo de atualização que selecionou.  

> [!NOTE]  
>  O pacote de servidores contém atualizações para os seguintes componentes:  
>   
>  -   Servidor do site  
>  -   Fornecedor de SMS  
>  -   Base de dados do site  

 Em seguida, na página **Configurar Método de Implementação de Atualização do Software** do assistente, selecione a opção **Utilizarei a distribuição de software**. Esta seleção direciona o Assistente para criar os pacotes de implementação de software.  

 Depois de concluído o assistente, pode ver os pacotes criados na consola do Configuration Manager no **pacotes** no nó de **biblioteca de Software** área de trabalho. Em seguida, pode utilizar o processo padrão para implementar pacotes de software em clientes do Configuration Manager. Quando um pacote é executado num cliente, instala as atualizações para os componentes aplicáveis do Configuration Manager no computador cliente.  

 Para obter informações sobre como implementar pacotes nos clientes do Configuration Manager, consulte [pacotes e programas no System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

###  <a name="BKMK_DeployCollections"></a>Criar coleções para implementar atualizações do Configuration Manager  
 Pode implementar atualizações específicas em clientes aplicáveis. As seguintes informações podem ajudar a criar coleções de dispositivos para os diferentes componentes do Configuration Manager.  

|Componente do Configuration Manager|Instruções|  
|----------------------------------------|------------------|  
|Servidor do site de administração central|Crie uma consulta de associação direta e adicione o computador do servidor do site de administração central.|  
|Todos os servidores primários do site|Crie uma consulta de associação direta e adicione cada computador do servidor do site primário.|  
|Todos os servidores do site secundário|Crie uma consulta de associação direta e adicione cada computador do servidor do site secundário.|  
|Todos os clientes x86|Crie uma coleção com os seguintes critérios de consulta:<br /><br /> **Selecione \* de SMS_R_System interna associar SMS_G_System_SYSTEM no SMS_G_System_SYSTEM. ResourceID = SMS_R_System.ResourceId onde SMS_G_System_SYSTEM. SystemType = "PC baseado em X86"**|  
|Todos os clientes x64|Crie uma coleção com os seguintes critérios de consulta:<br /><br /> **Selecione \* de SMS_R_System interna associar SMS_G_System_SYSTEM no SMS_G_System_SYSTEM. ResourceID = SMS_R_System.ResourceId onde SMS_G_System_SYSTEM. SystemType = "PC baseado em X64"**|  
|Todos os computadores que executam a consola do Configuration Manager|Crie uma consulta de associação direta e adicione cada computador.|  
|Computadores remotos que executam uma instância do Fornecedor de SMS|Crie uma consulta de associação direta e adicione cada computador.|  

> [!NOTE]  
>  Para atualizar uma base de dados do site, implemente a atualização no servidor deste site.  

 Para obter informações sobre como criar coleções, veja [Como criar coleções no System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

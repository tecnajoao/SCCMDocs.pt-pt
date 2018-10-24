---
title: Exemplos de MDT
titleSuffix: Microsoft Deployment Toolkit
description: 'Amostras do Microsoft Deployment Toolkit. '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 2ff0100c-b7ef-4e09-8c96-fc1898390b6d
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 6b36da9f98749858829ab591571496532b26f290
ms.sourcegitcommit: 7198ec49d9ce68c6d55bfb9e2d537b5442a132cb
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/09/2018
ms.locfileid: "33915977"
---
# <a name="microsoft-deployment-toolkit-samples-guide"></a>Guia de amostras do Microsoft Deployment Toolkit  
 Este guia faz parte do Microsoft® Deployment Toolkit (MDT) 2013 e guias de uma equipa especialista em através da implementação de sistemas operativos Windows e Microsoft Office. Especificamente, este guia foi concebido para fornecer definições de configuração de exemplo para cenários de implementação específicos.  

> [!NOTE]
>  Neste documento, *Windows* aplica-se aos sistemas operativos Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2, exceto indicação em contrário. MDT não suporta ARM processador versões do Windows. Da mesma forma, *MDT* refere-se ao MDT 2013, salvo indicação em contrário.  

 **Para utilizar este guia**  

 Reveja a lista de tópicos do cenário na tabela de conteúdo.  

1.  Selecione o cenário que melhor coincida representa os objetivos de implementação da sua organização.  

2.  Reveja as definições de configuração de exemplo para o cenário selecionado.  

3.  Utilize as definições de configuração de exemplo como a base para as definições de configuração no seu ambiente.  

4.  Personalize as definições de configuração de exemplo para o seu ambiente.  

 Em muitos casos, mais do que um cenário poderá ser necessário para concluir as definições de configuração para o ambiente.  

 Dado que este guia contém apenas definições de configuração de exemplo, rever os guias listados na tabela seguinte pode ainda mais ajudar a personalizar as definições de configuração para o ambiente.  

 |Guia|Este guia oferece assistência para o ajudar|  
 |-|-|  
 |*Guia de introdução do Microsoft System Center 2012 R2 Configuration Manager* |Utilize System Center 2012 R2 Configuration Manager para instalar o sistema operativo do Windows 8.1 num cenário de implementação do novo computador.|  
 |*Guia de introdução para instalação Lite Touch* |Instale o sistema de operativo do Windows 8.1 através do Lite Touch Installation (LTI) utilizando suportes de dados de um cenário de implementação do novo computador.|  
 |*Guia de introdução para instalação orientado por utilizador* |Instale o sistema operativo do Windows 8.1 com o modo de instalação e o System Center 2012 R2 Configuration Manager, um cenário de implementação do novo computador.|  
 |*Utilizar o Microsoft Deployment Toolkit* |Personalize ainda mais os ficheiros de configuração utilizados em implementações de Zero Touch instalação (ZTI) e LTI. Este guia também fornece orientações de configuração genérico e uma referência técnica para definições de configuração.|


## <a name="deploying-windows-8-applications-using-mdt"></a>Implementação de aplicações do Windows 8 com o MDT  
 MDT, pode implementar pacotes de aplicações do Windows 8, que tem uma extensão de ficheiro. AppX. Estes pacotes de aplicações estiver familiarizados com o Windows 8. Para obter mais informações sobre estas aplicações, consulte [desenvolvimento da aplicação da loja Windows.](http://msdn.microsoft.com/windows/apps)  

 Implemente aplicações do Windows 8 com o MDT, efetuando os seguintes passos:  

-   Implementar aplicações do Windows 8 com LTI, conforme descrito em [implementar o Windows 8 aplicações utilizando LTI](#DeployWin8LTI).  

-   Implementar aplicações do Windows 8 utilizando o modo instalação (UDI) conforme descrito em [implementar o Windows 8 aplicações utilizando UDI](#DeployWin8UDI).  

###  <a name="DeployWin8LTI"></a> Implementação de aplicações do Windows 8 com LTI  
 Pode implementar aplicações do Windows 8 com LTI como qualquer outra aplicação que inicia o processo de instalação de uma linha de comandos. Pode adicionar aplicações do Windows 8 em implementações LTI no nó de aplicações no Deployment Workbench.  

 **Para implementar uma aplicação do Windows 8 com LTI**  

1.  Crie uma pasta partilhada de rede onde pretende armazenar a aplicação.  

2.  Copie a aplicação do Windows 8 para a pasta de rede partilhada que criou no passo anterior.  

     Certifique-se de que copie o ficheiro. AppX de aplicação do Windows 8 e quaisquer outros ficheiros necessários, tal como um ficheiro. cer que contém o certificado de aplicação.  

3.  Crie um item de aplicação LTI para a aplicação do Windows 8 no nó de aplicações no Deployment Workbench com o novo Assistente de aplicação.  

     Ao concluir o Assistente de nova aplicação, no **detalhes do comando** no assistente página **linha de comandos**, tipo **app_file_name** (onde *app_file_name*  é o nome da aplicação do Windows 8).  

     Para obter mais informações sobre como concluir o Assistente de aplicação nova no Deployment Workbench, consulte as secções seguintes no documento do MDT, *utilizar o Microsoft Deployment Toolkit*:  

    -   "Criar uma nova aplicação é implementada a partir da partilha de implementação"  

    -   "Criar uma nova aplicação é implementada a partir da outra pasta partilhada de rede"  

4.  Selecione o item de aplicação LTI criado no passo anterior de uma sequência de tarefas LTI.  

###  <a name="DeployWin8UDI"></a> Implementação de aplicações do Windows 8 com o UDI  
 Pode implementar aplicações do Windows 8 com o UDI como qualquer outra aplicação que inicia o processo de instalação de uma linha de comandos. Pode adicionar aplicações do Windows 8 para implementações de UDI no **ApplicationPage** página do assistente no UDI Wizard Designer.  

> [!NOTE]
>  Implementação do Windows 8 e aplicações do Windows 8 com o UDI requer o System Center 2012 R2 Configuration Manager.  

 **Para implementar uma aplicação do Windows 8 com o UDI**  

1.  Crie uma pasta partilhada de rede onde pretende armazenar a aplicação.  

     Esta pasta será a pasta de origem para a aplicação do Configuration Manager que irá criar posteriormente no processo.  

2.  Copie a aplicação do Windows 8 para a pasta de rede partilhada que criou no passo anterior.  

     Certifique-se de que copie o ficheiro. AppX de aplicação do Windows 8 e quaisquer outros ficheiros necessários, tal como um ficheiro. cer que contém o certificado de aplicação.  

3.  Adicionar a aplicação do Windows 8 como uma aplicação do Configuration Manager  

4.  Crie um item de aplicação do Configuration Manager para a aplicação do Windows 8 utilizando o Assistente para criar aplicação da consola do Configuration Manager.  

     Ao concluir o Assistente para criar aplicação, crie um tipo de implementação para implementar a aplicação do Windows 8 utilizando o Assistente para criar tipo de implementação. No Assistente de criação de implementação de tipo no **conteúdo** na página **programa de instalação**, tipo **app_file_name** (onde *app_file_name*é o nome da aplicação do Windows 8).  

     Para obter mais informações sobre como concluir o Assistente para criar aplicação na consola do Configuration Manager, consulte as secções seguintes na biblioteca de documentação do System Center 2012 Configuration Manager, que é incluído no Configuration Manager:  

    -   [Como criar aplicações no Configuration Manager](http://technet.microsoft.com/library/gg682159.aspx)  

    -   [Como criar tipos de implementação no Configuration Manager](http://technet.microsoft.com/library/gg682174.aspx#BKMK_Step3)  

    -   [Como gerir aplicações e tipos de implementação no Configuration Manager](http://technet.microsoft.com/library/gg682031)  

5.  Certifique-se de que a funcionalidade de (UDA) de afinidade de dispositivo do utilizador no Configuration Manager está corretamente configurada para suportar a afinidade entre utilizadores e dispositivos para implementação de aplicação do Configuration Manager.  

     Para obter mais informações sobre como configurar o UDA para suportar a implementação de aplicação do Configuration Manager, consulte [como gerir afinidade dispositivo / utilizador no Configuration Manager](http://technet.microsoft.com/library/gg699365).  

6.  Implemente a aplicação que criou no passo 4 para os utilizadores-alvo.  

     Para obter mais informações sobre como implementar uma aplicação para utilizador, consulte [como implementar aplicações no Configuration Manager](http://technet.microsoft.com/library/gg682082).  

7.  Configurar o **ApplicationPage** página do Assistente para incluir a aplicação do Configuration Manager criada no passo 4 com o UDI Wizard Designer.  

     Para obter mais informações sobre como configurar o **ApplicationPage** página do assistente com o UDI Wizard Designer, consulte a secção "passo 5-11: Personalizar o ficheiro de configuração do Assistente de UDI para o computador de destino,"no documento MDT *manual para a instalação do modo de início rápido*.  

8.  Selecione o item de aplicação de UDI criado no passo anterior numa sequência de tarefas UDI.  

    > [!NOTE]
    >  O Windows 8 aplicação não está instalada para a sequência de tarefas, mas em vez disso, vai ser instalado na primeira vez a utilizador inicia sessão no computador de destino (conforme definido pela definição UDA configurada no passo 5) a utilizar a funcionalidade de instalador de aplicação centrada no utilizador (AppInstall.exe) no UDI.  

     Para obter mais informações sobre a funcionalidade de instalador de aplicação centrada no utilizador no UDI, consulte a secção "Centrada no utilizador aplicação instalador Reference", no documento MDT *Toolkit referência*.  

## <a name="managing-mdt-using-windows-powershell"></a>Gerir o MDT com o Windows PowerShell  
 Pode gerir partilhas de implementação do MDT com o Deployment Workbench e o Windows PowerShell. MDT inclui um Windows PowerShell™ snap in—Microsoft.BDD.SnapIn—that têm de ser carregados antes de utilizar as funcionalidades específicas do MDT no Windows PowerShell. O snap-in do MDT Windows PowerShell inclui:  

-   Um fornecedor de Windows PowerShell — MDTProvider — que fornece acesso ao conteúdo de uma partilha de implementação  

-   Cmdlets que fornecem a capacidade para administrar as partilhas de implementação do MDT  

 Faça a gestão de partilhas de implementação do MDT com o Windows PowerShell, efetuando os seguintes passos:  

-   Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [ao carregar o Snap-In do PowerShell do Windows MDT](#LoadMDTSnapIn).  

-   Criar uma partilha de implementação com o Windows PowerShell conforme descrito em [criar uma implementação partilhar utilizando o Windows PowerShell](#CreateDeployShare).  

-   Ver propriedades de partilha de implementação com o Windows PowerShell conforme descrito em [visualizar implementação partilhar as propriedades utilizando o Windows PowerShell](#ViewDeployShareProp).  

-   Ver a lista de partilhas de implementação através do Windows PowerShell, conforme descrito em [ver a lista de implementação partilhas utilizando o Windows PowerShell](#ViewListDeployShare).  

-   Atualizar uma partilha de implementação, o que gera novas imagens de arranque de ambiente de pré-instalação do Windows (Windows PE), conforme descrito em [atualizar uma implementação partilhar utilizando o Windows PowerShell](#UpdateDeployShare).  

-   Atualizar uma partilha de implementação ligado, que replica conteúdo a partir de uma partilha de implementação para a partilha de implementação ligado, conforme descrito em [atualizar um ligado implementação partilhar utilizando o Windows PowerShell](#UpdateLinkedDeployShare).  

-   Atualizar a implementação suporte de dados que replica conteúdo a partir de uma partilha de implementação para o suporte de dados de implementação e, em seguida, gera novas imagens de arranque, conforme descrito em [atualizar a implementação de suportes de dados utilizando o Windows PowerShell](#UpdateDeployMedia).  

-   Gerir itens numa partilha de implementação (por exemplo, sistemas operativos, pacotes de sistema operativo, aplicações e controladores de dispositivo), conforme descrito em [itens gerir uma implementação partilhar utilizando o Windows PowerShell](#ManageItemDeployShare).  

-   Automatizar a população de itens numa partilha de implementação (por exemplo, sistemas operativos, pacotes de sistema operativo, aplicações e controladores de dispositivo), conforme descrito em [automatizar a população de uma partilha de implementação](#AutomatePopulateDeployShare).  

-   Gerir as pastas numa partilha de implementação com o Windows PowerShell conforme descrito em [gerir implementação partilhar pastas utilizando o Windows PowerShell](#ManageDeployShareFolder).  

###  <a name="LoadMDTSnapIn"></a> Carregar o Snap-In do PowerShell do Windows MDT  
 Os cmdlets do MDT são fornecidos num snap-in do Windows PowerShell **Microsoft.BDD.SnapIn** que têm de ser carregados antes de utilizar os cmdlets do MDT. Pode carregar o snap-in do MDT Windows PowerShell utilizando qualquer um dos seguintes métodos:  

-   Carregue o snap-in do MDT Windows PowerShell utilizando a consola de módulos do PowerShell de janela conforme descrito em [carregar o MDT Windows PowerShell Snap-In utilizando a tarefa de módulos do sistema de importação](#LoadMDTSnapInImport).  

-   Carga o snap-in do MDT Windows PowerShell utilizando o **Add-PSSnapIn** cmdlet, conforme descrito em [carregar o MDT Windows PowerShell Snap-In utilizando o Cmdlet Add-PSSnapIn](#LoadMDTSnapInCmdlet).  

####  <a name="LoadMDTSnapInImport"></a> Carregar o MDT Windows Snap-In do PowerShell através da tarefa de módulos do sistema de importação  
 A tarefa de importação sistema módulos inclui automaticamente todos os módulos do Windows PowerShell e snap-ins que se encontrem nos módulos no diretório %Windir%\System32\WindowsPowerShell\1.0\Modules. MDT instala automaticamente o snap-in Windows PowerShell do MDT **Microsoft.BDD.SnapIn** nessa pasta durante o processo de instalação do MDT.  

> [!NOTE]
>  A tarefa de importação sistema módulos está disponível apenas no Windows 7 e Windows Server 2008 R2 quando o Windows PowerShell 3.0 não está instalado no computador. A partir do Windows PowerShell 3.0, os módulos são importados automaticamente na primeira vez que utilize um cmdlet no módulo.  

 Pode iniciar uma consola do Windows PowerShell com a tarefa de importação sistema módulos efetuando um dos seguintes procedimentos:  

-   Na barra de tarefas, clique com botão direito do **do Windows PowerShell** ícone e, em seguida, clique em **importar sistema módulos**.  

-   Clique em **iniciar**, aponte para **ferramentas administrativas** e, em seguida, clique em **módulos do Windows PowerShell**.  

 Para obter mais informações sobre uma consola do Windows PowerShell com módulos de sistema de importação de iniciar a máquina, consulte [iniciar o Windows PowerShell com módulos de sistema de importação](http://msdn.microsoft.com/library/windows/desktop/hh847866.aspx).  

####  <a name="LoadMDTSnapInCmdlet"></a> Carregar o MDT Windows Snap-In do PowerShell utilizando o Cmdlet adicionar-PSSnapIn  
 Pode carregar o snap-in Windows PowerShell do MDT **Microsoft.BDD.PSSnapIn** de qualquer ambiente do Windows PowerShell utilizando o [Add-PSSnapIn](http://technet.microsoft.com/library/hh849705.aspx) cmdlet, como a mostrar no exemplo seguinte:  

```  
Add-PSSnapin -Name Microsoft.BDD.PSSnapIn  
```  

###  <a name="CreateDeployShare"></a> Criar uma partilha de implementação com o Windows PowerShell  
 Pode criar partilhas de implementação utilizando os cmdlets do Windows PowerShell do MDT. A pasta de raiz para a partilha de implementação é criada e partilhados com o padrão cmdlets do Windows PowerShell e chamadas para comandos de classe de Windows Management Instrumentation (WMI). A partilha de implementação é preenchida com o fornecedor de MDTProvider Windows PowerShell e o [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) cmdlet. A unidade de MDTProvider Windows PowerShell é persistente através de **adicionar MDTPersistentDrive** cmdlet.  

 **Para preparar uma partilha de implementação utilizando os cmdlets do Windows PowerShell do MDT**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [ao carregar o Snap-In do PowerShell do Windows MDT](#LoadMDTSnapIn).  

2.  Criar a pasta que irá ser a raiz da nova implementação partilha utilizando o **Novo Item** cmdlet, como mostrado no exemplo seguinte e descrito em [utilizando o Cmdlet New-Item](http://technet.microsoft.com/library/ee176914.aspx):  

    ```  
    New-Item "C:\MDTDeploymentShare$" -Type directory  
    ```  

     O cmdlet apresenta a criação com êxito da pasta.  

3.  Partilhe a pasta que criou o passo anterior utilizando o **WMI win32_share** classe como sown no exemplo seguinte:  

    ```  
    ([wmiclass]"win32_share").Create("C:\MDTDeploymentShare$", "MDTDeploymentShare$",0)  
    ```  

     A chamada para o **win32_share** classe devolve os resultados da chamada. Se o valor de **ReturnValue** é zero (0), em seguida, a chamada foi concluída com êxito.  

4.  Especifique a pasta partilhada novo como uma partilha de implementação utilizando o [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose  
    ```  

     O cmdlet começa automaticamente a criar a partilha de implementação e copiar as informações de modelo para a nova partilha de implementação. Após a conclusão do processo de cópia, o cmdlet apresenta as informações para a nova partilha de implementação.  

    > [!NOTE]
    >  O valor fornecido a *nome* parâmetro (DS002) têm de ser exclusivo e não pode ser o mesmo que uma partilha de implementação existente unidade do Windows PowerShell.  

5.  Certifique-se de que as pastas de partilha de implementação adequada foram criadas utilizando o **dir** comando, como a mostrar no exemplo seguinte:  

    ```  
    dir ds002:  
    ```  

     É apresentada a lista de pastas predefinidas na raiz da partilha de implementação.  

6.  Adicionar a nova partilha de implementação para a lista de partilhas de implementação MDT persistentes, utilizando o **adicionar MDTPersistentDrive** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    $NewDS=Get-PSDrive "DS002"  
    Add-MDTPersistentDrive  -Name "DS002" -InputObject $NewDS Verbose  
    ```  

     Neste exemplo, o *$NewDS* variável é utilizada para transmitir o objeto de unidade do Windows PowerShell para a nova partilha de implementação para o cmdlet.  

     Em alternativa, pode ter combinadas o [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) e **adicionar MDTPersistentDrive** cmdlets, conforme mostrado no exemplo seguinte:  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose | Add-MDTPersistentDrive -Verbose  
    ```  

     No exemplo anterior, a pipeline do Windows PowerShell fornece o *nome* e *InputObject* parâmetros.  

###  <a name="ViewDeployShareProp"></a> Ver propriedades de partilha de implementação com o Windows PowerShell  
 Pode ver as propriedades de partilhas de implementação do MDT com o [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) cmdlet e o fornecedor de MDTProvider Windows PowerShell. Estas propriedades mesmas também podem ser vistas no Deployment Workbench.  

 **Para ver as propriedades de partilha de implementação utilizando os cmdlets do Windows PowerShell do MDT**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [ao carregar o Snap-In do PowerShell do Windows MDT](#LoadMDTSnapIn).  

2.  Certifique-se as implementações do MDT partilham do Windows PowerShell unidades são restauradas com autoridade utilizando o **restauro MDTPersistentDrive** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implementações do MDT que partilhem unidades do Windows PowerShell já forem restauradas, receberá uma mensagem de aviso que indica que o cmdlet não consegue restaurar a unidade.  

3.  Certifique-se de que as implementações do MDT que partilhem unidades do Windows PowerShell são restauradas corretamente utilizando o [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet, da seguinte forma:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell que são fornecidas utilizando a MDTProvider estão listadas.  

4.  Ver as propriedades da partilha de implementação utilizando o [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Get-ItemProperty "DS002:"  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell devolvido no passo 3. O cmdlet devolve as propriedades para a partilha de implementação.  

###  <a name="ViewListDeployShare"></a> Ver a lista de partilhas de implementação com o Windows PowerShell  
 Pode ver a lista de partilhas de implementação do MDT com o [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet e o fornecedor de MDTProvider Windows PowerShell. A mesma lista de partilhas de implementação também pode ser visualizada no Deployment Workbench.  

 **Para ver uma lista de partilhas de implementação utilizando os cmdlets do Windows PowerShell do MDT**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [ao carregar o Snap-In do PowerShell do Windows MDT](#LoadMDTSnapIn).  

2.  Certifique-se de que as implementações do MDT partilham do Windows PowerShell unidades são restauradas com autoridade utilizando o **restauro MDTPersistentDrive** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implementações do MDT que partilhem unidades do Windows PowerShell já forem restauradas, receberá uma mensagem de aviso que indica que o cmdlet não consegue restaurar a unidade.  

3.  Ver a lista de implementações do MDT que partilhem unidades de Windows PowerShell, um para cada partilha de implementação, utilizando o [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet, da seguinte forma:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista do Windows PowerShell unidades fornecidas a utilizar o MDTProvider estiver listadas, um para cada partilha de implementação.  

###  <a name="UpdateDeployShare"></a> Atualizar uma partilha de implementação com o Windows PowerShell  
 Pode atualizar as partilhas de implementação utilizando o **atualização MDTDeploymentShare** cmdlet e o fornecedor de MDTProvider Windows PowerShell. Atualizar uma partilha de implementação cria as imagens de arranque do Windows PE (WIM e International Organization para ficheiros uniformização [ISO]) necessário para iniciar a implementação LTI. Pode efetuar o mesmo processo utilizando o Deployment Workbench, conforme descrito em "Atualizar uma implementação partilha no Deployment Workbench".  

 **Para atualizar uma partilha de implementação com o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [ao carregar o Snap-In do PowerShell do Windows MDT](#LoadMDTSnapIn).  

2.  Certifique-se de que as implementações do MDT que partilhem unidades do Windows PowerShell são restauradas com autoridade utilizando o **restauro MDTPersistentDrive** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implementações do MDT que partilhem unidades do Windows PowerShell já forem restauradas, receberá uma mensagem de aviso que indica que o cmdlet não consegue restaurar a unidade.  

3.  Certifique-se de que as implementações do MDT que partilhem unidades do Windows PowerShell são restauradas corretamente utilizando o [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet, da seguinte forma:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecida a utilizar o MDTProvider estão listadas.  

4.  Atualização da partilha de implementação utilizando o **atualização MDTDeploymentShare** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Update-MDTDeploymentShare -Path "DS002:" -Force  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell devolvido no passo 3.  

    > [!NOTE]
    >  A partilha de implementação de atualização pode demorar muito tempo. O progresso do cmdlet é apresentado na parte superior da consola do Windows PowerShell.  

     O cmdlet devolve sem saída se a atualização for concluída com êxito.  

###  <a name="UpdateLinkedDeployShare"></a> Atualizar uma partilha de implementação ligado com o Windows PowerShell  
 Pode atualizar as partilhas de implementação ligado (replicar) utilizando o **atualização MDTLinkedDS** cmdlet e o fornecedor de MDTProvider Windows PowerShell. Atualizar uma partilha de implementação ligado replica os conteúdos da partilha de implementação original para a partilha de implementação ligado. Pode efetuar o mesmo processo utilizando o Deployment Workbench, conforme descrito em "Replicar ligado implementação partilhas no Deployment Workbench".  

 **Para atualizar uma partilha de implementação ligado com o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [ao carregar o Snap-In do PowerShell do Windows MDT](#LoadMDTSnapIn).  

2.  Certifique-se de que as implementações do MDT que partilhem unidades do Windows PowerShell são restauradas com autoridade utilizando o **restauro MDTPersistentDrive** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implementações do MDT que partilhem unidades do Windows PowerShell já forem restauradas, receberá uma mensagem de aviso que indica que o cmdlet não consegue restaurar a unidade.  

3.  Certifique-se de que as implementações do MDT que partilhem unidades do Windows PowerShell são restauradas corretamente utilizando o [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet, da seguinte forma:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecida a utilizar o MDTProvider estão listadas.  

4.  Atualização da partilha de implementação utilizando o **atualização MDTDeploymentShare** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell devolvido no passo 3.  

    > [!NOTE]
    >  A atualização da partilha de implementação ligado, pode demorar muito tempo. O progresso do cmdlet é apresentado na parte superior da consola do Windows PowerShell.  

     O cmdlet devolve sem saída se a atualização for concluída com êxito.  

###  <a name="UpdateDeployMedia"></a> Atualizar o suporte de dados de implementação através do Windows PowerShell  
 Pode atualizar (gerar) através de suportes de dados de implementação de **atualização MDTMedia** cmdlet e o fornecedor de MDTProvider Windows PowerShell. Suporte de dados de implementação de atualização replica os conteúdos da partilha de implementação original para a partilha de implementação ligado e, em seguida, gera ficheiros. ISO e. wim. Pode efetuar o mesmo processo utilizando o Deployment Workbench, conforme descrito em "Gerar suporte de dados de imagens no Deployment Workbench".  

 Quando o **atualização MDTMedia** cmdlet termina, são criados os seguintes ficheiros:  

-   Um ficheiro. ISO do *media_folder* pasta (onde *media_folder* é o nome da pasta que especificou para o suporte de dados)  

     O ficheiro. ISO a gerar é uma opção que configura através de:  

    -   Selecionar o **gerar uma imagem ISO de arranque Lite Touch** caixa de verificação a **geral** separador do **multimédia propriedades** caixa de diálogo (desmarque esta caixa de verificação para reduzir o tempo necessário para gerar o suporte de dados, a menos que precisa criar suportes DVDs ou iniciar máquinas virtuais [VMs] do ficheiro. ISO.)  

    -   Definir a propriedade mesmo utilizando o [conjunto ItemProperty](http://technet.microsoft.com/library/hh849844) cmdlet  

-   Ficheiros WIM no *media_folder*\Content\Deploy\Boot pasta (onde *media_folder* é o nome da pasta que especificou para o suporte de dados)  

 **Para atualizar uma partilha de implementação ligado com o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [ao carregar o Snap-In do PowerShell do Windows MDT](#LoadMDTSnapIn).  

2.  Certifique-se de que as implementações do MDT partilham do Windows PowerShell unidades são restauradas com autoridade utilizando o **restauro MDTPersistentDrive** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implementações do MDT que partilhem unidades do Windows PowerShell já forem restauradas, receberá uma mensagem de aviso que indica que o cmdlet não consegue restaurar a unidade.  

3.  Certifique-se de que as implementações do MDT que partilhem unidades do Windows PowerShell são restauradas corretamente utilizando o [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet, da seguinte forma:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecida a utilizar o MDTProvider estão listadas.  

4.  Atualização da partilha de implementação utilizando o **atualização MDTDeploymentShare** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell devolvido no passo 3.  

    > [!NOTE]
    >  A atualização da partilha de implementação ligado, pode demorar muito tempo. O progresso do cmdlet é apresentado na parte superior da consola do Windows PowerShell.  

     O cmdlet devolve sem saída se a atualização for concluída com êxito.  

###  <a name="ManageItemDeployShare"></a> Gerir itens numa partilha de implementação com o Windows PowerShell  
 Uma partilha de implementação contém itens que são utilizados para efetuar implementações, tais como sistemas operativos, aplicações, controladores de dispositivo, sistema operativo pacotes e sequências de tarefas. Estes itens podem geridos através de cmdlets do Windows PowerShell e aos fornecidos com o MDT.  

 Para obter mais informações sobre a manipulação de itens diretamente utilizando cmdlets do Windows PowerShell, consulte [manipular diretamente itens](http://technet.microsoft.com/library/dd315266.aspx). A estrutura de pastas para uma partilha de implementação também pode ser gerida com o Windows PowerShell. Para obter mais informações, consulte [gerir implementação partilha pastas utilizando o Windows PowerShell](#ManageDeployShareFolder).  

####  <a name="ImportItemDeployShare"></a> Importar um Item para uma partilha de implementação  
 Pode importar cada tipo de item, como sistemas operativos, aplicações ou de controladores de dispositivo, utilizando cmdlets do MDT. Para cada tipo de item, há um cmdlet específico do MDT. Se pretender importar vários itens para uma partilha de implementação com o Windows PowerShell, consulte [automatizar a população de uma partilha de implementação](#AutomatePopulateDeployShare).  

 A tabela seguinte lista o MDT Windows PowerShell cmdlets utilizados para importar itens para uma partilha de implementação e fornece uma breve descrição de cada cmdlet. Exemplos de como utilizar cada cmdlet é fornecido na secção que corresponde a cada cmdlet.  

 |**Cmdlet** | **Descrição** |  
 |-|-|  
 |**Import-MDTApplication** |Importa uma aplicação para uma partilha de implementação|  
 |**Import-MDTDriver** |Importa um ou mais controladores de dispositivo para uma partilha de implementação|  
 |**Import-MDTOperatingSystem** |Importa um ou mais sistemas de operativos para uma partilha de implementação|  
 |**Import-MDTPackage** |Importa um ou mais pacotes de sistema operativo para uma partilha de implementação|  
 |**Import-MDTTaskSequence** |Importa uma sequência de tarefas para uma partilha de implementação|  

####  <a name="ViewPropertyDeployShare"></a> Ver as propriedades de um Item numa partilha de implementação  
 Cada item numa partilha de implementação tem um conjunto diferente de propriedades. Pode ver as propriedades de um item numa partilha de implementação utilizando o [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) cmdlet. O [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) cmdlet utiliza o MDTProvider para apresentar as propriedades de um item específico, tal como pode ver as propriedades no Deployment Workbench.  

 Se pretender pretende ver as propriedades de vários itens numa implementação partilhar com o Windows PowerShell, consulte o artigo [automatizar a população de uma partilha de implementação](#AutomatePopulateDeployShare).  

 **Para ver as propriedades de um item numa partilha de implementação com o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [ao carregar o Snap-In do PowerShell do Windows MDT](#LoadMDTSnapIn).  

2.  Certifique-se de que as implementações do MDT que partilhem unidades do Windows PowerShell são restauradas com autoridade utilizando o **restauro MDTPersistentDrive** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implementações do MDT que partilhem unidades do Windows PowerShell já forem restauradas, receberá uma mensagem de aviso que indica que o cmdlet não consegue restaurar a unidade.  

3.  Certifique-se de que as implementações do MDT que partilhem unidades do Windows PowerShell são restauradas corretamente utilizando o [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecida a utilizar o MDTProvider estão listadas.  

4.  Devolver uma lista dos itens para o tipo de item para o qual são intenção ver as propriedades utilizando o [Get-Item](http://technet.microsoft.com/library/hh849788) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     No exemplo anterior, é apresentada uma lista de todos os sistemas operativos na partilha de implementação. O resultado é direcionado para o **formato-lista** cmdlet para que os nomes dos sistemas operativos longos podem ser vistos. Para obter mais informações sobre como utilizar o **formato-lista** cmdlet, consulte [utilizando o Cmdlet de formato-lista](http://technet.microsoft.com/library/ee176830.aspx). O mesmo processo pode ser utilizado para devolver a lista de outros tipos de itens, tais como controladores de dispositivo ou aplicações.  

    > [!TIP]
    >  Foi também utiliza o **dir** comando para ver a lista de sistemas operativos em vez do [Get-Item](http://technet.microsoft.com/library/hh849788) cmdlet.  

5.  Ver as propriedades de um dos itens listados o passo anterior utilizando o [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Get-ItemProperty -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     Neste exemplo, o valor da *caminho* parâmetro é o caminho completamente qualificado do Windows PowerShell para o item, incluindo o nome de ficheiro que foi devolvido no passo anterior. Pode utilizar o mesmo processo para ver as propriedades dos outros tipos de itens, tais como controladores de dispositivo ou aplicações.  

####  <a name="RemoveItemDeployShare"></a> Remover um Item a uma partilha de implementação  
 Pode remover um item de uma partilha de implementação utilizando o [Remove-Item](http://technet.microsoft.com/library/hh849765) cmdlet. O [Remove-Item](http://technet.microsoft.com/library/hh849765) cmdlet utiliza o MDTProvider para remover um item específico, tal como pode remover um item no Deployment Workbench. Se pretender remover vários itens numa implementação partilhar com o Windows PowerShell, consulte [automatizar a população de uma partilha de implementação](#AutomatePopulateDeployShare).  

> [!NOTE]
>  Remover um item que utiliza uma sequência de tarefas faz com que a sequência de tarefas falhar. Certifique-se de que um item não é referenciado por outros itens numa partilha de implementação antes de remover o item. Assim que um item é removido, este não pode ser recuperado.  

 **Para remover um item a uma partilha de implementação com o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [ao carregar o Snap-In do PowerShell do Windows MDT](#LoadMDTSnapIn).  

2.  Certifique-se de que as implementações do MDT que partilhem unidades do Windows PowerShell são restauradas com autoridade utilizando o **restauro MDTPersistentDrive** cmdlet, conforme mostrado no exemplo seguinte.  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implementações do MDT que partilhem unidades do Windows PowerShell já forem restauradas, receberá uma mensagem de aviso que indica que o cmdlet não consegue restaurar a unidade.  

3.  Certifique-se de que as implementações do MDT que partilhem unidades do Windows PowerShell são restauradas corretamente utilizando o [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecida a utilizar o MDTProvider estão listadas.  

4.  Devolver uma lista dos itens para o tipo de item para o qual são intenção ver as propriedades utilizando o [Get-Item](http://technet.microsoft.com/library/hh849788) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     No exemplo anterior, é apresentada uma lista de todos os sistemas operativos na partilha de implementação. O resultado é direcionado para o **formato-lista** cmdlet para que os nomes dos sistemas operativos longos podem ser vistos. Para obter mais informações sobre como utilizar o **formato-lista** cmdlet, consulte [utilizando o Cmdlet de formato-lista](http://technet.microsoft.com/library/ee176830.aspx). Pode utilizar o mesmo processo para devolver a lista de outros tipos de itens, tais como controladores de dispositivo ou aplicações.  

    > [!TIP]
    >  Foi também utiliza o **dir** comando para ver a lista de sistemas operativos em vez do [Get-Item](http://technet.microsoft.com/library/hh849788) cmdlet.  

5.  Remover um dos itens listados o passo anterior utilizando o [Remove-Item](http://technet.microsoft.com/library/hh849765) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Remove-Item -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     Neste exemplo, o valor da *caminho* parâmetro é o caminho completamente qualificado do Windows PowerShell para o item, incluindo o nome de ficheiro que foi devolvido no passo anterior.  

     Pode utilizar o mesmo processo para remover outros tipos de itens, tais como controladores de dispositivo ou aplicações.  

    > [!NOTE]
    >  Remover um item que utiliza uma sequência de tarefas faz com que a sequência de tarefas falhar. Certifique-se de que um item não é referenciado por outros itens numa partilha de implementação antes de remover o item.  

###  <a name="AutomatePopulateDeployShare"></a> Automatizar a população de uma partilha de implementação  
 Os cmdlets Windows PowerShell do MDT permitem-lhe gerir itens individuais. No entanto, utilizando algumas das funcionalidades scripts do Windows PowerShell, os cmdlets podem ser utilizados para automatizar a população de uma partilha de implementação.  

 Por exemplo, uma organização poderá ter de implementar várias partilhas de implementação para unidades empresariais diferentes ou uma organização pode fornecer do sistema operativo dos serviços de implementação de outras organizações. Em ambos estes exemplos, as organizações necessitam da capacidade de criar e preencher as partilhas de implementação que estão configuradas de forma consistente.  

 Um método para a gestão de vários itens seria utilizar um ficheiro de valores separados por vírgulas (CSV) que contém uma lista de todos os itens que pretende gerir numa implementação partilham utilizando o [importação de CSV](http://technet.microsoft.com/library/dd347665.aspx) cmdlet.  

 Segue-se um excerpt de um script do Windows PowerShell para importar uma lista de aplicações com base nas informações de um ficheiro. csv, utilizando o [importação de CSV](http://technet.microsoft.com/library/dd347665.aspx), [ForEach-Object](http://technet.microsoft.com/library/hh849731), e  **Importar MDTApplication** cmdlets:  

```  
$List=Import-CSV "C:\MDT\Import-MDT-Apps.csv"  
ForEach-Object ($App in $List) {  
Import-MDTApplication –path $App.ApplicationFolder -enable "True" –Name $App.DescriptiveName –ShortName $App.Shortname –Version $App.Version –Publisher $App.Publisher –Language $App.Language –CommandLine $App.CommandLine –WorkingDirectory $App.WorkingDirectory –ApplicationSourcePath $App.SourceFolder –DestinationFolder $App.DestinationFolder –Verbose  
}  
```  

 Neste exemplo, o ficheiro de C:\MDT\Import-MDT-Apps.csv contém um campo para cada variável necessário para importar uma aplicação. Para obter mais informações sobre como criar um ficheiro. csv para utilização com o [importação de CSV](http://technet.microsoft.com/library/dd347665.aspx) cmdlet, consulte [utilizando o Cmdlet de importação de Csv](http://technet.microsoft.com/library/ee176874.aspx).  

 Pode utilizar este método mesmo para importar os sistemas operativos, controladores de dispositivo e outros itens numa partilha de implementação, efetuando os seguintes passos:  

1.  Crie um ficheiro. csv para cada tipo de item de partilha de implementação que pretende povoar.  

2.  Para obter mais informações sobre como criar um ficheiro. csv para utilização com o [importação de CSV](http://technet.microsoft.com/library/dd347665.aspx) cmdlet, consulte [utilizando o Cmdlet de importação de Csv](http://technet.microsoft.com/library/ee176874.aspx).  

3.  Crie um ficheiro de script do Windows PowerShell que será utilizado para automatizar a população da partilha de implementação.  

     Para obter mais informações sobre como criar um script do Windows PowerShell, consulte [Scripting com o Windows PowerShell](http://technet.microsoft.com/scriptcenter/powershell.aspx).  

4.  Crie qualquer estrutura de pastas de pré-requisitos necessária na partilha de implementação antes de importar os itens de partilha de implementação.  

     Para obter mais informações, consulte [gerir implementação partilha pastas utilizando o Windows PowerShell](#ManageDeployShareFolder).  

5.  Adicionar o [importação de CSV](http://technet.microsoft.com/library/dd347665.aspx) linha do cmdlet para um dos ficheiros. csv criada no passo 1.  

     Para mais informações sobre o [importação de CSV](http://technet.microsoft.com/library/dd347665.aspx) cmdlet, consulte [utilizando o Cmdlet de importação de Csv](http://technet.microsoft.com/library/ee176874.aspx).  

6.  Criar um [ForEach-Object](http://technet.microsoft.com/library/hh849731) ciclo de cmdlet que processa cada item do ficheiro. csv referenciado no [importação de CSV](http://technet.microsoft.com/library/dd347665.aspx) cmdlet no passo anterior.  

     Para mais informações sobre o [ForEach-Object](http://technet.microsoft.com/library/hh849731) cmdlet, consulte [utilizando o Cmdlet ForEach-Object](http://technet.microsoft.com/library/ee176828).  

7.  Adicione o cmdlet do MDT correspondente para importar os itens de partilha de implementação no interior do [ForEach-Object](http://technet.microsoft.com/library/hh849731) ciclo de cmdlet criado no passo anterior.  

     Para obter mais informações sobre os cmdlets do MDT utilizados para importar itens para uma partilha de implementação, consulte [importar um Item para uma partilha de implementação](#ImportItemDeployShare).  

###  <a name="ManageDeployShareFolder"></a> Gerir pastas de partilha de implementação com o Windows PowerShell  
 Pode gerir pastas de uma partilha de implementação utilizando ferramentas de linha de comandos, tal como o **mkdir** comando ou utilizar cmdlets do Windows PowerShell, como o [Novo Item](http://technet.microsoft.com/library/hh849795) cmdlet e o MDTProvider Windows Fornecedor do PowerShell. A mesma estrutura de pasta de partilhas de implementação também pode ser vista e gerida no Deployment Workbench. Para obter mais informações sobre a manipulação de itens diretamente utilizando cmdlets do Windows PowerShell, consulte [manipular diretamente itens](http://technet.microsoft.com/library/dd315266.aspx).  

#### <a name="create-a-folder-in-a-deployment-share-using-windows-powershell"></a>Crie uma pasta numa partilha de implementação com o Windows PowerShell  
 **Para criar uma pasta numa partilha de implementação com o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [ao carregar o Snap-In do PowerShell do Windows MDT](#LoadMDTSnapIn).  

2.  Certifique-se de que as implementações do MDT que partilhem unidades do Windows PowerShell são restauradas com autoridade utilizando o **restauro MDTPersistentDrive** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implementações do MDT que partilhem unidades do Windows PowerShell já forem restauradas, receberá uma mensagem de aviso que indica que o cmdlet não consegue restaurar a unidade.  

3.  Ver a lista de implementações do MDT que partilhem unidades de Windows PowerShell, um para cada partilha de implementação, utilizando o [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet da seguinte forma:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista do Windows PowerShell unidades fornecidas a utilizar o MDTProvider estiver listadas, um para cada partilha de implementação  

4.  Crie uma pasta denominada *Windows_8* na pasta numa implementação de sistemas operativos partilhar utilizando o **mkdir** comando, conforme mostrado no exemplo seguinte:  

    ```  
    mkdir "DS002:\Operating Systems\Windows_8"  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell devolvido no passo 3.  

5.  Certifique-se de que a pasta é criada corretamente, escrevendo o seguinte comando:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     É apresentada a pasta de Windows_8 e quaisquer outras pastas existentes na pasta de sistemas operativos.  

6.  Crie uma pasta denominada *Windows_7* pasta na pasta de sistemas operativos numa partilha de implementação utilizando o [Novo Item](http://technet.microsoft.com/library/hh849795) cmdlet, como mostrado no exemplo seguinte e descrito em [utilizando o Cmdlet de novo Item](http://technet.microsoft.com/library/ee176914.aspx):  

    ```  
    New-Item "DS002:\Operating Systems\Windows_7" -Type directory  
    ```  

     O cmdlet apresenta a criação com êxito da pasta.  

7.  Certifique-se de que a pasta é criada corretamente, escrevendo o seguinte comando:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     É apresentada a pasta de Windows_7 e quaisquer outras pastas existentes na pasta de sistemas operativos.  

#### <a name="delete-a-folder-in-a-deployment-share-using-windows-powershell"></a>Eliminar uma pasta numa partilha de implementação com o Windows PowerShell  
 **Para eliminar uma pasta numa partilha de implementação com o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [ao carregar o Snap-In do PowerShell do Windows MDT](#LoadMDTSnapIn).  

2.  Certifique-se de que as implementações do MDT que partilhem unidades do Windows PowerShell são restauradas com autoridade utilizando o **restauro MDTPersistentDrive** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implementações do MDT que partilhem unidades do Windows PowerShell já forem restauradas, receberá uma mensagem de aviso que indica que o cmdlet não consegue restaurar a unidade.  

3.  Ver a lista de implementações do MDT que partilhem unidades de Windows PowerShell, um para cada partilha de implementação, utilizando o [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet da seguinte forma:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista do Windows PowerShell unidades fornecidas a utilizar o MDTProvider estiver listadas, um para cada partilha de implementação.  

4.  Eliminar (remover) uma pasta denominada *Windows_8* na pasta numa implementação de sistemas operativos partilhar utilizando o **mkdir** comando, conforme mostrado no exemplo seguinte:  

    ```  
    rmdir "DS002:\Operating Systems\Windows_8"  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell devolvido no passo 3.  

5.  Certifique-se de que a pasta é removida corretamente, escrevendo o seguinte comando:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     A pasta de Windows_8 já não é apresentada na lista de pastas na pasta de sistemas operativos  

6.  Eliminar (remover) uma pasta denominada *Windows_7* pasta na pasta de sistemas operativos numa partilha de implementação utilizando o [Remove-Item](http://technet.microsoft.com/library/hh849765) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Remove-Item "DS002:\Operating Systems\Windows_7"  
    ```  

     O cmdlet apresenta a remoção com êxito da pasta.  

7.  Certifique-se de que a pasta é criada corretamente, escrevendo o seguinte comando:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     A pasta de Windows_7 já não é apresentada na lista de pastas na pasta de sistemas operativos.  

#### <a name="rename-a-folder-in-a-deployment-share-using-windows-powershell"></a>Mudar o nome de uma pasta numa partilha de implementação com o Windows PowerShell  
 **Para mudar o nome de uma pasta numa partilha de implementação com o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [ao carregar o Snap-In do PowerShell do Windows MDT](#LoadMDTSnapIn).  

2.  Certifique-se de que as implementações do MDT partilham do Windows PowerShell unidades são restauradas com autoridade utilizando o **restauro MDTPersistentDrive** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implementações do MDT que partilhem unidades do Windows PowerShell já forem restauradas, receberá uma mensagem de aviso que indica que o cmdlet não consegue restaurar a unidade.  

3.  Vista de lista de implementações do MDT partilhar unidades do Windows PowerShell, um para cada implementação partilhar, utilizando o [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet da seguinte forma:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista do Windows PowerShell unidades fornecidas a utilizar o MDTProvider estiver listadas, um para cada partilha de implementação.  

4.  Mudar o nome de uma pasta denominada *Windows_8* para *Win_8* na pasta numa implementação de sistemas operativos partilhar utilizando o **ren** comando, conforme mostrado no exemplo seguinte:  

    ```  
    ren "DS002:\Operating Systems\Windows_8" "Win_8"  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell devolvido no passo 3.  

5.  Certifique-se de que a pasta é removida corretamente, escrevendo o seguinte comando:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     A pasta de Windows_8 é mudada para *Win_8*.  

6.  Mudar o nome de uma pasta denominada *Windows_7* para *Win-7* na pasta numa implementação de sistemas operativos partilhar utilizando o [Item de mudança de nome](http://technet.microsoft.com/library/hh849763) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Rename-Item "DS002:\Operating Systems\Windows_7" "Win_7"  
    ```  

     O cmdlet apresenta a com êxito a mudança de nome da pasta.  

7.  Certifique-se de que a pasta é criada corretamente, escrevendo o seguinte comando:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     A pasta de Windows_7 é mudada para *Win_7*.  

## <a name="automating-the-application-of-operating-system-service-packs-in-deployment-shares"></a>Automatizar a aplicação de serviço do sistema operativo pacotes em partilhas de implementação  
 Pacotes de serviço do sistema operativo são uma parte normal do ciclo de vida do software. Os sistemas de operativos existentes numa implementação partilhas tem de ser atualizada com estes pacotes de serviço para ajudar a garantir que recentemente implementado ou atualizado computadores estão atualizados com as definições de configuração e as recomendações de segurança mais recentes.  

 Em situações em que uma organização tem várias partilhas de implementação com vários sistemas operativos em cada partilha de implementação, o processo para atualizar manualmente os sistemas operativos em cada partilha de implementação com os service packs pode ser demorado. Os métodos para automatizar a aplicação do serviço de sistema operativo de pacotes de implementação partilhas incluem:  

-   Copiar a atualizar o conteúdo de origem que já contém o pacote de serviço (por exemplo, Windows 7 com SP1 suporte de dados) para a pasta na partilha de implementação em que o sistema operativo existente reside, conforme descrito em [automatizar a aplicação de Pacotes de serviço do sistema operativo do suporte de dados de origem atualizados](#AutomateAppFromUSM)  

-   Aplicar o service pack para um computador de referência e, em seguida, capturar uma imagem atualizada do computador de referência, conforme descrito em [automatizar a aplicação do sistema operativo serviço pacotes a utilizar um computador de referência e o Windows PowerShell](#AutomateAppUsingRef)  

###  <a name="AutomateAppFromUSM"></a> Automatizar a aplicação dos pacotes de serviço do sistema operativo do suporte de dados de origem atualizados  
 Pode automatizar o processo de atualização de pacotes de serviço do sistema operativo com o Windows PowerShell quando tiver de suporte de dados de origem que incluem o service pack, tais como tendo um DVD que tenha o Windows 7 com SP1 já integrado.  

 Para que este método, o suporte de dados de origem de sistema operativo com o service pack é copiado os ficheiros de sistema operativo existente sem o service pack na partilha de implementação com o Windows PowerShell.  

 **Para automatizar a aplicação dos pacotes de serviço do sistema operativo do suporte de dados de origem das atualizações com o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [ao carregar o Snap-In do PowerShell do Windows MDT](#LoadMDTSnapIn).  

2.  Certifique-se de que as implementações do MDT que partilhem unidades do Windows PowerShell são restauradas com autoridade utilizando o **restauro MDTPersistentDrive** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implementações do MDT que partilhem unidades do Windows PowerShell já forem restauradas, receberá uma mensagem de aviso que indica que o cmdlet não consegue restaurar a unidade.  

3.  Vista de lista de implementações do MDT partilhar unidades do Windows PowerShell, um para cada implementação partilhar, utilizando o [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista do Windows PowerShell unidades fornecidas a utilizar o MDTProvider estiver listadas, um para cada partilha de implementação.  

4.  Remove a pasta para o sistema operativo existente da partilha de implementação utilizando o [Get-ChildItem](http://technet.microsoft.com/library/hh849800) e [Remove-Item](http://technet.microsoft.com/library/hh849765) cmdlets, conforme mostrado no exemplo seguinte:  

    ```  
    Get-ChildItem “DS002:\Operating Systems\Windows 7” –recurse | Remove-Item –recurse –force  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell devolvido no passo 3.  

5.  Copie o conteúdo dos ficheiros de origem do sistema operativo que têm o pacote de serviço integrado com o [Copy-Item](http://technet.microsoft.com/library/hh849793) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Copy-Item "E:\*" -Destination "DS002:\Operating Systems\Windows 7"-Recurse -Force  
    ```  

     Neste exemplo, os ficheiros de origem do sistema operativo estão numa unidade I, e *DS002:* é o nome de uma unidade do Windows PowerShell devolvido no passo 3.  

6.  Atualizar qualquer suporte de dados de implementação do MDT com base na partilha de implementação utilizando **atualização MDTMedia** cmdlet.  

 Para obter mais informações sobre como atualizar o suporte de dados de implementação MDT com base na implementação partilhar utilizando **atualização MDTMedia** cmdlet, consulte [atualizar a implementação de suportes de dados utilizando o Windows PowerShell](#UpdateDeployMedia).  

###  <a name="AutomateAppUsingRef"></a> Automatizar a aplicação dos pacotes de serviço do sistema operativo através de um computador de referência e o Windows PowerShell  
 Pode automatizar o processo de atualização de pacotes de serviço do sistema operativo com o Windows PowerShell quando tiver apenas o pacote de serviço que ainda não estiver integrado com o sistema operativo, tais como ter a SP1 para Windows 7, ainda não integrado com uma imagem do Windows 7.  

 Para que este método, implemente o sistema operativo sem o service pack para um computador de referência. Em seguida, aplicar o service pack para o computador de referência. Em seguida, capture uma imagem de sistema operativo do computador de referência. Por fim, copie o ficheiro. wim capturado o ficheiro Install.wim no sistema operativo na partilha de implementação com o Windows PowerShell.  

 **Para automatizar a aplicação dos pacotes de serviço do sistema operativo do suporte de dados de origem das atualizações com o Windows PowerShell**  

1.  Implemente o sistema de operativo de destino para um computador de referência.  

     Para obter mais informações sobre como implementar um computador de referência, consulte os seguintes recursos no documento do MDT, *utilizar o Microsoft Deployment Toolkit*:  

    -   "Preparar a implementação LTI ao computador de referência"  

    -   "A implementar e capturar uma imagem do computador de referência na LTI"  

2.  Instale o pacote de serviço pretendido para o computador de referência.  

     Para obter mais informações sobre como instalar o service pack, consulte a documentação que acompanha o service pack.  

3.  Capturar uma imagem do computador de referência ao criar e implementar uma sequência de tarefas com base no **Sysprep e captura** modelo de sequência de tarefas.  

     Para obter mais informações sobre como criar uma sequência de tarefas com base no **Sysprep e captura** modelo de sequência de tarefas, consulte "Criar uma nova tarefa de sequência no Deployment Workbench".  

4.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [ao carregar o Snap-In do PowerShell do Windows MDT](#LoadMDTSnapIn).  

5.  Certifique-se de que as implementações do MDT que partilhem unidades do Windows PowerShell são restauradas com autoridade utilizando o **restauro MDTPersistentDrive** cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implementações do MDT que partilhem unidades do Windows PowerShell já forem restauradas, receberá uma mensagem de aviso que indica que o cmdlet não consegue restaurar a unidade.  

6.  Vista de lista de implementações do MDT partilhar unidades do Windows PowerShell, um para cada implementação partilhar, utilizando o [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista do Windows PowerShell unidades fornecidas a utilizar o MDTProvider estiver listadas, um para cada partilha de implementação.  

7.  Copie o ficheiro. wim capturado no passo 3 sobre o ficheiro Install.wim no sistema operativo da partilha de implementação utilizando o [Copy-Item](http://technet.microsoft.com/library/hh849793) cmdlet, conforme mostrado no exemplo seguinte:  

    ```  
    Copy-Item "DS002:\Captures\Win7SP1.wim" -Destination "DS002:\Operating Systems\Windows 7\sources\Install.wim" Force  
    ```  

     Neste exemplo, o ficheiro de imagem do sistema operativo capturada (Win7SP1.wim) na pasta na partilha de DS002 capturas: é o nome de uma unidade do Windows PowerShell devolvido no passo 6 e sistema operativo existente Windows 7 é armazenado na pasta denominada  *Windows 7*.  

8.  Atualizar qualquer suporte de dados de implementação do MDT com base na partilha de implementação utilizando **atualização MDTMedia** cmdlet.  

     Para obter mais informações sobre como atualizar o suporte de dados de implementação MDT com base na implementação partilhar utilizando **atualização MDTMedia** cmdlet, consulte [atualizar a implementação de suportes de dados utilizando o Windows PowerShell](#UpdateDeployMedia).  

## <a name="customizing-deployment-based-on-chassis-type"></a>Personalizar a implementação com base no tipo de Chassis  
 Pode personalizar a implementação com base no tipo de chassis do computador. Os scripts criar variáveis locais que podem ser processadas no ficheiro CustomSettings.ini. As variáveis locais `IsLaptop`, `IsDesktop`, e `IsServer` indicar se o computador é um computador portátil, o computador de secretária ou o servidor, respetivamente.  

> [!NOTE]
>  Em versões anteriores do Deployment Workbench, a `IsServer` sinalizador indicado que o sistema operativo existente é um sistema de operativo de servidor (por exemplo, o Windows Server 2003 Enterprise Edition). Este sinalizador foi mudado para `IsServerOS`.  

 **Para implementar as variáveis locais no ficheiro CustomSettings.ini**  

1.  No `[Settings]` na secção de `Priority` linha, adicionar uma secção personalizada para personalizar a implementação com base no tipo de chassis (`ByChassisType` no exemplo seguinte, onde *Chassis* representa o tipo de computador).  

2.  Criar a secção personalizada que corresponde à secção personalizada definida no passo 1 (`ByChassisType` no exemplo no exemplo seguinte, onde *Chassis* representa o tipo de computador).  

3.  Definir uma subsecção para cada tipo de chassis detetar (`Subsection=Laptop-%IsLaptop%, Subsection=Desktop-%IsDesktop%, Subsection=Server-%IsServer%` no exemplo seguinte).  

4.  Criar uma subsecção para cada `True` e `False` estado de cada subsecção definida no passo 3 (tais como `[Laptop-True], [Laptop-False], [Desktop-True], [Desktop-False]` no exemplo seguinte).  

5.  Em cada `True` e `False` subsecção, adicione as definições apropriadas com base no tipo de chassis.  

 **Listar 1. Exemplo de personalização a implementação com base no tipo de Chassis no ficheiro CustomSettings.ini**  

```  
[Settings]  

Priority=...,ByLaptopType,ByDesktopType,ByServerType  

[ByLaptopType]  
Subsection=Laptop-%IsLaptop%  

[ByDesktopType]  
Subsection=Desktop-%IsDesktop%  

[ByServerType]  
Subsection=Server-%IsServer%  
.  
.  
.  

[Laptop-True]  
.  
.  
.  

[Laptop-False]  
.  
.  
.  

[Desktop-True]  
.  
.  
.  

[Desktop-False]  
.  
.  
.  

[Server-True]  
.  
.  
.  

[Server-False]  
.  
.  
.  
```  

## <a name="deploying-applications-based-on-earlier-application-versions"></a>Implementar aplicações com base nas versões anteriores da aplicação  
 Muitas vezes, ao instalar um sistema operativo num computador existente, irá instalar as aplicações mesmas que anteriormente instalado no computador. Fazê-lo utilizando scripts do MDT (em especial, ZTIGather.wsf) para consultar duas origens diferentes de informações:  

-   **Funcionalidade de inventário de software do Configuration Manager.** Contém um registo para cada pacote de aplicação — neste caso, as listagens em programas e funcionalidades no Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 — instalado a última vez que o Configuration Manager inventariados o computador.  

-   **Uma tabela de mapeamento.** Descreve o pacote e programa tem de ser instalado para cada registo (porque os registos do programa e funcionalidades ou adicionar ou remover programas não especificam exatamente o pacote instalado a aplicação, impossibilitando selecionar automaticamente o pacote com base no inventário autónomo).  

 **Para efetuar uma instalação de aplicação específicos de computador dinâmica**  

1.  Utilize a tabela na base de dados MDT ligar pacotes específicas com as aplicações listadas no sistema operativo de destino.  

2.  Povoar a tabela com dados que associa o pacote adequado a aplicação listada no programa e funcionalidades ou adicionar ou remover programas.

     **Consulta SQL para preencher a tabela**  

    ```  
    use [MDTDB]  
    go  
    INSERT INTO [PackageMapping] (ARPName, Packages) VALUES('Office12.0', 'XXX0000F:Install Office 2010 Professional Plus')  
    go  
    ```  

     A linha inserida liga-se em qualquer computador que tenha a entrada `Office12.0` com o Microsoft Office 2010 Professional Plus do pacote.  

     Isto significa que o Microsoft Office 2010 Professional Plus irá ser instalado em qualquer computador atualmente com o sistema do Microsoft Office 2007 (Office 12.0). Adicione entradas semelhantes para outros pacotes. Qualquer item para que não há nenhuma entrada é ignorada (nenhum pacote será instalada).  

3.  Crie um procedimento armazenado para simplificar a associar as informações na tabela de novo com os dados de inventário.  

    ```  
    use [MDTDB]  
    go  

    if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[RetrievePackages]') and OBJECTPROPERTY(id, N'IsProcedure') = 1)  
    drop procedure [dbo].[RetrievePackages]  
    go  

    CREATE PROCEDURE [dbo].[RetrievePackages]  
    @MacAddress CHAR(17)  
    AS  

    SET NOCOUNT ON  

    /* Select and return all the appropriate records based on current inventory */  
    SELECT * FROM PackageMapping  
    WHERE ARPName IN  
    (  
      SELECT ProdID0 FROM CM_DB.dbo.v_GS_ADD_REMOVE_PROGRAMS a, CM_DB.dbo.v_GS_NETWORK_ADAPTER n  
      WHERE a.ResourceID = n.ResourceID AND  
      MACAddress0 = @MacAddress  
    )  
    go  
    ```  

     O procedimento armazenado no exemplo que precede parte do princípio de que a base de dados do site primário central do Configuration Manager reside no computador no qual o SQL Server está em execução como a BD do MDT. Se a base de dados do site primário central reside num computador diferente, as modificações adequadas tem de ser efetuadas para o procedimento armazenado. Além disso, o nome da base de dados (`CM_DB`) têm de ser atualizados. Considere também a concessão de permissões de acesso de leitura de contas adicionais para o **v_GS_ADD_REMOVE_PROGRAMS** vista na base de dados do Configuration Manager.  

4.  Configurar o ficheiro CustomSettings.ini para consultar esta tabela da base de dados, especificando o nome de uma secção (`[DynamicPackages]` no **prioridade** lista) que aponta para as informações da base de dados.  

    ```  
    [Settings]  
    …  
    Priority=MacAddress, DefaultGateway, DynamicPackages, Default  
    …  
    ```  

5.  Criar um `[DynamicPackages]` secção para especificar o nome de uma secção de base de dados.  

    ```  
    [DynamicPackages]  
    SQLDefault=DB_DynamicPackages  
    ```  

6.  Crie uma secção de base de dados para especificar os detalhes de informações e consulta de base de dados.  

    ```  
    [DB_DynamicPackages]  
    SQLServer=SERVER1  
    Database=MDTDB  
    StoredProcedure=RetrievePackages  
    Parameters=MacAddress  
    SQLShare=Logs  
    Instance=SQLEnterprise2005  
    Port=1433  
    Netlib=DBNMPNTW  
    ```  

     No exemplo que precede, a BD do MDT com o nome *MDTDB* no computador que executa o SQL Server instanced com o nome *servidor1* irá ser consultado. A base de dados contém um procedimento armazenado com o nome `RetrievePackages` (criada no passo 3).  

 Quando ZTIGather.wsf for executada, uma linguagem SQL (Structured Query) `SELECT` instrução é gerada automaticamente e o valor do **MakeModelQuery** chave personalizada é transmitida como um parâmetro para a consulta:  

 ```  
 EXECUTE RetrievePackages ?  
 ```  

 O valor real do **MACAddress** chave personalizada será substituída pelos correspondente "?".  Esta consulta devolve um conjunto de registos com as linhas que introduziu no passo 2.  

 Um número de argumentos variável não pode ser transmitido para um procedimento armazenado. Como resultado, quando um computador tiver mais do que um endereço MAC, nem todos os endereços MAC podem ser passados para o procedimento armazenado. Como alternativa, substitua o procedimento armazenado com uma vista que lhe permite consultar a vista com uma `SELECT` instrução com uma `IN` cláusula passar todos os valores de endereço MAC.  

 Com base no cenário apresentado aqui, se o computador atual tem o valor `Office12.0` inseridos na tabela (passo 2), é devolvida uma linha (`XXX0000F:Install Office 2010 Professional Plus`). Isto indica que esse pacote que xxx0000f:Install Office 2001 Professional Plus será instalada pelo processo de ZTI durante a fase de restauro de estado.  

## <a name="fully-automated-lti-deployment-scenario"></a>Cenário de implementação LTI totalmente automatizado  
 O objetivo principal de LTI é automatizar o processo de implementação quanto possível. Embora ZTI fornece a automatização da implementação completa a utilizar os scripts de MDT e serviços de implementação do Windows, LTI foi concebida para funcionar com menos requisitos de infraestrutura.  

 Pode automatizar o Assistente de implementação do Windows utilizadas no processo de implementação LTI para reduzir (ou eliminar) as páginas do assistente apresentadas. Pode ignorar o Assistente de implementação completa do Windows, especificando o **SkipWizard** propriedade no CustomSettings.ini. Para ignorar as páginas do assistente individuais, utilize as seguintes propriedades:  

-   **SkipAdminPassword**  

-   **SkipApplications**  

-   **SkipBDDWelcome**  

-   **SkipBitLocker**  

-   **SkipBitLockerDetails**  

-   **SkipTaskSequence**  

-   **SkipCapture**  

-   **SkipComputerBackup**  

-   **SkipComputerName**  

-   **SkipDomainMembership**  

-   **SkipFinalSummary**  

-   **SkipLocaleSelection**  

-   **SkipPackageDisplay**  

-   **SkipProductKey**  

-   **SkipSummary**  

-   **SkipTimeZone**  

-   **SkipUserData**  

Para obter mais informações sobre estas propriedades individuais, consulte a propriedade correspondente no documento MDT *Toolkit referência*.  

Para cada página do assistente foi ignorada, forneça os valores para as propriedades correspondentes que normalmente são recolhidas através de página do assistente nos ficheiros de CustomSettings.ini e BootStrap.ini. Para obter mais informações sobre as propriedades que devem ser configurados nestes ficheiros, consulte a secção "Fornecer propriedades para ignorada implementação páginas do assistente", no documento MDT *Toolkit referência*.  

## <a name="fully-automated-lti-deployment-for-a-refresh-computer-scenario"></a>Implementação LTI totalmente automatizado para um cenário de computador de atualização  
 O seguinte ilustra um ficheiro CustomSettings.ini utilizado para um cenário de atualizar o computador para ignorar todas as páginas do Assistente de implementação do Windows. Neste exemplo, as propriedades para fornecer quando a ignorar a página do assistente são imediatamente abaixo da propriedade que ignora a página do assistente.  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  
SkipCapture=YES  
SkipAdminPassword=YES  
SkipProductKey=YES  

DeploymentType=REFRESH  

SkipDomainMembership=YES  
JoinDomain=DomainName  
DomainAdmin=Administrator  
DomainAdminDomain=DomainName  
DomainAdminPassword=a_secure_password  

SkipUserData=yes  
UserDataLocation=AUTO  
UDShare=\\Servername\Sharename\Directory  
UDDir=%ComputerName%  

SkipComputerBackup=YES  
ComputerBackuplocation=AUTO  
BackupShare=\\Servername\Backupsharename  
BackupDir=%ComputerName%  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%ComputerName%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  
UserID=Administrator  
UserDomain=DomainName  
UserPassword=P@ssw0rd  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=DomainName\Username  
```  

## <a name="fully-automated-lti-deployment-for-a-new-computer-scenario"></a>Implementação LTI totalmente automatizado para um novo cenário de computador  
 Segue-se um exemplo de um ficheiro CustomSettings.ini utilizado para um cenário novo computador para ignorar todas as páginas do Assistente de implementação do Windows. Neste exemplo, as propriedades para fornecer quando a ignorar a página do assistente são imediatamente abaixo da propriedade que ignora a página do assistente.  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  

SkipCapture=YES  
ComputerBackupLocation=\\WDG-MDT-01\Backup$\  
BackupFile=MyCustomImage.wim  

SkipAdminPassword=YES  
SkipProductKey=YES  

SkipDomainMembership=YES  
JoinDomain=WOODGROVEBANK  
DomainAdmin=Administrator  
DomainAdminDomain=WOODGROVEBANK  
DomainAdminPassword=P@ssw0rd  

SkipUserData=Yes  
UserDataLocation=\\WDG-MDT-01\UserData$\Directory\usmtdata  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%SerialNumber%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=WOODGROVEBANK\PilarA  
CaptureGroups=YES  
SLShare=\\WDG-MDT-01\UserData$\Logs  
Home_page=http://www.microsoft.com/NewComputer  
```  

## <a name="calling-web-services-in-mdt"></a>Serviços Web de chamar no MDT  
 Em versões anteriores do MDT, processamento de regras foi suportadas através de bases de dados, do qual foi possível obter os valores do computador local e CustomSettings.ini — normalmente, através do WMI — para tomar decisões que necessários ser efetuada em cada computador durante a implementação. Além disso, foi possível efetuar as consultas SQL e chamadas de procedimento armazenado para obter informações adicionais de bases de dados externas. Ocorreram desafios com esse abordagem, embora — especialmente com efetuar ligações seguras do SQL Server.  

 Para solucionar este problema, o MDT tem capacidade para efetuar chamadas de serviço web com base nas regras simples definidas no CustomSettings.ini. Estes pedidos de serviço web não requerem qualquer contexto de segurança especial e podem utilizar qualquer porta de TCP/IP é necessária para simplificar as configurações de firewall.  

 O seguinte mostra como configurar CustomSettings.ini para chamar um serviço web específico. Neste cenário, o serviço web é escolhido aleatoriamente de uma pesquisa na Internet. Esta utiliza um código postal como entrada e devolve a cidade, o estado, o indicativo e o fuso horário (como uma letra) para o código postal especificado.  

```  
[Settings]  
Priority=Default, USZipService  
Properties=USZip, City, State, Zip, Area_Code, Time_Zones   
[Default]  
USZip=98052   
[USZipService]  
WebService=http://www.webservicex.net/uszip.asmx/GetInfoByZIP  
Parameters=USZip  
```  

 Executar este código produz o resultado semelhante ao seguinte:
```  
Added new custom property USZIP  
Added new custom property CITY  
Added new custom property STATE  
Added new custom property ZIP  
Added new custom property AREA_CODE  
Added new custom property TIME_ZONES  
Using from [Settings]: Rule Priority = DEFAULT, USZIPSERVICE  
------ Processing the [DEFAULT] section ------  
Property USZIP is now = 98052  
Using from [DEFAULT]: USZIP = 98052  
------ Processing the [USZIPSERVICE] section ------  
Using COMMAND LINE ARG: Ini file = CustomSettings.ini  
CHECKING the [USZIPSERVICE] section  
About to execute web service call to http://www.webservicex.net/uszip.asmx/GetInfoByZIP: USZip=98052  
Response from web service: 200 OK  
Successfully executed the web service.  
Property CITY is now = Redmond  
Obtained CITY value from web service:  CITY = Redmond  
Property STATE is now = WA  
Obtained STATE value from web service:  STATE = WA  
Property ZIP is now = 98052  
Obtained ZIP value from web service:  ZIP = 98052  
Property AREA_CODE is now = 425  
Obtained AREA_CODE value from web service:  AREA_CODE = 425  
------ Done processing CustomSettings.ini ------  
```  

 Existem alguns complicações secundárias para observar durante a execução de um serviço web:  

-   Não fazer nada, uma especial com os servidores de proxy. Se existir um proxy anónimo presente, utilizá-la, mas autenticar proxies possa provocar problemas. Na maioria dos casos, um serviço web não será chamado.  

-   CustomSettings.ini ou ZTIGather.xml procura as propriedades definidas na marcação de XML devolvida como resultado da chamada de serviço web (tal como com uma consulta de base de dados ou outra regra). No entanto, a pesquisa XML é sensível às maiúsculas e minúsculas. Felizmente, o serviço web, descrito aqui devolve todos os nomes de propriedade em maiúsculas, que é o que espera ZTIGather.xml. É possível remapear entradas em minúsculas ou caso misto, para contornar esta.  

-   A `POST` pedido para o serviço web é recomendado, pelo que a chamada de serviço web deve ser capaz de suportar um `POST`.  

## <a name="connecting-to-network-resources"></a>Ligar a recursos de rede  
 Durante os processos de implementação LTI e ZTI, poderá necessitar de acesso a um recurso de rede num servidor diferente do servidor que aloja a partilha de implementação. Tem de ser autenticado no outro servidor para que possam aceder pastas partilhadas ou serviços não existe. Por exemplo, pode instalar uma aplicação de uma pasta partilhada num servidor diferente do servidor que aloja a partilha de implementação que utilizam os scripts do MDT.  

> [!NOTE]
>  Para consultar as bases de dados do SQL Server alojadas num servidor diferente do servidor que aloja a partilha de implementação, consulte o **base de dados**, **DBID**, **DBPwd**, **instância** , **NetLib**, **ordem**, **parâmetros**, **ParameterCondition**, **SQLServer** , **SQLShare**, e **tabela** propriedades no documento MDT *Toolkit referência*.  

 Utilizar o script de ZTIConnect.wsf, pode ligar a outros servidores e aceder a recursos nos mesmos. A sintaxe para o script de ZTIConnect.wsf é o seguinte (onde *unc_path* é um caminho de convenção de Nomenclatura Universal [UNC] para ligar ao servidor):  

```  
Cscript.exe “%SCRIPTROOT%\ZTIConnect.wsf” /uncpath:unc_path  
```  

 Na maioria dos casos, execute o script de ZTIConnect.wsf como uma tarefa do sequenciador de tarefas. Execute o script de ZTIConnect.wsf antes de tarefas que necessitam de acesso a um servidor diferente do servidor que aloja a partilha de implementação.  

 **Para adicionar o script de ZTIConnect.wsf como uma tarefa para a sequência de tarefas de compilação**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share*/Task sequências (onde *deployment_share* é o nome da partilha de implementação para configurar ).  

3.  No painel de detalhes, clique em ***task_sequence*** (onde *task_sequence* é a sequência de tarefas para modificar).  

4.  No painel ações, clique em **propriedades**.  

5.  Clique no separador de sequência de tarefas, navegue para **grupo** (onde *grupo* é o grupo no qual pretende executar o script de ZTIConnec.wsf) e clique em **adicionar**. Clique em **geral**e, em seguida, clique em **executar linha de comandos**.  

    > [!NOTE]
    >  Adicione a tarefa antes de adicionar quaisquer tarefas que necessitam de acesso a recursos no servidor de destino.  

6.  Concluir o **propriedades** separador da tarefa de novo com as seguintes informações:

    |**Nesta caixa** |**Fazê-lo** |  
    |-|-|  
    |**Nome** |Tipo **ligar ao servidor** (onde o servidor é o nome do servidor ao qual pretende ligar).|  
    |**Descrição** |Digite um texto que explica por que razão a ligação tem de ser efetuadas.|  
    |**Comando** |Tipo **Cscript.exe "% SCRIPTROOT%\ZTIConnect.wsf" /uncpath:unc_path** (onde *unc_path* é o caminho UNC para uma pasta partilhada no servidor).|  

7.  Concluir o **opções** separador da tarefa de novo com as informações seguintes. A menos que especificado, aceite os valores predefinidos e, em seguida, clique em **OK**.  

    |**Nesta caixa** |**Fazê-lo** |  
    |-|-|  
    |**Códigos de êxito** |Tipo **0 3010**. (O script de ZTIConnect.wsf devolve estes códigos após a conclusão com êxito.)|  
    |**Caixa de lista de condições** |Adicione quaisquer condições que poderão ser necessárias. (Na maioria das instâncias esta tarefa não requer nenhum condições.)|  

 Depois de adicionar a tarefa que irão executar o script de ZTIConnect.wsf, as tarefas subsequentes podem aceder a recursos de rede no servidor especificado no **/uncpath** opção do ZTIConnect.wsf script.  

## <a name="deploying-the-correct-device-drivers-to-computers-with-the-same-hardware-devices-but-different-make-and-model"></a>Implementar os controladores de dispositivo correto para computadores com o mesmo dispositivos de Hardware, mas a diferentes marca e o modelo  
 Podem existir variações no nomes e números de modelo com virtualmente nenhuma diferença no conjunto de controlador. Essas variações nos nomes e números de modelo, desnecessariamente, podem aumentar o tempo despendido efetuar várias entradas de base de dados de um modelo específico. O procedimento seguinte mostra como definir uma nova propriedade através de uma chamada de função de saída de utilizador que devolve uma subcadeia do número de modelo.  

 **Para criar aliases de modelo**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share* (onde *deployment_share* é o nome da partilha de implementação para configurar).  

3.  No painel ações, clique em **propriedades**.  

4.  No **propriedades** caixa de diálogo, clique em de **regras** separador.  

5.  Crie alias para tipos de hardware a marca e modelo secções da base de dados do MDT. Truncar o tipo de modelo em parêntesis abrir "(" no nome do modelo. Por exemplo, *HP DL360 (G112)* fica *HP DL360*.  

6.  Adicione a variável personalizada **ModelAlias** para cada secção.  

7.  Crie um novo `[SetModel]` secção.  

8.  Adicionar o `[SetModel]` secção para o **prioridade** definições no `[Settings]` secção.  

9. Adicionar uma linha para o `ModelAlias` secção referir-se a um script de saída de utilizador que será truncar o nome do modelo no "(".  

10. Criar um **MMApplications** pesquisa de base de dados onde **ModelAlias** é igual ao **modelo**.  

11. Criar um script de saída de utilizador e colocá-lo no mesmo diretório do ficheiro CustomSettings.ini para truncar o nome do modelo.  

    O seguinte mostra que um CustomSettings.ini e o utilizador saia script, respetivamente.  

     **CustomSettings.ini**:  

    ```  
    [Settings]   
    Priority=SetModel, MMApplications, Default   
    Properties= ModelAlias   
    [SetModel]   
    ModelAlias=#SetModelAlias()#   
    Userexit=Userexit.vbs   
    [MMApplications]   
    SQLServer=Server1  
    Database=MDTDB   
    Netlib=DBNMPNTW   
    SQLShare=logs   
    Table= MakeModelSettings    
    Parameters=Make, ModelAlias   
    ModelAlias=Model   
    Order=Sequence  
    ```  

     **Script de saída do utilizador**:  

    ```  
    Function UserExit(sType, sWhen, sDetail, bSkip)   
      UserExit = Success   
    End Function   

    Function SetModelAlias()   
      If Instr(oEnvironment.Item("Model"), "(") <> 0 Then   
        SetModelAlias = Left(oEnvironment.Item("Model"), _  
                          Instr(oEnvironment.Item("Model"), _  
                            "(") - 1)   
        oLogging.CreateEntry "USEREXIT – " & _  
          "ModelAlias has been set to " & SetModelAlias, _  
          LogTypeInfo  
      Else   
        SetModelAlias = oEnvironment.Item("Model")   
        oLogging.CreateEntry " USEREXIT - " & _  
          "ModelAlias has not been changed.", LogTypeInfo   
      End if   
    End Function  
    ```  

## <a name="configuring-conditional-task-sequence-steps"></a>Passos de sequência de tarefas condicional a configurar  
 Em alguns cenários, considere executar um passo de sequência de tarefas condicionalmente com base nos critérios definidos. As combinações destas condições podem ser adicionadas para determinar se deve ser executado o passo de sequência de tarefas. Por exemplo, utilize o valor da variável de sequência de tarefas e o valor de uma definição de registo para determinar se um passo de sequência de tarefas deve ser executado.  

 Com o MDT, execute uma sequência de tarefas condicionalmente com base na:  

-   Um ou mais **se** instruções  

-   Uma variável de sequência de tarefas  

-   A versão do sistema operativo de destino  

-   Os resultados booleanos de uma consulta WMI  

-   Uma definição de registo  

-   O software instalado no computador de destino  

-   As propriedades de uma pasta  

-   As propriedades de um ficheiro  

### <a name="configuring-a-conditional-task-sequence-step"></a>Configurar um passo de sequência de tarefas condicional  
 Passos de sequência de tarefas condicional são configurados no Deployment Workbench, no **opções** separador de um passo de sequência de tarefas. Pode adicionar uma ou mais condições para o passo de sequência de tarefas para criar a condição apropriada para em execução ou não ser executado o passo.  

> [!NOTE]
>  Tem, pelo menos, um de cada passo de sequência de tarefas condicional **se** instrução.  

 **Para ver o separador Opções do passo de sequência de tarefas**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share*/Task sequências (onde *deployment_share* é o nome da partilha de implementação para configurar ).  

3.  No painel de detalhes, clique em **task_sequence** (onde *task_sequence* é o nome da sequência de tarefas para configurar).  

4.  No painel ações, clique em **propriedades**.  

5.  No ***task_sequence*** **propriedades** caixa de diálogo a **sequência de tarefas** separador, clique em ***passo*** (onde *passo* é o nome do passo de sequência de tarefas para configurar) e, em seguida, clique em de **opções** separador.  

 No **opções** separador do passo de sequência de tarefas, efetuar as seguintes ações:  

-   **Adicione.** Clique neste botão para adicionar uma condição para o passo de sequência de tarefas.  

-   **Remova.** Clique neste botão para remover uma condição existente no passo de sequência de tarefas.  

-   **Edite.** Clique neste botão para modificar uma condição existente no passo de sequência de tarefas.  

### <a name="if-statements-in-conditions"></a>Se as instruções em condições  
 Todas as condições de sequência de tarefas incluem um ou mais **se** instruções. **Se** instruções são a base para a criação de passos de sequência de tarefas condicional. Uma condição de passo de sequência de tarefas pode incluir apenas um **se** declaração, mas vários **se** instruções podem ser aninhadas abaixo de nível superior **se** instrução para criar mais complexas condições.  

 Um **se** pode basear-se nas condições listadas na tabela a seguir, são configurados na instrução o **propriedades da declaração se** caixa de diálogo.  

 |**Condição** |**Selecione esta opção para executar a sequência de tarefas se** |  
 |-|-|  
 |**Todas as condições** |Todas as condições sob este **se** instrução tem de ser verdadeira.|  
 |**Quaisquer condições** |Todas as condições sob este **se** instrução são verdadeiras.|  
 |**Nenhum** |Nenhum as condições sob este **se** instrução são verdadeiras.|  

 Conclua a condição para executar o passo de sequência de tarefas adicionando outros critérios para as condições (por exemplo, as variáveis de sequência de tarefas ou valores de uma definição de registo).  

 **Para adicionar uma condição de instrução se a um passo de sequência de tarefas**  

1.  No ***passo*** **opção** separador (onde *passo* é o nome do passo de sequência de tarefas para configurar), clique em **adicionar**e, em seguida, clique em **Se instrução**.  

2.  No **se propriedades da declaração** caixa de diálogo, clique em **condição** (onde *condição* é uma das condições listada na tabela anterior) e, em seguida, clique em **OK**.  

### <a name="task-sequence-variables-in-conditions"></a>Variáveis de sequência de tarefas em condições  
 Utilize o **variável de sequência de tarefas** condição para avaliar quaisquer variável de sequência de tarefas criada por uma **definir variável da sequência de tarefas** tarefa ou por quaisquer tarefas na sequência de tarefas. Por exemplo, considere uma rede que contenha os computadores de cliente do Windows XP que fazem parte de um domínio e algumas que estão num grupo de trabalho. Saber que a política de domínio atual força todas as definições de utilizador guardados na rede, as definições de utilizador poderão ter de ser guardado apenas para computadores que não fazem parte do domínio — ou seja, os computadores que estejam no grupo de trabalho. Esse caso, adicione uma condição para a **capturar ficheiros do utilizador e definições** tarefas que tenha como destino os computadores no grupo de trabalho.  

 **Para adicionar uma condição com base na variável de sequência de tarefas**  

1.  No ***passo*** **opções** separador (onde *passo* é o nome do passo de sequência de tarefas para configurar), clique em **adicionar condição**e, em seguida, clique em **Variável de sequência de tarefas**.  

2.  No **Task Sequence Variable** condições caixa de diálogo, o **variável** caixa, escreva **OSDJoinType**.  

    > [!NOTE]
    >  Esta variável é definida como **0** para computadores que estão associados a um domínio e a **1** os num grupo de trabalho.  

3.  No **condição** , clique em **igual**.  

4.  No **valor** caixa, escreva **1**e, em seguida, clique em **OK**.  

### <a name="operating-system-version-in-conditions"></a>Versão do sistema operativo em condições  
 Utilize o **versão do sistema operativo** condição para verificar a versão do sistema operativo existente de um computador de destino ou o cliente existente (ao capturar uma imagem). Por exemplo, considere uma rede que contém vários servidores que serão atualizados do Windows Server 2003 para o Windows Server 2008. As definições de rede devem ser copiadas e aplicadas apenas aos servidores que executam o Windows Server 2003. Todos os outros servidores terão as predefinições de rede que utiliza o Windows Server 2008.  

 **Para adicionar uma condição com base na versão do sistema operativo**  

1.  Clique no Editor de sequência de tarefas, o **capturar definições de rede** tarefas.  

2.  Clique em **adicionar condição**e, em seguida, clique em **versão do sistema operativo**.  

3.  No **arquitetura** caixa, clique no servidor relevante. Neste exemplo, clique em **x86**.  

4.  No **sistema operativo** , clique em sistema operativo e versão para o qual pretende definir uma condição. Neste exemplo, clique em **x86 Windows 2003**.  

5.  No **condição** caixa, clique a condição relevante e, em seguida, clique em **OK**.  

### <a name="file-properties-in-conditions"></a>Propriedades do ficheiro em condições  
 Utilize o **propriedades do ficheiro** condição para verificar a versão e/ou vezes tamp de um determinado ficheiro para determinar se deve ou não esteja a executar uma tarefa ou um grupo de tarefas. Neste exemplo, o ambiente de produção contém uma imagem do Windows Server 2003 é constantemente atualizada e utilizada para cada novo servidor que é adicionado à rede. Todos os computadores de servidor no ambiente de executarem uma aplicação personalizada que necessite de interface de programação da aplicação (API) versão 3.60.6815 de objeto de acesso digitais (DAO).  

 Todos os servidores existentes estão a funcionar corretamente. No entanto, a cada novo servidor que foi adicionado à rede com a imagem não é possível executar a aplicação. Porque é da responsabilidade de um grupo diferente para manter e atualizar imagens, decidir que a sequência de tarefas de implementação ser alterado para instalar a versão relevante do DAO se a versão existente do DAO implementada com a imagem está incorreta.  

 **Para adicionar propriedades de um ficheiro de condição de uma sequência de tarefas passo no Configuration Manager 2007 R3**  

1.  No Configuration Manager 2007 R3, crie um pacote para instalar DAO 3.60.6815. Este pacote de chamar *DAO*, com um programa designado *InstallDAO*. Para saber mais sobre a criação de pacotes, consulte [como criar um pacote](http://technet.microsoft.com/library/bb693627.aspx).  

2.  Criar um **instalar Software** passo para implementar o pacote DAO.  

3.  Clique em de **instalar Software** criado no passo 2 de passo de sequência de tarefas e, em seguida, clique em de **opções** separador.  

4.  Clique em **adicionar condição**e, em seguida, clique em **propriedades do ficheiro**.  

5.  No **caminho** caixa, escreva **C:\Program Files\Microsoft Shared\DAO\dao360.dll**.  

6.  Selecione o **verificar a versão** caixa de verificação e, em seguida, clique em **não é igual a** para a condição.  

7.  No **versão** caixa, escreva **3.60.6815**.  

8.  Neste caso, limpar o **Verifique o carimbo** caixa de verificação e, em seguida, clique em **OK**.  

### <a name="folder-properties-in-conditions"></a>Propriedades da pasta nas condições  
 Utilize o **as propriedades da pasta** condição para verificar o carimbo de hora de uma determinada pasta para determinar se deve executar uma tarefa ou um grupo de tarefas. Por exemplo, considere uma situação em que uma aplicação desenvolvida internamente foi atualizada para funcionar com o Windows 8. No entanto, nem todos os computadores na rede tem a versão mais recente da aplicação instalada e tem de efetuar um processo de conversão de dados antes de poder atualizar a aplicação.  

 Se o carimbo de hora da pasta na qual a aplicação é instalada é 31/12/2007 ou anterior, o computador de destino está a executar a versão incompatível da aplicação e o utilizador deve executar o processo de conversão de dados no computador de destino. Condicionalmente, execute um passo de sequência de tarefas para executar o processo de conversão de dados em computadores que tenham uma versão anterior da aplicação.  

 **Para adicionar uma condição de propriedades da pasta para um passo de sequência de tarefas**  

1.  Na consola do Configuration Manager ou no Deployment Workbench, no editor de sequência de tarefas, edite ***task_sequence*** (onde *sequência de tarefas* é a sequência de tarefas que pretende editar).  

2.  Criar um **linha de comandos** tarefas para executar o processo de conversão de dados.  

3.  Clique na tarefa criada no passo 1.  

4.  Clique em **adicionar condição**e, em seguida, clique em **as propriedades da pasta**.  

5.  No **caminho** caixa, escreva o caminho da pasta que contém a aplicação.  

6.  Selecione o **Verifique o carimbo** caixa de verificação.  

7.  Clique em **menor que ou igual a** para a condição.  

8.  No **data** , clique em **31/12/2007**.  

9. No **tempo** , clique em **12:00:00: 00**e, em seguida, clique em **OK**.  

### <a name="registry-settings-in-conditions"></a>Definições de registo em condições  
 Utilize o **definição de registo** condição para verificar a existência de chaves e valores de registo e a correspondente aos dados armazenado valores de registo. Por exemplo, considere o caso em que uma aplicação atualmente a ser utilizada num pequeno conjunto de computadores não é possível executar no Windows 8 e uma implementação do Windows 8 no local para atualizar computadores atualmente com o Windows XP. Crie uma condição na tarefa relativo ao primeiro numa sequência para verificar o registo para uma entrada para a aplicação incompatível e interromper o processo de implementação para esse computador se for encontrado.  

 **Para adicionar uma condição de definição de registo para um passo de sequência de tarefas**  

1.  Na consola do Configuration Manager ou no Deployment Workbench, no editor de sequência de tarefas, edite ***task_sequence*** (onde *sequência de tarefas* é a sequência de tarefas que implementa o Windows 8).  

2.  Clicar na primeira tarefa na sequência e, em seguida, clique o **opções** separador.  

3.  Clique em **adicionar condição**e, em seguida, clique em **definição de registo**.  

4.  No **chave de raiz** lista, clique em **HKEY_LOCAL_MACHINE**.  

5.  No **chave** caixa, escreva **SOFTWARE\WOODGROVE**.  

6.  Clique em **não existe** para a condição. Neste caso, a tarefa será executada e continuar a sequência apenas se a chave não existe.  

7.  Opcionalmente, a condição foi possível procurar a não existência de um valor se digitou o nome do valor de **nome do valor** caixa.  

8.  Se uma condição diferente **existe/não existe** foi utilizado, especifique um valor e o tipo de valor.  

9. Clique em **OK**.  

### <a name="wmi-queries-in-conditions"></a>Consultas do WMI em condições  
 Utilize o **consulta de WMI** condição para executar qualquer consulta WMI. A condição é avaliada como True se a consulta devolver pelo menos um resultado. Por exemplo, considere o que necessita de uma equipa de implementação para atualizar o sistema operativo de todos os servidores de um modelo específico — Dell 1950, para a instância. Pode utilizar uma consulta WMI para verificar o modelo de cada computador e continuar com a implementação só se encontra-se o modelo à direita.  

 **Para adicionar uma condição de consulta de WMI para um passo de sequência de tarefas**  

1.  Na consola do Configuration Manager ou no Deployment Workbench, no editor de sequência de tarefas, edite ***task_sequence*** (onde *sequência de tarefas* é a sequência de tarefas que irá atualizar os servidores).  

2.  Clicar na primeira tarefa na sequência e, em seguida, clique o **opções** separador.  

3.  Clique em **adicionar condição**e, em seguida, clique em **consulta WMI**.  

4.  No **espaço de nomes WMI** caixa, escreva **root\cimv2**.  

5.  No **consulta WQL** caixa, escreva **selecione \* de Win32_ComputerSystem onde modelo como "% Dell % % 1950%"**. Clique em **OK**.  

### <a name="installed-software-in-conditions"></a>O Software instalado em condições  
 Utilize um **instalado Software** condição para verificar se uma parte específica do software está atualmente instalada num computador de destino. Apenas o software instalado com ficheiros do Microsoft Installer (MSI) pode ser avaliado com esta condição. Por exemplo, imagine que pretende atualizar o sistema operativo de todos os servidores exceto aos que estão a executar o Microsoft SQL Server 2012.  

 **Para adicionar uma condição de Software instalado para um passo de sequência de tarefas**  

1.  Na consola do Configuration Manager ou no Deployment Workbench, no editor de sequência de tarefas, edite ***task_sequence*** (onde *sequência de tarefas* é a sequência de tarefas que irá atualizar os servidores).  

2.  Clicar na primeira tarefa na sequência e, em seguida, clique o **opções** separador.  

3.  Clique em **adicionar condição**e, em seguida, clique em **instalado Software**.  

4.  Clique em **procurar**e, em seguida, clique em ficheiro MSI para SQL Server 2012.  

5.  Selecione o **corresponder a este produto específico** caixa de verificação para especificar que apenas os computadores com SQL Server 2012 e não quaisquer outras versões são os computadores de destino deve detetar esta consulta.  

6.  Clique em **OK**.  

### <a name="complex-conditions"></a>Condições complexas  
 Várias condições podem ser agrupadas utilizando **se** instruções para criar condições complexas. Por exemplo, imagine um determinado passo deve ser executado apenas para computadores de Contoso 1950 com o Windows Server 2003 ou Windows Server 2008. Escritos como um programático **se** declaração, seria ter um aspeto semelhante ao seguinte:  

```  
IF ((Computer Model IS “Contoso 1950”) AND (operating system=2003 OR operating system=2008))  
```  

 **Para adicionar uma condição complexa**  

1.  Na consola do Configuration Manager ou no Deployment Workbench, no editor de sequência de tarefas, edite ***task_sequence*** (onde *sequência de tarefas* é a sequência de tarefas que irá atualizar os servidores).  

2.  Clique no passo de sequência de tarefas para o qual pretende adicionar a condição e, em seguida, clique o **opções** separador.  

3.  Clique em **adicionar condição**, clique em **instrução se**e, em seguida, clique em **todas as condições**. Clique em **OK**.  

4.  Clique a declaração de condição, clique em **adicionar condição**e, em seguida, clique em **consulta de WMI**.  

5.  Certifique-se **root\cimv2** está especificado como o espaço de nomes WMI e, em seguida, no **consulta WQL** caixa, escreva **SELECIONE \* de Win32_ComputerSystem onde ComputerModel como "% % de Contoso % de 1950 "**. Clique em **OK**.  

6.  Clique em de **se** declaração e, em seguida, clique em **adicionar condição**. Clique em **se instrução**e, em seguida, clique em **qualquer condição**. Clique em **OK**.  

7.  Clique no segundo **se** instrução. Clique em **adicionar condição**e, em seguida, clique em **versão do sistema operativo**.  

8.  No **arquitetura** , clique na arquitetura para os servidores. Neste exemplo, clique em **x86**.  

9. No **sistema operativo** , clique em sistema operativo e versão. Neste exemplo, clique em **x86 Windows 2003 original versão**. Clique em **OK**.  

10. Clique no segundo **se** instrução. Clique em **adicionar condição**e, em seguida, clique em **versão do sistema operativo**.  

11. No **arquitetura** , clique na arquitetura para os servidores. Neste exemplo, clique em **x86**.  

12. No **sistema operativo** , clique em sistema operativo e versão. Neste exemplo, clique em **x86 Windows 2008 original versão**. Clique em **OK**.  

## <a name="creating-a-highly-scalable-lti-deployment-infrastructure"></a>Criação de uma infraestrutura de implementação LTI altamente dimensionável  
 Neste cenário, nenhuma distribuição de software eletrónicas está disponível para a infraestrutura de implementação para tirar partido, para utilizar o MDT para criar uma infraestrutura de implementação LTI totalmente automatizada. A infraestrutura LTI escalável utiliza o SQL Server, serviços de implementação do Windows e tecnologias do Windows Server 2003 ficheiro replicação do sistema distribuído (DFS-R).  

 Dimensione a infraestrutura LTI por:  

-   Ensuring que a infraestrutura adequada existe conforme descrito em [garantir que a infraestrutura adequado existe](#EnsureInfrastructure)  

-   Adicionar conteúdo à MDT, conforme descrito em [adicionar conteúdo ao MDT](#AddContent)  

-   Preparar serviços de implementação do Windows, conforme descrito em [Preparar serviços de implementação do Windows](#PrepareDeployment)  

-   Configurar DFS-R, conforme descrito em [configurar a replicação de sistema de ficheiros distribuído](#ConfigureFileReplication)  

-   A preparar a replicação do SQL Server, tal como descrito no [a preparar replicação do SQL Server](#PrepareSQLReplication)  

-   Configurar a replicação do SQL Server, conforme descrito em [configurar a replicação do SQL Server](#ConfigureSQLReplication)  

 Este cenário presumes que MDT está configurado num servidor de implementação principal e que a configuração da base de dados do MDT já foi concluída tal como explicado no início deste documento.  

###  <a name="EnsureInfrastructure"></a> Garantir que a infraestrutura adequada existe  
 A infraestrutura de implementação LTI altamente dimensionável utiliza uma topologia de concentrador hub-and-spoke para a replicação de conteúdo; primeiro para um servidor de implementação no ambiente de produção que irá executar a função de servidor a mestre implementação por conseguinte, indicar.  Segue-se os componentes necessários para o servidor de implementação principal.  

 |**Componente necessário** |**Objetivo/comentário** |  
 |-|-|  
 |Windows Server 2003 R2|Necessário para suportar o DFS-R|  
 |MDT |Contém a cópia principal da partilha de implementação|  
 |SQL Server 2005|Tem de ser uma versão completa para permitir a replicação da base de dados do MDT|  
 |DFS-R |Necessário para a replicação de partilha de implementação|  
 |Serviços de Implementação do Windows |Necessário para permitir instalações de rede com base em PXE ser iniciada|  

 Quando tiver selecionado o servidor de implementação principal, Aprovisione servidores adicionais em cada site para suportar implementações LTI.  Segue-se os componentes necessários para o servidor de implementação do subordinado.  

 |**Componente necessário** |**Objetivo/comentário** |  
 |-|-|  
 |Windows Server 2003 R2|Necessário para suportar o DFS-R|  
 |Microsoft SQL Server 2005 Express Edition |Recebe cópias replicadas da BD do MDT|  
 |DFS-R |Necessário para a replicação de partilha de implementação|  
 |Serviços de Implementação do Windows |Necessário para permitir instalações de rede com base em PXE ser iniciada|  

> [!NOTE]
>  Serviços de implementação do Windows tem de ser configurados e configurados em cada servidor subordinado, mas não é necessário adicionar imagens de arranque ou instalação.  

###  <a name="AddContent"></a> Adicionar conteúdo à MDT  
 Preencha o servidor de implementação principal com conteúdo utilizando o Deployment Workbench e criar e preencher a BD do MDT, conforme descrito nas secções seguintes. Para informações sobre a preencher a base de dados com:  

-   As aplicações, consulte a secção "Configurar aplicações no Deployment Workbench", no documento MDT *utilizar o Microsoft Deployment Toolkit*  

-   Sistemas operativos, consulte a secção "Configurar os sistemas operativos no Deployment Workbench", no documento MDT *utilizar o Microsoft Deployment Toolkit*  

-   Pacotes do sistema operativo, consulte a secção "Configurar pacotes no Deployment Workbench", no documento MDT *utilizar o Microsoft Deployment Toolkit*  

-   Controladores de dispositivo, consulte a secção "Configurar dispositivo controladores no Deployment Workbench", no documento MDT *utilizar o Microsoft Deployment Toolkit*  

-   As sequências de tarefas, consulte a secção "Configurar tarefas sequências no Deployment Workbench", no documento MDT *utilizar o Microsoft Deployment Toolkit*  

> [!NOTE]
>  Certifique-se de que o ficheiro de LiteTouchPE_x86.wim criado quando a partilha de implementação é atualizada foi adicionado aos serviços de implementação do Windows.  

###  <a name="PrepareDeployment"></a> Preparar os serviços de implementação do Windows  
 Porque o ficheiro LiteTouchPE_x86.wim será replicado periodicamente através do grupo de replicação de DFS-R, o arquivo de dados de configuração de arranque deve ser atualizado periodicamente para refletir o ambiente Windows PE recentemente replicado. Execute os seguintes passos em cada um dos servidores de implementação.  

 **Para preparar os serviços de implementação do Windows**  

1.  Abra uma janela de linha de comandos.  

2.  Tipo **WDSUtil/set-servidor/BCDRefreshPolicy/ativada: Sim / RefreshPeriod:60**, e, em seguida, prima ENTER.  

> [!NOTE]
>  No exemplo aqui apresentado, o período de atualização está definido como 60 minutos; No entanto, pode configurar este valor para replicar durante um período igual do DFS-R.  

###  <a name="ConfigureFileReplication"></a> Configurar replicação do sistema de ficheiros distribuído  
 Quando o dimensionamento a arquitetura de implementação LTI, utilize DFS-R como base para replicar o conteúdo de partilha de implementação MDT e o ambiente de arranque do Windows PE Lite Touch e do servidor de implementação principal para os servidores de implementação do subordinado.  

> [!NOTE]
>  Certifique-se de que o DFS-R está instalado antes de efetuar os seguintes passos.  

 **Para configurar o DFS-R para replicar o conteúdo de implementação**  

1.  Abrir a consola de gestão de DFS.  

2.  Na consola de gestão de DFS, expanda gestão de DFS.  

3.  Clique com botão direito **replicação**e, em seguida, clique em **novo grupo de replicação**.  

4.  No Assistente de grupo de nova replicação, no **tipo de grupo de replicação** página, clique em **novo grupo de replicação de múltiplas finalidades**.  

5.  Clique em **Seguinte**.  

6.  No **nome e domínio** página, introduza as seguintes informações:  

    -   No **nome para o grupo de replicação** caixa, escreva um nome para o grupo de replicação — por exemplo, **grupo de replicação do MDT 2010**.  

    -   No **uma descrição opcional do grupo de replicação** caixa, digite uma descrição do grupo de replicação — por exemplo, **grupo de replicação dos dados de 2010 do MDT**.  

    -   Certifique-se de que o **domínio** caixa contém o nome de domínio correto.  

7.  Clique em **Seguinte**.  

8.  No **membros do grupo de replicação** página, execute estes passos:  

    1.  Clique em **Adicionar**.  

    2.  Escreva os nomes de todos os servidores que estão a ser membros deste grupo de replicação — por exemplo, todos os servidores de implementação de subordinados e o servidor de implementação principal.  

    3.  Clique em **OK**.  

9. Clique em **Seguinte**.  

10. No **seleção de topologia** página, clique em **Hub- and -Spoke**e, em seguida, clique em **seguinte**.  

11. No **Hub membros** página, clique no servidor de implementação principal e, em seguida, clique em **adicionar**.  

12. Clique em **Seguinte**.  

13. No **Hub- and Spoke ligações** página, certifique-se de que para cada subordinado listado o servidor de principal de implementação de servidor de implementação é o **necessário membro de Hub**.  

14. Clique em **Seguinte**.  

15. No **largura de banda e agendamento de grupo de replicação** página, especifique uma agenda para replicar o conteúdo entre servidores.  

16. Clique em **Seguinte**.  

17. No **membro principal** na página de **membro principal** caixa, clique no servidor de implementação principal.  

18. Clique em **Seguinte**.  

19. No **pastas replicar** página, clique em **adicionar**e, em seguida, execute estes passos:  

    1.  No **caminho Local da pasta para replicar** , clique em **procurar** para ir para o *x:\\*pasta de implementação (onde *X* é a letra de unidade no servidor de implementação).  

    2.  Clique em **utilize o nome com base no caminho**.  

    3.  Clique em **OK**.  

    4.  Clique em **Adicionar**.  

    5.  No **Adicionar pasta replicar** caixa de diálogo, clique em **procurar** para ir para o *x:* \RemoteInstall\Boot pasta.  

    6.  Clique em **utilize o nome com base no caminho**.  

20. Clique em **Seguinte**.  

21. No **caminho de distribuição Local em outros membros** página, execute estes passos:  

    1.  Selecione todos os membros do grupo de distribuição e, em seguida, clique em **editar**.  

    2.  No **Editar Caminho Local** caixa de diálogo, clique em **ativado**.  

    3.  Escreva o caminho onde a pasta de partilha de implementação deve ser armazenada no servidor de implementação do subordinado — por exemplo, ***X:\Deployment*** (onde *X* é a letra de unidade no servidor de implementação).  

    4.  Clique em **OK**.  

22. Clique em **Seguinte**.  

23. No **Local caminho de arranque em outros membros** página, execute estes passos:  

    1.  Selecione todos os membros do grupo de distribuição e, em seguida, clique em **editar**.  

    2.  No **Editar Caminho Local** caixa de diálogo, clique em **ativado**.  

    3.  Escreva o caminho em que a pasta de arranque deve ser armazenada no servidor de implementação do subordinado — por exemplo, ***X:\RemoteInstall\Boot*** (onde *X* é a letra de unidade no servidor de implementação).  

    4.  Clique em **OK**.  

24. Clique em **Seguinte**.  

25. No **definições remotas e criar o grupo de replicação** página, clique em **criar** para concluir o Assistente de novo grupo de replicação.  

26. No **confirmação** página, clique em **fechar** para fechar o assistente.  

> [!NOTE]
>  Certifique-se de que o novo grupo de replicação está agora listado abaixo do nó de replicação.  

###  <a name="PrepareSQLReplication"></a> A preparar replicação do SQL Server  
 Antes de replicação do SQL Server pode ser configurada, conclua vários passos de pré-configuração para se certificar de que os servidores de implementação estão configurados corretamente.  

 **Para preparar a replicação do SQL Server no servidor de implementação principal**  

1.  Crie uma pasta para armazenar os instantâneos da base de dados e, em seguida, configure a pasta como uma partilha.  

    > [!NOTE]
    >  Para obter mais informações sobre como proteger a pasta de instantâneos, consulte [proteger a pasta de instantâneos](http://msdn2.microsoft.com/library/ms151151.aspx).  

2.  Certifique-se de que o serviço de Browser do SQL Server esteja ativado e definido para automático.  

3.  No **configuração de área de superfície do SQL Server** , clique em **ligações locais e remotos**.  

 **Para preparar a replicação do SQL Server no servidor de implementação de subordinados**  

1.  No **configuração de área de superfície do SQL Server** , clique em **ligações locais e remotos**.  

2.  Opcionalmente, crie uma base de dados vazio para alojar a base de dados replicados do MDT.  

> [!NOTE]
>  Esta base de dados deve ser dada o mesmo nome da base de dados do MDT no servidor de implementação principal. Por exemplo, se a BD do MDT no servidor de implementação principal é denominada *MDTDB*, criar uma base de dados vazio denominado *MDTDB* no servidor de implementação do subordinado.  

###  <a name="ConfigureSQLReplication"></a> Configurar a replicação do SQL Server  
 Depois de configurar a replicação de ficheiros e pastas necessárias para criar a infraestrutura de implementação, configure o SQL Server para replicar a BD do MDT.  

> [!NOTE]
>  Também é possível manter a apenas um único central MDT DB; No entanto, por manter uma versão replicada da base de dados do MDT, pode ser mantido maior controlo sobre dados transferir através da rede de área alargada (WAN).  

 SQL Server 2005 utiliza um modelo de replicação que é semelhante a um modelo de distribuição magazine:  

1.  A *magazine* é disponibilizada (publicado) por um *publicador*.  

2.  *Distribuidores* são utilizados para distribuir a publicação.  

3.  *Os leitores* pode subscrever uma publicação de modo a que essa publicação é entregue ao subscritor periodicamente (um *push subscrição*).  

 É utilizada este terminologia através os assistentes de instalação e configuração de replicação do SQL Server.  

#### <a name="configure-a-sql-server-publisher"></a>Configurar um publicador do SQL Server  
 Para configurar o servidor de implementação principal como um publicador do SQL Server, execute estes passos:  

1.  Abra o SQL Server Management Studio.  

2.  Clique com botão direito do **replicação** nó e, em seguida, clique em **configurar distribuição**.  

3.  No Assistente de configuração de distribuição, clique em **seguinte**.  

4.  No **distribuidor** página, clique em **atuará como o seu próprio distribuidor; SQL Server irá criar uma base de dados de distribuição e o registo**e, em seguida, clique em **seguinte**.  

5.  No **pasta de instantâneos** na página de **a preparar replicação do SQL Server** secção, escreva o caminho UNC para a pasta de instantâneos criado.  

6.  No **base de dados de distribuição** página, clique em **seguinte**.  

7.  No **publicadores** página, clique no servidor de implementação principal para defini-lo como distribuidor e, em seguida, clique em **seguinte**.  

8.  No **ações do assistente** página, clique em **configurar distribuição**e, em seguida, clique em **seguinte**.  

9. Clique em **concluir**e, em seguida, clique em **fechar** quando o assistente é concluído.  

#### <a name="enable-the-mdt-db-for-replication"></a>Ativar a BD do MDT para replicação  
 Para ativar a BD do MDT para replicação no servidor de implementação principal, execute estes passos:  

1.  No SQL Server Management Studio, clique com botão direito do **replicação** nó e, em seguida, clique em **publicador propriedades**.  

2.  No **publicador propriedades** página, execute estes passos:  

    1.  Clique em **bases de dados do publicador**.  

    2.  Clique a BD do MDT e, em seguida, clique em **transacional**.  

    3.  Clique em **OK**.  

 A BD do MDT está agora configurada para replicação transacional e de instantâneo.  

#### <a name="create-a-publication-of-the-mdt-db"></a>Criar uma publicação da BD do MDT  
 Para criar uma publicação da BD do MDT aos quais podem subscrever os servidores de implementação de subordinados, execute estes passos:  

1.  No SQL Server Management Studio, expanda a replicação, faça duplo clique **publicações Local**e, em seguida, clique em **publicação novo**.  

2.  No Assistente de nova publicação, clique em **seguinte**.  

3.  No **base de dados de publicação** página, clique a BD do MDT e, em seguida, clique em **seguinte**.  

4.  No **publicação tipo** página, clique em **publicação de instantâneo**e, em seguida, clique em **seguinte**.  

5.  No **artigos** página, selecione todos os **tabelas, procedimentos armazenados**, e **vistas**e, em seguida, clique em **seguinte**.  

6.  No **problemas de artigos** página, clique em **seguinte**.  

7.  No **linhas da tabela de filtro** página, clique em **seguinte**.  

8.  No **agente de instantâneo** página, execute estes passos:  

    1.  Selecione **criar um instantâneo imediatamente e manter o instantâneo disponível para inicializar subscrições**.  

    2.  Clique em **agendar o agente de instantâneos para executar nas seguintes alturas**.  

    3.  Clique em **Alterar**.  

    > [!NOTE]
    >  Especifique uma agenda que irá ocorrer uma hora antes da base de dados são replicados.  

9. Clique em **Seguinte**.  

10. No **segurança do agente** página, clique na conta sob a qual o agente de instantâneo é executados e, em seguida, clique em **seguinte**.  

11. No **ações do assistente** página, clique em **criar a publicação**e, em seguida, clique em **seguinte**.  

12. No **conclua o assistente** na página de **nome da publicação** caixa, escreva um nome descritivo da publicação.  

13. Clique em **concluir** conclua o assistente e, em seguida, clique em **fechar** quando o assistente ter criado a publicação.  

    > [!NOTE]
    >  A publicação agora estará visível sob o nó de publicações Local no SQL Server Management Studio.  

#### <a name="subscribe-child-deployment-servers-to-the-published-mdt-db"></a>Subscrever os servidores de implementação de subordinados para a BD do MDT publicada  
 Agora que foi publicada a BD do MDT, pode adicionar os servidores de implementação subordinado como subscritores para esta publicação; ou seja, que irá receber uma cópia da base de dados com base numa agenda de modo a que durante uma implementação, os computadores cliente podem consultar uma base de dados que é local para a rede em vez do na WAN.  

 **Para subscrever os servidores de implementação de subordinados para a publicação de BD do MDT**  

1.  No SQL Server Management Studio, vá para publicações Local/replicação.  

2.  Clique com o botão direito a publicação que criou na secção anterior e, em seguida, clique em **novas subscrições**.  

3.  No Assistente de novas subscrições, clique em **seguinte**.  

4.  No **publicação** página, clique na publicação que criou na secção anterior.  

5.  No **localização do agente de distribuição** página, clique em **executar todos os agentes no distribuidor SERVERNAME (subscrições de emissão)** e, em seguida, clique em **seguinte**.  

6.  No **subscritores** página, adicionar cada um dos servidores de implementação subordinado, efetuando os seguintes passos:  

    1.  Clique em **adicionar subscritor**e, em seguida, clique em **adicionar subscritor do SQL Server**.  

    2.  Adicione cada servidor de implementação do subordinado.  

    3.  Para cada servidor de implementação de subordinados adicionado no **base de dados de subscrição** , clique na BD do MDT vazio nesse servidor de implementação do subordinado.  

    > [!NOTE]
    >  Se a BD do MDT vazio ainda não foi criada, além de **base de dados de subscrição** caixa, selecione a opção para criar uma nova base de dados.  

    > [!NOTE]
    >  Esta base de dados deve ser dada o mesmo nome da base de dados do MDT no servidor de implementação principal. Por exemplo, se a BD do MDT no servidor de implementação principal é denominada *MDTDB*, criar uma base de dados vazio denominado *MDTDB* no servidor de implementação do subordinado.  

7.  Clique em **Seguinte**.  

8.  No **segurança do agente de distribuição** página, clique em **...** Para abrir o **segurança do agente de distribuição** caixa de diálogo.  

9. Introduza os detalhes da conta a utilizar para o agente de distribuição e, em seguida, clique em **seguinte**.  

10. No **agenda de sincronização** página, execute estes passos:  

    1.  No **agenda do agente** , clique em **< Definir agenda\>**.  

    2.  Especifique o agendamento que deve ser utilizado para replicar a base de dados entre os servidores de implementação do principal e subordinada e, em seguida, clique em **seguinte**.  

11. No **inicializar subscrição** página, clique em **seguinte**.  

12. No **ações do assistente** página, clique em **criar as subscrições**e, em seguida, clique em **seguinte**.  

13. Clique em **concluir**e, em seguida, clique em **fechar** quando o assistente foi concluído com êxito.  

 Replicação do SQL Server está agora configurada e a BD do MDT será replicada do servidor de implementação principal para todos os servidores de implementação de subordinados que foram subscritos-la numa base periódica.  

#### <a name="configure-customsettingsini"></a>Configurar CustomSettings.ini  
 A infraestrutura de implementação LTI tem agora foi criada com êxito e cada localização irá conter um servidor de implementação LTI, com uma cópia replicada:  

-   A partilha de implementação  

-   A BD do MDT  

-   O ambiente de LiteTouchPE_x86 Windows PE que tenha sido adicionado aos serviços de implementação do Windows  

 Agora, pode configurar o ficheiro CustomSettings.ini para a partilha de implementação a utilizar os conteúdos de implementação (partilha de implementação e da base de dados) do respetivo servidor de implementação de local, o servidor que fornece o ambiente de LiteTouchPE_x86.wim através da implementação do Windows Serviços.  

 Quando o ficheiro LiteTouchPE_x86.wim for entregue a partir dos serviços de implementação do Windows, uma chave de registo está configurada com o nome do servidor de serviços de implementação do Windows que estiver a utilizar. MDT captura este nome de servidor numa variável (% WDSServer %) que pode utilizar para configurar CustomSettings.ini.  

 **Para utilizar sempre o servidor de implementação LTI local**  

> [!NOTE]
>  O procedimento seguinte parte do princípio de que a partilha de implementação foi criada e definida como a partilha de $ de implementação.  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share* (onde *deployment_share* é o nome da partilha de implementação para configurar).  

3.  No painel ações, clique em **propriedades**.  

4.  Clique em de **regras** separador e, em seguida, modifique o ficheiro CustomSettings.ini para configurar as seguintes propriedades:  

    -   Para cada secção do SQL Server adicionada, configurar **SQLServer** para utilizar o nome do servidor **% WDSServer % —** por exemplo, **SQLServer = % WDSServer %**.  

    -   Se configurar **DeployRoot**, configurar **DeployRoot** para utilizar o **% WDSServer %** variável — por exemplo, **DeployRoot =\\ \\%WDSServer%\Deployment$**.  

5.  Clique em **editar Bootstrap.ini**.  

6.  Configurar BootStrap.ini para utilizar o **% WDSServer %** propriedade por adicionar ou alterar o **DeployRoot** valor **DeployRoot =\\\\%WDSServer%\Deployment$** .  

7.  Clique em **ficheiro**e, em seguida, clique em **guardar** para guardar as alterações ao ficheiro BootStrap.ini.  

8.  Clique em **OK**.  

     A partilha de implementação e ambiente LiteTouchPE_x86.wim Windows PE tem de ser atualizados.  

9. No painel ações, clique em **partilha de implementação de atualização**.  

     Inicia o Assistente de partilha de implementação da atualização.  

10. No **opções** página, selecione as opções pretendidas para atualizar a partilha de implementação e, em seguida, clique em **seguinte**.  

11. No **resumo** página, verifique os detalhes estão corretos e, em seguida, clique em **seguinte**.  

12. No **confirmação** página, clique em **concluir**.  

 O exemplo a seguir ilustra CustomSettings.ini depois de efetuar os passos descritos nesta secção.  

 **CustomSettings.ini configurado para a infraestrutura de implementação LTI dimensionável de exemplo**  

```  
[Settings]  
Priority=CSettings,CPackages, CApps, CAdmins, CRoles, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac  

[CSettings]  
SQLServer=%WDSServer%  
Instance=  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerSettings  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CPackages]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerPackages  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CApps]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerApplications  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CAdmins]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerAdministrators  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CRoles]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerRoles  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
```  

## <a name="selecting-a-local-mdt-server-when-multiple-servers-exist"></a>Selecionar um servidor Local do MDT quando existem vários servidores  
 Neste cenário, vários servidores do MDT estão a ser utilizados para suportar um grande volume de implementações em simultâneo e implementações de múltiplos sites. Quando uma implementação LTI é inicializada, o comportamento predefinido é um caminho para o servidor do MDT para ligar a e aceder aos ficheiros necessários para iniciar o processo de implementação do pedido.  

 O Assistente de implementação do Windows podem utilizar o ficheiro de LocalServer.xml para apresentar uma escolha de servidores conhecidos de implementação para cada localização.  

 Utilize o ficheiro de LocationServer.xml por:  

-   Compreender a finalidade e a utilização de LocationServer.xml conforme descrito em [compreender LocationServer.xml](#UnderstandingLocationServer)  

-   Criar o ficheiro de LocationServer.xml conforme descrito em [criar o ficheiro LocationServer.xml](#CreateLocationServer)  

-   Adicionar o ficheiro de LocationServer.xml para o diretório de ficheiros adicionais, conforme descrito em adicionar o ficheiro de LocationServer.xml para o diretório de ficheiros adicionais  

-   Atualizar o ficheiro BootStrap.ini conforme descrito em [atualizar o ficheiro BootStrap.ini](#UpdateBootstrap)  

-   A partilha de implementação de atualização, conforme descrito em [atualizar partilha de implementação](#UpdateDeploymentShare)  

 Este cenário pressupõe que o MDT é configurado num servidor de implementação.  

###  <a name="UnderstandingLocationServer"></a> Noções sobre LocationServer.xml  
 Em primeiro lugar, tem de compreender que como o MDT utiliza LocationServer.xml. Durante a LTI, scripts de MDT ler e processam o ficheiro BootStrap.ini para recolher iniciais informações sobre a implementação. Isto ocorre antes de uma ligação foi efetuada para o servidor de implementação. Por conseguinte, o **DeployRoot** propriedade costuma é utilizada para especificar o ficheiro BootStrap.ini o servidor de implementação para o qual este deve estabelecer uma ligação.  

 Se o ficheiro BootStrap.ini não contém um **DeployRoot** propriedade, scripts de MDT carregar uma página do Assistente para solicitar ao utilizador para um caminho para o servidor de implementação. Ao inicializar o **aplicação HTML (HTA)** página do assistente, MDT scripts Verifique a existência do ficheiro LocationServer.xml e, se existir, utilize LocationServer.xml para apresentar os servidores de implementação disponíveis.  

#### <a name="understand-when-to-use-locationserverxml"></a>Compreender quando deve utilizar LocationServer.xml  
 MDT oferece várias formas para determinar que servidor se ligue aos durante uma implementação LTI. Métodos diferentes para localizar o servidor de implementação são mais adequados para diferentes cenários; Por conseguinte, é importante compreender quando deve utilizar LocationServer.xml.  

 O MDT fornece vários métodos para detetar e utilizar o servidor de implementação mais adequado automaticamente. Estes métodos estão listados na seguinte tabela.

 |**Método** |**Detalhes** |  
 |-|-|  
 |**%WDSServer%** |Este método é utilizado quando o servidor do MDT conjuntamente está alojado no servidor de serviços de implementação do Windows.<br /><br /> Quando uma implementação LTI é iniciada a partir de serviços de implementação do Windows, uma variável de ambiente — % WDSServer % — é criadas e preenchidas com o nome do servidor dos serviços de implementação do Windows.<br /><br /> O **DeployRoot** variável pode utilizar esta variável para ligar automaticamente a uma partilha de implementação no servidor de serviços de implementação do Windows — por exemplo:<br /><br /> **DeployRoot=\\\\%WDSServer%\Deployment$** |  
 |**Com base na localização de automatização** |MDT pode utilizar com base na localização de automatização no ficheiro BootStrap.ini para determinar o servidor ao qual deve implementar.<br /><br /> Utilize o **Gateway predefinido** propriedade para distinguir entre as diferentes localizações; para cada **Gateway predefinido**, um servidor diferente do MDT que está especificado.<br /><br /> Para obter mais informações sobre a utilização de automatização com base na localização, consulte "Selecionar os métodos para aplicar as definições de configuração".|  

 Cada abordagem listada na tabela que precede oferece uma forma de automatizar a seleção do servidor numa localização especificada para determinados cenários de implementação. Estas abordagens são direcionadas para cenários específicos — por exemplo, quando o servidor do MDT é conjuntamente alojado com os serviços de implementação do Windows.  

 Existem outros cenários em que estas abordagens não são adequadas — por exemplo, se existirem vários servidores de implementação a uma determinada lógica de automatização ou localização não é possível (por exemplo, a rede não é segmentada suficiente para permitir a determinação de localização ou o servidor do MDT está separado dos serviços de implementação do Windows).  

 Nestes cenários, o ficheiro de LocationServer.xml fornece uma forma flexível para apresentar estas informações no momento da implementação sem necessidade de conhecimento de nomes de servidor e os nomes das partilhas de implementação.  

###  <a name="CreateLocationServer"></a> Criar o ficheiro LocationServer.xml  
 Para apresentar uma lista de servidores de implementação disponíveis durante uma implementação LTI, crie um ficheiro de LocationServer.xml que contém detalhes sobre cada servidor. Não há nenhum ficheiro de LocationServer.xml predefinido no MDT, por isso, crie um usando as seguintes orientações.  

#### <a name="create-a-locationserverxml-file-to-support-multiple-locations"></a>Criar um ficheiro de LocationServer.xml para suportar várias localizações  
 O método mais simples para criar e utilizar LocationServer.xml consiste em criar um ficheiro de LocationServer.xml e adicionar entradas para cada servidor de implementação no ambiente (que pode ser na mesma localização ou em localizações diferentes).  

 Construir o ficheiro LocationServer.xml ao criar uma nova secção para cada servidor e, em seguida, adicionar as seguintes informações:  

-   Um identificador exclusivo  

-   Um nome de localização, utilizado para apresentar um nome facilmente identificável para essa localização  

-   Um caminho UNC para o servidor do MDT para essa localização  

 Os seguintes ilustra como o ficheiro LocationServer.xml é criado através de cada uma destas propriedades utilizando um ficheiro de LocationServer.xml exemplo configurado para várias localizações.  

 **Exemplo de ficheiro LocationServer.xml para suportar várias localizações**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 Utilizar este formato, especifique as entradas de servidor diferente para cada localização ou para situações em que existem vários servidores dentro de uma única localização, especificando uma entrada de servidor diferente para cada servidor em que a localização, conforme mostrado no exemplo seguinte.   

 **Exemplo de ficheiro LocationServer.xml para suportar vários servidores em várias localizações**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ DS1, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso HQ DS2, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS02\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

#### <a name="create-a-locationserverxml-file-to-load-balance-multiple-servers-at-different-locations"></a>Criar um ficheiro de LocationServer.xml para o balanceamento de carga vários servidores em diferentes localizações  
 Utilizar LocationServer.xml, especificar vários servidores por entrada de localização e, em seguida, efetuar o balanceamento de carga básica para que quando é escolhida uma localização, MDT seleciona automaticamente um servidor de implementação da lista de servidores disponíveis. Para disponibilizar esta funcionalidade, o ficheiro LocationServer.xml suporta a especificação de uma métrica de peso.  

 O seguinte ilustra um ficheiro de LocationServer.xml exemplo configurado para vários servidores em diferentes localizações.  

 **Exemplo de ficheiro de LocationServer.xml para localizações diferentes**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <Server1>\\STLDS01\Deployment$</Server1>  
        <Server2>\\STLDS02\Deployment$</Server2>  
        <Server3>\\STLDS03\Deployment$</Server3>  
        <Server weight=”1”>\\STLDS01\Deployment$</Server>  
        <Server weight=”2”>\\STLDS02\Deployment$</Server>  
        <Server weight=”4”>\\STLDS03\Deployment$</Server>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 Especifique a métrica de peso utilizando o < ponderação servidor\> etiqueta, que utiliza o MDT no processo de seleção de servidor. A probabilidade de um servidor que está a ser selecionado é calculada ao:  

 **Servidor ponderação/soma de todas as ponderações de servidor**  

 No exemplo anterior, os três servidores em Contoso HQ estão listados como 1, 2 e 4. A probabilidade de um servidor com um peso de 2 a ser selecionados torna-se 2 no 7. Por conseguinte, para utilizar o sistema de peso, determinar a capacidade dos servidores disponíveis numa localização e cada servidor de importância pela capacidade do servidor em relação a cada um dos outros servidores.  

### <a name="adding-the-locationserverxml-file-to-the-extra-files-directory"></a>Adicionar o ficheiro de LocationServer.xml para o diretório de ficheiros adicionais  
 Depois de ter criado o ficheiro LocationServer.xml, adicione-o para as imagens de arranque LiteTouch_x86 e LiteTouch_x64 Windows PE no ***x:\\Deploy\Control pasta***. Utilizar o Deployment Workbench, adicione outros ficheiros e pastas para estas imagens do Windows PE, especificando um diretório adicional para adicionar as propriedades de partilha de implementação.  

 **Para adicionar LocationServer.xml para a partilha de implementação**  

1.  Crie uma pasta denominada *ficheiros adicionais* na pasta de partilha de implementação de raiz (por exemplo, D:\Production implementação Share\Extra ficheiros).  

2.  Crie uma estrutura de pasta na pasta do ficheiros adicionais que reflete a localização do Windows PE onde o ficheiro adicional deve residir.  

     Por exemplo, o ficheiro LocationServer.xml têm de residir na pasta \Deploy\Control no Windows PE; Por conseguinte, crie a mesma estrutura de pasta em ficheiros adicionais (por exemplo, D:\Production implementação Share\Extra Files\Deploy\Control).  

3.  Copiar LocationServer.xml para o *deployment_share*\Extra Files\Deploy\Control pasta (onde *deployment_share* é o caminho completamente qualificado para a pasta raiz da partilha de implementação).  

4.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

5.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share* (onde *deployment_share* é o nome da partilha de implementação para configurar).  

6.  No painel ações, clique em **propriedades**.  

7.  No ***deployment_shareProperties*** (onde deployment_share é o nome da partilha de implementação) da caixa de diálogo executar estes passos:  

    1.  Clique em de **plataforma do Windows PE definições** separador (onde *plataforma* é a arquitetura da imagem do Windows PE para ser configurado).  

    2.  No **personalizações do Windows PE** na secção de **Extra diretório para adicionar** caixa, escreva ***caminho*** (onde *caminho* está completamente qualificado caminho para a pasta de ficheiros adicionais — por exemplo, o D:\Production implementação Share\Extra ficheiros) e, em seguida, clique em **OK**.  

###  <a name="UpdateBootstrap"></a> Atualizar o ficheiro BootStrap.ini  
 Quando cria uma partilha de implementação a utilizar o Deployment Workbench, um **DeployRoot** propriedade é automaticamente criada e preenchida no ficheiro BootStrap.ini. Porque o ficheiro de LocationServer.xml é utilizado para preencher o **DeployRoot** propriedade, tem de remover este valor do ficheiro BootStrap.ini.  

 **Para remover a propriedade DeployRoot BootStrap.ini**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share* (onde *deployment_share* é o nome da partilha de implementação para configurar).  

3.  No painel ações, clique em **propriedades**.  

4.  No ***deployment_shareProperties*** caixa de diálogo (onde *deployment_share* é o nome da partilha de implementação), clique em de **regras** separador e, em seguida, clique em **Editar BootStrap.ini**.  

5.  Remova o **DeployRoot** valor (por exemplo, **DeployRoot =\\\Server\Deployment$**).  

6.  Clique em **ficheiro**e, em seguida, clique em **guardar** para guardar as alterações ao ficheiro BootStrap.ini.  

7.  Clique em **OK** para submeter as alterações.  

###  <a name="UpdateDeploymentShare"></a> A partilha de implementação de atualização  
 A partilha de implementação seguinte têm de ser atualizada para gerar um ambiente de arranque LiteTouch_x86 e LiteTouch_x64 novo que contém o ficheiro de LocationServer.xml e o ficheiro BootStrap.ini atualizado.  

 **Para atualizar a partilha de implementação**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share* (onde *deployment_share* é o nome da partilha de implementação para configurar).  

3.  No painel ações, clique em **partilha de implementação de atualização**.  

     Inicia o Assistente de partilha de implementação da atualização.  

4.  No **opções** página, selecione as opções pretendidas para atualizar a partilha de implementação e, em seguida, clique em **seguinte**.  

5.  No **resumo** página, verifique os detalhes estão corretos e, em seguida, clique em **seguinte**.  

6.  No **confirmação** página, clique em **concluir**.  

> [!NOTE]
>  Quando tiver concluído o processo de atualização, adicione os novos ambientes LiteTouch_x86 e LiteTouch_x64 Windows PE para o serviços de implementação do Windows ou grave-os para o suporte de dados a utilizar durante a implementação de arranque.  

## <a name="replacing-an-existing-computer-with-a-new-computer-using-lite-touch-installation"></a>Substituir um computador existente com um novo computador com o método Lite Touch Installation  
 Pode utilizar o MDT para implementar uma imagem para um novo computador que irá substituir um computador existente na arquitetura da empresa. Esta situação foi surgir ao atualizar a partir de um sistema operativo para outro (um novo sistema operativo pode necessitar de hardware novo) ou se a organização precisar de computadores mais recentes, mais rápidos para as aplicações existentes.  

 Quando a substituir um computador existente com um novo computador, a Microsoft recomenda tendo em consideração todas as definições que serão migradas de um computador para outro, tais como contas de utilizador e dados de estado do utilizador. Além disso, é importante criar uma solução de recuperação no caso de falha de migração.  

 Nesta implementação de exemplo, substitua o computador existente (WDG-existe-01) com um novo computador (WDG-novo-02) no domínio CORP pela captura de dados de estado de utilizador a partir de 01 WDG existe e guardá-lo para uma partilha de rede. Em seguida, implementar uma imagem existente WDG 02 novo e, finalmente, restaurar os dados de estado de utilizador capturados WDG 02 novo. A implementação será efetuada a partir de um servidor de implementação (WDG-MDT-01).  

 No MDT, utilize o modelo de sequência de tarefas de substituir do cliente padrão para criar uma sequência de tarefas que irá efetuar todas as tarefas de implementação necessárias.  

 Esta demonstração parte do princípio de que:  

-   MDT foi instalado no servidor de implementação (WDG MDT 01)  

-   A partilha de implementação já foi criada e preenchida, incluindo imagens de sistemas operativos, aplicações e controladores de dispositivo  

-   Uma imagem de um computador de referência já foram capturada e será implementada para o novo computador (WDG novo 02)  

-   Uma pasta partilhada de rede (UserStateCapture$) foi criada e partilhada no servidor de implementação (WDG MDT 01) com as permissões adequadas de partilha  

 Uma partilha de implementação deve existir antes de iniciar este exemplo. Para obter mais informações sobre como criar uma partilha de implementação, consulte a secção "Gerir implementação partilhas no Deployment Workbench", no documento MDT *utilizar o Microsoft Deployment Toolkit*.  

### <a name="step-1-create-a-task-sequence-to-capture-the-user-state"></a>Passo 1: Criar uma sequência de tarefas para capturar o estado do utilizador  
 Crie sequências de tarefas do MDT no nó sequências de tarefas no Deployment Workbench com o Assistente de nova sequência de tarefas. Para efetuar a primeira parte do cenário de implementação de substituir o computador (capturar o estado do utilizador no computador de existente), selecione o modelo de sequência de tarefas de substituir do cliente padrão no Assistente de nova sequência de tarefas.  

 **Para criar uma sequência de tarefas para capturar o estado do utilizador no cenário de implementação de substituir o computador**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação / *deployment_share*/Task sequências (onde *deployment_share* é o nome da partilha de implementação para configurar ).  

3.  No painel ações, clique em **nova sequência de tarefas**.  

     Inicia o Assistente de nova sequência de tarefas.  

4.  Conclua o Assistente de nova sequência de tarefas utilizando as seguintes informações. Aceite os valores predefinidos exceto indicação em contrário.  

    |**Na página do Assistente** |**Fazê-lo** |  
    |-|-|  
    |**Definições gerais** |1.  No **ID de sequência de tarefas**, tipo **VISTA_EXIST**.<br />2.  No **nome da sequência de tarefas**, tipo **efetuar substituir o cenário de computador num computador existente**.<br />3.  Clique em **Seguinte**.|  
    |**Selecione o modelo** |No **os modelos de sequência de tarefas seguintes estão disponíveis**. **Selecione a que pretende utilizar como um ponto de partida**, selecione **sequência de tarefas de substituir do cliente padrão**e, em seguida, clique em **seguinte**.|  
    |**Resumo** |Certifique-se de que os detalhes de configuração estão corretos e, em seguida, clique em **seguinte**.|  
    |**Confirmação** |Clique em **Concluir**.|  

 O Assistente de nova sequência de tarefas é concluída e o **VISTA_EXIST** sequência de tarefas é adicionada à lista de sequências de tarefas.  

### <a name="step-2-create-a-task-sequence-to-deploy-operating-system-and-restore-the-user-state"></a>Passo 2: Criar uma sequência de tarefas para implementar o sistema operativo e restaurar o estado do utilizador  
 Crie sequências de tarefas do MDT no nó sequências de tarefas no Deployment Workbench, utilizando o Assistente de nova sequência de tarefas. Para efetuar a segunda parte do cenário de implementação de substituir o computador (implementar o sistema operativo e, em seguida, restaurar o estado do utilizador no computador de existente), selecione o modelo de sequência de tarefas de cliente padrão no Assistente de nova sequência de tarefas.  

 **Para criar uma sequência de tarefas para implementar o estado do utilizador no cenário de implementação de substituir o computador**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share*/Task sequências (onde *deployment_share* é o nome da partilha de implementação para configurar ).  

3.  No painel ações, clique em **nova sequência de tarefas**.  

     Inicia o Assistente de nova sequência de tarefas.  

4.  Conclua o Assistente de nova sequência de tarefas utilizando as seguintes informações. Aceite os valores predefinidos exceto indicação em contrário.  

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Definições gerais**|1.  No **ID de sequência de tarefas**, tipo **VISTA_NEW**.<br />2.  No **nome da sequência de tarefas**, tipo **efetuar substituir o cenário de computador no novo computador**.<br />3.  Clique em **Seguinte**.|  
    |**Selecione o modelo**|No **os modelos de sequência de tarefas seguintes estão disponíveis**. **Selecione a que pretende utilizar como um ponto de partida**, selecione **sequência de tarefas de cliente padrão**e, em seguida, clique em **seguinte**.|  
    |**Selecione o SO**|No **imagens de sistema operativo que se seguem estão disponíveis para implementação com esta sequência de tarefas**. Selecione um para utilizar, selecione ***captured_vista_image*** (onde *captured_vista_image* é a imagem capturada do computador de referência adicionado ao nó sistemas operativos no Deployment Workbench) e, em seguida, Clique em *seguinte*.|  
    |**Especifique a chave de produto**|Selecione **não especificar uma chave de produto neste momento**e, em seguida, clique em **seguinte**.|  
    |Definições de SO|1.  No **nome completo**, tipo **Woodgrove empregado**.<br />2.  No **organização**, tipo **Banco Woodgrove**.<br />3.  No **Home Page do Internet Explorer**, tipo **http://www.woodgrovebank.com**.<br />4.  Clique em **Seguinte**.|  
    |**Palavra-passe de administrador**|No **palavra-passe de administrador** e **confirme a palavra-passe de administrador**, tipo **P@ssw0rd**e, em seguida, clique em **concluir**.|  
    |**Confirmação**|Clique em **Concluir**.|  

 O Assistente de nova sequência de tarefas é concluída e o **VISTA_NEW** sequência de tarefas é adicionada à lista de sequências de tarefas.  

### <a name="step-3-customize-the-mdt-configuration-files"></a>Passo 3: Personalizar os ficheiros de configuração do MDT  
 Quando tiver sido criada a sequência de tarefas do MDT, personalize os ficheiros de configuração do MDT que fornecem as definições de configuração para capturar informações de estado do utilizador. Especificamente, personalize o ficheiro CustomSettings.ini, modificando o ficheiro nas propriedades de partilha de implementação criado anteriormente no processo de implementação. Num passo posterior, a partilha de implementação será atualizada para se certificar de que o ficheiro de configuração está atualizado na partilha de implementação.  

 **Para personalizar os ficheiros de configuração do MDT para capturar informações de estado do utilizador**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share* (onde *deployment_share* é o nome da partilha de implementação para configurar).  

3.  No painel ações, clique em **propriedades**.  

     O **propriedades** é apresentada a caixa de diálogo.  

4.  No **propriedades** caixa de diálogo, clique em de **regras** separador.  

5.  No **regras** separador, modifique o ficheiro CustomSettings.ini para refletir as alterações necessárias, conforme mostrado no exampple seguinte. Efetue quaisquer modificações adicionais que requer o ambiente.  

     **Ficheiro CustomSettings.ini personalizado**  

    ```  
    [Settings]  
    Priority=Default  
    Properties=MyCustomProperty  

    [Default]  
    OSInstall=Y  

    UDShare=\\WDG-MDT-01\UserStateCapture$  
    UDDir=%OSDCOMPUTERNAME%  
    UserDataLocation=NETWORK  
    SkipCapture=NO  
    SkipAdminPassword=YES  
    SkipProductKey=YES  

    ```  

6.  No **propriedades** caixa de diálogo, clique em **OK**.  

7.  Feche todas as janelas abertas e caixas de diálogo.  

### <a name="step-4-configure-the-windows-pe-options-for-the-deployment-share"></a>Passo 4: Configurar as opções de PE do Windows para a partilha de implementação  
 Configure as opções do Windows PE para a partilha de implementação no nó de partilhas de implementação no Deployment Workbench.  

> [!NOTE]
>  Se os controladores de dispositivo para o computador existente (WDG-existe-01) e o novo computador (WDG-novo-01) são incluídos com o Windows Vista, ignore este passo e continue com o passo seguinte.  

 **Para configurar as opções do Windows PE para a partilha de implementação**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share* (onde *deployment_share* é o nome da partilha de implementação para configurar).  

3.  No painel ações, clique em **propriedades**.  

     O **propriedades** é apresentada a caixa de diálogo.  

4.  No **propriedades** caixa de diálogo a **do Windows PE *plataforma* componentes** separador (onde *plataforma* é a arquitetura do Windows Imagem PE seja configurado), na **perfil seleção**, selecione ***device_drivers*** (onde *device_drivers* é o nome da seleção do controlador de dispositivo perfil) e, em seguida, clique em **OK**.  

### <a name="step-5-update-the-deployment-share"></a>Passo 5: Atualize a partilha de implementação  
 Depois de configurar as opções do Windows PE para a partilha de implementação, atualize a partilha de implementação. A atualização da partilha de implementação de atualizações de todos os ficheiros de configuração do MDT e gera uma versão personalizada do Windows PE. A versão personalizada do Windows PE é utilizado para iniciar o computador de referência e iniciar o processo de implementação LTI.  

 **Para atualizar a partilha de implementação no Deployment Workbench**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share* (onde *deployment_share* é o nome da partilha de implementação para configurar).  

3.  No painel ações, clique em **atualização DeploymentShare**.  

     Inicia o Assistente de partilha de implementação da atualização.  

4.  No **opções** página, selecione as opções pretendidas para atualizar a partilha de implementação e, em seguida, clique em **seguinte**.  

5.  No **resumo** página, verifique os detalhes estão corretos e, em seguida, clique em **seguinte**.  

6.  No **confirmação** página, clique em **concluir**.  

 Deployment Workbench inicia a atualização da partilha de implementação. Deployment Workbench cria o os ficheiros litetouchpe_x86.ISO e LiteTouchPE_x86.wim (para computadores de destino de 32 bits) ou os ficheiros de ficheiros LiteTouchPE_x64.iso e LiteTouchPE_x64.wim (para computadores de destino de 64 bits) no *deployment_share*\Boot pasta (onde *deployment_share* é a pasta partilhada utilizada como a partilha de implementação).  

### <a name="step-6-create-the-lti-bootable-media"></a>Passo 6: Criar LTI suportes de dados  
 Fornece um método para iniciar o computador com a versão personalizada do Windows PE criada durante a partilha de implementação foi atualizada. Deployment Workbench cria o os ficheiros litetouchpe_x86.ISO e LiteTouchPE_x86.wim (para computadores de destino de 32 bits) ou os ficheiros de ficheiros LiteTouchPE_x64.iso e LiteTouchPE_x64.wim (para computadores de destino de 64 bits) no *deployment_share*\Boot pasta (onde *deployment_share* é a pasta partilhada utilizada como a partilha de implementação). Crie adequado LTI suportes de dados a partir de uma destas imagens.  

 **Para criar LTI suportes de dados**  

1.  No Explorador do Windows, navegue para *deployment_share*\Boot pasta (onde *deployment_share* é a pasta partilhada utilizada como a partilha de implementação).  

2.  Com base no tipo de computador utilizado para o computador existente (WDG-existe-01) e o novo computador (WDG-novo-02), execute uma das seguintes tarefas:  

    -   Se o computador de referência for um computador físico, crie um CD ou DVD do ficheiro ISO.  

    -   Se o computador de referência é uma VM, inicie a VM diretamente a partir do ficheiro ISO ou a partir de um CD ou DVD do ficheiro ISO.  

### <a name="step-7-start-the-existing-computer-with-the-lti-bootable-media"></a>Passo 7: Iniciar o computador existente com LTI suportes de dados  
 Inicie o computador existente (WDG-existe-01) com LTI suportes de dados criado anteriormente no processo. Este CD inicia o Windows PE no computador existente e iniciará o processo de implementação do MDT. No final do processo de implementação MDT, as informações de migração de estado do utilizador são armazenadas na pasta partilhada UserStateCapture$.  

> [!NOTE]
>  Também pode iniciar o processo de MDT ao iniciar o computador de destino a partir dos serviços de implementação do Windows. Para obter mais informações, consulte a secção "Preparar serviços de implementação", no documento MDT *utilizar o Microsoft Deployment Toolkit*.  

 **Para iniciar o computador existente com LTI suportes de dados**  

1.  Inicie 01 WDG existe com LTI suportes de dados criado anteriormente no processo.  

     Windows PE inicia e, em seguida, inicia o Assistente de implementação do Windows.  

2.  Conclua o Assistente de implementação do Windows com as informações seguintes. Aceite os valores predefinidos exceto indicação em contrário.  

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Bem-vindo à implementação**|Clique em **executar o Assistente de implementação** para instalar um novo sistema operativo e, em seguida, clique em **seguinte**.|  
    |**Especifique as credenciais para ligar a partilhas de rede.**|1.  No **nome de utilizador**, tipo **administrador**.<br />2.  No **palavra-passe**, tipo **P@ssw0rd**.<br />3.  No **domínio**, tipo **CORP**.<br />4.  Clique em **OK**.|  
    |**Selecione uma sequência de tarefas para executar neste computador.**|Clique em *efetuar substituir o cenário de computador num computador existente*e, em seguida, clique em **seguinte**.|  
    |**Especifique onde pretende guardar as definições e dados**|Clique em **Seguinte**.|  
    |**Especifique onde pretende guardar uma cópia de segurança de computador completo**|Clique em **não efetuar cópias de segurança do computador existente**e, em seguida, clique em **seguinte**.|  
    |**Pronto para começar**|Clique em **começar**.|  

     Se ocorrerem erros ou avisos, consulte o documento de MDT *referência de resolução de problemas*.  

3.  No **resumo de implementação** caixa de diálogo, clique em **detalhes**.  

     Se tiver ocorrido quaisquer erros ou avisos, reveja os erros ou avisos e registe as informações de diagnóstico.  

4.  No **resumo de implementação** caixa de diálogo, clique em **concluir**.  

 As informações de migração de estado do utilizador são capturadas e são armazenadas na pasta de rede partilhada (UserStateCapture$) criada anteriormente no processo.  

### <a name="step-8-start-the-new-computer-with-the-lti-bootable-media"></a>Passo 8: Iniciar o novo computador com LTI suportes de dados  
 Inicie o novo computador (WDG-novo-02) com LTI suportes de dados criado anteriormente no processo. Este CD inicia o Windows PE no computador de referência e inicia o processo de implementação do MDT. No final do processo de implementação MDT, Windows Vista é implementado no novo computador e as informações de migração de estado de utilizador capturados são restauradas para o novo computador.  

> [!NOTE]
>  Também pode iniciar o processo de MDT ao iniciar o computador de destino a partir dos serviços de implementação do Windows. Para obter mais informações, consulte a secção "Preparar serviços de implementação", no documento MDT *utilizar o Microsoft Deployment Toolkit*.  

 **Para iniciar o novo computador com LTI suportes de dados**  

1.  Inicie WDG 02 novo com LTI suportes de dados criado anteriormente no processo.  

     Windows PE inicia e, em seguida, inicia o Assistente de implementação do Windows.  

2.  Conclua o Assistente de implementação do Windows, utilizando as seguintes informações. Aceite os valores predefinidos exceto indicação em contrário.  

    |**Na página do Assistente**|**Fazê-lo**|  
    |--|--|
    |**Bem-vindo à implementação**|Clique em **executar o Assistente de implementação para instalar um novo sistema operativo**e, em seguida, clique em **seguinte**.|  
    |**Especifique as credenciais para ligar a partilhas de rede.**|1.  No **nome de utilizador**, tipo **administrador**.<br />2.  No **palavra-passe**, tipo **P@ssw0rd**.<br />3.  No **domínio**, tipo **CORP**.<br />4.  Clique em **OK**.|  
    |**Selecione uma sequência de tarefas para executar neste computador.**|Clique em **efetuar substituir o cenário de computador no novo computador**e, em seguida, clique em **seguinte**.|  
    |**Configurar o nome do computador**|No **nome do computador**, tipo **WDG novo 02**e, em seguida, clique em **seguinte**.|  
    |**Associar o computador a um domínio ou grupo de trabalho**|Clique em **Seguinte**.|  
    |**Especifique se pretende restaurar dados de utilizador**|1.  Clique em **especificar uma localização**.<br />2.  No **localização**, tipo  **\\\WDG-MDT-01\UserStateCapture$\WDG-EXIST-01**.<br />3.  Clique em **Seguinte**.|  
    |**Seleção de região**|Clique em **Seguinte**.|  
    |**Definir o fuso horário**|Clique em **Seguinte**.|  
    |**Especifique se pretende capturar uma imagem**|Clique em **não capturar uma imagem deste computador**e, em seguida, clique em **seguinte**.|  
    |**Especificar a configuração do BitLocker**|Clique em **não ativar o BitLocker para este computador**e, em seguida, clique em **seguinte**.|  
    |**Pronto para começar**|Clique em **começar**.|  

     Se devem ocorrer erros ou avisos, consulte o documento de MDT *referência de resolução de problemas*.  

3.  No **resumo de implementação** caixa de diálogo, clique em **detalhes**.  

     Se tiver ocorrido quaisquer erros ou avisos, reveja os erros ou avisos e registe as informações de diagnóstico.  

4.  No **resumo de implementação** caixa de diálogo, clique em **concluir**.  

 Windows Vista está agora instalado no novo computador e as informações de migração de estado de utilizador capturados também são restauradas.  

## <a name="integrating-custom-deployment-code-into-mdt"></a>Integrar o código de implementação personalizada em MDT  
 É comum para uma equipa de implementação ter complexos requisitos, específicos ao seu respetivo ambiente de destino, que não são satisfeitos as ações de sequência de tarefas do Deployment Workbench predefinidas ou ficheiros de configuração do MDT predefinido. Nesta situação, implemente código personalizado para satisfazer os seus requisitos.  

 Integre o código de implementação personalizada no MDT por:  

-   Escolher uma linguagem de script, conforme descrito em [escolher o idioma de Scripting adequado](#ChooseAppropLanguage)  

-   Tirar partido ZTIUtility.vbs conforme descrito em [compreender como tire partido ZTIUtility](#UnderstandLeverageZTI)  

-   Integrar o código de implementação personalizada, tal como descrito no [integrar o código de implementação personalizada](#IntegrateCustomDeploy)  

 As secções seguintes partem do princípio de que o MDT é configurado num servidor de implementação.  

###  <a name="ChooseAppropLanguage"></a> Escolha a linguagem de scripts adequada  
 Embora qualquer código que pode ser executado no Windows ou no Windows PE pode ser chamado como instalação de uma aplicação ou através de um passo de sequência de tarefas do MDT, a Microsoft recomenda com scripts sob a forma de ficheiros. vbs ou .wsf.  

 A vantagem de utilizar ficheiros .wsf está incorporada de registo, além disso, para algumas funções predefinidas já utilizadas por processos ZTI e UDI LTI. Estas funções estão disponíveis no script ZTIUtility distribuído com o MDT.  

 Quando referenciado a partir de um script personalizado, o script de ZTIUtility inicializa as classes de ambiente e a configuração do MDT. Estas classes estão disponíveis:  

-   **Registo**. Esta classe fornece a funcionalidade de registo que utilizam todos os scripts de MDT. Também cria um único ficheiro de registo para cada script a executar durante a implementação e um ficheiro de registo consolidado de todos os scripts. Estes ficheiros de registo são criados num formato concebido para ser lidos por TRACE32; Esta ferramenta está disponível no [V2 de Toolkit do System Center Configuration Manager 2007](https://www.microsoft.com/download/en/details.aspx?id=9257).  

-   **Ambiente**. Esta classe configura as variáveis de ambiente recolhidas através do WMI e MDT processamento da regra e permite-lhes seja referenciado diretamente a partir do script. Isto permite que as propriedades de implementação a ser lido, conceder acesso a todas as informações de configuração utilizadas por processos ZTI e UDI LTI.  

-   **Utilitário**. Esta classe fornece utilitários gerais que são utilizados em toda a scripts ZTI e LTI. A Microsoft recomenda que qualquer código personalizado for desenvolvido esta classe de tempo deve ser examinado para ver se qualquer código simplesmente pode ser reutilizado. Informações adicionais sobre algumas das funcionalidades fornecidas esta classe estão incluídas posteriormente nesta secção.  

-   **Base de dados**. Esta classe efetua funções como ligar às bases de dados e ler informações de bases de dados. Em geral, aceder a classe de base de dados diretamente não se recomenda a; em vez disso, o processamento da regra deve ser utilizado para efetuar pesquisas de base de dados.  

-   **Cadeias**. Esta classe efetua rotinas de processamento de cadeia comuns, como criar uma lista delimitada de itens, que apresenta um valor hexadecimal, espaços em branco corte de uma cadeia, direito alinhar uma cadeia, à esquerda Alinhar uma cadeia, forçar um valor para o formato de cadeia, forçar um valor à matriz o formato, gerar um identificador de exclusivo global (GUID) aleatório e conversões de Base64.  

-   **FileHandling**. Esta classe executa funções como normalizing caminhos e copiar, mover e eliminar ficheiros e pastas.  

-   **clsRegEx**. Esta classe executa funções de expressão regular.  

 No MDT, faça algumas alterações foi implementada para a arquitetura de script para tornar o cliente do Microsoft Visual Basic® Scripting Edition (VBScript) mais robusto e fiável. Estas alterações incluem:  

-   Um vasto conjunto alterações ZTIUtility.vbs (biblioteca principal do script), incluindo novas APIs e maior processamento de erros  

-   Um aspeto novo para a estrutura geral da ZTI_*xxx*.wsf scripts  

 A estrutura geral dos MDT scripts também foi alterada. A maioria dos scripts de MDT são agora encapsulados dentro de VBScript **classe** objetos. A classe é inicializada e chamada com o **RunNewInstance** função.  

> [!NOTE]
>  A maioria dos scripts existentes do MDT 2008 Update 1 irão funcionar como-está a ser MDT, mesmo com as alterações mais extensas ZTIUtility.vbs, como a maioria dos scripts de MDT irão incluir ZTIUtility.vbs.  

###  <a name="UnderstandLeverageZTI"></a> Compreender como tirar partido das ZTIUtility  
 O ficheiro de ZTIUtility.vbs contém classes de objetos que podem ser aproveitadas no seu código personalizado. Integrar o código personalizado com o MDT utilizando o:  

-   Classe de registo definida ZTIUtility.vbs conforme descrito em [utilizar a classe de registo de ZTIUtility](#UseZTILogging)  

-   Classe de ambiente definida no ZTIUtility.vbs conforme descrito em [utilizar a classe de ambiente de ZTIUtility](#UseZTIEnvironment)  

-   Utilitário de classe definida ZTIUtility.vbs conforme descrito em [utilizar a classe de utilitário ZTIUtility](#UseZTIUtility)  

####  <a name="UseZTILogging"></a> Utilizar a classe de registo ZTIUtility  
 A classe de registo no ZTIUtiliy.vbs fornece um mecanismo simple para código personalizado para erros, avisos e informações de estado de registo da mesma forma que outros scripts durante uma implementação ZTI ou LTI. Este uniformização também garante que o **resumo de implementação LTI** caixa de diálogo corretamente comunica o estado de qualquer código personalizado que é executado.  

 O seguinte ilustra um script de código personalizado de exemplo que utiliza o **oLogging.CreateEntry** e **TestAndFail** funções para diferentes tipos de mensagens em fila, consoante os resultados dos vários de registo ações de script.  

 **Script de exemplo utilizando ZTIUtility registo: ZTI_Example.wsf**  

```  
<job id="ZTI_Example">  
<script language="VBScript" src="ZTIUtility.vbs"/>  
<script language="VBScript">  

' //*******************************************************  
' //  
' // Copyright (c) Microsoft Corporation.  All rights reserved  
' // Microsoft Deployment Toolkit Solution Accelerator  
' // File: ZTI_Example.wsf  
' //  
' // Purpose: Example of scripting with the  
' //          Microsoft Deployment Toolkit.  
' //  
' // Usage: cscript ZTI_Example.wsf [/debug:true]  
' //  
' //*******************************************************  

Option Explicit  
RunNewInstance  

'//--------------------------------------------------------  
'// Main Class  
'//--------------------------------------------------------  
Class ZTI_Example  

'//--------------------------------------------------------  
'// Main routine  
'//--------------------------------------------------------  

Function Main()  

  Dim iRetVal  
  Dim sScriptPath  

  iRetVal = SUCCESS  

  oLogging.CreateEntry "Begin example script…", _  
    LogTypeInfo  

  ' %ServerA% is a generic variable available within  
  ' every CustomSettings.ini file.  

  sScriptPath = "\\" & oEnvironment.Item("ServerA") & _  
    "\public\products\Applications\User\Technet\USEnglish"  

  ' Validate a connection to server, net connect with  
  ' credentials if necessary.  
  iRetVal = oUtility.ValidateConnection( sScriptPath )  
  TestAndFail iRetVal, 9991, "Validate Connection to [" & _  
    sScriptPath & "]"  

  'Run Setup Program  

  iRetVal = oUtility.RunWithHeartbeat( """" & _  
    sScriptPath & "\setup.exe"" /?" )  
  TestAndFail iRetVal, 9991, "RunWithHeartbeat [" & _  
    sScriptPath & "]"  

  'Perform any cleanup from installation process  

  oShell.RegWrite "HKLM\Software\Microsoft\SomeValue", _  
    "Done with Execution of XXX.", "REG_SZ"  

  Main = iRetVal  

End Function  

End Class  

</script>  
</job>  
```  

> [!NOTE]
>  Se pretender continuar a utilizar scripts que chamada **ZTIProcess()** com **ProcessResults()**, pode continuar a fazê-lo. No entanto, determinadas funcionalidades de processamento de erros avançadas não serão ativadas.  

####  <a name="UseZTIEnvironment"></a> Utilizar a classe de ambiente de ZTIUtility  
 A classe de ambiente no ZTIUtiliy.vbs fornece acesso a e a capacidade para atualizar as propriedades do MDT. Exemplo de que precede, **oEnvironment.Item("Memory")** é utilizado para obter a quantidade de RAM disponível; também pode ser utilizado para obter o valor de qualquer uma das propriedades descritas no documento MDT *Toolkit de referência* .  

####  <a name="UseZTIUtility"></a> Utilizar a classe de utilitário ZTIUtility  
 O script de ZTIUtility.vbs contém um número de utilitários frequentemente utilizados, que pode utilizar qualquer script de implementação personalizada. Pode adicionar estes utilitários qualquer script da mesma forma que o **oLogging** e **oEnvironment** classes.  

A tabela seguinte fornece detalhes sobre algumas funções útil disponíveis e o respetivo resultado. Para obter uma lista completa de funções disponíveis, consulte o ficheiro ZTIUtility.vbs.  

|**Função**|**Saída**|  
|-|-|
|**oUtility.LocalRootPath**|Devolve o caminho da pasta raiz que está a ser utilizada pelo processo de implementação no computador de destino — por exemplo, C:\MININT|  
|**oUtility.BootDevice**|Devolve o dispositivo de arranque do sistema — por exemplo, MULTI(0)DISK(0)RDISK(0)PARTITION(1)|  
|**oUtility.LogPath**|Devolve o caminho para a pasta de registos que está a ser utilizada durante a implementação — por exemplo, C:\MININT\SMSOSD\OSDLOGS|  
|**oUtility.StatePath**|Devolve o caminho do arquivo de estado atualmente configurados — por exemplo, C:\MININT\StateStore|  
|**oUtility.ScriptName**|Devolve o nome do script ao chamar a função — por exemplo, o Z-RAMTest|  
|**oUtility.ScriptDir**|Devolve o caminho para o script que está a chamar a função — por exemplo, \\\server_name\Deployment$\Scripts|  
|**oUtility.ComputerName**|Determina o nome do computador que será utilizado durante o processo de compilação — por exemplo, nome_do_computador|  
|**oUtility.ReadIni (ficheiro, secção, item)**|Permite que o item especificado para ler a partir de um ficheiro. ini|  
|**oUtility.WriteIni (ficheiro, secção, item, valor)**|Permite que o item especificado para ser escrito para um ficheiro. ini|  
|**oUtility.Sections(file)**|Lê as secções de um ficheiro. ini e armazena-os num objeto de referência|  
|**oUtility.SectionContents (ficheiro, secção)**|Lê o conteúdo do ficheiro. ini especificado e armazena-os num objeto|  
|**oUtility.RunWithHeartbeat(sCmd)**|Quando o comando é executado, escrever informações de heartbeat para os registos de cada 0.5 segundos|  
|**oUtility.FindFile**<br /><br /> **(sFilename,sFoundPath)**|Procura o ficheiro especificado na pasta DeployRoot e subpastas padrão, incluindo a manutenção, ferramentas, USMT, modelos, Scripts e controlo|  
|**oUtility.findMappedDrive(sServerUNC)**|Verifica se uma unidade está mapeada para o caminho UNC especificado e devolve a letra de unidade|  
|**oUtility.ValidateConnection(sServerUNC)**|Verifica se existe uma ligação ao servidor especificado e, se não existir, tenta criar um|  
|**MapNetworkDrive**<br /><br /> **(sShare, SDomID, sDomPwd)**|Mapeia uma letra de unidade para o caminho UNC especificado como a partilha e devolve a letra de unidade utilizada; Devolve um erro se sem êxito|  
|**VerifyPathExists(strPath)**|Verifica se o caminho especificado existe|  
|**oEnvironment.Substitute(sVal)**|Uma cadeia fornecida expande quaisquer variáveis ou funções dentro dessa cadeia|  
|**oEnvironment.Item**<br /><br /> **(sName)**|Lê ou escreve uma variável para um arquivo persistente|  
|**oEnvironment.Exists**<br /><br /> **(sName)**|Testa para verificar se a variável existe|  
|**oEnvironment.ListItem**<br /><br /> **(sName)**|Lê ou escreve uma variável do tipo **matriz** para um arquivo persistente|  
|**oLogging.ReportFailure**<br /><br /> **(sMessage, iError)**|Utilizado para efetuar uma saída estruturada se for detetado um erro irrecuperável|  
|**oLogging.CreateEvent**<br /><br /> **(iEventID iType, sMessage, arrParms)**|Escreve uma mensagem para o ficheiro de registo e envia o evento para um servidor definido|  
|**oLogging.CreateEntry**<br /><br /> **(sLogMsg, iType)**|Escreve uma mensagem para o ficheiro de registo|  
|**TestAndFail (iRc iError, sMessage)**|Sai o script com **iError** se **iRc** for false ou falhar|  
|**TestAndLog (iRc, sMessage)**|Regista um aviso apenas se for **iRc** for false ou falhar|  

###  <a name="IntegrateCustomDeploy"></a> Integrar o código de implementação personalizada  
 Código de implementação personalizadas pode ser integrado no processo de MDT de várias formas; No entanto, independentemente do método utilizado, as duas regras seguintes devem ser cumpridas:  

-   O nome de script de código de implementação personalizada sempre deve iniciar com a letra Z.  

-   O código de implementação personalizada deve ser colocado na pasta de Scripts na partilha de implementação — por exemplo, D:\Production Share\Scripts de implementação.  

 Os métodos mais frequentemente utilizados para integrar o código personalizado que certifique-se consistente registo também são:  

-   Implementar o código como uma aplicação de MDT  

-   Inicie o código como um comando de sequência de tarefas do MDT  

-   Inicie o código como um script de saída do utilizador  

#### <a name="deploy-custom-code-as-an-mdt-application"></a>Implementar código personalizado como uma aplicação de MDT  
 Código de implementação personalizada pode ser importado para o Deployment Workbench e gerido da mesma forma que qualquer outra aplicação.  

 **Para criar uma nova aplicação para executar o código de implementação personalizada**  

1.  Copie o código de implementação personalizada para o *deployment_share*\Scripts pasta (onde *deployment_share* é o caminho completamente qualificado para a partilha de implementação).  

2.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

3.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação /*deployment_share*/Applications (onde *deployment_share* é o nome da partilha de implementação para configurar).  

4.  No painel ações, clique em **nova aplicação**.  

     Inicia o Assistente de nova aplicação.  

5.  Conclua o Assistente de aplicação nova com as informações seguintes. Aceite as predefinições, a menos que especificado em contrário.  

    |**Na página do Assistente**|**Fazê-lo**|  
    |-|-|  
    |**Tipo de aplicação**|Clique em **aplicações sem ficheiros de origem ou noutro local na rede**e, em seguida, clique em **seguinte**.|  
    |**Detalhes**|Conclua esta página com as informações da aplicação e, em seguida, clique em **seguinte**.|  
    |**Detalhes do comando**|1.  No **linha de comandos** caixa, escreva **cscript.exe %SCRIPTROOT%\custom_code** (onde *custom_code* é o nome do código personalizado que tem sido desenvolvido).<br />2.  No **diretório de trabalho** caixa, escreva ***working_directory*** (onde working_directory é o nome do diretório de trabalho do código personalizado; isto é, geralmente, a mesma pasta que o especificado no **Linha de comandos** caixa).<br />3.  Clique em **Seguinte**.|  
    |**Resumo**|Certifique-se de que as definições de configuração estão corretas e, em seguida, clique em **seguinte**.|  
    |**Confirmação**|Clique em **Concluir**.|  

 A aplicação aparece no nó de aplicações no Deployment Workbench.  

#### <a name="add-the-custom-code-as-a-task-sequence-step"></a>Adicione o código personalizado como um passo de sequência de tarefas  
 Código de implementação personalizada pode ser chamado diretamente a partir de qualquer ponto dentro de uma sequência de tarefas; Isto proporciona acesso para as regras de sequência de tarefas habitual e as opções.  

 **Para adicionar o código de implementação personalizada a uma sequência de tarefas existente**  

1.  Copie o código de implementação personalizada para o *deployment_share*\Scripts pasta (onde *deployment_share* é o caminho completamente qualificado para a partilha de implementação).  

2.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

3.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*sequências de tarefas/deployment_share* (onde *deployment_share* é o nome da partilha de implementação para configurar ).  

4.  No painel de detalhes, clique em ***task_sequence*** (onde *task_sequence* é o nome da sequência de tarefas que executa o código personalizado).  

5.  No painel ações, clique em **propriedades**.  

6.  No ***task_sequenceProperties*** caixa de diálogo, clique em de **sequência de tarefas** separador.  

7.  Na árvore da consola, aceda a *grupo* (onde *grupo* é o grupo para adicionar o passo de sequência de tarefas).  

8.  Clique em **adicionar**, clique em **geral**e, em seguida, clique em **executar linha de comandos**.  

9. Na árvore da consola, clique em **executar linha de comandos**e, em seguida, clique em de **propriedades** separador.  

10. No **nome** caixa, escreva ***nome*** (onde *nome* é um nome descritivo do código personalizado).  

11. No **propriedades** separador o **linha de comandos** caixa, escreva ***command_line*** (onde *command_line* é o comando a executar o código personalizado — Por exemplo, **cscript.exe %SCRIPTROOT%\CustomCode.vbs**).  

12. No **iniciar no** caixa, escreva ***caminho*** (onde *caminho* é o caminho completamente qualificado para a pasta de trabalho do código personalizado; normalmente, este é o mesmo caminho especificado no  **Command line** caixa) e, em seguida, clique em **OK**.  

 O passo de sequência de tarefas recentemente criada aparece na lista dos passos de sequência de tarefas.  

#### <a name="run-custom-code-as-a-user-exit-script"></a>Executar código personalizado como um Script de saída do utilizador  
 Também é possível executar o código personalizado como um script de saída de utilizador do CustomSettings.ini com a **UserExit** diretiva. Isto fornece um mecanismo para obter informações para ser transmitido para o processo de validação de regras CustomSettings.ini e fornece uma atualização dinâmica de propriedades de MDT  

 Para mais informações sobre o utilizador saia scripts e **UserExit** diretiva, consulte a secção "Utilizador sair Scripts no ficheiro CustomSettings.ini", no documento MDT *utilizar o Microsoft Deployment Toolkit*.  

## <a name="installing-device-drivers-using-various-installation-methods"></a>Instalar controladores de dispositivo utilizando vários métodos de instalação  
 Neste cenário, utilizar o MDT para implementar um sistema operativo a diferentes tipos de hardware. Como parte do processo de implementação, identificar e instalar controladores de dispositivo, para que cada tipo de hardware irá funcionar corretamente. Existem dois principais tipos de controladores de dispositivo cada um tem de ser processada de forma durante o processo de implementação:  

-   Controladores de dispositivo que contêm um ficheiro. inf que pode ser utilizado para importar o controlador de dispositivo no Deployment Workbench  

-   Controladores de dispositivo que são empacotadas como uma aplicação e que tem de ser instalado como uma aplicação  

 Com o MDT, pode processar os dois tipos de controladores como parte da implementação do sistema operativo.  

 Instale controladores de dispositivo por:  

-   Determinar os métodos para instalar cada controlador de dispositivo, conforme descrito em [determinar qual o método a utilizar para instalar um controlador de dispositivo](#WhichMethodtoInstallDriver)  

-   Utilizando o método de controladores de out-of-box, conforme descrito em [instalar dispositivo controladores utilizando o método de controladores de Out-of-Box](#InstallOutofBoxDrivers)  

-   Instalação dos mesmos como aplicações, conforme descrito em [instalar controladores de dispositivo que as aplicações](#InstallDriversasApplications)  

 Este cenário pressupõe que o MDT está em execução num servidor de implementação.  

###  <a name="WhichMethodtoInstallDriver"></a> Determinar qual o método a utilizar para instalar um controlador de dispositivo  
 Fabricantes de hardware versão controladores de dispositivo de uma das duas formas:  

-   Como um pacote que pode extrair e que contém ficheiros de ficheiro. inf utilizados para importar o controlador para o Deployment Workbench  

-   Como uma aplicação que tem de instalar através de processos de instalação de aplicação tradicionais  

 Pacotes de controladores de dispositivo que podem ser extraídos para aceder aos ficheiros de ficheiro. inf podem utilizar o processo de deteção e instalação de controlador automática do MDT ao primeiro importar o controlador para o nó de Out-of-Box controladores no Deployment Workbench.  

 Pacotes de controladores de dispositivo que não não possível extrair para isolar os ficheiros de ficheiro. inf ou que não funcionam corretamente sem primeiro a ser instalados com um instalador da aplicação como um ficheiro MSI ou Setup.exe podem utilizar a funcionalidade de MDT instalar aplicação e instale o dispositivo controlador durante o processo de implementação apenas para qualquer aplicação normal.  

###  <a name="InstallOutofBoxDrivers"></a> Instalar controladores de dispositivo utilizando o método de controladores  
 Pode importar pacotes de controladores de dispositivo que incluem um ficheiro. inf para Deployment Workbench e instalação-los automaticamente como parte do processo de implementação. Para implementar este tipo de implementação de controladores de dispositivo, adicione primeiro o controlador de dispositivo ao Deployment Workbench.  

 **Para adicionar o controlador de dispositivo ao Deployment Workbench**  

1.  Transfira os controladores de dispositivo necessários para os tipos de hardware para ser implementado e extraia o pacote de controladores de dispositivo para uma localização temporária.  

2.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

3.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share*/Out-of-Box controladores (onde *deployment_share* é o nome da partilha de implementação para Configure).  

4.  No painel ações, clique em **importar controladores**.  

     Inicia o Assistente de controladores de dispositivo de importação.  

5.  No **especificar diretório** na página a **unidade origem** secção do diretório, clique em **procurar** Ir para a pasta que contém os novos controladores de dispositivo e, em seguida, clique em  **Seguinte**.  

    > [!NOTE]
    >  O Assistente de novo controlador de dispositivo irá procurar todos os subdiretórios do diretório de origem de controlador; Por conseguinte, se existirem várias controladores a instalar, extraia-los para pastas no mesmo diretório de raiz e, em seguida, defina o controlador de diretório de origem como o diretório de raiz que contém todos os do controlador de pastas de origem.  

6.  No **resumo** página, certifique-se de que as definições estão corretas e, em seguida, clique em **seguinte** para importar os controladores para o Deployment Workbench.  

7.  No **confirmação** página, clique em **concluir**.  

 Se os controladores de dispositivo contém controladores críticos de arranque, como o armazenamento em massa ou controladores de classe de rede, a partilha de implementação seguinte deve ser atualizada para gerar um ambiente de arranque LiteTouch_x86 e LiteTouch_x64 novo que contém os novos controladores.  

 **Para adicionar controladores de dispositivo para as imagens de Lite Windows Touch PE**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share* (onde *deployment_share* é o nome da partilha de implementação para configurar).  

3.  No painel ações, clique em **partilha de implementação de atualização**.  

     Inicia o Assistente de partilha de implementação da atualização.  

4.  No **opções** página, selecione as opções pretendidas para atualizar a partilha de implementação e, em seguida, clique em **seguinte**.  

5.  No **resumo** página, certifique-se de que os detalhes estão corretos e, em seguida, clique em **seguinte**.  

6.  No **confirmação** página, clique em **concluir**.  

###  <a name="InstallDriversasApplications"></a> Instalar controladores de dispositivo que as aplicações  
 Controladores de dispositivo que estão empacotadas como aplicações e que não é possível extrair para uma pasta que contém um ficheiro. inf, para além dos ficheiros de controlador, devem ser adicionados ao Deployment Workbench como uma aplicação para a instalação durante o processo de implementação.  

 As aplicações podem ser especificadas como um passo de sequência de tarefas ou especificadas no CustomSettings.ini; No entanto, as aplicações de controladores de dispositivo devem ser instaladas apenas quando a sequência de tarefas é executada num computador com os dispositivos. Para garantir que isto, execute o passo de sequência de tarefas para implementar as aplicações de controladores de dispositivo relevante como um passo de sequência de tarefas condicional. Os critérios condicionais podem ser especificados para executar o passo de sequência de tarefas através de consultas WMI para o dispositivo no computador de destino.  

#### <a name="add-the-device-driver-application-to-the-deployment-workbench"></a>Adicionar a aplicação de controladores de dispositivo no Deployment Workbench  
 Cada aplicação de controladores de dispositivo primeiro tem de ser importada para o Deployment Workbench.  

> [!NOTE]
>  Configurar se a aplicação deve está visível durante a implementação no **propriedades** caixa de diálogo de qualquer aplicação, selecionando ou desmarcando a **ocultar esta aplicação no Assistente de implementação** caixa de verificação. Repita este processo para cada aplicação de controladores de dispositivo utilizada durante a implementação.  

 **Para adicionar a aplicação de controladores de dispositivo no Deployment Workbench**  

1.  Transferir a aplicação de controladores de dispositivo e guardá-lo para uma localização temporária.  

2.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

3.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share*/Applications (onde *deployment_share* é o nome da partilha de implementação para configurar) .  

4.  No painel ações, clique em **nova aplicação**.  

     Inicia o Assistente de nova aplicação.  

5.  No **tipo de aplicação** página, clique em **aplicação com ficheiros de origem**e, em seguida, clique em **seguinte**.  

6.  No **detalhes** página, escreva os detalhes relevantes sobre a aplicação e, em seguida, clique em **seguinte**.  

7.  No **origem** na página **o diretório de origem** secção, clique em **procurar** para aceder à e, em seguida, clique no diretório que contém os ficheiros de origem da aplicação de controladores de dispositivo. Clique em **OK**.  

8.  Clique em **Seguinte**.  

9. No **destino** página, escreva um nome para o diretório de destino e, em seguida, clique em **seguinte**.  

10. No **detalhes do comando** na página de **linha de comandos** secção, digite o comando que permite a instalação automática da aplicação de controladores de dispositivo.  

11. No **resumo** página, verifique as definições estão corretas e, em seguida, clique em **seguinte** para importar a aplicação de controladores de dispositivo no Deployment Workbench.  

12. No **confirmação** página, clique em **concluir**.  

 Depois das aplicações são importadas para o Deployment Workbench, adicioná-los para o processo de implementação utilizando a lógica adequada para se certificar de que a aplicação é instalada apenas quando executado no hardware correto. Existem vários métodos para alcançar isto:  

-   Especifique a aplicação de controladores de dispositivo como parte da sequência de tarefas de implementação.  

-   Especifique a aplicação de controladores de dispositivo CustomSettings.ini.  

-   Especifique a aplicação de controladores de dispositivo na base de dados do MDT.  

 Cada abordagem é abordada mais detalhadamente nas secções seguintes.  

####  <a name="SpecifyDeviceAppTask"></a> Especifique a aplicação de controladores de dispositivo como parte da sequência de tarefas  
 O primeiro método para adicionar uma aplicação de controladores de dispositivo para o processo de implementação é utilizar uma sequência de tarefas para adicionar os passos para cada aplicação de controladores de dispositivo.  

 Existem duas abordagens de principais de gestão de aplicações de controladores de dispositivo na sequência de tarefas:  

-   Criar um novo grupo de sequência de tarefas para cada modelo de hardware e, em seguida, adicione uma consulta para executar ações que o grupo se o computador corresponder a um tipo de hardware específico.  

-   Criar um grupo de sequência de tarefas para aplicações de hardware específico e, em seguida, adicione as consultas para cada ação de sequência de tarefas para que cada passo de sequência de tarefas é avaliado em comparação com o tipo de hardware e será executada apenas se for encontrada uma correspondência.  

 **Para criar um novo grupo de sequência de tarefas para cada tipo de hardware**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share*/Task sequências (onde *deployment_share* é o nome da partilha de implementação para configurar ).  

3.  No painel de detalhes, clique em ***task_sequence*** (onde *task_sequence* é a sequência de tarefas de implementação que irá ser necessário instalar a aplicação de controladores de dispositivo).  

4.  No painel ações, clique em **propriedades**.  

5.  No ***task_sequenceProperties*** caixa de diálogo a **sequência de tarefas** separador, no painel de detalhes, aceda ao estado de Restauro/Windows Update (pré-aplicações de instalação).  

6.  No **sequência de tarefas** separador, clique em **adicionar**e, em seguida, clique em **novo grupo**.  

     Esta ação cria um novo grupo de sequência de tarefas na sequência de tarefas. Utilize este novo grupo de sequência de tarefas para criar os passos para instalar as aplicações de controladores de dispositivo de hardware específico.  

7.  No painel de detalhes, clique em **novo grupo**.  

8.  No **propriedades** separador o **nome** caixa, escreva ***group_name*** (onde *group_name* é o nome do grupo; por exemplo, *Aplicações específicas do hardware – Dell computador Corporation*).  

9. No **opções** separador, clique em **adicionar**e, em seguida, clique em **consulta WMI**.  

10. No **condição de WMI de sequência de tarefas** diálogo caixa, escreva os seguintes detalhes:  

    -   No **espaço de nomes WMI** caixa, escreva **root\cimv2**.  

    -   No **consulta WQL** caixa, escreva uma consulta de linguagem WQL (WMI Query) utilizando o **Win32_ComputerSystem** classe para se certificar de que a aplicação é instalada apenas para um tipo específico de aplicação — por exemplo:  

         **Selecione \* de Win32_ComputerSystem onde modelo como *% hardware_model %* e fabricante como *% hardware_manufacturer %***  

         Neste exemplo, *hardware_model* é o nome do modelo de computador (por exemplo, Latitude D620) e *hardware_manufacturer* igualmente o nome do computador (por exemplo, a Dell Corporation).  

         O **%** símbolo é o caráter universal que está incluído nos nomes para permitir aos administradores devolver quaisquer modelos de computador ou manufactures que contém o valor especificado para ***hardware_model***ou ***hardware_manufacturer***.  

     Para obter mais informações sobre consultas do WMI e WQL, consulte a secção "Adicionar WMI consultas para sequência passo condições da tarefa", no documento MDT *utilizar o Microsoft Deployment Toolkit*e ver [consultar com WQL](http://msdn.microsoft.com/library/aa392902.aspx).  

11. Clique em **OK** submeter a consulta e, em seguida, clique em **OK** para submeter as alterações à sequência de tarefas.  

> [!NOTE]
>  Este processo tem de ser repetido para cada tipo de hardware de cada aplicação de controladores de dispositivo para ser instalada.  

 Depois da tarefa de hardware específico grupos de sequências de ter sido criado, controlador de dispositivo de aplicações podem ser adicionadas a cada grupo.  

 **Para adicionar aplicações de controladores de dispositivo para grupos de sequências de tarefas de hardware específico**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share*/Task sequências (onde *deployment_share* é o nome da partilha de implementação para configurar ).  

3.  No painel de detalhes, clique em ***task_sequence*** (onde *task_sequence* é a sequência de tarefas de implementação que irá ser necessário instalar a aplicação de controladores de dispositivo).  

4.  No painel ações, clique em **propriedades**.  

5.  No ***task_sequenceProperties*** caixa de diálogo, clique em de **sequência de tarefas** separador.  

6.  No painel de detalhes, aceda ao restauro do estado /*hardware_specific_group* (onde *hardware_specific_group* é o nome do grupo de hardware específico onde será adicionado o passo de sequência de tarefas para instalar o aplicação de controladores de dispositivo).  

7.  No **sequência de tarefas** separador, clique em **adicionar**, clique em **geral**e, em seguida, clique em **instalar aplicação**.  

     O **instalar aplicação** passo de sequência de tarefas é apresentado no painel de detalhes.  

8.  No painel de detalhes, clique em **instalar aplicação.**  

9. No **propriedades** separador, clique em **instalar uma única aplicação**e, no **aplicação a instalar** lista, selecione ***hardware_application***(onde *hardware_application* é a aplicação para instalar a aplicação de hardware específico).  

> [!NOTE]
>  Este processo tem de ser repetido para cada aplicação de controladores de dispositivo que tem de ser utilizada durante uma implementação.  

#### <a name="specify-the-device-driver-application-in-customsettingsini"></a>Especifique a aplicação de controladores de dispositivo no CustomSettings.ini  
 Quando começa uma implementação LTI ou ZTI, uma das primeiras ações seja concluída é o processamento dos ficheiros de controlo BootStrap.ini e CustomSettings.ini. Ambos estes ficheiros contêm regras que podem ser utilizadas para personalizar dinamicamente a implementação.  

 Devido à forma como o MDT processa ficheiro CustomSettings.ini, pode utilizá-lo para adicionar aplicações com base nas condições específicas. Esta lógica será utilizada para adicionar aplicações para dispositivos específicos – controlador durante a implementação com base nos tipos de hardware específico. As aplicações são referenciadas na CustomSettings.ini pelo GUID da aplicação, localizada no ficheiro Applications.xml na partilha de implementação.  

 **Para localizar o GUID de uma aplicação importada**  

1.  Na partilha de implementação do servidor de implementação, abra a pasta de controlo — por exemplo, D:\Production Share\Control de implementação.  

2.  Localize e abra o ficheiro Applications.xml.  

3.  Localize a aplicação necessária.  

4.  Localize a GUID da aplicação através da localização da linha entre a aplicação `<guid>` etiquetas; por exemplo, `<application guid={c303fa6e-3a4d-425e-8102-77db9310e4d0}>`.  

 Como parte do processo de inicialização, o processo LTI tanto ZTI recolher informações sobre o computador no qual está a ser executado. Como parte deste processo, são realizadas consultas do WMI e os valores do **Win32_ComputerSystem** classe para a marca e do fabricante são povoadas como variáveis **% disponibilizar %** e **% % de modelo,** respetivamente.  

 Estes valores podem ser utilizados durante o processamento do ficheiro CustomSettings.ini dinamicamente ler secções do ficheiro, consoante a marca e modelo detetado.  O exemplo seguintes mostra um exemplo do ficheiro CustomSettings.ini.  

 **CustomSettings.ini configurado para uma instalação de Hardware específico de aplicação de exemplo**  

```  
[Settings]  
Priority=Make, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  

[Dell Computer Corporation]  
Subsection=Dell-%Model%  

[Dell-Latitude D620]  
MandatoryApplications001={1D7DF331-47B7-472C-87B3-442597EC2F7D}  

[Dell-Latitude D610]  
MandatoryApplications001={c303fa6e-3a4d-425e-8102-77db9310e4d0}  
```  

 Utilize as seguintes propriedades para especificar as aplicações em CustomSettings.ini:  

-   **Aplicações**. Esta propriedade pode ser utilizada quando os administradores de implementação não pretendem apresentar um Assistente de aplicação como parte do processo de implementação, especificando **SkipApplications = YES** no CustomSettings.ini.  

-   **MandatoryApplications**. Esta propriedade pode ser utilizada se pretendem que os administradores de implementação apresentar o Assistente de aplicação durante a implementação para permitir que os engenheiros de implementação selecionar aplicações adicionais para ser instalado durante a implementação.  

     Se o Assistente de aplicação é utilizado sem a **MandatoryApplications** propriedade (por exemplo, **SkipApplications = não**), irá substituir aplicações especificadas pelo **aplicações**  propriedade.  

     O sampole previousi mostra como utilizar o **% disponibilizar %** e **% modelo %** valores das variáveis para manipular dinamicamente como é criada a lista de aplicações. Os valores da marca e modelo de cada tipo de hardware podem ser localizados utilizando um dos seguintes métodos:  

-   **A ferramenta de informações do sistema**. Utilize o nó de resumo do sistema Esta ferramenta para identificar o **fabricante do sistema** (certifique-) e **modelo de sistema** (modelo).  

-   **Windows PowerShell**. Utilize o **Get-WMIObject – classe Win32_ComputerSystem** cmdlet para determinar a marca e modelo do computador.  

-   **Linha de comandos do Windows Management Instrumentation**. Utilize **CSProduct obter o nome, fabricante** para devolver o nome (modelo) e o fornecedor (disponibilizar) do computador.  

 **Para modificar CustomSettings.ini adicionem lógica de hardware específico**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share* (onde *deployment_share* é o nome da partilha de implementação para configurar).  

3.  No painel ações, clique em **propriedades**.  

4.  Clique em de **regras** separador.  

5.  Informações escritas neste separador são armazenadas no ficheiro CustomSettings.ini. Modificar as entradas do ficheiro CustomSettings.ini adicionem lógica para cada modelo de hardware que tem uma aplicação de controlador – específicos do dispositivo, conforme descrito em [especificar a aplicação de controladores de dispositivo como parte da sequência de tarefas](#SpecifyDeviceAppTask).  

6.  Clique em **OK** para submeter as alterações.  

7.  No painel de detalhes, clique em *deployment_share* (onde *deployment_share* é o nome da partilha de implementação para configurar).  

8.  No painel ações, clique em **partilha de implementação de atualização**.  

     Inicia o Assistente de partilha de implementação da atualização.  

9. No **opções** página, selecione as opções pretendidas para atualizar a partilha de implementação e, em seguida, clique em **seguinte**.  

10. No **resumo** página, verifique os detalhes estão corretos e, em seguida, clique em **seguinte**.  

11. No **confirmação** página, clique em **concluir**.  

 Por predefinição, todas as aplicações disponíveis são apresentadas no Assistente de implementação do Windows durante uma implementação LTI. Porque as aplicações de controlador específicas do dispositivo são aplicáveis apenas a tipos específicos de hardware, que poderá não quer que eles apresentado sempre. Ao especificar o pacote de aplicação – específicas do controlador de dispositivo no CustomSettings.ini, a aplicação pode ser ocultada utilizando o **ocultar a aplicação no Assistente de implementação** opção na configuração de aplicação.  

 **Para ocultar uma aplicação no Assistente de implementação**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share*/Applications (onde *deployment_share* é o nome da partilha de implementação para configurar) .  

3.  No painel de detalhes, clique em ***device_driver_application*** (onde *device_driver_application* é a aplicação de ficar ocultas a partir do Assistente de implementação).  

4.  No painel ações, clique em **propriedades**.  

5.  No **geral** separador, selecione o **ocultar a aplicação no Assistente de implementação** caixa de verificação.  

6.  Clique em **aplicar**e, em seguida, feche o **propriedades** caixa de diálogo.  

#### <a name="specify-the-device-driver-application-in-the-mdt-db"></a>Especifique a aplicação de controladores de dispositivo na base de dados do MDT  
 A BD do MDT é uma versão de base de dados do ficheiro CustomSettings.ini e podem ser consultada no momento da implementação para obter informações a serem utilizadas durante a implementação. Para obter mais informações sobre a utilização da base de dados do MDT, consulte "Selecionar os métodos para aplicar as definições de configuração".  

 Ao consultar a base de dados do MDT no momento da implementação, três métodos estão disponíveis para identificar o computador de destino:  

-   Pesquisa para o computador individual (utilizando o endereço MAC, etiqueta de recursos, ou semelhante).  

-   Procure a localização do computador (utilizando o gateway predefinido).  

-   Procure a marca e modelo do computador (utilizando o fabricante WMI ou consultas marca e modelo).  

 Para cada entrada de base de dados cria, pode especificar propriedades de implementação, aplicações, se pretende utilizar pacotes do Configuration Manager e os administradores. Ao criar a marca e modelo de entradas na base de dados, pode adicionar as aplicações de controladores de dispositivos de hardware específico necessários.  

 **A criação de entradas na base de dados MDT para permitir a instalação do dispositivo de aplicações de controlador**  

> [!NOTE]
>  Repita este processo para cada marca de hardware e o modelo que necessita de uma aplicação de controladores de dispositivo.  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /**deployment_share**avançadas da base de dados/configuração/marca e modelo (onde *deployment_share* é o nome da partilha de implementação para configurar).  

3.  No painel ações, clique em **novo**.  

4.  No **propriedades** caixa de diálogo a **identidade** separador o **tornar** caixa, escreva ***make_name*** (onde *make_name*  é um nome facilmente identificado para associar o fabricante do computador de destino).  

5.  No **modelo** caixa, escreva ***model_name*** (onde *model_name* é um nome facilmente identificado para associar o modelo do computador de destino).  

6.  No **aplicações** separador, adicionar cada uma das aplicações de controladores de dispositivo necessárias para este modelo de hardware.  

## <a name="initiating-mdt-using-windows-deployment-services"></a>Iniciar o MDT utilizar serviços de implementação do Windows  
 Windows Server 2008 utiliza serviços de implementação do Windows, como uma versão atualizada e reestruturada dos serviços de instalação remota, a ferramenta de implementação predefinidos no Windows Server 2003 com SP2. Utilizar serviços de implementação do Windows, pode implementar sistemas operativos Windows — particularmente Windows 7, Windows Server 2008 ou sistemas operativos posteriores — através de uma rede utilizando com PXE ativado rede arranque ou de adaptador de suporte de dados um computador.  

 Antes de implementar os serviços de implementação do Windows, determine quais as seguintes opções de integração melhor se adequa aos ambiente:  

-   Opção 1. Computadores de arranque PXE para iniciar o processo LTI.  

-   Opção 2. Implemente uma imagem de sistema operativo a partir do arquivo de imagens dos serviços de implementação do Windows.  

-   Opção 3. Utilize multicast com o MDT e a função de servidor Serviços de implementação do Windows do Windows Server 2008.  

### <a name="option-1-boot-computers-in-pxe-to-initiate-the-lti-process"></a>Opção 1: Computadores de arranque de PXE para iniciar o processo LTI  
 Ajude a minimizar o custo de gerir implementações do sistema operativo ao iniciar o processo de implementação do MDT com serviços de implementação do Windows em conjunto com Dynamic Host Configuration Protocol. Esta ação remove o requisito de criação e distribuição de suportes de dados para cada computador de destino.  

#### <a name="create-and-import-the-deployment-workbench-windows-pe-image-into-windows-deployment-services"></a>Criar e importar a imagem do Windows PE do Workbench a implementação para serviços de implementação do Windows  
 Quando criar uma nova partilha de implementação do MDT ou modificar uma implementação existente do MDT partilhar, pode criar uma imagem de arranque personalizada do Windows PE. Quando a partilha de implementação é atualizada, a imagem de arranque do Windows PE é automaticamente gerada e atualizada com informações sobre a partilha de implementação e irá inserir quaisquer controladores adicionais ou especificados durante a configuração de partilha de implementação de componentes.  

 Imagem de arranque do Windows PE é gerada como um ficheiro de imagem ISO, que pode escrever um CD ou DVD, e ficheiros WIM de arranque. Pode importar o ficheiro WIM aos serviços de implementação do Windows para que os computadores que podem efetuar o arranque no PXE podem transferir e executar a imagem de arranque LTI Windows PE através de uma rede utilizada para inicializar uma instalação.  

 **Para criar uma imagem de arranque do Windows PE no Deployment Workbench**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share* (onde *deployment_share* é o nome da partilha de implementação para configurar).  

3.  No painel ações, clique em **propriedades**.  

     No ***deployment_shareProperties*** caixa de diálogo, clique em de **do Windows PE *plataforma* definições** separador (em que plataforma é a arquitetura da imagem do Windows PE para ser configurada).  

4.  No **Lite Touch imagem as definições de arranque** área, selecione o **gerar uma Lite Touch RAM disco ISO imagem de arranque** caixa de verificação.  

5.  Clique em de **do Windows PE *plataforma* componentes** separador (onde *plataforma* é a arquitetura da imagem do Windows PE para ser configurado).  

6.  No **Injeção de controlador** secção, clique nos tipos de controladores adequados para incluir.  

    > [!NOTE]
    >  Este passo não é necessário se o Windows PE já inclua os controladores de dispositivo necessários.  

7.  No **Injeção de controlador** na secção de **perfil seleção** lista, selecione o perfil de seleção de controlador adequado.  

8.  No **propriedades** caixa de diálogo, clique em **OK**.  

    > [!NOTE]
    >  Este passo não é necessário se o Windows PE já inclua os controladores de dispositivo necessários.  

9. No painel de detalhes, clique em ***deployment_share*** (onde *deployment_share* é o nome da partilha de implementação para configurar).  

10. No painel ações, clique em **partilha de implementação de atualização**.  

     Inicia o Assistente de partilha de implementação da atualização.  

11. No **opções** página, selecione as opções pretendidas para atualizar a partilha de implementação e, em seguida, clique em **seguinte**.  

12. No **resumo** página, verifique os detalhes estão corretos e, em seguida, clique em **seguinte**.  

13. No **confirmação** página, clique em **concluir**.  

     Quando este processo estar concluído, a pasta de arranque na partilha de implementação irá conter um número de imagens de arranque — por exemplo:  

     D:\Production Deployment Share\Boot\LiteTouchPE_x64.iso  

     D:\Production implementação Share\Boot\LiteTouchPE_x64.wim  

     D:\Production implementação Share\Boot\LiteTouchPE_x86.iso  

     D:\Production implementação Share\Boot\LiteTouchPE_x86.wim  

 Pode escrever ficheiros ISO que tenham sido gerados diretamente CD ou DVD ou utilizá-los para iniciar o processo LTI num novo hardware. Pode importar os ficheiros WIM de arranque para serviços de implementação do Windows, também, para que os novos computadores podem iniciar o processo de implementação LTI sem necessidade de qualquer suporte de dados físico.  

 **Para importar a imagem do Windows PE para serviços de implementação do Windows**  

1.  Inicie a consola de serviços de implementação do Windows e, em seguida, ligar aos serviços de implementação do Windows.  

2.  Na árvore da consola, faça duplo clique **imagens de arranque**e, em seguida, clique em **adicionar imagem de arranque**.  

3.  Navegue para a imagem WIM importar — por exemplo, o D:\Production implementação Share\Boot\LiteTouchPE_x86.wim.  

4.  O processo de importação lê automaticamente os metadados da imagem de arranque, mas o **nome da imagem** e **descrição da imagem** também podem ser editados valores; o **nome da imagem** afeta as informações de opção de arranque apresentadas pelo Gestor de arranque do Windows quando o cliente arranca no PXE.  

5.  Quando a imagem de arranque tiver sido importada, qualquer computador que arranca no PXE e recebe uma resposta de serviços de implementação do Windows será possível transferir a imagem de arranque LTI e iniciar uma instalação de LTI.  

 Instalar e configurar os serviços de implementação do Windows não é abordada neste guia. Para obter informações adicionais sobre os serviços de implementação do Windows, consulte o [guia de serviços de implementação do Windows](http://technet.microsoft.com/library/cc265612.aspx).  

#### <a name="use-windows-deployment-services-to-automatically-detect-the-deployment-server"></a>Utilizar os serviços de implementação do Windows para detetar automaticamente o servidor de implementação  
 Uma opção adicional está disponível ao utilizar serviços de implementação do Windows para imagens de arranque do anfitrião MDT quando a partilha de implementação do MDT que está alojada no mesmo servidor que serviços de implementação do Windows.  

 Quando um cliente PXE carrega a imagem de arranque do MDT, o nome do servidor de serviços de implementação do Windows que aloja a imagem de arranque é capturado e colocado no MDTProperty **WDSServer**. Em seguida, pode referenciar esta propriedade no ficheiro BootStrap.ini da imagem de arranque e no ficheiro CustomSettings.ini de partilha de implementação pelo **DeployRoot** propriedade. Se o fizer, resulta num cliente de que efetua o arranque dos serviços de implementação do Windows automaticamente utilizando a partilha de implementação alojada no servidor de serviços de implementação do Windows. Isto elimina a necessidade de especificar um nome de servidor em qualquer ficheiro de configuração.  

 **Configurar o servidor de serviços de implementação do Windows local como o servidor de implementação**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share*avançadas de configuração/base de dados (onde *deployment_share* é o nome do partilha de implementação para configurar).  

3.  No painel ações, clique em **propriedades**.  

4.  Clique em de **regras** separador.  

     Informações escritas neste separador são armazenadas no ficheiro CustomSettings.ini.  

5.  Configurar o **DeployRoot** propriedade para utilizar o **% WDSServer %** variável — por exemplo, **DeployRoot =\\\\%WDSServer%\Deployment$**.  

6.  Clique em **editar Bootstrap.ini**.  

7.  Configurar BootStrap.ini para utilizar o **% WDSServer %** propriedade por adicionar ou alterar o **DeployRoot** valor **DeployRoot =\\\\%WDSServer%\Deployment$** .  

8.  No **ficheiro** menu, clique em **guardar** para guardar as alterações ao ficheiro BootStrap.ini.  

9. Clique em **OK**.  

     A partilha de implementação tem de ser atualizado.  

10. No painel de detalhes, clique em **deployment_share** (onde *deployment_share* é o nome da partilha de implementação para configurar).  

11. No painel ações, clique em **partilha de implementação de atualização**.  

     Inicia o Assistente de partilha de implementação da atualização.  

12. No **opções** página, selecione as opções pretendidas para atualizar a partilha de implementação e, em seguida, clique em **seguinte**.  

13. No **resumo** página, verifique os detalhes estão corretos e, em seguida, clique em **seguinte**.  

14. No **confirmação** página, clique em **concluir**.  

15. Importe o WIM de arranque atualizada para serviços de implementação do Windows.  

### <a name="option-2-deploy-an-operating-system-image-from-the-windows-deployment-services-store"></a>Opção 2: Implementar uma imagem de sistema operativo a partir da loja de serviços de implementação do Windows  
 Se já estiver a utilizar serviços de implementação do Windows para implementação do sistema operativo, expandir a funcionalidade do MDT, configurando-o para referenciar as imagens de sistema operativo de serviços de implementação do Windows já em utilização em vez de utilizar o seu próprio arquivo e para complementar as implementações de serviços de implementação do Windows com a gestão de controladores, implementação de aplicações, instalação da atualização, processamento da regra e outras funcionalidades do MDT. Depois do MDT tem de referenciar uma imagem de sistema operativo de serviços de implementação do Windows, pode tratá-la como qualquer sistema operativo tiver sido testado para uma partilha de implementação do MDT.  

 **Para fazer referência a uma imagem de sistema operativo de serviços de implementação do Windows**  

> [!NOTE]
>  Os seguintes passos requerem que pelo menos uma imagem do sistema operativo anteriormente foi importada para o servidor de serviços de implementação do Windows.  

1.  Atualize o MDT para poder aceder a imagens de serviços de implementação do Windows ao copiar os seguintes ficheiros da pasta de origens de suportes de dados do Windows para a pasta C:\Program Files\Microsoft implementação Toolkit\bin no servidor de serviços de implementação do Windows:  

    -   Wdsclientapi.dll  

    -   Wdscsl.dll  

    -   Wdsimage.dll  

    -   Wdstptc.dll (isto é apenas aplicável se copiar entre os diretórios de origem do Windows Server 2008)  

    > [!NOTE]
    >  O diretório de origem do Windows que está a ser utilizado tem de corresponder da plataforma do sistema operativo em execução no computador onde está instalado o MDT.  

2.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

3.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share*/Operating Systems (onde *deployment_share* é o nome da partilha de implementação para Configure).  

4.  No painel ações, clique em **sistema de operativo importação**.  

     O novo Assistente de SO for iniciado.  

5.  No **tipo de SO** página, clique em **imagens dos serviços de implementação do Windows**e, em seguida, clique em **seguinte**.  

6.  No **servidor WDS** , escreva o nome do servidor de serviços de implementação a ser referenciado — por exemplo, **WDSSvr001**— e, em seguida, clique em **seguinte**.  

7.  No **resumo** página, verifique as definições estão corretas e, em seguida, clique em **seguinte**.  

8.  No **confirmação** página, clique em **concluir**.  

     Todas as imagens disponíveis no servidor de serviços de implementação do Windows estarão agora disponíveis para as sequências de tarefas do MDT.  

> [!NOTE]
>  A importação de imagens de implementação dos serviços do Windows não copia os ficheiros de origem do servidor de serviços de implementação do Windows para a partilha de implementação. MDT continua a utilizar os ficheiros de origem a partir da respetiva localização original.  

### <a name="option-3-use-multicasting-with-mdt-and-the-windows-server-2008-windows-deployment-services-role"></a>Opção 3: Utilizar multicast com o MDT e a função de serviços de implementação do Windows Server 2008 Windows  
 Com a versão do Windows Server 2008, os serviços de implementação do Windows foi melhorado para suportar a implementação de imagens com as transmissões de multicast. MDT também inclui atualizações para integrar o MDT com multicast de serviços de implementação do Windows.  

 Além disso, um atualizado Windows Automated Installation Kit (Windows AIK), versão 1.1, inclui Wdsmcast.exe. Isto permite sessões multicast de ser manualmente associados e permite que o cliente iniciar Wdsmcast.exe para copiar ficheiros de uma sessão ativa de multicast.  

 O script de LTIApply.wsf utiliza Wdsmcast.exe quando acede a ficheiros de origem do sistema operativo da partilha de implementação. LTIApply.wsf aspeto que tem para Wdsmcast.exe na implementação da partilha tem o *deployment_share*\Tools\x86 ou *deployment_share*\Tools\x64 pasta (onde *deployment_share* é o nome da pasta de sistema de ficheiro que contém a partilha de implementação), consoante a versão do Windows PE, que está em execução.  

 Quando executa LTIApply.wsf sempre a tentativa de aceder e transferir imagens WIM a partir de um fluxo multicast existente, mas irá reverter para uma cópia de ficheiros padrão se não existir uma transmissão em fluxo multicast.  

> [!NOTE]
>  Este processo apenas se aplica a ficheiros de imagem WIM.  

 Os pré-requisitos do servidor de implementação para se preparar para MDT multicasting são:  

-   O servidor de implementação deve executar o Windows Server 2008 ou posterior  

-   A função Serviços de implementação do Windows tem de estar instalada na consola de gestão de servidor  

-   Deve ser instalado o Windows AIK 1.1 para o Windows Server 2008  

-   MDT tem de ser instalado  

-   Como com qualquer implementação com o MDT, imagem WIM, pelo menos, um sistema operativo tem de ter sido importado, como um conjunto completo de ficheiros de origem ou como uma imagem personalizada com ficheiros de configuração  

> [!NOTE]
>  É importante utilizar a versão mais recente do Windows AIK para multicasting; a cópia do Windows PE incluída nas versões anteriores do Windows AIK — por exemplo, o Windows AIK 1.0 — não suporta a transferir a partir de um servidor multicast.  

 **Para configurar o MDT para multicasting de uma partilha de implementação existente**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share* (onde *deployment_share* é o nome da partilha de implementação para configurar).  

3.  No painel ações, clique em **propriedades**.  

4.  No **geral** separador, selecione o **multicast ativar para esta partilha de implementação (requer os serviços de implementação do Windows do Windows Server 2008)** caixa de verificação.  

5.  Clique em **OK**.  

6.  No painel ações, clique em **partilha de implementação de atualização**.  

     Inicia o Assistente de partilha de implementação da atualização.  

7.  No **opções** página, selecione as opções pretendidas para atualizar a partilha de implementação e, em seguida, clique em **seguinte**.  

8.  No **resumo** página, verifique os detalhes estão corretos e, em seguida, clique em **seguinte**.  

9. No **confirmação** página, clique em **concluir**.  

 A partilha de implementação está agora configurada para transmissão multicast de serviços de implementação do Windows.  

 Este processo cria um transmissão multicast de serviços de implementação do Windows de conversão automática que diretamente utiliza a partilha de implementação MDT existente. MDT não cria as transmissões de conversão de agendada. Tenha também em atenção que não existem imagens adicionais são importadas para serviços de implementação do Windows e que não é possível utilizar multicast para imagens de arranque, porque o cliente multicast não pode ser carregado até depois de executar o Windows PE.  

 **Para verificar que foi gerada à transmissão multicast nos serviços de implementação do Windows**  

1.  Clique em **iniciar**, aponte para **ferramentas administrativas**e, em seguida, clique em **dos serviços de implementação do Windows**.  

2.  Na árvore da consola de serviços de implementação do Windows, clique com botão direito **servidores**e, em seguida, clique em **Adicionar servidor**.  

3.  No **adicionar servidores (s)** caixa de diálogo, clique em **computador Local**e, em seguida, clique em **OK**.  

4.  Na árvore da consola de serviços de implementação do Windows, clique em **servidores**, em seguida, clique em ***server_name*** (onde *server_name* é o nome do computador com a implementação do Windows Serviços). Clique em **as transmissões de Multicast**.  

5.  No painel de detalhes, um novo transmissão de conversão automática para a partilha de implementação será apresentado — por exemplo, **implementação BDD partilhar $**.  

6.  Certifique-se de que o estado do **BDD partilha implementação$** transmissão de conversão automática está definido como **Active Directory**.  

 Após ter sido implementado num computador, certifique-se de que o sistema operativo foi transferido de um transmissão multicast, examinando o ficheiro de BDD.log na pasta \Windows\Temp\DeploymentLogs.  

 Haverá duas entradas na pasta de registos, ambos os início com **transferência Multicast**; verifique-los para verificar se a transferência foi concluída com êxito. Para obter mais informações sobre as transmissões de multicast com o MDT e serviços de implementação do Windows, consulte a secção "Ativar Windows implementação dos serviços de implementação para LTI implementações Multicast", no documento MDT *utilizando o Microsoft Deployment Toolkit*.  

## <a name="performing-staged-deployments-using-mdt-oem-preload"></a>Efetuar testado implementações com o MDT (OEM pré-carregamento)  
 Em muitas organizações, os computadores estão carregados com a imagem do sistema operativo antes da implementação para a rede de produção. Em alguns casos, a carregar a imagem do sistema operativo é efetuada por um agrupamento dentro da organização responsável pela criação dos computadores num ambiente de teste. Noutros casos, ao carregar a imagem do sistema operativo é efetuado pelo fornecedor de hardware do computador, também conhecido como um *fabricante de equipamento original* (OEM).  

> [!NOTE]
>  O processo de pré-carregamento OEM é suportado no MDT apenas para implementações efetuada utilizando LTI. Para o Configuration Manager, utilize a funcionalidade de suporte de dados pré-configurado.  

### <a name="overview-of-the-oem-preload-process-in-mdt"></a>Descrição geral do processo de pré-carregamento OEM no MDT  
 O processo de pré-carregamento OEM está dividido em três fases:  

-   **Fase 1**. Crie uma imagem com base no suporte de dados do computador de referência para ser aplicada no ambiente de teste.  

-   **Fase 2**. Aplica a imagem do computador de referência para o computador de destino num ambiente de teste.  

-   **Fase 3**. Concluir a implementação do computador de destino no ambiente de produção.  

 Fase 1 e a fase 3 normalmente são executadas pela organização de implementação. Consoante a utilização do processo de pré-carregamento OEM na organização, a fase 2 pode ser efetuada pela organização ou o fornecedor de hardware do computador que fornece os computadores. Se a organização efetua a fase 2, o ambiente de teste é na sua organização. Se um OEM efetua a fase 2, o ambiente de teste é no ambiente do OEM.  

#### <a name="overview-of-mdt-configuration-files-in-the-oem-preload-process"></a>Descrição geral dos ficheiros de configuração do MDT no processo de pré-carregamento OEM  
 Separado MDT os ficheiros de configuração (CustomSettings.ini e Bootstrap.ini) são utilizados pelas sequências de tarefas são executadas durante a fase 1 e 3 fase do processo de pré-carregamento OEM. No entanto, ambos os ficheiros de configuração existem em simultâneo em estruturas de pasta diferente.  

 Na primeira fase, os ficheiros de configuração são utilizados durante a criação do computador de referência em são armazenados na pasta específica para a sequência de tarefas utilizada nessa fase. Os ficheiros de configuração utilizados na fase de terceiro e o apelido do processo de pré-carregamento OEM são armazenados na pasta que é específica para a sequência de tarefas utilizada nessa fase.  

 Quando efetuar alterações para os ficheiros de configuração, certifique-se de que são efetuadas alterações ao ficheiro de configuração que corresponda à sequência de tarefas adequadas em cada fase do processo de pré-carregamento OEM.  

#### <a name="overview-of-mdt-log-files-in-the-oem-preload-process"></a>Descrição geral dos ficheiros de registo do MDT no processo de pré-carregamento OEM  
 Ficheiros de registo separados MDT são gerados durante a fase 1 e 3 fase do processo de pré-carregamento OEM:  

-   Os ficheiros de registo do MDT para a fase 1 são armazenados nas pastas C:\MININT e C:\SMSTSLog.  

-   Os ficheiros de registo do MDT para a fase 3 são armazenados na pasta %WINDIR%\System32\CCM\Logs para implementações baseadas em x86 ou na pasta %WINDIR%\SysWow64\CCM\Logs para implementações baseadas em x64.  

 Utilize a pasta adequada quando diagnosticar ou a resolução de problemas de implementação relacionados com o MDT.  

### <a name="staged-deployments-using-lti"></a>Implementações de teste com LTI  
 Para implementações LTI, execute o através da pré-carregamento processo OEM um *suporte de dados amovível (suporte de dados)* tipo de partilha de implementação. Outros tipos de partilha de implementação não são suportados para o processo de pré-carregamento OEM.  

 Para executar o processo de pré-carregamento OEM, crie uma sequência de tarefas com base no modelo de sequência de tarefas de sequência de tarefas do OEM Litetouch, além de quaisquer sequências de tarefas que será utilizado para implementar o sistema operativo de destino. Em seguida, crie um *suporte de dados amovível (suporte de dados)* partilha de implementação que, fundamentalmente, irá criar um ficheiro ISO da implementação da partilha de conteúdo, especificamente os ficheiros LiteTouchPE_x86.iso ou os ficheiros LiteTouchPE_x64.iso (baseado em ficheiros no destino plataforma de processador de computador). O processo de atualização de partilha de implementação também cria uma estrutura de pasta que pode ser utilizada para criar suportes de dados do formato de disco Universal.  

#### <a name="lti-oem-preload-processphase-1-create-a-media-based-image"></a>Processo de pré-carregamento LTI OEM — fase 1: Criar uma imagem com base no suporte de dados  
 A organização de implementação executa a primeira fase do processo de pré-carregamento OEM. Final deliverable nesta fase é uma imagem de arranque (por exemplo, um ficheiro ISO) ou suportes de dados (tais como um DVD) que é enviado para o OEM ou para o ambiente de teste dentro da organização de implementação. A maioria destes passos é efetuada no Deployment Workbench.  

 **Para criar uma imagem com base no suporte de dados para a entrega de OEM ou o ambiente de teste dentro da organização de implementação**  

1.  Preencher os seguintes nós para a partilha de implementação no Deployment Workbench:  

    -   Sistemas Operativos  

    -   Aplicações  

    -   Pacotes  

    -   Controladores de Out-of-Box  

     Para obter mais informações sobre como efetuar este passo, consulte a secção "Gerir implementação partilhas no Deployment Workbench", no documento MDT *utilizar o Microsoft Deployment Toolkit*.  

2.  Crie uma nova sequência de tarefas com base no modelo de sequência de tarefas de sequência de tarefas Litetouch OEM no Deployment Workbench.  

     Para obter mais informações sobre como efetuar este passo, consulte a secção "Configurar tarefas sequências no Deployment Workbench", no documento MDT *utilizar o Microsoft Deployment Toolkit*.  

3.  Crie um ou mais sequências de tarefas que serão utilizadas para implementar o sistema de operativo de destino no computador de destino após a implementação no ambiente de produção.  

     Para obter mais informações sobre como efetuar este passo, consulte a secção "Configurar tarefas sequências no Deployment Workbench", no documento MDT *utilizar o Microsoft Deployment Toolkit*.  

4.  Crie um perfil de seleção que inclui as aplicações, sistemas operativos, controladores, pacotes e sequências de tarefas necessárias para a implementação do OEM.  

     Para obter mais informações sobre como efetuar este passo, consulte a secção "Gerir seleção perfis", no documento MDT *utilizar o Microsoft Deployment Toolkit*.  

5.  Crie suportes de dados de implementação.  

     Para obter mais informações sobre a execução deste passo, consulte a secção "Gerir LTI implementação suporte de dados" no documento MDT *utilizar o Microsoft Deployment Toolkit*.  

6.  Atualize o suporte de dados de implementação criado no Deployment Workbench no passo anterior.  

     Quando atualizar o suporte de dados de implementação, o Deployment Workbench cria o ficheiro LiteTouchMedia.iso. Para obter mais informações sobre como efetuar este passo, consulte a secção "Gerir LTI implementação suporte de dados" no documento MDT *utilizar o Microsoft Deployment Toolkit*.  

7.  Grave um DVD do ficheiro LiteTouchMedia.iso criado no passo anterior.  

    > [!NOTE]
    >  Se fornecer o ficheiro ISO, OEM ou ambiente de teste da organização, este passo não é necessário.  

8.  Entrega o ficheiro ISO ou a unidade de DVD ao OEM ou para o ambiente de teste da organização.  

#### <a name="lti-oem-preload-processphase-2-apply-the-image-to-the-target-computer"></a>Processo de pré-carregamento LTI OEM — fase 2: Aplicar a imagem ao computador de destino  
 A segunda fase do processo de pré-carregamento OEM é executada pelo OEM ou pela equipa de implementação no ambiente de teste da organização de implementação. Durante esta fase do processo, o ficheiro. ISO ou DVD que criou na fase 1 é aplicada aos computadores de destino. Deliverable nesta fase é a imagem implementada nos computadores de destino para que estas estão prontas para implementação no ambiente de produção.  

 **Para aplicar a imagem aos computadores de destino**  

1.  Inicie um computador de destino com o suporte de dados criada na fase 1.  

     Windows PE inicia e, em seguida, inicia o Assistente de implementação do Windows.  

2.  No Assistente de implementação do Windows, clique em de **sequência de tarefas de pré-instalação do OEM para o ambiente de teste** sequência de tarefas.  

     A sequência de tarefas será iniciado e o conteúdo de suportes de dados será copiado para o disco rígido local do computador de destino.  

3.  Quando o Assistente de implementação do Windows está concluído para o **sequência de tarefas de pré-instalação do OEM para o ambiente de teste** sequência de tarefas, o disco rígido estará pronto para iniciar o resto do processo de implementação através da execução do Windows Assistente de implementação para as sequências de tarefas que são utilizados para implementar o sistema operativo.  

     O **sequência de tarefas de pré-instalação do OEM para o ambiente de teste** sequência de tarefas é responsável por implementar a imagem ao computador de destino e iniciar o processo de LTI. O Assistente de implementação do Windows será iniciado uma segunda vez para executar as sequências de tarefas utilizadas para implementar o sistema operativo no computador de destino.  

4.  Clone o conteúdo do disco rígido primeiro a tantos computadores de destino no ambiente de teste conforme necessário.  

5.  Os computadores de destino são entregues para o ambiente de produção para implementação.  

#### <a name="lti-oem-preload-processphase-3-complete-target-computer-deployment"></a>Processo de pré-carregamento LTI OEM — fase 3: Concluir a implementação de computador de destino  
 A fase de terceira e final do processo de pré-carregamento OEM é executada num ambiente de produção da organização de implementação. Durante esta fase do processo, o computador de destino é iniciado e começa a imagem de suportes de dados, colocada no disco rígido no ambiente de teste durante a fase de anterior.  

 **Para concluir a implementação dos computadores de destino no ambiente de produção**  

1.  Inicie o computador de destino.  

     Windows PE inicia e, em seguida, inicia o Assistente de implementação do Windows.  

2.  Conclua o Assistente de implementação do Windows utilizando as informações de configuração específicos para cada computador de destino.  

     Para obter mais informações sobre como concluir este passo, consulte a secção "A executar o Assistente de implementação", no documento MDT *utilizar o Microsoft Deployment Toolkit*.  

 Quando esta fase estiver concluída, o computador de destino estará pronto a utilizar no ambiente de produção.  

## <a name="using-windows-powershell-to-perform-common-tasks"></a>Com o Windows PowerShell para executar tarefas comuns  
 As tarefas de administração do MDT no Deployment Workbench são efetuadas por cmdlets do Windows PowerShell subjacentes, o que pode utilizar para automatizar tarefas administrativas comuns, tais como aqueles nas secções seguintes.  

 Pode automatizar a administração do MDT, efetuando os seguintes passos:  

-   Criar uma nova partilha de implementação, conforme descrito em [criar uma nova partilha de implementação](#CreateNewDeployShare).  

-   Crie uma pasta numa partilha de implementação, conforme descrito em [criando uma pasta](#CreateFolder).  

-   Eliminar uma pasta de uma partilha de implementação, conforme descrito em [eliminar uma pasta](#DeleteFolder).  

-   Importar um controlador de dispositivo para uma partilha de implementação, conforme descrito em [importar um controlador de dispositivo](#ImportDeviceDriver).  

-   Eliminar um controlador de dispositivo de uma partilha de implementação, conforme descrito em [eliminar um controlador de dispositivo](#DeleteDeviceDriver).  

-   Importar um pacote do sistema operativo para uma partilha de implementação, conforme descrito em [importar um pacote do sistema operativo](#ImportOpSysPackage).  

-   Eliminar um pacote do sistema operativo de uma partilha de implementação, conforme descrito em [eliminar um pacote do sistema operativo](#DeleteOpSysPackage).  

-   Importar um sistema operativo para uma partilha de implementação, conforme descrito em [importação de um sistema operativo](#ImportOpSys).  

-   Eliminar um sistema operativo de uma partilha de implementação, conforme descrito em [eliminar um sistema operativo](#DeleteOpSys).  

-   Criar uma aplicação numa partilha de implementação, conforme descrito em [criar uma aplicação](#CreateApplication).  

-   Eliminar uma aplicação a partir de uma partilha de implementação, conforme descrito em [eliminar uma aplicação](#DeleteApplication).  

-   Criar uma sequência de tarefas numa partilha de implementação, conforme descrito em [criar uma sequência de tarefas](#CreateTaskSequence).  

-   Eliminar uma sequência de tarefas a partir de uma partilha de implementação, conforme descrito em [eliminar uma sequência de tarefas](#DeleteTaskSequence).  

-   Criar uma base de dados do MDT, conforme descrito em [criar uma base de dados do MDT](#CreateMDTDB).  

-   Criar um perfil de seleção, conforme descrito em [criar um perfil de seleção](#CreateSelectProfile).  

-   Uma partilha de implementação de atualização, conforme descrito em [uma partilha de implementação de atualização](#UpdatingDeployShare).  

-   Crie uma partilha de implementação ligado, conforme descrito em [criar uma partilha de implementação ligado](#CreateLinkedDeployShare).  

-   Atualizar uma partilha de implementação ligado, conforme descrito em [atualizar uma partilha de implementação ligado](#UpdatingLinkedDeployShare).  

-   Eliminar uma partilha de implementação ligado, conforme descrito em [eliminar uma partilha de implementação ligado](#DeleteLinkedDeployShare).  

-   Criar suportes de dados de implementação, conforme descrito em [criar suportes de dados](#CreateMedia).  

-   Gerar suporte de dados de implementação, conforme descrito em [gerar o suporte de dados](#GenerateMedia).  

-   Eliminar suporte de dados de implementação, conforme descrito em [suporte de dados eliminar](#DeleteMedia).  

###  <a name="CreateNewDeployShare"></a> Criar uma nova partilha de implementação  
 Os seguintes comandos do Windows PowerShell criam uma nova partilha de implementação na partilha de implementação de D:\Production denominado *produção$*. A nova partilha de implementação será apresentada no Deployment Workbench como produção.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "D:\Production Deployment Share" -Description "Production" -NetworkPath "\\Deployment_Server\Production$" -Verbose | add-MDTPersistentDrive -Verbose  
    ```  

###  <a name="CreateFolder"></a> Criar uma pasta  
 Os seguintes comandos do Windows PowerShell criam uma pasta de Adobe na árvore da consola do Deployment Workbench no Deployment Workbench\/partilhas de implementação\/produção\/aplicações.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Applications" -enable "True" -Name "Adobe" -Comments "This folder contains Adobe software" -ItemType "folder" -Verbose remove-psdrive DS001 -Verbose  
    ```  

    > [!NOTE]
    >  Adicionar "`remove-psdrive`" para o script assegura que o processo em segundo plano é concluída antes de continuar.  

###  <a name="DeleteFolder"></a> Eliminar uma pasta  
 Os seguintes comandos do Windows PowerShell eliminar Deployment Workbench\/partilhas de implementação\/produção\/aplicações\/pasta Adobe.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Remove-item -path "DS002:\Applications\Adobe" -Verbose  
    ```  

> [!NOTE]
>  O script irá falhar se a pasta não está vazia.  

###  <a name="ImportDeviceDriver"></a> Importar um controlador de dispositivo  
 Os seguintes comandos do Windows PowerShell irão importar o controlador de dispositivo do monitor Dell 2407 WFP para a partilha de implementação de produção.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtdriver -path "DS002:\Out-of-Box Drivers\Monitor" -SourcePath "D:\Drivers\Dell\2407 WFP" -Verbose  
    ```  

###  <a name="DeleteDeviceDriver"></a> Eliminar um controlador de dispositivo  
 O seguinte comando do Windows PowerShell elimina o controlador de monitor Dell 2407 WFP da partilha de implementação de produção.  

```  
Remove-item -path "DS002:\Out-of-Box Drivers\Dell Inc. Monitor 2407WFP.INF 1.0" -Verbose  
```  

###  <a name="ImportOpSysPackage"></a> Importar um pacote do sistema operativo  
 Os seguintes comandos do Windows PowerShell importar todos os pacotes de sistema operativo localizados d:\\atualizações\\Microsoft\\Vista. Estes pacotes de sistema operativo serão armazenados numa partilha de implementação de produção, que está a ser d:\\partilha de implementação de produção.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtpackage -path "DS002:\Packages" -SourcePath "D:\Updates\Microsoft\Vista" -Verbose  
    ```  

###  <a name="DeleteOpSysPackage"></a> Eliminar um pacote do sistema operativo  
 O seguinte comando do Windows PowerShell elimina o pacote do sistema operativo especificado da partilha de implementação de produção.  

```  
Remove-item -path "DS002:\Packages\Package_1_for_KB940105 neutral x86 6.0.1.0 KB940105" -Verbose  
```  

###  <a name="ImportOpSys"></a> Importação de um sistema operativo  
 Os seguintes comandos do Windows PowerShell importar sistema operativo Windows Vista localizado na d:\\sistemas operativos\\Windows Vista x86. O sistema operativo será armazenado numa partilha de implementação de produção, que está a ser d:\\partilha de implementação de produção.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtoperatingsystem -path "DS002:\Operating Systems" -SourcePath "D:\Operating Systems\Windows Vista x86" -DestinationFolder "Windows Vista x86" -Verbose  
    ```  

###  <a name="DeleteOpSys"></a> Eliminar um sistema operativo  
 O seguinte comando do Windows PowerShell elimina o sistema operativo do Windows Vista HOMEBASIC da partilha de implementação de produção.  

```  
Remove-item -path "DS002:\Operating Systems\Windows Vista HOMEBASIC in Windows Vista x86 install.wim" -Verbose  
```  

###  <a name="CreateApplication"></a> Criar uma aplicação  
 Os seguintes comandos do Windows PowerShell criam a aplicação Adobe leitor 9 utilizando ficheiros de origem d:\\Software\\Adobe\\leitor 9. A aplicação será armazenada numa partilha de implementação de produção, que está a ser d:\\partilha de implementação de produção.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-MDTApplication -path "DS002:\Applications" -enable "True" -Name "Adobe Reader 9" -ShortName "Reader" -Version "9" -Publisher "Adobe" -Language "" -CommandLine "setup.exe" -WorkingDirectory ".\Applications\Adobe Reader 9" -ApplicationSourcePath "D:\Software\Adobe\Reader 9" -DestinationFolder "Adobe Reader 9" -Source ".\Applications\Adobe Reader 9" -Verbose  
    ```  

###  <a name="DeleteApplication"></a> Eliminar uma aplicação  
 O seguinte comando do Windows PowerShell elimina a aplicação Adobe leitor 9 da partilha de implementação de produção.  

```  
Remove-item -path "DS002:\Applications\Adobe Reader 9" -Verbose  
```  

###  <a name="CreateTaskSequence"></a> Criar uma sequência de tarefas  
 Os comandos do Windows PowerShell seguintes criam a **compilação do Windows Vista produção** sequência na partilha de implementação de produção, que está localizada em d: de tarefas\\partilha de implementação de produção.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdttasksequence -path "DS002:\Task Sequences" -Name "Windows Vista Business Production Build" -Template "Client.xml" -Comments "Approved for use in the production environment.  This task sequence uses the Standard Client task sequence template" -ID "Vista_Ref" -Version "1.0" -OperatingSystemPath "DS002:\Operating Systems\Windows Vista BUSINESS in Windows Vista x86 install.wim" -FullName "Fabrikam User" -OrgName "Fabrikam" -HomePage "http://www.Fabrikam.com" -AdminPassword "secure_password" -Verbose  
    ```  

###  <a name="DeleteTaskSequence"></a> Eliminar uma sequência de tarefas  
 O seguinte comando do Windows PowerShell elimina o **compilação do Windows Vista produção** sequência da partilha de implementação de produção de tarefas.  

```  
Remove-item -path "DS002:\Task Sequences\Windows Vista Business Production Build" -force -Verbose  
```  

###  <a name="CreateMDTDB"></a> Criar uma base de dados do MDT  
 Os seguintes comandos do Windows PowerShell criam uma nova base de dados do MDT no *implementação\_servidor* servidor para a partilha de implementação de produção. A ligação de base de dados será através de TCP\/IP.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-MDTDatabase -path "DS002:" -SQLServer "DeploymentServer" -Netlib "DBMSSOCN" -Database "MDT2010" -SQLShare "DB_Connect" -Force -Verbose  
    ```  

###  <a name="CreateSelectProfile"></a> Criar um perfil de seleção  
 Os seguintes comandos do Windows PowerShell criam um novo perfil de seleção de aplicações.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Selection Profiles" -enable "True" -Name "Applications" -Comments "" -Definition "<SelectionProfile><Include path="Applications" /></SelectionProfile>" -ReadOnly "False" -Verbose  
    ```  

###  <a name="UpdatingDeployShare"></a> Atualizar uma partilha de implementação  
 Os seguintes comandos do Windows PowerShell atualizar partilha de implementação de produção, que está a ser d:\\partilha de implementação de produção.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  
    
-   ```
    Update\-MDTDeploymentShare \-path "DS002:" \-Verbose  
    ```
    
###  <a name="CreateLinkedDeployShare"></a> Criar uma partilha de implementação ligado  
 Os comandos do Windows PowerShell seguintes criam uma partilha de implementação que está ligada à partilha de implementação de produção e reside no \\ \\ *remoto\_servidor\_nome* \\Partilha de implementação do $. Tudo o perfil de seleção é utilizado para determinar o conteúdo é replicado para a partilha de implementação ligado. Conteúdo da partilha de implementação de produção irá ser intercalado com conteúdo que já exista no \\ \\ *remoto\_servidor\_nome*\\partilha de implementação do $.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Linked Deployment Shares" -enable "True" -Name "LINKED001" -Comments "" -Root "\\RemoteServerName\Deployment$" -SelectionProfile "Everything" -Replace "False" -Verbose  
    ```  

###  <a name="UpdatingLinkedDeployShare"></a> Atualizar uma partilha de implementação ligado  
 Os seguintes comandos do Windows PowerShell, atualize a partilha de implementação LINKED001.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Replicate-MDTContent -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="DeleteLinkedDeployShare"></a> Eliminar uma partilha de implementação ligado  
 Os seguintes comandos do Windows PowerShell eliminar a partilha de implementação LINKED001.  

-   Adicionar\-PSSnapIn Microsoft.BDD.PSSnapIn  

-   ```  
    Remove-item -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="CreateMedia"></a> Criar suporte de dados  
 Os comandos do Windows PowerShell seguintes criam uma pasta de origem que contém conteúdo utilizado para criar suportes de dados. A partilha de implementação de produção será utilizada como origem. Tudo o perfil de seleção determina o conteúdo é colocado na pasta de conteúdo de multimédia. Será criado o ficheiro de LiteTouchMedia.iso quando é gerado o suporte de dados. O suporte de dados irá suportar plataformas x86 e x64.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Media" -enable "True" -Name "MEDIA001" -Comments "some comment here" -Root "D:\Media" -SelectionProfile "Everything" -SupportX86 "True" -SupportX64 "True" -GenerateISO "True" -ISOName "LiteTouchMedia.iso" -Verbose  
    ```  

-   ```  
    New-PSDrive -Name "MEDIA001" -PSProvider "MDTProvider" -Root "D:\Media\Content" -Description "Embedded media deployment share" -Force -Verbose  
    ```  

###  <a name="GenerateMedia"></a> Gerar o suporte de dados  
 Os seguintes comandos do Windows PowerShell criam o ficheiro de LiteTouchMedia.iso em d:\\suportes de dados, o que irão utilizar o conteúdo da pasta de origem de suporte de dados MEDIA001.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Generate-MDTMedia -path "DS002:\Media\MEDIA001" -Verbose  
    ```  

###  <a name="DeleteMedia"></a> A eliminar o suporte de dados  
 O seguinte comando do Windows PowerShell elimina o suporte de dados MEDIA001 da partilha de implementação de produção.  

```  
Remove-item -path "DS002:\Media\MEDIA001" -Verbos  
```  

## <a name="delaying-domain-join-to-avoid-application-of-group-policy-objects"></a>Atrasando a associação a um domínio para evitar a aplicação de objetos de política de grupo  
 Política de grupo é uma tecnologia de avançado e flexível que fornece a capacidade de gerir um grande número de objetos de computador e utilizador de serviços de domínio do Active Directory (AD DS) através de um modelo centralizado, um-para-muitos de forma eficiente. Definições de política de grupo estão contidas num objeto de política de grupo (GPO) e ligadas a um ou mais contentores do serviço de AD DS — sites, domínios e unidades organizacionais (UOs).  

 Algumas organizações têm definições de política de grupo que são restritiva e pode causar problemas durante implementações do sistema operativo. Por exemplo, as seguintes definições de política de grupo podem interromper um processo de início de sessão automática:  

-   Restrições de AutoLogon  

-   Mudar o nome conta de administrador  

-   Faixas legais e legendas  

-   Políticas de segurança restritivas (por exemplo, a especializada segurança – política de limitação de funcionalidades [SSLF])  

 É uma opção de ultrapassar os problemas que possam causar um GPO durante a implementação associar o computador ao domínio mais tarde possíveis no processo de implementação. Esta associação pode ser feita utilizando um passo de sequência de tarefas personalizada que executa o script de ZTIDomainJoin.wsf.  

 Para associar o computador de destino ao domínio, o script de ZTIDomainJoin.wsf utiliza o **DomainAdmin**, **DomainAdminDomain**, **DomainAdminPassword**,  **JoinDomain**, e **MachineObjectOU** propriedades. Podem declarar estas propriedades utilizando o Assistente de implementação do Windows, as regras de partilha de implementação, a BD do MDT e regras de computador e coleção do Configuration Manager. A conta utilizada tem de ter os direitos necessários para criar e eliminar objetos do computador no domínio.  

 Normalmente, o script de ZTIConfigure.wsf atualiza o ficheiro Unattend.xml ou Unattend.txt com os valores que especificar estas propriedades. Estas definições, em seguida, são analisadas pelo programa de configuração do Windows e o sistema tenta aderir ao domínio no início do processo de implementação. Se o fizer, subjects o computador de destino para as definições especificadas na GPOs do domínio e, possivelmente, pode provocar a falha no processo de implementação.  

 Atrasar intencionalmente a associação do computador de destino ao domínio durante o processo de implementação, pode remover determinados elementos do ficheiro Unattend.xml. O script de ZTIConfigure.wsf irá ignorar escrever propriedades no ficheiro Unattend.xml se o elemento de propriedade associados está em falta no ficheiro de.  

> [!NOTE]
>  Este exemplo trabalho-em torno só é válido quando implementar sistemas operativos Windows 7, Windows Server 2008 ou Windows Server 2008 R2.  

 **Prepare o ficheiro unattend.xml para que o computador de destino não tenta aderir ao domínio durante a configuração do Windows**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share*/Task sequências /*task_sequence* (onde *deployment_share*é o nome da partilha de implementação e *task_sequence* é o nome da sequência de tarefas seja configurado).  

3.  No painel ações, clique em **propriedades**.  

4.  No **informações do SO** separador, clique em **editar Unattend.xml**.  

     Inicia o Gestor de imagens de sistema do Windows (Windows SIM).  

5.  No **ficheiro de resposta** painel, aceda a **4 especialização/identificação/credenciais**. Clique com botão direito **credenciais**e, em seguida, clique em **eliminar**.  

6.  Clique em **Sim**.  

7.  Guarde o ficheiro de resposta e, em seguida, saia Windows SIM.  

8.  Clique em **OK** na sequência de tarefas **propriedades** caixa de diálogo.  

 Com o `Credentials` elementos em falta no ficheiro unattend.xml, o script de ZTIConfigure.wsf não é capaz de preencher as informações de associação de domínio no ficheiro Unattend.xml, o que irá impedir que o programa de configuração do Windows a tentar associar ao domínio.  

 **Para adicionar um passo de sequência de tarefas que associa o computador de destino ao domínio**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft Deployment Toolkit**e, em seguida, clique em **Deployment Workbench**.  

2.  Na árvore da consola Deployment Workbench, vá para partilhas de implementação. o Workbench/implementação /*deployment_share*/Task sequências /*task_sequence* (onde *deployment_share*é o nome da partilha de implementação e *task_sequence* é o nome da sequência de tarefas seja configurado).  

3.  No painel ações, clique em **propriedades**.  

4.  No **sequência de tarefas** separador, aceda a e expanda o nó de restauro de estado.  

5.  Certifique-se de que o **recuperar do domínio** passo de sequência de tarefas está presente. Se Sim, avance para o passo 9.  

6.  Na sequência de tarefas **propriedades** caixa de diálogo, clique em **adicionar**, aceda a **definições**e clique em **recuperar do domínio**.  

7.  Adicionar o **recuperar do domínio** passo de sequência de tarefas para o editor de sequência de tarefas. Certifique-se de que o passo consiste na localização pretendida na sequência de tarefas.  

8.  Certifique-se de que as definições para o **recuperar do domínio** passo de sequência de tarefas estão configurados para satisfazer as suas necessidades.  

9. Clique em **OK** na sequência de tarefas **propriedades** caixa de diálogo para guardar a sequência de tarefas.

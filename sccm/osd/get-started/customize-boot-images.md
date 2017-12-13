---
title: 'Personalizar imagens de arranque '
titleSuffix: Configuration Manager
description: "Saiba várias formas de utilizar a ferramenta de linha de comandos do Configuration Manager ou Deployment Image Servicing and Management (DISM) para personalizar uma imagem de arranque."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9cbfc406-d009-446d-8fee-4938de48c919
caps.latest.revision: "15"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 184768e87406051508c8dcacfa63db5ff85c3732
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/12/2017
---
# <a name="customize-boot-images-with-system-center-configuration-manager"></a>Personalizar imagens de arranque com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Cada versão do Configuration Manager suporta uma versão específica do Windows Assessment and Deployment Kit (Windows ADK). Pode atualizar ou personalizar, imagens de arranque a partir da consola do Configuration Manager quando são baseadas numa versão do Windows PE da versão suportada do Windows ADK. Outras imagens de arranque devem ser personalizadas através de outro método, como a ferramenta de linha de comandos Gestão e Atualização de Imagens de Implementação (DISM) que faz parte do Windows AIK e do Windows ADK.  

 O seguinte fornece a versão suportada do Windows ADK, a versão do Windows PE nas quais se baseia a imagem de arranque que pode ser personalizada a partir da consola do Configuration Manager e as versões do Windows PE na qual se baseia a imagem de arranque que pode personalizar com o DISM e depois adicione a imagem para o Configuration Manager.  

-   **Versão do Windows ADK**  

     Windows ADK para Windows 10  

-   **Versões do Windows PE para imagens de arranque personalizáveis a partir da consola do Configuration Manager**  

     Windows PE 10  

-   **Versões do Windows PE para imagens de arranque não podem ser personalizadas na consola do Configuration Manager**  

     Windows PE 3.1<sup>1</sup> e Windows PE 5  

     <sup>1</sup> só é possível adicionar uma imagem de arranque para o Configuration Manager quando se baseia no Windows PE 3.1. Instale o Suplemento do Windows AIK para o Windows 7 SP1 para atualizar o Windows AIK para o Windows 7 (baseado no Windows PE 3) com o Suplemento do Windows AIK para Windows 7 SP1 (baseado no Windows PE 3.1). Poderá transferir o Suplemento do Windows AIK para Windows 7 SP1 a partir do [Centro de Transferências da Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

     Por exemplo, quando tiver do Configuration Manager, pode personalizar imagens de arranque do Windows ADK para Windows 10 (baseado no Windows PE 10) na consola do Configuration Manager. No entanto, embora as imagens de arranque baseadas no Windows PE 5 sejam suportadas, tem de personalizá-las a partir de um computador diferente e utilizar a versão do DISM que é instalada com o Windows ADK para Windows 8. Em seguida, pode adicionar a imagem de arranque à consola do Configuration Manager.  

 Os procedimentos deste tópico demonstram como adicionar os componentes opcionais exigidos pelo Configuration Manager para a imagem de arranque, utilizando os seguintes pacotes do Windows PE:  

-   **WinPE-WMI**: Adiciona suporte de Windows Management Instrumentation (WMI).  

-   **WinPE-Scripting**: Adiciona suporte de Script anfitrião para WSH (Windows).  

-   **WinPE-WDS-Tools**: Instala ferramentas dos serviços de implementação do Windows.  

 Existem outros pacotes do Windows PE disponíveis que pode adicionar. Os recursos seguintes fornecem mais informações sobre os componentes opcionais que pode adicionar à imagem de arranque.  

-   Para o Windows PE 5, consulte [WinPE: Adicionar pacotes (referência de componentes opcionais)](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx)  

-   Para o Windows PE 3.1, veja o tópico [Adicionar um Pacote a uma Imagem do Windows PE](http://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) na Biblioteca de Documentação do TechNet relativa ao Windows 7.  

> [!NOTE]
>Quando executar o arranque do WinPE a partir de uma imagem de arranque personalizado que inclua ferramentas que adicionou, pode abrir uma linha de comandos a partir do WinPE e escrever o nome do ficheiro da ferramenta para executá-lo. A localização destas ferramentas são automaticamente adicionados à variável de caminho. Só é possível adicionar a linha de comandos se o **ativar suporte de comando (apenas teste)** definição está selecionada no **personalização** separador nas propriedades da imagem de arranque.

## <a name="customize-a-boot-image-that-uses-windows-pe-5"></a>Personalizar uma imagem de arranque que utiliza o Windows PE 5  
 Para personalizar uma imagem de arranque que utiliza o Windows PE 5, é necessário instalar o Windows ADK e utilizar a ferramenta de linha de comandos DISM para montar a imagem de arranque, adicionar componentes e controladores adicionais e consolidar as alterações da imagem de arranque. Utilize o procedimento seguinte para personalizar a imagem de arranque.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-5"></a>Para personalizar uma imagem de arranque que utiliza o Windows PE 5  

1.  Instalar o Windows ADK num computador que não tenha outra versão do Windows AIK ou Windows ADK, e não tem quaisquer componentes do Configuration Manager instalado.  

2.  Transfira o Windows ADK para Windows 8.1 a partir do [Centro de Transferências da Microsoft](http://www.microsoft.com/download/details.aspx?id=39982).  

3.  Copie a imagem de arranque (wimpe.wim) da pasta de instalação Windows ADK (por exemplo, <*caminho de instalação*> \Windows Kits\\<*versão*> \Assessment e implementação Kit\Windows Preinstallation ambiente\\<*x86 ou amd64*>\\<*região*>) para uma pasta de destino no computador a partir do qual irá personalizar a imagem de arranque. Este procedimento utiliza C:\WinPEWAIK como o nome da pasta de destino.  

4.  Utilize o DISM para montar a imagem de arranque numa pasta local do Windows PE. Por exemplo, escreva a seguinte linha de comandos:  

     **DISM.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

     Em que C:\WinPEWAIK é a pasta que contém a imagem de arranque e C:\WinPEMount é a pasta montada.  

    > [!NOTE]
    >  Para obter mais informações sobre o DISM, veja o tópico [Referência Técnica de Deployment Image Servicing and Management (DISM)](http://technet.microsoft.com/library/hh824821.aspx) na Biblioteca de Documentação do TechNet relativa ao Windows 8.1 e ao Windows 8.

5.  Depois de montar a imagem de arranque, utilize o DISM para adicionar componentes opcionais à imagem de arranque. No Windows PE 5, os componentes opcionais de 64 bits estão localizados em <*Caminho de instalação*>\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs.  

    > [!NOTE]
    >  Este procedimento utiliza a seguinte localização para os componentes opcionais: C:\Programas\Microsoft ficheiros (x86) kits\8.1\assessment and Deployment Kit\Windows perguntas de environment\amd64\winpe_ocs. pré-instalação. O caminho utilizado pode ser diferente, dependendo da versão e das opções de instalação que escolher para o Windows ADK.  

     Escreva o seguinte para instalar os componentes opcionais:  

     **DISM.exe /image:C:\WinPEMount /add-package /packagepath: "C:\Program Files (x86) kits\8.1\assessment e implementação Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wmi.cab"**  

     **DISM.exe /image:C:\WinPEMount /add-package /packagepath: "C:\Program Files (x86) kits\8.1\assessment e implementação Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-scripting.cab"**  

     **DISM.exe /image:C:\WinPEMount /add-package /packagepath: "C:\Program Files (x86) kits\8.1\assessment e implementação Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wds-tools.cab"**  

     **DISM.exe /image:C:\WinPEMount /add-package /packagepath: "C:\Program Files (x86) kits\8.1\assessment e implementação Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-SecureStartup.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-SecureStartup_** *<locale\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-WMI_** *<locale\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-Scripting** *<locale\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-WDS-Tools_** *<locale\>* **.cab"**  

     Em que C:\WinPEMount é a pasta montada e região é a região dos componentes. Por exemplo, para a região **en-us**, teria de escrever:  

     **DISM.exe /image:C:\WinPEMount /add-package /packagepath: "C:\Program Files (x86) kits\8.1\assessment e implementação Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-SecureStartup_en-us.cab"**  

     **DISM.exe /image:C:\WinPEMount /add-package /packagepath: "C:\Program Files (x86) kits\8.1\assessment e implementação Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WMI_en-us.cab"**  

     **DISM.exe /image:C:\WinPEMount /add-package /packagepath: "C:\Program Files (x86) kits\8.1\assessment e implementação Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-Scripting_en-us.cab"**  

     **DISM.exe /image:C:\WinPEMount /add-package /packagepath: "C:\Program Files (x86) kits\8.1\assessment e implementação Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"**  

    > [!TIP]
    >  Para obter mais informações sobre os componentes opcionais que pode adicionar à imagem de arranque, veja o tópico [Referência dos Componentes Opcionais do Windows PE](http://technet.microsoft.com/library/hh824926.aspx) na Biblioteca de Documentação do TechNet relativa ao Windows 8.1 e ao Windows 8.  

6.  Utilize o DISM para adicionar controladores específicos à imagem de arranque, se for necessário. Escreva o seguinte para adicionar controladores à imagem de arranque:  

     **dism.exe /image:C:\WinPEMount /add-driver /driver:<** *caminho para o ficheiro .inf do controlador* **>**  

     Em que C:\WinPEMount é a pasta montada.  

7.  Escreva o seguinte para desmontar o ficheiro de imagem de arranque e confirmar as alterações.  

     **DISM.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

     Em que C:\WinPEMount é a pasta montada.  

8.  Adicione a imagem de arranque atualizada para o Configuration Manager para poder ser utilizada nas sequências de tarefas. Utilize os passos seguintes para importar a imagem de arranque atualizada:  

    1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

    2.  Na área de trabalho **Biblioteca de Software**, expanda **Sistemas Operativos** e clique em **Imagens de Arranque**.  

    3.  No separador **Home Page**, no grupo **Criar**, clique em **Adicionar Imagem de Arranque** para iniciar o Assistente Adicionar Imagem de Arranque.  

    4.  Na página **Origem de Dados**, especifique as seguintes opções e clique em **Seguinte**.  

        -   Na caixa **Caminho**, especifique o caminho para o ficheiro de imagem de arranque atualizado. O caminho especificado tem de ser um caminho de rede válido no formato UNC. Por exemplo:  **\\ \\ <**  *servername***>\\<***partilha WinPEWAIK***> \winpe.wim**.  

        -   Selecione a imagem de arranque na lista pendente **Imagem de Arranque**. Se o ficheiro WIM contiver várias imagens de arranque, será listada cada imagem.  

    5.  Na página **Geral**, especifique as seguintes opções e clique em **Seguinte**.  

        -   Na caixa **Nome**, especifique um nome exclusivo para a imagem de arranque.  

        -   Na caixa **Versão**, especifique um número de versão para a imagem de arranque.  

        -   Na caixa **Comentário**, insira uma breve descrição do modo como a imagem de arranque é utilizada.  

    6.  Conclua o assistente.  

9. Pode ativar uma shell de comandos na imagem de arranque para depuração e resolução de problemas da imagem de arranque no Windows PE. Utilize os passos seguintes para ativar a shell de comandos.  

    1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

    2.  Na área de trabalho **Biblioteca de Software**, expanda **Sistemas Operativos** e clique em **Imagens de Arranque**.  

    3.  Localize a nova imagem de arranque na lista e identifique o ID de pacote da imagem. O ID de pacote encontra-se na coluna **ID de imagem** da imagem de arranque.  

    4.  Numa linha de comandos, escreva **wbemtest** para abrir o Recurso de Teste do Windows Management Instrumentation.  

    5.  Tipo  **\\ \\ <**  *computador do fornecedor de SMS***> \root\sms\site_ <***sitecode*  **>**  no **espaço de nomes**e, em seguida, clique em **Connect**.  

    6.  Clique em **Abrir Instância**, escreva **sms_bootimagepackage.packageID="<packageID\>"** e, em seguida, clique em **OK**. Para packageID, introduza o valor que identificou no passo 3.  

    7.  Clique em **Atualizar Objeto** e, em seguida, clique em **EnableLabShell** no painel **Propriedades**.  

    8.  Clique em **Editar Propriedade**, altere o valor para **VERDADEIRO** e clique em **Guardar Propriedade**.  

    9. Clique em **Guardar Objeto** e, em seguida, saia do Recurso de Teste do Windows Management Instrumentation.  

10. É necessário distribuir a imagem de arranque para pontos de distribuição, grupos de pontos de distribuição ou coleções que estejam associadas a grupos de pontos de distribuição para poder utilizar a imagem de arranque numa sequência de tarefas. Utilize os passos seguintes para personalizar a imagem de arranque.  

    1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

    2.  Na área de trabalho **Biblioteca de Software**, expanda **Sistemas Operativos** e clique em **Imagens de Arranque**.  

    3.  Clique na imagem de arranque identificada no passo 3.  

    4.  No separador **Home Page**, no grupo **Implementação**, clique em **Atualizar Pontos de Distribuição**.  

## <a name="customize-a-boot-image-that-uses-windows-pe-31"></a>Personalizar uma imagem de arranque que utiliza o Windows PE 3.1  
 Para personalizar uma imagem de arranque que utiliza o WinPE 3.1, é necessário instalar o Windows AIK, instalar o suplemento do Windows AIK para Windows 7 SP1 e utilizar a ferramenta de linha de comandos DISM para montar a imagem de arranque, adicionar componentes e controladores adicionais e consolidar as alterações da imagem de arranque. Utilize o procedimento seguinte para personalizar a imagem de arranque.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-31"></a>Para personalizar uma imagem de arranque que utiliza o Windows PE 3.1  

1.  Instalar o Windows AIK num computador que não tenha outra versão do Windows AIK ou Windows ADK, e não tem quaisquer componentes do Configuration Manager instalado. Transfira o Windows AIK a partir do [Centro de Transferências da Microsoft](http://www.microsoft.com/download/details.aspx?id=5753).  

2.  Instale o Suplemento do Windows AIK para Windows 7 com SP1 no computador do passo 1. Transfira o Suplemento do Windows AIK para Windows 7 SP1 a partir do [Centro de Transferências da Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

3.  Copie a imagem de arranque (wimpe.wim) da pasta de instalação do Windows AIK (por exemplo, <*CaminhoDaInstalação*>\Windows AIK\Tools\PETools\amd64\\) para uma pasta no computador a partir do qual irá personalizar a imagem de arranque. Este procedimento utiliza C:\WinPEWAIK como o nome da pasta.  

4.  Utilize o DISM para montar a imagem de arranque numa pasta local do Windows PE. Por exemplo, escreva a seguinte linha de comandos:  

     **DISM.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

     Em que C:\WinPEWAIK é a pasta que contém a imagem de arranque e C:\WinPEMount é a pasta montada.  

    > [!NOTE]
    >  Para obter mais informações sobre o DISM, veja o tópico [Referência Técnica de Deployment Image Servicing and Management](http://technet.microsoft.com/library/dd744256\(v=ws.10\).aspx) na Biblioteca de Documentação do TechNet relativa ao Windows 7.  

5.  Depois de montar a imagem de arranque, utilize o DISM para adicionar componentes opcionais à imagem de arranque. No Windows PE 3.1, por exemplo, os componentes opcionais estão localizados em <*CaminhoDaInstalação*>\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\.  

    > [!NOTE]
    >  Este procedimento utiliza a seguinte localização para os componentes opcionais: C:\Programas\Microsoft Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs. O caminho utilizado pode ser diferente, dependendo da versão e das opções de instalação que escolher para o Windows AIK.  

     Escreva o seguinte para instalar os componentes opcionais:  

     **DISM.exe /image:C:\WinPEMount /add-package /packagepath: "C:\Programas\Microsoft Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wmi.cab"**  

     **DISM.exe /image:C:\WinPEMount /add-package /packagepath: "C:\Programas\Microsoft Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-scripting.cab"**  

     **DISM.exe /image:C:\WinPEMount /add-package /packagepath: "C:\Programas\Microsoft Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wds-tools.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-wmi_** *<locale\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-scripting_** *<locale\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-wds-tools_** *<locale\>* **.cab"**  

     Em que C:\WinPEMount é a pasta montada e região é a região dos componentes. Por exemplo, para a região **en-us**, teria de escrever:  

     **DISM.exe /image:C:\WinPEMount /add-package /packagepath: "C:\Programas\Microsoft Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wmi_en-us.cab"**  

     **DISM.exe /image:C:\WinPEMount /add-package /packagepath: "C:\Programas\Microsoft Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-scripting_en-us.cab"**  

     **DISM.exe /image:C:\WinPEMount /add-package /packagepath: "C:\Programas\Microsoft Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wds-tools_en-us.cab"**  

    > [!TIP]
    >  Para obter mais informações sobre os diferentes pacotes que pode adicionar à imagem de arranque, veja o tópico [Adicionar um Pacote a uma Imagem do Windows PE](http://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) na Biblioteca de Documentação do TechNet relativa ao Windows 7.  

6.  Utilize o DISM para adicionar controladores específicos à imagem de arranque, se for necessário. Escreva o seguinte para adicionar controladores à imagem de arranque, se for necessário:  

     **dism.exe /image:C:\WinPEMount /add-driver /driver:<** *caminho para o ficheiro .inf do controlador* **>**  

     Em que C:\WinPEMount é a pasta montada.  

7.  Escreva o seguinte para desmontar o ficheiro de imagem de arranque e confirmar as alterações.  

     **DISM.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

     Em que C:\WinPEMount é a pasta montada.  

8.  Adicione a imagem de arranque atualizada para o Configuration Manager para poder ser utilizada nas sequências de tarefas. Utilize os passos seguintes para importar a imagem de arranque atualizada:  

    1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

    2.  Na área de trabalho **Biblioteca de Software**, expanda **Sistemas Operativos** e clique em **Imagens de Arranque**.  

    3.  No separador **Home Page**, no grupo **Criar**, clique em **Adicionar Imagem de Arranque** para iniciar o Assistente Adicionar Imagem de Arranque.  

    4.  Na página **Origem de Dados**, especifique as seguintes opções e clique em **Seguinte**.  

        -   Na caixa **Caminho**, especifique o caminho para o ficheiro de imagem de arranque atualizado. O caminho especificado tem de ser um caminho de rede válido no formato UNC. Por exemplo:  **\\ \\ <**  *servername***>\\<***partilha WinPEWAIK***> \winpe.wim**.  

        -   Selecione a imagem de arranque na lista pendente **Imagem de Arranque**. Se o ficheiro WIM contiver várias imagens de arranque, será listada cada imagem.  

    5.  Na página **Geral**, especifique as seguintes opções e clique em **Seguinte**.  

        -   Na caixa **Nome**, especifique um nome exclusivo para a imagem de arranque.  

        -   Na caixa **Versão**, especifique um número de versão para a imagem de arranque.  

        -   Na caixa **Comentário**, insira uma breve descrição do modo como a imagem de arranque é utilizada.  

    6.  Conclua o assistente.  

9. Pode ativar uma shell de comandos na imagem de arranque para depuração e resolução de problemas da imagem de arranque no Windows PE. Utilize os passos seguintes para ativar a shell de comandos.  

    1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

    2.  Na área de trabalho **Biblioteca de Software**, expanda **Sistemas Operativos** e clique em **Imagens de Arranque**.  

    3.  Localize a nova imagem de arranque na lista e identifique o ID de pacote da imagem. O ID de pacote encontra-se na coluna **ID de imagem** da imagem de arranque.  

    4.  Numa linha de comandos, escreva **wbemtest** para abrir o Recurso de Teste do Windows Management Instrumentation.  

    5.  Tipo  **\\ \\ <**  *computador do fornecedor de SMS***> \root\sms\site_ <***sitecode*  **>**  no **espaço de nomes**e, em seguida, clique em **Connect**.  

    6.  Clique em **Abrir Instância**, escreva **sms_bootimagepackage.packageID="<packageID\>"** e, em seguida, clique em **OK**. Para packageID, introduza o valor que identificou no passo 3.  

    7.  Clique em **Atualizar Objeto** e, em seguida, clique em **EnableLabShell** no painel **Propriedades**.  

    8.  Clique em **Editar Propriedade**, altere o valor para **VERDADEIRO** e clique em **Guardar Propriedade**.  

    9. Clique em **Guardar Objeto** e, em seguida, saia do Recurso de Teste do Windows Management Instrumentation.  

10. É necessário distribuir a imagem de arranque para pontos de distribuição, grupos de pontos de distribuição ou coleções que estejam associadas a grupos de pontos de distribuição para poder utilizar a imagem de arranque numa sequência de tarefas. Utilize os passos seguintes para personalizar a imagem de arranque.  

    1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

    2.  Na área de trabalho **Biblioteca de Software**, expanda **Sistemas Operativos** e clique em **Imagens de Arranque**.  

    3.  Clique na imagem de arranque identificada no passo 3.  

    4.  No separador **Home Page**, no grupo **Implementação**, clique em **Atualizar Pontos de Distribuição**.  

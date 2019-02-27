---
title: Criar aplicações Windows
titleSuffix: Configuration Manager
description: Saiba mais informações sobre a criação e implantação de aplicativos do Windows no Configuration Manager.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: c70212962342bd254a5024c17bb292783b760233
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838876"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Criar aplicativos do Windows no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Além de outros requisitos do Configuration Manager e os procedimentos para o [criação de um aplicativo](/sccm/apps/deploy-use/create-applications), também de ter em conta as seguintes considerações ao criar e implementar aplicações em dispositivos Windows.  



## <a name="bkmk_general"></a> Considerações gerais  

O Configuration Manager suporta a implementação de pacote de aplicação do Windows (. AppX) e formatos de pacote (. appxbundle) de aplicação para Windows 8.1 e dispositivos Windows 10.

Quando cria uma aplicação na consola do Configuration Manager, selecione o ficheiro de instalação do aplicativo **tipo** como **pacote de aplicação do Windows (\*. AppX, \*. appxbundle, \*. msix, \*.msixbundle)**. Para obter mais informações sobre a criação de aplicações em geral, consulte [criem aplicativos](/sccm/apps/deploy-use/create-applications). Para obter mais informações sobre o formato MSIX, consulte [suporte para o formato MSIX](#bkmk_msix). 

> [!Note]  
> Para tirar partido das novas funcionalidades do Configuration Manager, primeiro de atualizar os clientes para a versão mais recente. Enquanto a nova funcionalidade surge na consola do Configuration Manager ao atualizar a consola e do site, o cenário completo não é funcional até que a versão do cliente também é a versão mais recente.<!--SCCMDocs issue 646-->  



## <a name="bkmk_provision"></a> Aprovisionar os pacotes de aplicações do Windows para todos os utilizadores num dispositivo
<!--1358310--> A partir da versão 1806, aprovisionar uma aplicação com um pacote de aplicação do Windows para todos os utilizadores no dispositivo. Um exemplo comum deste cenário é aprovisionar uma aplicação a partir da Microsoft Store para empresas e educação, como o Minecraft: Edição de educação, para todos os dispositivos utilizados pelos alunos de uma instituição de ensino. Anteriormente, o Configuration Manager apenas suportada a instalar estas aplicações por utilizador. Depois de iniciar sessão para um novo dispositivo, um estudante teria de espera para aceder a uma aplicação. Agora, quando a aplicação é aprovisionada no dispositivo para todos os utilizadores, eles podem ser produtivos mais rapidamente.

> [!Important]  
> Tenha cuidado com a instalação, aprovisionamento e a atualizar versões diferentes do mesmo pacote de aplicação do Windows num dispositivo, que poderá provocar resultados inesperados. Esse comportamento pode ocorrer ao utilizar o Gestor de configuração para aprovisionar a aplicação, mas, em seguida, permitindo que os usuários atualizar a aplicação a partir da Microsoft Store. Para obter mais informações, consulte a documentação de orientação passo seguinte quando [gerir aplicações a partir da Microsoft Store para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#next-steps).  

Quando aprovisionar uma aplicação com licença offline, o Configuration Manager não permite Windows automaticamente atualizá-la a partir da Microsoft Store.  

O Configuration Manager suporta o aprovisionamento de aplicações nas seguintes versões do Windows:<!--SCCMDocs-pr issue 2762-->
- Instale a ação: Windows 10, versão 1607 e posterior
- Ação de desinstalação: Windows 10, versão 1703 e posterior

Para configurar um tipo de implementação de aplicação do Windows para esta funcionalidade, ative a opção para **aprovisionar esta aplicação para todos os utilizadores no dispositivo**. Para obter mais informações, consulte [criem aplicativos](/sccm/apps/deploy-use/create-applications).


> [!Note]  
> Se precisar de desinstalar uma aplicação de aprovisionamento de dispositivos nas quais os utilizadores já tem iniciado sessão, tem de criar duas implementações de desinstalação. Destino a primeira implementação para uma coleção de dispositivos que contenha os dispositivos da desinstalação. O segundo de destino a implementação para uma coleção de utilizadores que contém os utilizadores que já tem sessão iniciada dispositivos com o aplicativo aprovisionado da desinstalação. Quando desinstalar uma aplicação aprovisionada num dispositivo, Windows atualmente não desinstale essa aplicação para os utilizadores também. 



## <a name="bkmk_msix"></a> Suporte para o formato MSIX
<!--1357427-->

A partir da versão 1806, o pacote de aplicação do Configuration Manager suporta o novo Windows 10 (.msix) e aplicação agrupar formatos (.msixbundle). Windows 10 versão 1809 ou posterior suportam a esses novos formatos.  

- Para uma descrição geral MSIX, consulte [atentamente MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).  

- Para saber como criar uma nova aplicação MSIX, consulte [introduzido no Insider 17682 de criar o suporte MSIX](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).  


### <a name="convert-applications-to-msix"></a>Converter aplicações para MSIX
<!--3607729, fka 1359029-->

A partir da versão 1810, converta seus aplicativos existentes do Windows Installer (MSI) para o formato MSIX. 

#### <a name="prerequisites"></a>Pré-requisitos
- Um dispositivo de referência com o Windows 10 versão 1809 ou posterior  

- Inicie sessão no Windows neste dispositivo como um utilizador com direitos administrativos locais  

- Instale as seguintes aplicações neste dispositivo:  

    - Consola do Configuration Manager  

    - Instalar o [ferramenta de empacotamento de MSIX](https://www.microsoft.com/store/productId/9N5LW3JBCXKF) da Microsoft Store  

    - Instalar o [driver de ferramenta de empacotamento de MSIX](https://docs.microsoft.com/windows/msix/packaging-tool/mpt-known-issues#msix-packaging-tool-driver-considerations)<!--SCCMDocs-pr issue #3091-->  

Não instale outras aplicações ou serviços neste dispositivo. É o sistema de referência. 

#### <a name="process-to-convert-applications-to-msix-format"></a>Processo para converter aplicações para o formato MSIX
1. Elevar a consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**e selecione o **aplicativos** nó.  

2. Selecione uma aplicação que tenha um tipo de implementação do Windows Installer (MSI).  

    > [!Note]  
    > Tem de ser capaz de aceder a conteúdo de origem do aplicativo a partir do dispositivo de referência.  
    > 
    > O nome da aplicação não pode ter carateres especiais. O Configuration Manager utiliza o nome da aplicação, como o nome do ficheiro de saída.  
    > 
    > Não, instale esta aplicação no dispositivo de referência com antecedência.  

3. Selecione **converter. MSIX** na faixa de opções.

Quando o assistente terminar, a ferramenta de empacotamento MSIX cria um ficheiro MSIX na localização especificada no assistente. Durante este processo, o Configuration Manager instala automaticamente a aplicação no dispositivo de referência.

Se o processo falhar, a página de resumo aponta para o ficheiro de registo com mais informações. Se existir um erro sobre como capturar o estado do utilizador, termine a sessão em Windows. Volte a iniciar sessão, poderá resolver este problema.

Para utilizar esta aplicação MSIX, primeiro tem de assinar digitalmente para que os clientes confiam nele. Para obter mais informações sobre este processo, consulte os artigos seguintes: 
- [A assinatura do pacote MSIX MSIX – a ferramenta de empacotamento MSIX –](https://blogs.msdn.microsoft.com/sgern/2018/09/06/msix-the-msix-packaging-tool-signing-the-msix-package/)
- [Como assinar um pacote do aplicativo usando o SignTool](https://docs.microsoft.com/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool)

Depois de iniciar a aplicação, crie um novo tipo de implementação na aplicação no Configuration Manager. Para obter mais informações, consulte [criar tipos de implementação para a aplicação](/sccm/apps/deploy-use/create-applications#bkmk_create-dt).




## <a name="bkmk_uwp"></a> Suporte para Windows Universal aplicações de plataforma (UWP)  

Dispositivos Windows 10 não requerem uma chave de sideload para instalar aplicações de linha de negócio. Para permitir o sideload no Windows, no entanto, a chave de registo `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` tem de ter um valor de **1**.  

Se não configurar esta chave de registo, o Configuration Manager define automaticamente este valor como **1** na primeira vez que implementa uma aplicação no dispositivo. Se tiver definido este valor **0**, Configuration Manager não pode alterar automaticamente o valor e ocorre uma falha de implementação da sua aplicação de linha de negócio.  

Assine digitalmente as aplicações de linha de negócio do UWP. Utilize um certificado de assinatura de código considerado fidedigno em cada dispositivo em que pretende implementar a aplicação. Utilização de certificados de PKI da sua organização ou comprar um certificado de um fornecedor de terceiros cujo certificado de raiz público já é considerado fidedigno pelo Windows.  

Para iniciar a sessão de pacotes de aplicações móveis, utilize a tabela seguinte para determinar o tipo de certificado de assinatura de código a utilizar:

| Pacote  | Symantec  | Não Symantec  |
|---------|---------|---------|
| Universal **. AppX** pacotes em dispositivos Windows 10 Mobile | Sim | Sim |
| **. xap** pacotes | Sim | Não | 
| **. AppX** pacotes incorporados para Windows Phone 8.1 para instalação em dispositivos Windows 10 Mobile | Sim | Não | 



## <a name="bkmk_mdm-msi"></a> Implementar aplicações do Windows Installer em dispositivos inscritos na MDM do Windows 10  

O **Windows Installer através de MDM (\*. msi)** tipo de implementação permite-lhe criar e implementar aplicações baseadas no Windows Installer em dispositivos inscritos na MDM com o Windows 10.  

Quando utiliza este tipo de implementação, considere os seguintes pontos:    

-   Carregar apenas um único ficheiro com a extensão MSI.  

-   O Configuration Manager utiliza o código de produto e versão do produto do ficheiro para deteção da aplicação.  

-   Windows utiliza o comportamento de reinício predefinido da aplicação. O Gestor de configuração não controlar o comportamento de reinício da aplicação.  

-   Pacotes MSI por utilizador são instalados para um único utilizador.  

-   Pacotes MSI por máquina são instalados para todos os utilizadores do dispositivo.  

-   O Configuration Manager suporta atualizações de aplicações. O código de produto MSI de cada versão tem de ser o mesmo.  

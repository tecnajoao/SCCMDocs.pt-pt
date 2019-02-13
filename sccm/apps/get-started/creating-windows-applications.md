---
title: Criar aplicações Windows
titleSuffix: Configuration Manager
description: Saiba mais informações sobre a criação e implantação de aplicativos do Windows no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1fa26147539abc611b86791f6dd9a4be0bc89c59
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156479"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Criar aplicativos do Windows no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Além de outros requisitos do Configuration Manager e os procedimentos para o [criação de um aplicativo](/sccm/apps/deploy-use/create-applications), também de ter em conta as seguintes considerações ao criar e implementar aplicações em dispositivos Windows.  



## <a name="bkmk_general"></a> Considerações gerais  

O Configuration Manager suporta a implementação de pacote de aplicação do Windows (. AppX) e formatos de pacote (. appxbundle) de aplicação para Windows 8.1 e dispositivos Windows 10.

A partir da versão 1806, Configuration Manager também suporta o Windows 10 novo pacote de aplicação (.msix) e aplicação agrupar formatos (.msixbundle). A versão mais recente [Windows Insider Preview](https://insider.windows.com/) compilações atualmente suportam estes novos formatos.<!--1357427-->  

- Para uma descrição geral MSIX, consulte [atentamente MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).  

- Para saber como criar uma nova aplicação MSIX, consulte [introduzido no Insider 17682 de criar o suporte MSIX](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).  

Quando cria uma aplicação na consola do Configuration Manager, selecione o ficheiro de instalação do aplicativo **tipo** como **pacote de aplicação do Windows (\*. AppX, \*. appxbundle, \*. msix, \*.msixbundle)**. Para obter mais informações, consulte [criem aplicativos](/sccm/apps/deploy-use/create-applications). 

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

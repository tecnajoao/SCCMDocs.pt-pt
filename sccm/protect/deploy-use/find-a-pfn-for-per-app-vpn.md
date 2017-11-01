---
title: "Localizar um nome de família de pacotes (PFN) para VPN por aplicação"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as duas formas de localizar um nome de família de pacotes, para que possa configurar uma VPN por aplicação."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47118499-3d26-4c25-bfde-b129de7eaa59
caps.latest.revision: "3"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 640f44985ad45442b05f2bbf4ee1ec9c2590cba4
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="find-a-package-family-name-pfn-for-per-app-vpn"></a>Localizar um nome de família de pacotes (PFN) para VPN por aplicação

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Existem duas formas de localizar um PFN para que possa configurar uma VPN por aplicação.

## <a name="find-a-pfn-for-an-app-thats-installed-on-a-windows-10-computer"></a>Localize um PFN para uma aplicação que está instalada num computador Windows 10

Se a aplicação estiver a trabalhar com já estiver instalada num computador Windows 10, pode utilizar o [Get-AppxPackage](https://technet.microsoft.com/library/hh856044.aspx) cmdlet do PowerShell para obter o PFN.

A sintaxe de Get-AppxPackage é:

` Parameter Set: __AllParameterSets`
` Get-AppxPackage [[-Name] <String> ] [[-Publisher] <String> ] [-AllUsers] [-User <String> ] [ <CommonParameters>]`

> [!NOTE]
> Poderá ter de executar o PowerShell como administrador para obter o PFN

Por exemplo, para obter informações sobre todas as aplicações universais instaladas no computador, utilize `Get-AppxPackage`.

Para obter informações sobre uma aplicação sabe o nome de, ou parte do nome, utilize `Get-AppxPackage *<app_name>`. Tenha em atenção a utilização do caráter universal, particularmente útil se não tiver a certeza do nome completo da aplicação. Por exemplo, para obter as informações para o OneNote, utilize `Get-AppxPackage *OneNote`.


Eis as informações obtidas para o OneNote:

`Name                   : Microsoft.Office.OneNote`

`Publisher              : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`

`Architecture           : X64`

`ResourceId             :`

`Version                : 17.6769.57631.0`

`PackageFullName        : Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`InstallLocation        : C:\Program Files\WindowsApps`

`\Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`IsFramework            : False`

**`PackageFamilyName      : Microsoft.Office.OneNote_8wekyb3d8bbwe`**

`PublisherId            : 8wekyb3d8bbwe`



## <a name="find-a-pfn-if-the-app-is-not-installed-on-a-computer"></a>Localize um PFN se a aplicação não estiver instalada num computador

1.  Aceda a https://www.microsoft.com/en-us/store/apps
2.  Introduza o nome da aplicação na barra de procura. No nosso exemplo, procure OneNote.
3.  Clique na ligação para a aplicação. Tenha em atenção que o URL a que acede tem uma série de letras no final. No nosso exemplo, o URL tem este aspeto:`https://www.microsoft.com/en-us/store/apps/onenote/9wzdncrfhvjl`
4.  Noutro separador, cole o seguinte URL, `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/<app id>/applockerdata`, substituindo `<app id>` com o id da aplicação obtida https://www.microsoft.com/en-us/store/apps - a série de letras no final do URL no passo 3. No nosso exemplo, o exemplo do OneNote, teria de colar: `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/9wzdncrfhvjl/applockerdata`.

No Edge, são apresentadas as informações que pretende; no Internet Explorer, clique em **abra** para ver as informações. O valor PFN é atribuído na primeira linha. Eis o aspeto dos resultados para o nosso exemplo:


`{`
`  "packageFamilyName": "Microsoft.Office.OneNote_8wekyb3d8bbwe",`
`  "packageIdentityName": "Microsoft.Office.OneNote",`
`  "windowsPhoneLegacyId": "ca05b3ab-f157-450c-8c49-a1f127f5e71d",`
`  "publisherCertificateName": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"`
`}`

---
title: Novidades no Guia do MDT 2013
titleSuffix: Microsoft Deployment Toolkit
description: 'Saiba mais sobre o Microsoft Deployment Toolkit 2013. '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: article
ms.assetid: 17466fa9-1a26-4dd8-a36f-c0c68fa1984c
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: fd207a77bad880a37cf04abc159aac6689a99afe
ms.sourcegitcommit: 645cd5a324bdd299906efa27eaca5885eafc9e9c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/16/2018
---
# <a name="whats-new-in-microsoft-deployment-toolkit-mdt-2013-guide"></a>Novidades no Guia do Microsoft Deployment Toolkit (MDT) 2013
Microsoft Deployment Toolkit (MDT) 2013 é a próxima versão do Microsoft Solution Accelerator para o sistema operativo e implementação de aplicação. O objetivo deste guia é explicação as alterações no MDT 2013 a partir do MDT 2012 Update 1.  

 Especificamente, este guia descreve a versão do MDT 2013 e pressupõe familiaridade com conceitos de versão anteriores do MDT, funcionalidades e capacidades.  

> [!NOTE]   
>  Neste documento, *Windows* aplica-se aos sistemas operativos Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2, exceto indicação em contrário. MDT não suporta ARM processador versões do Windows. Da mesma forma, *MDT* refere-se ao MDT 2013, salvo indicação em contrário.  

## <a name="whats-new-in-this-release"></a>Quais são as Novidades nesta versão  
 MDT inclui vários melhoramentos que adiciona novas funcionalidades e melhora a experiência de utilizador com o MDT. Além disso, esta versão do MDT inclui muitos outros melhoramentos pequenos e correções de erros que não estão listadas abaixo.  

### <a name="support-for-upgrading-from-previous-versions-of-mdt"></a>Suporte para atualizar a partir de versões anteriores do MDT  
 MDT suporta atualizar a partir do MDT 2012 Update 1.  

> [!NOTE]   
>  Crie uma cópia de segurança da infraestrutura existente do MDT antes de tentar uma atualização.  

### <a name="support-for-windows-81-and-windows-server-2012-r2"></a>Suporte para Windows 8.1 e Windows Server 2012 R2  
 Pode utilizar o MDT para implementar os sistemas operativos Windows 8.1 e Windows Server 2012 R2 utilizando os métodos de implementação LTI, ZTI e UDI. Funções e funcionalidades específicas do Windows 8.1 e Windows Server 2012 R2 estão disponíveis na lista de função.  

### <a name="support-for-the-windows-adk-for-windows-81"></a>Suporte para o Windows ADK para Windows 8.1  
 MDT suporta a utilização do Windows ADK para Windows 8.1 para implementar sistemas operativos. O Windows ADK para Windows 8.1 inclui as ferramentas de implementação, tais como a ferramenta Deployment Image Servicing and Management (DISM), o ambiente de pré-instalação do Windows (Windows PE) e a ferramenta de migração de estado de utilizador (USMT).  

### <a name="support-for-system-center-2012-r2-configuration-manager"></a>Suporte para o System Center 2012 R2 Configuration Manager  
 ZTI e métodos de implementação de UDI no MDT suportam a integração com o System Center 2012 R2 Configuration Manager, incluindo novas funcionalidades, como várias contas de acesso de rede.  

### <a name="improved-deployment-to-x86-based-computers-that-use-the-uefi-standard"></a>Implementação melhorada para computadores baseados em x86 que utilizam a norma UEFI  
 Unificada Extensible Firmware Interface (UEFI) é uma especificação que define uma interface de software entre um sistema operativo e o firmware da plataforma. UEFI é uma substituição mais segura para a interface de firmware de sistema básico de entrada/saída (BIOS) mais antiga presente em alguns computadores pessoais, que é vulnerável a software maligno que efetua a ataques durante o arranque ou de energia em processos de Self-testar.  

 Por predefinição, o MDT cria as partições apropriadas para suportar computadores com UEFI. MDT suporta versões do UEFI de 2.0 até 2.3.1. UEFI 2.3.1 é uma versão mais recente UEFI que será utilizada em computadores em conformidade com o logótipo do Windows 8.  

 Para obter mais informações sobre o suporte UEFI no MDT, consulte a secção "Implementar para computadores com UEFI", no documento MDT *utilizar o Microsoft Deployment Toolkit*.  

## <a name="whats-been-removed-from-this-release"></a>O que é que foram removido desta versão?  
 Esta versão do MDT não inclui as seguintes funcionalidades que existiam em versões anteriores do MDT:  

-   Implementação do Windows 8.1 Preview  

-   Implementação do Windows Server 2012 R2 Preview  

-   ZTI com  

    -   System Center Configuration Manager 2007  

    -   System Center 2012 Configuration Manager  

    -   System Center 2012 Configuration Manager SP1  

    -   System Center 2012 R2 Configuration Manager Preview  

-   Utilizar o Windows ADK para Windows 8  

-   Utilizar o Windows AIK para Windows 7  

-   Implementação do Windows XP ou Windows Server 2003  

-   Implementação do Windows Vista ou Windows Server 2008  

-   Out-of-box objetos política de grupo (GPOs) de Security Compliance Manager (SCM). Ferramentas e GPOs tem de ser instalados com o SCM antes de poderem ser utilizados no MDT.  

## <a name="operating-system-support-in-this-release"></a>Suporte do sistema operativo nesta versão  
A tabela seguinte lista o suporte do sistema operativo que LTI e fornecem implementações ZTI nesta versão do MDT.  

|||||  
|-|-|-|-|  
|Sistema Operativo|LTI|ZTI|UDI|  
|Windows 8,1|●|●|●|  
|Windows Server 2012 R2|●|●||  
|Windows 8|●|●|●|  
|Windows Server 2012|●|●||  
|Windows 7|●|●|●|  
|Windows Server 2008 R2|●|●||  
|Versão 5.0 do Windows PE|●|●|●|  

 ● = suportados  

## <a name="windows-adk-support"></a>Suporte do Windows ADK  
 A tabela seguinte lista o suporte do Windows ADK e o Windows AIK que fornecem implementações LTI, ZTI e UDI no MDT.  

|||||  
|-|-|-|-|  
|Windows ADK|LTI|ZTI|UDI|  
|Windows ADK para Windows 8.1|●|●|●|  

 ● = suportados  

## <a name="microsoft-net-framework-and-windows-powershell-support"></a>Microsoft .NET Framework e suporte do Windows PowerShell  
A tabela seguinte lista as versões do Microsoft .NET Framework e do Windows PowerShell de que são suportadas pelo MDT pela versão do sistema operativo Windows.  


||||  
|-|-|-|  
|Versão do Windows|.NET|PowerShell|  
|Windows 8,1|4.0|3.0|  
|Windows Server 2012 R2|4.0|3.0|  
|Windows 8|4.0|3.0|  
|Windows Server 2012|4.0|3.0|  
|Windows 7|3.5 com SP1|2.0|  
|Windows Server 2008 R2|3.5 com SP1|2.0|

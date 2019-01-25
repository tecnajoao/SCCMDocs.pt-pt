---
title: Como utilizar o plug-in de conversão
titleSuffix: Configuration Manager
description: Utilize o Gestor de conversão de pacotes Plug-in para personalizar os processos de análise e conversão.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 83cf156c-36de-483f-a9e6-2e06158f3b20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 5ed885ba459a584939881235e44d632515138cdf
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896367"
---
# <a name="how-to-use-the-package-conversion-manager-plug-in"></a>Como utilizar o Gestor de conversão de pacotes Plug-in

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1357861-->

O Gestor de conversão de pacotes Plug-in ajuda-o a personalizar os processos de análise e conversão. Para utilizar o Gestor de conversão de pacotes Plug-in, escreva um ficheiro executável ou script que efetue funcionalidades personalizadas. Em seguida, edite o ficheiro de configuração, configurationmanagement, para chamar o ficheiro executável ou script. As linguagens mais comuns usadas para escrever o script são VBScript ou PowerShell.

O Gestor de conversão de pacotes Plug-in é executado uma vez para cada pacote. Se analisa ou converter múltiplos pacotes ao mesmo tempo, o Gestor de conversão de pacotes Plug-in é executado cada vez.

> [!NOTE]  
> Para obter mais informações sobre os elementos de Gestor de conversão de pacotes no ficheiro de configuração do Configuration Manager, consulte [referência técnica para a configuração de plug-in do Gestor de conversão de pacotes XML](/sccm/apps/pcm/plugin-config-xml).



## <a name="default-process"></a>Processo padrão

Por predefinição, o Gestor de conversão de pacotes faz as seguintes ações:

1.  Leia um pacote do Configuration Manager.  

2.  Criar uma aplicação a partir do pacote e adicionar atributos predefinidos.  

3.  Analisar a aplicação e determinar um Estado de preparação do pacote.  

4.  Efetuar uma das seguintes ações, dependendo da operação do Gestor de conversão de pacotes:  

    - **Analisar**: Apresenta o estado de preparação do pacote na consola do Configuration Manager.  

    - **Converter**: Escreva a aplicação para a base de dados do Configuration Manager.  


## <a name="plug-in-based-process"></a>Processo de plug-in com base em 

Quando utilizar o plug-in, o Gestor de conversão de pacotes faz as seguintes ações:

1.  Leia um pacote do Configuration Manager.  

2.  Criar uma aplicação a partir do pacote e adicionar atributos predefinidos.  

3.  Converta a aplicação em XML. Em seguida, guarde o ficheiro no disco.  

4.  Execute o script de plug-in para modificar a aplicação XML. Para obter mais informações, consulte [referência técnica para a configuração de plug-in do Gestor de conversão de pacotes XML](/sccm/apps/pcm/plugin-config-xml).  

5.  Converta a aplicação XML numa aplicação do Configuration Manager.  

6.  Analisar a aplicação e determinar um Estado de preparação do pacote.  

7.  Efetuar uma das seguintes ações, dependendo da operação do Gestor de conversão de pacotes:  

    - **Analisar**: Apresenta o estado de preparação do pacote na consola do Configuration Manager.  

    - **Converter**: Escreva a aplicação à base de dados do Configuration Manager.  



## <a name="see-also"></a>Consulte também

[Referência técnica para a configuração de plug-in do Gestor de conversão de pacotes XML](/sccm/apps/pcm/plugin-config-xml)

---
title: "Ferramenta de registo de atualização"
titleSuffix: Configuration Manager
description: "Determinar quando e como utilizar a ferramenta de registo de atualização para importar manualmente uma atualização para a consola do Configuration Manager."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
caps.latest.revision: "8"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 2e62d3d1df75bd7edd7ef12e7cefd7613cf794bd
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-system-center-configuration-manager"></a>Utilizar a Ferramenta de Registo de Atualização para importar correções para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Algumas atualizações do Configuration Manager não estão disponíveis no serviço em nuvem Microsoft e só são obtidas fora de banda. Um exemplo é uma correção de versão limitada para resolver um problema específico.   
Quando tem de instalar uma versão de fora de banda e o nome de ficheiro de atualização ou correção termina com a extensão **update.exe**, utilize o **ferramenta de registo de atualização** para importar manualmente a atualização para a consola do Configuration Manager. A ferramenta permite extrair e transferir o pacote de atualização para o servidor do site e registar a atualização na consola do Configuration Manager.  

 Se o ficheiro de correção tiver a **.exe** extensão de ficheiro (não **update.exe**), consulte [utilizar o instalador de correções para instalar atualizações para o System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  

> [!NOTE]  
>  Este tópico fornece orientações gerais sobre como instalar correções que atualizam o System Center Configuration Manager. Para obter detalhes sobre uma correção ou atualização específica, consulte o artigo da Base de dados de conhecimento (KB) correspondente no Support da Microsoft.  

 **Pré-requisitos para utilizar a ferramenta de registo de atualização:**  

-   Apenas fora de banda de atualizações que terminam com o **. update.exe** extensão pode ser instalada utilizando esta ferramenta  

-   A ferramenta é autónoma e contém as atualizações individuais que obtém diretamente da Microsoft  

-   A ferramenta não tem uma dependência sobre o modo do ponto de ligação de serviço  

-   A ferramenta deve ser executada no computador que aloja o ponto de ligação de serviço  

-   O computador onde a ferramenta é executada (o computador de ponto de serviço do ligação) tem de ter o Framework .NET 4.52 instalado  

-   A conta que utiliza para executar a ferramenta tem de ter **administrador local** permissões no computador que aloja o ponto de ligação de serviço (onde a ferramenta é executada)  

-   A conta que utiliza para executar a ferramenta tem de ter **escrever** permissões para a seguinte pasta no computador que aloja o ponto de ligação de serviço:  **&lt;Diretório de instalação do ConfigMgr\>\EasySetupPayload\offline**  

### <a name="to-use-the-update-registration-tool"></a>Utilizar a ferramenta de registo de atualização  

1.  No computador que aloja o ponto de ligação de serviço:  

    -   Abra uma linha de comandos com privilégios administrativos e, em seguida, altere os diretórios para a localização que contém  **&lt;produto\>-&lt;versão do produto\>-&lt;ID do artigo KB\>-ConfigMgr.Update.exe**  

2.  Execute o seguinte comando para iniciar a ferramenta de registo de atualização:  

    -   **&lt;Produto\>-&lt;versão do produto\>-&lt;ID do artigo KB\>-ConfigMgr.Update.exe**  

    Depois de a correção ser registada, é apresentada como uma nova atualização na consola no prazo de 24 horas.  Pode acelerar o processo:

    - Abra a consola do Configuration Manager e aceda a **administração** > **atualizações e manutenção**e, em seguida, clique em **procurar atualizações**. (Antes da versão 1702, atualizações e manutenção estava **administração** > **serviços em nuvem**.) 

    A ferramenta de registo de atualização regista as ações num ficheiro .log no computador local. O ficheiro de registo tem o mesmo nome como ficheiro .exe e é escrito o **%SystemRoot%/Temp** pasta.  

     Depois de a atualização ser registada, pode fechar a ferramenta de registo de atualização.  

3.  Abra a consola do Configuration Manager e navegue para **administração** > **atualizações e manutenção**. As correções importadas estão agora disponíveis para instalação. (Antes da versão 1702, atualizações e manutenção estava **administração** > **serviços em nuvem**.)

 Para obter informações sobre a instalação de atualizações, consulte [instalar atualizações na consola do System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  

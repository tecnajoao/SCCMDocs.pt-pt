---
title: Instalar o Updates Publisher
titleSuffix: Configuration Manager
description: Instale o System Center Updates Publisher em seu ambiente
ms.date: 02/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 37a468a2b9727d66f7d3fe0cafd1aae044585b2a
ms.sourcegitcommit: e18853c214c95e4d21b2f032aba6d17c21e97027
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/20/2019
ms.locfileid: "56443958"
---
# <a name="install-updates-publisher"></a>Instalar o Updates Publisher

*Aplica-se a: System Center Updates Publisher*

As informações nestes artigos podem ajudá-lo a transferir, instalar e configurar o Updates Publisher para utilização com o seu ambiente do System Center Configuration Manager.

## <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações
System Center Updates Publisher só pode ser utilizado com o System Center Configuration Manager. Ele não é destinado ao uso com hierarquias WSUS autónomos.

As secções seguintes detalham os requisitos para instalar e utilizar o Updates Publisher e limitações ou problemas conhecidos para a sua utilização.  

### <a name="operating-systems"></a>Sistemas operativos
Instalar e executar o Updates Publisher num edições de 64 bits dos sistemas operativos seguintes. Não há nenhuma atualização cumulativa mínima ou requisitos de pacote de serviço.

-   Windows Server 2016 (Standard, Datacenter)
-   Windows Server 2012 R2 (Standard, Datacenter)
-   Windows 10 (Pro, Education, Pro Education, Enterprise)
-   Windows 8.1 (Professional, Enterprise)

### <a name="prerequisites"></a>Pré-requisitos
A seguir é necessárias no computador que executa o Updates Publisher.

-   **sistema operativo de 64 bits**: O computador onde instalou o Updates Publisher tem de executar um sistema operativo de 64 bits.
-   **WSUS 4.0 ou posterior**:
    -   No Windows Server, instale a consola de administração para cumprir este requisito de predefinição.
    -   Para Windows 10 e Windows 8.1, instalar o [remoto administração ferramentas servidor (FARS) para sistemas de operativos Windows](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems). Esta ação instala o suporte necessário para utilizar o Updates Publisher (*cmdlets do PowerShell e API*, e *Console de gerenciamento de Interface do usuário*).
-   **Permissões**:
    -   Instalação: Administrador local
    -   A maioria das operações: utilizador local
    -   A publicação ou operações que envolvem o WSUS: Membro do grupo de administradores WSUS no servidor WSUS.

### <a name="supported-languages"></a>Idiomas suportados
Publicador de atualizações está disponível apenas em inglês, mas pode gerir atualizações para outros idiomas. O suporte ao idioma depende da tarefa, como publicação, criar ou editar as atualizações.

Quando exportar ou a publicação de atualizações, o Updates Publisher exibe o título e descrição da atualização de software com base na localidade do computador onde está instalado o Updates Publisher.

Por exemplo, criar uma atualização de software que tem um título de inglês e espanhol.

-   Se criar a atualização num computador cujas localidades é o inglês, por padrão, veria o título e a descrição em inglês.
-   Se, em seguida, exportar ou publicar essa atualização para um computador cujas localidades é o espanhol, nesse computador veria o título e a descrição em espanhol.

### <a name="publishing"></a>Publicação
Quando publica atualizações de software, pode especificar o idioma do ficheiro de binários de atualização de software. Também pode especificar que o binário é o idioma neutro. São suportados os seguintes idiomas:

-   Árabe
-   Chinês (RAE de Hong Kong)
-   Chinês (Tradicional)
-   Chinês (Simplificado)
-   Checo
-   Dinamarquês
-   Neerlandês
-   Inglês
-   Finlandês
-   Francês
-   Alemão
-   Grego
-   Hebraico
-   Húngaro
-   Italiano
-   Japonês
-   Coreano
-   Norueguês
-   Polaco
-   Português
-   Português (Brasil)
-   Russo
-   Espanhol
-   Sueco
-   Turco

### <a name="software-update-titles-and-descriptions"></a>Títulos de atualização de software e as descrições
Os seguintes idiomas são suportados para títulos de atualização de software e as descrições.

-   Chinês (Tradicional)
-   Chinês (Simplificado)
-   Inglês
-   Francês
-   Alemão
-   Italiano
-   Japonês
-   Coreano
-   Português (Brasil)
-   Russo
-   Espanhol



## <a name="install-updates-publisher"></a>Instalar o Updates Publisher
Obter o **UpdatesPubliser.msi** para instalar a partir do System Center Updates Publisher a [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=55543).

Para instalar o Updates Publisher, execute **UpdatesPublisher.msi** num computador que cumpra os *pré-requisitos*. O instalador cria a pasta seguinte para incluir os ficheiros necessários para executar o Updates Publisher:  *&lt;caminho&gt;\Program Files\Microsoft\UpdatesPublisher*.

Uma vez que esta pasta contém todos os ficheiros necessários para utilizar o Updates Publisher, pode copiar a pasta e o respetivo conteúdo para uma localização nova ou computador e, em seguida, utilizar o Updates Publisher a partir dessa localização. No entanto, a nova localização ou o computador tem de cumprir os pré-requisitos para executar o Updates Publisher.

Depois de concluída a instalação, execute **UpdatesPublisher.exe** partir do *UpdatesPublisher* pasta para iniciar o Updates Publisher.

## <a name="next-steps"></a>Passos seguintes
 Depois de instalar o Updates Publisher, recomendamos que [configurar as opções](updates-publisher-options.md) para o Updates Publisher. Tem de configurar algumas opções antes de poder utilizar alguns recursos do Updates Publisher.

 No entanto, se deseja usar os padrões e não pretenda implementar atualizações para um servidor de atualização ou para dispositivos geridos, pode avançar diretamente para [gerenciamento de catálogos de atualizações de software](updates-publisher-catalogs.md), ou [criar atualizações de software](create-updates-with-updates-publisher.md) e Crie catálogos de atualizações de seus próprios.


---
title: "Instalar o publicador de atualizações"
titleSuffix: Configuration Manager
description: Instalar o System Center Updates Publisher no seu ambiente
ms.custom: na
ms.date: 07/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
caps.latest.revision: "1"
author: mestew
ms.author: mstewart
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 629e7dd98b1b5ff7f240461b61893dfc433f61dc
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="install-updates-publisher"></a>Instalar o publicador de atualizações

*Aplica-se a: O System Center Updates Publisher*

As informações neste tópico podem ajudar a obter, instalar e configurar o Updates Publisher para utilização com o seu ambiente.


## <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações
As secções seguintes requisitos para instalar e utilizar o Updates Publisher e limitações ou problemas conhecidos para a sua utilização de detalhe.

### <a name="operating-systems"></a>Sistemas operativos
Instalar e executar o Updates Publisher um edições de 64 bits dos sistemas operativos seguintes. Existem não requisitos de pacote de serviço ou atualização cumulativa mínima.

-   Windows Server 2016 (Standard, Datacenter)
-   Windows Server 2012 R2 (Standard, Datacenter)
-   Windows 10 (Pro, Education, educação Pro, Enterprise)
-   Windows 8.1 (Professional, Enterprise)

### <a name="prerequisites"></a>Pré-requisitos
Os seguintes são necessárias no computador que executa o Updates Publisher.

-   **sistema operativo de 64 bits**: O computador onde instalou o Updates Publisher tem de executar um sistema operativo de 64 bits.
-   **WSUS 4.0 ou posterior**:
    -   No Windows Server, instale a consola de administração para cumprir este requisito de predefinição.
    -   Para Windows 10 e Windows 8.1, instale o [remoto servidor ferramentas de administração (FARS) para sistemas operativos Windows](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems). Esta ação instala o suporte necessário para utilizar o Updates Publisher (*cmdlets API e PowerShell*, e *consola de gestão de Interface de utilizador*).
-   **Permissões**:
    -   Instalação: Administrador local
    -   A maioria das operações: utilizador local
    -   A publicação ou operações que envolvem o WSUS: Membro do grupo de administradores do WSUS no servidor WSUS.

### <a name="supported-languages"></a>Idiomas suportados
Publicador de atualizações está disponível apenas em inglês, mas pode gerir as atualizações para outros idiomas. O suporte de idioma depende da tarefa, tal como a publicação, criar ou editar as atualizações.

Quando exportar ou publicação de atualizações, o Updates Publisher apresenta o título e a descrição da atualização de software com base na região do computador onde está instalado o Updates Publisher.

Por exemplo, crie uma atualização de software que tenha um título inglês e espanhol.

-   Se criar a atualização num computador cujo região é o inglês, por predefinição, verá o título e a descrição em inglês.
-   Se exportar ou publicar que a atualização para um computador cujo região é espanhol, nesse computador verá o título e descrição espanhol.

### <a name="publishing"></a>Publicar
Quando publicar as atualizações de software, pode especificar o idioma do ficheiro binário de atualização de software. Também pode especificar que o binário é independente de idioma. São suportados os seguintes idiomas:

-   Árabe
-   Chinês (RAE de Hong Kong)
-   Chinês (tradicional)
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

### <a name="software-update-titles-and-descriptions"></a>Títulos de atualização de software e descrições
Os seguintes idiomas são suportados para títulos de atualização de software e descrições.

-   Chinês (tradicional)
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



## <a name="install-updates-publisher"></a>Instalar o publicador de atualizações
Obter o **UpdatesPubliser.msi** para instalar a partir do System Center Updates Publisher o [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=847967).

Para instalar o Updates Publisher, execute **UpdatesPublisher.msi** num computador que cumpra o *pré-requisitos*. O instalador cria a seguinte pasta que contém os ficheiros necessários para executar o Updates Publisher:  *&lt;caminho&gt;\Program Files\Microsoft\UpdatesPublisher*.

Porque esta pasta contém todos os ficheiros necessários para utilizar o Updates Publisher, pode copiar a pasta e respetivo conteúdo para uma localização nova ou o computador e, em seguida, utilizar o Updates Publisher a partir dessa localização. No entanto, a nova localização ou o computador tem de cumprir os pré-requisitos para executar o Updates Publisher.

Depois de concluída a instalação, execute **UpdatesPublisher.exe** do *UpdatesPublisher* pasta para iniciar o Updates Publisher.

## <a name="next-steps"></a>Passos seguintes
 Depois de instalar o Updates Publisher, recomendamos que [configurar as opções](updates-publisher-options.md) para o Updates Publisher. Tem de configurar algumas opções antes de poder utilizar algumas funcionalidades do Updates Publisher.

 No entanto, se pretender utilizar as predefinições e não planear implementar atualizações para um servidor de atualização ou para dispositivos geridos, pode avançar diretamente para [gerir catálogos de atualização de software](updates-publisher-catalogs.md), ou [criar atualizações de software](create-updates-with-updates-publisher.md) e criar catálogos de atualização do seu próprio.


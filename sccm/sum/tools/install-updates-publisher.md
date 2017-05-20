---
title: "Instala o Publisher atualizações | Documentos do Microsoft"
description: Instalar o System Center Updates Publisher no seu ambiente
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
caps.latest.revision: 1
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.translationtype: Machine Translation
ms.sourcegitcommit: 90775fcf2549080a43e9c1606caa79d9eb90a89c
ms.openlocfilehash: 996766d0bd9ab2a3acb1970414f0ae511d97fbff
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="install-updates-publisher"></a>Instalar o Updates Publisher

*Aplica-se a: System Center Updates Publisher*

As informações neste tópico podem ajudar a obter, instalar e configurar o Updates Publisher para utilização com o seu ambiente.


## <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações
As secções seguintes descrevem pormenorizadamente requisitos para instalar e utilizar o Updates Publisher e limitações ou problemas conhecidos para poder ser utilizado.

### <a name="operating-systems"></a>Sistemas operativos
Instalar e executar o Updates Publisher num edições de 64 bits dos sistemas operativos seguintes. Não existem sem atualização cumulativa mínima ou requisitos de pacote de serviço.

-   Windows Server 2016 (Standard, Datacenter)
-   Windows Server 2012 R2 (Standard, Datacenter)
-   Windows 10 (Pro, educação, educação Pro, Enterprise)
-   Windows 8.1 (Professional, Enterprise)

### <a name="prerequisites"></a>Pré-requisitos
É necessários o seguinte procedimento no computador que executa o Updates Publisher.

-   **sistema operativo de 64 bits**: O computador onde irá instalar o Updates Publisher tem de executar um sistema operativo de 64 bits.
-   **WSUS 4.0 ou posteriores**:
    -   No Windows Server, instale a consola de administração para cumprir este requisito de predefinição.
    -   Para Windows 10 e Windows 8.1, instale o [remoto servidor administração ferramentas (RSAT) para sistemas operativos Windows](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems). Esta ação instala o suporte necessário para utilizar o Updates Publisher (*cmdlets API e PowerShell*, e *consola de gestão de Interface de utilizador*).
-   **Permissões**:
    -   Instalação: Administrador local
    -   Maioria das operações: utilizador local
    -   A publicação ou operações que impliquem a WSUS: Membro do grupo de administradores do WSUS no servidor WSUS.

### <a name="supported-languages"></a>Idiomas suportados
Updates Publisher está disponível apenas em inglês, mas pode gerir atualizações para outros idiomas. O suporte de idioma depende a tarefa, tal como a publicação, criando ou editando as atualizações.

Ao exportar ou publicação de atualizações, o Updates Publisher apresenta o título e a descrição da atualização de software com base na região do computador onde está instalado o Updates Publisher.

Por exemplo, crie uma atualização de software que tem um título de inglês e espanhol.

-   Se criar a atualização num computador cujo região for inglês, por predefinição, verá o título e a descrição em inglês.
-   Se, em seguida, exportar ou publicar essa atualização para um computador cujo região é espanhol, nesse computador que veria o título e a descrição em espanhol.

### <a name="publishing"></a>Publicação
Quando publica atualizações de software, pode especificar o idioma de ficheiro binário de atualização de software. Também pode especificar que o binário é independente do idioma. São suportados os seguintes idiomas:

-   Árabe
-   Chinês (RAE de Hong Kong s.a.r.)
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

### <a name="software-update-titles-and-descriptions"></a>Títulos de atualização de software e as descrições
Os seguintes idiomas são suportados para títulos de atualização de software e as descrições.

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



## <a name="install-updates-publisher"></a>Instalar o Updates Publisher
Obter o **UpdatesPubliser.msi** para instalar o System Center Updates Publisher, a partir de [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=847967).

Para instalar o Updates Publisher, execute **UpdatesPublisher.msi** num computador que cumpra os *pré-requisitos*. O instalador cria a seguinte pasta que contém os ficheiros necessários para executar o Updates Publisher:  *&lt;caminho&gt;\Program Files\Microsoft\UpdatesPublisher*.

Porque esta pasta contém todos os ficheiros necessários para utilizar o Updates Publisher, pode copiar a pasta e respetivo conteúdo para uma localização nova ou o computador e, em seguida, utilizar o Updates Publisher a partir dessa localização. No entanto, a nova localização ou o computador tem de cumprir os pré-requisitos para executar o Updates Publisher.

Depois de concluída a instalação, execute **UpdatesPublisher.exe** a partir de *UpdatesPublisher* pasta para iniciar o Updates Publisher.

## <a name="next-steps"></a>Passos seguintes
 Depois de instalar o Updates Publisher, recomendamos que [configurar as opções](/tools/updates-publisher-options) Updates Publisher. Tem de configurar algumas opções antes de poder utilizar algumas funcionalidades do Updates Publisher.

 No entanto, se pretender utilizar as predefinições e não planear implementar atualizações para um servidor de atualização ou para dispositivos geridos, pode ir para a direita para [gerir catálogos de atualização de software](/tools/updates-publisher-catalogs), ou [criar atualizações de software](/tools/create-updates-with-updates-publisher) e criar catálogos de atualização do seu próprio.


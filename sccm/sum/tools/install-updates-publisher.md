---
title: Instalar o Updates Publisher | Microsoft Docs
description: Instale o System Center Updates Publisher em seu ambiente
ms.custom: na
ms.date: 07/03/2017
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
ms.sourcegitcommit: 70772ba7d08560aa66abcce29dc6cc6334aa2032
ms.openlocfilehash: 63ea0383497a3f06870c0907c732010259d1a809
ms.contentlocale: pt-pt
ms.lasthandoff: 07/03/2017

---
# <a name="install-updates-publisher"></a>Instalar o Updates Publisher

*Aplica-se a: System Center Updates Publisher*

As informações neste tópico podem ajudá-lo a obter, instalar e configurar o Updates Publisher para uso com o seu ambiente.


## <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações
As seções a seguir detalham os requisitos para instalar e usar o Updates Publisher e limitações ou os problemas conhecidos para seu uso.

### <a name="operating-systems"></a>Sistemas operativos
Instale e execute o Updates Publisher em um edições de 64 bits dos sistemas operacionais a seguir. Não existem requisitos de service pack ou atualização cumulativa mínima.

-   Windows Server 2016 (Standard, Datacenter)
-   Windows Server 2012 R2 (Standard, Datacenter)
-   Windows 10 (Pro, Education, educação Pro, Enterprise)
-   Windows 8.1 (Professional, Enterprise)

### <a name="prerequisites"></a>Pré-requisitos
A seguir é necessários no computador que executa o Updates Publisher.

-   **sistema operacional de 64 bits**: O computador onde você instala o Updates Publisher deve executar um sistema operacional de 64 bits.
-   **WSUS 4.0 ou posterior**:
    -   No Windows Server, instale o Console de administração para atender a esse requisito padrão.
    -   Para Windows 10 e Windows 8.1, instale o [remoto ferramentas (Administração de servidor) para sistemas operacionais Windows](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems). Isso instala o suporte necessário para usar o Updates Publisher (*API e cmdlets do PowerShell*, e *Console de gerenciamento de Interface do usuário*).
-   **Permissões**:
    -   Instalação: Administrador local
    -   A maioria das operações: usuário local
    -   Publicação ou operações que envolvem o WSUS: Membro do grupo de administradores do WSUS no servidor do WSUS.

### <a name="supported-languages"></a>Idiomas com suporte
O Updates Publisher está disponível somente em inglês, mas pode gerenciar atualizações para outros idiomas. O suporte de idioma depende da tarefa, como publicação, criando ou editando as atualizações.

Ao exportar ou publicar atualizações, o Updates Publisher exibe o título e a descrição da atualização de software com base na localidade do computador onde o Updates Publisher é instalado.

Por exemplo, você pode criar uma atualização de software com um título em inglês e espanhol.

-   Se você criar a atualização em um computador cujo local é o inglês, por padrão, você verá o título e a descrição em inglês.
-   Se, em seguida, exportar ou publicar essa atualização em um computador cujo local é o espanhol, nesse computador você veria o título e a descrição em espanhol.

### <a name="publishing"></a>Publicação
Quando você publicar atualizações de software, você pode especificar o idioma do arquivo binário de atualização de software. Você também pode especificar que o binário é neutralidade de idioma. Há suporte para os seguintes idiomas:

-   Árabe
-   Chinês (RAE de Hong Kong)
-   Chinês (tradicional)
-   Chinês (Simplificado)
-   Checo
-   Dinamarquês
-   Holandês
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

### <a name="software-update-titles-and-descriptions"></a>Descrições e títulos de atualização de software
Os idiomas a seguir têm suporte para obter descrições e títulos de atualização de software.

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
Obter o **UpdatesPubliser.msi** para instalar o System Center Updates Publisher do [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=847967).

Para instalar o Updates Publisher, execute **UpdatesPublisher.msi** em um computador que atenda a *pré-requisitos*. O instalador cria a seguinte pasta para conter os arquivos necessários para executar o Updates Publisher:  *&lt;caminho&gt;\Program Files\Microsoft\UpdatesPublisher*.

Porque esta pasta contém todos os arquivos necessários para usar o Updates Publisher, você pode copiar a pasta e seu conteúdo para um novo local ou o computador e, em seguida, usar o Updates Publisher desse local. No entanto, o novo local ou o computador deve atender aos pré-requisitos para executar o Updates Publisher.

Após a conclusão da instalação, execute **UpdatesPublisher.exe** do *UpdatesPublisher* pasta para iniciar o Updates Publisher.

## <a name="next-steps"></a>Passos seguintes
 Depois de instalar o Updates Publisher, é recomendável que você [Configurando as opções](updates-publisher-options.md) para o Updates Publisher. Você deve configurar algumas opções antes de poder usar alguns recursos do Updates Publisher.

 No entanto, se você quiser usar os padrões e não pretende implantar as atualizações para um servidor de atualização ou a dispositivos gerenciados, você pode ir direito [Gerenciando catálogos de atualização de software](updates-publisher-catalogs.md), ou [criar atualizações de software](create-updates-with-updates-publisher.md) e criar catálogos de atualização de sua preferência.


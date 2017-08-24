---
title: "Sobre a atualização, atualização e instalação | Microsoft Docs"
description: "Saiba a diferença entre os termos de licenciamento para a instalação, atualização e atualização, quando gerir a infraestrutura do Configuration Manager."
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
caps.latest.revision: "0"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 6bd6cd7ea3c41fa1d70e17a1290c9f1f74cc9e37
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Sobre a atualização, atualizar e instalar a infraestrutura de hierarquia e site

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Ao gerir o site do System Center Configuration Manager e a infraestrutura de hierarquia, os termos de licenciamento *atualizar*, *atualizar*, e *instalar* são utilizados para descrever três conceitos diferentes.

## <a name="upgrade"></a>Atualização
*Atualizar* ou *atualização no local*, é utilizado ao converter o site do Configuration Manager 2012 ou a hierarquia para um que executa o System Center Configuration Manager.
Quando atualizar o System Center 2012 Configuration Manager para o System Center Configuration Manager, continuar a utilizar os mesmos servidores para alojar o seus sites e servidores de site e manter os dados existentes e configurações do Configuration Manager.  Isto é diferente do [migração](/sccm/core/migration/migrate-data-between-hierarchies) que é uma forma de manter os dados sobre os dispositivos geridos e configurações durante a utilização de novos sites do System Center Configuration Manager instalados para novo hardware.

Para obter mais detalhes, consulte [atualizar para o System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).



## <a name="update"></a>Atualização
*Atualização* é utilizado para instalar atualizações na consola do System Center Configuration Manager e para atualizações fora de banda que são as atualizações que não não possível entregar a partir da consola do Configuration Manager. Atualizações na consola podem modificar a versão do seu site Current Branch (ou sites Technical Preview), de modo a que é executada uma versão superior. Por exemplo, que se o seu site executa a versão 1606, pode instalar uma atualização para a versão 1610. Atualizações também podem instalar correções para um problema conhecido, sem modificar a versão de sites.      

Normalmente, as atualizações de adicionar correções de segurança, novas funcionalidades e melhoramento da qualidade, a sua implementação existente. Se utilizar o ramo do Technical Preview, uma atualização pode instalar uma versão mais recente do Technical Preview.
-   Escolher quando instalar a atualização na consola, começando no site de nível superior da hierarquia.
- Pode instalar qualquer atualização que está disponível a partir da consola. Por exemplo, se o site executa a versão 1602 e são disponibilizadas 1606 e 1610, deve considerar a instalar a versão 1610 porque cada versão inclui as funcionalidades que foram primeiro disponibilizada em versões lançadas anteriormente.
- Após uma nova atualização concluir a instalação no seu site de nível superior, os sites primários subordinados iniciam automaticamente o processo de atualização. No entanto, pode definir [períodos](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkservicewindowa-service-windows-for-site-servers) para controlar a temporização das atualizações.
- Os sites secundários não instalam automaticamente as atualizações. Em vez disso, é iniciada manualmente a atualização da consola do Configuration Manager.

Para obter mais informações, consulte [atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates), e [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).



## <a name="install"></a>Instalar
*Instalar* é utilizado quando criar uma nova hierarquia do Configuration Manager a partir do zero ou adicionar sites adicionais para uma hierarquia existente.  

Quando instala um novo site primário ou site de administração central, a localização de setup.exe e os respetivos ficheiros de origem relacionados que utilizar depende do seu cenário de instalação.

Para obter mais informações, consulte [preparar para instalar sites](/sccm/core/servers/deploy/install/prepare-to-install-sites).

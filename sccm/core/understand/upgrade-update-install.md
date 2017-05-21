---
title: "Sobre a atualização, atualização e instalação | Documentos do Microsoft"
description: "Saiba a diferença entre os termos de instalação, atualização e atualização, ao gerir a infraestrutura do Configuration Manager."
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
caps.latest.revision: 0
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0d0735c170820259ac8bb6706aac7cc5569a1628
ms.openlocfilehash: 6bd6cd7ea3c41fa1d70e17a1290c9f1f74cc9e37
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---

# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Sobre a atualização, atualizar e instalar o site e da hierarquia de infraestrutura

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Ao gerir o site do System Center Configuration Manager e a infraestrutura da hierarquia, os termos *atualizar*, *atualizar*, e *instalar* são utilizados para descrever três conceitos separados.

## <a name="upgrade"></a>Atualização
*Atualizar* ou *atualização no local*, é utilizada ao converter o site do Configuration Manager 2012 ou a hierarquia para um que executa o System Center Configuration Manager.
Quando atualizar o System Center 2012 Configuration Manager para System Center Configuration Manager, continuar a utilizar os mesmos servidores para alojar os seus sites e servidores de sites e manter os dados existentes e configurações para o Configuration Manager.  Isto é diferente do [migração](/sccm/core/migration/migrate-data-between-hierarchies) que é uma forma de reter os configurações e os dados sobre os dispositivos geridos ao utilizar os novos sites de System Center Configuration Manager instalados para novo hardware.

Para obter mais detalhes, consulte o artigo [atualizar para o System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).



## <a name="update"></a>Atualização
*Atualização* é utilizada para instalar atualizações na consola do System Center Configuration Manager e para fora de banda atualizações que são as atualizações que não não possível entregar a partir da consola do Configuration Manager. Na consola atualizações podem modificar a versão do seu site de ramo atual (ou o site de pré-visualização técnica), para que executa uma versão superior. Por exemplo, que se o site executa versão 1606, é possível instalar uma atualização para a versão 1610. As atualizações também podem instalar correções para um problema conhecido, sem modificar a versão de sites.      

Normalmente, as atualizações de adicionar correções de segurança, melhoramento da qualidade e novas funcionalidades à implementação existente. Se utilizar o ramo de pré-visualização técnica, uma atualização pode instalar uma versão mais recente da pré-visualização técnica.
-    Pode escolher quando instalar a atualização na consola, começando no site de nível superior da hierarquia.
- É possível instalar qualquer atualização que está disponível a partir de dentro da consola. Por exemplo, se o seu site for executada versão 1602 e 1606 e 1610 oferecida, deve considerar a instalar a versão 1610 porque cada versão inclui funcionalidades que foram primeira disponibilizada em versões lançadas anteriormente.
- Após uma nova atualização concluir a instalação no seu site de nível superior, os sites primários subordinados iniciar automaticamente o processo de atualização. No entanto, pode definir [Windows serviço](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkservicewindowa-service-windows-for-site-servers) para controlar a temporização das atualizações.
- Os sites secundários não instalam automaticamente as atualizações. Em vez disso, é iniciada manualmente a atualização a partir da consola do Configuration Manager.

Para obter mais informações, consulte o artigo [atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates), e [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).



## <a name="install"></a>Instalar
*Instalar* é utilizada ao criar uma nova hierarquia do Configuration Manager a partir do zero ou adicionar sites adicionais para uma hierarquia existente.  

Quando instala um novo site primário ou site de administração central, a localização do setup.exe e dos ficheiros de origem relacionados que utilizar depende do cenário de instalação.

Para obter mais informações, consulte o artigo [preparar a instalar sites](/sccm/core/servers/deploy/install/prepare-to-install-sites).


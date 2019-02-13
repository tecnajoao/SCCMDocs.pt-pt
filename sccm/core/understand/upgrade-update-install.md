---
title: Sobre a atualização, atualização e instalação
titleSuffix: Configuration Manager
description: Aprenda a diferença entre os termos de instalação, atualização e a atualização, ao gerir a infraestrutura do Configuration Manager.
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: df4daee11a72100debb93270fc6e51ab1a5e2622
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140049"
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Sobre a atualização de versão, atualização e instalação da infraestrutura de hierarquia e site

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Ao gerir o site do System Center Configuration Manager e a infraestrutura de hierarquia, os termos *atualizar*, *atualizar*, e *instalar* são utilizados para descrever três separado conceitos.

## <a name="upgrade"></a>Atualização
*Atualize* ou *atualização in-loco*, é utilizado ao converter o site do Configuration Manager 2012 ou a hierarquia de forma que executa o System Center Configuration Manager.
Ao atualizar o System Center 2012 Configuration Manager para o System Center Configuration Manager, continua a utilizar os mesmos servidores para alojar os seus sites e servidores de site, e mantém seus dados existentes e as configurações do Configuration Manager.  Isso é diferente da [migração](/sccm/core/migration/migrate-data-between-hierarchies) que é uma forma de manter os dados sobre os dispositivos geridos e configurações durante a utilização de novos sites do System Center Configuration Manager instalados para novo hardware.

Para obter mais detalhes, consulte [atualizar para o System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).



## <a name="update"></a>Atualizar
*Atualização* é utilizada para instalar atualizações na consola do System Center Configuration Manager e para atualizações fora de banda que são as atualizações que não não possível entregar a partir da consola do Configuration Manager. Atualizações na consola podem modificar a versão do seu site do ramo atual (ou sites Technical Preview) de modo a que execute uma versão superior. Por exemplo, se seu site executa a versão 1606, pode instalar uma atualização para a versão 1610. As atualizações também podem instalar as correções para um problema conhecido, sem modificar a versão de sites.      

Normalmente, as atualizações de adicionar correções de segurança, melhoria de qualidade e novas funcionalidades à sua implementação existente. Se usar o ramo de pré-visualização técnica, uma atualização pode instalar uma versão mais recente do Technical Preview.
-   Pode escolher quando instalar a atualização na consola, começando no site de nível superior da sua hierarquia.
- Pode instalar qualquer atualização que está disponível a partir da consola. Por exemplo, se seu site executa a versão 1602 e são oferecidas 1606 e 1610, deve considerar a instalar a versão 1610, porque cada versão inclui as funcionalidades que foram primeiros disponibilizada em versões anteriores.
- Após uma nova atualização concluir a instalação no seu site de nível superior, os sites primários subordinados iniciam automaticamente o processo para atualizar. No entanto, pode definir [serviço Windows](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkservicewindowa-service-windows-for-site-servers) para controlar a temporização das atualizações.
- Os sites secundários não instalam automaticamente as atualizações. Em vez disso, iniciar manualmente a atualização a partir da consola do Configuration Manager.

Para obter mais informações, consulte [atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates), e [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).



## <a name="install"></a>Instalar
*Instalar* é utilizado quando criar uma nova hierarquia do Configuration Manager a partir do zero, ou adicionar sites adicionais para uma hierarquia existente.  

Quando instala um novo site primário ou site de administração central, a localização do setup.exe e os respetivos ficheiros de origem relacionados que utilizar depende do seu cenário de instalação.

Para obter mais informações, consulte [preparar a instalação de sites](/sccm/core/servers/deploy/install/prepare-to-install-sites).

---
title: Detetar recursos de dispositivo e utilizador
titleSuffix: Configuration Manager
description: "Ler uma descrição geral da deteção de registos de dados de deteção e o processo."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
caps.latest.revision: "20"
caps.handback.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: b380df38c4e08a04691a0bca9d46580fedf7b78a
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="run-discovery-for-system-center-configuration-manager"></a>Executar a deteção no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize um ou mais métodos de deteção no System Center Configuration Manager para localizar os recursos de dispositivo e utilizador que pode gerir. Também pode utilizar a deteção para identificar a infraestrutura de rede no seu ambiente. Existem vários métodos diferentes que pode utilizar para detetar diversos elementos, e cada método tem as suas próprias configurações e limitações.  

## <a name="overview-of-discovery"></a>Descrição geral do processo de deteção  
 A deteção é o processo pelo qual o Configuration Manager aprende as coisas que pode gerir. Seguem-se os métodos de deteção disponíveis:  

-   Deteção de Florestas do Active Directory  

-   Deteção de Grupos do Active Directory  

-   Deteção de Sistemas do Active Directory  

-   Deteção de Utilizadores do Active Directory  

-   Deteção de Heartbeat  

-   Deteção de Redes  

-   Deteção de Servidores  

> [!TIP]  
>  Pode saber mais sobre os métodos de deteção individuais em [Acerca dos métodos de deteção para o System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  
>   
>  Para obter assistência selecionar métodos a utilizar e, em que sites na hierarquia, consulte [selecionar métodos de deteção a utilizar para o System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md).  

 Para utilizar a maioria dos métodos de deteção, tem de ativar o método num site e defina-o até de rede pesquisa ou localizações do Active Directory. Quando é executado, consulta a localização especificada para obter informações sobre dispositivos ou utilizadores que o Configuration Manager pode gerir. Quando um método de deteção localiza com êxito informações sobre um recurso, coloca essas informações para um ficheiro denominado registo de dados de deteção (DDR). Se o ficheiro é processado por um site de administração central ou primário. O processamento de um DDR cria um novo registo na base de dados do site para os recursos detetados recentemente ou atualiza os registos existentes com as novas informações.  

 Alguns métodos de deteção podem gerar um grande volume de tráfego de rede e o DDR produzem pode resultar de uma utilização intensiva de recursos da CPU durante o processamento. Por conseguinte, planeie utilizar apenas os métodos de deteção necessários para atingir os seus objetivos. Pode utilizar apenas um ou dois métodos de deteção e, posteriormente, ativar métodos adicionais de forma controlada para expandir o nível de deteção no ambiente.  

 Depois das informações de deteção são adicionadas à base de dados do site, as informações de, em seguida, replicam a cada site na hierarquia, independentemente de onde foram detetado ou processado. Por conseguinte, enquanto que pode configurar diferentes agendamentos e definições para métodos de Deteção em diferentes sites, poderá executar um método de deteção específico apenas num único site. Isto reduz a utilização de largura de banda de rede através de ações de deteção duplicadas e reduz o processamento de dados de deteção redundantes em vários sites.  

 Pode utilizar dados de deteção para criar coleções personalizadas e consultas que agrupem logicamente os recursos para tarefas de gestão. Por exemplo:  

-   Emitir instalações de cliente ou atualizar.  

-   Implementação de conteúdo para utilizadores ou dispositivos.  

-   Implementar definições de cliente e configurações relacionadas.

##  <a name="BKMK_DDRs"></a>Sobre os registos de dados de deteção  
 DDR são ficheiros criados por um método de deteção. Contêm informações sobre um recurso pode gerir no Configuration Manager, tais como computadores, utilizadores e em alguns casos, a infraestrutura de rede. São processados em sites primários ou em sites de administração central. Depois das informações de recursos do DDR são introduzidas na base de dados, este é eliminado e as informações são replicadas como dados globais para todos os sites na hierarquia.  

 O site onde um DDR é processado depende das informações que contém:  

-   DDR de recursos detetados recentemente que não na base de dados são processados no site de nível superior da hierarquia. Site de nível superior cria um novo registo de recurso na base de dados e atribui-um identificador exclusivo. Os DDR são transferidos através da replicação baseada em ficheiros até atingirem o site de nível superior.  

-   Os DDR de objetos detetados anteriormente são processados em sites primários. Os sites primários subordinados não transferem DDRs para o site de administração central quando o DDR contém informações sobre um recurso que já se encontra na base de dados.  

-   Os sites secundários não processam DDR e sempre transferi-los através da replicação baseada em ficheiros para o respetivo site primário principal.  

Os ficheiros DDR são identificados pela extensão .ddr e têm um tamanho típico de cerca de 1 KB.  

## <a name="get-started-with-discovery"></a>Introdução ao processo de deteção:  
 Antes de utilizar a consola do Configuration Manager para configurar a deteção, deve compreender as diferenças entre os métodos, o que pode fazer e para algumas pessoas, as limitações.  

Os tópicos seguintes podem criar uma base que irão ajudar a utilizar métodos de deteção com êxito:  

-   [Acerca dos métodos de deteção para o System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Selecionar os métodos de deteção a utilizar para o System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Em seguida, quando compreender os métodos que pretende utilizar, encontrar orientações para configurar cada método [configurar métodos de deteção para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

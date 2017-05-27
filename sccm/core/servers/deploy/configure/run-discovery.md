---
title: Detetar recursos de dispositivo e utilizador | Documentos do Microsoft
description: "Ler uma descrição geral da deteção de processo e deteção de registos de dados."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
caps.latest.revision: 20
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 7b6674f331c82cc7899b8661cf38b9d3022cf21b
ms.openlocfilehash: 647826e9d340d3ef97abab0dba51041a3727dedc
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="run-discovery-for-system-center-configuration-manager"></a>Executar a deteção no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize um ou mais métodos de deteção no System Center Configuration Manager para localizar recursos de dispositivo e utilizador que pode gerir. Também pode utilizar a deteção para identificar a infraestrutura de rede no seu ambiente. Existem vários métodos diferentes que pode utilizar para detetar diferentes aspetos e cada método tem as suas próprias configurações e as limitações.  

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
>  Para obter assistência na seleção os métodos da utilizar e para as quais os sites da hierarquia, consulte o artigo [selecione métodos de deteção a utilizar para o System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md).  

 Para utilizar a maioria dos métodos de deteção, tem de ativar o método num site e defina-o até rede específica de pesquisa ou localizações do Active Directory. Quando este é executado, consulta na localização especificada para obter informações sobre dispositivos ou utilizadores que pode gerir o Configuration Manager. Quando um método de deteção localiza com êxito informações sobre um recurso, coloca essas informações num ficheiro denominado um registo de dados de deteção (DDR). Esse ficheiro, em seguida, é processado por um site primário ou de administração central. O processamento de um DDR cria um novo registo na base de dados do site para os recursos detetados recentemente ou atualiza os registos existentes com as novas informações.  

 Alguns métodos de deteção podem gerar um grande volume de tráfego de rede e o DDR produzem pode resultar numa utilização intensiva de recursos da CPU durante o processamento. Por conseguinte, planeie utilizar apenas os métodos de deteção necessários para atingir os seus objetivos. Pode utilizar apenas um ou dois métodos de deteção e, posteriormente, ativar métodos adicionais de forma controlada para expandir o nível de deteção no ambiente.  

 Depois de informações de deteção são adicionadas à base de dados do site, em seguida, as informações são replicadas para cada site na hierarquia, independentemente de onde foram detetado ou processado. Por conseguinte, enquanto que pode configurar definições para métodos de deteção e agendas diferentes em diferentes sites, poderá executar um método de deteção específicas apenas um único site. Isto reduz a utilização de largura de banda de rede através de ações de deteção duplicados e reduz o processamento de dados de deteção redundantes em vários sites.  

 Pode utilizar dados de deteção para criar coleções personalizadas e consultas que agrupem os recursos para tarefas de gestão. Por exemplo:  

-   Efetuar instalações push instalações de cliente ou atualizar.  

-   Implementação de conteúdos para utilizadores ou dispositivos.  

-   Implementar definições de cliente e configurações relacionadas.

##  <a name="BKMK_DDRs"></a>Acerca de registos de dados de deteção  
 DDR são ficheiros criados por um método de deteção. Contêm também informações sobre um recurso pode gerir no Configuration Manager, tais como computadores, utilizadores e em alguns casos, a infraestrutura de rede. São processados em sites primários ou em sites de administração central. Depois das informações de recursos do DDR são introduzidas na base de dados, este é eliminado e as informações são replicadas como dados globais para todos os sites na hierarquia.  

 O site onde um DDR é processado depende das informações que contém:  

-   Os DDRs de recursos detetados recentemente que não estão na base de dados são processados no site de nível superior da hierarquia. Site de nível superior cria um novo registo de recurso na base de dados e atribui-lhe um identificador exclusivo. Os DDR são transferidos através da replicação baseada em ficheiros até atingirem o site de nível superior.  

-   Os DDR de objetos detetados anteriormente são processados em sites primários. Os sites primários subordinados não transferem DDRs para o site de administração central quando o DDR contém informações sobre um recurso que já se encontra na base de dados.  

-   Os sites secundários não processar os DDR e transfere-os sempre pela replicação baseada em ficheiros para o respetivo site primário principal.  

Os ficheiros DDR são identificados pela extensão .ddr e têm um tamanho típico de cerca de 1 KB.  

## <a name="get-started-with-discovery"></a>Introdução ao processo de deteção:  
 Antes de utilizar a consola do Configuration Manager para configurar a deteção, deve compreender as diferenças entre os métodos, o que podem fazer e para algumas pessoas, as limitações.  

Os tópicos seguintes podem construir uma Fundação que irão ajudar a utilizar métodos de deteção com êxito:  

-   [Sobre os métodos de deteção para o System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Selecione os métodos de deteção a utilizar para o System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Em seguida, quando compreender os métodos que pretende utilizar, encontrar orientações para configurar cada método no [configurar métodos de deteção para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  


---
title: Detetar recursos de dispositivo e utilizador
titleSuffix: Configuration Manager
description: Leia uma visão geral da deteção de registos de dados de deteção e de processo.
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49ef4e9047d132904ea3b78078ad1894bcd001ac
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132038"
---
# <a name="run-discovery-for-system-center-configuration-manager"></a>Executar a deteção no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize um ou mais métodos de deteção no System Center Configuration Manager para localizar os recursos de dispositivo e utilizador que pode gerir. Também pode utilizar a deteção para identificar a infraestrutura de rede no seu ambiente. Existem vários métodos diferentes, que pode utilizar para detetar diversos elementos, e cada método tem suas próprias configurações e limitações.  

## <a name="overview-of-discovery"></a>Descrição geral do processo de deteção  
 A deteção é o processo pelo qual o Configuration Manager aprende sobre coisas que pode gerir. Seguem-se os métodos de deteção disponíveis:  

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
>  Para obter assistência na seleção dos métodos a utilizar e, em que sites na hierarquia, consulte [selecionar métodos de deteção a utilizar para o System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md).  

 Para utilizar a maioria dos métodos de deteção, tem de ativar o método num site e configurá-lo para a rede específica de pesquisa ou localizações do Active Directory. Quando é executado, ele consulta a localização especificada para obter informações sobre dispositivos ou utilizadores que gerem o Configuration Manager. Quando um método de deteção localiza com êxito informações sobre um recurso, ele coloca essas informações num ficheiro denominado registo de dados de deteção (DDR). Esse ficheiro é processado por um site de administração central ou primário. O processamento de um DDR cria um novo registo na base de dados do site para os recursos detetados recentemente ou atualiza os registos existentes com as novas informações.  

 Alguns métodos de deteção podem gerar um grande volume de tráfego de rede e o DDR produzem pode resultar numa utilização de recursos da CPU durante o processamento. Por conseguinte, planeie utilizar apenas os métodos de deteção necessários para atingir os seus objetivos. Pode utilizar apenas um ou dois métodos de deteção e, posteriormente, ativar métodos adicionais de forma controlada para expandir o nível de deteção no ambiente.  

 Depois de informações de deteção são adicionadas à base de dados do site, as informações, em seguida, replica para cada site na hierarquia, independentemente de onde foram detetada ou processada. Desta forma, apesar de poder configurar diferentes agendamentos e definições para métodos de Deteção em sites diferentes, pode executar um método de deteção específico apenas num único site. Isso reduz a utilização de largura de banda de rede por meio de ações da deteção de duplicados e reduz o processamento de dados de deteção redundantes em vários sites.  

 Pode utilizar dados de deteção para criar coleções personalizadas e consultas que agrupem logicamente os recursos para tarefas de gestão. Por exemplo:  

-   Emitir instalações de cliente ou atualizar.  

-   Implementar o conteúdo para utilizadores ou dispositivos.  

-   Implementar definições de cliente e configurações relacionadas.

##  <a name="BKMK_DDRs"></a> Sobre os registos de dados de deteção  
 DDR são ficheiros criados por um método de deteção. Eles contêm informações sobre um recurso que pode gerir no Configuration Manager, tais como computadores, utilizadores e em alguns casos, a infraestrutura de rede. São processados em sites primários ou em sites de administração central. Depois das informações de recurso DDR são introduzidas na base de dados, o DDR é eliminado e as informações são replicadas como dados globais para todos os sites na hierarquia.  

 O site onde um DDR é processado depende das informações que contém:  

-   Os DDR de recursos detetados recentemente que não são na base de dados são processados no site de nível superior da hierarquia. Site de nível superior cria um novo registo de recurso na base de dados e atribui-lhe um identificador exclusivo. DDR são transferidos através da replicação baseada em ficheiros até atingirem o site de nível superior.  

-   Os DDR de objetos detetados anteriormente são processados em sites primários. Os sites primários subordinados não transferem DDRs para o site de administração central quando o DDR contém informações sobre um recurso que já se encontra na base de dados.  

-   Sites secundários não processam DDR e sempre transferi-las através da replicação baseada em ficheiros para o respetivo site primário principal.  

Os ficheiros DDR são identificados pela extensão .ddr e têm um tamanho típico de cerca de 1 KB.  

## <a name="get-started-with-discovery"></a>Introdução ao processo de deteção:  
 Antes de utilizar a consola do Configuration Manager para configurar a deteção, deve compreender as diferenças entre os métodos, o que pode fazer e para alguns, as suas limitações.  

Os tópicos seguintes podem servir de base que irão ajudá-lo a utilizar os métodos de deteção com êxito:  

-   [Sobre métodos de deteção para o System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Selecione os métodos de deteção a utilizar para o System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Em seguida, quando compreender os métodos que pretende utilizar, procure orientações para configurar cada método na [configurar métodos de deteção para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

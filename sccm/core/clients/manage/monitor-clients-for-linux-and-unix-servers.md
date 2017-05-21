---
title: Monitorizar clientes Linux/UNIX - Configuration Manager | Documentos do Microsoft
description: Monitorizar clientes em servidores Linux e UNIX no System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: d6478fa75c27e07e22702f3f8d5577df73ebdd48
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Como monitorizar clientes para servidores Linux e UNIX no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode ver informações de servidores Linux e UNIX na consola do System Center Configuration Manager utilizando os mesmos métodos que utiliza para ver informações de clientes baseados em Windows.  

 As informações que pode ver incluem:  

-   Detalhes do estado dos clientes, os dashboards de consola do Configuration Manager  

-   Detalhes sobre clientes nos relatórios do Configuration Manager predefinido  

-   Detalhes de inventário no Explorador de Recursos  

 As secções seguintes descrevem hoe para obter estas informações a partir do Explorador de recursos e relatórios.  

##  <a name="BKMK_UseResourceExpforLnU"></a>Utilize o Explorador de recursos para ver o inventário para servidores Linux e UNIX  

 Após um cliente do Configuration Manager submete o inventário de hardware para o site do Configuration Manager, pode utilizar o Explorador de recursos para ver estas informações. O cliente do Configuration Manager para Linux e UNIX não adiciona novas classes ou vistas para o inventário para o Explorador de recursos. Os dados de inventário de Linux e UNIX são mapeados para as classes WMI existentes. Pode ver os detalhes de inventário para os seus servidores Linux e UNIX nas classificações baseadas no Windows utilizando o Explorador de Recursos.  

 Por exemplo, é possível recolher a lista de todos os programas instalados nativamente encontrados nos seus servidores Linux e UNIX. Exemplos de programas instalados nativamente incluem **.rpms** no Linux ou **.pkgs** no Solaris. Depois do inventário foi submetido por um cliente de Linux ou UNIX, pode ver a lista de todos os os nativamente Linux ou UNIX programas instalados no Explorador de recursos na consola do Configuration Manager.  

 Para obter informações sobre como utilizar o Explorador de recursos, consulte o artigo [como utilizar o Explorador de recursos para ver o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="BKMK_UseReportsforLnU"></a> Como utilizar Relatórios para Ver Informações de Servidores Linux e UNIX  
 Os relatórios do Configuration Manager incluem informações a partir de servidores Linux e UNIX, juntamente com informações a partir de computadores baseados em Windows. Não são necessárias configurações adicionais para integrar os dados de Linux e UNIX nos relatórios.  

 Por exemplo, se executar o relatório chamado Contagem de Versões de Sistemas Operativos, este apresenta a lista dos diferentes sistemas operativos e o número de clientes que estão a executar cada sistema operativo. O relatório está baseado nas informações de inventário de hardware foi enviadas pelo diferentes clientes do Configuration Manager que são executados nos sistemas operativos diferentes.  

 Também é possível criar relatórios personalizados específicos de dados de servidores Linux e UNIX. A propriedade **Legenda** da classe de inventário de hardware **Sistema Operativo** é um atributo útil que poderá utilizar para identificar Sistemas Operativos específicos na consulta do relatório.  

 Para obter informações sobre os relatórios no Configuration Manager, consulte o artigo [Reporting no System Center Configuration Manager](../../../core/servers/manage/reporting.md).  


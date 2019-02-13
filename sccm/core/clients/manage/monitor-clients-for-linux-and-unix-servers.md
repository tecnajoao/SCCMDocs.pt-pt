---
title: 'Monitorizar clientes do Linux/UNIX '
titleSuffix: Configuration Manager
description: Monitorizar clientes em servidores Linux e UNIX no System Center Configuration Manager.
ms.date: 08/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5e8e10b4297e1367f6835e61ced77f2a1154319b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127937"
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Como monitorizar clientes para servidores Linux e UNIX no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode ver informações dos servidores Linux e UNIX na consola do System Center Configuration Manager utilizando os mesmos métodos que utiliza para ver informações de clientes baseados em Windows.  

 As informações que pode ver incluem:  

- Detalhes do Estado de clientes, nos dashboards de consola do Configuration Manager  

- Detalhes sobre clientes nos relatórios do Configuration Manager predefinido  

- Detalhes de inventário no Explorador de Recursos  

  As secções seguintes descrevem como obter estes detalhes do Explorador de recursos e os relatórios.  

##  <a name="BKMK_UseResourceExpforLnU"></a> Utilizar o Explorador de recursos para ver o inventário para servidores Linux e UNIX  

 Depois de um cliente do Configuration Manager envia o inventário de hardware para o site do Configuration Manager, pode utilizar o Explorador de recursos para ver estas informações. O cliente do Configuration Manager para Linux e UNIX não adiciona novas classes ou vistas de inventário para o Explorador de recursos. Os dados de inventário de Linux e UNIX são mapeados para as classes WMI existentes. Pode ver os detalhes de inventário para os seus servidores Linux e UNIX nas classificações baseadas no Windows utilizando o Explorador de Recursos.  

 Por exemplo, é possível recolher a lista de todos os programas instalados nativamente encontrados nos seus servidores Linux e UNIX. Exemplos de programas instalados nativamente incluem **.rpms** no Linux ou **.pkgs** no Solaris. Depois do inventário ter sido submetido por um cliente Linux ou UNIX, pode ver a lista de todos os programas instalados nativamente Linux ou UNIX no Explorador de recursos na consola do Configuration Manager.  

 Para obter informações sobre como utilizar o Explorador de recursos, consulte [como utilizar o Explorador de recursos para ver o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="BKMK_UseReportsforLnU"></a> Como utilizar Relatórios para Ver Informações de Servidores Linux e UNIX  
 Os relatórios do Configuration Manager incluem informações de servidores Linux e UNIX, juntamente com informações de computadores baseados em Windows. Não são necessárias configurações adicionais para integrar os dados de Linux e UNIX nos relatórios.  

 Por exemplo, se executar o relatório chamado Contagem de Versões de Sistemas Operativos, este apresenta a lista dos diferentes sistemas operativos e o número de clientes que estão a executar cada sistema operativo. O relatório baseia-se as informações de inventário de hardware que foram enviadas pelos diferentes clientes do Configuration Manager que são executados em diferentes sistemas operativos.  

 Também é possível criar relatórios personalizados específicos de dados de servidores Linux e UNIX. A propriedade **Legenda** da classe de inventário de hardware **Sistema Operativo** é um atributo útil que poderá utilizar para identificar Sistemas Operativos específicos na consulta do relatório.  

 Para obter informações sobre os relatórios no Configuration Manager, consulte [relatórios no System Center Configuration Manager](../../../core/servers/manage/reporting.md).  

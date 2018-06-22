---
title: Pré-requisitos de coleções
titleSuffix: Configuration Manager
description: Obter os pré-requisitos para utilizar coleções no System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 12cbffb63ce449afedb9159174409fb5b1f7583f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32343790"
---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>Pré-requisitos para coleções no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Coleções no System Center Configuration Manager contém apenas as dependências no produto.  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Ponto do Reporting Services|A função do sistema de sites do ponto do Reporting Services deve ser instalada para que possa executar relatórios para coleções. Para obter mais informações, veja [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Devem ter sido concedidas permissões de segurança específicas para gerir coleções|Deve ter as seguintes permissões de segurança para gerir definições de conformidade:<br /><br /> -Para criar e gerir coleções: **Criar**, **eliminar**, **modificar**, **modificar pasta**, **mover objeto**, **leitura** e **Ler recurso** para o **coleção** objeto.<br /><br /> -Para gerir as definições da coleção: **Modificar a definição de coleção** para o **coleção** objeto.<br /><br /> A permissão **Modificar Pasta** é necessária para todas as pastas de coleção, incluindo a pasta de raiz.|  

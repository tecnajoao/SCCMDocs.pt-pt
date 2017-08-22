---
title: "Pré-requisitos de coleções | Microsoft Docs"
description: "Obter os pré-requisitos para utilizar coleções no System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
caps.latest.revision: "7"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 41fc3eb20a7441939eb0dc80bc121c8f3ea322b2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>Pré-requisitos para coleções no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Coleções no System Center Configuration Manager contém apenas as dependências no produto.  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Ponto do Reporting Services|A função do sistema de sites do ponto do Reporting Services deve ser instalada para que possa executar relatórios para coleções. Para obter mais informações, veja [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Devem ter sido concedidas permissões de segurança específicas para gerir coleções|Deve ter as seguintes permissões de segurança para gerir definições de conformidade:<br /><br /> -Para criar e gerir coleções: **Criar**, **eliminar**, **modificar**, **modificar pasta**, **mover objeto**, **leitura** e **ler recurso** para o **coleção** objeto.<br /><br /> -Para gerir as definições da coleção: **Modificar a definição de coleção** para o **coleção** objeto.<br /><br /> A permissão **Modificar Pasta** é necessária para todas as pastas de coleção, incluindo a pasta de raiz.|  

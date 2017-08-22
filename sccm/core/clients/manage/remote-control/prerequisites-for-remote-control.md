---
title: "Pré-requisitos de controlo remoto | Microsoft Docs"
description: "Obter os pré-requisitos para controlo remoto no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 12c602ddfa237768af497324440091e17e597ae9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-remote-control-in-system-center-configuration-manager"></a>Pré-requisitos para controlo remoto no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Controlo remoto no System Center Configuration Manager tem dependências externas e dependências no produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Controlador de placa de vídeo do computador|Certifique-se de que tem instalado o controlador de vídeo mais atualizado nos computadores cliente para assegurar um excelente desempenho do controlo remoto.|  

 Os dispositivos que executam o Windows Embedded, Windows Embedded para o Ponto de Serviço (POS) e o Windows Fundamentals para Computadores Legados não são compatíveis com o visualizador de controlo remoto, mas suportam o cliente de controlo remoto.  

 Controlo remoto do Configuration Manager não pode ser utilizado para administrar remotamente computadores cliente que executam o Systems Management Server 2003 ou do Configuration Manager 2007.  

> [!NOTE]  
>  Não são necessários serviços do Windows como dependência externa para o controlo remoto.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Sistemas operativos suportados para o visualizador de controlo remoto  
O Visualizador de controlo remoto é suportado em todos os sistemas operativos que são suportados para a consola do Configuration Manager. Para informações, consulte [configurações suportadas para consolas do System Center Configuration Manager](../../../../core/plan-design/configs/supported-operating-systems-consoles.md).   

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|O controlo remoto deve estar ativado para os clientes|Por predefinição, o controlo remoto não está ativado quando instalar o Configuration Manager. Para obter informações sobre como ativar e configurar o controlo remoto, consulte [configurar o controlo remoto no System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Ponto do Reporting Services|A função do sistema de sites do ponto do Reporting Services deve ser instalada para que possa executar relatórios para controlo remoto. Para obter mais informações, veja [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Permissões de segurança para gerir o controlo remoto|Para aceder a recursos da coleção e para iniciar uma sessão de controlo remoto a partir da consola do Configuration Manager: **Leitura**, **ler recurso**, e **controlo remoto** permissão para o **coleção** objeto.<br /><br /> O **operador de ferramentas remotas** função de segurança inclui estas permissões que são necessárias para gerir o controlo remoto no Configuration Manager.<br /><br /> Para obter mais informações, consulte [configurar a administração baseada em funções para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Além disso, devem ser dada visualizadores permissão para utilizar o controlo remoto ao adicionar estes utilizadores para o **permitido visualizadores de controlo remoto e assistência remota** lista o **ferramentas remotas** as definições de cliente.

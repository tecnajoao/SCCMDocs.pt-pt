---
title: "Pré-requisitos de controlo remoto | Documentos do Microsoft"
description: "Obter os pré-requisitos para controlo remoto no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: e08bca886dfc0730ab45ab899754394ae61335e3
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="prerequisites-for-remote-control-in-system-center-configuration-manager"></a>Pré-requisitos para controlo remoto no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Controlo remoto no System Center Configuration Manager tem dependências externas e dependências no produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Controlador de placa de vídeo do computador|Certifique-se de que tem instalado o controlador de vídeo mais atualizado nos computadores cliente para assegurar um excelente desempenho do controlo remoto.|  

 Os dispositivos que executam o Windows Embedded, Windows Embedded para o Ponto de Serviço (POS) e o Windows Fundamentals para Computadores Legados não são compatíveis com o visualizador de controlo remoto, mas suportam o cliente de controlo remoto.  

 Controlo remoto do Configuration Manager não pode ser utilizado para administrar remotamente computadores cliente com sistemas de gestão Server 2003 ou do Configuration Manager 2007.  

> [!NOTE]  
>  Não são necessários serviços do Windows como dependência externa para o controlo remoto.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Sistemas operativos suportados para o visualizador de controlo remoto  
 A tabela seguinte fornece informações sobre os sistemas operativos suportados para o visualizador de controlo remoto: Para obter informações sobre sistemas operativos cliente suportados, consulte o artigo [configurações suportadas para o System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md).  

|Sistema operativo|Suporte do Visualizador|Mais informações|  
|----------------------|--------------------|----------------------|  
|Windows XP (32 bits)|Sim|Para executar o Visualizador de controlo remoto neste sistema operativo, primeiro tem de transferir e instalar o [7.0 (KB969084) de atualização do cliente de ligação de ambiente de trabalho remoto (RDC)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) a partir de Center Download Microsoft.|  
|Windows XP (64 bits)|Não|Não existem informações adicionais.|  
|Windows Vista (32 bits)|Sim|Para executar o Visualizador de controlo remoto neste sistema operativo, primeiro tem de transferir e instalar o [7.0 (KB969084) de atualização do cliente de ligação de ambiente de trabalho remoto (RDC)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) a partir de Center Download Microsoft.|  
|Windows Vista (64 bits)|Sim|Para executar o Visualizador de controlo remoto neste sistema operativo, primeiro tem de transferir e instalar o [7.0 (KB969084) de atualização do cliente de ligação de ambiente de trabalho remoto (RDC)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) a partir de Center Download Microsoft.|  
|Windows 7 (32-bit)|Sim|Não existem informações adicionais.|  
|Windows 7 (64 bits)|Sim|Não existem informações adicionais.|  
|Windows Server 2003 (32 bits)|Não|Não existem informações adicionais.|  
|Windows Server 2003 (64 bits)|Não|Não existem informações adicionais.|  
|Windows Server 2008 (32 bits)|Não|Não existem informações adicionais.|  
|Windows Server 2008 (64 bits)|Não|Não existem informações adicionais.|  
|Windows Server 2008 R2 (64 bits)|Sim|Não existem informações adicionais.|  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|O controlo remoto deve estar ativado para os clientes|Por predefinição, o controlo remoto não está ativado quando instalar o Configuration Manager. Para obter informações sobre como ativar e configurar o controlo remoto, consulte o artigo [configurar o controlo remoto no System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Ponto do Reporting Services|A função do sistema de sites do ponto do Reporting Services deve ser instalada para que possa executar relatórios para controlo remoto. Para obter mais informações, veja [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Permissões de segurança para gerir o controlo remoto|Para aceder a recursos de coleção e iniciar uma sessão de controlo remoto a partir da consola do Configuration Manager: **Controlar AMT**, **leitura**, **ler recurso**, e **controlo remoto** permissão para o **coleção** objeto.<br /><br /> O **operador de ferramentas remotas** função de segurança inclui as permissões que são necessárias para gerir o controlo remoto no Configuration Manager.<br /><br /> Para obter mais informações, consulte o artigo [configurar a administração baseada em funções para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Além disso, deve adicionar utilizadores aos quais pretende conceder permissão para utilizar o controlo remoto e assistência remota à lista de vistas permitidas de controlo remoto utilizando a opção **Visualizadores autorizados do Controlo Remoto e da Assistência Remota** nas definições de cliente **Ferramentas Remotas** .|  


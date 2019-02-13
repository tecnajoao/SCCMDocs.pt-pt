---
title: Serviço Windows
titleSuffix: Configuration Manager
description: Utilize as janelas de serviço para controlar quando os sites do System Center Configuration Manager instalam as atualizações.
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 495d109d73a32617f58383b78d11a10bf05edf75
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134542"
---
#  <a name="service-windows-for-site-servers"></a>Janelas de manutenção para servidores do site

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode configurar janelas de manutenção em sites de administração central e sites primários para controlar quando podem instalar atualizações na consola.  Pode configurar várias janelas, com a janela de permissão para instalar as atualizações que está a ser determinadas por uma combinação de todas as janelas de serviço para esse servidor do site.

Quando não estiver configurada nenhuma janela de serviço:
- **No seu site de nível superior** (um site de administração central ou site primário autónomo) que escolher quando iniciar a instalação da atualização.
- **Num site primário subordinado**, a atualização é instalada automaticamente após a atualização de concluir a instalação no site de administração central.
- **Num site secundário**, nunca de início das atualizações automaticamente. Em vez disso, tem de iniciar manualmente a instalação da atualização da consola, depois do site primário principal tem instalada a atualização.

Quando uma janela de serviço está configurada:
- **No seu site de nível superior**, não será capaz de iniciar a instalação de qualquer nova atualização a partir da consola do Configuration Manager. Mesmo com uma janela de serviço configurada, o site transfere automaticamente as atualizações para que eles estão prontos para instalar.  
- **Num site primário subordinado**, as atualizações que têm instalado num site de administração central irão transferir para o site primário, mas não automaticamente início. Não é possível iniciar manualmente a instalação de uma atualização durante um período de tempo bloqueado pelo uso de uma janela de serviço. Cada vez quando já não é o bloco de períodos de administração da instalação da atualização, a instalação da atualização automaticamente é iniciado.
- **Os sites secundários** não suportam janelas de serviço e não instalar atualizações automaticamente. Depois do site primário principal de um site secundário instala uma atualização, pode começar a atualização do site secundário a partir da consola.

## <a name="to-configure-a-service-window"></a>Para configurar uma janela de serviço

1.  Na consola do Configuration Manager open **Administration** > **configuração do Site** > **Sites**e, em seguida, selecione o servidor de site em que pretende configurar uma janela de serviço.  

2.  Em seguida, edite as **Propriedades** dos servidores do site e selecione o separador **Período de Administração** , onde pode configurar um ou mais períodos de administração para esse servidor do site.  

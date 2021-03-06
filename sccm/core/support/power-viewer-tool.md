---
title: Ferramenta de Visualizador de Energia
titleSuffix: Configuration Manager
description: Utilize a ferramenta de Visualizador de energia para ver o estado da funcionalidade de gestão de energia num cliente do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5f9695decaf7af8d947d57443bd4b14032545b7d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133321"
---
# <a name="power-viewer-tool"></a>Ferramenta de Visualizador de Energia

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A ferramenta de Visualizador de energia é um da [ferramentas do Configuration Manager](/sccm/core/support/tools). Utilize-o para ver o estado da funcionalidade de gestão de energia num cliente do Configuration Manager.

Execute **PowerVwr.exe** como administrador. Quando a ferramenta é iniciado, ele apresenta as capacidades de energia e as definições de energia do computador local do **Power Config** separador. 

Para ver os dados de gestão de energia de um computador remoto:  

1. Vá para o **arquivo** menu e clique em **Connect**. 

2. Introduza o **computador** nome e um **nome de utilizador** e **palavra-passe**, se necessário. 

Existem três separadores no Visualizador de energia:  

- **Configuração de energia**: Ver as capacidades de energia e as definições do computador de destino de energia.  

- **Atividade diária**: Ver os gráficos de atividade diária do cliente, que inclui as seguintes informações:  

    - **Computador em**: O estado de energia do computador num dia. Modo de suspensão é considerado como poder desativar.  

    - **Monitorizar no**: Ou desativar o estado do monitor num dia.  

    - **Utilizador ativo**: Informações de atividade do usuário num dia.  

- **Eventos de energia**: Ver todos os eventos de energia diário. O cliente resume esses eventos em 12:00 AM. Este resumo gera dados para o gráfico de atividade diária.  

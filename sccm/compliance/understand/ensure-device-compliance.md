---
title: Assegurar a conformidade do dispositivo
titleSuffix: Configuration Manager
description: Gerir a configuração e a conformidade dos dispositivos na sua organização ao utilizar o System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 7568c9aa-b99e-4466-bfc8-0301aa376930
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2ac27cfd7bccc55da891707878fccd8829c43d93
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125945"
---
# <a name="ensure-device-compliance-with-system-center-configuration-manager"></a>Garantir a compatibilidade do dispositivo com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Definições de compatibilidade no System Center Configuration Manager dá-lhe as ferramentas e os recursos necessários para gerir a configuração e a conformidade dos dispositivos na sua organização. Isto ajuda-o a suportar os seguintes requisitos comerciais:  

-   Comparar a configuração de PCs com o Windows, computadores Macs, servidores e dispositivos móveis que gere com as configurações de melhores práticas que cria ou obtém de outros fornecedores  

-   Identificar configurações de dispositivos não autorizados  

-   Reportar a conformidade com as políticas de regulamentação e políticas de segurança internas  

-   Identificar vulnerabilidades de segurança  

-   Fornecer o suporte técnico com as informações para detetar as causas prováveis de incidentes e problemas comunicados, ao identificar as configurações não compatíveis  

-   Remediar automaticamente algumas definições não conformes em dispositivos móveis  

-   Remediar a incompatibilidade ao implementar aplicações, pacotes e programas ou scripts numa coleção que é preenchido automaticamente com dispositivos que reportam a que estão em conformidade  


## <a name="get-started"></a>Introdução  
 Aprenda as noções básicas sobre definições de compatibilidade e as tarefas que poderá realizar com as mesmas.  

 [Introdução às definições de compatibilidade](../../compliance/get-started/get-started-with-compliance-settings.md)  

## <a name="plan-and-design"></a>Planear e estruturar  
 Antes de começar a trabalhar com as definições de compatibilidade, certifique-se de que implementou os pré-requisitos necessários que encontrará neste tópico.  

 [Planear e configurar as definições de compatibilidade](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

## <a name="common-tasks"></a>Tarefas comuns  
 Nesta secção, irá encontrar alguns cenários comuns que o ajudará a aprender a utilizar as definições de compatibilidade no Configuration Manager.  

 [Tarefas comuns para gerir a compatibilidade](../../compliance/plan-design/common-tasks-for-managing-compliance.md)  

## <a name="remote-connection-profiles"></a>Perfis de ligação remota  
 Este tipo de item de configuração permite-lhe configurar PCs dos utilizadores liguem remotamente a computadores de trabalho quando não estiverem ligados ao domínio ou se os seus computadores pessoais estiverem ligados através da Internet.  

 [Criar perfis de ligação remota](/sccm/compliance/deploy-use/create-remote-connection-profiles)  

## <a name="user-data-and-profiles"></a>Dados e perfis de utilizador  
 Este tipo de item de configuração contém definições que gerem o redirecionamento de pastas, ficheiros offline e perfis itinerantes em computadores que executam o Windows 8 e posterior para utilizadores na sua hierarquia.  

 [Criar itens de configuração de dados e perfis de utilizador](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items)  

## <a name="windows-edition-upgrade-policy"></a>Política de atualização de edição do Windows  
 A política de atualização de edição permite atualizar automaticamente dispositivos Windows 10 para uma versão mais recente. Pode especificar uma chave de produto para atualizar versões de ambiente de trabalho do Windows 10 ou um ficheiro de licença que pode ser utilizado para atualizar dispositivos com o Windows 10 Mobile e o Windows 10 Holographic.  

 [Atualizar dispositivos Windows com a política de atualização de edição](/sccm/compliance/deploy-use/upgrade-windows-version)  

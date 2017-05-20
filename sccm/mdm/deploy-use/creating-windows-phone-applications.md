---
title: "Criar aplicações do Windows Phone | Documentos do Microsoft"
description: "Consulte as considerações tem de efetuar para conta quando criar e implementar aplicações para dispositivos Windows Phone."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: 6cbf2389a72c0c384ef8e84a1755ac77b64bfc6d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>Criar aplicações do Windows Phone com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma aplicação do System Center Configuration Manager tem um ou mais tipos de implementação que compõem os ficheiros de instalação e informações que são necessários para implementar software num dispositivo. Um tipo de implementação também contém as regras que especificam quando e como o software é implementado.  

 Pode criar aplicações utilizando os seguintes métodos:  

-   Crie automaticamente os tipos de aplicação e implementação ao ler os ficheiros de instalação da aplicação.  

-   Criar manualmente a aplicação e adicionar posteriormente os tipos de implementação.  

-   Importe uma aplicação a partir de um ficheiro.  

Consulte o artigo [iniciar o Assistente para criar aplicação](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) para os passos necessários para criar do Configuration Manager aplicações e tipos de implementação. Além disso, mantenha as seguintes considerações em consideração quando criar e implementar aplicações para dispositivos Windows Phone.  

## <a name="general-considerations"></a>Considerações gerais  
 O Configuration Manager suporta os seguintes tipos de ficheiro de aplicação a implementar:  

|Tipo de Dispositivo|Tipos de ficheiro suportados|  
|-----------------|---------------------|  
|Windows Phone 8|. xap|  
|Windows Phone 8.1|. xap,. AppX,. appxbundle|
|Windows 10 Mobile|. xap,. AppX,. appxbundle|

 As seguintes ações de implementação são suportadas:  

|Tipo de Dispositivo|Ações suportadas|  
|-----------------|-----------------------|  
|Windows Phone 8, Windows Phone 8.1 e Windows 10 Mobile|Disponível, Necessário, Desinstalar|  

## <a name="steps-to-deploy-the-latest-windows-phone-company-portal-app-with-supersedence"></a>Passos para implementar a mais recente Windows Phone aplicação portal da empresa com substituição  
 A tabela seguinte fornece os passos, detalhes e mais informações para criar e implementar a mais recente aplicação do portal da empresa do Windows Phone 8.  

|Passo|Mais informações|  
|----------|----------------------|  
|**Passo 1:** Obter a aplicação do portal da empresa mais recente.|Transfira a [aplicação do portal da empresa do Windows Phone 8](http://go.microsoft.com/fwlink/?LinkId=268440).|  
|**Passo 2:** Assinar a aplicação do portal da empresa com o certificado da Symantec.|Para obter informações sobre como assinar a aplicação do portal da empresa, consulte o artigo [configurar o Windows Phone e Windows 10 Mobile gestão de dispositivos de híbrida com o System Center Configuration Manager e o Microsoft Intune](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Passo 3:** Criar uma nova aplicação com a versão mais recente da aplicação portal da empresa e especificar uma relação de substituição.|Para obter mais informações, consulte o artigo [criar aplicações](../../apps/deploy-use/create-applications.md) e [rever e substituir aplicações](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Passo 4:** Adicione a aplicação ao Assistente de subscrição do Microsoft Intune.|Para obter mais informações, consulte o artigo [configurar o Windows Phone e Windows 10 Mobile gestão de dispositivos de híbrida com o System Center Configuration Manager e o Microsoft Intune](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Passo 5:** Elimine a implementação que foi criada automaticamente quando a aplicação do portal da empresa foi adicionada ao Assistente de subscrição do Microsoft Intune.|A subscrição do Microsoft Intune criou uma implementação automática desta aplicação, como esta implementação não suporta substituição.|  
|**Passo 6:** Crie uma nova implementação da aplicação. No **definições de implementação** página do **Assistente de implementação de Software**, verifique **automaticamente atualização qualquer superceded versões desta aplicação**.|Crie uma nova implementação com substituição, utilizando a aplicação que criou com a relação de substituição.|  
|**Passo 7 (opcional):** Por predefinição, as aplicações de substituição são instalam nos dispositivos decorridos 7 dias. Para implementar a empresa da aplicação do portal mais cedo para anteriormente os dispositivos inscritos, altere o **agendar reavaliação para implementações** na definição de um valor inferior.<br /><br /> Se definir este valor para um valor inferior a predefinição, poderá afetar negativamente o desempenho da sua rede e dos computadores cliente.|Não existem informações adicionais.|  


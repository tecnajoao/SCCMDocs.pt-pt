---
title: "Segurança e privacidade para gestão de energia | Documentos do Microsoft"
description: "Obter informações de segurança e privacidade para gestão de energia no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: 94d5418c364c318dba92dc9f9066f54d1130aa34
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="security-and-privacy-for-power-management-in-system-center-configuration-manager"></a>Segurança e privacidade para gestão de energia no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Esta secção contém informações de segurança e privacidade para gestão de energia no System Center Configuration Manager.  

## <a name="security-best-practices-for-power-management"></a>Melhores práticas de segurança para gestão de energia  
 Não existem melhores práticas relacionadas com segurança para gestão de energia.  

## <a name="privacy-information-for-power-management"></a>Informações de privacidade para gestão de energia  
 A gestão de energia utiliza funcionalidades incorporadas no Windows para monitorizar a utilização da energia e aplicar definições de energia aos computadores durante as horas de expediente e fora de expediente. O Configuration Manager recolhe informações de utilização do power a partir de computadores, que inclui dados sobre quando um utilizador está a utilizar um computador. Apesar do Configuration Manager monitoriza a utilização de energia para uma coleção e não para cada computador, uma coleção pode conter apenas um computador. A gestão de energia não está ativada por predefinição e tem de ser configurada por um administrador.  

 As informações de utilização do power são armazenadas na base de dados do Configuration Manager e não são enviadas à Microsoft. As informações detalhadas são mentidas na base de dados por 31 dias e as informações resumidas são mantidas por 13 meses. Não pode configurar o intervalo de eliminação.  

 Antes de configurar a gestão de energia, considere os requisitos de privacidade.  

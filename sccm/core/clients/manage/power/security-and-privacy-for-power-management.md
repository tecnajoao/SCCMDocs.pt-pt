---
title: "Segurança e privacidade para gestão de energia | Microsoft Docs"
description: "Obter informações de segurança e privacidade para gestão de energia no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
caps.latest.revision: "5"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 51a29eec13373f92a65ac09dfb23d1b5cdd1683a
ms.sourcegitcommit: f6a428a8db7145affa388f59e0ad880bdfcf17b5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/14/2017
---
# <a name="security-and-privacy-for-power-management-in-system-center-configuration-manager"></a>Segurança e privacidade para gestão de energia no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Esta secção contém informações de segurança e privacidade para gestão de energia no System Center Configuration Manager.  

## <a name="security-best-practices-for-power-management"></a>Melhores práticas de segurança para gestão de energia  
 Não existem melhores práticas relacionadas com segurança para gestão de energia.  

## <a name="privacy-information-for-power-management"></a>Informações de privacidade para gestão de energia  
 A gestão de energia utiliza funcionalidades incorporadas no Windows para monitorizar a utilização da energia e aplicar definições de energia aos computadores durante as horas de expediente e fora de expediente. O Configuration Manager recolhe informações de utilização de energia dos computadores, que inclui dados sobre quando um utilizador está a utilizar um computador. Apesar do Configuration Manager monitoriza a utilização de energia de uma coleção em vez de cada computador, uma coleção pode conter apenas um computador. A gestão de energia não está ativada por predefinição e tem de ser configurada por um administrador.  

 As informações de utilização de energia são armazenadas na base de dados do Configuration Manager e não são enviadas à Microsoft. As informações detalhadas são mentidas na base de dados por 31 dias e as informações resumidas são mantidas por 13 meses. Não pode configurar o intervalo de eliminação.  

 Antes de configurar a gestão de energia, considere os requisitos de privacidade.  

---
title: Segurança e privacidade para gestão de energia
titleSuffix: Configuration Manager
description: Obter informações de segurança e privacidade para gestão de energia no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 47ddbf358426b7683dab42b4f7a6a89ad8e631de
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
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

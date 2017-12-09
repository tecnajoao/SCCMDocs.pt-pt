---
title: "Utilização de dados de diagnóstico"
titleSuffix: Configuration Manager
description: "Saiba mais sobre como a Microsoft utiliza os diagnósticos e dados de utilização recolhe do System Center Configuration Manager."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
caps.latest.revision: "5"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: d34305ddb158a01c0d79189705af597344a56f8d
ms.sourcegitcommit: da27d37cc4e4e06cf23758846cdd7acb617f744b
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/08/2017
---
# <a name="how-diagnostics-and-usage-data-is-used-for-system-center-configuration-manager"></a>Como os diagnósticos e dados de utilização são utilizados para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Dados de diagnóstico e de utilização que recolhe do System Center Configuration Manager disponibilizam comentários quase de imediato à Microsoft sobre como o produto está a funcionar e é utilizado para ajustar as futuras atualizações. A Microsoft também consegue ver dados de configuração que nos ajudam a criar e testar as configurações que estão em produção. Por exemplo:  

-   As versões do Windows Server que são utilizadas por servidores de site  

-   Os pacotes de idiomas instalados  

-   O delta do esquema SQL relativamente à predefinição do produto  

Estes dados ajudam a equipa de engenharia a planear futuros testes, para garantir a melhor experiência nas configurações mais comuns. Como as atualizações do Configuration Manager são lançadas a uma cadência mais rápida (para suportar melhorar mudar depressa de tecnologias como o Windows 10 e o Microsoft Intune), estes dados são fundamentais para ajustar e adaptar rapidamente.  

Igualmente não é importante o modo como os diagnósticos e dados de utilização não são utilizados. A Microsoft não utiliza estes dados para:  

-   Auditorias de licenciamento, como comparar a utilização de cliente contra contratos de licença  

-   Auditoria de produtos que estão fora de suporte  

-   Publicidade com base nos dados disponíveis, tais como a utilização da funcionalidade ou a geolocalização (fuso horário)  

##  <a name="bkmk_improve"></a>Exemplos de como os diagnósticos e dados de utilização melhora o produto  
A Microsoft utiliza os dados disponíveis para melhorar o produto. Seguem-se alguns exemplos:  

-   **Suporte revisto para sistemas de operativos mais antigos do servidor:**  

     O suporte inicial oferecido pelo ramo atual do System Center Configuration Manager limitada linha cronológica de suporte para Windows Server 2008 R2. Após analisar os dados de utilização de clientes que tinham atualizados para o ramo atual do Configuration Manager, identificámos a necessidade de rever e expandir esta linha cronológica para suportar clientes que ainda utilizam este sistema de operativo de servidor para alojar servidores de sites e funções de sistema de sites.  

-   **Verificações de pré-requisitos melhorados:**  

     Com base nos dados de utilização, iremos tem melhorado as verificações de pré-requisitos para instalar uma atualização para remover regras obsoletas, conta casos adicionais e, em alguns casos, remediar automaticamente alguns problemas.  

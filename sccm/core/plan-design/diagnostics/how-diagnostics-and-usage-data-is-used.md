---
title: "Utilização de dados do diagnostics | Documentos do Microsoft"
description: "Saiba mais sobre como a Microsoft utiliza os diagnósticos e dados de utilização recolhe do System Center Configuration Manager."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 24a233516058e645df2a43623855665b97b041b0
ms.openlocfilehash: 9864f6ba7b9a2211c99b1a5d9ebd582e01ccfeb6
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-diagnostics-and-usage-data-is-used-for-system-center-configuration-manager"></a>Como os diagnósticos e dados de utilização são utilizados para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Dados de utilização e de diagnóstico que o System Center Configuration Manager recolhe fornece comentários quase imediato da Microsoft sobre como o produto está a funcionar e é utilizado para ajustar as futuras atualizações. A Microsoft também consegue ver dados de configuração que nos ajudam a criar e testar as configurações que estão em produção. Por exemplo:  

-   As versões do Windows Server que são utilizadas por servidores de site  

-   Os pacotes de idiomas instalados  

-   O delta do esquema SQL relativamente à predefinição do produto  

Estes dados ajudam a equipa de engenharia a planear futuros testes, para garantir a melhor experiência nas configurações mais comuns. Como são lançadas atualizações do Configuration Manager num cadence mais rápido (para um melhor suporte rapidamente mover as tecnologias como o Windows 10 e o Microsoft Intune), estes dados são fundamental ajustar rapidamente e adaptar o.  

Igualmente não são importante o modo como os dados de diagnóstico e de utilização não são utilizados. A Microsoft não utiliza estes dados para:  

-   Auditorias de licenciamento, como comparar a utilização de cliente contra contratos de licença  

-   Auditoria de produtos que estão fora de suporte  

-   Publicidade com base nos dados disponíveis, tais como a utilização da funcionalidade ou geolocalização (fuso horário)  

##  <a name="bkmk_improve"></a>Exemplos de como dados de utilização e de diagnóstico melhora o produto  
A Microsoft utiliza os dados disponíveis para melhorar o produto. Seguem-se alguns exemplos:  

-   **Suporte revisto para sistemas de operativos mais antigos do servidor:**  

     O suporte inicial oferecido pelo ramo atual do System Center Configuration Manager limitado a linha cronológica de suporte para Windows Server 2008 R2. Após analisar os dados de utilização dos clientes que tinham atualizado para o ramo atual do Configuration Manager, é identificada a necessidade de rever e expandir esta linha cronológica para suportar clientes que ainda utilizam este sistema operativo de servidor para servidores do anfitrião de sites e funções do sistema de sites.  

-   **Verificações de pré-requisitos melhorados:**  

     Com base nos dados de utilização, iremos tem melhorado as verificações de pré-requisitos para instalar uma atualização para remover regras obsoletas, para casos adicionais e, em alguns casos, a remediação automática alguns problemas de contas.  


---
title: Utilização de dados de diagnóstico
titleSuffix: Configuration Manager
description: Saiba mais sobre como a Microsoft usa os diagnósticos e dados de utilização que recolhe do System Center Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 404c68f954828dffe2bb9aed9dc59800aff83110
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120781"
---
# <a name="how-diagnostics-and-usage-data-is-used-for-system-center-configuration-manager"></a>Como os diagnósticos e dados de utilização são utilizados para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Dados de diagnóstico e de utilização que recolhe do System Center Configuration Manager disponibilizam comentários quase de imediato à Microsoft sobre como o produto está a funcionar e é utilizado para ajustar as futuras atualizações. A Microsoft também consegue ver dados de configuração que nos ajudam a criar e testar as configurações que estão em produção. Por exemplo:  

-   As versões do Windows Server que são utilizadas por servidores de site  

-   Pacotes de idiomas instalados  

-   O delta do esquema SQL relativamente à predefinição do produto  

Estes dados ajudam a equipa de engenharia a planear futuros testes, para garantir a melhor experiência nas configurações mais comuns. Como as atualizações para o Configuration Manager são lançadas a uma cadência mais rápida (para um melhor suporte a transferência de tecnologias como Windows 10 e o Microsoft Intune), estes dados são fundamentais para ajustar e adaptar rapidamente.  

Igualmente importante são como os dados de diagnóstico e utilização não são utilizados. A Microsoft não utiliza estes dados para:  

-   Auditorias de licenciamento, como comparar a utilização de cliente contra contratos de licença  

-   Auditoria de produtos que estão fora de suporte  

-   Publicidade com base nos dados disponíveis, como a utilização da funcionalidade ou a geolocalização (fuso horário)  

##  <a name="bkmk_improve"></a> Exemplos de como os dados de diagnóstico e utilização aumenta o produto  
A Microsoft utiliza os dados disponíveis para melhorar o produto. Seguem-se alguns exemplos:  

-   **Suporte revisto para sistemas de operativos mais antigos do servidor:**  

     O suporte inicial oferecido pelo ramo atual do System Center Configuration Manager limitado a linha cronológica de suporte para o Windows Server 2008 R2. Após analisar os dados de utilização de clientes que atualizaram para o Configuration Manager current branch, identificamos a necessidade de rever e expandir a linha de tempo para suportar os clientes que ainda utilizam este sistema de operativo de servidor para alojar servidores de sites e o sistema de sites funções.  

-   **Verificações de pré-requisitos melhorados:**  

     Com base nos dados de utilização, melhorámos as verificações de pré-requisitos para instalar uma atualização para remover regras obsoletas, conta para casos adicionais e, em alguns casos, para remediar automaticamente alguns problemas.  

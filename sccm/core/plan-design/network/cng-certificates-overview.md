---
title: "Descrição geral de certificados CNG"
titleSuffix: Configuration Manager
description: "Uma descrição geral dos certificados CNG no Configuration Manager"
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 
author: vhorne
ms.author: victorh
manager: angrobe
ms.openlocfilehash: f5f5138270d4f14b76b2c41e41ec034a0c12a932
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/21/2017
---
# <a name="cng-certificates-overview"></a>Descrição geral de certificados CNG
<!-- 1356191 --> 

O Configuration Manager limitou o suporte de criptografia: Certificados de geração (CNG) do seguintes. Clientes do Configuration Manager podem utilizar o certificado de autenticação de cliente PKI com chave privada no fornecedor de armazenamento de chaves do CNG (KSP). Com suporte para KSP, os clientes do Configuration Manager suportam a chave das privada baseada em hardware, tal como KSP de TPM para certificados de autenticação de cliente PKI.

## <a name="supported-scenarios"></a>Cenários suportados
Pode utilizar [Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) modelos para os seguintes cenários de certificado:

- O registo de cliente e comunicação com um ponto de gestão HTTPS.   
- Distribuição e aplicação de implementação de software com um ponto de distribuição de HTTPS.   
- Implementação do sistema operativo.  
- Cliente SDK (com a atualização mais recente) e o ISV Proxy de mensagens.   
- Configuração do Gateway de gestão de nuvem.  

> [!NOTE]
> CNG é retrocompatível com Crypto API (CAPI). Certificados CAPI continuam a ser suportada, mesmo quando o suporte CNG está ativado no cliente.

## <a name="unsupported-scenarios"></a>Cenários não suportados

Os cenários seguintes não são atualmente suportados:

- Serviço Web do catálogo de aplicações, o Web site do catálogo de aplicações, o ponto de registo e o proxy de registo do ponto de funções não está operacional quando instalada no modo HTTPS com um certificado CNG vinculado ao web site nos serviços de informações Internet (IIS). Centro de software não apresentar aplicações e pacotes como disponíveis que são implementadas em coleções de grupo do utilizador ou de utilizador.

- Ponto de migração de estado não está operacional quando instalada no modo HTTPS com um certificado CNG vinculado ao web site no IIS.

- Certificados CNG para criar um ponto de distribuição na nuvem.

- Módulo de política de NDES a comunicação de ponto de registo de certificados (CRP) falha se o módulo de política de NDES estiver a utilizar um certificado CNG para certificado de autenticação de cliente.

- Criação de suportes de dados de sequência de tarefas não consegue criar suportes de dados, se for especificado um certificado CNG.

## <a name="to-use-cng-certificates"></a>Para utilizar certificados CNG

Para utilizar certificados CNG, a sua autoridade de certificação (AC) tem de fornecer modelos de certificado CNG máquinas de destino. Detalhes de modelo variam de acordo com o cenário; No entanto, as seguintes propriedades são necessárias:

- **Compatibilidade** separador

    - **Autoridade de certificado** tem de ser Windows Server 2008 ou posterior. (Windows Server 2012 é recomendado.)

    - **Destinatário do certificado** tem de ser Windows Vista/Server 2008 ou posterior. (Windows 8/Windows Server 2012 é recomendado.)

- **Criptografia** separador

    - **Categoria de fornecedor** tem de ser **Key Storage Provider**. (obrigatório)

> [!NOTE]
> Os requisitos para o seu ambiente ou a organização podem ser diferentes. Contacte o seu especialista PKI. O ponto importante a ter em consideração é que um modelo de certificado tem de utilizar um fornecedor de armazenamento de chave para tirar partido das CNG.

Para obter os melhores resultados, recomendamos a criação de nome do requerente de informações do Active Directory. Utilize o nome de DNS para **formato de nome de requerente** e incluir o nome DNS no nome do requerente alternativo. Caso contrário, tem de fornecer estas informações quando inscreve o dispositivo para o perfil de certificado.
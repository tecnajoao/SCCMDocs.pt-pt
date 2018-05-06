---
title: Descrição geral de certificados CNG
titleSuffix: Configuration Manager
description: Saiba mais sobre o suporte para certificados de Cryptography Next Generation (CNG) para servidores e clientes do Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4a4f37330f94111bcc41b81d9127039056f69e2b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="cng-certificates-overview"></a>Descrição geral de certificados CNG
<!-- 1356191 --> 

O Configuration Manager limitou o suporte de criptografia: Certificados de geração (CNG) do seguintes. Clientes do Configuration Manager podem utilizar o certificado de autenticação de cliente PKI com chave privada no fornecedor de armazenamento de chaves do CNG (KSP). Com suporte para KSP, os clientes do Configuration Manager suportam a chave das privada baseada em hardware, tal como KSP de TPM para certificados de autenticação de cliente PKI.

## <a name="supported-scenarios"></a>Cenários suportados
Pode utilizar [Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) modelos para os seguintes cenários de certificado:

- O registo de cliente e comunicação com um ponto de gestão HTTPS   
- Implementação de distribuição e a aplicação de software com um ponto de distribuição de HTTPS   
- Implementação do sistema operativo  
- Cliente mensagens SDK (com a atualização mais recente) e o ISV Proxy   
- Configuração do Gateway de gestão de nuvem  

A partir da versão 1802, utilize certificados CNG para as seguintes funções de servidor ativado para HTTPS: <!-- 1357314 -->   
- Ponto de gestão
- Ponto de distribuição
- Ponto de atualização de software
- Ponto de Migração de Estado     

> [!NOTE]
> CNG é retrocompatível com Crypto API (CAPI). Certificados CAPI continuam a ser suportada, mesmo quando o suporte CNG está ativado no cliente.

## <a name="unsupported-scenarios"></a>Cenários não suportados

Os cenários seguintes não são atualmente suportados:

- As seguintes funções de servidor não estão operacionais quando instalada no modo HTTPS com um certificado CNG vinculado ao web site nos serviços de informações Internet (IIS): 
    - Serviço de web do catálogo de aplicações
    - Web site do catálogo de aplicações
    - Ponto de inscrição  
    - Ponto proxy de registo  

- Centro de software não apresentar aplicações e pacotes como disponíveis que são implementadas em coleções de grupo do utilizador ou de utilizador.

- Certificados CNG para criar um ponto de distribuição na nuvem.

- Se o módulo de política NDES estiver a utilizar um certificado CNG para autenticação de cliente, falha de comunicação para o ponto de registo de certificados.

- Se especificar um certificado CNG durante a criação de suportes de dados de sequência de tarefas, o assistente não consegue criar suportes de dados.

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
---
title: Descrição geral de certificados CNG
titleSuffix: Configuration Manager
description: Saiba mais sobre o suporte para certificados de Cryptography Next Generation (CNG) para servidores e clientes do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b85961c14c3db69c3e02e776798588fadd0fc89
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383158"
---
# <a name="cng-certificates-overview"></a>Descrição geral de certificados CNG
<!-- 1356191 --> 

O Configuration Manager tem suporte limitado para criptografia: Próxima certificados de geração (CNG). Clientes do Configuration Manager podem utilizar o certificado de autenticação de cliente PKI com chave privada no fornecedor de armazenamento de chaves do CNG (KSP). Com o suporte KSP, clientes do Configuration Manager suportam a chave de privada baseada em hardware, como o KSP de TPM para certificados de autenticação de cliente PKI.

## <a name="supported-scenarios"></a>Cenários suportados
Pode usar [API de criptografia: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) modelos para os seguintes cenários de certificado:

- Registo de clientes e a comunicação com um ponto de gestão HTTPS   
- Implantação de aplicativo e distribuição de software com um ponto de distribuição de HTTPS   
- Implementação do sistema operativo  
- Cliente de mensagens SDK (com a atualização mais recente) e de ISV Proxy   
- Configuração do Gateway de gestão de cloud  

A partir da versão 1802, utilize certificados CNG para as seguintes funções de servidor com capacidade para HTTPS: <!-- 1357314 -->   
- Ponto de gestão
- Ponto de distribuição
- Ponto de atualização de software
- Ponto de Migração de Estado     

A partir da versão 1806, utilize certificados CNG para as seguintes funções de servidor com capacidade para HTTPS:

- Ponto de registo de certificados, incluindo o servidor do NDES com o módulo de política do Configuration Manager <!--1357314-->

> [!NOTE]
> A CNG é retrocompatível com Crypto CAPI (API). Certificados CAPI continuam a ser suportada, mesmo quando o suporte da CNG está ativado no cliente.

## <a name="unsupported-scenarios"></a>Cenários não suportados

Os cenários seguintes não são atualmente suportados:

- As seguintes funções de servidor não estão operacionais quando instalado no modo HTTPS com um certificado CNG vinculado ao web site nos serviços de informação Internet (IIS): 
    - Serviço de web do catálogo de aplicações
    - Web site do catálogo de aplicações
    - Ponto de inscrição  
    - Ponto proxy de registo  

- Centro de software não apresenta as aplicações e pacotes como estando disponíveis que são implementadas para o utilizador ou coleções de grupo de utilizadores.

- Utilizar certificados CNG para criar um ponto de distribuição de nuvem.

- Se o módulo de política NDES estiver a utilizar um certificado CNG para autenticação de cliente, a comunicação com o ponto de registo de certificados falhará. 
    - Isso é suportado a partir do Configuration Manager versão 1806.

- Se especificar um certificado da CNG ao criar suportes de dados de sequência de tarefas, o assistente não consegue criar suportes de dados.
    - Isso é suportado a partir do Configuration Manager versão 1806.

## <a name="to-use-cng-certificates"></a>Para utilizar certificados CNG

Para utilizar certificados CNG, a sua autoridade de certificação (AC) tem de fornecer modelos de certificado da CNG para máquinas de destino. Detalhes do modelo variam de acordo com o cenário. No entanto, as seguintes propriedades são necessárias:

- **Compatibilidade** separador

    - **Autoridade de certificação** tem de ser Windows Server 2008 ou posterior. (O Windows Server 2012 é recomendado.)

    - **Destinatário do certificado** tem de ser Windows Vista/Server 2008 ou posterior. (O Windows 8 e Windows Server 2012 é recomendado.)

- **Criptografia** separador

    - **Categoria de fornecedor** tem de ser **Key Storage Provider**. (obrigatório)
    - **Pedido tem de utilizar um dos seguintes fornecedores:** tem de ser **Microsoft Software Key Storage Provider**. 

> [!NOTE]
> Os requisitos para o seu ambiente ou a organização poderão ser diferentes. Entre em contato com o especialista PKI. O ponto importante a considerar é que um modelo de certificado tem de utilizar um fornecedor de armazenamento de chave para tirar partido da CNG.

Para obter melhores resultados, recomendamos a criação de nome do requerente de informações do Active Directory. Utilize o nome de DNS para **formato de nome de requerente** e incluir o nome DNS no nome do requerente alternativo. Caso contrário, tem de fornecer estas informações quando o dispositivo é inscrito para o perfil de certificado.
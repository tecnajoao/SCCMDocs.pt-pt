---
title: "Propriedades de instalação de cliente nos serviços de domínio do Active Directory | Documentos do Microsoft"
description: "Utilize as propriedades de instalação de cliente publicadas nos serviços de domínio do Active Directory no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 4eee9731a4a27328c47c0d15931cab28cf520a18
ms.openlocfilehash: 744bc3792a02f13d3cf940cd1a4f2fd8749ee2f4
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services"></a>Acerca das propriedades de instalação de cliente publicadas nos serviços de domínio do Active

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando expande o esquema do Active Directory para o System Center Configuration Manager e o site esteja publicado nos serviços de domínio do Active, muitas propriedades de instalação de cliente são publicadas no Active Directory Domain Services. Se um computador conseguir localizar estas propriedades de instalação de cliente, poderá utilizá-las durante a implementação do cliente do Configuration Manager.  

 As vantagens da utilização dos Serviços de Domínio do Active Directory para publicação das propriedades de instalação do cliente incluem:  

-   Instalações de cliente baseada em ponto de atualização de software e as instalações de cliente de política de grupo não requerem parâmetros de configuração ser configurada em cada computador.  

-   Como estas informações são geradas automaticamente, o risco de erro humano associado à introdução manual das propriedades de instalação é eliminado.  

> [!NOTE]  
>  Para obter mais informações sobre como expandir o esquema do Active Directory para o Configuration Manager e como publicar um site, consulte o artigo [extensões de esquema para o System Center Configuration Manager](../../plan-design/network/schema-extensions.md).  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Propriedades de instalação de cliente publicadas nos serviços de domínio do Active  
Segue-se uma lista das propriedades de instalação de cliente. Para obter mais informações sobre cada item na lista abaixo, consulte o artigo [acerca das propriedades de instalação de cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

-   O código do site do Configuration Manager.  

-   O certificado de assinatura do servidor do site.  

-   A chave de raiz fidedigna.  

-   As portas de comunicação de cliente para HTTP e HTTPS.  

-   O ponto de estado de contingência. Se o site tiver vários pontos de estado de contingência, apenas o primeiro que tenha sido instalado é publicado para serviços de domínio do Active Directory.  

-   Uma definição para indicar que o cliente terá de comunicar utilizando apenas HTTPS.  

-   Definições relacionadas com os certificados PKI:  

   -   Se deverá ser utilizado um certificado PKI de cliente.  

   -   Os critérios de seleção de certificado. Isto poderá ser necessário porque o cliente tiver mais do que um certificado PKI válido que pode ser utilizado para o Configuration Manager.  

   -   Uma definição para determinar qual o certificado a utilizar se o cliente tiver vários certificados válidos após o processo de seleção de certificados.  

   -   A lista de emissores de certificados que contém uma lista de certificados de AC de raiz fidedigna.  

-   As propriedades de instalação client.msi especificadas no separador **Cliente** da caixa de diálogo **Propriedades da Instalação Push do Cliente** .

Instalação do cliente (CCMSetup) utiliza as propriedades que são publicadas nos serviços de domínio do Active apenas se não outras são especificadas propriedades, utilizando qualquer um dos seguintes procedimentos:  

-   O método de instalação manual (descrito neste artigo)

-   O método de instalação de política de grupo (descrito neste artigo)

> [!NOTE]  
>  As propriedades de instalação do cliente são utilizadas para instalar o cliente. Estas propriedades poderão ser substituídas por novas definições a partir do respetivo site atribuído após o cliente é instalado e tiver sido atribuído com êxito a um site do Configuration Manager.  

 Utilize as informações nas secções seguintes para determinar que métodos de instalação de cliente do Configuration Manager utilizarem Serviços de domínio do Active Directory para obter propriedades de instalação do cliente.  

## <a name="client-push-installation"></a>Instalação push do cliente  
 A instalação push do cliente não utiliza Serviços de Domínio do Active Directory para obter as propriedades de instalação.  

 Em vez disso, pode especificar propriedades de instalação do cliente no **cliente** separador do **propriedades da instalação Push do cliente** caixa de diálogo. Estas opções e definições do site relacionadas com o cliente são armazenadas num ficheiro lido pelo cliente durante a instalação de cliente.  

> [!NOTE]  
>  Não é necessário especificar quaisquer propriedades CCMSetup para a instalação push do cliente, para o ponto de estado de contingência ou para a chave de raiz fidedigna no separador **Cliente** . Estas definições são fornecidas automaticamente aos clientes quando são instalados utilizando a instalação push do cliente.  

 Quaisquer propriedades que especificou no **cliente** separador são publicadas nos serviços de domínio do Active se o site for publicado naqueles serviços de domínio do Active Directory. Estas definições são lidas pelas instalações de cliente em que o CCMSetup seja executado sem propriedades de instalação.  

## <a name="software-update-point-based-installation"></a>Instalação baseada em pontos de atualizações de software  
 O método de instalação baseada em pontos de atualizações de software não suporta a adição de propriedades de instalação à linha de comandos CCMSetup.  

 Se não tiverem sido aprovisionadas propriedades de linha de comandos no computador cliente utilizando a Política de Grupo, o CCMSetup procurará as propriedades de instalação nos Serviços de Domínio do Active Directory.  

## <a name="group-policy-installation"></a>Instalação de Política de Grupo  
 O método de instalação de Política de Grupo não suporta a adição de propriedades de instalação à linha de comandos CCMSetup.  

 Se não tiverem sido aprovisionadas propriedades de linha de comandos no computador cliente, o CCMSetup procurará as propriedades de instalação nos Serviços de Domínio do Active Directory.  

## <a name="manual-installation"></a>Instalação manual  
 O CCMSetup procura as propriedades de instalação dos Serviços de Domínio do Active Directory nas seguintes circunstâncias:  

-   Não são especificadas propriedades da linha de comandos após o comando CCMSetup.exe.  

-   O computador não foi aprovisionado com propriedades de instalação utilizando a Política de Grupo.  

## <a name="logon-script-installation"></a>Instalação do script de início de sessão  
 O CCMSetup procura as propriedades de instalação dos Serviços de Domínio do Active Directory nas seguintes circunstâncias:  

-   Não são especificadas propriedades da linha de comandos após o comando CCMSetup.exe.  

-   O computador não foi aprovisionado com propriedades de instalação utilizando a Política de Grupo.  

## <a name="software-distribution-installation"></a>Instalação de distribuição de software  
 O CCMSetup procura as propriedades de instalação dos Serviços de Domínio do Active Directory nas seguintes circunstâncias:  

-   Não são especificadas propriedades da linha de comandos após o comando CCMSetup.exe.  

-   O computador não foi aprovisionado com propriedades de instalação utilizando a Política de Grupo.  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services"></a>Instalações para clientes que não é possível aceder a serviços de domínio do Active Directory  
Estes computadores cliente não consegue ler ou aceder às propriedades de instalação publicadas a partir de serviços de domínio do Active Directory.

 Estes clientes incluem:  

-   Computadores de grupo de trabalho.  

-   Clientes que estejam atribuídos a um site do Configuration Manager que não está publicado para serviços de domínio do Active Directory.  

-   Clientes que são instalados quando se encontram na Internet.  


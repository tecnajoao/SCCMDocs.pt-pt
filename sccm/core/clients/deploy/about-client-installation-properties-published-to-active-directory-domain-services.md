---
title: Propriedades de instalação de cliente nos serviços de domínio do Active Directory
titleSuffix: Configuration Manager
description: Utilize propriedades de instalação de cliente publicadas nos serviços de domínio do Active Directory no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 46ede93e8366b4ae387f7e04b83dcb33ce854c5e
ms.sourcegitcommit: 3dfe3f4401651afa9dc65d14a8944ae4e4198b3e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/08/2018
ms.locfileid: "48862520"
---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services"></a>Acerca das propriedades de instalação de cliente publicadas no Active Directory Domain Services

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando expande o esquema do Active Directory para o System Center Configuration Manager e o site é publicado para serviços de domínio do Active Directory, muitas propriedades de instalação de cliente são publicadas para serviços de domínio do Active Directory. Se um computador conseguir localizar estas propriedades de instalação do cliente, pode utilizá-los durante a implementação de cliente do Configuration Manager.  

 As vantagens da utilização dos Serviços de Domínio do Active Directory para publicação das propriedades de instalação do cliente incluem:  

-   Instalações de cliente baseada em pontos de atualização de software e as instalações de cliente de política de grupo não necessitam de parâmetros de configuração para configurar em cada computador.  

-   Como estas informações são geradas automaticamente, o risco de erro humano associado à introdução manual das propriedades de instalação é eliminado.  

> [!NOTE]  
>  Para obter mais informações sobre como expandir o esquema do Active Directory para o Configuration Manager e como publicar um site, consulte [extensões de esquema para o System Center Configuration Manager](../../plan-design/network/schema-extensions.md).  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Propriedades de instalação de cliente publicadas para serviços de domínio do Active Directory  
Segue-se uma lista de propriedades de instalação do cliente. Para obter mais informações sobre cada item, listado abaixo, veja [acerca das propriedades de instalação de cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

-   O código do site do Configuration Manager.  

-   O certificado de assinatura do servidor do site.  

-   A chave de raiz fidedigna.  

-   As portas de comunicação de cliente para HTTP e HTTPS.  

-   O ponto de estado de contingência. Se o site tiver vários pontos de estado de contingência, apenas o primeiro aquele que foi instalado é publicado no Active Directory Domain Services.  

-   Uma definição para indicar que o cliente terá de comunicar utilizando apenas HTTPS.  

-   Definições relacionadas com os certificados PKI:  

   -   Se deverá ser utilizado um certificado PKI de cliente.  

   -   Os critérios de seleção para a seleção de certificado. Isso pode ser necessário uma vez que o cliente tiver mais do que um certificado PKI válido que pode ser utilizado para o Configuration Manager.  

   -   Uma definição para determinar qual o certificado a utilizar se o cliente tiver vários certificados válidos após o processo de seleção de certificados.  

   -   A lista de emissores de certificados que contém uma lista de certificados de AC de raiz fidedigna.  

-   As propriedades de instalação client.msi especificadas no separador **Cliente** da caixa de diálogo **Propriedades da Instalação Push do Cliente** .

Instalação do cliente (CCMSetup) utiliza as propriedades que são publicadas em serviços de domínio do Active Directory apenas se não existem outras propriedades são especificadas com qualquer um dos seguintes procedimentos:  

-   O método de instalação manual (descrito mais adiante neste artigo)

-   O método de instalação de política de grupo (descrito mais adiante neste artigo)

> [!NOTE]  
>  As propriedades de instalação de cliente são utilizadas para instalar o cliente. Essas propriedades podem ser substituídas por novas definições do respetivo site atribuído após o cliente é instalado e que lhe foi atribuído com êxito um site do Configuration Manager.  

 Utilize os detalhes nas seções a seguir para determinar quais métodos de instalação de cliente do Configuration Manager utilizam serviços de domínio do Active Directory para obter as propriedades de instalação de cliente.  

## <a name="client-push-installation"></a>Instalação push do cliente  
 A instalação push do cliente não utiliza Serviços de Domínio do Active Directory para obter as propriedades de instalação.  

 Em vez disso, pode especificar propriedades de instalação do cliente na **das propriedades de instalação** separador da **propriedades da instalação Push do cliente** caixa de diálogo. Estas opções e definições do site relacionadas com o cliente são armazenadas num ficheiro lido pelo cliente durante a instalação de cliente.  

> [!NOTE]  
>  Não é necessário especificar quaisquer propriedades CCMSetup para a instalação push do cliente, ou o ponto de estado de contingência ou a chave de raiz fidedigna no **das propriedades de instalação** separador. Estas definições são fornecidas automaticamente aos clientes quando são instalados utilizando a instalação push do cliente.
Para além das propriedades de Client. msi, o CCMSetup suporta os seguintes parâmetros: /forcereboot, /skipprereq, /logon, /BITSPriority, /downloadtimeout, /forceinstall

 Todas as propriedades que especificou na **das propriedades de instalação** separador são publicados para serviços de domínio do Active Directory se o site é publicado para serviços de domínio do Active Directory. Estas definições são lidas pelas instalações de cliente em que o CCMSetup seja executado sem propriedades de instalação.  

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
Estes computadores cliente não é possível ler ou acessar as propriedades de instalação publicadas dos serviços de domínio do Active Directory.

 Esses clientes incluem:  

-   Computadores de grupo de trabalho.  

-   Clientes que estejam atribuídos a um site do Configuration Manager que não está publicado para serviços de domínio do Active Directory.  

-   Clientes que são instalados quando se encontram na Internet.  

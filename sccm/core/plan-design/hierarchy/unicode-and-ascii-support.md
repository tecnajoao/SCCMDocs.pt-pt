---
title: Unicode e ASCII suporte
titleSuffix: Configuration Manager
description: Saiba mais sobre o suporte para caracteres Unicode e ASCII no System Center Configuration Manager objetos.
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8700919d372722f16001fcf1405531b0e2b383ff
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138386"
---
# <a name="unicode-and-ascii-support-in-system-center-configuration-manager"></a>Suporte de Unicode e ASCII no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager cria a maioria dos objetos utilizando carateres Unicode. No entanto, vários objetos suportam apenas carateres ASCII ou têm outras limitações.  

 As secções seguintes listam os objetos que tem de utilizar apenas de conjunto de carateres ASCII ou que têm outras limitações.  

-   [Objetos que utilizam carateres ASCII](#BKMK_ASCIIchar)  

-   [Limitações adicionais](#BKMK_OtherCharLimitations)  

-   [Objetos do Configuration Manager que não estão localizados](#BKMK_LangNonLocalize)  

##  <a name="BKMK_ASCIIchar"></a> Objetos que utilizam carateres ASCII  
 O Configuration Manager suporta apenas quando são criados os seguintes objetos de conjunto de carateres ASCII:  

-   Código do site  

-   Todos os nomes de computador do servidor de sistema do site  

-   As seguintes contas do Configuration Manager:  

    > [!NOTE]  
    >  Estas contas suportam carateres ASCII e carateres RUS num site que é executado em russo.  

    -   Conta de instalação push do cliente  

    -   Conta de publicação de referência de estado de funcionamento  

    -   Conta de consulta de referência do Estado de funcionamento  

    -   Base de dados ligar a conta de ponto de gestão  

    -   Conta de acesso à rede  

    -   Conta de acesso do pacote  

    -   Conta de remetente padrão  

    -   Conta de instalação do sistema de sites  

    -   Conta de ligação de ponto de atualização de software  

    -   Conta de servidor de proxy de ponto de atualização de software  

    > [!NOTE]  
    >  As contas que especificar para a administração baseada em funções suportam Unicode.  
    >   
    >  Conta suporta Unicode, com exceção dos carateres RUS do ponto do Reporting Services.  

-   Nome de domínio completamente qualificado (FQDN) para servidores de site e sistemas de sites  

-   Caminho de instalação para o Configuration Manager  

-   Nomes de instâncias do SQL Server  

-   O caminho para as seguintes funções de sistema de sites:  

    -   Ponto de serviço Web do Catálogo de Aplicações  

    -   Ponto de site do Catálogo de Aplicações  

    -   Ponto de inscrição  

    -   Ponto proxy de registo  

    -   Ponto do Reporting Services  

    -   Ponto de Migração de Estado  

-   O caminho para as seguintes pastas:  

    -   A pasta que armazena dados de migração de estado do cliente  

    -   A pasta que contém os relatórios do Configuration Manager  

    -   A pasta que armazena a cópia de segurança do Configuration Manager  

    -   A pasta que armazena os ficheiros de origem de instalação para a configuração do site  

    -   A pasta que armazena o pré-requisito downloads para utilização pela configuração  

-   O caminho para os seguintes objetos:  

    -   Web site do IIS  

    -   Caminho de instalação de aplicação virtual  

    -   Nome da aplicação virtual  

-   Os seguintes objetos para AMT e de gestão fora de banda:  

    -   O FQDN do computador baseado em AMT  

    -   O nome do computador do computador baseado em AMT  

    -   O nome NetBIOS do domínio  

    -   O nome do perfil sem fio e o SSID  

    -   O nome de autoridade de certificação de raiz fidedigna  

    -   O nome da autoridade de certificação (AC) e nomes de modelos  

    -   O nome de ficheiro e caminho para o ficheiro de imagem de redirecionamento de IDE  

    -   O conteúdo do armazenamento de dados AMT  

-   Suporte de dados nomes de ficheiro ISO  

##  <a name="BKMK_OtherCharLimitations"></a> Limitações adicionais  
 Seguem-se limitações adicionais para conjuntos de carateres suportados e versões de idioma:  

-   O Configuration Manager não suporta a alteração da localidade do computador do servidor do site.  

-   Uma autoridade de certificação (AC) empresarial não suporta nomes de computadores cliente que utilizam conjuntos de caracteres de byte duplo (DBCS). Os nomes de computador cliente que podem ser utilizados são restringidos pela limitação PKI do conjunto de carateres IA5. Além disso, o Configuration Manager não suporta nomes de AC ou valores de nome de requerente que utilizem DBCS.  

##  <a name="BKMK_LangNonLocalize"></a> Objetos do Configuration Manager que não estão localizados  
 A base de dados do Configuration Manager suporta Unicode para a maioria dos objetos que armazena e sempre que possível, apresenta estas informações no idioma do sistema operativo que corresponde à região de um computador. Para a interface do cliente ou a consola do Configuration Manager para apresentar informações no idioma do sistema operativo do computador, a região do computador tem de corresponder ao idioma cliente ou servidor que instalar num site.  

 No entanto, vários objetos do Configuration Manager não suportam Unicode e eles são armazenados na base de dados utilizando ASCII ou têm outras limitações de idioma. Estas informações são sempre apresentadas utilizando o conjunto de carateres ASCII ou no idioma que estava a ser utilizado quando o objeto foi criado.  

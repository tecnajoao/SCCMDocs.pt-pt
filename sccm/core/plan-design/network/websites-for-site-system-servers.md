---
title: Web sites para sistemas de sites
titleSuffix: Configuration Manager
description: Saiba mais sobre sites predefinidos e personalizados para servidores de sistema de sites no System Center Configuration Manager.
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
caps.latest.revision: "15"
caps.handback.revision: "0"
author: mstewart
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 6249a46714396c2dee0c061e8c2c26480fee8569
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="websites-for-site-system-servers-in-system-center-configuration-manager"></a>Sites para servidores do sistema de sites no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Várias funções de sistema de sites do Configuration Manager requerem a utilização dos serviços de informação de Internet do Microsoft (IIS) e utilizam o site predefinido do IIS para alojar serviços do sistema de sites. Quando tem de executar outras aplicações web mesmo servidor e as definições não são compatíveis com o Configuration Manager, considere utilizar um Web site personalizado para o Configuration Manager.  

> [!TIP]  
>  Uma melhor prática de segurança é dedique um servidor para os sistemas de sites do Configuration Manager necessitam do IIS. Quando executar outras aplicações num Gestor de configuração do sistema de sites, aumenta a superfície de ataque desse computador.  




##  <a name="BKMK_What2Know"></a>O que deve saber antes de optar por utilizar sites personalizados  
 Por predefinição, as funções do sistema de sites utilizam o **Site Predefinido** no IIS. Isto é configurado automaticamente quando instala a função de sistema de sites. No entanto, nos sites primários, pode optar por utilizar sites personalizados como alternativa. Quando utilizar Web sites personalizados:  

-   Os Web sites personalizados estão ativados para todo o local em vez de para funções ou servidores do sistema de sites individuais.  

-   Em sites primários, cada computador que irá alojar uma função de sistema de sites aplicável deve ser configurado com um Web site personalizado denominado **SMSWEB**. Depois de criar este Web site e configurar funções de sistema de sites nesse computador para utilizar o Web site personalizado, os clientes poderão não conseguir comunicar com funções de sistema de sites nesse computador.  

-   Porque os sites secundários são automaticamente configurados para utilizar um Web site personalizado quando o respetivo site primário principal está configurado para fazê, tem também de criar os Web sites personalizados no IIS em cada servidor de sistema de sites secundários que requer o IIS.  


  **Pré-requisitos para utilizar sites personalizados:**  

 Antes de ativar a opção para utilizar Web sites personalizados num site, tem de:  

-   Criar um Web site personalizado denominado **SMSWEB** no IIS em cada servidor de sistema de sites que requer o IIS. Pode fazê-lo no site primário e em quaisquer sites secundários.  

-   Configure o Web site personalizado para responder à mesma porta que configurou para a comunicação de cliente do Configuration Manager (porta de pedido de cliente).  

-   Para cada personalizado ou Web site predefinido que utilize uma pasta personalizada, coloque uma cópia da predefinida documentar tipo que utilizar na pasta raiz que aloja o Web site. Por exemplo, num computador Windows Server 2008 R2 com configurações predefinidas, **iisstart.htm** é uma das predefinido vários tipos de documentos que estão disponíveis. Pode encontrar este ficheiro na raiz do Web site predefinido e, em seguida, coloque uma cópia deste ficheiro (ou uma cópia do tipo de documento predefinido que utilizar) na pasta raiz que aloja o site personalizado SMSWEB. Para mais informações sobre tipos de documentos predefinidos, consulte [documento predefinido &lt;defaultDocument\> para o IIS](http://www.iis.net/configreference/system.webserver/defaultdocument).  

**Sobre os requisitos do IIS:**
**as seguintes funções do sistema de sites requerem o IIS e um Web site para alojar os serviços de sistema de sites:**  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Ponto de Web site do Catálogo de Aplicações  

-   Ponto de distribuição  

-   Ponto de inscrição  

-   Ponto proxy de registo  

-   Ponto de estado de contingência  

-   Ponto de gestão  

-   Ponto de atualização de Software  

-   Ponto de migração de estado  

Considerações adicionais:  

-   Quando um site primário tem sites personalizados ativados, os clientes atribuídos a esse site são direcionados para comunicar com os sites personalizados em vez dos sites predefinidos em servidores do sistema de sites aplicáveis  

-   Se utilizar sites personalizados para um site primário, considere os Web sites personalizados para todos os sites primários na hierarquia para garantir que os clientes podem fazer roaming com êxito na hierarquia. (Roaming é quando move um computador cliente para um novo segmento de rede gerido por um site diferente. O roaming pode afetar recursos que um cliente pode aceder localmente em vez de através de uma ligação WAN).  

-   Funções de sistema de sites que utilizam IIS, mas não aceitam ligações de cliente, como o ponto do Reporting Services, também utilizam o site SMSWEB em vez do Web site predefinido.  

-   Os Web sites personalizados necessitam que atribua números de porta diferentes das que utiliza o Web site predefinido do computador. Um site predefinido e um site personalizado não podem ser executados em simultâneo se ambos tentarem utilizar as mesmas portas TCP/IP.  

-   As portas TCP/IP que configurou no IIS para o Web site personalizado têm de corresponder as portas de pedido de cliente para o site.  

## <a name="switch-between-default-and-custom-websites"></a>Alternar entre sites predefinidos e personalizados  
Embora possa verificar ou desmarque a caixa para utilizar sites personalizados num site primário em qualquer altura (é a caixa no separador Geral das propriedades do site), planeie cuidadosamente antes de efetuar esta alteração. Quando esta configuração é alterada, todas as funções de sistema de sites aplicáveis no site primário e sites secundários subordinados têm de desinstalar e reinstalar:  

As seguintes funções **são reinstaladas automaticamente**:  

-   Ponto de gestão  

-   Ponto de distribuição  

-   Ponto de atualização de Software  

-   Ponto de estado de contingência  

-   Ponto de migração de estado  

As seguintes funções têm de ser **reinstaladas manualmente**:  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Ponto de Web site do Catálogo de Aplicações  

-   Ponto de inscrição  

-   Ponto proxy de registo  

Além disso,  

-   Quando muda do Web site predefinido para utilizar um Web site personalizado, o Configuration Manager não remove os diretórios virtuais antigos. Se pretender remover os ficheiros que utilizados do Configuration Manager, terá de eliminar manualmente os diretórios virtuais que foram criados no Web site predefinido.  

-   Se alterar o site para utilizar sites personalizados, os clientes já atribuídos ao site têm de ser reconfigurados para utilizar as novas portas de pedido de cliente para os sites personalizados. Consulte [como configurar portas de comunicação de cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

## <a name="set-up-custom-websites"></a>Configurar sites personalizados  
Uma vez que os passos para criar um site personalizado variam consoante as versões do sistema operativo, consulte a documentação da versão do seu sistema operativo para obter os passos exatos, mas utilize as seguintes informações quando for aplicável:  

-   O nome do site tem de ser: **SMSWEB**.  

-   Quando configurar o HTTPS, tem de especificar um certificado SSL para poder guardar a configuração.  

-   Depois de criar o Web site personalizado, remova as portas do Web site personalizado que utiliza a partir de outros sites no IIS:  

    1.  Editar o **enlaces** dos outros sites para remover as portas que correspondem às que são atribuídos ao **SMSWEB** Web site.  

    2.  Iniciar o **SMSWEB** Web site.  

    3.  Reinicie o serviço **SMS_SITE_COMPONENT_MANAGER** no servidor do site.  

---
title: Os Web sites para os sistemas de sites | Documentos do Microsoft
description: Saiba mais sobre predefinidos e Web sites personalizados para servidores de sistema de sites no System Center Configuration Manager.
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 26bbec1e8d6c53ce297689ba4390b9347229eb15
ms.openlocfilehash: 886ff3b8e867fc340c79648a57feae81653b0ccd
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="websites-for-site-system-servers-in-system-center-configuration-manager"></a>Sites para servidores do sistema de sites no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Várias funções de sistema de sites do Configuration Manager requerem a utilização dos serviços de informação de Internet do Microsoft (IIS) e utilizarem o Web site do IIS predefinido para serviços do sistema de sites de anfitrião. Quando tem de executar outras aplicações web mesmo servidor e as definições não são compatíveis com o Configuration Manager, considere utilizar um Web site personalizado para o Configuration Manager.  

> [!TIP]  
>  Uma melhor prática de segurança é dedique um servidor para os sistemas de sites do Configuration Manager que requerem o IIS. Quando executar outras aplicações num Gestor de configuração do sistema de sites, aumenta a superfície de ataque do computador.  




##  <a name="BKMK_What2Know"></a>O que deve saber antes de optar por utilizar Web sites personalizados  
 Por predefinição, as funções do sistema de sites utilizam o **Site Predefinido** no IIS. Isto é configurado automaticamente quando instala a função de sistema de sites. No entanto, nos sites primários, pode optar por utilizar sites personalizados como alternativa. Quando utilizar Web sites personalizados:  

-   Os Web sites personalizados estão ativados para todo o site em vez de para servidores do sistema de sites individuais ou funções.  

-   Nos sites primários, cada computador que irá alojar uma função do sistema de sites aplicável tem ser configurado com um Web site personalizado denominado **SMSWEB**. Até que criar neste Web site e configurar funções de sistema de sites nesse computador para utilizar o Web site personalizado, os clientes poderão não ser capazes de comunicar com funções de sistema de sites nesse computador.  

-   Uma vez que os sites secundários são automaticamente configurados para utilizar um Web site personalizado ao respetivo site principal primário está configurado para fazê-lo, também deve criar Web sites personalizados no IIS em cada servidor de sistema de sites secundários que requer o IIS.  


  **Pré-requisitos para utilizar Web sites personalizados:**  

 Antes de ativar a opção para utilizar Web sites personalizados num site, tem de:  

-   Criar um Web site personalizado denominado **SMSWEB** no IIS em cada servidor de sistema de sites que requer o IIS. Pode fazê-lo no site primário e em quaisquer sites secundários.  

-   Configure o Web site personalizado para responder à mesma porta que configurou para comunicação de cliente do Configuration Manager (porta de pedido do cliente).  

-   Para cada personalizada ou o Web site predefinido que utilize uma pasta personalizada, o local de tipo que utilizar na pasta raiz que aloja o site de documento de uma cópia da predefinida. Por exemplo, num computador Windows Server 2008 R2 com configurações predefinidas, **iisstart** é uma das predefinido vários tipos de documentos que estão disponíveis. Pode encontrar este ficheiro na raiz do Web site predefinido e, em seguida, coloque uma cópia deste ficheiro (ou uma cópia do tipo de documento predefinido que utilizar) na pasta raiz que aloja o site personalizado SMSWEB. Para mais informações sobre tipos de documentos predefinidos, consulte o artigo [documento predefinido &lt;defaultDocument\> do IIS](http://www.iis.net/configreference/system.webserver/defaultdocument).  

**Sobre os requisitos do IIS:**
**as seguintes funções de sistema de sites necessitam do IIS e um Web site para alojar os serviços de sistema de sites:**  

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

-   Quando um site primário tem os Web sites personalizados ativados, os clientes atribuídos a esse site são direcionados para comunicar com os Web sites personalizados em vez dos Web sites predefinido em servidores de sistema de sites aplicável  

-   Se utilizar Web sites personalizados para um site primário, considere os Web sites personalizados para todos os sites primários da hierarquia para garantir que os clientes podem com êxito se movem para dentro da hierarquia. (Roaming é quando move um computador cliente para um novo segmento de rede gerido por um site diferente. Roaming pode afetar a recursos que um cliente pode aceder localmente em vez de através de uma ligação WAN).  

-   Funções de sistema de sites que utilizam o IIS, mas não aceitam ligações de cliente, como o ponto do reporting services, também utilizam o Web site SMSWEB em vez do Web site predefinido.  

-   Os Web sites personalizados necessitam de atribuir números das portas que são diferentes dos que utiliza o Web site predefinido do computador. Um site predefinido e um site personalizado não podem ser executados em simultâneo se ambos tentarem utilizar as mesmas portas TCP/IP.  

-   As portas TCP/IP que configura no IIS para o Web site personalizado tem de corresponder ao portas de pedido do cliente para o site.  

## <a name="switch-between-default-and-custom-websites"></a>Alternar entre predefinidos e Web sites personalizados  
Embora possa verificar ou desmarque a caixa para utilizar Web sites personalizados num site primário em qualquer altura (a caixa é no separador Geral das propriedades do site), planeie cuidadosamente antes de efetuar esta alteração. Quando esta configuração for alterada, todas as funções de sistema de sites aplicável no site primário e os sites secundários subordinados tem de desinstalar e reinstalar:  

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

-   Quando alterar do Web site predefinido para utilizar um Web site personalizado, o Configuration Manager não remove os diretórios virtuais antigos. Se pretender remover os ficheiros utilizados pelo Configuration Manager, tem de eliminar manualmente os diretórios virtuais que foram criados no Web site predefinido.  

-   Se alterar o site para utilizar Web sites personalizados, os clientes que já estão atribuídos ao site, em seguida, devem ser reconfigurados para utilizar as novas portas de pedido de cliente para os Web sites personalizados. Consulte o artigo [como configurar as portas de comunicação de clientes no System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

## <a name="set-up-custom-websites"></a>Configurar os Web sites personalizados  
Uma vez que os passos para criar um site personalizado variam consoante as versões do sistema operativo, consulte a documentação da versão do seu sistema operativo para obter os passos exatos, mas utilize as seguintes informações quando for aplicável:  

-   O nome do Web site tem de ser: **SMSWEB**.  

-   Quando configurar o HTTPS, tem de especificar um certificado SSL antes de poder guardar a configuração.  

-   Depois de criar o Web site personalizado, remova as portas de Web site personalizado que utiliza a partir de outros Web sites no IIS:  

    1.  Editar o **enlaces** da outros Web sites a remover as portas que correspondam aos que estão atribuídas ao **SMSWEB** Web site.  

    2.  Iniciar o **SMSWEB** Web site.  

    3.  Reinicie o serviço **SMS_SITE_COMPONENT_MANAGER** no servidor do site.  


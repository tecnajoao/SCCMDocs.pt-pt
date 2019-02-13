---
title: Web sites para sistemas de sites
titleSuffix: Configuration Manager
description: Saiba mais sobre sites predefinidos e personalizados para servidores do sistema de sites no System Center Configuration Manager.
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fd2e358a93ff91c79f0f4716a596a9f7026c5daa
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123455"
---
# <a name="websites-for-site-system-servers-in-system-center-configuration-manager"></a>Sites para servidores do sistema de sites no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Várias funções de sistema de sites do Configuration Manager requerem a utilização do Microsoft Internet Information Services (IIS) e utilizam o site do IIS predefinido para alojar serviços do sistema de sites. Quando tem de executar outras aplicações web mesmo servidor e as definições não são compatíveis com o Configuration Manager, considere utilizar um Web site personalizado para o Configuration Manager.  

> [!TIP]  
>  Uma melhor prática de segurança é dedicar um servidor para os sistemas de sites do Configuration Manager que necessitem do IIS. Quando executa outras aplicações num Gestor de configuração do sistema de sites, aumenta a superfície de ataque desse computador.  




##  <a name="BKMK_What2Know"></a> O que deve saber antes de optar por utilizar sites personalizados  
 Por predefinição, as funções do sistema de sites utilizam o **Site Predefinido** no IIS. Este passo é configurado automaticamente quando instala a função de sistema de sites. No entanto, nos sites primários, pode optar por utilizar sites personalizados como alternativa. Quando utilizar Web sites personalizados:  

-   Web sites personalizados estão ativados para todo o site em vez de para servidores do sistema de sites individuais ou funções.  

-   Nos sites primários, cada computador que irá alojar uma função de sistema de sites aplicável tem de ser definido com um Web site personalizado denominado **SMSWEB**. Até que cria este Web site e configurar funções de sistema de sites nesse computador a utilizar o Web site personalizado, os clientes poderão não conseguir comunicar com funções de sistema de sites nesse computador.  

-   Uma vez que os sites secundários são automaticamente configurados para utilizar um Web site personalizado quando o site principal está configurado para fazê-lo, tem também de criar Web sites personalizados no IIS em cada servidor de sistema de sites secundários que requer o IIS.  


  **Pré-requisitos para utilizar sites personalizados:**  

 Antes de ativar a opção para utilizar Web sites personalizados num site, tem de:  

-   Criar um Web site personalizado denominado **SMSWEB** no IIS em cada servidor de sistema de sites que requer o IIS. Pode fazê-lo no site primário e em quaisquer sites secundários.  

-   Configure o Web site personalizado para responder à mesma porta que configurou para a comunicação de cliente do Configuration Manager (porta de pedido do cliente).  

-   Para cada personalizado ou Web site predefinido que utilize uma pasta personalizada, coloque uma cópia do padrão de documento tipo que utilizar na pasta raiz que aloja o site. Por exemplo, num computador Windows Server 2008 R2 com configurações predefinidas, **iisstart. htm** é um padrão de vários tipos de documentos que estão disponíveis. Pode encontrar este ficheiro na raiz do Web site predefinido e, em seguida, coloque uma cópia deste ficheiro (ou uma cópia do tipo de documento predefinido que utilizar) na pasta raiz que aloja o site personalizado smsweb. Para mais informações sobre tipos de documentos predefinidos, consulte [documento predefinido &lt;defaultDocument\> para IIS](http://www.iis.net/configreference/system.webserver/defaultdocument).  

**Sobre os requisitos do IIS:**
**as seguintes funções de sistema de sites requerem o IIS e um Web site para alojar os serviços do sistema de sites:**  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Ponto de Web site do Catálogo de Aplicações  

-   Ponto de distribuição  

-   Ponto de inscrição  

-   Ponto proxy de registo  

-   Ponto de estado de contingência  

-   Ponto de gestão  

-   Ponto de atualização de software  

-   Ponto de Migração de Estado  

Considerações adicionais:  

-   Quando um site primário tem sites personalizados ativados, os clientes que estão atribuídos a esse site são direcionados para comunicar com os sites personalizados em vez dos sites predefinidos em servidores do sistema de sites aplicáveis  

-   Se utilizar sites personalizados para um site primário, considere os Web sites personalizados para todos os sites primários da hierarquia para garantir que os clientes podem fazer roaming com êxito dentro da hierarquia. (Roaming é quando move um computador cliente para um novo segmento de rede gerido por um site diferente. O roaming pode afetar recursos que um cliente pode aceder localmente em vez de num link WAN).  

-   Funções de sistema de sites que utilizam o IIS, mas não os aceitar ligações de cliente, como o ponto do reporting services, também utilizam o site SMSWEB em vez do Web site predefinido.  

-   Web sites personalizados necessitam que atribua números de porta diferentes dos que utiliza o Web site predefinido do computador. Um site predefinido e um site personalizado não podem ser executados em simultâneo se ambos tentarem utilizar as mesmas portas TCP/IP.  

-   As portas TCP/IP que configurou no IIS para o Web site personalizado têm de corresponder as portas de pedido de cliente para o site.  

## <a name="switch-between-default-and-custom-websites"></a>Alternar entre sites predefinidos e personalizados  
Embora pode marcar ou desmarcar a caixa para utilizar sites personalizados num site primário em qualquer altura (a caixa está no separador Geral das propriedades do site), planeie cuidadosamente antes de efetuar esta alteração. Quando esta configuração é alterada, todas as funções de sistema de sites aplicáveis no site primário e em sites secundários subordinados necessário desinstalar e reinstalar:  

As seguintes funções **são reinstaladas automaticamente**:  

-   Ponto de gestão  

-   Ponto de distribuição  

-   Ponto de atualização de software  

-   Ponto de estado de contingência  

-   Ponto de Migração de Estado  

As seguintes funções têm de ser **reinstaladas manualmente**:  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Ponto de site do Catálogo de Aplicações  

-   Ponto de inscrição  

-   Ponto proxy de registo  

Além disso,  

-   Quando muda do Web site predefinido para utilizar um Web site personalizado, o Configuration Manager não remove os diretórios virtuais antigos. Se pretende remover os ficheiros que utilizados do Configuration Manager, tem de eliminar manualmente os diretórios virtuais que foram criados no Web site predefinido.  

-   Se alterar o site para utilizar sites personalizados, os clientes que já estão atribuídos ao site têm de ser reconfigurados para utilizar as novas portas de pedido de cliente para os sites personalizados. Ver [como configurar portas de comunicação de cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

## <a name="set-up-custom-websites"></a>Configurar sites personalizados  
Uma vez que os passos para criar um site personalizado variam consoante as versões do sistema operativo, consulte a documentação da versão do seu sistema operativo para obter os passos exatos, mas utilize as seguintes informações quando for aplicável:  

-   O nome do site tem de ser: **SMSWEB**.  

-   Quando configurar o HTTPS, tem de especificar um certificado SSL para poder guardar a configuração.  

-   Depois de criar o Web site personalizado, remova as portas do Web site personalizado que utiliza a partir de outros sites no IIS:  

    1.  Editar a **enlaces** dos outros sites para remover as portas que correspondem às atribuídas para o **SMSWEB** Web site.  

    2.  Iniciar o **SMSWEB** Web site.  

    3.  Reinicie o serviço **SMS_SITE_COMPONENT_MANAGER** no servidor do site.  

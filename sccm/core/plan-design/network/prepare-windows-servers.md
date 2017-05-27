---
title: Preparar servidores Windows | Documentos do Microsoft
description: "Certifique-se de que um computador cumpre os pré-requisitos para ser utilizado como um servidor de site ou um servidor de sistema de sites para o System Center Configuration Manager."
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dd102603356864add4084c6881c39bebcbd635f2
ms.openlocfilehash: 9b97dedb5d2be0bd2e47260033e6e4361467dc4e
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="prepare-windows-servers-to-support-system-center-configuration-manager"></a>Preparar Servidores do Windows para suportar o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de poder utilizar um computador com o Windows como um servidor de sistema de sites para o System Center Configuration Manager, o computador tem de cumprir os pré-requisitos para poder ser utilizado como um servidor do site ou servidor de sistema de sites que se destinam.  

-   Estes pré-requisitos, muitas vezes, incluem um ou mais funcionalidades do Windows ou funções, que são ativadas utilizando os Gestor de servidores de computadores.  

-   Uma vez que o método de ativar as funcionalidades do Windows e funções difere entre sistemas operativos, consulte a documentação para o seu sistema operativo para obter informações detalhadas sobre como configurar o sistema operativo que utilizar.  

As informações neste artigo fornecem uma descrição geral dos tipos de configurações do Windows que são necessários para suportar os sistemas de sites do Configuration Manager. Para obter detalhes de configuração para funções de sistema de sites específicas, consulte o artigo [Site e os pré-requisitos de sistema de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

##  <a name="BKMK_WinFeatures"></a>Funcionalidades do Windows e de funções  
 Ao configurar funcionalidades do Windows e funções num computador, poderá ser necessário reiniciar o computador para concluir que a configuração. Por conseguinte, é uma boa ideia para identificar os computadores que irão alojar funções de sistema de sites específicas antes de instalar um site do Configuration Manager ou o servidor do sistema de sites.
### <a name="features"></a>Funcionalidades  
 As seguintes funcionalidades do Windows são necessárias em determinados servidores de sistema de sites e devem ser definidas antes de instalar uma função de sistema de sites nesse computador.  

-   **.NET framework**: Incluindo  

    -   ASP.NET  
    -   Ativação HTTP  
    -   Ativação HTTP não  
    -   Serviços do Windows comunicação Foundation (WCF)  

    Funções do sistema de sites diferentes necessitam de versões diferentes do .NET Framework.  

    .NET Framework 4.0 e posterior não é compatível com versões anteriores para substituir as versões anteriores e 3,5, quando diferentes versões são listadas como necessárias, planear a ativação de cada versão no mesmo computador.  

-   **Serviços de transferência inteligente em segundo plano (BITS) em segundo plano**: Pontos de gestão necessitam de BITS (e automaticamente selecionadas opções) para suportar a comunicação com os dispositivos geridos.  

-   **BranchCache**: Pontos de distribuição podem ser configurados com o BranchCache para suportar clientes que utilizam o BranchCache.  

-   **Eliminação de dados duplicados**: Pontos de distribuição podem ser configurados com e beneficiam de eliminação de duplicados de dados.  

-   **Compressão de diferencial remota (RDC)**: Cada computador que aloja um servidor do site ou um ponto de distribuição requer RDC.   
    O RDC é utilizado para gerar assinaturas de pacote e efetuar comparações de assinaturas.  

### <a name="roles"></a>Funções  
 As seguintes funções do Windows são necessárias para suportar funcionalidades específicas, como atualizações de software e implementações do sistema operativo, enquanto o IIS é necessário para as funções do sistema de sites mais comuns.  

 -   **Serviço de inscrição de dispositivos de rede** (em serviços de certificados do Active Directory):  Esta função do Windows é um pré-requisito para utilizar perfis de certificado no Configuration Manager.  

 -   **Servidor Web (IIS)**: Incluindo:  
    -   Funcionalidades HTTP comuns >  
        -   Redirecionamento HTTP  
    -   Desenvolvimento de aplicações >  
        -   Extensibilidade .NET  
        -   ASP.NET  
        -   Extensões ISAPI  
        -   Filtros ISAPI  
    -   Ferramentas de gestão >  
        -   Compatibilidade de Gestão do IIS 6  
        -   Compatibilidade com Metabase do IIS 6  
        -   Compatibilidade do IIS 6 Windows Management Instrumentation (WMI)  
    -   Segurança >  
        -   Filtragem de Pedidos  
        -   Autenticação do Windows  

 As seguintes funções de sistema de sites utilizam um ou mais das configurações IIS listadas:  
    -   Ponto de serviço Web do Catálogo de Aplicações  
    -   Ponto de Web site do Catálogo de Aplicações  
    -   Ponto de distribuição  
    -   Ponto de inscrição  
    -   Ponto proxy de registo  
    -   Ponto de estado de contingência  
    -   Ponto de gestão  
    -   Ponto de atualização de Software  
    -   Ponto de migração de estado     

    A versão mínima do IIS necessária é a versão fornecida com o sistema operativo do servidor do site.  

    Além destas configurações de IIS, poderá ter de configurar o [IIS filtragem de pedidos para pontos de distribuição](#BKMK_IISFiltering).  

-   **Serviços de implementação do Windows**: Esta função é utilizada com a implementação do sistema operativo.  
-   **Windows Server Update Services**: Esta função é necessária quando irá implementar atualizações de software.  

##  <a name="BKMK_IISFiltering"></a>IIS filtragem de pedidos para pontos de distribuição  
 Por predefinição, IIS utiliza filtragem de pedidos para bloquear várias extensões de nome de ficheiros e localizações de pastas contra o acesso por comunicação HTTP ou HTTPS. Um ponto de distribuição, isto impede que os clientes a transferência de pacotes que tem bloqueado extensões ou localizações de pastas.  

 Quando os ficheiros de origem do pacote tiverem extensões bloqueadas no IIS pela sua configuração de filtragem de pedidos, tem de configurar filtragem de pedidos para permitir que os mesmos. Isto é efetuado ao [editar a Funcionalidade de Filtragem de Pedidos](https://technet.microsoft.com/library/hh831621.aspx) no Gestor do IIS nos computadores dos pontos de distribuição.  

 Além disso, as seguintes extensões de nome de ficheiro são utilizadas pelo Configuration Manager para pacotes e aplicações. Certifique-se de que as configurações de filtragem de pedidos não bloqueiam estas extensões de ficheiro:  

-   .PCK  
-   .PKG  
-   .STA  
-   .TAR  

Por exemplo, ficheiros de origem para uma implementação de software poderá incluir uma pasta denominada **bin** ou tem um ficheiro que tenha o **. mdb** extensão de nome de ficheiro.  

-   Por predefinição, a filtragem de pedidos no IIS bloqueia o acesso a estes elementos (**bin** está bloqueado como um segmento ocultas e **. mdb** está bloqueado como uma extensão de nome de ficheiro).  

-   Quando utiliza a configuração predefinida do IIS num ponto de distribuição, os clientes que utilizam o BITS não conseguem transferir esta implementação de software a partir do ponto de distribuição e indicam que estão a aguardar conteúdo.  

-   Para permitir que os clientes transferir este conteúdo, cada ponto de distribuição aplicável, edite **filtragem de pedidos** no Gestor dos IIS para permitir o acesso aos extensões de ficheiros e pastas que se encontrem nos pacotes e aplicações que implementar.  

> [!IMPORTANT]  
>  As edições ao Filtro de Pedidos podem aumentar a superfície de ataque do computador.  
>   
>  -   As edições efetuadas ao nível do servidor são aplicadas a todos os Web sites no servidor.  
> -   Aplicam as edições efetuadas a Web sites individuais para apenas esse Web site.  
>   
>  É a melhor prática de segurança executar o Configuration Manager no servidor web dedicado. Se tiver de executar outras aplicações no servidor web, utilize um Web site personalizado para o Configuration Manager. Para obter informações, veja [Sites para servidores do sistema de sites no System Center Configuration Manager](../../../core/plan-design/network/websites-for-site-system-servers.md).  

## <a name="http-verbs"></a>Verbos HTTP
**Pontos de gestão:** Para garantir que os clientes podem comunicar com um ponto de gestão, no servidor de ponto de gestão Certifique-se que os seguintes verbos HTTP são permitidos:  
 - GET
 - POST
 - CCM_POST
 - HEAD
 - PROPFIND

**Pontos de distribuição:** Pontos de distribuição requerem que os seguintes verbos HTTP como permitidos:
 - GET
 - HEAD
 - PROPFIND

Para obter informações sobre como configurar a filtragem de pedidos, consulte o artigo [configurar a filtragem de pedidos no IIS](https://technet.microsoft.com/library/hh831621.aspx#Verbs) no TechNet ou outra documentação que se aplica à versão do Windows Server que aloja o ponto de gestão.


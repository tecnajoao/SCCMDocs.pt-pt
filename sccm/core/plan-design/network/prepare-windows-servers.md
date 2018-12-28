---
title: Preparar servidores do Windows
titleSuffix: Configuration Manager
description: Certifique-se de que um computador cumpre os pré-requisitos para utilização como um servidor de site ou um servidor de sistema de sites do Configuration Manager.
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a531168aaedc67c1a403946374edb7b79273eb64
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53423852"
---
# <a name="prepare-windows-servers-to-support-configuration-manager"></a>Preparar Servidores do Windows para suportar o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de poder utilizar um computador Windows como um servidor de sistema de sites do Configuration Manager, o computador tem de cumprir os pré-requisitos para poder ser utilizado como um servidor do site ou servidor de sistema de sites.  

- Estes pré-requisitos, muitas vezes, incluem um ou mais recursos do Windows ou funções, que estão ativadas utilizando os Gestor de servidores de computadores.  

- Uma vez que o método para ativar funcionalidades do Windows e funções é diferente entre versões do sistema operacional, consulte a documentação para a sua versão de SO para obter informações detalhadas sobre como configurar o sistema operativo que utilizar.  

As informações neste artigo fornecem uma descrição geral dos tipos de configurações do Windows que são necessárias para oferecer suporte a sistemas de sites do Configuration Manager. Para obter detalhes de configuração para funções de sistema de sites específicas, consulte [Site e pré-requisitos de sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

##  <a name="BKMK_WinFeatures"></a> Funções e funcionalidades do Windows  
Quando configurar funcionalidades do Windows e funções num computador, poderá ser necessário reiniciar o computador para concluir essa configuração. Portanto, é uma boa idéia para identificar computadores que irão alojar funções do sistema de sites específicas antes de instalar um site do Configuration Manager ou o servidor de sistema de sites.

### <a name="features"></a>Funcionalidades  
As seguintes funcionalidades do Windows são necessárias em determinados servidores de sistema de sites e devem ser configuradas antes de instalar uma função de sistema de sites nesse computador.  

- **.NET framework**: Incluindo  

    - ASP.NET  
    - Ativação HTTP  
    - Ativação não HTTP  
    - Serviços do Windows Communication Foundation (WCF)  

    Funções de sistema de sites diferentes exigem diferentes versões do .NET Framework.  

    Como o .NET Framework 4.0 e posterior não é retrocompatível para substituir as versões 3.5 e anteriores, quando são listadas diferentes versões como necessário, planeie ativar cada versão no mesmo computador.  

- **Em segundo plano (BITS) de serviços de transferência inteligente**: Pontos de gestão requerem os BITS (e as opções selecionadas automaticamente) para suportar a comunicação com dispositivos geridos.  

- **BranchCache**: Pontos de distribuição podem ser configurados com o BranchCache para suportar clientes que utilizem o BranchCache.  

- **A eliminação de duplicados de dados**: Pontos de distribuição podem ser configurados com e beneficiam da eliminação de duplicados de dados.  

- **Compressão de diferencial remota (RDC)**: Cada computador que aloja um servidor de site ou um ponto de distribuição requer RDC. O RDC é utilizado para gerar assinaturas de pacote e efetuar comparações de assinaturas.  

### <a name="roles"></a>Funções  
As seguintes funções do Windows são necessárias para suportar funcionalidades específicas, como atualizações de software e implementações de sistema operacional, enquanto o IIS é necessário para as funções de sistema de sites mais comuns.  

- **Serviço de inscrição de dispositivos de rede** (em serviços de certificados do Active Directory): Esta função do Windows é um pré-requisito para utilizar perfis de certificado no Configuration Manager.  

- **Servidor Web (IIS)**: Incluindo:  
    - Funcionalidades HTTP Comuns  
          - Redirecionamento HTTP  
    - Programação de Aplicações  
          - Extensibilidade .NET  
          - ASP.NET  
          - Extensões ISAPI  
          - Filtros ISAPI  
    - Ferramentas de Gestão  
          - Compatibilidade de Gestão do IIS 6  
          - Compatibilidade com Metabase do IIS 6  
          - Compatibilidade do IIS 6 Windows Management Instrumentation (WMI)  
    - Segurança  
          - Filtragem de Pedidos  
          - Autenticação do Windows  

  As seguintes funções de sistema de sites utilizam um ou mais das configurações do IIS listadas:  
  - Ponto de serviço Web do Catálogo de Aplicações  
  - Ponto de Web site do Catálogo de Aplicações  
  - Ponto de distribuição  
  - Ponto de inscrição  
  - Ponto proxy de registo  
  - Ponto de estado de contingência  
  - Ponto de gestão  
  - Ponto de atualização de software  
  - Ponto de Migração de Estado     

  A versão mínima do IIS necessária é a versão fornecida com o sistema operativo do servidor do site.  

  Além destas configurações de IIS, poderá ter de configurar [IIS Request Filtering para pontos de distribuição](#BKMK_IISFiltering).  

- **Serviços de implantação do Windows**: Esta função é utilizada na implementação do SO.  

- **Windows Server Update Services**: Esta função é necessária para as atualizações de software.  


##  <a name="BKMK_IISFiltering"></a> Filtragem de pontos de distribuição de pedidos do IIS  
Por predefinição, o IIS utiliza a filtragem de pedidos para bloquear várias extensões de nomes de ficheiros e localizações de pastas contra o acesso por comunicação HTTP ou HTTPS. Num ponto de distribuição, isto impede que os clientes de transferirem pacotes com tem bloqueado extensões ou localizações de pastas.  

Quando os ficheiros de origem do pacote tiverem extensões bloqueadas no IIS pela sua configuração de filtragem de pedidos, tem de configurar a filtragem de pedidos para permitir que os mesmos. Isso é feito pela [edição a filtragem de pedidos de funcionalidades](https://technet.microsoft.com/library/hh831621.aspx) computadores do ponto no Gerenciador do IIS na sua distribuição.  

Além disso, as seguintes extensões de nome de ficheiro são utilizadas pelo Configuration Manager para pacotes e aplicações. Certifique-se de que o pedido de configurações de filtragem não bloqueiam estes itens extensões de ficheiros:  

- .PCK  
- .PKG  
- .STA  
- .TAR  

Por exemplo, arquivos de origem para uma implementação de software pode incluir uma pasta denominada **bin** ou um ficheiro que tem de ter o **. mdb** extensão de nome de ficheiro.  

- Por predefinição, filtragem bloqueia o acesso a estes elementos de pedidos do IIS (**bin** está bloqueado como um segmento oculto e **. mdb** está bloqueado como uma extensão de nome de ficheiro).  

- Quando utiliza a configuração predefinida do IIS num ponto de distribuição, os clientes que utilizam o BITS não conseguem transferir esta implementação de software a partir do ponto de distribuição e indicam que está a aguardar conteúdo.  

- Para permitir que os clientes transferir este conteúdo, em cada ponto de distribuição aplicável, edite **filtragem de pedidos** no Gestor do IIS para permitir o acesso às extensões de ficheiros e pastas que estão em pacotes e aplicações que implementar.  

> [!IMPORTANT]  
> As edições ao filtro de solicitação podem aumentar a superfície de ataque do computador.  
> 
> - As edições efetuadas ao nível do servidor se aplicam a todos os Web sites no servidor.   
>     - As edições efetuadas a Web sites individuais aplicam-se apenas esse site.  
> 
> É a melhor prática de segurança executar o Configuration Manager no servidor web dedicado. Se tiver de executar outras aplicações no servidor web, utilize um Web site personalizado para o Configuration Manager. Para obter informações, consulte [sites para servidores de sistema de sites](/sccm/core/plan-design/network/websites-for-site-system-servers).  

## <a name="http-verbs"></a>Verbos HTTP
**Pontos de gestão:** Para garantir que os clientes podem comunicar com um ponto de gestão, no servidor de ponto de gestão, verifique se que os seguintes verbos HTTP são permitidos:  
- GET
- POST
- CCM_POST
- HEAD
- PROPFIND

**Pontos de distribuição:** Pontos de distribuição requerem que os seguintes verbos HTTP como permissão:
- GET
- HEAD
- PROPFIND

Para obter mais informações, consulte [configurar filtragem de pedidos no IIS](https://technet.microsoft.com/library/hh831621.aspx#Verbs). 

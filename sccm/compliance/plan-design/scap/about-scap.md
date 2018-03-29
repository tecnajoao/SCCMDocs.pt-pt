---
title: Sobre as extensões Security Content Automation Protocol (SCAP)
titleSuffix: System Center Configuration Manager
description: Saiba mais sobre as extensões Security Content Automation Protocol (SCAP)
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
caps.latest.revision: ''
caps.handback.revision: ''
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: fc986e2175583124377ccb7c080df4b219ea8df0
ms.sourcegitcommit: 27da4be015f1496b7b89ebddb517a2685f1ecf74
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/28/2018
---
# <a name="about-the-security-content-automation-protocol-scap-extensions"></a>Sobre as extensões Security Content Automation Protocol (SCAP)

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

> [!Tip]  
> Esta funcionalidade foi introduzida pela primeira vez na versão de pré-visualização técnica 1803 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Esta versão de pré-lançamento das extensões SCAP pode ser instalado em quaisquer versões atualmente suportadas do ramo atual do Configuration Manager e LTSB 1606. O ficheiro de instalação está localizado em cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi a partir de pré-visualização técnica 1803. 

As extensões SCAP para o Microsoft System Center Configuration Manager ajuda a analisar e avaliar o seu ambiente de rede para compatibilidade com o SCAP Security Content Automation Protocol (). SCAP é definido e mantido pelos E.U.A. National Institute of Standards and Technology (NIST).

As extensões SCAP para o Microsoft System Center Configuration Manager utilizar a funcionalidade de definições de compatibilidade no Microsoft System Center Configuration Manager para analisar os computadores no seu ambiente e, em seguida, documentar o nível de compatibilidade com o Unidos Mandato Estados Government Configuration da linha de base USGCB ().

As extensões permitem que o Configuration Manager consuma fluxos de dados Security Content Automation Protocol (SCAP), avaliar a compatibilidade dos sistemas e gerar resultados do relatório no formato SCAP. A organização pode utilizar a infraestrutura existente do Configuration Manager para ajudar a garantir a computadores que gere cumpram este requisito de compatibilidade federal e geram o relatório usgcb do National Institute of Standards e Technology (NIST) e E.U.A. Office de gestão e do orçamento (OMB).

Este guia fornece informações para ajudar a instalar, configurar e executar as extensões SCAP na sua infraestrutura do System Center Configuration Manager.



# <a name="what39s-new-in-scap-extensions-prerelease-for-microsoft-system-center-configuration-manager"></a>O que&#39;s no pré-lançamento de extensões SCAP para o Microsoft System Center Configuration Manager

Utilize esta secção para saber mais sobre os&#39;s novo na versão mais recente.

Pré-lançamento de extensões SCAP para o System Center Configuration Manager:

- Inclui uma extensão de consola do Configuration Manager completamente suporta a conversão de conteúdo SCAP linhas de base de definições de compatibilidade para o ramo atual do System Center Configuration Manager
- Suporta a versão 1.2 do SCAP e é retrocompatível com as versões 1.1 e 1.0 do SCAP.


  - Suporta Extensible Configuration lista de verificação descrição formato (XCCDF) versão 1.2.
  - Suporta as versões de Open Vulnerability and Assessment Language (OVAL), até à versão 5.10.
  - Suporta a geração de relatórios do Asset Reporting formato (ARF) 1.1.
  - Enumeração de plataforma comum suporta (CPE) 2.3
  - Suporta CVE (Exposures) e vulnerabilidades comuns
  - Suporta comuns configuração enumeração CCE () versão 5
  - Suporta USGCB Internet Explorer 8, Windows 7 e Firewall do Windows 7 USGCB.

- Inclui um Assistente de IU para importar SCAP 1.2/1.1/1.0 e OVAL conteúdo para a conversão para linhas de base de configuração.


  - Permite a seleção de fluxos de dados de origem SCAP e benchmarks e perfis XCCDF para conversão.

- Inclui um Assistente de IU para exportar o resultado da avaliação de configuração para o formato SCAP relatório XML


  - Apresenta o ficheiro de origem, fluxo de dados SCAP, XCCDF Benchmark e perfil XCCDF utilizado para gerar a linha de base.
  - Suporta a gerar o relatório Cyberscope Lightweight Asset resumo resultados (LASR).

- Suporta a criação de relatórios SCAP com base na implementação de linha de base de configuração. Inclui um novo dashboard para visualizar a conformidade do cliente, bem como compatibilidade de regra de XCCDF. O dashboard suporta desagregação através de relatórios onde pode pesquisar o mais detalhadas e de filtro.
- Melhora o desempenho de vários tipos de que itens de configuração convertidos a partir de testes OVAL, permitindo a avaliação mais rápida.

- Correções vários problemas encontrados no conteúdo do Windows 10 Desa v1r3.

# <a name="scap-extensions-for-microsoft-system-center-configuration-manager-deployment-process"></a>Extensões SCAP para o processo de implementação do Microsoft System Center Configuration Manager

Este guia descreve como analisar, avaliar e relatórios sobre compatibilidade SCAP ao utilizar as extensões SCAP para o Microsoft System Center Configuration Manager. Aqui&#39;s um breve resumo dos procedimentos&#39;odas seguir:

- Prepare a infraestrutura de pré-requisito para tirar partido das extensões.
- Instalar e configurar as extensões SCAP para o Microsoft System Center Configuration Manager.
- Transferir, instalar e configurar os ficheiros de fluxo de dados SCAP do [base de dados de vulnerabilidades nacional de normalização](http://nvd.nist.gov) (NVD).
- Converter e importar os ficheiros de fluxo de dados SCAP diretamente para uma linha de base para os definições de compatibilidade do System Center Configuration Manager, que se utilizando o Assistente Importar **ou** através de um ficheiro CAB (. cab) através da linha de comandos Ferramenta de Microsoft.Sces.ScapToDcm.exe.
- Exporte resultados de compatibilidade para o formato SCAP, utilizando o Assistente Exportar ou a ferramenta de Microsoft.Sces.DcmToScap.exe da linha de comandos.

# <a name="terms"></a>Termos de licenciamento

**ID DO OVAL:** Um identificador de uma definição OVAL específico que está em conformidade com o formato para os IDs de OVAL.

**Fluxo de dados do SCAP resultado:** Um grupo de componentes do SCAP, juntamente com os mapeamentos de referências entre os componentes do SCAP, que contêm conteúdo de saída (resultado).

**Fluxo de dados de origem SCAP:** Um grupo de componentes do SCAP, juntamente com os mapeamentos de referências entre os componentes do SCAP, que contêm conteúdo de entrada (origem).

# <a name="prepare-the-prerequisite-infrastructure"></a>Preparar a infraestrutura de pré-requisito

Certifique-se de que os seguintes requisitos de software e hardware são cumpridos para tirar partido das extensões SCAP para o Microsoft System Center Configuration Manager.

## <a name="software-requirements"></a>Requisitos de Software

Para instalar, configurar e executar as extensões SCAP para o Microsoft System Center Configuration Manager, necessita de um computador com o seguinte software:

- A [versão suportada](/sccm/core/servers/manage/current-branch-versions-supported) da consola de ramo atual do System Center Configuration Manager.
- Um sistema operativo compatível com a consola do System Center Configuration Manager. Para obter uma lista dos sistemas de operativos compatíveis, consulte o [sistemas operativos suportados para consolas do System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles) artigo.

Para além do computador com as extensões SCAP, também terá dos seguintes itens:

- Uma infraestrutura ramo atual do System Center Configuration Manager. Para obter mais informações sobre os requisitos para uma implementação do Configuration Manager, consulte o [configurações suportadas para o Configuration Manager](/sccm/core/plan-design/configs/supported-configurations) artigo.

Os computadores que pretende avaliar para compatibilidade SCAP tem o software e configurações seguintes:

- O componente de gestão de definições de compatibilidade e ativado no cliente do Configuration Manager.
- Windows PowerShell 2.0 ou superior.
- A política de execução do PowerShell do Gestor de configuração definida como **ignorar**. Para obter mais informações, consulte o [política de execução do PowerShell](/sccm/core/clients/deploy/about-client-settings#computer-agent) artigo.
- Um dos seguintes sistemas operativos
  - Versão de lançamento do Windows 7 ou Sp1, 32 bits ou 64 bits
  - Windows 10, 32 bits ou 64 bits
  - Windows Server 2012 R2

## <a name="hardware-requirements"></a>Requisitos de Hardware

Os requisitos mínimos do sistema são fornecidos aqui:

[Planear configurações de Hardware para o Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware)



## <a name="accessibility-features"></a>Funcionalidades de acessibilidade

As extensões SCAP para o System Center Configuration Manager incluem ferramentas de linha de comandos do Windows que podem tirar partido das funcionalidades de acessibilidade e ferramentas no Windows.

- Os parâmetros da linha de comandos são documentados neste guia de utilizador para Microsoft.Sces.ScapToDcm.exe e Microsoft.Sces.DcmToScap.exe.
- -ajudar e -? irá imprimir a utilização da ferramenta para o ecrã onde estarão disponível para leitores de ecrã e outra tecnologia de apoio.
- Windows [acessibilidade](http://windows.microsoft.com/windows/help/accessibility)

As extensões SCAP também facilitam a utilização de funcionalidades no System Center Configuration Manager.  O Configuration Manager inclui funcionalidades que tornam o produto mais acessível para pessoas com incapacidades.

- [Funcionalidades de acessibilidade no System Center Configuration Manager](/sccm/core/understand/accessibility-features)

Para obter informações gerais sobre os serviços e produtos de acessibilidade da Microsoft, visite o [Web site da Microsoft Accessibility](http://go.microsoft.com/fwlink/p/?LinkId=9212).

## <a name="next-step"></a>Passo seguinte
> [!div class="nextstepaction"]
> [Instalar e configurar as extensões SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)

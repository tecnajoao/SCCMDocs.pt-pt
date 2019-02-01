---
title: Extensões SCAP
titleSuffix: Configuration Manager
description: Saiba mais sobre as extensões Security Content Automation Protocol (SCAP) para o Configuration Manager.
ms.date: 01/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e42027663f06bff715cb7e9087ececbc421cc495
ms.sourcegitcommit: 013ca76d5a3c07306de7b5bfd985b0289d1be599
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/31/2019
ms.locfileid: "55482457"
---
# <a name="about-the-security-content-automation-protocol-scap-extensions"></a>Acerca das extensões Security Content Automation Protocol (SCAP)

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As extensões SCAP para o Configuration Manager ajudam a analisar e avaliar o seu ambiente de rede para conformidade com o SCAP Security Content Automation Protocol (). SCAP é definido e mantido pelo National Institute of Standards and Technology (NIST). Para obter mais informações, consulte a [visão geral do projeto SCAP](https://csrc.nist.gov/projects/security-content-automation-protocol).

> [!Note]  
> Esta versão da ferramenta é uma funcionalidade de pré-lançamento que só está disponível na versão 1806. Esta versão não é certificada pela NIST. <!--SCCMDocs-pr issue 3323-->
> 
> Se exigir uma ferramenta de certificados, ou se estiver a utilizar outra versão do Configuration Manager current branch, utilize a seguinte versão das extensões SCAP:
> - [Transferir as extensões SCAP para o System Center Configuration Manager](https://www.microsoft.com/download/details.aspx?id=48741)
> - [Documentação para extensões SCAP versão 3.0](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/mt228311\(v%3dtechnet.10\))

As extensões SCAP para o Configuration Manager utilizam a funcionalidade de definições de conformidade para primeiro analisar os computadores no seu ambiente. Ele documenta, em seguida, o nível de compatibilidade com os Estados Unidos Government configuração da linha de base (USGCB).

As extensões permitem que o Configuration Manager consuma fluxos de dados SCAP, avaliar a sistemas de conformidade e gerar resultados do relatório no formato SCAP. Sua organização pode utilizar a sua infraestrutura existente do Configuration Manager para ajudar a garantir a computadores que gere cumprem este requisito de compatibilidade federal. Também utilize o Gestor de configuração para gerar os relatórios USGCB exigidos pelo NIST e como o Office de gerenciamento e orçamento (OMB).

Este artigo fornece informações para ajudar a instalar, configurar e executar as extensões SCAP na sua infraestrutura do Configuration Manager.



## <a name="whats-new"></a>Novidades

Esta versão das extensões de SCEP para o Configuration Manager inclui e suporta as seguintes funcionalidades:  

- Uma extensão da consola do Configuration Manager, que suporta a conversão de conteúdo de SCAP às linhas de base de definições de conformidade.  

- SCAP versão 1.2, o que inclui os seguintes componentes:  

  - Extensível configuração lista de verificação descrição do formato XCCDF () versão 1.2
  - Abra as versões de vulnerabilidade e a avaliação de idioma (OVAL) até à versão 5.10
  - geração de relatórios do Asset Reporting formato (ARF) 1.1
  - Common Platform Enumeration (CPE) 2.3
  - Comuns vulnerabilidades e exposições (CVE)
  - Enumeração de configuração comum (CCE) versão 5
  - USGCB Internet Explorer 8, o USGCB Windows 7 e o Firewall do Windows 7 USGCB  

- Compatível com as versões 1.1 e 1.0 do SCAP.  

- Um Assistente de consola para importar SCAP 1.2/1.1/1.0 e OVAL conteúdo para a conversão para linhas de base de configuração.  

  - Permite a seleção de fluxos de dados de origem SCAP e benchmarks e perfis XCCDF para conversão.

- Um Assistente de consola para exportar o resultado da avaliação de configuração para o relatório SCAP formatada XML.  

  - Apresenta o ficheiro de origem, o fluxo de dados SCAP, o XCCDF benchmark e o perfil XCCDF utilizado para gerar a linha de base.
  - Gere o relatório Cyberscope Lightweight Asset resumo resultados de relatórios LARS ().  

- Gerar SCAP relatórios com base na implementação de linha de base de configuração. Este componente inclui um novo dashboard para visualizar a conformidade do cliente, bem como a conformidade de regra XCCDF. O dashboard oferece suporte a desagregar para relatórios, onde pode procurar e filtrar mais detalhadas.  

- Desempenho melhorado de vários tipos de itens de configuração convertido de testes OVAL, que permite a avaliação mais rápida.  

- Corrige vários problemas encontrados no conteúdo do Windows 10 DISA v1r3.  



## <a name="terms"></a>Termos

- **OVAL ID**: Um identificador para uma definição OVAL específico que está em conformidade com o formato para os IDs de OVAL.  

- **Fluxo de dados de resultado do SCAP**: Um pacote de componentes do SCAP, juntamente com os mapeamentos de referências entre os componentes do SCAP, que contêm conteúdo de saída (resultado).  

- **Fluxo de dados de origem SCAP**: Um pacote de componentes do SCAP, juntamente com os mapeamentos de referências entre os componentes do SCAP, que contêm conteúdo de entrada (origem).



## <a name="deployment-process"></a>Processo de implantação

Aqui está um resumo do processo geral de implantação:  

- [Preparar a infraestrutura](#bkmk_prepare) de utilizar as extensões  

- [Instalar e configurar as extensões SCAP](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_install) para o Configuration Manager  

- [Transferir e instalar os ficheiros de fluxo de dados SCAP](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_scap-data-stream-files) do NIST  

- Converter e importar os ficheiros de fluxo de dados SCAP numa linha de base de definições de compatibilidade do Configuration Manager. Utilize um dos dois métodos seguintes:   

    - [Processo manual](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import) utilizando o Assistente de importação na consola do Configuration Manager  

    - [Processo de](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_auto-convert-and-import) com a ferramenta de linha de comando Microsoft.Sces.ScapToDcm.exe  

- [Implementar](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_deploy) linhas de base de configuração para coleções  

- [Monitor](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_monitor) os dados de conformidade  

- Exporte resultados de compatibilidade para o formato SCAP, através de um dos dois métodos seguintes:  

    - [Processo manual](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_export) utilizando o Assistente de exportação na consola do  

    - [Processo de](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_auto-export) usando a ferramenta de linha de comando Microsoft.Sces.DcmToScap.exe  



## <a name="bkmk_prepare"></a> Preparar a infraestrutura

### <a name="software-requirements"></a>Requisitos de software

Para instalar, configurar e executar as extensões SCAP para o Configuration Manager, precisa de um computador com o seguinte software:

- R [uma versão suportada](/sccm/core/servers/manage/current-branch-versions-supported) da consola de ramo atual do Configuration Manager.  

- Uma versão de sistema operacional compatível com a consola do Configuration Manager. Para obter mais informações, consulte [sistemas operativos suportados por consolas do Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).  

Para além do computador com as extensões SCAP, também terá dos seguintes itens:

- Uma infraestrutura ramo atual do Configuration Manager. Para obter mais informações sobre os requisitos para uma implementação do Configuration Manager, consulte a [configurações suportadas para o Configuration Manager](/sccm/core/plan-design/configs/supported-configurations) artigo.  

Os computadores que pretende avaliar para compatibilidade SCAP precisam do software e configurações seguintes:

- O cliente do Configuration Manager.  

- Windows PowerShell 2.0 ou superior.  

- A política de execução do PowerShell do Gestor de configuração definida como **ignorar**. Para obter mais informações, consulte a [política de execução do PowerShell](/sccm/core/clients/deploy/about-client-settings#computer-agent) artigo.  

- Um dos seguintes sistemas operativos:  
  - O Windows 7 SP1, 32 bits ou 64 bits
  - Windows 10, 32 bits ou 64 bits
  - Windows Server 2012 R2

### <a name="hardware-requirements"></a>Requisitos de Hardware

Para obter mais informações sobre os requisitos mínimos do sistema do Configuration Manager, consulte [planear configurações de hardware para o Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware).



## <a name="accessibility-features"></a>Funcionalidades de acessibilidade

As extensões SCAP para o Configuration Manager incluem ferramentas da linha de comandos do Windows. Essas ferramentas podem tirar partido das funcionalidades de acessibilidade e ferramentas no Windows.

- Parâmetros da linha de comandos são documentados para Microsoft.Sces.ScapToDcm.exe e Microsoft.Sces.DcmToScap.exe. Para obter mais informações, consulte [Microsoft.Sces.ScapToDcm.exe. Parâmetros da linha de comandos](/sccm/compliance/plan-design/scap/install-configure-scap#microsoftscesscaptodcmexe-command-line-parameters) e [parâmetros de linha de comando Microsoft.Sces.DcmToScap.exe](/sccm/compliance/plan-design/scap/import-scap-compliance-settings#microsoftscesdcmtoscapexe-command-line-parameters).  

- Os parâmetros da linha de comandos `-help` e `-?` para cada ferramenta imprimir a utilização na tela. Estes detalhes de utilização, em seguida, estão disponíveis para os leitores de ecrã e outra tecnologia de apoio.  

- Para obter mais informações, consulte [acessibilidade do Windows](http://windows.microsoft.com/windows/help/accessibility).

As extensões SCAP Certifique-se também utilizar funcionalidades de acessibilidade no Configuration Manager. Para obter mais informações, consulte [funcionalidades de acessibilidade no Configuration Manager](/sccm/core/understand/accessibility-features).

Para obter mais informações sobre os serviços e produtos de acessibilidade da Microsoft, consulte a [Web site da Microsoft Accessibility](http://go.microsoft.com/fwlink/p/?LinkId=9212).



## <a name="next-step"></a>Passo seguinte
> [!div class="nextstepaction"]
> [Instalar e configurar as extensões do SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)

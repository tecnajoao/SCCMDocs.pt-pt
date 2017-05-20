---
title: "Dados de diagnóstico para 1602 | Documentos do Microsoft"
description: "Saiba mais sobre os níveis de diagnóstico e dados de utilização que o System Center Configuration Manager versão 1602 recolhe."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1210a1ca-78c7-4d17-81cf-ac1bc5c5cf3e
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 3e50327678d29fa2c1fed4ac0fd63738e65776cb
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1602-of-system-center-configuration-manager"></a>Níveis de recolha de dados de diagnóstico de utilização para a versão 1602 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager versão 1602 recolhe três níveis de diagnóstico e dados de utilização: **Básicas**, **avançada**, e **completa**. Por predefinição, esta funcionalidade está definida no nível Avançado. As secções seguintes fornecem detalhes adicionais sobre os dados que recolhe de cada nível.

Alterações de versões anteriores são descritas com ***[novo]*** ou ***[atualizado]***.

> [!IMPORTANT]
>  O Configuration Manager não recolher códigos de site, os nomes de sites, endereços IP, nomes de utilizador, nomes de computador, os endereços físicos ou endereços de correio eletrónico nos níveis de nível básico ou avançado. Qualquer coleção destas informações no nível completo não é purposeful, isto é, potencialmente incluído na informação de diagnóstico avançada, como ficheiros de registo ou instantâneos de memória. Microsoft não irá utilizar estas informações para identificar, contactar ou desenvolver publicidade.

##  <a name="bkmk_change"></a> Como alterar o nível
 Os administradores que têm um âmbito de administração baseada em funções que inclui **modificar** permissões a **Site** classe de objeto pode alterar o nível de dados recolhidos nas definições de diagnóstico e dados de utilização na consola do Configuration Manager.


  Para tal, na consola, aceda ao separador da vista backstage (no canto superior esquerdo separador com a seta de lista pendente), selecione **dados de utilização**e, em seguida, selecione o nível de dados que pretende utilizar.  

##  <a name="bkmk_level1"></a> Nível 1 - Básico
 O nível básico inclui dados sobre a sua hierarquia, os dados que seja necessário para o ajudar a melhorar a sua instalação ou atualização experiência e os dados que ajuda a determinar as atualizações do Configuration Manager que são aplicáveis para a sua hierarquia.

 Iniciar com o System Center Configuration Manager versão 1602, este nível inclui o seguinte:


 -   Informações de configuração:
     - Criar, instalar o tipo, pacotes de idiomas, funcionalidades que ativou a  

     - ***[Atualizado] *** Atualizar estado de implementação de pacote e erros, o progresso da transferência e erros de pré-requisitos     

     - ***[Novo] *** Versão do script pós-atualização

     - ***[Novo] *** Utilização tocarem rápida de atualização

-   Métricas de desempenho de base de dados (replicação processamento informações, superior procedimentos armazenados do SQL Server por processador e a utilização de disco)

-   Configuração de base de dados básica (processadores, configuração do cluster e configuração das vistas distribuídas)

-   Esquema de base de dados do Configuration Manager (hash de todas as definições de objetos)

-   Versões de cliente de contagem do Configuration Manager e versões do sistema operativo

-   Contagem de sistemas operativos para dispositivos geridos e políticas definidas pelo conector do Exchange

-   Contagem de idiomas de cliente e regiões

-   Contagem de dispositivos Windows 10 por ramo e compilação

-   Básicas do Configuration Manager hierarquia dados do site (lista de site, tipo, versão, o estado, contagem de clientes e fuso horário)

-   Informações do servidor de sistema básico de site (funções de sistema de sites utilizadas, estado de Internet e o SSL, sistema operativo, processadores e máquina física ou virtual)

-   Estatísticas de deteção de utilizador básica (utilizador deteção contagem de máximo/mínimo/média grupo tamanho e)

-   Informações básicas Endpoint protection (proteção contra software maligno versões de cliente)

-   Tipo de aplicação e implementação básico conta (aplicações total, aplicações total com vários tipos de implementação, aplicações total com dependências, total substituídas aplicações e contagem de tecnologias de implementação em utilização)

-   Implementação básica sistema operativo (OSD) conta (imagens)

-   Ponto de distribuição e ponto de gestão tipos e informações de configuração básica (protegidos, pré-configurado, PXE, multicast estado SSL, pontos de distribuição de solicitação/ponto a ponto, ativada de MDM, preparados para SSL, etc.)

-   Estatísticas de telemetria (quando executadas, tempo de execução e erros)

- ***[Novo] *** Configurado ao nível de telemetria, de modo (online ou offline) e configuração de atualização rápida

- ***[Novo] *** Utilização da deteção de rede (ativado ou desativado)
- ***[Novo] *** Consola de administração:

    -  Estatísticas sobre ligações de consolas (versão do sistema opeating, idioma, SKU e arquitetura, memória do sistema, contagem de processadores lógicos, ligar o ID do site, versões instaladas do .NET e pacotes de idiomas da consola)

##  <a name="bkmk_level2"></a> Nível 2 - Avançado
O nível de avançado é a predefinição após a conclusão da configuração. Este nível inclui dados que são recolhidos no nível básico, dados específicos da funcionalidade (frequência e duração de utilização), as definições de cliente do Configuration Manager (nome do componente, estado e determinadas definições como intervalos de consulta) e informações básicas sobre as atualizações de software.

Este nível é recomendado porque proporciona Microsoft com os dados mínimos necessário para melhorar o útil em futuras versões dos produtos e serviços. Este nível nomes de objetos não recolher (sites, os utilizadores, computadores ou objetos), os detalhes sobre objetos relacionados com a segurança ou vulnerabilidades, como contagens dos sistemas que necessitam de atualizações de software.

Iniciar com o System Center Configuration Manager versão 1602, este nível inclui o seguinte:

-   **Gestão de aplicações:**

  -   ***[Atualizado] *** Informações de utilização/filtragem básica para tipos de implementação que são utilizados na organização (utilizador em comparação com o dispositivo de destino, necessário versus aplicações disponíveis e universais)  

  -  ***[Atualizado] *** Informações de implementação de aplicação (instalar/desinstalar, necessita de aprovação, interação do utilizador ativado/desativado, dependências e substituições)  

  -   Estatísticas de pedidos de aplicação disponíveis  

  -   Contagem de pacotes por tipo  

  -   Contagem de aplicabilidade de aplicações por sistema operativo  

  -   Contagem de implementações de pacote/programa  

  -   Contagem de ambientes de App-V e propriedades de implementação  

  -   Contagem de licenças de aplicação licenciadas para Windows 10  

  -   ***[Atualizado] *** Número de máximo/mínimo/média de implementações de aplicações por utilizador/dispositivo por período de tempo

  -   Tipo e duração da janela de manutenção  

  -  ***[Novo] *** Estatísticas de tamanho e complexidade da política aplicação

-   **Cliente:**

    -   Lista/contagem de agentes de cliente ativados

    -   Contagem de instalações de cliente a partir de cada tipo de localização de origem

    -   Contagem de falhas de instalação de cliente

-   **Definições de compatibilidade:**

    -   Contagem de itens de configuração por tipo

    -   Informações básicas de linha de base de configuração (contagem, número de implementações e número de referências)

    -   Contagem de implementações que referenciam definições incorporadas (o valor de definição não é capturado)

    -   Contagem de regras e implementações criadas para definições personalizadas

    -   ***[Atualizado] *** Contagem dos modelos de Simple Certificate Enrollment Protocol, VPN, Wi-Fi, o certificado (. pfx) e política de conformidade implementadas   

    -  ***[Novo] *** Certificado de contagem de SCEP Simple Certificate Enrollment Protocol (), VPN, Wi-Fi, o certificado (. pfx) e implementações de política de conformidade por plataforma

-   **Conteúdo:**

    -   Contagem de limites por tipo

    -   Informações sobre grupos de limites (contagem de limites e sistemas de sites que estão atribuídos a cada grupo de limites)

    -   Informações do grupo de ponto de distribuição (contagem de pacotes e os pontos de distribuição que estão atribuídos a cada grupo de pontos de distribuição)

    -   Informações de configuração de ponto de distribuição (utilize da cache do ramo e monitorização do ponto de distribuição)

    -   Informações de configuração do Gestor de distribuição (threads, intervalo entre repetições, número de tentativas e as definições do ponto de distribuição de extração)

-   **Endpoint Protection:**

    -   Antimalware do Endpoint Protection e a utilização de política de Firewall do Windows (número de políticas exclusivos atribuído ao grupo)<br /><br />Isto não incluir quaisquer informações sobre as definições que estão incluídas na política.

    -   Erros de implementação do Endpoint Protection (contagem de códigos de erro de implementação do Endpoint Protection política)

    -   Contagem de coleções que estão selecionadas apareça no dashboard do endpoint protection

    -   Contagem de alertas que estão configurados para a funcionalidade Endpoint Protection

-   **Gestão de aplicações móveis (MAM):**

    -   Contagem de aplicações do Office preparados para MAM, aplicações de linha de negócio e políticas pelo sistema operativo

    -   Contagem de implementações de aplicações/política de MAM

    -   Contagem de regras que são criados por definição de MAM

-   **Gestão de dispositivos móveis (MDM):**

    -   Contagem de emitido ações do dispositivo móvel: bloquear, afixe colocar, apagar e extinguir comandos

    -   Contagem de dispositivos móveis que são geridos pelo Configuration Manager e a Microsoft Intune e a forma como foram inscritos (em massa ou baseado no utilizador)

    -   Consulta agenda e as estatísticas de duração de verificação de dispositivo móvel do dispositivo móvel

    -   Contagem de políticas de dispositivos móveis

    -   Contagem de utilizadores que possuem vários dispositivos móveis inscritos

-   **Resolução de problemas do Microsoft Intune:**

    -   Contagem e o tamanho do Estado, o estado, o inventário, DDR, RDR, inquilino e UDX mensagens de estado, POL, registo, certificados, CRP, ressincronização, CFD, RDO, BEX, ISM e conformidade que são transferidas a partir do Microsoft Intune

    -   Contagem e o tamanho das ações de dispositivo (apagar, extinguir, bloquear) telemetria e mensagens de dados que são replicadas para o Microsoft Intune

    -   Completo e diferenças estatísticas de sincronização de utilizador para o Microsoft Intune

-   **Gestão de dispositivos móveis (MDM) no local:**

    -   Estatísticas de êxito/falha de implementação para implementações de aplicações MDM no local

    -   Contagem de pacotes e perfis de inscrição em massa do Windows 10

-   **Implementação do sistema operativo:**

    -   Contagem de imagens de arranque, controladores, pacotes de controladores, pontos de distribuição preparados com multicast ativado, pontos de distribuição com PXE ativado e sequências de tarefas

-   **Atualizações de software:**

    -   Total/média número de coleções que têm de implementações de atualizações de software e o número de máximo/média de atualizações implementadas

    -   Número de regras de implementação automática que estão associadas a sincronização

    -   Número de regras de implementação automática que criam atualizações novas ou acrescentam atualizações a um grupo existente

    -   Disponível e o prazo deltas que são utilizados nas regras de implementação automática

    -   Número médio e máximo de atribuições por atualização

    -   Contagem das atualizações que são criados e implementados com o System Center Update Publisher

    -   Contagem de grupos de atualização e atribuições

    -   Contagem de pacotes de atualização e o número de máximo/mínimo/média de pontos de distribuição que são visadas com pacotes

    -   Número de grupos de atualização e número máximo/mínimo/médio de atualizações por grupo

    -   Número de atualizações e a percentagem de atualizações que são implementadas, expirado, substituído, transferido e contenham EULAs

    -   Atualizar códigos de erro de análise e contagem de máquinas

    -   Avaliação de atualização de cliente e agendas de análise

    -   Agenda de sincronização de ponto de atualização de software

    -   Número de regras de implementação automática que tenham várias implementações

    -   Configurações que são utilizadas para o Active Directory Windows 10 plano de manutenção

    -   Versões de conteúdo de dashboard do Windows 10

    -   Clientes de contagem do Windows 10 que utilizam o Windows Update para empresas

    -   Estatísticas de aplicação de patches de cluster

    -   Contagem de atualizações do Office 365 implementadas

    -   ***[Novo] *** Classificações são sincronizadas pelo ponto de atualização de Software

-   **Dados de desempenho/SQL:**

    -   Contagem das maiores tabelas de bases de dados

    -   Informações de réplica do SQL Always-On

    -   Contagem de coleções por tipo

    -   ***[Atualizado] *** Estatísticas de avaliação de coleção (hora, atribuída versus contagens não atribuídas, contagens por tipo, o rollover de ID e utilização de regras de consulta)

    - ***[Novo] *** Período de retenção do registo de alterações do SQL Server

-   ***[Novo] Atualizações de sites:***

    - ***[Novo] *** Versões das correções instaladas do Gestor de Configuraton

##  <a name="bkmk_level3"></a> Nível 3 - Completo
O nível de total inclui todos os dados nos níveis de básico e avançado. Também inclui informações adicionais sobre o Endpoint Protection, percentagens de compatibilidade de atualização e informações de atualização de software. Este nível pode também incluir informações de diagnóstico avançadas, como ficheiros de sistema e instantâneos de memória, que podem incluir informações pessoais que existiam na memória ou ficheiros de registo no momento da captura.

Iniciar com o System Center Configuration Manager versão 1602, este nível inclui o seguinte:

-   Estatísticas de avaliação e de atualização de coleções

-   Resumo do estado de funcionamento do Endpoint Protection (incluindo contagem de clientes protegidos, em risco, desconhecidos e não suportados)

-   Configuração da política do Endpoint Protection

-   Informações de implementação de atualização de software (percentagem das implementações direcionadas com cliente versus hora UTC, necessário opcional versus automática e, a supressão de reinicialização)

-   Compatibilidade geral das implementações de atualizações de software

-   Informações de agenda de avaliação de regras de implementações automáticas

-   Número de clientes que tenham políticas de proteção de acesso de rede

-   Contagens e códigos de erro de implementação de atualizações de software

-   Número máximo/mínimo/médio de clientes inativos em coleções de implementações de atualização de software

-   Contagem de grupos que já passaram da validade atualizações de software

-   Número máximo/mínimo/médio de atualizações de software por pacote

-   Percentagens de êxito de análise de atualização de software

-   Número máximo/mínimo/médio de horas desde a última análise de atualização de software

-   ***[Novo] *** Produtos de atualização de software sincronizados com êxito pelo ponto de atualização de Software
-   ***[Novo] *** Definições de compatibilidade: Detalhes de configuração de modelo SCEP, VPN, Wi-Fi e política de conformidade

-   ***[Novo] *** Tipo do EAS condicional as políticas de acesso (bloco ou quarentena) de dispositivos geridos pelo Intune


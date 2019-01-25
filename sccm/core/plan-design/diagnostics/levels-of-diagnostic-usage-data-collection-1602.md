---
title: Dados de diagnóstico para a versão 1602
titleSuffix: Configuration Manager
description: Saiba mais sobre os níveis de diagnósticos e dados de utilização recolhe do System Center Configuration Manager versão 1602.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1210a1ca-78c7-4d17-81cf-ac1bc5c5cf3e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 64bd6ee21c98b7a047f3a8330cf5995ed762501b
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897972"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1602-of-system-center-configuration-manager"></a>Níveis de recolha de dados de utilização de diagnóstico da versão 1602 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager versão 1602 recolhe três níveis de diagnósticos e dados de utilização: **Básica**, **avançada**, e **completa**. Por predefinição, esta funcionalidade está definida no nível Avançado. As secções seguintes fornecem detalhes adicionais sobre os dados que recolhe de cada nível.

Alterações das versões anteriores são indicadas com ***[novo]*** ou ***[atualizado]***.

> [!IMPORTANT]
>  O Configuration Manager não recolhe códigos de site, nomes de sites, endereços IP, nomes de utilizador, nomes de computador, endereços físicos ou endereços de e-mail nos níveis básico ou avançado. Qualquer recolha destas informações no nível completo não é intencional, ou seja, potencialmente incluídas nas informações de diagnóstico avançadas, como ficheiros de registo ou instantâneos de memória. Microsoft não utilizará estas informações para identificar, contactar ou desenvolver advertising.

##  <a name="bkmk_change"></a> Como alterar o nível
 Os administradores que tenham um âmbito de administração baseada em funções que inclua **modificar** permissões sobre o **Site** classe de objeto pode alterar o nível dos dados recolhidos nas definições de diagnóstico e dados de utilização na consola do Configuration Manager.


  Para tal, na consola, aceda ao separador de backstage (o canto superior esquerdo separador com a seta de lista pendente), selecione **dados de utilização**e, em seguida, selecione o nível de dados que pretende utilizar.  

##  <a name="bkmk_level1"></a> Nível 1 - Básico
 O nível básico inclui dados sobre a hierarquia, os dados necessários para o ajudar a melhorar a sua instalação ou atualização de experiência e os dados que ajuda a determinar as atualizações do Configuration Manager que são aplicáveis para a sua hierarquia.

 Começando com o System Center Configuration Manager versão 1602, este nível inclui o seguinte:


- Informações de configuração:
  - Crie, instalar o tipo, pacotes de idiomas, funcionalidades ativadas por si  

  - ***[Atualizado]***  Atualizar o estado de implementação de pacote e erros, o progresso do download e erros de pré-requisitos     

  - ***[Novo]***  Versão do script pós-atualização

  - ***[Novo]***  Uso de cadência rápida de atualização

-   Métricas de desempenho da base de dados (de processamento de informações, principais procedimentos de armazenados do SQL Server por processador e utilização do disco de replicação)

-   Configuração de base de dados básica (processadores, configuração de cluster e configuração de vistas distribuídas)

-   Esquema de base de dados do Configuration Manager (hash de todas as definições de objetos)

-   Versões de cliente de contagem do Configuration Manager e versões do sistema operativo

-   Contagem de sistemas operativos para dispositivos geridos e políticas definidas pelo conector do Exchange

-   Contagem de localidades e idiomas de cliente

-   Contagem de dispositivos Windows 10 por ramo e compilação

-   Configuration Manager site hierarquia dados básicos (lista de sites, tipo, versão, estado, contagem de clientes e fuso horário)

-   Informações de servidor para sistema de site básico (funções de sistema de sites utilizadas, estado de Internet e o SSL, sistema operativo, processadores e máquina física ou virtual)

-   Estatísticas de deteção de utilizador básico (utilizador deteção contagem máximo/mínimo/médio grupo tamanhos e)

-   Informações de proteção de ponto final básicas (versões de cliente de antimalware)

-   Tipo de aplicação e a implantação básico contagens (total de aplicações, total de aplicações com vários tipos de implementação, aplicações de aplicativos no total com as dependências, total substituídas e contagem de tecnologias de implantação em utilização)

-   Implementação de básica do sistema operativo (OSD) conta (imagens)

-   Ponto de distribuição e gestão de pontos de tipos e informações básicas de configuração (protegida, pré-configurado, PXE, multicast, estado SSL, pontos de distribuição de extração/ponto a ponto, compatível com MDM, habilitados para SSL, etc.)

-   Estatísticas de telemetria (quando executadas, tempo de execução e erros)

- ***[Novo]***  Configurada a nível de telemetria, modo (online ou offline) e configuração de atualização rápida

- ***[Novo]***  Utilização de deteção de rede (ativada ou desativada)
- ***[Novo]***  Consola de administração:

    -  Estatísticas sobre ligações de consolas (versão do sistema opeating, idioma, SKU e arquitetura, memória do sistema, contagem de processadores lógicos, ligue o ID do site, versões de .NET instaladas e pacotes de idiomas da consola)

##  <a name="bkmk_level2"></a> Nível 2 - Avançado
O nível avançado é a predefinição após a conclusão da configuração. Este nível inclui dados recolhidos no nível básico, dados específicos de funcionalidades (frequência e duração de utilização), as definições de cliente do Configuration Manager (nome do componente, estado e determinadas definições como intervalos de consulta) e informações básicas sobre atualizações de software.

Este nível é recomendado porque disponibiliza à Microsoft com os dados mínimos necessários para fazer melhorias úteis em versões futuras dos produtos e serviços. Nesse nível nomes de objetos não recolher (sites, utilizadores, computadores ou objetos), detalhes sobre objetos relacionados com segurança nem vulnerabilidades como contagens dos sistemas que necessitam de atualizações de software.

Começando com o System Center Configuration Manager versão 1602, este nível inclui o seguinte:

- **Gestão de aplicações:**

  -   ***[Atualizado]***  Informações básicas de utilização/segmentação para tipos de implementação que são utilizados dentro da organização (utilizador em comparação com o dispositivo segmentado, necessário em comparação com as aplicações disponíveis e universais)  

  -  ***[Atualizado]***  Informações de implementação de aplicações (instalar/desinstalar, necessita de aprovação, interação do utilizador ativado/desativado, dependência e substituição)  

  -   Estatísticas de pedidos de aplicação disponíveis  

  -   Contagem de pacotes por tipo  

  -   Contagem de aplicabilidade de aplicações por sistema operativo  

  -   Contagem de implementações de pacote/programa  

  -   Contagem de ambientes de App-V e propriedades de implementação  

  -   Contagem de licenças de aplicação licenciadas para Windows 10  

  -   ***[Atualizado]***  Número máximo/mínimo/médio de implementações de aplicações por utilizador/dispositivo por período de tempo

  -   Tipo e duração da janela de manutenção  

  -  ***[Novo]***  Estatísticas de tamanho e a complexidade de política de aplicação

- **Cliente:**

  -   Lista/contagem de agentes de cliente ativados

  -   Contagem de instalações de cliente a partir de cada tipo de localização de origem

  -   Contagem de falhas de instalação de cliente

- **Definições de compatibilidade:**

  -   Contagem de itens de configuração por tipo

  -   Informações básicas de linha de base de configuração (contagem, número de implementações e número de referências)

  -   Contagem de implementações que referenciam definições incorporadas (o valor de configuração não é capturado)

  -   Contagem de regras e implementações criadas para as definições personalizadas

  -   ***[Atualizado]***  Contagem de modelos de Simple Certificate Enrollment Protocol, VPN, Wi-Fi, certificado (. pfx) e política de conformidade implementadas   

  -  ***[Novo]***  Certificado de contagem de SCEP Simple Certificate Enrollment Protocol (), VPN, Wi-Fi, certificado (. pfx) e implementações de política de conformidade por plataforma

- **Conteúdo:**

  -   Contagem de limites por tipo

  -   Informações do grupo de limites (contagem de limites e sistemas de sites que estão atribuídos a cada grupo de limites)

  -   Informações do grupo de ponto de distribuição (contagem de pacotes e pontos de distribuição que são atribuídos a cada grupo de pontos de distribuição)

  -   Informações de configuração de ponto de distribuição (utilização da cache de ramificação e a monitorização do ponto de distribuição)

  -   Informações de configuração do Gestor de distribuição (threads, repita o atraso, número de repetições e as definições do ponto de distribuição de extração)

- **Endpoint Protection:**

  -   Antimalware do Endpoint Protection e utilização da política de Firewall do Windows (número de políticas únicas atribuídas ao grupo)<br /><br />Não inclui quaisquer informações sobre as definições que estão incluídas na política.

  -   Erros de implementação do Endpoint Protection (contagem de códigos de erro de implementação de política de proteção de ponto final)

  -   Contagem de coleções que estão selecionadas para aparecerem no dashboard do endpoint protection

  -   Contagem de alertas que estão configurados para a funcionalidade Endpoint Protection

- **Gestão de aplicações móveis (MAM):**

  -   Contagem de aplicações do Office com MAM ativada, aplicativos de linha de negócio e políticas pelo sistema operativo

  -   Contagem de implementações de aplicações/política de MAM

  -   Contagem de regras que são criadas por definição de MAM

- **Gestão de dispositivos móveis (MDM):**

  -   Contagem de emitido ações do dispositivo móvel: bloquear, afixar rest, apagar e extinguir comandos

  -   Contagem de dispositivos móveis que são geridos pelo Configuration Manager e o Microsoft Intune e como foram inscritos (em massa ou baseada no usuário)

  -   Consulta de agenda e as estatísticas de duração de entrada de dispositivo móvel de dispositivos móveis

  -   Contagem de políticas de dispositivos móveis

  -   Contagem de utilizadores que têm vários dispositivos móveis inscritos

- **Resolução de problemas do Microsoft Intune:**

  -   Contagem e tamanho de estado, estado, inventário, RDR, DDR, UDX, inquilino mensagens de estado, POL, LOG, certificado, CRP, ressincronização, CFD, RDO, BEX, ISM e conformidade que são transferidas a partir do Microsoft Intune

  -   Contagem e tamanho das ações do dispositivo (apagar, extinguir, bloquear) telemetria e mensagens de dados que são replicadas para o Microsoft Intune

  -   Diferenciais e completas estatísticas de sincronizações de utilizador para o Microsoft Intune

- **Gestão de dispositivos móveis (MDM) no local:**

  -   Estatísticas de êxito/falha de implementação para implementações de aplicações MDM no local

  -   Contagem de pacotes e perfis de inscrição em massa do Windows 10

- **Implementação do sistema operativo:**

  -   Contagem de imagens de arranque, controladores, pacotes de controladores, pontos de distribuição preparados com multicast ativado, pontos de distribuição com PXE ativado e sequências de tarefas

- **Atualizações de software:**

  -   Número total/médio de coleções com implementações de atualizações de software e o número máximo/médio de implementar atualizações

  -   Número de regras de implementação automática que estão associadas a sincronização

  -   Número de regras de implementação automática que criam atualizações novas ou acrescentam atualizações a um grupo existente

  -   Deltas disponíveis e de prazo que são utilizados nas regras de implementação automática

  -   Número médio e máximo de atribuições por atualização

  -   Contagem de atualizações que são criados e implementados com o System Center Update Publisher

  -   Contagem de grupos de atualização e atribuições

  -   Contagem de pacotes de atualização e o número máximo/mínimo/médio de pontos de distribuição que são segmentados com pacotes

  -   Número de grupos de atualização e número máximo/mínimo/médio de atualizações por grupo

  -   Número de atualizações e percentagem de atualizações que são implementadas, expiradas, substituídas, transferidas e contêm EULAs

  -   Atualizar códigos de erro de análise e contagem de máquinas

  -   Avaliação de atualização de cliente e agendas de análise

  -   Agenda de sincronização de ponto de atualização de software

  -   Número de regras de implementação automática que têm várias implementações

  -   Configurações que são utilizadas para o Active Directory Windows 10, planos de manutenção

  -   Versões de conteúdo de dashboard do Windows 10

  -   Clientes de contagem do Windows 10 que utilizam o Windows Update para empresas

  -   Estatísticas de aplicação de patches de cluster

  -   Contagem de atualizações do Office 365 implementadas

  -   ***[Novo]***  Classificações são sincronizadas pelo ponto de atualização de Software

- **Dados de desempenho/SQL:**

  -   Contagem das maiores tabelas de bases de dados

  -   Informações de réplica do SQL Always-On

  -   Contagem de coleções por tipo

  -   ***[Atualizado]***  Estatísticas de avaliação de coleção (tempo, atribuído versus contagens não atribuídas, contagens por tipo, o rollover de ID e o uso de regra de consulta)

  - ***[Novo]***  Período de retenção de registo de alterações SQL

- ***[Novo] Atualizações do site:***

  - ***[Novo]***  Versões das correções instaladas do Configuration Manager

##  <a name="bkmk_level3"></a> Nível 3 - Completo
O nível completo inclui todos os dados nos níveis de básico e avançado. Também inclui informações adicionais sobre o Endpoint Protection, percentagens de compatibilidade de atualização e informações de atualização de software. Este nível também pode incluir informações de diagnóstico avançadas, como ficheiros de sistema e instantâneos de memória, que podem incluir informações pessoais que existiam na memória ou ficheiros de registo no momento da captura.

Começando com o System Center Configuration Manager versão 1602, este nível inclui o seguinte:

-   Estatísticas de avaliação e de atualização de coleções

-   Resumo do estado de funcionamento do Endpoint Protection (incluindo contagem de clientes protegidos, em risco, desconhecidos e não suportados)

-   Configuração da política do Endpoint Protection

-   Informações de implementação de atualizações de software (percentagem das implementações segmentadas com cliente versus a hora UTC, necessário opcional versus silencioso e supressão de reinício)

-   Compatibilidade geral das implementações de atualizações de software

-   Informações de agenda de avaliação de regras de implementações automáticas

-   Número de clientes que têm políticas de proteção de acesso de rede

-   Contagens e códigos de erro de implementação de atualizações de software

-   Número máximo/mínimo/médio de clientes inativos em coleções de implementações de atualização de software

-   Contagem de grupos que têm atualizações de software expiradas

-   Número máximo/mínimo/médio de atualizações de software por pacote

-   Percentagens de êxito de análise de atualização de software

-   Número máximo/mínimo/médio de horas desde a última análise de atualização de software

-   ***[Novo]***  Produtos de atualização de software sincronizados pelo ponto de atualização de Software
-   ***[Novo]***  As definições de compatibilidade: Detalhes de configuração de modelo SCEP, VPN, Wi-Fi e política de conformidade

-   ***[Novo]***  Políticas de tipo de acesso condicional do EAS (bloqueio ou quarentena) para dispositivos geridos pelo Intune

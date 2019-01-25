---
title: Dados de diagnóstico para a versão 1606
titleSuffix: Configuration Manager
description: Saiba mais sobre os níveis de diagnósticos e dados de utilização recolhe do System Center Configuration Manager versão 1606.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f7350d03-f440-4744-82d4-75f8c6c25028
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: af82e3b5d0f555494705a28fba291253c83b00ea
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898023"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1606-of-system-center-configuration-manager"></a>Níveis de recolha de dados de utilização de diagnóstico para a versão 1606 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager versão 1606 recolhe três níveis de diagnósticos e dados de utilização: **Básica**, **avançada**, e **completa**. Por predefinição, esta funcionalidade está definida no nível Avançado. As secções seguintes fornecem detalhes adicionais sobre os dados que recolhe de cada nível.

Alterações das versões anteriores são indicadas com ***[novo]***, ***[atualizado]***, ***[removido]***, ou ***[movido]***.


> [!IMPORTANT]
>  O Configuration Manager não recolhe códigos de site, nomes de sites, endereços IP, nomes de utilizador, nomes de computador, endereços físicos ou endereços de e-mail nos níveis básico ou avançado. Qualquer recolha destas informações no nível completo não é intencional, ou seja, potencialmente incluídas nas informações de diagnóstico avançadas, como ficheiros de registo ou instantâneos de memória. Microsoft não utilizará estas informações para identificar, contactar ou desenvolver advertising.

##  <a name="bkmk_change"></a> Como alterar o nível
 Os administradores que tenham um âmbito de administração baseada em funções que inclua **modificar** permissões sobre o **Site** classe de objeto pode alterar o nível dos dados recolhidos nas definições de diagnóstico e dados de utilização na consola do Configuration Manager.

   Para tal, na consola, aceda ao separador de backstage (o canto superior esquerdo separador com a seta de lista pendente), selecione **dados de utilização**e, em seguida, selecione o nível de dados que pretende utilizar.  

##  <a name="bkmk_level1"></a> Nível 1 - Básico
 O nível básico inclui dados sobre a hierarquia, os dados necessários para o ajudar a melhorar a sua instalação ou atualização de experiência e os dados que ajuda a determinar as atualizações do Configuration Manager que são aplicáveis para a sua hierarquia.

 Começando com o System Center Configuration Manager versão 1606, este nível inclui o seguinte:


 -   Informações de configuração:
      - Crie, instalar o tipo, pacotes de idiomas, funcionalidades ativadas por si  

      -   Atualizar estado de implementação de pacote e erros, transfira o progresso e os erros de pré-requisitos  

      -  Versão do script pós-atualização

      -  Utilização de cadência rápida de atualização

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

-   Informações básicas do Endpoint Protection (versões de cliente de antimalware)

-   Tipo de aplicação e a implantação básico contagens (total de aplicações, total de aplicações com vários tipos de implementação, aplicações de aplicativos no total com as dependências, total substituídas e contagem de tecnologias de implantação em utilização)

-   Implementação de básica do sistema operativo (OSD) conta (imagens)

-   Ponto de distribuição e gestão de pontos de tipos e informações básicas de configuração (protegida, pré-configurado, PXE, multicast, estado SSL, pontos de distribuição de extração/ponto a ponto, compatível com MDM, habilitados para SSL, etc.)

-   Estatísticas de telemetria (quando executadas, tempo de execução e erros)

-  Nível de telemetria configurado, o modo (online ou offline) e configuração de atualização rápida

-  Utilização da deteção de rede (ativada ou desativada)
-  Consola de administração:

     -  Estatísticas sobre ligações de consolas (versão do sistema operativo, linguagem, SKU e arquitetura, memória do sistema, contagem de processadores lógicos, ligue o ID do site, versões de .NET instaladas e pacotes de idiomas da consola)    


- ***[Novo]***  Versão SQL, nível de service pack, edição, ID de agrupamento e caracteres definido


##  <a name="bkmk_level2"></a> Nível 2 - Avançado
O nível avançado é a predefinição após a conclusão da configuração. Este nível inclui dados recolhidos no nível básico, dados específicos de funcionalidades (frequência e duração de utilização), as definições de cliente do Configuration Manager (nome do componente, estado e determinadas definições como intervalos de consulta) e informações básicas sobre atualizações de software.

Este nível é recomendado porque disponibiliza à Microsoft com os dados mínimos necessários para fazer melhorias úteis em versões futuras dos produtos e serviços. Nesse nível nomes de objetos não recolher (sites, utilizadores, computadores ou objetos), detalhes sobre objetos relacionados com segurança nem vulnerabilidades como contagens dos sistemas que necessitam de atualizações de software.

Começando com o System Center Configuration Manager versão 1606, este nível inclui o seguinte:

-   **Gestão de aplicações:**  

    -    Informações básicas de utilização/segmentação para tipos de implementação que são utilizados dentro da organização (utilizador em comparação com o dispositivo segmentado, necessário em comparação com as aplicações disponíveis e universais)  

    -   Informações de implementação de aplicações (instalar/desinstalar, necessita de aprovação, interação do utilizador ativado/desativado, dependência e substituição)  

    -   Estatísticas de pedidos de aplicação disponíveis  

    -   Contagem de pacotes por tipo  

    -   Contagem de aplicabilidade de aplicações por sistema operativo  

    -   Contagem de implementações de pacote/programa  

    -   Contagem de ambientes de App-V e propriedades de implementação  

    -   Contagem de licenças de aplicação licenciadas para Windows 10  

    -   Número de máximo/mínimo/médio de implementações de aplicações por utilizador/dispositivo por período de tempo

    -   Tipo e duração da janela de manutenção  

    -  Estatísticas de tamanho e a complexidade de política de aplicação

    - ***[Novo]***  Contagem da Windows Store para aplicações de negócio e estatísticas de sincronização (incluindo resumidos tipos de aplicações)  

    - ***[Novo]***  Estatísticas de grupo de limites (quantos mais rápidas e quantos lento e contagem por grupo)

    - ***[Novo]***  Contagens e opções de configuração de MSI

    - ***[Novo]***  Requisitos da aplicação (a contagem de condições incorporadas é referenciada por tecnologia de implantação)

    - ***[Novo]***  Substituição da aplicação, a profundidade máxima da cadeia

    - ***[Novo]***  Utilização de acesso de dados universal (UDA) e como criado



-   **Cliente:**  

    -   Lista/contagem de agentes de cliente ativados  

    -   Contagem de instalações de cliente a partir de cada tipo de localização de origem  

    -   Contagem de falhas de instalação de cliente  

    -  ***[Novo]***  Configuração de implementação de atualização automática de cliente incluindo a criação de pilotos de cliente

    -  ***[Novo]***  Estatísticas de estado de funcionamento do cliente e o resumo do problema superior

    - ***[Novo]***  Idade de BIOS em anos

    - ***[Novo]***  Idade de sistema operativo em meses

    - ***[Novo]***  Ações de contagem de centro de Software

    - ***[Novo]***  Versão de cliente do active Management Technology (AMT)

    - ***[Novo]***  Erros de transferência de implementação do cliente

    - ***[Novo]***  Cliente notificação ação estado da operação (é de quantas vezes cada execução, Máx. número de clientes de destinados e a taxa média de êxito)

    - ***[Novo]***  Métodos de implantação usados para cliente e a contagem de clientes por método de implementação

    - ***[Novo]***  Configuração de tamanho de cache do cliente



- ***[Novo]***  **Serviços cloud:**

  - ***[Novo]***  Contagem de coleções que são sincronizados com o Operations Management Suite

  - ***[Novo]***  Conector de cloud se o Operations Management Suite está ativada



- ***[Novo] Coleções:***

    -  ***[Movido]***  Estatísticas de avaliação de coleção (tempo, atribuído versus contagens não atribuídas, contagens por tipo, o rollover de ID e o uso de regra de consulta)

    - ***[Novo]***  Coleções sem uma implementação

    - ***[Novo]***  Utilização de ID de coleção (não ficar sem IDs)



-   **Definições de compatibilidade:**  

    -   Contagem de itens de configuração por tipo  

    -   Informações básicas de linha de base de configuração (contagem, número de implementações e número de referências)  

    -   ***[Atualizado]***  Contagem de implementações que referenciam definições incorporadas (agora capturar remediar definição)  

    -   ***[Atualizado]***  Contagem de regras e implementações criadas para as definições personalizadas (agora capturar remediar definição)  
    -   Contagem de modelos de certificado de protocolo SCEP (Simple Enrollment), VPN, Wi-Fi, certificado (. pfx) e política de conformidade implementadas

    -  Contagem do certificado de SCEP, VPN, Wi-Fi, certificado (. pfx) e implementações de política de conformidade por plataforma

    - ***[Novo]***  Passport para a política de trabalho (criado, implantado)



-   **Conteúdo:**  

    -   Contagem de limites por tipo  

    -   Informações do grupo de limites (contagem de limites e sistemas de sites que estão atribuídos a cada grupo de limites)  

    -   Informações do grupo de ponto de distribuição (contagem de pacotes e pontos de distribuição que são atribuídos a cada grupo de pontos de distribuição)  

    -   Informações de configuração de ponto de distribuição (utilização da cache de ramificação e a monitorização do ponto de distribuição)  

    -   Informações de configuração do Gestor de distribuição (threads, repita o atraso, número de repetições e as definições do ponto de distribuição de extração)  


-   **Endpoint Protection:**  

    -   Antimalware do Endpoint Protection e utilização da política de Firewall do Windows (número de políticas únicas atribuídas ao grupo)<br /><br /> Não inclui quaisquer informações sobre as definições que estão incluídas na política.  

    -   Erros de implementação do Endpoint Protection (contagem de códigos de erro de implementação de política de proteção de ponto final)  

    -   Contagem de coleções que estão selecionadas para aparecerem no dashboard do Endpoint Protection  

    -   Contagem de alertas que estão configurados para a funcionalidade Endpoint Protection  

    - ***[Novo]***  Políticas de proteção avançada de ameaças (ATP) (contagem de políticas e se as políticas são implementadas)


-   ***[Removido]***  **Gestão de aplicações móveis (MAM):**  

    -   ***[Removido]***  Aplicativos habilitados para contagem de MAM Office, aplicativos de linha de negócio e políticas pelo sistema operativo  

    -   ***[Removido]***  Implementações de aplicações/política de contagem de MAM  

    -   ***[Removido]***  Contagem de regras que são criadas por definição de MAM  


- ***[Novo]***  **Migração:**

  -  ***[Novo]***  Contagem de objetos migrados (utilização do Assistente de migração)



-   **Gestão de dispositivos móveis (MDM):**  

    -   Contagem de emitido ações do dispositivo móvel: bloquear, afixar rest, apagar e extinguir comandos  

    -   Contagem de dispositivos móveis que são geridos pelo Configuration Manager e o Microsoft Intune e como foram inscritos (em massa ou baseada no usuário)  

    -   Consulta de agenda e as estatísticas de duração de entrada de dispositivo móvel de dispositivos móveis  

    -   Contagem de políticas de dispositivos móveis  

    -   Contagem de utilizadores que têm vários dispositivos móveis inscritos  

-   **Resolução de problemas do Microsoft Intune:**

    -   Contagem e tamanho de estado, estado, inventário, RDR, DDR, UDX, inquilino mensagens de estado, POL, LOG, certificado, CRP, ressincronização, CFD, RDO, BEX, ISM e conformidade que são transferidas a partir do Microsoft Intune

    -   Contagem e tamanho das ações do dispositivo (apagar, extinguir, bloquear) telemetria e mensagens de dados que são replicadas para o Microsoft Intune

    -   Diferenciais e completas estatísticas de sincronizações de utilizador para o Microsoft Intune


-   **Gestão de dispositivos móveis (MDM) no local:**  

    -   Estatísticas de êxito/falha de implementação para implementações de aplicações MDM no local  

    -   Contagem de pacotes e perfis de inscrição em massa do Windows 10  



-   **Implementação do sistema operativo:**  

    -   Contagem de imagens de arranque, controladores, pacotes de controladores, pontos de distribuição preparados com multicast ativado, pontos de distribuição com PXE ativado e sequências de tarefas  

    -   ***[Novo]***  Contagens de sequência de tarefas passo utilização



-   **Atualizações do site:**

    - Versões das correções instaladas do Configuration Manager




-   **Atualizações de Software:**  

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

    -   Classificações são sincronizadas pelo ponto de atualização de Software

    -   ***[Novo]***  Estatísticas de balanceamento de carga de ponto de atualização de software



-   **Dados de desempenho/SQL:**  

    -   Contagem das maiores tabelas de bases de dados  

    -   Informações de réplica do SQL Always-On  

    -  Período de retenção de registo de alterações SQL

    - ***[Novo]***  Tipos de deteção, ativados e a agenda (completos e incrementais)

    - ***[Novo]***  Estatísticas operacionais de deteção (contagem de foram encontrados objetos)

    - ***[Novo]***  Controlo de problemas de desempenho, o período de retenção e o estado de limpeza automática de alterações do SQL



- ***[Novo]***  **Diversos**

    - ***[Novo]***  Contagem de sites com reativação em Lan (WOL)



##  <a name="bkmk_level3"></a> Nível 3 - Completo
O nível completo inclui todos os dados nos níveis de básico e avançado. Também inclui informações adicionais sobre o Endpoint Protection, percentagens de compatibilidade de atualização e informações de atualização de software. Este nível também pode incluir informações de diagnóstico avançadas, como ficheiros de sistema e instantâneos de memória que podem incluir informações pessoais que existiam na memória ou ficheiros de registo no momento da captura.

Começando com o System Center Configuration Manager versão 1606, este nível inclui o seguinte:

-   Estatísticas de avaliação e de atualização de coleções

-   Resumo do estado de funcionamento do Endpoint Protection (incluindo contagem de clientes protegidos, em risco, desconhecidos e não suportados)

-   Configuração da política do Endpoint Protection

-   Informações de implementação de atualizações de software (percentagem das implementações direcionadas com o cliente em relação a hora UTC, necessário opcional versus silencioso e supressão de reinício)

-   Compatibilidade geral das implementações de atualizações de software

-   Informações de agenda de avaliação de regras de implementações automáticas

-   ***[REMOVIDO]***  Número de clientes que têm políticas de proteção de acesso de rede

-   Contagens e códigos de erro de implementação de atualizações de software

-   Número máximo/mínimo/médio de clientes inativos em coleções de implementações de atualização de software

-   Contagem de grupos que têm atualizações de software expiradas

-   Número máximo/mínimo/médio de atualizações de software por pacote

-   Percentagens de êxito de análise de atualização de software

-   Número máximo/mínimo/médio de horas desde a última análise de atualização de software

-    Produtos de atualização de software sincronizados pelo ponto de atualização de Software
-    Definições de compatibilidade: Detalhes de configuração de modelo SCEP, VPN, Wi-Fi e política de conformidade

-    Tipo de políticas de acesso condicional do EAS (bloqueio ou quarentena) para dispositivos que gere o Intune

-   ***[Novo]***  Top 50 CPUs no ambiente

-   ***[Novo]***  Pacote de configuração do DCM para utilização do System Center Configuration Manager

-   ***[Novo]***  Código de produto MSI (aplicações comuns que os clientes implementar)

-   ***[Novo]***  Resumo do Estado de funcionamento do ATP

-   ***[Novo]***  Detalhadas de erros de instalação de implementação do cliente

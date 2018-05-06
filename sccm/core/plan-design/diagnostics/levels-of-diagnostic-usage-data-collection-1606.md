---
title: Dados de diagnóstico para 1606
titleSuffix: Configuration Manager
description: Saiba mais sobre os níveis de diagnósticos e dados de utilização que o System Center Configuration Manager versão 1606 recolhe.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f7350d03-f440-4744-82d4-75f8c6c25028
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 902e5e91b64cf3061862deeb98b0d9bf427e4598
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1606-of-system-center-configuration-manager"></a>Níveis de diagnóstico de utilização de recolha de dados para a versão 1606 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager versão 1606 recolhe três níveis de diagnósticos e dados de utilização: **Básico**, **avançada**, e **completa**. Por predefinição, esta funcionalidade está definida no nível Avançado. As secções seguintes fornecem detalhes adicionais sobre os dados que recolhe de cada nível.

As alterações de versões anteriores são assinaladas com ***[New]***, ***[atualizado]***, ***[removida]***, ou ***[movido]***.


> [!IMPORTANT]
>  O Configuration Manager não recolhe códigos de site, os nomes de sites, endereços IP, nomes de utilizador, nomes de computador, endereços físicos ou endereços de correio eletrónico nos níveis básico ou avançado. Qualquer recolha destas informações no nível completo não é tem um fim específico, ou seja, potencialmente incluídas nas informações de diagnóstico avançadas, como ficheiros de registo ou instantâneos de memória. Microsoft não utilizará estas informações para identificar, contactar ou desenvolver publicidade.

##  <a name="bkmk_change"></a> Como alterar o nível
 Os administradores que tenham um âmbito de administração baseada em funções que inclua **modificar** permissões a **Site** classe de objeto pode alterar o nível dos dados recolhidos nas definições de diagnóstico e dados de utilização na consola do Configuration Manager.

   Para tal, na consola, aceda ao separador de backstage (superior separador à esquerda com a seta pendente), selecione **dados de utilização**e, em seguida, selecione o nível de dados que pretende utilizar.  

##  <a name="bkmk_level1"></a> Nível 1 - Básico
 O nível básico inclui dados sobre a sua hierarquia, dados necessárias para ajudar a melhorar a sua instalação ou atualização experiência e os dados que ajuda a determinar as atualizações do Configuration Manager que são aplicáveis para a sua hierarquia.

 Começando com o System Center Configuration Manager versão 1606, este nível inclui o seguinte:


 -   Informações de configuração:
      - Criar, instalar o tipo, pacotes de idiomas, funcionalidades que tiver ativado  

      -   Atualizar o estado de implementação de pacote e erros, transfira o progresso e erros de pré-requisitos  

      -  Versão do script pós-atualização

      -  Utilização do anel rápida de atualização

-   Métricas de desempenho de base de dados (replicação processar informações, principais procedimentos armazenados do SQL Server por processador e utilização do disco)

-   Configuração de base de dados básica (processadores, configuração de cluster e a configuração das vistas distribuídas)

-   Esquema de base de dados do Configuration Manager (hash de todas as definições de objetos)

-   Versões de cliente de contagem do Configuration Manager e versões do sistema operativo

-   Contagem de sistemas operativos para dispositivos geridos e políticas definidas pelo conector do Exchange

-   Contagem de idiomas de cliente e regiões

-   Contagem de dispositivos Windows 10 por ramo e compilação

-   Básico do Configuration Manager hierarquia dados do site (lista de sites, tipo, versão, estado, contagem de clientes e fuso horário)

-   Informações de servidor de sistema básico do site (funções de sistema de site utilizadas, estado e SSL da Internet, sistema operativo, processadores e máquina física ou virtual)

-   Estatísticas de deteção de utilizador básico (utilizador deteção contagem e máximo/mínimo/médio tamanhos de grupos)

-   Informações básicas do Endpoint Protection (versões de cliente antimalware)

-   Contagens de tipo de implementação e de aplicação básico (total de aplicações, total de aplicações com vários tipos de implementação, as aplicações de total de aplicações com dependências, totais substituídas e contagem de tecnologias de implementação em utilização)

-   Implementação básica do sistema operativo (OSD) conta (imagens)

-   Ponto de distribuição e ponto de gestão tipos e informações básicas de configuração (protegida, pré-configurado, PXE, multicast, estado SSL, pontos de distribuição de extração/ponto a ponto, MDM ativado, com SSL ativado, etc.)

-   Estatísticas de telemetria (quando executadas, tempo de execução e erros)

-  Nível de telemetria configurado, modo (online ou offline) e a configuração de atualização rápida

-  Utilização da deteção de rede (ativada ou desativada)
-  Consola de administração:

     -  Estatísticas sobre as ligações da consola (versão do sistema operativo, idioma, SKU e arquitetura, memória do sistema, contagem de processadores lógicos, ligar o ID do site, versões de .NET instaladas e pacotes de idiomas da consola)    


- ***[Novo]***  Versão SQL, nível de service pack, edição, ID de agrupamento e caráter definido


##  <a name="bkmk_level2"></a> Nível 2 - Avançado
O nível avançado é a predefinição após a conclusão da configuração. Este nível inclui dados recolhidos no nível básico, dados específicos da funcionalidade (frequência e duração de utilização), definições de cliente do Configuration Manager (nome do componente, estado e determinadas definições como intervalos de consulta) e informações básicas sobre atualizações de software.

Este nível é recomendado porque disponibiliza à Microsoft os dados mínimos necessárias para fazer melhorias úteis em futuras versões dos produtos e serviços. Este nível nomes de objeto não recolher (sites, os utilizadores, computador ou objetos), detalhes sobre objetos relacionados com segurança nem vulnerabilidades como contagens dos sistemas que necessitam de atualizações de software.

Começando com o System Center Configuration Manager versão 1606, este nível inclui o seguinte:

-   **Gestão de aplicações:**  

    -    Informações básicas de utilização/segmentação para tipos de implementação que são utilizados na sua organização (utilizador versus dispositivo segmentado, necessário versus aplicações disponíveis e universais)  

    -   Informações de implementação de aplicação (instalar/desinstalar, necessita de aprovação, interação do utilizador ativada/desativada, dependências e substituições)  

    -   Estatísticas de pedidos de aplicação disponíveis  

    -   Contagem de pacotes por tipo  

    -   Contagem de aplicabilidade de aplicações por sistema operativo  

    -   Contagem de implementações de pacote/programa  

    -   Contagem de ambientes de App-V e propriedades de implementação  

    -   Contagem de licenças de aplicação licenciadas para Windows 10  

    -   Número máximo/mínimo/médio de implementações de aplicações por utilizador/dispositivo por período de tempo

    -   Tipo e duração da janela de manutenção  

    -  Política tamanho e complexidade das estatísticas da aplicação

    - ***[Novo]***  Contagem da loja Windows para aplicações empresariais e as estatísticas de sincronização (incluindo resumidos tipos de aplicações)  

    - ***[Novo]***  Estatísticas de grupo de limites (quantos rápido, quantos lenta e count por grupo de)

    - ***[Novo]***  Contagens e opções de configuração de MSI

    - ***[Novo]***  Requisitos da aplicação (contagem de condições incorporadas é referenciada por tecnologia de implementação)

    - ***[Novo]***  Substituição de aplicações, a profundidade máxima de cadeia

    - ***[Novo]***  Utilização de acesso de dados universal (UDA) e como criada



-   **Cliente:**  

    -   Lista/contagem de agentes de cliente ativados  

    -   Contagem de instalações de cliente a partir de cada tipo de localização de origem  

    -   Contagem de falhas de instalação de cliente  

    -  ***[Novo]***  Configuração de implementação de atualização automática de cliente, incluindo testes de implementação de cliente

    -  ***[Novo]***  Estatísticas de estado de funcionamento do cliente e o resumo do problema superior

    - ***[Novo]***  Idade do BIOS no anos

    - ***[Novo]***  Idade do sistema operativo nos meses

    - ***[Novo]***  Ações de contagem de centro de Software

    - ***[Novo]***  Versão do cliente active Management Technology (AMT)

    - ***[Novo]***  Erros de transferência de implementação do cliente

    - ***[Novo]***  Notificação operação ação estado do cliente (o quantas vezes é o número de execução, máximo de clientes alvo e a taxa de êxito médio)

    - ***[Novo]***  Os métodos de implementação de cliente e a contagem de clientes por método de implementação

    - ***[Novo]***  Configuração de tamanho de cache do cliente



- ***[Novo]***  **Serviços em nuvem:**

  - ***[Novo]***  Contagem de coleções que são sincronizados para o Operations Management Suite

  - ***[Novo]***  Conector da nuvem se o Operations Management Suite está ativado



- ***[Novo] Coleções:***

    -  ***[Movido]***  Estatísticas de avaliação de coleção (tempo, atribuído versus contagens não atribuídas, contagens por tipo, rollover de ID e a utilização de regra de consulta)

    - ***[Novo]***  Coleções sem uma implementação

    - ***[Novo]***  Utilização de ID de coleção (não a ficar sem IDs)



-   **Definições de compatibilidade:**  

    -   Contagem de itens de configuração por tipo  

    -   Informações básicas de linha de base de configuração (contagem, número de implementações e número de referências)  

    -   ***[Atualizado]***  Contagem de implementações que referenciam definições incorporadas (agora capturar remediar definição)  

    -   ***[Atualizado]***  Contagem de regras e implementações criadas para as definições personalizadas (agora capturar remediar definição)  
    -   Contagem de modelos de certificado de inscrição de SCEP (Simple Protocol), VPN, Wi-Fi, certificado (. pfx) e política de conformidade implementadas

    -  Contagem do certificado de SCEP, VPN, Wi-Fi, certificado (. pfx) e implementações de política de conformidade por plataforma

    - ***[Novo]***  Passport para a política de trabalho (criado, implementado)



-   **Conteúdo:**  

    -   Contagem de limites por tipo  

    -   Informações sobre grupos de limites (contagem de limites e sistemas de sites que estão atribuídos a cada grupo de limites)  

    -   Informações do grupo de ponto de distribuição (contagem de pacotes e pontos de distribuição que estão atribuídos a cada grupo de pontos de distribuição)  

    -   Informações de configuração de ponto de distribuição (utilização da cache de ramo e monitorização do ponto de distribuição)  

    -   Informações de configuração do Gestor de distribuição (threads, repita o atraso, número de tentativas e as definições do ponto de distribuição de extração)  


-   **Endpoint Protection:**  

    -   Antimalware do Endpoint Protection e a utilização da política de Firewall do Windows (número de políticas únicas atribuídas ao grupo)<br /><br /> Isto inclui qualquer informação sobre as definições que estão incluídas na política.  

    -   Erros de implementação do Endpoint Protection (contagem de códigos de erro de implementação de política do Endpoint Protection)  

    -   Contagem de coleções que estão selecionadas para aparecerem no dashboard do Endpoint Protection  

    -   Contagem de alertas que estão configurados para a funcionalidade Endpoint Protection  

    - ***[Novo]***  Políticas advanced Threat Protection (ATP) (contagem de políticas e se as políticas são implementadas)


-   ***[Removida]***  **Gestão de aplicações móveis (MAM):**  

    -   ***[Removida]***  Aplicações Office com contagem de MAM, aplicações de linha de negócio e políticas pelo sistema operativo  

    -   ***[Removida]***  Implementações de aplicações/política de contagem de MAM  

    -   ***[Removida]***  Contagem de regras que são criadas por definição de MAM  


- ***[Novo]***  **Migração:**

  -  ***[Novo]***  Contagem de objetos migrados (utilize do Assistente de migração)



-   **Gestão de dispositivos móveis (MDM):**  

    -   Número de emitido ações do dispositivo móvel: bloquear, afixar rest, apagar e extinguir comandos  

    -   Contagem de dispositivos móveis que são geridos pelo Configuration Manager e Microsoft Intune e como foram inscritos (em massa ou com base no utilizador)  

    -   Consulta de agenda e as estatísticas de duração de verificação de dispositivos móveis de dispositivos móveis  

    -   Contagem de políticas de dispositivos móveis  

    -   Contagem de utilizadores que têm vários dispositivos móveis inscritos  

-   **Resolução de problemas de Microsoft Intune:**

    -   Contagem e tamanho de estado, o estado, inventário, RDR, DDR, UDX, inquilino mensagens de estado, POL, registo, certificado, CRP, ressincronização, CFD, RDO, BEX, ISM e conformidade que são transferidas a partir do Microsoft Intune

    -   Contagem e tamanho das ações do dispositivo (apagar, extinguir, bloquear) telemetria e mensagens de dados que são replicadas para o Microsoft Intune

    -   Diferenciais e completas estatísticas de sincronização de utilizador para o Microsoft Intune


-   **Gestão de dispositivos móveis (MDM) no local:**  

    -   Estatísticas de êxito/falha de implementação para implementações de aplicações MDM no local  

    -   Contagem de pacotes e perfis de inscrição em massa do Windows 10  



-   **Implementação do sistema operativo:**  

    -   Contagem de imagens de arranque, controladores, pacotes de controladores, pontos de distribuição preparados com multicast ativado, pontos de distribuição com PXE ativado e sequências de tarefas  

    -   ***[Novo]***  Contagens de sequência de tarefas passo utilização



-   **Atualizações de sites:**

    - Versões das correções instaladas do Configuration Manager




-   **Atualizações de Software:**  

    -   Número total/médio de coleções com implementações de atualização de software e o número máximo/médio de implementação de atualizações  

    -   Número de regras de implementação automática que estão associadas a sincronização  

    -   Número de regras de implementação automática que criam atualizações novas ou acrescentam atualizações a um grupo existente  

    -   Disponível e o prazo deltas que são utilizados em regras de implementação automática  

    -   Número médio e máximo de atribuições por atualização  

    -   Contagem das atualizações que são criados e implementados com o System Center Update Publisher  

    -   Contagem de grupos de atualização e atribuições  

    -   Contagem de pacotes de atualização e o número máximo/mínimo/médio de pontos de distribuição são segmentados com pacotes  

    -   Número de grupos de atualização e número máximo/mínimo/médio de atualizações por grupo  

    -   Número de atualizações e percentagem de atualizações que são implementadas, expiradas, substituídas, transferidas e contenham contêm EULAs  

    -   Atualizar códigos de erro de análise e contagem de máquinas  

    -   Avaliação de atualização de cliente e agendas de análise  

    -   Agenda de sincronização de ponto de atualização de software  

    -   Número de regras de implementação automática com várias implementações  

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

    - ***[Novo]***  Tipos de deteção, ativados e o agendamento (completo, incremental)

    - ***[Novo]***  Estatísticas operacionais de deteção (contagem de objetos encontrado)

    - ***[Novo]***  Problemas de desempenho, o período de retenção e o estado de automático limpeza o registo de alterações do SQL Server



- ***[Novo]***  **Diversas**

    - ***[Novo]***  Contagem de sites com reativação numa Lan (WOL)



##  <a name="bkmk_level3"></a> Nível 3 - Completo
O nível completo inclui todos os dados os níveis básico e avançado. Também inclui informações adicionais sobre o Endpoint Protection, percentagens de compatibilidade de atualização e informações de atualização de software. Este nível também pode incluir informações de diagnóstico avançadas como instantâneos de memória que podem incluir informações pessoais que existiam na memória ou ficheiros de registo no momento da captura e de ficheiros de sistema.

Começando com o System Center Configuration Manager versão 1606, este nível inclui o seguinte:

-   Estatísticas de avaliação e de atualização de coleções

-   Resumo do estado de funcionamento do Endpoint Protection (incluindo contagem de clientes protegidos, em risco, desconhecidos e não suportados)

-   Configuração da política do Endpoint Protection

-   Informações de implementação de atualização de software (percentagem das implementações direcionadas com o cliente em comparação com a hora UTC, necessário opcional versus silencioso e supressão de reinício)

-   Compatibilidade geral das implementações de atualizações de software

-   Informações de agenda de avaliação de regras de implementações automáticas

-   ***[REMOVIDA]***  Número de clientes que têm políticas de proteção de acesso de rede

-   Contagens e códigos de erro de implementação de atualizações de software

-   Número máximo/mínimo/médio de clientes inativos em coleções de implementações de atualização de software

-   Contagem de grupos que têm atualizações de software expiradas

-   Número máximo/mínimo/médio de atualizações de software por pacote

-   Percentagens de êxito de análise de atualização de software

-   Número máximo/mínimo/médio de horas desde a última análise de atualização de software

-    Produtos de atualização de software sincronizados com êxito pelo ponto de atualização de Software
-    Definições de compatibilidade: Detalhes de configuração de modelo do SCEP, VPN, Wi-Fi e política de conformidade

-    Tipo de políticas de acesso condicional do EAS (bloquear ou colocar em quarentena) para dispositivos que gere o Intune

-   ***[Novo]***  Principais 50 CPUs no ambiente

-   ***[Novo]***  Pacote de configuração de DCM para utilização do System Center Configuration Manager

-   ***[Novo]***  Código de produto MSI (aplicações comuns que os clientes implementar)

-   ***[Novo]***  Resumo do Estado de funcionamento ATP

-   ***[Novo]***  Detalhadas erros de instalação de implementação do cliente

---
title: "Dados de diagnóstico para 1610 | O System Center Configuration Manager"
description: "Saiba mais sobre os níveis de diagnósticos e dados de utilização que o System Center Configuration Manager versão 1610 recolhe."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eb20eb90-bcc0-41de-bfea-638ea470c0dd
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
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
ms.openlocfilehash: ba1e53fdc895690bb958c12d59f82a26067ecad3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1610-of-system-center-configuration-manager"></a>Níveis de diagnóstico de utilização de recolha de dados para a versão 1610 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager versão 1610 recolhe três níveis de diagnósticos e dados de utilização: **Básico**, **avançada**, e **completa**. Por predefinição, esta funcionalidade está definida no nível Avançado. As secções seguintes fornecem detalhes adicionais sobre os dados que recolhe de cada nível.

As alterações de versões anteriores são assinaladas com ***[New]***, ***[atualizado]***, ***[removida]***, ou ***[movido]***.


> [!IMPORTANT]
>  O Configuration Manager não recolhe códigos de site, os nomes de sites, endereços IP, nomes de utilizador, nomes de computador, endereços físicos ou endereços de correio eletrónico nos níveis básico ou avançado. Qualquer recolha destas informações no nível completo não é tem um fim específico, ou seja, potencialmente incluídas nas informações de diagnóstico avançadas, como ficheiros de registo ou instantâneos de memória. Microsoft não utilizará estas informações para identificar, contactar ou desenvolver publicidade.

##  <a name="bkmk_change"></a> Como alterar o nível
 Os administradores que tenham um âmbito de administração baseada em funções que inclua **modificar** permissões a **Site** classe de objeto pode alterar o nível dos dados recolhidos nas definições de diagnóstico e dados de utilização na consola do Configuration Manager.

A partir da versão 1610, alterar o nível de recolha de dados de dentro da consola, navegando até **administração** > **descrição geral** > **configuração do Site** > **Sites**. Abra **definições de hierarquia**e, em seguida, selecione o nível de dados que pretende utilizar.  

##  <a name="bkmk_level1"></a> Nível 1 - Básico
 O nível básico inclui dados sobre a sua hierarquia, dados necessárias para ajudar a melhorar a sua instalação ou atualização experiência e os dados que ajuda a determinar as atualizações do Configuration Manager que são aplicáveis para a sua hierarquia.

 Para o System Center Configuration Manager versão 1610, este nível inclui o seguinte:


-   Informações de configuração:
      - Criar, instalar o tipo, pacotes de idiomas, funcionalidades que tiver ativado  

      - Atualizar o estado de implementação de pacote e erros, transfira o progresso e erros de pré-requisitos    

      - Versão do script pós-atualização

      - Utilização do anel rápida de atualização

    - ***[Novo] *** Pré-lançamento utilização, o tipo de suporte de dados de configuração, o tipo de sucursais

    - ***[Novo] *** Data de expiração do software Assurance

- Métricas de desempenho de bases de dados (informações de processamento de replicação, principais procedimentos armazenados do SQL Server por processador e utilização de disco)

- Configuração de base de dados básica (processadores, configuração de cluster e a configuração das vistas distribuídas)

- Esquema de base de dados do Configuration Manager (hash de todas as definições de objetos)

- Versões de cliente de contagem do Configuration Manager e versões do sistema operativo

- Contagem de sistemas operativos para dispositivos geridos e políticas definidas pelo conector do Exchange

- Contagem de idiomas de cliente e regiões

- Contagem de dispositivos Windows 10 por ramo e compilação

- Básico do Configuration Manager hierarquia dados do site (lista de sites, tipo, versão, estado, contagem de clientes e fuso horário)

- Informações de servidor de sistema básico do site (funções de sistema de site utilizadas, estado e SSL da Internet, sistema operativo, processadores e máquina física ou virtual)

- Estatísticas de deteção de utilizador básico (utilizador deteção contagem e máximo/mínimo/médio tamanhos de grupos)

- Informações básicas do Endpoint Protection (versões de cliente antimalware)

- Contagens de tipo de implementação e de aplicação básico (total de aplicações, total de aplicações com vários tipos de implementação, as aplicações de total de aplicações com dependências, totais substituídas e contagem de tecnologias de implementação em utilização)

- Implementação básica do sistema operativo (OSD) conta (imagens)

- Ponto de distribuição e ponto de gestão tipos e informações básicas de configuração (protegida, pré-configurado, PXE, multicast, estado SSL, pontos de distribuição de extração/ponto a ponto, MDM ativado, com SSL ativado, etc.)

- Estatísticas de telemetria (momento da execução, tempo de execução, erros)

- Nível de telemetria configurado, modo (online ou offline) e a configuração de atualização rápida

- Utilização da deteção de rede (ativada ou desativada)
- Consola de administração:

     - Estatísticas sobre as ligações da consola (versão do sistema operativo, idioma, SKU e arquitetura, memória do sistema, contagem de processadores lógicos, ligar o ID do site, versões de .NET instaladas e pacotes de idiomas da consola)    

- Versão do SQL, nível de service pack, edição, ID de agrupamento e conjunto de carateres


##  <a name="bkmk_level2"></a> Nível 2 - Avançado
O nível avançado é a predefinição após a conclusão da configuração. Este nível inclui dados recolhidos no nível básico e dados específicos da funcionalidade (frequência e duração de utilização), definições de cliente do Configuration Manager (nome do componente, estado e determinadas definições como intervalos de consulta) e informações básicas sobre atualizações de software.

Este nível é recomendado porque disponibiliza à Microsoft os dados mínimos necessárias para fazer melhorias úteis em futuras versões dos produtos e serviços. Este nível nomes de objeto não recolher (sites, os utilizadores, computador ou objetos), detalhes de objetos relacionados com segurança nem vulnerabilidades como contagens dos sistemas que necessitam de atualizações de software.

Para o System Center Configuration Manager versão 1610, este nível inclui o seguinte:

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

    - ***[Atualizado] *** Contagem da loja Windows para aplicações empresariais e estatísticas de sincronização (incluindo resumidos tipos de aplicações, licenciado estado da aplicação e o número de online e offline licenciado aplicações)  

    - Estatísticas de grupo de limites (quantos rápido, quantos lenta e count por grupo de)

    - Contagens e opções de configuração de MSI

    - Requisitos de aplicações (contagem de condições incorporadas é referenciada por tecnologia de implementação)

    - Substituição de aplicações, profundidade máxima de cadeia

    - Utilização de acesso de dados (UDA) universal, como criado

    - ***[Novo] *** Frequência de utilização e estatísticas de aprovação de aplicações



-   **Cliente:**  

    -   Lista/contagem de agentes de cliente ativados  

    -   Contagem de instalações de cliente a partir de cada tipo de localização de origem  

    -   Contagem de falhas de instalação de cliente  

    -  ***[Atualizado] *** Atualização automática de cliente: configuração de implementação, incluindo pilotagem e exclusão de utilização de cliente (cliente de interoperabilidade expandido)

    -  Estatísticas de estado de funcionamento do cliente e o resumo do problema superior

    - Idade do BIOS no anos

    - Idade do sistema operativo nos meses

    - Ações de contagem de centro de Software

    - Versão de cliente do Active Management Technology (AMT)

    - Erros de transferência de implementação do cliente

    - Notificação operação ação estado do cliente (o quantas vezes é o número de execução, máximo de clientes alvo e a taxa de êxito médio)

    - Métodos de implementação de cliente e a contagem de clientes por método de implementação

    - Configuração de tamanho de cache do cliente

    - ***[Novo] *** Número de classes de inventário de hardware, as regras de inventário de software e regras de recolha de ficheiros




- **Serviços de cloud:**

  - Contagem das coleções sincronizados para o Operations Management Suite

  -  Indica se o conector em nuvem do Operations Management Suite está ativado

  - ***[Novo] *** Estatísticas de configuração e utilização do Gateway de gestão de nuvem

  - ***[Novo] *** Contagem dos conectores de análise de atualização




- **Coleções:**

    -  Estatísticas de avaliação de coleção (hora de consulta, atribuída versus contagens não atribuídas, contagens por tipo, rollover de ID e a utilização de regra)

    - Coleções sem uma implementação

    - Utilização de ID de coleção (não a ficar sem IDs)



-   **Definições de compatibilidade:**  

    -   Contagem de itens de configuração por tipo  

    -   Informações básicas de linha de base de configuração (contagem, número de implementações e número de referências)  

    -   Contagem de implementações que definições incorporadas de referência (agora capturar remediar definição)  

    -   Contagem de regras e implementações criadas para as definições personalizadas (agora capturar remediar definição)  
    -   Contagem de modelos de certificado de inscrição de SCEP (Simple Protocol), VPN, Wi-Fi, certificado (. pfx) e política de conformidade implementadas

    -  Contagem do certificado de SCEP, VPN, Wi-Fi, certificado (. pfx) e implementações de política de conformidade por plataforma

    - Passport para a política de trabalho (criado, implementado)



-   **Conteúdo:**  

    -   Contagem de limites por tipo  

    -   Informações sobre grupos de limites (contagem de limites e sistemas de sites que estão atribuídos a cada grupo de limites)  

    - ***[Novo] *** Relações de grupo de limites e a configuração de contingência

    -   Informações do grupo de ponto de distribuição (contagem de pacotes e pontos de distribuição que estão atribuídos a cada grupo de pontos de distribuição)  

    -   Informações de configuração de ponto de distribuição (utilização da cache de ramo e monitorização do ponto de distribuição)  

    -   Informações de configuração do Gestor de distribuição (threads, repita o atraso, número de tentativas e as definições do ponto de distribuição de extração)  

    - ***[Novo] *** Contagem de clientes de cache ponto a ponto e estatísticas de utilização

    - ***[Novo] *** Estatísticas de transferência do conteúdo de cliente


-   **Endpoint Protection:**  

    -   Antimalware do Endpoint Protection e a utilização da política de Firewall do Windows (número de políticas únicas atribuídas ao grupo)<br /><br /> Isto inclui qualquer informação sobre as definições incluídas na política.  

    -   Erros de implementação do Endpoint Protection (contagem de códigos de erro de implementação de política do Endpoint Protection)  

    -   Contagem de coleções que estão selecionadas para aparecerem no dashboard do Endpoint Protection  

    -   Contagem de alertas que estão configurados para a funcionalidade Endpoint Protection  

    -   Políticas de proteção de ameaça (ATP) avançadas (contagem de políticas e se as políticas são implementadas)


- **Migração:**

  -   Contagem de objetos migrados (utilize do Assistente de migração)



-   **Gestão de dispositivos móveis (MDM):**  

    -   ***[Atualizado] *** Número emitido ações do dispositivo móvel: bloquear, afixar rest, apagar, extinguir e sincronizar agora comandos  

    -   Contagem de dispositivos móveis que são geridos pelo Configuration Manager e Microsoft Intune e como foram inscritos (em massa, baseado no utilizador)  

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

    -   Contagens de utilização de passo de sequência de tarefas

    - ***[Novo] *** Contagem de políticas de atualização de edição



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

    -   Estatísticas de balanceamento de carga de ponto de atualização de software

    -  ***[Novo] *** Configuração do Windows 10 express atualizações




-   **Dados de desempenho/SQL:**  

    -   Contagem das maiores tabelas de bases de dados  

    -   ***[Atualizado] *** Estado de informações, utilização e estado de funcionamento da réplica SQL AlwaysOn

    -  Período de retenção de registo de alterações SQL

    - Tipos de deteção, ativados e o agendamento (completo, incremental)

    - Estatísticas de deteção operacionais (contagem de objetos encontrado)

    - Problemas de desempenho, o período de retenção e o estado de automático limpeza o registo de alterações do SQL Server



- **Diversas**

    - Contagem de sites com reativação numa Lan (WOL)

    - ***[Novo] *** Estatísticas de utilização e desempenho de relatórios  



##  <a name="bkmk_level3"></a> Nível 3 - Completo
O nível completo inclui todos os dados os níveis básico e avançado. Também inclui informações adicionais sobre o Endpoint Protection, percentagens de compatibilidade de atualização e informações de atualização de software.  Este nível também pode incluir informações de diagnóstico avançadas como instantâneos de memória que podem incluir informações pessoais que existiam na memória ou ficheiros de registo no momento da captura e de ficheiros de sistema.

Para o System Center Configuration Manager versão 1610, este nível inclui o seguinte:

-   Estatísticas de avaliação e de atualização de coleções

-   Resumo do estado de funcionamento do Endpoint Protection (incluindo contagem de clientes protegidos, em risco, desconhecidos e não suportados)

-   Configuração da política do Endpoint Protection

-   Informações de implementação de atualização de software (percentagem das implementações direcionadas com o cliente em comparação com a hora UTC, necessário opcional versus silencioso e supressão de reinício)

-   Compatibilidade geral das implementações de atualizações de software

-   Informações de agenda de avaliação de regras de implementações automáticas

-   Contagens e códigos de erro de implementação de atualizações de software

-   Número máximo/mínimo/médio de clientes inativos em coleções de implementações de atualização de software

-   Contagem de grupos que têm atualizações de software expiradas

-   Número máximo/mínimo/médio de atualizações de software por pacote

-   Percentagens de êxito de análise de atualização de software

-   Número máximo/mínimo/médio de horas desde a última análise de atualização de software

-    Produtos de atualização de software sincronizados com êxito pelo ponto de atualização de Software
-    Definições de compatibilidade: Detalhes de configuração de modelo do SCEP, VPN, Wi-Fi e política de conformidade

-    Tipo de políticas de acesso condicional do EAS (bloquear ou colocar em quarentena) para dispositivos que gere o Intune

-   Principais 50 CPUs no ambiente

-   Pacote de configuração de DCM para utilização do System Center Configuration Manager

-   Código de produto MSI (aplicações comuns que os clientes implementar)

-   Resumo do Estado de funcionamento ATP

-   Erros de instalação de implementação do cliente de detalhado

- ***[Novo] *** Da loja Windows para detalhes de negócio da aplicação (não sejam de agregação lista de aplicações sincronizadas, incluindo AppID, o estado online ou o estado offline e contagens de licenças adquiridas total)

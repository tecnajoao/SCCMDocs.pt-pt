---
title: "Dados de diagnóstico para 1610 | O System Center Configuration Manager"
description: "Saiba mais sobre os níveis de diagnóstico e dados de utilização que o System Center Configuration Manager versão 1610 recolhe."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eb20eb90-bcc0-41de-bfea-638ea470c0dd
caps.latest.revision: 4
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: ba1e53fdc895690bb958c12d59f82a26067ecad3
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1610-of-system-center-configuration-manager"></a>Níveis de recolha de dados de diagnóstico de utilização para a versão 1610 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager versão 1610 recolhe três níveis de diagnóstico e dados de utilização: **Básicas**, **avançada**, e **completa**. Por predefinição, esta funcionalidade está definida no nível Avançado. As secções seguintes fornecem detalhes adicionais sobre os dados que recolhe de cada nível.

Alterações de versões anteriores são descritas com ***[novo]***, ***[atualizado]***, ***[removido]***, ou ***[movido]***.


> [!IMPORTANT]
>  O Configuration Manager não recolher códigos de site, os nomes de sites, endereços IP, nomes de utilizador, nomes de computador, os endereços físicos ou endereços de correio eletrónico nos níveis de nível básico ou avançado. Qualquer coleção destas informações no nível completo não é purposeful, isto é, potencialmente incluído na informação de diagnóstico avançada, como ficheiros de registo ou instantâneos de memória. Microsoft não irá utilizar estas informações para identificar, contactar ou desenvolver publicidade.

##  <a name="bkmk_change"></a> Como alterar o nível
 Os administradores que têm um âmbito de administração baseada em funções que inclui **modificar** permissões a **Site** classe de objeto pode alterar o nível de dados recolhidos nas definições de diagnóstico e dados de utilização na consola do Configuration Manager.

A partir da versão 1610, alterar nível da coleção de dados a partir da consola do navegando até **administração** > **descrição geral** > **configuração do Site** > **Sites**. Abrir **definições de hierarquia**e, em seguida, selecione o nível de dados que pretende utilizar.  

##  <a name="bkmk_level1"></a> Nível 1 - Básico
 O nível básico inclui dados sobre a sua hierarquia, os dados que seja necessário para o ajudar a melhorar a sua instalação ou atualização experiência e os dados que ajuda a determinar as atualizações do Configuration Manager que são aplicáveis para a sua hierarquia.

 Para o System Center Configuration Manager versão 1610, este nível inclui o seguinte:


-   Informações de configuração:
       - Criar, instalar o tipo, pacotes de idiomas, funcionalidades que lhe ativadas  

       - Atualizar o estado de implementação de pacote e de erros, transferir o curso e erros de pré-requisitos     

       - Versão do script pós-atualização

       - Utilização de tocar rápida de atualização

    - ***[Novo] *** Pré-lançamento da utilização, o tipo de suporte de dados de configuração, o tipo de ramo

    - ***[Novo] *** Data de expiração de software Assurance

- Métricas de desempenho de bases de dados (informações de processamento de replicação, principais procedimentos armazenados do SQL Server por processador e utilização de disco)

- Configuração de base de dados básica (processadores, configuração do cluster e configuração das vistas distribuídas)

- Esquema de base de dados do Configuration Manager (hash de todas as definições de objetos)

- Versões de cliente de contagem do Configuration Manager e versões do sistema operativo

- Contagem de sistemas operativos para dispositivos geridos e políticas definidas pelo conector do Exchange

- Contagem de idiomas de cliente e regiões

- Contagem de dispositivos Windows 10 por ramo e compilação

- Básicas do Configuration Manager hierarquia dados do site (lista de site, tipo, versão, o estado, contagem de clientes e fuso horário)

- Informações do servidor de sistema básico de site (funções de sistema de sites utilizadas, estado de Internet e o SSL, sistema operativo, processadores e máquina física ou virtual)

- Estatísticas de deteção de utilizador básica (utilizador deteção contagem de máximo/mínimo/média grupo tamanho e)

- Informações básicas de Endpoint Protection (proteção contra software maligno versões de cliente)

- Tipo de aplicação e implementação básico conta (aplicações total, aplicações total com vários tipos de implementação, aplicações total com dependências, total substituídas aplicações e contagem de tecnologias de implementação em utilização)

- Implementação básica sistema operativo (OSD) conta (imagens)

- Ponto de distribuição e ponto de gestão tipos e informações de configuração básica (protegidos, pré-configurado, PXE, multicast estado SSL, pontos de distribuição de solicitação/ponto a ponto, ativada de MDM, preparados para SSL, etc.)

- Estatísticas de telemetria (momento da execução, tempo de execução, erros)

- Nível de telemetria configurado, de modo (online ou offline) e configuração de atualização rápida

- Utilização da deteção de rede (ativado ou desativado)
- Consola de administração:

     - Estatísticas sobre ligações de consolas (versão do sistema operativo, idioma, SKU e arquitetura, memória do sistema, contagem de processadores lógicos, ligar o ID do site, versões instaladas do .NET e pacotes de idiomas da consola)    

- Versão do SQL Server, nível de service pack, edição, ID de agrupamento e conjunto de carateres


##  <a name="bkmk_level2"></a> Nível 2 - Avançado
O nível de avançado é a predefinição após a conclusão da configuração. Este nível inclui dados que são recolhidos no nível básico e dados específicos da funcionalidade (frequência e duração de utilização), as definições de cliente do Configuration Manager (nome do componente, estado e determinadas definições como intervalos de consulta) e informações básicas sobre as atualizações de software.

Este nível é recomendado porque proporciona Microsoft com os dados mínimos necessário para melhorar o útil em futuras versões dos produtos e serviços. Este nível nomes de objetos não recolher (sites, os utilizadores, computadores ou objetos), os detalhes dos objetos relacionados com a segurança ou vulnerabilidades, como contagens dos sistemas que necessitam de atualizações de software.

Para o System Center Configuration Manager versão 1610, este nível inclui o seguinte:

-   **Gestão de aplicações:**  

    -    Informações de utilização/filtragem básica para tipos de implementação que são utilizados na organização (utilizador em comparação com o dispositivo de destino, necessário versus aplicações disponíveis e universais)  

    -   Informações de implementação de aplicação (instalar/desinstalar, necessita de aprovação, interação do utilizador ativado/desativado, dependências e substituições)  

    -   Estatísticas de pedidos de aplicação disponíveis  

    -   Contagem de pacotes por tipo  

    -   Contagem de aplicabilidade de aplicações por sistema operativo  

    -   Contagem de implementações de pacote/programa  

    -   Contagem de ambientes de App-V e propriedades de implementação  

    -   Contagem de licenças de aplicação licenciadas para Windows 10  

    -   Número de máximo/mínimo/média de implementações de aplicações por utilizador/dispositivo por período de tempo

    -   Tipo e duração da janela de manutenção  

    -  Estatísticas de tamanho e complexidade da política aplicação

    - ***[Atualizado] *** Contagem da loja Windows para aplicações empresariais e as estatísticas de sincronização (incluindo resumidos tipos de aplicações, licenciado estado da aplicação e o número de online e offline licenciado aplicações)  

    - Estatísticas de grupo de limites (quantos rápida, quantos mais lento e count por grupo de)

    - Opções de configuração do MSI e contagens

    - Requisitos da aplicação (contagem de condições incorporadas é referenciada por tecnologia de implementação)

    - Substituição de aplicações, profundidade máxima de cadeia

    - Utilização de dados. o Access (UDA) universal, como criado

    - ***[Novo] *** Frequência de estatísticas e a utilização de aprovação de aplicações



-   **Cliente:**  

    -   Lista/contagem de agentes de cliente ativados  

    -   Contagem de instalações de cliente a partir de cada tipo de localização de origem  

    -   Contagem de falhas de instalação de cliente  

    -  ***[Atualizado] *** a atualização automática de cliente: configuração de implementação, incluindo cliente piloting ou exclusão utilização (cliente de interoperabilidade expandida)

    -  Estatísticas de estado de funcionamento do cliente e o resumo do problema superior

    - Idade do BIOS em anos

    - Idade do sistema operativo em meses

    - Ações de contagem de centro de Software

    - Versão de cliente do Active Management Technology (AMT)

    - Erros de transferência de implementação do cliente

    - Notificação operação ação estado do cliente (quantas vezes é número de execução, máximo de clientes de destino e a taxa de êxito médio)

    - Métodos de implementação utilizados para o cliente e contagem de clientes por método de implementação

    - Configuração de tamanho de cache do cliente

    - ***[Novo] *** Número de classes de inventário de hardware, as regras de inventário de software e as regras de recolha de ficheiros




- **Serviços em nuvem:**

  - Contagem de coleções sincronizados para o conjunto de aplicações de gestão de operações

  -  Se o conector de nuvem do conjunto de aplicações do Operations Management está activado

  - ***[Novo] *** Estatísticas de configuração e a utilização da nuvem Management Gateway

  - ***[Novo] *** Contagem dos conectores de análise de atualização




- **Coleções:**

    -  Estatísticas de avaliação de coleção (hora de consulta, atribuída versus contagens não atribuídas, contagens por tipo, o rollover de ID e utilização de regras de)

    - Coleções sem uma implementação

    - Utilização de ID de coleção (não a ficar sem IDs)



-   **Definições de compatibilidade:**  

    -   Contagem de itens de configuração por tipo  

    -   Informações básicas de linha de base de configuração (contagem, número de implementações e número de referências)  

    -   Contagem de implementações que definições incorporadas de referência (agora capturar remediar definição)  

    -   Contagem de regras e às implementações criadas para definições personalizadas (agora capturar remediar definição)  
    -   Contagem de modelos de certificado de inscrição de protocolo SCEP (Simple), VPN, Wi-Fi, o certificado (. pfx) e política de conformidade implementadas

    -  Contagem do certificado de SCEP, VPN, Wi-Fi, o certificado (. pfx) e implementações de política de conformidade por plataforma

    - Passport para a política de trabalho (criados, implementado)



-   **Conteúdo:**  

    -   Contagem de limites por tipo  

    -   Informações sobre grupos de limites (contagem de limites e sistemas de sites que estão atribuídos a cada grupo de limites)  

    - ***[Novo] *** Relações de grupo de limites e a configuração de contingência

    -   Informações do grupo de ponto de distribuição (contagem de pacotes e os pontos de distribuição que estão atribuídos a cada grupo de pontos de distribuição)  

    -   Informações de configuração de ponto de distribuição (utilize da cache do ramo e monitorização do ponto de distribuição)  

    -   Informações de configuração do Gestor de distribuição (threads, intervalo entre repetições, número de tentativas e as definições do ponto de distribuição de extração)  

    - ***[Novo] *** Contagem de clientes de cache de elemento de rede e estatísticas de utilização

    - ***[Novo] *** Estatísticas de transferência de conteúdo de cliente


-   **Endpoint Protection:**  

    -   Antimalware do Endpoint Protection e a utilização de política de Firewall do Windows (número de políticas exclusivos atribuído ao grupo)<br /><br /> Isto não incluir quaisquer informações sobre as definições incluída na política.  

    -   Erros de implementação do Endpoint Protection (contagem de códigos de erro de implementação do Endpoint Protection política)  

    -   Contagem de coleções que estão selecionadas apareça no dashboard do Endpoint Protection  

    -   Contagem de alertas que estão configurados para a funcionalidade Endpoint Protection  

    -     Políticas de proteção de ameaça (ATP) avançadas (contagem de políticas e se as políticas estiverem implementadas)


- **Migração:**

  -   Contagem de objetos migrados (utilize do Assistente de migração)



-   **Gestão de dispositivos móveis (MDM):**  

    -   ***[Atualizado] *** Contar de emitido ações do dispositivo móvel: bloquear, afixe resto, apagar, extinguir e sincronizar agora comandos  

    -   Contagem de dispositivos móveis que são geridos pelo Configuration Manager e a Microsoft Intune e a forma como foram inscritos (em massa, baseada no utilizador)  

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

    -   Contagens de utilização de passo de sequência de tarefas

    - ***[Novo] *** Contagem das políticas de atualização de edição



-   **Atualizações de sites:**

    - Versões das correções instaladas do Configuration Manager




-   **Atualizações de Software:**  

    -   Total/Méd número de coleções que têm de implementações de atualizações de software e o número de máximo/média de atualizações implementadas  

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

    -   Classificações que são sincronizadas pelo ponto de atualização de Software

    -   Estatísticas de balanceamento de carga de ponto de atualização de software

    -  ***[Novo] *** Configuração do Windows 10 express atualizações




-   **Dados de desempenho/SQL:**  

    -   Contagem das maiores tabelas de bases de dados  

    -   ***[Atualizado] *** Estado de informações, a utilização e o estado de funcionamento da réplica SQL AlwaysOn

    -  Período de retenção do registo de alterações do SQL Server

    - Tipos de deteção, ativados e a agenda (completas, incrementais)

    - Estatísticas operacionais de deteção (número de objetos encontrado)

    - Problemas de desempenho, o período de retenção e o estado de auto-limpeza do registo de alterações do SQL Server



- **Diversas**

    - Contagem de sites com reativação na reativação por Lan (WOL)

    - ***[Novo] *** Reporting estatísticas de utilização e desempenho  



##  <a name="bkmk_level3"></a> Nível 3 - Completo
O nível de total inclui todos os dados nos níveis de básico e avançado. Também inclui informações adicionais sobre o Endpoint Protection, percentagens de compatibilidade de atualização e informações de atualização de software.  Este nível pode também incluir informações de diagnóstico avançadas, como ficheiros de sistema e instantâneos de memória que podem incluir informações pessoais que existiam na memória ou ficheiros de registo no momento da captura.

Para o System Center Configuration Manager versão 1610, este nível inclui o seguinte:

-   Estatísticas de avaliação e de atualização de coleções

-   Resumo do estado de funcionamento do Endpoint Protection (incluindo contagem de clientes protegidos, em risco, desconhecidos e não suportados)

-   Configuração da política do Endpoint Protection

-   Informações de implementação de atualização de software (percentagem de implementações que têm como destino com o cliente em oposição a hora UTC, necessário opcional versus automática e, a supressão de reinicialização)

-   Compatibilidade geral das implementações de atualizações de software

-   Informações de agenda de avaliação de regras de implementações automáticas

-   Contagens e códigos de erro de implementação de atualizações de software

-   Número máximo/mínimo/médio de clientes inativos em coleções de implementações de atualização de software

-   Contagem de grupos que já passaram da validade atualizações de software

-   Número máximo/mínimo/médio de atualizações de software por pacote

-   Percentagens de êxito de análise de atualização de software

-   Número máximo/mínimo/médio de horas desde a última análise de atualização de software

-    Produtos de atualização de software sincronizados com êxito pelo ponto de atualização de Software
-    Definições de compatibilidade: Detalhes de configuração de modelo SCEP, VPN, Wi-Fi e política de conformidade

-    Tipo de políticas de acesso condicional do EAS (bloco ou quarentena) para dispositivos que o Intune gere

-   Início 50 CPUs no ambiente do

-   Pacote de configuração de DCM para utilização do System Center Configuration Manager

-   Código de produto MSI (comuns as aplicações que implementar clientes)

-   Resumo do Estado de funcionamento ATP

-   Erros de instalação de implementação de cliente detalhadas

- ***[Novo] *** Loja Windows para detalhes da aplicação empresarial (lista de não agregado das aplicações sincronizadas incluindo AppID estado online ou offline e as contagens de licenças adquiridas total)

---
title: Dados de diagnóstico para 1702
titleSuffix: Configuration Manager
description: Saiba mais sobre os níveis de diagnósticos e dados de utilização recolhe do System Center Configuration Manager versão 1702.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d43ab033-2902-4681-8716-b4b17a6df372
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1a7b152b86eb622f389febfb17c313e9bffe93ac
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121765"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1702-of-system-center-configuration-manager"></a>Níveis de diagnóstico de utilização de recolha de dados para a versão 1702 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager versão 1702 recolhe três níveis de diagnósticos e dados de utilização: **Básica**, **avançada**, e **completa**. Por predefinição, esta funcionalidade está definida no nível Avançado. As secções seguintes fornecem detalhes adicionais sobre os dados que recolhe de cada nível.

Alterações das versões anteriores são indicadas com ***[novo]***, ***[atualizado]***, ***[removido]***, ou ***[movido]***.


> [!IMPORTANT]
>  O Configuration Manager não recolhe códigos de site, nomes de sites, endereços IP, nomes de utilizador, nomes de computador, endereços físicos ou endereços de e-mail nos níveis básico ou avançado. Qualquer recolha destas informações no nível completo não é intencional, ou seja, potencialmente incluídas nas informações de diagnóstico avançadas, como ficheiros de registo ou instantâneos de memória. Microsoft não utilizará estas informações para identificar, contactar ou desenvolver advertising.



##  <a name="bkmk_change"></a> Como alterar o nível
 Os administradores que tenham um âmbito de administração baseada em funções que inclua **modificar** permissões sobre o **Site** classe de objeto pode alterar o nível dos dados recolhidos nas definições de diagnóstico e dados de utilização na consola do Configuration Manager.

Alterar o nível de recolha de dados de dentro da consola ao navegar até **Administration** > **descrição geral** > **configuração do Site**  >  **Sites**. Open **definições de hierarquia**e, em seguida, selecione o nível de dados que pretende utilizar.  



##  <a name="bkmk_level1"></a> Nível 1 - Básico
O nível básico inclui dados sobre a hierarquia, os dados necessários para o ajudar a melhorar a sua instalação ou atualização de experiência e os dados que ajuda a determinar as atualizações do Configuration Manager que são aplicáveis para a sua hierarquia.

Para o System Center Configuration Manager versão 1702, este nível inclui o seguinte:

- Consola de administração:
   - Estatísticas sobre ligações de consolas (versão do sistema operativo, linguagem, SKU e arquitetura, memória do sistema, contagem de processadores lógicos, ligue o ID do site, versões de .NET instaladas e pacotes de idiomas da consola)

- Tipo de aplicação e a implantação básico contagens (total de aplicações, total de aplicações com vários tipos de implementação, aplicações de aplicativos no total com as dependências, total substituídas e contagem de tecnologias de implantação em utilização)

- Configuration Manager site hierarquia dados básicos (lista de sites, tipo, versão, estado, contagem de clientes e fuso horário)

- Configuração de base de dados básica (processadores, configuração de cluster e configuração de vistas distribuídas)

- ***[Atualizado]***  Estatísticas de deteção básica (deteção contagem máximo/mínimo/médio grupo tamanhos e), incluindo quando o site está em execução inteiramente com os serviços do Active Directory do Azure.

- Informações básicas do Endpoint Protection (versões de cliente de antimalware)

- Implementação de básica do sistema operativo (OSD) conta (imagens)

- Informações de servidor para sistema de site básico (funções de sistema de sites utilizadas, estado de Internet e o SSL, sistema operativo, processadores e máquina física ou virtual)

- Esquema de base de dados do Configuration Manager (hash de todas as definições de objetos)

- Nível de telemetria configurado, o modo (online ou offline) e configuração de atualização rápida

- Contagem de localidades e idiomas de cliente

- Versões de cliente de contagem do Configuration Manager e versões do sistema operativo

- Contagem de sistemas operativos para dispositivos geridos e políticas definidas pelo conector do Exchange

- Contagem de dispositivos Windows 10 por ramo e compilação

- Métricas de desempenho de bases de dados (informações de processamento de replicação, principais procedimentos armazenados do SQL Server por processador e utilização de disco)

- Ponto de distribuição e gestão de pontos de tipos e informações básicas de configuração (protegida, pré-configurado, PXE, multicast, estado SSL, pontos de distribuição de extração/ponto a ponto, compatível com MDM, habilitados para SSL, etc.)

- Informações de configuração:
     - Crie, instalar o tipo, pacotes de idiomas, funcionalidades ativadas por si   

     - Utilização da versão de pré-lançamento, o tipo de suporte de dados de configuração, o tipo do ramo

     - Data de expiração do Software Assurance      

     - Atualizar estado de implementação de pacote e erros, transfira o progresso e os erros de pré-requisitos     

     - Utilização de cadência rápida de atualização

     - Versão do script pós-atualização

- Versão do SQL, nível de service pack, edição, ID de agrupamento e o conjunto de carateres     
- Estatísticas de telemetria (momento da execução, tempo de execução, erros)

- Utilização da deteção de rede (ativada ou desativada)




##  <a name="bkmk_level2"></a> Nível 2 - Avançado
O nível avançado é a predefinição após a conclusão da configuração. Este nível inclui dados recolhidos no nível básico e dados específicos de funcionalidades (frequência e duração de utilização), as definições de cliente do Configuration Manager (nome do componente, estado e determinadas definições como intervalos de consulta) e informações básicas sobre atualizações de software.

Este nível é recomendado porque disponibiliza à Microsoft com os dados mínimos necessários para fazer melhorias úteis em versões futuras dos produtos e serviços. Nesse nível nomes de objetos não recolher (sites, utilizadores, computadores ou objetos), os detalhes dos objetos relacionados com segurança nem vulnerabilidades como contagens dos sistemas que necessitam de atualizações de software.

Para o System Center Configuration Manager versão 1702, este nível inclui o seguinte:

- **Gestão de aplicações:**  

   - Requisitos da aplicação (a contagem de condições incorporadas é referenciada por tecnologia de implantação)

   - Substituição de aplicações, profundidade máxima da cadeia

   - Frequência de utilização e estatísticas de aprovação de aplicações

   - ***[Atualizado]***  Informações de implementação de aplicação (utilizar instalação em comparação com a desinstalação, requer a aprovação, interação do utilizador ativado/desativado, a dependência, substituição e contagem de utilização da funcionalidade de comportamento de instalação)  

   - Estatísticas de tamanho e a complexidade de política de aplicação

   - Estatísticas de pedidos de aplicação disponíveis

   - ***[Novo]***  Informações básicas de configuração de pacotes e programas (opções de implementação e sinalizadores de programa)

   - Informações básicas de utilização/segmentação para tipos de implementação que são utilizados dentro da organização (utilizador em comparação com o dispositivo segmentado, necessário em comparação com as aplicações disponíveis e universais)

   - Estatísticas de grupo de limites (quantos mais rápidas e quantos lento e contagem por grupo)

   - Contagem de ambientes de App-V e propriedades de implementação

   - Contagem de aplicabilidade de aplicações por sistema operativo  

   - ***[Novo]***  Contagem de aplicações que são referenciados por uma sequência de tarefas

   - Contagem de pacotes por tipo  

   - Contagem de implementações de pacote/programa  

   - Contagem de licenças de aplicação licenciadas para Windows 10  

   - Contagem da Windows Store para aplicações de negócio e as estatísticas de sincronização (incluindo resumidos tipos de aplicações, licenciado o estado de aplicações e aplicações licenciadas do número de online e offline)  

   - Tipo e duração da janela de manutenção  

   - Número de máximo/mínimo/médio de implementações de aplicações por utilizador/dispositivo por período de tempo

   - ***[Novo]***  Mais comuns códigos de erro de instalação de aplicações através de uma tecnologia de implantação

   - Contagens e opções de configuração de MSI

   - ***[Novo]***  Estatísticas em interação do utilizador final com notificação para implementações de software necessárias   

   - Utilização universal de acesso de dados (UDA), como criado




- **Cliente:**  

   - Versão de cliente do Active Management Technology (AMT)

   - Idade de BIOS em anos

   - Atualização automática do cliente: configuração de implementação, incluindo a criação de piloto e de exclusão uso cliente (cliente de interoperabilidade expandido)

   - Configuração de tamanho de cache do cliente

   - Erros de transferência de implementação do cliente

   - Estatísticas de estado de funcionamento do cliente e o resumo do problema superior

   - Cliente notificação ação estado da operação (é de quantas vezes cada execução, Máx. número de clientes de destinados e a taxa média de êxito)
   - Contagem de instalações de cliente a partir de cada tipo de localização de origem  

   - Contagem de falhas de instalação de cliente  

   - ***[Novo]***  Contagem de dispositivos virtualizadas por Hyper-V ou do Azure  

   - Ações de contagem de centro de Software   

   - ***[Novo]***  Dispositivos ativados por contagem de UEFI

   - Métodos de implantação usados para cliente e a contagem de clientes por método de implementação

   - Lista/contagem de agentes de cliente ativados  

   - Idade de sistema operativo em meses

   - Número de classes de inventário de hardware, as regras de inventário de software e as regras de recolha de ficheiros

   - ***[Novo]***  Códigos de estatísticas de atestado de estado de funcionamento do dispositivo incluindo erro mais comuns, número de servidores no local e contagens de dispositivos em vários Estados.



- **Serviços cloud:**

  - Estatísticas de configuração e utilização do Gateway de gestão da Cloud

  - ***[Novo]***  Contagem de clientes associados ao Azure Active Directory Services

  - Contagem de coleções sincronizado com o Operations Management Suite

  - Contagem de conectores de análise de atualização

  - Se o conector de nuvem do Operations Management Suite está ativado




- **Coleções:**

    - Utilização de ID de coleção (não ficar sem IDs)

    - Estatísticas de avaliação de coleção (hora de consulta, atribuída versus contagens não atribuídas, contagens por tipo, o rollover de ID e o uso de regra)

    - Coleções sem uma implementação




- **Definições de compatibilidade:**  

    - Informações básicas de linha de base de configuração (contagem, número de implementações e número de referências)  

    - Contagem de itens de configuração por tipo  

    - Contagem de implementações que definições incorporadas de referência (agora capturar remediar definição)  

    - Contagem de regras e implementações criadas para as definições personalizadas (agora capturar remediar definição)  
    -  Contagem de modelos de certificado de protocolo SCEP (Simple Enrollment), VPN, Wi-Fi, certificado (. pfx) e política de conformidade implementadas

    - Contagem do certificado de SCEP, VPN, Wi-Fi, certificado (. pfx) e implementações de política de conformidade por plataforma

    - Passport para a política de trabalho (criado, implantado)



- **Conteúdo:**  

    - Informações do grupo de limites (contagem de limites e sistemas de sites que estão atribuídos a cada grupo de limites)  

    - As relações de grupo de limites e configuração de contingência

    - Estatísticas de transferência de conteúdo de cliente

    - Contagem de limites por tipo  

    - Contagem de clientes de cache ponto a ponto e estatísticas de utilização

    - Informações de configuração do Gestor de distribuição (threads, repita o atraso, número de repetições e as definições do ponto de distribuição de extração)  

    - Informações de configuração de ponto de distribuição (utilização da cache de ramificação e a monitorização do ponto de distribuição)

    - Informações do grupo de ponto de distribuição (contagem de pacotes e pontos de distribuição que são atribuídos a cada grupo de pontos de distribuição)  



- **Endpoint Protection:**  

   - Políticas de proteção contra ameaças (ATP) avançadas (contagem de políticas e se as políticas são implementadas)

   - Contagem de alertas que estão configurados para a funcionalidade Endpoint Protection  

   - Contagem de coleções que estão selecionadas para aparecerem no dashboard do Endpoint Protection  

   - Erros de implementação do Endpoint Protection (contagem de códigos de erro de implementação de política de proteção de ponto final)  

   - Antimalware do Endpoint Protection e utilização da política de Firewall do Windows (número de políticas únicas atribuídas ao grupo)<br /><br /> Não inclui quaisquer informações sobre as definições incluídas na política.  



- **Migração:**

  - Contagem de objetos migrados (utilização do Assistente de migração)



- **Gestão de dispositivos móveis (MDM):**  

    - Contagem de emitido ações do dispositivo móvel: bloquear, afixar rest, apagar, extinguir e, agora os comandos de sincronização

    - Contagem de políticas de dispositivos móveis  

    - Contagem de dispositivos móveis que são geridos pelo Configuration Manager e o Microsoft Intune e como foram inscritos (em massa, baseado no usuário)  

    - Contagem de utilizadores que têm vários dispositivos móveis inscritos  

    - Consulta de agenda e as estatísticas de duração de entrada de dispositivo móvel de dispositivos móveis  




- **Resolução de problemas do Microsoft Intune:**

    - Contagem e tamanho das ações do dispositivo (apagar, extinguir, bloquear) telemetria e mensagens de dados que são replicadas para o Microsoft Intune

    - Contagem e tamanho de estado, estado, inventário, RDR, DDR, UDX, inquilino mensagens de estado, POL, LOG, certificado, CRP, ressincronização, CFD, RDO, BEX, ISM e conformidade que são transferidas a partir do Microsoft Intune

    - Diferenciais e completas estatísticas de sincronizações de utilizador para o Microsoft Intune



- **Gestão de dispositivos móveis (MDM) no local:**  

    - Contagem de pacotes e perfis de inscrição em massa do Windows 10  

    - Estatísticas de êxito/falha de implementação para implementações de aplicações MDM no local  




- **Implementação do sistema operativo:**  

    - Contagem de imagens de arranque, controladores, pacotes de controladores, pontos de distribuição preparados com multicast ativado, pontos de distribuição com PXE ativado e sequências de tarefas  

    - Contagem de políticas de atualização de edição

    - Contagens de utilização de passo de sequência de tarefas



- **Atualizações do site:**

    - Versões das correções instaladas do Configuration Manager



- **Atualizações de Software:**  

    - Deltas disponíveis e de prazo que são utilizados nas regras de implementação automática  

    - Número médio e máximo de atribuições por atualização  

    - Avaliação de atualização de cliente e agendas de análise  

    - Classificações são sincronizadas pelo ponto de atualização de Software

    - Estatísticas de aplicação de patches de cluster  

    - Configuração de atualizações do Windows 10 express

    - Configurações que são utilizadas para o Active Directory Windows 10, planos de manutenção  

    - Contagem de atualizações do Office 365 implementadas  

    - Contagem de grupos de atualização e atribuições  

    - Contagem de pacotes de atualização e o número máximo/mínimo/médio de pontos de distribuição que são segmentados com pacotes  

    - Contagem de atualizações que são criados e implementados com o System Center Update Publisher  

    - Clientes de contagem do Windows 10 que utilizam o Windows Update para empresas  

    - Número de regras de implementação automática que estão associadas a sincronização  

    - Número de regras de implementação automática que criam atualizações novas ou acrescentam atualizações a um grupo existente  

    - Número de regras de implementação automática que têm várias implementações  
    - Número de grupos de atualização e número máximo/mínimo/médio de atualizações por grupo  

    - Número de atualizações e percentagem de atualizações que são implementadas, expiradas, substituídas, transferidas e contêm EULAs  

    - Estatísticas de balanceamento de carga de ponto de atualização de software

    - Agenda de sincronização de ponto de atualização de software  

    - Número total/médio de coleções com implementações de atualizações de software e o número máximo/médio de implementar atualizações  

    - Atualizar códigos de erro de análise e contagem de máquinas  

    - Versões de conteúdo de dashboard do Windows 10  



- **Dados de desempenho/SQL:**  

    - ***[Novo]***  Configuração e a duração do resumo de site

    - Contagem das maiores tabelas de bases de dados  

    - Estatísticas operacionais de deteção (contagem de foram encontrados objetos)

    - Tipos de deteção, ativados e a agenda (completos e incrementais)

    - Estado de informações, utilização e estado de funcionamento da réplica SQL AlwaysOn

    - Controlo de problemas de desempenho, o período de retenção e o estado de limpeza automática de alterações do SQL

    - Período de retenção de registo de alterações SQL

    - ***[Novo]***  Estatísticas de desempenho, incluindo tipos de mensagens mais comuns e mais caros de mensagens de estado e Estado



- **Diversos**

    - ***[Novo]***  Configuração do armazém de ponto de serviço dados incluindo a hora de agendamento e a média de sincronização

    - Contagem de sites com reativação em Lan (WOL)

    - Relatório de estatísticas de utilização e desempenho  



##  <a name="bkmk_level3"></a> Nível 3 - Completo
O nível completo inclui todos os dados nos níveis de básico e avançado. Também inclui informações adicionais sobre o Endpoint Protection, percentagens de compatibilidade de atualização e informações de atualização de software.  Este nível também pode incluir informações de diagnóstico avançadas, como ficheiros de sistema e instantâneos de memória que podem incluir informações pessoais que existiam na memória ou ficheiros de registo no momento da captura.

Para o System Center Configuration Manager versão 1702, este nível inclui o seguinte:

- Informações de agenda de avaliação de regras de implementações automáticas

- Resumo do Estado de funcionamento do ATP

- Estatísticas de avaliação e de atualização de coleções

- Definições de compatibilidade: Detalhes de configuração de modelo contagem de grupos que têm atualizações de software expiradas de SCEP, VPN, Wi-Fi e política de conformidade

- Pacote de configuração do DCM para utilização do System Center Configuration Manager

- Erros de instalação de implementação detalhadas do cliente
- Resumo do estado de funcionamento do Endpoint Protection (incluindo contagem de clientes protegidos, em risco, desconhecidos e não suportados)

- Configuração da política do Endpoint Protection

- ***[Novo]***  Lista de processos configurado com o comportamento de instalação para aplicações

- Número máximo/mínimo/médio de horas desde a última análise de atualização de software

- Número máximo/mínimo/médio de clientes inativos em coleções de implementações de atualização de software

- Número máximo/mínimo/médio de atualizações de software por pacote

- Código de produto MSI (aplicações comuns que os clientes implementar)

- Compatibilidade geral das implementações de atualizações de software

- Contagens e códigos de erro de implementação de atualizações de software

- Informações de implementação de atualizações de software (percentagem das implementações que são visados com o cliente em relação a hora UTC, necessário opcional versus silencioso e supressão de reinício)

- Produtos de atualização de software sincronizados pelo ponto de atualização de Software

- Percentagens de êxito de análise de atualização de software

- CPUs de 50 principais no ambiente

- Tipo de políticas de acesso condicional do EAS (bloqueio ou quarentena) para dispositivos que gere o Intune

- Windows Store para detalhes de aplicativo de negócios (não é de agregação lista de aplicativos sincronizados, incluindo AppID, o estado online ou o estado offline e contagens de licenças adquiridas total)

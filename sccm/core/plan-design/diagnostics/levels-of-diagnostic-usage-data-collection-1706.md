---
title: "Dados de diagnóstico para 1706"
titleSuffix: Configuration Manager
description: "Saiba mais sobre os níveis de diagnósticos e dados de utilização que o System Center Configuration Manager versão 1706 recolhe."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 14ee4fb0-7790-45a6-906e-6e55627d4079
caps.latest.revision: 
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
ms.openlocfilehash: 759579ea3a76b05460a3e2dbad595844bd182cb6
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1706-of-system-center-configuration-manager"></a>Níveis de diagnóstico de utilização de recolha de dados para a versão 1706 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager versão 1706 recolhe três níveis de diagnósticos e dados de utilização: **Básico**, **avançada**, e **completa**. Por predefinição, esta funcionalidade está definida no nível Avançado. As secções seguintes fornecem detalhes adicionais sobre os dados que recolhe de cada nível.

As alterações de versões anteriores são assinaladas com ***[New]***, ***[atualizado]***, ***[removida]***, ou ***[movido]***.


> [!IMPORTANT]
>  O Configuration Manager não recolhe códigos de site, os nomes de sites, endereços IP, nomes de utilizador, nomes de computador, endereços físicos ou endereços de correio eletrónico nos níveis básico ou avançado. Qualquer recolha destas informações no nível completo não é tem um fim específico, ou seja, potencialmente incluídas nas informações de diagnóstico avançadas, como ficheiros de registo ou instantâneos de memória. Microsoft não utilizará estas informações para identificar, contactar ou desenvolver publicidade.



##  <a name="bkmk_change"></a> Como alterar o nível
 Os administradores que tenham um âmbito de administração baseada em funções que inclua **modificar** permissões a **Site** classe de objeto pode alterar o nível dos dados recolhidos nas definições de diagnóstico e dados de utilização na consola do Configuration Manager.

Alterar o nível de recolha de dados de dentro da consola, navegando até **administração** > **descrição geral** > **configuração do Site** > **Sites**. Abra **definições de hierarquia**e, em seguida, selecione o nível de dados que pretende utilizar.  



##  <a name="bkmk_level1"></a> Nível 1 - Básico
O nível básico inclui dados sobre a sua hierarquia, dados necessárias para ajudar a melhorar a sua instalação ou atualização experiência e os dados que ajuda a determinar as atualizações do Configuration Manager que são aplicáveis para a sua hierarquia.

Para o System Center Configuration Manager versão 1706, este nível inclui o seguinte:

- Consola de administração:
   - Estatísticas sobre as ligações da consola (versão do sistema operativo, idioma, SKU e arquitetura, memória do sistema, contagem de processadores lógicos, ligar o ID do site, versões de .NET instaladas e pacotes de idiomas da consola)

- Contagens de tipo de implementação e de aplicação básico (total de aplicações, total de aplicações com vários tipos de implementação, as aplicações de total de aplicações com dependências, totais substituídas e contagem de tecnologias de implementação em utilização)

- Básico do Configuration Manager hierarquia dados do site (lista de sites, tipo, versão, estado, contagem de clientes e fuso horário)

- Configuração de base de dados básica (processadores, configuração de cluster e a configuração das vistas distribuídas)

- Estatísticas básicas de deteção (deteção contagem e máximo/mínimo/médio tamanhos de grupos), incluindo quando o site está em execução inteiramente com serviços de diretório do Azure Active Directory.

- Informações básicas do Endpoint Protection (versões de cliente antimalware)

- Implementação básica do sistema operativo (OSD) conta (imagens)

- ***[Atualizado]***  Informações de servidor de sistema básico do site (funções de sistema de sites utilizadas, estado e SSL da Internet, sistema operativo, processadores, físico ou máquina virtual e utilização de elevada disponibilidade do servidor de site)

- Esquema de base de dados do Configuration Manager (hash de todas as definições de objetos)

- Nível de telemetria configurado, modo (online ou offline) e a configuração de atualização rápida

- Contagem de idiomas de cliente e regiões

- Versões de cliente de contagem do Configuration Manager e versões do sistema operativo

- Contagem de sistemas operativos para dispositivos geridos e políticas definidas pelo conector do Exchange

- Contagem de dispositivos Windows 10 por ramo e compilação

- Métricas de desempenho de bases de dados (informações de processamento de replicação, principais procedimentos armazenados do SQL Server por processador e utilização de disco)

- Ponto de distribuição e ponto de gestão tipos e informações básicas de configuração (protegida, pré-configurado, PXE, multicast, estado SSL, pontos de distribuição de extração/ponto a ponto, MDM ativado, com SSL ativado, etc.)

- ***[Novo]***  Hashed lista de extensões para páginas de propriedades de consola de administração e assistentes

- Informações de configuração:
     - Criar, instalar o tipo, pacotes de idiomas, funcionalidades que tiver ativado   

     - Utilização de pré-lançamento, o tipo de suporte de dados de configuração, o tipo de sucursais

     - Data de expiração do Software Assurance      

     - Atualizar o estado de implementação de pacote e erros, transfira o progresso e erros de pré-requisitos     

     - Utilização do anel rápida de atualização

     - Versão do script pós-atualização

- Versão do SQL, nível de service pack, edição, ID de agrupamento e conjunto de carateres     
- Estatísticas de telemetria (momento da execução, tempo de execução, erros)

- Utilização da deteção de rede (ativada ou desativada)




##  <a name="bkmk_level2"></a> Nível 2 - Avançado
O nível avançado é a predefinição após a conclusão da configuração. Este nível inclui dados recolhidos no nível básico e dados específicos da funcionalidade (frequência e duração de utilização), definições de cliente do Configuration Manager (nome do componente, estado e determinadas definições como intervalos de consulta) e informações básicas sobre atualizações de software.

Este nível é recomendado porque disponibiliza à Microsoft os dados mínimos necessárias para fazer melhorias úteis em futuras versões dos produtos e serviços. Este nível nomes de objeto não recolher (sites, os utilizadores, computador ou objetos), detalhes de objetos relacionados com segurança nem vulnerabilidades como contagens dos sistemas que necessitam de atualizações de software.

Para o System Center Configuration Manager versão 1706, este nível inclui o seguinte:

- **Gestão de aplicações:**  

   - Requisitos de aplicações (contagem de condições incorporadas é referenciada por tecnologia de implementação)

   - Substituição de aplicações, profundidade máxima de cadeia

   - Frequência de utilização e estatísticas de aprovação de aplicações

   - ***[Novo]***  Estatísticas de tamanho do conteúdo da aplicação

   - Informações de implementação de aplicação (utilizar instalação em comparação com a desinstalação, necessita de aprovação, interação do utilizador ativada/desativada, dependência, substituição e contagem de utilização da funcionalidade do comportamento de instalação)  

   - Política tamanho e complexidade das estatísticas da aplicação

   - Estatísticas de pedidos de aplicação disponíveis

   - Informações de configuração básica de pacotes e programas (opções de implementação e sinalizadores de programa)

   - Informações básicas de utilização/segmentação para tipos de implementação que são utilizados na sua organização (utilizador versus dispositivo segmentado, necessário versus aplicações disponíveis e universais)

   - Estatísticas de grupo de limites (quantos rápido, quantos lenta e count por grupo de)

   - Contagem de ambientes de App-V e propriedades de implementação

   - Contagem de aplicabilidade de aplicações por sistema operativo  

   - Contagem de aplicações que são referenciados por uma sequência de tarefas

   - ***[Novo]***  Contagem de imagem corporativa distintos do catálogo de aplicações

   - ***[Novo]***  Criadas com o dashboard de aplicações de contagem do Office 365

   - Contagem de pacotes por tipo  

   - Contagem de implementações de pacote/programa  

   - Contagem de licenças de aplicação licenciadas para Windows 10  

   - ***[Novo]***  Tipos de implementação de contagem do Windows Installer desinstalar por definições de conteúdo

   - Contagem da loja Windows para aplicações empresariais e estatísticas de sincronização (incluindo resumidos tipos de aplicações, licenciado estado da aplicação e o número de online e offline licenciado aplicações)  

   - Tipo e duração da janela de manutenção  

   - Número máximo/mínimo/médio de implementações de aplicações por utilizador/dispositivo por período de tempo

   - Mais comuns códigos de erro de instalação de aplicações através da tecnologia de implementação

   - Contagens e opções de configuração de MSI

   - Estatísticas de interação do utilizador final com a notificação para implementações de software necessárias   

   - Utilização de acesso de dados (UDA) universal, como criado




- **Cliente:**  

   - Versão de cliente do Active Management Technology (AMT)

   - Idade do BIOS no anos
   
   - ***[Novo]***  Contagem de dispositivos com o arranque seguro ativado
   
   - ***[Novo]***  Contagem de dispositivos por Estado TPM

   - A atualização automática de cliente: configuração de implementação, incluindo pilotagem e exclusão de utilização de cliente (cliente de interoperabilidade expandido)

   - Configuração de tamanho de cache do cliente

   - Erros de transferência de implementação do cliente

   - Estatísticas de estado de funcionamento do cliente e o resumo do problema superior

   - Notificação operação ação estado do cliente (o quantas vezes é o número de execução, máximo de clientes alvo e a taxa de êxito médio)
   - Contagem de instalações de cliente a partir de cada tipo de localização de origem  

   - Contagem de falhas de instalação de cliente  

   - Contagem de dispositivos virtualizado pelo Hyper-V ou do Azure  

   - Ações de contagem de centro de Software   

   - Contagem de dispositivos ativados por UEFI

   - Métodos de implementação de cliente e a contagem de clientes por método de implementação

   - Lista/contagem de agentes de cliente ativados  

   - Idade do sistema operativo nos meses

   - Número de classes de inventário de hardware, as regras de inventário de software e regras de recolha de ficheiros

   - Estatísticas para fins de atestado do Estado de funcionamento de dispositivos, incluindo mais comuns códigos de erro, número de servidores no local e o número de dispositivos em vários Estados.



- **Serviços de cloud:**

  - ***[Novo]***  Estatísticas de deteção do azure Active Directory

  - ***[Atualizado]***  Estatísticas de configuração e utilização do Gateway de gestão de nuvem, incluindo contagens dos ambientes e regiões e estatísticas de autenticação/autorização

  - ***[Novo]***  Contagem do Azure Active Directory aplicações e serviços ligados para o Configuration Manager

  - Contagem de clientes associados a serviços de diretório do Azure Active Directory

  - Contagem das coleções sincronizados para o Operations Management Suite

  - Contagem de conectores de análise de atualização

  - Indica se o conector em nuvem do Operations Management Suite está ativado





- **Coleções:**

    - Utilização de ID de coleção (não a ficar sem IDs)

    - Estatísticas de avaliação de coleção (hora de consulta, atribuída versus contagens não atribuídas, contagens por tipo, rollover de ID e a utilização de regra)

    - Coleções sem uma implementação




- **Definições de compatibilidade:**  

    - Informações básicas de linha de base de configuração (contagem, número de implementações e número de referências)

    - ***[Novo]***  Estatísticas de erro de política de conformidade

    - Contagem de itens de configuração por tipo  

    - Contagem de implementações que definições incorporadas de referência (agora capturar remediar definição)  

    - Contagem de regras e implementações criadas para as definições personalizadas (agora capturar remediar definição)  
    -  Contagem de modelos de certificado de inscrição de SCEP (Simple Protocol), VPN, Wi-Fi, certificado (. pfx) e política de conformidade implementadas

    - Contagem do certificado de SCEP, VPN, Wi-Fi, certificado (. pfx) e implementações de política de conformidade por plataforma

    - Passport para a política de trabalho (criado, implementado)



- **Conteúdo:**  

    - Informações sobre grupos de limites (contagem de limites e sistemas de sites que estão atribuídos a cada grupo de limites)  

    - Relações de grupo de limites e a configuração de contingência

    - Estatísticas de transferência do conteúdo de cliente

    - Contagem de limites por tipo  

    - ***[Atualizado]***  Contagem de clientes de cache ponto a ponto, estatística de utilização e estatísticas de transferência parcial

    - Informações de configuração do Gestor de distribuição (threads, repita o atraso, número de tentativas e as definições do ponto de distribuição de extração)  

    - Informações de configuração de ponto de distribuição (utilização da cache de ramo e monitorização do ponto de distribuição)

    - Informações do grupo de ponto de distribuição (contagem de pacotes e pontos de distribuição que estão atribuídos a cada grupo de pontos de distribuição)  



- **Endpoint Protection:**  

   - Políticas de proteção de ameaça (ATP) avançadas (contagem de políticas e se as políticas são implementadas)

   - Contagem de alertas que estão configurados para a funcionalidade Endpoint Protection  

   - Contagem de coleções que estão selecionadas para aparecerem no dashboard do Endpoint Protection  

   - Erros de implementação do Endpoint Protection (contagem de códigos de erro de implementação de política do Endpoint Protection)  

   - Antimalware do Endpoint Protection e a utilização da política de Firewall do Windows (número de políticas únicas atribuídas ao grupo)<br /><br /> Isto inclui qualquer informação sobre as definições incluídas na política.  



- **Migração:**

  - Contagem de objetos migrados (utilize do Assistente de migração)



- **Gestão de dispositivos móveis (MDM):**  

    - Número de emitido ações do dispositivo móvel: bloquear, afixar rest, apagar, extinguir e sincronizar agora comandos

    - Contagem de políticas de dispositivos móveis  

    - Contagem de dispositivos móveis que são geridos pelo Configuration Manager e Microsoft Intune e como foram inscritos (em massa, baseado no utilizador)  

    - Contagem de utilizadores que têm vários dispositivos móveis inscritos  

    - Consulta de agenda e as estatísticas de duração de verificação de dispositivos móveis de dispositivos móveis  




- **Resolução de problemas de Microsoft Intune:**

    - Contagem e tamanho das ações do dispositivo (apagar, extinguir, bloquear) telemetria e mensagens de dados que são replicadas para o Microsoft Intune

    - Contagem e tamanho de estado, o estado, inventário, RDR, DDR, UDX, inquilino mensagens de estado, POL, registo, certificado, CRP, ressincronização, CFD, RDO, BEX, ISM e conformidade que são transferidas a partir do Microsoft Intune

    - Diferenciais e completas estatísticas de sincronização de utilizador para o Microsoft Intune



- **Gestão de dispositivos móveis (MDM) no local:**  

    - Contagem de pacotes e perfis de inscrição em massa do Windows 10  

    - Estatísticas de êxito/falha de implementação para implementações de aplicações MDM no local  




- **Implementação do sistema operativo:**  

    - Contagem de imagens de arranque, controladores, pacotes de controladores, pontos de distribuição preparados com multicast ativado, pontos de distribuição com PXE ativado e sequências de tarefas  

    - ***[Novo]***  Imagens de contagem de arranque pela versão de cliente do Configuration Manager

    - ***[Novo]***  Imagens de contagem de arranque pela versão do Windows PE

    - Contagem de políticas de atualização de edição

    - ***[Novo]***  Contagem de identificadores de hardware excluídos PXE

    - ***[Novo]***  Contagem de implementações de sequência de tarefas utilizando a opção para transferir o conteúdo previamente

    - Contagens de utilização de passo de sequência de tarefas

    - ***[Novo]***  Versão do Windows ADK instalado


- **Atualizações de sites:**

    - Versões das correções instaladas do Configuration Manager



- **Atualizações de Software:**  

    - Disponível e o prazo deltas que são utilizados em regras de implementação automática  

    - Número médio e máximo de atribuições por atualização  

    - Avaliação de atualização de cliente e agendas de análise  

    - Classificações são sincronizadas pelo ponto de atualização de Software

    - Estatísticas de aplicação de patches de cluster  

    - Configuração de atualizações do Windows 10 express

    - Configurações que são utilizadas para o Active Directory Windows 10, planos de manutenção  

    - Contagem de atualizações do Office 365 implementadas  

    - ***[Novo]***  Controladores de contagem de superfície da Microsoft sincronizadas

    - Contagem de grupos de atualização e atribuições  

    - Contagem de pacotes de atualização e o número máximo/mínimo/médio de pontos de distribuição são segmentados com pacotes  

    - Contagem das atualizações que são criados e implementados com o System Center Update Publisher  

    - Clientes de contagem do Windows 10 que utilizam o Windows Update para empresas  

    - ***[Novo]***  Contagem do Windows Update para criar e implementar as políticas de negócio

    - Número de regras de implementação automática que estão associadas a sincronização  

    - Número de regras de implementação automática que criam atualizações novas ou acrescentam atualizações a um grupo existente  

    - Número de regras de implementação automática com várias implementações  
    - Número de grupos de atualização e número máximo/mínimo/médio de atualizações por grupo  

    - Número de atualizações e percentagem de atualizações que são implementadas, expiradas, substituídas, transferidas e contenham contêm EULAs  

    - Estatísticas de balanceamento de carga de ponto de atualização de software

    - Agenda de sincronização de ponto de atualização de software  

    - Número total/médio de coleções com implementações de atualização de software e o número máximo/médio de implementação de atualizações  

    - Atualizar códigos de erro de análise e contagem de máquinas  

    - Versões de conteúdo de dashboard do Windows 10  



- **Dados de desempenho/SQL:**  

    - ***[Novo]***  Configuração e a duração do resumo de site

    - Contagem das maiores tabelas de bases de dados  

    - Estatísticas de deteção operacionais (contagem de objetos encontrado)

    - Tipos de deteção, ativados e o agendamento (completo, incremental)

    - Estado de informações, utilização e estado de funcionamento da réplica SQL AlwaysOn

    - Problemas de desempenho, o período de retenção e o estado de automático limpeza o registo de alterações do SQL Server

    - Período de retenção de registo de alterações SQL

    - Estatísticas de desempenho, incluindo os tipos de mensagens mais comuns e mais dispendiosos de mensagens de estado



- **Diversas**

    - Configuração do ponto de serviço de armazém de dados, incluindo a hora de agendamento e a média de sincronização

    - ***[Novo]***  Contagem de Scripts e estatísticas de execução

    - Contagem de sites com reativação numa Lan (WOL)

    - Relatório de estatísticas de utilização e desempenho  



##  <a name="bkmk_level3"></a> Nível 3 - Completo
O nível completo inclui todos os dados os níveis básico e avançado. Também inclui informações adicionais sobre o Endpoint Protection, percentagens de compatibilidade de atualização e informações de atualização de software.  Este nível também pode incluir informações de diagnóstico avançadas como instantâneos de memória que podem incluir informações pessoais que existiam na memória ou ficheiros de registo no momento da captura e de ficheiros de sistema.

Para o System Center Configuration Manager versão 1706, este nível inclui o seguinte:

- Informações de agenda de avaliação de regras de implementações automáticas

- Resumo do Estado de funcionamento ATP

- Estatísticas de avaliação e de atualização de coleções

- ***[Novo]***  Estatísticas de política de conformidade de erros e de conformidade

- Definições de compatibilidade: Detalhes de configuração de modelo contagem de grupos que têm atualizações de software expiradas de SCEP, VPN, Wi-Fi e política de conformidade

- Pacote de configuração de DCM para utilização do System Center Configuration Manager

- Erros de instalação de implementação do cliente de detalhado

- Resumo do estado de funcionamento do Endpoint Protection (incluindo contagem de clientes protegidos, em risco, desconhecidos e não suportados)

- Configuração da política do Endpoint Protection

- Lista de processos configurados com o comportamento de instalação de aplicações

- Número máximo/mínimo/médio de horas desde a última análise de atualização de software

- Número máximo/mínimo/médio de clientes inativos em coleções de implementações de atualização de software

- Número máximo/mínimo/médio de atualizações de software por pacote

- Código de produto MSI (aplicações comuns que os clientes implementar)

- Compatibilidade geral das implementações de atualizações de software

- Contagens e códigos de erro de implementação de atualizações de software

- Informações de implementação de atualização de software (percentagem das implementações direcionadas com o cliente em comparação com a hora UTC, necessário opcional versus silencioso e supressão de reinício)

- Produtos de atualização de software sincronizados com êxito pelo ponto de atualização de Software

- Percentagens de êxito de análise de atualização de software

- Principais 50 CPUs no ambiente

- Tipo de políticas de acesso condicional do EAS (bloquear ou colocar em quarentena) para dispositivos que gere o Intune

- Loja Windows para detalhes de negócio da aplicação (não sejam de agregação lista de aplicações sincronizadas, incluindo AppID, o estado online ou o estado offline e contagens de licenças adquiridas total)

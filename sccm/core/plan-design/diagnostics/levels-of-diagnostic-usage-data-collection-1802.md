---
title: Dados de diagnóstico e utilização para 1802
titleSuffix: Configuration Manager
description: Saiba mais sobre os níveis de diagnósticos e dados de utilização recolhidos na versão 1802.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 29dd51b8-6576-4010-81ba-3129ed2c3421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 561fd23795d52debe0304fa16fd07234dc63e4c2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1802-of-system-center-configuration-manager"></a>Níveis de diagnóstico de utilização de recolha de dados para a versão 1802 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager versão 1802 recolhe três níveis de diagnósticos e dados de utilização: **Básico**, **avançada**, e **completa**. Por predefinição, esta funcionalidade está definida no nível Avançado. As secções seguintes fornecem detalhes adicionais sobre dados recolhidos em cada nível.

As alterações de versões anteriores são assinaladas com ***[New]***, ***[atualizado]***, ***[removida]***, ou ***[movido]***.


> [!IMPORTANT]
>  Do Configuration Manager não recolhe códigos de site, os nomes de sites, endereços IP, nomes de utilizador, nomes de computador, endereços físicos ou endereços de correio eletrónico nos níveis básico ou avançado. Qualquer recolha destas informações no nível completo não é tem um fim específico. Potencialmente está incluído na informações de diagnóstico avançadas, como ficheiros de registo ou instantâneos de memória. A Microsoft não utiliza estas informações para identificar, contactar ou desenvolver publicidade.



##  <a name="bkmk_change"></a> Como alterar o nível
 Os administradores que tenham um âmbito de administração baseada em funções que inclua **modificar** permissões a **Site** classe de objeto pode alterar o nível dos dados recolhidos nas definições de diagnóstico e dados de utilização na consola do Configuration Manager.

Alterar o nível de recolha de dados de dentro da consola, navegando até **administração** > **descrição geral** > **configuração do Site** > **Sites**. Abra **definições de hierarquia**e, em seguida, selecione o nível de dados que pretende utilizar.  



##  <a name="bkmk_level1"></a> Nível 1 - Básico
O nível básico inclui dados sobre a sua hierarquia, dados necessárias para ajudar a melhorar a sua instalação ou atualização experiência e os dados que ajuda a determinar as atualizações do Configuration Manager que são aplicáveis para a sua hierarquia.

Para o Configuration Manager versão 1802, este nível inclui os seguintes dados:

- Estatísticas sobre as ligações da consola do Configuration Manager: Versão do SO, idioma, SKU e arquitetura, memória do sistema, contagem de processadores lógicos, ligar o ID do site, versões de .NET instaladas e pacotes de idiomas da consola

- Aplicação básica e tipo de implementação contagens: total de aplicações, total de aplicações com vários tipos de implementação, as aplicações de total de aplicações com dependências, totais substituídas e contagem de tecnologias de implementação em utilização

- Dados de hierarquia de site do Configuration Manager básico: lista, tipo, versão, estado, contagem de clientes e fuso horário do site

- Configuração de base de dados básica: processadores, a configuração de cluster e a configuração das vistas distribuídas

- Estatísticas básicas da deteção: contagem de deteção, tamanhos de máximo/mínimo/médio de grupo, e quando o site está em execução inteiramente com serviços de diretório do Azure Active Directory

- Informações básicas do Endpoint Protection sobre as versões de cliente antimalware

- Implementação básica do SO contagens de imagens

- Informações do servidor de sistema de sites básico: funções do sistema utilizadas, internet e estado SSL, SO, processadores, físico ou máquina virtual e utilização de elevada disponibilidade do servidor de site do site

- Esquema de base de dados do Configuration Manager (hash de todas as definições de objetos)

- Nível de telemetria configurado, modo online ou offline e da configuração rápida de atualização

- Contagem de idiomas de cliente e regiões

- Versões de cliente de contagem do Configuration Manager, as versões do SO e versões do Office

- Contagem de sistemas operativos para dispositivos geridos e políticas definidas pelo conector do Exchange

- Contagem de dispositivos Windows 10 por ramo e compilação

- ***[Movido]***  Clientes de contagem do Windows 10 que utilizam o Windows Update para empresas  

- Métricas de desempenho de base de dados: replicação processar informações, principais procedimentos armazenados do SQL Server por processador e utilização do disco

- Ponto de distribuição e ponto de gestão tipos e informações de configuração básica: protegidos, pré-configurado, PXE, multicast, estado SSL, pontos de distribuição de extração/ponto a ponto, MDM ativado e SSL ativado

- Hash de lista de extensões para páginas de propriedades de consola de administração e assistentes

- Informações de configuração:
     - Criar, instalar o tipo, pacotes de idiomas, funcionalidades que tiver ativado   

     - Utilização de pré-lançamento, o tipo de suporte de dados de configuração, o tipo de sucursais

     - Data de expiração do Software Assurance      

     - Atualizar o estado de implementação de pacote e erros, transfira o progresso e erros de pré-requisitos     

     - Utilização do anel rápida de atualização

     - Versão do script pós-atualização

- Versão do SQL, nível de service pack, edição, ID de agrupamento e conjunto de carateres     

- Estatísticas de telemetria: quando executada, tempo de execução, erros

- Se a deteção de rede está ativada ou desativada

- ***[Movido]***  Contagem de clientes associados ao Azure Active Directory

- ***[Novo]***  Contagem de implementações faseadas criadas por tipo

- ***[Novo]***  Contagem de clientes de interoperabilidade expandida

- ***[Novo]***  Hashed lista de propriedades de inventário de hardware mais de 255 carateres



##  <a name="bkmk_level2"></a> Nível 2 - Avançado
O nível avançado é a predefinição após a conclusão da configuração. Este nível inclui dados recolhidos no nível básico e dados específicos da funcionalidade (frequência e duração de utilização), definições de cliente do Configuration Manager (nome do componente, estado e determinadas definições como intervalos de consulta) e informações básicas sobre atualizações de software.

Este nível é recomendado porque disponibiliza à Microsoft os dados mínimos necessárias para fazer melhorias úteis em futuras versões dos produtos e serviços. Este nível nomes de objeto não recolher (sites, os utilizadores, computador ou objetos), detalhes de objetos relacionados com segurança nem vulnerabilidades como contagens dos sistemas que necessitam de atualizações de software.

Para o Configuration Manager versão 1802, este nível inclui os seguintes dados:

### <a name="application-management"></a>Gestão de aplicações  

   - Requisitos da aplicação: contagem de condições incorporadas referenciada por tecnologia de implementação

   - Substituição de aplicações, profundidade máxima de cadeia

   - Frequência de utilização e estatísticas de aprovação de aplicações

   - Estatísticas de tamanho do conteúdo da aplicação

   - Informações de implementação de aplicação: a utilização de instalação versus desinstalar, necessita de aprovação, interação do utilizador ativada/desativada, dependência, substituição e contagem de utilização da funcionalidade do comportamento de instalação  

   - Política tamanho e complexidade das estatísticas da aplicação

   - Estatísticas de pedidos de aplicação disponíveis

   - Informações de configuração básica de pacotes e programas: opções de implementação e sinalizadores de programa

   - Informações básicas de utilização/segmentação para tipos de implementação: utilizador versus dispositivo segmentado, necessário em comparação com as aplicações disponíveis e universais

   - Contagem de ambientes de App-V e propriedades de implementação

   - Contagem de aplicabilidade de aplicações pelo SO  

   - Contagem de aplicações que são referenciados por uma sequência de tarefas

   - Contagem de imagem corporativa distintos do catálogo de aplicações

   - Criados com o dashboard de aplicações de contagem do Office 365

   - Contagem de pacotes por tipo  

   - Contagem de implementações de pacote/programa  

   - Contagem de licenças de aplicação licenciadas para Windows 10  

   - Tipos de implementação de contagem do Windows Installer por desinstalar definições de conteúdo

   - Contagem do Microsoft Store para aplicações empresariais e estatísticas de sincronização: resumidos tipos de aplicações, o estado de aplicação licenciadas e o número de online e offline licenciado aplicações  

   - Tipo e duração da janela de manutenção  

   - Número máximo/mínimo/médio de implementações de aplicações por utilizador/dispositivo por período de tempo

   - Mais comuns códigos de erro de instalação de aplicações através da tecnologia de implementação

   - Contagens e opções de configuração de MSI

   - Estatísticas de interação do utilizador final com a notificação para implementações de software necessárias   

   - Utilização de acesso a dados universal, como criado

   - ***[Novo]***  Estatísticas agregadas afinidade dispositivo / utilizador 

   - ***[Novo]***  Máxima e média utilizadores primários por dispositivo


### <a name="client"></a>Cliente  

   - Versão de cliente do Active Management Technology (AMT)

   - Idade do BIOS no anos

   - Contagem de dispositivos com o arranque seguro ativado

   - Contagem de dispositivos por Estado TPM

   - A atualização automática de cliente: configuração de implementação, incluindo pilotagem e exclusão de utilização de cliente (cliente de interoperabilidade expandido)

   - Configuração de tamanho de cache do cliente

   - Erros de transferência de implementação do cliente

   - Estatísticas de estado de funcionamento do cliente e o resumo do problema superior

   - Estado de ação da operação de notificação de cliente: quantas vezes é o número de execução, máximo de clientes alvo e a taxa de êxito médio

   - Contagem de instalações de cliente a partir de cada tipo de localização de origem  

   - Contagem de falhas de instalação de cliente  

   - Contagem de dispositivos virtualizado pelo Hyper-V ou do Azure  

   - Ações de contagem de centro de Software   

   - Contagem de dispositivos ativados por UEFI

   - Métodos de implementação de cliente e a contagem de clientes por método de implementação

   - Lista/contagem de agentes de cliente ativados  

   - Idade do SO nos meses

   - Número de classes de inventário de hardware, as regras de inventário de software e regras de recolha de ficheiros

   - As estatísticas de atestado de estado de funcionamento: os códigos de erro mais comuns, número de servidores no local e o número de dispositivos em vários Estados

   - ***[Novo]***  Contagem de dispositivos pelo browser predefinido


### <a name="cloud-services"></a>Serviços cloud  

  - Estatísticas de deteção do Active Directory do Azure

  - Estatísticas de configuração e utilização do Gateway de gestão de nuvem: contagens de regiões e ambientes e estatísticas de autenticação/autorização

  - Aplicações de contagem do Azure Active Directory e os serviços ligados para o Configuration Manager

  - Contagem das coleções sincronizados para o Operations Management Suite

  - Contagem de conectores de análise de atualização

  - Indica se o conector em nuvem do Operations Management Suite está ativado


### <a name="co-management"></a>Gestão conjunta  
  - Agregar estatísticas de utilização da gestão conjunta: número de clientes inscritos, os clientes receber a política, Estados de carga de trabalho, tamanhos de coleção do projeto piloto/exclusão e erros de inscrição  

  - Contagem de clientes pelo método de inscrição de gestão conjunta  

  - Estatísticas de erro para a inscrição de gestão conjunta  

  - Agenda de inscrição e estatísticas de histórico  

  - Contagem de clientes elegíveis para gestão conjunta  

  - Associado inquilino do Microsoft Intune


### <a name="collections"></a>Coleções  

   - Utilização de ID de coleção (não a ficar sem IDs)

   - Estatísticas de avaliação de coleção: hora de consulta, atribuída versus contagens não atribuídas, contagens por tipo, rollover de ID e a utilização de regra

   - Coleções sem uma implementação


### <a name="compliance-settings"></a>Definições de compatibilidade  

  - Informações da linha de base de configuração básica: contagem, número de implementações e número de referências

  - Estatísticas de erro de política de conformidade

  - Contagem de itens de configuração por tipo  

  - Contagem de implementações que referenciam definições incorporadas, incluindo remediar definição  

  - Contagem de regras e implementações criadas para as definições personalizadas, incluindo remediar definição  

  - Contagem de implementado SCEP Simple Certificate Enrollment Protocol (), VPN, Wi-Fi, certificado (. pfx) e modelos de política de conformidade

  - Contagem do certificado de SCEP, VPN, Wi-Fi, certificado (. pfx) e implementações de política de conformidade por plataforma

  - Windows Hello para a política de negócio (criado, implementado)


### <a name="content"></a>Conteúdo  

  - ***[Atualizado]***  Estatísticas de grupo de limites: rápido quantos, quantos lenta, contagem por grupo e as relações de contingência

  - Informações do grupo de limites: contagem de limites e sistemas de sites que estão atribuídos a cada grupo de limites  

  - Relações de grupo de limites e a configuração de contingência

  - Estatísticas de transferência do conteúdo de cliente

  - Contagem de limites por tipo  

  - Contagem de clientes de cache ponto a ponto, estatística de utilização e estatísticas de transferência parcial

  - As informações de configuração do Gestor de distribuição: threads, repita o atraso, número de tentativas e as definições do ponto de distribuição de extração  

  - Informações de configuração de ponto de distribuição: a utilização de cache do ramo e monitorização do ponto de distribuição

  - Informações do grupo de ponto de distribuição: contagem de pacotes e pontos de distribuição que estão atribuídos a cada grupo de pontos de distribuição  


### <a name="endpoint-protection"></a>Endpoint Protection  

   - As políticas do Windows Defender Advanced Threat Protection (ATP): contagem de políticas, e se as políticas são implementadas

   - Contagem de alertas que estão configurados para a funcionalidade Endpoint Protection  

   - Contagem de coleções que estão selecionadas para aparecerem no dashboard do Endpoint Protection  

   - Políticas de contagem do Windows Defender exploram Guard, implementações e os clientes visados

   - Erros de implementação do Endpoint Protection, contagem de códigos de erro de implementação de política do Endpoint Protection  

   - Antimalware do Endpoint Protection e a utilização da política de Firewall do Windows (número de políticas únicas atribuídas ao grupo)<br /><br /> Estes dados não incluem quaisquer informações sobre as definições incluídas na política.  


### <a name="migration"></a>Migração  

  - Contagem de objetos migrados (utilize do Assistente de migração)


### <a name="mobile-device-management-mdm"></a>Gestão de dispositivos móveis (MDM)  

   - Número de emitido ações do dispositivo móvel: bloquear, afixar rest, apagar, extinguir e sincronizar agora comandos

   - Contagem de políticas de dispositivos móveis  

   - Contagem de dispositivos móveis que são geridos pelo Configuration Manager e Microsoft Intune e como foram inscritos (em massa, baseado no utilizador)  

   - Contagem de utilizadores que têm vários dispositivos móveis inscritos  

   - Consulta de agenda e as estatísticas de duração de verificação de dispositivos móveis de dispositivos móveis  


### <a name="microsoft-intune-troubleshooting"></a>Resolução de problemas do Microsoft Intune  

   - Contagem e tamanho das ações do dispositivo (apagar, extinguir, bloquear) telemetria e mensagens de dados que são replicadas para o Microsoft Intune

   - Contagem e tamanho de estado, o estado, inventário, RDR, DDR, UDX, inquilino mensagens de estado, POL, registo, certificado, CRP, ressincronização, CFD, RDO, BEX, ISM e conformidade que são transferidas a partir do Microsoft Intune

   - Diferenciais e completas estatísticas de sincronização de utilizador para o Microsoft Intune


### <a name="on-premises-mobile-device-management-mdm"></a>Gestão de dispositivos móveis (MDM) no local  

   - Contagem de pacotes e perfis de inscrição em massa do Windows 10  

   - Estatísticas de êxito/falha de implementação para implementações de aplicações MDM no local  


### <a name="os-deployment"></a>Implementação do SO  

   - Contagem de imagens de arranque, controladores, pacotes de controladores, pontos de distribuição preparados com multicast ativado, pontos de distribuição com PXE ativado e sequências de tarefas  

   - Contagem de imagens de arranque pela versão de cliente do Configuration Manager

   - Contagem de imagens de arranque pela versão do Windows PE

   - Contagem de políticas de atualização de edição

   - Contagem de identificadores de hardware excluídos PXE

   - Implementação de contagem do SO pela versão do SO

   - Atualizações de contagem do SO ao longo do tempo

   - Contagem de implementações de sequência de tarefas utilizando a opção para transferir o conteúdo previamente

   - Contagens de utilização de passo de sequência de tarefas

   - Versão do Windows ADK instalado


### <a name="site-updates"></a>Atualizações de sites  

   - Versões das correções instaladas do Configuration Manager


### <a name="software-updates"></a>Atualizações de Software  

   - Disponível e o prazo deltas que são utilizados em regras de implementação automática  

   - Número médio e máximo de atribuições por atualização  

   - Avaliação de atualização de cliente e agendas de análise  

   - Ponto de atualização de classificações são sincronizadas por software

   - Estatísticas de aplicação de patches de cluster  

   - Configuração de atualizações do Windows 10 express

   - Configurações que são utilizadas para o Active Directory Windows 10, planos de manutenção  

   - Contagem de atualizações do Office 365 implementadas  

   - Controladores de contagem de superfície da Microsoft sincronizadas

   - Contagem de grupos de atualização e atribuições  

   - Contagem de pacotes de atualização e o número máximo/mínimo/médio de pontos de distribuição são segmentados com pacotes  

   - Contagem das atualizações que são criados e implementados com o System Center Update Publisher  

   - Contagem de Windows Update para criar e implementar as políticas de negócio

   - ***[Novo]***  Agregar estatísticas de Windows Update para configurações de negócio

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


### <a name="sqlperformance-data"></a>Dados de desempenho/SQL  

   - Configuração e a duração do resumo de site

   - Contagem das maiores tabelas de bases de dados  

   - Estatísticas de deteção operacionais (contagem de objetos encontrado)

   - Tipos de deteção, ativada e agendar (completas, incrementais)

   - Estado de informações, utilização e estado de funcionamento da réplica SQL AlwaysOn

   - Problemas de desempenho, o período de retenção e o estado de automático limpeza o registo de alterações do SQL Server

   - Período de retenção de registo de alterações SQL

   - Estatísticas de desempenho, incluindo os tipos de mensagens mais comuns e mais dispendiosos de mensagens de estado


### <a name="miscellaneous"></a>Diversas  

   - Configuração de ponto de serviço de armazém de dados, incluindo a hora de agendamento e a média de sincronização

   - Contagem de scripts e estatísticas de execução

   - Contagem de sites com reativação numa LAN (WOL)

   - Relatório de estatísticas de utilização e desempenho
  
   - ***[Novo]***  Fases estatísticas de utilização de implementação



##  <a name="bkmk_level3"></a> Nível 3 - Completo
O nível completo inclui todos os dados os níveis básico e avançado. Também inclui informações adicionais sobre o Endpoint Protection, percentagens de compatibilidade de atualização e informações de atualização de software. Este nível também pode incluir informações de diagnóstico avançadas como instantâneos de memória, que podem incluir informações pessoais que existiam na memória ou ficheiros de registo no momento da captura e de ficheiros de sistema.

Para o Configuration Manager versão 1802, este nível inclui os seguintes dados:

- Informações de agenda de avaliação de regras de implementações automáticas

- Resumo do Estado de funcionamento ATP

- Estatísticas de avaliação e de atualização de coleções

- Estatísticas de política de conformidade de erros e de conformidade

- Definições de compatibilidade: SCEP, VPN, Wi-Fi e conformidade detalhes de configuração de modelo de política

- Pacote de configuração de DCM para utilização do System Center Configuration Manager

- Erros de instalação de implementação do cliente de detalhado

- Endpoint Protection estado de funcionamento resumo: incluindo contagem de, em risco, desconhecidos e não suportados clientes protegidos

- Configuração da política do Endpoint Protection

- Lista de processos configurados com o comportamento de instalação de aplicações

- Número máximo/mínimo/médio de horas desde a última análise de atualização de software

- Número máximo/mínimo/médio de clientes inativos em coleções de implementações de atualização de software

- Número máximo/mínimo/médio de atualizações de software por pacote

- ***[Atualizado]***  Estatísticas de implementação de código de produto MSI 

- Compatibilidade geral das implementações de atualizações de software

- Contagem de grupos que têm atualizações de software expiradas

- Contagens e códigos de erro de implementação de atualizações de software

- Informações de implementação de atualização de software: percentagem das implementações direcionadas com o cliente em comparação com a hora UTC, necessário opcional versus silencioso e supressão de reinício

- Produtos de atualização de software sincronizados com êxito pelo ponto de atualização de software

- Percentagens de êxito de análise de atualização de software

- Principais 50 CPUs no ambiente

- Tipo de Exchange Active Sync (EAS) políticas de acesso condicional (bloquear ou colocar em quarentena) para dispositivos que gere o Microsoft Intune

- Microsoft Store para detalhes de negócio da aplicação: lista de não sejam de agregação de aplicações sincronizadas, incluindo AppID, o estado online ou o estado offline e contagens de licenças adquiridas total
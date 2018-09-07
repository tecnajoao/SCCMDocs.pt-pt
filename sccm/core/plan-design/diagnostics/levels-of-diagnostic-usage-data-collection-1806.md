---
title: Dados de diagnóstico e utilização para 1806
titleSuffix: Configuration Manager
description: Saiba mais sobre os níveis de diagnósticos e dados de utilização recolhidos na versão 1806.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a0287beb-70a9-4b57-a627-e7bfba27fd3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d964295134538cf281af214830a5bc416484be51
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893676"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1806"></a>Níveis de recolha de dados de diagnóstico de utilização para a versão 1806

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager versão 1806 recolhe três níveis de diagnósticos e dados de utilização: **Básica**, **avançada**, e **completa**. Por predefinição, esta funcionalidade está definida no nível Avançado. As secções seguintes fornecem detalhes adicionais sobre os dados recolhidos em cada nível.

Alterações das versões anteriores são indicadas com ***[novo]***, ***[atualizado]***, ***[removido]***, ou ***[movido]***.


> [!IMPORTANT]
>  O Configuration Manager não recolhe códigos de site, nomes de sites, endereços IP, nomes de utilizador, nomes de computador, endereços físicos ou endereços de e-mail nos níveis básico ou avançado. Qualquer recolha destas informações no nível completo não é intencional. Potencialmente está incluído nas informações de diagnóstico avançadas, como ficheiros de registo ou instantâneos de memória. Microsoft não utiliza estas informações para identificar, contactar ou desenvolver advertising.



##  <a name="bkmk_change"></a> Como alterar o nível
 Os administradores que tenham um âmbito de administração baseada em funções que inclua **modificar** permissões sobre o **Site** classe de objeto pode alterar o nível dos dados recolhidos nas definições de diagnóstico e dados de utilização na consola do Configuration Manager.

Alterar o nível de recolha de dados de dentro da consola ao navegar até **Administration** > **descrição geral** > **configuração do Site**  >  **Sites**. Open **definições de hierarquia**e, em seguida, selecione o nível de dados que pretende utilizar.  



##  <a name="bkmk_level1"></a> Nível 1 - Básico
O nível básico inclui dados sobre a hierarquia, os dados necessários para o ajudar a melhorar a sua instalação ou atualização de experiência e os dados que ajuda a determinar as atualizações do Configuration Manager que são aplicáveis para a sua hierarquia.

Para o Configuration Manager versão 1806, este nível inclui os seguintes dados:

- Estatísticas sobre as ligações da consola do Configuration Manager: Versão do SO, idioma, SKU e arquitetura, memória de sistema de contagem de processadores lógicos, ligarem o ID do site, versões de .NET instaladas e pacotes de idiomas da consola

- Contagens de tipo de aplicação básica e de implementação: total de aplicações, total de aplicações com vários tipos de implementação, aplicações de aplicativos no total com as dependências, total substituídas e contagem de tecnologias de implantação em utilização

- Dados de hierarquia de site do Configuration Manager básica: lista, tipo, versão, estado, contagem de clientes e fuso horário do site

- ***[Atualizado]***  Configuração básica da base de dados: processadores, tamanho da memória, as definições de memória, configuração de base de dados do Configuration Manager, tamanho de base de dados do Configuration Manager, configuração de cluster e configuração de vistas distribuídas

- Estatísticas de deteção básica: contagem de deteção, tamanhos de máximo/mínimo/médio de grupo, e quando o site está em execução inteiramente com os serviços do Active Directory do Azure

- Informações básicas do Endpoint Protection sobre as versões de cliente de antimalware

- Implementação básica do sistema operacional contagens de imagens

- Informações do servidor de sistema de site básico: funções do sistema utilizadas, internet e estado SSL, sistema operacional, processadores, físico ou máquina virtual e utilização elevada de disponibilidade no servidor do site do site

- Esquema de base de dados do Configuration Manager (hash de todas as definições de objetos)

- Nível configurado para diagnósticos e dados de utilização, modo online ou offline e configuração de atualização rápida

- Contagem de localidades e idiomas de cliente

- Versões de cliente de contagem do Configuration Manager, versões de SO e versões do Office

- Contagem de sistemas operativos para dispositivos geridos e políticas definidas pelo conector do Exchange

- Contagem de dispositivos Windows 10 por ramo e compilação

- Clientes de contagem do Windows 10 que utilizam o Windows Update para empresas  

- Métricas de desempenho de base de dados: processamento de informações, principais procedimentos de armazenados do SQL Server por processador e utilização do disco de replicação

- Ponto de distribuição e gestão de pontos de tipos e informações básicas de configuração: protegido, pré-configurado, PXE, multicast, estado SSL, pontos de distribuição de extração/ponto a ponto, compatível com MDM e habilitados para SSL

- Hash de lista de extensões para os assistentes e páginas de propriedades de consola de administração

- Informações de configuração:
     - Crie, instalar o tipo, pacotes de idiomas, funcionalidades ativadas por si   

     - Utilização da versão de pré-lançamento, o tipo de suporte de dados de configuração, o tipo do ramo

     - Data de expiração do Software Assurance      

     - Atualizar estado de implementação de pacote e erros, transfira o progresso e os erros de pré-requisitos     

     - Utilização de cadência rápida de atualização

     - Versão do script pós-atualização

- Versão do SQL, nível de service pack, edição, ID de agrupamento e o conjunto de carateres     

- Diagnóstico e estatísticas de dados de utilização: quando executado, tempo de execução, erros

- Se a deteção de rede está ativada ou desativada

- Contagem de clientes associados ao Azure Active Directory

- Contagem de implementações faseadas criado por tipo

- Contagem de clientes de interoperabilidade estendida

- Lista de hash de propriedades de inventário de hardware mais de 255 carateres

- ***[Movido]***  Contagem de clientes por método de inscrição de cogestão  

- ***[Movido]***  Estatísticas de erros de inscrição de cogestão  

- ***[Novo]***  Contagem de clientes por idade de SO Windows, para o mais próximo intervalo de três meses  

- ***[Novo]***  Nomes de processador de top 10 utilizados nos clientes  

- ***[Novo]***  Contagem e processar taxas de objetos do Configuration Manager da chave: registos de dados de deteção (DDR), as mensagens de estado, as mensagens de estado, inventário de hardware, inventário de software e contagem geral de ficheiros em pastas a receber  

- ***[Novo]***  Informações de desempenho de disco e de processador do servidor do site  

- ***[Novo]***  Informações de utilização de memória e tempo de atividade para processos de servidor de site do Configuration Manager  

- ***[Novo]***  Contagem de falhas de processos de servidor de site do Configuration Manager e o ID de assinatura do Watson, se disponível  



##  <a name="bkmk_level2"></a> Nível 2 - Avançado
O nível avançado é a predefinição após a conclusão da configuração. Este nível inclui dados recolhidos no nível básico e dados específicos de funcionalidades (frequência e duração de utilização), as definições de cliente do Configuration Manager (nome do componente, estado e determinadas definições como intervalos de consulta) e informações básicas sobre atualizações de software.

Este nível é recomendado porque disponibiliza à Microsoft com os dados mínimos necessários para fazer melhorias úteis em versões futuras dos produtos e serviços. Nesse nível não nomes de recolha de objetos (sites, utilizadores, computadores ou objetos), os detalhes dos objetos relacionados com segurança nem vulnerabilidades como contagens dos sistemas que necessitam de atualizações de software.

Para o Configuration Manager versão 1806, este nível inclui os seguintes dados:

### <a name="application-management"></a>Gestão de aplicações  

   - Requisitos de aplicações: contagem de condições incorporadas referenciado pela tecnologia de implantação

   - Substituição de aplicações, profundidade máxima da cadeia

   - Frequência de utilização e estatísticas de aprovação de aplicações

   - Estatísticas de tamanho do conteúdo da aplicação

   - Informações de implementação de aplicação: Utilizar instalação em comparação com a desinstalação, requer a aprovação, interação do utilizador ativado/desativado, a dependência, substituição e contagem de utilização da funcionalidade de comportamento de instalação  

   - Estatísticas de tamanho e a complexidade de política de aplicação

   - Estatísticas de pedidos de aplicação disponíveis

   - Informações básicas de configuração de pacotes e programas: opções de implementação e sinalizadores de programa

   - Informações básicas de utilização/segmentação para tipos de implementação: utilizador versus dispositivo segmentado, necessário em comparação com as aplicações disponíveis e universais

   - Contagem de ambientes de App-V e propriedades de implementação

   - Contagem de aplicabilidade de aplicações por sistema operacional  

   - Contagem de aplicações que são referenciados por uma sequência de tarefas

   - Contagem de imagem corporativa distintas do catálogo de aplicações

   - Aplicativos de contagem do Office 365 criados com o dashboard

   - Contagem de pacotes por tipo  

   - Contagem de implementações de pacote/programa  

   - Contagem de licenças de aplicação licenciadas para Windows 10  

   - Tipos de implementação de contagem do Windows Installer por desinstalar definições de conteúdo

   - Contagem da Microsoft Store para aplicações de negócio e estatísticas de sincronização: resumidos tipos de aplicações, o estado de aplicação com licença e o número de online e aplicações licenciadas offline  

   - Tipo e duração da janela de manutenção  

   - Número de máximo/mínimo/médio de implementações de aplicações por utilizador/dispositivo por período de tempo

   - Mais comuns códigos de erro de instalação de aplicações através de uma tecnologia de implantação

   - Contagens e opções de configuração de MSI

   - Estatísticas de interação do utilizador final com notificação para implementações de software necessárias   

   - Utilização de acesso a dados universal, como criado

   - Estatísticas agregadas de afinidade dispositivo / utilizador 

   - Utilizadores primários, máximos e média por dispositivo  

   - ***[Novo]***  Utilização de condição global da aplicação por tipo  

   - ***[Novo]***  Configuração de personalização do Centro de software  

   - ***[Novo]***  Contagens e preparação para o Gestor de conversão de pacotes  

   - ***[Novo]***  Contagem de métodos de deteção de aplicações por tipo  

   - ***[Novo]***  Contagem de erros de imposição de aplicações  

   - ***[Novo]***  Propriedades de instalador do MSI 

   - ***[Novo]***  Estatísticas do utilizador instalar pedidos



### <a name="client"></a>Cliente  

   - Versão de cliente do Active Management Technology (AMT)

   - Idade de BIOS em anos

   - Contagem de dispositivos com o arranque seguro ativado

   - Contagem de dispositivos por Estado TPM

   - Atualização automática do cliente: configuração de implementação, incluindo a criação de piloto e de exclusão uso cliente (cliente de interoperabilidade expandido)

   - Configuração de tamanho de cache do cliente

   - Erros de transferência de implementação do cliente

   - ***[Atualizado]***  Cliente estado de funcionamento estatísticas e de cima resumo do problema por versão de cliente

   - Estado de ação da operação de notificação de cliente: quantas vezes cada é o número máximo de execução de clientes de destinados e a taxa média de êxito

   - Contagem de instalações de cliente a partir de cada tipo de localização de origem  

   - Contagem de falhas de instalação de cliente  

   - Contagem de dispositivos virtualizadas por Hyper-V ou do Azure  

   - Ações de contagem de centro de Software   

   - Contagem de dispositivos habilitados para UEFI

   - Métodos de implantação usados para cliente e a contagem de clientes por método de implementação

   - Lista/contagem de agentes de cliente ativados  

   - Idade de SO em meses

   - Número de classes de inventário de hardware, as regras de inventário de software e as regras de recolha de ficheiros

   - As estatísticas de atestado de estado de funcionamento do dispositivo: códigos de erro mais comuns, número de servidores no local e contagens de dispositivos em vários Estados

   - Contagem de dispositivos por browser predefinido  

   - ***[Novo]***  Certificados de autenticação de servidor gerado pelo contagem do Configuration Manager  

   - ***[Novo]***  Dispositivos de contagem do Microsoft Surface por modelo  


### <a name="cloud-services"></a>Serviços cloud  

  - Estatísticas de deteção do Active Directory do Azure

  - Estatísticas de configuração e utilização do Gateway de gestão da Cloud: contagens de regiões e ambientes e estatísticas de autenticação/autorização

  - Contagem do Azure Active Directory aplicações e serviços ligados para o Configuration Manager

  - Contagem de coleções sincronizado com o Azure Log Analytics

  - Contagem de conectores de análise de atualização

  - Se o Azure Log Analytics na cloud conector está ativada  

  - ***[Novo]***  Pontos de contagem de distribuição de extração com um ponto de distribuição de nuvem como localização de origem  


### <a name="co-management"></a>Cogestão  
  - Agregar estatísticas de utilização de cogestão: número de clientes inscritos, clientes que recebem a política, Estados de carga de trabalho, tamanhos de coleção piloto/exclusão e erros de inscrição  

  - Agenda de inscrição e estatísticas históricas  

  - Contagem de clientes elegíveis para a cogestão  

  - Inquilino associado do Microsoft Intune


### <a name="collections"></a>Coleções  

   - Utilização de ID de coleção (não ficar sem IDs)

   - Estatísticas de avaliação de coleção: tempo de consulta, atribuído versus contagens não atribuídas, contagens por tipo, o rollover de ID e o uso de regra

   - Coleções sem uma implementação


### <a name="compliance-settings"></a>Definições de compatibilidade  

  - Informações de linha de base de configuração básica: contagem, número de implementações e número de referências

  - Estatísticas de erro de política de conformidade

  - Contagem de itens de configuração por tipo  

  - Contagem de implementações que referenciam definições incorporadas, incluindo remediar definição  

  - Contagem de regras e implementações criadas para as definições personalizadas, incluindo remediar definição  

  - Contagem de implementado SCEP Simple Certificate Enrollment Protocol (), VPN, Wi-Fi, certificado (. pfx) e modelos de política de conformidade

  - Implementações de política de certificado, VPN, Wi-Fi, certificado (. pfx) e conformidade contagem de SCEP por plataforma

  - Windows política Hello para empresas (criado, implantado)  

  - ***[Novo]***  Contagem de políticas de browser Microsoft Edge implementadas  


### <a name="content"></a>Conteúdo  

  - Estatísticas de grupo de limites: quantos mais rápidas e quantos lento, contagem por grupo e relações de contingência

  - Informações do grupo de limites: contagem de limites e sistemas de sites que são atribuídos a cada grupo de limites  

  - As relações de grupo de limites e configuração de contingência

  - Estatísticas de transferência de conteúdo de cliente

  - Contagem de limites por tipo  

  - Contagem de clientes de cache ponto a ponto, estatísticas de utilização e estatísticas de transferência parcial

  - Informações de configuração do Gestor de distribuição: threads, repita o atraso, número de repetições e as definições do ponto de distribuição de extração  

  - Informações de configuração do ponto de distribuição: utilizar da cache de ramificação e a monitorização do ponto de distribuição

  - Informações do grupo de ponto de distribuição: contagem de pacotes e pontos de distribuição que são atribuídos a cada grupo de pontos de distribuição  

  - ***[Novo]***  Tipo de biblioteca, de conteúdo, seja local ou remoto  


### <a name="endpoint-protection"></a>Endpoint Protection  

   - Políticas de proteção de ameaças avançada do Windows Defender (ATP): contagem de políticas, e se as políticas são implementadas

   - Contagem de alertas que estão configurados para a funcionalidade Endpoint Protection  

   - Contagem de coleções que estão selecionadas para aparecerem no dashboard do Endpoint Protection  

   - Políticas de contagem do Windows Defender Exploit Guard, implementações e os clientes de destinados

   - Erros de implementação do Endpoint Protection, contagem de códigos de erro de implementação de política de proteção de ponto final  

   - Antimalware do Endpoint Protection e utilização da política de Firewall do Windows (número de políticas únicas atribuídas ao grupo)<br /><br /> Estes dados não incluem quaisquer informações sobre as definições incluídas na política.  


### <a name="migration"></a>Migração  

  - Contagem de objetos migrados (utilização do Assistente de migração)


### <a name="mobile-device-management-mdm"></a>Gestão de dispositivos móveis (MDM)  

   - Contagem de emitido ações do dispositivo móvel: bloquear, afixar rest, apagar, extinguir e, agora os comandos de sincronização

   - Contagem de políticas de dispositivos móveis  

   - Contagem de dispositivos móveis que são geridos pelo Configuration Manager e o Microsoft Intune e como foram inscritos (em massa, baseado no usuário)  

   - Contagem de utilizadores que têm vários dispositivos móveis inscritos  

   - Consulta de agenda e as estatísticas de duração de entrada de dispositivo móvel de dispositivos móveis  


### <a name="microsoft-intune-troubleshooting"></a>Resolução de problemas do Microsoft Intune  

   - Contagem e tamanho das ações do dispositivo (apagar, extinguir, bloquear) dados de utilização e mensagens de dados que são replicadas para o Microsoft Intune

   - Contagem e tamanho de estado, estado, inventário, RDR, DDR, UDX, inquilino mensagens de estado, POL, LOG, certificado, CRP, ressincronização, CFD, RDO, BEX, ISM e conformidade que são transferidas a partir do Microsoft Intune

   - Diferenciais e completas estatísticas de sincronizações de utilizador para o Microsoft Intune


### <a name="on-premises-mobile-device-management-mdm"></a>Gestão de dispositivos móveis (MDM) no local  

   - Contagem de pacotes e perfis de inscrição em massa do Windows 10  

   - Estatísticas de êxito/falha de implementação para implementações de aplicações MDM no local  


### <a name="os-deployment"></a>Implementação do SO  

   - Contagem de imagens de arranque, controladores, pacotes de controladores, pontos de distribuição preparados com multicast ativado, pontos de distribuição com PXE ativado e sequências de tarefas  

   - Contagem de imagens de arranque da versão de cliente do Configuration Manager

   - Contagem de imagens de arranque pela versão do Windows PE

   - Contagem de políticas de atualização de edição

   - Contagem de identificadores de hardware excluídos do PXE

   - Implementação de contagem de sistema operacional pela versão do SO

   - Atualizações de contagem de SO ao longo do tempo

   - Contagem de implementações de sequência de tarefas usando a opção para pré-transferir conteúdo

   - Contagens de utilização de passo de sequência de tarefas

   - Versão de ADK de Windows instalado  

   - ***[Novo]***  Contagem de tarefas de manutenção de imagem  


### <a name="site-updates"></a>Atualizações do site  

   - Versões das correções instaladas do Configuration Manager


### <a name="software-updates"></a>Atualizações de Software  

   - Deltas disponíveis e de prazo que são utilizados nas regras de implementação automática  

   - Número médio e máximo de atribuições por atualização  

   - Avaliação de atualização de cliente e agendas de análise  

   - Ponto de atualização de classificações são sincronizadas por software

   - Estatísticas de aplicação de patches de cluster  

   - Configuração de atualizações do Windows 10 express

   - Configurações que são utilizadas para o Active Directory Windows 10, planos de manutenção  

   - Contagem de atualizações do Office 365 implementadas  

   - Controladores de contagem do Microsoft Surface sincronizados

   - Contagem de grupos de atualização e atribuições  

   - Contagem de pacotes de atualização e o número máximo/mínimo/médio de pontos de distribuição que são segmentados com pacotes  

   - Contagem de atualizações que são criados e implementados com o System Center Update Publisher  

   - Contagem de Windows Update para políticas de negócios criados e implementados

   - Estatísticas agregadas de atualização do Windows para configurações de negócios

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

   - ***[Novo]***  Contagem de subscrições de catálogo de atualização de software de terceiros e de utilização  

   - ***[Novo]***  Contagem de atualizações de software implementadas com e sem conteúdo  


### <a name="sqlperformance-data"></a>Dados de desempenho/SQL  

   - Configuração e a duração do resumo de site

   - Contagem das maiores tabelas de bases de dados  

   - Estatísticas operacionais de deteção (contagem de foram encontrados objetos)

   - Tipos de deteção, ativada e agendar (completas e incrementais)

   - Estado de informações, utilização e estado de funcionamento da réplica SQL AlwaysOn

   - Controlo de problemas de desempenho, o período de retenção e o estado de limpeza automática de alterações do SQL

   - Período de retenção de registo de alterações SQL

   - Estatísticas de desempenho, incluindo tipos de mensagens mais comuns e mais caros de mensagens de estado e Estado


### <a name="miscellaneous"></a>Diversos  

   - Configuração do ponto de serviço de armazém de dados incluindo a hora de agendamento e a média de sincronização

   - Contagem de scripts e estatísticas de execução

   - Contagem de sites com reativação em LAN (WOL)

   - Relatório de estatísticas de utilização e desempenho
  
   - Estatísticas de utilização de implementação por fases  

   - ***[Novo]***  CMPivot estatísticas de utilização  

   - ***[Novo]***  Contagens e o progresso de item de informações de gestão  

   - ***[Novo]***  Processa de contagem de falhas para exclusivos não - Configuration Manager no servidor do site e ID de assinatura do Watson, se disponível



##  <a name="bkmk_level3"></a> Nível 3 - Completo
O nível completo inclui todos os dados nos níveis de básico e avançado. Também inclui informações adicionais sobre o Endpoint Protection, percentagens de compatibilidade de atualização e informações de atualização de software. Este nível também pode incluir informações de diagnóstico avançadas, como ficheiros de sistema e instantâneos de memória, que podem incluir informações pessoais que existiam na memória ou ficheiros de registo no momento da captura.

Para o Configuration Manager versão 1806, este nível inclui os seguintes dados:

- Informações de agenda de avaliação de regras de implementações automáticas

- Resumo do Estado de funcionamento do ATP

- Estatísticas de avaliação e de atualização de coleções

- Estatísticas de política de conformidade em conformidade e erros

- Definições de compatibilidade: SCEP, VPN, Wi-Fi e conformidade detalhes de configuração de modelo de política

- Pacote de configuração do DCM para utilização do System Center Configuration Manager

- Erros de instalação de implementação detalhadas do cliente

- Integridade de proteção de ponto final resumida: incluindo a contagem de, em risco, desconhecidos e não suportados clientes protegidos

- Configuração da política do Endpoint Protection

- Lista de processos configurado com o comportamento de instalação para aplicações

- Número máximo/mínimo/médio de horas desde a última análise de atualização de software

- Número máximo/mínimo/médio de clientes inativos em coleções de implementações de atualização de software

- Número máximo/mínimo/médio de atualizações de software por pacote

- Estatísticas de implementação de código de produto MSI 

- Compatibilidade geral das implementações de atualizações de software

- Contagem de grupos que têm atualizações de software expiradas

- Contagens e códigos de erro de implementação de atualizações de software

- Informações de implementação de atualizações de software: percentagem das implementações que são visados com o cliente em relação a hora UTC, necessário opcional versus silencioso e supressão de reinício

- Produtos de atualização de software sincronizados pelo ponto de atualização de software

- Percentagens de êxito de análise de atualização de software

- CPUs de 50 principais no ambiente

- Tipo de Exchange Active Sync (EAS) políticas de acesso condicional (bloqueio ou quarentena) para dispositivos que gere o Microsoft Intune

- Microsoft Store para obter detalhes de aplicativo de negócios: lista de não é de agregação de aplicativos sincronizados, incluindo AppID, o estado online ou o estado offline e contagens de licenças adquiridas total

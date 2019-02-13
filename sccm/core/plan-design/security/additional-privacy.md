---
title: Informações de privacidade adicionais
titleSuffix: Configuration Manager
description: Saiba mais sobre como a Microsoft recolhe e utiliza dados do Configuration Manager.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8e5a42249df462be1584a153657a42ae325f1b9a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125373"
---
# <a name="additional-information-about-privacy-for-configuration-manager"></a>Informações adicionais sobre a privacidade do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


## <a name="updates-and-servicing"></a>As atualizações e manutenção

O Configuration Manager utiliza um modelo de atualização que ajuda a manter o seu ambiente atual com as mais recentes atualizações e funcionalidades. Esse recurso usa uma função do sistema de site chamada o ponto de ligação de serviço. Selecione o servidor onde instalar esta função. 

Para obter mais informações sobre informações recolhidas e como são utilizadas, consulte [dados de utilização](#usage-data).



## <a name="usage-data"></a>Dados de utilização

O Configuration Manager recolhe os diagnósticos e dados de utilização sobre ele próprio, que a Microsoft utiliza para melhorar a experiência de instalação, qualidade e segurança de versões futuras.
Dados de diagnóstico e utilização estão ativados para cada hierarquia do Configuration Manager. Ele consiste em consultas de SQL Server que são executadas semanalmente em cada site primário e para o site de administração central. Quando a hierarquia utiliza um site de administração central, os dados de sites primários são replicados para esse site. No site de nível superior da hierarquia, o ponto de ligação de serviço envia estas informações quando verifica a existência de atualizações. Se o ponto de ligação de serviço estiver no modo offline, as informações são transferidas ao utilizar a ferramenta de ligação de serviço.

O Configuration Manager recolhe dados apenas a partir SQL server da base de dados do site, o, e não recolhe dados diretamente a partir de clientes ou servidores de site.

Os administradores podem alterar o nível de dados que são recolhidos ao aceder a **dados de utilização** secção da consola do Configuration Manager.

Para obter mais informações sobre os níveis de dados de utilização e as definições, consulte [diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).



## <a name="customer-experience-improvement-program"></a>Programa de Melhoramento da Experiência do Cliente

> [!Note]  
> A funcionalidade do PMEC a partir do Configuration Manager versão 1802, é removida do produto.

O programa de melhoramento da experiência do cliente (PMEC) recolhe informações básicas da consola do Configuration Manager sobre a configuração de hardware e como utilizar o nosso software e serviços para identificar tendências e padrões de utilização. O PMEC também recolhe o tipo e número de erros que encontrar, desempenho do software e hardware e a velocidade dos serviços. Não recolhemos seu nome, endereço ou outras informações de contacto. Não são recolhidos dados do PMEC a partir de computadores cliente.

Utilizamos estas informações para melhorar a qualidade, a fiabilidade e o desempenho do software e serviços da Microsoft.

Para obter mais informações sobre as informações recolhidas, processadas ou transmitidas pelo PMEC, consulte a [declaração de privacidade do PMEC](https://go.microsoft.com/fwlink/?LinkID=525211).



## <a name="log-analytics-connector"></a>Conector do log Analytics

O conector do Log Analytics sincroniza dados, como coleções, a partir do Configuration Manager para o serviço cloud do Azure. O ID de subscrição do Azure e a chave secreta são armazenados na base de dados do Configuration Manager quando um administrador configura a funcionalidade. O segredo do cliente do Azure Active Directory e a chave partilhada de área de trabalho do Azure são armazenados na base de dados do Configuration Manager no local. Todas as comunicações entre o Configuration Manager e do Azure utilizam HTTPS. Não existem informações adicionais sobre as coleções são fornecidas para a Microsoft fora aleatório de diagnósticos e dados de utilização. 

Para obter mais informações sobre as informações que o Log Analytics recolhe, consulte [segurança de dados de análise de registo](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-security).



## <a name="asset-intelligence"></a>Asset Intelligence

O Asset Intelligence permite aos administradores definir, controlar e gerir proativamente a compatibilidade com os padrões de configuração. A medição e elaboração de relatórios relativamente à implementação e utilização de aplicações físicas e virtuais permitem que as empresas tomem decisões comerciais mais corretas em termos de licenciamento de software e mantenham a compatibilidade com os contratos de licenciamento. Depois de coletar dados de utilização de clientes do Configuration Manager, pode utilizar diferentes funcionalidades para ver os dados, incluindo coleções, consultas e relatórios.

Durante cada sincronização, um catálogo de software conhecido é transferido da Microsoft. Pode optar por enviar informações da Microsoft sobre títulos de software não categorizados detetados dentro da sua organização para serem investigados e adicionados ao catálogo. Antes de carregar essas informações, uma caixa de diálogo mostra os dados que vão ser carregado. Não não possível resgatar os dados carregados. Do Asset Intelligence não envia informações sobre utilizadores e computadores ou utilização de licenças para a Microsoft.

Após o carregamento de um título de software, os investigadores da Microsoft identificar, categorizarem e disponibilizam esse conhecimento para todos os outros clientes que utilizam esta funcionalidade e a outros consumidores do catálogo. Os títulos de software carregados passam a ser públicos. O aplicativo e a respetiva categorização passam a fazer parte do catálogo e, em seguida, podem ser baixados por outros consumidores do catálogo de. Antes de configurar a recolha de dados do Asset Intelligence e decidir se pretende enviar informações para a Microsoft, tenha em consideração os requisitos de privacidade da sua empresa.

O Asset Intelligence não está ativado por predefinição no Configuration Manager. Carregar títulos não categorizados nunca ocorre de forma automática e o sistema não é projetado para automatizar esta tarefa. Deve selecionar e aprovar manualmente o carregamento de cada título de software.



## <a name="endpoint-protection"></a>Endpoint Protection

Microsoft Cloud Protection Service era anteriormente conhecida como Microsoft Active Protection Service ou mapas.

Os produtos aplicáveis são o System Center Endpoint Protection e a funcionalidade de Endpoint Protection do System Center Configuration Manager (para gerenciar o System Center Endpoint Protection e o Windows Defender para Windows 10). Esta funcionalidade não está implementada no System Center Endpoint Protection para Linux ou do System Center Endpoint Protection para Mac.

A Comunidade de antimalware da Microsoft Cloud Protection Service é uma voluntária Comunidade mundial online que inclui utilizadores do System Center Endpoint Protection. Ao aderir ao Microsoft Cloud Protection Service, o System Center Endpoint Protection automaticamente envia informações à Microsoft. A Microsoft utiliza as informações para determinar o software a investigar quanto a potenciais ameaças e ajudar a melhorar a eficácia do System Center Endpoint Protection. Esta Comunidade ajuda a impedir a propagação de novas infeções de software malicioso. Se um relatório do Microsoft Cloud Protection Service inclui detalhes sobre malware ou software potencialmente indesejável que o cliente do Endpoint Protection seja capaz de remover, o Microsoft Cloud Protection Service transfere a assinatura mais recente para resolver o problema. Serviço de proteção do Microsoft Cloud pode também detetar "falsos positivos" e corrigi-los. (Falsos positivos são em que algo originalmente identificado como software maligno na verdade não deve ser.) 

Relatórios do serviço de proteção do Microsoft Cloud incluem informações sobre potenciais ficheiros de malware, como nomes de ficheiros, hash criptográfico, fornecedor, tamanho e carimbos de data. Além disso, o serviço de proteção do Microsoft Cloud pode recolher URLs completos para indicar a origem do ficheiro. Estes URLs, ocasionalmente, poderão ter informações pessoais, como termos de pesquisa ou dados que foram inseridos em formulários. Relatórios também podem incluir ações que realizou quando o Endpoint Protection notificou sobre software indesejável. Relatórios do serviço de proteção do Microsoft Cloud incluem esta informação para ajudar a Microsoft a medir a eficácia com o Endpoint Protection pode detectar e remover malware e software potencialmente indesejável e para tentar identificar novos malwares.

Pode associar-se a Microsoft Cloud Protection Service se tiver uma associação básica ou avançada. Relatórios de membros básicos têm as informações descritas anteriormente. Membros do nível relatórios são mais abrangentes e podem incluir detalhes adicionas sobre o software que o Endpoint Protection Deteta avançado, como a localização desse software, nomes de ficheiros, como funciona o software e como afetou o seu computador. Os relatórios e relatórios de outros utilizadores de Endpoint Protection que participam na ajuda do serviço de proteção do Microsoft Cloud os investigadores da Microsoft descobrir novas ameaças mais rapidamente. Definições de malware são então criadas para programas que satisfazem os critérios da análise e as definições atualizadas são disponibilizadas a todos os utilizadores através do Microsoft Update.

Para ajudar a detetar e corrigir determinados tipos de infeções de malware, o produto envia regularmente informações do serviço de proteção de Cloud do Microsoft sobre o estado de segurança do seu PC. Estas informações incluem informações sobre as definições de segurança do seu PC e ficheiros de registo que descrevem os controladores e outro software que é carregado enquanto o computador arranca.

Também é enviado um número que identifica exclusivamente o seu PC. Além disso, o Microsoft Cloud Protection Service pode recolher os endereços IP que os potenciais ficheiros de malware se ligam a.

Relatórios do serviço de proteção de Cloud do Microsoft são utilizados para melhorar o software e serviços Microsoft. Os relatórios também podem ser utilizados para estatística, outros testes ou fins analíticos e para gerar definições. Apenas os funcionários da Microsoft, subcontratados, parceiros e fornecedores que têm necessidade de utilizar os relatórios podem aceder aos mesmos.

Serviço de proteção de Cloud do Microsoft não recolhe intencionalmente informações pessoais. Na medida em que serviço de proteção do Microsoft Cloud recolhe quaisquer informações pessoais, a Microsoft não utiliza as informações para identificá-lo ou contactá-lo.

Para obter mais informações, consulte [Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection).



## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Hierarquia do site – vista geográfica com Bing Maps

Na consola do Configuration Manager, vá para o **monitorização** área de trabalho, selecione a **hierarquia do Site** nó e mude para o **vista geográfica**. Esta vista permite-lhe utilizar mapas que Microsoft Bing Maps fornece para ver a topologia de servidor físico do Configuration Manager. Para ativar esta funcionalidade, as informações de localização que fornecer são enviadas do seu servidor para o serviço Web do Bing Maps.

A Microsoft utiliza as informações para explorar e melhorar o Microsoft Bing Maps e outros serviços e sites da Microsoft. Para obter mais informações, consulte a [declaração de privacidade do Microsoft](https://go.microsoft.com/fwlink/?LinkId=823548).

Pode optar por não utilizar a Vista Geográfica da Hierarquia do Site. A vista de diagrama de hierarquia padrão permite-lhe ver a hierarquia e não utiliza o serviço Bing Maps.



## <a name="microsoft-intune-subscription"></a>Subscrição do Microsoft Intune

Os clientes que comprou uma subscrição do Microsoft Intune podem utilizar o Configuration Manager para gerir os dispositivos móveis que estão ligados através do Microsoft Intune. [Declaração de privacidade do Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=262214) aplica-se aos serviços online da Microsoft, que inclui o Microsoft Intune. Se os clientes também têm uma subscrição do Microsoft Intune, o [declaração de privacidade do Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=262214) deve ser lida juntamente com a presente declaração de privacidade.

Todas as comunicações com o Microsoft Intune utilizam HTTPS. Para configurar a subscrição do Microsoft Intune e para transferir o certificado de solicitação de assinatura (CSR) necessário para configurar o suporte do iOS, um administrador tem de iniciar sessão Microsoft Intune utilizando a conta profissional e a palavra-passe. Estas credenciais não são armazenadas no Configuration Manager. Todas as outras comunicações com o Microsoft Intune são autenticadas utilizando certificados PKI de que o Microsoft Intune gera automaticamente.

Para gerir dispositivos que estão ligados ao Microsoft Intune, algumas informações são enviadas e recebidas do Microsoft Intune. Estas informações incluem o utilizador nome Principal (UPN) de todos os utilizadores que estão atribuídos às informações de inventário de serviço e dispositivo para os dispositivos que são geridos pelo Microsoft Intune. Metadados, como o nome da aplicação, publicador e versão, para conteúdo que é atribuído aos pontos de distribuição Manage.Microsoft.com é enviado para o Microsoft Intune. O conteúdo do binário real atribuído a um ponto de distribuição Manage.Microsoft.com é encriptado antes de ser carregado para o Microsoft Intune.

Esta funcionalidade não está configurada por predefinição. Os administradores controlam o conteúdo que é transferido para o ponto de distribuição Manage.Microsoft.com e os utilizadores que estão atribuídos ao serviço. A funcionalidade pode ser removida em qualquer altura.

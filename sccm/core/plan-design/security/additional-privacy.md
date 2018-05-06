---
title: Declaração de privacidade - informações adicionais
titleSuffix: Configuration Manager
description: Saiba mais sobre como a Microsoft recolhe e utiliza os dados do System Center Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e98afcbc4215d3157a361eb35b9df54223df97e0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="additional-information-about-privacy-for-system-center-configuration-manager"></a>Informações adicionais sobre a privacidade do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


## <a name="updates-and-servicing"></a>Atualizações e manutenção
System Center Configuration Manager apresenta um novo modelo de atualização que ajuda a manter a sua implementação do Configuration Manager atuais com as mais recentes atualizações e funcionalidades. Quando é instalada, esta funcionalidade adiciona uma nova função de sistema de sites que tem o ponto de ligação de serviço num servidor do site que opta por um administrador. Para obter detalhes sobre as informações recolhidas e como são utilizadas, consulte a secção de dados de utilização neste artigo.


## <a name="usage-data"></a>Dados de utilização
System Center Configuration Manager recolhe os diagnósticos e dados de utilização sobre si próprio, que utiliza a Microsoft para melhorar a experiência de instalação, qualidade e segurança de versões futuras.
Os diagnósticos e dados de utilização está ativada para cada hierarquia do System Center Configuration Manager. Consiste em consultas do SQL Server que são executadas semanalmente em cada site primário e no site de administração central. Quando a hierarquia utiliza um site de administração central, os dados de sites primários são replicados para esse site. No site de nível superior da hierarquia, o ponto de ligação de serviço envia estas informações quando verifica a existência de atualizações. Se o ponto de ligação de serviço estiver no modo offline, as informações são transferidas ao utilizar a ferramenta de ligação de serviço.

O Configuration Manager recolhe os dados apenas a partir SQL server da base de dados do site e não recolhe dados diretamente a partir de clientes ou servidores de site.

Administradores podem alterar o nível dos dados recolhidos pelo vai o **dados de utilização** secção da consola do Configuration Manager.

Para obter mais informações, consulte os artigos "Mais informações" sobre níveis de dados de utilização e definições no [diagnósticos e dados de utilização para o System Center Configuration Manager](https://go.microsoft.com/fwlink/?LinkID=626566) artigo.


## <a name="customer-experience-improvement-program"></a>Programa de Melhoramento da Experiência do Cliente

> [!Note]  
> A partir do Configuration Manager versão 1802 a funcionalidade CEIP é removida do produto.

O programa de melhoramento da experiência do cliente (PMEC) recolhe informações básicas da consola do Configuration Manager sobre a configuração de hardware e como utilizar o nosso software e serviços para identificar tendências e padrões de utilização. O PMEC também recolhe o tipo e número de erros que encontrar, desempenho de hardware e software e a velocidade dos serviços. Não iremos recolher o nome, endereço ou outras informações de contacto. Não são recolhidos dados do PMEC a partir de computadores cliente.

Utilizamos estas informações para melhorar a qualidade, a fiabilidade e o desempenho do software e serviços da Microsoft.

Para obter mais informações sobre as informações recolhidas, processadas ou transmitidas pelo PMEC, consulte o [declaração de privacidade do PMEC](https://go.microsoft.com/fwlink/?LinkID=525211).

## <a name="operations-management-suite-connector"></a>Conector do Operations Management Suite
O conector do Microsoft Operations Management Suite sincroniza-se dados, tais como coleções, do System Center Configuration Manager, no Microsoft Operations Management Suite. O ID de subscrição do Microsoft Azure e a chave secreta são armazenados na base de dados do Configuration Manager quando um administrador configura a funcionalidade. O segredo do cliente do Azure Active Directory e a chave partilhada de área de trabalho do Microsoft Operations Management Suite são armazenadas na base de dados do System Center Configuration Manager no local. Todas as comunicações entre o System Center Configuration Manager e do Microsoft Operations Management Suite utilizam HTTPS. Não existem informações adicionais sobre as coleções são fornecidas para a Microsoft fora os dados telemétricos aleatório. Para obter detalhes sobre as informações que recolhe do Microsoft Operations Management Suite, consulte [registo de segurança de análise](https://go.microsoft.com/fwlink/?LinkId=823545).

## <a name="asset-intelligence"></a>Asset Intelligence
O Asset Intelligence permite que os administradores de TI definir, controlar e gerir proativamente a conformidade com as normas de configuração. A medição e elaboração de relatórios relativamente à implementação e utilização de aplicações físicas e virtuais permitem que as empresas tomem decisões comerciais mais corretas em termos de licenciamento de software e mantenham a compatibilidade com os contratos de licenciamento. Depois de recolher dados de utilização de clientes do Configuration Manager, os administradores podem utilizar várias funcionalidades para ver os dados, incluindo coleções, consultas e relatórios.

Durante cada sincronização, é transferido um catálogo de software conhecido da Microsoft. Administradores de TI podem optar por enviar as informações da Microsoft sobre títulos de software não categorizados detetados dentro das suas organizações para serem investigados e adicionados ao catálogo. Antes de carregar estas informações, uma caixa de diálogo mostra os dados que vão ser carregado. Não é possível resgatar os dados carregados. O Asset Intelligence não envia informações sobre utilizadores e computadores nem sobre a utilização de licenças para a Microsoft.

Após um título de software, os investigadores da Microsoft identificam, categorizam e disponibilizam conhecimentos para todos os clientes que utilizam esta funcionalidade e outros consumidores do catálogo de. Os títulos de software carregados passam a ser públicos. A aplicação e a respetiva categorização passam a fazer parte do catálogo e, em seguida, podem ser transferidos por outros consumidores do catálogo. Antes de configurar a recolha de dados do Asset Intelligence e decidir se pretende enviar informações para a Microsoft, tenha em consideração os requisitos de privacidade da sua empresa.

Asset Intelligence não está ativado no System Center Configuration Manager por predefinição. O carregamento de títulos não categorizados nunca ocorre de forma automática e o sistema não foi concebido para automatizar esta tarefa. Deve selecionar e aprovar manualmente o carregamento de cada título de software.

## <a name="endpoint-protection"></a>Endpoint Protection
Serviço de proteção do Microsoft Cloud era anteriormente conhecido como Microsoft Active Protection Service ou MAPS.
Os produtos aplicáveis são System Center Endpoint Protection e a funcionalidade Endpoint Protection do System Center Configuration Manager (Gerir o System Center Endpoint Protection e o Windows Defender para Windows 10). Esta funcionalidade não está implementada para System Center Endpoint Protection para Linux ou System Center Endpoint Protection para Mac.

A Comunidade do serviço de proteção de nuvem do Microsoft antimalware é uma voluntária Comunidade mundial online que inclui os utilizadores do System Center Endpoint Protection. Quando associa o serviço de proteção de nuvem do Microsoft System Center Endpoint Protection envia automaticamente informações à Microsoft. A Microsoft utiliza as informações para determinar o software a investigar quanto a potenciais ameaças e para ajudar a melhorar a eficácia do System Center Endpoint Protection. Esta Comunidade ajuda a parar a propagação de novas infeções de software malicioso. Se um relatório de serviço de proteção do Microsoft Cloud inclui detalhes sobre software maligno ou software potencialmente indesejável que o cliente do Endpoint Protection pode conseguir remover, o serviço de proteção do Microsoft Cloud transfere a assinatura mais recente para resolver. Serviço de proteção do Microsoft Cloud pode também detetar "falsos positivos" (em que algo originalmente identificado como software maligno ativa a não deve ser), corrigindo-os.

Relatórios do serviço de proteção do Microsoft Cloud incluem informações sobre potenciais ficheiros de software maligno, como nomes de ficheiros, hash criptográfico, fornecedor, tamanho e carimbos de data. Além disso, o serviço de proteção do Microsoft Cloud pode recolher URLs completos para indicar a origem do ficheiro. Estes URLs ocasionalmente, poderão ter informações pessoais como termos de pesquisa ou dados que foi introduzidos em formulários. Os relatórios também podem incluir as ações que demorou quando o Endpoint Protection é notificado sobre software indesejável. Relatórios do serviço de proteção do Microsoft Cloud incluem estas informações para ajudar a Microsoft a avaliar como eficazmente o Endpoint Protection pode detetar e remover malware e software potencialmente indesejável e para tentar identificar novo software maligno.

Pode associar o serviço de proteção do Microsoft Cloud se tiver uma adesão básica ou avançada. Os relatórios para membros básicos tem as informações descritas anteriormente. Avançadas membro relatórios são mais compreensivos e podem incluir detalhes adicionas sobre o software detetado pelo Endpoint Protection, como a localização desse software, nomes de ficheiro, como o software funciona e como afetou o seu computador. Estes relatórios e relatórios de outros utilizadores de Endpoint Protection que participam na ajuda do serviço de proteção do Microsoft Cloud, os investigadores da Microsoft descobrir novas ameaças mais rapidamente. Definições de software maligno, em seguida, são criadas para programas que satisfazem os critérios da análise e as definições atualizadas são disponibilizadas para todos os utilizadores através do Microsoft Update.

Para ajudar a detetar e corrigir determinados tipos de infeções de malware, o produto envia regularmente informações do serviço de proteção de nuvem do Microsoft sobre o estado de segurança do seu PC. Estas informações incluem informações sobre as definições de segurança do seu PC e ficheiros de registo que descrevem os controladores e outro software que é carregado enquanto o computador arranca.
Também é enviado um número que identifica exclusivamente o seu PC. Além disso, o serviço de proteção de nuvem do Microsoft poderá recolher os endereços IP que os potenciais ficheiros de software maligno à.

Relatórios do serviço de proteção de nuvem do Microsoft são utilizados para melhorar o software e serviços Microsoft. Os relatórios também podem ser utilizados para fins analíticos ou estatísticos ou outros testes e para gerar definições. Apenas os funcionários da Microsoft, contratantes, parceiros e fornecedores que tenham uma empresa tem de utilizar os relatórios podem aceder aos mesmos.

Serviço de proteção de nuvem do Microsoft não recolhe intencionalmente informações pessoais. Mesmo que serviço de proteção do Microsoft Cloud recolhe quaisquer informações pessoais, a Microsoft não utiliza as informações para o identificar ou contactar.

Detalhes adicionais sobre os dados recolhidos podem ser encontrados na documentação do produto em [Endpoint Protection no System Center Configuration Manager](https://go.microsoft.com/fwlink/?LinkId=823547).

## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Hierarquia do site – vista geográfica com Bing Maps
Hierarquia do site - a vista geográfica permite-lhe utilizar o maps Microsoft Bing Maps fornece para visualizar a topologia de servidor físico do Configuration Manager. Para ativar esta funcionalidade, informações de localização que fornecer são enviadas do seu servidor para o serviço Bing Maps Web.

A Microsoft utiliza as informações para explorar e melhorar o Microsoft Bing Maps e outros serviços e sites da Microsoft. Para obter mais informações, consulte o [declaração de privacidade do Microsoft](https://go.microsoft.com/fwlink/?LinkId=823548).
Pode optar por não utilizar a Vista Geográfica da Hierarquia do Site. A vista de diagrama de hierarquia permite-lhe ver a hierarquia e não utiliza o serviço do Bing Maps.

## <a name="microsoft-intune-subscription"></a>Subscrição do Microsoft Intune
Os clientes que comprou a uma subscrição do Microsoft Intune podem utilizar o Configuration Manager para gerir os respetivos dispositivos móveis que estão ligados através do Microsoft Intune. [Declaração de privacidade do Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=262214) aplica-se o Microsoft online Services, que inclui o Microsoft Intune. Se os clientes também têm uma subscrição do Microsoft Intune, o [declaração de privacidade do Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=262214) deve ser lida juntamente com a presente declaração de privacidade.

Todas as comunicações com o Microsoft Intune utilizam HTTPS. Para configurar a subscrição do Microsoft Intune e para transferir o certificado de solicitação de assinatura (CSR) para configurar o suporte do iOS, um administrador deve iniciar sessão no Microsoft Intune utilizando a conta profissional e a palavra-passe. Estas credenciais não são armazenadas no Configuration Manager. Todas as outras comunicações com o Microsoft Intune são autenticadas utilizando certificados PKI que gera automaticamente Microsoft Intune.

Para gerir dispositivos que estão ligados ao Microsoft Intune, algumas informações é enviadas e recebidas a partir do Microsoft Intune. Estas informações incluem o utilizador nome Principal (UPN) de todos os utilizadores que são atribuídos às informações de inventário de serviço e dispositivo para os dispositivos que são geridos pelo Microsoft Intune. Os metadados, como o nome da aplicação, publicador e versão para o conteúdo que é atribuído aos pontos de distribuição Manage.Microsoft.com são enviados para o Microsoft Intune. O conteúdo do binário real atribuído a um ponto de distribuição Manage.Microsoft.com é encriptado antes de ser carregado para o Microsoft Intune.

Por predefinição, esta funcionalidade não está configurada. Administradores de controlam o conteúdo que é transferido para o ponto de distribuição Manage.Microsoft.com e os utilizadores que estão atribuídos ao serviço. A funcionalidade pode ser removida em qualquer altura.

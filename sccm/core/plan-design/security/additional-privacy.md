---
title: "Declaração de privacidade do System Center Configuration Manager - informações adicionais | Documentos do Microsoft"
description: "Saiba mais sobre como a Microsoft recolhe e utiliza dados a partir de uma implementação do System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translation.priority.ht:
- cs-cz
- de-de
- en-gb
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
ms.sourcegitcommit: 47d473b3884c3cd2ff7516629a7c32d4e52ac39b
ms.openlocfilehash: ef7b3656f9b4a31e07227aa4e864448d0dd1fcdc
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="additional-information-about-privacy-for-system-center-configuration-manager"></a>Informações adicionais sobre a privacidade para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


## <a name="updates-and-servicing"></a>As atualizações e manutenção
System Center Configuration Manager apresenta um novo modelo de atualização que ajuda a manter a implementação do Configuration Manager atual com as mais recentes atualizações e funcionalidades. Quando é instalada, esta funcionalidade adiciona uma nova função de sistema de sites tem chamado para o ponto de ligação de serviço a um servidor de site que escolhe um administrador. Para obter detalhes sobre as informações recolhidas e como são utilizadas, consulte a secção de dados de utilização neste artigo.


## <a name="usage-data"></a>Dados de utilização
System Center Configuration Manager recolhe diagnostics e dados de utilização sobre si, o qual a Microsoft utiliza para melhorar a experiência de instalação, qualidade e segurança dos lançamentos futuros.
Dados de utilização de diagnóstico e está ativada para cada hierarquia do System Center Configuration Manager. Ele consiste em consultas de SQL Server que são executadas semanalmente em cada site primário e para o site de administração central. Quando a hierarquia utiliza um site de administração central, os dados de sites primários são replicados para esse site. No site de nível superior da hierarquia, o ponto de ligação de serviço envia as informações quando verifica a existência de atualizações. Se o ponto de ligação de serviço estiver no modo offline, as informações são transferidas ao utilizar a ferramenta de ligação de serviço.

O Configuration Manager recolhe dados apenas a partir da base de dados de servidor do site SQL, e não recolhe dados diretamente a partir de clientes ou servidores de sites.

Os administradores podem alterar o nível de dados que são recolhidos indo para o **dados de utilização** secção da consola do Configuration Manager.

Para mais informações, consulte os artigos de "Obter mais informações" de mensagens em fila sobre níveis de dados de utilização e definições do [diagnósticos e dados de utilização para o System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626566) artigo.


## <a name="customer-experience-improvement-program"></a>Programa de Melhoramento da Experiência do Cliente
O programa de melhoramento da experiência de cliente (CEIP) recolhe informações básicas a partir da consola do Configuration Manager sobre a configuração do hardware e como utilizar o nosso software e serviços para identificar tendências e padrões de utilização. O PMEC também recolhe o tipo e número de erros que encontrar, desempenho do software e hardware e a velocidade dos serviços. Não iremos recolher o seu nome, endereço ou outras informações de contacto. Não são recolhidos dados do PMEC a partir de computadores cliente.

Utilizamos estas informações para melhorar a qualidade, a fiabilidade e o desempenho do software e serviços da Microsoft.

Para mais informações sobre as informações recolhidas, processadas ou transmitidas pelo PMEC, consulte o [declaração de privacidade do PMEC](http://go.microsoft.com/fwlink/?LinkID=525211).

## <a name="operations-management-suite-connector"></a>Conector do Operations Management Suite
O conector de conjunto de aplicações do Microsoft Operations gestão sincroniza os dados, tais como coleções, a partir do System Center Configuration Manager, ao conjunto de aplicações do Microsoft Operations gestão. O ID de subscrição do Microsoft Azure e a chave secreta são armazenados na base de dados do Configuration Manager quando um administrador configura a funcionalidade. O segredo do cliente do Azure Active Directory e a chave partilhada do conjunto de aplicações do Microsoft Operations gestão área de trabalho são armazenadas na base de dados do System Center Configuration Manager no local. Todas as comunicações entre o System Center Configuration Manager e o conjunto de aplicações do Microsoft Operations gestão utilizam HTTPS. Não existem informações adicionais sobre as coleções são fornecidas para a Microsoft fora dados telemétricos aleatório. Para obter detalhes sobre as informações que o conjunto de aplicações do Microsoft Operations gestão recolhe, consulte o artigo [registo de segurança de análise](http://go.microsoft.com/fwlink/?LinkId=823545).

## <a name="asset-intelligence"></a>Asset Intelligence
Asset Intelligence permite aos administradores de TI definir, controlar e gerir proativamente a conformidade com as normas de configuração. A medição e elaboração de relatórios relativamente à implementação e utilização de aplicações físicas e virtuais permitem que as empresas tomem decisões comerciais mais corretas em termos de licenciamento de software e mantenham a compatibilidade com os contratos de licenciamento. Após a recolha de dados de utilização a partir de clientes do Configuration Manager, os administradores podem utilizar várias funcionalidades para ver os dados, incluindo coleções, consultas e relatórios.

Durante cada sincronização, é transferido um catálogo de software conhecido da Microsoft. Administradores de TI podem optar por enviar informações da Microsoft sobre títulos de software não categorizados detetados dentro das suas empresas para serem investigados e adicionados ao catálogo. Antes de carregar estas informações, uma caixa de diálogo mostra os dados que vão ser carregado. Não é possível resgatar os dados carregados. O Asset Intelligence não envia informações sobre utilizadores e computadores nem sobre a utilização de licenças para a Microsoft.

Depois de um título de software é carregado, os investigadores da Microsoft identificam, categorizar e disponibilizam conhecimentos para todos os clientes que utilizam esta funcionalidade e para outros consumidores do catálogo. Os títulos de software carregados passam a ser públicos. A aplicação e a respetiva categorização tornam-se parte do catálogo e, em seguida, podem ser transferidos por outros consumidores do catálogo. Antes de configurar a recolha de dados do Asset Intelligence e decidir se pretende enviar informações para a Microsoft, tenha em consideração os requisitos de privacidade da sua empresa.

Asset Intelligence não está ativado no System Center Configuration Manager por predefinição. O carregamento de títulos não categorizados nunca ocorre de forma automática e o sistema não foi concebido para automatizar esta tarefa. Deve selecionar e aprovar manualmente o carregamento de cada título de software.

## <a name="endpoint-protection"></a>Endpoint Protection
Serviço de proteção de nuvem Microsoft era anteriormente conhecido como o serviço de proteção ativa Microsoft ou mapas.
Produtos aplicáveis são System Center Endpoint Protection e a funcionalidade Endpoint Protection do System Center Configuration Manager (para gerir o System Center Endpoint Protection e o Windows Defender para Windows 10). Esta funcionalidade não é implementada no System Center Endpoint Protection para Linux ou System Center Endpoint Protection para Mac.

A Comunidade de proteção contra software maligno do serviço de proteção de nuvem Microsoft é uma voluntária Comunidade mundial online que inclui os utilizadores do System Center Endpoint Protection. Quando se junta o serviço de proteção de nuvem Microsoft, o System Center Endpoint Protection envia automaticamente informações à Microsoft. A Microsoft utiliza as informações para determinar o software a investigar quanto a potenciais ameaças, ajudando a melhorar a eficácia do System Center Endpoint Protection. Esta Comunidade ajuda a impedir a propagação de novas infeções de software malicioso. Se um relatório de serviço de proteção de nuvem Microsoft inclui detalhes sobre malware ou software potencialmente indesejável que o cliente do Endpoint Protection seja capaz de remover, o serviço de proteção de nuvem Microsoft transfere a assinatura mais recente para resolver. Serviço de proteção de nuvem Microsoft pode também detetar "falsos positivos" (em que algo originalmente identificado como software maligno revela não deve ser), corrigindo-os.

Serviço de proteção de nuvem Microsoft relatórios incluem informações sobre potenciais ficheiros de malware, como nomes de ficheiros, hash criptográfico, fornecedor, tamanho e carimbos de data. Além disso, o serviço de proteção de nuvem Microsoft pode recolher URLs completos para indicar a origem do ficheiro. Estes URLs, ocasionalmente, poderão ter informações pessoais como termos de pesquisa ou dados que foi introduzidos em formulários. Os relatórios também podem incluir ações que demorou ao Endpoint Protection notificados se software indesejável. Relatórios de serviço de proteção de nuvem Microsoft incluem esta informação para ajudar a Microsoft a avaliar como eficazmente o Endpoint Protection pode detetar e remover e software maligno software potencialmente indesejável e para tentar identificar novo software maligno.

Pode participar serviço de proteção de nuvem Microsoft se tiver uma adesão básica ou avançada. Membros no nível básico relatórios têm as informações descritas anteriormente. Avançado membro relatórios são mais compreensivos e podem incluir detalhes adicionas sobre o software detetado pelo Endpoint Protection, como a localização desse software, nomes dos ficheiros, como o software funciona e como afetou o seu computador. Estes relatórios e relatórios de outros utilizadores de Endpoint Protection que participam na ajuda do serviço de proteção de nuvem Microsoft, os investigadores da Microsoft descobrir novas ameaças mais rapidamente. Definições de software maligno são então criadas para programas que satisfazem os critérios da análise e as definições atualizadas são disponibilizadas a todos os utilizadores através do Microsoft Update.

Para ajudar a detetar e corrigir determinados tipos de infeções de malware, o produto envia regularmente informações do serviço de proteção de nuvem Microsoft sobre o estado de segurança do seu PC. Estas informações incluem informações sobre as definições de segurança do seu PC e ficheiros de registo que descrevem os controladores e outro software que é carregado enquanto o computador arranca.
Também é enviado um número que identifica exclusivamente o seu PC. Além disso, o serviço de proteção de nuvem Microsoft poderá recolher os endereços IP que os potenciais ficheiros de software maligno que estabelecer ligação com.

Relatórios de serviço de proteção de nuvem Microsoft são utilizados para melhorar o software e serviços Microsoft. Os relatórios também podem ser utilizados para fins analíticos ou estatísticos ou outros testes e para gerar definições. Apenas funcionários da Microsoft, empreiteiros, parceiros e fornecedores que tenham necessidade dos utilizar os relatórios podem aceder aos mesmos.

Serviço de proteção de nuvem Microsoft não recolhe intencionalmente informações pessoais. Na medida em que serviço de proteção de nuvem Microsoft recolha informações pessoais, a Microsoft não utiliza as informações para o identificar ou contactar.

Podem encontrar detalhes adicionais sobre dados recolhidos na documentação do produto em [Endpoint Protection no System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkId=823547).

## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Hierarquia do site – vista geográfica com Bing Maps
Hierarquia do site – vista geográfica permite-lhe utilizar mapas que Microsoft Bing Maps fornece para visualizar a topologia de servidor físico do Configuration Manager. Para ativar esta funcionalidade, são enviadas informações de localização que fornece a partir do seu servidor para o serviço Bing Maps Web.

A Microsoft utiliza as informações para explorar e melhorar o Microsoft Bing Maps e outros serviços e sites da Microsoft. Para obter mais informações, consulte o [declaração de privacidade do Microsoft](http://go.microsoft.com/fwlink/?LinkId=823548).
Pode optar por não utilizar a Vista Geográfica da Hierarquia do Site. A vista de diagrama da hierarquia permite-lhe ver a hierarquia e não utiliza o serviço Bing Maps.

## <a name="microsoft-intune-subscription"></a>Subscrição do Microsoft Intune
Os clientes que comprou uma subscrição do Microsoft Intune podem utilizar o Configuration Manager para gerir os dispositivos móveis que estejam ligados através do Microsoft Intune. [Declaração de privacidade do Microsoft Online Services](http://go.microsoft.com/fwlink/?LinkId=262214) aplica-se para os serviços online da Microsoft, que inclui o Microsoft Intune. Se os clientes também tiverem uma subscrição do Microsoft Intune, o [declaração de privacidade do Microsoft Online Services](http://go.microsoft.com/fwlink/?LinkId=262214) deve ser lida juntamente com a presente declaração de privacidade.

Todas as comunicações com o Microsoft Intune utilizam HTTPS. Para configurar a subscrição do Microsoft Intune e para transferir o certificado de assinatura do pedido (CSR) necessário para configurar o suporte do iOS, um administrador deve iniciar sessão no Microsoft Intune utilizando uma conta institucional e a palavra-passe. Estas credenciais não são armazenadas no Configuration Manager. Todas as outras comunicações com o Microsoft Intune são autenticadas utilizando certificados PKI que gera automaticamente Microsoft Intune.

Para gerir dispositivos ligados ao Microsoft Intune, algumas informações são enviadas e recebidas a partir do Microsoft Intune. Estas informações incluem o utilizador nome Principal (UPN) de todos os utilizadores que estão atribuídos às informações de inventário do serviço e de dispositivos para os dispositivos que são geridos pelo Microsoft Intune. Os metadados, como o nome da aplicação, publicador e versão para o conteúdo que é atribuído aos pontos de distribuição Manage.Microsoft.com são enviados para o Microsoft Intune. O conteúdo do binário real atribuído a um ponto de distribuição Manage.Microsoft.com é encriptado antes de ser carregado para o Microsoft Intune.

Por predefinição, esta funcionalidade não está configurada. Os administradores controlam o conteúdo que é transferido para o ponto de distribuição Manage.Microsoft.com e os utilizadores a quem estão atribuídos ao serviço. A funcionalidade pode ser removida em qualquer altura.


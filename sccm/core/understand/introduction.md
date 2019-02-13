---
title: Introdução
titleSuffix: Configuration Manager
description: Obtenha informações básicas, como uma introdução ao System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 10e30b2446d1b2f51d2de8d97c4d8b084357ae32
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133390"
---
# <a name="introduction-to-system-center-configuration-manager"></a>Introdução ao System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Um produto no pacote do Microsoft System Center de soluções de gestão, System Center Configuration Manager pode ajudá-lo a gerir dispositivos e utilizadores no local e na cloud.  

**Pode utilizar o Configuration Manager para o ajudar a:**   
-   Aumentar a produtividade e eficiência ao reduzir as tarefas manuais e permitindo que se concentre em projetos de alto valor.  
-   Maximize os investimentos de hardware e software.  
-   Aumentar a produtividade do usuário por disponibilizar o software adequado no momento certo.  

**Configuration Manager ajuda a fornecer serviços de TI mais eficazes ao permitir:**  

-   Implementação de software segura e escalável.  
-   Gestão de definições de conformidade.  
-   Gestão abrangente de recursos de servidores, computadores de secretária, computadores portáteis e dispositivos móveis.  

**Configuration Manager expande e funciona em conjunto com as suas soluções e tecnologias Microsoft já existentes.**  

Por exemplo, o Configuration Manager integra-se com:  

-   Microsoft Intune para gerir uma ampla variedade de plataformas de dispositivos móveis.  
-   Windows Server Update Services (WSUS) para gerir atualizações de software.  
-   Serviços de certificados.  
-   Exchange Server e Exchange Online.  
-   Política de grupo do Windows.
-   DNS.   
-   Windows Automated Deployment Kit (Windows ADK) e o User State Migration Tool (USMT).  
-   Os serviços de implantação do Windows (WDS).  
-   Assistência remota e ambiente de trabalho remota.  

O Configuration Manager também utiliza:  

-   Serviços de Domínio do Active Directory para fins de segurança, localização de serviço e configuração, bem como para detetar os utilizadores e os dispositivos que pretende gerir.  
-   Microsoft SQL Server como uma base de dados de gestão de alterações distribuída — e integra-se com o SQL Server Reporting Services (SSRS) para produzir relatórios para monitorar e controlar atividades de gestão.  
-   Funções de sistema de sites que expandem a funcionalidade de gestão e utilizam os serviços web dos serviços de informação Internet (IIS).
-   Serviço de Transferência Inteligente em Segundo Plano (BITS) e BranchCache para ajudar a gerir a largura de banda disponível da rede.  

Para ter êxito com o Configuration Manager, primeiro tem minuciosamente planejar e testar as funcionalidades de gestão antes de utilizar o Configuration Manager num ambiente de produção. Como uma aplicação de gestão poderosa, o Configuration Manager tem o potencial de afetar todos os computadores na sua organização. Quando implementar e gerir o Configuration Manager com o planejamento cuidadoso e tendo em conta os requisitos de negócio, o Configuration Manager pode reduzir a sobrecarga administrativa e o custo total de propriedade.  

Utilize os seguintes tópicos e as secções adicionais deste tópico para saber mais sobre o Configuration Manager.  


**Tópicos relacionados nesta biblioteca de documentação:**  

-   [Funcionalidades e capacidades removidas do System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md)  
-   [Escolher uma solução de gestão de dispositivos para o System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  
-   [Alterações em relação ao System Center Configuration Manager, a partir do System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)
-   [Noções Básicas do System Center Configuration Manager](../../core/understand/fundamentals.md)  
-   [Avaliar o System Center Configuration Manager ao criar o seu ambiente de laboratório](/sccm/core/get-started/set-up-your-lab)
-   [Encontrar ajuda para utilizar o System Center Configuration Manager](../../core/understand/find-help.md)  
-   [Itens removidos e preteridos do System Center Configuration Manager](../../core/plan-design/changes/deprecated/removed-and-deprecated.md)  

##  <a name="BKMK_Console"></a> A consola do Configuration Manager  
 Depois de instalar o Configuration Manager, utilize a consola do Configuration Manager para configurar os sites e clientes e para executar e monitorizar tarefas de gestão. Esta consola é o principal ponto de administração e permite-lhe gerir vários sites.  

 Pode utilizar a consola para executar consolas secundárias que fornecem suporte para tarefas de gestão de cliente específicas, tais como:  

-   **Explorador de Recursos**, para ver informações de inventário de hardware e software.  
-   **Controlo remoto**, para ligar remotamente a um computador cliente para executar tarefas de resolução de problemas.  

Pode instalar a consola do Configuration Manager em computadores adicionais e restringir o acesso e limitar o que os utilizadores administrativos podem ver na consola do utilizando a administração baseada em funções do Configuration Manager.  

Para obter mais informações, veja [Instalar consolas do System Center Configuration Manager](../../core/servers/deploy/install/install-consoles.md).

##  <a name="BKMK_ApplicationCatalog"></a> O Catálogo de Aplicações, o Centro de Software e o Portal da Empresa  
 O **Catálogo de Aplicações** é um site onde os utilizadores podem procurar e pedir software para os seus PCs baseados em Windows. Para utilizar o Catálogo de Aplicações, tem de instalar o ponto do serviço Web do Catálogo de Aplicações e o ponto do Web site do Catálogo de Aplicações.  

 **Centro de software** é uma aplicação que é instalada quando o cliente do Configuration Manager está instalado em computadores baseados em Windows. Os utilizadores executam esta aplicação para solicitar software e gerir o software que implementa o Configuration Managê-los. O Centro de Software permite aos utilizadores efetuarem o seguinte:  

-   Procurar e instalar software a partir do catálogo de aplicações.  
-   Ver o respetivo histórico de pedidos de software.  
-   Configure quando o Configuration Manager pode instalar software nos respetivos dispositivos.  
-   Configure definições de acesso para controlo remoto, se um utilizador administrativo ativado o controlo remoto.  

**O Portal da empresa** é uma aplicação ou site que fornece funções semelhantes ao catálogo de aplicações, mas para dispositivos móveis inscritos pelo Microsoft Intune.  

Para obter mais informações, consulte [introdução à gestão de aplicações no System Center Configuration Manager](../../apps/understand/introduction-to-application-management.md).  

###  <a name="BKMK_Client"></a> Propriedades do Configuration Manager (em Windows PCs)  
 Quando o cliente do Configuration Manager é instalado em computadores Windows, o Configuration Manager está instalado no painel de controlo. Normalmente, não precisa de configurar esta aplicação porque a configuração de cliente é efetuada na consola do Configuration Manager. Esta aplicação ajuda os utilizadores administrativos e o suporte técnico a resolver problemas relacionados com clientes individuais.  

 Para obter mais informações sobre a implementação do cliente, veja [Métodos de instalação de cliente no System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md).  

##  <a name="BKMK_ExampleScenarios"></a> Cenários exemplo para o Configuration Manager  
 Os cenários de exemplo seguintes demonstram como uma empresa chamada Trey Research utiliza o System Center Configuration Manager para permitir aos utilizadores:  

-   Se mais produtivos.  
-   Unificar a gestão da compatibilidade dos dispositivos para uma experiência de administração mais simplificada.
-   Simplificar a gestão de dispositivos para reduzir os custos operacionais de TI.  

Em todos os cenários, Afonso é o administrador principal para o Configuration Manager.  

###  <a name="BKMK_ScenarioEmpower"></a> Cenário exemplo: Capacitar os usuários, garantindo o acesso às aplicações a partir de qualquer dispositivo  
 Trey Research pretende assegurar que os funcionários tenham acesso aos aplicativos que precisam, mais eficientemente possível. O Afonso mapeia estes requisitos da empresa para os seguintes cenários:  

|Requisito|Estado da atual gestão do cliente|Estado da gestão futura do cliente|  
|-----------------|-------------------------------------|------------------------------------|  
|Os novos funcionários podem trabalhar de forma eficaz desde o primeiro dia.|Quando os funcionários ingressam na empresa, têm de esperar por aplicativos a serem instalados após iniciarem sessão pela primeira vez.|Quando os funcionários ingressam na empresa, iniciam sessão e seus aplicativos estão instalados e prontos a utilizar.|  
|Os funcionários podem solicitar de forma rápida e simples o software adicional de que necessitam.|Quando os funcionários têm de aplicações adicionais, enviam um ticket com o suporte técnico. Em seguida, normalmente, aguardam dois dias para o ticket seja processado e para os aplicativos a serem instalados.|Quando os funcionários têm de aplicações adicionais, pode solicitá-los a partir de um Web site. Serão instaladas imediatamente se não existirem restrições de licenciamento. Se existirem restrições de licenciamento, os utilizadores devem primeiro solicitar a aprovação para poderem instalar a aplicação.<br /><br /> O Web site mostra os utilizadores apenas as aplicações que eles têm permissão para instalar.|  
|Os funcionários podem utilizar os seus dispositivos móveis no local de trabalho se os dispositivos cumprirem as políticas de segurança que são controladas e impostas.<br /><br /> Estas políticas incluem impor uma palavra-passe segura, bloquear um dispositivo após o período de inatividade e limpar remotamente dispositivos perdidos ou roubados.|Os funcionários ligam os seus dispositivos móveis ao Exchange Server para o serviço de e-mail. Mas, para confirmar que estão em conformidade com as políticas de segurança nas políticas de caixa de correio do Exchange ActiveSync padrão. A utilização pessoal de dispositivos móveis poderá ser proibida, a menos que as TI possam confirmar a adesão à política.|A organização de TI pode informar a compatibilidade de segurança do dispositivo móvel com as definições necessárias. Esta confirmação permite que os utilizadores continuem a utilizar os seus dispositivos móveis no local de trabalho. Os utilizadores podem apagar remotamente o dispositivo móvel se ele de perda ou roubo e o suporte técnico pode apagar dispositivos móveis de qualquer utilizador declarado como perdido ou roubado.<br /><br /> Fornece o registo do dispositivo móvel num ambiente PKI para segurança e controlo adicionais.|  
|Os funcionários podem ser produtivos, mesmo que não estejam nas suas secretárias.|Quando os funcionários não estão nas suas secretárias e não possuem computadores portáteis, eles não é possível acessar seus aplicativos utilizando os computadores de quiosque que estão disponíveis em toda a empresa.|Os funcionários podem utilizar computadores de quiosque para aceder às suas aplicações e dados.|  
|Normalmente, a continuidade do negócio tem precedência sobre a instalação de aplicações e atualizações de software necessárias.|Muitas vezes, as aplicações e atualizações de software que requerem instalação durante o dia interrompem o trabalho dos utilizadores, uma vez que os seus computadores ficam mais lentos ou são reiniciados durante a instalação.|Os utilizadores podem configurar o seu horário de trabalho para impedir que o software necessário seja instalado enquanto estiver a utilizar o computador.|  

 Para cumprir os requisitos, Afonso utiliza estas capacidades de gestão do Configuration Manager e as opções de configuração:  

-   Gestão de aplicações  
-   Gestão de dispositivos móveis  

Implementa-as utilizando os passos de configuração na tabela a seguir:  

|Passos de configuração|Resultado|  
|-------------------------|-------------|  
|O Afonso certifica-se de que os novos utilizadores têm contas de utilizador no Active Directory e cria uma nova coleção baseada em consultas no Configuration Manager para estes utilizadores. Define então a afinidade dispositivo/utilizador para estes utilizadores, criando um ficheiro que mapeia as contas de utilizador para os computadores primários que utilizarão e importando esse ficheiro para o Configuration Manager.<br /><br /> As aplicações que os novos utilizadores tem de ter já são criadas no Configuration Manager. Ele, em seguida, implementa as aplicações que têm um objetivo necessário na coleção que contém os novos utilizadores.|Por causa das informações de afinidade de dispositivo do utilizador, as aplicações são instaladas no computador principal ou computadores de cada utilizador antes do utilizador inicia sessão.<br /><br /> Os aplicativos estão prontos a utilizar assim que o utilizador inicia sessão com êxito.|  
|O Afonso instala e configura as funções do sistema de sites do Catálogo de Aplicações para que os utilizadores possam procurar as aplicações a instalar. Cria implementações de aplicações com o objetivo Disponível e implementa tais aplicações na coleção que contém os novos utilizadores.<br /><br /> No caso de aplicações com um número restrito de licenças, o Afonso configura-as para requererem aprovação.|Os utilizadores podem agora utilizar o catálogo de aplicações para procurar as aplicações que eles têm permissão para instalar. Os utilizadores podem, em seguida, instalar os aplicativos imediatamente, ou solicitar a aprovação e regressar ao catálogo de aplicações para instalá-los após a aprovação do pedido de suporte técnico.|  
|O Artur cria um conector do Exchange Server no Configuration Manager para gerir os dispositivos móveis que se ligam ao Exchange Server no local da empresa. Configura este conector com definições de segurança que incluem o requisito para definir uma palavra-passe segura e bloqueiam o dispositivo móvel após um período de inatividade.<br /><br /> Para a gestão adicional para dispositivos que executam o Windows Phone 8, Windows RT e iOS, o Afonso obtém uma subscrição do Microsoft Intune. Em seguida, ele instala a função de sistema de sites de ponto de ligação de serviço. Esta solução de gestão de dispositivos móveis melhora o suporte de gestão da empresa para estes dispositivos. Isto inclui a disponibilizar aplicativos para os utilizadores instalarem sobre estes dispositivos e gerenciamento de configurações extensa. Além disso, as ligações de dispositivos móveis são protegidas por certificados PKI que são automaticamente criados e implementados pelo Intune.<br /><br /> Depois de configurar o ponto de ligação de serviço e a subscrição para utilização com o Configuration Manager, o Afonso envia uma mensagem de e-mail aos utilizadores proprietários destes dispositivos móveis para que cliquem numa ligação para iniciar o processo de inscrição.<br /><br /> Para os dispositivos móveis sejam inscritos pelo Microsoft Intune, o Afonso utiliza definições de compatibilidade para configurar definições de segurança para estes dispositivos móveis. Estas definições incluem o requisito para definir uma palavra-passe segura e bloqueiam o dispositivo móvel após um período de inatividade.|Com estas duas soluções de gestão de dispositivos móveis, o departamento de informática pode fornecer informações para relatórios sobre os dispositivos móveis utilizados na rede empresarial e respetiva compatibilidade com as definições de segurança configuradas.<br /><br /> Os utilizadores são apresentados como apagar remotamente os seus dispositivos móveis ao utilizar o catálogo de aplicações ou o Portal da empresa, se o dispositivo móvel for perdido ou roubado. O suporte técnico também é instruído como apagar remotamente um dispositivo móvel para os utilizadores com a consola do Configuration Manager.<br /><br /> Além disso, para os dispositivos móveis inscritos pelo Microsoft Intune, Afonso pode agora implementar aplicações móveis para os utilizadores a instalar, recolher mais dados de inventário a partir destes dispositivos e têm um melhor controlo de gestão dos dispositivos por ser capaz de aceder a mais definições.|  
|A Trey Research tem vários computadores de quiosque que são utilizados pelos funcionários que visitam o escritório. Os funcionários querem que seus aplicativos para que estejam disponíveis sempre que iniciam sessão. No entanto, o Afonso não pretende instalar localmente todos os aplicativos em cada computador.<br /><br /> Para atingir esse objetivo, o Afonso cria as aplicações necessárias, que têm dois tipos de implementação:<br /><br /> **O primeiro:** Uma instalação local e completa da aplicação que tenha o requisito de que só pode ser instalado no dispositivo primário dos utilizadores.<br /><br /> **O segundo:** Uma versão virtual das aplicações que tenham o requisito de que não poderem ser instaladas no dispositivo primário do utilizador.|Durante a visita a funcionários de início de sessão para um computador de quiosque, verão as aplicações que necessitam ser apresentadas como ícones na área de trabalho do computador de quiosque. Quando executam a aplicação, são transmitido como uma aplicação virtual. Dessa forma, eles podem ser tão produtivos como se elas residem no seu ambiente de trabalho.|  
|Permite o Artur, os utilizadores saibam o que pode configurar o horário comercial no Centro de Software e pode selecionar opções para impedir que atividades de implantação de software durante esse período e quando o computador está no modo de apresentação.|Uma vez que os utilizadores podem controlar quando o Configuration Manager implementa software em seus computadores, mantêm-se mais produtivo durante o dia de trabalho.|  

 Estes passos e resultados de configuração permitem que a Trey Research capacite os seus funcionários, garantindo o acesso às aplicações a partir de qualquer dispositivo.  

###  <a name="BKMK_ScenarioUnify"></a> Cenário exemplo: Uniformizar a gestão de conformidade dos dispositivos  
 A Trey Research procura uma solução unificada de gestão dos clientes que garanta que os seus computadores executam software antivírus que seja automaticamente mantido atualizado. Ou seja:  

-   Firewall do Windows está ativada.  
-   Atualizações de software críticas estão instaladas.  
-   Chaves de registo específicas estão definidas.  
-   Dispositivos móveis geridos não é possível instalar nem executar aplicações não assinadas.  

A empresa pretende também alargar esta proteção à Internet, para computadores portáteis que passem da intranet para a Internet.  

O Afonso mapeia estes requisitos da empresa para os seguintes cenários:  

|Requisito|Estado da atual gestão do cliente|Estado da gestão futura do cliente|  
|-----------------|-------------------------------------|------------------------------------|  
|Todos os computadores executam software antimalware com ficheiros de definições atualizados e que autoriza a Firewall do Windows.|Computadores diferentes executados soluções antimalware diferentes que não são sempre mantidas atualizadas. Embora o Windows Firewall está ativada por predefinição, os utilizadores, às vezes, desativá-la.<br /><br /> É pedido aos utilizadores que contactem o suporte técnico se for detetado malware nos seus computadores.|Todos os computadores executam a mesma solução antimalware, que transfere automaticamente os ficheiros de atualização de definições mais recentes e volta a ativar automaticamente a Firewall do Windows se os utilizadores a desativarem.<br /><br /> Se for detetado malware, o suporte técnico será automaticamente notificado por correio eletrónico.|  
|Todos os computadores instalam as atualizações de software críticas no prazo de um mês a contar do seu lançamento.|Embora as atualizações de software estão instaladas nos computadores, muitos computadores não instalar automaticamente as atualizações de software críticas até duas ou três meses após terem sido lançadas. Isso deixa-os vulneráveis a ataques durante esse período.<br /><br /> Para os computadores que não a instale as atualizações de software críticas, o suporte técnico começa por envia mensagens de e-mail pedir aos utilizadores para instalar as atualizações. Se os computadores se mantiverem não compatíveis, os engenheiros ligam-se remotamente aos computadores e instalam manualmente as atualizações de software em falta.|A taxa de conformidade atual no mês especificado foi melhorada para mais de 95% sem enviar mensagens de e-mail ou solicitar o suporte técnico para instalar manualmente.|  
|Definições de segurança para aplicações específicas são regularmente verificadas e remediadas se não for necessário.|Os computadores executam scripts de arranque complexos que se baseiam na respetiva associação a grupos para repor os valores do registo de aplicações específicas.<br /><br /> Uma vez que estes scripts só são executados no arranque e alguns computadores ficam em dias, não é possível verificar o suporte técnico para os descompassos de configuração de forma atempada.|Os valores do registo são verificados e automaticamente remediados, sem depender da associação do computador a grupos e sem o reiniciar.|  
|Dispositivos móveis não é possível instalar nem executar aplicações não seguras.|É pedido aos utilizadores não para transferir e executar aplicações potencialmente não seguras a partir da Internet. Mas não há nenhum controle em monitorizar e impor tais pedidos.|Dispositivos móveis que são geridos com o Microsoft Intune ou Configuration Manager automaticamente impedem a instalação ou execução aplicações não assinadas.|  
|É necessário proteger os computadores portáteis que passam da intranet para a Internet.|Os utilizadores que viajam, eles frequentemente não é possível ligar através da ligação VPN diariamente. Estes portáteis deixam de estar em conformidade com os requisitos de segurança.|Uma ligação à Internet é tudo o que é necessário para manter a compatibilidade dos computadores portáteis com os requisitos de segurança. Os utilizadores não têm que iniciar sessão ou utilizar a ligação VPN.|  

 Para cumprir os requisitos, Afonso utiliza estas capacidades de gestão do Configuration Manager e as opções de configuração:  

-   Endpoint Protection  
-   Atualizações de software  
-   Definições de compatibilidade  
-   Gestão de dispositivos móveis  
-   Gestão de clientes baseada na Internet  

Implementa-as utilizando os passos de configuração na tabela a seguir:  

|Passos de configuração|Resultado|  
|-------------------------|-------------|  
|O Artur configura o Endpoint Protection. Ele permite que a definição de cliente para desinstalar outras soluções de antimalware e ativa a Firewall do Windows. Configura regras de implementação automática para que os computadores procurem e instalem regularmente as atualizações de definições mais recentes.|A solução antimalware única ajuda a proteger todos os computadores, minimizando a sobrecarga administrativa. Uma vez que o suporte técnico é automaticamente notificado por uma mensagem de e-mail, se for detetado malware, os problemas podem ser resolvidos rapidamente. Isto ajuda a impedir ataques a outros computadores.|  
|Para ajudar a aumentar as taxas de conformidade, Afonso utiliza regras de implementação automática, define as janelas de manutenção para servidores e investiga as vantagens e desvantagens de usar o Wake-on-LAN em computadores que hibernem.|A compatibilidade com as atualizações de software críticas aumenta, reduzindo os requisitos de instalação manual de atualizações de software pelos utilizadores ou pelo suporte técnico.|  
|O Afonso utiliza definições de compatibilidade para verificar a presença das aplicações especificadas. Quando as aplicações são detetadas, os itens de configuração, em seguida, verifique os valores de registo e remedeiam-nos automaticamente se estiverem em conformidade.|Ao utilizar itens de configuração e linhas de base de configuração que são implementadas em todos os computadores e verificar a conformidade de todos os dias, já não requerem scripts separados que se baseiam na associação de computador e o computador seja reiniciado.|  
|O Afonso utiliza as definições de compatibilidade para dispositivos móveis inscritos, configurando o conector do Exchange Server de modo a proibir a instalação e execução de aplicações não assinadas em dispositivos móveis.|Uma vez que são proibidas de aplicações não assinadas, dispositivos móveis são automaticamente protegidos contra aplicações potencialmente prejudiciais.|  
|O Afonso certifica-se de que os servidores de sistema de sites e computadores possuem os certificados PKI exigidos pelo Configuration Manager para ligações HTTPS. Em seguida, ele instala funções do sistema de sites adicionais na rede de perímetro que aceitam ligações de cliente a partir da Internet.|Os computadores que passam da intranet para a Internet continuam automaticamente a ser geridos pelo Configuration Manager quando têm uma ligação à Internet. Esses computadores não dependem dos utilizadores o início de sessão no respetivo computador ou a ligação VPN a ligar.<br /><br /> Estes computadores continuam a ser geridos no que respeita a antimalware e à Firewall do Windows, atualizações de software e itens de configuração. Em resultado, os níveis de compatibilidade aumentam automaticamente.|  

 Estes passos e resultados de configuração permitem à Trey Research unificar com sucesso a gestão de compatibilidade dos dispositivos.  

###  <a name="BKMK_ScenarioSimplify"></a> Cenário exemplo: Simplificar a gestão de clientes de dispositivos  
 A Trey Research quer que todos os novos computadores instalem automaticamente a imagem de computador base da empresa, que executa o Windows 7. Depois da imagem do sistema operativo é instalada nesses computadores, tem de ser geridos e monitorizados para software adicional instalado pelos utilizadores. Os computadores que armazenam informações altamente confidenciais requerem políticas de gestão mais restritivas do que os restantes. Por exemplo, os engenheiros do suporte técnico não devem ligar remotamente a tais computadores, é exigida a introdução do PIN do BitLocker ao reiniciar e apenas os administradores locais podem instalar software.  

 O Afonso mapeia estes requisitos da empresa para os seguintes cenários:  

|Requisito|Estado da atual gestão do cliente|Estado da gestão futura do cliente|  
|-----------------|-------------------------------------|------------------------------------|  
|O Windows 7 é instalado nos novos computadores.|O suporte técnico instala e configura o Windows 7 para os utilizadores e, em seguida, envia o computador para a respetiva localização.|Novos computadores ir diretamente para o destino final, são ligados à rede e automaticamente instalarem e configurar o Windows 7.|  
|Os computadores têm de ser geridos e monitorizados. Isto inclui a recolha de dados de inventário de hardware e software para ajudar a determinar requisitos de licenciamento.|O cliente do Configuration Manager é implementado utilizando a instalação push automática do cliente. O suporte técnico investiga as falhas de instalação e os clientes que não enviam dados de inventário quando é esperado.<br /><br /> As falhas são frequentes devido às dependências de instalação que não são cumpridas e de Corrupção de WMI no cliente.|Os dados de instalação e inventário do cliente recolhidos dos computadores são mais fiáveis e requerem uma menor intervenção do suporte técnico. Os relatórios mostram a utilização do software para obter informações de licenciamento.|  
|Alguns computadores precisam de políticas de gestão mais rigorosas.|Devido às políticas de gestão mais rigorosas, estes computadores não são atualmente geridos pelo Configuration Manager.|Estes computadores são geridos utilizando o Gestor de configuração para acomodar as exceções sem aumentar a sobrecarga administrativa.|  

 Para cumprir os requisitos, Afonso utiliza estas capacidades de gestão do Configuration Manager e as opções de configuração:  

-   Implementação do sistema operativo  
-   Implementação e estado do cliente  
-   Definições de compatibilidade  
-   Definições do cliente  
-   Métodos de inventário e Asset Intelligence  
-   Administração baseada em funções  

Implementa-as utilizando os passos de configuração na tabela a seguir:  

|Passos de configuração|Resultado|  
|-------------------------|-------------|  
|O Artur captura uma imagem de sistema operativo a partir de um computador que tenha o 7 de Windows instalado e configurado com as especificações da empresa. Em seguida, implementa o sistema operativo em novos computadores utilizando o suporte para computadores desconhecidos e o PXE. Ele também instala o cliente do Configuration Manager como parte da implementação do sistema operativo.|Os novos computadores estão ativos e a funcionar mais rapidamente e sem a intervenção do suporte técnico.|  
|O Artur configura a instalação de push automática do cliente em todo o site para instalar o cliente de Configuration Manager em todos os computadores detetados. Isto garante que todos os computadores que não foram instalados com o cliente ainda instalem o cliente para que o computador seja gerido pelo Configuration Manager.<br /><br /> O Artur configura o estado do cliente para retificar automaticamente quaisquer problemas detetados no mesmo. Ele também configura as definições de cliente que permitem a recolha de dados de inventário que é necessário e configura o Asset Intelligence.|Instalar o cliente em conjunto com o sistema operacional é mais rápido e mais fiável do que esperar do Configuration Manager para detetar o computador e, em seguida, tentar instalar os ficheiros de origem do cliente no computador. No entanto, deixando o push do cliente automática opção ativada, é fornecer um método de cópia de segurança para um computador que já tenha o sistema operativo instalado para instalar o cliente quando o computador liga-se à rede.<br /><br /> As definições do cliente garantem que os clientes enviem regularmente as suas informações de inventário para o site. Isso, além dos testes de estado do cliente, ajuda a manter o cliente em execução com intervenção mínima do suporte técnico. Por exemplo, os danos no WMI são detetados e retificados automaticamente.<br /><br /> Os relatórios do Asset Intelligence ajudam a monitorizar a utilização do software e as licenças.|  
|O Artur cria uma coleção para os computadores que têm de ter as definições de política mais rigorosas. Em seguida, ele cria uma definição de dispositivo de cliente personalizadas para esta coleção que desativa o controlo remoto, permite a entrada de PIN do BitLocker e permite que os administradores locais apenas instalar o software.<br /><br /> O Artur configura a administração baseada em funções para que os engenheiros de suporte técnico não vejam esta coleção de computadores. Isto ajuda a garantir que estes computadores não são geridos acidentalmente como computadores padrão.|Estes computadores são agora geridos pelo Configuration Manager, mas com definições específicas que não necessitam de um novo site.<br /><br /> A coleção destes computadores não está visível para os engenheiros de suporte técnico de ajuda. Isto ajuda a reduzir a possibilidade dos computadores que está a ser enviado acidentalmente implementações e scripts para computadores padrão.|  

 Estes passos e resultados de configuração permitem à Trey Research simplificar com sucesso a gestão de clientes dos dispositivos.  

##  <a name="BKMK_NextSteps"></a> Passos seguintes  
 Antes de instalar o Configuration Manager, pode se familiarizar com alguns conceitos e termos básicos específicos para o Configuration Manager.  

-   Se não estiver familiarizado com o System Center 2012 Configuration Manager, veja [o que mudou no System Center Configuration Manager, do System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) para compreender as novas funcionalidades.  
-   Para obter uma alto nível técnica descrição geral do System Center Configuration Manager, consulte [Noções básicas do System Center Configuration Manager](../../core/understand/fundamentals.md).  

Quando estiver familiarizado com os conceitos básicos, utilize a documentação do System Center Configuration Manager para o ajudar a implementar e utilizar o Configuration Manager com êxito.  

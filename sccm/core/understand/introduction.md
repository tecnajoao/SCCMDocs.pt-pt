---
title: "Introdução | Documentos do Microsoft"
description: "Obter informações básicas, como uma introdução ao System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
caps.latest.revision: 16
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 916aac9a8f724e37044884cd73de5fea1f1a8f97
ms.openlocfilehash: 76f907b17df0dd2f102e34ca3cfb3ffc813c0004
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="introduction-to-system-center-configuration-manager"></a>Introdução ao System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Um produto no conjunto de aplicações do Microsoft System Center das soluções de gestão, System Center Configuration Manager pode ajudar a gerir dispositivos e utilizadores no local e na nuvem.  

**Pode utilizar o Configuration Manager para o ajudar a:**   
-   Aumentar a produtividade IT e eficiência ao reduzir as tarefas manuais e permitindo que concentrar-se em projetos de alto valor.  
-   Maximize investimentos de hardware e software.  
-   Aumentar a produtividade dos produtividade do utilizador, fornecendo o software adequado no momento certo.  

**O Configuration Manager ajuda-o a fornecer serviços de TI mais eficientes através da:**  

-   Implementação de software segura e escalável.  
-   Gestão das definições de compatibilidade.  
-   Gestão abrangente de recursos de servidores, computadores de secretária, computadores portáteis e dispositivos móveis.  

**O Configuration Manager expande e funciona em conjunto com as suas tecnologias Microsoft existentes e soluções.**  

Por exemplo, o Configuration Manager integra-se com:  

-   Microsoft Intune para gerir uma ampla variedade de plataformas de dispositivos móveis.  
-   Windows Server Update Services (WSUS) para gerir atualizações de software.  
-   Serviços de certificados.  
-   Exchange Server e o Exchange Online.  
-   Política de grupo do Windows.
-   DNS.   
-   Windows Automated Deployment Kit (Windows ADK) e a ferramenta de migração de estado do utilizador (USMT).  
-   Serviços de implementação do Windows (WDS).  
-   Assistência remota e ambiente de trabalho remota.  

O Configuration Manager também utiliza:  

-   Serviços de Domínio do Active Directory para fins de segurança, localização de serviço e configuração, bem como para detetar os utilizadores e os dispositivos que pretende gerir.  
-   Microsoft SQL Server como uma base de dados de gestão de alterações distribuída — e integra-se com o SQL Server Reporting Services (SSRS) para produzir relatórios para monitorizar e controlar atividades de gestão.  
-   Funções de sistema de sites que expandem as funcionalidades de gestão e utilizam os serviços web dos serviços de informação Internet (IIS).
-   Serviço de Transferência Inteligente em Segundo Plano (BITS) e BranchCache para ajudar a gerir a largura de banda disponível da rede.  

Para ser bem-sucedido com o Configuration Manager, tem primeiro planear e testar cuidadosamente as funcionalidades de gestão antes de utilizar o Configuration Manager num ambiente de produção. Como uma aplicação de gestão poderosa, o Configuration Manager possui o potencial para afetar todos os computadores na sua organização. Quando implementar e gerir o Configuration Manager com um planeamento cuidadoso e tendo em conta os seus requisitos empresariais, o Configuration Manager pode reduzir a sobrecarga administrativa e o custo total de propriedade.  

Utilize os tópicos seguintes e adicionais secções deste tópico para saber mais sobre o Configuration Manager.  


**Tópicos relacionados nesta biblioteca de documentação:**  

-   [Funcionalidades e capacidades do System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md)  
-   [Escolha uma solução de gestão de dispositivos para o System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  
-   [O que é alterado no System Center Configuration Manager, a partir do System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)
-   [Noções básicas do System Center Configuration Manager](../../core/understand/fundamentals.md)  
-   [Avaliar o System Center Configuration Manager ao criar o seu ambiente de laboratório](/sccm/core/get-started/set-up-your-lab)
-   [Obtenha ajuda para utilizar o System Center Configuration Manager](../../core/understand/find-help.md)  
-   [Funcionalidades removidas e preteridas para o System Center Configuration Manager](../../core/plan-design/changes/removed-and-deprecated-features.md)  

##  <a name="BKMK_Console"></a> A consola do Configuration Manager  
 Depois de instalar o Configuration Manager, utilize a consola do Configuration Manager para configurar os sites e clientes e para executar e monitorizar as tarefas de gestão. Esta consola é o principal ponto de administração e permite-lhe gerir vários sites.  

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

**O Portal da empresa** é uma aplicação ou o Web site que fornece funções semelhantes ao catálogo de aplicações, mas para dispositivos móveis que são inscritos pelo Microsoft Intune.  

Para obter mais informações, consulte o artigo [começar com gestão de aplicações no System Center Configuration Manager](../../apps/understand/introduction-to-application-management.md).  

###  <a name="BKMK_Client"></a>Propriedades do Configuration Manager (no Windows PCs)  
 Quando o cliente do Configuration Manager é instalado em computadores Windows, o Configuration Manager está instalado no painel de controlo. Normalmente, não terá de configurar esta aplicação porque a configuração do cliente é efetuada na consola do Configuration Manager. Esta aplicação ajuda os utilizadores administrativos e o suporte técnico a resolver problemas relacionados com clientes individuais.  

 Para obter mais informações sobre a implementação do cliente, veja [Métodos de instalação de cliente no System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md).  

##  <a name="BKMK_ExampleScenarios"></a> Cenários exemplo para o Configuration Manager  
 Os cenários de exemplo seguintes demonstram como uma empresa denominada Trey Research utiliza o System Center Configuration Manager para aumentar a produtividade dos utilizadores para:  

-   Seja mais produtivo.  
-   Unificar a gestão da compatibilidade dos dispositivos para uma experiência de administração mais facilitada.
-   Simplificar a gestão de dispositivos para reduzir os custos operacionais de TI.  

Em todos os cenários, Afonso é o administrador principal do Configuration Manager.  

###  <a name="BKMK_ScenarioEmpower"></a>Cenário de exemplo: Aumentar a produtividade dos utilizadores garantindo o acesso às aplicações a partir de qualquer dispositivo  
 A Trey Research pretende assegurar que os funcionários têm acesso às aplicações de que necessitam, maior eficiência possível. O Afonso mapeia estes requisitos da empresa para os seguintes cenários:  

|Requisito|Estado da atual gestão do cliente|Estado da gestão futura do cliente|  
|-----------------|-------------------------------------|------------------------------------|  
|Os novos funcionários podem trabalhar de forma eficaz desde o primeiro dia.|Quando os funcionários ingressam na empresa, têm de aguardar que as aplicações sejam instaladas depois que iniciarem sessão pela primeira vez.|Quando os funcionários ingressam na empresa, que iniciarem sessão e as suas aplicações são instalada e pronta a ser utilizado.|  
|Os funcionários podem solicitar de forma rápida e simples o software adicional de que necessitam.|Quando os funcionários necessitam de aplicações adicionais, enviam ticket uma o suporte técnico. Em seguida, são normalmente Aguarde dois dias para que o ticket seja processado e para as aplicações ser instalada.|Quando os funcionários necessitam de aplicações adicionais, podem solicitá-las a partir de um Web site. Estas são instaladas de imediato se não existirem restrições de licenciamento. Se existirem restrições de licenciamento, os utilizadores devem primeiro solicitar a aprovação para poderem instalar a aplicação.<br /><br /> O Web site mostra aos utilizadores apenas as aplicações que está autorizados a instalar.|  
|Os funcionários podem utilizar os seus dispositivos móveis no local de trabalho se os dispositivos cumprirem as políticas de segurança que são controladas e impostas.<br /><br /> Estas políticas incluem impor uma palavra-passe, bloquear um dispositivo após período de inatividade e apagar remotamente os dispositivos perdidos ou roubados.|Os funcionários ligam os seus dispositivos móveis ao Exchange Server para o serviço de correio eletrónico. No entanto, não existe para confirmar que estão em conformidade com as políticas de segurança diretivas predefinidas de caixa de correio do Exchange ActiveSync. A utilização pessoal de dispositivos móveis poderá ser proibida, a menos que as TI possam confirmar a adesão à política.|A organização de TI pode informar a compatibilidade de segurança do dispositivo móvel com as definições necessárias. Esta confirmação permite que os utilizadores continuem a utilizar os seus dispositivos móveis no local de trabalho. Os utilizadores podem apagar remotamente os seus dispositivos móveis, caso de perda ou roubo e o suporte técnico pode apagar o dispositivo móvel qualquer utilizador que é comunicado como perdido ou roubado.<br /><br /> Fornece o registo do dispositivo móvel num ambiente PKI para segurança e controlo adicionais.|  
|Os funcionários podem ser produtivos, mesmo que não estão nas suas secretárias.|Quando os funcionários não estão nas suas secretárias e não possuem computadores portáteis, não é possível aceder as suas aplicações através da utilização dos computadores de quiosque que estão disponíveis em toda a empresa.|Os funcionários podem utilizar computadores de quiosque para aceder às suas aplicações e dados.|  
|Normalmente, a continuidade do negócio tem precedência sobre a instalação de aplicações e atualizações de software necessárias.|Muitas vezes, as aplicações e atualizações de software que requerem instalação durante o dia interrompem o trabalho dos utilizadores, uma vez que os seus computadores ficam mais lentos ou são reiniciados durante a instalação.|Os utilizadores podem configurar o seu horário de trabalho para impedir que o software necessário seja instalado enquanto estiver a utilizar os seus computadores.|  

 Para cumprir os requisitos, Afonso utiliza estas capacidades de gestão do Configuration Manager e as opções de configuração:  

-   Gestão de aplicações  
-   Gestão de dispositivos móveis  

Implementa-as utilizando os passos de configuração na tabela seguinte:  

|Passos de configuração|Resultado|  
|-------------------------|-------------|  
|Afonso certifica-se de que novos utilizadores têm contas de utilizador no Active Directory, cria uma nova coleção baseada em consultas no Configuration Manager para estes utilizadores. Define então a afinidade dispositivo/utilizador para estes utilizadores, criando um ficheiro que mapeia as contas de utilizador para os computadores primários que utilizarão e importando esse ficheiro para o Configuration Manager.<br /><br /> As aplicações que novos utilizadores necessitam já se encontram criadas no Configuration Manager. Em seguida, implementa as aplicações que têm um objetivo necessário na coleção que contém os novos utilizadores.|Devido a informações de afinidade de dispositivo do utilizador, as aplicações são instaladas no computador primário ou a computadores de cada utilizador antes do utilizador inicia sessão.<br /><br /> As aplicações estarão prontas a utilizar assim que o utilizador com êxito inicia sessão.|  
|O Afonso instala e configura as funções do sistema de sites do Catálogo de Aplicações para que os utilizadores possam procurar as aplicações a instalar. Cria implementações de aplicações com o objetivo Disponível e implementa tais aplicações na coleção que contém os novos utilizadores.<br /><br /> No caso de aplicações com um número restrito de licenças, o Afonso configura-as para requererem aprovação.|Os utilizadores agora podem utilizar o catálogo de aplicações para procurar as aplicações que está autorizados a instalar. Os utilizadores podem então instalar as aplicações de imediato, ou solicitar a aprovação e regressar ao catálogo de aplicações para as instalarem após a aprovação do pedido pelo suporte técnico.|  
|O Artur cria um conector do Exchange Server no Configuration Manager para gerir os dispositivos móveis que liguem ao Exchange Server no local da empresa. Configura este conector com definições de segurança que incluem o requisito para definir uma palavra-passe segura e bloqueiam o dispositivo móvel após um período de inatividade.<br /><br /> Para a gestão adicional para dispositivos que executam o Windows Phone 8, Windows RT e iOS, o Artur obtém uma subscrição do Microsoft Intune. Em seguida, instala a função de sistema de sites de ponto de ligação de serviço. Esta solução de gestão de dispositivos móveis melhora o suporte de gestão da empresa para estes dispositivos. Isto inclui a disponibilização de aplicações para os utilizadores instalarem nestes dispositivos extensa gestão e definições. Além disso, as ligações de dispositivo móvel são protegidas por certificados PKI que são criados e implementados automaticamente pelo Intune.<br /><br /> Depois de configurar o ponto de ligação de serviço e de subscrição para utilização com o Configuration Manager, Afonso envia uma mensagem de correio eletrónico aos utilizadores que estes dispositivos móveis para cliquem numa ligação para iniciar o processo de inscrição.<br /><br /> Para os dispositivos móveis sejam inscritos pelo Microsoft Intune, Afonso utiliza definições de compatibilidade para configurar definições de segurança para estes dispositivos móveis. Estas definições incluem o requisito para definir uma palavra-passe segura e bloqueiam o dispositivo móvel após um período de inatividade.|Com estas duas soluções de gestão de dispositivos móveis, o departamento de informática pode fornecer informações para relatórios sobre os dispositivos móveis utilizados na rede empresarial e respetiva compatibilidade com as definições de segurança configuradas.<br /><br /> É explicado aos utilizadores como apagar remotamente os seus dispositivos móveis utilizando o catálogo de aplicações ou o Portal da empresa se os seus dispositivos móveis são perdido ou roubado. O suporte técnico recebe também instruções sobre como apagar remotamente os dispositivos móveis dos utilizadores, utilizando a consola do Configuration Manager.<br /><br /> Além disso, para os dispositivos móveis inscritos pelo Microsoft Intune, Afonso pode agora implementar aplicações móveis para os utilizadores instalar, recolher mais dados de inventário a partir destes dispositivos e melhor controlo da gestão destes dispositivos conseguindo aceder a definições adicionais.|  
|A Trey Research tem vários computadores de quiosque que são utilizados pelos funcionários que visitam o escritório. Os funcionários querem que as suas aplicações estejam disponíveis sempre que iniciarem sessão. No entanto, Afonso não pretende instalar localmente todas as aplicações em cada computador.<br /><br /> Para atingir esse objetivo, o Afonso cria as aplicações necessárias, que têm dois tipos de implementação:<br /><br /> **O primeiro:** Uma instalação local, completa das aplicações que tenham o requisito de que só pode ser instalada no dispositivo primário do utilizador.<br /><br /> **O segundo:** Uma versão virtual da aplicação que tenha o requisito de que não poderem ser instaladas no dispositivo primário do utilizador.|Quando visita funcionários início de sessão para um computador de quiosque, verão as aplicações que necessitam, apresentadas como ícones no ambiente de trabalho do computador de quiosque. Quando executam a aplicação, ela é transmitida em sequência como uma aplicação virtual. Desta forma, podem ser tão produtivos como se estes estiverem sentada ao respetivo ambiente de trabalho.|  
|Permite ADAM utilizadores saber que pode configurar o respetivo horário de expediente no Centro de Software e pode selecionar opções que impedem as atividades de implementação de software durante esse período e quando o computador está no modo de apresentação.|Uma vez que os utilizadores podem controlar quando o Configuration Manager implementa software nos seus computadores, mantêm-se mais produtivos dia de trabalho.|  

 Estes passos e resultados de configuração permitem que a Trey Research capacite os seus funcionários, garantindo o acesso às aplicações a partir de qualquer dispositivo.  

###  <a name="BKMK_ScenarioUnify"></a>Cenário de exemplo: Unificar a gestão de conformidade dos dispositivos  
 A Trey Research procura uma solução unificada de gestão dos clientes que garanta que os seus computadores executam software antivírus que seja automaticamente mantido atualizado. Ou seja:  

-   Firewall do Windows está ativada.  
-   Atualizações de software críticas são instaladas.  
-   Chaves de registo específicas estão definidas.  
-   Dispositivos móveis geridos não conseguem instalar nem executar aplicações não assinadas.  

A empresa pretende também alargar esta proteção à Internet, para computadores portáteis que passem da intranet para a Internet.  

O Afonso mapeia estes requisitos da empresa para os seguintes cenários:  

|Requisito|Estado da atual gestão do cliente|Estado da gestão futura do cliente|  
|-----------------|-------------------------------------|------------------------------------|  
|Todos os computadores executam software antimalware com ficheiros de definições atualizados e que autoriza a Firewall do Windows.|Computadores diferentes executam soluções antimalware diferentes que não são sempre mantidas atualizadas. Embora a Firewall do Windows está ativada por predefinição, os utilizadores, por vezes, desativá-lo.<br /><br /> É pedido aos utilizadores que contactem o suporte técnico se for detetado malware nos seus computadores.|Todos os computadores executam a mesma solução antimalware, que transfere automaticamente os ficheiros de atualização de definições mais recentes e volta a ativar automaticamente a Firewall do Windows se os utilizadores a desativarem.<br /><br /> Se for detetado malware, o suporte técnico será automaticamente notificado por correio eletrónico.|  
|Todos os computadores instalam as atualizações de software críticas no prazo de um mês a contar do seu lançamento.|Embora as atualizações de software sejam instaladas nos computadores, muitos não instalam automaticamente as atualizações de software críticas senão dois ou três meses após o estão a ser lançadas. Isso deixa-os vulneráveis a ataques durante esse período.<br /><br /> Para os computadores que não instalem as atualizações de software críticas, o suporte técnico começa por enviar mensagens de correio eletrónico solicitar que os utilizadores instalam as atualizações. Se os computadores se mantiverem não compatíveis, os engenheiros ligam-se remotamente aos computadores e instalam manualmente as atualizações de software em falta.|A taxa de conformidade atual no mês especificado é melhorada para mais de 95% sem enviar mensagens de correio eletrónico nem solicitar que o suporte técnico para instalar manualmente.|  
|Definições de segurança de aplicações específicas são regularmente dada e remediadas, se necessário.|Os computadores executam scripts de arranque complexos que se baseiam na respetiva associação a grupos para repor os valores do registo de aplicações específicas.<br /><br /> Como estes scripts só são executados no arranque e alguns computadores ficam durante dias, o suporte técnico não consegue verificar para configuração ligados atempada.|Os valores do registo são verificados e automaticamente remediados, sem depender da associação do computador a grupos e sem o reiniciar.|  
|Dispositivos móveis não conseguem instalar nem executar aplicações não seguras.|É pedido aos utilizadores não transfiram nem executem aplicações potencialmente perigosas da Internet. No entanto, existem sem controlos monitorizar e impor tais pedidos.|Os dispositivos móveis que são geridos automaticamente com o Microsoft Intune ou o Configuration Manager impedem a instalação e execução de aplicações não assinadas.|  
|É necessário proteger os computadores portáteis que passam da intranet para a Internet.|Para os utilizadores que viajam, frequentemente não conseguem ligar através da ligação VPN diariamente. Estes portáteis deixam de estar em conformidade com os requisitos de segurança.|Uma ligação à Internet é tudo o que é necessário para manter a compatibilidade dos computadores portáteis com os requisitos de segurança. Os utilizadores não têm sessão ou utilizar a ligação VPN.|  

 Para cumprir os requisitos, Afonso utiliza estas capacidades de gestão do Configuration Manager e as opções de configuração:  

-   Endpoint Protection  
-   Atualizações de software  
-   Definições de compatibilidade  
-   Gestão de dispositivos móveis  
-   Gestão de clientes baseada na Internet  

Implementa-as utilizando os passos de configuração na tabela seguinte:  

|Passos de configuração|Resultado|  
|-------------------------|-------------|  
|O Artur configura o Endpoint Protection. Ele permite o definição de cliente para desinstalar outras soluções antimalware e ativa a Firewall do Windows. Configura regras de implementação automática para que os computadores procurem e instalem regularmente as atualizações de definições mais recentes.|A solução antimalware única ajuda a proteger todos os computadores, minimizando a sobrecarga administrativa. Uma vez que o suporte técnico é automaticamente notificado por mensagem de correio eletrónico se for detetado malware, os problemas podem ser resolvidos rapidamente. Isto ajuda a impedir ataques a outros computadores.|  
|Para ajudar a melhorar as taxas de conformidade, Afonso utiliza regras de implementação automática, define as janelas de manutenção dos servidores e investiga as vantagens e desvantagens da utilização de reativação por LAN em computadores que hibernem.|A compatibilidade com as atualizações de software críticas aumenta, reduzindo os requisitos de instalação manual de atualizações de software pelos utilizadores ou pelo suporte técnico.|  
|O Afonso utiliza definições de compatibilidade para verificar a presença das aplicações especificadas. Quando as aplicações são detetadas, itens de configuração, em seguida, verificam os valores de registo e remedeiam-nos automaticamente se estes estiverem em conformidade.|Ao utilizar itens de configuração e linhas de base de configuração que são implementadas em todos os computadores e verificação de compatibilidade todos os dias, que já não necessita de scripts separados que se baseiam na associação de computador reinícios de computador.|  
|O Afonso utiliza as definições de compatibilidade para dispositivos móveis inscritos, configurando o conector do Exchange Server de modo a proibir a instalação e execução de aplicações não assinadas em dispositivos móveis.|Porque estão proibidas de aplicações não assinadas, dispositivos móveis estão automaticamente protegidos a partir de aplicações potencialmente nocivos.|  
|Afonso certifica-se de que os computadores e servidores do sistema de sites possuem os certificados PKI exigidos pelo Configuration Manager para ligações HTTPS. Em seguida, instala funções do sistema de sites adicionais na rede de perímetro que aceitam ligações de cliente a partir da Internet.|Os computadores que passam da intranet para a Internet continuam automaticamente a ser geridos pelo Configuration Manager quando têm uma ligação à Internet. Esses computadores não dependem dos utilizadores a iniciar sessão no computador ou ligar para a ligação VPN.<br /><br /> Estes computadores continuam a ser geridos no que respeita a antimalware e à Firewall do Windows, atualizações de software e itens de configuração. Em resultado, os níveis de compatibilidade aumentam automaticamente.|  

 Estes passos e resultados de configuração permitem à Trey Research unificar com sucesso a gestão de compatibilidade dos dispositivos.  

###  <a name="BKMK_ScenarioSimplify"></a>Cenário de exemplo: Simplificar a gestão de cliente para dispositivos  
 Trey Research quer instalar automaticamente a imagem de base de computador da empresa, que executa o Windows 7 todos os computadores novos. Após a instalação da imagem do sistema operativo nestes computadores, tem de ser geridos e monitorizar o software adicional instalado pelos utilizadores. Os computadores que armazenam informações altamente confidenciais requerem políticas de gestão mais restritivas do que os restantes. Por exemplo, os engenheiros do suporte técnico não devem ligar remotamente a tais computadores, é exigida a introdução do PIN do BitLocker ao reiniciar e apenas os administradores locais podem instalar software.  

 O Afonso mapeia estes requisitos da empresa para os seguintes cenários:  

|Requisito|Estado da atual gestão do cliente|Estado da gestão futura do cliente|  
|-----------------|-------------------------------------|------------------------------------|  
|O Windows 7 é instalado nos novos computadores.|O suporte técnico instala e configura o Windows 7 para os utilizadores e, em seguida, envia o computador para a respetiva localização.|Novos computadores ir diretamente para o destino final, são ligados à rede e automaticamente instalarem e configurar o Windows 7.|  
|Os computadores têm de ser geridos e monitorizados. Isto inclui a recolha de dados de inventário de hardware e software para ajudar a determinar os requisitos de licenciamento.|O cliente do Configuration Manager é implementado utilizando a instalação push automática do cliente. O suporte técnico investiga as falhas de instalação e os clientes que não enviam dados de inventário quando é esperado.<br /><br /> As falhas são frequentes devido a dependências de instalação que não são satisfeitas e à corrupção de WMI no cliente.|Os dados de instalação e inventário do cliente recolhidos dos computadores são mais fiáveis e requerem uma menor intervenção do suporte técnico. Os relatórios mostram a utilização do software para obter informações de licenciamento.|  
|Alguns computadores precisam de políticas de gestão mais rigorosas.|Devido às políticas de gestão mais rigorosas, estes computadores atualmente não são geridos pelo Configuration Manager.|Estes computadores são geridos através do Configuration Manager para acomodar as exceções de sem a sobrecarga administrativa.|  

 Para cumprir os requisitos, Afonso utiliza estas capacidades de gestão do Configuration Manager e as opções de configuração:  

-   Implementação do sistema operativo  
-   Implementação e estado do cliente  
-   Definições de compatibilidade  
-   Definições do cliente  
-   Métodos de inventário e Asset Intelligence  
-   Administração baseada em funções  

Implementa-as utilizando os passos de configuração na tabela seguinte:  

|Passos de configuração|Resultado|  
|-------------------------|-------------|  
|O Artur captura uma imagem do sistema operativo a partir de um computador com Windows 7 instalado e está configurado para as especificações da empresa. Em seguida, implementa o sistema operativo em novos computadores utilizando o suporte para computadores desconhecidos e o PXE. Instala também o cliente do Configuration Manager como parte da implementação do sistema operativo.|Os novos computadores estão ativos e a funcionar mais rapidamente e sem a intervenção do suporte técnico.|  
|O Artur configura a instalação de push automática do cliente em todo o site para instalar o cliente do Configuration Manager em todos os computadores que são detetados. Isto garante que todos os computadores que não foram instalados com o cliente instalem o cliente para que o computador seja gerido pelo Configuration Manager.<br /><br /> O Artur configura o estado do cliente para retificar automaticamente quaisquer problemas detetados no mesmo. Artur também configura as definições de cliente que permitem a recolha de dados de inventário necessária e o Asset Intelligence.|Instalação do cliente juntamente com o sistema operativo é mais rápido e mais fiável do que à espera do Configuration Manager para detetar o computador e, em seguida, tentar instalar os ficheiros de origem do cliente no computador. No entanto, deixando a instalação push automática do cliente opção ativada, fornece um método de cópia de segurança para um computador que já tenha o sistema operativo instalado para instalar o cliente quando estabelecer ligação à rede.<br /><br /> As definições do cliente garantem que os clientes enviem regularmente as suas informações de inventário para o site. Esta situação, para além dos testes de estado de cliente, ajuda a manter o cliente em execução com intervenções mínimas por parte do suporte técnico. Por exemplo, os danos no WMI são detetados e retificados automaticamente.<br /><br /> Os relatórios do Asset Intelligence ajudam a monitorizar a utilização do software e as licenças.|  
|O Artur cria uma coleção para os computadores que devem possuir definições de política mais rigorosas. Em seguida, ele cria uma definição de dispositivo de cliente personalizadas para esta coleção que desativa o controlo remoto, que permite o PIN do BitLocker e esta definição permite aos administradores locais apenas instalar o software.<br /><br /> O Artur configura a administração baseada em funções para que os engenheiros do suporte técnico não vejam esta coleção de computadores. Isto ajuda a garantir que estes computadores não são geridos acidentalmente como computadores padrão.|Estes computadores são agora geridos pelo Configuration Manager, mas com definições específicas que não necessitam de um novo site.<br /><br /> A coleção destes computadores não está visível aos engenheiros do suporte técnico. Isto ajuda a reduzir a possibilidade dos computadores que está a ser envio acidental de implementações e scripts de computadores padrão.|  

 Estes passos e resultados de configuração permitem à Trey Research simplificar com sucesso a gestão de clientes dos dispositivos.  

##  <a name="BKMK_NextSteps"></a> Passos seguintes  
 Antes de instalar o Configuration Manager, familiarize-se com alguns conceitos e termos básicos que são específicos do Configuration Manager.  

-   Se estiver familiarizado com o System Center 2012 Configuration Manager, consulte o artigo [itens que são alterados no System Center Configuration Manager, a partir do System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) para compreender as novas funcionalidades.  
-   Para obter uma descrição de técnica alto nível do System Center Configuration Manager, consulte o artigo [Noções básicas do System Center Configuration Manager](../../core/understand/fundamentals.md).  

Quando estiver familiarizado com os conceitos básicos, utilize a documentação do System Center Configuration Manager para o ajudar a implementar e utilizar o Configuration Manager com êxito.  


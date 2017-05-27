---
title: "Site de administração de segurança e privacidade | Documentos do Microsoft"
description: "Otimize a segurança e privacidade para administração de sites no System Center Configuration Manager."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: a60b8c103a303dcae0bd66f3060d5a8f17d1cef9
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="security-and-privacy-for-site-administration-in-system-center-configuration-manager"></a>Segurança e privacidade para a administração de sites no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém segurança e informações de privacidade para sites do Configuration Manager do System Center e a hierarquia.

##  <a name="BKMK_Security_Sites"></a>Melhores práticas de segurança para a administração de sites  
 Utilize os seguintes procedimentos recomendados de segurança para o ajudar a segurança de sites do Configuration Manager do System Center e a hierarquia.  

 **Execute o programa de configuração apenas a partir de uma origem fidedigna e Proteja o canal de comunicação entre o suporte de dados de configuração e o servidor do site.**  

 Para ajudar a impedir que alguém adultere os ficheiros de origem, execute a configuração de uma origem fidedigna. Se armazenar os ficheiros na rede, proteja a localização de rede.  

 Se executar a configuração a partir de uma localização de rede, para ajudar a impedir que um atacante adultere os ficheiros à medida que são transmitidos através da rede, utilize a assinatura IPsec ou Server Message Block (SMB) entre a localização de origem dos ficheiros de configuração e o servidor do site.  

 Além disso, se utilizar a transferência da configuração para transferir os ficheiros que sejam exigidos pelo programa de configuração, certifique-se de que também protege a localização onde estes ficheiros são armazenados e Proteja o canal de comunicação para esta localização quando executar a configuração.  

 **Expandir o esquema do Active Directory para o System Center Configuration Manager e publique os sites Active Directory Domain Services.**  

 Não são necessárias extensões de esquema para executar o System Center Configuration Manager, mas criam um ambiente mais seguro porque os clientes do Configuration Manager e servidores de sites podem obter informações a partir de uma origem fidedigna.  

 Se os clientes estão num domínio não fidedigno, implemente as seguintes funções de sistema de sites nos domínios dos clientes:  

-   Ponto de gestão  

-   Ponto de distribuição  

-   Ponto de site do Catálogo de Aplicações  

> [!NOTE]  
>  Num domínio fidedigno para o Configuration Manager requer autenticação Kerberos. Isto significa que se os clientes estiverem noutra floresta que não possui uma fidedignidade de floresta bidirecional com a floresta do servidor de site, estes clientes são considerados como num domínio não fidedigno. Uma confiança externa não é suficiente para este efeito.  

 **Utilize IPsec para proteger as comunicações entre os sites e os servidores do sistema de sites.**  

 Apesar do Configuration Manager protegem a comunicação entre o servidor do site e o computador que executa o SQL Server, o Configuration Manager não proteger as comunicações entre funções de sistema de sites e o SQL Server. Só alguns sistemas de sites (o ponto de registo e o ponto de serviço Web do catálogo de aplicações) podem ser configurados com HTTPS para comunicações intra-site.  

 Se não utilizar controlos adicionais para proteger estes canais servidor-servidor, os atacantes poderão utilizar vários ataques man-in-the-middle e de spoofing contra sistemas de sites. Utilize a assinatura SMB quando não for possível utilizar IPsec.  

> [!NOTE]  
>  É especialmente importante proteger o canal de comunicação entre o servidor do site e o servidor de origem do pacote. Esta comunicação utiliza SMB. Se não for possível utilizar IPsec para proteger estas comunicações, utilize a assinatura SMB para assegurar que os ficheiros não são adulterados antes de os clientes os transferirem e executarem.  

 **Não altere os grupos de segurança do Configuration Manager cria e gere para as comunicações do sistema de sites.**  

 Grupos de segurança:  

-   **SMS_SiteSystemToSiteServerConnection_MP_&lt;SiteCode\>**  

-   **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;SiteCode\>**  

-   **SMS_SiteSystemToSiteServerConnection_Stat_&lt;SiteCode\>**  

O Configuration Manager cria e gere destes grupos de segurança automaticamente. Isto inclui a remoção de contas de computador quando uma função de sistema de sites é removida.  

Para assegurar a continuidade de serviço e o mínimo de privilégios, não edite manualmente estes grupos.  

**Se os clientes não conseguirem consultar o servidor de Catálogo Global para informações do Configuration Manager, gerir a processo de aprovisionamento de chave de raiz fidedigna.**  

Se os clientes não conseguirem consultar informações do Configuration Manager no Catálogo Global, terão de depender da chave de raiz fidedigna para autenticar pontos de gestão válidos. A chave de raiz fidedigna é armazenada no registo do cliente e pode ser definida utilizando a Política de Grupo ou configuração manual.  

Se o cliente não tiver uma cópia da chave de raiz fidedigna antes de contactar um ponto de gestão pela primeira vez, confiará no primeiro ponto de gestão com que comunicar. Para reduzir o risco de um atacante direcionar os clientes para um ponto de gestão não autorizado, pode aprovisionar previamente os clientes com a chave de raiz fidedigna. Para obter mais informações, consulte o artigo [planear a chave de raiz fidedigna](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

**Utilize números de porta não predefinidos.**  

Utilizar números de porta não predefinidos pode proporcionar segurança adicional porque tornar mais difícil aos atacantes a exploração do ambiente preparar um ataque. Se optar por utilizar não predefinidos, planeie-os antes de instalar o Configuration Manager e utilizá-los de forma consistente em todos os sites na hierarquia. As portas de pedido do cliente e Wake On LAN são exemplos onde pode utilizar números de porta não predefinidos.  

**Utilize separação de funções nos sistemas de sites.**  

Apesar de poder instalar todos as funções de sistema de sites num único computador, esta prática raramente é utilizada em redes de produção porque cria um ponto de falha único.  

**Reduza o perfil de ataque.**  

Isolando cada função do sistema de sites num servidor diferente reduz a possibilidade de um ataque contra as vulnerabilidades de um sistema de sites pode ser utilizado contra outro sistema de sites. Muitas funções de sistema de sites requerem a instalação dos serviços de informação Internet (IIS) no sistema de sites e Isto aumenta a superfície de ataque. Se tiver de combinar funções de sistema de sites para reduzir as despesas com hardware, combine funções de sistema de sites do IIS apenas com outras funções de sistema de sites que necessitem do IIS.  

> [!IMPORTANT]  
>  A função de ponto de estado de contingência é uma exceção. Como esta função do sistema de sites aceita dados não autenticados de clientes, recomendamos que alguma vez não atribuir a função de ponto de estado de contingência para outras do Configuration Manager site funções do sistema.  


**Siga as melhores práticas de segurança do Windows Server e execute o Assistente de Configuração de Segurança em todos os sistemas de sites.**  

O Assistente de Configuração de Segurança (SCW) ajuda a criar uma política de segurança que pode aplicar a qualquer servidor da rede. Depois de instalar o modelo do System Center Configuration Manager, o SCW reconhece funções de sistema de sites do Configuration Manager, serviços, portas e aplicações. Depois, permite a comunicação de que é necessário para o Configuration Manager e bloqueia as comunicações que não são necessárias.  

O Assistente de configuração de segurança está incluído com o toolkit do System Center 2012 Configuration Manager, que pode transferir a partir de Center Download Microsoft: [System Center 2012-Configuration Manager Component add-ons e extensões](http://go.microsoft.com/fwlink/p/?LinkId=251931).  

**Configure endereços IP estáticos para os sistemas de sites.**  

Os endereços IP estáticos são mais fáceis de proteger contra ataques de resolução de nomes.  

Endereços IP estáticos também facilitam a configuração do IPsec. Utilizar IPsec é a melhor prática de segurança para proteger a comunicação entre sistemas de sites no Configuration Manager.  

**Não instale outras aplicações em servidores de sistemas de sites.**  

Quando instala outras aplicações em servidores de sistema de sites, aumenta a superfície de ataque do Configuration Manager e problemas de incompatibilidade de risco.  

**Exija assinatura e ative a encriptação como uma opção de site.**  

Ative as opções de assinatura e encriptação para o site. Certifique-se de que todos os clientes suportam o algoritmo hash SHA-256 e, em seguida, ative a opção **exigir SHA-256**.  

**Restringir e monitorizar os utilizadores administrativos do Configuration Manager e utilizar a administração baseada em funções para conceder a estes utilizadores as permissões mínimas de que necessitam.**  

Conceda acesso administrativo para o Configuration Manager apenas aos utilizadores em quem confie e conceda-lhes permissões mínimas utilizando as funções de segurança incorporadas ou personalizando as funções de segurança. Os utilizadores administrativos que podem criar, modificar e implementar aplicações, sequência de tarefas, atualizações de software, itens de configuração e linhas de base de configuração, podem eventualmente, controlar dispositivos na hierarquia do Configuration Manager.  

Realize auditorias periódicas às atribuições dos utilizadores administrativos e ao respetivo nível de autorização para verificar as alterações necessárias.  

Para mais informações sobre a configuração da administração baseada em funções, veja [Configurar a Administração Baseada em Funções do System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md).  

**Proteja as cópias de segurança do Configuration Manager e o canal de comunicação quando a cópia de segurança e restauros.**  

Quando efetua uma segurança o Gestor de configuração, estas informações incluem certificados e outros dados confidenciais que podem ser utilizados por um atacante para representação.  

Utilize a assinatura SMB ou IPsec quando transferir estes dados através da rede e proteja a localização das cópias de segurança.  

**Sempre que exporta ou importar objetos a partir da consola do Configuration Manager para uma localização de rede, proteja a localização e Proteja o canal de rede.**  

Limite quem pode aceder à pasta de rede.  

Utilize a assinatura SMB ou IPsec entre a localização de rede e o servidor do site e entre o computador que executa o Gestor de configuração do servidor de consola e o site, para impedir que um atacante adultere os dados exportados. Utilize IPsec para encriptar os dados na rede para evitar a divulgação de informações.  

**Se um sistema de sites não está corretamente desinstalado ou deixa de funcionar e não pode ser restaurado, remova manualmente os certificados do Configuration Manager para este servidor a partir de outros servidores do Configuration Manager.**  

Para remover a PeerTrust originalmente estabelecida com o sistema de sites e funções do sistema de sites, remova manualmente os certificados do Configuration Manager para o servidor que falhou o **pessoas fidedignas** arquivo de certificados noutros servidores do sistema de sites. Isto é especialmente importante se reutilizar o servidor sem o formatar.  

Para obter mais informações sobre estes certificados, consulte a secção **controlos criptográficos para comunicações de servidor** no [Cryptographic controla referência técnica para o System Center Configuration Manager](../../../protect/deploy-use/cryptographic-controls-technical-reference.md).  

**Não configure sistemas de sites baseados na Internet para funcionar como bridge entre a rede de perímetro e a intranet.**  

Não configure servidores de sistema de sites como multihomed para que se ligar à rede de perímetro e à intranet. Embora esta configuração permita que sistemas de sites baseados na Internet aceitem ligações de clientes da Internet e da intranet, elimina um limite de segurança entre a rede de perímetro e a intranet.  

**Se o servidor de sistema de sites estiver numa rede não fidedigna (como uma rede de perímetro), configure o servidor de site para iniciar as ligações ao sistema de sites.**  

Por predefinição, os sistemas de sites iniciam as ligações ao servidor de site para a transferência de dados, o que pode constituir um risco de segurança quando a ligação for iniciada a partir de uma rede não fidedigna para a rede fidedigna. Quando os sistemas de sites aceitarem ligações da Internet ou residirem numa floresta não fidedigna, configure a opção de sistema de sites **Exigir que o servidor do site inicie ligações a este sistema de sites** para que, depois da instalação do sistema de sites e de quaisquer funções de sistema de sites, todas as ligações sejam iniciadas a partir da rede fidedigna.  

**Se utilizar um servidor proxy Web para a gestão de clientes baseados na Internet, utilize o protocolo de bridge SSL para SSL utilizando terminação com autenticação.**  

 Quando configura a terminação de SSL no servidor Web proxy, os pacotes da Internet são sujeitos a inspeção antes de serem reencaminhados para a rede interna. O servidor Web proxy autentica a ligação do cliente, termina-a e, em seguida, abre uma nova ligação autenticada para os sistemas de sites baseados na Internet.  

 Quando os computadores de cliente do Configuration Manager utilizam um servidor web proxy para estabelecer ligação com sistemas de sites baseados na Internet, a identidade do cliente (GUID do cliente) está contida em segurança no payload do pacote para que o ponto de gestão não considere o servidor web proxy como o cliente. Se o servidor Web proxy não suportar os requisitos do o protocolo de bridge SSL, a utilização de túnel SSL também é suportada. Esta é uma opção menos segura porque os pacotes SSL da Internet são reencaminhados para os sistemas de sites sem terminação, pelo que não é possível inspecioná-los relativamente a conteúdo malicioso.  

 Se o servidor Web proxy não suportar os requisitos do o protocolo de bridge SSL, pode utilizar o túnel SSL. No entanto, esta é uma opção menos segura porque os pacotes SSL da Internet são reencaminhados para os sistemas de sites sem terminação, pelo que não é possível inspecioná-los relativamente a conteúdo malicioso.  

> [!WARNING]  
>  Dispositivos móveis que são inscritos pelo Configuration Manager não é possível utilizar o protocolo de bridge SSL e têm de utilizar apenas o túnel SSL.  

**Configurações de utilização no caso de configurar o site para reativar computadores para instalação de software:**  

-   Se utilizar pacotes de reativação tradicionais, utilize unicast em vez de difusões direcionadas para a sub-rede.  

-   Se tiver de utilizar difusões direcionadas para sub-redes, configure os routers para permitirem difusões direcionadas para IP apenas a partir do servidor do site e apenas num número de porta não predefinidos.  

Para mais informações sobre as diferentes tecnologias de reativação por LAN, consulte o artigo [planear como reativar clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).

**Se utilizar notificações por correio eletrónico, configure o acesso autenticado ao servidor de correio SMTP.**  

Sempre que possível, utilize um servidor de correio que suporte acesso autenticado e utilize a conta de computador do servidor do site para autenticação. Se tiver de especificar uma conta de utilizador para autenticação, utilize uma conta que tenha privilégios mínimos.  

##  <a name="BKMK_Security_SiteServer"></a>Melhores práticas de segurança para o servidor do site  
 Utilize os seguintes procedimentos recomendados de segurança para ajudar a proteger o Gestor de configuração do servidor do site.  

 **Instale o Configuration Manager num servidor membro e não num controlador de domínio.**  

 Os sistemas de site e o servidor de sites do Configuration Manager não necessitam de instalação num controlador de domínio. Os controladores de domínio não têm uma base de dados SAM (Security Accounts Management) local além da base de dados do domínio. Quando instalar o Configuration Manager num servidor membro, pode manter as contas do Configuration Manager na base de dados SAM local, em vez de na base de dados do domínio.  

 Esta prática também reduz a superfície de ataque nos controladores de domínio.  

 **Instale sites secundários evitando copiar os ficheiros para o servidor do site secundário através da rede.**  

 Quando executar a configuração e criar um site secundário, não selecione a opção para copiar os ficheiros do site principal para o site secundário e não utilize uma localização de origem de rede. Quando copia ficheiros através da rede, um atacante hábil pode apoderar-se do pacote de instalação do site secundário e adulterar os ficheiros antes da sua instalação, apesar de a coordenação de um ataque destes ser difícil. Este ataque pode ser atenuado utilizando IPsec ou SMB quando transferir os ficheiros.  

 Em vez de copiar os ficheiros através da rede, no servidor do site secundário, copie os ficheiros de origem a partir da pasta de suporte de dados para uma pasta local. Em seguida, quando executar a configuração para criar um site secundário, o **ficheiros de origem de instalação** página, selecione **utilizar os ficheiros de origem disponíveis na seguinte localização no computador do site secundário (mais seguro)**, e especifique esta pasta.  

 Para obter mais informações, veja [Instalar um site secundário](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary) no tópico [Utilizar o Assistente de Configuração para instalar sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  

##  <a name="BKMK_Security_SQLServer"></a>Melhores práticas de segurança para o SQL Server  
 O Configuration Manager utiliza o SQL Server como a base de dados back-end. Se a base de dados for comprometida, os atacantes podem ignorar do Configuration Manager e aceder ao SQL Server diretamente para iniciar ataques através do Configuration Manager. Considere os ataques contra o SQL Server um risco muito elevado e mitigar adequadamente.  

 Utilize os seguintes procedimentos recomendados de segurança para o ajudar a proteger o SQL Server para o Configuration Manager.  

 **Não utilize o servidor de base de dados do site do Configuration Manager para executar outras aplicações do SQL Server.**  

 Quando aumenta o acesso ao servidor de base de dados do site do Configuration Manager, isto aumenta o risco aos dados do Configuration Manager. Se a base de dados do site do Configuration Manager for comprometida, outras aplicações no mesmo computador do SQL Server, em seguida, são também colocar em risco.  

 **Configure o SQL Server para utilizar a autenticação do Windows.**  

 Apesar do Configuration Manager acede a base de dados do site utilizando uma conta do Windows e autenticação do Windows, é possível configurar o SQL Server para utilizar o modo misto do SQL Server. O modo misto do SQL Server permite adicionais SQL inícios de sessão aceder à base de dados, o que não é necessários e aumenta a superfície de ataque.  

 **Efetue passos adicionais para garantir que os sites secundários que utilizam o SQL Server Express têm as atualizações de software mais recentes.**  

 Quando instala um site primário, o Configuration Manager transfere o SQL Server Express a partir do Center Download Microsoft e copia os ficheiros para o servidor de site primário. Quando instala um site secundário e seleciona a opção que instala o SQL Server Express, o Configuration Manager instala a versão transferida anteriormente e não verifica se existem novas versões. Para garantir que o site secundário tem as versões mais recentes, efetue uma das seguintes tarefas:  

-   Depois do site secundário foi instalado, execute o Windows Update no servidor do site secundário.  

-   Antes de instalar o site secundário, instale manualmente o SQL Server Express no computador que irá executar o servidor do site secundário e certifique-se de que instala a versão mais recente e as atualizações de software existentes. Em seguida, instalar o site secundário e selecione a opção para utilizar uma instância existente do SQL Server.  

Execute periodicamente o Windows Update nestes sites e todas as versões instaladas do SQL Server para garantir que têm as atualizações de software mais recentes.  

**Siga as melhores práticas para o SQL Server.**  

Identifique e siga as melhores práticas para a sua versão do SQL Server. No entanto, tenha em consideração os seguintes requisitos para o Configuration Manager:  

-   A conta de computador do servidor do site tem de ser membro do grupo Administradores no computador que executa o SQL Server. Se seguir a recomendação do SQL Server "aprovisionar principais de administrador explicitamente", a conta que utiliza para executar a configuração no servidor do site tem de ser um membro do grupo de utilizadores do SQL Server.  

-   Se instalar o SQL Server utilizando uma conta de utilizador de domínio, certifique-se de que a conta de computador do servidor do site é configurada para um Nome do Principal do Serviço (SPN) publicado nos Serviços de Domínio do Active Directory. Sem o SPN, a autenticação Kerberos falhar e a configuração do Configuration Manager falha.  

##  <a name="BKMK_Security_IIS"></a>Melhores práticas de segurança para sistemas de sites que executam o IIS  
Várias funções de sistema de sites no Configuration Manager necessitam do IIS. O processo de proteger IIS ativa do Configuration Manager funcione corretamente e reduz o risco de ataques de segurança. Quando práticos, estará a minimizar o número de servidores que necessitam do IIS. Por exemplo, execute apenas o número de pontos de gestão necessário para suportar a base de clientes, tendo em conta a disponibilidade elevada e o isolamento de rede da gestão de clientes baseados na Internet.  

 Utilize as melhores práticas de segurança seguintes para ajudar a proteger os sistemas de sites que executam o IIS.  

 **Desative as funções do IIS que não seja necessário.**  

 Instale apenas as funcionalidades mínimas do IIS para a função de sistema de sites que instalar. Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Configure as funções de sistema de sites para exigirem HTTPS.**  

 Quando os clientes ligam a um sistema de sites utilizando HTTP em vez de HTTPS, utilizam a autenticação do Windows e poderão, em caso de contingência, utilizar a autenticação NTLM em vez da autenticação Kerberos. Quando é utilizada a autenticação NTLM, os clientes podem ligar a um servidor não autorizado.  

 A exceção a esta melhor prática de segurança poderão ser os pontos de distribuição, uma vez que as contas de acesso a pacotes não funcionam quando o ponto de distribuição está configurado para HTTPS. As contas de acesso a pacotes fornecem autorização para o conteúdo, para que possa restringir os utilizadores que podem aceder ao conteúdo. Para obter mais informações, consulte o artigo [melhores práticas de segurança para gestão de conteúdo](../../../core/plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

**Configure uma lista fidedigna de certificados (CTL) no IIS para as funções de sistema de sites.**  

Funções do sistema de sites:  

-   Um ponto de distribuição que esteja configurado para HTTPS  

-   Um ponto de gestão que está configurado para HTTPS e ativado para suportar dispositivos móveis

Uma lista fidedigna de certificados (CTL) é uma lista definida de autoridades de certificação de raiz fidedigna. Quando utiliza uma CTL com a política de grupo e uma implementação de infraestrutura de chaves públicas (PKI), uma CTL permite-lhe complementar as autoridades de certificação de raiz fidedigna existentes configuradas na sua rede, como os que são automaticamente instaladas com o Microsoft Windows ou adicionadas através das autoridades de certificação do Windows enterprise raiz. No entanto, quando uma CTL é configurada no IIS, define um subconjunto dessas autoridades de certificação de raiz fidedigna.  

Este subconjunto proporciona maior controlo da segurança porque a CTL restringe os certificados de cliente que são aceites apenas aos que são emitidos pela lista de autoridades de certificação na CTL. Por exemplo, o Windows é fornecido com um número de certificados de autoridade de certificação bem conhecidas e de terceiros, como VeriSign e a Thawte.

Por predefinição, o computador que executa o IIS confia em certificados que encadeiem nestas autoridades de certificação conhecidas. Quando não configura o IIS com uma CTL para as funções do sistema de sites listadas, qualquer dispositivo que tenha um certificado de cliente emitido por estas autoridades de certificação é aceite como um cliente válido do Configuration Manager. Se configurar o IIS com uma CTL que não inclua estas autoridades de certificação, as ligações de cliente serão recusadas se o certificado encadear nestas autoridades de certificação. No entanto, para os clientes do Configuration Manager sejam aceites para as funções do sistema de sites listadas, tem de configurar IIS com uma CTL que especifique as autoridades de certificação que são utilizadas por clientes do Configuration Manager.  

> [!NOTE]  
>  Apenas as funções de sistema de sites listadas necessitam que configure uma CTL no IIS. A lista de emissores de certificados que o Configuration Manager utiliza para pontos de gestão fornece a mesma funcionalidade para computadores cliente quando estes ligam a pontos de gestão HTTPS.  

Para mais informações sobre como configurar uma lista de autoridades de certificação fidedignas no IIS, consulte a documentação do IIS.  

**Não coloque o servidor do site num computador com o IIS.**  

A separação de funções ajuda a reduzir o perfil de ataques e a melhorar a capacidade de recuperação. Além disso, a conta de computador do servidor do site tem normalmente privilégios administrativos em todas as funções de sistema de sites (e possivelmente nos clientes do Configuration Manager, se utilizar a instalação de push de cliente).  

**Utilize servidores de IIS dedicados para o Configuration Manager.**  

Embora possa alojar várias aplicações baseadas na web nos servidores de IIS que também sejam utilizados pelo Configuration Manager, esta prática pode aumentar significativamente a superfície de ataque. Uma aplicação mal configurada pode permitir a um atacante obter o controlo de um Gestor de configuração do sistema de sites, que poderia permitir um atacante obter o controlo da hierarquia.  

Se tiver de executar outras aplicações baseadas na web em sistemas de sites do Configuration Manager, crie um web site personalizado para sistemas de sites do Configuration Manager.  

**Utilize um Web site personalizado.**  

Para sistemas de sites que executam o IIS, pode configurar o Configuration Manager para utilizar um Web site personalizado em vez do Web site predefinido do IIS. Se tiver de executar outras aplicações web no sistema de sites, tem de utilizar um Web site personalizado. Esta definição é uma definição ao nível do site em vez de uma definição para um sistema de sites específicas.  

Além de fornecer segurança adicional, deve utilizar um Web site personalizado se executar outras aplicações Web no sistema de sites.  

**Se mudar do Web site predefinido para um Web site personalizado depois serem instaladas funções de ponto de distribuição, remova os diretórios virtuais predefinidos.**  

Quando alterar do Web site predefinido para um Web site personalizado, o Configuration Manager não remove os diretórios virtuais antigos. Remova os diretórios virtuais que originalmente criou o Configuration Manager no Web site predefinido.  

Por exemplo, os diretórios virtuais a remover de um ponto de distribuição são os seguintes:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**Siga as melhores práticas para o Servidor do IIS.**  

Identifique e siga as melhores práticas para a sua versão do Servidor do IIS. No entanto, tenha em consideração os requisitos que o Configuration Manager possui para funções de sistema de sites específicas. Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

##  <a name="BKMK_Security_ManagementPoint"></a>Melhores práticas de segurança para o ponto de gestão  
 Pontos de gestão são a interface primária entre dispositivos e o Configuration Manager. Considere os ataques contra o ponto de gestão e o servidor que executa no risco muito elevado e mitigar adequadamente. Aplique as melhores práticas de segurança adequadas e monitorize a ocorrência de atividade invulgar.  

 Utilize os seguintes procedimentos recomendados de segurança para ajudar a proteger um ponto de gestão no Configuration Manager.  

**Quando instala um cliente do Configuration Manager no ponto de gestão, atribua-o ao site desse ponto de gestão.**  

 Evite o cenário onde um cliente de Configuration Manager que se encontra num sistema de sites de ponto de gestão é atribuído a um site diferente do site do ponto de gestão.  

 Se efetuar a migração de uma versão anterior para o System Center Configuration Manager, migre o software de cliente no ponto de gestão para o System Center Configuration Manager logo que possível.  

##  <a name="BKMK_Security_FSP"></a>Melhores práticas de segurança para o ponto de estado de contingência  
 Utilize os seguintes procedimentos recomendados de segurança se instalar um ponto de estado de contingência no Configuration Manager.  

 Para mais informações sobre as considerações de segurança quando instala um ponto de estado de contingência, veja [Determinar se Necessita de um Ponto de Estado de Contingência](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md#determine-if-you-need-a-fallback-status-point).  


**Não execute outras funções de sistema de sites no sistema de sites e não instale o ponto de estado de contingência num controlador de domínio.**  

 Como o ponto de estado de contingência é concebido para aceitar comunicações não autenticadas de qualquer computador, a execução desta função de sistema de sites com outras funções de sistema de sites ou num controlador de domínio aumenta significativamente o risco desse servidor.  

**Quando utiliza certificados PKI para comunicações de clientes no Configuration Manager, instale o ponto de estado de contingência antes de instalar os clientes.**  

 Se os sistemas de sites do Configuration Manager não deve aceitar comunicações de cliente HTTP, poderá não saber que os clientes são geridos devido a problemas de certificados relacionados com PKI. No entanto, se os clientes são atribuídos a um ponto de estado de contingência, estes problemas de certificados são reportados pelo ponto de estado de contingência.  

 Por motivos de segurança, não é possível atribuir um ponto de estado de contingência a clientes após serem instalados. Em vez disso, pode atribuir esta função apenas durante a instalação do cliente.  

**Evite utilizar o ponto de estado de contingência na rede de perímetro.**  

 Por predefinição, o ponto de estado de contingência aceita dados a partir de qualquer cliente. Embora um ponto de estado de contingência na rede de perímetro possa ajudar a resolver problemas com clientes baseados na Internet, tem de equilibrar os benefícios da resolução de problemas com o risco de um sistema de sites aceitar dados não autenticados numa rede de acesso público.  

 Se instalar o ponto de estado de contingência na rede de perímetro ou em qualquer rede não fidedigna, configure o servidor de site para iniciar as transferências de dados em vez de utilizar a predefinição que permite que o ponto de estado de contingência inicie uma ligação ao servidor do site.  

##  <a name="BKMK_SecurityIssues_Clients"></a>Problemas de segurança de administração de sites  
 Reveja os seguintes problemas de segurança para o Configuration Manager:  

-   O Configuration Manager não possui nenhuma defesa contra um utilizador administrativo autorizado que utiliza o Configuration Manager para atacar a rede. Os utilizadores administrativos não autorizados constituem um risco de segurança elevado e, podem iniciar vários ataques, incluindo as seguintes estratégias:  

    -   Utilize a implementação de software para instalar e executar automaticamente software malicioso em todos os computadores de cliente do Configuration Manager na empresa.  

    -   Utilize o controlo remoto para assumir o controlo remoto de um cliente do Configuration Manager sem permissão do mesmo.  

    -   Configurar intervalos de consulta rápida e valores excessivos de inventário para criar ataques de recusa de serviço contra clientes e servidores.  

    -   Utilizar um site na hierarquia para escrever dados nos dados do Active Directory de outro site.  

    A hierarquia de sites é o limite de segurança. Considere sites serem apenas limites de gestão.  

    Audite todas as atividades do utilizador administrativo e reveja regularmente os registos de auditoria. Necessitam de todos os utilizadores administrativos do Configuration Manager para undergo uma verificação de fundo, antes de serem recrutados e exigem verificações periódicas como condição de emprego.  

-   Se o ponto de registo for comprometido, um intruso poderá obter certificados para autenticação e roubar as credenciais de utilizadores que inscrevem os respetivos dispositivos móveis.  

    O ponto de registo comunica com uma autoridade de certificação e pode criar, modificar e eliminar objetos do Active Directory. Nunca instale o ponto de inscrição na rede de perímetro e monitorize sempre de atividade invulgar.  

-   Se permitir políticas de utilizador para a gestão de clientes baseada na Internet ou configurar o ponto de serviço Web do Catálogo de Aplicações para utilizadores que estão na Internet, aumenta o seu perfil de ataque.  

    Para além de utilizar certificados PKI para ligações de cliente-servidor, estas configurações requerem a autenticação do Windows, podendo voltar a utilizar a autenticação NTLM em vez da autenticação Kerberos. A autenticação NTLM é vulnerável a ataques de representação e repetição. Para autenticar com sucesso um utilizador na Internet, tem de permitir a ligação do servidor do sistema de sites baseado na Internet a um controlador de domínio.  

-   A partilha Admin$ é obrigatória em servidores do sistema de sites.  

    O servidor do site do Configuration Manager utiliza a partilha Admin$ para estabelecer ligação ao e efetuar operações de serviço em sistemas de sites. Não desative nem remova a partilha Admin$.  

-   O Configuration Manager utiliza serviços de resolução de nome para ligar a outros computadores e estes serviços são difíceis de proteger contra ataques de segurança, como spoofing, adulteração, rejeição, divulgação de informações, recusa de serviço e elevação de privilégios.  

    Identifique e siga os procedimentos recomendados de segurança para a versão do DNS e WINS que utiliza para resolução de nomes.  

##  <a name="BKMK_Privacy_Cliients"></a>Informações de privacidade para deteção  
 A deteção cria registros para recursos de rede e armazena-os na base de dados do System Center Configuration Manager. Os registos de dados de deteção contêm informações sobre o computador como endereços IP, sistemas operativos e nomes de computador. Os métodos de deteção do Active Directory também podem ser configurados para detetar informações armazenadas nos Serviços de Domínio do Active Directory.  

 O único método de deteção que está ativado por predefinição é a deteção de Heartbeat, mas que método apenas Deteta os computadores que ainda têm o software de cliente do System Center Configuration Manager instalado.  

 As informações de deteção não são enviadas à Microsoft. Em vez disso, este é armazenado na base de dados do Configuration Manager. As informações são retidas na base de dados até serem eliminada pela tarefa de manutenção do site todos os 90 dias **eliminar dados de deteção desatualizados**.  

 Antes de configurar métodos de deteção adicionais ou expandir a deteção do Active Directory, considere os requisitos de privacidade.  


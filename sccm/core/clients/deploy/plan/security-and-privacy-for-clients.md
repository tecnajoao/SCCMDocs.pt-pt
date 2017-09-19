---
title: "Privacidade e segurança de cliente | Microsoft Docs"
description: "Saiba mais sobre segurança e privacidade para clientes no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
caps.latest.revision: "10"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: b354155d83ce6f3a14b13b98fb54e1f3bd2f54da
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/15/2017
---
# <a name="security-and-privacy-for-clients-in-system-center-configuration-manager"></a>Segurança e privacidade para clientes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo contém informações de privacidade para clientes no System Center Configuration Manager e para dispositivos móveis que são geridos pelo conector do Exchange Server e de segurança:  

##  <a name="BKMK_Security_Cliients"></a>Melhores práticas de segurança para clientes  
 Quando o Configuration Manager aceita dados de dispositivos que executam o cliente do Configuration Manager, ocorre o risco dos clientes poderem atacar o site. Por exemplo, poderiam enviar inventários incorretos ou tentar sobrecarregar os sistemas do site. Implemente o cliente do Configuration Manager apenas a dispositivos que considera fidedignos. Além disso, utilize os seguintes procedimentos recomendados para ajudar a proteger o site contra dispositivos não autorizados ou comprometidos:  

 **Utilize certificados de infraestrutura de chaves públicas (PKI) para comunicações de clientes com sistemas de sites que executam o IIS.**  

-   Como uma propriedade do site, configure **Definições do sistema de sites** para **Apenas HTTPS**.  

-   Instale os clientes com a propriedade **/UsePKICert** CCMSetup  

-   Utilize uma lista de revogação de certificados (CRL) e certifique-se de que os clientes e servidores em comunicação podem aceder-lhe sempre.  

 Estes certificados são necessários para as ligações à Internet dos clientes de dispositivos móveis e dos computadores cliente, e, à exceção dos pontos de distribuição, são recomendados para todas as ligações de cliente à intranet.  

 Para obter mais informações sobre os requisitos de certificados PKI e como são utilizados para ajudar a proteger o Configuration Manager, consulte [requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 **Aprovam automaticamente computadores cliente de domínios fidedignos e manualmente verificar e aprovar outros computadores**  

 Pode configurar a aprovação para a hierarquia como manual, automática para computadores em domínios fidedignos ou automática para todos os computadores. O método mais seguro de aprovação é aprovar automaticamente os clientes que são membros de domínios fidedignos e, em seguida, verificar manualmente e aprovar todos os outros computadores. Não é recomendável aprovar automaticamente todos os clientes, a menos que tenha outros controlos de acesso para impedir que computadores não fidedignos acedam à rede.  

 Aprovação identifica um computador que considere de confiança, para serem geridos pelo Configuration Manager quando não é possível utilizar a autenticação de PKI.  

 Para obter mais informações sobre como aprovar computadores manualmente, veja [Gerir Clientes a partir do Nó Dispositivos](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

 **Não pode confiar no bloqueio para impedir que os clientes acedam à hierarquia do Configuration Manager**  

 Os clientes bloqueados são rejeitados pela infraestrutura do Configuration Manager para que não conseguem comunicar com sistemas de sites para transferir políticas, carregar dados de inventário ou enviar mensagens de estado. No entanto, não pode confie no bloqueio para proteger a hierarquia do Configuration Manager de computadores não fidedignos quando os sistemas de sites aceitam ligações de cliente HTTP. Neste cenário, um cliente bloqueado poderia voltar a associar o site com um novo certificado autoassinado e um novo ID de hardware. O bloqueio foi concebido para ser utilizado no sentido de bloquear suportes de dados de arranque perdidos ou comprometidos ao implementar sistemas operativos nos clientes e quando todos os sistemas de sites aceitam ligações de cliente por HTTPS. Se utiliza uma infraestrutura de chaves públicas (PKI), e a mesma suportar uma lista de revogação de certificados (CRL), considere sempre a revogação de certificados como a primeira linha de defesa contra certificados potencialmente comprometidos. Bloqueio de clientes no Configuration Manager oferece uma segunda linha de defesa para proteger a hierarquia.  

 Para obter mais informações, veja [Determinar se deve bloquear clientes no System Center Configuration Manager](../../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

 **Utilize os métodos de instalação de cliente mais seguros e adequados ao seu ambiente:**  

-   Para computadores de domínio, os métodos de instalação de cliente de Política de Grupo e de instalação de cliente baseada em atualização de software são mais seguros do que a instalação push de cliente.  

-   O processamento de imagens e a instalação manual podem ser muito seguros, se aplicar controlos de acesso e alterar os controlos.  

 De todos os métodos de instalação de cliente, a instalação push de cliente é a menos segura devido à grande quantidade de dependências que possui, o que inclui permissões administrativas locais, a partilha Admin$ e muitas exceções de firewall. Estas dependências aumentam a superfície de ataque.  

 Para obter mais informações sobre os diferentes métodos de instalação do cliente, veja [Métodos de instalação de cliente no System Center Configuration Manager](../../../../core/clients/deploy/plan/client-installation-methods.md).  

 Além disso, sempre que possível, selecione um método de instalação de cliente necessita de, pelo menos, permissões de segurança no Configuration Manager e restrinja os utilizadores administrativos com atribuição de funções de segurança que incluam permissões que podem ser utilizadas para fins que não sejam de implementação do cliente. Por exemplo, a atualização automática de cliente requer a função de segurança **Administrador Total**, que concede a um utilizador administrativo todas as permissões de segurança.  

 Para obter mais informações sobre as dependências e permissões de segurança necessárias para cada método de instalação de cliente, consulte "Dependências de método de instalação" em [pré-requisitos para clientes de computador](../../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers).  

 **Se tiver de utilizar a instalação push do cliente, tome medidas adicionais para proteger a conta de instalação de Push de cliente**  

 Embora esta conta tem de ser um membro do local **administradores** grupo em cada computador que irá instalar o software de cliente do Configuration Manager, nunca adicione a conta de instalação de Push do cliente para o **Admins do domínio** grupo. Em vez disso, crie um grupo global e adicione esse grupo global ao grupo local de **Administradores** nos computadores cliente. Também pode criar um objeto de Política de Grupo para adicionar uma definição de Grupo Restrito, de modo a incluir a Conta de Instalação Push do Cliente no grupo local **Administradores**.  

 Para segurança adicional, crie várias Contas de Instalação Push do Cliente, cada uma com acesso administrativo a um número limitado de computadores, de forma que, no caso de uma conta ser comprometida, apenas os computadores cliente aos quais essa conta tem acesso sejam comprometidos.  

 **Remover certificados antes do processamento de imagens no computador cliente**  

 Se planeia implementar clientes através da utilização de tecnologia de processamento de imagens, remova sempre certificados tais como os certificados PKI que incluem autenticação de cliente e certificados autoassinados, antes da captura da imagem. Se não remover estes certificados, os clientes poderão representar-se entre si, e não será possível verificar os dados para cada cliente.  

 Para mais informações sobre como utilizar o Sysprep para preparar um computador para o processamento de imagens, consulte a documentação de implementação do Windows.  

 **Certifique-se de que os clientes de computador do Configuration Manager obtêm uma cópia autorizada destes certificados:**  

-   A chave de raiz fidedigna do Configuration Manager  

     Se não tiver expandido o esquema do Active Directory para o Configuration Manager e os clientes não utilizarem certificados PKI quando comunicam com pontos de gestão, os clientes dependem da chave de raiz fidedigna do Configuration Manager para autenticar pontos de gestão válido. Neste cenário, os clientes não têm como verificar que o ponto de gestão é um ponto de gestão fidedigno para a hierarquia, a não ser que utilizem a chave de raiz fidedigna. Sem a chave de raiz fidedigna, um intruso qualificado pode direcionar clientes para um ponto de gestão não autorizado.  

     Quando os clientes não conseguem transferir a chave de raiz fidedigna do Configuration Manager de Catálogo Global ou através da utilização de certificados PKI, pré-Aprovisione os clientes com a chave de raiz fidedigna para se certificar de que este não podem ser direcionado para um ponto de gestão não autorizado. Para obter mais informações, veja [Planear a Chave de Raiz Fidedigna](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

-   O certificado de assinatura do servidor do site  

     Os clientes utilizam o certificado de assinatura do servidor de site para verificar se o servidor do site assinou a política de cliente que transferiram a partir de um ponto de gestão. Este certificado é autoassinado pelo servidor do site e publicado nos Serviços de Domínio do Active Directory.  

     Quando os clientes não conseguem transferir o certificado de assinatura do servidor de site a partir do Catálogo Global, por predefinição transferem-no a partir do ponto de gestão. Quando o ponto de gestão está exposto a uma rede não fidedigna (tal como a Internet), instale manualmente o certificado de assinatura do servidor do site nos clientes, para garantir que não podem executar, a partir de um ponto de gestão comprometido, políticas de cliente que tenham sido adulteradas.  

     Para instalar manualmente o certificado de assinatura do servidor do site, utilize a propriedade CCMSetup client.msi **SMSSIGNCERT**. Para obter mais informações, veja [Acerca das propriedades de instalação do cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

 **Não utilize a atribuição automática de site, se o cliente irá transferir a chave de raiz fidedigna do primeiro ponto de gestão que contactar**  

 Este procedimento recomendado de segurança está ligado à entrada anterior. Para evitar o risco de um novo cliente transferir a chave de raiz fidedigna a partir de um ponto de gestão não autorizado, utilize a atribuição automática de site apenas nos cenários seguintes:  

-   O cliente pode aceder às informações de site do Configuration Manager que são publicadas para serviços de domínio do Active Directory.  

-   Pré-aprovisione o cliente com a chave de raiz fidedigna.  

-   Utilize certificados PKI de uma autoridade de certificação empresarial para estabelecer fidedignidade entre o cliente e o ponto de gestão.  

 Para obter mais informações sobre a chave de raiz fidedigna, veja [Planear a Chave de Raiz Fidedigna](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 **Instalar computadores cliente com a opção CCMSetup Client.msi SMSDIRECTORYLOOKUP = NoWINS**  

 O método mais seguro para a localização de serviço para os clientes localizarem sites e pontos de gestão é a utilização dos Serviços de Domínio do Active Directory. Se não for possível, por exemplo, porque não é possível expandir o esquema do Active Directory para o Configuration Manager, ou porque os clientes estão numa floresta não fidedigna ou um grupo de trabalho, pode utilizar a publicação de DNS como método de localização de serviço alternativo. Se estes dois métodos falharem, os clientes podem reverter para a utilização de WINS quando o ponto de gestão não estiver configurado para ligações de cliente HTTPS.  

 Como publicar para o WINS é menos seguro do que os outros métodos de publicação, configure os computadores cliente para não recorrerem à utilização de WINS especificando SMSDIRECTORYLOOKUP=NoWINS. Se tiver de utilizar WINS para a localização de serviço, utilize SMSDIRECTORYLOOKUP = WINSSECURE (a predefinição), que utiliza a chave de raiz fidedigna do Configuration Manager para validar o certificado autoassinado do ponto de gestão.  

> [!NOTE]  
>  Quando o cliente é configurado para SMSDIRECTORYLOOKUP = WINSSECURE e localiza um ponto de gestão a partir do WINS, o cliente verifica a respetiva cópia da chave de raiz fidedigna do Configuration Manager que está no WMI. Se a assinatura de gestão de ponto de correspondências de certificado do cliente da chave de raiz fidedigna, o certificado é validado, e o cliente comunica com o ponto de gestão que localizou através da utilização de WINS. Se a assinatura no certificado de ponto de gestão não corresponder do cliente da chave de raiz fidedigna, o certificado não é válido e o cliente não irá comunicar com o ponto de gestão que localizou através da utilização de WINS.  

 **Certifique-se de que as janelas de manutenção são suficientemente abrangentes para implementar atualizações de software críticas**  

 Pode configurar as janelas de manutenção para coleções de dispositivos restringir o número de vezes que o Configuration Manager pode instalar software nestes dispositivos. Se configurar a janela de manutenção para um período pequeno, o cliente pode não conseguir instalar as atualizações de software críticas, o que deixará o cliente vulnerável ao ataque que seria mitigado pela atualização de software.  

 **Para dispositivos Windows embedded que tenham filtros de escrita, tome medidas adicionais de segurança para reduzir a superfície de ataque se o Configuration Manager desative os filtros de escrita para manter as instalações de software e alterações**  

 Quando os filtros de escrita são ativados nos dispositivos Windows Embedded, quaisquer instalações ou alterações de software são efetuadas apenas na sobreposição e não persistem após o reinício do dispositivo. Se utilizar o Configuration Manager para desativar temporariamente os filtros de escrita para manter as instalações de software e as alterações, durante este período, o dispositivo incorporado é vulnerável a alterações em todos os volumes, o que inclui pastas partilhadas.  

 Apesar do Configuration Manager bloqueia o computador durante este período, para que apenas os administradores locais possam iniciar sessão, sempre que possível, tome medidas adicionais de segurança para ajudar a proteger o computador. Por exemplo, ative restrições adicionais na firewall e desligue o dispositivo da rede.  

 Se utilizar as janelas de manutenção para manter as alterações, planeie estas janelas cuidadosamente de forma a minimizar o tempo em que os filtros de escrita estão desativados mas com tempo suficiente para permitir as instalações de software e o reinício para concluir.  

 **Se utilizar a instalação de cliente baseada em atualização de software e instalar uma versão posterior do cliente no site, atualize a atualização de software que é publicada no ponto de atualização de software, para que os clientes recebam a versão mais recente**  

 Se instalar uma versão posterior do cliente no site, por exemplo, se atualizar o site, a atualização de software para a implementação do cliente que é publicada no ponto de atualização de software não é atualizada automaticamente. Deve voltar a publicar o cliente do Configuration Manager no ponto de atualização de software e clicar em **Sim** para atualizar o número de versão.  

 Para obter mais informações, consulte o procedimento "para publicar o cliente do Configuration Manager para o ponto de atualização de software" no [como instalar clientes do Configuration Manager pela instalação based](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

 **Configurar o agente do computador definição do dispositivo cliente entrada suspender o PIN do BitLocker no reinício sempre apenas para computadores nos quais confia e que tenham acesso físico restrito**  

 Quando configurar esta definição de cliente para **sempre**, Configuration Manager pode concluir a instalação do software para ajudar a garantir que as atualizações de software críticas são instaladas e que os serviços são retomados. No entanto, se um intruso intercetar o processo de reinício, ele poderá assumir o controlo do computador. Utilize esta definição apenas quando confiar no computador e quando o acesso físico ao computador é restrito. Por exemplo, esta definição pode ser apropriada para servidores num centro de dados.  

 **Não configure a política de execução de PowerShell de definição de dispositivo de cliente do agente do computador como "Ignorar".**  

 Esta definição de cliente permite que o cliente de Configuration Manager executar scripts PowerShell não assinados, o que poderia permitir a software maligno ser executada em computadores cliente. Se tem de selecionar esta opção, utilize uma definição de cliente personalizada e atribua-a apenas aos computadores cliente que têm de executar scripts PowerShell não assinados.  

##  <a name="bkmk_mobile"></a>Melhores práticas de segurança para dispositivos móveis  
 **Para dispositivos móveis que inscrever com o Configuration Manager e que serão suportados na Internet: Instalar o ponto de proxy de registo numa rede de perímetro e o ponto de registo na intranet**  

 Esta separação de funções ajuda a proteger o ponto de registo contra ataques. Se o ponto de registo for comprometido, um intruso poderá obter certificados para autenticação e roubar as credenciais de utilizadores que inscrevem os respetivos dispositivos móveis.  

 **Para dispositivos móveis: Configurar as definições de palavra-passe para ajudar a proteger dispositivos móveis contra acesso não autorizado**  

 Para dispositivos móveis que são inscritos pelo Configuration Manager: Utilize um item de configuração do dispositivo móvel para configurar a complexidade de palavra-passe para ser o PIN e, pelo menos, o comprimento predefinido para o comprimento mínimo da palavra-passe.  

 Para dispositivos móveis que não tenham o cliente do Configuration Manager instalado, mas que são geridos pelo conector do Exchange Server: Configurar o **definições de palavra-passe** para o conector do Exchange Server, de modo a que a complexidade de palavra-passe seja o PIN e especifique, pelo menos, o comprimento predefinido para o comprimento mínimo da palavra-passe.  

 **Para dispositivos móveis: Ajudar a impedir a adulteração de informações de inventário e as informações de estado, permitindo que as aplicações sejam executadas apenas quando são assinadas por empresas nas quais confia e não permite a ficheiros não assinados**  

 Para mais dispositivos móveis que são inscritos pelo Configuration Manager: Utilize um item de configuração do dispositivo móvel para configurar a definição de segurança **aplicações não assinadas** como **proibido** e configurar **ficheiros não assinados** seja uma origem fidedigna.  

 Para dispositivos móveis que não tenham o cliente do Configuration Manager instalado, mas que são geridos pelo conector do Exchange Server: Configurar o **definições da aplicação** para o conector do Exchange Server, de modo que **não assinados a instalação do ficheiro** e **aplicações não assinadas** estão configuradas como **proibido**.  

 **Para dispositivos móveis: Ajude a impedir ataques de elevação de privilégio ataques, bloqueando o dispositivo móvel quando não está a ser utilizado**  

 Para mais dispositivos móveis que são inscritos pelo Configuration Manager: Utilize um item de configuração do dispositivo móvel para configurar a definição de palavra-passe **tempo de inatividade em minutos antes do dispositivo móvel ser bloqueado**.  

 Para dispositivos móveis que não tenham o cliente do Configuration Manager instalado, mas que são geridos pelo conector do Exchange Server: Configurar o **definições de palavra-passe** para o conector do Exchange Server configure **tempo de inatividade em minutos antes do dispositivo móvel ser bloqueado**.  

 **Para dispositivos móveis: Ajude a impedir ataques de elevação de privilégios, restringindo os utilizadores que podem inscrever os respetivos dispositivos móveis.**  

 Utilize uma definição de cliente personalizada em vez de predefinições de cliente, para permitir que apenas utilizadores autorizados possam inscrever os respetivos dispositivos móveis.  

 **Para dispositivos móveis: Não implemente aplicações para utilizadores que têm dispositivos móveis inscritos pelo Configuration Manager ou o Microsoft Intune nos seguintes cenários:**  

-   Quando o dispositivo móvel é utilizado por mais do que uma pessoa.  

-   Quando o dispositivo é inscrito por um administrador em nome de um utilizador.  

-   Quando o dispositivo é transferido para outra pessoa sem extinção e, em seguida, reinscrição do dispositivo.  

 Durante a inscrição é criada uma relação de afinidade dispositivo/utilizador, que mapeia o utilizador que efetua a inscrição para o dispositivo móvel. Se outro utilizador usar o dispositivo móvel, ele poderá executar as aplicações que são implementadas para o utilizador original, o que poderá resultar numa elevação de privilégios. Da mesma forma, se um administrador inscrever o dispositivo móvel para um utilizador, as aplicações implementadas para o utilizador não serão instaladas no dispositivo móvel e, em vez disso, as aplicações que são implementadas para o administrador poderão ser instaladas.  

 Ao contrário da afinidade dispositivo / utilizador para computadores Windows, não é possível definir manualmente as informações de afinidade de dispositivo do utilizador para dispositivos móveis que são inscritos pelo Microsoft Intune.  

 Se transferir a propriedade de um dispositivo móvel inscrito pelo Intune, extinga o dispositivo móvel do Intune para remover a afinidade dispositivo / utilizador e, em seguida, peça ao utilizador atual para inscrever o dispositivo novamente.  

 **Para dispositivos móveis: Certifique-se de que os utilizadores inscrevem os seus próprios dispositivos móveis no Microsoft Intune**  

 Uma vez que durante a inscrição é criada uma relação de afinidade dispositivo/utilizador, que mapeia o utilizador que efetua a inscrição para o dispositivo móvel, se um administrador inscrever o dispositivo móvel para um utilizador, as aplicações implementadas para o utilizador não serão instaladas no dispositivo móvel e, em vez disso, as aplicações que são implementadas para o administrador poderão ser instaladas.  

 **Para o conector do Exchange Server: Certifique-se de que a ligação entre o servidor do site do Configuration Manager e o computador do Exchange Server está protegida**  

 Utilize IPsec se o Exchange Server for local; o Exchange alojado protege automaticamente a ligação utilizando SSL.  

 **Para o conector do Exchange Server: Utilize o princípio de menos privilégios para o conector**  

 Para obter uma lista dos cmdlets mínimos de que o conector do Exchange Server precisa, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

##  <a name="bkmk_macs"></a>Melhores práticas de segurança para Macs  
 **Para computadores Mac: Armazenar e aceder os ficheiros de origem do cliente a partir de uma localização segura.**  

 Gestor de configuração não verifica se estes ficheiros de origem de cliente foram adulterados antes da instalação ou a inscrição do cliente no computador Mac. Transfira estes ficheiros a partir de uma origem fidedigna e armazene-os e aceda aos mesmos de forma segura.  

 **Para computadores Mac: Independentemente do Configuration Manager, monitorize e controle o período de validade do certificado inscrito para os utilizadores.**  

 Para assegurar a continuidade do negócio, monitorize e controle o período de validade dos certificados que utiliza para computadores Mac. O Configuration Manager não suporta a renovação automática deste certificado nem indica que o certificado está prestes a expirar. Um período de validade típico é 1 ano.  

 Para obter informações sobre como renovar o certificado, veja [Renovar manualmente o certificado do cliente Mac](../../../../core/clients/deploy/deploy-clients-to-macs.md#renewing-the-mac-client-certificate).  

 **Para computadores Mac: Considere configurar o certificado de AC de raiz fidedigna de forma a que seja fidedigno para o protocolo SSL apenas para ajudar a proteger contra ataques de elevação de privilégios.**  

 Quando inscrever computadores Mac, um certificado de utilizador para gerir o cliente do Configuration Manager é instalado automaticamente, juntamente com o certificado de raiz fidedigna que o certificado de utilizador está encadeado. Se pretender restringir a fidedignidade deste certificado de raiz apenas para o protocolo SSL, pode utilizar o procedimento seguinte.  

 Depois de concluir este procedimento, o certificado de raiz não seria fidedigno para validar protocolos diferentes de SSL - por exemplo, correio seguro (S/MIME), autenticação extensível (EAP) ou assinatura de código.  

> [!NOTE]  
>  Também pode utilizar este procedimento se tiver instalado o certificado de cliente independentemente do Configuration Manager.  

 Para restringir o certificado de AC raiz apenas para o protocolo SSL:  

1.  No computador Mac, abra uma janela de terminal.  

2.  Introduza o comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

3.  Na caixa de diálogo **Acesso Keychain** da secção **Keychains**, clique em **Sistema** e, em seguida, na secção **Categoria**, clique em **Certificados**.  

4.  Localize e, em seguida, faça duplo clique sobre o certificado de AC raiz para o certificado de cliente Mac.  

5.  Na caixa de diálogo do certificado de AC de raiz, expanda a secção **Confiar** e, em seguida, faça as seguintes alterações:  

    1.  Na definição **Ao utilizar este certificado**, altere a predefinição **Confiar Sempre** para **Utilizar Predefinições do Sistema**.  

    2.  Na definição **Secure Sockets Layer (SSL)**, altere **nenhum valor especificado** para **Confiar Sempre**.  

6.  Fechar a caixa de diálogo e, quando lhe for pedido, introduza a palavra-passe de administrador e, em seguida, clique em **definições de atualização**.  

##  <a name="BKMK_SecurityIssues_Clients"></a>Problemas de segurança para clientes do Configuration Manager  
 Os seguintes problemas de segurança não têm nenhuma atenuação:  

-   As mensagens de estado que não são autenticadas  

     A autenticação não é efetuada nas mensagens de estado. Quando um ponto de gestão aceita ligações de cliente HTTP, qualquer dispositivo pode enviar mensagens de estado para o ponto de gestão. Se o ponto de gestão apenas aceita ligações de cliente HTTPS, um dispositivo tem de obter um certificado de autenticação de cliente válido junto de uma autoridade de certificação de raiz fidedigna, mas também poderia enviar qualquer mensagem de estado. Se um cliente envia uma mensagem de estado inválida, a mesma será rejeitada.  

     Há alguns potenciais ataques contra esta vulnerabilidade. Um intruso poderia enviar uma mensagem de estado fictícia para obter associação numa coleção baseada em consultas de mensagens de estado. Qualquer cliente poderia iniciar um denial of service contra o ponto de gestão, congestionando-o com mensagens de estado. Se as mensagens de estado estão a acionar ações nas regras de filtro de mensagem de estado, um intruso poderia acionar a regra de filtro de mensagens de estado. Um intruso também poderia enviar mensagens de estado que iriam tornar incorretas as informações dos relatórios.  

-   As políticas podem ser redirecionadas para os clientes não direcionados  

     Existem vários métodos que os atacantes poderiam utilizar para fazer com que uma política direcionada para um cliente fosse aplicada a um cliente completamente diferente. Por exemplo, um intruso num cliente fidedigno poderia enviar informações falsas de inventário ou deteção, para adicionar o computador a uma coleção a que não pertence, e depois receber todas as implementações a essa coleção. Embora existam controlos para ajudar a impedir os intrusos de modificarem as políticas diretamente, os intrusos poderiam utilizar uma política existente para reformatar e voltar a implementar um sistema operativo e enviá-lo para um computador diferente, criando um denial of service. Iriam requerer estes tipos de ataques necessitariam de temporização precisa e conhecimentos aprofundados da infraestrutura do Configuration Manager.  

-   Os registos de cliente permitem o acesso do utilizador  

     Todos os ficheiros de registo de cliente permitem aos utilizadores acesso de Leitura e aos Utilizadores Interativos acesso de Escrita. Se ativar o registo verboso, os intrusos podem ler os ficheiros de registo para procurarem informações sobre vulnerabilidades de compatibilidade ou de sistema. Os processos tais como a instalação de software que são executados no contexto de um utilizador têm de conseguir escrever nos registos com uma conta de utilizador de direitos restritos. Isto significa que um intruso também poderia escrever nos registos com uma conta de direitos restritos.  

     O risco mais grave é o facto de um intruso poder remover informações nos ficheiros de registo de que um administrador poderá necessitar para auditoria e deteção de intrusos.  

-   Um computador poderia ser utilizado para obter um certificado concebido para a inscrição do dispositivo móvel  

     Quando o Configuration Manager processa um pedido de inscrição, não é possível verificar se o pedido teve origem num dispositivo móvel ou um computador. Se o pedido de um computador, pode instalar um certificado PKI que depois permite o registo com o Configuration Manager. Para ajudar a evitar um ataque de elevação de privilégios neste cenário, permita que apenas utilizadores fidedignos inscrevam os respetivos dispositivos móveis, e monitorize com cuidado as atividades de inscrição.  

-   A ligação de um cliente ao ponto de gestão não é cancelada se um cliente for bloqueado, e o cliente bloqueado puder continuar a enviar pacotes de notificação de cliente para o ponto de gestão, como mensagens keep-alive  

     Quando bloqueia um cliente que já não confia, e o mesmo tenha estabelecido uma comunicação de notificação de cliente, o Configuration Manager não desliga a sessão. O cliente bloqueado pode continuar a enviar pacotes para o respetivo ponto de gestão, até o cliente desligar da rede. Estes pacotes são apenas pacotes pequenos, keep-alive, e estes clientes não podem ser geridos pelo Configuration Manager antes de serem desbloqueados.  

-   Quando utiliza a atualização automática de cliente e o cliente é direcionado para um ponto de gestão para transferir os ficheiros de origem do cliente, o ponto de gestão não é verificado como origem fidedigna  

-   Quando os utilizadores inscrevem computadores Mac pela primeira vez, estão em risco de spoofing de DNS  

     Quando o computador Mac liga ao ponto de proxy de registo durante a inscrição, não é provável que o computador Mac já tenha o certificado de AC raiz. Neste momento, o servidor não é considerado fidedigno pelo computador Mac e pede ao utilizador para continuar. Se o nome completamente qualificado do ponto de proxy de registo for resolvido por um servidor DNS não autorizado, poderá direcionar o computador Mac para um ponto proxy de registo não autorizado, e instalar certificados a partir de uma origem não fidedigna. Para ajudar a reduzir este risco, siga os procedimentos recomendados para evitar o spoofing de DNS no seu ambiente.  

-   A inscrição de Mac não limita os pedidos de certificado  

     Os utilizadores podem inscrever novamente os seus computadores Mac, pedindo de cada vez um novo certificado de cliente. Do Configuration Manager não verifica pedidos múltiplos nem limita o número de certificados pedidos a partir de um único computador. Um utilizador não autorizado poderia executar um script que repete o pedido de inscrição de linha de comandos, provocando um denial of service na rede ou na autoridade de certificação (AC) emissora. Para ajudar a reduzir este risco, monitorize com cuidado a AC emissora para detetar este tipo de comportamento suspeito. Um computador que apresenta este padrão de comportamento deve ser bloqueado imediatamente da hierarquia do Configuration Manager.  

-   Uma confirmação de eliminação de dados não verifica se os dados do dispositivo foram eliminados com êxito  

     Quando seleciona uma ação de eliminação de um dispositivo móvel e o Configuration Manager apresenta o estado da eliminação de dados a ser confirmada, a verificação é que o Configuration Manager enviada com êxito a mensagem e não que o dispositivo ter procedido à eliminação no mesmo. Além disso, para os dispositivos móveis que são geridos pelo conector do Exchange Server, uma confirmação de eliminação de dados verifica se o comando foi recebido pelo Exchange, e não pelo dispositivo.  

-   Se utilizar as opções para confirmar alterações nos dispositivos Windows Embedded, as contas podem ser bloqueadas mais cedo do que o esperado  

     Se o dispositivo Windows Embedded está a executar um sistema operativo anterior ao Windows 7 e um utilizador tenta iniciar sessão com os filtros de escrita desativados para confirmar as alterações efetuadas pelo Configuration Manager, o número de tentativas incorretas de início de sessão permitido antes da conta é bloqueada eficazmente para metade. Por exemplo, se a opção **Limiar de Bloqueio de Conta** estiver configurada para 6 e um utilizador errar três vezes a respetiva palavra-passe, a conta é bloqueada, criando uma situação de recusa de serviço.  Se os utilizadores tiverem de iniciar sessão em dispositivos incorporados neste cenário, devem ser alertados para a possibilidade de um limiar de bloqueio reduzido.  

##  <a name="BKMK_Privacy_Cliients"></a>Informações de privacidade para clientes do Configuration Manager  
 Ao implementar o cliente do Configuration Manager, ative as definições de cliente para poder utilizar funcionalidades de gestão do Configuration Manager. As definições que utiliza para configurar as funcionalidades podem ser aplicadas a todos os clientes na hierarquia do Configuration Manager, independentemente se estes são diretamente ligados à rede empresarial, ligadas através de uma sessão remota ou ligados à Internet, mas suportadas pelo Configuration Manager.  

 Informações de cliente são armazenadas na base de dados do Configuration Manager e não são enviadas à Microsoft. As informações são retidas na base de dados até serem eliminadas pelas tarefas de manutenção do site **Eliminar Dados de Deteção Desatualizados** todos os 90 dias. Pode configurar o intervalo de eliminação.  

 Antes de configurar o cliente do Configuration Manager, considere os requisitos de privacidade.  

### <a name="privacy-information-for-mobile-devices-that-are-enrolled-by-configuration-manager"></a>Informações de privacidade para dispositivos móveis inscritos pelo Configuration Manager  
 Para informações de privacidade para inscrever um dispositivo móvel pelo Configuration Manager, consulte [declaração de privacidade do System Center Configuration Manager - adenda do dispositivo móvel](../../../../core/misc/privacy/privacy-statement-mobile-device-addendum.md).  

### <a name="client-status"></a>Estado do cliente  
 O Configuration Manager monitoriza as atividades dos clientes e periodicamente avalia e pode retificar o cliente do Configuration Manager e as respetivas dependências. Estado do cliente está ativado por predefinição e utiliza a métrica do lado do servidor para verificações da atividade de cliente e, ações do lado do cliente para autoverificações, remediação e envio estado do cliente informações ao site do Configuration Manager. O cliente execute as autoverificações de acordo com uma agenda que pode ser configurada. O cliente envia os resultados das verificações para o site do Configuration Manager. Estas informações são encriptadas durante a transferência.  

 Informações de estado do cliente são armazenadas na base de dados do Configuration Manager e não são enviadas à Microsoft. As informações não são armazenadas em formato encriptado na base de dados do site. Estas informações são mantidas na base de dados até serem eliminadas de acordo com o valor configurado na definição do estado do cliente **Reter histórico do estado do cliente pelo seguinte número de dias**. O valor predefinido para esta definição é de 31 dias.  

 Antes de instalar o cliente do Configuration Manager com a verificação de estado do cliente, considere os requisitos de privacidade.  

##  <a name="BKMK_Privacy_ExchangeConnector"></a>Informações de privacidade para dispositivos móveis que são geridos com o conector do Exchange Server  
 O Conector do Exchange Server localiza e gere os dispositivos com ligação ao Exchange Server (no local ou alojado) utilizando o protocolo ActiveSync. Os registos localizados pelo conector do Exchange Server são armazenados na base de dados do Configuration Manager. As informações são recolhidas a partir do Exchange Server. Não contém qualquer informação adicional sobre o que é enviado para o Exchange Server pelos dispositivos móveis.  

 As informações do dispositivo móvel não são enviadas à Microsoft. As informações do dispositivo móvel são armazenadas na base de dados do Configuration Manager. As informações são retidas na base de dados até serem eliminadas pelas tarefas de manutenção do site **Eliminar Dados de Deteção Desatualizados** todos os 90 dias. Pode configurar o intervalo de eliminação.  

 Antes de instalar e configurar o conector do Exchange Server, considere os requisitos de privacidade.  

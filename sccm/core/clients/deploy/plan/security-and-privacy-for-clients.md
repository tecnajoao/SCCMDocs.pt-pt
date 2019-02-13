---
title: Cliente de segurança e privacidade
titleSuffix: Configuration Manager
description: Saiba mais sobre segurança e privacidade para clientes do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9671ccad42fc9135193cf41e058b472b52a412e1
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142311"
---
# <a name="security-and-privacy-for-configuration-manager-clients"></a>Segurança e privacidade para clientes do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo descreve a segurança e informações de privacidade para clientes do Configuration Manager. Também inclui informações para dispositivos móveis que são geridos pelos [conector do Exchange Server](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



##  <a name="BKMK_Security_Clients"></a> Melhores práticas de segurança para clientes  

Site do Configuration Manager aceita dados a partir de dispositivos que executam o cliente do Configuration Manager. Este comportamento introduz o risco de que os clientes poderem atacar o site. Por exemplo, poderiam enviar inventários incorretos ou tentar sobrecarregar os sistemas do site. Implemente o cliente do Configuration Manager apenas em dispositivos que confia. Além disso, utilize os seguintes procedimentos recomendados para ajudar a proteger o site contra dispositivos não autorizados ou comprometidos:  

#### <a name="use-public-key-infrastructure-pki-certificates-for-client-communications-with-site-systems-that-run-iis"></a>Utilizar certificados de infraestrutura de chaves públicas (PKI) para comunicações de clientes com sistemas de sites que executam o IIS  

-   Como uma propriedade do site, configure **Definições do sistema de sites** para **Apenas HTTPS**.  

-   Instale os clientes com o `UsePKICert` propriedade CCMSetup.  

-   Utilize uma lista de revogação de certificados (CRL) e certifique-se de que os clientes e servidores em comunicação podem aceder-lhe sempre.  

Clientes de dispositivos móveis e alguns clientes baseados na internet exigem estes certificados. A Microsoft recomenda estes certificados para todas as ligações de cliente na intranet.  

Para obter mais informações sobre os requisitos de certificado PKI e como eles são usados para ajudar a proteger o Configuration Manager, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


#### <a name="automatically-approve-client-computers-from-trusted-domains-and-manually-check-and-approve-other-computers"></a>Aprovar automaticamente computadores cliente de domínios fidedignos, e verificar e aprovar manualmente outros computadores  

Quando não é possível utilizar a autenticação de PKI, a aprovação identifica um computador que confia para serem geridos pelo Configuration Manager. A hierarquia tem as seguintes opções para configurar a aprovação do cliente:  
- Manual
- Automática para computadores em domínios fidedignos
- Automático para todos os computadores  

O método mais seguro de aprovação é aprovar automaticamente os clientes que são membros de domínios fidedignos. Em seguida, verificar manualmente e aprovar todos os outros computadores. Aprovar automaticamente todos os clientes não é recomendado, a menos que tenha outros controlos de acesso para impedir que computadores não fidedignos acedam à rede.  

Para obter mais informações sobre como aprovar computadores manualmente, consulte [gerir clientes a partir do nó dispositivos](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode).  


#### <a name="dont-rely-on-blocking-to-prevent-clients-from-accessing-the-configuration-manager-hierarchy"></a>Não se baseiam no bloqueio para impedir que os clientes acedam a hierarquia do Configuration Manager  

Os clientes bloqueados são rejeitados pela infraestrutura do Configuration Manager. Se os clientes estiverem bloqueados, não conseguirem comunicar com sistemas de sites para transferir a política, carregar dados de inventário ou enviar mensagens de estado. 

O bloqueio foi concebido para os seguintes cenários: 
- Para bloquear suportes de dados de arranque perdidos ou comprometidos ao implementar um sistema operacional a clientes
- Quando todos os sistemas de sites aceitam ligações de cliente HTTPS 

Quando os sistemas de sites aceitarem ligações de cliente HTTP, não pode confie no bloqueio para proteger a hierarquia do Configuration Manager de computadores não fidedignos. Neste cenário, um cliente bloqueado poderia voltar participar o site com um novo autoassinado certificado e hardware ID. 

Revogação de certificados é a primeira linha de defesa contra certificados potencialmente comprometidos. Uma lista de revogação de certificados (CRL) só está disponível a partir de uma infraestrutura de chaves públicas (PKI) suportada. Bloqueio de clientes no Configuration Manager oferece uma segunda linha de defesa para proteger a hierarquia.  

Para obter mais informações, consulte [determinar se deve bloquear clientes](/sccm/core/clients/deploy/plan/determine-whether-to-block-clients).  


#### <a name="use-the-most-secure-client-installation-methods-that-are-practical-for-your-environment"></a>Utilize os métodos de instalação de cliente mais seguros que adequados ao seu ambiente  

-   Para computadores de domínio, os métodos de instalação de cliente de Política de Grupo e de instalação de cliente baseada em atualização de software são mais seguros do que a instalação push de cliente.  

-   Se aplicar controlos de acesso e alterar os controlos, utilize os métodos de instalação de geração de imagens e manual.  

-   Na versão 1806 ou posterior, utilize a autenticação mútua Kerberos com a instalação push do cliente.  

De todos os métodos de instalação de cliente, instalação push do cliente é a menos segura devido à quantidade de dependências que ele possui. Estas dependências incluem permissões administrativas locais, a partilha Admin$ e exceções de firewall. O número e tipo destas dependências aumentam a superfície de ataque.  

A partir da versão 1806, ao utilizar o push de cliente, o site pode exigir a autenticação mútua do Kerberos, não permitindo fallback para NTLM antes de estabelecer a ligação. Esta melhoria ajuda a proteger a comunicação entre o servidor e o cliente. Para obter mais informações, consulte [como instalar clientes com a instalação push do cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).<!--1358204-->  

Para obter mais informações sobre os métodos de instalação de cliente diferentes, consulte [métodos de instalação de cliente](/sccm/core/clients/deploy/plan/client-installation-methods).  

Sempre que possível, selecione um método de instalação de cliente que requer menos permissões de segurança no Configuration Manager. Restringir os utilizadores administrativos que estão atribuídos a funções de segurança com permissões que podem ser utilizadas para fins que não sejam a implementação do cliente. Por exemplo, a configuração de atualização automática de cliente requer o **administrador total** função de segurança, que concede um utilizador administrativo todas as permissões de segurança.  

Para obter mais informações sobre as dependências e permissões de segurança necessárias para cada método de instalação do cliente, consulte "Dependências do método de instalação" em [pré-requisitos para clientes de computador](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#BKMK_prereqs_computers).  


#### <a name="if-you-must-use-client-push-installation-take-additional-steps-to-secure-the-client-push-installation-account"></a>Se tiver de utilizar a instalação push de cliente, tome medidas adicionais para proteger a Conta de Instalação Push do Cliente  

Esta conta tem de ser um membro do local **administradores** grupo em cada computador que instala o cliente do Configuration Manager. Nunca adicione a conta de instalação de Push do cliente para o **Admins do domínio** grupo. Em vez disso, crie um grupo global e, em seguida, adicione esse grupo global local **administradores** grupo nos seus clientes. Criar um objeto de política de grupo para adicionar uma definição de grupo restrito para adicionar a conta de instalação Push do cliente local **administradores** grupo.  

Para segurança adicional, crie vários cliente contas de instalação Push, cada um com acesso administrativo a um número limitado de computadores. Se uma conta for comprometida, apenas os computadores de cliente aos quais essa conta tem acesso sejam comprometidos.  


#### <a name="remove-certificates-before-imaging-clients"></a>Remover certificados antes dos clientes de geração de imagens  

Ao implementar clientes através da utilização de imagens do sistema operacional, remova sempre certificados antes de capturar a imagem. Estes certificados incluem certificados PKI para autenticação de cliente e certificados autoassinados. Se não remover estes certificados, os clientes poderão representar-se entre si. Não é possível verificar os dados para cada cliente.  

Para obter mais informações, consulte [criar uma sequência de tarefas para capturar um sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system).  


#### <a name="ensure-that-the-configuration-manager-computer-clients-get-an-authorized-copy-of-these-certificates"></a>Certifique-se de que os clientes de computador do Configuration Manager obtêm uma cópia autorizada destes certificados  

-   O certificado de chave de raiz fidedigna do Configuration Manager  

    Quando as duas das declarações a seguir forem verdadeiras, os clientes contam com a chave de raiz fidedigna do Configuration Manager para autenticar pontos de gestão válido:  

      - Ainda não tiver expandido o esquema do Active Directory para o Configuration Manager
      - Os clientes não utilizam certificados PKI quando comunicam com pontos de gestão  

    Neste cenário, os clientes não têm como verificar se o ponto de gestão é fidedigno para a hierarquia, a menos que utilizam a chave de raiz fidedigna. Sem a chave de raiz fidedigna, um intruso qualificado pode direcionar clientes para um ponto de gestão não autorizado.  

    Quando os clientes não é possível transferir a chave de raiz fidedigna do Configuration Manager a partir do Catálogo Global ou por certificados PKI, pré-Aprovisione os clientes com a chave de raiz fidedigna. Esta ação torna-se de que não são direcionados para um ponto de gestão não autorizado. Para obter mais informações, consulte [planear a chave de raiz fidedigna](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK).  

-   O certificado de assinatura do servidor do site  

     Os clientes utilizam este certificado para verificar que o servidor do site assinou a política transferida a partir de um ponto de gestão. Este certificado é autoassinado pelo servidor do site e publicado nos Serviços de Domínio do Active Directory.  

     Quando os clientes não é possível transferir o servidor de site certificado de assinatura de Catálogo Global, por predefinição transferem-lo do ponto de gestão. Se o ponto de gestão está exposto à rede não fidedigna, como a internet, instale manualmente o certificado em clientes de assinatura do servidor de site. Esta ação torna-se de que não conseguirem fazê-políticas de cliente violados partir de um ponto de gestão comprometido.  

     Para instalar manualmente o certificado de assinatura do servidor do site, utilize a propriedade CCMSetup client.msi **SMSSIGNCERT**. Para obter mais informações, consulte [acerca das propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties).  


#### <a name="dont-use-automatic-site-assignment-if-the-client-downloads-the-trusted-root-key-from-the-first-management-point-it-contacts"></a>Não utilize a atribuição automática de site se o cliente transfere a chave de raiz fidedigna a partir do primeiro ponto de gestão que contactar  

Para evitar o risco de um novo cliente transferir a chave de raiz fidedigna a partir de uma gestão de adesão apontar, atribuição para automática de site de utilização apenas nos seguintes cenários:  

-   O cliente pode aceder a informações de site do Configuration Manager que são publicadas para serviços de domínio do Active Directory.  

-   Pré-aprovisione o cliente com a chave de raiz fidedigna.  

-   Utilize certificados PKI de uma autoridade de certificação empresarial para estabelecer fidedignidade entre o cliente e o ponto de gestão.  

Para obter mais informações sobre a chave de raiz fidedigna, consulte [planear a chave de raiz fidedigna](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK).  


#### <a name="install-client-computers-with-the-ccmsetup-clientmsi-option-smsdirectorylookupnowins"></a>Instalar computadores cliente com a opção CCMSetup Client.msi SMSDIRECTORYLOOKUP=NoWINS  

O método mais seguro para a localização de serviço para os clientes localizarem sites e pontos de gestão é a utilização dos Serviços de Domínio do Active Directory. Às vezes, esse método não é possível que alguns ambientes. Por exemplo, porque não é possível expandir o esquema do Active Directory para o Configuration Manager ou porque os clientes estão numa floresta não fidedigna ou um grupo de trabalho. Se esse método não for possível, utilize a publicação de DNS como método de localização de serviço alternativo. Se estes dois métodos falharem, e quando o ponto de gestão não está configurado para ligações de cliente HTTPS, os clientes podem reverter utilização de WINS.  

Publicar para o WINS é menos seguro que os outros métodos de publicação. Configurar computadores cliente para não recorrerem à utilização de WINS especificando **SMSDIRECTORYLOOKUP = NoWINS**. Se tiver de utilizar WINS para a localização de serviço, utilize **SMSDIRECTORYLOOKUP = WINSSECURE**. Esta é a predefinição. Ele usa a chave de raiz fidedigna do Configuration Manager para validar o certificado autoassinado do ponto de gestão.  

> [!NOTE]  
>  Quando configura o cliente para **SMSDIRECTORYLOOKUP = WINSSECURE** e ele encontrar um ponto de gestão a partir do WINS, o cliente verifica a respetiva cópia da chave de raiz fidedigna do Configuration Manager que está no WMI.  
> 
> Se a assinatura do gerenciamento de ponto de correspondências de certificado cópia do cliente da chave de raiz fidedigna, o certificado é validado. Depois de validar o certificado, é iniciado o cliente comunica com o ponto de gestão que localizou através da utilização de WINS.  
> 
> Se a assinatura no certificado de ponto de gestão não corresponder a cópia do cliente da chave de raiz fidedigna, o certificado não é válido. Neste cenário, o cliente não comunicar com o ponto de gestão que localizou através da utilização de WINS.  


#### <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Certifique-se de que as janelas de manutenção são suficientemente abrangentes para implementar atualizações de software críticas  

Janelas de manutenção para coleções de dispositivos restringem as vezes que o Configuration Manager pode instalar software nestes dispositivos. Se configurar a janela de manutenção muito pequenos, o cliente não pode instalar atualizações de software críticas. Este comportamento deixa o cliente vulnerável a qualquer ataque que reduz a atualização de software.  


#### <a name="take-additional-security-precautions-to-reduce-the-attack-surface-on-windows-embedded-devices-with-write-filters"></a>Tome medidas adicionais de segurança para reduzir a superfície de ataque nos dispositivos de Windows embedded com filtros de escrita  

Quando ativa filtros de escrita em dispositivos Windows Embedded, quaisquer instalações de software ou alterações são feitas apenas na sobreposição. Estas alterações não persistem após o reinício do dispositivo. Se utilizar o Configuration Manager para desativar os filtros de escrita, durante este período o dispositivo incorporado é vulnerável a alterações em todos os volumes. Estes volumes incluem pastas compartilhadas.  

Gestor de configuração bloqueia o computador durante este período, para que apenas os administradores locais podem iniciar sessão. Sempre que possível, tome precauções de segurança adicionais para ajudar a proteger o computador. Por exemplo, ative restrições adicionais na firewall.  

Se utilizar janelas de manutenção para manter as alterações, planeie estas janelas cuidadosamente. Minimizar o tempo que escrever filtros estão desativados, mas que fiquem suficientemente longo para permitir que as instalações de software e o reinício para concluir.  


#### <a name="use-the-latest-client-version-with-software-update-based-client-installation"></a>Utilizar a versão mais recente do cliente com a instalação de cliente baseada em atualização de software

Se utilizar a instalação de cliente baseada em atualização de software e instalar uma versão posterior do cliente no site, atualize a atualização de software publicadas. Em seguida, os clientes recebem a versão mais recente do ponto de atualização de software.  

Quando atualizar o site, a atualização de software para implementação do cliente que é publicada no ponto de atualização de software não é atualizada automaticamente. Voltar a publicar o Gestor de configuração de cliente para a atualização de software de ponto e atualizar o número de versão.  

Para obter mais informações, consulte [como instalar clientes do Configuration Manager utilizando a instalação baseada em atualização de software](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientSUP).  


#### <a name="only-suspend-bitlocker-pin-entry-on-trusted-and-restricted-access-devices"></a>Apenas suspender a introdução de PIN do BitLocker em dispositivos fidedignos e acesso restrito  

Apenas configurar o definição de cliente **entrada de suspender o PIN do BitLocker no reinício** ao **sempre** para computadores que confia e que tenha acesso físico de restrito.

Ao configurar esta definição de cliente **sempre**, Configuration Manager pode concluir a instalação do software. Este comportamento ajuda a instalar atualizações de software críticas e retomar a serviços. Se um intruso intercetar o processo de reinício, eles poderá assumir o controlo do computador. Utilize esta definição apenas quando confiar no computador e quando o acesso físico ao computador é restrito. Por exemplo, esta definição pode ser apropriada para servidores num centro de dados.  

Para obter mais informações sobre esta definição de cliente, consulte [sobre as definições de cliente](/sccm/core/clients/deploy/about-client-settings#suspend-bitlocker-pin-entry-on-restart).  


#### <a name="dont-bypass-powershell-execution-policy"></a>Não ignorar a diretiva de execução do PowerShell   

Se configurar a definição de cliente do Configuration Manager **política de execução do PowerShell** para **omissão**, em seguida, o Windows permite a execução de scripts de PowerShell não assinados. Esse comportamento poderia permitir a software maligno ser executado em computadores cliente. Quando a sua organização requer que esta opção, utilize uma definição personalizada do cliente. Atribuí-lo a apenas os computadores de cliente que tem de executar scripts PowerShell não assinados.  

Para obter mais informações sobre esta definição de cliente, consulte [sobre as definições de cliente](/sccm/core/clients/deploy/about-client-settings#powershell-execution-policy).  



##  <a name="bkmk_mobile"></a> Melhores práticas de segurança para dispositivos móveis  


#### <a name="install-the-enrollment-proxy-point-in-a-perimeter-network-and-the-enrollment-point-in-the-intranet"></a>Instalar o ponto de proxy de registo numa rede de perímetro e o ponto de registo na intranet  

Para baseado na internet dispositivos móveis que inscrever com o Configuration Manager, instale o ponto de proxy de registo numa rede de perímetro e o ponto de registo na intranet. Esta separação de funções ajuda a proteger o ponto de registo contra ataques. Se um invasor compromete o ponto de registo, eles podem obter certificados para autenticação. Eles também podem roubar as credenciais de utilizadores que inscrevam os respetivos dispositivos móveis.  


#### <a name="configure-the-password-settings-to-help-protect-mobile-devices-from-unauthorized-access"></a>Configurar as definições de palavra-passe para ajudar a proteger dispositivos móveis contra acesso não autorizado  

*Para dispositivos móveis inscritos pelo Configuration Manager*: Utilize um item de configuração do dispositivo móvel para configurar a complexidade de palavra-passe como o PIN. Especifique, pelo menos, o comprimento mínimo da palavra-passe de predefinido.  

*Para dispositivos móveis que não tenham o cliente de Configuration Manager instalado, mas que são geridos pelo conector do Exchange Server*: Configurar o **definições de palavra-passe** para o conector do Exchange Server, de modo a que a complexidade de palavra-passe seja o PIN. Especifique, pelo menos, o comprimento mínimo da palavra-passe de predefinido.  


#### <a name="only-allow-applications-to-run-that-are-signed-by-companies-that-you-trust"></a>Permitir apenas as aplicações sejam executadas assinadas por empresas que confia  

Ajudar a impedir a adulteração de informações de inventário e informações de estado, permitindo que as aplicações sejam executadas apenas quando são assinadas por empresas nas que confia. Não permitir que os dispositivos instalar os ficheiros não assinados.  

*Para dispositivos móveis inscritos pelo Configuration Manager*: Utilize um item de configuração do dispositivo móvel para configurar a definição de segurança **aplicações não assinadas** como **proibido**. Configurar **ficheiros não assinados** para ser uma origem fidedigna.  

*Para dispositivos móveis que não tenham o cliente de Configuration Manager instalado, mas que são geridos pelo conector do Exchange Server*: Configurar o **as configurações do aplicativo** para o conector do Exchange Server, de modo que **instalação de ficheiros não assinados** e **aplicações não assinadas** são  **Proibido**.  


#### <a name="lock-mobile-devices-when-not-in-use"></a>Bloquear dispositivos móveis quando não está em utilização  

Ajudar a impedir ataques de elevação de privilégio ataques, bloqueando o dispositivo móvel quando não é utilizado.

*Para dispositivos móveis inscritos pelo Configuration Manager*: Utilize um item de configuração do dispositivo móvel para configurar a definição de palavra-passe **tempo de inatividade em minutos antes do dispositivo móvel ser bloqueado**.  

*Para dispositivos móveis que não tenham o cliente de Configuration Manager instalado, mas que são geridos pelo conector do Exchange Server*: Configurar o **definições de palavra-passe** para o conector do Exchange Server definir o **tempo de inatividade em minutos antes do dispositivo móvel ser bloqueado**.  


#### <a name="restrict-the-users-who-can-enroll-their-mobile-devices"></a>Restringir os utilizadores que podem inscrever os respetivos dispositivos móveis  

Ajudar a impedir ataques de elevação de privilégios, restringindo os utilizadores que podem inscrever os respetivos dispositivos móveis. Utilize uma definição de cliente personalizada em vez de predefinições de cliente, para permitir que apenas utilizadores autorizados possam inscrever os respetivos dispositivos móveis.  


#### <a name="user-device-affinity-guidance-for-mobile-devices"></a>Orientações de afinidade de dispositivo de utilizador para dispositivos móveis  

Não implemente aplicações para utilizadores que têm dispositivos móveis inscritos pelo Configuration Manager ou o Microsoft Intune nos seguintes cenários:  

-   O dispositivo móvel é utilizado por mais do que uma pessoa.  

-   O dispositivo é inscrito por um administrador em nome de um utilizador.  

-   O dispositivo é transferido para outra pessoa sem extinção e, em seguida, reinscrição do dispositivo.  

Inscrição de dispositivos cria uma relação de afinidade de dispositivo do utilizador. Esta relação mapeia o utilizador que efetua a inscrição para o dispositivo móvel. Se outro utilizador usar o dispositivo móvel, eles podem executar as aplicações implementadas para o utilizador original, o que poderá resultar numa elevação de privilégios. Da mesma forma, se um administrador inscrever o dispositivo móvel para um utilizador, as aplicações implementadas para o utilizador não estão instaladas no dispositivo móvel. Em vez disso, as aplicações implementadas para o administrador poderão ser instaladas.  

Ao contrário da afinidade dispositivo / utilizador para computadores Windows, não é possível definir manualmente as informações de afinidade de dispositivo do utilizador para dispositivos móveis inscritos pelo Microsoft Intune.  

Em primeiro lugar se transferir a propriedade de um dispositivo móvel inscrito pelo Intune, extinga o dispositivo móvel do Intune. Esta ação remove a relação de afinidade de dispositivo do utilizador. Em seguida, peça ao utilizador atual para inscrever o dispositivo novamente.  


#### <a name="make-sure-that-users-enroll-their-own-mobile-devices-for-microsoft-intune"></a>Certifique-se de que os utilizadores inscrevem os respetivos dispositivos móveis do Microsoft Intune  

Durante a inscrição, é criada uma relação de afinidade de dispositivo do utilizador. Esta ação mapeia o utilizador que efetua a inscrição para o dispositivo móvel. Se um administrador inscrever o dispositivo móvel para um utilizador, as aplicações implementadas para o utilizador não são instaladas no dispositivo móvel. Em vez disso, as aplicações implementadas para o administrador poderão ser instaladas.  


#### <a name="protect-the-connection-between-the-configuration-manager-site-server-and-the-exchange-server"></a>Proteger a ligação entre o servidor de site do Configuration Manager e o Exchange Server   

Se o servidor do Exchange no local, utilize o IPsec. Exchange alojado protege automaticamente a ligação utilizando SSL.  


#### <a name="use-the-principle-of-least-privileges-for-the-connector"></a>Utilize o princípio de menos privilégios para o conector  

Para obter uma lista dos cmdlets mínimos que requer que o conector do Exchange Server, consulte [gerir dispositivos móveis com o Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



##  <a name="bkmk_macs"></a> Melhores práticas de segurança para os Macs  


#### <a name="store-and-access-the-client-source-files-from-a-secured-location"></a>Store e acessar os arquivos de origem do cliente a partir de uma localização segura  

Antes de instalar ou a inscrição do cliente no computador Mac, o Configuration Manager não verifica se estes ficheiros de origem do cliente foram adulterados. Transferir estes ficheiros a partir de uma origem fidedigna. Armazenar e aceder aos mesmos em segurança.  


#### <a name="monitor-and-track-the-validity-period-of-the-certificate"></a>Monitorize e controle o período de validade do certificado  

Para assegurar a continuidade do negócio, monitorize e controle o período de validade dos certificados que utiliza para computadores Mac. O Configuration Manager não suporta a renovação automática deste certificado nem indica que o certificado está prestes a expirar. Um período de validade típico é um ano.  

Para obter mais informações sobre como renovar o certificado, consulte [renovar manualmente o certificado de cliente de Mac](/sccm/core/clients/deploy/deploy-clients-to-macs#renewing-the-mac-client-certificate).  


#### <a name="configure-the-trusted-root-certificate-for-ssl-only"></a>Configurar apenas o certificado de raiz fidedigna para SSL  

Para ajudar a proteger contra a elevação de privilégios, configure o certificado para a autoridade de certificação de raiz fidedigna, de modo que ele só é fidedigno para o protocolo SSL.

Ao inscrever computadores Mac, um certificado de utilizador para gerir o cliente do Configuration Manager é instalado automaticamente. Este certificado de utilizador inclui os certificados de raiz fidedigna na respetiva cadeia de confiança. Para restringir a fidedignidade deste certificado de raiz para o protocolo SSL apenas, utilize o seguinte procedimento:  

1.  No computador Mac, abra uma janela de terminal.  

2.  Introduza o seguinte comando: `sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3.  Na **acesso Keychain** caixa de diálogo a **Keychains** secção, clique em **sistema**. Em seguida, no **categoria** secção, clique em **certificados**.  

4.  Localize e faça duplo clique no certificado da AC de raiz para o certificado de cliente Mac.  

5.  Na caixa de diálogo do certificado de AC de raiz, expanda a secção **Confiar** e, em seguida, faça as seguintes alterações:  

    1.  **Ao utilizar este certificado**: Alteração da **confiar sempre** na definição **predefinições do sistema de utilização**.  

    2.  **Secure Sockets Layer (SSL)**: Alteração **nenhum valor especificado** ao **confiar sempre**.  

6.  Feche a caixa de diálogo. Quando lhe for pedido, introduza a palavra-passe do administrador e, em seguida, clique em **definições de atualização**.  

Depois de concluir este procedimento, o certificado de raiz só é considerada fidedigna para validar o protocolo SSL. Outros protocolos que são agora não fidedigno com este certificado de raiz incluir correio seguro (S/MIME), autenticação extensível (EAP) ou assinatura de código.  

> [!NOTE]  
>  Utilize também este procedimento se tiver instalado o certificado de cliente independentemente do Configuration Manager.  



##  <a name="BKMK_SecurityIssues_Clients"></a> Problemas de segurança de clientes do Configuration Manager  

Os seguintes problemas de segurança não têm nenhuma atenuação:  


#### <a name="status-messages-arent-authenticated"></a>Mensagens de estado não são autenticadas  

A autenticação não é efetuada nas mensagens de estado. Quando um ponto de gestão aceita ligações de cliente HTTP, qualquer dispositivo pode enviar mensagens de estado para o ponto de gestão. Se o ponto de gestão aceita ligações de cliente HTTPS apenas, um dispositivo tem de ter um certificado de autenticação de cliente válido, mas também poderia enviar qualquer mensagem de estado. O ponto de gestão. sys descartará qualquer mensagem de estado inválida recebida de um cliente.  

Há alguns potenciais ataques contra esta vulnerabilidade: 
- Um intruso poderá enviar uma mensagem de estado fictícia para obter associação numa coleção que se baseia em consultas de mensagens de estado. 
- Qualquer cliente poderia iniciar um denial of service contra o ponto de gestão, congestionando-o com mensagens de estado. 
- Se as mensagens de estado estão a acionar ações nas regras de filtro de mensagem de estado, um intruso poderia acionar a regra de filtro de mensagens de estado. 
- Um intruso poderia enviar mensagem de estado que iria tornar incorretas informações de relatórios.  


#### <a name="policies-can-be-retargeted-to-non-targeted-clients"></a>As políticas podem ser redirecionadas para os clientes não direcionados  

Existem vários métodos que os atacantes poderiam utilizar para fazer com que uma política direcionada para um cliente fosse aplicada a um cliente completamente diferente. Por exemplo, um intruso num cliente fidedigno poderia enviar informações falsas de inventário ou deteção para que o computador adicionado a uma coleção para que não deve pertencer. Em seguida, o que o cliente recebe todas as implementações a essa coleção. 

Existem controlos para ajudar a impedir que os atacantes modificar diretamente a política. No entanto, os intrusos poderiam utilizar uma política existente que reformata e reimplementa um sistema operacional e enviá-lo para um computador diferente. Esta política redirecionada foi possível criar um denial of service. Estes tipos de ataques exigiria que necessitariam de temporização precisa e conhecimentos aprofundados da infraestrutura do Configuration Manager.  


#### <a name="client-logs-allow-user-access"></a>Os registos de cliente permitem o acesso do utilizador  

Permitem a todos os ficheiros de registo de cliente a **usuários** grupo com *leitura* acesso e o especial **Interactive** utilizador com *escrever* acesso. Se ativar o registo verboso, os intrusos podem ler os ficheiros de registo para procurarem informações sobre vulnerabilidades de compatibilidade ou de sistema. Processos, como o software que o cliente é instalado num contexto do usuário devem escrever nos registos com uma conta de utilizador com direitos restritos. Este comportamento significa que um intruso também poderia escrever nos registos com uma conta com direitos restritos.  

O risco mais grave é que um intruso poder remover informações nos ficheiros de registo. Um administrador poderá ter estas informações para auditoria e deteção de intrusões.  


#### <a name="a-computer-could-be-used-to-obtain-a-certificate-thats-designed-for-mobile-device-enrollment"></a>Um computador poderia ser usado para obter um certificado que foi concebido para inscrição de dispositivos móveis  

Quando o Configuration Manager processa um pedido de inscrição, não consegue verificar o pedido teve originado a partir de um dispositivo móvel em vez de um computador. Se o pedido for de um computador, que pode instalar um certificado PKI que depois permite registar com o Configuration Manager. 

Para ajudar a evitar uma elevação de privilégio de ataque neste cenário, permitir apenas utilizadores fidedignos inscrevam os respetivos dispositivos móveis. Monitorize com cuidado as atividades de inscrição de dispositivo no site.  


#### <a name="a-blocked-client-can-still-send-messages-to-the-management-point"></a>Um cliente bloqueado pode ainda enviar mensagens para o ponto de gestão

Quando um cliente que já não confia, mas ele estabeleceu uma ligação de rede para a notificação do cliente, o Configuration Manager não desligar a sessão. O cliente bloqueado pode continuar a enviar pacotes para o respetivo ponto de gestão, até o cliente desligar da rede. Estes pacotes são apenas pacotes pequenos, keep-alive. Este cliente não pode ser gerido pelo Configuration Manager até que ele foi desbloqueado.  


#### <a name="automatic-client-upgrade-doesnt-verify-the-management-point"></a>Atualização automática de cliente não verifica o ponto de gestão

Quando utiliza a atualização automática do cliente, o cliente pode ser direcionado para um ponto de gestão para transferir os ficheiros de origem do cliente. Neste cenário, o cliente não verifica o ponto de gestão como uma origem fidedigna.  


#### <a name="when-users-first-enroll-mac-computers-theyre-at-risk-from-dns-spoofing"></a>Quando os utilizadores inscrevem os computadores Mac pela primeira vez, estes estão em risco de spoofing de DNS  

Quando o computador Mac liga ao ponto de proxy de inscrição durante a inscrição, é improvável que o computador Mac já possui o certificado de AC de raiz fidedigna. Neste momento, o computador Mac não confia no servidor e pede ao utilizador para continuar. Se um servidor DNS não autorizado resolve o nome de domínio completamente qualificado (FQDN) do ponto de proxy de registo, pode direcionar o computador Mac para um ponto de proxy de inscrição não autorizado a instalar certificados a partir de uma origem não fidedigna. Para ajudar a reduzir este risco, siga os procedimentos recomendados para evitar o spoofing de DNS no seu ambiente.  


#### <a name="mac-enrollment-doesnt-limit-certificate-requests"></a>Inscrição de MAC não limita os pedidos de certificado  

Os utilizadores podem inscrever novamente os seus computadores Mac, pedindo de cada vez um novo certificado de cliente. Gestor de configuração não verifica pedidos múltiplos ou limitar o número de certificados pedidos a partir de um único computador. Um utilizador não autorizado poderia executar um script que repete o pedido de inscrição da linha de comandos. Este ataque pode causar uma negação de serviço na rede ou sobre a autoridade de certificação (AC) emissora. Para ajudar a reduzir este risco, monitorize com cuidado a AC emissora para detetar este tipo de comportamento suspeito. Bloquear imediatamente da hierarquia do Configuration Manager qualquer computador que apresenta este padrão de comportamento.  


#### <a name="a-wipe-acknowledgment-doesnt-verify-that-the-device-has-been-successfully-wiped"></a>Uma confirmação de eliminação de dados não verifica que o dispositivo tiver sido eliminado com êxito  

Quando inicia uma ação de eliminação de dados para um dispositivo móvel e o Configuration Manager reconhece a eliminação dos dados, a verificação é que o Configuration Manager com êxito *enviados* a mensagem. Ele não verifica que o dispositivo *agia* no pedido. 

Para dispositivos móveis geridos pelo conector do Exchange Server, uma confirmação de eliminação de dados verifica que o comando foi recebido pelo Exchange, não pelo dispositivo.  


#### <a name="if-you-use-the-options-to-commit-changes-on-windows-embedded-devices-accounts-might-be-locked-out-sooner-than-expected"></a>Se utilizar as opções para confirmar alterações nos dispositivos Windows Embedded, as contas podem ser bloqueadas mais cedo do que o esperado  

Se o dispositivo Windows Embedded está a executar uma versão do SO anterior ao Windows 7 e um utilizador tenta iniciar sessão, os filtros de escrita desativados pelo Configuration Manager, Windows permite que apenas metade do número de tentativas incorretas de configurado antes do bloqueio da conta fora. 

Por exemplo, configurar a política de domínio para **limiar de bloqueio de conta** a seis tentativas. Um usuário digitar a palavra-passe três vezes e a conta é bloqueada. Este comportamento efetivamente cria um denial of service. Se os utilizadores tem de iniciar sessão dispositivos incorporados neste cenário, ser alertados o potencial de um limiar de bloqueio reduzido.  



##  <a name="BKMK_Privacy_Clients"></a> Informações de privacidade para clientes do Configuration Manager  

Ao implementar o cliente do Configuration Manager, ativar definições de cliente para recursos do Configuration Manager. As definições que utilizar para configurar as funcionalidades podem aplicar a todos os clientes na hierarquia do Configuration Manager. Este comportamento é o mesmo se forem diretamente ligados à rede interna, ligadas através de uma sessão remota ou ligados à internet.  

Informações do cliente são armazenadas na base de dados do Configuration Manager no seu SQL server e não são enviadas à Microsoft. Informações são mantidas na base de dados até serem eliminada pelas tarefas de manutenção do site **eliminar dados de deteção desatualizados** todos os 90 dias. Pode configurar o intervalo de eliminação. 

Alguns dados de diagnóstico e utilização de resumidas ou agregados são enviados à Microsoft. Para obter mais informações, consulte [diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  

Antes de configurar o cliente do Configuration Manager, considere os requisitos de privacidade.  


### <a name="privacy-information-for-mobile-devices-that-are-enrolled-by-configuration-manager"></a>Informações de privacidade para dispositivos móveis inscritos pelo Configuration Manager  

Para obter informações de privacidade quando inscreve um dispositivo móvel pelo Configuration Manager, consulte [declaração de privacidade do System Center Configuration Manager - adenda do dispositivo móvel](/sccm/core/misc/privacy/privacy-statement-mobile-device-addendum).  


### <a name="client-status"></a>Estado do cliente  

O Configuration Manager monitoriza as atividades dos clientes. Avalia o cliente do Configuration Manager periodicamente e pode remediar problemas com o cliente e as respetivas dependências. Estado do cliente está ativado por predefinição. Utiliza as métricas do lado do servidor para as verificações de atividade do cliente. Ações do lado do cliente de utiliza de estado do cliente para autoverificações, remediação e para o estado do cliente a enviar informações para o site. O cliente executa as autoverificações de acordo com uma agenda que configurar. O cliente envia os resultados das verificações de site do Configuration Manager. Estas informações são encriptadas durante a transferência.  

Informações de estado do cliente são armazenadas na base de dados do Configuration Manager no seu SQL server e não são enviadas à Microsoft. As informações não estão armazenadas em formato encriptado na base de dados do site. Estas informações são mantidas na base de dados até serem eliminada de acordo com o valor configurado para o **Reter histórico do Estado de cliente para o número de dias seguinte** definição do Estado do cliente. O valor predefinido para esta definição é de 31 dias.  

Antes de instalar o cliente do Configuration Manager com a verificação de estado do cliente, considere os requisitos de privacidade.  



##  <a name="BKMK_Privacy_ExchangeConnector"></a> Informações de privacidade para dispositivos móveis que são geridos com o conector do Exchange Server  

O conector do Exchange Server localiza e gere dispositivos que ligar no local ou hospedado do Exchange Server utilizando o protocolo ActiveSync. Os registos localizados pelo conector do Exchange Server são armazenados na base de dados do Configuration Manager no seu SQL server. As informações são coletadas do Exchange Server. Ele não contém qualquer informação adicional sobre o que os dispositivos móveis que enviar para o Exchange Server.  

As informações de dispositivo móvel não for enviadas à Microsoft. As informações de dispositivo móvel são armazenadas na base de dados do Configuration Manager no seu SQL server. Informações são mantidas na base de dados até serem eliminada pela tarefa de manutenção do site **eliminar dados de deteção desatualizados** todos os 90 dias. Configurar o intervalo de eliminação.  

Antes de instalar e configurar o conector do Exchange Server, considere os requisitos de privacidade.  

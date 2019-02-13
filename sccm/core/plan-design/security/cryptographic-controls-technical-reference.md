---
title: Referência técnica de controlos criptográficos
titleSuffix: Configuration Manager
description: Saiba como a assinatura e encriptação podem ajudar a proteger de ataques de leitura de dados no System Center Configuration Manager.
ms.date: 12/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17a99fff7b6486d6de26e2d4c153244a5665391a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136648"
---
# <a name="cryptographic-controls-technical-reference"></a>Referência técnica de controlos criptográficos

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


System Center Configuration Manager utiliza a assinatura e encriptação para ajudar a proteger a gestão de dispositivos na hierarquia do Configuration Manager. Com a assinatura, se os dados foram alterados em trânsito, é descartado. A criptografia ajuda a impedir que um atacante de ler os dados utilizando um analisador de protocolo de rede.  

 O algoritmo hash principal utilizadas pelo Configuration Manager para a assinatura é SHA-256. Quando dois sites do Configuration Manager comunicam entre si, assinam as respetivas comunicações com SHA-256. O algoritmo de encriptação principal implementado no Configuration Manager é o 3DES. Isto é utilizado para armazenar dados na base de dados do Configuration Manager e para a comunicação de cliente HTTP. Quando utiliza a comunicação de cliente através de HTTPS, pode configurar a sua infraestrutura de chaves públicas (PKI) para utilizar certificados RSA com os algoritmos de hash máximo e comprimentos de chave documentados em [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Na maioria das operações de criptografia para sistemas operacionais baseados em Windows, o Configuration Manager utiliza algoritmos SHA-2, 3DES e AES e RSA da Rsaenh de biblioteca CryptoAPI do Windows.  

> [!IMPORTANT]  
>  Consulte as informações sobre as alterações recomendadas em resposta às vulnerabilidades SSL em [About SSL Vulnerabilities](#about-ssl-vulnerabilities).  

##  <a name="cryptographic-controls-for-configuration-manager-operations"></a>Controlos criptográficos para operações do Configuration Manager  
 Informações no Configuration Manager podem ser assinadas e criptografadas, se é ou não utilizar certificados PKI com o Configuration Manager.  

### <a name="policy-signing-and-encryption"></a>Política de assinatura e encriptação  
 As atribuições de políticas de cliente são assinadas pelo certificado de assinatura autoassinado do servidor do site para ajudar a evitar o risco de segurança que representa o envio de políticas que tenham sido adulteradas por um ponto de gestão comprometido. Isso é importante se estiver a utilizar a gestão de clientes baseados na Internet porque este ambiente requer um ponto de gestão que é exposto a comunicações de Internet.  

 A política é encriptada com 3DES quando contém dados confidenciais. Políticas que contenham dados confidenciais são enviadas apenas para clientes autorizados. Políticas que não tenham dados confidenciais não são encriptadas.  

 Quando a política é armazenada nos clientes, é encriptada com a interface de programação de aplicativo proteção de dados (DPAPI).  

### <a name="policy-hashing"></a>Hash de políticas  
 Quando a política de pedido de clientes do Configuration Manager, obtêm primeiro uma atribuição de política para que eles saibam a quais diretivas se aplicam aos mesmos e, em seguida, solicitarem apenas os corpos dessas política. Cada atribuição de política contém o hash calculado para o corpo da política correspondente. O cliente obtém os corpos de políticas aplicáveis e calcula o hash desses corpos. Se o hash contido no corpo de política transferido não corresponder ao hash na atribuição de política, o cliente rejeita o corpo de política.  

 Os algoritmos hash para políticas são SHA-1 e SHA-256.  

### <a name="content-hashing"></a>Hash de conteúdo  
 O serviço de gestão de distribuição no servidor do site calcula o hash dos ficheiros de conteúdo de todos os pacotes. O fornecedor de política inclui o hash na política de distribuição de software. Quando o cliente do Configuration Manager transfere o conteúdo, o cliente volta a gerar o hash localmente e compara-a com aquele fornecido na política. Se os hashes coincidirem, o conteúdo não foi alterado e o cliente instala-o. Se um único byte do conteúdo tiver sido alterado, os hashes não coincidirão e o software não será instalado. Esta verificação ajuda a garantir que é instalado o software correto, uma vez que o conteúdo real é verificado em relação à política.  

 O algoritmo hash predefinido para conteúdo é o SHA-256. Para alterar esta predefinição, consulte a documentação para o Configuration Manager Software Development Kit (SDK).  

 Nem todos os dispositivos suportam hash de conteúdo. As exceções incluem:  

-   Clientes Windows, quando transmitem em fluxo conteúdo de App-V.  

-   Os clientes do Windows Phone, embora estes clientes verificam a assinatura de uma aplicação que esteja assinada por uma origem fidedigna.  

-   Cliente do Windows RT, embora estes clientes verificam a assinatura de um aplicativo que esteja assinada por uma origem fidedigna e também utiliza a validação do pacote (PFN) de nome completo.  

-   iOS, embora estes dispositivos verificam a assinatura de um aplicativo que esteja assinada por qualquer certificado de Programador de uma origem fidedigna.  

-   Clientes Nokia, no entanto, estes clientes verificam a assinatura de um aplicativo que usa um certificado autoassinado. Em alternativa, a assinatura de um certificado de uma origem fidedigna e o certificado podem assinar aplicações SIS (Symbian Installation Source) da Nokia.  

-   Android. Além disso, estes dispositivos não utilizam validação de assinaturas para instalação de aplicações.  

-   Os clientes executados em versões do Linux e UNIX que não suportam SHA-256. Para obter mais informações, consulte [planejar a implantação de cliente para computadores Linux e UNIX](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers).  

### <a name="inventory-signing-and-encryption"></a>Assinatura e encriptação de inventário  
 O inventário que os clientes enviam para os pontos de gestão é sempre assinado pelos dispositivos, independentemente de comunicarem com os pontos de gestão por HTTP ou HTTPS. Se utilizarem HTTP, pode optar por encriptar estes dados, que é a melhor prática de segurança.  

### <a name="state-migration-encryption"></a>Encriptação de migração de estado  
 Os dados armazenados em pontos de migração de estado da implementação de sistemas operativos são sempre encriptados pela Ferramenta de Migração de Estado de Utilizador (USMT) utilizando 3DES.  

### <a name="encryption-for-multicast-packages-to-deploy-operating-systems"></a>Encriptação de pacotes multicast implementar sistemas operativos  
 Para cada pacote de implementação de sistema operativo, pode ativar a encriptação quando o pacote for transferido para computadores através da utilização de multicast. A encriptação utiliza a norma AES (Advanced Encryption Standard). Se ativar a encriptação, não é necessária qualquer configuração adicional de certificados. O ponto de distribuição de capacidade multicast gera automaticamente chaves simétricas para encriptar o pacote. Cada pacote tem uma chave de encriptação diferente. A chave é armazenada no ponto de distribuição de capacidade multicast utilizando APIs padrão do Windows. Quando o cliente liga à sessão multicast, a troca de chaves ocorre através de um canal encriptado com o certificado de autenticação de cliente emitido pela PKI (quando o cliente utilizar HTTPS) ou o certificado autoassinado (quando o cliente utilizar HTTP). O cliente armazena a chave na memória apenas durante a sessão multicast.  

### <a name="encryption-for-media-to-deploy-operating-systems"></a>Encriptação para suporte de dados implementar sistemas operativos  
 Quando utiliza suportes de dados para implementar sistemas operativos e especifica uma palavra-passe para proteger os suportes de dados, as variáveis de ambiente são encriptadas utilizando AES (Advanced Encryption Standard). Outros dados existentes no suporte de dados, incluindo pacotes e conteúdo de aplicações, não estão encriptados.  

### <a name="encryption-for-content-that-is-hosted-on-cloud-based-distribution-points"></a>Encriptação de conteúdo que está alojado em pontos de distribuição baseado na nuvem  
 Começando com o System Center 2012 Configuration Manager SP1, quando utiliza pontos de distribuição baseado na nuvem, o conteúdo que carregar nestes pontos de distribuição é encriptado utilizando encriptação AES (Advanced Standard) com um tamanho de chave de 256 bits. O conteúdo será novamente encriptado sempre que for atualizado. Quando os clientes transferirem o conteúdo, este será encriptado e protegido pela ligação HTTPS.  

### <a name="signing-in-software-updates"></a>Inscrever-se em atualizações de software  
 Todas as atualizações de software têm de ser assinadas por um fabricante fidedigno para proteção contra adulteração. Em computadores cliente, o Windows Update Agent (WUA) procura as atualizações no catálogo, mas não instalará uma atualização se não conseguir localizar o certificado digital no arquivo Fabricantes Fidedignos no computador local. Se tiver sido utilizado um certificado autoassinado para publicar as atualizações no catálogo, como o certificado autoassinado WSUS Publishers, este terá de constar também no arquivo de certificados Autoridades de Certificação de Raiz Fidedigna, no computador local, para verificação da validade do certificado. O WUA também verifica se a definição de Política de Grupo **Permitir conteúdo assinado da localização do serviço de atualização da Microsoft na intranet** está ativada no computador local. Esta definição de política tem de estar ativada para que o WUA procure atualizações criadas e publicadas com o Updates Publisher.  

 Quando as atualizações de software são publicadas no System Center Updates Publisher, são assinadas por um certificado digital quando são publicadas ou atualizadas num servidor. Pode especificar um certificado PKI ou configurar o Updates Publisher para gerar um certificado autoassinado para assinar a atualização de software.  

### <a name="signed-configuration-data-for-compliance-settings"></a>Dados de configuração para definições de compatibilidade assinados  
 Quando importa dados de configuração, o Configuration Manager verifica a assinatura digital do ficheiro. Se os dados não tiverem sido assinados ou se a verificação da assinatura digital falhar, será apresentado um aviso e será perguntado se pretende continuar com a importação. Continue a importar os dados de configuração apenas se confiar explicitamente no fabricante e na integridade dos ficheiros.  

### <a name="encryption-and-hashing-for-client-notification"></a>Criptografia e hash para notificação de cliente  
 Se utilizar notificações de cliente, todas as comunicações utilizarão TLS e a encriptação mais elevada que os sistemas operativos do servidor e do cliente possam negociar. Por exemplo, um computador cliente executando o Windows 7 e um ponto de gestão com o Windows Server 2008 R2 suportam encriptação AES de 128 bits, enquanto um computador cliente executando o Vista para o mesmo ponto de gestão negociarão-se para baixo para a encriptação 3DES. A mesma negociação ocorre para o hash dos pacotes que são transferidos durante a notificação do cliente, que utiliza SHA-1 ou SHA-2.  

##  <a name="certificates-used-by-configuration-manager"></a>Certificados utilizados pelo Configuration Manager  
 Para obter uma lista dos certificados de infraestrutura de chaves públicas (PKI) que podem ser utilizadas pelo Configuration Manager, quaisquer requisitos especiais ou limitações, e como os certificados são utilizados, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements). Esta lista inclui os comprimentos de chaves e algoritmos hash suportados. A maioria dos certificados suporta SHA-256 e chaves de 2048 bits.  

> [!NOTE]  
>  Todos os certificados que utiliza o Configuration Manager tem de conter apenas carateres de byte único no nome do requerente ou nome alternativo do requerente.  

 Os certificados PKI são necessários para os seguintes cenários:  

- Quando gerir clientes do Configuration Manager na Internet.  

- Quando gerir clientes do Configuration Manager em dispositivos móveis.  

- Quando gerir computadores Mac.  

- Quando utilizar pontos de distribuição baseados na nuvem.  

  Para a maioria das outras comunicações do Configuration Manager que exigem certificados para autenticação, assinatura ou encriptação, o Configuration Manager utiliza automaticamente certificados PKI se estiverem disponíveis. Se não estiverem disponíveis, o Configuration Manager gera certificados autoassinados.  

  O Configuration Manager não utiliza certificados PKI quando gere dispositivos móveis utilizando o conector do Exchange Server.  

### <a name="mobile-device-management-and-pki-certificates"></a>Gestão de dispositivos móveis e certificados PKI  
 Se o dispositivo móvel não tiver sido bloqueado pela operadora do celular, pode utilizar o Configuration Manager ou o Microsoft Intune para pedir e instalar um certificado de cliente. Este certificado fornece autenticação mútua entre o cliente do dispositivo móvel e sistemas de sites do Configuration Manager ou dos serviços do Microsoft Intune. Se o seu dispositivo móvel estiver bloqueado, não é possível utilizar o Configuration Manager ou o Intune para implementar certificados.  

 Se ativar o inventário de hardware para dispositivos móveis, o Configuration Manager ou o Intune também fará um inventário dos certificados que estão instalados no dispositivo móvel.   

### <a name="operating-system-deployment-and-pki-certificates"></a>Implementação do sistema operativo e certificados PKI  
 Quando utilizar o Configuration Manager para implementar sistemas operativos e um ponto de gestão requer ligações de cliente HTTPS, o computador cliente também tem de ter um certificado para comunicar com o ponto de gestão, mesmo que se numa fase transitória, tais como arranque a partir de suportes de dados de sequência de tarefas ou um ponto de distribuição com PXE ativado. Para suportar este cenário, tem de criar um certificado de autenticação de cliente PKI e exportá-lo com a chave privada e, em seguida, importá-lo para as propriedades do servidor de site e também adicionar o certificado de AC de raiz fidedigna do ponto de gestão.  

 Se criar suportes de dados de arranque, importa o certificado de autenticação de cliente quando criar o suporte de dados de arranque. Configure uma palavra-passe no suporte de dados de arranque para ajudar a proteger a chave privada e outros dados confidenciais configurados na sequência de tarefas. Os computadores que iniciam a partir do suporte de dados de arranque irão apresentar o mesmo certificado ao ponto de gestão tal como necessário para as funções dos clientes, como o pedido de política de cliente.  

 Se estiver a utilizar o arranque PXE, importará o certificado de autenticação de cliente para o ponto de distribuição ativado com PXE, que utiliza o mesmo certificado para todos os clientes que iniciam a partir de um ponto de distribuição ativado com PXE. Como procedimento recomendado de segurança, solicite aos utilizadores que liguem os computadores a um serviço PXE para fornecer uma palavra-passe que ajude a proteger a chave privada e outros dados confidenciais nas sequências de tarefas.  

 Se algum destes certificados de autenticação de cliente for comprometido, bloqueie os certificados no nó **Certificados** na área de trabalho **Administração** , nó **Segurança** . Para gerir estes certificados, tem de ter a definição **Gerir certificado de implementação do sistema operativo** correta.  

 Depois do sistema operativo é implementado e o Configuration Manager está instalado, o cliente exigirá seu próprio certificado de autenticação de cliente PKI para comunicações HTTPS de clientes.  

### <a name="isv-proxy-solutions-and-pki-certificates"></a>Soluções de proxy ISV e certificados PKI  
 Fornecedores de Software independentes (ISVs) pode criar aplicativos que estendem o Configuration Manager. Por exemplo, um ISV poderia criar extensões para suportar plataformas de cliente não Windows, tais como computadores Macintosh ou UNIX. No entanto, se os sistemas de sites precisarem de ligações cliente HTTPS, estes clientes têm também de utilizar certificados KPI para a comunicação com o site. O Configuration Manager inclui a capacidade de atribuir um certificado ao proxy ISV que permite as comunicações entre os clientes proxy ISV e o ponto de gestão. Se utilizar extensões que requerem certificados de proxy ISV, consulte a documentação desse produto. Para obter mais informações sobre como criar certificados de proxy ISV, consulte o Software Developer Kit (SDK) do Configuration Manager.  

 Se o certificado ISV for comprometido, bloqueie o certificado no nó **Certificados** na área de trabalho **Administração** , nó **Segurança** .  

### <a name="asset-intelligence-and-certificates"></a>Asset intelligence e certificados  
 O Configuration Manager é instalado com um certificado X.509 que o ponto de sincronização do Asset Intelligence utiliza para ligar à Microsoft. O Configuration Manager utiliza este certificado para pedir um certificado de autenticação de cliente a partir do serviço de certificado Microsoft. O certificado de autenticação de cliente é instalado no servidor de sistema de site do ponto de sincronização do Asset Intelligence e é utilizado para autenticar o servidor para a Microsoft. O Configuration Manager utiliza o certificado de autenticação de cliente para transferir o catálogo do Asset Intelligence e para carregar os títulos de software.  

 Este certificado tem um comprimento de chave de 1024 bits.  

### <a name="cloud-based-distribution-points-and-certificates"></a>Pontos de distribuição baseado na nuvem e certificados  
 A partir do System Center 2012 Configuration Manager SP1, os pontos de distribuição baseado na nuvem exigem um certificado de gestão (auto-assinado ou PKI) que carrega para o Microsoft Azure. Este certificado de gestão requer a capacidade de autenticação de servidor e um comprimento de chave do certificado de 2048 bits. Além disso, é necessário configurar um certificado de serviço para cada ponto de distribuição baseado na nuvem, que não pode ser autoassinado mas tem de ter capacidade de autenticação de servidor e um comprimento de chave do certificado mínimo de 2048 bits.  

> [!NOTE]  
>  O certificado de gestão autoassinado destina-se apenas a fins de teste e não se destina a utilização em redes de produção.  

 Os clientes não necessitam de um certificado PKI de cliente para utilizarem pontos de distribuição baseados na nuvem; eles procedem à autenticação para a gestão através da utilização de um certificado autoassinado ou um certificado PKI de cliente. O ponto de gestão, em seguida, emite um token de acesso do Configuration Manager para o cliente, o que o cliente apresenta ao ponto de distribuição baseado na nuvem. O token é válido durante 8 horas.  

### <a name="the-microsoft-intune-connector-and-certificates"></a>O Microsoft Intune Connector e certificados  
 Quando o Microsoft Intune inscreve dispositivos móveis, pode gerir estes dispositivos móveis no Configuration Manager através da criação de um conector do Microsoft Intune. O conector utiliza um certificado PKI com capacidade de autenticação de cliente para autenticar o Configuration Manager para o Microsoft Intune e para transferir todas as informações entre eles, utilizando SSL. A chave do certificado tem o tamanho de 2048 bits e utiliza o algoritmo hash SHA-1.  

 Quando o conector é instalado, é criado um certificado de assinatura e armazenado no servidor do site para chaves de sideload e é criado um certificado de encriptação e armazenado no ponto de registo de certificados para encriptar o desafio SCEP (Simple Certificate Enrollment Protocol). Estes certificados também têm um tamanho de chave de 2048 bits e utilizam o algoritmo hash SHA-1.  

 Quando o Intune inscreve dispositivos móveis, instala um certificado PKI no dispositivo móvel. Este certificado tem capacidade de autenticação de cliente, utiliza um tamanho de chave de 2048 bits e utiliza o algoritmo hash SHA-1.  

 Estes certificados PKI são automaticamente solicitados, gerados e instalados pelo Microsoft Intune.  

### <a name="crl-checking-for-pki-certificates"></a>Verificação CRL para certificados PKI  
 Uma lista de revogação de certificados PKI (CRL) aumenta a sobrecarga administrativa e de processamento, mas apresenta mais segurança. No entanto, se a verificação CRL está ativada, mas a CRL está inacessível, a ligação de PKI falha. Para obter mais informações, consulte [segurança e privacidade para o Configuration Manager](/sccm/core/plan-design/security/security-and-privacy).  

 Verificação da lista (CRL) de revogação de certificado está ativada por predefinição no IIS, portanto, se estiver a utilizar uma CRL com a implementação de PKI, não há nada adicional a configurar na maioria dos sistemas de site do Configuration Manager que executam o IIS. A exceção é para atualizações de software, que requerem um passo manual para ativar a verificação CRL para verificar as assinaturas nos ficheiros de atualização de software.  

 A verificação CRL está ativada por predefinição para computadores cliente quando utilizam ligações de cliente HTTPS. Não é possível desativar a verificação CRL para clientes em computadores Mac no Configuration Manager SP1 ou posterior.  

 A verificação CRL não é suportada para as seguintes ligações no Configuration Manager:  

-   Ligações de servidor a servidor.  

-   Dispositivos móveis inscritos pelo Configuration Manager.  

-   Dispositivos móveis inscritos pelo Microsoft Intune.  

##  <a name="cryptographic-controls-for-server-communication"></a>Controlos criptográficos para comunicações de servidor  
 O Configuration Manager utiliza os seguintes controlos criptográficos para comunicações de servidor.  

### <a name="server-communication-within-a-site"></a>Comunicações de servidor dentro de um site  
 Cada servidor de sistema de sites utiliza um certificado para transferir dados para outros sistemas de sites no mesmo site do Configuration Manager. Algumas funções de sistema do site também utilizam certificados para autenticação. Por exemplo, se instalar o ponto proxy de registo num servidor e o ponto de registo noutro servidor, eles podem autenticar-se entre si utilizando este certificado de identidade. Quando o Configuration Manager utiliza um certificado para esta comunicação, se existir um certificado PKI disponível que tenha capacidade de autenticação de servidor, o Configuration Manager utiliza-o automaticamente; caso contrário, o Configuration Manager gera um certificado autoassinado. Este certificado autoassinado tem capacidade de autenticação de servidor, utiliza SHA-256 e tem um comprimento de chave de 2048 bits. O Configuration Manager copia o certificado para o arquivo de pessoas fidedignas noutros servidores de sistema de sites que poderá ter de confiar no sistema de sites. Os sistemas de sites podem depois confiar um do outro utilizando estes certificados e PeerTrust.  

 Além deste certificado para cada servidor de sistema de sites, o Configuration Manager gera um certificado autoassinado para a maioria das funções de sistema de sites. Quando existe mais do que uma instância da função de sistema do site no mesmo site, elas partilham o mesmo certificado. Por exemplo, pode ter vários pontos de gestão ou vários pontos de registo no mesmo site. Este certificado autoassinado também utiliza SHA-256 e tem um comprimento de chave de 2048 bits. É também copiado para o Arquivo de Pessoas Fidedignas nos servidores de sistema do site que poderão necessitar de confiar nele. As seguintes funções de sistema do site geram este certificado:  

- Ponto de serviço Web do Catálogo de Aplicações  

- Ponto de site do Catálogo de Aplicações  

- Ponto de sincronização do Asset Intelligence  

- Ponto de registo de certificados  

- Ponto de Endpoint Protection  

- Ponto de inscrição  

- Ponto de estado de contingência  

- Ponto de gestão  

- Ponto de distribuição com multicast ativado  

- Ponto de serviço fora de banda  

- Ponto do Reporting Services  

- Ponto de atualização de Software  

- Ponto de Migração de Estado  

- Ponto de Validação do Estado de Funcionamento do Sistema  

- Conector do Microsoft Intune  

  Estes certificados são geridos automaticamente pelo Configuration Manager e, quando necessário, gerados automaticamente.  

  Configuration Manager também utiliza um certificado de autenticação de cliente para enviar mensagens de estado do ponto de distribuição para o ponto de gestão. Quando o ponto de gestão está configurado apenas para ligações de cliente HTTPS, é necessário utilizar um certificado PKI. Se o ponto de gestão aceita ligações HTTP, é possível utilizar um certificado PKI ou selecionar a opção para utilizar um certificado autoassinado que tenha capacidade de autenticação de cliente, utilize SHA-256 e tenha um comprimento de chave de 2048 bits.  

### <a name="server-communication-between-sites"></a>Comunicações de servidor entre sites  
 O Configuration Manager transfere dados entre sites através da replicação de base de dados e replicação de ficheiros. Para obter mais informações, consulte [comunicações entre pontos finais](/sccm/core/plan-design/hierarchy/communications-between-endpoints).  

 O Configuration Manager configura a replicação de base de dados entre sites automaticamente e utiliza certificados PKI que tenham a capacidade de autenticação de servidor se estes estiverem disponíveis; caso contrário, o Configuration Manager cria certificados autoassinados para autenticação de servidor. Em ambos os casos, a autenticação entre sites é estabelecida utilizando os certificados do Arquivo de Pessoas Fidedignas que utilize PeerTrust. Este arquivo de certificados é utilizado para garantir que apenas os computadores do SQL Server que são utilizados pela hierarquia do Configuration Manager participam na replicação de site a site. Enquanto os sites primários e o site de administração central podem replicar alterações à configuração de todos os sites na hierarquia, os sites secundários podem replicar alterações à configuração apenas do respetivo site principal.  

 Os servidores de site estabelecem comunicação site a site através da utilização de uma troca de chaves segura que ocorre automaticamente. O servidor de site remetente gera um hash e assina-o com a respetiva chave privada. O servidor de site recetor verifica a assinatura, utilizando a chave pública e compara o hash com um valor gerado localmente. Se coincidirem, o site recetor aceita os dados replicados. Se os valores não corresponderem, o Configuration Manager rejeita os dados de replicação.  

 Replicação de base de dados no Configuration Manager utiliza o SQL Server Service Broker para transferir dados entre sites utilizando os seguintes mecanismos:  

- Ligação SQL Server a SQL Server: Esta opção utiliza credenciais do Windows para autenticação de servidor e certificados autoassinados com 1024 bits para assinar e encriptar os dados utilizando Advanced Encryption Standard (AES). Se existirem certificados PKI com capacidade de autenticação de servidor disponíveis, serão utilizados. O certificado tem de estar localizado no arquivo Pessoal para o arquivo de certificados de Computador.  

- SQL Service Broker: Esta opção utiliza certificados autoassinados com 2048 bits para assinar e encriptar os dados utilizando Advanced Encryption Standard (AES). O certificado tem de estar localizado na base de dados mestre do SQL Server.  

  A replicação baseada em ficheiros utiliza o protocolo Bloco de Mensagem de Servidor (SMB) e utiliza SHA-256 para assinar estes dados que não estão encriptados mas não contêm dados confidenciais. Se pretende encriptar estes dados, pode usar IPsec e tem de implementar isso forma independente do Configuration Manager.  

##  <a name="cryptographic-controls-for-clients-that-use-https-communication-to-site-systems"></a>Controlos criptográficos para clientes que utilizam comunicações HTTPS para sistemas de sites  
 Quando as funções de sistema do site aceitam ligações de cliente, pode configurá-las para aceitarem ligações HTTPS e HTTP ou apenas ligações HTTPS. As funções de sistema do site que aceitam ligações a partir da Internet só aceitam ligações de cliente através de HTTPS.  

 As ligações de cliente através de HTTPS oferecem um nível mais elevado de segurança, integrando com uma infraestrutura de chaves públicas (PKI), para ajudar a proteger a comunicação cliente-servidor. No entanto, configurar ligações de cliente HTTPS sem conhecimentos abrangentes de planeamento, implementação e operações PKI poderia deixá-lo vulnerável. Por exemplo, se não proteger a AC raiz, as pessoas mal intencionadas poderão comprometer a confiança de toda a sua infraestrutura PKI. Não conseguir implementar e gerir os certificados PKI utilizando processos controlados e seguros poderá ter como resultado clientes não geridos que não recebem atualizações ou pacotes de software críticos.  

> [!IMPORTANT]  
>  Os certificados PKI que são utilizados na comunicação de cliente protegem a comunicação apenas entre o cliente e alguns sistemas de sites. Não protegem o canal de comunicação entre o servidor de site e os sistemas de sites ou entre servidores de site.  

### <a name="communication-that-is-unencrypted-when-clients-use-https-communication"></a>Comunicação sem encriptação quando os clientes utilizam comunicação HTTPS  
 Quando os clientes comunicam com sistemas de sites utilizando HTTPS, as comunicações são geralmente encriptadas através de SSL. No entanto, nas seguintes situações, os clientes comunicam com sistemas de sites sem utilizar a encriptação:  

- O cliente não consegue efetuar uma ligação HTTPS através da intranet e reverter para a utilização de HTTP quando os sistemas de sites permitem esta configuração  

- Comunicação para as seguintes funções de sistema do site:  

  -   O cliente envia mensagens de estado para o ponto de estado de contingência  

  -   O cliente envia pedidos PXE para um ponto de distribuição com PXE ativado  

  -   O cliente envia dados de notificação para um ponto de gestão  

  Os pontos do Reporting Services estão configurados para utilizar HTTP ou HTTPS independentemente do modo de comunicação do cliente.  

##  <a name="cryptographic-controls-for-clients-chat-use-http-communication-to-site-systems"></a>Controlos criptográficos para bate-papo dos clientes utilizam comunicações HTTP para sistemas de sites  
 Quando os clientes utilizam comunicações HTTP para funções de sistema de sites, podem utilizar certificados PKI para autenticação de cliente ou certificados autoassinados, que o Configuration Manager gera. Quando o Configuration Manager gera certificados autoassinados, eles têm um identificador de objeto personalizado para assinatura e encriptação e estes certificados são utilizados para identificar exclusivamente o cliente. Para todos os sistemas operativos suportados exceto o Windows Server 2003, estes certificados autoassinados utilizam SHA-256 e têm um comprimento de chave de 2048 bits. Para o Windows Server 2003, é utilizado SHA1 com um comprimento de chave de 1024 bits.  

### <a name="operating-system-deployment-and-self-signed-certificates"></a>Implementação do sistema operativo e certificados autoassinados  
 Quando utiliza o Configuration Manager para implementar sistemas operativos com certificados autoassinados, um computador cliente também tem de ter um certificado para comunicar com o ponto de gestão, mesmo se o computador estiver numa fase transitória, como o arranque a partir de sequência de tarefas suporte de dados ou um ponto de distribuição com PXE ativado. Para suportar este cenário para ligações de cliente HTTP, o Configuration Manager gera certificados autoassinados com um identificador de objeto personalizado para assinatura e encriptação e estes certificados são utilizados para identificar exclusivamente o cliente. Para todos os sistemas operativos suportados exceto o Windows Server 2003, estes certificados autoassinados utilizam SHA-256 e têm um comprimento de chave de 2048 bits. Para o Windows Server 2003, é utilizado SHA1 com um comprimento de chave de 1024 bits. Se estes certificados autoassinados forem comprometidos, para impedir a sua utilização por atacantes para representar clientes fidedignos, bloqueie os certificados no nó **Certificados** da área de trabalho **Administração** , nó **Segurança** .  

### <a name="client-and-server-authentication"></a>Autenticação de cliente e servidor  
 Quando os clientes ligam por HTTP, efetuam os pontos de gestão, utilizando qualquer um dos serviços de domínio do Active Directory ou utilizando a chave de raiz fidedigna do Configuration Manager. Os clientes não autenticam outras funções de sistema de sites, como pontos de migração de estado ou pontos de atualização de software.  

 Quando um ponto de gestão autentica pela primeira vez um cliente utilizando o certificado de cliente autoassinado, este mecanismo fornece uma segurança mínima porque qualquer computador pode gerar um certificado autoassinado. Neste cenário, o processo de identificação de clientes tem de ser aumentado mediante aprovação. Apenas a computadores fidedignos devem ser aprovados, o automaticamente pelo Configuration Manager, ou manualmente, por um utilizador administrativo. Para obter mais informações, consulte a secção de aprovação [comunicações entre pontos finais](/sccm/core/plan-design/hierarchy/communications-between-endpoints).  

## <a name="about-ssl-vulnerabilities"></a>Acerca de vulnerabilidades SSL
Para melhorar a segurança dos seus servidores e clientes do Configuration Manager, faça o seguinte:

-   Ativar o TLS 1.2

    Para ativar o TLS 1.2 para o Configuration Manager, consulte o seguinte artigo da KB: [Como ativar o TLS 1.2 para o Configuration Manager](https://support.microsoft.com/en-us/help/4040243/how-to-enable-tls-1-2-for-configuration-manager).
-   Desativar o SSL 3.0, TLS 1.0 e TLS 1.1 
-   Reordenar os conjuntos de cifras TLS relacionados 

Para obter mais informações, consulte [como restringir a utilização de determinados algoritmos criptográficos e protocolos no Schannel](https://support.microsoft.com/en-us/kb/245030/) e [dar prioridade aos conjuntos de cifras de Schannel](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx). Estes procedimentos não afetam a funcionalidade do Configuration Manager.


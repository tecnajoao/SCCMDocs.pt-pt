---
title: Parâmetros de instalação de cliente e as propriedades
titleSuffix: Configuration Manager
description: Saiba mais sobre os parâmetros da linha de comandos ccmsetup e as propriedades para instalar o cliente do Configuration Manager.
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 735a8da57c0225aee533568eb997dc82d9816d6b
ms.sourcegitcommit: db6074317d5c68ebb5fc478be5bceeb441aa0737
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/17/2018
---
# <a name="about-client-installation-parameters-and-properties-in-system-center-configuration-manager"></a>Sobre os parâmetros de instalação de cliente e propriedades no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize o comando CCMSetup.exe para instalar o cliente do Configuration Manager. Se fornecer cliente parâmetros de instalação na linha de comandos, se modificar o comportamento de instalação. Se fornecer cliente propriedades de instalação na linha de comandos, se modificar a configuração inicial do agente cliente instalado.



##  <a name="aboutCCMSetup"></a> Acerca do CCMSetup.exe  
 O comando CCMSetup.exe transfere os ficheiros necessários para instalar o cliente a partir de um ponto de gestão ou para uma localização de origem. Esses ficheiros poderão incluir:  

-   O Windows Installer pacote client.msi que instala o software de cliente.  

-   Ficheiros de instalação da Microsoft em segundo plano inteligente serviço de transferência (BITS).  

-   Ficheiros de instalação do Windows Installer.  

-   Atualizações e correções do cliente do Configuration Manager.  

> [!NOTE]  
>  No Configuration Manager, não é possível executar o ficheiro Client.msi diretamente.  

 CCMSetup.exe fornece [parâmetros da linha de comandos](#ccmsetup-exe-command-line-parameters) para personalizar a instalação - parâmetros têm o prefixo com uma barra invertida e por convenção são minúsculas. Especifique o valor de um parâmetro quando é necessário utilizar ponto e vírgula seguido imediatamente pelo valor pretendido. Pode também fornecer propriedades para modificar o comportamento do client.msi na linha de comandos de CCMSetup.exe – propriedades por convenção são em todas as maiúsculas. Especifique um valor para uma propriedade com um sinal de igual seguido imediatamente pelo valor pretendido.  

> [!IMPORTANT]  
>  Especifique os parâmetros CCMSetup antes de especificar as propriedades de client.msi.  

 CCMSetup.exe e os ficheiros de suporte estão localizados no servidor do site no **cliente** pasta da pasta de instalação do Configuration Manager. Esta pasta é partilhada na rede como  **&lt;nome do servidor de Site\>\SMS_&lt;código do Site\>\Client**.  

 Na linha de comandos, o comando CCMSetup.exe utiliza o seguinte formato:  

 `CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

 Por exemplo:  

   `CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

 Este exemplo faz as seguintes ações:  

-   Especifica o ponto de gestão com o nome SMSMP01 para solicitar uma lista de pontos de distribuição para transferir os ficheiros de instalação de cliente.  

-   Especifica que instalação deverá ser interrompida se já existir uma versão do cliente no computador.  

-   Indica ao client.msi que atribua o código de site S01 ao cliente.  

-   Indica ao client.msi que utilize o ponto de estado de contingência com o nome SMSFP01.  

> [!NOTE]  
>  Se um valor de parâmetro tiver espaços, coloque-o entre aspas.  


> [!IMPORTANT]  
>  Caso tenha expandido o esquema do Active Directory para o Configuration Manager, o site publica muitas propriedades de instalação de cliente nos serviços de domínio do Active Directory. O cliente do Configuration Manager lê automaticamente estas propriedades. Para obter mais informações, consulte [acerca das propriedades de instalação de cliente publicadas nos serviços de domínio do Active Directory](about-client-installation-properties-published-to-active-directory-domain-services.md)  



##  <a name="ccmsetupexe-command-line-parameters"></a>Parâmetros da linha de comandos do CCMSetup.exe  

### <a name=""></a>/?  

Abre o **CCMSetup** caixa de diálogo que mostra os parâmetros da linha de comandos do ccmsetup.exe.  

Exemplo: **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/Source:&lt;caminho\>  

 Especifica a localização de transferência de ficheiros. Utilize uma localização ou caminho UNC. Os ficheiros são transferidos utilizando o protocolo de bloco (SMB) de mensagem de servidor. Para utilizar **/origem**, a conta de utilizador do Windows para a instalação do cliente tem de ter permissões de leitura para a localização.

> [!NOTE]  
>  Pode utilizar o **/origem** parâmetro mais do que uma vez numa linha de comandos para especificar alternativa transferir localizações.  

 Example: **ccmsetup.exe /source:"\\\computer\folder"**  

### <a name="mpltserver"></a>/MP:&lt;servidor\>

 Especifica um origem ponto de gestão de computadores estabelecerem ligação ao. Computadores utilizam este ponto de gestão para localizar o ponto de distribuição mais próximo para os ficheiros de instalação. Se existirem pontos de distribuição ou computadores não é possível transferir os ficheiros a partir dos pontos de distribuição depois de quatro horas, transferem os ficheiros do ponto de gestão especificado.  

> [!IMPORTANT]  
>  Este parâmetro é utilizado para especificar um ponto de gestão inicial para os computadores para localizar uma origem da transferência e pode ser qualquer ponto de gestão em qualquer site. Não *atribuir* o cliente para um ponto de gestão.   

 Os computadores transferem os ficheiros através de uma ligação HTTP ou HTTPS, conforme a configuração da função do sistema de sites para ligações de cliente. Se configurado, a transferência utilizará limitação BITS. Se todos os pontos de distribuição e pontos de gestão estiverem configurados cliente apenas para ligações HTTPS, certifique-se de que o computador cliente tem um certificado de cliente válido.  

Pode utilizar o **/mp** parâmetro da linha de comandos para especificar mais do que um ponto de gestão. Se o computador falhar a ligação ao primeiro, tentará o seguinte na lista especificado. Se especificar vários pontos de gestão, separe os valores por ponto e vírgula.

Se o cliente se liga a um ponto de gestão através de HTTPS, normalmente, tem de especificar o FQDN, não o nome do computador. O valor tem de corresponder ao certificado PKI do requerente ou nome alternativo do requerente do ponto de gestão. Apesar do Configuration Manager suporta a utilizar um nome de computador no certificado para ligações na intranet, é recomendado utilizar um FQDN.

Exemplo ao utilizar o nome do computador: `ccmsetup.exe /mp:SMSMP01`  

Exemplo ao utilizar o FQDN: `ccmsetup.exe /mp:smsmp01.contoso.com`  

Este parâmetro pode especificar o URL de um gateway de gestão de nuvem. Utilize este URL para instalar o cliente num dispositivo baseado na internet. Para obter o valor para este parâmetro, utilize os seguintes passos:
- Crie um gateway de gestão de nuvem.
- Um cliente do Active Directory, abra uma linha de comandos do Windows PowerShell como administrador. 
- Execute o seguinte comando: `(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
- Acrescente o prefixo "https://" para utilizar com o **/mp** parâmetro.

Exemplo ao utilizar o URL de gateway de gestão de nuvem: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

 > [!Important]
 > Quando especificar o URL de um gateway de gestão de nuvem para o **/mp** parâmetro, tem de começar com **https://**.


### <a name="retryltminutes"></a>/retry:&lt;minutos\>

O intervalo entre tentativas se o CCMSetup.exe não conseguir transferir ficheiros de instalação. CCMSetup continuará a tentar até atingir o limite especificado no **downloadtimeout** parâmetro.  

Exemplo: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Impede o CCMSetup de ser executado como um serviço, o que é a predefinição. Quando o CCMSetup é executado como um serviço, é executada no contexto da conta do sistema Local do computador. Esta conta poderá não ter direitos suficientes para aceder a recursos de rede necessária para a instalação. Com **/noservice**, CCMSetup.exe é executado no contexto da conta de utilizador que utilizar para iniciar a instalação. Além disso, se estiver a utilizar um script para executar o CCMSetup.exe com a **/service** parâmetro, o CCMSetup.exe terminará após o serviço é iniciado e não pode reportar corretamente os detalhes da instalação.   

Exemplo: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

Especifica que o CCMSetup deverá ser executado como um serviço que utiliza a conta do sistema local.  

Exemplo: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Especifica que o software de cliente deverá ser desinstalado. Para obter mais informações, consulte [como gerir clientes](../manage/manage-clients.md).  

Exemplo: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

Se já estiver instalada qualquer versão do cliente, este parâmetro especifica que a instalação do cliente deverá ser interrompida.  

Exemplo: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

 Especifica que o CCMSetup deverá forçar o computador cliente para reiniciar se for necessário para concluir a instalação. Se este parâmetro não está especificado, o CCMSetup terminará quando for necessário um reinício. Em seguida, continua após o próximo reinício manual.  

 Exemplo: `CCMSetup.exe /forcereboot`  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;Priority\>

 Especifica a prioridade de transferência quando os ficheiros de instalação do cliente são transferidos através de uma ligação HTTP. Os valores possíveis são:  

-   FOREGROUND  

-   HIGH  

-   NORMAL  

-   LOW  

 O valor predefinido é NORMAL.  

 Exemplo: `ccmsetup.exe /BITSPriority:HIGH`  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;minutos\>

O período de tempo em minutos que o CCMSetup tentará transferir os ficheiros de instalação antes da paragem. O valor predefinido é **1440** minutos (dia).  

Exemplo: `ccmsetup.exe /downloadtimeout:100`  

### <a name="usepkicert"></a>/UsePKICert

Quando especificado, o cliente utiliza um certificado PKI que incluem autenticação de cliente, se disponível. Se o cliente não é possível localizar um certificado válido, utiliza uma ligação HTTP com um certificado autoassinado. Este comportamento é o mesmo quando não utilizar este parâmetro.

> [!NOTE]  
>  Em alguns cenários, não tem de especificar este parâmetro, quando estiverem a instalar um cliente e continuar a utilizar um certificado de cliente. Estes cenários incluem a instalação do cliente utilizando push de cliente e a instalação de cliente baseada em pontos de atualização de software. No entanto, terá de especificar este parâmetro se manualmente de instala um cliente e utilizar o **/mp** parâmetro para especificar um ponto de gestão que está configurado para aceitar apenas ligações de cliente HTTPS. Também tem de especificar este parâmetro quando instala um cliente para comunicação apenas de internet. Utilize o CCMALWAYSINF = 1 propriedade em conjunto com as propriedades para o ponto de gestão baseado na internet (CCMHOSTNAME) e o código do site (SMSSITECODE). Para obter mais informações sobre a gestão de clientes baseada na internet, consulte [considerações sobre comunicações do cliente da internet ou numa floresta não fidedigna](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

 Exemplo: `CCMSetup.exe /UsePKICert`  

### <a name="nocrlcheck"></a>/NoCRLCheck

 Especifica que um cliente não deve verificar a lista de revogação de certificados (CRL) quando comunica por HTTPS com um certificado PKI.  

 Quando não especificado, o cliente verifica a CRL antes de estabelecer uma ligação HTTPS.  

 Para obter mais informações sobre a verificação de CRL cliente, consulte [planear a revogação de certificados PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).  

 Exemplo: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="configltconfiguration-file"></a>/config:&lt;ficheiro de configuração\>

Especifica o nome de um ficheiro de texto que apresenta uma lista de propriedades de instalação de cliente.

- Se não especificar o **/noservice** parâmetro do CCMSetup, este ficheiro tem de estar localizado na pasta CCMSetup, que é % Windir %\\Ccmsetup sistemas operativos de 32 bits e 64 bits.
- Se especificar o **/noservice** parâmetro, este ficheiro tem de estar localizado na mesma pasta a partir do qual o CCMSetup.exe é executado.  

Exemplo: `CCMSetup.exe /config:&lt;Configuration File Name.txt\>`  

Para fornecer o formato de ficheiro corretos, utilize o ficheiro mobileclienttemplate.tcf no &lt;diretório do Configuration Manager\>\\bin\\&lt;plataforma\> pasta no servidor do site. Este ficheiro tem também comentários sobre as secções e como são utilizados. Especifique as propriedades de instalação de cliente na secção [instalação do cliente], após o seguinte texto: **Install=INSTALL=ALL**.  

Entrada da secção [instalação do cliente] de exemplo: `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;filename\>

 Especifica que o CCMSetup.exe não deverá instalar o programa de pré-requisitos especificado ao instalar o cliente do Configuration Manager. Este parâmetro suporta a introdução de mais do que um valor. Utilize o caráter de ponto e vírgula (;) para separar os valores.  


 Exemplos: `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe` ou `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`  

### <a name="forceinstall"></a>/forceinstall

 Especifique que o CCMSetup.exe desinstala qualquer cliente existente e instala um novo cliente.  

### <a name="excludefeaturesltfeature"></a>/ExcludeFeatures:&lt;feature\>

Especifica que o CCMSetup.exe não instalar a funcionalidade especificada quando instala o cliente.  

Exemplo: `CCMSetup.exe /ExcludeFeatures:ClientUI` não instala o Centro de Software no cliente.  

> [!NOTE]  
>  **ClientUI** é o único valor suportado com o **/ExcludeFeatures** parâmetro.  



##  <a name="ccmsetupReturnCodes"></a> Códigos de retorno CCMSetup.exe  
 O comando CCMSetup.exe fornece que os seguintes códigos concluídos de retorno. Para resolver, consulte o ficheiro ccmsetup.log no computador cliente para o contexto e os detalhes adicionais sobre códigos de retorno.  

|Código de retorno|Significado|  
|-----------------|-------------|  
|0|Êxito|  
|6|Erro|  
|7|Reinício necessário|  
|8|Programa de configuração já em execução|  
|9|Falha de avaliação de pré-requisitos|  
|10|Falha de validação de hash do manifesto de configuração|  



## <a name="ccmsetupMsiProps"></a> Propriedades de Ccmsetup.msi  
 As seguintes propriedades, podem modificar o comportamento de instalação de ccmsetup.msi.

### <a name="ccmsetupcmd"></a>CCMSETUPCMD 

Especifica os parâmetros da linha de comandos e as propriedades que são transmitidas para ccmsetup.exe depois de ser instalado por ccmsetup.msi. Inclua outras propriedades dentro de aspas. Utilize esta propriedade quando bootstrapping cliente do Configuration Manager utilizando o método de instalação de MDM do Intune. 

Exemplo: `ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

 > [!Tip]
 > Microsoft Intune limita a linha de comandos a 1024 carateres. 



##  <a name="clientMsiProps"></a> Propriedades de Client.msi  
 As seguintes propriedades podem modificar o comportamento de instalação de client.msi. Se utilizar o método de instalação push do cliente, também pode especificar as propriedades no separador **Cliente** da caixa de diálogo **Propriedades da Instalação Push do Cliente** .  


### <a name="aadclientappid"></a>AADCLIENTAPPID

Especifica o identificador de aplicação de cliente do Azure Active Directory (Azure AD). A aplicação de cliente é criada ou importado quando [configurar os serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para gestão de nuvem. Um administrador do Azure pode obter o valor para esta propriedade do portal do Azure. Para obter mais informações, consulte [obter ID da aplicação](/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key). Para o **AADCLIENTAPPID** propriedade, este ID de aplicação é para o tipo de aplicação "Nativas".

Exemplo: `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`


### <a name="aadresourceuri"></a>AADRESOURCEURI

Especifica o identificador de aplicação de servidor do Azure AD. A aplicação de servidor é criada ou importado quando [configurar os serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para gestão de nuvem. Ao criar a aplicação de servidor, na caixa de diálogo Criar aplicação de servidor, esta propriedade é o **URI de ID de aplicação**.

Um administrador do Azure pode obter o valor para esta propriedade do portal do Azure. No **do Azure Active Directory** painel, localize a aplicação de servidor em **registos de aplicação**. Esta aplicação é de "aplicação Web / API" tipo de aplicação. Abra a aplicação, clique em **definições**e, em seguida, **propriedades**. Utilize o **URI de ID de aplicação** valor para esta propriedade de instalação de cliente AADRESOURCEURI.

Exemplo: `ccmsetup.exe AADRESOURCEURI=https://contososerver`


### <a name="aadtenantid"></a>AADTENANTID

Especifica o identificador de inquilino do Azure AD. Este inquilino está ligado ao Configuration Manager quando tiver [configurar os serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para gestão de nuvem. Para obter o valor para esta propriedade, utilize os seguintes passos:
- Num dispositivo Windows 10 que está associado ao mesmo inquilino do Azure AD, abra uma linha de comandos.
- Execute o seguinte comando: `dsregcmd.exe /status`
- A secção de estado do dispositivo, localize o **TenantId** valor. Por exemplo, `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

 > [!Note]
 > Um administrador do Azure também pode obter este valor no portal do Azure. Para obter mais informações, consulte [obter ID de inquilino](/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-tenant-id)

Exemplo: `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

Especifica uma ou mais contas ou grupos de utilizadores do Windows a que deve ser dado acesso a definições e políticas de cliente. Esta propriedade é útil em que o administrador do Configuration Manager não tem credenciais administrativas locais no computador cliente. Especifique uma lista de contas que são separados por ponto e vírgula.  

Exemplo: `CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"`  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Especifica que o computador está autorizado a reiniciar após a instalação do cliente, se necessário.  

> [!IMPORTANT]  
>  O computador é reiniciado sem aviso, mesmo se um utilizador tiver sessão iniciado.  

Exemplo: **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 Definido como **1** para especificar que o cliente é baseado na internet e nunca se liga à intranet. O tipo de ligação do cliente apresenta **Sempre Internet**.  

 Utilize esta propriedade em conjunto com CCMHOSTNAME, que especifica o FQDN do ponto de gestão baseado na internet. Também utilizá-lo com /UsePKICert de parâmetro CCMSetup e com o código do site.  

 Para obter mais informações sobre a gestão de clientes baseada na internet, consulte [considerações sobre comunicações do cliente da internet ou numa floresta não fidedigna](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

 Exemplo: `CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 Especifica a lista de emissores de certificados, o que é uma lista de certificados de certificação (AC) de raiz fidedigna que confie do site do Configuration Manager.  

 Para obter mais informações sobre a lista de emissores de certificados e como os clientes a utilizam durante o processo de seleção de certificados, consulte [planear a seleção de certificado de cliente PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

 Este valor é uma correspondência de maiúsculas e minúsculas para os atributos do assunto no certificado da AC de raiz. Os atributos podem ser separados por uma vírgula (,) ou ponto e vírgula (;). Especificar mais do que um certificados de AC de raiz utilizando uma barra separadora. Exemplo:  

 `CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &#124; CN=Litware Corporate Root CA; O=Litware, Inc.”`  

> [!TIP]  
>  Para copiar o **CertificateIssuers =&lt;cadeia\>**  para o site, referência ao ficheiro mobileclient.tcf no &lt;diretório do Configuration Manager\>\bin\\ &lt;plataforma\> pasta no servidor do site.  

### <a name="ccmcertsel"></a>CCMCERTSEL

 Especifica os critérios de seleção de certificados se o cliente tiver mais de um certificado para comunicação por HTTPS. Este certificado é um certificado válido que inclua a capacidade de autenticação de cliente.  

 Pode procurar uma correspondência exata (utilizar **requerente:**) ou uma correspondência parcial (utilize **SubjectStr:)** no nome do requerente ou nome alternativo do requerente. Exemplos:  

 `CCMCERTSEL="Subject:computer1.contoso.com"` procura um certificado com uma correspondência exata com o nome de computador "COMPUTADOR1.contoso.com" no nome do requerente ou nome alternativo do requerente.  

 `CCMCERTSEL="SubjectStr:contoso.com"` procura um certificado que contenha "contoso.com" no nome do requerente ou nome alternativo do requerente.  

 Também é possível utilizar o Identificador de Objeto (OID) ou os atributos de nome distinto nos atributos do Nome do Requerente ou do Nome Alternativo do Requerente. Por exemplo:  

 `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"` procura o atributo de unidade organizacional expresso como um identificador de objeto e denominado computadores.  

 `CCMCERTSEL="SubjectAttr:OU = Computers"` procura o atributo de unidade organizacional expresso como um nome distinto e denominado computadores.  

> [!IMPORTANT]  
>  Se utilizar a caixa de nome do requerente, o **requerente:** diferencia maiúsculas de minúsculas e o **SubjectStr:** sensível.  
>   
>  Se utilizar a caixa Nome alternativo do requerente, o **requerente:** e **SubjectStr:** são sensível.  

 A lista completa de atributos que pode utilizar para a seleção de certificados está listada no [valores de atributo suportados para os critérios de seleção de certificado PKI](#BKMK_attributevalues).  

 Se mais do que um certificado corresponder à procura e a propriedade CCMFIRSTCERT tiver sido definida como 1, será selecionado o certificado com o período de validade mais longo.  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 Especifica um nome de arquivo de certificado alternativo, se o certificado de cliente HTTPS não se encontra localizado no arquivo de certificados predefinido **pessoais** no arquivo do computador.  

 Exemplo: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  Ativa o registo de depuração. Valores podem ser definidos como 0 (desativado, predefinição) ou 1 (ativado). Esta propriedade faz com que o cliente registe informações de baixo nível para resolução de problemas. Como melhor prática, evite utilizar esta propriedade em sites de produção. Um registo excessivo pode ocorrer, o que poderá tornar mais difícil a localização informações relevantes nos ficheiros de registo. Também defina CCMENABLELOGGING para verdadeiro para ativar o registo de depuração.  

  Exemplo: `CCMSetup.exe CCMDEBUGLOGGING=1`  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  Por predefinição, esta propriedade está definida como TRUE para ativar o registo. Os ficheiros de registo são armazenados no **registos** pasta na pasta de instalação de cliente do Configuration Manager. Por predefinição, esta pasta é %Windir%\CCM\Logs.  

  Exemplo: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 A frequência que cliente executa a ferramenta de avaliação do Estado de funcionamento (ccmeval.exe). Pode ser **1** para **1440** minutos. Por predefinição, é executada uma vez por dia.  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 A hora quando a ferramenta de avaliação de estado de funcionamento do cliente (ccmeval.exe) é executado, entre **0** (meia-noite) e **23** (23: 00). É executada à meia-noite, por predefinição.  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 Se estiver definida como 1, esta propriedade especifica que o cliente deve selecionar o certificado PKI com o período de validade mais longo. Esta definição poderá ser necessária se estiver a utilizar a proteção de acesso de rede com imposição de IPsec.  

 Exemplo: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`  


### <a name="ccmhostname"></a>CCMHOSTNAME

 Se o cliente for gerido através da internet, esta propriedade especifica o FQDN do ponto de gestão baseado na internet.  

 Não especifique esta opção com a propriedade de instalação SMSSITECODE = AUTO. Os clientes baseados na Internet devem ser atribuídos diretamente para o respetivo site baseado na internet.  

 Exemplo: `CCMSetup.exe  /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

Esta propriedade pode especificar o endereço de um gateway de gestão de nuvem. Para obter o valor para esta propriedade, utilize os seguintes passos:
- Crie um gateway de gestão de nuvem.
- Um cliente do Active Directory, abra uma linha de comandos do Windows PowerShell como administrador. 
- Execute o seguinte comando: `(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
- Utilize o valor devolvido como-é com o **CCMHOSTNAME** propriedade.

Por exemplo: `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

 > [!Important]
 > Quando especificar o endereço de um gateway de gestão de nuvem para o **CCMHOSTNAME** propriedade, fazer *não* acrescentar como um prefixo **https://**. Este prefixo é utilizado apenas com o **/mp** URL de um gateway de gestão de nuvem.



### <a name="ccmhttpport"></a>CCMHTTPPORT

 Especifica a porta que o cliente deve utilizar quando comunicar por HTTP com servidores do sistema de sites. Defina a porta 80 por predefinição.  

 Exemplo: `CCMSetup.exe CCMHTTPPORT=80`  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Especifica a porta que o cliente deve utilizar quando comunicar por HTTPS com servidores do sistema de sites. Defina a porta 443 por predefinição.  

Exemplo: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 Identifica a pasta onde estão instalados os ficheiros de cliente do Configuration Manager, *% Windir %* \ccm. por predefinição. Independentemente de onde estes ficheiros são instalados, o ficheiro Ccmcore.dll é sempre instalado no *%Windir%\System32* pasta. Além disso, num sistema operativo de 64 bits, uma cópia do ficheiro Ccmcore.dll é sempre instalada no *% Windir %* \SysWOW64 pasta. Este ficheiro suporta aplicações de 32 bits que utilizem a versão de 32 bits das APIs do SDK do Configuration Manager de cliente.  

 Exemplo: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Especifica o nível de detalhes a escrever nos ficheiros de registo do Configuration Manager. Especifique um número inteiro entre 0 e 3, em que 0 é o registo mais verboso e 3 regista apenas erros. A predefinição é 1.  

Exemplo: `CCMSetup.exe CCMLOGLEVEL=3`  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Quando um ficheiro de registo do Configuration Manager atinge o tamanho máximo, o cliente muda o nome de cópia de segurança e cria um novo ficheiro de registo. O tamanho máximo é 250 000 bytes por predefinição, ou o valor especificado pela propriedade CCMLOGMAXSIZE.

Esta propriedade especifica quantos versões anteriores do ficheiro de registo a manter. O valor predefinido é 1. Se o valor for definido como 0, não serão guardados ficheiros de registo antigos.  

Exemplo: `CCMSetup.exe CCMLOGMAXHISTORY=0`  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

O tamanho de ficheiro de registo máximo em bytes. Quando um registo aumenta o tamanho especificado, o cliente muda o nome como um ficheiro de histórico e cria um novo ficheiro. Esta propriedade tem de ser definida para, pelo menos, 10 000 bytes. O valor predefinido é 250.000 bytes.  

Exemplo: `CCMSetup.exe CCMLOGMAXSIZE=300000`  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 Se definido em TRUE, esta propriedade desativa a capacidade dos utilizadores administrativos de alterar o site atribuído no **do Configuration Manager** painel de controlo.  

 Exemplo: **CCMSetup.exe DISABLESITEOPT = TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Se definido em TRUE, esta propriedade desativa a capacidade dos utilizadores administrativos de alterar as definições de pasta de cache do cliente no **do Configuration Manager** painel de controlo.  

Exemplo: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

 Especifica um domínio de DNS para os clientes localizarem pontos de gestão que sejam publicados no DNS. Quando um ponto de gestão é localizado, informa o cliente sobre outros pontos de gestão na hierarquia. Este comportamento significa que o ponto de gestão localizado utilizando a publicação de DNS não tem de ser do site do cliente, mas pode ser qualquer ponto de gestão na hierarquia.  

> [!NOTE]  
>  Não tem de especificar esta propriedade se o cliente estiver no mesmo domínio que um ponto de gestão publicado. Nesse caso, o domínio do cliente é automaticamente utilizado para procurar o DNS para pontos de gestão.  

 Para obter mais informações sobre a publicação de DNS como método de localização de serviço para clientes do Configuration Manager, consulte [localização e a forma como os clientes determinam o respetivo ponto de gestão atribuído Service](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).  

> [!NOTE]  
>  Por predefinição, a publicação de DNS não está ativada no Configuration Manager.  

 Exemplo: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`  

### <a name="fsp"></a>FSP

Especifica o ponto de estado de contingência que recebe e processa mensagens de estado enviadas por computadores cliente do Configuration Manager.  

Para obter mais informações sobre o ponto de estado de contingência, consulte [determinar se necessita de um ponto de estado de contingência](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point).  

Exemplo: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 Especifica que a presença de versão mínima necessária do Microsoft Application Virtualization (App-V) não é verificada antes do cliente está instalado.  

> [!IMPORTANT]  
>  Se instalar o cliente do Configuration Manager sem instalar o App-V, não é possível implementar aplicações virtuais.  

 Exemplo: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`  

### <a name="notifyonly"></a>NOTIFYONLY

Especifica que o cliente de relatórios de estado, mas não remediará problemas que encontra.  

Exemplo: `CCMSetup.exe NOTIFYONLY=TRUE`  

Para obter mais informações, consulte [como configurar o estado do cliente](configure-client-status.md).  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 Se um cliente tiver a chave de raiz fidedigna do Configuration Manager incorreta e não é possível contactar um ponto de gestão fidedigno para receber a nova chave de raiz fidedigna, utilize esta propriedade para remover manualmente a chave de raiz fidedigna antiga. Esta situação pode ocorrer quando move um cliente a partir de uma hierarquia de sites para outro. Esta propriedade aplica-se a clientes que utilizam a comunicação de cliente por HTTP e HTTPS.  

 Exemplo: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Permite a reatribuição de site automática para atualizações de cliente quando utilizado com [SMSSITECODE](#smssitecode)= AUTO.

Exemplo: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Especifica a localização da pasta de cache do cliente no computador cliente, que armazena ficheiros temporários. Por predefinição, a localização é *%Windir%\ccmcache*.  

Exemplo: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Esta propriedade pode ser utilizada em conjunto com a propriedade SMSCACHEFLAGS para controlar a localização de pasta de cache do cliente.  

Exemplo: `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE` instala a pasta de cache do cliente na maior unidade de disco de clientes disponíveis.  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Especifica mais detalhes de instalação para a pasta de cache do cliente. Pode utilizar as propriedades SMSCACHEFLAGS individualmente ou em combinação, separadas por ponto e vírgula. Se esta propriedade não está especificada, a pasta de cache do cliente é instalada, de acordo com a propriedade SMSCACHEDIR, a pasta não comprimida e o valor SMSCACHESIZE é utilizado como tamanho em MB da pasta.  

Esta definição é ignorada quando atualiza um cliente existente.  

Propriedades:  

-   PERCENTDISKSPACE: Especifica o tamanho da pasta como uma percentagem do espaço total do disco. Se especificar esta propriedade, terá de especificar também a propriedade SMSCACHESIZE como o valor percentual a utilizar.  

-   PERCENTFREEDISKSPACE: Especifica o tamanho da pasta como uma percentagem de espaço livre em disco. Se especificar esta propriedade, terá de especificar também a propriedade SMSCACHESIZE como o valor percentual a utilizar. Por exemplo, se o disco tiver 10 MB de espaço livre e SMSCACHESIZE for especificada como 50, o tamanho da pasta será definido como 5 MB. Não é possível utilizar esta propriedade com a propriedade PERCENTDISKSPACE.  

-   MAXDRIVE: Especifica que a pasta deve ser instalada no maior disco disponível. Este valor é ignorado se tiver sido especificado um caminho com a propriedade SMSCACHEDIR.  

-   MAXDRIVESPACE: Especifica que a pasta deve ser instalada na unidade de disco que tem mais espaço livre. Este valor é ignorado se tiver sido especificado um caminho com a propriedade SMSCACHEDIR.  

-   NTFSONLY: Especifica que a pasta pode ser instalada apenas em unidades de disco NTFS. Este valor é ignorado se tiver sido especificado um caminho com a propriedade SMSCACHEDIR.  

-   COMPRESS: Especifica que a pasta deve ser armazenada num formato comprimido.  

-   FAILIFNOSPACE: Especifica que o software de cliente deve ser removido se não existir espaço suficiente para instalar a pasta.  

Exemplo: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`  


### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> Definições de cliente estão disponíveis para especificar o tamanho da pasta de cache de cliente. A adição dessas definições de cliente substitui eficazmente a utilização de SMSCACHESIZE como uma propriedade de client.msi para especificar o tamanho da cache do cliente. Para obter mais informações, veja as [definições do cliente para tamanho da cache](about-client-settings.md#client-cache-settings).  

<!-- For 1602 and earlier, SMSCACHESIZE specifies the size of the client cache folder in megabyte (MB) or as a percentage when used with the PERCENTDISKSPACE or PERCENTFREEDISKSPACE property. If this property isn't set, the folder defaults to a maximum size of 5120 MB. The lowest value that you can specify is 1 MB.  -->

> [!NOTE]  
>  Se um novo pacote que tem de ser transferido faria com que a pasta ultrapasse o tamanho máximo, e não é possível limpar a pasta para disponibilizar espaço suficiente, a transferência do pacote falhará e o programa ou aplicação não é executado.  

Esta definição é ignorada quando atualiza um cliente existente e quando o cliente transfere as atualizações de software.  

Exemplo: `CCMSetup.exe SMSCACHESIZE=100`  

> [!NOTE]  
>  Se reinstalar um cliente, não é possível utilizar as propriedades de instalação SMSCACHESIZE ou SMSCACHEFLAGS para definir o tamanho da cache seja menor do que tinha anteriormente. Se tentar efetuar esta ação, o valor será ignorado. O tamanho da cache é automaticamente definido para o tamanho de anterior.  

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Especifica a localização e a ordem em que o programa de instalação do Configuration Manager verifica a existência de definições de configuração. A propriedade é uma cadeia de um ou mais carateres, definindo cada uma origem de configuração específicos. Utilize os valores de caráter R, P, M e U, isoladamente ou:  

-   R: Verifique a existência de definições de configuração no registo.  

   Para obter mais informações, consulte [informações sobre como armazenar propriedades de instalação de cliente no registo](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

-   P: Verifique a existência de definições de configuração nas propriedades de instalação fornecidas na linha de comandos.  

-   M: Verificar a existência de definições ao atualizar um cliente antigo com o software de cliente do Configuration Manager.  

-   U: Atualizar o cliente instalado para uma versão mais recente (e utilizar o código de site atribuído).  

 Por predefinição, a instalação do cliente utiliza `PU` para verificar primeiro as propriedades de instalação e, em seguida, as definições existentes.  

 Exemplo: `CCMSetup.exe SMSCONFIGSOURCE=RP`  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 Especifica se o cliente pode utilizar o WINS (Windows Internet Name Service) para localizar um ponto de gestão que aceite ligações HTTP. Os clientes utilizam este método quando não é possível encontrar um ponto de gestão nos serviços de domínio do Active Directory ou no DNS.  

 Esta propriedade não afeta se o cliente utilizar WINS para resolução de nomes.  

 Pode configurar dois modos diferentes para esta propriedade:  

-   NOWINS: Este valor é a definição mais segura para esta propriedade e impede os clientes de localizar um ponto de gestão no WINS. Quando utilizar esta definição, os clientes têm de ter um método alternativo para localizar um ponto de gestão na intranet, como os Serviços de Domínio do Active Directory ou a Publicação de DNS.  

-   WINSSECURE (predefinição): Neste modo, um cliente que utilize comunicações HTTP pode utilizar o WINS para localizar um ponto de gestão. No entanto, o cliente tem de ter uma cópia da chave de raiz fidedigna para poder ligar com êxito ao ponto de gestão. Para obter mais informações, consulte [planeamento para a chave de raiz fidedigna](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  


 Exemplo: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

Especifica um ponto de gestão inicial para o cliente do Configuration Manager para utilizar.  

> [!IMPORTANT]  
>  Se o ponto de gestão apenas aceita ligações de cliente através de HTTPS, terá de preceder o nome de ponto de gestão com https://.  

Exemplo: `CCMSetup.exe SMSMP=smsmp01.contoso.com`

Exemplo: `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  


### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 Especifica a chave de raiz fidedigna do Configuration Manager quando não é possível obter a partir de serviços de domínio do Active Directory. Esta propriedade aplica-se a clientes que utilizam a comunicação de cliente por HTTP e HTTPS. Para obter mais informações, consulte [planeamento para a chave de raiz fidedigna](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 Exemplo: `CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>`  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 Utilizada para reinstalar a chave de raiz fidedigna do Configuration Manager. Especifica o nome e o caminho completo de um ficheiro que contém a chave de raiz fidedigna. Esta propriedade aplica-se a clientes que utilizam a comunicação de cliente por HTTP e HTTPS. Para obter mais informações, consulte [planeamento para a chave de raiz fidedigna](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 Exemplo: ' CCMSetup.exe SMSROOTKEYPATH =&lt;completa e caminho do ficheiro\>`  

### <a name="smssigncert"></a>SMSSIGNCERT

 Especifica o nome e o caminho completo do ficheiro .cer do certificado autoassinado exportado no servidor do site.  

 Este certificado é armazenado no arquivo de certificados **SMS** e tem o nome de Requerente **Servidor do Site** e o nome amigável **Certificado de Assinatura do Servidor do Site**.  

 Exemplo: **CCMSetup.exe /usepkicert SMSSIGNCERT =&lt;nome de ficheiro e caminho completo\>**  

### <a name="smssitecode"></a>SMSSITECODE

 Especifica o site do Configuration Manager para atribuir o cliente. Este valor pode ser um código de site de três carateres ou a palavra AUTO. Se especificar AUTO ou se não especificar esta propriedade, o cliente tentará determinar a sua atribuição de site a partir de serviços de domínio do Active Directory ou de um ponto de gestão. Para ativar automática para atualizações de cliente, também tem de definir [SITEREASSIGN](#sitereassign) como TRUE.    

> [!NOTE]  
>  Não utilize AUTO se também de especificar o ponto de gestão baseado na internet (CCMHOSTNAME). Nesse caso, deve atribuir diretamente o cliente para o respetivo site.  

 Exemplo: `CCMSetup.exe SMSSITECODE=XZY`  

##  <a name="BKMK_attributevalues"></a> Valores de atributo suportados para os critérios de seleção de certificado PKI  
 O Configuration Manager suporta os seguintes valores de atributo para os critérios de seleção de certificado PKI:  

|Atributo OID|Atributo de Nome Único|Definição do atributo|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Componente do domínio|  
|1.2.840.113549.1.9.1|E ou E-mail|Endereço de e-mail|  
|2.5.4.3|CN|Nome comum|  
|2.5.4.4|SN|Nome do requerente|  
|2.5.4.5|SERIALNUMBER|Número de série|  
|2.5.4.6|C|Código de país|  
|2.5.4.7|L|Localidade|  
|2.5.4.8|S ou ST|Nome do estado ou distrito|  
|2.5.4.9|STREET|Morada|  
|2.5.4.10|O|Nome da organização|  
|2.5.4.11|OU|Unidade organizacional|  
|2.5.4.12|T ou Title|Título|  
|2.5.4.42|G ou GN ou GivenName|Nome próprio|  
|2.5.4.43|I ou Initials|Iniciais|  
|2.5.29.17|(sem valor)|Nome Alternativo do Requerente|  

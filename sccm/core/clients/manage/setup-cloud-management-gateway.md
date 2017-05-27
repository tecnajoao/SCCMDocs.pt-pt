---
title: "Configurar o Gateway de gestão da nuvem | Documentos do Microsoft"
description: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 05/01/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.translationtype: Machine Translation
ms.sourcegitcommit: d5a6fdc9a526c4fc3a9027dcedf1dd66a6fff5a7
ms.openlocfilehash: 97e1bc6585cee0ff433da0ec0b60b9604cb7348f
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---

# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurar o gateway de gestão da nuvem para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O processo de configuração de gateway de gestão da nuvem no Configuration Manager a partir na versão 1610, inclui os seguintes passos:

## <a name="step-1-configure-required-certificates"></a>Passo 1: Configurar certificados necessários

## <a name="option-1-preferred---use-the-server-authentication-certificate-from-a-public-and-globally-trusted-certificate-provider-like-verisign"></a>Opção 1 (preferencial) - utilize o certificado de autenticação de servidor a partir de um fornecedor de certificado pública e globalmente fidedigna (como o VeriSign)

Quando utiliza este método, os clientes serão automaticamente confiar no certificado e não é necessário criar um certificado SSL personalizado se.

1. Crie um registo de nome canónico (CNAME) no serviço de nomes de domínio público da sua organização (DNS) para criar um alias para o serviço de gateway de gestão de nuvem para um nome amigável, que será utilizado no certificado público.
Por exemplo, Contoso nomes respetivo serviço de nuvem management gateway **GraniteFalls** que no Azure será **GraniteFalls.CloudApp.Net**. Na público contoso.com espaço de nomes DNS da Contoso, o administrador DNS cria um novo registo CNAME para **GraniteFalls.Contoso.com** para o nome de anfitrião real, **GraniteFalls.CloudApp.net**.
2. Junto pedir um certificado de autenticação de servidor a partir de um fornecedor público utilizando o nome comum (CN) de CNAME alias.
Por exemplo, Contoso utiliza **GraniteFalls.Contoso.com** para o CN do certificado.
3. Crie o serviço de gateway de gestão em nuvem na consola do Configuration Manager utilizando este certificado.
    - No **definições** página do assistente criar nuvem gestão Gateway ao adicionar o certificado de servidor para este serviço em nuvem (a partir de **ficheiro de certificado**), o assistente irá extrair o nome de anfitrião do certificado CN como o nome do serviço e, em seguida, acrescentar esta opção para **cloudapp.net** (ou **usgovcloudapp.net** para a nuvem do Azure-nos para a administração pública) como o FQDN de serviço para criar o serviço no Azure.
Por exemplo, quando criar o gateway de gestão da nuvem Contoso, o nome de anfitrião **GraniteFalls** é extraída do certificado da CN, para que o serviço real do Azure seja criado como **GraniteFalls.CloudApp.net**.

### <a name="option-2---create-a-custom-ssl-certificate-for-cloud-management-gateway-in-the-same-way-as-for-a-cloud-based-distribution-point"></a>Opção 2 - criar um certificado SSL personalizado para o gateway de gestão da nuvem da mesma forma idêntica de um ponto de distribuição baseado na nuvem

Pode criar um certificado SSL personalizado para o gateway de gestão da nuvem da mesma forma que faria fazê-lo para um ponto de distribuição baseado na nuvem. Siga as instruções para [implementar o certificado de serviço para pontos de distribuição baseado na nuvem](/sccm/core/plan-design/network/example-deployment-of-pki-certificates) mas efetuar o seguinte diferente:

- Quando configurar o novo modelo de certificado, dar * * leitura * * e **inscrever** permissões para o grupo de segurança que configurou para servidores do Configuration Manager.
- Quando pedir o certificado de servidor web personalizado, fornecer um FQDN para o nome comum do certificado que termina em **cloudapp.net** para utilizar o gateway de gestão da nuvem no Azure nuvem pública ou **usgovcloudapp.net** para a nuvem do Azure para a administração pública.


## <a name="step-2-export-the-client-certificates-root"></a>Passo 2: Exportar raiz do certificado de cliente

A forma mais fácil obter exportação raiz dos certificados de cliente utilizado na rede, deve abrir um certificado de cliente numa das máquinas associados a um domínio que tenha uma e copie-o.

> [!NOTE] 
>
> São necessários certificados de cliente em qualquer computador que pretende gerir com o gateway de gestão de nuvem e no servidor do sistema de sites que aloja o conector de gateway de gestão de nuvem ponto. Se precisar de adicionar um certificado de cliente a qualquer uma destas máquinas, consulte o artigo [implementar o cliente certificado para computadores com o Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).

1.  Na janela executar, escreva **mmc** e prima ENTER.

2.  A partir do menu Ficheiro escolher **Adicionar/Remover Snap-in...** .

3.  Na caixa de diálogo Adicionar ou Remover Snap-ins, selecione **certificados** > **adicionar &gt;**   >  **conta de computador** > **seguinte** > **computador Local** > **concluir**. 

4.  Aceda a **certificados** &gt; **pessoal** &gt; **certificados**.

5.  Faça duplo clique no certificado para autenticação de cliente no computador, selecione o separador de caminho de certificação e, faça duplo clique na autoridade de raiz (na parte superior do caminho).

6.  No separador de detalhes, selecione **copiar para o ficheiro...** .

7.  Conclua o Assistente para exportar certificados utilizando o formato de certificado de predefinição. Certifique nota do nome e a localização do certificado de raiz que cria. Irá precisar dele para configurar o gateway de gestão de nuvem num [mais tarde passo](#step-4-set-up-cloud-management-gateway).

## <a name="step-3-upload-the-management-certificate-to-azure"></a>Passo 3: Carregar o certificado de gestão para o Azure

Um certificado de gestão do Azure é necessário para o Configuration Manager para aceder à API do Azure e configurar o gateway de gestão da nuvem. Para mais informações e instruções sobre como carregar um certificado de gestão, consulte os artigos seguintes na documentação do Azure:

- [Descrição geral de certificados para serviços de nuvem do Azure](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)

- [Carregar um certificado de gestão do Azure API de gestão](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)

>[!IMPORTANT]
>Certifique-se copiar o ID de subscrição associado o certificado de gestão. Terá de configurar o gateway de gestão da nuvem na consola do Configuration Manager no [passo seguinte](#step-4-set-up-cloud-management-gateway).

### <a name="subordinate-ca-certificates-and-azure"></a>Certificados de AC subordinados e Azure

Se o certificado foi emitido por uma AC subordinada (subCA) e, a sua infraestrutura PKI enterprise não estiver na Internet, utilize este procedimento para carregar o certificado para o Azure. 

1. No portal do Azure, depois de configurar um gateway de gestão da nuvem, localize o serviço de gateway de gestão de nuvem e ir para o **certificado** separador. Carregue o seu certificate(s) subCA existe. Se tiver mais do que um certificado de subCA, terá de carregar todos eles. 
2. Depois do certificado é carregado, registe o thumbprint. 
3. Adicione o thumbprint a base de dados do site ao utilizar este script:
    
```

    DIM serviceCName
    DIM subCAThumbprints

    ' Verify arguments
    IF WScript.Arguments.Count <> 2 THEN
    WScript.StdOut.WriteLine "Usage: CScript UpdateSubCAThumbprints.vbs <ServiceCName> <SubCA cert thumbprints, separated by ;>"
    WScript.Quit 1
    END IF

    'Get arguments
    serviceCName = WScript.Arguments.Item(0)
    subCAThumbprints = WScript.Arguments.Item(1)

    'Find SMS Provider
    WScript.StdOut.WriteLine "Searching for SMS Provider for local site..."
    SET objSMSNamespace = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms")
    SET results = objSMSNamespace.ExecQuery("SELECT * From SMS_ProviderLocation WHERE ProviderForLocalSite = true")

    'Process the results
    FOR EACH var in results
    siteCode = var.SiteCode
    NEXT

    IF siteCode = "" THEN
    WScript.StdOut.WriteLine "Failed to locate SMS provider."
    WScript.Quit 1
    END IF

    WScript.StdOut.WriteLine "SiteCode = " & siteCode 

    ' Connect to the SMS namespace
    SET objWMIService = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms\site_" & siteCode)

    'Get instance of SMS_AzureService
    DIM query
    query = "SELECT * From SMS_AzureService WHERE ServiceType = 'CloudProxyService' AND ServiceCName = '" & serviceCName & "'"
    WScript.StdOut.WriteLine "Run WQL query: " &  query
    SET objInstances = objWMIService.ExecQuery(query)

    IF IsNull(objInstances) OR (objInstances.Count = 0) THEN
    WScript.StdOut.WriteLine "Failed to get Azure_Service instance."
    WScript.Quit 1
    END IF

    FOR EACH var IN objInstances
    SET azService = var
    NEXT

    WScript.StdOut.WriteLine "Update [SubCACertThumbprint] to " & subCAThumbprints

    'Update SubCA cert thumbprints
    azService.Properties_.item("SubCACertThumbprint") = subCAThumbprints

    'Save data back to provider
    azService.Put_

    WScript.StdOut.WriteLine "[SubCACertThumbprint] is updated successfully."
```


## <a name="step-4-set-up-cloud-management-gateway"></a>Passo 4: Configurar o gateway de gestão da nuvem

>[!NOTE]
>Na versão 1610, nuvem management gateway é uma funcionalidade pré-lançamento. Para ativá-lo, consulte o artigo [utilizar funcionalidades de pré-lançamento das atualizações da](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

1. Na consola do Configuration Manager, aceda a **administração** > **serviços em nuvem** > **nuvem Management Gateway**.
2. Escolher **criar nuvem Management Gateway**.

3. No assistente criação de nuvem gestão de Gateway, introduza o seu ID de subscrição do Azure (copiado a partir do portal de gestão do Azure) e procure o ficheiro de certificado é utilizado para carregar como um certificado de gestão do Azure. Escolher **seguinte** e, em seguida, aguarde alguns momentos para que a consola para ligar ao Azure.

4. Preencha os detalhes adicionais no assistente:

    - Especifique o nome para o serviço que será executado no Azure. Nome do serviço tem de ser apenas carateres alfanuméricos e 3 e 24 carateres de comprimento.

    - Selecione a região Azure que pretende que o serviço para serem executadas no.

    - Especifique o número de máquinas virtuais que pretende utilizar para o serviço. A predefinição é 1, mas pode executar até 16 máquinas virtuais para o serviço.

    >[!NOTE]
    >Se utilizar um proxy de internet para o ponto de ligação do gateway de gestão na nuvem, terá de aumentar o número de portas do proxy, o número de máquinas virtuais que utiliza, começando na porta 10124.

    - Especifique a chave privada (ficheiro. pfx) que exportou a partir do certificado SSL personalizado.

    - Especifique o certificado de raiz exportado a partir do certificado de cliente.

    -   Especifique o mesmo nome de serviço FQDN que utilizou quando criou o novo modelo de certificado. Tem de especificar um dos seguintes sufixos FQDN nome do serviço com base na nuvem do Azure que está a utilizar:

    Nuvem do Azure | Prefixo FQDN
    --------------|-------------
    Nuvem pública de (comercial) | . cloudapp.net    
    Nuvem para a administração pública | . usgovcloudapp.net

  - Desmarque a caixa junto a **Certifique-se de revogação de certificados de cliente** (exceto se estiver publicamente publicar as informações de CRL).

  - Escolher **seguinte** quando terminar.

5. Se pretender monitorizar o tráfego de gateway de gestão de nuvem com um limiar de 14 dias, selecione a caixa de verificação para ativar o alerta do limiar. Em seguida, especifique o limiar e a percentagem no qual pretende elevar os diferentes níveis de alerta. Escolher **seguinte** quando terminar.

6. Reveja as definições e escolha **seguinte**. Gestor de configuração é iniciado como configurar o serviço. Depois de fechar o assistente irá demorar entre 5 a 15 minutos para aprovisionar o serviço completamente no Azure. Verifique o **estado** coluna para o recentemente a configuração nuvem management gateway para determinar quando o serviço está pronto.

## <a name="step-5-configure-primary-site-for-client-certification-authentication"></a>Passo 5: Configurar o site primário para autenticação de certificação de cliente

1. Na consola do Configuration Manager, aceda a **administração** > **configuração do Site** > **Sites**.

2. Selecione o site primário para os clientes que pretende gerir através do gateway de gestão de nuvem e escolher **propriedades**.

3. No separador das comunicações do computador cliente da folha de propriedades de site primário, verifique **certificado de cliente PKI de utilização (autenticação do cliente) se estiver disponível**.

4. Certifique-se limpar **verificam a lista de revogação de certificados (CRL) para sistemas de sites**. Esta opção apenas seria necessária se foram publicamente publicação de CRL.


## <a name="step-6-add-the-cloud-management-gateway-connector-point"></a>Passo 6: Adicionar o ponto de conector de gateway de gestão de nuvem

O ponto de conector do gateway de gestão na nuvem é uma nova função de sistema de sites para comunicação com gateway de gestão da nuvem. Para adicionar o ponto de conector do gateway de gestão na nuvem, siga as instruções em [adicionar funções do sistema de sites para o System Center Configuration Manager](/sccm/core/servers/deploy/configure/add-site-system-roles).

## <a name="step-7-configure-roles-for-cloud-management-gateway-traffic"></a>Passo 7: Configurar funções para o tráfego de gateway de gestão de nuvem

É o último passo na configuração do gateway de gestão da nuvem configurar as funções de sistema de sites para aceitar o tráfego de gateway de gestão de nuvem. Para Tech 1606 de pré-visualização, apenas o ponto de gestão, ponto de distribuição e as funções de ponto de atualização de software são suportadas para o gateway de gestão da nuvem. Tem de configurar cada função separadamente.

1. Na consola do Configuration Manager, aceda a **administração** > **configuração do Site** > **servidores e funções de sistema de sites**.

2. Selecione o servidor de sistema de sites para a função que pretende configurar para o tráfego de gateway de gestão de nuvem.

3. Selecione a função e, em seguida, selecione **propriedades**.

4. Na folha de propriedades da função, em ligações de cliente, escolha **HTTPS**, a caixa de verificação junto a **tráfego de gateway de gestão de nuvem de permitir que o Configuration Manager**e, em seguida, escolha **OK**. Repita estes passos para as restantes funções.

## <a name="step-8-configure-clients-for-cloud-management-gateway"></a>Passo 8: Configurar clientes para gateway de gestão da nuvem

Após a gestão de nuvem funções do sistema de sites e de gateway são completamente configuradas e em execução, os clientes obterão a localização do serviço de gateway de nuvem gestão automaticamente no pedido de localização seguinte. Os clientes devem estar na rede da empresa para receber a localização do serviço de gateway de gestão de nuvem. O ciclo de consulta para pedidos de localização é a cada 24 horas. Se não pretender aguardar que o pedido de localização normalmente agendadas, pode forçar o pedido, reiniciando o serviço de anfitrião de agente do SMS (ccmexec.exe) no computador.

Com a localização do serviço de gateway de nuvem gestão configurado no cliente, automaticamente pode determinar se está na intranet ou na Internet. Se o cliente pode contactar o controlador de domínio ou o ponto de gestão no local, irá utilizá-lo para comunicar com o Configuration Manager, caso contrário,-iremos considerá-lo está na Internet e utilizar a localização do management gateway na nuvem do serviço para comunicar.

>[!NOTE]
> Pode forçar o cliente utiliza sempre o gateway de gestão da nuvem independentemente de ser na intranet ou Internet. Para tal, defina a seguinte chave de registo no computador cliente: \
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`

Para verificar que os clientes podem contactar do Configuration Manager, pode executar o seguinte comando do PowerShell no computador cliente:

`gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate`

Este comando apresenta os pontos de gestão, que o cliente pode contactar incluindo o serviço de gateway de gestão de nuvem.

## <a name="next-steps"></a>Passos seguintes

[Monitorize os clientes para gateway de gestão da nuvem](monitor-clients-cloud-management-gateway.md)


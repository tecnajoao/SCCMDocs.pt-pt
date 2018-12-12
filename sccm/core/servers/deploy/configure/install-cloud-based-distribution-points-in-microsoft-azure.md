---
title: Instalar pontos de distribuição de nuvem
titleSuffix: Configuration Manager
description: Utilize estes passos para configurar um ponto de distribuição de nuvem no Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a9f29fcb0c1fea4bd5ff1de7327b58a05934eeeb
ms.sourcegitcommit: 2491fbe98915b7a30c2422a371c929d0d4ebf22f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53247446"
---
# <a name="install-a-cloud-distribution-point-for-configuration-manager"></a>Instalar um ponto de distribuição de nuvem para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo detalha os passos para instalar um ponto de distribuição de nuvem do Configuration Manager no Microsoft Azure. Ele inclui as secções seguintes:
- [Antes de começar](#bkmk_before) 
- [Configurar](#bkmk_setup)
- [Configurar o DNS](#bkmk_dns)
- [Configurar o proxy de servidor do site](#bkmk_proxy)
- [Distribuir o conteúdo e configure clientes](#bkmk_client)
- [Gerir e monitorizar](#bkmk_monitor)
- [Modificar](#bkmk_modify)
- [Resolução de problemas avançada](#bkmk_tshoot) 



## <a name="bkmk_before"></a> Antes de começar

Comece por ler o artigo [utilizar um ponto de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). Esse artigo ajuda-o a planear e estruturar os pontos de distribuição de nuvem. 

Utilize a lista de verificação seguinte para se certificar de que tem as informações necessárias e pré-requisitos para criar um ponto de distribuição de nuvem:  

- O servidor do site pode ligar ao Azure. Se a sua rede utilizar um proxy [configurar a função de sistema de sites](#bkmk_proxy).  

- O **ambiente do Azure** a utilizar. Por exemplo, nuvem pública do Azure ou a nuvem do Azure US Government.  

- A partir da versão 1806 e *recomendado*, utilize o **implementação Azure Resource Manager**. Ele tem os seguintes requisitos:<!--1322209-->  

    - Integração com o [do Azure Active Directory](/sccm/core/servers/deploy/configure/azure-services-wizard) para **gestão da Cloud**. Deteção de utilizadores do Azure AD não é necessária.  

    - O Azure **ID de subscrição**.  

    - O Azure **grupo de recursos**.  

    - R **conta de administrador de subscrição** tem de iniciar sessão durante o assistente.  

- Se planeia utilizar o Azure **implementação de serviço clássico**, precisa dos seguintes requisitos:  
    > [!Important]  
    > A partir da versão 1810, implementações de serviço clássico no Azure foram preteridas no Configuration Manager. Começar a utilizar implementações do Azure Resource Manager para o gateway de gestão na cloud. Para obter mais informações, consulte [planear CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).  

    - O Azure **ID de subscrição**.  

    - Do Azure **certificado de gestão**, exportado como ambas. CER e. Ficheiros PFX. Um administrador de subscrição do Azure tem de adicionar o. Certificado de gestão de CER para a subscrição na [portal do Azure](https://portal.azure.com).  

- R **certificado de autenticação de servidor**, exportado como um. Ficheiro PFX.  

- Globalmente exclusivo **nome do serviço** para o ponto de distribuição de nuvem.  

    > [!TIP]  
    > Antes de solicitar o certificado de autenticação de servidor que utiliza este nome de serviço, confirme que o nome de domínio do Azure pretendido é exclusivo. Por exemplo, *WallaceFalls.CloudApp.Net*. Inicie sessão no [Portal do Microsoft Azure](https://portal.azure.com). Selecione **criar um recurso**, escolha a **computação** categoria, em seguida, selecione **serviço em nuvem**. Na **nome DNS** campo, escreva o prefixo pretendido, por exemplo *WallaceFalls*. A interface reflete se o nome de domínio está disponível ou já em utilização por outro serviço. Não criar o serviço no portal, basta usar este processo para verificar a disponibilidade de nome.  
 
- O Azure **região** para esta implementação.  



##  <a name="bkmk_setup"></a> Configurar   

Efetuar este procedimento no site para alojar este ponto de distribuição de nuvem, conforme determinado pela sua [design](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_topology).  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **serviços Cloud**e selecione **pontos de distribuição de nuvem**. No Friso, selecione **criar ponto de distribuição na nuvem**.  

2.  Sobre o **gerais** página do Cloud distribuição ponto Assistente para criar, configurar as seguintes definições:  

    1. Especificar primeiro a **ambiente do Azure**.  

    2. A partir da versão 1806 e *recomendado*, selecione **implementação Azure Resource Manager** como o método de implementação. Selecione **iniciar sessão** para autenticar com uma conta de administrador de subscrição do Azure. O assistente é preenchido automaticamente os campos restantes das informações armazenadas durante o pré-requisito de integração do Azure AD. Se tiver várias subscrições, selecione o **ID de subscrição** da subscrição pretendida para utilizar.  

    > [!Note]  
    > A partir da versão 1810, implementações de serviço clássico no Azure foram preteridas no Configuration Manager. 
    > 
    > Se precisar de utilizar uma implementação de serviço clássico, selecione essa opção nesta página. Entrar pela primeira vez do Azure **ID de subscrição**. Em seguida, selecione **procurar** e selecione o. Ficheiro PFX do certificado de gestão do Azure.  

3.  Selecione **Seguinte**. Aguarde enquanto o site testa a ligação para o Azure.  

4.  Sobre o **definições** página, especifique as seguintes definições e, em seguida, selecione **próxima**:  

    - **Região**: Selecione a região do Azure onde pretende criar o ponto de distribuição de nuvem.  

    - **Grupo de recursos** (método de implementação Azure Resource Manager apenas)  

        - **Utilizar existente**: Selecione um grupo de recursos existente na lista pendente.  

        - **Criar um novo**: Introduza o nome do grupo de recursos novo para criar na sua subscrição do Azure.  

    - **Site primário**: Selecione o site primário para distribuir conteúdo para este ponto de distribuição.

    - **Ficheiro de certificado**: Selecione **procurar** e selecione o. Ficheiro PFX de certificado de autenticação de servidor este ponto de distribuição de nuvem. O nome comum deste certificado preenche necessários **FQDN de serviço** e **nome do serviço** campos.  

        > [!NOTE]  
        > O certificado de autenticação de servidor de ponto de distribuição de nuvem suporta carateres universais. Se utilizar um certificado de caráter universal, substitua o asterisco (\*) no **FQDN de serviço** campo com o nome de anfitrião desejado para o serviço.  

5. Sobre o **alertas** página, configurar quotas de armazenamento, quotas de transferência e em que percentagem destas quotas pretende que o Configuration Manager para gerar de alertas. Em seguida, selecione **seguinte**.  

6. Conclua o assistente.  


### <a name="monitor-installation"></a>Instalação do monitor  

O site começa a criar um novo serviço hospedado para o ponto de distribuição de nuvem. Depois de fechar o assistente, monitorize o progresso da instalação do ponto de distribuição em nuvem na consola do Configuration Manager. Monitorizar também o **Cloudmgr** ficheiro no servidor do site primário. Se necessário, monitorize o aprovisionamento do serviço cloud no portal do Azure.  

> [!NOTE]  
>  Pode demorar até 30 minutos para aprovisionar um novo ponto de distribuição no Azure. O **Cloudmgr** ficheiro repete a seguinte mensagem até que a conta de armazenamento seja aprovisionada:  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> Depois que ele fornece a conta de armazenamento, o serviço é criado e configurado.  


### <a name="verify-installation"></a>Verificar a instalação

Certifique-se de que a instalação de ponto de distribuição de nuvem está concluída através dos seguintes métodos:  

- Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **serviços Cloud**e selecione o **pontos de distribuição de nuvem** nó. Localize o novo ponto de distribuição de nuvem na lista. A coluna de estado deve ser **pronto**.  

- Na consola do Configuration Manager, vá para o **monitorização** área de trabalho. Expanda **estado do sistema**e selecione o **estado do componente** nó. Mostrar todas as mensagens a partir da **SMS_CLOUD_SERVICES_MANAGER** componente e procurar Estado ID de mensagem **9409**.  

- Se necessário, vá para o portal do Azure. O **implantação** apresenta o estado da distribuição da nuvem ponto **pronto**.  



##  <a name="bkmk_dns"></a> Configurar o DNS  

Antes dos clientes podem utilizar o ponto de distribuição de nuvem, deve conseguir resolver o nome do ponto de distribuição de nuvem para um endereço IP gerido pelo Azure. O ponto de gestão dá a eles a **FQDN de serviço** de ponto de distribuição de nuvem. O ponto de distribuição em nuvem existe no Azure como o **nome do serviço**. Consulte estes valores no **definições** separador de propriedades do ponto de distribuição de nuvem. 

> [!Note]  
> O **pontos de distribuição de nuvem** nó na consola do inclui uma coluna chamada **nome do serviço**, mas, na verdade, mostra o **FQDN de serviço** valor. Para ver os dois valores, abra **propriedades** para a distribuição de nuvem de ponto e mude para o **definições** separador.  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

Nome de comum do certificado de autenticação de servidor deve incluir o seu nome de domínio. Este nome é obrigatório quando comprar um certificado de um fornecedor de público. Recomenda-se ao emitir este certificado em sua PKI. Por exemplo, `WallaceFalls.contoso.com`. Ao especificar este certificado no assistente ponto de criação de distribuição de nuvem, o nome comum preenche os **FQDN de serviço** propriedade (`WallaceFalls.contoso.com`). O **nome do serviço** usa o mesmo nome de anfitrião (`WallaceFalls`) e o anexe ao nome de domínio do Azure, `cloudapp.net`. Neste cenário, os clientes precisam resolver o seu domínio **FQDN de serviço** (`WallaceFalls.contoso.com`) para o Azure **nome do serviço** (`WallaceFalls.cloudapp.net`). Crie um alias CNAME para mapear esses nomes.


### <a name="create-cname-alias"></a>Criar CNAME alias

Crie um registo de nome canónico (CNAME) no DNS público, com acesso à internet de sua organização. Este registo cria um alias para o ponto de distribuição de nuvem **FQDN de serviço** propriedade que os clientes recebem, para o Azure **nome do serviço**. Por exemplo, criar um novo registo CNAME `WallaceFalls.contoso.com` para `WallaceFalls.cloudapp.net`.  


### <a name="client-name-resolution-process"></a>Processo de resolução de nome de cliente

O processo a seguir mostra como um cliente resolve o nome do ponto de distribuição de nuvem:  

1. O cliente obtém os **FQDN de serviço** da distribuição em nuvem do ponto na lista de fontes de conteúdo. Por exemplo, `WallaceFalls.contoso.com`.  

2. Ele consulta DNS, que resolve o FQDN de serviço com o alias CNAME para o Azure **nome do serviço**. Por exemplo, `WallaceFalls.cloudapp.net`.  

3. Ele consulta DNS novamente, que resolve o nome do serviço do Azure para o endereço IP público do Azure.   

4. O cliente utiliza este endereço IP para iniciar a comunicação com o ponto de distribuição de nuvem.   

5. O ponto de distribuição em nuvem apresenta o servidor de certificado de autenticação para o cliente. O cliente utiliza a cadeia de fidedignidade do certificado para validar.  



## <a name="bkmk_proxy"></a> Configurar o proxy de servidor do site  

O servidor de site primário que gere as necessidades de ponto de distribuição de nuvem para comunicar com o Azure. Se a sua organização utilizar um servidor proxy para controlar o acesso à internet, configure o servidor de site primário para utilizar este proxy.   

Para obter mais informações, consulte [suporte de servidor de Proxy](/sccm/core/plan-design/network/proxy-server-support).  



## <a name="bkmk_client"></a> Distribuir o conteúdo e configure clientes

Distribua o conteúdo ao ponto de distribuição de nuvem a mesma como qualquer outro local ponto de distribuição. O ponto de gestão não inclui o ponto de distribuição em nuvem na lista de localizações de conteúdos, exceto se tiver o conteúdo solicitados pelos clientes. Para obter mais informações, consulte [distribuir e gerir conteúdos](/sccm/core/servers/deploy/configure/deploy-and-manage-content). 

Gerir um ponto de distribuição de nuvem o mesmo como qualquer outro local ponto de distribuição. Essas ações incluem atribui-la a um grupo de pontos de distribuição e gestão de pacotes de conteúdos. Para obter mais informações, consulte [instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).

Predefinições de cliente automaticamente permitem aos clientes utilizar pontos de distribuição de nuvem. Controlar o acesso a todos os pontos de distribuição de cloud na sua hierarquia com a seguinte definição de cliente:  

   - Na **definições de nuvem** de grupo, modifique a definição **permitir o acesso a pontos de distribuição de nuvem**.  

       - Por predefinição, esta definição está definida como **Sim**.  

       - Modificar e implementar esta definição para utilizadores e dispositivos.  



## <a name="bkmk_monitor"></a> Gerir e monitorizar  

Monitorizar o conteúdo que distribui para uma distribuição de cloud ponto igual com quaisquer outros pontos de distribuição no local. Para obter mais informações, consulte [monitorizar conteúdo](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed). 

### <a name="bkmk_alerts"></a> Alertas  

O Configuration Manager verifica periodicamente o serviço do Azure. Se o serviço não está ativo ou se existirem problemas de certificado ou de subscrição, o Configuration Manager gera um alerta. 

Configure limiares para a quantidade de dados que pretende armazenar no ponto de distribuição de nuvem e para a quantidade de dados transferidos pelos clientes a partir do ponto de distribuição. Utilize alertas para estes limiares para o ajudar a decidir quando parar ou eliminar o serviço em nuvem, ajustar o conteúdo que armazenar no ponto de distribuição de nuvem ou modificar os clientes que podem utilizar o serviço. 

- **Limiar de alerta de armazenamento**: O limiar de alerta de armazenamento define um limite superior em GB a quantidade de dados ou conteúdo que pretende que o arquivo no ponto de distribuição de cloud. Por predefinição, este limiar é 2000 GB. O Configuration Manager gera alertas de aviso e críticas quando o espaço livre restante atinge os níveis que especificar. Por predefinição, estes alertas ocorrem em 50% e 90% do limiar.  

- **Limiar de alerta de transferência mensal**: O limiar de alerta de transferência mensal ajuda-o a monitorizar a quantidade de conteúdo que é transferido do ponto de distribuição para os clientes durante um período de 30 dias. Por predefinição, este limiar é de 10 000 GB. O site gera alertas de aviso e críticas quando as transferências atingirem valores por si. Por predefinição, estes alertas ocorrem em 50% e 90% do limiar.  

    > [!IMPORTANT]  
    >  O Configuration Manager monitoriza a transferência de dados, mas não a interromperá a transferência de dados acima do limiar de alerta de transferência especificado.  

Especificar limiares para cada ponto de distribuição em nuvem durante a instalação ou utilizar o **alertas** separador de propriedades do ponto de distribuição de nuvem.  

> [!NOTE]  
>  Alertas para um ponto de distribuição em nuvem dependem das estatísticas de utilização do Azure, que pode demorar até 24 horas a ficar disponível. Para obter mais informações sobre a análise de armazenamento do Azure, consulte [a análise de armazenamento](https://docs.microsoft.com/rest/api/storageservices/storage-analytics).  

Num ciclo horário, o site primário que monitoriza o ponto de distribuição na nuvem transfere dados de transação do Azure. Ele armazena estes dados de transação no `CloudDP-<ServiceName>.log` ficheiro no servidor do site. Do Configuration Manager avalia então esta informação face às quotas de armazenamento e transferência para cada ponto de distribuição de nuvem. Quando a transferência de dados atinge ou excede o volume especificado para avisos e alertas críticos, o Configuration Manager gera o alerta adequado.  

> [!WARNING]  
>  Uma vez que o site transfere informações sobre as transferências de dados do Azure a cada hora, a utilização pode exceder um limiar de aviso ou crítico antes do Configuration Manager pode aceder aos dados e emitir um alerta.  



## <a name="bkmk_modify"></a> Modificar

Ver informações de alto nível sobre o ponto de distribuição no **pontos de distribuição de nuvem** no nó **serviços Cloud** no **administração** área de trabalho das Consola do Configuration Manager. Selecione um ponto de distribuição e selecione **propriedades** para ver mais detalhes.  

Ao editar as propriedades de um ponto de distribuição de nuvem, os seguintes separadores incluem definições para editar:  

#### <a name="settings"></a>Definições  

- **Descrição**  

- **Ficheiro de certificado**: Antes de expira o certificado de autenticação de servidor, emita um novo certificado com o mesmo nome comum. Em seguida, adicione o novo certificado aqui para o serviço começar a utilizar. Se o certificado expirar, os clientes não confiar e utilizar o serviço.  

#### <a name="alerts"></a>Alertas
Ajuste os limiares de dados de armazenamento e alertas de transferência mensal.  

#### <a name="content"></a>Conteúdo
Gerir conteúdo igual de um ponto de distribuição no local.  


### <a name="redeploy-the-service"></a>Reimplemente o serviço

Alterações mais significativas, como as seguintes configurações, necessitam de voltar a implementar o serviço:
- Método de implementação clássica para Azure Resource Manager
- Subscrição
- Nome do serviço
- Privado para PKI pública
- Região do Azure

A partir da versão 1806, se tiver uma ponto no método de implementação clássica, para poder utilizar o método de implementação Azure Resource Manager de distribuição de nuvem existente terá de implementar um novo ponto de distribuição de nuvem. Existem duas opções:

- Se quiser reutilizar o mesmo nome de serviço:  

    1. Primeiro de eliminar o ponto de distribuição de cloud clássica. Se não existir outro ponto de distribuição de nuvem, os clientes não poderá obter o conteúdo.  

    2. Crie um novo ponto de distribuição de cloud através de uma implementação do Resource Manager. Reutilize o mesmo certificado de autenticação de servidor.  

    3. Distribua o conteúdo do pacote de software necessárias para o novo ponto de distribuição de nuvem.  

- Se pretender utilizar um novo nome de serviço:  

    1. Crie um novo ponto de distribuição de cloud através de uma implementação do Resource Manager. Utilize um novo certificado de autenticação de servidor.  

    2. Distribua o conteúdo do pacote de software necessárias para o novo ponto de distribuição de nuvem.  

    3. Elimine o ponto de distribuição de cloud clássica.

> [!Tip]  
> Para determinar o modelo de implementação atual de um ponto de distribuição de nuvem:<!--SCCMDocs issue #611-->  
> 1. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **serviços Cloud**e selecione o **pontos de distribuição de nuvem** nó.  
> 2. Adicionar a **modelo de implementação** atributo como uma coluna para a vista de lista. Para uma implementação do Resource Manager, este atributo é **do Azure Resource Manager**.  


### <a name="stop-or-start-the-cloud-service-on-demand"></a>Parar ou iniciar o serviço em nuvem a pedido

Pare um ponto de distribuição de nuvem em qualquer altura na consola do Configuration Manager. Esta ação impede imediatamente os clientes transfiram conteúdo adicional do serviço. Reinicie o serviço de cloud a partir da consola do Configuration Manager para restaurar o acesso dos clientes. Por exemplo, deve pare um serviço em nuvem quando ela atinge um limiar de dados.  

Quando para um ponto de distribuição de nuvem, o serviço cloud não elimina o conteúdo da conta de armazenamento. Ele também não impede o servidor do site de transferir conteúdo adicional para o ponto de distribuição de nuvem. O ponto de gestão ainda retorna o ponto de distribuição de nuvem para clientes como uma origem de conteúdo válida. 

Utilize o procedimento seguinte para parar um ponto de distribuição de nuvem:  

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **serviços Cloud**e selecione o **pontos de distribuição de nuvem** nó.  

2. Selecione o ponto de distribuição de nuvem. Para parar o serviço em nuvem executado no Azure, selecione **parar serviço** na faixa de opções.  

3. Selecione **iniciar o serviço** para reiniciar o ponto de distribuição de nuvem.  


### <a name="delete-a-cloud-distribution-point"></a>Eliminar um ponto de distribuição de nuvem

Para desinstalar um ponto de distribuição de nuvem, selecione o ponto de distribuição na consola do Configuration Manager e, em seguida, selecione **eliminar**.  

Quando eliminar um ponto de distribuição de nuvem de uma hierarquia, o Gestor de configuração remove o conteúdo do serviço em nuvem no Azure. 

Remover manualmente os componentes no Azure faz com que o sistema para serem inconsistentes. Este Estado mantém informações órfãos e comportamentos inesperados podem ocorrer.



## <a name="bkmk_tshoot"></a> Resolução de problemas avançada

Se pretender recolher o registo de diagnósticos de VMS do Azure para o ajudar a resolver problemas relacionados com o seu ponto de distribuição de nuvem, utilize o seguinte exemplo do PowerShell para ativar a extensão de diagnóstico do serviço para a subscrição:<!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using 
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using 

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script. 
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate 
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```


O exemplo a seguir é um exemplo **diagnostics.wadcfgx** ficheiro referenciada na **public_config** variáveis no script de PowerShell acima. Para obter mais informações, consulte [esquema de configuração da extensão de diagnóstico do Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics-schema).  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```


---
title: Resolução de problemas de análise de área de trabalho
titleSuffix: Configuration Manager
description: Detalhes técnicos para ajudar a resolver problemas com a análise de ambiente de trabalho.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6bebf4065a4db1c45ee7eaa0a5b04b8d1533f29f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121546"
---
# <a name="troubleshooting-desktop-analytics"></a>Resolução de problemas de análise de área de trabalho

Utilize os detalhes neste artigo para ajudar a resolver problemas com a análise de ambiente de trabalho integrado com o Configuration Manager.



## <a name="confirm-prerequisites"></a>Confirmar pré-requisitos

Muitos problemas comuns são causados por pré-requisitos em falta. Em primeiro lugar, confirme as seguintes configurações:

- [Pré-requisitos](/sccm/desktop-analytics/overview#prerequisites)  

- [Atualizações de componentes do Windows](/sccm/desktop-analytics/enroll-devices#update-devices)  

- [Como ativar a partilha de dados](/sccm/desktop-analytics/enable-data-sharing), que abrange os seguintes tópicos:  

    - Pontos finais de Internet para que os clientes precisam de ligar  

    - Autenticação do servidor proxy  

    - Níveis de dados de diagnóstico  



## <a name="monitor-connection-health"></a>Ligação de monitor do Estado de funcionamento

Utilize o **estado de funcionamento da ligação** dashboard no Configuration Manager para fazer uma busca detalhada em categorias por Estado de funcionamento do dispositivo. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda o **manutenção do Microsoft 365** nó e selecione o **estado de funcionamento da ligação** dashboard.  

![Captura de ecrã do dashboard de estado de funcionamento do Gestor de configuração de ligação](media/connection-health-dashboard.png)

Se acha que alguns dispositivos não apresentarem no ambiente de trabalho de análise, verifique primeiro a percentagem de **dispositivos ligados**. Se for inferior a 100%, certifique-se de que os dispositivos são suportados pelo ambiente de trabalho de análise. Para obter mais informações, consulte [pré-requisitos](/sccm/desktop-analytics/overview#prerequisites).


### <a name="connection-health-states"></a>Estados de funcionamento da ligação

A seguir, rever o **estado de funcionamento da ligação** gráfico. Apresenta o número de dispositivos nas seguintes categorias de estado de funcionamento:  

- [Corretamente inscritos](#properly-enrolled)  
- [Problemas de configuração](#configuration-issues)  
- [cliente não instalado](#client-not-installed)  
- [A aguardar a inscrição](#waiting-for-enrollment)  
- [Pré-requisitos em falta](#missing-prerequisites)  
- [Dados em falta](#missing-data)  

Selecione o nome de categoria para remover ou adicioná-lo a partir do gráfico. Esta ação ajuda a reduzir o gráfico para que possa ver os tamanhos relativos de segmentos mais pequenos. 

#### <a name="properly-enrolled"></a>Corretamente inscritos
O dispositivo tem os seguintes atributos:  
- Uma versão 1810 ou posterior do cliente do Configuration Manager  
- Não há nenhum erro de configuração  
- Análise de área de trabalho recebeu dados de diagnóstico completos partir deste dispositivo nos últimos 28 dias  
- Análise de área de trabalho tem um inventário completo da configuração do dispositivo e aplicações instaladas  

#### <a name="configuration-issues"></a>Problemas de configuração
Configuration Manager detetar um ou mais problemas com a configuração necessária para a análise de ambiente de trabalho. Para obter mais informações, consulte a lista de [propriedades do dispositivo de análise de ambiente de trabalho no Configuration Manager](#bkmk_config-issues).  

#### <a name="client-not-installed"></a>cliente não instalado
O dispositivo é direcionado para a análise de ambiente de trabalho, mas não é um cliente do Configuration Manager. 

O cliente do Configuration Manager é necessário para configurar e gerir o dispositivo para a análise de ambiente de trabalho. Para obter mais informações, consulte [métodos de instalação de cliente](/sccm/core/clients/deploy/plan/client-installation-methods).  

#### <a name="waiting-for-enrollment"></a>A aguardar a inscrição
Análise de área de trabalho não tem dados de diagnóstico para este dispositivo. Este problema pode ser porque o dispositivo foi recentemente adicionado à coleção de destino e ainda não enviou a dados. Também pode significar o dispositivo não está a comunicar corretamente com o serviço e os dados de diagnóstico mais recente são a mais de 28 dias. 

Certifique-se de que o dispositivo é capaz de comunicar com o serviço. Para obter mais informações, consulte [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

#### <a name="missing-prerequisites"></a>Pré-requisitos em falta
O cliente do Configuration Manager não é, pelo menos, versão 1810 (5.0.8740). 

Atualize o cliente com a versão mais recente. Considere ativar a atualização automática de cliente para o site do Configuration Manager. Para obter mais informações, consulte [atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

#### <a name="missing-data"></a>Dados em falta
Análise de área de trabalho não é possível criar uma avaliação de compatibilidade. Ela não tem um conjunto de dados completo para a configuração do dispositivo (de censo) ou aplicações (inventário) instaladas. 

Este problema, muitas vezes, é corrigido automaticamente quando o dispositivo repete. Se persistir, certifique-se de que o dispositivo é capaz de comunicar com o serviço. Para obter mais informações, consulte [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints).  


### <a name="device-list"></a>Lista de dispositivos

Para ver uma lista específica de dispositivos por Estado, comece com o **estado de funcionamento da ligação** dashboard. Selecione um dos segmentos do **estado de funcionamento da ligação** mosaico e desagregar para obter uma lista de dispositivos desta categoria. Esta vista de dispositivo personalizado apresenta as seguintes colunas de análise de ambiente de trabalho, por predefinição:
- Configuração de ID comercial
- Atualização de compatibilidade mínimo
- Windows dados de diagnóstico participar
- Windows dados comerciais participar
- Conectividade de ponto final de diagnóstico do Windows
- Conectividade de ponto final de diagnóstico do Office

Estas colunas correspondem à chave [pré-requisitos](/sccm/desktop-analytics/overview#prerequisites) para dispositivos a comunicar com a análise de ambiente de trabalho. 

![Captura de ecrã de corretamente inscritos a lista de dispositivos](media/sccm-device-list-properly-enrolled.png)

Selecione um dispositivo para ver a lista completa das propriedades disponíveis no painel de detalhes. Também pode adicionar qualquer uma dessas propriedades como colunas à lista de dispositivos. 


### <a name="bkmk_config-issues"></a> Área de trabalho Propriedades de dispositivo de análise no Configuration Manager

As colunas seguintes estão disponíveis na lista de dispositivos:
- [Configuração de appraiser](#appraiser-configuration)  
- [Atualização de compatibilidade mínimo](#minimum-compatibility-update)  
- [Versão de appraiser](#appraiser-version)  
- [Última execução completa com êxito de Appraiser](#last-successful-full-run-of-appraiser)  
- [Recolha de dados de appraiser](#appraiser-data-collection)  
- [Última execução completa com êxito de censo](#last-successful-full-run-of-census)  
- [Recolha de dados de censo](#census-data-collection)  
- [Conectividade de ponto final de diagnóstico do Windows](#windows-diagnostic-endpoint-connectivity)  
- [Verifique os dados de diagnóstico do utilizador final](#check-end-user-diagnostic-data)  
- [Verifique o proxy de usuário](#check-user-proxy)  
- [Configuração de ID comercial](#commercial-id-configuration)  
- [Windows dados comerciais participar](#windows-commercial-data-opt-in)  
- [Verifique o nome do dispositivo em dados de diagnóstico](#check-device-name-in-diagnostic-data)  
- [Configuração do serviço DiagTrack](#diagtrack-service-configuration)  
- [Versão de DiagTrack](#diagtrack-version)  
- [Obtenção de ID de SQM](#sqm-id-retrieval)  
- [Obtenção de identificador exclusivo do dispositivo](#unique-device-identifier-retrieval)  
- [Windows dados de diagnóstico participar](#windows-diagnostic-data-opt-in)  
- [Conectividade de ponto final de diagnóstico do Office](#office-diagnostic-endpoint-connectivity)  

#### <a name="appraiser-configuration"></a>Configuração de appraiser
<!--20,21--> Appraiser é o componente do Windows que corresponde da [atualizações de compatibilidade](/sccm/desktop-analytics/enroll-devices#update-devices). Ele avalia as aplicações e os controladores do dispositivo para compatibilidade com a versão mais recente do Windows. 

Se esta verificação for bem sucedida, o componente de appraiser está corretamente configurado no dispositivo. 

Caso contrário, ele poderá apresentar um dos seguintes erros:

- Não é possível configurar a coleção de dados de compatibilidade de aplicações de dispositivo (SetRequestAllAppraiserVersions). Verifique os registos para os detalhes da exceção  

- Não é possível configurar a coleção de dados de compatibilidade de aplicações de dispositivo (SetRequestAllAppraiserVersions). Verifique os registos para os detalhes da exceção  

- Não é possível escrever o RequestAllAppraiserVersions chave de registo `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`. Verifique as permissões  

Verifique as permissões nesta chave de registo. Certifique-se de que a conta sistema local pode aceder a esta chave para o cliente do Configuration Manager definir.  

Para obter mais informações, consulte M365AHandler.log no cliente.  


#### <a name="minimum-compatibility-update"></a>Atualização de compatibilidade mínimo
<!--18,19,32--> A atualização de compatibilidade (appraiser.dll) não está instalado ou desatualizados no dispositivo. É mais antigo do que os requisitos mínimos para análise de ambiente de trabalho, 10.0.17763. 

Instale a atualização de compatibilidade mais recente. Para obter mais informações, consulte [atualizações de compatibilidade](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser).


#### <a name="appraiser-version"></a>Versão de appraiser
Esta propriedade apresenta a versão atual do componente Appraiser no dispositivo. Mostra a versão do ficheiro no `%windir%\System32\appraiser.dll`, sem os pontos decimais. Por exemplo, a versão do ficheiro 10.0.17763 mostra como 10017763. 


#### <a name="last-successful-full-run-of-appraiser"></a>Última execução completa com êxito de Appraiser
Esta propriedade apresenta a data e hora em que o dispositivo última execução com êxito Appraiser.


#### <a name="appraiser-data-collection"></a>Recolha de dados de appraiser
<!--Appraiser run status-->
<!--22,33--> Esta propriedade mostra o resultado mais recente do Windows em execução o componente de appraiser. 

Se não for bem sucedida, poderá mostrar um dos seguintes erros: 

- Não é possível recolher dados de compatibilidade de aplicações (RunAppraiser). Verifique os registos para obter detalhes  

- Coleção de dados de compatibilidade de aplicações (CompatTelRunner.exe) terminou com um código de erro  

Para obter mais informações, consulte M365AHandler.log no cliente. 

Verificar o seguinte ficheiro: `%windir%\System32\CompatTelRunner.exe`. Se não existir, reinstale o necessários [atualizações de compatibilidade](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser). Certifique-se de que nenhum outro componente do sistema está a remover deste ficheiro, como a diretiva de grupo ou um serviço de antimalware. 

Se o ficheiro de M365Handler.log no cliente inclui um dos seguintes erros: `RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1`
`RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005`
`RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005`  

Para ajudar a corrigir esses erros, execute os seguintes comandos a partir de uma consola elevada do Windows PowerShell no cliente afetado:

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force 

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

#### <a name="last-successful-full-run-of-census"></a>Última execução completa com êxito de censo
Esta propriedade apresenta a data e hora em que o dispositivo última execução com êxito censo. 

#### <a name="census-data-collection"></a>Recolha de dados de censo
<!-- Census run status -->
<!--51,52--> Recenseamento é o componente do Windows que faz o inventário do dispositivo. Estes dados de inventário são utilizados para compreender o dispositivo e a respetiva configuração. 

Esta propriedade mostra o resultado mais recente do Windows em execução o componente de censo.

Se não for bem sucedida, poderá mostrar um dos seguintes erros: 

- Não é possível recolher dados sobre o dispositivo e a respetiva configuração (RunCensus). Verifique os registos para os detalhes da exceção  

- Dispositivo e a configuração dados coleção ferramenta (devicecensus.exe) não encontrada  

Para obter mais informações, consulte M365AHandler.log no cliente. 

Verificar o seguinte ficheiro: `%windir%\System32\DeviceCensus.exe`. Se não existir, reinstale o necessários [atualizações de compatibilidade](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser). Certifique-se de que nenhum outro componente do sistema está a remover deste ficheiro, como a diretiva de grupo ou um serviço de antimalware. 


#### <a name="windows-diagnostic-endpoint-connectivity"></a>Conectividade de ponto final de diagnóstico do Windows
<!--12,15--> Se esta verificação for bem sucedida, o dispositivo é capaz de ligar para o endpoint de telemetria e experiência do usuário conectado (Vortex). 

Caso contrário, ele pode mostrar um dos seguintes erros:  

- Não é possível ligar para o endpoint de telemetria e experiência do usuário conectado (Vortex). Verifique as definições de rede/proxy  

- Não é possível verificar a conectividade para o endpoint de telemetria e experiência do usuário conectado (CheckVortexConnectivity). Verifique os registos para os detalhes da exceção  

Dispositivos verificam a conectividade com um pedido GET para o seguinte ponto de extremidade com base na versão do SO:

| Versão do SO | Ponto Final |
|------------|----------|
| Windows 10, versão 1803 ou posterior com a atualização cumulativa mais recente | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Atualizar do Windows 10, versão 1803 ou posterior sem 2018-09 ou cumulativa mais tarde | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, versão 1709 ou anterior | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| O Windows 7 ou Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Certifique-se de que o dispositivo é capaz de comunicar com o serviço. Esta verificação valida alguns, mas nem todos os pontos finais necessários. Para obter mais informações, consulte [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

Para obter mais informações, consulte M365AHandler.log no cliente.  


#### <a name="check-end-user-diagnostic-data"></a>Verifique os dados de diagnóstico do utilizador final
<!--1004-->

Se esta verificação não for bem-sucedida, um utilizador selecionado um inferior dados de diagnóstico Windows no dispositivo.

Consoante os seus requisitos empresariais, pode desativar a opção de usuário por meio da diretiva de grupo. Utilizar a definição para **interface de utilizador de participar da definição de telemetria de configurar**. Para obter mais informações, consulte [dados de diagnóstico de configurar o Windows na sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).


#### <a name="check-user-proxy"></a>Verifique o proxy de usuário
<!--30,35-->

A definição de DisableEnterpriseAuthProxy está ativada por predefinição para o Windows 7. Para computadores Windows 8.1, o Configuration Manager define a definição de DisableEnterpriseAuthProxy para 0 (não desativado).

Esta propriedade pode ser apresentado os seguintes erros:

- Proxy de autenticação está ativada. DisableEnterpriseAuthProxy de conjunto para 0 na `HKLM\Software\Policies\Microsoft\Windows\DataCollection` 

- Não é possível verificar o estado de proxy de autenticação. Verifique os registos para os detalhes da exceção

Para obter mais informações, consulte M365AHandler.log no cliente.  

Verifique as permissões nesta chave de registo. Certifique-se de que a conta sistema local pode aceder a esta chave para o cliente do Configuration Manager definir.  


#### <a name="commercial-id-configuration"></a>Configuração de ID comercial
<!--9, 11, 53--> A Microsoft utiliza um ID comercial exclusivo para mapear informações de dispositivos para a área de trabalho de análise de ambiente de trabalho. Quando integrar o Configuration Manager com a análise de ambiente de trabalho, ele consulta automaticamente o serviço para este ID. O Configuration Manager automaticamente deve aplicar este ID para os clientes para que as definições de análise de ambiente de trabalho de destino. 

Se esta verificação for bem sucedida, em seguida, o dispositivo está corretamente configurado com um ID comercial.

Caso contrário, ele pode mostrar um dos seguintes erros:

- Não é possível escrever o CommercialId chave de registo `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Verifique as permissões  

- Não é possível atualizar o CommercialId na chave do Registro `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Verifique os registos para os detalhes da exceção   

- Forneça o valor correto de CommercialId em `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

Para obter mais informações, consulte M365AHandler.log no cliente.  

Verifique as permissões nesta chave de registo. Certifique-se de que a conta sistema local pode aceder a esta chave para o cliente do Configuration Manager definir.  

Existe um ID diferente para o dispositivo. Esta chave de registo é utilizada pela política de grupo. Ela terá precedência sobre o ID fornecido pelo Configuration Manager.  


Para ver o ID comercial no portal do Analytics de ambiente de trabalho, utilize o seguinte procedimento: 

1. Ir para o portal de análise de ambiente de trabalho e selecione **serviços ligados** no grupo de definições globais.  

2. Na **serviços ligados** painel, o **inscrever dispositivos** painel está selecionado por predefinição. No painel de dispositivos de inscrição, a secção de informações apresenta sua chave ID comercial.  

![Captura de ecrã do ID comercial no portal de análise de ambiente de trabalho](media/commercial-id.png)

> [!Important]  
> Apenas **obter a chave de ID novo** quando não é possível utilizar atual. Se voltar a gerar o ID comercial, implemente o novo ID nos seus dispositivos. Este processo pode resultar na perda de dados de diagnóstico durante a transição.  


#### <a name="windows-commercial-data-opt-in"></a>Windows dados comerciais participar
<!--64-->

Esta propriedade é específica para dispositivos com o Windows 7 ou Windows 8.1. Ele executa testes de semelhantes como [Windows dados de diagnóstico participar](#windows-diagnostic-data-opt-in), exceto para o CommercialDataOptIn valor.


#### <a name="check-device-name-in-diagnostic-data"></a>Verifique o nome do dispositivo em dados de diagnóstico
<!--56,58-->

Se esta verificação for bem sucedida, o dispositivo está corretamente configurado para partilhar o nome do dispositivo.

Caso contrário, ele pode mostrar um dos seguintes erros:

- Não é possível procurar o nome do dispositivo sejam enviados à Microsoft como parte dos dados de diagnóstico do Windows. Verifique os registos para os detalhes da exceção  

- Não é possível escrever a chave de registo AllowDeviceNameInTelemetry `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`. Verifique as permissões  

Para obter mais informações, consulte M365AHandler.log no cliente.  

Verifique as permissões nesta chave de registo. Certifique-se de que a conta sistema local pode aceder a esta chave para o cliente do Configuration Manager definir.  

Certifique-se de que o outro mecanismo de diretiva, como a diretiva de grupo, não está a desativar esta definição. 


#### <a name="diagtrack-service-configuration"></a>Configuração do serviço DiagTrack
<!--44,45,50--> Se esta verificação for bem sucedida, o componente de DiagTrack está corretamente configurado no dispositivo. A versão mínima necessária para análise de ambiente de trabalho é 10010586 (10.0.10586). 

Caso contrário, ele poderá apresentar um dos seguintes erros:

- Ligado a experiência do usuário e o componente de telemetria (diagtrack.dll) está desatualizado. Verificar os requisitos  

- Não é possível localizar o componente de telemetria (diagtrack.dll) e a experiência do usuário conectado. Verificar os requisitos  

- Ativar e iniciar o serviço ligado experiências de utilizador e telemetria para enviar dados à Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Instale as atualizações mais recentes. Para obter mais informações, consulte [atualizações de dispositivo](/sccm/desktop-analytics/enroll-devices#update-devices).

Certifique-se de que o **ligado experiências de utilizador e telemetria** serviço no dispositivo está em execução.

#### <a name="diagtrack-version"></a>Versão de DiagTrack
Esta propriedade apresenta a versão atual do componente ligado a experiência do usuário e a telemetria no dispositivo. Mostra a versão do ficheiro no `%windir%\System32\diagtrack.dll`, sem os pontos decimais. Por exemplo, a versão do ficheiro 10.0.10586 mostra como 10010586. 

#### <a name="sqm-id-retrieval"></a>Obtenção de ID de SQM
<!--38-->

Esta propriedade é principalmente para dispositivos Windows 7. Ela pode ser usada por versões de SO posteriores como um identificador de contingência para o dispositivo. 

Se não for bem sucedida, ele pode ser apresentado o erro seguinte:

- Não é possível obter o identificador de telemetria do dispositivo legado (SQM ID)

Para obter mais informações, consulte M365AHandler.log no cliente.  

Certifique-se de que não ter IDs duplicados no seu ambiente. Por exemplo, se os dispositivos foram implementados com uma imagem de sistema operacional que não foi generalizada. 


#### <a name="unique-device-identifier-retrieval"></a>Obtenção de identificador exclusivo do dispositivo
<!--54--> Análise de área de trabalho utiliza o serviço de Account Microsoft para uma identidade de dispositivo mais confiável. 

Certifique-se de que o **conta de início de sessão no Assistente do Microsoft** serviço não está desativado. O tipo de arranque deve estar **Manual (início de Acionador)**.

Para desativar o acesso de conta Microsoft do utilizador final, utilize definições de política em vez de bloquear este ponto final. Para obter mais informações, consulte [conta da Microsoft na empresa](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).


#### <a name="windows-diagnostic-data-opt-in"></a>Windows dados de diagnóstico participar
<!--8,40,55,62--> Esta propriedade verifica se o Windows está configurado corretamente para permitir que os dados de diagnóstico. Ela verifica o valor de AllowTelemetry nas seguintes chaves de registo:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Verifique as permissões nessas chaves de Registro. Certifique-se de que a conta sistema local pode aceder essas chaves para o cliente do Configuration Manager definir.  

Para obter mais informações, consulte M365AHandler.log no cliente.  


#### <a name="office-diagnostic-endpoint-connectivity"></a>Conectividade de ponto final de diagnóstico do Office
<!-- 1001,1002,1003 -->

Se esta verificação for bem sucedida, o dispositivo é capaz de ligar para os pontos de extremidade diagnóstico do Office. 

Caso contrário, ele pode mostrar um dos seguintes erros:

- Não é possível ligar ao Office diagnóstico ponto final (Aria). Verifique as definições de rede/proxy  

- Não é possível ligar ao Office diagnóstico ponto final (Nexusrules). Verifique as definições de rede/proxy  

- Não é possível ligar ao Office diagnóstico ponto final (Nexus). Verifique as definições de rede/proxy  

Certifique-se de que o dispositivo é capaz de comunicar com o serviço. Para obter mais informações, consulte [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints).  



## <a name="log-files"></a>Ficheiros de registo

Utilize os seguintes ficheiros de registo para ajudar a resolver problemas com a análise de ambiente de trabalho integrado com o Configuration Manager. 


### <a name="service-connection-point"></a>Ponto de ligação de serviço

Os seguintes ficheiros de registo estão no ponto de ligação de serviço no diretório seguinte: `C:\Program Files\Configuration Manager\Logs\M365A`:

| registo | Descrição |
|---------|---------|
| **M365ADeploymentPlanWorker.log** | Informações sobre a sincronização de plano de implementação do ambiente de trabalho Analytics na cloud serviço no local do Configuration Manager |
| **M365ADeviceHealthWorker.log** | Informações sobre o estado de funcionamento do dispositivo carregar do Configuration Manager para a nuvem da Microsoft |
| **M365AUploadWorker.log** | Informações sobre a coleção e o dispositivo carregar do Configuration Manager para a nuvem da Microsoft |


### <a name="configuration-manager-client"></a>Cliente do Configuration Manager

Os seguintes ficheiros de registo estão no cliente do Configuration Manager no diretório seguinte: `C:\Windows\CCM\logs`:

| registo | Descrição |
|---------|---------|
| **M365Handler.log** | Informações sobre a política de definições de análise de ambiente de trabalho |


### <a name="enable-verbose-logging"></a>Ativar registo verboso 

1. No ponto de ligação de serviço, ir para a seguinte chave de registo: `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Definir o **LogLevel** valor `0`  
3. Execute o seguinte comando SQL na base de dados do site:  

    ```SQL
    DELETE FROM M365AProperties WHERE Name = 'M365ATenantUpdateInfo_LastUpdateTime'
    ```

4. Reinicie o **SMS_EXECUTIVE** serviço no servidor do site



## <a name="bkmk_MALogAnalyticsReader"></a> Função de aplicação MALogAnalyticsReader

Quando configura uma análise de ambiente de trabalho, aceita um consentimento em nome da sua organização. Este consentimento é atribuir a aplicação de MALogAnalyticsReader a função de leitor do Log Analytics para a área de trabalho. Esta função de aplicação é necessária ao ambiente de trabalho de análise. 

Se houver um problema com este processo durante o conjunto de cópia de segurança, utilize o seguinte processo para adicionar manualmente esta permissão:

1. Vá para o [portal do Azure](http://portal.azure.com)e selecione **todos os recursos**. Selecione a área de trabalho do tipo **do Log Analytics**.  

2. No menu da área de trabalho, selecione **controlo de acesso (IAM)**, em seguida, selecione **Add**.  

3. Na **adicionar permissões** painel, configure as seguintes definições:  

    - **Função**: **Leitor do log Analytics**  

    - **Atribuir acesso a**: **Utilizador, grupo ou aplicação AD do Azure**  

    - **Selecione**: **MALogAnalyticsReader**  
  
4. Selecione **Guardar**. 

O portal mostra uma notificação que este adicionado a atribuição de função.



---
title: Referência de variável de sequência de tarefas
titleSuffix: Configuration Manager
description: Saiba mais sobre as variáveis para controlar e personalizar uma sequência de tarefas do Configuration Manager.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 62f15230-d3a6-4afc-abd4-1e07e7ba6c97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cfecd7441abd206bdff1d2f6618d763a30dddc51
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/23/2018
ms.locfileid: "42756287"
---
# <a name="task-sequence-variables-in-configuration-manager"></a>Variáveis de sequência de tarefas no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo é uma referência para todas as variáveis disponíveis em ordem alfabética. Utilizar o browser **encontrar** função (normalmente **CTRL** + **F**) para encontrar uma variável específica. As notas de variável se é específico para o passo específico. O artigo sobre [passos de sequência de tarefas](/sccm/osd/understand/task-sequence-steps) inclui a lista de variáveis específicas de cada passo. 

Para obter mais informações, consulte [usando variáveis de sequência de tarefas](/sccm/osd/understand/using-task-sequence-variables).



## <a name="bkmk_tsvar"></a> Referência de variável de sequência de tarefas


### <a name="OSDDetectedWinDir"></a> _OSDDetectedWinDir

 A sequência de tarefas analisa unidades de disco rígido do computador para uma instalação de sistema operativo anterior ao Windows PE é iniciado. A localização da pasta do Windows é armazenada nesta variável. Pode configurar a sequência de tarefas para obter este valor a partir do ambiente e utilizá-la para especificar a localização da pasta Windows utilizada para a nova instalação do sistema operativo.


### <a name="OSDDetectedWinDrive"></a> _OSDDetectedWinDrive

 A sequência de tarefas analisa unidades de disco rígido do computador para uma instalação de sistema operativo anterior ao Windows PE é iniciado. A localização do disco rígido onde o sistema operativo é instalado é armazenada nesta variável. Pode configurar a sequência de tarefas para obter este valor a partir do ambiente e utilizá-la para especificar a localização do disco rígido utilizada para o novo sistema operativo.


### <a name="OSDMigrateUsmtPackageID"></a> _OSDMigrateUsmtPackageID

 *Aplica-se para o [capturar estado do utilizador](task-sequence-steps.md#BKMK_CaptureUserState) passo.*

 (entrada)

 Especifica o ID de pacote do pacote do Configuration Manager que contém os arquivos do USMT. Esta variável é necessária.


### <a name="OSDMigrateUsmtRestorePackageID"></a> _OSDMigrateUsmtRestorePackageID

 *Aplica-se para o [restaurar estado do utilizador](task-sequence-steps.md#BKMK_RestoreUserState) passo.*

 (entrada)

 Especifica o ID de pacote do pacote do Configuration Manager que contém os arquivos do USMT. Esta variável é necessária.


### <a name="SMSTSAdvertID"></a> _SMSTSAdvertID

 Armazena o ID exclusivo de implementação da sequência de tarefas atualmente em execução. Ela usa o mesmo formato como uma implementação de distribuição de software do Configuration Manager. Se a sequência de tarefas for executada a partir de um suporte de dados autónomo, esta variável é indefinida.

 #### <a name="example"></a>Exemplo
 `ABC20001`


### <a name="SMSTSAssetTag"></a> _SMSTSAssetTag

 *Aplica-se para o [definir variáveis dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables) passo.*

 Especifica a etiqueta de ativo para o computador.


### <a name="SMSTSBootImageID"></a> _SMSTSBootImageID

 Se a sequência de tarefas em execução atual fizer referência a um pacote de imagem de arranque, esta variável armazena o ID de pacote de imagem do arranque. Se a sequência de tarefas não referencia um pacote de imagem de arranque, esta variável não está definida.

 #### <a name="example"></a>Exemplo
 `ABC00001`  


### <a name="SMSTSBootUEFI"></a> Smstsbootuefi sempre

 A sequência de tarefas define esta variável que Deteta um computador que esteja no modo UEFI.


### <a name="SMSTSClientGUID"></a> _SMSTSClientGUID

 Armazena o valor de GUID do cliente do Configuration Manager. Se a sequência de tarefas for executada a partir de mídia autônoma, esta variável não está definida.

 #### <a name="example"></a>Exemplo
 `0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`


### <a name="SMSTSCurrentActionName"></a> Smstscurrentactionname

 Especifica o nome do passo da sequência de tarefas em execução atual. Esta variável é definida antes de o gestor da sequência de tarefas executar cada passo individual.

 #### <a name="example"></a>Exemplo
 `run command line`


### <a name="SMSTSDefaultGateways"></a> _SMSTSDefaultGateways

 *Aplica-se para o [definir variáveis dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables) passo.*

 Especifica os gateways predefinidos utilizados pelo computador.


### <a name="SMSTSDownloadOnDemand"></a> _SMSTSDownloadOnDemand

 Se a sequência de tarefas atual for executada no modo de transferência sob demanda, esta variável é `true`. Modo de transferência sob demanda significa que o Gestor da sequência de tarefas transfere o conteúdo localmente, apenas quando precisa de aceder o conteúdo.


### <a name="SMSTSInWinPE"></a> Smstsinwinpe

 Quando o passo de sequência de tarefas atual for executada no Windows PE, esta variável é `true`. Teste esta variável de sequência de tarefas para determinar o ambiente de sistema operacional atual.


### <a name="SMSTSIPAddresses"></a> _SMSTSIPAddresses

 *Aplica-se para o [definir variáveis dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables) passo.*

 Especifica os endereços IP utilizados pelo computador.


### <a name="SMSTSLastActionRetCode"></a> _SMSTSLastActionRetCode

 Armazena o código de retorno da última ação executada. Esta variável pode ser utilizada como uma condição para determinar se o próximo passo é executado.

 #### <a name="example"></a>Exemplo
 `0`


### <a name="SMSTSLastActionSucceeded"></a> _SMSTSLastActionSucceeded

 - Se a última etapa foi concluída com êxito, esta variável é `true`.  

 - Se tiver o último passo falhado, ele tem `false`.  

 - Se a sequência de tarefas ignorou a última ação, porque o passo está desativado ou a condição associada estava avaliada como **false**, esta variável não for redefinida. Que ainda retém o valor da ação anterior.  

 
### <a name="SMSTSLaunchMode"></a> Smstslaunchmode

 Especifica que a sequência de tarefas é iniciada através de um dos seguintes métodos:  

 - **SMS**: O cliente de Configuration Manager, como quando um usuário inicia-lo a partir do Centro de Software
 - **PEN USB**: Suporte de dados USB legado
 - **PEN USB + FORMATO**: Suporte de dados mais recentes do USB
 - **CD**: Um CD inicializável
 - **DVD**: Um DVD inicializável
 - **PXE**: Arranque de rede com PXE
 - **HD**: Suportes de dados num disco rígido


### <a name="SMSTSLogPath"></a> Smstslogpath

 Armazena o caminho completo do diretório de registo. Utilize este valor para determinar onde os passos de sequência de tarefas iniciar suas ações. Este valor não é definido quando uma unidade de disco rígido não está disponível.


### <a name="SMSTSMacAddresses"></a> _SMSTSMacAddresses

 *Aplica-se para o [definir variáveis dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables) passo.*

 Especifica os endereços MAC utilizados pelo computador.


### <a name="SMSTSMachineName"></a> Smstsmachinename

 Armazena e especifica o nome do computador. Armazena o nome do computador que a sequência de tarefas utiliza para registar todas as mensagens de estado. Para alterar o nome do computador em que o novo sistema operacional, utilize o [OSDComputerName](#OSDComputerName) variável.


### <a name="SMSTSMake"></a> _SMSTSMake

 *Aplica-se para o [definir variáveis dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables) passo.*

 Especifica a marca do computador.


### <a name="SMSTSMDataPath"></a> Smstsmdatapath

 Especifica o caminho definido pela [SMSTSLocalDataDrive](#SMSTSLocalDataDrive) variável. Ao definir SMSTSLocalDataDrive antes da sequência de tarefas é iniciada, como, definindo uma variável de coleção do Configuration Manager, em seguida, define a variável smstsmdatapath assim que a sequência de tarefas for iniciada.


### <a name="SMSTSMediaType"></a> Smstsmediatype

 Especifica o tipo de suporte de dados que é utilizado para iniciar a instalação. Exemplos de tipos de suportes de dados: Suporte de Dados de Arranque, Suporte de Dados Completo, PXE e Suporte de Dados Pré-configurado.


### <a name="SMSTSModel"></a> _SMSTSModel

 *Aplica-se para o [definir variáveis dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables) passo.*

 Especifica o modelo do computador.


### <a name="SMSTSMP"></a> _SMSTSMP

 Armazena o URL ou endereço IP de um ponto de gestão do Configuration Manager.


### <a name="SMSTSMPPort"></a> _SMSTSMPPort

 Arquivos de ponto do número de porta de um gestão do Configuration Manager.


### <a name="SMSTSOrgName"></a> Smstsorgname

 Armazena o nome do título imagem corporativa que a sequência de tarefas exibe na caixa de diálogo de progresso.


### <a name="SMSTSOSUpgradeActionReturnCode"></a> _SMSTSOSUpgradeActionReturnCode

 *Aplica-se para o [atualizar sistema operativo](task-sequence-steps.md#BKMK_UpgradeOS) passo.*

 Armazena o valor de código de saída que retorna do programa de configuração do Windows para indicar êxito ou falha. Esta variável é útil com o `/Compat` opção da linha de comandos.

 #### <a name="example"></a>Exemplo
 Na conclusão de uma análise somente de compatibilidade, tome medidas em passos posteriores consoante o código de saída de falha ou êxito. Em caso de êxito, inicie a atualização. Ou definir um marcador no ambiente de recolher com o inventário de hardware. Por exemplo, adicione um ficheiro ou definir uma chave de registo. Utilize este marcador para criar uma coleção de computadores que estão prontos para atualização ou que requerem uma ação antes da atualização.


### <a name="SMSTSPackageID"></a> _SMSTSPackageID

 Armazena o ID da sequência de tarefas atualmente em execução. Este ID utiliza o mesmo formato que um ID de pacote do Configuration Manager. 

 #### <a name="example"></a>Exemplo
 `HJT00001`


### <a name="SMSTSPackageName"></a> _SMSTSPackageName

 Armazena o nome de sequência de tarefas em execução atual. Um administrador do Configuration Manager especifica este nome ao criar a sequência de tarefas.

 #### <a name="example"></a>Exemplo
 `Deploy Windows 10 task sequence`


### <a name="SMSTSRunFromDP"></a> _SMSTSRunFromDP

 Definido como `true` se a sequência de tarefas atual for executada no modo de execução-de-ponto de distribuição. Este modo significa que o Gestor da sequência de tarefas obtém partilhas de pacotes do ponto de distribuição.


### <a name="SMSTSSerialNumber"></a> _SMSTSSerialNumber

 *Aplica-se para o [definir variáveis dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables) passo.*

 Especifica o número de série do computador.


### <a name="SMSTSSetupRollback"></a> _SMSTSSetupRollback

 Especifica se o programa de configuração do Windows executada uma operação de reversão durante uma atualização no local. Os valores das variáveis podem ser `true` ou `false`.


### <a name="SMSTSSiteCode"></a> _SMSTSSiteCode

 Armazena o código do site do site do Configuration Manager.

 #### <a name="example"></a>Exemplo
 `ABC`


### <a name="SMSTSTimezone"></a> Smststimezone

 Esta variável armazena as informações de fuso horário no seguinte formato: 

 ```
 Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName
 ```

 #### <a name="example"></a>Exemplo
 Para o fuso horário **hora do Leste (E.U.A. e Canadá)**: 

 ```
 300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time
 ```


### <a name="SMSTSType"></a> _SMSTSType

 Especifica o tipo da sequência de tarefas atualmente em execução. Ele pode ter um dos seguintes valores:  

 - **1**: Uma sequência de tarefas genérica
 - **2**: Uma sequência de tarefas de implementação do SO


### <a name="SMSTSUseCRL"></a> _SMSTSUseCRL

 Quando a sequência de tarefas utiliza HTTPS para comunicar com o ponto de gestão, esta variável Especifica se ele usa a lista de revogação de certificados (CRL).


### <a name="SMSTSUserStarted"></a> _SMSTSUserStarted

 Especifica se um utilizador iniciar a sequência de tarefas. Esta variável é definida apenas se a sequência de tarefas é iniciada a partir do Centro de Software. Por exemplo, se [smstslaunchmode](#SMSTSLaunchMode) está definida como `SMS`. 

 Esta variável pode ter os seguintes valores:  

 - `true`: Especifica que a sequência de tarefas é iniciada manualmente por um utilizador no Centro de Software.  

 - `false`: Especifica que a sequência de tarefas é iniciada automaticamente pelo agendador do Configuration Manager.


### <a name="SMSTSUseSSL"></a> _SMSTSUseSSL

 Especifica se a sequência de tarefas utiliza SSL para comunicar com o ponto de gestão do Configuration Manager. Se configurar os sistemas de sites para HTTPS, o valor é definido como `true`.


### <a name="SMSTSUUID"></a> _SMSTSUUID

 *Aplica-se para o [definir variáveis dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables) passo.*

 Especifica o UUID do computador.


### <a name="SMSTSWTG"></a> SMSTSWTG

 Especifica se o computador está a ser executado como um dispositivo Windows To Go.


### <a name="TSAppInstallStatus"></a> Tsappinstallstatus

 A sequência de tarefas define esta variável com o estado da instalação para o aplicativo durante a [instalar aplicação](task-sequence-steps.md#BKMK_InstallApplication) passo. Ele define um dos seguintes valores:  

 - **Indefinido**: O passo instalar aplicação não tiver sido executada.  

 - **Erro**: Pelo menos uma aplicação falha devido a um erro durante o passo instalar aplicação.  

 - **Aviso**: Nenhum erro ocorreu durante o passo instalar aplicação. Uma ou mais aplicações ou uma dependência necessária não tiver instalado porque não foi cumprido um requisito.  

 - **Êxito**: Não há erros ou avisos detetados durante o passo instalar aplicação.  


### <a name="OSDAdapter"></a> OSDAdapter

 *Aplica-se para o [aplicar definições de rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings) passo.*

 (entrada)

 Esta variável de sequência de tarefas é uma *matriz* variável. Cada elemento da matriz representa as definições para um adaptador de rede individual no computador. Aceder às definições para cada adaptador ao combinar o nome da variável de matriz com o índice de adaptador de rede baseado em zero e o nome da propriedade.

 Se o passo aplicar definições de rede configura vários adaptadores de rede, ele define as propriedades para o *segunda* placa de rede ao utilizar o índice **1** no nome da variável. Por exemplo: OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList e OSDAdapter1DNSDomain.

 Utilize os seguintes nomes de variáveis para definir as propriedades do *primeiro* adaptador de rede para o passo para configurar:

#### <a name="osdadapter0enabledhcp"></a>OSDAdapter0EnableDHCP
 Esta definição é obrigatória. Os valores possíveis são `True` ou `False`. Por exemplo:

 `true`: Ativar o protocolo de configuração dinâmica de anfitrião (DHCP) para o adaptador

#### <a name="osdadapter0ipaddresslist"></a>OSDAdapter0IPAddressList
 Lista delimitada por vírgulas de endereços IP para o adaptador. Esta propriedade é ignorada, a menos que **EnableDHCP** está definida como `false`. Esta definição é obrigatória.

#### <a name="osdadapter0subnetmask"></a>OSDAdapter0SubnetMask
 Lista delimitada por vírgulas de máscaras de sub-rede. Esta propriedade é ignorada, a menos que **EnableDHCP** está definida como `false`. Esta definição é obrigatória.

#### <a name="osdadapter0gateways"></a>OSDAdapter0Gateways
 Lista delimitada por vírgulas de endereços de gateway IP. Esta propriedade é ignorada, a menos que **EnableDHCP** está definida como `false`. Esta definição é obrigatória.

#### <a name="osdadapter0dnsdomain"></a>OSDAdapter0DNSDomain
 Domínio de sistema de nomes (DNS) de domínio para o adaptador.

#### <a name="osdadapter0dnsserverlist"></a>OSDAdapter0DNSServerList
 Lista delimitada por vírgulas de servidores DNS para o adaptador. Esta definição é obrigatória.

#### <a name="osdadapter0enablednsregistration"></a>OSDAdapter0EnableDNSRegistration
 Definido como `true` para registar o endereço IP para o adaptador no DNS.

#### <a name="osdadapter0enablefulldnsregistration"></a>OSDAdapter0EnableFullDNSRegistration
 Definido como `true` para registar o endereço IP para o adaptador no DNS com o nome DNS completo para o computador.

#### <a name="osdadapter0enableipprotocolfiltering"></a>OSDAdapter0EnableIPProtocolFiltering
 Definido como `true` para ativar a filtragem no adaptador de protocolo IP.

#### <a name="osdadapter0ipprotocolfilterlist"></a>OSDAdapter0IPProtocolFilterList
 Lista delimitada por vírgulas de protocolos podem ser executados por IP. Esta propriedade é ignorada se **EnableIPProtocolFiltering** está definida como `false`.

#### <a name="osdadapter0enabletcpfiltering"></a>OSDAdapter0EnableTCPFiltering
 Definido como `true` para ativar a filtragem para o adaptador de porta TCP.

#### <a name="osdadapter0tcpfilterportlist"></a>OSDAdapter0TCPFilterPortList
 Lista delimitada por vírgulas de portas para serão concedidas permissões de acesso por TCP. Esta propriedade é ignorada se **EnableTCPFiltering** está definida como `false`.

#### <a name="osdadapter0tcpipnetbiosoptions"></a>OSDAdapter0TcpipNetbiosOptions
 Opções para NetBIOS por TCP/IP. Os valores possíveis são:  

 - `0`: Utilizar definições NetBIOS do servidor DHCP  
 - `1`: Ativar o NetBIOS sobre TCP/IP  
 - `2`: Desativar NetBIOS por TCP/IP  

#### <a name="osdadapter0enablewins"></a>OSDAdapter0EnableWINS
 Definido como `true` para utilizar WINS para resolução de nomes.

#### <a name="osdadapter0winsserverlist"></a>OSDAdapter0WINSServerList
 Lista delimitada por vírgulas de endereços IP do servidor WINS. Esta propriedade é ignorada, a menos que **EnableWINS** está definida como `true`.

#### <a name="osdadapter0macaddress"></a>OSDAdapter0MacAddress
 Endereço de MAC utilizado para corresponder as definições para o adaptador de rede física.

#### <a name="osdadapter0name"></a>OSDAdapter0Name
 O nome da ligação de rede como ele aparece no programa de painel de controlo de ligações de rede. O nome é entre 0 e 255 carateres de comprimento.

#### <a name="osdadapter0index"></a>OSDAdapter0Index
 Índice das definições de adaptador de rede na matriz de definições.

#### <a name="example"></a>Exemplo
 - **OSDAdapterCount** = `1`  
 - **OSDAdapter0EnableDHCP** = `FALSE`  
 - **OSDAdapter0IPAddressList** = `192.168.0.40`  
 - **OSDAdapter0SubnetMask** = `255.255.255.0`  
 - **OSDAdapter0Gateways** = `192.168.0.1`  
 - **OSDAdapter0DNSSuffix** = `contoso.com`  


### <a name="OSDAdapterCount"></a> OSDAdapterCount

 *Aplica-se para o [aplicar definições de rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings) passo.*

 (entrada)

 Especifica o número de adaptadores de rede instalados no computador de destino. Ao definir o **OSDAdapterCount** valor, defina também a todas as opções de configuração para cada adaptador. 

 Por exemplo, se definir o **OSDAdapter0TCPIPNetbiosOptions** o valor para o primeiro adaptador, tem de configurar todos os valores para esse adaptador.

 Se não especificar este valor, a sequência de tarefas ignora todos **OSDAdapter** valores.


### <a name="OSDApplyDriverBootCriticalContentUniqueID"></a> OSDApplyDriverBootCriticalContentUniqueID

 *Aplica-se para o [aplicar pacote de controlador](task-sequence-steps.md#BKMK_ApplyDriverPackage) passo.*

 (entrada)

 Especifica o ID de conteúdo do controlador de dispositivo de armazenamento em massa a instalar a partir do pacote de controlador. Se esta variável não for especificada, é instalado nenhum controlador de armazenamento em massa.


### <a name="OSDApplyDriverBootCriticalHardwareComponent"></a> OSDApplyDriverBootCriticalHardwareComponent

 *Aplica-se para o [aplicar pacote de controlador](task-sequence-steps.md#BKMK_ApplyDriverPackage) passo.*

 (entrada)

 Especifica se um driver de dispositivo de armazenamento em massa está instalado, esta variável tem de ser **scsi**.

 Se [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) é definido, esta variável é necessária.


### <a name="OSDApplyDriverBootCriticalID"></a> OSDApplyDriverBootCriticalID

 *Aplica-se para o [aplicar pacote de controlador](task-sequence-steps.md#BKMK_ApplyDriverPackage) passo.*

 (entrada)

 Especifica o ID crítico de arranque do controlador de dispositivo de armazenamento em massa a instalar. Este ID está listado na **scsi** secção do ficheiro Txtsetup OEM do controlador de dispositivo.

 Se [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) é definido, esta variável é necessária.

### <a name="OSDApplyDriverBootCriticalINFFile"></a> OSDApplyDriverBootCriticalINFFile

 *Aplica-se para o [aplicar pacote de controlador](task-sequence-steps.md#BKMK_ApplyDriverPackage) passo.*

 (entrada)

 Especifica o ficheiro INF do controlador de armazenamento em massa a instalar.

 Se [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) é definido, esta variável é necessária.


### <a name="OSDAutoApplyDriverBestMatch"></a> OSDAutoApplyDriverBestMatch

 *Aplica-se para o [aplicar controladores automaticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers) passo.*

 (entrada)

 Se existirem vários controladores de dispositivo no catálogo de controladores que são compatíveis com um dispositivo de hardware, esta variável determina a ação de um passo. 

 #### <a name="valid-values"></a>Valores válidos
 - `true` (predefinição): Instalar apenas o melhor controlador de dispositivo  

 - `false`: Instala todos os drivers de dispositivo compatível e Windows escolhe o controlador mais adequado para utilizar  


### <a name="OSDAutoApplyDriverCategoryList"></a> OSDAutoApplyDriverCategoryList

 *Aplica-se para o [aplicar controladores automaticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers) passo.*

 (entrada)

 Uma lista delimitada por vírgulas dos IDs exclusivos das categorias do catálogo de controladores. O **aplicar controladores automaticamente** passo apenas os controladores de, pelo menos, uma das categorias especificadas. Este valor é opcional e não está definida por predefinição. Para obter os IDs de categorias disponíveis, a enumeração da lista de **SMS_CategoryInstance** objetos no site.


### <a name="OSDBitLockerRecoveryPassword"></a> OSDBitLockerRecoveryPassword

 *Aplica-se para o [Enable BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker) passo.*

 (entrada)

 Em vez de gerar uma palavra-passe de recuperação aleatória, a **Enable BitLocker** passo utiliza o valor especificado como a palavra-passe de recuperação. O valor tem de ser uma palavra-passe de recuperação do BitLocker numérica válida.


### <a name="OSDBitLockerStartupKey"></a> OSDBitLockerStartupKey

 *Aplica-se para o [Enable BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker) passo.*

 (entrada)

 Em vez de gerar uma chave de arranque aleatória para a opção de gestão de chaves **chave de arranque em USB apenas** a **ativar BitLocker** passo utiliza o Trusted Platform Module (TPM) como chave de arranque. O valor tem de ser uma chave de arranque do BitLocker codificada em Base64 de 256 bits válida.


### <a name="OSDCaptureAccount"></a> OSDCaptureAccount

 *Aplica-se para o [Capturar imagem do SO](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) passo.*

 (entrada)

 Especifica um nome de conta do Windows que tem permissões para armazenar a imagem capturada numa partilha de rede ([OSDCaptureDestination](#OSDCaptureDestination)). Especifique também a [OSDCaptureAccountPassword](#OSDCaptureAccountPassword).

 Para obter mais informações sobre a conta de imagem do sistema operacional de captura, consulte [contas](/sccm/core/plan-design/hierarchy/accounts#capture-operating-system-image-account).


### <a name="OSDCaptureAccountPassword"></a> OSDCaptureAccountPassword

 *Aplica-se para o [Capturar imagem do SO](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) passo.*

 (entrada)

 Especifica a palavra-passe para a conta do Windows ([OSDCaptureAccount](#OSDCaptureAccount)) utilizado para armazenar a imagem capturada numa partilha de rede ([OSDCaptureDestination](#OSDCaptureDestination)).


### <a name="OSDCaptureDestination"></a> OSDCaptureDestination

 *Aplica-se para o [Capturar imagem do SO](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) passo.*

 (entrada)

 Especifica a localização em que a sequência de tarefas salva a imagem capturada do sistema operacional. O comprimento máximo do nome do diretório é 255 carateres. Se a partilha de rede requer autenticação, especifique a [OSDCaptureAccount](#OSDCaptureAccount) e [OSDCaptureAccountPassword](#OSDCaptureAccountPassword) variáveis.


### <a name="OSDComputerName-input"></a> OSDComputerName (entrada)

 *Aplica-se para o [aplicar definições do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) passo.*

 Especifica o nome do computador de destino.

 #### <a name="example"></a>Exemplo
 `%_SMSTSMachineName%` (predefinição)


### <a name="OSDComputerName-output"></a> OSDComputerName (saída)

 *Aplica-se para o [capturar definições do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings) passo.*

 Definida como o nome NetBIOS do computador. O valor é definido apenas se o [OSDMigrateComputerName](#OSDMigrateComputerName) variável é definida como `true`.


### <a name="OSDConfigFileName"></a> OSDConfigFileName

 *Aplica-se para o [aplicar imagem do SO](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) passo.*

 (entrada)

 Especifica o nome de ficheiro do arquivo de resposta de implementação do sistema operacional associado com o pacote de imagem de implantação do sistema operacional.  


### <a name="OSDDataImageIndex"></a> OSDDataImageIndex

 *Aplica-se para o [aplicar imagem de dados](task-sequence-steps.md#BKMK_ApplyDataImage) passo.*

 (entrada)

 Especifica o valor de índice da imagem que é aplicada ao computador de destino.


### <a name="OSDDiskIndex"></a> OSDDiskIndex

 *Aplica-se para o [formatar e particionar disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk) passo.*

 (entrada)

 Especifica o número do disco físico a particionar.


### <a name="OSDDNSDomain"></a> OSDDNSDomain

 *Aplica-se para o [aplicar definições de rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings) passo.*

 (entrada)

 Especifica o servidor DNS primário que utiliza o computador de destino.


### <a name="OSDDNSSuffixSearchOrder"></a> OSDDNSSuffixSearchOrder

 *Aplica-se para o [aplicar definições de rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings) passo.*

 (entrada)

 Especifica a ordem de procura DNS para o computador de destino.


### <a name="OSDDomainName"></a> OSDDomainName

 *Aplica-se para o [aplicar definições de rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings) passo.*

 (entrada)

 Especifica o nome de domínio do Active Directory que o computador de destino junta. O valor especificado tem de ser um nome de domínio de Serviços de Domínio do Active Directory válido.


### <a name="OSDDomainOUName"></a> OSDDomainOUName

 *Aplica-se para o [aplicar definições de rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings) passo.*

 (entrada)

 Especifica o nome do formato RFC 1779 da unidade organizacional (UO) ao qual o computador de destino é associado. Se for especificado, o valor tem de conter o caminho completo.

 #### <a name="example"></a>Exemplo
 `LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`


### <a name="OSDDoNotLogCommand"></a> OSDDoNotLogCommand
 <!--1358493--> *A partir da versão 1806*  
 *Aplica-se para o [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) passo.*

 (entrada)

 Para impedir que os dados potencialmente confidenciais sejam apresentadas ou com sessão iniciada, definir esta variável como `TRUE`. Esta variável dissimula o nome do programa no **smsts** durante um [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) passo de sequência de tarefas.   


### <a name="OSDEnableTCPIPFiltering"></a> OSDEnableTCPIPFiltering

 *Aplica-se para o [aplicar definições de rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings) passo.*

 (entrada)

 Especifica se a filtragem TCP/IP está ativada.

 #### <a name="valid-values"></a>Valores válidos
 - `true`  
 - `false` (predefinição)  


### <a name="OSDGPTBootDisk"></a> OSDGPTBootDisk

 *Aplica-se para o [formatar e particionar disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk) passo.*

 (entrada)

 Especifica se pretende criar uma partição EFI num disco rígido GPT. Computadores baseados em EFI utilizam esta partição como disco de arranque.

 #### <a name="valid-values"></a>Valores válidos
 - `true`  
 - `false` (predefinição)


### <a name="OSDImageCreator"></a> OSDImageCreator

 *Aplica-se para o [Capturar imagem do SO](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) passo.*

 (entrada)

 Um nome opcional do utilizador que criou a imagem. Este nome é armazenado no ficheiro WIM. O comprimento máximo do nome de utilizador é 255 carateres.


### <a name="OSDImageDescription"></a> OSDImageDescription

 *Aplica-se para o [Capturar imagem do SO](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) passo.*

 (entrada)

 Uma utilizador-Descrição opcional definida da imagem capturada do sistema operacional. Esta descrição é armazenada no ficheiro WIM. O comprimento máximo da descrição é 255 carateres.


### <a name="OSDImageIndex"></a> OSDImageIndex

 *Aplica-se para o [aplicar imagem do SO](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) passo.*

 (entrada)

 Especifica o valor de índice da imagem do ficheiro WIM que é aplicado ao computador de destino.


### <a name="OSDImageVersion"></a> OSDImageVersion

 *Aplica-se para o [Capturar imagem do SO](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) passo.*

 (entrada)

 Um número de versão opcional definido pelo utilizador para atribuir à imagem capturada do sistema operacional. Este número de versão é armazenado no ficheiro WIM. Este valor pode ser qualquer combinação de carateres de alfanuméricos com um comprimento máximo de 32.


### <a name="OSDInstallDriversAdditionalOptions"></a> OSDInstallDriversAdditionalOptions
<!--516679/2840016--> *A partir da versão 1806*  
 *Aplica-se para o [aplicar pacote de controlador](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage) passo.*

 (entrada)

 Especifica opções adicionais para adicionar à linha de comando DISM ao aplicar um pacote de controladores. A sequência de tarefas não verifica as opções da linha de comandos. 

 Para utilizar esta variável, ative a definição **pacote de controladores de instalação através da execução do DISM com a opção recurse**, na **aplicar pacote de controlador** passo. 

 Para obter mais informações, consulte [opções de linha de comandos DISM do Windows 10](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).


### <a name="OSDJoinAccount"></a> OSDJoinAccount

 *Aplica-se para os seguintes passos:*  
 - [Aplicar definições de rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings)   
 - [Associar domínio ou grupo de trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  


 (entrada)

 Especifica a conta de utilizador de domínio que é utilizada para adicionar o computador de destino ao domínio. Esta variável é necessária ao associar um domínio.

 Para obter mais informações sobre o domínio de sequência de tarefas associar a conta, consulte [contas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-domain-joining-account).


### <a name="OSDJoinDomainName"></a> OSDJoinDomainName

 *Aplica-se para o [associar domínio ou grupo de trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) passo.*

 (entrada)

 Especifica o nome de domínio do Active Directory, o computador de destino associações. O comprimento do nome do domínio tem de ser entre 1 e 255 carateres.


### <a name="OSDJoinDomainOUName"></a> OSDJoinDomainOUName

 *Aplica-se para o [associar domínio ou grupo de trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) passo.*

 (entrada)

 Especifica o nome do formato RFC 1779 da unidade organizacional (UO) ao qual o computador de destino é associado. Se for especificado, o valor tem de conter o caminho completo. O comprimento do nome do UO tem de ser entre 0 e 32.767 carateres. Este valor não é definido se o [OSDJoinType](#OSDJoinType) variável é definida como `1` (associação a um grupo de trabalho).

 #### <a name="example"></a>Exemplo
 `LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

  
### <a name="OSDJoinPassword"></a> OSDJoinPassword

 *Aplica-se para os seguintes passos:*  
 - [Aplicar definições de rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
 - [Associar domínio ou grupo de trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  


 (entrada)

 Especifica a palavra-passe para o [OSDJoinAccount](#OSDJoinAccount) que o computador de destino usa para ingressar no domínio do Active Directory. Se o ambiente de sequência de tarefas não inclui esta variável, o programa de configuração do Windows tenta uma palavra-passe em branco. Se a variável [OSDJoinType](#OSDJoinType) variável é definida como `0` (associar domínio), este valor é necessário.


### <a name="OSDJoinSkipReboot"></a> OSDJoinSkipReboot

 *Aplica-se para o [associar domínio ou grupo de trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) passo.*

 (entrada)

 Especifica se pretende ignorar o reinício após o computador de destino ser associado ao domínio ou grupo de trabalho.

 #### <a name="valid-values"></a>Valores válidos
 - `true`  
 - `false`  


### <a name="OSDJoinType"></a> OSDJoinType

 *Aplica-se para o [associar domínio ou grupo de trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) passo.*

 (entrada)

 Especifica se o computador de destino é associado a um domínio Windows ou a um grupo de trabalho. 

 #### <a name="valid-values"></a>Valores válidos
 - `0`: Associar o computador de destino a um domínio do Windows  
 - `1`: Associar o computador de destino a um grupo de trabalho  


### <a name="OSDJoinWorkgroupName"></a> OSDJoinWorkgroupName

 *Aplica-se para o [associar domínio ou grupo de trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) passo.*

 (entrada)

 Especifica o nome de um grupo de trabalho ao qual o computador de destino é associado. O comprimento do nome do grupo de trabalho tem de ser entre 1 e 32 carateres.


### <a name="OSDKeepActivation"></a> OSDKeepActivation

 *Aplica-se para o [preparar Windows para captura](task-sequence-steps.md#BKMK_PrepareWindowsforCapture) passo.*

 (entrada)

 Especifica se o sysprep repõe o sinalizador de ativação do produto.

 #### <a name="valid-values"></a>Valores válidos
 - `true`
 - `false` (predefinição)


### <a name="OSDLocalAdminPassword"></a> OSDLocalAdminPassword

 *Aplica-se para o [aplicar definições do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) passo.*

 (entrada)

 Especifica a palavra-passe da conta de administrador local. Se ativar a opção para **aleatoriamente gerar a palavra-passe de administrador local e desativar a conta nas plataformas suportadas**, em seguida, o passo ignora esta variável. O valor especificado tem de ter entre 1 e 255 carateres.


### <a name="OSDMigrateAdapterSettings"></a> OSDMigrateAdapterSettings

 *Aplica-se para o [capturar definições de rede](task-sequence-steps.md#BKMK_CaptureNetworkSettings) passo.*

 (entrada)

 Especifica se a sequência de tarefas captura as informações da placa de rede. Estas informações incluem definições de configuração de TCP/IP, DNS e WINS.

 #### <a name="valid-values"></a>Valores válidos
 - `true` (predefinição)
 - `false`


### <a name="OSDMigrateAdditionalCaptureOptions"></a> OSDMigrateAdditionalCaptureOptions

 *Aplica-se para o [capturar estado do utilizador](task-sequence-steps.md#BKMK_CaptureUserState) passo.*

 (entrada)

 Especifica opções de linha de comandos adicionais para a ferramenta de migração do Estado utilizador (USMT), a sequência de tarefas utiliza para capturar o estado do utilizador. O passo não expõe estas definições no editor de sequência de tarefas. Especifica estas opções como uma cadeia de caracteres, a sequência de tarefas acrescenta à linha de comando USMT gerada automaticamente para o ScanState.

 As opções da USMT especificadas com esta variável de sequência de tarefas não são validadas para maior precisão, antes de executar a sequência de tarefas.

 Para obter mais informações sobre as opções disponíveis, consulte [sintaxe do ScanState](https://docs.microsoft.com/windows/deployment/usmt/usmt-scanstate-syntax).


### <a name="OSDMigrateAdditionalRestoreOptions"></a> OSDMigrateAdditionalRestoreOptions

 *Aplica-se para o [restaurar estado do utilizador](task-sequence-steps.md#BKMK_RestoreUserState) passo.*

 (entrada)

 Especifica opções da linha de comandos adicionais para a ferramenta de migração do Estado utilizador (USMT), a sequência de tarefas utiliza ao restaurar o estado do utilizador. Especifica as opções adicionais como uma cadeia de caracteres, a sequência de tarefas acrescenta à linha de comando USMT gerada automaticamente para o LoadState. 

 As opções da USMT especificadas com esta variável de sequência de tarefas não são validadas para maior precisão, antes de executar a sequência de tarefas.

 Para obter mais informações sobre as opções disponíveis, consulte [sintaxe do LoadState](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax).


### <a name="OSDMigrateComputerName"></a> OSDMigrateComputerName

 *Aplica-se para o [capturar definições do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings) passo.*

 (entrada)

 Especifica se o nome do computador é migrado.

 #### <a name="valid-values"></a>Valores válidos
 - `true` (predefinição). O [OSDComputerName (saída)](#OSDComputerName-output) variável é definida como o nome NetBIOS do computador.  
 - `false`   


### <a name="OSDMigrateConfigFiles"></a> OSDMigrateConfigFiles

 *Aplica-se para o [capturar estado do utilizador](task-sequence-steps.md#BKMK_CaptureUserState) passo.*

 (entrada)

 Especifica os ficheiros de configuração utilizados para controlar a captura de perfis de utilizador. Esta variável é utilizada apenas se [OSDMigrateMode](#OSDMigrateMode) está definida como `Advanced`. Este valor da lista delimitada por vírgulas está definido para efetuar a migração personalizada de perfis de utilizador.

 #### <a name="example"></a>Exemplo
 `miguser.xml,migsys.xml,migapps.xml`  


### <a name="OSDMigrateContinueOnLockedFiles"></a> OSDMigrateContinueOnLockedFiles

 *Aplica-se para o [capturar estado do utilizador](task-sequence-steps.md#BKMK_CaptureUserState) passo.*

 (entrada)

 Se o USMT não é possível capturar alguns ficheiros, esta variável permite a captura de estado de utilizador continuar. 

 #### <a name="valid-values"></a>Valores válidos
 - `true` (predefinição)  
 - `false`   


### <a name="OSDMigrateContinueOnRestore"></a> OSDMigrateContinueOnRestore

 *Aplica-se para o [restaurar estado do utilizador](task-sequence-steps.md#BKMK_RestoreUserState) passo.*

 (entrada)

 Continue o processo, mesmo que o USMT não é possível restaurar alguns ficheiros.

 #### <a name="valid-values"></a>Valores válidos
 - `true` (predefinição)  
 - `false`  


### <a name="OSDMigrateEnableVerboseLogging"></a> OSDMigrateEnableVerboseLogging

 *Aplica-se para os seguintes passos:*  
 - [Capturar estado do utilizador](task-sequence-steps.md#BKMK_CaptureUserState)  
 - [Restaurar estado do utilizador](task-sequence-steps.md#BKMK_RestoreUserState)  


 (entrada)

 Ativa o registo verboso do USMT. A etapa requer este valor.

 #### <a name="valid-values"></a>Valores válidos
 - `true`  
 - `false` (predefinição)  


### <a name="OSDMigrateLocalAccounts"></a> OSDMigrateLocalAccounts

 *Aplica-se para o [restaurar estado do utilizador](task-sequence-steps.md#BKMK_RestoreUserState) passo.*

 (entrada)

 Especifica se a conta de computador local é restaurada.

 #### <a name="valid-values"></a>Valores válidos
 - `true`  
 - `false` (predefinição)  


### <a name="OSDMigrateLocalAccountPassword"></a> OSDMigrateLocalAccountPassword

 *Aplica-se para o [restaurar estado do utilizador](task-sequence-steps.md#BKMK_RestoreUserState) passo.*

 (entrada)

 Se o [OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) variável é `true`, esta variável tem de conter a palavra-passe atribuída ao *todos os* migrados contas locais. USMT atribui a mesma palavra-passe para todas as contas locais migradas. Considere esta palavra-passe como temporário e alterá-la mais tarde por algum outro método.


### <a name="OSDMigrateMode"></a> OSDMigrateMode

 *Aplica-se para o [capturar estado do utilizador](task-sequence-steps.md#BKMK_CaptureUserState) passo.*

 (entrada)

 Permite-lhe personalizar os ficheiros que a ferramenta USMT captura. 

 #### <a name="valid-values"></a>Valores válidos
 - `Simple`: A sequência de tarefas utiliza apenas os ficheiros de configuração padrão da USMT  

 - `Advanced`: A variável de sequência de tarefas [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) Especifica os ficheiros de configuração que utiliza a USMT  


### <a name="OSDMigrateNetworkMembership"></a> OSDMigrateNetworkMembership

 *Aplica-se para o [capturar definições de rede](task-sequence-steps.md#BKMK_CaptureNetworkSettings) passo.*

 (entrada)

 Especifica se a sequência de tarefas migra as informações de associação do grupo de trabalho ou domínio.

 #### <a name="valid-values"></a>Valores válidos
 - `true` (predefinição)
 - `false`


### <a name="OSDMigrateRegistrationInfo"></a> OSDMigrateRegistrationInfo

 *Aplica-se para o [capturar definições do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings) passo.*

 (entrada)

 Especifica se o passo migra informações de utilizador e a organização.

 #### <a name="valid-values"></a>Valores válidos
 - `true` (predefinição). O [OSDRegisteredOrgName (saída)](#OSDRegisteredOrgName-output) variável é definida como o nome da organização registado do computador.  
 - `false`   


### <a name="OSDMigrateSkipEncryptedFiles"></a> OSDMigrateSkipEncryptedFiles

 *Aplica-se para o [capturar estado do utilizador](task-sequence-steps.md#BKMK_CaptureUserState) passo.*

 (entrada)

 Especifica se são capturados ficheiros encriptados.

 #### <a name="valid-values"></a>Valores válidos
 - `true`  
 - `false` (predefinição)  


### <a name="OSDMigrateTimeZone"></a> OSDMigrateTimeZone

 *Aplica-se para o [capturar definições do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings) passo.*

 (entrada)

 Especifica se o fuso horário do computador é migrado.

 #### <a name="valid-values"></a>Valores válidos
 - `true` (predefinição). A variável [OSDTimeZone (saída)](#OSDTimeZone-output) está definido para o fuso horário do computador.  
 - `false`   


### <a name="OSDNetworkJoinType"></a> OSDNetworkJoinType

 *Aplica-se para o [aplicar definições de rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings) passo.*

 (entrada)

 Especifica se o computador de destino é associado um domínio do Active Directory ou um grupo de trabalho.

 #### <a name="value-values"></a>Valores de valor
 - `0`: Junte-se a um domínio do Active Directory  
 - `1`: Aderir a um grupo de trabalho


### <a name="OSDPartitions"></a> OSDPartitions

 *Aplica-se para o [formatar e particionar disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk) passo.*

 (entrada)

 Esta variável de sequência de tarefas é uma variável de matriz de definições de partição. Cada um dos elementos da matriz representa as definições para uma partição individual no disco rígido. Acessar as definições especificadas para cada partição, ao combinar o nome da variável de matriz com o número de partição de disco baseado em zero e o nome da propriedade.

Utilize os seguintes nomes de variáveis para definir as propriedades para o *primeiro* partição que este passo cria no disco rígido:

 #### <a name="osdpartitions0type"></a>OSDPartitions0Type
 Especifica o tipo de partição. Esta propriedade é necessária. Os valores válidos são `Primary`, `Extended`, `Logical`, e `Hidden`.

 #### <a name="osdpartitions0filesystem"></a>OSDPartitions0FileSystem
 Especifica o tipo de sistema de ficheiros a utilizar ao formatar a partição. Esta propriedade é opcional. Se não especificar um sistema de ficheiros, o passo não formatar a partição. Os valores válidos são `FAT32` e `NTFS`.

 #### <a name="osdpartitions0bootable"></a>OSDPartitions0Bootable
 Especifica se a partição é de arranque. Esta propriedade é necessária. Se este valor é definido como `TRUE` para discos MBR, em seguida, a etapa marca esta partição como ativa.

 #### <a name="osdpartitions0quickformat"></a>OSDPartitions0QuickFormat
 Especifica o tipo de formato utilizado. Esta propriedade é necessária. Se este valor é definido como `TRUE`, o passo executa uma formatação rápida. Caso contrário, o passo efetua uma formação completa.

 #### <a name="osdpartitions0volumename"></a>OSDPartitions0VolumeName
 Especifica o nome atribuído ao volume quando é formatado. Esta propriedade é opcional.

 #### <a name="osdpartitions0size"></a>OSDPartitions0Size
 Especifica o tamanho da partição. Esta propriedade é opcional. Se esta propriedade não for especificada, a partição é criada utilizando todo o espaço livre restante. As unidades são especificadas pela variável **OSDPartitions0SizeUnits** .

 #### <a name="osdpartitions0sizeunits"></a>OSDPartitions0SizeUnits
 O passo utiliza estas unidades para interpretar os **OSDPartitions0Size** variável. Esta propriedade é opcional. Os valores válidos são `MB` (predefinição), `GB`, e `Percent`.

 #### <a name="osdpartitions0volumelettervariable"></a>OSDPartitions0VolumeLetterVariable
 Quando este passo cria partições, utiliza sempre a letra de unidade disponível seguinte no Windows PE. Utilize esta propriedade opcional para especificar o nome de outra variável de sequência de tarefas. O passo utiliza esta variável para guardar a nova letra de unidade para referência futura.

 Se definir várias partições com esta sequência de tarefas passo, as propriedades para o *segunda* partição definidas utilizando o **1** índice no nome da variável. Por exemplo: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**, e  **OSDPartitions1VolumeName**.


### <a name="OSDPartitionStyle"></a> OSDPartitionStyle

 *Aplica-se para o [formatar e particionar disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk) passo.*

 (entrada)

 Especifica o estilo de partição a utilizar ao particionar o disco. 

 #### <a name="valid-values"></a>Valores válidos
 - `GPT`: Utilizar o estilo de tabela de partições GUID
 - `MBR`: Utilizar o estilo de partição de registo de arranque principal


### <a name="OSDProductKey"></a> OSDProductKey

 *Aplica-se para o [aplicar definições do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) passo.*

 (entrada)

 Especifica a chave de produto do Windows. O valor especificado tem de ter entre 1 e 255 carateres.


### <a name="OSDRandomAdminPassword"></a> OSDRandomAdminPassword

 *Aplica-se para o [aplicar definições do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) passo.*

 (entrada)

 Especifica uma palavra-passe gerada aleatoriamente para a conta de administrador local em que o novo sistema operacional. 

 #### <a name="valid-values"></a>Valores válidos
 - `true` (predefinição): Configuração do Windows desativa a conta de administrador local no computador de destino  

 - `false`: Configuração do Windows permite que a conta de administrador local no computador de destino e define a palavra-passe de conta para o valor de [OSDLocalAdminPassword](#OSDLocalAdminPassword)  


### <a name="OSDRegisteredOrgName-input"></a> OSDRegisteredOrgName (entrada)

 *Aplica-se para o [aplicar definições do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) passo.*

 Especifica o nome da organização registado predefinido no novo sistema operacional. O valor especificado tem de ter entre 1 e 255 carateres.


### <a name="OSDRegisteredOrgName-output"></a> OSDRegisteredOrgName (saída)

 *Aplica-se para o [capturar definições do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings) passo.*

 Definida como o nome da organização registado do computador. O valor é definido apenas se o [OSDMigrateRegistrationInfo](#OSDMigrateRegistrationInfo) variável é definida como `true`.


### <a name="OSDRegisteredUserName"></a> OSDRegisteredUserName

 *Aplica-se para o [aplicar definições do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) passo.*

 (entrada)

 Especifica o nome de utilizador registado predefinido no novo sistema operacional. O valor especificado tem de ter entre 1 e 255 carateres.


### <a name="OSDServerLicenseConnectionLimit"></a> OSDServerLicenseConnectionLimit

 *Aplica-se para o [aplicar definições do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) passo.*

 (entrada)

 Especifica o número máximo de ligações permitido. O número especificado tem estar no intervalo de 5 a 9999 ligações.


### <a name="OSDServerLicenseMode"></a> OSDServerLicenseMode

 *Aplica-se para o [aplicar definições do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) passo.*

 (entrada)

 Especifica o modo de licenciamento do Windows Server que é utilizado.

 #### <a name="valid-values"></a>Valores válidos
 - `PerSeat`
 - `PerServer`


### <a name="OSDSetupAdditionalUpgradeOptions"></a> OSDSetupAdditionalUpgradeOptions

 *Aplica-se para o [atualizar sistema operativo](task-sequence-steps.md#BKMK_UpgradeOS) passo.*

 (entrada)

 Especifica as opções de linha de comandos adicionais que são adicionadas à configuração do Windows durante uma atualização do Windows 10. A sequência de tarefas não verifica as opções da linha de comandos. 

 Para obter mais informações, consulte [opções de linha de comandos de configuração do Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).


### <a name="OSDStateFallbackToNAA"></a> OSDStateFallbackToNAA

 *Aplica-se para o [Store de estado do pedido](task-sequence-steps.md#BKMK_RequestStateStore) passo.*

 (entrada)

 Quando a conta de computador falha a ligação ao ponto de migração de estado, esta variável Especifica se a sequência de tarefas retrocede para utilizar a conta de acesso de rede (NAA). 

 Para obter mais informações sobre a conta de acesso de rede, consulte [contas](/sccm/core/plan-design/hierarchy/accounts#network-access-account).

 #### <a name="valid-values"></a>Valores válidos
 - `true`  
 - `false` (predefinição)  


### <a name="OSDStateSMPRetryCount"></a> OSDStateSMPRetryCount

 *Aplica-se para o [Store de estado do pedido](task-sequence-steps.md#BKMK_RequestStateStore) passo.*

 (entrada)

 Especifica o número de vezes que o passo de sequência de tarefas tenta encontrar um ponto de migração de estado antes de o passo falhar. O número especificado tem de estar compreendido entre 0 e 600.


### <a name="OSDStateSMPRetryTime"></a> OSDStateSMPRetryTime

 *Aplica-se para o [Store de estado do pedido](task-sequence-steps.md#BKMK_RequestStateStore) passo.*

 (entrada)

 Especifica o número de segundos que o passo de sequência de tarefas aguarda entre as tentativas. O número de segundos pode ter um máximo de 30 carateres.


### <a name="OSDStateStorePath"></a> OSDStateStorePath

 *Aplica-se para os seguintes passos:*  
 - [Capturar estado do utilizador](task-sequence-steps.md#BKMK_CaptureUserState)  
 - [Store de estado da versão](task-sequence-steps.md#BKMK_ReleaseStateStore)  
 - [Store de estado do pedido](task-sequence-steps.md#BKMK_RequestStateStore)  
 - [Restaurar estado do utilizador](task-sequence-steps.md#BKMK_RestoreUserState)  


 (entrada)

 A partilha de rede ou o nome de caminho local da pasta em que a sequência de tarefas salva ou restaura o estado do utilizador. Não existe nenhum valor predefinido.


### <a name="OSDTargetSystemDrive"></a> OSDTargetSystemDrive

 *Aplica-se para o [aplicar imagem do SO](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) passo.*

 (saída)

 Especifica a letra de unidade da partição que contém os ficheiros de sistema operacional, depois da aplicação da imagem.


### <a name="OSDTargetSystemRoot-input"></a> OSDTargetSystemRoot (entrada)

 *Aplica-se para o [Capturar imagem do SO](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) passo.*

 Especifica o caminho para o diretório do Windows do sistema operacional instalado no computador de referência. A sequência de tarefas confirma-a como um SO suportado para captura pelo Configuration Manager.


### <a name="OSDTargetSystemRoot-output"></a> OSDTargetSystemRoot (saída)

 *Aplica-se para o [preparar Windows para captura](task-sequence-steps.md#BKMK_PrepareWindowsforCapture) passo.*

 Especifica o caminho para o diretório do Windows do sistema operacional instalado no computador de referência. A sequência de tarefas confirma-a como um SO suportado para captura pelo Configuration Manager.


### <a name="OSDTimeZone-input"></a> OSDTimeZone (entrada)

 *Aplica-se para o [aplicar definições do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings) passo.*

 Especifica a configuração de fuso horário padrão que é utilizada o novo sistema operacional.


### <a name="OSDTimeZone-output"></a> OSDTimeZone (saída)

 *Aplica-se para o [capturar definições do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings) passo.*

 Definida como o fuso horário do computador. O valor é definido apenas se o [OSDMigrateTimeZone](#OSDMigrateTimeZone) variável é definida como `true`.


### <a name="OSDWipeDestinationPartition"></a> OSDWipeDestinationPartition

 *Aplica-se para o [aplicar imagem de dados](task-sequence-steps.md#BKMK_ApplyDataImage) passo.*

 (entrada)

 Especifica se pretende eliminar os ficheiros localizados na partição de destino.

 #### <a name="valid-values"></a>Valores válidos
 - `true` (predefinição)
 - `false`


### <a name="OSDWorkgroupName"></a> OSDWorkgroupName

 *Aplica-se para o [aplicar definições de rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings) passo.*

 (entrada)

 Especifica o nome do grupo de trabalho ao qual o computador de destino é associado.

 Especifique a esta variável ou o [OSDDomainName](#OSDDomainName) variável. O nome do grupo de trabalho pode ter um máximo de 32 carateres. 


### <a name="SMSClientInstallProperties"></a> SMSClientInstallProperties

 *Aplica-se para o [configuração do Windows e ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) passo.*

 (entrada)

 Especifica as propriedades de instalação de cliente que a sequência de tarefas utiliza ao instalar o cliente do Configuration Manager.

 Para obter mais informações, consulte [sobre parâmetros de instalação de cliente e as propriedades](/sccm/core/clients/deploy/about-client-installation-properties).


### <a name="SMSConnectNetworkFolderAccount"></a> SMSConnectNetworkFolderAccount

 *Aplica-se para o [Connect To Network Folder](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) passo.*

 (entrada)

 Especifica a conta de utilizador que é utilizada para ligar à partilha de rede no [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath). Especifique a palavra-passe da conta com o [SMSConnectNetworkFolderPassword](#SMSConnectNetworkFolderPassword) valor.

 Para obter mais informações sobre a conta de ligação de pasta de rede de sequência de tarefas, consulte [contas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-network-folder-connection-account).


### <a name="SMSConnectNetworkFolderDriveLetter"></a> SMSConnectNetworkFolderDriveLetter

 *Aplica-se para o [Connect To Network Folder](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) passo.*

 (entrada)

 Especifica a letra de unidade de rede à qual ligar. Este valor é opcional. Se não for especificada, em seguida, a ligação de rede não está mapeada para uma letra de unidade. Se este valor for especificado, o valor tem de estar no intervalo de D para z. não utilize X, é a letra de unidade utilizada pelo Windows PE durante a fase Windows PE.

 #### <a name="examples"></a>Exemplos
 - `D:`  
 - `E:`  


### <a name="SMSConnectNetworkFolderPassword"></a> SMSConnectNetworkFolderPassword

 *Aplica-se para o [Connect To Network Folder](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) passo.*

 (entrada)

 Especifica a palavra-passe para o [SMSConnectNetworkFolderAccount](#SMSConnectNetworkFolderAccount) que é utilizado para ligar à partilha de rede na [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath). 


### <a name="SMSConnectNetworkFolderPath"></a> SMSConnectNetworkFolderPath

 *Aplica-se para o [Connect To Network Folder](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) passo.*

 (entrada)

 Especifica o caminho de rede para a ligação. Se precisar de mapear este caminho para uma letra de unidade, utilize o [SMSConnectNetworkFolderDriveLetter](#SMSConnectNetworkFolderDriveLetter) valor.

 #### <a name="example"></a>Exemplo
 `\\server\share`


### <a name="SMSInstallUpdateTarget"></a> SMSInstallUpdateTarget

 *Aplica-se para o [instalar atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) passo.*

 (entrada)

 Especifica se pretende instalar todas as atualizações ou apenas as atualizações obrigatórias.

 #### <a name="valid-values"></a>Valores válidos
 - `All`  
 - `Mandatory`  


### <a name="SMSRebootMessage"></a> SMSRebootMessage

 *Aplica-se para o [reiniciar o computador](task-sequence-steps.md#BKMK_RestartComputer) passo.*

 (entrada)

 Especifica a mensagem a apresentar aos utilizadores antes de reiniciar o computador de destino. Se esta variável não estiver configurada, o texto da mensagem predefinido é apresentado. A mensagem especificada não pode exceder os 512 carateres.

 #### <a name="example"></a>Exemplo
 `Save your work before the computer restarts.`  


### <a name="SMSRebootTimeout"></a> SMSRebootTimeout

 *Aplica-se para o [reiniciar o computador](task-sequence-steps.md#BKMK_RestartComputer) passo.*

 (entrada)

 Especifica o número de segundos durante o qual o aviso é apresentado ao utilizador antes de o computador ser reiniciado. 

 #### <a name="examples"></a>Exemplos
 - `0` (predefinição): Não exibir uma mensagem de reinício  
 - `60`: Apresentar o aviso durante um minuto  


### <a name="SMSTSAssignmentsDownloadInterval"></a> SMSTSAssignmentsDownloadInterval

 O número de segundos a aguardar antes do cliente tentar transferir a política desde a última tentativa que não devolveu qualquer política. Por predefinição, o cliente aguardará **0** segundos antes de tentar novamente. 

 Pode definir esta variável utilizando um comando de pré-início do suporte de dados ou do PXE.


### <a name="SMSTSAssignmentsDownloadRetry"></a> SMSTSAssignmentsDownloadRetry

 O número de vezes que um cliente tenta transferir a política após não existem políticas é encontrado na primeira tentativa. Por predefinição, o cliente tenta novamente **0** vezes.

 Pode definir esta variável utilizando um comando de pré-início do suporte de dados ou do PXE.


### <a name="SMSTSAssignUsersMode"></a> SMSTSAssignUsersMode

 Especifica como uma sequência de tarefas associa os utilizadores ao computador de destino. Defina a variável num dos seguintes valores:  

 - **Automática**: Quando a sequência de tarefas implementa o sistema operacional no computador de destino, ele cria uma relação entre os utilizadores especificados e o computador de destino.  

 - **Pendente**: A sequência de tarefas cria uma relação entre os utilizadores especificados e o computador de destino. Um administrador tem de aprovar a relação para defini-lo.  

 - **Desativado**: A sequência de tarefas não associa utilizadores ao computador de destino quando implementa o sistema operacional.


### <a name="SMSTSDisableStatusRetry"></a> SMSTSDisableStatusRetry
 <!--512358--> Em cenários desconectados, o motor de sequência de tarefas tenta repetidamente enviar mensagens de estado para o ponto de gestão. Este comportamento neste cenário faz com que os atrasos no processamento de sequência de tarefas. 

 A partir da versão 1802, definir esta variável como `true` e o motor de sequência de tarefas não tenta enviar mensagens de estado, após a primeira mensagem de falha de envio. Essa primeira tentativa inclui várias tentativas.

 Quando a sequência de tarefas é reiniciado, o valor da variável persiste. No entanto, a sequência de tarefas tenta enviar uma mensagem de estado inicial. Essa primeira tentativa inclui várias tentativas. Se tiver êxito, a sequência de tarefas continua a enviar estado independentemente do valor da variável. Se o estado de falha de envio, a sequência de tarefas utilizará o valor da variável.

 > [!NOTE]  
 > [Relatórios de estado de sequência de tarefas](/sccm/core/servers/manage/list-of-reports#task-sequence---deployment-status) conta com estas mensagens de estado para exibir o progresso, histórico e detalhes de cada passo.


### <a name="SMSTSDisableWow64Redirection"></a> SMSTSDisableWow64Redirection

 *Aplica-se para o [executar linha de comandos](task-sequence-steps.md#BKMK_RunCommandLine) passo.*

 (entrada)

 Por predefinição num sistema operacional de 64 bits, a sequência de tarefas localiza e executa o programa na linha de comandos com o redirecionador de sistema de ficheiros WOW64. Este comportamento permite que o comando para encontrar versões de 32 bits do SO programas e DLLs. A definição desta variável `true` desativa a utilização do redirecionador do sistema de ficheiros WOW64. O comando localiza as versões de 64 bits nativas de SO programas e DLLs do. Esta variável não tem efeito quando em execução num sistema operacional de 32 bits.


### <a name="SMSTSDownloadAbortCode"></a> SMSTSDownloadAbortCode

 Esta variável contiver o valor de código de anulação de para o dispositivo de transferência da programa externo. Este programa é especificado na [SMSTSDownloadProgram](#SMSTSDownloadProgram) variável. Se o programa devolver um código de erro igual ao valor da variável SMSTSDownloadAbortCode, em seguida, a transferência do conteúdo falha e nenhum outro método de transferência é tentado.


### <a name="SMSTSDownloadProgram"></a> SMSTSDownloadProgram

 Utilize esta variável para especificar um fornecedor de conteúdo alternativo (ACP). Um ACP é um programa de transferência que é utilizado para transferir o conteúdo. A sequência de tarefas utiliza a ACP em vez do dispositivo de transferência do Configuration Manager predefinido. Como parte do processo de transferência de conteúdo, a sequência de tarefas verifica essa variável. Se for especificado, a sequência de tarefas executa o programa para transferir o conteúdo.


### <a name="SMSTSDownloadRetryCount"></a> SMSTSDownloadRetryCount

 O número de vezes que o Configuration Manager tenta transferir conteúdo de um ponto de distribuição. Por predefinição, o cliente tenta novamente **2** vezes.


### <a name="SMSTSDownloadRetryDelay"></a> SMSTSDownloadRetryDelay

 O número de segundos que o Configuration Manager aguarda antes de voltar a tentar para transferir conteúdo de um ponto de distribuição. Por predefinição, o cliente aguardará **15** segundos antes de tentar novamente.


### <a name="SMSTSDriverRequestConnectTimeOut"></a> SMSTSDriverRequestConnectTimeOut

 *Aplica-se para o [aplicar controladores automaticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers) passo.*

 Quando solicitar o catálogo de controladores, esta variável é o número de segundos que a sequência de tarefas aguarda que a ligação ao servidor HTTP. Se a ligação demora mais tempo do que a definição de tempo limite, a sequência de tarefas cancela o pedido. Por predefinição, o tempo limite é definido como **60** segundos.


### <a name="SMSTSDriverRequestReceiveTimeOut"></a> SMSTSDriverRequestReceiveTimeOut

 *Aplica-se para o [aplicar controladores automaticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers) passo.*

 Quando solicitar o catálogo de controladores, esta variável é o número de segundos que a sequência de tarefas aguarda uma resposta. Se a ligação demora mais tempo do que a definição de tempo limite, a sequência de tarefas cancela o pedido. Por predefinição, o tempo limite é definido como **480** segundos.


### <a name="SMSTSDriverRequestResolveTimeOut"></a> SMSTSDriverRequestResolveTimeOut

 *Aplica-se para o [aplicar controladores automaticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers) passo.*

 Quando solicitar o catálogo de controladores, esta variável é o número de segundos que a sequência de tarefas aguarda para resolução de nomes HTTP. Se a ligação demora mais tempo do que a definição de tempo limite, a sequência de tarefas cancela o pedido. Por predefinição, o tempo limite é definido como **60** segundos.


### <a name="SMSTSDriverRequestSendTimeOut"></a> SMSTSDriverRequestSendTimeOut

 *Aplica-se para o [aplicar controladores automaticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers) passo.*

 Ao enviar um pedido para o catálogo de controladores, esta variável é o número de segundos que a sequência de tarefas aguarda para enviar o pedido. Se o pedido demora mais tempo do que a definição de tempo limite, a sequência de tarefas cancela o pedido. Por predefinição, o tempo limite é definido como **60** segundos.


### <a name="SMSTSErrorDialogTimeout"></a> SMSTSErrorDialogTimeout

 Quando ocorre um erro numa sequência de tarefas, ele exibe uma caixa de diálogo com o erro. A sequência de tarefas automaticamente descarte após o número de segundos especificado por esta variável. Por predefinição, este valor é **900** segundos (15 minutos).


### <a name="SMSTSLanguageFolder"></a> SMSTSLanguageFolder

 Utilize esta variável para alterar o idioma de apresentação de uma imagem de arranque de idioma neutro.


### <a name="SMSTSLocalDataDrive"></a> SMSTSLocalDataDrive

 Especifica onde a sequência de tarefas armazena ficheiros temporários no computador de destino durante a execução.

 Defina esta variável antes da iniciada de sequência de tarefas, como, definindo uma variável de coleção. Assim que a sequência de tarefas for iniciada, o Configuration Manager define a [smstsmdatapath](#SMSTSMDataPath) variável assim que a sequência de tarefas for iniciada.


### <a name="SMSTSMP"></a> SMSTSMP

 Utilize esta variável para especificar o URL ou endereço IP do ponto de gestão do Configuration Manager.


### <a name="SMSTSMPListRequestTimeoutEnabled"></a> SMSTSMPListRequestTimeoutEnabled

 *Aplica-se para os seguintes passos:*  
 - [Instalar aplicação](task-sequence-steps.md#BKMK_InstallApplication)  
 - [Instalar atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  


 (entrada) 

 Se o cliente não estiver na intranet, utilize esta variável para permitir pedidos de MPList repetidos atualizar o cliente. Por predefinição, esta variável é definida como `True`. 

 Quando os clientes estiverem na internet, definir esta variável como `False` para evitar atrasos desnecessários. 


### <a name="SMSTSMPListRequestTimeout"></a> SMSTSMPListRequestTimeout

 *Aplica-se para os seguintes passos:*  
 - [Instalar aplicação](task-sequence-steps.md#BKMK_InstallApplication)  
 - [Instalar atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  


 (entrada) 

 Se a sequência de tarefas não conseguir obter o ponto de gestão lista (MPList) dos serviços de localização, esta variável Especifica quantos milissegundos a aguardar antes de repetir o passo. Por predefinição, a sequência de tarefas aguarda `60000` milissegundos (60 segundos) antes de tentar novamente. Tentar novamente até três vezes.


### <a name="SMSTSPeerDownload"></a> SMSTSPeerDownload

 Utilize esta variável para permitir ao cliente utilizar a cache de ponto a ponto do Windows PE. A definição desta variável `true` permite esta funcionalidade.


### <a name="SMSTSPeerRequestPort"></a> SMSTSPeerRequestPort

 Uma porta de rede personalizada que utiliza a cache de ponto a ponto do Windows PE para a difusão inicial. É a porta predefinida configurada nas definições de cliente **8004**.


### <a name="SMSTSPersistContent"></a> SMSTSPersistContent

 Utilize esta variável para manter temporariamente o conteúdo na cache da sequência de tarefas. Esta variável é diferente da [SMSTSPreserveContent](#SMSTSPreserveContent), que mantém os conteúdos na cache do cliente do Configuration Manager após a conclusão da sequência de tarefas. SMSTSPersistContent utiliza a cache de sequência de tarefas, SMSTSPreserveContent utiliza a cache do cliente do Configuration Manager. 


### <a name="SMSTSPostAction"></a> SMSTSPostAction

 Especifica um comando que é executado após a conclusão da sequência de tarefas. Por exemplo, especifica um script que ativa filtros de escrita em dispositivos incorporados após a sequência de tarefas implementa um sistema operacional para o dispositivo.


### <a name="SMSTSPreferredAdvertID"></a> SMSTSPreferredAdvertID

 Força a sequência de tarefas para executar uma implementação direcionada específica no computador de destino. Defina esta variável através de um comando de Pré-início do suporte de dados ou PXE. Se esta variável for definida, a sequência de tarefas substitui quaisquer implementações necessárias.


### <a name="SMSTSPreserveContent"></a> SMSTSPreserveContent

 Esta variável sinaliza o conteúdo na sequência de tarefas ser mantidos na cache do cliente do Configuration Manager após a implementação. Esta variável é diferente da [SMSTSPersistContent](#SMSTSPersistContent), que mantém apenas o conteúdo para a duração da sequência de tarefas. SMSTSPersistContent utiliza a cache de sequência de tarefas, SMSTSPreserveContent utiliza a cache do cliente do Configuration Manager. Definir SMSTSPreserveContent `true` para ativar esta funcionalidade.


### <a name="SMSTSRebootDelay"></a> SMSTSRebootDelay

 Especifica quantos segundos deve aguardar até que o computador seja reiniciado. Se esta variável é zero (0), o Gestor da sequência de tarefas não exibe uma caixa de diálogo de notificação antes do reinício.

 #### <a name="example"></a>Exemplo
 - `0`: não apresentar uma notificação  

 - `60`: apresentar uma notificação para um minuto  


### <a name="SMSTSRebootMessage"></a> SMSTSRebootMessage

 Especifica a mensagem a apresentar na caixa de diálogo de notificação de reinício. Se esta variável não estiver configurada, é apresentada uma mensagem predefinida.

 #### <a name="example"></a>Exemplo
 `The task sequence is restarting this computer`


### <a name="SMSTSRebootRequested"></a> SMSTSRebootRequested

 Indica que é pedido um reinício após a conclusão do passo de sequência de tarefas atual. Se for necessário um reinício, definir esta variável como `true`, e o Gestor da sequência de tarefas reinicia o computador após este passo de sequência de tarefas. Se o passo de sequência de tarefas é necessário reiniciar para concluir a ação, defina esta variável. Depois do computador é reiniciado, a sequência de tarefas continua executar a partir do passo de sequência de tarefas seguinte.


### <a name="SMSTSRetryRequested"></a> SMSTSRetryRequested

 Pede uma repetição após a conclusão do passo de sequência de tarefas atual. Se esta variável de sequência de tarefas estiver definida, defina também a [SMSTSRebootRequested](#SMSTSRebootRequested) variável à `true`. Depois do computador é reiniciado, o Gestor da sequência de tarefas volta a executar o mesmo passo de sequência de tarefas.


### <a name="SMSTSRunCommandLineUserName"></a> SMSTSRunCommandLineUserName

 *Aplica-se para o [executar linha de comandos](task-sequence-steps.md#BKMK_RunCommandLine) passo.*

 (entrada)

 Especifica a conta através da qual a linha de comandos é executada. O valor é uma cadeia de formato nomedeutilizador ou domínio\nomedeutilizador. Especifique a palavra-passe da conta com o [SMSTSRunCommandLinePassword](#SMSTSRunCommandLinePassword) variável.

 Para obter mais informações sobre a conta sequência de tarefas executar como, consulte [contas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account).


### <a name="SMSTSRunCommandLinePassword"></a> SMSTSRunCommandLinePassword

 *Aplica-se para o [executar linha de comandos](task-sequence-steps.md#BKMK_RunCommandLine) passo.*

 (entrada)

 Especifica a palavra-passe para a conta especificada pelos [SMSTSRunCommandLineUserName](#SMSTSRunCommandLineUserName) variável.


### <a name="SMSTSSoftwareUpdateScanTimeout"></a> SMSTSSoftwareUpdateScanTimeout

 *Aplica-se para o [instalar atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) passo.*

 (entrada)

 Controle o tempo limite para a análise de atualizações de software durante este passo. Por exemplo, se esperar inúmeras atualizações durante a análise, aumenta o valor. O valor predefinido é `1800` segundos (30 minutos). O valor da variável é definido em segundos.


### <a name="SMSTSUDAUsers"></a> SMSTSUDAUsers

 Especifica os utilizadores primários do computador de destino utilizando o seguinte formato: `<DomainName>\<UserName>`. Separe múltiplos utilizadores com uma vírgula (`,`). Para obter mais informações, consulte [associar utilizadores a um computador de destino](/sccm/osd/get-started/associate-users-with-a-destination-computer).

 #### <a name="example"></a>Exemplo
 `contoso\jqpublic, contoso\megb, contoso\janedoh`


### <a name="SMSTSWaitForSecondReboot"></a> SMSTSWaitForSecondReboot

 *Aplica-se para o [instalar atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) passo.*

 (entrada)

 Esta variável de sequência de tarefas opcionais controla o comportamento do cliente, quando uma instalação de atualização de software exige dois reinícios. Defina esta variável antes deste passo para impedir que uma sequência de tarefas falhe devido uma segunda reinicialização da instalação da atualização de software.

 Defina o valor de SMSTSWaitForSecondReboot em segundos para especificar o tempo que a sequência de tarefas coloca em pausa neste passo enquanto o computador for reiniciado. Permita tempo suficiente no caso de uma segunda reinicialização. 

Por exemplo, se definir SMSTSWaitForSecondReboot para `600`, a sequência de tarefas coloca em pausa durante 10 minutos após um reinício antes de executam passos adicionais. Esta variável é útil quando centenas de atualizações de software é instalado de um único passo de sequência de tarefas instalar atualizações de Software.


### <a name="TSDisableProgressUI"></a> TSDisableProgressUI
 <!-- 1354291 --> Utilize esta variável para controlar quando a sequência de tarefas mostra o progresso para os utilizadores finais. Para ocultar ou exibir o progresso em momentos diferentes, defina esta variável várias vezes numa sequência de tarefas.  

 - `true`: Ocultar o progresso da sequência de tarefas  

 - `false`: Exibir o progresso da sequência de tarefas  


### <a name="TSErrorOnWarning"></a> Tserroronwarning como 

 *Aplica-se para o [instalar aplicação](task-sequence-steps.md#BKMK_InstallApplication) passo.*

 (entrada) 

 Especifique se o motor de sequência de tarefas considera um aviso detetado como um erro durante este passo. Os conjuntos de sequência de tarefas da [tsappinstallstatus](#TSAppInstallStatus) variável à `Warning` quando uma ou mais aplicações, ou uma dependência necessária não foi instalada porque não cumpre um requisito. Quando definir esta variável `True`e a tarefa de sequência de conjuntos **tsappinstallstatus** para `Warning`, o resultado é um erro. Um valor de `False` é o comportamento padrão.


### <a name="WorkingDirectory"></a> WorkingDirectory

 *Aplica-se para o [executar linha de comandos](task-sequence-steps.md#BKMK_RunCommandLine) passo.*

 (entrada)

 Especifica o diretório inicial para uma ação da linha de comandos. O nome do diretório especificado não pode exceder os 255 carateres.

 #### <a name="examples"></a>Exemplos
 - `C:\`  
 - `%SystemRoot%`  



## <a name="deprecated-variables"></a>Variáveis preteridas

As seguintes variáveis são preteridas:

- **OSDAllowUnsignedDriver**: Não é utilizada na implementação do Windows Vista e sistemas operativos posteriores
- **OSDBuildStorageDriverList**: Aplica-se apenas ao Windows XP e Windows Server 2003
- **OSDDiskpartBiosCompatibilityMode**: Apenas necessário ao implementar o Windows XP ou Windows Server 2003
- **OSDInstallEditionIndex**: Não é preciso após o Windows Vista
- **OSDPreserveDriveLetter**: Para obter mais informações, consulte [OSDPreserveDriveLetter](#OSDPreserveDriveLetter)

### <a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter

 > [!Important]
 > Esta variável de sequência de tarefas foi preterido. 
 >
 > Durante uma implementação do sistema operacional, por predefinição, a configuração do Windows determina a melhor letra de unidade a utilizar (normalmente c). 

 *Comportamento anterior*: ao aplicar uma imagem, a variável OSDPreverveDriveLetter determina se a sequência de tarefas utiliza a letra de unidade capturada no ficheiro de imagem (WIM). Defina o valor desta variável para `false` para utilizar a localização que especificou para o **destino** definição **aplicar sistema operativo** passo de sequência de tarefas. Para obter mais informações, consulte [imagem do SO aplicar](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).



## <a name="see-also"></a>Consulte também

- [Passos de sequência de tarefas](/sccm/osd/understand/task-sequence-steps)
- [Usando variáveis de sequência de tarefas](/sccm/osd/understand/using-task-sequence-variables)
- [Considerações sobre planeamento para automatizar tarefas](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)

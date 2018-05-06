---
title: Variáveis de ação de sequência de tarefas
titleSuffix: Configuration Manager
description: Utilize variáveis de ação de sequência, tais como as variáveis de definição de rede, para especificar definições de configuração para um único passo numa sequência de tarefas do Configuration Manager.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e2269031-0977-4f01-a274-420e00630575
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f66203e335524fa922ec1b6ab3dd4dc5fb917b0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>Variáveis de ação de sequência de tarefas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Variáveis de ação de sequência de tarefas especificam definições de configuração que são utilizadas por um passo individual numa sequência de tarefas do System Center Configuration Manager. Por predefinição, o passo de sequência de tarefas inicializa as respetivas definições antes de executar. Estas definições estão disponíveis apenas enquanto executa o passo de sequência de tarefas associadas. Por outras palavras, a sequência de tarefas adiciona o valor da variável de ação para o ambiente de sequência de tarefas antes do passo de sequência de tarefas é executado. A sequência de tarefas remove o valor do ambiente de depois da execução do passo.  

## <a name="action-variable-example"></a>Exemplo de Variável de Ação  
 Por exemplo, pode especificar um diretório de início para uma ação da linha de comandos utilizando o passo de sequência de tarefas **Executar Linha de Comandos** . Este passo inclui uma propriedade **Iniciar em** cujo valor predefinido é armazenado no ambiente de sequência de tarefas como a variável **WorkingDirectory** . A variável de ambiente **WorkingDirectory** é inicializada antes de a ação de sequência de tarefas **Executar Linha de Comandos** ser executada. Durante o passo **Executar Linha de Comandos** , o valor **WorkingDirectory** pode ser acedido através da propriedade **Iniciar em** . Depois de concluir o passo, a sequência de tarefas remove o valor da **WorkingDirectory** variável do ambiente. Se a sequência contiver outro **executar linha de comandos** passo de sequência de tarefas, a sequência de tarefas inicializa uma nova **WorkingDirectory** variável e define-o para o iniciar valor para o passo atual.  

 O *predefinido* valor para uma variável de ação de sequência de tarefas está presente quando o passo de sequência de tarefas é executada. Se definir um *novo* valor, fica disponível para vários passos numa sequência de tarefas. Se utilizar um dos métodos de criação de variáveis de sequência de tarefas para substituir um valor de variável incorporado, o novo valor permanece no ambiente e substitui o valor predefinido para outros passos da sequência de tarefas. Por exemplo, se adicionar um **definir variável da sequência de tarefas** passo como o primeiro passo da sequência de tarefas, que define o **WorkingDirectory** variável à **c:\\**, qualquer **executar linha de comandos** passo da sequência de tarefas utiliza o novo valor inicial do diretório.  

## <a name="action-variables-for-task-sequence-actions"></a>Variáveis de Ação para Ações de Sequência de Tarefas  
 Variáveis de sequência de tarefas do Configuration Manager estão agrupadas pela respetiva ação de sequência de tarefas associadas. Utilize as hiperligações seguintes para recolher informações sobre as variáveis de ação associadas a uma ação específica. As variáveis de sequência das tarefas definem o funcionamento da ação de sequência de tarefas. A ação de sequência de tarefas lê e utiliza as variáveis assinaladas pelo utilizador como variáveis de entrada. Em alternativa, pode utilizar o [Set Task Sequence Variable](task-sequence-steps.md#BKMK_SetTaskSequenceVariable) passo ou o objeto TSEnvironment COM para definir as variáveis no tempo de execução. Apenas a ação de sequência de tarefas assinala variáveis como variáveis de saída. As ações que ocorrem mais tarde na sequência de tarefas ler estas variáveis de saída.  

> [!NOTE]  
>  Nem todas as ações de sequência de tarefas estão associadas a um conjunto de variáveis de sequência de tarefas. Por exemplo, apesar de existirem variáveis associadas à ação Ativar BitLocker, não existe nenhuma variável associada à ação Desativar BitLocker.  



###  <a name="BKMK_ApplyDataImage"></a> Aplicar imagem de dados   
 Para obter mais informações, consulte [aplicar imagem de dados](task-sequence-steps.md#BKMK_ApplyDataImage). 

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (entrada)|Especifica o valor de índice da imagem que está aplicada ao computador de destino.|  
|OSDWipeDestinationPartition<br /><br /> (entrada)|Especifica se pretende eliminar os ficheiros localizados na partição de destino.<br /><br /> Valores válidos:<br /><br /> **Verdadeiro** (predefinição)<br /><br /> **false**|  



###  <a name="BKMK_ApplyDriverPackage"></a> Aplicar pacote de controlador   
Para obter mais informações, consulte [aplicar pacote de controlador](task-sequence-steps.md#BKMK_ApplyDriverPackage).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (entrada)|Especifica o ID de conteúdo do controlador de dispositivo de armazenamento em massa a instalar a partir do pacote de controlador. Se esta variável não for especificada, será instalado nenhum controlador de armazenamento em massa.|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (entrada)|Especifica o ficheiro INF do controlador de armazenamento em massa a instalar.<br /><br /> <br /><br /> Esta variável de sequência de tarefas é necessária se o OSDApplyDriverBootCriticalContentUniqueID for definido.|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (entrada)|Especifica se um controlador de dispositivo de armazenamento em massa está instalado, esta variável tem de ser **scsi**.<br /><br /> Esta variável de sequência de tarefas é necessária se o OSDApplyDriverBootCriticalContentUniqueID for definido.|  
|OSDApplyDriverBootCriticalID<br /><br /> (entrada)|Especifica o ID crítico de arranque do controlador de dispositivo de armazenamento em massa a instalar. Este ID está listado no **scsi** secção do ficheiro txtsetup.oem do controlador de dispositivo.<br /><br /> Esta variável de sequência de tarefas é necessária se o OSDApplyDriverBootCriticalContentUniqueID for definido.|  
|OSDAllowUnsignedDriver<br /><br /> (entrada)|Especifica se pretende configurar o Windows para permitir a instalação de controladores de dispositivo não assinados. Esta variável de sequência de tarefas não é utilizada quando implementar o Windows Vista e o sistema operativo posterior.<br /><br /> Valores válidos:<br /><br /> **VERDADEIRO**<br /><br /> **FALSO** (predefinição)|  



###  <a name="BKMK_ApplyNetworkSettings"></a> Aplicar definições de rede   
 Para obter mais informações, consulte [aplicar definições de rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (entrada)|Esta variável de sequência de tarefas é uma variável de matriz. Cada elemento da matriz representa as definições para um adaptador de rede individual no computador. Definições para cada adaptador de acesso através da combinação do nome de variável de matriz com o índice de adaptador de rede baseado em zero e o nome de propriedade.<br /><br />Se este passo configura vários adaptadores de rede, define as propriedades para a segunda placa de rede utilizando o índice no nome da variável. Por exemplo, OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList, OSDAdapter1DNSDomain, OSDAdapter1WINSServerList e OSDAdapter1EnableWINS.<br /><br />Por exemplo, utilize os seguintes nomes de variáveis para definir as propriedades da placa de rede primeiro para este passo de sequência de tarefas para configurar:<br /><br /> <ul><li>**OSDAdapter0EnableDHCP**: **verdadeiro** permite que o protocolo de configuração dinâmica de anfitrião (DHCP) para o adaptador.<br />    Esta definição é obrigatória. Os valores possíveis são: **Verdadeiro** ou **falso**.</li><li>**OSDAdapter0IPAddressList**: Lista delimitada por vírgulas de endereços IP para o adaptador. Esta propriedade é ignorada, a menos que **EnableDHCP** esteja definido como **falso**.<br />    Esta definição é obrigatória.</li><li>**OSDAdapter0SubnetMask**: Lista delimitada por vírgulas de máscaras de sub-rede. Esta propriedade é ignorada, a menos que **EnableDHCP** esteja definido como **falso**.<br />    Esta definição é obrigatória.</li><li>**OSDAdapter0Gateways**: Lista delimitada por vírgulas de endereços de gateway IP. Esta propriedade é ignorada, a menos que **EnableDHCP** esteja definido como **falso**.<br />    Esta definição é obrigatória.</li><li>**OSDAdapter0DNSDomain**: Domínio de Name System (DNS) de domínio para o adaptador.</li><li>**OSDAdapter0DNSServerList**: Lista delimitada por vírgulas dos servidores DNS para o adaptador.<br />    Esta definição é obrigatória.</li><li>**OSDAdapter0EnableDNSRegistration**: **verdadeiro** para registar o endereço IP para o adaptador no DNS.</li><li>**OSDAdapter0EnableFullDNSRegistration**: **verdadeiro** para registar o endereço IP para o adaptador no DNS sob o nome DNS completo para o computador.</li><li>**OSDAdapter0EnableIPProtocolFiltering**: **verdadeiro** para ativar o protocolo de endereço IP no adaptador de filtragem.</li><li>**OSDAdapter0IPProtocolFilterList**: Lista delimitada por vírgulas de protocolos podem ser executados através de IP. Esta propriedade é ignorada se **EnableIPProtocolFiltering** estiver definido como **falso**.</li><li>**OSDAdapter0EnableTCPFiltering**: **verdadeiro** para ativar a filtragem para o adaptador de porta TCP.</li><li>**OSDAdapter0TCPFilterPortList**: Lista delimitada por vírgulas de portas para ser concedido permissões de acesso para TCP. Esta propriedade é ignorada se **EnableTCPFiltering** estiver definido como **falso**.</li><li>**OSDAdapter0TcpipNetbiosOptions**: Opções para NetBIOS por TCP/IP. Os valores possíveis são:<br /><br /> <ul><li>**0**: Utilize definições NetBIOS do servidor DHCP.</li><li>**1**: Ative o NetBIOS através de TCP/IP.</li><li>**2**: Desative NetBIOS por TCP/IP.</li></ul></li><li>**OSDAdapter0EnableWINS**: **verdadeiro** utilizar WINS para resolução de nomes.</li><li>**OSDAdapter0WINSServerList**: Lista delimitada por vírgulas de endereços IP do servidor WINS. Esta propriedade é ignorada, a menos que **EnableWINS** esteja definido como **verdadeiro**.</li><li>**OSDAdapter0MacAddress**: Endereço MAC utilizado para corresponde às definições do adaptador de rede física.</li><li>**OSDAdapter0Name**: Nome da ligação de rede conforme é apresentado no programa de painel de controlo de ligações de rede. O nome tem entre 0 e 255 carateres.</li><li>**OSDAdapter0Index**: Índice de definições de adaptador de rede na matriz de definições.<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (entrada)|Especifica o número de adaptadores de rede instalados no computador de destino. Quando o valor **OSDAdapterCount** estiver definido, têm de ser definidas todas as opções de configuração para cada adaptador. Por exemplo, se definir o valor **OSDAdapterTCPIPNetbiosOptions** para um adaptador específico, todos os valores para esse adaptador têm também de ser configurados.<br /><br />Se este valor não for especificado, todos os valores **OSDAdapter** serão ignorados.|  
|OSDDNSDomain<br /><br /> (entrada)|Especifica o servidor DNS primário utilizado pelo computador de destino.|  
|OSDDomainName<br /><br /> (entrada)|Especifica o nome do domínio Windows ao qual o computador de destino é associado. O valor especificado tem de ser um nome de domínio de Serviços de Domínio do Active Directory válido.|  
|OSDDomainOUName<br /><br /> (entrada)|Especifica o nome do formato RFC 1779 da unidade organizacional (UO) ao qual o computador de destino é associado. Se for especificado, o valor tem de conter o caminho completo.<br /><br /> Exemplo:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (entrada)|Especifica se a filtragem TCP/IP está ativada.<br /><br /> Valores válidos:<br /><br /> **VERDADEIRO**<br /><br /> **FALSO** (predefinição)|  
|OSDJoinAccount<br /><br /> (entrada)|Especifica a conta de rede que é utilizada para adicionar o computador de destino a um domínio Windows.|  
|OSDJoinPassword<br /><br /> (entrada)|Especifica a palavra-passe de rede que é utilizada para adicionar o computador de destino a um domínio Windows.|  
|OSDNetworkJoinType<br /><br /> (entrada)|Especifica se o computador de destino é associado a um domínio Windows ou a um grupo de trabalho.<br /><br /> **0** indica que o computador de destino é associado um domínio Windows. **1** Especifica que o computador é associado um grupo de trabalho.<br /><br /> Valores válidos:<br /><br /> **0**<br /><br /> **1**|  
|OSDDNSSuffixSearchOrder<br /><br /> (entrada)|Especifica a ordem de procura DNS para o computador de destino.|  
|OSDWorkgroupName<br /><br /> (entrada)|Especifica o nome do grupo de trabalho ao qual o computador de destino é associado.<br /><br /> Especificar este valor ou o **OSDDomainName** valor. O nome do grupo de trabalho pode ter um máximo de 32 carateres.<br /><br /> Exemplo:<br /><br /> **Gestão de contas**|  



###  <a name="BKMK_ApplyOperatingSystem"></a> Aplicar imagem do sistema operativo   
 Para obter mais informações, veja [Aplicar Imagem do Sistema Operativo](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (entrada)|Especifica o nome de ficheiro do ficheiro de resposta de implementação do sistema operativo associado ao pacote de implementação do sistema operativo.|  
|OSDImageIndex<br /><br /> (entrada)|Especifica o valor de índice da imagem do ficheiro WIM aplicado ao computador de destino.|  
|OSDInstallEditionIndex<br /><br /> (entrada)|Especifica a versão do sistema operativo Windows Vista ou posterior que está instalado. Não se for especificada nenhuma versão, o programa de configuração do Windows determina a versão a instalar utilizando a chave de produto referenciada.<br /><br /> Utilize apenas um valor de zero (0) se as condições seguintes forem verdadeiras:<br /><br /> -Estiver a instalar um sistema de operativo anterior ao Windows Vista<br />-Estiver a instalar uma edição de licença de volume do Windows Vista ou posterior, e é especificada qualquer chave de produto.<br /><br /> Valores válidos:<br /><br /> **0** (predefinição)|  
|OSDTargetSystemDrive (saída)|Especifica a letra de unidade da partição que contém os ficheiros do sistema operativo.|  



###  <a name="BKMK_ApplyWindowsSettings"></a> Aplicar definições do Windows   
 Para obter mais informações, consulte [aplicar definições do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (entrada)|Especifica o nome do computador de destino.<br /><br /> Exemplo:<br /><br /> **% Smstsmachinename %** (predefinição)|  
|OSDProductKey<br /><br /> (entrada)|Especifica a chave de produto do Windows. O valor especificado tem de ter entre 1 e 255 carateres.|  
|OSDRegisteredUserName<br /><br /> (entrada)|Especifica o nome de utilizador registado predefinido no novo sistema operativo. O valor especificado tem de ter entre 1 e 255 carateres.|  
|OSDRegisteredOrgName<br /><br /> (entrada)|Especifica o nome da organização registado predefinido no novo sistema operativo. O valor especificado tem de ter entre 1 e 255 carateres.|  
|OSDTimeZone<br /><br /> (entrada)|Especifica a predefinição de fuso horário utilizada no novo sistema operativo.|  
|OSDServerLicenseMode<br /><br /> (entrada)|Especifica o modo de licenciamento do Windows Server utilizado.<br /><br /> Valores válidos:<br /><br /> **PerSeat**<br /><br /> **PerServer**|  
|OSDServerLicenseConnectionLimit<br /><br /> (entrada)|Especifica o número máximo de ligações permitido. O número especificado tem estar no intervalo de 5 a 9999 ligações.|  
|OSDRandomAdminPassword<br /><br /> (entrada)|Especifica uma palavra-passe gerada aleatoriamente para a conta de administrador no novo sistema operativo. Se definido como **verdadeiro**, configuração do Windows desativa a conta de administrador local no computador de destino. Se definido como **falso**, configuração do Windows permite que a conta de administrador local no computador de destino e define a palavra-passe de conta para o valor de **OSDLocalAdminPassword**.<br /><br /> Valores válidos:<br /><br /> **Verdadeiro** (predefinição)<br /><br /> **false**|  
|OSDLocalAdminPassword<br /><br /> (entrada)|Especifica a palavra-passe de administrador local. Se ativar **aleatoriamente gerar a palavra-passe de administrador local e desativar a conta nas plataformas suportadas**, em seguida, o passo ignora esta variável. O valor especificado tem de ter entre 1 e 255 carateres.|  



###  <a name="BKMK_AutoApplyDrivers"></a> Aplicar controladores automaticamente   
 Para obter mais informações, consulte [aplicar controladores automaticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (entrada)|Uma lista delimitada por vírgulas dos IDs exclusivos das categorias do catálogo de controladores. O **aplicar controladores automaticamente** passo considera apenas os controladores de, pelo menos, uma das categorias especificadas. Este valor é opcional e não está especificado por predefinição. Obter os IDs das categorias disponíveis ao enumerar a lista de **SMS_CategoryInstance** objetos no site.|  
|OSDAllowUnsignedDriver<br /><br /> (entrada)|Especifica se o Windows está configurado para permitir a instalação de controladores de dispositivo não assinados. Esta variável de sequência de tarefas não é utilizada na implementação do Windows Vista e sistemas operativos posteriores.<br /><br /> Valores válidos:<br /><br /> **VERDADEIRO**<br /><br /> **FALSO** (predefinição)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (entrada)|Se existirem vários controladores de dispositivo no catálogo de controladores que são compatíveis com um dispositivo de hardware, esta variável determina a ação do passo. Se definido como **verdadeiro**, o passo instala apenas o melhor controlador de dispositivo. Se **falso**, o passo instala todos os controladores de dispositivos compatíveis e Windows escolhe o controlador mais adequado para utilizar.<br /><br /> Valores válidos:<br /><br /> **Verdadeiro** (predefinição)<br /><br /> **false**|  
|SMSTSDriverRequestConnectTimeOut|Quando solicitar o catálogo de controladores, esta variável é o número de segundos que a sequência de tarefas aguarda que a ligação do servidor HTTP. Se a ligação demora mais que a definição de tempo limite, a sequência de tarefas cancela o pedido. Por predefinição, o tempo limite está definido como **60** segundos.|  
|SMSTSDriverRequestReceiveTimeOut|Quando solicitar o catálogo de controladores, esta variável é o número de segundos que a sequência de tarefas aguarda uma resposta. Se a ligação demora mais que a definição de tempo limite, a sequência de tarefas cancela o pedido. Por predefinição, o tempo limite está definido como **480** segundos.|
|SMSTSDriverRequestResolveTimeOut|Quando solicitar o catálogo de controladores, esta variável é o número de segundos que a sequência de tarefas aguarda para resolução de nomes HTTP. Se a ligação demora mais que a definição de tempo limite, a sequência de tarefas cancela o pedido. Por predefinição, o tempo limite está definido como **60** segundos.|
|SMSTSDriverRequestSendTimeOut|Ao enviar um pedido para o catálogo de controladores, esta variável é o número de segundos que a sequência de tarefas aguarda para enviar o pedido. Se o pedido demora mais que a definição de tempo limite, a sequência de tarefas cancela o pedido. Por predefinição, o tempo limite está definido como **60** segundos.|



###  <a name="BKMK_CaptureNetworkSettings"></a> Capturar definições de rede   
 Para obter mais informações, consulte [capturar definições de rede](task-sequence-steps.md#BKMK_CaptureNetworkSettings).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (entrada)|Especifica se as informações de configuração das definições do adaptador de rede (TCP/IP, DNS e WINS) são capturadas.<br /><br /> Exemplos:<br /><br /> **Verdadeiro** (predefinição)<br /><br /> **false**|  
|OSDMigrateNetworkMembership<br /><br /> (entrada)|Especifica se as informações de associação a grupos de trabalho ou a domínios são migradas como parte da implementação do sistema operativo.<br /><br /> Exemplos:<br /><br /> **Verdadeiro** (predefinição)<br /><br /> **false**|  



###  <a name="BKMK_CaptureOperatingSystemImage"></a> Capturar imagem do sistema operativo   
 Para obter mais informações, consulte [Capturar imagem do sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDCaptureAccount<br /><br /> (entrada)|Especifica o nome de uma conta do Windows que tem permissões para armazenar a imagem capturada numa partilha de rede.|  
|OSDCaptureAccountPassword<br /><br /> (entrada)|Especifica a palavra-passe para a conta do Windows utilizada para armazenar a imagem capturada numa partilha de rede.|  
|OSDCaptureDestination<br /><br /> (entrada)|Especifica a localização na qual a imagem do sistema operativo capturada é guardada. O comprimento máximo do nome do diretório é 255 carateres.|  
|OSDImageCreator<br /><br /> (entrada)|Um nome opcional do utilizador que criou a imagem. Este nome é armazenado no ficheiro WIM. O comprimento máximo do nome de utilizador é 255 carateres.|  
|OSDImageDescription<br /><br /> (entrada)|Uma descrição opcional definida pelo utilizador da imagem do sistema operativo capturada. Esta descrição é armazenada no ficheiro WIM. O comprimento máximo da descrição é 255 carateres.|  
|OSDImageVersion<br /><br /> (entrada)|Número da versão opcional definido pelo utilizador para atribuir à imagem do sistema operativo capturada. Este número de versão é armazenado no ficheiro WIM. Este valor pode ser qualquer combinação de letras com um comprimento máximo de 32 carateres.|  
|OSDTargetSystemRoot<br /><br /> (entrada)|Especifica o caminho para o diretório do Windows do sistema operativo instalado no computador de referência. Este sistema operativo é validado como sistema operativo suportado para captura pelo Configuration Manager.|  



###  <a name="BKMK_CaptureUserState"></a> Capturar estado do utilizador   
 Para obter mais informações, consulte [capturar estado do utilizador](task-sequence-steps.md#BKMK_CaptureUserState).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|O UNC ou o nome de caminho local da pasta onde o estado de utilizador é guardado. Não tem predefinição.|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (entrada)|Adicionais opções user state migration tool (USMT) da linha de comandos que utiliza a sequência de tarefas para capturar o estado do utilizador. O passo não expõe estas definições no editor de sequência de tarefas. Especificar estas opções como uma cadeia de carateres, a sequência de tarefas acrescenta a linha de comandos da USMT gerada automaticamente.<br /><br />As opções da USMT especificadas com esta variável da sequência de tarefas não são validadas em termos de exatidão antes da execução da sequência de tarefas.|  
|OSDMigrateMode<br /><br /> (entrada)|Permite-lhe personalizar os ficheiros que são capturados pela USMT. Se esta variável é definida como **simples**, em seguida, a sequência de tarefas utiliza apenas os ficheiros de configuração padrão da USMT. Se esta variável é definida como **avançadas**, em seguida, a variável de sequência de tarefas OSDMigrateConfigFiles Especifica os ficheiros de configuração que utiliza a USMT.<br /><br /> Valores válidos:<br /><br /> **Simples**<br /><br /> **Avançadas**|  
|OSDMigrateConfigFiles<br /><br /> (entrada)|Especifica os ficheiros de configuração utilizados para controlar a captura de perfis de utilizador. Esta variável só é utilizada se OSDMigrateMode estiver definido como avançadas. Este valor da lista delimitada por vírgulas está definido para efetuar a migração personalizada de perfis de utilizador.<br /><br /> Exemplo: miguser.xml,migsys.xml,migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (entrada)|Se o USMT não é possível capturar alguns ficheiros, esta variável permite a captura de estado do utilizador continuar.<br /><br /> Valores válidos:<br /><br /> **Verdadeiro** (predefinição)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrada)|Ativa o registo verboso para a USMT.<br /><br /> Valores válidos:<br /><br /> **VERDADEIRO**<br /><br /> **FALSO** (predefinição)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (entrada)|Especifica se são capturados ficheiros encriptados.<br /><br /> Valores válidos:<br /><br /> **VERDADEIRO**<br /><br /> **FALSO** (predefinição)|  
|_OSDMigrateUsmtPackageID<br /><br /> (entrada)|Especifica o ID de pacote do pacote do Configuration Manager que contém os ficheiros da USMT. Esta variável é necessária.|  



###  <a name="BKMK_CaptureWindowsSettings"></a> Capturar definições do Windows   
 Para obter mais informações, consulte [capturar definições do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (entrada)|Especifica se o nome do computador é migrado.<br /><br /> Valores válidos:<br /><br /> **Verdadeiro** (predefinição)<br /><br /> **false**<br /><br /> Se o valor for **verdadeiro**, a variável OSDComputerName é definida com o nome NetBIOS do computador.|  
|OSDComputerName<br /><br /> (saída)|Definida como o nome NetBIOS do computador. O valor é definido apenas se a variável OSDMigrateComputerName for definida **verdadeiro**.|  
|OSDMigrateRegistrationInfo<br /><br /> (entrada)|Especifica se o passo migra informações de utilizador e a organização.<br /><br /> Valores válidos:<br /><br /> **Verdadeiro** (predefinição)<br /><br /> **false**<br /><br /> Se o valor for **verdadeiro**, a variável OSDRegisteredOrgName é definido com o nome da organização registado do computador.|  
|OSDRegisteredOrgName<br /><br /> (saída)|Definida como o nome da organização registado do computador. O valor é definido apenas se a variável OSDMigrateRegistrationInfo for definida **verdadeiro**.|  
|OSDMigrateTimeZone<br /><br /> (entrada)|Especifica se o fuso horário do computador é migrado.<br /><br /> Valores válidos:<br /><br /> **Verdadeiro** (predefinição)<br /><br /> **false**<br /><br /> Se o valor for **verdadeiro**, a variável OSDTimeZone é definida para o fuso horário do computador.|  
|OSDTimeZone<br /><br /> (saída)|Definida como o fuso horário do computador. O valor é definido apenas se a variável OSDMigrateTimeZone for definida **verdadeiro**.|  



###  <a name="BKMK_ConnecttoNetworkFolder"></a> Ligar à pasta de rede   
 Para obter mais informações, consulte [ligar à pasta de rede](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (entrada)|Especifica a conta de administrador que é utilizada para ligar à partilha de rede.|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (entrada)|Especifica a letra de unidade de rede à qual ligar. Este valor é opcional; se não for especificado, a ligação de rede não é mapeada para uma letra de unidade. Se este valor for especificado, o valor tem de estar compreendido no intervalo de D: a Z:. Além disso, não utilize X:, uma vez que é a letra de unidade utilizada pelo Windows PE durante a fase Windows PE.<br /><br /> Exemplos:<br /><br /> **D:**<br /><br /> **E:**|  
|SMSConnectNetworkFolderPassword<br /><br /> (entrada)|Especifica a palavra-passe de rede que é utilizada para ligar à partilha de rede.|  
|SMSConnectNetworkFolderPath<br /><br /> (entrada)|Especifica o caminho de rede para a ligação.<br /><br /> Exemplo:<br /><br /> **\\\servername\sharename**|  



###  <a name="BKMK_EnableBitLocker"></a> Ativar o BitLocker   
 Para obter mais informações, consulte [ativar BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (entrada)|Em vez de gerar uma palavra-passe de recuperação aleatória, a ação da sequência de tarefas **Ativar BitLocker** utiliza o valor especificado como a palavra-passe de recuperação. O valor tem de ser uma palavra-passe de recuperação do BitLocker numérica válida.|  
|OSDBitLockerStartupKey<br /><br /> (entrada)|Em vez de gerar uma chave de arranque aleatória para a opção de gestão de chaves **chave de arranque em USB apenas,** o **ativar BitLocker** passo utiliza o Trusted Platform Module (TPM) como a chave de arranque. O valor tem de ser uma chave de arranque do BitLocker codificada em Base64 de 256 bits válida.|  



###  <a name="BKMK_FormatPartitionDisk"></a> Formatar e particionar disco   
 Para obter mais informações, consulte [formatar e particionar disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (entrada)|Especifica o número do disco físico a particionar.|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (entrada)|Ao particionar o disco rígido para compatibilidade com certos tipos de BIOS, esta variável Especifica se pretende desativar otimizações de alinhamento de cache. Isto é necessário ao implementar sistemas operativos Windows XP ou Windows Server 2003. Para mais informações, consulte o [artigo 931760](http://go.microsoft.com/fwlink/?LinkId=134081) e o [artigo 931761](http://go.microsoft.com/fwlink/?LinkId=134082) da Base de Dados de Conhecimento Microsoft.<br /><br /> Valores válidos:<br /><br /> **VERDADEIRO**<br /><br /> **FALSO** (predefinição)| 
|OSDGPTBootDisk<br /><br /> (entrada)|Especifica se pretende criar uma partição EFI num disco rígido GPT. Computadores baseados em EFI utilizam esta partição como disco de arranque.<br /><br /> Valores válidos:<br /><br /> **VERDADEIRO**<br /><br /> **FALSO** (predefinição)|  
|OSDPartitions<br /><br /> (entrada)|Especifica uma matriz de definições de partição; consulte o tópico do SDK para aceder a variáveis de matriz no ambiente de sequência de tarefas.<br /><br /> Esta variável de sequência de tarefas é uma variável de matriz. Cada um dos elementos da matriz representa as definições para uma partição individual no disco rígido. Aceder às definições especificadas para cada partição através da combinação do nome de variável de matriz com o número de partição de disco baseado em zero e o nome de propriedade.<br /><br /> Por exemplo, utilize os seguintes nomes de variáveis para definir as propriedades para a primeira partição, este passo cria no disco rígido:<br /><br /> - **OSDPartitions0Type**: Especifica o tipo de partição. Esta propriedade é necessária. Os valores válidos são **primário**, **expandida**, **Logical**, e **Hidden**.<br />-   **OSDPartitions0FileSystem**: Especifica o tipo de sistema de ficheiros a utilizar ao formatar a partição. Esta propriedade é opcional. Se não especificar um sistema de ficheiros, o passo não formatar a partição. Os valores válidos são **FAT32** e **NTFS**.<br />-   **OSDPartitions0Bootable**: Especifica se a partição é de arranque. Esta propriedade é necessária. Se este valor é definido como **verdadeiro** para discos MBR, em seguida, o passo marca esta partição como o Active Directory.<br />-   **OSDPartitions0QuickFormat**: Especifica o tipo de formato utilizado. Esta propriedade é necessária. Se este valor é definido como **verdadeiro**, o passo efetua uma formatação rápida. Caso contrário, o passo efetua um formato completo.<br />-   **OSDPartitions0VolumeName**: Especifica o nome que é atribuído ao volume quando é formatado. Esta propriedade é opcional.<br />-   **OSDPartitions0Size**: Especifica o tamanho da partição. As unidades são especificadas pela variável **OSDPartitions0SizeUnits** . Esta propriedade é opcional. Se esta propriedade não for especificada, a partição é criada utilizando todo o espaço livre restante.<br />-   **OSDPartitions0SizeUnits**: O passo utiliza estas unidades para interpretar o **OSDPartitions0Size** variável. Esta propriedade é opcional. Os valores válidos são **MB** (predefinição), **GB**, e **por cento**.<br />-   **OSDPartitions0VolumeLetterVariable**: Quando este passo cria partições, utiliza sempre a letra de unidade disponível seguinte no Windows PE. Utilize esta propriedade opcional para especificar o nome de outra variável da sequência de tarefas. O passo utiliza esta variável para guardar a nova letra de unidade para referência futura.<br /><br />Se definir várias partições com esta ação de sequência de tarefas, as propriedades para a segunda partição são definidas utilizando o respetivo índice no nome da variável. Por exemplo: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**, e  **OSDPartitions1VolumeName**.|  
|OSDPartitionStyle<br /><br /> (entrada)|Especifica o estilo de partição a utilizar ao particionar o disco. **MBR** indica o estilo de partição de registo de arranque principal e **GPT** indica o estilo de tabela de partições GUID.<br /><br /> Valores válidos:<br /><br /> **GPT**<br /><br /> **MBR**|  



###  <a name="BKMK_InstallApplication"></a> Instalar a aplicação   
 Para obter mais informações, consulte [instalar aplicação](task-sequence-steps.md#BKMK_InstallApplication).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
| TSErrorOnWarning |Especifique se o motor de sequência de tarefas considera um aviso detetado como um erro durante este passo. A sequência de tarefas define a variável tsappinstallstatus como **aviso** quando uma ou mais aplicações ou uma dependência necessária, não foi instalada porque não cumpriu um requisito. Quando definir esta variável como **verdadeiro**e a sequência de tarefas define tsappinstallstatus como aviso, o resultado é um erro. Um valor de **Falso** corresponde ao comportamento predefinido.| 
|SMSTSMPListRequestTimeoutEnabled|Utilize esta variável para permitir pedidos de MPList repetidos atualizar o cliente se o cliente não estiver na intranet. <br />Por predefinição, esta variável é definida como **verdadeiro**. Quando os clientes estão na internet, pode definir esta variável **falso** para evitar atrasos desnecessários. Esta variável é apenas aplicável aos passos de sequência de tarefas Instalar Aplicação e Instalar Atualizações de Software.|  
|SMSTSMPListRequestTimeout|Especifique a lista de pontos de quantos milissegundos uma sequência de tarefas aguarda antes de tentar para instalar uma aplicação após a falha ao obter a gestão dos serviços de localização. Por predefinição, a sequência de tarefas aguarda **60000** milissegundos (60 segundos) antes de repetir o passo e repete até três vezes.|  



###  <a name="BKMK_InstallSoftwareUpdates"></a> Instalar atualizações de Software   
Para obter mais informações, consulte [instalar atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (entrada)|Especifica se pretende instalar todas as atualizações ou apenas as atualizações obrigatórias.<br /><br /> Valores válidos:<br /><br /> **Todos os**<br /><br /> **Obrigatório**|  
|SMSTSSoftwareUpdateScanTimeout| Controla o tempo limite para a análise de atualizações de software durante este passo. Por exemplo, aumente o valor se prevê que as várias atualizações durante a análise. O valor predefinido é **1800** segundos (30 minutos). O valor da variável é definido em segundos. |
|SMSTSWaitForSecondReboot|Esta variável de sequência de tarefas opcionais controla o comportamento do cliente, quando uma instalação de atualização de software necessita de dois reinicializações. Defina esta variável antes deste passo para impedir que uma sequência de tarefas falhar devido a uma segunda reinicialização da instalação da atualização de software.<br /><br /> Defina o valor de SMSTSWaitForSecondReboot em segundos para especificar quanto a sequência de tarefas pausa sobre este passo enquanto o computador for reiniciado. Permita tempo suficiente no caso de existir uma segunda reinicialização. <br />Por exemplo, se definir SMSTSWaitForSecondReboot para 600, a sequência de tarefas interrompe durante 10 minutos após um reinício antes de executar passos adicionais. Esta variável é útil quando centenas de atualizações de software é instalado de um único passo de sequência de tarefas instalar atualizações de Software.| 
|SMSTSMPListRequestTimeoutEnabled|Utilize esta variável para permitir pedidos de MPList repetidos atualizar o cliente se o cliente não estiver na intranet. <br />Por predefinição, esta variável é definida como **verdadeiro**. Quando os clientes estão na internet, pode definir esta variável **falso** para evitar atrasos desnecessários. Esta variável é apenas aplicável aos passos de sequência de tarefas Instalar Aplicação e Instalar Atualizações de Software.|  
|SMSTSMPListRequestTimeout|Especifique a lista de pontos de quantos milissegundos uma sequência de tarefas aguarda antes de tentar para instalar uma atualização de software após a falha ao obter a gestão dos serviços de localização. Por predefinição, a sequência de tarefas aguarda **60000** milissegundos (60 segundos) antes de repetir o passo e repete até três vezes.|  



###  <a name="BKMK_JoinDomainWorkgroup"></a> Associar domínio ou grupo de trabalho   
 Para obter mais informações, consulte [associar domínio ou grupo de trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (entrada)|Especifica a conta que é utilizada pelo computador de destino para associar o domínio do Active Directory. Esta variável é necessária ao associar um domínio.|  
|OSDJoinDomainName<br /><br /> (entrada)|Especifica o nome de um domínio do Active Directory no computador de destino é associado. O comprimento do nome de domínio tem de ser entre 1 e 255 carateres.|  
|OSDJoinDomainOUName<br /><br /> (entrada)|Especifica o nome do formato RFC 1779 da unidade organizacional (UO) ao qual o computador de destino é associado. Se for especificado, o valor tem de conter o caminho completo. O comprimento do nome de UO tem de ser entre 0 e 32.767 carateres. Este valor não é definido se o **OSDJoinType** variável é definida como **1** (associar grupo de trabalho).<br /><br /> Exemplo:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDJoinPassword<br /><br /> (entrada)|Especifica a palavra-passe de rede que utiliza o computador de destino para associar o domínio do Active Directory. Se o ambiente de sequência de tarefas não inclui esta variável, o programa de configuração do Windows tenta uma palavra-passe em branco. Se a variável **OSDJoinType** variável é definida como **0** (associar domínio), este valor é necessário.|  
|OSDJoinSkipReboot<br /><br /> (entrada)|Especifica se pretende ignorar o reinício após o computador de destino ser associado ao domínio ou grupo de trabalho.<br /><br /> Valores válidos:<br /><br /> **VERDADEIRO**<br /><br /> **false**|  
|OSDJoinType<br /><br /> (entrada)|Especifica se o computador de destino é associado a um domínio Windows ou a um grupo de trabalho. Para associar o computador de destino a um domínio do Windows, especifique **0**. Para associar o computador de destino a um grupo de trabalho, especifique **1**.<br /><br /> Valores válidos:<br /><br /> **0**<br /><br /> **1**|  
|OSDJoinWorkgroupName<br /><br /> (entrada)|Especifica o nome de um grupo de trabalho ao qual o computador de destino é associado. O comprimento do nome do grupo de trabalho tem de ser entre 1 e 32 carateres.<br /><br /> Exemplo:<br /><br /> **Gestão de contas**|  



###  <a name="BKMK_PrepareWindowsCapture"></a> Preparar Windows para captura   
 Para obter mais informações, consulte [preparar Windows para captura](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (entrada)|Especifica se o Sysprep cria uma lista de controladores de dispositivo de armazenamento em massa. Esta definição aplica-se apenas ao Windows XP e ao Windows Server 2003. Esta variável preenche a secção [SysprepMassStorage] de sysprep.inf com informações sobre todos os controladores de armazenamento em massa que são suportadas pela imagem para serem capturadas.<br /><br /> Valores válidos:<br /><br /> **VERDADEIRO**<br /><br /> **FALSO** (predefinição)|  
|OSDKeepActivation<br /><br /> (entrada)|Especifica se o sysprep repõe o sinalizador de ativação do produto.<br /><br /> Valores válidos:<br /><br /> **VERDADEIRO**<br /><br /> **FALSO** (predefinição)|  
|OSDTargetSystemRoot<br /><br /> (saída)|Especifica o caminho para o diretório do Windows do sistema operativo instalado no computador de referência. Este sistema operativo é validado como sistema operativo suportado para captura pelo Configuration Manager.|  



###  <a name="BKMK_ReleaseStateStore"></a> Disponibilizar armazenamento de Estados   
 Para obter mais informações, consulte [disponibilizar armazenamento de Estados](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|O UNC ou nome do caminho local para a localização a partir da qual o estado do utilizador é restaurado. Este valor é utilizado pela ação da sequência de tarefas **Capturar Estado do Utilizador** e pela ação da sequência de tarefas **Restaurar Estado do Utilizador** .|  



###  <a name="BKMK_RequestState"></a> Solicitar armazenamento de Estados   
  Para obter mais informações, consulte [disponibilizar armazenamento de Estados](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (entrada)|Quando a conta de computador falha a ligação ao ponto de migração de estado, esta variável Especifica se a sequência de tarefas retrocede para utilizar a conta de acesso de rede (NAA).<br /><br /> Valores válidos:<br /><br /> **VERDADEIRO**<br /><br /> **FALSO** (predefinição)|  
|OSDStateSMPRetryCount<br /><br /> (entrada)|Especifica o número de vezes que o passo de sequência de tarefas tenta encontrar um ponto de migração de estado antes de o passo falhar. O número especificado tem de estar compreendido entre 0 e 600.|  
|OSDStateSMPRetryTime<br /><br /> (entrada)|Especifica o número de segundos que o passo de sequência de tarefas aguarda entre as tentativas. O número de segundos pode ter um máximo de 30 carateres.|  
|OSDStateStorePath<br /><br /> (saída)|O caminho UNC para a pasta no ponto de migração de estado onde o estado do utilizador está armazenado.|  



###  <a name="BKMK_RestartComputer"></a> Reiniciar computador   
 Para obter mais informações, consulte [reiniciar o computador](task-sequence-steps.md#BKMK_RestartComputer).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (entrada)|Especifica a mensagem a apresentar aos utilizadores antes de reiniciar o computador de destino. Se esta variável não for definida, será apresentado o texto da mensagem predefinida. A mensagem especificada não pode exceder os 512 carateres.<br /><br /> Exemplo:<br /><br /> **Guarde o trabalho antes do reinício do computador.**|  
|SMSRebootTimeout<br /><br /> (entrada)|Especifica o número de segundos durante o qual o aviso é apresentado ao utilizador antes de o computador ser reiniciado. Especifique zero segundos para indicar que não é apresentada qualquer mensagem de reinício.<br /><br /> Exemplos:<br /><br /> **0** (predefinição)<br /><br />  **60**|  



###  <a name="BKMK_RestoreUserState"></a> Restaurar estado do utilizador   
  Para obter mais informações, consulte [restaurar estado do utilizador](task-sequence-steps.md#BKMK_RestoreUserState).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|O UNC ou nome do caminho local da pasta a partir da qual o estado do utilizador é restaurado.|  
|OSDMigrateContinueOnRestore<br /><br /> (entrada)|Continue o processo, mesmo que o USMT não é possível restaurar alguns ficheiros.<br /><br /> Valores válidos:<br /><br /> **Verdadeiro** (predefinição)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrada)|Ativa o registo verboso para a ferramenta USMT. Este valor é necessário para a ação.<br /><br /> Valores válidos:<br /><br /> **VERDADEIRO**<br /><br /> **FALSO** (predefinição)|  
|OSDMigrateLocalAccounts<br /><br /> (entrada)|Especifica se a conta de computador local é restaurada.<br /><br /> Valores válidos:<br /><br /> **VERDADEIRO**<br /><br /> **FALSO** (predefinição)|  
|OSDMigrateLocalAccountPassword<br /><br /> (entrada)|Se o **OSDMigrateLocalAccounts** variável é "verdadeiro", esta variável deve conter a palavra-passe atribuída a todas as contas locais migradas. USMT atribui a mesma palavra-passe para todas as contas locais migradas. Considere esta palavra-passe como temporário e alterá-la mais tarde por algum outro método.|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (entrada)|Especifica adicionais opções user state migration tool (USMT) da linha de comandos que são utilizadas ao restaurar o estado do utilizador. As opções adicionais são especificadas sob a forma de cadeia que é acrescentada à linha de comando USMT gerada automaticamente. As opções da USMT especificadas com esta variável da sequência de tarefas não são validadas em termos de exatidão antes da execução da sequência de tarefas.|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (entrada)|Especifica o ID de pacote do pacote do Configuration Manager que contém os ficheiros da USMT. Esta variável é necessária.|  



###  <a name="BKMK_RunCommand"></a> Executar linha de comandos   
  Para obter mais informações, consulte [executar linha de comandos](task-sequence-steps.md#BKMK_RunCommandLine).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (entrada)|Por predefinição num sistema operativo de 64 bits, a sequência de tarefas localiza e executa o programa na linha de comandos com o redirecionador de sistema de ficheiros WOW64. Este comportamento permite que o comando para encontrar versões de 32 bits do sistema operativo programas e DLLs. A definição desta variável **verdadeiro** desativa a utilização do redirecionador do sistema de ficheiros WOW64. O comando localiza as versões de 64 bits nativas do sistema operativo programas e DLLs. Esta variável não produz qualquer efeito numa execução num sistema operativo de 32 bits.|  
|WorkingDirectory<br /><br /> (entrada)|Especifica o diretório inicial para uma ação da linha de comandos. O nome do diretório especificado não pode exceder os 255 caracteres.<br /><br /> Exemplos:<br /><br /> -   **C:\\**<br />-   **%SystemRoot%**|  
|SMSTSRunCommandLineUserName<br /><br /> (entrada)|Especifica a conta através da qual a linha de comandos é executada. O valor é uma cadeia de formato nomedeutilizador ou domínio\nomedeutilizador.|  
|SMSTSRunCommandLinePassword<br /><br /> (entrada)|Especifica a palavra-passe para a conta especificada pela variável SMSTSRunCommandLineUserName.|  



### <a name="set-dynamic-variables"></a>Definir Variáveis Dinâmicas  
Para obter mais informações, consulte [definir variáveis dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
|_SMSTSMake|Especifica a marca do computador.|  
|_SMSTSModel|Especifica o modelo do computador.|  
|_SMSTSMacAddresses|Especifica os endereços MAC utilizados pelo computador.|  
|_SMSTSIPAddresses|Especifica os endereços IP utilizados pelo computador.|  
|_SMSTSSerialNumber|Especifica o número de série do computador.|  
|_SMSTSAssetTag|Especifica a etiqueta de ativo para o computador.|  
|_SMSTSUUID|Especifica o UUID do computador.|  
|_SMSTSDefaultGateways|Especifica os gateways predefinidos utilizados pelo computador.|  



###  <a name="BKMK_SetupWindows"></a> Configurar Windows e ConfigMgr   
  Para obter mais informações, consulte [configurar Windows e ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (entrada)|Especifica as propriedades de instalação de cliente que são utilizadas ao instalar o cliente do Configuration Manager.|  



### <a name="upgrade-operating-system"></a>Atualizar Sistema Operativo  
 Para obter mais informações, consulte [atualizar sistema operativo](task-sequence-steps.md#BKMK_UpgradeOS).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (entrada)|Especifica as opções da linha de comandos adicionais que são adicionadas à configuração do Windows durante uma atualização do Windows 10. A sequência de tarefas não verifica as opções da linha de comandos.<br /><br /> Para obter mais informações, consulte [opções de linha de comandos de configuração do Windows](/windows-hardware/manufacture/desktop/windows-setup-command-line-options).|  

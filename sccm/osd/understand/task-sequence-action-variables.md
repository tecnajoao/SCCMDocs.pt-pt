---
title: "Variáveis de ação de sequência de tarefas"
titleSuffix: Configuration Manager
description: "Utilize variáveis de ação de sequência, tais como as variáveis de definição de rede, para especificar definições de configuração para um único passo numa sequência de tarefas do Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2269031-0977-4f01-a274-420e00630575
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 8c1462ca922f23250ffa44c6433f01a8220d3ad7
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>Variáveis de ação de sequência de tarefas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Variáveis de ação de sequência de tarefas especificam definições de configuração que são utilizadas por um passo individual numa sequência de tarefas do System Center Configuration Manager. Por predefinição, as definições utilizadas por um passo de sequência de tarefas são inicializadas antes de o passo ser executado e estão disponíveis apenas enquanto o passo de sequência de tarefas associado é executado. Por outras palavras, a definição da variável de sequência de tarefas é adicionada ao ambiente de sequência de tarefas antes de o passo de sequência de tarefas ser executado e o valor é removido do ambiente de sequência de tarefas após o passo de sequência de tarefas ter sido executado.  

## <a name="action-variable-example"></a>Exemplo de Variável de Ação  
 Por exemplo, pode especificar um diretório de início para uma ação da linha de comandos utilizando o passo de sequência de tarefas **Executar Linha de Comandos** . Este passo inclui uma propriedade **Iniciar em** cujo valor predefinido é armazenado no ambiente de sequência de tarefas como a variável **WorkingDirectory** . A variável de ambiente **WorkingDirectory** é inicializada antes de a ação de sequência de tarefas **Executar Linha de Comandos** ser executada. Durante o passo **Executar Linha de Comandos** , o valor **WorkingDirectory** pode ser acedido através da propriedade **Iniciar em** . Em seguida, depois de concluído o passo de sequência de tarefas, o valor da variável **WorkingDirectory** é removido do ambiente de sequência de tarefas. Se a sequência contiver outro passo de sequência de tarefas **Executar Linha de Comandos** , a nova variável **WorkingDirectory** é inicializada e definida como o valor inicial para esse passo de sequência de tarefas.  

 Ao passo que o valor predefinido para uma definição de ação de sequência de tarefas está presente enquanto o passo de sequência de tarefas é executado, qualquer novo valor que definiu pode ser utilizado por vários passos da sequência. Se utilizar um dos métodos de criação de variáveis de sequência de tarefas para substituir um valor de variável incorporado, o novo valor permanece no ambiente e substitui o valor predefinido para outros passos da sequência de tarefas. No exemplo anterior, se um **definir variável da sequência de tarefas** passo é adicionado como o primeiro passo de sequência de tarefas e define o **WorkingDirectory** variável de ambiente para o valor **c:\\**, ambos os **executar linha de comandos** passos da sequência de tarefas irão utilizar o novo valor inicial do diretório.  

## <a name="action-variables-for-task-sequence-actions"></a>Variáveis de Ação para Ações de Sequência de Tarefas  
 Variáveis de sequência de tarefas do Configuration Manager estão agrupadas pela respetiva ação de sequência de tarefas associadas. Utilize as hiperligações seguintes para recolher informações sobre as variáveis de ação associadas a uma ação específica. As variáveis de sequência das tarefas definem o funcionamento da ação de sequência de tarefas. A ação de sequência de tarefas lê e utiliza as variáveis assinaladas pelo utilizador como variáveis de entrada. Em alternativa, as variáveis podem ser configuradas no runtime através da ação Set Task Sequence Variable ou do objeto TSEnvironment COM. Apenas a ação de sequência de tarefas assinala variáveis como variáveis de saída que são lidas pelas ações que tenham lugar mais tarde na sequência de tarefas.  

> [!NOTE]  
>  Nem todas as ações de sequência de tarefas estão associadas a um conjunto de variáveis de sequência de tarefas. Por exemplo, apesar de existirem variáveis associadas à ação Ativar BitLocker, não existe nenhuma variável associada à ação Desativar BitLocker.  

###  <a name="BKMK_ApplyDataImage"></a> Variáveis de Ação da Sequência de Tarefas Aplicar Imagem de Dados  
 As variáveis para esta ação especificam a imagem de um ficheiro WIM que é aplicada ao computador de destino e se pretende eliminar os ficheiros na partição de destino. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [aplicar dados de imagem do passo de sequência](task-sequence-steps.md#BKMK_ApplyDataImage).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (entrada)|Especifica o valor de índice da imagem que está aplicada ao computador de destino.|  
|OSDWipeDestinationPartition<br /><br /> (entrada)|Especifica se pretende eliminar os ficheiros localizados na partição de destino.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"** (predefinição)<br /><br /> **"falso"**|  

###  <a name="BKMK_ApplyDriverPackage"></a> Variáveis de Ação da Sequência de Tarefas Aplicar Pacote de Controlador  
 As variáveis para esta ação especificam informações de instalação de controladores de armazenamento em massa e se pretende instalar controladores não assinados. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [aplicar pacote de controlador](task-sequence-steps.md#BKMK_ApplyDriverPackage).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (entrada)|Especifica o ID de conteúdo do controlador de dispositivo de armazenamento em massa a instalar a partir do pacote de controlador. Se não for especificado, não é instalado nenhum controlador de armazenamento em massa.|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (entrada)|Especifica o ficheiro INF do controlador de armazenamento em massa a instalar.<br /><br /> <br /><br /> Esta variável de sequência de tarefas é necessária se o OSDApplyDriverBootCriticalContentUniqueID for definido.|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (entrada)|Especifica se um controlador de dispositivo de armazenamento em massa está instalado, tem de ser **scsi**.<br /><br /> <br /><br /> Esta variável de sequência de tarefas é necessária se o OSDApplyDriverBootCriticalContentUniqueID for definido.|  
|OSDApplyDriverBootCriticalID<br /><br /> (entrada)|Especifica o ID crítico de arranque do controlador de dispositivo de armazenamento em massa a instalar. Este ID está listado no "**scsi**" secção do ficheiro txtsetup.oem do controlador de dispositivo.<br /><br /> <br /><br /> Esta variável de sequência de tarefas é necessária se o OSDApplyDriverBootCriticalContentUniqueID for definido.|  
|OSDAllowUnsignedDriver<br /><br /> (entrada)|Especifica se pretende configurar o Windows para permitir a instalação de controladores de dispositivo não assinados. Esta variável de sequência de tarefas não é utilizada quando implementar o Windows Vista e o sistema operativo posterior.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"**<br /><br /> **"falso"** (predefinição)|  

###  <a name="BKMK_ApplyNetworkSettings"></a> Variáveis de Ação da Sequência de Tarefas Aplicar Definições de Rede  
 As variáveis para esta ação especificam definições de rede para o computador de destino, tais como definições para os adaptadores de rede do computador, definições de domínio e definições do grupo de trabalho. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [passo de definições de rede aplicam-se](task-sequence-steps.md#BKMK_ApplyNetworkSettings).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (entrada)|Esta variável de sequência de tarefas é uma variável de matriz. Cada elemento da matriz representa as definições para um adaptador de rede individual no computador. As definições especificadas para cada adaptador são acedidas através da combinação do nome da variável de matriz com o índice de adaptador de rede baseado em zero e o nome da propriedade.<br /><br /> <br /><br /> Se vários adaptadores de rede forem configurados com esta ação de sequência de tarefas, as propriedades do segundo adaptador de rede são definidas utilizando o respetivo índice no nome da variável; por exemplo, OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList, OSDAdapter1DNSDomain, OSDAdapter1WINSServerList, OSDAdapter1EnableWINS, etc.<br /><br /> <br /><br /> Por exemplo, os nomes de variáveis seguintes podem ser utilizados para definir as propriedades para o primeiro adaptador de rede que será configurado por esta ação de sequência de tarefas:<br /><br /> <ul><li>**OSDAdapter0EnableDHCP** - TRUE para ativar o protocolo de configuração dinâmica de anfitrião (DHCP) para o adaptador.<br />    Esta definição é obrigatória. Os valores possíveis são:  VERDADEIRO ou FALSO.</li><li>**OSDAdapter0IPAddressList** -endereços lista delimitada por vírgulas de IP para o adaptador. Esta propriedade é ignorada, a menos que **EnableDHCP** esteja definido como **falso**.<br />    Esta definição é obrigatória.</li><li>**OSDAdapter0SubnetMask** -lista delimitada por vírgulas de máscaras de sub-rede. Esta propriedade é ignorada, a menos que **EnableDHCP** esteja definido como **falso**.<br />    Esta definição é obrigatória.</li><li>**OSDAdapter0Gateways** -lista delimitada por vírgulas de endereços de gateway IP. Esta propriedade é ignorada, a menos que **EnableDHCP** esteja definido como **falso**.<br />    Esta definição é obrigatória.</li><li>**OSDAdapter0DNSDomain** - domínio de Sistema de Nomes de Domínio (DNS) para o adaptador.</li><li>**OSDAdapter0DNSServerList** -lista delimitada por vírgulas de servidores DNS para o adaptador.<br />    Esta definição é obrigatória.</li><li>**OSDAdapter0EnableDNSRegistration** - **verdadeiro** para registar o endereço IP para o adaptador no DNS.</li><li>**OSDAdapter0EnableFullDNSRegistration** - **verdadeiro** para registar o endereço IP para o adaptador no DNS sob o nome DNS completo para o computador.</li><li>**OSDAdapter0EnableIPProtocolFiltering** - **verdadeiro** para ativar o protocolo de endereço IP no adaptador de filtragem.</li><li>**OSDAdapter0IPProtocolFilterList** -lista delimitada por vírgulas de protocolos de permissão para ser executada através de IP. Esta propriedade é ignorada se **EnableIPProtocolFiltering** estiver definido como **falso**.</li><li>**OSDAdapter0EnableTCPFiltering** - **verdadeiro** para ativar a filtragem para o adaptador de porta TCP.</li><li>**OSDAdapter0TCPFilterPortList** -lista delimitada por vírgulas de portas para ser concedido permissões de acesso para TCP. Esta propriedade é ignorada se **EnableTCPFiltering** estiver definido como **falso**.</li><li>**OSDAdapter0TcpipNetbiosOptions** -opções para NetBIOS por TCP/IP. Os valores possíveis são:<br /><br /> <ul><li>0 Utilizar definições NetBIOS do servidor DHCP.</li><li>1 Ativar NetBIOS por TCP/IP.</li><li>2 Desativar NetBIOS por TCP/IP.</li></ul></li><li>**OSDAdapter0EnableWINS** - **verdadeiro** utilizar WINS para resolução de nomes.</li><li>**OSDAdapter0WINSServerList** -lista delimitada por vírgulas de endereços IP do servidor WINS. Esta propriedade é ignorada, a menos que **EnableWINS** esteja definido como **verdadeiro**.</li><li>**OSDAdapter0MacAddress** -endereço de controlador (MAC) utilizado para corresponde às definições do adaptador de rede físico de acesso de suporte.</li><li>**OSDAdapter0Name** – nome da ligação de rede conforme aparece no programa de painel de controlo de ligações de rede. O nome tem entre 0 e 255 carateres.</li><li>**OSDAdapter0Index** -índice das definições de adaptador de rede na matriz de definições.<br /><br />     OSDAdapterCount = 1<br />    OSDAdapter0EnableDHCP = FALSE<br />    OSDAdapter0IPAddressList = 192.168.0.40<br />    OSDAdapter0SubnetMask = 255.255.255.0<br />    OSDAdapter0Gateways = 192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (entrada)|Especifica o número de adaptadores de rede instalados no computador de destino. Quando o valor **OSDAdapterCount** estiver definido, têm de ser definidas todas as opções de configuração para cada adaptador. Por exemplo, se definir o valor **OSDAdapterTCPIPNetbiosOptions** para um adaptador específico, todos os valores para esse adaptador têm também de ser configurados.<br /><br /> <br /><br /> Se este valor não for especificado, todos os valores **OSDAdapter** serão ignorados.|  
|OSDDNSDomain<br /><br /> (entrada)|Especifica o servidor DNS primário utilizado pelo computador de destino.|  
|OSDDomainName<br /><br /> (entrada)|Especifica o nome do domínio Windows ao qual o computador de destino é associado. O valor especificado tem de ser um nome de domínio de Serviços de Domínio do Active Directory válido.|  
|OSDDomainOUName<br /><br /> (entrada)|Especifica o nome do formato RFC 1779 da unidade organizacional (UO) ao qual o computador de destino é associado. Se for especificado, o valor tem de conter o caminho completo.<br /><br /> Exemplo:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (entrada)|Especifica se a filtragem TCP/IP está ativada.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"**<br /><br /> **"falso"** (predefinição)|  
|OSDJoinAccount<br /><br /> (entrada)|Especifica a conta de rede que é utilizada para adicionar o computador de destino a um domínio Windows.|  
|OSDJoinPassword<br /><br /> (entrada)|Especifica a palavra-passe de rede que é utilizada para adicionar o computador de destino a um domínio Windows.|  
|OSDNetworkJoinType<br /><br /> (entrada)|Especifica se o computador de destino é associado a um domínio Windows ou a um grupo de trabalho.<br /><br /> **"0"** indica que o computador de destino é associado um domínio Windows. **"1"** especifica que o computador é associado um grupo de trabalho.<br /><br /> Valores válidos:<br /><br /> **"0"**<br /><br /> **"1"**|  
|OSDDNSSuffixSearchOrder<br /><br /> (entrada)|Especifica a ordem de procura DNS para o computador de destino.|  
|OSDWorkgroupName<br /><br /> (entrada)|Especifica o nome do grupo de trabalho ao qual o computador de destino é associado.<br /><br /> Tem de especificar este valor ou o valor **OSDDomainName** . O nome do grupo de trabalho pode ter um máximo de 32 carateres.<br /><br /> Exemplo:<br /><br /> **"Contabilidade"**|  

###  <a name="BKMK_ApplyOperatingSystem"></a> Variáveis de Ação da Sequência de Tarefas Aplicar Imagem do Sistema Operativo  
 As variáveis para esta ação especificam definições para o sistema operativo que pretende instalar no computador de destino. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [aplicar imagem do sistema operativo](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (entrada)|Especifica o nome de ficheiro do ficheiro de resposta de implementação do sistema operativo associado ao pacote de implementação do sistema operativo.|  
|OSDImageIndex<br /><br /> (entrada)|Especifica o valor de índice da imagem do ficheiro WIM aplicado ao computador de destino.|  
|OSDInstallEditionIndex<br /><br /> (entrada)|Especifica a versão do sistema operativo Windows Vista ou posterior que está instalado. Se não for especificada uma versão, a configuração do Windows determinará a versão a instalar utilizando a chave de produto referenciada.<br /><br /> Utilize apenas um valor de zero (0) se as condições seguintes forem verdadeiras:<br /><br /> -Estiver a instalar um sistema de operativo anterior ao Windows Vista<br />-Estiver a instalar uma edição de licença de volume do Windows Vista ou posterior, e é especificada qualquer chave de produto.<br /><br /> Valores válidos:<br /><br /> **"0"** (predefinição)|  
|OSDTargetSystemDrive (saída)|Especifica a letra de unidade da partição que contém os ficheiros do sistema operativo.|  

###  <a name="BKMK_ApplyWindowsSettings"></a> Variáveis de Ação da Sequência de Tarefas Aplicar Definições do Windows  
 As variáveis para esta ação especificam definições do Windows para o computador de destino, tal como o nome do computador, a chave de produto do Windows, o utilizador e a organização registados, e a palavra-passe de administrador local. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [aplicar definições do Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (entrada)|Especifica o nome do computador de destino.<br /><br /> Exemplo:<br /><br /> **"%_SMSTSMachineName%"** (predefinição)|  
|OSDProductKey<br /><br /> (entrada)|Especifica a chave de produto do Windows. O valor especificado tem de ter entre 1 e 255 carateres.|  
|OSDRegisteredUserName<br /><br /> (entrada)|Especifica o nome de utilizador registado predefinido no novo sistema operativo. O valor especificado tem de ter entre 1 e 255 carateres.|  
|OSDRegisteredOrgName<br /><br /> (entrada)|Especifica o nome da organização registado predefinido no novo sistema operativo. O valor especificado tem de ter entre 1 e 255 carateres.|  
|OSDTimeZone<br /><br /> (entrada)|Especifica a predefinição de fuso horário utilizada no novo sistema operativo.|  
|OSDServerLicenseMode<br /><br /> (entrada)|Especifica o modo de licenciamento do Windows Server utilizado.<br /><br /> Valores válidos:<br /><br /> **"PerSeat"**<br /><br /> **"PerServer"**|  
|OSDServerLicenseConnectionLimit<br /><br /> (entrada)|Especifica o número máximo de ligações permitido. O número especificado tem estar no intervalo de 5 a 9999 ligações.|  
|OSDRandomAdminPassword<br /><br /> (entrada)|Especifica uma palavra-passe gerada aleatoriamente para a conta de administrador no novo sistema operativo. Se definido como **verdadeiro**, a conta de administrador local será desativada no computador de destino. Se definido como **falso**, a conta de administrador local será ativada no computador de destino e a palavra-passe da conta de administrador local será atribuída o valor da variável **OSDLocalAdminPassword**.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"** (predefinição)<br /><br /> **"falso"**|  
|OSDLocalAdminPassword<br /><br /> (entrada)|Especifica a palavra-passe de administrador local. Este valor é ignorado se a opção **Gerar aleatoriamente a palavra-passe do administrador local e desativar a conta nas plataformas suportadas** estiver ativada. O valor especificado tem de ter entre 1 e 255 carateres.|  

###  <a name="BKMK_AutoApplyDrivers"></a> Variáveis de Ação da Sequência de Tarefas Aplicar Controladores Automaticamente  
 As variáveis para esta ação especificam os controladores do Windows que estão instalados no computador de destino e se estão instalados controladores não assinados. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [aplicar controladores automaticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (entrada)|Uma lista delimitada por vírgulas dos IDs exclusivos das categorias do catálogo de controladores. Se for especificado, a ação da sequência de tarefas **Aplicar Controladores Automaticamente** considerará apenas os controladores que se encontram em, pelo menos, uma destas categorias ao instalar controladores. Este valor é opcional e não está especificado por predefinição. Os IDs das categorias disponíveis podem ser obtidos através da enumeração da lista de objetos **SMS_CategoryInstance** no site.|  
|OSDAllowUnsignedDriver<br /><br /> (entrada)|Especifica se o Windows está configurado para permitir a instalação de controladores de dispositivo não assinados. Esta variável de sequência de tarefas não é utilizada na implementação do Windows Vista e sistemas operativos posteriores.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"**<br /><br /> **"falso"** (predefinição)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (entrada)|Especifica o que faz a ação da sequência de tarefas se existirem vários controladores de dispositivo no catálogo de controladores que são compatíveis com um dispositivo de hardware. Se definido como **"true"**, apenas o melhor controlador de dispositivo será instalado.  Se **falso**, todos os controladores de dispositivo compatíveis serão instalados e o sistema operativo irá escolher o melhor controlador a utilizar.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"** (predefinição)<br /><br /> **"falso"**|  

###  <a name="BKMK_CaptureNetworkSettings"></a> Variáveis de Ação da Sequência de Tarefas Capturar Definições de Rede  
 As variáveis para esta ação especificam se as informações de configuração das definições do adaptador de rede (TCP/IP, DNS e WINS) são capturadas e se as informações de associação a grupos de trabalho ou a domínios são migradas como parte da implementação do sistema operativo. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [capturar definições de rede](task-sequence-steps.md#BKMK_CaptureNetworkSettings).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (entrada)|Especifica se as informações de configuração das definições do adaptador de rede (TCP/IP, DNS e WINS) são capturadas.<br /><br /> Exemplos:<br /><br /> **"verdadeiro"** (predefinição)<br /><br /> **"falso"**|  
|OSDMigrateNetworkMembership<br /><br /> (entrada)|Especifica se as informações de associação a grupos de trabalho ou a domínios são migradas como parte da implementação do sistema operativo.<br /><br /> Exemplos:<br /><br /> **"verdadeiro"** (predefinição)<br /><br /> **"falso"**|  

###  <a name="BKMK_CaptureOperatingSystemImage"></a> Variáveis de Ação da Sequência de Tarefas Capturar Imagem do Sistema Operativo  
 As variáveis para esta ação especificam informações sobre a imagem do sistema operativo que está a ser capturada, tais como onde está armazenada a imagem, quem criou a imagem e uma descrição da imagem. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [Capturar imagem do sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  

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

###  <a name="BKMK_CaptureUserState"></a> Variáveis de Ação da Sequência de Tarefas Capturar Estado do Utilizador  
 As variáveis para esta ação especificam informações utilizadas pela User State Migration Tool (USMT), tais como a pasta onde o estado do utilizador é guardado, opções da linha de comandos para a USMT e os ficheiros de configuração utilizados para controlar a captura de perfis de utilizador.  Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [capturar estado do utilizador](task-sequence-steps.md#BKMK_CaptureUserState).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|O UNC ou o nome de caminho local da pasta onde o estado de utilizador é guardado. Não tem predefinição.|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (entrada)|Especifica opções user state migration tool (USMT) linha de comandos que são utilizadas ao capturar o estado do utilizador, mas não são expostas na interface de utilizador do Configuration Manager. As opções adicionais são especificadas sob a forma de cadeia que é acrescentada à linha de comando USMT gerada automaticamente.<br /><br /> <br /><br /> As opções da USMT especificadas com esta variável da sequência de tarefas não são validadas em termos de exatidão antes da execução da sequência de tarefas.|  
|OSDMigrateMode<br /><br /> (entrada)|Permite-lhe personalizar os ficheiros que são capturados pela USMT. Se esta variável é definida como "Simple", em seguida, são utilizados apenas os ficheiros de configuração de USMT padrão. Se esta variável é definida como "Advanced", em seguida, a variável de sequência de tarefas OSDMigrateConfigFiles Especifica os ficheiros de configuração que utiliza a USMT.<br /><br /> Valores válidos:<br /><br /> **"Simples"**<br /><br /> **"Avançada"**|  
|OSDMigrateConfigFiles<br /><br /> (entrada)|Especifica os ficheiros de configuração utilizados para controlar a captura de perfis de utilizador. Esta variável só é utilizada se OSDMigrateMode estiver definido como "Advanced". Este valor da lista delimitada por vírgulas está definido para efetuar a migração personalizada de perfis de utilizador.<br /><br /> Exemplo: miguser.xml,migsys.xml,migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (entrada)|Permite que a captura de estado do utilizador prossiga se não for possível capturar alguns ficheiros.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"** (predefinição)<br /><br /> **"falso"**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrada)|Ativa o registo verboso para a USMT.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"**<br /><br /> **"falso"** (predefinição)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (entrada)|Especifica se são capturados ficheiros encriptados.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"**<br /><br /> **"falso"** (predefinição)|  
|_OSDMigrateUsmtPackageID<br /><br /> (entrada)|Especifica o ID de pacote do pacote do Configuration Manager que irá conter os ficheiros da USMT. Esta variável é necessária.|  

###  <a name="BKMK_CaptureWindowsSettings"></a> Variáveis de Ação da Sequência de Tarefas Capturar Definições do Windows  
 As variáveis para esta ação especificam se as definições específicas do Windows são migradas para o computador de destino, como o nome do computador, o nome da organização registado e informações de fuso horário. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [capturar definições do Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (entrada)|Especifica se o nome do computador é migrado.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"** (predefinição)<br /><br /> **"falso"**<br /><br /> Se o valor for "true", em seguida, a variável OSDComputerName é definida com o nome NetBIOS do computador.|  
|OSDComputerName<br /><br /> (saída)|Definida como o nome NetBIOS do computador. O valor é definido apenas se a variável OSDMigrateComputerName for definida como "true".|  
|OSDMigrateRegistrationInfo<br /><br /> (entrada)|Especifica se as informações sobre a organização e o utilizador do computador são migradas.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"** (predefinição)<br /><br /> **"falso"**<br /><br /> Se o valor for "true", em seguida, a variável OSDRegisteredOrgName é definida como o nome da organização registado do computador.|  
|OSDRegisteredOrgName<br /><br /> (saída)|Definida como o nome da organização registado do computador. O valor é definido apenas se a variável OSDMigrateRegistrationInfo for definida como "true".|  
|OSDMigrateTimeZone<br /><br /> (entrada)|Especifica se o fuso horário do computador é migrado.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"** (predefinição)<br /><br /> **"falso"**<br /><br /> Se o valor for "true", em seguida, a variável OSDTimeZone é definida para o fuso horário do computador.|  
|OSDTimeZone<br /><br /> (saída)|Definida como o fuso horário do computador. O valor é definido apenas se a variável OSDMigrateTimeZone for definida como "true".|  

###  <a name="BKMK_ConnecttoNetworkFolder"></a> Variáveis de Ação da Sequência de Tarefas Ligar à Pasta de Rede  
 As variáveis para esta ação especificam informações sobre uma pasta numa rede, tais como a conta utilizada e a palavra-passe para ligar à pasta de rede, a letra de unidade da pasta e o caminho para a pasta. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [ligar à pasta de rede](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (entrada)|Especifica a conta de administrador que é utilizada para ligar à partilha de rede.|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (entrada)|Especifica a letra de unidade de rede à qual ligar. Este valor é opcional; se não for especificado, a ligação de rede não é mapeada para uma letra de unidade. Se este valor for especificado, o valor tem de estar compreendido no intervalo de D: a Z:.  Além disso, não utilize X:, uma vez que é a letra de unidade utilizada pelo Windows PE durante a fase Windows PE.<br /><br /> Exemplos:<br /><br /> **"D:"**<br /><br /> **"E:"**|  
|SMSConnectNetworkFolderPassword<br /><br /> (entrada)|Especifica a palavra-passe de rede que é utilizada para ligar à partilha de rede.|  
|SMSConnectNetworkFolderPath<br /><br /> (entrada)|Especifica o caminho de rede para a ligação.<br /><br /> Exemplo:<br /><br /> **"\\\servername\sharename"**|  

###  <a name="BKMK_EnableBitLocker"></a> Variáveis de Ação da Sequência de Tarefas Ativar BitLocker  
 As variáveis para esta ação especificam as opções de palavra-passe de recuperação e de chave de arranque utilizadas para ativar o BitLocker no computador de destino. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [ativar BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (entrada)|Em vez de gerar uma palavra-passe de recuperação aleatória, a ação da sequência de tarefas **Ativar BitLocker** utiliza o valor especificado como a palavra-passe de recuperação. O valor tem de ser uma palavra-passe de recuperação do BitLocker numérica válida.|  
|OSDBitLockerStartupKey<br /><br /> (entrada)|Em vez de gerar uma chave de arranque aleatória para a opção de gestão de chaves **chave de arranque em USB apenas,** o **ativar BitLocker** ação de sequência de tarefas utiliza o Trusted Platform Module (TPM) como a chave de arranque. O valor tem de ser uma chave de arranque do BitLocker codificada em Base64 de 256 bits válida.|  

###  <a name="BKMK_FormatPartitionDisk"></a> Variáveis de Ação da Sequência de Tarefas Formatar e Particionar Disco  
 As variáveis para esta ação especificam informações para formatação e criação de partições de um disco físico, como o número de disco e uma matriz de definições de partição. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [formatar e particionar disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (entrada)|Especifica o número do disco físico a particionar.|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (entrada)|Especifica se pretende desativar otimizações de alinhamento de cache ao particionar o disco rígido para compatibilidade com certos tipos de BIOS. Isto poderá ser necessário ao implementar os sistemas operativos Windows XP ou Windows Server 2003. Para mais informações, consulte o [artigo 931760](http://go.microsoft.com/fwlink/?LinkId=134081) e o [artigo 931761](http://go.microsoft.com/fwlink/?LinkId=134082) da Base de Dados de Conhecimento Microsoft.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"**<br /><br /> **"falso"** (predefinição)|  
|OSDGPTBootDisk<br /><br /> (entrada)|Especifica se pretende criar uma partição EFI num disco rígido GPT para que possa ser utilizado como disco de arranque em computadores baseados em EFI.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"**<br /><br /> **"falso"** (predefinição)|  
|OSDPartitions<br /><br /> (entrada)|Especifica uma matriz de definições de partição; consulte o tópico do SDK para aceder a variáveis de matriz no ambiente de sequência de tarefas.<br /><br /> Esta variável de sequência de tarefas é uma variável de matriz. Cada um dos elementos da matriz representa as definições para uma partição individual no disco rígido. As definições especificadas para cada partição são acedidas através da combinação do nome da variável de matriz com o número de partição do disco baseado em zero e o nome da propriedade.<br /><br /> Por exemplo, os nomes de variáveis seguintes podem ser utilizados para definir as propriedades para a primeira partição que será criada por esta ação de sequência de tarefas no disco rígido:<br /><br /> - **OSDPartitions0Type** -Especifica o tipo de partição. Esta propriedade é necessária. Os valores válidos são "**Principal**", "**Expandida**", "**Lógica**" e "**Oculta**".<br />-   **OSDPartitions0FileSystem** - especifica o tipo de sistema de ficheiros a utilizar ao formatar a partição. Esta propriedade é opcional; se não for especificado um sistema de ficheiros, a partição não será formatada. Os valores válidos são "**FAT32**" e "**NTFS**".<br />-   **OSDPartitions0Bootable** - especifica se a partição é de arranque. Esta propriedade é necessária. Se este valor for definido como "**VERDADEIRO**" para discos MBR, esta será tornada na partição ativa.<br />-   **OSDPartitions0QuickFormat** -especifica o tipo de formato utilizado. Esta propriedade é necessária. Se este valor for definido como "**VERDADEIRO**", será efetuada uma formatação rápida; caso contrário, será efetuada uma formação completa.<br />-   **OSDPartitions0VolumeName** - especifica o nome atribuído ao volume quando é formatado. Esta propriedade é opcional.<br />-   **OSDPartitions0Size** - especifica o tamanho da partição. As unidades são especificadas pela variável **OSDPartitions0SizeUnits** . Esta propriedade é opcional. Se esta propriedade não for especificada, a partição é criada utilizando todo o espaço livre restante.<br />-   **OSDPartitions0SizeUnits** - especifica as unidades que serão utilizadas ao interpretar a variável da sequência de tarefas **OSDPartitions0Size** . Esta propriedade é opcional. Os valores válidos são "**MB**" (predefinição), "**GB**" e "**Percentagem**".<br />-   **OSDPartitions0VolumeLetterVariable** - as partições utilizarão sempre a letra de unidade disponível seguinte no Windows PE quando forem criadas. Utilize esta propriedade opcional para especificar o nome de outra variável da sequência de tarefas, que será utilizado para guardar a nova letra de unidade para referência futura.<br /><br /> <br /><br /> Se pretender definir várias partições com esta ação de sequência de tarefas, as propriedades para a segunda partição podem ser definidas utilizando o respetivo índice no nome da variável; por exemplo, **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**, **OSDPartitions1VolumeName** , etc.|  
|OSDPartitionStyle<br /><br /> (entrada)|Especifica o estilo de partição a utilizar ao particionar o disco. "**MBR**" indica o estilo de partição de registo de arranque principal e "**GPT**" indica o estilo de Tabela de Partições GUID.<br /><br /> Valores válidos:<br /><br /> **"GPT"**<br /><br /> **"MBR"**|  

###  <a name="BKMK_InstallSoftwareUpdates"></a> Variáveis de Ação da Sequência de Tarefas Instalar Atualizações de Software  
 A variável para esta ação especifica se pretende instalar todas as atualizações ou apenas as atualizações obrigatórias. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [instalar atualizações de Software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (entrada)|Especifica se pretende instalar todas as atualizações ou apenas as atualizações obrigatórias.<br /><br /> Valores válidos:<br /><br /> **"Todas"**<br /><br /> **"Obrigatórias"**|  

###  <a name="BKMK_JoinDomainWorkgroup"></a> Variáveis de Ação da Sequência de Tarefas Associar Domínio ou Grupo de Trabalho  
 As variáveis para esta ação especificam informações necessárias para associar o computador de destino a um grupo de trabalho ou domínio do Windows. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [associar domínio ou grupo de trabalho](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (entrada)|Especifica a conta utilizada pelo computador de destino para associar o domínio do Windows. Esta variável é necessária ao associar um domínio.|  
|OSDJoinDomainName<br /><br /> (entrada)|Especifica o nome de um domínio Windows ao qual o computador de destino é associado. O comprimento do nome do domínio do Windows tem de ser entre 1 e 255 carateres.|  
|OSDJoinDomainOUName<br /><br /> (entrada)|Especifica o nome do formato RFC 1779 da unidade organizacional (UO) ao qual o computador de destino é associado. Se for especificado, o valor tem de conter o caminho completo. O comprimento do nome da UO do domínio do Windows tem de ser entre 1 e 32.767 carateres. Este valor não é definido se a variável **OSDJoinType** for definida como "1" (associar grupo de trabalho).<br /><br /> Exemplo:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDJoinPassword<br /><br /> (entrada)|Especifica a palavra-passe de rede que é utilizada pelo computador de destino para associar um domínio Windows. Se a variável não for especificada, é experimentada uma palavra-passe em branco. Este valor é necessário se a variável **OSDJoinType** for definida como "**0**" (associar domínio).|  
|OSDJoinSkipReboot<br /><br /> (entrada)|Especifica se pretende ignorar o reinício após o computador de destino ser associado ao domínio ou grupo de trabalho.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"**<br /><br /> **"falso"**|  
|OSDJoinType<br /><br /> (entrada)|Especifica se o computador de destino é associado a um domínio Windows ou a um grupo de trabalho. Para associar o computador de destino a um domínio Windows, especifique "**0**". Para associar o computador de destino a um grupo de trabalho, especifique "**1**".<br /><br /> Valores válidos:<br /><br /> **"0"**<br /><br /> **"1"**|  
|OSDJoinWorkgroupName<br /><br /> (entrada)|Especifica o nome de um grupo de trabalho ao qual o computador de destino é associado. O comprimento do nome do grupo de trabalho tem de ser entre 1 e 32 carateres.<br /><br /> Exemplo:<br /><br /> **"Contabilidade"**|  

###  <a name="BKMK_PrepareWindowsCapture"></a> Variáveis de Ação da Sequência de Tarefas Preparar Windows para Captura  
 As variáveis para esta ação especificam informações utilizadas para capturar o sistema operativo Windows a partir do computador de destino. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [preparar ConfigMgr Client para captura](task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (entrada)|Especifica se o sysprep cria uma lista de controladores de dispositivo de armazenamento em massa. Esta definição aplica-se apenas ao Windows XP e ao Windows Server 2003. Preencherá a secção [SysprepMassStorage] de sysprep.inf com informações sobre todos os controladores de armazenamento em massa que são suportadas pela imagem a capturar.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"**<br /><br /> **"falso"** (predefinição)|  
|OSDKeepActivation<br /><br /> (entrada)|Especifica se o sysprep repõe o sinalizador de ativação do produto.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"**<br /><br /> **"falso"** (predefinição)|  
|OSDTargetSystemRoot<br /><br /> (saída)|Especifica o caminho para o diretório do Windows do sistema operativo instalado no computador de referência. Este sistema operativo é validado como sistema operativo suportado para captura pelo Configuration Manager.|  

###  <a name="BKMK_ReleaseStateStore"></a> Variáveis de Ação da Sequência Disponibilizar Armazenamento de Estados  
 As variáveis para esta ação especificam informações utilizadas para libertar o estado do utilizador armazenado. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [disponibilizar armazenamento de Estados](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|O UNC ou nome do caminho local para a localização a partir da qual o estado do utilizador é restaurado. Este valor é utilizado pela ação da sequência de tarefas **Capturar Estado do Utilizador** e pela ação da sequência de tarefas **Restaurar Estado do Utilizador** .|  

###  <a name="BKMK_RequestState"></a> Variáveis de Ação da Sequência de Tarefas Solicitar Armazenamento de Estados  
 As variáveis para esta ação especificam informações utilizadas para solicitar o estado do utilizador armazenado, como a pasta no ponto de migração de estado onde os dados de utilizador são armazenados. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [disponibilizar armazenamento de Estados](../../osd/understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (entrada)|Especifica se a Conta de Acesso à Rede é utilizada como contingência quando a conta de computador falha a ligação ao ponto de migração de estado.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"**<br /><br /> **"falso"** (predefinição)|  
|OSDStateSMPRetryCount<br /><br /> (entrada)|Especifica o número de vezes que o passo de sequência de tarefas tenta encontrar um ponto de migração de estado antes de o passo falhar. O número especificado tem de estar compreendido entre 0 e 600.|  
|OSDStateSMPRetryTime<br /><br /> (entrada)|Especifica o número de segundos que o passo de sequência de tarefas aguarda entre as tentativas. O número de segundos pode ter um máximo de 30 carateres.|  
|OSDStateStorePath<br /><br /> (saída)|O caminho UNC para a pasta no ponto de migração de estado onde o estado do utilizador está armazenado.|  

###  <a name="BKMK_RestartComputer"></a> Variáveis de Ação da Sequência de Tarefas Reiniciar Computador  
 As variáveis para esta ação especificam informações utilizadas para reiniciar o computador de destino. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [reiniciar o computador](task-sequence-steps.md#BKMK_RestartComputer).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (entrada)|Especifica a mensagem a apresentar aos utilizadores antes de reiniciar o computador de destino. Se esta variável não for definida, será apresentado o texto da mensagem predefinida. A mensagem especificada não pode exceder os 512 carateres.<br /><br /> Exemplo:<br /><br /> -"Este computador será reiniciado; Guarde o seu trabalho."|  
|SMSRebootTimeout<br /><br /> (entrada)|Especifica o número de segundos durante o qual o aviso é apresentado ao utilizador antes de o computador ser reiniciado. Especifique zero segundos para indicar que não é apresentada qualquer mensagem de reinício.<br /><br /> Exemplos:<br /><br /> **"0"** (predefinição)<br /><br /> **"5"**<br /><br /> **"10"**|  

###  <a name="BKMK_RestoreUserState"></a> Variáveis de Ação da Sequência de Tarefas Restaurar Estado do Utilizador  
 As variáveis para esta ação especificam informações utilizadas para restaurar o estado do utilizador do computador de destino, como o nome do caminho da pasta a partir da qual o estado do utilizador é restaurado e se a conta de computador local é restaurada. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [restaurar estado do utilizador](task-sequence-steps.md#BKMK_RestoreUserState).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|O UNC ou nome do caminho local da pasta a partir da qual o estado do utilizador é restaurado.|  
|OSDMigrateContinueOnRestore<br /><br /> (entrada)|Especifica que o restauro do estado do utilizador continua, mesmo se não for possível restaurar alguns ficheiros.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"** (predefinição)<br /><br /> **"falso"**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrada)|Ativa o registo verboso para a ferramenta USMT. Este valor é necessário para a ação; tem de ser definido como "verdadeiro" ou "falso".<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"**<br /><br /> **"falso"** (predefinição)|  
|OSDMigrateLocalAccounts<br /><br /> (entrada)|Especifica se a conta de computador local é restaurada.<br /><br /> Valores válidos:<br /><br /> **"verdadeiro"**<br /><br /> **"falso"** (predefinição)|  
|OSDMigrateLocalAccountPassword<br /><br /> (entrada)|Se o **OSDMigrateLocalAccounts** variável é "verdadeiro", esta variável deve conter a palavra-passe que está atribuída a todas as contas locais que forem migradas. Porque a mesma palavra-passe é atribuída a todas as contas locais migradas, é considerada uma palavra-passe temporária que será alterada mais tarde por algum método diferente de implementação do sistema operativo do Configuration Manager.|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (entrada)|Especifica opções adicionais da linha de comandos da User State Migration Tool (USMT), que são utilizadas ao restaurar o estado do utilizador. As opções adicionais são especificadas sob a forma de cadeia que é acrescentada à linha de comando USMT gerada automaticamente. As opções da USMT especificadas com esta variável da sequência de tarefas não são validadas em termos de exatidão antes da execução da sequência de tarefas.|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (entrada)|Especifica o ID de pacote do pacote do Configuration Manager que contém os ficheiros da USMT. Esta variável é necessária.|  

###  <a name="BKMK_RunCommand"></a> Variáveis de Ação da Sequência de Tarefas Executar Linha de Comandos  
 As variáveis para esta ação especificam informações utilizadas para executar um comando a partir da linha de comandos, tal como o diretório de trabalho onde o comando é executado. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [executar linha de comandos](task-sequence-steps.md#BKMK_RunCommandLine).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação|Descrição|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (entrada)|Por predefinição, numa execução num sistema operativo de 64 bits, o programa na linha de comandos é localizado e executado com o redirecionador do sistema de ficheiros WOW64, para que sejam encontradas as versões de 32 bits dos programas e DLLs do sistema operativo. A definição desta variável como "true" desativa a utilização do redirecionador do sistema de ficheiros WOW64, para que sejam encontradas as versões de 64 bits nativas do sistema operativo programas e DLLs. Esta variável não produz qualquer efeito numa execução num sistema operativo de 32 bits.|  
|WorkingDirectory<br /><br /> (entrada)|Especifica o diretório inicial para uma ação da linha de comandos. O nome do diretório especificado não pode exceder os 255 caracteres.<br /><br /> Exemplos:<br /><br /> -   **"C:\\"**<br />-   **"%SystemRoot%"**|  
|SMSTSRunCommandLineUserName<br /><br /> (entrada)|Especifica a conta através da qual a linha de comandos é executada. O valor é uma cadeia de formato nomedeutilizador ou domínio\nomedeutilizador.|  
|SMSTSRunCommandLinePassword<br /><br /> (entrada)|Especifica a palavra-passe para a conta especificada pela variável SMSTSRunCommandLineUserName.|  

### <a name="set-dynamic-variables"></a>Definir Variáveis Dinâmicas  
 As variáveis para esta ação são configuradas automaticamente quando adicionar o passo de sequência de tarefas Definir Variáveis Dinâmicas. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [definir variáveis dinâmicas](task-sequence-steps.md#BKMK_SetDynamicVariables).  

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

###  <a name="BKMK_SetupWindows"></a> Variáveis de Ação da Sequência de Tarefas Configurar Windows e ConfigMgr  
 A variável para esta ação Especifica as propriedades de instalação de cliente que são utilizadas ao instalar o cliente do Configuration Manager. Para obter mais informações sobre o passo de sequência de tarefas associado a estas variáveis, consulte [configurar Windows e ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (entrada)|Especifica as propriedades de instalação de cliente que são utilizadas ao instalar o cliente do Configuration Manager.|  

### <a name="upgrade-operating-system"></a>Atualizar Sistema Operativo  
 A variável para esta ação Especifica opções adicionais da linha de comandos que não estão disponíveis no Gestor de configuração de consola são adicionadas à configuração para uma atualização do Windows 10. Para obter mais informações sobre o passo de sequência de tarefas associado esta variável, consulte [atualizar sistema operativo](task-sequence-steps.md#BKMK_UpgradeOS).  

#### <a name="details"></a>Detalhes  

|Nome da Variável de Ação<br /><br /> (entrada)|Descrição|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (entrada)|Especifica as opções adicionais da linha de comandos que são adicionadas à Configuração durante uma atualização do Windows 10. As opções da linha de comandos não são verificadas. Por isso, verifique se a opção que introduz é precisa.<br /><br /> Para obter mais informações, consulte [Windows Setup Command-Line Options (Opções da Linha de Comandos de Configuração do Windows)](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx).|  

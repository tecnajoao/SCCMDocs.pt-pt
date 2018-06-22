---
title: Resolver problemas de MDT
titleSuffix: Microsoft Deployment Toolkit
description: 'Referência de resolução de problemas para o Microsoft Deployment Toolkit '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 91a7a69a-deac-4b0f-aac9-b7bd187c53fb
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: efb65086878a46bfb3485fdd8b0be6f613225261
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/27/2018
ms.locfileid: "27821556"
---
# <a name="troubleshooting-reference-for-the-microsoft-deployment-toolkit"></a>Referência de resolução de problemas para o Microsoft Deployment Toolkit
 A implementação de sistemas operativos e aplicações, bem como a migração de estado do utilizador pode ser um endeavor um desafio, mesmo quando estão equipados com as ferramentas apropriadas e orientação. Esta referência, o qual faz parte do Microsoft® Deployment Toolkit (MDT) 2013, fornece informações sobre problemas conhecidos atuais, possíveis soluções para esses problemas e a orientação de resolução de problemas.  

> [!NOTE]
>  Neste documento, *Windows* aplica-se aos sistemas operativos Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2, exceto indicação em contrário. MDT não suporta ARM processador versões do Windows. Da mesma forma, *MDT* refere-se ao MDT 2013, salvo indicação em contrário.  

> [!NOTE]
>  A Microsoft Diagnostics e Recovery Toolset (DaRT) contém ferramentas poderosas para recuperar e resolução de problemas de computadores cliente que não são iniciados ou ficam instável. Pode utilizar DaRT para determinar a causa de uma falha, restaurar ficheiros perdidos e assim sucessivamente. Também pode utilizar DaRT como uma ferramenta de resolução de problemas quando desenvolver e implementar um sistema operativo Windows. Por exemplo, se uma imagem incorporada não conseguir iniciar corretamente, pode iniciar o computador cliente que contém a imagem utilizando ERD Commander — um ambiente de diagnóstico. Em seguida, pode explorar o disco rígido do computador cliente, ver o registo de eventos, remover as atualizações, alterar definições do sistema operativo e assim sucessivamente. DaRT faz parte do Microsoft Desktop Optimization Pack para o Software Assurance. Para saber mais sobre DaRT, consulte o artigo [ http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx ](http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx).  

## <a name="understanding-logs"></a>Noções sobre registos  
 Antes de pode começar a resolução de problemas Efetivo do MDT, tem de ter uma compreensão clara dos ficheiros. log muitos utilizada durante uma implementação de sistema operativo. Quando souber que registo de ficheiros para pesquisar que condição de falha e, em que altura, problemas que uma vez foram mysterious e complicado perceber podem tornar-se limpar e compreensíveis.  

 O formato de ficheiro de registo do MDT foi concebido para ser lidos por Trace32, o que faz parte do System Center Configuration Manager 2007 Toolkit V2, disponível para transferência a partir do [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=9257). Os registos também podem ser lidos pelo Gestor de rastreio ferramenta de registo Configuration (CMTrace) que está disponível com o System Center 2012 Configuration Manager e versões posteriores. Utilize estas ferramentas sempre que possível ler os ficheiros de registo, porque faz a localizar erros muito mais fácil.  

 O resto desta secção determina os ficheiros de registo criados durante a implementação, bem como durante a configuração do Windows. Esta secção também fornece exemplos de quando deve utilizar os ficheiros para resolução de problemas.  

### <a name="mdt-logs"></a>Registos de MDT  
 Cada script MDT cria automaticamente os ficheiros de registo quando em execução. Os nomes destes ficheiros de registo corresponde ao nome do script — por exemplo, ZTIGather.wsf cria um ficheiro de registo com o nome *ZTIGather.log*. Cada script também atualiza um comuns mestre ficheiro de registo (BDD.log) que agrega os conteúdos dos ficheiros de registo que criar scripts do MDT. Ficheiros de registo do MDT residirem no C:\MININT\SMSOSD\OSDLOGS durante o processo de implementação. Dependendo do tipo de implementação que está a ser efetuada, os ficheiros de registo são movidos após a conclusão da implementação %WINDIR%\SMSOSD ou % WINDIR%\TEMP\SMSOSD. Para implementações do Lite Touch Installation (LTI), os registos iniciar C:\MININT\SMSOSD\OSDLogs. Estes acabar em %WINDIR%\TEMP\DeploymentLogs quando o processamento de sequência de tarefas está concluído.  

 MDT cria os seguintes ficheiros de registo:  

-   **BDD.log**. Este é o ficheiro de registo agregado do MDT que é copiado para uma localização de rede no fim da implementação, se especificar o **SLShare** propriedade no ficheiro Customsettings.ini.  

-   **LiteTouch.log**. Este ficheiro é criado durante a implementações LTI. Reside no %WINDIR%\TEMP\DeploymentLogs a menos que especifique o **/debug:true** opção.  

-   **Scriptname*.log**. Este ficheiro é criado por cada script MDT. *ScriptName* representa o nome do script em questão.  

-   **SMSTS.log**. Este ficheiro é criado pelo sequenciador de tarefas e descreve todas as transações do sequenciador de tarefas. Dependendo do cenário de implementação, pode residir no % TEMP %, % WINDIR%\System32\ccm\logs ou c:\\\_SMSTaskSequence ou C:\SMSTSLog.  

-   **Wizard.log**. Os assistentes de implementação criar e atualizar este ficheiro.  

-   **WPEinit.log**. Este ficheiro é criado durante o processo de inicialização do Windows PE e é útil para resolução de problemas de erros encontrados ao iniciar o Windows PE.  

-   **DeploymentWorkbench_*id*.log**. Este ficheiro de registo é criado na pasta % temp % quando especificar **um /depurar** quando iniciar o Deployment Workbench.  

### <a name="configuration-manager-operating-system-deployment-logs"></a>Registos de implementação do sistema do Configuration Manager  
 Para obter informações sobre o sistema operativo que criados pelo Microsoft System Center 2012 R2 Configuration Manager de ficheiros de registo de implementação, consulte [referência técnica para ficheiros de registo no Configuration Manager](http://technet.microsoft.com/library/hh427342.aspx).  

 Ao executar o Windows utilizador State Migration Tool (USMT), o MDT adiciona automaticamente as opções de registo para guardar os ficheiros de registo do USMT para as localizações de ficheiros de registo do MDT. Os ficheiros de registo e quando forem criados são os seguintes:  

-   **USMTEstimate.log**. Criado quando estimar os requisitos do USMT  

-   **USMTCapture.log**. Criado pela USMT quando capturar os dados  

-   **USMTRestore.log**. Criado pela USMT ao restaurar os dados  

 O script de ZeroTouchInstallation.vbs efetua análises automáticas aos ficheiros de registo de progresso do USMT para erros e avisos. O script gera o ID de evento 41010 ao Microsoft System Center Operations Manager com o resumo seguinte (onde *usmt_type* é **estimativa**, **SCANSTATE**, ou  **LOADSTATE**; *error_count* é o número total de erros encontrados; e *warning_count* é o número total de avisos encontrado):  

```  
ZTI USMT <usmt_type> reported <error_count> errors and <warning_count> warnings  
```  

 Se o número de erro for maior que 0, este evento é um tipo de erro. Se a contagem de aviso é maior que 0 sem erros, o evento é um tipo de aviso. Caso contrário, o evento é um tipo informativo.  

## <a name="identifying-error-codes"></a>Identificar os códigos de erro  
Tabela 1 apresenta uma lista os códigos de erro que criar os scripts do MDT e fornece uma descrição de cada código de erro. Estes códigos de erro são registados no ficheiro BDD.log.  

### <a name="table-1-error-codes-and-their-description"></a>Tabela 1. Códigos de erro e a respetiva descrição  

|**Código de erro**|**Descrição**|  
|-|-|  
|5201|Não foi possível estabelecer uma ligação para a partilha de implementação. Não irá continuar a implementação.|  
|5203|Não foi possível estabelecer uma ligação para a partilha de implementação. Não irá continuar a implementação.|  
|5205|Não foi possível estabelecer uma ligação para a partilha de implementação. Não irá continuar a implementação.|  
|5206|O Assistente de implementação foi cancelado ou não foi concluída com êxito. Não irá continuar a implementação.|  
|5207|Não foi possível estabelecer uma ligação para a partilha de implementação. Não irá continuar a implementação.|  
|5208|**DeploymentType** não está definido. Tem de definir um valor para **SkipWizard**.|  
|5208|Não é possível localizar o sequenciador de tarefas de SMS. Não irá continuar a implementação.|  
|5400|Crie o objeto: **Definir *class_instance* = New *class_name***|  
|5490|Create MSXML2.DOMDocument.|  
|5495|Create MSXML2.DOMDocument.ParseErr.ErrCode.|  
|5496|LoadControlFile.FindFile: *ConfigFile*|  
|5601|Certifique-se de SO guid: % OSGUID % existe.|  
|5602|Abra a XML com OSGUID: % OSGUID %.|  
|5610|Verifique se o ficheiro.|  
|5630|Verifique se o ficheiro: *ImagePath*.|  
|5640|Verifique se o ficheiro: *ImagePath*.|  
|5641|FindFile: ImageX.exe.|  
|5643|Localize BootSect.exe.|  
|5650|Verificar diretório: *SourcePath*.|  
|5651|Verificar diretório: *SourcePath*\Platform.|  
|5652|FindFile: bootsect.exe.|  
|6001|Certifique-se a unidade.|  
|6002|Certifique-se a unidade.|  
|6010|Testar TSGUID.|  
|6020|Robocopy valor devolvido: *Valor*.|  
|6021|Robocopy valor devolvido: *Valor*.|  
|6101|Verifique a existência de ficheiros: *DeployCab*.|  
|6102|Expanda os ficheiros Sysprep de implementar. FICHEIRO CAB.|  
|6111|Execute o Sysprep.exe.|  
|6121|Execute o Sysprep.|  
|6191|Testar **CloneTag** no registo para verificar o Sysprep foi concluída.|  
|6192|Testar **SystemSetupInProgress** no registo para verificar o Sysprep foi concluída.|  
|6401|Servidor DHCP autorizado.|  
|6501|Não é possível da cópia de segurança do computador, nenhum caminho de rede (**BackupShare**, **BackupDir**) especificado.|  
|6502|ERRO - não é possível localizar o IMAGEX, não é possível efetuar a cópia de segurança.|  
|6601|GetObject (... raiz/wmi:BCDStore).|  
|6602|BCD. OpenStore (*BCDStore*).|  
|6701|Protetores de configurado.|  
|6702|Mover os ficheiros do arranque.|  
|6703|Crie BDE partição.|  
|6704|Desfragmentar a unidade.|  
|6705|Reduzir a unidade.|  
|6706|Para mais de 1 partição de teste.|  
|6707|Crie ficheiros do arranque.|  
|6708|Encriptar o disco.|  
|6709|Ligar ao fornecedor WMI de MicrosoftVolumeEncryption.|  
|6710|Encriptar o disco.|  
|6711|**ProtectKeyWithTPM**.|  
|6712|**ProtectKeyWithTPMAndPIN**.|  
|6713|**ProtectKeyWithTPMAndStartupKey**.|  
|6714|Guarde o ficheiro de chave externa.|  
|6715|Proteger com a chave externa.|  
|6716|Guarde o ficheiro de chave externa.|  
|6717|Proteger a chave com palavra-passe numérica.|  
|6718|**GetKeyProtectorNumberialP@ssword.**|  
|6718|Guarde palavra-passe para o ficheiro.|  
|6719|Abra *PasswordFile*.|  
|6720|Encriptar a unidade.|  
|6721|Abra *DiskPartFile*.|  
|6722|Crie a partição.|  
|6723|Obter unidade BDE existente.|  
|6724|Abra *DiskPartFile*.|  
|6727|Tentativa de abrir *DiskPartFile*.|  
|6729|Criar ficheiro de texto *DiskPartFile*.|  
|6730|Executar **cmd /c DISKPART. EXE /s *DiskPartFile* >> *LogPath*\ZTIMarkActive_diskpart.log 2 > & 1**|  
|6731|Localize bcdboot.exe.|  
|6732|Ligar ao fornecedor de Microsoft TPM.|  
|6733|Obter uma instância da TPM na classe de fornecedor.|  
|6734|Obter a instância da TPM.|  
|6735|Verifique se o TPM está ativado.|  
|6736|Verifique se o TPM está ativado.|  
|6737|Verifique se o TPM tem proprietário.|  
|6738|Verifique se a propriedade TPM é permitida.|  
|6739|Verifique se o TPM está ativado.|  
|6740|Verifique se o TPM está ativado.|  
|6741|Verifique se o TPM tem proprietário e a propriedade é permitida.|  
|6741|Conjunto de palavra-passe proprietário do TPM|  
|6742|Proprietário do TPM P@ssword definido como **AdminP@ssword**.|  
|6743|Definir o proprietário do TPM P@ssword como valor.|  
|6744|Verifique se o TPM está ativado.|  
|6745|Verifique o proprietário do TPM.|  
|6746|Procurar par de chaves de endossamento.|  
|6747|Verifique se o TPM está ativado.|  
|6748|Verifique se a propriedade TPM é permitida.|  
|6749|Converter o proprietário p@ssword para autorização do proprietário.|  
|6750|Crie par de chaves de endossamento.|  
|6751|Alterar a autorização do proprietário.|  
|6752|Executar **Cmd**.|  
|6753|Valide o TPM.|  
|6754|Obter a instância BDE.|  
|6755|Proteger a chave com o TPM.|  
|6756|Verifique a existência de suporte de dados amovível configurar. **ProtectKeyWithTpmAndStartupKey**.|  
|6757|Proteger a chave com o TPM e chave de arranque.|  
|6758|Procure BDE pin.|  
|6759|Proteger a chave com o TPM e Pin.|  
|6760|Localizar o suporte de dados amovível para **BDEKeyLocation**.|  
|6761|Proteger com a chave externa.|  
|6762|Recuperação P@ssword sejam guardados *PasswordFile*.|  
|6764|Configure a política do BitLocker.|  
|7000|Não é possível localizar ZTIConfigure.xml; abortar.|  
|7001|Está à procura de instalação autónoma AnswerFile.|  
|7100|Erro - este script só deve executar no SO completo.|  
|7101|ERRO - não suficiente valores fornecidos para gerar ficheiro de resposta do DCPromo.|  
|7102|Erro - propriedades obrigatórias para criar uma nova réplica DC não foram especificadas.|  
|7103|Erro - propriedades obrigatórias para criar um novo domínio subordinado não foram especificadas.|  
|7104|Erro - propriedades obrigatórias para criar uma nova floresta não foram especificadas.|  
|7105|Erro - propriedades obrigatórias para criar uma nova floresta não foram especificadas.|  
|7200|Não é possível configurar o servidor DHCP porque o serviço não está instalado.|  
|7201|Não é possível ler os detalhes de âmbito; `GetScopeDetails()` falhou.|  
|7202|Insuficiente valores especificados para a criação de âmbito.|  
|7203|Insuficiente valores fornecidos para definir o intervalo IP para este âmbito.|  
|7204|Um valor especificado para o intervalo de exclusão de âmbito.|  
|7300|Não é possível emitir comandos DNS.|  
|7700|Não é um cenário de novo computador; partição de disco a ser fechado.|  
|7701|Disco não é suficientemente grande para partições de sistema e BDE, necessárias = 1,5 GB.|  
|7702|Disco não é suficientemente grande para partições de sistema e WinRE, necessárias = 10 GB.|  
|7703|DeployRoot está no disco # *DiskIndex*. Executar um cenário de OEM: Ignore.|  
|7704|Executar um cenário de OEM: Ignore.|  
|7704|As partições expandidas e lógicas não são permitidas com o BitLocker.|  
|7712|Verificar a unidade /*unidade do Volume* está presente. formato.|  
|7900|Findfile: Microsoft.BDD.PnpEnum.exe.|  
|7901|**AllDrivers.Exists("*GUID*").**|  
|7904|**AllDrivers.Exists("*GUID*").**|  
|9200|Findfile(PkgMgr.exe).|  
|9601|ERRO - a tarefa de restauro de estado de ZTITatoo deve estar a executar no SO completo; abortar.|  
|9701|Código de retorno diferentes de zero de estimativa do USMT, rc = *erro*.|  
|9702|Captura de estado de utilizador não é possível; espaço insuficiente de local e nenhum caminho de rede (UDShare, UDDir) especificado.|  
|9703|Código de retorno diferentes de zero da captura do USMT, rc = *erro*.|  
|9704|Não foi especificada nenhuma opção de linha de comandos válida.|  
|9801|Erro - ao tentar implementar um sistema operativo cliente para uma máquina com um sistema operativo do servidor.|  
|9802|Erro - ao tentar implementar um sistema operativo do servidor numa máquina com um sistema operativo do cliente.|  
|9803|Erro - Machine não está autorizado para atualizar (OSInstall =*OSInstall*); abortar.|  
|9804|ERRO - *memória* MB de memória é insuficiente. Pelo menos *memória* MB de memória é necessária.|  
|9805|Erro - velocidade de processador de *ProcessorSpeed* MHz é insuficiente.  Pelo menos um *ProcessorSpeed* processador MHz é necessária.|  
|9806|ERRO - o espaço insuficiente está disponível no *unidade*. Mais *tamanho* MB é necessário.|  
|9807|ERRO - o espaço insuficiente está disponível no *unidade*. Mais *tamanho* MB é necessário.|  
|9901|O script de ZTIWindowsUpdate não deverá ser executado no Windows PE.|  
|9902|ZTIWindowsUpdate tem de executar e falhou demasiadas vezes. Contagem = *contagem*.|  
|9903|Problema inesperado instalar o agente de atualização de Windows atualizada, rc = *erro*.|  
|9904|Falha ao criar o objeto: **Microsoft.Update.Session**.|  
|9905|Falha ao criar o objeto: **Microsoft.Update.UpdateColl**.|  
|9906|Ficheiros críticos *ficheiro* não encontrada; abortar.|  
|10000|Crie o objeto: **Definir oLTICleanup = LTICleanup novo**.|  
|10201|Não é possível associar domínio *domínio*. Pare a instalação.|  
|10203|FindFile(LTISuspend.wsf).|  
|10204|Executar programa *LTISuspend*.|  
|41024|Execute o ImageX.|  
|52012|Todos os parâmetros de assistente não estão definidos.|  

 Listar 1 fornece um excerpt de um ficheiro de registo que ilustra como encontrar o código de erro. Este excerpt, o código de erro comunicado é 5001.  

 **Listar 1. Excerpt a partir de um ficheiro SMSTS.log que contém o código de erro 5001**  

```  
.  
.  
.  
The operating system installation failed. Please contact your system administrator for assistance.  

The action "Zero Touch Installation - Validation" failed with exit code 5001  
.  
.  
.  

```  

### <a name="converting-error-codes"></a>Converter os códigos de erro  
 Vários códigos de erro apresentados nos ficheiros de registo parecem crípticas e difícil está correlacionado com uma condição de erro real. No entanto, o processo seguinte demonstra como converter um código de erro e obter informações importantes que poderão ajudar na resolução do problema.  

 **Problema**: Captura de imagem falha com o código de erro 0x80070040.  

 **Solução possível 1**: O código de erro apresentado está no formato hexadecimal que precisa para converter para formato decimal. Para tal, precisa de uma calculadora científicos e a Calculadora incluída com sistemas operativos Windows é adequada para esta tarefa.  

 **Para converter um código de erro**  

1.  Clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **acessórios**e, em seguida, clique em **Calculadora**.  

2.  Do **vista** menu, clique em **científica**.  

3.  Selecione **Hex**e, em seguida, introduza os últimos quatro dígitos do código — neste caso, **0040**, conforme mostrado na figura 1.  

     ![TroubleshootingReference1](media/TroubleshootingReference1.jpg "TroubleshootingReference1")  
Figura 1. Conversão de erro  

     **Figura 1. Conversão de erro**  

     Tenha em atenção que zeros à esquerda não são apresentadas enquanto a Calculadora está no modo Hexadecimal.  

4.  Selecione **Dec**.  

     O valor hexadecimal *40* é convertido para um valor decimal de *64*.  

5.  Abra uma janela da linha de comandos, escreva **NET HELPMSG 64**, e, em seguida, prima ENTER.  

     O **NET HELPMSG** comando traduz o código de erro numérica para um texto significativo. No caso do código de erro fornecido aqui, traduz "o nome de rede especificado já não está disponível."  

 Estas informações indica que um problema de rede pode existir no computador de destino ou entre o computador de destino e o servidor no qual reside a partilha de implementação. Estes problemas podem incluir controladores de rede que não a ser instalados corretamente ou um erro de correspondência na velocidade e definições duplex.  

 **Solução possível 2:** Utilize o utilitário de consulta de código de erro do Microsoft Exchange Server. Este utilitário da linha de comandos é útil em assistência com tradução de código de erro. Está disponível para transferência a partir do [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=985).  

### <a name="review-of-sample-logs"></a>Revisão de registos de exemplo  
 MDT cria ficheiros de registo que pode utilizar para resolver problemas no processo de implementação do MDT. As secções seguintes fornecem exemplos sobre como utilizar os ficheiros de registo do MDT para resolver o processo de implementação:  

-   Problemas relacionados com falhas de acesso à base de dados do MDT (MDT DB), conforme descrito em [falha para aceder à base de dados](#FailuretoAccesstheDatabase)  

####  <a name="FailuretoAccesstheDatabase"></a> Falha ao aceder à base de dados  
 **Problema:** Ocorre um erro ao executar uma implementação que utilizar um ficheiro CustomSettings.ini contém várias secções e especificar, com o **prioridade** propriedade, a prioridade de cada secção a ser processado. BDD.log contém as seguintes mensagens de erro:  

-   ```  
    ERROR - Opening Record Set (Error Number = -2147217911) (Error Description: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'.)  
    ```  

-   ```  
    ADO error: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'. (Error #-2147217911; Source: Microsoft OLE DB Provider for SQL Server; SQL State: 42000; NativeError: 229  
    ```  

-   ```  
    ERROR - Unhandled error returned by ZTIGather: Object required (424)  
    ```  

> [!NOTE]
>  Para efeitos de clareza, os conteúdos do ficheiro de registo acima tem sido representados como aparecem ao que está a ser visualizado através do programa de Trace32.  

 **Possíveis soluções:** O problema, como a indicada na primeira linha do exemplo de ficheiro de registo, é que a permissão para aceder à base de dados foi negada. Por conseguinte, o script não é possível estabelecer uma ligação segura para a base de dados, possivelmente devido um ID de utilizador e palavra-passe não estavam disponíveis. Como resultado, o acesso de base de dados foi tentado com a conta de computador. A forma mais fácil para contornar este problema é para conceder todas as pessoas acesso de leitura à base de dados.  

## <a name="troubleshooting"></a>Resolução de Problemas  
 Antes de aderir a no\-processos de resolução de problemas de profundidade, reveja os seguintes itens e certifique-se de que quaisquer requisitos associados foram cumpridos:  

-   Problemas de instalação podem resultar se não tiverem sido cumpridos todos os pré-requisitos de software e hardware.  

### <a name="application-installation"></a>Instalação da aplicação  
 Reveja os problemas e soluções para problemas de instalação da aplicação:  

-   Ficheiros de origem de instalação que estão bloqueados por motivos de segurança, conforme descrito em [executáveis bloqueado](#BlockedExecutables)  

-   Perda de conectividade de rede conforme descrito em [perdido ligações de rede](#LostNetworkConnections)  

-   Erro de instalação 30029 ao instalar o sistema Microsoft Office 2007 ou os ficheiros relacionados, conforme descrito em [o 2007 Microsoft Office System](#MicrosoftOfficeSystem)  

####  <a name="BlockedExecutables"></a> Executáveis bloqueado  
 **Problema:** Se os ficheiros de origem de instalação são transferidos a partir da Internet, é provável que serão marcados com um ou mais fluxos de dados do sistema ficheiros NTFS. Para obter mais informações sobre fluxos de dados NTFS, consulte [ficheiro fluxos](http://msdn2.microsoft.com/library/aa364404\(VS.85\).aspx). A existência de fluxos de dados de sistema de ficheiros NTFS poderá provocar um **ficheiro aberto – aviso de segurança** prompt a apresentar. A instalação não irá continuar até que clique em **executar** a linha.  

 Mostra a figura 2, pode ver através dos fluxos de dados de sistema para ficheiro NTFS o **mais** comando e o [fluxos utilitário](http://technet.microsoft.com/sysinternals/bb897440.aspx).  

 ![TroubleshootingReference2](media/TroubleshootingReference2.jpg "TroubleshootingReference2")  
Figura 2. Fluxos de dados NTFS  

 **Figura 2. Fluxos de dados NTFS**  

 **Solução possível 1:** Direito\-clique no ficheiro de origem de instalação e, em seguida, clique em **propriedades**. Clique em **desbloqueio**e, em seguida, clique em **OK** para remover os fluxos de dados do sistema de ficheiros NTFS do ficheiro. Repita este processo para cada ficheiro de origem de instalação que está bloqueado pela existência de um ou mais fluxos de dados do sistema ficheiros NTFS.  

 **Solução possível 2:** Utilize o utilitário de fluxos, como REF \_Ref308173670 \\mostra h figura 2, para remover o NTFS fluxos de dados do sistema de ficheiros do ficheiro de origem de instalação. O utilitário de fluxos pode remover fluxos de dados de sistema de ficheiros NTFS de um ou mais ficheiros ou pastas em simultâneo.  

####  <a name="LostNetworkConnections"></a> Ligações de rede perdida  
 **Problema:** Uma instalação poderá falhar caso instale controladores de dispositivo ou altera as configurações de dispositivo e da rede. Estas alterações podem resultar num intervalo na conectividade de rede que faz com que a instalação falha.  

 **Possíveis soluções:** Implemente o script de ZTICacheUtil.vbs para permitir a transferência e execução para a instalação. Este script foi concebido para otimizar o anúncio para ativar a transferir e executar. A transferência utilizará o serviço de transferência inteligente em segundo plano \(BITS\) se o ponto de distribuição do Configuration Manager é Web\-baseadas em Distributed Authoring e controlo de versões e BITS ativado. Ao mesmo tempo, modifica o Configuration Manager para executar o script de ZTICache.vbs em primeiro lugar, assegurando que o programa não eliminar o próprio durante o processo de implementação.  

####  <a name="MicrosoftOfficeSystem"></a> Sistema Microsoft Office 2007  
 **Problema:** Durante a implementação do sistema do Office 2007 e, incluindo uma correção do Windows Installer \(\\<ServerName>\SMS_<SITECODE>\HOTFIX\<KB\) ficheiro, a instalação poderá falhar com o código de erro 30029.  

 Investigação adicional no ZTIApplications.log mostra as seguintes mensagens:  

-   ```  
    About to run command: \\Server\Deployment$\Tools\X86\bddrun.exe \\Server\Share\Microsoft\Office\2007\Professional\setup.exe /adminfile \\Server\Share\Microsoft\Office\2007\Professional\file.msp  
    ```  

-   ```  
    ZTI Heartbeat: command has been running for 12 minutes (process ID 1600) Return code from command = 30029  
    ```  

-   ```  
    Application Microsoft Office 2007 Professional returned an unexpected return code: 30029  
    ```  

 **Solução possível 1:** Altere a localização do ficheiro \\<ServerName>\SMS_<SITECODE>\HOTFIX\<KB para o diretório de atualizações e, em seguida, execute setup.exe sem especificar o  **\/adminfile** opção. Para obter mais informações sobre a implementação de atualizações durante a instalação, consulte [implementação do sistema do Office 2007](http://technet.microsoft.com/library/cc303395\(v=Office.12\).aspx).  

 **Solução possível 2:** Certifique-se de que o ficheiro \\<ServerName>\SMS_<SITECODE>\HOTFIX\<KB não tem o **suprimir modal** caixa de verificação selecionada. Para obter mais informações sobre como configurar esta definição, consulte [descrição geral da implementação de sistema Office 2007](http://technet.microsoft.com/library/bb490141.aspx).  

### <a name="autologon"></a>AutoLogon  
 Reveja os problemas e soluções para problemas de início de sessão automático:  

-   Interrupção da LTI e Zero Touch instalação \(ZTI\) processos de implementação devido a faixas de segurança de início de sessão, tal como descrito no [faixas de segurança de início de sessão](#LogonSecutiryBanners)  

-   Interrupção da implementação LTI e ZTI processa devido a pedidos de credenciais de utilizador conforme descrito em [pedidas as credenciais de utilizador](#PromtedforUserCredentials)  

####  <a name="LogonSecutiryBanners"></a> Faixas de segurança de início de sessão  
 **Problema:** MDT sequências de tarefas são processadas durante uma sessão interativa de utilizador, que requer que o computador de destino ser autorizado a iniciar sessão automaticamente utilizando uma conta administrativa especificada. Se um objeto de política de grupo \(GPO\) está no local que impõe uma faixa de segurança de início de sessão, este início de sessão automático não será permitido para continuar, porque a faixa de segurança forem o processo de início de sessão enquanto aguarda a um utilizador aceitar a política declarada.  

 **Possíveis soluções:** Certifique-se de que o GPO é aplicado às unidades organizacionais específicas \(UOs\) e não incluídos no domínio predefinido GPO. Ao adicionar computadores ao domínio, especifique se ser adicionado a uma UO que não é afetada por um GPO que impõe uma faixa de segurança de início de sessão. No Editor de sequência de tarefas, como um dos passos de sequência de tarefas último incluem um script que relocates a conta de computador para a UO pretendida.  

> [!NOTE]
>  Se está a reutilizar existente serviços de domínio de Active Directory® \(do AD DS\) contas, certifique-se de que, antes de implementar no computador de destino tem relocalizada conta do computador de destino a uma UO que não é afetada pelo GPO que impõe a faixa de início de sessão de segurança.  

####  <a name="PromtedforUserCredentials"></a> Pedido de credenciais de utilizador  
 **Problema:** Criar uma imagem de um computador que foi associado ao domínio. Ao implementar a nova imagem para um computador de destino, a processo de implementação forem, porque automática\-início de sessão não ocorre e é pedido ao utilizador para introduzir as credenciais adequadas. O processo de implementação retoma quando são fornecidas as credenciais e o utilizador tiver sessão iniciado.  

 **Possíveis soluções:** Ao capturar imagens, o computador de origem não deve ser associado a um domínio. Se o computador foi associado a um domínio, associe o computador a um grupo de trabalho, re\-capturar a imagem e a tentativa de implementação para um computador de destino para determinar se o problema está resolvido.  

### <a name="bios"></a>BIOS  
 **Problema:** Ao implementar um computador de destino que está equipado com technology da Intel vPro, a implementação pode terminar com um erro de paragem. Apesar de todos os controladores atualizados tem sido incluídos como saída\-de\-controladores no Deployment Workbench, o computador de destino não for iniciada.  

 Possíveis soluções: Reveja as definições na entrada básico o computador de destino\/sistema de saída \(BIOS\) para determinar se o modo de Serial Advanced Technology Attachment predefinido está configurado como avançadas a Interface de controlador anfitrião \( AHCI\). Infelizmente, determinados sistemas operativos do Windows não suportam AHCI por predefinição.  

### <a name="database-problems"></a>Problemas de base de dados  
 Base de dados de revisão\-relacionado com problemas e soluções:  

-   Erros gerados como resultado de incorretamente configurado firewalls no servidor de base de dados, conforme descrito em [bloqueado pedidos de Browser do SQL Server](#BlockedSQLServerBrowserRequests)  

-   Erros gerados como resultado quebradas ligações com o servidor de base de dados, conforme descrito em [ligações de Pipe nomeado](#NamedPipeConnections)  

####  <a name="BlockedSQLServerBrowserRequests"></a> Pedidos de Browser do servidor SQL bloqueado  
 **Problema:** Durante o processo de implementação do MDT, podem ser obtidas informações Microsoft SQL Server® bases de dados. No entanto, podem também ser gerados erros relacionados com uma firewall incorretamente configurada no servidor de base de dados.  

 **Possíveis soluções:** A Firewall do Windows no Windows Server ajuda a impedir o acesso não autorizado aos recursos de computador. No entanto, se a firewall está configurada incorretamente, as tentativas para ligar a uma instância do SQL Server podem estar bloqueadas. Para aceder a uma instância do SQL Server que está atrás da firewall, configure a firewall no computador que está a executar o SQL Server. Para obter mais informações sobre como configurar portas de firewall para SQL Server, consulte o artigo Microsoft Support [como abrir a porta de firewall para SQL Server no Windows Server 2008?](http://support.microsoft.com/kb/968872)  

####  <a name="NamedPipeConnections"></a> Ligações de Pipe nomeado  
 **Problema:** Durante o processo de implementação do MDT, é podem obter as informações de bases de dados do SQL Server. No entanto, podem também ser gerados erros relacionados com ligações quebradas do SQL Server. Estes podem ser causados por não ativar ligações de pipe nomeado no Microsoft SQL Server.  

 **Possíveis soluções:** Para resolver estes problemas, ative os pipes nomeados no SQL Server. Além disso, especifique o **SQLShare** propriedade, o que é necessário quando efetuar uma nova ligação para uma base de dados externo a utilizar pipes nomeados. Ao utilizar pipes nomeados, utilize a segurança integrada para efetuar a ligação à base de dados. No caso de implementações LTI, a conta de utilizador que especificou, faz com que a ligação à base de dados. Para implementações ZTI que utilizam o Gestor de configuração, a conta de acesso de rede liga-se à base de dados. Uma vez do Windows PE não tem nenhum contexto de segurança por predefinição, tem de se uma ligação de rede para o servidor de base de dados para estabelecer um contexto de segurança para o utilizador que será possível efetuar a ligação.  

 Partilha de rede que o **SQLShare** propriedade especifica fornece um meio para estabelecer ligação ao servidor para obter um contexto de segurança adequada. Tem de ter acesso de leitura à partilha. Quando a ligação é efetuada, em seguida, pode estabelecer a ligação de pipe nomeado para a base de dados. O **SQLShare** propriedade não é necessária e não deve ser utilizada ao efetuar uma TCP\/ligação IP à base de dados.  

 Ative as ligações de pipe nomeado, efetuando as seguintes tarefas com base na versão do SQL Server estiver a utilizar:  

-   Ativar denominado ligações de pipe para o SQL Server 2008 R2, conforme descrito em [ativar ligações de Pipe nomeado no SQL Server 2008 R2](#EnableNamedPipeConnectionsinSQLServer).  

-   Ativar denominado ligações de pipe para o SQL Server 2005, conforme descrito em [ativar ligações de Pipe nomeado no SQL Server 2005](#EnableNamedPipeConnectionsinSQL).  

#####  <a name="EnableNamedPipeConnectionsinSQLServer"></a> Ativar as ligações de Pipe nomeado no SQL Server 2008 R2  
 Para ativar as ligações de pipe nomeado no SQL Server 2008 R2, execute os seguintes passos:  

1.  No computador com o SQL Server 2008 R2 que aloja a base de dados a ser consultado, clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft SQL Server 2008 R2**e, em seguida, clique em **SQL Server Management Studio**.  

2.  No **Microsoft SQL Server Management Studio** na consola o **Object Explorer,** direita\-clique ***sql\_servidor\_nome***e, em seguida, clique em **propriedades** \(onde *sql\_servidor\_nome* é o nome do computador com o SQL Server seja configurado\).  

3.  As propriedades do servidor \- ***sql\_servidor\_nome*** é apresentada a caixa de diálogo.  

4.  No **propriedades do servidor** \- ***sql\_servidor\_nome*** caixa de diálogo **selecionar uma página**, clique em  **Ligações**.  

5.  No **ligações** página, certifique-se a **permitir ligações remotas a este servidor** está selecionada a caixa de verificação e, em seguida, clique em **OK**.  

6.  Feche a consola do Microsoft SQL Server Management Studio.  

7.  No computador com o SQL Server 2008 R2 que aloja a base de dados a ser consultado, clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft SQL Server 2008 R2**, aponte para **ferramentas de configuração**e, em seguida, clique em **Gestor de configuração do SQL Server**.  

8.  No **Gestor de configuração do SQL Server** consola, aceda ao Gestor de configuração do servidor SQL \(Local\) \/ configuração de rede do SQL Server \/ protocolos para  *SQL Server\_instância* \(onde *sql\_instância* nome de instância do SQL Server seja configurado\).  

9. No painel de detalhes, com o botão direito\-clique **Pipes nomeados**e, em seguida, clique em **ativar**.  

     A caixa de diálogo de aviso é apresentado com a indicação de que as alterações serão guardadas, mas não entrará em vigor até que o serviço está parado e reiniciado.  

10. No **aviso** caixa de diálogo, clique em **OK**.  

11. No **Gestor de configuração do SQL Server** consola, aceda ao Gestor de configuração do servidor SQL \(Local\) \/ serviços do SQL Server.  

12. No painel de detalhes, com o botão direito\-clique **do SQL Server*\(sql\_instância\)*** e, em seguida, clique em **reiniciar** \(onde *sql\_instância* nome de instância do SQL Server que configurou no passo 2\).  

     A barra de progresso do Gestor de configuração do SQL Server é apresentada que mostra o estado de reinício de serviços. Depois do serviço for reiniciado, a barra de progresso é fechado.  

13. Feche a consola do Gestor de configuração do SQL Server.  

 Para obter informações adicionais, [como ativar ligações remotas no SQL Server 2008](http://blogs.msdn.com/b/walzenbach/archive/2010/04/14/how-to-enable-remote-connections-in-sql-server-2008.aspx).  

#####  <a name="EnableNamedPipeConnectionsinSQL"></a> Ativar as ligações de Pipe nomeado no SQL Server 2005  
 Para ativar as ligações de pipe nomeado no SQL Server 2005, execute os seguintes passos:  

1.  No computador com o SQL Server 2005 que aloja a base de dados a ser consultado, clique em **iniciar**e, em seguida, aponte para **todos os programas**. Aponte para **Microsoft SQL Server 2005**, aponte para **ferramentas de configuração**e, em seguida, clique em **configuração de área de superfície do SQL Server**.  

2.  No **configuração de área de superfície do SQL Server 2005** caixa de diálogo, clique em **configuração de área de superfície para serviços e ligações**.  

3.  No **área de superfície de configuração de serviços e ligações – *servidor\_nome***  caixa de diálogo \(onde *servidor\_nome*é o nome do computador que executa o SQL Server 2005\), na **selecionar um componente e, em seguida, configurar os serviços e ligações**, aceda a MSSQLSERVER\\motor de base de dados e, em seguida, clique em  **Ligações remotas**.  

4.  Clique em **ligações locais e remotas**, clique em **utilizando ambos os TCP\/IP e pipes nomeados**e, em seguida, clique em **aplicar**.  

5.  No **área de superfície de configuração de serviços e ligações – *servidor\_nome***  caixa de diálogo \(onde *servidor\_nome*é o nome do computador que executa o SQL Server 2005\), na **selecionar um componente e, em seguida, configurar os serviços e ligações**, aceda a MSSQLSERVER\\motor de base de dados e, em seguida, clique em  **Serviço**.  

6.  Clique em **parar**.  

     O serviço MSSQLSERVER interrompe.  

7.  Clique em **Iniciar**.  

     O serviço MSSQLSERVER é iniciado.  

8.  Clique em **OK**.  

9. Feche a configuração de área de superfície do SQL Server 2005.  

 Para obter mais informações, consulte o artigo Microsoft Support [como configurar o SQL Server 2005 para permitir ligações remotas](http://support.microsoft.com/kb/914277)  

### <a name="deployment-scripts"></a>Scripts de implementação  
 Reveja o MDT\-relacionado com problemas e soluções:  

-   Pedido de credenciais de utilizador e poderá receber o erro 0x80070035 conforme descrito em [Credentials_script](#Credentials_script)  

-   É apresentada uma mensagem de erro "Wuredist.cab não encontrada" conforme descrito em [ZTIWindowsUpdate](#ZTIWindowsUpdate)  

####  <a name="Credentials_script"></a> Credenciais\_script  
 **Problema:** Durante o último início\-cópias de segurança de um computador recentemente implementado, o utilizador é-lhe pedido para fornecer credenciais de utilizador e poderá receber o erro 0x80070035, que indica que o caminho de rede não foi encontrado.  

 **Possíveis soluções:** Certifique-se de que o ficheiro WIM não inclui um MININT ou \_SMSTaskSequence pasta. Para eliminar estas pastas, primeiro utilizar o utilitário de ImageX para instalar o ficheiro WIM e, em seguida, elimine as pastas.  

> [!NOTE]
>  Se um acesso negado erro ocorre quando tenta eliminar as pastas a partir do ficheiro WIM, abra uma janela da linha de comandos, mude para a raiz da imagem contida no ficheiro WIM em seguida, execute **RD MININT** e **RD \_ SMSTaskSequence**.  

####  <a name="ZTIWindowsUpdate"></a> ZTIWindowsUpdate  
 **Problema:** Se utilizar o script de ZTIWindowsUpdate.wsf para aplicar atualizações de software durante a implementação, tenha em atenção que este script pode comunicar diretamente com o Web site do Microsoft Update para transferir e instalar os binários de agente do Windows Update necessários, procurar aplicável atualizações de software, transferir os binários para as atualizações de software aplicáveis e, em seguida, instalar os binários transferidos. Este processo requer que a sua infraestrutura de rede sejam configuradas para permitir que o computador de destino obter acesso ao Web site do Microsoft Update.  

 Se a partilha de implementação não contém os ficheiros de instalação do agente do Windows Update e o computador de destino não tem acesso à Internet, é comunicado o erro "wuredist.cab não encontrada" nos ficheiros de ZTIWindowsUpdate.log e BDD.log.  

 **Possíveis soluções:** Siga os passos descritos na secção, "ZTIWindowsUpdate.wsf" no documento MDT *Toolkit referência*.  

### <a name="deployment-shares"></a>Partilhas de implementação  
 Reveja e soluções de problemas relacionados com partilha de implementação:  

-   Atualizar WIM ficheiros falha ao atualizar uma partilha de implementação, conforme descrito em [falha para ficheiros de atualização de WIM](#FailuretoUpdateWIMFiles).  

####  <a name="FailuretoUpdateWIMFiles"></a> Falha ao atualizar ficheiros WIM  
 Num ambiente "simples":  

-   Normalmente, seleciona MDT WIMGAPI. DLL de c:\\Windows\\system32 \(sempre no caminho\). A versão deste WIMGAPI. DLL tem de corresponder à versão \(criar\) do sistema operativo.  

-   Num 64\-bit de sistema operativo, MDT utiliza sempre o x64 WIMGAPI. Ficheiro da DLL; apenas se o ficheiro deve ser o caminho do sistema. No 32\-bit de sistema operativo, MDT utiliza sempre o x86 WIMGAPI. Ficheiro da DLL; apenas se o ficheiro deve ser o caminho do sistema. \(Outros produtos, tal como o Configuration Manager, utilizam a 32\-versão de bits do WIMGAPI. DLL, mesmo num 64\-sistema operativo de bits, mas gerir e instalar essa versão.\)  

 **Problema:** Quando tentar atualizar uma partilha de implementação, o utilizador será informado que a montagem de um ou mais ficheiros. wim não teve êxito.  

 **Possíveis soluções:** Abra uma janela de linha de comandos e execute **onde WIMGAPI. DLL**. A entrada primeiro na lista \(primeira localização encontrada ao procurar o caminho\), certifique-se de que o **versão** propriedade corresponde a compilação do Windows Assessment and Deployment Kit \(Windows ADK\) que está instalada. Certifique-se também de que a propriedade corresponde ao número de compilação do sistema operativo.  

### <a name="the-windows-deployment-wizard"></a>O Assistente de implementação do Windows  
 Reveja e soluções de problemas relacionados com o Assistente de implementação do Windows:  

-   Páginas do Assistente de implementação do Windows são apresentadas, mesmo quando LTI está configurado para ignorar as páginas do assistente, conforme descrito em [assistente páginas são ignorados](#WizardPagesareNotSkipped).  

####  <a name="WizardPagesareNotSkipped"></a> Páginas do assistente não são ignoradas  
 **Problema:** É apresentada uma página de assistente, apesar do ficheiro de base de dados do MDT ou CustomSettings.ini especificar que o assistente deve ser ignorado.  

 **Possíveis soluções:** Para ignorar corretamente uma página do assistente, inclua todas as propriedades que teriam de ser especificadas nessa página do assistente apropriado no ficheiro de base de dados do MDT ou CustomSettings.ini juntamente com os valores adequados. Se uma propriedade estiver configurada incorretamente para uma página do assistente ignorado, nessa página será apresentada. Para obter mais informações sobre as propriedades são necessárias para se certificar de que uma página do assistente é ignorada, consulte a secção "Fornecer propriedades para ignorada implementação páginas do assistente", no documento MDT *Toolkit referência*.  

### <a name="disks-and-partitioning"></a>Discos e criação de partições  
 Reveja e soluções de problemas de criação de partições de disco:  

-   A encriptação de unidade BitLocker® emite conforme descrito em [encriptação de unidade BitLocker](#BitLockerDriveEncryption)  

-   Erros de criação de partições, conforme descrito em erros de criação de partições de disco do disco  

-   As falhas durante causados por discos lógicos ou dinâmicos, conforme descrito em cenários de implementação de computador atualizar [suporte para Logical e os discos dinâmicos](#SupportforLoogicalandDynamicDisks)  

####  <a name="BitLockerDriveEncryption"></a> Encriptação de unidade BitLocker  
 A implementação de BitLocker requer uma configuração específica para a implementação correta. Os seguintes problemas potenciais podem estar relacionado com a configuração do computador de destino:  

-   Nas implementações ZTI e UDI, o Script de ZTIBde.wsf falhar com o erro "não é possível abrir a chave de registo ' HKEY\_atual\_utilizador\\painel de controlo\\internacional\\LocaleName' para leitura", como descrito no [ZTIBde.wsf Script falhar com o erro "Não é possível abrir a chave de registo 'HKEY_CURRENT_USER\Control Panel\International\LocaleName' para leitura"](#ZTIBde.wsf).  

-   Dispositivos USB, unidades de CD, unidades de DVD ou outros dispositivos de suporte de dados amovível no computador de destino que são apresentados como vários letras de unidade, conforme descrito em [dispositivos são apresentados como vários letras de unidade](#DevicesAppearasMultipleDriveLetters)  

-   Reduzir a unidade C no computador de destino para fornecer suficiente espaço em disco não alocado conforme descrito em [problemas com a redução dos discos](#ProblemswithShrinkingDisks)  

#####  <a name="ZTIBde.wsf"></a> Script de ZTIBde.wsf falha com o erro "não é possível abrir a chave de registo ' HKEY\_atual\_utilizador\\painel de controlo\\internacional\\LocaleName' para leitura"  
 **Problema:** Ao tentar implementar o BitLocker no computador de destino no ZTI ou UDI, o script de ZTIBde.wsf falha com o erro "não é possível abrir a chave de registo ' HKEY\_atual\_utilizador\\painel de controlo\\internacional\\LocaleName' para leitura. "  

 **Possíveis soluções:** Especificar a região no **UILanguage** propriedade. No ZTI e UDI, o script de ZTIBde.wsf executa no controlo de sistema, para que um perfil de utilizador completo não está carregado. Quando o script de ZTIBde.wsf tenta ler as informações de região não se encontra no registo, porque o registo \(perfil de utilizador\) não é totalmente carregado. Como solução, especifique a região no **UILanguage** propriedade.  

#####  <a name="DevicesAppearasMultipleDriveLetters"></a> Os dispositivos apresentados como letras de unidade de vários  
 **Problema:** Alguns dispositivos podem aparecer como vários letras de unidade lógica, dependendo do modo como são particionadas. Em alguns casos, podem emular um 1.44\-megabyte \(MB\) unidade de disco de disquetes e uma unidade de armazenamento de memória. Por conseguinte, o Windows pode atribuir as mesmo dispositivo letras de unidade A e B disquete emulação e F para a unidade de armazenamento de memória. Por predefinição, os scripts de MDT utilizam a letra de unidade mais baixa \(neste exemplo, um\).  

 **Possíveis soluções:** Substituir a definição predefinida no **especifique os detalhes de recuperação do BitLocker** página no Assistente de implementação do Windows. A página de resumo do Assistente de implementação do Windows apresenta um aviso a informar o utilizador não foi seleccionada que letra de unidade para armazenar as informações de recuperação do BitLocker. Além disso, os ficheiros BDD.log e ZTIBDE.log registam os dispositivos de suporte de dados amovível detetados e qual era o dispositivo foi selecionado para armazenar as informações de recuperação do BitLocker.  

#####  <a name="ProblemswithShrinkingDisks"></a> Problemas com a redução dos discos  
 **Problema:** Não suficiente espaço em disco não atribuído existe no computador de destino para ativar o BitLocker. Para implementar o BitLocker num computador de destino, pelo menos, 2 gigabytes \(GB\) do disco não atribuído espaço é necessário para criar o volume de sistema. O *volume de sistema* é o volume que contém o hardware\-ficheiros específicos, necessários para carregar o Windows após a BIOS tem arrancado o computador.  

 **Solução possível 1:** Em computadores existentes, utilize a ferramenta de Diskpart para reduzir a unidade C para que o volume de sistema pode ser criado. Em alguns casos, a ferramenta Diskpart poderá não conseguir encolher unidade C suficientemente para fornecer 2 GB de espaço em disco não atribuído, possivelmente devido a espaço de disco fragmentados dentro da unidade C.  

 Uma solução possíveis para este problema é desfragmentar a unidade C. Para tal, execute os seguintes passos:  

1.  Execute o utilitário Diskpart **diminuir querymax** comandos para identificar a quantidade máxima de espaço em disco que pode ser não alocado.  

2.  Se o valor devolvido no passo 1 é inferior a 2 GB, limpar unidade C de quaisquer ficheiros desnecessários e, em seguida, desfragmentá-lo.  

3.  Execute o utilitário Diskpart **diminuir querymax** comando novamente para verificar se mais do que 2 GB de espaço em disco não alocado.  

4.  Se o valor obtido no passo 3 ainda inferior a 2 GB, execute uma das seguintes tarefas:  

    -   Desfragmentar a unidade C várias vezes para se certificar de que está totalmente otimizado.  

    -   Criar cópias de segurança de dados na unidade C, elimine a partição existente, crie uma nova partição e, em seguida, restaurar os dados para a nova partição.  

 **Solução possível 2:** O script de ZTIBDE.wsf é executado a ferramenta de preparação de disco \(bdehdcfg.exe\) e configura o sistema partição tamanho do volume para 2 GB por predefinição. Pode personalizar o script de ZTIBDE.wsf para alterar a predefinição, se necessário. No entanto, a modificar os scripts de MDT não é recomendada.  

####  <a name="SupportforLoogicalandDynamicDisks"></a> Suporte para discos lógicos e dinâmicos  
 **Problema:** Quando efetuar um cenário de implementação de atualizar o computador, o processo de implementação poderá falhar quando implementar num computador de destino que está a utilizar as unidades lógicas ou discos dinâmicos.  

 **Possíveis soluções:** MDT não suporta a implementação de sistemas operativos para as unidades lógicas ou discos dinâmicos.  

### <a name="domain-join"></a>Domain Join  
 **Problema:** Durante a implementação, utilize o Assistente de implementação do Windows para fornecer todas as informações necessárias para o computador de destino, incluindo credenciais, informações de associação de domínio e configuração de IP estático. Quando a conclusão da configuração, pode ver que o sistema não está associada ao domínio e ainda está a ser um grupo de trabalho.  

 **Possíveis soluções:** Uma implementação LTI do MDT configura as informações de IP estáticas, depois do sistema operativo está a funcionar. Se o computador de destino está localizado num segmento de rede que não tenha o Dynamic Host Configuration Protocol \(DHCP\), uma associação de domínio automatizada especificada no Unattend.xml irão falhar quando não existem DHCP está presente.  

 Configure Unattend.xml para aderir a um grupo de trabalho. Em seguida, utilize o incorporado\-no **recuperar do domínio** passo de sequência de tarefas para adicionar um passo da sequência de tarefas para aderir ao domínio, após o IP estático.  

### <a name="driver-installation"></a>Instalação de controlador  
 Para garantir a melhor experiência de utilizador possível, instalação de dispositivos de hardware e controladores de software deve ser executada como perfeitamente possível, com pouca ou nenhuma intervenção do utilizador. A Microsoft fornece ferramentas e diretrizes para ajudar a criar pacotes de instalação que atingir este objetivo. Para obter informações gerais sobre a instalação de controladores, consulte [dispositivo e a instalação de controlador](http://www.microsoft.com/whdc/driver/install/default.mspx).  

 Reveja e soluções de problemas de instalação relacionados com controladores de dispositivo:  

-   Problemas que ocorrem quando utilizar controladores de armazenamento em massa de $ $OEM com o MDT conforme descrito em combinam $OEM controladores de armazenamento de massa $ com lógica de armazenamento em massa de MDT  

-   Resolução de problemas de instalação de controladores de dispositivo utilizando o SetupAPI.log conforme descrito em [resolver problemas de instalação do dispositivo com SetupAPI.log](#TroubleshootDeviceInstallationwithSetupAPI.log)  

####  <a name="TroubleshootDeviceInstallationwithSetupAPI.log"></a> Resolver problemas de instalação do dispositivo com SetupAPI.log  
 O documento técnico [resolução de problemas de instalação do dispositivo com o ficheiro de registo SetupAPI](http://msdn.microsoft.com/windows/hardware/gg463393.aspx) fornece informações sobre a depuração de instalação do Windows no dispositivo. Especificamente, o documento fornece orientações para programadores de controlador e testers interpretar o ficheiro de registo SetupAPI.  

 Um dos ficheiros de registo mais úteis para fins de depuração é o ficheiro de SetupAPI.log. Este simples\-ficheiro de texto mantém as informações que SetupAPI registos sobre a instalação do dispositivo, instalação do pacote de serviço e da instalação da atualização. Especificamente, o ficheiro mantém um registo de alterações e controladores de dispositivos, bem como as alterações principais do sistema a partir da instalação do Windows mais recente. Este documento centra-se utilizando o ficheiro de registo SetupAPI para resolver problemas de instalação do dispositivo; não descreve as secções do ficheiro de registo que estão associados com service pack e instalações de atualizações.  

### <a name="new-computer-deployments"></a>Novas implementações de computador  
 Reveja os problemas e soluções para cenários de implementação do novo computador:  

-   Problemas de iniciar o processo de implementação utilizando pré\-ambiente de execução de arranque \(PXE\) arranque conforme descrito em [arranque PXE](#PXEBoot)  

####  <a name="PXEBoot"></a> PXE Boot  
 No brief, o protocolo PXE funciona da seguinte forma: O computador cliente inicia o protocolo por difundir um pacote DHCP detetar que contém uma extensão que identifica o pedido como proveniente de um computador cliente que implementa o protocolo PXE. Partindo do princípio de que está disponível um servidor de arranque implementar este protocolo expandido, o servidor de arranque envia uma oferta que contém o endereço IP do servidor que irá processar o cliente. O cliente utiliza o protocolo de transferência de ficheiros Trivial para transferir o ficheiro executável a partir do servidor de arranque. Por fim, o computador cliente executa o programa de arranque de configuração transferido.  

 A fase inicial deste protocolo piggybacks num subconjunto das mensagens de DHCP para permitir ao cliente detetar um servidor de arranque \(ou seja, um servidor que fornece os ficheiros executáveis para a nova configuração de computador\). O computador cliente pode utilizar a oportunidade para obter um endereço IP \(que é o comportamento esperado\) mas não é necessária para o fazer.  

 A segunda fase deste protocolo ocorre entre o computador cliente e um servidor de arranque e utiliza o formato de mensagem DHCP como um formato conveniente para comunicação. Esta segunda fase caso contrário, não está relacionado com os serviços DHCP padrão. As páginas de alguns seguintes descrevem o passo\-por\-passo do processo durante a inicialização de computador de cliente PXE.  

 Para mais informações sobre resolução de problemas de PXE de arranque\-problemas relacionados nos serviços de implementação do Windows em execução no modo legado ou Mixed, consulte o artigo da Microsoft Support [descrição do PXE a interação entre cliente PXE, o DHCP e o servidor RIS ](http://support.microsoft.com/kb/244036).  

 Reveja as seguintes soluções para problemas de arranque PXE:  

-   Desativar o registo do Windows PE para SetupAPI.log conforme descrito em [desativar o Windows PE registo nos serviços de implementação do Windows](#DisableWindowsPELogginginWindowsDeploymentServices).  

-   Certifique-se de que o DHCP está configurado corretamente conforme descrito em [Certifique-se a configuração de DHCP adequado](#EnsuretheProperDHCPConfiguration).  

-   Melhorar os tempos de resposta para atribuir endereços IP a computadores de cliente PXE, conforme descrito em [melhorar o tempo de resposta de atribuição do PXE IP endereço](#ImprovePXEIPAddressAssignmentResponseTime).  

#####  <a name="DisableWindowsPELogginginWindowsDeploymentServices"></a> Desativar o registo no Windows dos serviços de implementação do Windows PE  
 O primeiro procedimento recomendado é certificar-se de que o registo para setupapi.log foi desativado.  

#####  <a name="EnsuretheProperDHCPConfiguration"></a> Certifique-se a configuração de DHCP adequado  
 Consoante os modelos de router em utilização, a configuração de router específico de reencaminhamento de difusão de DHCP pode ser suportada para uma sub-rede \(ou interface de router\) ou um anfitrião específico. Se os servidores DHCP e o computador a executar o serviços de implementação do Windows são computadores separados, certifique-se de que os routers que reencaminham difusões DHCP foram concebidos para que os servidores de DHCP e os serviços de implementação do Windows recebem difusões cliente; caso contrário, o computador cliente não receber uma resposta para o pedido de arranque remoto.  

 Existe um router entre o computador cliente e o servidor de instalação remota que não está a permitir que o DHCP\-baseada em pedidos ou respostas através de? Quando o computador de cliente de serviços de implementação do Windows e o servidor de serviços de implementação do Windows em sub-redes separadas, configure o router entre os dois sistemas para reencaminhar os pacotes DHCP para o servidor de serviços de implementação do Windows. Esta disposição é necessária, porque os computadores de cliente de serviços de implementação do Windows detetar um servidor de serviços de implementação do Windows através da utilização de uma mensagem de difusão de DHCP. Sem o DHCP num router de reencaminhamento conjunto de cópias de segurança, difusões DHCP dos computadores cliente não conseguirem contactar o servidor de serviços de implementação do Windows. Este processo de reencaminhamento de DHCP, por vezes, é referido como *DHCP Proxy* ou *endereço de programa auxiliar de IP* na como de configuração de router. Consulte as instruções de router para obter mais informações sobre como configurar o reencaminhamento de DHCP num router específico.  

#####  <a name="ImprovePXEIPAddressAssignmentResponseTime"></a> Melhorar o tempo de resposta de atribuição de endereço IP de PXE  
 Verifique os seguintes elementos, se estiver a demorar muito tempo \(15 – 20 segundos\) para o computador de cliente PXE obter um endereço IP:  

-   São o adaptador de rede no computador de destino e router ou comutador definido para a mesma velocidade \(automática, duplex, completo e outros\)  

-   É o endereço IP para o servidor de serviços de implementação do Windows no ficheiro de programa auxiliar de IP no router BGP através do qual o estabelecimento da ligação? Se a lista de endereços IP no ficheiro de programa auxiliar de IP for longa, pode mover o endereço para o servidor de serviços de implementação do Windows perto da parte superior  

### <a name="restarting-the-deployment-process"></a>Reiniciar o processo de implementação  
 **Problema:** Ao testar e resolução de problemas de uma sequência de tarefas novos ou modificados, poderá ter de reiniciar o computador de destino para que o processo de implementação pode começar a partir do início. Resultados inesperados podem ocorrer porque o MDT mantém um registo dos respetivos progresso ao escrever dados para o disco rígido; qualquer reiniciar o computador de destino tem MDT retomar onde foi deixada no reinício anterior.  

 **Possíveis soluções:** Para permitir que o processo de implementação reiniciar a partir do início, elimine a unidade c:\\MININT e c:\\\_SMSTaskSequence pastas antes de reiniciar o computador de destino.  

### <a name="sysprep"></a>Sysprep  
 Reveja o Sysprep\-relacionado com problemas e soluções:  

-   O computador de destino é não volte a aparecer na corretos AD DS UO conforme descrito em [o computador conta é na UO errado](#ComputerAccountisintheWrongOU).  

####  <a name="ComputerAccountisintheWrongOU"></a> A conta de computador está na UO errado  
 **Problema:** O computador de destino está corretamente associado ao domínio, mas a conta de computador está na UO errado.  

 **Solução possível 1:** Se uma conta pré-configurada\-existe para o computador de destino, a conta permanecerá no respetivo UO original. Para mover a conta para a UO especificada, adicione um passo de sequência de tarefas que utiliza uma ferramenta de automatização, tais como um Microsoft Visual Basic® Scripting Edition, mover a conta.  

 **Solução possível 2:** Certifique-se de que a UO especificada está no formato correto e se existe. O formato de UO correto deve ser `OU=Reception,OU=NYC,DC=Woodgrovebank,DC=com`.  

### <a name="configuration-manager"></a>Configuration Manager  
 **Problema:** A mensagem de erro mostrada na REF \_Ref308174600 \\h a figura 3 é apresentada ao tentar criar um serviço de PXE do Configuration Manager ponto utilizando o **criar Self-\-assinado certificado PXE** opção.  

 ![TroubleshootingReference3](media/TroubleshootingReference3.jpg "TroubleshootingReference3")  
Figura SEQ Figure \\ \* ARABIC 3. Erro de ponto de serviço PXE  

 **Figura SEQ Figure \\ \* ARABIC 3. Erro de ponto de serviço PXE**  

 **Possíveis soluções:** Se um ponto de serviço PXE existia anteriormente no servidor que está a configurar, o ponto de serviço PXE não pode ter eliminado o self\-criado certificados quando a respetiva desinstalação. Eliminar a pasta de certificados PXE do c:\\documentos e definições\\*utilizador\_nome*\\dados da aplicação\\Microsoft\\Crypto\\RSA, onde *utilizador\_nome* é o nome do utilizador efetuar a configuração atual ou a quem efetuou a configuração anterior. O Assistente de função do novo Site na consola do Configuration Manager deve ser concluída com êxito quando tiver eliminado a pasta.  

### <a name="task-sequences"></a>Sequências de tarefas  
 Reveja e soluções de problemas relacionados com sequência de tarefas:  

-   Sequência de tarefas não for concluída com êxito ou tem um comportamento imprevisível conforme descrito em [a tarefa sequência Does não concluir com êxito](#TaskSequenceDoesNotFinishSuccessfully).  

-   Fabricante de equipamento original \(OEM\) sequências de tarefas no LTI estão listadas nas imagens de arranque com a arquitetura de processador oposta, conforme descrito em [o OEM tarefas sequência incorretamente aparece para uma imagem de arranque criadas para um Arquitetura de processador diferente](#OEMTaskSequenceIncorrectlyAppearsforBootImage).  

-   O Assistente de implementação do Windows apresenta a mensagem de erro "Item de sequência de tarefas incorreto \(GUID inválido de SO\)" conforme descrito em [mensagem incorreto Item de sequência de tarefas (GUID inválido do SO) no Assistente de implementação do Windows](#BadTaskSequenceItem).  

-   Ao configurar um nome de ligação de rede, a mensagem ". Introduza um nome válido para o adaptador de rede" é apresentado conforme descrito em [aplicar definições de rede](#ApplyNetworkSettings).  

-   Problemas que possam ocorrer em resultado de uma configuração incorreta de continuar com as definições de configuração de erro para obter os passos de sequência de tarefas, conforme descrito em [utilize continuar com o erro](#UseContinueonError).  

####  <a name="TaskSequenceDoesNotFinishSuccessfully"></a> A sequência de tarefas não for concluída com êxito  
 **Problema:** Sequência de tarefas não pode ser concluída com êxito ou tem um comportamento imprevisível.  

 **Possíveis soluções:** O **instalar sistema operativo** passo de sequência de tarefas \(para LTI\) ou **aplicar imagem do sistema operativo** passo de sequência de tarefas \(para UDI e ZTI\)tiverem sido modificadas após a criação do passo de sequência de tarefas pode originar resultados imprevisíveis. Por exemplo, se tiver sido criada uma sequência de tarefas para implementar um 32\-bit de imagem do Windows 8.1 e, em seguida, posterior a **instalar sistema operativo** passo de sequência de tarefas ou **aplicar imagem do sistema operativo** tarefas passo de sequência foi alterado para fazer referência a um 64\-bits do Windows 8.1 imagem, a sequência de tarefas poderá não ser executado com êxito.  

 Recomenda-se que é criada uma nova sequência de tarefas para implementar uma imagem de sistema operativo diferente.  

####  <a name="OEMTaskSequenceIncorrectlyAppearsforBootImage"></a> A sequência de tarefas OEM é apresentada incorretamente uma imagem de arranque criada para uma arquitetura de processador diferente  
 **Problema:** Uma sequência de tarefas com base num modelo de sequência de tarefas LTI OEM está a ser mostrada cópias de segurança para uma imagem de arranque com uma arquitetura de processador diferente. Por exemplo, uma OEM sequência de tarefas que implementa um 64\-bits operação sistema está a ser mostrada no 32\-imagem de arranque de bits.  

 **Possíveis soluções:** Este comportamento está previsto como as sequências de tarefas do OEM LTI não são consideradas como sendo "plataforma\-específico" será sempre listado, independentemente da arquitetura do processador da imagem de arranque.  

####  <a name="BadTaskSequenceItem"></a> Item de sequência de tarefas incorreto \(GUID inválido de SO\) mensagem no Assistente de implementação do Windows  
 **Problema:** Ao executar o Assistente de implementação do Windows, o assistente apresenta a mensagem de erro "Item de sequência de tarefas incorreto \(GUID inválido de SO\)." O sistema operativo está listado no ficheiro OperatingSystem.xml; No entanto, o sistema operativo não é apresentado no Deployment Workbench.  

 **Possíveis soluções:** A origem original do sistema operativo tem dois ou mais ficheiros WIM associados. Um SKU que está associado uma sequência de tarefas é eliminado; No entanto, outros SKUs para a origem do sistema operativo ainda existem. Quando a sequência de tarefas que faça referência a SKU eliminado está selecionada no **Selecione uma sequência de tarefas para executar neste computador** página do assistente no Assistente de implementação do Windows, a mensagem de erro "Item de sequência de tarefas incorreto \( GUID de SO inválido\)"é apresentada depois de clicar em **seguinte** na página do assistente.  

 Para resolver este problema, efetue uma das seguintes tarefas:  

-   Remova todos os SKUs da origem de sistema operativo. O Assistente de implementação do Windows comporta-se normalmente e não é apresentada a mensagem de erro.  

-   Altere a sequência de tarefas a utilizar uma imagem de sistema operativo diferente.  

####  <a name="ApplyNetworkSettings"></a> Aplicar definições de rede  
 **Problema:** Quando configurar o nome da ligação de rede no Deployment Workbench, um erro de validação irá pedir-lhe com a mensagem, ". Introduza um nome válido para o adaptador de rede."  

 **Possíveis soluções:** Remova o nome de ligação especificada quaisquer espaços e carateres inválidos.  

####  <a name="UseContinueonError"></a> Utilize continuar com o erro  
 Se uma sequência de tarefas do MDT está configurada para não continuar com o erro e a sequência de tarefas devolve um erro, todas as sequências de tarefas restantes nesse grupo de sequência de tarefas são ignoradas. No entanto, os grupos de sequência de tarefas restantes são processados. Tenha em consideração o seguinte:  

 Foram criados dois grupos de sequência de tarefas e o grupo contém mais do que um passo de sequência de tarefas:  

-   Grupo A  

    -   Passo A  

    -   Passo B  

-   Grupo B  

    -   Passo A  

    -   Passo B  

 Se um grupo\\passo uma está configurado para não continuar com o erro, em seguida, o grupo A\\passo B não será processada. No entanto, todos os passos de sequência de tarefas no grupo B serão processados.  

### <a name="the-user-state-migration-tool"></a>A ferramenta de migração de estado do utilizador  
 Reveja o USMT\-relacionado com problemas e soluções:  

-   Atalhos que apontam para documentos armazenados em pastas partilhadas na rede podem não ser restaurados corretamente conforme descrito em [atalhos de ambiente de trabalho em falta](#MissingDesktopShortcuts).  

####  <a name="MissingDesktopShortcuts"></a> Atalhos de ambiente de trabalho em falta  
 **Problema:** Ao utilizar o USMT para migrar dados de utilizador, os atalhos que apontam para documentos de rede não podem ser restaurados. Os atalhos são capturados durante Scanstate; No entanto, estes são nunca restaurados para o computador de destino durante Loadstate.  

 **Possíveis soluções:** Edite o ficheiro de MigUser.xml e comente a linha seguinte:  

 Original:  

```  
<include> filter='MigXmlHelper.IgnoreIrrelevantLinks()'>  
```  

 Modificar:  

```  
<include> <!-- filter='MigXmlHelper.IgnoreIrrelevantLinks()'> -->  
```  

### <a name="windows-imaging-format-files"></a>Ficheiros de formato de processamento de imagens do Windows  
 Reveja WIM\-relacionado com problemas e soluções:  

-   Implementações LTI e ZTI falharam com erros de ficheiros WIM no ficheiro BDD.log, conforme descrito em [ficheiro WIM da danificado](#CorruptWIMFile).  

####  <a name="CorruptWIMFile"></a> Ficheiro WIM danificado  
 **Problema:** Quando implementar uma imagem, a implementação falhar com as seguintes entradas no ficheiro BDD.log:  

-   ```  
    The image \\Server\Deployment$\Operating Systems\Windows\version1.wim was not applied successfully by ImageX, rc = 2  
    ```  

-   ```  
    LTIApply COMPLETED.  Return Value = 2  
    ```  

-   ```  
    ZTI ERROR - Non-zero return code by LTIApply, rc = 2  
    ```  

 Investigar o problema ao montar o ficheiro WIM com o ImageX resultados de erros, "dados são inválidos." Investigação adicional mostra que o carimbo de data do ficheiro. wim está muitos anos antes da data atual. É possível que outro processo, tal como um detetor de vírus, foi que contém o ficheiro. wim aberta após anteriormente foi fechado na conclusão de um processo de leitura ou escrita.  

 **Possíveis soluções:** Restaure o ficheiro. wim do suporte de dados de cópia de segurança.  

### <a name="windows-pe"></a>Windows PE  
 Reveja e soluções de problemas relacionados com o Windows PE:  

-   O processo de implementação LTI ou ZTI não é iniciado devido a insuficiente RAM ou adaptadores de rede sem fios, conforme descrito em [implementação processo não foi iniciada — RAM limitada ou adaptador de rede sem fios](#LimitedRamorWirelessNetworkAdapter).  

-   O processo de implementação LTI ou ZTI não foi iniciado devido a falta de componentes do Windows PE, tal como descrito no [implementação processo não foi iniciada — componentes em falta](#MissingComponents).  

-   O processo de implementação LTI ou ZTI não é iniciado devido a controladores de dispositivo em falta ou incorretas, conforme descrito em [implementação processo não foi iniciada — em falta ou incorretos controladores](#MissingorIncorrectDrivers).  

####  <a name="LimitedRamorWirelessNetworkAdapter"></a> Processo de implementação não foi iniciado — RAM limitado ou um adaptador de rede sem fios  
 **Problema:** Quando implementar uma imagem a determinados computadores de destino, do Windows PE é iniciado, executa **wpeinit**, abre uma janela de linha de comandos, mas não inicia o processo de implementação. Resolução do problema mediante o mapeamento de unidade de rede do computador de destino indica que os controladores de placa de rede não estão carregados.  

 **Solução possível 1:** o Assistente de implementação não é iniciar, porque não há RAM suficiente. Certifique-se de que o computador de destino tem, pelo menos, 512 MB de RAM e que nenhum memória de vídeo partilhada consome mais do que 64 MB de 512 MB.  

 As versões do Windows PE, que suporta o MDT são não é possível executar num computador de destino que tem menos de 512 MB de RAM.  

 **Solução possível 2:** Não inclua os controladores sem fios na imagem do Windows PE.  

####  <a name="MissingComponents"></a> Processo de implementação não foi iniciado — em falta componentes  
 **Problema:** Quando a implementação de resolução de problemas, uma revisão do ficheiro BDD.log lista a entrada seguinte:  

```  
ERROR - Unable to create ADODB.Connection object, impossible to query SQL Server: ActiveX component can't create object (429).  
```  

 **Possíveis soluções:** Este erro poderá indicar que a imagem do Windows PE não foi criada com o MDT. Se estiver a utilizar o Configuration Manager, não utilize uma das imagens existentes do Windows PE que o Configuration Manager criou; em vez disso, crie uma imagem através do Assistente de sequência de tarefas de implementação de Microsoft de importação.  

> [!NOTE]
>  As imagens do Windows PE que o Configuration Manager cria contém componentes que suportam a criação de scripts, XML e o Windows Management Instrumentation (WMI), mas não contém componentes que suportam a objetos de dados de® do Microsoft ActiveX (ADO).  

####  <a name="MissingorIncorrectDrivers"></a> Processo de implementação não foi iniciado — controladores em falta ou incorretos  
 **Problema:** Quando implementar a determinados computadores de destino, do Windows PE é iniciado, executa **wpeinit**, abre uma janela de linha de comandos, mas não inicia o processo de implementação. Resolução de problemas mediante o mapeamento de unidade de rede do computador de destino indica que os controladores de placa de rede não estão carregados. Uma revisão do ficheiro SetupAPI.log localizado em *X*: \Windows\System32\Inf indica que o Windows PE gera erros quando está a configurar o adaptador de rede, um dos quais é, "este controlador não destinam-se nesta plataforma." Os controladores no **Out-of-Box controladores** lista ter sido injetados a imagem.  

 **Possíveis soluções:** É possível que o Windows PE é ter um conflito com outro controlador de controlador. Quando configurar as definições de imagem do Windows PE no Deployment Workbench, crie um grupo de controladores do Windows PE que contém apenas o adaptador de rede e controladores de armazenamento e, em seguida, configure a partilha de implementação a utilizar apenas o grupo de controladores Windows PE.  

## <a name="deployment-process-flow-charts"></a>Gráficos de fluxo do processo de implementação  
 Esta secção fornece dois conjuntos de gráficos de fluxo do MDT: um para implementações LTI e outro para implementações ZTI com o Configuration Manager. Cada fluxograma ilustra as tarefas em execução durante esse tipo de implementação.  

 Familiarize-se com os gráficos de fluxo do processo de implementação por:  

-   Rever as fluxogramas de processo de implementação LTI, conforme descrito em [fluxogramas de processo de implementação LTI](#LTIDeploymentProcessFlowcharts)  

-   Rever as fluxogramas de processo de implementação ZTI conforme descrito em [fluxogramas de processo de implementação ZTI](#ZTIDevelopmentProcessFlowcharts)  

###  <a name="LTIDeploymentProcessFlowcharts"></a> Fluxogramas de processo de implementação LTI  
 Gráficos de fluxo são fornecidos para as seguintes fases:  

-   Validação (figura 4)  

-   Captura de estado (figura 5 e figura 6)  

-   Preinstall (figura 7, 8 figura e figura 9)  

-   Instalar (figura 10)  

-   Postinstall (figura 11 e figura 12)  

-   Restauro de estado (figura 13, figura 14, 15 figura e figura 16)  

 ![TroubleshootingReference4](media/TroubleshootingReference4.jpg "TroubleshootingReference4")  
Figura 4. Fluxograma para a fase de validação  

 **Figura 4. Fluxograma para a fase de validação**  

 ![TroubleshootingReference5](media/TroubleshootingReference5.jpg "TroubleshootingReference5")  
Figura 5. Fluxograma para a fase de captura de estado (1 de 2)  

 **Figura 5. Fluxograma para a fase de captura de estado (1 de 2)**  

 ![TroubleshootingReference6](media/TroubleshootingReference6.jpg "TroubleshootingReference6")  
Figura 6. Fluxograma para a fase de captura de estado (2 de 2)  

 **Figura 6. Fluxograma para a fase de captura de estado (2 de 2)**  

 ![TroubleshootingReference7](media/TroubleshootingReference7.jpg "TroubleshootingReference7")  
A figura 7. Fluxograma para a fase de Preinstall (1 de 3)  

 **A figura 7. Fluxograma para a fase de Preinstall (1 de 3)**  

 ![TroubleshootingReference8](media/TroubleshootingReference8.jpg "TroubleshootingReference8")  
Figura 8. Fluxograma para a fase de Preinstall (2 de 3)  

 **Figura 8. Fluxograma para a fase de Preinstall (2 de 3)**  

 ![TroubleshootingReference9](media/TroubleshootingReference9.jpg "TroubleshootingReference9")  
Figura 9. Fluxograma para a fase de Preinstall (3 de 3)  

 **Figura 9. Fluxograma para a fase de Preinstall (3 de 3)**  

 ![TroubleshootingReference10](media/TroubleshootingReference10.jpg "TroubleshootingReference10")  
A figura 10. Fluxograma para a fase de instalação  

 **A figura 10. Fluxograma para a fase de instalação**  

 ![TroubleshootingReference11](media/TroubleshootingReference11.jpg "TroubleshootingReference11")  
Figura 11. Fluxograma para a fase de Postinstall (1 de 2)  

 **Figura 11. Fluxograma para a fase de Postinstall (1 de 2)**  

 ![TroubleshootingReference12](media/TroubleshootingReference12.jpg "TroubleshootingReference12")  
Fluxograma de figura 12 para a fase de Postinstall (2 de 2)  

 **Fluxograma de figura 12 para a fase de Postinstall (2 de 2)**  

 ![TroubleshootingReference13](media/TroubleshootingReference13.jpg "TroubleshootingReference13")  
Figura 13. Fluxograma para a fase de restauro de estado (1 de 4)  

 **Figura 13. Fluxograma para a fase de restauro de estado (1 de 4)**  

 ![TroubleshootingReference14](media/TroubleshootingReference14.jpg "TroubleshootingReference14")  
Figura 14. Fluxograma para a fase de restauro de estado (2 de 4)  

 **Figura 14. Fluxograma para a fase de restauro de estado (2 de 4)**  

 ![TroubleshootingReference15](media/TroubleshootingReference15.jpg "TroubleshootingReference15")  
Figura 15. Fluxograma para a fase de restauro de estado (3 de 4)  

 **Figura 15. Fluxograma para a fase de restauro de estado (3 de 4)**  

 ![TroubleshootingReference16](media/TroubleshootingReference16.jpg "TroubleshootingReference16")  
Figura 16. Fluxograma para a fase de restauro de estado (4 de 4)  

 **Figura 16. Fluxograma para a fase de restauro de estado (4 de 4)**  

###  <a name="ZTIDevelopmentProcessFlowcharts"></a> Fluxogramas de processo de implementação ZTI  
 Gráficos de fluxo são fornecidos para as seguintes fases de implementação de ZTI com o Configuration Manager:  

-   Inicialização (figura 17)  

-   Validação (figura 18)  

-   Captura de estado (figura 19)  

-   Preinstall (figura 20)  

-   Instalar (figura 21)  

-   Postinstall (figura 22)  

-   Restauro de estado (23 figura e figura 24)  

-   Capturar (figura 25)  

 ![TroubleshootingReference17](media/TroubleshootingReference17.jpg "TroubleshootingReference17")  
Figura 17. Fluxograma para a fase de inicialização  

 **Figura 17. Fluxograma para a fase de inicialização**  

 ![TroubleshootingReference18](media/TroubleshootingReference18.jpg "TroubleshootingReference18")  
Figura 18. Fluxograma para a fase de validação  

 **Figura 18. Fluxograma para a fase de validação**  

 ![TroubleshootingReference19](media/TroubleshootingReference19.jpg "TroubleshootingReference19")  
Figura 19. Fluxograma para a fase de captura de estado  

 **Figura 19. Fluxograma para a fase de captura de estado**  

 ![TroubleshootingReference20](media/TroubleshootingReference20.jpg "TroubleshootingReference20")  
Figura 20. Fluxograma para a fase de Preinstall  

 **Figura 20. Fluxograma para a fase de Preinstall**  

 ![TroubleshootingReference21](media/TroubleshootingReference21.jpg "TroubleshootingReference21")  
Figura 21. Fluxograma para a fase de instalação  

 **Figura 21. Fluxograma para a fase de instalação**  

 ![TroubleshootingReference22](media/TroubleshootingReference22.jpg "TroubleshootingReference22")  
Figura 22. Fluxograma para a fase de Postinstall  

 **Figura 22. Fluxograma para a fase de Postinstall**  

 ![TroubleshootingReference23](media/TroubleshootingReference23.jpg "TroubleshootingReference23")  
Figura 23. Fluxograma para a fase de restauro de estado (1 de 2)  

 **Figura 23. Fluxograma para a fase de restauro de estado (1 de 2)**  

 ![TroubleshootingReference24](media/TroubleshootingReference24.jpg "TroubleshootingReference24")  
Figura 24. Fluxograma para a fase de restauro de estado (2 de 2)  

 **Figura 24. Fluxograma para a fase de restauro de estado (2 de 2)**  

 ![TroubleshootingReference25](media/TroubleshootingReference25.jpg "TroubleshootingReference25")  
Figura 25. Fluxograma para a fase de captura  

 **Figura 25. Fluxograma para a fase de captura**  

## <a name="finding-additional-help"></a>Localizar ajuda adicional  
 Localize ajuda adicional na resolução de problemas de implementação do MDT por:  

-   Contactar a Microsoft Support, conforme descrito em [Support da Microsoft](#MicrosoftSupport)  

-   Obter suporte adicional através de blogues e outros recursos de Internet, conforme descrito em [suporte de Internet](#InternetSupport)  

###  <a name="MicrosoftSupport"></a> Microsoft Support  
 A Microsoft fornece Premier e profissional de suporte de nível para o Microsoft Deployment Toolkit.  

 Suporte de nível profissional: [http://support.microsoft.com/](http://support.microsoft.com/)  

 Suporte de nível Premier: [https://premier.microsoft.com/](https://premier.microsoft.com/)  

> [!NOTE]
>  Quando contactar o suporte, ser claro que é o problema com o MDT e a versão específica.  

###  <a name="InternetSupport"></a> Suporte de Internet  
 Várias origens online fornecem assistência adicional de resolução de problemas para o MDT para além de que é abrangido nesta referência. Estas origens online incluem:  

-   Blogues da Microsoft alojados  

    -   [Blogue da equipa do MDT](http://blogs.technet.com/b/msdeployment/)  

    -   [Blogue da equipa do Configuration Manager](http://blogs.technet.com/b/configmgrteam/)  

    -   [Blogue de Miguel Niehaus](http://blogs.technet.com/b/mniehaus/) (Miguel Niehaus escreve na implementação do Windows e o Microsoft Office.)  

-   Microsoft-alojado newsgroups e fóruns:  

     Newsgroups e fóruns que se seguem estão disponíveis com o suporte da Microsoft que os funcionários, parceiros da indústria e valores profissionais da Microsoft:  

    -   [Configuration Manager - implementação do sistema operativo](http://social.technet.microsoft.com/Forums/home?forum=configmanagerosd)  

    -   [Instalação do Windows 8, configuração e implementação](http://social.technet.microsoft.com/Forums/windows/home?forum=w8itproinstall)  

-   Origens de informações relacionadas com a implementação da Microsoft externa:  

    -   [DeployVista.com](http://www.deployvista.com/)  

    -   [myITforum.com](http://www.myitforum.com/)

---
title: Resolução de Problemas do Gestor de Conversão de Pacotes
titleSuffix: Configuration Manager
description: Saiba como resolver problemas com o Package Conversion Manager no Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cb616925-bb94-4b7c-a867-b3d95aef4d5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e586990d049119c3cb00a61c56a1b84763104309
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137903"
---
# <a name="troubleshoot-package-conversion-manager"></a>Resolução de Problemas do Gestor de Conversão de Pacotes

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1357861-->

Utilize as informações neste artigo para o ajudar a resolver problemas ao utilizar o Gestor de conversão de pacotes.



## <a name="sms-provider"></a>Fornecedor de SMS

Gestor de conversão de pacotes utiliza o fornecedor de SMS. Para obter mais informações, consulte [planear o fornecedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).

Se o fornecedor de SMS não está a funcionar corretamente, a consola do Configuration Manager, incluindo o Gestor de conversão de pacotes não funciona.



## <a name="package-readiness"></a>Preparação do pacote

Antes de converter um pacote a uma aplicação, analisar o pacote utilizando o Gestor de conversão de pacotes **Analyze** função. Após a análise, adicione a **preparação** coluna na **pacotes** nó da consola do Configuration Manager. A lista de pacotes apresentará um dos seguintes Estados de preparação do pacote analisado:

 - **Automática**: O pacote pode ser diretamente convertido utilizando o **converter** função.      

    > [!NOTE]  
    > As conversões automáticas não convertem consultas WQL em requisitos de aplicações. Utilize o **corrigir e converter** processo para converter estas consultas.  

 - **Manual**: O pacote precisa de algumas adições ou alterações antes de poder convertê-lo com o **corrigir e converter** função.  

 - **Não aplicável**: O pacote não é adequado para conversão. Ou corrija quaisquer problemas com o pacote ou continuar a implementá-lo como um pacote.  

 - **Erro**: O pacote contém erros. Corrija manualmente estes erros antes de poder analisar e convertê-lo.  

Painel de detalhes dos **pacotes** nó na consola do Configuration Manager mostra quaisquer problemas de preparação. Selecione um pacote e, em seguida, selecione o **resumo** separador no painel de detalhes.



## <a name="log-files"></a>Ficheiros de registo

### <a name="enable-logging"></a>Ativar registo

Quando ativar o registo de Gestor de conversão de pacotes, regista todas as suas ações, exceções e erros. 

Para ativar o registo para este componente no Configuration Manager, modifique **configurationmanagement**. Por predefinição, este ficheiro de configuração está localizado no seguinte caminho:  
`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`  

Insira o seguinte **comutadores** e **rastreio** elementos XML no **System. Diagnostics** elemento após a última **origens** elemento:

``` XML
</sources>

    <switches>
      <add name="PcmLogging" value="3"/>
    </switches>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="PcmTraceListener" type="Microsoft.ConfigurationManagement.UserCentric.Logging.RolloverLogTraceListener, Microsoft.ConfigurationManagement.UserCentric.Logging" initializeData="%UserProfile%\AppData\Local\Temp\PcmTrace.log"/>
      </listeners>
    </trace>

</system.diagnostics>
```

Este exemplo utiliza o ficheiro **PCMTrace.log**. Este registo é no computador que executa a consola do Configuration Manager no seguinte caminho:  
`%UserProfile%\AppData\Local\Temp`

Para configurar o nível de detalhe, altere a **PcmLogging** definição de parâmetro de rastreio. Conjunto a este valor para quatro níveis de detalhe, do menos detalhado (`1`) ao mais detalhado (`4`).


### <a name="smsprovlog"></a>SMSProv.log

Em algumas situações, as informações relevantes para o processo de conversão de pacote de solução de problemas são na **smsprov. log** ficheiro. Este ficheiro recolhe informações de fornecedor de SMS do Configuration Manager.

Por predefinição, este ficheiro de registo está localizado no servidor do site do Configuration Manager no seguinte caminho:  
`C:\Program Files\Microsoft Configuration Manager\Logs`

Se vir uma das seguintes mensagens de erro, o **smsprov. log** ficheiro pode conter informações de resolução de problemas relevantes:

- `The SMS Provider reported an error`

- `Generic Failure`

Estas mensagens de erro normalmente indicam que ocorreu um erro no servidor do site e que as informações de erro não foi enviadas para a consola do Configuration Manager.

Para obter mais informações, consulte [referência técnica para mensagens de erro do Gestor de conversão de pacotes](/sccm/apps/pcm/error-messages).



## <a name="changing-package-attributes-after-analysis"></a>Alterar os atributos de pacote após a análise

Depois de analisar um pacote e tem um Estado de preparação **automática** ou **Manual**, o processo de conversão poderá falhar se alterar qualquer um dos atributos relevantes.

Por exemplo, que analisa um pacote e o estado de preparação é **automática**. Em seguida, adicionar outro programa ao pacote. A conversão de pacote poderá falhar.

Se precisar de efetuar alterações a um pacote após a análise, volte a executar análise antes da conversão. 



## <a name="see-also"></a>Consulte também

[Referência técnica para mensagens de erro do Gestor de conversão de pacotes](/sccm/apps/pcm/error-messages)

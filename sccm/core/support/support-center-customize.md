---
title: Personalizar o Centro de suporte
titleSuffix: Configuration Manager
description: Personalize o ficheiro de configuração do Support Center.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b100daf91b8bb7c5d4dd5f041c57e7dc9dac390e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156785"
---
# <a name="customize-support-center"></a>Personalizar o Centro de suporte

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O [Support Center](/sccm/core/support/support-center) ferramenta inclui um ficheiro de configuração que pode personalizar. Por predefinição, quando instala o Support Center, este ficheiro está no seguinte caminho: `C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config`. O ficheiro de configuração altera o comportamento do programa:

  - [Personalizar a recolha de dados](#bkmk_datacoll): Editar os conjuntos de chaves de registo e espaços de nomes WMI inclui durante a recolha de dados  

  - [Personalizar grupos de registos](#bkmk_loggroups): Defina novos grupos de ficheiros de registo utilizando expressões regulares. Também adicione outros arquivos de log a grupos de registos.  

  - [Recolher ficheiros de registo adicionais utilizando carateres universais](#bkmk_wildcards): Utilizar pesquisas de com carateres universais para recolher ficheiros de registo adicionais  

Para efetuar estas alterações, precisa de permissões administrativas locais no cliente em que instalou o Support Center. Efetuar estas personalizações com um texto ou editor de XML, como o bloco de notas ou o Visual Studio.

> [!Important]  
> O ficheiro de configuração do Support Center é um ficheiro formatado em XML. É essencial para a operação do Centro de suporte. A modificação deste ficheiro só é recomendada para os utilizadores que estão familiarizados com XML e expressões regulares.  

Antes de personalizar o ficheiro de configuração do Support Center, guarde uma cópia de segurança do original. Esta cópia de segurança permite-lhe recuperar a funcionalidade original do Support Center se fizer erros ao editar o ficheiro. Se não criar uma cópia de segurança e o Support Center não funcionar corretamente depois de modificar o ficheiro de configuração, reinstale o Support Center. Também pode copiar um ficheiro de configuração de outra instalação do Support Center.



## <a name="bkmk_datacoll"></a> Personalizar a recolha de dados

Para personalizar a recolha de dados no cliente, modifique o ficheiro de configuração do Support Center, utilizando elementos XML contidos no `<dataCollectorSettings>` elemento.


### <a name="wmi-data-collection"></a>Recolha de dados do WMI

O `<CcmWmiDataCollector>` elemento contém um `<collectionScopes>` elemento. Utilize este elemento para alterar os espaços de nomes WMI do qual o Support Center recolhe dados. Ele também inclui um `<ignoreScopes>` elemento. Utilize este elemento para filtrar a recolha de dados a partir de partes dos espaços de nomes definidos no `<collectionScopes>` elemento.  
    
#### <a name="example"></a>Exemplo
O ficheiro de configuração predefinido recolhe dados a partir do `root\ccm` espaço de nomes. Ele inclui este caminho numa `<add/>` elemento no `<collectionScopes>`. 

Ele também ignora tudo sob o `\cimodels`, `\invagt`, `\events`, e `\policy` caminhos para este espaço de nomes. Ele inclui estes caminhos no `<add/>` elementos contidos no `<ignoreScopes>`.

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### <a name="registry-data-collection"></a>Recolha de dados de registo

O `<RegistryDataCollector>` elemento contém um `<registryKeys>` elemento. Utilize este elemento alterar o registo de chaves e subkeys que o Centro de suporte recolhe sob o `HKEY_LOCAL_MACHINE` caminho. Centro de suporte não suporta a recolha de dados de registo de outros caminhos de registo de raiz.

#### <a name="example"></a>Exemplo
Para recolher chaves de registo para os programas clássicos instaladas no dispositivo, adicione o seguinte `<add/>` elemento no `<registryKeys>` elemento: `<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="bkmk_loggroups"></a> Personalizar grupos de ficheiros de registo

Para personalizar o Centro de suporte de ficheiros de registo que recolhe e como ela apresenta-os na **grupos de registos** listar, usar elementos no `<logGroups>` elemento. Quando iniciar o Support Center, ele analisa esta secção do ficheiro de configuração. Em seguida, cria um grupo no **grupos de registos** lista para cada valor de atributo chave exclusiva encontrada no `<add/>` elementos contidos no `<logGroups>` elemento.

  - **Grupo de registos de componente**: O `<componentLogGroup>` elemento utiliza um atributo-chave para definir o nome do grupo de registo que é apresentada na lista. Ele também usa um atributo de valor que contém uma expressão regular (regex). Ele usa esse regex para recolher um conjunto de ficheiros de registo relacionados.  

  - **Grupo de registos estáticos:** O `<staticLogGroup>` elemento utiliza um atributo-chave para definir o nome do grupo de registo que é apresentada na lista. Ele também usa um atributo de valor que define um nome de ficheiro de registo.  

Se o mesmo valor de atributo chave é utilizado numa `<add/>` elemento em ambos os `<componentLogGroup>` elemento e o `<staticLogGroup>` elemento, o Support Center cria um único grupo. Esse grupo inclui os ficheiros de registo definidos por ambos os elementos que utilizam a mesma chave.

#### <a name="example"></a>Exemplo
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="bkmk_wildcards"></a> Recolher ficheiros de registo adicionais utilizando carateres universais

Para recolher ficheiros de registo adicionais, utilize carateres universais no nome de ficheiro ou caminho do ficheiro. Estes carateres universais, incluir variáveis de ambiente de todo o sistema, como `%WINDIR%`, mas excluir as variáveis de ambiente no âmbito do utilizador, tais como `%USERPROFILE%`. Para recolher ficheiros de registo adicionais utilizando esta pesquisa de ficheiros de registo não recursiva, utilize um `<add/>` elemento dentro do `<additionalLogFiles>` elemento. 

Estes exemplos mostram como o Support Center utiliza esta funcionalidade no arquivo de configuração padrão.

#### <a name="example-1-collect-all-windows-update-log-files-in-the-windows-directory"></a>Exemplo 1: Recolher todos os ficheiros de registo de atualização do Windows no diretório do Windows
O seguinte elemento recolhe qualquer ficheiro com o nome `WindowsUpdate.log` encontrados no diretório do Windows: 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### <a name="example-2-collect-all-log-files-in-the-windows-logs-directory"></a>Exemplo 2: Recolher todos os ficheiros de registo no diretório registos do Windows
O seguinte elemento recolhe qualquer arquivo que termine em `.log` encontrado no diretório de registos do Windows: 

`<add key="%WINDIR%\logs\*.log" />`

#### <a name="full-example-xml"></a>XML de exemplo completo
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```

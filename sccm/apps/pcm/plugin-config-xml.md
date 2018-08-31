---
title: XML de configuração do plug-in
titleSuffix: Configuration Manager
description: Referência técnica para os elementos XML do Package Conversion Manager Plug-in.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 863beac218dd493d75294686a00f9bda569fdfbb
ms.sourcegitcommit: 759098de944b8f7d5eedfc2bae2cb9a6ba15276f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/30/2018
ms.locfileid: "43297755"
---
# <a name="technical-reference-for-the-package-conversion-manager-plug-in-configuration-xml"></a>Referência técnica para a configuração de plug-in do Gestor de conversão de pacotes XML

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1357861-->

Este artigo descreve os elementos XML no ficheiro de configuração do Configuration Manager (configurationmanagement) que controlam o funcionamento do Package Conversion Manager Plug-in. Para obter mais informações sobre como utilizar este plug-in, consulte [como utilizar o Gestor de conversão de pacotes Plug-in](/sccm/apps/pcm/how-to-use-plug-in).



## <a name="xml-configuration-elements"></a>Elementos de configuração XML

A tabela seguinte descreve os elementos XML no ficheiro de configuração do Configuration Manager relacionadas para o Package Conversion Manager Plug-in.

|Elemento  |Type  |Descrição  |
|---------|---------|---------|
|**PcmPlugIn**|Cadeia|O nome do script ou executável a utilizar como o Package Conversion Manager Plug-in.|
|**PcmPlugInTimeoutMilliseconds**|Número inteiro|A quantidade máxima de tempo, em milissegundos, aguardar que o script de plug-in do Gestor de conversão de pacotes ou executável para concluir o processamento de um pacote.|
|**PcmPluginExitCode**|Número inteiro|O código de saída esperado do processo de plug-in. Este valor indica êxito. Todos os outros códigos são considerados como erro.|
|**ForceRequirementsExtraction**|Booleano|Permita a conversão automática para utilizar os requisitos de coleção associados um pacote. Isso só deve ser definido como True ao trabalhar com um pacote de Gestor de conversão de plug-in que foi concebido para tomar decisões sobre que requisitos utilizar.|



## <a name="sample-configuration-xml"></a>XML de configuração de exemplo

Esta secção fornece um exemplo da configuração do Gestor de conversão de pacotes elementos XML no ficheiro de configuração do Configuration Manager, **configurationmanagement**. Por predefinição, este ficheiro está no seguinte caminho:  
`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

No exemplo, os elementos relacionados com o Gestor de conversão de pacotes estão dentro do elemento do seguinte: `Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings`

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```


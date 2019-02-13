---
title: Instalar e configurar as extensões do SCAP
titleSuffix: Configuration Manager
description: Instalar e configurar as extensões Security Content Automation Protocol (SCAP) para o Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b63894764e45e67ef262e345140e245297a11c87
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133940"
---
# <a name="install-and-configure-the-scap-extensions-for-configuration-manager"></a>Instalar e configurar as extensões SCAP para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Após [preparar a infraestrutura](/sccm/compliance/plan-design/scap/about-scap#bkmk_prepare), está pronto para instalar e configurar as extensões SCAP para o Configuration Manager no computador do qual pretende executar este processo.



## <a name="bkmk_install"></a> Instalar as extensões do SCAP

O ficheiro de instalação está localizado no seguinte caminho no diretório de instalação no servidor do site do Configuration Manager:  
`cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi`

1. Cópia **ConfigMgrExtensionsforSCAP.msi** computador com a consola do Configuration Manager em que pretende executar este processo.  

2. No Explorador do Windows, aceda à pasta onde copiou **ConfigMgrExtensionsforSCAP.msi**. Clique duas vezes o arquivo para abri-lo e começar a das extensões SCAP para o Assistente de instalação do Configuration Manager.  

3. Revise o acordo de licença. Clique em **aceito os termos no contrato de licença** e, em seguida, clique em **instalar**.  

4. Quando a instalação estiver concluída, clique em **concluir** para fechar o Assistente de instalação.  

O Assistente de instalação instala as extensões SCAP na pasta de instalação da consola do Configuration Manager. Por predefinição, instalar a consola de pasta é `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole`.  



## <a name="bkmk_scap-data-stream-files"></a> Transferir e instalar os ficheiros de fluxo de dados SCAP

Antes de poder executar as extensões SCAP, tem de transferir os ficheiros de fluxo de dados SCAP de base de dados de vulnerabilidade nacional (NVD) [página de transferência](https://csrc.nist.gov/Projects/United-States-Government-Configuration-Baseline). Em seguida, copie-os para a pasta onde instalou as extensões SCAP.

Dependendo do seu ambiente, poderá não ter todos os dados ficheiros de fluxo SCAP listados na página de transferência.

### <a name="install-the-scap-data-streams"></a>Instalar os fluxos de dados SCAP

1. Visite o [site da NVD](http://nvd.nist.gov/) para identificar os fluxos de dados SCAP que são necessários para sua organização.
Os fluxos de dados SCAP publicados pelo NIST são organizados em múltiplos pacotes, que também são chamados _listas de verificação_.  

2. Transfira os fluxos de dados SCAP do [site da NVD](http://nvd.nist.gov/home.cfm), que são armazenadas em ficheiros comprimidos com uma extensão de nome de ficheiro. zip ou marcados como ficheiros DataStream XML.  

    > [!IMPORTANT]  
    > Existem muitos ficheiros de fluxo de dados SCAP com a extensão. XML que pode transferir da NVD. No entanto, apenas os ficheiros. XML que incluem XCCDF (SCAP1.0 e 1.1) / conteúdo do fluxo de dados (SCAP1.2) são adequados para utilização com as extensões SCAP.  

3. Extraia o SCAP dados fluxos ficheiro. zip ficheiros/DataStream XML que transferiu para a mesma pasta onde instalou as extensões SCAP.  



## <a name="bkmk_convert-and-import"></a> Converter e importar os ficheiros de fluxo de dados SCAP manualmente 

Depois de obter os fluxos de dados SCAP, está pronto para importar e converter os fluxos de dados em linhas de base de configuração. Os fluxos de dados SCAP publicados pelo NIST são organizados em múltiplos pacotes. Siga as instruções do NIST para verificar que pacotes deve utilizar no seu ambiente. Por exemplo, existe um pacote separado para cada versão do Windows, de outro pacote específico da versão para a configuração de firewall e de um pacote para o Internet Explorer. Utilize os procedimentos seguintes para realizar esta tarefa.  

> [!Note]  
> Esta secção descreve o processo manual para converter e importar os ficheiros de fluxo de dados com a consola do Configuration Manager. Para automatizar este processo, consulte a secção seguinte para [automaticamente converter e importar os ficheiros de fluxo de dados SCAP](#bkmk_auto-convert-and-import).  

1. Clique em **importação de conteúdo SCAP** assistente na faixa de opções do grupo de linha de base de configuração.

     ![Botão de conteúdo SCAP importar no Friso da consola](./media/import-scap-content.png)

2. Selecione a opção de conteúdo SCAP.

      ![Selecione a página de opção de conteúdo SCAP do Assistente de importação](./media/import-new-scap-content.png)

3. Selecione o ficheiro de fluxo de dados SCAP, XCCDF e CPE arquivo de dicionário ou ficheiro Oval de conteúdo.

     ![Selecione o ficheiro de fluxo de dados SCAP](./media/select-datastream-file.png)

4. Se o SCAP 1.2, selecione o fluxo de dados. Em seguida, selecione o parâmetro de comparação e o perfil para o SCAP 1.x. Clique em **seguinte** para converter o conteúdo. 

      ![Selecione o parâmetro de comparação e o perfil para 1.2 do SCAP](./media/select-benchmark-and-profile.png)

      > [!Tip]  
      > Esta página do assistente apresenta a linha de comandos que utilizaria com o **ScapToDcm.exe** ferramenta para automatizar o mesmo processo.  

5. Certifique-se os dados de configuração a serem importados.

      ![Confirmar a captura de ecrã de configuração](./media/confirm-configuration.png)

6. Clique em **seguinte** para importar os dados de configuração.

      ![Concluir a importação](./media/complete-import.png)



## <a name="bkmk_auto-convert-and-import"></a> Converter e importar os ficheiros de fluxo de dados SCAP automaticamente 

### <a name="import-with-the-command-line-tool"></a>Importar com a ferramenta de linha de comandos

Depois de obter os fluxos de dados SCAP, pode utilizar o **Microsoft.Sces.ScapToDcm.exe** ferramenta para converter os fluxos de dados SCAP em ficheiros. cab compatível com as definições de conformidade. Em seguida, importe os ficheiros. cab para o Configuration Manager. A ferramenta de Microsoft.Sces.ScapToDcm.exe converte os fluxos de dados SCAP em itens de configuração e linhas de base de configuração que pode usar no Configuration Manager. A ferramenta de Microsoft.Sces.ScapToDcm.exe converte os fluxos de dados SCAP em manifestos XML. Em seguida, empacota os manifestos XML num ficheiro. cab que pode ser importado para o Configuration Manager.

> [!Tip]  
> Passo 4 do processo manual na secção anterior mostra a página do assistente que apresenta a linha de comandos que utilizaria com o **ScapToDcm.exe** ferramenta para automatizar o mesmo processo.  


#### <a name="use-microsoftscesscaptodcmexe-to-convert-scap-data-streams-into-cab-files"></a>Utilizar Microsoft.Sces.ScapToDcm.exe para converter os fluxos de dados SCAP em ficheiros. cab

No prompt de comando, aceda a **AdminConsole\Bin** pasta e execute **Microsoft.Sces.ScapToDcm.exe**. Essa ferramenta gera um ficheiro. cab compatível com as definições de conformidade e o importa para o site do Configuration Manager.

   > [!NOTE]  
   > Sua conta tem de ter permissões de leitura/escrita para a pasta de saída.

**Utilização para o conteúdo de SCAP 1.0/1.1 (ficheiro XCCDF XML, como conteúdos USGCB e DISA):**  

`Microsoft.Sces.ScapToDcm.exe –xccdf <xccdf.xml> -cpe <cpe.xml> -out <outputFolder> [-select benchmark/profile] [-log LogFileName]`  

   > [!NOTE]  
   > Se não especificar o benchmark/perfil ao utilizar o `–select` parâmetro, em seguida, a ferramenta gera um arquivo. cab para cada benchmark no ficheiro de conteúdo.  

**Utilização para o conteúdo do SCAP 1.2 (ficheiro DataStream XML, como os conteúdos USGCB mais recentes):**  

`Microsoft.Sces.ScapToDcm.exe –scap <scapdatastreamfile.xml> -out <outputFolder> [-select datastream/benchmark/profile] [-log LogFileName]`  

   > [!NOTE]  
   > Se não especificar o fluxo de dados/benchmark/perfil ao utilizar o `–select` parâmetro, em seguida, a ferramenta gera um arquivo. cab para cada benchmark no ficheiro de conteúdo.

**Utilização para um ficheiro OVAL único com variáveis externas:**  

`Microsoft.Sces.ScapToDcm.exe –oval <singleOvalFile.xml> [-variable <externalVariableFile.xml>] -out <outputFolder> [-log LogFileName]`  

   > [!NOTE]  
   > Se existirem vários valores para uma variável no ficheiro de variável externa, em seguida, a ferramenta de Microsoft.Sces.ScapToDcm.exe trata os valores como uma matriz desta variável.  



#### <a name="microsoftscesscaptodcmexe-command-line-parameters"></a>Microsoft.Sces.ScapToDcm.exe command-line parameters

| Parâmetro | Utilização | Necessário |
| --- | --- | --- |
| `-scap [scap data stream file]` | Especifique o ficheiro de fluxo de dados SCAP | Sim (para fluxo de dados SCAP 1.2, mutuamente exclusivo com-xccdf e -oval / - variable) |
| `-xccdf [xccdf file]` | Especificar o ficheiro XCCDF | Sim (para XCCDF do SCAP 1.0/1.1, mutuamente exclusivo com-scap e -oval / - variable) |
| `-cpe [cpe file]` | Especifique o ficheiro CPE | Sim (para XCCDF do SCAP 1.0/1.1, mutuamente exclusivo com-scap e -oval / - variable) |
| `-oval [oval file]` | Especificar o ficheiro OVAL | Sim (para o ficheiro OVAL autónomo, mutuamente exclusivo com-xccdf e - scap) |
| `-variable [oval external variable file]` | Especifique o ficheiro OVAL de variável externo | Nenhum (opcional para um ficheiro OVAL autónomo quando existe um externo ficheiro OVAL de variável, mutuamente exclusivo com-xccdf e - scap) |
| `-select [xccdf benchmark/profile]` | Selecionar o benchmark XCCDF, perfil do fluxo de dados SCAP ou ficheiro XCCDF | Nenhum (este parâmetro não é necessária mas recomendado. Se não for especificado, em seguida, a ferramenta gera um cab para todos os perfis no fluxo de dados/benchmarks incorporados tudo) |
| `-out [output directory]` | Especifique onde será a saída do arquivo cab do DCM | Não (se não for especificado, em seguida, a ferramenta lista apenas o conteúdo sem conversão) |
| `-log [log file]` | Especifique o ficheiro de registo | Não (se não for especificado, em seguida, o registo é escrito para o ficheiro de Microsoft.Sces.ScapToDcm.log) |
| `-help` ou `-?` | Imprimir a utilização da ferramenta | Não |


#### <a name="microsoftscesscaptodcmexe-examples"></a>Microsoft.Sces.ScapToDcm.exe examples

**Conteúdo SCAP 1.2:**  

`Microsoft.Sces.ScapToDcm.exe –scap scap_gov.nist_USTCB-ie8.xml –out .\mytestfolder –select mySCAPDataStreamID/myBenchMarkID/myProfileID`  

**Conteúdos SCAP 1.0/1.1:**  

`Microsoft.Sces.ScapToDcm.exe–xccdf scap_gov.nist_Test-WinXP_xccdf.xml –cpe scap_gov.nist_Test-WinXP_cpe.xml –out .\mytestfolder –select XCCDFBenchmarkID/MyProfileID`  

**Conteúdo SCAP OVAL:**  

`Microsoft.Sces.ScapToDcm.exe –oval myOvalFile.xml –variable myOvalExternalVariableFile.xml –out .\mytestfolder`  


#### <a name="sample-output-from-microsoftscesscaptodcmexe"></a>Saída de exemplo de Microsoft.Sces.ScapToDcm.exe

```
  Compliance Settings compliant cab file created:

  Validate the schema of SCAP data stream file C:\24SCAP\BVT_Test_Data_Stream.xml

  Successfully validate the schema of SCAP data stream file C:\24SCAP\BVT_Test_Data_Stream.xml

  Process XCCDF Benchmark xccdf_tst.bvt_benchmark_Windows-F

  Process XCCDF Profile: xccdf_tst.bvt_profile_version_1.0.0.0-BVT Profile #1

  Process OVAL: scap_tst.bvt_comp_Windows-F-oval.xml

  Successfully finished process OVAL: scap_tst.bvt_comp_Windows-F-oval.xml

  Process OVAL: scap_tst.bvt_comp_Windows-F-cpe-oval.xml

  Successfully finished process OVAL: scap_tst.bvt_comp_Windows-F-cpe-oval.xml
   Process SCAP data stream: scap_tst.bvt_datastream_Windows-F.zip
    SCAP Data Stream: [scap_tst.bvt_datastream_Windows-F.zip]

  Version:        [1.2]

  Timestamp:      [2/24/2012]

  Use-case:       [CONFIGURATION]

  CPE Dictionary:  [scap_tst.bvt_comp_Windows-F-cpe-dictionary.xml]

  OVAL:              [Windows-F-cpe-oval.xml]
  Product name:    [National Institute of Standards and Technology]

  Product version: []

  Schema version:  [5.3]

  Timestamp:       [2/24/2012]

  XCCDF Benchmark: [xccdf_tst.bvt_benchmark_Windows-F]

  Version:       [v1.0.0.0]
   Update:        [http://usgcb.nist.gov]

  Timestamp:     [2/24/2012]

  Status:        [accepted]

  Status date:   [2/24/2012]

  Title:         [Ohh New BVT for SCAP 1.2]

 Description:   [My description]

  XCCDF Profile: [xccdf_tst.bvt_profile_version_1.0.0.0]
 
  OVAL:              [Windows-F-oval.xml]

   Product name:    [scaptool]

   Product version: []

   Schema version:  [5.4]

   Timestamp:       [2/24/2012]

  Start SCAP to DCM conversion...

  Processing SCAP data stream: scap_tst.bvt_datastream_Windows-F.zip

  Processing CPE dictionary: scap_tst.bvt_comp_Windows-F-cpe-dictionary.xml

  …

  Generating CI baseline cab file: C:\28\bbt\xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab

  Successfully generated CI baseline cab file: C:\28\bbt\xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab

  Successfully converted XCCDF profile: xccdf_tst.bvt_profile_version_1.0.0.0 into DCM baseline xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab
```


### <a name="import-the-cab-file"></a>Importar o ficheiro. cab.

A próxima etapa do processo é utilizar a consola do Configuration Manager para importar os ficheiros. cab compatível com as definições de conformidade para o Configuration Manager. Quando importar os ficheiros. cab que criou anteriormente neste processo, um ou mais itens de configuração e linhas de base de configuração são criadas na base de dados do Configuration Manager. Posteriormente no processo pode implementar linhas de base de configuração em coleções de dispositivos. Para obter mais informações, consulte [importar dados de configuração](/sccm/compliance/deploy-use/import-configuration-data).

A localização do ficheiro. cab que criou anteriormente é a pasta especificada pelo `–output` parâmetro da ferramenta Microsoft.Sces.ScapToDcm.exe.

> [!IMPORTANT]  
> Repita este processo para cada ficheiro. cab que criou anteriormente no processo. Há um arquivo. cab para cada perfil selecionado no ficheiro XCCDF/DataStreamXML que transferiu a partir do web site da NVD. Pode processar estes ficheiros ao executar a ferramenta de Microsoft.Sces.ScapToDcm.exe.  

A linha de base de configuração importados é só de leitura, o respetivo estado é *Enabled*e seu estado implantado *não*. O **data de modificação** propriedade mostra o tempo que importou a linha de base. O nome da linha de base de configuração é proveniente de secção nome a apresentar do XCCDF/Datastream XML. O nome é construído de acordo com a Convenção `ABC[XYZ]`, onde **ABC** é o ID do Benchmark XCCDF e **XYZ** é o ID de perfil XCCDF (se estiver selecionado um perfil).



## <a name="next-step"></a>Passo seguinte
> [!div class="nextstepaction"]
> [Implementar e monitorizar a conformidade do SCAP e exportar resultados de compatibilidade](/sccm/compliance/plan-design/scap/deploy-monitor-export)

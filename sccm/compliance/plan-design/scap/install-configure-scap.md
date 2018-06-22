---
title: Instalar e configurar as extensões Security Content Automation Protocol (SCAP)
titleSuffix: Configuraton Manager
description: Instalar e configurar as extensões Security Content Automation Protocol (SCAP)
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 891d21b44ed6efca73413a46d0483519b76f9cae
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336600"
---
# <a name="install-and-configure-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>Instalar e configurar as extensões SCAP para o Microsoft System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

> [!Tip]  
> Esta funcionalidade foi introduzida pela primeira vez na versão de pré-visualização técnica 1803 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Esta versão de pré-lançamento das extensões SCAP pode ser instalado em quaisquer versões atualmente suportadas do ramo atual do Configuration Manager e LTSB 1606. O ficheiro de instalação está localizado em cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi a partir de pré-visualização técnica 1803.   

Depois de preparar a infraestrutura de pré-requisito, está pronto para instalar e configurar as extensões SCAP para o Microsoft System Center Configuration Manager no computador a partir do qual pretende executar este processo.

## <a name="install-scap-extensions-configuration-manager"></a>Instalar o Gestor de configuração de extensões do SCAP

1. Execute o ConfigMgr\_extensões\_para\_SCAP.msi para instalar a ferramenta.
2. No Explorador do Windows, aceda à pasta onde transferiu o **ConfigMgr\_extensões\_para\_SCAP.msi** de ficheiros e, em seguida, faça duplo clique o **ConfigMgr\_ Extensões\_para\_SCAP.msi** ficheiro. Esta ação inicia as extensões SCAP para o Assistente de instalação do Microsoft System Center Configuration Manager.

Concluir o **das extensões SCAP para o Assistente de instalação do Microsoft System Center Configuration Manager** utilizando as informações na tabela seguinte, o Assistente de a aceitar&#39;predefinido s valores não ser que necessite de especificá-los.

**Tabela 1.0** das extensões SCAP para o processo de Assistente de instalação do Configuration Manager do Microsoft System Center

| Nome da página do Assistente | Ação do utilizador |
| --- | --- |
| Bem-vindo e o contrato de licença de utilizador final |1. Reveja o contrato de licença|
| Bem-vindo e o contrato de licença de utilizador final|2. Clique em **aceito os termos no contrato de licença**.|
| Bem-vindo e o contrato de licença de utilizador final|3. Clique em **Instalar**.|
| Concluir as extensões SCAP para o Assistente de instalação do Microsoft System Center Configuration Manager |4. Clique em **Concluir**.|
 



As extensões SCAP para o Assistente de instalação do Microsoft System Center Configuration Manager instala as extensões por predefinição na pasta de instalação da consola do Configuration Manager.



## <a name="download-and-install-the-scap-data-stream-files"></a>Transferir e instalar os ficheiros de fluxo de dados SCAP

Antes de poder executar as extensões SCAP para converter ficheiros de fluxo de dados SCAP e, em seguida, importe-as para a funcionalidade de definições de compatibilidade, tem de transferir os ficheiros de fluxo de dados SCAP de base de dados de vulnerabilidade National (NVD) [transferir página](http://nvd.nist.gov/fdcc/download_fdcc.cfm)Do Web site. Em seguida, copie-os para a pasta onde instalou as extensões SCAP

Dependendo do seu ambiente, poderá não ter todos os dados ficheiros de fluxo SCAP listados na página de transferência.

Para instalar os fluxos de dados SCAP

1. Visite o [site da Nvd](http://nvd.nist.gov/) para identificar os fluxos de dados SCAP que são exigidos pela sua organização.
Os fluxos de dados SCAP publicados pela NIST estão organizados em múltiplos pacotes, também designados por _listas de verificação_.

2. Transfira os fluxos de dados SCAP do [site da Nvd](http://nvd.nist.gov/home.cfm), que estão armazenados em ficheiros comprimidos com uma extensão de nome de ficheiro. zip ou marcados como ficheiros DataStream XML.

    >[!IMPORTANT] 
    >Existem muitos ficheiros de fluxo de dados SCAP com a extensão. XML que pode transferir da NVD. No entanto, apenas os ficheiros. XML que incluem XCCDF (scap 1.0 e 1.1) conteúdos DataStream (scap 1.2) são adequados para utilização com as extensões SCAP.

3. Extraia o SCAP dados fluxos. zip ficheiros/ficheiro DataStream XML que transferiu para a mesma pasta onde instalou as extensões SCAP.

## <a name="convert-and-import-the-scap-data-stream-files-using-the-import-scap-content-wizard"></a>Converter e importar os ficheiros de fluxo de dados SCAP utilizando o Assistente para importar conteúdo do SCAP

Após obter os fluxos de dados SCAP, está pronto para importar e converter os fluxos de dados em linhas de base de configuração. Os fluxos de dados SCAP publicados pela NIST estão organizados em múltiplos pacotes. Siga o NIST&#39;s as instruções para verificar que pacotes deve utilizar no seu ambiente. Por exemplo, é um pacote separado para cada versão do Windows, outro pacote específico da versão para a configuração da firewall e um pacote para o Internet Explorer 8.0. Utilize os procedimentos seguintes para realizar esta tarefa.

### <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>Para importar os fluxos de dados SCAP para o Configuration Manager

1. Inicie o Assistente de conteúdo SCAP para importar a partir do Friso de linha de base de configuração.

     ![Iniciar o Assistente de conteúdo de SCAP de importar a partir do Friso de linha de base de CI](./media/import-scap-content.png)

2. Selecione o tipo de conteúdo.

      ![Selecione o tipo de conteúdo](./media/import-new-scap-content.png)

3. Selecione o ficheiro datastream SCAP, XCCDF e CPE ficheiro de dicionário ou ficheiro Oval de conteúdo.

     ![Selecione o ficheiro de fluxo de dados SCAP](./media/select-datastream-file.png)

4. Se o SCAP 1.2, selecione o fluxo de dados. Em seguida, selecionar o benchmark e o perfil para o SCAP 1. x.  Selecione **seguinte** para converter o conteúdo. Verá uma barra de progresso.

      ![Selecionar o benchmark e perfil para o SCAP 1.2](./media/select-benchmark-and-profile.png)

5. Confirme os dados de configuração a serem importados.

      ![Confirme a captura de ecrã de configuração](./media/confirm-configuration.png)

6. Clique em**seguinte** para importar os dados de configuração.

      ![Concluir a importação](./media/complete-import.png)

## <a name="alternate-method-convert-and-import-the-scap-data-stream-files-using-the-cmd-line-tool"></a>(Método alternativo) Converter e importar os ficheiros de fluxo de dados SCAP com a ferramenta de linha cmd

Após obter os fluxos de dados SCAP, pode utilizar a ferramenta de Microsoft.Sces.ScapToDcm.exe para converter os fluxos de dados SCAP em ficheiros. cab de definições de compatibilidade. Em seguida, importe os ficheiros. cab para o Configuration Manager. A ferramenta de Microsoft.Sces.ScapToDcm.exe converte os fluxos de dados SCAP em itens de configuração e linhas de base de configuração que pode aceder ao utilizar a funcionalidade de definições de compatibilidade no Configuration Manager. A ferramenta de Microsoft.Sces.ScapToDcm.exe converte os fluxos de dados SCAP em manifestos XML. Em seguida, pacotes os manifestos XML num ficheiro. cab que poderá importar para o Configuration Manager.

Os fluxos de dados SCAP publicados pela NIST estão organizados em múltiplos pacotes. Siga o NIST&#39;s as instruções para verificar que pacotes deve utilizar no seu ambiente. Por exemplo, é um pacote separado para cada versão do Windows, outro pacote específico da versão para a configuração da firewall e um pacote para o Internet Explorer 8.0. Utilize os procedimentos seguintes para realizar esta tarefa.





## <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>Para importar os fluxos de dados SCAP para o Configuration Manager

1. Converta os fluxos de dados SCAP num ficheiro. cab de definições de compatibilidade.
2. Importe o ficheiro. cab para o Configuration Manager.

### <a name="convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files"></a>Converter os fluxos de dados SCAP em ficheiros do. cab de definições de compatibilidade

Antes de poder analisar e avaliar a compatibilidade dos seus sistemas, terá de converter os fluxos de dados SCAP em formato XML em manifestos XML que são compatíveis com itens de configuração de definições de compatibilidade e linhas de base de configuração. A ferramenta de Microsoft.Sces.ScapToDcm.exe converte os fluxos de dados SCAP em manifestos XML. Em seguida, pacotes os manifestos XML num ficheiro. cab que pode ser posteriormente importado para o Configuration Manager.

#### <a name="to-convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files-using-the-microsoftscesscaptodcmexe-tool"></a>**Converter os fluxos de dados SCAP em ficheiros. cab de definições de compatibilidade com a ferramenta de Microsoft.Sces.ScapToDcm.exe**

Na linha de comandos, aceda à pasta de AdminConsole\Bin, execute Microsoft.Sces.ScapToDcm.exe para gerar um cab de definições de compatibilidade e importe-o para o site do Configuration Manager.

   >[!NOTE] 
   > A conta tem de ter permissões de leitura/escrita para a pasta de saída

**Para conteúdos SCAP 1.0/1.1 (ficheiro XCCDF XML, como conteúdos USGCB e DISA):**

 Microsoft.Sces.ScapToDcm.exe-xccdf &lt;xccdf.xml&gt; - cpe &lt;cpe.xml&gt; -out &lt;outputFolder&gt; [-selecionar o benchmark/perfil] [-registo LogFileName]

   >[!NOTE] 
   >Se não&#39;t especificar o benchmark/perfil ao utilizar – parâmetro selecionado, a ferramenta irá gerar um cab DCM para cada benchmark no ficheiro de conteúdo.

**Para conteúdos scap 1.2 conteúdo-(ficheiro DataStream XML, como os conteúdos usgcb mais recentes):**

Microsoft.Sces.ScapToDcm.exe – scap &lt;scapdatastreamfile.xml&gt; -out &lt;outputFolder&gt; [-selecione o fluxo de dados/benchmark/perfil] [-registo LogFileName]

   >[!NOTE] 
   > Se não&#39;t especificar o fluxo de dados/benchmark/perfil ao utilizar o parâmetro selecionado, em seguida, a ferramenta irá gerar um cab DCM para cada benchmark no ficheiro de conteúdo.

**Para um ficheiro OVAL único com variáveis externas:**

Microsoft.Sces.ScapToDcm.exe – oval &lt;singleOvalFile.xml&gt; [-variável &lt;externalVariableFile.xml&gt;]-out &lt;outputFolder&gt; [-registo LogFileName]

   >[!NOTE] 
   > Se existirem vários valores para uma variável no ficheiro de variável externa, em seguida, a ferramenta de Microsoft.Sces.ScapToDcm.exe irão tratar os valores como uma matriz desta variável.



#### <a name="microsoftscesscaptodcmexe-command-line-parameters"></a>Microsoft.Sces.ScapToDcm.exe. Parâmetros da linha de comandos

| **Parâmetro** | **Utilização** | **Necessário** |
| --- | --- | --- |
| -scap [ficheiro de fluxo de dados scap] | Especifique o ficheiro de fluxo de dados SCAP | Sim (para fluxo de dados SCAP 1.2, mutuamente exclusivo com-xccdf e -oval / - variable) |
| -xccdf [ficheiro xccdf] | Especifique o ficheiro XCCDF | Sim (para XCCDF do SCAP 1.0/1.1, mutuamente exclusivo com-scap e -oval / - variable) |
| -cpe [ficheiro cpe] | Especifique o ficheiro CPE | Sim (para XCCDF do SCAP 1.0/1.1, mutuamente exclusivo com-scap e -oval / - variable) |
| -oval [ficheiro oval] | Especifique o ficheiro OVAL | Sim (para um ficheiro OVAL autónomo, mutuamente exclusivo com-xccdf e - scap) |
| -variável [ficheiro oval de variável externa] | Especifique o ficheiro OVAL de variável externo | Não (opcional para um ficheiro OVAL autónomo quando existe um externo ficheiro OVAL de variável, mutuamente exclusivo com-xccdf e - scap) |
| -Selecionar [benchmark/perfil de xccdf] | Selecionar o benchmark XCCDF, o perfil do fluxo de dados SCAP ou ficheiro XCCDF | Não (sugerimos que especifique este parâmetro. Se não for especificado, a ferramenta irá gerar um ficheiro cab para todos os perfis no fluxo de dados/benchmarks incorporados todos) |
| -out [diretório de saída] | Especifique onde será a saída do ficheiro cab de DCM | Não (se não for especificado, em seguida, a ferramenta só irá listar o conteúdo sem conversão) |
| -registo [ficheiro de registo] | Especifique o ficheiro de registo | Não (se não for especificado, em seguida, o registo é escritos no ficheiro de Microsoft.Sces.ScapToDcm.log) |
| -ajudar / -? | Imprimir a utilização da ferramenta | Não |





#### <a name="the-following-command-lines-are-samples-for-the-microsoftscesscaptodcmexe-tool"></a>As seguintes linhas de comando são exemplos para a ferramenta de Microsoft.Sces.ScapToDcm.exe:

**Conteúdos scap 1.2:**

  Microsoft.Sces.ScapToDcm.exe – scap scap\_gov.nist\_USTCB ie8.xml – horizontalmente. \mytestfolder – selecione myBenchMarkID/mySCAPDataStreamID/myProfileID

**SCAP1.0/1.1 conteúdo:**

   Microsoft.Sces.ScapToDcm.exe–xccdf scap\_gov.nist\_teste WinXP\_xccdf.xml – cpe scap\_gov.nist\_teste WinXP\_cpe.xml – horizontalmente. \mytestfolder – selecione XCCDFBenchmarkID/MyProfileID

**Conteúdo OVAL SCAP:**

  Microsoft.Sces.ScapToDcm.exe – oval myOvalFile.xml – myOvalExternalVariableFile.xml variável – horizontalmente. \mytestfolder

**O resultado seguinte é exemplo da ferramenta de Microsoft.Sces.ScapToDcm.exe:**

  Ficheiro de cab compatível do definições de compatibilidade criado:

  Validar o esquema do ficheiro de fluxo de dados SCAP C:\24SCAP\BVT\_teste\_dados\_Stream.xml

  Validar com êxito o esquema do ficheiro de fluxo de dados SCAP C:\24SCAP\BVT\_teste\_dados\_Stream.xml

  Processo XCCDF Benchmark xccdf\_tst.bvt\_benchmark\_Windows-F

  Perfil do processo XCCDF: xccdf\_tst.bvt\_perfil\_versão\_1.0.0.0-BVT perfil n. º 1

  Processo OVAL: scap\_tst.bvt\_concluída\_Windows-F-oval.xml

  Foi concluído com êxito o processo OVAL: scap\_tst.bvt\_concluída\_Windows-F-oval.xml

  Processo OVAL: scap\_tst.bvt\_concluída\_Windows-F-cpe-oval.xml

  Foi concluído com êxito o processo OVAL: scap\_tst.bvt\_concluída\_fluxo de dados SCAP de processos do Windows-F-cpe-oval.xml: scap\_tst.bvt\_datastream\_Windows F.zip SCAP dados Fluxo: [scap\_tst.bvt\_datastream\_Windows F.zip]

  Versão: [1.2]

  Timestamp: [24/2/2012]

  Caso de utilização: [Configuração]

  CPE dicionário: [scap\_tst.bvt\_concluída\_Windows-F-cpe-dictionary.xml]

  OVAL: Nome do produto [Windows-F-cpe-oval.xml]: [National Institute of Standards e tecnologia]

  Versão do produto:]

  Versão do esquema: [5.3]

  Timestamp: [24/2/2012]

  XCCDF Benchmark: [xccdf\_tst.bvt\_benchmark\_Windows-F]

  Versão: [v1.0.0.0] atualização: [http://usgcb.nist.gov]

  Timestamp: [24/2/2012]

  Estado: [aceites]

  Data de estado: [24/2/2012]

  Título: [esqueceu BVT novo para o SCAP 1.2]

 Descrição: [A minha descrição]

  Perfil XCCDF: [xccdf\_tst.bvt\_perfil\_versão\_1.0.0.0]
 
  OVAL: [Windows-F-oval.xml]

   Nome do produto: [scaptool]

   Versão do produto:]

   Versão do esquema: [5.4]

   Timestamp: [24/2/2012]

  Inicie SCAP a conversão de DCM...

  Processar o fluxo de dados SCAP: scap\_tst.bvt\_datastream\_F.zip do Windows

  Processamento de dicionário CPE: scap\_tst.bvt\_concluída\_Windows-F-cpe-dictionary.xml

  …

  A gerar o ficheiro do ficheiro cab de linha de base de CI: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Ficheiro do ficheiro cab de linha de base de CI foi gerado com êxito: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Converter com êxito de perfil XCCDF: xccdf\_tst.bvt\_perfil\_versão\_1.0.0.0 para xccdf de linha de base DCM\_tst.bvt\_benchmark\_Windows-F [xccdf \_tst.bvt\_perfil\_versão\_1.0.0.0].cab

## <a name="next-step"></a>Passo seguinte
> [!div class="nextstepaction"]
> [Importar as definições de compatibilidade SCAP e exportar resultados de compatibilidade](/sccm/compliance/plan-design/scap/import-scap-compliance-settings)

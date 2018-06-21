---
title: Importar as definições de compatibilidade SCAP
titleSuffix: Configuraton Manager
description: Importar as definições de compatibilidade SCAP como linhas de base de configuração e exportar os resultados
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 1f6b1fa0dd0775083eff9925a65509083b3f47d3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336617"
---
# <a name="import-the-compliance-settings-compliant-cab-files-into-system-center-configuration-manager"></a>Importar os ficheiros. cab de definições de compatibilidade para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

> [!Tip]  
> Esta funcionalidade foi introduzida pela primeira vez na versão de pré-visualização técnica 1803 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Esta versão de pré-lançamento das extensões SCAP pode ser instalado em quaisquer versões atualmente suportadas do ramo atual do Configuration Manager e LTSB 1606. O ficheiro de instalação está localizado em cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi a partir de pré-visualização técnica 1803. 

O próximo passo no processo consiste em utilizar a consola do Configuration Manager para importar os conformidade definições ficheiros. cab para o Configuration Manager. Quando importar os ficheiros. cab que criou anteriormente neste processo, um ou mais itens de configuração e linhas de base de configuração são criadas na base de dados do Configuration Manager. Posteriormente no processo pode atribuir cada uma das linhas de base de configuração para uma coleção de computadores no Configuration Manager.

## <a name="to-import-the-compliance-settings-compliant-cab-files-into-configuration-manager"></a>Para importar os ficheiros. cab de definições de compatibilidade para o Configuration Manager

1. Abra o **consola do Configuration Manager**.
2. No  **do Configuration Manager, no painel de navegação, aceda a \*\* ativos e compatibilidade**> **as definições de compatibilidade** > **linhas de base de configuração** .

3. No painel ações, clique em **importar dados de configuração** para iniciar o Assistente de dados de configuração de importação.

1. Concluir o **Assistente de importação de dados de configuração** utilizando as informações na seguinte tabela e aceitar os valores predefinidos exceto indicação em contrário.



Importar o processo do Assistente de dados de configuração

| Nome da página do Assistente | Ação do utilizador |
| --- | --- |
| **Escolher ficheiros** |1. Clique em **Adicionar**. </br>É apresentada a caixa de diálogo aberta.|
||2. No **abra** caixa de diálogo, aceda ao **&lt;saída cab compatível\_pasta &gt;**. Clique em de  **&lt; compatíveis\_cab&gt;** ficheiro. cab, onde _compliant cab **saída\_pasta** é a pasta que foi especificada a seguir – parâmetro de saída quando executou a ferramenta de Sces.ScapToDcm.exe. **em conformidade\_ficheiro** é o nome de um ficheiro. cab que criou anteriormente no processo. Em seguida, clique em **abra**. </br> Consola do Configuration Manager – aparece a caixa de diálogo de aviso de segurança.|
||3. No **consola do Configuration Manager-aviso de segurança** caixa de diálogo, clique em **executar**. Na página escolher ficheiros, os dados de configuração é apresentada na lista de linhas de base a importar.|
||3. Clique em **Seguinte**.|
| **Resumo** |5. Clique em **Seguinte**. |
| **A concluir o Assistente de dados de configuração de importação** |6. Clique em **Fechar**. |

A nova linha de base de configuração é apresentada no painel de informações da consola do Configuration Manager.

>[!IMPORTANT]
> Terá de repetir este processo para cada ficheiro. cab que criou anteriormente no processo. Não há um ficheiro. cab para cada selectedprofile no ficheiro XCCDF/DataStreamXML que transferiu a partir do site da Nvd, que pode processar ao executar a ferramenta de Microsoft.Sces.ScapToDcm.exe.

A linha de base de configuração importados é só de leitura e tem um Estado de &#39;ativado&#39; e um Estado de implementação inicial de &#39;não&#39;.  O &#39;data de modificação&#39; propriedade indica o tempo que a linha de base foi importada.  O nome da linha de base de configuração é retirado da secção nome a apresentar do XCCDF/Datastream XML. O nome é construído com a seguinte convenção:

ABC [XYZ], onde ABC é o ID do Benchmark XCCDF e XYZ é o ID de perfil XCCDF (se estiver selecionado um perfil).



## <a name="assign-configuration-baselines-to-the-computer-collections"></a>Atribuir linhas de base de configuração às coleções de computadores

Depois de criar as coleções de computadores apropriados para os computadores que pretende avaliar para compatibilidade SCAP, está pronto para atribuir linhas de base de configuração que importou para associar às coleções de computadores. Esta secção fornece informações para atribuir uma linha de base de configuração a uma coleção de computadores utilizando a consola do Configuration Manager.

Para atribuir uma linha de base de configuração a uma coleção de computadores:

1. Abra o **do Configuration Manager****consola**.

2. No **consola do Configuration Manager, no painel de navegação, aceda a **ativos e compatibilidade** > **as definições de compatibilidade**  >**  Configuração linhas de base * *.
3. No painel de navegação, clique em &lt; * * configuração\_linha de base >, onde &lt; _configuração\_linha de base&gt;_  é o nome da linha de base de configuração que pretende atribuir a uma coleção de computadores.

    Apresenta a lista de itens de configuração para a linha de base de configuração no painel de informações do Configuration Manager.

4. No painel ações, clique em **implementar**.

5. Concluir o **implementar****linha de base de configuração****diálogo** utilizando as informações na seguinte tabela e aceitar os valores predefinidos exceto indicação em contrário.

### <a name="deploy-configuration-baseline-dialog-process"></a>Implementar o processo de caixa de diálogo de linha de base de configuração

| Nome da página do Assistente | Ação do utilizador |
| --- | --- |
| **Escolher coleção** | 1. Clique em **Procurar**.|
||2. No **selecionar coleção** caixa de diálogo, selecione **coleções de dispositivos**. Em seguida, clique em  **&lt;computador\_coleção&gt;**, onde &lt; _computador\_coleção&gt;_  é o nome do coleção de computadores que criou anteriormente no processo. Clique em **OK**.|
| **Definir o agendamento** |3. Selecione o agendamento que é adequado para a sua organização.|
 
>[!IMPORTANT]
> Repita este processo para cada coleção de computadores que pretende atribuir a cada linha de base de configuração. No mínimo, atribua cada linha de base de configuração para, pelo menos, uma coleção de computadores.

## <a name="verify-that-the-compliance-data-has-been-collected"></a>Certifique-se de que os dados de compatibilidade foram recolhidos

Antes de exportar os dados de conformidade para o formato SCAP, terá de verificar que os dados foram recolhidos. Depois de atribuir uma linha de base de configuração para uma coleção de computadores, o cliente do Configuration Manager em cada computador na coleção reúne automaticamente as informações de compatibilidade. Em seguida, as informações de compatibilidade são armazenadas na base de dados do Configuration Manager.

Ver o estado da implementação de linha de base de configuração no Configuration Manager para se certificar de que os dados adequados foram recolhidos pelos clientes do Configuration Manager. É importante verificar que os dados de compatibilidade adequados foram recolhidos no Configuration Manager porque pode ajudar a validar os ficheiros de resultados XCCDF/DataStream que cria posteriormente no processo.



### <a name="verify-that-the-compliance-data-has-been-collected"></a>Certifique-se de que os dados de compatibilidade foram recolhidos

1. Abra a consola do Configuration Manager.
2. Na consola do Configuration Manager, no painel de navegação, aceda a **monitorização** > **implementações**.
3. Clique em de **funcionalidade tipo** para ordenar o tipo de implementação e encontrar itens cujo tipo seja **linha de base** na lista.
4. Clique com botão direito do &lt;configuração\_linha de base&gt; na lista que acabou de implementar a recolha e clique em **Ver estado**.
5. Em seguida, avance para o &lt;configuração\_linha de base&gt; nó para ver o estado de compatibilidade, se existir uma máquina no Estado desconhecido, significa que a recolha de dados de conformidade ainda não foi concluída para que a máquina.

### <a name="validate-the-xccdfdatastream-results"></a>Validar os resultados XCCDF/Datastream

1. Abra a consola do Configuration Manager.
2. Na consola do Configuration Manager, no painel de navegação, aceda a **as definições de compatibilidade** > **SCAP Dashboard**.
3. Selecione a linha de base de configuração, a atribuição, ficheiro SCAP, Datastream, Benchmark e perfil (se aplicável).
4. Clique em **Mostrar relatório**
 ![relatório SCAP](./media/scap-report.png)



## <a name="export-compliance-results-to-scap-format"></a>Exportar resultados de compatibilidade para o formato SCAP

A tarefa seguinte no processo consiste em exportar os dados de conformidade de definições de compatibilidade para o formato SCAP, que é um ficheiro de ARFreport no formato XML/legível por humanos. O Assistente de exportação de extensões do SCAP e a ferramenta de Microsoft.Sces.DcmToScap.exe exportar um ficheiro de resultados XCCDF/DataStreamARF separado para cada linha de base de configuração de definições de compatibilidade. Estes ficheiros correspondem a cada ficheiro de entrada XCCDF/DataStream que utiliza a ferramenta de Microsoft.Sces.ScapToDcm.exe para criar cada linha de base de configuração de definições de compatibilidade.

### <a name="export-the-compliance-settings-compliance-data-using-the-export-scap-report-wizard"></a>Exportar os dados de conformidade de definições de compatibilidade utilizando o Assistente para exportar relatórios SCAP

1. Inicie o Assistente para exportar relatórios SCAP do menu do clique direito no Dashboard do SCAP.
![Importar a partir do dashboard do SCAP](./media/import-from-scap-dashboard.png)

2. Selecione a linha de base de configuração e atribuição ![selecione linha de base](./media/select-ci-baseline.png)

3. Escolha a localização do ficheiro de fluxo de dados SCAP, ficheiro XCCDF/CPE ou ficheiros de conteúdo e variável Oval.
![Escolha o fluxo de dados](./media/export-scap-report-datastream.png)

4. Especifique o nome da organização e escolha a localização da pasta para exportar o relatório SCAP.
 ![Escolha o fluxo de dados](./media/specify-org-export.png)

5. Confirme as definições.
 ![Escolha o fluxo de dados](./media/confirm-export.png)

6. Escolha * * junto ao exportar o relatório.  Verá uma barra de progresso e, em seguida, uma página de conclusão.
 ![Concluir a exportação](./media/complete-report-export.png)



### <a name="alternate-method-export-the-compliance-settings-compliance-data-using-the-microsoftscesdcmtoscapexe-tool"></a>(Método alternativo) Exportar os dados de conformidade de definições de compatibilidade com a ferramenta de Microsoft.Sces.DcmToScap.exe

1. Na linha de comandos, vá para o tipo de pasta AdminConsole\Bin os parâmetros da linha de comandos listados na seguinte tabela e, em seguida, prima * * ENTER:

    >[!NOTE] 
    >A conta tem de ter permissões de leitura para o fornecedor do Configuration Manager e também de ter permissões de escrita para a pasta de saída especificado no parâmetro de saída da linha de comandos.

**Para conteúdos SCAP 1.0/1.1 (como conteúdos USGCB e DISA):**

Microsoft.Sces.DcmToScap.exe-a linha de base BaselineCIID-atribuição AssignmentID-xccdf &lt;xccdf.xml&gt; - cpe &lt;cpe.xml&gt; -selecione &lt;xccdfBenchmark/perfil&gt; -out &lt;outputResultFolder&gt; [-registo logFileName]

  >[!NOTE] 
    >Deve utilizar o – selecione parâmetro para especificar o benchmark/perfil que foi avaliado nos clientes se existirem múltiplos benchmarks/perfis no conteúdo.

**Para conteúdos scap 1.2 (por exemplo, os conteúdos USGCB mais recentes):**

Microsoft.Sces.DcmToScap.exe-linha de base BaselineCIID-atribuição AssignmentID-selecione &lt;xccdfBenchmark/datastream/perfil&gt; -out &lt;outputResultFolder&gt; [-registo logFileName]

   >[!NOTE] 
   >Deve utilizar o – selecione parâmetro para especificar o fluxo de dados/benchmark/perfil que foi avaliado nos clientes se existirem vários fluxos de dados/benchmark/perfil no conteúdo.

**Para um ficheiro OVAL único com variáveis externas:**

Microsoft.Sces.DcmToScap.exe-a linha de base BaselineCIID-atribuição AssignmentID – oval &lt;singleOvalFile.xml&gt; [-variável &lt;externalVariableFile.xml&gt;]-out &lt;outputResultFolder &gt; [-registo logFileName]

   >[!NOTE] 
    >O _will Microsoft.Sces.DcmToScap.exe apenas gerar o relatório de resultados de definição OVAL para cada computador de destino, o relatório ARF não será gerado.

#### <a name="how-to-get-baseline-ci-id-and-assignment-id"></a>Como obter o ID de CI de linha de base e o ID de atribuição

Na consola de administração, aceda a **ativos e compatibilidade** > **as definições de compatibilidade** > **linhas de base de configuração**. O ID de CI é o ID de CI de linha de base de configuração.

![Obter o CI ID e o ID de atribuição](./media/get-to-baselines.png)

Selecione a linha de base de configuração pretendida, clique o separador de implementações, se o ID de atribuição de mensagens em fila não se encontra no ecrã, faça duplo clique no cabeçalho da coluna, clique em ID de atribuição de ativá-la.
![Obter o CI ID e o ID de atribuição](./media/get-to-baselines.png)


#### <a name="microsoftscesdcmtoscapexe-command-line-parameters"></a>Parâmetros da linha de comandos Microsoft.Sces.DcmToScap.exe

| **Parâmetro** | **Utilização** | **Necessário** |
| --- | --- | --- |
| -a linha de base [ID de CI de linha de base] | Especifique a linha de base de configuração | Sim |
| -atribuição [ID de atribuição] | Especifique a implementação de linha de base de configuração | Sim |
| -organização [nome da organização] | Especifique o nome da organização, que será apresentado no relatório. Podem ser separado por &#39;; &#39; para especificar um nome de organização com várias linhas. | Não |
| -tipo [dinâmico/completo/completosemcs] | Especifique o tipo de resultado OVAL: resultado dinâmico, ou resultado completo ou resultado completo sem característica do sistema. | Não (se não for especificado, em seguida, o valor predefinido é completo) |
| -scap [ficheiro de fluxo de dados scap] | Especifique o ficheiro de fluxo de dados SCAP | Sim (para fluxo de dados SCAP 1.2, mutuamente exclusivo com-xccdf e -oval / - variable) |
| -xccdf [ficheiro xccdf] | Especifique o ficheiro XCCDF | Sim (para XCCDF do SCAP 1.0/1.1, mutuamente exclusivo com-scap e -oval / - variable) |
| -cpe [ficheiro cpe] | Especifique o ficheiro CPE | Sim (para XCCDF do SCAP 1.0/1.1, mutuamente exclusivo com-scap e -oval / - variable) |
| -oval [ficheiro oval] | Especifique o ficheiro OVAL | Sim (para um ficheiro OVAL autónomo, mutuamente exclusivo com-xccdf e - scap) |
| -variável [ficheiro oval de variável externa] | Especifique o ficheiro OVAL de variável externo | Não (opcional para um ficheiro OVAL autónomo quando existe um externo ficheiro OVAL de variável, mutuamente exclusivo com-xccdf e - scap) |
| -Selecionar [benchmark/perfil de xccdf] | Selecionar o benchmark XCCDF, o perfil do fluxo de dados SCAP ou ficheiro XCCDF | Sim (uma seleção têm de ser efetuada para gerar um relatório para que pode corresponder a linha de base DCM correspondente na base de dados do Configuration Manager |
| -out [diretório de saída] | Especificar a localização onde o ficheiro cab de definições de compatibilidade de saída | Não (se não for especificado, em seguida, a ferramenta lista apenas o conteúdo sem conversão) |
| -registo [ficheiro de registo] | Especifique o ficheiro de registo | Não (se não for especificado, em seguida, o registo é escritos no ficheiro de Microsoft.Sces.DcmToScap.log) |
| -ajudar / -? | Imprimir a utilização da ferramenta | Não |



 >[!TIP] 
 >Pode especificar? -h ou -help para apresentar a sintaxe da ferramenta Microsoft.Sces.DcmToScap.exe e uma lista dos parâmetros.

Por predefinição, a ferramenta de Microsoft.Sces.DcmToScap.exe acede a base de dados do Configuration Manager com as suas credenciais. A ferramenta de Microsoft.Sces.DcmToScap.exe requer um mínimo de acesso de leitura para a base de dados do Configuration Manager.

Depois de verificar que o adequado **ARF** relatório: _ARF\_xxxx.xml_ e/ou **legível por humanos** relatório: xxx.txt, **Cyberscope** relatório: LASR\_xxx.xml, **ConsumedOval** relatório: xx-oval -&lt;machineName&gt;. XML, **resultados do XCCDF Benchmark** relatório: xccdf\_xxx.xml ficheiros existem , na linha de comandos, escreva saída e, em seguida, prima **ENTER** para sair da linha de comandos.

## <a name="next-step"></a>Passo seguinte
> [!div class="nextstepaction"]
> [Resolução de problemas](/sccm/compliance/plan-design/scap/troubleshooting-scap)

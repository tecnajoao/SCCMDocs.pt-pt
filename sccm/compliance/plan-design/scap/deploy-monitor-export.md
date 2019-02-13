---
title: Implementar e monitorizar a conformidade do SCAP
titleSuffix: Configuration Manager
description: Implementar as definições de conformidade do SCAP como linhas de base de configuração, monitorizar a conformidade e exportar os resultados.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e3280edbe900e96cf97af8e59578ceab5322ee2a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137301"
---
# <a name="deploy-and-monitor-scap-compliance-in-configuration-manager"></a>Implementar e monitorizar a conformidade do SCAP no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois de ter [convertido e importados](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import) os ficheiros de fluxo de dados SCAP, consulte os seguintes passos:  

- [Implementar](#bkmk_deploy) linhas de base de configuração para coleções para avaliar dispositivos para compatibilidade SCAP  

- [Monitor](#bkmk_monitor) os dados de conformidade devolvido dos clientes de destinados  

- [Exportar](#bkmk_export) os resultados de compatibilidade para o formato SCAP  



## <a name="bkmk_deploy"></a> Implementar linhas de base de configuração de SCAP

Primeiro de criar as coleções de dispositivos para os computadores que pretende avaliar para compatibilidade SCAP. Para obter mais informações, consulte [criar coleções](/sccm/core/clients/manage/collections/create-collections).  

Agora, está pronto para implementar linhas de base de configuração que importou a estas coleções de dispositivos. Para obter mais informações, consulte [como implementar linhas de base de configuração](/sccm/compliance/deploy-use/deploy-configuration-baselines).  

> [!Tip]  
> Repita este processo para cada linha de base de configuração que pretende implementar em cada coleção de dispositivos. No mínimo, implemente cada linha de base de configuração à coleção, pelo menos, um dispositivo.



## <a name="bkmk_monitor"></a> Monitorizar os dados de conformidade do SCAP 

Antes de exportar os dados de conformidade para o formato SCAP, terá de verificar que o site tem recolhidos os dados. Depois de implementar uma linha de base de configuração para uma coleção de dispositivos, o cliente do Configuration Manager em cada computador na coleção reúne automaticamente as informações de conformidade. Em seguida, as informações de conformidade são armazenadas na base de dados do Configuration Manager.

Ver o estado da implementação de linha de base da configuração no Configuration Manager para se certificar de que os dados adequados foram recolhidos pelos clientes do Configuration Manager. É importante verificar que os dados de compatibilidade adequados foram recolhidos no Configuration Manager porque ele pode ajudá-lo a validar os ficheiros de resultados XCCDF/DataStream que cria posteriormente no processo.

Para obter mais informações, consulte [monitorizar as definições de conformidade](/sccm/compliance/deploy-use/monitor-compliance-settings).


### <a name="validate-the-xccdfdatastream-results"></a>Valide os resultados XCCDF/fluxo de dados

1. Na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**e selecione o **SCAP Dashboard**.  

2. Selecione a linha de base de configuração, atribuição, ficheiro SCAP, fluxo de dados, Benchmark e perfil (se aplicável).  

3. Clique em **Mostrar relatório**
 ![relatório SCAP de exemplo](./media/scap-report.png)



## <a name="bkmk_export"></a> Exportar resultados de compatibilidade para o formato SCAP

A próxima etapa do processo é exportar os dados de conformidade para o formato SCAP, que é um ficheiro de relatório ARF no formato XML/legível. O Assistente de exportação de extensões do SCAP e a ferramenta de linha de comando Microsoft.Sces.DcmToScap.exe exportar um arquivo de resultados XCCDF/DataStreamARF separado para cada linha de base de configuração. Estes ficheiros correspondem a cada ficheiro de entrada XCCDF/DataStream que a ferramenta de Microsoft.Sces.ScapToDcm.exe utiliza para criar cada linha de base de configuração.


### <a name="manually-export-with-the-console-wizard"></a>Exportar manualmente com o Assistente da consola

> [!Note]  
> Esta secção descreve o processo manual para exportar os resultados de compatibilidade com a consola do Configuration Manager. Para automatizar este processo, consulte a secção seguinte para [exportar automaticamente com a ferramenta de linha de comando](#bkmk_auto-export).  


1. Iniciar o **exportar o relatório de SCAP** assistente clicando com o **SCAP Dashboard** nó.  
![Iniciar o Assistente para exportar o relatório de SCAP a partir do Dashboard do SCAP](./media/import-from-scap-dashboard.png)

2. Selecione a linha de base de configuração, atribuição e tipo de conteúdo SCAP.  
![Selecione a linha de base](./media/select-ci-baseline.png)

3. Escolha a localização do ficheiro de fluxo de dados SCAP, ficheiro XCCDF/CPE ou ficheiros Oval de variável e conteúdos.  
![Escolha o fluxo de dados](./media/export-scap-report-datastream.png)

4. Especifique o nome da organização e escolher a localização da pasta para exportar o relatório SCAP.  
 ![Escolha o fluxo de dados](./media/specify-org-export.png)
   > [!Tip]  
   > Esta página do assistente apresenta a linha de comandos que utilizaria com o **DcmToScap.exe** ferramenta para automatizar o mesmo processo.  

5. Confirme as definições.  
 ![Escolha o fluxo de dados](./media/confirm-export.png)

6. Escolher **seguinte** para exportar o relatório. Conclua o assistente.  
 ![Concluir a exportação](./media/complete-report-export.png)


### <a name="bkmk_auto-export"></a> Exportar automaticamente com a ferramenta de linha de comandos

Abra a linha de comandos e aceda ao Configuration Manager **AdminConsole\Bin** pasta. Utilize um dos exemplos da linha de comandos a seguir:  

> [!NOTE]  
> Sua conta tem de ter permissões de leitura para o fornecedor do Gestor de configuração. Também precisa de permissões de escrita para a pasta especificada no `–out` parâmetro da linha de comandos.

**Para conteúdos de SCAP 1.0/1.1 (como conteúdos USGCB e DISA):**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –xccdf <xccdf.xml> -cpe <cpe.xml>  -select <xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

  > [!NOTE]  
  > Se existirem múltiplos benchmarks/perfis no conteúdo, utilize o `–select` parâmetro para especificar o benchmark/perfil que foi avaliado nos clientes.  

**Para conteúdos SCAP1.2 (por exemplo, os conteúdos USGCB mais recentes):**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID -select <datastream/xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > Se existirem vários fluxo de dados/benchmark/perfil no conteúdo, utilize o `–select` parâmetro para especificar o fluxo de dados/benchmark/perfil que foi avaliado nos clientes.  

**Para um ficheiro OVAL único com variáveis externas:**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –oval <singleOvalFile.xml> [-variable <externalVariableFile.xml>] -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > O Microsoft.Sces.DcmToScap.exe só gera o relatório de resultados de definição OVAL para cada máquina de destino. O relatório ARF não é gerado.  


#### <a name="how-to-get-the-baselineciid-and-assignmentid"></a>Como obter o BaselineCIID e AssignmentID

Na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**e selecione **linhas de base de configuração**. O `BaselineCIID` é o identificador (ID) para a linha de base de configuração.  
![Obter o CI ID e o ID de atribuição](./media/get-to-baselines.png)

Selecione a linha de base de configuração pretendida e clique nas **implementações** separador. O `AssignmentID` é o identificador (ID) para a implementação de linha de base de configuração para uma coleção de dispositivos. Se o ID de atribuição não for apresentado, clique com o botão direito no cabeçalho da coluna e selecione **ID de atribuição**.  
![Obter o CI ID e o ID de atribuição](./media/get-to-baselines.png)


#### <a name="microsoftscesdcmtoscapexe-command-line-parameters"></a>Parâmetros de linha de comando Microsoft.Sces.DcmToScap.exe

| Parâmetro | Utilização | Necessário |
| --- | --- | --- |
| `-baseline [Baseline CI ID]` | Especifique a linha de base de configuração | Sim |
| `-assignment [Assignment ID]` | Especifique a implementação de linha de base de configuração | Sim |
| `-organization [organization name]` | Especifique o nome da organização, que será apresentado no relatório. Pode ser separado por `;` para especificar um nome de organização com várias linhas. | Não |
| `-type [thin/full/fullnosc]` | Especifique o tipo de resultado OVAL: resultado dinâmico, ou resultado completo ou resultado completo sem característica do sistema. | Não (se não for especificado, em seguida, o valor predefinido é completo) |
| `-scap [scap data stream file]` | Especifique o ficheiro de fluxo de dados SCAP | Sim (para fluxo de dados SCAP 1.2, mutuamente exclusivo com-xccdf e -oval / - variable) |
| `-xccdf [xccdf file]` | Especificar o ficheiro XCCDF | Sim (para XCCDF do SCAP 1.0/1.1, mutuamente exclusivo com-scap e -oval / - variable) |
| `-cpe [cpe file]` | Especifique o ficheiro CPE | Sim (para XCCDF do SCAP 1.0/1.1, mutuamente exclusivo com-scap e -oval / - variable) |
| `-oval [oval file]` | Especificar o ficheiro OVAL | Sim (para o ficheiro OVAL autónomo, mutuamente exclusivo com-xccdf e - scap) |
| `-variable [oval external variable file]` | Especifique o ficheiro OVAL de variável externo | Nenhum (opcional para um ficheiro OVAL autónomo quando existe um externo ficheiro OVAL de variável, mutuamente exclusivo com-xccdf e - scap) |
| `-select [xccdf benchmark/profile]` | Selecionar o benchmark XCCDF, perfil do fluxo de dados SCAP ou ficheiro XCCDF | Sim (uma seleção têm de ser feita para gerar um relatório para que pode corresponder a linha de base DCM correspondente na base de dados do Configuration Manager |
| `-out [output directory]` | Especifique onde será a saída do arquivo cab de definições de compatibilidade | Não (se não for especificado, em seguida, a ferramenta lista apenas o conteúdo sem conversão) |
| `-log [log file]` | Especifique o ficheiro de registo | Não (se não for especificado, em seguida, o registo é escrito Microsoft.Sces.DcmToScap.log ficheiro) |
| `-help` ou `-?` | Imprimir a utilização da ferramenta | Não |

 > [!TIP]  
 > Pode especificar a `-?`, `–h`, ou `–help` para apresentar a sintaxe da ferramenta Microsoft.Sces.DcmToScap.exe e uma lista dos parâmetros.

Por predefinição, a ferramenta de Microsoft.Sces.DcmToScap.exe acessa o banco de dados do Configuration Manager com as suas credenciais. A ferramenta de Microsoft.Sces.DcmToScap.exe requer um mínimo de acesso de leitura para a base de dados do Configuration Manager.

Depois de executar a ferramenta, certifique-se de que os seguintes ficheiros existem: 
- **ARF** relatório: `_ARF_xxxx.xml_` e/ou **legível por humanos** relatório: `xxx.txt`
- **Cyberscope** relatório: `LASR_xxx.xml`
- **ConsumedOval** relatório: `xx-oval-<machineName>.xml`
- **Resultados do XCCDF Benchmark** relatório: `xccdf_xxx.xml` 



## <a name="next-step"></a>Passo seguinte
> [!div class="nextstepaction"]
> [Resolução de problemas](/sccm/compliance/plan-design/scap/troubleshooting-scap)

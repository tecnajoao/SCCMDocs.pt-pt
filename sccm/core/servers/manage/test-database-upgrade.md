---
title: "Testar a atualização do banco de dados | Microsoft Docs"
description: "Teste de atualização do banco de dados do site ao instalar as atualizações para o Configuration Manager."
ms.custom: na
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 3619a73d3a39659de927e1711a7ec81de9918064
ms.openlocfilehash: 6b76c97cd205bb02683a7bfa1eb378471a75551d
ms.contentlocale: pt-pt
ms.lasthandoff: 06/13/2017


---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>Testar a atualização do banco de dados, ao instalar uma atualização

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

As informações neste tópico podem ajudá-lo a executar uma atualização de banco de dados de teste antes de instalar uma atualização no console para a ramificação atual do Configuration Manager. No entanto, a atualização de teste não é mais necessário ou recomendável etapa, a menos que seu banco de dados é suspeito ou está modificado por personalizações não são explicitamente suportadas pelo Configuration Manager.

## <a name="do-i-need-to-run-a-test-upgrade"></a>É necessário executar uma atualização de teste?
A substituição desse teste de atualização é possibilitada devido a alterações que foram introduzidas com o System Center Configuration Manager. Essas alterações simplificam o processo e a velocidade em que um ambiente de produção pode ser atualizado para versões mais recentes. Essa reestruturação foi feita para ajudar os clientes a manter-se atualizado com menos risco e menos sobrecarga operacional durante a instalação de cada nova atualização.

As alterações são como instalar atualizações, incluindo lógica que será revertida automaticamente uma atualização com falha sem a necessidade de executar uma recuperação de site. Essas alterações permitem o uso do console para gerenciar instalações de atualização e incluem uma opção para [repetir a instalação de uma atualização com falha](/sccm/core/servers/manage/install-in-console-updates#bkmk_retry).

> [!TIP]
> Quando você atualizar para o System Center Configuration Manager de um produto mais antigo, como o System Center 2012 Configuration Manager, [atualizações de banco de dados de teste permanecem uma etapa recomendada](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#a-namebkmktesta-test-the-site-database-upgrade).

Se quiser testar a atualização de um banco de dados do site quando você instala uma atualização no console, os seguintes suplementos de informações de [orientação sobre como instalar uma atualização no console](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

## <a name="prepare-to-run-a-test-database-upgrade"></a>Preparar para executar uma atualização de banco de dados de teste  
Antes de instalar uma nova atualização em sua hierarquia, como atualizar 1702, você pode testar a atualização de seu banco de dados do site.

Para executar o teste de atualização, use a instalação do Configuration Manager dos arquivos de origem do [CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder) de um site que executa a versão do Configuration Manager que você está atualizando a. Esse requisito significa que, para testar a atualização do banco de dados para atualização 1702:
-   Você deve ter pelo menos um site que executa a versão 1702 do qual você pode obter esse CD. Pasta mais recente.
-   Se você não tiver um site que executa a versão necessária, considere instalar um site em um ambiente de laboratório e, em seguida, atualize o site para a nova versão. Isso cria o CD. Pasta mais recente com a versão correta dos arquivos de origem.

O teste de atualização é executado em um backup de seu banco de dados do site restaurado para uma instância separada do SQL Server.  Execute a instalação a partir de **CD. Última** pasta com o **testdbupgrade** opção de linha de comando para testar a atualização que restaurar a cópia do banco de dados. Após a atualização de teste, o banco de dados atualizado será descartado. Ele não pode ser usado por um site do Configuration Manager.

Se uma atualização falha da instalação, você não precisará recuperar o site. Em vez disso, você poderá repetir a instalação da atualização de dentro do console.

##  <a name="run-the-test-upgrade"></a>Executar o teste de atualização    
1.  Use o Gerenciador de configuração de instalação e os arquivos de origem do **CD. Última** pasta de um site que executa a versão que você planeja atualizar.  

2.  Copie o **CD. Última** pasta em um local na instância do SQL Server que você usará para executar a atualização do banco de dados de teste.

3.  Crie um backup de dados do site que você deseja testar a atualização. Em seguida, restaure uma cópia desse banco de dados a uma instância do SQL Server que não hospede um site do Configuration Manager. A instância do SQL Server deve usar a mesma edição do SQL Server como seu banco de dados do site.  

4.  Depois de restaurar a cópia do banco de dados, execute **instalação** do CD. Última pasta que contém os arquivos de origem da versão que você está atualizando a. Ao executar a Configuração, utilize a opção da linha de comandos **/TESTDBUPGRADE** . Se a instância do SQL Server que hospeda a cópia do banco de dados não é a instância padrão, forneça os argumentos de linha de comando para identificar a instância que hospeda a cópia de banco de dados do site.   

  Por exemplo, você tem um banco de dados do site com o nome do banco de dados *SMS_ABC*. Restaurar uma cópia desse banco de dados do site para uma instância com suporte do SQL Server com o nome da instância *DBTest*. Para testar uma atualização dessa cópia do banco de dados do site, use a seguinte linha de comando: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**.  

  Você pode encontrar o Setup.exe no seguinte local na mídia de origem para o System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

5.  Na instância do SQL Server em que você executar o teste de atualização, monitorar o *ConfigMgrSetup.log* na raiz da unidade do sistema para o progresso e o sucesso.  

     Se o teste de atualização falhar, corrija os problemas relacionados à falha de atualização do banco de dados do site. Em seguida, crie um novo backup do banco de dados do site e testar a atualização da nova cópia do banco de dados.  



## <a name="next-steps"></a>Passos seguintes
Após a atualização do banco de dados de teste for concluído com êxito, descarte o banco de dados atualizado. Ele não pode ser usado por um site do Configuration Manager. Você pode retornar a seu site ativo e [começar a instalação da atualização](/sccm/core/servers/manage/install-in-console-updates).


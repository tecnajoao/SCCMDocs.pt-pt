---
title: Atualização de base de dados de teste
titleSuffix: Configuration Manager
description: Teste de atualização de base de dados do site quando instalar atualizações para o Configuration Manager.
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3bd64cd937bf0a90a00ea6b17664d80394dcafab
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>Testar a atualização de base de dados quando instalar uma atualização

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As informações neste tópico podem ajudar a executar um teste de atualização de base de dados antes de instalar uma atualização na consola para o ramo atual do Configuration Manager. No entanto, o teste de atualização já não é necessária ou Recomendamos passo, a menos que a base de dados é suspeita ou é modificado pelo personalizações explicitamente não suportadas pelo Configuration Manager.

## <a name="do-i-need-to-run-a-test-upgrade"></a>É necessário executar um teste de atualização?
Descontinuação de teste de atualização é disponibilizada devido a alterações que foram introduzidas com o System Center Configuration Manager. Estas alterações simplificam o processo e a velocidade a que um ambiente de produção pode ser atualizado para versões mais recentes. Este recriar foi efetuada para ajudar os clientes Mantenha-se atualizado com menor o risco e menos sobrecarga operacional quando instalar cada atualização de novo.

As alterações são a forma como a instalação de atualizações, incluindo lógica automaticamente reverte uma atualização falhada sem a necessidade de executar uma recuperação de site. Estas alterações permitem a utilização da consola para gerir as instalações de atualizações e inclui uma opção para [repetir a instalação de uma atualização falhada](/sccm/core/servers/manage/install-in-console-updates#bkmk_retry).

> [!TIP]
> Quando atualizar para o System Center Configuration Manager a partir de um produto mais antigo, como o System Center 2012 Configuration Manager, [atualizações da base de dados de teste permanecem um passo recomendado](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#a-namebkmktesta-test-the-site-database-upgrade).

Se pretender testar a atualização da base de dados do site quando instala uma atualização na consola, as seguinte suplementos de informações ainda o [orientações sobre como instalar uma atualização na consola](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

## <a name="prepare-to-run-a-test-database-upgrade"></a>Preparar para executar um teste de atualização de base de dados  
Antes de instalar uma nova atualização na sua hierarquia, como a atualização 1702, pode testar a atualização da sua base de dados do site.

Para executar o teste de atualização, utilize o programa de configuração do Configuration Manager dos ficheiros de origem do [CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder) de um site que executa a versão do Configuration Manager que estão a atualizar a. Este requisito significa que para testar a atualização de base de dados para a atualização para 1702:
-   Tem de ter pelo menos um site que executa a versão 1702 da qual pode obter antes esse CD. Pasta mais recente.
-   Se não tiver um site que executa a versão necessária, considere a instalação de um site num ambiente de laboratório e, em seguida, atualizar esse site para a nova versão. Esta ação cria o CD. Pasta mais recente com a versão correta dos ficheiros de origem.

O teste de atualização é executado em relação a uma cópia de segurança da sua base de dados do site restaurada para uma instância separada do SQL Server.  Execute a configuração a partir de **CD. Mais recente** pasta com o **testdbupgrade** comutador da linha de comandos para testar a atualização restaurada da cópia da base de dados. Depois de concluir o teste da atualização, a base de dados atualizada é rejeitado. Não pode ser utilizado por um site do Configuration Manager.

Se uma atualização instalar falhar, deve não terá de recuperar o site. Em vez disso, pode tentar novamente a instalação de atualização a partir da consola.

##  <a name="run-the-test-upgrade"></a>Executar o teste da atualização    
1.  Utilize o Gestor de configuração do programa de configuração e os ficheiros de origem do **CD. Mais recente** pasta de um site que executa a versão que pretende atualizar.  

2.  Copiar o **CD. Mais recente** pasta para uma localização na instância do SQL Server que irá utilizar para executar o teste de atualização de base de dados.

3.  Crie uma cópia de segurança da base de dados do site que pretende testar a atualização. Em seguida, restaure uma cópia dessa base de dados para uma instância do SQL Server que não aloje um site do Configuration Manager. Instância do SQL Server tem de utilizar a mesma edição do SQL Server como a base de dados do site.  

4.  Depois de restaurar a cópia da base de dados, execute **configuração** partir do CD. Pasta mais recente que contém os ficheiros de origem da versão que está a atualizar. Ao executar a Configuração, utilize a opção da linha de comandos **/TESTDBUPGRADE** . Se a instância do SQL Server que aloja a cópia da base de dados não for a instância predefinida, fornece os argumentos da linha de comandos para identificar a instância que aloja a cópia da base de dados de site.   

  Por exemplo, tem uma base de dados do site com o nome de base de dados *SMS_ABC*. Restaurar uma cópia desta base de dados do site para uma instância suportada do SQL Server com o nome de instância *DBTest*. Para testar uma atualização desta cópia da base de dados do site, use a seguinte linha de comandos: **Setup.exe /testdbupgrade. DBtest\CM_ABC**.  

  Pode encontrar o Setup.exe na seguinte localização no suporte de dados de origem para o System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

5.  Na instância do SQL Server em que executou o teste de atualização, monitorizar o *ConfigMgrSetup.log* na raiz da unidade do sistema para o progresso e êxito.  

     Se o teste da atualização falhar, corrija quaisquer problemas relacionados com a falha de atualização de base de dados de site. Em seguida, crie uma nova cópia de segurança da base de dados do site e testar a atualização da nova cópia da base de dados.  



## <a name="next-steps"></a>Passos seguintes
Concluído com êxito a atualização de base de dados de teste, elimine a base de dados atualizado. Não pode ser utilizado por um site do Configuration Manager. Em seguida, pode regressar ao seu site do Active Directory e [começar a instalação da atualização](/sccm/core/servers/manage/install-in-console-updates).

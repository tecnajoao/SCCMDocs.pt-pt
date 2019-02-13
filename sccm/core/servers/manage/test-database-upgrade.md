---
title: Atualização da base de dados de teste
titleSuffix: Configuration Manager
description: Teste de atualização da base de dados do site quando instalar atualizações para o Configuration Manager.
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6adb326a484976335d114277e095884e107f9906
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124801"
---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>Testar a atualização de base de dados ao instalar uma atualização

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As informações neste tópico podem ajudá-lo a executar um teste de atualização da base de dados antes de instalar uma atualização na consola para o ramo atual do Configuration Manager. No entanto, o teste de atualização já não é necessária ou Recomendamos passo, a menos que a base de dados suspeito ou é modificada por personalizações que não tenham sido explicitamente suportadas pelo Configuration Manager.

## <a name="do-i-need-to-run-a-test-upgrade"></a>É necessário executar um teste de atualização?
Remoção de teste de atualização se tornou possível devido a alterações introduzidas com o System Center Configuration Manager. Estas alterações simplificam o processo e a velocidade pelo qual um ambiente de produção pode ser atualizado para versões mais recentes. Essa reformulação foi feita para ajudar os clientes a manter-se atualizado com menos riscos e menos sobrecarga operacional ao instalar a cada nova atualização.

As alterações são a forma como as atualizações são instaladas, incluindo lógica automaticamente reverterá-se de uma atualização falhada sem a necessidade de executar uma recuperação de site. Estas alterações permitem a utilização da consola para gerir as instalações de atualização e inclui uma opção para [repetir a instalação de uma atualização falhada](/sccm/core/servers/manage/install-in-console-updates#bkmk_retry).

> [!TIP]
> Ao atualizar para o System Center Configuration Manager a partir de um produto mais antigo, como o System Center 2012 Configuration Manager, [atualizações de base de dados de teste permaneçam um passo recomendado](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#a-namebkmktesta-test-the-site-database-upgrade).

Se ainda quiser testar a atualização de uma base de dados do site quando instalar uma atualização na consola, as seguinte suplementos de informações a [documentação de orientação sobre como instalar uma atualização na consola](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

## <a name="prepare-to-run-a-test-database-upgrade"></a>Preparar para executar um teste de atualização da base de dados  
Antes de instalar uma nova atualização na sua hierarquia, como a atualização 1702, pode testar a atualização da sua base de dados do site.

Para executar o teste de atualização, utilize a configuração do Configuration Manager dos arquivos de origem do [o CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder) de um site que executa a versão do Configuration Manager que está a atualizar a. Este requisito significa que, para testar a atualização da base de dados para atualização 1702:
-   Tem de ter pelo menos um site que executa a versão 1702 do que pode obter esse CD. Pasta mais recente.
-   Se não tiver um site que executa a versão necessária, considere a instalação de um site num ambiente de laboratório e, em seguida, atualizar esse site para a nova versão. Esta ação cria o CD. Pasta mais recente com a versão correta dos arquivos de origem.

O teste de atualização é executado em relação a uma cópia de segurança da sua base de dados do site restaurada para uma instância separada do SQL Server.  Executar a configuração da **CD. Mais recente** pasta com o **testdbupgrade** comutador da linha de comandos para testar a atualização que restaurar a cópia da base de dados. Depois de concluída a atualização de teste, a base de dados atualizada é descartado. Não pode ser utilizado por um site do Configuration Manager.

Se uma atualização instalar falhar, não deverá precisar recuperar o site. Em vez disso, pode tentar novamente a instalação da atualização da consola do.

##  <a name="run-the-test-upgrade"></a>Executar o teste de atualização    
1. Utilize o Gestor de configuração do programa de configuração e os ficheiros de origem a partir do **CD. Mais recente** pasta de um site que executa a versão que pretende atualizar.  

2. Copiar o **CD. Mais recente** pasta para uma localização na instância do SQL Server que irá utilizar para executar o teste de atualização da base de dados.

3. Crie uma cópia de segurança da base de dados do site que pretende testar a atualização. Em seguida, restaure uma cópia dessa base de dados para uma instância do SQL Server que não aloje um site do Configuration Manager. Instância do SQL Server tem de utilizar a mesma edição do SQL Server da base de dados do site.  

4. Após restaurar a cópia da base de dados, execute **configuração** partir do CD. Pasta mais recente que contém os ficheiros de origem da versão que está a atualizar. Ao executar a Configuração, utilize a opção da linha de comandos **/TESTDBUPGRADE** . Se a instância do SQL Server que aloja a cópia da base de dados não for a instância predefinida, fornece os argumentos da linha de comandos para identificar a instância que aloja a cópia de base de dados do site.   

   Por exemplo, tem uma base de dados do site com o nome de base de dados *SMS_ABC*. Restaurar uma cópia desta base de dados do site para uma instância suportada do SQL Server com o nome da instância *DBTest*. Para testar uma atualização desta cópia da base de dados do site, utilize a seguinte linha de comando: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**.  

   Pode encontrar Setup.exe na seguinte localização na mídia de origem para o System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

5. Na instância do SQL Server em que executou o teste de atualização, monitorizar o *configmgrsetup. log* na raiz da unidade do sistema para o progresso e êxito.  

    Se o teste de atualização falhar, corrija eventuais problemas relacionados com a falha de atualização de base de dados de site. Em seguida, crie uma nova cópia de segurança da base de dados do site e testar a atualização da nova cópia da base de dados.  



## <a name="next-steps"></a>Passos seguintes
Depois da atualização da base de dados de teste concluída com êxito, elimine a base de dados atualizado. Não pode ser utilizado por um site do Configuration Manager. Em seguida, pode regressar ao seu site do Active Directory e [começar a instalação da atualização](/sccm/core/servers/manage/install-in-console-updates).

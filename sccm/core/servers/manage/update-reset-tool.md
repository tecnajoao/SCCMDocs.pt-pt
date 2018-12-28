---
title: Ferramenta de reposição de atualizações
titleSuffix: Configuration Manager
description: Utilize a ferramenta de reposição de atualização para atualizações na consola do System Center Configuration Manager.
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de5c98e45c6f5d6dca1569de812825cce80d6f70
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417348"
---
# <a name="update-reset-tool"></a>Ferramenta de reposição de atualizações

*Aplica-se a: O System Center Configuration Manager (ramo atual)*  


Que começa com a versão 1706, sites de administração central e sites primários do Configuration Manager, incluir a atualização de reposição de ferramenta do Configuration Manager, **CMUpdateReset.exe**. Utilize a ferramenta para corrigir os problemas quando as atualizações na consola tem problemas ao transferir ou replicar. A ferramenta encontra-se no ***\cd.latest\SMSSETUP\TOOLS*** pasta do servidor do site.

Pode utilizar esta ferramenta com qualquer versão do ramo atual no suporte.

Utilize esta ferramenta quando uma [atualização na consola](/sccm/core/servers/manage/install-in-console-updates) ainda não tiver instalada e está no estado de falha. Estado de falha significa que o download de atualização está em progresso mas bloqueados ou a demorar um tempo excessivamente longo. Muito tempo é considerado como horário mais do que as suas expectativas históricas para pacotes de atualização de tamanho similar. Também pode ser uma falha ao replicar a atualização para sites primários subordinados.  

Quando executar a ferramenta, ele é executado em relação a atualização que especificou. Por predefinição, a ferramenta não elimina as atualizações instaladas ou transferidas com êxito.  

### <a name="prerequisites"></a>Pré-requisitos
A conta que utiliza para executar a ferramenta requer as seguintes permissões:
-   **Leia** e **escrever** permissões para a base de dados do site de administração central e para cada site primário na sua hierarquia. Para definir estas permissões, pode adicionar a conta de utilizador como membro do **db_datawriter** e **db_datareader** [funções de base de dados fixas](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) no Configuration Manager base de dados de cada site. A ferramenta não interage com os sites secundários.
-   **Administrador local** no site de nível superior da sua hierarquia.
-   **Administrador local** no computador que aloja o ponto de ligação de serviço.

É necessário o GUID do pacote de atualização que pretende repor. Para obter o GUID:
  1.   Na consola, aceda a **Administration** > **atualizações e manutenção**.
  2.   No painel de visualização, clique no título de uma das colunas (como **estado**), em seguida, selecione **Guid do pacote** para adicionar essa coluna à apresentação de.
  3.   A coluna mostra agora o GUID do pacote de atualização.

> [!TIP]  
> Para copiar o GUID, selecione a linha para o pacote de atualização que pretende reiniciar e, em seguida, utilize CTRL + C para copiar nessa linha. Se colar sua seleção copiada para um editor de texto, em seguida, pode copiar apenas o GUID para utilização como um parâmetro da linha de comandos ao executar a ferramenta.

### <a name="run-the-tool"></a>Execute a ferramenta    
A ferramenta tem de ser executada no site de nível superior da hierarquia.

Quando executar a ferramenta, utilize os parâmetros da linha de comandos para especificar:
  -   O SQL Server no site de nível superior da hierarquia.
  -   O nome de base de dados do site no site de nível superior.
  -   O GUID do pacote de atualização que pretende repor.

Com base no status da atualização, a ferramenta identifica os servidores adicionais que ela precisa acessar.   

Se o pacote de atualização está numa *publicar download* de estado, a ferramenta não limpe o pacote. Como opção, pode forçar a remoção de uma atualização transferida com êxito ao utilizar o parâmetro de eliminação de força (parâmetros da linha de comandos para o ver mais tarde deste tópico).

Depois da ferramenta é executada:
-   Se um pacote tiver sido eliminado, reinicie o serviço SMS_Executive no site de nível superior. Procurar atualizações, em seguida, para que possa transferir o pacote novamente.
-   Se um pacote não tiver sido eliminado, não é necessário efetuar qualquer ação. A atualização reinicializa e, em seguida, reinicia a instalação ou a replicação.

**Parâmetros da linha de comandos:**  


|                        Parâmetro                         |                                                       Descrição                                                        |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;FQDN do SQL Server do seu site de nível superior >** | *Necessário* <br> Especifique o FQDN do SQL Server que aloja a base de dados do site para o site de nível superior da sua hierarquia. |
|                **-D &lt;nome de base de dados >**                 |                          *Necessário* <br> Especifique o nome da base de dados do site de nível superior.                          |
|                 **-P &lt;GUID do pacote >**                 |                        *Necessário* <br> Especifique o GUID para o pacote de atualização que pretende repor.                        |
|           **-Me &lt;nome da instância do SQL Server >**           |                    *Opcional* <br> Identifica a instância do SQL Server que aloja a base de dados do site.                     |
|                       **-FDELETE**                       |                       *Opcional* <br> Forçar a eliminação de um pacote de atualização transferido com êxito.                        |

 **Exemplos:**  
 Num cenário típico, que pretende repor uma atualização que tem problemas de transferência. É o FQDN de servidores SQL *server1.fabrikam.com*, a base de dados do site é *CM_XYZ*e o pacote GUID é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Execute: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ 61F16B3C-F1F6-4F9F-8647-2A524B0C802C -P***

 Num cenário mais extremo, pretender forçar a eliminação do pacote de atualização problemático. É o FQDN de servidores SQL *server1.fabrikam.com*, a base de dados do site é *CM_XYZ*e o pacote GUID é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Execute: ***CMUpdateReset.exe - FDELETE -S server1.fabrikam.com -D CM_XYZ 61F16B3C-F1F6-4F9F-8647-2A524B0C802C -P***

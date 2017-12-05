---
title: "Ferramenta de reposição de atualização"
titleSuffix: Configuration Manager
description: "Utilize a ferramenta de reposição de atualização para atualizações na consola do System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
caps.latest.revision: "0"
caps.handback.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: cf854b1ea571991c1f070d6b3896db7861fe020f
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="update-reset-tool"></a>Ferramenta de reposição de atualização

*Aplica-se a: O System Center Configuration Manager (ramo atual)*  


Início com versão 1706, sites de administração central e sites primários do Configuration Manager, incluir a atualização de reposição de ferramenta do Configuration Manager, **CMUpdateReset.exe**. Utilize a ferramenta para corrigir os problemas quando as atualizações na consola tem problemas de transferir ou a replicar. A ferramenta se encontra no ***\cd.latest\SMSSETUP\TOOLS*** pasta do servidor do site.

Pode utilizar esta ferramenta com qualquer versão do ramo atual, que permanece no suporte.

Utilize esta ferramenta quando um [atualização na consola](/sccm/core/servers/manage/install-in-console-updates) ainda não instalou e está no estado de falha. Estado de falha significa que a transferência da atualização está em progresso mas bloqueados ou tendo um período de tempo excessivamente longo. Muito tempo é considerado horas mais do que as suas expectativas histórico para os pacotes de atualização do tamanho semelhante. Também pode ser uma falha ao replicar a atualização para sites primários subordinados.  

Quando executar a ferramenta, é executada relativamente a atualização que especificou. Por predefinição, a ferramenta não elimina atualizações instaladas ou transferidas com êxito.  

### <a name="prerequisites"></a>Pré-requisitos
A conta que utiliza para executar a ferramenta requer as seguintes permissões:
-   **Leitura** e **escrever** permissões para a base de dados do site de administração central e cada site primário na sua hierarquia. Para definir estas permissões, pode adicionar a conta de utilizador como membro do **db_datawriter** e **db_datareader** [fixo funções de base de dados](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) na base de dados do Configuration Manager de cada site. A ferramenta não interage com os sites secundários.
-   **Administrador local** no site de nível superior da hierarquia.
-   **Administrador local** no computador que aloja o ponto de ligação de serviço.

É necessário o GUID do pacote de atualização que pretende repor. Para obter o GUID:
  1.   Na consola, aceda a **administração** > **atualizações e manutenção**.
  2.   No painel de visualização, faça duplo clique no cabeçalho de uma das colunas (como **estado**), em seguida, selecione **Guid de pacote** adicionar essa coluna à apresentação de.
  3.   A coluna mostra agora o GUID do pacote de atualização.

> [!TIP]  
> Para copiar o GUID, selecione a linha para o pacote de atualização que pretende repor e, em seguida, utilize CTRL + C para copiar nessa linha. Se colar a seleção copiada para um editor de texto, em seguida, pode copiar apenas o GUID para utilização como um parâmetro de linha de comandos quando executar a ferramenta.

### <a name="run-the-tool"></a>Execute a ferramenta    
A ferramenta tem de ser executada no site de nível superior da hierarquia.

Quando executar a ferramenta, utilize os parâmetros da linha de comandos para especificar:
  -   O SQL Server no site de nível superior da hierarquia.
  -   O nome de base de dados do site no site de nível superior.
  -   O GUID do pacote de atualização que pretende repor.

Com base no estado da atualização, a ferramenta identifica os servidores adicionais, tem de aceder.   

Se o pacote de atualização está a ser um *após a transferência* Estado, a ferramenta de limpeza não configurar o pacote. Como opção, pode forçar a remoção de uma atualização transferida com êxito utilizando o parâmetro de eliminação de imposição (consulte os parâmetros da linha de comandos posteriormente neste tópico).

Depois da ferramenta é executada:
-   Se um pacote foi eliminado, reinicie o serviço SMS_Executive no site de nível superior. Em seguida, verifique a existência de atualizações, pelo que pode transferir o pacote novamente.
-   Se um pacote não foi eliminado, não terá de efetuar qualquer ação. A atualização reinicializa e, em seguida, reinicia a instalação ou a replicação.

**Parâmetros da linha de comandos:**  

| Parâmetro        |Descrição                 |  
|------------------|----------------------------|  
|**-S &lt;FQDN do SQL Server do seu site de nível superior >** | *Necessário* <br> Especifique o FQDN do SQL Server que aloja a base de dados do site para o site de nível superior da hierarquia.    |  
| **-D &lt;nome de base de dados >**                        | *Necessário* <br> Especifique o nome da base de dados no site de nível superior.  |  
| **-P &lt;GUID do pacote >**                         | *Necessário* <br> Especifique o GUID para o pacote de atualização que pretende repor.   |  
| **-I &lt;nome de instância do SQL Server >**             | *Opcional* <br> Identifica a instância do SQL Server que aloja a base de dados do site. |
| **-FDELETE**                              | *Opcional* <br> Forçar a eliminação de um pacote de atualização transferido com êxito. |  
 **Exemplos:**  
 Um cenário típico, que pretende repor uma atualização que tem problemas de transferência. O FQDN de servidores SQL é *server1.fabrikam.com*, a base de dados do site *CM_XYZ*e o pacote GUID é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Execute: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ 61F16B3C-F1F6-4F9F-8647-2A524B0C802C -P***

 Num cenário mais extremos, pretender forçar a eliminação do pacote de atualização problemáticas. O FQDN de servidores SQL é *server1.fabrikam.com*, a base de dados do site *CM_XYZ*e o pacote GUID é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Execute: ***CMUpdateReset.exe - FDELETE -S server1.fabrikam.com -D CM_XYZ 61F16B3C-F1F6-4F9F-8647-2A524B0C802C -P***

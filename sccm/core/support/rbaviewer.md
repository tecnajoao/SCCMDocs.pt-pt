---
title: Ferramenta de administração baseada em funções
titleSuffix: Configuration Manager
description: Utilize a administração baseada em funções e a ferramenta de auditoria para modelar e auditoria de funções de segurança e âmbitos no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 19e0e61681e26a2fc666f67909864ba09b68691d
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39387152"
---
# <a name="role-based-administration-and-auditing-tool"></a>Administração baseada em funções e a ferramenta de auditoria

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A administração baseada em funções e a ferramenta de auditoria é uma da [ferramentas do Configuration Manager](/sccm/core/support/tools). Utilize esta ferramenta para as seguintes tarefas:

- Funções de segurança do modelo com permissões específicas  

- As funções de segurança com outros utilizadores e âmbitos de segurança de auditoria



## <a name="requirements"></a>Requisitos

- Executá-lo no mesmo computador que a consola do Configuration Manager  

- Tem o **administrador total**, **analista só de leitura**, ou **administrador de segurança** função  

- Atribuir a sua conta para o **todos os** âmbito de segurança e todas as coleções  

- (*Opcional*) para analisar a segurança da pasta de relatório, tem de ter acesso SQL  

- (*Opcional*) para analisar a exploração do relatório, executar esta ferramenta no servidor de sistema do site com a função de ponto de reporting



## <a name="procedures"></a>Procedimentos


### <a name="model-permissions-for-a-new-role"></a>Permissões de modelo para uma nova função

Utilize o procedimento seguinte para permissões de modelo para uma nova função que pretende criar: 

1. Execute **RBAViewer.exe**.  

2. Selecione as funções de base de segurança que pretende criar ou iniciar a partir de um conjunto de permissões vazio. Selecione as permissões necessárias.  

3. Clique em **Analyze** ver o esta função personalizada da interface de utilizador irá ver.  

    > [!Note]  
    > Para ver se existe uma função de segurança existente que cumpre os seus requisitos, mude para o **semelhança** separador.  

4. Clique em **exportar** para guardar a função como um arquivo XML. Em seguida, importá-lo na consola do Configuration Manager. Para obter mais informações, consulte [criar funções de segurança personalizadas](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole).


### <a name="audit-existing-security-scopes"></a>Âmbitos de segurança existentes de auditoria

Utilize o procedimento seguinte para auditar todos os utilizadores administrativos existentes, coleções e âmbitos de segurança no Configuration Manager:

1. Execute **RBAViewer.exe**.  

2. Selecione o **RBA de auditoria** botão na barra de ferramentas.  

    1. Para ver as relações de coleção limitado numa exibição em árvore, mude para o **resumo de coleção** separador.  

    2. Para ver o objeto atribuído a uma função de segurança, mude para o **resumo de âmbito** separador.  


### <a name="audit-a-specific-user"></a>Um utilizador específico de auditoria

Utilize o procedimento seguinte para fazer auditoria da configuração de administração baseada em funções para um utilizador específico:

1. Execute **RBAViewer.exe**.  

2. Selecione o **Run** botão na barra de ferramentas.  

3. Introduza o nome de utilizador específico para verificar as permissões para essa conta.  

4. A ferramenta exibe as funções de segurança atribuídas ao utilizador ou grupo de segurança, o utilizador pertence. Ele também apresenta os objetos que este utilizador pode ver e as ações que podem realizar na consola do.  



## <a name="see-also"></a>Consulte também

- [Noções básicas sobre a administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration)
- [Configurar a administração baseada em funções](/sccm/core/servers/deploy/configure/configure-role-based-administration)
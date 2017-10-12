---
title: "Gerir atualização catálogos | Microsoft Docs"
description: "Gerir catálogos de atualização de software para o System Center Updates Publisher"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 887f8029-1a3a-423c-a9c1-31dc0d693386
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 7451d699e0e5e146b0538a57deca595188d113bf
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-software-update-catalogs-in-updates-publisher"></a>Gerir catálogos de atualização de software no publicador de atualizações

*Aplica-se a: O System Center Updates Publisher*

Utilize o **catálogos** **área de trabalho** para gerir catálogos de atualização de software. Isto inclui a adição de catálogos de mercados novo, gestão de subscrições existentes do catálogo e importar informações sobre as atualizações de um catálogo para o repositório do Updates Publisher.

Catálogos de atualização de software contêm informações sobre atualizações relacionadas que são criados por organizações que não sejam Microsoft. Outras organizações incluem a sua própria organização e os fornecedores de software de terceiros que registou as respetivas catálogos com a Microsoft. Catálogos registados fornecedores de software são denominados *parceiro catálogos*. Catálogos que cria e que não estão registados com a Microsoft, são denominados *utilizador* catálogos.

## <a name="add-software-update-catalogs"></a>Adicionar catálogos de atualização de software
Tem de adicionar um catálogo de atualização para o Updates Publisher, antes de poder gerir as atualizações que contém. Quando adiciona um catálogo, o publicador de atualizações:
-   Cria uma subscrição para esse catálogo, pelo que pode procurar atualizações para esse catálogo.
-   Adiciona o catálogo para uma lista no **My catálogos de atualização de Software** janela do **área de trabalho de catálogos**.  

Informações sobre cada subscrito catálogo estão disponíveis na consola do. Informações incluem o URL de transferência ou localização, o nome da empresa ou organização quem criou o catálogo e quando foi efetuada a última importados ou modificado.

Publicador de atualizações automaticamente pode verificar as suas subscrições do alterações sempre que for iniciada. Este é configurado como um [avançadas opção](/sccm/sum/tools/updates-publisher-options#advanced). Quando configurado, o Updates Publisher referencia as informações de URL ou localização de transferência para a subscrição e alertas quando existirem alterações ao catálogo que foram efetuadas desde a última vez importou-lo no repositório.

Para procurar uma atualização de catálogo manualmente, selecione o catálogo do **catálogos de atualização de Software os meus** lista e, em seguida, escolha **atualizar** a partir do Friso.

Para além da adição de catálogos e ver informações sobre catálogos subscritos, pode:
-  **Editar** informações para *utilizador* catálogos.
-  **Eliminar** (remover) um catálogo do Updates Publisher.
-  **Importar** atualizações a partir de um catálogo para o repositório do Updates Publisher. Quando importar atualizações, importar todas as atualizações contidas nesse catálogo. Em seguida, pode ver as atualizações na área de trabalho atualizações onde pode, em seguida, selecione e publicar atualizações para o servidor de atualização.

> [!NOTE]   
> Eliminar um catálogo do Updates Publisher resulta nas atualizações que catálogo a ser removido do seu repositório. Isto não afeta as atualizações que tiver publicado para o servidor de atualização. Para remover as atualizações do seu servidor de atualização que já não estão no seu repositório, consulte [expirar atualizações de software não referenciadas](/sccm/sum/tools/updates-publisher-options#expire-unreferenced-software-updates).

## <a name="manage-update-catalogs"></a>Gerir catálogos de atualização
Pode ver os catálogos de lista que importou no **My catálogos de atualização de Software** janela do **área de trabalho de catálogos**. Esta área de trabalho, pode:

-   **Adicione um catálogo de parceiros:** Utilize um dos seguintes procedimentos para localizar novo catálogos de parceiro:

    -   Na consola, aceda a **área de trabalho atualizações** > **descrição geral**. No **introdução** janela, escolha **adicionar catálogos de atualizações de Software de parceiros**.

    -   Na consola, aceda a **área de trabalho de catálogos** > **catálogos My**. Em seguida, a partir do Friso, escolha **adicionar catálogos**.

-   **Adicione um catálogo de utilizador:** Na consola, aceda a **área de trabalho de catálogos** > **catálogos My**. Em seguida, a partir do Friso, escolha **adicionar catálogos**. Para além da localização do ficheiro. cab, tem de especificar um fabricante, o nome e descrição para identificar o catálogo.


-   **Verificar se existem atualizações para catálogos:** Selecione um ou mais catálogos e, em seguida, escolha **atualizar** a partir do Friso.

-   **Edite um catálogo de utilizador:** Selecione um *utilizador* catálogo e, em seguida, escolha **editar** a partir do Friso. Em seguida, pode modificar as propriedades definidas pelo utilizador.

-   **Elimine catálogos:** Selecione um ou mais catálogos e, em seguida, escolha **remover** a partir do Friso. Esta ação remove o catálogo, a sua subscrição e as atualizações desses catálogos do seu repositório do Updates Publisher.

-   **Adicionar as atualizações a partir de um catálogo para o seu repositório**: Escolha **importação** a partir do friso para iniciar o **importação catálogo** assistente. Para obter mais infomration, consulte [importar atualizações](#import-updates)

## <a name="import-updates"></a>Importar as atualizações
Quando importa um catálogo, Gestor de atualizações adiciona as atualizações do que catálogo para o repositório do Updates Publisher. Depois das atualizações são importadas, pode publicá-los para o servidor de atualização para que fiquem disponíveis para dispositivos geridos.

### <a name="to-import-updates"></a>Para importar as atualizações
1.  Para iniciar o **importação catálogo** assistente, escolha **importação** a partir do Friso de uma das seguintes áreas de trabalho:

    -   Área de trabalho de catálogos

    -   Área de trabalho de atualizações

2.  No **tipo de importação** página, selecione um ou mais catálogos que adicionou ao Updates Publisher ou especifique um caminho para um catálogo ainda não adicionou como uma subscrição. Escolheu **seguinte** para ver o resumo ecrã e, quando está preparado, escolha **seguinte** para iniciar a importação.

3.  No **aviso de segurança-validação de catálogo** janela, reveja o certificado de catálogo e quando pronto, escolha **aceitar** para importar as atualizações.

    > [!CAUTION]    
    > Aceita as atualizações apenas de fabricantes que considera fidedignos. As atualizações de software de fabricantes que não são fidedignas potencialmente podem danificar computadores cliente quando a procura de atualizações.

    >  Se já não confia um fabricante, remova esse fabricante da lista de fabricantes fidedignos. Para obter mais informações sobre a aceitação de catálogos, clique em **informar-Me mais** no **aviso de segurança-validação de catálogo** caixa de diálogo.

    Se optar por sempre aceitar catálogos de um fabricante, esse publicador é adicionado ao [lista fabricantes fidedignos](/sccm/sum/tools/updates-publisher-options#trusted-publishers). Pode rever e editar esta lista como uma opção do Updates Publisher.

4.  Importe ignora a importação de uma atualização, quando a atualização já está a ser o repositório e uma das seguintes opções for verdadeira:

    -   A atualização é inalterada em relação a última vez que foi importada.

    -   A atualização foi editada e tem um novo valor de hash digital. Uma atualização de edição impede que uma nova atualização substituir original como fazê-lo, por isso, substituiria alterações que pode ter implementado.

5.  No **confirmação** página rever os resultados da importação.

6.  Clique em **fechar** para concluir o assistente. Agora, pode ver as atualizações para este catálogo na área de trabalho de atualizações.

## <a name="next-steps"></a>Passos seguintes
Depois de importar atualizações, ações comuns incluem:
-   [Gerir atualizações](/sccm/sum/tools/manage-updates-with-updates-publisher) agrupar, atribuir e implementá-las do servidor de atualização.
-   [Criar regras de aplicabilidade](/sccm/sum/tools/updates-publisher-applicability-rules) para ajudar a determinar quando as atualizações de implementar o servidor de atualização.

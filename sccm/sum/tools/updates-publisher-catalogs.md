---
title: "Gerir atualização catálogos | Documentos do Microsoft"
description: "Gerir catálogos de atualização de software para o publicador de atualizações do System Center"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 887f8029-1a3a-423c-a9c1-31dc0d693386
caps.latest.revision: 1
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.translationtype: Machine Translation
ms.sourcegitcommit: 31819a1df4e63e1114682490a9b3c3b4e5c99cfa
ms.openlocfilehash: 7451d699e0e5e146b0538a57deca595188d113bf
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="manage-software-update-catalogs-in-updates-publisher"></a>Gerir catálogos de atualização de software no Publisher atualizações

*Aplica-se a: System Center Updates Publisher*

Utilize o **catálogos** **área de trabalho** para gerir catálogos de atualização de software. Isto inclui adicionar novo catálogos, gerir subscrições de catálogo existentes e importar informações sobre as atualizações a partir de um catálogo para o repositório do Updates Publisher.

Catálogos de atualização de software contêm informações sobre atualizações relacionadas que são criados por organizações diferente da Microsoft. Outras organizações incluem as suas próprias organização e fornecedores de software de terceiros que registou o respetivo catálogos com a Microsoft. Registado catálogos a partir de fornecedores de software são denominados *catálogos do parceiro*. Catálogos que cria e que não estiverem registados com a Microsoft, são chamados *utilizador* catálogos.

## <a name="add-software-update-catalogs"></a>Adicionar catálogos de atualização de software
Tem de adicionar um catálogo de atualização para o Updates Publisher, antes de poder gerir as atualizações que contém. Quando adiciona um catálogo, Updates Publisher:
-   Cria uma subscrição que catálogo, pelo que pode verificar a existência de atualizações a esse catálogo.
-   Adiciona o catálogo para uma lista no **meu catálogos de atualização de Software** janela do **catálogos de área de trabalho**.  

Informações sobre cada catálogo subscrito estão disponíveis na consola. Informações incluem o URL de transferência ou localização, o nome da empresa ou organização quem criou o catálogo e quando foi importado ou modificado.

Updates Publisher pode verificar automaticamente as suas subscrições para alterações sempre que é iniciado. Isto é configurado como um [opção avançada](/sccm/sum/tools/updates-publisher-options#advanced). Quando configurado, o Updates Publisher referencia as informações de URL ou localização de transferência para a subscrição e os alertas quando existirem alterações para o catálogo que foram efetuadas desde a última vez importou-lo para o repositório.

Para verificar manualmente uma atualização do catálogo, selecione o catálogo a partir do **catálogos de atualização de Software meus** lista e, em seguida, escolha **atualizar** a partir do Friso.

Para além da adição de catálogos e ver informações sobre catálogos subscritos, pode:
-  **Editar** relativas *utilizador* catálogos.
-  **Eliminar** (remova) um catálogo do Updates Publisher.
-  **Importar** atualizações a partir de um catálogo para o repositório do Updates Publisher. Ao importar as atualizações, importar todas as atualizações contidas nesse catálogo. Em seguida, pode ver as atualizações na área de trabalho atualizações onde pode, em seguida, selecione e publicar as atualizações para o seu servidor de atualização.

> [!NOTE]   
> Eliminar um catálogo do Updates Publisher resulta nas atualizações no catálogo de que a ser removido do seu repositório. Isto não afeta as atualizações que tiver publicado para o seu servidor de atualização. Para remover as atualizações a partir do seu servidor de atualização que já não se encontram no seu repositório, consulte o artigo [expirar atualizações de software não referenciadas](/sccm/sum/tools/updates-publisher-options#expire-unreferenced-software-updates).

## <a name="manage-update-catalogs"></a>Gerir catálogos de atualização
Pode ver os catálogos de lista que importou no **meu catálogos de atualização de Software** janela do **catálogos de área de trabalho**. Esta área de trabalho, pode:

-   **Adicione um catálogo de parceiro:** Utilize um dos seguintes procedimentos para localizar novo catálogos de parceiro:

    -   Na consola, vá para **área de trabalho atualizações** > **descrição geral**. No **introdução** janela, escolha **adicionar catálogos de atualizações de Software de parceiros**.

    -   Na consola, vá para **catálogos de área de trabalho** > **catálogos meu**. Em seguida, no Friso, selecione **adicionar catálogos**.

-   **Adicione um catálogo de utilizador:** Na consola, vá para **catálogos de área de trabalho** > **catálogos minhas**. Em seguida, no Friso, selecione **adicionar catálogos**. Além da localização do ficheiro. cab, tem de especificar um publicador, nome e descrição para identificar o catálogo.


-   **Verifique se existem atualizações para catálogos:** Selecione um ou mais catálogos e, em seguida, escolha **atualizar** a partir do Friso.

-   **Edite um catálogo de utilizador:** Selecione um *utilizador* de catálogo e, em seguida, escolha **editar** a partir do Friso. Em seguida, pode modificar as propriedades definidas pelo utilizador.

-   **Elimine catálogos:** Selecione um ou mais catálogos e, em seguida, escolha **remover** a partir do Friso. Esta ação remove o catálogo, a sua subscrição e as atualizações a partir desses catálogos do seu repositório do Updates Publisher.

-   **Adicionar atualizações a partir de um catálogo para o seu repositório**: Escolher **importação** a partir do friso para iniciar o **importação catálogo** assistente. Para obter mais infomration, consulte o artigo [importar atualizações](#import-updates)

## <a name="import-updates"></a>Importar atualizações
Quando importa um catálogo, o Gestor de atualizações adiciona as atualizações do que catálogo para o repositório do Updates Publisher. Depois de importar as atualizações, pode publicá-los ao seu servidor de atualização para que fiquem disponíveis para dispositivos geridos.

### <a name="to-import-updates"></a>Para importar as atualizações
1.  Para iniciar o **importação catálogo** assistente, selecione **importação** no Friso de uma das seguintes áreas de trabalho:

    -   Área de trabalho de catálogos

    -   Área de trabalho atualizações

2.  No **tipo de importação** página, selecione um ou mais catálogos que adicionou ao Updates Publisher ou especifique um caminho para um catálogo que ainda não adicionados como uma subscrição. Escolheu **seguinte** para ver o ecrã de resumo e, quando está preparado, escolha **seguinte** para começar a importar.

3.  No **aviso de segurança-validação de catálogo** janela, reveja o certificado de catálogo e quando está preparado, escolher **aceitar** para importar as atualizações.

    > [!CAUTION]    
    > Aceite as atualizações apenas a partir de fabricantes que confia. Atualizações de software a partir de fabricantes que não são fidedignos potencialmente podem danificar computadores cliente quando a análise de atualizações.

    >  Se já não confia um fabricante, remova esse fabricante da lista fabricantes fidedignos. Para obter mais informações sobre aceitar catálogos, clique em **informar-Me mais** no **aviso de segurança-validação de catálogo** caixa de diálogo.

    Se optar por aceitar sempre catálogos de um fabricante, esse publisher é adicionada para o [lista fabricantes fidedignos](/sccm/sum/tools/updates-publisher-options#trusted-publishers). Pode rever e editar esta lista como uma opção de Updates Publisher.

4.  Importe ignora a importação de uma atualização durante a atualização já existe no repositório e um dos seguintes é verdadeiro:

    -   A atualização é inalterados desde a última vez que foi importado.

    -   A atualização foi editada e tem um novo hash digital. Editar uma atualização impede que uma nova atualização substituir o original como fazer irá substituir as alterações que tiver implementado.

5.  No **confirmação** página rever os resultados de importação.

6.  Clique em **fechar** para concluir o assistente. Agora pode ver as atualizações para este catálogo na área de trabalho de atualizações.

## <a name="next-steps"></a>Passos seguintes
Depois de importar as atualizações, ações comuns incluem:
-   [Gerir atualizações](/sccm/sum/tools/manage-updates-with-updates-publisher) agrupar, atribuir e implementá-las do servidor de atualização.
-   [Criar regras de aplicabilidade](/sccm/sum/tools/updates-publisher-applicability-rules) para ajudar a determinar quando a implementação das atualizações para o seu servidor de atualização.


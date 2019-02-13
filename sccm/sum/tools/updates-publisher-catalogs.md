---
title: Gerir catálogos de atualizações
titleSuffix: Configuration Manager
description: Gerir catálogos de atualizações de software para o System Center Updates Publisher
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 887f8029-1a3a-423c-a9c1-31dc0d693386
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 383cd0aaa8e20613cdef0009c95aa44c6b1117f1
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156496"
---
# <a name="manage-software-update-catalogs-in-updates-publisher"></a>Gerir catálogos de atualizações de software Updates Publisher

*Aplica-se a: System Center Updates Publisher*

Utilize o **catálogos** **área de trabalho** para gerir catálogos de atualizações de software. Isto inclui a adição de catálogos de novo, gestão de subscrições existentes do catálogo e importar informações sobre as atualizações a partir de um catálogo para o repositório do Updates Publisher.

Catálogos de atualizações de software contêm informações sobre atualizações relacionadas que são criados por organizações que não seja Microsoft. Outras organizações incluem sua própria organização e os fornecedores de software de terceiros que registou seus catálogos com a Microsoft. Registado catálogos de fornecedores de software são chamados *catálogos de parceiros*. Catálogos de que cria e que não estão registados com a Microsoft, são chamados *utilizador* catálogos.

## <a name="add-software-update-catalogs"></a>Adicionar catálogos de atualizações de software
Tem de adicionar um catálogo de atualização para o Updates Publisher, antes de poder gerir as atualizações que ele contém. Quando adiciona um catálogo, o Updates Publisher:
-   Cria uma subscrição para esse catálogo, portanto, pode verificar a existência de atualizações a esse catálogo.
-   Adiciona o catálogo para uma lista no **My catálogos de atualizações de Software** janela da **catálogos de área de trabalho**.  

Informações sobre cada subscrito catálogo estão disponíveis na consola do. Informações incluem o URL de transferência ou localização, o nome da empresa ou organização quem criou o catálogo e, quando era última importados ou modificado.

Publicador de atualizações automaticamente pode verificar as suas subscrições para alterações toda vez que iniciar. Este é configurado como um [opções avançadas](/sccm/sum/tools/updates-publisher-options#advanced). Quando configurado, o Updates Publisher referencia as informações de URL ou localização de transferência de subscrição e alertas quando existirem alterações para o catálogo que foram feitas desde a última vez que importou-lo para o repositório.

Para verificar manualmente uma atualização de catálogo, selecione o catálogo do **catálogos de atualização de Software My** lista e, em seguida, escolha **atualizar** a partir do Friso.

Além de adicionar catálogos e ver informações sobre catálogos subscritos, pode:
-  **Editar** informações para *utilizador* catálogos.
-  **Eliminar** (remover) um catálogo do Updates Publisher.
-  **Importar** atualizações a partir de um catálogo para o repositório do Updates Publisher. Ao importar as atualizações, importar todas as atualizações contidas nesse catálogo. Em seguida, pode ver as atualizações na área de trabalho atualizações em que pode, em seguida, selecionar e publicar atualizações ao seu servidor de atualização.

> [!NOTE]   
> Eliminar um catálogo do Updates Publisher faz as atualizações nesse catálogo a ser removido do seu repositório. Isto não afeta as atualizações que publica para o seu servidor de atualização. Para remover as atualizações do seu servidor de atualização que já não estão no seu repositório, consulte [expirar atualizações de software não referenciados](/sccm/sum/tools/updates-publisher-options#expire-unreferenced-software-updates).

## <a name="manage-update-catalogs"></a>Gerir catálogos de atualizações
Pode ver os catálogos de lista que importou na **My catálogos de atualizações de Software** janela da **catálogos de área de trabalho**. Esta área de trabalho, pode:

-   **Adicione um catálogo de parceiro:** Utilize um dos seguintes procedimentos para encontrar novos catálogos de parceiros:

    -   Na consola, aceda a **área de trabalho de atualizações** > **descrição geral**. Na **introdução** janela, escolha **adicionar catálogos de atualizações de Software de parceiros**.

    -   Na consola, aceda a **catálogos de área de trabalho** > **catálogos My**. Em seguida, no Friso e escolha **catálogos adicionar**.

-   **Adicione um catálogo de utilizador:** Na consola, aceda a **catálogos de área de trabalho** > **catálogos My**. Em seguida, no Friso e escolha **catálogos adicionar**. Além da localização do ficheiro. cab, tem de especificar um publicador, nome e descrição para identificar o catálogo.


-   **Verifique se existem atualizações para catálogos:** Selecione um ou mais catálogos e, em seguida, escolha **atualizar** a partir do Friso.

-   **Edite um catálogo de utilizador:** Selecione um *usuário* catálogo e, em seguida, escolha **editar** a partir do Friso. Em seguida, pode modificar as propriedades definidas pelo utilizador.

-   **Elimine catálogos:** Selecione um ou mais catálogos e, em seguida, escolha **remover** a partir do Friso. Esta ação remove o catálogo, a sua subscrição e as atualizações desses catálogos do seu repositório do Updates Publisher.

-   **Adicionar atualizações a partir de um catálogo para o seu repositório**: Escolher **importação** a partir do friso para iniciar o **importação catálogo** assistente. Para mais obter mais informações, consulte [importar as atualizações](#import-updates)

## <a name="import-updates"></a>Importar as atualizações
Quando importa um catálogo, o Gerenciador de atualizações adiciona as atualizações desse catálogo para o repositório do Updates Publisher. Depois das atualizações são importadas, pode publicá-las ao seu servidor de atualização para que fiquem disponíveis para dispositivos geridos.

### <a name="to-import-updates"></a>Para importar as atualizações
1. Para iniciar o **catálogo de importação** assistente, escolha **importação** da faixa de opções em uma das seguintes áreas de trabalho:

   -   Área de trabalho de catálogos

   -   Área de trabalho atualizações

2. Sobre o **tipo de importação** página, selecione um ou mais catálogos adicionar para o Updates Publisher ou especifique um caminho para um catálogo, ainda não tiver adicionado como uma assinatura. Escolheu **próxima** para ver a tela de resumo e, quando pronto, escolha **próxima** para iniciar a importação.

3. Sobre o **aviso de segurança – validação do catálogo** janela, reveja o certificado de catálogo e, quando pronto, escolha **Accept** para importar as atualizações.

   > [!CAUTION]
   > Aceita as atualizações apenas a partir de editores que confia. Atualizações de software dos publicadores que não são fidedignos podem danificar computadores cliente quando a análise de atualizações.
   > 
   >  Se confiar já não é um publicador, remova esse editor da lista de fabricantes fidedignos. Para obter mais informações sobre abertos ao recebimento de catálogos, clique em **informar-Me mais** no **aviso de segurança – validação de catálogo** caixa de diálogo.

   Se optar por aceitar sempre a catálogos de um editor, esse editor é adicionada para o [lista de fabricantes fidedignos](/sccm/sum/tools/updates-publisher-options#trusted-publishers). Pode rever e editar esta lista como uma opção do Updates Publisher.

4. Importe ignora a importação de uma atualização, quando a atualização já está no repositório e uma das seguintes opções for verdadeira:

   -   A atualização é inalterada em relação a última vez que foi importado.

   -   A atualização foi editada e tem um novo hash digital. Uma atualização de edição impede que uma nova atualização substituir o original, como o fazer seria substituir as alterações que deve ter implantado.

5. Sobre o **confirmação** página rever os resultados da importação.

6. Clique em **fechar** para concluir o assistente. Agora pode ver as atualizações para este catálogo na área de trabalho de atualizações.

## <a name="next-steps"></a>Passos seguintes
Depois de importar as atualizações, as ações comuns incluem:
-   [Gerir atualizações](/sccm/sum/tools/manage-updates-with-updates-publisher) agrupar, atribuir e implementá-las seu servidor de atualização.
-   [Criar regras de aplicabilidade](/sccm/sum/tools/updates-publisher-applicability-rules) para ajudar a determinar quando as atualizações de implementar no seu servidor de atualização.

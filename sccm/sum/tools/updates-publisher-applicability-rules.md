---
title: As regras de aplicabilidade | Microsoft Docs
description: Gerir as regras de aplicabilidade para o System Center Updates Publisher
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cf0c2cd-397a-4622-b11c-961f334fb7d7
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 2925abda07abaa46ad56b9b433ce003c22aede5e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-applicability-rules-in-updates-publisher"></a>Gerir as regras de aplicabilidade Updates Publisher

*Aplica-se a: O System Center Updates Publisher*

Com o Updates Publisher, as regras de aplicabilidade definem os requisitos que têm de ser cumpridos antes de um dispositivo pode instalar uma atualização. As regras também são utilizadas para determinar se o computador tem uma atualização instalada. Uma regra de aplicabilidade é complexa com várias partes é referida como uma regra de definida.

Os pacotes de atualizações não utilizam as regras de aplicabilidade.

## <a name="overview-of-applicability-rules"></a>Descrição geral das regras de aplicabilidade
Gerir as regras de aplicabilidade do **regras de área de trabalho**. Quando cria uma regra, especifica uma ou mais condições. Quando são especificadas várias condições, pode configurar as relações entre as condições, de modo a serem avaliados sequencialmente ou combinados lógica **e** ou **ou** instruções.

Por exemplo, o seguinte é um conjunto de regras que contém três regras. A primeira regra verifica se o *MyFile* ficheiro existe e as regras de segunda e terceira Certifique-se de que o idioma do sistema operativo Windows inglês ou japonês.

    And  
      File ‘\[PROGRAM\_FILES\] \\Microsoft\\MyFile’ exists  
      Or  
        Windows Language is English   
        Windows Language is Japanese

Todas as atualizações requerem, pelo menos, uma regra de aplicabilidade. Atualizações que importar já tem regras de aplicabilidade aplicadas e quando criar as suas próprias atualizações, tem de adicionar uma ou mais regras aos mesmos. Pode modificar e expanda nas regras de qualquer atualização numa Updates Publisher.

Para ver as regras que criou, no **regras de área de trabalho**, selecione uma regra do **meu regras guardadas** lista. As condições individuais e lógicas operações dessa regra apresentam o **as regras de aplicabilidade** painel da consola. Regras para as atualizações que importar apenas podem ser visualizadas e modificadas quando edita essa atualização.

Pode criar regras em duas localizações no publicador de atualizações:

-   No **área de trabalho de regras,** cria e **guardar** define a regra que pode utilizar mais tarde. Ao editar ou criar uma atualização, pode selecionar **guardado regra** como o **tipo de regra**e, em seguida, selecione de uma lista dos seus conjuntos de regras previamente criada.

-   Também pode criar novas regras no momento em que pode criar ou editar uma atualização. Regras que cria desta forma, não são guardadas para utilização futura.

## <a name="create-applicability-rule"></a>Criar regra de aplicabilidade
As seguintes informações são semelhantes à forma como as regras a partir do [assistente criar atualizar](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard). Mas, ao contrário do assistente, tem a opção para guardar os conjuntos de regras para utilização futura.

1.  No **regras de área de trabalho**, escolha **criar** para abrir o **criar regra** assistente.

2.  Especifique um nome para a regra e, em seguida, clique em ![nova regra](media/newrule.png). Esta ação abre o **regra de aplicabilidade** página onde pode configurar as regras.

3.  Para **tipo, de regra** selecione um dos seguintes. As opções que tem de configurar variam para cada tipo:

    -   **Ficheiro** – utilizar esta regra para exigir que um dispositivo tem um ficheiro com propriedades que cumprem um ou mais critérios que especificar antes desta atualização podem ser aplicados.

    -   **Registo –** utilizar este tipo para especificar detalhes de registo que tem de existir antes de um dispositivo se qualificam instalar esta atualização.

    -   **Sistema –** esta regra utiliza detalhes de sistema para determinar a aplicabilidade. Pode escolher entre definir uma versão do Windows, um idioma do Windows, a arquitetura de processador ou especificar uma consulta WMI para identificar o sistema operativo de dispositivos.

    -   **Windows Installer –** utilizar este tipo de regra para determinar a aplicabilidade com base num instalado. MSI ou do Windows Installer patch (.MSP). Também pode determinar se os componentes específicos ou funcionalidades são instaladas como parte do requisito.

       > [!IMPORTANT]   
       > No geridos deices, o Windows Update Agent não conseguiu detetar o Windows instalar pacotes que são instaladas por utilizador. Quando utilizar este tipo de regra, configure as regras de aplicabilidade adicionais, como as versões de ficheiro ou valores de chave de registo, para que o pacote Windows Installer pode ser detetado corretamente independentemente numa base por utilizador ou por sistema.

    -   **Guardar a regra –** esta opção permite-lhe localizar e utilizar as regras que configurou anteriormente e foram guardadas.

4.  Continue a adicionar e configurar regras adicionais conforme pretendido.

5.  Utilize os botões de funcionamento lógico para ordenação e grupo de regras diferentes para criar as verificações de pré-requisitos mais complexas.

6.  Quando o conjunto de regras estiver concluído, clique em **OK** para guardá-lo. A regra que defina agora aparece no **meu regras guardadas** lista.

## <a name="edit-applicability-rule-sets"></a>Editar os conjuntos de regras de aplicabilidade
Para editar uma regra de aplicabilidade, no **regras de área de trabalho** Selecione qualquer regra que é guardada no **meu regras guardadas** lista e, em seguida, escolha **editar** a partir do Friso. Esta ação abre o **Editar regra de** assistente.

O **Editar regra de** assistente apresenta as regras atuais para o conjunto de regras. Editar as regras da mesma forma como utiliza o **criar regra** Assistente para criar novas regras. Pode utilizar este assistente para mudar o nome do conjunto de regras e eliminar regras, reordenar as regras e as relações ou adicionar novas regras.

Depois de efetuar alterações, escolha **OK** para guardar as alterações e fechar o assistente.

Para obter mais detalhes sobre como utilizar o Assistente de regra, consulte **passo 7**, a página de aplicabilidade, do [assistente criar atualizar](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard).

## <a name="delete-applicability-rules"></a>Eliminar as regras de aplicabilidade
Para eliminar uma regra de aplicabilidade guardado no **regras de área de trabalho** selecione a regra ou um conjunto a partir de regras a **meu regras guardadas** lista e, em seguida, escolha **eliminar** a partir do Friso. Esta ação remove a regra guardada ou a regra que defina do Updates Publisher.

Para eliminar uma regra a partir de uma atualização específica, tem de [editar a atualização](/sccm/sum/tools/manage-updates-with-updates-publisher#edit-updates-and-bundles).

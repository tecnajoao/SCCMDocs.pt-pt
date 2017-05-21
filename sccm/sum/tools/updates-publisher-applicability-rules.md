---
title: As regras de aplicabilidade | Documentos do Microsoft
description: Gerir regras de aplicabilidade para o System Center Updates Publisher
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cf0c2cd-397a-4622-b11c-961f334fb7d7
caps.latest.revision: 1
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.translationtype: Machine Translation
ms.sourcegitcommit: 31819a1df4e63e1114682490a9b3c3b4e5c99cfa
ms.openlocfilehash: 2925abda07abaa46ad56b9b433ce003c22aede5e
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---

# <a name="manage-applicability-rules-in-updates-publisher"></a>Gerir regras de aplicabilidade no Updates Publisher

*Aplica-se a: System Center Updates Publisher*

Com o Updates Publisher, as regras de aplicabilidade definem requisitos que devem ser satisfeitos antes de um dispositivo pode instalar uma atualização. As regras também são utilizadas para determinar se o computador tem uma atualização instalada. Uma regra de aplicabilidade é complexa com várias partes é referida como uma regra definida.

Os pacotes de atualização que não utiliza as regras de aplicabilidade.

## <a name="overview-of-applicability-rules"></a>Descrição geral das regras de aplicabilidade
Gerir regras de aplicabilidade do **regras de área de trabalho**. Quando cria uma regra, especifica um ou mais condições. Quando são especificadas várias condições, pode configurar relações entre as condições, de modo a serem avaliados sequencialmente ou combinados lógica **e** ou **ou** instruções.

Por exemplo, segue-se um conjunto de regras que contém três regras. A primeira regra verifica se o *MyFile* ficheiro existe e as regras de segunda e terceira Verifique se o idioma do sistema operativo Windows em inglês ou japonês.

    And  
      File ‘\[PROGRAM\_FILES\] \\Microsoft\\MyFile’ exists  
      Or  
        Windows Language is English   
        Windows Language is Japanese

Todas as atualizações necessitam de pelo menos uma regra de aplicabilidade. Atualizações que importar já tem aplicadas as regras de aplicabilidade e ao criar as suas próprias atualizações, terá de adicionar uma ou mais regras às mesmas. Pode modificar e expandir nas regras para qualquer atualização no Publisher atualizações.

Para regras de vista que criou, no **regras de área de trabalho**, selecione uma regra a partir do **meu regras guardadas** lista. As condições individuais e operações lógicas dessa regra apresentam o **as regras de aplicabilidade** painel da consola. Regras para as atualizações que importar só podem ser visualizadas e modificadas quando edita que update.

Pode criar regras em duas localizações no Updates Publisher:

-   No **regras de área de trabalho,** cria e **guardar** regra define o que pode, em seguida, utilizar mais tarde. Quando editar ou criar uma atualização pode selecionar **guardados regra** como o **regra tipo**e, em seguida, selecione a partir de uma lista dos seus conjuntos de regras previamente criada.

-   Também pode criar novas regras no momento em que cria ou edita uma atualização. Regras que criar desta forma não são guardadas para utilização futura.

## <a name="create-applicability-rule"></a>Criar regra de aplicabilidade
As seguintes informações são semelhantes a como criar regras a partir do [assistente criar atualizar](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard). Mas, ao contrário do assistente, tem a opção para guardar os seus conjuntos de regras para utilização futura.

1.  No **regras de área de trabalho**, escolha **criar** para abrir o **criar regra** assistente.

2.  Especifique um nome para a regra e, em seguida, clique em ![nova regra](media/newrule.png). Esta ação abre o **aplicabilidade regra** página onde pode configurar as regras.

3.  Para **regra tipo,** selecione um dos seguintes procedimentos. As opções que tem de configurar variam para cada tipo:

    -   **Ficheiro** – Utilize esta regra para realizar um dispositivo tem de ter um ficheiro com propriedades que correspondam a um ou mais critérios especificados por si antes desta atualização podem ser aplicados.

    -   **Registo –** Utilize este tipo para especificar os detalhes de registo que tem de existir antes de um dispositivo está qualificada para instalar esta atualização.

    -   **Sistema –** esta regra utiliza detalhes de sistema para determinar a aplicabilidade. Pode escolher entre definir uma versão do Windows, um idioma do Windows, a arquitetura do processador ou especificar uma consulta WMI para identificar o sistema operativo de dispositivos.

    -   **Windows Installer –** utilizar este tipo de regra para determinar a aplicabilidade com base num instalado. MSI ou do Windows Installer patch (. MSP). Pode também determinar se específico componentes ou funcionalidades são instaladas como parte do requisito.

       > [!IMPORTANT]   
       > No geridos deices, o Windows Update Agent não consegue detetar Windows instalar pacotes que são instalados por utilizador. Quando utiliza este tipo de regra, configure as regras de aplicabilidade adicionais, como versões de ficheiro ou valores de chave de registo, para que o pacote Windows Installer pode ser detetado corretamente independentemente numa base por utilizador ou por sistema.

    -   **Regra – guardada** esta opção permite-lhe encontrar e utilizar as regras que tenha configurado anteriormente e guardado.

4.  Continue a adicionar e configurar regras adicionais conforme pretender.

5.  Utilize os botões de operação lógica para ordem e grupo regras diferentes para criar mais complexas verificações de pré-requisitos.

6.  Quando o conjunto de regras estiver concluído, clique em **OK** guardá-lo. A regra definida agora aparece no **meu regras guardadas** lista.

## <a name="edit-applicability-rule-sets"></a>Editar os conjuntos de regras de aplicabilidade
Para editar uma regra de aplicabilidade, no **regras de área de trabalho** Selecione qualquer regra que é guardada no **meu regras guardadas** lista e, em seguida, selecione **editar** a partir do Friso. Esta ação abre o **Editar regra** assistente.

O **Editar regra** assistente apresenta as regras atuais para o conjunto de regras. Editar regras da mesma forma como utiliza o **criar regra** Assistente para criar novas regras. Pode utilizar este assistente para o conjunto de regras de mudar o nome, eliminar regras, reordenar regras e as relações ou adicionar novas regras.

Depois de efetuar alterações, escolher **OK** para guardar as alterações e fechar o assistente.

Para obter mais detalhes sobre como utilizar o Assistente de regra, consulte o artigo **passo 7**, a página de aplicabilidade, da [assistente criar atualizar](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard).

## <a name="delete-applicability-rules"></a>Eliminar as regras de aplicabilidade
Para eliminar uma regra de aplicabilidade guardado, no **regras de área de trabalho** selecione a regra ou conjunto a partir de regras de **meu regras guardadas** lista e, em seguida, selecione **eliminar** a partir do Friso. Esta ação remove o regra guardada ou a regra definida a partir do Updates Publisher.

Para eliminar uma regra a partir de uma atualização específica, tem [editar a atualização](/sccm/sum/tools/manage-updates-with-updates-publisher#edit-updates-and-bundles).


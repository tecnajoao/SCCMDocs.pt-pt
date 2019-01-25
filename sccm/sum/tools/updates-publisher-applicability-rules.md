---
title: Regras de aplicabilidade
titleSuffix: Configuration Manager
description: Gerir regras de aplicabilidade para o System Center Updates Publisher
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 3cf0c2cd-397a-4622-b11c-961f334fb7d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 923329091e24505832af359c4486ec8686903527
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897581"
---
# <a name="manage-applicability-rules-in-updates-publisher"></a>Gerir regras de aplicabilidade em Updates Publisher

*Aplica-se a: System Center Updates Publisher*

Com o Updates Publisher, as regras de aplicabilidade definem requisitos que têm de ser cumpridos antes de um dispositivo pode instalar uma atualização. As regras também são usadas para determinar se o computador tem uma atualização instalada. Uma regra de aplicabilidade complexa com várias partes é referida para como uma regra de definir.

Os pacotes de atualizações não utilize as regras de aplicabilidade.

## <a name="overview-of-applicability-rules"></a>Descrição geral das regras de aplicabilidade
Gerir regras de aplicabilidade dos **regras de área de trabalho**. Quando cria uma regra, que está a especificar uma ou mais condições. Quando são especificadas várias condições, pode configurar as relações entre as condições para que eles são avaliados sequencialmente ou combinados em lógica **e** ou **ou** instruções.

Por exemplo, segue-se um conjunto de regras que contém três regras. A primeira regra verifica se o *MyFile* ficheiro existe e as regras de segunda e terceira Certifique-se de que o idioma do sistema operacional Windows é o inglês ou o japonês.

    And  
      File ‘\[PROGRAM\_FILES\] \\Microsoft\\MyFile’ exists  
      Or  
        Windows Language is English   
        Windows Language is Japanese

Todas as atualizações necessitam de pelo menos uma regra de aplicabilidade. Atualizações a que importar já tem aplicadas as regras de aplicabilidade e ao criar suas próprias atualizações, tem de adicionar uma ou mais regras para eles. Pode modificar e expandir as regras para qualquer atualização no Updates Publisher.

Para ver as regras que criou, além da **regras de área de trabalho**, selecione uma regra do **minhas regras de guardado** lista. As condições individuais e operações lógicas para essa regra apresentam a **regras de aplicabilidade** painel da consola. Regras para as atualizações que importar apenas podem ser visualizadas e modificadas quando editar essa atualização.

Pode criar regras em duas localizações no publicador de atualizações:

-   Na **regras de área de trabalho** cria e **guardar** conjuntos de regras que pode, em seguida, utilizar mais tarde. Quando editar ou criar uma atualização pode selecionar **regra guardado** como o **tipo de regra**e, em seguida, selecione uma lista de seus conjuntos de regras previamente criada.

-   Também pode criar novas regras no momento em que cria ou edita uma atualização. Regras criadas desta forma, não são guardadas para utilização futura.

## <a name="create-applicability-rule"></a>Criar regra de aplicabilidade
As seguintes informações são semelhantes a como criar regras de dentro do [Assistente de atualização de criar](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard). Mas, Diferentemente do assistente, tem a opção para guardar os seus conjuntos de regras para utilização futura.

1. No **regras de área de trabalho**, escolha **Create** para abrir o **criar regra** assistente.

2. Especifique um nome para a regra e, em seguida, clique em ![nova regra](media/newrule.png). Esta ação abre o **regra de aplicabilidade** página onde pode configurar regras.

3. Para **tipo, de regra** selecione um dos seguintes. As opções que tem de configurar variam para cada tipo:

   - **Ficheiro** – utilizar esta regra para exigir que um dispositivo tiver um ficheiro com propriedades corresponderem a uma ou mais critérios que especificar antes desta atualização podem ser aplicados.

   - **Registo –** usar esse tipo para especificar os detalhes de registo que tem de estar presentes antes de um dispositivo é elegível instalar esta atualização.

   - **Sistema –** esta regra utiliza detalhes de sistema para determinar a aplicabilidade. Pode escolher entre definir uma versão do Windows, um idioma do Windows, a arquitetura do processador, ou especificar uma consulta WMI para identificar o sistema operativo de dispositivos.

   - **Windows Installer –** utilizar este tipo de regra para determinar a aplicabilidade com base num instalado. MSI ou do Windows Installer patch (.MSP). Também pode determinar se os componentes específicos ou funcionalidades são instaladas como parte do requisito.

     > [!IMPORTANT]   
     > No managed deices, o Windows Update Agent não consegue detetar a pacotes de instalação do Windows de mensagens em fila que são instalados por utilizador. Quando utiliza este tipo de regra, configure regras de aplicabilidade adicionais, como versões de ficheiro ou valores de chave de registo, para que o pacote do Windows Installer pode ser detectado corretamente independentemente numa base por usuário ou por sistema.

   - **Guardar a regra –** esta opção permite-lhe localizar e utilizar as regras que tiver configurado e guardado.

4. Continue a adicionar e configurar regras adicionais conforme pretendido.

5. Utilize os botões de operação lógica para a ordem e grupo de regras diferentes para criar as verificações de pré-requisitos mais complexas.

6. Quando o conjunto de regras é concluído, clique em **OK** salvá-lo. A regra que defina agora aparece na **minhas regras de guardado** lista.

## <a name="edit-applicability-rule-sets"></a>Editar conjuntos de regras de aplicabilidade
Para editar uma regra de aplicabilidade, na **regras de área de trabalho** Selecione qualquer regra que é guardada na **minhas regras de guardado** lista e, em seguida, escolha **editar** a partir do Friso. Esta ação abre o **Editar regra de** assistente.

O **Editar regra de** assistente apresenta as regras atuais para o conjunto de regras. Editar regras da mesma forma que utiliza a **criar regra** Assistente para criar novas regras. Pode utilizar este assistente para mudar o nome do conjunto de regras, eliminar as regras, reordenar regras e as relações ou adicionar novas regras.

Depois de efetuar alterações, escolha **OK** para guardar as alterações e fechar o assistente.

Para obter mais detalhes sobre como utilizar o Assistente de regra, consulte **passo 7**, a página de aplicabilidade, da [Assistente de atualização de criar](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard).

## <a name="delete-applicability-rules"></a>Eliminar regras de aplicabilidade
Para eliminar uma regra de aplicabilidade guardado, na **regras de área de trabalho** selecione a regra ou um conjunto a partir de regras a **minhas regras de guardado** lista e, em seguida, escolha **eliminar** a partir do Friso. Esta ação remove a regra guardada ou definir do publicador de atualizações.

Para eliminar uma regra de uma atualização específica, terá [editar a atualização](/sccm/sum/tools/manage-updates-with-updates-publisher#edit-updates-and-bundles).

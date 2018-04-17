---
title: Configurar o Android para aplicações de trabalho com políticas de configuração de aplicação
titleSuffix: Configuration Manager
description: Ajude a eliminar os problemas de configuração em dispositivos com Android para trabalho ao implementar políticas de configuração de aplicação para os utilizadores antes de poderem executam as aplicações.
ms.custom: na
ms.date: 09/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9126d188-7780-45a4-b21d-7fcf4fad7da2
caps.latest.revision: 0
caps.handback.revision: 0
author: NathBarn
ms.author: NathBarn
manager: angrobe
ms.openlocfilehash: 0b1d4993e6ddb2301121a1e32b1672425e919dea
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/16/2018
---
# <a name="apply-settings-to-android-for-work-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Aplicar as definições para o Android para aplicações de trabalho com políticas de configuração de aplicações no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar políticas de configuração de aplicações no System Center Configuration Manager para distribuir as definições que poderão ser necessárias quando um utilizador executa uma aplicação. Por exemplo, uma aplicação pode requerer que um utilizador especificar estes detalhes:
- Um número de porta personalizado
- Definições de idioma
- Definições de segurança
- Definições de imagem corporativa, como um logótipo de empresa

Se o utilizador introduzir as definições incorretamente, o fardo corrigir recai no suporte técnico e implementação de aplicação é lenta. Para ajudar a evitar estes problemas, pode utilizar políticas de configuração de aplicação para implementar as definições necessárias para os utilizadores antes do que executar a aplicação. As definições estão associadas um utilizador automaticamente. O utilizador não tem de efetuar qualquer ação.
Em vez de implementar políticas de configuração diretamente a utilizadores e dispositivos, associar uma política com um tipo de implementação ao implementar a aplicação. As definições de política são aplicadas sempre que a aplicação verifica a existência de-los, normalmente, a primeira vez que a aplicação é executada.

Políticas de configuração de aplicação Android estão disponíveis apenas em dispositivos com o Android de trabalho. Aplicam políticas de configuração de aplicação para aplicações aprovadas da Play para o arquivo de trabalho. Para obter detalhes sobre as aplicações compradas em volume Android, consulte [como implementar aplicações Android para dispositivos de trabalho](https://docs.microsoft.com/intune/deploy-use/android-for-work-apps).

Para obter mais informações sobre os tipos de instalação de aplicações, consulte o [introdução à gestão de aplicações](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Criar uma política de configuração de aplicação

1. Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **políticas de configuração de aplicação**.
2. No **home page** separador o **políticas de configuração de aplicação** grupo, escolha **criar política de configuração de aplicação**.
3. No Assistente de criação de aplicação configuração política no **geral** página, defina estas informações de política:
  - **Nome**. Introduza um nome exclusivo para a política.
  - **Descrição**. (Opcional) Para tornar mais fácil de identificar a política, pode adicionar uma descrição.
  -  **Selecione um tipo de política de configuração**. Especifique a plataforma visada pela política de configuração de aplicação: **Política de configuração para Android para aplicações de trabalho**.
  -  **Atribuir categorias para melhorar a procura e filtragem**. (Opcional) Para criar e atribuir categorias para a política, escolha **categorias**. Categorias de tornam mais fácil para si ordenar e encontrar itens na consola do Configuration Manager.
4. No **Android para a política de trabalho** página, selecione como definir as informações de política de configuração:
  - **Especifique pares nome / valor**. Pode utilizar esta opção para ficheiros de lista de propriedades que não utilizem o aninhamento. Para especificar um par nome e valor:
        1. Para adicionar um novo par JSON, escolha **novo**.
        2. No **adicionar par de nome/valor** diálogo caixa, especifique os seguintes detalhes:
            - **Tipo**. Na lista, selecione o tipo de valor que pretende que especificar.
            - **Nome**. Introduza o nome da chave de lista de propriedade para o qual pretende especificar um valor.
            - **Valor**. Introduza o valor que será aplicado para a chave que introduziu.

  - **Procure um ficheiro JSON de lista de propriedade**. Utilize esta opção se já tiver um ficheiro JSON de configuração de aplicação ou para os ficheiros mais complexos que utilizam o aninhamento. No **política de configuração de aplicação** campo, introduza as informações de lista de propriedades no formato JSON correto.
5. Para importar um ficheiro JSON que criou anteriormente, escolha **selecionar ficheiro**.
6. Escolha **seguinte**. Se existirem erros no código JSON, corrija-os antes de continuar.
7. Conclua os passos apresentados no assistente.

A nova política de configuração de aplicação é apresentada no **biblioteca de Software** área de trabalho, no **políticas de configuração de aplicação** nós.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Associar uma política de configuração de aplicação a uma aplicação do Configuration Manager

Para associar uma política de configuração de aplicação com a implementação de um Android para a aplicação de trabalho, implementar a aplicação como faria normalmente, utilizando o procedimento a [implementar aplicações](/sccm/apps/deploy-use/deploy-applications) tópico.

No Assistente para implementar Software, no **políticas de configuração de aplicação** página, escolha **novo**. No **selecionar política de configuração de aplicação** diálogo caixa, escolha um tipo de implementação de aplicação e a política de configuração de aplicação que pretende associá-lo.
Quando o tipo de implementação é instalado, é aplicada automaticamente as definições de política de configuração de aplicação.

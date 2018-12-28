---
title: Configurar o Android for Work aplicações com políticas de configuração de aplicação
titleSuffix: Configuration Manager
description: Ajudar a eliminar problemas de configuração em dispositivos Android for Work mediante a implementação de políticas de configuração de aplicações aos utilizadores antes de executarem aplicações.
ms.date: 09/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9126d188-7780-45a4-b21d-7fcf4fad7da2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6f83f26f746c54e3d1defe31df47b3c7c8a7e117
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417953"
---
# <a name="apply-settings-to-android-for-work-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Aplicar as definições para Android para trabalho de aplicações com políticas de configuração de aplicações no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar políticas de configuração de aplicações no System Center Configuration Manager para distribuir as definições que poderão ser necessárias quando um utilizador executa uma aplicação. Por exemplo, uma aplicação poderá exigir que um utilizador especificar estes detalhes:
- Um número de porta personalizado
- Definições de idioma
- Definições de segurança
- Definições de imagem corporativa, como um logótipo de empresa

Se o utilizador introduzir as definições incorretamente, a carga corrigi-los recai sobre o suporte técnico e implementação da aplicação está lenta. Para ajudar a evitar estes problemas, pode utilizar políticas de configuração de aplicação para implementar as definições necessárias aos utilizadores antes de executarem a aplicação. As definições são automaticamente associadas a um utilizador. O utilizador não tem de efetuar qualquer ação.
Em vez de implementar políticas de configuração diretamente a utilizadores e dispositivos, associe uma política com um tipo de implementação ao implementar a aplicação. As definições de política são aplicadas sempre que a aplicação as verificar, normalmente a primeira vez que a aplicação é executada.

Políticas de configuração de aplicação Android estão disponíveis apenas em dispositivos Android for Work. Políticas de configuração de aplicações aplicam-se para aplicações aprovadas a partir da Play for Work store. Para obter detalhes sobre as aplicações compradas em volume Android, consulte [como implementar aplicações para Android para dispositivos de trabalho](https://docs.microsoft.com/intune/deploy-use/android-for-work-apps).

Para obter mais informações sobre os tipos de instalação de aplicações, consulte a [introdução à gestão de aplicações](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Criar uma política de configuração de aplicações

1. Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **políticas de configuração de aplicação**.
2. Na **home page** separador a **políticas de configuração de aplicação** de grupo, escolha **criar política de configuração de aplicação**.
3. No Assistente de criação aplicação configuração de política, sobre o **gerais** página, defina estas informações de política:
   - **Nome**. Introduza um nome exclusivo para a política.
   - **Descrição**. (Opcional) Para tornar mais fácil de identificar a política, pode adicionar uma descrição.
   -  **Selecione um tipo de política de configuração**. Especifique a plataforma visada pela política de configuração de aplicação: **Política de configuração para Android para aplicações de trabalho**.
   -  **Atribuir categorias para melhorar a procura e na filtragem**. (Opcional) Para criar e atribuir categorias para a política, escolha **categorias**. Categorias tornam mais fácil para que possa classificar e encontrar itens na consola do Configuration Manager.
4. Sobre o **do Android for Work política** página, selecione como definir as informações de política de configuração:
   - **Especifique pares nome / valor**. Pode utilizar esta opção para ficheiros de lista de propriedades que não usam o aninhamento. Para especificar um par de nome e valor:
        1. Para adicionar um novo par JSON, escolha **New**.
        2. Na **adicionar par de nome/valor** diálogo caixa, especifique os seguintes detalhes:
            - **tipo de**. Na lista, selecione o tipo de valor que pretende especificar.
            - **Nome**. Introduza o nome da chave de lista de propriedade para o qual pretende especificar um valor.
            - **Valor**. Introduza o valor que será aplicado para a chave que introduziu.

   - **Navegue para um ficheiro JSON de lista de propriedades**. Utilize esta opção se já tiver um ficheiro JSON de configuração de aplicação ou para os ficheiros mais complexos que utilizam o aninhamento. Na **política de configuração de aplicação** , insira as informações da lista de propriedade no formato JSON correto.
5. Para importar um ficheiro JSON que criou anteriormente, escolha **selecionar ficheiro**.
6. Selecione **Next**. Se houver erros no código JSON, corrija-os antes de continuar.
7. Conclua os passos apresentados no assistente.

A nova política de configuração de aplicações é mostrada na **biblioteca de Software** área de trabalho, na **políticas de configuração de aplicação** nó.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Associar uma política de configuração de aplicação a uma aplicação do Configuration Manager

Para associar uma política de configuração de aplicação com a implementação de uma aplicação Android for Work, a implementar a aplicação, tal como faria normalmente utilizando o procedimento a [implementar aplicações](/sccm/apps/deploy-use/deploy-applications) tópico.

No Assistente para implementar Software, sobre o **políticas de configuração de aplicação** página, selecione **New**. Na **selecionar política de configuração de aplicação** diálogo caixa, escolha um tipo de implementação de aplicação e a política de configuração de aplicação que pretende associá-la com.
Quando o tipo de implementação é instalado, as definições de política de configuração de aplicações é aplicada automaticamente.

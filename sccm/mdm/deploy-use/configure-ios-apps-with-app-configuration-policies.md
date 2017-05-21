---
title: "Configurar as aplicações iOS com as políticas de configuração de aplicação | Documentos do Microsoft"
description: "Ajude a eliminar problemas de configuração nos dispositivos que executam o iOS 8 ou posterior ao implementar políticas de configuração de aplicação para os utilizadores antes de estes executados aplicações."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0a78038-ea22-4826-9c07-1771b7dd2e8d
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 23b1d24e908d04b64c3bbfa518793a44e696d468
ms.openlocfilehash: 50aea2afaf34974ca92ac58b6569bff56403a9ab
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="apply-settings-to-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Aplicar definições a aplicações iOS com as políticas de configuração da aplicação no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Pode utilizar as políticas de configuração de aplicação no System Center Configuration Manager (Configuration Manager) para distribuir as definições que poderão ser necessárias quando um utilizador executa uma aplicação. Por exemplo, uma aplicação pode necessitar de um utilizador especificar esses detalhes:
- Um número de porta personalizado
- Definições de idioma
- Definições de segurança
- Definições de imagem corporativa, como um logótipo de empresa

Se o utilizador introduz as definições incorretamente, fica a carga para resolvê-los no seu suporte técnico e implementação de aplicações é lenta.
Para o ajudar a evitar estes problemas, pode utilizar as políticas de configuração de aplicação para implementar definições necessárias para os utilizadores antes que executar a aplicação. As definições são automaticamente associadas a um utilizador. O utilizador não tem de efetuar qualquer ação.
Para utilizar uma política de configuração de aplicações no Configuration Manager, em vez de implementar as políticas de configuração diretamente a utilizadores e dispositivos, associar uma política com um tipo de implementação quando implementar a aplicação. As definições de política são aplicadas sempre que a aplicação verifica a existência de-las (normalmente, a primeira vez a aplicação é executada).

Atualmente, as políticas de configuração de aplicação estão disponíveis apenas em dispositivos que executam o iOS 8 e posterior e para estes tipos de aplicação:

- **pacote de aplicação para iOS (*ficheiro. IPA)**
- **pacote de aplicação para iOS da App Store**

Para obter mais informações sobre tipos de instalação da aplicação, consulte o [introdução à gestão de aplicações](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Criar uma política de configuração de aplicação

1. Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **políticas de configuração de aplicação**.
2. No **base** separador o **políticas de configuração de aplicação** grupo, selecione **criar nova política de configuração de aplicação**.
3. No Assistente de criação App configuração política, no **geral** página, defina estas informações de política:
  - **Nome**. Introduza um nome exclusivo para a política.
  - **Descrição**. (Opcional) Para tornar mais fáceis de identificar a política, pode adicionar uma descrição.
  - **Categorias para melhorar a procura e filtragem atribuídas**. (Opcional) Para criar e atribuir categorias para a política, selecione **categorias**. Categorias facilitam organizar e localizar itens na consola do Configuration Manager.
4. No **política para iOS** página, selecione como definir as informações de política de configuração:
  - **Especifique os pares de nome e valor**. Pode utilizar esta opção para a propriedade listam os ficheiros que não utilizem o aninhamento.

      *Para especificar um par nome e valor*
        1. Para adicionar um novo par, escolha **novo**.
        2. No **adicionar par nome/valor** diálogo caixa, especifique o seguinte:
            - **Tipo de**. Na lista, selecione o tipo de valor que pretende especificar.
            - **Nome**. Introduza o nome da chave de lista de propriedades para o qual pretende especificar um valor.
            - **Valor**. Introduza o valor que será aplicado para a chave que introduziu.

  - **Procure um ficheiro de lista de propriedade**. Utilize esta opção se já tiver um ficheiro de XML de configuração de aplicação, ou ficheiros mais complexos que utilizam o aninhamento.

    *Para procurar um ficheiro de lista de propriedade*

      1.  No **política de configuração de aplicação** de campo, introduza as informações de lista de propriedade no formato XML correto.

      Para saber mais sobre listas de propriedades XML, consulte o artigo [Noções básicas sobre XML propriedade apresenta uma lista de](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) na biblioteca do programador do iOS.

O formato da lista de propriedade XML varia consoante a aplicação que estiver a configurar. Contacte o fornecedor da aplicação para obter detalhes sobre o formato a utilizar.
Intune suporta os seguintes tipos de dados de uma lista de propriedade:
            
            ```
            <integer>
            <real>
            <string>
            <array>
            <dict>
            <true /> or <false />
            ```
Para obter mais informações sobre tipos de dados, consulte o artigo [sobre propriedade apresenta uma lista de](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html) na biblioteca do programador do iOS.
Também o Intune suporta os seguintes tipos de token na lista de propriedade:
            
            ```
            {{userprincipalname}} - (Example: John@contoso.com)
            {{mail}} - (Example: John@contoso.com)
            {{partialupn}} - (Example: John)
            {{accountid}} - (Example: fc0dc142-71d8-4b12-bbea-bae2a8514c81)
            {{deviceid}} - (Example: b9841cd9-9843-405f-be28-b2265c59ef97)
            {{userid}} - (Example: 3ec2c00f-b125-4519-acf0-302ac3761822)
            {{username}} - (Example: John Doe)
            {{serialnumber}} - (Example: F4KN99ZUG5V2) for iOS devices
            {{serialnumberlast4digits}} - (Example: G5V2) for iOS devices
            ```

Os {{e}} carateres são utilizados por apenas tipos de token e não devem ser utilizados para outros fins.
            
5. Para importar um ficheiro XML que criou anteriormente, selecione **ficheiro selecione**.
6. Escolher **seguinte**. Se existirem erros no código XML, terá de corrigi-los antes de continuar.
7. Conclua os passos apresentados no assistente.

A nova política de configuração de aplicação é apresentada no **biblioteca de Software** área de trabalho, no **políticas de configuração de aplicação** nó.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Associar uma política de configuração de aplicação a uma aplicação do Configuration Manager

Para associar uma política de configuração de aplicação com a implementação de uma aplicação iOS, a implementar a aplicação, como faria normalmente, utilizando o procedimento apresentado a [implementar aplicações](/sccm/apps/deploy-use/deploy-applications) tópico.

No Assistente de implementação de Software, no **políticas de configuração de aplicação** página, selecione **novo**. No **selecionar política de configuração de aplicação** diálogo caixa, selecione um tipo de implementação de aplicação e a política de configuração de aplicação que pretende associar aos.
Quando é instalado o tipo de implementação, as definições de política de configuração de aplicação é aplicada automaticamente.

## <a name="example-format-for-the-mobile-app-configuration-xml-file"></a>Formato de exemplo para o ficheiro de XML de configuração de aplicação móvel

Quando cria um ficheiro de configuração de aplicação móvel, pode utilizar este formato para especificar um ou mais dos seguintes valores:

```
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
</dict>
```


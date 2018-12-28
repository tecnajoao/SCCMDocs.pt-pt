---
title: Configurar aplicações iOS com políticas de configuração de aplicação
titleSuffix: Configuration Manager
description: Ajudar a eliminar problemas de configuração em dispositivos com iOS 8 ou posterior ao implementar políticas de configuração de aplicações aos utilizadores antes de executarem aplicações.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: f0a78038-ea22-4826-9c07-1771b7dd2e8d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 19b55204566c49c95e76a3eff3f88206df553e13
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416168"
---
# <a name="apply-settings-to-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Aplicar as definições para aplicações iOS com políticas de configuração de aplicações no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Pode utilizar políticas de configuração de aplicações no System Center Configuration Manager (Configuration Manager) para distribuir as definições que poderão ser necessárias quando um utilizador executa uma aplicação. Por exemplo, uma aplicação poderá exigir que um utilizador especificar estes detalhes:
- Um número de porta personalizado
- Definições de idioma
- Definições de segurança
- Definições de imagem corporativa, como um logótipo de empresa

Se o utilizador introduzir as definições incorretamente, a carga corrigi-los recai sobre o suporte técnico e implementação da aplicação está lenta.
Para ajudar a evitar estes problemas, pode utilizar políticas de configuração de aplicação para implementar as definições necessárias aos utilizadores antes de executarem a aplicação. As definições são automaticamente associadas a um utilizador. O utilizador não tem de efetuar qualquer ação.
Para utilizar uma política de configuração de aplicações no Configuration Manager, em vez de implementar as políticas de configuração diretamente a utilizadores e dispositivos, associe uma política com um tipo de implementação ao implementar a aplicação. As definições de política são aplicadas sempre que a aplicação as verificar (normalmente, a primeira vez a aplicação é executada).

Atualmente, as políticas de configuração de aplicação estão disponíveis apenas em dispositivos com o iOS 8 e posterior e para estes tipos de aplicação:

- **pacote de aplicação para iOS (ficheiro IPA)**
- **pacote de aplicação para iOS da App Store**

Para obter mais informações sobre os tipos de instalação de aplicações, consulte a [introdução à gestão de aplicações](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Criar uma política de configuração de aplicações

1. Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **políticas de configuração de aplicação**.
2. Na **home page** separador a **políticas de configuração de aplicação** de grupo, escolha **criar nova política de configuração de aplicação**.
3. No Assistente de criação aplicação configuração de política, sobre o **gerais** página, defina estas informações de política:
   - **Nome**. Introduza um nome exclusivo para a política.
   - **Descrição**. (Opcional) Para tornar mais fácil de identificar a política, pode adicionar uma descrição.
   - **Atribuir categorias para melhorar a procura e na filtragem**. (Opcional) Para criar e atribuir categorias para a política, escolha **categorias**. Categorias tornam mais fácil para que possa classificar e encontrar itens na consola do Configuration Manager.
4. Sobre o **política para iOS** página, selecione como definir as informações de política de configuração:
   - **Especifique pares nome / valor**. Pode utilizar esta opção para ficheiros de lista de propriedades que não usam o aninhamento.

      *Para especificar um par de nome e valor*
        1. Para adicionar um novo par, escolha **New**.
        2. Na **adicionar par de nome/valor** diálogo caixa, especifique o seguinte:
            - **tipo de**. Na lista, selecione o tipo de valor que pretende especificar.
            - **Nome**. Introduza o nome da chave de lista de propriedade para o qual pretende especificar um valor.
            - **Valor**. Introduza o valor que será aplicado para a chave que introduziu.

   - **Navegue para um ficheiro de lista de propriedades**. Utilize esta opção se já tiver um ficheiro XML de configuração de aplicação ou para os ficheiros mais complexos que utilizam o aninhamento.

     *Para navegar para um ficheiro de lista de propriedades*

     1. Na **política de configuração de aplicação** , insira as informações da lista de propriedade no formato XML correto.

        Para saber mais sobre listas de propriedades XML, consulte [compreender listas de propriedades de XML](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) na iOS Developer Library.

O formato de lista de propriedades XML varia consoante a aplicação que está a configurar. Contacte o fornecedor de aplicação para obter detalhes sobre o formato a utilizar.
O Intune suporta os seguintes tipos de dados numa lista de propriedades:
            
            ```
            <integer>
            <real>
            <string>
            <array>
            <dict>
            <true /> or <false />
            ```
Para obter mais informações sobre tipos de dados, consulte [sobre listas de propriedades](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html) na iOS Developer Library.
O Intune também suporta os seguintes tipos de token na lista de propriedades:
            
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

O {{e}} carateres são utilizados por apenas tipos de token e não pode ser utilizados para outros fins.
            
5. Para importar um ficheiro XML que criou anteriormente, escolha **selecionar ficheiro**.
6. Selecione **Next**. Se houver erros no código XML, terá para corrigi-los antes de continuar.
7. Conclua os passos apresentados no assistente.

A nova política de configuração de aplicações é mostrada na **biblioteca de Software** área de trabalho, na **políticas de configuração de aplicação** nó.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Associar uma política de configuração de aplicação a uma aplicação do Configuration Manager

Para associar uma política de configuração de aplicação com a implementação de uma aplicação iOS, a implementar a aplicação, tal como faria normalmente utilizando o procedimento a [implementar aplicações](/sccm/apps/deploy-use/deploy-applications) tópico.

No Assistente para implementar Software, sobre o **políticas de configuração de aplicação** página, selecione **New**. Na **selecionar política de configuração de aplicação** diálogo caixa, escolha um tipo de implementação de aplicação e a política de configuração de aplicação que pretende associá-la com.
Quando o tipo de implementação é instalado, as definições de política de configuração de aplicações é aplicada automaticamente.

## <a name="example-format-for-the-mobile-app-configuration-xml-file"></a>Formato de exemplo para o ficheiro XML de configuração de aplicação móvel

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

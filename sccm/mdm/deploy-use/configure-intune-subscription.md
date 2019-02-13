---
title: Configurar a sua subscrição do Intune
titleSuffix: Configuration Manager
description: Configure a sua subscrição do Intune com o System Center Configuration Manager.
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 99de8fe7-560e-401a-8ab2-6d87d091be17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9ec6756e5c180561bef10bba799e3fdba3dcc303
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137631"
---
# <a name="configure-your-intune-subscription-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a sua subscrição do Intune com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A subscrição do Intune permite-lhe gerir dispositivos através da internet. Isto inclui especificar qual coleção de utilizador pode inscrever dispositivos e definir as informações apresentadas aos utilizadores. Ao criar a subscrição do Intune, também pode adicionar imagem corporativa portal da empresa do Intune com o seu logótipo da empresa e a cor personalizada esquemas.

A subscrição do Intune faz o seguinte:

-   Obtém o certificado de que o ponto de ligação de serviço necessita para efetuar a ligação ao serviço Intune
-   Define a coleção de utilizadores que permite aos utilizadores inscreverem dispositivos móveis
-   Define e configura as plataformas móveis que pretende suportar

> [!IMPORTANT]
>  Criar uma subscrição do Microsoft Intune no Configuration Manager irá colocar o ponto de ligação de serviço do seu site no "modo online". Veja [Acerca do ponto de ligação de serviço no System Center Configuration Manager](../../core/servers/deploy/configure/about-the-service-connection-point.md).

## <a name="to-create-the-microsoft-intune-subscription"></a>Para criar a subscrição do Microsoft Intune

1.  Se ainda não o fez, inscreva-se numa conta do Microsoft Intune em [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216).  Depois de criar a sua conta do Intune, não é necessário adicionar todos os utilizadores para a conta do Intune ou efetuar configurações de configurações adicionais.

2.  Na consola do Configuration Manager, clique em **Administração**.

3.  Na área de trabalho **Administração**, expanda **Serviços Cloud** e clique em **Subscrições do Microsoft Intune**. No separador **Home Page**, clique em **Adicionar Subscrição do Microsoft Intune**.

![Criar uma subscrição do Intune](../media/mdm-set-intune.png)

4. Na página **Introdução** do Assistente Criar Subscrição do Microsoft Intune, reveja o texto e clique em **Seguinte**.

5. Na página **Subscrição**, clique em **Iniciar sessão** e inicie sessão utilizando a sua conta escolar ou profissional. Na **definir a autoridade de gestão de dispositivos móveis** caixa de diálogo, selecione a caixa de verificação apenas para gerir dispositivos móveis utilizando o Gestor de configuração através da consola do Configuration Manager. Para continuar a subscrição, terá de selecionar esta opção.

   > [!IMPORTANT]
   >  Depois de selecionar o Configuration Manager como autoridade de gestão, só pode alterar a autoridade de gestão para o Microsoft Intune no Configuration Manager versão 1610 ou posterior e o Microsoft Intune version 1705 sem ter de contactar Support da Microsoft, e, sem ter de anular a inscrição e inscrever novamente os já existentes a dispositivos geridos. Para obter detalhes, consulte [alterar a sua autoridade MDM](/sccm/mdm/deploy-use/change-mdm-authority).

6. Clique nas hiperligações de privacidade para revê-las e clique em **Seguinte**.

7. Na página **Geral**, especifique as seguintes opções e clique em **Seguinte**.

   - **Coleção**: Especifique uma coleção de utilizadores que contenha os utilizadores que poderão inscrever os respetivos dispositivos móveis.

     > [!NOTE]
     >  Se um utilizador é removido da coleção, o dispositivo do utilizador continuará a ser gerido durante até 24 horas, quando o registo do utilizador é removido da base de dados do utilizador.

   - **Nome da empresa**: Especifique o nome da sua empresa.

   - **URL para a documentação de privacidade da empresa**: Se publicar as informações de privacidade da empresa numa ligação acessível a partir da Internet, forneça uma ligação que os utilizadores podem aceder a partir do portal da empresa, por exemplo http://www.contoso.com/CP_privacy.html. As informações de privacidade permitem clarificar as informações que os utilizadores partilham com a empresa.

   - **Esquema de cores para o portal da empresa**: Opcionalmente, altere a cor de predefinição de azul portais de empresa.

   - **Código de site do Configuration Manager**: Especifique um código de site para um site primário gerir os dispositivos móveis.

   > [!NOTE]
   >  A alteração do código do site afeta apenas as novas inscrições, não afetando os dispositivos já inscritos.

8. Sobre o **informações de contacto da empresa** , especifique as informações de contacto da empresa que são apresentadas para usuários sob **contactar TI** na aplicação Portal da empresa. Forneça informações de contacto para a sua empresa e, em seguida, clique em **seguinte**.

9. Sobre o **logótipo da empresa** página, pode escolher se pretende apresentar logótipos no portal da empresa e, em seguida, clique em **próxima**.

10. Conclua o assistente.

> [!div class="button"]
> [< Anterior passo](confirm-dns.md)[passo seguinte >](terms-and-conditions.md)

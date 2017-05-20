---
title: Inscrever dispositivos iOS. o Apple Configurator - Configuration Manager | Documentos do Microsoft
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: 5
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: f8242b4b454622388f45c34ba71c4148c87c27b7
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>inscrição do iOS híbridos através do Apple Configurator com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Empresas que comprem dispositivos iOS para serem utilizados pelos funcionários podem geri-los a através do Microsoft Intune. Para preparar a dispositivos iOS pertencentes para inscrição, pode configura um perfil de inscrição na consola do Configuration Manager e, em seguida, exportar o URL do perfil para utilização por Apple Configurator. Prepare o dispositivo iOS para inscrição ao ligar a um computador Mac com um cabo USB e através do Apple Configurator para configurá-lo. As definições de fábrica do Apple Configurator repõe o dispositivo e adiciona o perfil de inscrição para que o dispositivo seja inscrito quando o utilizador alimenta-o e executa o processo do Assistente de configuração.

Para dispositivos iOS dedicado que terão um único utilizador que utiliza o dispositivo para aceder ao e-mail da empresa e recursos da empresa, tais como aplicações e a data, recomenda-se o procedimento seguinte.  

## <a name="prerequisites"></a>Pré-requisitos  

-   Acesso físico aos dispositivos iOS  

-   Números de série do dispositivo - [como obter um número de série iOS](https://support.apple.com/en-us/HT204308)  

-   Computador Mac com [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017)  

-   Cabos USB para ligar dispositivos para o computador Mac  

## <a name="step-1-add-a-corporate-owned-device-enrollment-profile"></a>Passo 1: Adicionar um perfil de inscrição de dispositivos pertencentes à empresa

1.  Na consola do Configuration Manager, aceda a **ativos e compatibilidade** > **descrição geral** > **todos os dispositivos pertencentes** > **iOS** > **perfis de inscrição**. Clique em **criar perfil** para abrir o Assistente para criar perfil. Configure as definições nas seguintes páginas:  

2.  Na página **Geral** , especifique as seguintes informações:  

    -   **Nome** (não é visível para os utilizadores)  

    -   **Descrição** (não é visível para os utilizadores)  

    -   **Afinidade do utilizador** – especifica como os dispositivos são inscritos. Para a maioria dos cenários no Assistente de configuração, utilize **pedido de afinidade de utilizador de**.  

        -   **Pedido de afinidade de utilizador de**: O dispositivo tem de ser afiliado a um utilizador durante a configuração inicial e, em seguida, foi permitido para aceder ao e-mail desse utilizador e dados da empresa.  

        -   **Sem afinidade de utilizador**: O dispositivo não está afiliado a um utilizador. Utilize esta afiliação em dispositivos que efetuem tarefas sem aceder aos dados de utilizador locais. As aplicações que precisem da afiliação de utilizador não funcionam.

    Clique em **Seguinte** para continuar.  

3.  No **programa de inscrição de dispositivos** página, deixe a **definições de configurar o programa de inscrição de dispositivos para este perfil** caixa de verificação desmarcada e clique em **seguinte**.  

4.  Reveja o resumo e, em seguida, clique em **seguinte** para criar o perfil de inscrição. Clique em **Fechar** para concluir o assistente. Agora está pronto para adicionar números IMEI ou números de série para os dispositivos que pretende inscrever.  

## <a name="step-2-predeclare-devices-to-enroll-with-setup-assistant"></a>Passo 2: Predeclare dispositivos a inscrever-se com o Assistente de configuração

Neste passo, predeclare dispositivos como pertencentes ao fornecer uma lista de identificadores de hardware (IMEI ou números de série).

Para obter mais informações, consulte o artigo [Predeclare dispositivos com o número de série IMEI e iOS](predeclare-devices-with-hardware-id.md). Quando terminar nessa tarefa, devolva a esta página para continuar com o passo seguinte.

## <a name="step-3-export-the-profile-to-deploy-to-ios-devices"></a>Passo 3: Exportar o perfil a implementar nos dispositivos iOS

1.  Na consola do Configuration Manager, aceda a **ativos e compatibilidade** > **descrição geral** > **todos os dispositivos pertencentes** > **iOS** > **perfis de inscrição**.

2.  Selecione o perfil de inscrição para implementar em dispositivos móveis e clique em **exportar...** .

3.  Copie e guarde o **URL do perfil** num ficheiro pode editar.   

4.  Para suportar o Apple Configurator 2, o URL do perfil 2.0 tem de ser editada. Substitua a parte do URL seguinte:  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     com o  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```

5.  Guarde o URL do perfil editado. Irá utilizá-lo para adicionar o URL do perfil de inscrição no Apple Configurator no [secção seguinte](#step-4-prepare-the-device-with-apple-configurator).  

> [!NOTE]
> O URL do perfil de inscrição é válido durante duas semanas a partir da respetiva exportação. Após duas semanas, tem de exportá um novo URL para inscrever dispositivos iOS.

## <a name="step-4-prepare-the-device-with-apple-configurator"></a>Passo 4: Preparar o dispositivo com o Apple Configurator

Para preparar a dispositivos iOS para inscrição, pode ligar cada dispositivo a um computador Mac e carregar o perfil de inscrição-lo.  

> [!WARNING]  
>  Apple Configurator apaga e repõe dispositivos para as configurações de fábrica.  

1.  Num computador Mac, abra **Apple Configurator 2**.  

2.  Na barra de menus, clique em **Apple Configurator 2** > **preferências**.  

2.  No painel preferências, selecione **servidores** e clique no símbolo de "+" por baixo do painel da esquerda para iniciar o Assistente do servidor MDM. Clique em **Seguinte**.  

3.  Introduza o **nome** e **URL de inscrição** que guardou [anteriores](#step-3-export-the-profile-to-deploy-to-ios-devices). Clique em **Seguinte**.  

   > [!NOTE]
   > Se receber um aviso sobre os requisitos de perfil de confiança para Apple TV, pode cancelar em segurança a **fidedignidade perfil** opção clicando o cinzento "X". Também pode ignorar com segurança qualquer aviso de certificado de Âncora.

   Para continuar, clique em **seguinte** até que o assistente seja concluído.  

4.  No **servidores** painel, clique em "Editar" ao lado de perfil do novo servidor. Certifique-se de que o URL de inscrição corresponde exatamente ao URL que inseriu anteriormente. Reintroduza o URL, se for diferente e clique em **guardar**.  

5.  Com um cabo USB, ligue um dispositivo iOS ao computador Mac.  

  > [!WARNING]  
  >  Este processo repõe dispositivos para as configurações de fábrica. Antes de ligar o dispositivo, repor o dispositivo e de ativação-lo. Como melhor prática, o dispositivo deve estar no ecrã Olá antes de continuar.  

6.  Clique em **preparar**. No **preparar o dispositivo iOS** painel, selecione **Manual**e, em seguida, clique em **seguinte**.  

7.  No **inscrever no servidor MDM** painel, selecione o servidor de nomes que criou e, em seguida, clique em **seguinte**.  

9. No **criar uma organização** painel, escolha o **organização** ou criar uma nova organização e, em seguida, clique em **seguinte**.  

10. No **configurar Assistente de configuração iOS** painel, escolha os passos para apresentar ao utilizador e, em seguida, clique em **preparar**. Se lhe for solicitado, autenticar para atualizar as definições de fidedignidade.  

11. Quando terminar, pode desligar o cabo USB.  

Repita estes passos para todos os dispositivos que pretende preparar a inscrição.

## <a name="step-5-distribute-devices"></a>Passo 5: Distribuir dispositivos pelos

Os dispositivos estão agora prontos para a inscrição na empresa. Desligue os dispositivos e distribua-os pelos utilizadores. Quando o dispositivo estiver ativado, Assistente de configuração irá iniciar e pedirá ao utilizador para a respetiva conta escolar ou profissional para iniciar a inscrição.


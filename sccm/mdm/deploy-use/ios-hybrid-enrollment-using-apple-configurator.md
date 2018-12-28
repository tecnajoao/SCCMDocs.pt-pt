---
title: 'Inscrever dispositivos iOS do Apple Configurator '
titleSuffix: Configuration Manager
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.date: 08/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de83706e92150a654967ec5cf38c5b18508d4e2b
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416916"
---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>inscrição do iOS híbrida com o Apple Configurator com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Empresas que compram dispositivos iOS para ser utilizada pelos funcionários podem gerir--los através do Microsoft Intune. Para preparar os dispositivos iOS pertencentes à empresa para inscrição, configure um perfil de inscrição na consola do Configuration Manager e, em seguida, exportar o URL do perfil para utilização pelo Apple Configurator. Preparar o dispositivo iOS para inscrição ao ligá-la para um computador Mac com um cabo USB e utilizar o Apple Configurator para configurá-lo. Fábrica do Apple Configurator repõe o dispositivo e adiciona o perfil de inscrição para que o dispositivo seja inscrito quando o utilizador liga-se e executa o processo Assistente de configuração.

Para dispositivos iOS dedicados que terão um único utilizador que utiliza o dispositivo para aceder ao e-mail da empresa e recursos da empresa, tais como aplicações e a data, recomenda-se o procedimento seguinte.  

## <a name="prerequisites"></a>Pré-requisitos  

-   Acesso físico a dispositivos iOS  

-   Números de série do dispositivo - [como obter um número de série iOS](https://support.apple.com/en-us/HT204308)  

-   Computador Mac com [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017)  

-   Cabos USB para ligar dispositivos ao seu computador Mac  

## <a name="add-a-corporate-owned-device-enrollment-profile"></a>Adicionar um perfil de inscrição de dispositivos pertencentes à empresa

1.  Na consola do Configuration Manager, aceda a **ativos e compatibilidade** > **descrição geral** > **todos os dispositivos da empresa**  >  **iOS** > **perfis de inscrição**. Clique em **criar perfil** para abrir o Assistente Criar perfil. Configure as definições nas seguintes páginas:  

2.  Na página **Geral** , especifique as seguintes informações:  

    -   **Nome** (não visível aos utilizadores)  

    -   **Descrição** (não visível aos utilizadores)  

    -   **Afinidade do utilizador** – especifica como os dispositivos são inscritos. Na maioria dos cenários de Assistente de configuração, utilize **pedir afinidade do utilizador**.  

        -   **Pedir afinidade do utilizador**: O dispositivo tem de ser afiliado a um utilizador durante a configuração inicial e, em seguida, poderia ter permissão para aceder a e-mail que o utilizador e dados da empresa.  

        -   **Sem afinidade de utilizador**: O dispositivo não está afiliado a um utilizador. Utilize esta afiliação em dispositivos que efetuem tarefas sem aceder aos dados de utilizador locais. As aplicações que precisem da afiliação de utilizador não funcionam.

    Clique em **Seguinte** para continuar.  

3.  Sobre o **programa de inscrição de dispositivos** página, deixe a **definições de configurar o programa de inscrição de dispositivos para este perfil** caixa de verificação desmarcada e clique em **seguinte**.  

4.  Reveja o resumo e, em seguida, clique em **seguinte** para criar o perfil de inscrição. Clique em **Fechar** para concluir o assistente. Agora, está pronto para adicionar números IMEI ou números de série para os dispositivos que pretende inscrever.  

## <a name="predeclare-devices-to-enroll-with-setup-assistant"></a>Pré-declarar dispositivos para inscrição com o Assistente de configuração

Neste passo, pré-declarar dispositivos como pertencentes ao fornecer uma lista de identificadores de hardware (números de série ou IMEI).

Para obter mais informações, consulte [pré-declarar dispositivos com o número de série IMEI e iOS](predeclare-devices-with-hardware-id.md). Quando tiver terminado com essa tarefa, volte a esta página para continuar com a próxima etapa.

## <a name="export-the-profile-to-deploy-to-ios-devices"></a>Exportar o perfil a implementar nos dispositivos iOS

1.  Na consola do Configuration Manager, aceda a **ativos e compatibilidade** > **descrição geral** > **todos os dispositivos da empresa**  >  **iOS** > **perfis de inscrição**.

2.  Selecione o perfil de inscrição para implementar em dispositivos móveis e clique em **exportar...** .

3.  Copie e guarde o **URL de perfil** num arquivo pode editar.   

4.  Para suportar o Apple Configurator 2, o URL do perfil 2.0 tem de ser editado. Substitua a parte seguinte do URL:  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     com o  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```

5.  Guarde o URL do perfil editado. Irá utilizá-lo para adicionar o URL do perfil de inscrição no Apple Configurator no [próxima seção](#step-4-prepare-the-device-with-apple-configurator).  

> [!NOTE]
> O URL do perfil de inscrição é válido durante duas semanas a partir da respetiva exportação. Após duas semanas, tem de exportar um novo URL para inscrever dispositivos iOS.

## <a name="prepare-the-device-with-apple-configurator"></a>Preparar o dispositivo com o Apple Configurator

Para preparar os dispositivos iOS para inscrição, ligue cada dispositivo a um computador Mac e carregar o perfil de inscrição para o mesmo.  

> [!WARNING]  
>  Apple Configurator apaga e repõe os dispositivos para as configurações de fábrica.  

1. Num computador Mac, abra o **Apple Configurator 2**.  

2. Na barra de menus, clique em **Apple Configurator 2** > **preferências**.  

3. No painel de preferências, selecione **servidores** e clique no símbolo "+" por baixo do painel da esquerda para iniciar o Assistente do servidor MDM. Clique em **Seguinte**.  

4. Introduza o **Name** e **URL de inscrição** guardado [anteriores](#step-3-export-the-profile-to-deploy-to-ios-devices). Clique em **Seguinte**.  

   > [!NOTE]
   > Se receber um aviso sobre os requisitos de perfil de confiança para Apple TV, pode cancelar com segurança os **perfil de confiança** opção clicando no "X" cinzento. Também pode ignorar com segurança qualquer aviso de certificado de Âncora.

   Para continuar, clique em **seguinte** até que o assistente for concluído.  

5. Sobre o **servidores** painel, clique em "Editar" ao lado do perfil do novo servidor. Certifique-se de que o URL de inscrição corresponde exatamente ao URL que introduziu anteriormente. Se for diferente, reintroduza o URL e clique em **guardar**.  

6. Com um cabo USB, ligar um dispositivo iOS ao computador Mac.  

   > [!WARNING]  
   >  Este processo repõe os dispositivos para as configurações de fábrica. Antes de ligar o dispositivo, repor o dispositivo e ligue-o. Como melhor prática, o dispositivo deve estar no ecrã de boas-vindas antes de continuar.  

7. Clique em **preparar**. Sobre o **preparar o dispositivo iOS** painel, selecione **Manual**e, em seguida, clique em **seguinte**.  

8. Sobre o **inscrever no servidor MDM** painel, selecione o servidor de nomes que criou e, em seguida, clique em **próxima**.  

9. Sobre o **criar uma organização** painel, escolha a **organização** ou crie uma nova organização e, em seguida, clique em **seguinte**.  

10. Sobre o **configurar o Assistente de configuração iOS** painel, escolha os passos para apresentar ao usuário e, em seguida, clique em **preparar**. Se lhe for pedido, autentique para atualizar as definições de fidedignidade.  

11. Quando terminar, pode desligar o cabo USB.  

Repita estes passos para todos os dispositivos que pretende preparar para a inscrição.

## <a name="distribute-devices"></a>Distribuir dispositivos

Os dispositivos estão agora prontos para a inscrição na empresa. Desligue os dispositivos e distribua-os pelos utilizadores. Quando o dispositivo estiver ativado, Assistente de configuração irá iniciar e pedir ao utilizador para a conta profissional ou escolar para começar a inscrição.

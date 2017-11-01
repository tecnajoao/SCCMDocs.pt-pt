---
title: 'Inscrever dispositivos iOS Apple Configurator '
titleSuffix: Configuration Manager
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.custom: na
ms.date: 08/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: "5"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: e5f7356e2cfe003071a0f090add67cd66acfe062
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>inscrição do iOS híbrida com o Apple Configurator com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As empresas que comprar dispositivos iOS para ser utilizadas pelos empregados podem geri-los a utilizar o Microsoft Intune. Para preparar os dispositivos iOS pertencentes à empresa para a inscrição, pode configurar um perfil de inscrição na consola do Configuration Manager e, em seguida, exportar o URL do perfil para utilização pelo Apple Configurator. Preparar o dispositivo iOS para inscrição ao ligar a um computador Mac com um cabo USB e configurá-lo através do Apple Configurator. Fábrica de Apple Configurator repõe o dispositivo e adiciona o perfil de inscrição para que o dispositivo seja inscrito quando o utilizador for ligado, segurança e realiza o processo de Assistente de configuração.

O procedimento seguinte é recomendado para os dispositivos iOS dedicados que terão um único utilizador, que utiliza o dispositivo para aceder ao e-mail da empresa e recursos da empresa, tais como aplicações e data.  

## <a name="prerequisites"></a>Pré-requisitos  

-   Acesso físico aos dispositivos iOS  

-   Números de série do dispositivo - [como obter um número de série iOS](https://support.apple.com/en-us/HT204308)  

-   Computador Mac com [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017)  

-   Cabos USB para ligar dispositivos para o seu computador Mac  

## <a name="add-a-corporate-owned-device-enrollment-profile"></a>Adicionar um perfil de inscrição de dispositivos pertencentes à empresa

1.  Na consola do Configuration Manager, vá para **ativos e compatibilidade** > **descrição geral** > **todos os dispositivos pertencentes** > **iOS** > **perfis de inscrição**. Clique em **criar perfil** para abrir o Assistente de criação de perfil. Configure as definições nas seguintes páginas:  

2.  Na página **Geral** , especifique as seguintes informações:  

    -   **Nome** (não é visível para os utilizadores)  

    -   **Descrição** (não é visível para os utilizadores)  

    -   **Afinidade do utilizador** – especifica como os dispositivos são inscritos. Para a maioria dos cenários do Assistente de configuração, utilize **solicitar afinidade do utilizador**.  

        -   **Pedido de afinidade de utilizador de**: O dispositivo tem de ser afiliado a um utilizador durante a configuração inicial e, em seguida, pode ser autorizado a aceder ao e-mail do utilizador e dados da empresa.  

        -   **Sem afinidade de utilizador**: O dispositivo não está afiliado a um utilizador. Utilize esta afiliação em dispositivos que efetuem tarefas sem aceder aos dados de utilizador locais. As aplicações que precisem da afiliação de utilizador não funcionam.

    Clique em **Seguinte** para continuar.  

3.  No **Device Enrollment Program** página, deixe o **programa de inscrição de dispositivos de configurar as definições para este perfil** caixa de verificação desmarcada e clique em **seguinte**.  

4.  Reveja o resumo e, em seguida, clique em **seguinte** para criar o perfil de inscrição. Clique em **Fechar** para concluir o assistente. Agora, está pronto para adicionar os números IMEI ou os números de série para os dispositivos que pretende inscrever.  

## <a name="predeclare-devices-to-enroll-with-setup-assistant"></a>Pré-declarar dispositivos para inscrição com o Assistente de configuração

Neste passo, a pré-declarar dispositivos como pertencentes ao fornecer uma lista de identificadores de hardware (números de série ou IMEI).

Para obter mais informações, consulte [pré-declarar dispositivos com o número de série IMEI e iOS](predeclare-devices-with-hardware-id.md). Quando tiver terminado com essa tarefa, regresse a esta página para continuar com o passo seguinte.

## <a name="export-the-profile-to-deploy-to-ios-devices"></a>Exportar o perfil a implementar em dispositivos iOS

1.  Na consola do Configuration Manager, vá para **ativos e compatibilidade** > **descrição geral** > **todos os dispositivos pertencentes** > **iOS** > **perfis de inscrição**.

2.  Selecione o perfil de inscrição para implementar em dispositivos móveis e clique em **exportar...** .

3.  Copie e guarde o **URL do perfil** num ficheiro pode editar.   

4.  Para suportar o Apple Configurator 2, o URL do perfil 2.0 tem de ser editada. Substitua a parte seguinte do URL:  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     com o  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```

5.  Guarde o URL do perfil editado. Irá utilizá-lo para adicionar o URL do perfil de inscrição do Apple Configurator no [secção seguinte](#step-4-prepare-the-device-with-apple-configurator).  

> [!NOTE]
> O URL do perfil de inscrição é válido durante duas semanas a partir da respetiva exportação. Após duas semanas, tem de exportar um novo URL para inscrever dispositivos iOS.

## <a name="prepare-the-device-with-apple-configurator"></a>Preparar o dispositivo com o Apple Configurator

Para preparar os dispositivos iOS para inscrição, ligue cada dispositivo a um computador Mac e carregar o perfil de inscrição para a mesma.  

> [!WARNING]  
>  Apple Configurator apaga e repõe a dispositivos para as configurações de fábrica.  

1.  Num computador Mac, abra **Apple Configurator 2**.  

2.  Na barra de menus, clique em **Apple Configurator 2** > **preferências**.  

2.  No painel de preferências, selecione **servidores** e clique no símbolo "+" por baixo do painel da esquerda para iniciar o Assistente do servidor MDM. Clique em **Seguinte**.  

3.  Introduza o **nome** e **URL de inscrição** é guardado [anterior](#step-3-export-the-profile-to-deploy-to-ios-devices). Clique em **Seguinte**.  

   > [!NOTE]
   > Se receber um aviso sobre requisitos de perfil de confiança para Apple TV, pode cancelar em segurança o **perfil de confiança** opção clicando no "X" cinzento. Também pode ignorar com segurança qualquer aviso de certificado de Âncora.

   Para continuar, clique em **seguinte** até que o assistente esteja concluído.  

4.  No **servidores** painel, clique em "Editar" ao lado do perfil do novo servidor. Certifique-se de que o URL de inscrição corresponde exatamente ao URL que introduziu anteriormente. Reintroduza o URL, se for diferente e clique em **guardar**.  

5.  Com um cabo USB, ligar-se um dispositivo iOS ao computador Mac.  

  > [!WARNING]  
  >  Este processo repõe dispositivos para as configurações de fábrica. Antes de ligar o dispositivo, reponha o dispositivo e ligue-o. Como melhor prática, o dispositivo deve estar no ecrã de Olá antes de continuar.  

6.  Clique em **preparar**. No **preparar o dispositivo iOS** painel, selecione **Manual**e, em seguida, clique em **seguinte**.  

7.  No **inscrever no servidor MDM** painel, selecione o servidor de nomes que criou e, em seguida, clique em **seguinte**.  

9. No **criar uma organização** painel, escolha o **organização** ou crie uma nova organização e, em seguida, clique em **seguinte**.  

10. No **configurar Assistente de configuração iOS** painel, escolha os passos para apresentar ao utilizador e, em seguida, clique em **preparar**. Se lhe for pedido, autentique para atualizar as definições de fidedignidade.  

11. Quando terminar, pode desligar o cabo USB.  

Repita estes passos para todos os dispositivos que pretende preparar para a inscrição.

## <a name="distribute-devices"></a>Distribuir dispositivos

Os dispositivos estão agora prontos para a inscrição na empresa. Desligue os dispositivos e distribua-os pelos utilizadores. Quando o dispositivo estiver ativado, através do Assistente de configuração irá iniciar e solicitar ao utilizador para a respetiva conta escolar ou profissional para iniciar a inscrição.

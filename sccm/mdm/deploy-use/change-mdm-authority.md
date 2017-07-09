---
title: Alterar sua autoridade MDM | Microsoft Docs
description: "Saiba como alterar a autoridade MDM do Configuration Manager (híbrido) para o Intune autônomo ou vice-versa."
keywords: 
author: dougeby
manager: angrobe
ms.date: 06/02/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.translationtype: Machine Translation
ms.sourcegitcommit: 662901e850566756759fcfc61c58f3c0e56bc5aa
ms.openlocfilehash: b80fec937b50dca3ab995be281c44c3145300f9f
ms.contentlocale: pt-pt
ms.lasthandoff: 06/03/2017


---
# <a name="change-your-mdm-authority"></a>Alterar sua autoridade MDM
A partir do Configuration Manager versão 1610 e Microsoft Intune version 1705, você pode alterar sua autoridade MDM sem precisar entrar em contato com o Microsoft Support e sem a necessidade de cancelar o registro e registrar novamente os dispositivos gerenciados existentes.

## <a name="change-the-mdm-authority-to-intune-standalone"></a>Alterar a autoridade MDM como Intune autônomo
Use esta seção para alterar um locatário existente do Microsoft Intune configurado no console do Configuration Manager (híbrido) ao Intune autônomo, sem a necessidade de cancelar o registro e registrar novamente os dispositivos gerenciados existentes.

### <a name="key-considerations"></a>Considerações importantes
Depois de alterar para a nova autoridade MDM, provavelmente haverá tempo de transição (até 8 horas) antes do dispositivo verifica e sincroniza com o serviço. Será necessário configurar a autoridade MDM novo (Intune autônomo) para garantir que os dispositivos continuarão a ser gerenciado e protegido após a alteração. Tenha em atenção o seguinte:
- Dispositivos devem se conectar com o serviço após a alteração para que as configurações da autoridade de MDM novo (Intune autônomo) substituirá as configurações existentes no dispositivo.
- Depois de alterar a autoridade MDM, algumas das configurações básicas (como perfis) da autoridade de MDM anterior (híbrido) permanecem no dispositivo por até 7 dias. É recomendável que você configure aplicativos e configurações (políticas, perfis, aplicativos, etc.) na autoridade de MDM novo, assim que possível e implanta as configurações para os grupos de usuários que contém usuários que têm dispositivos registrados existentes. Assim que um dispositivo se conecta ao serviço após a alteração na autoridade MDM, ele receber as novas configurações da autoridade de MDM novo e evitar falhas na proteção e gerenciamento. As políticas de destino recentemente substituirão as políticas existentes no dispositivo.
- Após você alterar para a nova autoridade MDM, os dados de conformidade no console de administração do Microsoft Intune poderá levar até uma semana para relatar com precisão. No entanto, os estados de conformidade no Azure Active Directory e do dispositivo serão precisos para que o dispositivo ainda será protegido.

### <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Preparar para alterar a autoridade MDM para o Intune autônomo
Examine as informações a seguir para preparar para a alteração para a autoridade MDM:
- Você deve ter o Configuration Manager versão 1610 ou superior para a opção para alterar a autoridade MDM esteja disponível.
- Pode levar até 8 horas para um dispositivo conectar-se ao serviço após você alterar para a nova autoridade MDM.
- Verifique se todos os usuários que estão sendo gerenciados pelo híbrido tem uma licença do Intune/EMS especificamente atribuída a eles antes da alteração na autoridade MDM. Isso irá garantir que o usuário e seus dispositivos serão gerenciados pelo Intune autônomo após a alteração na autoridade MDM. Para obter mais informações, consulte [Intune atribuir licenças às suas contas de usuário](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Certifique-se de que a conta de usuário de administrador tem uma licença do EMS/Intune atribuída e confirme que a conta de usuário administrador pode entrar no Intune antes da alteração para a autoridade MDM. A autoridade de MDM deve exibir **definida para o Configuration Manager** (locatário híbrido) no console de administração do Microsoft Intune antes da alteração na autoridade MDM.
- No console do Configuration Manager, remova todas as funções do Gerenciador de registro do dispositivo. Vá para **administração** > **serviços de nuvem** > **assinaturas do Microsoft Intune**, selecione a assinatura do Microsoft Intune, clique em **propriedades**, clique no **Gerenciador de registro de dispositivo** guia e remova todas as funções do Gerenciador de registro do dispositivo.
- No console do Configuration Manager, remova as categorias de dispositivo existentes. Vá para **ativos e conformidade** > **visão geral** > **coleções de dispositivos**, escolha **gerenciar categorias de dispositivo**e remover categorias de dispositivo existentes.
- Não deve haver nenhum impacto perceptível para os usuários finais durante a alteração na autoridade MDM. No entanto, você talvez queira comunicar esta alteração aos usuários para certificar-se de que seus dispositivos estejam ligados e que eles se conectam com o serviço logo após a alteração. Isso garantirá que a tantos dispositivos possível se conectar e registrar com o serviço por meio da nova autoridade assim que possível.
- Se você estiver usando o Configuration Manager (locatário híbrido) para gerenciar dispositivos iOS antes da alteração na autoridade MDM, você deve garantir que o mesmo certificado de serviço (APNs) Apple Push Notification que era usado no Configuration Manager é renovado e usado para configurar o locatário novamente no Intune autônomo.    
    > [!IMPORTANT]  
    > Se um certificado de APNs diferente for usado para o Intune autônomo, já registrado anteriormente todos os dispositivos iOS ficará não registrados e você precisará passar pelo processo de registrar novamente-los. Antes de fazer com que a autoridade MDM alterar, certifique-se de que você saiba exatamente qual certificado APNs foi usado para gerenciar dispositivos iOS no Configuration Manager. Localizar o mesmo certificado listado no Portal certificados por Push da Apple (https://identity.apple.com) e verifique se o usuário cuja ID Apple usada para criar o certificado APNs original é identificado e disponível para renovar o certificado APNs mesmo como parte da mudança para a novo autoridade MDM.  

### <a name="change-the-mdm-authority-to-intune-standalone"></a>Alterar a autoridade MDM como Intune autônomo
O processo para alterar a autoridade MDM para o Intune autônomo inclui as seguintes etapas de alto nível:  
- No console do Configuration Manager, use o **autoridade de MDM de alteração para o Microsoft Intune** opção para remover a assinatura do Microsoft Intune existente.
- No console de administração do Microsoft Intune, defina a autoridade MDM novo como **Intune**.
- Configure o certificado Apple APNs usando o mesmo certificado de APNs que você renovada.
- No console de administração do Microsoft Intune, configurar e implantar novas configurações e aplicativos da autoridade de MDM novo (Intune).
- Os dispositivos de tempo Avançar conectam ao serviço, ele sincronizar e receber as novas configurações da autoridade MDM de novo.

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>Para alterar a autoridade MDM para o Intune autônomo
1.    No console do Configuration Manager, vá para **administração** &gt; **visão geral** &gt; **serviços de nuvem** &gt; **assinatura do Microsoft Intune**e excluir sua assinatura do Intune existente.
2.    Selecione **autoridade de MDM de alteração para o Microsoft Intune**e, em seguida, clique em **próximo**.

    ![Baixar a solicitação de certificado APNs](/sccm/mdm/deploy-use/media/mdm-change-delete-subscription.png)
3.    Entrar para o locatário do Intune que você usou originalmente quando você definir a autoridade MDM no Configuration Manager.
4.    Clique em **Seguinte** e conclua o assistente.
5.    A autoridade MDM agora é redefinida. A assinatura do Intune não devem ser exibida no nó assinaturas do Microsoft Intune do console do Configuration Manager.
6.    Logon para o [console de administração do Microsoft Intune](http://manage.microsoft.com) usando o mesmo locatário do Intune utilizado antes.
7.    Confirme se a autoridade MDM foi redefinida e, em seguida, defina a autoridade MDM como **Microsoft Intune**. Depois de alterar a autoridade MDM, você verá que ele esteja refletido no console do. Para obter mais informações, consulte [como definir a autoridade MDM](https://docs.microsoft.com/en-us/intune/deploy-use/prerequisites-for-enrollment#step-2-set-mdm-authority).
<!-- [Azure portal](https://docs.microsoft.com/en-us/intune-azure/enroll-devices/set-mdm-authority) -->


### <a name="configure-the-apns-certificate"></a>Configurar o certificado APNs
Quando você tiver dispositivos iOS, você deve configurar o certificado APNs no Intune.

#### <a name="to-configure-the-apns-certificate"></a>Para configurar o certificado APNs
1.    Baixe a solicitação de certificado de APNs.
    <!--The process is different depending on how you connect to Intune:
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment** &gt; **Apple MDM Push Certificate**, and then select **Download your CSR** to download and save the .csr file locally.   
    <br/>
    **Microsoft Intune administration console**   -->
    No [console de administração do Microsoft Intune](http://manage.microsoft.com), vá para **administração** &gt; **gerenciamento de dispositivo móvel** &gt; **iOS e Mac OS X** &gt; **carregar um certificado APNs**e, em seguida, escolha **baixar a solicitação de certificado APNs**. Guarde o ficheiro de pedido de assinatura de certificado (.csr) localmente.
    > [!IMPORTANT]    
    > Você deve baixar um nova solicitação de assinatura de certificado. Não use um arquivo existente ou falhará.

    ![Baixar a solicitação de certificado APNs](/sccm/mdm/deploy-use/media/mdm-change-download-apns-certificate.png)

2.    Vá para o [Portal certificados por Push da Apple](http://go.microsoft.com/fwlink/?LinkId=269844)e entre com a **mesmo** ID da Apple que foi usada anteriormente, criar e renovar o certificado de APNs que você usou no Configuration Manager (híbrido).

    ![Na página de entrada do Portal de certificados por Push da Apple](/sccm/mdm/deploy-use/media/mdm-change-apns-portal.png)

3.    Selecione o certificado de APNs que você usou no Configuration Manager (híbrido) e, em seguida, clique em **renovar**.   

    ![Renovar a caixa de diálogo de APNs](/sccm/mdm/deploy-use/media/mdm-change-renew-apns.png)

4.    Selecione o certificado de APNs assinatura de arquivo (. CSR) da solicitação que você baixou localmente e, em seguida, clique em **carregar**.

    ![Na página de entrada do Portal de certificados por Push da Apple](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)  
5.    Selecione os APNs mesmo e, em seguida, clique em **baixar**. Baixe o certificado APNs (. PEM) e salve o arquivo localmente.  

    ![Na página de entrada do Portal de certificados por Push da Apple](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-download.png)

6.    Carregue o certificado APNs renovado para o locatário do Intune usando a mesma ID Apple que antes.
<!--The process is different depending on how to connect to Intune:  
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment**  &gt; **Apple MDM Push Certificate**, enter your Apple ID in step 3, select the certificate (.pem) file in step 4, and then click **Upload**.     
    <br/>
    **Microsoft Intune administration console**    -->
    In the [Microsoft Intune administration console](http://manage.microsoft.com), go to **Administration** &gt; **Mobile Device Management** &gt; **iOS and Mac OS X** &gt; **Upload an APNs Certificate**, and then choose **Upload the APNs certificate**. Go to the certificate (.pem) file, choose **Open**, and then enter your **Apple ID**.   

    ![Upload the APNs certificate](/sccm/mdm/deploy-use/media/mdm-change-upload-apns-certificate.png)

### <a name="next-steps"></a>Passos seguintes
Depois que a alteração na autoridade MDM for concluída, examine as seguintes etapas:
- Quando o serviço Intune detecta que a autoridade MDM do locatário foi alterado, ele enviará uma mensagem de notificação a todos os dispositivos registrados para check-in e sincronizar com o serviço (isso está fora do check-in agendado regularmente). Portanto, depois que a autoridade MDM para o locatário foi alterada de híbrida ao Intune autônomo, todos os dispositivos que estejam ligados e online se conecta ao serviço, receber a nova autoridade MDM e ser gerenciado pelo Intune autônomo no futuro. Não haverá nenhuma interrupção para o gerenciamento e proteção desses dispositivos.
- Dispositivos que estão desativadas ou offline durante a (ou logo após) a alteração na autoridade MDM se conectará ao e sincronizar com o serviço na nova autoridade MDM quando eles estejam ligados e online.  

  dispositivos iOS exigem mais tempo para renovar e configurar o certificado APNs. Portanto, os dispositivos iOS não receberá a solicitação de verificação inicial. Mesmo se os dispositivos iOS estão ligadas e online durante (ou logo após) a alteração na autoridade MDM, haverá um atraso de até 8 horas (dependendo do tempo do que o próximo regular check-in agendado) antes de dispositivos são registrados com o serviço sob a nova autoridade MDM do iOS.    

  > [!IMPORTANT]
  > Entre o momento quando você altera o MDM autoridade e quando o certificado APNs renovado é carregado para o novo autoridade, novos registros de dispositivo e seleção de dispositivo para dispositivos iOS falharão. Portanto, é importante que você analise e carregue o certificado APNs para a novo autoridade assim que possível após a alteração na autoridade MDM.   

- Os usuários podem alterar rapidamente à autoridade de MDM novo iniciando manualmente um check-in do dispositivo para o serviço. Os usuários podem fazer isso facilmente usando o aplicativo de Portal da empresa e iniciar uma verificação de conformidade do dispositivo.
- Para validar que as coisas estão funcionando corretamente depois dispositivos ter check-in e sincronizados com o serviço após a alteração na autoridade MDM, procure os dispositivos de [console de administração do Microsoft Intune](http://manage.microsoft.com). Os dispositivos que foram anteriormente gerenciados pelo Configuration Manager (híbrido) agora serão exibidos como dispositivos gerenciados.    
- Há um período provisório quando um dispositivo estiver offline durante a alteração na autoridade MDM e quando o dispositivo verifica com o serviço. Para ajudar a garantir que o dispositivo permanece protegido e funcional durante esse período provisório, o seguinte permanecerão no dispositivo por até 7 dias (ou até que o dispositivo se conecta com a autoridade MDM novo e recebe novas configurações que substituirão os existentes):
    - Perfil de email
    - Perfil de VPN
    - Perfil de certificado
    - Perfil de Wi-Fi
    - Perfis de configuração
- Verifique se as novas configurações que se destinam para substituir as configurações existentes têm o mesmo nome que os anteriores para garantir que as configurações antigas serão substituídas. Caso contrário, os dispositivos podem acabar com políticas e perfis de redundância.
    > [!TIP]   
    > Como prática recomendada, você deve criar todas as configurações de gerenciamento e configurações, bem como implantações, logo após a alteração para a autoridade MDM foi concluída. Isso ajuda a garantir que os dispositivos estão protegidos e gerenciados ativamente durante o período de intermediários.   
-  Depois de alterar a autoridade MDM, execute as etapas a seguir para validar que novos dispositivos são registrados com êxito para a autoridade de novo:   
    - Registrar um novo dispositivo
    - Verifique se que o dispositivo registrado recentemente aparece no console de administração do Intune.
    - Execute uma ação, como bloqueio remoto do console de administração para o dispositivo. Se for bem-sucedida, o dispositivo está sendo gerenciado pela autoridade MDM de novo.
- Se você tiver problemas com dispositivos específicos, você pode cancelar o registro e registrar novamente os dispositivos para obtê-los conectado à autoridade de novo e gerenciadas mais rápido possível.

<!-- After the change in MDM authority and devices check-in with the service, note the following:      - The updated compliance status of devices will only display in the Azure portal immediately.
- There will be a delay for compliance status of devices to display in the Intune administrative console.-->


## <a name="change-the-mdm-authority-to-configuration-manager-hybrid"></a>Alterar a autoridade MDM para o Configuration Manager (híbrido)
Use esta seção para alterar um locatário existente do Microsoft Intune configurado do Intune e com a autoridade MDM definido como **Microsoft Intune** (autônomo) para **do Configuration Manager** (híbrido) sem precisar cancelar o registro e registrar novamente existente dispositivos gerenciados.

### <a name="key-considerations"></a>Considerações importantes
Depois que você alternar para a nova autoridade MDM, provavelmente haverá tempo de transição (até 8 horas) antes do dispositivo verifica e sincroniza com o serviço. Será necessário configurar a autoridade MDM novo (híbrido) para garantir que os dispositivos continuarão a ser gerenciado e protegido após a alteração. Tenha em atenção o seguinte:
- Dispositivos devem se conectar com o serviço após a alteração para que as configurações da autoridade de MDM novo (Intune autônomo) substituirá as configurações existentes no dispositivo.
- Depois de alterar a autoridade MDM, algumas das configurações básicas (como perfis) da autoridade de MDM anterior (Intune autônomo) permanecerão no dispositivo por até 7 dias ou até que o dispositivo se conecta ao serviço pela primeira vez. É recomendável que você configure aplicativos e configurações (políticas, perfis, aplicativos, etc.) na autoridade de MDM novo (híbrido), assim que possível e implanta as configurações para os grupos de usuários que contém usuários que têm dispositivos registrados existentes. Assim que um dispositivo se conecta ao serviço após a alteração na autoridade MDM, ele receber as novas configurações da autoridade de MDM novo e evitar falhas na proteção e gerenciamento.

### <a name="prepare-to-change-the-mdm-authority-to-configuration-manager-hybrid"></a>Preparar para alterar a autoridade MDM para o Configuration Manager (híbrido)
Examine as informações a seguir para preparar para a alteração para a autoridade MDM:
- Você deve ter o Configuration Manager versão 1610 ou superior para a opção para alterar a autoridade MDM esteja disponível.
- Pode levar até 8 horas para um dispositivo conectar-se ao serviço após você alterar para a nova autoridade MDM.
- Crie uma coleção de usuário do Configuration Manager com todos os usuários atualmente gerenciados pelo Intune Standalone que será usada quando você configura a assinatura do Intune no console do Configuration Manager. Isso ajuda a garantir que seus dispositivos e o usuário terão uma licença do Configuration Manager atribuída e ser gerenciados no ambiente de híbrida após a alteração para a autoridade MDM.
- Certifique-se de que o usuário do administrador de TI está nesta coleção de usuário muito.  
- Antes da alteração, a autoridade MDM mostrará como **definida como Microsoft Intune** (autônomo) no console de administração do Intune.
- A autoridade de MDM deve exibir **definida como Microsoft Intune** (independente de locatário) no console de administração do Microsoft Intune antes da alteração na autoridade MDM.
    > [!NOTE]    
    > Se sua autoridade MDM exibe **gerenciado pelo Intune e Office 365**, em seguida, o Office 365 dispositivos gerenciados do MDM não serão gerenciados quando você alterar sua autoridade MDM como **do Configuration Manager** (híbrido). É recomendável que você licenças aos usuários para o Intune ou Enterprise Mobility Suite antes de alterar a autoridade MDM.   

- No [console de administração do Microsoft Intune](http://manage.microsoft.com), remova a função de Gerenciador de registro do dispositivo. Para obter detalhes, consulte [excluir um Gerenciador de registro de dispositivo do Intune](/intune-classic/deploy-use/enroll-corporate-owned-devices-with-the-device-enrollment-manager-in-microsoft-intune#delete-a-device-enrollment-manager-from-intune).
- Desative a qualquer mapeamento de grupo de dispositivos que está configurado. Para obter detalhes, consulte [categorizar os dispositivos com o mapeamento do grupo de dispositivos no Microsoft Intune](/intune-classic/deploy-use/categorize-devices-with-device-group-mapping-in-microsoft-intune).
- Não deve haver nenhum impacto perceptível para os usuários finais durante a alteração na autoridade MDM. No entanto, você talvez queira comunicar esta alteração aos usuários para certificar-se de que seus dispositivos estejam ligados e que eles se conectam com o serviço logo após a alteração. Isso garantirá que a tantos dispositivos possível se conectar e registrar com o serviço por meio da nova autoridade assim que possível.
- Se você estiver usando o Intune autônomo para gerenciar dispositivos iOS antes da alteração na autoridade MDM, você deve garantir que o mesmo certificado de serviço (APNs) da Apple Push Notification que foi usado anteriormente no Intune é renovado e usado para configurar o locatário novamente no Configuration Manager (híbrido).    

    > [!IMPORTANT]  
    > Se um certificado APNs diferente for usado para híbrido, já registrado anteriormente todos os dispositivos iOS ficará não registrados e você precisará passar pelo processo de registrar novamente-los. Antes de fazer com que a autoridade MDM alterar, certifique-se de que você saiba exatamente qual certificado APNs foi usado para gerenciar dispositivos iOS no Intune. Localizar o mesmo certificado listado no Portal certificados por Push da Apple (https://identity.apple.com) e verifique se o usuário cuja ID Apple usada para criar o certificado APNs original é identificado e disponível para renovar o certificado APNs mesmo como parte da mudança para a novo autoridade MDM.  

### <a name="change-the-mdm-authority-to-configuration-manager"></a>Alterar a autoridade MDM para o Configuration Manager
O processo para alterar a autoridade MDM para o Configuration Manager (híbrido) inclui as seguintes etapas de alto nível:  
- No console do Configuration Manager, adicione a assinatura do Microsoft Intune.
- Configure o certificado Apple APNs usando o mesmo certificado de APNs que você renovada.
- No console do Configuration Manager, configurar e implantar novas configurações e aplicativos da autoridade de MDM novo (híbrido).
- Os dispositivos de tempo Avançar conectam ao serviço, ele sincronizar e receber as novas configurações da autoridade MDM de novo.

#### <a name="to-change-the-mdm-authority-to-configuration-manager"></a>Para alterar a autoridade MDM para o Configuration Manager
1.    No console do Configuration Manager, vá para **administração** &gt; **visão geral** &gt; **serviços de nuvem** &gt; **assinatura do Microsoft Intune**e selecione Adicionar uma assinatura do Intune.
2.    Entrar para o locatário do Intune que você usou originalmente quando você definir a autoridade MDM do Intune e clique em **próximo**.
3.    Selecione **alterar minha autoridade MDM para o Configuration Manager**e clique em **próximo**.
4.  Selecione a coleção de usuário que irá conter todos os usuários que continuarão a ser gerenciado pelo novo híbridos autoridade MDM.
5.  Clique em **Seguinte** e conclua o assistente.  
5.    A autoridade MDM foi alterada para **do Configuration Manager**.
6.    Logon para o [console de administração do Microsoft Intune](http://manage.microsoft.com) usando o Intune mesmo locatário e confirme que a autoridade MDM foi alterada para **definida para o Configuration Manager**.


### <a name="enable-ios-enrollment"></a>Habilitar o registro do iOS
Quando você tiver dispositivos iOS, você deve configurar o certificado APNs no Configuration Manager.

#### <a name="to-enable-ios-enrollment-and-configure-the-apns-certificate"></a>Para habilitar o registro do iOS e configurar o certificado APNs

1. **Baixar uma solicitação de assinatura de certificado**

    1.  No console do Configuration Manager, vá para **administração** &gt; **serviços de nuvem** &gt; **assinaturas do Microsoft Intune**e selecione **solicitação de certificado APNs criar** para abrir o **solicitação Apple Push notificação certificado de assinatura de solicitação de serviço** caixa de diálogo.  
    2.  **Navegue** para o caminho onde pretende guardar o ficheiro de pedido de assinatura de certificado novo (.csr). Guarde o ficheiro de pedido de assinatura de certificado (.csr) localmente.  
    3.  Clique em **Transferir**. O novo ficheiro .csr do Microsoft Intune é transferido e guardado pelo Configuration Manager.   

    > [!IMPORTANT]
    > Você deve baixar um nova solicitação de assinatura de certificado. Não use um arquivo existente ou falhará.  

2.    Vá para o [Portal certificados por Push da Apple](http://go.microsoft.com/fwlink/?LinkId=269844)e entre com a **mesmo** ID da Apple que foi usada anteriormente, criar e renovar o certificado de APNs que você usou no Intune autônomo.

    ![Na página de entrada do Portal de certificados por Push da Apple](/sccm/mdm/deploy-use/media/mdm-change-apns-portal.png)

3.    Selecione o certificado de APNs que você usou no Intune autônomo e, em seguida, clique em **renovar**.   

    ![Renovar a caixa de diálogo de APNs](/sccm/mdm/deploy-use/media/mdm-change-renew-apns.png)

4.    Selecione o certificado de APNs assinatura de arquivo (. CSR) da solicitação que você baixou localmente e, em seguida, clique em **carregar**.

    ![Na página de entrada do Portal de certificados por Push da Apple](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)  
5.    Selecione os APNs mesmo e, em seguida, clique em **baixar**. Baixe o certificado APNs (. PEM) e salve o arquivo localmente.  

    ![Na página de entrada do Portal de certificados por Push da Apple](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-download.png)

6.    Carregue o certificado APNs renovado para o locatário híbrida usando a mesma ID Apple que antes.

    1.  No console do Configuration Manager, vá para **administração** &gt; **serviços de nuvem** &gt; **assinatura do Microsoft Intune**e escolha **configurar plataformas** &gt; **iOS**.  
    2.  No **propriedades de assinatura do Microsoft Intune** caixa de diálogo, selecione o **certificado APNs** guia e clique para selecionar o **habilitar registro em iOS e MAC OS X (MDM)** caixa de seleção.  
    3.  Clique em **Procurar**e aceda ao ficheiro do certificado APNs (.cer) transferido a partir da Apple. O Configuration Manager apresenta as informações do certificado APNs. Clique em **OK** para guardar o certificado APNs no Intune.  

        ![Página de propriedades de assinatura do Intune - iOS](/sccm/mdm/deploy-use/media/mdm-change-subscription-properties-ios.png)

### <a name="enable-android-enrollment"></a>Habilitar o registro do Android
1. No console do Configuration Manager, vá para **administração** &gt; **serviços de nuvem** &gt; **assinatura do Microsoft Intune**e escolha **configurar plataformas** &gt; **Android**.  
2. Selecione **habilitar registro do Android** e clique em **Okey**.

### <a name="enable-windows-enrollment"></a>Habilitar o registro do Windows
1. No console do Configuration Manager, vá para **administração** &gt; **serviços de nuvem** &gt; **assinatura do Microsoft Intune**e escolha **configurar plataformas** &gt; **Windows**.  
2. Selecione **habilitar registro do Windows** e clique em **Okey**.

### <a name="enable-windows-phone-enrollment"></a>Habilitar o registro do Windows Phone
1. No console do Configuration Manager, vá para **administração** &gt; **serviços de nuvem** &gt; **assinatura do Microsoft Intune**e escolha **configurar plataformas** &gt; **do Windows Phone**.  
2. Selecione a plataforma que você deseja habilitar e clique em **Okey**.


### <a name="next-steps"></a>Passos seguintes
Depois que a alteração na autoridade MDM for concluída, examine as seguintes etapas:
- Quando o serviço Intune detecta que a autoridade MDM do locatário foi alterado, ele enviará uma mensagem de notificação a todos os dispositivos registrados para check-in e sincronizar com o serviço (isso está fora do check-in agendado regularmente). Portanto, depois que a autoridade MDM para o locatário foi alterada do Intune autônomo para híbrida, todos os dispositivos que estejam ligados e online se conecta ao serviço, receber a nova autoridade MDM e ser gerenciado pelo híbrido no futuro. Não haverá nenhuma interrupção para o gerenciamento e proteção desses dispositivos.
- Mesmo para dispositivos que estão ativados e online durante (ou logo após) a alteração na autoridade MDM, haverá haverá um atraso de até 8 horas (dependendo do tempo do que o próximo regular check-in agendado) antes de dispositivos que estão registrados com o serviço sob a nova autoridade MDM.    

  > [!IMPORTANT]
  > Entre o momento quando você altera o MDM autoridade e quando o certificado APNs renovado é carregado para o novo autoridade, novos registros de dispositivo e seleção de dispositivo para dispositivos iOS falharão. Portanto, é importante que você analise e carregue o certificado APNs para a novo autoridade assim que possível após a alteração na autoridade MDM.

- Os usuários podem alterar rapidamente à autoridade de MDM novo iniciando manualmente um check-in do dispositivo para o serviço. Os usuários podem fazer isso facilmente usando o aplicativo de Portal da empresa e iniciar uma verificação de conformidade do dispositivo.
- Para validar que as coisas estão funcionando corretamente depois dispositivos ter check-in e sincronizados com o serviço após a alteração na autoridade MDM, procure os dispositivos do console do Configuration Manager. Os dispositivos que foram anteriormente gerenciados pelo Intune agora serão exibidos como dispositivos gerenciados no console do Configuration Manager.    
- Há um período provisório quando um dispositivo estiver offline durante a alteração na autoridade MDM e quando o dispositivo verifica com o serviço. Para ajudar a garantir que o dispositivo permanece protegido e funcional durante esse período provisório, o seguinte permanecerão no dispositivo por até 7 dias (ou até que o dispositivo se conecta com a autoridade MDM novo e recebe novas configurações que substituirão os existentes):
    - Perfil de email
    - Perfil de VPN
    - Perfil de certificado
    - Perfil de Wi-Fi
    - Perfis de configuração
- Após você alterar para a nova autoridade MDM, os dados de conformidade no console de administração do Microsoft Intune poderá levar até uma semana para relatar com precisão. No entanto, os estados de conformidade no Azure Active Directory e do dispositivo serão precisos para que o dispositivo ainda será protegido.
- Verifique se as novas configurações que se destinam para substituir as configurações existentes têm o mesmo nome que os anteriores para garantir que as configurações antigas serão substituídas. Caso contrário, os dispositivos podem acabar com políticas e perfis de redundância.
    > [!TIP]   
    > Como prática recomendada, você deve criar todas as configurações de gerenciamento e configurações, bem como implantações, logo após a alteração para a autoridade MDM foi concluída. Isso ajuda a garantir que os dispositivos estão protegidos e gerenciados ativamente durante o período de intermediários.   
-  Depois de alterar a autoridade MDM, execute as etapas a seguir para validar que novos dispositivos são registrados com êxito para a autoridade de novo:   
    - Registrar um novo dispositivo
    - Verifique se que o dispositivo registrado recentemente aparece no console do Configuration Manager.
    - Execute uma ação, como bloqueio remoto do console de administração para o dispositivo. Se for bem-sucedida, o dispositivo está sendo gerenciado pela autoridade MDM de novo.
- Se você tiver problemas com dispositivos específicos, você pode cancelar o registro e registrar novamente os dispositivos para obtê-los conectado à autoridade de novo e gerenciadas mais rápido possível.


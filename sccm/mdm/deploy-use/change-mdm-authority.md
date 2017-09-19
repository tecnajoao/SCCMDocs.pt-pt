---
title: Alterar a autoridade de MDM | Microsoft Docs
description: "Saiba como alterar a autoridade de MDM do Configuration Manager (híbrido) para o Intune autónomo ou vice-versa."
keywords: 
author: dougeby
manager: angrobe
ms.date: 09/14/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: d24e6e736397a4612db7b47e997d8cb1f97c4de9
ms.sourcegitcommit: 948644072bd158b156f782a4376bcd50fac7c73a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/14/2017
---
# <a name="change-your-mdm-authority"></a>Alterar a autoridade de MDM
A partir do Configuration Manager versão 1610, pode alterar a autoridade de MDM sem ter de contactar o Support da Microsoft e sem ter de anular a inscrição e inscrever-se novamente os seus dispositivos geridos existentes. Este tópico fornece os passos para alterar um inquilino do Microsoft Intune existente configurado na consola do Configuration Manager (híbrido) para o Intune autónomo.

> [!Important]    
> Este tópico é para alterar a sua autoridade MDM não tenha sido anteriormente migrados os utilizadores. Para alterar a autoridade de MDM, depois de ter [migrado um subconjunto de utilizadores](migrate-hybridmdm-to-intunesa.md), consulte [alterar a autoridade de MDM](migrate-change-mdm-authority.md).

## <a name="key-considerations"></a>Considerações-chave
Depois de alterar para a autoridade de MDM novo, há será provavelmente ser hora de transição (até oito horas) antes do dispositivo ser registado e sincroniza com o serviço. Tem de configurar as definições no novo autoridade de MDM (Intune autónomo) para garantir que os dispositivos inscritos continuam a ser geridos e protegido após a alteração. Tenha em atenção as seguintes considerações:
- Dispositivos tem de ligar com o serviço após a alteração, para que as definições da autoridade de MDM novo (Intune autónomo) substitui as definições existentes no dispositivo.
- Depois de alterar a autoridade de MDM, algumas das definições básicas (por exemplo, perfis) da autoridade de MDM anterior (híbrido) permanecem no dispositivo até sete dias. Recomenda-se que configura as aplicações e definições (políticas, perfis, aplicações, etc.) na autoridade MDM novo logo que possível. Além disso, implemente as definições para os grupos de utilizadores que contêm os utilizadores que possuem dispositivos já inscritos. Quando um dispositivo se liga ao serviço após a alteração na autoridade de MDM, este recebe novas definições da autoridade MDM de novo. As políticas de destino recentemente irão substituir as políticas existentes no dispositivo.
- Depois de alterar para a nova autoridade de MDM, os dados de conformidade na consola de administração do Microsoft Intune podem demorar até uma semana comuniquem com precisão. No entanto, os Estados de compatibilidade no Azure Active Directory e o dispositivo será precisos para que o dispositivo ainda será protegido.
- Dispositivos que não tem utilizadores associados (normalmente, quando tiver iOS Device Enrollment Program ou efetuar a cenários de inscrição em massa) não são migrados para a autoridade de MDM de novo. Para os dispositivos, tem de chamar o suporte para obter ajuda para movê-los para a autoridade de MDM de novo.

## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Preparar para alterar a autoridade de MDM ao Intune autónomo
Reveja as informações seguintes para se preparar para a alteração à autoridade de MDM:
- Tem de ter o Configuration Manager versão 1610 ou superior para a opção para alterar a autoridade de MDM para estar disponível.
- Pode demorar até oito horas para um dispositivo para ligar ao serviço depois de alterar para a autoridade de MDM de novo.
- Certifique-se de que todos os utilizadores que sejam atualmente geridos pelo híbrida ter uma licença do Intune/EMS atribuída antes da alteração na autoridade de MDM. Ter a licença assegura que o utilizador e os respetivos dispositivos são geridos pelo Intune autónomo após a alteração na autoridade de MDM. Para obter mais informações, consulte [licenças do Intune atribuir às suas contas de utilizador](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Certifique-se de que a conta de utilizador de administrador tem uma licença do Intune/EMS atribuída e confirme que a conta de utilizador administrador pode iniciar sessão no Intune antes da alteração para a autoridade de MDM. A autoridade de MDM deve apresentar **definida para o Configuration Manager** (inquilino híbrida) na consola de administração do Microsoft Intune antes da alteração na autoridade de MDM.
- Na consola do Configuration Manager, remova todas as funções do Gestor de inscrição de dispositivos. Aceda a **administração** > **serviços em nuvem** > **subscrições do Microsoft Intune**, selecione a subscrição do Microsoft Intune, clique em **propriedades**, clique em de **Gestor de inscrição de dispositivos** separador e remova todas as funções do Gestor de inscrição de dispositivos.
- Na consola do Configuration Manager, remova as categorias de dispositivos existentes. Aceda a **ativos e compatibilidade** > **descrição geral** > **coleções de dispositivos**, escolha **gerir categorias de dispositivo**e remover as categorias de dispositivos existentes.
- Não deverá haver nenhum impacto considerável aos utilizadores finais durante a alteração na autoridade de MDM. 
- Se estiver a utilizar o Configuration Manager (inquilino híbrida) para gerir dispositivos iOS antes da alteração na autoridade de MDM, tem de se certificar de que o mesmo certificado de serviço (APNs) da notificação Push da Apple que foi utilizado anteriormente no Configuration Manager é renovado e utilizado para configurar o inquilino novamente no Intune autónomo.

   > [!IMPORTANT]  
   > Se outro certificado do APNs é utilizado para o Intune autónomo, em seguida, inscrito anteriormente todos os dispositivos iOS deixará de estar não inscritos e terá de percorrer o processo de se registá-los. Antes de efetuar a alteração de autoridade de MDM, certifique-se de que sabe exatamente o certificado do APNs foi utilizado para gerir dispositivos iOS no Configuration Manager. Localizar o mesmo certificado listado no Portal Apple Push Certificates (https://identity.apple.com) e certifique-se o utilizador cujo ID Apple utilizado para criar o certificado do APNs original foi identificado e está disponível para renovar o certificado do APNs mesmo como parte da alteração à autoridade MDM de novo.  

## <a name="change-the-mdm-authority-to-intune-standalone"></a>Alterar a autoridade de MDM ao Intune autónomo
O processo para alterar a autoridade de MDM ao Intune autónomo inclui os seguintes passos de alto nível:  
- Na consola do Configuration Manager, utilize o **autoridade de MDM de alteração para o Microsoft Intune** opção para remover a subscrição existente do Microsoft Intune.
- Na consola de administração do Microsoft Intune, defina a autoridade MDM novo para **Intune**.
- Configure o certificado do APNs da Apple utilizando o mesmo certificado de APNs é renovado.
- Na consola de administração do Microsoft Intune, configurar e implementar as novas definições e aplicações a partir da autoridade de MDM novo (Intune).
- Os dispositivos de hora seguintes ligam ao serviço, irá sincronizar e receber as novas definições da autoridade MDM de novo.

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>Para alterar a autoridade de MDM ao Intune autónomo
1. Na consola do Configuration Manager, vá para **administração** &gt; **descrição geral** &gt; **serviços em nuvem** &gt; **subscrição do Microsoft Intune**e eliminar a sua subscrição do Intune existente.
2. Selecione **autoridade de MDM de alteração para o Microsoft Intune**e, em seguida, clique em **seguinte**.
   ![Transferir o pedido de certificado do APNs](./media/mdm-change-delete-subscription.png)
3. Iniciar sessão para o inquilino do Intune que utilizou originalmente quando definir a autoridade de MDM no Configuration Manager.
4. Clique em **Seguinte** e conclua o assistente.
5. A autoridade de MDM é reposta. A subscrição do Intune já não deverá ser apresentada no nó de subscrições do Microsoft Intune da consola do Configuration Manager.
6. Início de sessão para o [consola de administração do Microsoft Intune](http://manage.microsoft.com) utilizar o mesmo inquilino do Intune que utilizou anteriormente.
7. Confirme que a autoridade de MDM foi reposta e, em seguida, definir a autoridade MDM como **Microsoft Intune**. Depois de alterar a autoridade de MDM, deverá ver que serão refletidas na consola do. Para obter mais informações, consulte [como definir a autoridade de MDM](https://docs.microsoft.com/en-us/intune/deploy-use/prerequisites-for-enrollment#step-2-set-mdm-authority).
<!-- [Azure portal](https://docs.microsoft.com/en-us/intune-azure/enroll-devices/set-mdm-authority) -->


## <a name="configure-the-apns-certificate"></a>Configurar o certificado do APNs
Quando tiver dispositivos iOS, tem de configurar o certificado do APNs no Intune.

#### <a name="to-configure-the-apns-certificate"></a>Para configurar o certificado do APNs
1. Transferir o pedido de certificado do APNs.
   <!--The process is different depending on how you connect to Intune:
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment** &gt; **Apple MDM Push Certificate**, and then select **Download your CSR** to download and save the .csr file locally.   
    <br/>
    **Microsoft Intune administration console**   -->
   No [consola de administração do Microsoft Intune](http://manage.microsoft.com), aceda a **administração** &gt; **gestão de dispositivos móveis** &gt; **iOS e Mac OS X** &gt; **carregar um certificado do APNs**e, em seguida, escolha **transferir o pedido de certificado do APNs**. Guarde o ficheiro de pedido de assinatura de certificado (.csr) localmente.
   > [!IMPORTANT]    
   > Transfira um novo pedido de assinatura de certificado. Não utilize um ficheiro existente ou irá falhar.

   ![Transferir o pedido de certificado do APNs](./media/mdm-change-download-apns-certificate.png)

2. Vá para o [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844)e inicie sessão com a **mesmo** ID Apple que foi utilizado para criar e renovar o certificado do APNs que utilizou no Configuration Manager (híbrido) anteriormente.

   ![Página de início de sessão no Apple Push Certificates Portal](./media/mdm-change-apns-portal.png)

3. Selecione o certificado do APNs que utilizou no Configuration Manager (híbrido) e, em seguida, clique em **renovar**.   

    ![Renovar a caixa de diálogo do APNs](./media/mdm-change-renew-apns.png)

4. Selecione o ficheiro de pedido (. CSR) que transferiu localmente de assinatura de certificado do APNs e, em seguida, clique em **carregar**.

    ![Página de início de sessão no Apple Push Certificates Portal](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)
 
5. Selecione o APNs mesmo e, em seguida, clique em **transferir**. Transfira o certificado do APNs (. pem) e guarde o ficheiro localmente.  

   ![Página de início de sessão no Apple Push Certificates Portal](./media/mdm-change-renew-apns-download.png)

6. Carregar o certificado do APNs renovado para o inquilino do Intune com o mesmo ID Apple que antes.
<!--The process is different depending on how to connect to Intune:  
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment**  &gt; **Apple MDM Push Certificate**, enter your Apple ID in step 3, select the certificate (.pem) file in step 4, and then click **Upload**.     
    <br/>
    **Microsoft Intune administration console**    -->
    In the [Microsoft Intune administration console](http://manage.microsoft.com), go to **Administration** &gt; **Mobile Device Management** &gt; **iOS and Mac OS X** &gt; **Upload an APNs Certificate**, and then choose **Upload the APNs certificate**. Go to the certificate (.pem) file, choose **Open**, and then enter your **Apple ID**.   

   ![Carregar o certificado do APNs](./media/mdm-change-upload-apns-certificate.png)

## <a name="next-steps"></a>Passos seguintes
Depois de concluída a alteração na autoridade de MDM, reveja os seguintes passos:
- Quando o serviço Intune Deteta que a autoridade de MDM de um inquilino foi alterado, que envia uma mensagem de notificação para todos os dispositivos inscritos para registar e sincronizar com o serviço (trata-se fora a verificação agendada regularmente na). Por conseguinte, depois da autoridade de MDM para o inquilino foi alterada híbrida ao Intune autónomo, todos os dispositivos que estão a alimentação ligados e online irão ligar-se com o serviço, receber a nova autoridade de MDM e de ser gerido pelo Intune autónomo passa. Será sem interrupções da gestão e a proteção destes dispositivos.
- Dispositivos que estão ligados desativado ou offline durante a (ou pouco depois) a alteração na autoridade de MDM ligar e sincronizar com o serviço sob a autoridade de MDM novo quando estão ligados à corrente no e online.  

  dispositivos iOS necessitam de mais tempo para renovar e configurar o certificado do APNs. Por conseguinte, os dispositivos iOS não irão receber a verificação inicial no pedido. Mesmo que os dispositivos iOS são ligados no e online durante a (ou pouco depois) a alteração na autoridade de MDM, existirá um atraso de até oito horas (consoante o período de tempo da verificação regular agendada seguinte no) antes dos dispositivos iOS estão registados com o serviço sob a autoridade de MDM de novo.    

  > [!IMPORTANT]
  > Entre a hora quando altera o MDM autoridade e quando o certificado do APNs renovado é carregado para a autoridade de novo, o novo inscrições de dispositivos e o dispositivo Verifique no iOS dispositivos irão falhar. Por conseguinte, é importante que analise e carregar o certificado do APNs para a novo autoridade logo que possível após a alteração na autoridade de MDM.   

- Os utilizadores podem alterar rapidamente para a autoridade de MDM novo iniciando manualmente uma verificação do dispositivo para o serviço. Os utilizadores podem facilmente efetuar este procedimento utilizando a aplicação Portal da empresa e iniciar uma verificação de conformidade do dispositivo.
- Para validar que coisas estão a funcionar corretamente depois de dispositivos têm deu entrada em e sincronizados com o serviço após a alteração na autoridade de MDM, procure os dispositivos a [consola de administração do Microsoft Intune](http://manage.microsoft.com). Os dispositivos que foram anteriormente geridos pelo Configuration Manager (híbrido) serão agora apresentados como os dispositivos geridos.    
- Não há um período provisória quando um dispositivo estiver offline durante a alteração na autoridade de MDM e quando verifica a que o dispositivo para o serviço. Para ajudar a garantir que o dispositivo permanece protegido e funcionais durante este período intermédio, o seguinte permanecem no dispositivo até sete dias (ou até que o dispositivo estabelece ligação com a autoridade de MDM novo e recebe novas definições de que irão substituir os existentes):
    - Perfil de e-mail
    - Perfil da VPN
    - Perfil de certificado
    - Perfil Wi-Fi
    - Perfis de configuração
- Certifique-se de que as novas definições que foram concebidas para substituir as definições existentes têm o mesmo nome que as anteriores para se certificar de que as definições antigas são substituídas. Caso contrário, os dispositivos poderão acaba por ficar com as políticas e perfis redundantes.    

  > [!TIP]   
  > Como melhor prática, deve criar todas as definições de gestão e configurações, bem como implementações, imediatamente após a alteração à autoridade de MDM foi concluída. Isto irá ajudar a garantir que os dispositivos estão protegidos e geridos ativamente durante o período de intermédio.   
-  Depois de alterar a autoridade de MDM, execute os seguintes passos para validar que a novos dispositivos são inscritos com êxito para a autoridade de novo:   
    - Inscrever um dispositivo novo
    - Certifique-se de que os dispositivos inscritos recentemente aparecem na consola de administração do Intune.
    - Efetue uma ação, tal como o bloqueio remoto, na consola de administração do dispositivo. Se for bem sucedida, o dispositivo está a ser gerido pela autoridade MDM de novo.
- Se tiver problemas com dispositivos específicos, pode anular a inscrição e inscrever-se novamente os dispositivos para obtê-los à autoridade de novo e geridas como rapidamente quanto possível.

<!-- After the change in MDM authority and devices check in with the service, note the following:      - The updated compliance status of devices will only display in the Azure portal immediately.
- There will be a delay for compliance status of devices to display in the Intune administrative console.-->
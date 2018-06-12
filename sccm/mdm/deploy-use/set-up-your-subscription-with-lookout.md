---
title: Configurar a sua subscrição Lookout
titleSuffix: Configuration Manager
description: Saiba como configurar defesa de ameaça móveis Lookout.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 85c2ae1039058f39bd96c7d0752f798504b0dd4d
ms.sourcegitcommit: 9cff0702c2cc0f214173b47ec241f7e5a40f84e6
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/04/2018
ms.locfileid: "34746115"
---
# <a name="set-up-your-subscription-for-lookout-mobile-threat-defense"></a>Configurar a sua subscrição do defesa de ameaça móveis Lookout

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os seguintes passos são necessários para configurar a subscrição de defesa Lookout ameaça móveis:

| #        |Passo  |
| ------------- |-------------|
| 1 | [Recolher informações do Azure AD](#collect-azure-ad-information) |
| 2 | [Configurar a sua subscrição](#configure-your-subscription) |
| 3 | [Configurar grupos de inscrição](#configure-enrollment-groups) |
| 4 | [Configurar a sincronização de estado](#configure-state-sync) |
| 5 | [Configurar informações de destinatários de e-mail de relatório de erro](#configure-error-report-email-recipient-information) |
| 6 | [Configurar definições de inscrição](#configure-enrollment-settings) |
| 7 | [Configurar notificações por e-mail](#configure-email-notifications) |
| 8 | [Configurar a classificação de ameaça](#configure-threat-classification) |
| 9 | [Observar inscrição](#watching-enrollment) |


> [!IMPORTANT]  
> Não é possível utilizar um inquilino existente da segurança de ponto final de Mobile Lookout ainda não estiver associado ao inquilino do Azure AD para a integração com o Azure AD e o Intune. Contacte o suporte de Lookout para criar um novo inquilino de segurança de ponto final do Lookout Mobile. Utilize o novo inquilino para carregar os utilizadores do Azure AD.




## <a name="collect-azure-ad-information"></a>Recolher informações do Azure AD
O inquilino de segurança de ponto final de mobilidade Lookout será associado a sua subscrição do Azure AD para integrar o Lookout com o Intune. Para ativar a sua subscrição do serviço de defesa do Lookout ameaça móveis, o suporte de Lookout (enterprisesupport@lookout.com) tem as seguintes informações:

- **ID de inquilino do Azure AD**
- **ID de objeto de grupo do Azure AD** para *completa* o acesso à consola Lookout
- **ID de objeto de grupo do Azure AD** para *restrito* Lookout acesso à consola (opcional)

Utilize os seguintes passos para reunir as informações que necessárias para lhe dar à equipa de suporte de Lookout.

1. Iniciar sessão para o [portal do Azure](https://portal.azure.com) e selecione a sua subscrição. 

2. Quando escolher o nome da sua subscrição, o URL resultante inclui o ID da subscrição. Se tiver algum problema ao localizar o seu ID de subscrição, consulte este [artigo de suporte da Microsoft](https://support.office.com/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b) para dicas sobre ao localizar o seu ID de subscrição.

3. Localizar o ID de grupo do Azure AD.  
     > [!NOTE]   
     > O **ID de objeto de grupo** no **propriedades** página do grupo no painel do Azure AD do portal do Azure.  

   A consola Lookout suporta dois níveis de acesso:  

   - **Acesso total:** O administrador do Azure AD pode criar um grupo de utilizadores que têm acesso total e, opcionalmente, criar um grupo de utilizadores que terão acesso restrito. Apenas os utilizadores nestes grupos podem iniciar sessão para o **consola Lookout**.
   - **Acesso restrito:** Os utilizadores deste grupo não terá acesso a vários configuração e módulos relacionadas com a inscrição da consola Lookout e têm acesso só de leitura para o **política de segurança** módulo da consola Lookout.  

     > [!TIP]  
     > Para obter mais informações sobre as permissões, consulte [este artigo de suporte Lookout](https://personal.support.lookout.com/hc/articles/114094105653).


4. Assim que recolhemos estas informações, contacte o suporte de Lookout (e-mail: enterprisesupport@lookout.com). O suporte de lookout irá trabalhar com o seu contacto principal para carregar a sua subscrição e criar a sua conta de empresa Lookout, utilizando as informações que recolheu.



## <a name="configure-your-subscription"></a>Configurar a sua subscrição

1. Depois do suporte de Lookout cria a conta de empresa Lookout, é enviado um e-mail de Lookout para contacto principal da sua empresa com uma ligação para o [url de início de sessão](https://aad.lookout.com/les?action=consent).

2. O início de sessão primeiro para a consola Lookout tem de ser com uma conta de utilizador com a função do Azure AD de Administrador Global para registar o inquilino do Azure AD. Posteriormente, o início de sessão não requer este nível de privilégio do Azure AD. É apresentada uma página de consentimento. Escolha **aceitar** para concluir o registo. Depois de aceite e o consentimento, são redirecionados para a consola Lookout.

   ![captura de ecrã da página tempo primeiro início de sessão da consola Lookout](media/lookout-initial-login.png)

3. No [Lookout consola](https://aad.lookout.com), do **sistema** módulo, escolha o **conectores** separador e selecione **Intune**.

   ![captura de ecrã da consola Lookout o separador de conectores abrir e, opção Intune realçado](media/lookout-setup-intune-connector.png)

4. Aceda a **conectores** > **as definições de ligação** e especifique o **Heartbeat frequência** em minutos.

   ![captura de ecrã do separador de definições de ligação com a frequência de heartbeat configuradas a mostrar](media/lookout-connection-settings.png)



## <a name="configure-enrollment-groups"></a>Configurar grupos de inscrição
1. Como melhor prática, crie um grupo de segurança do Azure AD no [portal do Azure](https://portal.azure.com) que contenha um pequeno número de utilizadores a integração de Lookout de teste.

    > [!NOTE]  
    > Todos os Lookout suportados, inscritos no Intune dispositivos dos utilizadores num grupo de inscrição no Azure AD que são identificados e inscrito e elegível para ativação na consola de Lookout MTD são suportados.

2. No [Lookout consola](https://aad.lookout.com), do **sistema** módulo, escolha o **conectores** separador e selecione **inscrição gestão** para definir um conjunto de utilizadores cujos dispositivos devem estar inscrito no Lookout. Adicione o grupo de segurança do Azure AD **nome a apresentar** para inscrição.

    ![captura de ecrã da página de inscrição do conector do Intune](media/lookout-enrollment.png)

    >[!IMPORTANT]  
    > O **nome a apresentar** diferencia maiúsculas de minúsculas conforme mostrado no **propriedades** do grupo de segurança no portal do Azure. Conforme mostrado na imagem abaixo, o **nome a apresentar** a segurança de grupo é camel case enquanto o título é todas as letras maiúsculas e minúsculas. Na correspondência de consola Lookout o **nome a apresentar** maiúsculas para o grupo de segurança.
    >![captura de ecrã do portal do Azure, o serviço de Azure Active Directory, a página de propriedades](media/aad-group-display-name.png)

    >[!NOTE]  
    >A melhor prática é utilizar a predefinição cinco minutos para que o incremento de tempo para verificar a existência de novos dispositivos. Limitações atuais, **Lookout não é possível validar os nomes a apresentar grupo:** Certifique-se a **nome a apresentar** campo no portal do Azure corresponde exatamente ao grupo de segurança do Azure AD. **Não é suportada a criação de aninhamento de grupos:**  Segurança do Azure AD grupos utilizados no Lookout tem de conter apenas os utilizadores. Não podem conter outros grupos.

3.  Assim que é adicionado um grupo, da próxima vez que um utilizador abre o Lookout para a aplicação de trabalho nos respetivos dispositivos suportados, o dispositivo se encontra ativado numa Lookout.

4.  Quando estiver satisfeito com os resultados, expanda a inscrição para grupos de utilizadores adicionais.



## <a name="configure-state-sync"></a>Configurar a sincronização de estado
No **sincronização de estado** opção, especifique o tipo de dados que devem ser enviados para o Intune. Estado do dispositivo e o estado de ameaça são necessários para a integração do Lookout Intune funcione corretamente. Estas definições estão ativadas por predefinição.



## <a name="configure-error-report-email-recipient-information"></a>Configurar informações de destinatários de e-mail de relatório de erro
No **erro gestão** opção, introduza o endereço de correio eletrónico que deve receber os relatórios de erros.

![captura de ecrã da página Gestão de erro de conector do Intune](media/lookout-connector-error-notifications.png)



## <a name="configure-enrollment-settings"></a>Configurar definições de inscrição
No **sistema** módulo, o **conectores** página, especifique o número de dias antes de um dispositivo é considerado como desligada. Dispositivos desligados são considerados como não conforme e serão impedidos de aceder a aplicações da empresa com as políticas de acesso condicional do SCCM. Pode especificar valores entre 1 e 90 dias.

![Definições de registo lookout](media/lookout-console-enrollment-settings.png)



## <a name="configure-email-notifications"></a>Configurar notificações por e-mail
Se pretende receber alertas de e-mail para ameaças, inicie sessão no [consola Lookout](https://aad.lookout.com) com a conta de utilizador que deve receber as notificações. No **preferências** separador do **sistema** módulo, escolha os níveis de ameaças que devem receber notificações e colocá-los **ON**. Guarde as alterações.

![captura de ecrã da página de preferências com a conta de utilizador apresentada](media/lookout-email-notifications.png) se já não pretender receber notificações por e-mail, definir as notificações como OFF e guarde as alterações.



## <a name="configure-threat-classification"></a>Configurar a classificação de ameaça
Defesa de ameaça móveis lookout classifica móveis ameaças de vários tipos. O [classificações de ameaça Lookout](http://personal.support.lookout.com/hc/articles/114094130693) têm níveis de risco predefinidos associados aos mesmos. Estas definições podem ser alteradas em qualquer altura, de acordo com os requisitos da sua empresa.

![captura de ecrã da página de política que mostra ameaça e classificações](media/lookout-threat-classification.png)

>[!IMPORTANT]  
> Níveis de risco são um aspeto importante de defesa ameaça móveis. A integração do Intune calcula a conformidade do dispositivo, de acordo com estes níveis de risco no tempo de execução. O administrador do Intune define uma regra de política para identificar um dispositivo como não conforme se o dispositivo tem uma ameaça Active Directory com um mínimo ao nível do **elevada**, **média**, ou **baixa**. A política de classificação de ameaça defesa de ameaça móveis Lookout unidades diretamente o cálculo de conformidade do dispositivo no Intune.



## <a name="watching-enrollment"></a>Observar inscrição
Assim que a configuração estiver concluída, defesa de ameaça móveis Lookout for iniciado consultar o Azure AD para dispositivos que correspondem aos grupos de inscrição especificado. Pode encontrar informações sobre os dispositivos inscritos no módulo de dispositivos. O estado inicial de dispositivos é mostrado como pendente. As alterações de estado de dispositivo depois do Lookout for Work aplicação é instalada, abrir e ativado no dispositivo. Para obter mais informações sobre como obter o Lookout para a aplicação de trabalho instalada no dispositivo, consulte [configurar e implementar o Lookout para aplicações de trabalho](configure-and-deploy-lookout-for-work-apps.md).


## <a name="next-steps"></a>Passos seguintes
[Ativar ligação Lookout MTP Intune](enable-lookout-connection-in-intune.md)

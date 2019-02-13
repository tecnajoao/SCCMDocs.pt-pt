---
title: Configurar a sua subscrição do Lookout
titleSuffix: Configuration Manager
description: Saiba como configurar a defesa contra ameaças móveis do Lookout.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f914cba7eee44f340bf5b696aca1854128aeb8b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141311"
---
# <a name="set-up-your-subscription-for-lookout-mobile-threat-defense"></a>Configurar a sua subscrição para a defesa contra ameaças móveis do Lookout

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os seguintes passos são necessários para configurar a subscrição de defesa contra ameaças móveis do Lookout:

| #        |Passo  |
| ------------- |-------------|
| 1 | [Recolher informações do Azure AD](#collect-azure-ad-information) |
| 2 | [Configurar a sua subscrição](#configure-your-subscription) |
| 3 | [Configurar grupos de inscrição](#configure-enrollment-groups) |
| 4 | [Configurar a sincronização do Estado](#configure-state-sync) |
| 5 | [Configurar informações de destinatário de e-mail de relatórios de erros](#configure-error-report-email-recipient-information) |
| 6 | [Configurar definições de inscrição](#configure-enrollment-settings) |
| 7 | [Configurar notificações por e-mail](#configure-email-notifications) |
| 8 | [Configurar a classificação de ameaças](#configure-threat-classification) |
| 9 | [Monitorizar as inscrições](#watching-enrollment) |


> [!IMPORTANT]  
> Um inquilino existente do Lookout Mobile Endpoint Security ainda não estiver associada ao seu inquilino do Azure AD não pode ser utilizado para a integração com o Azure AD e o Intune. Contacte o suporte do Lookout para criar um novo inquilino do Lookout Mobile Endpoint Security. Utilize o novo inquilino para integrar os utilizadores do Azure AD.




## <a name="collect-azure-ad-information"></a>Recolher informações do Azure AD
O inquilino do Lookout Mobile Endpoint Security será associado a sua subscrição do Azure AD para integrar o Lookout com o Intune. Para ativar a sua subscrição de serviço de defesa de ameaças móveis do Lookout, o suporte do Lookout (enterprisesupport@lookout.com) precisa das seguintes informações:

- **ID de inquilino do Azure AD**
- **ID de objeto de grupo do Azure AD** para *completa* acesso à consola do Lookout
- **ID de objeto de grupo do Azure AD** para *restrito* acesso de consola do Lookout (opcional)

Utilize os seguintes passos para reunir as informações que deve fornecer à equipa de suporte do Lookout.

1. Inicie sessão para o [portal do Azure](https://portal.azure.com) e selecione a sua subscrição. 

2. Ao escolher o nome da sua subscrição, o URL resultante incluirá o ID de subscrição. Se tiver dificuldades em localizar o seu ID de subscrição, veja este [artigo de suporte da Microsoft](https://support.office.com/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b) para obter dicas sobre como encontrar o ID da subscrição.

3. Encontrar o ID de grupo do Azure AD.  
     > [!NOTE]   
     > O **ID de objeto do grupo** está ativada a **propriedades** página do grupo no painel do Azure AD do portal do Azure.  

   A consola do Lookout suporta dois níveis de acesso:  

   - **Acesso total:** Os administradores do Azure AD podem criar um grupo para utilizadores que têm acesso total e, opcionalmente, crie um grupo para os utilizadores que terão acesso restrito. Apenas os utilizadores nestes grupos podem iniciar sessão para o **consola do Lookout**.
   - **Acesso restrito:** Os utilizadores neste grupo não terá acesso a vários configuração e módulos relacionadas com a inscrição na consola do Lookout e têm acesso só de leitura para o **política de segurança** módulo na consola do Lookout.  

     > [!TIP]  
     > Para obter mais informações sobre as permissões, consulte [neste artigo de suporte do Lookout](https://personal.support.lookout.com/hc/articles/114094105653).


4. Quando tiver recolhido estas informações, contacte o suporte do Lookout (e-mail: enterprisesupport@lookout.com). Suporte do lookout irá funcionar com o seu contacto principal para integrar a sua subscrição e criar a sua conta do Lookout Enterprise com as informações que recolheu.



## <a name="configure-your-subscription"></a>Configurar a sua subscrição

1. Após o suporte do Lookout cria a sua conta do Lookout Enterprise, será enviado um e-mail do Lookout para o contacto principal para a sua empresa com uma ligação para o [url de início de sessão](https://aad.lookout.com/les?action=consent).

2. O primeiro início de sessão na consola do Lookout tem de ser com uma conta de utilizador com a função de Administrador Global para registar o seu inquilino do Azure AD do Azure AD. Mais tarde, o início de sessão não requer esse nível de privilégio no Azure AD. É apresentada uma página de consentimento. Escolher **Accept** para concluir o registo. Depois de aceitar e consentir, será redirecionado para a consola do Lookout.

   ![captura de ecrã da página de início de sessão de iniciantes da consola do Lookout](media/lookout-initial-login.png)

3. Na [consola do Lookout](https://aad.lookout.com), da **System** módulo, escolha o **conectores** separador e selecione **Intune**.

   ![captura de ecrã da consola do Lookout com o separador conectores aberto e a opção Intune destacada](media/lookout-setup-intune-connector.png)

4. Aceda a **conectores** > **definições de ligação** e especifique o **frequência do Heartbeat** em minutos.

   ![captura de ecrã do separador de definições da ligação, com frequência do heartbeat configurado](media/lookout-connection-settings.png)



## <a name="configure-enrollment-groups"></a>Configurar grupos de inscrição
1. Como melhor prática, crie um grupo de segurança do Azure AD no [portal do Azure](https://portal.azure.com) que contém um pequeno número de utilizadores para testar a integração do Lookout.

    > [!NOTE]  
    > Todos os dispositivos de suporte do Lookout, inscritos no Intune de usuários numa inscrição de grupo no Azure AD que estão identificados e suportados serão inscritos e poderão ser ativados na consola do Lookout MTD.

2. Na [consola do Lookout](https://aad.lookout.com), da **System** módulo, escolha o **conectores** separador e selecione **gestão de inscrições** para definir um conjunto de utilizadores cujos dispositivos devem ser inscritos com o Lookout. Adicionar grupo de segurança do Azure AD **nome a apresentar** para a inscrição.

    ![captura de ecrã da página de inscrição do conector do Intune](media/lookout-enrollment.png)

    >[!IMPORTANT]  
    > O **nome a apresentar** diferencia maiúsculas de minúsculas conforme mostrado na **propriedades** do grupo de segurança no portal do Azure. Conforme mostrado na imagem abaixo, o **nome a apresentar** da segurança do grupo é maiúscula, o título é todo em minúsculas. Na correspondência de consola do Lookout a **nome a apresentar** maiúsculas para o grupo de segurança.
    >![captura de ecrã do portal do Azure, serviço Azure Active Directory, página de propriedades](media/aad-group-display-name.png)

    >[!NOTE]  
    >A melhor prática é utilizar a predefinição de cinco minutos para o intervalo de tempo para verificar a existência de novos dispositivos. Limitações atuais, **Lookout não consegue validar nomes a apresentar de grupo:** Certifique-se a **nome a apresentar** campo no portal do Azure corresponde exatamente ao grupo de segurança do Azure AD. **Não é suportada a criação de grupos aninhados:**  Segurança do Azure AD grupos utilizados no Lookout têm de conter apenas utilizadores. Não podem conter outros grupos.

3.  Assim que for adicionado um grupo, da próxima vez que um utilizador abre o Lookout for Work a aplicação no seu dispositivo suportado, o dispositivo é ativado no Lookout.

4.  Quando estiver satisfeito com os resultados, alargar a inscrição a grupos de utilizadores adicionais.



## <a name="configure-state-sync"></a>Configurar a sincronização do Estado
Na **sincronização do estado** opção, especifique o tipo de dados que devem ser enviados para o Intune. Estado do dispositivo e o estado da ameaça são necessários para a integração do Lookout Intune possa funcionar corretamente. Estas definições estão ativadas por predefinição.



## <a name="configure-error-report-email-recipient-information"></a>Configurar informações de destinatário de e-mail de relatórios de erros
Na **gerenciamento de erros** opção, introduza o endereço de e-mail que deve receber os relatórios de erros.

![captura de ecrã da página de gestão erro do conector do Intune](media/lookout-connector-error-notifications.png)



## <a name="configure-enrollment-settings"></a>Configurar definições de inscrição
Na **System** módulo, na **conectores** , especifique o número de dias antes de um dispositivo é considerado como estando desligado. Dispositivos desligados são considerados como não conforme e serão impedidos de aceder a aplicações da empresa com base nas políticas de acesso condicional do SCCM. Pode especificar valores entre 1 e 90 dias.

![Definições de inscrição do lookout](media/lookout-console-enrollment-settings.png)



## <a name="configure-email-notifications"></a>Configurar notificações por e-mail
Se pretender receber alertas de e-mail de ameaças, inicie sessão para o [consola do Lookout](https://aad.lookout.com) com a conta de utilizador que deve receber as notificações. Na **preferências** separador do **sistema** módulo, escolha os níveis de ameaças que devem receber notificações e defini-los como **ON**. Guarde as alterações.

![captura de ecrã da página de preferências a apresentar da conta de utilizador](media/lookout-email-notifications.png) se já não quiser receber notificações por e-mail, defina as mesmas como OFF e guarde as alterações.



## <a name="configure-threat-classification"></a>Configurar a classificação de ameaças
Defesa contra ameaças móveis do lookout classifica ameaças contra dispositivos móveis de vários tipos. O [classificações de ameaças do Lookout](http://personal.support.lookout.com/hc/articles/114094130693) têm níveis de risco predefinidos inerentes às mesmas. Estas definições podem ser alteradas em qualquer altura para atender às suas necessidades da empresa.

![captura de ecrã da página política apresentar ameaças e classificações](media/lookout-threat-classification.png)

>[!IMPORTANT]  
> Níveis de risco são um aspecto importante de defesa contra ameaças móveis. A integração do Intune calcula a conformidade do dispositivo, de acordo com estes níveis de risco em tempo de execução. O administrador do Intune define uma regra na política para identificar um dispositivo como não conforme se o dispositivo tiver uma ameaça ativa com um mínimo ao nível dos **elevada**, **médio**, ou **baixa**. A política de classificação de ameaças na defesa contra ameaças móveis do Lookout unidades diretamente o cálculo da conformidade de dispositivo no Intune.



## <a name="watching-enrollment"></a>Monitorizar as inscrições
Depois da configuração estiver concluída, a defesa contra ameaças móveis do Lookout inicia consultar o Azure AD para dispositivos que correspondam aos grupos de inscrição especificados. Pode encontrar informações sobre os dispositivos inscritos no módulo dispositivos. O estado inicial dos dispositivos é apresentado como pendente. As alterações de estado do dispositivo quando o Lookout for Work a aplicação estiver instalada, aberta e ativada no dispositivo. Para obter mais informações sobre como obter o Lookout for Work a aplicação no dispositivo pretendida, veja [configurar e implementar o Lookout for Work](configure-and-deploy-lookout-for-work-apps.md).


## <a name="next-steps"></a>Passos seguintes
[Ativar a ligação Lookout MTP ao Intune](enable-lookout-connection-in-intune.md)

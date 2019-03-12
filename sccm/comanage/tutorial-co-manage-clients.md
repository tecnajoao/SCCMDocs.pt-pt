---
title: Tutorial&#58; ativar a cogestão de clientes existentes do Configuration Manager
titleSuffix: Configuration Manager
description: Configure cogestão com o Microsoft Intune quando gere dispositivos Windows 10 com o Configuration Manager.
ms.date: 03/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: brenduns
ms.author: brenduns
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: af526f531ed81de105aea9d6c5d7f2ea81e8f104
ms.sourcegitcommit: af8693048e6706ffda72572374f56e0bc7dfce2c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/11/2019
ms.locfileid: "57737286"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Tutorial: Ativar a cogestão para os clientes existentes do Configuration Manager
Com a cogestão, pode manter os seus processos bem estabelecidos para utilizar o Configuration Manager para gerenciar PCs em sua organização. Ao mesmo tempo, está investindo na cloud através da utilização do Intune para segurança e provisionamento modernos.  

Neste tutorial, vai configurar cogestão dos seus dispositivos Windows 10 que já tenham sido inscritos no Configuration Manager. Este tutorial começa com a premissa de que já utilizam o Configuration Manager para gerir os dispositivos Windows 10.

Utilize este tutorial quando:  

- Tem do Active Directory no local que pode ligar ao Azure Active Directory (Azure AD) numa configuração híbrida do Azure AD. 

  Se não é possível implementar uma versão híbrida do Azure Active Directory (AD) que associa o ambiente AD com o Azure AD, recomendamos que siga o nosso tutorial de complementar [ativar a cogestão para dispositivos Windows 10 novos baseado na internet](/sccm/comanage/tutorial-co-manage-new-devices). 
- Tem clientes existentes do Configuration Manager que pretende anexar de cloud.


**Neste tutorial, irá:**  
> [!div class="checklist"]  
> * Rever pré-requisitos para o Azure e o seu ambiente no local  
> * Configurar o Azure AD híbrido  
> * Configurar os agentes de cliente do Configuration Manager para registar com o Azure AD  
> * Configurar o Intune para inscrição automática de dispositivos  
> * Atribuir licenças do Intune aos utilizadores  
> * Ativar a cogestão no Configuration Manager  


## <a name="prerequisites"></a>Pré-requisitos  

### <a name="azure-services-and-environment"></a>Serviços do Azure e o ambiente
- Subscrição do Azure ([avaliação gratuita](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Subscrição do Microsoft Intune
  > [!TIP]  
  > Uma Enterprise Mobility + Security (EMS) subscrição inclui o Azure Active Directory Premium e o Microsoft Intune. Subscrição do EMS ([avaliação gratuita](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

Se ainda não existir no seu ambiente, durante este tutorial irá:
- Atribuir uma licença para a utilizadores *Intune* e para *Azure Active Directory Premium*
- Configurar [do Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) entre seu Active Directory no local e o Azure Active Directory (AD) do inquilino


### <a name="on-premises-infrastructure"></a>Infraestrutura no local
- R [uma versão suportada](https://docs.microsoft.com/sccm/core/servers/manage/updates#supported-versions) do System Center Configuration Manager current branch
- O [autoridade de MDM](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority) tem de ser definido para o Intune  


### <a name="permissions"></a>Permissões
Neste tutorial, utilize as seguintes permissões para concluir tarefas:  
- Uma conta que seja um *administrador global* no Azure  
- Uma conta que seja um *administrador de domínio* na sua infraestrutura no local  
- Uma conta que seja um *administrador total* para *todos os* âmbitos no Configuration Manager   

## <a name="set-up-hybrid-azure-ad"></a>Configurar o Azure AD híbrido
Quando configurar um Azure AD híbrido, está realmente montando integração de uma local do AD com o Azure AD com o Azure AD Connect e serviços de federado do Active Directory (ADFS). Com a configuração com êxito, trabalhadores de forma totalmente integrada iniciar sessão com suas instalações de sistemas externos credenciais AD.

> [!IMPORTANT]  
> Este tutorial apresenta detalhes de um processo básico para configurar a híbrida do Azure AD para um domínio gerido. Recomendamos que esteja familiarizado com o processo e não contam com este tutorial como guia para compreender e implementar o Azure AD híbrido.
>
> Para obter mais informações sobre o Azure AD híbrido, começar com os artigos seguintes na documentação do Azure Active Directory:
> - [Planear a implementação de associação do Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> -  [Planear a implementação de associação do Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> -  [Controlar a associação do Azure AD híbrido dos seus dispositivos](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> -  [Configurar a associação do Azure AD híbrido para domínios federados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  


### <a name="set-up-azure-ad-connect"></a>Configurar o Azure AD Connect  
Azure AD híbrido requer a configuração do Azure AD Connect, para manter contas de computador no seu no local do Active Directory (AD) e o objeto de dispositivo no Azure AD sincronizado.

A partir da versão 1.1.819.0, o Azure AD Connect fornece um Assistente para configurar a associação do Azure AD híbrido. Utilização desse assistente simplifica o processo de configuração.  

Para configurar o Azure AD Connect, terá das credenciais de um administrador global do seu inquilino do Azure AD.  

> [!TIP]  
> O procedimento seguinte não devem ser considerado autoritativo para o conjunto de cópia de segurança do Azure AD Connect, mas é fornecido aqui para ajudar a simplificar a configuração de cogestão entre o Intune e Configuration Manager. Para o conteúdo autoritativo sobre isso e procedimentos relacionados para o conjunto de cópia de segurança do Azure AD, veja [configurar a associação do Azure AD híbrido para domínios geridos](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) na documentação do Azure AD.  


#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Configurar uma associação do Azure AD híbrido com o Azure AD Connect

1. Obtenha e instale o [a versão mais recente do Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 ou superior).  
2. Inicie o Azure AD Connect e, em seguida, selecione **configurar**.
3. Sobre o **tarefas adicionais** página, selecione **configurar opções do dispositivo**e, em seguida, selecione **seguinte**.
4. Sobre o **descrição geral** página, selecione **próxima**.
5. Sobre o **ligar para o Azure AD** página, introduza as credenciais de um administrador global do seu inquilino do Azure AD.
6. Sobre o **opções do dispositivo** página, selecione **associação ao configurar híbrido do Azure AD**e, em seguida, selecione **seguinte**.
7. Sobre o **SCP** página, para cada floresta no local que pretende que o Azure AD Connect para configurar o ponto de ligação de serviço (SCP), siga os passos abaixo e, em seguida, selecione **próxima**:  
   1. Selecione uma floresta.  
   2. Selecione o serviço de autenticação.  Se tiver um domínio federado, selecione o servidor do AD FS, a menos que sua organização tiver exclusivamente os clientes do Windows 10 e tiver configurado a sincronização do computador/dispositivo ou sua organização está a utilizar [SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Clique em **adicionar** para introduzir as credenciais de administrador de empresa.  
8. Sobre o **sistemas operativos de dispositivos** página, selecione os sistemas operativos utilizados pelos dispositivos no seu ambiente do Active Directory e, em seguida, selecione **próxima**.  

   Pode selecionar a opção para suportar dispositivos de associados a um domínio de nível inferior do Windows, mas tenha em mente que a cogestão de dispositivos só é suportada para o Windows 10.

9. Se tiver um domínio gerido, ignore este passo.  

   Sobre o **configuração de Federação** página, introduza as credenciais do seu administrador do AD FS e, em seguida, selecione **próxima**.
10. Sobre o **pronto para configurar** página, selecione **configurar**.
11. Sobre o **concluir a configuração** página, selecione **saída**.

Se ocorrerem problemas com a conclusão do Azure AD híbrido associação para o domínio associado a dispositivos Windows, consulte [associação do Azure AD híbrido de resolução de problemas para os dispositivos atuais do Windows](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).


## <a name="configure-client-settings-to-direct-clients-register-with-azure-ad"></a>Configurar definições de cliente para direcionar o registo de clientes com o Azure AD  
Utilize as definições de cliente para configurar clientes do Configuration Manager para registrar automaticamente com o Azure AD.  

1. Abra o **consola do Configuration Manager** > **administração** > **descrição geral** > **as definições de cliente** e, em seguida, edite os **predefinições de cliente**.  

2. Selecione **serviços Cloud**.  

3. Sobre o **predefinições** página, defina **automaticamente registar novos dispositivos associados a um domínio do Windows 10 com o Azure Active Directory** para = **Sim**.  

4. Selecione **OK** para guardar esta configuração.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Configurar a inscrição automática de dispositivos ao Intune   
Em seguida, iremos configurar a inscrição automática de dispositivos com o Intune. Com a inscrição automática, dispositivos que gere com o Configuration Manager automaticamente inscrever-se com o Intune.

A inscrição automática também permite que os utilizadores inscrevam os respetivos dispositivos Windows 10 ao Intune. Inscrever dispositivos quando um utilizador adiciona a conta profissional para seus dispositivos pessoais, ou quando um dispositivo pertencente à empresa é associado ao Azure Active Directory.  

1. Inicie sessão para o [portal do Azure](https://portal.azure.com/) e selecione **Azure Active Directory** > **mobilidade (MDM e MAM)** > **Microsoft Intune**.  

2. Configurar **âmbito do utilizador MDM**. Especifique um dos seguintes procedimentos para configurar dispositivos de utilizadores que são geridos pelo Microsoft Intune e aceitar as predefinições para os valores de URL.  

   - **Algumas** - selecione o **grupos** que podem inscrever automaticamente os dispositivos Windows 10  

   - **Todos os** -todos os utilizadores podem inscrever automaticamente os dispositivos Windows 10, quando definidos como **None**, inscrição automática de gestão de dispositivos móveis (MDM) está desabilitada

   > [!IMPORTANT]  
   > Se os dois **âmbito de utilizador MAM** e a inscrição MDM automática (**âmbito do utilizador MDM**) estão ativados para um grupo, apenas a MAM será ativada. Apenas aplicações móveis gestão (MAM) é adicionado para os utilizadores nesse grupo quando eles dispositivo pessoal de associação à área de trabalho. Dispositivos não são automaticamente inscritos na MDM.  

3. Selecione **guardar** para toda a configuração da inscrição automática.  

4. Volte ao **mobilidade (MDM e MAM)** e, em seguida, selecione **inscrição do Microsoft Intune**.  

5. Para o âmbito do utilizador MDM, selecione **todos os**e, em seguida **guardar**.  


## <a name="assign-intune-licenses-to-users"></a>Atribuir licenças do Intune aos utilizadores   
É uma ação geralmente subestimada, mas crítica atribuir uma licença do Intune para cada utilizador que irá utilizar um dispositivo que esteja cogerido.  

Para atribuir licenças a grupos de utilizadores, utilize o Azure Active Directory.  

1. Inicie sessão para o [portal do Azure](https://portal.azure.com/) com uma conta de administrador. Para gerir licenças, a conta tem de ser um administrador de conta de utilizador ou função de administrador global.  

2. Selecione **todos os serviços** no painel de navegação à esquerda e, em seguida, selecione **Azure Active Directory**.  

3. Sobre o **do Azure Active Directory** painel, selecione **licenças** para abrir um painel onde pode ver e gerir todos os produtos sujeito a licença no inquilino.  

4. Sob **todos os produtos**, selecione a opção de produto que inclui a licença do Intune e, em seguida, selecione **atribuir** na parte superior do painel.  

   Por exemplo, poderá selecionar **Enterprise Mobility + Security E5** se isso é como obter o Intune.  

5. Sobre o **atribuir licenças** painel, clique em **utilizadores e grupos** para abrir o **utilizadores e grupos** painel. Selecione os grupos e utilizadores individuais a quem pretende atribuir uma licença.  Em seguida, clique em **selecione** na parte inferior do painel para confirmar a seleção.  

6. Sobre o **atribuir licenças** painel, clique em **opções de atribuição** para apresentar todos os planos de serviço incluídos no produto que selecionou anteriormente. Se tiver selecionado um único produto, como o Intune, apenas esse produto é mostrado.  
   - Definir **Microsoft Intune** ao **no**.  
   - Atribuir uma licença para cada utilizador **Azure Active Directory Premium**.  

   Quando são atribuídas as licenças aplicável, selecione **OK**.  

7. Para concluir a atribuição, sobre o **atribuir licenças** painel, clique em **atribuir** na parte inferior do painel.

8. É apresentada uma notificação no canto superior direito que mostra o estado e o resultado do processo. Se não foi possível concluir a atribuição ao grupo (por exemplo, por causa de licenças pré-existentes no grupo), clique na notificação para ver os detalhes da falha.

Para obter mais informações sobre a atribuição de licenças do Intune aos utilizadores, consulte [atribuir licenças](https://docs.microsoft.com/intune/licenses-assign).


## <a name="enable-co-management-in-configuration-manager"></a>Ativar a cogestão no Configuration Manager
Com híbrida do Azure AD configurado, configurações de cliente do Configuration Manager no local e atribuídas a utilizadores de licenças de produtos, está pronto para mudar a opção e ativar a cogestão dos seus dispositivos Windows 10.  

> [!TIP]  
>  No passo seis o procedimento seguinte, irá passar a atribuir uma coleção como um *grupo-piloto* para a cogestão. Este é um grupo que contém um pequeno número de clientes para testar suas configurações de cogestão. Recomendamos que crie uma coleção adequada, antes de começar o procedimento. Em seguida, pode selecionar essa coleção sem sair o procedimento para fazer isso.  

1. Na consola do Configuration Manager, aceda a **Administration** > **descrição geral** > **serviços Cloud**  >  **Cogestão**.

2. No separador início, no grupo de gerir, selecione **configurar cogestão** para abrir o Assistente de configuração de cogestão.

3. Na página de subscrição, selecione **iniciar sessão** e inicie sessão no seu inquilino do Intune e, em seguida, selecione **próxima**.

4. Na página de ativação, do *inscrição automática no Intune* lista pendente, selecione uma das seguintes opções:  

   - **Piloto**  - *(recomendado)* membros da coleção que especificar são automaticamente inscritos no Intune e, em seguida, pode ser cogeridos. Especifique a coleção piloto na *teste* página deste assistente. Esta opção permite-lhe testar a cogestão num subconjunto de clientes. Em seguida, pode implementar a cogestão para clientes adicionais usando uma abordagem faseada.  

   - **Todos os** -cogestão está ativada para todos os clientes.  

5. Na página de cargas de trabalho pode mudar cargas de trabalho da **Configuration Manager** para um dos seguintes e, em seguida, quando estiver pronto para continuar, selecione **próxima**.  

   - **Criar um piloto do Intune** -muda de uma carga de trabalho apenas para os dispositivos do grupo piloto. Vai atribuir uma coleção que o grupo piloto na página seguinte do assistente.  

   - **Intune** -muda a carga de trabalho associada para todos os dispositivos Windows 10 cogeridos.  

   Não precisa de alternar quaisquer cargas de trabalho no momento que ativa a cogestão. Pode regressar ao mais tarde, esta configuração da consola do Configuration Manager após a configuração da cogestão.  

   Antes de mudar uma carga de trabalho, certifique-se de que a carga de trabalho correspondente no Intune é configurada e implementada. Por isso, mantém a fazer as cargas de trabalho gerido.  

6. Na página de teste, especifique uma coleção a utilizar para o **coleção de projetos-piloto**e, em seguida, clique em **próxima**. A coleção que especificar é utilizada como parte da sua implementação faseada de cogestão. Pode alterar as coleções no grupo piloto em qualquer altura a partir das propriedades de cogestão.  

7. Na página Resumo, selecione **próxima**e, em seguida **fechar** para concluir o assistente.  


## <a name="next-steps"></a>Passos seguintes
- Reveja o estado dos dispositivos cogeridos com o [dashboard de cogestão](/sccm/comanage/how-to-monitor)
- Iniciar a obtenção [valor imediato](quickstarts.md#immediate-value) da cogestão
- Uso [acesso condicional](quickstart-conditional-access.md) e regras de conformidade do Intune para gerir o acesso de utilizador aos recursos da empresa

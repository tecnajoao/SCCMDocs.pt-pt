---
title: Pré-visualização técnica 1709
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis na versão 1709 do Technical Preview do System Center Configuration Manager.
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79d7488e0554a36eb274bf4ef76cff92b48a71ba
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418446"
---
# <a name="capabilities-in-technical-preview-1709-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1709 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1709. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para a utilização de um técnico de pré-visualização, como atualizar entre as versões e como fornecer comentários sobre os recursos de uma technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos neste Technical Preview:**
- **Atualização para pré-visualizar a versão 1709 falha quando tem um servidor de site em modo passivo**. Quando executar a versão de pré-visualização 1706, versão 1707 ou 1708 e ter uma [servidor do site primário em modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), tem de desinstalar o servidor do site de modo passivo antes de poder atualizar o site de pré-visualização com êxito para a versão 1709. Pode reinstalar o servidor do site de modo passivo depois do seu site executa a versão 1709.

  Para desinstalar o servidor do site de modo passivo:
  1. Na consola, aceda a **Administration** > **descrição geral** > **configuração do Site** > **servidores e sites Funções do sistema**e, em seguida, selecione o servidor de site de modo passivo.
  2. Na **funções do sistema de sites** painel, clique direito na **servidor do Site** função e, em seguida, escolha **remover função**.
  3. Faça duplo clique no servidor do site de modo passivo e, em seguida, escolha **eliminar**.
  4. Depois de desinstala o servidor do site, no servidor do site primário active reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.


**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Experiência melhorada do perfil VPN na consola do Configuration Manager
<!-- 1313282 --> Com esta versão, atualizamos as páginas de assistente e propriedades de perfil VPN para apresentar as definições adequadas da plataforma selecionada. Especificamente:

- Cada plataforma tem seu próprio fluxo de trabalho, que significa que os novos perfis VPN contêm apenas a definição suportada pela plataforma.
- O **plataformas suportadas** as páginas são agora apresentadas após a **geral** página.  Agora, escolher a plataforma antes de definir os valores de propriedade.
- Quando a plataforma está definida como **Android**, **Android for Work**, ou **Windows Phone 8.1**, o **plataformas suportadas** página não é necessária e é Não é apresentada.
- O workflow baseada no cliente do Configuration Manager foi combinada com o híbrida dispositivos móveis (MDM) com base no cliente Windows 10 fluxos de trabalho; que suportam as mesmas definições.
- Cada fluxo de trabalho de plataforma inclui apenas as definições adequadas do fluxo de trabalho.  Por exemplo, o fluxo de trabalho Android contém definições adequadas para Android; definições adequadas para iOS ou Windows 10 Mobile já não aparecem no fluxo de trabalho Android.
- Para dispositivos Windows 8.1, definições geridas pelo Configuration Manager são claramente marcadas.
- A página de VPN automática está obsoleta e foi removida.

Estas alterações aplicam-se para novos perfis VPN.  

Para minimizar o risco de compatibilidade, os perfis VPN existentes permanecem inalterados.  Ao editar um perfil existente, as definições são apresentadas quanto eram quando o perfil foi criado.  

### <a name="try-it-out"></a>Experimente!

Crie um novo perfil VPN usando o processo normal. Tenha em atenção que a primeira página nas opções do Assistente de perfil VPN foram alteradas.

1.  Aceda a **ativos e compatibilidade** > **descrição geral** > **as definições de compatibilidade** > **acesso a recursos da empresa**   >  **Perfis VPN** e, em seguida, escolha **criar perfil VPN**.
2.  Introduza um nome na **gerais** página e escolha uma das seguintes opções na **especifique o tipo de perfil VPN que pretende criar**:

    - Windows 10  
    - Windows 8,1  
    - Windows Phone 8.1  
    - iOS e macOS  
    - Android  
    - Android for Work  

3.  Se escolher **Windows 8.1**, tem também a opção de **criar novo perfil** ou **importar do ficheiro**.
4.  Conclua o Assistente para concluir a criação do perfil.

À medida que seleciona as plataformas diferentes, tenha em atenção que apenas as definições relevantes para a exibição de plataforma selecionada.

## <a name="co-management-for-windows-10-devices"></a>Cogestão para os dispositivos com Windows 10    
<!-- 1350871 --> Muitos clientes pretendem gerir dispositivos Windows 10 da mesma forma que eles gerenciam dispositivos móveis com um custo mais baixo e simplificado, a solução baseada na cloud. No entanto, a efetuar a transição da gestão tradicional para a gestão moderna pode ser um desafio. Começando com o Windows 10, versão 1607 (também conhecido como a atualização de aniversário), pode associar um dispositivo Windows 10 para o local do Active Directory (AD) e com base na cloud do Azure AD ao mesmo tempo (Azure AD híbrido). Cogestão tira partido deste melhoramento e permite-lhe gerir em simultâneo os dispositivos Windows 10 com o Configuration Manager e o Intune. É uma solução que fornece uma ponte entre o tradicional para a gestão moderna e dá-lhe um caminho para fazer a transição de forma faseada. 

### <a name="prerequisites"></a>Pré-requisitos
Tem de ter os seguintes pré-requisitos em vigor antes de poder ativar a cogestão. Existem pré-requisitos gerais e pré-requisitos diferentes para os clientes existentes do Configuration Manager e dispositivos que não são clientes.

### <a name="known-issues"></a>Problemas conhecidos
Depois de criar uma política de cogestão, não é possível editar a política. Para alterar a política, eliminar e, em seguida, recriá-lo com as definições que necessita. 

#### <a name="general-prerequisites"></a>Pré-requisitos gerais
Seguem-se pré-requisitos gerais para a ativar a cogestão:  

- Pré-visualização técnica do Configuration Manager versão 1709
- Azure AD 
- Licença do Intune ou do EMS para todos os utilizadores
- Subscrição do Intune &#40;definido como a autoridade MDM no Intune **Intune**&#41;

   > [!Note]  
   > Se tiver um ambiente de MDM híbrido (Intune integrado com o Configuration Manager), não é possível ativar a cogestão. Se estiver interessado em migrar para o Intune autónomo, consulte [iniciar a migração da MDM híbrida para o Intune autónomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>Pré-requisitos adicionais para os clientes existentes do Configuration Manager
- Windows 10, versão 1709 (Fall Creators Update) e posterior
- Azure AD híbrido associou (associados ao AD e o Azure AD)

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>Pré-requisitos adicionais para novos dispositivos Windows 10
- Windows 10, versão 1709 (Fall Creators Update) e posterior
- [Gateway de gestão da cloud](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) no Configuration Manager

### <a name="workloads-you-can-switch-to-intune"></a>Cargas de trabalho que pode mudar para o Intune
Depois de ativar a cogestão, o Configuration Manager continua a gerir todas as cargas de trabalho. Quando decidir que está pronto, pode ter o Intune começar a gerir cargas de trabalho disponíveis. Nesta versão, pode ter o Intune gerir as seguintes cargas de trabalho.   

#### <a name="compliance-policies"></a>Políticas de conformidade
Políticas de conformidade definem as regras e definições que um dispositivo tem de cumprir para ser considerado conforme pelo acesso condicional políticas. Também pode utilizar as políticas de conformidade para monitorizar e resolver problemas de conformidade com dispositivos independentemente do acesso condicional. Para obter detalhes, consulte [políticas de conformidade do dispositivo](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/device-compliance-policies).  

#### <a name="windows-update-for-business-policies"></a>Atualização do Windows para políticas de negócio
Atualização do Windows para políticas de empresas permitem-lhe configurar políticas de diferimento de atualizações de funcionalidades do Windows 10 ou atualizações de qualidade para dispositivos Windows 10 geridos diretamente pelo Windows Update para empresas. Para obter detalhes, consulte [configurar o Windows Update para políticas de diferimento de negócios](https://docs.microsoft.com/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Ações remotas disponíveis no Intune no Azure para dispositivos cogeridos
Quando um dispositivo Windows 10 está ativado para a cogestão, tem as seguintes ações remotas disponíveis ao utilizador do Intune no Azure:  
- [Reposição de fábrica](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
- [Eliminação seletiva](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Eliminar dispositivos](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Reiniciar dispositivo](https://docs.microsoft.com/intune/device-restart)
- [Começar do zero](https://docs.microsoft.com/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>Preparar o Intune para a cogestão
Antes de mudar as cargas de trabalho do Configuration Manager para o Intune, crie os perfis e políticas que precisa no Intune para garantir que os dispositivos continuam a ser protegido.
Pode criar objetos no Intune com base nos objetos que tem no Configuration Manager. Em alternativa, se a sua estratégia atual baseia-se a gestão de legado ou tradicional, pode querer voltar um pouco para repensar que as políticas e perfis que precisa para a gestão moderna. Utilize os seguintes recursos para criar as políticas e perfis.    
<!-- - [Device compliance policies](https://docs.microsoft.com/intune/compliance-policy-create-windows)  -->
- [Atualização do Windows para políticas de negócio](https://docs.microsoft.com/intune/windows-update-for-business-configure)  
- [Perfis de configuração do dispositivo](https://docs.microsoft.com/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>Descrição geral da arquitetura para a cogestão
O diagrama seguinte apresenta uma visão geral da arquitetura de cogestão e como ele se adapta infraestruturas existentes de configuração e o Intune.

![Diagrama da arquitetura de cogestão](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>Cenários para ativar a cogestão  
Pode ativar a cogestão para ambos os dispositivos Windows 10 inscritos no Microsoft Intune e os clientes existentes do Windows 10 Configuration Manager. Ambos os cenários resultam em dispositivos Windows 10 simultaneamente geridos pelo Configuration Manager e o Intune, bem como associados ao AD e o Azure AD.  

#### <a name="devices-enrolled-in-intune"></a>Dispositivos inscritos no Intune  
Quando os dispositivos Windows 10 inscritos no Intune, pode instalar o cliente do Configuration Manager em dispositivos (usando um argumento da linha de comandos específico) para preparar os clientes para a cogestão. Em seguida, ativar a cogestão da consola do Configuration Manager para mover as cargas de trabalho específicas para o Intune para dispositivos específicos do Windows 10.  

Para dispositivos Windows 10 que ainda não estão inscritos no Intune, pode utilizar a inscrição automática no Azure para inscrever os dispositivos. Para novos dispositivos Windows 10, pode utilizar o Windows AutoPilot para configurar o fora da caixa de experiência de configuração inicial (OOBE), que inclui a inscrição automática que inscreve os dispositivos no Intune.  

#### <a name="configuration-manager-clients"></a>Clientes do Configuration Manager
Quando tiver dispositivos Windows 10 que são clientes do Configuration Manager, pode inscrever estes dispositivos e ativar a cogestão da consola do Configuration Manager. Informações de inquilino de acionadores do Configuration Manager, a inscrição automática no Intune com base no Azure AD.  

### <a name="prepare-windows-10-devices-for-co-management"></a>Preparar os dispositivos com Windows 10 para a cogestão
Pode ativar a cogestão em dispositivos Windows 10 que estão associados ao AD e o Azure AD e inscritos no Intune e um cliente no Configuration Manager. Para novos dispositivos Windows 10 e para dispositivos já inscritos no Intune, instale o cliente de Configuration Manager antes de poderem ser cogeridos. Para dispositivos Windows 10 que já são clientes do Configuration Manager, pode inscrever os dispositivos com o Intune e ativar a cogestão na consola do Configuration Manager.

#### <a name="command-line-to-install-configuration-manager-client"></a>Linha de comando para instalar o cliente do Configuration Manager
Crie uma aplicação no Intune para dispositivos Windows 10 que já não são clientes do Configuration Manager. Ao criar a aplicação nas próximas seções, utilize a seguinte linha de comando:

ccmsetup CCMSETUPCMD = "/ mp:&#60;*URL de ponto final a autenticação mútua de gateway de gestão de nuvem*&#62;/ CCMHOSTNAME =&#60;*URL de ponto final a autenticação mútua de gateway de gestão de nuvem* &#62;SMSSiteCode =&#60;*Sitecode* &#62; SMSMP = https:&#47;/&#60;*FQDN do pacote de gestão* &#62; AADTENANTID =&#60;*ID de inquilino do AAD*  &#62; AADTENANTNAME =&#60;*nome do inquilino* &#62; AADCLIENTAPPID =&#60;*AppID do servidor para a integração do AAD* &#62; AADRESOURCEURI = https:&#47;/&#60;*ID do recurso*&#62;"

Por exemplo, se tivesse os seguintes valores:

- **URL de ponto final a autenticação mútua de gateway de gestão de cloud**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Utilize o **MutualAuthPath** valor no **vProxy_Roles** vista SQL para o **URL de ponto final a autenticação mútua de gateway de gestão de cloud** valor.

- **FQDN do ponto de gestão (MP)**: sccmmp.corp.contoso.com    
- **Sitecode**: PS1    
- **ID de inquilino do Azure AD**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Nome de inquilino do Azure AD**: contoso    
- **ID de aplicação de cliente do Azure AD**: bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **URI de ID de recurso do AAD**: ConfigMgrServer    

  > [!Note]    
  > Utilize o **IdentifierUri** valor encontrado no **vSMS_AAD_Application_Ex** vista SQL para o **URI de ID de recurso do AAD** valor.

Usaria a seguinte linha de comando:

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer”

> [!Tip]
>Pode encontrar os parâmetros da linha de comandos para o seu site, utilizando os seguintes passos:     
> 1. Na consola do Configuration Manager, aceda a **Administration** > **descrição geral** > **serviços Cloud**  >  **Cogestão**.  
> 2. No separador início, no grupo gerenciar, escolha **configurar cogestão** para abrir o Assistente de ativação da cogestão.    
> 3. Na página de subscrição, clique em **iniciar sessão** e inicie sessão no seu inquilino do Intune e, em seguida, clique em **próxima**.    
> 4. Na página de ativação, clique em **cópia** no **dispositivos inscritos no Intune** secção para copiar a linha de comandos para a área de transferência e, em seguida, guarde a linha de comandos para utilizar o procedimento para criar a aplicação.  
> 5. Clique em **Cancelar** para sair do assistente.

#### <a name="new-windows-10-devices"></a>Novos dispositivos Windows 10
Para novos dispositivos Windows 10, pode utilizar o serviço de Autopilot para configurar o fora de experiência, que inclui a associar o dispositivo ao AD e o Azure AD, bem como a inscrição do dispositivo no Intune. Em seguida, crie uma aplicação no Intune para implementar o cliente do Configuration Manager.  
1. Ative o AutoPilot para novos dispositivos Windows 10. Para obter detalhes, consulte [descrição geral do Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).  
2. Configure a inscrição automática no Azure AD para os seus dispositivos para ser inscrito automaticamente no Intune. Para obter detalhes, consulte [dispositivos do Windows de inscrever para o Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).
3. Criar uma aplicação no Intune com o pacote de cliente do Configuration Manager e implementar a aplicação para dispositivos Windows 10 que deseja gerenciar em conjunto. Utilize o [linha de comando para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) quando passa pelos passos para [instalar clientes a partir da Internet com o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Dispositivos Windows 10 não inscritos no Intune ou um cliente do Configuration Manager
Para dispositivos Windows 10 que não estão inscritos no Intune ou que têm o cliente do Configuration Manager, pode utilizar a inscrição automática para inscrever o dispositivo no Intune. Em seguida, crie uma aplicação no Intune para implementar o cliente do Configuration Manager.
1. Configure a inscrição automática no Azure AD para os seus dispositivos para ser inscrito automaticamente no Intune. Para obter detalhes, consulte [dispositivos do Windows de inscrever para o Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  
2. Criar uma aplicação no Intune com o pacote de cliente do Configuration Manager e implementar a aplicação para dispositivos Windows 10 que deseja gerenciar em conjunto. Utilize o [linha de comando para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) quando passa pelos passos para [instalar clientes a partir da Internet com o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).

#### <a name="windows-10-devices-enrolled-in-intune"></a>Dispositivos Windows 10 inscritos no Intune
Para dispositivos Windows 10 que já tenham sido inscritos no Intune, crie uma aplicação no Intune para implementar o cliente do Configuration Manager. Utilize o [linha de comando para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) quando passa pelos passos para [instalar clientes a partir da Internet com o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

### <a name="switch-configuration-manager-workloads-to-intune"></a>Mudar as cargas de trabalho do Configuration Manager para o Intune
Na secção anterior, que preparou de dispositivos Windows 10 para a cogestão. Estes dispositivos agora estão associados ao AD e o Azure AD, pelo que estão inscritos no Intune e têm o cliente do Configuration Manager. É provável que ainda terá os dispositivos Windows 10 que estão associados ao AD e o cliente do Configuration Manager, mas não associados ao Azure AD ou inscritos no Intune. O procedimento seguinte disponibiliza os passos para ativar a cogestão, preparar o resto dos seus dispositivos Windows 10 (clientes do Configuration Manager sem a inscrição do Intune) para a cogestão e permite-lhe começar a mudar específico do Configuration Manager cargas de trabalho para o Intune.

1. Na consola do Configuration Manager, aceda a **Administration** > **descrição geral** > **serviços Cloud**  >  **Cogestão**.    
2. No separador início, no grupo gerenciar, escolha **configurar cogestão** para abrir o Assistente de ativação da cogestão.    
3. Na página de subscrição, clique em **iniciar sessão** e inicie sessão no seu inquilino do Intune e, em seguida, clique em **próxima**.   
4. Na página de teste, configure as seguintes definições e, em seguida, clique em **seguinte**:
    - **Grupo piloto**: O grupo piloto contém uma ou mais coleções que selecionar. Utilize este grupo como parte da sua implementação faseada de cogestão. Pode começar com uma coleção de teste pequeno e, em seguida, adicione mais coleções no grupo piloto, como implementar a cogestão para obter mais utilizadores e dispositivos. Pode alterar as coleções no grupo piloto em qualquer altura a partir das propriedades de cogestão.
    - **Produção**: Quando seleciona esta definição, todos os dispositivos Windows 10 suportados estão ativados para a cogestão. Configurar o **grupo de exclusão** com uma ou mais coleções. Dispositivos que são membros de qualquer uma das coleções deste grupo são excluídos da cogestão a utilizar. 
5. Na página de ativação, escolha **piloto** ou **todos os** (consoante as definições configuradas na página de teste) para ativar a inscrição automática no Intune e, em seguida, clique em **próxima**. Quando escolhe **piloto**, apenas os clientes de Gestor de configuração são membros do grupo piloto automaticamente estão inscritos no Intune. Isto permite-lhe ativar a cogestão num subconjunto de clientes para testar inicialmente cogestão e cogestão de implementação de forma faseada. 
6. Na página de cargas de trabalho, escolha se pretende mudar cargas de trabalho do Configuration Manager para ser gerido pelo Intune e, em seguida, clique em **seguinte**. Utilize os controlos de deslize para selecionar se pretende mudar a carga de trabalho para o grupo do piloto ou para todos os clientes do Windows 10 (consoante as definições configuradas na página de teste). 
7. Para ativar a cogestão, conclua o assistente.  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>Consulte também
Para obter informações sobre a instalação ou a atualizar o ramo de pré-visualização técnica, veja [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview). 

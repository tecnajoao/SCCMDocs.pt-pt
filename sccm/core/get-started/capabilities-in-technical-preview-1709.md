---
title: "Pré-visualização técnica 1709"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades disponíveis na versão de pré-visualização técnica 1709 para o System Center Configuration Manager."
ms.custom: na
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: erikje
ms.author: erikje
manager: angrobe
ms.openlocfilehash: f0acc5ae0d8207dce92c56a4c80e8321faf51393
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="capabilities-in-technical-preview-1709-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1709 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1709. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos neste Technical Preview:**
-   **Falha de atualização para pré-visualizar versão 1709 quando tiver um servidor de site no modo passivo**. Quando executar a versão de pré-visualização 1706, 1707 ou 1708 e ter um [servidor do site primário em modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), tem de desinstalar o servidor do site de modo passivo antes de poder atualizar o site de pré-visualização com êxito para a versão 1709. Pode reinstalar o servidor do site de modo passivo depois do site executa a versão 1709.

  Para desinstalar o servidor do site de modo passivo:
  1. Na consola, aceda a **administração** > **descrição geral** > **configuração do Site** > **servidores e funções de sistema de sites**e, em seguida, selecione o servidor de site de modo passivo.
  2. No **funções do sistema de sites** painel, clique direito no **servidor do Site** função e, em seguida, escolha **remover função**.
  3. Faça duplo clique no servidor do site de modo passivo e, em seguida, escolha **eliminar**.
  4. Depois de desinstala o servidor do site, no servidor do site primário Active Directory reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Experiência melhorada de perfil da VPN na consola do Configuration Manager
<!-- 1313282 -->
Com esta versão, atualizámos as páginas de assistente e propriedades de perfil VPN para apresentar as definições adequadas da plataforma selecionada. Especificamente:

- Cada plataforma tem o suas próprias fluxo de trabalho, que significa que os novos perfis VPN contém apenas a definição suportada pela plataforma do.
- O **plataformas suportadas** páginas que são apresentadas depois do **geral** página.  Agora, escolher a plataforma antes de definir os valores de propriedade.
- Quando a plataforma está definida como **Android**, **Android para trabalho**, ou **Windows Phone 8.1**, a **plataformas suportadas** página não é necessária e é Não é apresentada.
- O Configuration Manager baseada em cliente fluxo de trabalho foi combinado com híbrida dispositivos móveis (MDM) baseada no cliente Windows 10 fluxos de trabalho; suportam as mesmas definições.
- Cada fluxo de trabalho de plataforma inclui apenas as definições adequadas para esse fluxo de trabalho.  Por exemplo, o fluxo de trabalho Android contém as definições adequadas para Android; as definições adequadas para iOS ou Windows 10 Mobile não aparecem no fluxo de trabalho Android.
- Para dispositivos Windows 8.1, as definições geridas pelo Configuration Manager são claramente assinaladas.
- A página de VPN automática está obsoleta e foi removida.

Aplicam estas alterações para novos perfis VPN.  

Para minimizar o risco de compatibilidade, perfis VPN existentes são iguais.  Ao editar um perfil existente, as definições são apresentadas como quando o perfil foi criado.  

### <a name="try-it-out"></a>Experimente!

Crie um novo perfil VPN utilizando o processo normal. Tenha em atenção que a primeira página nas opções do Assistente de perfil VPN foram alteradas.

1.  Aceda a **ativos e compatibilidade** > **descrição geral** > **as definições de compatibilidade** > **acesso a recursos da empresa**   >  **Perfis VPN** e, em seguida, escolha **criar perfil VPN**.
2.  Introduza um nome no **geral** e escolha uma das seguintes opções na página **especifique o tipo de perfil da VPN que pretende criar**:

    - Windows 10  
    - Windows 8,1  
    - Windows Phone 8.1  
    - iOS e macOS  
    - Android  
    - Android for Work  

3.  Se optar por **Windows 8.1**, também tem a opção de **criar novo perfil** ou **importar de ficheiro**.
4.  Conclua o Assistente para concluir a criação do perfil.

À medida que seleciona diferentes plataformas, tenha em atenção que apenas as definições relevantes para a apresentação da plataforma selecionada.

## <a name="co-management-for-windows-10-devices"></a>Gestão conjunta para dispositivos Windows 10    
<!-- 1350871 -->
Muitos clientes pretendem gerir dispositivos Windows 10 da mesma forma que o se gerem dispositivos móveis utilizando um custo simplificado, inferior, uma solução baseada na nuvem. No entanto, efetuar a transição do gestão tradicional para gestão moderna pode ser um desafio. Iniciando com o Windows 10, versão 1607 (também conhecido como aniversário da atualização), pode associar um dispositivo Windows 10 no local do Active Directory (AD) e baseado na nuvem do Azure AD em simultâneo (híbrido do Azure AD). Gestão conjunta tira partido deste melhoramento e permite-lhe gerir em simultâneo os dispositivos Windows 10 através do Configuration Manager e o Intune. É uma solução que fornece uma ponte de tradicional para gestão moderna e dá-lhe um caminho para fazer a transição utilizando uma abordagem faseada. 

### <a name="prerequisites"></a>Pré-requisitos
Tem de ter os seguintes pré-requisitos no local antes de poder ativar gestão conjunta. Existem pré-requisitos gerais e pré-requisitos diferentes para dispositivos que não são clientes e os clientes existentes do Configuration Manager.

### <a name="known-issues"></a>Problemas conhecidos
Depois de criar uma política de gestão conjunta, não é possível editar a política. Para alterar a política, eliminá-lo e, em seguida, recriá-lo com as definições que necessita. 

#### <a name="general-prerequisites"></a>Pré-requisitos gerais
Seguem-se pré-requisitos gerais para a ativar a gestão conjunta:  

- Pré-visualização técnica 1709 de versão do Configuration Manager
- Azure AD 
- Licença do Intune ou do EMS para todos os utilizadores
- Subscrição do Intune &#40; Definido como a autoridade MDM no Intune **Intune**&#41;

   > [!Note]  
   > Se tiver um ambiente de MDM híbrido (Intune integrado com o Configuration Manager), não é possível ativar a gestão de conjunta. Se estiver interessado em migrar para o Intune autónomo, consulte o artigo [começar a migrar do MDM híbrido para o Intune autónomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>Pré-requisitos adicionais para os clientes existentes do Configuration Manager
- Versão 1709 (Outono criadores atualização) do Windows 10 e posterior
- Azure AD híbrido associado (associados aos AD e o Azure AD)

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>Pré-requisitos adicionais para novos dispositivos Windows 10
- Versão 1709 (Outono criadores atualização) do Windows 10 e posterior
- [Gateway de gestão de nuvem](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) no Configuration Manager

### <a name="workloads-you-can-switch-to-intune"></a>Cargas de trabalho que pode mudar para o Intune
Depois de ativar a gestão conjunta, o Configuration Manager continua a gerir todas as cargas de trabalho. Quando decidir o que está pronto, pode fazer com que o Intune começar a gerir as cargas de trabalho disponíveis. Nesta versão, pode ter o Intune gerir as seguintes cargas de trabalho.   

#### <a name="compliance-policies"></a>Políticas de conformidade
Políticas de conformidade definem as regras e definições que um dispositivo tem de cumprir para serem considerados conformes pelo acesso condicional políticas. Também pode utilizar as políticas de conformidade para monitorizar e resolver problemas de conformidade com dispositivos independentemente do acesso condicional. Para obter mais informações, consulte [políticas de conformidade do dispositivo](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/device-compliance-policies).  

#### <a name="windows-update-for-business-policies"></a>Windows Update para as políticas de negócio
Windows Update para políticas de empresas permitem-lhe configurar políticas de diferimento por para atualizações de funcionalidade do Windows 10 ou atualizações de qualidade de dispositivos Windows 10 geridos diretamente pelo Windows Update for Business. Para obter mais informações, consulte [configurar o Windows Update para políticas de diferimento por empresas](https://docs.microsoft.com/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Ações remoto disponíveis no Intune no Azure para dispositivos geridos conjuntamente
Quando um dispositivo Windows 10 está ativado para a gestão conjunta, tem as seguintes ações remotas disponíveis para o utilizador do Intune no Azure:  
- [Reposição de fábrica](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
- [Eliminação seletiva](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Eliminar dispositivos](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Reiniciar o dispositivo](https://docs.microsoft.com/intune/device-restart)
- [Início de raiz](https://docs.microsoft.com/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>Preparar o Intune para a gestão conjunta
Antes de mudar de cargas de trabalho do Configuration Manager para o Intune, que cria a perfis e terá das políticas no Intune para garantir que os seus dispositivos continuam a ser protegido.
Pode criar objetos no Intune com base em objetos que tenham no Configuration Manager. Em alternativa, se a sua estratégia de atual é com base na gestão de legado ou tradicional, poderá querer efetuar um passo de volta para rethink que políticas e perfis que precisa para a gestão moderna. Utilize os seguintes recursos para criar as políticas e perfis.    
<!-- - [Device compliance policies](https://docs.microsoft.com/intune/compliance-policy-create-windows)  -->
- [Windows Update para as políticas de negócio](https://docs.microsoft.com/intune/windows-update-for-business-configure)  
- [Perfis de configuração do dispositivo](https://docs.microsoft.com/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>Descrição geral da arquitetura de gestão conjunta
O diagrama seguinte fornece uma descrição geral da arquitetura de gestão conjunta e como se enquadra no existentes infraestruturas de configuração e o Intune.

![Diagrama da arquitetura de gestão conjunta](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>Cenários para ativar a gestão conjunta  
Pode ativar a gestão conjunta para ambos os dispositivos Windows 10 inscritos no Microsoft Intune e os clientes existentes do Gestor de configuração do Windows 10. Ambos os cenários resultam em dispositivos Windows 10 em simultâneo geridos pelo Configuration Manager e o Intune, bem como associado ao AD e o Azure AD.  

#### <a name="devices-enrolled-in-intune"></a>Dispositivos inscritos no Intune  
Quando os dispositivos Windows 10 inscritos no Intune, pode instalar o cliente do Configuration Manager nos dispositivos (utilizando um argumento da linha de comandos específico) para preparar os clientes para gestão conjunta. Em seguida, ativar a gestão conjunta da consola do Configuration Manager para iniciar a mover as cargas de trabalho específicas para o Intune para dispositivos Windows 10 específicos.  

Para dispositivos Windows 10 que ainda não estão inscritos no Intune, pode utilizar a inscrição automática no Azure para inscrever os dispositivos. Para dispositivos Windows 10 novo, pode utilizar o Windows AutoPilot para configurar o fora de caixa de experiência de primeira execução (OOBE), que inclui a inscrição automática que inscreve os dispositivos no Intune.  

#### <a name="configuration-manager-clients"></a>Clientes do Configuration Manager
Quando tiver dispositivos Windows 10 que sejam clientes do Configuration Manager, pode inscrever estes dispositivos e ativar a gestão conjunta da consola do Configuration Manager. Informações de inquilino de acionadores de Gestor de configuração automática inscrição no Intune com base no Azure AD.  

### <a name="prepare-windows-10-devices-for-co-management"></a>Preparar os dispositivos Windows 10 para gestão conjunta
Pode ativar a gestão conjunta em dispositivos Windows 10 que estejam associados ao AD e o Azure AD e inscritos no Intune e um cliente no Configuration Manager. Para novos dispositivos Windows 10 e para os dispositivos já inscritos no Intune, antes de instalar o cliente do Configuration Manager podem ser conjuntamente geridos. Para dispositivos Windows 10 que já estão a clientes do Configuration Manager, pode inscrever dispositivos com o Intune e ativar a gestão conjunta na consola do Configuration Manager.

#### <a name="command-line-to-install-configuration-manager-client"></a>Linha de comandos para instalar o cliente do Configuration Manager
Crie uma aplicação nos dispositivos do Intune para Windows 10 que já não são clientes do Configuration Manager. Quando cria a aplicação nas secções seguintes, utilize a seguinte linha de comandos:

ccmsetup.msi CCMSETUPCMD = "/ mp: &#60; *URL de ponto final a autenticação mútua de gateway de gestão de nuvem*&#62; / CCMHOSTNAME = &#60; *URL de ponto final a autenticação mútua de gateway de gestão de nuvem*&#62; SMSSiteCode = &#60; *Sitecode*&#62; SMSMP = https: &#47; / &#60; *FQDN do MP*&#62; AADTENANTID = &#60; *ID de inquilino do AAD*&#62; AADTENANTNAME = &#60; *Nome do inquilino*&#62; AADCLIENTAPPID = &#60; *AppID do servidor para a integração do AAD*&#62; AADRESOURCEURI = https: &#47; / &#60; *ID de recurso*&#62; "

Por exemplo, se tiver os seguintes valores:

- **URL de ponto final a autenticação mútua de gateway de gestão de nuvem**: https:/ &#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Utilize o **MutualAuthPath** valor o **vProxy_Roles** vista SQL para o **URL de ponto final a autenticação mútua de gateway de gestão de nuvem** valor.

- **FQDN do ponto de gestão (MP)**: sccmmp.corp.contoso.com    
- **Sitecode**: PS1    
- **ID de inquilino do Azure AD**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Nome de inquilino do Azure AD**: contoso    
- **ID de aplicação de cliente do Azure AD**: bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **URI de ID de recurso do AAD**: ConfigMgrServer    

  > [!Note]    
  > Utilize o **IdentifierUri** valor encontrado no **vSMS_AAD_Application_Ex** vista SQL para o **URI de ID de recurso do AAD** valor.

Pretende utilizar a seguinte linha de comandos:

ccmsetup.msi CCMSETUPCMD = "/ mp:https: / &#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode = PS1 SMSMP = https: / &#47; sccmmp.corp.contoso.com AADTENANTID = 72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME = contoso AADCLIENTAPPID = bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI = https: / &#47; ConfigMgrServer"

> [!Tip]
>Pode encontrar os parâmetros da linha de comandos para o seu site, utilizando os seguintes passos:     
> 1. Na consola do Configuration Manager, vá para **administração** > **descrição geral** > **serviços em nuvem**  >  **Gestão conjunta**.  
> 2. No separador início, no grupo de gerir, escolha **configurar a gestão conjunta** para abrir o Assistente de integração de gestão conjunta.    
> 3. Na página de subscrição, clique em **sessão** e inicie sessão no seu inquilino do Intune e, em seguida, clique em **seguinte**.    
> 4. Na página de ativação, clique em **cópia** no **dispositivos inscritos no Intune** secção para copiar a linha de comandos para a área de transferência e, em seguida, guarde a linha de comandos para utilizar o procedimento para criar a aplicação.  
> 5. Clique em **Cancelar** para sair do assistente.

#### <a name="new-windows-10-devices"></a>Novos dispositivos Windows 10
Para dispositivos Windows 10 novo, pode utilizar o serviço de Autopilot configurar Escalamento de experiência de caixa, que inclui a associar o dispositivo para o AD e o Azure AD, bem como a inscrição do dispositivo no Intune. Em seguida, crie uma aplicação no Intune para implementar o cliente do Configuration Manager.  
1. Ative AutoPilot para novos dispositivos Windows 10. Para obter mais informações, consulte [descrição geral do Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).  
2. Configure a inscrição automática no Azure AD para os seus dispositivos para ser inscrito automaticamente no Intune. Para obter mais informações, consulte [dispositivos Windows inscrever para o Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).
3. Criar uma aplicação no Intune com o pacote de cliente do Configuration Manager e implementar a aplicação para dispositivos Windows 10 que pretende gerir conjuntamente. Utilize o [linha de comandos para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) quando percorrer os passos para [instalar clientes da Internet com o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Dispositivos Windows 10 que não estão inscritos no Intune ou um cliente do Configuration Manager
Para dispositivos Windows 10 que não estão inscritos no Intune ou que têm o cliente do Configuration Manager, pode utilizar a inscrição automática para inscrever o dispositivo no Intune. Em seguida, crie uma aplicação no Intune para implementar o cliente do Configuration Manager.
1. Configure a inscrição automática no Azure AD para os seus dispositivos para ser inscrito automaticamente no Intune. Para obter mais informações, consulte [dispositivos Windows inscrever para o Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  
2. Criar uma aplicação no Intune com o pacote de cliente do Configuration Manager e implementar a aplicação para dispositivos Windows 10 que pretende gerir conjuntamente. Utilize o [linha de comandos para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) quando percorrer os passos para [instalar clientes da Internet com o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).

#### <a name="windows-10-devices-enrolled-in-intune"></a>Dispositivos Windows 10 inscritos no Intune
Para dispositivos Windows 10 que já estejam inscritos no Intune, crie uma aplicação no Intune para implementar o cliente do Configuration Manager. Utilize o [linha de comandos para instalar o cliente do Configuration Manager](#command-line-to-install-configuration-manager-client) quando percorrer os passos para [instalar clientes da Internet com o Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

### <a name="switch-configuration-manager-workloads-to-intune"></a>Cargas de trabalho do Gestor de configuração do comutador para o Intune
Na secção anterior, que preparou de dispositivos Windows 10 para gestão conjunta. Estes dispositivos agora estão associados ao AD e o Azure AD e estão inscritos no Intune e têm o cliente do Configuration Manager. Provavelmente, ainda tem de dispositivos Windows 10 que estão associados ao AD e o cliente do Configuration Manager, mas não associados ao Azure AD ou inscritos no Intune. O procedimento seguinte fornece os passos para ativar a gestão conjunta, preparar o resto dos seus dispositivos Windows 10 (clientes do Configuration Manager sem inscrição no Intune) para a gestão conjunta e permite-lhe iniciar mudar específico do Configuration Manager cargas de trabalho para o Intune.

1. Na consola do Configuration Manager, vá para **administração** > **descrição geral** > **serviços em nuvem**  >  **Gestão conjunta**.    
2. No separador início, no grupo de gerir, escolha **configurar a gestão conjunta** para abrir o Assistente de integração de gestão conjunta.    
3. Na página de subscrição, clique em **sessão** e inicie sessão no seu inquilino do Intune e, em seguida, clique em **seguinte**.   
4. Na página de teste, configure as seguintes definições e, em seguida, clique em **seguinte**:
    - **Grupo piloto**: O grupo piloto contém uma ou mais coleções que selecionar. Utilize este grupo como parte da sua implementação faseada de gestão conjunta. Pode começar com uma coleção de pequeno teste e, em seguida, adicione mais coleções ao grupo piloto como implementar gestão conjunta a mais utilizadores e dispositivos. Pode alterar as coleções no grupo de piloto em qualquer momento a partir das propriedades de gestão conjunta.
    - **Produção**: Quando seleciona esta definição, todos os dispositivos suportados do Windows 10 estão ativados para a gestão conjunta. Configurar o **grupo de exclusão** com uma ou mais coleções. Dispositivos que são membros de qualquer uma das coleções deste grupo são excluídos da gestão conjunta a utilizar. 
5. Na página de ativação, escolha o **piloto** ou **todos os** (consoante as definições que configurou na página de teste) para ativar a inscrição automática no Intune e, em seguida, clique em **seguinte**. Quando escolhe **piloto**, apenas os clientes de Gestor de configuração são membros do grupo piloto automaticamente estão inscritos no Intune. Isto permite-lhe ativar a gestão conjunta num subconjunto de clientes para testar inicialmente conjunta gestão e implementação da gestão conjunta utilizando uma abordagem faseada. 
6. Na página de cargas de trabalho, escolha se pretende mudar cargas de trabalho do Configuration Manager para serem geridos pelo Intune e, em seguida, clique em **seguinte**. Utilize os controlos de deslize para selecionar se pretende mudar a carga de trabalho para o grupo de piloto ou para todos os clientes Windows 10 (consoante as definições que configurou na página de teste). 
7. Para ativar a gestão conjunta, conclua o assistente.  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>Consulte também
Para obter informações sobre instalar ou atualizar o ramo de pré-visualização técnica, consulte [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview). 

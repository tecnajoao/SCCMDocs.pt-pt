---
title: Cargas de trabalho do Gestor de configuração do comutador para o Intune
titleSuffix: Configuraton Manager
description: Saiba como mudar cargas de trabalho atualmente gerenciadas pelo Configuration Manager para o Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: c1f5f96c4178068ced727cfe96b1c6fe8b60a0fc
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384004"
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>Cargas de trabalho do Gestor de configuração do comutador para o Intune
Na [dispositivos de preparar o Windows 10 para a cogestão](co-management-prepare.md), que preparou de dispositivos Windows 10 para a cogestão. Estes dispositivos estão associados ao AD, o Azure AD, inscritos no Intune e que o cliente do Configuration Manager. É provável que ainda terá os dispositivos Windows 10 que estão associados ao AD e o cliente do Configuration Manager, mas não associados ao Azure AD ou inscritos no Intune. O procedimento seguinte disponibiliza os passos para ativar a cogestão, preparar o resto dos seus dispositivos Windows 10 (clientes do Configuration Manager sem a inscrição do Intune) para a cogestão e permite-lhe começar a mudar específico do Configuration Manager cargas de trabalho para o Intune.


## <a name="switch-configuration-manager-workloads-to-intune"></a>Cargas de trabalho do Gestor de configuração do comutador para o Intune

1. Na consola do Configuration Manager, aceda a **Administration** > **descrição geral** > **serviços Cloud**  >  **Cogestão**.    
2. No separador início, no grupo gerenciar, escolha **configurar cogestão** para abrir o Assistente de configuração de cogestão.    
3. Na página de subscrição, clique em **iniciar sessão** e inicie sessão no seu inquilino do Intune e, em seguida, clique em **próxima**.   
4. Na página de ativação, escolha **piloto** ou **todos os** para ativar a inscrição automática no Intune e, em seguida, clique em **seguinte**. Quando escolhe **piloto**, apenas os clientes de Gestor de configuração são membros do grupo piloto automaticamente estão inscritos no Intune. Esta opção permite-lhe ativar a cogestão num subconjunto de clientes para testar inicialmente cogestão e cogestão de implementação de forma faseada. A linha de comando pode ser utilizada para implementar o cliente do Configuration Manager como uma aplicação no Intune para dispositivos já inscritos no Intune. Para obter detalhes, consulte [dispositivos Windows 10 inscritos no Intune](co-management-prepare.md#windows-10-devices-enrolled-in-intune).
5. Na página de cargas de trabalho, escolha se pretende mudar cargas de trabalho do Configuration Manager para ser gerido pelo Intune piloto ou o Intune e, em seguida, clique em **seguinte**. O **Intune piloto** definição muda a carga de trabalho apenas para os dispositivos associada do grupo piloto. O **Intune** definição muda a carga de trabalho associada para todos os dispositivos Windows 10 cogeridos. 
        
   > [!Important]    
   > Antes de alternar quaisquer cargas de trabalho, certifique-se de que a carga de trabalho correspondente no Intune, tem sido corretamente configurada e implementada. Isso faz com que as cargas de trabalho são sempre gerenciadas por uma das ferramentas de gerenciamento para os seus dispositivos.   
1. Na página de teste, configure as seguintes definições e, em seguida, clique em **seguinte**:
    - **Piloto**: O grupo piloto contém uma ou mais coleções que selecionar. Utilize este grupo como parte da sua implementação faseada de cogestão. Pode começar com uma coleção de teste pequeno e, em seguida, adicione mais coleções no grupo piloto, como implementar a cogestão para obter mais utilizadores e dispositivos. Pode alterar as coleções no grupo piloto em qualquer altura a partir das propriedades de cogestão.
    - **Produção**: Configurar o **grupo de exclusão** com uma ou mais coleções. Dispositivos que são membros de qualquer uma das coleções deste grupo são excluídos da cogestão a utilizar. 
2. Para ativar a cogestão, conclua o assistente.  

<!--1357377--> Os dispositivos cogeridos automaticamente a partir do Configuration Manager versão 1806, quando alterna uma carga de trabalho de cogestão, sincronizar política MDM do Microsoft Intune. Esta sincronização ocorre também quando inicia o **transferir política do computador** ação de notificações do cliente na consola do Configuration Manager. Para obter mais informações, consulte [iniciar a obtenção de política de cliente com a notificação do cliente](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).

## <a name="modify-your-co-management-settings"></a>Modificar as definições de cogestão
Depois de ativar a cogestão utilizando o assistente, pode modificar as definições nas propriedades de cogestão.  
- Na consola do Configuration Manager, aceda a **Administration** > **descrição geral** > **serviços Cloud**  >  **Cogestão**.  
Selecione o objeto de cogestão e, em seguida, no separador início, clique em **propriedades**. 

## <a name="workloads-able-to-be-transitioned-to-intune"></a>Cargas de trabalho capazes de ser transferido para o Intune
Determinadas cargas de trabalho estão disponíveis para mudar ao longo para o Intune. A lista seguinte será atualizada como cargas de trabalho se tornar disponíveis para a transição:
1. Políticas de conformidade do dispositivo
2. Políticas de acesso de recursos: Políticas de acesso de recurso configurar VPN, Wi-Fi, e-mail e as definições do certificado em dispositivos. Para obter mais informações, consulte [implementar perfis de acesso a recursos](https://docs.microsoft.com/intune/device-profiles).
      - Perfil de e-mail
      - Perfil de Wi-Fi
      - Perfil da VPN
      - Perfil de certificado
3. Políticas de atualização do Windows
4. Proteção de ponto de extremidade (a partir do Configuration Manager versão 1802)
      - Windows Defender Application Guard
      - Firewall do Windows Defender
      - Windows Defender SmartScreen
      - Encriptação do Windows
      - O Windows Defender Exploit Guard
      - Controlo de aplicações do Windows Defender
      - Centro de segurança do Windows Defender
      - Proteção avançada contra ameaças do Windows Defender
      - Proteção de informações do Windows

5. Configuração do dispositivo (a partir do Configuration Manager versão 1806) <!--1357903-->
       - Mover a carga de trabalho de configuração do dispositivo também move os **acesso a recursos** e **Endpoint Protection** cargas de trabalho a partir da versão 1806.
       - A partir da versão 1806, pode continuar a implementar as definições do Configuration Manager para dispositivos cogeridos, apesar do Intune é a autoridade de configuração de dispositivos. Essa exceção pode ser utilizada para configurar as definições que são necessárias pela sua organização, mas ainda não está disponível no Intune. Especifique esta exceção num [linha base de configuração do Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines.md). Ativar a opção para **sempre aplicam-se esta linha de base, mesmo para clientes cogeridos** ao criar a linha de base ou no **geral** separador das propriedades de uma linha de base existente.
6. Aplicações de clique-e-Use do Office 365 (a partir do Configuration Manager versão 1806) <!--1357841-->
       - Depois de mover a carga de trabalho, a aplicação é apresentada no **Portal da empresa** no dispositivo.
       - Atualizações do Office podem demorar cerca de 24 horas a aparecer no cliente, a menos que os dispositivos são reiniciados. 
       - Há uma nova condição global **aplicações do Office 365 são geridas pelo Intune no dispositivo**. Esta condição é adicionada por padrão, como um requisito para novos aplicativos do Office 365. Faça a transição esta carga de trabalho, clientes cogeridos não cumpre o requisito no aplicativo, assim, a não instalar o Office 365 implementado através do Configuration Manager.
7. Aplicações móveis (a partir do Configuration Manager versão 1806 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features)) <!--1357892-->
      - Depois de mudar esta carga de trabalho, todas as aplicações disponíveis implementadas a partir do Intune estão disponíveis no Portal da empresa. 
      -  Aplicações que implementa a partir do Configuration Manager estão disponíveis no Centro de Software.

## <a name="monitor-co-management"></a>Monitor de cogestão
Depois de ativar a cogestão, pode monitorizar dispositivos de cogestão através dos seguintes métodos:

- [O dashboard de cogestão](/sccm/core/clients/manage/co-management-dashboard)
- **SQL exibição e a classe WMI de**: Pode consultar o **v&#95;ClientCoManagementState** vista SQL na base de dados do site do Configuration Manager ou o **SMS&#95;Client&#95;ComanagementState** classe WMI. Com as informações na classe WMI, pode criar coleções personalizadas no Configuration Manager para ajudar a determinar o estado da implementação da cogestão. Para obter detalhes, consulte [como criar coleções](/sccm/core/clients/manage/collections/create-collections). Os campos seguintes estão disponíveis na vista de SQL e classe WMI: 
    - **MachineId**: Especifica um ID de dispositivo exclusivo para o cliente do Configuration Manager.
    - **MDMEnrolled**: Especifica se o dispositivo está inscrito para MDM. 
    - **Autoridade**: Especifica a autoridade para o qual o dispositivo é inscrito.
    - **ComgmtPolicyPresent**: Especifica se a política de cogestão do Configuration Manager existe no cliente. Se o **MDMEnrolled** valor é **0**, o dispositivo não estiver. conjuntamente geridos independentemente se a política de cogestão existe no cliente.

   > [!Note]    
   > Um dispositivo é cogeridos quando o **MDMEnrolled** campo e **ComgmtPolicyPresent** ambos os campos têm um valor de **1**.

- **Políticas de implementação**:  Duas políticas são criadas no **monitorização** > **implementações**, um para o grupo piloto e outra para produção. Estas políticas apenas o número de dispositivos onde o Configuration Manager tem aplicada a política de relatório. Eles não considerarem quantos dispositivos estão inscritos no Intune, que é um requisito antes dos dispositivos podem ser geridos conjuntamente.  

## <a name="check-compliance-for-co-managed-devices"></a>Verificar a conformidade para dispositivos cogeridos
Os utilizadores podem utilizar o Centro de Software para verificar a conformidade dos respetivos dispositivos Windows 10 cogeridos se o acesso condicional é gerido pelo Intune ou do Configuration Manager. Os utilizadores também podem verificar a conformidade com a aplicação de Portal da empresa quando o acesso condicional é gerido pelo Intune.

## <a name="next-steps"></a>Passos seguintes
Utilize os seguintes recursos para ajudar a gerir as cargas de trabalho que alternar para o Intune:
- [Políticas de conformidade do dispositivo](https://docs.microsoft.com/intune/device-compliance-get-started)
- [Políticas de acesso de recursos](https://docs.microsoft.com/intune/device-profiles)
- [Atualização do Windows para políticas de negócio](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [Proteção de ponto final para o Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)

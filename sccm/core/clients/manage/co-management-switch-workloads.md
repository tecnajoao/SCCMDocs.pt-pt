---
title: Mudar as cargas de trabalho do Configuration Manager para o Intune
titleSuffix: Configuration Manager
description: Saiba como mudar cargas de trabalho atualmente gerenciadas pelo Configuration Manager para o Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/10/2018
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 94e7e62d71d44abc2a069e814738d5ac6fecb174
ms.sourcegitcommit: 4659946369d5352234f27c7682bce65a0e86c697
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/12/2018
ms.locfileid: "53303810"
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>Mudar as cargas de trabalho do Configuration Manager para o Intune

Depois de [preparar os dispositivos Windows 10 para a cogestão](/sccm/core/clients/manage/co-management-prepare), a próxima etapa é ativar a inscrição automática do cliente para o Intune. Em seguida, quando estiver pronto, comece a alternância de cargas de trabalho específicas do Configuration Manager para o Intune. 


## <a name="setup-co-management"></a>Configurar cogestão

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **serviços Cloud**e selecione o **cogestão** nó.  

2. Na **home page** separador do Friso, no **gerir** de grupo, escolha **configurar cogestão**. Esta ação abre o Assistente de configuração de cogestão.  

3. Na página de subscrição, selecione **sessão**. Inicie sessão no seu inquilino do Intune e, em seguida, selecione **seguinte**.  

4. Na página de ativação, escolha **piloto** ou **todos os**.  

    Esta ação permite a inscrição automática do cliente no Intune. Quando escolhe **piloto**, apenas os clientes do Configuration Manager que são membros da coleção piloto são automaticamente inscritos no Intune. Esta opção permite-lhe ativar a cogestão num subconjunto de clientes para testar inicialmente cogestão e cogestão de implementação de forma faseada.  

    Utilize a linha de comando exibida para implementar o cliente do Configuration Manager como uma aplicação no Intune para dispositivos já inscritos no Intune. Para obter mais informações, consulte [dispositivos Windows 10 inscritos no Intune](/sccm/core/clients/manage/co-management-prepare#windows-10-devices-enrolled-in-intune).  

5. Na página de cargas de trabalho, escolha se pretende mudar cargas de trabalho do Configuration Manager para ser gerido pelo Intune. Pode ativar a inscrição na página anterior sem mudar de quaisquer cargas de trabalho neste momento. 

    O **Intune piloto** definição muda a carga de trabalho associada apenas para os dispositivos na coleção piloto. O **Intune** definição muda a carga de trabalho associada para todos os dispositivos Windows 10 cogeridos.  

    > [!Important] 
    > Antes de alternar quaisquer cargas de trabalho, certifique-se de configurar corretamente e deploye a carga de trabalho correspondente no Intune. Certifique-se de que as cargas de trabalho são sempre gerenciadas por uma das ferramentas de gerenciamento para os seus dispositivos.  

6. Na página de teste, configure as seguintes definições:  

    - **Piloto**: O grupo piloto contém uma ou mais coleções que selecionar. Utilize este grupo como parte da sua implementação faseada de cogestão. Começar com uma coleção de teste pequeno e, em seguida, adicione mais coleções no grupo piloto, como implementar a cogestão para obter mais utilizadores e dispositivos. Pode alterar as coleções no grupo piloto em qualquer altura.  

    - **Produção**: Configurar o **grupo de exclusão** com uma ou mais coleções. Dispositivos que são membros de qualquer uma das coleções deste grupo são excluídos da cogestão a utilizar.  

7. Para ativar a cogestão, conclua o assistente.  

<!--1357377--> Os dispositivos cogeridos automaticamente a partir do Configuration Manager versão 1806, quando alterna uma carga de trabalho de cogestão, sincronizar política MDM do Microsoft Intune. Esta sincronização ocorre também quando inicia o **transferir política do computador** ação a partir de notificações do cliente na consola do Configuration Manager. Para obter mais informações, consulte [iniciar a obtenção de política de cliente com a notificação do cliente](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).



## <a name="modify-your-co-management-settings"></a>Modificar as definições de cogestão

Depois de ativar a cogestão utilizando o assistente, modifique as definições nas propriedades de cogestão. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **serviços Cloud**e selecione o **cogestão** nó. Selecione o objeto de cogestão e, em seguida, selecione **propriedades** na faixa de opções. 



## <a name="supported-workloads"></a>Cargas de trabalho suportadas

As cargas de trabalho seguintes estão atualmente disponíveis mudar do Configuration Manager para o Intune:

- **Políticas de conformidade do dispositivo**  

- **Políticas de acesso de recurso**: Para obter mais informações sobre estas políticas do Intune, consulte [implementar perfis de acesso a recursos](https://docs.microsoft.com/intune/device-profiles).
    - Perfil de e-mail  
    - Perfil Wi-Fi  
    - Perfil VPN  
    - Perfil de certificado  

- **Políticas de atualização do Windows**  

- **Proteção de ponto final**: A partir do Configuration Manager versão 1802, esta carga de trabalho inclui as seguintes funcionalidades:  
    - Windows Defender Application Guard  
    - Firewall do Windows Defender  
    - Windows Defender SmartScreen  
    - Encriptação do Windows  
    - O Windows Defender Exploit Guard  
    - Controlo de aplicações do Windows Defender  
    - Centro de segurança do Windows Defender  
    - Proteção Avançada Contra Ameaças do Windows Defender  
    - Proteção de informações do Windows  

- **Configuração do dispositivo**: A partir do Configuration Manager versão 1806<!--1357903-->:  

    - Mover a carga de trabalho de configuração do dispositivo também move os **acesso a recursos** e **Endpoint Protection** cargas de trabalho  

    - Pode continuar a implementar as definições do Configuration Manager para dispositivos cogeridos, apesar do Intune é a autoridade de configuração de dispositivos. Essa exceção pode ser utilizada para configurar as definições que são necessárias pela sua organização, mas ainda não está disponível no Intune. Especifique esta exceção num [linha base de configuração do Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines). Ativar a opção para **sempre aplicam-se esta linha de base, mesmo para clientes cogeridos** ao criar a linha de base ou no **geral** separador das propriedades de uma linha de base existente.  

- **Aplicações de clique-e-Use do Office 365**: A partir do Configuration Manager versão 1806<!--1357841-->:  

    - Depois de mover a carga de trabalho, a aplicação é apresentada no **Portal da empresa** no dispositivo  

    - Atualizações do Office podem demorar cerca de 24 horas a aparecer no cliente, a menos que os dispositivos são reiniciados  

    - Há uma nova condição global **aplicações do Office 365 são geridas pelo Intune no dispositivo**. Esta condição é adicionada por padrão, como um requisito para novos aplicativos do Office 365. Faça a transição esta carga de trabalho, os clientes cogeridos não cumprem o requisito no aplicativo. Em seguida, o que eles não instalarem o Office 365 implementado através do Configuration Manager.  

- **Aplicações de cliente**: A partir do Configuration Manager versão 1806 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features))<!--1357892-->:  

    - Depois de mudar esta carga de trabalho, todas as aplicações disponíveis implementadas a partir do Intune estão disponíveis no Portal da empresa  

    - Aplicações que implementa a partir do Configuration Manager estão disponíveis no Centro de Software  



## <a name="monitor-co-management"></a>Monitor de cogestão

Depois de ativar a cogestão, monitorize dispositivos de cogestão através dos seguintes métodos:

- [O dashboard de cogestão](/sccm/core/clients/manage/co-management-dashboard)  

- **SQL exibição e a classe WMI de**: Consulta a **v_ClientCoManagementState** vista SQL na base de dados do site do Configuration Manager ou o **SMS_Client_ComanagementState** classe WMI. Com as informações na classe WMI, pode criar coleções personalizadas no Configuration Manager para ajudar a determinar o estado da implementação da cogestão. Para obter detalhes, consulte [como criar coleções](/sccm/core/clients/manage/collections/create-collections). Os campos seguintes estão disponíveis na vista de SQL e classe WMI:  
    - **MachineId**: Especifica um ID de dispositivo exclusivo para o cliente do Configuration Manager  
    - **MDMEnrolled**: Especifica se o dispositivo é inscrito para MDM  
    - **Autoridade**: Especifica a autoridade para o qual o dispositivo está inscrito  
    - **ComgmtPolicyPresent**: Especifica se a política de cogestão do Configuration Manager existe no cliente. Se o **MDMEnrolled** valor é **0**, o dispositivo não está conjuntamente gerido independentemente disso, se a política de cogestão existe no cliente.  

    > [!Note]  
    > Um dispositivo é cogeridos quando o **MDMEnrolled** campo e **ComgmtPolicyPresent** ambos os campos têm um valor de **1**.  

- **Políticas de implementação**: Duas políticas são criadas no **implementações** nó da **monitorização** área de trabalho. É uma política para o grupo piloto e outro para produção. Estas políticas apenas o número de dispositivos onde o Configuration Manager tem aplicada a política de relatório. Eles não considerarem quantos dispositivos estão inscritos no Intune, que é um requisito antes dos dispositivos podem ser geridos conjuntamente.  



## <a name="check-compliance-for-co-managed-devices"></a>Verificar a conformidade para dispositivos cogeridos

Os utilizadores podem utilizar o Centro de Software para verificar a conformidade dos respetivos dispositivos Windows 10 cogeridos se o acesso condicional é gerido pelo Intune ou do Configuration Manager. Os utilizadores também podem verificar a conformidade com a aplicação de Portal da empresa quando o acesso condicional é gerido pelo Intune.



## <a name="next-steps"></a>Passos seguintes

Utilize os seguintes recursos para ajudar a gerir as cargas de trabalho que alternar para o Intune:
- [Políticas de conformidade do dispositivo](https://docs.microsoft.com/intune/device-compliance-get-started)
- [Políticas de acesso de recursos](https://docs.microsoft.com/intune/device-profiles)
- [Atualização do Windows para políticas de negócio](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [Proteção de ponto final para o Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)

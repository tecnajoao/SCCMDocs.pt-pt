---
title: Cargas de trabalho do Gestor de configuração do comutador para o Intune
titleSuffix: System Center Configuration Manager
description: Saiba como mudar de cargas de trabalho atualmente geridas pelo Configuration Manager para o Microsoft Intune.
ms.prod: configuration-manager
ms.suite: na
ms.technology:
- configmgr-client
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.service: ''
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: cdfe52768499b929db473ac08d42207059965ffd
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>Cargas de trabalho do Gestor de configuração do comutador para o Intune
No [dispositivos de preparar o Windows 10 para gestão conjunta](co-management-prepare.md), preparou a dispositivos Windows 10 para gestão conjunta. Estes dispositivos estão associados ao AD, o Azure AD, estão inscritos no Intune e têm o cliente do Configuration Manager. Provavelmente, ainda tem de dispositivos Windows 10 que estão associados ao AD e o cliente do Configuration Manager, mas não associados ao Azure AD ou inscritos no Intune. O procedimento seguinte fornece os passos para ativar a gestão conjunta, preparar o resto dos seus dispositivos Windows 10 (clientes do Configuration Manager sem inscrição no Intune) para a gestão conjunta e permite-lhe iniciar mudar específico do Configuration Manager cargas de trabalho para o Intune.

1. Na consola do Configuration Manager, vá para **administração** > **descrição geral** > **serviços em nuvem**  >  **Gestão conjunta**.    
2. No separador início, no grupo de gerir, escolha **configurar a gestão conjunta** para abrir o Assistente de configuração de gestão conjunta.    
3. Na página de subscrição, clique em **sessão** e inicie sessão no seu inquilino do Intune e, em seguida, clique em **seguinte**.   
4. Na página de ativação, escolha o **piloto** ou **todos os** para ativar a inscrição automática no Intune e, em seguida, clique em **seguinte**. Quando escolhe **piloto**, apenas os clientes de Gestor de configuração são membros do grupo piloto automaticamente estão inscritos no Intune. Esta opção permite-lhe ativar a gestão conjunta num subconjunto de clientes para testar inicialmente conjunta gestão e implementação da gestão conjunta utilizando uma abordagem faseada. A linha de comandos pode ser utilizada para implementar o cliente do Configuration Manager como uma aplicação no Intune para dispositivos já inscritos no Intune. Para obter mais informações, consulte [dispositivos Windows 10 inscritos no Intune](co-management-prepare.md#windows-10-devices-enrolled-in-intune).
5. Na página de cargas de trabalho, escolha se pretende mudar cargas de trabalho do Configuration Manager para serem geridos pelo Intune piloto ou o Intune e, em seguida, clique em **seguinte**. O **piloto Intune** definição muda a carga de trabalho associada apenas para os dispositivos no grupo de piloto. O **Intune** definição muda a carga de trabalho associada para todos os dispositivos Windows 10 geridos conjuntamente. 
        
   > [!Important]    
   > Antes de mudar todas as cargas de trabalho, certifique-se a carga de trabalho correspondente no Intune foi corretamente configurada e implementada. Se o fizer, assegura que as cargas de trabalho são sempre geridas por uma das ferramentas de gestão para os seus dispositivos.   
1. Na página de teste, configure as seguintes definições e, em seguida, clique em **seguinte**:
    - **Piloto**: O grupo piloto contém uma ou mais coleções que selecionar. Utilize este grupo como parte da sua implementação faseada de gestão conjunta. Pode começar com uma coleção de pequeno teste e, em seguida, adicione mais coleções ao grupo piloto como implementar gestão conjunta a mais utilizadores e dispositivos. Pode alterar as coleções no grupo de piloto em qualquer momento a partir das propriedades de gestão conjunta.
    - **Produção**: Configurar o **grupo de exclusão** com uma ou mais coleções. Dispositivos que são membros de qualquer uma das coleções deste grupo são excluídos da gestão conjunta a utilizar. 
2. Para ativar a gestão conjunta, conclua o assistente.  

## <a name="modify-your-co-management-settings"></a>Modificar as definições de gestão conjunta
Depois de ativar a gestão conjunta utilizando o assistente, pode modificar as definições nas propriedades de gestão conjunta.  
- Na consola do Configuration Manager, vá para **administração** > **descrição geral** > **serviços em nuvem**  >  **Gestão conjunta**.  
Selecione o objeto de gestão conjunta e, em seguida, no separador início, clique em **propriedades**. 

## <a name="workloads-able-to-be-transitioned-to-intune"></a>Cargas de trabalho podem ser transitado para o Intune
Algumas cargas de trabalho estão disponíveis para ser mudado ao longo do Intune. A lista seguinte será atualizada como fiquem disponíveis para transição de cargas de trabalho:
1. Políticas de conformidade do dispositivo
2. Políticas de acesso a recursos
3. Políticas de Windows Update
4. Proteção de ponto final (a partir do Configuration Manager versão 1802)
      - Windows Defender antivírus
      - Proteção de aplicações do Windows Defender
      - Firewall do Windows Defender
      - Windows Defender SmartScreen
      - Encriptação do Windows
      - Proteção de exploração do Windows Defender
      - Controlo de aplicação do Windows Defender
      - Centro de segurança do Windows Defender
      - O Windows Defender Advanced Threat Protection



## <a name="monitor-co-management"></a>Gestão de coadministrador do monitor
Depois de ativar a gestão conjunta, pode monitorizar dispositivos de gestão conjunta utilizando os seguintes métodos:
- **SQL Server vista e a classe WMI**: Pode consultar o **v&#95;ClientCoManagementState** vista SQL na base de dados do site do Configuration Manager ou o **SMS&#95;cliente&#95;ComanagementState** classe WMI. Com as informações da classe WMI, pode criar coleções personalizadas no Configuration Manager para ajudar a determinar o estado da implementação gestão conjunta. Para obter mais informações, consulte [como criar coleções](/sccm/core/clients/manage/collections/create-collections). Os campos seguintes estão disponíveis na vista SQL e a classe WMI: 
    - **MachineId**: Especifica um ID de dispositivo exclusivo para o cliente do Configuration Manager.
    - **MDMEnrolled**: Especifica se o dispositivo está inscrito no MDM. 
    - **Autoridade**: Especifica a autoridade para o qual o dispositivo está inscrito.
    - **ComgmtPolicyPresent**: Especifica se a política de gestão conjunta do Configuration Manager existe no cliente. Se o **MDMEnrolled** valor é **0**, o dispositivo não for conjuntamente gerido independentemente se a política de gestão conjunta existe no cliente.

   > [!Note]    
   > Um dispositivo é gerido conjuntamente quando o **MDMEnrolled** campo e **ComgmtPolicyPresent** ambos os campos tenham um valor de **1**.

- **As políticas de implementação**:  Existem duas políticas que criou no **monitorização** > **implementações**; uma política para o grupo de piloto e outro para produção. Estas políticas apenas comunicam o número de dispositivos em que o Configuration Manager tem aplicada a política. Não considere quantos dispositivos estão inscritos no Intune, que é um requisito antes dos dispositivos podem ser geridos conjuntamente.  

## <a name="check-compliance-for-co-managed-devices"></a>Verificação de conformidade para dispositivos geridos conjuntamente
Os utilizadores podem utilizar o Centro de Software para verificar a compatibilidade dos respetivos dispositivos Windows 10 geridos conjuntamente independentemente se o acesso condicional é gerido pelo Configuration Manager ou o Intune. Os utilizadores também podem verificar conformidade utilizando a aplicação Portal da empresa quando o acesso condicional é gerido pelo Intune.

## <a name="next-steps"></a>Passos seguintes
Utilize os seguintes recursos para ajudar a gerir as cargas de trabalho que muda para o Intune:
- [Políticas de conformidade do dispositivo](https://docs.microsoft.com/intune/device-compliance-get-started)
- [Políticas de acesso a recursos](https://docs.microsoft.com/intune/device-profiles)
- [Windows Update para as políticas de negócio](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [Endpoint Protection para o Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)

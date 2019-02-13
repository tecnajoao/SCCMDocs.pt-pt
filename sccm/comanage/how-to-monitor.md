---
title: Monitorizar a cogestão
titleSuffix: Configuration Manager
description: Utilize o dashboard de cogestão para rever as informações sobre dispositivos cogeridos.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c731692bc2277cc5ce97e079387b392ca09ff3e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134017"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>Como monitorizar a cogestão no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Depois de ativar a cogestão, monitorize dispositivos de cogestão através dos seguintes métodos:

- [Dashboard de cogestão](#co-management-dashboard)  

- [Políticas de implementação](#deployment-policies)

- [Dados de dispositivo WMI](#wmi-device-data)



## <a name="co-management-dashboard"></a>Dashboard de cogestão

A partir da versão 1802, ver um dashboard com informações sobre a cogestão. O dashboard ajuda-o a rever as máquinas que fazem cogeridas no seu ambiente. Os gráficos podem ajudar a identificar os dispositivos que possam necessitar de atenção.<!--1356648-->

Na consola do Configuration Manager, vá para o **monitorização** área de trabalho e selecione o **cogestão** nó.

A partir da versão 1810, o dashboard de cogestão é aprimorado com informações mais detalhadas. <!--1358980-->

![Captura de ecrã do dashboard de cogestão](media/co-management-dashboard.png)


### <a name="co-managed-devices"></a>Dispositivos cogeridos

*Aplica-se a versões 1802 e 1806*

Mostra a percentagem de dispositivos cogeridos em todo o seu ambiente.

![Mosaico de dispositivos cogeridos](media/co-management-dashboard/Percent-Co-managed-graph.PNG)


### <a name="client-os-distribution"></a>Distribuição de SO de cliente

*Aplica-se a todas as versões* 

Mostra o número de cliente dispositivos por sistema operacional por versão. Ele usa os seguintes agrupamentos:  
- Windows 7 & 8.x  
- Windows 10 inferior a 1709  
- Windows 10 1709 e superior  

    > [!Tip]  
    > Windows 10, versão 1709 ou posterior, é um pré-requisito para a cogestão.  

Coloque o cursor sobre uma seção de gráfico para mostrar a percentagem de dispositivos nesse grupo de sistema operacional.

![Mosaico de distribuição de SO de cliente](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)


### <a name="co-management-status-donut"></a>Estado de cogestão (anel)

*Aplica-se a versões 1802 e 1806*

Mostra a divisão de dispositivo êxito ou falha nas seguintes categorias:
- Êxito, Azure AD híbrido associado  
- Êxito, associados ao Azure AD  
- Falha de: Inscrição automática falhou  

Coloque o cursor sobre uma seção de gráfico para mostrar a percentagem de dispositivos dessa categoria. 

![Mosaico de estado (anel) de cogestão](media/co-management-dashboard/Co-management-status-graph.PNG)

Selecione uma seção de gráfico para ver a lista de dispositivos dessa categoria.

![Lista de dispositivos de falha de inscrição](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)


### <a name="co-management-status-funnel"></a>Estado de cogestão (funil)

*Aplica-se a versão 1810 e posterior*

Um gráfico de funil que mostra o número de dispositivos com os seguintes Estados do processo de inscrição:  
- Dispositivos elegíveis  
- Agendado  
- Inscrição iniciada  
- Inscritos  

![Mosaico de estado (funil) de cogestão](media/co-management-dashboard/1358980-status-funnel.png)


### <a name="co-management-enrollment-status"></a>Estado de inscrição de cogestão

*Aplica-se a versão 1810 e posterior*

Mostra a divisão de estado do dispositivo nas seguintes categorias:
- Êxito, híbrido do Azure AD associado  
- Êxito, Azure AD associado  
- A inscrição, híbrido do Azure AD associado  
- Falha, híbrido do Azure AD associado  
- Falha, o Azure AD associado  
- Início de sessão de utilizadores pendentes  

Selecione um Estado no mosaico para explorar para obter uma lista de dispositivos com esse Estado.  

![Mosaico de estado de inscrição de cogestão](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="workload-transition"></a>Transição da carga de trabalho

*Aplica-se a todas as versões*

Apresenta um gráfico de barras com o número de dispositivos que tenha transferido para o Microsoft Intune para as cargas de trabalho disponíveis. 

A lista de cargas de trabalho varia consoante a versão do Configuration Manager. Para obter mais informações, consulte [cargas de trabalho capazes de ser transferido para o Intune](/sccm/comanage/workloads).

Coloque o cursor sobre uma seção de gráfico para ver o número de dispositivos a transição para a carga de trabalho. 

![Gráfico de barras de transição de carga de trabalho](media/co-management-dashboard/Workload-Transition.PNG)


### <a name="enrollment-errors"></a>Erros de inscrição

*Aplica-se a versão 1810 e posterior*

Esta tabela é uma lista de erros de inscrição de dispositivos. Estes erros podem vir do componente MDM no Windows, o núcleo do sistema operacional do Windows ou o cliente do Configuration Manager. 

Existem centenas de possíveis erros. A tabela seguinte lista os erros mais comuns.
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| Erro | Descrição |
|---------|---------|
| 2147549183 (0x8000FFFF) | Não foi configurada a inscrição MDM ainda no Azure AD, ou a inscrição do URL não é esperado.<br><br>[Ativar a inscrição automática do Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | É de licença de usuário no registro de bloqueio de um Estado inválido<br><br>[Atribuir licenças aos utilizadores](https://docs.microsoft.com/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | Ao tentar automaticamente se inscreverem no Intune, mas a configuração do Azure AD não está totalmente aplicada. Este problema deve ser transitório, como as repetições de dispositivo após um curto período de tempo. |
| 2149056554 (0x‭8018002A‬)<br>&nbsp; | O utilizador cancelou a operação<br><br>Se a inscrição MDM requer autenticação multifator e o utilizador ainda não tiver iniciado sessão com um segundo fator suportado, o Windows apresenta uma notificação de alerta para o utilizador para se inscrever. Se o utilizador não responder a notificação de alerta, este erro ocorre. Este problema deve ser transitório, como o Configuration Manager irá repetir e pedir ao utilizador. Os utilizadores devem utilizar a autenticação multifator quando iniciam sessão no Windows. Também educá-las esperassem esse comportamento e se lhe for pedido, execute as ações. | 
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | Gestão de dispositivos móveis em geral não suportado | 
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | Falha ao autenticar o utilizador do servidor<br><br> Não existe nenhum token do Azure AD para o utilizador. Certifique-se de que o usuário possa autenticar para o Azure AD. |
| 2147942450 (0x‭80070032‬)<br>&nbsp; | Inscrição automática MDM só é suportada no Windows RS3 e posteriores.<br><br>Certifique-se de que o dispositivo cumpra a [os requisitos mínimos](/sccm/comanage/overview#windows-10) para a cogestão. |
| 3400073293 | Resposta de conta de realm de usuário da ADAL desconhecida<br><br>Verifique a configuração do Azure AD e certifique-se de que os utilizadores podem autenticar com êxito. | 
| 3399548929 | Tem de utilizador iniciar sessão<br><br>Este problema deve ser transitório. Isso ocorre quando o utilizador rapidamente termina antes da tarefa de inscrição acontece. | 
| 3400073236 | Falha no pedido de token de segurança da ADAL.<br><br>Verifique a configuração do Azure AD e certifique-se de que os utilizadores podem autenticar com êxito. |
| 2149122477 | Problema HTTP genérico |
| 3400073247 | A autenticação ADAL integrada do Windows só é suportada no flow federado<br><br>[Planear a sua implementação híbrida do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) | 
| 3399942148 | O servidor ou proxy não foi encontrado.<br><br>Este problema deve ser transitório, quando o cliente não consegue comunicar com a nuvem. Se persistir, certifique-se de que o cliente tiver conectividade consistente para o Azure. | 
| 2149056532 | Plataforma específica ou a versão não é suportada<br><br>Certifique-se de que o dispositivo cumpra a [os requisitos mínimos](/sccm/comanage/overview#windows-10) para a cogestão. |
| 2147943568 | Elemento não encontrado<br><br>Este problema deve ser transitório. Se persistir, contacte Support da Microsoft. |
| 2192179208 | Recursos de memória insuficiente estão disponíveis para processar este comando.<br><br>Este problema deve ser transitório, ele deve resolvido de forma automática quando o cliente tenta novamente. |
| 3399614467 | Falha na concessão de autorização da ADAL para esta asserção<br><br>Verifique a configuração do Azure AD e certifique-se de que os utilizadores podem autenticar com êxito. |
| 2149056517 | Falha genérica do servidor de gestão, como o erro de acesso de DB<br><br>Este problema deve ser transitório. Se persistir, contacte Support da Microsoft. |
| 2149134055 | Nome de WinHTTP não resolvido<br><br>O cliente não é possível resolver o nome do serviço. Verifique a configuração de DNS. | 
| 2149134050 | tempo limite da Internet<br><br>Este problema deve ser transitório, quando o cliente não consegue comunicar com a nuvem. Se persistir, certifique-se de que o cliente tiver conectividade consistente para o Azure. | 


Para obter mais informações, consulte [valores de erro de registo do MDM](https://docs.microsoft.com/windows/desktop/mdmreg/mdm-registration-constants).



## <a name="deployment-policies"></a>Políticas de implementação

Duas políticas são criadas no **implementações** nó da **monitorização** área de trabalho. É uma política para o grupo piloto e outro para produção. Estas políticas apenas o número de dispositivos onde o Configuration Manager tem aplicada a política de relatório. Eles não considerarem quantos dispositivos estão inscritos no Intune, que é um requisito antes dos dispositivos podem ser geridos conjuntamente.  



## <a name="wmi-device-data"></a>Dados de dispositivo WMI

Consulta a **SMS_Client_ComanagementState** classe WMI. Pode criar coleções personalizadas no Configuration Manager, que ajudam a determinar o estado da implementação da cogestão. Para obter mais informações sobre como criar coleções personalizadas, consulte [como criar coleções](/sccm/core/clients/manage/collections/create-collections). 

Os campos seguintes estão disponíveis na classe WMI:  

- **MachineId**: Um ID de dispositivo exclusivo para o cliente do Configuration Manager  

- **MDMEnrolled**: Especifica se o dispositivo é inscrito para MDM  

- **Autoridade**: A autoridade para o qual o dispositivo está inscrito  

- **ComgmtPolicyPresent**: Especifica se a política de cogestão do Configuration Manager existe no cliente. Se o **MDMEnrolled** valor é **0**, o dispositivo não está conjuntamente gerido independentemente disso, se a política de cogestão existe no cliente.  

Um dispositivo é cogeridos quando o **MDMEnrolled** campo e **ComgmtPolicyPresent** ambos os campos têm um valor de **1**.  

---
title: Cargas de trabalho de cogestão
titleSuffix: Configuration Manager
description: Saiba mais sobre as cargas de trabalho que pode mudar do Configuration Manager para o Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.openlocfilehash: b03d97fc0246806a40d3b6bf56c4c80a0264503b
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54251195"
---
# <a name="co-management-workloads"></a>Cargas de trabalho de cogestão

Não tem de mudar as cargas de trabalho, ou pode fazê-los individualmente quando estiver pronto. O Configuration Manager continua a gerir todas as outras cargas de trabalho, incluindo essas cargas de trabalho que não mude para o Intune e não oferece suporte a todos os outros recursos do Configuration Manager que cogestão.

Cogestão suporta as seguintes cargas de trabalho:

- [Políticas de conformidade](#compliance-policies)  

- [Políticas de atualização do Windows](#windows-update-policies)  

- [Políticas de acesso de recursos](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Configuração do dispositivo](#device-configuration)  

- [Aplicações de clique-e-Use do Office](#office-click-to-run-apps)  

- [Aplicações de cliente](#client-apps)  



## <a name="compliance-policies"></a>Políticas de conformidade 

Políticas de conformidade definem as regras e definições que um dispositivo tem de cumprir para ser considerado conforme pelas políticas de acesso condicional. Também utilize políticas de conformidade para monitorizar e resolver problemas de conformidade com dispositivos independentemente do acesso condicional. 

Para obter mais informações sobre a funcionalidade do Intune, consulte [políticas de conformidade do dispositivo](https://docs.microsoft.com/intune/device-compliance-get-started).  



## <a name="windows-update-policies"></a>Políticas de atualização do Windows

Atualização do Windows para políticas de empresas permitem-lhe configurar políticas de diferimento de atualizações de funcionalidades do Windows 10 ou atualizações de qualidade para dispositivos Windows 10 geridos diretamente pelo Windows Update para empresas. 

Para obter mais informações sobre a funcionalidade do Intune, consulte [configurar o Windows Update para políticas de diferimento de negócios](https://docs.microsoft.com/intune/windows-update-for-business-configure).  



## <a name="resource-access-policies"></a>Políticas de acesso de recursos

Políticas de acesso de recurso configurar VPN, Wi-Fi, e-mail e as definições do certificado em dispositivos. 

Para obter mais informações sobre a funcionalidade do Intune, consulte [implementar perfis de acesso a recursos](https://docs.microsoft.com/intune/device-profiles).



## <a name="endpoint-protection"></a>Endpoint Protection
<!--1357365-->

A partir do Configuration Manager 1802, a carga de trabalho do Endpoint Protection inclui o conjunto do Windows Defender de funcionalidades de proteção antimalware: 

- Windows Defender Application Guard  
- Firewall do Windows Defender  
- Windows Defender SmartScreen  
- Encriptação do Windows  
- O Windows Defender Exploit Guard  
- Controlo de aplicações do Windows Defender  
- Centro de segurança do Windows Defender  
- Proteção Avançada Contra Ameaças do Windows Defender  
- Proteção de informações do Windows  

Para obter mais informações sobre a funcionalidade do Intune, consulte [Endpoint Protection do Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).



## <a name="device-configuration"></a>Configuração do dispositivo
<!--1357903-->

A partir do Configuration Manager 1806, a carga de trabalho de configuração de dispositivos inclui definições que gere para dispositivos na sua organização. Mudar esta carga de trabalho também move os **acesso a recursos** e **Endpoint Protection** cargas de trabalho.

Pode continuar a implementar as definições do Configuration Manager para dispositivos cogeridos, apesar do Intune é a autoridade de configuração de dispositivos. Essa exceção pode ser usada para configurar as definições de que sua organização requer, mas não ainda estão disponível no Intune. Especifique esta exceção num [linha base de configuração do Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines). Ativar a opção para **sempre aplicam-se esta linha de base, mesmo para clientes cogeridos** ao criar a linha de base. Pode alterá-lo mais tarde a **gerais** separador das propriedades de uma linha de base existente.  

Para obter mais informações sobre a funcionalidade do Intune, consulte [criar um perfil de dispositivo no Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create).  



## <a name="office-click-to-run-apps"></a>Aplicações de clique-e-Use do Office
<!--1357841-->

A partir do Configuration Manager 1806, esta carga de trabalho gerencia as aplicações do Office 365 em dispositivos cogeridos. 

- Depois de mover a carga de trabalho, a aplicação é apresentada no **Portal da empresa** no dispositivo  

- Atualizações do Office podem demorar cerca de 24 horas a aparecer no cliente, a menos que os dispositivos são reiniciados  

- Há uma nova condição global **aplicações do Office 365 são geridas pelo Intune no dispositivo**. Esta condição é adicionada por padrão, como um requisito para novos aplicativos do Office 365. Faça a transição esta carga de trabalho, os clientes cogeridos não cumprem o requisito no aplicativo. Em seguida, o que eles não instalarem o Office 365 implementado através do Configuration Manager.  

Para obter mais informações sobre a funcionalidade do Intune, consulte [aplicações de atribuir o Office 365 a dispositivos Windows 10 com o Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365). 



## <a name="client-apps"></a>Aplicações de cliente
<!--1357892-->

A partir do Configuration Manager versão 1806, utilize o Intune para gerir as aplicações de cliente em dispositivos cogeridos do Windows 10. Depois de mudar esta carga de trabalho, todas as aplicações disponíveis implementadas a partir do Intune estão disponíveis no Portal da empresa. Aplicações que implementa a partir do Configuration Manager estão disponíveis no Centro de Software.

Para obter mais informações sobre a funcionalidade do Intune, consulte [o que é a gestão de aplicações do Microsoft Intune?](https://docs.microsoft.com/intune/app-management). 

> [!Note]  
> A carga de trabalho de aplicações de cliente é uma funcionalidade de pré-lançamento. Para ativá-la, consulte [funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  



## <a name="next-steps"></a>Passos seguintes

[Como mudar as cargas de trabalho](/sccm/comanage/how-to-switch-workloads)  



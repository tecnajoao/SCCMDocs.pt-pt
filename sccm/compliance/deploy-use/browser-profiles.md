---
title: Configurar definições do Microsoft Edge
titleSuffix: Configuration Manager
description: Configurar definições para o browser Microsoft Edge em clientes Windows 10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.collection: M365-identity-device-management
ms.openlocfilehash: d97a67dd65dd79ba8b47541d0c7a7cad239dca28
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126039"
---
# <a name="configure-microsoft-edge-settings-in-system-center-configuration-manager"></a>Configurar definições do Microsoft Edge no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!-- 1357310 --> A partir da versão 1802, para os clientes que utilizam o [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) web browser em clientes Windows 10, criar uma política de definições de compatibilidade do Configuration Manager para configurar várias definições do Microsoft Edge. 

Esta política aplica-se apenas aos clientes no Windows 10, versão 1703 ou posterior. <!--511552-->


## <a name="policy-settings"></a>Definições de política
Atualmente, esta política inclui as seguintes definições:
- **Browser Microsoft Edge de conjunto como predefinição**: Configura a definição de aplicação de browser do Microsoft Edge predefinida de Windows 10
- **Permitir que a barra de endereços pendente**: Requer o Windows 10, versão 1703 ou posterior. Para obter mais informações, consulte [política de browser AllowAddressBarDropdown](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Sincronizar favoritos entre browsers da Microsoft de permitir**: Requer o Windows 10, versão 1703 ou posterior. Para obter mais informações, consulte [política de browser SyncFavoritesBetweenIEAndMicrosoftEdge](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Permitir a limpar dados de navegação à saída**: Requer o Windows 10, versão 1703 ou posterior. Para obter mais informações, consulte [política de browser ClearBrowsingDataOnExit](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Permitir cabeçalhos não controlar**: Para obter mais informações, consulte [política de browser AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Permitir Preenchimento automático**: Para obter mais informações, consulte [política de browser AllowAutofill](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Permitir cookies**: Para obter mais informações, consulte [política de browser AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Permitir Bloqueador de pop-up**: Para obter mais informações, consulte [política de browser AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Permitir sugestões de pesquisa na barra de endereço**: Para obter mais informações, consulte [política de browser AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Permitir o envio de tráfego de intranet para o Internet Explorer**: Para obter mais informações, consulte [política de browser SendIntranetTraffictoInternetExplorer](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Permitir Gestor de palavra-passe**: Para obter mais informações, consulte [política de browser AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Permitir ferramentas de programação**: Para obter mais informações, consulte [política de browser AllowDeveloperTools](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Permitir extensões**: Para obter mais informações, consulte [política de browser AllowExtensions](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).


### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Configurar as definições do Windows Defender SmartScreen para o Microsoft Edge
<!--1353701--> A partir da versão 1806, esta política adiciona três configurações para [Windows Defender SmartScreen](/windows/security/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview). A política agora inclui as seguintes definições adicionais sobre o **definições de SmartScreen** página:

- **Permite ao SmartScreen**: Especifica se o Windows Defender SmartScreen tem permissão. Para obter mais informações, consulte a [política de browser AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Os utilizadores podem substituir a linha de comandos do SmartScreen para sites**: Especifica se os utilizadores podem substituir os avisos do filtro do Windows Defender SmartScreen sobre sites potencialmente maliciosos. Para obter mais informações, consulte a [política de browser PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Os utilizadores podem substituir a linha de comandos do SmartScreen para ficheiros**: Especifica se os utilizadores podem substituir os avisos do filtro do Windows Defender SmartScreen sobre transferir ficheiros não verificados. Para obter mais informações, consulte a [política de browser PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="create-the-microsoft-edge-browser-profile"></a>Criar o perfil do browser Microsoft Edge

1. Na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho. Expanda **definições de compatibilidade** e selecione o **perfis de Browser do Microsoft Edge** nó. Clique na opção de faixa de opções para **perfil do Microsoft Edge criar**.
2. Especifique um **Name** para a política, opcionalmente, introduza um **Descrição**e clique em **seguinte**.
3. Sobre o **definições gerais** página, altere o valor para **configurado** para as definições a incluir nesta política e clique em **seguinte**. A definição para **definir a Browser Microsoft Edge como predefinido** tem de ser configurado para continuar.
4. Na versão 1806 e posterior, configure as definições na **definições de SmartScreen** página e, em seguida, clique em **próxima**. 
5. Sobre o **plataformas suportadas** , selecione as versões de SO e arquiteturas para a qual esta política aplica-se e clique em **próxima**. 
6. Conclua o assistente.



## <a name="deploy-the-policy"></a>Implementar a política

1. Selecione a política e clique na opção de faixa de opções para **Deploy**.
2. Clique em **procurar** para selecionar a coleção de utilizador ou dispositivo ao qual pretende implementar a política. 
3. Selecione as opções adicionais conforme necessário.  
     a. Gere alertas quando a política não está em conformidade.  
     b. Defina a agenda pela qual o cliente avalia a conformidade do dispositivo com esta política. 
4. Clique em **OK** para criar a implementação.



## <a name="next-steps"></a>Passos seguintes

Como qualquer política de definições de conformidade, o cliente efetua a remediação das definições na agenda que especificar. [Monitorizar e comunicar de conformidade do dispositivo](/sccm/compliance/deploy-use/monitor-compliance-settings) na consola do Configuration Manager.

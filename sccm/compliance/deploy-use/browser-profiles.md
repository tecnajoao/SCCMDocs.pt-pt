---
title: Configurar definições do Microsoft Edge
titleSuffix: Configuration Manager
description: Configurar definições do browser Microsoft Edge em clientes do Windows 10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/28/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 81bd0a59a24cab446668911f714548581c1347df
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32343801"
---
# <a name="configure-microsoft-edge-settings-in-system-center-configuration-manager"></a>Configurar definições do Microsoft Edge no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!-- 1357310 -->
A partir de versão 1802, para os clientes que utilizam o [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) web browser em clientes Windows 10, crie uma política de definições de compatibilidade do Configuration Manager para configurar várias definições do Microsoft Edge. 

Esta política aplica-se apenas aos clientes no Windows 10, versão 1703 ou posterior. <!--511552-->


## <a name="policy-settings"></a>Definições de política
Esta política atualmente inclui as seguintes definições:
- **Browser Microsoft Edge de conjunto como predefinição**: Configura a definição de aplicação do Windows 10 predefinida para o browser do Microsoft Edge
- **Permitir que a barra de endereço pendente**: Requer o Windows 10, versão 1703 ou posterior. Para obter mais informações, consulte [política de browser AllowAddressBarDropdown](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Permitir Sincronização Favoritos entre Microsoft browsers**: Requer o Windows 10, versão 1703 ou posterior. Para obter mais informações, consulte [política de browser SyncFavoritesBetweenIEAndMicrosoftEdge](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Permitir a navegação limpar dados de saída**: Requer o Windows 10, versão 1703 ou posterior. Para obter mais informações, consulte [política de browser ClearBrowsingDataOnExit](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Permitir que os cabeçalhos não controlar**: Para obter mais informações, consulte [política de browser AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Permitir Preenchimento automático**: Para obter mais informações, consulte [política de browser AllowAutofill](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Permitir cookies**: Para obter mais informações, consulte [política de browser AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Permitir Bloqueador de janelas de pop-up**: Para obter mais informações, consulte [política de browser AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Permitir sugestões de pesquisa na barra de endereço**: Para obter mais informações, consulte [política de browser AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Permitir o tráfego de intranet de envio para o Internet Explorer**: Para obter mais informações, consulte [política de browser SendIntranetTraffictoInternetExplorer](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Permitir palavra-passe manager**: Para obter mais informações, consulte [política de browser AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Permitir que as ferramentas de programador**: Para obter mais informações, consulte [política de browser AllowDeveloperTools](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Permitir extensões de**: Para obter mais informações, consulte [política de browser AllowExtensions](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).



## <a name="create-the-microsoft-edge-browser-profile"></a>Criar o perfil do browser Microsoft Edge

1. Na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho. Expanda **as definições de compatibilidade** e selecione o novo **perfis de Browser Microsoft Edge** nós. Clique na opção de friso para **criar política de Browser do Microsoft Edge**.
2. Especifique um **nome** para a política e, opcionalmente, introduza um **Descrição**e clique em **seguinte**.
3. No **definições** página, altere o valor para **configurado** para que as definições incluem nesta política e clique em **seguinte**.
4. No **plataformas suportadas** página, selecione as versões de sistema operativo e arquiteturas à qual esta política aplica-se e clique em **seguinte**. 
5. Conclua o assistente.



## <a name="deploy-the-policy"></a>Implementar a política

1. Selecione a política e clique na opção de friso para **implementar**.
2. Clique em **procurar** para selecionar a coleção de utilizador ou dispositivo ao qual pretende implementar a política. 
3. Selecione as opções adicionais conforme necessário. 
    a. Gere alertas quando a política não é compatível. 
    b. Defina o agendamento através do qual o cliente avalia a compatibilidade do dispositivo com esta política.
4. Clique em **OK** para criar a implementação.



## <a name="next-steps"></a>Passos seguintes

Como qualquer política de definições de conformidade, o cliente corrigir as definições na agenda que especificar. [Monitorizar e gerar relatórios sobre a conformidade de dispositivo](/sccm/compliance/deploy-use/monitor-compliance-settings) na consola do Configuration Manager.

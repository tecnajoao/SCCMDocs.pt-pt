---
title: "Nova versão 1710 | Microsoft Docs"
titleSuffix: Configuration Manager
description: "Obter informações sobre as alterações e novas funcionalidades introduzidas na versão 1710 do System Center Configuration Manager."
ms.custom: na
ms.date: 11/20/2017
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 33a5bff1e202822ce3ec5755958d34af461957e9
ms.sourcegitcommit: 536f7295e9ea361f1f9ead6c25f3685deb041ad8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/21/2017
---
# <a name="what39s-new-in-version-1710-of-system-center-configuration-manager"></a>O que &#39; s novidade na versão 1710 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Atualize 1710 para o ramo atual do System Center Configuration Manager está disponível como uma atualização na consola para sites anteriormente instalados com a versão 1610, 1702 ou 1706.

> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de linha de base do Configuration Manager.  
>  Saiba mais sobre:    
>   - [Instalar novos sites](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Instalar atualizações em sites](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As secções seguintes fornecem detalhes sobre as alterações e novas funcionalidades introduzidas na versão 1710 do Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated features](/sccm/core/plan-design/changes/removed-and-deprecated-features).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infraestrutura de sites

### <a name="updates-for-peer-cache-----sms500850---"></a>Atualizações para a Cache ponto a ponto<!-- sms500850 -->
A partir desta versão, a Cache já não é uma funcionalidade de pré-lançamento.  Não existem outras alterações para a Cache são introduzidas com esta versão. Para obter mais informações, consulte [Cache ponto a ponto para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>Suporte de ponto de distribuição de nuvem para a nuvem do Azure Government<!-- sms491428 -->
Agora, pode utilizar [pontos de distribuição baseado na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) na nuvem do Azure Government.   


<!-- ## Migration  -->


## <a name="client-management"></a>Gestão de clientes

### <a name="co-management-for-windows-10-devices"></a>Gestão conjunta para dispositivos Windows 10    
<!-- 1350871 -->
Iniciando com o Windows 10, versão 1607 (também conhecido como aniversário da atualização), pode associar um dispositivo Windows 10 no local do Active Directory (AD) e baseado na nuvem do Azure AD em simultâneo (híbrido do Azure AD). Gestão conjunta tira partido deste melhoramento e permite-lhe gerir em simultâneo os dispositivos Windows 10 através do Configuration Manager e o Intune. É uma solução que fornece uma ponte de tradicional para gestão moderna e dá-lhe um caminho para fazer a transição utilizando uma abordagem faseada. Para obter mais informações, consulte [conjunta management para Windows 10 dispositivos](/sccm/core/clients/manage/co-management-overview).

### <a name="restart-computers-form-the-configuration-manager-console-----1356283---"></a>Reinicie os computadores de forma a consola do Configuration Manager<!-- 1356283 -->
A partir desta versão, pode utilizar a consola do Configuration Manager para identificar dispositivos cliente que requerem o reinício e, em seguida, utilizar uma ação de notificação de cliente reiniciá-las.

Consulte [como gerir clientes no System Center Configuration Manager](/sccm/core/clients/manage/manage-clients#restart-clients)


<!--  ## Compliance settings  -->


## <a name="application-management"></a>Gestão de Aplicações
### <a name="improvements-for-run-scripts------1236459---"></a>Melhoramentos para executadas Scripts<!-- 1236459 -->
Esta versão inclui vários melhoramentos para o **executar Scripts** funcionalidade, que permite-lhe implementar scripts do PowerShell para executar em dispositivos geridos. Esta funcionalidade foi introduzida pela primeira vez na versão 1706.

Melhoramentos incluem:
- Utilize âmbitos de segurança para o ajudar a controlar quem pode utilizar Scripts de executar
- Monitorização dos scripts em tempo real, executar
- Parâmetros para a apresentação de script no Assistente de Script de criação, validação de suportar e são identificadas como obrigatórios ou opcionais.

Para obter mais informações sobre como utilizar executar Scripts, consulte [criar e executadas scripts](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Novas definições de política de gestão de aplicações móveis
<!-- 1324760 -->
Foram adicionadas as seguintes definições para as definições de política de gestão de aplicações móveis:
- **Desativar a sincronização de contactos**: Impede a aplicação de guardar os dados para a aplicação de contactos nativa no dispositivo.
- **Desativar a impressão**: Impede que a aplicação de trabalho de impressão ou dados escola.

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Centro de software já não distorts ícones maiores do que 250 x 250  
<!-- 1356194 -->

Com esta versão, o Centro de Software já não será distort ícones que são maiores do que 250 x 250. Centro de software efetuada essas ícones parecer blurry. Agora pode definir um ícone com um dimensões de pixel de até 512 x 512 e apresenta sem distortion.

Para adicionar um ícone para a sua aplicação no Centro de Software, consulte [criar aplicações](/sccm/apps/deploy-use/create-applications).

## <a name="operating-system-deployment"></a>Implementação do sistema operativo
 > [!TIP]   
 > <!-- 1354281 -->
 > A partir do Windows 10, versão 1709 (também conhecido como a atualização de criadores de reversão) versão, o suporte de dados do Windows inclui várias edições. Quando configurar uma sequência de tarefas para utilizar um pacote de atualização do sistema operativo ou a imagem do sistema operativo, é necessário selecionar um [edição que é suportada para utilização pelo Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

### <a name="add-child-task-sequences-to-a-task-sequence"></a>Adicionar sequências de tarefas de subordinados a uma sequência de tarefas
<!-- 1261338 -->

Pode adicionar um novo passo de sequência de tarefas é executada outra sequência de tarefas, que cria uma relação principal/subordinado entre as sequências de tarefas. Isto permite-lhe criar mais sequências de tarefas modulares que pode utilizar novamente.  

Para saber mais sobre a sequência de tarefas subordinadas, consulte o artigo [sequência de tarefas subordinado](/sccm/osd/understand/task-sequence-steps#child-task-sequence).

## <a name="software-center-customization"></a>Personalização de centro de software
<!-- 1351224 -->
Pode adicionar enterprise elementos de imagem corporativa e especificar a visibilidade dos separadores no Centro de Software. Pode adicionar o seu nome de empresa específica do Centro de Software, definir um tema de cor de configuração de centro de Software, defina um logótipo de empresa e definir os separadores visíveis para os dispositivos cliente.

Para obter mais informações, veja [Planear e configurar a gestão de aplicações no System Center Configuration Manager](/sccm/apps/plan-design/plan-for-and-configure-application-management).

## <a name="software-updates"></a>Atualizações de software

### <a name="surface-driver-updates-----1098490---"></a>Atualizações de controladores superfície<!-- 1098490 -->
A partir desta versão, gerir atualizações de controladores superfície já não é uma funcionalidade de pré-lançamento.  


## <a name="reporting"></a>Relatórios

### <a name="limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Limitar a telemetria melhorada do Windows 10 para apenas enviar dados relevantes para o estado de funcionamento de dispositivo de análise de Windows
<!-- 1356148 -->

Agora pode definir a recolha de dados de telemetria do Windows 10 para **avançado (limitado)**. Esta definição permite-lhe ganhar acionável conhecimentos aprofundados sobre os dispositivos no seu ambiente sem dispositivos que reportam a todos os dados no **avançado** nível de telemetria com o Windows 10 versão 1709 ou posterior.

Para obter mais informações, consulte [como configurar as definições de cliente no System Center Configuration Manager](/sccm/core/clients/deploy/configure-client-settings).

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>Gestão de dispositivos móveis

### <a name="windows-10-arm64-device-support"></a>Suporte de dispositivos Windows 10 ARM64
<!-- 1355000 -->

Cenários de gestão (MDM) de dispositivos móveis híbridos serão suportados em dispositivos ARM64 com o Windows 10 quando estes dispositivos estão disponíveis.

Estes cenários incluem:

- [Inscrever dispositivos](../../../mdm/deploy-use/enroll-hybrid-windows.md)
- [Executar ações de eliminação seletiva e completa](../../../mdm/deploy-use/wipe-lock-reset-devices.md)
- [Gerir as definições através de itens de configuração e linhas de base](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Gerir a política de conformidade](../../../mdm/deploy-use/device-compliance-policies.md)
- Gerir o acesso aos recursos da empresa através de:
   - [Perfis de certificados](../../../mdm/deploy-use/create-pfx-certificate-profiles.md)
   - [Perfis VPN](../../../mdm/deploy-use/create-vpn-profiles.md)
   - [Perfis de Wi-Fi](../../../mdm/deploy-use/create-wifi-profiles.md)
   - [Perfis de e-mail](../../../mdm/deploy-use/create-exchange-activesync-profiles.md)
- [Configurar o Windows Hello para a política de negócio](../../../mdm/deploy-use/windows-hello-for-business-settings.md)
- [Gerir aplicações](../../../mdm/deploy-use/management-tasks-applications.md)

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Experiência de perfil VPN melhorada na consola do Configuration Manager 
<!-- 1318232 -->

Com esta versão, atualizámos as páginas de assistente e propriedades de perfil VPN para apresentar as definições adequadas da plataforma selecionada:


- Cada plataforma tem o suas próprias fluxo de trabalho, que significa que os novos perfis VPN contém apenas a definição suportada pela plataforma do.
- O **plataformas suportadas** agora é apresentada a página depois do **geral** página.  Agora, escolher a plataforma antes de definir os valores de propriedade.
- Quando a plataforma está definida como **Android**, **Android para trabalho**, ou **Windows Phone 8.1**, a **plataformas suportadas** página não é necessária e é Não é apresentada.
- O Configuration Manager baseada em cliente fluxo de trabalho foi combinado com híbrida dispositivos móveis (MDM) baseada no cliente Windows 10 fluxos de trabalho; suportam as mesmas definições.
- Cada fluxo de trabalho de plataforma inclui apenas as definições adequadas para esse fluxo de trabalho.  Por exemplo, o fluxo de trabalho Android contém as definições adequadas para Android; as definições adequadas para iOS ou Windows 10 Mobile não aparecem no fluxo de trabalho Android.
- Para dispositivos Windows 8.1, tipos de ligação são geridos pelo cliente de Configuration Manager apenas (não é suportada pelo Intune) são claramente assinalado.
- A página de VPN automática está obsoleta e foi removida.

Aplicam estas alterações para novos perfis VPN.  

Para minimizar o risco de compatibilidade, perfis VPN existentes são iguais.  Ao editar um perfil existente, as definições são apresentadas como quando o perfil foi criado.  

Para obter mais informações, consulte [perfis VPN em dispositivos móveis no System Center Configuration Manager](../../../mdm/deploy-use/create-vpn-profiles.md).

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>Suporte limitado de criptografia: Certificados do próximos geração (CNG)<!-- 1356191 -->

O Configuration Manager limitou o suporte de criptografia: Certificados de geração (CNG) do seguintes. Clientes do Configuration Manager podem utilizar o certificado de autenticação de cliente PKI com chave privada no fornecedor de armazenamento de chaves do CNG (KSP). Com suporte para KSP, os clientes do Configuration Manager suportam a chave das privada baseada em hardware, tal como KSP de TPM para certificados de autenticação de cliente PKI.

Para obter mais informações, consulte [descrição geral de certificados CNG](../network/cng-certificates-overview.md).

## <a name="protect-devices"></a>Proteger dispositivos

### <a name="create-and-deploy-exploit-guard-policies"></a>Criar e implementar políticas de proteção Exploit
<!-- 1355468 -->

Pode [criar e implementar políticas](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) que gerir todos os quatro componentes do Windows Defender exploram Guard, incluindo a redução da superfície de ataque, a pasta controlada acesso, proteção de exploração e proteção de rede.

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Criar e implementar a política de proteção de aplicações do Windows Defender
<!-- 1351960 -->

Pode [criar e implementar políticas de proteção de aplicações do Windows Defender](/sccm/protect/deploy-use/create-deploy-application-guard-policy) utilizando o endpoint protection do Configuration Manager.

### <a name="device-guard-policy-changes"></a>Alterações de política de proteção de dispositivos
<!-- 1355092 -->
Foram efetuadas as seguintes alterações de três em relação a políticas de proteção de dispositivos:

- Políticas de proteção de dispositivos cujo nome foi mudadas para políticas de controlo de aplicação do Windows Defender. Sim, por exemplo, o **Assistente de política de criar Device Guard** tem agora o nome **Assistente de política de criar controlo de aplicação do Windows Defender**.
- Dispositivos com o Outono criadores atualização para Windows versão 1709 não necessitam de um reinício para aplicar as políticas de controlo de aplicação do Windows Defender. Reiniciar ainda é a predefinição, mas pode [desativar reinícios](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager).
- Pode [definir dispositivos a executar automaticamente software](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) considerado fidedigno pelo gráfico de segurança inteligente.





## <a name="next-steps"></a>Passos Seguintes
Quando estiver pronto para instalar esta versão, consulte [atualizações do Configuration Manager](/sccm/core/servers/manage/updates).

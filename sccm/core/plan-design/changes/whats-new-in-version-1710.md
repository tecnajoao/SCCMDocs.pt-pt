---
title: Nova versão 1710 | Documentos da Microsoft
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas funcionalidades introduzidas na versão 1710 do System Center Configuration Manager.
ms.date: 1/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4dcf5ce0c31f72db1e6af3ac9e024c83afe92337
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54250668"
---
# <a name="what39s-new-in-version-1710-of-system-center-configuration-manager"></a>O que&#39;s novo na versão 1710 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Atualização 1710 para o ramo atual do System Center Configuration Manager está disponível como uma atualização na consola para sites anteriormente instalados com a versão 1610, 1702 ou 1706.

Além das novas funcionalidades, esta versão também inclui alterações adicionais, como correções de erros. Para obter mais informações, consulte [resumo das alterações no ramo atual do System Center Configuration Manager, versão 1710](https://support.microsoft.com/help/4056470/summary-of-changes-in-system-center-configuration-manager-current-bran).

As seguintes atualizações adicionais para esta versão também estão agora disponíveis:
- [Update rollup para o ramo atual do System Center Configuration Manager, versão 1710](https://support.microsoft.com/help/4057517/update-rollup-for-system-center-configuration-manager-current-branch-v)
- [Update rollup 2 para o ramo atual do System Center Configuration Manager, versão 1710](https://support.microsoft.com/en-us/help/4086143/update-rollup-2-for-system-center-configuration-manager-current-branch)

> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de linha de base do Configuration Manager.  
>  Saiba mais sobre:    
>   - [Instalar novos sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Instalar atualizações em sites](/sccm/core/servers/manage/updates)  
>   - [Versões de linha de base e de atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As secções seguintes fornecem detalhes sobre alterações e novas funcionalidades introduzidas na versão 1710 do Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infraestrutura do site

### <a name="updates-for-peer-cache-----sms500850---"></a>Atualizações para a Cache ponto a ponto  <!-- sms500850 -->
A partir desta versão, Cache ponto a ponto já não é uma funcionalidade de pré-lançamento.  Nenhuma outra alteração para a Cache ponto a ponto é introduzidas com esta versão. Para obter mais informações, consulte [Cache ponto a ponto para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>Suporte de ponto de distribuição de cloud para a Cloud do Azure Government   <!-- sms491428 -->
Agora, pode utilizar [pontos de distribuição baseado na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) na cloud do Azure Government.   

### <a name="inventory-default-unit-revision----sms503697---"></a>Revisão de unidade de padrão de inventário <!-- sms503697 -->
Como os dispositivos agora incluem unidades de disco rígido com tamanhos nos gigabyte (GB), terabytes (TB) e escalas maiores, esta versão altera a unidade de predefinição (SMS_Units) utilizada nas vistas de muitos de megabytes (MB), a GB. Por exemplo, o valor de v_gs_LogicalDisk.FreeSpace relatórios agora unidades de GB.


<!-- ## Migration  -->


## <a name="client-management"></a>Gestão de clientes

### <a name="co-management-for-windows-10-devices"></a>Cogestão para os dispositivos com Windows 10    
<!-- 1350871 --> Nas atualizações anteriores do Windows 10, já pode participar num dispositivo Windows 10 para o local do Active Directory (AD) e com base na cloud do Azure AD ao mesmo tempo (Azure AD híbrido). A partir do Configuration Manager versão 1710, cogestão tira partido deste melhoramento e permite-lhe gerir em simultâneo com o Windows 10, versão 1709 (também conhecido como o Fall Creators Update) dispositivos com o Configuration Manager e o Intune. É uma solução que fornece uma ponte entre o tradicional para a gestão moderna e dá-lhe um caminho para fazer a transição de forma faseada. Para obter detalhes, consulte [cogestão para dispositivos Windows 10](/sccm/comanage/overview).

### <a name="restart-computers-from-the-configuration-manager-console-----1356283---"></a>Reinicie os computadores a partir da consola do Configuration Manager  <!-- 1356283 -->
Começando com esta versão, pode utilizar a consola do Configuration Manager para identificar os dispositivos de cliente que requerem um reinício e, em seguida, utilize uma ação de notificação de cliente para reiniciá-las.

Consulte [como gerir clientes no System Center Configuration Manager](/sccm/core/clients/manage/manage-clients#restart-clients)


<!-- ## Compliance settings -->


## <a name="application-management"></a>Gestão de Aplicações
### <a name="improvements-for-run-scripts------1236459---"></a>Melhorias para executar Scripts   <!-- 1236459 -->
Esta versão traz vários aprimoramentos para o **executar Scripts** recurso, que permite-lhe implementar scripts do PowerShell para executar em dispositivos geridos. Esse recurso foi introduzido pela primeira vez na versão 1706.

Melhoramentos incluem:
- Utilizar âmbitos de segurança para ajudar a controlar quem pode utilizar Scripts de execução
- Monitorização dos scripts em tempo real, executar
- Parâmetros para a exibição de script no Assistente de Script de criação, validação de suporte e são identificados como obrigatório ou opcional.

Para obter mais informações sobre como utilizar a executar Scripts, consulte [criar e executar scripts](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Novas definições de política de gestão de aplicações móveis
<!-- 1324760 --> Foram adicionadas as seguintes definições para as definições de política de gestão de aplicações móveis:
- **Desativar sincronização de contactos**: Impede que a aplicação de guardar os dados na aplicação nativa contactos no dispositivo.
- **Desativar a impressão**: Impede que a aplicação de trabalho de impressão dados escolares ou profissionais.

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Centro de software já não distorçam ícones maiores do que 250 x 250  
<!-- 1356194 -->

Com esta versão, o Centro de Software já não será distorcer os ícones que são maiores do que 250 x 250. Centro de software efetuada esses ícones parecer indistinta. Agora pode definir um ícone com um dimensões de pixel de até 512 x 512 e apresenta ao máximo sem distorção.

Para adicionar um ícone para a sua aplicação no Centro de Software, consulte [criem aplicativos](/sccm/apps/deploy-use/create-applications).

## <a name="operating-system-deployment"></a>Implementação do sistema operativo
 > [!TIP]   
 > <!-- 1354281 --> A partir do Windows 10, o lançamento da versão 1709 (também conhecido como o Fall Creators Update), o suporte de dados do Windows inclui várias edições. Ao configurar uma sequência de tarefas para utilizar um pacote de atualização do sistema operativo ou a imagem do sistema operativo, certifique-se de que selecione um [edition que é suportada para utilização pelo Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

### <a name="add-child-task-sequences-to-a-task-sequence"></a>Adicionar sequências de tarefas filho a uma sequência de tarefas
<!-- 1261338 -->

Pode adicionar um novo passo de sequência de tarefas que executa outra sequência de tarefas, que cria uma relação de pai/filho entre as sequências de tarefas. Isto permite-lhe criar mais sequências de tarefas modulares que pode utilizar novamente.  

Para saber mais sobre a sequência de tarefas filho, veja [sequência de tarefas de subordinado](/sccm/osd/understand/task-sequence-steps#child-task-sequence).

## <a name="software-center-customization"></a>Personalização do Centro de software
<!-- 1351224 --> Pode adicionar elementos de marca corporativa e especificar a visibilidade dos separadores no Centro de Software. Pode adicionar o seu nome de empresa específico do Centro de Software, defina um tema de cores de configuração do Centro de Software, defina um logótipo de empresa e definir as guias visíveis para os dispositivos de cliente.

Para obter mais informações, veja [Planear e configurar a gestão de aplicações no System Center Configuration Manager](/sccm/apps/plan-design/plan-for-and-configure-application-management).

## <a name="software-updates"></a>Atualizações de software

### <a name="surface-driver-updates-----1098490---"></a>Atualizações de controlador do Surface  <!-- 1098490 -->
A partir desta versão, gerenciamento de atualizações de controlador do Surface já não é uma funcionalidade de pré-lançamento.  


## <a name="reporting"></a>Relatórios

### <a name="limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Limitar telemetria avançada do Windows 10 para enviar apenas dados relevantes para o estado de funcionamento de dispositivos do Windows Analytics
<!-- 1356148 -->

Agora pode definir a recolha de dados de telemetria do Windows 10 para **avançado (limitado)**. Esta definição permite-lhe obter informações acionáveis sobre dispositivos no seu ambiente sem dispositivos que reportem todos os dados no **avançado** nível de telemetria com o Windows 10 versão 1709 ou posterior.

Para obter mais informações, consulte [como configurar as definições de cliente no System Center Configuration Manager](/sccm/core/clients/deploy/configure-client-settings).

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>Gestão de dispositivos móveis

### <a name="actions-for-non-compliance"></a>Ações de não conformidade 
<!--1321366 -->    
Agora, pode configurar uma sequência cronológica de ações que são aplicadas aos dispositivos que estão fora de conformidade. Por exemplo, pode notificar os utilizadores dos dispositivos não conformes por email ou marcar os dispositivos não conformes. Para obter detalhes, consulte [configurar as ações de não conformidade](/sccm/mdm/deploy-use/actions-for-noncompliance).

### <a name="windows-10-arm64-device-support"></a>Suporte para dispositivos Windows 10 ARM64
<!-- 1355000 -->

Cenários de gestão (MDM) de dispositivos móveis híbrida serão suportados em dispositivos de ARM64 com o Windows 10 quando estes dispositivos estão disponíveis.

Estes cenários incluem:

- [Inscrever dispositivos](../../../mdm/deploy-use/enroll-hybrid-windows.md)
- [Executar ações de eliminação seletiva e completa remota](../../../mdm/deploy-use/wipe-lock-reset-devices.md)
- [Gerir as definições através de itens de configuração e linhas de base](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Gerir política de conformidade](../../../mdm/deploy-use/device-compliance-policies.md) e [acesso condicional](../../../protect/deploy-use/manage-access-to-services.md)
- Gerir o acesso aos recursos da empresa através de:
   - [Perfis de certificados](../../../mdm/deploy-use/create-pfx-certificate-profiles.md)
   - [Perfis VPN](../../../mdm/deploy-use/create-vpn-profiles.md)
   - [Perfis de Wi-Fi](../../../mdm/deploy-use/create-wifi-profiles.md)
   - [Perfis de e-mail](../../../mdm/deploy-use/create-exchange-activesync-profiles.md)
- [Configurar o Windows Hello para política de negócio](../../../mdm/deploy-use/windows-hello-for-business-settings.md)
- [Gerir aplicações](../../../mdm/deploy-use/management-tasks-applications.md)

> [!NOTE]
> Implantação de aplicativos. appxbundle criados para várias arquiteturas poderá não funcionar nestes dispositivos, e este cenário não é suportado neste momento.

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Experiência de perfil VPN melhorado na consola do Configuration Manager 
<!-- 1318232 -->

Com esta versão, atualizamos as páginas de assistente e propriedades de perfil VPN para apresentar as definições adequadas da plataforma selecionada:


- Cada plataforma tem seu próprio fluxo de trabalho, que significa que os novos perfis VPN contêm apenas a definição suportada pela plataforma.
- O **plataformas suportadas** agora é apresentada a página após o **geral** página.  Agora, escolher a plataforma antes de definir os valores de propriedade.
- Quando a plataforma está definida como **Android**, **Android for Work**, ou **Windows Phone 8.1**, o **plataformas suportadas** página não é necessária e é Não é apresentada.
- O workflow baseada no cliente do Configuration Manager foi combinada com o híbrida dispositivos móveis (MDM) com base no cliente Windows 10 fluxos de trabalho; que suportam as mesmas definições.
- Cada fluxo de trabalho de plataforma inclui apenas as definições adequadas do fluxo de trabalho.  Por exemplo, o fluxo de trabalho Android contém definições adequadas para Android; definições adequadas para iOS ou Windows 10 Mobile já não aparecem no fluxo de trabalho Android.
- A página de VPN automática está obsoleta e foi removida.

Estas alterações aplicam-se para novos perfis VPN.  

Para minimizar o risco de compatibilidade, os perfis VPN existentes permanecem inalterados.  Ao editar um perfil existente, as definições são apresentadas quanto eram quando o perfil foi criado.  

Para obter mais informações, consulte [perfis de VPN em dispositivos móveis no System Center Configuration Manager](../../../mdm/deploy-use/create-vpn-profiles.md).

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>Suporte limitado de criptografia: Certificados de próxima geração (CNG) <!-- 1356191 -->

O Configuration Manager tem suporte limitado para criptografia: Próxima certificados de geração (CNG). Clientes do Configuration Manager podem utilizar o certificado de autenticação de cliente PKI com chave privada no fornecedor de armazenamento de chaves do CNG (KSP). Com o suporte KSP, clientes do Configuration Manager suportam a chave de privada baseada em hardware, como o KSP de TPM para certificados de autenticação de cliente PKI.

Para obter mais informações, consulte [descrição geral de certificados CNG](../network/cng-certificates-overview.md).

## <a name="protect-devices"></a>Proteger dispositivos

### <a name="create-and-deploy-exploit-guard-policies"></a>Criar e implementar políticas do Exploit Guard
<!-- 1355468 -->

Pode [criar e implementar políticas](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) que gerir todos os quatro componentes do Windows Defender Exploit Guard, incluindo a redução da superfície de ataque, acesso a pastas controladas, proteção de exploração e a proteção de rede.

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Criar e implementar a política do Windows Defender Application Guard
<!-- 1351960 -->

Pode [criar e implementar políticas do Windows Defender Application Guard](/sccm/protect/deploy-use/create-deploy-application-guard-policy) ao utilizar a proteção de ponto final do Configuration Manager.

### <a name="device-guard-policy-changes"></a>Alterações de política de proteção do dispositivo
<!-- 1355092 --> As seguintes três alterações foram feitas em relação a políticas de Device Guard:

- Políticas do Device Guard foram renomeadas para políticas de controlo de aplicações do Windows Defender. Assim, por exemplo, o **Assistente de política de criar o Device Guard** tem agora o nome **Assistente de política de criar controlo de aplicações do Windows Defender**.
- Dispositivos com o Fall Creators Update para Windows versão 1709 não exigem uma reinicialização para aplicar as políticas de controlo de aplicações do Windows Defender. Reiniciar ainda é o padrão, mas pode [desativar reinícios](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager).
- Pode [definir dispositivos ao software automaticamente, execute](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) considerado fidedigno pelo gráfico de segurança inteligente.





## <a name="next-steps"></a>Passos Seguintes
Quando estiver pronto para instalar esta versão, consulte [atualizações do Configuration Manager](/sccm/core/servers/manage/updates).

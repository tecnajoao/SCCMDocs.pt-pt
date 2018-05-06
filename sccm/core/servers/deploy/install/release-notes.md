---
title: Notas de versão
titleSuffix: Configuration Manager
description: Saiba mais sobre problemas urgentes que ainda não estão corrigidos no produto ou descritas na íntegra no artigo da Base de dados de Conhecimento Microsoft.
ms.date: 04/18/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4aeacdbc73e21c3bae18111e22c8407eba865a87
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Notas de versão do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o Configuration Manager, notas de versão do produto estão limitadas a problemas urgentes. Estes problemas ainda não estão corrigidos no produto ou detalhados num artigo da Base de dados de Conhecimento Microsoft.  

Documentação de específicos de funcionalidades inclui informações sobre problemas conhecidos que afetam os cenários principais.  

> [!TIP]  
>  Este tópico contém notas de versão para o ramo atual do Configuration Manager. Para obter informações sobre o ramo de pré-visualização técnica, consulte [pré-visualização técnica do System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

Para obter informações sobre as novas funcionalidades introduzidas com versões diferentes, consulte os artigos seguintes:
- [Novidades na versão 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)
- [Novidades na versão 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)
- [Novidades na versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  



## <a name="setup-and-upgrade"></a>Configuração e atualização  


### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>Ao utilizar os ficheiros redistribuíveis a partir do CD. Pasta mais recente, o programa de configuração falha com um erro de verificação manifesto
<!-- 510080, 490569  -->

Quando executar a configuração do CD. Pasta mais recente criado para a versão 1606 e utilizar os ficheiros redistribuíveis incluídos com antes esse CD. Pasta mais recente, o programa de configuração falha com os seguintes erros no registo de configuração do Configuration Manager:

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

#### <a name="workaround"></a>Solução
Utilize uma das seguintes opções:
 - Durante a configuração, optar por transferir os ficheiros redistribuíveis mais recentes da Microsoft. Utilize os ficheiros redistribuíveis mais recentes em vez de ficheiros incluídos no CD. Pasta mais recente.
 - Elimine manualmente o *cd.latest\redist\languagepack\zhh* pasta e, em seguida, execute novamente a configuração.


### <a name="setup-command-line-option-joinceip-must-be-specified"></a>Opção da linha de comandos que joinceip tem de ser especificado
<!--510806-->
*Aplica-se a: 1802 de versão do Configuration Manager*

A funcionalidade de programa de melhoramento da experiência de cliente (PMEC) a partir do Configuration Manager versão 1802, é removida do produto. Quando [automatizar a instalação](/sccm/core/servers/deploy/install/command-line-options-for-setup) de um novo site a partir de um script de linha de comandos ou automático, a configuração devolve um erro de que um parâmetro necessário em falta. 

#### <a name="workaround"></a>Solução
Enquanto não terá qualquer efeito no resultado do processo de configuração, incluem o **JoinCEIP** parâmetro na sua linha de comandos do programa de configuração.

 > [!Note]  
 > O parâmetro EnableSQM [a configuração da consola](/sccm/core/servers/deploy/install/install-consoles) não é necessária.



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Implementação e atualização do cliente

### <a name="azure-ad-enabled-clients-cant-communicate-with-management-point"></a>Os clientes preparados para AD do Azure não consegue comunicar com o ponto de gestão
<!--501089-->
*Aplica-se a: 1706 de versão do Configuration Manager*
<!--also fixed in 1710 HFRU-->
No cenário para [instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure), falha de comunicação de cliente quando o ponto de gestão ativado para HTTPS utiliza as credenciais da base de dados alternativa. 

#### <a name="workaround"></a>Solução
Mitigar este problema com uma das seguintes ações:
- Atualizar o site para a versão mais recente e aplique a correção mais recente
- Altere as credenciais que utiliza o ponto de gestão.


<!-- ## Operating system deployment  -->



## <a name="software-updates"></a>Atualizações de software

### <a name="servicing-plans-create-many-duplicate-software-update-groups-and-deployments-by-default"></a>Criar planos de manutenção muitas implementações e grupos de atualização de software duplicadas por predefinição  
<!-- 474326 -->
Por predefinição, o assistente Criar Plano de Manutenção é executado atualmente após cada sincronização de atualizações de software. Sempre que o assistente é executado, cria um novo grupo de atualização de software e implementação. Se tiver uma agenda de sincronização de atualizações de software que é executada várias vezes por dia, o Assistente Criar plano de manutenção cria vários grupos de atualização de software e implementações cada dia.  

#### <a name="workaround"></a>Solução
 Depois de criar um plano de manutenção, abra as propriedades do plano de manutenção, aceda ao separador **Agenda de Avaliação**, selecione **Executar a regra de forma programada**, clique em **Personalizar** e crie uma agenda personalizada. Por exemplo, pode fazer com que o plano de manutenção seja executado a cada 60 dias.  


### <a name="changing-office-365-client-setting-doesnt-apply"></a>A alteração do Office 365 definição de cliente não se aplica 
<!--511551-->
*Aplica-se a: 1802 de versão do Configuration Manager*  

Implementar um [definição de cliente](/sccm/core/clients/deploy/about-client-settings#enable-management-of-the-office-365-client-agent) com **ativar a gestão do agente de cliente do Office 365** configurado para `Yes`. Em seguida, altere essa definição para `No` ou `Not Configured`. Depois de atualizar a política em clientes de destino, as atualizações do Office 365 ainda são geridas pelo Configuration Manager. 

#### <a name="workaround"></a>Solução
Altere o valor de registo seguinte para `0` e reinicie o **serviço do Microsoft Office Clique para execução** (ClickToRunSvc):

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\office\16.0\Common\officeupdate]
"OfficeMgmtCOM"=dword:00000000
```



## <a name="mobile-device-management"></a>Gestão de dispositivos móveis  

### <a name="you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10"></a>Já não pode implementar perfis de VPN do Windows Phone 8.1 para o Windows 10
<!-- 503274  -->
*Aplica-se a: 1710 de versão do Configuration Manager*

Não é possível criar um perfil da VPN, utilizando o fluxo de trabalho do Windows Phone 8.1, que também é aplicável a dispositivos Windows 10. Estes perfis, o Assistente de criação já não apresenta a página de plataformas suportadas. Windows Phone 8.1 é selecionado automaticamente no back-end. A página de plataformas suportadas está disponível nas propriedades de perfil, mas não pode apresentar as opções do Windows 10.

#### <a name="workaround"></a>Solução
 Utilize o fluxo de trabalho do perfil de VPN do Windows 10 para dispositivos Windows 10. Se esta opção não é exequível para o seu ambiente, contacte o suporte. Suporte pode ajudar a adicionar o destino do Windows 10.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->

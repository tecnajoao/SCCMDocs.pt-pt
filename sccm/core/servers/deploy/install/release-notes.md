---
title: Notas de versão
titleSuffix: Configuration Manager
description: Saiba mais sobre problemas urgentes que ainda não estão corrigidos no produto ou abordados num artigo da base de dados de conhecimento Support da Microsoft.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bc19092f1272611ea3e05d708bf89bda1a4ba3b9
ms.sourcegitcommit: 0a23cde6112cbb5987f433bffcf6f223b994ba72
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/22/2019
ms.locfileid: "56667465"
---
# <a name="release-notes-for-configuration-manager"></a>Notas de versão para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o Configuration Manager, notas de versão do produto estão limitadas a problemas urgentes. Esses problemas ainda não estão corrigidos no produto ou detalhados num artigo da base de dados de Conhecimento Microsoft Support.  

Documentação de específicos de funcionalidades inclui informações sobre problemas conhecidos que afetam os cenários principais.  

> [!TIP]  
>  Este tópico contém notas de versão para o ramo atual do Configuration Manager. Para obter informações sobre o ramo de pré-visualização técnica, consulte [Technical Preview](/sccm/core/get-started/technical-preview)  

Para obter informações sobre os novos recursos introduzidos com versões diferentes, consulte os artigos seguintes:
- [O que há de novo na versão 1810](/sccm/core/plan-design/changes/whats-new-in-version-1810)
- [Novidades na versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)  
- [Novidades na versão 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)



## <a name="set-up-and-upgrade"></a>Configurar e atualizar  


### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>Ao utilizar os ficheiros redistribuíveis do CD. Pasta mais recente, a configuração falha com um erro de verificação de manifesto
<!-- 510080, 490569  -->

Quando executar a configuração, a partir do CD. Pasta mais recente criado para a versão 1606 e utilizar os ficheiros redistribuíveis incluídos com esse CD. Pasta mais recente, a instalação falha com os seguintes erros no registo de configuração do Configuration Manager:

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

#### <a name="workaround"></a>Solução
Utilize uma das seguintes opções:
 - Durante a configuração, optar por transferir os ficheiros redistribuíveis mais recentes da Microsoft. Utilize os ficheiros redistribuíveis mais recentes em vez dos arquivos incluídos no CD. Pasta mais recente.
 - Elimine manualmente os *cd.latest\redist\languagepack\zhh* pasta e, em seguida, execute novamente a configuração.


### <a name="setup-command-line-option-joinceip-must-be-specified"></a>Configurar a opção da linha de comandos, que tem de ser especificado JoinCEIP
<!--510806-->
*Aplica-se a: O Configuration Manager versão 1802*

A funcionalidade do programa de melhoramento da experiência de cliente (PMEC) a partir do Configuration Manager versão 1802, é removida do produto. Quando [automatização da instalação](/sccm/core/servers/deploy/install/command-line-options-for-setup) de um novo site de um script de linha de comando ou automático, a configuração devolve um erro que um parâmetro necessário está em falta. 

#### <a name="workaround"></a>Solução
Embora não tem efeito sobre o resultado do processo de configuração, inclui os **JoinCEIP** parâmetro na sua linha de comandos de configuração.

 > [!Note]  
 > O parâmetro Defaultsiteservername [configuração da consola](/sccm/core/servers/deploy/install/install-consoles) não é necessária.


### <a name="cloud-service-manager-component-stopped-on-site-server-in-passive-mode"></a>Componente do Gestor de serviço em nuvem parado no servidor de site em modo passivo
<!--VSO 2858826, SCCMDocs issue 772-->
*Aplica-se a: 1806 de versão do Configuration Manager*

Se o [ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) é foi colocalizado com a um [servidor do site em modo passivo](/sccm/core/servers/deploy/configure/site-server-high-availability), em seguida, implementação e monitorização de um [gateway de gestão na cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) não começa. O componente do Gestor de serviço cloud (SMS_CLOUD_SERVICES_MANAGER) está no estado parado.

#### <a name="workaround"></a>Solução
Mova a função de ponto de ligação de serviço para outro servidor.



<!-- ## Backup and recovery  -->


<!--## Client deployment and upgrade-->



## <a name="os-deployment"></a>Implementação de SO

### <a name="after-passive-site-server-is-promoted-the-default-boot-image-packages-still-have-package-source-on-the-previous-active-server"></a>Depois do servidor do site passivo é promovido, os pacotes de imagem de arranque predefinido ainda tem origem do pacote no servidor do Active Directory anterior
<!--3453224, SCCMDocs-pr issue 3097-->
*Aplica-se a: 1810 de versão do Configuration Manager*

Se tiver um servidor de site em modo passivo (servidor B), quando promover para ativo, a localização de conteúdo para imagens de arranque predefinidas continua a fazer referência servidor anteriormente ativo (servidor A). Se o servidor A tem uma falha de hardware, não é possível atualizar ou alterar imagens de arranque predefinidas.

#### <a name="workaround"></a>Solução
Nenhum



## <a name="software-updates"></a>Atualizações de software

### <a name="security-roles-are-missing-for-phased-deployments"></a>Funções de segurança estão em falta para as implementações faseadas
<!--3479337, SCCMDocs-pr issue 3095-->
*Aplica-se a: 1810 de versão do Configuration Manager*

O **Gestor de implementação do SO** função de segurança incorporada tem permissões para [faseada implementações](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence). As seguintes funções estão em falta estas permissões:  

- **Administrador da aplicação**  
- **Gestor de implementação de aplicações**  
- **Gestor de atualizações de software**  

O **autor da aplicação** função poderá apresentar um tem algumas permissões para as implementações faseadas, mas não deve ser capaz de criar implementações. 

As implementações para uma aplicação ou atualização de software por fases de um utilizador com uma dessas funções podem iniciar o assistente criar implementação faseada e podem ver. Não é possível concluir o assistente ou fazer alterações a uma implementação existente.

#### <a name="workaround"></a>Solução
Crie uma função de segurança personalizada. Copiar uma função de segurança existente e adicione as seguintes permissões no **implementação faseada** classe do objeto:
- Criar  
- Eliminar  
- Modificar  
- Leitura  

Para obter mais informações, consulte [criar funções de segurança personalizadas](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole)


### <a name="changing-office-365-client-setting-doesnt-apply"></a>A alteração do Office 365 definição de cliente não se aplica 
<!--511551-->
*Aplica-se a: O Configuration Manager versão 1802*  

Implementar um [definição de cliente](/sccm/core/clients/deploy/about-client-settings#enable-management-of-the-office-365-client-agent) com **ativar a gestão do agente de cliente do Office 365** configurado para `Yes`. Em seguida, alterar essa definição seja `No` ou `Not Configured`. Depois de atualizar a política nos clientes de destinados, as atualizações do Office 365 ainda são geridas pelo Configuration Manager. 

#### <a name="workaround"></a>Solução
Altere o valor de registo seguinte para `0` e reinicie o **serviço do Microsoft Office Clique-e-use** (ClickToRunSvc):

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\office\16.0\Common\officeupdate]
"OfficeMgmtCOM"=dword:00000000
```



## <a name="mobile-device-management"></a>Gestão de dispositivos móveis  

### <a name="you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10"></a>Já não pode implementar perfis de VPN do Windows Phone 8.1 para o Windows 10
<!-- 503274  -->
*Aplica-se a: O Configuration Manager versão 1710*

Não é possível criar um perfil da VPN com o fluxo de trabalho do Windows Phone 8.1, o que também é aplicável a dispositivos Windows 10. Para estes perfis, o Assistente de criação já não mostra a página de plataformas suportadas. Windows Phone 8.1 é selecionado automaticamente no back-end. A página de plataformas suportadas está disponível nas propriedades de perfil, mas não exibe as opções do Windows 10.

#### <a name="workaround"></a>Solução
 Utilize o fluxo de trabalho do perfil de VPN do Windows 10 para dispositivos Windows 10. Se esta opção não é viável para o seu ambiente, contacte o suporte. O suporte pode ajudá-lo a adicionar o direcionamento do Windows 10.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->

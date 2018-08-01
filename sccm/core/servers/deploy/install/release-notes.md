---
title: Notas de versão
titleSuffix: Configuration Manager
description: Saiba mais sobre problemas urgentes que ainda não estão corrigidos no produto ou abordados no artigo da Base de dados de Conhecimento Microsoft.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9daf0fb53face0cf7ed56f2a45ab044fbfac203c
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385512"
---
# <a name="release-notes-for-configuration-manager"></a>Notas de versão para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o Configuration Manager, notas de versão do produto estão limitadas a problemas urgentes. Esses problemas ainda não estão corrigidos no produto ou detalhados num artigo da Base de dados de Conhecimento Microsoft.  

Documentação de específicos de funcionalidades inclui informações sobre problemas conhecidos que afetam os cenários principais.  

> [!TIP]  
>  Este tópico contém notas de versão para o ramo atual do Configuration Manager. Para obter informações sobre o ramo de pré-visualização técnica, consulte [Technical Preview](../../../../core/get-started/technical-preview.md)  

Para obter informações sobre os novos recursos introduzidos com versões diferentes, consulte os artigos seguintes:
- [O que há de novo na versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)  
- [Novidades na versão 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)
- [Novidades na versão 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)



## <a name="setup-and-upgrade"></a>Configuração e atualização  


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
Embora não terá qualquer efeito sobre o resultado do processo de configuração, inclui os **JoinCEIP** parâmetro na sua linha de comandos de configuração.

 > [!Note]  
 > O parâmetro Defaultsiteservername [configuração da consola](/sccm/core/servers/deploy/install/install-consoles) não é necessária.



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Implementação e atualização do cliente

### <a name="azure-ad-enabled-clients-cant-communicate-with-management-point"></a>Os clientes habilitados para AD do Azure não consegue comunicar com o ponto de gestão
<!--501089-->
*Aplica-se a: O Configuration Manager versão 1706* 
 <!--also fixed in 1710 HFRU--> cenário para [instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure), falha de comunicação de cliente Quando o ponto de gestão ativado para HTTPS utiliza credenciais de base de dados alternativa. 

#### <a name="workaround"></a>Solução
Atenuar este problema com uma das seguintes ações:
- Atualizar o site para a versão mais recente e aplique a correção mais recente
- Altere as credenciais que utiliza o ponto de gestão.


<!-- ## Operating system deployment  -->



## <a name="software-updates"></a>Atualizações de software

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

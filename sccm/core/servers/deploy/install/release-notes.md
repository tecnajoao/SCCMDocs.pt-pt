---
title: "Notas de versão "
titleSuffix: Configuration Manager
description: "Para problemas urgentes que ainda não estão corrigidos no produto ou descritas na íntegra no artigo da Base de dados de conhecimento da Microsoft, consulte estas notas."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53685ef2647cfd87c2fcb603097186360f1c96a5
ms.sourcegitcommit: fbd4a9d2fa8ed4ddd3a0fecc4a2ec4fc0ccc3d0c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/19/2018
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Notas de versão do System Center Configuration Manager

Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o Configuration Manager, notas de versão do produto estão limitadas a problemas urgentes. Estes problemas ainda não estão corrigidos no produto ou detalhados num artigo da Base de dados de Conhecimento Microsoft.  

Documentação de específicos de funcionalidades inclui informações sobre problemas conhecidos que afetam os cenários principais.  

> [!TIP]  
>  Este tópico contém notas de versão para o ramo atual do Configuration Manager. Para obter informações sobre o ramo de pré-visualização técnica, consulte [pré-visualização técnica do System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

Para obter informações sobre as novas funcionalidades introduzidas com versões diferentes, consulte os artigos seguintes:
- [Novidades na versão 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)
- [Novidades na versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [Novidades na versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)



## <a name="setup-and-upgrade"></a>Configuração e atualização  


### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Ao instalar um site de sucursal de serviço de longo prazo utilizando a versão 1606, é instalado um site do ramo atual
<!-- Consider move to core content  -->
Quando utiliza a versão 1606 da linha de base suportes de dados a versão de Outubro de 2016 para instalar um site de longo prazo Servicing Branch (LTSB), o programa de configuração instala um site de Current Branch em vez disso. Este comportamento ocorre porque a opção para instalar um ponto de ligação de serviço com a instalação do site não está selecionada.

 - Embora um ponto de ligação de serviço não seja necessário, tem de estar selecionada para instalar durante a configuração para instalar um site LTSB.

Após a conclusão da configuração, pode desinstalar o ponto de ligação de serviço. No entanto, tem de ter uma ponto no modo offline ou online para submeter dados de telemetria e ao obter as atualizações de segurança para o ramo atual e LTSB sites de ligação de serviço.

Se o site instalado como um site do ramo atual, mas quer instalar o LTSB, pode desinstalar o site e, em seguida, reinstalá-la. Em alternativa, pode chamar [e suporte da Microsoft Help](http://go.microsoft.com/fwlink/?LinkId=243064) para obter assistência.  

Para confirmar que ramo instalado, na consola em **administração** > **configuração do Site** > **Sites**e abra **definições de hierarquia**. A opção para converter o site para um site de Current Branch só está disponível quando o site é executada a LTSB.  

**Solução:** Nenhuma.   


### <a name="an-update-persists-in-downloading-state-in-the-updates-and-servicing-node-of-the-console"></a>Uma atualização persistir no Estado em que as atualizações a transferir e a servir o nó da consola do  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
Durante a transferência automática de atualizações por um ponto de ligação de serviço online, uma atualização pode ficar bloqueada, com o estado a transferir. Quando a transferência de uma atualização fica bloqueada, aparecem entradas semelhantes à seguinte nos ficheiros de registo indicados:  

Registo de DMPdownloader:  
`ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"`  

ConfigMgrSetup.log:  
`Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.`  
`Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi`  

**Solução**: No servidor do site, modifique a seguinte chave de registo para fazer corresponder o seguinte valor:  

-   **Chave a editar**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Valor de estado**: Definido como **146944** Decimal ou **0x00023e00** Hexadecimal  

Em seguida, reinicie o serviço SMS_Executive ou aguarde até 24 horas para o próximo ciclo de transferência automática.

### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>Ao utilizar os ficheiros redistribuíveis a partir do CD. Pasta mais recente, o programa de configuração falha com um erro de verificação manifesto
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

Quando executar a configuração do CD. Pasta mais recente criado para a versão 1606 e utilizar os ficheiros redistribuíveis incluídos com antes esse CD. Pasta mais recente, o programa de configuração falha com os seguintes erros no registo de configuração do Configuration Manager:

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

**Solução:** Utilize uma das seguintes opções:
 - Durante a configuração, optar por transferir os ficheiros redistribuíveis mais recentes da Microsoft. Utilize os ficheiros redistribuíveis mais recentes em vez de ficheiros incluídos no CD. Pasta mais recente.
 - Elimine manualmente o *cd.latest\redist\languagepack\zhh* pasta e, em seguida, execute novamente a configuração.



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Implementação e atualização do cliente  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>Falha de instalação de cliente com o código de erro 0x8007064c
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*O seguinte problema aplica-se a todas as versões de Active Directory do Configuration Manager.*  

Quando implementar o cliente em computadores Windows, a instalação falha. O ficheiro ccmsetup.log contém as seguintes entradas: 

`File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation`  
`InstallFromManifest failed 0x8007064c`

**Solução**: Uma versão de danificada e instalada anteriormente do Silverlight faz com que este problema. Para corrigir este problema, execute a ferramenta seguinte no computador afetado: [Corrigir problemas que bloquear a programas de ser instalado ou removido](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed).

## <a name="operating-system-deployment"></a>Implementação do sistema operativo  

### <a name="servicing-plans-create-many-duplicate-software-update-groups-and-deployments-by-default"></a>Criar planos de manutenção muitas implementações e grupos de atualização de software duplicadas por predefinição  
Por predefinição, o assistente Criar Plano de Manutenção é executado atualmente após cada sincronização de atualizações de software. Sempre que o assistente é executado, cria um novo grupo de atualização de software e implementação. Se tiver uma agenda de sincronização de atualizações de software que é executada várias vezes por dia, o Assistente Criar plano de manutenção cria vários grupos de atualização de software e implementações cada dia.  

**Solução**: Depois de criar um plano de manutenção, abra as propriedades do plano de manutenção, aceda ao separador **Agenda de Avaliação**, selecione **Executar a regra de forma programada**, clique em **Personalizar** e crie uma agenda personalizada. Por exemplo, pode fazer com que o plano de manutenção seja executado a cada 60 dias.  



## <a name="software-updates"></a>Atualizações de software

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>Importar as definições de um cliente do Office 365 a partir de um ficheiro de configuração falha quando contém idiomas não suportados
<!-- 489258  Fixed in 1706  -->
*O seguinte problema aplica-se a versão 1702 e anterior.*   

Quando importar as definições de cliente do Office 365 a partir de um ficheiro de configuração XML existente e o ficheiro contém idiomas que não são suportados pelo cliente do Office 365 ProPlus, ocorre um erro. Para obter mais informações, consulte: [Implementar aplicações do Office 365 para clientes a partir do dashboard de gestão de clientes do Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Solução**: Utilizar apenas o [idiomas suportados pelo cliente do Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) no ficheiro de configuração XML.  



## <a name="mobile-device-management"></a>Gestão de dispositivos móveis  

### <a name="beginning-with-version-1710-you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10------503274--should-be-fixed-by-1802-if-not-sooner---"></a>A partir da versão 1710, já não pode implementar perfis de VPN do Windows Phone 8.1 para o Windows 10   <!-- 503274  Should be fixed by 1802, if not sooner -->
1710, já não é possível criar um perfil da VPN com o fluxo de trabalho do Windows Phone 8.1 que também é aplicável a dispositivos Windows 10. Estes perfis, a página de plataformas suportadas já não é apresentada no Assistente de criação. Windows Phone 8.1 é selecionado automaticamente no back-end. A página de plataformas suportadas está disponível nas propriedades de perfil, mas a consola não apresenta as opções do Windows 10.

**Solução**: Utilize o fluxo de trabalho do perfil de VPN do Windows 10 para dispositivos Windows 10. Se esta opção não é exequível para o seu ambiente, contacte o suporte. Suporte pode ajudar a adicionar o destino do Windows 10.


### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-of-memory"></a>Eliminação completa desativa a dispositivos Windows 10 com menos de 4 GB de memória
A eliminação completa nos dispositivos com o Windows 10, versão 1507, com menos de 4 GB de RAM pode deixar o dispositivo não utilizável. Após a tentar apagar o dispositivo, não é possível iniciar e não responde.

**Solução**: Certifique-se de que os dispositivos Windows 10 têm, pelo menos, 4 GB de memória disponível antes de efetuar uma eliminação completa. Para ver o número de versão de dispositivos Windows 10, introduza "winver" numa linha de comandos. Se já tiver eliminado o dispositivo e já não está a responder, utilize uma unidade de arranque USB do Windows 10 para recuperar o dispositivo.


### <a name="when-a-user-belongs-to-two-or-more-user-collections-to-which-you-deploy-a-terms-and-conditions-policy-the-user-sees-multiple-sets-of-the-same-terms"></a>Quando um utilizador pertence a duas ou mais coleções de utilizadores nos quais implementou uma política de termos e condições, o utilizador verá vários conjuntos dos mesmos termos  
<!-- 454394    -->
Se implementar um conjunto de termos em várias coleções de utilizador e um utilizador é membro de mais do que uma destas coleções, esse utilizador verá várias cópias de termos idênticos no Portal da empresa. Por exemplo:
- Um utilizador com o nome "SampleUser" for um membro de duas coleções de utilizador diferente, "CompanyEmployeesFTE" e "CompanyEmployeesNA"
- Implementar os "CompanyTerms" termos e condições em CompanyEmployeesFTE e em CompanyEmployeesNA
- SampleUser verá dois conjuntos idênticos de CompanyTerms na página de aceitação de termos de licenciamento no Portal da empresa. 

Os utilizadores só podem aceitar todas ou rejeitar todas as condições. Deste modo, não há nenhum perigo de estado de aceitação ambígua. (Esse Estado ambíguo é onde o utilizador aceita e rejeita os termos de licenciamento mesmos). O relatório de aceitação dos termos e condições inclui apenas uma linha para cada conjunto de termos de licenciamento por utilizador, pelo que não existe nenhum erro no relatório. O único efeito é que o utilizador verá dois conjuntos de termos na página de aceitação.  

**Solução**: Certifique-se de que cada utilizador está incluído apenas uma coleção à qual os termos são implementados.  


<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->

---
title: "Notas de versão "
titleSuffix: Configuration Manager
description: "Para problemas urgentes que ainda não estão corrigidos no produto ou descritas na íntegra no artigo da Base de dados de conhecimento da Microsoft, consulte estas notas."
ms.custom: na
ms.date: 11/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: "41"
caps.handback.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 8030ce7f98ebb34d9581ad036513b9b1c879c0ad
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Notas de versão do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o System Center Configuration Manager, notas de versão do produto estão limitadas a problemas urgentes que são ainda não corrigidos no produto (disponível através de uma atualização na consola) ou detalhados num artigo da Base de dados de Conhecimento Microsoft.  

Informações sobre problemas conhecidos que afetam os cenários principais são transmitidas na documentação do produto online, na biblioteca de documentação do System Center Configuration Manager.  

> [!TIP]  
>  Este tópico contém notas de versão para o ramo atual do System Center Configuration Manager. Para a pré-visualização técnica do System Center Configuration Manager, consulte [pré-visualização técnica do System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

Para obter informações sobre as novas funcionalidades introduzidas com versões diferentes, consulte o seguinte:
- [Novidades na versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [Novidades na versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)
- [Novidades na versão 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)



## <a name="setup-and-upgrade"></a>Configuração e atualização  


### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Ao instalar um site de sucursal de serviço de longo prazo utilizando a versão 1606, é instalado um site do ramo atual
<!-- Consider move to core content  -->
Quando utiliza a versão 1606 da linha de base suportes de dados a versão de Outubro de 2016 para instalar um site de longo prazo Servicing Branch (LTSB), o programa de configuração instala um site de Current Branch em vez disso. Isto ocorre porque a opção para instalar um ponto de ligação de serviço com a instalação do site não está selecionada.

 - Embora um ponto de ligação de serviço não seja necessário, tem de estar selecionada para instalar durante a configuração para instalar um site LTSB.

Depois de concluída a configuração pode desinstalar o ponto de ligação de serviço.  No entanto, tem de ter uma ponto no modo offline ou online para submeter dados de telemetria e ao obter as atualizações de segurança para o ramo atual e LTSB sites de ligação de serviço.

Se o site instalado como um site do ramo atual, mas quer instalar o LTSB, pode desinstalar o site e, em seguida, reinstalá-la. Em alternativa, pode chamar [e suporte da Microsoft Help](http://go.microsoft.com/fwlink/?LinkId=243064) para obter assistência.  

Para confirmar que ramo instalado, na consola em **administração** > **configuração do Site** > **Sites**e abra **definições de hierarquia**. A opção para converter o site para um site de Current Branch só está disponível quando o site é executada a LTSB.  

**Solução:**  Nenhuma.   


### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>Uma atualização está bloqueada com o estado A transferir no nó Atualizações e Manutenção da consola do Configuration Manager  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
Durante a transferência automática de atualizações por um ponto de ligação de serviço online, uma atualização pode ficar bloqueada, com o estado A transferir. Quando a transferência de uma atualização fica bloqueada, aparecem entradas semelhantes à seguinte nos ficheiros de registo indicados:  

Registo de DMPdownloader:  

-   ERRO: Falha ao transferir redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 com o comando /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /redisturl http://go.microsoft.com/fwlink/?LinkID=724434 /redistversion 112015 /NoUI "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log:  

-   Erro: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.  

-   Erro: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**Solução**: No servidor do site, modifique a seguinte chave de registo para fazer corresponder o seguinte e, em seguida, reinicie o serviço SMS_Executive ou aguarde até 24 horas para o próximo ciclo de transferência automática.  

-   **Chave a editar**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software publicação  

-   **Valor de estado**:  Definido como **146944** Decimal ou **0x00023e00** Hexadecimal  


###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>A configuração falha quando utilizar ficheiros de redistribuição a partir do CD. Pasta mais recente com um erro de verificação manifesto
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

Quando executar a configuração a partir de um CD. Pasta mais recente criada para a versão 1606 e utilizar ficheiros de redist incluídos com antes esse CD. Pasta mais recente, o programa de configuração falha com os seguintes erros no registo de configuração do Configuration Manager:

  - ERRO: Falha na verificação de hash de ficheiro para defaultcategories.dll
  - ERRO: Falha na verificação de manifesto. Versão correta do manifesto de?

**Solução:**  Utilize um dos seguintes:
 - Durante a configuração optar por transferir os ficheiros de redist mais recentes da Microsoft para utilizar em vez das incluída no CD. Pasta mais recente.
 - Elimine manualmente o *cd.latest\redist\languagepack\zhh* pasta e, em seguida, execute novamente a configuração.



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Implementação e atualização do cliente  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>Falha de instalação de cliente com o código de erro 0x8007064c
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*O seguinte aplica-se a todas as versões de Active Directory do Configuration Manager.*   
Com todas as ativas versões do quando implementar o cliente em computadores Windows, a instalação falha. O ficheiro ccmsetup.log contém uma entrada "o ficheiro 'C:\WINDOWS\ccmsetup\Silverlight.exe' devolveu o código de saída 1612. Falha de instalação"seguido de"InstallFromManifest falhou 0x8007064c".

**Solução** isto é causado por uma versão de danificada e instalada anteriormente do Silverlight. Pode tentar executar a ferramenta seguinte no computador afetado para corrigir esta situação: [https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)

## <a name="operating-system-deployment"></a>Implementação do sistema operativo  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>Por predefinição, os planos de manutenção criam muitas implementações e grupos de atualização de software duplicados  
Por predefinição, o assistente Criar Plano de Manutenção é executado atualmente após cada sincronização de atualizações de software. Sempre que o assistente é executado, cria um novo grupo de atualização de software e implementação. Se tiver uma agenda de sincronização de atualizações de software que é executada várias vezes por dia, por exemplo, o assistente Criar Plano de Manutenção irá criar vários, e provavelmente idênticos, grupos de atualização de software e implementações cada dia.  

**Solução**:    
Depois de criar um plano de manutenção, abra as propriedades do plano de manutenção, aceda ao separador **Agenda de Avaliação**, selecione **Executar a regra de forma programada**, clique em **Personalizar** e crie uma agenda personalizada. Por exemplo, pode fazer com que o plano de manutenção seja executado a cada 60 dias.  



## <a name="software-updates"></a>Atualizações de software

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>Importar as definições de um cliente do Office 365 a partir de um ficheiro de configuração falha quando contém idiomas não suportados
<!-- 489258  Fixed in 1706  -->
*O seguinte aplica-se versão 1702 e anterior.*   
Quando importar as definições de cliente do Office 365 a partir de um ficheiro de configuração XML existente e o ficheiro contém idiomas que não são suportados pelo cliente do Office 365 ProPlus, ocorrerá um erro. Para obter mais informações, consulte [implementar aplicações do Office 365 para clientes a partir do dashboard de gestão de clientes do Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Solução**:    
Utilizar apenas o [idiomas suportados pelo cliente do Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) no ficheiro de configuração XML.  



## <a name="mobile-device-management"></a>Gestão de dispositivos móveis  

### <a name="beginning-with-version-1710-you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10------503274--should-be-fixed-by-1802-if-not-sooner---"></a>A partir da versão 1710, já não pode implementar perfis de VPN do Windows Phone 8.1 para o Windows 10<!-- 503274  Should be fixed by 1802, if not sooner -->
1710, já não é possível criar um perfil da VPN com o fluxo de trabalho do Windows Phone 8.1 que também é aplicável a dispositivos Windows 10. Para estes perfis, a página de plataformas suportadas já não é apresentada no Assistente de criação e Windows Phone 8.1 é selecionado automaticamente no back-end; as páginas de propriedades, a página de plataformas suportadas estiver disponível, mas não são apresentadas as opções do Windows 10.

**Solução**: Utilize o fluxo de trabalho do perfil de VPN do Windows 10 para dispositivos Windows 10. Se isto não é exequível para o seu ambiente, contacte o suporte. Suporte pode ajudar a adicionar o destino do Windows 10, se necessário.


### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>A eliminação completa de dados desativa os dispositivos Windows 10 com menos de 4 GB de RAM
Fazer a eliminação completa de dados em dispositivos Windows 10 RTM (versões anteriores à versão 1511) com menos de 4 GB de RAM pode deixar o dispositivo não utilizável. Depois de tentar fazer a eliminação de dados do dispositivo, o dispositivo não liga e não responde.

**Solução**: Certifique-se de que o Windows 10 RTM PCs ter, pelo menos, 4 GB de RAM disponível antes de efetuar uma eliminação completa no dispositivo. Para ver o número de versão de dispositivos Windows 10, introduza "winver" numa linha de comandos. Se o dispositivo já tiver sido apagado e já não estiver a responder, utilize uma pen USB do Windows 10 de arranque para iniciar e recuperar o acesso ao dispositivo.


### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>Quando um utilizador pertence a duas ou mais coleções de utilizadores nos quais esteja implementada uma política de termos e condições, o utilizador verá vários conjuntos dos mesmos termos  
<!-- 454394    -->
Quando um administrador implementa um conjunto de termos em várias coleções de utilizadores e um utilizador é membro de mais de uma destas coleções, serão apresentadas a esse utilizador várias cópias de termos idênticos quando abrir o Portal da Empresa.  Por exemplo, se um utilizador com o nome "SampleUser" for um membro de duas coleções de utilizadores diferentes, uma denominada "CompanyEmployeesFTE" e "CompanyEmployeesNA", "e os termos e condições denominadas"CompanyTerms"é implementados em CompanyEmployeesFTE e em CompanyEmployeesNA, SampleUser irá ver dois conjuntos idênticos de CompanyTerms na página de aceitação de termos de licenciamento. Uma vez que os utilizadores só podem aceitar ou recusar todos os termos, não existe perigo de cair num estado de aceitação ambígua (em que o utilizador aceitou e rejeitou os termos). O relatório de aceitação dos Termos e Condições incluirá apenas uma linha para cada conjunto de termos para cada utilizador, pelo que não existe nenhum erro no relatório. O único efeito é que o utilizador verá dois conjuntos de termos na página de aceitação.  

**Solução**: Certifique-se de que cada utilizador está incluído apenas uma coleção à qual os termos são implementados.  


### <a name="android-for-work-email-profiles-that-use-certificate-authentication-are-not-applied-to-devices"></a>Android para perfis de e-mail de trabalho que utilizam a autenticação de certificado não são aplicadas aos dispositivos
<!--  487657      -->
Quando é criado um Android para o perfil de e-mail de trabalho, existem duas opções para a autenticação. Um é o nome de utilizador e palavra-passe, não sendo outros certificados. Neste momento, a opção de certificados não está a funcionar. Se o perfil ser criado com o método de autenticação definido como **certificados**, o perfil não é aplicado ao dispositivo e o utilizador será avisado para introduzir manualmente os detalhes da conta de e-mail.

**SOLUÇÃO**: Nenhuma. Administradores tem de utilizar o **nome de utilizador e palavra-passe** opção ou aguarde até que este problema foi resolvido.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->

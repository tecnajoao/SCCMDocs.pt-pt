---
title: "Notas de versão - Configuration Manager | Documentos do Microsoft"
description: "Consulte estas notas para com questões urgentes que ainda não fixo no produto ou abrangido num artigo da Base de dados de Conhecimento Microsoft."
ms.custom: na
ms.date: 05/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 41
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: d5166b16ffbe46af561b1ce98c0494cc4aaa72a8
ms.openlocfilehash: 9da6f9678a7fb5c76f365a3522f5e5e0fdfec037
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="release-notes-for-system-center-configuration-manager"></a>Notas de versão do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o System Center Configuration Manager, notas de versão do produto são limitadas com questões urgentes que ainda não fixo no produto (disponível através de uma atualização na consola) ou detalhadas num artigo da Base de dados de Conhecimento Microsoft.  

 Para problemas conhecidos que afetam os cenários principais, estas informações são transmitidas na documentação do produto online, na biblioteca de documentação do System Center Configuration Manager.  

> [!TIP]  
>  Este tópico contém notas de versão para o ramo atual do System Center Configuration Manager. Para a pré-visualização técnica do System Center Configuration Manager, consulte o artigo [pré-visualização técnica do System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

## <a name="setup-and-upgrade"></a>Configuração e atualização  

### <a name="after-you-update-a-configuration-manager-console-using-consolesetupexe-from-the-site-server-folder-recent-language-pack-changes-are-not-available"></a>Depois de atualizar uma consola do Configuration Manager utilizando ConsoleSetup.exe da pasta de servidor do site, recentes alterações ao pacote de idiomas não estão disponíveis
<!--  SMS 486420  Applicability should be 1610 and 1702.  -->
Depois de executar uma atualização no local para uma consola utilizando ConsoleSetup.exe a partir de uma pasta de instalação de servidores de site, o primeiro instalado recentemente pacotes poderão não ser availble. Isto ocorre quando:
- O site executa uma versão 1610 ou 1702.
- A consola é atualizada no local utilizando ConsoleSetup.exe da pasta de instalação do servidor de site.

Quando este problema ocorre, a consola reinstalada não utilizará o mais recente conjunto de pacotes de idiomas que foram configuradas. Não existem erros são devolvidos, mas não será foram alterados avaialble de pacotes de idiomas para a consola.  

**Solução:** Desinstalar a consola atual e, em seguida, reinstale a consola como uma nova instalação. Pode utilizar ConsoleSetup.exe da pasta de instalação de servidores de site. Durante a instalação, certifique-se de que seleciona os ficheiros de pacote de idioma que pretende utilizar.


### <a name="with-version-1702-the-default-site-boundary-group-is-configured-for-use-for-site-assignment"></a>Com a versão 1702, o grupo de limites de site predefinida está configurado para utilização para atribuição de sites
<!--  SMS 486380   Applicability should only be to 1702. -->
Com a versão 1702, o separador de referência de grupos de limites de site de predefinido tem uma verificação de **utilizar este grupo de limites para atribuição de site**, apresenta o site como o **site atribuído**e está a cinzento, para que a configuração não pode ser editada ou removida.

**Solução:** Nenhuma. Pode ignorar esta definição. Embora o grupo está ativado para atribuição de site, o grupo de limites de site predefinidos não é utilizado para atribuição de sites. Com 1702, esta configuração garante que o grupo de limites de site predefinido é associado ao site correto.



### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Ao instalar um site de ramo de serviço de longo prazo com a versão 1606, um site secundário atual está instalado
<!-- Consider move to core content  -->
Quando utiliza o suporte de dados da linha de base de 1606 versão de uma versão Outubro de 2016 para instalar um site secundário de manutenção de longo prazo (LTSB), o programa de configuração instala um site secundário atual em vez disso. Isto ocorre porque a opção para instalar um ponto de ligação de serviço com a instalação do site não estiver selecionada.

 - Embora um ponto de ligação de serviço não seja necessário, tem de ser selecionada para instalar durante a configuração para instalar um site LTSB.

Depois de concluída a configuração pode desinstalar o ponto de ligação de serviço.  No entanto, tem de ter um ponto no modo offline ou online para submeter dados de telemetria e obter atualizações de segurança para o ramo atual e sites LTSB de ligação de serviço.

Se o site instalado como um site secundário atual, mas pretendia instalar o LTSB, pode desinstalar o site e, em seguida, reinstalá-lo. Em alternativa, pode ligar [e suporte da Microsoft Help](http://go.microsoft.com/fwlink/?LinkId=243064) para obter assistência.  

Para confirmar que ramo instalado, a consola **administração** > **configuração do Site** > **Sites**, no computador e abra **definições de hierarquia**. A opção para converter o site para um site secundário atual só está disponível quando o site executa o LTSB.  

**Solução:**  Nenhuma.   



### <a name="the--sql-server-backup-model-in-use-by-configuration-manager-can-change-from-full-to-simple"></a>O modelo de cópia de segurança do SQL Server utilizado pelo Configuration Manager pode ser alterado de completa para simples  
<!-- Confirm applicability for upgrade to later baselines. 1511 is out of support. 1606 is minmum supported baseline  -->

 Ao atualizar para o System Center Configuration Manager versão 1511, o modelo de cópia de segurança do SQL Server utilizado pelo Configuration Manager pode ser alterado de completa para simples.  

-   Se utilizar uma tarefa de cópia de segurança personalizada do SQL Server com o modelo de cópia de segurança completa (em vez da tarefa de cópia de segurança incorporada para o Configuration Manager), a atualização pode alterar o seu modelo de cópia de segurança de completa para simples.  

**Solução**: Após a atualização para a versão 1511, reveja a configuração do SQL Server e restaurá-la para completas se for necessário.  



### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>Uma atualização está bloqueada com o estado A transferir no nó Atualizações e Manutenção da consola do Configuration Manager  
<!-- Source bug pending. Consider move to core content.  -->
Durante a transferência automática de atualizações por um ponto de ligação de serviço online, uma atualização pode ficar bloqueada, com o estado A transferir. Quando a transferência de uma atualização fica bloqueada, aparecem entradas semelhantes à seguinte nos ficheiros de registo indicados:  

Registo de DMPdownloader:  

-   ERRO: Falha ao transferir redist para 037cd17e-4d7b-40e1-802b-14bb682364c7 com comando /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 RedistVersion 112015 /noui. "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log:  

-   Erro: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.  

-   Erro: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**Solução**: No servidor do site, modifique a seguinte chave de registo para corresponder ao seguinte e, em seguida, reinicie o serviço SMS_Executive ou esperar até 24 horas para o próximo ciclo de transferência automática.  

-   **Chave para editar**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software publicação  

-   **Valor de estado**:  Definido como **146944** Decimal ou **0x00023e00** Hexadecimal  


###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>A configuração falha quando utilizar redist ficheiros a partir do CD. Pasta mais recente com um erro de verificação manifesto
<!-- Source bug pending  -->

Quando executar a configuração a partir de um CD. Pasta mais recente criado para a versão 1606 e utilizar os ficheiros de redist incluídos com esse CD. Pasta mais recente, o programa de configuração falha com os seguintes erros no registo de configuração do Configuration Manager:

  - ERRO: Falha na verificação de hash de ficheiro para defaultcategories.dll
  - ERRO: Falha na verificação manifesto. Versão incorreta do manifesto?

**Solução:**  Utilize um dos seguintes procedimentos:
 - Durante a configuração optar por transferir os ficheiros de redist mais recentes da Microsoft para utilizar em vez de os incluída no CD. Pasta mais recente.
 - Elimine manualmente o *cd.latest\redist\languagepack\zhh* pasta e, em seguida, execute o programa de configuração novamente.

### <a name="service-connection-tool-throws-an-exception-when-sql-server-is-remote-or-when-shared-memory-is-disabled"></a>Ferramenta de ligação de serviço emite uma exceção ao SQL server for remoto, ou quando a memória partilhada estiver desativada
A partir da versão 1606, a ferramenta de ligação de serviço gera uma exceção quando uma das seguintes opções for verdadeira:  
 -    A base de dados do site está distante do computador que aloja o ponto de ligação de serviço e utiliza uma porta padronizada (uma porta diferente é 1433)
 -     A base de dados do site está no mesmo servidor como o ponto de ligação de serviço, mas o protocolo SQL **memória partilhada** está desativado

A exceção é semelhante ao seguinte:
 - *Exceção não processada: System.Data.SqlClient.SqlException: Ocorreu um erro relacionadas com a rede ou específico da instância ao estabelecer uma ligação ao SQL Server. O servidor não foi encontrado ou não estava acessível. Certifique-se de que o nome da instância está correto e que o SQL Server está configurado para permitir ligações remotas. (fornecedor: Fornecedor Pipes nomeados, erro: 40 - não foi possível abrir uma ligação ao SQL Server)-*

**Solução**: Durante a utilização da ferramenta tem de modificar o registo do servidor que aloja o ponto de ligação de serviço para incluir informações sobre a porta do SQL Server:

   1.    Antes de utilizar a ferramenta, edite a seguinte chave de registo e adicionar o número da porta que está a ser utilizado para o nome do SQL Server:
    - Chave:   HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
      - Value: &lt;Nome do SQL Server >
    - Adicione: **,&lt;porta >**

    Por exemplo, para adicionar porta *15001* a um servidor com o nome *testserver.test.net*, a chave resultante seria: ***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.test.NET,15001***

   2.    Depois de adicionar a porta para o registo, a ferramenta deve funcionar normalmente.  

   3.    Após a utilização da ferramenta de conclusão, para ambas as **-ligar** e **-importar** passos, voltar a alterar a chave de registo para o valor original.  




<!-- No current Backup and Recovery relenotes
## Backup and recovery
-->



## <a name="client-deployment-and-upgrade"></a>Implementação e atualização do cliente  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>Falha de instalação do cliente com o código de erro 0x8007064c
<!--- SMS 486973 -->

Quando implementar o cliente para computadores Windows, a instalação falhará. O ficheiro ccmsetup contém uma entrada de "ficheiros 'C:\WINDOWS\ccmsetup\Silverlight.exe' devolveu o código de saída com falhas 1612. Falha de instalação"seguido de"InstallFromManifest falhou 0x8007064c".

**Solução** isto é provocado por uma versão danificada e anteriormente instalada do Silverlight. Pode tentar executar a ferramenta seguinte no computador afetado para corrigir este problema: [https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed) 




## <a name="operating-system-deployment"></a>Implementação do sistema operativo  

### <a name="issue-with-the-windows-adk-for-windows-10-version-1511"></a>Emitir com o Windows ADK para Windows 10, versão 1511  
Quando executa uma sequência de tarefas a partir do Centro de Software que utiliza uma imagem de arranque do Windows PE v.10.0.10586 a partir do Windows ADK 10, versão 1511, quando o computador reiniciar no Windows PE, ocorrerá uma falha quando "Inicializar dispositivos de hardware" com o erro: **Falha na inicialização do Windows PE com código de erro 0x80220014**  

**Solução**: Utilize o Windows 10 ADK original. Para obter mais informações, consulte o seguinte equipa blogue do System Center Configuration Manager: [Problema com o Windows ADK para Windows 10](http://blogs.technet.com/b/configmgrteam/archive/2015/11/20/issue-with-the-windows-adk-for-windows-10-version-1511.aspx)  

### <a name="dynamic-application-installation-fails-during-task-sequence-which-successfully-completes"></a>Falha da instalação da aplicação dinâmica durante a sequência de tarefas que foi concluída com êxito  
Quando implementa uma sequência de tarefas que utiliza a opção **Instalar aplicações de acordo com a lista de variáveis dinâmicas** e não for possível instalar uma das aplicações por qualquer motivo, a sequência de tarefas comunica êxito. Esta situação ocorre independentemente da forma como configura as seguintes opções:  

-   **Continuar com o erro** (no separador Opções do passo Instalar Aplicação)  

-   **Se a instalação de uma aplicação falhar, continue a instalar outras aplicações na lista** (no separador Propriedades do passo Instalar Aplicação)  

Pode ver o smsts.log, para determinar se não foi possível instalar uma aplicação.  

**Solução**: Utilize o **tsappinstallstatus** variável como uma condição uma passos subsequentes numa sequência de tarefas com uma condição para se a sequência de tarefas se Ocorreu um erro com uma das aplicações dinâmicas.  

### <a name="smb-might-not-work-properly-after-you-use-a-task-sequence-to-install-windows-10"></a>O SMB pode não funcionar corretamente depois de utilizar uma sequência de tarefas para instalar o Windows 10  
Quando utiliza uma sequência de tarefas para instalar uma imagem do Windows 10, o SMB pode não funcionar corretamente depois de o cliente do Configuration Manager ser instalado. Por exemplo, os seguintes passos da sequência de tarefas poderão falhar:  

-   Restaurar o Estado do Utilizador quando utilizado com um ponto de migração de estado  

-   Ligar à Pasta de Rede  

A partir de uma linha de comandos de administrador F8, pode continuar a fazer PING no computador, por exemplo, mas qualquer tráfego de rede SMB (como NET USE a partir de linha de comandos) pode falhar e aparecer o erro 1231 - A localização de rede não pode ser atingida.  

**Solução**:  
Adicione um passo de sequência de tarefas Executar Linha de Comandos após o passo de sequência de tarefas Configurar Windows e ConfigMgr para parar e, em seguida, inicie o serviço de Estação de Trabalho do seguinte modo:    
**net stop estação de trabalho /y & net iniciar estação de trabalho**  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>Por predefinição, os planos de manutenção criam muitas implementações e grupos de atualização de software duplicados  
Por predefinição, o assistente Criar Plano de Manutenção é executado atualmente após cada sincronização de atualizações de software. Sempre que o assistente é executado, cria um novo grupo de atualização de software e implementação. Se tiver uma agenda de sincronização de atualizações de software que é executada várias vezes por dia, por exemplo, o assistente Criar Plano de Manutenção irá criar vários, e provavelmente idênticos, grupos de atualização de software e implementações cada dia.  

**Solução**:    
Depois de criar um plano de manutenção, abra as propriedades do plano de manutenção, aceda ao separador **Agenda de Avaliação**, selecione **Executar a regra de forma programada**, clique em **Personalizar** e crie uma agenda personalizada. Por exemplo, pode fazer com que o plano de manutenção seja executado a cada 60 dias.  

### <a name="when-a-high-risk-deployment-dialog-is-visible-to-a-user-subsequent-high-risk-dialogs-with-a-sooner-deadline-are-not-displayed"></a>Quando uma caixa de diálogo de implementação de alto risco é visível para um utilizador, subsequentes caixas de diálogo de alto risco com um prazo sooner não são apresentadas
Depois de criar e implementar uma implementação de alto risco tarefas para os utilizadores, é apresentada uma caixa de diálogo de alto risco para o utilizador. Se o utilizador não fecha a caixa de diálogo, pode criar e implementar outra implementação de alto risco com um prazo sooner à frente da primeira, o utilizador não irão receber uma caixa de diálogo atualizado até que possam tem sido fechada a caixa de diálogo original. As implementações continuarão a executar nos prazos configurados.

**Solução**:  
O utilizador tem de fechar a caixa de diálogo para a implementação de alto risco primeiro ver a caixa de diálogo para a implementação de alto risco seguinte.

## <a name="mobile-device-management"></a>Gestão de dispositivos móveis  

### <a name="cannot-create-an-enrollment-profile-on-a-primary-site"></a>Não é possível criar um perfil de inscrição num site primário  
Um administrador não pode criar um perfil de inscrição na consola de administração do System Center Configuration Manager que ligue a um site primário. Quando tentar inscrever, o administrador verá um erro "token do DEP não tiver sido atualizado. Carregue um token de DEP"no Assistente do perfil de inscrição. Este erro ocorre apesar de ter sido carregado um token DEP válido para o site de administração central.  

**Solução**: Crie um perfil de inscrição na consola do System Center Configuration Manager que liga ao site de administração central.  

### <a name="dep-cannot-use-non-alpha-numeric-characters-in-enrollment-profiles"></a>O DEP não pode utilizar carateres não alfanuméricos em perfis de inscrição  
Os perfis de inscrição associados ao Perfil de Inscrição de Dispositivos (DEP) da Apple não podem utilizar carateres não alfanuméricos nos campos **Nome**, **Descrição**, **Departamento** e **Número de telefone** no perfil de inscrição quando o DEP está ativado. A utilização de carateres não alfanuméricos nestes campos irá criar um perfil de inscrição, mas o perfil não poderá ser carregado para a Apple. Não é apresentada qualquer mensagem de erro ou aviso pelo servidor Apple e os perfis não serão implementados em dispositivos geridos por DEP.  

**Solução**: Nenhuma.

### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>A eliminação completa de dados desativa os dispositivos Windows 10 com menos de 4 GB de RAM

Fazer a eliminação completa de dados em dispositivos Windows 10 RTM (versões anteriores à versão 1511) com menos de 4 GB de RAM pode deixar o dispositivo não utilizável. Depois de tentar fazer a eliminação de dados do dispositivo, o dispositivo não liga e não responde.

**Solução**: Certifique-se de que o Windows 10 RTM PCs ter, pelo menos, 4 GB de RAM disponível antes de efetuar uma eliminação completa no dispositivo. Para ver o número de versão de dispositivos Windows 10, introduza "winver" numa linha de comandos. Se o dispositivo já tiver sido apagado e já não estiver a responder, utilize uma pen USB do Windows 10 de arranque para iniciar e recuperar o acesso ao dispositivo.

### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>Quando um utilizador pertence a duas ou mais coleções de utilizadores nos quais esteja implementada uma política de termos e condições, o utilizador verá vários conjuntos dos mesmos termos  

Quando um administrador implementa um conjunto de termos em várias coleções de utilizadores e um utilizador é membro de mais de uma destas coleções, serão apresentadas a esse utilizador várias cópias de termos idênticos quando abrir o Portal da Empresa.  Por exemplo, se um utilizador com o nome "SampleUser" for um membro de duas coleções de utilizador diferente, uma denominada "CompanyEmployeesFTE" e "CompanyEmployeesNA", "e os termos e condições denominadas"CompanyTerms"for implementada CompanyEmployeesFTE e CompanyEmployeesNA, SampleUser verá dois conjuntos idênticos de CompanyTerms na página de aceitação de termos. Uma vez que os utilizadores só podem aceitar ou recusar todos os termos, não existe perigo de cair num estado de aceitação ambígua (em que o utilizador aceitou e rejeitou os termos). O relatório de aceitação dos Termos e Condições incluirá apenas uma linha para cada conjunto de termos para cada utilizador, pelo que não existe nenhum erro no relatório. O único efeito é que o utilizador verá dois conjuntos de termos na página de aceitação.  

**Solução**: Certifique-se de que cada utilizador está incluído apenas na uma coleção implementadas para os quais os termos de licenciamento.  

### <a name="android-for-work-email-profiles-that-use-certificate-authentication-are-not-applied-to-devices"></a>Android para perfis de e-mail de trabalho que utilizam a autenticação de certificados não serão aplicadas a dispositivos
<!--  487657 -->
Quando é criado um Android para o perfil de e-mail de trabalho, existem duas opções para autenticação. Uma é o nome de utilizador e palavra-passe e a outra é certificados. Neste momento, a opção de certificados não está a funcionar. Se o perfil é criado com o método de autenticação definido como **certificados**, o perfil não é aplicado no dispositivo e o utilizador irá ser-lhe pedido para introduzir manualmente detalhes da conta de correio eletrónico.

**SOLUÇÃO**: Nenhuma. Os administradores devem utilizar o **nome de utilizador e palavra-passe** opção ou aguarde até que este problema foi resolvido.

## <a name="reports-and-monitoring"></a>Monitorização e relatórios  

### <a name="the-health-attestation-report-is-empty-even-though-health-attestation-data-was-previously-collected"></a>O Relatório de Atestado de Estado de Funcionamento está vazio, apesar de os dados do atestado de estado de funcionamento terem sido recolhidos anteriormente  
Quando um utilizador administrativo com um direito de acesso que inclua a permissão **Leitura** para o grupo de permissões **Atestado de Estado de Funcionamento** visualiza o relatório de Atestado de Estado de Funcionamento, o relatório está vazio e não apresenta dados. Isto acontece porque as permissões para ver os dados no relatório de Atestado de Estado de Funcionamento estão ligadas ao grupo de permissões **Afinidade Dispositivo/Utilizador** e não ao grupo de permissões Atestado de Estado de Funcionamento.  

Este problema afeta o System Center Configuration Manager com o update 1602 e é esperado que seja resolvido numa atualização futura.  

**Solução**: Atribua o utilizador administrativo um grupo de segurança que inclua o **leitura** permissão para o **afinidades de dispositivo do utilizador** grupo de permissões.  

### <a name="conditional-access"></a>Acesso condicional  

#### <a name="the-same-user-collection-is-not-blocked-from-being-added-to-both-exempted-and-targeted-collections"></a>A mesma Coleção de Utilizador não é impedida de ser adicionada a Coleções Isentas e a Coleções de Destino.  
Isto só acontece quando adiciona a mesma **Coleção de Utilizadores** à página **Coleções Isentas** **antes** de adicioná-la à página **Coleção de Destino**.  Se adicionar primeiro uma **Coleção de Utilizador** à página **Coleções de Destino** e, em seguida, tentar adicionar a mesma **Coleção de Utilizador** à página **Coleção Isenta**, deverá ser apresentada uma mensagem de bloqueio normal.  

Acesso condicional do System Center Configuration Manager para este problema o afeta **Exchange no local** com atualização 1602 e é esperado que seja resolvido numa atualização futura.  

**Solução:** Adicionar o **coleção de utilizadores** para **visada coleções** página antes de selecionar **coleção de utilizadores** no **excluídos coleção** página ou certificar-se de que não está a adicionar o mesmo **coleção de utilizadores** visada e coleções excluídos.

## <a name="endpoint-protection"></a>Endpoint Protection
<!--  Product Studio bug 485370 added by Nathbarn 04 19 2017 -->
### <a name="antimalware-policy-fails-to-apply-on-windows-server-2016-core"></a>Política antimalware não consegue aplicar no Windows Server 2016 Core
Política antimalware não consegue aplicar no Windows Server 2016 Core.  O código de erro é 0x80070002.  Existe uma dependência em falta para ConfigSecurityPolicy.exe.

**Solução:**  Este problema for resolvido por [Knowledge Base artigo 4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) distribuídas 9 de Maio de 2017. 


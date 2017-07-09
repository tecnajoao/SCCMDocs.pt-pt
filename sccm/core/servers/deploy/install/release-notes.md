---
title: Notas - Configuration Manager | Microsoft Docs
description: "Consulte estas notas para problemas urgentes que ainda não foram corrigidos no produto ou abordados no artigo da Base de dados de Conhecimento Microsoft."
ms.custom: na
ms.date: 05/31/2017
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
ms.sourcegitcommit: dc221ddf547c43ab1f25ff83c3c9bb603297ece6
ms.openlocfilehash: 6113576ca38da27e9e8732b3930deee96db4ae2c
ms.contentlocale: pt-pt
ms.lasthandoff: 06/01/2017


---
# <a name="release-notes-for-system-center-configuration-manager"></a>Notas de versão do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Com o System Center Configuration Manager, notas de versão do produto são limitadas a problemas urgentes que ainda não foram corrigidos no produto (disponível por meio de uma atualização no console), ou são detalhados no artigo da Base de dados de Conhecimento Microsoft.  

 Para problemas conhecidos que afetam os cenários principais, estas informações são transmitidas na documentação do produto online, na biblioteca de documentação do System Center Configuration Manager.  

> [!TIP]  
>  Este tópico contém notas de versão para a ramificação atual do System Center Configuration Manager. Para a visualização técnica do System Center Configuration Manager, consulte [visualização técnica do System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

## <a name="setup-and-upgrade"></a>Configuração e atualização  

### <a name="after-you-update-a-configuration-manager-console-using-consolesetupexe-from-the-site-server-folder-recent-language-pack-changes-are-not-available"></a>Depois de atualizar um console do Configuration Manager usando ConsoleSetup.exe da pasta do servidor de site, as alterações recentes do pacote de idioma não estão disponíveis
<!--  SMS 486420  Applicability should be 1610 and 1702.  -->
Depois de executar uma atualização in-loco de um console usando ConsoleSetup.exe de uma pasta de instalação de servidores de site, os pacotes de idioma instalado recentemente podem não estar disponível. Isso ocorre quando:
- O site executa versão 1610 ou 1702.
- O console é atualizado no local usando ConsoleSetup.exe da pasta de instalação do servidor de site.

Quando esse problema ocorre, o console reinstalado não usa o último conjunto de pacotes de idiomas que foram configurados. Nenhum erro será retornado, mas disponíveis de pacotes de idioma para o console não terá sido alterado.  

**Solução alternativa:** Desinstalar o console atual e, em seguida, reinstale o console como uma nova instalação. Você pode usar ConsoleSetup.exe da pasta de instalação de servidores do site. Durante a instalação, certifique-se de selecionar os arquivos de pacote de idiomas que você deseja usar.


### <a name="with-version-1702-the-default-site-boundary-group-is-configured-for-use-for-site-assignment"></a>Com a versão 1702, o grupo de limites de site padrão está configurado para uso para a atribuição de site
<!--  SMS 486380   Applicability should only be to 1702. -->
Com a versão 1702, guia de referência padrão grupos de limites de site tem uma verificação de **utilize este grupo de limites para atribuição de site**, lista o site como o **site atribuído**e é esmaecida para que a configuração não pode ser editada ou removida.

**Solução alternativa:** Nenhuma. Você pode ignorar essa configuração. Embora o grupo está habilitado para atribuição de site, o grupo de limites de site padrão não é usado para atribuição de site. Com 1702, essa configuração garante que o grupo de limites de site padrão está associado com o site correto.



### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Ao instalar um site de filial de serviço de longo prazo, usando a versão 1606, um site de ramificação atual está instalado
<!-- Consider move to core content  -->
Quando você usar a mídia de linha de base versão 1606 da versão de outubro de 2016 para instalar um site de filial de manutenção de longo prazo (LTSB), o programa de instalação instala um site de ramificação atual. Isso ocorre porque a opção para instalar um ponto de conexão de serviço com a instalação do site não está selecionada.

 - Embora um ponto de conexão de serviço não seja necessário, ele deve ser selecionado para instalar durante a instalação para instalar um site LTSB.

Após a conclusão da instalação, você pode desinstalar o ponto de conexão de serviço.  No entanto, você deve ter uma conexão de serviço de ponto no modo offline ou online para enviar dados de telemetria e para obter atualizações de segurança para a ramificação atual e sites LTSB.

Se seu site instalado como um site de ramificação atual, mas você quiser instalar o LTSB, você pode desinstalar o site e, em seguida, reinstalá-lo. Como alternativa, você pode chamar [Microsoft Help and Support](http://go.microsoft.com/fwlink/?LinkId=243064) para obter assistência.  

Para confirmar que ramificação instalada, no console em **administração** > **configuração do Site** > **Sites**e abra **configurações da hierarquia**. A opção para converter o site em um site de ramificação atual está disponível apenas quando o site é executado o LTSB.  

**Solução alternativa:**  Nenhuma.   



### <a name="the--sql-server-backup-model-in-use-by-configuration-manager-can-change-from-full-to-simple"></a>O modelo de cópia de segurança do SQL Server utilizado pelo Configuration Manager pode ser alterado de completa para simples  
<!-- Confirm applicability for upgrade to later baselines. 1511 is out of support. 1606 is minmum supported baseline  -->

 Ao atualizar para o System Center Configuration Manager versão 1511, o modelo de cópia de segurança do SQL Server utilizado pelo Configuration Manager pode ser alterado de completa para simples.  

-   Se utilizar uma tarefa de cópia de segurança personalizada do SQL Server com o modelo de cópia de segurança completa (em vez da tarefa de cópia de segurança incorporada para o Configuration Manager), a atualização pode alterar o seu modelo de cópia de segurança de completa para simples.  

**Solução**: Após a atualização para a versão 1511, examine a configuração do SQL Server e restaure-o como completo, se necessário.  



### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>Uma atualização está bloqueada com o estado A transferir no nó Atualizações e Manutenção da consola do Configuration Manager  
<!-- Source bug pending. Consider move to core content.  -->
Durante a transferência automática de atualizações por um ponto de ligação de serviço online, uma atualização pode ficar bloqueada, com o estado A transferir. Quando a transferência de uma atualização fica bloqueada, aparecem entradas semelhantes à seguinte nos ficheiros de registo indicados:  

Registo de DMPdownloader:  

-   ERRO: Falha ao baixar redistribuição para 037cd17e-4d7b-40e1-802b-14bb682364c7 com o comando /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /redistversion 112015 /NoUI "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log:  

-   Erro: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.  

-   Erro: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**Solução**: No servidor do site, modifique a seguinte chave do registro para coincidir com o seguinte e, em seguida, reinicie o serviço SMS_Executive ou aguarde até 24 horas para o próximo ciclo de download automático.  

-   **Chave para editar**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software publicação  

-   **Valor do estado**:  Definido como **146944** Decimal ou **0x00023e00** Hexadecimal  


###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>A instalação falha ao usar arquivos de redistribuição do CD. Pasta mais recente com um erro de verificação de manifesto
<!-- Source bug pending  -->

Quando você executa a instalação de um CD. Pasta mais recente criado para a versão 1606 e usar os arquivos redist incluídos com esse CD. Pasta mais recente, a instalação falha com os seguintes erros no log de instalação do Configuration Manager:

  - ERRO: Falha na verificação de hash de arquivo para defaultcategories.dll
  - ERRO: Falha na verificação de manifesto. Versão incorreta do manifesto?

**Solução alternativa:**  Use um dos seguintes:
 - Durante a instalação escolha baixar os arquivos de redistribuição mais recentes da Microsoft para usar em vez das incluído no CD do. Pasta mais recente.
 - Exclua manualmente o *cd.latest\redist\languagepack\zhh* pasta e execute a instalação novamente.

### <a name="service-connection-tool-throws-an-exception-when-sql-server-is-remote-or-when-shared-memory-is-disabled"></a>Ferramenta de conexão de serviço gera uma exceção quando o SQL server for remoto, ou quando a memória compartilhada está desabilitada
A ferramenta de conexão de serviço a partir da versão 1606, gera uma exceção quando uma das seguintes opções for verdadeira:  
 -    O banco de dados do site é remoto do computador que hospeda o ponto de conexão de serviço e usa uma porta não padrão (uma porta diferente 1433)
 -     O banco de dados do site está no mesmo servidor como o ponto de conexão de serviço, mas o protocolo SQL **memória compartilhada** está desabilitado

A exceção é semelhante ao seguinte:
 - *Exceção sem tratamento: System.Data.SqlClient.SqlException: Ocorreu um erro relacionado à rede ou específico da instância ao estabelecer uma conexão com o SQL Server. O servidor não foi encontrado ou não estava acessível. Verifique se o nome da instância está correto e que o SQL Server está configurado para permitir conexões remotas. (provedor: Provedor de Pipes nomeados, erro: 40 - não foi possível abrir uma conexão com o SQL Server) –*

**Solução**: Durante o uso da ferramenta, você deve modificar o registro do servidor que hospeda o ponto de conexão de serviço para incluir informações sobre a porta do SQL Server:

   1.    Antes de usar a ferramenta, edite a seguinte chave do registro e adicione o número da porta que está em uso para o nome do SQL Server:
    - Chave:   HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
      - Value: &lt;Nome do SQL Server >
    - Adicione: **,&lt;porta >**

    Por exemplo, para adicionar a porta *15001* a um servidor chamado *testserver.test.net*, a chave resultante será: ***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.Test.NET,15001***

   2.    Depois de adicionar a porta no registro, a ferramenta deve funcionar normalmente.  

   3.    Após a conclusão, tanto para o uso da ferramenta de **-conectar** e **-importar** etapas, altere a chave do registro para o valor original.  




<!-- No current Backup and Recovery relenotes
## Backup and recovery
-->



## <a name="client-deployment-and-upgrade"></a>Implementação e atualização do cliente  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>A instalação do cliente falha com código de erro 0x8007064c
<!--- SMS 486973 -->

Quando você implanta o cliente para computadores Windows, a instalação falhará. O arquivo ccmsetup.log contém uma entrada "arquivo 'C:\WINDOWS\ccmsetup\Silverlight.exe' retornou o código de saída de falha 1612. Falha da instalação"seguido de"Falha de InstallFromManifest 0x8007064c".

**Solução alternativa** isso é causado por uma versão previamente instalada corrompida do Silverlight. Você pode tentar executar a ferramenta a seguir no computador afetado para corrigir esse problema: [https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)




## <a name="operating-system-deployment"></a>Implementação do sistema operativo  

### <a name="issue-with-the-windows-adk-for-windows-10-version-1511"></a>Emitir com o Windows ADK para Windows 10, versão 1511  
Quando você executa uma sequência de tarefas do Centro de Software que usa uma imagem de inicialização do Windows PE v. 10.0.10586 do Windows ADK 10, versão 1511, quando o computador é reiniciado no Windows PE, ele falhará ao "Inicializar dispositivos de hardware" com o erro: **Falha na inicialização do Windows PE com código de erro 0x80220014**  

**Solução**: Use o Windows 10 ADK original. Para obter mais informações, consulte o Blog de equipe do System Center Configuration Manager seguintes: [Problema com o Windows ADK para Windows 10](http://blogs.technet.com/b/configmgrteam/archive/2015/11/20/issue-with-the-windows-adk-for-windows-10-version-1511.aspx)  

### <a name="dynamic-application-installation-fails-during-task-sequence-which-successfully-completes"></a>Falha da instalação da aplicação dinâmica durante a sequência de tarefas que foi concluída com êxito  
Quando implementa uma sequência de tarefas que utiliza a opção **Instalar aplicações de acordo com a lista de variáveis dinâmicas** e não for possível instalar uma das aplicações por qualquer motivo, a sequência de tarefas comunica êxito. Esta situação ocorre independentemente da forma como configura as seguintes opções:  

-   **Continuar com o erro** (no separador Opções do passo Instalar Aplicação)  

-   **Se a instalação de uma aplicação falhar, continue a instalar outras aplicações na lista** (no separador Propriedades do passo Instalar Aplicação)  

Pode ver o smsts.log, para determinar se não foi possível instalar uma aplicação.  

**Solução**: Use o **tsappinstallstatus** variável como uma condição nas etapas posteriores em uma sequência de tarefas com uma condição de falha da sequência de tarefas se ocorreu um erro com um dos aplicativos dinâmicos.  

### <a name="smb-might-not-work-properly-after-you-use-a-task-sequence-to-install-windows-10"></a>O SMB pode não funcionar corretamente depois de utilizar uma sequência de tarefas para instalar o Windows 10  
Quando utiliza uma sequência de tarefas para instalar uma imagem do Windows 10, o SMB pode não funcionar corretamente depois de o cliente do Configuration Manager ser instalado. Por exemplo, os seguintes passos da sequência de tarefas poderão falhar:  

-   Restaurar o Estado do Utilizador quando utilizado com um ponto de migração de estado  

-   Ligar à Pasta de Rede  

A partir de uma linha de comandos de administrador F8, pode continuar a fazer PING no computador, por exemplo, mas qualquer tráfego de rede SMB (como NET USE a partir de linha de comandos) pode falhar e aparecer o erro 1231 - A localização de rede não pode ser atingida.  

**Solução**:  
Adicione um passo de sequência de tarefas Executar Linha de Comandos após o passo de sequência de tarefas Configurar Windows e ConfigMgr para parar e, em seguida, inicie o serviço de Estação de Trabalho do seguinte modo:    
**net stop workstation /y & net start estação de trabalho**  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>Por predefinição, os planos de manutenção criam muitas implementações e grupos de atualização de software duplicados  
Por predefinição, o assistente Criar Plano de Manutenção é executado atualmente após cada sincronização de atualizações de software. Sempre que o assistente é executado, cria um novo grupo de atualização de software e implementação. Se tiver uma agenda de sincronização de atualizações de software que é executada várias vezes por dia, por exemplo, o assistente Criar Plano de Manutenção irá criar vários, e provavelmente idênticos, grupos de atualização de software e implementações cada dia.  

**Solução**:    
Depois de criar um plano de manutenção, abra as propriedades do plano de manutenção, aceda ao separador **Agenda de Avaliação**, selecione **Executar a regra de forma programada**, clique em **Personalizar** e crie uma agenda personalizada. Por exemplo, pode fazer com que o plano de manutenção seja executado a cada 60 dias.  

### <a name="when-a-high-risk-deployment-dialog-is-visible-to-a-user-subsequent-high-risk-dialogs-with-a-sooner-deadline-are-not-displayed"></a>Quando uma caixa de diálogo de implantação de alto risco é visível para um usuário, caixas de diálogo de alto risco subsequentes com um prazo antes não são exibidas
Depois de criar e implantar uma implantação de tarefas de alto risco para os usuários, uma caixa de diálogo de alto risco é exibida para o usuário. Se o usuário não fechar a caixa de diálogo, crie e implante outra implantação de alto risco com um prazo antes que o primeiro, o usuário não receberá uma caixa de diálogo atualizado até que eles tenham fechado a caixa de diálogo original. As implantações ainda serão executada nos prazos configurados.

**Solução**:  
O usuário deve fechar a caixa de diálogo para a primeira implantação de alto risco ver a caixa de diálogo para a próxima implantação de alto risco.

## <a name="software-updates"></a>Atualizações de software

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>Um configurações de cliente do Office 365 de importação de um arquivo de configuração falha quando ela contém os idiomas sem suporte
Quando você importar as configurações de cliente do Office 365 de um arquivo de configuração XML existente e o arquivo contém os idiomas que não são suportados pelo cliente do Office 365 ProPlus, ocorrerá um erro. Para obter detalhes, consulte [implantar aplicativos do Office 365 para clientes do painel de gerenciamento de cliente do Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Solução**:    
Use somente o [idiomas com suporte pelo cliente do Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) no arquivo de configuração XML.  

## <a name="mobile-device-management"></a>Gestão de dispositivos móveis  

### <a name="cannot-create-an-enrollment-profile-on-a-primary-site"></a>Não é possível criar um perfil de inscrição num site primário  
Um administrador não pode criar um perfil de inscrição na consola de administração do System Center Configuration Manager que ligue a um site primário. Ao tentar registrar, o administrador verá o erro "token de DEP não foi atualizado. Carregue um token DEP"no Assistente de perfil de registro. Este erro ocorre apesar de ter sido carregado um token DEP válido para o site de administração central.  

**Solução**: Crie um perfil de registro no console do System Center Configuration Manager que se conecta ao site de administração central.  

### <a name="dep-cannot-use-non-alpha-numeric-characters-in-enrollment-profiles"></a>O DEP não pode utilizar carateres não alfanuméricos em perfis de inscrição  
Os perfis de inscrição associados ao Perfil de Inscrição de Dispositivos (DEP) da Apple não podem utilizar carateres não alfanuméricos nos campos **Nome**, **Descrição**, **Departamento** e **Número de telefone** no perfil de inscrição quando o DEP está ativado. A utilização de carateres não alfanuméricos nestes campos irá criar um perfil de inscrição, mas o perfil não poderá ser carregado para a Apple. Não é apresentada qualquer mensagem de erro ou aviso pelo servidor Apple e os perfis não serão implementados em dispositivos geridos por DEP.  

**Solução**: Nenhuma.

### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>A eliminação completa de dados desativa os dispositivos Windows 10 com menos de 4 GB de RAM

Fazer a eliminação completa de dados em dispositivos Windows 10 RTM (versões anteriores à versão 1511) com menos de 4 GB de RAM pode deixar o dispositivo não utilizável. Depois de tentar fazer a eliminação de dados do dispositivo, o dispositivo não liga e não responde.

**Solução**: Certifique-se de que computadores com Windows 10 RTM ter pelo menos 4 GB de RAM disponível antes de executar um apagamento completo do dispositivo. Para ver o número de versão de dispositivos Windows 10, introduza "winver" numa linha de comandos. Se o dispositivo já tiver sido apagado e já não estiver a responder, utilize uma pen USB do Windows 10 de arranque para iniciar e recuperar o acesso ao dispositivo.

### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>Quando um utilizador pertence a duas ou mais coleções de utilizadores nos quais esteja implementada uma política de termos e condições, o utilizador verá vários conjuntos dos mesmos termos  

Quando um administrador implementa um conjunto de termos em várias coleções de utilizadores e um utilizador é membro de mais de uma destas coleções, serão apresentadas a esse utilizador várias cópias de termos idênticos quando abrir o Portal da Empresa.  Por exemplo, se um usuário chamado "SampleUser" for um membro de duas coleções de usuário diferente, uma chamada "CompanyEmployeesFTE" e "CompanyEmployeesNA", "e os termos e condições chamadas"CompanyTerms"é implantado em CompanyEmployeesFTE e CompanyEmployeesNA, SampleUser verá dois conjuntos idênticos de CompanyTerms na página de aceitação dos termos. Uma vez que os utilizadores só podem aceitar ou recusar todos os termos, não existe perigo de cair num estado de aceitação ambígua (em que o utilizador aceitou e rejeitou os termos). O relatório de aceitação dos Termos e Condições incluirá apenas uma linha para cada conjunto de termos para cada utilizador, pelo que não existe nenhum erro no relatório. O único efeito é que o utilizador verá dois conjuntos de termos na página de aceitação.  

**Solução**: Certifique-se de que cada usuário está incluído somente em uma coleção à qual os termos foram implantados.  

### <a name="android-for-work-email-profiles-that-use-certificate-authentication-are-not-applied-to-devices"></a>Android para perfis de email de trabalho que usam a autenticação de certificado não são aplicadas a dispositivos
<!--  487657 -->
Quando um Android para o perfil de email de trabalho é criado, há duas opções para autenticação. Um é o nome de usuário e senha, e a outra é certificados. Neste momento, a opção de certificados não está funcionando. Se o perfil é criado com o método de autenticação definido como **certificados**, não será aplicado o perfil no dispositivo e o usuário será solicitado a inserir os detalhes da conta de email manualmente.

**SOLUÇÃO ALTERNATIVA**: Nenhuma. Administradores devem usar o **nome de usuário e senha** opção ou aguarde até que esse problema foi resolvido.

## <a name="reports-and-monitoring"></a>Monitorização e relatórios  

### <a name="the-health-attestation-report-is-empty-even-though-health-attestation-data-was-previously-collected"></a>O Relatório de Atestado de Estado de Funcionamento está vazio, apesar de os dados do atestado de estado de funcionamento terem sido recolhidos anteriormente  
Quando um utilizador administrativo com um direito de acesso que inclua a permissão **Leitura** para o grupo de permissões **Atestado de Estado de Funcionamento** visualiza o relatório de Atestado de Estado de Funcionamento, o relatório está vazio e não apresenta dados. Isto acontece porque as permissões para ver os dados no relatório de Atestado de Estado de Funcionamento estão ligadas ao grupo de permissões **Afinidade Dispositivo/Utilizador** e não ao grupo de permissões Atestado de Estado de Funcionamento.  

Esse problema afeta o System Center Configuration Manager com atualização 1602 e deve ser resolvido em uma atualização futura.  

**Solução**: Atribua ao usuário administrativo um grupo de segurança que inclui o **leitura** permissão para o **as afinidades de dispositivo** grupo de permissão.  

### <a name="conditional-access"></a>Acesso condicional  

#### <a name="the-same-user-collection-is-not-blocked-from-being-added-to-both-exempted-and-targeted-collections"></a>A mesma Coleção de Utilizador não é impedida de ser adicionada a Coleções Isentas e a Coleções de Destino.  
Isto só acontece quando adiciona a mesma **Coleção de Utilizadores** à página **Coleções Isentas** **antes** de adicioná-la à página **Coleção de Destino**.  Se adicionar primeiro uma **Coleção de Utilizador** à página **Coleções de Destino** e, em seguida, tentar adicionar a mesma **Coleção de Utilizador** à página **Coleção Isenta**, deverá ser apresentada uma mensagem de bloqueio normal.  

Esse problema afeta o acesso condicional para o System Center Configuration Manager **Exchange no local** com atualização 1602 e deve ser resolvido em uma atualização futura.  

**Solução alternativa:** Adicionar o **coleção de usuários** para **coleções de destino** página antes de selecionar **coleção de usuários** no **coleção isenta** página ou verifique se você está adicionando a mesma não **coleção de usuários** às coleções isenta e de destino.

## <a name="endpoint-protection"></a>Endpoint Protection
<!--  Product Studio bug 485370 added 04 19 2017 -->
### <a name="antimalware-policy-fails-to-apply-on-windows-server-2016-core"></a>Política de antimalware não se aplicam no Windows Server 2016 Core
Política de antimalware não se aplicam no Windows Server 2016 Core.  O código de erro é 0x80070002.  Há uma dependência ausente para ConfigSecurityPolicy.exe.

**Solução alternativa:**  Esse problema é resolvido pelo [artigo da Base de dados de Conhecimento 4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) distribuídas em 9 de maio de 2017.

<!-- Product Studio bug 462286 added  05 25 2017 and valid until July 2017 GA release -->
### <a name="windows-defender-advanced-threat-protection-policies-fail-on-older-client-agents"></a>Políticas do Windows Defender Advanced Threat Protection falharem em agentes de cliente mais antigos

Políticas do Windows Defender Advanced Threat Protection criado de um 1610 de versão do Configuration Manager ou servidor de site posterior não se aplicam à versão 1606 do Configuration Manager e os clientes anteriores.  Os clientes não são onboard e avaliação de política relata um erro. O **estado de implantação** na configuração do Windows Defender Advanced Threat Protection mostra **erro**.

**SOLUÇÃO ALTERNATIVA**: Atualize o cliente do Configuration Manager para a versão 1610 ou posterior.


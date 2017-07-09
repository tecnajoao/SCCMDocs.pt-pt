---
title: "Visualização técnica 1705 | Microsoft Docs"
description: "Saiba mais sobre os recursos disponíveis na versão de visualização técnica 1705 para o System Center Configuration Manager."
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f4c46bfab9b40b29654f4e883817a5508ab25b74
ms.openlocfilehash: 1a38d25fbc26bd1f45c6fa2a0e931536af2d8b2f
ms.contentlocale: pt-pt
ms.lasthandoff: 06/28/2017

---
# <a name="capabilities-in-technical-preview-1705-for-system-center-configuration-manager"></a>Recursos no Technical Preview 1705 do System Center Configuration Manager.

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos que estão disponíveis na visualização técnica para o System Center Configuration Manager, versão 1705. Você pode instalar esta versão para atualizar e adicionar novos recursos ao seu site do Configuration Manager technical preview. Antes de instalar esta versão da visualização técnica, analise [visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para usar uma visualização técnica, como atualizar entre versões e como fornecer comentários sobre os recursos em uma visualização técnica.    

**Problemas conhecidos nesta visualização técnica:**
-   **Conector do Operations Manager Suite não atualizar**. Quando você atualiza de uma versão anterior do Technical Preview que tiveram o conector do OMS configurado, esse conector não é atualizado e não está mais disponível no console do. Após a atualização, você deve [usar o Assistente de serviços do Azure](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) e restabeleça a conexão para seu espaço de trabalho do OMS.
-   **Superfície drivers não serão sincronizados com êxito**. Embora o suporte para drivers de superfície estão listados na **What's New** no console do Configuration Manager para o technical preview, esse recurso ainda não funcionem conforme o esperado.
-   **Não é possível criar o Windows Update para políticas de adiamento de negócios**. Embora a capacidade de configurar o Windows Update para políticas de adiamento de negócios é listada na **What's New** no console do Configuration Manager para o technical preview, o assistente não abrir, e não for possível configurar as políticas.


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**A seguir estão os novos recursos, que você pode experimentar com esta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>Ferramenta de redefinição de atualização  
Você pode usar a ferramenta Configuração do Gerenciador de atualização de redefinir, **CMUpdateReset.exe**, para corrigir problemas quando as atualizações no console tem problemas ao baixar ou replicação. Essa ferramenta é incluída na versão de Technical Preview 1705. Você pode encontrá-lo no servidor do site do seu site do technical preview, depois de instalar a visualização no ***\cd.latest\SMSSETUP\TOOLS*** pasta.

Você pode usar essa ferramenta com as versões de Technical Preview 1606 ou posteriores. Isso com versões anteriores suporte é fornecido para a ferramenta pode ser usada com cenários de atualização de um intervalo de visualização técnica, e sem ter de esperar até a próxima visualização técnica torna-se disponível.

Você pode usar essa ferramenta quando uma atualização no console ainda não foi instalado e está em um estado de falha. Um estado de falha pode significar o download da atualização permanece em andamento, mas está preso e demora muito tempo, talvez horas mais de suas expectativas históricas para pacotes de atualização de tamanho similar. Ele também pode ser uma falha ao replicar a atualização para os sites primários filho.  

Quando você executa a ferramenta, ele é executado em relação a atualização que você especificar. Por padrão, a ferramenta não exclui atualizações baixadas ou instaladas com êxito.  

### <a name="prerequisites"></a>Pré-requisitos
A conta usada para executar a ferramenta requer as seguintes permissões:
-   **Leitura** e **gravar** permissões para o banco de dados do site do site de administração central e cada site primário em sua hierarquia. Para definir essas permissões, você pode adicionar a conta de usuário como um membro do **db_datawriter** e **db_datareader** [funções de banco de dados fixas](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) no banco de dados do Configuration Manager de cada site. A ferramenta não consegue interagir com os sites secundários.
-   **Administrador local** no site de nível superior da hierarquia.
-   **Administrador local** no computador que hospeda o ponto de conexão de serviço.

Você precisará o GUID do pacote de atualização que você deseja redefinir. Para obter o GUID:
-   No console, vá para **administração** > **atualizações e manutenção** e, em seguida, no painel de exibição, clique no título de uma das colunas (como **estado**), em seguida, selecione **Guid do pacote**. Isso adiciona a coluna para a exibição e a coluna mostra o GUID do pacote de atualização.

> [!TIP]  
> Para copiar o GUID, selecione a linha para o pacote de atualização que deseja redefinir e, em seguida, use CTRL + C para copiar essa linha. Se você colar a seleção copiada em um editor de texto, você pode copiar somente o GUID para uso como um parâmetro de linha de comando quando você executar a ferramenta.

### <a name="run-the-tool"></a>Execute a ferramenta    
A ferramenta deve ser executada no site de nível superior da hierarquia.

Quando você executa a ferramenta, você usar parâmetros de linha de comando para especificar o SQL Server no site de nível superior da hierarquia, o nome de banco de dados do site e o GUID do pacote de atualização que você deseja redefinir. A ferramenta identifica os servidores adicionais necessárias para acessar, com base no status de atualizações.   

Se o pacote de atualização está em um *lançar download* de estado, a ferramenta não limpará o pacote. Como opção, você pode forçar a remoção de uma atualização que baixou com êxito usando o parâmetro de exclusão de força (consulte parâmetros de linha de comando neste tópico).

Depois que a ferramenta é executada:
-   Se um pacote foi excluído, reinicie o serviço SMS_Executive de sites de nível superior e, em seguida, verificar se há atualizações baixar o pacote novamente.
-   Se um pacote não foi excluído, você não precisa realizar qualquer ação, como a atualização será reinicializar e reinicie a instalação ou replicação.

**Parâmetros de linha de comando:**  

| Parâmetro        |Descrição                 |  
|------------------|----------------------------|  
|**-S &lt;FQDN do SQL Server do seu site de nível superior >** | *Necessário* <br> Você deve especificar o FQDN do SQL Server que hospeda o banco de dados do site para o site de nível superior da hierarquia.    |  
| **-D &lt;nome do banco de dados >**                        | *Necessário* <br> Você deve especificar o nome do banco de dados de sites de nível superior.  |  
| **-P &lt;GUID do pacote >**                         | *Necessário* <br> Você deve especificar o GUID para o pacote de atualização que você deseja redefinir.   |  
| **-I &lt;nome da instância do SQL Server >**             | *Opcional* <br> Use para identificar a instância do SQL Server que hospeda o banco de dados do site. |
| **-FDELETE**                              | *Opcional* <br> Use isto para forçar a exclusão de um pacote de atualização baixado com êxito. |  
 **Exemplos:**  
 Em um cenário típico, você deseja redefinir uma atualização que apresenta problemas de download. É o FQDN de servidores SQL *server1.fabrikam.com*, o banco de site é *CM_XYZ*e o pacote é o GUID *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Você pode executar: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ 61F16B3C-F1F6-4F9F-8647-2A524B0C802C -P***

 Em um cenário mais extremo, você deseja forçar a exclusão do pacote de atualização problemático. É o FQDN de servidores SQL *server1.fabrikam.com*, o banco de site é *CM_XYZ*e o pacote é o GUID *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Você pode executar: ***CMUpdateReset.exe - FDELETE -S server1.fabrikam.com -D CM_XYZ 61F16B3C-F1F6-4F9F-8647-2A524B0C802C -P***

### <a name="test-the-tool-with-the-technical-preview"></a>Testar a ferramenta com a visualização técnica  
Você pode usar essa ferramenta com as versões de Technical Preview 1606 ou posteriores. Isso com versões anteriores suporte é fornecido para que a ferramenta pode ser usada com um número maior de cenários de atualização da visualização técnica, sem a necessidade de aguardar até que a próxima versão de technical preview está disponível.

Execute a ferramenta em um pacote de atualização para uma versão technical preview antes que a atualização concluir sua verificação de pré-requisitos. Um estado de verificação de pré-requisitos concluída é identificado por um dos seguintes Status para o pacote no **administração** > **atualizações e manutenção**:  
-   **Verificação de pré-requisitos aprovada**
-   **Verificação de pré-requisitos aprovada com aviso**
-   **Falha na verificação de pré-requisito**


## <a name="high-dpi-console-support"></a>Suporte a alto DPI console

Com esta versão, problemas como o console do Configuration Manager pode ser expandido e exibe diferentes partes da interface do usuário quando exibido em dispositivos DPI alto (como um livro de superfície) devem ser corrigidos.


## <a name="peer-cache-improvements"></a>Aprimoramentos de Cache de mesmo nível
Começando com essa visualização técnica, o Cache par [não usa a conta de acesso de rede](/sccm/core/plan-design/hierarchy/client-peer-cache) para autenticar solicitações de download dos pares.


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>Melhorias para o SQL Server em grupos de disponibilidade AlwaysOn  
Com esta versão, agora você pode usar réplicas de confirmação assíncrona nos grupos de disponibilidade do SQL Server Always On usados com o Configuration Manager.  Isso significa que você pode adicionar mais réplicas para seus grupos de disponibilidade para usar como backups (remotos) fora do local e, em seguida, usá-los em um cenário de recuperação de desastres.  

-   Configuration Manager dá suporte usando a réplica de confirmação assíncrona para recuperar sua réplica de síncrona.  Consulte [opções de recuperação do banco de dados do site](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) no tópico Backup e recuperação para obter informações sobre como fazer isso.

-   Esta versão não dá suporte a failover para usar a réplica de confirmação assíncrona como seu banco de dados do site.
> [!CAUTION]  
> Porque o Configuration Manager não valida o estado da réplica de confirmação assíncrona para confirmar que é atual, e [por design dessa réplica pode estar fora de sincronia](https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes), uso de uma réplica de confirmação assíncrona, como o banco de dados do site pode colocar a integridade do site e dos dados em risco.  

-   Você pode usar o mesmo número e tipo de réplicas em um grupo de disponibilidade com suporte pela versão do SQL Server que você usa.   (O suporte anterior foi limitado a duas réplicas de confirmação síncrona).

### <a name="configure-an-asynchronous-commit-replica"></a>Configurar uma réplica de confirmação assíncrona
Para adicionar uma réplica assíncrona para um [grupo de disponibilidade que você usa com o Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database), você não precisa executar os scripts de configuração necessários para configurar uma réplica de síncrona. (Isso é porque não há suporte para usar essa réplica assíncrona como o banco de dados do site). Consulte [a documentação do SQL Server](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot)) para obter informações sobre como adicionar réplicas secundárias a grupos de disponibilidade.

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Usar a réplica assíncrona para recuperar o site
Antes de usar uma réplica assíncrona para recuperar o banco de dados do site, você deve parar o site primário ativo para impedir gravações adicionais para o banco de dados do site. Depois de parar o site, você pode usar uma réplica assíncrona em vez de usar um [banco de dados recuperado manualmente](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption).

Para parar o site, você pode usar o [ferramenta de manutenção de hierarquia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe) para interromper os serviços de chave no servidor do site. Use a linha de comando: **Preinst.exe /stopsite**   

Parar o site é equivalente a interromper o serviço Site Component Manager (sitecomp) seguido pelo serviço SMS_Executive, no servidor do site.

> [!TIP]  
> Se você usar uma réplica primária de passiva (introduzidos nesta visualização técnica como [alta disponibilidade da função de servidor do Site](#site-server-role-high-availability)), você não precisa interromper a réplica passiva. Somente o site primário ativo deve ser interrompido.



## <a name="improved-user-notifications-for-office-365-updates"></a>Melhor notificações de usuário para atualizações do Office 365
Melhorias foram feitas para aproveitar a experiência de usuário do Office clique para executar quando um cliente instala uma atualização do Office 365. Isso inclui notificações pop-up e no aplicativo e uma experiência de contagem regressiva. Antes desta versão, quando uma atualização do Office 365 foi enviada para um cliente, aplicativos do Office que estavam abertos foram fechados automaticamente sem aviso. Após essa atualização, aplicativos do Office serão não fechados inesperadamente.

### <a name="prerequisites"></a>Pré-requisitos
Esta atualização se aplica a clientes do Office 365 ProPlus.

### <a name="known-issues"></a>Problemas conhecidos
Quando um cliente avalia uma atribuição de atualização para a primeira vez e a atualização tem um prazo agendado no passado, agendado imediatamente ou programado dentro de 30 minutos do Office 365, a experiência de usuário do Office 365 pode ser inconsistente. Por exemplo, o cliente pode receber uma caixa de diálogo de contagem regressiva de 30 minutos para a atualização, mas foi possível iniciar a imposição real antes do final da contagem regressiva. Para evitar esse comportamento, considere o seguinte:
- Implante a atualização do Office 365 com um prazo final está agendada para mais de 60 minutos adiantados da hora atual.
- Configurar uma janela de manutenção durante o horário comercial na coleção ou configurar um período de cortesia de imposição na implantação.

### <a name="try-it-out"></a>Experimente!
Tente concluir as seguintes tarefas e, em seguida, envie-nos **comentários** do **início** guia da faixa de opções para nos contar como ela funcionou:
- Implante em um cliente de uma atualização do Office 365 com um prazo final definido para um tempo de pelo menos 60 minutos adiantados da hora atual. Observe o comportamento de novo no cliente.


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Configurar e implantar políticas de proteção de aplicativos do Windows Defender

[Proteção de aplicativo do Windows Defender](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) é um novo recurso do Windows que ajuda a proteger os usuários através da abertura de sites não confiáveis em um contêiner isolado seguro que não está acessível por outras partes do sistema operacional. Esse technical preview, adicionamos suporte para configurar esse recurso usando as configurações de conformidade do Configuration Manager que você configure e implante em uma coleção.
Este recurso será lançado na visualização para a versão de 64 bits da atualização do criador do Windows 10 (codinome: RS2). Para testar esse recurso agora, você deve estar usando uma versão de visualização desta atualização.


### <a name="before-you-start"></a>Antes de começar

Para criar e implantar políticas de proteção de aplicativos do Windows Defender, os dispositivos Windows 10 nos quais você implantar a política devem ser configurados com uma política de isolamento de rede. Para obter mais detalhes, consulte o blog post consultado posteriormente.
Esse recurso só funciona com versões atuais do Windows 10 Insider. Para testá-lo, os clientes devem estar executando uma recente Windows 10 Insider Build.

### <a name="try-it-out"></a>Experimente!

Certifique-se de que você leu uma postagem no blog para entender as Noções básicas sobre proteção de aplicativo do Windows Defender.

Para criar uma política e procurar as configurações disponíveis:

1.  No console do Configuration Manager, escolha **ativos e conformidade**.
2.  No **ativos e conformidade** espaço de trabalho, escolha **visão geral** > **Endpoint Protection** > **protetor de aplicativo do Windows Defender**.
3.  No **início** guia o **criar** de grupo, clique em **criar a política de proteção do Windows Defender aplicativo**.
4.  Usando a postagem do blog como referência, você pode procurar e defina as configurações disponíveis para experimentar o recurso.
5.  Quando tiver terminado, conclua o assistente e implantar a política para um ou mais dispositivos Windows 10.

### <a name="further-reading"></a>Leitura adicional

Para saber mais sobre a proteção de aplicativo do Windows Defender, consulte [esta postagem de blog]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97).
Além disso, para saber mais sobre o modo autônomo do Windows Defender aplicativo protetor, consulte [esta postagem de blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Novos recursos do AD do Azure e gerenciamento de nuvem

Nesta versão, você pode configurar os serviços de nuvem para usar o AD do Azure para suportar o cenário a seguir:

- Instalar o cliente do Configuration Manager da internet e que ele seja atribuído a um site do Configuration Manager manualmente.
- Use o Intune para implantar o cliente do Configuration Manager em dispositivos na internet.

### <a name="advantages"></a>Vantagens

Usar os serviços de nuvem e o Azure AD elimina a necessidade de usar certificados de autenticação de cliente.

Você pode descobrir os usuários do AD do Azure em seu site para usar nas coleções e outras operações do Configuration Manager.

### <a name="before-you-start"></a>Antes de começar

- Você deve ter um locatário do AD do Azure.
- Seus dispositivos devem executar o Windows 10 e ser AD do Azure associado.  Os clientes também podem ser Além disso integrado ao AD do Azure associado ao domínio).
- Além de [pré-requisitos existentes](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) para a função de sistema de site do ponto de gerenciamento, você deve adicionalmente garantir que **ASP.NET 4.5** (e quaisquer outras opções que são automaticamente selecionadas com esse) estão habilitadas no computador que hospeda esta função de sistema de site.
- Para usar o Microsoft Intune para implantar o cliente do Configuration Manager:
    - Você deve ter um trabalho de locatário do Intune (Configuration Manager e o Intune não precisam estar conectados).
    - No Intune, você criou e implantou um aplicativo que contém o cliente do Configuration Manager. Para obter detalhes sobre como fazer isso, consulte como instalar clientes em dispositivos Windows gerenciados por MDM do Intune.
- Para usar o Configuration Manager para implantar o cliente:
    - Pelo menos um ponto de gerenciamento deve ser configurado para modo HTTPS.
    - Você deve configurar um Gateway de gerenciamento de nuvem.


### <a name="set-up-the-cloud-management-gateway"></a>Configurar o Gateway de gerenciamento de nuvem

Configure o Gateway de gerenciamento de nuvem para permitir que clientes acessem seu site do Configuration Manager da internet sem o uso de certificados.

Você encontrará ajuda sobre como fazer isso nos tópicos a seguir:

- [Planejar para o gateway de gerenciamento de nuvem no Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway).
- [Configurar o gateway de gerenciamento de nuvem para o Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway).
- [Gateway de gerenciamento de nuvem no Gerenciador de configuração do monitor](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway).

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Configurar o aplicativo de serviços do Azure em serviços de nuvem do Configuration Manager

Isso conecta o site do Configuration Manager para o Azure AD e é um pré-requisito para todas as outras operações nesta seção. Para efetuar este procedimento:

1.  No **administração** espaço de trabalho do console do Configuration Manager, expanda **serviços de nuvem**e, em seguida, clique em **serviços do Azure**.
2.  No **início** guia o **serviços do Azure** de grupo, clique em **configurar os serviços do Azure**.
3.  Sobre o **serviços do Azure** página do Assistente de serviços do Azure, selecione **gerenciamento de nuvem** para permitir que os clientes sejam autenticados com a hierarquia usando o Azure AD.
4.  Sobre o **geral** página do assistente, especifique um nome e uma descrição para o serviço do Azure.
5.  Sobre o **aplicativo** página do assistente, selecione o seu ambiente do Azure na lista e clique em **procurar** para selecionar os aplicativos cliente e servidor que serão usados para configurar o serviço do Azure:
    - No **aplicativo Server** janela, selecione o aplicativo de servidor que você deseja usar e depois clique em **Okey**. Aplicativos de servidor são os aplicativos web do Azure que contêm as configurações para sua conta do Azure, incluindo sua ID de locatário, ID do cliente e uma chave secreta para clientes. Se você não tiver um aplicativo de servidor disponível, use um dos seguintes:
        - **Criar**: Para criar um novo aplicativo de servidor, clique em **criar**. Forneça um nome amigável para o aplicativo e o locatário. Em seguida, depois que você entrar no Azure, o Configuration Manager cria o aplicativo web do Azure para você, incluindo a ID do cliente e a chave secreta para uso com o aplicativo web. Posteriormente, você pode exibir essas do portal do Azure.
        - **Importação**: Para usar um aplicativo web que já existe na sua assinatura do Azure, clique em **importação**. Forneça um nome amigável para o aplicativo e o locatário e, em seguida, especifique a ID de locatário, ID do cliente e a chave secreta para o aplicativo web do Azure que você deseja que o Configuration Manager para usar. Depois de verificar as informações, clique em **Okey** para continuar. Este opton não está disponível atualmente nessa visualização técnica.
    - Repita o mesmo processo para o aplicativo cliente.

  Você precisa conceder a *ler dados do diretório* permissão do aplicativo quando você usar a importação de aplicativo, para definir as permissões corretas no portal do. Se você usar a criação de aplicativos, as permissões são criadas automaticamente com o aplicativo, mas você ainda precisa dar consentimento para o aplicativo no portal do Azure.
6.  No **descoberta** página do assistente, opcionalmente **ativar o Azure Active Directory usuário descoberta**e, em seguida, clique em **configurações**.
No **configurações de descoberta de usuário do AD do Azure** caixa de diálogo caixa, configure um agendamento para quando ocorre a descoberta. Você também pode habilitar a descoberta de deltas que verifica apenas novo ou alterado contas no AD do Azure.
7.  Conclua o assistente.

Neste ponto, você se conectou a seu site do Configuration Manager para o Azure AD.


### <a name="install-the-cm-client-from-the-internet"></a>Instalar o cliente CM da Internet

Antes de começar, certifique-se de que os arquivos de origem de instalação do cliente são armazenados localmente no dispositivo para o qual você deseja instalar o cliente.
Em seguida, use as instruções em [como implantar clientes em computadores com Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) usando a seguinte linha de comando de instalação (substitua os valores de exemplo com seus próprios valores):

**CCMSetup.exe /NoCrlCheck /Source:C:\CLIENT CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode = HEC AADTENANTID = 780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME = contoso AADCLIENTAPPID =<GUID> AADRESOURCEURI = https://contososerver**

- **/ NoCrlCheck**: Se o gerenciamento de nuvem ou ponto de gateway de gerenciamento usa um certificado de servidor não-públicos, em seguida, o cliente pode não ser capaz de alcançar o local da CRL.
- **/ Origem**: Pasta local:   Local dos arquivos de instalação do cliente.
- **CCMHOSTNAME**: O nome do seu ponto de gerenciamento da Internet. Você pode encontrá-lo executando **gwmi - namespace root\ccm\locationservices-classe SMS_ActiveMPCandidate** em um prompt de comando em um cliente gerenciado.
- **SMSMP**: O nome do seu ponto de gerenciamento da pesquisa – isso pode ser em sua intranet.
- **SMSSiteCode**: O código do site do site do Configuration Manager.
- **AADTENANTID**, **AADTENANTNAME**: A ID e o nome do locatário do AD do Azure é vinculado ao Configuration Manager. Você pode encontrar o dispositivo isso executando /status dsregcmd.exe em um prompt de comando no AD do Azure ingressado.
- **AADCLIENTAPPID**: A ID do aplicativo cliente do AD do Azure. Para obter ajuda sobre como encontrar isso, consulte [portal usado para criar um Active Directory do Azure principal do aplicativo e de serviço que pode acessar recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri**: O identificador de URI do aplicativo de servidor integrado do AD do Azure.

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>Use o Assistente para serviços do Azure para configurar uma conexão para OMS
Começando com a versão de visualização técnica 1705, use o **Assistente serviços Azure** para configurar sua conexão do Configuration Manager para o serviço de nuvem do Operations Management Suite (OMS). O assistente substitui os fluxos de trabalho anteriores para configurar essa conexão.

-   O assistente é usado para configurar os serviços de nuvem para o Configuration Manager, como o OMS, da Windows Store for Business (WSfB) e Azure Active Directory (AD do Azure).  

-   Configuration Manager se conecta ao OMS para recursos como [análise de Log](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite), ou [atualizar preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics).

### <a name="prerequisites-for-the-oms-connector"></a>Pré-requisitos para o conector do OMS
Pré-requisitos para configurar uma conexão para OMS são as mesmas [documentados para a versão da ramificação atual 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites). Essa informação é repetida aqui:  

-   Fornecendo a permissão do Configuration Manager para OMS.

-   O conector do OMS deve ser instalado no computador que hospeda um [ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) em [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

-   Você deve instalar um agente de monitoramento da Microsoft para o OMS instalado no ponto de conexão de serviço junto com o conector do OMS. O agente e o conector do OMS devem ser configurados para usar o mesmo **espaço de trabalho do OMS**. Para instalar o agente, consulte [Baixe e instale o agente](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) na documentação do OMS.
-   Depois de instalar o conector e o agente, você deve configurar o OMS para usar dados do Configuration Manager. Para fazer isso, no Portal do OMS é [coleções do Configuration Manager de importação](/azure/log-analytics/log-analytics-sccm#import-collections).

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Use o Assistente de serviços do Azure para configurar a conexão para OMS

1.  No console, vá para **administração** > **visão geral** > **serviços de nuvem** > **serviços do Azure**e, em seguida, escolha **configurar os serviços do Azure** do **início** guia da faixa de opções, para iniciar o **Assistente serviços Azure**.

2.  Sobre o **serviços do Azure** , selecione o serviço de nuvem do pacote de gerenciamento de operação. Forneça um nome amigável para o **nome do serviço do Azure** e uma descrição opcional e, em seguida, clique em **próximo**.

3.  Sobre o **aplicativo** , especifique seu ambiente do Azure (technical preview oferece suporte somente a nuvem pública). Em seguida, clique em **procurar** para abrir a janela do aplicativo de servidor.

4.  Selecione um aplicativo web:

    -   **Importação**: Para usar um aplicativo web que já existe na sua assinatura do Azure, clique em **importação**. Forneça um nome amigável para o aplicativo e o locatário e, em seguida, especifique a ID de locatário, ID do cliente e a chave secreta para o aplicativo web do Azure que você deseja que o Configuration Manager para usar. Depois que você **verificar** as informações, clique em **Okey** para continuar.   

    > [!NOTE]   
    > Quando você configura o OMS com essa visualização, o OMS oferece suporte somente a *importar* função para um aplicativo web. Não há suporte para a criação de um novo aplicativo web. Da mesma forma, não é possível reutilizar um aplicativo existente para o OMS.

5.  Se você concluiu todos os outros procedimentos com êxito, em seguida, as informações no **configuração de Conexão de OMS** tela aparecerão automaticamente nesta página. Informações para as configurações de conexão devem ser exibido para o **assinatura do Azure**, **grupo de recursos do Azure**, e **o espaço de trabalho do Operations Management Suite**.

6.  O assistente se conecta ao serviço OMS usando as informações que você tenha de entrada. Selecione as coleções de dispositivos que você deseja sincronizar com o OMS e, em seguida, clique em **adicionar**.

7.  Verifique suas configurações de conexão no **resumo** tela e, em seguida, selecione **próximo**. O **andamento** tela mostra o status de conexão e, em seguida, deve **concluir**.

8.  Depois que o assistente for concluído, o console do Configuration Manager mostra que você tenha configurado **operação Management Suite** como um **tipo de serviço de nuvem**.


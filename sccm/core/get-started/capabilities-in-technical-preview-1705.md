---
title: "Pré-visualização técnica 1705 | Microsoft Docs"
description: "Saiba mais sobre as funcionalidades disponíveis na versão de pré-visualização técnica 1705 para o System Center Configuration Manager."
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b977a79baec73999caa21648adcb6fcfec4a4935
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1705-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1705 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1705. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.    

**Problemas conhecidos neste Technical Preview:**
-   **Conector do Operations Manager Suite não atualizar**. Ao atualizar de uma versão anterior do Technical Preview que tinha o conector do OMS configurado, esse conector não está atualizado e já não está disponível na consola do. Após a atualização, tem de [utilizar o Assistente de serviços do Azure](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) e restabelecer a ligação à sua área de trabalho do OMS.
-   **Superfície controladores não sincronize com êxito**. Embora suporte para controladores superfície constam **Novidades** na consola do Configuration Manager para technical preview, esta funcionalidade não ainda funciona conforme esperado.
-   **Não é possível criar o Windows Update para políticas de diferimento por empresas**. Apesar da capacidade de configurar o Windows Update para políticas de diferimento por empresas está listada no **Novidades** na consola do Configuration Manager para technical preview, o assistente não for aberto e não é possível configurar as políticas.


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>Ferramenta de reposição de atualização  
Pode utilizar a ferramenta Configuration Manager Update repor, **CMUpdateReset.exe**, para corrigir os problemas quando as atualizações na consola tem problemas de transferir ou a replicar. Esta ferramenta está incluída com a versão de pré-visualização técnica 1705. Pode encontrá-lo no servidor do site do seu site de pré-visualização técnica depois de instalar a pré-visualização no ***\cd.latest\SMSSETUP\TOOLS*** pasta.

Pode utilizar esta ferramenta com versões do Technical Preview 1606 ou posteriores. Este efeitos suporte é fornecido para a ferramenta pode ser utilizada com cenários de atualização de um intervalo de pré-visualização técnica e sem ter de aguardar até a próxima pré-visualização técnica fica disponível.

Pode utilizar esta ferramenta quando uma atualização na consola ainda não tiver instalada e se encontra em estado de falha. Estado de falha pode significar a transferência da atualização continua em curso, mas está bloqueada e demorar uma hora excessivamente longa, talvez horas exceder as expetativas históricas para pacotes de atualização do tamanho semelhante. Também pode ser uma falha ao replicar a atualização para sites primários subordinados.  

Quando executar a ferramenta, é executada relativamente a atualização que especificou. Por predefinição, a ferramenta não elimina atualizações instaladas ou transferidas com êxito.  

### <a name="prerequisites"></a>Pré-requisitos
A conta que utiliza para executar a ferramenta requer as seguintes permissões:
-   **Leitura** e **escrever** permissões para a base de dados do site do site de administração central e cada site primário na sua hierarquia. Para definir estas permissões, pode adicionar a conta de utilizador como membro do **db_datawriter** e **db_datareader** [fixo funções de base de dados](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) na base de dados do Configuration Manager de cada site. A ferramenta não interage com os sites secundários.
-   **Administrador local** no site de nível superior da hierarquia.
-   **Administrador local** no computador que aloja o ponto de ligação de serviço.

Terá do GUID do pacote de atualização que pretende repor. Para obter o GUID:
-   Na consola, aceda a **administração** > **atualizações e manutenção** e, em seguida, no painel de visualização, faça duplo clique no cabeçalho de uma das colunas (como **estado**), em seguida, selecione **Guid de pacote**. Esta ação adiciona essa coluna à apresentação de e a coluna mostra o GUID do pacote de atualização.

> [!TIP]  
> Para copiar o GUID, selecione a linha para o pacote de atualização que pretende repor e, em seguida, utilize CTRL + C para copiar nessa linha. Se colar a seleção copiada para um editor de texto, em seguida, pode copiar apenas o GUID para utilização como um parâmetro de linha de comandos quando executar a ferramenta.

### <a name="run-the-tool"></a>Execute a ferramenta    
A ferramenta tem de ser executada no site de nível superior da hierarquia.

Quando executar a ferramenta, utilize os parâmetros da linha de comandos para especificar o SQL Server no site de nível superior da hierarquia, o nome de base de dados do site e o GUID do pacote de atualização que pretende repor. A ferramenta, em seguida, identifica os servidores adicionais, tem de aceder, com base no estado de atualizações.   

Se o pacote de atualização está a ser um *após a transferência* Estado, a ferramenta de limpeza não configurar o pacote. Como opção, pode forçar a remoção de uma atualização transferida com êxito utilizando o parâmetro de eliminação de imposição (consulte parâmetros de linha de comandos posteriormente neste tópico).

Depois da ferramenta é executada:
-   Se um pacote foi eliminado, reinicie o serviço do SMS_Executive de sites de nível superior e, em seguida, verifique a existência de atualizações a transferir o pacote novamente.
-   Se um pacote não foi eliminado, não terá de efetuar qualquer ação, tal como a atualização será reinicializar e reinicie a instalação ou a replicação.

**Parâmetros de linha de comandos:**  

| Parâmetro        |Descrição                 |  
|------------------|----------------------------|  
|**-S &lt;FQDN do SQL Server do seu site de nível superior >** | *Necessário* <br> Tem de especificar o FQDN do SQL Server que aloja a base de dados do site para o site de nível superior da hierarquia.    |  
| **-D &lt;nome de base de dados >**                        | *Necessário* <br> Tem de especificar o nome da base de dados de sites de nível superior.  |  
| **-P &lt;GUID do pacote >**                         | *Necessário* <br> Tem de especificar o GUID para o pacote de atualização que pretende repor.   |  
| **-I &lt;nome de instância do SQL Server >**             | *Opcional* <br> Utilize esta opção para identificar a instância do SQL Server que aloja a base de dados do site. |
| **-FDELETE**                              | *Opcional* <br> Utilize esta opção para forçar a eliminação de um pacote de atualização transferido com êxito. |  
 **Exemplos:**  
 Um cenário típico, que pretende repor uma atualização que tem problemas de transferência. O FQDN de servidores SQL é *server1.fabrikam.com*, a base de dados do site *CM_XYZ*e o pacote GUID é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Execute: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ 61F16B3C-F1F6-4F9F-8647-2A524B0C802C -P***

 Num cenário mais extremos, pretender forçar a eliminação do pacote de atualização problemáticas. O FQDN de servidores SQL é *server1.fabrikam.com*, a base de dados do site *CM_XYZ*e o pacote GUID é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Execute: ***CMUpdateReset.exe - FDELETE -S server1.fabrikam.com -D CM_XYZ 61F16B3C-F1F6-4F9F-8647-2A524B0C802C -P***

### <a name="test-the-tool-with-the-technical-preview"></a>Testar a ferramenta com o Technical Preview  
Pode utilizar esta ferramenta com versões do Technical Preview 1606 ou posteriores. Isto efeitos suporte é fornecido para que a ferramenta pode ser utilizada com um grande número de cenários de atualização de pré-visualização técnica, sem ter de aguardar até a próxima versão de pré-visualização técnica está disponível.

Execute a ferramenta num pacote de atualização para uma versão de pré-visualização técnica antes que a atualização a concluir a verificação de pré-requisitos. Um Estado de verificação de pré-requisitos concluída é identificado por um dos seguintes Estados para o pacote no **administração** > **atualizações e manutenção**:  
-   **Passada na verificação de pré-requisitos**
-   **Verificação de pré-requisito aprovada com aviso**
-   **Falha na verificação de pré-requisitos**


## <a name="high-dpi-console-support"></a>Suporte da consola PPP elevado

Com esta versão, problemas com como a consola do Configuration Manager dimensiona e apresenta as diferentes partes da IU quando são visualizados em dispositivos de PPP elevados (como uma superfície book) devem ser corrigidos.


## <a name="peer-cache-improvements"></a>Melhorias da Cache ponto a ponto
Começando com esta pré-visualização técnica, a Cache ponto a ponto [já não utiliza a conta de acesso de rede](/sccm/core/plan-design/hierarchy/client-peer-cache) para autenticar pedidos de transferência de elementos.


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>Melhoramentos para o SQL Server Always On nos grupos de disponibilidade  
Com esta versão, agora, pode utilizar réplicas com consolidação assíncrona na SQL Server Always On nos grupos de disponibilidade que utilizar com o Configuration Manager.  Isto significa que pode adicionar réplicas adicionais para os grupos de disponibilidade para utilizar como as cópias de segurança (remotas) fora das instalações e, em seguida, utilizá-los num cenário de recuperação após desastre.  

-   O Configuration Manager suporta utilizando a réplica de consolidação assíncrona para recuperar a réplica síncrona.  Consulte [opções de recuperação de base de dados do site](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) no tópico cópia de segurança e recuperação para obter informações sobre como efetuar este procedimento.

-   Esta versão não suporta a ativação pós-falha para utilizar a réplica de consolidação assíncrona como a base de dados do site.
> [!CAUTION]  
> Porque o Configuration Manager não valide o estado da réplica de consolidação assíncrona para confirmar a sua atual, e [por predefinição, este tipo uma réplica pode ser sincronizada](https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes), utilização de uma réplica de consolidação assíncrona, como a base de dados do site pode colocar a integridade do seu site e os dados em risco.  

-   Pode utilizar o mesmo número e tipo de réplicas num grupo de disponibilidade como suportada pela versão do SQL Server que utilizar.   (Suporte anterior estava limitado a duas réplicas com consolidação síncrona.)

### <a name="configure-an-asynchronous-commit-replica"></a>Configurar uma réplica de consolidação assíncrona
Para adicionar uma réplica assíncrona para uma [grupo de disponibilidade utilizar com o Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database), não terá de executar os scripts de configuração necessários para configurar uma réplica síncrona. (Isto acontece porque não são suportadas para utilizar essa réplica assíncrona como a base de dados do site.) Consulte [documentação do SQL Server](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot)) para obter informações sobre como adicionar réplicas secundárias para grupos de disponibilidade.

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Utilizar a réplica assíncrona para recuperar o site
Antes de utilizar uma réplica assíncrona para recuperar a base de dados do site, tem de parar o site primário Active Directory para impedir que escritas adicionais para a base de dados do site. Depois de parar o site, pode utilizar uma réplica assíncrona em vez de utilizar um [base de dados recuperada manualmente](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption).

Para parar o site, pode utilizar o [ferramenta manutenção da hierarquia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe) parar os serviços de chaves no servidor do site. Utilize a linha de comandos: **Preinst.exe /stopsite**   

Parar o site é equivalente ao parar o serviço do Gestor de componentes do Site (sitecomp) seguido pelo serviço do SMS_Executive, no servidor do site.

> [!TIP]  
> Se utilizar uma réplica primária passiva (introduzidas nesta pré-visualização técnica como [disponibilidade elevada da função de servidor do Site](#site-server-role-high-availability)), não terá de parar a réplica passiva. Tem de ser parado apenas o site primário Active Directory.



## <a name="improved-user-notifications-for-office-365-updates"></a>Melhorado notificações de utilizador para atualizações do Office 365
Foram efetuados melhoramentos ao tirar partido a experiência de utilizador do Office Clique para execução quando um cliente instala uma atualização do Office 365. Isto inclui uma experiência de contagem decrescente e notificações de pop-up e na aplicação. Antes desta versão, quando uma atualização do Office 365 foi enviada para um cliente, as aplicações do Office que tiverem sido abertas foram fechadas automaticamente sem aviso. Depois desta atualização, aplicações do Office serão já não é possível fechar inesperadamente.

### <a name="prerequisites"></a>Pré-requisitos
Esta atualização aplica-se aos clientes do Office 365 ProPlus.

### <a name="known-issues"></a>Problemas conhecidos
Quando um cliente avalia uma atribuição de atualizações para a primeira vez e a atualização possui um prazo agendado no passado, agendada imediatamente ou agendada dentro de 30 minutos do Office 365, a experiência de utilizador do Office 365 pode ser inconsistente. Por exemplo, o cliente pode receber uma caixa de diálogo de contagem decrescente até 30 minutos para a atualização, mas foi possível iniciar a imposição real antes do fim de contagem decrescente. Para evitar este comportamento, considere o seguinte:
- Implemente a atualização do Office 365 com um prazo que esteja agendada para mais de 60 minutos antes do tempo atual.
- Configurar uma janela de manutenção durante horas na coleção ou configurar um período de tolerância de imposição na implementação.

### <a name="try-it-out"></a>Experimente!
Experimente concluir as seguintes tarefas e, em seguida, envie-nos **comentários** do **home page** separador do friso para nos informar como correu:
- Implemente um cliente de uma atualização do Office 365 com um prazo definido para um período de tempo, pelo menos, 60 minutos antes do tempo atual. Observe o comportamento de novo no cliente.


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Configurar e implementar políticas de proteção de aplicações do Windows Defender

[Proteção de aplicações do Windows Defender](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) é uma nova funcionalidade do Windows que ajuda a proteger os seus utilizadores abrindo não fidedignos web sites num contentor isolado seguro que não pode ser acedido por outras partes do sistema operativo. Esta pré-visualização técnica, adicionámos suporte para configurar esta funcionalidade utilizando as definições de compatibilidade do Configuration Manager que configurar e, em seguida, implementar numa coleção.
Esta funcionalidade será lançada em pré-visualização para a versão de 64 bits da atualização do Windows 10 Creator (nome: RS2). Para testar esta funcionalidade agora, tem de utilizar uma versão de pré-visualização desta atualização.


### <a name="before-you-start"></a>Antes de começar

Para criar e implementar políticas de proteção de aplicações do Windows Defender, os dispositivos Windows 10 nos quais implementou a política tem de ser configurados com uma política de isolamento de rede. Para obter mais detalhes, consulte o blogue post referenciado mais tarde.
Esta capacidade funciona apenas com atuais compilações do Windows 10 internas. Para testar, os clientes tem de executar um recente Windows 10 Insider criar.

### <a name="try-it-out"></a>Experimente!

Certifique-se de que leu a mensagem de blogue para compreender as noções básicas sobre proteção de aplicações do Windows Defender.

Para criar uma política e, para procurar as definições disponíveis:

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade**.
2.  No **ativos e compatibilidade** área de trabalho, escolha **descrição geral** > **Endpoint Protection** > **Guard de aplicação do Windows Defender**.
3.  No **home page** separador o **criar** , clique em **criar Windows Defender Guard política aplicações**.
4.  Utilizar a mensagem de blogue como uma referência, pode procurar e configurar as definições disponíveis para experimentar a funcionalidade.
5.  Quando tiver terminado, conclua o assistente e implementar a política para um ou mais dispositivos do Windows 10.

### <a name="further-reading"></a>Ler mais

Para ler mais informações sobre proteção de aplicações do Windows Defender, consulte [esta mensagem de blogue]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97).
Além disso, para saber mais sobre o modo autónomo de proteção de aplicações do Windows Defender, consulte o artigo [esta mensagem de blogue](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Novas funcionalidades para o Azure AD e gestão de nuvem

Nesta versão, pode configurar os serviços de nuvem para utilizar o Azure AD para suportar o seguinte cenário:

- Instalar o cliente do Configuration Manager a partir da internet e que o atribua a um site do Configuration Manager manualmente.
- Utilize o Intune para implementar o cliente do Configuration Manager para dispositivos na internet.

### <a name="advantages"></a>Vantagens

Utilizar serviços em nuvem e do Azure AD remove a necessidade de utilizar certificados de autenticação de cliente.

Pode detetar os utilizadores do Azure AD para o site para utilizar em coleções e outras operações do Configuration Manager.

### <a name="before-you-start"></a>Antes de começar

- Tem de ter um inquilino do Azure AD.
- Os seus dispositivos tem de executar o Windows 10 e ser do Azure AD associado.  Os clientes também podem ser associado a um além para o Azure AD associada ao domínio).
- Para além de [pré-requisitos existentes](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) para função de sistema de sites do ponto de gestão, deve adicionalmente garantir que **ASP.NET 4.5** (e quaisquer outras opções selecionadas automaticamente com esta) estão ativados no computador que aloja esta função de sistema de sites.
- Para utilizar o Microsoft Intune para implementar o cliente do Configuration Manager:
    - Tem de ter um inquilino do Intune (Configuration Manager e efetue Intune não devem estar ligados).
    - No Intune, tem de criar e implementar uma aplicação que contém o cliente do Configuration Manager. Para obter mais informações sobre como fazê-lo, consulte como instalar clientes em dispositivos Windows geridos por MDM do Intune.
- Para utilizar o Configuration Manager para implementar o cliente:
    - Pelo menos um ponto de gestão tem de ser configurado para o modo HTTPS.
    - Tem de configurar um Gateway de gestão de nuvem.


### <a name="set-up-the-cloud-management-gateway"></a>Configurar o Gateway de gestão de nuvem

Configure o Gateway de gestão de nuvem para permitir que os clientes aceder ao site do Configuration Manager através da internet sem utilizar certificados.

Encontrará ajuda sobre como fazê-lo nos seguintes tópicos:

- [Planear para o gateway de gestão de nuvem no Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway).
- [Configurar o gateway de gestão de nuvem para o Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway).
- [Gateway de gestão de nuvem de monitor no Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway).

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Configurar a aplicação de serviços do Azure nos serviços de nuvem do Configuration Manager

Esta ação liga o site do Configuration Manager para o Azure AD e é um pré-requisito para todas as outras operações nesta secção. Para efetuar este procedimento:

1.  No **administração** área de trabalho da consola do Configuration Manager, expanda **serviços em nuvem**e, em seguida, clique em **serviços do Azure**.
2.  No **home page** separador o **serviços do Azure** , clique em **configurar os serviços do Azure**.
3.  No **serviços do Azure** página do Assistente de serviços do Azure, selecione **gestão de nuvem** para permitir que os clientes autenticar com a hierarquia de utilizar o Azure AD.
4.  No **geral** página do assistente, especifique um nome e uma descrição para o serviço do Azure.
5.  No **aplicação** página do assistente, selecione o seu ambiente do Azure da lista e clique em **procurar** para selecionar as aplicações de servidor e cliente que serão utilizadas para configurar o serviço do Azure:
    - No **aplicação Server** janela, selecione a aplicação de servidor que pretende utilizar e, em seguida, clique em **OK**. Aplicações de servidor são as aplicações web do Azure que contêm as configurações para a sua conta do Azure, incluindo o ID de inquilino, ID de cliente e uma chave secreta para clientes. Se não tiver uma aplicação de servidor disponível, utilize um dos seguintes:
        - **Criar**: Para criar uma nova aplicação de servidor, clique em **criar**. Forneça um nome amigável para a aplicação e de inquilino. Em seguida, depois, inicie sessão no Azure, o Configuration Manager cria a aplicação web no Azure para si, incluindo o ID de cliente e a chave secreta para utilização com a aplicação web. Mais tarde, pode ver estes do portal do Azure.
        - **Importar**: Para utilizar uma aplicação web que já existe na sua subscrição do Azure, clique em **importação**. Forneça um nome amigável para a aplicação e de inquilino e, em seguida, especifique o ID do inquilino, ID de cliente e a chave secreta para a aplicação web do Azure que pretende utilizar o Configuration Manager. Depois de verificar as informações, clique em **OK** para continuar. Este opton não está atualmente disponível nesta pré-visualização técnica.
    - Repita o mesmo processo para a aplicação de cliente.

  Tem de conceder a *ler os dados de diretório* permissão de aplicação ao utilizar a importação de aplicação, para definir as permissões corretas no portal. Se utilizar a criação da aplicação as permissões são automaticamente criadas com a aplicação, mas ainda tem de dar consentimento para a aplicação no portal do Azure.
6.  No **deteção** página do assistente, opcionalmente **ativar o Azure Active Directory deteção de utilizadores**e, em seguida, clique em **definições**.
No **definições de deteção de utilizador do Azure AD** diálogo caixa, configure uma agenda para quando ocorre a deteção. Também pode ativar a deteção de diferenças que verifica a existência de apenas novos ou alterados contas no Azure AD.
7.  Conclua o assistente.

Neste momento, ligou-se o site do Configuration Manager para o Azure AD.


### <a name="install-the-cm-client-from-the-internet"></a>Instalar o cliente CM a partir da Internet

Antes de começar, certifique-se de que os ficheiros de origem de instalação do cliente são armazenados localmente no dispositivo para o qual pretende instalar o cliente.
Em seguida, utilize as instruções no [como implementar clientes em computadores Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) utilizando a seguinte linha de comandos de instalação (substituir os valores de exemplo com os seus próprios valores):

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode = HEC AADTENANTID = 780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME = contoso AADCLIENTAPPID =<GUID> AADRESOURCEURI = https://contososerver**

- **/ /Nocrlcheck**: Se na nuvem ou ponto de gestão de gateway de gestão utiliza um certificado de servidor não público, em seguida, o cliente poderá não ser capaz de alcançar a localização da CRL.
- **/ Origem**: Pasta local:   Localização dos ficheiros de instalação de cliente.
- **CCMHOSTNAME**: O nome do seu ponto de gestão de Internet. Pode encontrá-lo executando **gwmi - espaço de nomes root\ccm\locationservices-classe SMS_ActiveMPCandidate** numa linha de comandos num cliente gerido.
- **SMSMP**: O nome do seu ponto de gestão de pesquisa – Isto pode ser na sua intranet.
- **SMSSiteCode**: O código do site do site do Configuration Manager.
- **AADTENANTID**, **AADTENANTNAME**: O ID e nome do inquilino do Azure AD ligado para o Configuration Manager. Pode encontrar isto executando dsregcmd.exe /status numa linha de comandos num Azure AD associada ao dispositivo.
- **AADCLIENTAPPID**: O ID de aplicação de cliente do Azure AD. Para ajudar a encontrar isto, consulte [portal de utilização para criar um Azure Active Directory principal de serviço e aplicação que pode aceder aos recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri**: O identificador URI da aplicação de servidor integradas do Azure AD.

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>Utilize o Assistente de serviços do Azure para configurar uma ligação à OMS
Começando com a versão de pré-visualização técnica 1705, utilize o **Assistente de serviços do Azure** para configurar a ligação do Configuration Manager para o serviço de nuvem do Operations Management Suite (OMS). O assistente substitui o anteriores fluxos de trabalho para configurar esta ligação.

-   O assistente é utilizado para configurar os serviços em nuvem para o Configuration Manager, como o OMS, a loja Windows para empresas (WSfB) e o Azure Active Directory (Azure AD).  

-   O Configuration Manager liga-se ao OMS para funcionalidades como [Log Analytics](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite), ou [atualizar preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics).

### <a name="prerequisites-for-the-oms-connector"></a>Pré-requisitos para o conector do OMS
Pré-requisitos para configurar uma ligação ao OMS são iguais às [documentados para a versão do ramo atual 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites). Essas informações são repetidas aqui:  

-   Conceder permissão de Gestor de configuração à OMS.

-   O conector do OMS tem de estar instalado no computador que aloja um [ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) que está a ser [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

-   Tem de instalar um agente de monitorização da Microsoft para OMS instalado no ponto de ligação de serviço juntamente com o conector do OMS. O agente e o conector do OMS tem de ser configurados para utilizar o mesmo **área de trabalho OMS**. Para instalar o agente, consulte [transferir e instalar o agente](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) na documentação do OMS.
-   Depois de instalar o conector e o agente, tem de configurar o OMS para utilizar os dados do Configuration Manager. Para tal, no Portal do OMS, [Gestor de configuração importar coleções](/azure/log-analytics/log-analytics-sccm#import-collections).

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Utilize o Assistente de serviços do Azure para configurar a ligação ao OMS

1.  Na consola, aceda a **administração** > **descrição geral** > **serviços em nuvem** > **serviços do Azure**e, em seguida, escolha **configurar os serviços do Azure** do **home page** separador do Friso, para iniciar o **Assistente de serviços do Azure**.

2.  No **serviços do Azure** página, selecione o serviço de nuvem operação Management Suite. Forneça um nome amigável para o **nome do serviço do Azure** e uma descrição opcional e, em seguida, clique em **seguinte**.

3.  No **aplicação** página, especifique o seu ambiente do Azure (technical preview suporta apenas na nuvem pública). Em seguida, clique em **procurar** para abrir a janela de aplicação de servidor.

4.  Selecione uma aplicação web:

    -   **Importar**: Para utilizar uma aplicação web que já existe na sua subscrição do Azure, clique em **importação**. Forneça um nome amigável para a aplicação e de inquilino e, em seguida, especifique o ID do inquilino, ID de cliente e a chave secreta para a aplicação web do Azure que pretende utilizar o Configuration Manager. Depois de **verifique** informações, clique em **OK** para continuar.   

    > [!NOTE]   
    > Quando configura o OMS com esta pré-visualização, OMS só suporta o *importar* função para uma aplicação web. Criar uma nova aplicação web não é suportada. Da mesma forma, não é possível reutilizar uma aplicação existente para OMS.

5.  Se lhe conseguido todos os outros procedimentos com êxito, em seguida, as informações no **configuração da ligação OMS** ecrã serão apresentadas automaticamente nesta página. As informações para as definições de ligação devem aparecer para sua **subscrição do Azure**, **grupo de recursos do Azure**, e **área de trabalho do Operations Management Suite**.

6.  O assistente liga ao serviço do OMS utilizando as informações que tenha de entrada. Selecione as coleções de dispositivos que pretende sincronizar com o OMS e, em seguida, clique em **adicionar**.

7.  Verifique as definições de ligação no **resumo** ecrã, em seguida, selecione **seguinte**. O **progresso** ecrã mostra o estado da ligação, em seguida, deve **concluída**.

8.  Depois de concluir o assistente, a consola do Configuration Manager mostra que configurou **operação Management Suite** como um **o tipo de serviço de nuvem**.

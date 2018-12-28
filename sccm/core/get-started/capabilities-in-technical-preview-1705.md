---
title: Pré-visualização técnica 1705
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis na versão 1705 Technical Preview do System Center Configuration Manager.
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a9a5aeb35137a74152333a78e95781fb727eecdf
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421608"
---
# <a name="capabilities-in-technical-preview-1705-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1705 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1705. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para a utilização de um técnico de pré-visualização, como atualizar entre as versões e como fornecer comentários sobre os recursos de uma technical preview.    

**Problemas conhecidos neste Technical Preview:**
-   **Conector do Operations Manager Suite não atualiza**. Ao atualizar de uma versão anterior do Technical Preview que tinha o conector do OMS configurado, esse conector não é atualizado e já não está disponível na consola do. Após a atualização, deve [utilizar o Assistente de serviços do Azure](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) e restabelecer a ligação à sua área de trabalho do OMS.
-   **Superfície drivers não sincronizar com êxito**. Mesmo que o suporte para drivers de superfície estão listados na **o que há de novo** na consola do Configuration Manager para technical preview, esta funcionalidade não ainda funciona conforme esperado.
-   **Não é possível criar a atualização do Windows para políticas de diferimento de negócios**. Embora a capacidade de configurar a atualização do Windows para políticas de diferimento de negócios está listada na **o que há de novo** na consola do Configuration Manager para technical preview, o assistente não for aberto e não consegue configurar qualquer políticas.


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>Ferramenta de reposição de atualizações  
Pode utilizar a ferramenta Configuration Manager Update repor, **CMUpdateReset.exe**, para corrigir os problemas quando as atualizações na consola tem problemas ao transferir ou replicar. Essa ferramenta está incluída na versão 1705 do Technical Preview. Pode encontrá-lo no servidor do site do seu site de pré-visualização técnica, depois de instalar a pré-visualização no ***\cd.latest\SMSSETUP\TOOLS*** pasta.

Pode utilizar esta ferramenta com versões de pré-visualização técnica 1606 ou posteriores. Isso para trás suporte é fornecido para que a ferramenta pode ser utilizada com cenários de atualização de um intervalo de pré-visualização técnica e sem ter de esperar até o próximo pré-visualização técnica torna-se disponível.

Pode utilizar esta ferramenta quando uma atualização na consola ainda não tiver instalada e está num Estado de falha. Estado de falha pode significar a transferir a atualização continua em curso, mas está bloqueada e demorar uma hora de excessivamente longa, talvez horas mais do que as suas expectativas históricas para pacotes de atualização de tamanho similar. Também pode ser uma falha ao replicar a atualização para sites primários subordinados.  

Quando executar a ferramenta, ele é executado em relação a atualização que especificou. Por predefinição, a ferramenta não elimina as atualizações instaladas ou transferidas com êxito.  

### <a name="prerequisites"></a>Pré-requisitos
A conta que utiliza para executar a ferramenta requer as seguintes permissões:
-   **Leia** e **escrever** permissões para a base de dados do site de administração central e cada site primário na sua hierarquia. Para definir estas permissões, pode adicionar a conta de utilizador como membro do **db_datawriter** e **db_datareader** [funções de base de dados fixas](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) no Configuration Manager base de dados de cada site. A ferramenta não interage com os sites secundários.
-   **Administrador local** no site de nível superior da sua hierarquia.
-   **Administrador local** no computador que aloja o ponto de ligação de serviço.

Terá do GUID do pacote de atualização que pretende repor. Para obter o GUID:
-   Na consola, aceda a **Administration** > **atualizações e manutenção** e, em seguida, no painel de visualização, clique no título de uma das colunas (como **estado** ), em seguida, selecione **pacote Guid**. Esta ação adiciona essa coluna para a exibição e a coluna mostra o GUID do pacote de atualização.

> [!TIP]  
> Para copiar o GUID, selecione a linha para o pacote de atualização que pretende reiniciar e, em seguida, utilize CTRL + C para copiar nessa linha. Se colar sua seleção copiada para um editor de texto, em seguida, pode copiar apenas o GUID para utilização como um parâmetro de linha de comandos ao executar a ferramenta.

### <a name="run-the-tool"></a>Execute a ferramenta    
A ferramenta tem de ser executada no site de nível superior da hierarquia.

Quando executar a ferramenta, a usar parâmetros de linha de comandos para especificar o SQL Server no site de nível superior da hierarquia, o nome de base de dados do site e o GUID do pacote de atualização que pretende repor. A ferramenta identifica, em seguida, os servidores adicionais que ela precisa acessar, com base no status de atualizações.   

Se o pacote de atualização está numa *publicar download* de estado, a ferramenta não limpe o pacote. Como opção, pode forçar a remoção de uma atualização transferida com êxito ao utilizar o parâmetro de eliminação de força (consulte parâmetros de linha de comando mais tarde deste tópico).

Depois da ferramenta é executada:
-   Se um pacote tiver sido eliminado, reinicie o serviço do SMS_Executive de sites de nível superior e, em seguida, verificar a existência de atualizações transferir o pacote novamente.
-   Se um pacote não tiver sido eliminado, não é necessário efetuar qualquer ação, como a atualização irá reinicializar e reiniciar a replicação ou a instalação.

**Parâmetros de linha de comandos:**  


|                        Parâmetro                         |                                                            Descrição                                                            |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;FQDN do SQL Server do seu site de nível superior >** | *Necessário* <br> Tem de especificar o FQDN do SQL Server que aloja a base de dados do site para o site de nível superior da sua hierarquia. |
|                **-D &lt;nome de base de dados >**                 |                             *Necessário* <br> Tem de especificar o nome da base de dados de sites de nível superior.                             |
|                 **-P &lt;GUID do pacote >**                 |                        *Necessário* <br> Tem de especificar o GUID para o pacote de atualização que pretende repor.                        |
|           **-Me &lt;nome da instância do SQL Server >**           |                   *Opcional* <br> Utilize esta opção para identificar a instância do SQL Server que aloja a base de dados do site.                   |
|                       **-FDELETE**                       |                      *Opcional* <br> Utilize esta opção para forçar a eliminação de um pacote de atualização transferido com êxito.                      |

 **Exemplos:**  
 Num cenário típico, que pretende repor uma atualização que tem problemas de transferência. É o FQDN de servidores SQL *server1.fabrikam.com*, a base de dados do site é *CM_XYZ*e o pacote GUID é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Execute: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ 61F16B3C-F1F6-4F9F-8647-2A524B0C802C -P***

 Num cenário mais extremo, pretender forçar a eliminação do pacote de atualização problemático. É o FQDN de servidores SQL *server1.fabrikam.com*, a base de dados do site é *CM_XYZ*e o pacote GUID é *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Execute: ***CMUpdateReset.exe - FDELETE -S server1.fabrikam.com -D CM_XYZ 61F16B3C-F1F6-4F9F-8647-2A524B0C802C -P***

### <a name="test-the-tool-with-the-technical-preview"></a>Testar a ferramenta com o Technical Preview  
Pode utilizar esta ferramenta com versões de pré-visualização técnica 1606 ou posteriores. Isso para trás o suporte é fornecido para que a ferramenta pode ser utilizada com um grande número de cenários de atualização de pré-visualização técnica, sem ter de esperar até que a próxima versão de pré-visualização técnica está disponível.

Execute a ferramenta num pacote de atualização de uma technical preview antes essa atualização concluir a verificação de pré-requisitos. Um Estado de verificação de pré-requisitos concluída é identificado por um dos seguintes Estados para o pacote na **Administration** > **atualizações e manutenção**:  
-   **Verificação de pré-requisito aprovada**
-   **Verificação de pré-requisito aprovada com aviso**
-   **Falha na verificação de pré-requisitos**


## <a name="high-dpi-console-support"></a>Suporte da consola DPI alta

Com esta versão, os problemas com como a consola do Configuration Manager pode ser dimensionada e apresenta diferentes partes da interface do Usuário quando visualizadas em dispositivos DPI altos (como um livro superfície) devem ser corrigidos.


## <a name="peer-cache-improvements"></a>Melhorias da Cache ponto a ponto
Começando com esta pré-visualização técnica, a Cache ponto a ponto [já não utiliza a conta de acesso de rede](/sccm/core/plan-design/hierarchy/client-peer-cache) para autenticar pedidos de transferência de colegas.


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>Melhorias para o SQL Server, grupos de disponibilidade Always On  
Com esta versão, agora, pode utilizar réplicas de consolidação assíncrona dos grupos de disponibilidade Always On do SQL Server na que utiliza com o Configuration Manager.  Isso significa que pode adicionar réplicas adicionais aos seus grupos de disponibilidade para utilizar como cópias de segurança externas (remotas) e, em seguida, utilizá-los num cenário de recuperação após desastre.  

- O Configuration Manager suporta a utilizar a réplica de consolidação assíncrona para recuperar sua réplica síncrona.  Ver [opções de recuperação de base de dados do site](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) no tópico cópia de segurança e recuperação para obter informações sobre como fazer isso.

- Esta versão não suporta a ativação pós-falha para utilizar a réplica de consolidação assíncrona como a base de dados do site.
  > [!CAUTION]  
  > Uma vez que o Configuration Manager não valida o estado da réplica de consolidação assíncrona para confirmar que é atual, e [por design, tal uma réplica pode ser sincronizada](https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes), usar de uma réplica de consolidação assíncrona, como a base de dados do site pode colocar o integridade do seu site e os dados em risco.  

- Pode utilizar o mesmo número e tipo de réplicas num grupo de disponibilidade suportada pela versão do SQL Server que utilizar.   (O suporte anterior foi limitado a duas réplicas com consolidação síncrona.)

### <a name="configure-an-asynchronous-commit-replica"></a>Configurar uma réplica de consolidação assíncrona
Adicionar uma réplica assíncrona para uma [grupo de disponibilidade que utiliza com o Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database), não é necessário executar os scripts de configuração necessários para configurar uma réplica síncrona. (Isso é porque não há suporte para utilizar essa réplica assíncrona como a base de dados do site.) Ver [documentação do SQL Server](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot)) para obter informações sobre como adicionar réplicas secundárias para grupos de disponibilidade.

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Utilizar a réplica assíncrona para recuperar o seu site
Antes de utilizar uma réplica assíncrona para recuperar a base de dados do site, tem de parar o site primário Active Directory para impedir que escritas adicionais para a base de dados do site. Depois de parar o site, pode utilizar uma réplica assíncrona em vez de utilizar um [base de dados recuperada manualmente](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption).

Para parar o site, pode utilizar o [ferramenta manutenção da hierarquia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe) parar os serviços de chave no servidor do site. Utilize a linha de comando: **Preinst.exe /stopsite**   

A parar o site é equivalente a parar o serviço de Gestor de componentes do Site (sitecomp) seguido pelo serviço do SMS_Executive, no servidor do site.

> [!TIP]  
> Se utilizar uma réplica passiva primária (introduzido desta pré-visualização técnica, como [disponibilidade elevada da função de servidor do Site](#site-server-role-high-availability)), não é necessário parar a réplica passiva. O Active Directory site primário tem de ser parado.



## <a name="improved-user-notifications-for-office-365-updates"></a>Melhorada a notificações de utilizador para atualizações do Office 365
Foram feitos aprimoramentos para aproveitar a experiência de utilizador do Office Click-to-Run, quando um cliente instala uma atualização do Office 365. Isto inclui notificações de pop-up e na aplicação e uma experiência de contagem regressiva. Antes desta versão, quando uma atualização do Office 365 foi enviada para um cliente, aplicativos do Office que foram abertos foram fechados automaticamente sem aviso. Depois desta atualização, aplicativos do Office serão já não são fechados inesperadamente.

### <a name="prerequisites"></a>Pré-requisitos
Esta atualização aplica-se aos clientes do Office 365 ProPlus.

### <a name="known-issues"></a>Problemas conhecidos
Quando um cliente avalia uma atribuição de atualização para a primeira vez e a atualização tem um prazo agendada no passado, agendado imediatamente ou agendada dentro de 30 minutos do Office 365, a experiência do usuário do Office 365 pode ser inconsistente. Por exemplo, o cliente pode receber uma caixa de diálogo de contagem decrescente de 30 minutos para a atualização, mas a imposição real foi possível iniciar antes do final da contagem regressiva. Para evitar este comportamento, considere o seguinte:
- Implemente a atualização do Office 365 com um prazo que esteja agendada para mais de 60 minutos antes da hora atual.
- Configurar uma janela de manutenção durante o horário não comercial na coleção ou configurar um período de tolerância de imposição na implementação.

### <a name="try-it-out"></a>Experimente!
Experimente concluir as seguintes tarefas e, em seguida, envie-nos **comentários** partir do **home page** separador do friso para nos informar como correu:
- Implemente um cliente de uma atualização do Office 365 com um prazo definido como um tempo, pelo menos, 60 minutos antes da hora atual. Observe o novo comportamento no cliente.


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Configurar e implementar políticas do Windows Defender Application Guard

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) é um novo recurso do Windows que ajuda a proteger os seus utilizadores ao abrir sites não confiáveis no contentor isolado seguro que não está acessível por outras partes do sistema operativo. Este technical preview, adicionámos suporte para configurar esta funcionalidade utilizando as definições de compatibilidade do Configuration Manager que configurar e, em seguida, implementar numa coleção.
Esta funcionalidade será lançada em pré-visualização para a versão de 64 bits da atualização do Windows 10 Creator (codinome: RS2). Para testar esta funcionalidade, agora, tem de utilizar uma versão de pré-visualização desta atualização.


### <a name="before-you-start"></a>Antes de começar

Para criar e implementar políticas do Windows Defender Application Guard, os dispositivos Windows 10 nos quais implementou a política tem de ser configurados com uma política de isolamento de rede. Para obter mais detalhes, consulte o blog post referenciado mais tarde.
Esta funcionalidade funciona apenas com compilações do Windows 10 Insider atuais. Para testá-lo, os clientes devem executar um recente Windows 10 Insider criar.

### <a name="try-it-out"></a>Experimente!

Certifique-se de que leu a mensagem de blogue para compreender as noções básicas sobre o Windows Defender Application Guard.

Para criar uma política e para procurar as definições disponíveis:

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade**.
2.  Na **ativos e compatibilidade** área de trabalho, escolha **descrição geral** > **Endpoint Protection** > **Windows Defender Application Guard**.
3.  Na **home page** separador a **Create** , clique em **criar política Windows Defender Application Guard**.
4.  Utilizar a mensagem de blogue como referência, pode procurar e configurar as definições disponíveis para experimentar a funcionalidade.
5.  Quando tiver terminado, conclua o assistente e implementar a política para um ou mais dispositivos do Windows 10.

### <a name="further-reading"></a>Leitura adicional

Para ler mais sobre o Windows Defender Application Guard, veja [nesta mensagem de blogue]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97).
Além disso, para saber mais sobre o modo autônomo do Windows Defender Application Guard, veja [nesta mensagem de blogue](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Novos recursos do Azure AD e gestão da cloud

Nesta versão, pode configurar os serviços cloud para utilizar o Azure AD para suportar o cenário a seguir:

- Instalar o cliente de Configuration Manager a partir da internet e tê-lo a atribuir a um site do Configuration Manager manualmente.
- Utilize o Intune para implementar o cliente do Configuration Manager para dispositivos na internet.

### <a name="advantages"></a>Vantagens

Utilizar serviços cloud e o Azure AD remove a necessidade de utilizar certificados de autenticação de cliente.

Pode detetar os utilizadores do Azure AD no seu site para utilizar em coleções e outras operações do Configuration Manager.

### <a name="before-you-start"></a>Antes de começar

- Tem de ter um inquilino do Azure AD.
- Os dispositivos tem de executar o Windows 10 e ser associados ao Azure AD.  Os clientes também podem estar associado, além disso, ao associados ao Azure AD).
- Além do [pré-requisitos existentes](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) para a função de sistema de sites do ponto de gestão, além disso verifique se **ASP.NET 4.5** (e quaisquer outras opções são automaticamente selecionadas com isso) estão ativadas no computador que aloja esta função de sistema de sites.
- Para utilizar o Microsoft Intune para implementar o cliente do Configuration Manager:
    - Tem de ter um inquilino do Intune (Configuration Manager e faça do Intune não precisam de estar ligados) em funcionamento.
    - No Intune, criar e implementar uma aplicação que contém o cliente do Configuration Manager. Para obter detalhes sobre como fazer isso, consulte como instalar clientes em dispositivos Windows geridos por MDM do Intune.
- Para utilizar o Configuration Manager para implementar o cliente:
    - Pelo menos um ponto de gestão deve ser configurado para o modo HTTPS.
    - Tem de configurar um Gateway de gestão na Cloud.


### <a name="set-up-the-cloud-management-gateway"></a>Configurar o Gateway de gestão da Cloud

Configure o Gateway de gestão da nuvem para permitir que os clientes acessem o site do Configuration Manager a partir da internet sem através de certificados.

Encontrará ajuda sobre como fazê-lo nos seguintes tópicos:

- [Planear para o gateway de gestão de nuvem no Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway).
- [Configurar o gateway de gestão na cloud para o Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway).
- [Gateway de gestão de nuvem do monitor no Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway).

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Configurar a aplicação de serviços do Azure nos serviços de nuvem do Configuration Manager

Isso se conecta seu site do Configuration Manager para o Azure AD e é um pré-requisito para todas as outras operações nesta secção. Para efetuar este procedimento:

1. Na **administração** área de trabalho da consola do Configuration Manager, expanda **serviços Cloud**e, em seguida, clique em **dos serviços do Azure**.
2. Sobre o **home page** separador a **dos serviços do Azure** , clique em **configurar os serviços do Azure**.
3. Sobre o **dos serviços do Azure** página do Assistente de serviços do Azure, selecione **gestão na Cloud** para permitir que os clientes para se autenticar com a hierarquia com o Azure AD.
4. Sobre o **gerais** página do assistente, especifique um nome e uma descrição para o seu serviço do Azure.
5. Sobre o **App** página do assistente, selecione o seu ambiente do Azure na lista, em seguida, clique em **procurar** para selecionar as aplicações de servidor e cliente que serão utilizadas para configurar o serviço do Azure:
   - Na **aplicação de servidor** janela, selecione a aplicação de servidor que pretende utilizar e clique em **OK**. As aplicações de servidor são as aplicações web do Azure que contêm as configurações para a sua conta do Azure, incluindo o ID de inquilino, ID de cliente e uma chave secreta para clientes. Se não tiver uma aplicação de servidor disponíveis, utilize um dos seguintes:
       - **criar**: Para criar uma nova aplicação de servidor, clique em **criar**. Forneça um nome amigável para a aplicação e o inquilino. Em seguida, depois que iniciar sessão para o Azure, o Configuration Manager cria a aplicação web no Azure para si, incluindo o ID de cliente e a chave secreta para utilização com a aplicação web. Mais tarde, pode visualizá-las no portal do Azure.
       - **Importar**: Para utilizar uma aplicação web que já existe na sua subscrição do Azure, clique em **importação**. Forneça um nome amigável para a aplicação e o inquilino e, em seguida, especifique o ID de inquilino, ID de cliente e a chave secreta da aplicação web do Azure que pretende que o Configuration Manager para utilizar. Depois de verificar as informações, clique em **OK** para continuar. Este opton não está atualmente disponível neste technical Preview.
   - Repita o mesmo processo para a aplicação de cliente.

   Tem de conceder a *ler dados do diretório* permissão da aplicação ao utilizar a importação de aplicativo, para definir as permissões corretas no portal do. Se usar a criação da aplicação as permissões são criadas automaticamente com o aplicativo, mas ainda precisa de dar consentimento para a aplicação no portal do Azure.
6. Sobre o **deteção** página do assistente, opcionalmente **ativar o Azure Active Directory deteção de utilizadores do**e, em seguida, clique em **definições**.
   Na **definições de deteção de utilizador do Azure AD** diálogo caixa, configure uma agenda para quando ocorre a deteção. Também pode ativar a deteção de diferenças que verifica a existência de apenas novas ou alteradas contas no Azure AD.
7. Conclua o assistente.

Neste momento, ligou-se o site do Configuration Manager para o Azure AD.


### <a name="install-the-cm-client-from-the-internet"></a>Instalar o cliente CM a partir da Internet

Antes de começar, certifique-se de que os ficheiros de origem de instalação de cliente são armazenados localmente no dispositivo para o qual pretende instalar o cliente.
Em seguida, utilize as instruções em [como implementar clientes em computadores do Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) utilizando a seguinte linha de comando de instalação (substitua os valores no exemplo pelos seus próprios valores):

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode = HEC AADTENANTID = 780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME = contoso AADCLIENTAPPID =<GUID> AADRESOURCEURI =<https://contososerver>**

- **/ NoCrlCheck**: Se a gestão de ponto ou na cloud gateway de gestão utiliza um certificado de servidor não pública, em seguida, o cliente poderá não ser capaz de alcançar a localização da CRL.
- **/ Origem**: Pasta local:   Localização dos ficheiros de instalação de cliente.
- **CCMHOSTNAME**: O nome do seu ponto de gestão de Internet. Pode encontrá-lo, executando **gwmi – namespace root\ccm\locationservices-classe SMS_ActiveMPCandidate** num prompt de comando num cliente gerenciado.
- **SMSMP**: O nome do seu ponto de gestão de pesquisa – isso pode ser na sua intranet.
- **SMSSiteCode**: O código do site do seu site do Configuration Manager.
- **AADTENANTID**, **AADTENANTNAME**: O ID e nome do inquilino do Azure AD é vinculado ao Configuration Manager. Pode encontrar isto executando dsregcmd.exe /status numa linha de comandos num Azure AD associado a um dispositivo.
- **AADCLIENTAPPID**: O ID de aplicação de cliente do Azure AD. Para ajudar a encontrar isto, consulte [utilize o portal para criar um Azure Active Directory principal de aplicações e serviço que pode aceder a recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri**: O identificador URI da aplicação de servidor integrado do Azure AD.

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>Utilize o Assistente de serviços do Azure para configurar uma ligação para o OMS
A partir da versão de pré-visualização técnica 1705, utilizar o **Assistente de serviços do Azure** para configurar a ligação do Configuration Manager para o serviço de nuvem do Operations Management Suite (OMS). O assistente substitui os fluxos de trabalho anteriores para configurar esta ligação.

-   O assistente é utilizado para configurar os serviços de cloud para o Configuration Manager, como o OMS, Windows Store para empresas (WSfB) e o Azure Active Directory (Azure AD).  

-   O Configuration Manager liga-se para o OMS para funcionalidades como [do Log Analytics](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite), ou [preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics).

### <a name="prerequisites-for-the-oms-connector"></a>Pré-requisitos para o conector do OMS
Pré-requisitos para configurar uma ligação para o OMS são iguais às [documentada para a versão do Current Branch 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites). Essas informações são repetidas aqui:  

-   Fornecer permissão de Gestor de configuração para OMS.

-   O conector do OMS tem de estar instalado no computador que aloja uma [ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) que está na [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

-   Tem de instalar um agente de monitorização da Microsoft para o OMS instalado no ponto de ligação de serviço, juntamente com o conector do OMS. O agente e o conector do OMS devem ser configurados para utilizar o mesmo **área de trabalho OMS**. Para instalar o agente, consulte [transfira e instale o agente](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) na documentação do OMS.
-   Depois de instalar o conector e o agente, tem de configurar o OMS para utilizar dados do Configuration Manager. Para tal, no Portal do OMS [coleções do Gestor de configuração da importação](/azure/log-analytics/log-analytics-sccm#import-collections).

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Utilize o Assistente de serviços do Azure para configurar a ligação para o OMS

1.  Na consola, aceda a **Administration** > **descrição geral** > **serviços Cloud** > **osserviçosdoAzure**e, em seguida, escolha **configurar os serviços do Azure** da **home page** separador do Friso, para iniciar o **Assistente de serviços do Azure**.

2.  Sobre o **dos serviços do Azure** , selecione o serviço em nuvem do Operation Management Suite. Forneça um nome amigável para o **nome do serviço do Azure** e uma descrição opcional e, em seguida, clique em **próxima**.

3.  Sobre o **aplicação** , especifique o seu ambiente do Azure (technical preview oferece suporte apenas a Cloud pública). Em seguida, clique em **procurar** para abrir a janela de aplicação de servidor.

4.  Selecione uma aplicação web:

    -   **Importar**: Para utilizar uma aplicação web que já existe na sua subscrição do Azure, clique em **importação**. Forneça um nome amigável para a aplicação e o inquilino e, em seguida, especifique o ID de inquilino, ID de cliente e a chave secreta da aplicação web do Azure que pretende que o Configuration Manager para utilizar. Depois de **Verifique se** as informações, clique em **OK** para continuar.   

    > [!NOTE]   
    > Quando configurar o OMS com esta pré-visualização, o OMS suporta apenas a *importar* função para uma aplicação web. Criar uma nova aplicação web não é suportado. Da mesma forma, não é possível reutilizar uma aplicação existente para o OMS.

5.  Se fizemos todos os outros procedimentos com êxito, em seguida, as informações sobre o **configuração da ligação OMS** ecrã aparece automaticamente nesta página. Informações para as definições de ligação devem ser apresentado em sua **subscrição do Azure**, **grupo de recursos do Azure**, e **área de trabalho do Operations Management Suite**.

6.  O assistente liga ao serviço do OMS utilizando as informações que tenha de entrada. Selecione as coleções de dispositivos que pretende sincronizar com o OMS e, em seguida, clique em **adicionar**.

7.  Verifique as definições de ligação no **resumo** ecrã, em seguida, selecione **próxima**. O **progresso** ecrã mostra o estado da ligação, em seguida, deve **concluída**.

8.  Depois de concluir o assistente, a consola do Configuration Manager mostra que configurou **Operation Management Suite** como um **tipo de serviço de nuvem**.

---
title: Implementar clientes em Windows
titleSuffix: Configuration Manager
description: Saiba como implementar o cliente do Configuration Manager em computadores Windows.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 639521ecf0084b40bf61ac3d635ab4f5e55d1321
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123850"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-configuration-manager"></a>Como implementar clientes em computadores Windows no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo fornece detalhes sobre como implementar o cliente do Configuration Manager em computadores Windows. Para obter mais informações sobre como planejar e preparar a implementação de cliente, consulte os artigos seguintes:
- [Métodos de instalação de cliente](/sccm/core/clients/deploy/plan/client-installation-methods)  
- [Pré-requisitos para implementar clientes em computadores Windows](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers)   
- [Segurança e privacidade para clientes do Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  
- [Melhores práticas para a implementação do cliente](/sccm/core/clients/deploy/plan/best-practices-for-client-deployment)  



##  <a name="BKMK_ClientPush"></a> Instalação push do cliente 

Existem três formas principais para utilizar o push de cliente:  

- Quando configura a instalação push do cliente para um site, a instalação do cliente é executada automaticamente em computadores que Deteta o site. Este método tem como escopo dos limites configurados do site quando esses limites estejam configurados como um grupo de limites.  

- Inicie a instalação push do cliente ao executar o Assistente de instalação de Push de cliente para uma coleção ou recurso específico dentro de uma coleção.  

- Utilize o Assistente de instalação Push do cliente para instalar o cliente do Configuration Manager [consulta](/sccm/core/servers/manage/queries-technical-reference) resultados. Para instalação com êxito, um dos itens devolvidos pela consulta tem de ser o **ResourceID** atributo da **recurso do sistema** classe.   

Se o servidor do site não é possível contactar o computador cliente ou iniciar o processo de configuração, repetirá automaticamente a cada hora de instalação. O servidor continuará a tentar até sete dias.  

Para ajudar a controlar o processo de instalação do cliente, instale um ponto de estado de contingência antes de instalar os clientes. Quando instala um ponto de estado de contingência, este será automaticamente atribuído aos clientes quando são instaladas pelo método de instalação push do cliente. Para controlar o progresso da instalação de cliente, ver os relatórios de implementação e a atribuição de cliente. 

Ficheiros de registo do cliente fornecem informações mais detalhadas para resolução de problemas. Os ficheiros de registo não necessitam de um ponto de estado de contingência. Por exemplo, o **CCM** ficheiro no servidor do site regista eventuais problemas do servidor do site quando ligar ao computador. O **Ccmsetup** ficheiro log no cliente regista o processo de instalação.  

> [!IMPORTANT]  
>  Para instalação push do cliente tenha êxito, certifique-se de que todos os pré-requisitos são cumpridos. Para obter mais informações, consulte [dependências do método de instalação](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#installation-method-dependencies).  


### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Configurar o site para utilizar automaticamente a instalação push do cliente para computadores detetados

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó.  

2.  Selecione o site para o qual pretende configurar a instalação push automática do cliente em todo o site.  

3.  Na **home page** separador do Friso, no **definições** de grupo, selecione **definições de instalação de cliente**e selecione **instalação Push do cliente**.  

4.  Sobre o **gerais** separador da janela de propriedades de instalação Push do cliente, selecione **ativar a instalação push automática do cliente em todo o site**.   

5. A partir da versão 1806, quando atualizar o site, permite que uma verificação de Kerberos para instalação push do cliente. A opção para **permitir a conexão fallback para NTLM** está ativada por predefinição, o que é consistente com o comportamento anterior. Se o site não é possível autenticar o cliente utilizando o Kerberos, tentar novamente a ligação utilizando o NTLM. A configuração recomendada para obter mais segurança é desativar esta definição, o que necessita de Kerberos sem NTLM contingência.<!--1358204-->  

    > [!Note]  
    > Ao utilizar o push de cliente para instalar o cliente do Configuration Manager, o servidor do site cria uma ligação remota para o cliente. A partir da versão 1806, o site pode exigir a autenticação mútua do Kerberos, não permitindo fallback para NTLM antes de estabelecer a ligação. Esta melhoria ajuda a proteger a comunicação entre o servidor e o cliente.  
    > 
    > Consoante as políticas de segurança, o seu ambiente já pode preferir ou requerem Kerberos através de autenticação de NTLM mais antiga. Para obter mais informações sobre as considerações de segurança, os protocolos de autenticação, consulte a [definição de política de segurança de Windows para restringir NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).  
    > 
    > Para utilizar esta funcionalidade, os clientes devem ser numa floresta do Active Directory fidedigna. Kerberos no Windows depende do Active Directory para autenticação mútua.  

6.  Selecione os tipos de sistema para o qual o Configuration Manager deve enviar por push o software de cliente. Selecione se pretende instalar o cliente em controladores de domínio.  

7.  Sobre o **contas** separador, especifique uma ou mais contas do Configuration Manager para utilizar quando se liga ao computador de destino. Clique nas **Create** ícone, introduza o **nome de utilizador** e **palavra-passe** (não mais de 38 caracteres), confirme a palavra-passe e, em seguida, clique em **OK** . Especifique a conta de instalação de push, pelo menos, um cliente. Esta conta tem de ter direitos de administrador local no computador de destino para instalar o cliente. Se não especificar uma conta de instalação push do cliente, o Configuration Manager tenta utilizar a conta de computador do sistema de sites. Instalação push do cliente entre domínios falhe ao utilizar a conta de computador do sistema de sites.  

    > [!NOTE]  
    >  Para utilizar o push de cliente a partir de um site secundário, especifique a conta no site secundário que inicia a instalação push do cliente.  
    >   
    >  Para obter mais informações sobre a conta de instalação push do cliente, consulte o procedimento seguinte, [utilizar o Assistente de instalação de Push de cliente](#use-the-client-push-installation-wizard).  

8.  Concluir o **das propriedades de instalação** separador.

     Se tiver expandido o esquema do Active Directory para o Configuration Manager, o site publica a especificado [das propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties) serviços de domínio do Active Directory. Quando o CCMSetup é executado sem propriedades de instalação, ele lê essas propriedades do Active Directory.  

    > [!NOTE]  
    >  Se ativar instalação push do cliente num site secundário, definir o **SMSSITECODE** propriedade para o código do site do Configuration Manager do respetivo site primário principal. Se tiver expandido o esquema do Active Directory para o Configuration Manager, para localizar automaticamente a atribuição de site correto, defina esta propriedade como **automática**.  


### <a name="use-the-client-push-installation-wizard"></a>Utilizar o Assistente de instalação de push de cliente

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó.  

2.  Selecione o site para o qual pretende configurar a instalação push automática do cliente em todo o site.  

3.  Na **home page** separador do Friso, no **definições** de grupo, selecione **definições de instalação de cliente**e selecione **instalação Push do cliente**.  

4.  Concluir o **das propriedades de instalação** separador.  

    Se tiver expandido o esquema do Active Directory para o Configuration Manager, o site publica a especificado [das propriedades de instalação de cliente](/sccm/core/clients/deploy/about-client-installation-properties) serviços de domínio do Active Directory. Quando o CCMSetup é executado sem propriedades de instalação, ele lê essas propriedades do Active Directory.   

5.  Na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho.  

6.  Na **dispositivos** nó, selecione um ou mais computadores. Ou selecione uma coleção de computadores a **coleções de dispositivos** nó.  

7.  Sobre o **home page** separador do Friso, selecione uma das seguintes opções:  

    -   Para enviar por push do cliente para um ou mais dispositivos, além da **dispositivo** de grupo, escolha **instalar cliente**.  

    -   Para enviar por push do cliente para uma coleção de dispositivos, além da **coleção** de grupo, escolha **instalar cliente**.  

8. Sobre o **antes de começar** página do Assistente para instalar o cliente, reveja as informações e, em seguida, escolha **próxima**.  

9. Concluir o **opções de instalação** página.  

10. Reveja as definições de instalação e, em seguida, conclua o assistente.  

> [!NOTE]  
> Utilize este assistente para instalar clientes, mesmo que o site não está configurado para a instalação push do cliente.  



##  <a name="BKMK_ClientSUP"></a> Instalação baseada em atualização de software  

Instalação de cliente baseada em atualização de software publica o cliente para um ponto de atualização de software como uma atualização de software. Utilize este método para uma primeira instalação ou atualização.  

Se um computador tiver o cliente do Configuration Manager instalado, ele recebe a política de cliente do site. Esta política inclui o nome do servidor de ponto de atualização de software e a porta da qual obter atualizações de software.   

> [!IMPORTANT]  
>  Para a instalação baseada em atualização de software, utilize o mesmo servidor do Windows Server Update Services (WSUS) para a instalação de cliente e atualizações de software. Este servidor deverá ser o ponto de atualização de software ativo num site primário. Para obter mais informações, consulte [instale um ponto de atualização de software](/sccm/sum/get-started/install-a-software-update-point).  

Se um computador não tiver o cliente do Configuration Manager instalado, configurar e atribuir um objeto de política de grupo. Esta política de grupo Especifica o nome do servidor de ponto de atualização de software.  

Não é possível adicionar propriedades de linha de comandos para uma instalação de cliente baseada em atualização de software. Se tiver expandido o esquema do Active Directory para o Configuration Manager, o cliente instalar automaticamente consultas de serviços de domínio do Active Directory para as propriedades de instalação.  

Se ainda não tiver expandido o esquema do Active Directory, utilize a política de grupo para aprovisionar definições de instalação de cliente. Estas definições são aplicadas automaticamente para qualquer instalação de cliente baseada em atualização de software. Para obter mais informações, consulte a secção sobre [como aprovisionar as propriedades de instalação de cliente](#BKMK_Provision) e o artigo sobre [como atribuir clientes a um site](/sccm/core/clients/deploy/assign-clients-to-a-site).  

Utilize os procedimentos seguintes para configurar computadores sem um cliente de Configuration Manager para utilizar o ponto de atualização de software. Também é um procedimento para publicar o software de cliente para o ponto de atualização de software.  

> [!Tip]  
>  Se os computadores estiverem num Estado de reinício pendente depois de uma instalação de software, em seguida, uma instalação de cliente baseada em atualização de software pode fazer com que o computador seja reiniciado.  


### <a name="configure-a-group-policy-object-to-specify-the-software-update-point"></a>Configurar um objeto de política de grupo para especificar o ponto de atualização de software  

1.  Utilize o **consola de gestão de políticas de grupo** para abrir um objeto de política de grupo novo ou existente.  

2.  Expanda **configuração do computador**, expanda **modelos administrativos**, expanda **componentes do Windows**e, em seguida, escolha **Windows Update**.  

3.  Abra as propriedades da definição **especificar a localização de serviço de atualização de Microsoft na intranet**e, em seguida, escolha **ativado**.  

4.  **Definir o serviço de atualização de intranet para detetar atualizações**: Especifique o nome e a porta do servidor de ponto de atualização de software.  

    -   Se tiver configurado o sistema de sites do Configuration Manager para utilizar um nome de domínio completamente qualificado (FQDN), utilize este formato.  

    -   Se o sistema de sites do Configuration Manager não está configurado para utilizar um FQDN, utilize um formato de nome abreviado.   

    > [!Tip]  
    >  Para determinar o número de porta, consulte [como determinar as definições de porta utilizadas pelo WSUS](/sccm/sum/plan-design/plan-for-software-updates).  

     Exemplo com o formato FQDN: `http://server1.contoso.com:8530`  

5.  **Definir o servidor de estatísticas de intranet**: Esta definição é normalmente o mesmo nome de servidor.   

6.  Atribua o objeto de diretiva de grupo para os computadores nos quais pretende instalar o cliente e receber atualizações de software.  


### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>Publicar o cliente do Configuration Manager para o ponto de atualização de software  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó.  

2.  Selecione o site para o qual pretende configurar a instalação de cliente baseada em atualização de software.  

3.  No **home page** separador do Friso, na **definições** de grupo, selecione **definições de instalação de cliente**e, em seguida, escolha **baseada cliente Instalação**.  

4.  Selecione **ativar a instalação de cliente baseada em atualização de software**.  

5.  Se a versão do cliente do site é mais recente do que a versão no ponto de atualização de software, o **detetada versão posterior do cliente pacote** é aberta a caixa de diálogo. Clique em **Sim** para publicar a versão mais recente.  

    > [!NOTE]  
    >  Se já não tiver publicado o software de cliente para o ponto de atualização de software, esta caixa está em branco.  

A atualização de software para o cliente do Configuration Manager não é atualizada automaticamente quando há uma nova versão. Quando atualizar o site, repita este procedimento para atualizar o cliente.  



##  <a name="BKMK_ClientGP"></a> Instalação de política de grupo 

Utilize a política de grupo nos serviços de domínio do Active Directory para publicar ou atribuir o cliente do Configuration Manager. O cliente é instalado quando o computador é iniciado. Ao usar a diretiva de grupo, o cliente será apresentado no **adicionar ou remover programas** painel de controlo para o utilizador instalar.  

Utilizar o pacote do Windows Installer **Ccmsetup** para instalações baseadas em políticas de grupo. Este ficheiro está localizado na pasta `<ConfigMgr installation directory>\bin\i386` no servidor do site. Não é possível adicionar propriedades a este ficheiro para modificar o comportamento de instalação.  

> [!IMPORTANT]  
>  Tem de ter **administrador** permissões para aceder os ficheiros de instalação do cliente.  

-   Se tiver expandido o esquema do Active Directory para o Configuration Manager e tiver selecionado **publicar este site nos serviços de domínio do Active Directory** no **avançadas** separador do **Site Propriedades** caixa de diálogo, computadores cliente procuram automaticamente os serviços de domínio do Active Directory para as propriedades de instalação. Para obter mais informações, consulte [acerca das propriedades de instalação de cliente publicadas no Active Directory Domain Services](/sccm/core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services).  

-   Se ainda não tiver expandido o esquema do Active Directory, para armazenar propriedades de instalação no registo do Windows de computadores, consulte a secção sobre [como aprovisionar as propriedades de instalação de cliente](#BKMK_Provision). O cliente utiliza estas propriedades de instalação quando ele é instalado.  

Para obter mais informações sobre como utilizar a política de grupo no Active Directory Domain Services para instalar software, consulte [como utilizar a política de grupo para instalar remotamente o software](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server).  



##  <a name="BKMK_Manual"></a> Instalação manual

Instalar manualmente o software de cliente em computadores utilizando **CCMSetup.exe**. Encontrar este programa e os respetivos ficheiros de suporte no **cliente** pasta da pasta de instalação do Configuration Manager no servidor do site. O site compartilha esta pasta na rede como:  

 `\\<Site Server Name>\SMS_<Site Code>\Client\`  

 em que `<Site Server Name>` é o nome de servidor do site primário, e `<Site Code>` é o código de site primário ao qual o cliente é atribuído. Para executar CCMSetup.exe a partir da linha de comandos no cliente, ligar a esta localização de rede e, em seguida, execute o comando.  

> [!IMPORTANT]  
>  Tem de ter **administrador** permissões para aceder os ficheiros de instalação do cliente.  

CCMSetup.exe copia todos os pré-requisitos necessários para o computador cliente e chama o pacote do Windows Installer (Client. msi) para instalar o cliente. Não é possível executar Client. msi diretamente.  

Para modificar o comportamento da instalação do cliente, especifique as opções de linha de comandos para CCMSetup.exe e Client. msi. Certifique-se de que especifica os parâmetros CCMSetup que começam com `/` antes de o especificar propriedades de Client. msi. Por exemplo:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`    

Instala o cliente neste exemplo, utilizando as seguintes opções:  

|Opção|Descrição|  
|--------------|-----------------|  
|`/mp:SMSMP01`|Este parâmetro de CCMSetup Especifica o ponto de gestão SMSMP01 para transferir os ficheiros de instalação de cliente necessários.|  
|`/logon`|Este parâmetro de CCMSetup Especifica que a instalação deverá ser interrompida se não for encontrado um cliente existente do Configuration Manager no computador.|  
|`SMSSITECODE=AUTO`|Esta propriedade de Client. msi Especifica que o cliente tenta localizar o código do site do Configuration Manager para utilizar. Por exemplo, ao utilizar serviços de domínio do Active Directory.|  
|`FSP=SMSFP01`|Esta propriedade de Client. msi Especifica que o ponto de estado de contingência com o nome SMSFP01 é utilizado para receber mensagens de estado enviadas pelo computador cliente.|  

 Para obter mais informações, consulte [sobre parâmetros de instalação de cliente e as propriedades](/sccm/core/clients/deploy/about-client-installation-properties).  

> [!Tip]  
> Para o procedimento para instalar o cliente do Configuration Manager num dispositivo Windows 10 moderno com a identidade do Azure AD, consulte [instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Esse procedimento é para os clientes na intranet ou na internet.  


### <a name="manual-installation-examples"></a>Exemplos de instalação manual

Esses exemplos destinam-se a clientes associados ao Active Directory na intranet. Utilizam os seguintes valores:  

- **MPSERVER**: servidor que aloja o ponto de gestão   
- **FSPSERVER**: servidor que aloja o ponto de estado de contingência  
- **ABC**: código do site  
- **contoso.com**: nome de domínio  

Configurar todos os servidores de sistema de sites com um FQDN de intranet. Publicar as informações do site para o Active Directory.  

Comece com os passos seguintes no computador cliente:  
1. Inicie sessão como um administrador local  
2. Mapear a unidade z para `\\MPSERVER\SMS_ABC\Client`  
3. Altere a linha de comandos para a unidade z:  

Em seguida, execute um dos seguintes comandos:  


#### <a name="manual-example-1"></a>Exemplo 1 do manual  

`CCMSetup.exe`  

Neste exemplo instala o cliente sem parâmetros adicionais ou propriedades. O cliente configura automaticamente com as propriedades de instalação de cliente publicadas no Active Directory Domain Services, incluindo as seguintes definições:  

- Código do site: Essa configuração requer a localização de rede do cliente a serem incluídos num grupo de limites que tenha configurado para atribuição de cliente.  
- Ponto de gestão
- Ponto de estado de contingência
- Comunicar através de HTTPS apenas  

Para obter mais informações, consulte [acerca das propriedades de instalação de cliente publicadas no Active Directory Domain Services](/sccm/core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services).  


#### <a name="manual-example-2"></a>Exemplo 2 do manual  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
Este exemplo substitui a configuração automática que fornece serviços de domínio do Active Directory. Ele não requer que a localização de rede do cliente está incluída no grupo de limites configurado para atribuição de cliente. Em vez disso, a instalação Especifica as seguintes definições:
- Código do site
- Ponto de gestão de intranet 
- Ponto de gestão baseado na Internet
- Ponto de estado de contingência que aceita ligações da internet
- Utilize um certificado PKI (se disponível) do cliente que tenha o período de validade mais longo  



##  <a name="BKMK_ClientLogonScript"></a> Instalação de script de início de sessão

O Configuration Manager suporta scripts de logon para instalar o software de cliente do Configuration Manager. Utilize o ficheiro de programa **CCMSetup.exe** num script de início de sessão para acionar a instalação de cliente.  

A instalação com script de início de sessão utiliza os mesmos métodos da instalação manual de cliente. Especifique o `/logon` parâmetro de instalação para CCMSsetup.exe. Se já existir uma versão do cliente no computador, este parâmetro impede que o cliente instalem. Este comportamento impede a reinstalação do cliente sempre que o script de início de sessão for executada.  

Se não especificar uma origem de instalação, o `/Source` parâmetro e nenhum ponto de gestão a partir da qual obter a instalação é especificada pelo `/MP` parâmetro, CCMSetup.exe localiza o ponto de gestão ao pesquisar o domínio do Active Directory Serviços. Este comportamento ocorre apenas se tiver expandido o esquema para o Configuration Manager e publicar o site de serviços de domínio do Active Directory. Em alternativa, o cliente pode utilizar DNS ou WINS para localizar um ponto de gestão.  



##  <a name="BKMK_ClientApp"></a> Instalação de pacote e programa  

Utilize o Gestor de configuração para criar e implementar um pacote e um programa que atualiza o software de cliente para dispositivos selecionados. O Configuration Manager fornece um ficheiro de definição de pacote que povoa as propriedades do pacote com valores normalmente utilizados. Personalize o comportamento da instalação do cliente especificando propriedades e os parâmetros da linha de comandos adicionais.  

> [!NOTE]  
>  Não é possível atualizar clientes do Configuration Manager 2007 com este método. Em vez disso, utilize a atualização automática de cliente, que cria e implementa automaticamente um pacote com a versão mais recente do cliente. Para obter mais informações, consulte [atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients).  
>   
>  Para obter mais informações sobre como migrar de versões mais antigas do cliente do Configuration Manager, consulte [planear uma estratégia de migração de clientes](/sccm/core/migration/planning-a-client-migration-strategy).  

 
### <a name="create-a-package-and-program-for-the-client-software"></a>Criar um pacote e programa para o software de cliente  

Utilize o procedimento seguinte para criar um pacote do Configuration Manager e o programa que pode implementar em computadores de cliente do Configuration Manager para atualizar o software de cliente.  

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**e selecione o **pacotes** nó.  

2.  No **home page** separador do Friso, no **Create** de grupo, selecione **criar pacote de definição**.  

3.  Sobre o **definição de pacote** página do assistente, selecione **Microsoft** do **publicador** na lista pendente e selecione **cliente do Configuration Manager Atualizar** partir de **definição do pacote** lista.  

4.  Sobre o **ficheiros de origem** página, selecione **obter sempre ficheiros da pasta de origem**.  

5.  Sobre o **pasta de origem** página, selecione **caminho de rede (nome UNC)**. Em seguida, introduza o caminho de rede para o servidor e a partilha que contém os ficheiros de instalação do cliente.  

    > [!NOTE]  
    >  O computador em que é executado a implementação do Configuration Manager tem de ter acesso à pasta de rede especificado. Caso contrário, a instalação de cliente falhar.  

    Para alterar qualquer uma das propriedades de instalação do cliente, modifique a linha de comandos CCMSetup.exe no **gerais** separador da **atualização silenciosa do agente do Configuration Manager propriedades** caixa de diálogo do programa. As propriedades de instalação predefinidas são `/noservice SMSSITECODE=AUTO`.  

6. Distribua o pacote por todos os pontos de distribuição que pretende que alojem o pacote de atualização de cliente. Em seguida, implemente o pacote para coleções de dispositivos que contêm clientes que pretende atualizar.  



## <a name="bkmk_mdm"></a> Dispositivos geridos pelo Intune MDM do Windows

Implemente o cliente do Configuration Manager em dispositivos que estão inscritos no Microsoft Intune. 

Este procedimento destina-se um cliente tradicional que está ligado à intranet. Ele usa os métodos de autenticação de cliente tradicionais. Para garantir que o dispositivo permanece no estado de gerido após a instalação do cliente, tem de ser na intranet e num limite de site do Configuration Manager.  

Para o procedimento para instalar o cliente do Configuration Manager num dispositivo Windows 10 moderno com a identidade do Azure AD, consulte [instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

> [!NOTE]  
> Por predefinição, depois de instalar o software de cliente, o dispositivo anular a inscrição no Intune.
> 
> A partir da versão 1710, os clientes não anular a inscrição do Intune. Eles podem ter o cliente do Configuration Manager e a inscrição de MDM ao mesmo tempo. Para obter mais informações, consulte [descrição geral de cogestão](/sccm/comanage/overview).  


###  <a name="install-clients-with-intune"></a>Instalar clientes com o Intune  

1. No Intune, [adicionar uma aplicação de linha de negócio do Windows](https://docs.microsoft.com/intune/lob-apps-windows) que contém o ficheiro de instalação de cliente do Configuration Manager **ccmsetup**. Este ficheiro está localizado na seguinte pasta no servidor do site: `<ConfigMgr installation directory>\bin\i386`  

2. No Intune Software Publisher, introduza os parâmetros da linha de comandos. Por exemplo, utilize a seguinte linha de comando com um cliente tradicional na intranet:  

   `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<Your site code> DNSSUFFIX=<DNS Suffix of management point>"`  

   > [!Note]  
   > Para uma linha de comando de exemplo utilizar com um cliente moderno do Windows 10 através da autenticação do Azure AD, consulte [como preparar os dispositivos baseados na internet para a cogestão](/sccm/comanage/how-to-prepare-win10#install-the-configuration-manager-client).  

3. [Atribuir a aplicação](https://docs.microsoft.com/intune/deploy-use/deploy-apps-in-microsoft-intune) a um grupo de computadores Windows inscritos.  



##  <a name="BKMK_ClientImage"></a> Instalação de imagem do SO

O cliente do Configuration Manager num computador de referência que utilizou para criar uma imagem de sistema operacional de pré-instalação.   

> [!Important]  
> Ao usar a sequência de tarefas do Configuration Manager para implantar a imagem do SO, o [Prepare ConfigMgr Client](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) passo de sequência de tarefas remove completamente o cliente do Configuration Manager.  


### <a name="prepare-the-client-computer-for-imaging"></a>Preparar o computador cliente para criação de imagens  

1.  Instale manualmente o software de cliente do Configuration Manager no computador de referência. Para obter mais informações, consulte [como instalar manualmente clientes do Configuration Manager](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Não especifique um código de site do Configuration Manager para o cliente nas propriedades da linha de comandos CCMSetup.exe.  

2.  No prompt de comando, digite `net stop ccmexec` para parar o **SMS Agent Host** service (Ccmexec.exe) no computador de referência.  

3.  Eliminar o ficheiro **SMSCFG. INI** partir de **Windows** pasta no computador de referência.  

4.  Remova quaisquer certificados que estão armazenados no arquivo do computador local no computador de referência. Por exemplo, se utilizar certificados de infraestrutura de chaves públicas (PKI), antes de criar a imagem do computador, remover os certificados no **pessoais** armazenar **computador** e **utilizador**.  

5.  Se os clientes estiverem instalados numa hierarquia do Configuration Manager diferente do que o computador de referência, remova a chave de raiz fidedigna do computador de referência.  

    > [!NOTE]  
    >  Se os clientes não conseguirem consultar os serviços de domínio do Active Directory para localizar um ponto de gestão, eles usam a chave de raiz fidedigna para determinar os pontos de gestão fidedigno. Se implantar a imagem de todos os clientes na mesma hierarquia do computador principal, deixe a chave de raiz fidedigna no local. 
    > 
    > Se implementar clientes em hierarquias diferentes, remova a chave de raiz fidedigna. Aprovisione também estes clientes com a nova chave de raiz fidedigna. Para obter mais informações, consulte [planear a chave de raiz fidedigna](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK).  

6.  Utilize o software de geração de imagens para capturar uma imagem de computador de referência.  

7.  Implemente a imagem nos computadores de destino.  



##  <a name="BKMK_ClientWorkgroup"></a> Computadores de grupo de trabalho  

O Configuration Manager suporta a instalação de cliente para computadores em grupos de trabalho. Instalar o cliente em computadores de grupo de trabalho usando o método especificado em [como instalar manualmente clientes do Configuration Manager](#BKMK_Manual).  


### <a name="prerequisites"></a>Pré-requisitos  

-   Instale manualmente o cliente em cada computador do grupo de trabalho. Durante a instalação, o usuário interativo tem de ter direitos de administrador local.  

-   Para acessar recursos no domínio do servidor de site do Configuration Manager, configure a conta de acesso de rede para o site. Especifica esta conta no componente de site de distribuição de software. Para obter mais informações, consulte [componentes do Site](/sccm/core/servers/deploy/configure/site-components).  


### <a name="limitations"></a>Limitações  

-   Os clientes do grupo de trabalho não é possível localizar pontos de gestão de serviços de domínio do Active Directory. Em vez disso utilizar DNS, WINS ou outro ponto de gestão.  

-   Não é suportado global roaming. Os clientes do grupo de trabalho não é possível consultar os serviços de domínio do Active Directory para informações de site.  

-   Métodos de deteção do Active Directory não conseguem detetar computadores em grupos de trabalho.  

-   Não é possível implementar software para os utilizadores de computadores do grupo de trabalho.  

-   Não é possível utilizar o método de instalação push do cliente para instalar o cliente em computadores de grupo de trabalho.  

-   Os clientes do grupo de trabalho não é possível utilizar o Kerberos para autenticação e podem exigir a aprovação manual.  

-   Não é possível configurar um cliente de grupo de trabalho como um ponto de distribuição. O Configuration Manager requer que ponto de distribuição computadores sejam membros de um domínio.  


### <a name="install-the-client-on-workgroup-computers"></a>Instalar o cliente em computadores de grupo de trabalho  

Verifique os pré-requisitos, em seguida, siga as instruções na secção [como instalar manualmente clientes do Configuration Manager](#BKMK_Manual).  


#### <a name="workgroup-example-1"></a>Exemplo de grupo de trabalho 1

Este exemplo faz as seguintes ações: 
- Instala o cliente para gestão de clientes da intranet
- Especifica o código do site 
- Especifica o sufixo DNS para localizar um ponto de gestão  

   `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

     
#### <a name="workgroup-example-2"></a>Grupo de trabalho exemplo 2

Este exemplo requer o cliente se encontre numa localização de rede que está configurada num grupo de limites. Este requisito destina-se a atribuição automática de sites seja bem-sucedida. O comando inclui um ponto de estado de contingência num servidor FSPSERVER. Esta propriedade ajuda a controlar a implementação do cliente e identificar qualquer comunicação com o cliente emite. 

   `CCMSetup.exe FSP=fspserver.constoso.com`  

      

##  <a name="BKMK_ClientInternet"></a> Gestão de clientes baseados na Internet  
 
> [!Note]  
> Esta secção não se aplica a clientes com uma [gateway de gestão da nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Para instalar os clientes baseados na internet através de um gateway de gestão na cloud, veja [instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

Quando o site do Configuration Manager suporta [gestão de clientes baseados na internet](/sccm/core/clients/manage/plan-internet-based-client-management) para clientes que umas vezes estão na intranet e, às vezes, na internet, tem duas opções quando instalar clientes na intranet:  

-   Incluir a propriedade de Client. msi `CCMHOSTNAME=<internet FQDN of the internet-based management point>` quando instala o cliente. Por exemplo, ao utilizar o push de cliente ou de instalação manual. Quando utiliza este método, atribua diretamente o cliente para o site. Não é possível utilizar a atribuição automática de site. Consulte a [como instalar manualmente clientes do Configuration Manager](#BKMK_Manual) seção, que fornece um exemplo deste método de configuração.  

-   Instale o cliente para gestão de clientes da intranet e, em seguida, atribuir o ponto de gestão de clientes baseada na internet para o cliente. Altere o ponto de gestão utilizando as propriedades de cliente no painel de controlo do Configuration Manager ou utilizando um script. Se utilizar este método, pode utilizar a atribuição automática de clientes. Para obter mais informações, consulte a [como configurar clientes para gestão de clientes baseados na internet após a instalação de cliente](#BKMK_ConfigureIBCM_MP) secção.  

Para instalar clientes na internet, escolha um dos seguintes métodos suportados:  

-   Fornece um mecanismo para estes clientes liguem temporariamente à intranet com uma VPN. Em seguida, instale o cliente utilizando um método de instalação de cliente adequado.  

-   Use um método de instalação que seja independente do Configuration Manager. Por exemplo, a empacotar os ficheiros de origem de instalação de cliente num suporte de dados amovível e enviar aos utilizadores para instalar. Os ficheiros de origem de instalação de cliente estão localizados no `<InstallationPath>\Client` pasta no servidor de site do Configuration Manager. Inclua no suporte de dados num script para copiar manualmente sobre a pasta do cliente. Nessa pasta, instale o cliente utilizando CCMSetup.exe e todas as CCMSetup da linha de comandos propriedades adequadas.  

> [!NOTE]  
>  O Configuration Manager não suporta a instalação do cliente diretamente a partir do ponto de gestão baseado na internet ou a partir do ponto de atualização de software baseado na internet.  

Os clientes que são geridos através da internet têm de comunicar com sistemas de sites baseados na internet. Certifique-se de que estes clientes também têm certificados de infraestrutura de chaves públicas (PKI) antes de instalar o cliente. Instale estes certificados independentemente do Configuration Manager. Para obter mais informações sobre os requisitos de certificado, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Instalar clientes na internet ao especificar as propriedades da linha de comandos do CCMSetup  

1.  Siga as instruções na secção [como instalar manualmente clientes do Configuration Manager](#BKMK_Manual). Sempre incluem as seguintes opções:  

    -   Parâmetro de linha de comandos do CCMSetup `/source:<local path to the copied Client folder>`  

    -   Parâmetro de linha de comandos do CCMSetup `/UsePKICert`  

    -   Propriedade Client. msi `CCMHOSTNAME=<FQDN of internet-based management point>`  

    -   Propriedade Client. msi `SMSSIGNCERT=<local path to exported site server signing certificate>`  

    -   Propriedade Client. msi `SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    >  Se o site tiver mais do que um ponto de gestão baseado na internet, não importa qual o ponto de gestão baseado na internet especificado para a propriedade CCMHOSTNAME. Quando um cliente do Configuration Manager estabelece ligação ao ponto de gestão baseado na internet especificado, ele envia ao cliente uma lista de pontos de gestão baseado na internet disponíveis no site. O cliente seleciona aleatoriamente um na lista.  

2.  Se não quiser que o cliente Verifique a lista de revogação de certificados (CRL), especifique o parâmetro de linha de comandos do CCMSetup `/NoCRLCheck`.  

3.  Se estiver a utilizar um ponto de estado de contingência baseado na internet, especifique a propriedade de Client. msi `FSP=<internet FQDN of the internet-based fallback status point>`.  

4.  Se estiver a instalar o cliente para gestão de clientes apenas na internet, especifique a propriedade de Client. msi `CCMALWAYSINF=1`.  

5.  Verifique se tem de especificar parâmetros de linha de comandos CCMSetup adicionais. Por exemplo, se o cliente tiver mais do que um certificado PKI válido, poderá ter de especificar um critério de seleção de certificado. Para obter uma lista de propriedades disponíveis, consulte [sobre parâmetros de instalação de cliente e as propriedades](/sccm/core/clients/deploy/about-client-installation-properties).  


#### <a name="internet-based-example"></a>Exemplo de baseado na Internet:  

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`    

Neste exemplo instala o cliente com os comportamentos seguintes:
  - Utilizar ficheiros de origem a partir de uma pasta na unidade D
  - Utilizar um certificado PKI de cliente 
  - Selecione o certificado com o período de validade mais longo 
  - Gestão de clientes apenas de Internet
  - Atribuir o cliente para utilizar o ponto de gestão baseado na internet com o nome SERVER1
  - Atribuir o ponto de estado de contingência baseado na internet no domínio contoso.com
  - Atribuir o cliente para o site ABC  


###  <a name="BKMK_ConfigureIBCM_MP"></a> Para configurar clientes para gestão de clientes baseados na internet após a instalação de cliente  

Para atribuir o ponto de gestão baseado na internet, depois de instalar o cliente, utilize um dos seguintes procedimentos. O primeiro requer configuração manual e é adequado para alguns clientes. A segunda é mais adequada para a configuração de vários clientes.  


#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-from-the-configuration-manager-control-panel"></a>Configurar clientes para gestão de clientes baseados na internet após a instalação do cliente do Configuration Manager no painel de controlo  

1.  Abra o **Configuration Manager** painel de controlo no cliente.  

2.  Sobre o **Internet** separador, introduza o nome de domínio completamente qualificado (FQDN) do ponto de gestão baseado na internet como o **FQDN de Internet**.  

    > [!NOTE]  
    >  O separador **Internet** só está disponível se o cliente tiver um certificado PKI de cliente.  

3.  Se o cliente acede à internet através de um servidor proxy, introduza as definições do servidor proxy.  


#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Configurar clientes para gestão de clientes baseada na internet após a instalação de cliente utilizando um script  

1.  Abra um editor de texto, como o Bloco de Notas.  

2.  Copie e insira o seguinte exemplo de VBScript para o ficheiro. Substitua *mp.contoso.com* com a internet FQDN do seu ponto de gestão baseado na internet.  

    ``` VBScript 
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the internet-based management point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

    > [!NOTE]  
    >  Para eliminar um ponto de gestão baseado na internet, remova o valor do FQDN dentro das aspas de servidor. A linha fique: `newInternetBasedManagementPointFQDN = ""`  

4.  Guarde o ficheiro com uma extensão .vbs.  

5.  Utilize cscript.exe para executar o script no cliente computadores, utilizando um dos seguintes métodos:  

    -   Implemente o ficheiro nos clientes existentes do Configuration Manager, utilizando um pacote e um programa.  

    -   Execute o ficheiro localmente nos clientes existentes do Configuration Manager, fazendo duplo clique no ficheiro de script no Explorador do Windows.  

Poderá ter de reiniciar o cliente para que as alterações entrem em vigor.  



##  <a name="BKMK_Provision"></a> Aprovisionar as propriedades de instalação de cliente para instalações de cliente baseada em atualização de software e de política de grupo

Política para aprovisionar computadores com propriedades de instalação de cliente do Configuration Manager de grupo da Windows utilizar. Essas propriedades são armazenadas no Registro do computador. O cliente lê-los quando ele é instalado. Este procedimento não é normalmente necessário, mas pode ser necessários para alguns cenários de instalação de cliente, tais como:  

-   Está a utilizar as definições de política de grupo ou métodos de instalação de cliente baseada em atualização de software. Ainda não tiver expandido o esquema do Active Directory para o Configuration Manager.  

-   Pretende substituir propriedades de instalação de cliente em computadores específicos.  

> [!NOTE]  
>  Se as propriedades de instalação são fornecidas na linha de comando CCMSetup.exe, não são utilizadas as propriedades de instalação aprovisionadas nos computadores.  

Um modelo administrativo de política de grupo com o nome **Configmgrinstallation** é fornecido no suporte de dados de instalação do Configuration Manager. Utilize este modelo para aprovisionar computadores de cliente com propriedades de instalação.   


### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Configurar e atribuir propriedades de instalação de cliente através de um objeto de política de grupo  

1.  Importar o modelo administrativo **Configmgrinstallation** num objeto de política de grupo novo ou existente, com um editor, como o Windows Group Policy Object Editor. Encontrar este ficheiro na pasta `TOOLS\ConfigMgrADMTemplates` na mídia de instalação do Configuration Manager.  

2.  Abra as propriedades da definição importada **Configurar Definições de Implementação de Cliente**.  

3.  Escolher **ativada**.  

4.  Na caixa **CCMSetup**, introduza as propriedades da linha de comandos CCMSetup necessárias. Para obter uma lista de todas as propriedades da linha de comandos CCMSetup e exemplos da sua utilização, consulte [sobre parâmetros de instalação de cliente e as propriedades](/sccm/core/clients/deploy/about-client-installation-properties).  

5.  Atribua o objeto de diretiva de grupo para os computadores que pretende aprovisionar com propriedades de instalação de cliente do Configuration Manager.  

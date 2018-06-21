---
title: Implementar clientes em Windows
titleSuffix: Configuration Manager
description: Saiba como implementar o cliente do Configuration Manager em computadores Windows.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5efca393afe2fc6441d074f987549228e7d0418f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342380"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>Como implementar clientes em computadores Windows no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de instalar clientes do Configuration Manager, certifique-se de que todos os o [pré-requisitos](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) estão no local e que concluiu todas as configurações de implementação necessária.   



##  <a name="BKMK_ClientPush"></a> Como instalar clientes com a instalação push do cliente  

Pode configurar a instalação de push de cliente para um site. Instalação de cliente é executado automaticamente em computadores que são detetados dentro de limites configurados do site quando esses limites estejam configurados como um grupo de limites. Em alternativa, pode iniciar uma instalação push do cliente ao executar o Assistente de Instalação Push do Cliente para uma coleção ou recurso específico na coleção.  

Também pode utilizar o Assistente de instalação de Push de cliente para instalar o cliente do Configuration Manager para [consulta](../../../core/servers/manage/queries-technical-reference.md) resultados. Para a instalação com êxito, um dos itens devolvidos pela consulta tem de ser o atributo **ResourceID** da classe **recurso do sistema**.   

Se o servidor do site não é possível contactar o computador cliente ou iniciar o processo de configuração, repete automaticamente a cada hora de instalação. O servidor continua a tentar novamente durante sete dias.  

Para ajudar a controlar o processo de instalação de cliente, instale um ponto de estado de contingência antes de instalar os clientes. Quando é instalado um ponto de estado de contingência, este será automaticamente atribuído aos clientes quando são instaladas pelo método de instalação de push de cliente. Para acompanhar o progresso da instalação de cliente, ver os relatórios de implementação e de atribuição de cliente. 

Ficheiros de registo do cliente fornecem informações mais detalhadas para resolução de problemas. Os ficheiros de registo não necessitam de um ponto de estado de contingência. Por exemplo, o **CCM.log** ficheiro no servidor do site regista eventuais problemas do servidor do site quando ligar ao computador. O **CCMSetup.log** ficheiro no cliente regista o processo de instalação.  

> [!IMPORTANT]  
>  Para que o push de cliente tenha êxito, certifique-se de que todos os pré-requisitos estão cumpridos. Para obter mais informações, consulte [dependências do método de instalação](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#installation-method-dependencies).  

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Configurar o site para utilizar automaticamente o push de cliente para os computadores detetados

1.  Na consola do Configuration Manager, escolha **administração** > **configuração do Site** > **Sites**.  

3.  Selecione o site para o qual pretende configurar a instalação push automática do cliente em todo o site.  

4.  No **home page** separador o **definições** grupo, escolha **definições de instalação de cliente** > **instalação Push do cliente**.  

5.  No **geral** separador do **propriedades de instalação Push do cliente** caixa de diálogo, selecione **ativar instalação push automática do cliente em todo o site**. Selecione os tipos de sistemas para os quais do Configuration Manager deve efetuar o push de cliente.  

6.  Selecione se pretende instalar o cliente nos controladores de domínio.  

7.  No **contas** separador, especifique uma ou mais contas para o Configuration Manager para utilizar quando ligar ao computador de destino. Clique em de **criar** ícone, introduza o **nome de utilizador** e **palavra-passe** (mais do que 38 caracteres), confirme a palavra-passe e, em seguida, clique em **OK**. Especifique a conta de instalação de push, pelo menos, um cliente. Esta conta tem de ter direitos de administrador local no computador de destino para instalar o cliente. Se não especificar uma conta de instalação de push de cliente, o Configuration Manager tenta utilizar a conta de computador do sistema de sites. Push de cliente entre domínios Falha ao utilizar a conta de computador do sistema de sites.  
    > [!NOTE]  
    >  Para utilizar o push de cliente de um site secundário, especifique a conta no site secundário que inicia a instalação push do cliente.  
    >   
    >  Para mais informações sobre a conta de instalação de push de cliente, consulte o procedimento seguinte, [utilizar o Assistente de instalação de Push de cliente](#use-the-client-push-installation-wizard).  

8.  Concluir o **as propriedades de instalação** separador.

     Se o esquema é expandido para o Configuration Manager, o site publica para serviços de domínio do Active Directory a [as propriedades de instalação de cliente](../../../core/clients/deploy/about-client-installation-properties.md) que especificou neste separador. Estas propriedades são lidas pelas instalações de cliente em que o CCMSetup é executado sem propriedades de instalação.  

    > [!NOTE]  
    >  Se ativar a instalação de push de cliente num site secundário, certifique-se de que o **SMSSITECODE** propriedade está definida como o nome de site do Configuration Manager do respetivo site primário principal. Se o esquema do Active Directory for expandido para o Configuration Manager, também pode definir esta propriedade para AUTO, de forma a localizar automaticamente a atribuição de site correta.  

### <a name="use-the-client-push-installation-wizard"></a>Utilizar o Assistente de instalação de Push de cliente

1.  Na consola do Configuration Manager, escolha **administração** >  **configuração do Site** > **Sites**.  

3.  Selecione o site para o qual pretende configurar a instalação push automática do cliente em todo o site.  

4.  No **home page** separador > **definições** grupo, escolha **definições de instalação de cliente** > **instalação Push do cliente**.  

5.  Concluir o **as propriedades de instalação** separador.  

     Se o esquema é expandido para o Configuration Manager, o site publica para serviços de domínio do Active Directory a [as propriedades de instalação de cliente](../../../core/clients/deploy/about-client-installation-properties.md) que especificou neste separador. Estas propriedades são lidas pelas instalações de cliente em que o CCMSetup é executado sem propriedades de instalação.   

6.  Na consola do Configuration Manager, escolha **ativos e compatibilidade**.  

7.  Na área de trabalho **Ativos e Compatibilidade**, selecione um ou mais computadores, ou uma coleção de computadores.  

8.  No **home page** separador, escolha uma das seguintes opções:  

    -   Se pretender instalar o cliente para um único computador ou em vários computadores, no **dispositivo** grupo, escolha **instalar cliente**.  

    -   Se pretender instalar o cliente numa coleção de computadores, no **coleção** grupo, escolha **instalar cliente**.  

9. No **antes de começar** página do **Assistente de instalação de cliente**, reveja as informações e, em seguida, escolha **seguinte**.  

10. Concluir o **opções de instalação** página.  

11. Reveja as definições de instalação e, em seguida, feche o assistente.  

> [!NOTE]  
>  Pode utilizar o Assistente para instalar clientes, mesmo que o site não está configurado para push de cliente.  



##  <a name="BKMK_ClientSUP"></a> Como instalar clientes com a instalação baseada em atualização de software  
 Instalação de cliente baseada em atualização de software publica o cliente para um ponto de atualização de software como uma atualização de software. Utilize este método para uma primeira hora instalação ou atualização.  

 Se um computador tiver o cliente do Configuration Manager instalado, este recebe a política de cliente do site. Esta política inclui o nome do servidor de ponto de atualização de software e a porta partir do qual obter as atualizações de software.   

> [!IMPORTANT]  
>  Para utilizar uma instalação baseada em atualizações de software, necessita de utilizar o mesmo servidor de Windows Server Update Services (WSUS) para a instalação do cliente e para as atualizações de software. Este servidor deverá ser o ponto de atualização de software ativo num site primário. Para obter mais informações, consulte [instalar um ponto de atualização de software](../../../sum/get-started/install-a-software-update-point.md).  

Se um computador não tiver o cliente do Configuration Manager instalado, configurar e atribuir um objeto de política de grupo nos serviços de domínio do Active Directory para especificar o nome do servidor do ponto de atualização de software.  

Não é possível adicionar propriedades de linha de comandos para uma instalação de cliente baseada em atualização de software. Se tiver expandido o esquema do Active Directory para o Configuration Manager, computadores cliente consultarão automaticamente serviços de domínio do Active Directory para as propriedades de instalação ao efetuar a instalação.  

Se não tiver expandido o esquema do Active Directory, pode utilizar a política de grupo para aprovisionar definições de instalação de cliente para computadores do seu site. Estas definições são automaticamente aplicadas a quaisquer instalações de cliente baseadas em atualizações de software. Para obter mais informações, consulte [como aprovisionar as propriedades de instalação de cliente (grupo política e o software de cliente baseada em atualização instalação)](#BKMK_Provision) e [como atribuir clientes a um site](../../../core/clients/deploy/assign-clients-to-a-site.md).  

Utilize os procedimentos seguintes para configurar computadores sem um cliente de Configuration Manager para utilizar a atualização de software ponto para a instalação de cliente e o software de atualizações e para publicar o cliente do ponto de atualização de software para o software.  

> [!NOTE]  
>  Se os computadores estiverem num estado de reinício pendente a seguir a uma instalação de software, uma instalação de cliente baseada em atualização de software pode causar o reinício do computador.  

### <a name="configure-a-group-policy-object-in-active-directory-domain-services-to-specify-the-software-update-point-for-client-installation-and-software-updates"></a>Configure um objeto de política de grupo nos serviços de domínio do Active Directory para especificar o ponto de atualização de software para atualizações de software e de instalação do cliente:  

1.  Utilize a consola de gestão de políticas de grupo para abrir um objeto de política de grupo novo ou existente.  

2.  Na consola, expanda **configuração do computador**, expanda **modelos administrativos**, expanda **componentes do Windows**e, em seguida, escolha **Windows Update**.  

3.  Abra as propriedades da definição **especificar a localização de serviço de atualização de Microsoft na intranet**e, em seguida, escolha **ativado**.  

4.  Na caixa de **definir o serviço de atualização de intranet para detetar atualizações**, especifique o nome e a porta do servidor de ponto de atualização de software:  

    -   Se o sistema de sites do Configuration Manager estiver configurado para utilizar um nome de domínio completamente qualificado (FQDN), utilize o formato FQDN.  

    -   Se o sistema de sites do Configuration Manager não está configurado para utilizar um FQDN, utilize um formato de nome curto.  

    > [!NOTE]  
    >  Para determinar o número da porta, consulte [como determinar as definições de porta utilizadas pelo WSUS](../../../sum/plan-design/plan-for-software-updates.md).  

     Exemplo: **http://server1.contoso.com:8530**  

5.  Na caixa de **definir o servidor de estatísticas de intranet**, especifique o nome do servidor de estatísticas de intranet. Não tem de ser o mesmo que o servidor de ponto de atualização de software. Se for o mesmo servidor, não tem o formato corresponder.  

6.  Atribua o objeto de política de grupo aos computadores nos quais pretende instalar o cliente e receber atualizações de software.  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>Publicar o cliente do Configuration Manager para o ponto de atualização de software  

1.  Na consola do Configuration Manager, clique em **administração** > **configuração do Site** > **Sites**.  

3.  Selecione o site para o qual pretende configurar a instalação de cliente baseada em atualização de software.  

4.  No **home page** separador o **definições** grupo, escolha **definições de instalação de cliente**e, em seguida, escolha **Software Update-Based a instalação do cliente**.  

5.  Selecione **ativar a instalação de cliente baseada em atualização de software**.  

6.  Se o software de cliente no servidor do site do Configuration Manager é uma versão posterior à versão no ponto de atualização de software, o **detetada versão posterior do cliente pacote** é aberta a caixa de diálogo. Clique em **Sim** para publicar a versão mais recente.  

    > [!NOTE]  
    >  Se o software de cliente não foi publicado anteriormente para o software de um ponto de atualização, esta caixa está em branco.  

A atualização de software para o cliente do Configuration Manager não é automaticamente atualizada se existir uma nova versão. Se atualizar o site, o que inclui uma nova versão de cliente, repita este procedimento e clique em **Sim** no passo 6.  



##  <a name="BKMK_ClientGP"></a> Como instalar clientes com a política de grupo  
 Pode utilizar política de grupo nos serviços de domínio do Active Directory para publicar ou atribuir o cliente do Configuration Manager para instalar nos computadores da sua empresa. O cliente é instalado quando o computador é iniciado. Quando utilizar a política de grupo, o cliente será apresentado no painel de controlo **adicionar ou remover programas** para o utilizador instalar.  

 Utilize o pacote do Windows Installer (CCMSetup.msi) para instalações baseadas em políticas de grupo. Este ficheiro está localizado na pasta  **&lt;diretório de instalação do ConfigMgr\>\bin\i386** no servidor do site do Configuration Manager. Não é possível adicionar propriedades a este ficheiro para modificar o comportamento de instalação.  

> [!IMPORTANT]  
>  Tem de ter permissões de administrador para aceder aos ficheiros de instalação do cliente.  

-   Se o esquema do Active Directory é expandido para o Configuration Manager e **publicar este site nos serviços de domínio do Active Directory** está selecionado no **avançadas** separador do **propriedades do Site** caixa de diálogo, computadores cliente procuram automaticamente os serviços de domínio do Active Directory para as propriedades de instalação. Para obter mais informações sobre as propriedades de instalação que são publicadas, consulte [acerca das propriedades de instalação de cliente publicadas nos serviços de domínio do Active Directory](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

-   Se não tiver sido expandido o esquema do Active Directory, pode utilizar o procedimento deste tópico para armazenar propriedades de instalação no registo dos computadores: [Como aprovisionar as propriedades de instalação de cliente (grupo política e o software de cliente baseada em atualização instalação)](#BKMK_Provision). Estas propriedades de instalação são utilizadas quando o cliente está instalado.  

Para obter informações sobre como utilizar a política de grupo nos serviços de domínio do Active Directory para instalar software, consulte a documentação do Windows Server.  



##  <a name="BKMK_Manual"></a> Como instalar clientes manualmente  
 Pode instalar manualmente o software de cliente em computadores na sua empresa utilizando o programa CCMSetup.exe. Este programa e respetivos ficheiros de suporte podem ser encontrados no **cliente** pasta da pasta de instalação do Configuration Manager no servidor do site e nos pontos de gestão do seu site. Esta pasta é partilhada na rede como  

 \\\\*&lt;Nome do servidor do site\>* \SMS_*&lt;código do Site\>* \Client\  

 onde *&lt;nome do servidor de Site\>* é o nome de um dos servidores que alojam um ponto de gestão, e *&lt;código do Site\>* se o código de site primário para qual é atribuído o cliente. Para executar CCMSetup.exe a partir da linha de comandos no cliente, tem de mapear uma unidade de rede para esta localização e, em seguida, execute o comando.  

> [!IMPORTANT]  
>  Tem de ter permissões de administrador para aceder aos ficheiros de instalação do cliente.  

 CCMSetup.exe copia todos os pré-requisitos necessários para o computador cliente e chama o pacote do Windows Installer (Client.msi) para instalar o cliente. Não é possível executar Client.msi diretamente.  

 Pode especificar propriedades da linha de comandos para CCMSetup.exe e Client.msi para modificar o comportamento da instalação do cliente. Certifique-se de que especifica as propriedades de CCMSetup (as propriedades que começam com **/**) antes de especificar as propriedades de Client.msi. Por exemplo:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`    

e o cliente instala, utilizando as seguintes propriedades:  

|Propriedade|Descrição|  
|--------------|-----------------|  
|**/mp:SMSMP01**|Esta propriedade de CCMSetup especifica que o ponto de gestão SMSMP01 transfere os ficheiros de instalação de cliente necessários.|  
|**/logon**|Esta propriedade de CCMSetup Especifica que a instalação deverá ser interrompida se for encontrado um cliente existente do Configuration Manager no computador.|  
|**SMSSITECODE=AUTO**|Esta propriedade de Client.msi Especifica que o cliente tenta localizar o código do site do Configuration Manager para utilizar, por exemplo, utilizando os serviços de domínio do Active Directory.|  
|**FSP=SMSFP01**|Esta propriedade de Client.msi Especifica que o ponto de estado de contingência com o nome SMSFP01 é utilizado para receber mensagens de estado enviadas do computador cliente.|  

 Para obter detalhes sobre todas as propriedades de CCMSetup.exe, consulte [acerca das propriedades de instalação do cliente](../../../core/clients/deploy/about-client-installation-properties.md)  

> [!Tip]  
> Para o procedimento instalar o cliente do Configuration Manager num dispositivo Windows 10 moderno utilizando a identidade do Azure AD, consulte [instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Esse procedimento destina-se a clientes na intranet ou à internet.  


### <a name="examples"></a>Exemplos
 Estes exemplos são clientes do Active Directory na intranet. Utilizam os seguintes valores para representar diferentes aspetos do site:  

 **MPSERVER** = o servidor que aloja o ponto de gestão   
**FSPSERVER** = o servidor que aloja o ponto de estado de contingência  
**ABC** = código do site  
**contoso.com** = nome do domínio  

 Todos os servidores de sistema de sites são configurados com um FQDN de intranet. O site é publicado na floresta do cliente do Active Directory.  

 No computador cliente, iniciar sessão como um administrador local, mapear uma unidade (z) para\\\MPSERVER\SMS_ABC\Client, mude a linha de comandos para a unidade z e, em seguida, execute um dos seguintes comandos:  

 **Exemplo 1:**  

`CCMSetup.exe`  

Este exemplo instala o cliente sem propriedades adicionais. O cliente é automaticamente configurado com as propriedades de instalação de cliente publicadas nos serviços de domínio do Active Directory. É automaticamente configurado para as seguintes definições: 
- Código do site. Esta definição necessita de localização de rede do cliente a ser incluído num grupo de limites que esteja configurado para atribuição de cliente. 
- Ponto de gestão
- Ponto de estado de contingência
- Comunicar utilizando apenas HTTPS  
  
Para obter mais informações, consulte [acerca das propriedades de instalação de cliente publicadas nos serviços de domínio do Active Directory](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 **Exemplo 2:**  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
Este exemplo substitui a configuração automática que fornece serviços de domínio do Active Directory. Não requer que a localização de rede do cliente está incluída num grupo de limites que esteja configurado para atribuição de cliente. Em vez disso, a instalação Especifica as seguintes definições:
- Código do site
- Ponto de gestão de intranet 
- Ponto de gestão baseado na Internet
- Ponto de estado de contingência que aceita ligações da internet
- Utilize um certificado PKI (se disponível) do cliente que tenha o período de validade mais longo  



##  <a name="BKMK_ClientLogonScript"></a> Como instalar clientes com scripts de início de sessão  
 O Configuration Manager suporta scripts de início de sessão para instalar o software de cliente do Configuration Manager. Pode utilizar o ficheiro de programa **CCMSetup.exe** num script de início de sessão para acionar a instalação do cliente.  

 A instalação com script de início de sessão utiliza os mesmos métodos da instalação manual de cliente. Pode especificar o **/início de sessão** propriedade de instalação para CCMSsetup.exe. Se já existir uma versão do cliente no computador, esta propriedade impede que o cliente instalar. Este comportamento impede a reinstalação do cliente a decorrer o script de início de sessão de cada vez que é executado.  

 Não se for especificada nenhuma origem de instalação pelo **/origem** propriedade e nenhum ponto de gestão a partir do qual obter a instalação é especificada pelo **/MP** propriedade, o CCMSetup.exe localiza o ponto de gestão ao pesquisar os serviços de domínio do Active Directory. Este comportamento só ocorre se o esquema tiver sido expandido para o Configuration Manager e o site é publicado para serviços de domínio do Active Directory. Em alternativa, o cliente pode utilizar DNS ou WINS para localizar um ponto de gestão.  



##  <a name="BKMK_ClientApp"></a> Como instalar clientes com um pacote e programa  
 Pode utilizar o Configuration Manager para criar e implementar um pacote e programa que Atualize o software de cliente para computadores selecionados na sua hierarquia. Um ficheiro de definição de pacote que povoa as propriedades do pacote com valores normalmente utilizados é fornecido com o Configuration Manager. Pode personalizar o comportamento da instalação do cliente especificando propriedades de linha de comandos adicionais.  

> [!NOTE]  
>  Não é possível atualizar clientes do Configuration Manager 2007 com este método. Em vez disso, utilize a atualização automática de cliente, que cria e implementa automaticamente um pacote com a versão mais recente do cliente. Para obter mais informações, consulte [atualizar clientes](../../../core/clients/manage/upgrade/upgrade-clients.md).  
>   
>  Para obter mais informações sobre como migrar a partir de versões mais antigas do cliente do Configuration Manager, consulte [planear uma estratégia de migração de cliente](../../../core/migration/planning-a-client-migration-strategy.md).  

 
### <a name="create-a-package-and-program-for-the-client-software"></a>Criar um pacote e programa para o software de cliente  

Utilize o procedimento seguinte para criar um pacote do Configuration Manager e o programa que pode implementar em computadores de cliente do Configuration Manager para atualizar o software de cliente.  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **pacotes**.  

3.  No **home page** separador o **criar** grupo, escolha **criar pacote a partir da definição**.  

4.  No **definição de pacote** página do assistente, selecione **Microsoft** do **publicador** na lista pendente e selecione **atualização de cliente do Configuration Manager** do **definição do pacote** lista.  

5.  No **ficheiros de origem** página, selecione **obter sempre ficheiros da pasta de origem**.  

6.  No **pasta de origem** página, selecione **caminho de rede (nome UNC)**. Em seguida, introduza o caminho de rede do computador e a pasta que contém os ficheiros de instalação de cliente.  

    > [!NOTE]  
    >  O computador em que a execução de implementação do Configuration Manager tem de ter acesso à pasta de rede que especificar, caso contrário, a instalação falha.  

    Para alterar qualquer uma das propriedades de instalação do cliente, modifique os parâmetros da linha de comandos de CCMSetup.exe no **geral** separador do **atualização silenciosa do agente do Configuration Manager propriedades** caixa de diálogo de programa caixa. As propriedades de instalação predefinidas são **/noservice SMSSITECODE=AUTO**.  

9. Distribua o pacote por todos os pontos de distribuição que pretende que alojem o pacote de atualização de cliente. Em seguida, pode implementar o pacote em coleções de computadores que contêm clientes que pretende atualizar.  



## <a name="bkmk_mdm"></a>Como instalar clientes em dispositivos Windows geridos por MDM do Intune

Pode implementar os ficheiros de instalação de cliente em computadores que estão inscritos no Microsoft Intune. 

Este procedimento é para um cliente tradicional que está ligado à intranet. Utiliza os métodos de autenticação de cliente tradicional. Para garantir que o dispositivo permanece no estado gerido depois do software de cliente é instalado, o dispositivo tem de estar na intranet e dentro de um limite de site do Configuration Manager.  

Para o procedimento instalar o cliente do Configuration Manager num dispositivo Windows 10 moderno utilizando a identidade do Azure AD, consulte [instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

> [!NOTE]
> Assim que o software de cliente é instalado, o dispositivo é removido do Intune.
> 
> A partir de versão 1710, os clientes não anular a inscrição do Intune. Pode têm o cliente do Configuration Manager e a inscrição MDM ao mesmo tempo. Para obter mais informações, consulte [gestão conjunta](/sccm/core/clients/manage/co-management-overview).

###  <a name="install-clients-with-intune"></a>Instale clientes com o Intune:

1. No Intune, [criar uma aplicação](/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune) que contém o ficheiro de instalação de cliente do Configuration Manager **ccmsetup.msi**. Este ficheiro está localizado na pasta  **&lt;diretório de instalação do ConfigMgr\>\bin\i386** no servidor do site do Configuration Manager.

2. O Intune Software Publisher, introduza os parâmetros da linha de comandos. Por exemplo, utilize a seguinte linha de comandos com um cliente tradicional na intranet:

  `CCMSETUPCMD="/MP:&lt;FQDN of management point> SMSMP=&lt;FQDN of management point> SMSSITECODE=&lt;Your site code> DNSSUFFIX=&lt;DNS Suffix of management point>"`  

   > [!Note]  
   > Para uma linha de comandos de exemplo utilizar com um cliente Windows 10 moderno utilizando a autenticação do Azure AD, consulte [dispositivos de preparar o Windows 10 para gestão conjunta](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).

3. [Implementar a aplicação](/intune/deploy-use/deploy-apps-in-microsoft-intune) aos computadores Windows inscritos.



##  <a name="BKMK_ClientImage"></a> Como instalar clientes com uma imagem do computador  
É possível pré-instalar o software de cliente do Configuration Manager num computador de referência que utilizou para criar uma imagem de SO.   

> [!Important]
> Ao utilizar a sequência de tarefas do Configuration Manager para implementar a imagem do SO, o [preparar ConfigMgr Client](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) passo de sequência de tarefas remove completamente o cliente do Configuration Manager. 

### <a name="prepare-the-client-computer-for-imaging"></a>Preparar o computador cliente para criação de imagens  

1.  Instale manualmente o software de cliente do Configuration Manager no computador de referência. Para obter mais informações, veja [Como Instalar Manualmente Clientes do Configuration Manager](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Não especifique um código de site do Configuration Manager para o cliente nas propriedades da linha de comandos do CCMSetup.exe.  

2.  Na linha de comandos, escreva `net stop ccmexec` para se certificar de que o **SMS Agent Host** serviço (Ccmexec.exe) não está em execução no computador de referência.
3.  Elimine o ficheiro **SMSCFG. INI** do **Windows** pasta no computador de referência.  
3.  Remova todos os certificados são armazenados no arquivo do computador local no computador de referência. Por exemplo, se utilizar certificados de infraestrutura de chaves públicas (PKI), terá de remover os certificados do arquivo **Pessoal** de **Computador** e de **Utilizador** antes de criar a imagem do computador.

4.  Se os clientes são instalados numa hierarquia do Configuration Manager diferente que o computador de referência, remova a chave de raiz fidedigna do computador de referência.  
    > [!NOTE]  
    >  Se os clientes não conseguirem consultar os Serviços de Domínio do Active Directory para localizar um ponto de gestão, utilizarão a chave de raiz fidedigna para determinar os pontos de gestão fidedignos. Se todos os clientes instalados são implementados na mesma hierarquia como computador principal, deixe a chave de raiz fidedigna no local. Se os clientes são implementados em hierarquias diferentes, remova a chave de raiz fidedigna. Aprovisione também estes clientes com a nova chave de raiz fidedigna. Para obter mais informações, consulte [planeamento para a chave de raiz fidedigna](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK). 

5.  Utilize o software de processamento de imagens para capturar a imagem do computador principal.  

6.  Implemente a imagem nos computadores de destino.  



##  <a name="BKMK_ClientWorkgroup"></a> Como instalar clientes em computadores de grupo de trabalho  
 O Configuration Manager suporta a instalação de cliente para computadores em grupos de trabalho. Instale o cliente em computadores de grupo de trabalho através do método especificado em [Como Instalar Manualmente Clientes do Configuration Manager](#BKMK_Manual).  

 Pré-requisitos:  

-   O cliente deve ser instalado manualmente em cada computador de grupo de trabalho. Durante a instalação, o utilizador com sessão iniciada tem de ter direitos de administrador local.  

-   Para poder aceder aos recursos no domínio do servidor de site do Configuration Manager, a conta de acesso de rede tem de ser configurada para o site. Especificar esta conta como uma propriedade de componente de distribuição de software. Para obter mais informações, veja [Componentes do site para o System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

 Limitações:  

-   Os clientes de grupo de trabalho não podem localizar pontos de gestão dos Serviços de Domínio do Active Directory e, em vez disso, devem utilizar DNS, WINS ou outro ponto de gestão.  

-   Não é suportado roaming global, uma vez que os clientes não conseguem consultar os Serviços de Domínio do Active Directory para obter informações do site.  

-   Os métodos de deteção do Active Directory não conseguem detetar computadores em grupos de trabalho.  

-   Não é possível implementar software para utilizadores de computadores de grupo de trabalho.  

-   Não é possível utilizar o método de instalação push de cliente para instalar o cliente em computadores de grupo de trabalho.  

-   Os clientes de grupo de trabalho não é possível utilizar o Kerberos para autenticação e podem exigir a aprovação manual.  

-   Não é possível configurar um cliente de grupo de trabalho como ponto de distribuição. O Configuration Manager requer que ponto de distribuição computadores sejam membros de um domínio.  

### <a name="install-the-client-on-workgroup-computers"></a>Instalar o cliente em computadores de grupo de trabalho  

Verifique os pré-requisitos, em seguida, siga as indicações na secção [como instalar clientes do Configuration Manager manualmente](#BKMK_Manual).  

   Este exemplo instala o cliente para gestão de clientes na intranet e especifica o código do site e o sufixo DNS para localizar um ponto de gestão. `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

     

   Este exemplo requer que o cliente se encontre numa localização de rede que está configurada num grupo de limites. Este requisito corresponde a atribuição automática de site com êxito. O comando inclui um ponto de estado de contingência num servidor FSPSERVER. Esta propriedade ajuda a controlar a implementação do cliente e para identificar qualquer comunicação do cliente problemas. 
   `CCMSetup.exe FSP=fspserver.constoso.com`  

      

##  <a name="BKMK_ClientInternet"></a> Como instalar clientes para gestão de clientes baseados na internet  
 
> [!Note]
> Esta secção não se aplica aos clientes que utilizam um [gateway de gestão de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Para instalar os clientes baseados na internet utilizando um gateway de gestão de nuvem, consulte [instale e atribua os clientes do Configuration Manager Windows 10 com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

Quando o site do Configuration Manager suporta [gestão de clientes baseados na internet](/sccm/core/clients/manage/plan-internet-based-client-management) para clientes que umas vezes estão na intranet e, por vezes na internet, tem duas opções ao instalar clientes na intranet:  

-   Pode incluir a propriedade Client.msi de CCMHOSTNAME =*&lt;internet FQDN do ponto de gestão baseado na internet\>*  quando instala o cliente, por exemplo, utilizando push de cliente ou de instalação manual. Se utilizar este método, deve também atribuir diretamente o cliente ao site e não pode utilizar a atribuição automática do site. O [como instalar clientes do Configuration Manager manualmente](#BKMK_Manual) deste tópico fornece um exemplo deste método de configuração.  

-   Pode instalar o cliente para gestão de clientes de intranet e, em seguida, atribua o ponto de gestão de clientes baseada na internet ao cliente. Altere o ponto de gestão utilizando as propriedades de cliente do Configuration Manager no painel de controlo ou através de um script. Se utilizar este método, pode utilizar a atribuição automática de clientes. Para obter mais informações, consulte o [como configurar clientes para gestão de clientes baseada na internet após a instalação de cliente](#BKMK_ConfigureIBCM_MP) deste tópico.  

 Se tem de instalar os clientes que estão na internet, escolha um dos seguintes métodos suportados:  

-   Fornece um mecanismo para estes clientes liguem temporariamente à intranet com uma VPN. Em seguida, instale o cliente utilizando um método de instalação de cliente adequado.  

-   Utilize um método de instalação que seja independente do Configuration Manager. Por exemplo, os ficheiros de origem de instalação de cliente num suporte de dados amovível que possa ser enviado para os utilizadores para instalar com as instruções do pacote. Os ficheiros de origem de instalação do cliente estão localizados no  *&lt;Caminhodainstalação\>* pasta \Client os pontos de gestão e servidor de site do Configuration Manager. Inclua no suporte de dados um script para copiar e substituir manualmente a pasta do cliente e, a partir desta pasta, instale o cliente, utilizando CCMSetup.exe e todas as propriedades da linha de comandos CCMSetup.exe adequadas.  

> [!NOTE]  
>  O Configuration Manager não suporta a instalação do cliente diretamente a partir do ponto de gestão baseado na internet ou a partir do ponto de atualização de software baseado na internet.  

 Clientes que são geridos através da internet têm de comunicar com sistemas de sites baseados na internet. Certifique-se de que estes clientes também têm certificados de infraestrutura de chaves públicas (PKI) antes de instalar o cliente. Instale estes certificados independentemente do Configuration Manager. Para obter mais informações sobre os requisitos de certificado, consulte [requisitos dos certificados PKI](../../../core/plan-design/network/pki-certificate-requirements.md).  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Instalar clientes na internet, especificando as propriedades da linha de comandos do CCMSetup  

1.  Siga as indicações na secção [como instalar clientes do Configuration Manager manualmente](#BKMK_Manual) e inclua sempre o seguinte:  

    -   Propriedade da linha de comandos CCMSetup **/Source:** *&lt;caminho local para a pasta Client copiada\>*  

    -   Propriedade da linha de comandos CCMSetup **/UsePKICert**  

    -   Propriedade Client.msi **CCMHOSTNAME =** *&lt;FQDN do ponto de gestão baseado na internet\>*  

    -   Propriedade Client.msi **SMSSIGNCERT =** *&lt;caminho local para o certificado de assinatura do servidor de site exportado\>*  

    -   Propriedade Client.msi **SMSSITECODE =** *&lt;código do ponto de gestão baseado na internet\>*  

    > [!NOTE]  
    >  Se o site tiver mais do que um ponto de gestão baseado na internet, é irrelevante o ponto de gestão baseado na internet especificado para a propriedade CCMHOSTNAME. Quando um cliente do Configuration Manager liga ao ponto de gestão baseado na internet especificado, o ponto de gestão envia ao cliente uma lista de pontos de gestão baseado na internet disponíveis no site. O cliente seleciona aleatoriamente um da lista.  

2.  Se não quiser que o cliente verifique a lista de revogação de certificados (CRL), especifique a propriedade da linha de comandos CCMSetup **/NoCRLCheck**.  

3.  Se estiver a utilizar um ponto de estado de contingência baseado na internet, especifique a propriedade de Client.msi **FSP =** *&lt;internet FQDN do ponto de estado de contingência baseado na internet\>*.  

4.  Se estiver a instalar o cliente para gestão de clientes apenas na internet, especifique a propriedade de Client.msi **CCMALWAYSINF = 1**.  

5.  Certifique-se de que o se tiver de especificar as propriedades da linha de comandos CCMSetup adicionais. Por exemplo, poderá ter de especificar um critério de seleção de certificado se o cliente tiver mais do que um certificado PKI válido. Para obter uma lista das propriedades disponíveis, consulte [acerca das propriedades de instalação de cliente](../../../core/clients/deploy/about-client-installation-properties.md).  

   Exemplo:  
   `CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`    

   Este exemplo instala o cliente com os comportamentos seguintes:
   - Utilizar ficheiros de origem a partir de uma pasta na unidade D
   - Utilizar um certificado PKI de cliente 
   - Selecione o certificado com o período de validade mais longo 
   - Gestão de clientes apenas de Internet
   - Atribuir o cliente para utilizarem o ponto de gestão baseado na internet com o nome SERVER1
   - Atribua o ponto de estado de contingência baseado na internet no domínio contoso.com
   - Atribuir o cliente para o site ABC  

###  <a name="BKMK_ConfigureIBCM_MP"></a>Para configurar clientes para gestão de clientes baseados na internet após a instalação de cliente  
 Para atribuir o ponto de gestão baseado na internet após a instalação do cliente, utilize um dos seguintes procedimentos. O primeiro requer configuração manual e é adequado para alguns clientes. A segundo é mais adequada para a configuração de vários clientes.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>Configurar clientes para gestão de clientes baseada na internet após a instalação de cliente através da atribuição do ponto de gestão baseado na internet nas propriedades do Configuration Manager  

1.  Navegue para **Configuration Manager** no Painel de Controlo do computador cliente e, em seguida, faça duplo clique para abrir as respetivas propriedades.  

2.  No **Internet** separador, introduza o nome de domínio completamente qualificado do ponto de gestão baseado na internet na internet FQDN caixa de texto.  

    > [!NOTE]  
    >  O separador **Internet** só está disponível se o cliente tiver um certificado PKI de cliente.  

3.  Se o cliente acede ao internet utilizando um servidor proxy, introduza as definições do servidor proxy.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Configurar clientes para gestão de clientes baseada na internet após a instalação de cliente utilizando um script  

1.  Abra um editor de texto, como o Bloco de Notas.  

2.  Copie e insira o seguinte exemplo de VBScript para o ficheiro. Substitua *mp.contoso.com* com a internet FQDN do seu ponto de gestão baseado na internet.  

    ```  
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
    >  Se for necessário eliminar um ponto de gestão baseado na internet especificado para que o cliente não está configurado para utilizar um ponto de gestão baseado na internet, remova o valor entre aspas para que a linha fique: `newInternetBasedManagementPointFQDN = ""`  

4.  Guarde o ficheiro com uma extensão .vbs.  

5.  Utilize cscript.exe para executar o script no cliente computadores, utilizando um dos seguintes métodos:  

    -   Implemente o ficheiro nos clientes existentes do Configuration Manager, utilizando um pacote e um programa.  

    -   Execute o ficheiro localmente nos clientes existentes do Configuration Manager, fazendo duplo clique no ficheiro de script no Explorador do Windows.  

 Poderá ter de reiniciar o cliente para que as alterações entrem em vigor.  



##  <a name="BKMK_Provision"></a> Como aprovisionar as propriedades de instalação de cliente (grupo política e o software de cliente baseada em atualização instalação)  
 Pode utilizar a política de grupo do Windows para aprovisionar computadores com propriedades de instalação de cliente do Configuration Manager. Estas propriedades são armazenadas no registo do computador e são lidos quando o software de cliente é instalado. Este procedimento não é normalmente necessário, mas pode ser necessários para alguns cenários de instalação de cliente, tais como:  

-   Está a utilizar as definições de política de grupo ou métodos de instalação de cliente baseada em atualização de software. Não tiver expandido o esquema do Active Directory para o Configuration Manager.  

-   Pretende substituir propriedades de instalação de cliente em computadores específicos.  

> [!NOTE]  
>  Se as propriedades de instalação são fornecidas na linha de comandos de CCMSetup.exe, não são utilizadas as propriedades de instalação aprovisionadas nos computadores.  

 É fornecido um modelo administrativo de política de grupo com o nome ConfigMgrInstallation.adm no suporte de dados de instalação do Configuration Manager. Este modelo pode ser utilizado para aprovisionar computadores cliente com propriedades de instalação.   

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Configurar e atribuir propriedades de instalação de cliente através da utilização de uma objeto de política de grupo  

1.  Importe o modelo administrativo ConfigMgrInstallation.adm para um objeto de política de grupo novo ou existente, utilizando um editor, como o Windows grupo objeto Editor de políticas. O ficheiro pode ser encontrado na pasta **TOOLS\ConfigMgrADMTemplates** no suporte de dados de instalação do Configuration Manager.  

2.  Abra as propriedades da definição importada **Configurar Definições de Implementação de Cliente**.  

3.  Escolha **ativada**.  

4.  Na caixa **CCMSetup**, introduza as propriedades da linha de comandos CCMSetup necessárias. Para obter uma lista de todas as propriedades da linha de comandos CCMSetup e exemplos da sua utilização, consulte [acerca das propriedades de instalação de cliente](../../../core/clients/deploy/about-client-installation-properties.md).  

5.  Atribua o objeto de política de grupo aos computadores que pretende aprovisionar com as propriedades de instalação de cliente do Configuration Manager.  

Para obter informações sobre a política de grupo do Windows, consulte a documentação do Windows Server.  



## <a name="next-steps"></a>Passos seguintes
Para obter mais ajuda a instalar o cliente do Configuration Manager, consulte [métodos de instalação de cliente](../../../core/clients/deploy/plan/client-installation-methods.md).
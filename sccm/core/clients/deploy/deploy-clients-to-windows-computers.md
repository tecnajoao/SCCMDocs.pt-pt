---
title: Implemente os clientes Windows | Documentos do Microsoft
description: Saiba como implementar clientes em computadores com Windows no System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
caps.latest.revision: 13
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: 83878b71b876c725920b228190000fc849a063db
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>Como implementar clientes em computadores Windows no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de instalar clientes do Configuration Manager, certifique-se de que todos os o [pré-requisitos](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) estão no local e que concluiu todas as configurações de implementação necessária.   

##  <a name="BKMK_ClientPush"></a>Como instalar clientes com push do cliente  

Pode configurar a instalação push de cliente num site para que a instalação do cliente seja automaticamente executada nos computadores que forem detetados dentro dos limites configurados do site, desde que esses limites estejam configurados como um grupo de limites. Em alternativa, pode iniciar uma instalação push do cliente ao executar o Assistente de Instalação Push do Cliente para uma coleção ou recurso específico na coleção.  

Também pode utilizar o Assistente de instalação Push do cliente para instalar o cliente do Configuration Manager [consulta](../../../core/servers/manage/queries-technical-reference.md) resultados. Para uma instalação com êxito, um dos itens devolvidos pela consulta tem de ser o atributo **ResourceID** da classe de **recurso de sistema**.   

Se o servidor do site não é possível contactar o computador cliente ou iniciar o processo de configuração, repetirá automaticamente a tentativa de instalação com intervalos de uma hora até de 7 dias.  

Para ajudar a controlar o processo de instalação do cliente, instale um sistema de sites de ponto de estado de reversão antes de instalar os clientes. Quando instalar um ponto de estado de reversão, este será automaticamente atribuído aos clientes quando forem instalados através do método de instalação push de cliente. Consulte os relatórios de implementação e de atribuição de clientes para controlar o progresso da instalação de cliente. 

Ficheiros de registo de cliente fornecem que informações mais detalhadas para resolução de problemas e não necessitam de um ponto de estado de contingência. Por exemplo, o ficheiro CCM.log localizado no servidor do site regista eventuais problemas que ocorram no servidor de sites ao estabelecer a ligação ao computador, enquanto o ficheiro CCMSetup.log do cliente regista o processo de instalação.  

> [!IMPORTANT]  
>  Para que o push de cliente tenha êxito, certifique-se de que todos os pré-requisitos estão cumpridos. Os pré-requisitos são indicados na secção "Dependências do método de instalação" na [pré-requisitos para implementação de clientes para computadores Windows no System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md).  

### <a name="to-configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Para configurar o site para utilizar automaticamente o cliente push para computadores detetados

1.  Na consola do Configuration Manager, escolha **administração** > **configuração do Site** > **Sites**.  

3.  Selecione o site para o qual pretende configurar a instalação push automática do cliente em todo o site.  

4.  No **base** separador o **definições** grupo, selecione **definições de instalação de cliente** > **instalação Push do cliente**.  

5.  No **geral** separador do **propriedades de instalação Push do cliente** caixa de diálogo, selecione **ativar a instalação push automática do cliente em todo o site**. Selecione os tipos de sistema para o qual o Configuration Manager deve push o software de cliente.  

6.  Selecione se pretende instalar o cliente em controladores de domínio.  

7.  No **contas** separador, especifique uma ou mais contas do Configuration Manager para utilizar quando ligar ao computador para instalar o software de cliente. Clique na **criar** ícone, introduza o **nome de utilizador** e **palavra-passe** (mais do que 38 caracteres), confirme a palavra-passe e, em seguida, clique em **OK**. Tem de especificar, pelo menos, uma conta de instalação push do cliente, que tem de ter direitos de administrador local em todos os computadores no qual pretende instalar o cliente. Se não especificar uma conta de instalação de push de cliente, o Configuration Manager tenta utilizar a conta de computador de sistema de sites, que irá fazer com que a instalação push do cliente de entre domínios a falhar.  

    
    > [!NOTE]  
    >  Se tenciona utilizar o método de instalação push do cliente a partir de um site secundário, a conta deverá ser especificada no site secundário que iniciar a instalação push de cliente.  
    >   
    >  Para mais informações sobre a conta de instalação de push de cliente, consulte o procedimento seguinte, "para utilizar o Assistente de instalação de Push de cliente".  

8.  Concluir o **as propriedades de instalação** separador.

     [As propriedades de instalação de cliente](../../../core/clients/deploy/about-client-installation-properties.md) que estão especificadas neste separador são publicadas no Active Directory Domain Services caso o esquema é expandido para o Configuration Manager e lido pelas instalações de cliente em que o CCMSetup é executado sem propriedades de instalação.  

    > [!NOTE]  
    >  Se ativar a instalação de push de cliente num site secundário, certifique-se de que a propriedade SMSSITECODE está definida para o nome do site do Configuration Manager do respetivo site primário principal. Se o esquema do Active Directory é expandido para o Configuration Manager, também poderá configurar esta definição para AUTO, para localizar automaticamente a atribuição de site correto.  

### <a name="to-use-the-client-push-installation-wizard"></a>Para utilizar o Assistente de Instalação Push do Cliente

1.  Na consola do Configuration Manager, escolha **administração** >  **configuração do Site** > **Sites**.  

3.  Selecione o site para o qual pretende configurar a instalação push automática do cliente em todo o site.  

4.  No **base** separador > **definições** grupo, selecione **definições de instalação de cliente** > **instalação Push do cliente**.  

5.  Concluir o **as propriedades de instalação** separador.  

     [As propriedades de instalação de cliente](../../../core/clients/deploy/about-client-installation-properties.md) que estão especificadas neste separador são publicadas no Active Directory Domain Services caso o esquema é expandido para o Configuration Manager e lido pelas instalações de cliente em que o CCMSetup é executado sem propriedades de instalação.  

6.  Na consola do Configuration Manager, escolha **ativos e compatibilidade**.  

7.  Na área de trabalho **Ativos e Compatibilidade**, selecione um ou mais computadores, ou uma coleção de computadores.  

8.  No separador **Home Page**, escolha uma das seguintes opções:  

    -   Se pretender instalar o cliente para um único computador ou em vários computadores, no **dispositivo** grupo, selecione **instalar cliente**.  

    -   Se pretender instalar o cliente numa coleção de computadores, no **coleção** grupo, selecione **instalar cliente**.  

9. No **antes de começar** página do **Assistente de instalação do cliente**, reveja as informações e, em seguida, selecione **seguinte**.  

10. Concluir o **opções de instalação** página.  

11. Reveja as definições de instalação e, em seguida, feche o assistente.  

> [!NOTE]  
>  Pode utilizar o assistente para instalar clientes, mesmo que o site não esteja configurado para push de cliente.  

##  <a name="BKMK_ClientSUP"></a>Como instalar clientes com a instalação baseada em atualização de software  
 Instalação de cliente baseada em atualização de software publica o cliente para um ponto de atualização de software como uma atualização de software. Utilize este método para uma primeira instalação ou atualização.  

 Se um computador tiver o cliente instalado, o Configuration Manager oferece o cliente com a política de cliente, que inclui o nome do servidor de ponto de atualização de software e a porta a partir do qual pode obter as atualizações de software.   

> [!IMPORTANT]  
>  Para utilizar uma instalação baseada em atualizações de software, necessita de utilizar o mesmo servidor de Windows Server Update Services (WSUS) para a instalação do cliente e para as atualizações de software. Este servidor deverá ser o ponto de atualização de software ativo num site primário. Para obter mais informações, consulte o artigo [instalar um ponto de atualização de software](../../../sum/get-started/install-a-software-update-point.md).  

Se um computador não tiver o cliente do Configuration Manager instalado, tem de configurar e atribuir um objeto de política de grupo (GPO) nos serviços de domínio do Active Directory para especificar o nome de servidor de ponto de atualização de software.  

Não é possível adicionar propriedades de linha de comandos a uma instalação de cliente baseada em atualizações de software. Se tiver expandido o esquema do Active Directory para o Configuration Manager, computadores cliente consultarão automaticamente os serviços de domínio do Active as propriedades de instalação ao efetuar a instalação.  

Se não tiver expandido o esquema do Active Directory, poderá utilizar a Política de Grupo para aprovisionar as definições de instalação de cliente nos computadores do site. Estas definições são automaticamente aplicadas a quaisquer instalações de cliente baseadas em atualizações de software. Para obter mais informações, veja [Como Aprovisionar as Propriedades de Instalação de Cliente (Instalação de Cliente Baseada em Política de Grupo e em Atualização de Software)](#BKMK_Provision) e [Como atribuir clientes a um site no System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

Utilize os procedimentos seguintes para configurar computadores sem um cliente de Configuration Manager para utilizar a atualização de software ponto de software e de instalação de cliente das atualizações e, para publicar o cliente do ponto de atualização de software para o software.  

> [!NOTE]  
>  Se os computadores estiverem num estado de reinício pendente a seguir a uma instalação de software, uma instalação de cliente baseada em atualização de software pode causar o reinício do computador.  

### <a name="configure-a-group-policy-object-in-active-directory-domain-services-to-specify-the-software-update-point-for-client-installation-and-software-updates"></a>Configure um objeto de política de grupo nos serviços de domínio do Active Directory para especificar o ponto de atualização de software para atualizações de software e de instalação de cliente:  

1.  Utilize a Consola de Gestão de Política de Grupo para abrir um Objeto de Política de Grupo novo ou existente.  

2.  Na consola, expanda **configuração do computador**, expanda **modelos administrativos**, expanda **componentes do Windows**e, em seguida, escolha **Windows Update**.  

3.  Abra as propriedades da definição **especificar a localização de serviço de atualização de Microsoft na intranet**e, em seguida, escolha **ativado**.  

4.  Na caixa de **definir o serviço de atualização de intranet para detetar atualizações**, especifique o nome e a porta do servidor de ponto de atualização de software:  

    -   Se o sistema de sites do Configuration Manager estiver configurado para utilizar um nome de domínio completamente qualificado (FQDN), utilize o formato FQDN.  

    -   Se o sistema de sites do Configuration Manager não está configurado para utilizar um FQDN, utilize um formato de nome abreviado.  

    > [!NOTE]  
    >  Para determinar o número da porta, consulte o artigo [como determinar as definições de porta utilizadas pelo WSUS no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

     Exemplo: **http://server1.contoso.com:8530**  

5.  Na caixa de **definir o servidor de estatísticas de intranet**, especifique o nome do servidor de estatísticas de intranet. Não tem de ser o mesmo que o servidor de ponto de atualização de software e o formato tem de corresponder ao se for o mesmo servidor.  

6.  Atribua o objeto de política de grupo aos computadores nos quais pretende instalar o cliente e de receber atualizações de software.  

### <a name="to-publish-the-configuration-manager-client-to-the-software-update-point"></a>Para publicar o cliente do Configuration Manager no ponto de atualização de software  

1.  Na consola do Configuration Manager, clique em **administração** > **configuração do Site** > **Sites**.  

3.  Selecione o site para o qual pretende configurar a instalação de cliente baseada em atualização de software.  

4.  No **base** no separador de **definições** grupo, selecione **definições de instalação de cliente**e, em seguida, selecione **instalação de cliente baseada**.  

5.  Selecione **ativar a instalação de cliente baseada em atualização de software**.  

6.  Se o software de cliente no servidor do site do Configuration Manager for posterior à versão que no software do ponto de atualização de **detetada versão posterior do cliente pacote** é aberta a caixa de diálogo. Clique em **Sim** para publicar a versão mais recente.  

    > [!NOTE]  
    >  Se o software de cliente anteriormente não foi publicado para o software de ponto de atualização, esta caixa estará em branco.  

A atualização de software para o cliente do Configuration Manager não é automaticamente atualizada se existir uma nova versão. Se atualizar o site, incluindo uma nova versão de cliente, terá de repetir este procedimento e clicar em **Sim** no passo 6.  

##  <a name="BKMK_ClientGP"></a>Como instalar clientes com a política de grupo  
 Pode utilizar a política de grupo nos serviços de domínio do Active Directory para publicar ou atribuir o cliente do Configuration Manager para instalar em computadores na sua empresa. A instalar o cliente quando o computador for iniciado. Quando utilizar a política de grupo, o cliente será apresentado no painel de controlo **adicionar ou remover programas** para o utilizador instalar.  

 Utilize o pacote do Windows Installer (CCMSetup.msi) para instalações baseadas na Política de Grupo. Este ficheiro está localizado na pasta  **&lt;diretório de instalação do ConfigMgr\>\bin\i386** no servidor do site do Configuration Manager. Não é possível adicionar propriedades a este ficheiro para modificar o comportamento de instalação.  

> [!IMPORTANT]  
>  Tem de ter permissões de administrador para aceder aos ficheiros de instalação do cliente.  

-   Se o esquema do Active Directory é expandido para o Configuration Manager e **publicar este site nos serviços de domínio do Active Directory** está selecionada no **avançadas** separador do **propriedades do Site** caixa de diálogo, computadores cliente procuram automaticamente os serviços de domínio do Active Directory para as propriedades de instalação. Para obter mais informações sobre as propriedades de instalação publicadas, veja [Acerca das propriedades de instalação de cliente publicadas nos Serviços de Domínio do Active Directory no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

-   Se não tiver sido expandido o esquema do Active Directory, pode utilizar o procedimento neste tópico para armazenar propriedades de instalação no registo dos computadores: [Como aprovisionar as propriedades de instalação de cliente (instalação de cliente baseada em atualização de política de grupo e de Software)](#BKMK_Provision). Estas propriedades de instalação serão utilizadas quando o cliente está instalado.  

Para obter informações sobre como utilizar a Política de Grupo nos Serviços de Domínio do Active Directory para a instalação de software, veja a documentação do Windows Server.  

##  <a name="BKMK_Manual"></a>Como instalar clientes manualmente  
 Pode instalar manualmente o software de cliente em computadores na sua empresa utilizando o programa de CCMSetup.exe. Este programa e os respetivos ficheiros de suporte podem ser encontrados no **cliente** pasta da pasta de instalação do Configuration Manager no servidor do site e nos pontos de gestão no seu site. Esta pasta é partilhada na rede como  

 \\\\*&lt;Nome do servidor do site\>*\SMS_*&lt;código do Site\>*\Client\  

 onde  *&lt;nome do servidor de Site\>*  é o nome de um dos servidores que alojam um ponto de gestão e  *&lt;código do Site\>*  destina-se o código de site primário do cliente irão pertencer a.  Para executar CCMSetup.exe a partir da linha de comandos no cliente, tem de mapear uma unidade de rede para esta localização e, em seguida, execute o comando.  

> [!IMPORTANT]  
>  Tem de ter permissões de administrador para aceder aos ficheiros de instalação do cliente.  

 CCMSetup.exe copia todos os pré-requisitos necessários para o computador cliente e chama o pacote Windows Installer (Client. msi) para instalar o cliente. Não é possível executar Client.msi diretamente.  

 Pode especificar propriedades da linha de comandos para CCMSetup.exe e Client.msi para modificar o comportamento da instalação do cliente. Certifique-se de que especifica as propriedades de CCMSetup (as propriedades que começam por  **/** ) antes de especificar as propriedades de Client. msi. Por exemplo:  

```  
CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01  
```  
e o cliente instala, utilizando as seguintes propriedades:  

|Propriedade|Descrição|  
|--------------|-----------------|  
|**smsmp01**|Esta propriedade de CCMSetup especifica que o ponto de gestão SMSMP01 transfere os ficheiros de instalação de cliente necessários.|  
|**/logon**|Esta propriedade de CCMSetup Especifica que a instalação deverá ser interrompida se for encontrado um cliente existente do Configuration Manager no computador.|  
|**SMSSITECODE = AUTO**|Esta propriedade de Client. msi Especifica que o cliente tenta localizar o código do site do Configuration Manager para utilizar, por exemplo, utilizando os serviços de domínio do Active Directory.|  
|**FSP = SMSFP01**|Esta propriedade de Client.msi especifica que o ponto de estado de contingência com o nome SMSFP01 será utilizado para receber mensagens de estado enviadas pelo computador cliente.|  

 Para detalhes sobre todas as propriedades de CCMSetup.exe, veja [Acerca das propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="examples"></a>Exemplos
 Estes exemplos dizem respeito a clientes do Active Directory na intranet e utilizam os seguintes valores para representar diferentes aspetos do site:  

 **MPSERVER** = o servidor que aloja o ponto de gestão   
**FSPSERVER** = o servidor que aloja o ponto de estado de contingência  
**ABC** = código do site  
**contoso.com** = nome do domínio  

 Todos os servidores de sistema de site são configurados com um FQDN de intranet e o site é publicado na floresta do cliente do Active Directory.  

 No computador cliente, iniciar sessão como um administrador local, mapear uma unidade (z:)) para\\\MPSERVER\SMS_ABC\Client, mude de comandos para a unidade de z e, em seguida, execute um dos seguintes comandos.  

 **Exemplo 1:**  

```  
CCMSetup.exe  
```  
Este exemplo instala o cliente sem propriedades adicionais para que o cliente é automaticamente configurado com as propriedades de instalação de cliente publicadas nos serviços de domínio do Active. Por exemplo, o cliente é automaticamente configurado para o código do site (requer a localização de rede do cliente seja incluída num grupo de limites que esteja configurado para atribuição de cliente), um ponto de gestão, o ponto de estado de contingência e se o cliente deve comunicar utilizando apenas HTTPS. Para obter mais informações sobre as propriedades de instalação do cliente que podem ser configuradas automaticamente para clientes do Active Directory, veja [Acerca das propriedades de instalação de cliente publicadas nos Serviços de Domínio do Active Directory no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 **Exemplo 2:**  

```  
CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com  
```  
Este exemplo substitui a configuração automática que serviços de domínio do Active Directory possam fornecer e requer que a localização de rede do cliente seja incluída num grupo de limites que esteja configurado para atribuição de cliente. Em vez disso, a instalação especifica o site, um ponto de gestão da intranet e um ponto de gestão baseado na Internet, um ponto de estado de contingência que aceita ligações da Internet e a utilização de um certificado PKI de cliente (se disponível) com a maior validade possível.  

##  <a name="BKMK_ClientLogonScript"></a>Como instalar clientes com scripts de início de sessão  
 O Configuration Manager suporta scripts de início de sessão para instalar o software de cliente do Configuration Manager. Pode utilizar o ficheiro de programa **CCMSetup.exe** num script de início de sessão para acionar a instalação do cliente.  

 A instalação com script de início de sessão utiliza os mesmos métodos da instalação manual de cliente. Pode especificar a propriedade de instalação **/logon** de CCMSetup.exe, que impede a instalação do cliente se já existir uma versão do cliente no computador. Isto impede a reinstalação do cliente cada vez que o script de início de sessão for executado.  

 Se não for especificada nenhuma origem de instalação que está a utilizar o **/origem** propriedade e nenhum ponto de gestão a partir do qual obter a instalação é especificada utilizando o **/MP** propriedade CCMSetup.exe pode localizar o ponto de gestão pesquisando os serviços de domínio do Active Directory se o esquema tiver sido expandido para o Configuration Manager e o site esteja publicado nos serviços de domínio do Active. Em alternativa, o cliente pode utilizar DNS ou WINS para localizar um ponto de gestão.  

##  <a name="BKMK_ClientApp"></a>Como instalar clientes com um pacote e programa  
 Pode utilizar o Configuration Manager para criar e implementar um pacote e programa que Atualize o software de cliente para computadores selecionados na sua hierarquia. Um ficheiro de definição de pacote que povoa as propriedades do pacote com valores normalmente utilizados é fornecido com o Configuration Manager. Pode personalizar o comportamento da instalação do cliente especificando propriedades de linha de comandos adicionais.  

> [!NOTE]  
>  Não é possível atualizar clientes do Configuration Manager 2007 com este método. Em vez disso, utilize a atualização automática de cliente, que cria e implementa automaticamente um pacote com a versão mais recente do cliente. Para obter mais informações, veja [Atualização dos clientes no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md).  
>   
>  Para obter mais informações sobre como migrar a partir de versões mais antigas do cliente do Configuration Manager, consulte o artigo [planear uma estratégia de migração do cliente no System Center Configuration Manager](../../../core/migration/planning-a-client-migration-strategy.md).  

 
###<a name="to-create-a-package-and-program-for-the-client-software"></a>Para criar um pacote e programa para o software de cliente  

Utilize o procedimento seguinte para criar um pacote do Configuration Manager e um programa que pode implementar em computadores de cliente do Configuration Manager para atualizar o software de cliente.  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **pacotes**.  

3.  No **base** separador o **criar** grupo, selecione **criar pacote a partir da definição**.  

4.  No **definição de pacote** página do assistente, selecione **Microsoft** a partir do **Publisher** na lista pendente e selecione **atualização de cliente do Configuration Manager** a partir do **definição do pacote** lista.  

5.  No **ficheiros de origem** página, selecione **obter sempre ficheiros da pasta de origem**.  

6.  No **pasta de origem** página, selecione **caminho de rede (nome UNC)** e introduza o caminho de rede do computador e a pasta que contém os ficheiros de instalação de cliente.  

    > [!NOTE]  
    >  O computador no qual a execução de implementação do Configuration Manager tem de ter acesso à pasta de rede que especificou, caso contrário, a instalação irá falhar.  

    Se pretender alterar qualquer uma das propriedades de instalação do cliente, pode modificar os parâmetros da linha de comandos de CCMSetup.exe no separador **Geral** da caixa de diálogo **Propriedades da Atualização silenciosa do agente do Configuration Manager**. As propriedades de instalação predefinidas são **/noservice SMSSITECODE=AUTO**.  

9. Distribua o pacote por todos os pontos de distribuição que pretende que alojem o pacote de atualização de cliente. Em seguida, pode implementar o pacote de coleções de computadores que contenham clientes que pretende atualizar.  

## <a name="how-to-install-clients-to-intune-mdm-managed-windows-devices"></a>Como instalar clientes em dispositivos Windows geridos por MDM do Intune

Pode implementar os ficheiros de instalação de cliente em computadores que estão inscritos com o Microsoft Intune. 

Para garantir que o dispositivo permanece num Estado de gerido depois do software de cliente é instalado, o dispositivo tem de estar na rede da empresa e dentro de um limite de site do Configuration Manager. 

> [!NOTE]
> Depois do software de cliente é instalado, o dispositivo será anulado do Intune.

### <a name="to-install-clients-with-intune"></a>Para instalar clientes com o Intune:

1. No Intune, [criar uma aplicação](/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune) que contém o ficheiro de instalação de cliente do Configuration Manager **ccmsetup**.

2. O Intune Software Publisher, utilize os seguintes parâmetros de linha de comandos:

  **CCMSETUPCMD = "/ MP:&lt;FQDN do ponto de gestão > SMSMP =&lt;FQDN do ponto de gestão > SMSSITECODE =&lt;o código do site > DNSSUFFIX =&lt;sufixo DNS de ponto de gestão >"**

3. [Implementar a aplicação](/intune/deploy-use/deploy-apps-in-microsoft-intune) para os computadores inscritos do Windows.

##  <a name="BKMK_ClientImage"></a>Como instalar clientes com uma imagem do computador  
É possível pré-instalar o software de cliente do Configuration Manager no computador de imagem original que irá utilizar para a imagem de outros computadores.   

### <a name="to-prepare-the-client-computer-for-imaging"></a>Para preparar o computador cliente para a implementação da imagem  

1.  Instale manualmente o software de cliente do Configuration Manager no computador de imagem original. Para obter mais informações, veja [Como Instalar Manualmente Clientes do Configuration Manager](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Não especifique um código de site do Configuration Manager para o cliente nas propriedades da linha de comandos CCMSetup.exe.  

2.  Numa linha de comandos, escreva **net stop ccmexec** para assegurar que o serviço **Anfitrião de Agente do SMS** (Ccmexec.exe) não está em execução no computador com a imagem principal.  

3.  Remova os certificados armazenados no arquivo de computador local do computador com a imagem principal.  Por exemplo, se utilizar certificados de infraestrutura de chaves públicas (PKI), terá de remover os certificados do arquivo **Pessoal** de **Computador** e de **Utilizador** antes de criar a imagem do computador.

4.  Se os clientes forem instalados numa hierarquia do Configuration Manager diferente do computador de imagem principal, remova a chave de raiz fidedigna a partir do computador de imagem original.  
    > [!NOTE]  
    >  Se os clientes não conseguirem consultar os Serviços de Domínio do Active Directory para localizar um ponto de gestão, utilizarão a chave de raiz fidedigna para determinar os pontos de gestão fidedignos. Se todos os clientes instalados por imagem se destinarem a ser implementados na mesma hierarquia do computador principal, não remova a chave de raiz fidedigna. Se os clientes se destinarem a ser implementados em hierarquias diferentes, remova a chave de raiz fidedigna e, como melhor prática, aprovisione antecipadamente estes clientes com a nova chave de raiz fidedigna. Para obter mais informações, veja [Planear a Chave de Raiz Fidedigna](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK). 

5.  Utilize o software de processamento de imagens para capturar a imagem do computador principal.  

6.  Implemente a imagem nos computadores de destino.  

##  <a name="BKMK_ClientWorkgroup"></a>Como instalar clientes em computadores de grupo de trabalho  
 O Configuration Manager suporta a instalação do cliente para computadores em grupos de trabalho. Instale o cliente em computadores de grupo de trabalho através do método especificado em [Como Instalar Manualmente Clientes do Configuration Manager](#BKMK_Manual).  

 Pré-requisitos:  

-   O cliente deve ser instalado manualmente em cada computador de grupo de trabalho. Durante a instalação, o utilizador com sessão iniciada tem de ter direitos de administrador local.  

-   Para poder aceder aos recursos no domínio do servidor de site do Configuration Manager, a conta de acesso à rede tem de ser configurada para o site. Especifica esta conta como uma propriedade de componente de distribuição de software. Para obter mais informações, veja [Componentes do site para o System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

 Limitações:  

-   Os clientes de grupo de trabalho não podem localizar pontos de gestão dos Serviços de Domínio do Active Directory e, em vez disso, devem utilizar DNS, WINS ou outro ponto de gestão.  

-   Não é suportado roaming global, uma vez que os clientes não conseguem consultar os Serviços de Domínio do Active Directory para obter informações do site.  

-   Os métodos de deteção do Active Directory não conseguem detetar computadores em grupos de trabalho.  

-   Não é possível implementar software para utilizadores de computadores de grupo de trabalho.  

-   Não é possível utilizar o método de instalação push de cliente para instalar o cliente em computadores de grupo de trabalho.  

-   Os clientes de grupo de trabalho não podem utilizar Kerberos para autenticação e poderão necessitar de aprovação manual.  

-   Não é possível configurar um cliente de grupo de trabalho como ponto de distribuição. O Configuration Manager requer que ponto de distribuição computadores sejam membros de um domínio.  

### <a name="to-install-the-client-on-workgroup-computers"></a>Para instalar o cliente em computadores de grupo de trabalho  

Verifique os pré-requisitos, em seguida, siga as instruções na secção [como instalar clientes manualmente do Configuration Manager](#BKMK_Manual).  

   Este exemplo instala o cliente para gestão de clientes na intranet e especifica o código do site e o sufixo DNS para localizar um ponto de gestão:`**CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com**`  

     

   Este exemplo requer que o cliente se encontre numa localização de rede que esteja configurada num grupo de limites para que a atribuição automática do site possa ser bem-sucedida. O comando inclui um ponto de estado de contingência num servidor FSPSERVER, para ajudar a monitorizar a implementação do cliente e identificar quaisquer problemas de comunicação de cliente:`**CCMSetup.exe FSP=fspserver.constoso.com**`  

      

##  <a name="BKMK_ClientInternet"></a>Como instalar clientes para gestão de clientes baseados na Internet  
 Quando o site do Configuration Manager suporta a gestão de clientes baseada na Internet para clientes que umas vezes estão na intranet e, por vezes na Internet, tem duas opções ao instalar clientes na intranet:  

-   Pode incluir a propriedade de Client. msi de CCMHOSTNAME =*&lt;FQDN de Internet do ponto de gestão baseado na Internet\>*  quando instala o cliente, por exemplo, utilizando push de cliente ou a instalação manual. Se utilizar este método, deve também atribuir diretamente o cliente ao site e não pode utilizar a atribuição automática do site. A secção [Como Instalar Manualmente Clientes do Configuration Manager](#BKMK_Manual) deste tópico fornece um exemplo deste método de configuração.  

-   Pode instalar o cliente para gestão de clientes na intranet e, em seguida, atribuir uma gestão de clientes baseada na Internet aponte para o cliente utilizando as propriedades do cliente do Configuration Manager no painel de controlo, ou utilizando um script. Se utilizar este método, pode utilizar a atribuição automática de clientes. Para obter mais informações, veja a secção [Como Configurar Clientes para Gestão de Clientes baseada na Internet após a Instalação do Cliente](#BKMK_ConfigureIBCM_MP) deste tópico.  

 Se tiver de instalar clientes que se encontram na Internet, quer porque são clientes apenas de Internet ou porque devem ser instalados antes de regressarem à intranet, escolhe um dos seguintes métodos suportados:  

-   Forneça um mecanismo para estes clientes liguem temporariamente à intranet com uma rede privada virtual (VPN) e, em seguida, instalá-las utilizando um método de instalação de cliente adequado.  

-   Utilize um método de instalação que seja independente do Configuration Manager, como o empacotamento dos ficheiros de origem de instalação de cliente num suporte de dados amovível que pode enviar aos utilizadores para instalar com as instruções. Os ficheiros de origem de instalação de cliente estão localizados no  *&lt;Caminhodainstalação\>*pasta \cliente os pontos de gestão e servidor de site do Configuration Manager. Inclua no suporte de dados um script para copiar e substituir manualmente a pasta do cliente e, a partir desta pasta, instale o cliente, utilizando CCMSetup.exe e todas as propriedades da linha de comandos CCMSetup.exe adequadas.  

> [!NOTE]  
>  O Configuration Manager não suporta a instalação do cliente diretamente a partir do ponto de gestão baseado na Internet ou a partir do ponto de atualização de software baseado na Internet.  

 Uma vez que os clientes que são geridos através da Internet têm de comunicar com sistemas de sites baseados na Internet, certifique-se de que estes clientes também têm certificados de infraestrutura de chaves públicas (PKI) instalados antes de os instalar. Tem de instalar estes certificados independentemente do Configuration Manager. Para obter mais informações sobre os requisitos de certificado, veja [Requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

### <a name="to-install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Para instalar clientes na Internet através da especificação de propriedades da linha de comandos CCMSetup  

1.  Siga as instruções da secção [Como instalar Manualmente Clientes do Configuration Manager](#BKMK_Manual) e inclua sempre o seguinte:  

    -   Propriedade da linha de comandos do CCMSetup **/Source:***&lt;caminho local para a pasta copiado do cliente\>*  

    -   Propriedade da linha de comandos CCMSetup **/UsePKICert**  

    -   Propriedade Client. msi **CCMHOSTNAME =***&lt;ponto de gestão baseado na FQDN de Internet\>*  

    -   Propriedade Client. msi **SMSSIGNCERT =***&lt;caminho local para o certificado de assinatura do servidor de site exportado\>*  

    -   Propriedade Client. msi **SMSSITECODE =***&lt;código do ponto de gestão baseado na Internet do site\>*  

    > [!NOTE]  
    >  Se o site tiver vários pontos de gestão baseados na Internet, não é relevante o ponto de gestão baseado na Internet que é especificado para a propriedade CCMHOSTNAME. Quando um cliente do Configuration Manager liga ao ponto de gestão baseado na Internet especificado, o ponto de gestão envia ao cliente uma lista de pontos de gestão baseado na Internet disponíveis no site e o cliente seleciona aleatoriamente um da lista.  

2.  Se não quiser que o cliente verifique a lista de revogação de certificados (CRL), especifique a propriedade da linha de comandos CCMSetup **/NoCRLCheck**.  

3.  Se estiver a utilizar um ponto de estado de contingência baseado na Internet, especifique a propriedade de Client. msi **FSP =***&lt;FQDN de Internet do ponto de estado de contingência baseado na Internet\>*.  

4.  Se estiver a instalar o cliente para gestão de clientes apenas de Internet, especifique a propriedade de Client.msi **CCMALWAYSINF=1**.  

5.  Verifique se é necessário especificar propriedades de linha de comandos CCMSetup adicionais. Por exemplo, poderá ter de especificar um critério de seleção de certificados se o cliente tiver mais do que um certificado PKI válido. Para obter uma lista de todas as propriedades disponíveis, veja [Acerca das propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

   Exemplo: `**CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1**`  

   Este exemplo instala os ficheiros de origem do cliente a partir de uma pasta da unidade D com definições para utilizar um certificado PKI de cliente e selecionar o certificado com o período de validade mais longo para a gestão de clientes apenas de Internet, atribui o cliente para utilizar o ponto de gestão baseado na Internet com o nome SERVER1 e o ponto de estado de contingência baseado na Internet no domínio contoso.com e atribui o cliente ao site ABC.  

###  <a name="BKMK_ConfigureIBCM_MP"></a>Para configurar clientes para gestão de clientes baseados na Internet após a instalação de cliente  
 Para atribuir o ponto de gestão baseado na Internet após a instalação do cliente, utilize um dos procedimentos seguintes. O primeiro requer configuração manual e é adequado para alguns clientes. O segundo é mais adequado para a configuração de muitos clientes.  

#### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>Para configurar clientes para gestão de clientes baseada na Internet após a instalação de cliente através da atribuição do ponto de gestão baseado na Internet nas Propriedades do Configuration Manager  

1.  Navegue para **Configuration Manager** no Painel de Controlo do computador cliente e, em seguida, faça duplo clique para abrir as respetivas propriedades.  

2.  No separador **Internet**, introduza o nome de domínio completamente qualificado do ponto de gestão baseado na Internet na caixa de texto FQDN de Internet.  

    > [!NOTE]  
    >  O separador **Internet** só está disponível se o cliente tiver um certificado PKI de cliente.  

3.  Introduza as definições do servidor proxy se o cliente for aceder à Internet através de um servidor proxy.  

#### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Para configurar clientes para a gestão de clientes baseada na Internet após a instalação de cliente através de um script  

1.  Abra um editor de texto, como o Bloco de Notas.  

2.  Copie e insira o seguinte no ficheiro. Substitua *mp.contoso.com* pelo FQDN de Internet do seu ponto de gestão baseado na Internet.  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the Internet-Based Management Point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

    > [!NOTE]  
    >  Se tiver de eliminar um ponto de gestão baseado na Internet especificado para que o cliente não seja configurado para utilizar um ponto de gestão baseado na Internet, remova o valor que se encontra entre aspas para que a linha fique com o aspeto **newInternetBasedManagementPointFQDN = ""**.  

4.  Guarde o ficheiro com uma extensão .vbs.  

5.  Utilize cscript para executar o script em computadores cliente, utilizando um dos seguintes métodos:  

    -   Implemente o ficheiro nos clientes existentes do Configuration Manager, utilizando um pacote e um programa.  

    -   Execute o ficheiro localmente nos clientes existentes do Configuration Manager, fazendo duplo clique no ficheiro de script no Explorador do Windows.  

 Poderá ter de reiniciar o cliente para que as alterações surtam efeito.  

##  <a name="BKMK_Provision"></a>Como aprovisionar as propriedades de instalação de cliente (grupo política e o software de cliente baseada em atualização instalação)  
 Pode utilizar a política de grupo do Windows para aprovisionar computadores com propriedades de instalação de cliente do Configuration Manager. Estas propriedades são armazenadas no registo do computador e são lidas quando o software de cliente é instalado. Este procedimento não seria normalmente necessário, mas poderá ser necessário para alguns cenários de instalação de cliente, tais como:  

-   Estiver a utilizar as definições de política de grupo ou métodos de instalação de cliente baseada em atualização de software e não tiver expandido o esquema do Active Directory para o Configuration Manager.  

-   Pretende substituir propriedades de instalação de cliente em computadores específicos.  

> [!NOTE]  
>  Se forem fornecidas quaisquer propriedades de instalação na linha de comandos CCMSetup.exe, as propriedades de instalação aprovisionadas nos computadores não serão utilizadas.  

 Um modelo administrativo de política de grupo com o nome Configmgrinstallation é fornecido no suporte de instalação do Configuration Manager, que pode ser utilizados para aprovisionar computadores cliente com propriedades de instalação.   

### <a name="to-configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Para configurar e atribuir propriedades de instalação de cliente através de um Objeto de Política de Grupo  

1.  Importe o modelo administrativo ConfigMgrInstallation.adm para um Objeto de Política de Grupo novo ou existente, utilizando um editor, tal como o Editor de Objetos de Política de Grupo do Windows. O ficheiro pode ser encontrado na pasta **TOOLS\ConfigMgrADMTemplates** no suporte de instalação do Configuration Manager.  

2.  Abra as propriedades da definição importada **Configurar Definições de Implementação de Cliente**.  

3.  Escolher **ativada**.  

4.  Na caixa **CCMSetup**, introduza as propriedades da linha de comandos CCMSetup necessárias. Para obter uma lista de todas as propriedades de linha de comandos CCMSetup e exemplos da sua utilização, veja [Acerca das propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

5.  Atribua o objeto de política de grupo aos computadores que pretende aprovisionar com as propriedades de instalação do cliente do Configuration Manager.  

 Para obter informações sobre Política de Grupo do Windows, consulte a documentação do Windows Server.  

### <a name="see-also"></a>Consulte também
[Métodos de instalação de cliente no System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md)

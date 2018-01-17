---
title: "Notas de versão"
titleSuffix: MDT 2013 release notes
description: "Compreenda os pré-requisitos e limitações da Microsoft implementação Toolkit 2013. "
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: article
ms.assetid: 6e32ce6d-585d-4801-a345-ff0f6f2d90ad
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 11b3eb6ed778cca78823c58b606d98166ded9b55
ms.sourcegitcommit: 645cd5a324bdd299906efa27eaca5885eafc9e9c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/16/2018
---
# <a name="microsoft-deployment-toolkit-2013-release-notes"></a>Notas de versão do Microsoft Deployment Toolkit 2013  
 Bem-vindo às notas de versão para o Microsoft® Deployment Toolkit (MDT) 2013. Leia estas notas de versão cuidadosamente antes de instalar o MDT 2013, que contêm informações que necessárias para instalar o toolkit de que a documentação de ajuda do MDT 2013 não pode abranger com êxito.  

 Esta versão suporta a implementação do Windows 8.1, Windows 8, Windows 7, dinâmico do PC Windows, Windows Embedded POSReady 7 (POSReady 7), Windows Server 2012 R2, Windows Server 2012 e sistemas de operativos do Windows Server 2008 R2. Consulte a biblioteca de documentação do Toolkit do Microsoft implementação, a qual está incluído com o MDT 2013, para a documentação completa para esta versão.  

> [!NOTE]
>  Neste documento, *Windows* aplica-se aos sistemas operativos Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2, exceto indicação em contrário. MDT não suporta ARM processador versões do Windows. Da mesma forma, *MDT* refere-se ao MDT 2013, salvo indicação em contrário.  

## <a name="prerequisites"></a>Pré-requisitos  
 Para implementações do Lite Touch Installation (LTI), o MDT requer os seguintes componentes:  

 Para instalar o MDT no:  

-   Windows 7 ou Windows Server 2008 R2 instale ou ative os seguintes componentes no computador no qual instala o MDT:  

    -   Versão da consola de gestão da Microsoft 3.0  

    -   O Microsoft .NET Framework 3.5 com Service Pack 1 (SP1)  

    -   Windows PowerShell™ versão 2.0  

    -   Windows Assessment e Deployment Kit (ADK) para Windows 8.1 (componentes de ferramentas de implementação, o Windows PE e o User State Migration Tool)  

-   Windows 8.1, Windows 8, Windows Server 2012 R2 ou Windows Server 2012, instale ou ative os seguintes componentes no computador no qual instala o MDT:  

    -   Windows ADK para Windows 8.1 (componentes de ferramentas de implementação, o Windows PE e o User State Migration Tool)  

    -   O Microsoft .NET Framework 4.0 (que está incluído no sistema operativo)  

    -   O Windows PowerShell versão 3.0 (que está incluído no sistema operativo)  

 Para implementações de Zero Touch instalação (ZTI), o MDT requer os seguintes componentes:  

-   Microsoft System Center 2012 R2 Configuration Manager  

> [!NOTE]
>  Consulte a documentação de produto do Configuration Manager para obter requisitos adicionais.  

 Para implementações de modo instalação (UDI), o MDT requer os seguintes componentes:  

-   Microsoft System Center 2012 R2 Configuration Manager  

-   Microsoft System Center 2012 Configuration Manager  

-   Microsoft System Center Configuration Manager 2007 R3  

> [!NOTE]
>  Consulte a documentação de produto do Configuration Manager para obter requisitos adicionais.  

 Para iniciar os runbooks do Microsoft System Center 2012 R2 Orchestrator com o MDT, instale o [actualização do ADO.NET Data Services para .NET Framework 3.5 SP1 para Windows 7 e Windows Server 2008 R2](http://www.microsoft.com/download/details.aspx?displaylang=en&id=2343).  

## <a name="installing-mdt"></a>Instalar o MDT  
 Certifique-se de que tem uma cópia de segurança completa do seu servidor antes de instalar o MDT num computador que tenha uma instalação existente do MDT.  

 O processo de instalação do MDT remove quaisquer instâncias existentes do MDT instalado no mesmo computador. Partilhas de implementação, pontos de distribuição e as bases de dados existentes são preservados durante este processo, mas tem de ser atualizados quando a instalação estiver concluída.  

### <a name="support-for-upgrading-from-previous-versions-of-mdt"></a>Suporte para atualizar a partir de versões anteriores do MDT  
 MDT 2013 suporta as seguintes versões do MDT a atualizar:  

-   MDT 2012 Update 1  

> [!NOTE]
>  Crie uma cópia de segurança da infraestrutura existente do MDT antes de tentar uma atualização.  

### <a name="usmt-download-requirements"></a>Requisitos de transferência do USMT  
 Já não precisam de separadamente transferir o Windows utilizador State Migration Tool (USMT). Versão 6 do USMT faz parte do Windows ADK para Windows 8.1. USMT 6 suporta captura estado do utilizador de todas as versões do Windows 8.1, Windows 8 e Windows 7.  

### <a name="the-lti-upgrade-process"></a>O processo de atualização de LTI  
 Após a instalação do MDT, pode atualizar uma partilha de implementação existente executando o Assistente de partilha de implementação abra partir do nó de partilhas de implementação no Deployment Workbench. Especifique o caminho para o diretório de partilha de implementação existente e, em seguida, selecione o **atualizar** caixa de verificação. Tenha em atenção que se o fizer, também atualiza partilhas de implementação de rede existente e partilhas de implementação de suportes de dados, pelo que as devem ser acessíveis. Não execute esta atualização ao efetuar implementações, porque os ficheiros em utilização podem causar problemas a atualização.  

### <a name="the-zti-upgrade-process"></a>O processo de atualização de ZTI  
 Não são modificadas durante o processo de instalação do MDT e devem continuar a funcionar sem qualquer problema existentes sequências de tarefas de MDT presente no System Center 2012 Configuration Manager. Não foi fornecido nenhum mecanismo para atualizar estas sequências de tarefas. Se pretender utilizar qualquer uma das novas funcionalidades do MDT, crie novos sequências de tarefas.  

 Quando o processo de atualização está concluído:  

-   **Execute a configurar o Assistente de integração do ConfigMgr.** Tem de executar este assistente após a atualização para registar os componentes novos e instalar os modelos de sequência de tarefas ZTI atualizados.  

-   **Certifique-se que crie um novo pacote de ficheiros do Microsoft implementação Toolkit para qualquer nova ZTI as sequências de tarefas que cria.** Pode utilizar o pacote de ficheiros de Toolkit do Microsoft implementação existente para sequências de tarefas ZTI criadas antes da atualização, mas tem de criar um novo pacote de ficheiros do Microsoft implementação Toolkit para sequências de tarefas do novo ZTI.  

## <a name="known-issues"></a>Problemas Conhecidos  
 Os problemas conhecidos do MDT 2013 são classificados da seguinte forma:  

-   Para problemas gerais, conforme descrito em [conhecido problemas gerais](#KnownIssue)  

-   Para implementações de LTI apenas, conforme descrito em [problemas conhecidos para implementações LTI apenas](#KnownIssuesLTI)  

-   Para implementações LTI e ZTI, conforme descrito em [problemas conhecidos para LTI e implementações ZTI](#KnownIssuesLTIZTI)  

-   Para implementações de UDI, conforme descrito em [problemas conhecidos para implementações de UDI](#KnownIssuesUDI)  

###  <a name="KnownIssue"></a>Problemas conhecidos de geral  
 Os seguintes problemas não são específicos para qualquer método de implementação.  

#### <a name="compiled-html-help-files-are-not-up-to-date"></a>Ficheiros de ajuda HTML compilados não estão atualizados  
 Compilado todos os ficheiros de ajuda HTML (. CHM) incluído com o MDT 2013, incluindo "Library.chm da documentação do Toolkit de implementação de Microsoft" e "Versão Notes.chm" são atual a partir da versão do MDT 2012 Update 1. Todas as ligações "Ajuda" no Deployment Workbench irão abrir conteúdo destes ficheiros.  

 SOLUÇÃO: Este documento contém as notas de versão para o MDT 2013 e substitui "Versão Notes.chm" no diretório de instalação.  

 Uma biblioteca de documentação do MDT atualizado no formato Microsoft Word for planeada para estar disponível a partir do Microsoft Download Center.  

#### <a name="modifying-key-task-sequence-steps-can-lead-to-unpredictable-results"></a>Modificar os passos de sequência de tarefas chave pode originar resultados imprevisíveis  
 Modificar o **instalar sistema operativo** passo de sequência de tarefas ou **aplicar imagem do sistema operativo** passo de sequência de tarefas após a criação do passo de sequência de tarefas pode originar resultados imprevisíveis. Por exemplo, se criar uma sequência de tarefas para implementar uma imagem do Windows 7 de 32 bits e, em seguida, posteriormente, altera o **instalar sistema operativo** passo de sequência de tarefas ou **aplicar imagem do sistema operativo** passo de sequência de tarefas para fazer referência a uma imagem do Windows 7 de 64 bits, a sequência de tarefas poderá não executado com êxito.  

 SOLUÇÃO: Crie uma nova sequência de tarefas para implementar uma imagem de sistema operativo diferente.  

#### <a name="domain-join-fails-when-an-organizational-unit-ou-contains-special-characters"></a>Associação a um domínio falha quando uma unidade organizacional (UO) contém carateres especiais  
 Falha na associação a um domínio quando uma unidade organizacional (UO) contém carateres especiais em formato Unicode. Se o nome da UO tiver espaços, os métodos descritos abaixo devem funcionar corretamente. Se a UO tem outros carateres, por exemplo, carateres de específicas do idioma, substitua os carateres com os respetivos equivalentes de carateres ANSI. Por exemplo, deverá alterar Cońtoso para Contoso.  

 SOLUÇÃO: Selecione um dos seguintes métodos para resolver este problema:  

-   Utilize o **MachineObjectOU** propriedade, conforme mostrado no exemplo seguinte, para especificar a unidade organizacional para o computador no ficheiro CustomSettings.ini, ou na base de dados do MDT (BD do MDT).  

    ```  
    [Settings]   
    Priority=MacAddress, Default   
    Properties=MyCustomProperty   

    [Default]   
    OSinstall=Y  

    [00:15:1d:ee:2a:aa]   
    OSDComputername=WDG-CLI-01   
    MachineObjectOU=OU=HelpDesk,OU=Corp,DC=Woodgrovebank,DC=com  
    ```  

-   Utilize o **DomainOUs** propriedade, conforme mostrado no exemplo seguinte, para criar uma lista de UOs no ficheiro CustomSettings.ini, ou a base de dados do MDT que podem ser selecionadas no Assistente de implementação.  

    ```  
    [Settings]   
    Priority=MacAddress, Default   
    Properties=MyCustomProperty   

    [Default]  
    OSInstall=Y  
    SkipAppsOnUpgrade=YES  
    SkipCapture=YES  
    SkipAdminPassword=NO  
    SkipProductKey=YES  
    DoCapture=YES  
    DomainOUs1=OU=Users,OU=Corp,DC=Woodgrovebank,DC=com   
    DomainOUs2=OU=HelpDesk,OU=corp,DC=Woodgrovebank,DC=com  
    ```  

-   Utilize o ficheiro de DomainOUList.xml, conforme mostrado no exemplo seguinte, para criar uma lista de UOs que podem ser selecionados no Assistente de implementação.  

    ```  
    <?xml version="1.0" encoding="utf-8"?>   
    <DomainOUs>   
       <DomainOU>   
          OU=Users,OU=Corp,DC=Woodgrovebank,DC=com  
       </DomainOU>   
       <DomainOU>   
         OU=HelpDesk,OU=corp,DC=Woodgrovebank,DC=com  
       </DomainOU>   
    </DomainOUs>  
    ```  

     Pode criar o ficheiro de DomainOUList.xml utilizando qualquer XML editor. Coloque o ficheiro de DomainOUList.xml na pasta de Scripts numa partilha de implementação para LTI ou no pacote de ficheiros MDT para ZTI e UDI.  

#### <a name="configure-adds-step-does-not-have-an-option-for-windows-server-2012-domain-and-forest-functional-levels"></a>Configurar o ADDS passo não tem uma opção para os níveis funcionais do Windows Server 2012 domínio e floresta  
 Quando configurar opções avançadas para o passo "Configurar adiciona" as listas de nível funcional da floresta e o nível funcional do domínio não tem uma opção para o Windows Server 2012.  

 SOLUÇÃO: Definir DomainLevel = 5 e/ou ForestLevel = 5 no CustomSettings.ini. Consulte a referência do Toolkit para obter mais detalhes sobre estas definições.  

#### <a name="gpo-packs-do-not-exist"></a>Não existem pacotes de GPO  
 Os pacotes de GPO Security Compliance Manager (SCM) não estão incluídos com o MDT 2013. O passo "Aplicar pacote Local GPO" (ZTIApplyGPOPack.wsf) irá iniciar uma entrada semelhante a um dos seguintes:  

 "O caminho do pacote de GPO – Templates\GPOPacks\ não é válido. O GPO não foi aplicado."  

 "MDT GPO pacote predefinido não está presente para este sistema operativo."  

 SOLUÇÃO: Crie a subpasta GPOPacks em modelos na partilha de implementação (por exemplo, C:\DeploymentShare\Templates\GPOPacks). Exportar uma cópia de segurança do GPO de SCM ou GPMC e, em seguida, adicione os seguintes ficheiros do SCM:  

-   GPOPack.wsf  

-   LocalPol.exe  

-   LocalSecurityDB.sdb  

 Crie uma subpasta em GPOPacks e copie este conteúdo. Em seguida, especifique o nome do diretório na propriedade GPOPackPath no CustomSettings.ini.  

#### <a name="the-configuration-manager-console-will-crash-if-mdt-is-uninstalled-without-removing-the-console-extensions"></a>Consola do Configuration Manager irá falhar se o MDT é desinstalado sem remover as extensões da consola.  
 Quando executar **configurar a integração do ConfigMgr**, se desmarque a opção **remover as extensões de MDT para o Configuration Manager 2012**, o erro seguinte irá ocorrer ao tentar iniciar o Consola do Configuration Manager:  

```  
Couldn’t load sqmapi.dll from bin\x86\sqmapi.dll. Last Error = (126)  
```  

 SOLUÇÃO: Nenhum  

#### <a name="oobe-settings-missing-from-windows-81-unattendxml-template"></a>Definições de OOBE em falta do modelo de Unattend.xml do Windows 8.1  
 Sequências de tarefas do Windows 8.1 utilizam um modelo de Unattend.xml anterior que não inclua várias propriedades no < OOBE\> secção, tal como HideWirelessSetupInOOBE, que pode exigir a interação manual com implementações de sistemas com sem fios adaptadores de rede.  

 SOLUÇÃO: Adicione as seguintes entradas para o < OOBE\> secção das sequências de tarefas Unattend.xml para Windows 8.1.  

```  
<OOBE>  
    <HideEULAPage>true</HideEULAPage>  
    <NetworkLocation>Work</NetworkLocation>  
    <ProtectYourPC>1</ProtectYourPC>  
    <HideLocalAccountScreen>true</HideLocalAccountScreen>  
    <HideOnlineAccountScreens>true</HideOnlineAccountScreens>  
    <HideWirelessSetupInOOBE>true</HideWirelessSetupInOOBE>  
</OOBE>  
```  

#### <a name="some-features-are-listed-incorrectly-for-windows-81"></a>Algumas funcionalidades são listadas incorretamente para Windows 8.1  
 Ao utilizar o **instalar funções e funcionalidades** ou **desinstalar funções e funcionalidades** passos e selecionar o Windows 8.1, aplicam os seguintes problemas:  

-   **Internet Explorer 10 (x86)**, que se refere a funcionalidade de Internet-Explorer-opcional-x86 e **Internet Explorer 10 (amd64)**, que se refere a funcionalidade de Internet-Explorer-opcional-amd64, é apresentada no Windows 8.1 como "Internet Explorer 11."  

-   O **cliente de pastas de trabalho** (WorkFolders do cliente) não está incluído na lista.  

 SOLUÇÃO: O Internet Explorer 10... as seleções ainda podem ser utilizadas, mas irão ativar ou desativar o Internet Explorer 11, em vez do Internet Explorer 10 conforme indicado. O cliente de pastas de trabalho tem de ser ativado ou desativado num separado **executar linha de comandos** passo com o DISM, por exemplo:  

```  
Dism /online /Enable-Feature /FeatureName:WorkFolders-Client  
```  

###  <a name="KnownIssuesLTI"></a>Problemas conhecidos apenas a implementações LTI  
 Segue-se uma lista dos problemas conhecidos relacionados com apenas a implementações LTI.  

#### <a name="check-for-updates-downloads-an-older-list-of-components"></a>Verifique a existência de transferências de atualizações uma lista mais antiga de componentes  
 No Deployment Workbench, informações Center, o nó de componentes, selecionar **procurar atualizações** do **ação** menu irá transferir uma versão mais antiga do bddmanifest.cab, revertendo o componente manifesto (ComponentList.xml) para uma versão mais antiga.  

 SOLUÇÃO: Não utilize **procurar atualizações**; esta funcionalidade foi preterida e será removida no futuro.  

#### <a name="windows-81-appx-cleanup-maintenance-task-can-affect-sysprep"></a>Tarefa de manutenção de limpeza do Windows 8.1 AppX pode afetar o Sysprep  
 Depois de instalar o Windows 8.1 uma tarefa de manutenção incorporadas, Pre-Staged limpeza de aplicação, será executado após 60 minutos de utilização do computador, seguidos de 15 minutos de tempo de inatividade da máquina. Se o Sysprep for executado após a conclusão desta tarefa de manutenção, irá gerar avisos no setupact.log para Sysprep. Se esta imagem, em seguida, é capturada e implementada, a experiência de utilizador final pode ser afetada negativamente. Especificamente pacotes de recursos com base no idioma, escala e DXFL que não foram instalados para as contas de utilizador atual serão eliminados. Se esta imagem é implementada numa máquina em que são aplicáveis os pacotes de recursos, tem de ser instalados como uma atualização através da loja ou através de um mecanismo de sideloading empresarial.  

 SOLUÇÃO: Existem duas opções para atenuar este problema. Em primeiro lugar, certifique-se de que o Sysprep for executado dentro de 75 minutos de concluir a instalação do Windows 8.1. Segundo, se não é possível garantir que o Sysprep será executado dentro de 75 minutos de concluir a instalação do Windows 8.1, desative a tarefa de manutenção.  

 Para desativar a tarefa de manutenção como parte da compilação do MDT e capturar a sequência de tarefas, imediatamente a seguir automaticamente o **recolha local apenas** passo no **restauro de estado** grupo Inserir um novo **Executar linha de comandos** passo com a seguinte linha de comandos:  

```  
Schtasks.exe /change /disable /tn "\Microsoft\Windows\AppxDeploymentClient\Pre-staged app cleanup"  
```  

 Por exemplo,  

 ![Imagem de notas de versão do MDT 2013 1](media/MDT2013ReleaseNotesImage1.jpg "MDT2013ReleaseNotesImage1")  

 Este passo só deve ser adicionado a sequências de tarefas que estejam a executar o Sysprep no Windows 8.1. Windows será automaticamente volte a ativar a tarefa de manutenção durante o Sysprep fase de generalização.  

#### <a name="existing-databases-will-retain-50-character-application-names-when-upgrading-to-mdt-2013"></a>Bases de dados existentes irão reter 50 nomes de aplicação de carateres, ao atualizar para o MDT 2013  
 MDT 2013 inclui uma alteração à base de dados para expandir o campo de nome de aplicação de 50 a 255 carateres. Uma nova base de dados no MDT 2013 irá utilizar o comprimento de 255 carateres do campo. Base de dados existente atualizado a partir do MDT 2012 Update 1 para o MDT 2013 irão manter o comprimento do campo de 50 carateres.  

 SOLUÇÃO: Após atualizar para o MDT 2013 manualmente altere a tabela de base de dados com os seguintes comandos do SQL Server:  

```  
ALTER TABLE [dbo].[Settings_Applications]   
ALTER COLUMN [Applications] [nvarchar] (256)  
```  

#### <a name="the-deployment-will-fail-on-a-legacy-bios-system-if-bitlocker-is-enabled-and-a-data-partition-is-created"></a>A implementação irá falhar num sistema de BIOS legado se BitLocker estiver ativado e é criada uma partição de dados  
 Se a implementação ativa o BitLocker, a predefinição "Formato e criar partições do disco" passo da sequência de tarefas é editada para incluir uma partição de dados adicionais (por exemplo, OSDisk [principal] 60%, dados [principal] 100%), e a sequência de tarefas for implementada um BIOS legado sistema, a implementação irá falhar arrancar em Windows com o erro:  

```  
Boot Device Not Found  
Please install an OS on your hard disk  
Hard Disk - (3F0)  
```  

 SOLUÇÃO: Nenhum  

#### <a name="provisioning-of-windows-store-applications-does-not-include-dependencies"></a>Aprovisionamento de aplicações da loja Windows não inclui dependências  
 Dependências configuradas para uma aplicação da loja Windows (. AppX) não serão instaladas quando a sequência de tarefas instala as aplicações.  

 SOLUÇÃO: Instale diretamente as dependências de aplicações na sequência de tarefas.  

#### <a name="gpt-drives-are-partitioned-as-mbr"></a>Unidades GPT são divididos em partições como MBR  
 Uma unidade estiver configurada para utilizar o disco de tabela de partições GUID (GPT), sistema de criação de partições de **formatar e particionar disco** passo de sequência de tarefas, mas é implementado através da criação de partições de sistema, em vez disso, o disco do registo de arranque principal (MBR). Este problema pode dever-se em computadores com o BIOS unidades segundo que são maiores do que 2 GB e requerem um sistema de criação de partições GPT.  

 SOLUÇÃO: execute os seguintes passos:  

1.  Na sequência de tarefas que pretende modificar, no **Preinstall** grupo, o **novo computador apenas** grupo, imediatamente antes do **formatar e particionar disco** passo de sequência de tarefas para o disco em questão, crie um passo de sequência de tarefas com base no **Set Task Sequence Variable** tipo para forçar a utilização do sistema de partição de disco GPT utilizando as seguintes informações de sequência de tarefas.

    |Para esta definição|Utilize este valor|  
    |-|-|  
    |Nome|Forçar a utilização do sistema de partição de disco GPT|  
    |Descrição|Força o seguinte formatar e particionar disco passo sequência de tarefas para utilizar o sistema de partição de disco GPT.|  
    |Variável de sequência de tarefas|OSDDiskType|  
    |Valor|GPT|  

2.  Imediatamente após o **formatar e particionar disco** passo de sequência de tarefas, identificado no passo anterior, criar um passo de sequência de tarefas com base no **Set Task Sequence Variable** tarefas tipo de sequência de repor o Utilize o sistema de partição de disco GPT utilizando as seguintes informações.

    |Para esta definição|Utilize este valor|  
    |-|-|  
    |Nome|Utilização de reposição do sistema de partição de disco GPT|  
    |Descrição|Permitir que quaisquer tarefas formatar e particionar disco subsequentes passos de sequência para utilizar o sistema de partição de disco especificado pelo BIOS.|  
    |Variável de sequência de tarefas|OSDDiskType|  
    |Valor||  

    > [!NOTE]
    >  Deixe o valor para o **OSDDiskType** propriedade introduzida na **valor** em branco.  

#### <a name="domain-join-fails-due-to-default-variable-values"></a>Associação a um domínio falha devido a valores de variáveis predefinido  
 Quando a ignorar a introdução de associação ao domínio valores no **detalhes do computador** página do assistente no Assistente de implementação (utilizando o **SkipDomainMembership** propriedade), os valores para o  **DomainAdminDomain**, **DomainAdminUser**, e **DomainAdminPassword** propriedades forem definidas para os valores predefinidos e o computador de destino não é possível a associação de propriedade de domínio. Este problema pode ser causado por não adicionar valores para estas propriedades no ficheiro CustomSettings.ini ou da base de dados do MDT.  

 SOLUÇÃO: Especifique pelo menos uma das seguintes propriedades no ficheiro CustomSettings.ini ou da base de dados do MDT:  

-   **DomainAdminDomain**  

-   **DomainAdminUser**  

-   **DomainAdminPassword**  

 Por exemplo, considere o seguinte excerpt de um ficheiro CustomSettings.ini:  

```  
SkipDomainMembership=YES  
DomainAdminDomain=Contoso  
JoinDomain=Contoso.com  
```  

 Especificar qualquer uma destas propriedades permitirá ao utilizador para a introduzir os valores de associação de domínio no **detalhes do computador** página do assistente no Assistente de implementação.  

> [!NOTE]
>  É também totalmente pode ignorar o **detalhes do computador** página do assistente especificando todas as propriedades listado acima no ficheiro CustomSettings.ini ou da base de dados do MDT. Para obter mais informações, consulte a secção "Fornecer propriedades para ignorada implementação páginas do assistente," no documento MDT *Toolkit referência*.  

#### <a name="user-data-may-not-be-restored-from-usb"></a>Dados de utilizador não podem ser restaurados a partir do USB  
 Dados de migração de estado de utilizador não podem ser restaurados ao guardar os dados de migração de estado de utilizador para uma unidade USB. Isto é causado por uma alteração para a letra de unidade para a unidade USB durante o processo de implementação.  

 SOLUÇÃO: Nenhum  

#### <a name="user-mapped-network-drive-z-is-not-restored"></a>Utilizador mapear a unidade de rede que não é restaurada z  
 Fundo de ambiente de trabalho de utilizador e não existem unidades de rede são restauradas no cenário de implementação de atualizar o computador. Isto pode acontecer quando o utilizador tem uma unidade de rede mapeada para a unidade Z. Depois de concluir o **resumo de implementação** caixa de diálogo, a imagem de fundo de ambiente de trabalho de utilizador será restaurada. No entanto, o utilizador poderá ter de recriar o mapeamento de unidade Z.  

 SOLUÇÃO: Nenhum  

#### <a name="bare-metal-deployment-fails-with-fixed-disk-usb-flash-drive-on-uefi-system"></a>Implementação bare-metal falha com o "disco fixo" unidade flash USB no sistema UEFI  
 Quando efetuar uma implementação bare-metal, com base no suporte de dados num Unified Extensible Firmware Interface (UEFI) utilizando uma USB mais recente do sistema pen (pen USB) que é detetado como "disco fixo" a pen USB é detetado como disco 1 (inicialmente atribuída a letra da unidade C) e interna disco rígido é disco 0. Depois do disco rígido interno está particionado e formatado, unidade letras são reatribuídas, de modo a que o OSDisk C e a pen USB está W. A implementação irá falhar o passo de Script de cópia.  

 SOLUÇÃO: Reiniciar o sistema e iniciar uma nova implementação. O será OSDisk ser atribuídos a letra da unidade C, será a pen USB atribuído D e será a implementação com êxito a continuar.  

#### <a name="lti-progress-on-the-windows-81-desktop-is-not-visible-from-the-start-screen"></a>Progresso LTI no ambiente de trabalho do Windows 8.1 não está visível no ecrã Iniciar  
 Um método lite touch installation (LTI) será automaticamente de início de sessão como administrador local para continuar a sequência de tarefas, no entanto, o Windows 8.1 será, por predefinição, início de sessão para o ecrã de início. LTI começa com êxito no início de sessão conforme esperado, mas o indicador de progresso só é apresentado no ambiente de trabalho.  

 SOLUÇÃO: Existem duas soluções possíveis. Em primeiro lugar, um utilizador na consola do pode clicar no ícone de ambiente de trabalho no ecrã para ver o progresso LTI.  

 Segundo, o seguinte comando pode ser adicionado à secção Unattend.xml FirstLogonCommands temporariamente ativar a definição de política de grupo, **Ir para o ambiente de trabalho em vez do início quando iniciar sessão no**.  

```  
<FirstLogonCommands>  
  <SynchronousCommand wcm:action="add">  
    <CommandLine>wscript.exe %SystemDrive%\LTIBootstrap.vbs</CommandLine>  
    <Description>Lite Touch new OS</Description>  
    <Order>1</Order>  
  </SynchronousCommand>  
  <SynchronousCommand wcm:action="add">  
    <CommandLine>cmd /c reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Explorer" /v GoToDesktopOnSignIn /t REG_DWORD /d 00000001 /f </CommandLine>  
    <Description>GoToDesktopOnSignIn</Description>  
    <Order>2</Order>  
  </SynchronousCommand>   </FirstLogonCommands>  
```  

> [!NOTE]
>  apenas o **segundo** SynchronousCommand elemento é adicionado; o primeiro será já existe no modelo Unattend.xml  

 Outro mecanismo também deve ser utilizado para posteriormente remover esta definição temporária, por exemplo, a política de grupo do Active Directory ou ao remover a chave de registo mais tarde na sequência de tarefas. Por exemplo,  

 ![Imagem de notas de versão do MDT 2013 2](media/MDT2013ReleaseNotesImage2.png "MDT2013ReleaseNotesImage2")  

### <a name="known-issues-for-all-configuration-manager-deployments"></a>Problemas conhecidos para todas as implementações do Configuration Manager  
 Segue-se uma lista dos problemas conhecidos relacionados com as implementações ZTI ou UDI que utilizam o System Center 2012 R2 Configuration Manager:  

#### <a name="default-os-image-installed-to-d-drive"></a>Imagem do SO predefinido instalada para a unidade d:  
 Importar a imagem de SO predefinida (install.wim) e a implementação com uma sequência de tarefas ZTI irão fazer com que o Windows ser instalada na unidade d: em vez da unidade c: padrão.  

 SOLUÇÃO: Defina a variável de sequência de tarefas OSDPreserveDriveLetter para um valor em branco, em vez do predefinido False.  

#### <a name="bitlocker-tasks-fails-during-zti"></a>Falha de tarefas do BitLocker durante ZTI  
 O **UILanguage** variável de sequência de tarefas tem de ser definida quando utilizar ZTIBde.wsf numa sequência de tarefas ZTI. Caso contrário, ZTIBde.wsf irá falhar.  

 SOLUÇÃO: Nenhum  

#### <a name="the-task-sequence-fails-when-local-administrator-accounts-exist"></a>A sequência de tarefas falha quando as contas de administrador local não existe  
 Atualizar um computador utilizando ZTI e UDI sequências de tarefas falha quando existem contas de administrador local no computador. Sequências de tarefas também falharem quando a predefinição **capturar estado do utilizador** passo tem **capturar todos os perfis de utilizador com opções padrão** selecionado, mas a predefinição **restaurar estado do utilizador** passo tem o **restaurar perfis de utilizador do computador local** caixa de verificação desmarcada e o Configuration Manager não é possível migrar as novas contas sem lhes atribuir palavras-passe.  

 SOLUÇÃO: Manualmente, modificar a sequência de tarefas, selecionando a opção para migrar as contas locais e especifique uma palavra-passe a ser utilizado com a conta local. Para obter mais informações, consulte [capturar estado do utilizador](http://technet.microsoft.com/library/bb680924.aspx).  

### <a name="known-issues-for-zti-deployments-only"></a>Problemas conhecidos apenas a implementações ZTI  
 Segue-se uma lista dos problemas conhecidos relacionados com apenas a implementações ZTI.  

#### <a name="installing-chinese-windows-7-prompts-for-user-input"></a>Instalar o Windows 7 chinês solicita a introdução do utilizador  
 Quando implementar o Windows 7 com o idioma chinês, o processo de instalação para aguardar a intervenção do utilizador. Isto é causado por um erro no ficheiro Lang.ini no Windows 7.  

 SOLUÇÃO: Atualize o ficheiro de Lang.ini como mostram abaixo.  

 Ficheiro Lang.ini original:  

```  
[Available UI Languages]  
zh-CN = 3  

[Fallback Languages]  
zh-CN = en-us  
```  

 Ficheiro de Lang.ini após a modificação:  

```  
zh-CN = 2  
en-us = 3  

[Fallback Languages]  
zh-CN = en-us  
```  

#### <a name="restore-user-state-step-is-skipped-during-replace-scenario"></a>Passo restaurar estado do utilizador é ignorado durante a substituição cenário  
 Num cenário de implementação de substituir o computador, o **restaurar estado do utilizador** passo de sequência de tarefas é ignorado se o **OSDStateStorePath** propriedade está definida como ou um caminho de convenção de Nomenclatura Universal válido.  

 SOLUÇÃO: Definir o **USMTLocal** propriedade para verdadeiro. Se o fizer, força ZTI UserState.wsf para reconhecer o caminho no **OSDStateStorePath** propriedade. Isto é provocado pelo passo de sequência de tarefas solicitar armazenamento de Estados que está a ser ignorada e o valor anterior no **OSDStateStorePath** propriedade que está a ser retida.  

#### <a name="the-task-sequence-may-fail-with-separate-system-or-active-partitions"></a>A sequência de tarefas poderá falhar com o sistema separado ou partições ativas  
 Windows não irá atribuir uma letra de unidade ao sistema ou partição ativa se essa unidade for diferente da unidade em que o sistema operativo está localizado. Se a partição maior também o sistema ou partição ativa, a sequência de tarefas pode falhar ao retomar no novo sistema operativo.  

 SOLUÇÃO: Certifique-se de que a partição do sistema ou o Active Directory não é maior do que a partição do sistema operativo se utilizar várias partições.  

#### <a name="usmt-targetwindows7-switch-fails-in-offline-scenario"></a>Falha de comutador de /TargetWindows7 USMT no cenário offline  
 O seguinte erro ocorre a scanstate.log ao efetuar o cenário de implementação do MDT atualizar computador ZTI a utilizar ao capturar informações de estado do utilizador utilizando a funcionalidade de migração offline do USMT:  

```  
USMT error code 27: [gle=0x00000006]  
```  

 SOLUÇÃO: Nenhum; Este é um problema conhecido com o USMT.  

#### <a name="configure-adds-step-does-not-save-correctly"></a>Configurar o ADDS passo não guardar corretamente  
 Utilizar o **configurar adiciona** passo, propriedades avançadas, para definir os níveis funcionais de domínio e floresta para Windows Server 2003 ou Windows Server 2008 R2 resultará em níveis funcionais definidos como Windows Server 2008.  

 SOLUÇÃO: Definir DomainLevel = 5 e/ou ForestLevel = 5 no CustomSettings.ini. Consulte a referência do Toolkit para obter mais detalhes sobre estas definições.  

#### <a name="server-task-sequence-template-fails-on-uefi-system"></a>Modelo de sequência de tarefas do servidor falha num sistema UEFI  
 Quando utilizar o modelo de sequência de tarefas do MDT 2013 servidor integrado no System Center 2012 R2 Configuration Manager, as implementações irão falhar em alguns sistemas Unified Extensible Firmware Interface (UEFI) ao executar o **formato e partição de disco (UEFI)**  passo com um erro da aplicação no OsdDiskPart.exe semelhante ao seguinte: "As instruções em 0x6e2c8374 referenciado 0x00000120 de memória. Não foi possível ler a memória. Clique em OK para terminar o programa."  

 SOLUÇÃO: Nenhuma com cenário ZTI. LTI ou só de ConfigMgr cenários funcionam.  

###  <a name="KnownIssuesLTIZTI"></a>Problemas conhecidos LTI e implementações ZTI  
 Segue-se uma lista dos problemas conhecidos relacionados com implementações LTI e ZTI.  

#### <a name="roles-and-features-requiring-multiple-restarts-cause-problems-for-task-sequences"></a>Funções e funcionalidades que requerem vários problemas de causa do reinício para as sequências de tarefas  
 Instalar funções ou funcionalidades, tais como **MICROSOFT-HYPER-V-todos os** ou **servidor de RD de RDS** que necessitam de vários reinícios ou dependem essas funções ou funcionalidades podem causar problemas durante a tarefa sequenciar e devem ser evitados.  

 SOLUÇÃO: Instale a funcionalidade ou função pretendida num computador de referência e capturar uma imagem que tenha a função pretendida ou funcionalidade já instalado.  

#### <a name="multiple-logs-created-during-deployment"></a>Vários registos criados durante a implementação  
 Durante os processos de Scanstate e Loadstate, várias cópias dos ficheiros de registo pode ser criada, por exemplo, BDD.log, BDD. log (1), ZTIUserstate.log e ZTIUserstate. log (1).  

 SOLUÇÃO: Excluir os ficheiros de registo ou os diretórios de registo ao executar Scanstate e Loadstate.  

###  <a name="KnownIssuesUDI"></a>Problemas conhecidos para implementações de UDI  
 Segue-se uma lista dos problemas conhecidos relacionados com implementações de UDI.  

#### <a name="udi-wizard-hides-no-data-option-on-user-state-page-in-capture-mode"></a>Assistente de UDI oculta opção sem dados na página de estado do utilizador no modo de captura  
 Não é possível personalizar a página de UserState com o botão de opção "Sem dados" quando estiver no modo de captura.  

 SOLUÇÃO: Abra o ficheiro de configuração do assistente com o bloco de notas e adicione a seguinte propriedade para a secção de página "Selecionar destino" que é executado no modo de captura:  

```  
<Setter Property="DisplayNoDataInCaptureMode">true</Setter>  
```  

 Por exemplo,  

```  
<Setter Property="DataSourceText">Please select a location where user data will be captured.</Setter>  
<Setter Property="Format">disable</Setter>  
<Setter Property="FormatPrompt">disable</Setter>  
<Setter Property="MinimumDriveSize">10</Setter>  
<Setter Property="State">Capture</Setter>  
<Setter Property="NetworkDrive">n:</Setter>  
<Setter Property="DisplayNoDataInCaptureMode">true</Setter>  
```  

 Para ocultar os dados"não" botão de opção defina o valor acima como false ou remova a entrada.  

#### <a name="the-time-and-currency-language-format-is-not-configured"></a>Formato de linguagem do tempo e moeda não está configurado  
 Formato de linguagem do tempo e moeda não está corretamente configurado no computador de destino, apesar do idioma correto tiver sido selecionado no **formato de hora e a moeda (região)** lista o **idioma** UDI Página do assistente. Este problema pode ser causado por um erro no ficheiro UDIWizard.wsf. O ficheiro UDIWizard.wsf está localizado no *mdt_files*\Scripts pasta (onde *mdt_files* é a pasta que é a origem para o MDT ficheiros de pacote que utiliza a sequência de tarefas).  

 SOLUÇÃO: Para corrigir o erro no ficheiro UDIWizard.wsf, execute os seguintes passos:  

1.  Edite o ficheiro UDIWizard.wsf, que reside no *mdt_files*\Scripts pasta (onde *mdt_files* é a pasta que é a origem para o MDT ficheiros de pacote que utiliza a sequência de tarefas).  

2.  Remova a seguinte linha do ficheiro UDIWizard.wsf:  

    ```  
    oEnvironment.Item("UserLocale") = oEnvironment.Item("InputLocale")  
    ```  

    > [!NOTE]
    >  O texto listado acima é uma linha no ficheiro UDIWizard.wsf. Qualquer encapsulamento de aplicações de linha é causado pelas restrições de formatação do documento.  

3.  Guarde o ficheiro UDIWizard.wsf.  

4.  Atualize os pontos de distribuição com a versão modificada do pacote de ficheiros do MDT que contém o ficheiro UDIWizard.wsf atualizado.  

#### <a name="applications-do-not-appear-after-added"></a>As aplicações não são apresentadas depois adicionada  
 As aplicações são não ser apresentado no Assistente de UDI de UDI Designer ou depois de serem adicionados no estruturador de UDI. Este problema pode ocorrer porque o grupo de aplicações de destino não está selecionado antes de adicionar uma aplicação.  

 SOLUÇÃO: Selecione o grupo de aplicações de destino antes de adicionar uma aplicação.  

#### <a name="applications-may-not-be-installed"></a>Aplicações poderão não estar instaladas  
 Instalador da aplicação (AppInstall.exe) não pode instalar aplicações que são implementadas para utilizadores corretamente. Este problema pode ser causado por **permitir ao utilizador para definir os seus dispositivos primários** a ser definido como **não**.  

 SOLUÇÃO: Defina o valor da **permitir ao utilizador para definir os seus dispositivos primários** para **Sim**. O **permitir ao utilizador para definir os seus dispositivos primários** controlo se encontra no **afinidade de dispositivo e utilizador** na secção de **predefinições** o Overview\Client caixa de diálogo No nó de definições a **administração** painel de navegação, na consola do Configuration Manager.  

#### <a name="deployment-time-is-not-correct-during-stand-alone-media-deployment"></a>Tempo de implementação não está correto durante a implementação de suportes de dados autónomos  
 Se estiver a utilizar o suporte de dados autónomo, o valor apresentado para **momento da implementação** por **OSDResults** no fim da implementação não é garantida correto, porque uma ligação de rede não é suposta estar estão disponíveis ao utilizar suportes de dados autónomos. Por conseguinte, o relógio do sistema básico de entrada/saída (BIOS) a máquina não é possível sincronizar com uma hora correta. Em alguns casos, o tempo de implementação pode mostrar negativo number, tal como ocorre quando o tempo disponível a partir do Windows PE no início está incorretamente definido com um valor que é realmente posterior à hora em que a conclusão da implementação.  

 SOLUÇÃO: Nenhum  

#### <a name="osddomainname-variable-does-not-work-as-expected"></a>Variável de OSDDomainName não funcionar conforme esperado  
 No caso de UDI, o **OSDDomainName** variável de sequência de tarefas é maiúsculas e minúsculas.  

 SOLUÇÃO: Ao definir o **OSDDomainName** valor através de um passo de sequência de tarefas ou da CS.ini, tem de ser uma correspondência exata com o valor de domínio definido no ficheiro de configuração de UDI.

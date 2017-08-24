---
title: Implementar clientes UNIX/Linux | Microsoft Docs
description: Saiba como implementar um cliente num servidor UNIX ou Linux no System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
caps.latest.revision: "9"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d61d53daa5ef3d9c986cba8791d4471fea94d29d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-system-center-configuration-manager"></a>Como implementar clientes em servidores UNIX e Linux no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de poder gerir um servidor Linux ou UNIX com o System Center Configuration Manager, tem de instalar o cliente do Configuration Manager para Linux e UNIX em cada servidor Linux ou UNIX. Pode efetuar a instalação do cliente manualmente em cada computador ou utilizar um script de shell que instala o cliente remotamente. O Configuration Manager não suporta a utilização da instalação push do cliente para servidores Linux ou UNIX. Opcionalmente, pode configurar um Runbook do System Center Orchestrator para automatizar a instalação do cliente no servidor Linux ou UNIX.  

 Independentemente do método de instalação utilizado, o processo de instalação requer a utilização de um script com o nome **install** para gerir o processo de instalação. Este script está incluído quando transferir o cliente para Linux e UNIX.  

 O script de instalação do cliente do Configuration Manager para Linux e UNIX suporta propriedades de linha de comandos. Algumas propriedades de linha de comandos são necessárias, enquanto outras são opcionais. Por exemplo, quando instala o cliente, tem de especificar um ponto de gestão do site que é utilizado pelo servidor Linux ou UNIX para o contacto inicial com o site. Para obter a lista completa de propriedades de linha de comandos, veja [Propriedades de Linha de Comandos para Instalação do Cliente em Servidores Linux e UNIX](#BKMK_CmdLineInstallLnUClient).  

 Depois de instalar o cliente, especifique as definições de cliente na consola do Configuration Manager para configurar o agente de cliente da mesma forma que faria com clientes baseados em Windows. Para obter mais informações, veja [Definições de cliente para servidores Linux e UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU).  

##  <a name="BKMK_AboutInstallPackages"></a> Acerca dos Pacotes de Instalação de Cliente e do Agente Universal  
 Para instalar o cliente para Linux e UNIX numa plataforma específica, tem de utilizar o pacote de instalação de cliente aplicável ao computador onde instalar o cliente. Os pacotes de instalação de cliente aplicáveis são incluídos como parte de cada transferência de cliente a partir do [Centro de Transferências da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). Para além de pacotes de instalação de cliente, a transferência do cliente inclui o script de **instalação** que gere a instalação do cliente em cada computador.  

 Quando instala um cliente, pode utilizar o mesmo processo e as mesmas propriedades de linha de comandos, independentemente do pacote de instalação de cliente que utiliza.  

 Para obter informações sobre os sistemas operativos, plataformas e pacotes de instalação de cliente suportados por cada versão do cliente do Configuration Manager para Linux e UNIX, consulte [servidores Linux e UNIX](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#linux-and-unix-servers).  

##  <a name="BKMK_InstallLnUClient"></a> Instalar o Cliente em Servidores Linux e UNIX  
 Para instalar o cliente para Linux e UNIX, tem de executar um script em cada computador Linux ou UNIX. O script tem o nome **install** e suporta propriedades de linha de comandos que modificam o comportamento de instalação e fazem referência ao pacote de instalação de cliente. O script de instalação e o pacote de instalação de cliente têm de estar localizados no cliente. O pacote de instalação de cliente contém os ficheiros de cliente do Configuration Manager para um sistema de operativo Linux ou UNIX específico e a plataforma.
Cada pacote de instalação de cliente contém todos os ficheiros necessários para realizar a instalação do cliente e, ao contrário dos computadores baseados em Windows, não transfere ficheiros adicionais de um ponto de gestão ou outra localização de origem.  

 Depois de instalar o cliente do Configuration Manager para Linux e UNIX, não é necessário reiniciar o computador. Assim que a instalação do software estiver concluída, o cliente está operacional. Se reiniciar o computador, o cliente do Configuration Manager reinicia automaticamente.  

 O cliente instalado é executado com credenciais de raiz. As credenciais de raiz são necessárias para recolher inventário de hardware e efetuar implementações de software.  

 Segue-se o formato do comando:  

 **. / instalar -mp &lt;computador\> - sitecode &lt;sitecode\> &lt;propriedade #1 > &lt;propriedade #2 > &lt;pacote de instalação de cliente\>**  

-   **install** é o nome do ficheiro de script que instala o cliente para Linux e UNIX. Este ficheiro é fornecido com o software de cliente.  

-   **-mp &lt;computador** Especifica o ponto de gestão inicial que é utilizado pelo cliente.  

     Exemplo: smsmp.contoso.com  

-   **-sitecode &lt;código do site\>**  Especifica o código do site que o cliente está atribuído.  

     Exemplo: S01  

-   &lt;propriedade #1 > &lt;propriedade #2 > especifica as propriedades da linha de comandos para utilizar com o script de instalação.  

    > [!NOTE]  
    >  Para obter mais informações, veja [Propriedades de Linha de Comandos para Instalação do Cliente em Servidores Linux e UNIX](#BKMK_CmdLineInstallLnUClient)  

-   **client installation package** é o nome do pacote .tar de instalação de cliente para o sistema operativo, versão e arquitetura de CPU deste computador. O ficheiro .tar de instalação de cliente tem de ser especificado no fim.  

     Exemplo: ccm-Universal-x64. &lt;criar\>. tar  

###  <a name="BKMK_ToInstallLnUClinent"></a> Para instalar o Cliente do Configuration Manager em servidores Linux e UNIX  

1.  Num computador Windows, [transfira o ficheiro de cliente adequado para o servidor Linux ou UNIX](http://go.microsoft.com/fwlink/?LinkID=525184) que pretende gerir.  

2.  Execute o ficheiro .exe de extração automática no computador Windows para extrair o script de instalação e o ficheiro .tar de instalação do cliente.  

3.  Copie o script **install** e o ficheiro .tar para uma pasta no servidor que pretende gerir.  

4.  No servidor UNIX ou Linux, execute o seguinte comando para permitir que o script seja executado como um programa: **chmod +x install**  

    > [!IMPORTANT]  
    >  É necessário utilizar credenciais de raiz para instalar o cliente.  

5.  Em seguida, execute o seguinte comando para instalar o cliente do Configuration Manager: **. / instalar -mp &lt;hostname\> - sitecode &lt;código\> ccm-Universal-x64.&lt; criar\>. tar**  

     Ao introduzir este comando, utilize as propriedades de linha de comandos adicionais de que necessita.  Para obter a lista de propriedades de linha de comandos, veja [Propriedades de Linha de Comandos para Instalação do Cliente em Servidores Linux e UNIX](#BKMK_CmdLineInstallLnUClient)  

6.  Após a execução do script, valide a instalação revendo o ficheiro **/var/opt/microsoft/scxcm.log** . Além disso, pode confirmar que o cliente é instalado e a comunicar com o site através da visualização dos detalhes do cliente no **dispositivos** o nó do **ativos e compatibilidade** área de trabalho na consola do Configuration Manager.  

###  <a name="BKMK_CmdLineInstallLnUClient"></a> Propriedades de Linha de Comandos para Instalação do Cliente em Servidores Linux e UNIX  
 As propriedades seguintes estão disponíveis para modificar o comportamento do script de instalação:  

> [!NOTE]  
>  Utilize a propriedade **-h** para apresentar esta lista de propriedades suportadas.  

-   **-mp &lt;FQDN do servidor\>**  

     Necessário. Especifica através do FQDN, o servidor de ponto de gestão que o cliente irá utilizar como ponto inicial de contacto.  

    > [!IMPORTANT]  
    >  Esta propriedade não especifica o ponto de gestão ao qual o cliente será atribuído após a instalação.  

    > [!NOTE]  
    >  Quando utiliza a propriedade **-mp** para especificar um ponto de gestão que está configurado para aceitar apenas ligações de cliente HTTPS, também tem de utilizar a propriedade **-UsePKICert** .  

-   **-sitecode &lt;sitecode\>**  

     Necessário. Especifica o site primário do Configuration Manager para atribuir o cliente do Configuration Manager.  

     Exemplo: -sitecode S01  

-   **-fsp &lt;servidor_fqdn >**  

     Opcional. Especifica através do FQDN, o servidor de ponto de estado de contingência que o cliente utiliza para submeter mensagens de estado.  

     Para obter mais informações sobre o ponto de estado de contingência, veja [Determinar se Necessita de um Ponto de Estado de Contingência](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point).  


-   **-dir &lt;diretório\>**  

     Opcional. Especifica uma localização alternativa para instalar os ficheiros de cliente do Configuration Manager.  

     Por predefinição, o cliente é instalado na seguinte localização: **/opt/microsoft**.  

-   **-nostart**  

     Opcional. Impede o início automático do serviço de cliente do Configuration Manager, **ccmexec.bin**, depois de concluída a instalação de cliente.  

     Após a instalação do cliente, tem de iniciar manualmente o serviço de cliente.  

     Por predefinição, o serviço de cliente é iniciado depois de concluída a instalação do cliente e sempre que o computador é reiniciado.  

-   **-clean**  

     Opcional. Especifica a remoção de todos os dados e ficheiros de cliente a partir de um cliente anteriormente instalado para Linux e UNIX, antes de a nova instalação ser iniciada. Isto remove a base de dados do cliente e o arquivo de certificados.  

-   **-keepdb**  

     Opcional. Especifica que a base de dados do cliente local é mantida e reutilizada quando reinstalar um cliente. Por predefinição, quando reinstalar um cliente, esta base de dados é eliminada.  

-   **-UsePKICert &lt;parâmetro\>**  

     Opcional. Especifica o nome de ficheiro e caminho completo de um certificado PKI X.509 no formato Public Key Certificate Standard (PKCS#12). Este certificado é utilizado para a autenticação de cliente. Se não for especificado um certificado durante a instalação e precisar de adicionar ou alterar um certificado, utilize o utilitário **certutil** . Veja [Como gerir certificados no cliente para Linux e UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts) para obter informações sobre o certutil.  

     Quando utiliza **-UsePKICert**, também tem de fornecer a palavra-passe associada ao ficheiro PKCS#12 através da utilização do parâmetro da linha de comandos **-certpw** .  

     Se não utilizar esta propriedade para especificar um certificado PKI, o cliente utiliza um certificado autoassinado e todas as comunicações com sistemas de sites são efetuadas por HTTP.  

     Se especificar um certificado inválido na linha de comandos de instalação do cliente, não são devolvidos erros. Isto acontece porque a validação do certificado ocorre após a instalação do cliente. Quando o cliente é iniciado, certificados são validados com o ponto de gestão e se um certificado falhar na validação a seguinte mensagem de erro é apresentado na **scxcm.log**, o ficheiro de registo de cliente Unix e Linux Configuration Manager: **Falha ao validar o certificado de ponto de gestão**. A localização do ficheiro de registo predefinida é:  **/var/opt/microsoft/scxcm.log**.  

    > [!NOTE]  
    >  Tem de especificar esta propriedade quando instala um cliente e utiliza a propriedade **-mp** para especificar um ponto de gestão que esteja configurado para aceitar apenas ligações de cliente HTTPS.  

     Exemplo: - UsePKICert &lt;completa e caminho do ficheiro\> - certpw &lt;palavra-passe\>  

-   **-certpw &lt;parâmetro\>**  

     Opcional. Especifica a palavra-passe associada ao ficheiro PKCS#12 que especificou com a propriedade **-UsePKICert** .  

     Exemplo: - UsePKICert &lt;completa e caminho do ficheiro\> - certpw &lt;palavra-passe\>  

-   **-NoCRLCheck**  

     Opcional. Especifica que um cliente não deve verificar a lista de revogação de certificados (CRL) quando comunica por HTTPS através de um certificado PKI. Se esta opção não for especificada, o cliente verifica a CRL antes de estabelecer uma ligação HTTPS através de certificados PKI. Para obter mais informações sobre a verificação da CRL de cliente, veja Planear a Revogação de Certificados PKI.  

     Exemplo: - UsePKICert &lt;completa e caminho do ficheiro\> - certpw &lt;palavra-passe\> - NoCRLCheck  

-   **-rootkeypath &lt;localização do ficheiro\>**  

     Opcional. Especifica o caminho completo e nome de ficheiro para a chave de raiz fidedigna do Configuration Manager. Fidedigna do Configuration Manager a chave de raiz fornece um mecanismo que clientes Linux e UNIX utilizam para verificar que estão ligados a um sistema de sites que pertença à hierarquia correta.  

     Se não especificar a chave de raiz fidedigna na linha de comandos, o cliente irá confiar no primeiro ponto de gestão com o qual comunica e irá obter automaticamente a chave de raiz fidedigna a partir desse ponto de gestão.  

     Para obter mais informações, veja [Planear a Chave de Raiz Fidedigna](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

     Exemplo: - rootkeypath &lt;completa e caminho do ficheiro\>  

-   **-httpport &lt;porta\>**  

     Opcional. Especifica a porta que está configurada nos pontos de gestão que o cliente utiliza ao comunicar com pontos de gestão através de HTTP. Se a porta não for especificada, será utilizado o valor predefinido 80.  

     Exemplo: -httpport 80  

-   **-httpsport &lt;porta\>**  

     Opcional. Especifica a porta que está configurada nos pontos de gestão que o cliente utiliza ao comunicar com pontos de gestão através de HTTPS. Se a porta não for especificada, será utilizado o valor predefinido 443.  

     Exemplo: - UsePKICert &lt;caminho completo e certificado nome\> - httpsport 443  

-   **-ignoreSHA256validation**  

     Opcional. Especifica que a instalação do cliente ignora a validação de SHA-256. Utilize esta opção ao instalar o cliente em sistemas operativos que não foram lançados com uma versão de OpenSSL que suporte SHA-256. Para obter mais informações, veja [Sobre Sistemas Operativos Linux e UNIX que não Suportam SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256).  

-   **-signcertpath &lt;localização do ficheiro\>**  

     Opcional. Especifica o caminho completo e o nome de ficheiro **.cer** do certificado autoassinado exportado no servidor do site. Se não estiverem disponíveis certificados PKI, o servidor de site do Configuration Manager gera automaticamente certificados autoassinados.  

     Estes certificados são utilizados para confirmar se as políticas de cliente transferidas do ponto de gestão foram enviadas a partir do site pretendido. Se não for especificado um certificado autoassinado durante a instalação ou se precisar de alterar um certificado, utilize o utilitário **certutil** . Veja [Como gerir certificados no cliente para Linux e UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts) para obter informações sobre o certutil.  

     Este certificado pode ser obtido através do arquivo de certificados **SMS** e tem o nome de Requerente **Servidor do Site** e o nome amigável **Certificado de Assinatura do Servidor do Site**.  

     Se esta opção não for especificada durante a instalação, os clientes Linux e UNIX irão confiar no primeiro ponto de gestão com o qual comunicam e irão obter automaticamente o certificado de assinatura a partir desse ponto de gestão.  

     Exemplo: - signcertpath &lt;nome de ficheiro e caminho completo\>  

-   **-rootcerts**  

     Opcional. Especifica certificados PKI adicionais a importar que não fazem parte de uma hierarquia de autoridade de certificação (AC) de pontos de gestão. Se especificar vários certificados na linha de comandos, estes devem ser delimitados por vírgulas.  

     Utilize esta opção se utilizar certificados de cliente PKI que não encadeiam num certificado de AC de raiz que seja considerada fidedigna pelos pontos de gestão. Pontos de gestão irão rejeitar o cliente se o certificado de cliente não encadear num certificado de raiz fidedigna na lista de emissores de certificados do site.  

     Se não utilizar esta opção, o cliente Linux e UNIX irá verificar a hierarquia de confiança ao utilizar apenas o certificado na opção **-UsePKICert** .  

     Exemplo: - rootcerts &lt;nome de ficheiro e caminho completo\>,&lt;nome de ficheiro e caminho completo\>  

###  <a name="BKMK_UninstallLnUClient"></a> Desinstalar o Cliente de Servidores Linux e UNIX  
 Para desinstalar o cliente do Configuration Manager para Linux e UNIX, utilize o utilitário de desinstalação, **desinstalação**. Por predefinição, este ficheiro está localizado na pasta **/opt/microsoft/configmgr/bin/** no computador cliente. Este comando de desinstalação não suporta quaisquer parâmetros de linha de comandos e irá remover todos os ficheiros relacionados com o software de cliente do servidor.  

 Para desinstalar o cliente, utilize a seguinte linha de comandos: **/opt/microsoft/configmgr/bin/uninstall**  

 Não é necessário reiniciar o computador depois de desinstalar o cliente do Configuration Manager para Linux e UNIX.  

##  <a name="BKMK_ConfigLnUClientCommuincations"></a> Configurar Portas de Pedido para o Cliente para Linux e UNIX  
 Semelhante para os clientes baseados em Windows, o cliente do Configuration Manager para Linux e UNIX utiliza HTTP e HTTPS para comunicar com sistemas de sites do Configuration Manager. As portas que o cliente do Configuration Manager utiliza para comunicar são referidas como portas de pedido.  

 Quando instala o cliente do Configuration Manager para Linux e UNIX, pode alterar as portas de pedido de predefinição de clientes, especificando o **- httpport** e **- httpsport** as propriedades de instalação. Se não especificar a propriedade de instalação e um valor personalizado, o cliente utilizará os valores predefinidos. Os valores predefinidos são **80** para tráfego HTTP e **443** para tráfego HTTPS.  

 Depois de instalar o cliente, não é possível alterar a configuração da respetiva porta de pedido. Em vez disso, para alterar a configuração da porta, tem de reinstalar o cliente e especificar a nova configuração de porta. Ao reinstalar o cliente para alterar os números de portas de pedido, execute o comando **install** semelhante à instalação do novo cliente, mas utilize a propriedade adicional da linha de comandos **-keepdb**. Este parâmetro dá instruções à instalação para manter a base de dados e os ficheiros do cliente, incluindo o arquivo de certificados e o GUID do cliente.  

 Para obter mais informações sobre os números de portas de comunicação de cliente, veja [Como configurar portas de comunicação de cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

##  <a name="BKMK_ConfigClientMP"></a> Configurar o Cliente para Linux e UNIX para Localizar Pontos de Gestão  
 Quando instala o cliente do Configuration Manager para Linux e UNIX, tem de especificar um ponto de gestão para utilizar como um ponto inicial de contacto.  

 O cliente do Configuration Manager para Linux e UNIX contacta este ponto de gestão durante que a instalação do cliente. Se o cliente não conseguir contactar o ponto de gestão, o software de cliente continuará a tentar até ter êxito.  

 Para obter mais informações sobre como os clientes localizam pontos de gestão, veja [Localizar Pontos de Gestão](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points).

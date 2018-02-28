---
title: "Planear a implementação do cliente para computadores Linux e UNIX"
titleSuffix: Configuration Manager
description: "Planear a implementação do cliente para computadores Linux e UNIX no System Center Configuration Manager."
ms.custom: na
ms.date: 08/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
caps.latest.revision: 
caps.handback.revision: 
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 9df979fe98dc4d4ead18ff3cfb276612681c9bce
ms.sourcegitcommit: b1fa7be6a6fa5bb7c49e90c0e28a21ba8b41c842
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/28/2018
---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-system-center-configuration-manager"></a>Planear a implementação do cliente para computadores Linux e UNIX no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode instalar o cliente do System Center Configuration Manager em computadores que executam o Linux ou UNIX. Este cliente foi concebido para servidores que funcionam como um computador de grupo de trabalho e o cliente não suporta a interação com utilizadores com sessão iniciada. Depois de instalar o software de cliente e o cliente estabelecer comunicação com o site do Configuration Manager, pode gerir o cliente utilizando a consola do Configuration Manager e relatórios.  

> [!NOTE]  
>  O cliente do Configuration Manager para computadores Linux e UNIX não suporta as seguintes capacidades de gestão:  
>   
>  -   Instalação push do cliente  
> -   Implementação do sistema operativo  
> -   Implementação de aplicações; em vez disso, implemente software utilizando pacotes e programas.  
> -   Inventário de software  
> -   Atualizações de software  
> -   Definições de compatibilidade  
> -   Controlo remoto  
> -   Gestão de energia  
> -   Verificação de cliente do estado do cliente e remediação  
> -   Gestão de clientes baseada na Internet  

 Para obter informações sobre as distribuições suportadas de Linux e UNIX e o hardware necessário para suportar o cliente para Linux e UNIX, veja [Hardware recomendado para o System Center Configuration Manager](../../../../core/plan-design/configs/recommended-hardware.md).  

 Utilize as informações neste artigo para o ajudar a planear implementar o cliente do Configuration Manager para Linux e UNIX.  

##  <a name="BKMK_ClientDeployPrereqforLnU"></a> Pré-requisitos para implementação do cliente para servidores Linux e UNIX  
 Utilize as seguintes informações para determinar os pré-requisitos que devem estar implementados para instalar o cliente para Linux e UNIX.  

###  <a name="BKMK_ClientDeployExternalforLnU"></a> Dependências externas ao Configuration Manager:  
 As tabelas seguintes descrevem os sistemas operativos UNIX e Linux necessários e as dependências de pacote.  

 **Versão do Red Hat Enterprise Linux Server 5.1 (Tikanga)**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliotecas Padrão C|2.5-12|  
|Openssl|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|0.9.8b-8.3.el5|  
|PAM|Módulos de Autenticação Incorporável|0.99.6.2-3.14.el5|  

 **Versão do Red Hat Enterprise Linux Server 6**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliotecas Padrão C|2.12-1.7|  
|Openssl|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|1.0.0-4|  
|PAM|Módulos de Autenticação Incorporável|1.1.1-4|  

 **Versão do Red Hat Enterprise Linux Server 7**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliotecas Padrão C|2.17|  
|Openssl|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|1.0.1|  
|PAM|Módulos de Autenticação Incorporável|1.1.1-4|  

 **Solaris 10 SPARC**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|Patch de sistema operativo necessário|Fuga de memória de PAM|117463-05|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Bibliotecas de Matemática e de Microtarefas (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Bibliotecas de Matemática e de Microtarefas (Root) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Bibliotecas de Solaris Principais (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Bibliotecas de Solaris Principais (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|Openssl|Bibliotecas de SUNopenssl (Usr)<br /><br /> A Sun fornece as bibliotecas OpenSSL para o Solaris 10 SPARC. Estão incluídas no sistema operativo.|11.10.0,REV=2005.01.21.15.53|  
|PAM|Módulos de Autenticação Incorporável<br /><br /> SUNWcsr, Core Solaris, (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|Patch de sistema operativo necessário|Fuga de memória de PAM|117464-04|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (i386)|5.10,REV=2004.12.20|  
|SUNWlibmsr|Bibliotecas Math e Microtasking (Root) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Core Solaris, (Shared Libs) (i386)|11.10.0,REV=2005.01.21.16.34|  
|SUNWcslr|Bibliotecas de Solaris Core (Root) (i386)|11.10.0, REV=2005.01.21.16.34|  
|Openssl|Bibliotecas de SUNWopenssl; Bibliotecas de OpenSSL (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|Módulos de Autenticação Incorporável<br /><br /> SUNWcsr Core Solaris, (Root)(i386)|11.10.0,REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Bibliotecas de Matemática e Microtarefas (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Bibliotecas de Solaris Principais (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Solaris Principal (Root)|11.11, REV=2009.11.11|  
|Bibliotecas de SUNWopenssl|Bibliotecas de OpenSSL (Usr)|11.11.0,REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------|-----------|---------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Bibliotecas de Matemática e Microtarefas (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Bibliotecas de Solaris Principais (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Solaris Principal (Root)|11.11, REV=2009.11.11|  
|Bibliotecas de SUNWopenssl|Bibliotecas de OpenSSL (Usr)|11.11.0,REV=2010.05.25.01.00|  


 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc-2.4-31.30|Biblioteca partilhada padrão C|2.4-31.30|  
|Openssl|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|0.90,8a-18,15|  
|PAM|Módulos de Autenticação Incorporável|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|Biblioteca partilhada padrão C|2.9-13.2|  
|PAM|Módulos de Autenticação Incorporável|pam-1.0.2-20.1|  

 **Universal Linux (pacote Debian) Debian, Ubuntu Server**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|libc6|Biblioteca partilhada padrão C|2.3.6|  
|Openssl|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|0.9.8 ou 1.0|  
|PAM|Módulos de Autenticação Incorporável|0.79-3|  

 **Universais Linux (pacote RPM) CentOS, Oracle Linux**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Biblioteca partilhada padrão C|2.5-12|  
|Openssl|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|0.9.8 ou 1.0|  
|PAM|Módulos de Autenticação Incorporável|0.99.6.2-3.14|  


 **IBM AIX 6.1**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|Versão do SO|Versão do sistema operativo|AIX 6.1, qualquer Nível de Tecnologia e Service Pack|  
|xlC.rte|XL C/C++ Runtime|9.0.0.5|  
|OpenSSL/openssl.base|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|0.9.8.4|  

 **IBM AIX 7.1 (Power)**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|Versão do SO|Versão do sistema operativo|AIX 7.1, qualquer Nível de Tecnologia e Service Pack|  
|xlC.rte|XL C/C++ Runtime||  
|OpenSSL/openssl.base|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede||  


 **HP-UX 11i v3 IA64**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|Base do Ambiente Operativo de HP-UX|B.110,310,0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Bibliotecas de desenvolvimento do IA específicas|B.110,31|  
|SysMgmtMin|Ferramentas de Implementação de Software Mínimas|B.110,310,0709|  
|SysMgmtMin.openssl|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|A.00.09.08d.002|  
|PAM|Módulos de Autenticação Incorporável|Em HP-UX, PAM faz parte dos componentes principais do sistema operativo. Não existem nenhumas outras dependências.|  

 **Dependências do Configuration Manager:** A tabela seguinte apresenta uma lista de funções de sistema de sites que suportam clientes Linux e UNIX. Para obter mais informações sobre estas funções do sistema de sites, veja [Determinar as funções do sistema de sites para clientes do System Center Configuration Manager](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

|Sistema de sites do Configuration Manager|Mais informações|  
|---------------------------------------|----------------------|  
|Ponto de gestão|Embora um ponto de gestão não é necessário para instalar um cliente do Configuration Manager para Linux e UNIX, tem de ter um ponto de gestão para transferir informações entre computadores cliente e servidores do Configuration Manager. Sem um ponto de gestão, não é possível gerir computadores cliente.|  
|Ponto de distribuição|O ponto de distribuição não é necessário para instalar um cliente de Configuration Manager para Linux e UNIX. No entanto, a função de sistema de sites é necessária se implementar software em servidores Linux e UNIX.<br /><br /> Porque o cliente do Configuration Manager para Linux e UNIX não suporta comunicações que utilizam SMB, os pontos de distribuição a que utilizar com o cliente tem de suportar comunicações HTTP ou HTTPS.|  
|Ponto de estado de contingência|O ponto de estado de contingência não é necessário para instalar um cliente de Configuration Manager para Linux e UNIX. No entanto, o ponto de estado de contingência aos computadores do site do Configuration Manager para enviar mensagens de estado quando não conseguirem comunicar com um ponto de gestão. O cliente também pode enviar o respetivo estado de instalação para o ponto de estado de contingência.|  

 **Requisitos de firewall**: Certifique-se de que as firewalls não bloqueiam as comunicações entre as portas que especificar como portas de pedido de cliente. O cliente para Linux e UNIX comunica diretamente com pontos de gestão, pontos de distribuição e pontos de estado de contingência.  

 Para obter informações sobre a as portas de pedido e a comunicação do cliente, veja [Configurar o Cliente para Linux e UNIX para Localizar Pontos de Gestão](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP).  

##  <a name="BKMK_PlanningforCommunicationsforLnU"></a> Planear a comunicação entre florestas confianças de entidades para servidores Linux e UNIX  
 Servidores Linux e UNIX que gere com o Configuration Manager funcionam como clientes do grupo de trabalho e requerem configurações semelhantes às clientes baseados em Windows que estão num grupo de trabalho. Para obter informações sobre comunicações a partir de computadores em grupos de trabalho, veja a secção [Comunicação entre florestas do Active Directory](../../../../core/plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest) do tópico [Comunicações entre pontos finais no System Center Configuration Manager](../../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

###  <a name="BKMK_ServiceLocationforLnU"></a> Localização do serviço pelo cliente para Linux e UNIX  
 A tarefa de localizar um servidor de sistema de sites que forneça serviços aos clientes é referida como localização de serviço. Ao contrário de um cliente baseado no Windows, o cliente para Linux e UNIX não utiliza o Active Directory para localização de serviço. Além disso, o cliente do Configuration Manager para Linux e UNIX não suporta uma propriedade de cliente que especifique o sufixo de domínio de um ponto de gestão. Em vez disso, o cliente toma conhecimento dos servidores de sistema de sites adicionais que fornecem serviços aos clientes a partir de um ponto de gestão conhecido, que é atribuído quando instala o software de cliente.  

 Para obter mais informações sobre a localização de serviço, veja a secção [Localização do Serviço e como os clientes determinam o seu ponto de gestão atribuído](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location) do tópico [Compreender a forma como os clientes localizam os recursos e os serviços do site no System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

##  <a name="BKMK_SecurityforLnU"></a> Planeamento de segurança e os certificados para servidores Linux e UNIX  
 Para comunicações seguras e autenticadas com sites do Configuration Manager, o cliente do Configuration Manager para Linux e UNIX utiliza o mesmo modelo para a comunicação que o cliente do Configuration Manager para Windows.  

 Quando instala o cliente Linux e UNIX, pode atribuir o cliente um certificado PKI que lhe permite utilizar HTTPS para comunicar com sites do Configuration Manager. Se não atribuir um certificado PKI, o cliente cria um certificado autoassinado e comunica apenas por HTTP.  

 Os clientes aos quais é fornecido um certificado PKI, quando são instalados, utilizam HTTPS para comunicar com pontos de gestão. Quando um cliente não consegue localizar um ponto de gestão que suporte HTTPS, irá reverter para a utilização de HTTP com o certificado PKI fornecido.  

 Se um cliente do Linux ou UNIX utilizar um certificado PKI, não tem de aprová-lo. Quando um cliente utiliza um certificado autoassinado, reveja as definições de hierarquia para aprovação do cliente na consola do Configuration Manager. Se o método de aprovação do cliente não for **Aprovar automaticamente todos os computadores (não recomendado)**, terá de aprovar manualmente o cliente.  

 Para obter mais informações sobre como aprovar manualmente o cliente, veja a secção [Gerir Clientes a partir do Nó Dispositivos](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) do tópico [Como gerir clientes no System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

 Para obter informações sobre como utilizar certificados no Configuration Manager, consulte [requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

###  <a name="BKMK_AboutCertsforLnU"></a> Sobre os certificados para utilização por servidores Linux e UNIX  
 O cliente do Configuration Manager para Linux e UNIX utiliza um certificado autoassinado ou um certificado x. 509 PKI, tal como os clientes baseados em Windows. Não foram efetuadas alterações aos requisitos do PKI para sistemas de sites do Configuration Manager quando gerir clientes Linux e UNIX.  

 Os certificados que utiliza para Linux e os clientes UNIX que comuniquem com sistemas de sites do Configuration Manager tem de estar no formato Public Key Certificate Standard (PKCS #12) e a palavra-passe tem de ser conhecida para poder especificá-la para o cliente quando especificar o certificado PKI.  

 O cliente do Configuration Manager para Linux e UNIX suporta um certificado PKI único e não suporta vários certificados. Por conseguinte, os critérios de seleção de certificado, configurar para um Gestor de configuração do site não se aplica.  

###  <a name="BKMK_ConfigCertsforLnU"></a> Configurar certificados para servidores Linux e UNIX  
 Para configurar um cliente de Configuration Manager para servidores Linux e UNIX utilizem comunicações HTTPS, tem de configurar o cliente para utilizar um certificado PKI no momento em que instala o cliente. Não é possível aprovisionar um certificado antes da instalação do software do cliente.  

 Ao instalar um cliente que utiliza um certificado PKI, utiliza o parâmetro de linha de comandos **-UsePKICert** para especificar a localização e o nome de um ficheiro PKCS#12 que contém o certificado PKI. Além disso, tem de utilizar o parâmetro de linha de comandos **-certpw** para especificar a palavra-passe do certificado.  

 Se não especificar **-UsePKICert**, o cliente gera um certificado autoassinado e tenta comunicar com os servidores do sistema de sites através de HTTP apenas.  

##  <a name="BKMK_NoSHA-256"></a> Sobre o Linux e UNIX sistemas operativos que efetue não, como suporte de SHA-256  
 Os seguintes Linux e UNIX sistemas operativos que são suportados como clientes do Configuration Manager foram lançados com versões do OpenSSL que não suportam SHA-256:  

-   Versões do Solaris 10 (SPARC/x86)  


 Para gerir estes sistemas operativos com o Configuration Manager, tem de instalar o cliente do Configuration Manager para Linux e UNIX com um comutador de linha de comandos que direciona o cliente para ignorar a validação de SHA-256. Clientes do Configuration Manager que executam estas versões de sistema operativo funcionam num modo menos seguro do que os clientes que suportam SHA-256. Este modo menos seguro de funcionamento tem o seguinte comportamento:  

-   Os clientes não validam a assinatura do servidor do site associada à política que solicitam de um ponto de gestão.  

-   Os clientes não validam o hash dos pacotes que transferiram de um ponto de distribuição.  

> [!IMPORTANT]  
>  A opção **ignoreSHA256validation** permite executar o cliente para computadores com Linux e UNIX num modo menos seguro. Destina-se à utilização em plataformas mais antigas que não incluíam suporte para SHA-256. Trata-se uma substituição de segurança e não é recomendada pela Microsoft, mas é suportada para utilização num ambiente de centro de dados seguro e fidedigno.  

 Quando instala o cliente do Configuration Manager para Linux e UNIX, o script de instalação verifica a versão do sistema operativo. Por predefinição, se a versão do sistema operativo for identificada como tendo sido lançada sem uma versão do OpenSSL que suporte SHA-256, a instalação do cliente do Configuration Manager falha.  

 Para instalar o cliente de Configuration Manager em sistemas operativos Linux e UNIX que não foram lançados com uma versão do OpenSSL que suporte SHA-256, tem de utilizar o parâmetro da linha de comandos de instalação **ignoreSHA256validation**. Quando utiliza esta opção de linha de comandos num sistema operativo aplicável Linux ou UNIX, o cliente do Configuration Manager irá ignorar a validação de SHA-256 e após a instalação, o cliente não utilizará SHA-256 para assinar os dados que enviar para sistemas de sites através de HTTP. Para obter informações sobre a configuração de clientes Linux e UNIX para utilizarem certificados, veja [Planear a Segurança e os Certificados para Servidores Linux e UNIX](#BKMK_SecurityforLnU) neste tópico. Para obter informações sobre a necessidade de SHA-256, veja a secção [Configurar a Assinatura e Encriptação](../../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption) do tópico [Configurar a segurança no System Center Configuration Manager](../../../../core/plan-design/security/configure-security.md).  

> [!NOTE]  
>  A opção **ignoreSHA256validation** da linha de comandos é ignorada em computadores que executem uma versão do Linux e UNIX que foi lançada com versões do OpenSSL que suportam SHA-256.  

---
title: Ferramenta manutenção da hierarquia
titleSuffix: Configuration Manager
description: Compreender o que faz a ferramenta manutenção da hierarquia, e por que pode usá-lo. Inclui referência de opções da linha de comandos.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cead6825-6113-4ba5-a381-ac3598dfee86
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 87819530c5a37885c66611da0ba66c1a8872ac57
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156632"
---
# <a name="hierarchy-maintenance-tool-preinstexe-for-system-center-configuration-manager"></a>Ferramenta Manutenção da Hierarquia (Preinst.exe) para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A ferramenta de manutenção da hierarquia (Preinst.exe) transmite comandos para o System Center Configuration Manager hierarquia Manager enquanto o serviço de Gestor da hierarquia está em execução. A ferramenta manutenção da hierarquia é instalada automaticamente quando instala um site do Configuration Manager. Pode encontrar Preinst.exe no \\ &lt; *SiteServerName*> \SMS_&lt;*SiteCode*\bin\X64\00000409 pasta partilhada no servidor do site.  

 Pode utilizar a ferramenta Manutenção da Hierarquia nos seguintes cenários:  

-   Quando é necessária uma troca de chaves segura, existem situações em que é necessário efetuar manualmente a troca inicial de chaves públicas entre sites. Para obter mais informações, veja [Trocar Manualmente Chaves Públicas Entre Sites](#BKMK_ManuallyExchangeKeys), neste tópico.  

-   Para remover tarefas ativas destinadas a um site de destino que já não está disponível.  

-   Para eliminar um servidor de site da consola do Configuration Manager quando não é possível desinstalar o site através da configuração. Por exemplo, se remover fisicamente um site do Configuration Manager sem primeiro programa de configuração em execução para desinstalar o site, as informações do site continuarão a existir na base de dados do site principal e site principal continuará a tentar comunicar com o site subordinado. Para resolver este problema, tem de executar a ferramenta manutenção da hierarquia e eliminar manualmente o site subordinado da base de dados do site principal.  

-   Para parar todos os serviços do Configuration Manager num site sem ter de parar os serviços individualmente.  

-   Quando estiver a recuperar um site, pode utilizar a opção CHILDKEYS para distribuir as chaves públicas de vários sites subordinados para o site de recuperação.  

Para executar a ferramenta Manutenção da Hierarquia, o utilizador atual deve ter privilégios administrativos no computador local. De igual modo, o utilizador deve ter explicitamente o direito de segurança Site - Administrador. Não é suficiente que o utilizador herde este direito pelo facto de ser membro de um grupo que tem essa permissão.  

## <a name="hierarchy-maintenance-tool-command-line-options"></a>Opções da Linha de Comandos da Ferramenta Manutenção da Hierarquia  
Quando utilizar a Ferramenta Manutenção da Hierarquia, deve executá-la localmente no servidor do site de administração central, do site primário ou do site secundário.  

Quando executa a ferramenta de manutenção da hierarquia, tem de utilizar a seguinte sintaxe: preinst.exe /&lt;opção\>. O que se segue são opções de linhas de comandos.  

 **/DELJOB &lt; *SiteCode* >**  -Utilize esta opção num site para eliminar todas as tarefas ou comandos desde o site atual até ao site de destino especificado.  

 **/DELSITE &lt; *ChildSiteCodeToRemove* >**  -Utilize esta opção num site principal para eliminar os dados de sites subordinados a partir da base de dados do site do site principal. Normalmente, utilize esta opção se o computador de um servidor do site for encerrado antes de desinstalar o site desse computador.  

> [!NOTE]  
>  A opção /DELSITE não desinstala o site no computador especificado pelo parâmetro ChildSiteCodeToRemove. Esta opção apenas remove as informações do site da base de dados do site do Configuration Manager.  

**/DUMP &lt; *SiteCode* >**  -Utilize esta opção no servidor do local site para escrever as imagens de controlo do site para a pasta raiz da unidade em que o site é instalado. Pode escrever uma imagem de controlo do site específica na pasta ou escrever todos os ficheiros de controlo do site na hierarquia.  

-   /DUMP &lt; *SiteCode*> escreve a imagem de controlo do site apenas para o site especificado.  

-   /DUMP escreve os ficheiros de controlo do site de todos os sites.  

Uma imagem é uma representação binária do ficheiro de controlo do site, que é armazenado na base de dados do site do Configuration Manager. A imagem de ficheiro de controlo do site capturada é a soma da imagem base com as imagens diferenciais pendentes.  

Depois de capturar uma imagem de ficheiro de controlo do site com a ferramenta manutenção da hierarquia, o nome do ficheiro está no formato sitectrl_&lt;*SiteCode*> gt;.ct0.  

**/STOPSITE** -Utilize esta opção no servidor do local site para iniciar um ciclo de encerramento para o serviço de Gestor de componentes do Site do Configuration Manager, que repõe parcialmente o site. Quando este ciclo de encerramento é executado, alguns serviços do Configuration Manager num servidor de site e seus sistemas de sites remotos são parados. Estes serviços são sinalizados para reinstalação. Devido a este ciclo de encerramento, algumas palavras-passe são alteradas automaticamente quando os serviços são reinstalados.  

> [!NOTE]  
>  Se pretender ver um registo de encerramento, reinstalação e alterações de palavras-passe do Gestor do Componentes do Site, ative o registo para este componente antes de utilizar esta opção da linha de comandos.  

Depois de ser iniciado, o ciclo de encerramento prossegue automaticamente, ignorando todos os componentes ou computadores sem resposta. No entanto, se o serviço Gestor de Componentes do Site não conseguir aceder a um sistema de sites remoto durante o ciclo de encerramento, os componentes instalados no sistema de sites remoto serão reinstalados quando o serviço Gestor de Componentes do Site for reiniciado. Quando é reiniciado, o serviço Gestor de Componentes do Site tenta repetidamente reinstalar todos os serviços sinalizados para reinstalação até ter êxito.  

Para reiniciar o serviço Gestor de Componentes do Site, utilize o Service Manager. Depois de ser reiniciado, todos os serviços afetados são desinstalados, reinstalados e reiniciados. Depois de utilizar a opção /STOPSITE para iniciar o ciclo de encerramento, não é possível evitar os ciclos de reinstalação depois de o serviço Gestor de Componentes do Site reiniciar.  

**/KEYFORPARENT** - utilize esta opção num site para distribuir a chave pública do site para um site principal.  

A opção /KEYFORPARENT coloca a chave pública do site no ficheiro &lt; *SiteCode*>. Unidade de CT4 na raiz do programa. Depois de executar preinst.exe com esta opção, copie manualmente o &lt; *SiteCode*>. Ficheiro de CT4 a pasta de...\Inboxes\hman.box do site principal (não box\pubkey).  

**/KEYFORCHILD** - utilize esta opção num site para distribuir a chave pública do site para um site subordinado.  

A opção /KEYFORCHILD coloca a chave pública do site no ficheiro &lt; *SiteCode*>. Unidade de CT5 na raiz do programa. Depois de executar preinst.exe com esta opção, copie manualmente o &lt; *SiteCode*>. Ficheiro de CT5 a pasta de...\Inboxes\hman.box do site subordinado (não box\pubkey).  

**/CHILDKEYS** - pode utilizar esta opção nos sites subordinados de um site que estiver a recuperar. Utilize esta opção para distribuir as chaves públicas de vários sites subordinados para o site de recuperação.  

A opção /CHILDKEYS coloca a chave do site onde executa a opção, bem como todos os sites subordinados chaves públicas para o ficheiro &lt; *SiteCode*>. CT6.  

Depois de executar preinst.exe com esta opção, copie manualmente o &lt; *SiteCode*>. Ficheiro de CT6 para a pasta de...\Inboxes\hman.box do site de recuperação (não box\pubkey).  

**/PARENTKEYS** - pode utilizar esta opção no site principal de um site que estiver a recuperar. Utilize esta opção para distribuir as chaves públicas de todos os sites principais para o site de recuperação.  

A opção /PARENTKEYS coloca a chave do site onde executa a opção e as chaves de cada site principal acima desse site no ficheiro &lt;SiteCode\>. CT7.  

Depois de executar preinst.exe com esta opção, copie manualmente o &lt; *SiteCode*>. Ficheiro de CT7 para a pasta de...\Inboxes\hman.box do site de recuperação (não box\pubkey).  

##  <a name="BKMK_ManuallyExchangeKeys"></a> Trocar manualmente chaves públicas entre Sites  
Por predefinição, o **exigir troca de chaves segura** opção está ativada para sites do Configuration Manager. Quando é necessária uma troca de chaves segura, existem duas situações em que é necessário efetuar manualmente a troca inicial de chaves entre sites:  

-   Se o esquema do Active Directory não tiver sido expandido para o Configuration Manager  

-   Sites do Configuration Manager não estão a publicar dados do site para o Active Directory  

Pode utilizar a ferramenta Manutenção da Hierarquia para exportar as chaves públicas para cada site. Depois de terem sido exportadas, tem de trocar manualmente as chaves entre os sites.  

> [!NOTE]  
>  Depois de trocar manualmente as chaves públicas, pode rever o ficheiro de registo **hman.log**, que regista as alterações da configuração do site e a publicação das informações do site nos Serviços de Domínio do Active Directory no servidor do site principal, para garantir que o site primário processou a nova chave pública.  

#### <a name="to-manually-transfer-the-child-site-public-key-to-the-parent-site"></a>Para transferir manualmente a chave pública do site subordinado para o site principal  

1.  Com sessão iniciada no site subordinado, abra uma linha de comandos e navegue para a localização do ficheiro **Preinst.exe**.  

2.  Escreva o seguinte para exportar a chave pública do site subordinado: **Preinst /keyforparent**  

3.  A opção /keyforparent coloca a chave pública do site subordinado no  **&lt;código do site\>. CT4** localizado na raiz da unidade do sistema de ficheiros.  

4.  Mover o  **&lt;código do site\>. CT4** ficheiros para o site principal  **&lt;diretório de instalação\>\inboxes\hman.box** pasta.  

#### <a name="to-manually-transfer-the-parent-site-public-key-to-the-child-site"></a>Para transferir manualmente a chave pública do site principal para o site subordinado  

1.  Com sessão iniciada no site principal, abra uma linha de comandos e navegue para a localização do ficheiro **Preinst.exe**.  

2.  Escreva o seguinte para exportar a chave pública do site principal: **Preinst /keyforchild**.  

3.  A opção /keyforchild coloca a chave pública do site principal no  **&lt;código do site\>. CT5** localizado na raiz da unidade do sistema de ficheiros.  

4.  Mover o  **&lt;código do site\>. CT5** do ficheiro para o  **&lt;diretório de instalação\>\inboxes\hman.box** diretório no site subordinado.  

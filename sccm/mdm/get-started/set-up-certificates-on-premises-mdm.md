---
title: Configurar certificados | Microsoft Docs
description: "Configure certificados para comunicações fidedignas para a gestão de dispositivos móveis no local no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
caps.latest.revision: "27"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 3d695a2a40fd86ad991a26db3dcecbbb9ca186cc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-certificates-for-trusted-communications-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Configurar certificados para comunicações fidedignas para a Gestão de Dispositivos Móveis no Local do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager no\-local gestão de dispositivos móveis requer o ponto de registo, ponto proxy de registo, ponto de distribuição e gestão de dispositivos do ponto de funções de sistema de sites para ser definido para comunicações fidedignas com os dispositivos geridos. Os servidores do sistema de sites que alojem uma ou mais dessas funções têm de ter um certificado PKI exclusivo vinculado ao servidor Web nesse sistema. Um certificado com a mesmo raiz do certificado nos servidores também tem de ser armazenado nos dispositivos geridos para estabelecer comunicação fidedigna com eles.  

 Para dispositivos associados a um domínio, os Serviços de Certificados do Active Directory instalam automaticamente o certificado necessário com a raiz fidedigna em todos os dispositivos. Para dispositivos não associados a um domínio, tem de obter um certificado válido com uma raiz fidedigna através de outros meios. Se utilizar a AC do site como a raiz fidedigna (que é a utilizada pelo Active Directory para dispositivos associados a um domínio), os servidores do sistema de sites para o ponto de registo e o ponto proxy de registo têm de ter um certificado emitido por essa AC vinculado aos mesmos.  

 Todos os dispositivos a gerir terão também de ter um certificado com a mesma raiz instalado no mesmos para suportarem comunicações fidedignas com as funções do sistema de sites. Para dispositivos inscritos em massa, pode incluir o certificado no pacote de inscrição que é adicionado ao dispositivo para inscrevê-lo quando o dispositivo for iniciado pela primeira vez por um utilizador. Para dispositivos inscritos pelo utilizador, tem de adicionar o certificado através de e-mail, transferência Web ou qualquer outro método.  

 Como alternativa para dispositivos não associados a um domínio, pode utilizar a raiz de uma AC pública conhecida (como a Verisign ou a GoDaddy) para emitir o certificado do servidor, evitando assim ter de instalar manualmente um certificado no dispositivo, porque a maioria dos dispositivos confia nativamente em ligações a servidores com a mesma raiz da AC pública. Esta é uma alternativa útil para dispositivos inscritos pelo utilizador, nos quais não é exequível instalar os certificados fidedignos através da AC do site em cada dispositivo.  

> [!IMPORTANT]  
>  Existem várias formas de configurar os certificados para comunicações fidedignas entre dispositivos e os servidores de sistema de sites para no\-no local a gestão de dispositivos móveis. As informações fornecidas neste artigo são um exemplo de uma forma de fazê-lo. Este método requer a execução de um servidor no site com a instalação da função Serviços de Certificados do Active Directory e a função dos serviços Autoridade de Certificação e Inscrição de Autoridade de Certificação via Web. Consulte [Serviços de Certificados do Active Directory](http://go.microsoft.com/fwlink/p/?LinkId=115018) para mais informações e orientação sobre esta função do Windows Server.  

 Para configurar o site do Configuration Manager para as comunicações SSL necessárias para nos\-local gestão de dispositivos móveis, siga estes passos de alto nível:  

-   [Configurar a autoridade de certificação (AC) para publicação de CRL](#bkmk_configCa)  

-   [Criar o modelo de certificado de servidor web na AC](#bkmk_certTempl)  

-   [Pedir o certificado de servidor web para cada função do sistema de sites](#bkmk_requestCert)  

-   [Vincular o certificado para o servidor web](#bkmk_bindCert)  

-   [Exportar o certificado com a mesma raiz como o certificado de servidor web](#bkmk_exportCert)  

##  <a name="bkmk_configCa"></a>Configurar a autoridade de certificação (AC) para publicação de CRL  
 Por predefinição, a autoridade de certificação (AC) utiliza listas de revogação de certificados (CRL) com base no LDAP que permite ligações para dispositivos associados a um domínio. Tem de adicionar CRLs baseados em HTTP à AC para que dispositivos não associados a um domínio sejam considerados fidedignos com emissões de certificados da AC. Estes certificados são necessários para as comunicações SSL entre os servidores que alojam as funções de sistema de sites do Configuration Manager e os dispositivos inscritos no\-no local a gestão de dispositivos móveis.  

 Siga os passos abaixo para configurar a AC para publicar automaticamente informações de CRL para a emissão de certificados que permitem ligações fidedignas para dispositivos associados e não associados a um domínio:  

1.  No servidor que executa a autoridade de certificação para o site, clique em **Iniciar** > **Ferramentas Administrativas** > **Autoridade de Certificação**.  

2.  Na consola da Autoridade de Certificação, clique com o botão direito do rato em **CertificateAuthority** e, em seguida, clique em **Propriedades**.  

3.  Nas propriedades de CertificateAuthority, clique no separador **Extensões**, certifique-se de que **Selecionar extensão** está definido como **Ponto de Distribuição da CRL (CDP)**  

4.  Selecione **http://<ServerDNSName\>/CertEnroll/<CAName\><CRLNameSuffix\><DeltaCRLAllowed\>.crl**. e as três opções abaixo:  

    -   **Inclua em CRLs. Os clientes utilizam isto para encontrar localizações Delta CRL.**  

    -   **Inclua na extensão CDP dos certificados emitidos.**  

    -   **Incluir na extensão IDP das CRLs emitidas**  

5.  Clique em de **módulo de saída** separador, clique em **propriedades...** , em seguida, selecione **permitir que os certificados sejam publicados para o sistema de ficheiros**.  

6.  Clique em **OK** quando for notificado de que os Serviços de Certificados do Active Directory têm de ser reiniciados.  

7.  Clique com o botão direito do rato em **Certificados Revogados**, clique em **Todas as Tarefas** e, em seguida, clique em **Publicar**.  

8.  Na caixa de diálogo Publicar CRL, selecione **Apenas delta CRL** e, em seguida, clique em **OK**.  

##  <a name="bkmk_certTempl"></a>Criar o modelo de certificado de servidor web na AC  
 Após a publicação da nova CRL na AC, o passo seguinte consiste em criar um modelo de certificado do servidor Web. Este modelo é necessário para emitir certificados para os servidores que alojam as funções do sistema de sites ponto de registo, ponto proxy de registo, ponto de distribuição e ponto de gestão de dispositivos. Estes servidores serão pontos finais SSL para comunicações fidedignas entre as funções do sistema de sites e os dispositivos inscritos.    Siga os passos abaixo para criar o modelo de certificado:  

1.  Crie um grupo de segurança denominado **Servidores MDM do ConfigMgr**, que contenha os servidores que executam os sistemas de sites que necessitam de comunicações fidedignas com os dispositivos inscritos.  

2.  Na consola da Autoridade de Certificação, clique com o botão direito do rato em **Modelos de Certificado** e clique em **Gerir** para carregar a consola de Modelos de Certificado.  

3.  No painel de resultados, clique com o botão direito do rato na entrada que apresenta **Servidor Web** na coluna **Nome a Apresentar do Modelo** e clique em **Duplicar Modelo**.  

4.  Na caixa de diálogo **Duplicar Modelo** , certifique-se de que **Windows 2003 Server, Enterprise Edition** se encontra selecionado e clique em **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**. O Configuration Manager não suporta modelos de certificado do Windows Server 2008 para comunicações fidedignas com HTTPS.  

    > [!NOTE]  
    >  Se a AC em utilização estiver no Windows Server 2012, não lhe será pedida a versão do modelo de certificado quando clicar em **Modelo Duplicado**. Em vez disso, especifique isto no separador **Compatibilidade** das propriedades do modelo, da seguinte forma:  
    >   
    >  **Autoridade de certificação**: **Windows Server 2003**  
    >   
    >  **Destinatário do certificado**: **Windows XP / Server 2003**  

5.  Na caixa de diálogo **Propriedades de Novo Modelo**, no separador **Geral**, introduza um nome de modelo para gerar os certificados Web que serão utilizados nos sistemas de sites do Configuration Manager, como **Servidor Web MDM do ConfigMgr**.  

6.  Clique no separador **Nome do Requerente**, selecione **Incorporar a partir das informações do Active Directory** e, no formato do nome do requerente, especifique **Nome DNS**. Desmarque a caixa de verificação do nome do requerente alternativo, se **Nome Principal de Utilizador (UPN)** estiver selecionado.  

7.  Clique no separador **Segurança** e remova a permissão **Inscrever** dos grupos de segurança **Admins do Domínio** e **Admins de Empresa**.  

8.  Clique em **Adicionar**, introduza **Servidores MDM do ConfigMgr** na caixa de texto e clique em **OK**.  

9. Selecione a permissão **Inscrever** para este grupo e não desmarque a permissão **Leitura**.  

10. Clique em **OK** e feche a consola Modelos de Certificado.  

11. Na consola da Autoridade de Certificação, clique com o botão direito do rato em **Modelos de Certificado**, clique em **Novo** e clique em **Modelo de Certificado a Emitir**.  

12. Na caixa de diálogo **Ativar Modelos de Certificado**, selecione o novo modelo que acabou de criar, **Servidor Web MDM do ConfigMgr** e, em seguida, clique em **OK**.  

##  <a name="bkmk_requestCert"></a>Pedir o certificado de servidor web para cada função do sistema de sites  
 Os dispositivos inscritos no\-local gestão de dispositivos móveis têm de confiar pontos finais SSL que aloja o ponto de registo, ponto proxy de registo, ponto de distribuição e ponto de gestão de dispositivos.  Os passos abaixo descrevem como pedir o certificado de servidor Web do IIS. Tem de efetuar esta ação para cada servidor (ponto final SSL) que aloja uma das funções do sistema de sites necessárias no\-no local a gestão de dispositivos móveis.  

1.  No servidor do site primário, abra a linha de comandos com a permissão de administrador, escreva **MMC** e prima **Enter**.  

2.  Na MMC, clique em **Ficheiro** > **Adicionar/Remover Snap-in**.  

3.  No snap-in Certificados, selecione **Certificados**, clique em **Adicionar**, selecione **Conta de computador**, clique em **Seguinte**, clique em **Concluir** e, em seguida, clique em **OK** para sair da janela Adicionar ou Remover Snap-in.  

4.  Clique com o botão direito do rato em **Pessoal** e, em seguida, clique em **Todas as Tarefas** > **Requisitar um Novo Certificado**.  

5.  No assistente de Inscrição de Certificado, clique em **Seguinte**, selecione **Política de Inscrição do Active Directory** e clique em **Seguinte**.  

6.  Selecione a caixa de verificação junto ao certificado do servidor Web (**Servidor Web MDM do ConfigMgr**) e, em seguida, clique em **Inscrever**.  

7.  Uma vez inscrito o certificado, clique em **Concluir**.  

 Porque cada servidor precisará de um certificado de servidor web exclusivo, terá de repetir este processo para cada servidor que aloja uma das funções do sistema de sites necessárias no\-no local a gestão de dispositivos móveis.  Se um servidor alojar todas as funções do sistema de sites, apenas terá de pedir um certificado de servidor Web.  

##  <a name="bkmk_bindCert"></a>Vincular o certificado para o servidor web  
 O novo certificado agora tem de ser vinculado ao servidor web de cada servidor do sistema de sites que alojam as funções do sistema de sites necessárias no\-no local a gestão de dispositivos móveis. Siga os passos abaixo para cada servidor que aloja as funções do sistema de sites ponto de registo e ponto proxy de registo. Se um servidor alojar todas as funções do sistema de sites, basta seguir estes passos uma vez. Não é necessário executar esta tarefa para as funções do sistema de sites ponto de distribuição e ponto de gestão de dispositivos, uma vez que estas recebem automaticamente o certificado necessário durante a inscrição.  

1.  No servidor que aloja o ponto de registo, o ponto proxy de registo, o ponto de distribuição ou o ponto de gestão de dispositivos, clique em **Iniciar** > **Ferramentas Administrativas** > **Gestor de IIS**.  

2.  Em ligações, navegue para e faça duplo clique **Web Site predefinido**e, em seguida, clique em **editar enlaces...**  

3.  Na caixa de diálogo enlaces de Site, clique em **https**e, em seguida, clique em **editar...**  

4.  Na caixa de diálogo Editar Enlace de Site, selecione o certificado que acabou de inscrever para o **Certificado SSL**, clique em **OK** e, em seguida, clique em **Fechar**.  

5.  Na consola do Gestor de IIS, em Ligações, selecione o servidor Web e, em seguida, no painel Ações à direita, clique em **Reiniciar**.  

##  <a name="bkmk_exportCert"></a>Exportar o certificado com a mesma raiz como o certificado de servidor web  
 Normalmente, os Serviços de Certificados do Active Directory instalam o certificado necessário a partir da AC em todos os dispositivos associados a um domínio. No entanto, os dispositivos não associados a um domínio não conseguirão comunicar com as funções do sistema de sites sem o certificado da AC de raiz. Para obter o certificado necessário para que os dispositivos comuniquem com as funções do sistema de sites, pode exportá-lo a partir do certificado vinculado ao servidor Web.  

 Siga estes passos para exportar o certificado de raiz do certificado do servidor Web.  

1.  No Gestor de IIS, clique em **Web Site predefinido**e, em seguida, no painel ação à direita, clique em **enlaces...**  

2.  Na caixa de diálogo enlaces de Site, clique em **https**e, em seguida, clique em **editar...**  

3.  Certifique-se o certificado de servidor web está selecionado e clique em **vista...**  

4.  Nas propriedades do certificado do servidor Web, clique em **Caminho da Certificação**, clique na raiz na parte superior do caminho da certificação e clique em **Ver Certificado**.  

5.  Nas propriedades do certificado de raiz, clique em **detalhes**e, em seguida, clique em **copiar para ficheiro...**  

6.  No Assistente Para Exportar Certificados, clique em **Seguinte**.  

7.  Certifique-se de que **Binário codificado DER X.509 (.CER)** está selecionado como formato e clique em **Seguinte**.  

8.  Para o nome de ficheiro, clique em **procurar...** , escolha uma localização para guardar o ficheiro de certificado, nome de ficheiro e, em **guardar**.  

     Os dispositivos a inscrever precisarão de acesso a este ficheiro para importar o certificado de raiz. Por isso, escolha uma localização comum, acessível pela maioria dos computadores e dispositivos, ou pode guardá-lo agora numa localização prática (como a unidade C) e movê-lo mais tarde para a localização comum.  

     Clique em **Seguinte**.  

9. Reveja as definições e clique em **Concluir**.  

---
title: "Inscrição em massa de dispositivos para a MDM no local"
titleSuffix: Configuration Manager
description: "Inscrição em volume dispositivos de uma forma automática com gestão de dispositivos móveis no local no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
caps.latest.revision: "13"
caps.handback.revision: "0"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 3d2f61a60b4f78e5e1edb883b6a6834237a36acf
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Como a inscrição em massa de dispositivos com gestão de dispositivos móveis no local no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Inscrição em massa na gestão de dispositivos móveis no local do System Center Configuration Manager é um meio mais automatizado de inscrição de dispositivos, em comparação com a inscrição do utilizador, que requer que os utilizadores introduzam as respetivas credenciais para inscrever o dispositivo.  A inscrição em massa utiliza um pacote de inscrição para autenticar o dispositivo durante a inscrição. O pacote (um ficheiro .ppkg) contém um perfil de certificado e, opcionalmente, um perfil Wi-Fi se o dispositivo precisar de conectividade de intranet para suportar a inscrição.  

> [!NOTE]  
>  O ramo atual do Configuration Manager suporta a inscrição na gestão de dispositivos móveis no local para dispositivos que executam os sistemas operativos seguintes:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 Enterprise de IoT   

As tarefas seguintes explicam como em massa inscrever computadores e dispositivos para no\-no local a gestão de dispositivos móveis:  

-   [Criar um perfil de certificado](#bkmk_createCert)  

-   [Criar um perfil Wi-Fi](#CreateWifi)  

-   [Criar um perfil de inscrição](#bkmk_createEnroll)  

-   [Criar um ficheiro de pacote de inscrição (ppkg)](#bkmk_createPpkg)  

-   [Utilizar o pacote para inscrever um dispositivo em massa](#bkmk_getPpkg)  

-   [Verificar a inscrição de dispositivos](#bkmk_verifyEnroll)  

##  <a name="bkmk_createCert"></a> Criar um perfil de certificado  
 O componente principal do pacote de inscrição é um perfil de certificado, o qual é utilizado para aprovisionar automaticamente um certificado de raiz fidedigna para o dispositivo que está a ser inscrito.  Este certificado de raiz é necessário para a comunicação fidedigna entre os dispositivos e as funções do sistema de sites necessárias para em\-no local a gestão de dispositivos móveis. Sem o certificado de raiz, o dispositivo não seria fidedigno nas ligações HTTPS entre si e os servidores que alojam o ponto de registo, o ponto proxy de registo, o ponto de distribuição e as funções do sistema de sites do ponto de gestão de dispositivos.  

 Como parte da preparação do sistema no\-local gestão de dispositivos móveis, pode exporta um certificado de raiz que pode utilizar o perfil de certificado do pacote de inscrição. Para obter instruções sobre como obter o certificado de raiz fidedigna, consulte [exportar o certificado com a mesma raiz como o certificado de servidor web](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).  

 Utilize o certificado de raiz exportado para criar um perfil de certificado. Para obter instruções, consulte [como criar perfis de certificado no System Center Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md).  

##  <a name="CreateWifi"></a> Criar um perfil Wi-Fi  
 O outro componente do pacote utilizado para a inscrição em massa é um perfil Wi-Fi. Alguns dispositivos podem não ter a conectividade de rede necessária para suportar a inscrição até que as definições de rede sejam aprovisionadas. Incluir um perfil Wi-Fi no pacote de inscrição fornece um meio para estabelecer a conectividade de rede para o dispositivo.  

 Para criar um perfil de Wi-Fi no Configuration Manager, siga as instruções no [como criar perfis de Wi-Fi no System Center Configuration Manager](../../protect/deploy-use/create-wifi-profiles.md).  

> [!IMPORTANT]  
>Tenha os seguintes problemas de dois em consideração quando criar um perfil de Wi-Fi para inscrição em massa:
>
> - O ramo atual do Configuration Manager só suporta as seguinte configurações de segurança Wi-Fi para\-no local a gestão de dispositivos móveis:  
>   
>   - Tipos de segurança: **WPA2 Enterprise** ou **WPA2 pessoal**  
>   - Tipos de encriptação: **AES** ou **TKIP**  
>   - Tipos de EAP: **Smart Card ou outro certificado** ou **PEAP**  
>
>
> - Apesar do Configuration Manager possui uma definição de informações do servidor proxy no perfil de Wi-Fi, não configura o proxy quando o dispositivo está inscrito. Se precisar de configurar um servidor proxy com os dispositivos inscritos, pode implementar as definições de itens de configuração a utilizar assim que os dispositivos estão inscritos ou criar o segundo pacote utilizando o Windows Image and Configuration Designer (ICD) para implementar ao longo do lado do pacote de inscrição em massa.

##  <a name="bkmk_createEnroll"></a> Criar um perfil de inscrição  
 O perfil de inscrição permite especificar as definições necessárias para a inscrição de dispositivos, incluindo um perfil de certificado que aprovisionará dinamicamente um certificado de raiz fidedigna para o dispositivo e um perfil Wi-Fi que aprovisionará as definições de rede, se necessário.  

 Antes de criar um perfil de inscrição, certifique-se de que tem um perfil de certificado e um perfil Wi-Fi criados (se necessário). Para obter mais informações, consulte [Criar um perfil de certificado](#bkmk_createCert) e [Criar um perfil Wi-Fi](#CreateWifi).  

#### <a name="to-create-an-enrollment-profile"></a>Para criar um perfil de inscrição:  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** >**descrição geral** >**todos os dispositivos pertencentes** >**Windows** >**perfis de inscrição**.  

2.  Clique com o botão direito do rato em **Perfil de Inscrição** e, em seguida, clique em **Criar Perfil**.  

3.  No assistente Criar Perfil de Inscrição, introduza um nome para o perfil, certifique-se de que a opção **No Local** está selecionada para **Autoridade de Gestão**e, em seguida, clique em **Seguinte**.  

4.  Selecione o código do site e clique em **Seguinte**.  

5.  Selecione **Apenas Intranet**, selecione os pontos proxy de registo que o dispositivo irá utilizar para iniciar o processo de inscrição e clique em **Seguinte**.  

6.  Selecione o perfil de certificado que contém o certificado de raiz fidedigna (o perfil que criou em [Create a certificate profile](#bkmk_createCert)) e clique em **Seguinte**.  

7.  Selecione o perfil W-Fi que contém as definições de rede necessárias para que os dispositivos liguem à intranet (o perfil que criou em [Create a Wi-Fi profile](#CreateWifi)) e clique em **Seguinte**.  

    > [!NOTE]  
    >  Se não estiver a utilizar um perfil Wi-Fi para o pacote de inscrição, ignore este passo.  

8.  Confirme as definições para o perfil de inscrição e clique em **seguinte**. Clique em **Fechar** para sair do assistente.  

##  <a name="bkmk_createPpkg"></a> Criar um ficheiro de pacote de inscrição (ppkg)  
 O pacote de inscrição é o ficheiro utiliza a inscrição em massa de dispositivos no\-no local a gestão de dispositivos móveis.  Este ficheiro tem de ser criado com o Configuration Manager. Pode criar tipos de pacotes semelhantes com o Windows Image and Configuration Designer (ICD), mas apenas os pacotes que criar no Configuration Manager podem ser utilizados para inscrever dispositivos para no\-no local a gestão de dispositivos móveis do início ao fim. Os pacotes criados com o Windows ICD só podem fornecer o nome principal de utilizador (UPN) necessário para a inscrição, mas não podem executar o processo de inscrição efetivo.  

 O processo para criar o pacote de inscrição requer o Windows Assessment and Deployment Kit (ADK) para Windows 10.  No servidor que executa a consola do Configuration Manager, certifique-se de que tem a versão 1511 do Windows ADK instalada. Para mais informações, consulte a secção ADK em [Transferir kits e ferramentas para o Windows 10](https://msdn.microsoft.com/windows/hardware/dn913721.aspx)  

> [!TIP]  
>  Se remover um pacote de inscrição a partir da consola do Configuration Manager, não pode ser utilizado para inscrever dispositivos. Pode utilizar a remoção do pacote como uma forma de gerir pacotes que já não pretende utilizar na inscrição em massa de dispositivos.  

#### <a name="to-create-an-enrollment-package-ppkg-file"></a>Para criar um ficheiro de pacote de inscrição (ppkg):  

1.  Clique com o botão direito do rato no perfil de acabou de criar (em [Criar um perfil de inscrição](#bkmk_createEnroll)e clique em **Exportar**.  

2.  Clique em **Procurar**, encontre uma localização na qual pretenda guardar o ficheiro .ppkg, introduza um nome para o pacote e, em seguida, clique em **Guardar**.  

3.  Se pretender proteger o pacote por palavra-passe, clique na caixa de verificação junto a **Encriptar Pacote**, clique em **Exportar** e aguarde cerca de 10 segundos para concluir a exportação.  

    > [!NOTE]  
    >  Se encriptou o pacote, o Configuration Manager fornece uma mensagem com a palavra-passe desencriptada no mesmo. Certifique-se de que guarda as informações de palavra-passe, uma vez quer irá precisar das mesmas para aprovisionar o pacote em dispositivos.  

4.  Clique em **OK**.  

##  <a name="bkmk_getPpkg"></a> Utilizar o pacote para inscrever um dispositivo em massa  
 Pode utilizar o pacote para inscrever dispositivos antes ou depois de o dispositivo ter sido aprovisionado através do processo de experiência de primeira execução (OOBE).   O pacote de inscrição também pode ser incluído como parte do pacote de aprovisionamento de um fabricante de equipamento original (OEM).  

 O pacote tem de ser fornecido fisicamente ao dispositivo para ser utilizado na inscrição em massa. Pode fornecer o pacote de inscrição ao dispositivo de várias formas, consoante as suas necessidades, incluindo:  

-   Copiar do sistema de ficheiros  

-   Anexar ao e-mail  

-   Copiar por ligação de comunicação de proximidade (NFC)  

-   Copiar do cartão de memória  

-   Ler o código de barras  

-   Copiar de um dispositivo tethered  

-   Incluir no pacote de aprovisionamento do OEM  

#### <a name="to-bulk-enroll-a-device"></a>Para inscrever um dispositivo em massa:  

1.  No dispositivo a inscrever, localize o pacote de inscrição (utilizando o explorador de ficheiros) e faça duplo clique no ficheiro .ppkg.  

2.  Clique em **Sim** na mensagem Controlo de Conta de Utilizador.  

3.  Na caixa de diálogo a perguntar se o pacote provém de uma origem confia, clique em **Sim, adicioná-lo**.  

     O processo de inscrição é iniciado e demora cerca de 5 minutos.  

4.  Abra **Definições**.  

5.  Clique em  **Contas** > **Acesso a trabalho**. Quando a inscrição é efetuada com êxito, verá a uma conta em **CompanyApps**  

6.  Clique na conta e, em seguida, clique em **sincronização**, que inicia a gestão com o Configuration Manager.  

##  <a name="bkmk_verifyEnroll"></a> Verificar a inscrição de dispositivos  
 Pode verificar que dispositivos foram inscritos com êxito na consola do Configuration Manager.  

-   Inicie a consola do Configuration Manager.  

-   Clique em **Ativos e Compatibilidade** > **Descrição geral** > **Dispositivos**. O dispositivo inscrito aparece na lista.  

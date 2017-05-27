---
title: "Configurar a inscrição de dispositivos | Documentos do Microsoft"
description: "Conceda aos utilizadores permissão para inscrever os respetivos dispositivos para gestão de dispositivos móveis no local no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: 16d4106d486d821b7ce92a1de65ebb04469d18de
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="set-up-device-enrollment-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Configurar a inscrição de dispositivos para Gestão de Dispositivos Móveis no Local do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Permitir que os utilizadores inscrevem os respetivos dispositivos para o System Center Configuration Manager no\-local gestão de dispositivos móveis requer que conceder-lhes permissão para fazê-lo. Para conceder aos utilizadores permissão para inscrever dispositivos, siga as tarefas abaixo.

-   [Criar um perfil de inscrição que permite aos utilizadores inscreverem dispositivos modernos](#bkmk_createProf)  

-   [Configurar definições de cliente adicionais para dispositivos inscritos](#bkmk_addClient)  

-   [Permitir aos utilizadores receber o perfil de inscrição de dispositivos modernos](#bkmk_enableUsers)  

-   [Armazenar o certificado de raiz nos dispositivos a serem inscritos](#bkmk_storeCert)  

##  <a name="bkmk_createProf"></a> Criar um perfil de inscrição que permite aos utilizadores inscreverem dispositivos modernos  
 Para as definições necessárias para permitir que os utilizadores a inscrição de dispositivos modernos de emissão, pode adicionar um novo perfil de inscrição para as predefinições de cliente, que obtém aplicadas a todos os utilizadores detetados no site do Configuration Manager.  

1.  Na consola do Configuration Manager, clique em **administração** > **descrição geral** > **definições de cliente**, abra **predefinições de cliente** e selecione **inscrição**.  

2.  Em Definições do Dispositivo, especifique o intervalo de consulta para dispositivos modernos.  

3.  Em Definições do Utilizador, selecione **Sim** para **Permitir aos utilizadores inscreverem dispositivos modernos**.  

4.  Junto a **perfil de inscrição de dispositivos modernos**, clique em **definir perfil...**  e, em seguida, clique em **criar...**  

5.  Em Criar Perfil de Inscrição, escreva um nome para o perfil de inscrição e escolha o código do site de gestão que pretende que os utilizadores com o perfil de inscrição utilizem. Clique em **OK** várias vezes para sair da página Predefinições.  

> [!NOTE]  
>  Se quiser implementar o perfil de inscrição num subconjunto de utilizadores detetados, pode utilizar uma coleção de utilizadores e criar definições de cliente personalizadas a implementar nessa coleção. Para obter mais informações sobre como criar definições de cliente, veja [Como configurar definições do cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md)  

##  <a name="bkmk_addClient"></a> Configurar definições de cliente adicionais para dispositivos inscritos  
 Para além de configurar os dispositivos modernos do perfil de inscrição, pode configurar as definições de cliente adicionais para configurar dispositivos quando que estão a ser inscritos.  Para obter mais informações sobre como configurar definições de cliente, veja [Como configurar definições do cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

 Nem todas as definições de cliente estão disponíveis para no\-local gestão de dispositivos móveis. O ramo atual do Configuration Manager suporta as seguintes definições de cliente para\-local gestão de dispositivos móveis:  

-   Inscrição - Estas definições especificam o perfil de inscrição de dispositivos geridos. Para obter mais informações sobre como configurar um perfil de inscrição, veja [Criar um perfil de inscrição que permite aos utilizadores inscreverem dispositivos modernos](#bkmk_createProf).  

-   Política de cliente - Estas definições especificam a frequência de transferência da política de cliente para o dispositivo. Também pode ativar as definições para utilizadores com a consulta da política de atribuição de destinos. Para obter mais informações sobre as definições de política do cliente, veja [Acerca das definições de cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

-   Implementação de software - Esta definição define o intervalo para avaliar os dispositivos de cliente para implementações de software. Para obter mais informações sobre as definições de implementação do software, veja a secção Implementação de Software em [Acerca das definições de cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md)  

    > [!NOTE]  
    >  No\-local gestão de dispositivos móveis, implementação de software, definições só podem ser utilizadas como predefinições de cliente. Definições de implementação de software não podem ser utilizadas com definições personalizadas de cliente do ramo atual do Configuration Manager.  

##  <a name="bkmk_enableUsers"></a> Permitir aos utilizadores receber o perfil de inscrição de dispositivos modernos  
 Para que os utilizadores recebem as definições de cliente modificadas com o perfil de inscrição no\-local gestão de dispositivos móveis, tem de ser detetadas através do método de deteção do Active Directory. Para assegurar que todas as pessoas que necessitam do perfil de inscrição o obtêm, execute a deteção de utilizadores do Active Directory. Para informações sobre como detetar utilizadores, veja [Executar a deteção para o System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

##  <a name="bkmk_storeCert"></a> Armazenar o certificado de raiz nos dispositivos a serem inscritos  
 Os utilizadores com dispositivos associados a um domínio, já terão, provavelmente, o certificado de raiz necessário para a comunicação fidedigna com os servidores que alojam as funções do sistema de sites, uma vez que a raiz foi emitida como parte do processo de associação ao domínio com o Active Directory. Será necessário instalar manualmente nos computadores e dispositivos móveis não associados a um domínio o certificado de raiz para permitir a inscrição. Estes dispositivos não terão o certificado de raiz necessário automaticamente.  

 O ficheiro de certificado exportado tem de ser fornecido ao dispositivo para instalação manual, o que pode ser feito por e-mail, OneDrive, cartão SD, thumbdrive USB ou de outro método que melhor corresponda às suas necessidades.  

 O certificado de raiz que pretende utilizar nos dispositivos é aquele que exportou em [Exportar o certificado com a mesma raiz do certificado do servidor Web](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).  

1.  No dispositivo a ser inscrito, localize o ficheiro de certificado de raiz e faça duplo clique no mesmo.  

2.  Na janela de certificado, clique em **instalar certificado...**  

3.  No Assistente para Importar Certificados, selecione **Computador Local**e clique em **Seguinte**.  

4.  Na janela Controlo de Conta de Utilizador, clique em **Sim**.  

5.  Selecione **Colocar todos os certificados no seguinte arquivo**e clique em **Procurar**.  

6.  Clique em **Autoridades de Certificação de Raiz Fidedigna**, clique em **OK**e, em seguida, clique em **Seguinte**.  

7.  Clique em **Concluir**.  


---
title: A publicação e o esquema do Active Directory
titleSuffix: Configuration Manager
description: Expanda o esquema do Active Directory para o System Center Configuration Manager, para simplificar o processo de implementar e configurar os clientes.
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 39227689c484bfcf0df7f49365b196d59b5cfac4
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138352"
---
# <a name="prepare-active-directory-for-site-publishing"></a>Preparar o Active Directory para publicação de site

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando expande o esquema do Active Directory para o System Center Configuration Manager, introduz novas estruturas no Active Directory que são utilizados por sites do Configuration Manager para publicar informações chave numa localização segura onde os clientes possam aceder facilmente às-lo.  

É uma boa idéia usar o Configuration Manager com um esquema do Active Directory expandido quando gerir clientes no local. Um esquema expandido pode simplificar o processo de implementação e configuração de clientes. Um esquema expandido também permite que os clientes a localizarem com eficiência de recursos, como servidores de conteúdo e serviços adicionais que fornecem as diferentes funções do sistema de site do Configuration Manager.  

-   Se não estiver familiarizado com o esquema expandido fornece para uma implementação do Configuration Manager, pode ler sobre [extensões de esquema para o System Center Configuration Manager](../../../core/plan-design/network/schema-extensions.md) para ajudar a tomar esta decisão.  

-   Quando não utiliza um esquema expandido, pode configurar outros métodos, como DNS e WINS para localizar serviços e servidores do sistema de sites. Estes métodos de localização de serviços necessitam de configurações adicionais e não são o método preferencial dos clientes para localização de serviços. Para saber mais, leia [compreender como os clientes localizam os recursos de site e os serviços do System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md),  

-   Se o esquema do Active Directory foi expandido para o Configuration Manager 2007 ou o System Center 2012 Configuration Manager, em seguida, não precisa de fazer muito mais. As extensões de esquema permanecem inalteradas e já estará em vigor.  

A extensão do esquema é uma ação única para qualquer floresta. Para expandir e, em seguida, utilize o esquema do Active Directory expandido, siga estes passos:  

## <a name="step-1-extend-the-schema"></a>Passo 1. Expandir o esquema  
Para expandir o esquema para o Configuration Manager:  

-   Utilize uma conta que seja membro do grupo de segurança Admins de esquema.  

-   Entrar para o controlador de domínio de mestre de esquema.  

-   Executar o **Extadsch.exe** ferramenta ou utilize o utilitário de linha de comandos LDIFDE com o **configmgr_ad_schema. ldf** ficheiro. A ferramenta e o ficheiro estão na **SMSSETUP\BIN\X64** pasta no suporte de dados de instalação do Configuration Manager.  

#### <a name="option-a-use-extadschexe"></a>Opção a: Utilizar Extadsch.exe  

1.  Execute o **extadsch.exe** para adicionar as novas classes e atributos ao esquema do Active Directory.  

    > [!TIP]  
    >  Execute esta ferramenta a partir de uma linha de comandos para ver comentários durante a execução da mesma.  

2.  Certifique-se de que a extensão do esquema foi efetuada com êxito extadsch na raiz da unidade do sistema.  

#### <a name="option-b-use-the-ldif-file"></a>Opção b: Utilizar o ficheiro LDIF  

1.  Editar a **configmgr_ad_schema. ldf** ficheiro para definir o domínio de raiz do Active Directory que pretende expandir:  

    -   Substitua todas as instâncias do texto, **DC = x**, no ficheiro com o nome completo do domínio a expandir.  

    -   Por exemplo, se o nome completo do domínio a expandir for widgets.microsoft.com, altere todas as instâncias de DC = x no ficheiro para **DC = widgets, DC = microsoft, DC = com**.  

2.  Utilize o utilitário de linha de comandos LDIFDE para importar o conteúdo dos **configmgr_ad_schema. ldf** ficheiro serviços de domínio do Active Directory:  

    -   Por exemplo, a seguinte linha de comandos importa as extensões de esquema para serviços de domínio do Active Directory, ativa o registo verboso e cria um ficheiro de registo durante o processo de importação: **ldifde – i – f configmgr_ad_schema. ldf – v – j &lt; localização para armazenar o ficheiro de registo\>**.  

3.  Para verificar que a extensão do esquema foi bem sucedida, reveja o ficheiro de registo criado pela linha de comandos utilizada no passo anterior.  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>Passo 2.  Criar o contentor de Gestão do Sistema e conceder permissões de sites ao contentor  
 Depois de expandir o esquema, tem de criar um contentor com o nome **System Management** em serviços de domínio do Active Directory (AD DS):  

-   Cria este contentor uma vez em cada domínio que tenha um site primário ou secundário que irá publicar dados para o Active Directory.  

-   Para cada contentor, conceder permissões à conta de computador de cada servidor de site primário e secundário que irá publicar dados nesse domínio. Cada conta necessita **controlo total** para o contentor com a permissão avançada, **aplicar em**, igual ao **este objeto e todos os objetos subordinados**.  

#### <a name="to-add-the-container"></a>Adicionar o contentor  

1.  Utilize uma conta que tenha a permissão **Criar Todos os Objetos Subordinados** no contentor **Sistema** nos Serviços de Domínio do Active Directory.  

2.  Execute **ADSI Edit** (Adsiedit. msc) e estabeleça ligação ao domínio do servidor do site.  

3.  Crie o contentor:  

    -   Expanda **domínio** &lt;computador nome de domínio completamente qualificado\>, expanda &lt;nome único\>, clique com botão direito **CN = System**, escolha  **Novos**e, em seguida, escolha **objeto**.  

    -   Na **criar o objeto** caixa de diálogo caixa, escolha **contentor**e, em seguida, escolha **seguinte**.  

    -   Na **valor** , introduza **System Management**e, em seguida, escolha **seguinte**.  

4.  Atribuir permissões:  

    > [!NOTE]  
    >  Se preferir, pode utilizar outras ferramentas como o Active Directory Users and Computers ferramenta administrativa (DSA. msc) para adicionar permissões ao contentor.  

    -   Com o botão direito **CN = System Management**e, em seguida, escolha **propriedades**.  

    -   Escolha o **Security** separador, escolha **Add**e, em seguida, adicione a conta de computador do servidor de site com o **controlo total** permissão.  

    -   Escolher **avançadas**, selecione a conta de computador do servidor do site e, em seguida, escolha **editar**.  

    -   Na **aplicar em** lista, escolha **este objeto e todos os objetos subordinados**.  

5.  Escolher **OK** para fechar a consola e guardar a configuração.  

## <a name="step-3-set-up-sites-to-publish-to-active-directory-domain-services"></a>Passo 3. Configurar sites para publicar no Active Directory Domain Services  
 Depois do contentor está configurado, as permissões são concedidas e tiver instalado um site primário do Configuration Manager, pode configurar esse site para publicar dados do Active Directory.  

 Para obter mais informações sobre a publicação, consulte [publicar dados do site para o System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md).  

---
title: "Publicação e esquema do Active Directory | Documentos do Microsoft"
description: Expanda o esquema do Active Directory para o System Center Configuration Manager, para simplificar o processo de implementar e configurar os clientes.
ms.custom: na
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
caps.latest.revision: 17
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 88649111ea3a38c027efb4952211546afd0bf27e
ms.openlocfilehash: 58beef440db8e019a06ce7c4c8eaabc8e85ce954
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="prepare-active-directory-for-site-publishing"></a>Preparar o Active Directory para publicação de site

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando expande o esquema do Active Directory para o System Center Configuration Manager, introduz novas estruturas ao Active Directory que são utilizados por sites do Configuration Manager publique informações chave numa localização segura onde os clientes possam aceder facilmente aos-lo.  

É aconselhável utilizar o Configuration Manager com um esquema do Active Directory expandido quando gerir clientes no local. Um esquema expandido pode simplificar o processo de implementação e configuração de clientes. Um esquema expandido também esta definição permite aos clientes localizar forma eficiente recursos, como servidores de conteúdo e serviços adicionais que fornecem as diferentes funções do sistema de site do Configuration Manager.  

-   Se não estiver familiarizado com o esquema expandido fornece para uma implementação do Configuration Manager, pode ler sobre [extensões de esquema para o System Center Configuration Manager](../../../core/plan-design/network/schema-extensions.md) para o ajudar a tomar esta decisão.  

-   Quando não utiliza um esquema expandido, pode configurar outros métodos, como DNS e WINS para localizar serviços e servidores do sistema de sites. Estes métodos de localização de serviços necessitam de configurações adicionais e não são o método preferencial dos clientes para localização de serviços. Para obter mais informações, consulte o artigo [compreender como os clientes localizam os recursos do site e os serviços do System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md),  

-   Se o esquema do Active Directory tiver sido expandido para o Configuration Manager 2007 ou o System Center 2012 Configuration Manager, em seguida, precisa de fazer muito mais. As extensões de esquema são iguais e já estará no local.  

Expandir o esquema é uma ação única para qualquer floresta. Para expandir e, em seguida, utilize o esquema do Active Directory expandido, siga estes passos:  

## <a name="step-1-extend-the-schema"></a>Passo 1. Expandir o esquema  
Expandir o esquema para o Configuration Manager:  

-   Utilize uma conta que seja um membro do grupo de segurança Admins de esquema.  

-   Ter sessão iniciada com o controlador de domínio principal do esquema.  

-   Executar o **Extadsch.exe** ferramenta ou utilizar o utilitário da linha de comandos LDIFDE com o **configmgr_ad_schema. ldf** ficheiro. A ferramenta e o ficheiro estão a **SMSSETUP\BIN\X64** pasta no suporte de instalação do Configuration Manager.  

#### <a name="option-a-use-extadschexe"></a>Opção r: Utilizar Extadsch.exe  

1.  Execute o **extadsch.exe** para adicionar as novas classes e atributos ao esquema do Active Directory.  

    > [!TIP]  
    >  Execute esta ferramenta a partir de uma linha de comandos para ver comentários durante a execução da mesma.  

2.  Certifique-se de que a extensão do esquema foi bem sucedida consultando extadsch na raiz da unidade do sistema.  

#### <a name="option-b-use-the-ldif-file"></a>Opção b: Utilizar o ficheiro LDIF  

1.  Editar o **configmgr_ad_schema. ldf** ficheiro para definir o domínio de raiz do Active Directory que pretende expandir:  

    -   Substituir todas as instâncias do texto, **DC = x**, no ficheiro com o nome completo do domínio a expandir.  

    -   Por exemplo, se o nome completo do domínio a expandir for widgets.microsoft.com, altere todas as instâncias de DC = x no ficheiro para **DC = widgets, DC = microsoft, DC = com**.  

2.  Utilizar o utilitário da linha de comandos LDIFDE para importar os conteúdos do **configmgr_ad_schema. ldf** ficheiro para serviços de domínio do Active Directory:  

    -   Por exemplo, a linha de comandos importa as extensões de esquema para serviços de domínio do Active Directory, ativa o registo verboso e cria um ficheiro de registo durante o processo de importação: **ldifde -i -f configmgr_ad_schema. ldf - v -j &lt;localização para armazenar o ficheiro de registo\>**.  

3.  Para verificar que a extensão do esquema foi bem sucedida, rever um ficheiro de registo criado pela linha de comandos utilizada no passo anterior.  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>Passo 2.  Criar o contentor de Gestão do Sistema e conceder permissões de sites ao contentor  
 Depois de expandir o esquema, tem de criar um contentor com o nome **System Management** nos serviços de domínio do Active Directory (AD DS):  

-   Criar este contentor de uma vez em cada domínio que tenha um site primário ou secundário que irá publicar dados no Active Directory.  

-   Para cada contentor, conceder permissões para a conta de computador de cada servidor de site primário e secundário que publicarão os dados para esse domínio. Cada conta necessita de **controlo total** para o contentor com a permissão avançada, **aplicam-se para**, igual a **este objeto e os objetos subordinados**.  

#### <a name="to-add-the-container"></a>Adicionar o contentor  

1.  Utilize uma conta que tenha a permissão **Criar Todos os Objetos Subordinados** no contentor **Sistema** nos Serviços de Domínio do Active Directory.  

2.  Executar **ADSI Edit** (Adsiedit. msc) e estabeleça ligação ao domínio do servidor do site.  

3.  Crie o contentor:  

    -   Expanda **domínio** &lt;computador nome de domínio completamente qualificado\>, expanda &lt;nome único\>, com o botão direito **CN = System**, escolha **novo**e, em seguida, escolha **objeto**.  

    -   No **criar objeto** diálogo caixa, selecione **contentor**e, em seguida, escolha **seguinte**.  

    -   No **valor** caixa, introduza **System Management**e, em seguida, escolha **seguinte**.  

4.  Atribuir permissões:  

    > [!NOTE]  
    >  Se preferir, pode utilizar outras ferramentas como a Active Directory computadores ferramenta administrativa utilizadores e (DSA. msc) para adicionar permissões ao contentor.  

    -   Com o botão direito **CN = System Management**e, em seguida, escolha **propriedades**.  

    -   Escolha o **segurança** separador, escolha **adicionar**e, em seguida, adicione a conta de computador do servidor de site com o **controlo total** permissão.  

    -   Escolher **avançadas**, selecione a conta de computador do servidor de site e, em seguida, escolha **editar**.  

    -   No **aplicam-se para** lista, escolha **este objeto e os objetos subordinados**.  

5.  Escolher **OK** para fechar a consola e guardar a configuração.  

## <a name="step-3-set-up-sites-to-publish-to-active-directory-domain-services"></a>Passo 3. Configurar sites para publicar nos serviços de domínio do Active Directory  
 Depois do contentor está configurado, são concedidas permissões e tiver instalado um site primário do Configuration Manager, pode configurar o site para publicar dados do Active Directory.  

 Para obter mais informações sobre a publicação, consulte o artigo [publicar dados do site para o System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md).  


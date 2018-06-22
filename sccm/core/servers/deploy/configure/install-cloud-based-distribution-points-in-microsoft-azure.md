---
title: Instalar pontos de distribuição baseado na nuvem
titleSuffix: Configuration Manager
description: Saiba o que precisa de fazer para começar a utilizar pontos de distribuição baseado na nuvem no Microsoft Azure.
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2c9c79c5e635a50fecf02c46e2a134df87c2d784
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32338419"
---
# <a name="install-cloud-based-distribution-points-in-microsoft-azure-for-system-center-configuration-manager"></a>Instalar pontos de distribuição baseado na nuvem no Microsoft Azure para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode instalar pontos de distribuição baseados na nuvem do System Center Configuration Manager no Microsoft Azure. Se não estiver familiarizado com os pontos de distribuição baseados na nuvem, consulte [utilizar um ponto de distribuição baseados na nuvem](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) antes de continuar.

 Antes de iniciar a instalação, certifique-se de que os ficheiros de certificado necessários:  

-   Um certificado de gestão do Microsoft Azure que seja exportado para um ficheiro. cer e para um ficheiro. pfx.  

-   Um Gestor de configuração baseado na nuvem certificado ponto de distribuição serviço que seja exportado para um ficheiro. pfx.  

    > [!TIP]
    >   Para obter mais informações sobre estes certificados, consulte a secção de pontos de distribuição baseado na nuvem a [requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md) tópico. Para um exemplo de implementação do certificado de serviço do ponto de distribuição baseados na nuvem, consulte a secção "Implementar o certificado de serviço para pontos de distribuição baseado na nuvem" [exemplo passo a passo de implementação da PKI certificados para o System Center Configuration Manager: Autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  


 Depois de instalar o ponto de distribuição baseado na nuvem, Azure automaticamente gera um GUID para o serviço e o acrescenta este para o sufixo DNS de **cloudapp.net**. Utilizando este GUID, terá de configurar DNS com um alias de DNS (registo CNAME). Isto permite-lhe mapear o nome do serviço definido no certificado de serviço de ponto de distribuição baseados na nuvem do Configuration Manager para o GUID automaticamente gerado.  

 Se utilizar um servidor web proxy, poderá ter de configurar as definições de proxy para ativar a comunicação com o serviço em nuvem que aloja o ponto de distribuição.  

##  <a name="BKMK_ConfigWindowsAzureandInstallDP"></a> Configurar o Azure e instalar pontos de distribuição baseado na nuvem  
 Utilize os procedimentos seguintes para configurar o Azure para suportar pontos de distribuição e, em seguida, instale o ponto de distribuição baseado na nuvem no Configuration Manager.  

### <a name="to-set-up-a-cloud-service-in-azure-for-a-distribution-point"></a>Para configurar um serviço em nuvem no Azure para um ponto de distribuição  

1.  Abra um browser para o portal do Azure, no https://manage.windowsazure.come aceder à sua conta.  

2.  Clique em **serviços alojados, contas de armazenamento e CDN**e, em seguida, selecione **certificados de gestão**.  

3.  Faça duplo clique sua subscrição e, em seguida, selecione **adicionar certificado**.  

4.  Para **ficheiro de certificado**, especifique o ficheiro. cer que contém o certificado de gestão do Azure exportado a utilizar para este serviço em nuvem e, em seguida, clique em **OK**.  

O certificado de gestão será carregado no Azure e poderá agora instalar um ponto de distribuição baseado na nuvem.  

### <a name="to-install-a-cloud-based-distribution-point-for-configuration-manager"></a>Para instalar um ponto de distribuição baseados na nuvem para o Configuration Manager  

1.  Conclua os passos no procedimento anterior para configurar um serviço em nuvem no Azure com um certificado de gestão.  

2.  No **administração** área de trabalho da consola do Configuration Manager, expanda **serviços em nuvem**e selecione **pontos de distribuição de nuvem**. No **home page** separador, clique em **criar ponto de distribuição na nuvem**.  

3.  No **geral** página do assistente criar uma nuvem distribuição ponto, configure o seguinte:  

    -   Especifique o **ID de subscrição** para a sua conta do Azure.  

        > [!TIP]  
        >  Pode encontrar o ID de subscrição do Azure no portal do Azure.  

    -   Especifique o **certificado de gestão**. Clique em **procurar** para especificar o ficheiro. pfx que contém o certificado de gestão do Azure exportado e, em seguida, introduza a palavra-passe do certificado. Opcionalmente, pode especificar um ficheiro de 1. publishsettings da versão do Azure SDK 1.7.  

4.  Clique em **Seguinte**. O Configuration Manager liga-se no Azure para validar o certificado de gestão.  

5.  No **definições** página, efetue o seguinte e, em seguida, clique em **seguinte**:  

    -   Para **região**, selecione a região do Azure onde pretende criar o serviço em nuvem que aloja este ponto de distribuição.  

    -   Para **ficheiro de certificado**, especifique o ficheiro. pfx que contém o certificado exportado para o serviço de ponto de distribuição baseados na nuvem do Configuration Manager. Em seguida, introduza a palavra-passe.  

        > [!NOTE]  
        >  O **FQDN de serviço** caixa é preenchida automaticamente do nome de requerente do certificado. Na maioria dos casos, não terá editá-lo. A exceção é se estiver a utilizar um certificado de caráter universal num ambiente de teste. Por exemplo, neste caso, poderá não especificou o nome do anfitrião, para que vários computadores que tenham o mesmo sufixo DNS, podem utilizar o certificado. Neste cenário, o requerente do certificado contém um valor semelhante a **CN =\*. contoso.com**, e do Configuration Manager apresenta uma mensagem que tem de especificar o FQDN correto. Clique em **OK** para fechar a mensagem e, em seguida, introduza um nome específico antes do sufixo DNS para fornecer um FQDN completo. Por exemplo, poderá adicionar **clouddp1** para especificar a service FQDN do **clouddp1.contoso.com**. O FQDN de serviço tem de ser exclusivo no seu domínio e não corresponde a qualquer dispositivo associado a um domínio.  
        >   
        >  Certificados de caráter universal são suportados para só a ambientes de teste.  

6.  No **alertas** página, defina quotas de armazenamento, quotas de transferência e em que percentagem destas quotas pretende que o Configuration Manager para gerar alertas. Em seguida, clique em **Seguinte**.  

7.  Conclua o assistente.  

O assistente cria um novo serviço alojado para o ponto de distribuição baseado na nuvem. Depois de fechar o assistente, pode monitorizar o progresso da instalação do ponto de distribuição baseado na nuvem na consola do Configuration Manager. Também pode monitorizar o **CloudMgr.log** ficheiro no servidor do site primário. Pode monitorizar o aprovisionamento do serviço de nuvem no portal do Azure.  

> [!NOTE]  
>  Pode demorar até 30 minutos para aprovisionar um novo ponto de distribuição no Azure. A mensagem seguinte será repetida no **CloudMgr.log** ficheiros até que a conta de armazenamento seja aprovisionada: **A aguardar que verifique existência do contentor. Irá verificar novamente dentro de 10 segundos**. Em seguida, o serviço é criado e configurado.  

 Pode identificar que a instalação do ponto de distribuição baseados na nuvem é concluída, utilizando os seguintes métodos:  

-   No portal do Azure, o **implementação** apresenta o estado de distribuição baseado na nuvem ponto **pronto**.  

-   Na consola do Configuration Manager, no **administração** área de trabalho, **configuração da hierarquia**, **nuvem** nó, o ponto de distribuição baseado na nuvem apresenta o estado **pronto**.  

-   Configuration Manager apresenta um ID de mensagem de estado **9409** para o componente SMS_CLOUD_SERVICES_MANAGER.  

##  <a name="BKMK_ConfigDNSforCloudDPs"></a> Configurar a resolução de nomes para pontos de distribuição baseado na nuvem  
 Antes dos clientes podem aceder ao ponto de distribuição baseado na nuvem, deve conseguir resolver o nome do ponto de distribuição baseado na nuvem para um endereço IP que gere o Azure. Os clientes fazem-em duas fases:  

1.  Mapeiam o nome de serviço fornecido com o certificado do serviço de ponto de distribuição baseados na nuvem do Configuration Manager para o FQDN de serviço do Azure. Este FQDN contém um GUID e o sufixo DNS de **cloudapp.net**. O GUID é gerado automaticamente depois de instalar o ponto de distribuição baseado na nuvem. Pode ver o FQDN completo no portal do Azure, consultando o **URL do SITE** no dashboard do serviço em nuvem. Um exemplo de site URL é **http://d1594d4527614a09b934d470.cloudapp.net**.  

2.  Resolvem o FQDN de serviço do Azure para o endereço IP que o Azure atribui. Este endereço IP também pode ser identificado no dashboard para o serviço em nuvem no portal do Azure e é denominado **pública endereço IP VIRTUAL (VIP)**.  

Para mapear o nome de serviço fornecido com o certificado de serviço do ponto de distribuição baseados na nuvem do Configuration Manager (por exemplo, **clouddp1.contoso.com**) para o Azure FQDN de serviço (por exemplo, **d1594d4527614a09b934d470.cloudapp.net**), servidores DNS na Internet tem de ter um alias de DNS (registo CNAME). Os clientes podem, em seguida, resolver o FQDN de serviço do Azure para o endereço IP utilizando servidores DNS na Internet.  

##  <a name="BKMK_ConfigProxyforCloud"></a> Configurar as definições de proxy para sites primários que gerem serviços cloud  
 Ao utilizar serviços em nuvem com o Configuration Manager, o site primário que gere o ponto de distribuição baseados na nuvem tem de ser capaz de ligar ao portal do Azure. O site estabelece a ligação utilizando o **sistema** conta de computador do site primário. Esta ligação é efetuada utilizando o browser predefinido no computador do servidor de site primário.  

 No servidor do site primário que gere o ponto de distribuição baseados na nuvem, poderá ser necessário configurar as definições de proxy para ativar o site primário para aceder à Internet e ao Azure.  

 Utilize o procedimento seguinte para configurar definições de proxy do servidor do site primário na consola do Configuration Manager.  

> [!TIP]  
>  Pode também configurar o servidor proxy ao instalar novas funções do sistema de sites no servidor do site primário, utilizando o **Adicionar Assistente de funções de sistema de Site**.  

#### <a name="to-set-up-proxy-settings-for-the-primary-site-server"></a>Para configurar definições de proxy do servidor do site primário  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração** , expanda a opção **Configuração do Site**e clique em **Servidores e Funções do Sistema de Sites**. Em seguida, selecione o servidor de site primário que gere o ponto de distribuição baseados na nuvem.  

3.  No painel de detalhes, faça duplo clique **sistema de sites**e, em seguida, clique em **propriedades**.  

4.  No **propriedades do sistema de sites**, selecione o **Proxy** separador e, em seguida, configure as definições de proxy para este servidor de site primário.  

5.  Clique em **OK** para guardar as definições.  

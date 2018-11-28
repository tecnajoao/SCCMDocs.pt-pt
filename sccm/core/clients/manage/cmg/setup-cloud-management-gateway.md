---
title: Configurar o gateway de gestão na cloud
titleSuffix: Configuration Manager
description: Utilize este processo passo a passo para configurar um gateway de gestão da cloud (CMG).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 041ea28e91b77545b8984742b4199782d1edb6b7
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456537"
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurar o gateway de gestão na cloud para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*  

Esse processo inclui os passos necessários para configurar um gateway de gestão da cloud (CMG). 

> [!Tip]
> Esse recurso foi introduzido pela primeira vez na versão 1610 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1802, esta funcionalidade já não é uma funcionalidade de pré-lançamento.



## <a name="before-you-begin"></a>Antes de começar

Comece por ler o artigo [planear para o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway). Use esse artigo para determinar o design do CMG. 

Utilize a lista de verificação seguinte para se certificar de que tem as informações necessárias e pré-requisitos para criar um CMG:  

- O ambiente do Azure para utilizar. Por exemplo, nuvem pública do Azure ou a nuvem do Azure US Government.  

- Precisa de um ou mais certificados para CMG, dependendo de seu design. Para obter mais informações, consulte [certificados para o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).  

- A partir da versão 1802, selecione o **do Azure Resource Manager deployment**. Para obter mais informações, consulte [do Azure Resource Manager](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager). Precisa dos seguintes requisitos para um CMG de implementação Azure Resource Manager:  

    - Integração com o [do Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) para **gestão da Cloud**. Deteção de utilizadores do Azure AD não é necessária.  

    - O administrador da subscrição tem de iniciar sessão.  

- Precisa dos seguintes requisitos para uma implementação de serviço clássico de CMG:  

    > [!Important]  
    > A partir da versão 1810, implementações de serviço clássico no Azure foram preteridas no Configuration Manager. Começar a utilizar implementações do Azure Resource Manager para o gateway de gestão na cloud. Para obter mais informações, consulte [planear CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).  

    - ID de subscrição do Azure  

    - Certificado de gestão do Azure  

- Um nome globalmente exclusivo para o serviço. Este nome é a partir da [certificado de autenticação de servidor CMG](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate).  

- A região do Azure para esta implementação do CMG.  

- Quantas instâncias VM precisa para dimensionamento e a redundância.  



## <a name="set-up-a-cmg"></a>Configurar um CMG

Efetue este procedimento no site de nível superior. Esse site é um site primário autónomo ou o site de administração central.

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **serviços Cloud**e selecione **Gateway de gestão da nuvem**.  

2. Selecione **criar Gateway de gestão de Cloud** na faixa de opções.  

3. A partir da versão 1802, na página geral do assistente, selecione **do Azure Resource Manager deployment** como o método de implementação do CMG.  

    Selecione **iniciar sessão** para autenticar com uma conta de administrador de subscrição do Azure. O assistente é preenchido automaticamente os campos restantes das informações armazenadas durante o pré-requisito de integração do Azure AD. Se tiver várias subscrições, selecione o **ID de subscrição** da subscrição pretendida para utilizar.

    > [!Note]  
    > A partir da versão 1810, implementações de serviço clássico no Azure foram preteridas no Configuration Manager. 
    > 
    > Se precisar de utilizar uma implementação de serviço clássico, selecione essa opção nesta página. Entrar pela primeira vez do Azure **ID de subscrição**. Em seguida, selecione **procurar**e escolha o. Ficheiro PFX do certificado de gestão do Azure. 

4. Especifique a **ambiente do Azure** para este CMG. As opções na lista pendente podem variar consoante o método de implementação.  

5. Selecione **seguinte**. Aguarde enquanto o site testa a ligação para o Azure.  

4. Na página Definições do assistente, selecione **procurar** e escolha o. Ficheiro PFX para o certificado de autenticação de servidor do CMG. O nome a partir deste certificado preenche necessários **FQDN de serviço** e **nome do serviço** campos.  

   > [!NOTE]  
   > A partir da versão 1802, o certificado de autenticação de servidor CMG suporta carateres universais. Se utilizar um certificado de caráter universal, substitua o asterisco (\*) no **FQDN de serviço** campo com o nome de anfitrião desejado para CMG.  
   <!--491233-->  

5. Selecione o **região** na lista pendente para escolher a região do Azure para este CMG.  

6. Na versão 1802 e está usando uma implementação do Azure Resource Manager, selecione um **grupo de recursos** opção. 
   1. Se escolher **utilizar existente**, em seguida, selecione um grupo de recursos existente na lista pendente.
   2. Se escolher **criar novo**, em seguida, introduza o nome do grupo de recursos novo.

6. Na **instância de VM** , insira o número de VMs para este serviço. A predefinição é um, mas pode dimensionar até 16 VMs por CMG.  

7. Selecione **certificados** adicionar certificados de raiz fidedigno do cliente. Adicione até dois de raiz fidedigna CAs e quatro CAs (subordinada) intermediárias.  

    > [!Note]  
    > A partir da versão 1806, quando cria um CMG, já não tem de fornecer um certificado de raiz fidedigna na página Definições. Este certificado não necessárias ao utilizar o Azure Active Directory (Azure AD) para autenticação de cliente, mas utilizado para ser necessário no assistente. Se estiver a utilizar certificados de autenticação de cliente PKI, em seguida, ainda tem de adicionar um certificado de raiz fidedigna para CMG.<!--SCCMDocs-pr issue #2872-->  

8. Por predefinição, o assistente ativa a opção para **verificar revogação de certificados de cliente**. Uma lista de revogação de certificados (CRL) tem de ser publicada publicamente para esta verificação funcionar. Se não o publicar uma CRL, desmarque esta opção.  

9. A partir da versão 1806, por predefinição, o assistente permite que a seguinte opção: **Permitir CMG funcionar como um ponto de distribuição de nuvem e servir conteúdo a partir de armazenamento do Azure**. Agora um CMG também pode servir conteúdo aos clientes. Esta funcionalidade reduz os certificados necessários e o custo das VMs do Azure.  

10. Selecione **seguinte**.  

11. Para monitorizar o tráfego CMG com um limiar de 14 dias, selecione a caixa de verificação para ativar o alerta de limiar. Em seguida, especifique o limiar e a percentagem em que elevar os níveis de alerta diferentes. Escolher **seguinte** quando terminar.  

12. Reveja as definições e escolha **seguinte**. Gestor de configuração é iniciado como configurar o serviço. Depois de fechar o assistente, irá demorar entre 5 a 15 minutos para aprovisionar o serviço completamente no Azure. Verifique os **estado** coluna para o novo CMG determinar quando o serviço está pronto.  

 > [!Note]  
 > Para resolver problemas de implementações do CMG, utilize **Cloudmgr** e **CMGSetup.log**. Para obter mais informações, consulte [ficheiros de registo](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="configure-primary-site-for-client-certificate-authentication"></a>Configurar o site primário para a autenticação de certificado de cliente

Se estiver a utilizar [certificados de autenticação de cliente](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate) para clientes para se autenticar com o CMG, siga este procedimento para configurar cada site primário.  

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione **Sites**.  

2. Selecione o site primário para que os clientes baseados na internet são atribuídos em escolha **propriedades**.  

3. Mude para o **comunicações de computador do cliente** separador da folha de propriedades de site primário, verificação **certificado de cliente PKI de utilização (autenticação de cliente) quando estiverem disponíveis**.  

4. Se não o publicar uma CRL, desmarque a opção para **os clientes verificam a lista de revogação de certificados (CRL) para sistemas de sites**.  



## <a name="add-the-cmg-connection-point"></a>Adicionar o ponto de ligação do CMG

O ponto de ligação do CMG é a função de sistema de sites para comunicação com o CMG. Para adicionar o ponto de ligação do CMG, siga as instruções gerais para [instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles). Na página seleção da função de sistema do Assistente de função sistema de sites adicionar, selecione **ponto de ligação de gateway de gestão da Cloud**. Em seguida, selecione o **nome do gateway de gestão de Cloud** para que este servidor liga. O assistente mostra a região para CMG selecionado. 

> [!Important]
> O ponto de ligação do CMG tem de ter uma [certificado de autenticação de cliente](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate) em alguns cenários. 

 > [!Note]  
 > Para resolver problemas de estado de funcionamento do serviço CMG, utilize **CMGService.log** e **sms_cloud_proxyconnector**. Para obter mais informações, consulte [ficheiros de registo](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="configure-client-facing-roles-for-cmg-traffic"></a>Configurar funções de com clientes para o tráfego CMG

Configure as gestão software e de ponto de atualização ponto sistemas de sites para aceitar o tráfego CMG. Efetue este procedimento no site primário, para todos os pontos de gestão e atualização de software pontos de gestão de clientes baseados na internet.  

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **servidores e funções de sistema de sites** nó. No separador base do Friso, no grupo de vista, selecione **servidores com função**. Em seguida, selecione **ponto de gestão** da lista.  

2. Selecione o servidor de sistema de sites que pretende configurar para o tráfego CMG. Selecione o **ponto de gestão** função no painel de detalhes e, em seguida, selecione **propriedades** na faixa de opções.  

3. Na gestão ponto folha de propriedades em ligações de cliente, marque a caixa junto a **tráfego de gateway de gestão de nuvem de permitir que o Configuration Manager**. 
    - Consoante o design CMG e versão do Configuration Manager, poderá ter de ativar a **HTTPS** opção. Para obter mais informações, consulte [ativar o ponto de gestão para HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https).  

4. Selecione **OK** para fechar a janela de propriedades do ponto de gestão.   

Repita estes passos para pontos de gestão adicionais, conforme necessário e, para qualquer software pontos de atualização. 



## <a name="configure-clients-for-cmg"></a>Configurar clientes para CMG

Assim que estiver a executar as funções do sistema CMG e o site, os clientes obtêm a localização do serviço CMG automaticamente no próximo pedido de localização. Os clientes devem ser na intranet para receber a localização do serviço CMG, a menos que [instale e atribua os clientes do Windows 10 com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure). O ciclo de consulta para pedidos de localização é a cada 24 horas. Se não quiser aguardar que o pedido de localização normalmente agendada, pode forçar o pedido ao reiniciar o serviço de anfitrião de agente do SMS (ccmexec.exe) no computador.  

> [!Note]
> Por predefinição todos os clientes recebem uma política CMG. Controlar esse comportamento com o definição de cliente [permitir que os clientes utilizar um gateway de gestão da cloud](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway).

O cliente do Configuration Manager determina automaticamente se ele está na intranet ou na internet. Se o cliente pode contactar um controlador de domínio ou uma gestão no local ponto, ele define o tipo de ligação para **actualmente intranet**. Caso contrário, ele muda para **actualmente Internet**e utiliza a localização do serviço CMG para comunicar com o site.

>[!NOTE]
> Pode forçar o cliente utiliza sempre o CMG independentemente de ser na intranet ou na internet. Esta configuração é útil para fins de teste ou para os clientes em escritórios remotos que deseja forçar a utilizar o CMG. Defina a seguinte chave de registo no cliente:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> Também pode especificar esta definição durante a instalação do cliente usando o [CCMALWAYSINF=1](/sccm/core/clients/deploy/about-client-installation-properties#ccmalwaysinf) propriedade.

Para verificar que os clientes têm a política de especificar o CMG, abra um prompt de comando do Windows PowerShell como administrador no computador cliente e execute o seguinte comando: `Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

Este comando apresenta quaisquer pontos de gestão baseado na internet que o cliente tem conhecimento. Embora o CMG não seja tecnicamente um ponto de gestão baseado na internet, os clientes vê-lo como um.

 > [!Note]  
 > Para resolver o tráfego de cliente do CMG, utilize **CMGHttpHandler.log**, **CMGService.log**, e **sms_cloud_proxyconnector**. Para obter mais informações, consulte [ficheiros de registo](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="modify-a-cmg"></a>Modificar um CMG

Depois de criar um CMG, pode modificar algumas das suas configurações. Selecionar de CMG na consola do Configuration Manager e selecione **propriedades**. Configure as definições nas seguintes guias:  

#### <a name="general"></a>Geral

- **Certificado de gestão do Azure**: alterar o certificado de gestão do Azure para o CMG. Esta opção é útil ao atualizar o certificado antes de expirar.  

#### <a name="settings"></a>Definições

- **Ficheiro de certificado**: alterar o certificado de autenticação de servidor para CMG. Esta opção é útil ao atualizar o certificado antes de expirar.  

- **Instância de VM**: alterar o número de máquinas virtuais que o serviço utiliza no Azure. Esta definição permite-lhe dimensionar dinamicamente o serviço ou reduzir verticalmente com base na utilização ou de considerações de custo.  

- **Certificados**: Adicionar ou remover raiz fidedigna ou certificados de AC intermediária. Esta opção é útil ao adicionar novas CAs ou extinguir certificados expirados.  

- **Certifique-se de revogação de certificados de cliente**: se originalmente não ativar esta definição quando criar CMG, pode ativá-la posteriormente depois de publicar a CRL.  

- **Permitir CMG funcionar como um ponto de distribuição de nuvem e servir conteúdo a partir de armazenamento do Azure**: A partir da versão 1806, esta nova opção está ativada por predefinição. Agora um CMG também pode servir conteúdo aos clientes. Esta funcionalidade reduz os certificados necessários e o custo das VMs do Azure.<!--1358651-->  

#### <a name="alerts"></a>Alertas
Reconfigure os alertas a qualquer altura depois de criar CMG. 


### <a name="redeploy-the-service"></a>Reimplemente o serviço

Alterações mais significativas, como as seguintes configurações, necessitam de voltar a implementar o serviço:
- Método de implementação clássica para Azure Resource Manager
- Subscrição
- Nome do serviço
- Privado para PKI pública
- Região

Mantenha sempre pelo menos um CMG Active Directory para clientes baseados na internet receber a política atualizada. Clientes baseados na Internet não consegue comunicar com um CMG foi removido. Os clientes não sabem sobre uma nova até que eles se movem para a intranet. Ao criar uma segunda instância CMG para eliminar a primeira, também crie outro ponto de ligação do CMG.

Política de atualização de clientes por predefinição a cada 24 horas, por isso, aguarde pelo menos um dia depois de criar um novo CMG antes de eliminar antigo. Se os clientes são desligados ou sem uma ligação à internet, terá de esperar mais tempo. 

A partir da versão 1802, se tiver um CMG existente no método de implementação clássica, terá de implementar um novo CMG para utilizar o método de implementação Azure Resource Manager.<!--509753--> Existem duas opções:  

- Se quiser reutilizar o mesmo nome de serviço:  

    1. Primeiro de eliminar o CMG clássico, tendo em conta as orientações tenham sempre pelo menos um CMG Active Directory para clientes baseados na internet.  

    2. Crie um novo CMG através de uma implementação do Resource Manager. Reutilize o mesmo certificado de autenticação de servidor.  

    3. Reconfigure o ponto de ligação CMG para utilizar a nova instância do CMG.  

- Se pretender utilizar um novo nome de serviço:  

    1. Crie um novo CMG através de uma implementação do Resource Manager. Utilize um novo certificado de autenticação de servidor.  

    2. Crie um novo ponto de ligação CMG e ligação com o novo CMG.  

    3. Aguarde pelo menos um dia para clientes baseados na internet receber a política sobre a nova CMG.  

    4. Elimine o CMG clássico.  

> [!Tip]  
> Para determinar o modelo de implementação atual de um CMG:<!--SCCMDocs issue #611-->  
> 1. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **serviços Cloud**e selecione o **Gateway de gestão da nuvem** nó.  
> 2. Selecione a instância do CMG.  
> 3. No painel de detalhes na parte inferior da janela, procure o **modelo de implementação** atributo. Para uma implementação do Resource Manager, este atributo é **do Azure Resource Manager**. 
> 
> Também pode adicionar os **modelo de implementação** atributo como uma coluna para a vista de lista.  


### <a name="modifications-in-the-azure-portal"></a>Modificações no portal do Azure

Só deve modificar o CMG a partir da consola do Configuration Manager. Modificações para o serviço ou VMs diretamente no Azure subjacentes não não suportada. Todas as alterações poderão perder-se sem aviso prévio. Tal como acontece com qualquer PaaS, o serviço pode recriar as VMs a qualquer altura. Estes recompilações podem acontecer para manutenção de hardware de back-end, quer a aplicar as atualizações do SO da VM.


### <a name="delete-the-service"></a>Eliminar o serviço

Se precisar de eliminar o CMG, também fazer isso partir da consola do Configuration Manager. Remover manualmente os componentes no Azure faz com que o sistema para serem inconsistentes. Este Estado mantém informações órfãos e comportamentos inesperados podem ocorrer. 



## <a name="next-steps"></a>Passos seguintes

- [Monitorizar clientes para o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway)
- [Perguntas mais frequentes sobre o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)

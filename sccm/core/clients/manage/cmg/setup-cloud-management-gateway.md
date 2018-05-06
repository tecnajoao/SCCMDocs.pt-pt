---
title: Configurar o gateway de gestão de nuvem
titleSuffix: Configuraton Manager
description: Utilize este processo passo a passo para configurar um gateway de gestão de nuvem (CMG).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 04c1b262704ec6458bd9773c28c43a50d8fc0840
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurar o gateway de gestão de nuvem para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*  

Este processo inclui os passos necessários para configurar um gateway de gestão de nuvem (CMG). 

> [!Tip]
> Esta funcionalidade foi introduzida pela primeira vez na versão 1610 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1802, esta funcionalidade já não é uma funcionalidade de pré-lançamento.



## <a name="before-you-begin"></a>Antes de começar

Comece por ler o artigo [planear para o gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway). Utilize esse artigo para determinar a estrutura CMG. 

Utilize a lista de verificação seguinte para se certificar de que tem as informações necessárias e pré-requisitos para criar um CMG:  

- O ambiente do Azure a utilizar. Por exemplo, nuvem pública do Azure ou a nuvem do Azure US Government.  

- Precisa de um ou mais certificados para CMG, consoante a sua estrutura. Para obter mais informações, consulte [certificados para o gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).  

- A partir de versão 1802, escolha se utilizar o **implementação Azure Resource Manager** ou um **implementação de serviço clássico**. Para obter mais informações, consulte [do Azure Resource Manager](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager). Terá dos seguintes requisitos para uma implementação do Azure Resource Manager CMG:  

    - Integração com [do Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) para **nuvem gestão**. Não é necessária a deteção de utilizadores do Azure AD.  

    - Um administrador da subscrição tem de iniciar sessão.  

- Terá dos seguintes requisitos para uma implementação de serviço clássico de CMG:  

    - ID de subscrição do Azure  

    - Certificado de gestão do Azure  

- Um nome globalmente exclusivo para o serviço. Este nome é do [certificado de autenticação de servidor CMG](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate).  

- A região do Azure para esta implementação CMG.  

- Quantas instâncias VM necessário para a escala e redundância.  



## <a name="set-up-a-cmg"></a>Configurar um CMG

Efetue este procedimento no site de nível superior. Esse site é um site primário autónomo ou o site de administração central.

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **serviços em nuvem**e selecione **Gateway de gestão de nuvem**.  

2. Clique em **criar Gateway de gestão de nuvem** no Friso.  

3. Primeiro a partir de versão 1802, na página geral do assistente, escolha o método de implementação de CMG **implementação Azure Resource Manager** ou **implementação do serviço clássico**.  

    1. Para o **implementação Azure Resource Manager**: Clique em **sessão** para autenticar com uma conta de administrador de subscrição do Azure. O Assistente de auto-preenche os campos restantes das informações armazenadas durante o pré-requisito de integração do Azure AD. Se tiver várias subscrições, selecione o **ID de subscrição** da subscrição pretendida para utilizar.  

    2. Para o **implementação de serviço clássico**, *e versões do Configuration Manager 1706 e 1710*: introduza o seu Azure **ID de subscrição**. Em seguida, clique em **procurar** e selecione o. Ficheiro PFX para o certificado de gestão do Azure. 

4. Especifique o **ambiente do Azure** para este CMG. As opções na lista pendente podem variar consoante o método de implementação.  

5. Clique em **Seguinte**. Aguarde que o site testa a ligação ao Azure.  

4. Na página de definições do assistente, primeiro clique em **procurar** e selecione o. Ficheiro PFX para o certificado de autenticação de servidor CMG. O nome deste certificado preenche necessários **FQDN de serviço** e **nome do serviço** campos.  

   > [!NOTE]  
   > A partir de versão 1802, o certificado de autenticação de servidor CMG suporta carateres universais. Se utilizar um certificado de caráter universal, substitua o asterisco (\*) no **FQDN de serviço** campo com o nome do anfitrião para o CMG pretendido.  
   <!--491233-->  

5. Clique em de **região** na lista pendente para selecionar a região do Azure para este CMG.  

6. Na versão 1802 e estão a utilizar uma implementação do Azure Resource Manager, selecione um **grupo de recursos** opção. 
   1. Se optar por **utilizar existente**, em seguida, selecione um grupo de recursos existente na lista pendente.
   2. Se optar por **criar nova**, em seguida, introduza o nome do novo grupo de recursos.

6. No **instância de VM** campo, introduza o número de VMs para este serviço. A predefinição é um, mas pode dimensionar até 16 VMs por CMG.  

7. Clique em **certificados** adicionar certificados de raiz fidedigno do cliente. Adicione até duas de raiz fidedigna ACs e quatro ACs (subordinadas) intermediária.  

8. Por predefinição, o assistente ativa a opção para **verificar a revogação de certificados de cliente**. Uma lista de revogação de certificados (CRL) tem de ser publicada publicamente para esta verificação funcione. Se não publicar uma CRL, desmarque esta opção.  

9. Clique em **Seguinte**.  

10. Para monitorizar o tráfego CMG com um limiar de 14 dias, selecione a caixa de verificação para ativar o alerta do limiar. Em seguida, especifique o limiar e a percentagem no qual pretende elevar os níveis de alerta diferentes. Escolha **seguinte** quando tiver terminado.  

11. Reveja as definições e escolha **seguinte**. Gestor de configuração é iniciado como configurar o serviço. Depois de fechar o assistente, irá demorar entre cinco para 15 minutos para aprovisionar o serviço completamente no Azure. Verifique o **estado** coluna para o novo CMG determinar quando o serviço está pronto.  

 > [!Note]  
 > Para resolver implementações CMG, utilize **CloudMgr.log** e **CMGSetup.log**. Para obter mais informações, consulte [ficheiros de registo](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="configure-primary-site-for-client-certificate-authentication"></a>Configurar o site primário para autenticação de certificados de cliente

Se estiver a utilizar [certificados de autenticação de cliente](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate) para os clientes autenticar com o CMG, siga este procedimento para configurar cada site primário.  

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **configuração do Site**e selecione **Sites**.  

2. Selecione o site primário ao qual os clientes baseados na internet são atribuídos e escolham **propriedades**.  

3. Mudar para o **comunicações de computadores cliente** separador da folha de propriedades do site primário, verificação **certificado de cliente PKI de utilização (autenticação de cliente) se estiver disponível**.  

4. Se não publicar uma CRL, desmarque a opção para **clientes verificam a lista de revogação de certificados (CRL) para sistemas de sites**.  



## <a name="add-the-cmg-connection-point"></a>Adicionar o ponto de ligação CMG

O ponto de ligação de CMG é a função de sistema de sites para comunicação com o CMG. Para adicionar o ponto de ligação CMG, siga as instruções gerais para [instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles). Na página seleção da função de sistema do assistente função adicionar de sistema de sites, selecione **ponto de ligação de gateway de gestão de nuvem**. Em seguida, selecione o **nome do gateway de gestão de nuvem** para que este servidor liga. O assistente mostra a região para a CMG selecionado. 

> [!Important]
> O ponto de ligação CMG tem de ter um [certificado de autenticação de cliente](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate) em alguns cenários. 

 > [!Note]  
 > Para resolver o estado de funcionamento do CMG serviço, utilize **CMGService.log** e **SMS_Cloud_ProxyConnector.log**. Para obter mais informações, consulte [ficheiros de registo](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="configure-client-facing-roles-for-cmg-traffic"></a>Configurar funções de orientado para o cliente para o tráfego CMG

Configure as gestão software e de ponto de atualização ponto sistemas de sites para aceitar o tráfego CMG. Efetue este procedimento no site primário, para todos os pontos de gestão e atualização de software pontos de servir clientes baseados na internet.  

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **configuração do Site**, faça duplo clique **servidores e funções de sistema de sites**e selecione **Ponto de gestão** da lista.  

2. Selecione o servidor de sistema de sites que pretende configurar para o tráfego CMG. Selecione o **ponto de gestão** função no painel de detalhes e, em seguida, clique em **propriedades** no Friso.  

3. Na gestão ponto folha de propriedades em ligações de cliente, selecione a caixa junto **tráfego de gateway de gestão de nuvem de permitir que o Configuration Manager**. 
    - Consoante a estrutura CMG e versão do Configuration Manager, poderá ter de ativar o **HTTPS** opção. Para obter mais informações, consulte [ativar o ponto de gestão para HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https).  

4. Clique em **OK**.   

Repita estes passos para pontos de gestão adicionais, conforme necessário e pontos de atualização de software. 



## <a name="configure-clients-for-cmg"></a>Configurar clientes para CMG

Assim que estiver a executar as funções do sistema CMG e o site, os clientes obtêm a localização do serviço CMG automaticamente no próximo pedido de localização. Os clientes devem estar na intranet para receber a localização do serviço CMG, a menos que [instale e atribua os clientes Windows 10 com o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure). O ciclo de consulta de pedidos de localização é a cada 24 horas. Se não pretender aguardar que o pedido de localização normalmente agendada, pode forçar o pedido reiniciando o serviço de anfitrião de agente do SMS (ccmexec.exe) no computador.  

> [!Note]
> Por predefinição, todos os clientes recebem política CMG. Controlar este comportamento com o definição de cliente [permitir que os clientes utilizar um gateway de gestão de nuvem](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway).

O cliente do Configuration Manager determina automaticamente se está na intranet ou à internet. Se o cliente pode contactar um controlador de domínio ou uma gestão no local ponto, define o tipo de ligação **atualmente intranet**. Caso contrário, muda para **atualmente Internet**e utiliza a localização do serviço CMG para comunicar com o site.

>[!NOTE]
> Pode forçar o cliente utiliza sempre o CMG independentemente de ser na intranet ou à internet. Esta configuração é útil para fins de teste, ou para clientes em escritórios remotos que pretende para forçar a utilizar o CMG. Defina a seguinte chave de registo no cliente:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> Também pode especificar esta definição durante a instalação de cliente utilizar o [CCMALWAYSINF](/sccm/core/clients/deploy/about-client-installation-properties#ccmalwaysinf) propriedade.

Para verificar que os clientes têm a política de especificar o CMG, abra uma linha de comandos do Windows PowerShell como administrador no computador cliente e execute o seguinte comando: `Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

Este comando apresenta quaisquer pontos de gestão baseado na internet que conhece o cliente. Enquanto o CMG não é tecnicamente um ponto de gestão baseado na internet, parece como tal, os clientes.

 > [!Note]  
 > Para resolver o tráfego de cliente CMG, utilize **CMGHttpHandler.log**, **CMGService.log**, e **SMS_Cloud_ProxyConnector.log**. Para obter mais informações, consulte [ficheiros de registo](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="modify-a-cmg"></a>Modificar um CMG

Depois de criar um CMG, pode modificar algumas das respetivas definições. Selecione o CMG na consola do Configuration Manager e clique em **propriedades**. As seguintes definições são configuráveis:  

- **Geral**  

    - **Certificado de gestão do Azure**: alterar o certificado de gestão do Azure para o CMG. Esta opção é útil quando atualizar o certificado antes de expirar.  

- **Definições**  

    - **Ficheiro de certificado**: alterar o certificado de autenticação de servidor para o CMG. Esta opção é útil quando atualizar o certificado antes de expirar.  

    - **Instância de VM**: alterar o número de máquinas virtuais que utiliza o serviço no Azure. Esta definição permite-lhe dinamicamente dimensionar o serviço de cópia de segurança ou para baixo com base na utilização ou considerações de custo.  

    - **Certificados**: Adicionar ou remover certificados de AC intermediária ou de raiz fidedigna. Esta opção é útil quando adicionar novos ACs ou extinguir certificados expirados.  

    - **Verificar a revogação de certificado de cliente**: se a originalmente ativar esta definição quando criar o CMG, pode ativá-la, posteriormente, depois de publicar a CRL.  

- **Alertas**: pode reconfigurar os alertas em qualquer altura depois de criar o CMG. 

As alterações mais significativas, tais como as seguintes configurações, necessitam de voltar a implementar o serviço:
- Método de implementação clássica para o Azure Resource Manager
- Subscrição
- Nome do serviço
- Privado públicas PKI
- Região

Manter sempre, pelo menos, um CMG Active Directory para clientes baseados na internet receber a política atualizada. Os clientes baseados na Internet não consegue comunicar com um CMG removido. Os clientes não souber sobre uma nova até que são utilizados em roaming voltar à intranet. Ao criar uma segunda instância CMG para eliminar o primeiro, também crie outro ponto de ligação de CMG.

Política de atualização de clientes por predefinição a cada 24 horas, por isso, aguarde pelo menos um dia depois de criar um novo CMG antes de eliminar o antigo. Se os clientes são ativados, desativado ou sem uma ligação à internet, poderá ter de aguardar já. 

A partir de versão 1802, se tiver um CMG existente no método de implementação clássica, terá de implementar um novo CMG para utilizar o método de implementação Azure Resource Manager.<!--509753--> Existem duas opções:
- Se pretender reutilizar o mesmo nome de serviço:
    1. Elimine primeiro CMG clássico, tendo em conta as orientações para ter sempre pelo menos um CMG Active Directory para clientes baseados na internet.
    2. Crie um novo CMG utilizando uma implementação do Resource Manager. Reutilize o mesmo certificado de autenticação de servidor.
    3. Reconfigure o ponto de ligação de CMG para utilizar a nova instância CMG.
- Se pretender utilizar um novo nome de serviço:
    1. Crie um novo CMG utilizando uma implementação do Resource Manager. Utilize um novo certificado de autenticação de servidor.
    2. Crie um novo ponto de ligação de CMG e ligação com o novo CMG.
    3. Aguarde pelo menos um dia para clientes baseados na internet receber a política sobre a nova CMG.
    4. Elimine o CMG clássico.

Só deve modificar o CMG a partir da consola do Configuration Manager. Não é suportado efetuar alterações ao serviço ou subjacente VMs diretamente no Azure. As alterações poderão perder-se sem aviso prévio. Tal como acontece com quaisquer PaaS, o serviço pode recriar as VMs em qualquer altura. Estes Reconstrói pode acontecer para manutenção de hardware de back-end, ou para aplicar as atualizações para o SO de VM.

Se precisar de eliminar o CMG, tal também partir da consola do Configuration Manager. Remover manualmente os componentes no Azure faz com que o sistema para serem inconsistentes. Este Estado mantém informações órfãos e comportamentos inesperados poderão ocorrer. 



## <a name="next-steps"></a>Passos seguintes

- [Monitorizar clientes para gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway)
- [Perguntas mais frequentes sobre o gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)

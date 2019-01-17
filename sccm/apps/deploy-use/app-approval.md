---
title: Aprovar aplicações
titleSuffix: Configuration Manager
description: Saiba mais sobre as configurações e comportamentos para aprovação de aplicativos no Configuration Manager.
ms.date: 12/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 776d0a477d56a178927fb2d09866eacf63b4895a
ms.sourcegitcommit: d5c013a29f53b975fe3a6cb0a41f1e817bd7b235
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/16/2019
ms.locfileid: "54342793"
---
# <a name="approve-applications-in-configuration-manager"></a>Aprovar aplicações no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando [implementar uma aplicação](/sccm/apps/deploy-use/deploy-applications) no Configuration Manager, pode exigir a aprovação antes da instalação. Os utilizadores solicitem a aplicação no Centro de Software e, em seguida, rever o pedido na consola do Configuration Manager. Pode aprovar ou negar o pedido. 



## <a name="bkmk_approval"></a> Definições de aprovação

O comportamento de aprovação de aplicação depende da sua versão do Configuration Manager. Uma das seguintes definições de aprovação é apresentado no **definições de implementação** página de implementação da aplicação:  

#### <a name="require-administrator-approval-if-users-request-this-application"></a>Exigir aprovação do administrador caso os utilizadores solicitem esta aplicação
*Aplica-se a versões anteriores e 1710*

O administrador aprova quaisquer pedidos de utilizador para a aplicação antes do utilizador pode instalá-lo. Esta opção é desativada quando o objetivo de implementação for **necessário**, ou ao implementar a aplicação para uma coleção de dispositivos.  

Os pedidos de aprovação da aplicação são apresentados no nó **Pedidos de Aprovação** , sob **Gestão de Aplicações** , na área de trabalho **Biblioteca de Software** . Se um pedido não está aprovado dentro de 30 dias, este é removido. Reinstalar o cliente poderá cancelar quaisquer pedidos de aprovação pendentes.  

Depois que tenha aprovado uma aplicação para a instalação, poderá **negar** o pedido na consola do Configuration Manager. Esta ação não fazer com que o cliente desinstalar a aplicação a partir de todos os dispositivos. Ele deixa de que os utilizadores instalem novas cópias da aplicação do Centro de Software.  


#### <a name="an-administrator-must-approve-a-request-for-this-application-on-the-device"></a>Um administrador tem de aprovar um pedido para esta aplicação no dispositivo
*Se aplica a versões 1802 e posteriores <sup> [Nota 1](#bkmk_note1)</sup>*

<a name="bkmk_note1"></a>

> [!Note]  
> **Tenha em atenção 1**: O Configuration Manager não permite esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para mais informações, consulte [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options). 
> 
> Se não ativar esta funcionalidade, verá a experiência anterior.  

O administrador aprova quaisquer pedidos de utilizador para a aplicação antes do utilizador pode instalá-lo no dispositivo pedido. Se o administrador aprova o pedido, o utilizador só é possível instalar o aplicativo nesse dispositivo. O utilizador tem de submeter outro pedido para instalar a aplicação noutro dispositivo. Esta opção é desativada quando o objetivo de implementação for **necessário**, ou ao implementar a aplicação para uma coleção de dispositivos. <!--1357015-->  

> [!Note]  
> Para tirar partido das novas funcionalidades do Configuration Manager, primeiro de atualizar os clientes para a versão mais recente. Enquanto a nova funcionalidade surge na consola do Configuration Manager ao atualizar a consola e do site, o cenário completo não é funcional até que a versão do cliente também é a versão mais recente.<!--SCCMDocs issue 646-->  

Modo de exibição **pedidos de aprovação** sob **gestão de aplicações** no **biblioteca de Software** área de trabalho da consola do Configuration Manager. Existe agora uma **dispositivo** coluna na lista para cada solicitação. Quando pega a ação na solicitação, a caixa de diálogo de pedido de aplicação também inclui o nome de dispositivo a partir do qual o utilizador submeteu o pedido.  

Se um pedido não está aprovado dentro de 30 dias, este é removido. Reinstalar o cliente poderá cancelar quaisquer pedidos de aprovação pendentes.  

Depois que tenha aprovado uma aplicação para a instalação, poderá **negar** o pedido na consola do Configuration Manager. Esta ação não fazer com que o cliente desinstalar a aplicação a partir de todos os dispositivos. Ele deixa de que os utilizadores instalem novas cópias da aplicação do Centro de Software.  

> [!Important]  
> A partir da versão 1806, *foi alterado o comportamento* quando revogar a aprovação de um aplicativo que foi anteriormente aprovado e instalado. Agora quando **negar** o pedido para o aplicativo, o cliente desinstala a aplicação do dispositivo do utilizador.<!--1357891-->  



## <a name="bkmk_email-approve"></a> Notificações por e-mail
<!--1321550-->

A partir da versão 1810, configure notificações por e-mail para pedidos de aprovação de aplicações. Quando um utilizador solicita uma aplicação, receberá uma mensagem de e-mail. Clique em ligações no e-mail para aprovar ou negar o pedido, sem a necessidade de consola do Configuration Manager.

Pode definir os endereços de e-mail dos utilizadores que podem aprovar ou negar o pedido ao criar uma nova implementação da aplicação. Se precisar de alterar a lista de endereços de e-mail, posteriormente, vá para o **monitorização** área de trabalho, expanda **alertas**e selecione o **subscrições** nó. Selecione **propriedades** de um da **aprovar a aplicação através do e-mail** subscrições que está relacionado com a implementação da aplicação. 

Se existir mais do que um alerta, pode determinar qual alerta vai com qual implementação. Abra as propriedades do alerta e ver a lista de **alertas selecionados** na guia Geral. A implementação está ativada como o alerta para esta subscrição. 


### <a name="prerequisites"></a>Pré-requisitos

#### <a name="to-send-email-notifications-and-take-action-on-internal-network"></a>Enviar notificações por e-mail e agir na rede interna
Com estes pré-requisitos, os destinatários receber um e-mail com a notificação do pedido. Se estes estão na rede interna, também pode aprovar ou negar o pedido de e-mail.

- Ativar a [funcionalidade opcional](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **aprovar pedidos de aplicações para utilizadores por dispositivo**.  

- Configurar [notificação por e-mail para alertas](/sccm/core/servers/manage/use-alerts-and-the-status-system#to-configure-email-notification-for-alerts).  

- Ative o fornecedor de SMS a utilizar um certificado.<!--SCCMDocs-pr issue 3135--> Utilize uma das seguintes opções:  

    - Ativar [avançada HTTP](/sccm/core/plan-design/hierarchy/enhanced-http) (recomendado)  

        > [!Note]  
        > Quando o site cria um certificado para o fornecedor de SMS, ele não ser considerado fidedigno pelo navegador da web no cliente. Com base nas suas definições de segurança, em resposta a um pedido de aplicação, poderá ver um aviso de segurança.  

    - Manualmente vincular um certificado PKI com base para a porta 443 no IIS no servidor que aloja a função de fornecedor de SMS  


#### <a name="to-take-action-from-internet"></a>Para tomar medidas a partir da internet
Com estes pré-requisitos opcionais adicionais, os destinatários podem aprovar ou negar o pedido de qualquer lugar, eles têm acesso à internet.

- Ative o serviço de administração do fornecedor de SMS através do gateway de gestão na cloud. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **servidores e funções de sistema de sites** nó. Selecione o servidor com a função de fornecedor de SMS. No painel de detalhes, selecione o **fornecedor de SMS** função e selecione **propriedades** na faixa de opções no separador de função de Site. Selecione a opção para **permitir que o Configuration Manager tráfego de gateway de gestão na cloud para o serviço de administração**.  

    - O fornecedor de SMS precisa **.NET 4.5.2** ou posterior.  

- [Gateway de gestão na cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)  

- Carregar o site para [serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para **gestão na Cloud**  

    - Ativar [deteção de utilizador do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - Configure manualmente as definições no Azure AD:  

        1. Vá para o [portal do Azure](https://portal.azure.com), selecione **Azure Active Directory**e, em seguida, selecione **registos das aplicações**.  

        2. Selecione a aplicação do tipo **nativo** que criou para o Configuration Manager **gestão de Cloud** integração.  

        3. Nas propriedades da aplicação, selecione **configurações**, em seguida, selecione **URIs de redirecionamento**.  

            1. No painel de URIs de redirecionamento, cole o seguinte caminho: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

            2. Substitua `<CMG FQDN>` com o nome de domínio completamente qualificado (FQDN) do seu serviço de gateway (CMG) de gestão na cloud. Por exemplo, GraniteFalls.Contoso.com.  

            3. Em seguida, selecione **guardar**. Fechar o **definições** painel.  

        4. Nas propriedades da aplicação, selecione **manifesto**.  

            1. No painel de manifesto de edição, encontre o **oauth2AllowImplicitFlow** propriedade.  

            2. Altere seu valor para **true**. Por exemplo, toda a linha deve ser semelhante a seguinte linha: `"oauth2AllowImplicitFlow": true,`   

            3. Selecione **Guardar**.  


### <a name="configure-email-approval"></a>Configurar a aprovação de e-mail

1. Na consola do Configuration Manager, [implementar uma aplicação](/sccm/apps/deploy-use/deploy-applications) como disponíveis para uma coleção de utilizadores. Sobre o **definições de implementação** página, ativá-la para aprovação. Em seguida, introduza um ou mais endereços de e-mail para receber a notificação. Separe os endereços de e-mail com ponto e vírgula (`;`).  

     > [!Note]  
     > Qualquer pessoa na sua organização do Azure AD que recebe o e-mail pode aprovar o pedido. Não reencaminhe o e-mail para outras pessoas, a menos que deseja que eles para tomar medidas.  

2. Como um utilizador, solicite a aplicação no Centro de Software.  

3. Receber uma notificação de e-mail dentro de cinco minutos. O conteúdo da mensagem de e-mail é semelhante ao seguinte exemplo:  

![Notificação de e-mail de exemplo para aprovação de aplicação](media/1321550-email.png)

> [!Note]  
> O link para aprovar ou recusar destina-se a utilização de uma única vez. Por exemplo, configurar um alias de grupo para receber notificações. MB aprova o pedido. Agora, Bruce não é possível negar o pedido.  

Reveja os **NotiCtrl.log** ficheiro no servidor do site para resolução de problemas.


## <a name="maintenance"></a>Manutenção 

Gestor de configuração armazena as informações sobre o pedido de aprovação de aplicação do banco de dados do site. Para pedidos que são cancelados ou negados, o site elimina o histórico de pedidos após 30 dias. Pode configurar esse comportamento de eliminação com o **eliminar solicitar dados de aplicação desatualizados** [tarefa de manutenção do site](/sccm/core/servers/manage/maintenance-tasks). O site nunca elimina qualquer aprovados ou pendentes de pedidos de aplicações.


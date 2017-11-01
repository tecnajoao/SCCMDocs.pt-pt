---
title: Funcionalidades no Technical Preview 1604
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, a versão 1604."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: e632a3f4819cb2cbdaa4517b8dd0ae34fe868b3c
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="capabilities-in-technical-preview-1604-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1604 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis do System Center Configuration Manager, a versão 1604 da Technical Preview. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão do technical preview, reveja o tópico introdutórias, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.  

 Seguem-se novas funcionalidades que pode experimentar com esta versão.  

##  <a name="BKMK_WindowsVPP"></a>Gerir aplicações compradas na loja Windows para empresas  
 O [loja Windows para empresas](https://www.microsoft.com/en-us/business-store) é onde pode encontrar e adquirir aplicações para a sua organização, individualmente ou em volume. Ao ligar a loja ao Configuration Manager, pode gerir aplicações compradas em volume da consola do Configuration Manager, por exemplo:  

-   Pode sincronizar a lista de aplicações adquiridas com o Configuration Manager  

-   As aplicações que são sincronizadas aparecem na consola do Configuration Manager e pode implementá-las como todas as outras aplicações  

-   Pode controlar quantas licenças estão disponíveis e quantas estão a ser utilizadas na consola do Configuration Manager  

### <a name="try-it-out"></a>Experimente!  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>Cenário 1: Configurar a loja Windows para a sincronização de negócio  

1.  No Azure Active Directory, registe o Configuration Manager como uma ferramenta de gestão "Aplicação Web e/ou API Web". Isto irá dar-lhe um ID de cliente que irá precisar mais tarde.  

    1.  No **do Active Directory** o nó de [https://manage.windowsazure.com](https://manage.windowsazure.com), selecione o seu Azure Active Directory, em seguida, clique em **aplicações** > **adicionar**.  

    2.  Clique em **adicionar uma aplicação que a minha organização está a desenvolver**.  

    3.  Introduza um nome para a aplicação, selecione **aplicação Web** e/ou **Web API**, em seguida, clique na seta seguinte.  

    4.  Introduza o mesmo URL para ambos os **URL de início de sessão** e **URI de ID de aplicação**.  O URL pode ser qualquer coisa e não precisa de resolver para um endereço real. Por exemplo, pode introduzir **https://&lt;oseudomínio\>/sccm**.  

    5.  Conclua o assistente.  

2.  No Azure Active Directory, crie uma chave de cliente para a ferramenta de gestão registada.  

    1.  Realce a aplicação que acabou de criar e clique em **configurar**.  

    2.  Em **chaves**, selecione uma duração da lista e clique em **guardar**.  Isto irá criar uma nova chave de cliente.  Não saia desta página até ter com êxito integrado da loja Windows para empresas para o Configuration Manager.  

3.  Na loja Windows para empresas, configure o Configuration Manager como a ferramenta de gestão de armazenamento.  

    1.  Abra [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e início de sessão se lhe for pedido.  

    2.  Aceite os termos de utilização, se necessário.  

    3.  Em **ferramentas de gestão**, clique em **adicionar uma ferramenta de gestão**.  

    4.  No **pesquisar a ferramenta por nome**, escreva o nome da aplicação que criou anteriormente no AAD, em seguida, clique em **adicionar**.  

    5.  Clique em **ativar** junto da aplicação que acabou de importar.  

    6.  No **aplicações licenciadas offline** assistente, clique em **Sim** se pretender permitir que as aplicações licenciadas offline sejam compradas.  

4.  Compre pelo menos uma aplicação da loja Windows para empresas.  

5.  No **administração** área de trabalho da consola do Configuration Manager, expanda **serviços em nuvem**, em seguida, clique em **loja Windows para empresas**.  

6.  No **home page** separador o **criar** , clique em **adicionar da loja Windows para empresas conta**.  

7.  Adicione o ID do inquilino, o id de cliente e a chave de cliente do Azure Active Directory, em seguida, conclua o assistente.  

8.  Quando tiver terminado, verá a conta configurada no **da loja Windows para empresas contas** lista na consola do Configuration Manager.  

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>Cenário 2: Criar e implementar uma aplicação do Configuration Manager de uma loja Windows para empresas as aplicações licenciadas offline  

1.  No **biblioteca de Software** área de trabalho da consola do Configuration Manager, expanda **gestão de aplicações**, em seguida, clique em **informações de licença para aplicações da loja**.  

2.  O **compradas na loja Windows para aplicações empresariais** lista mostra uma lista de aplicações que foram sincronizadas a partir da loja. Escolha a aplicação que pretende implementar, em seguida, no **home page** separador o **criar** , clique em **Criar aplicação**.  

3.  Uma aplicação do Configuration Manager é criada que contém a loja Windows para a aplicação de negócio. Em seguida, pode implementar e monitorizar esta aplicação como faria com qualquer outra aplicação do Configuration Manager.  

##  <a name="BKMK_PFW"></a>Melhoramentos à Microsoft Passport para a gestão de trabalho  
 Agora pode implementar o Passport para Work as políticas para dispositivos Windows 10 associados a domínios geridos pelo cliente de Configuration Manager.  

##  <a name="bkmk_switchsup"></a>Opção para os clientes mudarem para um novo ponto de atualização de software  
 No 1604 Technical Preview, pode ativar a opção para clientes do Configuration Manager mudar para um novo ponto de atualização de software quando existirem problemas com o ponto de atualização de software ativo. Para esta opção, tem de ter vários pontos de atualização de software disponíveis num site primário. Ative esta opção numa coleção de dispositivos e, uma vez ativada, os clientes na coleção irão procurar outro ponto de atualização de software na análise seguinte quando o cliente não consegue ligar com êxito para o ponto de atualização de software ativo. Dependendo das suas definições de configuração WSUS, (classificações de atualização, produtos, etc.), o comutador para um novo ponto de atualização de software irá gerar tráfego de rede adicional. Por conseguinte, só deve utilizar esta opção quando for necessário.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Para ativar a opção para mudar pontos de atualização de software  

1.  Na consola do Configuration Manager, aceda a **Ativos e Compatibilidade > Descrição geral > Coleções de dispositivos**.  

2.  No separador **Início** , no grupo **Coleção** , clique em **Notificação do Cliente**e, em seguida, clique em **Mudar para o Ponto de Atualização de Software seguinte**.  

> [!NOTE]  
>  Esta opção só está disponível nos sites com vários pontos de atualização de software.  

##  <a name="bkmk_peercache"></a>Definições de cliente para gerir definições de Cache do cliente e o cliente de Cache ponto a ponto  
 A versão 1604 da Technical preview introduz duas novas definições de cliente de dispositivo, que afetam a utilização da cache do cliente. Ambos podem ser utilizadas individualmente, mas são configuradas na mesma folha de propriedades das definições de cliente e combinam para o ajudar a gerir a implementação de conteúdo para os seus clientes em localizações remotas.  

-   É primeiro **cliente de Cache ponto a ponto**, uma solução incorporada do Configuration Manager para os clientes partilhem conteúdos com outros clientes diretamente a partir da respetiva cache local. Para clientes de Cache ponto a ponto partilhar conteúdo, têm de ser membros do mesmo grupo de limites. Cache ponto a ponto não substitui a utilização de outras soluções como BracnchCache mas em vez disso, funciona lado lado a lado para lhe dar mais opções para expandir as soluções de implementação de conteúdos tradicionais, como os pontos de distribuição.  

     Depois de implementar as definições de cliente que permitem a Cache ponto a ponto numa coleção, os membros dessa coleção podem agir como uma origem de conteúdo ponto a ponto para outros clientes no seu grupo de limites.  O cliente que funciona como um elemento de conteúdo de origem irá submeter uma lista dos conteúdos disponíveis foi colocado em cache para o respetivo ponto de gestão. Em seguida, quando o cliente seguinte nesse grupo de limites pede esse conteúdo, a origem de cache ponto a ponto é fornecida como uma origem de conteúdo potencial juntamente com todos os pontos de distribuição que estão configurados para serem rápida. O cliente seleciona uma origem de conteúdo aleatória deste agrupamento combinado de origens de conteúdo. Os clientes só irão procurar o ressarcimento de conteúdo a partir de um ponto de distribuição que está configurado para ser lento quando não existem pontos de distribuição rápida ou as origens de cache ponto a ponto estão presentes no grupo de limites.  

-   A segunda definição nova permite-lhe **gerir o tamanho da cache** nos clientes. Pode definir a cache para ter um tamanho máximo em megabytes e um tamanho máximo como uma percentagem do espaço na unidade de clientes.  O cliente impõe a definição que for atingida pela primeira vez.  

Para ajudar a compreender a utilização do cliente de Cache ponto a ponto, pode ver o **origens de dados de cliente** dashboard. Na consola, aceda a **monitorização > Estado do cliente > origens de dados de cliente**. Aqui, pode selecionar um período de tempo para aplicar ao dashboard. Em seguida, no ecrã, pode selecionar o grupo de limites ou o pacote para o qual pretende ver informações. Ao visualizar informações, pode pairar o rato sobre a superfície de para ver mais detalhes sobre o conteúdo diferente ou origens de política.  

 Também pode utilizar um novo relatório, **origens de dados de cliente - resumo**, para ver um resumo das origens de dados de cliente para cada grupo de limites.   
**Requisitos para utilizar a Cache ponto a ponto:**  

-   Tem de configurar o seu site com um **conta de acesso à rede** que tenha **controlo total** para a pasta de cache em cada cliente. Por predefinição, este é **%windir%\ccmcache**  

-   Os clientes só podem transferir conteúdo utilizando a Cache ponto a ponto quando forem membros do mesmo grupo de limites.  

#### <a name="to-configure-client-peer-cache-client-settings"></a>Para configurar as definições de cliente de Cache ponto a ponto do cliente  

1.  Ambas as definições são configuradas na mesma página de definições de cliente. Na consola do Configuration Manager, vá para **administração > definições de cliente**, e, em seguida, as definições de cliente de dispositivo abra objeto que pretende utilizar. Também pode modificar o objecto de predefinições de cliente.  

2.  Na lista de definições disponíveis, selecione **as definições de Cache do cliente**.  

3.  Para gerir o tamanho da cache, defina **configurar o tamanho da cache do cliente** igual a **Sim**. Em seguida, pode configurar o tamanho máximo da cache para ambos os megabytes e como uma percentagem do espaço na unidade de clientes.  

4.  Para permitir que os clientes participar num cliente de Cache ponto a ponto, defina **cliente de ativar o Configuration Manager no SO completo para partilhar conteúdo** igual a **Sim**. Em seguida, pode configurar as portas que os clientes utilizam, incluindo se estes serão HTTP ou HTTPS.  

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as seguintes tarefas e, em seguida, utilize as informações de feedback perto da parte superior deste tópico para nos informar como correu:  

1.  Modificar as definições de cliente para especificar um tamanho de cache do cliente novo e, em seguida, confirme esta definição num cliente.  

2.  Utilize as definições de cliente para configurar a múltiplos clientes para utilizar a Cache ponto a ponto  

3.  Implemente conteúdo em clientes para que algumas ou a maioria dos clientes obtém esse conteúdo de outro cliente através da utilização de Cache ponto a ponto.  Pode confirmar a origem de conteúdo que é utilizada, visualizando o dashboard novo.  

    > [!NOTE]  
    >  Para concluir esta tarefa com o technical preview e um único ponto de distribuição, configure o ponto de distribuição para ser lento na localização de rede de todos os seus clientes. Em seguida, distribua o conteúdo para um único cliente.  Depois de que o cliente obtém o conteúdo, pode distribuir o conteúdo para clientes adicionais que devem encontrar elementos da rede locais para utilizar como origem de conteúdo antes de utilizar o ponto de distribuição que é considerado lenta da localização do cliente.  

##  <a name="bkmk_passport"></a>Suporte do Passport for Work como um KSP  
 System Center Configuration Manager permite-lhe integrar com o Microsoft Passport for Work, que é um início de sessão método alternativo que utiliza o Active Directory ou uma conta do Azure Active Directory para substituir uma palavra-passe, um smart card ou um virtual smart card.  
O Passport permite utilizar um gesto de utilizador para iniciar sessão, em vez de uma palavra-passe. Um gesto de utilizador pode ser um PIN simples, a autenticação biométrica, como o Windows Hello ou um dispositivo externo, como um leitor de impressões digitais.  

-   Pode utilizar o Configuration Manager para controlar que utilizadores gestos podem e não podem utilizar para iniciar sessão e para configurar os requisitos de complexidade PIN.  

-   Pode armazenar certificados de autenticação no Passport para o fornecedor de armazenamento de chaves de trabalho (KSP).  

Quando um utilizador cria um PIN Passport, o Windows envia uma notificação que o Configuration Manager escuta.  Isto permite tornar-se rapidamente com suporte para o Configuration Manager dos utilizadores que criaram um PIN Passport. O Configuration Manager, em seguida, também podem emitir novos certificados para esses utilizadores se Passport for utilizado como o fornecedor de armazenamento de chaves num perfil de certificado.  

##  <a name="bkmk_onpremdha"></a>Atestado de estado de funcionamento de dispositivos no local  
 Atestado de estado de funcionamento para dispositivos Windows 10 pode agora ser configurado para comunicar utilizando a infraestrutura no local.  Os administradores podem especificar se comunicação é efetuada através da nuvem ou recursos no local.  Se **no local** está selecionado para relatórios de atestado de estado de funcionamento, em seguida, pode ser especificado um URI para o serviço. Isto permite que os computadores cliente sem acesso à internet utilizar ativar e gerir dispositivos através de atestado de estado de funcionamento.  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>Ativar o atestado de estado de funcionamento de dispositivos no local  

1.  Na consola do Configuration Manager, navegue para **Administração** > **Descrição Geral** > **Definições de cliente**e, em seguida, defina **Utilizar o Serviço de Atestado de Estado de Funcionamento no Local** como **Sim**.  

2.  Especifique o **URL do Serviço de Atestado de Estado de Funcionamento no Local**e, em seguida, clique em **OK**.  

Para experimentá-lo, configure o serviço de atestado de estado de funcionamento no local utilizando as definições de agente do cliente.  

##  <a name="BKMK_Smart"></a>Definição de SmartLock para dispositivos Android  
 Uma nova definição, **permitir SmartLock e outros agentes de confiança** foi adicionado para o **Android e Samsung KNOX** item de configuração que lhe permite controlar a funcionalidade de SmartLock em dispositivos Android compatíveis. Esta capacidade de telefone, por vezes conhecida como agentes de confiança, permite desativar ou ignorar a palavra-passe de bloqueio do ecrã do dispositivo se o dispositivo estiver numa localização fidedigna, como quando está ligado a um dispositivo Bluetooth específico ou quando está próximo de uma etiqueta NFC. Pode utilizar esta definição para impedir que os utilizadores finais configurem o SmartLock.  

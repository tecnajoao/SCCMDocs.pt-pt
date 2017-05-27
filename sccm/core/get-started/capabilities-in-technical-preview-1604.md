---
title: "Capacidades na pré-visualização técnica 1604 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1604."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 26b0d8ea7b3e841c48945df55f8860394a98a29f
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1604-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1604 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1604. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.  

 Seguem-se novas funcionalidades que pode experimentar com esta versão.  

##  <a name="BKMK_WindowsVPP"></a>Gerir aplicações adquirido o volume a partir da loja Windows para empresas  
 O [da loja Windows para empresas](https://www.microsoft.com/en-us/business-store) é onde pode encontrar e adquirir aplicações para a sua organização, individualmente ou em volume. Ao ligar-se no arquivo do Configuration Manager, pode gerir as aplicações adquirido o volume a partir da consola do Configuration Manager, por exemplo:  

-   Pode sincronizar a lista de aplicações adquiridas com o Configuration Manager  

-   As aplicações que são sincronizadas são apresentados na consola do Configuration Manager e é possível implementar estas como todas as outras aplicações  

-   Pode controlar quantas licenças estão disponíveis e quantas estão a ser utilizadas na consola do Configuration Manager  

### <a name="try-it-out"></a>Experimente!  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>Cenário 1: Configurar a loja Windows para a sincronização de negócio  

1.  No Azure Active Directory, registe o Configuration Manager como uma ferramenta de gestão "Web aplicação and/or Web API". Isto irá dar-lhe um ID de cliente que irá precisar mais tarde.  

    1.  No **do Active Directory** nó do [https://manage.windowsazure.com](https://manage.windowsazure.com), selecione o seu Azure Active Directory, em seguida, clique em **aplicações** > **adicionar**.  

    2.  Clique em **adicionar uma aplicação a minha organização está a desenvolver**.  

    3.  Introduza um nome para a aplicação, selecione **aplicação Web** e/ou **Web API**, em seguida, clique na seta seguinte.  

    4.  Introduza o mesmo URL para ambos os **URL de início de sessão** e **URI de ID de aplicação**.  O URL pode ser nada e não precisa de resolver para um endereço real. Por exemplo, pode introduzir **https://&lt;oseudomínio\>/sccm**.  

    5.  Conclua o assistente.  

2.  No Azure Active Directory, crie uma chave de cliente para a ferramenta de gestão registado.  

    1.  Realce a aplicação que acabou de criar e clique em **configurar**.  

    2.  Em **chaves**, selecione uma duração a partir da lista e clique em **guardar**.  Esta ação cria uma nova chave de cliente.  Não sai desta página até ter com êxito onboarded da loja Windows para empresas para o Configuration Manager.  

3.  Na loja Windows para empresas, configure o Configuration Manager como a ferramenta de gestão de arquivo.  

    1.  Abrir [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e início de sessão se lhe for solicitado.  

    2.  Aceite os termos de utilização se necessário.  

    3.  Em **ferramentas de gestão**, clique em **adicionar uma ferramenta de gestão**.  

    4.  No **pesquisa para a ferramenta de por nome**, escreva o nome da aplicação que criou anteriormente no AAD, em seguida, clique em **adicionar**.  

    5.  Clique em **ativar** junto da aplicação que acabou de importar.  

    6.  No **Show Offline-Licensed aplicações** assistente, clique em **Sim** se pretender permitir que as aplicações offline licenciado ser comprado.  

4.  Compre pelo menos uma aplicação da loja Windows para empresas.  

5.  No **administração** área de trabalho da consola do Configuration Manager, expanda **serviços em nuvem**, em seguida, clique em **da loja Windows para empresas**.  

6.  No **base** separador o **criar** grupo, clique em **para conta de empresas da loja Windows adicionar**.  

7.  Adicionar o seu ID de inquilino, o id de cliente e a chave de cliente a partir do Azure Active Directory, em seguida, conclua o assistente.  

8.  Quando tiver terminado, verá a conta configurada no **da loja Windows para empresas** lista na consola do Configuration Manager.  

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>Cenário 2: Criar e implementar uma aplicação do Configuration Manager de uma loja Windows para a aplicação licenciada offline de negócio  

1.  No **biblioteca de Software** área de trabalho da consola do Configuration Manager, expanda **gestão de aplicações**, em seguida, clique em **informações de licença de aplicações da loja**.  

2.  O **Purchased da loja Windows para aplicações de negócio** lista apresenta uma lista de aplicações que foram sincronizados a partir da loja. Escolha a aplicação que pretende implementar, em seguida, no **base** separador o **criar** grupo, clique em **Criar aplicação**.  

3.  Uma aplicação do Configuration Manager é criada que contém a loja Windows para a aplicação de negócio. Pode, em seguida, implementar e monitorizar esta aplicação, tal como faria com qualquer outra aplicação do Configuration Manager.  

##  <a name="BKMK_PFW"></a>Melhoramentos para Microsoft Passport para gestão de trabalho  
 Agora pode implementar Passport para políticas do trabalho para dispositivos Windows 10 associados a um domínio geridos pelo cliente do Configuration Manager.  

##  <a name="bkmk_switchsup"></a>Opção para os clientes mudar para um novo ponto de atualização de software  
 No 1604 pré-visualização técnica, pode ativar a opção para clientes do Configuration Manager mudar para um novo ponto de atualização de software quando existem problemas com o ponto de atualização de software ativo. Para esta opção, tem de ter vários pontos de atualização de software disponíveis num site primário. Ative esta opção numa coleção de dispositivos e, uma vez ativada, os clientes na coleção vai ficar o aspeto para outro ponto de atualização de software na análise seguinte quando o cliente não consegue estabelecer ligação com êxito para o ponto de atualização de software ativo. Dependendo das suas definições de configuração WSUS, (classificações de atualização, produtos, etc.), a transição para um novo ponto de atualização de software irá gerar tráfego de rede adicionais. Por conseguinte, só deve utilizar esta opção quando for necessário.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Para ativar a opção para mudar pontos de atualização de software  

1.  Na consola do Configuration Manager, aceda a **Ativos e Compatibilidade > Descrição geral > Coleções de dispositivos**.  

2.  No separador **Início** , no grupo **Coleção** , clique em **Notificação do Cliente**e, em seguida, clique em **Mudar para o Ponto de Atualização de Software seguinte**.  

> [!NOTE]  
>  Esta opção só está disponível nos sites que tenham vários pontos de atualização de software.  

##  <a name="bkmk_peercache"></a>Definições de cliente para gerir definições de Cache do cliente e cliente Cache ponto a ponto  
 Versão de pré-visualização técnica 1604 introduzirá duas novas definições de cliente de dispositivo, que afetam a utilização da cache do cliente. Ambos podem ser utilizadas individualmente, mas são configuradas na mesma folha de propriedades das definições de cliente e combinar para o ajudar a gerir a implementação de conteúdo aos clientes em localizações remotas.  

-   Primeiro é **cliente cache de elementos da**, uma solução de Configuration Manager incorporados para os clientes partilhem conteúdos com outros clientes diretamente a partir da respetiva cache local. Para clientes de Cache ponto a ponto partilhar conteúdo, têm de ser membros do mesmo grupo de limites. Cache ponto a ponto não substitui a utilização de outras soluções como BracnchCache mas funciona em vez disso, lado a lado para lhe dar mais opções para expandir as soluções de implementação de conteúdos tradicional como os pontos de distribuição.  

     Depois de implementar as definições de cliente que permitem Cache ponto a ponto para uma coleção, os membros da coleção de que podem agir como uma origem de conteúdo ponto a ponto para outros clientes no respetivo grupo de limites.  O cliente que funciona como um elemento de conteúdo de origem irá submeter uma lista de conteúdo disponível foi colocado em cache para o respetivo ponto de gestão. Em seguida, quando o cliente seguinte nesse grupo de limites solicita que o conteúdo, a origem de cache ponto a ponto é fornecida como uma potencial origem de conteúdo, juntamente com todos os pontos de distribuição que estão configurados para serem rápida. O cliente seleciona uma origem de conteúdo aleatória deste conjunto combinado das fontes de conteúdo. Os clientes apenas irão procurar conteúdo num ponto de distribuição que está configurado para ser lento quando não existem pontos de distribuição rápida ou origens de cache ponto a ponto estão presentes no grupo de limites.  

-   A segundo nova definição permite-lhe **gerir o tamanho da cache** nos clientes. Pode definir a cache de ter um tamanho máximo em megabytes e um tamanho máximo como uma percentagem do espaço na unidade de clientes.  O cliente impõe a definição que seja atingida pela primeira vez.  

Para ajudar a compreender a utilização do cliente de Cache ponto a ponto, pode ver o **origens de dados de cliente** dashboard. Na consola de ir para **monitorização > Estado do cliente > origens de dados de cliente**. Aqui pode selecionar um período de tempo para aplicar ao dashboard. Em seguida, no ecrã, pode selecionar o grupo de limites ou o pacote para o qual pretende visualizar as informações. Ao visualizar informações, pode passar o rato sobre a superfície de para ver mais detalhes sobre os conteúdos diferentes ou origens de política.  

 Também pode utilizar um novo relatório, **origens de dados de cliente - resumo**, para ver um resumo das origens de dados de cliente para cada grupo de limites.   
**Requisitos para utilizar a cache de elementos da:**  

-   Tem de configurar o seu site com um **conta de acesso à rede** que tenha **controlo total** para a pasta de cache em cada cliente. Por predefinição, esta é **%windir%\ccmcache**  

-   Os clientes apenas podem transferir conteúdo utilizando a Cache de elemento da rede quando estes forem membros do mesmo grupo de limites.  

#### <a name="to-configure-client-peer-cache-client-settings"></a>Para configurar as definições de cliente de Cache do cliente ponto a ponto  

1.  Ambas as definições são configuradas na mesma página de definições de cliente. Na consola do Configuration Manager, aceda a **administração > definições de cliente**, e, em seguida, as definições de cliente de dispositivo abrir objeto que pretende utilizar. Também pode modificar o objeto de predefinições de cliente.  

2.  A partir da lista de definições disponíveis, selecione **definições de Cache do cliente**.  

3.  Para gerir o tamanho da cache, defina **configurar tamanho da cache do cliente** igual a **Sim**. Em seguida, pode configurar o tamanho máximo da cache em ambos os megabytes e como uma percentagem do espaço na unidade de clientes.  

4.  Para permitir que os clientes participar no cliente de Cache ponto a ponto, defina **cliente de ativar o Configuration Manager no SO completo para partilhar conteúdo** igual a **Sim**. Em seguida, pode configurar as portas utilizadas pelos clientes, incluindo se que vão HTTP ou HTTPS.  

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as seguintes tarefas e, em seguida, utilize as informações de comentários perto da parte superior deste tópico para nos transmitir como trabalhou:  

1.  Modificar as definições de cliente para especificar um novo tamanho de cache do cliente e, em seguida, confirme esta definição num cliente.  

2.  Utilize as definições de cliente para configurar vários clientes para utilizar Cache ponto a ponto  

3.  Implemente conteúdo em clientes para que algumas ou a maior parte dos clientes obter esse conteúdo a partir de outro cliente utilizando Cache ponto a ponto.  Pode confirmar origem de conteúdo que é utilizada pelo novo dashboard de visualização.  

    > [!NOTE]  
    >  Para concluir esta tarefa com a pré-visualização técnica e de um único ponto de distribuição, configure o ponto de distribuição para ser lento para a localização de rede de todos os seus clientes. Em seguida, distribua o conteúdo para um único cliente.  Depois de que o cliente obtém o conteúdo, pode distribuir o conteúdo a clientes adicionais que deve encontrar elementos da rede locais para utilizar como uma origem de conteúdo antes de utilizar o ponto de distribuição que é considerado lenta a partir da localização do cliente.  

##  <a name="bkmk_passport"></a>Suporte para o Passport para trabalho como um KSP  
 System Center Configuration Manager permite-lhe integrar com o Microsoft Passport para o trabalho que é um início de sessão do método alternativo que utiliza o Active Directory ou uma conta do Azure Active Directory para substituir uma palavra-passe, smart card ou virtual smart card.  
Passport permite-lhe utilizar um gesto de utilizador para início de sessão, em vez de uma palavra-passe. Um gesto de utilizador pode ser um PIN simple, autenticação biométrica, tais como Windows Hello ou um dispositivo externo como um leitor de identificação digital.  

-   Pode utilizar o Configuration Manager para controlar que utilizadores de gestos podem e não podem utilizar para iniciar sessão e para configurar os requisitos de complexidade PIN.  

-   Pode armazenar certificados de autenticação Passport para o fornecedor de armazenamento de chaves de trabalho (KSP).  

Quando um utilizador cria um PIN Passport, o Windows envia uma notificação que escuta para o Configuration Manager.  Isto permite ao Configuration Manager rapidamente formos tomando conhecimento de que os utilizadores ter criado um PIN Passport. O Configuration Manager pode, em seguida, também emitir novos certificados para esses utilizadores se Passport é utilizado como o fornecedor de armazenamento de chave num perfil de certificado.  

##  <a name="bkmk_onpremdha"></a>Atestado de estado de funcionamento do dispositivo no local  
 Atestado de estado de funcionamento para dispositivos Windows 10 agora pode ser configurado para comunicar utilizando a infraestrutura no local.  Os administradores podem especificar se comunicação é efetuada através da nuvem ou recursos no local.  Se **no local** está selecionada para relatórios de atestado de estado de funcionamento, em seguida, pode ser especificado um URI para o serviço. Isto permite que o cliente PCs sem acesso à internet utilizar ativar e gerir dispositivos através de atestado de estado de funcionamento.  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>Ativar atestado de estado de funcionamento de dispositivos no local  

1.  Na consola do Configuration Manager, navegue para **Administração** > **Descrição Geral** > **Definições de cliente**e, em seguida, defina **Utilizar o Serviço de Atestado de Estado de Funcionamento no Local** como **Sim**.  

2.  Especifique o **URL do Serviço de Atestado de Estado de Funcionamento no Local**e, em seguida, clique em **OK**.  

Para experimentá-lo, configure serviço de atestado de estado de funcionamento no local utilizando as definições de agente do cliente.  

##  <a name="BKMK_Smart"></a>Definição de SmartLock para dispositivos Android  
 Uma nova definição **permitir SmartLock e outros confiar agentes** foi adicionado à **Android e Samsung KNOX** item de configuração que lhe permite controlar a funcionalidade de SmartLock em dispositivos Android compatíveis. Esta capacidade de telefone, por vezes conhecida como agentes de confiança, permite desativar ou ignorar a palavra-passe de bloqueio do ecrã do dispositivo se o dispositivo estiver numa localização fidedigna, como quando está ligado a um dispositivo Bluetooth específico ou quando está próximo de uma etiqueta NFC. Pode utilizar esta definição para impedir que os utilizadores finais SmartLock a configurar.  


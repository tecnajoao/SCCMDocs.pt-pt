---
title: Funcionalidades no Technical Preview 1604
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, a versão 1604.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: f2b4faed757acb10d7919f76ec8835dd7b8095b9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128022"
---
# <a name="capabilities-in-technical-preview-1604-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1604 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, a versão 1604. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.  

 Seguem-se os novos recursos, que pode experimentar com esta versão.  

##  <a name="BKMK_WindowsVPP"></a> Gerir aplicações compradas em volume a partir da Windows Store para empresas  
 O [Windows Store para empresas](https://www.microsoft.com/en-us/business-store) é onde pode encontrar e adquirir aplicações para a sua organização, individualmente ou em volume. Ao ligar a loja para o Configuration Manager, pode gerir aplicações compradas em volume da consola do Configuration Manager, por exemplo:  

-   Pode sincronizar a lista de aplicações adquiridas com o Configuration Manager  

-   As aplicações que são sincronizadas aparecem na consola do Configuration Manager e pode implementá-las como todas as outras aplicações  

-   Pode controlar quantas licenças estão disponíveis e quantas estão a ser utilizadas na consola do Configuration Manager  

### <a name="try-it-out"></a>Experimente!  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>Cenário 1: Configurar a Windows Store para sincronização de negócios  

1.  No Azure Active Directory, registe-se o Configuration Manager, como uma ferramenta de gestão "Aplicação Web e/ou API Web". Isso lhe fornecerá uma ID de cliente que irá precisar mais tarde.  

    1.  Na **do Active Directory** nó do [ https://manage.windowsazure.com ](https://manage.windowsazure.com), selecione o Azure Active Directory, em seguida, clique em **aplicativos** > **adicionar**.  

    2.  Clique em **adicionar uma aplicação que a minha organização está a desenvolver**.  

    3.  Introduza um nome para a aplicação, selecione **aplicação Web** e/ou **Web API**, em seguida, clique na seta seguinte.  

    4.  Introduza o mesmo URL para ambos os **URL de início de sessão** e **URI de ID de aplicação**.  O URL pode ser qualquer coisa e não precisa de resolver para um endereço real. Por exemplo, pode introduzir **https://&lt;oseudomínio\>/sccm**.  

    5.  Conclua o assistente.  

2.  No Azure Active Directory, crie uma chave de cliente para a ferramenta de gestão registada.  

    1.  Realce a aplicação que acabou de criar e clique em **configurar**.  

    2.  Sob **chaves**, selecione uma duração a partir da lista e clique em **guardar**.  Isto irá criar uma nova chave de cliente.  Não saia desta página até ter com êxito integrado a Windows Store para empresas para o Configuration Manager.  

3.  O Store do Windows para empresas, configure o Configuration Manager como a ferramenta de gestão de armazenamento.  

    1.  Open [ https://businessstore.microsoft.com/en-us/managementtools ](https://businessstore.microsoft.com/en-us/managementtools) e início de sessão se lhe for pedido.  

    2.  Aceite os termos de utilização, se necessário.  

    3.  Sob **ferramentas de gestão**, clique em **adicionar uma ferramenta de gerenciamento**.  

    4.  Na **pesquisar a ferramenta por nome**, escreva o nome da aplicação que criou anteriormente no AAD, em seguida, clique em **Add**.  

    5.  Clique em **Activate** junto da aplicação que acabou de importar.  

    6.  Na **aplicações licenciadas** assistente, clique em **Sim** se pretender permitir que aplicações licenciadas offline ser adquirido.  

4.  Compre, pelo menos, uma aplicação a partir da Windows Store para empresas.  

5.  Na **administração** área de trabalho da consola do Configuration Manager, expanda **serviços Cloud**, em seguida, clique em **Windows Store para empresas**.  

6.  Na **home page** separador a **Create** , clique em **Add Windows Store para empresas conta**.  

7.  Adicionar o seu ID de inquilino, o id de cliente e a chave de cliente do Azure Active Directory, em seguida, conclua o assistente.  

8.  Quando tiver terminado, verá a conta que configurou no **Windows Store para empresas contas** lista na consola do Configuration Manager.  

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>Cenário 2: Criar e implementar uma aplicação do Configuration Manager a partir de um Store do Windows para empresas aplicação com licença offline  

1.  Na **biblioteca de Software** área de trabalho da consola do Configuration Manager, expanda **gestão de aplicações**, em seguida, clique em **informações de licença para aplicações de Store**.  

2.  O **adquirido Windows Store para aplicações de negócio** lista mostra uma lista de aplicações que foram sincronizadas a partir da loja. Escolha a aplicação que pretende implementar, em seguida, na **home page** separador a **Create** , clique em **Criar aplicação**.  

3.  Uma aplicação do Configuration Manager é criada que contém a Windows Store para a aplicação de negócio. Em seguida, pode implementar e monitorizar esta aplicação como faria com qualquer outra aplicação do Configuration Manager.  

##  <a name="BKMK_PFW"></a> Melhorias para o Microsoft Passport para a gestão de trabalho  
 Agora, pode implementar o Passport para políticas de trabalho para dispositivos Windows 10 associados a domínios geridos pelo cliente do Configuration Manager.  

##  <a name="bkmk_switchsup"></a> Opção para os clientes mudarem para um novo ponto de atualização de software  
 No 1604 Technical Preview, pode ativar a opção para clientes do Configuration Manager mudar para um novo ponto de atualização de software quando existirem problemas com o ponto de atualização de software ativo. Para esta opção, tem de ter vários pontos de atualização de software disponíveis num site primário. Ative esta opção numa coleção de dispositivos e, uma vez ativada, os clientes na coleção irão procurar outro ponto de atualização de software na análise seguinte quando o cliente não consegue ligar com êxito para o ponto de atualização de software ativo. Dependendo das suas definições de configuração WSUS, (classificações de atualização, produtos, etc.), a mudança para um novo ponto de atualização de software irá gerar tráfego de rede adicional. Por conseguinte, só deve utilizar esta opção quando for necessário.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Para ativar a opção para mudar pontos de atualização de software  

1.  Na consola do Configuration Manager, aceda a **Ativos e Compatibilidade > Descrição geral > Coleções de dispositivos**.  

2.  No separador **Início** , no grupo **Coleção** , clique em **Notificação do Cliente**e, em seguida, clique em **Mudar para o Ponto de Atualização de Software seguinte**.  

> [!NOTE]  
>  Esta opção só está disponível nos sites com vários pontos de atualização de software.  

##  <a name="bkmk_peercache"></a> Definições de cliente para gerir as definições de Cache do cliente e o cliente de Cache ponto a ponto  
 Versão 1604 da Technical preview introduz duas novas definições de cliente de dispositivo, que afetam a utilização da cache do cliente. Ambos podem ser utilizadas individualmente, mas são configuradas na mesma folha de propriedades das definições de cliente e combinam para ajudar a gerir a implementação de conteúdos aos seus clientes em localizações remotas.  

-   Em primeiro lugar é **cliente de Cache ponto a ponto**, uma solução incorporada do Configuration Manager para os clientes partilhem conteúdos com outros clientes diretamente a partir da respetiva cache local. Para clientes de Cache ponto a ponto partilhar conteúdo, têm de ser membros do mesmo grupo de limites. Cache ponto a ponto não substitui a utilização de outras soluções como BracnchCache, mas em vez disso, funciona lado a lado para lhe dar mais opções para expandir soluções de implementação de conteúdos tradicionais, como pontos de distribuição.  

     Depois de implementar as definições de cliente que permitem a Cache ponto a ponto para uma coleção, os membros dessa coleção podem agir como uma origem de conteúdo de ponto a ponto para outros clientes no seu grupo de limites.  O cliente que funciona como um par de conteúdo de origem irá enviar uma lista de conteúdo disponível tiver em cache para o ponto de gestão. Em seguida, quando o cliente seguinte nesse grupo de limites solicitar esse conteúdo, a origem de cache ponto a ponto é oferecida como uma origem de conteúdo potencial juntamente com todos os pontos de distribuição que estão configuradas para ser rápido. O cliente seleciona uma origem de conteúdo aleatória deste conjunto combinado de fontes de conteúdo. Os clientes só vão procurar no conteúdo de um ponto de distribuição que está configurado para ser lento quando não existem pontos de distribuição rápida ou origens de cache ponto a ponto estão presentes no grupo de limites.  

-   A segunda definição nova permite-lhe **gerir o tamanho da cache** nos clientes. Pode definir a cache para ter um tamanho máximo em megabytes e um tamanho máximo como uma percentagem do espaço de disco de clientes.  O cliente impõe a definição que for atingida primeiro.  

Para ajudar a compreender a utilização do cliente de Cache ponto a ponto, pode ver o **origens de dados do cliente** dashboard. Na consola, aceda a **monitorização > Estado do cliente > origens de dados do cliente**. Aqui, pode selecionar um período de tempo para aplicar ao dashboard. Em seguida, no ecrã, pode selecionar o grupo de limites ou o pacote para o qual pretende ver informações. Ao visualizar informações, pode passar o rato sobre a superfície para ver mais detalhes sobre o conteúdo diferente ou origens de política.  

 Também pode utilizar um novo relatório **origens de dados de cliente - resumo**, para ver um resumo das origens de dados do cliente para cada grupo de limites.   
**Requisitos para utilizar a Cache ponto a ponto:**  

-   Tem de configurar o seu site com um **Network Access Account** que tem **controlo total** para a pasta de cache em cada cliente. Por predefinição, este é **%windir%\ccmcache**  

-   Os clientes só podem transferir conteúdo utilizando a Cache ponto a ponto quando forem membros do mesmo grupo de limites.  

#### <a name="to-configure-client-peer-cache-client-settings"></a>Configurar as definições de cliente de Cache ponto a ponto do cliente  

1.  Ambas as definições são configuradas na mesma página de definições de cliente. Na consola do Configuration Manager, aceda a **administração > definições de cliente**, e, em seguida, as definições de cliente de dispositivo aberto de objeto que pretende utilizar. Também pode modificar o objeto de predefinições de cliente.  

2.  Na lista de definições disponíveis, selecione **definições de Cache do cliente**.  

3.  Para gerir o tamanho da cache, defina **configurar o tamanho da cache do cliente** igual a **Sim**. Em seguida, pode configurar o tamanho máximo da cache para ambos os megabytes e como uma percentagem do espaço de unidade de clientes.  

4.  Para permitir que os clientes a participar num cliente de Cache ponto a ponto, defina **ativar o Configuration Manager cliente em OS completo partilhem conteúdo** igual a **Sim**. Em seguida, pode configurar as portas que os clientes utilizam, incluindo se eles serão HTTP ou HTTPS.  

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as seguintes tarefas e, em seguida, utilize as informações de feedback perto da parte superior deste tópico para nos informar como correu:  

1.  Modificar definições de cliente para especificar um novo tamanho de cache do cliente e, em seguida, confirme esta definição num cliente.  

2.  Utilize definições de cliente para configurar múltiplos clientes para utilizar a Cache ponto a ponto  

3.  Implemente conteúdo em clientes para que algumas ou a maioria dos clientes obtém esse conteúdo de outro cliente ao utilizar a Cache ponto a ponto.  Pode confirmar a origem de conteúdo que é utilizada, visualizando o novo dashboard.  

    > [!NOTE]  
    >  Para concluir esta tarefa com o technical preview e um único ponto de distribuição, configure o ponto de distribuição para ser lento na localização de rede de todos os seus clientes. Em seguida, distribua o conteúdo para um único cliente.  Depois que o cliente obtém o conteúdo, pode distribuir o conteúdo por clientes adicionais que devem encontrar elementos da rede locais para utilizar como uma origem de conteúdo antes de utilizar o ponto de distribuição que é considerado lenta da localização do cliente.  

##  <a name="bkmk_passport"></a> Suporte do Passport for Work como um KSP  
 System Center Configuration Manager permite integrar com o Microsoft Passport for Work, que é um início de sessão no método alternativo que utiliza o Active Directory ou uma conta do Azure Active Directory para substituir uma palavra-passe, smart cards ou virtual smart card.  
Passport, pode utilizar um gesto de utilizador para iniciar sessão, em vez de uma palavra-passe. Um gesto de utilizador pode ser um PIN simples, a autenticação biométrica, como o Windows Hello ou um dispositivo externo, como um leitor de impressões digitais.  

-   Pode utilizar o Configuration Manager para controlar que utilizadores de gestos podem e não podem utilizar para iniciar sessão e para configurar os requisitos de complexidade PIN.  

-   Pode armazenar certificados de autenticação no Passport para o fornecedor de armazenamento de chaves de trabalho (KSP).  

Quando um utilizador cria um PIN Passport, o Windows envia uma notificação que o Configuration Manager escuta.  Isto permite ao Configuration Manager tomar rapidamente conhecimento dos utilizadores que criaram um PIN Passport. O Configuration Manager, em seguida, também podem emitir novos certificados para os usuários se Passport for utilizado como o fornecedor de armazenamento de chave num perfil de certificado.  

##  <a name="bkmk_onpremdha"></a> Atestado de estado de funcionamento do dispositivo no local  
 Atestado de estado de funcionamento para dispositivos Windows 10 agora pode ser configurado para comunicar com a infraestrutura no local.  Os administradores podem especificar se comunicação é efetuada através da nuvem ou recursos no local.  Se **locais** está selecionado para relatórios de atestado de estado de funcionamento, em seguida, um URI que pode ser especificado para o serviço. Isso permite que os computadores de cliente sem acesso à internet utilizem a ativação e a gerir dispositivos através do atestado de estado de funcionamento.  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>Ativar o atestado de estado de funcionamento para dispositivos no local  

1.  Na consola do Configuration Manager, navegue para **Administração** > **Descrição Geral** > **Definições de cliente**e, em seguida, defina **Utilizar o Serviço de Atestado de Estado de Funcionamento no Local** como **Sim**.  

2.  Especifique o **URL do Serviço de Atestado de Estado de Funcionamento no Local**e, em seguida, clique em **OK**.  

Para experimentá-lo, configure o serviço de atestado de estado de funcionamento no local com as definições de agente do cliente.  

##  <a name="BKMK_Smart"></a> Definição de SmartLock para dispositivos Android  
 Uma nova definição **permitir SmartLock e outros agentes de confiança** foi adicionada para o **Android e Samsung KNOX** item de configuração que lhe permita controlar a funcionalidade de SmartLock em dispositivos Android compatíveis. Esta capacidade de telefone, por vezes conhecida como agentes de confiança, permite desativar ou ignorar a palavra-passe de bloqueio do ecrã do dispositivo se o dispositivo estiver numa localização fidedigna, como quando está ligado a um dispositivo Bluetooth específico ou quando está próximo de uma etiqueta NFC. Pode utilizar esta definição para impedir que os utilizadores finais configurem o SmartLock.  

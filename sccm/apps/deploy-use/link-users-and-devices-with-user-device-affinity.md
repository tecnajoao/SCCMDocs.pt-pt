---
title: Associar utilizadores e dispositivos com a afinidade dispositivo / utilizador | Documentos do Microsoft
description: "Associar utilizadores e dispositivos com a afinidade dispositivo / utilizador e implementar automaticamente aplicações em todos os dispositivos associados a um utilizador."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6b1393b2a329bcd017dc961366afb09fa7a77899
ms.openlocfilehash: 4e8e677851ad9ae7d027ab685e842a8ff5e35573
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="link-users-and-devices-with-user-device-affinity-in-system-center-configuration-manager"></a>Associar utilizadores e dispositivos com a afinidade de dispositivo / utilizador no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Afinidade de dispositivo / utilizador no System Center Configuration Manager (Gestor de configuração) associa um utilizador com um ou mais dispositivos. Isto pode eliminar a necessidade de conhecer os nomes dos dispositivos de um utilizador para implementar uma aplicação para o utilizador. Em vez de ser implementada para cada dispositivo do utilizador, a aplicação é implementada para o utilizador. Em seguida, a afinidade de dispositivo do utilizador assegura automaticamente que a aplicação é instalada em todos os dispositivos que estejam associados a esse utilizador.  

 É possível definir dispositivos primários que normalmente são os dispositivos que os utilizadores utilizam diariamente base para realizarem o seu trabalho. Quando cria uma afinidade entre um utilizador e um dispositivo, obtém mais opções de implementação de aplicações. Por exemplo, se um utilizador necessitar do Microsoft Visio, pode instalá-lo no dispositivo primário do utilizador, utilizando uma implementação do Windows Installer. No entanto, num dispositivo que não seja um dispositivo primário, pode implementar Visio como uma aplicação virtual. Também pode utilizar afinidade dispositivo / utilizador para pré-implementar software num dispositivo de um utilizador quando o utilizador não tiver sessão iniciado modo a que, quando o utilizador inicia sessão, a aplicação já estará instalada e pronta a ser executado.  

 Tem de gerir as informações de afinidade de dispositivo do utilizador para computadores. O Configuration Manager gere automaticamente afinidades de dispositivo do utilizador para os dispositivos móveis que inscreve.  

## <a name="manually-set-up-user-device-affinity"></a>Configurar manualmente a afinidade dispositivo / utilizador  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **dispositivos**.  

3.  Na lista, selecione um dispositivo. Em seguida, no **base** separador o **dispositivo** grupo, selecione **editar utilizadores primários**.  

4.  No **editar utilizadores primários** caixa de diálogo, procure e, em seguida, selecione os utilizadores a adicionar como utilizadores primários para o dispositivo selecionado. Escolher **adicionar**.  

    > [!NOTE]  
    > O **utilizadores primários** lista apresenta os utilizadores que já são utilizadores primários deste dispositivo e o método que cada utilizador-dispositivo foi atribuída a relação.  

## <a name="set-up-primary-devices-for-a-user"></a>Configurar dispositivos primários para um utilizador  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **utilizadores**.  

3.  Na lista, selecione um utilizador. Em seguida, no **dispositivo** separador, escolha **editar dispositivos primários**.  

4.  No **editar dispositivos primários** caixa de diálogo, procure e, em seguida, selecione os dispositivos a adicionar como dispositivos primários para o utilizador selecionado. Escolher **adicionar**.  

    > [!NOTE]  
    > O **dispositivos primários** lista mostra dispositivos que já estão definidos como dispositivos primários para este utilizador e o método que cada utilizador-dispositivo foi atribuída a relação.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Criar automaticamente afinidades de dispositivo do utilizador (apenas PCs Windows)  
 O Configuration Manager lê os dados relativos aos inícios de sessão do utilizador o registo de eventos do Windows. Para criar automaticamente afinidades dispositivo / utilizador, tem de ativar estas duas opções na política de segurança local em computadores cliente para armazenar eventos de início de sessão no registo de eventos do Windows:  

-   **Auditar eventos de início de sessão de conta**  
-   **Auditar eventos de início de sessão**  

 Para configurar estas definições, utilize a política de grupo do Windows.  

> [!IMPORTANT]  
> Se um erro provocar o registo de eventos do Windows gerar um número elevado de entradas, poderá ser criado um novo registo de eventos. Se isto ocorrer, os eventos de início de sessão existentes poderão já não estar disponíveis para o Configuration Manager.  
>   
> Tenha cuidado ao ativar o **auditar eventos de início de sessão de conta** e **auditar eventos de início de sessão** definições no Windows XP. Por predefinição, a política de retenção é de 7 dias e é muito provável que irão preencher estes eventos no registo de eventos de segurança. Os utilizadores padrão não será possível iniciar a sessão se o registo de eventos estiver cheio. Para evitar esta situação, para o registo de eventos de segurança, defina a política **método de retenção** o valor **substituir eventos conforme necessário**. Para obter dados suficientes para a afinidade dispositivo / utilizador, também defina o tamanho de registo de eventos de segurança máxima de política para um valor razoável, por exemplo, 5-20 MB.  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>Configurar o site para criar automaticamente afinidades de dispositivo do utilizador  

1.  Na consola do Configuration Manager, escolha **administração** > **definições de cliente**.  

2.  Para modificar as predefinições de cliente, selecione **predefinições de cliente**e, em seguida, no **base** separador o **propriedades** grupo, selecione **propriedades**. Para criar definições de agente de cliente personalizadas, selecione o **definições de cliente** nó e, em seguida, no **base** no separador de **criar** grupo, selecione **definições personalizadas do dispositivo cliente criar**.  

    > [!NOTE]  
    > Se modificar as predefinições do cliente, estas serão implementadas em todos os computadores na hierarquia. Para obter mais informações sobre como configurar definições de cliente, consulte o artigo [como configurar as definições de cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

3.  Para **afinidade de dispositivo e utilizador**, defina o seguinte:  

    -   **Limiar de afinidade de dispositivo do utilizador (minutos)**. Defina o número de minutos de utilização do dispositivo antes de é criada uma afinidade de dispositivo do utilizador.  

    -   **Limiar de afinidade de dispositivo do utilizador (dias)**. Defina o número de dias durante os quais é medido o limiar de afinidade baseada na utilização.  

    -   **Configurar automaticamente a afinidade de dispositivo do utilizador a partir dos dados de utilização**. Para permitir que o site automaticamente criar utilizador afinidades de dispositivo, da lista pendente, selecione **verdadeiro**. Se selecionar **falso**, terá de aprovar todas as atribuições de afinidade de dispositivo do utilizador.  

    > [!TIP]  
    > **Exemplo:** Se definir **limiar de afinidade de dispositivo do utilizador (minutos)** para **60** minutos e definir **limiar de afinidade de dispositivo do utilizador (dias)** para**5** dias, o utilizador tem de utilizar o dispositivo durante, pelo menos, 60 minutos num período de 5 dias para criar automaticamente uma afinidade de dispositivo do utilizador.  

Depois de uma afinidade de dispositivo do utilizador automática é criada, o Configuration Manager continua a monitorizar os limiares de afinidade de dispositivo do utilizador. Se a atividade do utilizador para o dispositivo for inferior aos limites que tiver configurado, é removida a afinidade dispositivo / utilizador. Definir **limiar de afinidade de dispositivo do utilizador (dias)** para um valor de, pelo menos, **7** dias para evitar situações em que uma afinidade de dispositivo do utilizador configurada automaticamente poderá perder-se enquanto o utilizador não é tem sessão iniciado, por exemplo, durante o fim de semana.  

## <a name="import-user-device-affinities-from-a-file"></a>Importar afinidades de dispositivo do utilizador a partir de um ficheiro  
 Criar várias relações de uma só vez, pode importar um ficheiro que tenha os detalhes para vários afinidades de dispositivo / utilizador. Para este procedimento, os dispositivos em causa necessário tenham sido detetados e existam como recursos na base de dados do Configuration Manager ou o procedimento falhará.  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **utilizadores** ou **dispositivos**.  

2.  No **base** separador o **criar** grupo, selecione **importar afinidade de dispositivo do utilizador**.  

3.  No Assistente de afinidade de dispositivo do utilizador de importação, no **escolher mapeamento** página, defina estas informações:  

    -   **Nome de ficheiro**. Especifique um ficheiro de valores separados por vírgulas (CSV) que tem uma lista de utilizadores e dispositivos entre os quais pretende criar uma afinidade. Neste ficheiro, cada par utilizador-dispositivo tem de ser na sua própria linha, com valores separados por uma vírgula. Utilizar este formato: <*domínio*> &#92; <*nome de utilizador*>, <*nome NetBIOS do dispositivo*>.  

    -   **Este ficheiro tem títulos de colunas para efeitos de referência**. Se o ficheiro. csv tem uma linha de cabeçalho superior, selecione esta opção e a linha de cabeçalho será ignorada durante a importação.  

4.  Se o ficheiro que está a importar tiver mais de dois itens em cada linha, pode utilizar **coluna** e **atribuir** para especificar as colunas que representam os utilizadores e dispositivos e as colunas a ignorar durante a importação.  

5.  Escolher **seguinte**e, em seguida, conclua o Assistente de afinidade de dispositivo de utilizador de importação.  

## <a name="let-users-create-their-own-device-affinities"></a>Permitir que os utilizadores criem os seus próprios afinidades de dispositivo  
 Com os procedimentos seguintes, pode configurar um utilizador para criar sua própria afinidade de dispositivo do utilizador na aplicação do Centro de Software.  

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>Configurar o site para permitir que os pedidos de afinidade de dispositivo do utilizador criados pelo utilizador  

1.  Na consola do Configuration Manager, escolha **administração** > **definições de cliente**.  

2.  Para modificar as predefinições de cliente, selecione **predefinições de cliente**e, em seguida, no **base** separador o **propriedades** grupo, selecione **propriedades**. Para criar definições de agente de cliente personalizadas, selecione o **definições de cliente** nó e, em seguida, no **base** separador o **criar** grupo, selecione **criar definições personalizadas do cliente utilizador**.  

    > [!NOTE]  
    > Se modificar as predefinições do cliente, estas serão implementadas em todos os computadores na hierarquia. Para obter mais informações sobre como configurar definições de cliente, consulte o artigo [configurar definições de cliente](../../core/clients/deploy/configure-client-settings.md).  

3.  Selecione a definição de cliente **Afinidade de Dispositivo do Utilizador** e, em seguida, na lista pendente **Permitir ao utilizador a definição dos seus dispositivos primários** , selecione **Verdadeiro**.  

### <a name="set-up-a-user-device-affinity"></a>Configurar uma afinidade de dispositivo do utilizador  

1.  No catálogo de aplicações, selecione **meus sistemas**.  

2.  Selecione a opção **uso com regularidade este computador para trabalhar**.  

## <a name="manage-user-device-affinity-requests-from-users"></a>Gerir pedidos de afinidade de dispositivo do utilizador a partir de utilizadores  
 Se a definição de cliente **Configurar automaticamente a afinidade de dispositivo do utilizador a partir dos dados de utilização** estiver definida como **Falso**, tem de aprovar todas as atribuições de afinidade de dispositivo do utilizador.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Aprovar ou rejeitar um pedido de afinidade de dispositivo do utilizador  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , selecione a coleção de utilizadores ou dispositivos para a qual pretende gerir pedidos de afinidade.  

3.  No **base** separador o **coleção** grupo, selecione **gerir pedidos de afinidade**.  

4.  No **gerir pedidos de afinidade de dispositivo do utilizador** caixa de diálogo, selecione um pedido de afinidade e, em seguida, escolha **aprovar** ou **rejeitar**.  


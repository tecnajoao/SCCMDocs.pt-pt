---
title: "Implementar aplicações | Documentos do Microsoft"
description: "Criar um tipo de implementação ou simular a implementação de uma aplicação utilizando o System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 23b1d24e908d04b64c3bbfa518793a44e696d468
ms.openlocfilehash: 0eaa1d13e9c273a6649f50d73fb357f04464d94c
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Implementar aplicações com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Antes de poder implementar uma aplicação do System Center Configuration Manager, tem de criar pelo menos um tipo de implementação para a aplicação. Para obter mais informações sobre como criar aplicações e tipos de implementação, consulte o artigo [criar aplicações ](../../apps/deploy-use/create-applications.md).

 Também pode simular a implementação de uma aplicação. Este tipo de implementação testa a aplicabilidade da implementação de uma aplicação em computadores sem instalar ou desinstalar a aplicação. Uma implementação simulada avalia o método de deteção, requisitos e as dependências de um tipo de implementação e reporta os resultados no **implementações** nó do **monitorização** área de trabalho. Para obter mais informações, consulte o artigo [simular implementações de aplicações ](../../apps/deploy-use/simulate-application-deployments.md).

> [!IMPORTANT]
>  Pode implementar (instalar ou desinstalar) necessário aplicações, mas não pacotes ou atualizações de software. Dispositivos inscritos MDM também não suportam implementações simuladas, experiência de utilizador ou as definições de agendamento.

## <a name="deploy-an-application"></a>Implementar uma aplicação

1.  Na consola do Configuration Manager, aceda a **biblioteca de Software** > **gestão de aplicações** > **aplicações**.

2.  Na lista **Aplicações** , selecione a aplicação que pretende implementar. No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.

### <a name="specify-general-information-about-the-deployment"></a>Especifique informações gerais sobre a implementação

No **geral** página do Assistente para implementar Software, especifique as seguintes informações:

- **Software**-apresenta a aplicação a implementar. Pode clicar em **Procurar** para selecionar uma aplicação diferente.
- **Recolha**-clique em **procurar** para selecionar a coleção para implementar a aplicação.
- **Utilizar grupos de pontos de distribuição predefinidos associados a esta coleção**-Selecione esta opção se pretende armazenar o conteúdo da aplicação no grupo de pontos de distribuição de predefinido da coleção. Se não tiver associado a coleção selecionada um grupo de pontos de distribuição, esta opção a cinzento.
- **Distribuir automaticamente o conteúdo para dependências**-se esta opção estiver ativada e se algum dos tipos de implementação da aplicação contiver dependências, em seguida, o conteúdo da aplicação dependente será também enviado para pontos de distribuição.

    >[!IMPORTANT]
    > Se atualizar a aplicação dependente após a implementação da aplicação principal, os eventuais conteúdos novos da dependência não serão automaticamente distribuídos.

- **Comentários (opcional)** – Opcionalmente, introduza uma descrição desta implementação.

### <a name="specify-content-options-for-the-deployment"></a>Especificar opções de conteúdo para a implementação

No **conteúdo** página, clique em **adicionar** para adicionar o conteúdo associado esta implementação a pontos de distribuição ou grupos de pontos de distribuição. Se tiver selecionado **utilizar pontos de distribuição predefinidos associados a esta coleção** no **geral** página, em seguida, esta opção será automaticamente preenchida e só pode ser modificada por um membro da função de segurança de administrador da aplicação.

### <a name="specify-deployment-settings"></a>Especificar definições de implementação

No **definições de implementação** página do Assistente para implementar Software, especifique as seguintes informações:

- **Ação**-a partir da lista pendente, escolha se esta implementação visa **instalar** ou **desinstalar** a aplicação.

    > [!NOTE]
    >  Se uma aplicação for implementada duas vezes num dispositivo, uma vez com uma ação **Instalar** e outra com uma ação **Desinstalar**, a implementação da aplicação com a ação **Instalar** terá prioridade.

Após ter sido criada, não é possível alterar a ação de uma implementação.

- **Objetivo**-na lista pendente, escolha uma das seguintes opções:
    - **Disponível**-se a aplicação for implementada para um utilizador, o utilizador verá a aplicação publicada no Centro de Software e pode instalá-la a pedido.
    - **Obrigatório**-a aplicação é implementada automaticamente, de acordo com a agenda. Se o estado de implementação da aplicação não se encontre oculto, qualquer pessoa que utilize a aplicação pode monitorizar o estado de implementação e instalar a aplicação a partir do Centro de Software antes do prazo.

    > [!NOTE]   
    >  Quando a ação de implementação estiver definida como **Desinstalar**, o objetivo da implementação é automaticamente definido como **Necessária** , não podendo ser alterado.  

- **Implementar automaticamente de acordo com a agenda quer exista ou não um utilizador tiver sessão iniciado**-se a implementação for para um utilizador, selecione esta opção para implementar a aplicação em dispositivos primários do utilizador. Esta definição não requer que o utilizador inicie sessão antes da execução da implementação. Não selecione esta opção se o utilizador tiver de fornecer dados para concluir a instalação. Esta opção só está disponível quando a implementação tem um objetivo de **Necessária**.


- **Enviar pacotes de reativação**-se o objetivo da implementação estiver definido como **necessário** e esta opção estiver selecionada, é enviado um pacote de reativação aos computadores antes da instalação da implementação. Este pacote wakes os computadores ao atingir o prazo de instalação. Para poder utilizar esta opção, os computadores e redes terão de estar configurados para Reativação por LAN.
- **Permitir que os clientes numa ligação de Internet limitada transfiram conteúdo após o prazo de instalação, o que pode implicar custos adicionais**-esta opção só está disponível para implementações com um objetivo de **necessário**.
- **Fechar automaticamente qualquer executáveis em execução que especificou no separador de comportamento da instalação da caixa de diálogo Propriedades do tipo de implementação** - para obter mais informações sobre como configurar uma lista dos executáveis que podem impedir que uma aplicação a partir da instalação, consulte o artigo **como efetuar a verificação para executar ficheiros executáveis antes de instalar uma aplicação** mais adiante neste tópico.
- **Exigir a aprovação do administrador caso os utilizadores solicitem esta aplicação**-se esta opção estiver selecionada, o administrador terá de aprovar os pedidos de utilizador para a aplicação antes de poderem ser instaladas. Esta opção está desativada quando o objetivo de implementação for **necessário** ou quando a aplicação for implementada para uma coleção de dispositivos.

    > [!NOTE]
    >  Os pedidos de aprovação da aplicação são apresentados no nó **Pedidos de Aprovação** , sob **Gestão de Aplicações** , na área de trabalho **Biblioteca de Software** . Se um pedido não seja aprovado no prazo de 45 dias, serão removido. Além disso, a reinstalação do cliente do Configuration Manager poderá cancelar quaisquer pedidos de aprovação pendentes.
    >  Depois de aprovou uma aplicação para a instalação, pode escolher subsequentemente negar o pedido clicando **negar** na consola do Configuration Manager (anteriormente, este botão era a cinzento após a aprovação).
    >  Esta ação não fazem com que a aplicação ser desinstalada a partir de todos os dispositivos, mas deixar de utilizadores de instalar novo cópias da aplicação a partir do Centro de Software.



- **Atualizar automaticamente as versões substituídas desta aplicação**-se esta opção estiver selecionada, as eventuais versões substituídas da aplicação serão atualizadas para a aplicação substituta.

### <a name="specify-scheduling-settings-for-the-deployment"></a>Especificar definições de agendamento para a implementação

No **agendamento** página do Software implementar assistente, definir a hora de quando a aplicação será implementada ou disponibilizada aos dispositivos cliente.
As opções desta página serão diferentes consoante a ação de implementação esteja definida para **Disponível** ou **Necessária**.

Em alguns casos, poderá querer conceder aos utilizadores mais tempo a instale necessário implementações de aplicações ou atualizações de software para além de qualquer prazos que configura. Isto é normalmente é necessário quando um computador foi desativado por um determinado período de tempo e tem de instalar um grande número de atualizações ou implementações de aplicações. Por exemplo, se um utilizador apenas tiver devolvido de férias, podem ter de aguardar muito tempo, como as implementações de aplicações em atraso estão instaladas. Para ajudar a resolver este problema, agora pode definir um período de tolerância de imposição implementando definições de cliente do Configuration Manager a uma coleção.

Para configurar o período de tolerância, execute as ações seguintes:

- No **agente do computador** página de definições de cliente, configure a nova propriedade **período de tolerância para imposição após a implementação do prazo (horas)** com um valor entre **1** e **120** horas.
- No **agendamento** página uma nova implementação de aplicações necessárias, ou nas propriedades de uma implementação existente, selecione a caixa **atrasar a imposição desta implementação, de acordo com as preferências do utilizador, até o período de tolerância definido nas definições de cliente**. O período de tolerância de imposição é utilizado por todas as implementações que tenham esta caixa selecionada e têm como destino dispositivos em que também implementada a definição de cliente.

Depois de instalar a aplicação for atingido o prazo, a aplicação será instalada na primeira janela de negócio não que o utilizador configurado até esse período de tolerância. No entanto, o utilizador ainda pode abrir o Centro de Software e instalar a aplicação em qualquer altura que queiram. Depois do período de tolerância expirar, a imposição reverte para comportamento normal para implementações em atraso.

Se a aplicação que estiver a implementar substituir outra aplicação, pode definir o prazo de instalação quando os utilizadores receberão a nova aplicação. Efetue este procedimento utilizando a definição **prazo de instalação** para atualizar utilizadores com aplicação substituída.

### <a name="specify-user-experience-settings-for-the-deployment"></a>Especificar definições de experiência de utilizador para a implementação


No **experiência de utilizador** página do Assistente para implementar Software, especifique as informações sobre como os utilizadores podem interagir com a instalação da aplicação.

Ao implementar aplicações em dispositivos Windows Embedded com filtro de escrita ativado, poderá especificar a instalação da aplicação na sobreposição temporária e consolidar as alterações posteriormente, ou consolidar as alterações no prazo de instalação ou durante uma janela de manutenção. Ao consolidar alterações no prazo de instalação ou durante uma janela de manutenção, tem de reiniciar o dispositivo. As alterações sejam mantidas no dispositivo.

>[!NOTE]
    >  Ao implementar uma aplicação num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada. Para mais informações sobre como as janelas de manutenção são utilizadas ao implementar aplicações em dispositivos Windows Embedded, consulte o artigo [aplicações criar Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).
    > As opções **Instalação de Software** e **Reinício do Sistema (se for necessário para concluir a instalação)** não serão utilizadas se o objetivo da implementação estiver definido como **Disponível**. Também poderá configurar o nível de notificações apresentadas aos utilizadores quando a aplicação é instalada.

### <a name="specify-alert-options-for-the-deployment"></a>Especifique as opções de alerta para a implementação

No **alertas** página do Assistente para implementar Software, configurar como do Configuration Manager e System Center Operations Manager gerarão alertas para esta implementação. Poderá configurar limiares para alertas de relatórios e desativar os relatórios durante a implementação.

### <a name="associate-the-deployment-with-an-ios-app-configuration-policy"></a>Associar a implementação de uma política de configuração de aplicação iOS

No **políticas de configuração de aplicação** página, clique em **novo** a associar a esta implementação de uma política de configuração de aplicação iOS (se tiver criado um). Para mais informações sobre este tipo de política, consulte o artigo [configurar aplicações iOS com as políticas de configuração de aplicação](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).

### <a name="finish-up"></a>Concluir

No **resumo** página do Assistente para implementar Software, reveja as ações que serão executadas por esta implementação e, em seguida, clique em **seguinte** para concluir o assistente.

A nova implementação será apresentada na lista **Implementações** do nó **Implementações** da área de trabalho **Monitorização** . Pode editar as propriedades desta implementação ou eliminar a implementação do separador **Implementações** do painel de detalhes da aplicação.

## <a name="delete-an-application-deployment"></a>Eliminar uma implementação de aplicações

1.  Na consola do Configuration Manager, aceda a **biblioteca de Software** > **gestão de aplicações** > **aplicações**.

3.  No **aplicações** lista, selecione a aplicação que inclui a implementação irá eliminar.

4.  No separador **Implementações** da lista *<nome da aplicação\>*, selecione a implementação da aplicação a eliminar. Em seguida, no **implementação** separador o **implementação** grupo, clique em **eliminar**.

 Quando elimina uma implementação de aplicações, as instâncias da aplicação que já tenham sido instaladas não serão removidas. Para remover estas aplicações, tem de implementar a aplicação em computadores com **desinstalar**. Se eliminar uma implementação de aplicações ou remover um recurso da coleção em que esteja a implementar, a aplicação deixará de estar visível no Centro de Software.

## <a name="user-notifications-for-required-deployments"></a>Notificações de utilizador para as implementações necessárias
Quando recebe software necessárias a partir de **suspender e avisar-me** definição, é possível selecionar a seguinte na lista pendente de valores:
- **Mais tarde**-Especifica se as notificações estão agendadas baseada nas definições de notificação configuradas nas definições do agente de cliente.
- **Corrigido tempo**-Especifica que a notificação será agendada para apresentar novamente após o tempo selecionado. Por exemplo, se selecionar 30 minutos, a notificação apresentará novamente dentro de 30 minutos.

![Página de agente de computador nas definições do agente de cliente](media/ComputerAgentSettings.png)

O tempo máximo premir suspender sempre é baseado nos valores de notificação configurados nas definições de agente do cliente em cada vez ao longo da linha cronológica de implementação. Por exemplo, se o **implementação prazo superior a 24 horas, lembrar utilizadores cada (horas)** a definição de **agente do computador** página está configurada para 10 horas e é mais do que 24 horas antes do prazo quando a caixa de diálogo for iniciada, seria apresentada com um conjunto de opções de premir suspender até mas nunca maior que 10 horas. Como se aproximar do prazo, a caixa de diálogo irá mostrar menos opções, consistentes com as definições de agente do cliente relevantes para cada componente da linha de tempo de implementação.

Além disso, para uma implementação de alto risco, tal como uma sequência de tarefas que implementa um sistema operativo, a experiência de notificação do utilizador está agora mais intrusivo. Em vez de uma notificação da barra de tarefas transitório, uma caixa de diálogo como o seguinte apresenta no seu computador sempre são notificadas que manutenção crítica do software é necessária:

![Caixa de diálogo de Software necessária](media/client-toast-notification.png)

## <a name="how-to-check-for-running-executable-files-before-installing-an-application"></a>Como efetuar a verificação para executar ficheiros executáveis antes de instalar uma aplicação

>[!Tip]
>Introduzida com a versão 1702, esta é uma funcionalidade pré-lançamento. Para ativá-lo, consulte o artigo [pré-lançamento funcionalidades no System Center Configuration Manager](https://docs.microsoft.com/sccm/core/servers/manage/pre-release-features).

No **propriedades** , na caixa de diálogo de uma implementação de escrever o **instalar comportamento** separador, pode especificar um dos ficheiros executáveis mais que, se a ser executado, irão bloquear a instalação do tipo de implementação. O utilizador tem de fechar o ficheiro executável está em execução (ou pode ser fechado automaticamente para implementações com um objetivo necessário) antes da implementação tipo pode ser instalado. Para configurar esta opção:

1. Abra o **propriedades** caixa de diálogo para qualquer tipo de implementação.
2. No **instalar comportamento** separador do  *<deployment type name>*  **propriedades** caixa de diálogo, clique em **adicionar**.
3. No **adicionar ou Editar ficheiro executável** diálogo caixa, introduza o nome do ficheiro executável que, se a ser executado, irá bloquear a instalação da aplicação. Opcionalmente, também pode introduzir um nome amigável para a aplicação para o ajudar a identificá-lo na lista.
4. Clique em **OK**, em seguida, feche o  *<deployment type name>*  **propriedades** caixa de diálogo.
5. Em seguida, ao implementar uma aplicação, no **definições de implementação** página do Assistente para implementar Software, selecione **fechar automaticamente qualquer executáveis em execução que especificou no separador de comportamento da instalação da caixa de diálogo Propriedades do tipo de implementação**, em seguida, continuar a implementar a aplicação.

Depois da aplicação atinge PCs de cliente, aplica-se o seguinte comportamento:

- Se a aplicação foi implementada como **disponível**e um utilizador final tenta instalá-lo, será pedido para fechar qualquer executáveis em execução que especificou antes que podem prosseguir com a instalação.

- Se a aplicação foi implementada como **necessário**e a opção **fechar automaticamente qualquer executáveis em execução que especificou no separador de comportamento da instalação da caixa de diálogo Propriedades do tipo de implementação** é selecionada, irá ver uma caixa de diálogo que informa que executáveis especificou são fechados automaticamente quando for atingido o prazo de instalação da aplicação. Pode agendar estas caixas de diálogo no **definições de cliente** > **agente do computador**. Se não pretender que o utilizador final para ver estas mensagens, selecione **ocultar no Centro de Software e em todas as notificações** no **experiência de utilizador** separador da folha de propriedades da implementação.

- Se a aplicação foi implementada como **necessário** e a opção **fechar automaticamente qualquer executáveis em execução que especificou no separador de comportamento da instalação da caixa de diálogo Propriedades do tipo de implementação** não estiver selecionada, em seguida, a instalação da aplicação irá falhar se existir uma ou mais das aplicações especificadas estão em execução.

## <a name="for-more-information"></a>Para obter mais informações:
- [Definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Como configurar as definições de cliente](../../core/clients/deploy/configure-client-settings.md)


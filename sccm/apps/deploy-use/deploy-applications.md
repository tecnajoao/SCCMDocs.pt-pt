---
title: "Implementar aplicações | Microsoft Docs"
description: "Criar um tipo de implementação ou simular a implementação de uma aplicação utilizando o System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
caps.latest.revision: "10"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f704d1b0ec48e3a7bbea784a7c18de77b21cd0ee
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Implementar aplicações com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de poder implementar uma aplicação do System Center Configuration Manager, tem de criar pelo menos um tipo de implementação para a aplicação. Para obter mais informações sobre como criar aplicações e tipos de implementação, consulte [criar aplicações](/sccm/apps/deploy-use/create-applications).

 Também pode simular a implementação de uma aplicação. Este tipo de implementação testa a aplicabilidade da implementação de uma aplicação em computadores sem instalar ou desinstalar a aplicação. Uma implementação simulada avalia o método de deteção, requisitos e dependências para um tipo de implementação e reporta os resultados no **implementações** o nó do **monitorização** área de trabalho. Para obter mais informações, consulte [simular implementações de aplicações](/sccm/apps/deploy-use/simulate-application-deployments).

> [!IMPORTANT]
>  Pode implementar (instalar ou desinstalar) necessário aplicações, mas não pacotes ou atualizações de software. Dispositivos inscritos no MDM também não suportam implementações simuladas, experiência de utilizador ou as definições de agendamento.

## <a name="deploy-an-application"></a>Implementar uma aplicação

1.  Na consola do Configuration Manager, vá para **biblioteca de Software** > **gestão de aplicações** > **aplicações**.

2.  Na lista **Aplicações** , selecione a aplicação que pretende implementar. No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.

### <a name="specify-general-information-about-the-deployment"></a>Especificar informações gerais sobre a implementação

No **geral** página do Assistente de implementação de Software, especifique as seguintes informações:

- **Software**  
Esta ação apresenta a aplicação a implementar. Pode clicar em **Procurar** para selecionar uma aplicação diferente.
- **Recolha**  
Clique em **procurar** para selecionar a coleção para implementar a aplicação.
- **Utilizar grupos de pontos de distribuição predefinidos associados a esta coleção**  
Selecione esta opção se pretender armazenar o conteúdo da aplicação no grupo de pontos de distribuição de predefinido da coleção. Se não associou a coleção selecionada com um grupo de pontos de distribuição, esta opção está desativada.
- **Distribuir automaticamente o conteúdo para dependências**  
Se esta opção estiver ativada e algum dos tipos de implementação da aplicação contiver dependências, o conteúdo da aplicação dependente é também enviado para pontos de distribuição.

    >[!IMPORTANT]
    > Se atualizar a aplicação dependente após a implementação da aplicação principal, os eventuais conteúdos novos da dependência não serão automaticamente distribuídos.

- **Comentários (opcional)**  
Opcionalmente, introduza uma descrição para esta implementação.

### <a name="specify-content-options-for-the-deployment"></a>Especificar opções de conteúdo para a implementação

No **conteúdo** página, clique em **adicionar** para adicionar o conteúdo associado esta implementação a pontos de distribuição ou grupos de pontos de distribuição. Se tiver selecionado **utilizar pontos de distribuição predefinidos associados a esta coleção** no **geral** página, em seguida, esta opção é preenchida automaticamente e só pode ser modificada por um membro da função de segurança de administrador da aplicação.

### <a name="specify-deployment-settings"></a>Especificar definições de implementação

No **definições de implementação** página do Assistente de implementação de Software, especifique as seguintes informações:

- **Ação**  
Na lista pendente, escolha se esta implementação visa **instalar** ou **desinstalação** a aplicação.

    > [!NOTE]
    >  Se uma aplicação for implementada duas vezes num dispositivo, uma vez com uma ação **instalar** e uma vez com uma ação **desinstalação**, a implementação de aplicação com uma ação **instalar** tem prioridade.

Após ter sido criada, não é possível alterar a ação de uma implementação.

- **Objetivo**  
Na lista pendente, escolha uma das seguintes opções:
    - **Disponível**  
    Se a aplicação for implementada para um utilizador, o utilizador verá a aplicação publicada no Centro de Software e pode instalá-la a pedido.
    - **Necessário**  
    A aplicação é implementada automaticamente, de acordo com a agenda. Se o estado de implementação da aplicação não se encontre oculto, qualquer pessoa a utilizar a aplicação pode controlar o estado de implementação e instalar a aplicação a partir do Centro de Software antes do prazo.

    > [!NOTE]   
    >  Quando a ação de implementação estiver definida como **Desinstalar**, o objetivo da implementação é automaticamente definido como **Necessária** , não podendo ser alterado.  

- **Implementar automaticamente de acordo com a agenda quer exista ou não um utilizador tiver sessão iniciado**  
Se a implementação for para um utilizador, selecione esta opção para implementar a aplicação em dispositivos primários do utilizador. Esta definição não requer que o utilizador inicie sessão antes da execução da implementação. Não selecione esta opção se o utilizador tiver de fornecer dados para concluir a instalação. Esta opção só está disponível quando a implementação tem um objetivo de **Necessária**.

- **Enviar pacotes de reativação**  
Se o objetivo da implementação estiver definido como **necessário** e esta opção estiver selecionada, é enviado um pacote de reativação para computadores antes da instalação da implementação. Este pacote sair os computadores na hora de prazo de instalação. Para poder utilizar esta opção, os computadores e redes terão de estar configurados para Reativação por LAN.
- **Permitir que os clientes numa ligação à Internet limitada para transferir conteúdo após o prazo de instalação, o que pode implicar custos adicionais**  
Esta opção só está disponível para implementações com um objetivo de **necessário**.
- **Fechar automaticamente quaisquer executáveis em execução, especificado no separador de comportamento de instalação de caixa de diálogo de propriedades do tipo de implementação**  
Para obter mais informações sobre como configurar uma lista dos executáveis que podem impedir que uma aplicação a instalar, consulte **como verificar para executar ficheiros executáveis antes de instalar uma aplicação** mais adiante neste tópico.
- **Exigir aprovação do administrador caso os utilizadores solicitem esta aplicação**  
Se esta opção for selecionada, o administrador terá de aprovar os pedidos de utilizador para a aplicação antes de poderem ser instaladas. Esta opção é desativada quando o objetivo de implementação for **necessário** ou quando a aplicação for implementada para uma coleção de dispositivos.

    > [!NOTE]
    >  Os pedidos de aprovação da aplicação são apresentados no nó **Pedidos de Aprovação** , sob **Gestão de Aplicações** , na área de trabalho **Biblioteca de Software** . Se um pedido não está aprovado no prazo de 45 dias, é removido. Além disso, se reinstalar o cliente do Configuration Manager, poderá cancelar quaisquer pedidos de aprovação pendentes.
    >  Depois de aprovar uma aplicação para a instalação, pode, subsequentemente, optar por negar o pedido ao clicar em **negar** na consola do Configuration Manager (anteriormente, este botão era cinzento após a aprovação).
    >  Esta ação não irá causar a aplicação a ser desinstalados a partir de qualquer dispositivo, mas mesmo impedir que os utilizadores de instalar novas cópias da aplicação a partir do Centro de Software.

- **Atualizar automaticamente qualquer versão substituída desta aplicação**  
Se esta opção for selecionada, qualquer versão da aplicação substituída está atualizado com a aplicação substituta.

### <a name="specify-scheduling-settings-for-the-deployment"></a>Especificar definições de agendamento para a implementação

No **agendamento** página do Software implementar assistente, defina o período de quando esta aplicação é implementada ou disponível para dispositivos cliente.
As opções desta página diferentes consoante a ação de implementação esteja definida **disponível** ou **necessário**.

Em alguns casos, pode querer dar aos utilizadores mais tempo para as implementações de aplicações de instalação necessária ou atualizações de software para além de qualquer prazos que configurou. Isto é normalmente necessário quando um computador foi desativado por um longo período de tempo e tem de instalar um grande número de atualizações ou implementações de aplicações. Por exemplo, se um utilizador tiver devolvido de férias, poderá ter de aguardar durante muito tempo, como implementações de aplicações em atraso são instaladas. Para ajudar a resolver este problema, agora pode definir um período de tolerância de imposição ao implementar as definições de cliente do Configuration Manager para uma coleção.

Para configurar o período de tolerância, efetuar as seguintes ações:

- No **agente do computador** página de definições de cliente, configure a nova propriedade **período de tolerância para a imposição após a implementação do prazo (horas)** com um valor entre **1** e **120** horas.
- No **agendamento** página numa nova implementação de aplicação necessária ou nas propriedades de uma implementação existente, selecione a caixa **atrasar imposição para esta implementação, de acordo com as preferências do utilizador, até ao período de tolerância definido nas definições de cliente**. O período de tolerância de imposição é utilizado por todas as implementações que tenham esta caixa selecionada e são direcionadas para os dispositivos nos quais tiver implementado também a definição de cliente.

Depois de instalar a aplicação for atingido o prazo, a aplicação será instalada na primeira janela de empresa-empresa que o utilizador configurado até esse período de tolerância. No entanto, o utilizador pode ainda abrir o Centro de Software e instalar a aplicação em qualquer altura em que pretende. Depois do período de tolerância expirar, imposição reverte para o comportamento normal para implementações em atraso.

Se a aplicação que estiver a implementar substituir outra aplicação, pode definir o prazo de instalação quando os utilizadores recebem a nova aplicação. Fazê-lo através da definição **prazo de instalação** para atualizar utilizadores com aplicação substituída.

### <a name="specify-user-experience-settings-for-the-deployment"></a>Especificar definições de experiência de utilizador para a implementação


No **experiência de utilizador** página do Assistente de implementação de Software, especifique informações sobre a forma como os utilizadores poderão interagir com a instalação da aplicação.

Ao implementar aplicações em dispositivos Windows Embedded com filtro de escrita ativado, poderá especificar a instalação da aplicação na sobreposição temporária e consolidar as alterações posteriormente, ou consolidar as alterações no prazo de instalação ou durante uma janela de manutenção. Ao consolidar alterações no prazo de instalação ou durante uma janela de manutenção, tem de reiniciar o dispositivo. As alterações sejam mantidas no dispositivo.

>[!NOTE]
    >  Ao implementar uma aplicação num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada. Para obter mais informações sobre como janelas de manutenção ao implementar aplicações em dispositivos Windows Embedded, consulte [aplicações criar Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).
    > As opções **Instalação de Software** e **Reinício do Sistema (se for necessário para concluir a instalação)** não serão utilizadas se o objetivo da implementação estiver definido como **Disponível**. Também poderá configurar o nível de notificações apresentadas aos utilizadores quando a aplicação é instalada.

### <a name="specify-alert-options-for-the-deployment"></a>Especifique as opções de alerta para a implementação

No **alertas** página do Assistente de implementação de Software, configurar a forma como o Configuration Manager e o System Center Operations Manager geram alertas para esta implementação. Poderá configurar limiares para alertas de relatórios e desativar os relatórios durante a implementação.

### <a name="associate-the-deployment-with-an-ios-app-configuration-policy"></a>Associar a implementação de uma política de configuração de aplicação iOS

No **políticas de configuração de aplicação** página, clique em **novo** para associar esta implementação de uma política de configuração de aplicação iOS (se tiver criado uma). Para mais informações sobre este tipo de política, consulte [configurar aplicações iOS com políticas de configuração de aplicação](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).

### <a name="finish-up"></a>Concluir a cópia de segurança

No **resumo** página do Assistente de implementação de Software, reveja as ações que são executadas por esta implementação e, em seguida, clique em **seguinte** para concluir o assistente.

A nova implementação é apresentada no **implementações** lista o **implementações** nó do **monitorização** área de trabalho. Pode editar as propriedades desta implementação ou eliminar a implementação do separador **Implementações** do painel de detalhes da aplicação.

## <a name="delete-an-application-deployment"></a>Eliminar uma implementação de aplicação

1.  Na consola do Configuration Manager, vá para **biblioteca de Software** > **gestão de aplicações** > **aplicações**.
3.  No **aplicações** lista, selecione a aplicação que inclui a implementação eliminar.
4.  No separador **Implementações** da lista *<nome da aplicação\>*, selecione a implementação da aplicação a eliminar. Em seguida, no **implementação** separador o **implementação** , clique em **eliminar**.

Quando elimina uma implementação de aplicações, as instâncias da aplicação que já tenham sido instaladas não serão removidas. Para remover estas aplicações, tem de implementar a aplicação em computadores com **desinstalação**. Se eliminar uma implementação de aplicações ou remover um recurso da coleção em que esteja a implementar, a aplicação deixará de estar visível no Centro de Software.

## <a name="user-notifications-for-required-deployments"></a>Notificações de utilizador para as implementações necessárias
Quando receber o software necessário a partir de **Snooze e avisar-me depois** definição, pode selecionar a partir da seguinte na lista pendente de valores:
- **Mais tarde**  
Especifica que as notificações são agendadas baseada nas definições de notificação configuradas nas definições do agente de cliente.
- **Tempo fixo**  
Especifica que a notificação será agendada a apresentar depois do tempo selecionado. Por exemplo, se selecionar 30 minutos, a notificação é apresentada novamente dentro de 30 minutos.

![Página de agente do computador nas definições do agente de cliente](media/ComputerAgentSettings.png)

O tempo máximo de suspensão é sempre com base nos valores de notificação configurados nas definições do agente do cliente em sempre ao longo da linha cronológica de implementação. Por exemplo, se o **implementação prazo superior a 24 horas, lembrar utilizadores cada (horas)** definição o **agente do computador** página está configurada para 10 horas e que é mais de 24 horas antes do prazo quando a caixa de diálogo é iniciada, o poderia ser apresentados com um conjunto de opções de suspensão até mas nunca superior a 10 horas. Como se aproxima do prazo, a caixa de diálogo mostra menos opções, consistentes com as definições de agente do cliente relevantes para cada componente da linha cronológica de implementação.

Além disso, para uma implementação de alto risco, como uma sequência de tarefas que implementa um sistema operativo, a experiência de notificação do utilizador é agora mais intrusivo. Em vez de uma notificação da barra de tarefas transitório, uma caixa de diálogo, tal como o seguinte apresenta no seu computador sempre for notificado de que é necessária a manutenção crítica do software:

![Caixa de diálogo de Software necessária](media/client-toast-notification.png)

## <a name="how-to-check-for-running-executable-files-before-installing-an-application"></a>Como verificar para executar ficheiros executáveis antes de instalar uma aplicação

>[!Tip]
>Introduzido com a versão 1702, esta é uma funcionalidade de pré-lançamento. Para ativá-la, consulte o artigo [no System Center Configuration Manager de funcionalidades de pré-lançamento](https://docs.microsoft.com/sccm/core/servers/manage/pre-release-features).

No **propriedades** , na caixa de diálogo de uma implementação de tipo de **instalar comportamento** separador, pode especificar um ou mais ficheiros executáveis que, se executar, bloqueiam a instalação do tipo de implementação. O utilizador tem de fechar o ficheiro executável está em execução (ou pode ser fechada automaticamente para implementações com um objetivo necessário) antes da implementação tipo pode ser instalado. Para configurar este:

1. Abra o **propriedades** caixa de diálogo para qualquer tipo de implementação.
2. No **instalar comportamento** separador do  *<deployment type name>*  **propriedades** caixa de diálogo, clique em **adicionar**.
3. No **adicionar ou Editar ficheiro executável** caixa de diálogo, introduza o nome do ficheiro executável que, se executar, bloqueia a instalação da aplicação. Opcionalmente, também pode introduzir um nome amigável para a aplicação para o ajudar a identificá-la na lista.
4. Clique em **OK**, em seguida, feche o  *<deployment type name>*  **propriedades** caixa de diálogo.
5. Em seguida, quando implementa uma aplicação, no **definições de implementação** página do Assistente de implementação Software, selecione **fechar automaticamente quaisquer executáveis em execução, especificado no separador de comportamento de instalação de caixa de diálogo de propriedades do tipo de implementação**, em seguida, avance para implementar a aplicação.

Depois da aplicação atinge os computadores cliente, o seguinte comportamento aplica-se:

- Se a aplicação foi implementada como **disponível**e um utilizador final tenta instalá-lo, são-lhe pedidos para fechar a qualquer executáveis em execução, especificado antes de poderão avançar com a instalação.

- Se a aplicação foi implementada como **necessário**e a opção **fechar automaticamente quaisquer executáveis em execução, especificado no separador de comportamento de instalação de caixa de diálogo de propriedades do tipo de implementação** é selecionado, veem uma caixa de diálogo que os informa de que o executáveis que especificou são fechadas automaticamente quando é atingido o prazo de instalação da aplicação. Pode agendar estas caixas de diálogo no **as definições de cliente** > **agente do computador**. Se não pretender que o utilizador final para ver estas mensagens, selecione **ocultar no Centro de Software e em todas as notificações** no **experiência de utilizador** separador de propriedades da implementação.

- Se a aplicação foi implementada como **necessário** e a opção **fechar automaticamente quaisquer executáveis em execução, especificado no separador de comportamento de instalação de caixa de diálogo de propriedades do tipo de implementação** não estiver selecionada, em seguida, a instalação da aplicação falhe se um ou mais das aplicações especificadas estão em execução.

## <a name="for-more-information"></a>Para obter mais informações

   -  [Definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md)  
   -  [Como configurar as definições do cliente](../../core/clients/deploy/configure-client-settings.md)

---
title: Implementar aplicações
titleSuffix: Configuration Manager
description: Criar ou simular uma implementação de uma aplicação numa coleção de dispositivo ou utilizador
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8a89c9d5a0fa4ea57a7824fe16b24120347ddaac
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Implementar aplicações com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Criar ou simular uma implementação de uma aplicação numa coleção de dispositivo ou utilizador no Configuration Manager. Esta implementação dá instruções para o cliente do Configuration Manager em como e quando instalar o software. 

Antes de poder implementar uma aplicação, crie pelo menos um tipo de implementação para a aplicação. Para obter mais informações, consulte [criar aplicações](/sccm/apps/deploy-use/create-applications).

 Também pode simular a implementação de uma aplicação. Este simulação testa a aplicabilidade da implementação de uma sem instalar ou desinstalar a aplicação. Uma implementação simulada avalia o método de deteção, requisitos e dependências para um tipo de implementação e reporta os resultados no **implementações** o nó do **monitorização** área de trabalho. Para obter mais informações, consulte [simular implementações de aplicações](/sccm/apps/deploy-use/simulate-application-deployments).

> [!IMPORTANT]
>  Pode simular a implementação de aplicações necessárias, mas não pacotes ou atualizações de software.   
>  Dispositivos inscritos de MDM não suportam implementações simuladas, experiência de utilizador ou as definições de agendamento.



## <a name="deploy-an-application"></a>Implementar uma aplicação

1.  Na consola do Configuration Manager, vá para **biblioteca de Software** > **gestão de aplicações** > **aplicações**.

2.  Na lista **Aplicações** , selecione a aplicação que pretende implementar. No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.

### <a name="specify-general-information-about-the-deployment"></a>Especificar informações gerais sobre a implementação

No **geral** página do Assistente de implementação de Software, especifique as seguintes informações:

- **Software**: Este valor apresenta a aplicação a implementar. Clique em **procurar** para selecionar uma aplicação diferente.
- **Coleção**: Clique em **procurar** para selecionar a coleção para implementar a aplicação.
- **Utilizar grupos de pontos de distribuição predefinidos associados a esta coleção**: Armazene o conteúdo da aplicação no grupo de pontos de distribuição de predefinido da coleção. Se não associou a coleção selecionada com um grupo de pontos de distribuição, esta opção está desativada.
- **Distribuir automaticamente o conteúdo para dependências**: Se algum dos tipos de implementação da aplicação contiver dependências, o site também envia conteúdo da aplicação dependente para pontos de distribuição.

    >[!IMPORTANT]
    > Se atualizar a aplicação dependente depois de implementar a aplicação principal, o site não distribui automaticamente a eventuais conteúdos novos da dependência.

- **Comentários (opcional)**: Opcionalmente, introduza uma descrição para esta implementação.

### <a name="specify-content-options-for-the-deployment"></a>Especificar opções de conteúdo para a implementação

No **conteúdo** página, clique em **adicionar** para adicionar o conteúdo associado esta implementação a pontos de distribuição ou grupos de pontos de distribuição. Se selecionar **utilizar pontos de distribuição predefinidos associados a esta coleção** no **geral** página, em seguida, esta opção é preenchida automaticamente. Apenas um membro da função de segurança de administrador da aplicação pode modificá-la.

### <a name="specify-deployment-settings"></a>Especificar definições de implementação

No **definições de implementação** página do Assistente de implementação de Software, especifique as seguintes informações:

- **Ação**: Na lista pendente, escolha se esta implementação é **instalar** ou **desinstalação** a aplicação.

    > [!NOTE]
    >  Se uma aplicação for implementada duas vezes num dispositivo, uma vez com uma ação **instalar** e uma vez com uma ação **desinstalação**, a implementação de aplicação com uma ação **instalar** tem prioridade.

  Não é possível alterar a ação de uma implementação depois de a criar.

- **Objetivo**: Na lista pendente, escolha uma das seguintes opções:  
    - **Disponível**: Se a aplicação for implementada para um utilizador, o utilizador verá a aplicação publicada no Centro de Software e pode instalá-la a pedido.
    - **Necessário**: A aplicação é implementada automaticamente, de acordo com a agenda. Se o estado de implementação da aplicação não se encontre oculto, qualquer pessoa a utilizar a aplicação pode controlar o estado de implementação e instalar a aplicação a partir do Centro de Software antes do prazo.

    > [!NOTE]   
    >  Quando a ação de implementação está definida como **desinstalação**, o objetivo da implementação é automaticamente definido para **necessário**. Não é possível alterar este comportamento.  

- **Implementar automaticamente de acordo com a agenda quer exista ou não um utilizador tiver sessão iniciado**: Se a implementação for para um utilizador, selecione esta opção para implementar a aplicação em dispositivos primários do utilizador. Esta definição não requer que o utilizador inicie sessão antes da execução da implementação. Selecione esta opção se o utilizador tem de interagir com a instalação. Esta opção só está disponível quando a implementação tem um objetivo de **Necessária**.

- **Enviar pacotes de reativação**: Se o objetivo de implementação for **necessário**, é enviado um pacote de reativação para computadores antes do cliente é executada a implementação. Este pacote sair os computadores na hora de prazo de instalação. Antes de utilizar esta opção, computadores e redes tem de ser configurados para Wake On LAN.
- **Permitir que os clientes numa ligação à Internet limitada para transferir conteúdo após o prazo de instalação, o que pode implicar custos adicionais**: Esta opção só está disponível para implementações com um objetivo de **necessário**.
- **Fechar automaticamente quaisquer executáveis em execução, especificado no separador de comportamento de instalação de caixa de diálogo de propriedades do tipo de implementação**: Para obter mais informações, consulte [procurar executar ficheiros executáveis antes de instalar uma aplicação](#how-to-check-for-running-executable-files-before-installing-an-application).

- **Exigir aprovação do administrador caso os utilizadores solicitem esta aplicação**: Para versões 1710 e anteriores, o administrador aprova quaisquer pedidos de utilizador para a aplicação antes do utilizador pode instalá-lo. Esta opção é desativada quando o objetivo de implementação for **necessário**, ou quando a aplicação for implementada para uma coleção de dispositivos.  

    > [!NOTE]
    >  Os pedidos de aprovação da aplicação são apresentados no nó **Pedidos de Aprovação** , sob **Gestão de Aplicações** , na área de trabalho **Biblioteca de Software** . Se um pedido não está aprovado no prazo de 45 dias, é removido. Reinstalar o cliente poderá cancelar quaisquer pedidos de aprovação pendentes.  
    >  Depois de ter aprovada uma aplicação para a instalação, pode **negar** o pedido na consola do Configuration Manager. Esta ação não fazer com que o cliente desinstalar a aplicação a partir de qualquer dispositivo, mas mesmo impedir que os utilizadores de instalar novas cópias da aplicação a partir do Centro de Software.

- **Um administrador tem de aprovar um pedido para esta aplicação no dispositivo**: A partir de versão 1802, o administrador aprova quaisquer pedidos de utilizador para a aplicação antes do utilizador pode instalá-lo no dispositivo pedido. Se o administrador aprova o pedido, o utilizador só é possível instalar a aplicação nesse dispositivo. O utilizador tem de submeter outro pedido para instalar a aplicação noutro dispositivo. Esta opção é desativada quando o objetivo de implementação for **necessário**, ou quando a aplicação for implementada para uma coleção de dispositivos. <!--1357015-->  

    Esta é uma funcionalidade opcional. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options). Se esta funcionalidade não está ativada, verá a experiência anterior.  

    > [!Important]  
    > O cliente do Configuration Manager tem de estar na versão 1802 bem. Tem também de utilizar o novo Centro de Software.  

    > [!Note]  
    > Vista **pedidos de aprovação** em **gestão de aplicações** no **biblioteca de Software** área de trabalho da consola do Configuration Manager. Não há agora um **dispositivo** coluna na lista para cada pedido. Quando efetuar a ação a pedido, a caixa de diálogo de pedido de aplicação também inclui o nome de dispositivo a partir do qual o utilizador submetido o pedido.  
    >  Se um pedido não está aprovado no prazo de 45 dias, é removido. Reinstalar o cliente poderá cancelar quaisquer pedidos de aprovação pendentes.  
    >  Depois de ter aprovada uma aplicação para a instalação, pode **negar** o pedido na consola do Configuration Manager. Esta ação não fazer com que o cliente desinstalar a aplicação a partir de qualquer dispositivo, mas mesmo impedir que os utilizadores de instalar novas cópias da aplicação a partir do Centro de Software.

- **Atualizar automaticamente qualquer versão substituída desta aplicação**: O cliente atualiza qualquer versão de substituição da aplicação com a aplicação substituta.    

    > [!NOTE]  
    > A iniciar na versão 1802, para um **disponível** ou **necessário** instalar fim, pode ativar ou desativar esta opção. <!--1351266--> 


### <a name="specify-scheduling-settings-for-the-deployment"></a>Especificar definições de agendamento para a implementação

No **agendamento** página do Software implementar assistente, defina o período de quando esta aplicação é implementada ou disponível para dispositivos cliente.
As opções desta página diferentes consoante a ação de implementação esteja definida **disponível** ou **necessário**.

Em alguns casos, pode querer dar aos utilizadores mais tempo para as implementações de aplicações de instalação necessária ou atualizações de software para além de qualquer prazos que configurou. Este comportamento é normalmente necessário quando um computador foi desativado para muito tempo e tem de instalar várias aplicações. Por exemplo, se um utilizador tiver devolvido de férias, poderá ter de aguardar durante muito tempo, como implementações de aplicações em atraso são instaladas. Para ajudar a resolver este problema, agora pode definir um período de tolerância de imposição ao implementar as definições de cliente do Configuration Manager para uma coleção.

Para configurar o período de tolerância, efetuar as seguintes ações:

- No **agente do computador** página de definições de cliente, configure a nova propriedade **período de tolerância para a imposição após a implementação do prazo (horas)** com um valor entre **1** e **120** horas.
- No **agendamento** página de uma implementação de aplicações necessárias, escolha a **atrasar imposição para esta implementação, de acordo com as preferências do utilizador, até ao período de tolerância definido nas definições de cliente**. O período de tolerância de imposição aplica-se a todas as implementações com esta opção ativada e direcionadas para os dispositivos nos quais tiver implementado também a definição de cliente.

Após ter sido atingido o prazo de instalação da aplicação, o cliente instala a aplicação na primeira janela de empresa-empresa, que o utilizador configurado, até esse período de tolerância. No entanto, o utilizador pode ainda abrir o Centro de Software e instalar a aplicação em qualquer altura em que pretende. Depois do período de tolerância expirar, imposição reverte para o comportamento normal para implementações em atraso.

Se a aplicação que estiver a implementar substituir outra aplicação, pode definir o prazo de instalação quando os utilizadores recebem a nova aplicação. Definir o **prazo de instalação** para atualizar utilizadores com aplicação substituída.

### <a name="specify-user-experience-settings-for-the-deployment"></a>Especificar definições de experiência de utilizador para a implementação

No **experiência de utilizador** página do Assistente de implementação de Software, especifique informações sobre a forma como os utilizadores poderão interagir com a instalação da aplicação.

Ao implementar aplicações em dispositivos Windows Embedded do filtro de escrita ativado, pode especificar a instalação da aplicação no temporária sobreposição e confirmar as alterações mais tarde. Também pode especificar a consolidar as alterações no prazo de instalação ou durante uma janela de manutenção. Se consolidar alterações no prazo de instalação ou durante uma janela de manutenção, tem de reiniciar o dispositivo. As alterações sejam mantidas no dispositivo.

>[!NOTE]
    >  Quando implementa uma aplicação num dispositivo Windows Embedded, certifique-se de que é um membro de uma coleção com uma janela de manutenção. Para obter mais informações sobre janelas de manutenção e dispositivos Windows Embedded, consulte [aplicações criar Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).
    > As opções **Instalação de Software** e **Reinício do Sistema (se for necessário para concluir a instalação)** não serão utilizadas se o objetivo da implementação estiver definido como **Disponível**. Também poderá configurar o nível de notificações apresentadas aos utilizadores quando a aplicação é instalada.

### <a name="specify-alert-options-for-the-deployment"></a>Especifique as opções de alerta para a implementação

No **alertas** página do Assistente de implementação de Software, configurar a forma como o Configuration Manager e o System Center Operations Manager geram alertas para esta implementação. Poderá configurar limiares para alertas de relatórios e desativar os relatórios durante a implementação.

### <a name="associate-the-deployment-with-an-ios-app-configuration-policy"></a>Associar a implementação de uma política de configuração de aplicação iOS

No **políticas de configuração de aplicação** página, clique em **novo** para associar esta implementação de uma política de configuração de aplicação iOS (se tiver criado uma). Para mais informações sobre este tipo de política, consulte [configurar aplicações iOS com políticas de configuração de aplicação](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).

### <a name="deployment-properties"></a>Propriedades de implementação

Localizar a nova implementação no **implementações** nó do **monitorização** área de trabalho. Pode editar as propriedades desta implementação ou eliminar a implementação do separador **Implementações** do painel de detalhes da aplicação.



## <a name="delete-an-application-deployment"></a>Eliminar uma implementação de aplicação

1.  Na consola do Configuration Manager, vá para **biblioteca de Software** > **gestão de aplicações** > **aplicações**.
3.  No **aplicações** lista, selecione a aplicação que inclui a implementação eliminar.
4.  No separador **Implementações** da lista *<nome da aplicação\>*, selecione a implementação da aplicação a eliminar. Em seguida, no **implementação** separador o **implementação** , clique em **eliminar**.

Quando elimina uma implementação de aplicação, não são removidas quaisquer instâncias da aplicação que já tenham sido instaladas. Para remover estas aplicações, tem de implementar a aplicação em computadores com **desinstalação**. Se eliminar uma implementação de aplicações ou remover um recurso da coleção em que estiver a implementar, a aplicação já não é visível no Centro de Software.



## <a name="user-notifications-for-required-deployments"></a>Notificações de utilizador para as implementações necessárias
Quando receber o software necessário a partir de **Snooze e avisar-me depois** definição, pode selecionar a partir da seguinte na lista pendente de valores:
- **Mais tarde**: Especifica que as notificações são agendadas baseada nas definições de notificação configuradas nas definições do cliente.
- **Corrigido tempo**: Especifica que a notificação está agendada para apresentar depois do tempo selecionado. Por exemplo, se selecionar 30 minutos, a notificação é apresentada novamente dentro de 30 minutos.

![Agente do computador predefinidas no grupo de definições de cliente](media/ComputerAgentSettings.png)

O tempo máximo de suspensão é sempre com base nos valores de notificação configurados nas definições do cliente em sempre ao longo da linha cronológica de implementação. Por exemplo:
- Configurar o **implementação prazo superior a 24 horas, lembrar utilizadores cada (horas)** definição o **agente do computador** página para 10 horas.
- O cliente apresenta a caixa de diálogo de notificação mais de 24 horas antes do prazo de implementação.
- A caixa de diálogo mostra as opções de suspensão até mas nunca superior a 10 horas. 
- Como se aproxima o prazo de implementação, a caixa de diálogo mostra menos opções. Estas opções são consistentes com as definições de cliente relevantes para cada componente da linha cronológica de implementação.

Para uma implementação de alto risco, como uma sequência de tarefas que implementa um sistema operativo, a experiência de notificação do utilizador é mais intrusivo. Em vez de uma notificação da barra de tarefas transitório, uma caixa de diálogo, tal como o seguinte apresenta cada hora está a notificado de que é necessária a manutenção de software críticas:

![Caixa de diálogo de software necessárias notifica-o de manutenção crítica do software](media/client-toast-notification.png)



## <a name="how-to-check-for-running-executable-files-before-installing-an-application"></a>Como verificar para executar ficheiros executáveis antes de instalar uma aplicação

No **propriedades** , na caixa de diálogo de uma implementação de tipo de **instalar comportamento** separador, especifique um ou mais ficheiros executáveis. Se um destes ficheiros executáveis está em execução no cliente, bloqueia a instalação do tipo de implementação. O utilizador tem de fechar o ficheiro executável está em execução antes do cliente pode instalar o tipo de implementação. Para implementações com um propósito de obrigatório, o cliente pode fechar automaticamente o ficheiro executável está em execução.

1. Abra o **propriedades** caixa de diálogo para qualquer tipo de implementação.
2. No **instalar comportamento** separador do *<deployment type name>* **propriedades** caixa de diálogo, clique em **adicionar**.
3. No **adicionar ou Editar ficheiro executável** caixa de diálogo, introduza o nome do ficheiro executável que, se executar, bloqueia a instalação da aplicação. Opcionalmente, também pode introduzir um nome amigável para a aplicação para o ajudar a identificá-la na lista.
4. Clique em **OK**, em seguida, feche o *<deployment type name>* **propriedades** caixa de diálogo.
5. Ao implementar a aplicação no **definições de implementação** página do Assistente de implementação Software, selecione **fechar automaticamente quaisquer executáveis em execução, especificado no separador de comportamento de instalação do tipo de implementação caixa de diálogo de propriedades**.

Depois dos clientes recebem a implementação, o seguinte comportamento aplica-se:

- Se implementou a aplicação como **disponível**e um utilizador final tenta instalá-lo, o cliente pede ao utilizador para fechar os ficheiros especificados em execução executáveis antes de prosseguir a instalação.

- Se implementou a aplicação como **necessário**e especificado para **fechar automaticamente quaisquer executáveis em execução, especificado no separador de comportamento de instalação de caixa de diálogo de propriedades do tipo de implementação**, em seguida, o utilizador verá uma caixa de diálogo a informá-los de que os ficheiros executáveis especificados são fechados automaticamente quando é atingido o prazo de instalação da aplicação. Pode agendar estas caixas de diálogo no **as definições de cliente** > **agente do computador**. Se não pretender que o utilizador final para ver estas mensagens, selecione **ocultar no Centro de Software e em todas as notificações** no **experiência de utilizador** separador de propriedades da implementação.

- Se implementou a aplicação como **necessário**e não especificar a **fechar automaticamente quaisquer executáveis em execução, especificado no separador de comportamento de instalação de caixa de diálogo de propriedades do tipo de implementação**, em seguida, a instalação da aplicação falhe se um ou mais das aplicações especificadas estão a executar.



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Implementar aplicações disponíveis ao utilizador no Azure AD-dispositivos associados a um
<!-- 1322613 -->
Se implementar aplicações como disponíveis para os utilizadores, a partir de versão 1802 podem procurar e instalá-los através do Centro de Software nos dispositivos do Azure Active Directory (Azure AD).  

#### <a name="prerequisites"></a>Pré-requisitos

- Ativar HTTPS no ponto de gestão  

- Integrar o site com [do Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) para **gestão de nuvem**  

    - Configurar [deteção de utilizador do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

- Implementar uma aplicação como disponíveis para uma coleção de utilizadores do Azure AD  

- Distribuir a qualquer conteúdo da aplicação para um [ponto de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

- Ativar a definição de cliente **utilizar o novo Centro de Software** no [agente do computador](/sccm/core/clients/deploy/about-client-settings#computer-agent) grupo  

- SO de cliente tem de ser Windows 10 e associados para o Azure AD. Um como puramente na nuvem associados a um domínio, ou híbrida do Azure AD associados.  

- Para suportar clientes baseados na internet:  

    - [Gateway de gestão de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway)  

    - Ative a definição de cliente: **Ativar pedidos da política de utilizador dos clientes Internet** no [política de cliente](/sccm/core/clients/deploy/about-client-settings#client-policy) grupo  

- Para suportar clientes na intranet:  

    - Adicionar o ponto de distribuição de nuvem a um grupo de limites utilizado pelos clientes do  

    - Os clientes têm de conseguir resolver o nome de domínio completamente qualificado (FQDN) do ponto de gestão ativado para HTTPS  



## <a name="next-steps"></a>Passos seguintes

   -  [Definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md)  
   -  [Como configurar as definições do cliente](../../core/clients/deploy/configure-client-settings.md)
   -  [Manual do utilizador do Software Center](/sccm/core/understand/software-center)


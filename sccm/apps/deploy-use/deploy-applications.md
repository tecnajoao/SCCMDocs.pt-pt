---
title: Implementar aplicações
titleSuffix: Configuration Manager
description: Criar ou simular uma implementação de uma aplicação a uma coleção de dispositivo ou utilizador
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ed6174bcb3c99461b00ec5fc57d4508b9390747d
ms.sourcegitcommit: acad0674b2743193f87990fb50194c4f17823a8e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/19/2018
ms.locfileid: "39146933"
---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Implementar aplicações com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Criar ou simular uma implementação de uma aplicação a uma coleção de dispositivo ou utilizador no Configuration Manager. Esta implementação dá instruções para o cliente do Configuration Manager sobre como e quando instalar o software. 

Antes de poder implementar uma aplicação, crie pelo menos um tipo de implementação para a aplicação. Para obter mais informações, consulte [criem aplicativos](/sccm/apps/deploy-use/create-applications).

 Também pode simular a implementação de uma aplicação. Esta simulação testa a aplicabilidade de uma implementação sem instalar ou desinstalar a aplicação. Uma implementação simulada avalia o método de deteção, requisitos e dependências para um tipo de implementação e reporta os resultados no **implementações** nó da **monitorização** área de trabalho. Para obter mais informações, consulte [simular implementações de aplicações](/sccm/apps/deploy-use/simulate-application-deployments).

> [!IMPORTANT]
>  Pode simular a implementação de aplicações necessárias, mas não pacotes ou atualizações de software.   
>  Dispositivos inscritos na MDM não suportam implementações simuladas, experiência do usuário ou definições de agendamento.



## <a name="deploy-an-application"></a>Implementar uma aplicação

1.  Na consola do Configuration Manager, aceda a **biblioteca de Software** > **gestão de aplicações** > **aplicativos**.

2.  Na lista **Aplicações** , selecione a aplicação que pretende implementar. No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.

### <a name="specify-general-information-about-the-deployment"></a>Especificar informações gerais sobre a implementação

Sobre o **gerais** página do Assistente de implementação de Software, especifique as seguintes informações:

- **Software**: Este valor apresenta a aplicação a implementar. Clique em **procurar** para selecionar uma aplicação diferente.
- **Coleção**: Clique em **procurar** para selecionar a coleção para implementar a aplicação.
- **Utilizar grupos de pontos de distribuição predefinidos associados a esta coleção**: Store o conteúdo da aplicação no grupo de pontos de distribuição de predefinido da coleção. Se não tiver associado a coleção selecionada um grupo de pontos de distribuição, esta opção está a cinzento.
- **Distribuir automaticamente o conteúdo para dependências**: Se algum dos tipos de implementação da aplicação contiver dependências, o site também envia conteúdo da aplicação dependente para pontos de distribuição.

    >[!IMPORTANT]
    > Se atualizar a aplicação dependente depois de implementar a aplicação principal, o site não distribuir automaticamente eventuais conteúdos novos da dependência.

- **Comentários (opcional)**: Opcionalmente, introduza uma descrição para esta implementação.

### <a name="specify-content-options-for-the-deployment"></a>Especificar opções de conteúdo para a implementação

Sobre o **conteúdo** página, clique em **Add** para adicionar o conteúdo associado esta implementação a pontos de distribuição ou grupos de pontos de distribuição. Se selecionar **utilizar pontos de distribuição predefinidos associados a esta coleção** sobre o **geral** página, em seguida, esta opção é preenchida automaticamente. Apenas um membro da função de segurança do administrador da aplicação pode modificá-la.

### <a name="specify-deployment-settings"></a>Especificar definições de implementação

Sobre o **definições de implementação** página do Assistente de implementação de Software, especifique as seguintes informações:

- **Ação**: Na lista pendente, escolha se esta implementação é **instale** ou **desinstalação** o aplicativo.

    > [!NOTE]
    >  Se uma aplicação for implementada duas vezes para um dispositivo, uma vez com uma ação **instalar** e outra com uma ação **desinstalação**, a implementação da aplicação com uma ação **instalar**tem prioridade.

  Não é possível alterar a ação de uma implementação depois de o criar.

- **Objetivo**: Na lista pendente, escolha uma das seguintes opções:  
    - **Disponível**: Se a aplicação é implementada para um utilizador, este verá a aplicação publicada no Centro de Software e pode instalá-la a pedido.
    - **Necessário**: A aplicação é implementada automaticamente, de acordo com a agenda. Se o estado de implementação da aplicação não se encontre oculto, qualquer pessoa que usar o aplicativo pode controlar o respetivo estado de implementação e instalar a aplicação a partir do Centro de Software antes do prazo.

    > [!NOTE]   
    >  Quando a ação de implementação está definida como **desinstalação**, o objetivo da implementação é automaticamente definido como **necessário**. Não é possível alterar esse comportamento.  

- **Implementar automaticamente de acordo com a agenda quer ou não um utilizador tem sessão iniciada**: Se a implementação for para um utilizador, selecione esta opção para implementar a aplicação em dispositivos primários do utilizador. Esta definição não requer que o utilizador inicie sessão antes da execução da implementação. Não selecione esta opção se o utilizador tem de interagir com a instalação. Esta opção só está disponível quando a implementação tem um objetivo de **Necessária**.

- **Enviar pacotes de reativação**: Se o objetivo da implementação estiver **necessário**, é enviado um pacote de reativação para computadores antes do cliente é executada a implementação. Este pacote reativa os computadores quando for atingido o prazo de instalação. Antes de utilizar esta opção, os computadores e redes devem ser configurados para reativação por LAN.
- **Permitir que os clientes numa ligação de Internet limitada para transferir conteúdo após o prazo de instalação, o que pode implicar custos adicionais**: Esta opção só está disponível para implementações com um objetivo de **necessário**.
- **Fechar automaticamente quaisquer executáveis em execução que especificou no separador de comportamento de instalação da caixa de diálogo de propriedades de tipo de implementação**: Para obter mais informações, consulte [para executar ficheiros executáveis antes de instalar uma aplicação de verificação](#how-to-check-for-running-executable-files-before-installing-an-application).

- **Exigir aprovação do administrador caso os utilizadores solicitem esta aplicação**: Para versões 1710 e anteriores, o administrador aprova quaisquer pedidos de utilizador para a aplicação antes do utilizador pode instalá-lo. Esta opção é desativada quando o objetivo de implementação for **necessário**, ou quando a aplicação for implementada para uma coleção de dispositivos.  

    > [!NOTE]
    >  Os pedidos de aprovação da aplicação são apresentados no nó **Pedidos de Aprovação** , sob **Gestão de Aplicações** , na área de trabalho **Biblioteca de Software** . Se um pedido não está aprovado no prazo de 45 dias, este é removido. Reinstalar o cliente poderá cancelar quaisquer pedidos de aprovação pendentes.  
    >  Depois que tenha aprovado uma aplicação para a instalação, poderá **negar** o pedido na consola do Configuration Manager. Esta ação não fazer com que o cliente desinstalar a aplicação a partir de todos os dispositivos, mas ele impede os utilizadores instalem novas cópias da aplicação do Centro de Software.

- **Um administrador tem de aprovar um pedido para esta aplicação no dispositivo**: A partir da versão 1802, o administrador aprova quaisquer pedidos de utilizador para a aplicação antes do utilizador pode instalá-lo no dispositivo pedido. Se o administrador aprova o pedido, o utilizador só é possível instalar o aplicativo nesse dispositivo. O utilizador tem de submeter outro pedido para instalar a aplicação noutro dispositivo. Esta opção é desativada quando o objetivo de implementação for **necessário**, ou quando a aplicação for implementada para uma coleção de dispositivos. <!--1357015-->  

    Esta é uma funcionalidade opcional. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options). Se esta funcionalidade não está ativada, verá a experiência anterior.  

    > [!Important]  
    > O cliente do Configuration Manager tem de ser na versão 1802 também. Tem também de utilizar o novo Centro de Software.  

    > [!Note]  
    > Modo de exibição **pedidos de aprovação** sob **gestão de aplicações** no **biblioteca de Software** área de trabalho da consola do Configuration Manager. Existe agora uma **dispositivo** coluna na lista para cada solicitação. Quando pega a ação na solicitação, a caixa de diálogo de pedido de aplicação também inclui o nome de dispositivo a partir do qual o utilizador submeteu o pedido.  
    >  Se um pedido não está aprovado no prazo de 45 dias, este é removido. Reinstalar o cliente poderá cancelar quaisquer pedidos de aprovação pendentes.  
    >  Depois que tenha aprovado uma aplicação para a instalação, poderá **negar** o pedido na consola do Configuration Manager. Esta ação não fazer com que o cliente desinstalar a aplicação a partir de todos os dispositivos, mas ele impede os utilizadores instalem novas cópias da aplicação do Centro de Software.

- **Atualizar automaticamente todas as versões substituídas desta aplicação**: O cliente atualiza todas as versões substituídas da aplicação com a aplicação substituta.    

    > [!NOTE]  
    > A partir da versão 1802, para **disponível** instalar fim, pode ativar ou desativar esta opção. <!--1351266--> 


### <a name="specify-scheduling-settings-for-the-deployment"></a>Especificar definições de agendamento para a implementação

Sobre o **agendamento** página de implementação de Software assistente, definir a hora quando esta aplicação é implementada ou disponíveis para dispositivos cliente.
As opções desta página diferem consoante a ação de implementação esteja definida **disponível** ou **necessário**.

Em alguns casos, pode querer dar aos utilizadores mais tempo para implementações de aplicações é necessária instalação ou atualização de software para além de quaisquer prazos que configurou. Este comportamento é normalmente exigido quando um computador foi desativado por longo tempo e tem de instalar várias aplicações. Por exemplo, se um utilizador tiver devolvido de férias, poderá ter de aguardar por muito tempo que as implementações de aplicações em atraso estejam instaladas. Para ajudar a resolver este problema, agora pode definir um período de tolerância de imposição ao implementar as definições de cliente do Configuration Manager para uma coleção.

Para configurar o período de tolerância, efetue as seguintes ações:

- Sobre o **agente do computador** página de definições de cliente, configurar a nova propriedade **período de tolerância para a imposição de após a implementação do prazo (horas)** com um valor entre **1** e **120** horas.
- Sobre o **agendamento** página de uma implementação de aplicação necessária, optar por **Trasar imposição para esta implementação, de acordo com as preferências do usuário, até o período de tolerância definido nas definições de cliente**. O período de tolerância de imposição aplica-se a todas as implementações com esta opção ativada e direcionadas para dispositivos em que implementou também a definição de cliente.

Após ter sido atingido o prazo de instalação do aplicativo, o cliente instala a aplicação na primeira janela não comerciais, que o utilizador configurado, até esse período de tolerância. No entanto, o utilizador ainda pode abrir o Centro de Software e instalar a aplicação a qualquer momento que desejarem. Assim que o período de tolerância expirar, imposição reverte para o comportamento normal para implementações em atraso.

Se a aplicação que estiver a implementar substituir outra aplicação, pode definir o prazo de instalação quando os utilizadores recebem a nova aplicação. Definir o **prazo de instalação** para atualizar utilizadores com aplicação substituída.

### <a name="specify-user-experience-settings-for-the-deployment"></a>Especificar definições de experiência de utilizador para a implementação

Sobre o **experiência de utilizador** página do Assistente de implementação de Software, especifique informações sobre como os usuários podem interagir com a instalação da aplicação.

Quando implementa aplicações em dispositivos Windows Embedded do filtro de escrita ativado, pode especificar a instalação da aplicação no temporária sobreposição e confirmar as alterações mais tarde. Também pode especificar para confirmar as alterações no prazo de instalação ou durante uma janela de manutenção. Se consolidar alterações no prazo de instalação ou durante uma janela de manutenção, tem de reiniciar o dispositivo. As alterações sejam mantidas no dispositivo.

>[!NOTE]
    >  Quando implementa uma aplicação num dispositivo Windows Embedded, certifique-se de que é um membro de uma coleção com uma janela de manutenção. Para obter mais informações sobre janelas de manutenção e dispositivos Windows Embedded, consulte [aplicações criar Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).
    > As opções **Instalação de Software** e **Reinício do Sistema (se for necessário para concluir a instalação)** não serão utilizadas se o objetivo da implementação estiver definido como **Disponível**. Também poderá configurar o nível de notificações apresentadas aos utilizadores quando a aplicação é instalada.

### <a name="specify-alert-options-for-the-deployment"></a>Especifique as opções de alerta para a implementação

Sobre o **alertas** página do Assistente de implementação de Software, configurar como o Configuration Manager e o System Center Operations Manager geram alertas para esta implementação. Poderá configurar limiares para alertas de relatórios e desativar os relatórios durante a implementação.

### <a name="associate-the-deployment-with-an-ios-app-configuration-policy"></a>Associar a implementação de uma política de configuração de aplicações iOS

Sobre o **políticas de configuração de aplicação** página, clique em **New** para associar esta implementação de uma política de configuração de aplicações iOS (se tiver criado uma). Para obter mais informações sobre este tipo de política, consulte [configurar aplicações iOS com políticas de configuração de aplicação](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).

### <a name="deployment-properties"></a>Propriedades de implementação

Encontrar a implementação de novo no **implementações** nó da **monitorização** área de trabalho. Pode editar as propriedades desta implementação ou eliminar a implementação do separador **Implementações** do painel de detalhes da aplicação.



## <a name="delete-an-application-deployment"></a>Eliminar uma implementação de aplicações

1.  Na consola do Configuration Manager, aceda a **biblioteca de Software** > **gestão de aplicações** > **aplicativos**.
3.  Na **aplicativos** , selecione a aplicação que inclui a implementação eliminar.
4.  No separador **Implementações** da lista *<nome da aplicação\>*, selecione a implementação da aplicação a eliminar. Em seguida, na **implantação** separador a **implantação** , clique em **eliminar**.

Quando elimina uma implementação de aplicações, as instâncias da aplicação que já tenham sido instaladas não são removidas. Para remover estas aplicações, tem de implementar a aplicação em computadores com **desinstalação**. Se eliminar uma implementação de aplicações ou remover um recurso da coleção que está a implementar, a aplicação já não é visível no Centro de Software.



## <a name="user-notifications-for-required-deployments"></a>Notificações do utilizador para as implementações necessárias
Quando receber o software obrigatório a partir da **suspender e lembrar-me** definir, pode selecionar na lista pendente seguinte de valores:
- **Mais tarde**: Especifica que as notificações estão agendadas com base nas definições de notificação configuradas nas definições do cliente.
- **Corrigido tempo**: Especifica que a notificação é agendada para apresentar novamente após o tempo selecionado. Por exemplo, se selecionar a 30 minutos, a notificação é apresentada novamente dentro de 30 minutos.

![Agente do computador de grupo em default definições do cliente](media/ComputerAgentSettings.png)

O tempo máximo suspender baseia-se sempre nos valores de notificação configurados nas definições de cliente em cada tempo ao longo da linha do tempo de implementação. Por exemplo:
- Configurar o **implementação prazo superior a 24 horas, lembrar os usuários a cada (horas)** definir o **agente do computador** página durante 10 horas.
- O cliente apresenta a caixa de diálogo de notificação mais de 24 horas antes do prazo de implementação.
- A caixa de diálogo mostra as opções de suspender até mas nunca maiores do que 10 horas. 
- À medida que aproxima o prazo de implementação, a caixa de diálogo mostra menos opções. Estas opções são consistentes com as definições de cliente relevantes para cada componente da linha da tempo de implementação.

Para uma implementação de alto risco, como uma sequência de tarefas que implementa um sistema operativo, a experiência de notificação do usuário é mais intrusiva. Em vez de uma notificação da barra de tarefas transitório, uma caixa de diálogo como a seguir sempre que receberá uma notificação que é preciso realizar manutenção crítica do software:

![Caixa de diálogo de software necessárias notifica-o de manutenção crítica do software](media/client-toast-notification.png)



## <a name="how-to-check-for-running-executable-files-before-installing-an-application"></a>Como verificar para executar ficheiros executáveis antes de instalar uma aplicação

Na **propriedades** , na caixa de diálogo de uma implementação escreva a **instalar comportamento** separador, especifique um ou mais ficheiros executáveis. Se um desses arquivos executáveis está em execução no cliente, bloqueia a instalação do tipo de implementação. O utilizador tem de fechar o ficheiro executável está em execução antes do cliente pode instalar o tipo de implementação. Para implementações com um objetivo necessário, o cliente pode fechar automaticamente o ficheiro executável está em execução.

1. Abra o **propriedades** caixa de diálogo para qualquer tipo de implementação.
2. Na **comportamento de instalação** separador da *<deployment type name>* **propriedades** caixa de diálogo, clique em **adicionar**.
3. Na **adicionar ou Editar ficheiro executável** caixa de diálogo, introduza o nome do ficheiro executável que, se executar, bloqueia a instalação da aplicação. Opcionalmente, também pode introduzir um nome amigável para a aplicação para o ajudar a identificá-lo na lista.
4. Clique em **OK**, em seguida, feche a *<deployment type name>* **propriedades** caixa de diálogo.
5. Ao implementar a aplicação, no **definições de implementação** página do Assistente de implementação Software, selecione **fechar automaticamente quaisquer executáveis em execução que especificou no separador de comportamento de instalação, o tipo de implementação caixa de diálogo de propriedades**.

Depois dos clientes recebem a implementação, o seguinte comportamento aplica-se:

- Se implementou a aplicação como **disponível**e um utilizador final tentar instalá-lo, o cliente solicita ao usuário para fechar os ficheiros executáveis em execução especificados antes de continuar com a instalação.

- Se implementou a aplicação como **necessários**e especificado para **fechar automaticamente quaisquer executáveis em execução que especificou no separador de comportamento de instalação da caixa de diálogo de propriedades de tipo de implementação**, em seguida, o utilizador verá uma caixa de diálogo a informar de que os ficheiros executáveis especificados automaticamente estão fechados quando é atingido o prazo de instalação do aplicativo. Pode agendar essas caixas de diálogo **definições de cliente** > **agente do computador**. Se não pretender que o utilizador final para ver estas mensagens, selecione **ocultar no Centro de Software e em todas as notificações** sobre o **experiência do usuário** separador de propriedades da implementação.

- Se implementou a aplicação como **necessários**e não tiver especificado ao **fechar automaticamente quaisquer executáveis em execução que especificou no separador de comportamento de instalação da caixa de diálogo de propriedades de tipo de implementação**, em seguida, a instalação da aplicação falha se uma ou mais das aplicações especificadas estão em execução.



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Implementar aplicações disponíveis para o utilizador em dispositivos associados ao AD do Azure
<!-- 1322613 --> Se implementar aplicações como disponíveis para os utilizadores, a partir da versão 1802 podem procurar e instalá-los através do Centro de Software em dispositivos do Azure Active Directory (Azure AD).  

#### <a name="prerequisites"></a>Pré-requisitos

- Ativar o HTTPS no ponto de gestão  

- Integrar o site com [do Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) para **gestão na Cloud**  

    - Configurar [deteção de utilizador do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

- Implementar uma aplicação como disponível para uma coleção de utilizadores do Azure AD  

- Distribuir qualquer conteúdo da aplicação para um [ponto de distribuição da nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

- Ativar a definição de cliente **utilizar o novo Centro de Software** no [agente do computador](/sccm/core/clients/deploy/about-client-settings#computer-agent) grupo  

- O sistema operacional de cliente tem de ser Windows 10 e associados ao Azure AD. Seja como puramente cloud associados a um domínio ou híbrido do Azure AD associado.  

- Para suportar clientes baseados na internet:  

    - [Gateway de gestão na cloud](/sccm/core/clients/manage/plan-cloud-management-gateway)  

    - Ative a definição de cliente: **Ativar pedidos da política de utilizador dos clientes Internet** no [política de cliente](/sccm/core/clients/deploy/about-client-settings#client-policy) grupo  

- Para suportar clientes na intranet:  

    - Adicionar o ponto de distribuição de nuvem a um grupo de limites usado pelos clientes  

    - Os clientes devem ser capazes de resolver o nome de domínio completamente qualificado (FQDN) do ponto de gestão ativado para HTTPS  



## <a name="next-steps"></a>Passos seguintes

   -  [Definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md)  
   -  [Como configurar as definições do cliente](../../core/clients/deploy/configure-client-settings.md)
   -  [Manual do utilizador do Software Center](/sccm/core/understand/software-center)


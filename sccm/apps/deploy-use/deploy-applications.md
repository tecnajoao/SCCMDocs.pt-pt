---
title: Implementar aplicações
titleSuffix: Configuration Manager
description: Criar ou simular uma implementação de uma aplicação a uma coleção de dispositivo ou utilizador
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e18832b7d8829d531f0e40c4d532141216d61c1
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122309"
---
# <a name="deploy-applications-with-configuration-manager"></a>Implementar aplicações com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Criar ou simular uma implementação de uma aplicação a uma coleção de dispositivo ou utilizador no Configuration Manager. Esta implementação dá instruções para o cliente do Configuration Manager sobre como e quando instalar o software. 

Antes de poder implementar uma aplicação, crie pelo menos um tipo de implementação para a aplicação. Para obter mais informações, consulte [criem aplicativos](/sccm/apps/deploy-use/create-applications).

Também pode simular a implementação de uma aplicação. Esta simulação testa a aplicabilidade de uma implementação sem instalar ou desinstalar a aplicação. Uma implementação simulada avalia o método de deteção, requisitos e dependências para um tipo de implementação e reporta os resultados no **implementações** nó da **monitorização** área de trabalho. Para obter mais informações, consulte [simular implementações de aplicações](/sccm/apps/deploy-use/simulate-application-deployments).

> [!Note]
>  Apenas pode simular a implementação de aplicações necessárias, mas não pacotes ou atualizações de software.   
> 
>  Dispositivos inscritos na MDM não suportam implementações simuladas, experiência do usuário ou definições de agendamento.



## <a name="bkmk_deploy"></a> Implementar uma aplicação

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**e selecione o **aplicativos** nó.  

2.  Na **aplicativos** , selecione uma aplicação a implementar. No Friso, clique em **Deploy**.  

> [!Note]  
> Ao visualizar as propriedades de uma implementação existente, as secções seguintes correspondem às guias da janela de propriedades de implementação:  
> - [Geral](#bkmk_deploy-general)
> - [Content](#bkmk_deploy-content)
> - [Definições de implementação](#bkmk_deploy-settings)
> - [Agendamento](#bkmk_deploy-sched)
> - [Experiência de utilizador](#bkmk_deploy-ux)
> - [Alertas](#bkmk_deploy-alerts)
> - [iOS: Políticas de configuração de aplicação](#bkmk_deploy-ios)


### <a name="bkmk_deploy-general"></a> Implantação **gerais** informações 

Sobre o **gerais** página do Assistente de implementação de Software, especifique as seguintes informações:  

- **Software**: Este valor apresenta a aplicação a implementar. Clique em **procurar** para selecionar uma aplicação diferente.  

- **Coleção**: Clique em **procurar** para selecionar a coleção para implementar a aplicação.  

- **Utilizar grupos de pontos de distribuição predefinidos associados a esta coleção**: Store o conteúdo da aplicação no grupo de pontos de distribuição de predefinido da coleção. Se ainda não associado a coleção selecionada um grupo de pontos de distribuição, esta opção está a cinzento.  

- **Distribuir automaticamente o conteúdo para dependências**: Se qualquer um dos tipos de implementação da aplicação tem dependências, o site também envia conteúdo da aplicação dependente para pontos de distribuição.  

    >[!Note]  
    > Se atualizar a aplicação dependente depois de implementar a aplicação principal, o site não distribuir automaticamente eventuais conteúdos novos da dependência.  

- **Comentários (opcional)**: Opcionalmente, introduza uma descrição para esta implementação.  


### <a name="bkmk_deploy-content"></a> Implantação **conteúdo** opções

Sobre o **conteúdo** página, clique em **Add** para distribuir o conteúdo para esta aplicação para um ponto de distribuição ou um grupo de pontos de distribuição. 

Se tiver selecionado a opção para **utilizar pontos de distribuição predefinidos associados a esta coleção** na página geral, em seguida, esta opção é preenchida automaticamente. Apenas um membro do **administrador da aplicação** função de segurança pode modificá-la.

Se o conteúdo da aplicação já tenham sido distribuído, em seguida, são apresentadas aqui. 


### <a name="bkmk_deploy-settings"></a> **Definições de implementação**

Sobre o **definições de implementação** , especifique as seguintes informações:  

- **Ação**: Na lista pendente, escolha se esta implementação é **instale** ou **desinstalação** o aplicativo.  

    > [!NOTE]  
    >  Se criar uma implementação para **instale** uma aplicação e outra implementação para **desinstalação** a mesma aplicação no mesmo dispositivo, o **instalar** implementação tem prioridade.  

    Não é possível alterar a ação de uma implementação depois de o criar.  

- **Objetivo**: Na lista pendente, escolha uma das seguintes opções:  

  - **Disponível**: O utilizador verá a aplicação no Centro de Software. Eles podem instalá-lo a pedido.  

  - **Necessário**: O cliente instala automaticamente a aplicação, de acordo com a agenda que definir. Se o aplicativo não estiver oculto, um utilizador pode controlar o respetivo estado de implementação. Eles também podem utilizar o Centro de Software para instalar a aplicação antes do prazo.  

    > [!NOTE]   
    >  Quando define a ação de implementação para **desinstalação**, o objetivo da implementação é automaticamente definido como **necessário**. Não é possível alterar esse comportamento.  

- **Permitir aos usuários finais tentam reparar esta aplicação**: A partir da versão 1810, se criou a aplicação com uma linha de comando de reparo, ative esta opção. Os utilizadores veem uma opção no Centro de Software para **reparação** o aplicativo.<!--1357866-->  

- **Pré-implementar software no dispositivo primário do utilizador**: Se a implementação for para um utilizador, selecione esta opção para implementar a aplicação no dispositivo primário do utilizador. Esta definição não exige que o utilizador que iniciem sessão antes da execução da implementação. Se o utilizador tem de interagir com a instalação, não selecione esta opção. Esta opção só está disponível quando a implementação estiver **necessário**.  

- **Enviar pacotes de reativação**: Se a implementação for **necessário**, Configuration Manager envia um pacote de reativação para computadores antes do cliente é executada a implementação. Este pacote reativa os computadores quando for atingido o prazo de instalação. Antes de utilizar esta opção, os computadores e redes devem ser configurados para reativação por LAN. Para obter mais informações, consulte [planear como reativar clientes](/sccm/core/clients/deploy/plan/plan-wake-up-clients).  

- **Permitir que os clientes numa ligação de Internet limitada para transferir conteúdo após o prazo de instalação, o que pode implicar custos adicionais**: Esta opção só está disponível para implementações com um objetivo de **necessário**.  

- **Atualizar automaticamente todas as versões substituídas desta aplicação**: O cliente atualiza todas as versões substituídas da aplicação com a aplicação substituta. 

    > [!Note]  
    > Esta opção funciona independentemente de aprovação de administrador. Se um administrador já aprovado a versão de substituição, não precisam de se aprovar também a versão de substituição. Aprovação é apenas para novos pedidos, não substituir as atualizações.<!--515824-->  

    > [!NOTE]  
    > A partir da versão 1802, para **disponível** instalar fim, pode ativar ou desativar esta opção. <!--1351266--> 


#### <a name="bkmk_approval"></a> Definições de aprovação
Uma das seguintes definições de aprovação é apresentada, consoante a sua versão do Configuration Manager:

- **Exigir aprovação do administrador caso os utilizadores solicitem esta aplicação**: Para versões 1710 e anteriores, o administrador aprova quaisquer pedidos de utilizador para a aplicação antes do utilizador pode instalá-lo. Esta opção é desativada quando o objetivo de implementação for **necessário**, ou ao implementar a aplicação para uma coleção de dispositivos.  

- **Um administrador tem de aprovar um pedido para esta aplicação no dispositivo**: A partir da versão 1802, o administrador aprova quaisquer pedidos de utilizador para a aplicação antes do utilizador pode instalá-lo no dispositivo pedido. Se o administrador aprova o pedido, o utilizador só é possível instalar o aplicativo nesse dispositivo. O utilizador tem de submeter outro pedido para instalar a aplicação noutro dispositivo. Esta opção é desativada quando o objetivo de implementação for **necessário**, ou ao implementar a aplicação para uma coleção de dispositivos.

 A partir da versão 1810, também pode definir uma lista de endereços de e-mail para notificar o pedido de aprovação. 
<!--1357015-->  

Para obter mais informações, consulte [aprovar aplicações](/sccm/apps/deploy-use/app-approval).


#### <a name="deployment-properties-deployment-settings"></a>Propriedades de implementação **definições de implementação**
Ao visualizar as propriedades de uma implementação, se for suportado pela tecnologia de tipo de implementação, a opção seguinte é apresentada no **definições de implementação** separador:

**Fechar automaticamente quaisquer executáveis em execução que especificou no separador de comportamento de instalação da caixa de diálogo de propriedades de tipo de implementação**. Para obter mais informações, consulte [para executar ficheiros executáveis antes de instalar uma aplicação de verificação](#bkmk_exe-check).



### <a name="bkmk_deploy-sched"></a> Implantação **agendamento** definições

Sobre o **agendamento** página, defina a hora quando esta aplicação é implementada ou disponíveis para dispositivos cliente.

Por predefinição, Configuration Manager torna a política de implementação disponíveis para os clientes imediatamente. Se pretender criar a implementação, mas não torná-la disponível para clientes até uma data posterior, configure a opção para **agendar a aplicação fique disponível**. Em seguida, selecione a data e hora, incluindo o facto de que se baseia em hora UTC ou hora de local do cliente. 

Se a implementação for **necessários**, especifique também a **prazo de instalação**. Por predefinição, este prazo seja, logo que possível. 

Por exemplo, precisa implantar uma nova aplicação de linha de negócio. Todos os utilizadores precisam para instalá-lo por um determinado período de tempo, mas quer lhes dar a opção de participar no início. Terá também de certificar-se de que o site distribuiu o conteúdo por todos os pontos de distribuição. Agendar a aplicação fique disponível em cinco dias de hoje. Esta agenda lhe dará tempo para distribuir o conteúdo e confirmar o estado do mesmo. Em seguida, definir o prazo de instalação durante um mês de hoje. Os utilizadores veem a aplicação no Centro de Software quando estiver disponível em cinco dias. Se elas não fazem nada, o cliente instala automaticamente o aplicativo no prazo de instalação. 

Se a aplicação que estiver a implementar substituir outra aplicação, defina o prazo de instalação quando os utilizadores recebem a nova aplicação. Definir o **prazo de instalação** para atualizar utilizadores com aplicação substituída.


#### <a name="delay-enforcement-with-a-grace-period"></a>Imposição de atraso com um período de tolerância
Talvez queira dar aos utilizadores mais tempo para instalar as aplicações necessárias *além* quaisquer prazos que definir. Este comportamento é normalmente exigido quando um computador está desativado por um longo tempo e tem de instalar várias aplicações. Por exemplo, quando um usuário retorna de férias, têm de aguardar por muito tempo, pois o cliente instala implementações em atraso. Para ajudar a resolver este problema, defina um período de tolerância de imposição.

- Primeiro, configure este período de tolerância com a propriedade **período de tolerância para a imposição de após a implementação do prazo (horas)** nas definições do cliente. Para obter mais informações, consulte a [agente do computador](/sccm/core/clients/deploy/about-client-settings#computer-agent) grupo. Especifique um valor entre **1** e **120** horas.  

- Sobre o **agendamento** página de uma implementação de aplicação necessária, ative a opção para **Trasar imposição para esta implementação, de acordo com as preferências do usuário, até o período de tolerância definido nas definições de cliente** . O período de tolerância de imposição aplica-se a todas as implementações com esta opção ativada e direcionadas para dispositivos em que implementou também a definição de cliente.

Após o prazo, o cliente instala a aplicação na primeira janela não comerciais, que o utilizador configurado, até esse período de tolerância. No entanto, o utilizador ainda pode abrir o Centro de Software e instalar a aplicação em qualquer altura. Assim que o período de tolerância expirar, imposição reverte para o comportamento normal para implementações em atraso.


### <a name="bkmk_deploy-ux"></a> Implantação **experiência de utilizador** definições

Sobre o **experiência de utilizador** , especifique informações sobre como os usuários podem interagir com a instalação da aplicação.

- **Notificações do utilizador**: Especifique se pretende apresentar a notificação no Centro de Software ao tempo disponível configurado. Esta definição controla se é necessário notificar os utilizadores nos computadores cliente. Para implementações disponíveis, não é possível selecionar a opção para **ocultar no Centro de Software e em todas as notificações**.  

- **Instalação de software** e **reiniciar o sistema**: Apenas a configurar estas definições para as implementações necessárias. Eles especificam os comportamentos quando a implementação de atinge o prazo de fora de quaisquer janelas de manutenção definida. Para obter mais informações sobre janelas de manutenção, consulte [como utilizar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).  

- **Processamento para dispositivos Windows Embedded do filtro de escrita**: Esta definição controla o comportamento de instalação em dispositivos Windows Embedded que estão ativados com um filtro de escrita. Escolha a opção para consolidar as alterações no prazo de instalação ou durante uma janela de manutenção. Quando seleciona esta opção, é necessário um reinício e as alterações sejam mantidas no dispositivo. Caso contrário, o aplicativo é instalado para a sobreposição temporária e confirmado posteriormente.  

    - Ao implementar uma atualização de software num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção e dispositivos Windows Embedded, consulte [aplicações criar Windows Embedded](/sccm/apps/get-started/creating-windows-embedded-applications).  


### <a name="bkmk_deploy-alerts"></a> Implementação **alertas**

Sobre o **alertas** página, configure a forma como o Configuration Manager gera alertas para esta implementação. Se também estiver a utilizar o System Center Operations Manager, configure os seus alertas também. Só pode configurar alguns alertas para as implementações necessárias. 


### <a name="bkmk_deploy-ios"></a> iOS: **Políticas de configuração de aplicação**

Ao implementar um tipo de implementação iOS, também verá os **políticas de configuração de aplicação** página. Se já tiver criado um iOS a política de configuração de aplicação, clique em **New** para associar esta implementação com a política. Para obter mais informações sobre este tipo de política, consulte [configurar aplicações iOS com políticas de configuração de aplicação](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).



## <a name="bkmk_phased"></a> Criar uma implementação faseada
<!--1358147--> A partir da versão 1806, crie uma implementação faseada para uma aplicação. As implementações faseadas permitem-lhe organizar uma implementação coordenada e sequenciada de software com base em critérios personalizáveis e grupos. Por exemplo, implementar a aplicação para uma coleção piloto e, em seguida, continuar automaticamente a implementação com base nos critérios de sucesso. 

Para obter mais informações, veja os artigos seguintes:  

- [Criar uma implementação faseada](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Gerir e monitorizar as implementações faseadas](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  



## <a name="bkmk_delete"></a> Eliminar uma implementação

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**e selecione o **aplicativos** nó.  

2.  Na **aplicativos** , selecione a aplicação que inclui a implementação que pretende eliminar.  

3.  Mude para o **implementações** separador do painel de detalhes e selecione a implementação da aplicação.  

4. No Friso, no **implantação** separador e o **implantação** , clique em **eliminar**.  

Quando elimina uma implementação de aplicações, as instâncias da aplicação que já tem instalado os clientes não são removidas. Para remover estas aplicações, implementar a aplicação para computadores **desinstalação**. Se eliminar uma implementação de aplicações ou remover um recurso da coleção para a qual estiver a implementar, a aplicação já não é visível no Centro de Software.



## <a name="bkmk_notify"></a> Notificações do utilizador para as implementações necessárias

Quando os utilizadores receber o software necessário e selecione o **suspender e lembrar-me** definir, podem escolher entre as seguintes opções:  

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



## <a name="bkmk_exe-check"></a> Verificação para a execução de ficheiros executáveis

Configure uma implementação para verificar se determinados ficheiros executáveis estão em execução no cliente. Utilize esta opção para verificar a existência de processos que poderão interromper a instalação do aplicativo. Se um desses arquivos executáveis está em execução, o cliente bloqueia a instalação do tipo de implementação. O utilizador tem de fechar o ficheiro executável está em execução antes do cliente pode instalar o tipo de implementação. Para implementações com um objetivo necessário, o cliente pode fechar automaticamente o ficheiro executável está em execução.

1. Abra o **propriedades** caixa de diálogo para o tipo de implementação.  

2. Mude para o **comportamento de instalação** separador e clique em **Add**.  

3. Na **adicionar ficheiro executável** caixa de diálogo, introduza o nome do ficheiro executável de destino. Opcionalmente, introduza um nome amigável para a aplicação para o ajudar a identificá-lo na lista.  

4. Clique em **OK**, em seguida, clique em **OK** para fechar a janela de propriedades do tipo de implementação.  

5. Quando implementar a aplicação, selecione a opção para **fechar automaticamente quaisquer executáveis em execução que especificou no separador de comportamento de instalação da caixa de diálogo de propriedades de tipo de implementação**. Essa opção permanece ativada a **definições de implementação** separador de propriedades de implementação.  


### <a name="client-behaviors-and-user-notifications"></a>Comportamentos de cliente e notificações de utilizador

Depois dos clientes recebem a implementação, o seguinte comportamento aplica-se:  

- Se implementou a aplicação como **disponível**e um utilizador tenta instalá-lo, o cliente solicita ao usuário para fechar os ficheiros executáveis em execução especificados antes de continuar com a instalação.  

- Se implementou a aplicação como **necessários**e especificado para **fechar automaticamente quaisquer executáveis em execução que especificou no separador de comportamento de instalação da caixa de diálogo de propriedades de tipo de implementação**, em seguida, o cliente apresenta uma notificação. Ele informa o utilizador que os ficheiros executáveis especificados automaticamente estão fechados quando é atingido o prazo de instalação do aplicativo.  

    - Agendar essas caixas de diálogo a **agente do computador** grupo de definições de cliente. Para obter mais informações, consulte [agente do computador](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

    - Se não pretender que o utilizador veja estas mensagens, selecione a opção para **ocultar no Centro de Software e em todas as notificações** sobre o **experiência do usuário** separador de propriedades da implementação. Para obter mais informações, consulte [definições de experiência de utilizador de implementação](#bkmk_deploy-ux).  

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

    - Os clientes tem de resolver o nome de domínio completamente qualificado (FQDN) do ponto de gestão ativado para HTTPS  



## <a name="next-steps"></a>Passos seguintes
 - [Monitorizar aplicações](/sccm/apps/deploy-use/monitor-applications-from-the-console)
 - [Tarefas de gestão para aplicações](/sccm/apps/deploy-use/management-tasks-applications)
 - [Manual do utilizador do Software Center](/sccm/core/understand/software-center)


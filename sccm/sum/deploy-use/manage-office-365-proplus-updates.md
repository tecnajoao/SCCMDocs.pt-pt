---
title: Gerir as atualizações do Office 365 ProPlus
titleSuffix: Configuration Manager
description: O Configuration Manager sincroniza atualizações de cliente do Office 365 do catálogo WSUS para o servidor do site para disponibilizar as atualizações disponíveis para implementação em clientes.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 1fa5646b17646258e4863b3a53960c9c15497389
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418191"
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>Gerir o Office 365 ProPlus com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager permite-lhe gerir aplicações do Office 365 ProPlus das seguintes formas:

- [Dashboard de gestão de clientes do Office 365](#office-365-client-management-dashboard): Pode rever as informações de cliente do Office 365 a partir do dashboard gestão de clientes do Office 365. A partir do Configuration Manager versão 1802, o dashboard de gestão de cliente do Office 365 mostra uma lista de dispositivos relevantes quando as secções do gráfico estão selecionadas. <!--1357281 -->

- [Implementar aplicações do Office 365](#deploy-office-365-apps): Pode começar o instalador do Office 365 a partir do dashboard de gestão de clientes do Office 365 para tornar a experiência mais fácil de instalação de aplicativo do Office 365 inicial. O assistente permite-lhe configurar definições de instalação do Office 365, transfira ficheiros a partir de redes de entrega de conteúdo do Office (CDNs) e criar e implementar uma aplicação de scripts com o conteúdo.    

- [Implementar atualizações do Office 365](#deploy-office-365-updates): Pode gerir atualizações de cliente do Office 365, utilizando o fluxo de trabalho de gestão de atualização de software. Quando a Microsoft publica uma nova atualização de cliente do Office 365 para rede Office da entrega de conteúdos (CDN), a Microsoft publica também um pacote de atualização para Windows Server Update Services (WSUS). Depois do Configuration Manager sincroniza a atualização do cliente do Office 365 do catálogo WSUS para o servidor do site, a atualização está disponível para implementação em clientes.    

- [Adicionar idiomas para o Office 365 atualizar downloads](#add-languages-for-office-365-update-downloads): Pode adicionar suporte para o Configuration Manager para transferir atualizações para outros idiomas suportados pelo Office 365. Significado Configuration Manager não tem que oferecer suporte o idioma, desde que faz do Office 365. Antes do Configuration Manager versão 1610 tem de transferir e implementar atualizações nos mesmos idiomas configurados em clientes do Office 365. 

- [Alterar o canal de atualização](#change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager): Pode utilizar a política de grupo para distribuir uma alteração do valor da chave de registo para clientes do Office 365 para alterar o canal de atualização.


## <a name="office-365-client-management-dashboard"></a>Dashboard de gestão de clientes do Office 365  
O dashboard de gestão de clientes do Office 365 fornece gráficos para as seguintes informações:

- Número de clientes do Office 365
- Versões de cliente do Office 365
- Idiomas de cliente do Office 365
- Canais de cliente do Office 365     
  Para obter mais informações, consulte [canais de descrição geral da atualização do Office 365 ProPlus](/DeployOffice/overview-of-update-channels-for-office-365-proplus).

Para ver o dashboard de gestão de clientes do Office 365 na consola do Configuration Manager, aceda a **biblioteca de Software** > **descrição geral** > **cliente do Office 365 Gestão**. Na parte superior do dashboard, utilize o **coleção** definição de lista pendente para filtrar os dados de dashboard por membros de uma coleção específica. A partir do Configuration Manager versão 1802, o dashboard de gestão de cliente do Office 365 mostra uma lista de dispositivos relevantes quando as secções do gráfico estão selecionadas.

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>Exibir dados no dashboard de gestão de clientes do Office 365
Os dados que são apresentados no dashboard de gestão de clientes do Office 365 provém de inventário de hardware. Ativar inventário de hardware e selecione o **as de configurações do Office 365 ProPlus** classe de inventário de hardware para os dados apresentar no dashboard. 
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>Para exibir dados no dashboard de gestão de clientes do Office 365
1. Ative inventário de hardware, se ainda não está ativada. Para obter detalhes, consulte [configurar o inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).
2. Na consola do Configuration Manager, navegue até **Administration** > **definições de cliente** > **predefinições de cliente**.  
3. No separador **Home page** , no grupo **Propriedades** , clique em **Propriedades**.  
4. Na caixa de diálogo **Predefinições de Cliente** , clique em **Inventário de Hardware**.  
5. Na lista **Definições do Dispositivo** , clique em **Definir Classes**.  
6. Na **Classes de inventário de Hardware** caixa de diálogo, selecione **as de configurações do Office 365 ProPlus**.  
7.  Clique em **OK** para guardar as suas alterações e fechar a caixa de diálogo **Classes de Inventário de Hardware** . <br/>O dashboard de gestão de clientes do Office 365 começa a exibição de dados de inventário de hardware é comunicado.

## <a name="deploy-office-365-apps"></a>Implementar aplicações do Office 365  
Inicie o instalador do Office 365 a partir do dashboard de gestão de clientes do Office 365 para a instalação inicial do aplicativo do Office 365. O assistente permite-lhe configurar definições de instalação do Office 365, transfira ficheiros a partir de redes de entrega de conteúdos (CDNs), do Office e criar e implementar uma aplicação de scripts para os ficheiros. Até que o Office 365 está instalada nos clientes e o [tarefas de atualizações do Office automática](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) execuções de atualizações do Office 365 não são aplicáveis. Para fins de teste, pode executar manualmente a tarefa de atualização.

Para versões anteriores do Configuration Manager, deve efetuar os seguintes passos para instalar aplicações do Office 365 pela primeira vez em clientes:
- Transferir a ferramenta de implantação do Office 365 (ODT)
- Transferir os ficheiros de origem de instalação do Office 365, incluindo todos os pacotes de idiomas que precisa.
- Gere a configuração. XML que especifica a versão correta do Office e o canal.
- Criar e implementar um pacote de legado ou uma aplicação de scripts para os clientes instalar aplicações do Office 365.

### <a name="requirements"></a>Requisitos
- O computador que executa o instalador do Office 365 tem de ter acesso à Internet.  
- O utilizador que executa o instalador do Office 365 tem de ter **leitura** e **escrever** acesso à partilha de localização de conteúdo fornecido no assistente.
- Se receber um erro 404 transferências, copie os seguintes ficheiros para a pasta % temp % do utilizador:
  - [releasehistory.xml](http://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-office-365-apps-using-configuration-manager-version-1806-or-higher"></a>Implemente aplicações do Office 365 com o Configuration Manager versão 1806 ou superior: 
A partir do Configuration Manager 1806, a ferramenta de personalização do Office está integrada com o instalador do Office 365 na consola do Configuration Manager. Ao criar uma implementação para o Office 365, pode configurar as definições de capacidade de gestão mais recentes do Office de forma dinâmica. <!--1358149-->

1. Na consola do Configuration Manager, navegue até **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**.
2. Clique em **Office 365 instalador** no painel de canto superior direito. É aberto o Assistente de instalação de cliente do Office 365.
3. Sobre o **as definições da aplicação** página, forneça um nome e descrição para a aplicação, introduza a localização de transferência para os ficheiros e, em seguida, clique em **próxima**. A localização deve ser especificada como &#92; &#92; *server*&#92;*partilhar*.
4. Sobre o **as configurações do Office** página, clique em **vá para a ferramenta de personalização do Office**. Esta ação abre o [ferramenta de personalização do Office para clique-e-use](https://config.office.com).
5. Configure as definições pretendidas para a sua instalação do Office 365. Clique nas **submeter** no canto superior direito da página quando concluir a configuração. 
6. Sobre o **implementação** página, determinar se deseja implementar agora ou mais tarde. Se optar por implementar mais tarde, pode encontrar a aplicação na **biblioteca de Software** < **gestão de aplicações** < **aplicativos**.  
7. Confirmar as definições na **resumo** página. 
8. Clique em **próxima** , em seguida, clique em **fechar** assim que concluir o Assistente de instalação de cliente do Office 365. 

### <a name="deploy-office-365-apps-using-configuration-manager-version-1802-and-prior"></a>Implemente aplicações do Office 365 com o Configuration Manager versão 1802 e anterior:

1. Na consola do Configuration Manager, navegue até **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**.
2. Clique em **Office 365 instalador** no painel de canto superior direito. É aberto o Assistente de instalação de cliente do Office 365.
3. Sobre o **as definições da aplicação** página, forneça um nome e descrição para a aplicação, introduza a localização de transferência para os ficheiros e, em seguida, clique em **próxima**. A localização deve ser especificada como &#92; &#92; *server*&#92;*partilhar*.
4. Sobre o **importar definições de cliente** página, selecione se pretende importar as definições de cliente do Office 365 a partir de um arquivo de configuração XML existente ou especifique manualmente as definições. Clique em **seguinte** quando terminar.  

    Quando tiver um ficheiro de configuração existente, introduza a localização do ficheiro e avance para o passo 7. Tem de especificar a localização na forma &#92; &#92; *server*&#92;*partilhar*&#92;*filename*. XML.
    > [!IMPORTANT]    
    > O ficheiro de configuração XML tem de conter apenas [idiomas suportados pelo cliente do Office 365 ProPlus](https://docs.microsoft.com/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016).

5. Sobre o **produtos de cliente** , selecione o pacote do Office 365 que utilizar. Selecione as aplicações que pretende incluir. Selecione os produtos adicionais do Office que devem ser incluídos e, em seguida, clique em **seguinte**.
6. Sobre o **definições de cliente** página, selecione as definições para incluir e, em seguida, clique em **próxima**.
7. Sobre o **implantação** página, escolha se pretende implementar a aplicação e, em seguida, clique em **próxima**. <br/>Se optar por não implementar o pacote no assistente, avance para o passo 9.
8. Configure o restante das páginas do assistente, tal como faria para uma implantação de aplicativos típico. Para obter detalhes, consulte [criar e implementar uma aplicação](/sccm/apps/get-started/create-and-deploy-an-application).
9. Conclua o assistente.
10. Pode implementar ou editar a aplicação a partir **biblioteca de Software** > **descrição geral** > **gestão de aplicações**  >   **Aplicativos**.    

Depois de criar e implementar aplicações do Office 365 com o instalador do Office 365, o Configuration Manager não gerir as atualizações do Office por predefinição. Para ativar clientes do Office 365 receber atualizações do Configuration Manager, consulte [com o Gestor de configuração de atualizações de implementar o Office 365](#deploy-office-365-updates-with-configuration-manager).

Depois de implementar aplicações do Office 365, pode criar regras de implementação automática para manter as aplicações. Para criar uma regra de implementação automática para aplicações do Office 365, clique em **criar uma ADR** partir do dashboard de gestão de clientes do Office 365. Selecione **cliente do Office 365** ao escolher o produto. Para obter mais informações, consulte [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates).


## <a name="deploy-office-365-updates"></a>Implementar atualizações do Office 365
Existe um agendadas [tarefas de atualizações automáticas no Office 365](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) que é executada várias vezes por semana. Se tiver instalado recentemente o Office 365, é possível que o canal de atualização ainda não foi definido e uma análise de atualização não irá encontrar atualizações aplicáveis para ele. Para fins de teste, pode iniciar manualmente a tarefa de atualização. 

Utilize os seguintes passos para implementar atualizações do Office 365 com o Configuration Manager:

1.  [Verifique se os requisitos](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates) para utilizar o Configuration Manager para gerir atualizações de cliente do Office 365 no **requisitos para utilizar o Configuration Manager para gerir atualizações de cliente do Office 365** secção do artigo.  

2.  [Configurar pontos de atualização de software](../get-started/configure-classifications-and-products.md) para sincronizar o cliente do Office 365 atualizações. Definir **atualizações** para a classificação e selecione **cliente do Office 365** para o produto. Sincronizar atualizações de software, depois de configurar os pontos de atualização de software para utilizar o **atualizações** classificação.
3.  Ative clientes do Office 365 receber atualizações do Configuration Manager. Definições de cliente utilize o Gestor de configuração ou política de grupo para permitir ao cliente.   

    **Método 1**: A partir do Configuration Manager versão 1606, pode utilizar a definição para gerir o agente do cliente do Office 365 de cliente do Configuration Manager. Depois de configurar esta definição e implementar atualizações do Office 365, o agente do cliente do Configuration Manager comunica com o agente de cliente do Office 365 para transferir as atualizações a partir de um ponto de distribuição e instalá-los. O Configuration Manager retira o inventário de definições de cliente do Office 365 ProPlus.    

      1.  Na consola do Configuration Manager, clique em **Administration** > **descrição geral** > **as definições de cliente**.  

      2.  Abra as definições de dispositivo adequados para ativar o agente de cliente. Para obter mais informações sobre o padrão e definições de cliente personalizadas, consulte [como configurar as definições de cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Clique em **atualizações de Software** e selecione **Sim** para o **ativar a gestão do agente de cliente do Office 365** definição.  

    **Método 2**: [Permitir que os clientes do Office 365 receber atualizações](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient) do Configuration Manager utilizando a ferramenta de implantação do Office ou a política de grupo.  

4. [Implementar as atualizações do Office 365](deploy-software-updates.md) aos clientes.   

> [!Important]
> - A partir de atualizações de cliente do Configuration Manager versão 1706 do Office 365 foram movidas para o **gestão de clientes do Office 365** >**atualizações do Office 365** nó. Esta mudança não afeta a configuração atual da ADR. 
> - Antes do Configuration Manager versão 1610 tem de transferir e implementar atualizações nos mesmos idiomas configurados em clientes do Office 365. Por exemplo, digamos que tenha um cliente do Office 365 configurado com o en-us e Alemanha-de idiomas. No servidor do site, baixe e implante o apenas en-us de conteúdo para uma atualização do Office 365 aplicável. Quando o usuário inicia a instalação do Centro de Software para esta atualização, a atualização trava ao transferir o conteúdo de-de.   


## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Reinicie as notificações de comportamento e de cliente para atualizações do Office 365
Ao implementar uma atualização para um cliente do Office 365, as notificações de cliente e o comportamento de reinício são diferentes consoante a versão do Configuration Manager. A tabela seguinte fornece informações sobre a experiência de utilizador final quando o cliente recebe uma atualização do Office 365:

|Versão do Configuration Manager |Experiência do utilizador final|  
|----------------|---------------------|
|1706, 1710|O cliente recebe notificações de pop-up e na aplicação, bem como uma caixa de diálogo de contagem regressiva, antes de instalar a atualização.|
|1802| O cliente recebe notificações de pop-up e na aplicação, bem como uma caixa de diálogo de contagem regressiva, antes de instalar a atualização. </br>Se estiver a executar todas as aplicações do Office 365 durante uma imposição de atualização de cliente do Office 365, os aplicativos do Office não serão forçados a fechar. Em vez disso, a instalação da atualização devolverá exigir um reinício do sistema <!--510006-->|


> [!Important]
>
>No Configuration Manager versão 1706, tenha em atenção os seguintes detalhes:
>
>- Apresenta um ícone de notificação na área de notificação na barra de tarefas para as aplicações necessárias em que o prazo é no prazo de 48 horas no futuro, e que o conteúdo da atualização foi transferido. 
>- Apresenta uma caixa de diálogo de contagem regressiva para as aplicações necessárias em que o prazo é dentro de 7,5 horas no futuro, e que a atualização foi transferida. O utilizador pode adiar a caixa de diálogo de contagem decrescente até três vezes antes do prazo. Quando adiada, a contagem regressiva mostra depois de duas horas. Se não for adiado, existe uma contagem decrescente de 30 minutos e atualização é instalada quando a contagem regressiva expira.
>- Uma notificação de pop-up poderão não ser mostrados até que o usuário clica no ícone na área de notificação. Além disso, se a área de notificação tem o espaço mínimo, o ícone de notificação pode não estar visível, a menos que o usuário abrir ou expande a área de notificação. 
>- A notificação e a caixa de diálogo de contagem regressiva poderiam começar enquanto o utilizador não está a trabalhar ativamente no dispositivo. Por exemplo, quando o dispositivo está bloqueado noite para o dia é possíveis aplicações do Office em execução no dispositivo foi forçado a fechar para instalar a atualização. Antes de fechar a aplicação, o Office guarda os dados de aplicações para evitar a perda de dados. 
>- Se o prazo estiver no passado ou configurado para iniciar logo que possível, execução de aplicações do Office será forçado a fechar sem notificações. 
>- Se o utilizador instala uma atualização do Office antes do prazo, o Configuration Manager verifica se a atualização é instalada quando for atingido o prazo. Se a atualização não for detectada num dispositivo, a atualização é instalada. 
>- A barra de notificação na aplicação não apresenta num aplicativo do Office que está a executar antes da atualização é transferida. Após a atualização ser transferida, a notificação na aplicação apresenta apenas para recentemente abertas de aplicações.
>- Para atualizações do Office acionada por um período de administração ou agendadas para o horário não comercial, é possível que a execução de aplicações do Office poderá ser forçado a fechar para instalar a atualização sem notificações. 
>- Para obter mais informações, consulte [notificações de atualização de utilizador final para o Office 365](https://docs.microsoft.com/deployoffice/end-user-update-notifications-for-office-365-proplus)



## <a name="add-languages-for-office-365-update-downloads"></a>Adicionar idiomas para as transferências de atualização do Office 365
Pode adicionar suporte para o Configuration Manager para transferir atualizações para outros idiomas que são suportados pelo Office 365, independentemente se elas têm suporte no Configuration Manager.    

> [!IMPORTANT]  
> A configuração de outros idiomas de atualização do Office 365 é uma definição ao nível do site. Depois de adicionar os idiomas utilizando o procedimento seguinte, todas as atualizações do Office 365 são transferidas nesses idiomas, bem como os idiomas que selecionou no **seleção de idioma** página na implementar ou transferir atualizações de Software Assistentes de atualizações de software.

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>Para adicionar suporte para transferir atualizações para idiomas adicionais
Utilize o procedimento seguinte no ponto de atualização de software no site de administração central ou site primário autónomo.
1. A partir de uma linha de comandos, escreva *wbemtest* como um utilizador administrativo para abrir o Testador de instrumentação de gerenciamento do Windows.
2. Clique em **Connect**e, em seguida, escreva *root\sms\site_&lt;siteCode&gt;*.
3. Clique em **consulta**, e, em seguida, execute a seguinte consulta: *selecionar &#42; do SMS_SCI_Component onde componentname = "SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![Consulta de WMI](../media/1-wmiquery.png)
4. No painel de resultados, faça duplo clique o objeto com o código do site para o site de administração central ou site primário autónomo.
5. Selecione o **propriedades** propriedade, clique em **Editar propriedade**e, em seguida, clique em **View Embedded**.
   ![Editor de propriedade](../media/2-propeditor.png)
6. Começando do primeiro resultado da consulta, abra cada objeto até encontrar aquela que acompanha **AdditionalUpdateLanguagesForO365** para o **PropertyName** propriedade.
7. Selecione **Value2** e clique em **Editar propriedade**.  
   ![Editar a propriedade Value2](../media/3-queryresult.png)
8. Adicionar idiomas adicionais para o **Value2** propriedade e clique em **guardar propriedade**. <br/> Por exemplo, pt-pt (em Português - Portugal), af-za (para Afrikaans – África do Sul), não nn (por Norueguês (Nynorsk) – Noruega), etc. Teria de escrever `pt-pt,af-za,nn-no` para os idiomas de exemplo. Não utilize espaços entre os idiomas.
 
   ![Adicionar idiomas no Editor de propriedade](../media/4-props.png)  
9. Clique em **fechar**, clique em **fechar**, clique em **guardar propriedade**e clique em **guardar objeto** (se clicar em **fechar**aqui os valores são eliminados). Clique em **fechar**e, em seguida, clique em **sair** para sair o Testador de instrumentação de gerenciamento do Windows.
10. Na consola do Configuration Manager, aceda a **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**  >  **Atualizações do office 365**.
11. Agora quando baixa atualizações do Office 365, serão transferidas as atualizações nos idiomas que selecione no assistente e configurou neste procedimento. Para verificar que a transferência de atualizações nos idiomas corretos, vão para a origem do pacote para a atualização e procurar ficheiros com o código de idioma no nome de ficheiro.  
    ![Nomes de ficheiros com idiomas adicionais](../media/5-verification.png)

## <a name="updating-office-365-during-task-sequences-when-office-365-is-installed-in-the-base-image"></a>A atualização do Office 365 durante sequências de tarefas quando o Office 365 é instalado na imagem base
Quando instala um sistema operativo em que o Office 365 já está instalado na imagem, é possível que o valor de chave do registo de canal de atualização tem a localização de instalação original. Neste caso, a análise de atualização não mostrará as atualizações de cliente do Office 365 conforme aplicável. Existe uma tarefa agendada de atualizações automáticas Office que é executada várias vezes por semana. Depois dessa tarefa é executada, o canal de atualização irá apontar para o URL de CDN configurado do Office e a análise, em seguida, irá mostrar estas atualizações, conforme aplicável. <!--510452-->

Para garantir que o canal de atualização está definido para que as atualizações aplicáveis serão encontradas, siga os passos abaixo:
1. Num computador com a mesma versão do Office 365, como a imagem base do sistema operacional, abra o agendador de tarefas (taskschd.msc) e identificar a tarefa de atualizações automáticas do Office 365. Normalmente, está localizado em **biblioteca do Programador de tarefas** >**Microsoft**>**Office**.
2. Botão direito do mouse sobre a automática de atualizações de tarefa e selecione **propriedades**.
3. Vá para o **ações** separador e clique em **editar**. Copie o comando e quaisquer argumentos. 
4. Na consola do Configuration Manager, edite a sequência de tarefas.
5. Adicionar um novo **executar linha de comandos** passo antes do **instalar atualizações** passo na sequência de tarefas. 
6. Copie o comando e os argumentos que obtidas com a tarefa agendada de atualizações automáticas do Office. 
7. Clique em **OK**. 

## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Alterar o canal de atualização depois de ativar clientes do Office 365 receber atualizações do Configuration Manager
Para alterar o canal de atualização depois de ativar clientes do Office 365 receber atualizações do Configuration Manager, utilize a política de grupo para distribuir uma alteração do valor da chave de registo para clientes do Office 365. Alteração da **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** chave de registo para utilizar um dos seguintes valores:

- Canal mensal <br/>
<i>(anteriormente conhecido como canal de atual) </i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Canal semi-anual <br/>
<i>(anteriormente conhecido como diferido canal) </i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- Canal mensal (direcionado)<Br/>
 <i>(anteriormente conhecido como um lançamento inicial para o canal atual) </i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- Canal Semianual (direcionado) <br/>
<i>(anteriormente conhecido como um lançamento inicial para o canal diferido) </i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf <!--the channel names changed in Sept 2017- https://docs.microsoft.com/en-us/DeployOffice/overview-of-update-channels-for-office-365-proplus?ui=en-US&rs=en-US&ad=US-->


<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->

---
title: "Gerir atualizações do Office 365 ProPlus | Microsoft Docs"
description: "O Gestor de configuração sincroniza atualizações de cliente do Office 365 no catálogo WSUS ao servidor do site para disponibilizar atualizações disponíveis para implementação em clientes."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 05/31/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 902d7f7216ca7bb585afae587a6706e2332da9d3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>Gerir o Office 365 ProPlus com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager permite-lhe gerir aplicações do Office 365 ProPlus das seguintes formas:

- [Dashboard de gestão de clientes do Office 365](#office-365-client-management-dashboard): A partir do Configuration Manager versão 1610, poderá rever as informações de cliente do Office 365 a partir do dashboard de gestão de clientes do Office 365.    

- [Implementar aplicações do Office 365](#deploy-office-365-apps): A partir da versão 1702, pode iniciar o instalador do Office 365 a partir do dashboard de gestão de clientes do Office 365 para tornar a experiência mais fácil de instalação de aplicações do Office 365 inicial. O assistente permite-lhe configurar definições de instalação do Office 365, transfira ficheiros a partir de redes de entrega de conteúdo do Office (CDNs) e criar e implementar uma aplicação de scripts com o conteúdo.    

- [Implementar atualizações do Office 365](#deploy-office-365-updates): A partir do Configuration Manager versão 1602, pode gerir atualizações de cliente do Office 365, utilizando o fluxo de trabalho de gestão de atualização de software. Quando a Microsoft publica uma nova atualização de cliente do Office 365 para rede Office da entrega de conteúdos (CDN), a Microsoft publica também um pacote de atualização para Windows Server Update Services (WSUS). Depois do Gestor de configuração sincroniza a atualização do cliente do Office 365 do catálogo WSUS para o servidor do site, a atualização está disponível para implementação em clientes.    

- [Adicionar atualizações de idiomas para o Office 365 transferências](#add-languages-for-office-365-update-downloads): A partir do Configuration Manager versão 1610, pode adicionar suporte para o Configuration Manager para transferir atualizações para os idiomas suportados pelo Office 365, independentemente se são suportados no Configuration Manager.  

- [Alterar o canal de atualização](#change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager): Pode utilizar a política de grupo para distribuir uma alteração de valor de chave de registo para clientes do Office 365 para alterar o canal de atualização.


## <a name="office-365-client-management-dashboard"></a>Dashboard de gestão de clientes do Office 365  
O dashboard de gestão de clientes do Office 365 fornece gráficos para as seguintes informações:

- Número de clientes do Office 365
- Versões de cliente do Office 365
- Idiomas de cliente do Office 365
- Canais de cliente do Office 365     
  Para obter mais informações, consulte [canais de consumo de descrição geral da atualização para o Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).

Para ver o dashboard de gestão de clientes do Office 365 na consola do Configuration Manager, aceda a **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**. Na parte superior do dashboard, utilize o **coleção** definição de lista pendente para filtrar os dados de dashboard por membros da coleção específica.

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>Apresentar dados no dashboard de gestão de clientes do Office 365
Os dados que são apresentados no dashboard de gestão de clientes do Office 365 provém de inventário de hardware. Tem de ativar o inventário de hardware e selecione o **Office 365 ProPlus configurações** apresenta de classe de inventário de hardware antes de dados no dashboard.
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>Para apresentar dados no dashboard de gestão de clientes do Office 365
1. Ative inventário de hardware, se ainda não estiver ativada. Para obter mais informações, consulte [configurar o inventário de hardware](\sccm\core\clients\manage\configure-hardware-inventory).
2. Na consola do Configuration Manager, navegue até à **administração** > **as definições de cliente** > **predefinições de cliente**.  
3. No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  
4. Na caixa de diálogo **Predefinições de Cliente** , clique em **Inventário de Hardware**.  
5. Na lista **Definições do Dispositivo** , clique em **Definir Classes**.  
6. No **Classes de inventário de Hardware** caixa de diálogo, selecione **Office 365 ProPlus configurações**.  
7.  Clique em **OK** para guardar as suas alterações e fechar a caixa de diálogo **Classes de Inventário de Hardware** .  
O dashboard de gestão de clientes do Office 365 inicia a apresentar dados como o inventário de hardware é comunicado.

## <a name="deploy-office-365-apps"></a>Implementar aplicações do Office 365  
A partir da versão 1702, inicie o instalador do Office 365 a partir do dashboard de gestão de clientes do Office 365 para a instalação inicial da aplicação do Office 365. O assistente permite-lhe configurar definições de instalação do Office 365, transfira ficheiros a partir de redes de entrega de conteúdo (CDNs) do Office e criar e implementar uma aplicação de scripts para os ficheiros. Até que seja instalada do Office 365 nos clientes, atualizações do Office 365 não são aplicáveis.

Para versões anteriores do Configuration Manager, tem de efetuar os seguintes passos para instalar aplicações do Office 365 pela primeira vez em clientes:
- Transferir a ferramenta de implementação do Office 365 (ODT)
- Transfira os ficheiros de origem de instalação do Office 365, incluindo todos os pacotes de idiomas que precisa.
- Gere Configuration.xml que especifica a versão correta do Office e o canal.
- Criar e implementar um pacote de legado ou uma aplicação de scripts para os clientes instalam as aplicações do Office 365.

### <a name="requirements"></a>Requisitos
- O computador que executa o instalador do Office 365 tem de ter acesso à Internet.  
- O utilizador que executa o instalador do Office 365 tem de ter **leitura** e **escrever** acesso à partilha de localização de conteúdo é fornecido no assistente.
- Se receber um erro de 404 transferência, copie os seguintes ficheiros para a pasta % temp % do utilizador:
  - [releasehistory.XML](http://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.XML](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  


### <a name="to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard"></a>Para implementar aplicações do Office 365 para clientes a partir do dashboard de gestão de clientes do Office 365
1. Na consola do Configuration Manager, navegue até à **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**.
2. Clique em **instalador do Office 365** no painel superior direito. É aberto o Assistente de instalação de cliente do Office 365.
3. No **definições da aplicação** página, forneça um nome e descrição para a aplicação, introduza a localização de transferência para os ficheiros e, em seguida, clique em **seguinte**. A localização tem de ser especificada como &#92; &#92; *server*&#92; *partilhar*.
4. No **importar as definições de cliente** página, escolha se importar as definições de cliente do Office 365 a partir de um ficheiro de configuração XML existente ou especifique manualmente as definições e, em seguida, clique em **seguinte**.  

    Quando tiver um ficheiro de configuração existente, introduza a localização do ficheiro e avance para o passo 7. Tenha em atenção que a localização tem de ser especificada no formulário &#92; &#92; *server*&#92; *partilhar*&#92; *nome de ficheiro*. XML.
    > [!IMPORTANT]    
    > O ficheiro de configuração XML tem de conter apenas [idiomas suportados pelo cliente do Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx).

5. No **cliente produtos** página, selecione o Office 365 suite que utilizar, selecione as aplicações que pretende incluir, selecione os produtos de Office adicionais que devem ser incluídos e, em seguida, clique em **seguinte**.
6. No **as definições de cliente** página, escolha as definições para incluir e, em seguida, clique em **seguinte**.
7. No **implementação** página, escolha se pretende implementar a aplicação e, em seguida, clique em **seguinte**.  
Se optar por não implementar o pacote no assistente, avance para o passo 9.
8. Configure as restantes páginas do assistente, tal como faria para uma implementação de aplicação típica. Para obter mais informações, consulte [criar e implementar uma aplicação](/sccm/apps/get-started/create-and-deploy-an-application).
9. Conclua o assistente.
10. Pode implementar ou editar a aplicação do **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **aplicações**.    

Depois de criar e implementar aplicações do Office 365, utilizando o instalador do Office 365, do Configuration Manager não irão gerir as atualizações do Office por predefinição. Para ativar os clientes do Office 365 receber atualizações do Configuration Manager, consulte [atualizações de implementar o Office 365 com o Configuration Manager](#deploy-office-365-updates-with-configuration-manager).

>[!NOTE]
>Depois de implementar aplicações do Office 365, pode criar regras de implementação automática para manter as aplicações. Para criar uma regra de implementação automática para aplicações do Office 365, clique em **criar uma ADR** do dashboard de gestão de clientes do Office 365 e selecione **cliente do Office 365** quando escolhe o produto. Para obter mais informações, consulte [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates).


## <a name="deploy-office-365-updates"></a>Implementar atualizações do Office 365
Utilize os seguintes passos para implementar atualizações do Office 365 com o Configuration Manager:

1.  [Certifique-se os requisitos](https://technet.microsoft.com/library/mt628083.aspx) para utilizar o Configuration Manager para gerir atualizações de cliente do Office 365 no **requisitos para utilizar o Configuration Manager para gerir atualizações de cliente do Office 365** secção do tópico.  

2.  [Configurar pontos de atualização de software](../get-started/configure-classifications-and-products.md) para sincronizar o cliente do Office 365 atualizações. Definir **atualizações** para a classificação e selecione **cliente do Office 365** para o produto. Sincronizar atualizações de software, depois de configurar os pontos de atualização de software para utilizar o **atualizações** classificação.
3.  Ative clientes do Office 365 receber atualizações do Configuration Manager. Pode fazê-lo utilizando a política de grupo ou definições de cliente do Configuration Manager. Utilize um dos seguintes métodos para ativar o cliente:   

    **Método 1**: A partir do Configuration Manager versão 1606, pode utilizar o Configuration Manager definição de cliente para gerir o agente do cliente do Office 365. Depois de configurar esta definição e implementar atualizações do Office 365, o agente do cliente do Configuration Manager comunica com o agente do cliente do Office 365 para transferir atualizações do Office 365 a partir de um ponto de distribuição e instalá-los. O Configuration Manager retira o inventário de definições de cliente do Office 365 ProPlus.    

      1.  Na consola do Configuration Manager, clique em **administração** > **descrição geral** > **as definições de cliente**.  

      2.  Abra as definições de dispositivo adequados para ativar o agente de cliente. Para obter mais informações sobre as definições de cliente personalizadas e predefinidas, consulte [como configurar as definições de cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Clique em **atualizações de Software** e selecione **Sim** para o **ativar a gestão do agente de cliente do Office 365** definição.  

    **Método 2**: [Ativar clientes do Office 365 receber atualizações](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient) do Configuration Manager utilizando a ferramenta de implementação do Office ou a política de grupo.  

4. [Implementar as atualizações do Office 365](deploy-software-updates.md) aos clientes.   

> [!Important]
> Tem de transferir e implementar atualizações nos idiomas mesmos configurados nos clientes do Office 365. Por exemplo, vamos supor que tem um cliente do Office 365 configurado com o en-us e Alemanha Alemanha idiomas. No servidor do site, transferir e implementar apenas en-us de conteúdo para uma atualização do Office 365 aplicável. Quando o utilizador inicia a instalação a partir do Centro de Software para esta atualização, a atualização, esta bloqueará ao transferir o conteúdo.   

## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Reinicie as notificações de comportamento e o cliente para atualizações do Office 365
Quando implementar uma atualização para um cliente do Office 365, as notificações de cliente e o comportamento de reinício são diferentes consoante a versão do Configuration Manager que tem. A tabela seguinte fornece informações sobre a experiência de utilizador final quando o cliente recebe uma atualização do Office 365:

|Versão do Configuration Manager |Experiência de utilizador final|  
|----------------|---------------------|
|Antes de 1610|Está definido um sinalizador de reinício e a atualização for instalada após o computador for reiniciado.|
|1610|Aplicações do Office 365 são encerradas sem aviso antes de instalar a atualização|
|1610 com a atualização <br/>1702|Está definido um sinalizador de reinício e a atualização for instalada após o computador for reiniciado.|
|1706|O cliente recebe as notificações de pop-up e na aplicação, bem como uma caixa de diálogo de contagem decrescente, antes de instalar a atualização.|


## <a name="add-languages-for-office-365-update-downloads"></a>Adicionar idiomas para as transferências de atualização do Office 365
A partir do Configuration Manager versão 1610, pode adicionar suporte para o Configuration Manager para transferir atualizações para os idiomas suportados pelo Office 365, independentemente se são suportados no Configuration Manager.    

> [!IMPORTANT]  
> Configurar outros idiomas de atualização do Office 365 é uma definição ao nível do site. Depois de adicionar os idiomas utilizando o procedimento seguinte, todas as atualizações do Office 365 são transferidas os idiomas selecionados, bem como os idiomas que selecionou no **seleção de idioma** página nos assistentes para transferir atualizações de Software ou implementar as atualizações de Software.

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>Para adicionar suporte para transferir atualizações para idiomas adicionais
Utilize o procedimento seguinte no ponto de atualização de software no site de administração central ou site primário autónomo.
1. A partir de uma linha de comandos, escreva *wbemtest* como um utilizador administrativo para abrir o recurso de teste do Windows Management Instrumentation.
2. Clique em **Connect**e, em seguida, escreva *root\sms\site_&lt;siteCode&gt;*.
3. Clique em **consulta**, e, em seguida, execute a seguinte consulta: *selecione &#42; do SMS_SCI_Component onde componentname = "SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![Consulta de WMI](..\media\1-wmiquery.png)
4. No painel de resultados, faça duplo clique o objeto com o código do site para o site de administração central ou site primário autónomo.
5. Selecione o **propriedades** propriedade, clique em **Editar propriedade**e, em seguida, clique em **vista incorporados**.
![Editor de propriedades](..\media\2-propeditor.png)
6. Começando no resultado da consulta primeiro, abra cada objeto até encontrar a **AdditionalUpdateLanguagesForO365** para o **PropertyName** propriedade.
7. Selecione **Value2** e clique em **Editar propriedade**.  
![Editar a propriedade de Value2](..\media\3-queryresult.png)
8. Adicionar outros idiomas para o **Value2** propriedade e clique em **guardar propriedade**.  
Por exemplo, pt-pt (para Português - Portugal), af-za (para Afrikaans - África do Sul), não nn (para norueguês (Nynorsk) - Noruega), etc.  
![Adicionar idiomas no Editor de propriedade](..\media\4-props.png)  
9. Clique em **fechar**, clique em **fechar**, clique em **guardar propriedade**, clique em **guardar objeto** (se clicar em **fechar** aqui os valores são eliminados), clique em **fechar**e, em seguida, clique em **sair** para sair do recurso de teste do Windows Management Instrumentation.
10. Na consola do Configuration Manager, vá para **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365** > **atualizações do Office 365**.
11. Agora quando transferir atualizações do Office 365, serão transferidas as atualizações nos idiomas de que seleciona no assistente e configurado neste procedimento. Para verificar se as atualizações de transferir nos idiomas corretos, avance para a origem do pacote para a atualização e procurarem ficheiros com o código de idioma no nome de ficheiro.  
![Nomes de ficheiros com outros idiomas](..\media\5-verification.png)


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Alterar o canal de atualização depois de ativar a clientes do Office 365 receber atualizações do Configuration Manager
Para alterar o canal de atualização depois de ativar a clientes do Office 365 receber atualizações do Configuration Manager, utilize a política de grupo para distribuir uma alteração de valor de chave de registo para clientes do Office 365. Alterar o **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** chave de registo para utilizar um dos seguintes valores:

- Canal atual:  
  **CDNBaseUrl** = http &#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Canal diferida:  
  **CDNBaseUrl** = http &#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- Primeira versão para o canal atual:  
  **CDNBaseUrl** = http &#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- Primeira versão para o canal diferida:  
  **CDNBaseUrl** = http &#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf



<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->

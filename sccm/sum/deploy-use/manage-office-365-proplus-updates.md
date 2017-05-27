---
title: "Gerir atualizações do Office 365 ProPlus | Documentos do Microsoft"
description: "O Gestor de configuração sincroniza atualizações de cliente do Office 365 no catálogo WSUS para o servidor do site para disponibilizar atualizações disponíveis para implementação em clientes."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/24/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 016580dc6ee3c5268833db941d42416a976d201c
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---

# <a name="manage-office-365-proplus-with-configuration-manager"></a>Gerir o Office 365 ProPlus com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager sincroniza atualizações de cliente do Office 365 e torna-os disponíveis para implementação em clientes com o Office 365 instalado. A partir do Configuration Manager versão 1610, pode rever as informações de cliente do Office 365 a partir do dashboard de gestão de clientes do Office 365.

A partir do Configuration Manager versão 1602, o Configuration Manager possui a capacidade para gerir atualizações de cliente do Office 365 utilizando o fluxo de trabalho de gestão de atualização de software. Quando a Microsoft publica uma nova atualização de cliente do Office 365 para o Office conteúdo entrega de rede (CDN), o Microsoft publica também um pacote de atualização para Windows Server Update Services (WSUS). Depois do Gestor de configuração sincroniza a atualização de cliente do Office 365 a partir do catálogo WSUS ao servidor do site, a atualização está disponível para implementação em clientes.

A partir na versão 1702, pode iniciar o instalador do Office 365 a partir do dashboard de gestão de clientes do Office 365 para efetuar a inicial do Office 365 App experiência mais fácil de instalar. O assistente permite-lhe configurar definições de instalação do Office 365, transferem ficheiros a partir de redes de entrega de conteúdo do Office (CDNs) e criar e implementar uma aplicação de scripts com o conteúdo.

## <a name="office-365-client-management-dashboard"></a>Dashboard de gestão de clientes do Office 365  
O dashboard de gestão de clientes do Office 365 a partir do Configuration Manager versão 1610, está disponível na consola do Configuration Manager. Para ver o dashboard, aceda a **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**.

O dashboard apresenta gráficos para os seguintes:

- Número de clientes do Office 365
- Versões de cliente do Office 365
- Idiomas de cliente do Office 365
- Canais de cliente do Office 365     
Para obter mais informações, consulte o artigo [canais de consumo de descrição geral da atualização para o Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

Na parte superior do dashboard, utilize o **coleção** definição de lista pendente para filtrar os dados de dashboard por membros de uma coleção específica.

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>Apresentar dados no dashboard de gestão de clientes do Office 365
Os dados que são apresentados no dashboard de gestão de clientes do Office 365 vem a partir do inventário de hardware. Inventário de hardware tem de estar ativado e tem de selecionar o **Office 365 ProPlus configurações** classe de inventário de hardware antes de dados são apresentados no painel de controlo.
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>Para apresentar os dados no dashboard de gestão de clientes do Office 365
1. Ative inventário de hardware, se ainda não estiver ativada. Para obter mais detalhes, consulte o artigo [configurar inventário de hardware](\sccm\core\clients\manage\configure-hardware-inventory).
2. Na consola do Configuration Manager, navegue para **administração** > **definições de cliente** > **predefinições de cliente**.  
3. No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  
4. Na caixa de diálogo **Predefinições de Cliente** , clique em **Inventário de Hardware**.  
5. Na lista **Definições do Dispositivo** , clique em **Definir Classes**.  
6. No **Classes de inventário de Hardware** caixa de diálogo, selecione **Office 365 ProPlus configurações**.  
7.  Clique em **OK** para guardar as suas alterações e fechar a caixa de diálogo **Classes de Inventário de Hardware** .  
O dashboard de gestão de clientes do Office 365 será iniciada apresentando os dados de inventário de hardware é comunicado.

## <a name="deploy-office-365-updates-with-configuration-manager"></a>Implementar atualizações do Office 365 com o Configuration Manager
Utilize os seguintes passos para implementar atualizações do Office 365 com o Configuration Manager:

1.  [Verifique se os requisitos](https://technet.microsoft.com/library/mt628083.aspx) para utilizar o Configuration Manager para gerir atualizações de cliente do Office 365 no **requisitos para utilizar o Configuration Manager para gerir atualizações de cliente do Office 365** secção do tópico.  

2.  [Configurar pontos de atualização de software](../get-started/configure-classifications-and-products.md) para sincronizar o cliente do Office 365 de atualizações. Definir **atualizações** para a classificação e selecione **cliente do Office 365** do produto. Poderá ter de sincronizar atualizações de software, pelo menos, uma vez antes do produto de cliente do Office 365 está disponível para a escolha. Tem de sincronizar as atualizações de software depois de configurar os pontos de atualização de software para utilizar o **atualizações** classificação.
3.  Permitir que os clientes do Office 365 receber atualizações do Configuration Manager. Pode fazê-lo através da utilização de definições de cliente do Configuration Manager ou utilizar a política de grupo. Utilize um dos seguintes métodos para ativar o cliente:  
    - Método 1: A partir do Configuration Manager versão 1606, pode utilizar a definição para gerir o agente de cliente do Office 365 do cliente do Configuration Manager. Depois de configurar esta definição e implementar atualizações do Office 365, o agente do cliente do Configuration Manager comunica com o agente de cliente do Office 365 para transferir atualizações do Office 365 a partir de um ponto de distribuição e instalá-los. O Configuration Manager demora inventário definições do Office 365 ProPlus cliente.
      1.  Na consola do Configuration Manager, clique em **administração** > **descrição geral** > **definições de cliente**.  

      2.  Abra as definições de dispositivo adequados para ativar o agente de cliente. Para mais informações sobre predefinida e definições personalizadas de cliente, consulte o artigo [como configurar as definições de cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Clique em **atualizações de Software** e selecione **Sim** para o **ativar a gestão do agente de cliente do Office 365** definição.  

    - Método 2: [Permitir que os clientes do Office 365 receber atualizações](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient) do Configuration Manager utilizando a ferramenta de implementação do Office ou a política de grupo.  

4. [Implementar as atualizações do Office 365](deploy-software-updates.md) aos clientes.   

> [!Important]
> Quando tiver um cliente do Office 365 com mais de um idioma e transferir atualizações para menos de idiomas, as atualizações falhará instalar. Por exemplo, digamos que tem um cliente do Office 365 com en-nos e pt-pt. No servidor do site, pode transferir e implementar apenas en-nos de conteúdo para uma atualização do Office 365 aplicável. Quando o utilizador inicia a instalação para esta atualização a partir do Centro de Software, a atualização irá bloquear ao transferir o conteúdo. Tem de transferir e implementar atualizações dos mesmos idiomas de que os clientes do Office 365.  


## <a name="add-other-languages-for-office-365-update-downloads"></a>Adicionar que transferências de atualização de outros idiomas para o Office 365
A partir do Configuration Manager versão 1610, pode adicionar suporte para o Configuration Manager para transferir atualizações para os idiomas suportados pelo Office 365, independentemente de se são suportados no Configuration Manager.
> [!IMPORTANT]  
> A configuração de outros idiomas de atualização do Office 365 é uma definição ao nível do site. Depois de adicionar os idiomas ao utilizar o procedimento seguinte, todas as atualizações do Office 365 serão transferidas os idiomas selecionados, bem como os idiomas que selecionou na página seleção de idioma nos assistentes para transferir atualizações de Software ou implementar atualizações de Software.

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>Para adicionar suporte para transferir atualizações para outros idiomas
Utilize o procedimento seguinte no site de administração central ou site primário autónomo, onde a função de sistema de sites de ponto de atualização de software está instalada.
1. A partir de uma linha de comandos, escreva *wbemtest* como um utilizador administrativo para abrir o recurso de teste do Windows Management Instrumentation.
2. Clique em **ligar**e, em seguida, escreva *root\sms\site_&lt;siteCode&gt;*.
3. Clique em **consulta**, e, em seguida, execute a seguinte consulta: *selecione &#42; a partir do SMS_SCI_Component onde componentname = "SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![Consulta de WMI](..\media\1-wmiquery.png)
4. No painel de resultados, faça duplo clique no objeto com o código do site para o site de administração central ou site primário autónomo.
5. Selecione o **propriedades** propriedade, clique em **Editar propriedade**e, em seguida, clique em **vista incorporado**.
![Editor de propriedade](..\media\2-propeditor.png)
6. Começando no resultado da primeira consulta, abra a cada objeto até encontrar a **AdditionalUpdateLanguagesForO365** para o **PropertyName** propriedade.
7. Selecione **valor2** e clique em **Editar propriedade**.  
![Editar a propriedade de Value2](..\media\3-queryresult.png)
8. Adicionar outros idiomas para o **valor2** propriedade e clique em **guardar propriedade**.  
Por exemplo, pt-pt (para Português - Portugal), af-za (para Afrikaans - África do Sul), não nn (para norueguês (Nynorsk) - Noruega), etc.  
![Adicionar idiomas no Editor de propriedade](..\media\4-props.png)  
9. Clique em **fechar**, clique em **fechar**, clique em **guardar propriedade**, clique em **guardar objeto** (se clicar em **fechar** aqui os valores são eliminados), clique em **fechar**e, em seguida, clique em **sair** para saia do recurso de teste do Intstrumentation de gestão do Windows.
10. Na consola do Configuration Manager, aceda a **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365** > **atualizações do Office 365**.
11. Agora, quando são transferidas atualizações do Office 365, serão transferidas as atualizações no idioma que selecionou no assistente e os idiomas que tiver configurado neste procedimento. Certifique-se de que as atualizações transferido nesses idiomas, aceda à origem do pacote para a atualização e procurar ficheiros com o código de idioma no nome do ficheiro.  
![Nomes de ficheiros com outros idiomas](..\media\5-verification.png)


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Alterar o canal de atualização depois de ativar os clientes do Office 365 receber atualizações do Configuration Manager
Para alterar o canal de atualização depois de ativar os clientes do Office 365 receber atualizações do Configuration Manager, pode utilizar a política de grupo para distribuir uma alteração de valor da chave de registo para clientes do Office 365. Alterar o **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** chave de registo para utilizar um dos seguintes valores:

- Canal de atual:  
  **CDNBaseUrl** = http &#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Canal diferida:  
  **CDNBaseUrl** = http &#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- Lançamento para o canal de atual:  
  **CDNBaseUrl** = http &#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- Lançamento para o canal diferida:  
  **CDNBaseUrl** = http &#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf

## <a name="deploy-office-365-apps"></a>Implementar aplicações do Office 365  
A partir na versão 1702, pode iniciar o instalador do Office 365 a partir do dashboard de gestão de clientes do Office 365 para efetuar a instalação inicial do Office 365 App experiência mais fácil. O assistente permite-lhe configurar definições de instalação do Office 365, transferir ficheiros de conteúdo entrega redes (CDNs) e criar e implementar uma aplicação de scripts para os ficheiros.

Isto é especialmente útil porque as atualizações do Office 365 não são aplicáveis para clientes sem o Office 365 instalado. Antes de versão 1702, para instalar aplicações do Office 365 pela primeira vez em clientes, seria necessário transferir o Office 365 implementação ferramenta (ODT) e os ficheiros de origem de instalação Office 365, incluindo todos os pacotes de idiomas que necessita, manualmente e gerar o Configuration.xml que especifica a versão correta do Office e o canal. Em seguida, seria necessário criar e implementar um pacote de legado ou uma aplicação de scripts para os clientes instalam as aplicações do Office 365.

> [!NOTE]
> - O computador que executa o programa de instalação do Office 365 tem de ter acesso à Internet.  
> - O utilizador que executa o programa de instalação do Office 365 tem de ter **leitura** e **escrever** acesso à partilha de localização de conteúdo é fornecido no assistente.
> - Se receber um erro 404 de transferências, copie os seguintes ficheiros para a pasta % temp % do utilizador:
>    - [releasehistory.XML](http://officecdn.microsoft.com.edgesuite.net/wsus/releasehistory.cab)
>    - [o365client_32bit.XML](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  
> - Depois de criar e implementar aplicações do Office 365 utilizando o instalador do Office 365, o Configuration Manager não gerir as atualizações do Office por predefinição. Para permitir que os clientes do Office 365 receber atualizações do Configuration Manager, consulte o artigo [atualizações de implementar o Office 365 com o Configuration Manager](#deploy-office-365-updates-with-configuration-manager).

### <a name="to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard"></a>Para implementar aplicações do Office 365 para clientes a partir do dashboard de gestão de clientes do Office 365
1. Na consola do Configuration Manager, navegue para **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**.
2. Clique em **instalador do Office 365** no painel do canto superior direito. É aberto o Assistente de instalação de cliente do Office 365.
3. No **definições da aplicação** página, forneça um nome e descrição para a aplicação, introduza a localização de transferência para os ficheiros e, em seguida, clique em **seguinte**. Tenha em atenção que a localização tem de ser especificada o formulário &#92; &#92; *server*&#92; *partilhar*.
4. No **importar definições de cliente** página, selecione se pretende importar as definições de cliente do Office 365 a partir de um ficheiro de configuração XML existente ou especifique manualmente as definições e, em seguida, clique em **seguinte**.  

    Quando tiver um ficheiro de configuração existente, introduza a localização para o ficheiro e avance para o passo 7. Tenha em atenção que a localização tem de ser especificada o formulário &#92; &#92; *server*&#92; *partilhar*&#92;* nome de ficheiro*. XML.
5. No **cliente produtos** página, selecione o Office 365 conjunto de aplicações que utilizam, selecione as aplicações que pretende incluir, selecione os produtos Office adicionais que devem ser incluídos e, em seguida, clique em **seguinte**.
6. No **definições de cliente** página, selecione as definições para incluir e, em seguida, clique em **seguinte**.
7. No **implementação** página, escolha se pretende implementar a aplicação e, em seguida, clique em **seguinte**.  
Se optar por não implementar o pacote no assistente, avance para o passo 9.
8. Configure o resto das páginas do assistente, tal como faria para uma implementação de aplicação normal. Para obter mais detalhes, consulte o artigo [criar e implementar uma aplicação](/sccm/apps/get-started/create-and-deploy-an-application).
9. Conclua o assistente.
10. Pode implementar ou editar a aplicação, tal como faria com qualquer outra aplicação no Configuration Manager a partir de **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **aplicações**.   

> [!IMPORTANT]
> A aplicação do Office 365 que criar e implementar utilizando o Assistente de aplicação do Office 365 no Configuration Manager não é automaticamente gerida pelo Configuration Manager até ativar o **ativar a gestão do cliente de 365 do Office novamente** definição de agente de cliente de atualizações de software. Para obter mais detalhes, consulte o artigo [sobre definições de cliente](/sccm/core/clients/deploy/about-client-settings).

>[!NOTE]
>Depois de implementar aplicações do Office 365, pode criar regras de implementação automática para manter as aplicações. Para criar uma regra de implementação automática para aplicações do Office 365, clique em **criar um ADR** a partir do dashboard de gestão de clientes do Office 365 e selecione **cliente do Office 365** quando escolher o produto. Para obter mais informações, consulte o artigo [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates).

<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->


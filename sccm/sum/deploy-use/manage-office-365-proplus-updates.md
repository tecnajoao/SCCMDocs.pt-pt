---
title: "Gerenciar atualizações do Office 365 ProPlus | Microsoft Docs"
description: "Gerenciador de configuração sincroniza atualizações de cliente do Office 365 do catálogo do WSUS para o servidor do site para fazer as atualizações disponíveis para implantar em clientes."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 05/31/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.translationtype: MT
ms.sourcegitcommit: a986c23b18f782b713d7df0048dff2543f640b66
ms.openlocfilehash: eb2f9ff61b68e015182a1f898afcb2a528b410ba
ms.contentlocale: pt-pt
ms.lasthandoff: 07/12/2017

---

# Gerenciar o Office 365 ProPlus com o Configuration Manager
<a id="manage-office-365-proplus-with-configuration-manager" class="xliff"></a>

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

O Configuration Manager permite-lhe gerir aplicações do Office 365 ProPlus das seguintes formas:

- [Dashboard de gestão de clientes do Office 365](#office-365-client-management-dashboard): A partir do Configuration Manager versão 1610, você pode examinar informações de cliente do Office 365 do painel de gerenciamento de cliente do Office 365.    

- [Implementar aplicações do Office 365](#deploy-office-365-apps): Começando na versão 1702, você pode iniciar o instalador do Office 365 do painel Gerenciamento de cliente do Office 365 para tornar a instalação inicial do aplicativo do Office 365 a experiência mais fácil. O assistente permite que você definir as configurações de instalação do Office 365, baixe arquivos de redes de fornecimento de conteúdo do Office CDNs () e criar e implantar um aplicativo de script com o conteúdo.    

- [Implementar atualizações do Office 365](#deploy-office-365-updates): A partir do Configuration Manager versão 1602, pode gerir atualizações de cliente do Office 365, utilizando o fluxo de trabalho de gestão de atualização de software. Quando a Microsoft publica uma nova atualização de cliente do Office 365 para o Office Content Delivery Network (CDN), o Microsoft também publica um pacote de atualização para o Windows Server Update Services (WSUS). Após a atualização do cliente Office 365 do catálogo do WSUS no servidor de site do Configuration Manager é sincronizada, a atualização está disponível para implantar em clientes.    

- [Adicionar atualizações de idiomas para o Office 365 transferências](#add-languages-for-office-365-update-downloads): A partir do Configuration Manager versão 1610, pode adicionar suporte para o Configuration Manager para transferir atualizações para os idiomas suportados pelo Office 365, independentemente se são suportados no Configuration Manager.  

- [Alterar o canal de atualização](#change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager): Pode utilizar a política de grupo para distribuir uma alteração de valor de chave de registo para clientes do Office 365 para alterar o canal de atualização.


## Painel de gerenciamento de clientes do Office 365
<a id="office-365-client-management-dashboard" class="xliff"></a>  
O dashboard de gestão de clientes do Office 365 fornece gráficos para as seguintes informações:

- Número de clientes do Office 365
- Versões de cliente do Office 365
- Idiomas do cliente Office 365
- Canais de cliente do Office 365     
  Para obter mais informações, consulte [canais de visão geral da atualização para o Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).

Para ver o dashboard de gestão de clientes do Office 365 na consola do Configuration Manager, aceda a **biblioteca de Software** > **descrição geral** > **gestão de clientes do Office 365**. Na parte superior do painel de controle, use o **coleção** configuração da lista suspensa para filtrar os dados do dashboard por membros de uma coleção específica.

### Exibir dados no painel de gerenciamento de cliente do Office 365
<a id="display-data-in-the-office-365-client-management-dashboard" class="xliff"></a>
Os dados que são exibidos no painel de gerenciamento de cliente do Office 365 vêm de inventário de hardware. Tem de ativar o inventário de hardware e selecione o **Office 365 ProPlus configurações** apresenta de classe de inventário de hardware antes de dados no dashboard.
#### Para exibir dados no painel de gerenciamento de cliente do Office 365
<a id="to-display-data-in-the-office-365-client-management-dashboard" class="xliff"></a>
1. Habilite inventário de hardware, se ainda não estiver habilitado. Para obter detalhes, consulte [configurar o inventário de hardware](\sccm\core\clients\manage\configure-hardware-inventory).
2. No console do Configuration Manager, navegue até **administração** > **configurações do cliente** > **configurações do cliente padrão**.  
3. No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  
4. Na caixa de diálogo **Predefinições de Cliente** , clique em **Inventário de Hardware**.  
5. Na lista **Definições do Dispositivo** , clique em **Definir Classes**.  
6. No **Classes de inventário de Hardware** caixa de diálogo, selecione **Office 365 ProPlus configurações**.  
7.  Clique em **OK** para guardar as suas alterações e fechar a caixa de diálogo **Classes de Inventário de Hardware** .  
O dashboard de gestão de clientes do Office 365 inicia a apresentar dados como o inventário de hardware é comunicado.

## Implantar aplicativos do Office 365
<a id="deploy-office-365-apps" class="xliff"></a>  
A partir da versão 1702, inicie o instalador do Office 365 a partir do dashboard de gestão de clientes do Office 365 para a instalação inicial da aplicação do Office 365. O assistente permite que você definir as configurações de instalação do Office 365, baixar arquivos do Office conteúdo entrega CDNs (redes) e criar e implantar um aplicativo de script para os arquivos. Até que seja instalada do Office 365 nos clientes, atualizações do Office 365 não são aplicáveis.

Para versões anteriores do Configuration Manager, tem de efetuar os seguintes passos para instalar aplicações do Office 365 pela primeira vez em clientes:
- Transferir a ferramenta de implementação do Office 365 (ODT)
- Transfira os ficheiros de origem de instalação do Office 365, incluindo todos os pacotes de idiomas que precisa.
- Gere Configuration.xml que especifica a versão correta do Office e o canal.
- Criar e implementar um pacote de legado ou uma aplicação de scripts para os clientes instalam as aplicações do Office 365.

### Requisitos
<a id="requirements" class="xliff"></a>
- O computador que executa o instalador do Office 365 deve ter acesso à Internet.  
- O usuário que executa o instalador do Office 365 deve ter **leitura** e **gravar** acesso ao compartilhamento de conteúdo local é fornecido no assistente.
- Se você receber um erro 404 download, copie os seguintes arquivos para a pasta % temp % do usuário:
  - [releasehistory.XML](http://officecdn.microsoft.com.edgesuite.net/wsus/releasehistory.cab)
  - [o365client_32bit.XML](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  


### Para implantar aplicativos do Office 365 em clientes do painel de gerenciamento de cliente do Office 365
<a id="to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard" class="xliff"></a>
1. No console do Configuration Manager, navegue até **biblioteca de Software** > **visão geral** > **gerenciamento de cliente do Office 365**.
2. Clique em **instalador do Office 365** no painel superior direito. Abre o Assistente de instalação de cliente do Office 365.
3. Sobre o **configurações do aplicativo** página, forneça um nome e uma descrição para o aplicativo, insira o local de download para os arquivos e, em seguida, clique em **próximo**. A localização tem de ser especificada como &#92; &#92; *server*&#92; *partilhar*.
4. Sobre o **importar configurações do cliente** página, escolha se deseja importar as configurações de cliente do Office 365 de um arquivo de configuração XML existente ou especifique manualmente as configurações e, em seguida, clique em **próximo**.  

    Quando você tiver um arquivo de configuração existente, digite o local para o arquivo e vá para a etapa 7. Observe que o local deve ser especificado no formato #92; & #92. *server*&#92; *compartilhar*&#92; *nome do arquivo*. XML.
    > [!IMPORTANT]    
    > O arquivo de configuração XML deve conter apenas [idiomas com suporte pelo cliente do Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx).

5. Sobre o **produtos de cliente** página, selecione o Office 365 suite que você usa, selecione os aplicativos que você deseja incluir, selecione qualquer produtos Office adicionais que devem ser incluídos e, em seguida, clique em **próximo**.
6. Sobre o **configurações do cliente** página, escolha as configurações para incluir e, em seguida, clique em **próximo**.
7. Sobre o **implantação** página, escolha se deseja implantar o aplicativo e, em seguida, clique em **próximo**.  
Se você optar por não implantar o pacote no assistente, vá para a etapa 9.
8. Configure o restante das páginas do assistente que você usaria para uma implantação de aplicativo típico. Para obter detalhes, consulte [criar e implantar um aplicativo](/sccm/apps/get-started/create-and-deploy-an-application).
9. Conclua o assistente.
10. Pode implementar ou editar a aplicação do **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **aplicações**.    

Depois de criar e implantar aplicativos do Office 365 usando o instalador do Office 365, o Configuration Manager não gerenciará as atualizações do Office por padrão. Para habilitar os clientes do Office 365 receber atualizações do Configuration Manager, consulte [atualizações de implantar o Office 365 com o Configuration Manager](#deploy-office-365-updates-with-configuration-manager).

>[!NOTE]
>Depois de implantar aplicativos do Office 365, você pode criar regras de implantação automática para manter os aplicativos. Para criar uma regra de implantação automática para aplicativos do Office 365, clique em **criar uma ADR** no painel de gerenciamento de cliente do Office 365 e selecione **cliente do Office 365** quando você escolhe o produto. Para obter mais informações, consulte [implantar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates).


## Implementar atualizações do Office 365
<a id="deploy-office-365-updates" class="xliff"></a>
Use as etapas a seguir para implantar atualizações do Office 365 com o Configuration Manager:

1.  [Verifique os requisitos de](https://technet.microsoft.com/library/mt628083.aspx) para usar o Configuration Manager para gerenciar atualizações do cliente Office 365 no **requisitos para usar o Configuration Manager para gerenciar atualizações do cliente Office 365** seção do tópico.  

2.  [Configurar pontos de atualização de software](../get-started/configure-classifications-and-products.md) para sincronizar o cliente do Office 365 atualizações. Definir **atualizações** para a classificação e selecione **cliente do Office 365** para o produto. Sincronizar atualizações de software, depois de configurar os pontos de atualização de software para utilizar o **atualizações** classificação.
3.  Permitir que os clientes do Office 365 receber atualizações do Configuration Manager. Pode fazê-lo utilizando a política de grupo ou definições de cliente do Configuration Manager. Use um dos métodos a seguir para habilitar o cliente:   

    **Método 1**: A partir da versão 1606 do Configuration Manager, você pode usar a configuração para gerenciar o agente de cliente do Office 365 do cliente do Configuration Manager. Depois que você definir essa configuração e implantar atualizações do Office 365, o agente de cliente do Configuration Manager se comunica com o agente de cliente do Office 365 para baixar atualizações do Office 365 de um ponto de distribuição e instalá-los. Configuration Manager faz um inventário das configurações de cliente do Office 365 ProPlus.    

      1.  No console do Configuration Manager, clique em **administração** > **visão geral** > **configurações do cliente**.  

      2.  Abra as configurações de dispositivo apropriados para habilitar o agente cliente. Para obter mais informações sobre o padrão e configurações personalizadas do cliente, consulte [como definir as configurações de cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Clique em **atualizações de Software** e selecione **Sim** para o **habilitar o gerenciamento do agente de cliente do Office 365** configuração.  

    **Método 2**: [Ativar clientes do Office 365 receber atualizações](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient) do Configuration Manager utilizando a ferramenta de implementação do Office ou a política de grupo.  

4. [Implantar as atualizações do Office 365](deploy-software-updates.md) aos clientes.   

> [!Important]
> Tem de transferir e implementar atualizações nos idiomas mesmos configurados nos clientes do Office 365. Por exemplo, vamos supor que tem um cliente do Office 365 configurado com o en-us e Alemanha Alemanha idiomas. No servidor do site, transferir e implementar apenas en-us de conteúdo para uma atualização do Office 365 aplicável. Quando o utilizador inicia a instalação a partir do Centro de Software para esta atualização, a atualização, esta bloqueará ao transferir o conteúdo.   

## Adicionar idiomas para as transferências de atualização do Office 365
<a id="add-languages-for-office-365-update-downloads" class="xliff"></a>
A partir do Configuration Manager versão 1610, pode adicionar suporte para o Configuration Manager para transferir atualizações para os idiomas suportados pelo Office 365, independentemente se são suportados no Configuration Manager.    

> [!IMPORTANT]  
> Configurar outros idiomas de atualização do Office 365 é uma configuração de todo o site. Depois de adicionar os idiomas utilizando o procedimento seguinte, todas as atualizações do Office 365 são transferidas os idiomas selecionados, bem como os idiomas que selecionou no **seleção de idioma** página nos assistentes para transferir atualizações de Software ou implementar as atualizações de Software.

### Para adicionar suporte para baixar atualizações para outros idiomas
<a id="to-add-support-to-download-updates-for-additional-languages" class="xliff"></a>
Utilize o procedimento seguinte no ponto de atualização de software no site de administração central ou site primário autónomo.
1. Em um prompt de comando, digite *wbemtest* como um usuário administrativo para abrir o Testador de instrumentação de gerenciamento do Windows.
2. Clique em **conectar**e, em seguida, digite *root\sms\site_&lt;siteCode&gt;*.
3. Clique em **consulta**, e, em seguida, execute a seguinte consulta: *select &#42; de SMS_SCI_Component onde componentname = "SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![Consulta WMI](..\media\1-wmiquery.png)
4. No painel de resultados, clique duas vezes o objeto com o código do site para o site de administração central ou site primário autônomo.
5. Selecione o **Props** propriedade, clique em **Editar propriedade**e, em seguida, clique em **exibição inserido**.
![Editor de propriedades](..\media\2-propeditor.png)
6. Começando no resultado da consulta primeiro, abra cada objeto até encontrar uma **AdditionalUpdateLanguagesForO365** para o **PropertyName** propriedade.
7. Selecione **Value2** e clique em **Editar propriedade**.  
![Editar a propriedade Value2](..\media\3-queryresult.png)
8. Adicionar idiomas adicionais para o **Value2** propriedade e clique em **Salvar propriedade**.  
Por exemplo, pt-pt (para português - Portugal), af-za (para africâner - África do Sul), não nn (para Norueguês (Nynorsk) - Noruega), etc.  
![Adicionar idiomas no Editor de propriedade](..\media\4-props.png)  
9. Clique em **fechar**, clique em **fechar**, clique em **guardar propriedade**, clique em **guardar objeto** (se clicar em **fechar** aqui os valores são eliminados), clique em **fechar**e, em seguida, clique em **sair** para sair do recurso de teste do Windows Management Instrumentation.
10. No console do Configuration Manager, vá para **biblioteca de Software** > **visão geral** > **gerenciamento de cliente do Office 365** > **atualizações do Office 365**.
11. Agora quando transferir atualizações do Office 365, serão transferidas as atualizações nos idiomas de que seleciona no assistente e configurado neste procedimento. Para verificar se as atualizações de transferir nos idiomas corretos, avance para a origem do pacote para a atualização e procurarem ficheiros com o código de idioma no nome de ficheiro.  
![Nomes de arquivos com outros idiomas](..\media\5-verification.png)


## Alterar o canal de atualização depois de habilitar os clientes do Office 365 receber atualizações do Configuration Manager
<a id="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager" class="xliff"></a>
Para alterar o canal de atualização depois de ativar a clientes do Office 365 receber atualizações do Configuration Manager, utilize a política de grupo para distribuir uma alteração de valor de chave de registo para clientes do Office 365. Alterar o **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** chave do registro para usar um dos seguintes valores:

- O canal atual:  
  **CDNBaseUrl** = #58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60 & http

- Canal adiada:  
  **CDNBaseUrl** = #58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114 & http

- Primeira versão do canal atual:  
  **CDNBaseUrl** = #58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be & http

- Primeira versão do canal adiada:  
  **CDNBaseUrl** = #58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf & http



<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->


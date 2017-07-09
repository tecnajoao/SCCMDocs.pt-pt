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
ms.translationtype: Machine Translation
ms.sourcegitcommit: dc221ddf547c43ab1f25ff83c3c9bb603297ece6
ms.openlocfilehash: 744bcb603a02bc7d237ffb3a7f925037b94a23ba
ms.contentlocale: pt-pt
ms.lasthandoff: 06/01/2017

---

# <a name="manage-office-365-proplus-with-configuration-manager"></a>Gerenciar o Office 365 ProPlus com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Configuration Manager sincroniza as atualizações do cliente Office 365 e os disponibiliza implantar em clientes com o Office 365 instalado. A partir do Configuration Manager versão 1610, você pode examinar informações de cliente do Office 365 do painel de gerenciamento de cliente do Office 365.

A partir do Configuration Manager versão 1602, o Configuration Manager tem a capacidade de gerenciar atualizações do cliente Office 365 usando o fluxo de trabalho de gerenciamento de atualização de software. Quando a Microsoft publica uma nova atualização de cliente do Office 365 para o Office Content Delivery Network (CDN), o Microsoft também publica um pacote de atualização para o Windows Server Update Services (WSUS). Após a atualização do cliente Office 365 do catálogo do WSUS no servidor de site do Configuration Manager é sincronizada, a atualização está disponível para implantar em clientes.

Começando na versão 1702, você pode iniciar o instalador do Office 365 do painel Gerenciamento de cliente do Office 365 para fazer com que o Office 365 App inicial mais fácil de experiência de instalação. O assistente permite que você definir as configurações de instalação do Office 365, baixe arquivos de redes de fornecimento de conteúdo do Office CDNs () e criar e implantar um aplicativo de script com o conteúdo.

## <a name="office-365-client-management-dashboard"></a>Painel de gerenciamento de clientes do Office 365  
A partir do Configuration Manager versão 1610, o painel de gerenciamento de cliente do Office 365 está disponível no console do Configuration Manager. Para exibir o painel de controle, vá para **biblioteca de Software** > **visão geral** > **gerenciamento de cliente do Office 365**.

O painel exibe gráficos para o seguinte:

- Número de clientes do Office 365
- Versões de cliente do Office 365
- Idiomas do cliente Office 365
- Canais de cliente do Office 365     
Para obter mais informações, consulte [canais de visão geral da atualização para o Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

Na parte superior do painel de controle, use o **coleção** configuração da lista suspensa para filtrar os dados do dashboard por membros de uma coleção específica.

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>Exibir dados no painel de gerenciamento de cliente do Office 365
Os dados que são exibidos no painel de gerenciamento de cliente do Office 365 vêm de inventário de hardware. Inventário de hardware deve ser habilitado e você deve selecionar o **Office 365 ProPlus configurações** classe de inventário de hardware antes de dados são exibidos no painel.
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>Para exibir dados no painel de gerenciamento de cliente do Office 365
1. Habilite inventário de hardware, se ainda não estiver habilitado. Para obter detalhes, consulte [configurar o inventário de hardware](\sccm\core\clients\manage\configure-hardware-inventory).
2. No console do Configuration Manager, navegue até **administração** > **configurações do cliente** > **configurações do cliente padrão**.  
3. No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  
4. Na caixa de diálogo **Predefinições de Cliente** , clique em **Inventário de Hardware**.  
5. Na lista **Definições do Dispositivo** , clique em **Definir Classes**.  
6. No **Classes de inventário de Hardware** caixa de diálogo, selecione **Office 365 ProPlus configurações**.  
7.  Clique em **OK** para guardar as suas alterações e fechar a caixa de diálogo **Classes de Inventário de Hardware** .  
O painel de gerenciamento de cliente do Office 365 começarão a exibir dados quando o inventário de hardware é reportado.

## <a name="deploy-office-365-updates-with-configuration-manager"></a>Implantar atualizações do Office 365 com o Configuration Manager
Use as etapas a seguir para implantar atualizações do Office 365 com o Configuration Manager:

1.  [Verifique os requisitos de](https://technet.microsoft.com/library/mt628083.aspx) para usar o Configuration Manager para gerenciar atualizações do cliente Office 365 no **requisitos para usar o Configuration Manager para gerenciar atualizações do cliente Office 365** seção do tópico.  

2.  [Configurar pontos de atualização de software](../get-started/configure-classifications-and-products.md) para sincronizar o cliente do Office 365 atualizações. Definir **atualizações** para a classificação e selecione **cliente do Office 365** para o produto. Talvez você precise sincronizar atualizações de software pelo menos uma vez antes do produto cliente do Office 365 está disponível para sua escolha. Você deve sincronizar as atualizações de software depois de configurar os pontos de atualização de software para usar o **atualizações** classificação.
3.  Permitir que os clientes do Office 365 receber atualizações do Configuration Manager. Você pode fazer isso usando as configurações de cliente do Configuration Manager ou usar a diretiva de grupo. Use um dos métodos a seguir para habilitar o cliente:  
    - Método 1: A partir da versão 1606 do Configuration Manager, você pode usar a configuração para gerenciar o agente de cliente do Office 365 do cliente do Configuration Manager. Depois que você definir essa configuração e implantar atualizações do Office 365, o agente de cliente do Configuration Manager se comunica com o agente de cliente do Office 365 para baixar atualizações do Office 365 de um ponto de distribuição e instalá-los. Configuration Manager faz um inventário das configurações de cliente do Office 365 ProPlus.
      1.  No console do Configuration Manager, clique em **administração** > **visão geral** > **configurações do cliente**.  

      2.  Abra as configurações de dispositivo apropriados para habilitar o agente cliente. Para obter mais informações sobre o padrão e configurações personalizadas do cliente, consulte [como definir as configurações de cliente no System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Clique em **atualizações de Software** e selecione **Sim** para o **habilitar o gerenciamento do agente de cliente do Office 365** configuração.  

    - Método 2: [Permitir que os clientes do Office 365 receber atualizações](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient) do Configuration Manager usando a ferramenta de implantação do Office ou a política de grupo.  

4. [Implantar as atualizações do Office 365](deploy-software-updates.md) aos clientes.   

> [!Important]
> Quando você tiver um cliente do Office 365 com mais de um idioma e baixar atualizações para menos idiomas, as atualizações não instalar. Por exemplo, digamos que você tenha um cliente do Office 365 com en-us e de-de. No servidor do site, você descarregue e implantar somente en-us de conteúdo para uma atualização do Office 365 aplicável. Quando o usuário inicia a instalação desta atualização no Centro de Software, a atualização parará ao baixar o conteúdo. Você deve baixar e implantar atualizações nos mesmos idiomas que os clientes do Office 365.  


## <a name="add-other-languages-for-office-365-update-downloads"></a>Adicione que outros idiomas para o Office 365 downloads de atualização
A partir do Configuration Manager versão 1610, você pode adicionar suporte para o Configuration Manager para baixar atualizações para qualquer idioma com suporte pelo Office 365, independentemente de se eles tiverem suporte no Configuration Manager.
> [!IMPORTANT]  
> Configurar outros idiomas de atualização do Office 365 é uma configuração de todo o site. Depois de adicionar os idiomas usando o procedimento a seguir, todas as atualizações do Office 365 serão baixadas nesses idiomas, bem como os idiomas que você selecionar na página seleção de idioma nos assistentes para baixar atualizações de Software ou implantar atualizações de Software.

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>Para adicionar suporte para baixar atualizações para outros idiomas
Use o procedimento a seguir no site de administração central ou site primário autônomo, onde a função do sistema de site do ponto de atualização de software está instalada.
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
9. Clique em **fechar**, clique em **fechar**, clique em **Salvar propriedade**, clique em **Salvar objeto** (se você clicar em **fechar** aqui os valores são descartados), clique em **fechar**e, em seguida, clique em **sair** para saia do Testador de Intstrumentation de gerenciamento do Windows.
10. No console do Configuration Manager, vá para **biblioteca de Software** > **visão geral** > **gerenciamento de cliente do Office 365** > **atualizações do Office 365**.
11. Agora, quando você baixar as atualizações do Office 365, as atualizações serão baixadas no idioma que você seleciona no assistente e os idiomas que você configurou neste procedimento. Para verificar se as atualizações baixadas nesses idiomas, vá para a origem do pacote para a atualização e procure por arquivos com o código de idioma no nome de arquivo.  
![Nomes de arquivos com outros idiomas](..\media\5-verification.png)


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Alterar o canal de atualização depois de habilitar os clientes do Office 365 receber atualizações do Configuration Manager
Para alterar o canal de atualização depois de habilitar os clientes do Office 365 receber atualizações do Configuration Manager, você pode usar a diretiva de grupo para distribuir uma alteração de valor de chave do registro para os clientes do Office 365. Alterar o **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** chave do registro para usar um dos seguintes valores:

- O canal atual:  
  **CDNBaseUrl** = #58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60 & http

- Canal adiada:  
  **CDNBaseUrl** = #58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114 & http

- Primeira versão do canal atual:  
  **CDNBaseUrl** = #58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be & http

- Primeira versão do canal adiada:  
  **CDNBaseUrl** = #58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf & http

## <a name="deploy-office-365-apps"></a>Implantar aplicativos do Office 365  
Começando na versão 1702, você pode iniciar o instalador do Office 365 do painel Gerenciamento de cliente do Office 365 para tornar a instalação inicial do aplicativo do Office 365 a experiência mais fácil. O assistente permite que você definir as configurações de instalação do Office 365, baixar arquivos do Office conteúdo entrega CDNs (redes) e criar e implantar um aplicativo de script para os arquivos.

Isso é especialmente útil porque as atualizações do Office 365 não são aplicáveis para clientes sem instalado do Office 365. Antes da versão 1702, para instalar aplicativos do Office 365 pela primeira vez em clientes, você precisa baixar o Office 365 Deployment Tool (ODT) e os arquivos de origem de instalação do Office 365, incluindo todos os pacotes de idiomas que você precisa, e gerar o Configuration.xml que especifica a versão correta do Office e o canal manualmente. Em seguida, você precisa criar e implantar um pacote herdado ou um aplicativo de script para os clientes instalam os aplicativos do Office 365.

> [!NOTE]
> - O computador que executa o instalador do Office 365 deve ter acesso à Internet.  
> - O usuário que executa o instalador do Office 365 deve ter **leitura** e **gravar** acesso ao compartilhamento de conteúdo local é fornecido no assistente.
> - Se você receber um erro 404 download, copie os seguintes arquivos para a pasta % temp % do usuário:
>    - [releasehistory.XML](http://officecdn.microsoft.com.edgesuite.net/wsus/releasehistory.cab)
>    - [o365client_32bit.XML](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  
> - Depois de criar e implantar aplicativos do Office 365 usando o instalador do Office 365, o Configuration Manager não gerenciará as atualizações do Office por padrão. Para habilitar os clientes do Office 365 receber atualizações do Configuration Manager, consulte [atualizações de implantar o Office 365 com o Configuration Manager](#deploy-office-365-updates-with-configuration-manager).

### <a name="to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard"></a>Para implantar aplicativos do Office 365 em clientes do painel de gerenciamento de cliente do Office 365
1. No console do Configuration Manager, navegue até **biblioteca de Software** > **visão geral** > **gerenciamento de cliente do Office 365**.
2. Clique em **instalador do Office 365** no painel superior direito. Abre o Assistente de instalação de cliente do Office 365.
3. Sobre o **configurações do aplicativo** página, forneça um nome e uma descrição para o aplicativo, insira o local de download para os arquivos e, em seguida, clique em **próximo**. Observe que o local deve ser especificado no formato #92; & #92. *server*&#92; *compartilhar*.
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
10. Você pode implantar ou editar o aplicativo como faria com qualquer outro aplicativo no Configuration Manager do **biblioteca de Software** > **visão geral** > **gerenciamento de aplicativos** > **aplicativos**.   

> [!IMPORTANT]
> O aplicativo do Office 365 que você criar e implanta usando o Assistente de aplicativo do Office 365 no Configuration Manager não é automaticamente gerenciado pelo Configuration Manager até que você habilite o **habilitar o gerenciamento do agente de cliente do Office 365** configuração de agente do cliente de atualizações de software. Para obter detalhes, consulte [sobre configurações do cliente](/sccm/core/clients/deploy/about-client-settings).

>[!NOTE]
>Depois de implantar aplicativos do Office 365, você pode criar regras de implantação automática para manter os aplicativos. Para criar uma regra de implantação automática para aplicativos do Office 365, clique em **criar uma ADR** no painel de gerenciamento de cliente do Office 365 e selecione **cliente do Office 365** quando você escolhe o produto. Para obter mais informações, consulte [implantar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates).

<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->


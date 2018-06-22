---
title: Nova versão 1702
titleSuffix: Configuration Manager
description: Obter informações sobre as alterações e novas funcionalidades introduzidas na versão 1702 do System Center Configuration Manager.
ms.date: 05/02/2017
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 99e5cf970a2b4e1afa1a52d49be3afcc8c9d13fc
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32343057"
---
# <a name="what39s-new-in-version-1702-of-system-center-configuration-manager"></a>O que&#39;s novidade na versão 1702 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Atualize 1702 para o ramo atual do System Center Configuration Manager está disponível como uma atualização na consola para sites anteriormente instalados com a versão 1602, 1606 ou 1610. Também está disponível como uma versão de linha de base que pode utilizar ao instalar uma nova implementação.

> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de linha de base do Configuration Manager.  
>  Saiba mais sobre:    
>   - [Instalar novos sites](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Instalar atualizações em sites](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As secções seguintes fornecem detalhes sobre as alterações e novas funcionalidades introduzidas na versão 1702 do Configuration Manager.  

## <a name="deprecated-features-and-operating-systems"></a>Funcionalidades preteridas e sistemas operativos
Saiba mais sobre as alterações de suporte antes de são implementados no [removidas e preteridas itens](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

1702 remoções versão suportem para os seguintes produtos:
- **SQL Server 2008 R2**, para os servidores de base de dados do site. Descontinuação do suporte foi [anunciada pela primeira vez](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-support-for-sql-server-versions-as-a-site-database) no dia 10 de Julho de 2015. Esta versão do SQL Server continua a ser suportada quando utiliza uma versão do Configuration Manager antes da versão 1702.
- **Windows Server 2008 R2**para servidores do sistema de sites e a maioria das funções de sistema de sites. Descontinuação do suporte foi [anunciada pela primeira vez](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems) no dia 10 de Julho de 2015. Esta versão do Windows continua a ser suportada quando utiliza uma versão do Configuration Manager antes da versão 1702.  
- **Windows Server 2008**para servidores do sistema de sites e a maioria das funções de sistema de sites. Descontinuação do suporte foi [anunciada pela primeira vez](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems) no dia 10 de Julho de 2015.
- **Windows XP Embedded**, como um sistema operativo cliente. Descontinuação foi [anunciada pela primeira vez](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems) no dia 10 de Julho de 2015. Esta versão do Windows continua a ser suportada quando utiliza uma versão do Configuration Manager antes da versão 1702.




## <a name="site-infrastructure"></a>Infraestrutura de sites

### <a name="improvements-for-in-console-search"></a>Melhoramentos para pesquisa na consola
Seguem-se melhoramentos ao utilizar a procura na consola do Configuration Manager:
 - **Caminho do objeto:**  
  Muitos objetos suportam agora uma coluna chamada **caminho de objecto**.  Quando pesquisar e inclua esta coluna nos resultados a apresentar, pode ver o caminho para cada objeto. Por exemplo, se executar uma pesquisa de aplicações no nó de aplicações e também procura nodes secundárias, a *caminho de objecto* coluna no painel de resultados mostra o caminho para cada objeto que é devolvido.   

- **Preservação de texto de pesquisa:**  
  Quando introduzir o texto na caixa de texto de pesquisa e, em seguida, alternar entre a procurar nó secundárias e o nó atual, o texto que introduziu serão agora persistem e permanecem disponível para uma nova procura sem ter de reintroduzi-lo.

- **Preservação de sua decisão para procurar nodes secundárias:**  
 A opção que escolher para procurar o *atual nó* ou *todos os nós secundárias* agora persistir quando altera o nó que está a trabalhar. Este novo comportamento significa que não é necessário repor constantemente esta decisão como mover-se a consola. Por predefinição, quando abrir a consola, a opção é procurar apenas o nó atual.


### <a name="send-feedback-from-the-configuration-manager-console"></a>Enviar comentários a partir da consola do Configuration Manager

 Pode utilizar as opções de comentários na consola para enviar comentários diretamente para a equipa de desenvolvimento.

 Pode encontrar o **comentários** opção:
 -  No Friso, na extremidade esquerda do separador de início de cada nó.  
    ![Friso](./media/feedback-home.png)

 -  Quando lhe com o botão direito em qualquer objeto na consola do.   
     ![Opção de clique ecrãs](./media/feedback-option.png)   

 Escolher **comentários** abre o seu browser para o [Web site de comentários do UserVoice do Configuration Manager](https://go.microsoft.com/fwlink/?linkid=617029).


###  <a name="changes-for-updates-and-servicing"></a>Alterações para atualizações e manutenção
Seguem-se as alterações para atualizações e manutenção:

- **Localização do nó**   
  Depois de instalar a versão 1702, o **atualizações e manutenção** nó aparece como um nó de nível superior em **administração**. Já não se trata de um nó subordinado abaixo **serviços em nuvem**.

- **Novos Estados da atualização**  
  Ao ver as atualizações disponíveis na consola, existem dois novos Estados:  
  - **Disponível para instalação** -esta é uma atualização que foi transferido e pronto para instalar.
  - **Pronto para transferência** -esta atualização está disponível, mas não foi transferida. Pode optar por transferir esta atualização, mas foi substituída por uma atualização mais recente.


- **Opções de atualização mais simples**  
  Da próxima vez que qualificam da sua infraestrutura de dois ou mais atualizações, só a atualização mais recente é transferida. Por exemplo, se a versão atual do site é dois ou mais antiga que a versão mais recente está disponível, apenas esse mais recente versão de atualização é transferida automaticamente.  

  Pode optar por transferir e instalar as outras atualizações disponíveis, mesmo quando não estão a versão mais atual. Se transferir uma atualização mais antiga, receberá um aviso que a atualização foi substituída por uma mais recente. Para transferir uma atualização que é *disponível para transferência*, selecione a atualização na consola e, em seguida, clique em **transferir**.

- **Limpeza melhorada de atualizações anteriores**   
  Adicionámos uma função de limpeza automática, que elimina as transferências desnecessárias da pasta 'EasySetupPayload' no seu servidor do site. Porque esta é introduzida com a versão 1702, limpeza começa a funcionar depois de instalar uma atualização subsequente como um rollup de atualização ou a versão de atualização futura.  


### <a name="data-warehouse-service-point"></a>Ponto de serviço do armazém de dados
 Utilize o ponto de serviço do armazém de dados para armazenar e elaborar relatórios sobre dados históricos a longo prazo para a sua implementação do Configuration Manager.

 O armazém de dados suporta até 2 TB de dados, com carimbos de registo de alterações. Armazenamento de dados é conseguido ao sincronizações automáticas da base de dados do site do Configuration Manager para a base de dados do armazém de dados. Esta informação, em seguida, é acessível a partir do seu ponto de Reporting Services.

 Para obter mais informações, consulte [ponto de serviço do armazém de dados](/sccm/core/servers/manage/data-warehouse).


### <a name="peer-cache-improvements"></a>Melhorias da Cache ponto a ponto
 A partir da versão 1702, um computador de origem de cache ponto a ponto irão rejeitar um pedido para o conteúdo quando o computador de origem de cache ponto a ponto cumpre qualquer uma das seguintes condições:  
  -  Está no modo de bateria baixo.
  -  Carga da CPU excede 80% momento solicitados.
  -  E/s de disco tem um *AvgDiskQueueLength* excede que 10.
  -  Não existem ligações mais não disponíveis para o computador.   
Para obter mais informações, consulte **acesso a uma origem de cache ponto a ponto limitado** no [Cache ponto a ponto para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).   

Além disso, as três novos relatórios são adicionados para o ponto de Reporting Services. Pode utilizar estes relatórios para obter mais detalhes sobre pedidos de conteúdo rejeitados, incluindo o limite de grupo, o computador e o conteúdo foi envolvido de compreender. Consulte [monitorização](/sccm/core/plan-design/hierarchy/client-peer-cache#monitoring) no tópico de cache ponto a ponto.

### <a name="content-library-cleanup-tool"></a>Ferramenta de limpeza da biblioteca de conteúdos
 Utilize o [ferramenta de limpeza da biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) para remover o conteúdo dos pontos de distribuição quando esse conteúdo já não está associado uma aplicação.


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>Utilizar o conector do OMS com a nuvem do Azure Government
Pode utilizar o conector do OMS para ligar ao OMS Log Analytics na nuvem do Microsoft Azure Government. Isto requer a modificar um ficheiro de configuração antes de instalar o conector do OMS, para que o conector pode trabalhar com a nuvem do Governo dos EUA. Para obter mais informações, consulte [utilizar o conector do OMS com a nuvem do Azure Government](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig).

### <a name="software-update-points-are-added-to-boundary-groups"></a>Pontos de atualização de software são adicionados a grupos de limites
A partir da versão 1702, os clientes utilizam grupos de limites para localizar um novo ponto de atualização de software e de contingência e localizar uma nova atualização de software ponto, se os respetivos um atual já não está acessível. Pode adicionar pontos de atualização de individual software para diferentes grupos de limites para controlar quais os servidores de um cliente pode localizar. Para obter mais informações, consulte [pontos de atualização de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) no [configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) tópico.


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="new-compliance-settings-for-ios"></a>Novas definições de conformidade para iOS

Adicionámos muitas novas definições para dispositivos iOS para corresponderem às disponível com o Microsoft Intune.
Para obter uma lista de todas as definições disponíveis, consulte [criar itens de configuração para iOS e dispositivos Mac OS X geridos com o Intune](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client).


## <a name="application-management"></a>Gestão de Aplicações

### <a name="improved-support-for-windows-store-for-business-apps"></a>Suporte melhorado para a loja Windows para as aplicações da empresa

Agora pode implementar as aplicações licenciadas online da loja Windows para empresas para Windows 10 PCs que gere com o cliente do Configuration Manager.
Para obter mais informações, consulte [gerir aplicações da loja Windows para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

### <a name="check-for-running-executable-files-before-installing-an-application"></a>Verifique a existência de executar ficheiros executáveis antes de instalar uma aplicação

No **propriedades** , na caixa de diálogo de uma implementação de tipo de **instalar comportamento** separador, pode agora especificar um dos ficheiros executáveis mais que, se em execução, irão bloquear a instalação do tipo de implementação. O utilizador tem de fechar o ficheiro executável está em execução (ou pode ser fechada automaticamente para implementações com um objetivo necessário) antes da implementação tipo pode ser instalado.

Se a aplicação foi implementada como **disponível**e um utilizador final tenta instalar uma aplicação, será pedido para fechar a qualquer executáveis em execução, especificado antes de poderão avançar com a instalação.

Se a aplicação foi implementada como **necessário**e a opção **fechar automaticamente quaisquer executáveis em execução, especificado no separador de comportamento de instalação de caixa de diálogo de propriedades do tipo de implementação** é selecionado, verá uma caixa de diálogo que os informa de que executáveis que especificou são fechados automaticamente quando é atingido o prazo de instalação da aplicação.

### <a name="app-management-improvements-for-hybrid-mdm"></a>Melhorias de gestão de aplicações para MDM híbrida

- [Implementar aplicações iOS compradas em volume para coleções de dispositivos](#deploy-volume-purchased-ios-apps-to-device-collections)
- [Suporte para iOS Volume Purchase Program para as educação](#support-for-ios-volume-purchase-program-for-education)
- [Suporte para vários tokens do volume-purchase program](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>Implementação do sistema operativo

### <a name="expire-stand-alone-media"></a>Expirar suportes de dados autónomos
Quando cria suporte de dados autónomo, existem novas opções para definir opcionais datas de início e de expiração no suporte de dados. Estas definições estão desativadas por predefinição. As datas são em comparação com a hora do sistema no computador antes do suporte de dados autónomo é executado. Quando a hora do sistema é anterior à hora de início ou posterior à hora de expiração, o suporte de dados autónomo não foi iniciado. Estas opções também estão disponíveis utilizando o cmdlet New-CMStandaloneMedia PowerShell. Para obter mais informações, consulte [criar suportes de dados autónomos](/sccm/osd/deploy-use/create-stand-alone-media).

### <a name="package-id-displayed-in-task-sequence-steps"></a>ID de pacote apresentado nos passos de sequência de tarefas
Qualquer passo de sequência de tarefas que faça referência a um pacote, o pacote de controladores, a imagem do sistema operativo, a imagem de arranque ou o pacote de atualização do sistema operativo irá apresentar agora o ID de pacote do objeto referenciado. Quando um passo de sequência de tarefas faz referência a uma aplicação, apresentará o ID de objeto.

### <a name="support-for-additional-content-in-stand-alone-media"></a>Suporte para conteúdo adicional no suporte de dados autónomo
Conteúdo adicional é agora suportado no suporte de dados autónomo. Pode selecionar pacotes adicionais, pacotes de controladores e aplicações para testado no suporte de dados, juntamente com outros conteúdos referenciados na sequência de tarefas. Anteriormente, apenas os conteúdos referenciados na sequência de tarefas foi testado no suporte de dados autónomo. Para obter mais informações, consulte [criar suportes de dados autónomos](/sccm/osd/deploy-use/create-stand-alone-media).

### <a name="hardware-inventory-collects-uefi-information"></a>Inventário de hardware recolhe informações de UEFI
Uma nova classe de inventário de hardware (**SMS_Firmware**) e a propriedade (**UEFI**) estão disponíveis para o ajudar a determinar se um computador é iniciado no modo UEFI. Quando um computador for iniciado no modo UEFI, o **UEFI** propriedade está definida como **verdadeiro**. Esta opção estiver ativada no inventário de hardware por predefinição. Para obter mais informações sobre o inventário de hardware, consulte [como configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>Melhoramentos para mensagens de aviso do Centro de Software para sequências de tarefas de elevado impacto
Esta versão inclui os seguintes melhoramentos para mensagens de aviso do Centro de Software para sequências de tarefas de implementação de elevado impacto:

- Nas propriedades para a sequência de tarefas, agora pode configurar qualquer sequência de tarefas, incluindo sequências de tarefas de sistema não operacionais, como uma implementação de alto risco. Qualquer sequência de tarefas que cumpra determinadas condições é automaticamente definida como impacto elevado. Para obter mais informações, consulte [gerir implementações de alto risco](/sccm/protect/understand/settings-to-manage-high-risk-deployments).
- Nas propriedades para a sequência de tarefas, pode optar por utilizar a mensagem de notificação predefinidas ou criar a sua própria mensagem de notificação personalizada para implementações de elevado impacto.
- Nas propriedades para a sequência de tarefas, pode configurar o Centro de Software propriedades, que incluem efetuar um reinício necessário, o tamanho de transferência da sequência de tarefas, e o estimado tempo de execução.
- A mensagem de implementação de elevado impacto predefinida para direta atualiza agora os Estados que as aplicações, dados e definições são migradas automaticamente. Anteriormente, a mensagem predefinida para qualquer instalação do sistema operativo for indicado que todas as aplicações, dados e as definições serão perdidas, que não era aplica-se uma atualização no local.

Para obter mais informações, consulte [configurar as definições de sequência de tarefas de elevado impacto](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Regressar à página anterior, quando ocorre uma falha de uma sequência de tarefas
Agora pode regressar a uma página anterior quando executa uma sequência de tarefas e não existe uma falha. Antes desta versão, era necessário reiniciar a sequência de tarefas quando ocorreu uma falha. Por exemplo, pode utilizar o **anterior** botão nos seguintes cenários:

- Quando um computador é iniciado no Windows PE, o diálogo de arranque de configuração de sequência de tarefas pode apresentar antes da sequência de tarefas está disponível. Quando clicar em seguinte neste cenário, a página final da sequência de tarefas é apresentada uma mensagem que existem não existem sequências de tarefas disponíveis. Agora, pode clicar em **anterior** para novamente procurar sequências de tarefas disponíveis. Pode repetir este processo até que a sequência de tarefas esteja disponível.
- Quando executa uma sequência de tarefas, mas os pacotes de conteúdos dependentes ainda não estão disponíveis nos pontos de distribuição, a sequência de tarefas falhará. Pode agora distribuir o conteúdo em falta (se não foi distribuída ainda) ou aguardar que o conteúdo fique disponível nos pontos de distribuição e, em seguida, clique em **anterior** ter a pesquisa de sequência de tarefas novamente para o conteúdo.

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Pré-armazenar conteúdo em cache para as implementações disponíveis e sequências de tarefas
A partir da versão 1702, para as implementações disponíveis de sequências de tarefas, pode optar por utilizar pré-armazenar conteúdo em cache. Pré-armazenar conteúdo em cache dá-lhe a opção para permitir que o cliente transferir apenas o conteúdo aplicável logo que recebe a implementação. Por conseguinte, quando o utilizador clica em **instalar** no Centro de Software, o conteúdo está pronto e a instalação inicia rapidamente porque o conteúdo no disco rígido local. Para obter mais informações, consulte [configurar pré-armazenar conteúdo em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>A conversão de BIOS em UEFI durante uma atualização no local
Atualização do Windows 10 criadores introduz uma ferramenta de conversão simples que automatiza o processo para reparticionar o disco rígido para hardware ativado para UEFI e integra-se a ferramenta de conversão para o Windows 7 para o processo de atualização do Windows 10 no local. Ao combinar esta ferramenta com a sequência de tarefas de atualização do sistema operativo e a ferramenta do OEM que converte o firmware de BIOS para UEFI, pode converter os seus computadores de BIOS para UEFI durante uma atualização no local para o Windows 10 criadores Update. Para obter mais informações, consulte [para gerir o BIOS para conversão de UEFI, os passos de sequência de tarefas](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>Passo de melhorias à sequência de tarefas instalar aplicações
Esta versão introduziu os seguintes melhoramentos:
- Aumentar o número máximo de aplicações que pode instalar a 99 no **instalar aplicações** passo de sequência de tarefas. O número máximo anterior foi 9 aplicações.
- Ao adicionar aplicações para o **instalar aplicações** passo de sequência de tarefas no editor de sequência de tarefas, agora, pode selecionar a várias aplicações a **selecionar a aplicação a instalar** painel.

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>Melhoramentos à sequência de tarefas aplicar controladores automaticamente
Novas variáveis de sequência de tarefas estão agora disponíveis para configurar o valor de tempo limite no passo de sequência de tarefas aplicar controladores automaticamente quando são efetuados pedidos do catálogo HTTP. As seguintes variáveis e valores predefinidos (em segundos) estão disponíveis:
   - SMSTSDriverRequestResolveTimeOut  
     Predefinição: 60
   - SMSTSDriverRequestConnectTimeOut  
     Predefinição: 60
   - SMSTSDriverRequestSendTimeOut  
     Predefinição: 60
   - SMSTSDriverRequestReceiveTimeOut  
     Predefinição: 480

### <a name="windows-10-adk-tracked-by-build-version"></a>Windows 10 ADK controlada pela versão de compilação
O Windows 10 ADK agora é controlado pela versão de compilação para garantir uma experiência mais suportada ao personalizar imagens de arranque do Windows 10. Por exemplo, se o site utiliza o Windows ADK para Windows 10, versão 1607, imagens de arranque com a versão 10.0.14393 podem ser personalizadas na consola do. Para obter mais informações sobre como personalizar versões do WinPE, consulte [personalizar imagens de arranque](/sccm/osd/get-started/customize-boot-images).

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>Já não é possível alterar o caminho de origem de imagem de arranque predefinido
Imagens de arranque predefinidas são geridas pelo Configuration Manager e o caminho de origem de imagem de arranque predefinido já não pode ser alterado na consola do Configuration Manager ou utilizando o SDK do Configuration Manager. Pode continuar a configurar um caminho de origem personalizada para imagens de arranque personalizadas.

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>Imagens de arranque predefinidas são regeneradas após atualizar o Configuration Manager para uma nova versão
A partir desta versão, quando atualizar a versão do Windows ADK e, em seguida, utilizar as atualizações e manutenção para instalar a versão mais recente do Configuration Manager, Configuration Manager gera de novo as imagens de arranque predefinidas. Isto inclui a nova versão do PE de janela do Windows ADK atualizado, a nova versão do cliente do Configuration Manager, controladores, personalizações, etc. Imagens de arranque personalizadas não são modificadas. Para obter mais informações, consulte [gerir imagens de arranque](/sccm/osd/get-started/manage-boot-images#BKMK_BootImageDefault).

## <a name="software-updates"></a>Atualizações de software

### <a name="deploy-office-365-apps-to-clients"></a>Implementar aplicações do Office 365 nos clientes
A partir da versão 1702, a partir do dashboard de gestão de clientes do Office 365, pode iniciar o instalador de 365 do Office que lhe permite configurar definições de instalação do Office 365, transfira ficheiros a partir de redes de entrega de conteúdo (CDNs) do Office e implementar os ficheiros como uma aplicação no Configuration Manager. Para obter mais informações, consulte [de atualizações de gerir o Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps).

> [!IMPORTANT]
> A aplicação do Office 365 que criar e implementar utilizando o Assistente de aplicação do Office 365 no Configuration Manager não é automaticamente gerida pelo Configuration Manager até que tenha ativado a **ativar a gestão de cliente de 365 do Office novamente** definição de agente de cliente de atualizações de software. Para obter mais informações, consulte [sobre definições de cliente](/sccm/core/clients/deploy/about-client-settings).

### <a name="manage-express-installation-files-for-windows-10-updates"></a>Gerir ficheiros de instalação rápida para atualizações do Windows 10
A partir da versão 1702, o Configuration Manager suporta ficheiros de instalação rápida para atualizações do Windows 10. Quando utiliza uma versão suportada do Windows 10, pode utilizar definições de Configuration Manager para transferir apenas as alterações entre Windows 10 atualização o mês atual cumulativa e a atualização do mês anterior. Sem ficheiros de instalação rápida, o Configuration Manager transfere a completa Windows 10 atualização cumulativa (incluindo todas as atualizações de meses anteriores) por mês. A utilização de ficheiros de instalação rápida fornece para transferências mais pequenas e tempos de instalação mais rápidos nos clientes. Para obter mais informações, consulte [gerir ficheiros de instalação rápida para atualizações do Windows 10](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Gestão de dispositivos móveis

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Android e iOS versões deixam de ser targetable em assistentes de criação para MDM híbrida

A partir da versão 1702 híbrida gestão de dispositivos móveis (MDM), já não tem como destino a versões específicas do Android e iOS, quando criar novas políticas e perfis de dispositivos geridos pelo Intune. Em vez disso, escolha um dos seguintes tipos de dispositivos:

- Android
- Samsung KNOX Standard 4.0 e posterior
- iPhone
- iPad

Esta alteração afeta os assistentes para criar os seguintes itens:

- Itens de configuração
- Políticas de conformidade
- Perfis de certificado
- Perfis de e-mail
- Perfis da VPN
- Perfis de Wi-Fi

Com esta alteração, implementações híbridas podem fornecer suporte mais rapidamente para novas versões de Android e iOS sem necessitar de uma nova versão do Configuration Manager ou a extensão. Depois de uma nova versão é suportada no Intune autónomo, os utilizadores conseguirão atualizar os respetivos dispositivos móveis para essa versão.

Para evitar problemas ao atualizar a partir de versões anteriores do Configuration Manager, versões de sistema operativo móvel ainda estão disponíveis as páginas de propriedades para estes itens. Se ainda precisar de uma versão específica de destino, pode criar o novo item e, em seguida, especifique a versão especificada na página de propriedades do item criado recentemente. 

> [!NOTE]
> A última versão de sistema operativo móvel disponível nas páginas de propriedades aplica-se de que a versão e todas as versões subsequentes. Páginas de propriedades fornecem as seguintes opções de filtragem de sistemas operativos posteriores ao Android 7 e iOS 10: 
> - **Android 7 e superior**
> - **Todos os 10 superiores iPhone ou iPod touch os dispositivos iOS e**
> - **Todos os iOS 10 e superiores dispositivos iPad**

### <a name="android-for-work-support"></a>Android para o suporte de trabalho
A partir do 1702, gestão de dispositivos móveis híbrida com o Microsoft Intune suporta agora Android para gestão e de inscrição de dispositivos de trabalho. Android gerido para obter orientações de dispositivos de trabalho:

- [Inscrição Android para dispositivos de trabalho](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-enrollment)
- [Aprovar e implementar Android para aplicações de trabalho](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Criar itens de configuração para Android para o trabalho](/sccm/mdm/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-for-work-configuration-items)
- [Eliminação seletiva no Android para dispositivos de trabalho](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)
- [Perfis de e-mail para Android para o trabalho](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Políticas de conformidade para Android para o trabalho](/sccm/mdm/deploy-use/create-compliance-policy)


### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Implementar aplicações iOS compradas em volume para coleções de dispositivos

Pode agora implementar aplicações licenciadas para dispositivos, bem como os utilizadores. Consoante a capacidade de aplicações para suportar o dispositivo de licenciamento, uma licença adequada irá ser reclamada quando a implementá-la, da seguinte forma:

|||||
|-|-|-|-|
|Versão do Configuration Manager|Aplicação suporta o licenciamento do dispositivo?|Tipo de coleção de implementação|Licença pedida|
|Anteriores ao 1702|Sim|Utilizador|Licença de utilizador|
|Anteriores ao 1702|Não|Utilizador|Licença de utilizador|
|Anteriores ao 1702|Sim|Dispositivo|Licença de utilizador|
|Anteriores ao 1702|Não|Dispositivo|Licença de utilizador|
|1702 e posterior|Sim|Utilizador|Licença de utilizador|
|1702 e posterior|Não|Utilizador|Licença de utilizador|
|1702 e posterior|Sim|Dispositivo|Licença de dispositivo|
|1702 e posterior|Não|Dispositivo|Licença de utilizador|

Para mais informações sobre as aplicações iOS compradas em volume, consulte [gerir aplicações iOS compradas em volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

### <a name="support-for-ios-volume-purchase-program-for-education"></a>Suporte para iOS Volume Purchase Program para as educação

Pode também implementar e controlar aplicações compradas do iOS Volume Purchase Program para Education.
Para mais informações sobre as aplicações iOS compradas em volume, consulte [gerir aplicações iOS compradas em volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>Suporte para vários tokens do volume-purchase program

Agora pode associar vários tokens de programa de compra da Apple com o Configuration Manager.
Para mais informações sobre as aplicações iOS compradas em volume, consulte [gerir aplicações iOS compradas em volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>Suporte para a linha de negócio aplicações na loja Windows para empresas

Agora pode sincronizar personalizada aplicações de linha de negócio da loja Windows para empresas.

### <a name="conditional-access-device-compliance-policy-improvements"></a>Melhoramentos de política de conformidade de dispositivos de acesso condicional

Uma nova regra de política de conformidade de dispositivo está disponível para ajudar a bloquear o acesso aos recursos empresariais que suportam o acesso condicional, quando os utilizadores estão a utilizar aplicações que fazem parte de uma lista de aplicações não conformes. A lista de aplicações não conformes pode ser definida pelo administrador ao adicionar a nova regra de conformidade **aplicações que não não possível instalar**. Esta regra requer que o administrador para introduzir o **nome da aplicação**, a **ID da aplicação**e o **fabricante da aplicação** (opcional) quando adicionar uma aplicação à lista de não conformidade. Esta definição aplica-se apenas a dispositivos iOS e Android.

Além disso, ajuda as organizações a mitigar a fuga de dados através de aplicações não segura e impedir que o consumo excessivo de dados através de determinadas aplicações.

- Saiba mais [como funcionam as políticas de conformidade do dispositivo](/sccm/mdm/deploy-use/device-compliance-policies).
- Saiba mais [como criar políticas de conformidade de dispositivo](/sccm/mdm/deploy-use/create-compliance-policy).

### <a name="new-mobile-threat-defense-monitoring-tools"></a>Defesa de ameaça Mobile novas ferramentas de monitorização

A partir da versão 1702, terá de novas formas para monitorizar o estado de compatibilidade com o fornecedor de serviços móveis defesa de ameaça.

- Saiba mais [como monitorizar a conformidade de defesa de ameaça Mobile](https://docs.microsoft.com/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).

## <a name="protect-devices"></a>Proteger dispositivos

### <a name="detect-outdated-antimalware-client-versions"></a>Detetar as versões de cliente Desatualizadas antimalware
A partir da versão 1702, pode configurar um alerta para garantir que os clientes de Endpoint Protection não estão desatualizados. Para obter mais informações, consulte [alertas para o cliente de software maligno Desatualizadas](/sccm/protect/deploy-use/endpoint-configure-alerts#detect-outdated-antimalware-client-versions).

### <a name="device-health-attestation-updates"></a>Atualizações de atestado de estado de funcionamento do dispositivo
Serviço de atestado de estado de funcionamento do dispositivo no local clientes agora podem ser configurados e geridos a partir do ponto de gestão. Para obter mais informações, consulte [atestado de estado de funcionamento](/sccm/core/servers/manage/health-attestation).

### <a name="certificate-profiles-for-windows-hello-for-business"></a>Perfis de certificado para o Windows Hello para empresas

Se pretende armazenar os perfis de certificado no Windows Hello para o contentor de chaves de negócio e o perfil de certificado utiliza a EKU de início de sessão de Smart Card, tem de configurar permissões para o registo de chave garantir que o certificado é validado corretamente.
Para obter mais informações, consulte [Windows Hello para definições da empresa](/sccm/protect/deploy-use/windows-hello-for-business-settings).

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>Novo do Windows Hello para notificação de negócio para os utilizadores finais
Uma nova notificação do Windows 10 informa os utilizadores finais que requerem ações adicionais para concluir Windows Hello para a configuração de negócio (por exemplo, definição de um PIN).

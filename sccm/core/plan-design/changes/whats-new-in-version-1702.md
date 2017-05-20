---
title: "Nova versão 1702 | Documentos do Microsoft"
description: "Obter informações sobre as alterações e novas capacidades introduzidas na versão 1702 do System Center Configuration Manager."
ms.custom: na
ms.date: 05/02/2017
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f4cb711f369698fe8e045f8c83dd96ec6fb29d70
ms.openlocfilehash: a2954b3c6f9a09b7246347e780c4cfc49ba39ca1
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="what39s-new-in-version-1702-of-system-center-configuration-manager"></a>O que &#39; s Novidades na versão 1702 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Atualize 1702 para ramo atual do System Center Configuration Manager está disponível como uma atualização na consola de sites instaladas anteriormente com a versão 1602, 1606 ou 1610. Também está disponível como uma versão de linha de base que pode utilizar ao instalar uma nova implementação.

> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de linha de base do Configuration Manager.  
>  Saiba mais sobre:    
>   - [Instalar novos sites](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Instalação de atualizações de sites](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As secções seguintes fornecem detalhes sobre as alterações e funcionalidades novas, introduzidas na versão 1702 do Configuration Manager.  

## <a name="deprecated-features-and-operating-systems"></a>Sistemas operativos e funcionalidades preteridas
Saiba mais sobre alterações de suporte antes que estão implementadas na [removido e preterido funcionalidades](/sccm/core/plan-design/changes/removed-and-deprecated-features).

1702 remoções versão suportem para os seguintes produtos:
- **SQL Server 2008 R2**, dos servidores de base de dados do site. Depreciação do suporte foi [primeiro comunicadas](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-support-for-sql-server-versions-as-a-site-database) 10 de Julho de 2015. Esta versão do SQL Server permanece suportada quando utilizar uma versão do Configuration Manager antes da versão 1702.
- **Windows Server 2008 R2**, para a maioria das funções de sistema de sites e servidores de sistema de sites. Depreciação do suporte foi [primeiro comunicadas](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems) 10 de Julho de 2015. Esta versão do Windows permanece suportado quando utilizar uma versão do Configuration Manager antes da versão 1702.  
- **Windows Server 2008**, para a maioria das funções de sistema de sites e servidores de sistema de sites. Depreciação do suporte foi [primeiro comunicadas](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems) 10 de Julho de 2015.
- **Windows XP Embedded**, como um sistema operativo cliente. Foi preterição [primeiro comunicadas](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems) 10 de Julho de 2015. Esta versão do Windows permanece suportado quando utilizar uma versão do Configuration Manager antes da versão 1702.




## <a name="site-infrastructure"></a>Infraestrutura de sites

### <a name="improvements-for-in-console-search"></a>Melhoramentos na cópia de pesquisa na consola
Seguem-se melhoramentos para utilizar a procura na consola do Configuration Manager:
 - **Caminho do objeto:**  
  Muitos objetos suportam agora uma coluna chamada **caminho do objeto**.  Quando pesquisar e inclua esta coluna nos resultados da sua apresentação, pode ver o caminho para cada objeto. Por exemplo, se executar uma procura de aplicações no nó de aplicações e também estiver à procura nodes secundárias, a *caminho do objeto* coluna no painel de resultados irá mostrar o caminho para cada objeto que é devolvido.   

- **Preservação de texto de pesquisa:**  
  Quando introduzir texto na caixa de texto de pesquisa e, em seguida, alternar entre procurar um nó secundárias e o nó atual, o texto que escreveu agora irá manter e permanecem disponível para uma nova procura sem ter de reintroduzi-lo.

- **Preservação de sua decisão para pesquisar nodes secundárias:**  
 A opção que escolher para procurar o *nó atual* ou *todos os nós secundárias* agora persistir quando altera o nó onde está a trabalhar. Este novo comportamento significa que não é necessário repor constantemente esta decisão como mover-se a consola. Por predefinição, ao abrir a consola a opção é procurar apenas o nó atual.


### <a name="send-feedback-from-the-configuration-manager-console"></a>Enviar comentários a partir da consola do Configuration Manager

 Pode utilizar as opções de comentários na consola para enviar comentários diretamente para a equipa de desenvolvimento.

 Pode encontrar o **comentários** opção:
 -  No Friso, na extremidade esquerda do separador de cada nó.  
    ![Friso](./media/feedback-home.png)

 -  Quando lhe com o botão direito em qualquer objeto na consola.   
     ![Opção de clique Righ](./media/feedback-option.png)   

 Escolher **comentários** abre-se o browser para o [Web site do Configuration Manager UserVoice comentários](https://go.microsoft.com/fwlink/?linkid=617029).


###  <a name="changes-for-updates-and-servicing"></a>Alterações à atualizações e manutenção
Seguem-se as alterações à atualizações e manutenção:

- **Localização do nó**   
  Depois de instalar a versão 1702, o **atualizações e a manutenção** nó aparece como um nó de nível superior **administração**. Já não é um nó subordinado abaixo **serviços em nuvem**.

- **Novos Estados da atualização**  
  Quando vê as atualizações disponíveis na consola, existem dois novos Estados:  
  - **Disponível para instalação** -trata de uma atualização que foi transferido e pronto para instalar.
  - **Está preparado para transferência** -esta atualização está disponível, mas não foi transferida. Pode optar por transferir esta atualização, mas foi substituída por uma atualização mais recente.


- **Opções de atualização mais simples**  
  Da próxima vez que a infraestrutura são considerados para duas ou mais atualizações, apenas a atualização mais recente é transferida. Por exemplo, se a versão atual do site é dois ou mais mais antiga do que a versão mais recente está disponível, apenas essa versão de atualização mais recente é transferido automaticamente.  

  Pode optar por transferir e instalar outras atualizações disponíveis, mesmo quando não estiverem a versão mais atual. Se transferir uma atualização anterior, receberá um aviso de que a atualização foi substituída por uma mais recente. Para transferir uma atualização que seja *disponível para transferência*, selecione a atualização na consola e, em seguida, clique em **transferir**.

- **Limpeza melhorada de atualizações anteriores**   
  Adicionámos uma função de limpeza automática que elimina as transferências desnecessários da pasta 'EasySetupPayload' no servidor do site. Porque esta é introduzida com a versão 1702, limpeza começa a funcionar depois de instalar uma atualização subsequente como uma atualização do rollup ou versão de atualização futuros.  


### <a name="data-warehouse-service-point"></a>Ponto de serviço do armazém de dados
 Utilize o ponto de serviço do armazém de dados para armazenar e elaborar relatórios sobre dados históricos a longo prazo para a implementação do Configuration Manager.

 O armazém de dados suporta até 2 TB de dados, com carimbos de registo de alterações. Armazenamento de dados é realizado por sincronizações automáticas da base de dados do site do Configuration Manager para a base de dados do armazém de dados. Esta informação, em seguida, é acessível a partir do seu ponto de Reporting Services.

 Para obter mais informações, consulte o artigo [ponto de serviço do armazém de dados](/sccm/core/servers/manage/data-warehouse).


### <a name="peer-cache-improvements"></a>Melhoramentos de Cache ponto a ponto
 A partir da versão 1702, um computador de origem de cache ponto a ponto irão rejeitar um pedido de conteúdo quando o computador de origem de cache ponto a ponto cumpra qualquer um dos seguintes condições:  
  -  Está no modo de bateria baixo.
  -  Carga de CPU excede 80% o momento que o conteúdo de exemplos é solicitado.
  -  E/s de disco tem um *AvgDiskQueueLength* que excede 10.
  -  Não existem ligações não mais disponíveis para o computador.   
Para obter mais informações, consulte o artigo **limitada acesso a uma origem de cache ponto a ponto** no [Cache ponto a ponto para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).   

Além disso, são adicionados três novos relatórios para o ponto do reporting. Pode utilizar estes relatórios para obter mais detalhes sobre rejeitados dos pedidos de conteúdo, incluindo o limite de grupo, o computador e o conteúdo foi envolvido de compreender. Consulte o artigo [monitorização](/sccm/core/plan-design/hierarchy/client-peer-cache#monitoring) no tópico de cache ponto a ponto.

### <a name="content-library-cleanup-tool"></a>Ferramenta de limpeza da biblioteca de conteúdos
 Utilize o [ferramenta de limpeza da biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) para remover o conteúdo a partir de pontos de distribuição quando esse conteúdo já não se encontra associado a uma aplicação.


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>Utilizar o conector OMS com a nuvem do Azure para a administração pública
Pode utilizar o conector OMS para ligar a análise do registo OMS na nuvem do Microsoft Azure para a administração pública. Isto requer que a modificar um ficheiro de configuração antes de instalar o conector OMS, para que o conector pode trabalhar com a nuvem para a administração pública. Para obter mais informações, consulte o artigo [utilizar o conector OMS com a nuvem do Azure para a administração pública](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig).

### <a name="software-update-points-are-added-to-boundary-groups"></a>Pontos de atualização de software são adicionados a grupos de limites
A partir da versão 1702, os clientes utilizam os grupos de limites para localizar um novo ponto de atualização de software e de contingência e localizar uma atualização de software novo ponto se os respetivos um atual já não está acessível. Pode adicionar pontos de atualização de individual software a grupos de limites diferentes para controlar quais os servidores de um cliente pode encontrar. Para obter mais informações, consulte o artigo [pontos de atualização de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) no [configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) tópico.


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="new-compliance-settings-for-ios"></a>Novas definições de compatibilidade para iOS

Adicionámos muitas novas definições para dispositivos iOS para corresponderem aos disponível com o Microsoft Intune.
Para obter uma lista de todas as definições disponíveis, consulte o artigo [criar itens de configuração do iOS e Mac OS X dos dispositivos geridos com o Intune](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client).


## <a name="application-management"></a>Gestão de Aplicações

### <a name="improved-support-for-windows-store-for-business-apps"></a>Suporte melhorado para a loja Windows para as aplicações da empresa

Pode agora implementar aplicações licenciadas online a partir da loja Windows para a empresa para Windows 10 PCs que gere com o cliente do Configuration Manager.
Para obter mais informações, consulte o artigo [gerir aplicações na loja Windows para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

### <a name="check-for-running-executable-files-before-installing-an-application"></a>Verifique a existência de ficheiros executáveis a ser executado antes de instalar uma aplicação

No **propriedades** , na caixa de diálogo de uma implementação de escrever o **instalar comportamento** separador, pode agora especificar um dos ficheiros executáveis mais que, se a ser executado, irão bloquear a instalação do tipo de implementação. O utilizador tem de fechar o ficheiro executável está em execução (ou pode ser fechado automaticamente para implementações com um objetivo necessário) antes da implementação tipo pode ser instalado.

Se a aplicação foi implementada como **disponível**e um utilizador final tenta instalar uma aplicação, será pedido para fechar qualquer executáveis em execução que especificou antes que podem prosseguir com a instalação.

Se a aplicação foi implementada como **necessário**e a opção **fechar automaticamente qualquer executáveis em execução que especificou no separador de comportamento da instalação da caixa de diálogo Propriedades do tipo de implementação** é selecionada, irá ver uma caixa de diálogo que informa que executáveis especificou são fechados automaticamente quando for atingido o prazo de instalação da aplicação.

### <a name="app-management-improvements-for-hybrid-mdm"></a>Melhorias na gestão de aplicação para uma implementação híbrida MDM

- [Implementar aplicações iOS adquiridos de volume em coleções de dispositivos](#deploy-volume-purchased-ios-apps-to-device-collections)
- [Suporte para iOS do programa de compra de Volume para a educação](#support-for-ios-volume-purchase-program-for-education)
- [Suporte para vários tokens de programa de compra de volume](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>Implementação do sistema operativo

### <a name="expire-stand-alone-media"></a>Expirar suportes de dados autónomos
Quando cria o suporte de dados autónomo, existem novas opções para definir opcionais datas de início e de expiração no suporte de dados. Estas definições estão desativadas por predefinição. As datas são comparados com a hora do sistema no computador antes da execução do suporte de dados autónomo. Quando a hora do sistema é anterior à hora de início ou posterior à hora de expiração, o suporte de dados autónomo não está iniciado. Estas opções também estão disponíveis ao utilizar o cmdlet New-CMStandaloneMedia do PowerShell. Para obter mais detalhes, consulte o artigo [criar suportes de dados autónomos](/sccm/osd/deploy-use/create-stand-alone-media).

### <a name="package-id-displayed-in-task-sequence-steps"></a>ID do pacote apresentado nos passos de sequência de tarefas
Qualquer passo de sequência de tarefas que faça referência a um pacote, o pacote de controladores, a imagem do sistema operativo, a imagem de arranque ou o pacote de atualização do sistema operativo agora irá apresentar o ID do pacote do objeto referenciado. Quando um passo de sequência de tarefas referencia uma aplicação, apresentará o ID de objeto.

### <a name="support-for-additional-content-in-stand-alone-media"></a>Suporte para o conteúdo adicional no suporte de dados autónomo
Conteúdo adicional é agora suportado no suporte de dados autónomo. Pode selecionar adicionais pacotes, pacotes de controladores e aplicações a ser testado no suporte de dados juntamente com outros conteúdos referenciados na sequência de tarefas. Anteriormente, apenas o conteúdo referenciado na sequência de tarefas foi pré-configurados no suporte de dados autónomo. Para obter mais detalhes, consulte o artigo [criar suportes de dados autónomos](/sccm/osd/deploy-use/create-stand-alone-media).

### <a name="hardware-inventory-collects-uefi-information"></a>Inventário de hardware recolhe informações de UEFI
Uma nova classe de inventário de hardware (**SMS_Firmware**) e propriedades (**UEFI**) estão disponíveis para o ajudar a determinar se um computador arrancar no modo UEFI. Quando um computador for iniciado no modo UEFI, o **UEFI** propriedade está definida como **verdadeiro**. Isto é ativado no inventário de hardware por predefinição. Para obter mais informações sobre o inventário de hardware, consulte o artigo [como configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>Melhoramentos para as mensagens de aviso do Centro de Software para sequências de tarefas de impacto elevado
Esta versão inclui os seguintes melhoramentos para as mensagens de aviso do Centro de Software para sequências de tarefas de implementação de impacto elevado:

- Nas propriedades para a sequência de tarefas, agora pode configurar qualquer sequência de tarefas, incluindo sequências de tarefas não pertencente ao sistema operativo, como uma implementação de alto risco. Qualquer sequência de tarefas que cumpre determinadas condições é automaticamente definida como impacto elevado. Para obter mais detalhes, consulte o artigo [gerir implementações de alto risco](/sccm/protect/understand/settings-to-manage-high-risk-deployments).
- Nas propriedades para a sequência de tarefas, pode optar por utilizar a mensagem de notificação predefinidas ou crie a sua própria mensagem de notificação personalizada para implementações de impacto elevado.
- Nas propriedades para a sequência de tarefas, pode configurar o Centro de Software propriedades, que incluem tornar um reinício obrigatório, o tamanho de transferência da sequência de tarefas, e o estimado tempo de execução.
- A mensagem de implementação de impacto elevado predefinida para direta atualiza agora os Estados que suas definições, aplicações e dados são migradas automaticamente. Anteriormente, a mensagem predefinida para qualquer instalação do sistema operativo indicado que todas as aplicações, dados e definições, seria perdidas, que não era aplica-se uma atualização no local.

Para obter mais detalhes, consulte o artigo [configurar definições da sequência de tarefas de impacto elevado](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Regressar à página anterior, quando uma sequência de tarefas falhar
Agora, pode regressar à página anterior quando executa uma sequência de tarefas e existir uma falha. Esta versão, era necessário reiniciar a sequência de tarefas quando ocorreu uma falha. Por exemplo, pode utilizar o **anterior** botão nos seguintes cenários:

- Quando um computador arrancar no Windows PE, o diálogo de arranque de configuração de sequência de tarefas pode apresentar antes da sequência de tarefas está disponível. Quando clicar em seguinte neste cenário, a página final da sequência de tarefas apresentada com uma mensagem que não existem não sequências de tarefas disponível. Agora, pode clicar em **anterior** para procurar novamente sequências de tarefas disponíveis. Pode repetir este processo até que a sequência de tarefas esteja disponível.
- Quando executa uma sequência de tarefas, mas os pacotes de conteúdos dependentes ainda não estão disponíveis nos pontos de distribuição, a sequência de tarefas falhará. Pode agora distribuir o conteúdo em falta (se não foi distribuída ainda) ou aguardar que o conteúdo fique disponível nos pontos de distribuição e, em seguida, clique em **anterior** com a pesquisa de sequência de tarefas novamente para o conteúdo.

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Conteúdo da cache de pré-lançamento para as implementações disponíveis e sequências de tarefas
A partir na versão 1702, para as implementações de sequências de tarefas disponíveis, pode optar por utilizar o conteúdo da cache de pré-lançamento. O conteúdo da pré-cache de dá-lhe a opção para permitir que o cliente transferir apenas o conteúdo aplicável assim que receber a implementação. Por conseguinte, quando o utilizador clica **instalar** no Centro de Software, o conteúdo estiver disponível e a instalação for iniciada rapidamente porque o conteúdo está no disco rígido local. Para obter mais detalhes, consulte o artigo [configurar conteúdos em pré-cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Converter de BIOS para UEFI durante uma atualização no local
Atualização do Windows 10 criadores apresenta uma ferramenta de conversão simples que automatiza o processo para criar partições do disco rígido para o hardware preparados para UEFI e integra-se a ferramenta de conversão para o Windows 7 para o processo de atualização de no local do Windows 10. Esta ferramenta se as combinar com a sequência de tarefas de atualização do sistema operativo e a ferramenta do OEM que converte o firmware de BIOS UEFI, pode converter os computadores de BIOS para UEFI durante uma atualização no local para a atualização de criadores do Windows 10. Para obter mais detalhes, consulte o artigo [tarefas passos de sequência para gerir BIOS para conversão de UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>Melhoramentos à sequência de tarefas instalar aplicações passo
Esta versão introduziu os seguintes melhoramentos:
- Aumenta o número máximo de aplicações que pode instalar e 99 no **instalar aplicações** passo de sequência de tarefas. O número máximo anterior era 9 aplicações.
- Ao adicionar aplicações para o **instalar aplicações** passo de sequência de tarefas no editor de sequência de tarefas, agora pode selecionar várias aplicações a partir do **selecionar a aplicação a instalar** painel.

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>Melhoramentos à sequência de tarefas aplicar controlador automaticamente
Novas variáveis de sequência de tarefas estão agora disponíveis para configurar o valor de tempo limite no passo de sequência de tarefas aplicar controlador automaticamente quando efetuar pedidos do catálogo de HTTP. Estão disponíveis as seguintes variáveis e valores predefinidos (em segundos):
   - SMSTSDriverRequestResolveTimeOut  
     Predefinição: 60
   - SMSTSDriverRequestConnectTimeOut  
     Predefinição: 60
   - SMSTSDriverRequestSendTimeOut  
     Predefinição: 60
   - SMSTSDriverRequestReceiveTimeOut  
     Predefinição: 480

### <a name="windows-10-adk-tracked-by-build-version"></a>Windows 10 ADK controlada pela versão de compilação
O Windows 10 ADK agora é controlado pela versão de compilação para garantir uma experiência mais suportada ao personalizar imagens de arranque do Windows 10. Por exemplo, se o site utiliza o Windows ADK para Windows 10, versão 1607, apenas as imagens de arranque com a versão 10.0.14393 podem ser personalizadas na consola. Para obter detalhes sobre como personalizar WinPE versões, consulte o artigo [personalizar imagens de arranque](/sccm/osd/get-started/customize-boot-images).

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>Já não é possível alterar o caminho de origem de imagem de arranque predefinido
Imagens de arranque predefinidas são geridas pelo Configuration Manager e o caminho de origem de imagem de arranque predefinido já não pode ser alterado na consola do Configuration Manager ou utilizando o SDK do Configuration Manager. Pode continuar a configurar um caminho de origem personalizado para imagens de arranque personalizadas.

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>Imagens de arranque predefinidas são regeneradas após a atualização do Configuration Manager para uma nova versão
A partir nesta versão, se atualizar a versão do Windows ADK e, em seguida, utilizar as atualizações e a servir para instalar a versão mais recente do Configuration Manager, Configuration Manager gera novamente as imagens de arranque predefinidas. Isto inclui a nova versão de janela PE a partir do Windows ADK atualizado, a nova versão do cliente do Configuration Manager, controladores, personalizações, etc. Imagens de arranque personalizadas não são modificadas. Para obter mais detalhes, consulte o artigo [gerir imagens de arranque](/sccm/osd/get-started/manage-boot-images#BKMK_BootImageDefault).

## <a name="software-updates"></a>Atualizações de software

### <a name="deploy-office-365-apps-to-clients"></a>Implementar aplicações do Office 365 para clientes
Iniciar na versão 1702, a partir do dashboard de gestão de clientes do Office 365, pode iniciar o instalador do Office 365 que permite-lhe configurar definições de instalação do Office 365, transferem ficheiros a partir de redes de entrega de conteúdo (CDNs) do Office e implementar os ficheiros como uma aplicação no Configuration Manager. Para obter mais detalhes, consulte o artigo [atualizações gerir Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps).

> [!IMPORTANT]
> A aplicação do Office 365 que criar e implementar utilizando o Assistente de aplicação do Office 365 no Configuration Manager não é automaticamente gerida pelo Configuration Manager até ativar o **ativar a gestão do cliente de 365 do Office novamente** definição de agente de cliente de atualizações de software. Para obter mais detalhes, consulte o artigo [sobre definições de cliente](/sccm/core/clients/deploy/about-client-settings).

### <a name="manage-express-installation-files-for-windows-10-updates"></a>Gerir ficheiros de instalação rápida de atualizações do Windows 10
A partir na versão 1702, o Configuration Manager suporta ficheiros de instalação rápida para atualizações do Windows 10. Quando utiliza uma versão suportada do Windows 10, pode utilizar definições do Configuration Manager para transferir apenas as alterações entre Windows 10 atualização o mês atual cumulativa e a atualização do mês anterior. Sem ficheiros de instalação expressa do Configuration Manager transfere a completo Windows 10 atualização cumulativa (incluindo todas as atualizações de meses anteriores) por mês. Utilizar ficheiros de instalação rápida fornece para transferências mais pequenas e tempos mais rápidos de instalação em clientes. Para obter mais detalhes, consulte o artigo [gerir ficheiros de instalação rápida para atualizações do Windows 10](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Gestão de dispositivos móveis

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Versões do Android e iOS já não são targetable nos assistentes de criação para uma implementação híbrida MDM

A partir na versão 1702 híbrida gestão de dispositivos móveis (MDM), já não tem de versões específicas do Android e iOS de destino quando criar novas políticas e perfis de dispositivos geridos pelo Intune. Em vez disso, escolha um dos seguintes tipos de dispositivos:

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

Com esta alteração, implementações híbridas podem fornecer suporte mais rapidamente para novas versões do Android e iOS sem necessitar de uma nova versão do Configuration Manager ou a extensão. Depois de uma nova versão é suportada no Intune autónomo, os utilizadores será possível atualizar os respetivos dispositivos móveis para essa versão.

Para evitar problemas ao atualizar a partir de versões anteriores do Configuration Manager, versões de sistema operativo móvel ainda estão disponíveis nas páginas de propriedades para estes itens. Se ainda precisar de uma versão específica de destino, pode criar o novo item e, em seguida, especifique a versão de destino na página de propriedades do item criado recentemente.

### <a name="android-for-work-support"></a>Android para o suporte de trabalho
A partir da 1702, gestão de dispositivos móveis híbrida com o Microsoft Intune agora suporta Android para inscrição de dispositivos de trabalho e de gestão. Android gerido para orientação do trabalho de dispositivos:

- [Inscrição Android para dispositivos de trabalho](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-enrollment)
- [Aprovar e implementar Android para aplicações de trabalho](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Criar itens de configuração para Android para trabalhar](/sccm/mdm/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-for-work-configuration-items)
- [Eliminação seletiva no Android para dispositivos de trabalho](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)
- [Perfis de e-mail para Android para trabalhar](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Políticas de conformidade para Android para trabalhar](/sccm/mdm/deploy-use/create-compliance-policy)


### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Implementar aplicações iOS adquiridos de volume em coleções de dispositivos

Pode agora implementar aplicações licenciadas dispositivos, bem como os utilizadores. Dependendo da capacidade de aplicações para suportar o dispositivo de licenciamento, uma licença adequada irá ser reclamada quando implementá-la, da seguinte forma:

|||||
|-|-|-|-|
|Versão do Configuration Manager|A aplicação suporta licenciamento do dispositivo?|Tipo de coleção de implementação|Licença alegada|
|Anteriores ao 1702|Sim|Utilizador|Licença de utilizador|
|Anteriores ao 1702|Não|Utilizador|Licença de utilizador|
|Anteriores ao 1702|Sim|Dispositivo|Licença de utilizador|
|Anteriores ao 1702|Não|Dispositivo|Licença de utilizador|
|1702 e posterior|Sim|Utilizador|Licença de utilizador|
|1702 e posterior|Não|Utilizador|Licença de utilizador|
|1702 e posterior|Sim|Dispositivo|Licença de dispositivo|
|1702 e posterior|Não|Dispositivo|Licença de utilizador|

Para mais informações sobre as aplicações iOS adquiridos de volume, consulte o artigo [gerir aplicações iOS adquiridos volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

### <a name="support-for-ios-volume-purchase-program-for-education"></a>Suporte para iOS do programa de compra de Volume para a educação

Pode também implementar e monitorizar aplicações comprou a partir do iOS do programa de compra de Volume para a educação.
Para mais informações sobre as aplicações iOS adquiridos de volume, consulte o artigo [gerir aplicações iOS adquiridos volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>Suporte para vários tokens de programa de compra de volume

Agora pode associar vários tokens de programa de compra de volume Apple com o Configuration Manager.
Para mais informações sobre as aplicações iOS adquiridos de volume, consulte o artigo [gerir aplicações iOS adquiridos volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>Suporte para a linha de negócio na loja Windows para empresas

Agora pode sincronizar personalizada aplicações de linha de negócio a partir da loja Windows para empresas.

### <a name="conditional-access-device-compliance-policy-improvements"></a>Melhoramentos de política de conformidade de dispositivos de acesso condicional

Uma nova regra de política de conformidade do dispositivo está disponível para ajudar a bloquear o acesso aos recursos empresariais que suportam o acesso condicional, quando os utilizadores estão a utilizar as aplicações que fazem parte de uma lista de aplicações não conformes. A lista de aplicações não conformes pode ser definida pelo administrador quando adicionar a nova regra compatível **aplicações que não não possível instalar**. Esta regra requer que o administrador para introduzir o **nome da aplicação**, a **ID da aplicação**e o **App Publisher** (opcional) quando adicionar uma aplicação à lista de não conformidade. Esta definição só se aplica a dispositivos iOS e Android.

Além disso, esta ajuda as organizações a mitigar fuga de dados através de aplicações não segura e a prevenir consumo excessivo de dados através de determinadas aplicações.

- Saiba mais [como funcionam as políticas de conformidade do dispositivo](/sccm/mdm/deploy-use/device-compliance-policies).
- Saiba mais [como criar políticas de conformidade de dispositivos](/sccm/mdm/deploy-use/create-compliance-policy).

### <a name="new-mobile-threat-defense-monitoring-tools"></a>Novo Mobile ameaça defesa ferramentas de monitorização

Iniciar na versão 1702, tem de novas formas de monitorizar o estado de compatibilidade com o fornecedor de serviços móveis defesa de ameaça.

- Saiba mais [como monitorizar a compatibilidade de Mobile ameaça defesa](https://docs.microsoft.com/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).

## <a name="protect-devices"></a>Proteger os dispositivos

### <a name="detect-outdated-antimalware-client-versions"></a>Detetar as versões de cliente de proteção contra software maligno Desatualizadas
A partir da versão 1702, pode configurar um alerta para garantir que os clientes de Endpoint Protection não estão desatualizados. Para obter mais informações, consulte o artigo [alertas para o cliente de software maligno Desatualizadas](/sccm/protect/deploy-use/endpoint-configure-alerts#detect-outdated-antimalware-client-versions).

### <a name="device-health-attestation-updates"></a>Atualizações de atestado de estado de funcionamento do dispositivo
Serviço de atestado de estado de funcionamento de dispositivos no local clientes agora podem ser configurados e geridos a partir do ponto de gestão. Para obter mais informações, consulte o artigo [atestado de estado de funcionamento](/sccm/core/servers/manage/health-attestation).

### <a name="certificate-profiles-for-windows-hello-for-business"></a>Perfis de certificado para o Windows Hello para empresas

Se tenciona guardar os perfis de certificado no Windows Hello do contentor de chaves de empresas e o perfil de certificado utiliza a EKU de início de sessão de Smart Card, é necessário configurar permissões para o registo de chave garantir que o certificado é validado corretamente.
Para obter mais informações, consulte o artigo [Windows Hello para definições de empresas](/sccm/protect/deploy-use/windows-hello-for-business-settings).

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>Novo Windows Hello para notificação de negócio para os utilizadores finais
Uma nova notificação do Windows 10 informa os utilizadores finais que o que tem de realizar ações adicionais para concluir Windows Hello para a configuração de negócio (por exemplo, definição de um PIN).


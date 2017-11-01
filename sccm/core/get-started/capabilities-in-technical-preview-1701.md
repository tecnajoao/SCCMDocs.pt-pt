---
title: Funcionalidades no Technical Preview 1701
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1701."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 56c2ceea56eec984715d61f8d195c1b47fd3c571
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="capabilities-in-technical-preview-1701-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1701 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*



Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1701. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja o tópico introdutórias, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>Melhoramentos de grupos de limites para o software de pontos de atualização
Começando com esta pré-visualização, agora, utilizar grupos de limites para associar os clientes com pontos de atualização de software. Esta é a parte do trabalho contínuo para expandir as alterações de grupos de limites gerir funções de sistema de sites adicionais.  As alterações de grupos de limites foi introduzida pela primeira vez no Technical Preview 1609 e o ramo atual versão 1610.  

Com esta pré-visualização, utilize o novo limite grupo comportamento para gerir os pontos de atualização de software pode utilizar um cliente, semelhante à forma como que gere o ponto de distribuição de que um cliente pode utilizar:  

- Configurar grupos de limites para associar um ou mais servidores que alojam um software de um ponto de atualização.
- Clientes que procuram um novo ponto de atualização de software tentará utilizar uma que está associado ao respetivo grupo de limites atuais.
- Quando o cliente não consegue alcançar os respetivos software atual ponto de atualização e não é possível localizar um do respetivo grupo de limites atual, o cliente utiliza o comportamento de contingência para expandir o conjunto disponível de pontos de atualização de software que pode utilizar.    

Para obter mais informações sobre grupos de limites, consulte [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) no conteúdo para o ramo atual.

No entanto, com esta pré-visualização, grupos de limites para os pontos de atualização de software são apenas parcialmente implementados. Pode adicionar pontos de atualização de software e configurar grupos de limites de vizinho que contêm pontos de atualização de software, mas o tempo de contingência para pontos de atualização de software ainda não é suportado e os clientes serão Aguarde duas horas antes de começar contingência.

O seguinte descreve o comportamento de pontos de atualização de software com este technical preview:  

-   **Novos clientes utilizam grupos de limites para selecionar pontos de atualização de software,** um cliente que instale depois de instalar seleciona versão 1701 uma atualização de software ponto a partir das associadas ao grupo de limites do cliente.

  Esta ação substitui o anterior comportamento onde os clientes selecionam um ponto de atualização de software aleatoriamente entre uma lista de aqueles que partilham a floresta de clientes.   

-   **Anteriormente instalados os clientes continuam a utilizar o respetivo ponto de atualização de software atual até que a contingência para localizar um novo.**
Clientes que tenham sido anteriormente instalados e que já tenham um ponto de atualização de software irão continuar a utilizar esse ponto de atualização de software até que a contingência. Isto inclui pontos de atualização de software que não estão associados ao grupo de limites atual do cliente. Não imediatamente tentam localizar e utilizar um ponto de atualização de software do respetivo grupo de limites atual.

  Um cliente que já tem um ponto de atualização de software começa a utilizar este novo comportamento de grupo de limites apenas depois do cliente não consegue contactar o respetivo ponto de atualização de software atual e começa a contingência.
Este atraso da mudança ativação pós-falha para o novo comportamento é intencional. Isto acontece porque uma alteração de ponto de atualização de software pode resultar numa grande utilização de largura de banda de rede, como o cliente sincroniza os dados com o novo ponto de atualização de software. O atraso em transição pode ajudar a evitar saturating a sua rede devem todos os seus clientes mudarem para o novo software de pontos de atualização em simultâneo.

-   **Configurações de tempo de contingência:** Configurações para quando os clientes começam a contingência para procurar um novo ponto de atualização de software não são suportadas nesta pré-visualização técnica. Isto inclui as configurações para **contingência exceder o tempo (em minutos)** e **nunca contingência**, que pode configurar para relações de grupo de limites diferentes.

  Em vez disso, os clientes mantém o respetivo comportamento atual em que um cliente tenta ligar ao respetivo ponto de atualização de software atual para duas horas antes de iniciar contingência, para localizar um novo ponto de atualização de software que pode utilizar.

  Quando um cliente utiliza a contingência, irá utilizar as configurações do grupo de limites para contingência para criar um conjunto de pontos de atualização de software disponível. Este agrupamento inclui todos os pontos de atualização de software dos clientes *atual grupo de limites*, *vizinho grupos de limites*e os clientes *grupo de limites do site predefinido*.

- **Configure o grupo de limites de site predefinido:**  
 Considere adicionar um ponto de atualização de software para o *predefinição-Site-limite-grupo&lt;sitecode >*. Isto garante que os clientes que não são membros de outro grupo de limites podem contingência para localizar o software de um ponto de atualização.


Para gerir pontos de atualização de software para os grupos de limites, utilize o [procedimentos na documentação do Current Branch](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#procedures-for-boundary-groups), mas não se esqueça de que tempos de contingência que poderá configurar não são ainda utilizados para pontos de atualização de software.


## <a name="hardware-inventory-collects-uefi-information"></a>Inventário de hardware recolhe informações de UEFI
Uma nova classe de inventário de hardware (**SMS_Firmware**) e a propriedade (**UEFI**) estão disponíveis para o ajudar a determinar se um computador é iniciado no modo UEFI. Quando um computador for iniciado no modo UEFI, o **UEFI** propriedade está definida como **verdadeiro**. Esta opção estiver ativada no inventário de hardware por predefinição. Para obter mais informações sobre o inventário de hardware, consulte [como configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="improvements-to-operating-system-deployment"></a>Melhorias para implementação do sistema operativo
Efetuamos as seguintes melhorias para implementação do sistema operativo, muitas das que foram o resultado dos seus comentários de voz do utilizador.
- [**Suporte para mais aplicações para o passo de sequência de tarefas instalar aplicações**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t): Podemos ter aumentado o número máximo de aplicações que pode instalar a 99 no **instalar aplicações** passo de sequência de tarefas. O número máximo anterior foi 9 aplicações.
- [**Selecione a várias aplicações no passo de sequência de tarefas instalar aplicação**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step): Ao adicionar aplicações para a sequência de tarefas instalar aplicação passo no editor de sequência de tarefas, agora, pode selecionar várias aplicações a partir de **selecionar a aplicação a instalar** painel.
- [**Expirar o suporte de dados autónomo**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media): Quando cria suporte de dados autónomo, existem novas opções para definir opcionais datas de início e de expiração no suporte de dados. Estas definições estão desativadas por predefinição. As datas são em comparação com a hora do sistema no computador antes do suporte de dados autónomo é executado. Quando a hora do sistema é anterior à hora de início ou posterior à hora de expiração, o suporte de dados autónomo não foi iniciado. Estas opções também estão disponíveis utilizando o cmdlet New-CMStandaloneMedia PowerShell.
- [**Suporte para conteúdo adicional no suporte de dados autónomo**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic): Conteúdo adicional é agora suportado no suporte de dados autónomo. Pode selecionar pacotes adicionais, pacotes de controladores e aplicações para testado no suporte de dados, juntamente com outros conteúdos referenciados na sequência de tarefas. Anteriormente, apenas os conteúdos referenciados na sequência de tarefas foi testado no suporte de dados autónomo.
- [**Limite de tempo configurável para o passo de sequência de tarefas aplicar controladores automaticamente**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout): Novas variáveis de sequência de tarefas estão agora disponíveis para configurar o valor de tempo limite no passo de sequência de tarefas aplicar controladores automaticamente quando são efetuados pedidos do catálogo HTTP. As seguintes variáveis e valores predefinidos (em segundos) estão disponíveis:
   - SMSTSDriverRequestResolveTimeOut predefinição: 60
   - SMSTSDriverRequestConnectTimeOut predefinição: 60
   - SMSTSDriverRequestSendTimeOut predefinição: 60
   - SMSTSDriverRequestReceiveTimeOut predefinição: 480
- [**ID do pacote é apresentado no passos de sequência de tarefas**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste): Qualquer passo de sequência de tarefas que faça referência a um pacote, o pacote de controladores, a imagem do sistema operativo, a imagem de arranque ou o pacote de atualização do sistema operativo irá apresentar agora o ID de pacote do objeto referenciado. Quando um passo de sequência de tarefas faz referência a uma aplicação apresentará o ID de objeto.
- **Windows 10 ADK controlada pela versão de compilação**: O Windows 10 ADK agora é controlado pela versão de compilação para garantir uma experiência mais suportada ao personalizar imagens de arranque do Windows 10. Por exemplo, se o site utiliza o Windows ADK para Windows 10, versão 1607, imagens de arranque com a versão 10.0.14393 podem ser personalizadas na consola do. Para obter mais informações sobre como personalizar versões do WinPE, consulte [personalizar imagens de arranque](/sccm/osd/get-started/customize-boot-images).
- **Já não é possível alterar o caminho de origem de imagem de arranque predefinido**: Imagens de arranque predefinidas são geridas pelo Configuration Manager e o caminho de origem de imagem de arranque predefinido já não pode ser alterado na consola do Configuration Manager ou utilizando o SDK do Configuration Manager. Pode continuar a configurar um caminho de origem personalizada para imagens de arranque personalizadas.

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>Atualizações de software de anfitrião em pontos de distribuição baseado na nuvem
Começando com esta versão de pré-visualização, pode utilizar um ponto de distribuição baseado na nuvem para alojar um pacote de atualização de software. No entanto, uma vez que pode configurar clientes para transferir as atualizações de software diretamente a partir do Microsoft Update, considere os custos adicionais que implementar o software de um pacote de atualização para um ponto de distribuição baseado na nuvem que podem implicar.

Para obter informações sobre como utilizar pontos de distribuição baseado na nuvem, consulte [utilizar um ponto de distribuição baseados na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) no conteúdo para a atual filial do Configuration Manager.

## <a name="validate-device-health-attestation-data-via-management-points"></a>Validar os dados de atestado de estado de funcionamento de dispositivos através de pontos de gestão

Começando com esta versão de pré-visualização, pode configurar pontos de gestão para validar os dados para o serviço de atestado de estado de funcionamento de nuvem ou no local do relatório de atestado de estado de funcionamento. Um novo **opções avançadas** separador o **propriedades do componente de ponto de gestão** caixa de diálogo permite-lhe **adicionar**, **editar**, ou **remover** o **URL do serviço de atestado de estado de funcionamento de dispositivos no local**. Também pode especificar **definições personalizadas do dispositivo** para o agente de cliente **utilizar no local o serviço de atestado de estado de funcionamento**.  Definição **Sim** para esta definição irá ativar relatórios para o local do ponto de gestão em vez do serviço baseado na nuvem.

### <a name="try-it-out"></a>Experimente

- **Ativar o atestado de estado de funcionamento de dispositivos no local num ponto de gestão**<br>  Na consola do Configuration Manager, navegue para o ponto de gestão e abra **propriedades do componente de ponto de gestão** e, em seguida, clique em de **opções avançadas** separador. Clique em **adicionar** e especificar o URL no local (por exemplo, https://10.10.10.10) para **URLs do serviço de atestado de estado de funcionamento de dispositivos no local**.
- **Ativar o atestado estado de funcionamento no local gestão ponto de Reporting Services para o agente do cliente**<br>Na consola do Configuration Manager, escolha **administração** > **as definições de cliente** e faça duplo clique ou crie um novo **definições personalizadas do dispositivo**. Selecione **agente do computador** e defina **utilizar no local o serviço de atestado de estado de funcionamento** para **Sim**. Se **ativar comunicação com o serviço de atestado de estado de funcionamento do dispositivo** está definido como **Sim** e **utilizar no local atestado de estado de funcionamento** está definido como **não**, o ponto de gestão irá utilizar o serviço de atestado de estado de funcionamento de dispositivos baseado na nuvem.

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>Utilizar o conector do OMS para a nuvem do Microsoft Azure Government
Com esta pré-visualização técnica, agora, pode utilizar o conector do Microsoft Operations Management Suite (OMS) para ligar a uma área de trabalho do OMS que não está na nuvem do Microsoft Azure Government.  

Para tal, modificar um ficheiro de configuração para apontar para a nuvem do Governo dos EUA e, em seguida, instalar o conector do OMS.

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>Configurar um conector do OMS à nuvem do Microsoft Azure Government
1.  Em qualquer computador que tenha a consola do Configuration Manager instalada, edite o ficheiro de configuração seguintes para apontar para a nuvem pública:  ***&lt;Caminho de instalação do CM > \AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **Edições:**

    Altere o valor para o nome da definição *FairFaxArmResourceID* para ser igual a "https://management.usgovcloudapi.net/"

   - **Original:** &lt;nome da definição = "FairFaxArmResourceId" serializeAs = "Cadeia" >   
      &lt;valor > &lt; /value >   
      &lt;/ definição >

   - **Editadas:**     
      &lt;nome da definição = "FairFaxArmResourceId" serializeAs = "Cadeia" > &lt;valor > https://management.usgovcloudapi.net/ &lt; /value >  
      &lt;/ definição >

  Altere o valor para o nome da definição *FairFaxAuthorityResource* para ser igual a "https://login.microsoftonline.com/"

  - **Original:** &lt;nome da definição = "FairFaxAuthorityResource" serializeAs = "Cadeia" >   
    &lt;valor > &lt; /value >

    - **Editadas:** &lt;nome da definição = "FairFaxAuthorityResource" serializeAs = "Cadeia" >   
    &lt;valor > https://login.microsoftonline.com/ &lt; /value >

2.  Depois de guardar o ficheiro com as duas alterações, reiniciar a consola do Configuration Manager no mesmo computador e, em seguida, utilize essa consola para instalar o conector do OMS. Para instalar o conector, utilize as informações em [sincronizar os dados do Configuration Manager para o Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)e selecione o **área de trabalho do Operations Management Suite** que não está na nuvem do Microsoft Azure Government.

3.  Depois de instala o conector do OMS, a ligação para a nuvem do Governo dos EUA está disponível quando utiliza qualquer consola que liga ao site.

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Android e iOS versões deixam de ser targetable em assistentes de criação para MDM híbrida

A partir desta pré-visualização técnica para gestão de dispositivos móveis híbridos (MDM), já não tem como destino a versões específicas do Android e iOS, quando criar novas políticas e perfis de dispositivos geridos pelo Intune. Em vez disso, escolha um dos seguintes tipos de dispositivos:

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

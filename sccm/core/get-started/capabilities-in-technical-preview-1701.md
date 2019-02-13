---
title: Capacidades na pré-visualização técnica 1701
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1701.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4edec748950b4601c4f5889f180f74c158171b33
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136818"
---
# <a name="capabilities-in-technical-preview-1701-for-system-center-configuration-manager"></a>Capacidades na pré-visualização técnica 1701 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*



Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1701. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.    


**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>Melhorias de grupos de limites para o software de pontos de atualização
Começando com esta pré-visualização, agora, utilizar grupos de limites para associar os clientes com pontos de atualização de software. Isso faz parte do trabalho contínuo para expandir as alterações de grupos de limites para gerir funções de sistema de sites adicionais.  As alterações para grupos de limites foi introduzido pela primeira vez na versão 1609 de pré-visualização técnica e o ramo atual na versão 1610.  

Com esta pré-visualização, utilize o novo limite grupo comportamento para gerir os pontos de atualização de software pode utilizar um cliente, semelhante a como gerir o ponto de distribuição de que um cliente pode utilizar:  

- Configurar grupos de limites para associar uma ou mais servidores que alojam um software de ponto de atualização.
- Os clientes que procuram um novo ponto de atualização de software tentará utilizar um que está associada ao respetivo grupo de limites atual.
- Quando o cliente falhará em atingir seu software atual ponto de atualização e não é possível localizar um do respetivo grupo de limites atual, o cliente utiliza o comportamento de contingência para expandir o conjunto disponível de pontos de atualização de software pode utilizar.    

Para obter mais informações sobre grupos de limites, consulte [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) no conteúdo para o ramo atual.

No entanto, com esta pré-visualização, grupos de limites para os pontos de atualização de software são apenas parcialmente implementados. Pode adicionar pontos de atualização de software e configurar grupos de limites do vizinho que contêm pontos de atualização de software, mas o tempo de contingência para pontos de atualização de software ainda não é suportado e clientes aguardará duas horas antes de começar contingência.

A seguir descreve o comportamento de pontos de atualização de software com esta pré-visualização técnica:  

- **Novos clientes utilizam grupos de limites para selecionar pontos de atualização de software,** um cliente que instala depois de instalar o seleciona versão 1701 uma atualização de software ponto a partir as associadas ao grupo de limites do cliente.

  Esta ação substitui o comportamento anterior em que os clientes selecionam um ponto de atualização de software aleatoriamente de uma lista de aqueles que partilham a floresta de clientes.   

- **Anteriormente instalados clientes continuam a utilizar o seu atual ponto de atualização de software até que a contingência para localizar um novo.**
  Clientes que tiverem sido instaladas e que já tenham um ponto de atualização de software irão continuar a utilizar esse ponto de atualização de software até que eles contingência. Isto inclui pontos de atualização de software que não estão associados ao grupo de limites atual do cliente. Eles não imediatamente tente encontrar e utilizar um ponto de atualização de software do respetivo grupo de limites atual.

  Um cliente que já tem um ponto de atualização de software começa a utilizar esse novo comportamento de grupo de limites apenas depois do cliente não consegue contactar o seu atual ponto de atualização de software e começa a contingência.
  Este atraso na mudança para o novo comportamento é intencional. Isto acontece porque uma alteração de ponto de atualização de software pode resultar numa grande utilização de largura de banda de rede, como o cliente sincroniza os dados com o novo ponto de atualização de software. O atraso em transição pode ajudar a evitar saturar a rede devem todos os seus clientes mudarem para o novo software de pontos de atualização ao mesmo tempo.

- **Configurações de tempo de contingência:** Configurações para quando os clientes começam a contingência para procurar um novo ponto de atualização de software não são suportadas neste technical Preview. Isso inclui configurações para **tempos de contingência (em minutos)** e **Never contingência**, que pode configurar para relações de grupo de limites diferentes.

  Em vez disso, os clientes retenham seu comportamento atual em que um cliente tenta ligar ao seu ponto de atualização de software atual de duas horas antes de iniciar fallback, para localizar um novo ponto de atualização de software pode utilizar.

  Quando um cliente utiliza a contingência, irá utilizar as configurações do grupo de limites de contingência para criar um conjunto de pontos de atualização de software disponíveis. Este conjunto inclui todos os pontos de atualização de software dos clientes *grupo de limites atual*, *vizinho grupos de limites*e os clientes *grupo de limite predefinido de site*.

- **Configure o grupo de limites de site padrão:**  
  Considere adicionar um ponto de atualização de software para o *predefinição---grupo de limite Site&lt;sitecode >*. Isto garante que os clientes que não são membros de outro grupo de limites podem fallback para localizar um software de ponto de atualização.


Para gerir pontos de atualização de software para grupos de limites, utilize o [procedimentos da documentação do Current Branch](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#procedures-for-boundary-groups), mas lembre-se de que pode configurar tempos de contingência não são utilizados ainda para pontos de atualização de software.


## <a name="hardware-inventory-collects-uefi-information"></a>Inventário de hardware recolhe informações de UEFI
Uma nova classe de inventário de hardware (**SMS_Firmware**) e a propriedade (**UEFI**) estão disponíveis para ajudar a determinar se um computador é iniciado no modo UEFI. Quando um computador é iniciado no modo UEFI, o **UEFI** estiver definida como **verdadeiro**. Esta opção estiver ativada no inventário de hardware por predefinição. Para obter mais informações sobre o inventário de hardware, consulte [como configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="improvements-to-operating-system-deployment"></a>Melhorias para implementação do sistema operativo
Que fizemos as seguintes melhorias para implementação do sistema operativo, muitos dos quais foram o resultado dos seus comentários de voz do utilizador.
- [**Suporte para mais aplicações para o passo de sequência de tarefas instalar aplicativos**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t): Podemos aumentaram consideravelmente o número máximo de aplicações que pode instalar a 99 no **instalar aplicações** passo de sequência de tarefas. O número máximo anterior era 9 aplicativos.
- [**Selecione várias aplicações no passo de sequência de tarefas instalar aplicação**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step): Ao adicionar aplicações para a sequência de tarefas instalar aplicação passo no editor de sequência de tarefas, agora, pode selecionar vários aplicativos sejam os **selecione a aplicação a instalar** painel.
- [**Expirar a mídia autônoma**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media): Quando criar suportes de dados autónomo, existem novas opções para definir as datas de início e de expiração opcionais no suporte de dados. Estas definições estão desativadas por predefinição. As datas são em comparação com a hora do sistema no computador antes do suporte de dados autónomo é executado. Quando a hora do sistema é anterior à hora de início ou posterior à hora de expiração, o suporte de dados autónomo não está iniciado. Estas opções também estão disponíveis ao utilizar o cmdlet New-CMStandaloneMedia PowerShell.
- [**Suporte para conteúdo adicional no suporte de dados autónomo**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic): Conteúdo adicional é agora suportado no suporte de dados autónomo. Pode selecionar pacotes adicionais, pacotes de controladores e aplicações para ser preparado no suporte de dados, juntamente com os outros conteúdos referenciados na sequência de tarefas. Anteriormente, apenas os conteúdos referenciados na sequência de tarefas foi testado no suporte de dados autónomo.
- [**Tempo limite configuráveis para o passo de sequência de tarefas aplicar controladores automaticamente**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout): Novas variáveis de sequência de tarefas estão agora disponíveis para configurar o valor de tempo limite no passo de sequência de tarefas aplicar controladores automaticamente quando são efetuados pedidos do catálogo HTTP. Estão disponíveis as seguintes variáveis e valores predefinidos (em segundos):
   - Predefinição de SMSTSDriverRequestResolveTimeOut: 60
   - Predefinição de SMSTSDriverRequestConnectTimeOut: 60
   - Predefinição de SMSTSDriverRequestSendTimeOut: 60
   - SMSTSDriverRequestReceiveTimeOut Default: 480
- [**ID do pacote é apresentado no passos de sequência de tarefas**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste): Qualquer passo de sequência de tarefas que faça referência a um pacote, o pacote de controladores, a imagem do sistema operativo, a imagem de arranque ou o pacote de atualização do sistema operativo agora irá apresentar o ID do pacote do objeto referenciado. Quando um passo de sequência de tarefas faz referência um aplicativo apresentará o ID de objeto.
- **Windows 10 ADK controlados por versão de compilação**: O Windows 10 ADK agora é controlado pela versão de compilação para garantir uma experiência mais suporte ao personalizar imagens de arranque do Windows 10. Por exemplo, se o site utiliza o Windows ADK para Windows 10, versão 1607, apenas as imagens de arranque com a versão 10.0.14393 podem ser personalizadas na consola do. Para obter detalhes sobre como personalizar as versões do WinPE, consulte [personalizar imagens de arranque](/sccm/osd/get-started/customize-boot-images).
- **Já não pode ser alterado o caminho de origem de imagem de arranque predefinido**: Imagens de arranque predefinidas são geridas pelo Configuration Manager e o caminho de origem de imagem de arranque predefinido já não pode ser alterado na consola do Configuration Manager ou com o SDK do Configuration Manager. Pode continuar a configurar um caminho de origem de dados personalizada para imagens de arranque personalizadas.

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>Anfitrião de atualizações de software em pontos de distribuição baseado na nuvem
A partir desta versão de pré-visualização, pode utilizar um ponto de distribuição baseado na nuvem para alojar um pacote de atualização de software. No entanto, uma vez que pode configurar clientes para transferir atualizações de software diretamente a partir do Microsoft Update, considere podem implicar custos adicionais que a implementação de um software pacote de atualização para um ponto de distribuição baseado na nuvem.

Para obter informações sobre como utilizar pontos de distribuição baseado na nuvem, consulte [utilizar um ponto de distribuição baseado na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) no conteúdo para o atual ramo do Configuration Manager.

## <a name="validate-device-health-attestation-data-via-management-points"></a>Validar dados de atestado de estado de funcionamento do dispositivo através de pontos de gestão

A partir desta versão de pré-visualização, pode configurar pontos de gestão para validar os dados para o serviço de atestado de estado de funcionamento na cloud ou no local de relatório de atestado de estado de funcionamento. Um novo **opções avançadas** separador a **propriedades do componente de ponto de gestão** caixa de diálogo permite-lhe **Add**, **editar**, ou **Remova** o **URL do serviço de atestado de estado de funcionamento de dispositivo local**. Também pode especificar **definições personalizadas do dispositivo** para o agente de cliente **utilização no local o serviço de atestado de estado de funcionamento**.  A definição **Sim** para esta definição irá permitir relatórios com o local do ponto de gestão, em vez do serviço baseado na nuvem.

### <a name="try-it-out"></a>Experimentar

- **Ativar o atestado de estado de funcionamento do dispositivo no local num ponto de gestão**<br>  Na consola do Configuration Manager, navegue para o ponto de gestão e abra **propriedades do componente do ponto de gestão** e, em seguida, clique nas **opções avançadas** separador. Clique em **Add** e especifique o URL no local (por exemplo, https://10.10.10.10) para **URLs do serviço de atestado de estado de funcionamento de dispositivos locais**.
- **Ativar no local gestão ponto de estado de funcionamento de relatório de atestado para o agente de cliente**<br>Na consola do Configuration Manager, escolha **Administration** > **definições de cliente** e clique duas vezes ou crie um novo **definições personalizadas do dispositivo**. Selecione **agente do computador** e defina **utilização no local o serviço de atestado de estado de funcionamento** para **Sim**. Se **ativar comunicação com o serviço de atestado de estado de funcionamento do dispositivo** está definida como **Sim** e **utilizar no local atestado de estado de funcionamento** está definido como **não**, o ponto de gestão irá utilizar o serviço de atestado de estado de funcionamento de dispositivos baseado na cloud.

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>Utilizar o conector do OMS para a cloud do Microsoft Azure Government
Com esta pré-visualização técnica, agora, pode utilizar o conector do Microsoft Operations Management Suite (OMS) para ligar a uma área de trabalho do OMS que está na cloud do Microsoft Azure Government.  

Para fazer isso, modifique um ficheiro de configuração para apontar para a cloud de Governo e, em seguida, instale o conector do OMS.

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>Configurar um conector do OMS para a cloud do Microsoft Azure Government
1. Em qualquer computador que tenha a consola do Configuration Manager instalada, edite o seguinte ficheiro de configuração para apontar para a cloud de governo:  ***&lt;Caminho de instalação do CM > \AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

   **Edições:**

   Altere o valor para o nome da definição *FairFaxArmResourceID* igual a "<https://management.usgovcloudapi.net/”>

   - **Original:** &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
     &lt;value>&lt;/value>   
     &lt;/setting>

   - **Editadas:**     
     &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value><https://management.usgovcloudapi.net/&lt;/value>>  
     &lt;/setting>

   Altere o valor para o nome da definição *FairFaxAuthorityResource* igual a "<https://login.microsoftonline.com/>"

   - **Original:** &lt;nome da definição = "FairFaxAuthorityResource" serializeAs = "String" >   
     &lt;value>&lt;/value>

   - **Editado:** &lt;nome da definição = "FairFaxAuthorityResource" serializeAs = "String" >   
     &lt;value><https://login.microsoftonline.com/&lt;/value>>

2. Depois de guardar o ficheiro com as duas alterações, reiniciar a consola do Configuration Manager no mesmo computador e, em seguida, utilize essa consola para instalar o conector do OMS. Para instalar o conector, utilize as informações em [sincronizar dados do Configuration Manager para o Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)e selecione o **área de trabalho do Operations Management Suite** isso estiver nos a cloud do Microsoft Azure Government.

3. Depois de instala o conector do OMS, a ligação para a cloud de Governo está disponível quando utiliza qualquer consola que liga ao site.

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Versões do Android e iOS já não são targetable nos assistentes de criação para MDM híbrida

A partir desta pré-visualização técnica para gestão de dispositivos móveis híbridos (MDM), já não precisar de atingir versões específicas do Android e iOS durante a criação de novas políticas e perfis de dispositivos geridos pelo Intune. Em vez disso, escolha um dos seguintes tipos de dispositivos:

- Android
- Samsung KNOX Standard 4.0 e superior
- iPhone
- iPad

Esta alteração afeta os assistentes para criar os seguintes itens:

- Itens de configuração
- Políticas de conformidade
- Perfis de certificados
- Perfis de e-mail
- Perfis VPN
- Perfis de Wi-Fi

Com esta alteração, implementações híbridas podem fornecer suporte mais rapidamente para novas versões do Android e iOS sem a necessidade de uma nova versão do Configuration Manager ou a extensão. Depois de uma nova versão é suportada no Intune autónomo, os utilizadores poderão atualizar os dispositivos móveis para essa versão.

Para evitar problemas durante a atualização de versões anteriores do Configuration Manager, versões de sistema operativo móvel ainda estão disponíveis nas páginas de propriedades para esses itens. Se ainda precisar de uma versão específica de destino, pode criar o novo item e, em seguida, especifique a versão de destino na página de propriedades do item criado recentemente.

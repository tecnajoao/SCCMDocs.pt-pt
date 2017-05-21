---
title: "Capacidades na pré-visualização técnica 1701 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1701."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: b330c97a0853d1673f1cf7e0691891b72407fa51
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1701-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1701 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*



Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1701. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>Pontos de atualização de melhorias de grupos de limites de software
A partir desta pré-visualização, agora, utilizar grupos de limites para associar os clientes com pontos de atualização de software. Isto faz parte do trabalho contínua para expandir as alterações de grupos de limites gerir funções de sistema de sites adicionais.  Alterações de grupos de limites primeiro foi introduzido no 1609 de pré-visualização técnica e o ramo atual na versão 1610.  

Com esta pré-visualização, utilize o novo limite comportamento de grupo para gerir os pontos de atualização de software um cliente pode utilizar, semelhante ao modo como gere ponto de distribuição de que um cliente pode utilizar:  

- Configurar grupos de limites para associar um ou mais servidores que alojam o software de um ponto de atualização.
- Os clientes que procuram um novo ponto de atualização de software tentará utilizar uma que esteja associado com o atual grupo de limites.
- Quando o cliente não consegue contactar o respetivo software atual do ponto de atualização e não é possível localizar um partir do respetivo grupo de limites atual, o cliente utiliza o comportamento de contingência para expandir o conjunto disponível de pontos de atualização de software que possa utilizar.    

Para obter mais informações sobre grupos de limites, consulte o artigo [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) no conteúdo para o ramo atual.

No entanto, com esta pré-visualização, grupos de limites para os pontos de atualização de software são apenas parcialmente implementados. Pode adicionar pontos de atualização de software e configurar grupos de limites de vizinho que contenham pontos de atualização de software, mas o tempo de contingência para pontos de atualização de software ainda não é suportado e os clientes serão Aguarde duas horas antes de iniciar contingência.

O seguinte descreve o comportamento de pontos de atualização de software com este pré-visualização técnica:  

-    **Os novos clientes utilizam os grupos de limites para selecionar pontos de atualização de software,** um cliente que instale depois de instalar seleciona versão 1701 uma atualização de software ponto a partir do associada ao grupo de limites do cliente.

  Esta ação substitui o anterior comportamento onde os clientes selecionam um ponto de atualização de software aleatoriamente a partir de uma lista das pessoas que partilham a floresta de clientes.   

-    **Anteriormente instalados os clientes continuam a utilizar o respetivo ponto de atualização de software atual até que contingência para localizar um novo.**
Os clientes que tiverem sido instaladas e que já tenham um ponto de atualização de software irão continuar a utilizar esse ponto de atualização de software até que contingência. Isto inclui pontos de atualização de software que não estão associados ao grupo de limites atual do cliente. Estes não imediatamente tente localizar e utilizar um ponto de atualização de software a partir do respetivo grupo de limites atual.

  Um cliente que já tenha um ponto de atualização de software começa a utilizar este novo comportamento de grupo de limites apenas depois do cliente não consegue aceder ao respetivo ponto de atualização de software atual e começa a reversão.
Este atraso em alterar para o novo comportamento é intencional. Isto acontece porque uma alteração de ponto de atualização de software pode implicar uma utilização grande de largura de banda de rede como o cliente sincroniza os dados com o novo ponto de atualização de software. O atraso em transição pode ajudar a evitar saturating rede devem todos os seus clientes mudarem para o novo software pontos de atualização ao mesmo tempo.

-    **Configurações para tempo de contingência:** Configurações para quando os clientes iniciar contingência para procurar um novo ponto de atualização de software não são suportadas neste technical preview. Isto inclui as configurações para **contingência tempo limite (em minutos)** e **nunca contingência**, que pode configurar para relações de grupo de limites diferentes.

  Em vez disso, os clientes mantêm o respetivo comportamento atual em que um cliente tenta estabelecer ligação ao respetivo ponto de atualização de software atual para duas horas antes de iniciar contingência, para localizar um novo ponto de atualização de software que possa utilizar.

  Quando um cliente utilizam a reversão, este irá utilizar as configurações de grupo de limites para contingência para criar um conjunto de pontos de atualização de software disponível. Este conjunto inclui todos os pontos de atualização de software dos clientes *atual grupo de limites*, *vizinho grupos de limites*e os clientes *grupo de limites do site predefinido*.

- **Configure o grupo de limites de site predefinido:**  
 Considere adicionar um ponto de atualização de software para o *limites-grupo de predefinido-Site&lt;sitecode >*. Isto garante que os clientes que não sejam membros de outro grupo de limites podem reversão para localizar o software de um ponto de atualização.


Para gerir pontos de atualização de software para grupos de limites, utilize o [procedimentos a partir de documentação do ramo atual](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#procedures-for-boundary-groups), mas lembre-se de que contingência vezes, pode configurar não são utilizados ainda para pontos de atualização de software.


## <a name="hardware-inventory-collects-uefi-information"></a>Inventário de hardware recolhe informações de UEFI
Uma nova classe de inventário de hardware (**SMS_Firmware**) e propriedades (**UEFI**) estão disponíveis para o ajudar a determinar se um computador arrancar no modo UEFI. Quando um computador for iniciado no modo UEFI, o **UEFI** propriedade está definida como **verdadeiro**. Isto é ativado no inventário de hardware por predefinição. Para obter mais informações sobre o inventário de hardware, consulte o artigo [como configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="improvements-to-operating-system-deployment"></a>Melhorias na implementação do sistema operativo
Iremos efetuar os seguintes melhoramentos à implementação de sistema operativo, muitos dos quais foram o resultado dos seus comentários de voz do utilizador.
- [**Suporte para obter mais aplicações para o passo de sequência de tarefas instalar aplicações**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t): Iremos aumentou o número máximo de aplicações que pode instalar e 99 no **instalar aplicações** passo de sequência de tarefas. O número máximo anterior era 9 aplicações.
- [**Selecionar várias aplicações no passo de sequência de tarefas instalar aplicação**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step): Ao adicionar aplicações à sequência de tarefas instalar aplicação passo no editor de sequência de tarefas, agora pode selecionar várias aplicações a partir de **selecionar a aplicação a instalar** painel.
- [**Expirar suporte de dados autónomo**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media): Quando cria o suporte de dados autónomo, existem novas opções para definir opcionais datas de início e de expiração no suporte de dados. Estas definições estão desativadas por predefinição. As datas são comparados com a hora do sistema no computador antes da execução do suporte de dados autónomo. Quando a hora do sistema é anterior à hora de início ou posterior à hora de expiração, o suporte de dados autónomo não está iniciado. Estas opções também estão disponíveis ao utilizar o cmdlet New-CMStandaloneMedia do PowerShell.
- [**Suporte para o conteúdo adicional no suporte de dados autónomo**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic): Conteúdo adicional é agora suportado no suporte de dados autónomo. Pode selecionar adicionais pacotes, pacotes de controladores e aplicações a ser testado no suporte de dados juntamente com outros conteúdos referenciados na sequência de tarefas. Anteriormente, apenas o conteúdo referenciado na sequência de tarefas foi pré-configurados no suporte de dados autónomo.
- [**Tempo limite configurável para o passo de sequência de tarefas aplicar controlador automaticamente**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout): Novas variáveis de sequência de tarefas estão agora disponíveis para configurar o valor de tempo limite no passo de sequência de tarefas aplicar controlador automaticamente quando efetuar pedidos do catálogo de HTTP. Estão disponíveis as seguintes variáveis e valores predefinidos (em segundos):
   - Predefinição de SMSTSDriverRequestResolveTimeOut: 60
   - Predefinição de SMSTSDriverRequestConnectTimeOut: 60
   - Predefinição de SMSTSDriverRequestSendTimeOut: 60
   - Predefinição de SMSTSDriverRequestReceiveTimeOut: 480
- [**ID do pacote é agora apresentado nos passos de sequência de tarefas**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste): Qualquer passo de sequência de tarefas que faça referência a um pacote, o pacote de controladores, a imagem do sistema operativo, a imagem de arranque ou o pacote de atualização do sistema operativo agora irá apresentar o ID do pacote do objeto referenciado. Quando um passo de sequência de tarefas referencia uma aplicação apresentará o ID de objeto.
- **Windows 10 ADK controlada pela versão de compilação**: O Windows 10 ADK agora é controlado pela versão de compilação para garantir uma experiência mais suportada ao personalizar imagens de arranque do Windows 10. Por exemplo, se o site utiliza o Windows ADK para Windows 10, versão 1607, apenas as imagens de arranque com a versão 10.0.14393 podem ser personalizadas na consola. Para obter detalhes sobre como personalizar WinPE versões, consulte o artigo [personalizar imagens de arranque](/sccm/osd/get-started/customize-boot-images).
- **Já não é possível alterar o caminho de origem de imagem de arranque predefinido**: Imagens de arranque predefinidas são geridas pelo Configuration Manager e o caminho de origem de imagem de arranque predefinido já não pode ser alterado na consola do Configuration Manager ou utilizando o SDK do Configuration Manager. Pode continuar a configurar um caminho de origem personalizado para imagens de arranque personalizadas.

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>Atualizações de software do anfitrião em pontos de distribuição baseado na nuvem
Iniciar com esta versão de pré-visualização, pode utilizar um ponto de distribuição baseado na nuvem para alojar um pacote de atualização de software. No entanto, uma vez que pode configurar clientes para transferir atualizações de software diretamente a partir do Microsoft Update, considere podem implicar custos adicionais que implementar o software de um pacote de atualização para um ponto de distribuição baseado na nuvem.

Para obter informações sobre como utilizar pontos de distribuição baseado na nuvem, consulte o artigo [utilizar um ponto de distribuição baseado na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) no conteúdo para o atual secundário do Configuration Manager.

## <a name="validate-device-health-attestation-data-via-management-points"></a>Validar dados de atestado de estado de funcionamento de dispositivos através de pontos de gestão

Iniciar com esta versão de pré-visualização, pode configurar pontos de gestão para validar dados para o serviço de nuvem ou no local atestado de integridade de relatórios de atestado de estado de funcionamento. Um novo **opções avançadas** separador o **propriedades do componente de ponto de gestão** caixa de diálogo permite-lhe **adicionar**, **editar**, ou **remover** o **URL do serviço de atestado de estado de funcionamento de dispositivos no local**. Também pode especificar **definições personalizadas do dispositivo** para o agente de cliente **utilização no local serviço de integridade de atestado**.  Definição **Sim** para esta definição irá permitir relatórios para o local do ponto de gestão em vez de um serviço baseado na nuvem.

### <a name="try-it-out"></a>Experimente

- **Ativar atestado de estado de funcionamento de dispositivos no local num ponto de gestão**<br>  Na consola do Configuration Manager, navegue para o ponto de gestão e abra **propriedades do componente do ponto de gestão** e, em seguida, clique na **opções avançadas** separador. Clique em **adicionar** e especificar o URL no local (por exemplo, https://10.10.10.10) para **URLs do serviço de atestado de estado de funcionamento de dispositivos no local**.
- **Ativar relatórios para o agente de cliente dos atestado de estado de funcionamento de ponto para gestão no local**<br>Na consola do Configuration Manager, escolha **administração** > **definições de cliente** e faça duplo clique ou criar um novo **definições personalizadas do dispositivo**. Selecione **agente do computador** e defina **utilização no local serviço de integridade de atestado** para **Sim**. Se **ativar a comunicação com o serviço de atestado de estado de funcionamento de dispositivos** está definido como **Sim** e **utilização no local atestado de estado de funcionamento** está definido como **não**, o ponto de gestão utilizará o serviço de atestado de estado de funcionamento de dispositivos baseada na nuvem.

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>Utilizar o conector OMS para a nuvem do Microsoft Azure para a administração pública
Com esta pré-visualização técnica, agora, pode utilizar o conector do Microsoft Operations gestão Suite (OMS) para ligar a uma área de trabalho OMS que se encontra na nuvem do Microsoft Azure para a administração pública.  

Para fazê-lo, pode modificar um ficheiro de configuração para apontar para a nuvem para a administração pública e, em seguida, instalar o conector OMS.

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>Configurar um conector OMS nuvem do Microsoft Azure para a administração pública
1.  Em qualquer computador que tenha a consola do Configuration Manager instalada, edite o ficheiro de configuração seguinte para apontar para a nuvem para a administração pública:  ***&lt;Caminho de instalação do CM > \AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **Edições:**

    Altere o valor para o nome da definição *FairFaxArmResourceID* para ser igual a "https://management.usgovcloudapi.net/"

   - **Original:** 
      &lt;nome da definição = serializeAs "FairFaxArmResourceId" = "Cadeia" >   
      &lt;valor > &lt; /value >   
      &lt;/ definição >

   - **Editadas:**     
      &lt;nome da definição = serializeAs "FairFaxArmResourceId" = "Cadeia" > &lt;valor > https://management.usgovcloudapi.net/ &lt; /value >  
      &lt;/ definição >

  Altere o valor para o nome da definição *FairFaxAuthorityResource* para ser igual a "https://login.microsoftonline.com/"

  - **Original:** &lt;nome da definição = serializeAs "FairFaxAuthorityResource" = "Cadeia" >   
    &lt;valor > &lt; /value >

    - **Editadas:** &lt;nome da definição = serializeAs "FairFaxAuthorityResource" = "Cadeia" >   
    &lt;valor > https://login.microsoftonline.com/ &lt; /value >

2.    Depois de guardar o ficheiro com as alterações de dois, reiniciar a consola do Configuration Manager no mesmo computador e, em seguida, utilize essa consola para instalar o conector OMS. Para instalar o conector, utilize as informações no [sincronizar dados do Configuration Manager para o conjunto de aplicações de gestão do Microsoft Operations](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)e selecione o **área de trabalho do Operations Management Suite** que esteja na nuvem do Microsoft Azure para a administração pública.

3.    Após instala o conector OMS, a ligação para a nuvem para a administração pública está disponível quando utiliza qualquer consola que liga ao site.

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Versões do Android e iOS já não são targetable nos assistentes de criação para uma implementação híbrida MDM

A partir deste pré-visualização técnica híbrida gestão de dispositivos móveis (MDM), já não tem de versões específicas do Android e iOS de destino quando criar novas políticas e perfis de dispositivos geridos pelo Intune. Em vez disso, escolha um dos seguintes tipos de dispositivos:

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


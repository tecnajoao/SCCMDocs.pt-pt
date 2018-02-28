---
title: "Pré-visualização técnica 1802 | Microsoft Docs"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades disponíveis na versão de pré-visualização técnica 1802 para o System Center Configuration Manager."
ms.custom: na
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 162c47d867e78498650da685327c0fe296aa2eda
ms.sourcegitcommit: b1fa7be6a6fa5bb7c49e90c0e28a21ba8b41c842
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/28/2018
---
# <a name="capabilities-in-technical-preview-1802-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1802 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1802. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. 

Reveja [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview) antes de instalar esta versão do technical preview. Esse artigo familiarizes, com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como os seus comentários.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->
## <a name="known-issues-in-this-technical-preview"></a>Problemas conhecidos nesta pré-visualização técnica
-   **Falha de atualização para uma nova versão de pré-visualização quando tiver um servidor de site no modo passivo**. Se tiver um [servidor do site primário em modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), em seguida, tem de desinstalar o servidor do site de modo passivo antes de atualizar para esta nova versão de pré-visualização. Pode reinstalar o servidor do site de modo passivo depois do seu site é concluída a atualização.

  Para desinstalar o servidor do site de modo passivo:
  1. Na consola do Configuration Manager, vá para **administração** > **descrição geral** > **configuração do Site**  >  **Servidores e funções de sistema de sites**e, em seguida, selecione o servidor de site de modo passivo.
  2. No **funções do sistema de sites** painel, o botão direito no **servidor do Site** função e, em seguida, escolha **remover função**.
  3. Faça duplo clique no servidor do site de modo passivo e, em seguida, escolha **eliminar**.
  4. Depois de desinstala o servidor do site, no servidor do site primário Active Directory reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.
<!--sms 489412-->


</br>

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  


## <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Carga de trabalho de proteção de ponto final de transição para o Intune utilizando a gestão de conjunta    
<!-- 1357365 -->
Nesta versão, pode agora efetuar a transição a Endpoint Protection carga de trabalho do Configuration Manager para o Intune depois de ativar a gestão conjunta. A transição a carga de trabalho do Endpoint Protection, vá para a página de propriedades de gestão conjunta e desloque o cursor de controlo do Configuration Manager para **piloto** ou **todos os**. Para obter mais informações, consulte [conjunta management para Windows 10 dispositivos](/sccm/core/clients/manage/co-management-overview).


 
## <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configurar a otimização de entrega do Windows para utilizar grupos de limites do Configuration Manager
<!-- 1324696 -->
Utilize grupos de limites do Configuration Manager para definir e regular a distribuição de conteúdo através da rede empresarial em escritórios remotos. [Otimização de entrega de Windows](/windows/deployment/update/waas-delivery-optimization) é uma tecnologia de baseado na nuvem, ponto a ponto para partilhar conteúdo entre dispositivos Windows 10. A partir desta versão, configure a otimização de entrega a utilizar os grupos de limites, quando a partilha de conteúdo entre elementos. Uma nova definição de cliente aplica-se o identificador do grupo de limites como o identificador do grupo de otimização de entrega no cliente. Quando o cliente comunica com o serviço de nuvem de otimização de entrega, utiliza este identificador para localizar os elementos de rede com os conteúdos pretendidos. 

### <a name="prerequisites"></a>Pré-requisitos
- Otimização de entrega está disponível apenas em clientes Windows 10

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar **comentários** do **home page** separador do Friso nos informar como correu.

1. Na consola do Configuration Manager, **administração** área de trabalho, **as definições de cliente** nó, criar uma política de definições de dispositivos de cliente personalizadas.
2. Selecione o novo **otimização de entrega** grupo.
3. Ativar a definição **Utilize grupos de limites de Gestor de configuração para o ID de grupo de otimização de entrega**.

Para obter mais informações, consulte o **grupo** opção de modo de entrega em [opções de otimização de entrega](/windows/deployment/update/waas-delivery-optimization#group-id).



## <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Sequência de tarefas de atualização no local do Windows 10 através do gateway de gestão de nuvem
<!-- 1357149 -->

O Windows 10 [sequência de tarefas de atualização no local](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version) suporta agora a implementação de clientes baseados na internet geridos através de [gateway de gestão de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Esta capacidade permite aos utilizadores remotos mais facilmente atualizar para o Windows 10, sem necessitar de ligar à rede empresarial. 

Certifique-se de que todo o conteúdo referenciado pela sequência de tarefas de atualização no local é distribuído para um [ponto de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). Caso contrário, os dispositivos não é possível executar a sequência de tarefas.

Quando implementa uma sequência de tarefas de atualização, utilize as seguintes definições:
- **Permitir que a sequência de tarefas executar o cliente na Internet**, no separador de experiência de utilizador da implementação.
- **Transferir todo o conteúdo localmente antes de iniciar a sequência de tarefas**, no separador de pontos de distribuição da implementação. Outras opções como **transferir o conteúdo localmente quando necessário para a sequência de tarefas em execução** não funcionam neste cenário. O motor de sequência de tarefas é atualmente não é possível obter conteúdo de um ponto de distribuição na nuvem. O cliente do Configuration Manager tem de transferir o conteúdo do ponto de distribuição de nuvem antes de iniciar a sequência de tarefas.
- (*Opcional*) **previamente transferir conteúdo para esta sequência de tarefas**, no separador Geral da implementação. Para obter mais informações, consulte [configurar pré-armazenar conteúdo em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Melhoramentos à sequência de tarefas de atualização no local do Windows 10
<!-- 1357425 -->
O modelo de sequência de tarefas predefinido para a atualização no local do Windows 10 inclui agora grupos adicionais com as ações recomendadas para adicionar antes e depois do processo de atualização. Estas ações são comuns entre muitos clientes que com êxito estiver a atualizar dispositivos para Windows 10. 

### <a name="new-groups-under-prepare-for-upgrade"></a>Novos grupos em **preparar para atualização**
- **Verifica a bateria**: Adicione passos neste grupo para verificar se o computador está a utilizar bateria ou com fios energia. Esta ação requer um script personalizado ou o utilitário para executar esta verificação.
- **Rede/com fios verificações de ligação**: Adicione passos neste grupo para verificar se o computador está ligado a uma rede e não está a utilizar uma ligação sem fios. Esta ação requer um script personalizado ou o utilitário para executar esta verificação.
- **Remover aplicações incompatíveis**: Adicione passos neste grupo para remover todas as aplicações que são incompatíveis com esta versão do Windows 10. Varia consoante o método para desinstalar uma aplicação. Se a aplicação utiliza o Windows Installer, copie o **programa de desinstalação** linha de comandos a partir de **programas** separador Propriedades do tipo de implementação do Windows Installer da aplicação. Em seguida, adicione um **executar linha de comandos** passo neste grupo com a linha de comandos do programa de desinstalação. Por exemplo: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Remover controladores incompatíveis**: Adicione passos neste grupo para remover os controladores que sejam incompatíveis com esta versão do Windows 10.
- **Remover/suspender a segurança de terceiros**: Adicione passos neste grupo para remover ou suspender a programas de segurança de terceiros, como antivírus.
   - Se estiver a utilizar um programa de encriptação de disco de terceiros, fornecer o controlador de encriptação à configuração do Windows com o **/ReflectDrivers** [opção da linha de comandos](/windows-hardware/manufacture/desktop/windows-setup-command-line-options). Adicionar um [Set Task Sequence Variable](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) passo à sequência de tarefas neste grupo. Definir a variável de sequência de tarefas **OSDSetupAdditionalUpgradeOptions**. Defina o valor como **/ReflectDriver** com o caminho para o controlador. Isto [variável de ação de sequência de tarefas](/sccm/osd/understand/task-sequence-action-variables#upgrade-operating-system) acrescenta a configuração do Windows da linha de comandos utilizada pela sequência de tarefas. Contacte o fabricante de software para qualquer orientações adicionais sobre este processo.

### <a name="new-groups-under-post-processing"></a>Novos grupos em **pós-processamento**
- **Aplicar controladores baseados na configuração**: Adicione passos neste grupo para instalar controladores baseados no programa de configuração (.exe) a partir de pacotes.
- **Instalar/ativar segurança de terceiros**: Adicione passos neste grupo para instalar ou ative a programas de segurança de terceiros, como antivírus. 
- **Definir aplicações do Windows predefinido e as associações**: Adicione passos neste grupo para definir as aplicações do Windows predefinido e associações de ficheiros. Primeiro, prepare um computador de referência com associações a aplicação pretendida. Em seguida, execute a seguinte linha de comandos para exportar: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Adicione o ficheiro XML a um pacote. Em seguida, adicione um [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) passo deste grupo. Especifique o pacote que contém o ficheiro XML e, em seguida, especifique a linha de comandos: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Para obter mais informações, consulte [exportar ou importar predefinido associações de aplicação](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).
- **Aplicar as personalizações e personalização**: Adicione passos neste grupo para aplicar as personalizações do menu Iniciar, tais como organizar grupos de programa. Para obter mais informações, consulte [personalizar o ecrã de início](/windows-hardware/manufacture/desktop/customize-the-start-screen).

### <a name="additional-recommendations"></a>Recomendações adicionais
- Reveja a documentação do Windows para [erros de atualização do Windows 10 resolver](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Este artigo também inclui informações detalhadas sobre o processo de atualização.
- A predefinição **verificar disponibilidade** passo, ativar **assegurar espaço mínimo livre em disco (MB)**. Defina o valor para, pelo menos, **16384** (16 GB) para um SO de 32 bits atualizar o pacote, ou **20480** (20 GB) de 64 bits. 
- Utilize o **SMSTSDownloadRetryCount** [variável de sequência de tarefas incorporadas](/sccm/osd/understand/task-sequence-built-in-variables) para transferir política de repetição. Atualmente, por predefinição, o cliente duas vezes; repetir Esta variável é definida como dois (2). Se os clientes não estiverem numa ligação de rede empresarial com fios, tentativas adicionais ajudam o cliente obter a política. Utilizar esta variável faz com que nenhum efeito negativo, que não sejam falha atrasada se não é possível transferir a política.<!-- 501016 --> Aumentar também o **SMSTSDownloadRetryDelay** variável da predefinição 15 segundos.
- Efetue uma avaliação de compatibilidade inline. 
   - Adicionar uma segunda **atualizar sistema operativo** passo antecipadamente no **preparar a atualização** grupo. Nome *da avaliação da atualização*. Especifique o mesmo pacote de atualização e, em seguida, ative a opção de **análise de compatibilidade de executar a configuração do Windows sem iniciar a atualização**. Ativar **continuar com o erro** no separador de opções. 
   - Imediatamente a seguir esta *da avaliação da atualização* passo, adicione um **executar linha de comandos** passo. Especifique a linha de comandos:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>No **opções** separador, adicione a seguinte condição: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Este código de retorno é o equivalente decimal MOSETUP_E_COMPAT_SCANONLY (0xC1900210), que é uma análise de compatibilidade efetuada com êxito sem problemas. Se o *avaliação da atualização* passo for bem sucedida e devolve este código, este passo é ignorado. Caso contrário, se o passo de avaliação devolve qualquer código de retorno, este passo falhe a sequência de tarefas com o código de retorno da análise de compatibilidade de configuração do Windows.
   - Para obter mais informações, consulte [atualizar sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).
- Se pretender alterar o dispositivo de BIOS para UEFI durante esta sequência de tarefas, consulte [converter da BIOS UEFI durante uma atualização no local](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

Enviar **comentários** do **home page** separador do Friso se tiver mais recomendações ou sugestões.



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Melhoramentos para pontos de distribuição com PXE ativado
<!-- 1357580 -->
Para esclarecer o comportamento de [nova funcionalidade PXE](/sccm/core/get-started/capabilities-in-technical-preview-1706#pxe-network-boot-support-for-ipv6) primeiro introduzida na versão de pré-visualização técnica 1706, iremos mudar o nome de **suporte IPv6** opção. No **PXE** separador de propriedades do ponto de distribuição, verifique **ativar um dispositivo de resposta PXE sem o serviço de implementação do Windows**. 

Esta opção permite que um dispositivo de resposta PXE no ponto de distribuição, o que não necessite de serviços de implementação do Windows (WDS). Se ativar esta opção novo num ponto de distribuição que já está preparada para PXE, o Configuration Manager suspende o serviço WDS. Se desativar esta opção novo, mas ainda **ativar suporte PXE para clientes**, em seguida, o ponto de distribuição permite WDS novamente.

Porque o WDS não for necessário, o ponto de distribuição com PXE ativado pode ser um sistema de operativo cliente ou servidor, incluindo o Windows Server Core. Este novo serviço de dispositivo de resposta PXE continua a suportar IPv6 e melhora também a flexibilidade de pontos de distribuição com PXE ativado em escritórios remotos.

> [!NOTE]
> Este serviço utiliza a mesma tecnologia fundamental como o [serviço de dispositivo de resposta baseada no cliente PXE](/sccm/core/get-started/capabilities-in-technical-preview-1712#client-based-pxe-responder-service) na versão de pré-visualização técnica 1712. Essa funcionalidade não requer a sobrecarga da função de ponto de distribuição.

### <a name="multicast"></a>Multicast
Para ativar e configurar o multicast no **Multicast** separador Propriedades do ponto de distribuição, o ponto de distribuição tem de utilizar o WDS. 
- Se lhe **ativar suporte PXE para clientes** e **ativar multicast para enviar dados em simultâneo a múltiplos clientes**, em seguida, não é possível **ativar um dispositivo de resposta PXE sem o serviço de implementação do Windows** .
- Se lhe **ativar suporte PXE para clientes** e **ativar um dispositivo de resposta PXE sem o serviço de implementação do Windows**, em seguida, não é possível **ativar multicast para enviar dados em simultâneo a múltiplos clientes**



## <a name="deployment-templates-for-task-sequences"></a>Modelos de implementação para sequências de tarefas
<!-- 1357391 -->
O Assistente de implementação para sequências de tarefas agora pode criar um modelo de implementação. O modelo de implementação pode ser guardado e aplicado a uma sequência de tarefas existente ou novo para criar uma implementação. 

### <a name="try-it-out"></a>Experimente!  
Experimente concluir as tarefas. Em seguida, enviar **comentários** do **home page** separador do Friso nos informar como correu. 

 **Criar um modelo de implementação para uma nova implementação de sequência de tarefas** <br/> 
1. No **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.
2. Clique com o botão direito numa sequência de tarefas e selecione **implementar**. 
3. No **geral** separador, tenha em atenção é agora uma opção para **selecionar modelo de implementação**. 
4. Continuar com a **Assistente de implementação de Software** selecionar as definições de implementação para a sequência de tarefas. 
5. Quando chegar a **resumo** separador do **Assistente de implementação de Software**, clique em **guardar como modelo**.
6. Dê um nome de modelo, selecione as definições para guardar no modelo. 
7. Clique em **Guardar**. O modelo está agora disponível para utilização do **selecionar modelo de implementação** opção.



## <a name="product-lifecycle-dashboard"></a>Dashboard de ciclo de vida do produto
<!--1319632-->
A nova [dashboard de ciclo de vida do produto](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard) mostra o estado da política de ciclo de vida de produto de Microsoft para produtos da Microsoft instalado nos dispositivos geridos com o Configuration Manager. O dashboard fornece informações sobre os produtos da Microsoft no seu ambiente, o estado de Suportabilidade e datas de fim de suporte. Pode utilizar o dashboard para compreender a disponibilidade de suporte para cada produto. 

Para aceder ao Dashboard do ciclo de vida, na consola do Configuration Manager, aceda a **ativos e compatibilidade** >**do Asset Intelligence** >**ciclo de vida do produto**



## <a name="improvements-to-reporting"></a>Melhoramentos aos relatórios
<!--1357653-->
Como resultado de [os seus comentários](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and) adicionámos um novo relatório, **detalhes de manutenção do Windows 10 para uma coleção específica**. Este relatório mostra o ID de recurso, nome NetBIOS, nome do SO, nome da versão de SO, compilação, SO ramo e estado para dispositivos Windows 10 de manutenção. Para aceder ao relatório, aceda a **monitorização** >**relatórios** >**relatórios** >**sistemas de operativos**  > **Detalhes de manutenção do Windows 10 para uma coleção específica**.



## <a name="improvements-to-software-center"></a>Melhoramentos ao centro de Software
<!--1357592-->
Como resultado de [os seus comentários](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid) agora podem ser ocultadas aplicações instaladas no Centro de Software. As aplicações que já se encontram instaladas deixarão de aparecer no separador de aplicações quando esta opção está ativada. 

### <a name="try-it-out"></a>Experimente!
Ativar o **Ocultar aplicações instaladas no Centro de Software** definição nas definições de cliente do Centro de Software. Observe o comportamento no Centro de Software quando o utilizador final instala uma aplicação.



## <a name="improvements-to-run-scripts"></a>Melhoramentos para executar Scripts
<!--1236459-->
O [executar Scripts](/sccm/apps/deploy-use/create-deploy-scripts) funcionalidade agora devolve o script de saída com formatação JSON. Este formato consistentemente devolve um resultado de script legível. Scripts que falham para executar podem não obter resultados devolvidos. 



## <a name="boundary-group-fallback-for-management-points"></a>Grupo de limites contingência para pontos de gestão
<!-- 1324594 -->
A partir desta versão, pode configurar as relações de contingência para pontos de gestão entre [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups). Este comportamento proporciona maior controlo para os pontos de gestão que os clientes utilizam. No **relações** separador das propriedades do grupo de limites, é uma nova coluna para o ponto de gestão. Quando adiciona um novo grupo de limites de contingência, o tempo de contingência para o ponto de gestão é atualmente sempre zero (0). Este comportamento é o mesmo para o **comportamento predefinido** no grupo de limites de site predefinido.

Anteriormente, um problema comum ocorre quando tiver um protegido ponto de gestão numa rede segura. Os clientes na rede empresarial principal recebem a política que inclui este ponto de gestão protegidos, apesar de não conseguirem comunicar com o mesmo através de uma firewall. Para resolver este problema, utilize o **nunca contingência** opção para garantir que apenas contingência para gestão de clientes aponta com que possam comunicar.

Ao atualizar o site para esta versão, o Configuration Manager adiciona todos os pontos de gestão de não-acesso à internet para o grupo de limites do site predefinido. Este comportamento atualização assegura que as versões cliente anteriores continuam a comunicar com pontos de gestão. Para tirar partido desta funcionalidade, mova os pontos de gestão para os grupos de limites pretendido.

Reversão de grupo de limites de ponto de gestão não altera o comportamento durante a instalação de cliente (ccmsetup). Se a linha de comandos não especificar o ponto de gestão inicial com o parâmetro /MP, o novo cliente recebe a lista completa dos pontos de gestão disponíveis. Para o seu processo de arranque de configuração inicial, o cliente utiliza o primeiro ponto de gestão que possa aceder. Depois do cliente regista com o site, este recebe a lista de pontos de gestão ordenada corretamente com este novo comportamento. 

### <a name="prerequisites"></a>Pré-requisitos
- Ativar [pontos de gestão preferenciais](/sccm/core/servers/deploy/configure/boundary-groups#preferred-management-points). Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **configuração do Site** e selecione **Sites**. Clique em **definições de hierarquia** no Friso. No **geral** separador, ative **os clientes preferem utilizar pontos de gestão especificados em grupos de limites**. 

### <a name="known-issues"></a>Problemas conhecidos
- Processos de implementação do sistema operativo não têm conhecimento dos grupos de limites.

### <a name="troubleshooting"></a>Resolução de Problemas
Novas entradas são apresentados no **LocationServices.log**. O **Localidade** atributo identifica um dos seguintes Estados:
- 0: Desconhecido
- 1: O ponto de gestão especificado é apenas no grupo de limites de site predefinido para contingência
- 2: O ponto de gestão especificado está num grupo de limites de vizinhança ou remoto. Quando o ponto de gestão está num vizinho e os grupos de limites do site predefinido, a Localidade é 2.
- 3: O ponto de gestão especificado está no grupo de limites local ou atual. Quando o ponto de gestão está no grupo de limites atuais, bem como um vizinho ou o grupo de limites do site predefinido, a Localidade é 3. Se não ativar os pontos de gestão preferenciais definição nas definições de hierarquia, a Localidade é sempre 3, independentemente dos limites do ponto de gestão de grupo está a ser.

Os clientes utilizam pontos de gestão local primeiro (Localidade 3), segundo remoto (Localidade 2) e contingência (Localidade 1). 

Quando um cliente recebe erros de cinco numa dez minutos e não consegue comunicar com um ponto de gestão no respetivo grupo de limites atual, este tenta contactar um ponto de gestão de um vizinho ou o grupo de limites do site predefinido. Se o ponto de gestão atual grupo de limites mais tarde voltar a ficar online, o cliente irá devolver ao ponto de gestão local no próximo ciclo de atualização. O ciclo de atualização é de 24 horas, ou quando o serviço de agente do Configuration Manager for reiniciado.



## <a name="improved-support-for-cng-certificates"></a>Suporte melhorado para certificados CNG
<!-- 1357314 -->
Suporta a versão do Configuration Manager (ramo atual) 1710 [criptografia: Certificados do próximos geração (CNG)](/sccm/core/plan-design/network/cng-certificates-overview). Suportam 1710 limites de versão para certificados de cliente em vários cenários. 

A partir desta versão de pré-visualização técnica, utilize certificados CNG para as seguintes funções de servidor ativado para HTTPS:
- Ponto de gestão
- Ponto de distribuição
- Ponto de atualização de software

A lista de [não suportado cenários](/sccm/core/plan-design/network/cng-certificates-overview#unsupported-scenarios) permanece igual.



## <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Suporte de gateway de gestão de nuvem do Azure Resource Manager
<!-- 1324735 -->
Quando criar uma instância do [gateway de gestão de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG), o assistente fornece agora a opção para criar um **implementação Azure Resource Manager**. [O Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para gerir todos os recursos de solução como uma única entidade, chamada um [grupo de recursos](/azure/azure-resource-manager/resource-group-overview#resource-groups). Quando implementar CMG com o Azure Resource Manager, o site utiliza o Azure Active Directory (Azure AD) para autenticar e criar os recursos de nuvem necessário. Esta implementação modernized não necessita que o certificado de gestão do Azure clássico.  

O assistente CMG ainda fornece a opção para um **implementação de serviço clássico** a utilizar um certificado de gestão do Azure. Para simplificar a implementação e gestão de recursos, recomendamos que utilize o modelo de implementação Azure Resource Manager para todas as instâncias CMG novo. Se for possível, volte a implementar instâncias CMG através do Gestor de recursos existentes.

O Configuration Manager não migra existentes instâncias CMG clássicas para o modelo de implementação Azure Resource Manager. Crie novas instâncias CMG com implementações do Azure Resource Manager e, em seguida, remova clássicas CMG instâncias. 

> [!IMPORTANT]
> Esta capacidade não ative o suporte para fornecedores de serviços de nuvem do Azure (CSP). A implementação de CMG com o Azure Resource Manager continua a utilizar o serviço de nuvem clássico, que não suporta o CSP. Para obter mais informações, consulte [serviços do Azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="prerequisites"></a>Pré-requisitos
- Integração com [do Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Não é necessária a deteção de utilizadores do Azure AD.
- O mesmo [requisitos do gateway de gestão de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway#requirements-for-cloud-management-gateway), exceto o certificado de gestão do Azure.

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as tarefas. Em seguida, enviar **comentários** do **home page** separador do Friso nos informar como correu.

1. Na consola do Configuration Manager, **administração** área de trabalho, expanda **serviços em nuvem**e selecione **Gateway de gestão de nuvem**. Clique em **criar Gateway de gestão de nuvem** no Friso. 
2. No **geral** página, selecione **implementação Azure Resource Manager**. Clique em **sessão** para autenticar com uma conta de administrador de subscrição do Azure. O Assistente de auto-preenche os campos restantes das informações de subscrição do Azure AD armazenados durante o pré-requisito de integração. Se tiver várias subscrições, selecione a subscrição pretendida a utilizar. Clique em **Seguinte**.  
3. No **definições** , indique o servidor de ficheiro de certificado PKI como habitualmente. Este certificado define o nome do serviço CMG no Azure. Selecione o **região**e, em seguida, selecione uma opção de grupo de recursos para qualquer **criar nova** ou **utilizar existente**. Introduza o nome do novo grupo de recursos ou selecione um grupo de recursos existente na lista pendente. 
4. Conclua o assistente.

> [!NOTE] 
> Para o Azure AD selecionado aplicação de servidor, o Azure atribui a subscrição **contribuinte** permissão. 

Monitorizar o progresso da implementação de serviço com **cloudmgr.log** no ponto de ligação de serviço.



## <a name="approve-application-requests-for-users-per-device"></a>Aprovar pedidos de aplicações para os utilizadores por dispositivo
<!-- 1357015 -->
A partir desta versão, quando um utilizador solicita uma aplicação que necessita de aprovação, o nome de dispositivo específico faz agora parte do pedido. Se o administrador aprova o pedido, o utilizador só é possível instalar a aplicação nesse dispositivo. O utilizador tem de submeter outro pedido para instalar a aplicação noutro dispositivo. 

> [!NOTE]
> Esta funcionalidade é opcional. Ao atualizar para esta versão, ative esta funcionalidade no Assistente de atualização. Em alternativa, ative a funcionalidade na consola do mais tarde. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).

### <a name="prerequisites"></a>Pré-requisitos
- Atualizar o cliente do Configuration Manager para a versão mais recente
- Ativar a definição de cliente **utilizar o novo Centro de Software** no [agente do computador](/sccm/core/clients/deploy/about-client-settings#computer-agent) grupo

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar **comentários** do **home page** separador do Friso nos informar como correu.

1. Implemente uma aplicação disponível como uma coleção de utilizadores.
2. No **definições de implementação** página, ative a opção: **Um administrador tem de aprovar um pedido para esta aplicação no dispositivo**.
3. Como um utilizador direcionado, utilize o Centro de Software para submeter um pedido para a aplicação. 
4. Vista **pedidos de aprovação** em **gestão de aplicações** no **biblioteca de Software** área de trabalho da consola do Configuration Manager. Não há agora um **dispositivo** coluna na lista para cada pedido. Quando efetuar a ação a pedido, a caixa de diálogo de pedido de aplicação também inclui o nome de dispositivo a partir do qual o utilizador submetido o pedido.



## <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Utilizar o Centro de Software para procurar e instalar aplicações disponíveis ao utilizador no Azure AD-dispositivos associados a um
<!-- 1322613 -->
Se implementar aplicações como disponíveis para os utilizadores, pode agora navegar e instalá-los através do Centro de Software nos dispositivos do Azure Active Directory (Azure AD).  

### <a name="prerequisites"></a>Pré-requisitos
- Ativar HTTPS no ponto de gestão
- Integrar o site com [do Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure)
- Implementar uma aplicação como disponíveis para uma coleção de utilizadores
- Distribuir a qualquer conteúdo da aplicação para um [ponto de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)
- Ativar a definição de cliente **utilizar o novo Centro de Software** no [agente do computador](/sccm/core/clients/deploy/about-client-settings#computer-agent) grupo
- O cliente tem de ser: 
   - Windows 10
   - O Azure AD associados, também conhecido como nuvem associados a um domínio
- Para suportar clientes baseados na internet:
    - [Gateway de gestão de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway) 
    - Ative a definição de cliente: **Ativar pedidos da política de utilizador dos clientes Internet** no [política de cliente](/sccm/core/clients/deploy/about-client-settings#client-policy) grupo
- Para suportar clientes na rede empresarial:
    - Adicionar o ponto de distribuição de nuvem a um grupo de limites utilizado pelos clientes do
    - Os clientes têm de conseguir resolver o nome de domínio completamente qualificado (FQDN) do ponto de gestão ativado para HTTPS



## <a name="report-on-windows-autopilot-device-information"></a>Relatório sobre as informações do dispositivo Windows AutoPilot
<!-- 1351442 -->
Windows AutoPilot é uma solução de integração e a configuração de novos dispositivos Windows 10 de forma moderna. Para obter mais informações, consulte um [descrição geral do Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). É um método de registo de dispositivos existentes com Windows AutoPilot carregar as informações do dispositivo para a Microsoft Store para empresas e Education. Estas informações incluem o número de série do dispositivo, identificador de produto do Windows e um identificador de hardware. Utilize o Configuration Manager para recolher e comunicar estas informações do dispositivo. 

### <a name="prerequisites"></a>Pré-requisitos
- Estas informações de dispositivo só se aplica aos clientes no Windows 10, versão 1703 e posterior

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar **comentários** do **home page** separador do Friso nos informar como correu.

1. Na consola do Configuration Manager, **monitorização** área de trabalho, expanda o **relatórios** nó, expanda **relatórios**e selecione o **Hardware - geral**  nós.
2. Executar o novo relatório, **informações de dispositivo do Windows AutoPilot** e ver os resultados. 
3. No Visualizador de relatórios, clique o **exportar** ícone e selecione **CSV (delimitado por vírgulas)** opção.
4. Depois de guardar o ficheiro, carrega os dados para a Microsoft Store para empresas e Education. Para obter mais informações, consulte [adicionar dispositivos no Microsoft Store para empresas e as educação](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile). 



## <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Melhoramentos às políticas do Configuration Manager para o Windows Defender exploram proteção
<!-- 1356220 -->
Foram adicionadas definições de política adicionais para os componentes de acesso de pasta de redução da superfície de ataque e controlados no Configuration Manager para [Windows Defender exploram Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard).

**Novas definições para o acesso à pasta de controlados**<br/>
Existem duas opções adicionais quando configurar o acesso de pasta controlados: **Bloquear setores de disco só** e **setores de disco só de auditoria**. Estas duas definições permitir o acesso de pasta controlados estar ativado para setores de arranque apenas e não ativar a proteção de pastas específicas ou as pastas de predefinição protegida. 

**Novas definições de redução da superfície de ataque**
- Utilize proteção avançada contra ransomware.
- Bloquear credencial roubo do subsistema de autoridade de segurança local do Windows. 
- Bloquear os ficheiros executáveis a execução, a menos que cumprem um prevalência, idade ou lista fidedigna de critérios. 
- Bloquear não fidedignos e não assinados processos que são executadas a partir do USB.



## <a name="microsoft-edge-browser-policies"></a>Políticas de browser Microsoft Edge
<!-- 1357310 -->
Para os clientes que utilizam o [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) browser nos clientes do Windows 10, agora, pode criar uma política de definições de compatibilidade do Configuration Manager para configurar várias definições do Microsoft Edge. Esta política atualmente inclui as seguintes definições:
- **Browser Microsoft Edge de conjunto como predefinição**: Configura a definição de aplicação do Windows 10 predefinida para o browser do Microsoft Edge
- **Permitir que o endereço da barra de menu pendente**: Requer o Windows 10, versão 1703 ou posterior. Para obter mais informações, consulte [política de browser AllowAddressBarDropdown](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Permitir Sincronização Favoritos entre Microsoft browsers**: Requer o Windows 10, versão 1703 ou posterior. Para obter mais informações, consulte [política de browser SyncFavoritesBetweenIEAndMicrosoftEdge](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Permitir a navegação limpar dados de saída**: Requer o Windows 10, versão 1703 ou posterior. Para obter mais informações, consulte [política de browser ClearBrowsingDataOnExit](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Permitir que os cabeçalhos não controlar**: Para obter mais informações, consulte [política de browser AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Permitir Preenchimento automático**: Para obter mais informações, consulte [política de browser AllowAutofill](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Permitir cookies**: Para obter mais informações, consulte [política de browser AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Permitir Bloqueador de janelas de pop-up**: Para obter mais informações, consulte [política de browser AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Permitir sugestões de pesquisa na barra de endereço**: Para obter mais informações, consulte [política de browser AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Permitir o tráfego de intranet de envio para o Internet Explorer**: Para obter mais informações, consulte [política de browser SendIntranetTraffictoInternetExplorer](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Permitir palavra-passe manager**: Para obter mais informações, consulte [política de browser AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Permitir que as ferramentas de programador**: Para obter mais informações, consulte [política de browser AllowDeveloperTools](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Permitir extensões de**: Para obter mais informações, consulte [política de browser AllowExtensions](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).

### <a name="prerequisites"></a>Pré-requisitos
- Cliente Windows 10 que está associada ao Azure Active Directory. 

### <a name="known-issues"></a>Problemas conhecidos
- Dispositivos de associados a domínios no local não é possível aplicar esta política nesta versão. Este problema também diz respeito aos dispositivos associados a um domínio de híbrida.

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as tarefas. Em seguida, enviar **comentários** do **home page** separador do Friso nos informar como correu.

**Criar uma política**
1. Na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho. Expanda **as definições de compatibilidade** e selecione o novo **perfis de Browser Microsoft Edge** nós. Clique na opção de friso para **criar política de Browser do Microsoft Edge**.
2. Especifique um **nome** para a política e, opcionalmente, introduza um **Descrição**e clique em **seguinte**.
3. No **definições** página, altere o valor para **configurado** para que as definições incluem nesta política e clique em **seguinte**.
4. No **plataformas suportadas** página, selecione as versões de sistema operativo e arquiteturas à qual esta política aplica-se e clique em **seguinte**. 
5. Conclua o assistente.

**Implementar a política**
1. Selecione a política e clique na opção de friso para **implementar**.
2. Clique em **procurar** para selecionar a coleção de utilizador ou dispositivo ao qual pretende implementar a política. 
3. Selecione as opções adicionais conforme necessário. Gere alertas quando a política não é compatível. Defina o agendamento através do qual o cliente avalia a compatibilidade do dispositivo com esta política.
4. Clique em **OK** para criar a implementação.

Como qualquer política de definições de conformidade, o cliente corrigir as definições na agenda que especificar. [Monitorizar e gerar relatórios sobre a conformidade de dispositivo](/sccm/compliance/deploy-use/monitor-compliance-settings) na consola do Configuration Manager.



## <a name="report-for-default-browser-counts"></a>Relatório de contagens de browser predefinido
<!-- 1357830 -->
Agora é um relatório novo para mostrar a contagem de clientes com um browser específico, como a predefinição do Windows. 

### <a name="known-issues"></a>Problemas conhecidos
- Quando abrir o relatório pela primeira vez, apenas mostra a contagem e não o BrowserProgID. Para contornar este problema, edite a consulta para o relatório para a seguinte sintaxe:  
    `select BrowserProgId00 as BrowserProgId, Count(*) as Count`  
    `from DEFAULT_BROWSER_DATA as dbd`  
    `group by BrowserProgId00`

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as tarefas. Em seguida, enviar **comentários** do **home page** separador do Friso nos informar como correu.
1. No **do Configuration Manager** consola, **monitorização** área de trabalho, expanda **relatórios**, expanda **relatórios**, selecione **Software - empresas e produtos**.
2. Execute o **contagens de Browser predefinido** relatório.

Utilize a referência seguinte para BrowserProgIDs comuns:
- **AppXq0fevzme2pys62n3e0fbqa7peapykr8v**: Microsoft Edge
- **IE.HTTP**: Microsoft Internet Explorer
- **ChromeHTML**: Google Chrome
- **OperaStable**: Opera Software
- **FirefoxURL-308046B0AF4A39CB**: Mozilla Firefox



## <a name="support-for-windows-10-arm64-devices"></a>Suporte para dispositivos Windows 10 ARM64
<!-- 1353704 -->
A partir desta versão que cliente do Configuration Manager é suportado em dispositivos Windows 10 ARM64. As funcionalidades de gestão existentes do cliente deverá trabalhar com estes novos dispositivos. Por exemplo, hardware e inventário de software, atualizações de software e gestão de aplicações. Implementação do sistema operativo não é atualmente suportada. 

## <a name="changes-to-phased-deployments"></a>Alterações das implementações faseada
<!-- 1357405 -->
Implementações faseadas automatizam uma coordenada, sequenciada implementação de software através de várias coleções. Nesta versão do Technical Preview, o Assistente de implementação faseada pode ser concluído para sequências de tarefas na consola de administração e as implementações são criadas. No entanto, a segunda fase não for iniciado automaticamente após que satisfaçam os critérios de sucesso da primeira fase. A segunda fase pode ser manualmente iniciada com uma instrução SQL.   

### <a name="try-it-out"></a>Experimente!  
  Experimente concluir as tarefas. Em seguida, enviar **comentários** do **home page** separador do Friso nos informar como correu.
 
**Criar uma implementação faseada para uma sequência de tarefas** </br>
1. No **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.
2. Faça duplo clique na sequência de tarefas existente e selecione **criar implementação fases**. 
3. No **geral** separador, atribua a implementação faseada um nome, descrição (opcional) e selecione **criar automaticamente uma implementação de fase dois predefinido**. 
4. Preencher o **primeira coleção** e **segunda coleção** campos. Selecione **seguinte**.
5. No **definições** separador, escolha uma opção para cada uma das definições de agendamento e selecione **seguinte** quando concluir. 
6. No **fases** separador, editar qualquer das fases, se necessário, em seguida, clique em **seguinte**.
7. Confirme as suas seleções no **resumo** separador, em seguida, clique em **seguinte** para continuar.
8. Quando for atingida os critérios de êxito para a primeira fase, siga as instruções para a segunda fase de começar com uma instrução SQL.
 
**Segunda fase de começar com uma instrução SQL**
1. Identificar PhasedDeploymentID para a implementação que criou com a seguinte consulta SQL:<br/> `Select * from PhasedDeployment`
2. Execute a seguinte instrução para iniciar a fase de produção:<br/> `UPDATE PhasedDeployment SET EvaluatePhasedDeployment = 1, Action = 3 WHERE PhasedDeploymentID = <Phased Deployment ID>`


## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre instalar ou atualizar o ramo de pré-visualização técnica, consulte [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    

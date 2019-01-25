---
title: Technical Preview 1802 | Microsoft Docs
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis na versão 1802 Technical Preview do System Center Configuration Manager.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 7ff02203efac1802db166fef4a1c5a65d1b72615
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898533"
---
# <a name="capabilities-in-technical-preview-1802-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1802 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1802. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. 

Revisão [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview) antes de instalar esta versão do technical preview. Nesse artigo familiariza com os requisitos gerais e limitações para a utilização de uma technical preview, como ao atualizar entre versões e como fornecer comentários.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->
## <a name="known-issues-in-this-technical-preview"></a>Problemas conhecidos neste Technical Preview
- **Atualização para uma nova versão de pré-visualização falha quando tem um servidor de site em modo passivo**. Se tiver um [servidor do site primário em modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), em seguida, tem de desinstalar o servidor do site de modo passivo antes de atualizar para esta nova versão de pré-visualização. Pode reinstalar o servidor do site de modo passivo após a atualização do seu site estiver concluída.

  Para desinstalar o servidor do site de modo passivo:
  1. Na consola do Configuration Manager, aceda a **Administration** > **descrição geral** > **configuração do Site**  >  **Servidores e funções de sistema de sites**e, em seguida, selecione o servidor de site de modo passivo.
  2. Na **funções do sistema de sites** painel, o botão direito do mouse no **servidor do Site** função e, em seguida, escolha **remover função**.
  3. Faça duplo clique no servidor do site de modo passivo e, em seguida, escolha **eliminar**.
  4. Depois de desinstala o servidor do site, no servidor do site primário active reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.
  <!--sms 489412-->


</br>

**Seguem-se os novos recursos, que pode experimentar com esta versão.**  


## <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Carga de trabalho de proteção de ponto final de transição para o Intune através de cogestão    
<!-- 1357365 --> Nesta versão, agora é possível passar a Endpoint Protection carga de trabalho do Configuration Manager para o Intune depois de ativar a cogestão. Para fazer a transição da carga de trabalho do Endpoint Protection, vá para a página de propriedades de cogestão e mova a barra de controlo de deslize do Configuration Manager para **piloto** ou **todos os**. Para obter detalhes, consulte [cogestão para dispositivos Windows 10](/sccm/core/clients/manage/co-management-overview).


 
## <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configurar a Otimização da entrega do Windows para utilizar grupos de limites do Configuration Manager
<!-- 1324696 --> Utilizar grupos de limites do Configuration Manager para definir e regular a distribuição de conteúdo em sua rede empresarial e em escritórios remotos. [Otimização da entrega do Windows](/windows/deployment/update/waas-delivery-optimization) é uma tecnologia baseada na cloud, o ponto-a-ponto para partilhar conteúdo entre os dispositivos Windows 10. A partir desta versão, configure a otimização de entrega a utilizar os grupos de limites, quando partilha de conteúdo entre elementos de rede. Um nova definição de cliente aplica-se o identificador de grupo de limites como o identificador de grupo de Otimização da entrega no cliente. Quando o cliente comunica com o serviço de cloud de otimização de entrega, ele usa esse identificador para localizar os colegas com os conteúdos pretendidos. 

### <a name="prerequisites"></a>Pré-requisitos
- Otimização da entrega só está disponível em clientes Windows 10

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie **comentários** da **home page** separador do Friso nos informar como correu.

1. Na consola do Configuration Manager, **Administration** área de trabalho **definições de cliente** nó, criar uma política de definições personalizadas de cliente.
2. Selecione a nova **Otimização da entrega** grupo.
3. Ativar a definição **utilizar grupos de limites de Gestor de configuração para o ID de grupo de otimização de entrega**.

Para obter mais informações, consulte a **grupo** opção de modo de entrega na [opções de Otimização da entrega](/windows/deployment/update/waas-delivery-optimization#group-id).



## <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Sequência de tarefas de atualização in-loco do Windows 10 através do gateway de gestão da cloud
<!-- 1357149 -->

O Windows 10 [sequência de tarefas atualização in-loco](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version) agora oferece suporte à implantação para os clientes baseados na internet geridos através do [gateway de gestão da nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Esta capacidade permite aos usuários remotos mais facilmente atualizar para o Windows 10, sem terem de se ligar à rede empresarial. 

Certifique-se de que todo o conteúdo referenciado pela sequência de tarefas de atualização in-loco é distribuído para um [ponto de distribuição da nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). Caso contrário, os dispositivos não é possível executar a sequência de tarefas.

Quando implementa uma sequência de tarefas de atualização, utilize as seguintes definições:
- **Permitir que a sequência de tarefas executar o cliente na Internet**, no separador experiência de utilizador da implementação.
- **Transferir todo o conteúdo localmente antes de iniciar a sequência de tarefas**, no separador de pontos de distribuição da implantação. Outras opções, como **transferir o conteúdo localmente quando necessário para a sequência de tarefas em execução** não funcionar neste cenário. O motor de sequência de tarefas é atualmente não é possível obter o conteúdo a partir de um ponto de distribuição de nuvem. O cliente do Configuration Manager tem de transferir o conteúdo do ponto de distribuição de cloud antes de iniciar a sequência de tarefas.
- (*Opcional*) **pré-transferir conteúdos para esta sequência de tarefas**, na guia Geral da implantação. Para obter mais informações, consulte [configurar pré-armazenar conteúdo em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Melhoramentos à sequência de tarefas de atualização in-loco do Windows 10
<!-- 1357425 --> O modelo de sequência de tarefas padrão para a atualização in-loco do Windows 10 inclui agora grupos adicionais com as ações recomendadas para adicionar antes e depois do processo de atualização. Estas ações são comuns entre muitos clientes que estão com êxito a atualizar dispositivos Windows 10. 

### <a name="new-groups-under-prepare-for-upgrade"></a>Novos grupos em **preparar para atualização**
- **Verificações da bateria**: Adicione passos neste grupo para verificar se o computador está utilizar bateria ou alimentação. Esta ação requer um script personalizado ou o utilitário para executar esta verificação.
- **Verificações de ligação de rede/wired**: Adicione passos neste grupo para verificar se o computador está ligado a uma rede e não está a utilizar uma conexão sem fio. Esta ação requer um script personalizado ou o utilitário para executar esta verificação.
- **Remover aplicações incompatíveis**: Adicione passos neste grupo para remover todas as aplicações que são incompatíveis com esta versão do Windows 10. O método para desinstalar uma aplicação varia. Se o aplicativo usa o Windows Installer, copie os **programa de desinstalação** linha de comandos da **programas** separador Propriedades do tipo de implementação do Windows Installer do aplicativo. Em seguida, adicione uma **executar linha de comandos** passo neste grupo com a linha de comando do programa de desinstalação. Por exemplo: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Remover controladores incompatíveis**: Adicione passos neste grupo para remover todos os controladores que são incompatíveis com esta versão do Windows 10.
- **Remover/suspender a segurança de terceiros**: Adicione passos neste grupo para remover ou suspender programas de segurança de terceiros, como um antivírus.
   - Se estiver a utilizar um programa de encriptação de disco de terceiros, forneça o respectivo driver de encriptação à configuração do Windows com o **/ReflectDrivers** [opção da linha de comandos](/windows-hardware/manufacture/desktop/windows-setup-command-line-options). Adicionar uma [Set Task Sequence Variable](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) passo à sequência de tarefas neste grupo. Defina a variável de sequência de tarefas **OSDSetupAdditionalUpgradeOptions**. Defina o valor como **/ReflectDriver** com o caminho para o controlador. Isso [variável de ação de sequência de tarefas](/sccm/osd/understand/task-sequence-action-variables#upgrade-operating-system) acrescenta a configuração do Windows da linha de comandos utilizado pela sequência de tarefas. Contacte o fabricante de software para obter orientações adicionais sobre este processo.

### <a name="new-groups-under-post-processing"></a>Novos grupos em **pós-processamento**
- **Aplicar controladores baseados na configuração**: Adicione passos neste grupo para instalar controladores baseados na configuração (.exe) dos pacotes.
- **Instalar/ativar segurança de terceiros**: Adicione passos neste grupo para instalar ou ativar programas de segurança de terceiros, como um antivírus. 
- **Definir aplicações predefinidas do Windows e associações**: Adicione passos neste grupo para definir aplicações predefinidas do Windows e associações de arquivo. Em primeiro lugar, prepare um computador de referência com suas associações de aplicação pretendida. Em seguida, execute a seguinte linha de comando para exportar: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Adicione o ficheiro XML a um pacote. Em seguida, adicione uma [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) passo neste grupo. Especifique o pacote que contém o arquivo XML e, em seguida, especifique a linha de comandos: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Para obter mais informações, consulte [exportação ou importação predefinido associações de aplicativos](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).
- **Aplicar personalizações e personalização**: Adicione passos neste grupo para aplicar personalizações do menu Iniciar, por exemplo, organizar grupos de programas. Para obter mais informações, consulte [personalizar o ecrã de início](/windows-hardware/manufacture/desktop/customize-the-start-screen).

### <a name="additional-recommendations"></a>Recomendações adicionais
- Consulte a documentação de Windows para [erros de atualização do Windows 10 resolver](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Este artigo também contém informações detalhadas sobre o processo de atualização.
- A predefinição **verificar disponibilidade** passo, ative **assegurar espaço mínimo livre em disco (MB)**. Defina, pelo menos, o valor como **16384** (16 GB) para um sistema operacional de 32 bits Atualize o pacote, ou **20480** (20 GB) de 64 bits. 
- Utilize o **SMSTSDownloadRetryCount** [variável de sequência de tarefas incorporadas](/sccm/osd/understand/task-sequence-built-in-variables) para transferir política de repetição. Atualmente por predefinição, o cliente tenta novamente duas vezes; Esta variável é definida como duas (2). Se seus clientes não estiverem numa conexão de rede empresarial com fios, tentativas adicionais ajudam o cliente obter a política. Utilizar esta variável faz com que nenhum efeito negativo, que não seja atrasada falha se ele não é possível transferir a política.<!-- 501016 --> Também aumentar o **SMSTSDownloadRetryDelay** variável da predefinição de 15 segundos.
- Efetue uma avaliação de compatibilidade de inline. 
   - Adicione um segundo **atualizar sistema operativo** entrar no início do **preparar para a atualização** grupo. Atribua o nome *avaliação da atualização*. Especifique o pacote de atualização do mesmo e, em seguida, ativar a opção para **análise de compatibilidade de executar a configuração do Windows sem iniciar a atualização**. Ativar **continuar com o erro** no separador de opções. 
   - Imediatamente após isso *avaliação da atualização* passo, adicione um **executar linha de comandos** passo. Especifica a seguinte linha de comando:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Sobre o **opções** separador, adicione a seguinte condição: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Este código de retorno é o equivalente decimal MOSETUP_E_COMPAT_SCANONLY (0xC1900210), que é uma análise de compatibilidade bem-sucedida sem problemas. Se o *avaliação da atualização* passo for concluída com êxito e devolve esse código, este passo é ignorado. Caso contrário, se o passo de avaliação retornar qualquer outro código de retorno, este passo falha a sequência de tarefas com o código de retorno da análise de compatibilidade de configuração do Windows.
   - Para obter mais informações, consulte [atualizar sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).
- Se pretender alterar o dispositivo de BIOS para UEFI durante esta sequência de tarefas, consulte [converter BIOS para UEFI durante uma atualização in-loco](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

Envie **comentários** partir a **home page** separador do Friso caso tenha outras recomendações ou sugestões.



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Melhorias aos pontos de distribuição com PXE ativado
<!-- 1357580 --> Para esclarecer o comportamento de [nova funcionalidade PXE](/sccm/core/get-started/capabilities-in-technical-preview-1706#pxe-network-boot-support-for-ipv6) introduzido pela primeira vez na versão de pré-visualização técnica 1706, renomeamos a **suporte IPv6** opção. Sobre o **PXE** separador de propriedades do ponto de distribuição, verificação **ativar um dispositivo de resposta PXE sem o serviço de implementação do Windows**. 

Esta opção permite que um dispositivo de resposta do PXE no ponto de distribuição, o que não necessite de serviços de implantação do Windows (WDS). Se ativar esta opção nova num ponto de distribuição que já está preparado para PXE, o Configuration Manager suspende o serviço WDS. Se desativar esta opção nova, mas ainda **ativar suporte PXE para clientes**, em seguida, o ponto de distribuição permite que o WDS novamente.

Uma vez que o WDS não é necessário, o ponto de distribuição com PXE ativado pode ser um sistema de operativo cliente ou servidor, incluindo o Windows Server Core. Este novo serviço de resposta do PXE continua a oferecer suporte a IPv6 e também melhora a flexibilidade de pontos de distribuição com PXE ativado em escritórios remotos.

> [!NOTE]
> Este serviço utiliza a mesma tecnologia fundamental, como o [serviço de resposta baseada no cliente PXE](/sccm/core/get-started/capabilities-in-technical-preview-1712#client-based-pxe-responder-service) na versão de Technical Preview versão 1712. Essa funcionalidade não requer a sobrecarga da função de ponto de distribuição.

### <a name="multicast"></a>Multicast
Para ativar e configurar o multicast no **Multicast** separador Propriedades do ponto de distribuição, o ponto de distribuição tem de utilizar o WDS. 
- Se **ativar suporte PXE para clientes** e **ativar multicast para enviar dados em simultâneo a múltiplos clientes**, em seguida, não pode **ativar um dispositivo de resposta PXE sem o serviço de implementação do Windows** .
- Se **ativar suporte PXE para clientes** e **ativar um dispositivo de resposta PXE sem o serviço de implementação do Windows**, em seguida, não pode **ativar multicast para enviar dados em simultâneo a múltiplos clientes**



## <a name="deployment-templates-for-task-sequences"></a>Modelos de implementação para sequências de tarefas
<!-- 1357391 --> O Assistente de implementação para sequências de tarefas pode criar um modelo de implementação. O modelo de implementação pode ser salvo e aplicado a uma sequência de tarefas nova ou existente para criar uma implementação. 

### <a name="try-it-out"></a>Experimente!  
Experimente concluir as tarefas. Em seguida, envie **comentários** da **home page** separador do Friso nos informar como correu. 

 **Criar um modelo de implementação para uma nova implementação de sequência de tarefas** <br/> 
1. Na **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.
2. Com o botão direito numa sequência de tarefas e selecione **Deploy**. 
3. Sobre o **gerais** separador, tenha em atenção de que existe agora uma opção para **selecionar modelo de implementação**. 
4. Continuar através do **Assistente de implementação de Software** selecionar as definições de implementação para a sequência de tarefas. 
5. Quando chegar a **resumo** separador da **Assistente de implementação de Software**, clique em **Salvar como modelo**.
6. Dê um nome ao modelo e selecione as definições para guardar no modelo. 
7. Clique em **Guardar**. O modelo agora está disponível para utilização a partir da **selecionar modelo de implementação** opção.



## <a name="product-lifecycle-dashboard"></a>Dashboard de ciclo de vida do produto
<!--1319632--> A nova [dashboard ciclo de vida do produto](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard) mostra o estado da política de ciclo de vida de produto de Microsoft para produtos Microsoft instalados nos dispositivos geridos com o Configuration Manager. O dashboard fornece informações sobre os produtos da Microsoft no seu ambiente, o estado de capacidade de suporte e datas de término do suporte. Pode utilizar o dashboard para compreender a disponibilidade de suporte para cada produto. 

Para aceder ao Dashboard do ciclo de vida, na consola do Configuration Manager, aceda a **ativos e compatibilidade** >**Asset Intelligence** >**ciclo de vida do produto**



## <a name="improvements-to-reporting"></a>Melhorias aos relatórios
<!--1357653--> Como resultado de [seus comentários](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and) adicionamos um novo relatório **detalhes de manutenção do Windows 10 para uma coleção específica**. Este relatório mostra o ID de recurso, nome NetBIOS, nome do SO, o nome de versão do SO, compilação, ramo de SO e manutenção de estado para dispositivos Windows 10. Para aceder ao relatório, aceda a **monitorização** >**relatórios** >**relatórios** >**sistemas de operativos**  > **Detalhes da manutenção do Windows 10 para uma coleção específica**.



## <a name="improvements-to-software-center"></a>Melhoramentos ao centro de Software
<!--1357592--> Como resultado de [seus comentários](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid) agora é possível ocultar aplicações instaladas no Centro de Software. Aplicações que já estão instalados já não aparecerá no separador aplicações quando esta opção está ativada. 

### <a name="try-it-out"></a>Experimente!
Ativar a **Ocultar aplicações instaladas no Centro de Software** definição nas definições do Centro de Software de cliente. Observe o comportamento no Centro de Software quando o utilizador final instala uma aplicação.



## <a name="improvements-to-run-scripts"></a>Melhorias para executar Scripts
<!--1236459--> O [executar Scripts](/sccm/apps/deploy-use/create-deploy-scripts) funcionalidade devolve agora com a formatação do JSON de saída do script. Este formato consistentemente devolve uma saída de script legível. Scripts que falham para executar não podem obter o resultado devolvido. 



## <a name="boundary-group-fallback-for-management-points"></a>Contingência para pontos de gestão do grupo de limites
<!-- 1324594 --> A partir desta versão, pode configurar as relações de contingência para pontos de gestão entre [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups). Esse comportamento fornece maior controle para os pontos de gestão que os clientes utilizam. Sobre o **relações** separador de propriedades do grupo de limites, há uma nova coluna para o ponto de gestão. Quando adiciona um novo grupo de limites de contingência, o tempo de contingência para o ponto de gestão é atualmente sempre zero (0). Este comportamento é o mesmo para o **comportamento padrão** no grupo de limite predefinido do site.

Anteriormente, um problema comum ocorre quando tem um protegido ponto de gestão numa rede segura. Os clientes na rede corporativa principal recebem uma política que inclui este ponto de gestão protegidos, mesmo que não conseguem comunicar com ele através de uma firewall. Para resolver esse problema, utilize o **Never contingência** opção para garantir que apenas fallback para a gestão de clientes aponta com que eles possam comunicar.

Ao atualizar o site para esta versão, o Configuration Manager adiciona todos os pontos de gestão de não-acesso à internet ao grupo de limite predefinido do site. Esse comportamento de atualização garante que as versões mais antigas do cliente continuam a comunicar com pontos de gestão. Para tirar partido desta funcionalidade, mova os pontos de gestão para os grupos de limites pretendido.

Contingência de grupo de limite de ponto de gestão não altera o comportamento durante a instalação de cliente (ccmsetup). Se a linha de comandos não especificar o ponto de gestão inicial usando o parâmetro /MP, o novo cliente recebe a lista completa de pontos de gestão disponíveis. Para o processo de arranque de configuração inicial, o cliente utiliza o primeiro ponto de gestão que possa aceder. Assim que o cliente registra com o site, ele recebe a lista de pontos de gestão ordenada corretamente com esse novo comportamento. 

### <a name="prerequisites"></a>Pré-requisitos
- Ativar [pontos de gestão preferenciais](/sccm/core/servers/deploy/configure/boundary-groups#preferred-management-points). Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **configuração do Site** e selecione **Sites**. Clique em **definições de hierarquia** na faixa de opções. Sobre o **gerais** separador, ative **os clientes preferem utilizar pontos de gestão especificados em grupos de limites**. 

### <a name="known-issues"></a>Problemas conhecidos
- Processos de implementação do sistema operativo não têm conhecimento de grupos de limites.

### <a name="troubleshooting"></a>Resolução de Problemas
Novas entradas são apresentados no **Locationservices**. O **Localidade** atributo identifica um dos seguintes Estados:
- 0: Desconhecido
- 1: O ponto de gestão especificado é apenas o grupo de limite predefinido de site de contingência
- 2: O ponto de gestão especificado está num grupo de limites da vizinhança ou remoto. Quando o ponto de gestão está num vizinho e os grupos de limites do site padrão, a Localidade é 2.
- 3: O ponto de gestão especificado está no grupo de limites atual ou local. Quando o ponto de gestão está no grupo de limites atual, bem como um vizinho ou o grupo de limite predefinido de site, a Localidade é 3. Se não ativar os pontos de gestão preferenciais definição nas definições de hierarquia, a Localidade é sempre 3, independentemente da que limite o ponto de gestão de grupo está em.

Os clientes utilizam pontos de gestão local primeiro (Localidade de 3), segundo remoto (Localidade de 2), em seguida, contingência (Localidade de 1). 

Quando um cliente recebe erros de cinco em dez minutos e não consegue comunicar com um ponto de gestão no seu grupo de limite atual, ele tenta contactar um ponto de gestão num vizinho ou do grupo de limite predefinido do site. Se o ponto de gestão mais tarde o grupo de limites atual estiver online novamente, o cliente irá devolver ao ponto de gestão local no próximo ciclo de atualização. O ciclo de atualização é de 24 horas, ou quando reinicia o serviço de agente do Configuration Manager.



## <a name="improved-support-for-cng-certificates"></a>Suporte aprimorado para certificados CNG
<!-- 1357314 --> Configuration Manager (ramo atual) versão 1710 suporta [Cryptography: Certificados de próxima geração (CNG)](/sccm/core/plan-design/network/cng-certificates-overview). Limites de versão 1710 suportam para certificados de cliente em vários cenários. 

A partir desta versão de pré-visualização técnica, utilize certificados CNG para as seguintes funções de servidor com capacidade para HTTPS:
- Ponto de gestão
- Ponto de distribuição
- Ponto de atualização de software

A lista de [não suportado cenários](/sccm/core/plan-design/network/cng-certificates-overview#unsupported-scenarios) permanece o mesmo.



## <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Suporte do gateway de gestão da cloud para o Azure Resource Manager
<!-- 1324735 --> Ao criar uma instância do [gateway de gestão na cloud](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG), o assistente agora fornece a opção para criar um **implementação Azure Resource Manager**. [O Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para o gerenciamento de todos os recursos de solução como uma única entidade, chamada um [grupo de recursos](/azure/azure-resource-manager/resource-group-overview#resource-groups). Quando implementa o CMG com o Azure Resource Manager, o site utiliza o Azure Active Directory (Azure AD) para autenticar e criar os recursos da cloud necessários. Esta implementação reestruturação não requer o certificado de gestão clássico do Azure.  

O assistente CMG ainda fornece a opção para um **implementação de serviço clássico** a utilizar um certificado de gestão do Azure. Para simplificar a implementação e gestão de recursos, recomendamos que utilize o modelo de implementação Azure Resource Manager para todas as novas instâncias do CMG. Se possível, volte a implementar instâncias CMG existentes através do Resource Manager.

O Configuration Manager não migra instâncias existentes de CMG clássicas ao modelo de implementação Azure Resource Manager. Criar novas instâncias CMG com implementações do Azure Resource Manager e, em seguida, remover instâncias CMG clássicas. 

> [!IMPORTANT]
> Esta capacidade não ativa o suporte para fornecedores de serviços de Cloud do Azure (CSP). A implementação do CMG com o Azure Resource Manager continua a utilizar o serviço cloud clássico, que não suporta o CSP. Para obter mais informações, consulte [serviços do Azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="prerequisites"></a>Pré-requisitos
- Integração com o [do Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Deteção de utilizadores do Azure AD não é necessária.
- O mesmo [requisitos do gateway de gestão da cloud](/sccm/core/clients/manage/plan-cloud-management-gateway#requirements-for-cloud-management-gateway), exceto para o certificado de gestão do Azure.

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as tarefas. Em seguida, envie **comentários** da **home page** separador do Friso nos informar como correu.

1. Na consola do Configuration Manager, **Administration** área de trabalho, expanda **serviços Cloud**e selecione **Gateway de gestão da nuvem**. Clique em **criar Gateway de gestão de Cloud** na faixa de opções. 
2. Sobre o **gerais** página, selecione **implementação Azure Resource Manager**. Clique em **iniciar sessão** para autenticar com uma conta de administrador de subscrição do Azure. O assistente é preenchido automaticamente os campos restantes das informações de subscrição do Azure AD armazenados durante a pré-requisitos de integração. Se tiver várias subscrições, selecione a subscrição pretendida a utilizar. Clique em **Seguinte**.  
3. Sobre o **definições** , indique o servidor de ficheiro de certificado PKI como de costume. Este certificado define o nome do serviço CMG no Azure. Selecione o **região**e, em seguida, selecione uma opção de grupo de recursos de **criar nova** ou **utilizar existente**. Introduza o nome do grupo de recursos novo ou selecione um grupo de recursos existente na lista pendente. 
4. Conclua o assistente.

> [!NOTE] 
> Para o Azure AD selecionado aplicação de servidor, o Azure atribui a subscrição **contribuinte** permissão. 

Monitorizar o progresso da implementação de serviço com **cloudmgr** no ponto de ligação de serviço.



## <a name="approve-application-requests-for-users-per-device"></a>Aprovar pedidos de aplicações para utilizadores por dispositivo
<!-- 1357015 --> A partir desta versão, quando um utilizador solicita um aplicativo que necessite de aprovação, o nome de dispositivo específico é agora uma parte do pedido. Se o administrador aprova o pedido, o utilizador só é possível instalar o aplicativo nesse dispositivo. O utilizador tem de submeter outro pedido para instalar a aplicação noutro dispositivo. 

> [!NOTE]
> Esta funcionalidade é opcional. Ao atualizar para esta versão, habilite esse recurso no Assistente de atualização. Em alternativa, ative a funcionalidade na consola mais tarde. Para mais informações, consulte [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).

### <a name="prerequisites"></a>Pré-requisitos
- Atualizar o cliente do Configuration Manager para a versão mais recente
- Ativar a definição de cliente **utilizar o novo Centro de Software** no [agente do computador](/sccm/core/clients/deploy/about-client-settings#computer-agent) grupo

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie **comentários** da **home page** separador do Friso nos informar como correu.

1. Implemente uma aplicação como disponível para uma coleção de utilizadores.
2. Sobre o **definições de implementação** página, ative a opção: **Um administrador tem de aprovar um pedido para esta aplicação no dispositivo**.
3. Como um utilizador visado, utilize o Centro de Software para submeter um pedido para a aplicação. 
4. Modo de exibição **pedidos de aprovação** sob **gestão de aplicações** no **biblioteca de Software** área de trabalho da consola do Configuration Manager. Existe agora uma **dispositivo** coluna na lista para cada solicitação. Quando pega a ação na solicitação, a caixa de diálogo de pedido de aplicação também inclui o nome de dispositivo a partir do qual o utilizador submeteu o pedido.



## <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Utilizar o Centro de Software para procurar e instalar aplicações disponíveis para o utilizador em dispositivos associados ao AD Azure
<!-- 1322613 --> Se implementar aplicações como disponíveis para os utilizadores, agora pode procurar e instalá-los através do Centro de Software em dispositivos do Azure Active Directory (Azure AD).  

### <a name="prerequisites"></a>Pré-requisitos
- Ativar o HTTPS no ponto de gestão
- Integrar o site com [do Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure)
- Implementar uma aplicação como disponível para uma coleção de utilizadores
- Distribuir qualquer conteúdo da aplicação para um [ponto de distribuição da nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)
- Ativar a definição de cliente **utilizar o novo Centro de Software** no [agente do computador](/sccm/core/clients/deploy/about-client-settings#computer-agent) grupo
- O cliente tem de ser: 
   - Windows 10
   - O Azure AD associado, também conhecido como na cloud associados a um domínio
- Para suportar clientes baseados na internet:
    - [Gateway de gestão na cloud](/sccm/core/clients/manage/plan-cloud-management-gateway) 
    - Ative a definição de cliente: **Ativar pedidos da política de utilizador dos clientes Internet** no [política de cliente](/sccm/core/clients/deploy/about-client-settings#client-policy) grupo
- Para suportar clientes na rede empresarial:
    - Adicionar o ponto de distribuição de nuvem a um grupo de limites usado pelos clientes
    - Os clientes devem ser capazes de resolver o nome de domínio completamente qualificado (FQDN) do ponto de gestão ativado para HTTPS



## <a name="report-on-windows-autopilot-device-information"></a>Relatório sobre as informações de dispositivo do Windows AutoPilot
<!-- 1351442 --> Windows AutoPilot é uma solução de integração e a configuração de novos dispositivos Windows 10 de uma maneira moderna. Para obter mais informações, consulte um [descrição geral do Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). É um método de registo de dispositivos existentes no Windows AutoPilot carregar as informações de dispositivo para a Microsoft Store para empresas e Education. Estas informações incluem o número de série do dispositivo, o identificador do produto Windows e um identificador de hardware. Utilize o Gestor de configuração para recolher e comunicar estas informações de dispositivo. 

### <a name="prerequisites"></a>Pré-requisitos
- Estas informações de dispositivo só se aplica aos clientes no Windows 10, versão 1703 e posteriores

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie **comentários** da **home page** separador do Friso nos informar como correu.

1. Na consola do Configuration Manager, **monitorização** área de trabalho, expanda o **Reporting** nó, expanda **relatórios**e selecione o **Hardware - geral**  nó.
2. Executar o novo relatório **informações de dispositivo do Windows AutoPilot** e ver os resultados. 
3. No Visualizador de relatórios clique a **exportar** ícone e selecione **CSV (delimitado por vírgulas)** opção.
4. Depois de guardar o ficheiro, carregue os dados para a Microsoft Store para empresas e Education. Para obter mais informações, consulte [adicionar dispositivos no Microsoft Store para empresas e educação](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile). 



## <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Melhorias às políticas do Configuration Manager para o Windows Defender exploram Guard
<!-- 1356220 --> Foram adicionadas definições de política adicionais para os componentes de acesso à pasta de redução da superfície de ataque e controlado no Configuration Manager para [Windows Defender Exploit Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard).

**Novas definições para o acesso a pastas controladas**<br/>
Existem duas opções adicionais ao configurar o acesso a pastas controladas: **Bloquear apenas os setores de disco** e **auditar apenas os setores de disco**. Estas duas definições permitir o acesso a pastas controladas ser ativada para apenas os setores de inicialização e não ative a proteção de pastas específicas ou as pastas padrão protegido. 

**Novas definições para a redução da superfície de ataque**
- Utilize a proteção avançada contra ransomware.
- Impedir o roubo do subsistema de autoridade de segurança local do Windows de credenciais. 
- Impeça ficheiros executáveis de serem executados a menos que cumpram uma lista de critérios de prevalência, idade ou fidedignidade. 
- Bloqueie processos não fidedignos e não assinados executados a partir de USB.



## <a name="microsoft-edge-browser-policies"></a>Políticas de browser Microsoft Edge
<!-- 1357310 --> Para os clientes que utilizam o [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) navegador da web em clientes do Windows 10, agora, pode criar uma política de definições de compatibilidade do Configuration Manager para configurar várias definições do Microsoft Edge. Atualmente, esta política inclui as seguintes definições:
- **Browser Microsoft Edge de conjunto como predefinição**: Configura a definição de aplicação de browser do Microsoft Edge predefinida de Windows 10
- **Permitir o endereço de barra pendente**: Requer o Windows 10, versão 1703 ou posterior. Para obter mais informações, consulte [política de browser AllowAddressBarDropdown](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Sincronizar favoritos entre browsers da Microsoft de permitir**: Requer o Windows 10, versão 1703 ou posterior. Para obter mais informações, consulte [política de browser SyncFavoritesBetweenIEAndMicrosoftEdge](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Permitir a limpar dados de navegação à saída**: Requer o Windows 10, versão 1703 ou posterior. Para obter mais informações, consulte [política de browser ClearBrowsingDataOnExit](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Permitir cabeçalhos não controlar**: Para obter mais informações, consulte [política de browser AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Permitir Preenchimento automático**: Para obter mais informações, consulte [política de browser AllowAutofill](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Permitir cookies**: Para obter mais informações, consulte [política de browser AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Permitir Bloqueador de pop-up**: Para obter mais informações, consulte [política de browser AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Permitir sugestões de pesquisa na barra de endereço**: Para obter mais informações, consulte [política de browser AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Permitir o envio de tráfego de intranet para o Internet Explorer**: Para obter mais informações, consulte [política de browser SendIntranetTraffictoInternetExplorer](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Permitir Gestor de palavra-passe**: Para obter mais informações, consulte [política de browser AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Permitir ferramentas de programação**: Para obter mais informações, consulte [política de browser AllowDeveloperTools](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Permitir extensões**: Para obter mais informações, consulte [política de browser AllowExtensions](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).

### <a name="prerequisites"></a>Pré-requisitos
- Cliente do Windows 10 que estiver associado a um Azure Active Directory. 

### <a name="known-issues"></a>Problemas conhecidos
- Dispositivos de associados a um domínio no local não é possível aplicar esta política nesta versão. Este problema também diz respeito a dispositivos associados a um domínio de híbrida.

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as tarefas. Em seguida, envie **comentários** da **home page** separador do Friso nos informar como correu.

**Criar a política**
1. Na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho. Expanda **definições de compatibilidade** e selecione a nova **perfis de Browser do Microsoft Edge** nó. Clique na opção de faixa de opções para **criar política de Browser do Microsoft Edge**.
2. Especifique um **Name** para a política, opcionalmente, introduza um **Descrição**e clique em **seguinte**.
3. Sobre o **definições** página, altere o valor para **configurado** para as definições a incluir nesta política e clique em **seguinte**.
4. Sobre o **plataformas suportadas** , selecione as versões de sistema operativo e arquiteturas para a qual esta política aplica-se e clique em **próxima**. 
5. Conclua o assistente.

**Implementar a política**
1. Selecione a política e clique na opção de faixa de opções para **Deploy**.
2. Clique em **procurar** para selecionar a coleção de utilizador ou dispositivo ao qual pretende implementar a política. 
3. Selecione as opções adicionais conforme necessário. Gere alertas quando a política não está em conformidade. Defina a agenda pela qual o cliente avalia a conformidade do dispositivo com esta política.
4. Clique em **OK** para criar a implementação.

Como qualquer política de definições de conformidade, o cliente efetua a remediação das definições na agenda que especificar. [Monitorizar e comunicar de conformidade do dispositivo](/sccm/compliance/deploy-use/monitor-compliance-settings) na consola do Configuration Manager.



## <a name="report-for-default-browser-counts"></a>Relatório de contagens de browser predefinido
<!-- 1357830 --> Agora há um novo relatório para mostrar a contagem de clientes com um navegador da web específicas como sendo o padrão do Windows. 

### <a name="known-issues"></a>Problemas conhecidos
- Primeira vez que abrir o relatório, apenas mostra a contagem e não o BrowserProgID. Para contornar este problema, edite a consulta para o relatório para a seguinte sintaxe:  
    `select BrowserProgId00 as BrowserProgId, Count(*) as Count`  
    `from DEFAULT_BROWSER_DATA as dbd`  
    `group by BrowserProgId00`

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as tarefas. Em seguida, envie **comentários** da **home page** separador do Friso nos informar como correu.
1. Na **Configuration Manager** consola, **monitorização** área de trabalho, expanda **relatórios**, expanda **relatórios**, selecione **Software - empresas e produtos**.
2. Executar o **contagens de Browser predefinido** relatório.

Utilize a seguinte referência para BrowserProgIDs comuns:
- **AppXq0fevzme2pys62n3e0fbqa7peapykr8v**: Microsoft Edge
- **IE.HTTP**: Microsoft Internet Explorer
- **ChromeHTML**: Google Chrome
- **OperaStable**: Opera Software
- **FirefoxURL-308046B0AF4A39CB**: Mozilla Firefox



## <a name="support-for-windows-10-arm64-devices"></a>Suporte para dispositivos Windows 10 ARM64
<!-- 1353704 --> A partir desta versão que cliente do Configuration Manager é suportado em dispositivos Windows 10 ARM64. Funcionalidades de gestão de cliente existentes devem trabalhar com esses novos dispositivos. Por exemplo, hardware e inventário de software, atualizações de software e gerenciamento de aplicativos. Implementação do sistema operativo não é atualmente suportada. 

## <a name="changes-to-phased-deployments"></a>Alterações para as implementações faseadas
<!-- 1357405 --> As implementações faseadas automatizam uma implementação coordenada e sequenciada de software entre várias coleções. Nesta versão do Technical Preview, o Assistente de implementação por fases que pode ser concluído para sequências de tarefas na consola de administração e implementações são criadas. No entanto, a segunda fase não for iniciado automaticamente depois que satisfaça os critérios de êxito da primeira fase. A segunda fase pode ser manualmente iniciada com uma instrução SQL.   

### <a name="try-it-out"></a>Experimente!  
  Experimente concluir as tarefas. Em seguida, envie **comentários** da **home page** separador do Friso nos informar como correu.
 
**Criar uma implementação faseada para uma sequência de tarefas** </br>
1. Na **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.
2. Com o botão direito na sequência de tarefas existente e selecione **criar implementação faseada**. 
3. Sobre o **gerais** separador, dê um nome, descrição (opcional), à implementação faseada e selecione **criar automaticamente uma implementação padrão em duas fases**. 
4. Preencher o **primeira coleção** e **segunda coleção** campos. Selecione **Seguinte**.
5. Sobre o **definições** separador, escolher uma opção para cada uma das definições de agendamento e selecione **próxima** quando terminar. 
6. Sobre o **fases** separador, edite qualquer uma das fases se for necessário, em seguida, clique em **próxima**.
7. Confirme as suas seleções no **resumo** separador, em seguida, clique em **próxima** para continuar.
8. Quando os critérios de êxito para a primeira fase for atingido, siga as instruções para iniciar a segunda fase com uma instrução SQL.
 
**Segunda fase de começar com uma instrução SQL**
1. Identificar o PhasedDeploymentID para a implementação que criou com a seguinte consulta SQL:<br/> `Select * from PhasedDeployment`
2. Execute a declaração seguinte para iniciar a fase de produção:<br/> `UPDATE PhasedDeployment SET EvaluatePhasedDeployment = 1, Action = 3 WHERE PhasedDeploymentID = <Phased Deployment ID>`


## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre a instalação ou a atualizar o ramo de pré-visualização técnica, veja [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    

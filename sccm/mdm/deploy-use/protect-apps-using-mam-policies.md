---
title: Proteger aplicações ao utilizar políticas de gestão de aplicações móveis
titleSuffix: Configuration Manager
description: Modificar a funcionalidade das aplicações que implementa para que atenderá a conformidade da empresa e as políticas de segurança.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 28115475-e563-4e16-bf30-f4c9fe704754
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7da4767bd8ef26ebf3f56010e99bc1cbd0b0c10
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120396"
---
# <a name="protect-apps-using-mobile-application-management-policies-in-system-center-configuration-manager"></a>Proteger aplicações através de políticas de gestão de aplicações móveis no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Políticas de gestão de aplicações do System Center Configuration Manager permitem-lhe modificar a funcionalidade das aplicações que implementa para ajudar a alinhá-los com a sua empresa políticas de conformidade e segurança. Por exemplo, pode restringir operações de corte, cópia e colagem numa aplicação restrita ou configurar uma aplicação para abrir todas as URLs num browser gerido. Suporte para políticas de gestão de aplicações:  

-   Dispositivos a executar o Android 4 e posterior  

-   Dispositivos que executam o iOS 9 e posteriores  

Também pode utilizar políticas de gestão de aplicações móveis para proteger aplicações em dispositivos que não são geridos pelo Intune. Através desta nova funcionalidade, pode aplicar políticas de gestão de aplicações móveis para aplicações que ligam a serviços do Office 365. Não é suportada para aplicações que se ligam a no local para o Exchange ou SharePoint.  

Para utilizar esta nova capacidade, terá de utilizar o portal de pré-visualização do Azure. Os tópicos seguintes podem ajudá-lo a familiarizar-se:  
- [Introdução às políticas de gestão de aplicações móveis no portal do Azure](https://technet.microsoft.com/library/mt627830.aspx)  
- [Criar e implementar políticas de gestão de aplicações móveis com o Microsoft Intune](https://technet.microsoft.com/library/mt627829.aspx)  

  Não implemente uma política de gestão de aplicações diretamente, tal como sucede com itens de configuração e linhas de base no Configuration Manager. Em vez disso, associa a política ao tipo de implementação da aplicação que pretende restringir. Quando o tipo de implementação de aplicação é implementado e instalado em dispositivos, as definições que especificar entrem em vigor.  

Para aplicar restrições a uma aplicação, a aplicação tem de incorporar o Microsoft Intune App Software Development Kit (SDK). Existem dois métodos para obter este tipo de aplicação:  

-   **Utilizar uma aplicação gerida por política** (Android e iOS): Estas aplicações têm o SDK da aplicação incorporado. Para adicionar este tipo de aplicação, especifique uma ligação para a aplicação a partir de uma loja de aplicações, como o iTunes ou o Google Play. Não é necessário processamento adicional para este tipo de aplicação. Para obter uma lista de aplicações geridas por política que estão disponíveis para dispositivos iOS e Android, veja [Aplicações geridas para as políticas de gestão de aplicações móveis do Microsoft Intune](https://technet.microsoft.com/library/dn708489.aspx).  

-   **Utilizar uma aplicação "encapsulada"** (Android e iOS): Estas aplicações são empacotadas novamente para incluir o SDK da aplicação através da **Microsoft Intune App Wrapping Tool**. Normalmente esta ferramenta é utilizada para processar aplicações da empresa que foram criadas internamente. Não pode ser utilizada para processar aplicações que foram transferidas a partir da loja de aplicações. Veja os artigos seguintes para obter mais informações:
    - [Preparar as aplicações iOS para gestão de aplicações móveis com a ferramenta de encapsulamento de aplicações do Microsoft Intune](https://technet.microsoft.com/library/dn878028.aspx)

    - [Preparar as aplicações Android para gestão de aplicações móveis com a ferramenta de encapsulamento de aplicações do Microsoft Intune](https://technet.microsoft.com/library/mt147413.aspx)  

## <a name="create-and-deploy-an-app-with-a-mobile-application-management-policy"></a>Criar e implementar uma aplicação com uma política de gestão de aplicações móveis  

##  <a name="step-1-obtain-the-link-to-a-policy-managed-app-or-create-a-wrapped-app"></a>Passo 1: Obter a ligação a uma aplicação gerida por política ou criar uma aplicação encapsulada  

-   **Para obter uma ligação para uma política de aplicação gerida**: Na loja de aplicações, encontre e anote o URL da aplicação gerida por política que pretende implementar.  

     Por exemplo, o URL da aplicação Microsoft Word para iPad é **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**  

-   **Para criar uma aplicação encapsulada**: Utilize as informações dos tópicos [preparar as aplicações iOS para gestão de aplicações móveis com a ferramenta de encapsulamento de aplicações do Microsoft Intune](https://technet.microsoft.com/library/dn878028.aspx) e [preparar aplicações Android para gestão de aplicações móveis com o Microsoft Intune Ferramenta de encapsulamento de aplicações](https://technet.microsoft.com/library/mt147413.aspx) para criar uma aplicação encapsulada.  

     A ferramenta cria uma aplicação processada e um ficheiro de manifesto associado. Utilizar estes ficheiros quando criar uma aplicação do Configuration Manager que contém a aplicação.  

##  <a name="step-2-create-a-configuration-manager-application-that-contains-an-app"></a>Passo 2: Criar uma aplicação do Configuration Manager que contenha uma aplicação  
 O procedimento para criar a aplicação do Configuration Manager difere quando se está a utilizar uma aplicação gerida por política (ligação externa) ou uma aplicação que foi criada utilizando a ferramenta de encapsulamento de aplicações do Microsoft Intune para iOS (pacote de aplicação para iOS). Utilize um dos seguintes procedimentos para criar a aplicação do Configuration Manager.  

1. Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **aplicativos**.  

2. No **home page** separador a **Create** de grupo, escolha **Criar aplicação** para abrir o **Criar aplicação** assistente.  

3. Na página **Geral** , selecione **Detetar automaticamente informação sobre esta aplicação nos ficheiros de instalação**.  

4. Na lista pendente **Tipo**, selecione **Pacote de aplicação para iOS (ficheiro \*.ipa)**.  

5. Escolher **navegue** para selecionar o pacote de aplicação que pretende importar e, em seguida, escolha **próxima**.  

6. Na página **Informações Gerais** , introduza o texto descritivo e as informações sobre a categoria que pretende que os utilizadores vejam no portal da empresa.  

7. Conclua o assistente.  

   A nova aplicação é apresentada no nó **Aplicações** da área de trabalho **Biblioteca de Software** .  

### <a name="create-an-application-that-contains-a-link-to-a-policy-managed-app"></a>Criar uma aplicação que contém uma ligação para uma aplicação gerida por política  

1. Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **aplicativos**.  

2. No **home page** separador a **Create** de grupo, escolha **Criar aplicação** para abrir o **Criar aplicação** assistente.  

3. Na página **Geral** , selecione **Detetar automaticamente informação sobre esta aplicação nos ficheiros de instalação**.  

4. Na lista pendente **Tipo** , selecione um dos seguintes:  

   -   Para iOS: **Pacote de aplicação para iOS da App Store**  

   -   Para Android: **Pacote de aplicação para Android no Google Play**  

5. Introduza o URL para a aplicação (a partir do passo 1) e, em seguida, escolha **seguinte**.  

6. Na página **Informações Gerais** , introduza o texto descritivo e as informações sobre a categoria que pretende que os utilizadores vejam no portal da empresa.  

7. Conclua o assistente.  

   A nova aplicação é apresentada no nó **Aplicações** da área de trabalho **Biblioteca de Software** .  

##  <a name="step-3-create-an-application-management-policy"></a>Passo 3: Criar uma política de gestão de aplicações  
 Em seguida, crie uma política de gestão de aplicações que associar à aplicação. Pode criar uma política de browser gerido ou geral.  

1)  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **políticas de gestão de aplicações** .  

2)  Na **home page** separador a **Create** de grupo, escolha **criar política de gestão de aplicações**.  

3)  Sobre o **gerais** página, introduza o nome e descrição para a política e, em seguida, escolha **próxima**.  

4)  Sobre o **tipo de política** página, selecione a plataforma e o tipo de política para esta política e, em seguida, escolha **próxima**. Estão disponíveis os seguintes tipos de política:  

-   **Geral**: O tipo de política geral permite modificar a funcionalidade das aplicações que implementa para ajudar a alinhá-los com a conformidade da empresa e as políticas de segurança. Por exemplo, pode restringir as operações de corte, cópia e colagem numa aplicação restrita.  

-   **Browser gerido**: A política de Browser gerido permite-lhe decidir se pretende permitir ou bloquear o browser gerido de abrir uma lista de URLs. A política de Browser Gerido permite modificar a funcionalidade da aplicação Intune Managed Browser. É um browser que lhe permite gerir as ações que os utilizadores podem realizar, incluindo os sites que podem visitar e como são abertas as ligações para conteúdo no browser. Saiba mais sobre a  [aplicação Intune Managed Browser para iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) e a [aplicação Intune Managed Browser para Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

5)  Sobre o **política para iOS** ou **política do Android** página, configure os seguintes valores conforme necessário e, em seguida, escolha **seguinte**. As opções podem variar dependendo do tipo de dispositivo para o qual está a configurar a política.  

|Valor|Mais informações|  
|-----------|----------------------|  
|**Restringir o conteúdo Web a apresentar num browser gerido pela empresa**|Permite que todas as ligações na aplicação para abrir no Browser gerido. Para esta opção funcionar, esta aplicação tem de estar implementada em dispositivos.|  
|**Impedir cópias de segurança de Android** ou **Impedir cópias de segurança de iTunes e iCloud**|Desativa a cópia de segurança de informações da aplicação.|  
|**Permitir que a aplicação transfira dados para outras aplicações**|Especifica as aplicações para as quais esta aplicação pode enviar dados. Pode optar por não permitir a transferência de dados para qualquer aplicação, apenas permitir a transferência para outras aplicações restritas ou permitir a transferência para qualquer aplicação.<br /><br /> Em dispositivos iOS, para impedir a transferência de documentos entre aplicações geridas e não geridas, também tem de configurar e implementar uma política de segurança de dispositivos móveis que desativa a definição **Permitir documentos geridos noutras aplicações não geridas**.<br /><br /> Se selecionar apenas permitir a transferência para outras aplicações restritas, os visualizadores de PDF do Intune e de imagem (se estiverem implementados) são utilizados para abrir conteúdos dos respetivos tipos.|  
|**Permitir que a aplicação receba dados de outras aplicações**|Especifica de que aplicações esta aplicação pode receber dados. Pode optar por não permitir a transferência de dados de qualquer aplicação, apenas permitir a transferência de outras aplicações restritas ou permitir a transferência de qualquer aplicação.|  
|**Impedir "Guardar Como"**|Desativa a utilização dos **guardar como** opção em qualquer aplicação que utiliza esta política.|  
|**Restringir as operações de corte, cópia e colagem com outras aplicações**|Especifica como as operações de corte, cópia e colagem podem ser utilizadas com a aplicação. Escolha entre:<br /><br /> **Bloqueado** – não permitir operações de corte, cópia e colagem entre esta aplicação e outras aplicações.<br /><br /> **Aplicações geridas por políticas** – permite que cortar, copiar e colar operações entre apenas esta aplicação e outras aplicações restritas.<br /><br /> **Aplicações geridas por políticas com colar em** – permite que os dados cortados ou copiados desta aplicação apenas sejam colados noutras aplicações restritas. Permite que os dados cortados ou copiados de qualquer aplicação sejam colados nesta aplicação.<br /><br /> **Qualquer aplicação** – não existem restrições de cortar, copiar e colar operações de ou para esta aplicação.|  
|**Exigir PIN simples para acesso**|Requer que o utilizador introduza um PIN que especifica para utilizar esta aplicação. É pedido ao utilizador para configurar estas definições na primeira vez que executar a aplicação.|  
|**Número de tentativas antes de redefinição do PIN**|Especifica o número de tentativas de introdução do PIN que podem ser efetuadas antes do utilizador ter de repor o PIN.|  
|**Exigir credenciais da empresa para obter acesso**|Requer que o utilizador tem de introduzir as informações de início de sessão empresariais antes de poder aceder a aplicação.|  
|**Exigir a conformidade do dispositivo com a política empresarial para acesso**|Permite que a aplicação ser utilizado apenas quando o dispositivo não tem jailbreak nem Root.|  
|**Verificar novamente os requisitos de acesso após (minutos)**|Especifica o período de tempo antes dos requisitos de acesso da aplicação serem novamente verificados após a aplicação é iniciada (no **tempo limite** campo).<br /><br /> Na **período de tolerância Offline** campo, se o dispositivo estiver offline, especifica o período de tempo antes dos requisitos de acesso da aplicação serem novamente verificados.|  
|**Encriptar dados da aplicação**|Especifica que todos os dados que está associados esta aplicação são encriptados, incluindo os dados armazenados externamente, como os dados armazenados em cartões SD.<br /><br /> **Encriptação para iOS**<br /><br /> Para aplicações que estão associadas uma política de gestão de aplicações móveis do Configuration Manager, os dados são encriptados em descanso ao utilizar a encriptação ao nível do dispositivo fornecida pelo sistema operacional. Isto é ativado através de um dispositivo de política de PIN tem de ser definida pelo administrador de TI. Quando for necessário um PIN, os dados são encriptados de acordo com as definições na política de gestão de aplicações móveis. Conforme indicado na documentação da Apple, [os módulos utilizados pelo iOS 7 têm a certificação FIPS 140-2](http://support.apple.com/en-us/HT202739).<br /><br /> **Encriptação para Android**<br /><br /> Para aplicações que estão associadas uma política de gestão de aplicações móveis do Configuration Manager, a encriptação é fornecida pela Microsoft. Os dados são encriptados em sincronia durante operações de E/S de ficheiros, de acordo com a definição na política de gestão de aplicações móveis. As aplicações geridas no Android utilizam encriptação AES-128 no modo CBC ao utilizar as bibliotecas de criptografia da plataforma. O método de encriptação não tem certificação FIPS 140-2. Conteúdo no armazenamento do dispositivo é sempre encriptado.|  
    |**Bloquear captura de ecrã** (apenas dispositivos Android)|Especifica que as funcionalidades de captura de ecrã do dispositivo estão bloqueadas durante a utilização desta aplicação.|  
    |**Desativar sincronização de contactos**| A partir da versão 1710, esta opção impede que a aplicação guardar os dados na aplicação nativa contactos no dispositivo. Se selecionar não, a aplicação pode guardar dados na aplicação nativa contactos no dispositivo.|  
    |**Desativar a impressão**| A partir da versão 1710, esta opção impede que a aplicação de trabalho de impressão dados escolares ou profissionais. |  

6)  Sobre o **Managed Browser** página, selecione se é permitido ao browser gerido abra apenas URLs na lista ou para bloquear o browser gerido de abrir os URLs na lista e, em seguida, escolha **próxima**.  
Para obter mais informações, consulte [acesso à Internet gerir através de políticas de browser gerido](manage-internet-access-using-managed-browser-policies.md).  

7)  Conclua o assistente.  

 A nova política é apresentada no nó **Políticas de Gestão de Aplicações** da área de trabalho **Biblioteca de Software** .  

##  <a name="step-4-associate-the-application-management-policy-with-a-deployment-type"></a>Passo 4: Associar a política de gestão de aplicações com um tipo de implementação  

 Quando é criado um tipo de implementação de uma aplicação que necessita de uma política de gestão de aplicações, o Configuration Manager reconhece isso e pede-lhe para associar uma política de gestão de aplicações. Para o Managed Browser, tem de associar a política de um Browser gerido e geral. Para obter mais informações, consulte [criem aplicativos](create-applications.md).  

> [!IMPORTANT]  
>  Se a aplicação já está a ser implementada, a implementação para o novo tipo de implementação falhará até esta associação ser efetuada. Pode fazer a associação em **Propriedades** da aplicação, no separador **Gestão de Aplicações** .  

> [!IMPORTANT]  
>  Para dispositivos que executem sistemas operativos anteriores ao iOS 7.1, as políticas associadas não são removidas quando a aplicação é desinstalada.  
>   
>  Se o dispositivo não estiver inscrito do Configuration Manager, as políticas não são removidas das aplicações. As aplicações com políticas aplicadas mantém as definições de política, mesmo depois da aplicação é desinstalada e reinstalada.  

##  <a name="step-5-monitor-the-app-deployment"></a>Passo 5: Monitorizar a implementação da aplicação  
 Depois de criar e implementar uma aplicação que está associada uma política de gestão de aplicações móveis, pode monitorizar a aplicação e resolver eventuais conflitos de política.  

1. Na consola do Configuration Manager, escolha **biblioteca de Software** > **descrição geral** > **implementações**.  

2. Selecione a implementação que criou. Em seguida, no **home page** separador, escolha **propriedades**.  

3. No painel de detalhes para a implementação, sob **objetos relacionados**, escolha **políticas de gestão de aplicações**.  

   Para obter mais informações sobre a monitorização de aplicações, consulte [monitorizar aplicações](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

##  <a name="learn-how-policy-conflicts-are-resolved"></a>Saiba como são resolvidos os conflitos de políticas  
 Quando existe um conflito de política de gestão de aplicações móveis na primeira implementação para o utilizador ou dispositivo, o valor de definição específica que está em conflito é removido da política que é implementada na aplicação. Em seguida, a aplicação utiliza um valor de conflito incorporado.  

 Quando existe um conflito de política de gestão de aplicações móveis em implementações posteriores na aplicação ou utilizador, o valor de definição específico que está em conflito não será atualizado na política de gestão de aplicações móveis que é implementada na aplicação, e a aplicação utiliza o valor existente para essa definição .  

 Nos casos em que o dispositivo ou o utilizador recebe duas políticas em conflito, aplica-se o comportamento seguinte:  

-   Se ainda tiver sido implementada uma política no dispositivo, as definições de política existentes não serão substituídas.  

-   Se já não foi implementada nenhuma política no dispositivo e são implementadas duas definições em conflito, é utilizada a predefinição incorporada no dispositivo.  

##  <a name="see-a-list-of-available-policy-managed-apps"></a>Ver uma lista de aplicações geridas por políticas disponíveis  
 Para obter uma lista da política de aplicações geridas que estão disponíveis para dispositivos iOS e Android, consulte [parceiros de aplicações do Microsoft Intune](https://www.microsoft.com/cloud-platform/microsoft-intune-partners).  

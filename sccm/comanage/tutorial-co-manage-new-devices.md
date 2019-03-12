---
title: Tutorial&#58; ativar a cogestão para dispositivos Windows 10 novos baseado na internet
titleSuffix: Configuration Manager
description: Configure cogestão para dispositivos Windows 10 para o Configuration Manager e o Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/08/2019
ms.topic: tutorial
ms.prod: configuration-manager
ms.service: ''
ms.technology: ''
ms.assetid: ''
ms.openlocfilehash: 61400d382a539efa495af99795e32fc1f2a517ab
ms.sourcegitcommit: af8693048e6706ffda72572374f56e0bc7dfce2c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/11/2019
ms.locfileid: "57737374"
---
# <a name="tutorial-enable-co-management-for-new-internet-based-devices"></a>Tutorial: Ativar a cogestão para novos dispositivos baseados na internet
Com a cogestão, pode manter os seus processos bem estabelecidos para utilizar o Configuration Manager para gerenciar PCs em sua organização. Ao mesmo tempo, está investindo na cloud através da utilização do Intune para segurança e provisionamento modernos. 

Neste tutorial, vai configurar cogestão de dispositivos Windows 10 num ambiente onde pode utilizar ambos os Azure Active Directory (AD) e no local AD, mas não tem um [híbrida do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/overview#hybrid-azure-ad-joined-devices) (AD). Ambiente do Configuration Manager inclui um único site primário com todas as funções de sistema de sites localizadas no mesmo servidor, o servidor do site. Este tutorial começa com a premissa de que os dispositivos Windows 10 já estão inscritos no Intune. 

Se tiver uma versão híbrida do Azure AD que associa o ambiente AD com o Azure AD, recomendamos que siga o nosso tutorial de complementar [ativar a cogestão para clientes do Configuration Manager](/sccm/comanage/tutorial-co-manage-clients). 
 
Utilize este tutorial quando:  
- Tiver dispositivos Windows 10 para que passem a cogestão. Estes dispositivos podem ter sido aprovisionados através do Windows Autopilot ou são diretos do seu hardware OEM. 
- Tiver dispositivos Windows 10 na internet que gerencia atualmente com o Intune para o qual pretende adicionar o cliente do Configuration Manager.


**Neste tutorial, irá:**  
> [!div class="checklist"]  
> * Rever pré-requisitos para o Azure e o seu ambiente no local
> * Pedir um certificado SSL público para o gateway de gestão da cloud (CMG)
> * Ativar os serviços do Azure no Configuration Manager
> * Implementar e configurar um gateway de gestão da cloud  
> * Configurar o ponto de gestão e os clientes utilizem o CMG
> * Ativar a cogestão no Configuration Manager
> * Configurar o Intune para instalar o cliente do Configuration Manager
> * Atribuir licenças para serviços em nuvem



## <a name="prerequisites"></a>Pré-requisitos  

### <a name="azure-services-and-environment"></a>Serviços do Azure e o ambiente
- Subscrição do Azure ([avaliação gratuita](https://azure.microsoft.com/free)) 
- Azure Active Directory Premium 
- Subscrição do Microsoft Intune 
  > [!TIP]  
  > Do Enterprise Mobility and Security (EMS) subscrição inclui o Azure Active Directory Premium e o Microsoft Intune. Subscrição do EMS ([avaliação gratuita](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

- Os utilizadores têm de ser [licenças atribuídas](tutorial-co-manage-clients.md#assign-intune-licenses-to-users) para *Intune* e *Azure Active Directory Premium*
- Intune está configurado para [inscrição automática de dispositivos](tutorial-co-manage-clients.md#configure-auto-enrollment-of-devices-to-intune)  


### <a name="on-premises-infrastructure"></a>Infraestrutura no local
- System Center Configuration Manager atual branch, versão 1810 ou posterior.  
  
  Versão 1810 introduz [avançada HTTP](/sccm/core/plan-design/hierarchy/enhanced-http), que é utilizado neste tutorial, para evitar requisitos mais complexos de PKI. Através da utilização de HTTP avançada, o site primário que utiliza para gerir os clientes têm de ser configurado para utilizar certificados gerados pelo Configuration Manager para sistemas de sites HTTP.  
   
  Versão 1810 também apresenta uma linha de comando mais simples para instalação baseada na internet do cliente do Configuration Manager.

- O [autoridade de MDM](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority) tem de ser definido para o Intune  

### <a name="external-certificates"></a>Certificados externos:
- Certificado de autenticação de servidor do CMG. Este certificado é um certificado SSL de um fornecedor do certificado público e globalmente confiáveis. Por exemplo, mas não limitado a, DigiCert, Thawte ou VeriSign. Terá de exportar este certificado como. Ficheiro PFX com chave privada.  

- Mais tarde neste tutorial fornecemos documentação de orientação sobre como configurar o pedido para este certificado.

### <a name="permissions"></a>Permissões
Neste tutorial, utilize as seguintes permissões para concluir tarefas:
- Uma conta que seja um *administrador global* no Azure  
- Uma conta que seja um *administrador de domínio* na sua infraestrutura no local  
- Uma conta que seja um *administrador total* para *todos os* âmbitos no Configuration Manager   


## <a name="request-a-public-certificate-for-the-cloud-management-gateway"></a>Pedir um certificado público para o gateway de gestão da nuvem
Quando os dispositivos estão na internet, a cogestão requer que o gateway de gestão do Configuration Manager na cloud (CMG). O CMG permite que os dispositivos Windows 10 baseado na internet comunicar com a sua implementação do Configuration Manager no local. Para estabelecer uma confiança entre os dispositivos e o ambiente do Configuration Manager, o CMG requer um certificado SSL.

Este tutorial utiliza um certificado público chamado **certificado de autenticação de servidor CMG** que deriva a autoridade de um fornecedor de certificados globalmente confiáveis. Embora seja possível configurar cogestão usando certificados que derivam de autoridade do seu local o autoridade de certificação Microsoft, utilização de certificados autoassinados está além do escopo deste tutorial.

O **certificado de autenticação de servidor CMG** é utilizado para encriptar o tráfego de comunicações entre o cliente do Configuration Manager e o CMG. Os rastreios de certificado para uma raiz confiável para verificar a identidade do servidor para o cliente. O certificado público inclui uma raiz fidedigna que os clientes do Windows já confiam.

Sobre este certificado: 

- Identificar um nome exclusivo para o seu serviço CMG no Azure e, em seguida, especifique esse nome no seu pedido de certificado.  
- Gerar o pedido de certificado num servidor específico e, em seguida, submeter o pedido para um fornecedor do certificado público para obter o certificado SSL necessário.  
- Importe o certificado que receberá de volta do fornecedor para o sistema que gerou o pedido. Utilize o mesmo computador para exportar o certificado para utilização quando implementar mais tarde CMG para o Azure.  
- Quando instala o CMG, ele cria um serviço CMG no Azure com o nome que especificou no certificado.  

### <a name="identify-a-unique-name-for-your-cloud-management-gateway-in-azure"></a>Identificar um nome exclusivo para o seu gateway de gestão na cloud no Azure
Quando pedir o certificado de autenticação de servidor CMG, tem de especificar o que tem de ser um nome exclusivo para identificar seu *(clássica) do serviço em nuvem* no Azure. Por predefinição, o público do Azure na cloud utiliza *cloudapp.net*, e o CMG está hospedado no domínio cloudapp.net como  *\<YourUniqueDnsName >. cloudapp.net*.  

> [!TIP]  
> Neste tutorial, o **certificado de autenticação de servidor CMG** utiliza um FQDN que termina em *contoso.com*.  Depois de criarmos o CMG irá ser configurado um registo de nome canónico (CNAME) no DNS público da nossa organização. Este registo cria um alias para o CMG que mapeia para o nome que utilizamos no certificado público.  

Antes de pedir o certificado público, confirme o nome que pretende utilizar está disponível no Azure. Não cria diretamente o serviço no Azure. Em vez disso, o nome especificado no certificado público que solicitar é utilizado pelo Configuration Manager para criar o serviço em nuvem, ao instalar o CMG.  

1. Inicie sessão no [Portal do Microsoft Azure](https://portal.azure.com/).  

2. Selecione **criar um recurso**, escolha a **computação** categoria, em seguida, selecione **serviço em nuvem**. É aberto o painel de (clássico) do serviço Cloud.

3. Para **nome DNS**, especifique o nome de prefixo para o serviço em nuvem que usará. Este prefixo tem de ser o mesmo que o que irá utilizar mais tarde quando pedir um certificado de publicar para o certificado de autenticação de servidor do CMG. Usamos *MyCSG*, que cria o espaço de nomes do *MyCSG.cloudapp.net*. A interface confirma se o nome está disponível ou já em utilização por outro serviço.  
 Depois de confirmar o nome que pretende utilizar está disponível, está pronto para submeter o certificado de assinatura do pedido (CSR).

### <a name="request-the-certificate"></a>Pedir o certificado
Utilize as seguintes informações para submeter um pedido para seu CMG para um fornecedor do certificado público de assinatura de certificado. Altere os valores seguintes para ser relevantes ao seu ambiente.  

- *MyCMG* para identificar o nome do serviço do gateway de gestão na cloud
- *Contoso* como o nome da empresa
- *Contoso.com* como o domínio público

Recomendamos que utilize o seu servidor de site primário para gerar o certificado de assinatura de pedidos (CSR). Quando obtiver o certificado, tem de inscrevê-lo no mesmo servidor que gerou o CSR ou não é possível exportar a chave privada de certificados, que é necessária.  

Solicite um tipo de fornecedor de chave de versão 2 ao gerar um CSR. Apenas os certificados versão 2 são suportados.  

> [!TIP]  
> Quando vamos implementa o CMG, podemos irá também instalar um ponto de distribuição de nuvem (CDP) ao mesmo tempo. Por predefinição, quando implanta um CMG, a opção **permitir CMG para funcionar como um ponto de distribuição de nuvem e servir conteúdo a partir de armazenamento do Azure** está selecionada. A colocalização o CDP no servidor com o CMG remove a necessidade de certificados separados e configurações para suportar o CDP. Embora o CDP não é necessário usar a cogestão, é útil na maioria dos ambientes.  
>
> Se pretender utilizar pontos de distribuição de nuvem adicional para a cogestão, terá de pedir certificados separados para cada servidor adicional. Para pedir um certificado de públicas para o CDP, utilize os detalhes do mesmo como para o gateway de gestão de nuvem CSR. Só tem de alterar o nome comum para que seja exclusivo para cada CDP.  

**Detalhes para o gateway de gestão de cloud CSR**
- **Nome comum**: ClousServiceNameCMG.YourCompanyPubilcDomainName.com  
Exemplo: MyCSG.contoso.com  
- **Nome alternativo do requerente**: Mesmo que o nome comum (CN)  
- **Organização**:  O nome da sua organização  
- **Departamento**: Por sua organização  
- **Cidade**: Por sua organização  
- **estado**: Por sua organização  
- **País**: Por sua organização  
- **Tamanho da chave: 2048**  
- **Fornecedor de: Fornecedor de criptografia do Microsoft RSA SChannel**  

### <a name="import-the-certificate"></a>Importar o certificado
Depois de receber o certificado público, importá-lo para o arquivo de certificados local do computador que criou o CSR. Em seguida, exporte o certificado como um. Ficheiro PFX para que possa utilizá-lo para seu CMG no Azure.  

Fornecedores de certificado pública oferecem, normalmente, instruções de importação do certificado. O processo para importar o certificado deve assemelhar-se as seguintes orientações:  

1. No computador que o certificado está a ser importado para, localize o ficheiro. pfx do certificado.  

2. O ficheiro com o botão direito e, em seguida, selecione **Instalar PFX**  

3. Quando é iniciado o Assistente para importar certificados, selecione **seguinte**.  

4. Sobre o **arquivo a ser importado** página, selecione **próxima**. 

5. Sobre o **palavra-passe** página, introduza a palavra-passe para a chave privada na caixa de palavra-passe e, em seguida, selecione **próxima**.  
  
   Selecione a opção para tornar a chave exportável.

6. Na **página de certificado Store**, escolha **automaticamente, selecione o arquivo de certificados com base no tipo de certificado**e, em seguida, selecione **seguinte**.  

7.  Selecione **Concluir**.

### <a name="export-the-certificate"></a>Exportar o certificado
Exportar os *certificado de autenticação de servidor CMG* do seu servidor. Exportar o certificado torna a utilizável para o seu gateway de gestão na cloud no Azure.  

1. No servidor em que importou o certificado SSL público, execute **certlm** para abrir a consola do Gestor de certificados.  

2. Na consola do Gestor de certificados, selecione **pessoais > certificados**. Em seguida, clique com botão direito no *certificado de autenticação de servidor CMG* inscritos no procedimento anterior e, em seguida, selecione **todas as tarefas > exportar**.  

3. No Assistente para exportar certificados, selecione **próxima**, selecione **Sim, exportar a chave privada**e, em seguida **seguinte**.  

4. Na página exportar formato de ficheiro, selecione **Personal Information Exchange - PKCS #12 (. PFX)**, selecione **próxima**e forneça uma palavra-passe. Para o nome de ficheiro, especifique um nome, como **C:\ConfigMgrCloudMGServer**. Irá referenciar este ficheiro quando criar CMG no Azure.  

5. Selecione **próxima**e, em seguida, confirme as seguintes definições antes de selecionar **concluir** para concluir a exportação:  

   - Exportar chaves = Sim  
   - Incluir todos os certificados no caminho de certificação = Sim  
   - Formato de ficheiro = Personal Information Exchange (*. pfx)  

6. Depois de concluir a exportação, localize o ficheiro. pfx e coloque uma cópia do mesmo no **C:\Certs** no servidor de site primário do Configuration Manager, que irá gerir os clientes baseados na internet. A pasta de certificados é uma pasta temporária para utilizar na movimentação de certificados entre servidores. Acessar o ficheiro de certificado do servidor do site primário quando implementar o gateway de gestão da cloud para o Azure.  

Depois de copiar o certificado para o servidor de site primário, pode eliminar o certificado do arquivo de certificados pessoais no servidor membro. 


## <a name="enable-azure-cloud-services-in-configuration-manager"></a>Ativar serviços cloud do Azure no Configuration Manager
Para configurar os serviços do Azure a partir da consola do Configuration Manager, utilize o Assistente para configurar os serviços do Azure e criar duas aplicações do Azure Active Directory (Azure AD).  

- **Aplicação de servidor** – uma *aplicação Web* no Azure AD  
- **Aplicação de cliente** – uma *cliente nativo* aplicação no Azure AD  

Execute o procedimento seguinte do servidor do site primário.  

1. Do servidor do site primário, abra a consola do Configuration Manager e aceda à **administração > Serviços Cloud > Serviços do Azure**e selecione **configurar os serviços do Azure**.  

   Na página configurar o serviço do Azure, especifique um nome amigável para o serviço de gestão de cloud que está a configurar. Por exemplo: *Meu serviço de gestão da cloud*   

   Em seguida, selecione **gestão na Cloud**e, em seguida, selecione **próxima**.  
   
   > [!TIP]  
   > Para obter mais informações sobre as configurações que fizer no assistente, consulte [iniciar o Assistente de serviços do Azure](https://docs.microsoft.com/sccm/core/servers/deploy/configure/Azure-services-wizard#start-the-azure-services-wizard)


2. Sobre o **as propriedades da aplicação** página, para **aplicação Web**, selecione **procurar** para abrir o **aplicação de servidor** caixa de diálogo e, em seguida, selecione  **Criar**. Configure os seguintes campos:

   - **Nome da aplicação**: Especifique um nome amigável para a aplicação, tal como *aplicação web de gestão na Cloud*.  

   - **URL da home page**: Este valor não é utilizado pelo Configuration Manager, mas é necessário pelo Azure AD. Por predefinição, este valor é https://ConfigMgrService.  
   
   - **URI de ID de aplicação**: Este valor tem de ser exclusivo no seu inquilino do Azure AD. É no token de acesso utilizado pelo cliente do Configuration Manager para pedir acesso ao serviço. Por predefinição, este valor é https://ConfigMgrService.  

   Em seguida, selecione **iniciar sessão**e especifique uma conta de Administrador Global do Azure. Estas credenciais não são guardadas pelo Configuration Manager. Essa pessoa não requer permissões no Configuration Manager e não precisa de ser a mesma conta que executa o Assistente de serviços do Azure. 

   Depois de iniciar sessão, os resultados são apresentados. Selecione **OK** para fechar a caixa de diálogo Criar aplicação de servidor e voltar para a página de propriedades da aplicação. 

3. Para **aplicação de cliente nativo**, selecione **procurar** para abrir o **aplicação de cliente** caixa de diálogo. 

4. Selecione **Create** para abrir o **Criar aplicação de cliente** caixa de diálogo e, em seguida, configure os seguintes campos:  

   - **Nome da aplicação**: Especifique um nome amigável para a aplicação, tal como *aplicação de cliente nativo de gestão na Cloud*.
   
   - **URL de resposta**: Este valor não é utilizado pelo Configuration Manager, mas necessários pelo Azure AD. Por predefinição, este valor é https://ConfigMgrClient.
   Em seguida, selecione **iniciar sessão**e especifique uma conta de Administrador Global do Azure. Como a aplicação Web, estas credenciais não são guardadas e não necessitam de permissões no Configuration Manager.
   
   Depois de iniciar sessão, os resultados são apresentar. Selecione **OK** para fechar a caixa de diálogo Criar aplicação de cliente e voltar para a página de propriedades da aplicação. Em seguida, selecione **seguinte** para continuar.

5. No **configurar definições de deteção** página, marque a caixa de **ativar o Azure Active Directory deteção de utilizadores**, selecione **seguinte**e, em seguida, toda a configuração das Caixas de diálogo de deteção para o seu ambiente.  

6. Continuar através das páginas de resumo, o progresso e conclusão e, em seguida, feche o assistente.  

   Serviços do Azure para a deteção de utilizador do Azure AD está agora ativada no Configuration Manager.  Deixe a consola aberta por agora.  

7. Abra um browser e inicie sessão para o [portal do Azure](https://portal.azure.com/).  

8. Selecione **todos os serviços > Azure Active Directory > registos das aplicações**e, em seguida:

   1. Selecione a aplicação Web que criou. 

   2. Aceda a **definições > permissões obrigatórias**, selecione **conceder permissões**e, em seguida, selecione **Sim**.  

   3. Selecione a aplicação de cliente nativo que criou. 

   4. Aceda a **definições > permissões obrigatórias**, selecione **conceder permissões**e, em seguida, selecione **Sim**.  

9. Na consola do Configuration Manager, aceda a **administração > Descrição geral > Serviços Cloud > Serviços do Azure**e selecione o seu serviço do Azure. Em seguida, clique em **do Azure Active Directory utilizador detetar** e selecione **executar agora deteção completa**. Selecione **Sim** para confirmar a ação.  

10. No servidor do site primário, abra o Gestor de configuração **SMS_AZUREAD_DISCOVERY_AGENT.log** e procure a seguinte entrada confirmar que a deteção está a funcionar:  *UDX foi publicada com êxito para os utilizadores do Azure Active Directory*  

    Por predefinição, o ficheiro de registo está no *%Program_Files%\Microsoft configuração Manager\Logs*.  


## <a name="create-the-cloud-services-in-azure"></a>Criar os serviços cloud no Azure
**Nesta secção do tutorial, irá**:
- Criar o serviço de nuvem do CMG  
- Criar registos para ambos os serviços DNS CNAME  

### <a name="create-the-cmg"></a>Criar CMG
Utilize este procedimento para instalar um gateway de gestão na cloud como um serviço no Azure. Instala o CMG no site de nível superior da hierarquia. Neste tutorial, vamos continuar a utilizar o site primário onde foram inscritos e exportar certificados.

1. No servidor do site primário, abra a consola do Configuration Manager e, em seguida, aceda **administração > Descrição geral > Serviços Cloud > Gateway de gestão na Cloud**e, em seguida, selecione **criar Gateway de gestão na Cloud**.  

2. Sobre o **gerais** página:  

   1. Selecione o ambiente de cloud para o **ambiente do Azure**. Este tutorial utiliza **AzurePublicCloud**.  
   
   2. Selecione **do Azure Resource Manager deployment**.  
  
   3. **Inicie sessão no** à sua subscrição do Azure. O Configuration Manager preenche informações adicionais com base nas informações configuradas quando ativou a serviços cloud do Azure para o Configuration Manager.  

   Selecione **seguinte** para continuar.  

3. Sobre o **definições** página, procure e selecione o ficheiro com o nome **ConfigMgrCloudMGServer.pfx**, que é o ficheiro que exportou depois de importar o certificado de autenticação de servidor do CMG. Depois de especificar a palavra-passe, o **nome do serviço** e **nome da implementação** preencher automaticamente, com base em detalhes no ficheiro de certificado. pfx. 

4. Definir sua **região**.

5. Para **grupo de recursos**, utilize um grupo de recursos existente ou criar um grupo com um nome amigável que utiliza sem espaços, como **CofigMgrCloudServices**. Se optar por criar um grupo, o grupo é adicionado como um grupo de recursos no Azure.  

6. A menos que está pronto para configurar uma escala, utilize um (1) o para o número de **instâncias de VM**. O número de instâncias de VM permite que um único serviço Cloud do Gateway de gestão da Cloud (CMG) aumentar horizontalmente para suportar mais ligações de cliente. Mais tarde, pode utilizar a consola do Configuration Manager para voltar e editar o número de instâncias VM que utiliza.  

7. Ativar a caixa de verificação **verificar revogação de certificados de cliente**. 

8. Ativar a caixa de verificação **permitir CMG para funcionar como um ponto de distribuição de nuvem e servir conteúdo a partir de armazenamento do Azure** se pretender implementar um ponto de distribuição de nuvem com o CMG.

9. Selecione **seguinte** para continuar.

10. Reveja os valores na **alerta** página e, em seguida, selecione **próxima**.

11. Reveja os **resumo** página e clique em **seguinte** para criar o gateway de gestão de cloud serviço em nuvem. Selecione **fechar** para concluir o assistente.  

12. No nó de Gateway de gestão na Cloud da consola do Configuration Manager, pode agora ver o novo serviço.  

### <a name="create-dns-cname-records"></a>Criar registos DNS CNAME

Quando cria uma entrada DNS para o CMG, ativar os dispositivos Windows 10, dentro e fora da rede da sua empresa utilizem a resolução de nome para encontrar o serviço de nuvem do CMG no Azure.

Nosso exemplo de registo CNAME utiliza os seguintes detalhes:  

- É o nome da empresa **Contoso** com um espaço de nomes DNS público dos ***Contoso.com***.  

- É o nome do serviço CMG **MyCMG**, que se torna ***MyCMG.CloudApp.Net*** no Azure.  

Exemplo de registo CNAME: *MyCMG.contoso.com => My.cloudapp.net*

## <a name="configure-the-management-point-and-clients-to-use-the-cmg"></a>Configurar o ponto de gestão e os clientes utilizem o CMG
Configure as definições que permitem a pontos de gestão no local e os clientes para utilizar o gateway de gestão na cloud. 

Uma vez que utilizamos HTTP avançada para comunicações de cliente, não é necessário para utilizar um ponto de gestão HTTPS.  

### <a name="create-the-cmg-connection-point"></a>Criar ponto de ligação CMG
Configure o site para oferecer suporte a HTTP avançada.  

1. Na consola do Configuration Manager, aceda a **administração > Descrição geral > Configuração do Site > Sites**e abra as propriedades do site primário.  

2. Sobre o **comunicação do computador cliente** separador, selecione a *HTTPS ou HTTP* opção para **sistemas de sites de certificados gerados pelo utilize o Gestor de configuração para HTTP**e, em seguida, Selecione **OK** para guardar a configuração. 

3. Agora, aceda a **administração > Descrição geral > Configuração do Site > servidores e funções de sistema de sites** e selecione o servidor com um ponto de gestão onde pretende instalar o ponto de ligação do gateway de gestão na cloud.  

4. Selecione **Add Site System Roles**e, em seguida **próxima**> **seguinte**.  

5. Selecione o **ponto de ligação de gateway de gestão da Cloud** e, em seguida, selecione **próxima** para continuar.  

6. Reveja as seleções predefinidas na **ponto de ligação de gateway de gestão da Cloud** página e certifique-se de CMG correta está selecionada. Se tiver vários gateways de gestão na cloud, pode utilizar a lista pendente para especificar um CMG diferente. Também pode alterar o CMG em uso, após a instalação. Selecione **seguinte** para continuar.

7. Selecione **seguinte** para iniciar a instalação e, em seguida, ver os resultados na página de conclusão.  Selecione **fechar** para concluir a instalação do ponto de ligação. 

8. Agora, aceda a **administração > Descrição geral > Configuração do Site > servidores e funções de sistema de sites** e abra o **propriedades** para o ponto de gestão onde instalou o ponto de ligação. Sobre o **gerais** separador, marque a caixa **tráfego de gateway de gestão de nuvem de permitir que o Configuration Manager**e, em seguida, selecione **OK** para guardar a configuração. 
   > [!TIP]  
   > Embora não sejam necessárias para ativar a cogestão, recomendamos que efetue esta edição mesmo para qualquer software de pontos de atualização. 

### <a name="configure-client-settings-to-direct-clients-to-use-the-cmg"></a>Configurar definições de cliente para direcionar clientes para utilizarem o CMG
Utilize as definições de cliente para configurar clientes do Configuration Manager para comunicar com o CMG.  

1. Abra o **consola do Configuration Manager > Administração > Descrição geral > definições de cliente**e, em seguida, edite a **predefinições de cliente**.  

2. Selecione **serviços Cloud**.

3. Sobre o **predefinições** página, defina as seguintes definições para = **Sim**  

   - **Registar automaticamente novos dispositivos associados a um domínio do Windows 10 com o Azure Active Directory**  

   - **Permitir que os clientes utilizar um gateway de gestão da cloud** 

   - **Permitir o acesso ao ponto de distribuição da nuvem** 

4. Sobre o **política de cliente** página, defina **ativar pedidos da política de utilizador dos clientes internet** = **Sim** 

1. Selecione **OK** para guardar esta configuração. 



## <a name="enable-co-management-in-configuration-manager"></a>Ativar a cogestão no Configuration Manager
Com as configurações do Azure, funções de sistema de sites e definições de cliente no local, pode configurar o Configuration Manager para ativar a cogestão. No entanto, ainda precisará fazer algumas configurações no Intune depois de ativar a cogestão antes da conclusão deste tutorial. Uma dessas tarefas é configurar o Intune para implementar o cliente do Configuration Manager. Essa tarefa é facilitada ao guardar a linha de comandos para implementação de cliente que está disponível a partir do Assistente de configuração de cogestão. É por isso que vamos ativar a cogestão agora, antes de podermos concluir as configurações do Intune. 

> [!TIP]  
>  No passo seis o procedimento seguinte, irá passar a atribuir uma coleção como um *grupo-piloto* para a cogestão. Este é um grupo que contém um pequeno número de clientes para testar suas configurações de cogestão. Recomendamos que crie uma coleção adequada, antes de começar o procedimento. Em seguida, pode selecionar essa coleção sem sair o procedimento para fazer isso.  
 
1. Na consola do Configuration Manager, aceda a **Administration** > **descrição geral** > **serviços Cloud**  >  **Cogestão**.

2. No separador início, no grupo de gerir, selecione **configurar cogestão** para abrir o Assistente de configuração de cogestão.

3. Sobre o *subscrição* página, selecione **iniciar sessão** e inicie sessão no seu inquilino do Intune e, em seguida, selecione **seguinte**.

4. Na *ativação* página, da *a inscrição automática no Intune* lista pendente, selecione uma das seguintes opções:  

   - **Piloto**  - *(recomendado)* membros da coleção que especificar são automaticamente inscritos no Intune e, em seguida, pode ser cogeridos. Especifique a coleção piloto na *teste* página deste assistente. Esta opção permite-lhe testar a cogestão num subconjunto de clientes. Em seguida, pode implementar a cogestão para clientes adicionais usando uma abordagem faseada.  

   - **Todos os** -cogestão está ativada para todos os clientes.  

   Antes de prosseguir para a página seguinte do assistente, selecione **cópia** e guarde a linha de comandos CCMSetup, que é fornecida. Irá utilizar a linha de comando mais tarde quando configurar o Intune para implementar o cliente do Configuration Manager. Se não as guardar esta linha de comandos agora, pode rever a configuração de cogestão em qualquer altura para obter esta linha de comandos. 

5. Na *cargas de trabalho* página, pode mudar cargas de trabalho da **Configuration Manager** para um dos seguintes e, em seguida, quando estiver pronto para continuar, selecione **seguinte**.  
   
   - **Criar um piloto do Intune** -muda de uma carga de trabalho apenas para os dispositivos do grupo piloto. Vai atribuir uma coleção que o grupo piloto na página seguinte do assistente.  
   
   - **Intune** -muda a carga de trabalho associada para todos os dispositivos Windows 10 cogeridos.  

   Não precisa de alternar quaisquer cargas de trabalho no momento que ativa a cogestão. Pode regressar ao mais tarde, esta configuração da consola do Configuration Manager após a configuração da cogestão.  

   Antes de mudar uma carga de trabalho, certifique-se de que a carga de trabalho correspondente no Intune é configurada e implementada. Por isso, mantém a fazer as cargas de trabalho gerido.  

6. Sobre o *teste* , especifique uma coleção a utilizar para o **coleção de projetos-piloto**e, em seguida, clique em **seguinte**. A coleção que especificar é utilizada como parte da sua implementação faseada de cogestão. Pode alterar as coleções no grupo piloto em qualquer altura a partir das propriedades de cogestão.  

7. Sobre o *resumo* página, selecione **próxima**e, em seguida **fechar** para concluir o assistente.  

## <a name="use-intune-to-deploy-the-configuration-manager-client"></a>Utilizar o Intune para implementar o cliente do Configuration Manager
Pode utilizar o Intune para instalar o cliente de Configuration Manager em dispositivos Windows 10 que estão atualmente apenas geridos com o Intune.  

Em seguida, quando inscreve um dispositivo Windows 10 anteriormente não gerido com o Intune, ele automaticamente instala o cliente do Configuration Manager.

### <a name="create-an-intune-app-to-install-the-configuration-manager-client"></a>Criar uma aplicação do Intune para instalar o cliente do Configuration Manager

1. Do servidor do site primário, inicie sessão para o [portal do Azure](https://portal.azure.com/) e vá para o **Intune > aplicações de cliente > aplicações > Adicionar**.

2. Para **tipo de aplicação**: Selecione **aplicação de linha de negócio**.

3. Selecione **o ficheiro de pacote de aplicação**e, em seguida, navegue até à localização do ficheiro de Configuration Manager **ccmsetup**e, em seguida, selecione **aberto > OK**.
Por exemplo, *C:\Program Files\Microsoft Configuration Manager\bin\i386\ccmsetup.msi*   

4. Selecione **informações da aplicação**e, em seguida, especifique os seguintes detalhes:
   - **Descrição**: Cliente do Configuration Manager  

   - **Publisher**: Microsoft  

   - **Argumentos da linha de comandos**:  *\<Especifique a **CCMSETUPCMD** linha de comandos. Pode utilizar a linha de comandos que guardou a partir da* ativação *página do Assistente de configuração de cogestão. Esta linha de comandos inclui os nomes do seu serviço de nuvem e os valores adicionais que permitem que os dispositivos instalar o Configuration Manager software de cliente. >*  

     A estrutura de linha de comando deve assemelhar-se neste exemplo, utilizar apenas os parâmetros CCMSETUPCMD e SMSSiteCode:  
 
         CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  

     > [!TIP]  
     > Se não tiver a linha de comandos disponível, pode ver as propriedades de *CoMgmtSettingsProd* na consola do Configuration Manager para obter uma cópia da linha de comandos.    

5. Selecione **OK > Adicionar**.  A aplicação é criada e torna-se disponível na consola do Intune. Depois da aplicação está disponível, pode utilizar a secção seguinte para configurar o Intune para atribuí-lo a dispositivos Windows 10.

### <a name="assign-the-intune-app-to-install-the-configuration-manager-client"></a>Atribuir a aplicação do Intune para instalar o cliente do Configuration Manager
O procedimento seguinte implementa as aplicações para instalar o cliente do Configuration Manager que criou no procedimento anterior. 

1. Inicie sessão no [portal do Azure](https://portal.azure.com/).  Selecione **todos os serviços > Intune > aplicações de cliente > aplicações**e, em seguida, selecione **arranque de configuração de cliente do ConfigMgr**, a aplicação que criou para implementar o cliente do Configuration Manager.  

2. Selecione **atribuições > Adicionar grupo**.  Definir **tipo de atribuição** como **necessário**e, em seguida, utilizar **grupos incluídas** e **grupos excluídos** para definir o Azure Active Directory (AD) grupos de usuários tem dispositivos que pretende participar de cogestão.  

3. Selecione **OK** e, em seguida **guardar** a configuração.
A aplicação é agora necessário por utilizadores e dispositivos que foi atribuída. Depois da aplicação instala o cliente do Configuration Manager num dispositivo, é gerido pelo cogestão.

## <a name="assign-intune-licenses-to-users"></a>Atribuir licenças do Intune aos utilizadores   
É uma ação geralmente subestimada, mas crítica atribuir uma licença do Intune a cada utilizador que utiliza um dispositivo que está cogerido.  

Para atribuir licenças a grupos de utilizadores, utilize o Azure Active Directory.  

1. Inicie sessão para o [portal do Azure](https://portal.azure.com/) com uma conta de administrador. Para gerir licenças, a conta tem de ser um administrador de conta de utilizador ou função de administrador global.  

2. Selecione **todos os serviços** no painel de navegação à esquerda e, em seguida, selecione **Azure Active Directory**.  

3. Sobre o **do Azure Active Directory** painel, selecione **licenças** para abrir um painel onde pode ver e gerir todos os produtos sujeito a licença no inquilino.  
 
4. Sob **todos os produtos**, selecione a opção de produto que inclui a licença do Intune e, em seguida, selecione **atribuir** na parte superior do painel.  

   Por exemplo, poderá selecionar **Enterprise Mobility + Security E5** se isso é como obter o Intune.  

5. Sobre o **atribuir licenças** painel, clique em **utilizadores e grupos** para abrir o **utilizadores e grupos** painel. Selecione os grupos e utilizadores individuais a quem pretende atribuir uma licença.  Em seguida, clique em **selecione** na parte inferior do painel para confirmar a seleção.  

6. Sobre o **atribuir licenças** painel, clique em **opções de atribuição** para apresentar todos os planos de serviço incluídos no produto que selecionou anteriormente. Se tiver selecionado um único produto, como o Intune, apenas esse produto é mostrado.  
   - Definir **Microsoft Intune** ao **no**.  
   - Atribuir uma licença para cada utilizador **Azure Active Directory Premium**.  

   Quando são atribuídas as licenças aplicável, selecione **OK**.  

7. Para concluir a atribuição, sobre o **atribuir licenças** painel, clique em **atribuir** na parte inferior do painel.  

8. É apresentada uma notificação no canto superior direito que mostra o estado e o resultado do processo. Se não foi possível concluir a atribuição ao grupo (por exemplo, por causa de licenças pré-existentes no grupo), clique na notificação para ver os detalhes da falha. 


## <a name="summary"></a>Resumo 
Depois de concluir os passos de configuração deste tutorial, incluindo a última ação para garantir que as licenças são atribuídas, os dispositivos com êxito podem ser cogeridos. 

## <a name="next-steps"></a>Passos seguintes
- Reveja o estado dos dispositivos cogeridos com o [dashboard de cogestão](https://docs.microsoft.com/sccm/core/clients/manage/co-management-dashboard)
- Uso [Windows Autopilot]() para aprovisionar novos dispositivos
- Uso [acesso condicional](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access) e regras de conformidade do Intune para gerir o acesso de utilizador aos recursos da empresa

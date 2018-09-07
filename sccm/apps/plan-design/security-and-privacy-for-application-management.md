---
title: Segurança e privacidade para aplicações
titleSuffix: Configuration Manager
description: Orientações e recomendações de segurança e privacidade quando gerir aplicações no Configuration Manager.
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 65e4d68f05087d24bc83e8e4a3dd67489fdbaed3
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893588"
---
# <a name="security-and-privacy-for-application-management-in-configuration-manager"></a>Segurança e privacidade para gestão de aplicações no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


##  <a name="security-guidance-for-application-management"></a>Orientações de segurança para gestão de aplicações  


### <a name="use-the-new-software-center-without-the-application-catalog"></a>Utilizar o novo Centro de Software sem o catálogo de aplicações
<!--1358309--> A partir da versão 1806, funções de catálogo de aplicações já não são necessárias para apresentar as aplicações disponíveis para o utilizador no Centro de Software. Esta configuração ajuda a reduzir a infraestrutura de servidor necessária para fornecer aplicativos aos usuários. Também reduz a infraestrutura de servidor reduz a superfície de ataque. 

Para fornecer uma experiência consistente e segura de aplicativos para clientes baseados na internet, utilize o Azure Active Directory e o gateway de gestão na cloud.

Para obter mais informações, consulte [configurar o Centro de Software](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex). 


### <a name="use-https-with-the-application-catalog"></a>Utilizar o HTTPS com o catálogo de aplicações

Configure o ponto de Web site do catálogo de aplicações e o ponto de serviço do catálogo de aplicações web para aceitar ligações HTTPS. Com esta configuração, o servidor seja autenticado para os utilizadores. Os dados transmitidos estão protegidos contra adulteração e visualização. 

Ajudar a evitar ataques de engenharia social ensinando os utilizadores a ligar-se apenas a Web sites fidedignos. Informe os utilizadores sobre os perigos dos Web sites maliciosos.

Quando não utiliza HTTPS, não utilize as opções de configuração de imagem corporativa. Estas definições de mostrarem o nome da sua organização no catálogo de aplicações como prova de identidade.  


### <a name="use-role-separation"></a>Utilize separação de funções

Instale o ponto de Web site do catálogo de aplicações e o ponto de serviço web do catálogo de aplicações em servidores separados. Se o ponto de sites do catálogo de aplicações for comprometido, é separada do ponto de serviço web do catálogo de aplicações. Este design ajuda a proteger os clientes do Configuration Manager e a infraestrutura. Esta configuração é especialmente importante se o ponto de Web site do catálogo de aplicações aceitar ligações de cliente a partir da internet. Faz o servidor mais vulnerável a ataques.  


### <a name="close-browser-windows"></a>Janelas do browser fechar

Informe os utilizadores de que devem fechar a janela do browser quando terminarem de utilizar o Catálogo de Aplicações. Se os utilizadores navegarem para um Web site externo na mesma janela de browser que utilizaram para o Catálogo de Aplicações, o browser continuará a utilizar as definições de segurança adequadas aos sites fidedignos da intranet.  


### <a name="centrally-specify-user-device-affinity"></a>Especificar centralmente a afinidade dispositivo / utilizador

Especifica manualmente a afinidade dispositivo / utilizador em vez de permitir que os utilizadores a identificar o respetivo dispositivo primário. Não ative a configuração baseada na utilização.

Não considere as informações recolhidas junto dos utilizadores ou do dispositivo como autoritativos. Se implementar software ao utilizar a afinidade dispositivo / utilizador não especifica um administrador fidedigno, o software pode ser instalado em computadores e utilizadores que não estão autorizados a recebê-lo.  


### <a name="dont-run-deployments-from-distribution-points"></a>Não executar implementações de pontos de distribuição

Configure sempre as implementações para transferirem conteúdo a partir de pontos de distribuição em vez de executarem a partir destes. Quando configura implementações para transferir o conteúdo de um ponto de distribuição e executar localmente, o Gestor de configuração cliente verifica o hash do pacote depois de transferir o conteúdo. O cliente. sys descartará o pacote se o hash não corresponde ao hash na política. 

Se configurar a implementação para executar diretamente a partir de um ponto de distribuição, o cliente do Configuration Manager não verifica o hash do pacote. Este comportamento significa que o Gestor de configuração de cliente pode instalar o software que foi adulterado.

Se tiver de executar implementações diretamente a partir de pontos de distribuição, usar o NTFS, pelo menos, permissões nos pacotes em pontos de distribuição. Também utilize o protocolo (IPsec internet security) para proteger o canal entre o cliente e os pontos de distribuição e entre os pontos de distribuição e o servidor do site.


### <a name="bkmk_interact"></a> Não permita que os usuários interajam com processos elevados
  
Se ativar as opções para **executados com direitos administrativos** ou **instalar para o sistema**, não deixe que os usuários interajam com esses aplicativos. Quando configura uma aplicação, pode definir a opção como **permitir que os utilizadores visualizem e interajam com a instalação do programa**. Esta definição permite aos utilizadores responder a todos os pedidos necessários na interface do usuário. Se também de configurar o aplicativo **executados com direitos administrativos**, ou a partir da versão 1802 **instalar para o sistema**, um atacante no computador que executa o programa poderá utilizar a interface de utilizador para aumentar os privilégios no computador cliente.

Utilize os programas que utilizam o Windows Installer para instalação e por usuário elevados privilégios para implementações de software que necessitem de credenciais administrativas. A configuração tem de ser executada no contexto de um utilizador que não tenha credenciais administrativas. Privilégios elevados de por utilizador do Windows Installer fornecem a forma mais segura para implementar aplicações que tenham este requisito.


### <a name="restrict-whether-users-can-install-software-interactively"></a>Restrinja a capacidade dos utilizadores instalarem software interativamente

Configurar o **permissões de instalação** definição cliente do **agente do computador** grupo. Esta definição limita os tipos de utilizadores que podem instalar software utilizando o catálogo de aplicações ou o Centro de Software. 

Por exemplo, crie uma definição personalizada de cliente com **Permissões de instalação** definida como **Apenas administradores**. Aplicam-se esta definição de cliente para uma coleção de servidores. Esta configuração impede os utilizadores sem permissões administrativas de instalar software nesses servidores.  


### <a name="for-mobile-devices-deploy-only-applications-that-are-signed"></a>Em dispositivos móveis, implemente apenas aplicações assinadas.

Implemente aplicações para dispositivos móveis apenas se eles são assinadas por código por uma autoridade de certificação (AC) que o dispositivo móvel confie. 

Por exemplo:
- Um aplicativo de um fornecedor assinada por uma AC conhecida, como o VeriSign.  

- Um aplicativo interno que inicie independente do Configuration Manager com a sua AC interna.  

- Uma aplicação interna que seja assinada utilizando o Gestor de configuração ao criar o tipo de aplicação e utilizar um certificado de assinatura.


### <a name="secure-the-location-of-the-mobile-device-application-signing-certificate"></a>Proteja a localização do certificado de assinatura de aplicações a dispositivos móveis

Se assinar aplicações para dispositivos móveis utilizando o **Assistente para criar aplicação** no Configuration Manager, proteja a localização do ficheiro de certificado de assinatura e Proteja o canal de comunicação. Para ajudar a proteger contra a elevação de privilégios e ataques man-in-the-middle, armazene o ficheiro de certificado de assinatura numa pasta protegida. 

Utilize IPsec entre os seguintes computadores:
- O computador que executa a consola do Configuration Manager
- O computador que armazena o ficheiro de assinatura de certificado
- O computador que armazena os ficheiros de origem do aplicativo

Em alternativa, assine o aplicativo independente do Configuration Manager e antes de executar o **Assistente para criar aplicação**.


### <a name="implement-access-controls"></a>Implementar controlos de acesso

Para proteger os computadores de referência, implemente controlos de acesso. Quando configurar o método de deteção num tipo de implementação navegando para um computador de referência, certifique-se de que o computador não é comprometido.


### <a name="restrict-and-monitor-administrative-users"></a>Restrinja e monitorize os utilizadores administrativos

Restrinja e monitorize os utilizadores administrativos que conceda as seguintes funções de segurança baseada em funções de gestão de aplicações:
- **Administrador da aplicação**
- **Autor da aplicação**
- **Gestor de implementação de aplicações**

Mesmo quando configura a administração baseada em funções, os utilizadores administrativos que criem e implementem aplicações poderão ter mais permissões do que pensa. Por exemplo, os utilizadores administrativos que criar ou alterar um aplicativo podem selecionar aplicações dependentes que não estão no seu âmbito de segurança.


### <a name="configure-app-v-apps-in-virtual-environments-with-the-same-trust-level"></a>Configurar aplicações de App-V em ambientes virtuais com o mesmo nível de confiança

Quando configurar ambientes virtuais do Microsoft Application Virtualization (App-V), selecione as aplicações que tenham o mesmo nível de confiança no ambiente virtual. Porque os aplicativos num ambiente virtual de App-V podem partilhar recursos, como a área de transferência, configure o ambiente virtual para que as aplicações selecionadas tenham o mesmo nível de confiança.

Para obter mais informações, consulte [ambientes virtuais App-V criar](/sccm/apps/deploy-use/create-app-v-virtual-environments).


### <a name="make-sure-macos-apps-are-from-a-trustworthy-source"></a>Certifique-se aplicações macOS estão por uma fonte confiável

Se implementar aplicações para dispositivos macOS, certifique-se de que os ficheiros de origem estão por uma fonte confiável. A ferramenta CMAppUtil não valida a assinatura do pacote de origem. Certifique-se de que o pacote provém de uma origem de que confia. A ferramenta CMAppUtil não consegue detetar se os ficheiros foram adulterados.


### <a name="secure-the-cmmac-file-for-macos-apps"></a>Proteger o ficheiro de cmmac para aplicações de macOS

Se implementar aplicações para computadores de macOS, proteja a localização dos **. cmmac** ficheiro. A ferramenta CMAppUtil gera este ficheiro e, em seguida, importá-la para o Configuration Manager. Este ficheiro não é assinado ou validado. 

Proteja o canal de comunicação quando importar este ficheiro para o Configuration Manager. Para ajudar a impedir a adulteração com esse arquivo, armazene-o numa pasta protegida. Utilize IPsec entre os seguintes computadores:
- O computador que executa a consola do Configuration Manager  
- O computador que armazena os **. cmmac** ficheiro  


### <a name="use-https-for-web-applications"></a>Utilizar o HTTPS para aplicativos web

Se configurar um tipo de implementação de aplicações web, utilize HTTPS para proteger a ligação. Se implementar uma aplicação web utilizando um link HTTP em vez de uma ligação HTTPS, o dispositivo pode ser redirecionado para um servidor não autorizado. Dados transferidos entre o dispositivo e o servidor poderão ser adulterados.



##  <a name="security-issues-for-application-management"></a>Problemas de segurança para gestão de aplicações  

-   Os utilizadores com direitos restritos podem copiar ficheiros da cache do cliente no computador cliente.  

     Os utilizadores podem ler a cache do cliente, mas não conseguem escrever nela. Com permissões de leitura, um utilizador pode copiar ficheiros de instalação de aplicações de um computador para outro.  

-   Utilizadores com direitos restritos podem alterar os ficheiros que registam o histórico de implementação de software no computador cliente.  

     Uma vez que as informações de histórico de aplicação não estão protegidas, um utilizador pode alterar os ficheiros que indicam se uma aplicação é instalada.  

-   Pacotes de App-V não tem sessão iniciados.  

     Pacotes de App-V no Configuration Manager não suportam a assinatura. Assinaturas digitais verificam o conteúdo é proveniente de uma origem fidedigna e não foi alterado em trânsito. Não existe nenhuma forma de atenuar este problema de segurança. Siga a prática recomendada de segurança para transferir o conteúdo de uma origem fidedigna e a partir de uma localização segura.  

-   As aplicações de App-V publicadas podem ser instaladas por todos os utilizadores do computador.  

     Quando uma aplicação de App-V é publicada num computador, todos os utilizadores que iniciem sessão nesse computador podem instalar a aplicação. Não é possível restringir os utilizadores que podem instalar a aplicação depois da sua publicação.  

-   Não é possível restringir as permissões de instalação para o portal da empresa em dispositivos móveis.  

     Embora seja possível configurar uma definição para restringir permissões de instalação do cliente, esta definição não funciona para o portal da empresa. Este problema pode resultar numa elevação de privilégios. Os utilizadores podem instalar uma aplicação que não deve ter permissão para instalar.  



##  <a name="BKMK_CertificatesSilverlight5"></a> Certificados para o Microsoft Silverlight 5 e modo de confiança elevada necessários para o catálogo de aplicações  

> [!Important]  
> A partir do Configuration Manager versão 1802, o cliente não instala automaticamente Silverlight.
> 
> A partir da versão 1806, o **experiência de usuário do Silverlight** para o site do catálogo de aplicativos ponto já não é suportado. Os utilizadores devem utilizar o novo Centro de Software. Para obter mais informações, consulte [configurar o Centro de Software](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).  

 A versão 1710 e anterior de clientes do Configuration Manager necessita do Microsoft Silverlight 5, que deve ser executado no modo de confiança elevada para que os utilizadores instalem software do catálogo de aplicações. Por predefinição, as aplicações Silverlight são executadas no modo de confiança parcial para impedir que acedam aos dados do utilizador. Se já não estiver instalado, o Configuration Manager instala automaticamente o Microsoft Silverlight 5 nos clientes. Por predefinição, o Configuration Manager define o agente do computador **permitir que aplicações Silverlight sejam executadas em modo de confiança elevada** definição de cliente **Sim**. Esta definição permite assinado e fidedigno modo de confiança elevada Silverlight aplicativos pedido.  

 Ao instalar a função de sistema de sites do ponto de Web site do catálogo de aplicações, o cliente também instala um certificado no arquivo de certificados fabricantes fidedignos de um computador em cada computador de cliente do Configuration Manager de assinatura da Microsoft. As aplicações Silverlight assinadas por este certificado é executado no modo de confiança elevada, o que os computadores necessitam para instalar software a partir do catálogo de aplicações. O Gestor de configuração gere automaticamente este certificado de assinatura. Para aumentar a continuidade do serviço, não manualmente eliminar ou mover este certificado de assinatura da Microsoft.  

> [!WARNING]  
>  Quando ativada, o **permitir que aplicações Silverlight sejam executadas em modo de confiança elevada** definição de cliente permite que todos os aplicativos do Silverlight, que são assinados por certificados no arquivo de certificados fabricantes fidedignos no computador arquivo ou o utilizador, executar no modo de confiança elevada. A definição de cliente não é possível ativar o modo de confiança elevada especificamente para o catálogo de aplicações do Configuration Manager ou para o arquivo de certificados fabricantes fidedignos no arquivo do computador. Se o software maligno adiciona um certificado não autorizado no arquivo fabricantes fidedignos, software maligno que utiliza uma aplicação Silverlight própria agora também pode executar no modo de confiança elevada.  

 Se definir o **permitir que aplicações Silverlight sejam executadas em modo de confiança elevada** definição **não**, os clientes não remover o certificado de assinatura da Microsoft.  

 Para obter mais informações sobre aplicações fidedignas no Silverlight, consulte [aplicativos confiáveis](https://go.microsoft.com/fwlink/p/?LinkId=252842).  



##  <a name="privacy-information-for-application-management"></a>Informações de privacidade para gestão de aplicações  

 Gestão de aplicações permite-lhe executar qualquer aplicação, programa ou script em qualquer cliente na hierarquia. O Configuration Manager não possui nenhum controle sobre os tipos de aplicações, programas ou scripts que execute ou o tipo de informações que transmitem. Durante o processo de implantação do aplicativo, Configuration Manager pode transmitir informações que identifica o dispositivo e as contas de início de sessão entre clientes e servidores.  

 O Configuration Manager mantém informações de estado sobre o processo de implantação de software. Informações de estado de implementação de software não encriptadas durante a transmissão, a menos que o cliente comunica através de HTTPS. As informações de estado não estão armazenadas no formato encriptado na base de dados.  

 A utilização de instalação da aplicação remotamente, interativamente ou silenciosamente instalar software nos clientes do Configuration Manager pode ser sujeita aos termos de licença de software para o software. Esse uso é separado dos termos de licenciamento de Software para o System Center Configuration Manager. Reveja e aceite os termos de licenciamento para Software antes de implementar software utilizando o Gestor de configuração sempre.  

 O Configuration Manager recolhe os diagnósticos e dados de utilização sobre aplicativos, que é utilizada pela Microsoft para melhorar versões futuras. Para obter mais informações, consulte [diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).

 Implementação de aplicações não acontece por predefinição e requer vários passos de configuração.  

 As seguintes funcionalidades ajudam a implementação eficaz do software:   

- **Afinidade dispositivo / utilizador** mapeia um utilizador para dispositivos. Um administrador do Configuration Manager implementa o software de um utilizador. O cliente instala automaticamente o software num ou mais computadores que o utilizador utilize com mais frequência.  

- O **catálogo de aplicações** é um Web site que permite que os utilizadores pedido instalar software.  

    > [!Note]  
    > A partir do Configuration Manager 1802, a funcionalidade primária do catálogo de aplicações agora está incluída no Centro de Software. Para obter mais informações, consulte [configurar o Centro de Software](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).  

-  **Centro de software** é instalado automaticamente num dispositivo ao instalar o cliente do Configuration Manager. Os utilizadores alteram as definições, procurarem as aplicações e instalam aplicações a partir do Centro de Software.  

 Veja as secções seguintes para obter informações de privacidade sobre [afinidade dispositivo / utilizador](#bkmk_privacy-uda) e [Centro de Software e o catálogo de aplicações](#bkmk_privacy-userex).  

 Antes de configurar a gestão de aplicações, considere os requisitos de privacidade.  


### <a name="bkmk_privacy-uda"></a> Afinidade dispositivo / utilizador  

-  O Configuration Manager pode transmitir informações entre clientes e sistemas de sites de ponto de gestão. As informações podem identificar a conta de computador e início de sessão e a utilização resumida para contas de início de sessão.  

-  As informações que são transmitidas entre o cliente e o servidor não são criptografadas, a menos que o ponto de gestão está configurado para exigir que os clientes comuniquem por HTTPS.  

-  Os computador e início de sessão conta informações de utilização, que são utilizadas para mapear um utilizador para um dispositivo, são armazenadas nos computadores cliente, enviadas para os pontos de gestão e, em seguida, armazenadas na base de dados do Configuration Manager. Por predefinição, as informações antigas são eliminadas da base de dados após 90 dias. O comportamento de eliminação é configurável através da definição da tarefa de manutenção do site **Eliminar Dados de Afinidade Dispositivo/Utilizador Desatualizados** .  

-  O Configuration Manager mantém informações de estado sobre a afinidade dispositivo / utilizador. Informações de estado não estão encriptadas durante a transmissão, a menos que os clientes são configurados para comunicar com pontos de gestão utilizando HTTPS. Informações de estado não estão armazenadas no formato encriptado na base de dados.  

-  Informações de utilização de computadores e início de sessão que são utilizadas para estabelecer a afinidade dispositivo / utilizador está sempre ativadas. Os utilizadores e os utilizadores administrativos podem fornecer informações de afinidade de dispositivo do utilizador.  


### <a name="bkmk_privacy-userex"></a> Centro de software e o catálogo de aplicações  

-  Centro de software e o catálogo de aplicações permitem que o administrador do Configuration Manager publicar qualquer aplicação ou o programa ou script para os utilizadores executarem. O Configuration Manager não possui nenhum controle sobre os tipos de programas ou scripts que são publicados no catálogo ou o tipo de informações que transmitem.  

-  O Configuration Manager pode transmitir informações entre clientes e as funções de sistema de sites do catálogo de aplicações. As informações podem identificar as contas de computador e início de sessão. As informações que são transmitidas entre o cliente e servidores não são criptografadas, a menos que estas funções de sistema de sites estiverem configuradas para exigir que os clientes estabelecem ligação através de HTTPS.  

-  As informações sobre o pedido de aprovação de aplicação são armazenadas na base de dados do Configuration Manager. Pedidos que são cancelados ou negados e as entradas de histórico de pedidos correspondentes são eliminadas por predefinição após 30 dias. O comportamento de eliminação é configurável através da definição da tarefa de manutenção do site **Eliminar Dados de Pedidos de Aplicação Desatualizados** . Pedidos de aprovação de aplicações que são aprovados e pendente Estados nunca são eliminados.  

-  Centro de software é instalado automaticamente quando instala o cliente do Configuration Manager num dispositivo.  

-  O catálogo de aplicações não está instalado por predefinição. Esta instalação requer vários passos de configuração.  

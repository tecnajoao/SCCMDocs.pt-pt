---
title: Segurança e privacidade para gestão de aplicações
titleSuffix: Configuration Manager
description: Saiba mais sobre orientações e recomendações de segurança e privacidade quando gerir aplicações
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 80ae609bccd60e68cfee76878bd7a461b5f61716
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="security-and-privacy-for-application-management-in-system-center-configuration-manager"></a>Segurança e privacidade para gestão de aplicações no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


##  <a name="security-guidance-for-application-management"></a>Orientações de segurança para gestão de aplicações  

|Orientações de segurança|Mais informações|  
|----------------------------|----------------------|  
|Configure os pontos do Catálogo de Aplicações para utilizarem ligações HTTPS e informe os utilizadores sobre os perigos dos Web sites maliciosos.|Configure o ponto de Web site do catálogo de aplicações e o ponto de serviço web de catálogo de aplicações para aceitarem ligações HTTPS. Com esta configuração, o servidor seja autenticado para os utilizadores e os dados transmitidos estão protegidos contra adulteração e visualização. Ajude a impedir ataques de engenharia social ensinando os utilizadores a ligar apenas a Web sites fidedignos.<br /><br /> Se não utilizar o HTTPS, não utilize as opções de configuração imagem corporativa, que mostram o nome da sua organização no catálogo de aplicações, como prova de identidade.|  
|Utilize a separação de funções e instale o ponto de Web sites do Catálogo de Aplicações e o ponto de serviço do Catálogo de Aplicações em servidores separados.|Se o ponto de Web site do catálogo de aplicações for comprometido, instale-o num servidor separado do ponto de serviço web do catálogo de aplicações. Este design ajuda a proteger os clientes do Configuration Manager e a infraestrutura do Configuration Manager. Esta configuração é especialmente importante se o ponto de Web site do catálogo de aplicações aceitar ligações de cliente a partir da Internet. Torna o servidor vulnerável a ataques.|  
|Informe os utilizadores de que devem fechar a janela do browser quando terminarem de utilizar o Catálogo de Aplicações.|Se os utilizadores navegarem para um Web site externo na mesma janela de browser que utilizaram para o Catálogo de Aplicações, o browser continuará a utilizar as definições de segurança adequadas aos sites fidedignos da intranet.|  
|Especifique manualmente a afinidade dispositivo / utilizador em vez de permitir que os utilizadores identifiquem o respetivo dispositivo primário. Não ative a configuração baseada na utilização.|Não considere as informações recolhidas junto dos utilizadores ou do dispositivo como autoritativos. Se implementar software através da utilização de afinidade dispositivo / utilizador não especifica um administrador fidedigno, o software poderá ser instalado em computadores e para os utilizadores que não estão autorizados a receber esse software.|  
|Configure sempre as implementações para transferirem conteúdo a partir de pontos de distribuição em vez de executarem a partir destes.|Quando configura implementações para transferir conteúdo de um ponto de distribuição e executar localmente, o Gestor de configuração cliente verifica o hash do pacote depois de transferir o conteúdo. O cliente elimina o pacote se o hash não coincidir com o hash existente na política. Em comparação, se configurar a implementação para execução direta a partir de um ponto de distribuição, o cliente do Configuration Manager não verificar o hash do pacote. Este comportamento significa que o cliente do Configuration Manager pode instalar software que tenha sido adulterado.<br /><br /> Se tiver de executar implementações diretamente a partir de pontos de distribuição, utilizar o NTFS, pelo menos, permissões nos pacotes em pontos de distribuição. Também utilize a segurança de protocolo de Internet (IPsec) para proteger o canal entre o cliente e os pontos de distribuição e entre os pontos de distribuição e o servidor do site.|  
|<a name="bkmk_interact"></a>Não permitir que os utilizadores interagem com aplicações, se ativar o **executar com direitos administrativos** ou **instalar para o sistema** opções.|Quando configura uma aplicação, pode definir a opção **permitir que os utilizadores visualizem e interajam com a instalação do programa**. Esta definição permite aos utilizadores responder a serem apresentados quaisquer pedidos necessários na interface de utilizador. Se também de configurar a aplicação para **executar com direitos administrativos**, ou a partir de versão 1802 **instalar para o sistema**, um atacante no computador que executa o programa poderá utilizar a interface de utilizador para aumentar os privilégios no computador cliente.<br /><br /> Utilize os programas que utilizam o Windows Installer para a configuração e de utilizador elevados privilégios para implementações de software que necessitem de credenciais administrativas. A configuração tem de ser executada no contexto de um utilizador que tenha credenciais administrativas. Por utilizador do Windows Installer privilégios elevados fornecer a forma mais segura de implementar as aplicações que tenham este requisito.|  
|Restrinja a capacidade de os utilizadores instalarem software interativamente utilizando a definição **Permissões de instalação** do cliente.|Configurar o **agente do computador** dispositivo cliente **permissões de instalação** definição para restringir os tipos de utilizadores que podem instalar o software utilizando o catálogo de aplicações ou centro de Software. Por exemplo, crie uma definição personalizada de cliente com **Permissões de instalação** definida como **Apenas administradores**. Em seguida, aplique esta definição de cliente numa coleção de servidores para impedir que os utilizadores sem permissões administrativas de instalar software nesses computadores.|  
|Para dispositivos móveis, implemente apenas aplicações assinadas.|Implemente aplicações para dispositivos móveis apenas se estiverem código assinado por uma autoridade de certificação (AC) considerada fidedigna pelo dispositivo móvel. Por exemplo:<br /><ul><li>Uma aplicação de um fornecedor assinada por uma AC conhecida, como VeriSign.</li><li>Uma aplicação interna que inicia sessão independente do Configuration Manager utilizando a AC interna.</li><li>Uma aplicação interna que seja assinada utilizando o Gestor de configuração ao criar o tipo de aplicação e utilizar um certificado de assinatura.</li></ul>|  
|Se assinar aplicações para dispositivos móveis utilizando o **Assistente para criar aplicação** no Configuration Manager, proteja a localização do ficheiro de certificado de assinatura e Proteja o canal de comunicação.|Para ajudar a proteger contra ataques de elevação de privilégios e ataques man-in-the-middle, guarde o ficheiro de certificado de assinatura numa pasta protegida. Utilize IPsec entre os seguintes computadores:<br /><ul><li>O computador que executa a consola do Configuration Manager</li><li>O computador que armazena o certificado de assinatura de ficheiro</li><li>O computador que armazena os ficheiros de origem da aplicação</li></ul> Em alternativa, assine a aplicação independente do Configuration Manager e antes de executar o **Assistente para criar aplicação**.|  
|Para proteger os computadores de referência, implemente controlos de acesso.|Quando um utilizador administrativo configurar o método de deteção num tipo de implementação navegando para um computador de referência, certifique-se de que esse computador não foi comprometido.|  
|Restrinja e monitorize os utilizadores administrativos que conceda as seguintes funções de segurança baseada em funções de gestão de aplicações:<br /><ul><li>**Administrador da aplicação**</li><li>**Autor da aplicação**</li><li> **Gestor de implementação de aplicação**</li></ul>|Mesmo quando configura a administração baseada em funções, os utilizadores administrativos que criem e implementem aplicações poderão ter mais permissões do que pensa. Por exemplo, os utilizadores administrativos que criar ou alterar uma aplicação podem selecionar aplicações dependentes que não se encontram no respectivo âmbito de segurança.|  
|Quando configurar ambientes virtuais do Microsoft Application Virtualization (App-V), selecione as aplicações que tenham o mesmo nível de confiança no ambiente virtual.|Porque as aplicações num ambiente virtual App-V podem partilhar recursos, como a área de transferência, configure o ambiente virtual para que as aplicações selecionadas tenham o mesmo nível de fidedignidade.<br /><br /> Para obter mais informações, consulte [ambientes virtuais App-V criar](../../apps/deploy-use/create-app-v-virtual-environments.md).|  
|Caso implemente aplicações para computadores Mac, certifique-se de que os ficheiros de origem são provenientes de uma fonte fidedigna.|A ferramenta CMAppUtil não valida a assinatura do pacote de origem, pelo que deve certificar-se de que o pacote provém de uma origem em que confia. A ferramenta CMAppUtil não consegue detetar se os ficheiros foram adulterados.|  
|Se implementar aplicações para computadores Mac, proteja a localização do **. cmmac** de ficheiros e Proteja o canal de comunicação quando importar este ficheiro para o Configuration Manager.|O **. cmmac** ficheiros que a ferramenta CMAppUtil gera e que é importado para o Configuration Manager não estão assinado ou validado. Para ajudar a impedir a adulteração deste ficheiro, guarde-o numa pasta protegida e utilize IPsec ou SMB entre os seguintes computadores:<br /><br /><ul><li>O computador que executa a consola do Configuration Manager</li><li>O computador que armazena o **. cmmac** ficheiro</li></ul>|  
|Se configurar um tipo de implementação de aplicações web, utilize HTTPS em vez de HTTP para proteger a ligação.|Se implementar uma aplicação web utilizando uma ligação HTTP em vez de uma ligação HTTPS, o dispositivo foi redirecionado para um servidor não autorizado. Dados que são transferidos entre o dispositivo e o servidor poderão ser adulterados.|  



##  <a name="security-issues-for-application-management"></a>Problemas de segurança para gestão de aplicações  

-   Os utilizadores com direitos restritos podem copiar ficheiros da cache do cliente no computador cliente.  

     Os utilizadores podem ler a cache do cliente, mas não é possível escrever no mesmo. Com permissões de leitura, um utilizador pode copiar ficheiros de instalação de aplicações de um computador para outro.  

-   Os utilizadores direitos restritos podem alterar ficheiros que registam o histórico de implementação de software no computador cliente.  

     Porque as informações de histórico de aplicação não estão protegidas, um utilizador pode alterar os ficheiros que indicam se uma aplicação é instalada.  

-   Os pacotes de App-V não são assinados.  

     Pacotes de App-V no Configuration Manager não suportam a assinatura. Assinaturas digitais, certifique-se o conteúdo é de uma origem fidedigna e não foi alterado em trânsito. Não há nenhuma atenuação para este problema de segurança. Seguir a prática de segurança para transferir o conteúdo de uma origem fidedigna e a partir de uma localização segura.  

-   As aplicações de App-V publicadas podem ser instaladas por todos os utilizadores do computador.  

     Quando uma aplicação de App-V é publicada num computador, todos os utilizadores que inicie sessão computador podem instalar a aplicação. Não é possível restringir os utilizadores podem instalar a aplicação depois da sua publicação.  

-   Não é possível restringir as permissões de instalação para o portal da empresa.  

     Embora seja possível configurar uma definição de cliente para restringir permissões de instalação, por exemplo, para os utilizadores primários de um dispositivo ou apenas aos administradores locais, esta definição não funciona para o portal da empresa. Este problema poderá resultar numa elevação de privilégios. Os utilizadores foi possível instalar uma aplicação que não deve ter permissão para instalar.  



##  <a name="BKMK_CertificatesSilverlight5"></a> Certificados para o Microsoft Silverlight 5 e modo de confiança elevada necessários para o catálogo de aplicações  
 Clientes do Configuration Manager necessitam do Microsoft Silverlight 5, que deve ser executado no modo de confiança elevada para que os utilizadores instalem software do catálogo de aplicações. Por predefinição, as aplicações Silverlight são executadas no modo de confiança parcial para impedir que acedam aos dados do utilizador. Se já não está instalado, o Configuration Manager instala automaticamente o Microsoft Silverlight 5 nos clientes. Por predefinição, o Configuration Manager define o agente do computador **permitir que aplicações Silverlight sejam executadas em modo de confiança elevada** definição de cliente para **Sim**. Esta definição permite-lhe com sessão iniciado e fidedigno modo de confiança elevada Silverlight aplicações pedido.  

 Quando instalar a função de sistema de sites do ponto de Web site do catálogo de aplicações, o cliente também instala uma certificado no arquivo de certificados fabricantes fidedignos computador em cada computador cliente do Configuration Manager de assinatura da Microsoft. As aplicações Silverlight assinadas por este certificado é executado no modo de confiança elevada, o que os computadores necessitam para instalar software no catálogo de aplicações. O Gestor de configuração gere automaticamente este certificado de assinatura. Para assegurar a continuidade do serviço, não elimine manualmente ou mover este certificado de assinatura da Microsoft.  

> [!WARNING]  
>  Quando ativada, o **permitir que aplicações Silverlight sejam executadas em modo de confiança elevada** definição de cliente permite que todas as aplicações Silverlight, que se encontram assinadas por certificados no arquivo de certificados fabricantes fidedignos no computador arquivo ou o utilizador, executado no modo de confiança elevada. A definição de cliente não é possível ativar o modo de confiança elevada especificamente para o catálogo de aplicações do Configuration Manager ou para o arquivo de certificados fabricantes fidedignos no arquivo do computador. Se o software maligno adiciona um certificado não autorizado no arquivo fabricantes fidedignos, software maligno que utiliza a aplicação Silverlight própria agora também pode executar no modo de confiança elevada.  

 Se definir o **permitir que aplicações Silverlight sejam executadas em modo de confiança elevada** definição **não**, os clientes não remova o certificado de assinatura da Microsoft.  

 Para obter mais informações sobre aplicações fidedignas no Silverlight, consulte [aplicações fidedignas](https://go.microsoft.com/fwlink/p/?LinkId=252842).  

 > [!NOTE]
 > A partir do Configuration Manager 1802, Silverlight está já não é instalado automaticamente. A funcionalidade principal do catálogo de aplicações está agora incluída no Centro de Software. Suporte para as extremidades de web site do catálogo de aplicações com a primeira atualização lançada após 1 de Junho de 2018.



##  <a name="privacy-information-for-application-management"></a>Informações de privacidade para gestão de aplicações  
 Gestão de aplicações permite-lhe executar qualquer aplicação, programa ou script em qualquer cliente na hierarquia. O Configuration Manager possui não controla os tipos de aplicações, programas ou scripts que executar ou o tipo de informações que transmitem. Durante o processo de implementação de aplicação, o Configuration Manager pode transmitir informações que identifica o dispositivo e as contas de início de sessão entre clientes e servidores.  

 O Configuration Manager mantém as informações de estado sobre o processo de implementação de software. Informações de estado de implementação de software não estão encriptadas durante a transmissão, a menos que o cliente comunica por HTTPS. As informações de estado não estão armazenadas em formato encriptado na base de dados.  

 A utilização da instalação da aplicação do Configuration Manager remoto, interativo ou silencioso instalar software nos clientes pode estar sujeita aos termos de licenciamento de software para esse software. Esta utilização é separada dos termos de licenciamento de Software para o System Center Configuration Manager. Reveja e aceite os termos de licenciamento para Software antes de implementar o software utilizando o Gestor de configuração sempre.  

 Implementação de aplicação não acontece por predefinição e requer vários passos de configuração.  

 Duas funcionalidades que permitem uma implementação eficaz do software são a afinidade dispositivo/utilizador e o Catálogo de Aplicações:  

-   Afinidade dispositivo / utilizador mapeia um utilizador para dispositivos. Um administrador do Configuration Manager implementa software a um utilizador. O cliente instala automaticamente o software num ou mais computadores que o utilizador utiliza com maior frequência.  

-   O catálogo de aplicações é um Web site que permite que o software de pedido de utilizadores a instalar.  

 Veja as secções seguintes para obter informações de privacidade sobre a afinidade dispositivo/utilizador e o Catálogo de Aplicações.  

 Antes de configurar a gestão de aplicações, considere os requisitos de privacidade.  



##  <a name="user-device-affinity"></a>Afinidade dispositivo / utilizador  
-  O Configuration Manager pode transmitir informações entre clientes e sistemas de sites do ponto de gestão. As informações poderão identificar a conta de computador e inicie sessão e a utilização resumida das contas de início de sessão.  
-  As informações que são transmitidas entre o cliente e o servidor não estão encriptadas, a menos que o ponto de gestão está configurado para exigir que os clientes comuniquem por HTTPS.  
-  Os computador e inicie sessão utilização informações de conta, que são utilizadas para mapear um utilizador num dispositivo, são armazenadas nos computadores cliente, enviadas para os pontos de gestão e depois armazenadas na base de dados do Configuration Manager. Por predefinição, as informações antigas são eliminadas da base de dados após 90 dias. O comportamento de eliminação é configurável através da definição da tarefa de manutenção do site **Eliminar Dados de Afinidade Dispositivo/Utilizador Desatualizados** .
-  O Configuration Manager mantém as informações de estado sobre a afinidade de dispositivo do utilizador. As informações de estado não são encriptadas durante a transmissão, a menos que os clientes sejam configurados para comunicar com pontos de gestão por HTTPS. As informações de estado não são armazenadas em formato encriptado na base de dados.  
-  Computador, informações de utilização da conta de início de sessão e as informações de estado não são enviadas à Microsoft.  
-  Informações de utilização computador e início de sessão que são utilizadas para estabelecer a afinidade dispositivo / utilizador está sempre ativadas. Além disso, os utilizadores e os utilizadores administrativos podem fornecer informações sobre a afinidade dispositivo/utilizador.  



##  <a name="application-catalog"></a>Catálogo de aplicações  
-  O catálogo de aplicações permite que o administrador do Configuration Manager publicar qualquer aplicação ou programa ou script para os utilizadores executarem. O Configuration Manager possui não controla os tipos de programas ou scripts que são publicados no catálogo ou o tipo de informações que transmitem.    
-  O Configuration Manager pode transmitir informações entre clientes e as funções de sistema de sites do catálogo de aplicações. As informações poderão identificar as contas de computador e inicie sessão. As informações que são transmitidas entre o cliente e servidores não estão encriptadas, a menos que estas funções de sistema de sites são configuradas para exigir que os clientes estabelecem ligação através de HTTPS.  
-  As informações sobre o pedido de aprovação de aplicações são armazenadas na base de dados do Configuration Manager. Pedidos que são cancelados ou negados e as entradas do histórico de pedido correspondente são eliminadas por predefinição após 30 dias. O comportamento de eliminação é configurável através da definição da tarefa de manutenção do site **Eliminar Dados de Pedidos de Aplicação Desatualizados** . Pedidos de aprovação de aplicações que são aprovados e pendente Estados nunca são eliminados.  
-  As informações que são enviadas de e para o Catálogo de Aplicações não são enviadas à Microsoft.  
-  Por predefinição, o Catálogo de Aplicações não está instalado. Esta instalação requer vários passos de configuração.  

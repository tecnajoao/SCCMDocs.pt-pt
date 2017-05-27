---
title: "Segurança e privacidade para gestão de aplicações | Documentos do Microsoft"
description: "Segurança e privacidade melhores práticas para a gestão de aplicações no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 521b90b9d497818a4c1e546fca38cd15d4cab487
ms.openlocfilehash: 6ee99fa0c07676f004e41a50bf16d0d17604e790
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="security-and-privacy-for-application-management-in-system-center-configuration-manager"></a>Segurança e privacidade para gestão de aplicações no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


##  <a name="security-best-practices-for-application-management"></a>Melhores práticas de segurança da gestão de aplicações  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Configure os pontos do Catálogo de Aplicações para utilizarem ligações HTTPS e informe os utilizadores sobre os perigos dos Web sites maliciosos.|Configure o ponto de Web sites do Catálogo de Aplicações e o ponto de serviço Web do Catálogo de Aplicações para aceitarem ligações HTTPS, por forma a que o servidor seja autenticado para os utilizadores e os dados transmitidos sejam protegidos contra adulteração e visualização. Ajude a evitar ataques de engenharia social ensinando os utilizadores a ligar apenas a Web sites fidedignos.<br /><br /> Não utilize as opções de configuração de imagem corporativa que apresentam o nome da sua organização no catálogo de aplicações como prova de identidade quando não utilizar HTTPS.|  
|Utilize a separação de funções e instale o ponto de Web sites do Catálogo de Aplicações e o ponto de serviço do Catálogo de Aplicações em servidores separados.|Se o ponto de Web site do catálogo de aplicações estiver comprometido, instale num servidor separado do ponto de serviço web do catálogo de aplicações. Isto irá ajudar a proteger a infraestrutura do Configuration Manager e os clientes do Configuration Manager. Isto é especialmente importante se o ponto de Web sites do Catálogo de Aplicações aceitar ligações de cliente a partir da Internet, porque esta configuração torna o servidor vulnerável a ataques.|  
|Informe os utilizadores de que devem fechar a janela do browser quando terminarem de utilizar o Catálogo de Aplicações.|Se os utilizadores navegarem para um Web site externo na mesma janela de browser que utilizaram para o Catálogo de Aplicações, o browser continuará a utilizar as definições de segurança adequadas aos sites fidedignos da intranet.|  
|Especifique manualmente a afinidade dispositivo / utilizador em vez de permitir que os utilizadores identifiquem o respetivo dispositivo primário. Não ative a configuração baseada na utilização.|Não considere informações recolhidas junto dos utilizadores ou do dispositivo autoritativas. Se implementar software utilizando uma afinidade dispositivo/utilizador não especificada por um utilizador administrativo fidedigno, o software poderá ser instalado em computadores e para utilizadores que não têm autorização para receber esse software.|  
|Configure sempre as implementações para transferirem conteúdo a partir de pontos de distribuição em vez de executarem a partir destes.|Quando configura implementações para transferir conteúdo de um ponto de distribuição e execução local, o Configuration Manager cliente verifica o hash do pacote depois de transferir o conteúdo. O cliente rejeita o pacote se o hash não coincidir com o hash na política. Em comparação, se configurar a implementação para execução direta a partir de um ponto de distribuição, o cliente do Configuration Manager não verifique se o hash do pacote, o que significa que o Configuration Manager de cliente pode instalar o software que tenha sido adulterado.<br /><br /> Se tiver de executar implementações diretamente a partir de pontos de distribuição, utilize NTFS, pelo menos, permissões nos pacotes em pontos de distribuição e, utilizar segurança do protocolo Internet (IPsec) para proteger o canal entre o cliente e os pontos de distribuição e entre os pontos de distribuição e o servidor do site.|  
|Não permitir que os utilizadores interajam com programas se a **executar com direitos administrativos** opção é necessária.|Quando configurar um programa, pode definir o **permitir que os utilizadores interajam com este programa** opção para que os utilizadores possam responder a qualquer pedidos necessários na interface de utilizador. Se o programa também for configurado com **Executa com direitos de administrador**, um atacante no computador que executa o programa poderá utilizar a interface de utilizador para aumentar os privilégios no computador cliente.<br /><br /> Utilize programas que utilizam o Windows Installer para a configuração e por utilizador privilégios elevados para de implementações de software que necessitem de credenciais administrativas. Programa de configuração tem de ser executado no contexto de um utilizador que não tenha credenciais administrativas. Privilégios elevados por utilizador do Windows Installer fornecer a forma mais segura de implementar aplicações que tenham este requisito.|  
|Restrinja a capacidade de os utilizadores instalarem software interativamente utilizando a definição **Permissões de instalação** do cliente.|Configurar o **agente do computador** dispositivo cliente **permissões de instalação** definição para restringir os tipos de utilizadores que podem instalar software utilizando o catálogo de aplicações ou o Centro de Software. Por exemplo, crie uma definição personalizada de cliente com **Permissões de instalação** definida como **Apenas administradores**. Em seguida, aplique esta definição de cliente para uma coleção de servidores para impedir os utilizadores sem permissões administrativas de instalar software nesses computadores.|  
|Para dispositivos móveis, implemente apenas aplicações assinadas.|Implemente aplicações para dispositivos móveis apenas se estiverem assinada por código por uma autoridade de certificação (AC) considerada fidedigna pelo dispositivo móvel. Por exemplo:<br /><br /><ul><li>Uma aplicação de um fornecedor assinada por uma AC conhecida, como o VeriSign.</li><li>Uma aplicação interna que seja assinada independente do Configuration Manager utilizando a AC interna.</li><li>Uma aplicação interna que seja assinada utilizando o Configuration Manager quando cria o tipo de aplicação e utilizar um certificado de assinatura.</li></ul>|  
|Se assinar aplicações para dispositivos móveis utilizando o **Assistente para criar aplicação** no Configuration Manager, proteja a localização do ficheiro de certificado de assinatura e Proteja o canal de comunicação.|Para ajudar a proteger contra a elevação de privilégios e ataques man-in-the-middle, guarde o ficheiro de certificado de assinatura numa pasta protegida e utilize IPsec ou Server Message Block (SMB) entre os seguintes computadores:<br /><br /><ul><li>O computador que executa a consola do Configuration Manager</li><li>O computador que armazena o certificado de assinatura de ficheiro</li><li>O computador que armazena os ficheiros de origem da aplicação</li></ul> Em alternativa, assine a aplicação independente do Configuration Manager e antes de executar o **Assistente para criar aplicação**.|  
|Implemente controlos de acesso para proteger computadores de referência.|Quando um utilizador administrativo configurar o método de deteção num tipo de implementação navegando para um computador de referência, certifique-se de que esse computador não foi comprometido.|  
|Restrinja e monitorize os utilizadores administrativos a quem sejam concedidas as funções de segurança baseadas em funções relacionadas com gestão de aplicações:<br /><br /><ul><li>**Administrador da aplicação**</li><li>**Autor da aplicação**</li><li> **Gestor de implementação de aplicações**</li></ul>|Mesmo quando configura a administração baseada em funções, os utilizadores administrativos que criem e implementem aplicações poderão ter mais permissões do que pensa. Por exemplo, os utilizadores administrativos que criar ou alterar uma aplicação podem selecionar aplicações dependentes que não estão no seu âmbito de segurança.|  
|Quando configurar ambientes virtuais do Microsoft Application Virtualization (App-V), selecione as aplicações que tenham o mesmo nível de confiança no ambiente virtual.|Uma vez que as aplicações de um ambiente virtual de App-V podem partilhar recursos, como a área de transferência, configure o ambiente virtual para que as aplicações selecionadas tenham o mesmo nível de confiança.<br /><br /> Para obter mais informações, consulte o artigo [ambientes virtuais App-V criar](../../apps/deploy-use/create-app-v-virtual-environments.md).|  
|Caso implemente aplicações para computadores Mac, certifique-se de que os ficheiros de origem são provenientes de uma fonte fidedigna.|A ferramenta CMAppUtil não valida a assinatura do pacote de origem, pelo que deve certificar-se de que o pacote provém de uma origem em que confia. A ferramenta CMAppUtil não consegue detetar se os ficheiros foram adulterados.|  
|Se implementar aplicações para computadores Mac, proteja a localização do **. cmmac** de ficheiros e Proteja o canal de comunicação quando importar este ficheiro para o Configuration Manager.|O **. cmmac** ficheiro que a ferramenta CMAppUtil gera e que é importado para o Configuration Manager não é assinado ou validado. Para ajudar a impedir a adulteração deste ficheiro, guarde-o numa pasta protegida e utilize IPsec ou SMB entre os seguintes computadores:<br /><br /><ul><li>O computador que executa a consola do Configuration Manager</li><li>O computador que armazena o **. cmmac** ficheiro</li></ul>.|  
|Se configurar um tipo de implementação de aplicações web, utilize HTTPS em vez de HTTP para proteger a ligação.|Se implementar uma aplicação web utilizando uma ligação HTTP em vez de uma ligação HTTPS, o dispositivo poderá ser redirecionado para um servidor não autorizado e os dados transferidos entre o dispositivo e o servidor poderão ser adulterados.|  

##  <a name="security-issues-for-application-management"></a>Problemas de segurança da gestão de aplicações  

-   Os utilizadores com direitos restritos podem copiar ficheiros da cache do cliente no computador cliente.  

     Os utilizadores podem ler a cache do cliente, mas não conseguem escrever nela. Com permissões de leitura, um utilizador pode copiar ficheiros de instalação de aplicações de um computador para outro.  

-   Os utilizadores com direitos restritos podem alterar ficheiros que registam o histórico de implementação de software no computador cliente.  

     Como as informações de histórico da aplicação não são protegidas, um utilizador pode alterar os ficheiros que indicam se uma aplicação é instalada.  

-   Os pacotes de App-V não são assinados.  

     Pacotes de App-V no Configuration Manager não suportam assinatura para confirmar que o conteúdo é de uma origem fidedigna e que não foi alterado em trânsito. Não existe nenhuma atenuação para este problema de segurança. Certifique-se de que segue o recomendado de segurança para transferir o conteúdo de uma origem fidedigna e a partir de uma localização segura.  

-   As aplicações de App-V publicadas podem ser instaladas por todos os utilizadores do computador.  

     Quando uma aplicação de App-V é publicada num computador, todos os utilizadores que iniciem sessão nesse computador podem instalar a aplicação. Isto significa que não é possível restringir os utilizadores podem instalar a aplicação depois da sua publicação.  

-   Não é possível restringir as permissões de instalação para o portal da empresa.  

     Embora seja possível configurar uma definição de cliente para restringir permissões de instalação, por exemplo, aos utilizadores primários de um dispositivo ou apenas aos administradores locais, esta definição não funciona para o portal da empresa. Isto pode resultar numa elevação de privilégios porque os utilizadores podem instalar uma aplicação que não deve ter permissão para instalar.  

##  <a name="BKMK_CertificatesSilverlight5"></a>Certificados do Microsoft Silverlight 5 e modo de confiança elevada necessários para o catálogo de aplicações  
 Clientes do Configuration Manager necessitam do Microsoft Silverlight 5, que deve ser executado no modo de confiança elevada para os utilizadores instalarem o software a partir do catálogo de aplicações. Por predefinição, as aplicações Silverlight são executadas no modo de confiança parcial para impedir que acedam aos dados do utilizador. Configuration Manager instala automaticamente Microsoft Silverlight 5 nos clientes se não estiver já instalado. Por predefinição, o Configuration Manager define o agente do computador **permitir que aplicações Silverlight sejam executadas em modo de confiança elevada** definição de cliente para **Sim**. Esta definição permite assinado e fidedigno modo de confiança elevada Silverlight aplicações pedido.  

 Ao instalar a função de sistema de sites do ponto de Web site do catálogo de aplicações, o cliente também instala uma certificado no arquivo de certificados fabricantes fidedignos computador em cada computador de cliente do Configuration Manager de assinatura da Microsoft. Este certificado permite que as aplicações Silverlight assinadas por este certificado executar no modo de confiança elevada que os computadores necessitam para instalar o software a partir do catálogo de aplicações. O Configuration Manager gere automaticamente este certificado de assinatura. Para assegurar a continuidade do serviço, não elimine nem mova manualmente este certificado de assinatura da Microsoft.  

> [!WARNING]  
>  Quando ativada, o **permitir que aplicações Silverlight sejam executadas em modo de confiança elevada** permite de definição de cliente armazenam todas as aplicações Silverlight assinadas por certificados no certificado de fabricantes fidedignos no arquivo do computador ou o utilizador executa em modo de confiança elevada. A definição de cliente não é possível ativar o modo de confiança elevada especificamente para o catálogo de aplicações do Configuration Manager ou para o arquivo de certificados fabricantes fidedignos no arquivo do computador. Se for adicionado um certificado não autorizado ao arquivo Fabricantes Fidedignos por software maligno, no arquivo de utilizador por exemplo, o software maligno que utiliza uma aplicação Silverlight própria poderá agora ser executado também no modo de confiança elevada.  

 Se definir o **permitir que aplicações Silverlight sejam executadas em modo de confiança elevada** definição de cliente para **não**, isto não remove o certificado de assinatura da Microsoft dos clientes.  

 Para mais informações sobre aplicações fidedignas no Silverlight, consulte o artigo [aplicações fidedignas](http://go.microsoft.com/fwlink/p/?LinkId=252842).  

##  <a name="privacy-information-for-application-management"></a>Informações de privacidade da gestão de aplicações  
 Gestão de aplicações permite-lhe para executar qualquer aplicação, o programa ou o script em qualquer computador cliente ou dispositivo móvel do cliente na hierarquia. O Configuration Manager possui não controla os tipos de aplicações, programas ou scripts que executar ou o tipo de informações transmitem. Durante o processo de implementação de aplicação do Configuration Manager pode transmitir informações que identificam o dispositivo e o início de sessão contas entre clientes e servidores.  

 O Configuration Manager mantém as informações de estado sobre o processo de implementação de software. As informações do estado de implementação do software não são encriptadas durante a transmissão, a menos que o cliente efetue a comunicação por HTTPS. As informações de estado não são armazenadas em formato encriptado na base de dados.  

 A utilização de instalação da aplicação do Configuration Manager remoto, interativo ou silencioso instalar software nos clientes pode estar sujeita aos termos de licenciamento de software para esse software. Esta utilização é separada dos termos de licenciamento de Software para o System Center Configuration Manager. Reveja e aceite os termos de licenciamento para Software antes de implementar software utilizando o Gestor de configuração sempre.  

 Implementação de aplicação não acontece por predefinição e requer vários passos de configuração.  

 Duas funcionalidades que permitem uma implementação eficaz do software são a afinidade dispositivo/utilizador e o Catálogo de Aplicações:  

-   Afinidade dispositivo / utilizador mapeia um utilizador para dispositivos para que um administrador do Configuration Manager pode implementar software num utilizador e o software é instalado automaticamente num ou mais computadores que o utilizador utiliza mais frequentemente.  

-   O catálogo de aplicações é um Web site que permite aos utilizadores pedido software para instalar.  

 Veja as secções seguintes para obter informações de privacidade sobre a afinidade dispositivo/utilizador e o Catálogo de Aplicações.  

 Antes de configurar a gestão de aplicações, considere os requisitos de privacidade.  

##  <a name="user-device-affinity"></a>Afinidade dispositivo / utilizador  
-  O Configuration Manager pode transmitir informações entre clientes e sistemas de sites de ponto de gestão. As informações podem identificar a conta de computador e início de sessão e a utilização resumida das contas de início de sessão.  
-  As informações que são transmitidas entre o cliente e o servidor não estão encriptadas, a menos que o ponto de gestão está configurado para exigir que os clientes comuniquem por HTTPS.  
-  Computador e início de sessão na conta informações de utilização são utilizadas para mapear um utilizador para um dispositivo são armazenadas nos computadores cliente, enviadas aos pontos de gestão e depois armazenadas na base de dados do Configuration Manager. Por predefinição, as informações antigas são eliminadas da base de dados após 90 dias. O comportamento de eliminação é configurável através da definição da tarefa de manutenção do site **Eliminar Dados de Afinidade Dispositivo/Utilizador Desatualizados** .
-  O Configuration Manager mantém as informações de estado sobre a afinidade dispositivo / utilizador. As informações de estado não são encriptadas durante a transmissão, a menos que os clientes sejam configurados para comunicar com pontos de gestão por HTTPS. As informações de estado não são armazenadas em formato encriptado na base de dados.  
-  Computador, informações de utilização da conta de início de sessão e informações de estado não são enviadas à Microsoft.  
-  Informações de utilização de computadores e início de sessão são utilizadas para estabelecer a afinidade dispositivo / utilizador estão sempre ativadas. Além disso, os utilizadores e os utilizadores administrativos podem fornecer informações sobre a afinidade dispositivo/utilizador.  

##  <a name="application-catalog"></a>Catálogo de aplicações  
-  O catálogo de aplicações permite que o administrador do Configuration Manager publicar quaisquer aplicações ou programa ou script para os utilizadores para executarem. O Configuration Manager possui não controla os tipos de programas ou scripts que são publicados no catálogo ou o tipo de informações transmitem.    
-  O Configuration Manager pode transmitir informações entre clientes e as funções de sistema de sites do catálogo de aplicações. As informações podem identificar as contas de computador e início de sessão. As informações que são transmitidas entre o cliente e os servidores não estão encriptadas, a menos que estas funções do sistema de sites sejam configuradas para requerer que os clientes estabeleçam ligação através do HTTPS.  
-  As informações sobre o pedido de aprovação de aplicações são armazenadas na base de dados do Configuration Manager. Pedidos que são cancelados ou negados e as entradas do histórico de pedidos correspondente são eliminadas por predefinição após 30 dias. O comportamento de eliminação é configurável através da definição da tarefa de manutenção do site **Eliminar Dados de Pedidos de Aplicação Desatualizados** . Pedidos de aprovação de aplicações que são aprovados em pendente Estados nunca são eliminados.  
-  As informações que são enviadas de e para o Catálogo de Aplicações não são enviadas à Microsoft.  
-  Por predefinição, o Catálogo de Aplicações não está instalado. Esta instalação requer vários passos de configuração.  


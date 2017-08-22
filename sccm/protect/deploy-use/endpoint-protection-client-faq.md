---
title: Cliente do Endpoint Protection perguntas mais frequentes | Microsoft Docs
description: "Obtenha respostas às perguntas mais frequentes sobre o Windows Defender e Endpoint Protection."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3aaa9d2-a40e-42b1-ad75-5a115351729e
caps.latest.revision: "15"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: b88bc5f734b85527b81e5848deb0617db4c8dfbc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="endpoint-protection-client-frequently-asked-questions"></a>Perguntas mais frequentes de cliente do Endpoint Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Este artigo destina-se a utilizadores de computador cujo administrador de TI implementou o Windows Defender ou o Endpoint Protection no respetivo computador gerido. O conteúdo não podem ser aplicadas a outro software antimalware. Microsoft System Center Endpoint Protection gere o Windows Defender no Windows 10. Também pode implementar e gerir o cliente do Endpoint Protection nos computadores anteriores ao Windows 10. Embora o Windows Defender seja descrito neste artigo, as respetivas informações também se aplicam ao Endpoint Protection.  

-   [Por que razão necessito de software antivírus e antispyware?](#why-do-i-need-antivirus-and-antispyware-software)  
-   [Como posso saber se o meu computador está infetado com software malicioso?](#how-can-i-tell-if-my-computer-is-infected-with-malicious-software)
-   [Como posso encontrar a versão do Windows Defender?](#how-can-i-find-the-version-of-windows-defender)
-   [O que posso fazer se o Windows Defender ou Endpoint Protection detetar software malicioso no meu computador?](#what-should-i-do-if-windows-defender-or-endpoint-protection-detects-software-on-my-computer)  
-   [O que é um vírus?](#what-is-a-virus)  
-   [O que é um spyware?](#what-is-spyware)  
-   [O que é a diferença entre vírus, spyware e outro software potencialmente prejudicial?](#hat-s-the-difference-between-viruses-spyware-and-other-potentially-harmful-software)  
-   [Onde vírus, spyware e outro software potencialmente indesejável provenientes?](#where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from)  
-   [Pode obter software malicioso sem o saber?](#can-i-get-malicious-software-without-knowing-it)  
-   [Por que motivo é importante rever os contratos de licença antes de instalar software?](#why-is-it-important-to-review-license-agreements-before-installing-software)  
-   [O que é a diferença entre o Endpoint Protection e o Windows Defender?](#what-s-the-difference-between-endpoint-protection-and-windows-defender)  
-   [Por que motivo o Windows Defender não Deteta cookies?](#why-doesn-t-windows-defender-detect-cookies)  
-   [Como posso impedir software maligno?](#how-can-i-prevent-malware)  
-   [Quais são as definições de vírus e spyware?](#what-are-virus-and-spyware-definitions)  
-   [Como mantenho as definições de vírus e spyware atualizadas?](#how-do-i-keep-virus-and-spyware-definitions-up-to-date)  
-   [Como remover ou restaurar itens colocados em quarentena pelo Windows Defender ou o Endpoint Protection?](#how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection)  
-   [O que é a proteção em tempo real?](#what-is-real-time-protection)  
-   [Como posso saber que o Windows Defender ou o Endpoint Protection está em execução no meu computador?](#how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer)
-   [Como configurar alertas do Windows Defender ou o Endpoint Protection?](#how-to-set-up-windows-defender-or-endpoint-protection-alerts)  

##  <a name="why-do-i-need-antivirus-and-antispyware-software"></a>Por que razão necessito de software antivírus e antispyware?  

 É fundamental certificar-se de que o computador está a executar software que protege contra software maligno. O software maligno, que inclui vírus, spyware ou outro software potencialmente indesejável, pode tentar instalar-se no seu computador sempre que estabelecer ligação à Internet. Também pode infetar o computador quando instala um programa com um CD, DVD ou outro suporte de dados amovível. O software malicioso também pode ser programado para ser executado em momentos inesperados e não apenas quando é instalado.  

 O Windows Defender ou o Endpoint Protection oferece três formas de ajudar a impedir que software malicioso infete o seu computador:  

-   **Utilizar a proteção em tempo real** - proteção em tempo real permite que o Windows Defender monitorizar o seu computador sempre e alerta-o quando o software malicioso, incluindo vírus, spyware ou outro potencialmente software indesejável tenta instalação ou execução no seu computador. Em seguida, o Windows Defender suspende o software e permite que o utilizador siga a recomendação sobre o software ou execute uma ação alternativa.  

    |**Opção de proteção em tempo real** |**objetivo** |

    |-|-|  
    | Analisar todas as transferências | Esta opção monitoriza ficheiros e programas que sejam transferidos, incluindo ficheiros que são automaticamente transferidos através do Windows Internet Explorer e do Microsoft Outlook® Express, tal como ActiveX® controla e programas de instalação de software. Estes ficheiros podem ser transferidos, instalados ou executados pelo próprio browser. O software maligno, incluindo vírus, spyware e outro software potencialmente indesejável, pode ser incluído com estes ficheiros e instalado sem o conhecimento do utilizador.<br /><br /> Com a opção de proteção em tempo real, o Windows Defender monitoriza sempre o seu computador e verifica a existência de quaisquer programas ou ficheiros maliciosos que possa ter transferido. Esta funcionalidade de monitorização significa que o Windows Defender não necessita de abrandar a sua navegação ou a experiência de e-mail, exigindo uma verificação de quaisquer ficheiros ou programas possa querer transferir. |  
    | Monitorizar a atividade de programas e ficheiros no seu computador | Esta opção monitoriza quando os ficheiros e programas começam a ser executado no seu computador e, em seguida, alerta-o sobre quaisquer ações desempenhadas e as ações efetuadas nos mesmos. Isto é importante porque o software malicioso pode utilizar vulnerabilidades em programas que tenha instalado para executar o software malicioso ou indesejável sem o conhecimento do utilizador. Por exemplo, o spyware pode ser executado automaticamente em segundo plano quando inicia um programa que utiliza com frequência. O Windows Defender monitoriza os seus programas e alerta-o se detetar atividade suspeita. |  
    | Ativar monitorização de comportamento | Esta opção monitoriza coleções de comportamento de padrões suspeitos que poderão não ser detetados pelos métodos tradicionais de deteção de antivírus. |  

    | Ativar o sistema de inspeção de rede | Esta opção ajuda a proteger o computador contra exploits "de dia zero" de vulnerabilidades conhecidas, diminuindo o período de tempo entre o momento em que uma vulnerabilidade é detetada e uma atualização é aplicada. |  

-   **Opções de análise** -pode utilizar o Windows Defender para analisar quanto a potenciais ameaças, tais como vírus, spyware e outro software malicioso que pode colocar o seu computador em risco. Também pode utilizá-las para agendar análises regulares e para remover software malicioso detetado durante uma análise.  

-   **Comunidade do Microsoft Active Protection Service** -Comunidade do Microsoft Active Protection Service online ajuda-o a ver como outras pessoas respondem a software que ainda não tenha sido classificado relativamente a riscos. Pode utilizar estas informações para ajudar a escolher se pretende permitir este software no seu computador. Por sua vez, se participar, as opções são adicionadas às classificações da comunidade para ajudar outras pessoas a decidir o que fazer.  

##  <a name="how-can-i-tell-if-my-computer-is-infected-with-malicious-software"></a>Como posso saber se o meu computador está infetado com software malicioso?  

 Poderá ter alguma forma de software malicioso, incluindo vírus, spyware ou outro software potencialmente indesejável, no seu computador se:  

-   Reparar em novas barras de ferramentas, ligações ou favoritos que não adicionou intencionalmente ao seu browser.  

-   A sua home page, o ponteiro do rato ou o programa de pesquisa mudar inesperadamente.  

-   Escrever o endereço de um site específico, tal como um motor de busca, mas for direcionado para um site diferente sem aviso prévio.  

-   Ficheiros forem automaticamente eliminados do seu computador.  

-   O computador for utilizado para atacar outros computadores.  

-   Vir janelas de publicidade, mesmo que não esteja na Internet.  

-   Subitamente o seu computador começar a funcionar mais lentamente do que o normal. Nem todos os problemas de desempenho do computador são causados por software malicioso, mas o software malicioso, sobretudo o spyware, pode causar uma mudança considerável.  

Pode existir software malicioso no seu computador, mesmo que não veja qualquer sintoma. Este tipo de software pode recolher informações sobre si e o seu computador sem o seu conhecimento ou consentimento. Para ajudar a proteger a sua privacidade e o seu computador, deve executar sempre o Windows Defender ou o Endpoint Protection.  

## <a name="how-can-i-find-the-version-of-windows-defender"></a>Como posso encontrar a versão do Windows Defender?
 Para ver a versão do Windows Defender em execução no seu computador, abra o Windows Defender (clique **iniciar** e, em seguida, procure **Windows Defender**), clique em **definições**e desloque-se na parte inferior das definições do Windows Defender para localizar **informação da versão**.

##  <a name="what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer"></a>O que posso fazer se o Windows Defender ou Endpoint Protection detetar software malicioso no meu computador?  

 Se o Windows Defender detetar software malicioso ou software potencialmente indesejável no computador (ao monitorizar o computador com a proteção em tempo real ou após a execução de uma análise), notifica-o sobre o item detetado, apresentando uma mensagem de notificação no canto inferior direito do ecrã.  

 A mensagem de notificação inclui um botão **Limpar computador** e uma ligação **Mostrar detalhes** que lhe permite ver informações adicionais sobre o item detetado. Clique na ligação **Mostrar detalhes** para abrir a janela **Detalhes das potenciais ameaças** para obter informações adicionais sobre o item detetado. Pode agora escolher a ação a aplicar ao item ou clicar em **Limpar computador**. Se precisar de ajuda para determinar a ação a aplicar ao item detetado, utilize o nível de alerta que o Windows Defender atribuiu ao item como guia (para mais informações, consulte Compreender os níveis de alerta).  

 Os níveis de alerta ajudam-no a escolher a forma de resposta face a vírus, spyware e a outro software potencialmente indesejável. Apesar de o Windows Defender recomendar que remova todos os vírus e spyware, nem todo o software assinalado é malicioso ou indesejável. As seguintes informações podem ajudá-lo a decidir o que fazer se o Windows Defender detetar software potencialmente indesejável no computador.  

 Dependendo do nível de alerta, pode selecionar uma das seguintes ações a aplicar ao item detetado:  

-   **Remover** -esta ação elimina permanentemente o software a partir do seu computador.  

-   **Quarentena** -esta ação coloca a em quarentena o software de modo a que não é possível executar. Quando o Windows Defender coloca o software em quarentena, este move-o para outra localização no seu computador e, em seguida, impede que o software seja executado até decidir restaurá-lo ou removê-lo do computador.  

-   **Permitir** -esta ação adiciona o software para a lista de permitidos do Windows Defender e permite que seja executado no seu computador. O Windows Defender deixará de o alertar sobre riscos que o software possa implicar para a sua privacidade ou para o seu computador.  

 Se escolher **Permitir** para um item, tal como software, o Windows Defender deixará de o alertar sobre riscos que o software possa implicar para a sua privacidade ou para o seu computador. Por conseguinte, adicione software à lista de permitidos apenas se confiar no software e no publicador do software.  

### <a name="how-to-remove-potentially-harmful-software"></a>Como remover software potencialmente prejudicial

Para remover todos os itens potencialmente prejudiciais ou indesejáveis que o Windows Defender deteta rápida e facilmente, utilize a opção **Limpar computador** .  

1.  Quando vir a mensagem de notificação que é apresentada na Área de notificação depois de detetar potenciais ameaças, clique em **Limpar computador**.  

2.  O Windows Defender remove a potencial ameaça (ou ameaças) e, em seguida, notifica-o quando tiver concluído a limpeza do seu computador.  

3.  Para saber mais sobre as ameaças detetadas, clique no separador **Histórico** e selecione **Todos os itens detetados**.  

4.  Caso não veja todos os itens detetados, clique em **Ver detalhes**. Se lhe for pedida uma palavra-passe de administrador ou confirmação, escreva a palavra-passe ou confirme a ação. Em sistemas com o Windows XP, poderá ter de iniciar sessão como administrador neste computador.  

> [!NOTE]  
>  Durante a limpeza do computador, sempre que possível, o Windows Defender remove apenas a parte infetada de um ficheiro e não o ficheiro completo.  

##  <a name="what-is-a-virus"></a>O que é um vírus?  
 Os vírus informáticos são programas de software concebidos deliberadamente para interferir com o funcionamento do computador, para registar, danificar ou eliminar dados, ou para infetar outros computadores por toda a Internet. Os vírus frequentemente retardam as operações e, no processo, causam outros problemas.  

##  <a name="what-is-spyware"></a>O que é o spyware?  
 O spyware é software que pode instalar-se ou executar automaticamente no computador sem o seu consentimento ou sem fornecer-lhe aviso ou controlo adequado. O spyware pode não apresentar sintomas após infetar o seu computador, mas muitos programas maliciosos ou indesejáveis podem afetar o funcionamento do seu computador. Por exemplo, o spyware pode monitorizar o seu comportamento online ou recolher informações sobre si (incluindo informações que o possam identificar ou outras informações sensíveis), alterar definições no computador ou abrandar o funcionamento do computador.  

##  <a name="whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software"></a>O que é a diferença entre vírus, spyware e outro software potencialmente prejudicial?  
 Quer os vírus quer o spyware são instalados no computador sem o seu consentimento e ambos têm o potencial de ser intrusivos e destrutivos. Também têm a capacidade de capturar informações do computador e de danificar ou eliminar essas informações. Ambos podem afetar negativamente o desempenho do computador.  

 A principal diferença entre vírus e spyware reside na forma como se comportam no seu computador. O objetivo dos vírus, à semelhança dos organismos vivos, é infetar um computador, replicar-se e, em seguida, propagar-se pelo maior número de computadores possível. No entanto, o spyware, é mais um espião - pretende "mover para" do computador e ficar lá, desde que possível, enviando informações valiosas sobre o computador para uma origem externa enquanto existe.  

##  <a name="where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from"></a>Onde vírus, spyware e outro software potencialmente indesejável provenientes?  
 O software indesejável, tal como os vírus, pode ser instalado por Web sites ou programas que transfere ou instala utilizando um CD, DVD, disco rígido externo ou um dispositivo. O spyware é normalmente instalado através de software gratuito, tais como programas de partilha de ficheiros, proteções de ecrã ou barras de ferramentas de pesquisa.  

##  <a name="can-i-get-malicious-software-without-knowing-it"></a>Pode obter software malicioso sem o saber?  
 Sim, algum software malicioso pode ser instalado a partir de um Web site através de um script ou programa incorporado numa página Web. Outro tipo de software malicioso requer a sua ajuda para o instalar. Este tipo de software utiliza pop-ups Web ou software gratuito que requer a aceitação de um ficheiro transferível. No entanto, se mantiver o Microsoft Windows® atualizado e não reduzir as definições de segurança, pode minimizar as hipóteses de uma infeção.  

##  <a name="why-is-it-important-to-review-license-agreements-before-installing-software"></a>Por que motivo é importante rever os contratos de licença antes de instalar software?  
 Quando visita Web sites, não concorda automaticamente em transferir tudo que o site oferece. Se transferir software gratuito, como os programas de partilha de ficheiros ou as proteções de ecrã, leia o contrato de licença atentamente. Esteja atento a cláusulas que afirmam que deve aceitar anúncios e pop-ups da empresa ou que o software enviará determinadas informações de volta ao respetivo fabricante.  

##  <a name="whats-the-difference-between-endpoint-protection-and-windows-defender"></a>O que é a diferença entre o Endpoint Protection e o Windows Defender?  
 O Endpoint Protection é um software antimalware, o que significa que foi concebido para detetar e ajudar a proteger o computador contra uma ampla gama de software malicioso, incluindo vírus, spyware e outro software potencialmente indesejável. O Windows Defender, que é automaticamente instalado com o sistema operativo Windows, é software que deteta e para spyware.  

##  <a name="why-doesnt-windows-defender-detect-cookies"></a>Por que motivo o Windows Defender não Deteta cookies?  
 Os cookies são pequenos ficheiros de texto que Web sites colocam no seu computador para o arquivo de informações sobre si e as suas preferências. Web sites utilizam cookies para oferecer uma experiência personalizada e para recolher informações sobre a utilização do Web site. O Windows Defender não Deteta cookies porque não os considera uma ameaça à sua privacidade ou à segurança do computador. Maioria dos browsers permitem-lhe bloquear cookies.  

##  <a name="how-can-i-prevent-malware"></a>Como posso impedir software maligno?  
 Duas das principais preocupações dos utilizadores de computador hoje em dia são os vírus e o spyware. Em ambos os casos, embora estes possam ser um problema, pode defender-se contra eles com bastante facilidade com apenas um pouco de planeamento:  

-   Mantenha o software do computador atual e não se esqueça de instalar todas as correções. Lembre-se de atualizar regularmente o sistema operativo.  

-   Certifique-se de que o seu software antivírus e antisspyware, o Windows Defender, está a utilizar as atualizações mais recentes contra potenciais ameaças (consulte Como mantenho as definições de vírus e spyware atualizadas?). Certifique-se também de que está a utilizar sempre a versão mais recente do Windows Defender.  

-   Transfira apenas as atualizações a partir de origens seguras. Para sistemas operativos Windows, aceda sempre a [Microsoft Update](http://go.microsoft.com/fwlink/?LinkID=96304) (http://go.microsoft.com/fwlink/?LinkID=96304) e de outro software, utilize sempre os Web sites legítimos da empresa ou pessoa que os produz.  

-   Se receber um e-mail com um anexo e desconhecer a origem, deverá eliminá-lo imediatamente. Não transfira aplicações ou os ficheiros a partir de origens desconhecidas e tenha cuidado ao trocar ficheiros com outros utilizadores.  

-   Instale e utilize uma firewall. É recomendado que ative a Firewall do Windows.  

##  <a name="what-are-virus-and-spyware-definitions"></a>Quais são as definições de vírus e spyware?  
 Quando utiliza o Windows Defender ou o Endpoint Protection, é importante que tenha as definições de vírus e spyware atualizadas. As definições são ficheiros que atuam como uma enciclopédia crescente de potenciais ameaças de software. O Windows Defender ou o Endpoint Protection utiliza definições para determinar se o software que deteta é um vírus, spyware ou outro software potencialmente indesejável e, em seguida, para alertá-lo em relação a potenciais riscos. Para o ajudar a manter as definições atualizadas, o Windows Defender ou o Endpoint Protection funciona com o Microsoft Update para instalar automaticamente as novas definições à medida que são lançadas. Também pode configurar o Windows Defender ou o Endpoint Protection para verificar online a existência de definições atualizadas antes da análise.  

##  <a name="how-do-i-keep-virus-and-spyware-definitions-up-to-date"></a>Como mantenho as definições de vírus e spyware atualizadas?  
 As definições de vírus e spyware são ficheiros que atuam como uma enciclopédia de software malicioso conhecido, incluindo vírus, spyware e outro software potencialmente indesejável. Uma vez que o software malicioso está continuamente a ser desenvolvido, o Windows Defender ou o Endpoint Protection depende de definições atualizadas para determinar se o software que está a tentar instalar, executar ou alterar as definições no seu computador é um vírus, spyware ou outro software potencialmente indesejável.  

### <a name="to-automatically-check-for-new-definitions-before-scheduled-scans-recommended"></a>Para verificar automaticamente a existência de novas definições antes das análises agendadas (recomendadas)  

1.  Abra o cliente do Windows Defender ou do Endpoint Protection, clicando no ícone na área de notificação ou iniciando-o a partir do menu **Iniciar** .  

2.  Clique em **Definições**e, em seguida, clique em **Análise agendada**.  

3.  Certifique-se de que a caixa de verificação **Procurar as definições de vírus e spyware mais recentes antes de executar uma análise agendada** está selecionada e, em seguida, clique em **Guardar alterações**. Se lhe for pedida uma palavra-passe de administrador ou confirmação, escreva a palavra-passe ou confirme a ação.  

### <a name="to-check-for-new-definitions-manually"></a>Para verificar a existência de novas definições manualmente

 O Windows Defender ou o Endpoint Protection atualiza automaticamente as definições de vírus e spyware no seu computador. Se as definições ainda não foi atualizadas com mais de sete dias (por exemplo, se não ativou o seu computador para uma semana), o Windows Defender ou o Endpoint Protection será notificado, que as definições estão Desatualizadas.  

1.  Abra o cliente do Windows Defender ou do Endpoint Protection, clicando no ícone na área de notificação ou iniciando-o a partir do menu **Iniciar** .  

2.  Para verificar manualmente a existência de novas definições, clique no separador **Atualizar** e, em seguida, clique em **Atualizar definições**.  

##  <a name="how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>Como remover ou restaurar itens colocados em quarentena pelo Windows Defender ou o Endpoint Protection?  

 Quando o Windows Defender ou o Endpoint Protection coloca o software em quarentena, este move o software para outra localização no seu computador e, em seguida, impede que o software seja executado até decidir restaurá-lo ou removê-lo do computador.  

 Em todos os passos mencionados neste procedimento, se lhe for pedida uma palavra-passe de administrador ou confirmação, escreva a palavra-passe ou indique confirmação.  

###  <a name="to-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>Para remover ou restaurar itens colocados em quarentena pelo Windows Defender ou o Endpoint Protection


1.  Clique no separador **Histórico** , selecione **Itens em quarentena**e, em seguida, selecione a opção **Itens em quarentena** .  

2.  Clique em **Ver detalhes** para ver todos os itens.  

3.  Reveja cada item e, em cada um deles, clique em **Remover** ou **Restaurar**. Se pretender remover todos os itens em quarentena do seu computador, clique em **Remover tudo**.  

##  <a name="what-is-real-time-protection"></a>O que é a proteção em tempo real?  

 A proteção em tempo real permite que o Windows Defender monitorize sempre o computador e o alerte quando potenciais ameaças, tais como vírus e spyware, estiverem a tentar instalar-se ou a executar automaticamente no seu computador. Uma vez que esta funcionalidade é um elemento importante da forma como o Windows Defender ajuda a proteger o seu computador, deve certificar-se de que a proteção em tempo real está sempre ativada. Se a proteção em tempo real for desativada, o Windows Defender notifica-o e altera o computerâ€™ Estado s â "œAt riskâ".  

 Sempre que a proteção em tempo real detetar uma ameaça ou potencial ameaça, o Windows Defender apresenta uma notificação. Agora, pode escolher entre as seguintes opções:  

-   Clique em **Limpar computador** para remover o item detetado. O Windows Defender removerá automaticamente o item do computador.  

-   Clique na ligação **Mostrar detalhes** para apresentar a janela Detalhes das ameaças potenciais e, em seguida, escolha a ação a aplicar ao item detetado.  

 Pode escolher o software e as definições que pretende que o Windows Defender monitorize, mas recomendamos que ative a proteção em tempo real e ative todas as opções de proteção em tempo real. A tabela seguinte explica as opções disponíveis.  

|||  
|-|-|  
|**Opção de proteção em tempo real**|**Objetivo**|  
|Analisar todas as transferências|Esta opção monitoriza ficheiros e programas que sejam transferidos, incluindo ficheiros que são automaticamente transferidos através do Windows Internet Explorer e do Microsoft Outlook® Express, tal como controlos ActiveX® e programas de instalação de software. Estes ficheiros podem ser transferidos, instalados ou executados pelo próprio browser. O software maligno, incluindo vírus, spyware e outro software potencialmente indesejável, pode ser incluído com estes ficheiros e instalado sem o conhecimento do utilizador.<br /><br /> Com a opção de proteção em tempo real, o Windows Defender monitoriza sempre o seu computador e verifica a existência de quaisquer programas ou ficheiros maliciosos que possa ter transferido. Esta funcionalidade de monitorização significa que o Windows Defender não tem de abrandar a sua experiência de navegação ou e-mail, exigindo uma verificação de quaisquer ficheiros ou programas que possa querer transferir.|  
|Monitorizar a atividade dos ficheiros e programas no computador|Esta opção monitoriza quando os ficheiros e programas começam a ser executado no seu computador e, em seguida, alerta-o sobre quaisquer ações que executem e as ações executadas nos mesmos. Isto é importante porque o software malicioso pode utilizar vulnerabilidades em programas que tenha instalado para executar o software malicioso ou indesejável sem o conhecimento do utilizador. Por exemplo, o spyware pode ser executado automaticamente em segundo plano quando inicia um programa que utiliza com frequência. O Windows Defender monitoriza os seus programas e alerta o utilizador se detetar atividade suspeita.|  
|Ativar a monitorização de comportamento|Esta opção monitoriza coleções de comportamento em termos de padrões suspeitos que poderão não ser detetados pelos métodos tradicionais de deteção de antivírus.|  
|Ativar o Sistema de Inspeção de Rede|Esta opção ajuda a proteger o computador contra exploits de € â €œzero dayâ de vulnerabilidades conhecidas, diminuindo o período de tempo entre o momento em que uma vulnerabilidade é detetada e uma atualização é aplicada.|  

### <a name="to-turn-off-real-time-protection"></a>Para desativar a proteção em tempo real  

1.  Clique em **Definições**e, em seguida, clique em **Proteção em tempo real**.  

2.  Desmarque as opções de proteção em tempo real que pretende desativar e, em seguida, clique em **Guardar alterações**. Se lhe for pedida uma palavra-passe de administrador ou confirmação, escreva a palavra-passe ou confirme a ação.  

##  <a name="how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer"></a>Como posso saber que o Windows Defender ou o Endpoint Protection está em execução no meu computador?  

 Depois de instalar o Windows Defender no seu computador, pode fechar a janela principal e permitir que o Windows Defender seja executado em modo silencioso em segundo plano. O Windows Defender continuará a ser executado no computador, a monitorizá-lo e a ajudar a protegê-lo contra ameaças.  

 Obviamente, saberá que o Windows Defender está a ser executado sempre que este apresenta as mensagens de notificação na área de notificação. Estas notificações alertam-no para potenciais ameaças detetadas pelo Windows Defender.  

 Também irá receber outras notificações de alerta, por exemplo, se por alguma razão a proteção em tempo real tiver sido desativada, se não tiver atualizado as definições de vírus e spyware durante vários dias ou quando as atualizações ao programa ficarem disponíveis. O Windows Defender também apresenta por breves instantes uma notificação para informá-lo de que está a analisar o computador.  

> [!TIP]  

>Se não vir o ícone do Windows Defender na área de notificação, clique na seta na área de notificação para mostrar os ícones ocultos, incluindo o ícone do Windows Defender.  


 A cor do ícone depende do estado atual do seu computador:  

-   Verde indica que o estado do computador é "Protegido".  

-   Amarelo indica que o estado do computador é "Potencialmente não protegido".  

-   Vermelho indica que o estado do computador é "Em risco".  

##  <a name="how-to-set-up-windows-defender-or-endpoint-protection-alerts"></a>Como configurar alertas do Windows Defender ou o Endpoint Protection?  
 Quando o Windows Defender está a ser executado no seu computador, alerta-o automaticamente se detetar vírus, spyware ou outro software potencialmente indesejável. Também pode configurar o Windows Defender para o alertar caso execute software que ainda não tenha sido analisado, podendo optar por receber alertas quando o software faz alterações ao seu computador.  

### <a name="to-set-up-alerts"></a>Para configurar alertas  

1.  Clique em **Definições**e, em seguida, clique em **Proteção em tempo real**.  

2.  Certifique-se de que a caixa de verificação **Ativar a proteção em tempo real (recomendado)** está selecionada.  

3.  Selecione as caixas de verificação junto às opções de proteção em tempo real que pretende executar e, em seguida, clique em **Guardar alterações**. Se lhe for pedida uma palavra-passe de administrador ou confirmação, escreva a palavra-passe ou confirme a ação.  

### <a name="see-also"></a>Consulte também  
 [Resolução de problemas de cliente do Windows Defender ou Endpoint Protection](troubleshoot-endpoint-client.md)   

 [Ajuda do cliente do Endpoint Protection](endpoint-protection-client-help.md)

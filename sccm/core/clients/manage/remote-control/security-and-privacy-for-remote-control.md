---
title: "Privacidade de segurança do controlo remoto"
titleSuffix: Configuration Manager
description: "Obter informações de segurança e privacidade para controlo remoto no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 272ee86b-d3d9-4fd9-b5c4-73e490e1a1e4
caps.latest.revision: "6"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 4923aee0e55f42f679c6f17ea0fd760c1909f9ef
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="security-and-privacy-for-remote-control-in-system-center-configuration-manager"></a>Segurança e privacidade para controlo remoto no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém informações de privacidade para controlo remoto no System Center 2012 Configuration Manager e de segurança.  

##  <a name="BKMK_Security_HardwareInventory"></a> Melhores práticas de segurança para controlo remoto  
 Utilize as melhores práticas de segurança seguintes quando gerir computadores cliente utilizando o controlo remoto.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Quando ligar a um computador remoto, não continue se for utilizada a autenticação NTLM em vez de Kerberos.|Quando o Configuration Manager detetar que a sessão de controlo remoto foi autenticada utilizando NTLM em vez de Kerberos, verá uma linha de comandos que avisa-o de que não é possível verificar a identidade do computador remoto. Não continue a sessão de controlo remoto. A autenticação NTLM é um protocolo de autenticação mais fraco que Kerberos e é vulnerável a repetição e representação.|  
|Não ative a partilha da Área de Transferência no visualizador de controlo remoto.|A Área de Transferência suporta objetos, como ficheiros executáveis e texto, e pode ser utilizada pelo utilizador no computador anfitrião durante a sessão de controlo remoto para executar um programa no computador de origem.|  
|Não introduza palavras-passe para contas com privilégios quando administrar remotamente um computador.|É possível que software que observe a introdução por teclado capture a palavra-passe. Em alternativa, se o programa que está a ser executado no computador cliente não for o programa que o utilizador do controlo remoto assume, o programa pode estar a capturar a palavra-passe. Quando forem necessárias contas e palavras-passe, o utilizador final deve introduzi-las.|  
|Bloqueie o teclado e o rato durante uma sessão de controlo remoto.|Se o Configuration Manager detetar que a ligação de controlo remoto foi terminada, o Configuration Manager bloqueia automaticamente o teclado e rato para que um utilizador não pode assumir o controlo da sessão de controlo remoto aberta. No entanto, esta deteção pode não ocorrer imediatamente e não ocorre se o serviço de controlo remoto for terminado.<br /><br /> Selecione a ação **Bloquear Teclado e Rato Remotos** na janela **Controlo Remoto do ConfigMgr** .|  
|Não permita aos utilizadores configurar as definições de controlo remoto no Centro de Software.|Não ative a definição de cliente **Os utilizadores podem alterar as definições de notificação ou da política no Centro de Software** para ajudar a impedir que os utilizadores sejam espiados.<br /><br /> Esta definição é para o computador, não para o utilizador com sessão iniciada.|  
|Ative o perfil da Firewall do Windows **Domínio** .|Ative a definição de cliente **Ativar controlo remoto nos perfis de exceção de Firewall de clientes** e, em seguida, selecione a Firewall do Windows **Domínio** para computadores de intranet.|  
|Se terminar a sessão durante uma sessão de controlo remoto e iniciar sessão como um utilizador diferente, certifique-se de que termina a sessão antes de desligar a sessão de controlo remoto.|Se não terminar a sessão neste cenário, a sessão permanece aberta.|  
|Não conceda direitos de administrador local aos utilizadores.|Quando conceder direitos de administrador local aos utilizadores, estes poderão assumir o controlo da sua sessão de controlo remoto ou comprometer as suas credenciais.|  
|Utilize a política de grupo ou do Configuration Manager para configurar definições da assistência remota, mas não ambos.|Pode utilizar o Configuration Manager e a política de grupo para efetuar alterações de configuração para as definições de assistência remota. Quando a Política de Grupo é atualizada no cliente, por predefinição, otimiza o processo ao alterar apenas as políticas que foram alteradas no servidor. Gestor de configuração altera as definições na política de segurança local, não podendo ser substituídas, a menos que a atualização da política de grupo é forçada.<br /><br /> A definição da política em ambos os locais pode originar resultados inconsistentes. Escolha um dos seguintes métodos para configurar as definições de Assistência Remota.|  
|Ative a definição de cliente **Solicitar ao utilizador permissão do Controlo Remoto**.|Embora existam formas desta definição de cliente solicitar a um utilizador para confirmar uma sessão de controlo remoto, ative esta definição para reduzir a probabilidade de os utilizadores serem espiados enquanto estão a trabalhar em tarefas confidenciais.<br /><br /> Além disso, informe os utilizadores para verificarem o nome da conta apresentado durante a sessão de controlo remoto e desligarem a sessão se suspeitarem que a conta não está autorizada.|  
|Limite a lista de Visualizadores Permitidos.|Não são necessários direitos de administrador local para um utilizador poder utilizar o controlo remoto.|  

### <a name="security-issues-for-remote-control"></a>Problemas de segurança do controlo remoto  
 A gestão de computadores cliente utilizando o controlo remoto tem os seguintes problemas de segurança:  

-   Não considere as mensagens de auditoria do controlo remoto fiáveis.  

     Se iniciar uma sessão de controlo remoto e, em seguida, iniciar sessão utilizando credenciais alternativas, a conta original envia as mensagens de auditoria e não a conta que utilizou as credenciais alternativas.  

     Mensagens de auditoria não são enviadas se copiar os ficheiros binários para controlo remoto em vez de instalar a consola do Configuration Manager e, em seguida, execute o controlo remoto na linha de comandos.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Informações de privacidade do controlo remoto  
 Controlo remoto permite-lhe ver as sessões ativas nos computadores de cliente do Configuration Manager e potencialmente ver todas as informações armazenadas nesses computadores. Por predefinição, o controlo remoto não está ativado.  

 Embora possa configurar o controlo remoto para fornecer avisos evidentes e obter consentimento de um utilizador antes do início da sessão de controlo remoto, também pode monitorizar os utilizadores sem a sua permissão ou conhecimento. Pode configurar o nível de acesso Ver Apenas para que nada possa ser alterado no controlo remoto, ou Controlo Total. A conta do administrador de ligação é apresentada na sessão de controlo remoto, para ajudar os utilizadores a identificar quem está a ligar ao respetivo computador.  

 Por predefinição, o Configuration Manager concede o local de administradores permissões de controlo remoto do grupo.  

 Antes de configurar o controlo remoto, considere os requisitos de privacidade.  

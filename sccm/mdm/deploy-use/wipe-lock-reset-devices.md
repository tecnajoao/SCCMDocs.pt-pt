---
title: "Proteger dados através de eliminação remota, bloqueio ou código de acesso reposto utilizando o System Center Configuration Manager | Documentos do Microsoft"
description: "Proteger os dados de dispositivo com a eliminação completa, a eliminação seletiva, bloqueio remoto ou código de acesso reposto utilizando o System Center Configuration Manager."
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
caps.latest.revision: 18
caps.handback.revision: 0
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dda2f4c01078fbbd174cbcb30357554c24f6abeb
ms.openlocfilehash: 351fdc6328dd0859d60e00b128963df738e69f81
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="protect-data-with-remote-wipe-lock-or-passcode-reset-by-using-system-center-configuration-manager"></a>Proteger dados através de eliminação remota, bloqueio ou código de acesso reposto utilizando o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager oferece eliminação seletiva, eliminação completa, bloqueio remoto e funcionalidades de reposição do código de acesso. Os dispositivos móveis podem armazenar dados empresariais confidenciais e fornecer acesso a muitos recursos da empresa. Para ajudar a proteger os dispositivos, pode emitir:  

- Uma eliminação completa para restaurar o dispositivo para as respetivas definições de fábrica.  

- Uma eliminação seletiva para remover apenas os dados da empresa.  

- Um bloqueio remoto para ajudar a proteger o dispositivo em caso de perda.  

- Uma reposição do código de acesso do dispositivo.  

## <a name="full-wipe"></a>Eliminação completa  
Pode emitir um comando de eliminação para um dispositivo quando precisa de proteger um dispositivo perdido ou quando extingue um dispositivo de utilização ativa.  

Emita uma **eliminação completa** para um dispositivo para restaurar o mesmo para as respetivas predefinições de fábrica. Esta ação remove todos os dados e definições da empresa e do utilizador. Pode efetuar uma eliminação completa em dispositivos Windows Phone, iOS, Android e Windows 10.  

> [!NOTE]
> Apagar dispositivos Windows 10 em versões anteriores ao versão 1511 com menos de 4 GB de RAM pode deixar o dispositivo não responde. [Saiba mais](https://technet.microsoft.com/library/mt592024.aspx#full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram).

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Para iniciar uma eliminação remota de dados a partir da consola do Configuration Manager  

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade** e escolha **dispositivos**. Em alternativa, pode escolher **coleções de dispositivos** e selecione uma coleção.  

2. Selecione o dispositivo que pretende extinguir/eliminar.  

3. Escolher **ações de dispositivo remotas** no **grupo de dispositivos**e, em seguida, escolha **extinguir/apagar**.  

## <a name="selective-wipe"></a>Eliminação seletiva  
Emita uma **eliminação seletiva** para um dispositivo para remover apenas os dados da empresa. A tabela seguinte descreve, por plataforma, que dados são removidos e o efeito nos dados que permanecem no dispositivo após uma eliminação seletiva.  

**iOS**  

|Conteúdo removido quando estiver extinguir um dispositivo|iOS|  
|--------------------------------------------|---------|  
|Aplicações da empresa e dados associados instalados utilizando o Configuration Manager e o Intune|As aplicações são desinstaladas. Os dados da aplicação da empresa são removidos.|  
|Perfis de VPN e de Wi-Fi|Removidos.|  
|Certificados|Removidos e revogados.|  
|Definições|Removido, exceto para: **Permitir chamadas em roaming**, **permitir roaming de dados**, e **permitir sincronização automática em roaming**.|  
|Agente de gestão|O perfil de gestão é removido.|  
|Perfis de e-mail|Para perfis de e-mail configuradas pelo Intune, a conta de correio eletrónico e correio eletrónico são removidos.|  

**Android e o Android Samsung KNOX Standard**  

|Conteúdo removido quando estiver extinguir um dispositivo|Android|Samsung KNOX Standard|  
|--------------------------------------------|-------------|------------------|  
|Aplicações da empresa e dados associados instalados utilizando o Configuration Manager e o Intune|As aplicações e os dados permanecem instalados.|As aplicações são desinstaladas.|  
|Perfis de VPN e de Wi-Fi|Removidos.|Removidos.|  
|Certificados|Revogados.|Revogados.|  
|Definições|Requisitos são removidos.|Requisitos são removidos.|  
|Agente de gestão|O privilégio de Administrador de Dispositivos é revogado.|O privilégio de Administrador de Dispositivos é revogado.|  
|Perfis de e-mail|Não aplicável.|Para perfis de e-mail configuradas pelo Intune, a conta de correio eletrónico e correio eletrónico são removidos.|  

**Android para trabalhar**

Efetuar uma eliminação seletiva num Android para o dispositivo de trabalho remove o perfil de trabalho juntamente com todos os dados, aplicações e definições no perfil de trabalho nesse dispositivo. Ter extinguido o dispositivo da gestão com o Configuration Manager e do Intune. Eliminação completa não é suportada para Android para trabalhar.

 **Windows 10, Windows 8.1, Windows RT 8.1 e Windows RT**  

|Conteúdo removido quando estiver extinguir um dispositivo|Windows 10, Windows 8.1 e Windows RT 8.1|  
|---------------------------------|-------------|
|Aplicações da empresa e dados associados instalados utilizando o Configuration Manager e o Intune|As aplicações são desinstaladas e as chaves de sideload são removidas. As aplicações que utilizam a eliminação seletiva do Windows terão a chave de encriptação revogada e dados deixarão de estar acessíveis.|  
|Perfis de VPN e de Wi-Fi|Removidos.|  
|Certificados|Removidos e revogados.|  
|Definições|Requisitos são removidos.|
|Agente de gestão|Não aplicável. Agente de gestão está incorporado no.|  
|Perfis de e-mail|Correio eletrónico que tenha o EFS ativado for removido, o que inclui a aplicação correio para Windows e-mail e anexos.|  

 **Windows 10 Mobile, Windows Phone 8.0 e Windows Phone 8.1**

|Conteúdo removido quando estiver extinguir um dispositivo|Windows 10 Mobile, Windows Phone 8 e Windows Phone 8.1|  
|-|-|
|Aplicações da empresa e dados associados instalados utilizando o Configuration Manager e o Intune|As aplicações são desinstaladas. Os dados da aplicação da empresa são removidos.|  
|Perfis de VPN e de Wi-Fi|Removido no Windows 10 Mobile e Windows Phone 8.1.|  
|Certificados|Removido no Windows Phone 8.1.|  
|Agente de gestão|Não aplicável. Agente de gestão está incorporado no.|  
|Perfis de e-mail|Removido (exceto o Windows Phone 8.0).|  

As seguintes definições são também removidas a partir de dispositivos Windows 10 Mobile e Windows Phone 8.1:  

- **Exigir uma palavra-passe para desbloquear os dispositivos móveis**  
- **Permitir palavras-passe simples**  
- **Comprimento mínimo da palavra-passe**  
- **Tipo de palavra-passe obrigatório**
- **Expiração de palavra-passe (dias)**  
- **Memorizar histórico de palavra-passe**  
- **Número de falhas de início de sessão consecutivas a permitir antes do dispositivo ser apagado**  
- **Minutos de inatividade antes da palavra-passe é exigida**  
- **Tipo de palavra-passe obrigatório – número mínimo de conjuntos de carateres**  
- **Permitir câmara**
- **Encriptação obrigatória no dispositivo móvel**  
- **Permitir armazenamento amovível**  
- **Permitir browser**  
- **Permitir loja de aplicações**  
- **Permitir captura de ecrã**  
- **Permitir geolocalização**  
- **Permitir conta Microsoft**  
- **Permitir copiar e colar**  
- **Permitir partilha de Wi-Fi**  
- **Permitir ligação automática a hotspots Wi-Fi**  
- **Permitir relatórios de hotspots Wi-Fi**  
- **Permitir a reposição de fábrica**
- **Permitir Bluetooth**  
- **Permitir NFC**
- **Permitir Wi-Fi**

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Para iniciar uma eliminação remota de dados a partir da consola do Configuration Manager  

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade** e escolha **dispositivos**. Em alternativa, pode escolher **coleções de dispositivos** e selecione uma coleção.  

2. Selecione o dispositivo que pretende extinguir/eliminar.  

3. Escolher **ações de dispositivo remotas** no **grupo de dispositivos**e, em seguida, escolha **extinguir/apagar**.  

## <a name="wiping-efs-enabled-content"></a>Apagar conteúdo com EFS ATIVO.  
Windows 8.1 e Windows RT 8.1 suportam a eliminação seletiva de conteúdo encriptado de sistema de encriptação ficheiro EFS. As seguintes informações aplicam-se a uma eliminação seletiva de conteúdo com o EFS ativado:  

- Apenas as aplicações e dados que estão protegidos pelo EFS através do mesmo domínio de Internet que a conta do Intune são apagados seletivamente. Para mais informações, consulte o artigo [Eliminação Seletiva do Windows para a Gestão de Dados de Dispositivos](http://technet.microsoft.com/library/dn486874.aspx).  

- Se forem efetuadas quaisquer alterações ao domínio associado ao EFS, as alterações podem demorar até 48 horas antes das aplicações e dados que utilizam o novo domínio poderem ser apagados.  

- Cada domínio registado com o Intune é o domínio que será apagado.  

Os dados e aplicações que tenha o EFS seletivo atualmente apagar suporta são:  

- Aplicação correio para Windows.  

- Pastas de trabalho.

- Ficheiros e pastas encriptados pelo EFS. Para mais informações, consulte o artigo [Melhores práticas para o Sistema de Encriptação de Ficheiros](http://support.microsoft.com/kb/223316).  

### <a name="best-practices-for-selective-wipe"></a>Melhores práticas para limpeza seletiva  

- Para um apagar e-mails com êxito, configure perfis de e-mail para dispositivos Windows Phone 8.1 e iOS.  

- Para um apagar aplicações com êxito, certifique-se de que as aplicações são distribuídas através da gestão de aplicações de dispositivos móveis.  

- No iOS, configure a definição **permitir cópia de segurança para iCloud** para **não permitir** para que os utilizadores não possam restaurar conteúdo com o iCloud.  

- Se uma conta tiver sido desativada, em seguida, após um ano, Intune será extinguir a conta e será efetuada uma eliminação seletiva.  

##  <a name="passcode-reset"></a>Repor código de acesso  
Se um utilizador se esquecer do respetivo código de acesso, pode ajudá-lo ao remover o código de acesso de um dispositivo ou ao aplicar um novo código de acesso temporário num dispositivo. A tabela seguinte lista como a reposição de código de acesso funciona em diferentes plataformas móveis.  

|Plataforma|Repor código de acesso|  
|--------------|--------------------|  
|iOS|Suportado para a eliminação do código de acesso de um dispositivo. Não cria um novo código de acesso temporário.|
|macOS| Não suportada.|
|Android|Suportada, e é criado um código de acesso temporário.|
|Android for Work | Não suportada.|
|PCs Windows 10|Não suportada.|  
|Windows 10 móveis|Suportada, excluir o Azure AD associados a dispositivos.|
|Windows Phone 8.1|Suportado.|  
|Windows RT 8.1 |Não suportada.|  
|PCs Windows 8.1 |Não suportada.|  

#### <a name="to-reset-the-passcode-on-a-mobile-device-remotely-in-configuration-manager"></a>Para repor o código de acesso remotamente num dispositivo móvel no Configuration Manager  

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade** e escolha **dispositivos**. Em alternativa, pode escolher **coleções de dispositivos** e selecione uma coleção.  

2. Selecione o dispositivo ou dispositivos em que pretende repor o código de acesso.  

3. Escolher **ações de dispositivo remotas** no **grupo de dispositivos**e, em seguida, escolha **reposição**.  

#### <a name="to-show-the-state-of-the-passcode-reset"></a>Para mostrar o estado da reposição do código de acesso  

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade** e escolha **dispositivos**. Em alternativa, pode escolher **coleções de dispositivos** e selecione uma coleção.  

2. Selecione o dispositivo ou dispositivos em que pretende mostrar o estado da reposição do código de acesso.  

3. Escolher **ações de dispositivo remotas** no **grupo de dispositivos**e, em seguida, escolha **Mostrar código de acesso estado**.  

## <a name="remote-lock"></a>Bloqueio remoto  
Se um utilizador perder o respetivo dispositivo, pode bloquear remotamente o dispositivo. A tabela seguinte indica como o bloqueio remoto funciona em diferentes plataformas móveis.  

|Plataforma|Bloqueio remoto|  
|--------------|-----------------|  
|iOS|Suportado.|  
|Android|Suportado.|  
|Windows 10|De momento, não é suportado.|  
|Windows Phone 8 e Windows Phone 8.1|Suportado.|  
|Windows RT 8.1 |Suportado se o utilizador atual do dispositivo for o mesmo utilizador que inscreveu o dispositivo.|  
|Windows 8,1|Suportado se o utilizador atual do dispositivo for o mesmo utilizador que inscreveu o dispositivo.|  

#### <a name="to-lock-a-mobile-device-remotely-through-the-configuration-manager-console"></a>Para bloquear um dispositivo móvel remotamente através da consola do Configuration Manager  

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade** e escolha **dispositivos**. Em alternativa, pode escolher **coleções de dispositivos** e selecione uma coleção.  

2. Selecione o dispositivo ou dispositivos a bloquear.  

3. Escolher **ações de dispositivo remotas** no **grupo de dispositivos**e, em seguida, escolha **bloqueio remoto**.  

#### <a name="to-show-the-state-of-the-remote-lock"></a>Para mostrar o estado do bloqueio remoto  

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade** e escolha **dispositivos**. Em alternativa, pode escolher **coleções de dispositivos** e selecione uma coleção.  

2. Selecione o dispositivo em que pretende mostrar o estado do bloqueio remoto.  

3. Escolher **ações de dispositivo remotas** no **grupo de dispositivos**e, em seguida, escolha **Mostrar estado do bloqueio remoto**.  

### <a name="see-also"></a>Consulte também  
[Windows Selective wipe eliminação dados para gestão de dispositivos](http://technet.microsoft.com/library/dn486874.aspx)   


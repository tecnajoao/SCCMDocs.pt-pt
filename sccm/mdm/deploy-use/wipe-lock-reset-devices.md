---
title: Proteger os dados com a reposição de eliminação, bloqueio ou código de acesso remoto
titleSuffix: Configuration Manager
description: Protege os dados de dispositivo com a eliminação completa, eliminação seletiva, bloqueio remoto ou utilizando o Gestor de configuração de reposição do código de acesso.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ebc2b995c763aa54e1d47ee38ab2d250554f5a29
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136029"
---
# <a name="protect-data-with-remote-wipe-lock-or-passcode-reset-by-using-configuration-manager"></a>Proteger dados através de eliminação remota, bloqueio ou utilizando o Gestor de configuração de reposição do código de acesso

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager fornece a eliminação seletiva, eliminação completa, bloqueio remoto e funcionalidades de reposição do código de acesso. Os dispositivos móveis podem armazenar dados empresariais confidenciais e fornecer acesso a muitos recursos da empresa. Para ajudar a proteger os dispositivos, pode emitir:  

- Uma eliminação completa para restaurar o dispositivo para as definições de fábrica  

- Uma eliminação seletiva para remover apenas os dados da empresa  

- Um bloqueio remoto para ajudar a proteger um dispositivo que poderão perder-se  

- Uma reposição do código de acesso do dispositivo  

> [!Important]  
> A partir de 14 de Agosto de 2018, gestão de dispositivos móveis híbrida é um [funcionalidade preterida](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para obter mais informações, consulte [o que é a MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="full-wipe"></a>Eliminação completa  

Pode emitir um comando de eliminação para um dispositivo quando precisa de proteger um dispositivo perdido ou quando extingue um dispositivo de utilização ativa.  

Emita uma **eliminação completa** para um dispositivo para restaurar o mesmo para as respetivas predefinições de fábrica. Esta ação remove todos os dados e definições da empresa e do utilizador. Pode fazer uma eliminação completa nos dispositivos Windows Phone, iOS, Android e Windows 10.  

> [!NOTE]
> Só pode efetuar uma eliminação completa nos dispositivos pertencentes à empresa.

> [!NOTE]
> Limpar dispositivos Windows 10 em versões anteriores à versão 1511 com menos de 4 GB de RAM pode deixar o dispositivo não responde. [Saiba mais](https://technet.microsoft.com/library/mt592024.aspx#full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram).

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Para iniciar uma eliminação remota de dados a partir da consola do Configuration Manager  

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade** e escolha **dispositivos**. Em alternativa, pode escolher **coleções de dispositivos** e selecionar uma coleção.  

2. Selecione o dispositivo que pretende extinguir/eliminar.  

3. Escolher **ações do dispositivo remoto** na **grupo de dispositivos**e, em seguida, escolha **extinguir/limpar**.  



## <a name="selective-wipe"></a>Eliminação seletiva  

Emita uma **eliminação seletiva** para um dispositivo para remover apenas os dados da empresa. A tabela seguinte descreve, por plataforma, que dados são removidos e o efeito nos dados que permanecem no dispositivo após uma eliminação seletiva.  

**iOS**  

|Conteúdo removido quando estiver a extinguir um dispositivo|iOS|  
|--------------------------------------------|---------|  
|Aplicações da empresa e dados associados instalados utilizando o Configuration Manager e o Intune|As aplicações são desinstaladas. Os dados da aplicação da empresa são removidos.|  
|Perfis de VPN e de Wi-Fi|Removidos.|  
|Certificados|Removidos e revogados.|  
|Definições|Removido, exceto para: **Permitir roaming de voz**, **permitir roaming de dados**, e **permitir sincronização automática em roaming**.|  
|Agente de gestão|O perfil de gestão é removido.|  
|Perfis de e-mail|Para perfis de e-mail configurados pelo Intune, a conta de e-mail e o e-mail são removidos.|  

**Android e Android Samsung KNOX Standard**  

|Conteúdo removido quando estiver a extinguir um dispositivo|Android|Samsung KNOX Standard|  
|--------------------------------------------|-------------|------------------|  
|Aplicações da empresa e dados associados instalados utilizando o Configuration Manager e o Intune|As aplicações e os dados permanecem instalados.|As aplicações são desinstaladas.|  
|Perfis de VPN e de Wi-Fi|Removidos.|Removidos.|  
|Certificados|Revogados.|Revogados.|  
|Definições|Requisitos são removidos.|Requisitos são removidos.|  
|Agente de gestão|O privilégio de Administrador de Dispositivos é revogado.|O privilégio de Administrador de Dispositivos é revogado.|  
|Perfis de e-mail|Não aplicável.|Para perfis de e-mail configurados pelo Intune, a conta de e-mail e o e-mail são removidos.|  

**Android for Work**

Fazer uma eliminação seletiva num dispositivo Android for Work remove o perfil de trabalho, juntamente com todos os dados, aplicações e definições no perfil de trabalho nesse dispositivo. Esta ação extingue o dispositivo da gestão com o Configuration Manager e o Intune. Eliminação completa não é suportada para Android for Work.

 **Windows 10, Windows 8.1, Windows RT 8.1 e Windows RT**  

|Conteúdo removido quando estiver a extinguir um dispositivo|Windows 10, Windows 8.1 e Windows RT 8.1|  
|---------------------------------|-------------|
|Aplicações da empresa e dados associados instalados utilizando o Configuration Manager e o Intune|As aplicações são desinstaladas e as chaves de sideload são removidas. Aplicações que utilizam a eliminação seletiva do Windows terão a chave de encriptação revogada e dados já não estará acessíveis.|  
|Perfis de VPN e de Wi-Fi|Removidos.|  
|Certificados|Removidos e revogados.|  
|Definições|Requisitos são removidos.|
|Agente de gestão|Não aplicável. Agente de gestão baseia-se.|  
|Perfis de e-mail|Mensagem de e-mail que tenha o EFS ativado é removida, que inclui a aplicação de correio para e-mail do Windows e os anexos.|  

 **Windows 10 Mobile, Windows Phone 8.0 e Windows Phone 8.1**

|Conteúdo removido quando estiver a extinguir um dispositivo|Windows 10 Mobile, Windows Phone 8 e Windows Phone 8.1|  
|-|-|
|Aplicações da empresa e dados associados instalados utilizando o Configuration Manager e o Intune|As aplicações são desinstaladas. Os dados da aplicação da empresa são removidos.|  
|Perfis de VPN e de Wi-Fi|Removido para Windows 10 Mobile e Windows Phone 8.1.|  
|Certificados|Removido no Windows Phone 8.1.|  
|Agente de gestão|Não aplicável. Agente de gestão baseia-se.|  
|Perfis de e-mail|Removido (exceto o Windows Phone 8.0).|  

As seguintes definições também são removidas dos dispositivos Windows 10 Mobile e Windows Phone 8.1:  

- **Exigir uma palavra-passe para desbloquear dispositivos móveis**  
- **Permitir palavras-passe simples**  
- **Comprimento mínimo da palavra-passe**  
- **Tipo de palavra-passe necessária**
- **Expiração de palavra-passe (dias)**  
- **Memorizar histórico de palavras-passe**  
- **Número de falhas de início de sessão consecutivas a permitir antes do dispositivo ser apagado**  
- **Minutos de inatividade antes da palavra-passe é necessária**  
- **Tipo de palavra-passe obrigatório – número mínimo de conjuntos de carateres**  
- **Permitir câmara**
- **Exigir encriptação no dispositivo móvel**  
- **Permitir armazenamento amovível**  
- **Permitir browser**  
- **Permitir loja de aplicações**  
- **Permitir captura de ecrã**  
- **Permitir geolocalização**  
- **Permitir conta Microsoft**  
- **Permitir copiar e colar**  
- **Permitir tethering Wi-Fi**  
- **Permitir ligação automática a hotspots Wi-Fi**  
- **Permitir relatórios de hotspots de Wi-Fi**  
- **Permitir reposição de fábrica**
- **Permitir Bluetooth**  
- **Permitir NFC**
- **Permitir Wi-Fi**

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Para iniciar uma eliminação remota de dados a partir da consola do Configuration Manager  

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade** e escolha **dispositivos**. Em alternativa, pode escolher **coleções de dispositivos** e selecionar uma coleção.  

2. Selecione o dispositivo que pretende extinguir/eliminar.  

3. Escolher **ações do dispositivo remoto** na **grupo de dispositivos**e, em seguida, escolha **extinguir/limpar**.  



## <a name="wiping-efs-enabled-content"></a>Eliminar conteúdo com o EFS ativado  

Windows 8.1 e Windows RT 8.1 suportam a eliminação seletiva de conteúdo encriptado com EFS do sistema de arquivos com criptografia. As seguintes informações aplicam-se a uma eliminação seletiva de conteúdo com o EFS ativado:  

- Apenas as aplicações e dados que estão protegidos pelo EFS através do mesmo domínio de Internet que a conta do Intune são apagados seletivamente. Para mais informações, consulte o artigo [Eliminação Seletiva do Windows para a Gestão de Dados de Dispositivos](http://technet.microsoft.com/library/dn486874.aspx).  

- Se todas as alterações são feitas ao domínio associado ao EFS, as alterações podem demorar até 48 horas antes das aplicações e dados que utilizam o novo domínio poderem ser apagados seletivamente.  

- Cada domínio registado com o Intune é o domínio que será apagado.  

Os dados e aplicações que o EFS seletivas apagar atualmente suporta são:  

- Aplicação de correio para Windows.  

- Pastas de trabalho.

- Ficheiros e pastas encriptados pelo EFS. Para mais informações, consulte o artigo [Melhores práticas para o Sistema de Encriptação de Ficheiros](http://support.microsoft.com/kb/223316).  


### <a name="best-practices-for-selective-wipe"></a>Melhores práticas para limpeza seletiva  

- Para uma eliminação com êxito de e-mail, configure perfis de e-mail para iOS e dispositivos Windows Phone 8.1.  

- Para um apagar aplicações com êxito, certifique-se de que as aplicações são distribuídas através da gestão de aplicações de dispositivos móveis.  

- Para iOS, configure a definição **permitir cópia de segurança para iCloud** ao **não permitir** para que os usuários não possam restaurar conteúdo com o iCloud.  

- Se uma conta tiver sido desativada, em seguida, após um ano, Intune irão extinguir a conta e uma eliminação seletiva será feita.  



##  <a name="passcode-reset"></a>Repor código de acesso  

Se um utilizador se esquecer do respetivo código de acesso, pode ajudá-lo ao remover o código de acesso de um dispositivo ou ao aplicar um novo código de acesso temporário num dispositivo. A tabela seguinte lista como a reposição de código de acesso funciona em diferentes plataformas móveis.  

| Plataforma                              | Repor código de acesso                                                                               |
|---------------------------------------|----------------------------------------------------------------------------------------------|
| iOS                                   | Suportado para a eliminação do código de acesso de um dispositivo. Não cria um novo código de acesso temporário. |
| macOS                                 | Não suportada.                                                                               |
| Android                               | Suportado em versões anteriores ao Android 7.0. Cria um código de acesso temporário.                |
| Android for Work                      | Não suportada.                                                                               |
| PCs com Windows 10                        | Não suportada.                                                                               |
| Windows 10 mobile                     | Suportado, excluir o Azure AD associado a dispositivos.  |
| Windows Phone 8 e Windows Phone 8.1 | Suportado.                                                                                   |
| Windows RT 8.1                        | Não suportada.                                                                               |
| PCs Windows 8.1                       | Não suportada.                                                                               |

> [!Note]    
> Tem de efetuar a ação de reposição do código de acesso do site de nível superior no seu ambiente. Por exemplo, se utilizar um site de administração central, só pode efetuar a ação do site em questão. Se estiver a utilizar um site primário autónomo, só pode efetuar a ação do site em questão.

#### <a name="to-reset-the-passcode-on-a-mobile-device-remotely-in-configuration-manager"></a>Para repor o código de acesso remotamente num dispositivo móvel no Configuration Manager  

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade** e escolha **dispositivos**. Em alternativa, pode escolher **coleções de dispositivos** e selecionar uma coleção.  

2. Selecione o dispositivo ou dispositivos em que pretende repor o código de acesso.  

3. Escolher **ações do dispositivo remoto** na **grupo de dispositivos**e, em seguida, escolha **repor código de acesso**.  

#### <a name="to-show-the-state-of-the-passcode-reset"></a>Para mostrar o estado da reposição do código de acesso  

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade** e escolha **dispositivos**. Em alternativa, pode escolher **coleções de dispositivos** e selecionar uma coleção.  

2. Selecione o dispositivo ou dispositivos em que pretende mostrar o estado da reposição do código de acesso.  

3. Escolher **ações do dispositivo remoto** na **grupo de dispositivos**e, em seguida, escolha **Mostrar estado do código de acesso**.  



## <a name="remote-lock"></a>Bloqueio remoto  

Se um utilizador perder o dispositivo, pode bloquear o dispositivo remotamente. A tabela seguinte indica como o bloqueio remoto funciona em diferentes plataformas móveis.  

|Plataforma|Bloqueio remoto|  
|--------------|-----------------|  
|iOS|Suportado.|  
|Android|Suportado.|  
|Windows 10|De momento, não é suportado.|  
|Windows Phone 8 e Windows Phone 8.1|Suportado.|  
|Windows RT 8.1 |Suportado se o utilizador atual do dispositivo for o mesmo utilizador que inscreveu o dispositivo.|  
|Windows 8,1|Suportado se o utilizador atual do dispositivo for o mesmo utilizador que inscreveu o dispositivo.|  

> [!Note]    
> Tem de efetuar a ação bloqueio remoto do site de nível superior no seu ambiente. Por exemplo, se utilizar um site de administração central, só pode efetuar a ação do site em questão. Se estiver a utilizar um site primário autónomo, só pode efetuar a ação do site em questão.

#### <a name="to-lock-a-mobile-device-remotely-through-the-configuration-manager-console"></a>Para bloquear um dispositivo móvel remotamente através da consola do Configuration Manager  

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade** e escolha **dispositivos**. Em alternativa, pode escolher **coleções de dispositivos** e selecionar uma coleção.  

2. Selecione o dispositivo ou dispositivos a bloquear.  

3. Escolher **ações do dispositivo remoto** na **grupo de dispositivos**e, em seguida, escolha **bloqueio remoto**.  

#### <a name="to-show-the-state-of-the-remote-lock"></a>Para mostrar o estado do bloqueio remoto  

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade** e escolha **dispositivos**. Em alternativa, pode escolher **coleções de dispositivos** e selecionar uma coleção.  

2. Selecione o dispositivo em que pretende mostrar o estado do bloqueio remoto.  

3. Escolher **ações do dispositivo remoto** na **grupo de dispositivos**e, em seguida, escolha **Mostrar estado do bloqueio remoto**.  



## <a name="see-also"></a>Consulte também  

[De eliminação Seletivo do Windows para gestão de dados do dispositivo](http://technet.microsoft.com/library/dn486874.aspx)   

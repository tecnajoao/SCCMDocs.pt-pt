---
title: "Criar itens de configuração para o cliente gerido Windows 10 - Configuration Manager | Microsoft Docs"
description: "Utilize o item de configuração do System Center Configuration Manager Windows 10 para gerir as definições para computadores Windows 10 que são geridos pelo cliente do Configuration Manager."
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
caps.latest.revision: "17"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: be1a88341b08c454537279b27a27ce4fb90998de
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/15/2017
---
# <a name="how-to-create-configuration-items-for-windows-10-devices-managed-with-the-system-center-configuration-manager-client"></a>Como criar itens de configuração para dispositivos Windows 10 geridos com o cliente do System Center Configuration Manager
Utilizar o System Center Configuration Manager **Windows 10** item de configuração para gerir as definições para computadores Windows 10 que são geridos pelo cliente do Configuration Manager.  
  
> [!IMPORTANT]  
>  Nesta versão, se tiver criado uma **palavra-passe** definição como parte de um item de configuração do tipo **Windows 10** (para um dispositivo gerido com o cliente do Configuration Manager), em seguida, se a definição já não existe ou não foi configurada no dispositivo Windows 10, será incorretamente avaliada como compatível.  
>   
>  Como solução, quando cria uma definição para estes dispositivos, certifique-se de que a opção **Remediar definições incompatíveis** está selecionada nas páginas de definições do assistente estiver selecionada nas páginas de definições do Assistente de Criação de Item de Configuração. Além disso, ao implementar uma linha de base da configuração que contenha um item de configuração do Windows 10 que contenha definições de palavra-passe, selecione **Remediar regras incompatíveis quando suportado** na caixa de diálogo Implementar Linhas de Base de Configuração. Ao utilizar esta solução, a definição será monitorizada e remediada, caso seja considerada não compatível. Após a remediação, a definição será corretamente comunicada como **Compatível** (a menos que seja encontrado um problema, caso esse em que irá comunicar **Erro**).  
  
### <a name="to-create-a-windows-10-configuration-item"></a>Para criar um item de configuração do Windows 10  
  
1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  
  
2.  Na área de trabalho **Ativos e Conformidade** , expanda **Definições de Conformidade**e, em seguida, clique em **Itens de Configuração**.  
  
3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Item de Configuração**.  
  
4.  Na página **Geral** do **Assistente de Criação de Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  
  
5.  Em **Especifique o tipo de item de configuração que pretende criar**, selecione **Windows 10**.  
  
6.  Clique em **categorias** se criar e atribuir categorias para o ajudar a procurar e filtrar itens de configuração na consola do Configuration Manager.  
  
7.  Na página **Plataformas Suportadas** do assistente, selecione as plataformas específicas do Windows 10 que irão avaliar o item de configuração.  
  
8.  Na página **Definições do Dispositivo** do assistente, selecione o grupo de definições que pretende configurar. Consulte [Windows 10 configuration item settings reference](#BKMK_Ref) neste tópico para obter detalhes e, em seguida, clique em **Seguinte**.  
  
    > [!TIP]  
    >  Se a definição pretendida não estiver listada, selecione a caixa de verificação **Configurar definições adicionais que não estejam incluídas nos grupos de predefinições**.  
  
9. Em cada página de definições, configure as definições de que necessita e se pretende resolvê-las quando não forem compatíveis com dispositivos (quando esta opção é suportada).  
  
10. Para cada grupo de definições, também pode configurar a gravidade que será comunicada quando um item de configuração não for compatível:  
  
    -   **Nenhum** -dispositivos que não cumpram esta regra de compatibilidade não reportam uma gravidade de falha para relatórios do Configuration Manager.  
  
    -   **Informações** -dispositivos que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **informações** para relatórios do Configuration Manager.  
  
    -   **Aviso** -dispositivos que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **aviso** para relatórios do Configuration Manager.  
  
    -   **Crítico** -dispositivos que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **críticos** para relatórios do Configuration Manager.  
  
    -   **Crítico com evento** -dispositivos que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **críticos** para relatórios do Configuration Manager. Este nível de gravidade é também registado como um evento do Windows no registo de eventos da aplicação.  
  
11. Na página **Aplicabilidade da Plataforma** do assistente, reveja as definições que não são compatíveis com as plataformas suportadas que selecionou anteriormente. Pode voltar atrás e remover estas definições ou pode continuar.  
  
    > [!TIP]  
    >  As definições não suportadas não são avaliadas em termos de compatibilidade.  
  
12. Conclua o assistente.  
  
 Pode ver o novo item de configuração no nó **Itens de Configuração** da área de trabalho **Ativos e Compatibilidade** .  
  
##  <a name="windows-10-configuration-item-settings-reference"></a>Referência de definições de item de configuração do Windows 10  
  
### <a name="password"></a>Palavra-passe  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Exigir definições de palavra-passe em dispositivos**|Exigir uma palavra-passe em dispositivos suportados.|  
|**Comprimento mínimo de palavra-passe (carateres)**|O comprimento mínimo, em carateres, da palavra-passe.|  
|**Expiração da palavra-passe em dias**|O número de dias antes de a palavra-passe ter de ser alterada.|  
|**Número de palavras-passe memorizadas**|Impede a reutilização de palavras-passe anteriores.|  
|**Número de tentativas de início de sessão falhadas antes de um dispositivo ser apagado**|Apaga o dispositivo se o início de sessão falhar este número de vezes.|  
|**Tempo de inatividade antes do dispositivo está bloqueado**|Especifica o número de minutos durante o qual o dispositivo tem de ficar inativo antes de ser automaticamente bloqueado.|  
|**Complexidade de palavra-passe**|Escolher se pretende especificar um PIN como "1234" ou se tem de fornecer uma palavra-passe segura.|
|**Define o número de carateres complexos necessário na palavra-passe**|Se tiver selecionado um **forte** palavra-passe, utilize esta definição para configurar o número de conjuntos de carateres complexos necessários. Uma palavra-passe forte, este deve ser definido, pelo menos, **3** que significa letras e números são necessários. Selecione **4** se pretende impor uma palavra-passe além disso, tais como a requer carateres especiais **($ de %**.<br>(Apenas no Windows 10)  |
  
###  <a name="device"></a>Dispositivo  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Bluetooth**|Permite a utilização da funcionalidade Bluetooth no dispositivo.|  
  
### <a name="cloud"></a>Nuvem  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Sincronização de definições**|Permite a sincronização de definições entre dispositivos.|  
|**Sincronização de credenciais**|Permite a sincronização de credenciais entre dispositivos.|  
|**Sincronização de definições através de ligações com tráfego limitado**|Permitir a sincronização de definições quando a ligação à Internet tem tráfego limitado.|  
  
### <a name="roaming"></a>Roaming  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Roaming de dados**|Permitir roaming entre redes ao aceder a dados.|  
  
### <a name="encryption"></a>Encriptação  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Encriptação de ficheiros no dispositivo**|Requer que os ficheiros no dispositivo estejam encriptados.|  
  
### <a name="system-security"></a>Segurança do sistema  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Controlo de Conta de Utilizador**|Configura o modo de funcionamento do Controlo de Conta de Utilizador do Windows no dispositivo.<br />Por exemplo, pode desativá-lo ou definir o nível no qual o notifica.|  
|**Firewall da rede**|Ativa ou desativa a Firewall do Windows.|  
|**SmartScreen**|Ativar ou desativar o Windows SmartScreen.|  
|**Proteção contra vírus**|Requer que o software antivírus esteja instalado e configurado.|  
|**As assinaturas da proteção contra vírus estão atualizadas**|Requer que os ficheiros de assinatura para o software antivírus no dispositivo tem de ser atualizados.|  
  
### <a name="windows-information-protection-wip"></a>O Windows Information Protection (WIP)

Com o aumento dos dispositivos pertencentes a funcionários na empresa, existe também um risco crescente de fugas de dados acidentais através de aplicações e serviços, como o e-mail, redes sociais e a nuvem pública, que fogem ao controlo da empresa. Por exemplo, quando um empregado envia as imagens de engenharia mais recentes a partir da respetiva conta de e-mail pessoal, copia e cola informações sobre produtos num tweet ou guarda um relatório de vendas em curso no respetivo armazenamento de nuvem pública.

O Windows Information Protection (anteriormente proteção de dados da empresa) ajuda a proteger desta potencial fuga dados sem interferir com a experiência do empregado. WIP também ajuda a proteger aplicações da empresa e dados contra fugas de dados acidentais em dispositivos pertencentes à empresa e dispositivos pessoais que os empregados a funcionar sem necessidade de alterações no seu ambiente ou outras aplicações.

 Itens de configuração de proteção de informações do Windows do Configuration Manager gerir a lista de aplicações protegidas pelo WIP, localizações de rede da empresa, nível de proteção e definições de encriptação.
  

Para obter informações sobre como configurar a proteção de informações do Windows com o Configuration Manager, consulte [proteger os dados de enterprise através de proteção de informações do Windows (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).
  
## <a name="see-also"></a>Consulte Também  
 [Itens de configuração para dispositivos geridos com o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md)

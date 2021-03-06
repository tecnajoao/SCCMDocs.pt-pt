---
title: Ajuda do cliente do Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba mais sobre funcionalidades e melhoramentos no Endpoint Protection que melhor ajudá-lo a proteger o computador de ameaças.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: fdcee455-22e3-451d-bcf3-e7b62792f04a
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55615761dfa18c0a6bfc4988c18a4327446f02ca
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124869"
---
# <a name="endpoint-protection-client-help"></a>Ajuda do cliente do Endpoint Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Esta versão do Windows Defender ou Endpoint Protection inclui as seguintes funcionalidades para ajudar a proteger o computador de ameaças:  

-   **Integração da Firewall do Windows.** A configuração do Endpoint Protection permite-lhe ativar ou desativar a Firewall do Windows.  
-   **Sistema de Inspeção de Rede.** Esta funcionalidade melhora a proteção em tempo real ao inspecionar o tráfego de rede para ajudar a bloquear de forma pró-ativa a exploração de vulnerabilidades conhecidas baseadas na rede.  
-   **Motor de proteção.** Proteção em tempo real localiza e impede o malware a instalação e execução no seu PC. O motor atualizado oferece deteção melhorada e capacidades de limpeza com melhor desempenho.  

O Windows Defender é fornecido como parte do sistema operativo Windows 10.  Em versões anteriores do Windows, o administrador possa fornecer o Windows Defender ou Endpoint Protection utilizando software de gestão.

Também pode encontrar uma lista de [perguntas mais frequentes sobre o Windows Defender e Endpoint Protection](endpoint-protection-client-faq.md). Para obter ajuda a resolver problemas, consulte [cliente de resolução de problemas do Windows Defender ou o Endpoint Protection](troubleshoot-endpoint-client.md). Para obter uma lista dos novos recursos, consulte [o que há de novo cliente do Windows Defender](https://support.microsoft.com/help/29276/windows-10-whats-new-in-windows-defender).

## <a name="windows-firewall-integration"></a>Integração da Firewall do Windows  
 A Firewall do Windows pode ajudar a evitar que atacantes ou software malicioso obtenham acesso ao seu computador através da Internet ou de uma rede. Agora, quando instalar o Endpoint Protection, o assistente de instalação verifica se a Firewall do Windows está ativada. Se desativou a Firewall do Windows intencionalmente, pode desmarcar uma caixa de verificação para evitar ativá-la. Pode alterar as definições da Firewall do Windows a qualquer altura através das definições de Sistema e Segurança no Painel de Controlo.  

## <a name="network-inspection-system"></a>Sistema de Inspeção de Rede  
 Cada vez mais os atacantes levam a cabo ataques baseados na rede contra vulnerabilidades expostas, antes que os fabricantes de software consigam desenvolver e distribuir atualizações de segurança. Os estudos de vulnerabilidades demonstram que pode demorar um mês ou mais desde o momento em que é criado um relatório de ataque inicial até que uma atualização de segurança adequada seja desenvolvida, testada e lançada. Esta falha na proteção deixa muitos computadores vulneráveis a ataques e a exploração durante um período de tempo substancial. O Sistema de Inspeção de Rede funciona com proteção em tempo real para o ajudar a proteger contra ataques baseados na rede, reduzindo significativamente o período de tempo entre as divulgações de vulnerabilidade e a implementação de atualizações de semanas para algumas horas.  

## <a name="award-winning-protection-engine"></a>Motor de proteção premiado  
 Nos bastidores do Windows Defender ou Endpoint Protection é seu mecanismo de proteção premiado que é atualizado regularmente. O motor é suportado por uma equipa de investigadores de antimalware do Centro Microsoft de Proteção Contra Software Maligno, respondendo às mais recentes ameaças de software maligno 24 horas por dia.  

## <a name="windows-defender-settings"></a>Definições do Windows Defender
Definições do Windows Defender ativam as definições que ajudam a proteger o computador contra software malicioso. O administrador pode gerir algumas definições do Windows Defender para. Pode gerir outros a utilizar as definições do Windows Defender. Recomendamos que ative as definições do Windows Defender ajudar a proteger seu computador e seus dados.

Para ver as definições do Windows Defender, procure `Windows Defender` no seu PC. Open **o Windows Defender** e selecione **definições**. Definições do Windows Defender incluem:
- **Proteção em tempo real** - localize e impede o malware a instalação e execução no seu PC.
- **Proteção baseada na cloud** -Windows Defender envia informações à Microsoft sobre potenciais ameaças de segurança.
- **Submissão automática de** -permitir que o Windows Defender para enviar exemplos de ficheiros suspeitos para a Microsoft para ajudar a melhorar a deteção de software maligno.
- **Exclusões** -pode exlude de ficheiros específicos, pastas, extensões de ficheiro ou processos de verificação do Windows Defender.
- **Notificação de avançada** -permite que as notificações que o informam sobre o estado de funcionamento do seu PC. Até mesmo **desativar** irá receber as notificações críticas.
- **Windows Defender Offline** -pode executar o Windows Defender Offline para ajudar a localizar e remover software malicioso. Esta análise irá reiniciar o seu PC e irá demorar cerca de 15 minutos.

### <a name="see-also"></a>Consulte também  
 [Perguntas mais frequentes de cliente do Endpoint Protection](endpoint-protection-client-faq.md)   
 [Resolução de problemas do cliente do Windows Defender ou o Endpoint Protection](troubleshoot-endpoint-client.md)

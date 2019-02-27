---
title: Mensagens de estado no Configuration Manager
titleSuffix: Configuration Manager
description: Descrições de mensagens de estado nas versões suportadas do System Center Configuration Manager.
ms.date: 02/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ca97919e201db09e6b01ec968e73374f441c47cd
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/26/2019
ms.locfileid: "56839059"
---
# <a name="state-messages-in-system-center-configuration-manager"></a>Mensagens de estado no System Center Configuration Manager 

*Aplica-se a: Todas as versões do System Center Configuration Manager com suporte.*

Mensagens de estado de contenham informações concisas sobre condições no cliente do Configuration Manager 2012. O estado do sistema de mensagens é utilizado por componentes específicos do Configuration Manager, como atualizações de software, gestão de configuração pretendida e proteção de acesso à rede.

Clientes do Configuration Manager enviam mensagens de estado para o ponto de estado de contingência ou ponto de gestão de sistemas de site para reportar o estado atual de operações de cliente do Configuration Manager. Relatórios podem ser criados e utilizados para ver mensagens de estado enviadas por clientes do Configuration Manager.

Cada funcionalidade do Configuration Manager que utiliza as mensagens de estado é identificada pelo tipo de tópico da mensagem de estado. Os tipos de tópico de mensagens de estado listados na tabela seguinte podem ser usados para definir a funcionalidade do Configuration Manager que uma mensagem de estado se relaciona com.

> [!NOTE}
>
> Um valor de ID de mensagem de estado de zero (0) normalmente indica o tipo de tópico está num Estado desconhecido.

## <a name="300-statetopictypesumassignmentcompliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|       0   | Estado de conformidade desconhecido|
|   1   | Compatível | 
|   2   | Incompatível | 

## <a name="301-statetopictypesumassignmentenforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   0    | Estado de imposição desconhecido |
|   1    | A instalar as atualizações        | 
|   2    | Aguardar o reinício              | 
|   3    | A aguardar a conclusão da outra instalação         | 
|   4    | Update(2) instalada com êxito             | 
|   5    | Reinício de sistema pendente           | 
|   6    | Falha ao instalar as atualizações          | 
|   7    | A transferir as atualizações   | 
|   8    | Atualizações transferidas    | 
|   9    | Falha ao transferir as atualizações     | 
|   10   | A aguardar a janela de manutenção antes de instalar         | 
|   11   | A aguardar pela orquestração            | 

## <a name="302-statetopictypesumassignmentevaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|      
|0|        Estado de avaliação desconhecido|                 
|   1    |Avaliação ativada       |
|   2    |Avaliação com êxito      |
|   3    |Avaliação com falhas         |


## <a name="400-statetopictypesumcidetection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
| 0  | Estado de deteção desconhecido|
|   1|  Não é necessário      |
|   2|  Não é detetado          |
|   3|  Detetado      |

## <a name="401-statetopictypesumcicompliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|0| Estado de conformidade desconhecido|
|   1   |Compatível         |
|   2   |Incompatível         |
|   3   |Conflito detetado     |
|   4   |Erro             |
|   5   |Desconhecido           |
|   6   |Conformidade parcial   |
|   7   |Conformidade não configurada     |

## <a name="402-statetopictypesumcienforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
| 0 | Estado de imposição desconhecido|
|   1   |Imposição iniciada                   |
|   2   |Imposição a aguardar conteúdo               |
|   3   | A aguardar a conclusão da outra instalação         |
|   4   |A aguardar a janela de manutenção antes de instalar              |
|   5   |Reinício necessário antes de instalar            |
|   6   |Falha geral           |
|   7   |Instalação pendente              |
|   8   |Instalar a atualização                 |
|   9   |Reinício de sistema pendente        |
|   10  |Atualização instalada com êxito             |
|   11  |Falha ao instalar a atualização          |
|   12  |A transferir atualização        |
|   13  | Atualização transferida        |
|   14  |Falha ao transferir a atualização         |

## <a name="500-statetoptctypesumupdatedetection"></a>500 STATE_TOPTCTYPE_SUM_UPDATE_DETECTION

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|0 |Estado de deteção desconhecido|
|   1   | Não é necessária a atualização     |
|   2   | A atualização é necessária         |
|   3   | A atualização está instalada    |

## <a name="501-statetopictypesumupdatesourcescan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|0 |Estado de análise desconhecido|
|   1   | Análise está a aguardar conteúdo        |
|   2   | Análise está em execução            |
|   3   | Análise completa          |
|   4   | Análise tem uma repetição pendente      |
|   5   | Falha na análise        |
|   6   | Análise concluída com erros |

## <a name="700-statetopictyperesyncstatemsg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

    No State IDs.

## <a name="701-statetopictypesystemheartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

    No State IDs.

## <a name="702-statetopictypeckdupdate"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
    No State IDs.

## <a name="800-statetopictypeclientdeployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   100 |Implementação de cliente iniciada             |          
|   101 |A aguardar para download                  |          
|   102 |Implementação agendada                  |          
|   103 | A aguardar a janela antes de implementar |
|   104 |Implementação ignorada                |          
|   301 |Falha de implementação de cliente desconhecida |          
|   302 |Falha ao criar o serviço ccmsetup  |         
|   303 |Falha ao eliminar o serviço ccmsetup |          
|   304 |Não é possível instalar sobre o sistema operativo embedded com o arquivo com base em escrever filtro (FBWF) ativado na unidade do sistema |          
|   305 |Modo de segurança nativo não é válido no Windows 2000  |         
|   306 |Falha ao iniciar o processo de transferência do ccmsetup  |         
|   307 |Linha de comandos ccmsetup inválidos |        
|   308 |Falha ao transferir o ficheiro utilizando WinHTTP no endereço |        
|   309 |Falha ao transferir os ficheiros utilizando BITS no endereço |       
|   310 |Falha ao instalar a versão BITS |         
|   311 |Não é possível verificar que esse ficheiro de pré-requisitos está assinado pela MS  |          
|   312 |Falha ao copiar o ficheiro porque o disco está cheio |       
|   313 |Instalação de Client. msi falhou com o erro MSI |          
|   314 |Falha ao carregar o ficheiro de manifesto ccmsetup |          
|   315 |Falha ao obter um certificado de cliente  |         
|   316 |O ficheiro de pré-requisitos não está assinado pela MS |         
|   317 |É necessário reiniciar para continuar a instalação  |          
|   318 |Não é possível instalar o cliente no PG porque as versões do PG e do cliente não correspondem |        
|   319 |Sistema operativo ou o service pack não suportada  |        
|   320 |Implementação não suportada                  |          
|   321 |Bits em falta                      |          
|   322 |Pasta de origem não está disponível                  |          
|   323 |Appv não suportado                    |          
|   324 |Versão de Site incorreta                    |          
|   325 |Erro de correspondência do hash Prerequsite                 |          
|   326 |Anulação de registo do MDM falhou             |          
|   327 |Detetado o registo do MDM             |          
|   328 |Intune detetado                   |          
|   329 |Rede com tráfego limitado não permitida            |          
|   400 |Implementação de cliente concluída com êxito |  
|   401 |Implementação concluída com êxito o reinício é necessário          |          
|   402 |Implementação concluída com êxito a reinicialização foi concluída com êxito         |
|   500 |Atribuição de cliente iniciada|
|   601 |Falha de atribuição de cliente desconhecida|
|   602 |O seguinte código do site é inválido|
|   603 |Falha ao atribuir ao MP|
|   604 |Falha ao detetar o ponto de gestão predefinido|
|   605 |Falha ao transferir o certificado de assinatura do site|
|   606 |Falha ao automaticamente detetar o código do site|
|   607 |Atribuição de site falha; versão do cliente é superior à versão do site|
|   608 |Falha ao obter a versão do Site do Active Directory Domain Services e do SLP|
|   609 |Falha ao obter a versão do cliente|
|   700 |Atribuição de cliente com êxito|

## <a name="801-statetopictypedeviceclientdeployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

    No State IDs.

## <a name="810-statetopictypeclientcomanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   100 | Estado de inscrição         |
|   101 | Inscrição agendada          |
|   102 | Inscrição cancelada          |
|   105 | Inscrição iniciada            |
|   106 | Inscrição foi concluída com êxito, mas não está aprovisionada   
|   107 | Inscrição foi concluída com êxito e está aprovisionada   
|   108 | Inscrição sem utilizador ativo         |
|   110 | Falha ao         |


## <a name="820--statetopictypeclientwufb"></a>820  STATE_TOPICTYPE_CLIENT_WUFB

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   | Atualização do Windows para o estado do cliente de negócios| 

## <a name="900-statetopictypebranchdp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   | Espaço em disco      | 

## <a name="901-statetopictyperemotedpmonitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

    No State IDs.

## <a name="902-statetopictypepulldpmonitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

    No State IDs.

## <a name="903-statetopictypedpusage"></a>903 STATE_TOPICTYPE_DP_USAGE

    No State IDs.

## <a name="1000--statetopictypeclientframeworkcomm"></a>1000  STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1      | Cliente que está a comunicar corretamente com o ponto de gestão |
|   2      | Cliente não conseguiu comunicar com o ponto de gestão |

## <a name="1001-statetopictypeclientframeworklocal"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Cliente obteve com êxito o certificado do arquivo de certificados local       |
|   2   |Falha ao obter o certificado do arquivo de certificados local de cliente |

## <a name="1002-statetopictypedeviceclientframeworkcomm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

    No State IDs.

## <a name="1003-statetopictypedeviceclientframeworklocal"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

    No State IDs.

## <a name="1004-statetopictypedeviceclientframeworkcertificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

    No State IDs.

## <a name="1005-statetopictypedeviceclientwipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

    No State IDs.

## <a name="1006-statetopictypedeviceclientretire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

    No State IDs.

## <a name="1007-statetopictypedeviceclientwipeintune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

    No State IDs.

## <a name="1008-statetopictypedeviceclientretireintune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

    No State IDs.

## <a name="1009-statetopictypedeviceclientdevicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

    No State IDs.

## <a name="1010-statetopictypedeviceclientdevicelockintune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

    No State IDs.

## <a name="1011-statetopictypedeviceclientdevicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

    No State IDs.

## <a name="1012-statetopictypedeviceclientdevicepinresetintune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

    No State IDs.

## <a name="1013-statetopictypedeviceclientdevicepinresetonprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

    No State IDs.

## <a name="1014-statetopictypedeviceclientdevicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

    No State IDs.

## <a name="1015-statetopictypedeviceclientdevicealbypassintune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

    No State IDs.

## <a name="1100-statetopictypeclientframeworkmodereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Cliente não está pronto para o modo nativo  |
|   2   |Cliente pronto para o modo nativo       |

## <a name="1200-statetopictypeamtclientdatasynchronize"></a>1200 STATE_TOPICTYPE_AMT_CLIENT_DATA_SYNCHRONIZE

AMT é não suportada no System Center Configuration Manager 2012.

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   | Fabrico de dados        |

## <a name="1201-statetopictypeamtupdatemachineproperty"></a>1201 STATE_TOPICTYPE_AMT_UPDATE_MACHINE_PROPERTY

AMT é não suportada no System Center Configuration Manager 2012.

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Início do aprovisionamento          |
|   2   | Concluir aprovisionamento        |
|   3   |Anular o aprovisionamento completo         |
|   4   |Anular o aprovisionamento parcial          |
|   5   |Suprimir a limpeza automática          |
|   6   |Conclusão da manutenção   |
|   7   |Manutenção Kerb concluir      |
|   8   |Aprovisionar Miscdatafill   |


## <a name="1300-statetopictypeclienthealth"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |   Êxito|    
|   2   |   Não teve êxito |   

## <a name="1401-statetopictypestatereport"></a>1401 STATE_TOPICTYPE_STATE_REPORT

    No State IDs.

## <a name="1500-state-topictype-cal-track-ut"></a>1500 Topictype Cal Track Ut de estado

    No State IDs.

## <a name="1500-statetopictypecaltrackut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

    No State IDs.

## <a name="1502-statetopictypecaltrackmt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

    No State IDs.

## <a name="1503-statetopictypecaltrackml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

    No State IDs.   

## <a name="1600-statetopictypeuseraffinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Conjunto de afinidade de utilizador        |
|   2   |Useraffinity removido         |

## <a name="1700-statetopictypeappciscan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

    No State IDs.

## <a name="1701-statetopictypeappcicompliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

    No State IDs.

## <a name="1702-statetopictypeappcienforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1000    |Item de configuração foi concluída com êxito                      |
|   1001    |Item de configuração foi concluída com êxito já instalado            |
|   1002    |Item de configuração foi concluída com êxito de simulação                |
|   1003    |Estado do Item de configuração rápido efetuada com êxito                  |
|   2000    |Item de configuração em curso                    |
|   2001    |Item de configuração em curso a aguardar conteúdo            |
|   2002    |Item de configuração na instalação do curso                 |
|   2003    |Item de configuração no reinício de espera de progresso             |
|   2004    |Item de configuração em curso a aguardar a janela de manutenção         |
|   2005    |Item de configuração na agenda de espera de progresso               |
|   2006    |Item de configuração em curso a transferir conteúdo dependente     |
|   2007    |Item de configuração em curso a instalação de dependências        |
|   2008    |Item de configuração em curso com reinício pendente             |
|   2009    |Item de configuração no conteúdo de progresso transferido             |
|   2010    |Item de configuração em curso a atualização pendente             |
|   2011    |Restabelecimento de ligação do Item de configuração em curso a aguardar utilizador         |
|   2012    |Item de configuração em curso a aguardar a fim de sessão do utilizador            |
|   2013    |Item de configuração em curso a aguardar início de sessão do utilizador             |
|   2014    |Instalar o Item de configuração em curso a aguardar            |
|   2015    |Item de configuração em curso a aguardar entre tentativas              |
|   2016    |Item de configuração em curso a aguardar presmode               |
|   2017    |Item de configuração em curso a aguardar pela orquestração          |
|   2018    |Item de configuração em curso a aguardar rede            |
|   2019    |Item de configuração em curso a atualização VE pendente              |
|   2020    |Item de configuração em curso a atualização VE            |
|   3.000    |Requisitos de Item de configuração não foram cumpridos                       |
|   3001    |Anfitrião de requisitos não cumpridos de Item de configuração não aplicável           |
|   4000    |Item de configuração desconhecido                    |
|   5000    |Erro de Item de configuração                          |
|   5001    |A avaliação de erro do Item de configuração                   |
|   5002    |A instalar de erro do Item de configuração                   |
|   5003    |Erro de Item de configuração ao obter conteúdo               |
|   5004    |Erro de Item de configuração a instalar dependência            |
|   5005    |Erro de Item de configuração ao obter a dependência de conteúdo        |
|   5006    |Conflito de regras de erro de Item de configuração                   |
|   5007    |Erro de Item de configuração à espera de repetição                |
|   5008    |Desinstalar a substituição de erro do Item de configuração        |
|   5009    |Erro de Item de configuração baixar substituída               |
|   5010    |Erro de configuração do Item a atualizar VE                  |
|   5011    |Licença instalação de erro do Item de configuração               |
|   5012    |Erro de Item de configuração ao obter a permitir que todos os aplicativos confiáveis       |
|   5013    |Erro de Item de configuração não existem licenças disponíveis            |
|   5014    |Erro de Item de configuração não suportado do SO                 |
|   6000    |Lançamento de Item de configuração foi concluída com êxito                           |
|   6010    |Erro de início de Item de configuração                           |
|   6020    |Lançamento de Item de configuração desconhecido|

## <a name="1703-statetopictypeappciassignmentevaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

    No State IDs.

## <a name="1704-statetopictypeappcilaunch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

    No State IDs.

## <a name="1800-statetopictypeeventintrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

    No State IDs.

## <a name="1801-statetopictypeeventextrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

    No State IDs.

## <a name="1900-statetopictypeepaminfection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

    No State IDs.

## <a name="1901-state-topictype-ep-am-health"></a>O estado de funcionamento do Topictype Ep Am de estado de 1901

    No State IDs.

## <a name="1902-statetopictypeepmalware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

    No State IDs.

## <a name="1950-statetopictypeatphealthstatus"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

    No State IDs.

## <a name="2001-statetopictypeepclientdeployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Proteção de ponto final não gerida       |
|   2   |Proteção de ponto final a aguardar instalação  |
|   3   |Proteção de ponto final gerenciada         |
|   4   |Falhada de instalação do Endpoint Protection     |
|   5   |Reinício de proteção de ponto final pendente  |
|   6   |Proteção de ponto final não suportada       |
|   7   |Proteção de ponto final comanaged       |

## <a name="2002-statetopictypeepclientpolicyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   0   |Política aplicação estado do Endpoint Protection desconhecido        |
|   1   |Aplicação de política do Endpoint Protection foi concluída com êxito         |
|   2   |Aplicação de política de proteção de ponto final falhou        |

## <a name="2003-statetopictypeclientaction"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   0   |  Desconhecido            |
|   1   |  Active            |
|   2   |  Inativo          |

## <a name="2100-statetopictypewpclientdeployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   | Proxy de reativação não está instalado          |
|   2   | Proxy de reativação está a aguardar instalação       |
|   3   | Proxy de reativação está instalado          |
|   4   | Falha na instalação do Proxy de reativação       |
|   5   | Proxy de reativação está a aguardar o reinício         |
|   6   | Proxy de reativação não é suportado neste SO   |
|   7   | Anular o servidor de Proxy de reativação        |
|   8   | Falha na desinstalação do Proxy de reativação      |
|   9   | Tempo de execução do Proxy de reativação não suportado         |

## <a name="2200-statetopictypefdm"></a>2200 STATE_TOPICTYPE_FDM

    No State IDs.

## <a name="2201-statetopictypeccmcertbinding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

    No State IDs.

## <a name="2202-statetopictypeserverstatistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

    No State IDs.

## <a name="3000-statetopictypedmwnschannel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|0  | Conjunto de canal de serviço do Windows Push Notification|

## <a name="4000-statetopictypemdmdeviceproperty"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

    No State IDs.

## <a name="4002-statetopictypemdmclientidenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

    No State IDs.

## <a name="4003-statetopictypemdmapplicationrequest"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

    No State IDs.

## <a name="4004-statetopictypemdmapplicationstate"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

    No State IDs.

## <a name="4005-statetopictypemdmlicensedevicerelation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

    No State IDs.

## <a name="4006-statetopictypemdmlicensekeys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

    No State IDs.

## <a name="4007-statetopictypemdmpolicyassignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

    No State IDs.

## <a name="4008-statetopictypemdmandroidcount"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

    No State IDs.

## <a name="4009-statetopictypemdmslkstatus"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

    No State IDs.

## <a name="4010-statetopictypemdmusercompanytermacceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

    No State IDs.

## <a name="4022-statetopictypemdmdepsyncnowstatus"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

    No State IDs.

## <a name="4023-statetopictypemdmmamstoreappsync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

    No State IDs.

## <a name="5000-statetopictypecertificateenrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Desafio emitido                    |
|   2   |Falha na emissão do desafio              |
|   3   |Falha ao criar pedido                 |
|   4   |Falhada de envio do pedido               |
|   5   |Validação do desafio de foi concluída com êxito          |
|   6   |Falha na validação do desafio             |
|   7   |Falha na emissão                    |
|   8   |Emitir pendentes                   |
|   9   |Emitido                      |
|   10  |Falha no processamento de resposta          |
|   11  |Resposta pendentes                    |
|   12  |Inscrição foi concluída com êxito                    |
|   13  |Inscrição não necessária                   |
|   14  |Revoked                         |
|   15  |Removido da coleção                 |
|   16  |Renovar verificado                  |
|   17  |Falha na instalação              |
|   18  |Instalado                   |
|   19  |Falha ao eliminar                   |
|   20  |eliminado                     |
|   21  |Pedido de renovação               |


## <a name="5001-statetopictypecertificatecrp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Desafio emitido                       |
|   2   |Falha na emissão do desafio                 |
|   3   |Falha ao criar pedido                    |
|   4   |Falhada de envio do pedido                  |
|   5   |Validação do desafio de foi concluída com êxito             |
|   6   |Falha na validação do desafio                |
|   7   |Falha na emissão                       |
|   8   |Emitir pendentes                      |
|   9   |Emitido                         |
|   10  |Falha no processamento de resposta             |
|   11  |Resposta pendentes                       |
|   12  |Inscrição foi concluída com êxito                       |
|   13  |Inscrição não necessária                      |
|   14  |Revoked                            |
|   15  |Removido da coleção                    |
|   16  |Renovar verificado                     |
|   17  |Falha na instalação                 |
|   18  |Instalado                      |
|   19  |Falha ao eliminar                      |
|   20  |eliminado                        |
|   21  |Pedido de renovação                  |

## <a name="5200-statetopictyperesourceaccessstatus"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   | Configuração do Estado de pin foi concluída com êxito                   |
|   2   | Falha na configuração de pin de estado                  |
|   3   | Configuração de pin de estado não suportada               |
|   4   | Configuração de pin de estado em curso             |

## <a name="6000-statetopictyperemoteappsubscriptionstatus"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

    No State IDs.

## <a name="6001-statetopictyperemoteappsubscriptionsyncstatus"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

    No State IDs.

## <a name="6002-statetopictyperemoteappauthcookiessyncstatus"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

    No State IDs.

## <a name="6003-statetopictyperemoteapplicationssyncstatus"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

    No State IDs.

## <a name="6004-statetopictyperemoteapplockresult"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

    No State IDs.

## <a name="7000-statetopictypeusercompanytermacceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

    No State IDs.

## <a name="7001-statetopictypepfxcertificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Desafio emitido               |
|   2   |Falha na emissão do desafio         |
|   3   |Falha ao criar pedido            |
|   4   |Falhada de envio do pedido          |
|   5   |Validação do desafio de foi concluída com êxito     |
|   6   |Falha na validação do desafio        |
|   7   |Falha na emissão               |
|   8   |Emitir pendentes              |
|   9   |Emitido                 |
|   10  |Falha no processamento de resposta     |
|   11  |Resposta pendentes               |
|   12  |Inscrição foi concluída com êxito               |
|   13  |Inscrição não necessária              |
|   14  |Revoked                    |
|   15  |Removido da coleção            |
|   16  |Renovar verificado             |
|   17  |Falha na instalação         |
|   18  |Instalado              |
|   19  |Falha ao eliminar              |
|   20  |eliminado                |
|   21  |Pedido de renovação          |

## <a name="7010-statetopictypeconditionalaccesscompliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
||  1   | Sucesso de conformidade             |
|   2   | Ativação de conformidade no pacote de gestão      |
|   3   | Ativação de conformidade no cliente      |
|   4   | Ativação de conformidade no Intune      |
|   5   | Ativação de conformidade no AAD         |
|   6   | Conformidade comgmt Intune       |

## <a name="7200-statetopictypesuperpeerupdatecachemap"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Origem de Cache ponto a ponto adicionado                |
|   2   |Removido de origem de Cache ponto a ponto          |

## <a name="7201-statetopictypesuperpeerupdateconfig"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Origem de Cache ponto a ponto desativado              |
|   2   |Origem de Cache ponto a ponto está ativa                |

## <a name="7202-statetopictypedownloadaggregatedata"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Baixe o carregamento de dados de agregação       |

## <a name="7203-statetopictypepeersourcereqrejectionstats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Carregamento de dados de rejeição de origem do elemento de rede     |

## <a name="7300-statetopictypeproxytraffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

    No State IDs.

## <a name="7301-statetopictypeproxyconnection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

    No State IDs.

## <a name="7302-statetopictypesrsusagedata"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

    No State IDs.

## <a name="7303-statetopictypeproxytrafficidentity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

    No State IDs.

## <a name="8001-statetopictypehasreport"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     ID de mensagem de estado     |  Descrição da mensagem de estado |
|:-------------|:------|
|   1   |Atestado de estado de funcionamento é suportado         |
|   2   |Atestado de estado de funcionamento não é suportado         |

## <a name="statetopictypedeviceclientedplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

    No State IDs.

## <a name="8003-statetopictypeenablelostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

    No State IDs.

## <a name="8004-statetopictypedisablelostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

    No State IDs.

## <a name="8005-statetopictypelocatedevice"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

    No State IDs.

## <a name="8006-statetopictyperebootdevice"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

    No State IDs.

## <a name="8007-statetopictypelogoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

    No State IDs.

## <a name="8008-statetopictypeuserslist"></a>8008 STATE_TOPICTYPE_USERSLIST

    No State IDs.

## <a name="8009-statetopictypedeleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

    No State IDs.

## <a name="8010-statetopictypecleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

    No State IDs.

## <a name="8011-statetopictypecleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

    No State IDs.

## <a name="8012-statetopictypesetdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

    No State IDs.

## <a name="9000-statetopictypebookcicompliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

    No State IDs.

## <a name="9001-statetopictypebookcienforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

    No State IDs.

## <a name="next-steps"></a>Passos seguintes

- [Descrição do Estado do sistema de mensagens no System Center Configuration Manager](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [Documento técnico do gerenciamento de atualizações de software para o System Center Configuration Manager](https://www.microsoft.com/download/details.aspx?id=44578)

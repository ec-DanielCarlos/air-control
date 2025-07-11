# AirControl – Controle Inteligente de Climatização

## 🎯 Objetivo

Desenvolver um dispositivo embarcado capaz de controlar o acionamento e a temperatura de equipamentos de ar-condicionado por meio de comandos recebidos via MQTT. O dispositivo deverá interpretar os comandos e emitir sinais infravermelhos apropriados utilizando o módulo IR KY-005. Cada unidade do AirControl será responsável por controlar um único equipamento de ar-condicionado. O microcontrolador obrigatório é o iMCP HTNB32L.

## 🧰 Componentes Utilizados

- **Microcontrolador:** iMCP HTNB32L  
- **Módulo Emissor IR:** KY-005 (GPIO)  
- **Conectividade:** NB-IoT (via modem interno do HTNB32L)  
- **Broker MQTT:**  
  - IP: `131.255.82.115`  
  - Porta: `1883`  
- **PCB personalizada:** não se aplica a este projeto

## ⚙️ Requisitos Funcionais

### Recebimento de comandos via MQTT

- Escutar dois tópicos MQTT:
  - Um para controle de **ligar/desligar** o ar-condicionado.
  - Um para definição da **temperatura desejada**.
- Comportamentos esperados:
  - Ao receber `"ON"`: enviar sinal IR para **ligar** o ar-condicionado.
  - Ao receber `"OFF"`: enviar sinal IR para **desligar**.
  - Ao receber valor numérico (ex: `"24"`): enviar sinal IR para **ajustar a temperatura**.

### Emissão de sinal IR

- Utilizar o módulo IR KY-005.
- Os sinais devem ser compatíveis com o protocolo do modelo de ar-condicionado utilizado.
- Garantir envio confiável dos comandos IR (repetições, delays, etc.).

### Modo de operação

- Operar continuamente, aguardando comandos MQTT.
- Implementar reconexão automática ao broker em caso de falha.

## 🛰️ Tópicos MQTT Padronizados

> **IMPORTANTE**: Substitua `<ambiente>` pelo nome do local e `<equipamento>` por um identificador único do ar-condicionado (ex: `lab1`, `ac1`). Ambos devem ser em letras minúsculas e sem espaços.

| Finalidade   | Tópico MQTT                                         | Direção   | Tipo de dado     |
|--------------|------------------------------------------------------|-----------|------------------|
| Estado       | `hana/<ambiente>/aircontrol/<equipamento>/power`    | Assinatura | `"ON"` / `"OFF"` |
| Temperatura  | `hana/<ambiente>/aircontrol/<equipamento>/temperature` | Assinatura | `"22"`, `"24"`    |


## 🛰️ Tópicos MQTT Divididos por alunos

| Ambiente      | Sensor | Aluno   | Tópicos MQTT                                                                 |
|---------------|--------|---------|------------------------------------------------------------------------------|
| Mesanino      | 1      | Sergio  | - `hana/mesanino/aircontrol/01/power`<br>- `hana/mesanino/aircontrol/01/temperature` |
| Externo       | 1      | Claus   | - `hana/externo/aircontrol/01/power`<br>- `hana/externo/aircontrol/01/temperature` |
| Externo       | 2      | Daniel  | - `hana/externo/aircontrol/02/power`<br>- `hana/externo/aircontrol/02/temperature` |
| Prototipagem  | 1      | Bruno   | - `hana/prototipagem/aircontrol/01/power`<br>- `hana/prototipagem/aircontrol/01/temperature` |



## 🖨️ Desenvolvimento da PCB

- **Não aplicável.** Este projeto não exige o desenvolvimento de uma placa personalizada.

## 🔍 Observações Técnicas

- Conectar o KY-005 a um pino digital do HTNB32L.
- Utilizar biblioteca IR compatível com o protocolo do ar-condicionado (ex: NEC, LG, Samsung).
- Pode ser necessário capturar os códigos IR do controle original.
- Testar tempo entre comandos e uso de repetições.
- Implementar reconexão MQTT automática.

## 📋 Critérios de Avaliação

- Funcionamento correto do recebimento dos comandos via MQTT.
- Funcionamento correto da emissão funcional dos sinais IR com base nos comandos recebidos.
- Uso correto dos tópicos MQTT conforme padrão estabelecido.
- Documentação completa, na wiki do github, com evolução do projeto e dificuldades encontradas durante o desenvolvimento.  
  - Exemplo de documentação: [Hands-On Linux Wiki](https://github.com/rafaelfacioni/Hands-On-Linux/wiki)  
- Apresentação prática do projeto final.
- *(Opcional)* Registro pessoal na Wiki do repositório com os principais aprendizados adquiridos ao longo do curso.

---

> Este projeto faz parte do Módulo 4 do Curso de Capacitação em Sistemas Embarcados com o iMCP HTNB32L.

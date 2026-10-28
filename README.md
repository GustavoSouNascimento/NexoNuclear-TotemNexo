# Estação Nexo - Projeto Nexo Nuclear

## 1. Integrantes
| Nome | RM | Turma |
|------|----|-------|
| Murillo Kenzo | RM566948 | 2TDSPA |
| Kauan Prado | RM566990 | 2TDSPA |
| Cauã Rocha | RM567593 | 2TDSPR |
| Gustavo Souza | RM567134 | 2TDSPR |

## 2. Descrição

A Estação Nexo é um totem educativo que transforma uma ideia abstrata ("a radiação está em toda parte") em algo medido e visível. 
Instalado em escolas, museus e locais públicos, o totem ira medir a radiação natural e dados do ambiente e mostra o resultado ao visitante, com uma explicação simples.

Cada totem também envia suas leituras ao site do projeto. O totem exibe um QR Code que leva o visitante a esse site, onde há:
 
- Um **mapa interativo** com as medições de cada totem e projetos espalhados pelo brasil que utilizam de tecnologia nuclear.
- Um **quiz de mitos e verdades** sobre tecnologia nuclear, em que cada resposta vem com uma explicação objetiva e a referência utilizada.

### Como contribui para o projeto
 
- **Torna o tema concreto:** o visitante vê a radiação natural do próprio ambiente, em vez de ouvir falar dela só em notícias e filmes.
- **Quebra o medo e os mitos:** a medição vem acompanhada de explicações sobre as fontes naturais (raios cósmicos, solo e rochas, radônio, plantas e o próprio corpo) e sobre as aplicações da tecnologia nuclear no dia a dia.
- **Leva o público ao conteúdo digital:** o QR Code conecta o espaço físico ao mapa e ao quiz, com gamificação.

### Onde IoT e Redes são aplicadas
 
| Onde | Necessidade que atende |
| --- | --- |
| **IoT** no totem (sensores ligados ao ESP32) | Medir de verdade a radiação natural, a temperatura e a umidade do local, e detectar a presença do visitante. |
| **Redes** (Wi-Fi do local e HTTP) | Enviar as leituras de vários totens para um mesmo sistema, permitindo compará-las no mapa do site. |

## 3. Componentes

| Componente | Função |
| --- | --- |
| ESP32 | Microcontrolador do totem: lê os sensores, processa os dados, controla o display e envia as leituras ao servidor via Wi-Fi. |
| Contador Geiger-Müller RadiationD v1.1 | Mede a radiação natural do ambiente. |
| Sensor de presença HC-SR04 | Detecta a presença de pessoas próximas ao totem e ativa o display. |
| Sensor de temperatura e umidade DHT22 | Mede temperatura e umidade do ambiente, para complementar a leitura de radiação. |
| Tela ou display | Mostra ao visitante as leituras e mensagens educativas. |

## 4. Comunicação

### Entre sensores e ESP32
 
| Dispositivo | Como se comunica com o ESP32 |
| --- | --- |
| RadiationD v1.1 | Envia um pulso digital a cada detecção, o ESP32 conta os pulsos por interrupção em um pino GPIO. |
| DHT22 | Protocolo digital de um fio. |
| HC-SR04 | Pinos `TRIG` (disparo) e `ECHO` (retorno), o ESP32 calcula a distância pelo tempo do eco. |
| Tela ou display | Interface digital |
 
### Entre o ESP32 e o sistema
 
O ESP32 usa o módulo Wi-Fi integrado, conectado à rede do local onde o totem está instalado. 
Com a biblioteca `HTTPClient.h`, envia as leituras por HTTP POST, em JSON, a uma API REST consumida pelo site do projeto. 
Se o Wi-Fi cair, o totem continua exibindo as leituras no display e reenvia os dados quando a conexão voltar.

### Tecnologias previstas
 
- **ESP32**, com firmware em C/C++ (Arduino framework)
- **Sensores:** Geiger-Müller (RadiationD v1.1), DHT22 e HC-SR04
- **Rede:** Wi-Fi, HTTP/HTTPS e JSON
- **Servidor:** API REST e banco de dados ORACLE
- **Site:** mapa interativo e quiz de mitos e verdades 

## 5. Fluxograma

<img width="1912" height="2200" alt="Image" src="https://github.com/user-attachments/assets/4b6f347f-02ee-44f5-802c-e03d842fa71d" />

## 6. Vídeo de Apresentação

[Link do Youtube](https://youtu.be/-3WUUPl9VXM)

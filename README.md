# UAS Intent Dataset — Shanghai

Dataset de comunicações entre VANTs (UAS/UAVs) e controle de tráfego aéreo urbano, com rótulos de intenção para uso em classificação por LLMs.

## Contexto

Os dados simulam operações de gestão de tráfego aéreo urbano (UTM) sobre a cidade de **Xangai, China** (latitude ~31.17–31.30, longitude ~121.39–121.64), com base em infraestrutura e densidade de voo compatíveis com a região.

## Origem

O dataset foi produzido a partir da combinação de dois conjuntos de dados:

1. **Mensagens do GP de Fórmula 1 em Interlagos** — comunicações de rádio entre pilotos e equipes durante o Grande Prêmio de Interlagos, utilizadas como base para os padrões linguísticos e estrutura das mensagens de voz/texto entre aeronaves e controle.
2. **LADE (Logistics and Delivery dataset)** — dataset de logística urbana da China, utilizado para fornecer as coordenadas geográficas, rotas e padrões de tráfego na região de Xangai.

A partir desses dois conjuntos, foram geradas mensagens de rádio realistas entre aeronaves e o controle, rotuladas manualmente e semi-automaticamente com intenções de comunicação.

## Estrutura

```
dataset/
├── uas_chat_final.txt       # Log de comunicações no formato de chat (timestamp, remetente, mensagem)
└── uas_dataset_final.csv    # Dataset estruturado com rótulos de intenção e coordenadas GPS

prompts/
└── llm_contextual.py        # Prompts e lógica de classificação de intenção via LLM
```

## Dataset (`uas_dataset_final.csv`)

| Coluna      | Descrição                                             |
|-------------|-------------------------------------------------------|
| `timestamp` | Data e hora da comunicação                            |
| `sender`    | Identificador do remetente (UAS-XX, UAV-XX, Control) |
| `intent`    | Rótulo de intenção (I1–I8, outros)                    |
| `mensagem`  | Texto da comunicação                                  |
| `lat`       | Latitude (região de Xangai)                           |
| `lng`       | Longitude (região de Xangai)                          |
| `ciclo_id`  | ID do ciclo de missão                                 |
| `fragmento` | Indica se a mensagem é fragmento de outra             |

**Total de registros:** 1.150 mensagens

## Classes de Intenção

| Classe   | Descrição                          |
|----------|------------------------------------|
| `I1`     | Solicitação de decolagem/partida   |
| `I2`     | Autorização de decolagem           |
| `I3`     | Reporte de status em voo           |
| `I4`     | Solicitação de pouso               |
| `I5`     | Autorização de pouso               |
| `I6`     | Alerta / aviso de conflito         |
| `I7`     | Atualização de posição/rota        |
| `I8`     | Encerramento de missão             |
| `outros` | Comunicações sem intenção definida |

## Localização

Os voos cobrem a área urbana de Xangai, incluindo regiões de alta densidade como Pudong e Puxi.

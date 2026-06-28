# Gêmeo Digital — Rocket Tank (ROS 2)

**Contexto:** Projeto de pesquisa de mestrado · IARA++ — UFABC · 2024–presente

---

## Visão Geral

Desenvolvimento de um sistema de **gêmeo digital** para o robô de esteira de baixo custo *Rocket Tank*, utilizando ROS 2 como middleware de comunicação. O projeto investiga como representações virtuais em tempo real podem apoiar monitoramento, depuração e controle de robôs físicos de forma acessível.

---

## Problema

Robôs de esteira (skid-steer) apresentam desafios clássicos de odometria: o deslizamento das esteiras torna os modelos cinemáticos convencionais imprecisos. Ao mesmo tempo, rodar todo o processamento no microcontrolador embarcado é limitante em termos de capacidade computacional e flexibilidade.

A proposta do projeto é deslocar o cálculo de odometria para fora do MCU (*off-MCU odometry*), processando os dados de encoders em um computador de bordo com ROS 2, e validar o resultado com uma câmera overhead como ground truth independente.

---

## Arquitetura do Sistema

```
Rocket Tank (hardware)
  └── Encoders → MCU → Serial → ROS 2 (nó de odometria)
                                    ↓
                             Gêmeo Digital (RViz / simulação)

Câmera Overhead (Raspberry Pi)
  └── Marcadores ArUco → nó ROS 2 de ground truth
                              ↓
                       Comparação APE (evo)
```

---

## Tecnologias

- **ROS 2** — comunicação entre nós, publicação de odometria e ground truth
- **Python** — nós de processamento e integração
- **OpenCV + ArUco** — rastreamento de posição via câmera overhead
- **evo** — avaliação de trajetória (Absolute Pose Error)
- **Raspberry Pi** — sistema embarcado para streaming e processamento de câmera

---

## Estado Atual

Projeto em andamento. Artigo sendo preparado para submissão em periódico IEEE (IEEE Access ou IEEE Latin America Transactions).

---

## Repositório

🔗 *(link para o repositório será adicionado após publicação do artigo)*

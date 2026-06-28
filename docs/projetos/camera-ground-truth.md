# Sistema de Ground Truth com ArUco e Raspberry Pi

**Contexto:** Infraestrutura de laboratório · IARA++ — UFABC · 2024

---

## Visão Geral

Desenvolvimento de um sistema de **câmera overhead embarcada** para rastreamento de robôs em tempo real dentro do laboratório, utilizando marcadores ArUco como referência visual. O sistema funciona como fonte de ground truth independente para validação de algoritmos de odometria.

---

## Motivação

Para avaliar a precisão de um sistema de odometria, é necessária uma referência externa confiável — algo que diga *onde o robô realmente está*, sem depender do próprio sistema que está sendo testado. A câmera overhead com ArUco cumpre esse papel de forma econômica e reprodutível.

---

## Como Funciona

Um **Raspberry Pi** com câmera USB é instalado no teto do laboratório. Ele captura vídeo do ambiente e transmite via MJPEG usando **ustreamer**. Um nó ROS 2 consome esse stream, detecta marcadores ArUco afixados ao robô, e publica a posição estimada como `geometry_msgs/PoseStamped` no tópico `/ground_truth`.

Esse tópico é então comparado com os dados de odometria do robô usando a biblioteca **evo**, calculando o erro absoluto de trajetória (APE).

---

## Arquitetura

```
Raspberry Pi (overhead)
  └── Câmera USB
       └── ustreamer (MJPEG stream, porta 8080)
            └── ground_truth_node.py (ROS 2)
                 └── Detecção ArUco (OpenCV)
                      └── /ground_truth (PoseStamped)
```

---

## Tecnologias

- **Raspberry Pi Zero 2 W / 3B+** — hardware embarcado
- **ustreamer** — streaming MJPEG de baixa latência
- **OpenCV + ArUco** — detecção e estimativa de pose dos marcadores
- **ROS 2** — integração com o restante do sistema robótico
- **Python** — implementação do nó de ground truth

---

## Resultado

Sistema funcional e integrado ao pipeline de avaliação do projeto de gêmeo digital do Rocket Tank. Permite comparação objetiva entre odometria estimada e posição real do robô ao longo de trajetórias no laboratório.

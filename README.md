# 🎨 Totem FlexBuy — Assistente Inteligente de Recomendação Acessível  

### 🚀 FIAP Challenge FlexMedia — Sprint 1  
**Tema:** Totem inteligente com IA e interatividade  
**Equipe:** Cloves Silva Filho, Jose Luiz de Oliveira Junior, Kaique Cadimiel Amasio De Souza
**Ano:** 2025  

---

## 📋 1. Introdução  

O **Totem FlexBuy** é um assistente interativo que ajuda usuários a **encontrar o produto ideal** de forma **rápida, acessível e sem depender de celular**.  

A solução é voltada para **ambientes comerciais, culturais e educacionais**, oferecendo uma experiência **inclusiva, gamificada e inteligente**.  

O diferencial do FlexBuy está na sua **entrada por desenho**, que substitui a voz — tornando o sistema mais preciso em locais barulhentos — e em seus **modos de acessibilidade**, que permitem o uso por **pessoas com deficiência visual ou auditiva**.

---

## 💡 2. Problema  

Nos ambientes de compra físicos, muitos usuários enfrentam:  
- Dificuldade para comparar produtos e encontrar o melhor custo-benefício;  
- Falta de acessibilidade em totens tradicionais;  
- Dependência de celulares e vídeos comparativos;  
- Ambientes ruidosos que inviabilizam o uso de comandos por voz.  

Esses fatores prejudicam a **autonomia, inclusão e eficiência** na tomada de decisão do consumidor.

---

## 🎯 3. Solução Proposta  

O **Totem FlexBuy** é um sistema baseado em **Python + IA + MongoDB** que permite ao usuário **desenhar o produto desejado** diretamente na tela touch.  
O sistema reconhece o desenho e sugere produtos similares, apresentando informações sobre **preço, avaliações e custo-benefício**.  

A interface é **gamificada e acessível**, oferecendo dois modos de interação:

- **Modo Visual:** Interface colorida e interativa com vídeos em Libras, ícones e gamificação;  
- **Modo Audioguia:** Navegação por áudio e toques, com narração automática dos elementos para usuários com deficiência visual.

---

## 🧠 4. Objetivos da Solução  

- Facilitar o processo de escolha e comparação de produtos;  
- Promover **inclusão e acessibilidade** em ambientes físicos;  
- Operar de forma **offline**, com **atualização remota** via servidor HTTP;  
- Proporcionar uma **experiência lúdica e envolvente**;  
- Coletar dados anônimos sobre engajamento e preferências.

---

## ⚙️ 5. Arquitetura da Solução  

```pgsql
            +------------------------------------+
            |        Servidor Remoto (Cloud)     |
            | Flask API + MongoDB Atlas (backup) |
            | Atualização de catálogo e logs     |
            +--------------------▲---------------+
                                 │
                       Sincronização (JSON)
                                 │
    ┌────────────────────────────▼──────────────────────────┐
    │                TOTEM FLEXBUY (Linux)                  │
    │-------------------------------------------------------│
    │  Servidor Flask local (HTTP)                          │
    │  Banco de dados MongoDB local                         │
    │  Módulo de IA de Desenho (TensorFlow / TeachableML)   │
    │  Interface Gamificada (HTML/CSS/JS)                   │
    │  Módulo Libras + Audioguia (pyttsx3)                  │
    │-------------------------------------------------------│
    │  Entrada: Desenho em tela touch, toques e sons        │
    │  Saída: Tela, Libras, fala e sons interativos         │
    └───────────────────────────────────────────────────────┘
```


---

## 🧩 6. Funcionalidades  

- **Entrada por desenho** — o usuário desenha o produto desejado, e o sistema identifica e recomenda opções semelhantes.  
- **Recomendações personalizadas** — produtos exibidos com base em similaridade e custo-benefício.  
- **Modo gamificado** — interação leve, com pontos e recompensas simbólicas.  
- **Modo Libras** — vídeos explicativos e legendas automáticas.  
- **Modo Audioguia** — navegação completa por voz, com leitura automática dos elementos.  
- **Operação offline** — usa base local, mas sincroniza dados e catálogo remotamente.  
- **Acesso remoto para manutenção** — via API Flask e banco MongoDB Atlas.  

---

## 🧰 7. Tecnologias Utilizadas  

| Camada | Tecnologia |
|--------|-------------|
| **Linguagem principal** | Python |
| **Servidor local** | Flask |
| **Banco de dados local** | MongoDB Community |
| **Banco remoto (opcional)** | MongoDB Atlas |
| **Interface Web** | HTML5, CSS3, JavaScript (Canvas API) |
| **IA de reconhecimento de desenho** | TensorFlow / Teachable Machine |
| **Acessibilidade visual (voz)** | pyttsx3 (offline) |
| **Acessibilidade auditiva (Libras)** | Vídeos MP4 e ícones visuais |
| **Sistema operacional** | Linux (Ubuntu / Raspbian) |
| **Hardware sugerido** | Microcomputador com tela touch |

---

## ♿️ 8. Inclusão e Acessibilidade  

O Totem FlexBuy foi projetado para ser **totalmente inclusivo**, atendendo pessoas com diferentes deficiências:

| Necessidade | Recurso Acessível |
|--------------|------------------|
| **Auditiva** | Vídeos em Libras e legendas automáticas |
| **Visual** | Narração de texto (voz), sons de interface e toque guiado |
| **Motora** | Áreas amplas de toque e suporte a teclado físico |
| **Cognitiva** | Interface gamificada e linguagem simples |

### Modo Audioguia
- Ativado ao **tocar e segurar na tela por 3 segundos**.  
- Sistema passa a **narrar os elementos** e confirmações por voz.  
- Navegação por **toque único** (ouvir opção) e **duplo toque** (confirmar).  

### 🔊 Exemplo de Código (narração de texto)
```python
import pyttsx3

def falar(texto):
    engine = pyttsx3.init()
    engine.say(texto)
    engine.runAndWait()

```

## 🧾 9. Estrutura de Banco de Dados (MongoDB)
```json
{
  "produto_id": 101,
  "nome": "Notebook Flex Pro",
  "categoria": "Informática",
  "preco": 3299.90,
  "avaliacao": 4.7,
  "descricao": "Notebook leve, ideal para estudos e trabalho.",
  "tags": ["notebook", "trabalho", "custo-beneficio"]
}
```
## 🗂️ 10. Estrutura de Pastas

```pgsql
totem-flexbuy/
│
├── app/
│   ├── main.py             # Servidor Flask
│   ├── draw_recognizer.py  # IA de reconhecimento de desenhos
│   ├── recommender.py      # Lógica de recomendação
│   ├── db.py               # Conexão com MongoDB
│   ├── audio_guide.py      # Modo audioguia
│   ├── static/             # CSS, JS, vídeos, sons
│   └── templates/          # HTMLs da interface
│
├── docs/
│   ├── arquitetura.png
│   └── README.md
│
├── requirements.txt
└── .gitignore
```

## 🛠️ 11. Plano de Desenvolvimento  

| Sprint | Foco | Entregas |
|--------|------|----------|
| **Sprint 1** | Planejamento e arquitetura | Escopo, tecnologias e documentação técnica |
| **Sprint 2** | Protótipo funcional | Interface HTML + IA simples + base local |
| **Sprint 3** | Integração e acessibilidade | Modo audioguia, Libras e sincronização remota |

---

## 🔒 12. Segurança e Privacidade  

- Dados de uso **anonimizados** (sem informações pessoais)  
- Comunicação segura entre totens e servidor (**HTTPS**)  
- **Controle de acesso administrativo** por senha  
- Conformidade com **LGPD**  
- Armazenamento local e remoto protegido por autenticação  

---

## 🧭 13. Benefícios da Solução  

- Interface acessível e inclusiva  
- Não depende de celular ou internet constante  
- Gamificação e engajamento do usuário  
- Operação offline + atualização remota  
- Compatível com Linux e hardware de baixo custo  
- Modular e expansível para novos tipos de interação  

---

## 🧾 14. Licença  

Este projeto foi desenvolvido para fins educacionais como parte do **Challenge FlexMedia – FIAP 2025**.  
O uso, reprodução ou modificação fora do contexto acadêmico requer autorização dos autores e da instituição.

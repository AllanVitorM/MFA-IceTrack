# Ice Track: Sistema de Rastreamento e Qualidade de Alimentos (IoT)

[![Deploy on Render](https://img.shields.io/badge/Deploy-Render-46e3b7?style=for-the-badge&logo=render)](https://icetrack.onrender.com/)
[![GitHub Repository](https://img.shields.io/badge/GitHub-MFA--IceTrack-100000?style=for-the-badge&logo=github)](https://github.com/AllanVitorM/MFA-IceTrack)

## Descrição do Projeto

O **Ice Track** é um **Sistema Integrado de Rastreamento e Monitoramento da Qualidade de Alimentos** perecíveis durante o transporte, baseado em **IoT (Internet das Coisas)**. Utilizando sensores de temperatura e GPS, o sistema garante a transmissão de dados em tempo real para a nuvem, oferecendo visibilidade e controle contínuo sobre a cadeia de frio.

Este projeto foi detalhado no "Plano Integrado de Qualidade para o projeto do PI (IoT)" e envolve um dispositivo embarcado (ESP32), comunicação via MQTT/HTTP e integração com um backend/nuvem para o Dashboard.

---

## Problema Solucionado

O principal desafio na cadeia de frio é a **falta de visibilidade e controle contínuo** da temperatura durante o transporte de alimentos. Isso resulta em:

*   **Falhas de Temperatura:** Ocorrência de desvios que comprometem a qualidade e segurança dos produtos.
*   **Dados Incompletos:** Dificuldade em gerar um histórico confiável para análise.
*   **Dificuldade de Compliance:** Impedimento em atender às exigências rigorosas dos órgãos fiscalizadores.

## Como o Ice Track Soluciona

O Ice Track transforma a gestão da cadeia de frio através de uma solução tecnológica completa:

| Solução | Descrição |
| :--- | :--- |
| **Hardware Dedicado** | Utiliza ESP32, Sensores DHT11 (temperatura/umidade) e GPS NEO-6M para coleta precisa de dados. |
| **Conectividade Real-Time** | Transmissão imediata de dados via MQTT/HTTP para serviços de nuvem (AWS ou Firebase). |
| **Monitoramento Ativo** | Geração de alertas automáticos para desvios de temperatura e falhas de comunicação. |
| **Cibersegurança** | Proteção de dados sensíveis com criptografia robusta **AES-256**. |
| **Gestão de Dados** | Relatórios automatizados essenciais para auditoria e garantia de compliance regulatório. |

---

## Arquitetura do Sistema

O projeto Ice Track é estruturado em três camadas principais que garantem a coleta, processamento e visualização dos dados:

1.  **Hardware IoT (Coleta de Dados)**
    *   **Componentes:** ESP32, DHT11, GPS NEO-6M.
    *   **Função:** Coleta a amostragem de dados de localização, umidade e temperatura.

2.  **Backend (Processamento e Armazenamento)**
    *   **Tecnologias:** Thinkspeak (para extração inicial dos dados do hardware) e tratamento posterior com **Python**.
    *   **Função:** Receber, processar, armazenar e disponibilizar os dados coletados.

3.  **Front-end (Visualização e Interação)**
    *   **Tecnologia:** **React.ts** (mencionado na arquitetura) e **Flask** (para a aplicação web e MFA).
    *   **Função:** Exibição do dashboard com os dados processados e um mapa de rastreamento em tempo real.

---

## Objetivos de Qualidade

O projeto foi desenvolvido com foco em métricas de qualidade rigorosas para garantir a confiabilidade e segurança da solução:

| Objetivo | Métrica | Descrição |
| :--- | :--- | :--- |
| **Confiabilidade** | 99,5% | Disponibilidade contínua do sistema. |
| **Desempenho** | 30 segundos | Latência máxima na transmissão e exibição dos dados. |
| **Segurança** | 100% | Todos os dados protegidos com criptografia AES-0256. |
| **Usabilidade** | 15 minutos | Tempo de aprendizado para utilização do Dashboard. |
| **Manutenibilidade** | 24 horas | Tempo máximo para correção de defeitos críticos. |

---

## Detalhes Técnicos do Dashboard Web (Flask MFA v2)

A aplicação web (Dashboard) é construída com **Flask** e incorpora **Multi-Factor Authentication (MFA)** para garantir a segurança do acesso aos dados.

### ⚙️ Tecnologias Utilizadas

*   **Backend:** Python, Flask, PyMongo (MongoDB), Pandas.
*   **Segurança:** PyOTP (MFA), Werkzeug Security.
*   **Frontend:** HTML/CSS (Bootstrap), JavaScript.

### Estrutura de Pastas

```
.
├── static/
│   └── styles.css
├── templates/
│   ├── base.html
│   ├── dashboard.html
│   ├── index.html
│   ├── login.html
│   ├── mfa_setup.html
│   ├── mfa_verify.html
│   └── register.html
├── .gitignore
├── README.md
├── app.py
├── dados.csv
├── render.yaml
└── requirements.txt
```

### 📦 Dependências (`requirements.txt`)

```
Flask>=2.0
pyotp
qrcode[pil]
gunicorn
pymongo
python-dotenv
pandas
```

### Como Rodar Localmente

Siga os passos abaixo para configurar e executar o projeto em seu ambiente local:

1.  **Clone o repositório:**
    ```bash
    git clone https://github.com/AllanVitorM/MFA-IceTrack.git
    cd MFA-IceTrack
    ```

2.  **Crie e ative o ambiente virtual:**
    ```bash
    python3 -m venv venv
    source venv/bin/activate
    ```

3.  **Instale as dependências:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Configure as variáveis de ambiente:**
    O projeto requer o `APP_SECRET` e o `MONGO_URI` (para conexão com o MongoDB).

    ```bash
    # Exemplo de exportação (para testes)
    export APP_SECRET='uma_senha_secreta_muito_segura'
    export MONGO_URI='mongodb://localhost:27017/MFA-BigData' # Substitua pela sua URI
    ```

5.  **Execute a aplicação:**
    ```bash
    python app.py
    ```

A aplicação estará disponível em `http://127.0.0.1:5000/`.

---

## Implantação

O projeto está hospedado e acessível publicamente através do **Render**:

*   **Link de Acesso:** [https://icetrack.onrender.com/](https://icetrack.onrender.com/)

### Configuração do Render (`render.yaml`)

O arquivo de configuração para o serviço web no Render é o seguinte:

```yaml
services:
  - type: web
    name: flask-mfa-v2
    env: python
    region: oregon
    plan: free
    buildCommand: pip install -r requirements.txt
    startCommand: gunicorn --bind 0.0.0.0:$PORT app:app
```

---

## Equipe

Este projeto foi desenvolvido pelos seguintes membros:

*   Allan Vitor Marques
*   Emerson Costa
*   Felipe Pimentel
*   Gabriel Martins
*   Heloisa Costa
*   Ricardo Tompson
*   Walison Brandão

---

## Conclusão

O **Ice Track** é mais do que um protótipo; é uma plataforma robusta de IoT que monitora em tempo real temperatura e localização, com alta disponibilidade e criptografia de ponta a ponta. Sustentado por testes automatizados e monitoramento contínuo, oferece a confiabilidade e segurança necessárias para apoiar decisões estratégicas, reduzir perdas, garantir conformidade regulatória e escalar para frotas reais e novos mercados.

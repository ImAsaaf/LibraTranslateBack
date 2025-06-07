# 🧠 Libra Translate - Backend (FastAPI)

Este é o backend da aplicação **Libra Translate**, que utiliza **FastAPI** e um modelo de IA para reconhecer letras em Libras a partir de imagens.

## ✅ Pré-requisitos

- Python **3.10**
- `pip` atualizado
- Git (opcional)

> ⚠️ Este projeto **não é compatível com Python 3.11+** devido a limitações de pacotes como `tensorflow-io-gcs-filesystem`.

---

## ⚙️ Instalação

1. **Clone o repositório**

```bash
git clone https://github.com/seu-usuario/libra-translate-be.git
cd libra-translate-be
```

2. **Crie e ative um ambiente virtual**

```bash
python -m venv .venv

# No Windows:
.venv\Scripts\activate

# No macOS/Linux:
source .venv/bin/activate
```

3. **Instale as dependências**

```bash
pip install -r requirements.txt
```

> 🔁 **Ajustes feitos no `requirements.txt`:**
> - `tensorflow-io-gcs-filesystem==0.31.0` usado por compatibilidade com Python 3.11
> - `uvloop` removido por ser incompatível com Windows

---

## ▶️ Como rodar o backend

Dentro da pasta raiz do projeto, execute:

```bash
uvicorn app.main:app --reload
```

O servidor FastAPI será iniciado em:

```
http://127.0.0.1:8000
```

---

## 🧪 Endpoints disponíveis

| Método | Rota       | Descrição                                                   |
|--------|------------|-------------------------------------------------------------|
| GET    | `/info`    | Retorna informações básicas da aplicação                    |
| POST   | `/predict` | Recebe uma imagem e retorna a letra em Libras correspondente |

Para testar o endpoint `/predict`, envie uma imagem `.jpg` ou `.png` com uma mão fazendo um sinal de uma letra.

---

## 📁 Estrutura básica

```
libra-translate-be/
├── app/
│   ├── core/
│   ├── utils/
│   ├── main.py
│   └── __init__.py
├── requirements.txt
├── setup.py
└── ...
```

---

## 👨‍💻 Autor

Desenvolvido por Taciano da Hora e equipe.
---

## 🔗 Conectando o Frontend (React Native/Expo) ao Backend

Para que o aplicativo em React Native consiga se comunicar com a API do FastAPI, siga as instruções abaixo:

### 1. Inicie o backend primeiro

Certifique-se de que o backend está rodando com:

```bash
uvicorn app.main:app --reload
```

Ele estará acessível em: `http://127.0.0.1:8000` (ou `http://localhost:8000`)

---

### 2. Configure a URL da API no frontend

No código do frontend (React Native), altere a base URL das requisições para o backend:

#### 💻 Se estiver rodando o app no emulador ou Expo no MESMO computador:

```js
const API_URL = "http://localhost:8000";
```

#### 📱 Se estiver rodando o app no celular via Expo:

Descubra o IP local do seu computador (ex: `192.168.0.105`) e use:

```js
const API_URL = "http://192.168.0.105:8000";
```

> ⚠️ Importante: O celular e o PC devem estar na **mesma rede Wi-Fi** para isso funcionar.

---

### 3. Rodar o frontend com Expo

No terminal do frontend:

```bash
npm install
npm start
```

Use o QR Code no celular (com o app do Expo Go) para abrir o app.

---

### ❗ Erros comuns

- **CORS bloqueando requisições?**
  Certifique-se de que o FastAPI permite requisições do frontend. Se necessário, adicione:

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # Ou especifique seu IP ou domínio
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

Adicione isso logo após criar o `FastAPI()` no `main.py`.

---
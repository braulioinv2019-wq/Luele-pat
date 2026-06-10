# LUELE PAT — Sistema de Gestão Patrimonial

**Sociedade Mineira do Luele · Sector de Património**

-----

## 1. Criar o Projecto Firebase

1. Acede a <https://console.firebase.google.com>
1. Clica em **“Adicionar projecto”**
1. Nome: `luele-pat` (ou similar)
1. Desactiva o Google Analytics (opcional)
1. Clica em **“Criar projecto”**

-----

## 2. Configurar o Firestore

1. No menu lateral, clica em **“Firestore Database”**
1. Clica em **“Criar base de dados”**
1. Selecciona **“Iniciar em modo de teste”** (para começar)
1. Escolhe a região: `eur3 (europe-west)` ou `nam5`
1. Clica em **“Activar”**

-----

## 3. Obter as Credenciais

1. No menu lateral, clica no ícone de engrenagem → **“Definições do projecto”**
1. Em baixo, na secção **“As suas aplicações”**, clica em **”</> Web”**
1. Nome da app: `luele-pat-web`
1. Clica em **“Registar app”**
1. Copia o bloco `firebaseConfig` — vai ser assim:

```js
const firebaseConfig = {
  apiKey: "AIza...",
  authDomain: "luele-pat.firebaseapp.com",
  projectId: "luele-pat",
  storageBucket: "luele-pat.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

-----

## 4. Configurar o Sistema

1. Abre o ficheiro `index.html`
1. Localiza a secção `/* === CONFIGURAÇÃO FIREBASE === */`
1. Substitui os valores pelo teu `firebaseConfig`
1. Faz o mesmo no ficheiro `import_data.html`

-----

## 5. Importar os Dados do Inventário

1. Abre o ficheiro `import_data.html` no browser
1. Clica em **“Importar 371 Ativos”**
1. Aguarda a conclusão (pode demorar 1-2 minutos)
1. Verifica no Firestore Console se a colecção `ativos` foi criada

-----

## 6. Deploy no GitHub Pages

```bash
# Criar repositório
git init
git add .
git commit -m "LUELE PAT v1.0 - Sistema de Gestão Patrimonial"
git remote add origin https://github.com/braulioinv2019-wq/luele-pat.git
git push -u origin main

# Activar GitHub Pages
# Settings → Pages → Source: Deploy from branch → main → / (root)
```

URL do sistema: `https://braulioinv2019-wq.github.io/luele-pat`

-----

## Estrutura do Projecto

```
luele-pat/
├── index.html          ← Sistema principal (todos os módulos)
├── import_data.html    ← Ferramenta de importação do inventário
└── README.md           ← Este ficheiro
```

-----

## Módulos do Sistema

|Módulo        |Descrição                            |
|--------------|-------------------------------------|
|Dashboard     |KPIs, gráficos, alertas de ativos    |
|Cadastro      |Registo e edição de ativos           |
|Transferências|Movimentação entre sectores          |
|Termos        |Geração de termos de responsabilidade|
|Depreciação   |Cálculo automático de valor actual   |
|Relatórios    |Exportação Excel e PDF               |
|Utilizadores  |Controlo de acesso por perfil        |

-----

## Regras Firestore (Produção)

Quando o sistema estiver estável, actualiza as regras no Firestore:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.time < timestamp.date(2026, 1, 1);
    }
  }
}
```

-----

*LUELE PAT v1.0 — Junho 2025*

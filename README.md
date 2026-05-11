# 📦 Envio Comprovado — Te provei

> Grave e comprove cada embalagem enviada. Proteção total para vendedores de marketplace.

---

## O que é

O **Envio Comprovado** é um sistema composto por:

- 📱 **App mobile** (Android / iOS) — grava o processo de embalagem usando a câmera do celular
- 💻 **Servidor PC** (Windows) — recebe e organiza os vídeos na sua rede local

Ao embalar um pedido, o app detecta automaticamente o código de rastreio da etiqueta Shopee e inicia a gravação. O vídeo é enviado diretamente para o seu computador via Wi-Fi — sem internet, sem nuvem, sem nenhum dado saindo da sua rede.

---

## Para quem é

- Vendedores de Shopee, Mercado Livre, Magalu e outros marketplaces
- Quem precisa provar o conteúdo e peso de um envio
- Pequenos negócios que despacham pedidos diariamente

---

## Como funciona

```
Celular (app)  ──Wi-Fi local──▶  PC (servidor)
     │                                │
     │  1. Detecta etiqueta BR...     │
     │  2. Inicia gravação            │
     │  3. Envia vídeo ao PC          │  4. Salva como:
     │                                │  BR269644_20260509_170229_Galaxy.mov
```

---

## Instalação — Servidor PC (Windows)

### Requisitos
- Windows 10 ou 11 (64 bits)
- Python 3.10+ instalado ([python.org](https://python.org))
- ffmpeg instalado (opcional — para compressão automática de vídeos)

### Passo a passo

**1. Baixar o código**
```bash
# Opção A: clonar via git
git clone https://github.com/SEU_USUARIO/envio-comprovado.git

# Opção B: baixar o ZIP
# Clique em "Code" → "Download ZIP" e extraia
```

**2. Instalar dependências**
```bash
cd envio-comprovado/pc
pip install flask werkzeug Pillow
```

**3. Iniciar o servidor**
```bash
python launcher.py
```

**4. Ou gerar o .exe (uma vez só)**
```bash
cd pc
BUILD.bat
# O executável aparece em pc/dist/EnvioComprovado.exe
```

### Pasta padrão de gravações
```
C:\EnvioSeguro\Gravacoes
```
Criada automaticamente ao iniciar o servidor. Pode ser alterada na interface.

---

## Instalação — App Mobile

### Android
Disponível na **Google Play Store**:  
🔗 [play.google.com/store/apps/details?id=com.enviocomprovado.app](https://play.google.com/store/apps/details?id=com.enviocomprovado.app)

### iOS
Em breve na App Store.

### Para desenvolvedores (Expo)
```bash
cd mobile
npm install
npx expo start
```

---

## Configuração inicial

1. **Inicie o servidor no PC** — anote o IP exibido em verde (ex: `192.168.1.105`)
2. **Abra o app no celular** — siga o tutorial de 4 passos
3. **Digite o IP do PC** no app — salvo automaticamente para próximas sessões
4. **Certifique-se** que celular e PC estão na mesma rede Wi-Fi
5. **Aponte para a etiqueta** — a gravação inicia automaticamente

---

## Nome dos arquivos gerados

Os vídeos são salvos com o seguinte formato:

```
BR2696445115281_20260509_170229_GalaxyA54.mov
│               │         │      │
│               │         │      └── Nome do dispositivo
│               │         └───────── Hora (HHMMSS)
│               └─────────────────── Data (YYYYMMDD)
└─────────────────────────────────── Código de rastreio (chave primária)
```

---

## Requisitos de rede

| Item | Requisito |
|------|-----------|
| Celular e PC | Mesma rede Wi-Fi |
| Porta usada | TCP 5000 |
| Internet | **Não necessária** |
| Nuvem | **Não utilizada** |

> ⚠️ Roteadores com múltiplas sub-redes (repetidores em modo roteador) podem impedir a comunicação. Use modo bridge/AP nesses casos.

---

## Segurança e privacidade

- ✅ 100% local — nenhum dado sai da sua rede
- ✅ IP salvo com criptografia AES-256 (Keychain do SO)
- ✅ Autenticação por Device-ID + token de sessão em cada request
- ✅ Sem conta, sem login, sem cadastro
- ✅ Você controla todos os arquivos gerados

---

## Estrutura do repositório

```
envio-comprovado/
├── mobile/                  ← App Android/iOS (Expo SDK 54)
│   ├── src/
│   │   ├── screens/
│   │   │   ├── CameraScreen.tsx     ← Câmera + gravação + upload
│   │   │   └── ConnectScreen.tsx    ← Configuração de conexão
│   │   └── hooks/
│   │       ├── useShopeeLabel.ts    ← Detecção de etiqueta BR/SPX
│   │       ├── useServerConnection.ts ← Conexão e upload
│   │       └── useSecurity.ts       ← Keychain + autenticação
│   ├── App.tsx
│   ├── app.json
│   └── package.json
└── pc/                      ← Servidor Windows (Python + Flask)
    ├── server.py            ← Flask: recebe e salva vídeos
    ├── launcher.py          ← Interface gráfica (Tkinter)
    ├── BUILD.bat            ← Gera EnvioComprovado.exe
    └── enviocomprovado.spec ← Config PyInstaller
```

---

## Stack técnica

| Componente | Tecnologia |
|-----------|-----------|
| App mobile | React Native + Expo SDK 54 |
| Câmera | expo-camera 16.x |
| Upload | expo-file-system (FOREGROUND) |
| Armazenamento seguro | expo-secure-store (AES-256) |
| Servidor PC | Python 3 + Flask |
| Interface PC | Tkinter |
| Compressão de vídeo | ffmpeg (H.264 CRF23) |
| Detecção de etiqueta | Regex BR/SPX + barcode scanner |

---

## Licença

Código do servidor PC disponibilizado para fins de auditoria e instalação pelos usuários do app.  
O app mobile é um produto comercial — todos os direitos reservados.

---

## Suporte

- 📧 E-mail: [SEU EMAIL AQUI]
- 🌐 Site: [SEU SITE AQUI]

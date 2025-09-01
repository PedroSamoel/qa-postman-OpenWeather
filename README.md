![Postman](https://img.shields.io/badge/Postman-API%20Testing-orange?logo=postman)
![QA](https://img.shields.io/badge/QA-Portfolio-blue)
![OpenWeather](https://img.shields.io/badge/API-OpenWeather-1E90FF)
![Status](https://img.shields.io/badge/Status-Em%20Desenvolvimento-yellow)

# <h1 align="center">Portfólio QA – Testes de API com Postman (OpenWeather v3.0) 👨🏻‍💻

Este projeto integra meu portfólio de **Quality Assurance (QA)** e demonstra o uso do **Postman** para testes de API na **OpenWeather v3.0** (endpoint *One Call*).  
A suíte valida **clima atual**, **previsão horária**, **previsão diária** e **alertas meteorológicos**, além de **casos negativos** (coordenadas inválidas).

## 📌 O que foi feito
- Validação de status code, formato JSON e **SLA** simples
- Checagens de **estrutura e tipos** nos blocos `current`, `hourly`, `daily` e `alerts`
- Verificação de **coerência** entre `lat/lon` do ambiente e do payload (tolerância)
- **Casos negativos**: 400 (coordenadas inválidas) e reconhecimento de 429 (rate limit)
- Organização em pastas temáticas: *Clima Atual*, *Previsão Horária*, *Previsão Diária*, *Alertas Meteorológicos* e *Negativos*

## 🚀 Como usar no Postman
1. Baixe os arquivos em `postman/` deste repositório:
   - Environment: `OpenWeather v3.0 (Publico).postman_environment.json`
   - Collection: `QA Portfolio – OpenWeather v3.0.postman_collection.json`
2. Importe a **Collection** e o **Environment** no Postman.
3. No **Environment**, configure:
   - `apiKey` → sua API key da OpenWeather
   - `base_url` → `https://api.openweathermap.org`
   - `lat`, `lon` → por padrão `-23.55`, `-46.63` (São Paulo) — pode ajustar
   - `units` → `metric` (opções: `metric`, `imperial`, `standard`)
   - `lang` → `pt_br`
   - (opcional para negativo) `invalidLat=999`, `invalidLon=999`
4. Execute as requisições nas pastas:
   - **Clima Atual** (One Call – visão consolidada)
   - **Previsão Horária** (`hourly[]`)
   - **Previsão Diária** (`daily[]`)
   - **Alertas Meteorológicos** (`alerts[]` – pode não existir para a região)
   - **Negativos** (coordenadas inválidas)

## <h1 align="center">🔄 Fluxo dos testes (One Call)

```mermaid
flowchart LR
    A["GET /data/3.0/onecall?lat={lat}&lon={lon} - Clima Atual"]:::get --> B["GET /data/3.0/onecall - Previsão Horária (hourly[])"]:::get
    B --> C["GET /data/3.0/onecall - Previsão Diária (daily[])"]:::get
    C --> D["GET /data/3.0/onecall - Alertas Meteorológicos (alerts[])"]:::get
    A -.-> E["GET /data/3.0/onecall?lat=999&lon=999 - Negativo 400"]:::neg
    A -.-> F["Reconhecer 429 (rate limit) quando ocorrer"]:::neg

classDef get fill:#3b82f6,stroke:#1e3a8a,stroke-width:2px,color:white;
classDef neg fill:#ef4444,stroke:#7f1d1d,stroke-width:2px,color:white;
```

## ✅ Exemplos de validações (resumo)
- **Clima Atual**: `lat/lon` ~ ambiente (tolerância); `current.temp` é numérico; `current.weather[0].description` existe.
- **Previsão Horária**: `hourly[0]` contém chaves `dt`, `temp`, `feels_like`, `pressure`, `humidity`, `wind_speed`, `pop` e `weather[0].description`.
- **Previsão Diária**: `daily[0]` possui `dt`, `temp.min`, `temp.max`, `humidity`, `pressure`, `clouds` e `weather[0].description`.
- **Alertas**: quando `alerts` existe, valida `event`, `description`, `start`, `end`. Se não existir, apenas loga.

## 🧪 Observações técnicas
- A variável da chave de API no **Environment** é `apiKey`.
- Os testes tratam `alerts` como **opcional** (pode não haver fenômenos ativos).
- Para `lat/lon`, utiliza-se **tolerância numérica** para evitar falsos negativos.
- Estrutura pensada para evoluir com **Geocoding** e **Air Pollution** (futuro).

## <h1 align="center">📊 Estatísticas

### 👤 Perfil GitHub
![Pedro's GitHub stats](https://github-readme-stats.vercel.app/api?username=PedroSamoel&show_icons=true&theme=apprentice)
![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=PedroSamoel&layout=compact&theme=apprentice)

---

### 📂 Este Repositório
![Repo size](https://img.shields.io/github/repo-size/PedroSamoel/qa-postman-openweather)
![Stars](https://img.shields.io/github/stars/PedroSamoel/qa-postman-openweather?style=social)
![Forks](https://img.shields.io/github/forks/PedroSamoel/qa-postman-openweather?style=social)
![Last commit](https://img.shields.io/github/last-commit/PedroSamoel/qa-postman-openweather)

---

### <h1 align="center">📈 Gráfico de Contribuições
![GitHub Activity Graph](https://github-readme-activity-graph.vercel.app/graph?username=PedroSamoel&theme=xcode)

<h1 align="center">

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/pedro-samoel/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?logo=github&logoColor=white)](https://github.com/PedroSamoel)
[![Email](https://img.shields.io/badge/Email-D14836?logo=gmail&logoColor=white)](mailto:pedrosamoel.qa@gmail.com)

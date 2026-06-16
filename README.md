# Projeto LangChain4j + Google Gemini

Este é um projeto simples que demonstra a integração do [LangChain4j](https://github.com/langchain4j/langchain4j) com o [Google Gemini](https://ai.google.dev/) utilizando Spring Boot.

O projeto implementa um **Assistente Virtual para uma Locadora Corporativa**, capaz de responder dúvidas informativas e realizar cálculos de cotação de aluguel de veículos através de ferramentas (Function Calling).

## 🚀 Tecnologias

- **Java 25** (conforme configurado no `pom.xml`)
- **Spring Boot 3.5.6**
- **LangChain4j 1.7.1-beta14**
- **Google AI Gemini API**

## ⚙️ Configuração

Para executar este projeto, você precisará de uma chave de API do Google Gemini.

1. Obtenha sua chave em: [Google AI Studio](https://aistudio.google.com/).
2. Defina uma variável de ambiente chamada `GEMINI_API_KEY` com o valor da sua chave:
   ```bash
   # Windows (PowerShell)
   $env:GEMINI_API_KEY="sua_chave_aqui"

   # Linux / macOS
   export GEMINI_API_KEY="sua_chave_aqui"
   ```

A configuração do modelo está presente no arquivo `src/main/resources/application.properties`:
- `gemini.model`: `gemini-2.5-flash`

## 🛠️ Funcionalidades

### 1. AI Service (`AssistantAiService`)
Define o comportamento do assistente. Ele está instruído a responder apenas sobre locação corporativa nas categorias: **economico, suv e premium**.

### 2. Tools (`AssistantTools`)
O assistente possui acesso a uma ferramenta de cálculo de cotação (`calculateQuotation`). Quando o usuário solicita um valor ou preço mencionando categoria e dias, a IA identifica a intenção e executa automaticamente este método Java.

### 3. Controller REST
A interação é feita via endpoint POST:
- **URL**: `http://localhost:8080/api/assistant`
- **Body**: Texto simples (String) com a pergunta do usuário.

## 🏃 Como Executar

1. Certifique-se de ter o Java 25 e o Maven instalados.
2. Clone o repositório.
3. Configure a variável de ambiente `GEMINI_API_KEY`.
4. Execute o comando:
   ```bash
   ./mvnw spring-boot:run
   ```

## 🧪 Exemplo de Uso

Você pode testar a API usando `curl` ou qualquer cliente HTTP:

```bash
curl -X POST http://localhost:8080/api/assistant \
     -H "Content-Type: text/plain" \
     -d "Quanto custa alugar um SUV por 5 dias?"
```

**Resposta esperada:** O assistente calculará o valor usando a `AssistantTools` e retornará a cotação formatada.

---
Projeto desenvolvido para fins de estudo sobre integração de LLMs em aplicações Java.

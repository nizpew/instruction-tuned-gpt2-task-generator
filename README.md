
# 🧠 Gerador de Tarefas com LLM — GPT-2 Ajustado por Instruções

Modelo de linguagem **GPT-2 ajustado (fine-tuning)** para transformar comandos em linguagem natural em **tarefas estruturadas**, disponibilizado por meio de uma **API REST em Flask**.

Este projeto demonstra um pipeline completo de **engenharia de modelos de linguagem**:  
**curadoria de dados → fine-tuning → inferência → disponibilização via API**.

---

## 🎯 Problema

Comandos em linguagem natural são ambíguos e não estruturados, o que dificulta sua integração direta com sistemas de produtividade, agendas ou assistentes virtuais.

Exemplo:
> “me lembre de ligar para o médico”

Como transformar isso em algo que um sistema consiga executar?

---

## 💡 Solução

Este projeto ajusta o modelo **GPT-2** utilizando **dados no formato de instruções**, permitindo que o modelo:

- Entenda a intenção do usuário  
- Gere uma resposta clara  
- Retorne uma **estrutura padronizada de tarefa**, contendo:
  - Nome da tarefa
  - Horário sugerido  

O modelo treinado é servido localmente por meio de uma **API Flask**, pronta para integração com outros sistemas.

---

## 🏗️ Arquitetura do Sistema

```

Prompt do Usuário
↓
Tokenização
↓
GPT-2 Ajustado por Instruções
↓
Saída Estruturada (TASK + TIME)
↓
API REST (Flask)

````

---

## ⚙️ Detalhes Técnicos

- **Modelo base:** GPT-2  
- **Técnica:** Fine-tuning com instruções (instruction tuning)  
- **Frameworks:** PyTorch, Hugging Face Transformers  
- **Serviço:** Flask (API local)  
- **Inferência:** Pipeline local  

---

## 🧪 Exemplo de Uso

### Requisição para a API
```bash
curl -X POST http://localhost:5000/generate \
     -H "Content-Type: application/json" \
     -d '{"prompt": "Crie uma tarefa para ir ao dentista"}'
````

### Resposta Esperada

```json
{
  "response": "Tarefa de consulta no dentista adicionada.\n[TASK: Consulta no dentista | TIME: 10:00]"
}
```

---

## 📂 Conjunto de Dados (Formato de Instrução)

O modelo é treinado com exemplos no seguinte formato:

```json
{
  "text": "Usuário: me lembre de regar as plantas\nAssistente:\nLembrete criado para regar as plantas.\n[TASK: Regar plantas | TIME: 09:00]"
}
```

Esse padrão ensina o modelo a:

* Reconhecer intenções
* Manter consistência na saída
* Sugerir horários coerentes com o contexto da tarefa

---

## 🚀 Funcionamento Interno

1. Curadoria e tokenização de um dataset customizado
2. Ajuste fino do GPT-2 com o `Trainer` da Hugging Face
3. Exportação do modelo treinado
4. Disponibilização via API REST local

---

## 📈 Resultados

* Boa compreensão da intenção do usuário
* Saídas estruturadas consistentes
* Sugestão de horários realistas
* Inferência local estável

---

## 🧠 Por Que Este Projeto É Relevante?

Este repositório vai além do uso básico de LLMs e demonstra:

* Criação de datasets orientados a tarefas reais
* Ajuste fino de modelos de linguagem
* Transformação de texto livre em dados estruturados
* Deploy local pronto para integração

Aplicável a:

* Ferramentas de produtividade
* Agendas inteligentes
* Assistentes virtuais
* Backends conversacionais

---

## 🔍 Exemplo de Inferência Local

```python
from transformers import pipeline

generator = pipeline(
    "text-generation",
    model="./gpt2-tasker",
    tokenizer="./gpt2-tasker"
)

prompt = "Usuário: me lembre de ligar para o médico\nAssistente:\n"
output = generator(prompt, max_length=100, do_sample=True)

print(output[0]["generated_text"])
```

---

## 👤 Sobre Mim

Este projeto faz parte da minha exploração prática em:

* Modelos de Linguagem de Grande Escala (LLMs)
* Instruction tuning
* Curadoria de dados para aplicações reais
* Engenharia de IA com foco em produto

Se você busca alguém que una **engenharia de modelos** com **visão prática de sistemas**, este projeto reflete exatamente isso.

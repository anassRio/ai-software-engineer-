# 01 — LLM Fundamentals

**Goal**: Understand how Large Language Models actually work.  
**Duration**: 2-3 weeks  
**Outcome**: You can explain what an LLM does, its capabilities, limitations, and how to use it effectively

---

## 🎯 Objective

Understand the complete LLM pipeline from first principles:
- Text → tokens → embeddings → transformer → next token prediction
- How inference works (autoregressive generation)
- What different models can/can't do
- Key parameters and their effects
- Cost and latency tradeoffs

You'll move from "LLM is a black box" to "I understand what's happening inside."

---

## 🧠 Core Concepts

### Tokenization
- **Token**: Subword unit (not a word, not a character)
- **Tokenizer**: Algorithm that splits text into tokens
- **Vocabulary**: ~50K-100K tokens for modern LLMs
- **Why**: Fixes variable-length words, enables multilingual support
- **Cost**: Longer token sequence = more compute = more expensive

**Example**:
```
Text: "Hello, world!"
Tokens: ["Hello", ",", "world", "!"]
IDs: [15339, 11, 1917, 0]
```

### Embeddings
- **Embedding**: Vector representation of a token (e.g., 4096 dimensions)
- **Meaning in space**: Semantic relationships encoded in vector space
- **Learned**: Embeddings trained during pretraining
- **Why**: Allows model to work with continuous numbers (not discrete tokens)

**Example**:
```
Token "king" → Embedding [0.2, -0.5, 0.1, ..., 0.8]  (4096 numbers)
Token "queen" → Embedding [0.15, -0.4, 0.12, ..., 0.75]
(Similar vectors because they're related concepts)
```

### Transformer Architecture
- **Transformer**: Neural network architecture (not specific to LLMs)
- **Key innovation**: Self-attention (neurons can look at any position in sequence)
- **Scales better** than older architectures (RNNs, LSTMs)
- **Parallelizable**: Can process entire sequence at once

### Attention Mechanism
- **Self-attention**: Each token "attends to" or looks at other tokens
- **Query, Key, Value**: Three transformations of each token
- **Why**: Model learns what to pay attention to
- **Cost**: O(n²) memory where n = sequence length

**Intuition**:
```
When processing "The bank executive..."
The word "bank" needs to know:
- Am I a river bank or financial bank?
- What words nearby clarify this?
(Attention mechanism "looks" at nearby words)
```

### Multi-Head Attention
- **Multiple attention patterns**: Different "heads" focus on different things
- **Head 1**: Might track pronouns and references
- **Head 2**: Might track semantic relationships
- **Head 3**: Might track syntactic structure
- **Combined**: Richer understanding of relationships

### Positional Encoding
- **Problem**: Attention is permutation-invariant (order-agnostic by default)
- **Solution**: Encode position information into embeddings
- **Types**: Absolute (fixed position), Relative (distance-based), Rotary (modern)
- **Why it matters**: "Dog bites man" vs "Man bites dog" must be different

### Next-Token Prediction
- **Training objective**: Predict next token given all previous tokens
- **Autoregressive**: Generate one token at a time
- **Probability**: Model outputs probability distribution over vocabulary
- **Sampling**: Choose next token from distribution (not deterministic)

**Example**:
```
Prompt: "The quick brown"
Model predicts: P(fox)=0.85, P(dog)=0.10, P(bear)=0.05
We sample → get "fox" (most likely)
Now: "The quick brown fox"
Repeat...
```

### Pretraining vs Instruction Tuning
- **Pretraining**: Unsupervised learning on massive text (predicting next token)
- **Instruction Tuning**: Supervised fine-tuning on human feedback
- **RLHF**: Reinforcement Learning from Human Feedback
- **Why both**: Pretraining = learn language. Tuning = learn to follow instructions.

### Context Window
- **Maximum tokens** the model can process at once
- **GPT-4**: 8K-128K tokens
- **Claude 3**: 200K tokens
- **Llama 2**: 4K tokens
- **Cost**: Longer context = higher latency and cost
- **Limitation**: Can't see beyond context window

### Sampling Parameters (Inference)
- **Temperature**: Randomness (0=deterministic, 1=normal, 2+=very random)
- **top-k**: Only sample from top k most likely tokens
- **top-p**: Only sample from tokens with cumulative probability > p
- **Why**: Control tradeoff between creativity and determinism

### Reasoning Models
- **New capability**: Extended thinking (o1, Gemini 2.0 reasoning mode)
- **How**: Model takes time to "think" before answering
- **When to use**: Complex reasoning, math, coding
- **Cost**: Significantly more expensive (token usage)
- **Speed**: Much slower (by design)

### Hallucinations
- **Problem**: Model generates plausible-sounding but false information
- **Why**: Pattern matching on training data, not genuine understanding
- **When it happens**: Out-of-distribution questions, current events, rare facts
- **Mitigation**: Retrieval-augmented generation (RAG), tools, structured outputs

### Structured Outputs
- **JSON mode**: Force output to be valid JSON
- **Function calling**: Predict function to call instead of free text
- **Why**: Enable deterministic downstream processing
- **Cost**: Slightly higher latency

### Model Capabilities at Different Scales
- **7B parameters**: Good for simple tasks, can run locally
- **13B-70B**: Strong general purpose, good reasoning
- **100B+**: Advanced reasoning, rare knowledge, complex instructions
- **Scaling laws**: Performance improves logarithmically with size

### Token Economics
- **Input tokens**: Cheaper (model reads)
- **Output tokens**: More expensive (model generates)
- **Batch processing**: More efficient than streaming
- **Context**: Longer context window = higher cost

**Example pricing**:
```
GPT-4 Turbo: $0.01 per 1K input, $0.03 per 1K output
Prompt: "Analyze this 50K token document" (input)
Response: 1K token summary (output)
Cost: ($0.01 * 50) + ($0.03 * 1) = $0.53
```

---

## 🗺️ Mental Model: The Complete Pipeline

```
┌──────────────────────────┐
│  Raw Text    │ "Explain quantum computing"
└──────────────┬───────────┘
       ↓
┌──────────────────────────┐
│  Tokenizer   │ "Explain" → [2091], "quantum" → [15339]
└──────────────┬───────────┘
       ↓
┌────────────────────────────────────────────┐
│  Token Embeddings    │ [2091] → [0.1, -0.5, 0.8, ...] (4096 dims)
└──────────────┬───────────────────────────┘
       ↓
┌──────────────────────────────────────────────────────────────────┐
│  Transformer Layers × N          │ Self-attention, feed-forward
│  (12-96 layers depending on size)│ Processing relationships
└──────────────┬───────────────────────────────────────────────┘
       ↓
┌──────────────────────────────────────────┐
│  Output Projection   │ Map hidden state to vocabulary size
└──────────────┬───────────────────────┘
       ↓
┌──────────────────────────┐
│  Softmax             │ Convert to probabilities
└──────────────┬───────────┘
       ↓
┌────────────────────────────────────────────────────────────┐
│  Token Sampling                  │ P(token1)=0.6, P(token2)=0.3, ...
│  (temperature, top-k, top-p)     │ Pick next token
└──────────────┬───────────────────────────────────────┘
       ↓
┌──────────────────────────┐
│  Detokenize         │ [2091, 4534, ...] → "Quantum computing is..."
└──────────────────────┘

Repeat for each output token until <END> or max length
```

---

## 📚 Resources

### Primary (Best Learning Order)
1. **Hugging Face - LLM Course**
   - https://huggingface.co/learn/llm-course/chapter1/1
   - Start here. Clear, structured, code examples
   - Chapters: Intro, Transformer, Tokenization, Fine-tuning, Inference

2. **The Illustrated Transformer** by Jay Alammar
   - https://jalammar.github.io/illustrated-transformer/
   - Best visual explanation of attention mechanism
   - Also read: "Illustrated BERT" by same author

3. **Attention Is All You Need** (Original Paper)
   - https://arxiv.org/abs/1706.03762
   - If you want the academic foundation
   - Skip math proofs, focus on architecture description

### Supplementary
- **Hugging Face Documentation**
  - https://huggingface.co/docs
  - Reference for tokenizers, models, inference

- **LLM Visualization**
  - https://bbycroft.net/llm.html
  - Interactive visualization of transformer layer

---

## 💻 Labs (Hands-On Practice)

Do these in order. Build confidence with LLM APIs progressively.

### Lab 1: Tokenizer Explorer (20 min)
**What you'll build**: Understand tokenization in practice

**Concepts**: Tokens, vocabulary, token IDs, tokenization efficiency

**Steps**:
1. Load a tokenizer (e.g., `tiktoken` for OpenAI models)
2. Tokenize various texts:
   - Simple: "Hello world"
   - Complex: "Quantum computing algorithms leverage superposition"
   - Non-English: "你好世界" (Chinese)
   - Code: `def hello(): print("world")`
3. Count tokens for each
4. Observe:
   - Longer words = more tokens?
   - Numbers = how many tokens?
   - Punctuation = separate token?
   - Non-English = token explosion?
5. Reverse tokenization: token IDs → text

**What you learn**: Tokenization impacts cost and model behavior

**File**: `labs/lab-01-tokenizer.py`

---

### Lab 2: Temperature & Determinism (20 min)
**What you'll build**: Understand sampling parameters

**Concepts**: Temperature, top-k, top-p, deterministic vs random

**Steps**:
1. Use OpenAI or Anthropic API
2. Same prompt, generate 3 responses with:
   - temperature=0 (deterministic)
   - temperature=0.7 (normal)
   - temperature=2.0 (very creative)
3. Compare outputs
4. Try top-k=5, top-p=0.9
5. Observe: Which settings for which use cases?

**Prompt example**:
```
"Write a one-sentence description of a cat."
```

**What you learn**: How to control model creativity

**File**: `labs/lab-02-temperature.py`

---

### Lab 3: Model Comparison (30 min)
**What you'll build**: Compare different models

**Concepts**: Model capabilities, cost-quality tradeoff

**Steps**:
1. Use same prompt across multiple models:
   - GPT-3.5 Turbo
   - GPT-4
   - Claude 3 Haiku
   - Claude 3 Opus
   - Open source (if you want): Mistral, Llama
2. Same prompt to each model (5-10 test prompts)
3. Compare:
   - Quality of responses
   - Speed (latency)
   - Cost (if using APIs)
   - Reasoning depth
4. Create comparison table

**Test prompts**:
- Logic: "If all roses are flowers and some flowers are red, can some roses be not red?"
- Coding: "Write a Python function to find median of unsorted list"
- Creative: "Describe a world where gravity works backwards"
- Knowledge: "What was happening in the world in 1891?"

**What you learn**: Different models have different strengths. Choose right tool for job.

**File**: `labs/lab-03-model-comparison.py`

---

### Lab 4: Context Window Exploration (20 min)
**What you'll build**: Understand context window limitations

**Concepts**: Context window, needle-in-haystack, lost-in-the-middle

**Steps**:
1. Create a long document (10K tokens)
2. Insert a "fact" in the middle
3. Ask model to find the fact with varying context:
   - Fact at start
   - Fact in middle
   - Fact at end
4. Observe: Does position affect retrieval accuracy?
5. Try pushing limits:
   - 50K token document (if using Claude)
   - Does model still find facts?
   - Performance at different positions?

**What you learn**: Context matters, position matters, there are practical limits

**File**: `labs/lab-04-context-window.py`

---

### Lab 5: Structured Output & Function Calling (30 min)
**What you'll build**: Use LLM to make deterministic function calls

**Concepts**: Function calling, structured output, reliability

**Steps**:
1. Define tool schema (JSON):
   ```json
   {
     "type": "function",
     "name": "get_weather",
     "parameters": {
       "type": "object",
       "properties": {
         "city": {"type": "string"},
         "unit": {"enum": ["celsius", "fahrenheit"]}
       },
       "required": ["city"]
     }
   }
   ```
2. Prompt model to use tool:
   ```
   "I want to know the weather in Paris. Use the get_weather function."
   ```
3. Model returns:
   ```json
   {
     "tool": "get_weather",
     "city": "Paris",
     "unit": "celsius"
   }
   ```
4. Execute function, return result
5. Compare:
   - Free text response → messy parsing
   - Function calling → reliable extraction

**What you learn**: Structure beats free text for programmatic use

**File**: `labs/lab-05-function-calling.py`

---

## ✅ Validation Checklist

You've mastered this module when you can:

- [ ] Explain tokenization and why token count matters (cost/speed)
- [ ] Explain next-token prediction (model generates one token at a time)
- [ ] Explain transformer architecture in 2-3 sentences
- [ ] Explain attention mechanism ("model looks at relationships between tokens")
- [ ] Identify when context window is a limitation
- [ ] Explain temperature and when to use it
- [ ] Distinguish between pretraining and instruction tuning
- [ ] Explain why hallucinations happen
- [ ] Know which model to use for which task (small/fast vs large/capable)
- [ ] Explain token economics (input vs output cost)
- [ ] Use function calling to make model output deterministic
- [ ] Build a simple LLM application using an API

---

## 📝 Notes

*Fill this in as you progress:*

- Biggest insights from this module:

- Limitations I discovered:

- Tools/APIs I'm comfortable using:

- Questions for next module (Context Engineering):

---

## 📊 Progress

- [ ] Read Hugging Face LLM Course (Chapters 1-2)
- [ ] Completed Lab 1 (tokenizer explorer)
- [ ] Completed Lab 2 (temperature & sampling)
- [ ] Completed Lab 3 (model comparison)
- [ ] Completed Lab 4 (context window)
- [ ] Completed Lab 5 (function calling)
- [ ] Can explain key concepts to someone else
- [ ] Built a simple LLM application
- [ ] Validation checklist complete

---

## 🎯 Next Steps

When ready for **Module 02 (Context Engineering)**:

✅ You understand how LLMs work (tokenization → transformer → next token)  
✅ You can use LLM APIs effectively  
✅ You know sampling parameters affect output  
✅ You recognize context window limitations  

**Next**: Master the art of structuring context and prompts for reliable agent behavior

---

**Previous**: [00 — AI Fundamentals](../00-fundamentals/)  
**Next**: [02 — Context Engineering](../02-context-engineering/)
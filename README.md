<details>
<summary>LLMs</summary>

- As the number of parameters within a model increases, so does its demand for memory. This expansion not only necessitates more storage but also enhances the model's capability to tackle increasingly complex tasks.

- The input text provided to a Large Language Model (LLM) is referred to as a prompt. The available memory or capacity allocated for this prompt is known as the context window. Generally, the context window can accommodate several thousand words, although its size varies across different models. The text generated by the model is termed a completion, and the process of employing the model to produce text is identified as inference.

### Collection of the Base LLMs
 - GPT
 - BLOOM
 - LLaMa
 - FLAN-T5
 - PaLM 
 - BERT

</details>

<details>
<summary>Transformers</summary>

- Transformers over RNNs: Transformers improve upon RNNs by efficiently processing all words in a sentence simultaneously, enabling better performance in natural language tasks.
- Self-Attention Mechanism: Enables the model to understand the context and relevance of each word in relation to every other word in the input, regardless of their position, significantly enhancing language understanding and generation capabilities.
- Encoder-Decoder Architecture: The transformer model is split into two parts: the encoder, which processes the input text, and the decoder, which generates the output text. These components share a number of similarities and work in conjunction.
- Tokenization: Text must be converted into tokens, representing either whole words or parts of words, which are then used by the model for processing. The choice of tokenizer affects the model's understanding and generation of text.  In general, word are used as tokens.
- Embedding Layer: Maps each token to a high-dimensional vector space, allowing the model to capture the meaning and context of each token. Positional encodings are added to maintain word order. In original transformer paper, the vector size is 512. The vector weights of the embeddings are updated through backpropagation.
- Multi-Headed Self-Attention: A key feature where multiple sets of attention weights (heads) learn different aspects of the language independently. This allows the model to focus on various relationships within the text simultaneously. The weights of the self-attention mechanism—including those for each head are randomly initialized. 
- Feed-Forward Network: Processes the output from the self-attention mechanism, resulting in logits that represent the probability scores for each possible word in the dictionary(tokens). 
- Softmax Layer: Normalizes the logits into a probability distribution over all words in the vocabulary, with the highest probability indicating the most likely next word. 

### Different Types of Transformer Models

1. **Encoder-only Models** (e.g., BERT, RoBERTa)
   - **Use Cases**: Ideal for classification tasks, such as sentiment analysis.
   - **Pre-training Method**: Masked Language Modeling (MLM).
   - **Objective**: Denoising objective to predict masked tokens and reconstruct the original sentence.
   - **Features**: Builds bi-directional representations of the input sequence, understanding the full context around each token.

2. **Encoder-decoder Models** (e.g., BART, T5)
   - **Use Cases**: Suitable for sequence-to-sequence tasks like translation, summarization, and question-answering.
   - **Pre-training Method**: Span Corruption.
   - **Objective**: The encoder masks random sequences of input tokens replaced by a unique Sentinel token. The decoder's task is to reconstruct the masked token sequences auto-regressively.
   - **Features**: Utilizes both the encoder and decoder components of the original transformer architecture. Sentinel tokens do not correspond to any actual word but are placeholders for masked sequences.

3. **Decoder-only Models** (e.g., GPT series, BLOOM, Jurassic, LLaMA)
   - **Use Cases**: Primarily used for text generation. Larger models demonstrate strong zero-shot inference abilities for a range of tasks.
   - **Pre-training Method**: Causal Language Modeling.
   - **Objective**: Predict the next token based on the previous sequence of tokens, focusing on autoregressive training.
   - **Features**: Employs the decoder component of the original architecture, enabling unidirectional context. Models are trained to build a statistical representation of language by learning to predict the next word.

### End-to-end process of the transformers (Translation)

1. Tokenization of input words with the same tokenizer used in network training.
2. Tokens fed into the encoder, passing through the embedding layer and multi-headed attention layers.
3. Encoder outputs, a deep representation of the input sequence's structure and meaning, fed into the decoder.
4. Start of sequence token triggers the decoder to predict the next token, based on encoder-provided context.
5. Decoder outputs pass through its feed-forward network and softmax output layer to predict tokens until an end-of-sequence token is reached.
6. The process concludes with detokenizing the final sequence of tokens into the output sentence.

</details>

<details>
<summary>Prompt Engineering</summary>

## Main Points

### Key Terms:
- **Prompt**: Input text for the model.
- **Inference**: Generating text with the model.
- **Completion**: The model's output text.
- **Context Window**: Memory limit for the prompt.

### Prompt Engineering:
Refining the prompt to improve outcomes, utilizing strategies like in-context learning to guide the model with examples.

### Inference Types:
- **Zero-Shot**: No examples given; larger models often excel.
- **One-Shot/Few-Shot**: Including one or a few examples to help smaller models grasp and perform tasks.

### Model Performance:
Performance varies with model size; larger models better generalize tasks through zero-shot inference, while smaller models might need more specific guidance. When adding examples doesn't suffice, consider fine-tuning the model with additional data.

### Choosing a Model:
Test different models to find the right fit for your task, and adjust settings to fine-tune completions.

## Methods and Configuration Parameters for Next-Word Generation:

- **Configuration Parameters (at inference time)**: Influence output by controlling aspects like the maximum number of tokens and creativity.
  - Examples include limiting the number of tokens (max new tokens) and adjusting the output's creativity.

- **Max New Tokens**: Sets a limit on how many tokens the model will generate, effectively capping the output length.

- **Softmax Layer Output**: Represents a probability distribution across all possible words, guiding the model in next-word selection.

### Decoding Strategies:

- **Greedy Decoding**: Chooses the highest probability word each time. Simple but prone to repetition.

- **Random Sampling**: Introduces variability by selecting words based on their probability, reducing repetitiveness but may lead to off-topic generations.

- **Top K Sampling**: Limits selection to the top K most probable tokens, balancing randomness and sensibility.

- **Top P Sampling (Nucleus Sampling)**: Chooses from a subset of tokens whose cumulative probability is under a threshold (P), aiming for sensible yet varied output.

- **Temperature**: Adjusts the probability distribution's shape to control randomness. Higher temperatures increase randomness, while lower temperatures make choices more predictable.

### Key Points for configuration of inference:

- Different methods and parameters allow for fine-tuning the model's behavior during text generation, balancing between creativity and coherence.
- Parameters like `max new tokens`, sampling strategies (`top k`, `top p`), and `temperature` provide tools to adjust the model's output during inference.
- The choice of strategy and parameter settings can significantly influence the model's output quality and relevance to the task at hand.

</details>

<details>
<summary>Generative AI Project Lifecycle</summary>

- Consider choosing between using pre-existing models or pre-training custom models.
- Guidance on model customization and fine-tuning for specific data or tasks.

### 1. Define the Scope
- **Crucial Step**: Narrowly and accurately define the project scope.
- **Model Considerations**: Decide the function of the LLM based on the task complexity and specificity.

### 2. Choose Your Model
- **Decision Point**: Opt between training a model from scratch or leveraging an existing model.
- **Feasibility Assessment**: Considerations and rules of thumb for model training or adaptation will be discussed.

### 3. Assess and Train
- **Performance Assessment**: Evaluate the model's initial performance for your specific use case.
- **Prompt Engineering vs. Fine-Tuning**: Start with in-context learning; move to fine-tuning if necessary.

### 4. Adapt and Align
- **Behavioral Alignment**: Ensure the model's outputs align with human preferences using techniques like reinforcement learning with human feedback.
- **Iterative Evaluation**: Continuously evaluate and adjust model performance and alignment through iterative training and prompt engineering.

### 5. Deployment
- **Integration and Optimization**: Deploy the optimized model within your application infrastructure for efficient use of compute resources.
- **User Experience**: Focus on providing the best possible experience for application users.

### 6. Address Limitations
- **Overcoming LLM Limitations**: Learn techniques to mitigate inherent LLM challenges, like inventing information or limited reasoning capabilities.

### Model Selection and Evaluation:

- Exploration of the various large language model options available, both open-source and proprietary.
- Criteria for evaluating and selecting the most suitable model for a project's needs.

### Model Size and Capability:

- Discussion on the relationship between model size (e.g., parameter count) and its capabilities.
- Insights into when large models are necessary versus when smaller models can be equally effective.
- Examples of specific use cases that may not require the largest models for successful implementation.

</details>

<details>
<summary>Computational Challenges</summary>

Training Large Language Models (LLMs) is highly memory-intensive. Efficient memory management is crucial due to the massive number of parameters involved. This document summarizes the key aspects of memory requirements and strategies for optimizing memory usage during the training of LLMs.

### Memory Requirements for LLMs

- **Storing Model Weights**: A single parameter in a model, represented as a 32-bit float, requires four bytes of memory. Consequently, storing one billion parameters necessitates approximately 4 GB of GPU RAM just for the model weights.

### Additional Memory Needs During Training

- **Training Overheads**: Additional components such as the Adam optimizer states, gradients, activations, and temporary variables significantly increase memory requirements. For a one billion parameter model, the memory needed can be approximately 24 GB of GPU RAM, which is about 6 times the memory required just for storing the model weights.

### Quantization: A Strategy to Reduce Memory Usage

- **What is Quantization?**: Quantization involves reducing the precision of the model weights from 32-bit floating-point numbers to lower precision formats like 16-bit (FP16 or BFLOAT16) or even 8-bit integers (int8). This reduces the memory footprint significantly.

- **FP32 vs. FP16 vs. BFLOAT16**:
  - **FP32 (32-bit Full Precision)**: Uses 1 bit for the sign, 8 bits for the exponent, and 23 bits for the fraction (mantissa).
  - **FP16 (16-bit Half Precision)**: Reduces the exponent to 5 bits and the fraction to 10 bits, cutting the memory requirement in half compared to FP32.
  - **BFLOAT16**: Maintains the 8-bit exponent of FP32 but reduces the fraction to 7 bits, offering a balance between dynamic range and memory efficiency.

### Challenges with Large Models

- **Scaling Challenges**: As model sizes reach tens or hundreds of billions of parameters, memory requirements become vast, necessitating distributed computing across multiple GPUs.

### Fine-tuning Large Models

- **Memory Considerations**: Fine-tuning involves adjusting pre-trained model parameters for specific tasks, which also demands substantial memory, though less than training from scratch.

</details>

<details>
<summary>Scaling Laws</summary>
# Exploring Model Size, Training Configuration, and Performance

Understanding the relationship between model size, training configuration, and performance is essential for optimizing the training of large language models (LLMs). This section outlines key research findings and concepts relevant to the development and optimization of LLMs.

## Key Concepts and Measures

### Compute Budget
- **Definition**: A critical constraint that includes factors such as the number of GPUs available and the time allocated for model training.
- **Impact**: Determines the scale and feasibility of model training efforts.

### PetaFLOP per Second Day
- **Definition**: A unit measuring the computational resources required, equivalent to one quadrillion floating-point operations per second across a full day.
- **Equivalence**: Roughly corresponds to the output of eight NVIDIA V100 GPUs or two NVIDIA A100 GPUs operating at full efficiency for one day.

## Model Training Insights

### Dataset vs. Model Parameters
- Increasing the size of the training dataset or the number of model parameters can improve performance, within the constraints of the available compute budget.

### Compute Resources for Pre-training
- **Example**: Training large models like GPT-3 (175 billion parameters) necessitates substantial compute resources, approximately 3,700 petaFLOP per second days, in contrast to 100 for T5 XL (3 billion parameters).

### Trade-offs
- Research shows well-defined relationships between dataset size, model size, and compute budget, with performance improvements following a power-law relationship with the compute budget.

## Findings from the Chinchilla Paper

### Overparameterization
- Models like GPT-3 may have more parameters than necessary ("overparameterized") and could benefit from larger training datasets ("undertrained").

### Optimal Training Dataset Size
- **Rule of Thumb**: The optimal size is about 20 times the number of model parameters. For a model with 70 billion parameters, the ideal dataset contains 1.4 trillion tokens.

### Compute Optimal Models
- Smaller models trained on larger datasets can achieve comparable or better performance than larger models trained less optimally.

</details>

---
sidebar_position: 1
---

# GenAI Models Comparison

## Introduction

Amazon Bedrock brings together, through a single API, a variety of high-performance foundation models (FMs) from different vendors. This platform allows you to create generative AI applications with security, privacy, and responsibility, enabling integration with the entire AWS ecosystem. In this document, we present a detailed analysis of the available models—including all identified versions for each vendor—and offer expanded descriptions, pros, cons, and practical cost examples.

The analyzed vendors are:

- **Anthropic** (Claude family, with versions including *Instant*, *2.x*, and various *Claude 3* variants—Sonnet, Haiku, Opus)
- **Meta** (Llama family, including the Llama 3.3, 3.2, 3.1 series, Llama 3, and Llama 2 Chat)
- **DeepSeek** (DeepSeek R-1 model)
- **Amazon** (Titan models for text, code, and chat tasks, in addition to Nova models for text and image generation)

Billing is based on token usage for text models (input and output) and, for image models, per generated image or applied resolution.

---

## Pricing Structure

The prices shown refer to the charge per 1,000 tokens for text models or, in the case of image models, the cost per image/resolution. These prices may vary by region, usage volume, and inference mode (on-demand, batch, or provisioned throughput).

---

## 1. Anthropic

Anthropic’s models are known for their focus on safety and responsibility, offering various versions of the Claude family to meet diverse performance and latency requirements.

### Models and Context

- **Claude Instant**  
  Focused on providing fast responses with low latency, ideal for applications requiring real-time interactions such as chatbots and virtual assistants.  
  **Pros:**  
  - Near-instant responses  
  - Low latency for dynamic interactions  
  **Cons:**  
  - May be less robust in complex conversational contexts

- **Claude 2.0 / 2.1**  
  Intermediate versions that improve contextual understanding and response quality, maintaining a good balance between speed and performance.  
  **Pros:**  
  - Better context and nuance comprehension  
  - Suitable for more elaborate dialogues  
  **Cons:**  
  - Slightly higher costs compared to the Instant model

- **Claude 3 – Sonnet, Haiku, and Opus Variants**  
  These variants represent the new generation of the Claude family, where:  
  - **Sonnet (3.7 and 3.5):** Optimized to provide responses with high coherence and robustness, ideal for applications requiring accuracy without sacrificing speed.  
  - **Haiku:** Focused on scenarios where token economy is crucial, maintaining excellent cost-effectiveness.  
  - **Opus:** Offers maximum performance, indicated for critical use cases that demand the highest possible quality, although at a higher cost.  
  **General Pros (Claude 3):**  
  - High performance in language understanding and generation  
  - Multiple versions let you adjust the application based on cost and latency requirements  
  **General Cons (Claude 3):**  
  - More robust versions (like Opus) can be expensive for high-volume applications  
  - Availability of specific versions may vary by region

### Price Table (per 1,000 tokens)

| Model                      | Price (Input) | Price (Output) |
|----------------------------|---------------|----------------|
| Claude Instant             | USD 0.0008    | USD 0.0024     |
| Claude 2.0 / 2.1           | USD 0.008     | USD 0.024      |
| Claude 3.7 Sonnet          | USD 0.003     | USD 0.015      |
| Claude 3.5 Sonnet          | USD 0.003     | USD 0.015      |
| Claude 3.5 Haiku           | USD 0.0008    | USD 0.0040     |
| Claude 3 Haiku             | USD 0.00025   | USD 0.00125    |
| Claude 3 Sonnet            | USD 0.003     | USD 0.015      |
| Claude 3 Opus              | USD 0.015     | USD 0.075      |

---

## 2. Meta

Meta’s models, in the Llama family, are known for their open-source nature and high customization, catering to a wide range of applications—from conversational systems to large-scale natural language processing tasks.

### Models and Context

- **Llama 3.3 Instruct (70B)**  
  A high-capacity model designed for complex instructions and tasks that require deep understanding, ideal for systems demanding elaborate answers.  
  **Pros:**  
  - Excellent for complex tasks  
  - High precision and robustness  
  **Cons:**  
  - Requires robust infrastructure to operate

- **Llama 3.2 Instruct (1B, 3B, 11B, and 90B)**  
  A series offering different sizes, enabling you to choose based on the desired balance of cost, speed, and accuracy. Smaller models (1B and 3B) are ideal for resource-constrained applications, while larger ones (11B and 90B) serve more demanding needs.  
  **Pros:**  
  - Flexibility for various use cases  
  - Lower cost on smaller models  
  **Cons:**  
  - Larger models may require greater expertise and infrastructure

- **Llama 3.1 Instruct (8B, 70B, 405B)**  
  Offers intermediate and advanced options, with the 405B version being one of the largest, suitable for high-performance tasks.  
  **Pros:**  
  - Broad range of models to meet diverse needs  
  **Cons:**  
  - Configuration and fine-tuning can be complex

- **Llama 3 Instruct (8B and 70B)**  
  Versions optimized for instructions, focused on providing accurate answers with low response time.  
  **Pros:**  
  - Good balance of performance and cost for instructional tasks  
  **Cons:**  
  - Less flexibility compared to the Llama 3.2 and 3.1 series for certain applications

- **Llama 2 Chat (13B and 70B)**  
  Models specifically optimized for conversational applications, enabling natural and coherent interactions in chat systems and virtual assistants.  
  **Pros:**  
  - Excellent for customer support and chatbots  
  - Low latency and good adaptability  
  **Cons:**  
  - Limited in non-conversational tasks compared to instructional models

### Price Table (per 1,000 tokens)

| Model                               | Price (Input) | Price (Output) |
|-------------------------------------|---------------|----------------|
| Llama 3.3 Instruct (70B)            | USD 0.00072   | USD 0.00072    |
| Llama 3.2 Instruct (1B)             | USD 0.00010   | USD 0.00010    |
| Llama 3.2 Instruct (3B)             | USD 0.00015   | USD 0.00015    |
| Llama 3.2 Instruct (11B)            | USD 0.00016   | USD 0.00016    |
| Llama 3.2 Instruct (90B)            | USD 0.00072   | USD 0.00072    |
| Llama 3.1 Instruct (8B)             | USD 0.00022   | USD 0.00022    |
| Llama 3.1 Instruct (70B)            | USD 0.00072   | USD 0.00072    |
| Llama 3.1 Instruct (405B)           | USD 0.00240   | USD 0.00240    |
| Llama 3 Instruct (8B)               | USD 0.00030   | USD 0.00060    |
| Llama 3 Instruct (70B)              | USD 0.00265   | USD 0.00350    |
| Llama 2 Chat (13B)                  | USD 0.00075   | USD 0.00100    |
| Llama 2 Chat (70B)                  | USD 0.00195   | USD 0.00256    |

---

## 3. DeepSeek

DeepSeek provides a model focused on efficiency for query processing and data analysis. This model is designed to deliver fast answers in scenarios where agility in information analysis is crucial.

### Model and Context

- **DeepSeek R-1**  
  Ideal for applications that need fast query processing and analysis of large volumes of data.  
  **Pros:**  
  - High efficiency in executing complex queries  
  - Good balance of cost and performance for analytics  
  **Cons:**  
  - Less support and community compared to major players  
  - Updates may occur less frequently

### Price Table (per 1,000 tokens)

| Model           | Price (Input) | Price (Output) |
|-----------------|---------------|----------------|
| DeepSeek R-1    | USD 0.00135   | USD 0.00540    |

---

## 4. Amazon

Amazon provides two sets of models: **Titan**, focused on text, code, and chat applications, and **Nova**, which cover both text generation and image creation. These models are natively integrated with the AWS ecosystem, allowing for scalability and cost optimization as demand grows.

### 4.1. Amazon Titan Models

#### Context and Description

- **Titan Text**  
  Optimized for natural language processing and generation, Titan Text is suitable for a wide range of tasks, from content creation to text analysis.  
  **Pros:**  
  - High-quality text generation  
  - Smooth integration with other AWS services  
  **Cons:**  
  - May require careful cost analysis for high-volume applications

- **Titan Code**  
  Focused on helping developers generate and correct code, providing intelligent suggestions and optimizations during development.  
  **Pros:**  
  - Specialized for programming tasks  
  - Reduces development time with code suggestions  
  **Cons:**  
  - May be limited in non-programming tasks

- **Titan Chat**  
  A variant optimized for conversational interactions, ideal for customer service and virtual assistants.  
  **Pros:**  
  - Fast, contextualized answers  
  - Suitable for support and chatbot applications  
  **Cons:**  
  - Performance may vary with dialogue complexity

- **Titan V2 (Text Ingestor)**  
  A solution geared toward ingesting and processing large volumes of input tokens at very low costs, serving as the foundation for applications that require massive text data reading and processing.

#### Price Table (per 1,000 tokens)

| Model                                | Price (Input) | Price (Output) |
|--------------------------------------|---------------|----------------|
| Titan Text                           | USD 0.0025    | USD 0.0050     |
| Titan Code                           | USD 0.0030    | USD 0.0060     |
| Titan Chat                           | USD 0.0028    | USD 0.0056     |
| Titan V2 (Text Ingestor)            | USD 0.00002   | N/A            |

### 4.2. Amazon Nova Models

#### For Text Generation

- **Nova Micro, Nova Lite, Nova Pro, and Nova Pro (optimized latency)**  
  These models vary according to capacity and latency optimization. They are recommended for applications that require rapid text generation with different balances of cost and performance.

| Model                         | Price (Input) | Price (Output) |
|-------------------------------|---------------|----------------|
| Nova Micro                    | USD 0.000035  | USD 0.000140   |
| Nova Lite                     | USD 0.000060  | USD 0.000240   |
| Nova Pro                      | USD 0.000800  | USD 0.003200   |
| Nova Pro (optimized latency)  | USD 0.001000  | –              |

#### For Image Generation

- **Nova Canvas**  
  Focused on image generation, Nova Canvas is available in different resolutions and qualities (Standard and Premium), enabling the creation of visual content according to the application’s requirements.

| Model       | Resolution         | Price per Image                               |
|------------|--------------------|-----------------------------------------------|
| Nova Canvas | Up to 1,024 x 1,024 | Standard: USD 0.04 / Premium: USD 0.06         |
| Nova Canvas | Up to 2,048 x 2,048 | Standard: USD 0.06 / Premium: USD 0.08         |

#### General Pros and Cons – Amazon

**Pros:**
- Native integration with the AWS ecosystem, simplifying scalability and connections to other services  
- Variety of models catering to both text and visual needs  
- Robust infrastructure and specialized technical support, ensuring high availability and reliability  

**Cons:**
- The pricing structure can be complex, requiring detailed analysis for cost optimization  
- Some variants may need additional configurations or throughput commitments to achieve ideal performance

---

## Cost Examples

To illustrate the financial impact in practical scenarios, consider the following examples:

1. **Text Summary with Titan Text Lite:**  
   A developer makes API calls to summarize text using the Titan Text Lite model. Suppose the summary involves an input of 2,000 tokens and generates an output of 1,000 tokens:  
   - **Hourly cost calculation:**  
     - Input: (2,000 tokens / 1,000) × USD 0.0003 = USD 0.0006  
     - Output: (1,000 tokens / 1,000) × USD 0.0004 = USD 0.0004  
     - **Total cost per hour = USD 0.0006 + USD 0.0004 = USD 0.001**

2. **Image Generation with Titan’s Image Generator:**  
   A developer requests 1,000 images of 1,024 x 1,024 pixels in standard quality, at a cost of USD 0.01 per image:  
   - **Total cost = 1,000 images × USD 0.01 = USD 10**

These examples demonstrate how costs can vary depending on the volume of processed tokens or the number of generated images, allowing a more precise evaluation of the financial impact for each application.

---

## Final Considerations

When choosing the ideal generative AI model on Amazon Bedrock, it is essential to consider:

- **Cost vs. Performance:**  
  Evaluate the volume of tokens (or images) your application will consume and determine which model offers the best balance of quality, speed, and cost.

- **Use Case:**  
  Models optimized for dialogues (such as Claude Instant or Titan Chat) may be more suitable for conversational applications, while models like Titan Code or more robust variants of the Llama family may be ideal for technical or data analysis tasks.

- **Integration and Support:**  
  Amazon’s native solutions offer simpler integration with other AWS services, while partner models (Anthropic, Meta, and DeepSeek) provide greater flexibility and customization options.

The cost examples provided show how practical model usage can impact the application’s budget, highlighting the importance of a detailed analysis before implementation.
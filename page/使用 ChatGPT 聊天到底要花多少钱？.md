OpenAI 在 6 月 13 日进行了大规模降价和升级，text-embedding-ada-002 降价 95%，GPT-3.5-turbo 降价 25%，GPT-4 最高支持 32K 文本。本文将带你详细了解 ChatGPT 的价格计算方式，以及如何最大化利用 OpenAI 提供的服务。

## ChatGPT 的价格计算方式

在 OpenAI 的官网上，对 ChatGPT 的价格计算方式有详细说明（以 token 为单位）。我们来具体算算现在的价格实际是多少。

### 官网聊天

官方网页上的聊天功能是免费的，收费项目主要针对 API 用户。每个 API 用户默认会赠送 5 美元额度。

### 大语言模型的价格计算

#### 计算方法

OpenAI 提供了一个示例：  
> Multiple models, each with different capabilities and price points. Prices are per 1,000 tokens. You can think of tokens as pieces of words, where 1,000 tokens is about 750 words. This paragraph is 35 tokens.

官方示例中提到，这段文字的长度为 35 个 tokens。ChatGPT 使用的分词算法是 Byte-Pair Encoding (BPE)。以下是几种常见的 token 计算方法：

1. **Transformers**  
2. **OpenAI tiktoken**  
3. **单词数 ÷ 0.75**

以下是使用代码计算 tokens 的示例：

python
def get_transformers_tokens(text: str, encoding_name: str) -> int:
    tokenizer = transformers.AutoTokenizer.from_pretrained(encoding_name)
    tokens = tokenizer.tokenize(text)
    return len(tokens)


python
def get_tiktoken_tokens(text: str, encoding_name: str) -> int:
    encoding = tiktoken.get_encoding(encoding_name)
    return len(encoding.encode(text))


通过以上方法计算，得到的 tokens 值为 45，而 OpenAI 官方网页中给出的值是 35。不过，使用 OpenAI 官方的 [token 计算器](https://bit.ly/bewildcard) 计算，结果也是 45。

#### tokens 消耗的影响因素

tokens 的消耗主要受到以下三个因素的影响：

1. **System Prompt**：聊天的背景信息，通常由软件自动处理，用户不可见。  
2. **User Prompt**：用户的提问。  
3. **AI's Reply**：ChatGPT 的回答。

以下是一个示例代码，用于计算 ChatGPT 的 tokens 消耗：

python
import transformers

# 加载 ChatGPT 的分词器
tokenizer = transformers.AutoTokenizer.from_pretrained("EleutherAI/gpt-neo-2.7B")

# 示例文本
text = "Hello, how are you?"
tokens = tokenizer.tokenize(text)

# 计算 tokens 数量
num_tokens = len(tokens)
print("Number of tokens:", num_tokens)


### 不同模型的价格

#### ChatGPT 3.5

| 模型         | 输入价格（每 1K tokens） | 输出价格（每 1K tokens） |
|--------------|--------------------------|--------------------------|
| 4K context   | $0.0015                  | $0.002                   |
| 16K context  | $0.003                   | $0.004                   |

以 5 美元为例，用户大约可以进行 6887 次对话（以英文为例，中文对话可能会有所不同）。

#### GPT-4

| 模型         | 输入价格（每 1K tokens） | 输出价格（每 1K tokens） |
|--------------|--------------------------|--------------------------|
| 8K context   | $0.03                    | $0.06                    |
| 32K context  | $0.06                    | $0.12                    |

#### InstructGPT

| 模型    | 价格（每 1K tokens） |
|---------|-----------------------|
| Ada     | $0.0004              |
| Babbage | $0.0005              |
| Curie   | $0.0020              |
| Davinci | $0.0200              |

#### Fine-tuning 模型

| 模型    | 训练价格（每 1K tokens） | 使用价格（每 1K tokens） |
|---------|--------------------------|--------------------------|
| Ada     | $0.0004                  | $0.0016                  |
| Babbage | $0.0006                  | $0.0024                  |
| Curie   | $0.0030                  | $0.0120                  |
| Davinci | $0.0300                  | $0.1200                  |

#### Embedding 模型

| 模型      | 使用价格（每 1K tokens） |
|-----------|--------------------------|
| Ada v2    | $0.0001                  |
| Ada v1    | $0.0040                  |
| Babbage v1| $0.0050                  |
| Curie v1  | $0.0200                  |
| Davinci v1| $0.2000                  |

### 其他模型

#### 图像模型

| 分辨率      | 价格（每张图片） |
|-------------|------------------|
| 1024×1024   | $0.020           |
| 512×512     | $0.018           |
| 256×256     | $0.016           |

#### 音频模型

| 模型    | 使用价格（每分钟） |
|---------|--------------------|
| Whisper | $0.006             |

## 总结

虽然 OpenAI 提供了 token 计算工具，但工具的计算值与官方网页中的说明可能存在差异。以 ChatGPT 3.5 为例，账号自带的 5 美元额度，大约可以进行 6000 多次对话。

想深入理解 token 和分词的原理，还需要进一步学习相关概念。

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)
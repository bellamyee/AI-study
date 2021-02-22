Recent Trends Transformer

• Transformer model and its self-attention block has become a general-purpose sequence (or
set) encoder and decoder in recent NLP applications as well as in other areas.
• Training deeply stacked Transformer models via a self-supervised learning framework has
significantly advanced various NLP tasks through transfer learning, e.g., BERT, GPT-3, XLNet,
ALBERT, RoBERTa, Reformer, T5, ELECTRA…
• Other applications are fast adopting the self-attention and Transformer architecture as well as
self-supervised learning approach, e.g., recommender systems, drug discovery, computer
vision, …
• As for natural language generation, self-attention models still requires a greedy decoding of
words one at a time.
Attention Is All You Need, NeurIPS’17

ⓒ NAVER Connect Foundation
GPT-1
4
ⓒ NAVER Connect Foundation
Improving Language Understanding by Generative Pre-training
5
• GPT-1
• It introduces special tokens, such as <S> /<E>/ $, to achieve effective transfer learning
during fine-tuning
• It does not need to use additional task-specific architectures on top of transferred
representations
• 12-layer decoder-only transformer
• 12 head / 768 dimensional states
• GELU activation unit
https://blog.openai.com/language-unsupervised/
ⓒ NAVER Connect Foundation 6
• Experimental Results
Improving Language Understanding by Generative Pre-training
https://blog.openai.com/language-unsupervised/
ⓒ NAVER Connect Foundation
BERT
7
ⓒ NAVER Connect Foundation 8
• Learn through masked language modeling task
• Use large-scale data and large-scale model
BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding
Unidirectional Bi-LSTM
BERT: Pre-training of deep bidirectional transformers for language understanding, NAACL’19
ⓒ NAVER Connect Foundation 9
• Motivation
• Language models only use left context or right context, but language understanding is bidirectional
• If we use bi-directional language model?
• Problem: Words can “see themselves” (cheating) in a bi-directional encoder
Masked Language Model
ⓒ NAVER Connect Foundation 10
• Masked Language Model (MLM)
– Mask some percentage of the input tokens at random, and then predict those masked
tokens.
– 15% of the words to predict
• 80% of the time, replace with [MASK]
• 10% of the time, replace with a random word
• 10% of the time, keep the sentence as same
• Next Sentence Prediction (NSP)
– Predict whether Sentence B is an actual sentence that proceeds Sentence A, or a random
sentence
Pre-training Tasks in BERT
https://nlp.stanford.edu/seminar/details/jdevlin.pdf
ⓒ NAVER Connect Foundation 11
• How to
• Mask out k% of the input words, and then predict the masked words
• e.g., use k= 15%
• Too little masking : Too expensive to train
• Too much masking : Not enough to capture context
Pre-training Tasks in BERT: Masked Language Model
https://nlp.stanford.edu/seminar/details/jdevlin.pdf
ⓒ NAVER Connect Foundation 12
• Problem
• Mask token never seen during fine-tuning
• Solution
• 15% of the words to predict, but don’t replace with [MASK] 100% of the time. Instead:
• 80% of the time, replace with [MASK]
– went to the store → went to the [MASK]
• 10% of the time, replace with a random word
– went to the store → went to the running
• 10% of the time, keep the same sentence
– went to the store → went to the store
Pre-training Tasks in BERT: Masked Language Model
ⓒ NAVER Connect Foundation 13
• To learn the relationships among sentences, predict whether Sentence B is an actual
sentence that proceeds Sentence A, or a random sentence
Pre-training Tasks in BERT: Next Sentence Prediction
https://nlp.stanford.edu/seminar/details/jdevlin.pdf
ⓒ NAVER Connect Foundation 14
1. Model Architecture
– BERT BASE: L = 12, H = 768, A = 12
– BERT LARGE: L = 24, H = 1024, A = 16
2. Input Representation
– WordPiece embeddings (30,000 WordPiece)
– Learned positional embedding
– [CLS] – Classification embedding
– Packed sentence embedding [SEP]
– Segment Embedding
3. Pre-training Tasks
– Masked LM
– Next Sentence Prediction
BERT Summary
ⓒ NAVER Connect Foundation
Transformer: Positional Encoding Transformer
15
• Use sinusoidal functions of different frequencies
𝑃𝐸(𝑝𝑜𝑠,2𝑖) = sin(𝑝𝑜𝑠/100002𝑖/𝑑𝑚𝑜𝑑𝑒𝑙)
𝑃𝐸(𝑝𝑜𝑠,2𝑖+1) = cos(𝑝𝑜𝑠/100002𝑖/𝑑𝑚𝑜𝑑𝑒𝑙)
• Easily learn to attend by relative position, since for any fixed offset 𝑘,
𝑃𝐸(𝑝𝑜𝑠+𝑘) can be represented as linear function of 𝑃𝐸 𝑝𝑜𝑠
http://nlp.seas.harvard.edu/2018/04/03/attention
ⓒ NAVER Connect Foundation 16
BERT: Input Representation
BERT: Pre-training of deep bidirectional transformers for language understanding, NAACL’19
• The input embedding is the sum of the token embeddings, the segmentation embeddings
and the position embeddings
ⓒ NAVER Connect Foundation 17
• Learn through masked language modeling task
• Use large-scale data and large-scale model
BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding
Unidirectional Bi-LSTM
BERT: Pre-training of deep bidirectional transformers for language understanding, NAACL’19
ⓒ NAVER Connect Foundation 18
BERT: Fine-tuning Process
BERT: Pre-training of deep bidirectional transformers for language understanding, NAACL’19
• Transfer Learning
https://blog.openai.com/language-unsupervised/
ⓒ NAVER Connect Foundation 19
BERT vs GPT-1
• Comparison of BERT and GPT-1
• Training-data size
• GPT is trained on BookCorpus(800M words) ; BERT is trained on the BookCorpus and
Wikipedia (2,500M words)
• Training special tokens during training
• BERT learns [SEP],[CLS], and sentence A/B embedding during pre-training
• Batch size
• BERT – 128,000 words ; GPT – 32,000 words
• Task-specific fine-tuning
• GPT uses the same learning rate of 5e-5 for all fine-tuning experiments; BERT
chooses a task-specific fine-tuning learning rate.
ⓒ NAVER Connect Foundation 20
BERT: GLUE Benchmark Results
• GLUE Benchmark Results
BERT: Pre-training of deep bidirectional transformers for language understanding, NAACL’19
ⓒ NAVER Connect Foundation 21
Machine Reading Comprehension (MRC), Question Answering
ⓒ NAVER Connect Foundation 22
BERT: SQuAD 1.1
Only new parameters: Start vector and end vector
https://rajpurkar.github.io/SQuAD-explorer/
ⓒ NAVER Connect Foundation 23
BERT: SQuAD 2.0
• Use token 0 ([CLS]) to emit logit for “no answer”
• “No answer” directly competes with answer span
• Threshold is optimized on dev set
https://rajpurkar.github.io/SQuAD-explorer/
ⓒ NAVER Connect Foundation 24
BERT: On SWAG
• Run each Premise + Ending through BERT
• Produce logit for each pair on token 0 ([CLS])
https://leaderboard.allenai.org/swag/submissions/public
ⓒ NAVER Connect Foundation 25
BERT: Ablation Study
• Big models help a lot
• Going from 110M to 340M params helps even on datasets with 3,600 labeled
examples
• Improvements have not asymptoted
BERT: Pre-training of deep bidirectional transformers for language understanding, NAACL’19
ⓒ NAVER Connect Foundation
2.
Advanced Self-supervised Pre-training Models
26
GPT-2
GPT-3
ALBERT
ELECTRA
Light-weight Models
Fusing Knowledge Graph into Language Model
ⓒ NAVER Connect Foundation
GPT-2
27
ⓒ NAVER Connect Foundation 28
GPT-2: Language Models are Unsupervised Multi-task Learners
• Just a really big transformer LM
• Trained on 40GB of text
• Quite a bit of effort going into making sure the dataset is good quality
• Take webpages from reddit links with high karma
• Language model can perform down-stream tasks in a zero-shot setting – without any
parameter or architecture modification
ⓒ NAVER Connect Foundation 29
GPT-2: Language Models are Unsupervised Multi-task Learners
https://blog.floydhub.com/gpt2/
ⓒ NAVER Connect Foundation 30
GPT-2: Motivation (decaNLP)
• The Natural Language Decathlon: Multitask Learning as Question Answering
• Bryan McCann, Nitish Shirish Keskar, Caiming Xiong, Richard Socher
https://decanlp.com/
ⓒ NAVER Connect Foundation 31
GPT-2: Datasets
• A promising source of diverse and nearly unlimited text is web scrape
such as common crawl
• They scraped all outbound links from Reddit, a social media platform, WebText
• 45M links
• Scraped web pages which have been curated/filtered by humans
• Received at least 3 karma (up-vote)
• 8M removed Wikipedia documents
• Use dragnet and newspaper to extract content from links
ⓒ NAVER Connect Foundation 32
GPT-2: Datasets
• Preprocess
• Byte pair encoding (BPE)
• Minimal fragmentation of words across multiple vocab tokens
ⓒ NAVER Connect Foundation 33
GPT-2: Model
• Modification
• Layer normalization was moved to the input of each sub-block, similar to a pre-activation
residual network
• Additional layer normalization was added after the final self-attention block.
• Scaled the weights of residual layer at initialization by a factor of ൗ
1
𝑛
where 𝑛 is the
number of residual layer
https://openai.com/blog/better-language-models/
ⓒ NAVER Connect Foundation 34
GPT-2: Question Answering
• Use conversation question answering dataset(CoQA)
• Achieved 55 F1 score, exceeding the performance 3 out of 4 baselines
without labeled dataset
• Fine-tuned BERT achieved 89 F1 performance
ⓒ NAVER Connect Foundation 35
GPT-2: Summarization
• CNN and Daily Mail Dataset
• Add text TL;DR: after the article and generate 100 tokens
• (TL;DR: Too long, didn’t read)
https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf
ⓒ NAVER Connect Foundation 36
GPT-2: Translation
• User WMT14 en-fr dataset for evaluation
• Use LMs on a context of example pairs of
the format:
• English sentence = French sentence
• Achieve 5 BLEU score in word-by-word
substitution
• Slightly worse than MUSE (Conneau et al., 2017)
https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf
ⓒ NAVER Connect Foundation
GPT-3
37
ⓒ NAVER Connect Foundation 38
GPT-3: Language Models are Few-Shot Learners
Language Models are Few-shot Learners
• Scaling up language models greatly improves task-agnostic, few-shot performance
• An autoregressive language model with 175 billion parameters in the few-shot setting
• 96 Attention layers, Batch size of 3.2M
0
30
60
90
120
150
180
BERT GPT-2 T5 GPT-3
Number of Parameters (B)
Model size
ⓒ NAVER Connect Foundation 39
GPT-3: Language Models are Few-Shot Learners
Language Models are Few-shot Learners
• Prompt: the prefix given to the model
• Zero-shot: Predict the answer given only a natural language description of the task
• One-shot: See a single example of the task in addition to the task description
• Few-shot: See a few examples of the task
Zero-shot One-shot Few-shot
Language Models are Few-show Learners, NeurIPS’20
ⓒ NAVER Connect Foundation 40
GPT-3: Language Models are Few-Shot Learners
Language Models are Few-shot Learners
• Zero-shot performance improves steadily with model size
• Few-shot performance increases more rapidly
Language Models are Few-show Learners, NeurIPS’20
ⓒ NAVER Connect Foundation 41
ALBERT: A Lite BERT for Self-supervised Learning of Language Representations
• Is having better NLP models as easy as having larger models?
• Obstacles
• Memory Limitation
• Training Speed
• Solutions
• Factorized Embedding Parameterization
• Cross-layer Parameter Sharing
• (For Performance) Sentence Order Prediction
ⓒ NAVER Connect Foundation 42
ALBERT: A Lite BERT for Self-supervised Learning of Language Representations
• Factorized Embedding Parameterization
Dimension size should be same in BERT
http://jalammar.github.io/illustrated-transformer/
ⓒ NAVER Connect Foundation 43
ALBERT: A Lite BERT for Self-supervised Learning of Language Representations
• Factorized Embedding Parameterization
• V = Vocabulary size
• H = Hidden-state dimension
• E = Word embedding dimension
http://jalammar.github.io/illustrated-transformer/
x
V x E
E x H
BERT ALBERT
V x H
ⓒ NAVER Connect Foundation 44
ALBERT: A Lite BERT for Self-supervised Learning of Language Representations
• Cross-layer Parameter Sharing
• Shared-FFN: Only sharing feed-forward network parameters across layers
• Shared-attention: Only sharing attention parameters across layers
• All-shared: Both of them
ALBERT: A Lite BERT for Self-supervised Learning of Language Representations, ICLR’20
ⓒ NAVER Connect Foundation 45
ALBERT: A Lite BERT for Self-supervised Learning of Language Representations
• Sentence Order Prediction
• Next Sentence Prediction pretraining task in BERT is too easy
• Predict the ordering of two consecutive segments of text
• Negative samples the same two consecutive segments
but with their order swapped
ALBERT: A Lite BERT for Self-supervised Learning of Language Representations, ICLR’20
ⓒ NAVER Connect Foundation 46
ALBERT: A Lite BERT for Self-supervised Learning of Language Representations
• GLUE Results
ALBERT: A Lite BERT for Self-supervised Learning of Language Representations, ICLR’20
ⓒ NAVER Connect Foundation 47
ELECTRA: Efficiently Learning an Encoder that Classifies Token Replacements Accurately
• Efficiently Learning an Encoder that Classifies Token Replacements Accurately
• Learn to distinguish real input tokens from plausible but synthetically generated replacements
• Pre-training text encoders as discriminators rather than generators
• Discriminator is the main networks for pre-training.
ELECTRA: Pre-training Text Encoders as Discriminators Rather Than Generators, ICLR’20
ⓒ NAVER Connect Foundation 48
ELECTRA: Efficiently Learning an Encoder that Classifies Token Replacements Accurately
• Replaced token detection pre-training vs masked language model pre-training
• Outperforms MLM-based methods such as BERT given the same model size, data, and
compute
ELECTRA: Pre-training Text Encoders as Discriminators Rather Than Generators, ICLR’20
ⓒ NAVER Connect Foundation 49
Light-weight Models
• DistillBERT (NeurIPS 2019 Workshop)
• A triple loss, which is a distillation loss over the soft target probabilities of the
teacher model leveraging the full teacher distribution
• TinyBERT (Findings of EMNLP 2020)
• Two-stage learning framework, which performs Transformer distillation at both
the pre-training and task-specific learning stages
ⓒ NAVER Connect Foundation 50
Fusing Knowledge Graph into Language Model
• ERNIE: Enhanced Language Representation with Informative Entities (ACL 2019)
• Informative entities in a knowledge graph enhance language representation
• Information fusion layer takes the concatenation of the token embedding and
entity embedding
• KagNET: Knowledge-Aware Graph Networks for Commonsense Reasoning
(EMNLP 2019)
• A knowledge-aware reasoning framework for learning to answer commonsense
questions
• For each pair of question and answer candidate, it retrieves a sub-graph from an
external knowledge graph to capture relevant knowledge
ⓒ NAVER Connect Foundation
References
51
• GPT-1
• https://blog.openai.com/language-unsupervised/
• BERT : Pre-training of deep bidirectional transformers for language understanding, NAACL’19
• https://arxiv.org/abs/1810.04805
• SQuAD: Stanford Question Answering Dataset
• https://rajpurkar.github.io/SQuAD-explorer/
• SWAG: A Large-scale Adversarial Dataset for Grounded Commonsense Inference
• https://leaderboard.allenai.org/swag/submissions/public
• How to Build OpenAI’s GPT-2: “ The AI That Was Too Dangerous to Release”
• https://blog.floydhub.com/gpt2/
ⓒ NAVER Connect Foundation
References
52
• GPT-2
• https://openai.com/blog/better-language-models/
• https://cdn.openai.com/better-language
models/language_models_are_unsupervised_multitask_learners.pdf
• Language Models are Few-shot Learners, NeurIPS’20
• https://arxiv.org/abs/2005.14165
• Illustrated Transformer
• http://jalammar.github.io/illustrated-transformer/
• ALBERT: A Lite BERT for Self-supervised Learning of Language Representations, ICLR’20
• https://arxiv.org/abs/1909.11942
• ELECTRA: Pre-training Text Encoders as Discriminators Rather Than Generators, ICLR’20
• https://arxiv.org/abs/2003.10555
ⓒ NAVER Connect Foundation
References
53
• DistillBERT, a distilled version of BERT: smaller, faster, cheaper and lighter
• https://arxiv.org/abs/1910.01108
• TinyBERT: Distilling BERT for Natural Language Understanding, Findings of EMNLP’20
• https://arxiv.org/abs/1909.10351
• ERNIE: Enhanced Language Representation with Informative Entities
• https://arxiv.org/abs/1905.07129
• KagNet: Knowledge-Aware Graph Networks for Commonsense Reasoning
• https://arxiv.org/abs/1909.02151

---
myst:
   html_meta:
      title: AutoRAG - Unified Evaluation Workflow Strategy Support
      description: Analysis of AutoRAG's support for strategies in the unified evaluation workflow
      keywords: AutoRAG,RAG,evaluation,workflow,strategies,support
---

# Unified Evaluation Workflow Strategy Support

This document analyzes which strategies from the unified evaluation workflow are natively supported by AutoRAG in its full installation. A strategy is considered **supported** only if AutoRAG provides it natively once fully installed, without requiring custom module implementation or external library integration beyond what's included in the full installation.

## Summary

AutoRAG is a specialized RAG (Retrieval-Augmented Generation) optimization framework that focuses on automatically finding optimal RAG pipelines. The analysis below details which strategies from the unified evaluation workflow are supported.

---

## Phase 0: Provisioning (The Runtime)

### Step A: Harness Installation

**Strategy 1: PyPI Packages** ✅ **SUPPORTED**
- AutoRAG can be installed via pip: `pip install AutoRAG`
- Supports optional extras for GPU, parsing, vLLM, and language-specific features
- Full installation: `pip install "AutoRAG[all]"`
- Git-based installation also supported: `pip install git+https://github.com/Marker-Inc-Korea/AutoRAG.git`

**Strategy 2: Git Clone** ✅ **SUPPORTED**
- Repository can be cloned and installed from source
- Installation from source: `git clone https://github.com/Marker-Inc-Korea/AutoRAG.git && cd AutoRAG && pip install -e .`

**Strategy 3: Container Images** ✅ **SUPPORTED**
- AutoRAG provides prebuilt Docker images on Docker Hub
- Available images: `autoraghq/autorag:api-latest`, `autoraghq/autorag:all`, `autoraghq/autorag:gpu`
- Container-based deployment supported for API servers

**Strategy 4: Binary Packages** ❌ **NOT SUPPORTED**
- AutoRAG does not provide standalone executable binaries
- Must be installed through Python package managers

**Strategy 5: Node Package** ❌ **NOT SUPPORTED**
- AutoRAG is Python-based only
- No npm, npx, or Node.js package manager support

### Step B: Service Authentication

**Strategy 1: Evaluation Platform Authentication** ❌ **NOT SUPPORTED**
- AutoRAG does not integrate with external evaluation platforms or leaderboard submission APIs
- No command-line authentication flows for evaluation services

**Strategy 2: API Provider Authentication** ✅ **SUPPORTED**
- Supports environment variable configuration for API keys (OpenAI, Cohere, Voyage AI, etc.)
- Environment variable setup: `export OPENAI_API_KEY="sk-..."`
- `.env` file support with `python-dotenv`
- Required for using commercial LLM and embedding providers

**Strategy 3: Repository Authentication** ✅ **SUPPORTED**
- Integrates with Hugging Face for model and dataset access
- Uses standard Hugging Face authentication tokens
- Supports both public and gated model access through HF ecosystem

---

## Phase I: Specification (The Contract)

### Step A: SUT Preparation

**Strategy 1: Model-as-a-Service (Remote Inference)** ✅ **SUPPORTED**
- Extensive support for remote API-based models:
  - OpenAI models (GPT-4, GPT-3.5, embeddings)
  - Cohere API for reranking
  - Voyage AI for embeddings and reranking
  - MixedBread AI for reranking
  - AWS Bedrock models
  - Nvidia NIM
  - Custom OpenAI-compatible endpoints
- Configuration through YAML files and API clients

**Strategy 2: Model-in-Process (Local Inference)** ✅ **SUPPORTED**
- Local model loading via HuggingFace transformers
- Integration with LlamaIndex for local LLMs
- Support for local embedding models (sentence-transformers)
- Local rerankers (FlashRank, BAAI/bge-reranker, ColBERT, MonoT5, etc.)
- GPU acceleration support with `pip install "AutoRAG[gpu]"`
- vLLM support for optimized local inference

**Strategy 3: Algorithm Implementation (In-Memory Structures)** ✅ **SUPPORTED**
- BM25 (lexical retrieval) with rank_bm25
- Vector database indexes (FAISS via Milvus, HNSW via Qdrant, etc.)
- Multiple vector database backends: Chroma, Milvus, Weaviate, Pinecone, Qdrant, Couchbase
- Hybrid retrieval combining BM25 and semantic search

**Strategy 4: Policy/Agent Instantiation (Stateful Controllers)** ❌ **NOT SUPPORTED**
- AutoRAG focuses on RAG pipeline evaluation, not agent/policy evaluation
- No support for reinforcement learning policies or autonomous agents
- No multi-agent systems or robot controller support

### Step B: Benchmark Preparation (Inputs)

**Strategy 1: Benchmark Dataset Preparation (Offline)** ✅ **SUPPORTED**
- Parquet-based dataset loading for QA and corpus data
- Data parsing from multiple formats (PDF, DOCX, etc.) via LlamaIndex and Langchain
- Chunking modules for preprocessing (token-based, semantic, etc.)
- Dataset validation and casting utilities
- Integration with Hugging Face datasets
- Sample datasets available on Hugging Face

**Strategy 2: Synthetic Data Generation (Generative)** ✅ **SUPPORTED**
- QA dataset generation from corpus using LLMs
- Query generation (`factoid_query_gen`, multi-hop queries)
- Answer generation (`make_basic_gen_gt`, `make_concise_gen_gt`)
- Retrieval ground truth generation
- Filtering mechanisms (e.g., `dontknow_filter_rule_based`)

**Strategy 3: Simulation Environment Setup (Simulated)** ❌ **NOT SUPPORTED**
- No support for interactive environments or simulations
- No 3D virtual environments or physics simulations
- Focus is on text-based RAG evaluation only

**Strategy 4: Production Traffic Sampling (Online)** ❌ **NOT SUPPORTED**
- No native support for sampling real-world production traffic
- No streaming traffic buffering or online feedback collection
- Evaluation is offline/batch-based only

### Step C: Benchmark Preparation (References)

**Strategy 1: Judge Preparation** ✅ **SUPPORTED**
- LLM-as-judge metrics supported:
  - G-Eval for coherence, consistency, fluency, relevance
  - DeepEval-based prompts for evaluation
- Pre-configured judge models (GPT-4, etc.)
- Custom LLM judge configuration through YAML

**Strategy 2: Ground Truth Preparation** ✅ **SUPPORTED**
- Pre-loading of ground truth from parquet datasets
- Retrieval ground truth (doc IDs and content)
- Generation ground truth (reference answers)
- Embedding index preparation for semantic retrieval
- BM25 index preparation for lexical retrieval

---

## Phase II: Execution (The Run)

### Step A: SUT Invocation

**Strategy 1: Batch Inference** ✅ **SUPPORTED**
- Primary execution mode in AutoRAG
- Evaluates entire QA datasets through RAG pipelines
- Supports batch processing with configurable batch sizes
- Multiple module combinations tested in parallel
- AutoML-style grid search over configurations

**Strategy 2: Interactive Loop** ❌ **NOT SUPPORTED**
- No support for stateful, iterative interactions
- No tool-based reasoning or multi-turn dialogues
- No physics simulation or multi-agent coordination
- Focus is on single-turn question-answering

**Strategy 3: Arena Battle** ❌ **NOT SUPPORTED**
- No native pairwise comparison of SUTs on same inputs
- Evaluation compares different pipeline configurations, not different models side-by-side
- No dedicated arena battle mode

**Strategy 4: Production Streaming** ❌ **NOT SUPPORTED**
- No continuous processing of live production traffic
- No real-time drift monitoring
- API server supports streaming responses but not production traffic evaluation

---

## Phase III: Assessment (The Score)

### Step A: Individual Scoring

**Strategy 1: Deterministic Measurement** ✅ **SUPPORTED**
- Retrieval metrics:
  - Precision, Recall, F1, NDCG, MRR, MAP
  - Token-based metrics (retrieval_token_f1, retrieval_token_recall, etc.)
- Generation metrics:
  - BLEU (n-gram based)
  - ROUGE (n-gram based recall)
  - METEOR (with stemming and synonyms)
- Exact matching and algorithmic calculations

**Strategy 2: Embedding Measurement** ✅ **SUPPORTED**
- Semantic similarity metrics:
  - SemScore (sentence embedding similarity)
  - BERTScore support through embeddings
- Embedding models: OpenAI, HuggingFace, custom models
- Context precision using embeddings (Ragas-based)

**Strategy 3: Subjective Measurement** ✅ **SUPPORTED**
- LLM-as-judge metrics:
  - G-Eval (coherence, consistency, fluency, relevance)
  - Custom prompt-based evaluation
  - GPT-4 and other LLMs as evaluators
- DeepEval integration for subjective assessments

**Strategy 4: Performance Measurement** ❌ **NOT SUPPORTED**
- No native metrics for latency, throughput, or resource consumption
- No built-in profiling for memory, FLOPs, or energy costs
- API server exists but performance benchmarking not included in evaluation framework

### Step B: Collective Aggregation

**Strategy 1: Score Aggregation** ✅ **SUPPORTED**
- Automatic aggregation of per-instance scores to benchmark-level metrics
- Mean, median, and other statistical aggregations
- Summary CSV files with aggregate results
- Multi-metric optimization support in YAML configs

**Strategy 2: Uncertainty Quantification** ❌ **NOT SUPPORTED**
- No bootstrap resampling for confidence intervals
- No Prediction-Powered Inference (PPI)
- No uncertainty bounds around aggregate metrics

---

## Phase IV: Reporting (The Output)

### Step A: Insight Presentation

**Strategy 1: Execution Tracing** ❌ **NOT SUPPORTED**
- No detailed step-by-step execution logs showing reasoning paths
- No tool call visualization or intermediate state displays
- Basic logging available but not detailed execution traces

**Strategy 2: Subgroup Analysis** ❌ **NOT SUPPORTED**
- No built-in stratification by demographic groups, domains, or task categories
- Results are aggregated globally, not broken down by subgroups
- Users must manually analyze subgroups

**Strategy 3: Chart Generation** ✅ **SUPPORTED**
- Dashboard with visualizations (via Panel and Seaborn)
- Performance comparison charts across modules
- Metric trend visualization
- Interactive plots in dashboard

**Strategy 4: Dashboard Creation** ✅ **SUPPORTED**
- Web-based dashboard: `autorag dashboard --trial_dir /path/to/trial`
- Interactive web interface for exploring results
- Table-based result browsing
- Runs on localhost with configurable port
- Visualization of module comparisons and rankings

**Strategy 5: Leaderboard Publication** ❌ **NOT SUPPORTED**
- No integration with public or private leaderboards
- No result submission APIs
- Results remain local to the project

**Strategy 6: Regression Alerting** ❌ **NOT SUPPORTED**
- No automatic comparison with historical baselines
- No performance degradation detection
- No alerting mechanisms for metric thresholds

---

## Conclusion

### Supported Strategies Summary

AutoRAG natively supports **18 out of 38** strategies (47%) from the unified evaluation workflow:

**Phase 0 - Provisioning:** 5/8 strategies
- ✅ PyPI Packages, Git Clone, Container Images
- ✅ API Provider Authentication, Repository Authentication

**Phase I - Specification:** 7/9 strategies
- ✅ Model-as-a-Service, Model-in-Process, Algorithm Implementation
- ✅ Benchmark Dataset Preparation, Synthetic Data Generation
- ✅ Judge Preparation, Ground Truth Preparation

**Phase II - Execution:** 1/4 strategies
- ✅ Batch Inference

**Phase III - Assessment:** 4/6 strategies
- ✅ Deterministic Measurement, Embedding Measurement, Subjective Measurement
- ✅ Score Aggregation

**Phase IV - Reporting:** 2/5 strategies
- ✅ Chart Generation, Dashboard Creation

### Core Strengths

AutoRAG excels at:
1. **RAG-specific evaluation**: Comprehensive support for retrieval and generation metrics
2. **Model flexibility**: Both remote API and local model support
3. **Data preparation**: Strong synthetic data generation and dataset handling
4. **Batch evaluation**: Robust AutoML-style pipeline optimization
5. **Visualization**: Interactive dashboard for result exploration

### Notable Gaps

AutoRAG does not support:
1. **Interactive/online evaluation**: No streaming production traffic or agent loops
2. **Performance benchmarking**: No latency, throughput, or resource metrics
3. **Leaderboard integration**: No public leaderboard submission
4. **Uncertainty quantification**: No confidence intervals or statistical uncertainty
5. **Advanced analytics**: No subgroup analysis or regression alerting
6. **Non-RAG modalities**: Focused solely on text-based RAG, no RL/robotics/simulation

These gaps are expected and appropriate given AutoRAG's focused mission as a RAG pipeline optimization tool rather than a general-purpose evaluation harness.

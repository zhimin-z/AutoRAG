# AutoRAG Evaluation Workflow Support - Quick Reference

**Last Updated:** 2025-12-12

## Overall Support: 18/34 Strategies (53%)

### ✅ Fully Supported Areas

1. **Installation & Setup**
   - PyPI packages (`pip install AutoRAG`)
   - Git clone and source installation
   - Docker containers (API, GPU, all variants)
   - API key authentication (OpenAI, Cohere, etc.)
   - Hugging Face repository authentication

2. **Model Integration**
   - Remote API models (OpenAI, Cohere, Bedrock, etc.)
   - Local models (HuggingFace, LlamaIndex, vLLM)
   
   **Note:** Vector databases and BM25 are used as pipeline components, not evaluated as standalone SUTs

3. **Data & Benchmarks**
   - Parquet dataset loading
   - Synthetic QA generation
   - Ground truth preparation
   - LLM-as-judge setup

4. **Evaluation Metrics**
   - Retrieval: Precision, Recall, F1, NDCG, MRR, MAP
   - Generation: BLEU, ROUGE, METEOR, SemScore
   - Embedding-based similarity
   - LLM-as-judge (G-Eval, DeepEval)

5. **Results & Visualization**
   - Interactive dashboard
   - Performance charts
   - Summary CSV files
   - Metric aggregation

### ❌ Not Supported

1. **Interactive/Online Evaluation**
   - No production traffic streaming
   - No agent/RL policy evaluation
   - No multi-turn dialogues

2. **Performance Benchmarking**
   - No latency/throughput metrics
   - No resource profiling (memory, FLOPs, energy)

3. **Advanced Analytics**
   - No subgroup/stratified analysis
   - No uncertainty quantification
   - No regression alerting

4. **External Integration**
   - No leaderboard submission
   - No evaluation platform APIs

## See Full Documentation

For detailed analysis of each strategy, see [evaluation_workflow_support.md](evaluation_workflow_support.md)

## Key Takeaway

AutoRAG is optimized for **batch RAG pipeline evaluation** with strong support for:
- Model flexibility (API + local)
- Comprehensive RAG metrics
- Data generation
- Visual result exploration

It focuses on offline optimization rather than online monitoring, interactive agents, or performance profiling.

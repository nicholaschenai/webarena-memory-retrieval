# Attribution
The original authors of WebArena can be found here:
[[Code](https://github.com/web-arena-x/webarena)]
[[Site](https://webarena.dev/)]
[[Paper](https://arxiv.org/2307.13854)]

# Intro
This repo is a modification of WebArena, forked from version 9c01d57a48bf170a24c7a50e21d881edf36d38b2 Aug 28, 2023

## Modification 1: CoT + Task Chat Memory
Chat memory that persists throughout the task, but observation is limited to the latest appearance (i.e. old observations are not included), as observations are lengthy. Default CoT in the paper only has memory of the previous issued action

Usage:

```python
python run.py --instruction_path agent/prompts/jsons/historical_cot_best.json --test_start_idx 0 --test_end_idx 812 --model gpt-3.5-turbo --result_dir outputs/historical_cot
```

### Upgrades
- Fixed inconsistent backticks issue in prompt
- Prompting to remind agent not to act on past history, and be mindful of repeating actions

## Modification 2: CoT + VectorDB Retrieval
Retrieves the top-k relevant history to aid agent. Code works but have not fully evaluated it; Past trajectories take up a lot of context and exceeds the limit quickly — This implementation still requires a technique to condense the past results e.g. maybe another LM to summarize the history?

Usage:

```python
python run.py --instruction_path agent/prompts/jsons/vectorDB_cot.json --retrieval_top_k 3 --test_start_idx 0 --test_end_idx 3 --model gpt-3.5-turbo --result_dir outputs/vectorDB_cot
```
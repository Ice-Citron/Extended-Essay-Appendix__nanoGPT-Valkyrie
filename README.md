# Extended Essay: nanoGPT-Valkyrie Evaluation Appendix

**[Read the full extended essay][paper]**

[Main research repository: nanoGPT-Valkyrie][research]

This repository is the appendix of my my IB Computer Science Extended Essay on 
GPT-2 normalisation. I used LLM-as-a-judge to evaluate the GPT-2s I pre-trained
and SFT'd with GPT-4o, for which this repository contains CSV files which 
are records from GPT-4o.

The CSV files combine model outputs with GPT-4o scores and feedback.
Use them to inspect the individual assessments behind the study.

## Data files

| Task | Input source | Records | File |
|---|---|---:|---|
| Question answering | SQuAD v2 | 200 | [View CSV][qa] |
| Summarisation | BillSum | 200 | [View CSV][summary] |
| Text generation | 25 prompts | 200 | [View CSV][generation] |

Each task contains 25 records for each of eight model variants.
The three files contain 600 evaluation records in total.

## Model variants

The models use LayerNorm (`LN`) or RMSNorm (`RMSN`).
Each normalisation method has four variants:

| Variant | Normalisation within each Transformer block |
|---|---|
| `baseModel` | Before attention and before the feedforward network. |
| `AttnOnly` | Before attention only. |
| `FFNonly` | Before the feedforward network only. |
| `noNorm` | No normalisation within the block. |

The final normalisation layer remains in all four variants.

The SQuAD and BillSum files identify the task-specific models through
`model_name`. They also contain `norm_type` and `variant` columns.

The text generation file uses shorter names, such as `LN_AttnOnly`.

### Scores

GPT-4o was prompted to assess each of my trained model variant's output against 
five criteria on a scale from 1 to 5. The criteria differ between tasks:

| Criterion | SQuAD | BillSum | Text generation |
|---|:---:|:---:|:---:|
| Correctness | Yes | N/A | N/A |
| Completeness | Yes | N/A | N/A |
| Accuracy | N/A | Yes | N/A |
| Conciseness | Yes | Yes | N/A |
| Coherence | N/A | Yes | Yes |
| Creativity | N/A | N/A | Yes |
| Engagement | N/A | N/A | Yes |
| Fluency | Yes | Yes | Yes |
| Relevance | Yes | Yes | Yes |

In these files, `Overall Score` is the mean of the five criterion scores.

Addiionally, we also prompted GPT-4o to supply additional `Overall Feedback` and `Comments on Columns` about each of their respective evaluations. These fields 
contain the GPT-4o's written explanations.

For more detail, see our [paper][paper] which explained the evaluation method 
and statistical analysis.

## Relationship to nanoGPT-Valkyrie

[nanoGPT-Valkyrie][research] is the main repository for this research.
It contains the paper and the experiment code.

The main repository also contains identical copies of these CSV files.
Find them in its [statistical analysis inputs][data]:

- `results/statistics/squad/inputs/`
- `results/statistics/billsum/inputs/`
- `results/statistics/text-generation/inputs/`

This appendix provides direct access to the combined evaluation records.

## Repository structure

```text
Extended-Essay-Appendix/
├── README.md
├── LICENSE
├── Question Answering/
│   └── GPT-4o Source Files/
│       └── combined_data_truncated_squad.csv
├── Summarisation/
│   └── GPT-4o Source Files/
│       └── combined_data_truncated.csv
└── Text Generation/
    └── GPT-4o Source Files/
        └── combined_data_truncated.csv
```

## Citation

Ng, Shi Hao. *The Impact of Layer Normalisation Methods on Training
Effectiveness and Performance of Decoder-Only Transformer Architectures.*
IB Computer Science Extended Essay.

[Read the paper][paper] · [Research code and results][research]

## Licence

This repository uses the [MIT License](LICENSE).

[paper]:
  https://drive.google.com/file/d/1dlhTgv4-A2cCYSsL00An_XpfGpg1DyWy/view
[research]: https://github.com/Ice-Citron/nanoGPT-Valkyrie
[data]:
  https://github.com/Ice-Citron/nanoGPT-Valkyrie/tree/main/results/statistics
[qa]:
  <Question Answering/GPT-4o Source Files/combined_data_truncated_squad.csv>
[summary]:
  <Summarisation/GPT-4o Source Files/combined_data_truncated.csv>
[generation]:
  <Text Generation/GPT-4o Source Files/combined_data_truncated.csv>

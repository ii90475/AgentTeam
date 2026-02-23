# Data/ML Pipeline Template

## Description
Data processing pipelines, machine learning projects, analytics, ETL workflows.

## Typical Tech Stacks

| Layer | Options |
|-------|---------|
| Language | Python |
| Data Processing | Pandas, Polars, DuckDB |
| ML Framework | scikit-learn, PyTorch, TensorFlow |
| Notebooks | Jupyter, Marimo |
| Orchestration | Airflow, Dagster, Prefect |
| Experiment Tracking | MLflow, Weights & Biases |
| Storage | S3, GCS, local parquet |

## Recommended Agents

### Local Agents (Routine Tasks)
| Agent | Use For |
|-------|---------|
| **code-scaffolder** | Data loaders, transformers, models |
| **code-reviewer** | Data leakage, pipeline bugs |
| **test-builder** | Data validation tests |
| **doc-generator** | Data dictionaries, model cards |
| **status-updater** | Experiment logs |

### Claude Agents (Complex Tasks)
| Agent | Use For |
|-------|---------|
| **project-manager** | Experiment planning, milestones |
| **technology-analyst** | Model selection, architecture |

## Project Structure

```
{project-name}/
├── .claude/
├── CLAUDE.md
├── README.md
├── docs/
│   ├── architecture.md
│   ├── data-dictionary.md
│   ├── model-card.md
│   ├── project-status.md
│   └── changelog.md
├── notebooks/
│   ├── 01_exploration.ipynb
│   ├── 02_preprocessing.ipynb
│   └── 03_modeling.ipynb
├── src/
│   ├── data/            # Data loading/processing
│   ├── features/        # Feature engineering
│   ├── models/          # Model definitions
│   ├── training/        # Training scripts
│   ├── evaluation/      # Metrics, validation
│   └── utils/           # Helpers
├── data/
│   ├── raw/             # Original data (gitignored)
│   ├── processed/       # Cleaned data
│   └── external/        # Third-party data
├── models/              # Saved models (gitignored)
├── tests/
├── configs/             # Experiment configs
├── .env.example
├── .gitignore
├── requirements.txt
└── Makefile
```

## Initial Setup Checklist

- [ ] Initialize git repository
- [ ] Set up virtual environment
- [ ] Configure data storage paths
- [ ] Create data loading pipeline
- [ ] Set up experiment tracking
- [ ] Configure reproducibility (random seeds, versioning)
- [ ] Create evaluation framework
- [ ] Set up model registry
- [ ] Document data sources and schemas
- [ ] Create training/inference scripts

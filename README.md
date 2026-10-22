# Experiment 5 — Feature Store with Feast

## Aim

Define reusable ML features, retrieve historical features for training, materialize features into a local online store, and retrieve values for inference.

## Tools

- Feast 0.67.0 with its local provider
- Pandas and the sample Parquet data included with the Feast repository
- Local SQLite registry and online store

## Run the practical

Install the repository dependencies from the root, then run the local workflow from the Feast feature repository:

```powershell
Set-Location experiment-05-feature-store\feast_repo\feature_repo
python test_workflow.py
```

The script applies feature definitions, retrieves historical training features, materializes the local online store, retrieves online features, and demonstrates a stream update. It retains local SQLite state so the registry and online-store files can be inspected after the run.

## Implementation

- [`feast_repo/feature_repo/feature_store.yaml`](./feast_repo/feature_repo/feature_store.yaml) configures Feast's local provider and SQLite online store.
- [`feast_repo/feature_repo/feature_definitions.py`](./feast_repo/feature_repo/feature_definitions.py) defines entities, feature views, request-time transformations, feature services, and labels.
- [`feast_repo/feature_repo/data/`](./feast_repo/feature_repo/data/) contains the small sample Parquet sources.
- [`feature_store_demo.py`](./feature_store_demo.py) is a separate lightweight SQLite concept demonstration.

## Captured output

[`OUTPUT.txt`](./OUTPUT.txt) records the actual Feast command output from a local run. Values in the offline and online results are from the generated sample data; they are not a production feature service.

## Result

The local Feast workflow successfully applied definitions, returned historical features, materialized two feature views to SQLite, performed online feature retrieval, and demonstrated updating a driver's features. The provider, registry, and online store are local only; shared or production infrastructure is not configured.

## Viva questions

1. How does historical feature retrieval prevent training-serving skew?
2. Why does an online store need materialized values?
3. What is the difference between a feature view and a feature service?

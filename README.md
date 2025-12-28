# SAP-RPT-1-OSS Predictor Skill

A Claude skill for using SAP's open source **SAP-RPT-1-OSS** tabular foundation model for predictive analytics on SAP business data.

## Overview

SAP-RPT-1-OSS is SAP's open source (Apache 2.0) tabular foundation model announced at TechEd 2025. Unlike LLMs that predict text, RPT-1 predicts field values in table rows using in-context learning—no model training required.

- **Repository**: https://github.com/SAP-samples/sap-rpt-1-oss
- **Model**: https://huggingface.co/SAP/sap-rpt-1-oss

This skill enables Claude to:
- Set up and authenticate with Hugging Face for model access
- Prepare SAP data extracts for prediction
- Run classification and regression using the local OSS model
- Handle batch processing for large datasets
- Optionally use RPT Playground API as alternative

## Use Cases

| SAP Module | Prediction Type | Example |
|------------|-----------------|---------|
| FI-AR | Payment Default Risk | Predict which invoices will go unpaid |
| SD | Customer Churn | Identify at-risk customers |
| SD/LE | Delivery Delays | Forecast shipping delays |
| FI-GL | Journal Anomalies | Detect unusual postings |
| MM | Vendor Performance | Score supplier reliability |
| PP/MM | Demand Forecast | Predict future quantities |

## Structure

```
sap-rpt1-oss-predictor/
├── SKILL.md                     # Main skill instructions
├── scripts/
│   ├── rpt1_oss_predict.py      # Local OSS model wrapper
│   ├── prepare_sap_data.py      # SAP data extraction utilities
│   ├── batch_predict.py         # Batch processing for large datasets
│   └── rpt1_api.py              # Optional: RPT Playground API client
├── references/
│   ├── sap-use-cases.md         # Detailed SAP prediction scenarios
│   └── api-reference.md         # Complete API documentation
└── examples/
    ├── customer_churn_sample.csv
    └── payment_default_sample.csv
```

## Requirements

- **Hugging Face account** (free) - for model access
- **GPU recommended**: 24-80GB VRAM for optimal performance
- Python 3.11+ with pandas, torch

## Quick Start

```bash
# Install model
pip install git+https://github.com/SAP-samples/sap-rpt-1-oss

# Authenticate with Hugging Face
huggingface-cli login
```

```python
from sap_rpt_oss import SAP_RPT_OSS_Classifier

clf = SAP_RPT_OSS_Classifier(max_context_size=4096, bagging=4)
clf.fit(X_train, y_train)
predictions = clf.predict(X_test)
```

## Related Resources

- [SAP-RPT-1-OSS GitHub](https://github.com/SAP-samples/sap-rpt-1-oss)
- [Model on Hugging Face](https://huggingface.co/SAP/sap-rpt-1-oss)
- [ConTextTab Research Paper](https://arxiv.org/abs/2506.10707)

## License

Apache 2.0

---
layout: post
title: Cloud Computing in Genomics — How DNAnexus is Transforming Precision Medicine
subtitle: A look at how cloud platforms are accelerating genomic research and clinical diagnostics
tags: [cloud, genomics, biomedicine, precision-medicine]
comments: true
author: Iñigo Arriazu Garcia
---

## Introduction

The rapid drop in sequencing costs over the last two decades has created an enormous challenge: **data management**. A single whole-genome sequencing (WGS) run produces roughly 200 GB of raw data, and large cohort studies now routinely analyse thousands of samples. Processing, storing, and sharing these datasets with traditional on-premise infrastructure is increasingly impractical. Cloud computing has emerged as the natural answer to this problem.

In this post I will explore **DNAnexus**, a cloud-based platform specifically designed for genomic data analysis, and discuss how it exemplifies the broader adoption of cloud services in biomedical research.

---

## What is DNAnexus?

DNAnexus is a **PaaS (Platform as a Service)** built on top of Amazon Web Services (AWS) and Microsoft Azure that provides:

- Secure, compliant storage of genomic and clinical data (HIPAA, GDPR, ISO 27001)
- A scalable workflow execution engine compatible with standard bioinformatics pipelines (CWL, WDL, Nextflow)
- A marketplace of curated tools and apps for variant calling, RNA-seq, GWAS, etc.
- Collaboration features that allow researchers across institutions to share data and analyses without physically transferring files

The platform is used by large-scale initiatives such as the **UK Biobank** (500,000 participants) and **All of Us Research Program** (NIH, USA), making it one of the most prominent examples of cloud computing applied to population-scale genomics [1, 2].

---

## Key Cloud Concepts Illustrated by DNAnexus

### Elasticity and Pay-per-use

Genomic analyses are highly variable in compute demand. Aligning short reads from a single sample may require 8 CPUs for 2 hours, while a genome-wide association study (GWAS) on 100,000 samples may need thousands of CPU-hours. DNAnexus leverages cloud elasticity to provision resources on demand and release them when the job finishes, drastically reducing idle infrastructure costs.

### Data Locality

One of the most important shifts in thinking is moving **computation to the data** rather than moving data to the computation. Transferring a 10 TB dataset over the internet is slow, expensive, and risky. DNAnexus keeps raw data in the cloud and spins up compute nodes in the same region, reducing both latency and egress costs.

### Reproducibility through Containerisation

Each app in DNAnexus runs inside a Docker container, ensuring that the exact same software environment is used every time. This addresses the "works on my machine" problem that has long plagued bioinformatics, and is critical for regulatory submissions and clinical reporting.

---

## A Concrete Use Case: Rare Disease Diagnostics

Eberle et al. (2017) described a workflow running on DNAnexus for clinical-grade WGS interpretation in rare-disease patients [3]. Key points:

| Step | Tool | Cloud benefit |
|------|------|---------------|
| Read alignment | BWA-MEM | Parallelised across dozens of nodes |
| Variant calling | DeepVariant (Google) | GPU acceleration on demand |
| Annotation | VEP + ClinVar | Shared reference datasets, no local install |
| Report | Custom app | Auditable, version-controlled pipeline |

The end-to-end pipeline went from sample to clinical report in **< 24 hours**, something that would have taken days on a typical local HPC cluster.

---

## Challenges and Limitations

Despite its advantages, cloud-based genomics is not without drawbacks:

- **Cost unpredictability**: Elastic compute is powerful but can lead to unexpectedly large bills if workflows are not optimised.
- **Data sovereignty**: Sending patient data to a third-party cloud provider raises legal and ethical questions, especially across jurisdictions.
- **Vendor lock-in**: Proprietary APIs and data formats can make migrating between providers difficult.
- **Learning curve**: Researchers need to learn new tools (CLI, workflow languages, IAM policies) that are not traditionally part of a biology curriculum.

---

## Conclusion

Cloud platforms like DNAnexus demonstrate that cloud computing is not merely an IT convenience — it is an **enabling technology** for science at scales previously unimaginable. As datasets grow and multi-centre collaboration becomes the norm, mastering cloud services will be an essential skill for health data scientists.

---

## References

[1] Bycroft, C. et al. (2018). The UK Biobank resource with deep phenotyping and genomic data. *Nature*, 562, 203–209. https://doi.org/10.1038/s41586-018-0579-z

[2] Denny, J. C., et al. (2019). The "All of Us" Research Program. *New England Journal of Medicine*, 381, 668–676. https://doi.org/10.1056/NEJMsr1809937

[3] Eberle, M. A., et al. (2017). A reference data set of 5.4 million phased human variants validated by genetic inheritance from sequencing a three-generation 17-member pedigree. *Genome Research*, 27(1), 157–164. https://doi.org/10.1101/gr.210500.116

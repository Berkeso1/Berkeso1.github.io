---
layout: post
title: Meta-Analysis
comments: true
mathjax: true

---

As a fellow member of the machine learning community, one thing that everyone wishes for but can't always have is labeled, high-quality training data. But like lots of it. Certain topics that you may want to apply machine learning to may not have sufficient data to train a model on which can pose an issue. Therefore I decided to explore a paper that addresses synthetic data creation using large language models to overcome this limitation. The paper can be found [here](https://www-jstor-org.horacemann.idm.oclc.org/stable/48784778?searchText=large+language+model).

# Overcoming the Labeled Training Data Bottleneck: A Route to Specialized AI

The paper "Overcoming the Labeled Training Data Bottleneck: A Route to Specialized AI" focuses on utilizing LLMs to compose synthetic datasets in order to overcome the shortage of labeled data, specifically for special tasks in cybersecurity.

The null hypothesis of this research was that the use of large language models (LLMs) and synthetically generated datasets does not improve the accuracy or effectiveness of cybersecurity AI systems, particularly in zero-day exploit detection.

Two of the two other challenging "alternative" hypotheses indicated by the researchers are: first, that LLMs actually can create high-value, task-specialized synthetic data which actually will improve machine learning model performance, and secondly, this actually does represent one effective way to solve one of the leading challenges in cybersecurity, zero-day exploit detection, by creating a dataset specific to this mission.

## Who is collecting and analyzing this data?

Similar to what Ms. Feng did in her post, I will also be giving a score from 1-5 of trustworthiness for each section.

**Journal Reputation**: The paper Overcoming the Labeled Training Data Bottleneck: A Route to Specialized AI by Dr. Ravi Starzl was published in The Cyber Defense Review in the Summer 2024 issue, Volume 9, No. 2. Although this isn't a very well known journal, The Cyber Defense Review is published by the Army Cyber Institute, a US government-funded research institute operating under the U.S. Military Academy at West Point. I personally believe that anything related to the army and/or the US government is reliable, therefore I will be giving this a **5** in terms of trustworthiness.

**Institutional Affiliations**: Dr. Ravi Starzl, a former PhD student and current Carnegie Mellon University (CMU) faculty member, is the primary researcher collecting and analyzing this data. Recently, Dr. Ravi Starzl has been recognized for his contributions to the AI and ML community, recently receiving the 2024 Award for Artificial Intelligence Excellence from the Business Intelligence Group. I will be giving this section a **4/5** due to his affiliation with successful and well-known institutions.

**Funding**: As previously mentioned, this research was done for the purpose of cybersecurity, specifically for a US government-funded institute. Therefore, there is a chance that the US government may be funding Dr. Ravi Starzl in his research. However I cannot be completely sure of this, therefore I will have to give this section a **3** since there is no clear indication that he was funded by an external orginization.

## What datasets does this study reference or use?

The study references several publicly available datasets (I have provided links), including:

[KDD Cup 99 Dataset](http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html):
Despite its age, this dataset remains a cornerstone in network intrusion detection, offering a broad spectrum of network connection features.

[NSL-KDD Dataset](https://www.unb.ca/cic/datasets/nsl.html):
An evolution of the KDD Cup 99 dataset, the NSL-KDD addresses previous limitations by eliminating redundant records, thereby enhancing the dataset's utility for training and testing intrusion detection models.

[CICIDS2017 Dataset (Canadian Institute for Cybersecurity Intrusion Detection System 2017)](https://www.unb.ca/cic/datasets/ids-2017.html):
Featuring both malicious and benign attacks, this dataset reflects contemporary attack scenarios with detailed network traffic features and, for some attack types, payload data.

[UNSW-NB15 Dataset](https://www.unsw.adfa.edu.au/unsw-canberra-cyber/cybersecurity/ADFA-NB15-Datasets/):
Provided by the Australian Cyber Security Centre, this dataset mixes real normal activities with synthetic attack behaviors, offering a diverse array of network traffic analysis features.

[ISCX VPN-nonVPN Traffic Dataset (ISCXVPN2016)](https://www.unb.ca/cic/datasets/vpn.html):
Containing labeled network traffic that differentiates between VPN and non-VPN traffic, this dataset is invaluable for studying encrypted traffic patterns and potentially high-entropy payloads.

[CTU-13 Dataset](https://mcfp.felk.cvut.cz/publicDatasets/CTU-13-Dataset/):
This dataset includes botnet traffic alongside normal and background traffic, facilitating the study of botnet behaviors which may share similarities with zero-day exploit traffic patterns, especially in command and control communications and lateral movements.

[MAWI Working Group Traffic Archive](http://mawi.wide.ad.jp/mawi/):
A compilation of real-world internet backbone traffic datasets from the Wide project, capturing a variety of internet activities over extended periods. While not cybersecurity-specific, it offers a rich baseline for normal traffic pattern analysis.

[The CAIDA UCSD Datasets](https://www.caida.org/data/passive/):
Provided by the Center for Applied Internet Data Analysis (CAIDA), these datasets consist of anonymized internet traces, aiding in the modeling of both normal and anomalous network behaviors.

[ToN IoT Telemetry Dataset](https://research.unsw.edu.au/projects/toniot-dataset):
A contemporary dataset focusing on Internet of Things (IoT) telemetry, including network traffic, logs, and attack data. It is particularly suited for exploring IoT-specific threats and anomalies.

These datasets can be found on pages 116 and 117 at this [link](https://www.jstor.org/stable/10.2307/48784778)

These datasets are publicly available and have been extensively used in the cybersecurity research community. The research uses these datasets as a base and supplements them with synthetically generated data​.

## Why are they interested in this data?

Imagine trying to solve a mystery but only having half the clues — frustrating, right? That’s exactly what researchers face when they don't have enough high-quality, labeled data to train machine learning models. In the fast-paced world of cybersecurity, where new threats like zero-day exploits pop up unexpectedly, having the right data can mean the difference between catching the bad guys or letting them slip through the cracks.

So why are they so interested in this data? Well its simple — it’s the missing piece of the puzzle. By gathering real-world datasets (think cyber attack traffic and network behaviors), and then supercharging them with synthetic data generated by large language models (LLMs), they’re able to create the ultimate training ground for machine learning models. This allows AI models to become digital detectives, spotting security threats more accurately and efficiently.

In short, they need this data to teach AI how to outsmart the hackers and keep us all safe in this ever-evolving digital landscape! But without sufficient high quality data, they simply cannot do this.

## What data is being recorded? What data might be left out?

Alright, let’s get into the specifics! The data they’re collecting is all about the fine details of network traffic, like the "digital footprints" left behind when data moves through a network. In this study, they’re recording things like **protocol types**, **source and destination bytes**, **error rates**, **urgent counts**, and **service flags** (you know, all the nerdy stuff that makes network traffic tick). For example, the paper mentions recording values like **Rerror Rate** and **Srv Count** — basically, they're trying to capture the whole picture of what's happening in the network at any given time​. Heres a specific piece of text from the paper:

![text](/assets/img/picture3.png)

But, let’s face it, not every bit of data gets recorded. Some real-world variability might not make the cut. For instance, things like new vulnerabilities that haven’t been documented yet or very rare attack patterns could be missing. These gaps are like trying to catch a rare animal in the wild — if no one’s seen it before, it’s hard to include it in the dataset! The study highlights how creating synthetic data with Large Language Models (LLMs) tries to fill some of these gaps, but even then, there’s always the chance that some specific, one-off events might slip through the cracks.

In short: They’re recording a ton of useful stuff to teach AI how to detect threats, but no dataset can capture every possible scenario. There’s always something that might be left out, especially with how quickly new cyber threats evolve!







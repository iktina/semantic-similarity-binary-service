# Binary Semantic Similarity


## Welcome

The service receives a pair of text files and uses it as an input for a pre-trained neural classifier model.

## What’s the point?

The service outputs a binary semantic homogeneity parameter for the pair of input sentences. 
The value of the parameter '1' means similarity of sentences, and '0' means their distinction.
The input sentences are limited to 60 tokens each.

## Model details
The service receives a couple of textual sentences in English and uses it as input for the BERT Base neural model trained to solve the classification task using a combination/fusion of several open-source datasets on the basis of semantic similarity estimation and paraphrase detection and infers whether the entered sentences are semantically equivalent or not (1/0). The model runs on a P100 GPU. The input sequences are limited to 60 words each.

## How does it work?

The user must provide the following inputs in order to start the service and get a response:

Inputs:

 -   `endpoint`: bss.naint.tech.
 -   `method`: ss_bert.
 -   `input_path`: Path to '\*.txt' file containing JSON representation of input arguments 'a' and 'b', and their respective values - sentences to compare.

Example of input file content:

```
{"a": "He said the foodservice pie business doesn 't fit the company 's long-term growth strategy .", "b": "The foodservice pie business does not fit our long-term growth strategy ."}
```

You can call the service from SingularityNET CLI (`snet`).

Assuming that you have an open channel (`id: 0`) to this service:

```
$ snet client call 0 0.1 bss.naint.tech ss_bert samples/sample.txt

Read call params from the file: samples/sample.txt

answer: "1"
```

## What to expect from this service?

Input data:

Sentence 1: `He said the foodservice pie business doesn 't fit the company 's long-term growth strategy .`
Sentence 2: `The foodservice pie business does not fit our long-term growth strategy .`

Response:
`answer: "1"` (similar)

Input data:

Sentence 1: `Magnarelli said Racicot hated the Iraqi regime and looked forward to using his long years of training in the war .`

Sentence 2: `His wife said he was " 100 percent behind George Bush " and looked forward to using his years of training in the war .`

Response:
`answer: "0"` (distant)

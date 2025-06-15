# Multi-Species Codon Transformer

A unified transformer model for cross-species codon optimization that generates optimized DNA sequences from protein inputs using species-specific codon usage patterns.

## Overview

The Multi-Species Codon Transformer addresses the challenge of codon optimization across different organisms by conditioning codon generation on both protein context and target species. Unlike existing models that require separate optimizers for each species, our approach uses a single unified model that can optimize codons for multiple organisms simultaneously.

## Model Architecture

The model extends CodonBERT with additional biological context through:

1. **Codon Embeddings**: Pretrained CodonBERT token representations
2. **Amino Acid Embeddings**: Learned representations for each amino acid
3. **Species Embeddings**: Organism-specific context vectors
4. **DNA+Protein Tokenization**: It takes the protein into context along with the DNA

### Vocabulary Expansion
Extended CodonBERT vocabulary with:
- 37 additional codon tokens
- 5 organism-specific tokens
- 20 amino acid tokens
- Standard BERT special tokens ([CLS], [SEP], [MASK], [UNK])

### Input Format
```
[CLS] [SPECIES_TOKEN] [CODON_SEQUENCE] [SEP] [AMINO_ACID_SEQUENCE] [SEP]
```

## Dataset

Training data derived from CodonTransformer dataset with focus on top 5 organisms:
- **Homo sapiens**: 111,997 sequences
- **Nicotiana tabacum**: 69,642 sequences  
- **Mus musculus**: 68,447 sequences
- **Danio rerio**: 47,006 sequences
- **Arabidopsis thaliana**: 40,558 sequences

### Data Split
- **Training**: 80,000 entries (20k per organism)
- **Validation**: 20,000 entries (4k per organism)
- **Test**: 30,000 entries (randomly picked)

## Training
Masked language modelling technique was used to train the model.

### Hyperparameters
- **Epochs**: 15
- **Learning Rate**: 2.41e-4
- **Batch Size**: 32
- **Weight Decay**: 0.193
- **Warmup Ratio**: 0.1
- **Scheduler**: Linear

## Results
### Performance Metrics
- **Training Loss**: 2.153
- **Validation Loss**: 2.140
- **Training Perplexity**: 8.61
- **Validation Perplexity**: 8.50
- **Test Perplexity**: 8.52

<!-- ### Key Features

- **Multi-species support**: Single model handles codon optimization for multiple organisms
- **Bidirectional optimization**: Uses masked language modeling for context-aware codon selection
- **Species-conditional generation**: Incorporates species embeddings for organism-specific codon bias
- **DNA-Protein tokenization**: Novel dual-input scheme capturing amino acid-codon relationships
- **Extensible architecture**: Easy fine-tuning for new species or tissue-specific preferences -->


## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Built upon [CodonBERT](https://huggingface.co/lhallee/CodonBERT) by Hallee et al.
- Dataset derived from [CodonTransformer](https://github.com/Allahpour/CodonTransformer) repository
- Inspired by recent advances in protein language modeling and codon optimization

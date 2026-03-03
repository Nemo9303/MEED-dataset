# MEED-dataset

MEED (Multimodal Epistemic Emotion Dataset) is a multimodal emotional dataset collected from authentic face-to-face Collaborative Problem Solving (CPS) learning environments.

The dataset captures natural student interactions during group-based problem-solving tasks and provides temporally aligned multimodal features at the utterance level.

Modalities Included

👁 Visual modality – video-derived behavioral features

🎙 Acoustic modality – speech-based acoustic features

💬 Text modality – utterance-level transcripts and text embeddings

All modalities are strictly aligned along the temporal dimension and segmented at the dialogue-utterance level.

Each utterance is annotated into one of five epistemic emotion categories.

| Label ID | Emotion Category |
| -------- | ---------------- |
| 0        | Neutral          |
| 1        | Delight          |
| 2        | Curiosity        |
| 3        | Confusion        |
| 4        | Frustration      |


These categories are grounded in epistemic emotion theories and reflect students' emotional states during knowledge construction and problem-solving.

The dataset statistics are summarized in the table below.

| Split      | Dialogue | Utterance | Neutral | Delight | Curiosity | Confusion | Frustration |
|------------|----------|-----------|---------|----------|------------|------------|--------------|
| Total      | 210      | 2995      | 1625    | 657      | 299        | 305        | 109          |
| Train_Set  | 168      | 2393      | 1300    | 526      | 238        | 244        | 85           |
| Test_Set   | 42       | 602       | 325     | 131      | 61         | 61         | 34           |

The dataset supports:

- Unimodal emotion recognition

- Multimodal fusion modeling

- Multi-turn dialogue-level emotion dynamics modeling

- Cognitive-affective interaction research

Due to the privacy-sensitive nature of educational data, raw video, audiodata are not publicly released. 
Instead, we provide anonymized and pre-extracted multimodal feature representations stored in: `multimodal_features.pkl`

The data could be loaded using code below:
```python
import pickle

videoIDs, videoSpeakers, videoLabels, videoText, videoAudio, videoVisual, videoSentence,trainVid, testVid = pickle.load(
            open('multimodal_features.pkl', 'rb'))
```

The descriptions of each variable are provided in the table below.

### Data Dictionary

| Variable Name   | Type | Description | Feature Dimension |
|----------------|------|-------------|-------------------|
| `videoIDs`     | dict | A dictionary describing dialogue structure. Keys are `DialogueID`. Values are lists formatted as `DialogueID-UtteranceID-SpeakerID`. The length of each list equals the number of utterances in that dialogue. | — |
| `videoSpeakers`| dict | A dictionary describing speaker information for each dialogue. Keys are `DialogueID`, and values are lists of `SpeakerID` corresponding to each utterance. | — |
| `videoLabels`  | dict | A dictionary containing epistemic emotion labels. Keys are `DialogueID`, and values are lists of emotion labels aligned at the utterance level. | 5 emotion classes |
| `videoText`    | dict | Text modality features extracted using **BERT-Large**. Each utterance is represented as a 1024-dimensional embedding vector. | 1024 |
| `videoAudio`   | dict | Acoustic modality features extracted using **OpenSMILE**. Each utterance is represented as a 1582-dimensional feature vector. | 1582 |
| `videoVisual`  | dict | Visual modality features extracted using **ResNet**. Each utterance is represented as a 512-dimensional feature vector. | 512 |
| `videoSentence`| dict | Raw textual transcripts for each dialogue at the utterance level. | — |
| `trainVid`     | list | List of `DialogueID`s included in the training set. | — |
| `testVid`      | list | List of `DialogueID`s included in the test set. | — |

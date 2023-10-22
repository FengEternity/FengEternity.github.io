---
title: "Efficient Prompt Tuning for Vision and Language Models"
collection: publications
permalink: /publication/2023-11-20-Efficient_Prompt_Tuning_for_Vision_and_Language_Models
# excerpt: 'This paper is about the number 1. The number 2 is left for future work.'
date: 2023-11-20
venue: '20 November'
paperurl: 'https://fengeternity.github.io/files/Efficient_Prompt_Tuning_for_Vision_and_Language_Models.pdf'
# citation: 'Feng Li, You. (2009). &quot;Paper Title Number 1.&quot; <i>Journal 1</i>. 1(1).'
---

**Abstract:** Recently, large-scale pre-trained visual language models have demonstrated excellent performance in many downstream tasks. A more efficient adapta-tion method for different downstream tasks is prompt tuning, which fixes the parameters of the visual language model and adjusts only prompt pa-rameters in the process of adapting the downstream tasks, using the knowledge learned by the visual language model during pre-training to solve the problems in the down-stream tasks. However, the loss of the downstream task and the original loss of the visual language model are not exactly same during model training. For example, CLIP uses contrast learn-ing loss to train the model, while the downstream image classification task uses the cross-entropy loss commonly used in classification problems. Dif-ferent loss has different guiding effects on the task. The trend of the accura-cy of the visual language model task during training is also different from that with the downstream task. The choice of an appropriate loss function and a reasonable prompt tuning method have a great impact on the perfor-mance of the model. Therefore, we pro-pose a more efficient method of prompt tuning for CLIP, experiments on 11 datasets demonstrate that our method  achieves better performance and faster convergence in the down-stream task.

[Download paper here](https://fengeternity.github.io/files/Efficient_Prompt_Tuning_for_Vision_and_Language_Models.pdf)

<!-- 
Recommended citation: Your Name, You. (2009). "Paper Title Number 1." <i>Journal 1</i>. 1(1). -->
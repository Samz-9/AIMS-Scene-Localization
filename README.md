# Scene Localization in Dense Images via Natural Language Queries

## 1. Introduction
In many real-world applications such as surveillance, autonomous systems, and contextual visual analytics, dense scenes often contain multiple simultaneous activities. This project aims to build a system that can identify and localize specific sub-scenes within a single dense image based on a natural language query describing one of the events occurring in the scene. Given a high-resolution image depicting multiple activities (e.g., a street market, a park, a railway station), and a textual description such as "a person snatching a chain" or "a vendor selling vegetables to a customer," the model must output a cropped image region that semantically corresponds to the input description.

***

## 2. Project Journey & Challenges

This project's development has been a journey of experimentation with various state-of-the-art vision-language models. The primary challenge lies in the complexity of the "sub-scene" task, which requires a model to understand not just objects but the semantic relationships and actions between them. Standard object detection models are insufficient for this purpose.

### **Initial Attempts**
The first approach involved a zero-shot inference with pre-trained models, without any custom training:

* **OWL-ViT**: A Vision Transformer model designed for open-vocabulary object detection. While powerful for general objects, it struggled with the nuanced, action-based queries required for sub-scene localization.
* **CLIP (Single Query)**: A powerful model for text-image similarity. However, it provides a similarity score for the entire image, not a localized bounding box, making it unsuitable for this specific task.

### **Custom Model Training**
Recognizing the limitations of zero-shot approaches, the next step was to train a custom model:

* A model was trained on a small, custom dataset of 1,000 images.
* The model showed some promise but failed to produce good bounding boxes due to the limited size of the training data. The model struggled to generalize and often returned imprecise localizations.

### **Advanced Model Exploration**
In the final stages, more advanced vision-language models were explored:

* **MDETR**: An end-to-end model for vision-and-language understanding. The implementation proved to be highly challenging, with numerous technical issues encountered during fine-tuning.
* **Grounding DINO**: A cutting-edge model for open-vocabulary object detection and grounding. Despite its potential, significant challenges were faced during implementation and fine-tuning, preventing the model from being successfully used.

***

## 3. Dataset

A custom dataset was created to support this project's fine-tuning attempts. The images and annotations were meticulously extracted and curated from two large-scale datasets:

* **COCO (Common Objects in Context)**: Provided the rich, dense images with multiple objects.
* **RefCOCOg**: A dataset for referring expression comprehension, providing the natural language descriptions of objects and their corresponding bounding boxes.

***

## 4. Conclusion & Future Work

This project represents a comprehensive exploration of scene localization via natural language queries. While a robust, working model has yet to be achieved, the journey has provided valuable insights into the challenges of fine-tuning advanced models on small-scale datasets for complex tasks.

**Future work will focus on:**
* Revisiting the **Grounding DINO** implementation with a more robust training environment and refined configuration.
* Expanding the custom dataset to improve the model's ability to generalize and produce accurate bounding boxes.
* Exploring alternative methods for scene localization, such as fine-tuning models on video data to learn about temporal actions.
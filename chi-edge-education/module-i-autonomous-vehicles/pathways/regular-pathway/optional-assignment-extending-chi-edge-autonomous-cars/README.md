---
description: >-
  An example of stepping beyond the educational module and into the domain of
  exploration.
---

# Assignment: Extending CHI@Edge Autonomous Cars

## Introduction to Assignment

As stated previously, the purpose of this educational module is to act as a jumping-off point for future students and scientists. On this page, an extension assignment that shows how this module can be utilized for jumping off is presented. This project utilizes various models intrinsic to Donkeycar and compares them with one another.

This is an independent assignment for the student and requires deeper understanding of the material beyond just implementation and copy pasting the UNIX commands. Even then, we have taken the liberty to gather the required resources for this assignment. However, as this assignment is supposed to solidify the learner's understanding, there is relatively little hand-holding beyond the resources provided and a brief explication of how to use these resources.

### Required Reading and Documents

1. [Donkeycar Keras Documentation](https://docs.donkeycar.com/parts/keras/)
2. [Donkeycar Command Line Utilities](https://docs.donkeycar.com/utility/donkey/)
3. [Keras File](https://github.com/autorope/donkeycar/blob/5e234c3101cc5f54935c240819e3840596c753a3/donkeycar/parts/keras.py#L976)&#x20;
4. [Donkeycar Guide to Keras Models (Building your own)](https://docs.donkeycar.com/dev\_guide/model/)

## Instructions

In this assignment, you will review and refine all of the knowledge that you have gained through this educational module on Autonomous cars. This assignment is not a large jump from what you have already accomplished thus far.

The end goal of this assignment is to give you (the learner) a chance to do things on their own, reading community maintained code and documentation, but without dumping them unprepared into a sea of code.

You will gain the most by thinking deeply about what you are actually changing and its implications on the car. Read the **Required Readings and Documents** very carefully.

There are a total of 8 usable in-built Keras mode. Compare them with one another and create a short paper describing differences between the various models.

### Questions to Answer

1. How long does it take to train each model?
2. How many records were used for training?
3. Which data augmentations and transformations were used and why?
4. When running the models, how long did they run before running off the track or crashing (this is the episode time)?
5. How does the validation loss compare for each model type?
6. Which model is the best? Why?&#x20;
   * Are there limitations to this model and if yes, show them with data-driven visualizations?
   * Are there situations where a worse model becomes more preferable? Support this with quantitative data.

### Things to Figure Out

1. Which models can you even utilize?
2. How can you create data-driven visualizations?&#x20;
   * Is there a command for that?
   * &#x20;How is it used?
3. How can you add additional augmentations and transformations?


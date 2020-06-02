# Automated Data Visualization for COVID patient and virus data
## Automatically translate tabular data on patients and virus strains into graphs and charts for clinicians treating COVID-19 patients

### Need
COVID-19 cases vary in severity and clinical need from person to person, and even among people with similar ages and comorbidities. We are only beginning to understand the causes drive how the disease is expressed in a given patient. There is some emergent evidence that genetic differences bewteen patients interact with differently with different strains of the COVID-19 virus. And those interact with patient age, history, and comobidities.  

A visual representation of the patient's (and the virus') data can help clinicians make life-saving decisions. But visualizing this data takes time: selecting the most important fields, transforming and scaling data, selecting a useful chart type, selecting colors, etc. This is generally repetitive but highly skilled work. 

In this consulting project, the aim is to build a model that takes tabular data on patient and virus genomics in a variety of formats and automatically generates the most appropriate visualization (or set of visualizations) for the clinician. 

### Approach
Data2Vis ([github](https://github.com/victordibia/data2vis), [paper](https://arxiv.org/abs/1804.03126)) provides a precident for automatically translating tabular data into visualizations. I intend to modify Data2Vis for this purpose, specifically, to understand and generate visualizations of genomic data as well as other tabular data.  

Data2Vis in turn implements [seq2seq](https://github.com/google/seq2seq), a general model for translating a sequence of one thing to a sequence of another thing. It is a recurrent neural network, and the cannonical application is language translation. It runs on TensorFlow.

In the case of data2vis, the input is tabular data and the output are attributes of a chart: the most important data fields, the type of chart, data transformations and scales, colors, labels, etc.  Those chart attributes are then translated into a visualization grammer, like seaborn, ggplot2, D3, etc. Here is the model architecture, lifted from the data2vis github page: 

![data2vis architecture](https://github.com/victordibia/data2vis/blob/master/static/assets/datatransform.jpg?raw=true)

I've run into some difficulty so far in getting data2vis to run -- it requires old versions of TensorFlow, Python, and more, and setting up a compatible environment is tedious. Also, using more recent software will be more useful for the client. Finally, the old versions prohibit using google colab.
Right now, we're leaning towards building an LSTM model from scratch and training it on the same data sources as Data2Vis. 

### Outcome
We're trying for a working model capable of generating 6 different kinds of charts from diverse data inputs. 
A *minimum viable product* (1) identifies chart type and (2) selects features to chart. 
Client has requested that I focus on getting a model working and not on putting it into production. 
However, I'll want to make a compelling demo.  The data is private patient data and under NDA but I have written permission to share both the trained model and source code.

### Steps and things to try
- fork data2vis and get it working on example data, and some of my past research data
- try it out with some of the collaborative COVID data that the client has (this won't show up on github!) 
- train a model on client's training data
- transfer learning to adapt trained data2vis model to client's training data, compare to model trained on client's data alone
- validate model on collaborative COVID data 
- get clinician feedback on visualizations? 
- integrate model into client's pipeline
- create a toy version that doesn't need identifiable patient data to demonstrate the model to insight, companies

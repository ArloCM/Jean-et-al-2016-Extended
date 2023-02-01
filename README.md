# Jean-et-al-2016-Extended

Arlo Malmberg
Reproducing Jean et al.

Idea
In the journal Science, Jean et al (2016) document how they used transfer learning to extend a convolutional neural network (CNN) pretrained on the ImageNet dataset to predict wealth (as measured by nightlights and surveys) from daytime satellite photos. The paper maps poverty for 5 African countries. My idea is to reproduce their results on a different country: Panama. Panama is an interesting place to measure wealth because of the vast range of wealth levels it contains. Data is available (see below) and while the paper’s method is advanced, it is well documented for purposes of replicability. My first understanding of the process for this project would be as follows:
1. Use the first few layers of the pretrained CNN to take in daytime images and predict the nighttime light intensity
2. Regress daytime images on survey data and features extracted by the CNN from nighttime images
An easier reroute could be to combine the nighttime light intensities and survey data into a composite score and map that field.

Data
I will need three datasets (source):
• Survey data on consumption expenditure and asset wealth
• Nighttime satellite images (National Geophysical Data Center)
• Daytime satellite images (Google Static Maps API or Sentinel Hub API or Planet API)
Potential Problems
• Expertise. I’m not 100% percent sure I know how to do this, but I am also taking a machine learning class (INFO 254) that will be a resource for me.
• Compute. I’m hoping Panama’s small size will reduce the time it takes to train the model. If this turns out to be a problem then maybe I can just pick a province.
• Cost of API access. Sentinel is free but Planet might be higher quality and easier to use. Luckily Planet offers a 14-day free trial that might be sufficient.

Motivation
Since doing an image recognition project last semester, I have been interested in the potential of neural networks to extract new information from images. Having spent three years in rural Panama with the Peace Corps, I have a deep interest in poor rural communities. Remote sensing presents an enormously rich dataset and Jean et al. (2016) combines neural networks and remote sensing to make important insights into the consumption levels of poor rural communities. I took on this project in order to push myself to learn more about neural networks while diving into a subject area that I am personally invested in.

Method
The methods used in Jean et al. are not state of the art and can be implemented in Python using widely-used open-source packages; they are, however, on the limits of my personal understanding and completing the project contributed greatly to my learning. The methodology can be broken down into the following steps: 1) data collection; 2) feature extraction; 3) dimensionality reduction; and 4) transfer learning.
Data Collection
Following in the direction of the original authors, I collected over 50,000 satellite images from the Google Maps API. The images covered
Feature Extraction
	Convolutional neural networks can be used to extract a matrix of features from images.
Transfer Learning
	One of the exciting insights of this paper was the demonstration that we can use models pretrained on rote image classification tasks to perform on domain-specific tasks; in this case, predicting consumption levels from daytime satellite images.
Dimensionality Reduction
	The final prediction of consumption is done with a relatively simple ridge regression. To prepare the data for this final step, the authors perform a principle component analysis to reduce the dimensionality of the data, in this case to 100 features. 
Further Exploration
	My conceptual understanding, Python aptitude and available time were stretched to their respective limits by the basic replication task. I was, however, left with two questions that I would love to explore when I get the chance: 1. Is it efficient to use a model pretrained (by the method described above) to predict consumption levels in Africa to predict consumption in other poor rural regions of the world? And 2. How can we incorporate data that give context to the daytime satellite images into the model?
	Question 1. essentially asks if the variation of consumption levels across the globe always looks the same from space. One can imagine a region of the world where zinc roofs are more widely distributed across wealth levels, or where paved roads are prevalent (or not) due to long ago government investment that does not reflect accurately on current consumption levels.
	Question 2. is sparked by a personal experience of mine: when I was in the Peace Corps, I travelled to dozens of poor rural towns to work with those communities for a period of days or weeks. While learning to use the Google Maps API I downloaded images from a few of these towns and was struck by how indistinguishable they were. This impression was later borne out by predicting consumption levels on those images with the final model.

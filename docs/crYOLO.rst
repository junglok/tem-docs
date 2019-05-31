******
CrYOLO
******
CrYOLO is a fast and accurate particle picking procedure. It's based on convolutional neural networks and utilizes the popular You Only Look Once (YOLO) object detection system.
(from http://sphire.mpg.de/wiki/doku.php?id=pipeline:window:cryolo)

* crYOLO makes picking fast – On a modern GPU it will pick your particles at up to 6 micrographs per second.
* crYOLO makes picking smart – The network learns the context of particles (e.g. not to pick particles on carbon or within ice contamination )
* crYOLO makes training easy – You might use a general network model and skip training completely. However, if the general model doesn't give you satisfactory results or if you would like to improve them, you might want to train a specialized model specific for your data set by selecting particles (no selection of negative examples necessary) on a small number of micrographs.
* crYOLO makes training tolerant – Don't worry if you miss quite a lot particles during creation of your training set. crYOLO will still do the job.

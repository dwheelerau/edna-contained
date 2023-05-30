# The eDNA-container app

## Introduction
A Docker image containing a eDNA/amplicon pipeline based on
[QIIME2](https://qiime2.org/). The pipeline is controlled via flask GUI that runs
in the users browser.   

**The advantages of the pipeline are:**  
- simple to setup and run using point and click with a browser based GUI
- should run on any machine where [Docker-desktop](https://www.docker.com/products/docker-desktop/) can be installed
- adaptable to any primer combination or taxonomic database
- snakemake is used to confirm successful completion of each stage of the pipeline
- species summary tables with counts are created, including the ASV sequence for manual confirmation of the taxonomic classification
- rarefaction and taxonomic barplots are generated that can be viewed using the [QIIME viewer](https://view.qiime2.org/) (drag and drop)
- A PDF report is generated containing QC plots and important information about the ASV generation so that QC parameters can be optimised 

The pipeline can also be used without Docker as described at this [repo](https://bitbucket.org/dpi_data_analytics/snakemake-qiime-edna/src/master/).  

## Running the image in a container on Windows
Ensure that the Docker-desktop app is installed on your windows computer. The
offical guide for installing Docker-desktop can be found [here](https://docs.docker.com/desktop/install/windows-install/).
If you run into any issues a more complete guide is available
[here](https://github.com/dwheelerau/docker-guide).  

1. Start by opening the Docker-desktop app.  
2. In the search bar at the top of the page search for `dwheelerau/edna`, then use the "Pull"
button to obtain a copy of the pipeline image.  
![Search dockerhub for the pipeline image under "dwheelerau/edna"](images/dh1.PNG)

3. After the image has downloaded click the "Run" button.  
![Start a container using the Run button](images/dh2.PNG)

4. Use the "Optional settings" drop down to open host port 5000 as shown in the image
below, then click "Run".  
![Add 5000 to the "Host port" option](images/dh3.PNG)

5. The log section of the container should look like the image below, this is showning the IP
address for The eDNA-container app user interface, click on the top link or type `http://127.0.0.1:5000`
in an internet browser (**Note:** No data is transfered over the internet, the pipeline will
run using the local computer resources).
![Click on the top link to open the user interface in a browser window](iamges/dh4.PNG)

6. Please wait a few seconds while the pipeline setup beings, if this has been successful the
following screen should display.
![The eDNA-container app welcome screen](images/dh5.PNG)

Follow the instructions below to carry out an eDNA analysis using the pipeline. **Note** for
future runs on the pipeline all that is required is to click the "Play" Button next to the 
container ID in the Docker-desktop app. Remember to shutdown the container using the "Stop"
button to free up system resources after you have completed the analysis.

## Analysing paired-end sequencing data using The eDNA-container app  
The pipeline is currently only configured to process paired-end fastq.gz sequencing files.
Ensure that only the files you wish to analyse are in their own directory.

1. Using the browser based user interface select the folder of fastq.gz files that you wish to process.
![Select the sequencing folder using the file explorer dialogue]()

2. Click the "Process folder" button.
3. The next page is the settings page, the following table details each option

```
table
```

## Running the pipeline using terminal commands  
```
docker pull dwheelerau/edna:edna
```
Downloading the image (~7GB) will take some time depending on your internet connnection.

4. The image should appear in your Docker desktop app under the 'images' section (see screen shot below). 
Click the copy icon next to the iamge id code as shown below (this code will be used in the next command). 

![Use the copy icon to copy the image ID for dwheelerau/edna](images/image1.PNG).

5. Type the following command in the terminal window replacing "IMAGEID"
with the code you copied above (you can "paste" by right clicking on the command prompt window boarder
and selecting edit->paste).
```
docker run -p 80:5000 --rm IMAGEID
```
![The bottom run command uses the IMAGEID to run the container](images/image2.PNG)

6. Open a internet browser (we recommend chrome or firebox) and enter the following IP address  
```
http://127.0.0.1:80
```
The following window should open (after a short wait for the app to start). Any errors during 
the run should appear in the command prompt window.
![The start screen](images/image3.PNG)

7. Using the 'select' or 'browse' button select the folder where the fastq.gz sequencing files for this project are located and accept the image upload dialogue.
![Click accept](images/image4.PNG)

8. Click 'process folder' button and update the settings on the next page as required (the default if the telo fish eDNA primers)
![Modify the run-time paramaters as required](images/image7.PNG)

9. When you are ready use the 'Run pipeline!' button to run the application on your data (the progress will be logged to the command prompt terminal window).
![Progress as well as errors will be logged to the command prompt screen](images/image5.PNG)

10. A running screen will be replaced by a download link to the results (zipped folder). Any errors will be reported in the command prompt window.
![Analysis completed](images/image6.PNG) 

If you wish to re-use the pipeline in the future, simply open the Docker-desktop app and follow the instructions from Step 5.

## Running the image in a container on Linux
1. Make sure you have Docker installed on your OS
2. Pull the image from a terminal window
```
docker pull dwheelerau/edna:edna
```
3. Find out the image ID using
```
docker images
```
4. Run the image replacing IMAGEID with the number in the first column from the above command.
```
docker run -p 80:5000 --rm IMAGEID
```
5. Open a firefox/chrome browser window and naviate to the following IP address  (or localhost on port 80):
```
http://127.0.0.1:80
```
The app should open in the browser after a short delay. Any errors during pipeline running 
should appear in the terminal window.

6. Follow the instructions from step 7 in the windows section above.

## Building the latest version of the pipeline
Quick start after cloning this repository:
```
cd edna-contained
sudo docker build -f Dockerfile . -t dwheelerau/edna:edna
```
Once the image is stored on your computer the `docker run` command can be used to run the app.

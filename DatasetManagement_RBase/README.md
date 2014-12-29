
// How to Download Yahoo! Research 10 Category Dataset
// Eric F. Johnson
// Columbia University 2014 - Big Data Analytics
// December 18, 2014

These installation instructions assume that you are familiar with using R-Base or R-Studio.  Please note that it 
is possible to do this download using alternate programs such as Python, Java, or C++ however we chose to use R for its
simplicity and widespread use.  Please note that we have also provided our own version of the text 
file that Yahoo Research provided with image IDs and URLs.  We chose to do this because the original file 
had a great dead of formatting issues that we were only able to avoid after first importing the text as a FWF
(fixed width format) and then cleaning the data as needed.  This file we provided (download.txt) shows the 
text after our cleaning and will save the user a great deal of time and frustration that we faced when first starting
this project.

Please note that these instructions are designed for R-Base which is the terminal based
version of R for Ubuntu and OS X and since we noticed signification performance issues
when using R-Studio. If you for some reason would prefer to use R-Studio you can use the
same command prompts on that version of R but you should not attempt to run more than 4
instances of R-Studio simultaneously because it will most likely crash your machine.

1) Install R-Base

Ubuntu Instructions of R-Base
	Press Ctrl+Alt+T to open Terminal
	sudo apt-get update 
	sudo apt-get install r-base

// OS X Instructions of R-Base
R-base comes preinstalled on the newer versions of OS X

2) Install the “RCurl” Package of R-Base

	install.packages(“RCurl”)

3) Run Curl

	library(“RCurl”)

4) Importing the URL File we provided (downloads.txt) 

	url <- "";	
	id <- "";
	output <- "";
	download <- read.delim("~/Desktop/download.txt", stringsAsFactors=FALSE);

5) Download Images to Local Directory 

// Here you can specify the start and stop using the for loop and the start:stop parameters 
we noticed the best success when downloading he images in groups of 20,000. Please note that although
OS X and Ubuntu are designed to hold up to 4 million files in a single folder that this is very resource 
intensive and will lock up your system. The biggest problem we noticed aside from the amount of time 
that it takes to download the images is actually managing the files themselves. We recommend you 
DO NOT try to open any of the folder that contact these images, it WILL FREEZE your system.  Instead 
you should manage and move the files through command line ONLY.  This can all be down through R or terminal 
by reading the contents of the folders into memory as a vector and then accessing the appropriate index as 
necessary.  If you chose to make your folders only contain 20k or fewer images you will not notice a substantial 
UI problem but if you chose to group them into larger groups as we did (making 3 main folders with 500,000 images in 
each folder) you will DEFINITELY crash your machine when you try to open a single folder.  DO NOT DO THIS

// We recommend downloading the 1.5 million Training Images into 3 folders, each having 500,000 images the best way of
doing this is to run 20 instance of R-Base in 20 different windows/threads of Terminal. If you do this you can expect the
downloads to complete in a little longer than 48 hrs of continuous downloading. As we stated in our presentation we actually 
destroyed a 2011 Macbook Pro by overheating it from 2 days of continous downloading.  We highly recommend that you try 
doing this on a desktop computer instead which will have sufficient cooling power to manager the task.

******************* PLEASE DO NOT DO THIS ON A LAPTOP - YOU WILL OVERHEAT / DESTROY YOUR LAPTOP *********************

// Thread 1 (1 to 75,000)

for (i in 1:75000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 2 (75,001 to 150,000)

for (i in 75001:150000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 3 (150,001, to 225,000)

for (i in 150001:225000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 4 (225,001, to 300,000)

for (i in 225001:300000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 5 (300,001 to 375,000)

for (i in 300001:375000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 6 (375,001 to 450,000)

for (i in 375001:450000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 7 (450,001 to 525,000)

for (i in 450001:525000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 8 (525,001 to 600,000)

for (i in 525001:600000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 9 (600,001 to 675,000)

for (i in 600001 to 675,000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 10 (675,001 to 750,000)

for (i in 675001:750000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 11 (750,001 to 825,000)

for (i in 750001:825000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 12 (825,001 to 900,000)

for (i in 825001:900000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 13 (900,001 to 975,000)

for (i in 900000:975000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 14 (975,001 to 1,050,000)

for (i in 975001:1050000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 14 (1,050,001 to 1,125,000)

for (i in 1050001:1125000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 15 (1,125,001 to 1,200,000)

for (i in 1125001:1200000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 16 (1,200,001 to 1,275,000)

for (i in 1200001:1275000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 17 (1,275,001 to 1,325,000)

for (i in 1275001:1325000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 18 (1,325,001 to 1,400,000)

for (i in 1325001:1400000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 19 (1,400,001 to 1,475,000)

for (i in 1400001:1475000) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Thread 20 (1,475,001 to 1,500,000)

for (i in 1475001:length(download$ids)) {
        url <- download$urls[[i]];
        id <- download$ids[[i]];
        output <- paste("/Volumes/Takadatsu/YahooDataSet/Training/D1/“,  id, ".jpg", sep= "");
        download.file(url, output, "auto", quiet = FALSE, mode = "w", cacheOK = TRUE, extra = getOption("download.file.extra"));
        print(i);
}

// Please note that the 1.5 million training images will require approximately 100 GB of free storage and 50 hours of continuous internet connection
depending on these connection speed your computer has.  As already stately we highly recommend you DO NO DO THIS ON A LAPTOP COMPUTER and only 
start this downloading on a SERVER or PROPERLY COOLED DESKTOP. 
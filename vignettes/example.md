---
title: "A Worked Out Example of Managing with abbyyR"
author: "Gaurav Sood"
date: "2016-05-15"
vignette: >
  %\VignetteIndexEntry{A Worked Out Example of Managing with abbyyR}
  %\VignetteEngine{knitr::rmarkdown}
  %\VignetteEncoding{UTF-8}
---

#### Load the package

To get started, load the package. The latest version of the package will always be on github. Instructions for installing the package from github are provided below.




```r
library(abbyyR)
```



```r
"
Get the latest version from github:

# install.packages('devtools')
devtools::install_github('soodoku/abbyyR')
"
```

#### Set credentials

Your first task on loading the package should be to set the credentials - application ID and password. If you haven't already, you can get this information 
[http://ocrsdk.com/](http://ocrsdk.com/). Once you have the application ID and password, set it via the `setapp` function. 



```r
setapp(c("factbook", "7YVBc8E6xMricoTwp0mF0aH"))
```

#### Get Information about Application



```r
getAppInfo()
```

```
## Name of Application: factbook
## No. of Pages Remaining: 99
## No. of Fields Remaining: 495
## Application Credits Expire on: 2015-08-28T00:00:00
## Type: Normal
```

#### List Tasks 

List all the tasks -- completed, in progress, queued etc. The function returns a data frame.



```r
tasklist <- listTasks()
```

```
## Total No. of Tasks:  30 
## No. of Finished Tasks:  22
```


```r
listTasks(excludeDeleted="true")
```

```
## Total No. of Tasks:  28 
## No. of Finished Tasks:  22
```


```r
listTasks(fromDate="2015-05-30T20:28:43Z", toDate="2015-05-31T20:28:43Z")
```

```
## No tasks in the application.
```

#### List Finished Tasks



```r
listFinishedTasks()
```

```
## No. of Finished Tasks:  24
```

#### Get Task Status



```r
getTaskStatus(taskId="47f9b0d4-79a2-4aed-b656-2683a85ac203")
```

```
## Status of the task:  Deleted
```

#### Delete Task

Deleting an already deleted task will result in an error.



```r
#deleteTask(taskId="47f9b0d4-79a2-4aed-b656-2683a85ac203")
```

**Submit an Image for Processing**

Note: I am uploading a sample image that Abbyy provides for free to test its software. You can find this image in the data folder of the package.




```r
submitImage(file_path="t1.tif", pdfPassword="")
```

```
## Status of the task:  Submitted 
## Task ID:  4c088272-003d-4fc7-b0f7-b805495c4466
```

**Process an Image**



```r
processImage(file_path="t1.tif")
```

```
## Status of the task:  Queued 
## Task ID:  650d4cd3-964c-40c6-9118-97eecc099b34
```

**Process a Remote Image**



```r
processRemoteImage(img_url="https://raw.githubusercontent.com/soodoku/abbyyR/master/inst/extdata/t1.TIF")
```

```
## Status of the task:  Submitted 
## Task ID:  7f5112b8-6541-435e-86c4-dc978a45749e
```

**Process Document**



```r
res <- listTasks()
```

```
## Total No. of Tasks:  33 
## No. of Finished Tasks:  23
```


```r
processDocument(taskId=res$id[res$status=="Submitted"][1])
```

```
## Status of the task:  Queued
```

**Get Results**

Go through all the finished tasks and download all the data.



```r
# getResults()
```

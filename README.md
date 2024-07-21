Videos are usually downloaded and embedded in web-broswer, but not all web sites allow us to save the videos for later use. In this project, we discuss how to save any embedded videos. We discuss the process to analyze browser network traffic to retrieve the downloaded video segments and re-encode them into a viewable format. The re-encoded video is a single file that could be saved for our own purpose.

### Step 1 - Locate video segment files
Videos are typically segmented following DASH protocols. Each file is individually downloaded by the browswer and could be monitored/accessed using inspect tool.

Locate the web element encapsulating the embedded video. Try to isolate the network traffic where the content of the target tag is transferred. For instance, only begin capturing network traffic right before the play button is pressed.

+ Navigate to the Network Tab. Reload the page with the Developer Tools open to begin recording the network activity. Make sure the Network tab is selected.
+ Filter for Media Files. Use the filter tool within the Network tab and select "Media" to see only the video and audio files being downloaded by the browser. This is where video segments, if they are being streamed, will appear.
+ Identify and Save Video Segments: Look for files with extensions typically used for video segments, such as .ts, .mp4, or .m4s. We can right-click on a file in the list and select "Open in new tab" or "Copy link address" to access the file directly.
+ Here is a potential location to access the files in Windows: C:\Users\[Username]\AppData\Local\Google\Chrome\User Data\Default\Cache


### Step 2 - concatenate files together and encode in viewable format such as mp4.

+ Create a file list. Create a text file listing all the segments in the order they should be concatenated. We can do this manually or using a script. Here's an example how the file (filelist.txt) should look like:

```
file 'segment1.ts'
file 'segment2.ts'
file 'segment3.ts'
```

Use ffmpeg to concatenate them into a single `mp4` file:
```
ffmpeg -f concat -safe 0 -i filelist.txt -c copy output.mp4
```

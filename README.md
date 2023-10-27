## Video_Caption_Summary 

📺 Software concept for summarizing YouTube video captions.

### CONCEPT

Summarizing YouTube video captions into a video description.

![Video_Caption_Summary](https://github.com/sourceduty/Video_Caption_Summary/assets/123030236/f84e474b-819f-4c7e-b1fc-0f20a0cae558)

### FEATURES

- Automatic YouTube video descriptions.

### CHATGPT CONCEPT

Set up a YouTube Data API key:

a. Go to the Google Cloud Console (https://console.cloud.google.com/).

b. Create a new project.

c. Enable the YouTube Data API for the project.

d. Create credentials and generate an API key.

```
pip install google-api-python-client google-auth-httplib2 google-auth-oauthlib gensim nltk
```
```
import os
import googleapiclient.discovery
import gensim
from gensim.summarization import summarize
import nltk

# Set up the YouTube Data API key
api_key = "YOUR_YOUTUBE_API_KEY"
os.environ["OAUTHLIB_INSECURE_TRANSPORT"] = "1"  # For development purposes only

# Set up the YouTube Data API client
youtube = googleapiclient.discovery.build("youtube", "v3", developerKey=api_key)

def get_video_captions(video_id):
    response = youtube.captions().list(
        part="snippet",
        videoId=video_id
    ).execute()
    captions = []
    for item in response.get("items", []):
        caption_id = item["id"]
        caption = youtube.captions().download(id=caption_id).execute()
        captions.append(caption["body"])
    return " ".join(captions)

def summarize_captions(video_id):
    captions = get_video_captions(video_id)
    # You can adjust the ratio and word_count parameters for your desired summary length.
    summary = summarize(captions, ratio=0.2, word_count=200)
    return summary

if __name__ == "__main__":
    video_id = "YOUR_VIDEO_ID"  # Replace with the ID of the YouTube video you want to summarize
    summary = summarize_captions(video_id)
    print(summary)
```
Replace "YOUR_YOUTUBE_API_KEY" with your actual YouTube Data API key and "YOUR_VIDEO_ID" with the ID of the YouTube video you want to summarize.

Please note that this code uses the Gensim library for text summarization, which may not always produce perfect summaries. You may need to fine-tune the summarization parameters to achieve the desired level of brevity and coherence in the summaries.
#

### REFERENCES

[DownSub](https://downsub.com/)

[download-youtube-subtitle](https://pypi.org/project/download-youtube-subtitle/)

[Text Summarization in Python](https://www.mygreatlearning.com/blog/text-summarization-in-python/)

[ChatGPT Plugin](https://video-summary.copilot.us/)

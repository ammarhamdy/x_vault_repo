
**MIME types** (Multipurpose Internet Mail Extensions types) are a standardized way to indicate the **nature and format of a file**. 

They help software (like web browsers, email clients, or servers) understand how to handle the content being sent or received.


# Structure of a MIME Type

A MIME type has two parts, separated by a slash:
```
type/subtype
```
- **type**: The general category of the data (e.g., `text`, `image`, `audio`, `application`)
- **subtype**: The specific format of the data (e.g., `html`, `png`, `mp3`, `json`)

# Common Examples

|File Type|MIME Type|
|---|---|
|HTML|`text/html`|
|Plain text|`text/plain`|
|JSON|`application/json`|
|JavaScript|`application/javascript`|
|PNG image|`image/png`|
|JPEG image|`image/jpeg`|
|MP3 audio|`audio/mpeg`|
|MP4 video|`video/mp4`|
|PDF document|`application/pdf`|
|ZIP archive|`application/zip`|

# Why MIME Types Matter

- **Web servers** send MIME types in the `Content-Type` header to tell browsers how to render or download files.
    
- **Email clients** use MIME to handle attachments.
    
- **APIs** use them to specify data formats in requests and responses (e.g., `Content-Type: application/json`).
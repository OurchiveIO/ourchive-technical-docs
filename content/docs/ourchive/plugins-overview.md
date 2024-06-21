---
title: "Plugins"
weight: 6
---

## Search

Ourchive MVP supports Postgres searching. Ourchive 1.0 will support Elasticsearch.

Search is its own module, `ourchive_app.search`. The 'Search Provider' setting determines which provider will be used. 

## File Storage

Ourchive MVP supports local file storage. Ourchive 1.0 will support S3 through [boto3](https://github.com/boto/boto3). 

File processor selection is controlled by `settings.FILE_PROCESSOR`. With MVP, file processing is instantiated through `api.file_helpers.py`. 1.0 will move file processing into its own module, with expanded support for more processors over time.

## Audio Processing

Ourchive uses [audioread](https://github.com/beetbox/audioread) to process audio. The library supports a number of audio processors; we recommend `ffmpeg`. Because admins may not be able to install audio software on their server, we allow this capability to be disabled via the 'Audio Processing' setting. If processing is disabled, users can manually input audio length information.

As Ourchive matures to 1.0, we'll be looking at adding more advanced multimedia processing.
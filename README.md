<a href="https://www.patreon.com/stefansarya"><img src="http://anisics.stream/assets/img/support-badge.png" height="20"></a>
[![Build Status](https://travis-ci.org/StefansArya/LittleYoutube-PHP.svg?branch=master)](https://travis-ci.org/StefansArya/LittleYoutube-PHP)
[![Latest Version](https://img.shields.io/badge/build-beta-yellow.svg)](https://packagist.org/packages/scarletsfiction/littleyoutube)
[![Software License](https://img.shields.io/badge/license-GPL2-brightgreen.svg)](LICENSE)

LittleYoutube
==========

Have you ever dreamed put your own channel on your own website?
LittleYoutube is here to help you

> Note:
>   Please use this library for fair use when downloading any youtube content. If you want to display youtube video to your website, please embed youtube link rather than download it. And don't ever use this for commercial use.

## Table of contents
 - [LittleYoutube](#littleyoutube)
 - [Table of contents](#table-of-contents)
 - [Getting Started](#getting-started)
 - [Download via composer](#download-via-composer)
 - [Sample Usage](#sample-usage)
 - [Documentation](#documentation)
   - [Initialize LittleYoutube](#initialize-littleyoutube)
   - [Set youtube video URL](#set-youtube-video-url)
   - [Get video image preview](#get-video-image-preview])
   - [Get last error message](#get-last-error-message)
   - [Get embed link](#get-embed-link)
   - [Get info](#get-info)
   - [Parse subtitle](#parse-subtitle)
   - [Change settings dynamically](#change-settings-dynamically)
 - [Contribution](#contribution)
 - [License](#license)

## Getting Started
>  * Clone/download this repo
>  * Include `LittleYoutube.php` to your php script

### Download via composer

Add LittleYoutube to composer.json configuration file.
```
$ composer require scarletsfiction/littleyoutube
```

And update the composer
```
$ composer update
```

## Sample Usage
```php
<?php
    // require 'vendor/autoload.php';
    require_once "LittleYoutube.php";

    use ScarletsFiction\LittleYoutube;

    $LittleYoutube = new LittleYoutube();
    $LittleYoutube->video("https://www.youtube.com/watch?v=xQomv1gqmb4");
    echo("Video ID:".$LittleYoutube->info['videoID']."\n");
    print_r($LittleYoutube->getVideoImages());
```

## Documentation
### Initialize LittleYoutube
> $LittleYoutube = new LittleYoutube(options);

Available options
```
{
    "temporaryDirectory"=>realpath(__DIR__."/temp"),
    "signatureDebug"=>false,
    "loadVideoSize"=>false
}
```

### Init youtube video
> $video = $LittleYoutube->videoID("videoURLHere", ProcessDetails=true);

Return video class

#### Get video map
> $video->info['video'];
>>  Not available when ProcessDetails = false
>> You can also call $video->processDetails() to refresh data

Return Associative Arrays
```
{
    "encoded"=>[
        [0] => {
            "itag",
            "type"=>[
                [0] => Media    //video
                [1] => Format   //mp4
                [2] => Encoder  //avc1.64001F, mp4a.40.2
            ],
            "expire",  //timestamp
            "quality", //hd720, medium, small
            "url",
            "size" //When loadVideoSize was enabled
        },
        ...
    ],
    "adaptive"=>[
        [0] => {
            "itag",
            "type"=>[
                [0] => Media    //video
                [1] => Format   //mp4
                [2] => Encoder  //avc1.4d401f
            ],
            "expire",  //timestamp
            "quality", //1080p, 720p, 192k, 144k
            "url",
            "size" //When loadVideoSize was enabled
        },
        ...
    ]
}
```

#### Get video image preview
> $video->getVideoImages();

Return Indexed Array
```
[ "HighQualityURL", "MediumQualityURL", "DefaultQualityURL" ]
```

#### Get embed link
> $video->getEmbedLink();

```
// Usually we will wrap it with iframe

echo('<iframe width="480" height="360" src="'.$LittleYoutube->getEmbedLink().'" frameborder="0" allowfullscreen></iframe>');
```

#### Parse subtitle
> $video->parseSubtitle(args);
>>  args: subtitle index or xml string
>>  note: if you pass subtitle index, ProcessDetails must be enabled/called

```
[
    [0]=>[
        [time] => 1.31,
        [duration] => 6.609,
        [text]=>"in a single lifetime we can take a days"
    ],
    ...
]
```

#### Get info
> $video->info;

Return Associative Array of current video info
```
{ "videoID",

//When ProcessDetail was enabled/called
"playerID", "title", "duration", "viewCount", "like", "dislike", "author", "video" "subtitle", "uploaded", "description", "metatag", "channelID",

//When signatureDebug was enabled
    "signature"=>{
        "playerID", //Log for current playerID 
        "log" //Last video log
    },
    ...
}
```

### Get last error message
> $LittleYoutube->error;

Return string
```
errorMsg //Failed to do stuff
```

### Change settings dynamically
You can also change the settings after initialize LittleYoutube
> $LittleYoutube->settings[options] = value;

## Contribution

If you want to help in LittleYoutube library, please make it even better and start a pull request into it.

Keep it simple and keep it clear.

## License

LittleYoutube is under the GPL license.
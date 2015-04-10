##WHAT

A set of [FileMaker](http://www.filemaker.com/) custom functions that will create and read JSON.

##WHY

My previous [FileMaker-JSON](https://github.com/dansmith65/FileMaker-JSON) project was script based and used [Let Notation](http://filemakerstandards.org/pages/viewpage.action?pageId=5668879) as an intermediary format. While this method worked, it introduced the overhead of an intermediary format that may not be desirable if your intention is to create JSON to send to a web service, or parse the response from a web service. That method also relies on Evaluating text as code, which introduces a security issue that may be unacceptable in certain circumstances.

##HOW

Utilizes recursive custom functions and native FileMaker functions.

##WHO

I'd like to thank [geist interactive](https://www.geistinteractive.com/) for sponsoring this project. I've wanted to work in it for a while now, but with out the sponsorship, I'm not sure when I would have gotten around to it.

##STATUS

This project is currently in a very early stage of development, so you should account for the potential for major changes to be made to it. That being said; my goal is to match the functionality of the [BaseElements](http://www.goya.com.au/baseelements/plugin) backed set of custom functions with the same name available at [geistinteractive/JSONCustomFunctions](https://github.com/geistinteractive/JSONCustomFunctions).

The current implementation includes 24 private custom functions to support the the 7 public functions. My goal is to combine many of the private functions so there are as few as possible; I think 3-4 is likely, but I'm not certain, yet.

These functions are drastically slower than the BaseElements backed functions and approximately twice as slow as the JSON module that converts json to Let Notation. My goal is to implement caching to improve the performance of these functions.

##INSTALLATION

You can use the CFUpdater.fmp12 file to install or update the functions. That file is still very new and rough, but it works. [Watch this demo](https://youtu.be/vJG2Ee1CItM) to learn how to use it.
##WHAT

A set of recursive [FileMaker](http://www.filemaker.com/) custom functions that can create and read JSON.

When reading JSON, utilizes cache in $local variables to improve the speed of reading more than one value. The cache also allows for reading from JSON that is too large to be read in a single pass (due to FileMaker's max of 50,000 recursive calls).


##WHY

My previous [FileMaker-JSON](https://github.com/dansmith65/FileMaker-JSON) project was script based and used [Let Notation](http://filemakerstandards.org/pages/viewpage.action?pageId=5668879) as an intermediary format. While this method worked, it introduced the overhead of an intermediary format that may not be desirable if your intention is to create JSON to send to a web service, or parse the response from a web service. That method also relies on evaluating text as code, which introduces a security issue that may be unacceptable in certain circumstances.

##HOW TO INSTALL

Copy all functions from [FileMaker-JSON-Functions.fmp12](FMFiles/FileMaker-JSON-Functions.fmp12) and paste them into your own file.

##HOW TO USE

Refer to the Test Expression field in [FileMaker-JSON-Functions.fmp12](FMFiles/FileMaker-JSON-Functions.fmp12) for example code. There are examples of using similar functions here: https://www.geistinteractive.com/docs/fmqbo/working-with-json/

##WHO

I'd like to thank [geist interactive](https://www.geistinteractive.com/) for sponsoring this project. I've wanted to work in it for a while now, but with out the sponsorship, I'm not sure when I would have gotten around to it.

##STATUS

Stable (as far as I know) first release. There are currently ~180 test to verify these functions work as expected.

My goal is to match the functionality of the [BaseElements](http://www.goya.com.au/baseelements/plugin) backed set of custom functions with the same name available at [geistinteractive/JSONCustomFunctions](https://github.com/geistinteractive/JSONCustomFunctions). This project is much slower than the BaseElements backed functions, so if the BaseElements plugin is available to you, those functions are preferred.

## License

See the [LICENSE](LICENSE.md) file for license rights and limitations (MIT).

# react-native-tesseract-ocr [![npm version](https://badge.fury.io/js/react-native-tesseract-ocr.svg)](https://badge.fury.io/js/react-native-tesseract-ocr)
<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->
[![All Contributors](https://img.shields.io/badge/all_contributors-2-orange.svg?style=flat-square)](#contributors-)
<!-- ALL-CONTRIBUTORS-BADGE:END -->

react-native-tesseract-ocr is a react-native wrapper for [Tesseract OCR](https://github.com/tesseract-ocr) using base on
  - [tess-two](https://github.com/rmtheis/tess-two) for Android
  - [Tesseract-OCR-iOS](https://github.com/gali8/Tesseract-OCR-iOS) for iOS *(Not implemented yet)*

## Getting started

`$ npm install react-native-tesseract-ocr --save`

or

`$ yarn add react-native-tesseract-ocr`

### Mostly automatic installation

`$ react-native link react-native-tesseract-ocr`

*Don't forget to ...*
- *add [v3.04 trained data files](https://github.com/tesseract-ocr/tessdata/tree/3.04.00) to the appropriate folder*
- *install [CocoaPods](https://cocoapods.org/) in your react-native project and add the following line to your Podfile then run `pod install` __(iOS only)__*
   ```
   pod 'TesseractOCRiOS', '4.0.0'
   ```


### Manual installation


#### iOS

1. In XCode, in the project navigator, right click `Libraries` ➜ `Add Files to [your project's name]`
2. Go to `node_modules` ➜ `react-native-tesseract-ocr` and add `RNTesseractOcr.xcodeproj`
3. In XCode, in the project navigator, select your project. Add `libRNTesseractOcr.a` to your project's `Build Phases` ➜ `Link Binary With Libraries`
4. Run your project (`Cmd+R`)<

#### Android

1. Open up `android/app/src/main/java/[...]/MainActivity.java`
  - Add `import com.reactlibrary.RNTesseractOcrPackage;` to the imports at the top of the file
  - Add `new RNTesseractOcrPackage()` to the list returned by the `getPackages()` method
2. Append the following lines to `android/settings.gradle`:
  	```
  	include ':react-native-tesseract-ocr'
  	project(':react-native-tesseract-ocr').projectDir = new File(rootProject.projectDir, 	'../node_modules/react-native-tesseract-ocr/android')
  	```
3. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
  	```
      compile project(':react-native-tesseract-ocr')
  	```
4. [v3.04 Trained data files](https://github.com/tesseract-ocr/tessdata/tree/3.04.00) for a language must be
extracted in `android/app/src/main/assets/tessdata`.

## Usage

Two methods are provided:

* `recognize` - For single-block text recognition (returns the complete text string)
* `recognizeWithBounds` - For individual word recognition (returns each word and its bounding box)

```javascript
import RNTesseractOcr from 'react-native-tesseract-ocr';

/**
 * @param {string} imgPath - The path of the image.
 * @param {string} lang - The language you want to process.
 * @param {object} tessOptions - Tesseract options.
 */
 const tessOptions = {
  whitelist: null,
  blacklist: '1234567890\'!"#$%&/()={}[]+*-_:;<>'
};

// performs a recognition and returns all the text in a single string
RNTesseractOcr.recognize(imgPath, lang, tessOptions)
  .then((result) => {
    this.setState({ ocrResult: result });
    console.log("OCR Result: ", result);
  })
  .catch((err) => {
    console.log("OCR Error: ", err);
  })
  .done();

// performs a recognition and returns an array with all individual words and their respective bounding boxes
RNTesseractOcr.recognizeWithBounds(imgPath, lang, tessOptions)
  .then((result) => {
    this.setState({ ocrResult: result });

    result.forEach((word, i) => {
        console.log(`OCR Result ${i}: `, word["text"], word["x1"], word["y1"], word["x2"], word["y2"]);
    });
  })
  .catch((err) => {
    console.log("OCR Error: ", err);
  })
  .done();
```

*NOTE: The method _startOcr_ is deprecated. Instead, use _recognize_ or _recognizeWithBounds_*


### Supported languages
  - LANG_AFRIKAANS
  - LANG_AMHARIC
  - LANG_ARABIC
  - LANG_ASSAMESE
  - LANG_AZERBAIJANI
  - LANG_BELARUSIAN
  - LANG_BOSNIAN
  - LANG_BULGARIAN
  - LANG_CHINESE_SIMPLIFIED
  - LANG_CHINESE_TRADITIONAL
  - LANG_CROATIAN
  - LANG_DANISH
  - LANG_ENGLISH
  - LANG_ESTONIAN
  - LANG_FRENCH
  - LANG_GALICIAN
  - LANG_GERMAN
  - LANG_HEBREW
  - LANG_HUNGARIAN
  - LANG_ICELANDIC
  - LANG_INDONESIAN
  - LANG_IRISH
  - LANG_ITALIAN
  - LANG_JAPANESE
  - LANG_KOREAN
  - LANG_LATIN
  - LANG_LITHUANIAN
  - LANG_NEPALI
  - LANG_NORWEGIAN
  - LANG_PERSIAN
  - LANG_POLISH
  - LANG_PORTUGUESE
  - LANG_RUSSIAN
  - LANG_SERBIAN
  - LANG_SLOVAK
  - LANG_SPANISH
  - LANG_SWEDISH
  - LANG_TURKISH
  - LANG_UKRAINIAN
  - LANG_VIETNAMESE

### If you want to use your own trained data file
  - LANG_CUSTOM

 *Locate your own trained data file as `custom.traineddata` into `android/app/src/main/assets/tessdata`.*


## Example
Try the included [TesseractOcrSample](https://github.com/jonathanpalma/react-native-tesseract-ocr/tree/master/tesseractOcrSample):
- `git clone git@github.com:jonathanpalma/react-native-tesseract-ocr.git`
- `cd react-native-tesseract-ocr/tesseractOcrSample/`
- `npm install` or `yarn`

*NOTE: Don't forget to ...*
- *add [v3.04 trained data files](https://github.com/tesseract-ocr/tessdata/tree/3.04.00) to the appropriate folder*
- *install [CocoaPods](https://cocoapods.org/) in your react-native project and add the following line to your Podfile then run `pod install` __(iOS only)__*
   ```
   pod 'TesseractOCRiOS', '4.0.0'
   ```

## TODOS
Check the [project boards](https://github.com/jonathanpalma/react-native-tesseract-ocr/projects)

## Contribution
Contributions are welcome :raised_hands:

## License
This repository is distributed under [MIT license](https://github.com/jonathanpalma/react-native-tesseract-ocr/blob/master/LICENSE)
 - [Tesseract OCR](https://github.com/tesseract-ocr) - maintained by Google, is distributed under [Apache 2.0 license](http://www.apache.org/licenses/LICENSE-2.0)
 - [tess-two](https://github.com/rmtheis/tess-two) is distributed under [Apache 2.0 license](https://github.com/rmtheis/tess-two/blob/master/COPYING)
 - [Tesseract-OCR-iOS](https://github.com/gali8/Tesseract-OCR-iOS) is distributed under [MIT license](https://github.com/gali8/Tesseract-OCR-iOS/blob/master/LICENSE.md)


## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="http://jonathanpalma.me"><img src="https://avatars3.githubusercontent.com/u/12414771?v=4" width="100px;" alt=""/><br /><sub><b>Jonathan Palma</b></sub></a><br /><a href="https://github.com/jonathanpalma/react-native-tesseract-ocr/commits?author=jonathanpalma" title="Code">💻</a> <a href="https://github.com/jonathanpalma/react-native-tesseract-ocr/commits?author=jonathanpalma" title="Documentation">📖</a> <a href="#example-jonathanpalma" title="Examples">💡</a></td>
    <td align="center"><a href="https://github.com/jrunestone"><img src="https://avatars3.githubusercontent.com/u/2293001?v=4" width="100px;" alt=""/><br /><sub><b>Johan Runsten</b></sub></a><br /><a href="https://github.com/jonathanpalma/react-native-tesseract-ocr/commits?author=jrunestone" title="Code">💻</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!

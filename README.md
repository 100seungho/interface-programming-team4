# interface-programming-team4
2019 Fall Interface Programming

for more information about MVC design pattern checkout [iOS: Three ways to pass data from Model to Controller](https://medium.com/@stasost/ios-three-ways-to-pass-data-from-model-to-controller-b47cc72a4336) and [Modern MVC](https://medium.com/ios-os-x-development/modern-mvc-39042a9097ca)

![Image of MVC design Pattern](http://natashatherobot.com/wp-content/uploads/Screen-Shot-2014-04-28-at-6.13.10-AM.png)


## Model

### YoutubeManager.swift
Youtube API를 사용해 동영상 정보를 불러오는 Model입니다.

#### `protocol YoutubeManagerDelegate `
- `ViewController`와 소통하기 위한 `protocol`
- `func didUpdateVideos(_ youtubeManager: YoutubeManager, with video: YoutubeModel)`: video 정보 호출을 성공할 시, delegate은 해당 method를 부릅니다.
- `func didFailWithError(error: Error)`: error가 날 시, delegate은 해당 method를 부릅니다.


#### `func fetchVideo(searchName: String)`
Delegate(`YoutubeViewController`)은 이 method에 검색어를 parameter로 넘기고, 이 함수는 넘겨받은 검색어를 사용해 youtubeAPI에 사용할 url을 생성 후 이를 parameter로 `YoutubeManager.performRequest()`를 호출합니다.

#### `func performRequest(urlString: String)`
넘겨받은 url을 사용해 `URLSession`과 `URLSession.dataTask(with: url)`을 생성, data를 받아오는 함수입니다. 실패시 delegate method인 `didFailWithError()`를 호출하고, 성공시에는 `YoutubeManager.parseJSON(with: safeData)`를 호출합니다. 

#### `func parseJSON(videoData: Data) -> YoutubeModel?`
1. `Foundation` 라이브러리 내장함수인  `JSONDecoder()`를 사용해 받아온 JSONdata를 parsing합니다.
3. 미리 준비된 data model(`YoutubeModel`)에 집어넣는 함수입니다. 

### YoutubeData.swift
YoutubeAPI가 제공하는 JSON data file에서 필요한 정보들을 찾기 위한 data type입니다. 변수명이 달라질 시, 정확한 정보를 담을 수 없습니다. `YoutubeData.items[].snippet.thumnails.dafault` 는 `default`라는 swift 예약어를 사용하기 때문에, 백틱(`)을 사용해 변수명을 선언했습니다. 

### YoutubeModel.swift
동영상 정보를 내부적으로 활용하기 위한 data 구조입니다. 

## View

### Main.stroyboard


## Controller

### ViewController.swift

### YoutubeViewController.swift

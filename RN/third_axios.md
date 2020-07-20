# 3장. axios

## 3 - 1) axios란

axios는 HTTP 클라이언트 라이브러리로써, 비동기 방식으로 HTTP 데이터 요청을 실행합니다. 내부적으로 AXIOS는 직접적으로 XMLHttpRequest 를 다루지 않고 “AJAX 호출”을 할 수 있습니다.

### axios의 특징

1. Promise 기반의 API 형식 .
2. Promise란 비동기 로직 처리에 유용한 자바스크립트 객체이다

<br/>

### axios 장점

1. 구형브라우저를 지원합니다.
2. 요청을 중단시킬 수 있습니다.
3. 응답 시간 초과를 설정하는 방법이 있습니다.
4. JSON 데이터 자동변환
5. Node.js 에서 사용

<br/>

### axios의 기능
1. axios를 통해 HTTP 요청으로 데이터를 가져올 수 있습니다.
2. success이면. get함수와 연결되 then 함수로, failure 할 경우 catch()함수로 이동합니다.
3. Axios를 통해 가져오는 결과값은 response 입니다.
(response는 다른 명칭으로 변경 가능합니다.)
4. API구조를 알고 있으면 JSON형식으로 불러올 수 있다.

<br/>

>axios를 사용하세요
axios는 현재 가장 성공적인 HTTP 클라이언트 라이브러리 중 하나입니다. 아직 1.x 버전이 릴리즈 되지 않았지만 스타가 1만개가 넘을 정도로 인기가 좋습니다. 특별히 언급할만한 부분은 요청 취소와 TypeScript를 사용할 수 있는 것 입니다. 이 글에서는 기본적인 vue와 axios의 사용 방법을 알아봅니다. axios의 github 프로젝트를 살펴보시면 더 많은 내용을 익힐 수 있을 것입니다.



## 3 - 2) axios 설치 & 구문
```JAVASCRIPT
npm install --save axios
```

#### GET요청시
```JAVASCRIPT

axios.get('https://reqres.in/api') 
        .then(res => {
            //성공 코드
            console.log(res);
        })
        .catch(err => {
            //실패
            console.log(err);
        })
        .then(() => {
            //성공했을때, 실패했을때 상관없이 띄어줌
            console.log('test');
        })
```

#### POST 요청시
```JAVASCRIPT 

axios.post('https://reqres.in/api/register', {
            "email": "eve.holt@reqres.in",
            "password": "pistol"
        })
        .then(res => {
            console.log(res);
            this.userId = res.data.token;
        })
        .catch(err => {
            console.log(err);
        });
    }
```

<br/>

#### 요청과 결과
| API유형 | 처리결과 |
|:--:|:--:|
| axios.get('URL주소').then().catch() | 해당 URL로 get방식으로 요청. then()안에 반환값 로직 작성. catch()안에는 오류발생시 로직 작성. |
| axios.post('URL주소').then().catch() | 해당 URL로 POST방식으로 요청. then()안에 반환값 로직 작성. catch()안에는 오류발생시 로직 작성.  |
| axios({옵션}) | HTTP요청에 대한 자세한 속성들을 직접 정의하여 보낼 수 있음 |

# 3 - 3) 실습 프로젝트 구현

View를 만들어 놓은 파일에 axios를 이용해 데이터를 넣어봅시다. 빈 화면에 데이터를 뿌려 렌더링을 제어하기 위해서 state를 설정해 주세요. state에 변화를 줄 useEffect도 설정해봅시다.

#### App.js
```JAVASCRIPT
import { StatusBar } from 'expo-status-bar';
import React, {useState, useEffect} from 'react'; //import는 필수 입니다.
import axios from 'axios'; // import는 필수입니다.
import { StyleSheet, Text, View, ScrollView } from 'react-native';

const NewsCard = () => {
    ...
}


export default function App() {
    const [news, setNews] = useState([]);

    useEffect(() => {
        getNewsFromAPI()
    }, [])

    function getNewsFromAPI() {
        //여기에다 axios로 데이터를 불러 오겠습니다.
    }

    return (
        <ScrollView> {/*ScrollView는 모바일 디바이스에서 overflow된 데이터에 맞게 scroll이 가능하게 해줍니다.*/}
            <NewsCard />
            <NewsCard />
            <NewsCard />
            <NewsCard />
            <NewsCard />
        </ScrollView>
  );
}

const styles = StyleSheet.create({
    ...
})
```

axios로 저희는 데이터를 요청하고 값만 받을 것이기때문에 get으로 요청하도록 하겠습니다. get과 post는 통신규약의 종류입니다.

#### App.js
```JAVASCRIPT
import { StatusBar } from 'expo-status-bar';
import React, {useState, useEffect} from 'react'; 
import axios from 'axios';
import { StyleSheet, Text, View, ScrollView } from 'react-native';

const NewsCard = () => {
    ...
}


export default function App() {
    const [news, setNews] = useState([]);

    useEffect(() => {
        getNewsFromAPI()
    }, [])

    function getNewsFromAPI() {
        axios.get('https://newsapi.org/v2/top-headlines?country=kr&apiKey=219ca3f214c941dcbea9c6291420fe4e')
      .then(async function (res) {
        console.log(res.data); // 데이터를 콘솔에 찍어보겠습니다.
        setNews(res.data) // setNews에 바뀐 값을 넣어주는 코드입니다.
        // console.log("여기 데이타________________", news.articles, "________________여기 데이타")
      })
      .catch(function (error) {
        console.log(error);
      })
    }

    // news에 값이 담기지 않았을경우 error를 무시하기 위해서 
    if (!news) {
        return null;
    }

    return (
        <ScrollView> {/*ScrollView는 모바일 디바이스에서 overflow된 데이터에 맞게 scroll이 가능하게 해줍니다.*/}
            <NewsCard />
            <NewsCard />
            <NewsCard />
            <NewsCard />
            <NewsCard />
        </ScrollView>
  );
}

const styles = StyleSheet.create({
    ...
})
```

<img src="./4.jpg" width="30%" height="">

이제 마지막입니다. 각 데이터를 추출해서 각 자리에 맞게 넣어주시면 됩니다.

```JAVASCRIPT
import { StatusBar } from 'expo-status-bar';
import React, {useState, useEffect} from 'react'; 
import axios from 'axios';
import { StyleSheet, Text, View, FlatList } from 'react-native'; //flatList는 데이터의 키값에 따라 반복적인 리스트를 만들어 주는 react-native전용 컴포넌트입니다.

const NewsCard = ({item}) => {
    <View style={styles.cardWrap}>
        <Text style={styles.title} numberOfLines={2}>{item.title}</Text>
        <Text style={styles.author}>{item.author}</Text>
        <Text style={styles.date}>{item.publishedAt}</Text>
        <Text style={styles.description} numberOfLines={3}>
            {item.description}
        </Text>
        <Text style={styles.source} numberOfLines={1} onPress={() => Linking.openURL(item.url)}>{item.url}</Text>
    </View>
}


export default function App() {
    const [news, setNews] = useState([]);

    useEffect(() => {
        getNewsFromAPI()
    }, [])

    function getNewsFromAPI() {
        axios.get('https://newsapi.org/v2/top-headlines?country=kr&apiKey=219ca3f214c941dcbea9c6291420fe4e')
      .then(async function (res) {
        console.log(res.data); // 데이터를 콘솔에 찍어보겠습니다.
        setNews(res.data) // setNews에 바뀐 값을 넣어주는 코드입니다.
      })
      .catch(function (error) {
        console.log(error);
      })
    }

    // news에 값이 담기지 않았을경우 error를 무시하기 위해서 
    if (!news) {
        return null;
    }

    return (
        // FlatList는 자체적으로 스크롤뷰를 제공함으로 ScrollView를 빼주어도 무방합니다.
        <View>
            <FlatList
                data={news.articles}
                keyExtractor={(item, index) => 'key' + index}
                renderItem={({ item }) => {
                return <NewsCard item={item} />
                }}
            />
        </View>
    );
}

const styles = StyleSheet.create({
    ...
})
```

_*FlatList에 관한 자세한 내용은 [React-Native FlatList](https://reactnative.dev/docs/flatlist)를 참고해주세요._


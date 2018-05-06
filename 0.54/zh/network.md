---
id: version-0.54-network
title: 网络通信
original_id: network
---

大部分移动端APP通过请求`URL`于远程服务器上拉取数据资源。你可以通过对`REST API`发起`POST`请求以交互用户数据。亦或者仅仅需要获取(`fetch`)其它服务器上的静态资源。

## Using Fetch - 使用Fetch

`React-native` 提供了一套供给开发者进行网络访问需求的 `Fetch API`( 与Web标准一致 )。`Fetch`与所谓的`AJAX(XMLHttpRequest)`十分相似，但本文无意详细讲解缘起于Js新标准的`Fetch`使用方法，读者可前往由mozilla基金会构建的MDN Web Docs进行学习：[Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

### Making requests - 发起请求

若要从任何网址获取数据，仅需将`URL`作为参数传入`Fetch`方法。

``` jsx
fetch('https://mywebsite.com/mydata.json');
```

`Fetch`方法亦支持可选的多参数，以此开发者将可以自定义`HTTP请求`,例如指定`header`参数，或是指定使用 `POST`请求：

```jsx
fetch('https://mywebsite.com/endpoint/', {
  method: 'POST',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    firstParam: 'yourValue',
    secondParam: 'yourOtherValue',
  }),
});
```

请阅读 [Fetch Request docs](https://developer.mozilla.org/en-US/docs/Web/API/Request) 以获取完整的Fetch参数列表。

### Handling the response - 解析服务器响应数据

在上面的示例中演示了如何发起请求。与此同时，你亦需要知道如何接受解析服务器返回的响应数据。

网络通信的本质是一种**异步请求**，Fetch方法将返回一种名为[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)的对象，这种模式将极大的简化异步请求操作代码（译者注：其极大的改变了往常的callback回调写法）

``` jsx
function getMoviesFromApiAsync() {
  return fetch('https://facebook.github.io/react-native/movies.json')
    .then((response) => response.json())
    .then((responseJson) => {
      return responseJson.movies;
    })
    .catch((error) => {
      console.error(error);
    });
}
```

开发者可以在React Native应用中使用ES7标准中的async/await 语法(译者注：网络请求的异步本质无法变更)：

``` jsx
async function getMoviesFromApi() {
  try {
    let response = await fetch(
      'https://facebook.github.io/react-native/movies.json'
    );
    let responseJson = await response.json();
    return responseJson.movies;
  } catch (error) {
    console.error(error);
  }
}
```

不要忘记使用`catch`方法收集`fetch`可能抛出的异常，否则请求出错时你无法看到任何报错及警告。

```SnackPlayer name=Fetch%20Example
import React from 'react';
import { FlatList, ActivityIndicator, Text, View  } from 'react-native';

export default class FetchExample extends React.Component {

  constructor(props){
    super(props);
    this.state ={ isLoading: true}
  }

  componentDidMount(){
    return fetch('https://facebook.github.io/react-native/movies.json')
      .then((response) => response.json())
      .then((responseJson) => {

        this.setState({
          isLoading: false,
          dataSource: responseJson.movies,
        }, function(){

        });

      })
      .catch((error) =>{
        console.error(error);
      });
  }



  render(){

    if(this.state.isLoading){
      return(
        <View style={{flex: 1, padding: 20}}>
          <ActivityIndicator/>
        </View>
      )
    }

    return(
      <View style={{flex: 1, paddingTop:20}}>
        <FlatList
          data={this.state.dataSource}
          renderItem={({item}) => <Text>{item.title}, {item.releaseYear}</Text>}
          keyExtractor={(item, index) => index}
        />
      </View>
    );
  }
}
```

> 默认情况下，iOS会阻止所有非https(SSL加密)请求。如果你请求的接口是http协议，那么首先需要添加一个`App Transport Security`的例外，如果您事先知道需要访问的域名，那么仅为这些域名添加例外情况会更安全; 如果域名并不确定，则可以完全禁用`ATS`。 不过请注意，从2017年1月起，苹果的`App Store`审查将需要合理的理由来禁用ATS。 有关更多信息，请参阅[Apple的文档](https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW33)。

## 使用其他的网络通信库

`React Native`中已经内置了`XMLHttpRequest API(ajax)`。一些基于`XMLHttpRequest`封装的第三方库也可以使用，例如`frisbee`或是`axios`等。(但注意不能使用jQuery，因为jQuery中还使用了很多浏览器中才有而RN中没有的东西)。
``` jsx
var request = new XMLHttpRequest();
request.onreadystatechange = (e) => {
  if (request.readyState !== 4) {
    return;
  }
ss
  if (request.status === 200) {
    console.log('success', request.responseText);
  } else {
    console.warn('error');
  }
};

request.open('GET', 'https://mywebsite.com/endpoint/');
request.send();
```

> react-native 中的安全机制与web开发并不相同，并不存在请求的跨域问题。

## WebSocket Support - WebSocket支持

React Native亦支持[WebSockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket)，一种基于TCP连接并支持全双工通信模式的网络协议。

``` jsx
var ws = new WebSocket('ws://host.com/path');

ws.onopen = () => {
  // connection opened
  ws.send('something'); // send a message
};

ws.onmessage = (e) => {
  // a message was received
  console.log(e.data);
};

ws.onerror = (e) => {
  // an error occurred
  console.log(e.message);
};

ws.onclose = (e) => {
  // connection closed
  console.log(e.code, e.reason);
};s
```

## High Five!

If you've gotten here by reading linearly through the tutorial, then you are a pretty impressive human being. Congratulations. Next, you might want to check out [all the cool stuff the community does with React Native](more-resources.md).

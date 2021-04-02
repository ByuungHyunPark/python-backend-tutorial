# [Chapter03] 첫 API 개발 시작

프론트엔드 시스템과 백엔드 API 시스템은 일반적으로 HTTP 프로토콜을 기반으로 통신한다. 이 책에서 앞으로 우리가 만들어 나갈 API 시스템 또한 HTTP 프로토콜 기반이 될 것이다. 그러므로 백엔드 API 시스템을 구현하는 데에 있어서 HTTP 프로토콜을 이해하는 것은 필수라고 할 수 있다. 이번 장에서는 HTTP의 구조 및 백엔드 API 시스템 개발에 필요한 핵심 요소들을 알아보도록 하자. 
- HTTP 핵심 요소
- HTTP 구조
- 자주 사용되는 HTTP 메소드와 Status Code


##### &#10004; STEP01 : HTTP란?
HTTP는 HypeRText Transfer Protocol의 약자로서, 웹상에서 서로 다른 서버 간에 하이퍼텍스트 문서, 즉 HTML을 서로 주고받을 수 있도록 만들어진 프로토콜, 통신 규약이다. 웹상에서 네트워크를 통해 서버 사이에 통신할 때 어떠한 형식으로 서로 통신하자고 규정해 놓은 "통신 형식"혹은 "통신 구조"라고 보면 된다. 공통의 통신 형식을 __프로토콜__ 이라고도 하며, 가장 널리 사용되는 프로토콜이 HTTP이다.

##### &#10004; STEP02 : HTTP통신 방식

HTTP 통신 방식에는 크게 2가지로, __requests__와 __response__방식이 존재한다. 

##### &#10004; STEP03 : HTTP 요청 구조
HTTP 통신은 요청과 그에 대한 응답으로 이루어져 있다. 이제 HTTP 요청과 응답 메시지(message)가 어떠한 구조로 이뤄져 있는지를 알아보자. 먼저 HTTP 요청 메시지의 구조에 대해서 알아보자. HTTP 요청은 다음과 같은 형태로 이뤄져있다. 
```
#1
POST /payment-sync HTTP/1.1 

#2
Accept: application/json 
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 83
Content-Type: application/json
Host: intropython.com
User-Agent: HTTPie/0.9.3

#3
{
    "imp_uid": "imp_1234567890",
    "merchant_id": "order_id_8237352",
    "status": "paid"
}
```

HTTP 요청 메시지는 크게 세 부분으로 이뤄져있다.<br>
__\#1 : Start Line__
- HTTP 메소드
- Request target
- HTTP version

__\#2 : Headers__
- Host : 요청이 전송되는 target의 호스트 URL을 알려주는 헤더
- User-Agent : 요청을 보내는 클라이언트에 대한 정보
- Accept : 해당 요청이 받을 수 있는 응답(response) body 데이터 타입을 알려주는 헤더

__\#3 : Body__
- HTTP 요청 메세지에서 body 부분은 HTTP 요청이 전송하는 데이터를 담고 있는 부분이다. 전송하는 데이터가 없다면 body 부분은 비어잇게 된다. 

보통 HTTP 요청과 응답 메시지의 모든 부분을 직접 구현할 필요는 없다. 일반적으로 개발자가 직접 지정해야 하는 부분은 HTTP 메소드와 status code, 몇 개의 헤더 정보, 그리고 body 부분이다. 하지만 그래도 HTTP 응답과 요청의 구조와 내용을 이해는 하고 있어야 한다.


##### &#10004; STEP04 : 자주 사용되는 HTTP 메소드
앞에서 HTTP 메소드는 HTTP 요청이 의도하는 액션을 정의하는 부분이다. <br>
API를 개발하는 데 있어서 HTTP 메소드를 잘 이해하고 적절한 HTTP 메소드를 사용하는 것이 중요하다. 다양한 HTTP 메소드들이 있는데 그 중 가장 자주 사용되는 HTTP 메소드들에 대해서 조금 더 자세하게 알아보자. 

- 1. GET
  
GET 메소드는 이름 그대로 어떠한 데이터를 서버로부터 요청(GET)할 때 주로 사용하는 메소드이다. 즉, 데이터의 생성이나 수정 그리고 삭제 등의 변경 사항이 없이 단순히 데이터를 받아 오는 요청이 주로 GET 메소드로 요청된다. 언급한 대로 주로 데이터를 받아 올 때 사용되므로 해당 HTTP 요청의 body가 비어있는 경우가 많다.
- 2. POST

GET  메소드와 함께 가장 자주 사용되는 HTTP 메소드다. GET과 다르게 데이터를 생성하거나 수정 및 삭제 요청을 할 때 주로 사용되는 HTTP 메소드이다. 

##### &#10004; STEP05 : API 엔드포인트 아키텍처 패턴
API의 엔드포인트 구조를 구현하는 방식에도 널리 알려지고 사용되는 패턴들이 있다. 크게 2가지가 있는데 하나는 REST 방식이고 다른 하나는 GraphQL 이다. REST 방식은 가장 널리 사용되는 API 엔드포인트 아키텍쳐 패턴이다. 이미 많은 API 시스템들이 REST 방식으로 구현되어 있다. GraphQL은 페이스북이 개발한 기술이며, 비교적 최근에 나온 방식이다. 

__1. RESTful HTTP API__ <br>
REST(Representation State Transfer)ful API는 API 시스템을 구현하기 위한 아키텍처의 한 형식이다. REST의 개념은 로이 필딩 박사가 2000년 그의 박사학위 논문으로 처음 소개했다고 한다. <br>

RESTful API는 API에서 전송하는 리소스(resource)를 URI로 표현하고 해당 리소스에 행하고자 하는 의도를 HTTP 메소드로 정의하는 방식이다. 각 엔드포인트는 처리하는 리소스를 표현하는 고유의 URI 주소를 가지고 있으며, 해당 리소스에 행할 수 있는 행위를 표현하는 HTTP 메소드를 처리할 수 있게 된다. 예를 들어, 사용자 정보를 리턴하는 "/users" 라는 엔드포인트에서 사용자 정보를 받아 오는 HTTP 요청은 다음과 같이 표현할 수 있다. 
```
HTTP GET /users
GET /users
```
새로운 사용자를 생성하는 엔드포인트는 URI를 "/user"로 정하고 HTTP 요청은 다음과 같이 표현할 수 있다.
```
POST /user
{
    "name" : "송은우",
    "email" : "songew@gmail.com
}
```
이러한 구조로 설계된 API를 Restful API라고 한다. RESTful API의 장점은 몇 가지가 있는데, 그중 가장 장점은 자기 설명력(self-descriptiveness)이다. 즉 엔드포인트의 구조만 보더라도 해당 엔드포인트가 제공하는 리소스와 기능을 파악할 수 있다. API를 구현하다 보면 엔드포인트의 수가 많아지면서 엔드포인트들의 역할과 기능을 파악하기가 쉽지 않을 때가 많은데, REST 방식으로 구현하면 구조가 훨씬 직관적이며 간단해진다. 

__2. GrashQL__ <br>
한동안 REST 방식이 API를 구현하는 데에 있어서 정석으로 여겨졌다. 그래서 많은 기업들이 API를 REST 방식으로 구현하였다. 그러나 REST 방식으로 구현해도 여전히 구조적으로 생기는 문제들이 있었다. 특히 가장 자주 생기는 문제는 API 구조가 특정 클라이언트에 맞춰져서 다른 클라이언트에서 사용하기에 적합하지 않게 된다는 점이다. 페이스북이 2012년에 모바일 앱 개발에 사용하기에는 적합하지 않았고, 모바일 앱용 API를 따로 만들어야 했다. 이러한 문제가 생기는 이유는, REST 방식의 API에서는 클라이언트들이 API가 엔드포인트들을 통해 구현해 놓은 틀에 맞춰 사용해야 하다 보니 그 틀에서 벗어나는 사용은 어려워지기 때문이다. <br>

이러한 문제를 해결하기 위해서 페이스북은 GraphQL을 만들게 된다. GraphQL은 REST방식의 API와는 다르게 엔드포인트가 오직 하나다. 그리고 엔드포인트에 클라이언트가 필요한 것을 정의해서 요청하는 식이다. 기존 REST 방식의 API와 반대라고 보면 된다. 

◎ ___GraphQL의 예시를 들어보자___ <br>
아이디가 1인 사용자의 정보와 그의 친구들의 이름 정보를 API로부터 받아 와야 한다고 예를 들어 보자. 일반적인 REST 방식의 API에서는 다음과 같이 두 번의 HTTP 요청을 보내야 한다. 
```
GET /users/1
GET /users/1/friends
```
앞서 두 번의 요청을 한번의 HTTP 요청으로 줄이기 위해서는 다음처럼 HTTP요청을 내보내야 한다.


```
GET /users/1?include=friends.name
```

둘 다 비효율적이고, 복잡한 것을 볼 수 있다. 만일 사용자 정보들 중 다 필요하지 않고 이름만 필요하든가 혹은 어떤 경우에는 친구들의 이름 외에도 친구들의 이메일도 필요하다면 HTTP 요청은 더 복잡해질 것이다. GraphQL을 사용하면 다음과 같이 HTTP 요청을 보내면 된다.


```
POST /graphql

{
    user(id: 1){
        name
        age
        friends {
            name
        }
    }
}
```
만일 사용자 정보는 이름만 필요하고, 대신 친구들의 이름과 이메일이 필요하다면 다음과 같이 보내면 된다.
```
POST /graphql

{
    user(id: 1){
        name
        friends {
            name
            email
        }
    }
}
```
GraphQL이 장점이 많지만, REST에 비해 나온지 얼마 되지 않아 대부분 REST를 많이 씀. 이 책에서도 REST위주로 작성할 예정이라고 함

# Next 사용하기

```
npm init
npm install react react-dom next
```

pages 폴더만들기
index.jsx 파일 생성해서 테스트 해보시고.

실행할려고 하다보니 npm run dev 명령어가없어서 생성해줌

package.json

```
"scripts": {
    "dev":"next dev",
    "build":"next build",
    "start":"next start"
}
```


_app.jsx 파일을 만듬

그전과 다르게 pageProps 내용을 삽입함

_document.jsx
코드를 복붙함 (styled component 할때 serverside rendering 안되어서 css를 서버사이드랜더링을 처리할려고 코드를 복붙함 )
```
npm install styled-components
```


.babelrc 
서버사이드랜더링 CSS처리하기위해서 추가적인 바벨설정을 함
```
npm install babel-plugin-styled-components
```

> Components - 화면을 구성하는 최소단위들
> Layouts - header 컴포넌트, footer 컴포넌트 , Navigation 
> Providers - Store내용을 Theme 
> reducers - actions 내용과 reducer 내용을 넣는 디렉토리
> saga - redux middle ware 인 saga내용을 넣는 디렉토리
> pages - 페이지의 화면의 대표화면에 대한 컴포넌트
> utils - 커스텀 hook이라던가 데이터 정리할수있는 코드들


## Providers 
> rootProvider.js  : 페이지 컴포넌트에서 감싸줄 애들입니다.

## Layouts 
> ThemeLayout.jsx : 페이지 컴포넌트를 감싸줄건데. UI적인 부분 담당


# Redux 셋팅
```
npm install redux
npm install react-redux
npm install next-redux-wrapper
npm install redux-saga

npm install redux-devtools-extension
npm install axios
```

# Redux를 셋팅할때 제일먼저할것 ?

store만들기 

> Providers -> createCtx.js (10분..) 

만들었으니 사용방법은

> _app.jsx 
wrapper.withReudx 감싸주기

> saga 디렉토리에서 
index.js 파일을 생성해주고 ( 다른 미들웨들을 묶어주는 )
sagaEffect 사용했습니다.

> postSaga.js 파일생성
Saga 만듭니다.


> reducers > index.js
파일을 완성시킵니다 ( reducer를 묶어주는 역활 )

> post.js 
post관련된 actions 내용을 넣고
action.type에 따른 state를 바꾸는 작업을 함


2. 인피니티스크롤
3. 클릭시 해당 글만 가져오는 동적라우팅


-----------

# 인피니티스크롤
[posts.jsx]
import { useEffect } from 'react'

1. window.scrollY
: 현 시점 스크롤의 높이

2. document.documentElement.clientHeight
: 내 브라우저(눈에 보이는)의 높이

3. document.documentElement.scrollHeight
: 토탈 높이
1+2 = 3 이 됨

암튼 이거 라이브러리 있음


# 클릭시 해당 글만 가져오는
.../posts/1
해당 id 값만 가져오는

/pages/posts/[id].jsx 생성

import { useRouter } from "next/router"

const Post = ()=>{
    const router = useRouter()
    const {id} = router.query

    return(
        <>
            hello {id}
        </>
    )
}

export default Post

이거를 서버사이드렌더링으로 바꿔보자구

이 id 값에 해당하는 값ㅇ르 initalState의 postDetail 에 담을것이다.
이게 더 정확함 post 에서 필터링하는것보다는

/reducers/post.js

export const GET_POSTS_DETAIL_REQUEST = "GET_POSTS_DETAIL_REQUEST"
export const GET_POSTS_DETAIL_SUCCESS = "GET_POSTS_DETAIL_SUCCESS"
export const GET_POSTS_DETAIL_FAIL = "GET_POSTS_DETAIL_FAIL"



export const GET_POSTS_DETAIL = (data) =>{
    return{
        type : GET_POSTS_DETAIL_REQUEST,
        data
    }
}


case 도 3개

추가함

/saga/postSaga.js

GET_POSTS_DETAIL_REQUEST,
    GET_POSTS_DETAIL_SUCCESS,
    GET_POSTS_DETAIL_FAIL
얘네를 import 해옴


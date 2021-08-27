[pages/index.jsx]
rootProvider 로 감싸면서

# 실행순서
_document.jsx
_app.jsx
index.jsx


ThemeLayout 은 [Layouts/ThemeLayout.jsx]에서 가져온거임


꼭 data 가 필요한곳 에서 data 가 없으면 페이지 렌더가 안되는경우..? 이거 서버사이드 렌더링으로 해결해야함 

브라우저 - 프론트 - 백 - 프론트(데이터완성) - 브라우저
상태값을 먼저 채우고 보내주는거

기존에는 상태를 만들기 전에 그려줬다면 이제는 상태 먼저 채우고 해줘야함

요청방식 useEffect 가 아니라!

[서버사이드렌더링]
export const getServerSideProps = wrapper.getServerSideProps((Store)=>(req,res)=>{

})
redux로 감싸고 있던 상태를 담고있는녀석

익명함수 안에 익명함수...

// console.log(Store);
해보면 
dispatch
getState
sageTask
이런게 나옴
쓸 수 있다는거지..


두번째 success dispatch 날려줘야함
[posts.jsx]
이거는 그냥 받아들여야함
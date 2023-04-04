ICIA 최종프로젝트 Wedding Dive
---
프로젝트 기간 : 2022.12 ~ 2023.01 <br><br>
프로젝트 인원 : 6명<br><br>
사용 프로그램 : visual studio, intellj, Mysql<br><br>
사용 언어 : Html, CSS, JavaScript, React, Java<br>
## 환경 구성
IDE(통합개발환경) : IntelliJ Ultimate(유료 버전), Visual Studio Code<br><br>
프레임워크 : Spring Boot<br><br>
데이터베이스 : Mysql<br><br>
DB 접근 기술 : JPA<br><br>
View 템플릿 : React<br>
## 프로젝트 설명<br>
결혼하는 과정에 필요한 스드메, 신혼여행, 예식장 등 필요한걸 하나에 모아놓은 웨딩 중개 사이트입니다.<br> 

- #### 메인페이지 화면<br><br>
![image](https://user-images.githubusercontent.com/117874997/215312693-84f6a19e-68c2-48b6-9819-7d17f8b525db.png)

- #### ERD 구성<br><br>
![image](https://user-images.githubusercontent.com/117874997/215296621-de57e2fe-60a8-4aab-98e9-eb945509b133.png)

## 제가 구현한 기능으로는<br>
- 마이페이지(내 정보, 정보 수정)<br>
- 게시판(게시글 출력, 페이징 처리, session을 이용해 회원과 관리자의 기능 구분(글삭제, 글수정, 글신고, 댓글기능, 댓글삭제, 댓글신고, 댓글수정))<br>
- 회원가입<br>


## 마이페이지

※ Mypage.jsx 컴포넌트(마이페이지 회원정보)

```javascript

const Mypage = () => {
  const nav = useNavigate();
  const id = sessionStorage.getItem("mid");
  console.log(id)

 

  useEffect(() => {

    if(id === null || id === ""){
        alert("로그인 후 가능한 기능입니다");
        nav("/");
        // return;
    }
  });
  

  const modify= () => {
    nav('/member/edit')
  }
  
  const { userInfo } = useAuth()

  const onSubmitHandler = (e) => {
    e.preventDefault()
  }
  const remove=() => {
    // console.log(remove);
    let confirm = window.confirm('회원 탈퇴하시겠습니까?');
    if(confirm === true) {
      axios
      .post('/resignMy', userInfo)
      .then(res => {
        console.log(res);
  
        if(res.data === 'Ok'){
          window.alert('정상적으로 탈퇴되었습니다.');
          sessionStorage.removeItem("mid");
          sessionStorage.removeItem("grade");
          nav('/');
        }else {
          window.alert('탈퇴에 실패하였습니다.');
        }
      })
      .catch((err) => console.log(err));
    } else {
      window.alert('취소되었습니다.');
    }
  
  }

  return (
    <form style={{margin:'0 auto' ,width: '70%' }} onSubmit={onSubmitHandler}>
      <Stack style={{ width: '100%' }}>
        <InputGroup label="아이디">
          <Input style={{border: 0}} type="text" value={userInfo.mid} readOnly />
        </InputGroup>
        <InputGroup label="성함">
          <Input style={{border: 0}} type="text" value={userInfo.mname} readOnly />
        </InputGroup>
        <InputGroup label="이메일">
          <Input style={{border: 0}} type="text" value={userInfo.memail} readOnly/>
        </InputGroup>
        <InputGroup label="연락처">
          <Input style={{border: 0}} type="text" value={userInfo.mphone} readOnly />
        </InputGroup>
        <InputGroup label="주소">
          <Input style={{border: 0}} type="text" value={userInfo.maddr} readOnly />
        </InputGroup>
        <InputGroup label="상세주소">
          <Input style={{border: 0}} type="text" value={userInfo.mdaddr} readOnly />
        </InputGroup>
        <FlexBox gap={30} style={{ width: '500px', margin: '0 auto' }}>
          <Button onClick={modify} style={{ flex: 1 }}>수정하기</Button>
          <Button onClick={remove} style={{ flex: 1 }}>탈퇴하기</Button>
        </FlexBox>
      </Stack>
    </form>
  )
}
export default Mypage;
```

- #### 마이페이지<br>
<img width="1107" alt="내 정보" src="https://user-images.githubusercontent.com/117880554/224944992-51f8dda4-293b-4b80-87ff-4a35cf64849e.png">

로그인을 한 후에 페이지 우측 상단의 '마이페이지' 버튼을 누르면 보이는 기본 마이페이지로 회원정보를 확인할 수 있고, '수정하기' 버튼 클릭 시 회원정보 수정 카테고리로 이동되며, '탈퇴하기' 버튼 클릭 시 회원 알림창으로 다시 한번 확인 후 회원 정보를 삭제합니다.




## Back_MemberController
```java
    public class MemberController {
        @Autowired
        private MemberService mServ;
        // 마이페이지 내정보
        @PostMapping("mypage")
        public Member mypage(@RequestParam String mid) {
            log.info("mypage()");
            log.info("불러와 :" +mid);
            Member member = mServ.mypage(mid);
            log.info(member.toString());
            return member;
        }
        
        // 마이페이지 회원탈퇴
        @PostMapping("resignMy")
        public String resignMy(@RequestBody Member mem ){
            log.info("resignMy()");
            return mServ.removeMy(mem);
        }
    }
```
## Back_MemberService
```java
    @Service
    @Log
    public class MemberService {
        @Autowired
        MemberRepository mRepo;
        // 마이페이지 내정보
        public Member mypage(String mid) {
            log.info("mypage()");
            Member mem = new Member();
            try {
                mem = mRepo.findByMid(mid);
                mem = mRepo.findById(mid).get();

                log.info(mem.toString());
                mRepo.save(mem);
                log.info("bb"+mem);
                log.info("담았느냐");
            }catch (Exception e) {
                log.info("못담았느냐");
                e.printStackTrace();
            }
                return mem;
        }
        
            // 마이페이지 회원 탈퇴
        public String removeMy(Member mem) {
        log.info("removeMy()");
        String msg = null;
        try {
            mRepo.delete(mem);
            msg = "Ok";
        } catch (Exception e){
            msg = "fail";
        }
        return msg;
    }
    }
    
```
프론트에서 넘어온 id 값을 통해 해당 유저의 정보들을 findby~를 사용하여 데이터베이스에서 찾아서 return 해줍니다.<br><br>

## 내 정보 수정

※ PageCorrection.jsx 컴포넌트

```javascript

const PageCorrection= () => {


const id = sessionStorage.getItem("mid");

const nav = useNavigate();

const inputBoard = useRef();
const borderCh = (e) => {
  inputBoard.current.style.border = '1px solid lightgray';
  inputBoard.current.style.background = 'white';
  inputBoard.current = e.target
  inputBoard.current.style.border = '1px solid black';
  inputBoard.current.style.background = 'rgb(245,245,245)';

}

const [userInfo, setUserInfo] = useState({})
const [data, setData] = useState({
  
});
const [a, setA] = useState('');
useEffect(()=> {
  const id = sessionStorage.getItem("mid");

    axios
    .post("/mypage", null,{params:{mid:id}})
    .then((res)=> {
      console.log(res.data)
      setUserInfo(res.data);
      setData(res.data)
    })
    .catch((err)=> console.log(err));
  
  console.log(userInfo)
  //setA(userInfo.maddr);
},[])

// console.log(data)

const onch = useCallback(
  (e) => {
    if(a === '') {
      console.log(a)
      setA(data.maddr)
    }
    //setA()
    let newData = {
      ...data,
      mpwd : '',
      maddr:a,
      [e.target.name]: e.target.value,      
    }

    console.log(newData)
    setData(newData)
  },[data]
);

const pwdRegExp = /^(?=.*[a-zA-Z])(?=.*[!@#$%^*+=-])(?=.*[0-9]).{8,25}$/;

const onWrite = useCallback(
  (e) => {
    e.preventDefault();
    console.log(id);
    console.log(data)
    
      if(!pwdRegExp.test(data.mpwd)&&data.mpwd!==""){
        window.alert('숫자+영문자+특수문자 조합으로 8자리 이상 입력해주세요!')
        return;
      }else if(pwdRegExp.test(data.mpwd)||data.mpwd===""){
        axios
        .post("/updateMy", data)
        .then((res)=>{
      console.log(res.data);
      if(res.data === '수정 성공'){
        window.alert('수정되었습니다.');
        sessionStorage.removeItem('myPage')
        console.log(data.mpwd)
        
        nav('/member/mypage');
        
      } else{
        window.alert("수정 실패");
        console.log(data.mpwd)
        
      }
    }).catch((err) => console.log(err));
    }    
  }, 
);

const cancle = () => {
  window.alert('취소되었습니다.')
  nav('/member/mypage');
}


// 팝업창 상태 관리
const [isPopupOpen, setIsPopupOpen] = useState(false)

// 팝업창 열기
const openPostCode = () => {
  setIsPopupOpen(true)
}

// 팝업창 닫기
const closePostCode = (v) => {
  setIsPopupOpen(false)
  console.log(v)
  //console.log(a)
  console.log(data)
    let newData = {
      ...data,
      maddr: v,  
    }

    console.log(newData)
    setData(newData)
}

  return (
    <form style={{ margin:'0 auto' ,width: '70%' }} onSubmit={()=>{onWrite()}}>
    <Stack style={{ width: '100%' }}>
      <InputGroup label="아이디">
        <Input style={{border: 0}} type="text" value={userInfo.mid} readOnly />
      </InputGroup>
      <InputGroup label="성함">
        <Input type="text" name='mname' ref={inputBoard} onClick={(e)=>borderCh(e)} onChange={(e)=>{onch(e)}} defaultValue={userInfo.mname} />
      </InputGroup>
      <InputGroup label="비밀번호">
        <Input type="password" name='mpwd' ref={inputBoard} onClick={(e)=>borderCh(e)} onChange={(e)=>{onch(e)}} />
      </InputGroup>
      <InputGroup label="이메일">
        <Input
          type="text" name='memail' ref={inputBoard} onClick={(e)=>borderCh(e)} onChange={(e)=>{onch(e)}} defaultValue={userInfo.memail} />
      </InputGroup>
      <InputGroup label="연락처">
        <Input
          type="text" name='mphone' ref={inputBoard} onClick={(e)=>borderCh(e)} onChange={(e)=>{onch(e)}} defaultValue={userInfo.mphone}  />
      </InputGroup>
      <InputGroup label="주소">
        <TextArea style={{overflow:'hidden', lineHeight:'25px', textAlign:'left'}}
          className="Input" type="text" value={a} name="maddr" 
          required defaultValue={userInfo.maddr} onClick={() => openPostCode()} ref={inputBoard}
           />
        </InputGroup>
        <InputGroup label="상세 주소">
         <Input 
            type="text" name="mdaddr" ref={inputBoard} onClick={(e)=>borderCh(e)} onChange={(e)=>{onch(e)}} defaultValue={userInfo.mdaddr}
           />
        {/* <TextArea name='maddr'  onChange={(e)=>{onch(e)}} defaultValue={userInfo.maddr}  /> */}
      </InputGroup>
      <FlexBox gap={30} style={{ width: '500px', margin: '0 auto' }}>
        <Button onClick={(e)=>{onWrite(e);} }  style={{ flex: 1 }}>수정완료</Button>
        <Button onClick={cancle} style={{ flex: 1 }}>수정취소</Button>
        {/* 클릭 시 팝업 생성 */}
      {/* 팝업 생성 기준 div */}
      <div id="popupDom">
        {isPopupOpen && (
          <PopAddDom>
            <PopAddPostCode onClose={closePostCode} setA={setA} />
          </PopAddDom>
        )}
      </div>
      </FlexBox>
    </Stack>
  </form>
  
  )
}
export default PageCorrection;
```

#### 내 정보 수정 화면<br><br>
<img width="1106" alt="정보 수정" src="https://user-images.githubusercontent.com/117880554/224945597-64e61998-427c-4cd2-8023-6e8c52715443.png">

#### 주소 api<br><br>
<img width="885" alt="주소 api" src="https://user-images.githubusercontent.com/117880554/224945831-6a3cf8bd-da33-4c87-9c87-c9d1cf70133d.png">

마이페이지 화면에서 '내 정보 수정' 버튼을 클릭했을 때 이동되는 컴포넌트입니다. Session에 저장돼 있는 로그인 아이디를 사용하여 유저의 이름, 비밀번호, 이메일, 연락처, 주소를 변경 할 수 있습니다. 주소 변경에서는 카카오 주소 api를 활용 했습니다.

## Back_MemberController 
```java
    // 마이페이지 정보수정
    @ResponseBody
    @PostMapping("updateMy")
    public String updateMy(@RequestBody Member mem){
        log.info("updateMy()");
        return  mServ.updateMy(mem);
    }
```
## Back_MemberService
```java
// 마이페이지 정보수정
    public String updateMy(Member mem) {
        log.info("updateMy()");
        Member mData = null;
        String msg =null;
        try {
            mData = mRepo.findById(mem.getMid()).get();
            log.info("ㅠㅠ" + mem.getMpwd());
            log.info("흐악ㅇㄱㅇㄱㅇ"+mem);

            if(mem.getMpwd()!="") {
                String epwd = encoder.encode(mem.getMpwd());
                mData.setMpwd(epwd);
            }
            if(mem.getMname()!="") {
                mData.setMname(mem.getMname());
            }
            if(mem.getMemail()!="") {
                mData.setMemail(mem.getMemail());
            }
            if(mem.getMphone()!="") {
                mData.setMphone(mem.getMphone());
            }
            if(mem.getMaddr()!="") {
                mData.setMaddr(mem.getMaddr());
            }
            if(mem.getMdaddr()!="") {
                mData.setMdaddr(mem.getMdaddr());
            }
//
            mRepo.save(mData);
            msg ="수정 성공";
        } catch (Exception e){
            e.printStackTrace();
            msg = "수정 실패";
        }
        return msg;
    }
```


## CommuMain.jsx 컴포넌트
※ 전체 게시판
```javascript
const CommuMain = () => {
  const df = date => moment(date).format('YYYY- MM-DD HH:mm')
    
  const nav = useNavigate()
  const mid = sessionStorage.getItem('mid')
  // const grade = sessionStorage.getItem('grade');
  let pnum = sessionStorage.getItem('pageNum')
  // let bview = sessionStorage.getItem("bview");
  const [bitem, setBitem] = useState({})
  const [page, setPage] = useState({
    totalPage: 0,
    pageNum: 1,
    btype: "",
  })

  const [bData, setBdata]=useState([]);
  useEffect(()=>{
    axios.get("/bdRank")
    .then((res)=>{
      console.log(res.data);
      setBdata(res.data);
    }).catch((err)=>
    console.log(err));
  },[])
  const {a,b,c,d,e} = bData;

    // const bn = sessionStorage.getItem('bno');
    const id = sessionStorage.getItem("mid");
    const str = sessionStorage.getItem("btitle");
    const grade = sessionStorage.getItem("admin");
    const [board, setBoard] = useState({
        bno : 0,
        btype:"",
        btitle: "",
        bmid: id,
        bstr: "",
        bview: "",
    })

  const [notice, setNotice] = useState([]);
  const [ reco, setReco ] = useState([]);
  const [ worry, setWorry ] = useState([]);
  const [ show, setShow ] = useState([]);
  const [ review, setReview ] = useState([]);

  useEffect(()=>{
  let aa=[];
  if(a!==undefined){
  for(let i=a.length-1; i>a.length-4; i--){
    if(i < 0){
      return;}
    aa.push({name: a[i].btitle, read: a[i].bview, bno:a[i].bno});
    setNotice(aa);}}
    console.log(aa)

  let bb=[];
  if(b!==undefined){
  for(let i=b.length-1; i>b.length-4; i--){
    if(i < 0){
      return;}
    bb.push({name: b[i].btitle, read: b[i].bview, bno:b[i].bno});
    setReco(bb);}}

  let ee=[];
  if(e!==undefined){
  for(let i=e.length-1; i>e.length-4; i--){
    if(i < 0){
      return;}
    ee.push({name: e[i].btitle, read: e[i].bview, bno:e[i].bno});
    setWorry(ee);}}

  let dd=[];
  if(d!==undefined){
    for(let i=d.length-1; i>d.length-4; i--){
      if(i < 0){
        return;}
    dd.push({name: d[i].btitle, read: d[i].bview, bno:d[i].bno});
    setShow(dd);}}

  let cc=[];
  if(c!==undefined){
  for(let i=c.length-1; i>c.length-4; i--){
    if(i < 0){
      return;}
    console.log(c)
    cc.push({name: c[i].btitle, read: c[i].bview, bno:c[i].bno});
    setReview(cc);}}
},[a,b,c,d,e])

const move = (ta,id) => {
  console.log(ta);
  switch(ta){
    case "notice":
      console.log(notice);
      console.log(notice[id].bno);
      localStorage.setItem('bno', notice[id].bno);
      nav('/commuBoardDetail');
      break;
    case "reco" :
      console.log(reco);
      console.log(reco[id])
      console.log(reco[id].bno);
      localStorage.setItem('bno', reco[id].bno);
      nav('/commuBoardDetail');
      break;
    case "worry" :
      console.log(worry);
      console.log(worry[id].bno);
      localStorage.setItem('bno', worry[id].bno);
      nav('/commuBoardDetail');
      break;
    case "show" :
      console.log(show);
      console.log(show[id].bno);
      localStorage.setItem('bno', show[id].bno);
      nav('/commuBoardDetail');
      break;
    case "review" :
      console.log(review);
      console.log(review[id].bno);
      localStorage.setItem('bno', review[id].bno);
      nav('/commuBoardDetail');
      break;
    
  }
}
  return (
    // <Section title=<>이시간 <h1 style={{color:"red"}}>HOT</h1></>  style={{ height: '100%' }}>
    <Section title= '커뮤니티 인기글' style={{ height: '100%' }}>
      <Table
        style={{ marginTop: 30, fontSize:'18px', fontSize:'18px' }}
        columns={[
          //배열
          {
            name: '',
            // render: (v, id) => id + 1,
            style: {
              width: 80,
            },
          },
          {
            //예시
            name: <a href="/community/commuBoardNoti">공지사항</a>,
            id: 'name',
            render:(v, id)=>(<p className="link" onClick={()=>move("notice",id)}>{v}</p>)
          },
          {
            name: <a href="/community/commuBoardNoti">+</a>,
            id: 'read',
            style: {
              width: 80,
            },
          },
        ]}
        dataSource={notice}
      ></Table>
      <div>
        <div className="table1">
          <Table
            style={{ marginTop: 30, marginRight: '50px', float: 'left', fontSize:'18px' }}
            // data-aos="fade-up"
            columns={[
              //배열
              {
                name: '',
                // render: (v, id) => id + 1,
                style: {
                  width: 80,
                },
              },
              {
                //예시
                name: <a href="/community/commuBoardReco">추천할래요</a>,
                id: 'name',
                render:(v, id)=>(<p className="link" onClick={()=>move("reco",id)}>{v}</p>)

              },
              {
                name: <a href="/community/commuBoardReco">+</a>,
                id: 'read',
                style: {
                  width: 80,
                },
              },
            ]}
            dataSource={reco}
          />

          <Table
            style={{ marginTop: 30, float: 'right' , fontSize:'18px'}}
            // data-aos="fade-up"
            columns={[
              //배열
              {
                name: '',
                // render: (v, id) => id + 1,
                style: {
                  width: 80,
                },
              },
              {
                //예시
                name: <a href="/community/commuBoardWorry">고민있어요</a>,
                id: 'name',
                render:(v, id)=>(<p className="link" onClick={()=>move("worry",id)}>{v}</p>)

              },
              {
                name: <a href="/community/commuBoardWorry">+</a>,
                id: 'read',
                style: {
                  width: 80,
                },
              },
            ]}
            dataSource={worry}
          />
        </div>
        <div className="table1" style={{ marginBottom: '20px' }}>
          <Table
            style={{ marginTop: '30px', marginRight: '50px', float: 'left', fontSize:'18px' }}
            // data-aos="fade-up"
            columns={[
              //배열
              {
                name: '',
                // render: (v, id) => id + 1,
                style: {
                  width: 80,
                },
              },
              {
                //예시
                name: <a href="/community/commuBoardShow">자랑할래요</a>,
                id: 'name',
                render:(v, id)=>(<p className="link" onClick={()=>move("show",id)}>{v}</p>)

              },
              {
                name: <a href="/community/commuBoardShow">+</a>,
                id: 'read',
                style: {
                  width: 80,
                },
              },
            ]}
            dataSource={show}
          />

          <Table
            style={{ marginTop: '30px', fontSize:'18px' }}
            // data-aos="fade-up"
            columns={[
              //배열
              {
                name: '',
                // render: (v, id) => id + 1,
                style: {
                  width: 80,
                },
              },
              {
                //예시
                name: <a href="/community/commuBoardReview">업체후기톡톡</a>,
                id: 'name',
                render:(v, id)=>(<p className="link" onClick={()=>move("review",id)}>{v}</p>)

              },
              {
                name: <a href="/community/commuBoardReview">+</a>,
                id: 'read',
                style: {
                  width: 80,
                },
              },
            ]}
            dataSource={review}
          />
        </div>
      </div>
    </Section>
  )
}

export default CommuMain
```
모든 게시판의 글들이 카테고리별로 출력되며 출력순서는 조회수 기준으로 카테고리별로 3개의 글까지 출력됩니다.

#### 전체 게시판 화면<br><br>
<img width="1106" alt="전체 게시판" src="https://user-images.githubusercontent.com/117880554/224947728-9a356b61-9d17-41cf-8991-f4a46b1bac2b.png">

## Back_BoardController
```java
    // 커뮤니티 인기글
    @GetMapping ("bdRank")
    public Map<String, List<Board>> bdRank(){
        log.info("bdRank()");
        return bServ.bdRank();
    }
```
## Back_BoardService
```java
    //커뮤니티 인기글
    public Map<String, List<Board>> bdRank() {
        log.info("bdRank");
        Map<String, List<Board>> bMap = new HashMap<>();
        try {
            bMap.put("a",bRepo.findAllByBtype("공지사항", Sort.by("bview")));
            bMap.put("b",bRepo.findAllByBtype("추천할래요", Sort.by("bview")));
            bMap.put("c",bRepo.findAllByBtype("업체후기톡톡", Sort.by("bview")));
            bMap.put("d",bRepo.findAllByBtype("자랑할래요", Sort.by("bview")));
            bMap.put("e",bRepo.findAllByBtype("고민있어요", Sort.by("bview")));
        } catch(Exception e){
            e.printStackTrace();
        }
        log.info(bMap.toString());
        return bMap;
    }
```
Sort함수를 사용해 게시글을 조회수 기준으로 정렬시켰습니다.

## CommuboardNoti.jsx 컴포넌트

※ 게시판(형식이 모두 같아서 공지사항 게시판으로 정리했습니다)

```javascript
    const CommuBoardNoti = () => {
  const { setNotiback } = useAuth();
  const df = date => moment(date).format('YYYY- MM-DD HH:mm')
  const cb = sessionStorage.setItem("cb", "공지사항");
  const grade = sessionStorage.getItem('grade');

  const nav = useNavigate()
  
  let pnum = sessionStorage.getItem('pageNum')

  const [bitem, setBitem] = useState({})
  const [page, setPage] = useState({
    totalPage: 0,
    pageNum: 1,
    btype: '공지사항',
  })

  // 게시글 목록을 서버로부터 가져오는 함수
  const getList = pnum => {
    axios
      .get('/list', { params: { pageNum: pnum, type: '공지사항' } })
      .then(res => {
        console.log(res.data)
        const { bList, totalPage, pageNum, btype } = res.data
        setPage({ totalPage: totalPage, pageNum: pageNum, btype: btype })
        // console.log(totalPage);
        setBitem(bList)
        sessionStorage.setItem('pageNum', pageNum)
      })
      .catch(err => console.log(err))
  }

  const getBoard = useCallback(bno => {
    // 보여질 게시글 번호를 localStorage에 저장(글 번호 유지)
    localStorage.setItem('bno', bno)
    nav('/commuBoardDetail')
  }, [])

  // main 페이지가 화면에 보일때 서버로부터 게시글 목록을 가져옴
  useEffect(() => {
    pnum !== null ? getList(pnum) : getList(1)
  }, [])

  // 출력할 게시글 목록 작성 
  let list = null
  if (bitem.length === 0) {
    list = (
      <CTableRow key={0}>
        <CTableColumn span={5}>게시글이 없습니다.</CTableColumn>
      </CTableRow>
    )
  } else {
    list = Object.values(bitem).map((item, i) => (
      <CTableRow key={item.bno}>
      <CTableColumn wd="w-10">{(pnum - 1)*10 + i +1}</CTableColumn>
    <CTableColumn wd="w-40">
      <div onClick={() => getBoard(item.bno)}>{item.btitle}</div>
        </CTableColumn>
        <CTableColumn wd="w-20">{item.bmid}</CTableColumn>
        <CTableColumn wd="w-20">{df(item.bdate)}</CTableColumn>
        <CTableColumn wd="w-10">{item.bview}</CTableColumn>
      </CTableRow>
    ))
  }

  // 글쓰기 화면으로 이동
  const onWrite = () => {
    const id = sessionStorage.getItem('mid')
    if (id === '' || id == null) {
      window.alert('로그인 후, 게시글을 작성하실 수 있습니다.')
    } else {
      nav('/CommuBoardWr')
    }
  }

  return (
    <div>
      <div className="Main">
        <div className="Content_table">
          <CTable hName={['No', '제목', '작성자', '날짜', '조회수']}>{list}</CTable>
          <Paging page={page} getList={getList} wd="w-20" />
          <div className="btn">
            {grade === 'admin' ? 
            <Button style={{width:'90px',height:'50px',background:'#C3B6D9', borderRadius:'10px'}} onClick={onWrite}>글쓰기</Button>: null}
          </div>
        </div>
      </div>
    </div>
  )
}

export default CommuBoardNoti
```
공지사항 게시판이 처음 열렸을 때 데이터베이스에서 type이 "공지사항"인 데이터만 가져옵니다. 일반회원과 관리자의 권한을 나누어서 관리자만 글을 작성할 수 있고, 관리자는 글쓰기 버튼이 있지만, 일반회원은 공지사항 게시판에 들어가면 글쓰기 버튼이 나타나지 않습니다.

#### 일반회원 게시판 화면<br><br>
<img width="1105" alt="공지사항 게시판" src="https://user-images.githubusercontent.com/117880554/224948518-1506e506-9872-4d4c-81d5-86d7cd9e1295.png">

#### 관리자 게시판 화면<br><br>
<img width="1106" alt="관리자 공지사항" src="https://user-images.githubusercontent.com/117880554/224949756-58adc48b-8ad3-4815-9eb7-6c8762e23504.png">

## Back_BoardController
```java
    // 커뮤니티 리스트
    @GetMapping("list")
    public Map<String, Object> getList(@RequestParam Integer pageNum,String type ,HttpSession session){
        log.info("getList()");
        log.info(""+type);
        return bServ.getBoardList(type, pageNum);
    }
```
## Back_BoardService
```java
    //커뮤니티 게시글 리스트
    public Map<String, Object> getBoardList(String type,Integer pageNum){
        log.info("getBoardList()");

        if (pageNum == null){ // 처음에 접속할때 pageNum 못넘어오게
            pageNum = 1;
        }
        int listCnt = 10; // 페이지당 보여질 게시글 갯수

        // 페이징 조건 생성
        Pageable pb = PageRequest.of((pageNum - 1), listCnt,
                Sort.Direction.DESC, "bno");

        Page<Board> result = bRepo.findByBtype(type, pb);
        List<Board> bList = result.getContent();
        int totalPage = result.getTotalPages();

        Map<String, Object> res = new HashMap<>();
        res.put("totalPage", totalPage);
        res.put("pageNum", pageNum);
        res.put("bList", bList);
        log.info(""+result.getContent());

        return res;
    }
```

## CommuBoardWr.jsx 컴포넌트
※ 게시판 작성
```javascript
const CommuBoardWr = () => {
// const CommuBoardWr = ({handleList}) => {
    const nav = useNavigate();
    
  // const titleRef = useRef();
  // const contetnRef = useRef();
  const [fileImage, setFileImage] = useState('')

  const id = sessionStorage.getItem("mid");
  const grade = sessionStorage.getItem("grade");
  const cb = sessionStorage.getItem("cb");
  console.log(cb);
  const [data, setData] = useState({
    btype: cb,
    btitle: "",
    bmid: id,
    bstr: "",
    bview: "",
  });

  useEffect(()=>{
    console.log(data);
  },[data])
  const inputBoard = useRef();
  const borderCh = (e) => {
    inputBoard.current.style.border = '1px solid lightgray';
    inputBoard.current.style.background = 'white';
    inputBoard.current = e.target
    inputBoard.current.style.border = '1px solid black';
    inputBoard.current.style.background = 'rgb(248,248,248)';
  
  }
  //전송 데이터와 파일을 담을 멀티파트 폼 생성
  let formData = new FormData();
  // const { btitle, bstr, btype,  } = data;

  //작성한 내용(글, 파일들) 전송 함수
  const onWrite = useCallback(
    (e) => {
      e.preventDefault();
      //console.log(data);
      //전송 시 파일 이외의 데이터를 폼데이터에 추가
      formData.append(
        "data",
        new Blob([JSON.stringify(data)], { type: "application/json" })
      );

      axios
        .post("/writeProc", formData, {
          headers: { "Content-Type": "multipart/form-data" },
        })
        .then((res) => {
          if (res.data === "Ok") {
            alert("작성 성공");
            sessionStorage.removeItem("pageNum");
            nav(-1);
          } else {
            alert("작성 실패");
            //formData = new FormData();
          }
        })
        .catch((error) => console.log(error));
    },
    [data]
  );
  const onChange = useCallback(
    (e) => {
      const dataObj = {
        ...data,
        [e.target.name]: e.target.value,
        bmid:id,
      };
      console.log(dataObj);
      setData(dataObj);
    },
    [data]
  );
  //console.log(data);
  //파일 선택 시 폼데이터에 파일 목록 추가(다중파일)
  const onFileChange = useCallback(
    (e) => {
      const files = e.target.files;
      console.log(files);
      for (let i = 0; i < files.length; i++) {
        setFileImage(URL.createObjectURL(e.target.files[0]))
        formData.append("files", files[i]);
      }
    },
    [formData]
  );
    const imageInput = useRef();
    const onClickImg = () => {
        imageInput.current.click();
    }
    
  const options = [
    {
      defaultLabel: '공지사항',
      value : '공지사항',
      label :'공지사항'
    },
    {
      defaultLabel: '추천할래요',
      value : '추천할래요',
      label :'추천할래요'
    },
    
    {
      defaultLabel: '고민있어요',
      value : '고민있어요',
      label :'고민있어요'
    },
    {
      defaultLabel: '자랑할래요',
      value : '자랑할래요',
      label :'자랑할래요'
    },
    {
    defaultLabel: '업체후기톡톡',
    value : '업체후기톡톡',
    label :'업체후기톡톡'
  },
  ]
  const options1 = [
    // {
    //     defaultLabel: 1,
    //     value : 1,
    //     label :'공지사항'
    // },
  {
    defaultLabel: '추천할래요',
    value : '추천할래요',
    label :'추천할래요'
  },
  
  {
    defaultLabel: '고민있어요',
    value : '고민있어요',
    label :'고민있어요'
  },
  {
    defaultLabel: '자랑할래요',
    value : '자랑할래요',
    label :'자랑할래요'
  },
  {
    defaultLabel: '업체후기톡톡',
    value : '업체후기톡톡',
    label :'업체후기톡톡'
    },
  ]
    return(
        <div>
            <Header />
        <div className="Main">
            <form className="Content" onSubmit={onWrite}>
                {/*  onSubmit={onWrite} */}
                {/* <h1>글쓰기</h1><br /> */}
               
                <div style={{marginTop:"50px", marginBottom:"30px"}}>
                   {grade === 'admin' ?(
                    <Sel defaultValue={data.btype} style={{width: "150px", height:"51px",paddingTop:'12px',paddingLeft:'20px', border:'1px solid lightgray', borderBottom:'none'}}
                    name="btype" onChange={onChange}>
                      {options.map((item)=>(
                        <option value={item.value} onChange={onChange}>{item.label}</option>
                      ))}
                    </Sel>):(
                    <Sel defaultValue={data.btype} style={{width: "150px", height:"51px",paddingTop:'12px',paddingLeft:'20px', border:'1px solid lightgray', borderBottom:'none'}}
                    name="btype" onChange={onChange}>
                      {options1.map((item)=>(
                        <option value={item.value} onChange={onChange}>{item.label}</option>
                      ))}
                    </Sel>)}
                    <input style={{width:"900px", height:"50px", borderBottom:'none'}}
                    className="Input" ref={inputBoard} onClick={(e)=>borderCh(e)}  placeholder="제목을 입력하세요." autoFocus required 
                      name="btitle" value={data.btitle} onChange={onChange}
                    />
                    <textarea style={{width: "1050px", height:"500px",}} onScroll 
                    className="Textarea" ref={inputBoard} onClick={(e)=>borderCh(e)}  placeholder="게시글을 작성하세요."
                      name="bstr" onChange={onChange} value={data.bstr} 
                    ></textarea>
                    <div>
                      {fileImage && (
                        <div>
                          <img alt="image" src={fileImage} style={{ width: '350px', height: '350px' }} />
                        </div>
                      )}
                    </div>
                    <input type="file" name = "files" multiple className="Input" accept="image/*" ref={imageInput} onChange={onFileChange}
                    style={{ display:'none',
                        width:"1000px", height:"50px", fontSize:"1rem", marginTop:"-10px", paddingLeft:"10px"
                    }} />
                    <button style={{width: '120px', height: '50px', background:'#C3B6D9',border:'1px solid #D6C7ED', color:'',borderRadius:'10px'}} type="button" className="filebtn" onClick={onClickImg}>첨부하기</button>
                </div>
                <div className="Buttons">
                    <Button  wsize="s-30" style={{marginRight:"10px",width: '120px', height: '50px', background:'#C9A3B6',borderRadius:'10px'}}>
                        작성하기
                    </Button>
                    <Button type="button" wsize="s-10" color="gray" outline onClick={() => nav(-1)}
                    style={{width: '120px', height: '50px', backgroundColor:"lightgray",borderRadius:'10px'}}>취소하기</Button>
                </div>
            </form>
        </div>
        <Footer />
        </div>
    );
}
export default CommuBoardWr;
```

#### 글 작성 화면<br><br>
<img width="1103" alt="게시글 작성" src="https://user-images.githubusercontent.com/117880554/224950287-f0615474-065a-415c-8ca0-31261a52faa5.png">


## Back_BoardController
```java
    // 커뮤니티 게시글 작성
    @PostMapping("writeProc")
    public String writeProc(@RequestPart(value = "data", required = true) Board board,
                                          @RequestPart(value = "files", required = false) List<MultipartFile> files,
                                          HttpSession session){
        log.info("writeProc()");
        board.setBmid(board.getBmid());
        log.info("보드에 아이디 넣기");
        log.info(board.getBtitle()+", "+board.getBview());
        return bServ.insertBoard(board, files, session);
    }
    
```
## Back_BoardService
```java
    // 커뮤니티 게시글 작성
    public String insertBoard(Board board, List<MultipartFile> files, HttpSession session){
        log.info("insertBoard()");
        String msg ="fail";
        log.info("Board : " + board.toString());
        try {
            bRepo.save(board);
            log.info("bno : " + board.getBno());

            if (files != null){
                log.info("files not null");
                fileUpload(files, session, board.getBno(), board.getBtype());
                log.info("files not null and fileUploading");
            }else{
                log.info("파일이 없어요");
            }

            msg = "Ok";
        } catch (Exception e){
            e.printStackTrace();
        }
        return msg;
    }
        // 게시글 작성 파일 업로드
    public void fileUpload(List<MultipartFile> files, HttpSession session, int bno, String btype)
            throws Exception{
        log.info("fileUpload()");
        // 파일 저장 위치 지정. session을 활용
        String realPath = session.getServletContext().getRealPath("/");
        log.info("realPath : " + realPath);
        // 파일 업로드용 폴더를 자동으로 생성하도록 처리
        // 업로드용 폴더 : upload
        realPath += "upload/";
        File folder = new File(realPath);
        if (folder.isDirectory() == false){ // 폴더가 없을 경우 실행
            folder.mkdir(); // 폴더 생성 메소드
        }
        for (MultipartFile mf : files){
            String orname = mf.getOriginalFilename(); // 업로드 파일명 가져오기
            if (orname.equals("")){
                // 업로드할 파일이 없음
                return; // 저장처리 중지
            }

            // 파일 정보를 저장(to filetbl)
            Files bf = new Files();
            Board board = bRepo.findByBno(bno);
            bf.setFid(board.getBno()); // 뮨제 생기면 여기임
            bf.setForiname(orname);
            String sysname = System.currentTimeMillis() +
                    orname.substring(orname.lastIndexOf("."));
            bf.setFsysname(sysname);
            bf.setFtype(btype);

            // 업로드하는 파일을 upload 폴더에 저장
            File file = new File(realPath + sysname);

            // 파일 저장(upload 폴더)
            mf.transferTo(file);

            // 파일 정보를 DB에 저장
            bfRepo.save(bf);
        }
    }
```


## Commuboardetail.jsx 컴포넌트
※ 게시판 상세보기
```javascript
const df = date => moment(date).format('YYYY-MM-DD HH:mm:ss')

const CommuBoardDetail = () => {

  const decbno = sessionStorage.getItem("bno");
  const bn = localStorage.getItem('bno')
  const id = sessionStorage.getItem('mid')
  const grade = sessionStorage.getItem('grade')

  const nav = useNavigate()

  const boardList = () => {
    nav('/commuBoardUp')
  }

  const [board, setBoard] = useState({bno:bn});

  const [flist, setFlist] = useState([
    {
      bno: '',
      fnum: 0,
      fid: 0,
      bmid: id,
      foriname: '',
      fsysname: 'Nothing',
      image: '',
      bview: '',
    },
  ])
  const [ decla, setDecla ] = useState({
    decidx: 0,
    dectype: '',
    decmid: id,
    decbmid:board.bmid,
    decbno:decbno,
  });

  useEffect(() => {
    console.log(bn) //게시글번호
    axios
      .get('/getBoard', { params: { bno: bn } })
      .then(res => {
        console.log(res.data)
        localStorage.setItem('btype', res.data.btype)
        localStorage.setItem('btitle', res.data.btitle)
        localStorage.setItem('bstr', res.data.bstr)
        localStorage.setItem('bmid', res.data.bmid)

        setBoard(res.data)

        if (res.data.bfList.length > 0) {
          let newFileList = []
          for (let i = 0; i < res.data.bfList.length; i++) {
            const newFile = {
              ...res.data.bfList[i],
              image: 'upload/' + res.data.bfList[i].fsysname,
            }
            newFileList.push(newFile)
          }
          setFlist(newFileList)
        }
      })
      .catch(err => console.log(err))
  }, [])


  const viewFlist = flist.map((v, i) => {
    return (
      <span className="Down" key={i} >
        {v.image && <img src={v.image} alt="preview-img" style={{width:'500px'}} />}
      </span>
    )
  })
  
  const deleteBoard = ()=>{
    console.log(deleteBoard);

    let confirm = window.confirm('삭제하시겠습니까?');
    if(confirm === true){
        axios
        .get('/deleteProc', {params:{bno:bn}})
        .then(res => {

            console.log(res);

            if(res.data === 'Ok'){
                window.alert("삭제되었습니다.");
                nav(-2);
            } else {
                window.alert('삭제실패하였습니다.');
            }
        })
        .catch(err => window.alert(err))
    } else{
        window.alert('취소되었습니다.');
    }
}
const [declbtn2, setDeclbtn2]= useState(false);
const decl=() => {
  if(id === board.bmid){
    window.alert('본인은 신고하실 수 없습니다.');
    return;
  }
  
  if(id === '' || id === null){
    window.alert('로그인 후, 이용가능한 서비스입니다.');
    return;
  }

    let confirm = window.confirm('신고하시겠습니까?');
    
  if(confirm === true) {
    setDecla({
      dectype: '게시글',
      decmid: id,
      decbmid:board.bmid,
      decbno:board.bno,
    })
    setDeclbtn2(true);  
  } else {
    window.alert('신고를 취소하였습니다.')
  }
}

  useEffect(()=>{
    
    if(declbtn2===true){
      axios
      .post("/declProc" , decla)
      .then((res) => {
        console.log(res.data);

        setDecla(res.data);

        if(res.data === "Ok"){
          window.alert('정상적으로 신고되었습니다.');
        }else if(res.data === "Already"){
          window.alert('이미 신고하였습니다.');
        }
        else{
          window.alert('신고에 실패하였습니다.');
        }
      })
      .catch((err) => console.log(err) );
    }
  },[declbtn2,decla])

  const [comment, setComment] = useState({
    mentstr: '',
    mentbno: bn,
    mentmid: id,
  })
  const [comList, setComList] = useState([
    {
      mentnum: 0,
      mentbno: '',
      mentdate: '',
      mentmid: id,
      mentstr: '',
    }],
  )

  const com = () => {
    console.log(comment)
    if(id == null){
        window.alert("로그인 후 작성 가능합니다.");
        return;
    }

    if(comment.mentstr === "" || comment.mentstr === null){
        window.alert("내용을 입력해주세요");
        return;
    } else{
        axios
          .post('/Bwritecomment', comment)
          .then(res => {
            console.log(res.data)
    
            const Obj = {
              mentnum: 0,
              mentstr: '',
              mentbno: bn,
              mentmid: id,
            }
            setComment(Obj)
            comList.push(res.data)
            window.alert("작성되었습니다.");
            delwrite.current.value="";
            console.log(res.data);
          })
          .catch(err => console.log(err))
    }
}
const { setNotiBack, notiBack, setRecoBack, recoBack, 
  setReviewBack, reviewBack, setShowBack, showBack, setWorryBack, worryBack } = useAuth()


const onch = e => {
  delwrite.current=e.target;
  const Obj = {
    ...comment,
    [e.target.name]: e.target.value,
  } 
  setComment(Obj)
  console.log(comment);
}
const move=(type)=>{
  console.log(type);
  switch(type){
    case "공지사항":
      nav("/community/commuBoardNoti");
      break;
      case "추천할래요":
      nav("/community/commuBoardReco");
      break;
      case "고민있어요":
      nav("/community/commuBoardWorry");
      break;
      case "자랑할래요":
      nav("/community/commuBoardShow");
      break;
      case "업체후기톡톡":
      nav("/community/commuBoardReview");
      break;
  }
}
const delwrite = useRef();
  return (
    <div>
      <Header />
      <EstimateBanner text="community" />
      <Section title="">
        <div className="Main">
          <form className="Content_table">
            <div style={{ marginTop: '50px', marginBottom: '30px' }}>
              <input className="Input inputTitle" readOnly value={board.btitle}></input>
              <div className="divBoard divBdInfo">
                <div>
                  <span>NO.&emsp;{board.bno}</span>
                </div>
                <span>작성자&emsp;{board.bmid}</span>
                <span>작성일&emsp;{df(board.bdate)}</span>
                <span>조회수&emsp;{board.bview}&emsp;</span>
              </div>
              <div className="Box">
                <div style={{marginTop:'30px'}} className="FileData">{viewFlist}</div>
              </div>
              <textarea style={{border:'none', height:'500px'}}
                onScroll readOnly className="Textarea TextStr" placeholder="내용" value={board.bstr} >
              </textarea>
              
            </div>
           
            <div className="divbtn" style={{  display:'flex'}}>
               {id===""||id===undefined||id===null ? null: board.bmid !== id || grade === "admin" ? (
              <Button type='button' onClick={()=>decl()} style={{ opacity:'90%', background:'#E63535', borderRadius:'100px', width: '120px', height: '50px' }}>🚨 신고하기</Button> 
              ): <div />}
              <div>{board.bmid === id || grade === "admin" ? (
                <Button type="button" onClick={boardList} 
                style={{ width: '120px', height: '50px',background:'#C9A3B6' ,borderRadius:'10px', marginRight:'10px'}}>글수정</Button> ) : null}
                {board.bmid === id || grade ==="admin" ? (
                <Button type="button" onClick={()=>{deleteBoard(); move(board.btype)}} style={{ width: '120px', height: '50px', background: 'lightgray',borderRadius:'10px' }}>
                    삭제하기</Button>): null}
              </div>
            </div>
            <div
              style={{ display: 'flex', justifyContent: 'center', lineHeight:'50px',width: '100%', marginTop: '30px'}}>
              <Button type="button" onClick={() => move(board.btype)} style={{ width: '120px', height: '50px', background:'#C9A3B6' ,borderRadius:'10px' }}>
                목록
              </Button>
            </div>
          </form>
          <form className="">
            <div style={{ marginTop: '50px', display: 'flex', marginLeft:'50px', }}>
              <input className="inputdiv inputWrBtn" ref={delwrite} placeholder="댓글을 입력하세요." name="mentstr"
                 onChange={onch}></input>
                <Button className='wtBtn' type="button" onClick={com} 
                style={{   width: '150px', height: '90px', background:'#C9A3B6', borderTopRightRadius:'15px', borderBottomRightRadius:'15px',}}>
                작성하기
                </Button>
          </div>
          </form>
      </div>
        <DetailReple comment={comment} setComment={setComment} comList={comList} setComList={setComList}/>
      </Section>
      <Footer />
    </div>
  )
}
export default CommuBoardDetail
```
게시글 화면에서 글 제목을 클릭했을 때 이동되는 상세페이지 컴포넌트입니다. 클릭한 글의 번호를 localStorage에 저장 후 해당하는 글의 상세페이지로 이동합니다. 상세 페이지에서는 댓글달기, 글 수정하기(작성자와 관리자만), 글 삭제하기(작성자와 관리자만), 글 신고하기를 할 수 있습니다.

#### 공지사항 상세보기 출력 화면 <br><br>
<img width="436" alt="게시글 디테일" src="https://user-images.githubusercontent.com/117880554/224950994-0ce411ee-6c73-4a31-8aa8-b3b3feea558f.png">

## Back_BoardController
```java
    @GetMapping("getBoard")
    public Board getBoard(@RequestParam int bno){
        log.info("getBoard() bno:" + bno);
        Board board = bServ.getBoard(bno);
        log.info(board.toString());
        return board;
    }
```
## Back_BoardService
```java
    public Board getBoard(int bno){
        log.info("getBoard()");
        Board board = new Board();
        try{
            // 게시글 담기
            board = bRepo.findByBno(bno);
            board = bRepo.findById(bno).get();
            int view = board.getBview();
            board.setBview(view +1);
            bRepo.save(board);

            log.info("board collecting");
        }catch (Exception e){
            log.info("board Collecting Fail");
            e.printStackTrace();
    }
```


## CommuBoardUp.jsx 컴포넌트
※ 게시판 
```javascript
const CommuBoardUp = () => {
// const CommuBoardWr = ({handleList}) => {
    const nav = useNavigate();
    
  // const titleRef = useRef();
  // const contetnRef = useRef();

//   const da = localStorage.getItem("bdate");
  const bti = localStorage.getItem("btitle");
  const grade = sessionStorage.getItem("grade");
  const bs = localStorage.getItem("bstr");
  const cb = sessionStorage.getItem("cb");

  const [data, setData] = useState({
    // bno:bno,
    btype:cb,
    // bdate: da,
    btitle: bti,
    bstr: bs,
  });
  const bn = localStorage.getItem("bno");

  const inputBoard = useRef();
const borderCh = (e) => {
  inputBoard.current.style.border = '1px solid lightgray';
  inputBoard.current.style.background = 'white';
  inputBoard.current = e.target
  inputBoard.current.style.border = '1px solid black';
  inputBoard.current.style.background = 'rgb(248,248,248)';

}


  //전송 데이터와 파일을 담을 멀티파트 폼 생성
  let formData = new FormData();
  // const { btitle, bstr, btype } = data;

  //작성한 내용(글, 파일들) 전송 함수
  const onWrite = useCallback(
    (e) => {
      e.preventDefault();
      //console.log(data);
      //전송 시 파일 이외의 데이터를 폼데이터에 추가
      formData.append(
        "data",
        new Blob([JSON.stringify(data)], { type: "application/json" })
      );

      axios
        .post("/updateProc", formData, {params:{bno:bn}}, {
          headers: { "Content-Type": "multipart/form-data" },
        })
        .then((res) => {
          if (res.data === "Ok") {
            alert("수정 성공");
            sessionStorage.removeItem("pageNum");
            nav(-1);
          } else {
            alert("수정 실패");
            //formData = new FormData();
          }
        })
        .catch((error) => console.log(error));
    },
    [data]
  );
  const onChange = useCallback(
    (e) => {
      const dataObj = {
        ...data,
        [e.target.name]: e.target.value,
      };
      //console.log(dataObj);
      setData(dataObj);
      console.log(dataObj);
    },
    [data]
  );
  //console.log(data);
  //파일 선택 시 폼데이터에 파일 목록 추가(다중파일)
  const onFileChange = useCallback(
    (e) => {
      const files = e.target.files;
      //console.log(files);
      for (let i = 0; i < files.length; i++) {
        formData.append("files", files[i]);
      }
    },
    [formData]
  );
    const imageInput = useRef();
    const onClickImg = () => {
        imageInput.current.click();
    }
    
    const options = [
      {
          defaultLabel: '공지사항',
          value : '공지사항',
          label :'공지사항'
      },
      {
        defaultLabel: '추천할래요',
        value : '추천할래요',
        label :'추천할래요'
      },
      
      {
        defaultLabel: '고민있어요',
        value : '고민있어요',
        label :'고민있어요'
      },
      {
        defaultLabel: '자랑할래요',
        value : '자랑할래요',
        label :'자랑할래요'
      },
      {
        defaultLabel: '업체후기톡톡',
        value : '업체후기톡톡',
        label :'업체후기톡톡'
        },
    ]
    const options1 = [
      // {
      //     defaultLabel: 1,
      //     value : 1,
      //     label :'공지사항'
      // },
    {
      defaultLabel: '추천할래요',
      value : '추천할래요',
      label :'추천할래요'
    },
    
    {
      defaultLabel: '고민있어요',
      value : '고민있어요',
      label :'고민있어요'
    },
    {
      defaultLabel: '자랑할래요',
      value : '자랑할래요',
      label :'자랑할래요'
    },
    {
      defaultLabel: '업체후기톡톡',
      value : '업체후기톡톡',
      label :'업체후기톡톡'
      },
    ]
    return(
        <div>
            <Header />
        <div className="Main">
            <form className="Content" onSubmit={onWrite}>
                {/*  onSubmit={onWrite} */}
                {/* <h1>글쓰기</h1><br /> */}
                <div style={{marginTop:"50px", marginBottom:"30px"}}>
                   {grade === 'admin' ?(
                    <Sel defaultValue={data.btype} style={{width: "150px", height:"51px",paddingTop:'11px',paddingLeft:'20px', border:'1px solid lightgray', borderBottom:'none'}}
                    name="btype" onChange={onChange}>
                      {options.map((item)=>(
                        <option value={item.value} onChange={onChange}>{item.label}</option>
                      ))}
                    </Sel>):(
                    <Sel defaultValue={data.btype} style={{width: "150px", height:"51px",paddingTop:'11px',paddingLeft:'20px', border:'1px solid lightgray', borderBottom:'none'}}
                    name="btype" onChange={onChange}>
                      {options1.map((item)=>(
                        <option value={item.value} onChange={onChange}>{item.label}</option>
                      ))}
                    </Sel>)}
                    <input style={{width:"900px", height:"50px", borderBottom:'none'}}
                    className="Input" ref={inputBoard} onClick={(e)=>borderCh(e)} placeholder="제목을 입력하세요." autoFocus required 
                      name="btitle" value={data.btitle} onChange={onChange}
                    />
                    <textarea style={{width: "1050px", height:"500px",}} onScroll 
                    className="Textarea" ref={inputBoard} onClick={(e)=>borderCh(e)} placeholder="게시글을 작성하세요."
                      name="bstr" onChange={onChange} value={data.bstr} 
                    ></textarea>
                    {/* <input className="Input" type="file" name="files" onChange={onFileChange} multiple /> */}
                    <input type="file" name = "files" multiple className="Input" ref={imageInput} onChange={onFileChange}
                    style={{ display:"none",
                        width:"1000px", height:"50px", fontSize:"1rem", marginTop:"-10px", paddingLeft:"10px"
                    }} />
                    <button style={{width: '120px', height: '50px', background:'#C3B6D9',border:'1px solid #D6C7ED', color:'',borderRadius:'10px'}} type="button" className="filebtn" onClick={onClickImg}>첨부하기</button>
                </div>
                <div className="Buttons">
                    <Button wsize="s-30" style={{marginRight:"10px",width: '120px', height: '50px', background:'#C9A3B6',borderRadius:'10px'}}>
                        수정하기
                    </Button>
                    <Button type="button" wsize="s-10" color="gray" outline onClick={() => nav(-1)}
                    style={{width: '120px', height: '50px', backgroundColor:"lightgray",borderRadius:'10px'}}>취소하기</Button>
                </div>
            </form>
        </div>
        <Footer />
        </div>
    );
}
export default CommuBoardUp;
```

#### 공지사항 수정 화면 <br><br>
<img width="539" alt="게시판 수정" src="https://user-images.githubusercontent.com/117880554/224952302-ba84e866-8c8f-44c4-b58d-9a72b0969403.png">

## Back_BoardController
```java
    // 게시글 수정 페이지로 전환
    @PostMapping("updateProc")
    public String updateProc(@RequestPart(value = "files", required = false) List<MultipartFile> files,  HttpSession session,
                             int bno, @RequestPart(value = "data", required = true) Board board){
        log.info("updateProc()");
        log.info("글번호 : "+bno);
        log.info("제목 : " + board.getBtitle());
        String msg = bServ.boardUpdate(files, session, bno, board);
        return msg;
    }
```
## Back_BoardService
```java
    // 커뮤니티 게시글 수정
    @Transactional
    public String boardUpdate(List<MultipartFile> files, HttpSession session, int bno, Board board) {
        log.info("boardUpdate()");
        String msg = null;
        try {
            Board bData = bRepo.findByBno(bno);
            bData.setBtitle(board.getBtitle());
            bData.setBstr(board.getBstr());
            bData.setBtype(board.getBtype());
            bRepo.save(bData);
//            bRepo.findByBno(board.getBno());
            if (files != null){
                log.info("files not null");
                fileUpload(files, session, bno, board.getBtype());
                log.info("files not null and fileUploading");
            }else{
                log.info("파일이 없어요");
            }
            msg = "Ok";
        } catch (Exception e) {
            e.printStackTrace();
            msg = "수정 실패";
        }
        return msg;
    }
```

## CommuBoardDetail.jsx 컴포넌트
※ 게시판 삭제
```javascript
const deleteBoard = ()=>{
    console.log(deleteBoard);

    let confirm = window.confirm('삭제하시겠습니까?');
    if(confirm === true){
        axios
        .get('/deleteProc', {params:{bno:bn}})
        .then(res => {

            console.log(res);

            if(res.data === 'Ok'){
                window.alert("삭제되었습니다.");
                nav(-2);
            } else {
                window.alert('삭제실패하였습니다.');
            }
        })
        .catch(err => window.alert(err))
    } else{
        window.alert('취소되었습니다.');
    }
}
```

#### 공지사항 삭제 화면 <br><br>
<img width="506" alt="게시글 삭제" src="https://user-images.githubusercontent.com/117880554/224956224-b94f4b7a-5806-4f19-bbaa-7326478bf698.png">


## Back_BoardController
```java
    // 게시글 삭제
    @GetMapping("deleteProc")
    public String deleteProc(@RequestParam int bno, HttpSession session){
        log.info("deleteProc()");
        log.info("보드"+bno);
        return bServ.deleteBoard(bno, session);
    }
```
## Back_BoardService
```java
    // 게시글 삭제
    @Transactional
    public String deleteBoard(int bno, HttpSession session) {
        log.info("deleteBoard()");
        String msg = null;
//        Board board = new Board();
//        board.setBno(bno);
//        board.setBno(board.getBno());

        log.info("ㅠㅜㅠㅜㅠㅜ:" + bno);

        String realPath = session.getServletContext().getRealPath("/");
        realPath += "upload/";

        List<Files> bfList = bfRepo.findByFid(bno);
        try {
            // 파일삭제
            for (Files bf : bfList){
                realPath += bf.getFsysname();
                File file = new File(realPath);

                if (file.exists()){
                    file.delete();
                }
                // 파일 정보 삭제
                fRepo.deleteByFid(bf.getFid());
            }
            // 댓글삭제
            cRepo.deleteByMentbno(bno);
            // 게시글 삭제
            bRepo.deleteById(bno);

            msg = "Ok";
        } catch (Exception e){
            e.printStackTrace();
            msg = "fail";
        }

        return msg;
    }
```

## JoinModal.jsx 컴포넌트

※ 회원가입
```javascript

const JoinModal = ( props ) => {
    const nav = useNavigate();
    const [bb, setBb] = useState(false);
    const modalRef = useRef(null);
    const [cfBtn, setCfBtn] = useState(false);
    const [test, setTest] = useState({})
    const [a, setA] = useState("");
    const [b, setB] = useState(false);
    const [p1, setP1] = useState("");
    const [p2, setP2] = useState("");
    const [p3, setP3] = useState("");
    const [r1, setR1] = useState("");
    const [r2, setR2] = useState("");
    const reftest = useRef();
    const [account, setAccount] = useState(
        {
        }
        )
        useEffect(()=>{
            axios.get("/compareId", {params:{mid:account.mid}})
            .then((res)=>{
                setTest({...test,
                fi:res.data});
            })
        },[account.mid]);


        //input에 입력될 때마다 account state값이 변경되게 하는 함수
    const onChangeAccount = (e) => {
        console.log(e.target.value+"asdsadadsda")
        console.log(test)
    if(e.target.name=="p1"){
        setP1(e.target.value);
    }
    if(e.target.name=="p2"){
        setP2(e.target.value);
    }
    if(e.target.name=="p3"){
        setP3(e.target.value);
    }
    if(e.target.name=="r1"){
        setR1(e.target.value);
    }
    if(e.target.name=="r2"){
        setR2(e.target.value);
    }

    const r = r1 + r2
    const p = p1 + p2 + p3;
    const addr = a
            setAccount({
                ...account,
            [e.target.name]: e.target.value,
            mpid : r,
            mphone: p,
            maddr: addr
        });

        // const joinIn=document.getElementById("joinIn");
        // if(a!= "" && b!= false){
        //     joinIn.disabled=false;
        // } else{
        //     joinIn.disabled=true;
        // }
        // if((account.mid&&account.mpwd&&account.mname&&account.mpid&&account.maddr&&account.mphone&&account.memail)!=""){
        //     joinIn.disabled=false;
        //     joinIn.style.background="black"
        // }
}


    const jbtn = () => {
        axios.post("/joinProc", account)
        .then((res) => {
            console.log(res);
            window.alert("이랏샤이마세 👏");
            props.setMymodal(false);
            setAccount({});
        }).catch(err => console.log(err))
    }


    // 팝업창 상태 관리
    const [isPopupOpen, setIsPopupOpen] = useState(false);

    useEffect(() => {
        // 이벤트 핸들러 함수
        if(isPopupOpen===true||bb===true){
            return;
        }
        const handler = (event) => {
            // mousedown 이벤트가 발생한 영역이 모달창이 아닐 때, 모달창 제거 처리
            if (!modalRef.current.contains(event.target)) {
                props.setMymodal(false);
                const scrollY = document.body.style.top;
                document.body.style.cssText = '';
                window.scrollTo(0, parseInt(scrollY || '0', 10) * -1);}
        };

        document.addEventListener('mousedown', handler);
        
        return () => {
            document.removeEventListener('mousedown', handler);
        };
    });

    
    // 팝업창 열기
    const openPostCode = () => {
        setIsPopupOpen(true)
    }
    
    // 팝업창 닫기
    const closePostCode = () => {
        setIsPopupOpen(false)
    }
    
    useEffect(()=>{
        console.log(reftest.current);
        let id1 = document.getElementById("checkId");
        let idresult = document.getElementById("idresult");
        const idRegExp = /^(?=.*[a-zA-Z][0-9])[^!@#$%^*+=-]{4,12}$/;
        let pwd1 = document.getElementById("pwd1");
        let pwd2 = document.getElementById("pwd2");
        let pwdresult = document.getElementById("pwdresult");
        let cresult = document.getElementById("cresult");
        const pwdRegExp = /^(?=.*[a-zA-Z])(?=.*[!@#$%^*+=-])(?=.*[0-9]).{8,25}$/;
        if(reftest.current===id1){
        if(account.mid===""||account.mid===undefined){
            idresult.style.display="none";
        } else if (!idRegExp.test(account.mid)) {
            setTest({...test, ai:0});
            idresult.innerHTML="대소문자 또는 숫자 조합으로 4-12자리 입력해 주세요!";
            idresult.style.display="block";
            idresult.style.color="red";
        }else if(test.fi==="Failed"){
            console.log("이걸봐"+test.fi);
            setTest({...test, ai:0});
            idresult.innerHTML="중복된 아이디 입니다.";
            idresult.style.display="block";
            idresult.style.color="red";
            console.log(test.ai)
        }else if(idRegExp.test(account.mid)&&test.fi==="Ok") {
            console.log("이걸봐"+test.fi);
            setTest({...test, ai:1});
            idresult.innerHTML="사용가능한 아이디 입니다.";
            idresult.style.display="block";
            idresult.style.color="limeGreen";
            console.log("할렐루야")
        }}

        if(reftest.current===pwd1){
        if(pwd1.value == "" || pwd1.value===undefined){
            pwdresult.style.display="none";
            setTest({...test,bi:0});
        } else if(!pwdRegExp.test(pwd1.value)){
            pwdresult.innerHTML="숫자+영문자+특수문자 조합으로 8자리 이상 입력해주세요!"
            pwdresult.style.display="block";
            pwdresult.style.color="red";
            console.log("asddsa")
            setTest({...test, bi:0});
        }  else if(pwdRegExp.test(pwd1.value)) {
            pwdresult.innerHTML=("안전한 비밀번호 입니다.");
            pwdresult.style.display="block";
            pwdresult.style.color="limeGreen";
            setTest({...test, bi:1});
        }
    }
        if(reftest.current===pwd2){   
            if(pwd1.value == "" || pwd2.value==""){
            cresult.style.display="none";
            setTest({...test,ci:0});;
        }else if(pwd1.value==pwd2.value){
            cresult.style.display="block";
            cresult.style.color="limeGreen";
            cresult.innerHTML="비밀번호가 일치합니다.";
            setTest({...test,ci:1});;
        } else{
            cresult.style.display="block";
            cresult.style.color="red";
            cresult.innerHTML="비밀번호가 일치하지않습니다."
            setTest({...test,ci:0});;
        }
    }

    // const regName = () => {
        const nameCheck=document.getElementById("nameCheck");
        if(reftest.current===nameCheck){ 
            const nameRegExp = /^[a-zA-zㄱ-ㅎ|ㅏ-ㅣ|가-힣]{0,12}$/;
            if(!nameRegExp.test(nameCheck.value)){
                nameCheck.value="";
                alert("한글 또는 영어 12자 이하로 입력해주세요")
            }
        }
    // }

    // const regRno = () => {
        const rnoCheck1=document.getElementById("rnoCheck1");
        const rnoCheck2=document.getElementById("rnoCheck2");
        if(reftest.current===rnoCheck1||reftest.current===rnoCheck2){ 
            const rnoRegExp = /^[0-9]{0,7}$/;
            const rnoRegExp2 = /^[0-9]{6}$/;
            const rnoRegExp3 = /^[0-9]{7}$/;

        if(!rnoRegExp.test(rnoCheck1.value)){
            rnoCheck1.value="";
            alert("숫자만 입력해주세요.")
        }
        if(!rnoRegExp.test(rnoCheck2.value)){
            rnoCheck2.value="";
            alert("숫자만 입력해주세요.")
        }

        if(rnoRegExp2.test(rnoCheck1.value)&&rnoRegExp3.test(rnoCheck2.value)){
            setTest({...test,
                ei:1
            })
        }else{
            setTest({...test,
                ei:0
            })
        }
    }
    // }
    // const regPno = () => {
        const pnoCheck1=document.getElementById("pnoCheck1");
        const pnoCheck2=document.getElementById("pnoCheck2");
        const pnoCheck3=document.getElementById("pnoCheck3");
        if(reftest.current===pnoCheck1 ||reftest.current===pnoCheck2 ||reftest.current===pnoCheck3){ 
        const pnoRegExp = /^[0-9]{0,4}$/;
        const pnoRegExp2 = /^[0-9]{3}$/;
        const pnoRegExp3 = /^[0-9]{4}$/;


        if(!pnoRegExp.test(pnoCheck1.value)){
            pnoCheck1.value="";
            alert("숫자만 입력해주세요.")
        }
        if(!pnoRegExp.test(pnoCheck2.value)){
            pnoCheck2.value="";
            alert("숫자만 입력해주세요.")
        }
        if(!pnoRegExp.test(pnoCheck3.value)){
            pnoCheck3.value="";
            alert("숫자만 입력해주세요.")
        }

        if(pnoRegExp2.test(pnoCheck1.value)&&pnoRegExp3.test(pnoCheck2.value)&&pnoRegExp3.test(pnoCheck3.value)){
            setTest({...test,
                di:1
            })
        }else{
            setTest({...test,
                di:0
            })
            setB(false);
        }
    }
    
    const myemail = document.getElementById("myE");
    if(reftest.current===myemail){
            console.log('이거다아아')
            const emailRegExp = /^[a-zA-Z0-9+-\_.]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$/
            if(emailRegExp.test(myemail.value)){
                setTest({...test,
                    gi:1
                })
            } else{
                setTest({...test,
                    gi:0
                })
            }
        }
    
        const addr2 = document.getElementById("addr2");
        if(reftest.current===addr2){
            console.log(addr2.value);
            if(addr2.value===""||addr2.value===undefined){
                setTest({...test,
                    hi:0
                })
            } else{
                setTest({...test,
                    hi:1
                })
            }
        }
    
    },[account.mid,account.mpwd,account.mpwd2,account.mpid, account.mname ,account.mphone, account.maddr, account.mdaddr,account.memail ,test.fi])
    console.log(test)
    const click= (e) => {
        reftest.current = e.target;
        console.log(reftest.current)
    }
    return (
        <div className="JoinModal">
           <div ref={modalRef} className="JoinContainer">
               <section className="user-input">
                   <div className="jtx"><Logo>Wedding Dive<br/> Join</Logo></div>
                   <hr className="jhr"/>
                   <form>
                   <div className="jinput-container">
                   <div className="join-title">아이디</div>
                   <input className="input-basic" id="checkId" type="text" required placeholder="아이디를 입력하세요." name="mid" ref={reftest} onClick={(e)=>click(e)} onChange={(e)=> { onChangeAccount(e); click(e)}} autoFocus/>
                   </div>
                   <div id="idresult" style={{display:"none", color:"red", textIndent:"0%", textAlign:"left" , paddingBottom:"15px",lineHeight:"0px" , marginLeft:"210px"}}></div>
                   <div className="jinput-container">
                   <div className="join-title">비밀번호</div>
                   <input className="input-basic" id="pwd1" type="password" required placeholder="비밀번호를 입력하세요." name="mpwd"ref={reftest} onClick={(e)=>click(e)} onChange={(e)=>{ onChangeAccount(e); click(e)}} />
                   </div>
                   <div id="pwdresult" style={{display:"none", color:"red", textIndent:"0%", textAlign:"left" ,paddingBottom:"15px",lineHeight:"0px" , marginLeft:"210px"}}></div>
                   <div className="jinput-container">
                   <div className="join-title">비밀번호 <br/>재확인</div>
                   <input className="input-basic" id="pwd2" name="mpwd2" type="password" required placeholder="비밀번호를 입력하세요. " ref={reftest} onClick={(e)=>click(e)}  onChange={(e)=>{ onChangeAccount(e); click(e)}}/>
                   </div>
                   <div id="cresult" style={{display:"none", color:"red", textIndent:"0%", textAlign:"left" , paddingBottom:"15px",lineHeight:"0px" , marginLeft:"210px"}}></div>
                   <div className="jinput-container">
                   <div className="join-title">이름</div>
                   <input className="input-basic" id="nameCheck" type="text" required placeholder="이름을 입력하세요." name="mname" ref={reftest} onClick={(e)=>click(e)} onChange={(e) => {onChangeAccount(e); click(e)}}/>
                   </div>
                   <div className="jinput-container">
                   <div className="join-title">주민번호</div>
                        <div style={{width:"350px"}}>
                            <input className="mtrno" id="rnoCheck1" type="text" maxLength="6" minLength="6" required placeholder="950618" name="r1" ref={reftest} onClick={(e)=>click(e)} onChange={(e) => {onChangeAccount(e); click(e)}}/><span style={{margin:"0 2%"}}>-</span>
                            <input className="mtrno" id="rnoCheck2" type="password" maxLength="7" minLength="7" required placeholder="1xxxxxx" name="r2" ref={reftest} onClick={(e)=>click(e)} onChange={(e) =>{onChangeAccount(e); click(e)}}/>
                        </div>
                   </div>
                   <div className="jinput-container">
                   <div className="join-title">주소</div>
                   <input className="input-basic" type="text" value={a} name="maddr" readOnly required placeholder="주소를 입력하세요." onClick={() => openPostCode()}/>
                   </div>
                   <div className="jinput-container">
                   <div className="join-title">상세주소</div>
                   <input className="input-basic" type="text" id="addr2" name="mdaddr" required placeholder="상세주소를 입력하세요."ref={reftest} onClick={(e)=>click(e)} onChange={(e)=>{onChangeAccount(e); click(e)}}/>
                   </div>
                   <div className="jinput-container">
                   <div className="join-title">핸드폰 <br/>번호</div>
                   <span className="phone-container">
                    { b === false ? <>
                   <input className="phone-box" id="pnoCheck1" type="text" minLength="2" maxLength="3" required placeholder="010" name="p1" ref={reftest} onClick={(e)=>click(e)} onChange={(e) =>{onChangeAccount(e); click(e)}}/><span className="phonew">-</span>
                   <input className="phone-box" id="pnoCheck2" type="text" minLength="4" maxLength="4" required placeholder="0000" name="p2"ref={reftest} onClick={(e)=>click(e)}  onChange={(e) =>{onChangeAccount(e); click(e)}}/><span className="phonew">-</span>
                   <input className="phone-box" id="pnoCheck3" type="text" minLength="4" maxLength="4" required placeholder="0000" name="p3" ref={reftest} onClick={(e)=>click(e)} onChange={(e) =>{onChangeAccount(e); click(e)}}/></> :  <>
                   <input className="phone-box" id="pnoCheck1" type="text" minLength="2" maxLength="3" required placeholder="010" name="p1" disabled onChange={(e) =>{onChangeAccount(e); click(e)}}/><span className="phonew">-</span>
                   <input className="phone-box" id="pnoCheck2" type="text" minLength="4" maxLength="4" required placeholder="0000" name="p2" disabled  onChange={(e) =>{onChangeAccount(e); click(e)}}/><span className="phonew">-</span>
                   <input className="phone-box" id="pnoCheck3" type="text" minLength="4" maxLength="4" required placeholder="0000" name="p3" disabled  onChange={(e) =>{onChangeAccount(e); click(e)}}/></> }
                   { test.di ===1 ?
                   <PhoneConfirm opacity={1} background={'#C3B6D9'} setB={setB} setBb={setBb} account={account} p1={p1} p2={p2} p3={p3} /> : <PhoneConfirm background={"#C3B6D9"} opacity={0.7} setB={setB} disabled={true} />}
                   </span>
                   </div>
                   <div className="jinput-container">
                   <div className="join-title">이메일</div>
                   <input className="input-basic" id="myE" type="email" name="memail" required placeholder="@이메일주소를 입력하세요." ref={reftest} onChange={(e)=>{onChangeAccount(e); click(e)}}/>
                   </div>
                   {account.mid!==""&&account.mpwd!==""&&account.mname!==""&&account.mpid!==""&&account.maddr!==""&&account.mphone!==""&&account.memail!==""&&a!==""&&b!==false&&test.bi===1&&test.ci===1&&test.di===1&&test.ei===1&&test.gi===1&&test.hi===1 ?
                   <button type="button" className="join-btn" id="joinIn" style={{background:"#C9A3B6"}} onClick={jbtn}>회원가입</button> : <button type="button" className="join-btn" id="joinIn" style={{background:"#C9A3B6", opacity:"0.7"}} disabled>회원가입</button>}
                    { props.mymodal ? <button className="join-btn-del" style={{background:"lightgray"}} onClick={()=>props.setMymodal(false)}>취소하기</button>:<button className="join-btn-del" style={{background:"lightgray"}} onClick={() =>props.setSelectJoin(false)}>돌아가기</button>}
               </form>
               </section>
               <div>
                </div>
                </div>
                    {/* 클릭 시 팝업 생성 */}
                    {/* 팝업 생성 기준 div */}
                    <div id='popupDom'>
                        {isPopupOpen && (
                            <PopAddDom>
                                <PopAddPostCode onClose={closePostCode} setA={setA} />
                            </PopAddDom>
                        )}
                </div>
        <div>
    </div>
</div>         
    );
}

export default JoinModal;
```
정규화를 통해 회원가입 양식을 만들었고, 필수 입력사항들을 입력하지 않으면 회원가입 버튼이 비 활성화 됩니다. 주소입력란은 카카오 api를 사용했고 핸드폰 인증란은 아임포트 휴대폰 인증 api를 사용하였숩니다. 입력한 휴대폰번호와 이름이 휴대폰 인증 모듈에 전달되고 인증 완료 후에 휴대폰 번호 혹은 이름을 바꾸면 인증 내역이 해제됩니다. 

#### 회원가입 화면<br><br>
<img width="1106" alt="회원가입 창" src="https://user-images.githubusercontent.com/117880554/224960470-6422cb4c-b872-4306-9f20-07694167a144.png">

#### 회원가입 정규화 화면<br><br>
<img width="396" alt="회원가입 정규화" src="https://user-images.githubusercontent.com/117880554/224960500-9b380d1e-ee1a-41c5-b0c3-8c5d19226171.png">
#### 회원가입 정규화 화면 1<br><br>
<img width="391" alt="회원가입 정규화 2" src="https://user-images.githubusercontent.com/117880554/224960529-9bb817a8-0f33-4f63-814e-ba8a6e8e367e.png">

#### 카카오 주소 api<br><br>
<img width="331" alt="주소 api2" src="https://user-images.githubusercontent.com/117880554/224960551-82bdaaeb-0ab8-4192-8dc2-1ff98b7e0554.png">

#### 아임포트 휴대폰 인증 api<br><br>
<img width="263" alt="휴대폰 인증" src="https://user-images.githubusercontent.com/117880554/224962492-32715b7e-ad68-4e9d-9c8e-31fd7c0a5eab.png">

#### 회원가입 성공 화면<br><br>
<img width="1106" alt="회원가입 성공" src="https://user-images.githubusercontent.com/117880554/224960570-127339e2-a366-471f-9753-aa317337fc72.png">



## Back_MemberController
```java
    @PostMapping("/joinProc")
    public String joinProc(@RequestBody Member member){
        log.info("joinProc()");
        String res = mServ.joinMember(member);
        return res;
    }
```
## Back_MemberService
```java
    @Transactional
    public String joinMember(Member member) {
        log.info("joinMember()");
        String res = null;

        String epwd = encoder.encode(member.getMpwd());
        member.setMpwd(epwd);
        try{
            if(member.getMid()!=""){
            mRepo.save(member);
            res="ok";}else{res="아이디를입력하세요";}
        }catch(Exception e){
            e.printStackTrace();
            res="failed";
        }
        return res;
    };
```


마치며
---
#### 소감<br><br>
프로젝트를 시작하기 전 리액트를 3~4일 정도만 배웠어서 코드 자체가 번잡한 부분이 많습니다. 앞으로 더 열심히 해서 점점 나아지는 모습 기대해주세요. 이 프로젝트는 저에게는 화합의 중요성과 자기발전 등 많은 경험이 되었고, 저의 부족한 부분과 제가 할 수 있는 부분을 구별할 수 있었고, 더욱 성장하는 발판이 되었습니다. 그렇기에 부족한 부분은 더 공부하고, 할 수 있는 부분은 더 전문적이고 발전할수 있도록 항상 노력하겠습니다. 감사합니다.
